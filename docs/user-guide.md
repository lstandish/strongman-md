# Using Strongman
[Open Strongman Password Manager]

---

### Fast and Easy Instructions

#### To Retrieve a Password
1. Enter the master passphrase
2. Start typing the domain name in the 'Domain' field. If you have used this password before, you will see the domain-username in a dropdown list. Click to choose it. You're done; the password is automatically copied to the clipboard for you (unless you've disabled that in the settings menu.)
3. If you have a lot of password entries, you can filter them by category.

#### To Create a New Password Entry
1. Just enter the domain and username. Change the password computation options for this username if necessary (use the '☰' icon). **Select the appropriate category from the dropdown list.**
2. Click the "Compute" button. The password is calculated and (optionally) copied to clipboard. The next time you need this password, you can select it from the dropdown list.  This is a *computed* password. If you need to change it later, you can increment the password number in the '☰' options menu.
3. If you want to want to *use your own password* instead of a computed one, just edit edit the password field and click the "Save" button. This *"custom"* password will be AES256-encrypted and stored on the server.

### Secure Notes
Any password entry, either "computed" or "custom", can have AES-256- encrypted secure notes.  Click the book icon just above the password entry field. A text area for the notes will pop into view. When done, click the "Save" link to encrypt and save your notes to the server.

### Password Categories
New in version 1.10 and up: You can now organize your password into categories.  **The default categories are:**

- Uncategorized
- Banking
- E-commerce
- Services
- Social Media
- Admin Panel
- Forums
- Government

Plus there are 2 additional unnamed categories available.  **You can change the names of any of these categories as you wish.** Look in "Settings and Tools" at the bottom of the Strongman window.

### Password Import / Export
1. **Import from CSV file**  
Passwords can be imported from virtually any CSV file. The header row is a requirement. The following fields are imported from each row:
    - Website (required)
    - Login Name (required)
    - Password (required)
    - Comments (optional)
If your CVS header names are different from these, you can map them to different names.  If your CSV file has more fields than these, they will be ignored. 

2. **Import from another Strongman account**  
To import passwords from another Strongman account into the currently open account, you need to be able to provide the imported account's master password. The category names of the destination account will be applied to the imported entries.  Matching domain-username entries will be overwritten. This feature is often used to *change the master password* (see below).

3. **Export to CSV file**  
Passwords can be exported to a CSV file. Keepass v1.x format is used.

!!! Note
    **To Change the Master Password**
    
    1. Enter the new master password and click 'submit'..
    2. Since customized category names are not imported, if you modified the default category names in the old (origin) account, it is recommended that before importing you change the categories in the new account to be the same.
    3. Use "Import Passwords from Another Strongman Account" (under "Settings and Tools/Account Actions" near the bottom of the Strongman app), specifying the master password of the old account.
    4. After the passwords and notes are imported, you can delete the old Strongman account via the 'Delete Strongman Account' option.

### Short Demo Video

To be published soon!
[Open Strongman Password Manager]: /app/index.php


<!--stackedit_data:
eyJoaXN0b3J5IjpbMTQ0NTI5NTI3LDk5MTA0MDc5NV19
-->