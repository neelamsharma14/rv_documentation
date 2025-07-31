# Resident Verify Portal API Documentation

## Overview

The Resident Verify Portal provides a comprehensive set of endpoints for identity verification, income verification, document verification, and other screening services. This documentation covers all available endpoints, their parameters, and expected responses.

## Base URL

The base URL varies by environment:
- **Development**: `http://{host}`
- **Staging/Production**: `https://{host}`

## Authentication

Most endpoints require authentication via URL parameters:
- `keys` or `param`: Encrypted parameters containing session/authentication data
- `module`: The module identifier
- `action`: The specific action to perform

## Endpoints

### 1. Identity Verification Endpoints

#### Base Path: `/idVerification/`

##### 1.1 Verify Kick Off
- **URL**: `/idVerification/?module=id_verification&action=verify_kick_off`
- **Method**: GET/POST
- **Description**: Initiates the identity verification process
- **Parameters**:
  - `keys` (required): Encrypted session parameters
  - `module`: `id_verification`
  - `action`: `verify_kick_off`

##### 1.2 Verify Code Entry
- **URL**: `/idVerification/?module=id_verification&action=verify_code_entry`
- **Method**: GET/POST
- **Description**: Handles verification code entry for identity verification
- **Parameters**:
  - `keys` (required): Encrypted session parameters
  - `module`: `id_verification`
  - `action`: `verify_code_entry`

##### 1.3 Submit Code Entry
- **URL**: `/idVerification/?module=id_verification&action=submit_code_entry`
- **Method**: POST
- **Description**: Submits verification code for processing
- **Parameters**:
  - `keys` (required): Encrypted session parameters
  - `module`: `id_verification`
  - `action`: `submit_code_entry`

##### 1.4 Knowledge IQ Questionnaires
- **URL**: `/idVerification/?module=id_verification&action=kiq_questionnaires`
- **Method**: GET/POST
- **Description**: Displays knowledge-based identity questions
- **Parameters**:
  - `keys` (required): Encrypted session parameters
  - `module`: `id_verification`
  - `action`: `kiq_questionnaires`

##### 1.5 Submit Knowledge IQ Score Request
- **URL**: `/idVerification/?module=id_verification&action=submit_knowledge_iq_score_request`
- **Method**: POST
- **Description**: Submits knowledge-based identity verification scores
- **Parameters**:
  - `keys` (required): Encrypted session parameters
  - `module`: `id_verification`
  - `action`: `submit_knowledge_iq_score_request`

##### 1.6 End Verification Process
- **URL**: `/idVerification/?module=id_verification&action=end_verification_process`
- **Method**: GET/POST
- **Description**: Completes the identity verification process
- **Parameters**:
  - `keys` (required): Encrypted session parameters
  - `module`: `id_verification`
  - `action`: `end_verification_process`

##### 1.7 Verify Unfreeze PIN Entry
- **URL**: `/idVerification/?module=id_verification&action=verify_unfreeze_pin_entry`
- **Method**: GET/POST
- **Description**: Handles credit freeze PIN entry for verification
- **Parameters**:
  - `keys` (required): Encrypted session parameters
  - `module`: `id_verification`
  - `action`: `verify_unfreeze_pin_entry`

##### 1.8 Submit Access PIN
- **URL**: `/idVerification/?module=id_verification&action=submit_access_pin`
- **Method**: POST
- **Description**: Submits access PIN for credit report access
- **Parameters**:
  - `keys` (required): Encrypted session parameters
  - `module`: `id_verification`
  - `action`: `submit_access_pin`

### 2. Verification of Income (VOI) Endpoints

#### Base Path: `/voi/`

##### 2.1 Verification of Income Request
- **URL**: `/voi/?module=application_verification_of_income&action=verification_of_income_request`
- **Method**: GET/POST
- **Description**: Initiates income verification process
- **Parameters**:
  - `keys` (required): Encrypted session parameters
  - `module`: `application_verification_of_income`
  - `action`: `verification_of_income_request`

##### 2.2 Verification Completed
- **URL**: `/voi/?module=application_verification_of_income&action=verification_completed`
- **Method**: GET/POST
- **Description**: Handles completion of income verification
- **Parameters**:
  - `keys` (required): Encrypted session parameters
  - `module`: `application_verification_of_income`
  - `action`: `verification_completed`

