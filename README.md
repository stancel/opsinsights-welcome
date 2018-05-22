# Mautic Theme - Ops Insights Welcome Email

Mautic Themes are used for email templates, landing pages and pop ups to collect data to be inputted into the Mautic Marketing Automation software. 

#### Mautic Theme Development Info

`https://github.com/mautic/developer-documentation/blob/master/source/includes/_themes.md#theme-thumbnail`

#### Creating an Installable Theme File

If you want to make your theme installable via the Theme Manager, make a zip package from it. The zip package name must be the same as the final folder name of the theme in the /themes folder. The contents of the zip folder must contain the theme files directly, not in a subfolder


	- Re-zip directory into zip file (with no hidden Mac files) so that it can be distributed
		- `cd /into/folder/where/published/zip/files/were/unzipped`
		- `zip -r NameOfModuleZipFile.zip . -x \*.DS_Store -x "__MACOSX"``
		- Login to Mautic, click gear in top right hand corner (Settings) then go to the Themes option
		- Upload the zip file and click install
		- Navigate to the email or landing page template you just uploaded
		
#### Troubleshooting / Theme File Not Showing Up?

Mautic can be very finnicky about not showing updates. It uses a cache that seems needs to be cleared after every small change. Here are the steps that will resolve the issue.

	- SSH into your Mautic server
	- Clear the Mautic Cache (where /var/www/html is the path to your Mautic folder)
		- `php /var/www/html/app/console cache:clear`
	- If above fails then:
		- `rm -rf /var/www/html/app/cache/run/*`
		- `rm -rf /var/www/html/app/cache/prod/*`
	- Reset the permissions to the web server user (www-data in this case)
		- `chown -R www-data:www-data /var/www/html`
	- Make sure the web server user has the permissions to access the needed files
		- `chmod -R 755 /var/www/html/app/cache`
	- Restart the webserver (Apache via systemd restart in this case)
		- `systemctl restart apache2.service`
		
