# Linux Lab

## Find and Initialise your new storage device

Use the `lsblk` command to view the block devices and find your new storage device.

```sudo lsblk```

Let's assume your new storage device is /dev/sdb. Initialise the disk with fdisk.

```sudo fdisk /dev/sdb```

Inside the fdisk utility:

Press `n` to create a new partition.

Press `p` for primary.

Press `1` for the first partition.

Press Enter to accept the default values for the first sector.

If you plan to have more partitions, follow the instructions on the screen (e.g., type +10G for the last sector if you want to allocate 10GB to the partition). Otherwise, just press Enter.

Press `w` to write the partition table and exit.

## Mount your new storage device to /var/www/html/wordpress/
Create the mount point.

`sudo mkdir -p /var/www/html/wordpress/`

Mount the partition to this directory.

`sudo mount /dev/sdb1 /var/www/html/wordpress/`

## Deploy WordPress to the /var/www/html/wordpress/ directory and install it
We are using the LAMP stack software bundle.

LAMP stands for Linux, Apache, MySQL, and PHP. Together, they provide a powerful web server environment.

Here are the general steps to install a full LAMP stack and deploy WordPress on CentOS Stream 9.

MySQL has already been deployed. You can see it with systemctl status mysqld. Database name, username and password has been set to wordpress.

Please note that this is a general guide, and depending on your specific setup and needs, you might need to adjust these steps.

<b>1. Update your system: </b> Keep your system up-to-date. 

`sudo dnf update -y`

<b>2. Install Apache: </b> Apache is a web server software.

`sudo dnf install httpd -y`

After installation, you need to start and enable Apache to make sure it starts automatically at system boot.

```
sudo systemctl start httpd
sudo systemctl enable httpd
```
<b> 3.Install PHP: </b> PHP is a popular scripting language that is especially suited to web development.

`sudo dnf install php php-mysqlnd -y`

After the installation, restart Apache to make sure it recognizes and uses PHP.

`sudo systemctl restart httpd`

<b> 4.Download and Install WordPress: </b>

First, navigate to the Apache document root.

`cd /var/www/html/`

Download wget is required:

`sudo dnf install wget`

Download WordPress.

`sudo wget http://wordpress.org/latest.tar.gz`

Extract the downloaded file.

`sudo tar xzvf latest.tar.gz`

Remove compressed file.

`sudo rm latest.tar.gz`

Now, you should have a WordPress directory in /var/www/html/.

<b>5.Configure WordPress:</b>

Move to the WordPress directory.

`cd /var/www/html/wordpress/`

Copy the sample WordPress config file to create your own config file.

`sudo cp wp-config-sample.php wp-config.php`

Open the WordPress config file and replace the 'database_name_here', 'username_here', and 'password_here' placeholders with your database details.

`sudo vi wp-config.php`

