# Screening Criteria Templates Complete Documentation

## Table of Contents
1. [Overview](#overview)
2. [Business Explanation](#business-explanation)
3. [Navigation](#navigation)
4. [Configuration](#configuration)
5. [Business Flow](#business-flow)
6. [Main Files](#main-files)
7. [Main Tables](#main-tables)
8. [Key Functions](#key-functions)
9. [User Interface](#user-interface)
10. [Common Operations](#common-operations)
11. [Troubleshooting](#troubleshooting)

## Overview

Screening criteria templates in Entrata define the evaluation rules and thresholds used to assess applicant screening results. Think of them as "grading rubrics" that determine whether an applicant passes, fails, or needs additional conditions to be approved.

### What are Screening Criteria Templates?

Screening criteria templates are configurable rule sets that define:
- **Evaluation thresholds** (minimum credit score, maximum criminal records, etc.)
- **Recommendation logic** (PASS, FAIL, PASSWITHCONDITIONS)
- **Condition triggers** (when to apply additional requirements)
- **Screen type specific rules** (credit, criminal, income verification, etc.)

### Key Components

- **Criteria Templates**: Reusable evaluation rule sets
- **Criteria Settings**: Specific thresholds and values
- **Screen Type Associations**: Link criteria to specific background checks
- **Condition Sets**: Define additional requirements when criteria aren't fully met
- **Filter Rules**: Time-based and category-specific filtering

### Entry Points

1. **Setup → Leasing → Screening → Criteria Templates** (Primary)
2. **Package Management → Criteria Tab** (Package-specific)
3. **Screen Type Management** (Screen type-specific)
4. **Application Screening Process** (Runtime evaluation)

## Business Explanation

### Purpose

Screening criteria templates serve several critical business purposes:

1. **Standardized Evaluation**: Ensure consistent applicant assessment across properties
2. **Risk Management**: Define acceptable risk thresholds for different applicant types
3. **Compliance**: Meet legal and regulatory requirements for tenant screening
4. **Flexibility**: Allow property-specific customization of screening standards
5. **Automation**: Enable automated decision-making based on screening results

### Business Rules

1. **Screen Type Specificity**: Each criteria template is designed for specific screen types
   - **Credit Criteria**: Credit score thresholds, debt-to-income ratios, payment history
   - **Criminal Criteria**: Felony/misdemeanor classifications, time-based filtering
   - **Income Criteria**: Income verification, employment history, pay frequency
   - **Identity Criteria**: Identity verification, fraud detection
   - **Rental History**: Previous rental performance, eviction history

2. **Recommendation Types**:
   - **PASS**: Applicant meets all criteria requirements
   - **FAIL**: Applicant does not meet minimum requirements
   - **PASSWITHCONDITIONS**: Applicant meets basic requirements but needs additional conditions

3. **Condition Integration**: Criteria can trigger condition sets for borderline applicants
4. **Time-Based Filtering**: Criminal records and rental history can be filtered by time periods
5. **Category Classification**: Criminal offenses can be categorized by severity and type

### User Roles and Access

- **Property Managers**: Can view and select criteria templates for their properties
- **Leasing Agents**: Can use criteria during application screening
- **System Administrators**: Can create, edit, and manage all criteria templates
- **Corporate Users**: May have access to corporate-specific criteria

## Navigation

### Primary Navigation Path

1. **User Login** → User logs into the system
2. **Setup Menu** → User navigates to Setup section
3. **Leasing Tab** → User selects Leasing tab
4. **Screening Section** → User navigates to Screening section
5. **Criteria Templates** → User selects Criteria Templates option
6. **Screen Type Selection** → User chooses screen type (Credit, Criminal, Income, etc.)
7. **Criteria List View** → System displays available criteria templates for selected screen type
8. **Action Selection** → User chooses an action:
   - **View**: Display criteria template details
   - **Edit**: Modify existing criteria template
   - **Create**: Build new criteria template
   - **Copy**: Duplicate existing template
   - **Publish**: Make template available for use

### URL Structure

**Primary Navigation**:
- Criteria Templates: `/?module=screening_package_newcriteriasxxx&action=view_screening_package_criterias`

**Screen Type Specific**:
- View Screen Type Criteria: `/?module=screening_package_newcriteriasxxx&action=view_screen_type_criterias&screen_type=[ID]`
- View Criteria Template: `/?module=screening_package_newcriteriasxxx&action=view_criteria_template&screening_criteria_id=[ID]`

**Package Integration**:
- Package Criteria: `/?module=screening_package_newxxx&action=view_screening_package_screen_type_criteria&screening_package[id]=[ID]&screen_type_id=[ID]`

### Secondary Navigation Paths

**Package Management Path**:
1. Package Details → Criteria Tab
2. Screen Type Selection → Choose screen type
3. Criteria Template Selection → Select or create criteria
4. Configuration → Set thresholds and rules
5. Save and Publish → Make criteria active

**Application Process Path**:
1. Application Screening → Execute background checks
2. Criteria Evaluation → Apply selected criteria templates
3. Result Assessment → Determine recommendation
4. Condition Application → Apply conditions if needed

## Configuration

### Criteria Template Configuration

#### Basic Information
- **Template Name**: Human-readable name for the criteria template
- **Screen Type**: Associated screen type (Credit, Criminal, Income, etc.)
- **Description**: Detailed explanation of the criteria purpose
- **Status**: Draft, Published, Archived

#### Evaluation Settings
- **Recommendation Logic**: How to determine PASS/FAIL/PASSWITHCONDITIONS
- **Threshold Values**: Minimum/maximum acceptable values
- **Required Conditions**: Mandatory criteria that must be met
- **Optional Conditions**: Additional criteria that can influence decisions

#### Filter Configuration
- **Time-Based Filters**: How far back to look for records
- **Category Filters**: Specific types of records to include/exclude
- **Geographic Filters**: Regional restrictions on records
- **Severity Filters**: Classification of offense severity

### Screen Type Specific Configuration

#### Credit Criteria
- **Credit Score Thresholds**: Minimum acceptable credit scores
- **Debt-to-Income Ratios**: Maximum acceptable debt ratios
- **Payment History**: Required payment performance standards
- **Collection Accounts**: Treatment of collection accounts
- **Bankruptcy History**: Time-based bankruptcy restrictions

#### Criminal Criteria
- **Felony Classifications**: Categories of felony offenses
- **Misdemeanor Classifications**: Categories of misdemeanor offenses
- **Time-Based Filtering**: How recent offenses affect decisions
- **Offense Categories**: Specific types of criminal activity
- **Geographic Restrictions**: State/local record considerations

#### Income Criteria
- **Income Verification**: Required income documentation
- **Employment History**: Minimum employment duration
- **Income Thresholds**: Minimum income requirements
- **Pay Frequency**: Acceptable payment schedules
- **Additional Income**: Treatment of secondary income sources

#### Identity Criteria
- **Identity Verification**: Required identity documentation
- **Fraud Detection**: Fraud prevention measures
- **Address Verification**: Address confirmation requirements
- **Document Authentication**: Document validation standards

### Condition Set Integration

#### Condition Triggers
- **Automatic Conditions**: Conditions applied based on criteria results
- **Manual Conditions**: Conditions applied by leasing staff
- **Condition Logic**: AND/OR logic for multiple conditions
- **Condition Priority**: Order of condition evaluation

#### Condition Types
- **Financial Conditions**: Increased deposits, higher rent
- **Documentation Conditions**: Additional documentation requirements
- **Procedural Conditions**: Additional steps or verifications

## Business Flow

### Criteria Template Creation Flow

```
1. Navigate to Criteria Templates
2. Select Screen Type (Credit, Criminal, Income, etc.)
3. Click "Add Template"
4. Enter Basic Information:
   - Template Name
   - Description
   - Screen Type Association
5. Configure Evaluation Settings:
   - Set thresholds and values
   - Define recommendation logic
   - Configure filters
6. Set up Condition Integration:
   - Link condition sets
   - Define trigger conditions
   - Set evaluation order
7. Save as Draft
8. Test with Sample Data
9. Publish Template
10. Associate with Screening Packages
```

### Application Screening Flow

```
1. Applicant Submits Application
2. System Identifies Screening Package
3. Package Contains Screen Type Associations
4. Each Screen Type Has Associated Criteria Template
5. Background Checks Execute:
   - Credit check
   - Criminal background check
   - Income verification
   - Identity verification
6. Results Evaluated Against Criteria:
   - Compare results to thresholds
   - Apply filter rules
   - Determine recommendation
7. Generate Screening Decision:
   - PASS: Approve application
   - FAIL: Deny application
   - PASSWITHCONDITIONS: Apply conditions
8. Apply Conditions if Needed
9. Final Decision Made
```

### Criteria Evaluation Process

```
1. Load Criteria Template for Screen Type
2. Retrieve Screening Results
3. Apply Time-Based Filters:
   - Filter records by date ranges
   - Apply geographic restrictions
   - Apply category filters
4. Evaluate Against Thresholds:
   - Compare values to minimum/maximum requirements
   - Check required conditions
   - Assess optional conditions
5. Determine Recommendation:
   - All criteria met: PASS
   - Critical criteria failed: FAIL
   - Some criteria failed: PASSWITHCONDITIONS
6. Trigger Condition Sets if Needed
7. Return Evaluation Results
```

## Main Files

### Controllers

#### 1. CScreeningPackageCriteriasNewController.class.php
**Location**: `Applications/Entrata/Application/Setup/LeasingTab/Screening/Packages/Package_New/Criteria/`

**Purpose**: Main controller for screening criteria template management

**Key Methods**:
- `execute()`: Main entry point, handles different actions
- `handleViewScreeningPackageCriterias()`: Displays criteria template list
- `handleViewScreenTypeCriterias()`: Shows criteria for specific screen type
- `handleViewCriteriaTemplate()`: Displays individual criteria template details
- `handleLoadCriminalKeywordSubCategories()`: Manages criminal subcategories
- `handleManageCriminalSubCategories()`: Criminal category management
- `handleCreateOffenseSubCategories()`: Creates offense subcategories
- `handleSaveClassificationSubCategories()`: Saves classification categories

**Responsibilities**:
- Criteria Template Management: Create, edit, view, publish criteria templates
- Screen Type Integration: Link criteria to specific screen types
- Criminal Classification: Manage criminal offense categories
- Permission Management: Control access to criteria features

#### 2. CScreeningPackageCriteriaNewController.class.php
**Location**: `Applications/Entrata/Application/Setup/LeasingTab/Screening/Packages/Package_New/Criteria/`

**Purpose**: Individual criteria template management

**Key Methods**:
- `handleCreateScreeningCriteria()`: Create new criteria template
- `handleEditScreeningCriteria()`: Edit existing criteria template
- `handleUpdateScreeningCriteria()`: Update criteria template
- `handlePublishScreeningCriteria()`: Publish criteria template

#### 3. CScreeningPackageNewController.class.php
**Location**: `Applications/Entrata/Application/Setup/LeasingTab/Screening/Packages/Package_New/Package/`

**Purpose**: Package-level criteria integration

**Key Methods**:
- `handleViewScreeningPackageScreenTypeCriteria()`: View criteria for package screen type
- `handleViewCriteriaTemplates()`: Display available criteria templates
- `handleChangeCriteriaTemplate()`: Change criteria template association

### Models

#### 1. CScreeningCriteria.class.php
**Location**: `Eos/Screening/Base/CBaseScreeningCriteria.class.php`

**Purpose**: Core criteria template model

**Key Properties**:
- `$m_intId`: Criteria unique identifier
- `$m_intCid`: Company identifier
- `$m_strCriteriaName`: Name of the criteria template
- `$m_intScreenTypeId`: Associated screen type
- `$m_strDescription`: Criteria description
- `$m_boolIsPublished`: Publication status
- `$m_boolIsTemplate`: Whether this is a template
- `$m_intCreatedBy`: User who created the criteria
- `$m_strCreatedOn`: When criteria was created

**Key Methods**:
- `setCriteriaName($strName)`: Set criteria name
- `getCriteriaName()`: Get criteria name
- `setScreenTypeId($intType)`: Set screen type
- `getScreenTypeId()`: Get screen type
- `setIsPublished($boolPublished)`: Set publication status
- `getIsPublished()`: Get publication status
- `toArray()`: Convert to array format
- `applyRequestForm($arrData)`: Apply form data to model

#### 2. CScreeningCriteriaSetting.class.php
**Location**: `Eos/Screening/Base/CBaseScreeningCriteriaSetting.class.php`

**Purpose**: Individual criteria settings model

**Key Properties**:
- `$m_intId`: Setting unique identifier
- `$m_intScreeningCriteriaId`: Reference to criteria template
- `$m_intScreeningConfigPreferenceTypeId`: Configuration preference type
- `$m_intScreeningConditionSetId`: Associated condition set
- `$m_intRequiredMinValue`: Minimum required value
- `$m_intRequiredMaxValue`: Maximum required value
- `$m_boolIsActive`: Active status

**Key Methods**:
- `setScreeningCriteriaId($intId)`: Set criteria reference
- `getScreeningCriteriaId()`: Get criteria reference
- `setRequiredMinValue($intValue)`: Set minimum value
- `getRequiredMinValue()`: Get minimum value
- `setRequiredMaxValue($intValue)`: Set maximum value
- `getRequiredMaxValue()`: Get maximum value

#### 3. CScreeningCriteriaConfigPreferenceTypeFilter.class.php
**Location**: `Eos/Screening/Base/CBaseScreeningCriteriaConfigPreferenceTypeFilter.class.php`

**Purpose**: Criteria filter configuration model

**Key Properties**:
- `$m_intId`: Filter unique identifier
- `$m_intScreeningCriteriaId`: Reference to criteria template
- `$m_intScreeningConfigPreferenceTypeId`: Configuration preference type
- `$m_intScreeningFilterId`: Associated filter
- `$m_boolIsActive`: Active status
- `$m_intExcludeFrom`: Exclude from value
- `$m_intExcludeTo`: Exclude to value

### Service Classes

#### 1. CScreeningCriterias.php
**Location**: `Psi/Eos/Screening/CScreeningCriterias.php`

**Purpose**: Service class for criteria operations

**Key Methods**:
- `fetchPublishedScreeningCriteriasByScreenTypeIdByCid($intScreenTypeId, $intCid, $objDatabase)`: Get published criteria by screen type
- `fetchScreeningCriteriaByIdByCid($intId, $intCid, $objDatabase)`: Get specific criteria
- `fetchActiveScreeningCriteriasByCid($intCid, $objDatabase)`: Get active criteria by company

#### 2. CScreeningCriteriaSettings.php
**Location**: `Psi/Eos/Screening/CScreeningCriteriaSettings.php`

**Purpose**: Service class for criteria settings operations

**Key Methods**:
- `fetchActiveScreeningCriteriaSettingsDataByScreeningCriteriaId($intCriteriaId, $objDatabase)`: Get active settings for criteria
- `fetchScreeningCriteriaSettingsByScreeningCriteriaId($intCriteriaId, $objDatabase)`: Get all settings for criteria
- `fetchScreeningCriteriaSettingsByScreeningPackageIdsByCid($arrintPackageIds, $intCid, $objDatabase)`: Get settings by package IDs

#### 3. CScreeningCriteriaConfigPreferenceTypeFilters.php
**Location**: `Psi/Eos/Screening/CScreeningCriteriaConfigPreferenceTypeFilters.php`

**Purpose**: Service class for criteria filter operations

**Key Methods**:
- `fetchActiveScreeningCriteriaConfigPreferenceTypeFiltersByScreeningCriteriaId($intCriteriaId, $objDatabase)`: Get active filters for criteria
- `fetchActiveScreeningCriteriaConfigPreferenceTypeFiltersByScreenTypeId($intScreenTypeId, $objDatabase)`: Get filters by screen type

### Templates

#### 1. view_screening_package_criterias.tpl
**Location**: `Interfaces/Templates/Entrata/setup/leasing_tab/screening/package_new/criterias/`

**Purpose**: Main criteria template list view

**Key Features**:
- Screen type tabs for different background checks
- Criteria template list with sortable columns
- Action buttons for create, edit, copy, publish
- Permission-based button visibility
- AJAX loading for dynamic content

#### 2. view_screen_type_criterias.tpl
**Location**: `Interfaces/Templates/Entrata/setup/leasing_tab/screening/package_new/criterias/`

**Purpose**: Screen type specific criteria view

**Key Features**:
- Criteria template list for specific screen type
- Template status indicators
- Quick action buttons
- Search and filter capabilities

#### 3. view_criteria_template.tpl
**Location**: `Interfaces/Templates/Entrata/setup/leasing_tab/screening/package_new/criterias/`

**Purpose**: Individual criteria template detail view

**Key Features**:
- Template information display
- Configuration preference settings
- Filter configuration
- Condition set associations
- Search action configuration

## Main Tables

### Core Tables

#### 1. screening_criterias
**Purpose**: Stores criteria template definitions

**Key Columns**:
- `id`: Primary key, unique identifier
- `cid`: Company identifier
- `criteria_name`: Name of the criteria template
- `screen_type_id`: Associated screen type (credit, criminal, income, etc.)
- `description`: Detailed description of the criteria
- `is_published`: Publication status (true/false)
- `is_template`: Whether this is a template (true/false)
- `created_by`, `created_on`, `updated_by`, `updated_on`: Audit fields

**Sample Data**:
```
id: 1
criteria_name: "Standard Credit Criteria"
screen_type_id: 1 (Credit)
description: "Standard credit evaluation criteria for conventional applicants"
is_published: true
is_template: true
```

#### 2. screening_criteria_settings
**Purpose**: Stores individual criteria configuration settings

**Key Columns**:
- `id`: Primary key
- `screening_criteria_id`: Reference to criteria template
- `screening_config_preference_type_id`: Configuration preference type
- `screening_condition_set_id`: Associated condition set
- `required_min_value`: Minimum required value
- `required_max_value`: Maximum required value
- `is_active`: Active status
- `created_by`, `created_on`, `updated_by`, `updated_on`: Audit fields

**Sample Data**:
```
screening_criteria_id: 1
screening_config_preference_type_id: 1 (Credit Score)
required_min_value: 650
required_max_value: null
screening_condition_set_id: 2
is_active: true
```

#### 3. screening_criteria_config_preference_type_filters
**Purpose**: Stores filter configurations for criteria

**Key Columns**:
- `id`: Primary key
- `screening_criteria_id`: Reference to criteria template
- `screening_config_preference_type_id`: Configuration preference type
- `screening_filter_id`: Associated filter
- `is_active`: Active status
- `exclude_from`: Exclude from value (for time-based filters)
- `exclude_to`: Exclude to value (for time-based filters)
- `created_by`, `created_on`, `updated_by`, `updated_on`: Audit fields

**Sample Data**:
```
screening_criteria_id: 1
screening_config_preference_type_id: 3 (Criminal Records)
screening_filter_id: 1 (Time-based filter)
exclude_from: 7 (7 years)
exclude_to: null
is_active: true
```

#### 4. screening_criteria_condition_sets
**Purpose**: Links criteria templates to condition sets

**Key Columns**:
- `id`: Primary key
- `screening_criteria_id`: Reference to criteria template
- `screening_condition_set_id`: Reference to condition set
- `is_active`: Active status
- `created_by`, `created_on`, `updated_by`, `updated_on`: Audit fields

**Sample Data**:
```
screening_criteria_id: 1
screening_condition_set_id: 3
is_active: true
```

#### 5. screening_criteria_screen_type_actions
**Purpose**: Stores search actions for criteria

**Key Columns**:
- `id`: Primary key
- `screening_criteria_id`: Reference to criteria template
- `screening_config_preference_type_id`: Configuration preference type
- `screen_type_id`: Associated screen type
- `screening_search_action_id`: Associated search action
- `is_published`: Publication status
- `created_by`, `created_on`, `updated_by`, `updated_on`: Audit fields

### Supporting Tables

#### 6. screening_config_preference_types
**Purpose**: Defines configuration preference types

**Key Columns**:
- `id`: Primary key
- `name`: Preference type name
- `screening_config_value_type_id`: Value type
- `description`: Type description
- `is_published`: Publication status
- `order_num`: Display order

#### 7. screening_config_preference_type_filters
**Purpose**: Defines available filters for preference types

**Key Columns**:
- `id`: Primary key
- `screening_config_preference_type_id`: Reference to preference type
- `screening_filter_id`: Reference to filter
- `is_active`: Active status
- `order_num`: Display order

#### 8. screening_filters
**Purpose**: Defines available screening filters

**Key Columns**:
- `id`: Primary key
- `name`: Filter name
- `screening_filter_type_id`: Filter type
- `description`: Filter description
- `is_published`: Publication status

#### 9. screening_package_screen_type_associations
**Purpose**: Links screening packages to criteria templates

**Key Columns**:
- `id`: Primary key
- `screening_package_id`: Reference to screening package
- `screen_type_id`: Reference to screen type
- `screening_criteria_id`: Reference to criteria template
- `is_published`: Publication status
- `created_by`, `created_on`, `updated_by`, `updated_on`: Audit fields

### Criminal-Specific Tables

#### 10. criminal_criteria_settings
**Purpose**: Stores criminal-specific criteria settings

**Key Columns**:
- `id`: Primary key
- `cid`: Company identifier
- `screening_criteria_id`: Reference to criteria template
- `criminal_classification_type_id`: Criminal classification type
- `felony_screening_package_condition_set_id`: Felony condition set
- `misdemeanor_screening_package_condition_set_id`: Misdemeanor condition set
- `felony_years`: Felony time restriction
- `misdemeanor_years`: Misdemeanor time restriction
- `created_by`, `created_on`, `updated_by`, `updated_on`: Audit fields

#### 11. client_criminal_classification_subtypes
**Purpose**: Stores client-specific criminal classifications

**Key Columns**:
- `id`: Primary key
- `cid`: Company identifier
- `screening_criteria_id`: Reference to criteria template
- `criminal_classification_type_id`: Classification type
- `subtype_name`: Subtype name
- `is_active`: Active status
- `created_by`, `created_on`, `updated_by`, `updated_on`: Audit fields

## Key Functions

### Criteria Template Management Functions

#### Create Criteria Template
```php
public function createCriteriaTemplate($data) {
    $criteria = new CScreeningCriteria();
    $criteria->setCriteriaName($data['criteria_name']);
    $criteria->setScreenTypeId($data['screen_type_id']);
    $criteria->setDescription($data['description']);
    $criteria->setIsTemplate(true);
    $criteria->setIsPublished(false); // Start as draft
    return $criteria->save();
}
```

#### Load Criteria Templates by Screen Type
```php
public function loadCriteriaTemplatesByScreenType($screenTypeId, $companyId) {
    $sql = "SELECT * FROM screening_criterias
            WHERE screen_type_id = ? AND cid = ? AND is_published = true
            ORDER BY criteria_name";
    return $this->fetchCriteriaTemplates($sql, $this->m_objScreeningDatabase, [$screenTypeId, $companyId]);
}
```

#### Evaluate Criteria Against Results
```php
public function evaluateCriteria($criteriaId, $screeningResults) {
    // Load criteria settings
    $settings = CScreeningCriteriaSettings::createService()
        ->fetchActiveScreeningCriteriaSettingsDataByScreeningCriteriaId($criteriaId, $this->m_objScreeningDatabase);

    // Load filters
    $filters = CScreeningCriteriaConfigPreferenceTypeFilters::createService()
        ->fetchActiveScreeningCriteriaConfigPreferenceTypeFiltersByScreeningCriteriaId($criteriaId, $this->m_objScreeningDatabase);

    $evaluation = new CScreeningEvaluation();

    foreach ($settings as $setting) {
        $result = $this->evaluateSetting($setting, $screeningResults, $filters);
        $evaluation->addResult($result);
    }

    return $evaluation->getRecommendation();
}
```

#### Apply Filters to Results
```php
public function applyFilters($results, $filters) {
    $filteredResults = $results;

    foreach ($filters as $filter) {
        switch ($filter->getScreeningFilterTypeId()) {
            case CScreeningFilterType::TIMELINE_FILTER:
                $filteredResults = $this->applyTimelineFilter($filteredResults, $filter);
                break;
            case CScreeningFilterType::CATEGORY_FILTER:
                $filteredResults = $this->applyCategoryFilter($filteredResults, $filter);
                break;
            case CScreeningFilterType::GEOGRAPHIC_FILTER:
                $filteredResults = $this->applyGeographicFilter($filteredResults, $filter);
                break;
        }
    }

    return $filteredResults;
}
```

### Navigation Functions

#### Load Exit Tags
```php
public function loadExitTags() {
    // Criteria template management
    $this->m_arrstrExitTags['view_screening_package_criterias'] =
        $this->m_strSecureBaseName . '/?module=screening_package_newcriteriasxxx&action=view_screening_package_criterias';

    $this->m_arrstrExitTags['view_screen_type_criterias'] =
        $this->m_strSecureBaseName . '/?module=screening_package_newcriteriasxxx&action=view_screen_type_criterias';

    $this->m_arrstrExitTags['view_criteria_template'] =
        $this->m_strSecureBaseName . '/?module=screening_package_newcriteriasxxx&action=view_criteria_template';

    // Package integration
    $this->m_arrstrExitTags['view_screening_package_screen_type_criteria'] =
        $this->m_strSecureBaseName . '/?module=screening_package_newxxx&action=view_screening_package_screen_type_criteria';
}
```

#### Handle Criteria Actions
```php
public function execute() {
    switch($this->getRequestAction()) {
        case 'view_screening_package_criterias':
            $this->handleViewScreeningPackageCriterias();
            break;
        case 'view_screen_type_criterias':
            $this->handleViewScreenTypeCriterias();
            break;
        case 'view_criteria_template':
            $this->handleViewCriteriaTemplate();
            break;
        case 'load_criminal_keyword_sub_categories':
            $this->handleLoadCriminalKeywordSubCategories();
            break;
        case 'manage_criminal_sub_categories':
            $this->handleManageCriminalSubCategories();
            break;
    }
}
```

### Criminal Classification Functions

#### Load Criminal Subcategories
```php
public function loadCriminalSubcategories($criteriaId) {
    $sql = "SELECT * FROM client_criminal_classification_subtypes
            WHERE screening_criteria_id = ? AND is_active = true
            ORDER BY subtype_name";
    return $this->fetchCriminalSubcategories($sql, [$criteriaId]);
}
```

#### Save Classification Subcategories
```php
public function saveClassificationSubcategories($criteriaId, $subcategories) {
    foreach ($subcategories as $subcategory) {
        $clientSubtype = new CClientCriminalClassificationSubtype();
        $clientSubtype->setScreeningCriteriaId($criteriaId);
        $clientSubtype->setCriminalClassificationTypeId($subcategory['type_id']);
        $clientSubtype->setSubtypeName($subcategory['name']);
        $clientSubtype->setIsActive(true);
        $clientSubtype->save();
    }
}
```

## User Interface

### Navigation Elements

#### Primary Navigation
1. **Setup Menu** → User accesses setup section
2. **Leasing Tab** → User selects leasing options
3. **Screening Section** → User navigates to screening
4. **Criteria Templates** → User selects criteria management

#### Screen Type Tabs
- **Credit**: Credit score and payment history criteria
- **Criminal**: Criminal background check criteria
- **Income**: Income verification criteria
- **Identity**: Identity verification criteria
- **Rental History**: Previous rental performance criteria

#### Criteria Template List Interface
- **Template Name**: Display name of the criteria template
- **Screen Type**: Associated screen type
- **Status**: Published/Draft/Archived
- **Last Updated**: When template was last modified
- **Actions**: View, Edit, Copy, Publish buttons

#### Criteria Template Detail Interface
- **Template Information**: Name, description, screen type
- **Configuration Preferences**: Settings for each preference type
- **Filter Configuration**: Time-based and category filters
- **Condition Sets**: Associated condition sets
- **Search Actions**: Search action configuration

### Form Elements

#### Criteria Template Creation Form
- **Template Name**: Text input for template name
- **Screen Type**: Dropdown with available screen types
- **Description**: Textarea for detailed description
- **Configuration Preferences**: Dynamic form based on screen type
- **Filter Settings**: Time-based and category filter options
- **Condition Set Association**: Dropdown for condition sets

#### Configuration Preference Form
- **Preference Type**: Display name of preference type
- **Minimum Value**: Number input for minimum threshold
- **Maximum Value**: Number input for maximum threshold
- **Condition Set**: Dropdown for associated condition set
- **Active Status**: Checkbox for active/inactive

#### Filter Configuration Form
- **Filter Type**: Display name of filter type
- **Time Range**: Date inputs for time-based filters
- **Category Selection**: Checkboxes for category filters
- **Geographic Options**: Dropdown for geographic filters
- **Active Status**: Checkbox for active/inactive

## Common Operations

### Creating a New Criteria Template

1. **Navigate to Criteria Templates**: Setup → Leasing → Screening → Criteria Templates
2. **Select Screen Type**: Choose the screen type (Credit, Criminal, Income, etc.)
3. **Click "Add Template"**: Opens criteria template creation form
4. **Enter Basic Information**:
   - Template Name: "Standard Credit Criteria"
   - Screen Type: Credit
   - Description: "Standard credit evaluation criteria for conventional applicants"
5. **Configure Settings**:
   - Credit Score: Minimum 650
   - Debt-to-Income Ratio: Maximum 40%
   - Payment History: No more than 2 late payments in 12 months
6. **Set up Filters**:
   - Time-based: Look back 7 years for credit history
   - Category: Include all account types
7. **Associate Condition Sets**:
   - Link to "Pass with Conditions" condition set
8. **Save as Draft**: Template is created but not published
9. **Test Configuration**: Verify settings work correctly
10. **Publish Template**: Make template available for use

### Editing an Existing Criteria Template

1. **Navigate to Criteria Templates**: View all available templates
2. **Select Screen Type**: Choose the appropriate screen type tab
3. **Click Template Name**: Opens template detail view
4. **Select Edit Mode**: Click edit button
5. **Modify Settings**:
   - Update template name or description
   - Adjust threshold values
   - Modify filter settings
   - Change condition set associations
6. **Save Changes**: Updates are applied
7. **Test Changes**: Verify modifications work correctly
8. **Publish Updates**: Make changes available

### Managing Criminal Classifications

1. **Navigate to Criminal Criteria**: Select Criminal screen type tab
2. **Select Criteria Template**: Choose the template to modify
3. **Click "Manage Classifications"**: Opens classification management
4. **Add Subcategories**:
   - Enter subcategory name
   - Select classification type
   - Set time restrictions
   - Define condition sets
5. **Configure Keywords**:
   - Add keyword associations
   - Set severity levels
   - Define automatic actions
6. **Save Classifications**: Store subcategory configurations
7. **Test Classifications**: Verify criminal evaluation works correctly

### Publishing Criteria Templates

1. **Review Template**: Ensure all settings are correct
2. **Test with Sample Data**: Verify evaluation logic works
3. **Check Dependencies**: Ensure condition sets are published
4. **Click "Publish"**: Make template available for use
5. **Associate with Packages**: Link to screening packages
6. **Monitor Usage**: Track template usage in applications
7. **Gather Feedback**: Collect user feedback on template performance

### Applying Criteria to Applications

1. **During Screening Process**: System identifies screening package
2. **Load Criteria Templates**: Retrieve associated criteria for each screen type
3. **Execute Background Checks**: Run credit, criminal, income checks
4. **Apply Filters**: Filter results based on criteria configuration
5. **Evaluate Results**: Compare results against thresholds
6. **Generate Recommendation**: Determine PASS/FAIL/PASSWITHCONDITIONS
7. **Apply Conditions**: Trigger condition sets if needed
8. **Final Decision**: Complete screening evaluation

## Troubleshooting

### Common Issues

#### Criteria Template Not Visible
**Problem**: Criteria template not appearing in list

**Check**:
```sql
-- Verify template is published and active
SELECT id, criteria_name, screen_type_id, is_published
FROM screening_criterias
WHERE cid = [COMPANY_ID] AND id = [TEMPLATE_ID];

-- Check screen type association
SELECT screen_type_id FROM screening_criterias
WHERE id = [TEMPLATE_ID];
```

**Solution**:
- Ensure template is published (`is_published = true`)
- Verify screen type association is correct
- Check company ID matches current company

#### Criteria Not Evaluating Correctly
**Problem**: Criteria evaluation not working as expected

**Check**:
```sql
-- Verify criteria settings
SELECT * FROM screening_criteria_settings
WHERE screening_criteria_id = [CRITERIA_ID] AND is_active = true;

-- Check filter configuration
SELECT * FROM screening_criteria_config_preference_type_filters
WHERE screening_criteria_id = [CRITERIA_ID] AND is_active = true;
```

**Solution**:
- Verify all required settings are configured
- Check filter values are appropriate
- Ensure condition sets are properly linked

#### Criminal Classifications Not Working
**Problem**: Criminal criteria not properly classifying offenses

**Check**:
```sql
-- Verify criminal criteria settings
SELECT * FROM criminal_criteria_settings
WHERE screening_criteria_id = [CRITERIA_ID];

-- Check subcategory configuration
SELECT * FROM client_criminal_classification_subtypes
WHERE screening_criteria_id = [CRITERIA_ID] AND is_active = true;
```

**Solution**:
- Ensure criminal criteria settings are configured
- Verify subcategories are properly set up
- Check keyword associations are correct

### Debug Commands

#### Check Criteria Template Status
```php
// Debug criteria template loading
$templates = CScreeningCriterias::createService()
    ->fetchPublishedScreeningCriteriasByScreenTypeIdByCid($screenTypeId, $companyId, $database);

foreach ($templates as $template) {
    echo "Template: " . $template->getCriteriaName() . " (ID: " . $template->getId() . ")\n";
    echo "Screen Type: " . $template->getScreenTypeId() . "\n";
    echo "Published: " . ($template->getIsPublished() ? 'Yes' : 'No') . "\n";
}
```

#### Verify Criteria Evaluation
```php
// Test criteria evaluation
$criteriaId = 1;
$screeningResults = $this->getScreeningResults($applicationId);

$recommendation = $this->evaluateCriteria($criteriaId, $screeningResults);
echo "Criteria Evaluation Result: " . $recommendation . "\n";
```

#### Test Filter Application
```php
// Test filter application
$results = $this->getRawScreeningResults($applicationId);
$filters = $this->loadCriteriaFilters($criteriaId);

$filteredResults = $this->applyFilters($results, $filters);
echo "Filtered Results Count: " . count($filteredResults) . "\n";
```

### Performance Optimization

#### Database Queries
```sql
-- Add indexes for better performance
CREATE INDEX idx_screening_criterias_cid_screen_type ON screening_criterias(cid, screen_type_id);
CREATE INDEX idx_screening_criterias_published ON screening_criterias(is_published);
CREATE INDEX idx_screening_criteria_settings_criteria_id ON screening_criteria_settings(screening_criteria_id);
CREATE INDEX idx_screening_criteria_filters_criteria_id ON screening_criteria_config_preference_type_filters(screening_criteria_id);
```

#### Caching
```php
// Cache frequently accessed data
$cacheKey = "criteria_templates_" . $screenTypeId . "_" . $companyId;
$templates = Cache::get($cacheKey);

if (!$templates) {
    $templates = CScreeningCriterias::createService()
        ->fetchPublishedScreeningCriteriasByScreenTypeIdByCid($screenTypeId, $companyId, $database);
    Cache::set($cacheKey, $templates, 3600); // Cache for 1 hour
}
```

---

## Summary

This comprehensive documentation covers all aspects of screening criteria templates in the Entrata system, including:

- **Business Logic**: How criteria templates work and their purpose
- **Navigation**: How users access and manage criteria templates
- **Configuration**: Detailed setup and configuration options
- **Business Flow**: Step-by-step processes for creation and evaluation
- **Technical Implementation**: Controllers, models, and database structure
- **User Interface**: Forms and interaction elements
- **Common Operations**: Practical procedures for daily use
- **Troubleshooting**: Common issues and solutions

The documentation provides both high-level business understanding and detailed technical implementation guidance for developers, administrators, and end users working with screening criteria templates.
