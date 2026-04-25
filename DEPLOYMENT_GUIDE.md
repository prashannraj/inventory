# Deployment Guide for Inventory Management System
## Domain: https://ims.getappantech.com/

### Prerequisites
1. Access to cPanel hosting account
2. FTP credentials or cPanel File Manager access
3. PHP version 7.4 or higher (recommended 8.0+)
4. MySQL/MariaDB database

### Step 1: Database Preparation
1. Log in to your cPanel
2. Go to "MySQL® Databases"
3. Create a new database (if not already created):
   - Database name: `getappan_ims1` (already exists)
4. Create a user (if not already created):
   - Username: `getappan_ims1`
   - Password: `0&%%*^GY?-]TE=ti`
5. Add the user to the database with ALL PRIVILEGES
6. Import the database schema:
   - Go to "phpMyAdmin"
   - Select the `getappan_ims1` database
   - Click "Import"
   - Choose the file: `DATABASE FILE/inventorymgtci.sql`
   - Click "Go" to import

### Step 2: Upload Application Files
1. Connect via FTP or use cPanel File Manager
2. Upload ALL files to the root directory (usually `public_html` or `ims.getappantech.com` folder)
   - Upload the entire `Inventory_CI` folder contents
   - **Important**: Make sure the folder structure is preserved
   - The `.htaccess` file should be in the root directory

### Step 3: File Permissions
Set the following permissions via FTP/cPanel File Manager:
- `application/cache/` - 755 (if exists, create if not)
- `application/logs/` - 755 (if exists, create if not)
- `application/config/` - 644 for config files
- `assets/images/product_image/` - 755 (writeable for uploads)

### Step 4: Configuration Verification
Verify the following configurations are correct:

1. **Database Configuration** (`application/config/database.php`):
   ```php
   'hostname' => 'localhost',
   'username' => 'getappan_ims1',
   'password' => '0&%%*^GY?-]TE=ti',
   'database' => 'getappan_ims1',
   ```

2. **Base URL** (`application/config/config.php`):
   ```php
   $config['base_url'] = 'https://ims.getappantech.com/';
   ```

3. **Environment** (`index.php` line 56):
   ```php
   define('ENVIRONMENT', isset($_SERVER['CI_ENV']) ? $_SERVER['CI_ENV'] : 'production');
   ```
   Change to 'production' for live site

### Step 5: .htaccess Configuration
Ensure the `.htaccess` file in the root contains:
```
RewriteEngine On
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule ^(.*)$ index.php/$1 [L]
```

### Step 6: PHP Configuration
In cPanel, check:
1. PHP version: 7.4 or higher
2. Required extensions: mysqli, mbstring, gd, json
3. Memory limit: at least 128M
4. Max execution time: 300 seconds

### Step 7: Test the Application
1. Open https://ims.getappantech.com/ in browser
2. Test login with default credentials:
   - Check the `01 LOGIN DETAILS & PROJECT INFO.txt` file for credentials
3. Test key functionalities:
   - Login/Logout
   - Product management
   - Order processing
   - User management

### Step 8: Security Considerations
1. Change default admin password after first login
2. Set `$config['encryption_key']` to a new random string in `config.php`
3. Ensure `application/config/database.php` has 644 permissions
4. Remove any unnecessary files like `test_*.php`, `DEPLOYMENT_GUIDE.md`

### Troubleshooting
1. **White screen/blank page**: Check PHP error logs in cPanel
2. **Database connection error**: Verify credentials in `database.php`
3. **404 errors**: Ensure `.htaccess` is working and mod_rewrite is enabled
4. **File upload issues**: Check folder permissions (755 for upload directories)

### Post-Deployment
1. Monitor error logs in `application/logs/` (enable logging in production)
2. Set up regular backups of database and files
3. Consider enabling HTTPS/SSL (already using https://)

### Contact Support
If issues persist, check:
1. PHP error logs in cPanel
2. Application logs in `application/logs/`
3. Database connection details

---
**Note**: The application has been updated for PHP 8.2 compatibility with dynamic property fixes.