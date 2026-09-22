# INC0010005 Deleted User Restoration

| Number | Caller | Assignment Group | Short Description |
|---|---|---|---|
| INC0010005 | Alice Anderson | IT Help Desk | User account deleted, unable to log in |

## Workflow

Open ADUC and attempt to locate the user's account through `Find` in `Entire Directory`:

<img width="1548" height="910" alt="5-account-missing" src="https://github.com/user-attachments/assets/dd185fda-65b4-4861-9982-b9d7fb44e57c" />

Unable to locate the account, pivot to ADAC and check the `Deleted Objects` container.  
Here, I am met with a permissions gate. This is grounds for escalating to higher tier support.

<img width="1548" height="909" alt="6-adac-confirmation-boundary" src="https://github.com/user-attachments/assets/ce1d2419-cbc4-4a4c-abab-9fd6e0dc8d62" />

I communicate this through my work notes, describing the measures I had already taken for the next technician to work from.

<img width="1548" height="806" alt="7-working-notes" src="https://github.com/user-attachments/assets/05fa83cf-88a7-44c9-84f0-42e0a344d714" />

An administrator with proper permissions and access to the ADAC AD Recycle Bin is able to restore the account, verified via ADUC.

<img width="1548" height="910" alt="9-restored" src="https://github.com/user-attachments/assets/be32c0da-9183-4d66-90b7-ccc368f78e83" />

<img width="1548" height="911" alt="10-find-account" src="https://github.com/user-attachments/assets/125f9595-625e-496b-9df2-3238b9aa9a40" />

Ticket is closed with informative resolution notes in case user opens a future ticket related to the incident.

<img width="1548" height="795" alt="11-ticket" src="https://github.com/user-attachments/assets/e3269643-a4f6-4d7c-8d6c-72aaa477f9b8" />