##### 2.3 Show Success Page
- **URL**: `/voi/?module=application_verification_of_income&action=show_success_page`
- **Method**: GET
- **Description**: Displays success page after income verification
- **Parameters**:
  - `keys` (required): Encrypted session parameters
  - `module`: `application_verification_of_income`
  - `action`: `show_success_page`

##### 2.4 View FAQs
- **URL**: `/voi/?module=application_verification_of_income&action=view_faqs`
- **Method**: GET
- **Description**: Displays frequently asked questions
- **Parameters**:
  - `keys` (required): Encrypted session parameters
  - `module`: `application_verification_of_income`
  - `action`: `view_faqs`

##### 2.5 Don't Have Bank Account
- **URL**: `/voi/?module=application_verification_of_income&action=dont_have_bank_account`
- **Method**: GET/POST
- **Description**: Handles case when applicant doesn't have a bank account
- **Parameters**:
  - `keys` (required): Encrypted session parameters
  - `module`: `application_verification_of_income`
  - `action`: `dont_have_bank_account`

##### 2.6 Submit Don't Have Bank Account
- **URL**: `/voi/?module=application_verification_of_income&action=submit_dont_have_bank_account`
- **Method**: POST
- **Description**: Submits response for no bank account scenario
- **Parameters**:
  - `keys` (required): Encrypted session parameters
  - `module`: `application_verification_of_income`
  - `action`: `submit_dont_have_bank_account`

##### 2.7 Show Thank You Page
- **URL**: `/voi/?module=application_verification_of_income&action=show_thank_you_page`
- **Method**: GET
- **Description**: Displays thank you page
- **Parameters**:
  - `keys` (required): Encrypted session parameters
  - `module`: `application_verification_of_income`
  - `action`: `show_thank_you_page`

##### 2.8 Need Assistance
- **URL**: `/voi/?module=application_verification_of_income&action=need_assistance`
- **Method**: GET/POST
- **Description**: Provides assistance options
- **Parameters**:
  - `keys` (required): Encrypted session parameters
  - `module`: `application_verification_of_income`
  - `action`: `need_assistance`

### 3. VOI Premium Endpoints

#### Base Path: `/voi/`

##### 3.1 Verification of Income Request (Premium)
- **URL**: `/voi/?module=verification_of_income&action=verification_of_income_request`
- **Method**: GET/POST
- **Description**: Premium income verification initiation
- **Parameters**:
  - `keys` (required): Encrypted session parameters
  - `module`: `verification_of_income`
  - `action`: `verification_of_income_request`

##### 3.2 Bank Income Submitted
- **URL**: `/voi/?module=verification_of_income&action=bank_income_submitted`
- **Method**: POST
- **Description**: Handles bank income submission
- **Parameters**:
  - `keys` (required): Encrypted session parameters
  - `module`: `verification_of_income`
  - `action`: `bank_income_submitted`

##### 3.3 Get Bank Income Transaction Status
- **URL**: `/voi/?module=verification_of_income&action=get_bank_income_transaction_status`
- **Method**: GET
- **Description**: Retrieves bank income transaction status
- **Parameters**:
  - `keys` (required): Encrypted session parameters
  - `module`: `verification_of_income`
  - `action`: `get_bank_income_transaction_status`

##### 3.4 Initiate Payroll Income
- **URL**: `/voi/?module=verification_of_income&action=initiate_payroll_income`
- **Method**: POST
- **Description**: Initiates payroll income verification
- **Parameters**:
  - `keys` (required): Encrypted session parameters
  - `module`: `verification_of_income`
  - `action`: `initiate_payroll_income`

##### 3.5 Payroll Income Submitted
- **URL**: `/voi/?module=verification_of_income&action=payroll_income_submitted`
- **Method**: POST
- **Description**: Handles payroll income submission
- **Parameters**:
  - `keys` (required): Encrypted session parameters
  - `module`: `verification_of_income`
  - `action`: `payroll_income_submitted`

##### 3.6 Get Payroll Income Transaction Status
- **URL**: `/voi/?module=verification_of_income&action=get_payroll_income_transaction_status`
- **Method**: GET
- **Description**: Retrieves payroll income transaction status
- **Parameters**:
  - `keys` (required): Encrypted session parameters
  - `module`: `verification_of_income`
  - `action`: `get_payroll_income_transaction_status`

