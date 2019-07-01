## Updating Wordpress

Project that follow these steps
- RPF https://www.righteouspersons.org/

Go to RPF folder run docker-compose up and go into theme folder and run gulp
#### 0# Pull  

#### 1# Back up Local & Production database
Go to wp-config and grab database info and open up Squeal Pro and find database and export and save in a safe place.

#### 2# Go to 101.com and export database go to hosting.
Go to 1&1 phpmyadmin click wordpress database and then export.

#### 3# Back up everything on the FTP
Drag plugins into RFP folder thats dated for this update.
RPF has FTP

#### 4# Check if plugins are supported by the current WP Core and change logs don't raise any conflicts. 
Go into the plugins WP page and click view change logs for each plugin once confirmed no conflicts make update and then make a commit to version from to. I.E. Yoast SEO 9.5 - Yoast SEO 9.7

#### 5# Update each plugins locally
After each plugin update make a commit message.
Example `Advanced Custom Fields PRO - 5.7.9`

#### 6# Update production plugins

#### 7# Leave slack message

##### Example
Updates
Core 5.0.3

Advanced Custom Fields PRO 5.7.10
Ninja Forms 3.4.1
Smush 3.0.2
WP Mail SMTP 1.4.1
WP Offload Media Lite 2.0.1
Yoast SEO 9.4
