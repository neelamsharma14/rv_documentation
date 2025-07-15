# Screening Packages Navigation - Text Only Documentation

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

## Overview

Screening package navigation in Entrata provides the interface and routing system for managing screening packages throughout the application. It enables users to create, edit, view, and manage screening packages from various entry points in the system.

### What are Screening Packages?

Screening packages are collections of background checks (credit, criminal, income verification, etc.) that are applied together to evaluate rental applications. Think of them as "recipes" for what to check when screening an applicant.

### Key Components

- **Navigation Controllers**: Handle routing and request processing
- **UI Templates**: Provide the user interface
- **Database Models**: Manage data persistence
- **Permission System**: Control access to screening features
- **URL Routing**: Define application endpoints

### Entry Points

1. **Setup → Leasing → Screening → Packages** (Primary)
2. **Property Preferences → Screening** (Property-specific)
3. **Financial → Vendors → Screening Packages** (Legacy)
4. **Application Screening Process** (Runtime)

## Business Explanation

### Purpose

Screening package navigation serves several business purposes:

1. **Package Management**: Create and configure screening packages for different property types and lease scenarios
2. **Property Association**: Link screening packages to specific properties
3. **Criteria Configuration**: Set up evaluation rules and thresholds
4. **Condition Management**: Define approval conditions and requirements
5. **Workflow Integration**: Integrate with the application screening process

### Business Rules

1. **Package Types**: Different package types for different scenarios
   - Standard (Conventional) - Basic screening for regular applicants
   - Student - Specialized for student applicants
   - Affordable - Modified criteria for affordable programs
   - Corporate - Enhanced screening for business clients
   - VA Corporate - Specialized for VA housing
   - VA Criminal - VA-specific criminal screening
   - Ban the Box - Fair chance housing
   - Military - Specialized for military personnel

2. **Property Association**: Packages must be associated with properties to be used
3. **Lease Type Compatibility**: Packages specify which lease types they support
4. **Permission Requirements**: Users need specific permissions to manage packages
5. **Active Status**: Only active packages can be used in screening

### User Roles and Access

- **Property Managers**: Can view and select packages for their properties
- **Leasing Agents**: Can use packages during application screening
- **System Administrators**: Can create, edit, and manage all packages
- **Corporate Users**: May have access to corporate-specific packages

## Navigation Flow

### Primary Navigation Path

1. **User Login** → User logs into the system
2. **Setup Menu** → User navigates to Setup section
3. **Leasing Tab** → User selects Leasing tab
4. **Screening Section** → User navigates to Screening section
5. **Packages** → User selects Packages option
6. **Package List View** → System displays list of available packages
7. **Action Selection** → User chooses an action:
   - **View**: Display package details
   - **Edit**: Modify existing package
   - **Create**: Build new package
   - **Copy**: Duplicate existing package
   - **Delete**: Remove package

### Package Detail Navigation

When viewing a package, users can access:
- **Package Information**: Basic details and settings
- **Screen Types**: What background checks are performed
- **Criteria**: Evaluation rules and thresholds
- **Conditions**: Additional requirements for approval
- **Properties**: Associated properties

### Secondary Navigation Paths

**Property Preferences Path**:
1. Property Preferences → Screening Section
2. Package Association → Select Packages
3. Set Default Packages → Configure defaults
4. Save Preferences → Store settings

**Application Process Path**:
1. Application Process → Screening Step
2. Package Selection → Choose appropriate package
3. Execute Screening → Run background checks
4. Review Results → Evaluate outcomes

### URL Structure

**Primary Navigation**:
- Package List: `/?module=screening_packages_newxxx&action=view_screening_packages`

**Package Management**:
- View Package: `/?module=screening_package_newxxx&action=view_screening_package&screening_package[id]=[ID]`
- Edit Package: `/?module=screening_package_newxxx&action=edit_screening_package&screening_package[id]=[ID]`
- Create Package: `/?module=screening_package_newxxx&action=create_new_screening_package`

**Property Association**:
- Associate Properties: `/?module=property_leasing_screeningxxx&action=associate_property_packages`

## Main Files and Controllers

### Controllers

#### 1. CScreeningPackagesNewController.class.php
**Location**: `Applications/Entrata/Application/Setup/LeasingTab/Screening/Packages/Package_New/Package/`

**Purpose**: Main controller for screening package list management

**Key Methods**:
- `execute()`: Main entry point, handles different actions
- `handleViewScreeningPackages()`: Displays package list
- `handleActivateOrDeactivateScreeningPackage()`: Toggles package status
- `handleCopyScreeningPackage()`: Duplicates existing package
- `handleFilterScreeningPackagesByProperties()`: Filters packages by property

