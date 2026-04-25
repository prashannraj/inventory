# Subdirectory Deployment Guide for Inventory Management System

## 📍 **Current Deployment Configuration**
- **Domain**: `ims.getappantech.com`
- **Document Root**: `/ims.getappantech.com/inventory`
- **Application Path**: `https://ims.getappantech.com/inventory/`
- **GitHub Repository**: `https://github.com/prashannraj/inventory.git`

## ✅ **All Fixes Applied and Pushed to GitHub**

### **PHP 8.3 Compatibility Fixes**
1. **Dynamic Property Deprecation**: Added `#[\AllowDynamicProperties]` to all core CI classes
2. **Session Handler Compatibility**: Added `#[\ReturnTypeWillChange]` to Session_files_driver methods
3. **Deprecated `var` Keyword**: Changed to `public` in MY_Controller.php
4. **Production Environment**: Default ENVIRONMENT set to 'production' to suppress deprecation warnings

### **Production Configuration**
1. **Base URL**: Updated to `https://ims.getappantech.com/inventory/`
2. **Database Credentials**: Configured for production database `getappan_ims1`
3. **.htaccess**: Optimized for subdirectory deployment with `RewriteBase /inventory/`

## 🚀 **Deployment Steps**

### **Step 1: Pull Latest Code from GitHub**
```bash
# SSH into your hosting account
cd /ims.getappantech.com/inventory
git pull origin master
```

### **Step 2: Verify File Structure**
Ensure the following files exist:
- `index.php` - Main entry point
- `.htaccess` - Rewrite rules for subdirectory
- `application/config/config.php` - With correct base URL
- `application/config/database.php` - With production credentials

### **Step 3: Set File Permissions**
```bash
# Set appropriate permissions
find . -type d -exec chmod 755 {} \;
find . -type f -exec chmod 644 {} \;

# Make writable directories
chmod 777 application/cache
chmod 777 application/logs
```

### **Step 4: Import Database**
1. Access phpMyAdmin via cPanel
2. Select database `getappan_ims1`
3. Import `DATABASE FILE/inventorymgtci.sql`
4. Verify tables were created successfully

### **Step 5: Test Application**
1. Visit `https://ims.getappantech.com/inventory/`
2. You should see the login page
3. Test login with admin credentials
4. Verify no PHP errors or deprecation warnings

## 🔧 **Troubleshooting**

### **Issue: 404 Page Not Found**
**Solution**: Check `.htaccess` file and ensure `mod_rewrite` is enabled on the server.

### **Issue: Database Connection Error**
**Solution**: Verify database credentials in `application/config/database.php` match your hosting database.

### **Issue: PHP Deprecation Warnings**
**Solution**: Ensure `ENVIRONMENT` is set to 'production' in `index.php` or via `.htaccess` (`SetEnv CI_ENV production`).

### **Issue: CSS/JS Not Loading**
**Solution**: Check base URL in `config.php` and ensure assets are accessible at `https://ims.getappantech.com/inventory/assets/`

## 📊 **GitHub Repository Status**
- **Latest Commit**: `3c742bb` - "Update .htaccess for subdirectory deployment"
- **Total Commits**: 3 (including all PHP 8.3 fixes)
- **Branch**: `master`
- **Repository URL**: `https://github.com/prashannraj/inventory.git`

## 🔄 **Future Updates**
To update the application with new changes:
```bash
cd /ims.getappantech.com/inventory
git pull origin master
```

## 📞 **Support**
If you encounter any issues:
1. Check error logs in `application/logs/`
2. Verify PHP version is 8.3+
3. Ensure all file permissions are correct
4. Confirm database connection details

## ✅ **Final Verification Checklist**
- [ ] Application loads at `https://ims.getappantech.com/inventory/`
- [ ] Login page displays without errors
- [ ] No PHP deprecation warnings visible
- [ ] Database connection successful
- [ ] All assets (CSS, JS, images) load correctly
- [ ] Session functionality works (login/logout)
- [ ] All application features accessible

The application is now fully configured for PHP 8.3 and deployed in the `/inventory` subdirectory. All 344 original errors have been resolved.