# Practice Problems: Introduction to AI-Powered Data Engineering

**Module:** Introduction to AI-Powered Data Engineering  
**Estimated Time:** 25-30 minutes  
**Difficulty:** Foundational

---

## Overview

These practice problems reinforce the core concepts from the lecture (AI data lifecycle, automation patterns) and introduce the Python fundamentals you'll need for the lab. Complete these before attempting the lab.

---

## Part A: Conceptual Understanding

### Problem 1: Lifecycle Stage Identification

**Scenario:** You work at a fintech company that uses ML to detect fraudulent transactions. Read each description and identify which stage of the AI data lifecycle it belongs to.

**Stages:** Ingestion, Storage, Transformation, Serving, Monitoring

| Description | Lifecycle Stage |
|-------------|-----------------|
| A. Credit card swipes are captured from point-of-sale terminals and sent to your system | ___________ |
| B. Raw transaction records are stored in a cloud data lake for long-term retention | ___________ |
| C. Transaction amounts are converted from multiple currencies to USD and enriched with merchant category codes | ___________ |
| D. The fraud detection model receives a batch of cleaned transactions every hour for scoring | ___________ |
| E. An alert fires when the model's precision drops below 85% over a 24-hour window | ___________ |

---

### Problem 2: Batch vs. Streaming Classification

**Instructions:** For each use case, determine whether **batch processing**, **streaming processing**, or **both** would be most appropriate. Justify your choice in one sentence.

1. **Daily sales reports** sent to executives each morning summarizing yesterday's revenue.

   Processing type: ___________  
   Justification: _______________________________________________

2. **Real-time fraud alerts** that block suspicious transactions before they complete.

   Processing type: ___________  
   Justification: _______________________________________________

3. **Training a recommendation model** on the past 6 months of user interactions.

   Processing type: ___________  
   Justification: _______________________________________________

---

## Part B: Python Fundamentals for Data Engineering

These exercises introduce Python patterns you'll use in the lab.

### Problem 3: Working with File Paths

The `pathlib` module is the modern way to handle file paths in Python. Complete the code below.

```python
from pathlib import Path

# TODO: Create a Path object pointing to the customers.csv file
# The file is located at ../datasets/customers.csv (relative to this notebook)
data_file = _______________

# TODO: Check if the file exists and print the result
file_exists = _______________
print(f"File exists: {file_exists}")

# TODO: If the file exists, print its size in bytes
# Hint: Use the .stat() method and .st_size attribute
if file_exists:
    file_size = _______________
    print(f"File size: {file_size} bytes")

# BONUS: What happens when a file doesn't exist?
# Try creating a Path to a non-existent file and check .exists()
fake_file = Path("data/nonexistent.csv")
print(f"Fake file exists: {fake_file.exists()}")
```

---

### Problem 4: Reading and Inspecting CSV Data

Before uploading data to the cloud, you should inspect it. Complete the code below.

```python
import pandas as pd
from pathlib import Path

def inspect_csv(file_path: str) -> dict:
    """
    Load a CSV file and return basic statistics about it.
    
    Args:
        file_path: Path to the CSV file
        
    Returns:
        Dictionary with row_count, column_count, and column_names
    """
    # TODO: Load the CSV file into a DataFrame
    df = _______________
    
    # TODO: Create and return a dictionary with:
    # - "row_count": number of rows
    # - "column_count": number of columns  
    # - "column_names": list of column names
    result = {
        "row_count": _______________,
        "column_count": _______________,
        "column_names": _______________
    }
    
    return result

# Test your function with the actual dataset
stats = inspect_csv("../datasets/customers.csv")
print(stats)
```

---

### Problem 5: Basic Error Handling

Cloud operations can fail for many reasons. Practice writing defensive code with try/except.

```python
from pathlib import Path

def safe_read_file(file_path: str) -> dict:
    """
    Safely attempt to read a file and return status information.
    
    Args:
        file_path: Path to the file
        
    Returns:
        Dictionary with success status, file_size or error message
    """
    result = {
        "success": False,
        "file_path": file_path,
        "file_size_bytes": None,
        "error": None
    }
    
    # TODO: Complete the try/except block
    # - If successful: set success=True and file_size_bytes
    # - If FileNotFoundError: set error message "File not found: {file_path}"
    # - If any other exception: set error message with the exception details
    
    try:
        path = Path(file_path)
        # TODO: Get file size and update result
        _______________
        _______________
        _______________
    except FileNotFoundError:
        # TODO: Handle file not found
        _______________
    except Exception as e:
        # TODO: Handle any other exception
        _______________
    
    return result

# Test with the actual dataset (should succeed)
print(safe_read_file("../datasets/customers.csv"))

# Test with a file that doesn't exist (should show error handling)
print(safe_read_file("data/nonexistent_file.csv"))
```

---

### Problem 6: Understanding Cloud Upload Patterns

