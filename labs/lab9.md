

# Lab 9: WordPress Vulnerable Setup (Older Version)

#### Prerequisites:
- **LAMP Stack** installed and configured (Refer to Lab 1).
- **Basic knowledge of WordPress** and web application security.
- **An isolated testing environment** (e.g., Virtual Machine or Docker container).
- **Older, vulnerable version of WordPress** (e.g., **4.7.x**).

---

## Step-by-Step Setup for a Vulnerable WordPress Installation

### Step 1: Download the Vulnerable WordPress Version

1. **Navigate to the web server directory**:
   ```bash
   cd /var/www/html
   ```

2. **Download a vulnerable version of WordPress**:
   - For the purpose of this lab, we will download **WordPress 4.7.5**, which has a known **Rest API vulnerability** and others.
   - You can find older versions on the official WordPress release archives: [WordPress Release Archive](https://wordpress.org/download/releases/).

   ```bash
   sudo wget https://wordpress.org/wordpress-4.7.5.tar.gz
   ```

3. **Extract the downloaded archive**:
   ```bash
   sudo tar -xvzf wordpress-4.7.5.tar.gz
   ```

4. **Rename the extracted directory** (for clarity):
   ```bash
   sudo mv wordpress wp-vulnerable
   ```

5. **Set proper permissions**:
   ```bash
   sudo chown -R www-data:www-data /var/www/html/wp-vulnerable
   sudo chmod -R 755 /var/www/html/wp-vulnerable
   ```

---

### Step 2: Create and Configure MySQL Database

1. **Log into MySQL**:
   ```bash
   sudo mysql -u root -p
   ```

2. **Create a new database for WordPress**:
   ```sql
   CREATE DATABASE wordpress_vulnerable;
   ```

3. **Create a user for WordPress**:
   ```sql
   CREATE USER 'wp_user'@'localhost' IDENTIFIED BY 'wp_password';
   GRANT ALL PRIVILEGES ON wordpress_vulnerable.* TO 'wp_user'@'localhost';
   FLUSH PRIVILEGES;
   ```

4. **Exit MySQL**:
   ```sql
   EXIT;
   ```

---

### Step 3: Configure WordPress

1. **Navigate to the WordPress directory**:
   ```bash
   cd /var/www/html/wp-vulnerable
   ```

2. **Rename the configuration sample file**:
   ```bash
   sudo mv wp-config-sample.php wp-config.php
   ```

3. **Edit the wp-config.php file** to configure the database connection:
   ```bash
   sudo nano wp-config.php
   ```

4. **Update the database details** in `wp-config.php`:
   ```php
   define( 'DB_NAME', 'wordpress_vulnerable' );
   define( 'DB_USER', 'wp_user' );
   define( 'DB_PASSWORD', 'wp_password' );
   define( 'DB_HOST', 'localhost' );
   ```

5. **Save and exit** the file editor (CTRL+X, Y, Enter).

---

### Step 4: Install WordPress

1. Open your browser and go to:
   ```
   http://localhost/wp-vulnerable
   ```

2. Follow the **WordPress installation wizard**:
   - Set up your **site name**, **admin username**, **password**, and **email**.
   - Complete the installation and log into the WordPress admin dashboard.

---

### Step 5: Install Vulnerable Plugins and Themes

To simulate real-world vulnerabilities, we’ll install **known vulnerable plugins** that work with WordPress 4.7.x.

1. **Install Vulnerable Plugins**:
   - **RevSlider** (vulnerable to remote code execution).
   - **WP-File-Manager** (vulnerable to unauthorized file access).
   - **WordPress Mobile Pack** (vulnerable to XSS attacks).
   
   **Installation Method**:
   - Download the vulnerable plugins from a trusted GitHub repository or known source.
   - Upload them to `/wp-content/plugins/`.
   - Activate the plugins via the WordPress Admin Panel under **Plugins > Installed Plugins**.

2. **Install Vulnerable Themes**:
   - You can use older versions of WordPress themes known to have vulnerabilities. For example, themes like **Twenty Seventeen** can be vulnerable in older versions.
   - Download vulnerable themes from GitHub or repositories, then upload them to `/wp-content/themes/`.
   - Activate the theme via the WordPress Admin Panel under **Appearance > Themes**.

---

### Step 6: Explore Common Vulnerabilities in WordPress

The following are known vulnerabilities found in older versions like 4.7.x:

1. **SQL Injection**:
   - Check input fields like **search**, **login**, or **comment** sections for SQL injection vulnerabilities.
   - Use **SQLMap** or manual testing for exploiting SQLi.
   - Example payload: `' OR 1=1 --`.

2. **Cross-Site Scripting (XSS)**:
   - Test comment forms, post titles, and other input areas for reflected XSS.
   - Example payload: `<script>alert('XSS')</script>`.

3. **Remote Code Execution (RCE)**:
   - **RevSlider** plugin in WordPress 4.7.x has a **Remote Code Execution (RCE)** vulnerability.
   - Try uploading a **PHP shell** or a malicious file through this plugin to gain code execution on the server.

4. **Local File Inclusion (LFI)**:
   - Test if plugins or themes are vulnerable to LFI, which can include files like `/etc/passwd`.
   - Example payload: `file.php?include=../../../../etc/passwd`.

5. **Cross-Site Request Forgery (CSRF)**:
   - Exploit CSRF vulnerabilities by creating malicious links that can change user settings or post content without the user's consent.
   
6. **Sensitive Data Exposure**:
   - Check if sensitive information like passwords or API keys is exposed in plaintext.
   - Use tools like **Burp Suite** or **Wireshark** to monitor unencrypted traffic.

---

### Step 7: Exploit Vulnerabilities

Here are some ways to exploit vulnerabilities in this setup:

1. **SQL Injection**:
   - Use **SQLMap** or manual payloads to test SQL injection.
   - Example payload: `' OR 1=1 --`.

2. **XSS**:
   - Inject **JavaScript** in comment forms, post titles, or any input field.
   - Example payload: `<script>alert('XSS')</script>`.

3. **RCE (Remote Code Execution)**:
   - Upload a malicious **PHP file** through plugins like **RevSlider**.
   - Execute the PHP file using a browser: `evil.php?cmd=ls`.

4. **LFI (Local File Inclusion)**:
   - Use **LFI** to read sensitive system files.
   - Example payload: `file.php?include=../../../../etc/passwd`.

5. **Brute Force**:
   - Use **Hydra** or **Burp Suite** to attempt **brute-forcing** the admin login.
   - WordPress default usernames (`admin`) are common targets.

---

### Step 8: Secure the WordPress Installation

After exploiting the vulnerabilities, secure the WordPress installation by:

1. **Updating WordPress and Plugins**:
   - Ensure WordPress is updated to the latest version.
   - Regularly update plugins and themes.

2. **Enable Two-Factor Authentication (2FA)**:
   - Install the **Two-Factor Authentication** plugin to secure admin login.

3. **Use Strong Passwords**:
   - Ensure users use **strong, complex passwords** for all accounts.

4. **Limit Login Attempts**:
   - Use a plugin like **Limit Login Attempts** to prevent brute force attacks.

5. **Use a Web Application Firewall (WAF)**:
   - Install plugins like **Wordfence** or **iThemes Security** to add a firewall and other security measures.

6. **Remove Unnecessary Plugins/Themes**:
   - Delete any unused plugins and themes to reduce the attack surface.

7. **Use HTTPS**:
   - Set up an SSL certificate to encrypt the communication between the client and the server.

---

### Conclusion

By completing this lab, you have set up a **vulnerable WordPress site** using an older version (WordPress 4.7.x) and explored common vulnerabilities like **SQL injection**, **XSS**, and **remote code execution**. You also learned how to exploit these vulnerabilities, followed by securing the WordPress site by applying best practices. This process helps in understanding the importance of securing WordPress installations in real-world scenarios.