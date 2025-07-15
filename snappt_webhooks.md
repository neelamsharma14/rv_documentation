# SNAPPT Webhooks Documentation

## Overview

SNAPPT (Resident Verify Portal) webhooks provide real-time notifications for document verification, income verification, and ID scanning processes. These webhooks enable seamless integration between the Resident Verify Portal and the Entrata screening system.

## Webhook Types

### 1. Document Verification Webhooks
**Purpose**: Notify when document verification results are ready
**Controller**: `CDocumentVerificationWebhook`
**Location**: `Applications/ResidentVerifyPortal/DocumentVerification/Application/DocumentVerification/`

### 2. Income Verification Webhooks
**Purpose**: Notify when income verification reports are ready
**Controller**: `CApplicationVerificationOfIncomeWebhookController`
**Location**: `Applications/ResidentVerifyPortal/voi/Application/voi/`

### 3. ID Scanning Webhooks
**Purpose**: Notify when ID scanning verification is complete
**Controller**: `CIDScanningWebhook`
**Location**: `Applications/ResidentVerifyPortal/IDScanning/Application/IDScanning/`

## Webhook URLs

### Base URLs
The Resident Verify Portal uses dynamic URL generation based on the environment:

- **Production**: `https://residentverify.com/`
- **Stage**: `https://residentverify.com/`
- **Development**: `http://[env-stack-id].residentverify.com/`

### Specific Endpoints
Based on the codebase analysis, webhooks are accessed through the Resident Verify Portal with module/action routing:

- **Document Verification**: `/?module=document_verification&action=webhook`
- **Income Verification**: `/?module=voi&action=trigger_webhook`
- **ID Scanning**: `/?module=id_scanning&action=webhook`

### Actual Webhook URL Structure
The webhook URLs follow the Resident Verify Portal routing pattern:
```
https://residentverify.com/?module=[module_name]&action=[action_name]&keys=[encrypted_parameters]
```

## Security Features

### HMAC-SHA256 Signature Verification
All webhooks use HMAC-SHA256 signature verification for security:

```php
// Signature format in header
SNAPPT-Signature: t=timestamp,v1=signature

// Verification process
$strToSign = $timestamp . '.' . $requestBody;
$strHash = hash_hmac('sha256', $strToSign, $apiKeyId, true);
$strExpectedSignature = rtrim(strtr(base64_encode($strHash), '+/', '-_'), '=');
```

### Required Headers
```
Content-Type: application/json
SNAPPT-Signature: t=1642248600,v1=abc123...
User-Agent: SNAPPT-Webhook/1.0
```

## Document Verification Webhook

### Payload Structure

```json
{
  "apiKeyId": "api_key_12345",
  "webhookId": "webhook_67890",
  "eventType": "REPORT_READY",
  "applicantDetailId": "applicant_12345",
  "applicantId": "app_67890",
  "data": {
    "result": "CLEAN",
    "verificationDate": "2024-01-15T10:30:00Z",
    "documentType": "PAY_STUB",
    "verificationScore": 95.5,
    "verificationDetails": {
      "employerName": "ABC Company",
      "employerAddress": "123 Main St, City, State",
      "employmentStartDate": "2020-01-15",
      "employmentEndDate": null,
      "position": "Software Engineer",
      "salary": 75000,
      "payFrequency": "BI_WEEKLY"
    },
    "verificationMetadata": {
      "verificationMethod": "AUTOMATED",
      "verificationProvider": "Resident Verify",
      "processingTime": 2.5
    }
  },
  "timestamp": "2024-01-15T10:30:00Z"
}
```

### Response Codes
- **200 OK**: Webhook processed successfully
- **400 Bad Request**: Invalid request format
- **401 Unauthorized**: Invalid signature
- **500 Internal Server Error**: Processing error

### Result Types
- **CLEAN**: Document verified successfully
- **EDITED**: Document verified with manual edits
- **UNDETERMINED**: Verification inconclusive
- **FAILED**: Document verification failed

## Income Verification Webhook

### Payload Structure

```json
{
  "webhook_type": "CHECK_REPORT",
  "webhook_code": "CHECK_REPORT_READY",
  "user_id": "user_12345",
  "successful_products": [
    "cra_base_report",
    "cra_income_insights"
  ],
  "environment": "sandbox",
  "timestamp": "2024-01-15T10:30:00Z"
}
```

