# Migrating from 1Password to Apple Passwords in Minutes

Are you looking to switch from 1Password to Apple's built-in password manager? This guide will walk you through the process of migrating your passwords quickly and easily.

## Steps to Migrate

1. **Export from 1Password**
   - Open 1Password on your Mac
   - Go to File > Export > All Items
   - Choose CSV as the export format
   - Save the file to a secure location on your Mac

2. **Reshape CSV Content**
   - Open Terminal on your Mac
   - Navigate to the directory where you saved the exported CSV file
   - Run the following command to reshape the CSV content:

     ```bash
     python -c "import csv, sys; r = csv.DictReader(sys.stdin); w = csv.writer(sys.stdout); w.writerow(['Title', 'URL', 'Username', 'Password', 'Notes', 'OTPAuth']); [w.writerow([row.get('Title', ''), row.get('URL', ''), row.get('Username', ''), row.get('Password', ''), row.get('Notes', ''), row.get('OTPAuth', '')]) for row in r]" < ./1PasswordExport-xxxxxxxx-20240827-181514.csv > apple_passwords_import.csv
     ```

   Note: Replace `./1PasswordExport-xxxxxxxx-20240827-181514.csv` with the actual name of your 1Password export file.

   This command creates a new CSV file named `apple_passwords_import.csv` with the columns arranged according to Apple Passwords schema: Title, URL, Username, Password, Notes, and OTPAuth.

3. **Import into Apple Passwords**
   - Open the Passwords app on your Mac
   - Click on "File" in the menu bar
   - Select "Import Passwords..." from the dropdown menu
   - Choose the `apple_passwords_import.csv` file you created in step 2
   - Click "Import" to begin the process
   - Review and confirm the imported passwords

4. **Verify the Import**
   - After the import is complete, check your Apple Passwords to ensure all items were imported correctly
   - Pay special attention to entries with two-factor authentication (2FA) or one-time password (OTP) information

5. **Clean Up**
   - Once you've verified that all your passwords have been successfully imported, securely delete the CSV files you created during this process
   - Use a secure deletion tool or overwrite the files multiple times before deleting them
