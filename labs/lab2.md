
# Lab 2: Mutillidae II Setup and Exploration  

This lab focuses on deploying **Mutillidae II**, an intentionally vulnerable web application designed for security training. It offers a hands-on opportunity to explore, understand, and exploit common web vulnerabilities in a controlled environment.

---

## Lab Objectives  

1. Install and configure Mutillidae II on the pre-installed LAMP stack.  
2. Understand the structure of a vulnerable web application.  
3. Test and document various web application vulnerabilities using industry-standard tools.  

---

## Prerequisites  

Before beginning, ensure you have the following ready:  

1. **Ubuntu Server** with a working LAMP stack (set up in Lab 1).  
2. **Root or sudo access** for administrative tasks.  
3. **Basic Linux knowledge**, including navigating directories and using commands.  
4. **A secondary machine (attacker’s machine)**, such as Kali Linux, for testing.  
5. **Network connectivity** between the target (Ubuntu Server) and the attacker’s machine.  

---

## Step-by-Step Setup  

### Step 1: Verify LAMP Stack Configuration  

Confirm the LAMP stack is functional by creating a simple PHP file and accessing it from a browser:  

1. Create a test PHP file:  
   ```bash  
   echo "<?php phpinfo(); ?>" | sudo tee /var/www/html/info.php  
   ```  

2. Access it in your browser:  
   ```
   http://<your-server-ip>/info.php  
   ```  

   If the PHP configuration page loads, your LAMP stack is ready.

3. Delete the test file for security:  
   ```bash  
   sudo rm /var/www/html/info.php  
   ```  

---

### Step 2: Navigate to the Web Root  

All web applications hosted on the LAMP stack reside in the `/var/www/html` directory. Move into this directory:  

```bash  
cd /var/www/html  
```  

---

### Step 3: Download Mutillidae II  

1. Clone the Mutillidae II repository from GitHub:  
   ```bash  
   sudo git clone https://github.com/webpwnized/mutillidae.git  
   sudo mv mutillidae mutillidae-II  
   ```  

2. Set correct permissions for the application files:  
   ```bash  
   sudo chown -R www-data:www-data /var/www/html/mutillidae-II  
   sudo chmod -R 755 /var/www/html/mutillidae-II  
   ```  

---

### Step 4: Verify PHP Extensions  

Ensure the `mysqli` extension is enabled, as it is critical for database interaction:  

1. Check if `mysqli` is active:  
   ```bash  
   php -m | grep mysqli  
   ```  

2. If not installed, add it:  
   ```bash  
   sudo apt install php-mysqli -y  
   sudo systemctl restart apache2  
   ```  

---

### Step 5: Access Mutillidae II  

1. Open a browser and navigate to:  
   ```
   http://<your-server-ip>/mutillidae-II  
   ```  

2. You should see the Mutillidae II home page. If not, revisit the previous steps to verify your configuration.

---

### Step 6: Initialize the Database  

1. On the Mutillidae II interface, locate the **Setup/reset the DB** option.  
2. Click this button to initialize the database schema and seed the data.  
3. Confirm that the application is fully operational by browsing through its features.  

---

## Exploring Vulnerabilities  

### Understanding Vulnerability Categories  

Mutillidae II simulates real-world vulnerabilities categorized as:  

- **Injection Flaws** (SQL, Command Injection)  
- **Cross-Site Scripting (XSS)**  
- **Cross-Site Request Forgery (CSRF)**  
- **Insecure Direct Object References (IDOR)**  
- **Authentication and Session Management Flaws**  
- **Security Misconfigurations**  

---

### Example Testing Scenarios  

#### **Scenario 1: SQL Injection**  

1. Navigate to **User Info** or any similar feature that accepts input.  
2. Enter the payload `' OR '1'='1` into an input field.  
3. Observe if all records from the database are displayed.  

   - **Tools**: Use `SQLmap` for advanced testing:  
     ```bash  
     sqlmap -u "http://<your-server-ip>/mutillidae-II/page.php?param=value" --dbs  
     ```  

---

#### **Scenario 2: Cross-Site Scripting (XSS)**  

1. Navigate to a search or comment feature.  
2. Enter a simple XSS payload:  
   ```html  
   <script>alert('XSS Vulnerability');</script>  
   ```  
3. Observe whether the browser executes the script.  

   - **Tools**: Use **OWASP ZAP** or **Burp Suite** to test for XSS vulnerabilities systematically.  

---

#### **Scenario 3: Scanning with OWASP ZAP**  

1. Launch OWASP ZAP on your Kali Linux machine.  
2. Set the target to:  
   ```
   http://<your-server-ip>/mutillidae-II  
   ```  
3. Perform a full scan and analyze the results.  

---

## Advanced Usage  

### Enhancing Security Testing  

1. **Password Attacks**: Use Hydra to test for weak passwords:  
   ```bash  
   hydra -l admin -P /path/to/password-list.txt <your-server-ip> http-post-form "/mutillidae-II/login.php:username=^USER^&password=^PASS^:Invalid username or password"  
   ```  

2. **Command Injection**: Locate areas that execute system commands and test with payloads like:  
   ```
   ; cat /etc/passwd  
   ```  

---

### Resetting the Environment  

To reset the application to its original state, use the **Setup/reset the DB** option on the Mutillidae II interface.  

---

## Notes and Best Practices  

1. **Isolate the Lab**: Use a separate network or virtual environment to contain potential risks.  
2. **Log Findings**: Document all vulnerabilities discovered, along with the steps and tools used.  
3. **Regular Updates**: Keep the Mutillidae II repository updated to leverage any new features.  

---

## Additional Resources  

- [Mutillidae II GitHub Repository](https://github.com/webpwnized/mutillidae)  
- [OWASP Top 10 Vulnerabilities](https://owasp.org/www-project-top-ten/)  
- [Kali Linux Tools Documentation](https://www.kali.org/docs/tools/)  

---
