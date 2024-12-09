
# Lab 10 - Altoro Mutual Setup

**Altoro Mutual** is a vulnerable web application designed for training on web application security. This lab will guide you through the process of setting up Altoro Mutual, which is used to practice penetration testing and ethical hacking skills.

#### **Repository**
You can clone the Altoro Mutual repository from the following link:

- **GitHub Repository**: [Altoro Mutual GitHub](https://github.com/AppSecDev/AltoroJ/)

#### **Prerequisites**
- **LAMP Stack (Linux, Apache, MySQL, PHP)** must be installed and configured on your system (as set up in **Lab 1**).
- **Git** should be installed on your server.

#### **Steps to Install Altoro Mutual**

1. **Clone the Repository**
   
   Clone the Altoro Mutual repository to your server:

   ```bash
   cd /var/www/html
   git clone https://github.com/AppSecDev/AltoroJ.git
   ```

2. **Set Permissions**
   
   Change ownership of the cloned directory to ensure Apache has the correct permissions:

   ```bash
   sudo chown -R www-data:www-data /var/www/html/AltoroJ
   sudo chmod -R 755 /var/www/html/AltoroJ
   ```

3. **Configure Apache**

   Ensure your Apache server is configured to serve the Altoro Mutual application. You can create a new virtual host configuration for this app:

   Open the Apache config file for editing:

   ```bash
   sudo nano /etc/apache2/sites-available/altoro-mutual.conf
   ```

   Add the following configuration:

   ```apache
   <VirtualHost *:80>
       ServerAdmin webmaster@localhost
       DocumentRoot /var/www/html/AltoroJ
       ServerName altoro-mutual.local
       ErrorLog ${APACHE_LOG_DIR}/error.log
       CustomLog ${APACHE_LOG_DIR}/access.log combined
   </VirtualHost>
   ```

   Enable the new site and reload Apache:

   ```bash
   sudo a2ensite altoro-mutual.conf
   sudo systemctl reload apache2
   ```

4. **Configure MySQL Database**
   
   Altoro Mutual requires a MySQL database to store application data.

   - Access MySQL:

     ```bash
     sudo mysql -u root -p
     ```

   - Create the database and user:

     ```sql
     CREATE DATABASE altoro_mutual;
     CREATE USER 'altoro_user'@'localhost' IDENTIFIED BY 'password';
     GRANT ALL PRIVILEGES ON altoro_mutual.* TO 'altoro_user'@'localhost';
     FLUSH PRIVILEGES;
     ```

   - Import the provided database schema from the repository:

     ```bash
     cd /var/www/html/AltoroJ
     mysql -u altoro_user -p altoro_mutual < database/altoro_mutual.sql
     ```

5. **Configure PHP**
   
   Altoro Mutual might require certain PHP configurations to be set up, such as enabling extensions like `mysqli`. Ensure PHP is properly configured:

   ```bash
   sudo apt-get install php-mysqli
   sudo systemctl restart apache2
   ```

6. **Access the Application**
   
   Open a browser and go to your server's IP or `localhost`:

   ```bash
   http://<your-server-ip>/AltoroJ
   ```

   If you set up a virtual host with `altoro-mutual.local`, use that URL:

   ```bash
   http://altoro-mutual.local
   ```

7. **Login and Start Training**

   The default credentials for logging into the **Altoro Mutual** application are:

   - **Username**: `admin`
   - **Password**: `admin`

---

### **Conclusion**

You have successfully set up the **Altoro Mutual** vulnerable application. This web application will be useful for practicing penetration testing and ethical hacking techniques.

Now, you can begin exploring the different vulnerabilities in the Altoro Mutual application, such as SQL Injection, Cross-Site Scripting (XSS), and others. Use this vulnerable app for exercises like vulnerability scanning, penetration testing, and exploiting common web application security flaws.

---
