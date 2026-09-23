# INC0010007 NTFS Permissions

| Number |	Caller |	Assignment Group |	Short Description |
|---|---|---|---|
| INC0010007 | Carol Carter | IT Help Desk | User reports issues with making modifications to files despite having access to them |

First, verify `ccarter` belongs to the proper groups for DeptShare modifications.

<img width="1548" height="912" alt="10-groups-check" src="https://github.com/user-attachments/assets/91184b93-b197-4019-9c73-103a0c41e1dc" />

After confirming, I navigate to `\\WinDC-01\` in File Explorer, right-click the `DeptShare` folder and inspect `Properties`.  
I note that `IT-Security` group is not present.

<img width="1548" height="912" alt="11-groups-check" src="https://github.com/user-attachments/assets/fc9515a7-13a1-408b-9ea9-864228ef8365" />

I navigate to `Advanced`, then `Effective Access`. I enter `ccarter`'s account and review.  
Upon selecting `View effective access`, a banner is displayed in the window indicating I have insufficient permissions to evaluate effective rights access.

<img width="1548" height="910" alt="13-t2-limitation" src="https://github.com/user-attachments/assets/654df6e9-1161-487c-958a-a4a62443aea0" />

I document the steps I took and submit the relevant work notes, escalating the ticket to a higher-tier support technician.

<img width="1341" height="458" alt="14-work-notes" src="https://github.com/user-attachments/assets/0ea3cc74-edca-4d42-98d5-1f0682c8c345" />

## L2 Support

Inspecting the Effective Access information for the IT-Security group, I can see there is no access available to the group.

<img width="1548" height="910" alt="15-share-access-it-sec" src="https://github.com/user-attachments/assets/fb012b96-95d6-4574-be44-498806f64240" />

Navigating to `\\WinDC-01\C$\Shares\DeptShare` in File Explorer through the address bar, I right-click `DeptShare > Properties > Security > Edit > Add` and enter IT-Security, clicking `Check Names` to ensure the group 
information is populated. Selecting OK, then checking `Modify` and `Apply` then `OK` again, I'm able to verify that the fix is implemented after viewing Effective Access once again.

<img width="1548" height="907" alt="16-fix" src="https://github.com/user-attachments/assets/f687b381-ea78-4a60-90c4-30d7e300d9fd" />

IT-Security group now present and correctly configured.

<img width="1548" height="910" alt="17-fix" src="https://github.com/user-attachments/assets/b39f4b0d-517e-4afb-8438-e1cf4748a348" />

