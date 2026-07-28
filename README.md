# Candidate Screening Automation

## Project Name

Candidate Screening Automation using n8n

---

# Problem Statement

Recruitment teams often spend a significant amount of time manually reviewing candidate applications to determine whether applicants meet the minimum job requirements. This manual process is repetitive, time consuming, and prone to inconsistencies.

The objective of this project is to automate the initial candidate screening process by reading applicant information from a Google Sheet, validating required fields, applying predefined screening rules, categorizing candidates, updating the screening results, and sending automated email notifications based on the screening outcome.

---

# Objective

The objectives of this project are:

* Automate candidate data processing.
* Validate candidate information before evaluation.
* Apply predefined screening criteria.
* Categorize applicants into Selected, Review, or Rejected.
* Update screening results automatically in Google Sheets.
* Send automated email notifications to candidates.
* Reduce manual effort during the recruitment process.

---

# Workflow Architecture

```
Google Sheets Trigger
        │
        ▼
Read Candidate Data
        │
        ▼
Validate Required Fields
        │
        ▼
Apply Screening Rules
        │
        ▼
Categorize Candidate
        │
        ▼
Update Result in Google Sheets
        │
        ▼
Selected?
   ┌─────────────┐
   │             │
 Yes            No
   │             │
   ▼             ▼
Send         Review?
Selected     ┌──────┐
Email        │      │
            Yes    No
             │      │
             ▼      ▼
        Send Review  Send Rejection
            Email        Email
```

---

# Technologies Used

* n8n
* Google Sheets
* Gmail
* JavaScript
* Google Workspace APIs

---

# Nodes Used

| Node | Purpose |
|-------|---------|
| Google Sheets Trigger | Detects newly added or updated candidate records |
| Google Sheets (Read) | Reads candidate information |
| IF Node | Validates required fields |
| Code Node | Applies screening rules |
| Code Node | Categorizes candidates |
| Google Sheets (Update Row) | Updates screening status in the spreadsheet |
| IF Node | Determines whether candidate is Selected |
| IF Node | Determines whether candidate requires Review |
| Gmail | Sends Selected email |
| Gmail | Sends Review email |
| Gmail | Sends Rejection email |

---

# Setup Instructions

## 1. Clone or Import Workflow

Import the provided `workflow.json` file into n8n.

## 2. Create Google Sheet

Create a spreadsheet named:

```
Candidates
```

Add the following columns:

| Name | Email | Degree | Skills | Experience | Availability | Status | Category | Remarks |
|------|------|------|------|------|------|------|------|------|

## 3. Configure Google Sheets Credentials

Authenticate Google Sheets within n8n.

Select:

* Spreadsheet
* Worksheet
* Trigger

## 4. Configure Gmail Credentials

Authenticate Gmail using your Google account.

Grant email sending permissions.

## 5. Execute Workflow

Enable the workflow.

Whenever a candidate is added or updated, the workflow will automatically process the application.

---

# Credentials Required

Only the credential names are listed below.

* Google Sheets Account
* Gmail Account

No passwords, API keys, or secrets are included in this repository.

---

# Workflow Explanation

### Step 1

The Google Sheets Trigger detects when a new candidate record is added or updated.

### Step 2

Candidate information is retrieved from Google Sheets.

### Step 3

The workflow validates that all required fields are present.

Required fields include:

* Name
* Email
* Degree
* Skills
* Experience
* Availability

Candidates with missing information are marked as invalid.

### Step 4

Screening rules are applied.

The scoring system evaluates:

* Relevant Degree
* Technical Skills
* Years of Experience
* Availability

### Step 5

Each candidate receives a screening score.

Example scoring:

| Criteria | Points |
|----------|-------:|
| BSCS / BSAI / BSSE Degree | 30 |
| Python | 20 |
| Machine Learning | 20 |
| Deep Learning | 20 |
| SQL | 10 |
| Experience ≥ 3 Years | 20 |
| Experience 1–2 Years | 10 |
| Immediate Availability | 10 |

### Step 6

Candidates are categorized.

| Score | Category | Status |
|-------:|----------|---------|
| 80 or above | Selected | Approved |
| 50–79 | Review | Pending |
| Below 50 | Rejected | Rejected |

### Step 7

The workflow updates the candidate's row in Google Sheets.

Updated fields include:

* Status
* Category
* Remarks

### Step 8

Based on the category, an appropriate email is automatically sent.

Selected candidates receive a congratulatory email.

Review candidates receive an application update.

Rejected candidates receive a polite rejection email.

---

# Test Cases

| Test Case | Expected Result |
|-----------|-----------------|
| Candidate with all required qualifications | Selected |
| Candidate meeting partial requirements | Review |
| Candidate with insufficient qualifications | Rejected |
| Candidate with missing mandatory fields | Validation Failure |
| Invalid email format | Email delivery failure |
| Duplicate candidate record | Existing row updated |

---

# Error Handling

The workflow includes basic validation and error handling.

* Missing required fields are detected before screening.
* Google Sheets update failures stop workflow execution.
* Email delivery failures are reported in n8n execution logs.
* Invalid candidate records are prevented from proceeding through the workflow.
* Candidate categorization occurs only after successful validation.

---

# Known Limitations

* Screening rules are static and manually defined.
* Duplicate detection is based on the configured matching column.
* Email templates are fixed.
* Resume parsing is not included.
* Skills are matched using simple keyword searches.
* The workflow does not integrate with Applicant Tracking Systems (ATS).

---

# Future Improvements

* Resume parsing using OCR or PDF extraction.
* AI-powered resume ranking using Large Language Models.
* Dynamic scoring based on job descriptions.
* Integration with LinkedIn and job portals.
* Dashboard for recruitment analytics.
* Candidate interview scheduling automation.
* Support for multiple job positions.
* AI-generated candidate feedback.
* Integration with HR management systems.
* Slack or Microsoft Teams notifications for recruiters.

---

# Repository Structure

```
candidate-screening-automation/
│
├── workflow/
│   └── workflow.json
│
├── screenshots/
│
├── sample-data/
│
└── README.md
```

---

# Sample Input

| Name | Email | Degree | Skills | Experience | Availability |
|------|------|------|------|------:|------|
| Ali Khan | ali@gmail.com | BSCS | Python, SQL, Machine Learning | 3 | Immediate |

---

# Sample Output

| Name | Status | Category | Remarks |
|------|------|------|------|
| Ali Khan | Approved | Selected | Excellent Match |

---

# Author

AI Automation Internship Project

Candidate Screening Automation using n8n
