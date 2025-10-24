# Mako Bug Squash Interview - Setup Instructions

## Prerequisites
- Python 3.8 or higher
- pip (Python package manager)

## Setup Instructions

### 1. Navigate to the Project Directory
```bash
cd /Users/hadihamid/Desktop/mako
```

### 2. Create and Activate Virtual Environment
The virtual environment has already been created, but if you need to recreate it:

```bash
# Create virtual environment
python3 -m venv venv

# Activate on macOS/Linux
source venv/bin/activate

# Activate on Windows
# venv\Scripts\activate
```

### 3. Install Dependencies
```bash
pip install -e .
```

## Running Tests

### Run All Tests
```bash
pytest test/
```

### Run Specific Test File
```bash
pytest test/test_util.py
pytest test/test_lookup.py
```

### Run Tests with Verbose Output
```bash
pytest test/ -v
```

### Run Specific Test Case
```bash
pytest test/test_util.py::UtilTest::test_fast_buffer_truncate
```

### Run Tests and Stop at First Failure
```bash
pytest test/ -x
```

### Run Tests with Short Traceback
```bash
pytest test/ --tb=short
```

### Run Tests in Quiet Mode
```bash
pytest test/ -q
```

## Expected Test Results

**Current State (with bugs):**
- 2 tests should FAIL
- 466 tests should PASS
- 47 tests should be SKIPPED

**After Fixing Bugs:**
- 0 tests should FAIL
- 468 tests should PASS
- 47 tests should be SKIPPED

## Deactivating Virtual Environment
When you're done:
```bash
deactivate
```

## Troubleshooting

### If pytest is not found:
```bash
pip install pytest
```

### If import errors occur:
```bash
pip install -e .
```

### To see installed packages:
```bash
pip list
```