**Responsibilities**:
- List Management: View, filter, and manage package lists
- Bulk Operations: Copy, activate/deactivate packages
- Property Filtering: Filter packages by property association

#### 2. CScreeningPackageNewController.class.php
**Location**: `Applications/Entrata/Application/Setup/LeasingTab/Screening/Packages/Package_New/Package/`

**Purpose**: Individual package management (create, edit, view)

**Key Methods**:
- `execute()`: Main entry point for package actions
- `handleViewScreeningPackage()`: Display package details
- `handleCreateNewScreeningPackage()`: Create new package
- `handleUpdateScreeningPackage()`: Update existing package
- `handleScreeningPackageScreenTypeCriteria()`: Manage criteria

**Responsibilities**:
- Individual Package Management: Create, edit, view individual packages
- Criteria Management: Configure screening criteria for packages
- Property Association: Manage property associations
- Package History: Track package changes and usage

#### 3. CBaseScreeningPackagesNewController.class.php
**Location**: `Applications/Entrata/Application/Setup/LeasingTab/Screening/Packages/Package_New/Package/`

**Purpose**: Base controller with common functionality

**Key Methods**:
- `loadExitTags()`: Sets up navigation URLs
- `loadScreeningDatabase()`: Connects to screening database
- `checkPermissions()`: Validates user access

**Responsibilities**:
- Common Functionality: Shared methods and properties
- Exit Tags: URL generation for navigation
- Database Access: Screening database connections
- Permission Management: Access control and validation

### Models

#### 1. CScreeningPackage.class.php
**Location**: `Eos/Shared/Base/CBaseScreeningPackage.class.php`

**Purpose**: Core screening package model

**Key Properties**:
- `$m_intId`: Package unique identifier
- `$m_intCid`: Company identifier
- `$m_strName`: Package name
- `$m_intScreeningPackageTypeId`: Package type (Conventional, Student, etc.)
- `$m_boolIsActive`: Whether package is active
- `$m_boolIsUseForPrescreening`: Enable tiered screening
- `$m_arrintScreeningPackageLeaseTypeIds`: Supported lease types

**Key Methods**:
- `setName($strName)`: Set package name
- `getName()`: Get package name
- `setIsActive($boolIsActive)`: Set active status
- `getIsActive()`: Get active status
- `toArray()`: Convert to array format
- `applyRequestForm($arrData)`: Apply form data to model

#### 2. CScreeningPackages.php
**Location**: `Psi/Eos/Screening/CScreeningPackages.php`

**Purpose**: Service class for screening package operations

**Key Methods**:
- `fetchPublishedScreeningPackagesByCid($intCid, $objDatabase)`: Get active packages for company
- `fetchScreeningPackageByIdByCid($intId, $intCid, $objDatabase)`: Get specific package
- `createScreeningPackage($data)`: Create new package
- `updateScreeningPackage($package)`: Update existing package
- `deleteScreeningPackage($packageId)`: Remove package

### Templates

#### 1. view_screening_packages.tpl
**Location**: `Interfaces/Templates/Entrata/setup/leasing_tab/screening/package_new/packages/`

**Purpose**: Main package list view

**Key Features**:
- Package list table with sortable columns
- Action buttons for create, edit, copy, delete
- Property filtering options
- Status indicators (active/inactive)

#### 2. view_screening_package.tpl
**Location**: `Interfaces/Templates/Entrata/setup/leasing_tab/screening/package_new/packages/`

**Purpose**: Individual package detail view

**Key Features**:
- Tabbed interface for different sections
- Package information display
- Screen type configuration
- Property association management
- History tracking

## Database Tables

### Core Tables

#### 1. screening_packages
**Purpose**: Stores main package information

**Key Columns**:
- `id`: Primary key, unique identifier
- `cid`: Company identifier
- `parent_package_id`: Reference to parent package (for inheritance)
- `screening_package_type_id`: Package type (1=Conventional, 2=Student, etc.)
- `name`: Package name
- `description`: Package description
- `is_use_for_prescreening`: Boolean for tiered screening
- `is_published`: Publication status (1=published, 0=draft)
- `is_active`: Active status (true/false)
- `screening_package_lease_type_ids`: Array of supported lease types
- `created_by`: User who created the package
- `created_on`: Creation timestamp
- `updated_by`: User who last updated
- `updated_on`: Last update timestamp

**Sample Data**:
```
id: 1
name: "Lease Holder - Package 1"
screening_package_type_id: 1
is_active: true
is_published: 1
lease_types: [1, 2, 3] (New Lease, Renewal, Transfer)
```

