# Deploy Umair's Gym Frontend on Apache2 Server (AWS EC2)

## Prerequisites

1. **AWS Account:** Ensure you have an active AWS account.
2. **Frontend Application Content:** You will directly create the HTML file for Umair's Gym using `nano`.
3. **AWS CLI (Optional):** Install the AWS Command Line Interface for convenience.

---

## Step 1: Launch an EC2 Instance

1. **Log in to the AWS Management Console:**
   Navigate to the **EC2 Dashboard**.

2. **Launch an Instance:**
   - Click on **Launch Instance**.
   - **Choose an AMI:** Select an Amazon Machine Image (AMI), such as **Amazon Linux 2** or **Ubuntu Server**.
   - **Instance Type:** Select **t2.micro** (free tier eligible).
   - **Configure Security Group:** Allow the following inbound rules:
     - **HTTP (Port 80):** Open to `0.0.0.0/0`.
     - **SSH (Port 22):** Restrict to your IP or open to `0.0.0.0/0` (not recommended for production).
   - **Key Pair:** Create or select an existing key pair for SSH access.
   - **Launch the Instance.**

---

## Step 2: Connect to Your EC2 Instance

1. **SSH into the Instance:**
   Use the `.pem` key file to connect:
   ```bash
   ssh -i "your-key-file.pem" ec2-user@<INSTANCE_PUBLIC_IP>
   ```

2. **Update the Package Manager:**
   Run the following commands to update the system:
   ```bash
   sudo yum update -y   # For Amazon Linux
   sudo apt update -y   # For Ubuntu
   ```

---

## Step 3: Install Apache Web Server

1. **Install Apache:**
   ```bash
   sudo yum install httpd -y   # For Amazon Linux
   sudo apt install apache2 -y # For Ubuntu
   ```

2. **Start and Enable Apache:**
   ```bash
   sudo systemctl start httpd   # For Amazon Linux
   sudo systemctl enable httpd
   sudo systemctl start apache2 # For Ubuntu
   sudo systemctl enable apache2
   ```

3. **Verify Apache Installation:**
   Access the EC2 instance's public IP in your browser:
   ```
   http://<INSTANCE_PUBLIC_IP>
   ```
   You should see the default Apache welcome page.

---

## Step 4: Create Umair's Gym Frontend

1. **Open the HTML File for Editing:**
   Use `nano` to create or edit the `index.html` file:
   ```bash
   sudo nano /var/www/html/index.html
   ```

2. **Paste the Following HTML Content:**
   ```html
   <!DOCTYPE html>
   <html lang="en">
   <head>
       <meta charset="UTF-8">
       <meta name="viewport" content="width=device-width, initial-scale=1.0">
       <title>Umair's Gym</title>
       <style>
           body {
               font-family: Arial, sans-serif;
               margin: 0;
               padding: 0;
               background-color: #f4f4f4;
               color: #333;
               text-align: center;
           }
           header {
               background: #333;
               color: #fff;
               padding: 20px 0;
           }
           h1 {
               margin: 0;
               font-size: 2.5em;
           }
           section {
               padding: 20px;
           }
           .cta {
               background: #007BFF;
               color: white;
               padding: 15px;
               display: inline-block;
               margin-top: 20px;
               text-decoration: none;
               font-weight: bold;
           }
           .cta:hover {
               background: #0056b3;
           }
       </style>
   </head>
   <body>
       <header>
           <h1>Welcome to Umair's Gym</h1>
       </header>
       <section>
           <p>Your ultimate destination for fitness and health.</p>
           <p>Join us today to start your fitness journey!</p>
           <a href="#" class="cta">Sign Up Now</a>
       </section>
   </body>
   </html>
   ```

3. **Save and Exit:**
   - Press `CTRL + O` to save the file.
   - Press `CTRL + X` to exit.

4. **Set Correct Permissions:**
   Ensure the file has the correct permissions:
   ```bash
   sudo chmod 644 /var/www/html/index.html
   ```

---

## Step 5: Verify Deployment

1. Open your browser and navigate to the public IP of your EC2 instance:
   ```
   http://<INSTANCE_PUBLIC_IP>
   ```

2. You should see the Umair's Gym homepage displayed.

---

## Step 6: Secure and Clean Up

1. **Enhance Security:**
   - Restrict SSH access to specific IPs in the security group.
   - Regularly update and patch the system.

2. **Clean Up Unused Files:**
   Delete unnecessary files from `/var/www/html` to keep the server clean.
