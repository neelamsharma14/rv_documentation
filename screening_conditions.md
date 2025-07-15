# Screening Conditions Complete Documentation

## Table of Contents
1. [Overview](#overview)
2. [Business Explanation](#business-explanation)
3. [Navigation Flow](#navigation-flow)
4. [Main Files and Controllers](#main-files-and-controllers)
5. [Database Tables](#database-tables)
6. [Key Functions](#key-functions)
7. [URL Structure](#url-structure)
8. [User Interface](#user-interface)
9. [Common Operations](#common-operations)
10. [Troubleshooting](#troubleshooting)
11. [Webhook Integration](#webhook-integration)
12. [Security and Permissions](#security-and-permissions)

## Overview

Screening conditions in Entrata are additional requirements that must be satisfied for an application to be approved when the initial screening criteria are not fully met. Think of them as "homework" that applicants need to complete to qualify for approval.

### What are Screening Conditions?

Screening conditions are specific requirements that can be financial (increased deposit, higher rent), documentation-based (provide pay stubs, add guarantor), or procedural (complete forms, attend property tour). They provide flexibility in the approval process while maintaining standards.

### Key Components

- **Condition Templates**: Pre-defined sets of conditions that can be reused
- **Condition Sets**: Groups of related conditions with logic (AND/OR)
- **Available Conditions**: Individual condition types that can be configured
- **Condition Evaluation**: Logic to determine if conditions are satisfied
- **Condition Satisfaction**: Tracking when and how conditions are met

### Entry Points

1. **Setup → Leasing → Screening → Condition Templates** (Primary)
2. **Package Management → Conditions Tab** (Package-specific)
3. **Application Screening Process** (Runtime evaluation)
4. **Dashboard → Conditional Offers** (Management)

## Business Explanation

### Purpose

Screening conditions serve several business purposes:

1. **Flexible Approval**: Allow approval of borderline applicants with additional requirements
2. **Risk Mitigation**: Reduce risk through additional financial or documentation requirements
3. **Standardization**: Provide consistent condition templates across properties
4. **Compliance**: Ensure legal and regulatory requirements are met
5. **Revenue Optimization**: Increase deposits or rent for higher-risk applicants

### Business Rules

1. **Condition Types**: Different types for different scenarios
   - **Financial Conditions**: Increase deposit, higher rent, additional fees
   - **Documentation Conditions**: Provide pay stubs, add guarantor, submit references
   - **Procedural Conditions**: Complete forms, attend tour, provide verification

2. **Logic Types**: How conditions are evaluated
   - **AND Logic**: All conditions must be satisfied
   - **OR Logic**: Any condition can be satisfied
   - **Complex Logic**: Combinations of AND/OR with subsets

3. **Evaluation Order**: Conditions are evaluated in priority order
4. **Satisfaction Tracking**: System tracks when and how conditions are met
5. **Automation**: Some conditions can be automatically processed

### User Roles and Access

- **Property Managers**: Can view and manage condition templates
- **Leasing Agents**: Can apply conditions during screening
- **System Administrators**: Can create and configure condition templates
- **Applicants**: Can view and satisfy conditions through portal

## Navigation Flow

### Primary Navigation Path

1. **User Login** → User logs into the system
2. **Setup Menu** → User navigates to Setup section
3. **Leasing Tab** → User selects Leasing tab
4. **Screening Section** → User navigates to Screening section
5. **Condition Templates** → User selects Condition Templates option
6. **Condition List View** → System displays list of available condition templates
7. **Action Selection** → User chooses an action:
   - **View**: Display condition template details
   - **Edit**: Modify existing condition template
   - **Create**: Build new condition template
   - **Copy**: Duplicate existing template
   - **Archive**: Remove template from active use

### URL Structure

**Primary Navigation**:
- Condition Templates: `/?module=screening_package_newconditionsxxx&action=view_screening_condition_templates`

**Condition Management**:
- View Template: `/?module=screening_package_newconditionsxxx&action=edit_screening_condition_template&screening_condition_set_id=[ID]`
- Add Template: `/?module=screening_package_newconditionsxxx&action=add_screening_condition_template`
- Manage Conditions: `/?module=screening_package_newconditionsxxx&action=add_edit_screening_available_conditions`

**Application Process**:
- View Conditions: `/?module=application_screeningsxxx&action=view_applied_conditions`
- Apply Conditions: `/?module=application_screeningsxxx&action=apply_screening_conditions`

## Main Files and Controllers

### Controllers

#### 1. CScreeningConditionTemplatesController.class.php
**Location**: `Applications/Entrata/Application/Setup/LeasingTab/Screening/ConditionTemplates/`

**Purpose**: Main controller for screening condition template management

**Key Methods**:
- `execute()`: Main entry point, handles different actions
- `handleViewScreeningConditionTemplates()`: Displays condition template list
- `handleAddScreeningConditionTemplate()`: Create new condition template
- `handleEditScreeningConditionTemplate()`: Edit existing template
- `handleCopyScreeningConditionTemplate()`: Duplicate template
- `handleArchiveScreeningConditionTemplate()`: Archive template
- `handleAddEditScreeningAvailableConditions()`: Manage available conditions

#### 2. CApplicationScreeningsController.class.php
**Location**: `Applications/Entrata/Application/Prospects/ApplicationsTab/Application/ApplicationScreenings/`

**Purpose**: Handles condition application during screening process

**Key Methods**:
- `handleViewAppliedConditions()`: Display conditions for application
- `handleApplyScreeningConditions()`: Apply conditions to application
- `handleSatisfyScreeningConditions()`: Mark conditions as satisfied
- `handleLoadScreeningPackageConditionSets()`: Load available condition sets

#### 3. CCentralizedScreeningDecisionController.class.php
**Location**: `Applications/Entrata/Application/Prospects/ApplicationsTab/Centralization/Screenings/`

**Purpose**: Centralized screening decision management including conditions

### Models

#### 1. CScreeningConditionSet.class.php
**Location**: `Eos/Screening/Base/CBaseScreeningConditionSet.class.php`

**Purpose**: Core condition set model

**Key Properties**:
- `$m_intId`: Condition set unique identifier
- `$m_intCid`: Company identifier
- `$m_strConditionName`: Name of the condition set
- `$m_intScreeningRecommendationTypeId`: Associated recommendation type
- `$m_intScreeningPackageOperandTypeId`: Logic type (AND/OR)
- `$m_intEvaluationOrder`: Priority order for evaluation
- `$m_boolIsTemplate`: Whether this is a template
- `$m_boolIsPublished`: Publication status

#### 2. CScreeningAvailableCondition.class.php
**Location**: `Eos/Screening/Base/CBaseScreeningAvailableCondition.class.php`

**Purpose**: Available condition types model

#### 3. CScreeningCondition.class.php
**Location**: `Eos/Screening/Base/CBaseScreeningCondition.class.php`

**Purpose**: Individual condition instance model

### Service Classes

#### 1. CScreeningConditionSets.php
**Location**: `Psi/Eos/Screening/CScreeningConditionSets.php`

**Purpose**: Service class for condition set operations

#### 2. CScreeningConditions.php
**Location**: `Psi/Eos/Screening/CScreeningConditions.php`

**Purpose**: Service class for condition operations

## Database Tables

### Core Tables

#### 1. screening_condition_sets
**Purpose**: Stores condition set templates

**Key Columns**:
- `id`: Primary key, unique identifier
- `cid`: Company identifier
- `screening_recommendation_type_id`: Associated recommendation type (PASS, FAIL, PASSWITHCONDITIONS)
- `screening_package_operand_type_id`: Logic type (1=AND, 2=OR)
- `condition_name`: Name of the condition set
- `evaluation_order`: Priority order for evaluation
- `is_template`: Whether this is a template (true/false)
- `is_published`: Publication status (true/false)
- `created_by`, `created_on`, `updated_by`, `updated_on`: Audit fields

#### 2. screening_available_conditions
**Purpose**: Stores available condition types

**Key Columns**:
- `id`: Primary key
- `cid`: Company identifier
- `screening_package_condition_type_id`: Condition type (financial, documentation, etc.)
- `condition_name`: Condition name
- `base_charge_code_id`: Base charge code
- `charge_type_id`: Charge type
- `is_published`: Publication status

#### 3. screening_conditions
**Purpose**: Stores individual condition instances

**Key Columns**:
- `id`: Primary key
- `cid`: Company identifier
- `screening_id`: Reference to screening
- `screening_package_condition_set_id`: Reference to condition set
- `is_active`: Active status
- `satisfied_by`: User who satisfied the condition
- `satisfied_on`: When condition was satisfied

#### 4. screening_condition_subsets
**Purpose**: Stores condition subsets within sets

#### 5. screening_condition_subset_values
**Purpose**: Links subsets to available conditions

### Supporting Tables

#### 6. screening_package_condition_types
**Purpose**: Defines condition types

#### 7. screening_package_operand_types
**Purpose**: Defines logic types

#### 8. screening_application_condition_sets
**Purpose**: Links applications to condition sets

#### 9. screening_application_condition_values
**Purpose**: Stores condition values for applications

## Key Functions

### Condition Template Management Functions

#### Create Condition Template
```php
public function createConditionTemplate($data) {
    $conditionSet = new CScreeningConditionSet();
    $conditionSet->setConditionName($data['condition_name']);
    $conditionSet->setScreeningRecommendationTypeId($data['recommendation_type_id']);
    $conditionSet->setScreeningPackageOperandTypeId($data['operand_type_id']);
    $conditionSet->setEvaluationOrder($data['evaluation_order']);
    $conditionSet->setIsTemplate(true);
    $conditionSet->setIsPublished(true);
    return $conditionSet->save();
}
```

#### Evaluate Condition Logic
```php
public function evaluateConditionLogic($conditionSet, $satisfiedConditions) {
    $subsetOneSatisfied = 0;
    $subsetTwoSatisfied = 0;

    // Count satisfied conditions in each subset
    foreach ($satisfiedConditions as $condition) {
        if ($condition->getSubsetId() == 1) {
            $subsetOneSatisfied++;
        } elseif ($condition->getSubsetId() == 2) {
            $subsetTwoSatisfied++;
        }
    }

    // Apply logic based on operand type
    if ($conditionSet->getScreeningPackageOperandTypeId() == CScreeningPackageOperandType::AND) {
        return ($subsetOneSatisfied >= $conditionSet->getRequiredItemsSubsetOne() &&
                $subsetTwoSatisfied >= $conditionSet->getRequiredItemsSubsetTwo());
    } else { // OR logic
        return ($subsetOneSatisfied >= $conditionSet->getRequiredItemsSubsetOne() ||
                $subsetTwoSatisfied >= $conditionSet->getRequiredItemsSubsetTwo());
    }
}
```

### Navigation Functions

#### Load Exit Tags
```php
public function loadExitTags() {
    // Condition template management
    $this->m_arrstrExitTags['view_screening_condition_templates'] =
        $this->m_strSecureBaseName . '/?module=screening_package_newconditionsxxx&action=view_screening_condition_templates';

    $this->m_arrstrExitTags['add_screening_condition_template'] =
        $this->m_strSecureBaseName . '/?module=screening_package_newconditionsxxx&action=add_screening_condition_template';

    $this->m_arrstrExitTags['edit_screening_condition_template'] =
        $this->m_strSecureBaseName . '/?module=screening_package_newconditionsxxx&action=edit_screening_condition_template';

    // Available conditions management
    $this->m_arrstrExitTags['add_edit_screening_available_conditions'] =
        $this->m_strSecureBaseName . '/?module=screening_package_newconditionsxxx&action=add_edit_screening_available_conditions';
}
```

## URL Structure

### Module Assignment
**File**: `Applications/Entrata/Application/AssignApplicationModules.php`

```php
// Screening condition controllers
'screening_package_newconditionsxxx' => './Setup/LeasingTab/Screening/ConditionTemplates/CScreeningConditionTemplatesController.class.php',

// Application screening controllers
'application_screeningsxxx' => './Prospects/ApplicationsTab/Application/ApplicationScreenings/CApplicationScreeningsController.class.php',

// Centralized screening controllers
'centralized_screening_decisionxxx' => './Prospects/ApplicationsTab/Centralization/Screenings/CCentralizedScreeningDecisionController.class.php',
```

### URL Patterns

**Condition Template Operations**:
- View Templates: `/?module=screening_package_newconditionsxxx&action=view_screening_condition_templates`
- Add Template: `/?module=screening_package_newconditionsxxx&action=add_screening_condition_template`
- Edit Template: `/?module=screening_package_newconditionsxxx&action=edit_screening_condition_template&screening_condition_set_id=[ID]`
- Copy Template: `/?module=screening_package_newconditionsxxx&action=copy_screening_condition_template`
- Archive Template: `/?module=screening_package_newconditionsxxx&action=archive_screening_condition_template`

**Available Conditions Operations**:
- Manage Conditions: `/?module=screening_package_newconditionsxxx&action=add_edit_screening_available_conditions`
- Update Conditions: `/?module=screening_package_newconditionsxxx&action=insert_or_update_screening_available_conditions`

**Application Process Operations**:
- View Applied Conditions: `/?module=application_screeningsxxx&action=view_applied_conditions`
- Apply Conditions: `/?module=application_screeningsxxx&action=apply_screening_conditions`
- Satisfy Conditions: `/?module=application_screeningsxxx&action=satisfy_screening_conditions`

## User Interface

### Navigation Elements

#### Primary Navigation
1. **Setup Menu** → User accesses setup section
2. **Leasing Tab** → User selects leasing options
3. **Screening Section** → User navigates to screening
4. **Condition Templates** → User selects condition management

#### Condition Template List Interface
- **Template Name**: Display name of the condition template
- **Conditions**: Description of condition logic
- **Evaluation Order**: Priority number for evaluation
- **Actions**: View, Edit, Copy, Archive buttons
- **Drag Handle**: For reordering templates

#### Condition Template Detail Interface
- **Template Information**: Name, description, recommendation type
- **Logic Configuration**: AND/OR logic selection
- **Subset 1**: First group of conditions and required items
- **Subset 2**: Second group of conditions and required items
- **Lease Types**: Associated lease types
- **Evaluation Order**: Priority setting

### Form Elements

#### Condition Template Creation Form
- **Template Name**: Text input for template name
- **Recommendation Type**: Dropdown (PASS, FAIL, PASSWITHCONDITIONS)
- **Logic Type**: Radio buttons (AND/OR)
- **Subset Configuration**: Condition selection for each subset
- **Required Items**: Number inputs for required conditions
- **Lease Types**: Checkboxes for supported lease types
- **Evaluation Order**: Number input for priority

#### Available Conditions Form
- **Condition Name**: Text input for condition name
- **Condition Type**: Dropdown (Financial, Documentation, Procedural)
- **Charge Code**: Dropdown for associated charge codes
- **Amount Type**: Dropdown for amount calculation
- **Rate Association**: Link to rate management
- **Integration Code**: Mapping to external systems

## Common Operations

### Creating a New Condition Template

1. **Navigate to Condition Templates**: Setup → Leasing → Screening → Condition Templates
2. **Click "Add Template"**: Opens condition template creation form
3. **Enter Basic Information**:
   - Template Name: "Pass with Conditions - Custom 1"
   - Recommendation Type: PASSWITHCONDITIONS
   - Logic Type: OR
4. **Configure Subset 1**:
   - Select Conditions: Increase Deposit, Add Guarantor
   - Required Items: 1
5. **Configure Subset 2**:
   - Select Conditions: Increase Rent, Provide Income Proof
   - Required Items: 2
6. **Set Lease Types**: New Lease, Renewal
7. **Set Evaluation Order**: 1
8. **Save Template**: Template is created and available for use

### Editing an Existing Condition Template

1. **Navigate to Condition Templates**: View all available templates
2. **Click Template Name**: Opens template detail view
3. **Select Edit Mode**: Click edit button
4. **Modify Settings**:
   - Update template name or description
   - Change logic type (AND/OR)
   - Modify condition subsets
   - Adjust required items
   - Change lease type associations
5. **Save Changes**: Updates are applied

### Managing Available Conditions

1. **Navigate to Condition Templates**: Access condition management
2. **Click "Manage Conditions"**: Opens available conditions form
3. **Add New Conditions**:
   - Enter condition name
   - Select condition type
   - Configure charge codes
   - Set up rates
4. **Edit Existing Conditions**:
   - Modify condition properties
   - Update charge associations
   - Adjust rate settings
5. **Save Changes**: Updates condition configuration

### Applying Conditions to Applications

1. **During Screening Process**: System evaluates screening results
2. **Condition Evaluation**: Check if conditions should be applied
3. **Condition Offer**: Present conditions to applicant
4. **Condition Selection**: Applicant chooses which conditions to satisfy
5. **Condition Satisfaction**: Track completion of conditions
6. **Final Approval**: Approve application when conditions are met

## Troubleshooting

### Common Issues

#### Condition Template Not Visible
**Problem**: Condition template not appearing in list

**Check**:
```sql
-- Verify template is published and active
SELECT id, condition_name, is_template, is_published
FROM screening_condition_sets
WHERE cid = [COMPANY_ID] AND id = [TEMPLATE_ID];

-- Check evaluation order
SELECT evaluation_order FROM screening_condition_sets
WHERE id = [TEMPLATE_ID];
```

**Solution**:
- Ensure template is published (`is_published = true`)
- Verify template flag is set (`is_template = true`)
- Check evaluation order is set correctly

#### Conditions Not Applying
**Problem**: Conditions not being applied to applications

**Check**:
```sql
-- Verify condition set is associated with screening package
SELECT * FROM screening_package_condition_sets
WHERE screening_package_id = [PACKAGE_ID] AND condition_set_id = [CONDITION_SET_ID];

-- Check screening recommendation type
SELECT screening_recommendation_type_id FROM screening_condition_sets
WHERE id = [CONDITION_SET_ID];
```

**Solution**:
- Ensure condition set is associated with screening package
- Verify recommendation type matches screening result
- Check evaluation order and logic

#### Condition Logic Not Working
**Problem**: AND/OR logic not evaluating correctly

**Check**:
```sql
-- Verify subset configuration
SELECT * FROM screening_condition_subsets
WHERE screening_condition_set_id = [CONDITION_SET_ID];

-- Check subset values
SELECT * FROM screening_condition_subset_values
WHERE screening_condition_subset_id = [SUBSET_ID];
```

**Solution**:
- Verify subset configuration is correct
- Check required items count
- Ensure operand type is set correctly

### Debug Commands

#### Check Condition Template Status
```php
// Debug condition template loading
$templates = CScreeningConditionSets::createService()
    ->fetchActiveScreeningConditionTemplatesByCid($companyId, $database);

foreach ($templates as $template) {
    echo "Template: " . $template->getConditionName() . " (ID: " . $template->getId() . ")\n";
    echo "Published: " . ($template->getIsPublished() ? 'Yes' : 'No') . "\n";
    echo "Evaluation Order: " . $template->getEvaluationOrder() . "\n";
}
```

#### Verify Condition Logic
```php
// Test condition evaluation
$conditionSet = CScreeningConditionSet::loadById($conditionSetId);
$satisfiedConditions = $this->getSatisfiedConditions($applicationId);

$isSatisfied = $this->evaluateConditionLogic($conditionSet, $satisfiedConditions);
echo "Condition Set Satisfied: " . ($isSatisfied ? 'Yes' : 'No') . "\n";
```

### Performance Optimization

#### Database Queries
```sql
-- Add indexes for better performance
CREATE INDEX idx_screening_condition_sets_cid_template ON screening_condition_sets(cid, is_template);
CREATE INDEX idx_screening_condition_sets_evaluation_order ON screening_condition_sets(evaluation_order);
CREATE INDEX idx_screening_conditions_screening_id ON screening_conditions(screening_id);
CREATE INDEX idx_screening_application_condition_sets_app_id ON screening_application_condition_sets(application_id);
```

#### Caching
```php
// Cache frequently accessed data
$cacheKey = "condition_templates_" . $companyId;
$templates = Cache::get($cacheKey);

if (!$templates) {
    $templates = CScreeningConditionSets::createService()
        ->fetchActiveScreeningConditionTemplatesByCid($companyId, $database);
    Cache::set($cacheKey, $templates, 3600); // Cache for 1 hour
}
```

## Webhook Integration

### Document Verification Webhooks

#### CDocumentVerificationWebhook Class
**Location**: `Applications/Entrata/Application/Webhooks/DocumentVerification/`

**Purpose**: Processes document verification webhook notifications from Resident Verify Portal

**Key Methods**:
- `processWebhook($request)`: Main webhook processing method
- `validateRequest($request)`: Validates incoming webhook request
- `verifySignature($payload, $signature, $secret)`: Verifies HMAC-SHA256 signature
- `updateDocumentVerification($data)`: Updates document verification details
- `evaluateResults($verificationData)`: Evaluates verification results
- `updateScreeningStatus($screeningId, $status)`: Updates screening status
- `logActivity($action, $data)`: Logs webhook activities

**Webhook Flow**:
1. **Receive Webhook**: System receives POST request from Resident Verify
2. **Validate Request**: Check request format and required fields
3. **Verify Signature**: Validate HMAC-SHA256 signature for security
4. **Process Data**: Extract and validate document verification data
5. **Update Records**: Update screening and application records
6. **Evaluate Results**: Determine if verification passes/fails
7. **Update Status**: Update screening status based on results
8. **Log Activity**: Record webhook processing for audit trail

**Security Features**:
- **HMAC-SHA256 Signature Verification**: Ensures webhook authenticity
- **Request Validation**: Validates all required fields
- **Error Handling**: Comprehensive error handling and logging
- **Rate Limiting**: Prevents webhook abuse
- **Audit Logging**: Tracks all webhook activities

### Webhook Payload Structure

#### Document Verification Webhook Payload
```json
{
  "webhook_id": "unique_webhook_identifier",
  "timestamp": "2024-01-15T10:30:00Z",
  "event_type": "document_verification_completed",
  "verification_id": "verification_unique_id",
  "application_id": "application_unique_id",
  "document_type": "pay_stub",
  "verification_status": "verified",
  "verification_score": 95.5,
  "verification_details": {
    "employer_name": "ABC Company",
    "employer_address": "123 Main St, City, State",
    "employment_start_date": "2020-01-15",
    "employment_end_date": null,
    "position": "Software Engineer",
    "salary": 75000,
    "pay_frequency": "bi-weekly"
  },
  "verification_metadata": {
    "verification_method": "automated",
    "verification_provider": "Resident Verify",
    "verification_date": "2024-01-15T10:25:00Z",
    "processing_time": 2.5
  },
  "signature": "hmac_sha256_signature_here"
}
```

#### Webhook Response
```json
{
  "status": "success",
  "message": "Document verification processed successfully",
  "processing_id": "processing_unique_id",
  "timestamp": "2024-01-15T10:30:05Z"
}
```

## Security and Permissions

### Permission System

#### User Roles
- **Property Manager**: Full access to condition management
- **Leasing Agent**: View and apply conditions
- **System Administrator**: Global condition configuration
- **Applicant**: View assigned conditions through portal

#### Permission Checks
```php
// Check user permissions for condition management
public function checkConditionPermissions($userId, $action) {
    $user = CUser::loadById($userId);
    
    switch($action) {
        case 'create_template':
            return $user->hasPermission('screening_conditions_create');
        case 'edit_template':
            return $user->hasPermission('screening_conditions_edit');
        case 'delete_template':
            return $user->hasPermission('screening_conditions_delete');
        case 'apply_conditions':
            return $user->hasPermission('screening_conditions_apply');
        default:
            return false;
    }
}
```

### Data Security

#### Input Validation
```php
// Validate condition template data
public function validateConditionTemplate($data) {
    $errors = [];
    
    if (empty($data['condition_name'])) {
        $errors[] = 'Condition name is required';
    }
    
    if (!in_array($data['recommendation_type_id'], [1, 2, 3])) {
        $errors[] = 'Invalid recommendation type';
    }
    
    if (!in_array($data['operand_type_id'], [1, 2])) {
        $errors[] = 'Invalid operand type';
    }
    
    return $errors;
}
```

#### SQL Injection Prevention
```php
// Use prepared statements for all database operations
public function fetchConditionTemplates($companyId) {
    $sql = "SELECT * FROM screening_condition_sets 
            WHERE cid = ? AND is_template = true 
            ORDER BY evaluation_order";
    
    $stmt = $this->m_objDatabase->prepare($sql);
    $stmt->bind_param('i', $companyId);
    $stmt->execute();
    
    return $stmt->get_result()->fetch_all(MYSQLI_ASSOC);
}
```

### Audit Trail

#### Activity Logging
```php
// Log condition template changes
public function logConditionTemplateChange($templateId, $action, $userId, $changes = []) {
    $log = new CScreeningConditionLog();
    $log->setConditionId($templateId);
    $log->setAction($action);
    $log->setUserId($userId);
    $log->setActionDate(date('Y-m-d H:i:s'));
    $log->setOldValues(json_encode($changes['old'] ?? []));
    $log->setNewValues(json_encode($changes['new'] ?? []));
    $log->setNotes($changes['notes'] ?? '');
    $log->save();
}
```

---

## Summary

This comprehensive documentation covers all aspects of screening conditions in the Entrata system, including:

- **Business Logic**: How conditions work and their purpose
- **Navigation**: How users access and manage conditions
- **Technical Implementation**: Controllers, models, and database structure
- **User Interface**: Forms and interaction elements
- **Common Operations**: Step-by-step procedures
- **Troubleshooting**: Common issues and solutions
- **Webhook Integration**: Document verification processing
- **Security**: Permissions and data protection

The documentation provides both high-level business understanding and detailed technical implementation guidance for developers, administrators, and end users working with screening conditions.
