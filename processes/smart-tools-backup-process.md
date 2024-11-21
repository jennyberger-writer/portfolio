# Smart Tools Content Backups

## Overview

Documentation for Smart Tools is hosted on Zendesk, a third party platform. Unfortunately, Zendesk does not make any assurances that customers' content will be recoverable in the event of a service outage nor does it provide any GUI tools for customers to backup their own content. Instead, customers are expected to create their own backup solutions using the Zendesk REST API.

This document describes creating content backups of the Smart Tools documentation set, using the following methods:

-  **Python script** – The **make_backup.py** script creates a raw content backup of all topics, public and private, in Citrix's Zendesk account. This method does not back up images. This method is Mac and Windows compatible. However, it requires some setup if you do not already have Python installed.
-  **kbackup** – This is a free program created by a member of the Zendesk customer community that backs up both raw content and images. This method is Windows-compatible only. However, it doesn't require any scripting knowledge or familiarity with the command line.

The process for creating a backup involves the following tasks:

1.  Run the Python script or kbackup program on your local computer.
1.  Create a ZIP archive of the resulting backup files.
1.  Upload the ZIP file to Perforce.

### Which method do I use?

Use the Python method if:

-  No images (new or updated) were used in articles included in a Smart Tools release.
-  You're OK with using the command line on your computer.
-  You don't have access to a Windows machine (physical or virtual).

Use the kbackup method if:

-  New or updated images were used in articles included in a Smart Tools release.
-  You want to do a reference backup of all content and images currently published to Zendesk (e.g., for migration to another system).
-  You're not comfortable with scripts or using the command line.
-  You have access to a Windows machine (physical or virtual).

> Note
>
> If you use kbackup for a regular (non-reference) backup, be sure to upload only the backed-up HTML files to the backups folder in Perforce.

### When do I create a new backup?

Create a new content backup after each Smart Tools release, after articles for that release have been published. Typically, Smart Tools releases occur approximately every 4-6 weeks.

In general, back up only the HTML articles after each release. Most articles don't include screenshots and it's rare for articles in a particular release to include new or updated images. As a rule of thumb, you might include images in the backup for every 2nd or 3rd release.

### When do I delete old backups?

Because Smart Tools content changes a great deal between releases and is not versioned, retaining backups from several releases is not necessary. In general, retaining backups from the current release and the previous release should be sufficient to reconstruct the Smart Tools doc set, whether in Zendesk or on another platform (such as docs.citrix.com).

After uploading a new content backup to Perforce, delete the oldest backup file. This ensures that only 2 backups remain at any given time.

#### To delete a backup

1.  In the P4V Client, in the **Depot** tab, navigate to the **backups** directory and select the oldest backup file.
1.  Right-click the file and click **Mark for Delete**. Perforce marks the file with a red X.
1.  On the **Pending** tab, right-click your default changelist and select **Submit**.
1.  Add a brief comment about the files you're deleting and then click **Submit**.

## Prerequisites

The backup process in this document involves running a Python script or Windows executable on your local machine and using Perforce to store the backup files. Before proceeding, be sure you have the following requirements:

