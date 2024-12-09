# Lab 5: Hackazon (Vulnerable Web Application) Setup and Exploration

**Hackazon** is an intentionally vulnerable web application that mimics real-world applications for security testing, penetration testing, and ethical hacking training. Hackazon is designed to provide hands-on experience with common vulnerabilities and attack techniques, making it a great learning tool for students in the **Certified Cybersecurity Instructor Programme**.

---

## Lab Objectives

1. Install and configure Hackazon on your LAMP stack environment.
2. Explore the various vulnerabilities in Hackazon.
3. Practice penetration testing techniques on a vulnerable application.
4. Learn how to secure the application after identifying vulnerabilities.

---

## Prerequisites

Ensure the following before starting:

1. **LAMP Stack** is installed and configured correctly (validated in **Lab 1**).
2. **Git** is installed to clone the Hackazon repository.
3. **Docker** is installed to run Hackazon in a container (optional, but recommended for easier management).
4. Basic understanding of web application vulnerabilities and penetration testing.

---

## Step-by-Step Setup

### Step 1: Install Docker (Optional but Recommended)

While Hackazon can be installed manually, using Docker simplifies the installation process. If you don’t have Docker installed, follow these steps to install it:

1. Update the package index:
   ```bash
   sudo apt update
   ```

2. Install Docker:
   ```bash
   sudo apt install docker.io -y
   ```

3. Start and enable Docker service:
   ```bash
   sudo systemctl start docker
   sudo systemctl enable docker
   ```

4. Verify Docker installation:
   ```bash
   sudo docker --version
   ```

---

### Step 2: Clone the Hackazon Repository

If you're using Docker, you can directly pull the Hackazon image. However, if you wish to manually install Hackazon, you can clone it from GitHub.

#### Option 1: Using Docker

1. Pull the Hackazon Docker image:
   ```bash
   sudo docker pull hackazon/hackazon
   ```

2. Run Hackazon in a Docker container:
   ```bash
   sudo docker run -d -p 8080:8080 hackazon/hackazon
   ```

   This command runs the Hackazon container in the background and maps port 8080 of the container to port 8080 on your server.

#### Option 2: Manually Installing Hackazon

1. Navigate to the web root directory:
   ```bash
   cd /var/www/html
   ```

2. Clone the Hackazon repository:
   ```bash
   sudo git clone https://github.com/rapid7/hackazon.git
   ```

3. Change to the Hackazon directory:
   ```bash
   cd hackazon
   ```

4. Install the required dependencies (Apache, MySQL, PHP):
   ```bash
   sudo apt install apache2 mysql-server php php-mysqli php-xml libapache2-mod-php -y
   ```

5. Configure MySQL and create a Hackazon database:

   Log in to MySQL:
   ```bash
   sudo mysql -u root -p
   ```

   Create the Hackazon database:
   ```sql
   CREATE DATABASE hackazon;
   ```

   Create the database tables:
   ```bash
   sudo mysql hackazon < hackazon.sql
   ```

---

### Step 3: Configure Apache for Hackazon

1. Create an Apache virtual host for Hackazon. Open the Apache configuration file:
   ```bash
   sudo nano /etc/apache2/sites-available/hackazon.conf
   ```

2. Add the following configuration:
   ```apache
   <VirtualHost *:80>
       ServerAdmin webmaster@localhost
       DocumentRoot /var/www/html/hackazon
       ServerName hackazon.local

       ErrorLog ${APACHE_LOG_DIR}/error.log
       CustomLog ${APACHE_LOG_DIR}/access.log combined
   </VirtualHost>
   ```

3. Enable the new site configuration:
   ```bash
   sudo a2ensite hackazon.conf
   sudo systemctl restart apache2
   ```

---

### Step 4: Access Hackazon in the Browser

1. Open your browser and go to:
   ```
   http://<your-server-ip>/hackazon
   ```

2. The Hackazon login page should appear. The default credentials are:
   - **Username**: `admin`
   - **Password**: `admin`

3. After logging in, you will be directed to the Hackazon homepage, where you can explore various vulnerabilities and challenges.

---

### Step 5: Explore Hackazon Vulnerabilities

Hackazon contains a wide range of vulnerabilities, including:

1. **SQL Injection**: Learn how attackers exploit vulnerable input fields to manipulate the database.
2. **Cross-Site Scripting (XSS)**: Discover how attackers inject malicious scripts into web pages.
3. **Cross-Site Request Forgery (CSRF)**: Understand how attackers can trick users into making unwanted requests.
4. **Authentication Bypass**: Test the application's authentication mechanisms for weaknesses.
5. **File Upload Vulnerabilities**: Explore how insecure file upload features can lead to remote code execution.

Each vulnerability in Hackazon is designed to simulate a common security flaw that can be exploited by attackers.

---

### Step 6: Exploit Vulnerabilities

1. Start by exploring the **SQL Injection** vulnerability:
   - Look for input fields that interact with the database (e.g., search bars, login forms).
   - Use SQL injection techniques such as `' OR 1=1 --` to bypass authentication and retrieve data from the database.

2. Explore **XSS** vulnerabilities:
   - Try injecting JavaScript code into input fields and observing how the application handles it.
   - Use tools like **Burp Suite** or **OWASP ZAP** to identify additional XSS vulnerabilities.

3. Investigate **File Upload Vulnerabilities**:
   - Test the file upload functionality by uploading malicious files, such as PHP shells or reverse shells.

4. Complete the challenges provided in the Hackazon interface, following each vulnerability's instructions.

---

### Step 7: Remediation

After exploiting the vulnerabilities in Hackazon, the next step is to learn how to secure the application. For each vulnerability, research and apply remediation techniques:

1. **SQL Injection**: Use parameterized queries or prepared statements to prevent SQL injection attacks.
2. **XSS**: Sanitize user input and implement Content Security Policies (CSP) to mitigate XSS attacks.
3. **CSRF**: Implement anti-CSRF tokens to prevent unauthorized requests from being submitted on behalf of the user.
4. **Authentication Bypass**: Use multi-factor authentication (MFA) and strong password policies to secure user accounts.
5. **File Upload**: Validate file types and restrict file sizes to prevent malicious file uploads.

---

## Conclusion

- You've successfully installed and configured **Hackazon** on your LAMP stack environment.
- You have explored various vulnerabilities within Hackazon and practiced penetration testing techniques to exploit them.
- By identifying and remediating vulnerabilities, you’ve learned important skills that are essential in securing web applications.

---

## Further Exploration

1. **Penetration Testing Tools**: Integrate tools like **Burp Suite**, **OWASP ZAP**, and **Nikto** to help discover more vulnerabilities.
2. **Security Best Practices**: Implement the security best practices discussed during remediation to secure web applications against common attacks.
3. **OWASP Top 10**: Continue practicing and exploring the OWASP Top 10 vulnerabilities and how to defend against them.

---

For more details on Hackazon and the associated challenges, visit:  
[Hackazon GitHub Repository](https://github.com/rapid7/hackazon)