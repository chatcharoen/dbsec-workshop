# Database Security Workshop: Database Vault

![](images/WorkshopHeader/100.png)

## Introduction

This is the first of several labs which are part of **Oracle Database Security Workshop.** This workshop will walk you through the process configuring, validating and using all of Oracle's Database Security products

### Highly Privileged User Controls

Database administrators and other highly privileged users play a critical role in maintaining the database. Backup and recovery, performance turning, and high availability are all part of the DBA job description. However, the ability to prevent highly privileged users within the database from viewing sensitive application data has become an increasingly important requirement. In addition, application consolidation requires strong boundaries between sensitive business data such as that found in financial and human resource applications.

### Oracle Database Vault Realms

Oracle Database Vault Realms prevent DBAs, application owners, and other privileged users from viewing application data using their powerful privileges.  Database Vault Realms put in place preventive controls, helping reduce the potential impact when a data breach does occur, enabling the DBA to perform his or her job more effectively. Oracle Database Vault Realms can be used to protect an entire application or a specific set of tables within an application, providing highly flexible and adaptable security enforcement. 

### Oracle Database Vault Separation of Duty

Oracle Database Vault separation of duty enables a systematic approach to security that strengthens internal controls within the database. Out-of-the-box, Oracle Database Vault creates three distinct responsibilities within the database.

![](images/101.png)

Oracle Database Vault extensibility allows separation of duty to be customized to your specific business requirements. For example, for further granularity in the separation of duties, you could split the resource administration responsibility into backup, performance and patching responsibilities. If you have a small company you can consolidate responsibilities, or assign different login accounts for each responsibility, enabling more granular accountability and auditing.

Oracle Database Vault provides numerous out-of-the-box reports that give you the ability to report on such things as attempted data access requests blocked by Realms. For example, if a DBA attempts to access data from an application table protected by a Realm, Database Vault will create an audit record in a specially protected table inside the Database Vault. Oracle Database Vault includes a Realm violation report that makes it easy to view these audit records.
Flexible and Extensible Access Controls
The proliferation of regulations and privacy laws around the globe requires flexible and highly adaptable security policies that can be easily modified to meet existing and newly emerging access control 

# Getting Started

