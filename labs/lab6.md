#Lab 6: OWASP Juice Shop Guide (Vulnerable Web Application)

**OWASP Juice Shop** is an intentionally vulnerable web application for training purposes, offering a great learning experience for penetration testers and ethical hackers. It contains a wide range of vulnerabilities from the **OWASP Top 10** and beyond. Juice Shop simulates a modern e-commerce website and is ideal for practical experience in finding and exploiting web application vulnerabilities.

---

## Lab Objectives

1. Install and configure **OWASP Juice Shop**.
2. Explore the vulnerabilities in Juice Shop.
3. Practice penetration testing techniques and exploit common web application security flaws.
4. Learn to secure the application by identifying and remediating vulnerabilities.

---

## Prerequisites

Ensure that the following conditions are met before proceeding:

1. **LAMP Stack** is installed and configured correctly (as validated in **Lab 1**).
2. **Node.js** and **npm** are installed (required for Juice Shop).
3. Basic knowledge of web application security and penetration testing techniques.

---

## Step-by-Step Setup

### Step 1: Install Node.js and npm

1. Update the package list:
   ```bash
   sudo apt update
   ```

2. Install **Node.js** and **npm** (Node Package Manager):
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

### Step 2: Install and Configure OWASP Juice Shop

1. Navigate to the directory where you want to install Juice Shop:
   ```bash
   cd /var/www/html
   ```

2. Clone the **OWASP Juice Shop** repository from GitHub:
   ```bash
   sudo git clone https://github.com/juice-shop/juice-shop.git
   ```

3. Change to the Juice Shop directory:
   ```bash
   cd juice-shop
   ```

4. Install the required dependencies:
   ```bash
   sudo npm install
   ```

5. Start the Juice Shop application:
   ```bash
   sudo npm start
   ```

6. Juice Shop will now be accessible on your local machine. The application typically runs on port `3000`. Open a browser and visit the following URL:
   ```
   http://localhost:3000
   ```

---

### Step 3: Access the Juice Shop Application

1. Open your browser and go to:
   ```
   http://localhost:3000
   ```

2. The **Juice Shop** homepage should load. It is designed to look like an e-commerce store selling juice and related products.

3. The default user account for Juice Shop is **admin** with no password. However, there are other ways to interact with the app, including registering new accounts and exploring different security features.

---

### Step 4: Explore Juice Shop Vulnerabilities

OWASP Juice Shop contains a range of common vulnerabilities, including:

1. **SQL Injection (SQLi)**: Test for vulnerabilities in database queries by injecting SQL commands into user input fields.
2. **Cross-Site Scripting (XSS)**: Check for vulnerable input fields where JavaScript code can be injected.
3. **Cross-Site Request Forgery (CSRF)**: Discover hidden vulnerabilities where the application allows malicious requests from an authenticated user.
4. **Insecure Direct Object References (IDOR)**: Manipulate URLs to access resources or data that are not intended to be available to the user.
5. **Broken Authentication**: Test the login page and authentication system for weaknesses that allow bypassing login or privilege escalation.
6. **File Upload Vulnerabilities**: Attempt to upload malicious files to the server.
7. **Sensitive Data Exposure**: Investigate if sensitive data is exposed through insecure communication or storage.

### Using Burp Suite or OWASP ZAP:
- You can use **Burp Suite** or **OWASP ZAP** to test for these vulnerabilities. These tools can help identify XSS, CSRF, and SQL injection vulnerabilities by intercepting and modifying HTTP requests.

---

### Step 5: Exploit Vulnerabilities in Juice Shop

Explore and exploit each vulnerability in the Juice Shop application. Here are some common attacks you can perform:

1. **SQL Injection**:
   - Look for login forms or search functionality.
   - Try injecting SQL commands like `' OR 1=1 --` to bypass authentication.

2. **XSS (Cross-Site Scripting)**:
   - Inject JavaScript into input fields like contact forms, search bars, or product reviews.
   - Observe if the application reflects the input without sanitizing it, allowing execution of JavaScript.

3. **CSRF (Cross-Site Request Forgery)**:
   - Look for actions that can be performed without re-authentication, such as changing user details or performing transactions.
   - Try submitting requests without user consent using tools like **Burp Suite** or **OWASP ZAP**.

4. **IDOR (Insecure Direct Object References)**:
   - Modify URLs or parameters to access data you shouldn’t have access to.
   - For example, change the user ID in the URL to try accessing someone else’s data.

5. **Broken Authentication**:
   - Test the login form for weaknesses like predictable credentials or weak session management.
   - Try brute-forcing the login page using tools like **Hydra**.

6. **File Upload Vulnerabilities**:
   - Attempt to upload a file with a dangerous payload (e.g., PHP script or reverse shell).
   - Observe how the application handles file uploads and whether it allows unsafe files.

---

### Step 6: Remediate Vulnerabilities

After exploiting each vulnerability, the next step is to learn how to secure the application. Here are some best practices to secure a vulnerable web application like Juice Shop:

1. **SQL Injection**:
   - Use prepared statements and parameterized queries to avoid SQL injection vulnerabilities.

2. **XSS (Cross-Site Scripting)**:
   - Sanitize and escape user inputs.
   - Implement a **Content Security Policy (CSP)** to limit which scripts can execute on the page.

3. **CSRF (Cross-Site Request Forgery)**:
   - Implement anti-CSRF tokens for all state-changing requests (e.g., changing passwords, making purchases).
   - Ensure the application verifies the **Origin** and **Referer** headers.

4. **IDOR (Insecure Direct Object References)**:
   - Use proper authorization checks to ensure that users can only access data they are authorized to view.

5. **Broken Authentication**:
   - Enforce strong password policies and implement multi-factor authentication (MFA).
   - Secure session management, such as using secure and HttpOnly flags for cookies.

6. **File Upload Vulnerabilities**:
   - Only allow safe file types to be uploaded (e.g., images or PDFs).
   - Scan uploaded files for malicious content and restrict executable files.

---

### Step 7: Explore Additional Juice Shop Features

OWASP Juice Shop provides various challenges to help you learn and exploit the application, including:

1. **Capture the Flag (CTF)**: Juice Shop has a set of **CTF challenges** that you can solve as you exploit the application. Completing these challenges will help reinforce your understanding of web application vulnerabilities.

2. **Admin Panel**: Access the admin panel to perform administrative tasks, such as managing users and viewing logs.

3. **REST API**: Juice Shop exposes a **REST API** that you can interact with. Explore how vulnerabilities in the API can be exploited and learn how to secure them.

4. **Security Headers**: Investigate missing security headers, like **X-Content-Type-Options**, **Strict-Transport-Security (HSTS)**, and **X-Frame-Options**, and learn how to implement them in a production environment.

---

## Conclusion

- You’ve successfully set up **OWASP Juice Shop** and explored various common vulnerabilities.
- By exploiting and securing the vulnerabilities, you've gained hands-on experience in penetration testing and ethical hacking.
- The next step is to apply the knowledge gained in securing real-world applications.

---

## Further Exploration

1. **Automated Vulnerability Scanners**: Try running automated tools like **OWASP ZAP** or **Burp Suite** against Juice Shop to identify vulnerabilities faster.
2. **Web Application Firewalls (WAFs)**: Explore how a WAF can block common attacks like SQL injection and XSS in Juice Shop.
3. **OWASP Top 10**: Continue practicing the **OWASP Top 10** vulnerabilities, as Juice Shop covers many of these issues.

---

For more details on **OWASP Juice Shop**, check out the official repository:  
[OWASP Juice Shop GitHub Repository](https://github.com/juice-shop/juice-shop)