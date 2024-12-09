# Lab: Putting It All Together – Creating a Beautiful Home Page for Easy Access

**Objective:**
In this lab, you will create a stylish HTML and CSS-based homepage that will display links to all 10 vulnerable applications installed on your VM. The page will be accessible by others on the network via the VM’s IP address, providing a simple and organized way to access any of the installed applications.

---

### **Steps to Create the Beautiful Homepage:**

---

### **1. Set Up Your VM for Access**

Before you start building the homepage, ensure that your VM's network settings are configured to allow access from other machines.

1. **Find your VM’s IP address**:
   - Run `ip a` or `ifconfig` in your terminal to find the IP address of the VM.

2. **Enable Apache Web Server**:
   Ensure the Apache web server is running so that others can access your page.
   ```bash
   sudo systemctl start apache2
   sudo systemctl enable apache2
   ```

---

### **2. Create the HTML File for the Homepage**

1. **Navigate to the Apache directory** where your HTML files will be served:
   ```bash
   cd /var/www/html
   ```

2. **Create an index.html file**:
   ```bash
   sudo nano index.html
   ```

3. **Add the following code** to the `index.html` file to create a clean and organized homepage.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Vulnerable Web Apps - CTF Access Page</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>

    <header>
        <h1>Welcome to the CTF Lab Environment</h1>
        <p>Click on any of the links below to access the vulnerable web applications.</p>
    </header>

    <main>
        <div class="container">
            <div class="app-card">
                <h2>Lab 1: DVWA</h2>
                <p>A PHP/MySQL-based web app designed to be vulnerable for testing</p>
                <a href="http://<your_vm_ip>/DVWA" target="_blank" class="btn">Go to DVWA</a>
            </div>
            <div class="app-card">
                <h2>Lab 2: OWASP Mutillidae II</h2>
                <p>A web application for practicing OWASP Top 10 vulnerabilities</p>
                <a href="http://<your_vm_ip>/Mutillidae" target="_blank" class="btn">Go to Mutillidae</a>
            </div>
            <div class="app-card">
                <h2>Lab 3: bWAPP</h2>
                <p>A web app that includes over 100 vulnerabilities for practice</p>
                <a href="http://<your_vm_ip>/bWAPP" target="_blank" class="btn">Go to bWAPP</a>
            </div>
            <div class="app-card">
                <h2>Lab 4: WebGoat</h2>
                <p>An OWASP-supported platform for teaching web security</p>
                <a href="http://<your_vm_ip>/WebGoat" target="_blank" class="btn">Go to WebGoat</a>
            </div>
            <div class="app-card">
                <h2>Lab 5: Hackazon</h2>
                <p>A vulnerable e-commerce site for penetration testing</p>
                <a href="http://<your_vm_ip>/Hackazon" target="_blank" class="btn">Go to Hackazon</a>
            </div>
            <div class="app-card">
                <h2>Lab 6: Juice Shop</h2>
                <p>A modern web application for testing web security knowledge</p>
                <a href="http://<your_vm_ip>/JuiceShop" target="_blank" class="btn">Go to Juice Shop</a>
            </div>
            <div class="app-card">
                <h2>Lab 7: NodeGoat</h2>
                <p>A Node.js-based vulnerable app to learn security concepts</p>
                <a href="http://<your_vm_ip>/NodeGoat" target="_blank" class="btn">Go to NodeGoat</a>
            </div>
            <div class="app-card">
                <h2>Lab 8: WackoPicko</h2>
                <p>A vulnerable website for simulating common web exploits</p>
                <a href="http://<your_vm_ip>/WackoPicko" target="_blank" class="btn">Go to WackoPicko</a>
            </div>
            <div class="app-card">
                <h2>Lab 9: WordPress Vulnerable Setup</h2>
                <p>A deliberately insecure WordPress site with outdated plugins</p>
                <a href="http://<your_vm_ip>/WordPress" target="_blank" class="btn">Go to WordPress</a>
            </div>
            <div class="app-card">
                <h2>Lab 10: Altoro Mutual</h2>
                <p>A vulnerable banking web application for pen testing practice</p>
                <a href="http://<your_vm_ip>/AltoroMutual" target="_blank" class="btn">Go to Altoro Mutual</a>
            </div>
        </div>
    </main>

    <footer>
        <p>All Rights Reserved © 2024 - CTF Lab Environment</p>
    </footer>

</body>
</html>
```

**Explanation:**
- Replace `<your_vm_ip>` with the actual IP address of your VM (e.g., `http://192.168.1.100`).
- Each "Go to" button links to a specific lab application that you have installed in the VM.

---

### **3. Create the CSS File**

To style the homepage, we’ll create a separate CSS file.

1. **Navigate to the same directory** where the `index.html` is located:
   ```bash
   cd /var/www/html
   ```

2. **Create a `styles.css` file**:
   ```bash
   sudo nano styles.css
   ```

3. **Add the following CSS code** to style the page:

```css
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: Arial, sans-serif;
}

body {
    background-color: #f4f4f9;
    color: #333;
}

header {
    text-align: center;
    padding: 30px 0;
    background-color: #4CAF50;
    color: white;
}

h1 {
    font-size: 2.5em;
}

p {
    font-size: 1.2em;
}

.container {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
    gap: 20px;
    padding: 20px;
}

.app-card {
    background-color: white;
    padding: 20px;
    border: 1px solid #ddd;
    border-radius: 10px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    text-align: center;
    transition: transform 0.3s;
}

.app-card:hover {
    transform: scale(1.05);
}

h2 {
    font-size: 1.8em;
    margin-bottom: 10px;
}

p {
    font-size: 1em;
    margin-bottom: 20px;
}

.btn {
    display: inline-block;
    background-color: #4CAF50;
    color: white;
    padding: 10px 20px;
    text-decoration: none;
    border-radius: 5px;
    font-weight: bold;
    transition: background-color 0.3s;
}

.btn:hover {
    background-color: #45a049;
}

footer {
    text-align: center;
    padding: 20px;
    background-color: #4CAF50;
    color: white;
    position: fixed;
    bottom: 0;
    width: 100%;
}
```

**Explanation:**
- This CSS will create a responsive layout with card-style boxes for each application.
- Buttons will have a green color and will change when hovered over.
- The page will be mobile-friendly, adjusting to smaller screens by displaying the cards in a grid format.

---

### **4. Access the Page**

- Once you have created the `index.html` and `styles.css` files, open a browser on any machine within the network.
- Type in the IP address of your VM to access the homepage:
  - Example: `http://192.168.1.100`
- You should now see a beautiful homepage with links to all the vulnerable web applications you’ve set up.

---

### **5. Share the Link**

- Share the IP address with other users (penetration testers or students) so they can access the page.
- They can click on any of the links to open the corresponding application in a new tab.

---

### Conclusion

You’ve now successfully created a homepage that provides an easy, organized access point to all the vulnerable web applications installed on your VM. This will allow penetration testers or students to quickly access any of

 the labs and start testing them.