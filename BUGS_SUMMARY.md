# Bug Squash Mock Interview - Implementation Summary

## Overview
Two realistic bugs have been successfully introduced into the Mako codebase to create a Stripe-style bug squash interview scenario.

## Bugs Implemented

### Bug #1: Stale Reference Bug in FastEncodingBuffer
- **Type**: Missing state reset / stale pointer reference
- **Location**: `mako/util.py`, line 152-153
- **What was changed**: Removed `self.write = self.data.append` from the `truncate()` method
- **Impact**: After calling `truncate()`, the `self.write` pointer still references the old deque's append method, causing new writes to be lost
- **Test affected**: `test/test_util.py::UtilTest::test_fast_buffer_truncate`

### Bug #2: Off-by-One Error in Path Processing  
- **Type**: Off-by-one error in string slicing
- **Location**: `mako/lookup.py`, line 294
- **What was changed**: Changed `filename[len(dir_) :]` to `filename[len(dir_) + 1 :]`
- **Impact**: Strips one extra character from the path, removing the leading slash from the URI
- **Test affected**: `test/test_lookup.py::LookupTest::test_uri_adjust`

## Test Results

### With Bugs (Current State)
```
2 failed, 466 passed, 47 skipped
```

**Failed tests:**
1. `test/test_util.py::UtilTest::test_fast_buffer_truncate`
   - Error: `AssertionError: '' != 'string c string d'`
   
2. `test/test_lookup.py::LookupTest::test_uri_adjust`
   - Error: `AssertionError: assert 'etc/lala/index.html' == '/etc/lala/index.html'`

### After Fixing Bugs
```
468 passed, 47 skipped
```

## Files Created

1. **Interviewer_Guide.md**
   - Detailed guide for the interviewer
   - Bug locations and descriptions
   - Debugging tips and hints
   - Expected candidate behavior
   - Progressive hints if candidate gets stuck

2. **README_SETUP.md**
   - Setup instructions for the interview
   - How to run tests
   - Expected test results
   - Troubleshooting guide

## Bug Characteristics

Both bugs are:
- ✅ **Realistic**: Common bug patterns seen in production code
- ✅ **Subtle**: Not immediately obvious from casual inspection
- ✅ **Debuggable**: Clear test failures with actionable error messages
- ✅ **Fixable**: Can be fixed with 1-line changes once identified
- ✅ **Well-tested**: Clear pass/fail criteria

## Bug Types Align With Stripe Interview Focus

From the Stripe interview guide:
- ✅ Off-by-one errors (Bug #2)
- ✅ Reference/pointer issues (Bug #1) 
- ✅ State management bugs (Bug #1)
- ✅ String manipulation bugs (Bug #2)

## How to Use for Interview

1. **Setup** (before interview):
   - Candidate should have the codebase
   - Environment should be set up per README_SETUP.md
   - Verify tests fail with `pytest test/`

2. **During interview**:
   - Give candidate README_SETUP.md only
   - Keep Interviewer_Guide.md for yourself
   - Have candidate run tests and observe failures
   - Watch their debugging approach
   - Use progressive hints from guide if needed

3. **Success criteria**:
   - Candidate finds and fixes both bugs
   - Tests pass after fixes
   - Good communication throughout
   - Systematic debugging approach

## To Revert Bugs (Reset to Clean State)

If you need to restore the codebase:

```bash
git checkout mako/util.py
git checkout mako/lookup.py
```

Or manually:

1. In `mako/util.py` line 152-153, add back:
   ```python
   self.write = self.data.append
   ```

2. In `mako/lookup.py` line 294, change:
   ```python
   return filename[len(dir_) + 1 :]
   ```
   to:
   ```python
   return filename[len(dir_) :]
   ```

