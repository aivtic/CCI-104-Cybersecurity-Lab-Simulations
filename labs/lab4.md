# Lab 4: WebGoat (Vulnerable Web Application) Setup and Exploration

**WebGoat** is an intentionally vulnerable web application designed by OWASP for the purpose of educating and testing cybersecurity enthusiasts. It simulates common vulnerabilities found in real-world applications and provides a safe environment for penetration testing and security training.

---

## Lab Objectives

1. Install and configure WebGoat on your LAMP stack environment.
2. Explore and exploit various vulnerabilities within WebGoat.
3. Practice penetration testing techniques to understand common web application vulnerabilities and how to mitigate them.

---

## Prerequisites

Before starting, ensure:

1. LAMP stack is installed and functioning correctly (validated in **Lab 1**).
2. You have root or sudo access to the server.
3. Your machine and the testing machine (e.g., Kali Linux) are on the same network.
4. Java is installed on your Ubuntu server, as WebGoat runs on a Java platform.

---

## Step-by-Step Setup

### Step 1: Install Java (if not already installed)

1. WebGoat requires Java to run. Ensure that Java is installed:
   ```bash
   java -version
   ```

2. If Java is not installed, run the following commands:
   ```bash
   sudo apt update
   sudo apt install openjdk-11-jdk -y
   ```

3. Verify Java installation:
   ```bash
   java -version
   ```

---

### Step 2: Download WebGoat

1. Navigate to the web root directory:
   ```bash
   cd /var/www/html
   ```

2. Download the latest release of WebGoat from GitHub:
   ```bash
   sudo git clone https://github.com/OWASP/WebGoat.git
   ```

3. Change directory to the WebGoat folder:
   ```bash
   cd WebGoat
   ```

4. Run the WebGoat application:
   ```bash
   ./mvnw clean install
   ```

   This command installs all required dependencies and compiles the WebGoat application.

---

### Step 3: Start WebGoat

1. Once the build is successful, you can start WebGoat using:
   ```bash
   ./mvnw spring-boot:run
   ```

2. The WebGoat application should now be running on `http://localhost:8080` (or replace `localhost` with your server’s IP address).

---

### Step 4: Access WebGoat in the Browser

1. Open your browser and go to:
   ```
   http://<your-server-ip>:8080/WebGoat
   ```

2. The WebGoat login page should appear. Use the default login credentials:
   - **Username**: `guest`
   - **Password**: `guest`

3. After logging in, you’ll be directed to the main WebGoat interface where various exercises are available.

---

### Step 5: Explore WebGoat Vulnerabilities

WebGoat provides several lessons that simulate common web vulnerabilities. Some of the available lessons include:

1. **SQL Injection**: Learn how attackers exploit SQL Injection vulnerabilities to manipulate databases.
2. **Cross-Site Scripting (XSS)**: Understand how malicious scripts can be injected into trusted websites.
3. **Insecure Cryptography**: Learn how poor cryptographic practices can lead to compromised sensitive data.
4. **Cross-Site Request Forgery (CSRF)**: Explore how attackers can trick users into performing unwanted actions.
5. **Session Management**: Learn about vulnerabilities in session handling that can lead to session hijacking.
6. **File Upload Vulnerabilities**: Learn how attackers exploit insecure file upload functionalities.

### Step 6: Start Working on the Lessons

1. In the WebGoat interface, select a vulnerability lesson (e.g., **SQL Injection**).
2. Each lesson provides a description of the vulnerability and steps to exploit it.
3. Follow the instructions provided in the lesson to exploit the vulnerability. For example, in SQL Injection, you’ll practice injecting malicious SQL queries into the input fields to manipulate the database.

4. Record your steps and findings to understand how the vulnerability can be exploited and what mitigation techniques can be used.

---

### Step 7: Use Penetration Testing Tools

1. To assist with vulnerability testing, tools such as **Burp Suite**, **OWASP ZAP**, and **Nikto** can be used to analyze WebGoat and identify potential weaknesses.

2. For example, use **Burp Suite** to intercept and modify requests, or **OWASP ZAP** to scan for XSS vulnerabilities.

---

## Conclusion

- You've successfully installed and configured **WebGoat** on your LAMP stack environment.
- You now have access to a range of web application vulnerabilities that you can explore and exploit in a safe environment.
- The hands-on practice with WebGoat provides invaluable experience in identifying and mitigating common security flaws found in real-world applications.

---

## Further Exploration

1. **Penetration Testing Tools**: Consider integrating WebGoat with penetration testing tools like **Burp Suite** or **OWASP ZAP** to enhance your testing capabilities.
2. **Security Best Practices**: After identifying vulnerabilities, look into how these issues can be mitigated by implementing secure coding practices and employing industry-standard security techniques.
3. **OWASP Top 10**: Review and practice each of the OWASP Top 10 vulnerabilities and their mitigations through WebGoat’s lessons.

---

By completing this lab, students will gain practical skills in exploiting common web application vulnerabilities and learn how to safeguard against them.

---

For more details and to access the WebGoat documentation, visit:  
[WebGoat Official Site](https://owasp.org/www-project-webgoat/)