#### 2. screening_package_screen_type_associations
**Purpose**: Links packages to screen types and criteria

**Key Columns**:
- `id`: Primary key
- `screening_package_id`: Reference to screening package
- `screen_type_id`: Reference to screen type (1=Credit, 2=Criminal, etc.)
- `screening_criteria_id`: Reference to criteria for this screen type
- `screening_data_provider_id`: Reference to data provider
- `is_published`: Publication status
- `created_by`, `created_on`, `updated_by`, `updated_on`: Audit fields

**Sample Data**:
```
screening_package_id: 1
screen_type_id: 1 (Credit)
screening_criteria_id: 5
is_published: 1
```

#### 3. screening_packages_properties
**Purpose**: Associates packages with properties

**Key Columns**:
- `id`: Primary key
- `cid`: Company identifier
- `property_id`: Reference to property
- `screening_package_id`: Reference to screening package
- `screening_package_name`: Package name (denormalized)
- `is_active`: Active status
- `created_by`, `created_on`, `updated_by`, `updated_on`: Audit fields

**Sample Data**:
```
property_id: 101
screening_package_id: 1
screening_package_name: "Lease Holder - Package 1"
is_active: 1
```

#### 4. screening_package_types
**Purpose**: Defines available package types

**Key Columns**:
- `id`: Primary key
- `name`: Type name (Conventional, Student, etc.)
- `description`: Type description
- `is_published`: Publication status
- `order_num`: Display order

**Sample Data**:
```
id: 1
name: "Conventional"
description: "Standard screening for regular applicants"
is_published: 1
order_num: 1
```

### Supporting Tables

#### 5. screening_criterias
**Purpose**: Stores criteria templates

**Key Columns**:
- `id`: Primary key
- `name`: Criteria name
- `screen_type_id`: Associated screen type
- `is_published`: Publication status
- `created_by`, `created_on`, `updated_by`, `updated_on`: Audit fields

#### 6. screening_criteria_settings
**Purpose**: Stores individual criteria rules

**Key Columns**:
- `id`: Primary key
- `screening_criteria_id`: Reference to criteria
- `screening_config_preference_type_id`: Type of setting (credit score, DTI ratio, etc.)
- `screening_config_value_type_id`: Value type (percentage, flag, date, etc.)
- `required_min_value`: Minimum threshold
- `required_max_value`: Maximum threshold
- `screening_recommendation_type_id`: Recommendation when condition met

#### 7. screening_package_condition_sets
**Purpose**: Stores condition templates

**Key Columns**:
- `id`: Primary key
- `screening_package_id`: Reference to package
- `name`: Condition set name
- `screening_recommendation_type_id`: Recommendation type
- `operand_type_id`: Logic type (1=AND, 2=OR)
- `required_items_subset_one`: Required items from first subset
- `required_items_subset_two`: Required items from second subset
- `is_active`: Active status

#### 8. screening_package_conditions
**Purpose**: Stores individual conditions

**Key Columns**:
- `id`: Primary key
- `screening_package_condition_set_id`: Reference to condition set
- `condition_type_id`: Type of condition (financial, documentation, etc.)
- `condition_value_type_id`: Value type
- `condition_value`: Condition value
- `subset_id`: Which subset this condition belongs to (1 or 2)

## Key Functions

### Package Management Functions

#### Create Package
```php
public function createScreeningPackage($data) {
    $package = new CScreeningPackage();
    $package->setName($data['name']);
    $package->setScreeningPackageTypeId($data['package_type_id']);
    $package->setIsActive(true);
    $package->setScreeningPackageLeaseTypeIds($data['lease_type_ids']);
    return $package->save();
}
```

#### Load Package List
```php
public function loadScreeningPackages($companyId) {
    $sql = "SELECT * FROM screening_packages
            WHERE cid = ? AND is_published = 1 AND is_active = true
            ORDER BY name";
    return $this->fetchScreeningPackages($sql, $this->m_objScreeningDatabase, [$companyId]);
}
```

#### Associate Properties
```php
public function associatePackageWithProperties($packageId, $propertyIds) {
    foreach ($propertyIds as $propertyId) {
        $association = new CScreeningPackagesProperties();
        $association->setScreeningPackageId($packageId);
        $association->setPropertyId($propertyId);
        $association->setIsActive(1);
        $association->save();
    }
}
```

### Navigation Functions

