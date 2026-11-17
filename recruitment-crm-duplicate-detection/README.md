
# Recruitment CRM Data Quality Automation

**Focus:** Automating candidate database quality checks

**Project type:** Personal project for my HR Automation Portfolio

**Goal:** Build an automated process to detect and classify potential duplicate records in a recruitment CRM.

**Tools:** Google Sheets, n8n

**Data:** For testing, I used a synthetic dataset of 20,605 candidate records, created with Codex and [Faker.js](https://fakerjs.dev/) based on the structure of my own GameDev recruitment database. No real candidates' personal data is published.

## Project Objectives

- Automatically detect potential duplicate candidate records using full names, LinkedIn profiles, email addresses, and phone numbers.
- Generate a report with the results of the checks.
- Reduce the time spent manually auditing the recruitment database.

## Implementation Steps

1. **Prepared the test data.** Used Codex and Faker.js to transform my original CSV file containing real candidate information into a CSV file with synthetic test data.

2. **Designed the duplicate detection logic.** Implemented a JavaScript algorithm in n8n that:
   - Normalizes candidate data: email addresses, phone numbers, LinkedIn URLs, and full names.
   - Uses synthetic LinkedIn URLs with the `linkedin.example` domain in the demo dataset.
   - Groups records by matching LinkedIn profiles, emails, phone numbers, and full names to avoid comparing every candidate against the entire database.
   - Analyzes potential duplicate pairs based on matching and conflicting information.
   - Automatically assigns one of three statuses: `Confirmed duplicate`, `Manual review`, or `Not duplicate`.
   - Creates a unique `Pair_ID` for each pair, allowing results to be updated without creating duplicate entries when the workflow runs again.

3. **Built the workflow in n8n.** Connected and configured the required nodes.

4. **Tested the workflow on real data** to check that it worked correctly.

5. **Ran the workflow on synthetic data** to demonstrate the automation process.

## Results

The workflow processed **20,605 candidate records** and identified **2,272 potential duplicate pairs**.

The results were saved to the `Audit_Results` sheet, with an automatic classification for each pair.

### Audit_Results Report Structure

| Field | Description |
|---|---|
| `Record_1`, `Record_2` | Record numbers of the two candidates with a potential match |
| `Name_1`, `Name_2` | Candidate names for easy identification |
| `Matching_Signals` | Matching signals: LinkedIn, Email, Phone, Exact name, Workplace, Position |
| `Name_Comparison` | Name comparison result: exact, similar, different, or missing |
| `Auto_Decision` | Automatic classification: Confirmed duplicate, Manual review, or Not duplicate |
| `Decision_Reason` | Explanation of why the algorithm made its decision |
| `Needs_Review` | Yes/No flag indicating whether manual review is required |
| `Pair_ID` | Unique pair identifier used to update results without creating duplicates |

The report helps recruiters separate automatically confirmed duplicates from unclear cases that require manual review. It also shows the reason behind each decision.
## Video Demo

[Watch the Recruitment CRM Automation Demo](https://github.com/rina-alami/Portfolio-Projects/releases/download/v1.0/recruitment-crm-duplicate-detection-demo.mov)