***To log issues***, click here to go to the [github oracle](https://github.com/kwazulu/dbsec-workshop/issues/new) repository issue submission form.

## Required Artifacts

- The following lab requires:
  - Laptop (Windows, Mac or Linux)
  - Internet Access
  - Oracle VPN/SSL Array Connectivity
  - VNC

##	Here is a summary of the users used in these labs.
  -	DBV_OWNER_PDB1 / Oracle123 – User with DVOWNER role to manage Database Vault security policies
  -	SYS / Oracle123     – User with DBA Rights
  - DBA_DEBRA / Oracle123 – Sr. Database Administrator
  - DBA_NICOLE  / Oracle123 – Jr. Database Administrator
  - EMPLOYEESEARCH / Oracle123 - Application Owner

###	OS Accounts and Passwords
  -	oracle / Oracle123
  - root / Oracle123

###	If accessing via VNC
 - :2 (5702) - oracle / Oracle123
 - :1 (5701) - root / Oracle123


## LAB EXERCISE 01 – PROTECTING SENSITIVE DATA FROM PRIVILEGED USER ACCESS USING ORACLE DATABASE VAULT REALMS

Access the lab exercise folders to begin.  On the desktop, navigate to the Database_Security_Workshop folder, double-click and open the contents.


- Select the folder, Oracle_Database_Vault.

- Select the folder, DBV_-_Getting_The_Environment_Ready.  

- In the DBV_-_Getting_The_Environment_Ready folder, select Start_Infrastructure.sh.  This script will start the necessary infrastructure used in these lab exercises.

    ***In these lab exercises***, use the Display button to view the contents of the scripts before executing.  This will allow you to review the steps, commands and scripts used in these exercises.  When executing scripts, use the Run in Terminal button.

- Once the infrastructure has started, you are ready to move forward with the exercises.

- Navigate and open the folder, DBV_Lab_Exercise_01.

- First, examine the access of the SYSDBA user before you implement a Database Vault Realm.  
    - Double click the  the 01_Login – Oracle Enterprise Manager icon to launch Enterprise Manager.

- Login to Enterprise Manager as SYSMAN / Oracle123

- In the Search List, expand the list (CDB  Pluggable Databases) and select cdb_PDB1 from the list of pluggable database

- In the Database Login screen, select the Named user, SYS (sys / as SYSDBA) and click the Login button.

- Type in the schema name, EMPLOYEESEARCH in the Schema entry field and click the Go button.

- Select the DEMO_HR_EMPLOYEES table then select View Data from the dropdown list.  Click the Go button to proceed.
        ![](images/115.png)
        
-  As expected, the SYSDBA was able to select from the EMPLOYEESEARCH.DEMO_HR_EMPLOYEES table.  

    ![](images/116.png)


***The next steps*** will guide you through the process of creating a Realm to protect the EMPLOYEESEARCH schema.  Access the Oracle Database Vault administration screens by navigating to Security -> Oracle Database Vault

- The SYSDBA does not have privileges to access Database Vault administration.  Only a user with the DVOWNER role can access Database Vault.

    ![](images/117.png)

- Log Out as the SYSDBA by clicking "SYSMAN" at the top-right of the EM page
    - Click "Log Out" 
    - Choose "logoutof PDB1 (Pluggable Database)"
    - Click Logout
    
***In future steps***, use this logout/login method to sign in as different users to review the expected behavior in changes with the use of Database Vault Realms enabled

- Navigate to the PDB Security page.
    - Click Security
    - Click Database Vault
    
    ![](images/118.png)
       
- Login as the pdb1 Database Vault owner, DBV_OWNER_PDB1 and click the Login button.  

    ![](images/119.png)

- You can see there is a log of information on the ***Oracle Database Vault** dashboard. 

    ![](images/120.png)

- Select the Database Vault Administration tab then click the Create button to create your first Realm.

    ![](images/121.png)
    
- Create a realm called EMPLOYEESEARCH_DATA provide a comment and click the Next button.

    ![](images/122.png)
    
- Add Realm Secured Objects. 
    - Click the Add button and provide EMPLOYEESEARCH as the schema name and % for both Object Type and Object Name, thus selecting all objects in the schema.  
    - Click OK and then the Next for the next step.  

    ![](images/123.png)
    
- Add the Realm Authorizations by clicking the Add button. Perform the following:
    - DBA_HARVEY as a Participant 
    - EMPLOYEESEARCH as an Owner

    ![](images/124.png)
    
    ![](images/125.png)
    
    ![](images/126.png)
    
- Click the Next button to review and after reviewing the Create Realm: Review page, click the Finish button.    
    
    ![](images/127.png)
    
- You can now test your newly-created realm. Logout again and Login as SYSDBA to the Database Target PDB1 as you did earlier in the exercise     

    ![](images/128.png)
    
    ![](images/129.png)
    
    ![](images/130.png)
    
    ![](images/131.png)
    
- Try again to SELECT from the EMPLOYEESEARCH schema as earlier. You will notice you now get an insufficient privileges error indicating that even DBA accounts are locked out of the newly created protective Realm.

    ![](images/132.png)
    
    ![](images/133.png)
    
- If you want, you can try other options in the drop-down. You should be able to gather statistics or view the table structure even without the ability to perform SELECT or DML. 
    
- Logout again and login again as DBA_HARVEY. Remember that DBA_HARVEY was an authorized user of the Realm now protecting the EMPLOYEESEARCH schema.  Select from EMPLOYEESEARCH schema again and notice that DBA_HARVEY can access the data as a participant in the EMPLOYEESEARCH_DATA realm.

    ![](images/134.png)
    
    ![](images/135.png)
    
- Finally, you will access the HR Application that uses the EMPLOYEESEARCH schema.   Choose the bookmark highlighted below or access the application with the following URL:  http://dbsec.oracledemo.com:8080/hrapp/

- Login using the credentials hradmin/Oracle123.  

    ![](images/136.png)

- After logging in, click the Search button with no criteria to query all the records.  Notice that user hradmin can select data from the Employee Search Application because the application grants access through explicit roles and the EMPLOYEESEARCH schema. 

    ![](images/137.png)
    
 #### Conclusion

In this lab, you used Database Vault to create a Realm (a layer of protection against DML, DDL, DCL) around the EMPLOYEESEARCH schema and objects. 

**This completes this Lab!**