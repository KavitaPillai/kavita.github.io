# Installing ownCloud Enterprise Edition 

You have the flexibility to install the ownCloud Enterprise Edition using the Linux package manager or by manually performing the installation. If you opt the package manager, then an installation wizard would guide you through the installation. The configuration procedure involves associating the manager with ownCloud Enterprise repository, importing the signing key, and installing and updating the ownCloud packages. For in-depth information on setting up the package manager, review the *README- ownCloud Package Installation.txt* document, which can be accessed from your owncloud.com account.

High-level workflow of the installation procedure:

 ![](/images/Step1_install.png)
 ![](/images/Step2_install.png) 
 ![](/images/Step3_install.png) 
 ![](/images/Step4_install.png) 
 ![](/images/Step5_install.png)

## Downloading the ownCloud installer

**To bootstrap a production deployment of ownCloud on Enterprise Edition on Linux:**

1. Download the ownCloud installer (tar.bz2 or .zip archive) from the https://owncloud.org/download/. 
2. Download the corresponding checksum file, e.g. owncloud-x.y.z.tar.bz2.md5, or owncloud-x.y.z.tar.bz2.sha256.
3. Verify that the MD5 or SHA256 functions using the following command:

    ``` 
    md5sum -c owncloud-x.y.z.tar.bz2.md5 < owncloud-x.y.z.tar.bz2
    sha256sum -c owncloud-x.y.z.tar.bz2.sha256 < owncloud-x.y.z.tar.bz2
    md5sum  -c owncloud-x.y.z.zip.md5 < owncloud-x.y.z.zip
    sha256sum  -c owncloud-x.y.z.zip.sha256 < owncloud-x.y.z.zip
    ```
4. Verify that the Pretty Good Privacy (PGP) signature is configured. To verify, run the following command:

    ```
    wget https://download.owncloud.org/community/owncloud-x.y.z.tar.bz2.asc
    wget https://owncloud.org/owncloud.asc
    gpg --import owncloud.asc
    gpg --verify owncloud-x.y.z.tar.bz2.asc owncloud-x.y.z.tar.bz2
    ```
5. Uncompress the tar.bz2 or .zip file that you have downloaded using the following command:
    
    ``` 
    tar -xjf owncloud-x.y.z.tar.bz2
    unzip owncloud-x.y.z.zip
    ```
A single directory with the **ownCloud** name is created on your machine. 

6. Copy the **ownCloud** directory to the document root location from where you plan to install the Apache HTTP. Run the following command to copy the directory:

    ``` 
    cp -r owncloud */path/to/webserver/document-root*
    ```

**Note**: Specify the path of the document root of your Web server. If using the HTTP servers, install ownCloud at a location that is not document root.

## Configuring the Apache Web server

On the Debian and Ubuntu-based distributions, Apache Web server is installed with certain default configurations. For ownCloud installation, you must create an ownCloud-specific configuration file and replace the default directory paths with relevant paths.

**To create an ownCloud configuration file:**

1. Create a owncloud.conf file in /etc/apache2/sites-available/. The file must contain the following contents:

    ``` 
    Alias /owncloud */var/www/owncloud/*

    <Directory */var/www/owncloud/*>
    Options +FollowSymlinks
    AllowOverride All

    <IfModule mod_dav.c>
    Dav off
    </IfModule>

    SetEnv HOME */var/www/owncloud*
    SetEnv HTTP_HOME */var/www/owncloud*

    </Directory> 
    ```

    **Note**: You must use the directory path specific to your environment.

2. Create a symbolic link to /etc/apache2/sites-enabled.

    ```
    ln -s /etc/apache2/sites-available/owncloud.conf /etc/apache2/sites-enabled/owncloud.conf
    ```

**Additional configurations on Apache Web server**

ownCloud requires some additional configurations on Apache Web server for an error-free installation.

1. Enable the mod_rewrite, mod_headers, mod_env, mod_dir, and mod_mime modules. Run the following command:

    ``` 
    a2enmod rewrite
    a2enmod headers
    a2enmod env
    a2enmod dir
    a2enmod mime
    ```

    **Note**: The mod_headers modules is required when you intend to use the OAuth2 app.

2. Disable the server-configured authentication for ownCloud since it uses the basic authentication internally for the DAV services. If you have enabled authentication on a parent folder (via, e.g., an AuthType Basic directive), then disable the authentication for the ownCloud entry. 

3. In the configuration file, add the following in the <*Directory*> section.
    ``` 
    Satisfy Any
    ```
4. If using SSL, make sure to specify the **ServerName** in the server configuration file. Also, in the **CommonName** field of the certificate. If you want to access the ownCloud via the Internet, then set both, **ServerName** and **CommonName** field to the domain that you want to access through the ownCloud server.

5. Restart the Apache Web server using the following command:
    ``` 
    service apache2 restart
    ```
If you are running ownCloud in a sub-directory, and want to use CalDAV or CardDAV clients, then ensure to configure the correct Service discovery URLs.

**Multi-Processing Module (MPM)**

Use Apache prefork. Do not use a threaded MPM like event or worker with mod_php because PHP is currently not thread safe.

**Secure Sockets Layer (SSL)**

You can use ownCloud over plain HTTP. However, it is strongly recommended to  use SSL/TLS certificates to authenticate the identity, to encrypt in-flight data, and protect the user’s logins.

The Apache Web server installed under Ubuntu has a default self-signed certificate. Note that self-signed certificates have their limitations when the ownCloud server is publicly accessible. It is recommended to consider getting a certificate signed by a commercial signing authority. Consult your domain name registrar or hosting service for the commercial certificates offering.

Activate the certificate and enable the SSL module. For instructions, see [SSL](https://doc.owncloud.org/server/10.0/admin_manual/installation/source_installation.html#enable-ssl).

## Running the installation wizard

After restarting the Apache server, run the installation wizard to complete the installation. You can run the wizard using the GUI or the command line from the ownCloud console. 

To run the wizard through GUI, see the [GUI installation](https://doc.owncloud.org/server/10.0/admin_manual/installation/installation_wizard.html)
And, for the ownCloud console, see the [Command line installation ](https://doc.owncloud.org/server/10.0/admin_manual/installation/command_line_installation.html)

## Performing the post-installation steps

Once the ownCloud installation is complete, ensure that you perform the following steps to secure your ownCloud server from serious risks caused by unauthorized access.
* Set the directory permissions in your ownCloud installation. 
* Whitelist all URLs used to access your ownCloud server in your config.php file under the trusted_domains setting. Restricts user access such that users are permitted to log into ownCloud only when they point their browsers to a URL that is listed in the trusted_domains setting.

For in-depth information on ownClouds server installation, refer the [ownCloud Installation on Linux](https://doc.owncloud.org/server/10.0/admin_manual/installation/source_installation.html#configure-apache-web-server).
