# Overview

Use this Pipeline pattern to fully automate employee data management, sourcing from multiple HR applications and writing to the Box application. This pattern finds active users in Workday that were updated within the last two hours and copies employee files into their corresponding sub-folders, using the file structure created from the Box Folder Management Pipeline.

In this pattern, the parent directory for employee files is divided into _Active_ and _Terminated_ folders. Each of these folders comprise of subfolders from A-Z (representing the first letter an employee’s last name) that store the employee file folders found with the _EmployeeID\_LastName\_FirstName_ naming convention. Additional subfolders are created within each employee folder, each representing a functional category of documents that HR may want to capture, such as performance, expenses, and training.

**Pipeline #1 Get Employee Files**

****![](<../.gitbook/assets/image (8).png>)****



This Pipeline finds active users updated in Workday within the last 2 hours to determine what information from Workday’s _Get\_Workers_ object can be included. Subsequently, the following actions are triggered in the given sequence.

1. Initiate the Box Folder Management Pipeline.
2. Get the user’s active status, employee name, and ID from Workday.
3. Get the user’s Jobvite candidate information.
4. Get the user’s 7Geese information and write it to the user’s Performance subfolder.
5. Get the user’s Skilljar information and write it to the user’s Training subfolder.
6. Get the user’s DocuSign information.
7. Get the user’s Expensify information and write it to the user’s Expenses subfolder.

**Pipeline #2 Box Folder Management**

****![](<../.gitbook/assets/image (4).png>)****

This Pipeline creates a folder structure within Box to store relevant data for a new hire. In the case where an employee leaves the company, their folders are moved to the Terminated folder. If an ex-employee is re-hired, their Terminated folders are archived.

**Pipeline #3 Check and Create Folder**

****![](<../.gitbook/assets/image (7).png>)****

This Pipeline checks if the requested folder already exists, and if not, creates a new folder.

**Pipeline #4 Push File to Box**

****![](<../.gitbook/assets/image (1).png>)****

This Pipeline reads a file from the SnapLogic Platform and writes it to a user’s Box folder.
