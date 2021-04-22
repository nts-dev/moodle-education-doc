# moodle-education-doc

## **1. Windows Installation**

Make sure you have a webserver running.

Requirement for webserver

    - Apache2
    - Php 7.4
    - Mysql 5.7 or higher
The most naive way you can have this setup is by downloading and installing Xampp from https://www.apachefriends.org/download.html . Make sure the version you are downloading is of php 7.4

**1.1 Download moodle**

Download stable moodle `standalone code` from here
`https://download.moodle.org/releases/latest/`

    Note

    Do not download moodle-xampp prepackaged. We are only interested with the code base

**1.2 Extract moodle zip to webserver directory**

Once download is complete unpack the zip file with rar program inside your webserver directory:
If you have an apache setup the directory is named `htdocs`

For example `C:\apache2\htdocs`

    Complete path after unpacking moodle

    C:\apache2\htdocs\moodle

If you are using xampp, the directory will be as follows,`C:\xampp\htdocs`

    Complete path after unpacking moodle

    C:\xampp\htdocs\moodle


**1.3 Start your Installation**

Head to your browser and type the url as below to begin installation

    http://localhost/moodle  or 
    http://127.0.0.1/moodle or 
    http://[your_id_address]/moodle

    If you have a domain name, use it instead 
    http://[domain_name]/moodle

Fill in the required steps to complete the installation


## **2. Ubuntu Installation**
   
**2.1 Setup your local repository and download Moodle** 

We will use /opt for this installation.

   Git is what is called a "version control system". By using git it will much easier down the road to update the moodle core application. Within Step 5 there is a little more detail on why we put the moodle core application code in the /opt directory.

`cd /opt`

Download the Moodle Code and Index

`sudo git clone git://git.moodle.org/moodle.git`

Change directory into the downloaded Moodle folder

`cd moodle`

Retrieve a list of each branch available

`sudo git branch -a`

Tell git which branch to track or use

`sudo git branch --track MOODLE_39_STABLE origin/MOODLE_39_STABLE`

Finally, Check out the Moodle version specified

`sudo git checkout MOODLE_39_STABLE`

**2.2  Copy local repository to /var/www/html/**

`sudo cp -R /opt/moodle /var/www/html/`


`sudo mkdir /var/moodledata`

`sudo chown -R www-data /var/moodledata`

Give read write permissions

`sudo chmod -R 777 /var/moodledata`

`sudo chmod -R 0755 /var/www/html/moodle`

## **3. Updating moodle after Changes in Domain/IP Addresses**
**Motive**

Moodle caches its resources with full URL presented at the time of installation. 
Due to this, when your address is changed moodle will keep on redirecting to the previous address and pages won't load anymore.
To make it work, you will do the following

 
    Change $CFG->wwwroot in your config.php to the new URL. 

    Example
    
    Current
    $CFG->wwwroot = 'http://localhost/moodle'

    Updated
    $CFG->wwwroot = 'http://[new_domain/IP]/moodle'
    
    This file is located at the root of moodle dir

Inorder to make your resources (css/js/images/videos etc) work correctly. You need to 
run the search/replace tool.

    Login in as an admin, tack /admin/tool/replace/index.php onto the root url to replace the old URL with the new URL.

    Steps
    1.    Go to http://[new_domain/IP]/moodle/admin/tool/replace/index.php
    2.    Fill in the "search whole database for" box with the old URL
    3.    Fill in the "replace with this string" box with the new URL
    4.    Check the box for "shorten result if necessary". It appears to be required, at least the last time I used the tool.
    5.    Check the box for "I understand the risks of this operation".
    6.    Click the "Yes do it!" button.

Reload to check if work correctly

