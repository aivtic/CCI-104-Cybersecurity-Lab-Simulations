# Lab 7: NodeGoat Guide (Vulnerable Web Application)

**NodeGoat** is a deliberately vulnerable web application built with **Node.js**, designed to teach web application security concepts. Similar to Juice Shop, it allows learners to explore and exploit various vulnerabilities in a safe, controlled environment. NodeGoat covers multiple types of vulnerabilities like **SQL Injection**, **Cross-Site Scripting (XSS)**, and **Broken Authentication**, providing practical exposure to penetration testing.

---

## Lab Objectives

1. Install and configure **NodeGoat**.
2. Explore the vulnerabilities present in NodeGoat.
3. Practice penetration testing techniques and exploit vulnerabilities.
4. Learn how to remediate common vulnerabilities in a web application.

---

## Prerequisites

Before you begin, make sure you meet the following prerequisites:

1. **LAMP Stack** is installed and configured (refer to **Lab 1**).
2. **Node.js** and **npm** are installed on your system.
3. Basic knowledge of web application security and penetration testing.

---

## Step-by-Step Setup

### Step 1: Install Node.js and npm

If you haven't already installed **Node.js** and **npm**, follow the steps below:

1. Update your package list:
   ```bash
   sudo apt update
   ```

2. Install **Node.js** and **npm**:
   ```bash
   sudo apt install nodejs npm -y
   ```

3. Verify the installation of Node.js:
   ```bash
   node -v
   ```

4. Verify the installation of npm:
   ```bash
   npm -v
   ```

---

### Step 2: Install and Configure NodeGoat

1. Navigate to the directory where you want to install NodeGoat:
   ```bash
   cd /var/www/html
   ```

2. Clone the **NodeGoat** repository from GitHub:
   ```bash
   sudo git clone https://github.com/owasp/nodegoat.git
   ```

3. Change to the NodeGoat directory:
   ```bash
   cd nodegoat
   ```

4. Install the required dependencies:
   ```bash
   sudo npm install
   ```

5. Start the NodeGoat application:
   ```bash
   sudo npm start
   ```

6. By default, NodeGoat will run on port `3000`. Open a browser and visit the following URL to access the application:
   ```
   http://localhost:3000
   ```

---

### Step 3: Access the NodeGoat Application

1. Open your browser and visit:
   ```
   http://localhost:3000
   ```

2. You should see the **NodeGoat homepage**. The application is designed to simulate a basic web app with an authentication system and user functionality.

3. The default credentials to log in are:
   - **Username**: admin
   - **Password**: admin

   You can change the password once logged in or register a new user.

---

### Step 4: Explore Vulnerabilities in NodeGoat

NodeGoat includes many common web application vulnerabilities. Here are some key vulnerabilities to look for:

1. **SQL Injection (SQLi)**: Test user input fields for SQL injection vulnerabilities by injecting SQL commands.
2. **Cross-Site Scripting (XSS)**: Look for opportunities to inject malicious JavaScript into input fields.
3. **Cross-Site Request Forgery (CSRF)**: Check if actions can be performed on behalf of a user without their consent.
4. **Insecure Direct Object References (IDOR)**: Try modifying URLs or parameters to access resources that should not be available to you.
5. **Broken Authentication**: Test the login and authentication process for weaknesses like weak session management or predictable credentials.
6. **File Upload Vulnerabilities**: Check if you can upload files that could exploit the application.
7. **Sensitive Data Exposure**: Look for sensitive data like passwords or session tokens in an insecure manner.

---

### Step 5: Exploit Vulnerabilities in NodeGoat

1. **SQL Injection**:
   - Test the login or search forms with malicious SQL input like `' OR 1=1 --`.
   - This should bypass authentication or return unintended results.

2. **Cross-Site Scripting (XSS)**:
   - Try injecting scripts like `<script>alert('XSS');</script>` into various input fields (e.g., login, registration, or comment sections).
   - If the application reflects your input without proper sanitization, the script will execute.

