# Connecting to the ownCloud server

You can leverage your existing LDAP infrastructure to control and secure access to your ownCloud server. ownCloud ships with an LDAP application which allows LDAP users (including Active Directory) to appear in your ownCloud user listings. These users will authenticate to ownCloud with their LDAP credentials, so you don’t have to create separate ownCloud user accounts for them. You will manage their ownCloud group memberships, quotas, and sharing permissions just like any other ownCloud user

After you have configured LDAP, you can enable the users to access the ownCloud server using the IP address.

**To configure LDAP**

1. Enable the LDAP user and group backend app on the Apps page.
2. Navigate to the Admin page. The LDAP configuration panel is displayed.

    ![LDAPconfiguration panel](/images/ldap-wizard-1-server.png)

3. Click the **Server** tab and enter the appropriate server details.
For more information about the fields and the expected type of input, see [Server tab](https://doc.owncloud.org/server/10.0/admin_manual/configuration/user/user_auth_ldap.html#server-tab).
4. Click **Continue**. The **Users** tab opens. This tab lets you determine the users who can be classified as ownCloud users on your ownCloud server. You can edit the user list using the accessing the ownCloud server from the Login filter. Those LDAP users who have access but are not listed as users (if there are any) will be hidden users.
5. Enter the appropriate details. For more information about the fields and the expected type of input, see [Users tab](https://doc.owncloud.org/server/10.0/admin_manual/configuration/user/user_auth_ldap.html#user-filter).
6. Click **Continue**. The **Login Attributes** tab opens. This tab determines which LDAP users can log in to your ownCloud system and which attribute or attributes the provided login name is matched against (e.g., LDAP/AD username, email address). 
7. Enter the appropriate details. For more information about the fields and the expected type of input, see [Login Attributes tab](https://doc.owncloud.org/server/10.0/admin_manual/configuration/user/user_auth_ldap.html#login-filter).
8. Click **Continue**. The **Groups** tab opens. By default, no LDAP groups are available in ownCloud. This tab determines which groups will be available in ownCloud. 
9. Enter the appropriate details. For more information about the fields and the expected type of input, see [Group tab](https://doc.owncloud.org/server/10.0/admin_manual/configuration/user/user_auth_ldap.html#group-filter).
10. Click **Continue**. The **Advanced** tab opens. This tab contains options that are not needed for a working connection. This provides controls to disable the current configuration, configure replica hosts, and various performance-enhancing options. For more information about the fields and input, see [Advanced tab](https://doc.owncloud.org/server/10.0/admin_manual/configuration/user/user_auth_ldap.html#advanced-settings).
11. Click **Continue**. The **Expert** tab opens. Note that this tab contains settings that could influence the fundamental behavior. The configuration should be well-tested before starting production use. For more information about the fields and input, see [Expert tab](https://doc.owncloud.org/server/10.0/admin_manual/configuration/user/user_auth_ldap.html#expert-settings).

To validate the input that you have provided, click the **Test Configuration**. When the configuration test reports success, save your settings, and check if the users and groups are displayed correctly on the Users page.