#### Load Exit Tags
```php
public function loadExitTags() {
    // Plural Exit Tags (Package Lists)
    $this->m_arrstrExitTags['view_screening_packages'] =
        $this->m_strSecureBaseName . '/?module=screening_packages_newxxx&action=view_screening_packages';

    // Singular Exit Tags (Individual Packages)
    $this->m_arrstrExitTags['view_screening_package'] =
        $this->m_strSecureBaseName . '/?module=screening_package_newxxx&action=view_screening_package';
}
```

#### Handle Package Actions
```php
public function execute() {
    switch($this->getRequestAction()) {
        case 'view_screening_packages':
            $this->handleViewScreeningPackages();
            break;
        case 'create_new_screening_package':
            $this->handleCreateNewScreeningPackage();
            break;
        case 'update_screening_package':
            $this->handleUpdateScreeningPackage();
            break;
    }
}
```

## URL Structure

### Module Assignment
**File**: `Applications/Entrata/Application/AssignApplicationModules.php`

```php
// Screening package controllers
'screening_packages_newxxx' => './Setup/LeasingTab/Screening/Packages/Package_New/Package/CScreeningPackagesNewController.class.php',
'screening_package_newxxx' => './Setup/LeasingTab/Screening/Packages/Package_New/Package/CScreeningPackageNewController.class.php',

// Supporting controllers
'screening_package_newconditionsxxx' => './Setup/LeasingTab/Screening/ConditionTemplates/CScreeningConditionTemplatesController.class.php',
'screening_package_newcriteriasxxx' => './Setup/LeasingTab/Screening/Packages/Package_New/Criteria/CScreeningPackageCriteriasNewController.class.php',
```

### URL Patterns

**Package List Operations**:
- View Packages: `/?module=screening_packages_newxxx&action=view_screening_packages`
- Filter by Properties: `/?module=screening_packages_newxxx&action=filter_screening_packages_by_properties`
- Activate/Deactivate: `/?module=screening_packages_newxxx&action=activate_or_deactivate_screening_package`
- Copy Package: `/?module=screening_packages_newxxx&action=copy_screening_package`

**Individual Package Operations**:
- View Package: `/?module=screening_package_newxxx&action=view_screening_package&screening_package[id]=[ID]`
- Create Package: `/?module=screening_package_newxxx&action=create_new_screening_package`
- Edit Package: `/?module=screening_package_newxxx&action=edit_screening_package&screening_package[id]=[ID]`
- Update Package: `/?module=screening_package_newxxx&action=update_screening_package`

### Exit Tags
```php
// Plural Exit Tags (Package Lists)
'view_screening_packages' => '/?module=screening_packages_newxxx&action=view_screening_packages'
'activate_or_deactivate_screening_package' => '/?module=screening_packages_newxxx&action=activate_or_deactivate_screening_package'
'copy_screening_package' => '/?module=screening_packages_newxxx&action=copy_screening_package'

// Singular Exit Tags (Individual Packages)
'view_screening_package' => '/?module=screening_package_newxxx&action=view_screening_package'
'update_screening_package' => '/?module=screening_package_newxxx&action=update_screening_package'
'create_new_screening_package' => '/?module=screening_package_newxxx&action=create_new_screening_package'
```

## User Interface

### Navigation Elements

#### Primary Navigation
1. **Setup Menu** → User accesses setup section
2. **Leasing Tab** → User selects leasing options
3. **Screening Section** → User navigates to screening
4. **Packages** → User selects package management

#### Package List Interface
- **Package Name**: Display name of the package
- **Lease Type**: Supported lease types (New Lease, Renewal, etc.)
- **Associated Properties**: Number of properties using this package
- **Last Update**: When package was last modified
- **Actions**: View, Edit, Copy, Delete buttons

#### Package Detail Interface
- **Package Details Tab**: Basic information and settings
- **Screen Types Tabs**: Credit, Criminal, Income, Identity, etc.
- **Criteria Tab**: Evaluation rules and thresholds
- **Conditions Tab**: Additional requirements
- **Properties Tab**: Associated properties
- **History Tab**: Change tracking

### Form Elements

#### Package Creation Form
- **Package Name**: Text input for package name
- **Package Type**: Dropdown with available types
- **Lease Types**: Checkboxes for supported lease types
- **Screen Types**: Checkboxes for background checks
- **Properties**: Multi-select for property association

#### Package Edit Form
- **Basic Information**: Name, type, description
- **Screen Type Configuration**: Criteria selection for each screen type
- **Property Association**: Add/remove property associations
- **Advanced Settings**: Prescreening, waterfalls, international credit

## Common Operations

### Creating a New Package