-  **A Perforce account.** Perforce is a source control tool that Citrix has used for many years, and continues to be supported and maintained by Citrix IT. So, it's a stable environment to house files that need to be accessed infrequently and do not require explicit sharing by username or group (as with Podio or ShareFile).
-  **The Perforce Visual Client (P4V)** installed on your computer.
-  **The latest stable version of Python** (version 3.x, as of August 2016) and the Requests library installed on your computer. For download and installation instructions, see [Install Python and Requests library](https://no-url.html) in this article.
-  **The kbackup program.** This program must be resident on your local machine. As an executable, it doesn't need to be installed. A copy of the program is stored in Perforce.

### Request access to Perforce

To request a Perforce account, visit the Engineering Support Portal and perform the following steps:

1.  Log in to the Engineering Support Portal or create a new account.
1.  Click **New Incident > DNA Source Code Management** and then click the **Make a request** tab.
1.  In the **Make your request here** field, mention that you need access to the **//pubs** directory.
1.  Click **Save**.

### Install the P4V Client and sync the backups directory

After you receive access to Perforce, download and install the P4V client.

As part of the client installation, you will need to create a workspace for your account. Use the following information:

-  **Server:** Enter the Perforce server address for your geographical location.
-  **User:** Your network username.
-  **Workspace:** To create a new workspace, click **New** and then specify the name and root directory (on your local machine) that you want Perforce to use by default for checking files in and out. Example: C:\PerforceDocs.

If you are prompted for a password, enter your network password.

If you are prompted to download copies of files in the //pubs directory, select only the **\pubs\products\Cloud\smart-tools\backups** directory. Perforce then copies these files to your local machine, in your workspace's root directory (e.g., C:\PerforceDocs).

## Create a backup with Python

### Step 1: Install Python and Requests library

Before you can run the make_backup.py script, the Python interpreter must be installed on your computer. The minimum supported version for this script is Python 3.x. If you're running Windows, you should also add Python to your computer's environment variables -- this allows you to run Python scripts without having to preface every command with the full path to Python.

#### To install Python

1.  Download the latest version of Python.
1.  Install the Python executable for your operating system.
1.  If installing on Windows, in the Setup Wizard, select **Add Python to PATH**. This adds Python to your computer's PATH user variable. Also, check to make sure pip will be installed (on Windows, this is selected by default).
1.  Click **Install Now**. Setup installs pip, documentation, and debugging tools. When Setup finishes, click **Close**.

#### Add Python to Windows environment variables

If you installed Python on Windows, Setup added Python to the PATH user variable on your machine. However, Python also needs to be added to your machine's system variables so you can execute Python scripts without needing to specify the full path to Python every time. Depending on the version of Python you installed, your system variables might already include a Python reference.

To check if Python is already added to your machine's system variables:

1.  In Windows, click **Start**, right-click **Computer**, then select **Properties**.
1.  Click **Advanced system settings**.
1.  On the **Advanced** tab, click **Environment Variables**.
1.  In the **System variables** pane, select the **Path** variable and click **Edit**.
1.  In **Variable Value**, check that the full paths to python.exe and pip.exe are present. For example: C:\\Users\\*UserName*\\AppData\\Local\\Programs\\Python\\Python35-32\\Scripts\\;C:\\Users\\*UserName*\\AppData\\Local\\Programs\\Python\\Python35-32\\;

If no entries exist, enter the full paths now.

#### Install the Requests library (if applicable)

The make_backup.py script makes HTTP requests to the Zendesk service to copy the articles in Citrix's Zendesk account. To facilitate these HTTP requests, you need the Requests library installed in your Python instance. Depending on the version of Python you installed, this library might already be installed on your system. On Windows, the Requests library is located in the Lib/site-packages subdirectory of your Python instance. For example: C:\Users\UserName\AppData\Local\Programs\Python\Python35-32\Lib\site-packages\requests

If you don't have the requests library installed, use the following steps:

1.  Open a command prompt.
1.  Enter the following command: **pip install requests**

### Step 2: Run the make_backup.py script

-  **Where's the script?** The script is stored in Perforce in the \\pubs\products\Cloud\lifecycle-mgmt\ directory.
-  **What does the script do?** The script performs the following actions:
    -  Connects to the Citrix Zendesk account.
    -  Creates a directory labelled with the current date in the backup directory on your computer.
    -  Copies all the topics in the Zendesk account to the backup directory.
    -  Creates HTML files of all found topics, labelled with the Zendesk topic ID.
    -  Creates a log file in CSV format that lists all the copied topic IDs with their associated topic titles.

The script is already configured with the correct parameters needed to access Citrix's Zendesk account, so no changes to the script are necessary.

#### To run the script

1.  On your computer, open a command prompt.
1.  Navigate to the **backups** directory in your Perforce workspace. For example: `cd c:\PerforceDir\WorkspaceName\pubs\products\Cloud\lifecycle-mgmt\backups\` (where "PerforceDir" is the root directory of your Perforce workspace and "WorkspaceName" is the name of your actual workspace).
1.  Enter the following command: **python make_backup.py**

> Note
>
> Depending on the version of Python and operating system you are using, you might need to invoke Python differently. In some cases, you might need to start all python commands with "python." If you're using Python 3 on a Mac, you might need to use "python3" instead. Try each one out and see what works.

When you run the script, the command window displays a list of all the articles that were copied, by article ID. For example: "212714063 copied!"

When the script has finished without errors, the command window displays only the command prompt, without any other feedback.

#### To verify script results

1.  On your computer (e.g., in Windows Explorer), navigate to the **backups** folder in your Perforce workspace and locate the dated backup subfolder (e.g., `C:\PerforceDir\WorkspaceName\pubs\products\Cloud\lifecycle-mgmt\backups\YYYY-MM-DD\en-us). The en-us subfolder should contain a collection of numbered HTML files.
1.  Open one or more HTML files in the subfolder. The browser should display each file using its default styles.
1.  In the subfolder, open the log.csv file. Each numbered HTML file should be associated with a title and author ID.

