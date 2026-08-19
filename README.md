# Release Governance App

**Release Governance App** is a Salesforce application designed to provide structured governance and control over Salesforce deployment and release activities.

The application helps teams manage deployment requests, deployment tasks, approvals, release activities, and deployment audit history directly within Salesforce.

## Overview

Release Governance App provides a controlled release-management process for Salesforce teams.

The application supports a governance workflow such as:

```text
Create Deployment Request
        ↓
Create Deployment Tasks
        ↓
Complete Deployment Tasks
        ↓
Submit Deployment Request
        ↓
Approval Request
        ↓
Release Manager Approval / Rejection
        ↓
Approved
        ↓
Deployment
        ↓
Deployment Audit
```

The application is designed to help organizations establish a consistent and auditable release process across Salesforce environments.

---

## Key Features

### Deployment Request Management

Create and manage deployment requests with information such as:

* Deployment Request Number
* Environment
* Requested By
* Deployment Date
* Status
* Comments

Supported deployment statuses include:

* **Draft**
* **Submitted**
* **Approved**
* **Deployed**

### Deployment Task Management

Deployment requests can contain multiple deployment tasks.

Typical tasks include:

* Code Review
* Unit Testing
* QA Testing
* Approval
* Production Validation

Tasks can track:

* Task Type
* Assigned User
* Status
* Due Date
* Deployment Request

Task status can be managed through the application's governance rules.

### Approval Management

When the required deployment tasks are completed, the Deployment Request can move to **Submitted**.

An Approval Request is then created for the appropriate approval process.

The Release Manager can:

* Approve the request
* Reject the request
* Provide comments

The application updates the Deployment Request according to the approval decision.

### Automated Notifications

The application can send email notifications for important release events, including:

* Deployment Request approval
* Deployment Request rejection
* Approval activities

### Deployment Audit

Release Governance App maintains deployment audit information for governance, compliance, and reporting.

Audit information can include:

* Deployment Request
* Approval Request
* Action
* Action Date
* Performed By

### Governance and Security

The application uses Salesforce security and governance mechanisms to control release activities.

These include:

* Permission Sets
* Custom Permissions
* Validation Rules
* Flow-based automation
* Role-based governance
* Audit records

The application is designed to prevent unauthorized users from performing restricted release activities.

---

## Application Components

The application includes Salesforce metadata such as:

### Custom Objects

* `Deployment_Request__c`
* `Deployment_Task__c`
* `Approval_Request__c`
* `Deployment_Audit__c`
* `Release_Team__c`
* `Release_Governance_Settings__mdt`

### Automation

The application uses Salesforce Flow for release governance automation, including processes for:

* Creating deployment tasks
* Validating task completion
* Creating approval requests
* Processing approval decisions
* Updating deployment status
* Creating deployment audit records
* Sending notifications

### User Interface

The application includes Salesforce Lightning components such as:

* Lightning App
* Custom Tabs
* Record Pages
* Reports
* Dashboards
* Permission Sets

---

## Release Governance Process

The recommended release process is:

### 1. Create Deployment Request

A user creates a Deployment Request with the required deployment information.

Initial status:

**Draft**

### 2. Deployment Tasks

The application creates the required deployment tasks.

Each task is assigned to the appropriate user or release team member.

### 3. Complete Tasks

Assigned users complete their deployment tasks.

The application validates task completion according to the configured governance rules.

### 4. Submit Request

Once all required deployment tasks are completed, the Deployment Request can move to:

**Submitted**

### 5. Approval

An Approval Request is created.

The Release Manager reviews the deployment request and can approve or reject it.

### 6. Approval Decision

If approved:

**Submitted → Approved**

If rejected:

**Submitted → Rejected**

### 7. Deployment

After approval, the deployment can proceed according to the organization's release process.

### 8. Audit

The application records relevant release actions in Deployment Audit records.

---

## Project Structure

This project follows the Salesforce DX source format.

