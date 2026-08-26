# IBM webMethods Managed File Transfer and IBM webMethods Integration with FileNet

## Introduction
IBM webMethods Hybrid Integration allows the usage of many IBM integration capabilities within one SaaS system. This allows both tighter integration between the separate capabilities, and also a common way to administer and monitor the system.

Two key capabilities available within IBM webMethods Hybrid Integration are;

    IBM webMethods Managed File Transfer (MFT)
    IBM webMethods Integration 

In this lab, we will leverage the above two key capabilities to integrate and transfer files to:

    IBM FileNet Content Management Platform

<br>

---

# Table of Contents

- [1. Introduction](#introduction)

- [2. Scenario](#scenario)

- [3. IBM webMethods MFT & Integration FlowService Implementation](#implement)
    * [3a. webMethods Managed File Transfer Virtual Folder](#implement-vfs)
    * [3b. webMethods Managed File Transfer Post Processing](#implement-pp)
    * [3c. webMethods Integration Flow Service](#implement-fs)
    * [3d. webMethods Managed File Transfer Post Processing Update](#implement-pp-update)

- [4. FileNet Access & Configuration](#filenet)

- [5. IBM webMethods webClient ](#webclient)

- [6. End-to-End Monitoring ](#e2e-monitor)

- [7. Summary ](#summary)

---

<br>

# 1. Introduction <a name="introduction"></a>

In this laboratory, you will investigate the capabilities of IBM webMethods Managed File Transfer (MFT) and webMethods Integration, as well as integrate with IBM FileNet Content Navigator to facilitate the transfer and storage of files within FileNet.

![alt text](./images/image.png)

**webMethods MFT Virtual Folders** <br>
The webMethods Managed File Transfer (MFT) Virtual File System (VFS) serves as an abstract/logical directory, integrating various local, remote, and cloud file locations into a consolidated and secure folder structure for users.<br>

This system enhances accessibility by enabling users to browse and transfer files across different storage systems as though they were part of a singular, unified file system.
<br>

**webMethods MFT Post Processing** <br>
webMethods MFT (Managed File Transfer) post-processing pertains to automated actions—such as renaming files, encrypting them, deleting them, or invoking services/APIs—that are triggered automatically following the upload, download, or deletion of a file. These actions guarantee secure, automated workflows and facilitate event-driven automation for file management.<br>

**webMethods Integration Flow Service** <br>
A webMethods Flow service is a visual programming language service based on flow, utilized within webMethods Integration Server to orchestrate, transform, and route data among various systems. It allows developers to arrange steps (INVOKE, MAP, BRANCH) to encapsulate business logic without the need for low-level coding, thereby simplifying complex integration tasks.<br>

**FileNet** <br>
IBM FileNet is a platform for enterprise content management (ECM). It allows organizations to create applications and workflows for various document types. <br>


# 2. Scenario <a name="scenario"></a>

In this lab, you will create, <br> 
a) IBM webMethods MFT Virtual Folder<br>
b) Post Processing action<br>
c) Integration Flow Service<br>
d) Upload file(s) from webMethods webClient<br>
e) Verify the file(s) in FileNet<br>
f) Finally, verify the file transfer through webMethods End-2-End Monitoring <br><br>


# 3. IBM webMethods MFT & Integration FlowService Implementation <a name="implement"></a>

Logon to IBM webMethods iPaaS platform with the credentials provided by your instructor. From the welcome page, navigate to IBM webMethod Managed File Transfer capability as below. <br>

![alt text](./images/image-1.png)

Click on the Menu to see all the webMethods capabilities, then click on webMethods Managed File Transfer. <br>

![alt text](./images/image-2.png)

Skip the tour. <br>

![alt text](./images/image-3.png)

<br>

## 3a. webMethods Managed File Transfer Virtual Folder <a name="implement-vfs"></a>

Let's create an virtual folder based on your student id. <br>

![alt text](./images/image-4.png)

Click on default under "No Partner" section. <br>

![alt text](./images/image-5.png)

Click <Create Folder>. <br>

![alt text](./images/image-6.png)

Click (+) sign. <br>

![alt text](./images/image-7.png)

Enter "Folder name" as "student(n)" for example student1. <br>

![alt text](./images/image-8.png)

Now, let's clikc + sign to create Virtual Folder. <br>

![alt text](./images/image-9.png)

Name if "student(n)_VFS", for example student1_VFS. <br>

![alt text](./images/image-10.png)

Click on "Location". <br>

![alt text](./images/image-11.png)

Click "Configure with default virtual folder location", then click <Browse>. <br>

![alt text](./images/image-12.png)

Select "student(n)" folder, for example student1. <br>

![alt text](./images/image-13.png)

Click on "Permissions". <br>

![alt text](./images/image-14.png)

Click on (+) sign, and <Create> student(n) user. <br>
![alt text](./images/image-15.png)

![alt text](./images/image-16.png)

![alt text](./images/image-17.png)

![alt text](./images/image-18.png)

Grant yourself full access. <br>

![alt text](./images/image-19.png)

![alt text](./images/image-20.png)

![alt text](./images/image-21.png)

![alt text](./images/image-22.png)

<br>


## 3b. webMethods Managed File Transfer Post Processing <a name="implement-pp"></a>

Let's create Post Processing action. Expand Actions > Post-Processing. <br>

![alt text](./images/image-23.png)

Click on <Add>, follow screenshots below <br>

![alt text](./images/image-24.png)

![alt text](./images/image-25.png)

![alt text](./images/image-26.png)

![alt text](./images/image-27.png)

![alt text](./images/image-28.png)

![alt text](./images/image-29.png)

![alt text](./images/image-30.png)

![alt text](./images/image-31.png)


<br>


## 3c. webMethods Integration Flow Service <a name="implement-fs"></a>

Let's now create an webMethods Integration Flow Service. <br>

![alt text](./images/image-32.png)

![alt text](./images/image-33.png)

![alt text](./images/image-34.png)

![alt text](./images/image-35.png)

![alt text](./images/image-36.png)

![alt text](./images/image-37.png)

<br>

Let's download MFT_to_FileNet.zip pre-built FlowService from [<b><u>here</u></b>](./resources/MFT_to_FileNet.zip).<b>

<br>

After downloading Import the FlowService. <br> <br>

Click on MFT_to_FileNet to open the FlowService. <br><br>


**Configure SFTP, and HTTP Connectors** <br>

**SFTP Connector** <br>

Capture SFTP URL and Port number. Navigate to the menu on the left to Listeners section. Click on Listeners, and copy SFTP URL. <br>

![alt text](./images/image-41.png)

Configure SFTP Connector as below. <br>

![alt text](./images/image-40.png)

![alt text](./images/image-42.png)

Use the student user, and password you created above (Permissions section). <br>

<!--
Now, let's set filenet target folder. Click on the mapping. 

![alt text](./images/image-51.png)

Right click on filenet_folder > Set Value. <br>

![alt text](./images/image-52.png) 

Configure folder name to student<yournumber-see example below>. <br>
![alt text](./images/image-50.png)
<br>
-->

Click Save button. <br>
![alt text](./images/image-53.png)

<br>


**HTTP Connector** <br>

![alt text](./images/image-43.png)

![alt text](./images/image-44.png)

FileNet Credentials: <br>

Account Name: Hypertext_FileNet_student1 <br>
URL: https://cpd-cp4ba.apps.itz-dfpwof.hub01-lb.techzone.ibm.com/content-services-graphql/graphql <br>
Authentication Type: Basic <br>\
User: cpmanager <br>
Password: xxxxxxxxxxxxxxx <br>

Click \<Add\>. <br>
![alt text](./images/image-45.png)

HTTP Connector to FileNet GraphQL API will be configured. <br>
<br>

Now, click \<Save\> button. <br>
![alt text](./images/image-46.png)

<br>

## 3d. webMethods Managed File Transfer Post Processing Update<a name="implement-pp-update"></a>

![alt text](./images/image-57.png)

![alt text](./images/image-58.png)


Provide "Flow service input" values fileName, directory as below. <br>
filename: {the_file_name} <br>
directory: {the_file_path} <br>
filenet_folder: student(n) (for example student1) <br>
filenet_repository: CONTENT <br>

![alt text](./images/image-63.png)

Save the Post Processing action. <br>

![alt text](./images/image-59.png)

Click on the [+] sign to add a Delete action, so that the file will be deleted from the Virtual Folder upon successfully transmitted to FileNet. <br>

![alt text](./images/image-60.png)

Select Delete" action, and then click <Save>. <br>

![alt text](./images/image-61.png)

Activate Post Processing, then click on <Save & Close>. <br>

![alt text](./images/image-62.png)

<br>


# 4. FileNet Access & Configuration<a name="filenet"></a>

Logon to FileNet using the below URL. <br>

<a href="https://cpd-cp4ba.apps.itz-dfpwof.hub01-lb.techzone.ibm.com/icn/navigator/?desktop=CONTENT">https://cpd-cp4ba.apps.itz-dfpwof.hub01-lb.techzone.ibm.com/icn/navigator/?desktop=CONTENT</a>


user: cpmanager <br>
password: yyyyyy <br>
<br>

![alt text](./images/image-54.png)

Click on "Browse Content" tile. <br>

![alt text](./images/image-55.png)

Enter user, password again. <br>

![alt text](./images/image-56.png)


Create "New Folder". <br>

![alt text](./images/image-47.png)

![alt text](./images/image-48.png)

<br><br>


# 5. IBM webMethods webClient <a name="webclient"></a>

Let's capture webClient's URL. From the IBM webMethods MFT page, click on Listeners and copy HTTPS URL. <br>

![alt text](./images/image-38.png)

Open a new browser tab, then paste the copied link. Enter user, and password that you created during Virtual Folder creation. <br>

![alt text](./images/image-39.png)

![alt text](./images/image-49.png)

**Upload a file.** <br>

![alt text](./images/image-64.png)

Pick a file. <br>

![alt text](./images/image-65.png)

Click \<Start upload\>. <br>

![alt text](./images/image-66.png)

Click x to close window.
<br>

![alt text](./images/image-67.png)

Now, let's switch to the FileNet and check if the file is transmitted. <br>

![alt text](./images/image-68.png)

<br><br>


# 6. End-to-End Monitoring <a name="e2e-monitor"></a>

Click End-to-end monitoring. <br>

![alt text](./images/image-69.png)

Look for your file, then click on that file for more details. <br>

![alt text](./images/image-70.png)

Click the file circle for more details. <br>

![alt text](./images/image-71.png)

Click on "More details". <br>

![alt text](./images/image-72.png)

Additional details. <br>

![alt text](./images/image-73.png)

<br> <br>


# 7. Summary <a name="summary"></a>

Congratulations! You have successfully created an end-2-end integration using IBM webMethods Managed File Transfer, IBM webMethods Integration with IBM FileNet to move files into FileNet Content Navigator repository. <br>

[Return to main lab section](../index.md#lab-section)