##### 3.7 Income Verification Success
- **URL**: `/voi/?module=verification_of_income&action=income_verification_success`
- **Method**: GET
- **Description**: Displays income verification success page
- **Parameters**:
  - `keys` (required): Encrypted session parameters
  - `module`: `verification_of_income`
  - `action`: `income_verification_success`

##### 3.8 Income Verification Fail
- **URL**: `/voi/?module=verification_of_income&action=income_verification_fail`
- **Method**: GET
- **Description**: Displays income verification failure page
- **Parameters**:
  - `keys` (required): Encrypted session parameters
  - `module`: `verification_of_income`
  - `action`: `income_verification_fail`

##### 3.9 Income Verification Error
- **URL**: `/voi/?module=verification_of_income&action=income_verification_error`
- **Method**: GET
- **Description**: Displays income verification error page
- **Parameters**:
  - `keys` (required): Encrypted session parameters
  - `module`: `verification_of_income`
  - `action`: `income_verification_error`

### 4. Webhook Endpoints

#### 4.1 Document Verification Webhook
- **URL**: `/DocumentVerification/?module=default`
- **Method**: POST
- **Description**: Receives document verification results from external providers
- **Headers**:
  - `HTTP_SNAPPT_SIGNATURE`: Signature for webhook verification
  - `Content-Type`: `application/json`
- **Request Body** (JSON):
  ```json
  {
    "apiKeyId": "string",
    "webhookId": "string",
    "eventType": "REPORT_READY",
    "applicantDetailId": "string",
    "applicantId": "string",
    "data": {
      "id": "string",
      "result": "string",
      "note": "string",
      "status": "string"
    }
  }
  ```
- **Response**: `200 OK` with "OK" message

#### 4.2 VOI Webhook Endpoints

##### 4.2.1 Handle OA Income Verification Report Ready
- **URL**: `/voi/?module=webhook&action=handle_oa_income_verification_report_ready`
- **Method**: POST
- **Description**: Handles Online Application income verification webhooks
- **Request Body** (JSON):
  ```json
  {
    "webhook_type": "string",
    "webhook_code": "string",
    "user_id": "string",
    "successful_products": ["string"],
    "environment": "string"
  }
  ```

##### 4.2.2 Handle OA Payroll Verification Report Ready
- **URL**: `/voi/?module=webhook&action=handle_oa_payroll_verification_report_ready`
- **Method**: POST
- **Description**: Handles Online Application payroll verification webhooks

##### 4.2.3 Handle RV Income Verification Report Ready
- **URL**: `/voi/?module=webhook&action=handle_rv_income_verification_report_ready`
- **Method**: POST
- **Description**: Handles Resident Verify income verification webhooks

##### 4.2.4 Handle RV Payroll Verification Report Ready
- **URL**: `/voi/?module=webhook&action=handle_rv_payroll_verification_report_ready`
- **Method**: POST
- **Description**: Handles Resident Verify payroll verification webhooks

#### 4.3 ID Scanning Webhook
- **URL**: `/IDScanning/?module=default`
- **Method**: POST
- **Description**: Receives ID scanning verification results
- **Request Body** (JSON):
  ```json
  {
    "identity_verification_id": "string",
    "status": "string",
    "result": "object"
  }
  ```

#### 4.4 International Credit Webhook
- **URL**: `/IntlCredit/?module=default`
- **Method**: POST
- **Description**: Receives international credit verification results
- **Request Body** (JSON):
  ```json
  {
    "publicToken": "string",
    "status": "string"
  }
  ```
- **Status Values**:
  - `SUCCESS`: Verification successful
  - `PENDING`: Verification in progress
  - `NOT_FOUND`: Applicant not found
  - `NOT_AUTHENTICATED`: Authentication failed
  - `ERROR`: Internal error
  - `SKIPPED`: Process skipped
  - `EXPIRED`: Link expired
  - `BUREAU_UNRESPONSIVE`: Bureau outage
  - `UNSUPPORTED_COUNTRY`: Country not supported
  - `FINISH_LATER_INITIATED`: Finish later option selected

### 5. Disputes Endpoints

#### Base Path: `/disputes/`

##### 5.1 Create Dispute Info
- **URL**: `/disputes/?module=dispute&action=create_dispute_info`
- **Method**: GET/POST
- **Description**: Creates dispute information
- **Parameters**:
  - `keys` (required): Encrypted session parameters
  - `module`: `dispute`
  - `action`: `create_dispute_info`