### Alternative Payload (Payroll Verification)

```json
{
  "webhook_type": "INCOME",
  "webhook_code": "INCOME_VERIFICATION",
  "item_id": "gAXlMgVEw5uEGoQnnXZ6tn9E7Mn3LBc4PJVKZ",
  "user_id": "user_12345",
  "verification_status": "VERIFICATION_STATUS_PROCESSING_COMPLETE",
  "environment": "sandbox",
  "timestamp": "2024-01-15T10:30:00Z"
}
```

### Webhook Codes
- **CHECK_REPORT_READY**: Income report ready
- **CHECK_REPORT_FAILED**: Income report failed
- **INCOME_VERIFICATION**: Payroll verification complete
- **VERIFICATION_STATUS_PROCESSING_COMPLETE**: Processing successful
- **VERIFICATION_STATUS_PROCESSING_FAILED**: Processing failed

## ID Scanning Webhook

### Payload Structure

```json
{
  "identity_verification_id": "id_verification_12345",
  "verification_status": "COMPLETED",
  "verification_result": "VERIFIED",
  "document_type": "DRIVERS_LICENSE",
  "verification_score": 98.5,
  "verification_details": {
    "documentNumber": "DL123456789",
    "expirationDate": "2025-12-31",
    "state": "CA",
    "firstName": "John",
    "lastName": "Doe",
    "dateOfBirth": "1990-01-15"
  },
  "timestamp": "2024-01-15T10:30:00Z"
}
```

## Postman Testing Guide

### Step 1: Setup Postman Collection

1. Create a new collection named "SNAPPT Webhooks"
2. Set up environment variables:
   - `base_url`: `https://residentverify.com`
   - `api_key`: Your SNAPPT API key
   - `webhook_secret`: Your webhook secret

### Step 2: Document Verification Test

**Request Setup:**
- **Method**: POST
- **URL**: `{{base_url}}/?module=document_verification&action=webhook`
- **Headers**:
  ```
  Content-Type: application/json
  SNAPPT-Signature: t={{timestamp}},v1={{signature}}
  ```

**Body (raw JSON):**
```json
{
  "apiKeyId": "{{api_key}}",
  "webhookId": "webhook_test_123",
  "eventType": "REPORT_READY",
  "applicantDetailId": "applicant_test_123",
  "applicantId": "app_test_456",
  "data": {
    "result": "CLEAN",
    "verificationDate": "2024-01-15T10:30:00Z",
    "documentType": "PAY_STUB",
    "verificationScore": 95.5,
    "verificationDetails": {
      "employerName": "Test Company",
      "employerAddress": "123 Test St, Test City, TS",
      "employmentStartDate": "2020-01-15",
      "position": "Test Engineer",
      "salary": 75000,
      "payFrequency": "BI_WEEKLY"
    }
  },
  "timestamp": "{{timestamp}}"
}
```

### Step 3: Income Verification Test

**Request Setup:**
- **Method**: POST
- **URL**: `{{base_url}}/?module=voi&action=trigger_webhook`
- **Headers**:
  ```
  Content-Type: application/json
  SNAPPT-Signature: t={{timestamp}},v1={{signature}}
  ```

**Body (raw JSON):**
```json
{
  "webhook_type": "CHECK_REPORT",
  "webhook_code": "CHECK_REPORT_READY",
  "user_id": "user_test_123",
  "successful_products": [
    "cra_base_report",
    "cra_income_insights"
  ],
  "environment": "sandbox",
  "timestamp": "{{timestamp}}"
}
```

### Step 4: ID Scanning Test

**Request Setup:**
- **Method**: POST
- **URL**: `{{base_url}}/?module=id_scanning&action=webhook`
- **Headers**:
  ```
  Content-Type: application/json
  SNAPPT-Signature: t={{timestamp}},v1={{signature}}
  ```

**Body (raw JSON):**
```json
{
  "identity_verification_id": "id_verification_test_123",
  "verification_status": "COMPLETED",
  "verification_result": "VERIFIED",
  "document_type": "DRIVERS_LICENSE",
  "verification_score": 98.5,
  "verification_details": {
    "documentNumber": "DL123456789",
    "expirationDate": "2025-12-31",
    "state": "CA",
    "firstName": "John",
    "lastName": "Doe",
    "dateOfBirth": "1990-01-15"
  },
  "timestamp": "{{timestamp}}"
}
```

