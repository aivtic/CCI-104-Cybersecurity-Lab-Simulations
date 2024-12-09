# Lab 8: WackoPicko Guide (Vulnerable Web Application)

**WackoPicko** is a deliberately vulnerable web application that is designed for web security training, penetration testing, and vulnerability exploitation. It is a PHP-based application and simulates common web application vulnerabilities, making it an excellent tool for learning how to secure real-world applications. Similar to other vulnerable applications like **NodeGoat** and **Juice Shop**, WackoPicko helps users practice exploiting vulnerabilities in a controlled environment.

---

## Lab Objectives

1. Install and configure **WackoPicko**.
2. Explore the vulnerabilities present in **WackoPicko**.
3. Practice penetration testing techniques and exploit vulnerabilities.
4. Learn how to secure a vulnerable web application by remediating the vulnerabilities.

---

## Prerequisites

Before proceeding with the setup and exploration, ensure the following prerequisites are met:

1. **LAMP Stack** is installed and configured (refer to **Lab 1**).
2. **PHP** and **MySQL** are installed.
3. **Basic knowledge of web application security** and **penetration testing** tools.
4. **A secure, isolated environment** (e.g., a virtual machine or Docker container) is recommended for testing the vulnerabilities safely.

---

## Step-by-Step Setup

### Step 1: Download WackoPicko

1. Change to the **web server root directory** (e.g., `/var/www/html`):
   ```bash
   cd /var/www/html
   ```

2. **Download WackoPicko** from GitHub:
   ```bash
   sudo git clone https://github.com/xdavidhu/wackoPicko.git
   ```

3. Change to the **WackoPicko directory**:
   ```bash
   cd wackoPicko
   ```

4. Set the **appropriate permissions** for the directory:
   ```bash
   sudo chown -R www-data:www-data /var/www/html/wackoPicko
   sudo chmod -R 755 /var/www/html/wackoPicko
   ```

---

### Step 2: Configure MySQL Database

1. **Log into MySQL**:
   ```bash
   sudo mysql -u root -p
   ```

2. **Create a new database** for WackoPicko:
   ```sql
   CREATE DATABASE wackopicko;
   ```

3. **Create a user** with privileges to the database:
   ```sql
   CREATE USER 'wacko_user'@'localhost' IDENTIFIED BY 'password';
   GRANT ALL PRIVILEGES ON wackopicko.* TO 'wacko_user'@'localhost';
   FLUSH PRIVILEGES;
   ```

4. **Exit MySQL**:
   ```sql
   EXIT;
   ```

---

### Step 3: Configure WackoPicko

1. Navigate to the **config directory** inside the WackoPicko directory:
   ```bash
   cd /var/www/html/wackoPicko/config
   ```

2. **Edit the configuration file** (`config.php` or similar):
   ```bash
   sudo nano config.php
   ```

3. Update the database connection details to match the database you just created:

   ```php
   $db = array(
       'host' => 'localhost',
       'user' => 'wacko_user',
       'password' => 'password',
       'dbname' => 'wackopicko'
   );
   ```

4. **Save and exit** the editor.

---

### Step 4: Install Dependencies (if required)

WackoPicko may require additional PHP modules. Ensure the following are installed:

1. Install the necessary PHP modules:
   ```bash
   sudo apt install php-mysqli php-xml php-gd php-mbstring -y
   ```

2. Restart the Apache server to apply the changes:
   ```bash
   sudo systemctl restart apache2
   ```

---

### Step 5: Access WackoPicko Application

1. Open your browser and visit the following URL to access **WackoPicko**:
   ```
   http://localhost/wackoPicko
   ```

2. You should see the **WackoPicko homepage**. The default credentials are typically:

   - **Username**: `admin`
   - **Password**: `admin`

---

### Step 6: Explore the Vulnerabilities in WackoPicko

WackoPicko contains a variety of common vulnerabilities for exploitation. Here are some of the key vulnerabilities to explore:

1. **SQL Injection (SQLi)**:
   - Test input fields such as search boxes, login forms, or any other user-supplied data fields with SQL injection payloads like `' OR 1=1 --`.
   - Look for areas where input isn't properly sanitized, allowing you to manipulate database queries.

2. **Cross-Site Scripting (XSS)**:
   - Inject **JavaScript** into user input fields (e.g., user registration, comments, or search fields) to check if the application reflects it back to the user without proper sanitization.
   - Try input such as:
     ```html
     <script>alert('XSS');</script>
     ```