##### 5.2 Create Statement Request
- **URL**: `/disputes/?module=dispute&action=create_statement_request`
- **Method**: POST
- **Description**: Creates statement request for dispute
- **Parameters**:
  - `keys` (required): Encrypted session parameters
  - `module`: `dispute`
  - `action`: `create_statement_request`

##### 5.3 Submit Dispute
- **URL**: `/disputes/?module=dispute&action=submit_dispute`
- **Method**: POST
- **Description**: Submits dispute for processing
- **Parameters**:
  - `keys` (required): Encrypted session parameters
  - `module`: `dispute`
  - `action`: `submit_dispute`

##### 5.4 Check Dispute Status
- **URL**: `/disputes/?module=dispute&action=check_dispute_status`
- **Method**: GET
- **Description**: Checks current dispute status
- **Parameters**:
  - `keys` (required): Encrypted session parameters
  - `module`: `dispute`
  - `action`: `check_dispute_status`

##### 5.5 View Dispute Status
- **URL**: `/disputes/?module=dispute&action=view_dispute_status`
- **Method**: GET
- **Description**: Displays dispute status page
- **Parameters**:
  - `keys` (required): Encrypted session parameters
  - `module`: `dispute`
  - `action`: `view_dispute_status`

##### 5.6 Load Dispute Type Reason
- **URL**: `/disputes/?module=dispute&action=load_dispute_type_reason`
- **Method**: GET
- **Description**: Loads dispute type reasons
- **Parameters**:
  - `keys` (required): Encrypted session parameters
  - `module`: `dispute`
  - `action`: `load_dispute_type_reason`

### 6. Consumer Reports Endpoints

#### Base Path: `/ConsumerReports/`

##### 6.1 Consumer Authentication
- **URL**: `/ConsumerReports/?module=consumer_authentication`
- **Method**: GET/POST
- **Description**: Handles consumer authentication for reports
- **Parameters**:
  - `keys` (required): Encrypted session parameters
  - `module`: `consumer_authentication`

### 7. E-Signature Endpoints

#### 7.1 E-Sign Policy Documents
- **URL**: `/EsignPolicyDocuments/?module=application_esign_policy_document`
- **Method**: GET/POST
- **Description**: Handles e-signature for policy documents
- **Parameters**:
  - `keys` (required): Encrypted session parameters
  - `module`: `application_esign_policy_document`

#### 7.2 GCIC E-Sign
- **URL**: `/GCICConsentForms/?module=application_gcic_esign`
- **Method**: GET/POST
- **Description**: Handles GCIC consent form e-signatures
- **Parameters**:
  - `keys` (required): Encrypted session parameters
  - `module`: `application_gcic_esign`

#### 7.3 Parental Consent Forms
- **URL**: `/ParentalConsentForms/?module=parental_consent_form`
- **Method**: GET/POST
- **Description**: Handles parental consent form processing
- **Parameters**:
  - `keys` (required): Encrypted session parameters
  - `module`: `parental_consent_form`

## Error Responses

### Standard Error Format
```json
{
  "error": "Error message",
  "code": 400,
  "details": "Additional error details"
}
```

### Common HTTP Status Codes
- `200 OK`: Request successful
- `400 Bad Request`: Invalid request parameters
- `401 Unauthorized`: Authentication required
- `404 Not Found`: Endpoint or resource not found
- `500 Internal Server Error`: Server error

## Security Considerations

1. **Authentication**: All endpoints require valid encrypted parameters via `keys` or `param`
2. **Webhook Verification**: Webhook endpoints verify signatures to ensure authenticity
3. **HTTPS**: All production endpoints use HTTPS
4. **Input Validation**: All input parameters are validated and sanitized
5. **Rate Limiting**: Implemented on webhook endpoints to prevent abuse

## Rate Limits

- **Webhook Endpoints**: 100 requests per minute per IP
- **User-Facing Endpoints**: 1000 requests per hour per session
- **Authentication Endpoints**: 10 requests per minute per IP

## Testing

### Development Environment
- Base URL: `http://localhost` or development server
- Test data available for all endpoints
- Debug logging enabled

### Staging Environment
- Base URL: `https://stage.{domain}`
- Production-like data
- Full testing capabilities

### Production Environment
- Base URL: `https://{domain}`
- Live data only
- Minimal logging for performance

## Support

For technical support or questions about the API:
- Email: [Support Email]
- Documentation: [Documentation URL]
- Status Page: [Status Page URL]
