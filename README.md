# WordPress-Deployment-on-AWS
A Step-by-Step Guide to Deploying a WordPress Website on AWS. #AWS_Challenge

Deploying a WordPress website on AWS (Amazon Web Services) is a valuable skill for anyone interested in cloud computing and website management. In this tutorial, I'll guide you through the process of setting up a WordPress site on an AWS EC2 instance, a virtual server in the cloud. We'll take it step by step, making it easy to follow along, even if you're new to these concepts.  
<br>
Architectural Diagram - Deploying a WordPress website on AWS    

![image](https://github.com/user-attachments/assets/f8b35f25-9e94-4c2e-9d31-0506ba341c3d)  

First things first - you'll need an AWS account to dive into this project. If you don't have one yet, don't worry - signing up is easy peasy! And guess what? All the services we'll use here are part of the free tier, so you can play around without spending a dime.  

### Step 1: Launch an EC2 Instance

1. Once you're logged into the AWS console, search for the EC2 service. When you spot it, just click on it to dive right in! You can add EC2 to your favourites by clicking on the star icon next to the service name.
And don't forget to check that you're in the right region.

    ![image](https://github.com/user-attachments/assets/e3388d8e-4b85-45ba-955f-5ca9c1138bd5)

2. Click on 'Instances' to check out the list of your current instances. If it's  looking a bit empty, don't worry - we're about to change that! Hit 'Launch Instances' to start creating your new virtual buddy.

    ![image](https://github.com/user-attachments/assets/efbb1c58-2d01-4c2a-b4d9-2ce3289b3efe)

3. You'll be redirected to a new window where you'll enter your instance details, and AWS will take care of the rest. Let's walk through each step together.
Give your server a name - let your creativity flow! I'm choosing 'WordPressServer' for this project, but pick a name that fits your needs perfectly.

    ![image](https://github.com/user-attachments/assets/44324349-54f8-458e-8994-d56be7c277f0)

4. I'm going with Ubuntu as my operating system.
   
    ![image](https://github.com/user-attachments/assets/bccaeaf6-fad9-4d66-88f6-9b3e75dca558)
  
5. In the Instance Type section, select t2.micro (the default option), which is free-tier eligible. Feel free to choose the instance type that best suits your needs.

    ![image](https://github.com/user-attachments/assets/51cc5d2b-9e8e-4521-a104-d40073da6d3d)

6. In the Key pair section, click on 'Create new key pair.' You'll need this if you want to log in to the server using SSH with this key pair. If you've already created a key pair, just select it from your list. Since I haven't made mine yet, I'll go ahead and do that now.

    ![image](https://github.com/user-attachments/assets/2c8fa5a5-01fa-4fb1-8f09-a8ba037f9b13)

7. A new window will pop up where you'll need to enter your key pair details. I'm naming mine 'wordpress.' For the rest of the options, I'm sticking with the defaults.

    ![image](https://github.com/user-attachments/assets/cab5c968-9d80-4270-9883-bde1704ba610)

8. When you click on 'Create pair,' your private key will be downloaded. Be sure to keep this private key super safe - if anyone else gets their hands on it, they can connect to and log in to your virtual machine.
  
9. The next step is to configure the network settings. Be sure to enable both of these options:

   -- Allow HTTPS traffic from the internet.  
   -- Allow HTTP traffic from the internet.

   ![image](https://github.com/user-attachments/assets/e6623f69-4e87-4aea-b65c-fca10f8758fa)

10. Finally, configure your storage. I'm sticking with the default settings for simplicity, but you can adjust this based on your needs.

    ![image](https://github.com/user-attachments/assets/475abc52-46cc-4a32-9271-49acf5791245)

11. Click on 'Launch Instance,' and voilà - you've just created a virtual computer in the cloud!

    ![image](https://github.com/user-attachments/assets/fee78e4d-211a-4c0c-896f-3f450764a864)

12. Return to your instances page to find your newly created instance listed there.

    ![image](https://github.com/user-attachments/assets/f8c89f6e-f095-4ff0-8cf4-4a437645aea0)

13. Once your instance is created, we're ready to connect to it. But first, we need to assign it an Elastic IP address. This is important because, without it, your instance's public IP address will change every time you reboot. By using an Elastic IP, you ensure a static IP address that stays the same even if you restart your instance.

    ![image](https://github.com/user-attachments/assets/b8fd03df-192c-4422-bc30-bf5a1a7e2cd9)

14. To do this, head over to the EC2 dashboard and click on Elastic IPs.

    ![image](https://github.com/user-attachments/assets/3fd8999f-e56f-4864-8955-1d68c8a8d216)

15. Select 'Allocate Elastic IP address.'

    ![image](https://github.com/user-attachments/assets/00e6026c-feb7-494e-9ac1-27657f75ac74)

16. A new window will open with the Elastic IP address settings. I'm keeping the default settings as is, so just click on 'Allocate.'

    ![image](https://github.com/user-attachments/assets/db048159-0738-4f80-b86b-2f4569bd8ad6)

17. As you can see, we've successfully created an Elastic IP address.

    ![image](https://github.com/user-attachments/assets/24baa626-8539-4d34-bb52-552ac7aaa0f2)

18. The next step is to assign this Elastic IP to your newly created virtual machine. To do this, select the Elastic IP address you've just created. Go to 'Actions' and click on 'Associate Elastic IP address.'

    ![image](https://github.com/user-attachments/assets/308b1916-25a6-4cf3-8d45-490a5bd4e2db)

19. This will open a new window where you need to select the instance you want to associate with this Elastic IP. Select the instance you created from the 'Instance' drop-down menu, and then click 'Associate.'

    ![image](https://github.com/user-attachments/assets/a1decca6-81e6-4056-9c4c-97180ae5c539)

20. Return to 'Instances' to verify that the Elastic IP address is successfully associated with your virtual machine. You'll also notice that the public IPv4 address has changed to the newly created Elastic IP address.

    ![image](https://github.com/user-attachments/assets/48ea0ebc-a128-4fd5-9242-67da20be2790)

21. Now that your instance has the new public IPv4 address, you can connect to it using this address. To do so via SSH, you'll need an SSH client. For this project, I used MobaXterm to connect to my instance.  Open MobaXterm, then click on 'SSH.' In the remote host session, enter the public IPv4 address. Specify the username, select 'Use private key,' and browse to the private key file you downloaded.

    ![image](https://github.com/user-attachments/assets/fd74194f-f213-49b1-93af-47625b42cd23)

22. You can also connect via a browser. Ensure you enter the correct IP address and username if you are using SSH. As I didn't specify a custom username, the default username 'ubuntu' will be used.  Once connected to the server, we can proceed with the next steps.   Install the Apache web server on your instance.  Run the following command to install it.

    ```sudo apt install apache2```

    ![image](https://github.com/user-attachments/assets/3fbf5ab5-0123-4b94-80a5-2519b80b8b6b)

23. To verify that the web server is installed correctly, open your browser and enter http://<public IPv4> into the address bar, then press Enter.  If you see a page like the one below, it means the web server is working.

    ![image](https://github.com/user-attachments/assets/1d703f41-ee77-485b-bc11-58bbf515b49e)

### Step 2: Install PHP and MySQL

1. Next, we'll install the PHP runtime on the instance, as WordPress is built with PHP. We can proceed by installing the PHP runtime and the MySQL connector for PHP using the following command.

   ```sudo apt install php libapache2-mod-php php-mysql```

   ![image](https://github.com/user-attachments/assets/adb96636-6a8b-44bb-aa8d-524f7b9a2b4e)

2. Next, we need to install the MySQL server to manage the database. To do this, execute the following command:

   ```sudo apt install mysql-server```

   ![image](https://github.com/user-attachments/assets/c724ed14-d5bf-4ee8-bd76-d12e8a134d7c)

3. Before proceeding to the next step, there is a small configuration required for your MySQL server. You need to change the MySQL authentication plugin to mysql_native_password so you can log in to the MySQL server with a standard password.  To change the authentication plugin, first log in to the MySQL prompt as the root user. Use the following command to do so:

   ```sudo mysql -u root```

   ![image](https://github.com/user-attachments/assets/a3b74d0b-1dfe-4193-a87d-fb913fc3b4f2)

4. To change the authentication plugin type, use the following command:

   ```ALTER USER 'root'@localhost IDENTIFIED WITH mysql_native_password BY '<the password that you want to use for your root account>';```

   ![image](https://github.com/user-attachments/assets/3b1df894-0ab8-4797-8198-3644a9987478)

5. Create a new user, other than root, to use with WordPress. Execute the below command for that:

   ```CREATE USER 'wp_user'@localhost IDENTIFIED BY '<Your_Password>';```

   ![image](https://github.com/user-attachments/assets/4307d66e-f2ed-47e8-8eda-2f76c12a2399)

6. Now, create a separate database for WordPress. Execute the following command:

   ```CREATE DATABASE <DB_name>;```

   ![image](https://github.com/user-attachments/assets/324ee5e3-bccd-49f0-81ec-6bc063130e00)

7. Next, grant all privileges on the newly created database to the new WordPress user. Execute the following command:

   ```GRANT ALL PRIVILEGES ON <db_name>.* TO '<user_name>'@localhost;```

   ![image](https://github.com/user-attachments/assets/1a2e2138-99c4-4b13-83d3-54cb9d88c005)

### Step 3: Install WordPress on your server  

1. Next, we'll install WordPress on your server. To get started, navigate to your tmp directory.

   ```cd tmp```

2. We need to download the latest version of WordPress to install it on our server. You can either search for 'wordpress.org' in your web browser and download the .zip file manually, or, for a quicker option, you can use the following command on your server to download it directly:

   ```wget https://wordpress.org/latest.zip```

   ![image](https://github.com/user-attachments/assets/d719b7c3-ee2f-4d7a-98b7-dea601ab7e2a)

3. Unzip the downloaded file, and you'll see a new folder named 'wordpress' has been created.

   ![image](https://github.com/user-attachments/assets/e9a2e0d0-c0b7-4b64-a064-27b2daa67ab8)

4. Let's move the 'wordpress' folder to the /var/www/html directory. If you are facing any permission error then use sudo before the mv command.

   ```mv wordpress/ /var/www/html```

5. Once the wordpress folder is successfully moved, you can verify it by navigating to the /var/www/html directory. You should see the wordpress folder there.
You can use the following command to check:

```ls /var/www/html```

![image](https://github.com/user-attachments/assets/a653f7f2-03f7-4271-8e0a-eceec8eb474b)

6. Now, open your web browser and enter the following URL:

   ```http://<your-public-ipv4-address>/wordpress```

   Replace <your-public-ipv4-address> with the actual public IPv4 address of your EC2 instance.

7. You should see the WordPress setup page. If everything is set up correctly, this means that WordPress is installed and ready for configuration.

   ![image](https://github.com/user-attachments/assets/6c59266e-df23-44d5-ac91-e355be795ac0)

8. Click on the "Let's go" button to start the WordPress setup process.
   - Database Name: Enter the name of the database you created for WordPress.
  - Username: Input the username for the database user you set up.
- Password: Enter the password for the database user.

Once you've filled in these details, click on the "Submit" button to proceed.  

![image](https://github.com/user-attachments/assets/24efeda2-2183-4a5f-b399-13f331a461dd)

9. After clicking Submit, you'll see a new window prompting you to Run the Installation. This means WordPress has successfully connected to your database - great job, we're almost there!
    Click on 'Run the installation'.

   ![image](https://github.com/user-attachments/assets/58a7a0ec-fe5e-4e2d-9dab-83a6c294da68)

10. After you click on Run the Installation, follow the on-screen instructions to set up your site's title and create an admin username and password.

    ![image](https://github.com/user-attachments/assets/aa8cdfbc-e692-4248-a3ce-7dc0ac0ff831)

11. Once you complete these steps, WordPress will be installed, and you can log in to your new site using the credentials you just created.

    ![image](https://github.com/user-attachments/assets/e7aa3ed9-c782-4269-9433-6c10aa18d58e)

    ![image](https://github.com/user-attachments/assets/86f60f84-452f-4267-83a4-eddcbaf70c0e)  

### Step 4: Modifying Apache Configuration

You might notice that WordPress is accessible by adding /wordpress at the end of the IP address. To access it directly with just the IP address, you need to modify the Apache configuration.  

1. Navigate to the directory by running cd /etc/apache2/sites-available/. In this directory, you'll find a file named `000-default.conf`.

   ![image](https://github.com/user-attachments/assets/e855396e-b5fe-42b3-b243-756854e2ac1b)

2. We need to edit this file. Open it and locate the DocumentRoot section. Then, add `wordpress` at the end.

   ![image](https://github.com/user-attachments/assets/55f21f0e-df7d-45d7-a3e6-88b0410d10ec)

3. Save the file and restart apache2.

   ```sudo systemctl restart apache2```

You should now be able to access your WordPress site directly by typing the IP address into your browser, without needing to include /wordpress in the URL. The changes made to the Apache configuration should ensure that your WordPress site is served correctly from the root of the IP address.   

![image](https://github.com/user-attachments/assets/1d797e1f-976e-4651-8e58-3e4670723b61)

<br>

Congratulations! 🎉 You've successfully deployed a WordPress website on AWS. Well done! Got questions, comments, or want to share your experience? Feel free to drop a comment below! If this guide helped make your day easier, follow for more cloud adventures and tech tips!