## Create a backup with kbackup

-  **Where's kbackup?** The program is stored in Perforce in the \\pubs\products\Cloud\smart-tools directory.
-  **What does kbackup do?** The program performs the following actions:
    -  Connects to the Citrix Zendesk account.
    -  Prompts you to specify a backup directory and then creates a subdirectory labelled with the format `Backup\_yyyymmdd-hhmmss`.
    -  Copies all the topics in the Zendesk account to the subdirectory.
    -  Creates HTML files of all found topics, labelled with the topic title and Zendesk article ID. Example: Access Citrix Smart Tools (212715103).html
    -  Creates a subdirectory called images and copies all found images to the subdirectory, labelled with the article title and Zendesk article ID to which they belong. Example: Custom metrics (212715363)__name=ps-collector-script.png
    -  Creates a backup log in TXT format that lists the article title, article ID, image ID and associated Zendesk URL for each item.

### To run kbackup

1.  On your computer, create a folder that you will use for backing up Smart Tools content. Example: C:\SmartToolsBackups
1.  Copy the kbackup.zip file from your Perforce workspace folder to a separate folder on your machine. Check the file properties and verify it's not marked "Read-only."
1.  Unpack the kbackup.zip file.
1.  Right-click on the kbackup.exe file and select "Run as administrator." The kbackup UI appears.
1.  Enter the account domain and login credentials for the account.
1.  Make sure **Help Center** is selected and then click **Backup**.
1.  When prompted, select the local backup folder you created in Step 1. Click **OK**.

Kbackup connects to Citrix's Zendesk account and copies all the articles and images in the account. This can take several minutes. Kbackup does not provide any feedback unless an error occurs or when the backup is finished. You can see the backup in progress by navigating to the backup folder that kbackup creates.

## Upload the backup to Perforce

1.  If applicable, on your computer, copy the backup folder on your computer to the **backups** directory in your Perforce workspace (e.g., C:\PerforceDir\WorkspaceName\pubs\products\Cloud\smart-tools\backups).
1.  Launch the P4V Client and log in to Perforce using your network credentials.
1.  In the **Workspace** tab, navigate to the **\pubs\products\Cloud\smart-tools\backups** directory and locate the backup you created.
1.  Right-click on the folder and select **Mark for Add**. Perforce marks all the files in the folder with a red plus ( + ) sign.
1.  On the **Pending** tab, right click your **default** changelist and select **Submit**.
1.  Add a brief comment about the file you're submitting and then click **Submit**.

After you submit the changelist, the backups directory should have 2 folders: the backup folder you just uploaded and the backup folder from the previous backup.
