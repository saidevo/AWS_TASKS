Step 1: Create an EC2 Instance with User Data

1. **Log in to the AWS Management Console** and navigate to the **EC2** dashboard.

2. **Launch an Instance:**
   - Click on "Launch Instance."
   - Choose an Amazon Machine Image (AMI), such as **Amazon Linux 2**.
   - Select an instance type (e.g., `t2.micro` for the free tier).
   - In the "Configure Instance" step, look for the **User Data** section.
    ![preview](1.png)
3. **Add User Data Script:**
   In the User Data field, enter the following script:

   ```bash
   #!/bin/bash
   yum update -y
   yum install -y httpd
   systemctl start httpd
   systemctl enable httpd
    
![preview](2.png)
 
   # Create a simple HTML page that displays the current time
   echo "<html><body><h1>Current Time</h1><p>The current time is: $(date)</p></body></html>" > /var/www/html/index.html
   ```

4. **Configure Security Group:**
   - Allow inbound traffic on port `80` (HTTP) and `22` (SSH).
   
![preview](3.png)

5. **Review and Launch:**
   - Review your configurations and click "Launch."
   - Choose or create a key pair for SSH access.

Step 2: Access Your Application

1. **Get the Public IP Address:**
   - Once the instance is running, note the public IP address from the EC2 dashboard.

2. **Open a Web Browser:**
   - Navigate to `http://your-instance-public-ip`.
   - You should see a webpage displaying the current time.

![preview](4.png)

Step 3: Verify the User Data Execution

1. **SSH into Your Instance:**
   ```bash
   ssh -i your-key.pem ec2-user@your-instance-public-ip
   ```

2. **Check the Web Server Status:**
   ```bash
   sudo systemctl status httpd
   ```
![preview](5.png)
3. **Verify the HTML File:**
   ```bash
   cat /var/www/html/index.html
   ```
![preview](6.png)
Conclusion

You've successfully created a simple web application that utilizes AWS User Data to automatically 
install and configure a web server on EC2 launch. The webpage displays the current time, 
demonstrating how User Data can be used to run scripts at startup for real-time applications.