Cloud SDKs follow similar patterns across providers. Study this pseudocode pattern, then answer the questions below.

```python
# Generic cloud upload pattern (pseudocode)
def upload_file(local_path, bucket_name, object_key):
    # 1. Create a client connection to the cloud service
    client = CloudProvider.create_client()
    
    # 2. Verify local file exists
    if not file_exists(local_path):
        raise FileNotFoundError(f"Local file not found: {local_path}")
    
    # 3. Upload the file
    client.upload(
        source=local_path,
        destination_bucket=bucket_name,
        destination_key=object_key
    )
    
    # 4. Verify upload succeeded
    remote_metadata = client.get_object_info(bucket_name, object_key)
    
    return remote_metadata
```

**Questions:**

a) Why do we check if the local file exists before attempting to upload?

   _______________________________________________

b) What is the purpose of step 4 (verifying upload)?

   _______________________________________________

c) The `object_key` parameter often looks like a file path (e.g., `"raw/customers/2025/01/customers.csv"`). Why might we organize cloud storage this way?

   _______________________________________________

---

### Problem 7: Timestamps and Data Organization

Data pipelines often organize files by date. Complete this function that generates a timestamped path.

```python
from datetime import datetime

def generate_upload_path(base_folder: str, filename: str) -> str:
    """
    Generate a cloud storage path organized by date.
    
    Example output: "raw/customers/2025/01/23/customers.csv"
    
    Args:
        base_folder: Base folder path (e.g., "raw/customers")
        filename: Name of the file (e.g., "customers.csv")
        
    Returns:
        Full path with date components
    """
    # TODO: Get current date
    now = datetime.now()
    
    # TODO: Extract year, month, day as strings
    # Hint: Use strftime or access .year, .month, .day attributes
    # Make sure month and day are zero-padded (01, 02, etc.)
    year = _______________
    month = _______________
    day = _______________
    
    # TODO: Construct and return the full path
    # Format: "{base_folder}/{year}/{month}/{day}/{filename}"
    full_path = _______________
    
    return full_path

# Test your function
print(generate_upload_path("raw/customers", "customers.csv"))
# Expected output (will vary by date): "raw/customers/2025/01/23/customers.csv"
```

---

### Problem 8: Putting It Together - Mini Pipeline

Combine what you've learned to write a function that prepares a file for upload.

```python
import pandas as pd
from pathlib import Path
from datetime import datetime

def prepare_for_upload(local_path: str, destination_bucket: str) -> dict:
    """
    Prepare a local CSV file for cloud upload.
    
    This function:
    1. Validates the file exists
    2. Inspects the data
    3. Generates the destination path
    4. Returns a summary ready for upload
    
    Args:
        local_path: Path to the local CSV file
        destination_bucket: Name of the cloud storage bucket
        
    Returns:
        Dictionary with upload details or error information
    """
    result = {
        "ready_for_upload": False,
        "local_path": local_path,
        "destination_bucket": destination_bucket,
        "destination_key": None,
        "file_size_bytes": None,
        "row_count": None,
        "timestamp": datetime.now().isoformat(),
        "error": None
    }
    
    # TODO: Implement the preparation logic
    # Step 1: Check if file exists
    
    # Step 2: Get file size
    
    # Step 3: Load and get row count (for CSV files)
    
    # Step 4: Generate destination key using the filename and current date
    # Example: "raw/data/2025/01/23/customers.csv"
    
    # Step 5: Set ready_for_upload = True if all checks pass
    
    return result

# Test your function with the actual dataset
result = prepare_for_upload("../datasets/customers.csv", "my-data-bucket")
for key, value in result.items():
    print(f"{key}: {value}")
```

---

## Part C: Concept Check (Multiple Choice)

### Question 1
Why is data engineering considered foundational to AI systems?

- [ ] A. Data engineers build the machine learning models
- [ ] B. Models cannot function without reliable data pipelines delivering quality data
- [ ] C. Data engineering is more important than model development
- [ ] D. AI systems only need data engineering during initial setup

### Question 2
Which statement best describes the relationship between batch and streaming in production AI systems?

- [ ] A. Organizations must choose one pattern and use it exclusively
- [ ] B. Streaming has replaced batch processing in modern systems
- [ ] C. Most production systems combine both patterns for different use cases
- [ ] D. Batch processing is only used for legacy systems

### Question 3
The AI data lifecycle is described as "iterative" because:

- [ ] A. Data engineers iterate on code until it works
- [ ] B. Monitoring insights feed back into earlier stages, enabling continuous improvement
- [ ] C. Models are retrained iteratively until accuracy is acceptable
- [ ] D. Data is processed multiple times before storage

---

## Submission

Complete these practice problems and check your answers against the solution notebook before proceeding to the lab. The lab will build on these Python patterns to upload data to actual cloud storage.
