# Expected Test Results

## Test 1: Valid Translation Request

**Payload:** `payloads/01-valid-translation-request.json`

**Expected route:** Valid Jobs

**Expected key values:**
- `service_type`: `translation`
- `source_language`: `English`
- `target_language`: `Canadian French`
- `quote_requested`: `true`
- `file_or_order_number`: `LF-2026-7248`

**Actual result:** Passed

**Verification:** Confirmed that the request was saved to the valid jobs data table.

## Test 2: Missing Target Language

**Payload:** `payloads/02-missing-target-language.json`

**Expected route:** Manual Review

**Expected key values:**
- `service_type`: `translation`
- `source_language`: `German`
- `target_language`: empty or `null`
- `quote_requested`: `true`
- `file_or_order_number`: `LF-2026-8315`

**Actual result:** Passed

**Verification:** Confirmed that the request was saved to the review data table and not the valid jobs data table.