
# Lab 1: Damn Vulnerable Web Application (DVWA)  

Welcome to Lab 1, where you will set up and explore the **Damn Vulnerable Web Application (DVWA)**. DVWA is a PHP/MySQL-based web application intentionally designed to be vulnerable. It is an excellent resource for practicing ethical hacking techniques and learning about web security.  

---

## Objectives  

- Set up DVWA on Ubuntu Server.  
- Understand common web application vulnerabilities.  
- Perform initial vulnerability assessment.  

---

## Prerequisites  

Before starting this lab, ensure the following requirements are met:  

1. **Ubuntu Server installed and running.**  
2. **Basic familiarity with Linux commands.**  
3. **LAMP stack (Linux, Apache, MySQL, PHP) installed and configured.**  
4. **Root or sudo access to the server.**  

---

## Step-by-Step Guide  

### Step 1: Update Your System  

Update your system to ensure you have the latest software versions.  
```bash  
sudo apt update && sudo apt upgrade -y  
```  

---

### Step 2: Install LAMP Stack  

Install the required components of the LAMP stack.  

#### Install Apache  
```bash  
sudo apt install apache2 -y  
sudo systemctl enable apache2  
sudo systemctl start apache2  
```  

#### Install MySQL  
```bash  
sudo apt install mysql-server -y  
sudo mysql_secure_installation  
```  

Follow the prompts to secure your MySQL installation.  

#### Install PHP  
```bash  
sudo apt install php libapache2-mod-php php-mysql -y  
```  

Restart Apache to apply the changes.  
```bash  
sudo systemctl restart apache2  
```  

---

### Step 3: Download DVWA  

Navigate to the web directory and download DVWA from its official GitHub repository.  
```bash  
cd /var/www/html  
sudo git clone https://github.com/digininja/DVWA.git  
sudo mv DVWA dvwa  
```  

Set the correct permissions:  
```bash  
sudo chown -R www-data:www-data /var/www/html/dvwa  
sudo chmod -R 755 /var/www/html/dvwa  
```  

---

### Step 4: Configure DVWA  

Navigate to the DVWA directory:  
```bash  
cd /var/www/html/dvwa/config  
```  

Copy the sample configuration file and edit it:  
```bash  
sudo cp config.inc.php.dist config.inc.php  
sudo nano config.inc.php  
```  

Update the database credentials. Use the following default values or your custom MySQL credentials:  
```php  
$_DVWA[ 'db_user' ] = 'root';  
$_DVWA[ 'db_password' ] = '';  
$_DVWA[ 'db_database' ] = 'dvwa';  
```  

Save and exit the file (`Ctrl+O`, `Enter`, `Ctrl+X`).  

---

### Step 5: Set Up the Database  

Log in to MySQL and create the DVWA database.  
```bash  
sudo mysql -u root -p  
```  

Run the following commands in the MySQL prompt:  
```sql  
CREATE DATABASE dvwa;  
GRANT ALL PRIVILEGES ON dvwa.* TO 'root'@'localhost';  
FLUSH PRIVILEGES;  
EXIT;  
```  

---

### Step 6: Adjust PHP Settings  

Modify the `php.ini` file to enable the required settings for DVWA.  
```bash  
sudo nano /etc/php/*/apache2/php.ini  
```  

Ensure the following settings are enabled:  
```ini  
allow_url_include = On  
allow_url_fopen = On  
```  

Save and exit the file, then restart Apache.  
```bash  
sudo systemctl restart apache2  
```  

---

### Step 7: Access DVWA  

Open your web browser and navigate to:  
```
http://<your-server-ip>/dvwa  
```  

You will see the DVWA setup page. Follow the on-screen instructions to complete the installation.  

---

### Step 8: Set Security Level  

Log in using the default credentials:  
- **Username:** admin  
- **Password:** password  

Go to the **DVWA Security** tab and set the security level to "Low" for testing purposes.  

---

### Step 9: Perform Vulnerability Testing  

Explore the different vulnerabilities available in DVWA, such as:  
- SQL Injection  
- Cross-Site Scripting (XSS)  
- Command Injection  
- File Upload  

Use tools like **Burp Suite**, **OWASP ZAP**, or custom scripts to test these vulnerabilities.  

---

## Notes and Best Practices  

- **Isolate the Lab:** Always isolate DVWA in a controlled lab environment. Do not expose it to the internet.  
- **Take Backups:** Regularly back up your VM or server to restore it to a clean state.  
- **Use Logs for Learning:** Analyze server and application logs to understand attack patterns and responses.  

---

## Resources  

- [DVWA Official GitHub Repository](https://github.com/digininja/DVWA)  
- [OWASP Web Security Testing Guide](https://owasp.org/www-project-web-security-testing-guide/)  
- [Kali Linux Documentation](https://www.kali.org/docs/)  

---