1. **Navigate to Package List**: Setup → Leasing → Screening → Packages
2. **Click "Add Package"**: Opens package creation form
3. **Enter Basic Information**:
   - Package Name: "Premium Screening Package"
   - Package Type: Conventional
   - Lease Types: New Lease, Renewal
4. **Select Screen Types**:
   - Credit Check
   - Criminal Background
   - Income Verification
   - Identity Verification
5. **Associate Properties**: Select properties that can use this package
6. **Save Package**: Package is created and available for use

### Editing an Existing Package

1. **Navigate to Package List**: View all available packages
2. **Click Package Name**: Opens package detail view
3. **Select Edit Mode**: Click edit button
4. **Modify Settings**:
   - Update package name or description
   - Change screen type associations
   - Modify property associations
   - Adjust criteria settings
5. **Save Changes**: Updates are applied

### Copying a Package

1. **Navigate to Package List**: View existing packages
2. **Click Copy Icon**: Duplicates the package
3. **Modify as Needed**: Update name and settings
4. **Save New Package**: Creates new package based on original

### Associating Packages with Properties

1. **Navigate to Package Details**: Open specific package
2. **Select Properties Tab**: View current associations
3. **Add Properties**: Check properties to associate
4. **Remove Properties**: Uncheck properties to disassociate
5. **Save Changes**: Updates property associations

## Troubleshooting

### Common Issues

#### Package Not Visible
**Problem**: Screening package not appearing in list

**Check**:
```sql
-- Verify package is active and published
SELECT id, name, is_active, is_published
FROM screening_packages
WHERE cid = [COMPANY_ID] AND id = [PACKAGE_ID];

-- Check property association
SELECT * FROM screening_packages_properties
WHERE screening_package_id = [PACKAGE_ID] AND property_id = [PROPERTY_ID];
```

**Solution**:
- Ensure package is active (`is_active = true`)
- Verify package is published (`is_published = 1`)
- Check property association exists

#### Navigation Not Working
**Problem**: Links not responding or redirecting incorrectly

**Check**:
- Verify exit tags are loaded in controller
- Check module assignment in `AssignApplicationModules.php`
- Look for JavaScript errors in browser console

**Solution**:
- Ensure exit tags are properly loaded in controller
- Verify module is assigned correctly
- Check for JavaScript errors

#### Permission Denied
**Problem**: User cannot access screening packages

**Check**:
```sql
-- Verify user permissions
SELECT * FROM user_permissions
WHERE user_id = [USER_ID] AND module_name = 'screening_packages_newxxx';

-- Check company access
SELECT * FROM company_users
WHERE user_id = [USER_ID] AND cid = [COMPANY_ID];
```

**Solution**:
- Grant appropriate permissions to user
- Verify user is associated with correct company
- Check module permissions in system settings

### Debug Commands

#### Check Package Status
```php
// Debug package loading
$packages = CScreeningPackages::createService()
    ->fetchPublishedScreeningPackagesByCid($companyId, $database);

foreach ($packages as $package) {
    echo "Package: " . $package->getName() . " (ID: " . $package->getId() . ")\n";
    echo "Active: " . ($package->getIsActive() ? 'Yes' : 'No') . "\n";
    echo "Published: " . $package->getIsPublished() . "\n";
}
```

#### Verify Navigation Structure
```php
// Check navigation items
$navigationItems = $this->getPrimaryNavigationItems();
foreach ($navigationItems as $key => $item) {
    echo "Navigation: $key => " . $item['navigation_text'] . "\n";
}
```

#### Test URL Generation
```php
// Test exit tag generation
$exitTags = $this->m_arrstrExitTags;
foreach ($exitTags as $key => $url) {
    echo "Exit Tag: $key => $url\n";
}
```

### Performance Optimization

#### Database Queries
```sql
-- Add indexes for better performance
CREATE INDEX idx_screening_packages_cid_active ON screening_packages(cid, is_active);
CREATE INDEX idx_screening_packages_properties_package ON screening_packages_properties(screening_package_id);
CREATE INDEX idx_screening_package_screen_type_assoc_package ON screening_package_screen_type_associations(screening_package_id);
```

#### Caching
```php
// Cache frequently accessed data
$cacheKey = "screening_packages_" . $companyId;
$packages = Cache::get($cacheKey);

if (!$packages) {
    $packages = CScreeningPackages::createService()
        ->fetchPublishedScreeningPackagesByCid($companyId, $database);
    Cache::set($cacheKey, $packages, 3600); // Cache for 1 hour
}
```

This text-only documentation provides comprehensive information about screening package navigation, business logic, file structure, database schema, and troubleshooting without relying on visual diagrams.
