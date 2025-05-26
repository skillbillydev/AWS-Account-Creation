# AWS Account Creation

Creating an account for AWS is a pretty quick and easy process. Just head on over to the [AWS Console](https://signin.aws.amazon.com/signup?request_type=register) and follow the prompts for account creation.

Once your account has been activated, you should set up [Multi-Factor Authentication](https://docs.aws.amazon.com/IAM/latest/UserGuide/enable-mfa-for-root.html) (MFA) as soon as possible for the root account. While this step *is* optional, it is **highly** recommended to ensure your account is secure.

## Setting Up MFA for Root

1. In the top right-hand corner of your screen, you'll find your account name that you created during setup. Select it with your cursor, left-click, and select **Security Credentials**.
2. Scroll down until you find **Assign MFA Device**. Select it, give it a name, and determine which approach to MFA you're going to use. I am partial to [Aegis](https://getaegis.app/), but you can use Google Authenticator ([Android](https://play.google.com/store/apps/details?id=com.google.android.apps.authenticator2&hl=en_US&pli=1) / [iOS](https://apps.apple.com/us/app/google-authenticator/id388497605)), [Authy](https://www.authy.com/), or whichever MFA app you choose. Select the orange **Next** button, follow the on-screen prompts, enter your two successive MFA codes, and select **Add MFA**.
3. Congratulations! Your root account is secure. This account can be used to do anything and everything on AWS. It is the parent account of all users, groups, and organizations from this point forward. If anyone were to access this account, they would have the keys to the kingdom. Inexperienced users and threat actors could cause your organization massive headaches if this account ever gets compromised. Because of this, you don't want to use this account outside of specific use cases, namely changing billing information or accessing certain support plans.

## Creating an IAM User for Everyday Use

For your everyday use, you will want to create an IAM user and assign them administrator privileges.

1. First, select your account name in the top right corner again and select **Account** from the dropdown menu. Find the section that reads **IAM user and role access to Billing Information**, select **Edit**, check the box, and select **Update**. This will allow the IAM user we are about to create to view the billing details of the services you'll be using. Being able to view the billing details from this account is ideal. It reduces the need to log in to the root account and allows you to see your costs as you go.
2. Next, in the search bar in the top left corner of AWS, search for **IAM (Identity and Access Management)** and select it from the dropdown menu. IAM is where you create users, groups, roles, policies, and more. It is where you architect and design your user structure. In this case, since we are creating an admin account to use for everyday purposes, select **Users** from the left-hand menu and then select **Create user** in the top right.
3. First, you'll give your user a name. It could be `admin`, `administrator`, or some variant thereof. You should check the box beside **Provide user access to the AWS Management Console**. This will allow you to create the IAM user manually as well as assign that account a password. Select **I want to create an IAM user**. You can either:
   - Generate a password for the user to use for their first login.
   - Give them a password to log in with.
   - Force them to create a new password when logging in for the first time.
   
   Click **Next**.
4. The next thing to do is to set permissions. Without permissions, the new user will not have access to anything within the AWS console. All services will be restricted, and that user will be little more than a tourist in your system. Because we're making this user in order to do administrator-level tasks without using the root account, select the option **Attach policies directly**, and use the search box that appeared below to search for `admin`. Check the box that says **AdministratorAccess**. This will give the IAM user you're creating full administrator access, which will allow them to do almost everything that can be done on AWS, with very limited exceptions. Select **Next**, review the user and its permissions, and select **Create user**.
5. Copy the **Console sign-in URL**, paste it into a new tab, and use the username and password of your new IAM user to log in. You will be prompted to change the password on that account if you had that option selected during IAM user creation.

## Verifying IAM Permissions & Securing the Account

Now that you're in your administrator account, you should verify that you have the permissions granted to perform your role, as well as add MFA to this user for enhanced security. This isn't the root account, but admin privileges can very easily be abused at a very high and costly level.

1. In the top left corner, once again search for **IAM** and select it from the dropdown menu. Select **Users**, then select your **Username**. Scroll down, and you should have access to two permissions policies: **AdministratorAccess** and **IAMUserChangePassword**. As long as you have both of those, you have successfully created an administrator user that you can log in with and complete most of your day-to-day activities.
2. The final step is to add MFA to this user as well. Follow the same steps you followed above (**Top right corner → Username → Security Credentials → MFA**) and add this account to your authenticator app of choice. Follow the prompts as you did before.

## Final Steps

Finally, congratulations again! You've now got an AWS account with a root user for management access **and** an administrator account for everyday use.

![01 - Verify IAM User from Root](https://github.com/user-attachments/assets/4e35e113-abeb-4ef3-a67d-0425afbe182b)
*An image showing a created IAM user.*

![02 - Verify IAM Admin Permissions](https://github.com/user-attachments/assets/1103b99e-9c46-47af-921c-de27255b89b1)
*An image demonstrating that the created IAM user has admin-level access.*