### Step 5: Pre-request Script for Signature

Add this pre-request script to generate the signature:

```javascript
// Generate timestamp
const timestamp = Math.floor(Date.now() / 1000);
pm.environment.set("timestamp", timestamp);

// Get request body
const requestBody = pm.request.body.raw;

// Create signature
const message = timestamp + '.' + requestBody;
const signature = CryptoJS.HmacSHA256(message, pm.environment.get("webhook_secret"));
const base64Signature = CryptoJS.enc.Base64.stringify(signature);
const urlSafeSignature = base64Signature.replace(/\+/g, '-').replace(/\//g, '_').replace(/=/g, '');

pm.environment.set("signature", urlSafeSignature);
```

### Step 6: Test Scripts

Add this test script to validate responses:

```javascript
// Test response status
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

// Test response body
pm.test("Response contains OK", function () {
    pm.expect(pm.response.text()).to.include("OK");
});

// Test response time
pm.test("Response time is less than 5000ms", function () {
    pm.expect(pm.response.responseTime).to.be.below(5000);
});
```

## Verification Steps

### 1. Webhook URL Verification
- Verify the webhook URL is accessible from your network
- Test with a simple GET request to ensure the endpoint responds
- Check for any firewall or network restrictions

### 2. Authentication Verification
- Ensure your API key is valid and active
- Verify the webhook secret is correctly configured
- Test signature generation and verification

### 3. Payload Verification
- Validate JSON structure matches expected format
- Check all required fields are present
- Verify data types and formats

### 4. Response Verification
- Confirm webhook returns expected status codes
- Verify response body contains expected content
- Check response time is within acceptable limits

### 5. Database Verification
- Verify webhook data is properly stored in database
- Check screening status updates correctly
- Confirm activity logs are created

## Error Handling

### Common Error Responses

**400 Bad Request:**
```json
{
  "error": "Invalid request format",
  "message": "Missing required fields",
  "timestamp": "2024-01-15T10:30:00Z"
}
```

**401 Unauthorized:**
```json
{
  "error": "Unauthorized",
  "message": "Invalid signature",
  "timestamp": "2024-01-15T10:30:00Z"
}
```

**500 Internal Server Error:**
```json
{
  "error": "Processing error",
  "message": "Failed to process webhook",
  "timestamp": "2024-01-15T10:30:00Z"
}
```

### Retry Logic
- Webhooks are retried up to 3 times with exponential backoff
- Retry intervals: 1s, 5s, 15s
- Failed webhooks are logged for manual review

## Monitoring and Logging

### Activity Logging
All webhook activities are logged with:
- Webhook ID
- Timestamp
- Processing status
- Error details (if any)
- Response time

### Database Tables
- `screening_transactions`: Main screening records
- `document_verification_details`: Document verification records
- `document_verification_result_details`: Verification results
- `screening_activity_logs`: Activity tracking

### Log Levels
- **INFO**: Successful webhook processing
- **WARNING**: Retry attempts
- **ERROR**: Processing failures
- **DEBUG**: Detailed processing steps

## Best Practices

### Security
1. Always verify HMAC signatures
2. Use HTTPS for all webhook endpoints
3. Rotate API keys regularly
4. Monitor for suspicious activity

### Performance
1. Respond quickly (under 5 seconds)
2. Use async processing for heavy operations
3. Implement proper error handling
4. Monitor response times

### Reliability
1. Implement idempotency
2. Use retry logic with exponential backoff
3. Log all activities for audit trail
4. Test webhooks in sandbox environment first

## Troubleshooting

### Common Issues

**Signature Verification Fails:**
- Check API key configuration
- Verify timestamp format
- Ensure correct signature algorithm

**Webhook Not Received:**
- Verify endpoint URL
- Check firewall settings
- Validate request format

**Processing Errors:**
- Check database connectivity
- Verify required fields
- Review error logs

### Debug Steps
1. Enable debug logging
2. Check webhook payload format
3. Verify database records
4. Test with sample data
5. Review activity logs

## Support

For webhook support:
- **Email**: webhooks@entrata.com
- **Documentation**: https://docs.entrata.com/webhooks
- **Status Page**: https://status.entrata.com
- **API Support**: https://support.entrata.com/api
