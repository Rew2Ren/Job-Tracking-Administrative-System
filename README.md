# Job Tracking Administrative System

> **Case study.** The source code belongs to the client and is not public. This page describes the system, my role and our approach.

A web system built in CakePHP 5 for a real client: the engineering and architecture branch of a larger Australian company that designs and builds houses across Victoria. It replaced the spreadsheets the business used to run its inquiries, quotes and jobs. Built as a Monash University team project (Team 126).

## Why the administrative system matters

Before this system, every inquiry, supplier quote and job lived in separate Excel files. The Admin Portal turned that into one place to run the business:

- **One source of truth.** Inquiries, quotes, jobs, invoices and client communication sit together, instead of being spread across spreadsheets and inboxes.
- **The business process is built in.** The system follows the real workflow, from inquiry to quote, acceptance, job, invoice and completion, so steps can't be skipped or lost.
- **Client data is protected.** Role-based access control means staff, clients and suppliers each see only what they're allowed to, enforced on the server.
- **Mistakes are recoverable.** Records are soft-deleted by default. Permanent deletion needs two-factor authentication and manager approval.
- **Managers get visibility.** Search, filtering and Excel and PDF export make reporting quick, instead of manually combining spreadsheets.

## How it works

The system follows the client's full business flow: a customer inquiry, information gathering, collecting quotes from several suppliers, combining them into one customer quote, the customer accepting or rejecting it, then job creation, invoicing, supplier and architect assignment, and the final invoice.

| Portal | Who uses it | What they can do |
|--------|-------------|------------------|
| **Admin (CRM)** | Staff and managers | Manage inquiries, quotes, jobs and users; reporting; deletion approvals |
| **Client** | Customers | View their own quotes and job progress; accept or reject quotes |
| **Supplier/Architect** | Contractors | View and update the jobs assigned to them |

Supporting features:
- A **support chatbot** for common questions
- **Centralised communication:** Microsoft Power Automate flows that file client emails and attachments into the right OneDrive job folders, with user documentation for staff

## My role

- Major coding development across the system
- Penetration testing of the system as part of the team

## How we tested it

- Wrote user stories with Given/When/Then acceptance criteria, each with functional test cases covering the happy path, edge cases and invalid input
- Added security checks to each story, focused on the risks most relevant to a multi-portal system:
  - **Access between portals:** confirming that one client or supplier can't view another's jobs or quotes by changing an ID in the URL
  - **Server-side enforcement:** checking that 2FA and approval steps can't be skipped by calling the underlying request directly
  - **Input handling:** cross-site scripting, cross-site request forgery, and formula injection in exported spreadsheets
- Ran automated tests and static analysis (PHPStan) as part of development

[Add one or two sentences on what you personally tested and the kind of issue you found, for example "found and fixed an access-control gap in the supplier portal". Keep it general: don't publish specific weaknesses in the client's live system.]

## What I learned

- **Real requirements change once you see the process.** The client's flow diagrams revealed steps the first requirements list missed, such as combining supplier quotes and payment-gated job progression, so we added user stories to cover them.
- **Security has to be checked on the server.** Hiding a button in the interface doesn't stop a determined user, so every permission needed a test that went around the interface.

## Tools and practices

PHP (CakePHP 5), GitLab, Agile delivery with a real client, Microsoft Power Automate, PHPStan, and AI coding tools including, GitHub Copilot and Gemini.