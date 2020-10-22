https://githubsfdeploy.herokuapp.com/app/githubdeploy/bbellanc/partner-billing


# Introduction
This app implements basic billing functionality for freelancers and small consultancies.
The app is created and developed based on my personal needs as an independent salesforce consulting and implementation partner.
I currently do not have decided upon a license, so please do not fork / clone!

# Overview
In a galaxy far, far away, this app will provide full Billing / Account Management capabilities. For now, you can:
* Create Budgets for your Accounts to keep track of hours logged and hours invoiced (against said budget)
* Log time entries to track your work (store additional information like the resource and the product)
* Perform a bill run to convert time entries to invoices
* Generate PDFs for your invoice records and send them to billing contacts (using e-mail).

I use JIRA to organize releases and epics, however the release logs in GitHub are accurate.

## Mass Edit Line Items
* Conventiently mass-edit line items in tableview
* Highlight edited cells (fields) and new rows
* Reset changes (for complete table or single row)
* Add new rows and delete complete rows with single button-clicks
* Commit all changes with a single button-click

<img src="screenshots/edit-line-items.gif" alt="Edit line items animation"/>

## Create PDFs from Invoice Records
Many utility features to handle PDF generation from the record.

### Preview the generated PDF
* Multi-language support (maintain existing and add new translations with translation workbench)
* Toggle rendering of the Invoice's timesheet
* Select your company profile, that is used to fill header and footer
* Review all changes in real-time

<img src="screenshots/show-pdf-preview.gif" alt="PDF Preview"/>
<img src="screenshots/draft-invoice-preview.gif" alt="Preview for Draft"/>

### Store generated PDFs as Attachments and Documents
* Store all generated PDFs as full "Content Documents"
* Creates new content versions for subsequently generated PDFs with same settings, new Documents for different settings
* Watermark is added for PDFs that are generated while Invoice is still a draft (currently not localized)

<img src="screenshots/draft-and-activated-invoice-pdf.gif" alt="Draft and activated PDF"/>

### Handle automatic sync or delete of PDF
* Track changes on all relevant fields (amount, billing address, date, etc)
* Decide, if changes will create a new version of PDF or delete the whole document alltogether
* Store the configurable options that will be used when creating a new PDF file

<img src="screenshots/select-pdf-sync-options.gif" alt="Sync/Delete PDFs"/>

## Perform invoicing runs
* Automatically generate invoices for selected time entries in a filtered service period
* Review and edit generated draft invoices and activate them
* Generate PDFs for all activated invoices and preview them
* Send PDFs with selected E-Mail template to configured billing contacts

<img src="screenshots/full-invoicing-run.gif" alt="Full Invoicing Run"/>


# Contribute
Please contact me if you want to fork the repo or contribute. Lincense is tbd.

## Branching Model
Branching model is based on GitFlow, but slightly adjusted to better work with SFDX (Package deploys & CI). The main stable branch is `master` and I use multiple feature and version branches (`feature/PB-xx-story-name` and `version/major.minor.patch`) where development is done. To reduce overhead, work can be done in both feature and version branches (as long as the version is developed by a single person). Feature branches always merge to version branches. Version branches merge to master. CI triggers on version branches will create new package versions and install them on Staging / UAT Sandboxes and perform a full regression run of all apex & jest tests.

## Development Workflow
Setup Scratch org using the scripts. This will speed up test data import, permission sets, etc.

Windows:
```shell
.\dev-tools\win\default_init.ps1 -a "ScratchAlias"
```

MacOs:
```shell
bash dev-tools/macOS/default_init.sh
```