3. **Cross-Site Request Forgery (CSRF)**:
   - Modify HTTP requests (e.g., using **Burp Suite** or **OWASP ZAP**) to forge actions like password changes without the user's consent.
   - If the application does not validate the origin of requests properly, the attacker can perform these actions on behalf of the user.

4. **Insecure Direct Object References (IDOR)**:
   - Modify URL parameters like user IDs or order numbers to access other users' data or perform actions you shouldn’t be able to.

5. **Broken Authentication**:
   - Try to brute-force login credentials using tools like **Hydra** or **Burp Suite**.
   - Test if there are any session management weaknesses like predictable session tokens or lack of session expiration.

6. **File Upload Vulnerabilities**:
   - Attempt to upload malicious files, such as PHP scripts or shell scripts, and see if the server executes them.

7. **Sensitive Data Exposure**:
   - Inspect HTTP responses to check for sensitive data leakage, such as passwords in plaintext or session tokens in URLs.

---

### Step 6: Remediate Vulnerabilities

After successfully exploiting vulnerabilities, the next step is to learn how to secure the application. Here are some best practices to secure **NodeGoat** and similar applications:

1. **SQL Injection**:
   - Use **parameterized queries** and **prepared statements** to avoid SQL injection vulnerabilities.
   - Validate and sanitize all user inputs.

2. **Cross-Site Scripting (XSS)**:
   - Always sanitize and escape user inputs to prevent JavaScript execution.
   - Implement **Content Security Policy (CSP)** headers to restrict script execution.

3. **Cross-Site Request Forgery (CSRF)**:
   - Use **anti-CSRF tokens** for every state-changing request (e.g., password change).
   - Verify the **Origin** and **Referer** headers for requests that modify data.

4. **Insecure Direct Object References (IDOR)**:
   - Always perform **access control checks** before serving or modifying resources.
   - Validate user input to ensure they can only access their own data.

5. **Broken Authentication**:
   - Enforce strong password policies and implement **multi-factor authentication** (MFA).
   - Use **secure session management** by setting **HttpOnly**, **Secure**, and **SameSite** flags for cookies.

6. **File Upload Vulnerabilities**:
   - Limit the types of files users can upload (e.g., only images or PDFs).
   - Scan uploaded files for malicious content using tools like **ClamAV**.

7. **Sensitive Data Exposure**:
   - Always use **HTTPS** to encrypt sensitive data in transit.
   - Store sensitive data, like passwords, using secure hashing algorithms (e.g., **bcrypt**).

---

### Step 7: Explore Additional Features in NodeGoat

1. **CTF Challenges**:
   - NodeGoat includes **Capture The Flag (CTF)** challenges that guide you through exploiting specific vulnerabilities.
   - Completing these challenges will deepen your understanding of web application security.

2. **REST API**:
   - NodeGoat provides a **REST API** that you can test for vulnerabilities.
   - Try sending **malicious** requests through tools like **Postman** or **Burp Suite**.

3. **Authentication & Authorization**:
   - Explore how **JWT tokens** are used in authentication.
   - Try to perform **privilege escalation** by manipulating tokens.

4. **Security Headers**:
   - Check if the app sends **security headers** like **Strict-Transport-Security (HSTS)** or **X-Content-Type-Options**.
   - Learn how to configure these headers for better security.

---

## Conclusion

You have successfully set up **NodeGoat** and explored common vulnerabilities in a web application, including SQL injection, XSS, and broken authentication. You’ve learned how to exploit these vulnerabilities and how to remediate them to secure a vulnerable application.

---

## Further Exploration

1. **Automated Scanning Tools**:
   - Use tools like **OWASP ZAP** or **Burp Suite** to scan NodeGoat for vulnerabilities and learn how automated tools can identify weaknesses.
   
2. **Security Practices**:
   - Study the OWASP **Top 10** and implement best security practices in real-world applications.

3. **Web Application Firewalls (WAFs)**:
   - Explore how a **WAF** can mitigate common attacks like SQLi and XSS in NodeGoat.
  
---

For more information and challenges related to **NodeGoat**, check out the official repository:  
[NodeGoat GitHub Repository](https://github.com/owasp/nodegoat)