```text
.
├── force-app/
│   └── main/
│       └── default/
│           ├── applications/
│           ├── classes/
│           ├── customMetadata/
│           ├── customPermissions/
│           ├── dashboards/
│           ├── flows/
│           ├── layouts/
│           ├── objects/
│           ├── permissionsets/
│           ├── reports/
│           ├── tabs/
│           └── ...
│
├── manifest/
│   └── package.xml
│
├── config/
│   └── ...
│
├── sfdx-project.json
└── README.md
```

---

## Prerequisites

Before working with the project, install:

* Salesforce CLI
* Visual Studio Code
* Salesforce Extension Pack
* Access to a Salesforce development environment

Salesforce CLI:

https://developer.salesforce.com/tools/salesforcecli

Salesforce VS Code Extensions:

https://developer.salesforce.com/tools/vscode/

---

## Salesforce DX Commands

Authorize a Salesforce org:

```bash
sf org login web
```

List authorized orgs:

```bash
sf org list
```

Open an org:

```bash
sf org open -o <ORG_ALIAS>
```

Deploy metadata:

```bash
sf project deploy start -o <ORG_ALIAS>
```

Retrieve metadata:

```bash
sf project retrieve start -o <ORG_ALIAS>
```

Deploy using a manifest:

```bash
sf project deploy start -x manifest/package.xml -o <ORG_ALIAS>
```

Retrieve using a manifest:

```bash
sf project retrieve start -x manifest/package.xml -o <ORG_ALIAS>
```

Run Apex tests:

```bash
sf apex run test
```

---

## Development

The application is developed using Salesforce DX source-driven development.

Recommended development process:

```text
Salesforce Org
      ↓
Retrieve / Develop
      ↓
VS Code
      ↓
Git
      ↓
Validate
      ↓
Deploy
      ↓
Test
      ↓
Package
```

All Salesforce metadata should be maintained in source control.

---

## Packaging

Release Governance App is being prepared as a Salesforce ISV application using Salesforce managed packaging.

The project is intended to support Salesforce packaging and distribution through the Salesforce partner ecosystem.

Packaging-related configuration is maintained in:

```text
sfdx-project.json
```

The project should be validated in the appropriate Salesforce packaging/development environments before creating a managed package version.

---

## Testing

Before releasing a package version, validate:

### Functional Testing

* Deployment Request creation
* Deployment Task creation
* Task assignment
* Task completion
* Due Date calculation
* Submission
* Approval
* Rejection
* Deployment
* Audit creation
* Email notifications

### Security Testing

Verify that users with different roles and permissions can perform only the actions permitted by the governance rules.

Test at minimum:

* Developer
* QA Engineer
* Release Manager
* Administrator

### Automation Testing

Validate all relevant Salesforce Flows and ensure that:

* Required tasks are created
* Tasks receive the correct assignments
* Due Dates are populated
* Approval Requests are created
* Deployment status changes correctly
* Audit records are created
* Notifications are sent

---

## Git Workflow

Recommended workflow:

```text
Feature Branch
      ↓
Development
      ↓
Testing
      ↓
Pull Request
      ↓
Code Review
      ↓
Merge
      ↓
Release Validation
      ↓
Package Version
```

Before committing changes:

```bash
git status
```

Review changes:

```bash
git diff
```

Commit:

```bash
git add .
git commit -m "Describe the change"
```

Push:

```bash
git push
```

---

## Important Configuration

Before deploying the application to another Salesforce org, verify:

* Custom Permissions
* Permission Sets
* User Roles
* Validation Rules
* Custom Metadata
* Custom Labels
* Email configuration
* Flow activation
* Object permissions
* Field-level security
* Record access

Some configuration may be organization-specific and should be validated during installation and implementation.

---

## Support

For issues or enhancement requests, create an issue in the project repository with:

* Description of the issue
* Salesforce org/environment
* Steps to reproduce
* Expected result
* Actual result
* Relevant Flow/Apex error
* Debug log, if applicable

---

## Product

**Release Governance App**

A Salesforce application for structured deployment and release governance.

**Developer:** Vidushi Infotech

---

## License

This project is distributed as part of the Release Governance App Salesforce application.

Refer to the applicable commercial and Salesforce AppExchange terms for licensing and distribution information.
