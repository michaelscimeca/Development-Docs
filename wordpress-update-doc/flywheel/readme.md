Fenway

## Updating Wordpress with Flywheel

#### 1# Back up local database
Go to wp-config and grab database info and open up Squeal Pro and find database and export and save in a safe place.

#### 2# Check if plugins are supported by the current WP Core and change logs don't raise any conflicts
Go into the plugins WP page and click view change logs for each plugin.

#### 3# Update each plugins locally
After each plugin update make a commit message.
Example `Advanced Custom Fields PRO - 5.7.9`

#### 4# Backup Wordpress on [Flywheel](https://app.getflywheel.com/)
Login to Flywheel and Backup before you update plugins or/and WP core on production

#### 5# Leave slack message
##### Example
Updates
Core 5.0.3

Advanced Custom Fields PRO 5.7.10
Ninja Forms 3.4.1
Smush 3.0.2
WP Mail SMTP 1.4.1
WP Offload Media Lite 2.0.1
Yoast SEO 9.4
