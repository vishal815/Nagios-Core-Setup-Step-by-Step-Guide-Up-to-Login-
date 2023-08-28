# Nagios-Core-Setup-Step-by-Step-Guide-Up-to-Login-
Comprehensive guide for setting up Nagios Core on AWS EC2. Follow steps, scripts, and configs to deploy Nagios Core and plugins. Monitoring made easy.

![download](https://github.com/vishal815/Nagios-Core-Setup-Step-by-Step-Guide-Up-to-Login-/assets/83393190/47759b16-b655-4c5b-8e30-da55cab9c601)
---

# Setting Up Nagios Core on AWS EC2 Instance

This guide will walk you through the process of setting up Nagios Core on an AWS EC2 instance. Nagios Core is a powerful monitoring system that allows you to monitor the status of various services and hosts. Follow the steps below to get Nagios Core up and running.

## Step 1: Create AWS EC2 Security Group

1. Open AWS EC2 Dashboard.
2. Navigate to Security Groups and create a new security group.
3. Save the security group rules.
4. While creating a new EC2 instance, select the existing security group.
5. (Or you alredy created security group just edit it like that)
   ![image](https://github.com/vishal815/Nagios-Core-Setup-Step-by-Step-Guide-Up-to-Login-/assets/83393190/8eb8b806-a4d9-4fee-8a91-9037921f57de)








## Step 2: Install and Configure Nagios Core

1. Update system packages:

   ```sh
   sudo apt update
   ```

2. Install required packages:

   ```sh
   sudo apt install wget unzip curl openssl build-essential libgd-dev libssl-dev libapache2-mod-php php-gd php apache2 -y
   ```

3. Download Nagios Core:

   ```sh
   wget https://assets.nagios.com/downloads/nagioscore/releases/nagios-4.4.6.tar.gz
   ```

4. Extract downloaded files:

   ```sh
   sudo tar -zxvf nagios-4.4.6.tar.gz
   ```

5. Navigate to the setup directory:

   ```sh
   cd nagios-4.4.6
   ```

6. Run Nagios Core configure script:

   ```sh
   sudo ./configure
   ```

7. Compile main program and CGIs:

   ```sh
   sudo make all
   ```

8. Make and install group and user:

   ```sh
   sudo make install-groups-users
   ```

9. Add `www-data` user to the `nagios` group:

   ```sh
   sudo usermod -a -G nagios www-data
   ```

10. Install Nagios:

    ```sh
    sudo make install
    ```

11. Initialize installation configuration scripts:

    ```sh
    sudo make install-init
    ```

12. Install and configure permissions on the configs' directory:

    ```sh
    sudo make install-commandmode
    ```

13. Install sample config files:

    ```sh
    sudo make install-config
    ```

14. Install Apache files:

    ```sh
    sudo make install-webconf
    ```

15. Enable Apache rewrite mode:

    ```sh
    sudo a2enmod rewrite
    ```

16. Enable CGI config:

    ```sh
    sudo a2enmod cgi
    ```

17. Restart the Apache service:

    ```sh
    sudo systemctl restart apache2
    ```

18. Create a user and set the password when prompted:

    ```sh
    sudo htpasswd -c /usr/local/nagios/etc/htpasswd.users admin
    ```

## Step 3: Install Nagios Plugins

1. Download Nagios Core plugin:

   ```sh
   cd ~/
   wget https://nagios-plugins.org/download/nagios-plugins-2.3.3.tar.gz
   ```

2. Extract the downloaded plugin:

   ```sh
   sudo tar -zxvf nagios-plugins-2.3.3.tar.gz
   ```

3. Navigate to the plugins' directory:

   ```sh
   cd nagios-plugins-2.3.3/
   ```

4. Run the plugin configure script:

   ```sh
   sudo ./configure --with-nagios-user=nagios --with-nagios-group=nagios
   ```

5. Compile Nagios Core plugins:

   ```sh
   sudo make
   ```

6. Install the plugins:

   ```sh
   sudo make install
   ```

## Step 4: Verify Nagios Configuration

1. Verify the Nagios Core configuration:

   ```sh
   sudo /usr/local/nagios/bin/nagios -v /usr/local/nagios/etc/nagios.cfg
   ```

2. Start the Nagios service:

   ```sh
   sudo systemctl start nagios
   ```

3. Enable Nagios service to run at system startup:

   ```sh
   sudo systemctl enable nagios
   ```

## Step 5: Access Nagios Web Interface

Open your web browser and access the Nagios web interface using the URL http://ServerIP/nagios (replace `ServerIP` with your server's public IP). For example: http://yourpublicip/nagios
![image](https://github.com/vishal815/Nagios-Core-Setup-Step-by-Step-Guide-Up-to-Login-/assets/83393190/ddb70943-df0c-4956-81c9-49ee64f57c91)
http://ServerIP/nagios
![image](https://github.com/vishal815/Nagios-Core-Setup-Step-by-Step-Guide-Up-to-Login-/assets/83393190/bbfb9587-5921-4dc9-b561-fd31910e612a)
![image](https://github.com/vishal815/Nagios-Core-Setup-Step-by-Step-Guide-Up-to-Login-/assets/83393190/7f9151ef-959a-4333-b955-9db51dc184c9)
![image](https://github.com/vishal815/Nagios-Core-Setup-Step-by-Step-Guide-Up-to-Login-/assets/83393190/cf5f5d6c-3786-4537-a0e2-0eef899b489e)


You have successfully set up Nagios Core on an AWS EC2 instance using these commands.

---




## In case you are fessing login error 


```sh
sudo htpasswd -c /usr/local/nagios/etc/htpasswd.users admin
```

👉👉If you do not remember your password, you can reset it by running the command above. When you run this command, type your password and press enter (the password you type will not be displayed on the screen). You will then be prompted to retype the password to confirm it.



Once you've reset or confirmed your password, follow these steps:

1. Go to the Nagios web interface at: http://ServerIP/nagios (replace `ServerIP` with your server's public IP).

2. The login page will appear. Enter your username (`admin`) and the password you just reset or set. If you changed the default username, use that username and the corresponding password.

3. After successful login, you will have access to the Nagios web interface and its monitoring capabilities.

Your Nagios Core setup is now complete and ready to use.

## Happy Learning 😃...

---
