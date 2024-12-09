# Lab 3: bWAPP (Buggy Web Application) Setup and Exploration

**bWAPP (Buggy Web Application)** is another intentionally vulnerable web application designed for security professionals and enthusiasts to practice web application security testing. It simulates real-world vulnerabilities, allowing students to safely exploit them in a controlled environment.

---

## Lab Objectives

1. Deploy and configure bWAPP on the pre-installed LAMP stack.
2. Explore and exploit various web vulnerabilities within bWAPP.
3. Practice using penetration testing tools and techniques to identify and exploit vulnerabilities.

---

## Prerequisites

Before proceeding, ensure:

1. LAMP stack is installed and functioning correctly (validated in **Lab 1**).
2. You have root or sudo access to the server.
3. Your machine and the testing machine (e.g., Kali Linux) are on the same network.
4. PHP extensions `mysqli` and `gd` are installed.

---

## Step-by-Step Setup

### Step 1: Install Required PHP Extensions (If Not Already Installed)

1. Ensure the following PHP extensions are installed:
   - `mysqli`
   - `gd`
   - `mbstring`

2. Install missing extensions (if necessary):
   ```bash
   sudo apt update
   sudo apt install php-mysqli php-gd php-mbstring -y
   sudo systemctl restart apache2
   ```

3. Confirm installation:
   ```bash
   php -m | grep -E 'mysqli|gd|mbstring'
   ```

---

### Step 2: Download and Deploy bWAPP

1. Change to the web root directory:
   ```bash
   cd /var/www/html
   ```

2. Download bWAPP from the official GitHub repository:
   ```bash
   sudo git clone https://github.com/ethicalhack3r/bWAPP.git
   ```

3. Set the correct file permissions for the bWAPP directory:
   ```bash
   sudo chown -R www-data:www-data /var/www/html/bWAPP
   sudo chmod -R 755 /var/www/html/bWAPP
   ```

---

### Step 3: Configure bWAPP

1. Navigate to the bWAPP directory:
   ```bash
   cd /var/www/html/bWAPP
   ```

2. Copy the configuration file:
   ```bash
   sudo cp config.inc.php.sample config.inc.php
   ```

3. Open the configuration file for editing:
   ```bash
   sudo nano config.inc.php
   ```

4. Update the database settings in `config.inc.php` to match your MySQL credentials:
   ```php
   define('DB_SERVER', 'localhost');
   define('DB_USERNAME', 'root');  // Your MySQL username
   define('DB_PASSWORD', 'your_mysql_password');  // Your MySQL password
   define('DB_DATABASE', 'bwapp');  // Database name
   ```

5. Save and exit the editor (Ctrl + O, Enter, Ctrl + X).

---

### Step 4: Create and Set Up the bWAPP Database

1. Log into MySQL:
   ```bash
   mysql -u root -p
   ```

2. Create a database for bWAPP:
   ```sql
   CREATE DATABASE bwapp;
   ```

3. Import the bWAPP database schema:
   ```bash
   exit
   sudo mysql -u root -p bwapp < /var/www/html/bWAPP/install.sql
   ```

---

### Step 5: Set Up the bWAPP Application

1. Open bWAPP in your browser:
   ```
   http://<your-server-ip>/bWAPP
   ```

2. Use the default login credentials:
   - **Username**: `bee`
   - **Password**: `bug`

3. Once logged in, you should see the bWAPP dashboard with a variety of vulnerabilities to choose from.

---

### Step 6: Explore the Vulnerabilities

1. From the **Vulnerabilities** section, you can select various categories of vulnerabilities to explore:
   - **SQL Injection**
   - **Cross-Site Scripting (XSS)**
   - **Cross-Site Request Forgery (CSRF)**
   - **File Inclusion**
   - **Command Injection**
   - **Remote File Inclusion (RFI)**
   - **Session Management**
   - And many others.

2. Select a vulnerability (e.g., SQL Injection), and follow the instructions provided to exploit it.

3. Optionally, use tools such as **Burp Suite** or **OWASP ZAP** to assist in testing and exploiting these vulnerabilities.

---

### Step 7: Modify Security Levels

1. On the main dashboard, you can change the security level of the application. The default level is **Low**, but you can increase the difficulty by selecting **Medium** or **High**.

2. Each security level will introduce additional layers of protection, simulating more advanced security mechanisms that can be bypassed with more sophisticated techniques.

---

## Conclusion

- You’ve successfully set up **bWAPP** on your LAMP stack.
- You now have a fully functional vulnerable web application environment for ethical hacking practice.
- Use this lab to explore common web vulnerabilities, understand their impacts, and practice the exploitation techniques that ethical hackers use.

---

## Further Exploration

1. **Penetration Testing Tools**: Consider using tools like **Burp Suite**, **OWASP ZAP**, or **Nikto** to test for vulnerabilities.
2. **Security Research**: Explore the OWASP Top 10 vulnerabilities and practice identifying them in bWAPP.
3. **Document Your Findings**: Record the steps taken to exploit each vulnerability and learn how to patch them effectively.  

---

By completing this lab, students will develop an in-depth understanding of how web applications can be attacked and the tools used to identify vulnerabilities. This hands-on practice is essential for preparing for real-world penetration testing scenarios.

--- 

For more details, please refer to the bWAPP documentation: [bWAPP Official Site](http://www.itsecgames.com/)