3. **File Upload Vulnerabilities**:
   - Check if the application allows the upload of arbitrary files such as PHP scripts or shell scripts that could lead to remote code execution.
   - Test with various file types like `.php`, `.html`, or `.txt`.

4. **Cross-Site Request Forgery (CSRF)**:
   - Test if sensitive actions (like changing the password or deleting an account) can be triggered without proper authentication via a **malicious link**.
   - Check if CSRF tokens are present in the forms and if requests can be made without them.

5. **Session Management Flaws**:
   - Test if **session fixation** is possible (forcing a user’s session ID) or if **session expiration** doesn’t occur after logging out.
   - Try to steal or hijack a session by manipulating the session cookie or parameters.

6. **Insecure Direct Object References (IDOR)**:
   - Try modifying URL parameters (e.g., user IDs, post IDs) to access resources or actions you shouldn't be able to, such as viewing other users' data.

7. **Sensitive Data Exposure**:
   - Check if sensitive data such as **passwords** or **session tokens** are transmitted or stored in an insecure manner (e.g., in **plaintext**).

---

### Step 7: Exploit Vulnerabilities in WackoPicko

1. **SQL Injection**:
   - Try injecting SQL statements like `' OR 1=1 --` into input fields such as login or registration forms.
   - You should be able to bypass the authentication if the application is vulnerable to SQL injection.

2. **Cross-Site Scripting (XSS)**:
   - Inject JavaScript code like `<script>alert('XSS');</script>` into fields such as username, comment, or post fields.
   - If the application reflects the input without sanitization, the script will run in the user's browser.

3. **File Upload Vulnerabilities**:
   - Attempt to upload PHP or other executable files to see if the application allows for **remote code execution**.
   - Try to upload a file named `evil.php` with malicious code.

4. **Cross-Site Request Forgery (CSRF)**:
   - Create a malicious link that can trigger actions like changing the user's email address or password.
   - If the application lacks proper anti-CSRF protections, the attacker can execute such actions on behalf of the user.

5. **Session Management Flaws**:
   - Try logging in and then manipulating the session cookies to gain access to another user's session.
   - Test for vulnerabilities like session fixation or hijacking.

6. **Insecure Direct Object References (IDOR)**:
   - Modify URL parameters such as `user_id=2` to access other users' data or actions.

7. **Sensitive Data Exposure**:
   - Use tools like **Burp Suite** or **Wireshark** to intercept traffic and look for sensitive data in **plaintext** during transmission.
   - Ensure that the application uses **HTTPS** and encrypts sensitive data.

---

### Step 8: Remediate Vulnerabilities

After identifying and exploiting the vulnerabilities, it’s important to apply fixes to secure the application. Below are some **best practices** for remediation:

1. **SQL Injection**:
   - Use **prepared statements** and **parameterized queries** to prevent SQL injection.
   - Sanitize user inputs and validate them before using them in SQL queries.

2. **Cross-Site Scripting (XSS)**:
   - Always **escape** user input before displaying it back to the browser.
   - Implement a **Content Security Policy (CSP)** to restrict the sources from which scripts can be loaded.

3. **File Upload Vulnerabilities**:
   - Limit the types of files that can be uploaded (e.g., only allow image files).
   - Scan uploaded files for malware and store them in a non-executable directory.

4. **Cross-Site Request Forgery (CSRF)**:
   - Use **anti-CSRF tokens** in all forms that perform state-changing actions.
   - Validate the **Origin** or **Referer** headers for sensitive requests.

5. **Session Management Flaws**:
   - Use **secure cookies** with **HttpOnly**, **Secure**, and **SameSite** flags.
   - Implement **session expiration** and ensure that sessions cannot be reused after logout.

6. **Insecure Direct Object References (IDOR)**:
   - Implement **access

 controls** to ensure users can only access their own resources.
   - Validate that users have the appropriate permissions before granting access to resources.

7. **Sensitive Data Exposure**:
   - Use **TLS/SSL** to encrypt sensitive data during transmission.
   - Store passwords securely using **bcrypt** or **Argon2** hashing algorithms.

---

## Conclusion

By completing this lab, you have successfully set up **WackoPicko**, explored its vulnerabilities, and learned how to exploit and secure web applications. This exercise helps you understand common web application vulnerabilities and gain hands-on experience with security tools and techniques.

