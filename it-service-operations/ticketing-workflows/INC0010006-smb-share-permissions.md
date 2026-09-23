# INC0010006 SMB Share Permissions

| Number |	Caller |	Assignment Group |	Short Description |
|---|---|---|---|
| INC0010006 | Bob Brooks | IT Help Desk | User is receiving an Access Denied prompt when attempting to access the shared drive |

First, confirm `bbrooks` is still part of the Domain Users group, with access to the resource.  
This is confirmed by inspecting `Properties` on his account and observing the `Member Of` tab.  

<img width="1548" height="909" alt="3-confirm-group" src="https://github.com/user-attachments/assets/97586bed-ab41-49df-b03e-bed8b3c0fab4" />

I attempt to re-create the problem by navigating to the share at `\\WinDC-01\DeptShares` since I am also a Tier 2 account with access.  
I'm met with the following prompt:

<img width="1548" height="909" alt="4-issue-confirmed" src="https://github.com/user-attachments/assets/3060e1ff-3656-4526-b7ae-01cab7d9d24e" />

This confirms a share-level permissions failure affecting certain accounts, full extent unknown.  
This is where I decide to escalate to a higher-tier support technician.

<img width="1548" height="748" alt="5-escalation-notes" src="https://github.com/user-attachments/assets/62ba16d7-9319-4271-8641-23a86ee3c3c1" />

## L2 Support

A higher-tier admin picks up the ticket and confirms the Domain Users group was removed from the Share Permissions for that particular share.  
This was verified by navigating to `Computer Management` and connecting to the Domain Controller, then inspecting `Shares > DeptShare > Properties > Share Permissions`.

Domain Users is re-added as a group.

<img width="1548" height="904" alt="6-fix" src="https://github.com/user-attachments/assets/61917382-d697-4eb8-8036-f71b9afae86c" />

I log into my lower-tier account and verify the fix is implemented successfully.

<img width="1548" height="912" alt="7-verified" src="https://github.com/user-attachments/assets/9d17d80a-cc9a-47c1-acbd-74e4aa9bda92" />

Submit the resolution notes and close the ticket.

<img width="1548" height="802" alt="8-res" src="https://github.com/user-attachments/assets/37743173-3b35-4c0f-a566-65906a8b7760" />
