# Database Security Workshop: Privilege Analysis

## Introduction

This is the one of several labs which are part of **Oracle Database Security Workshop.** This workshop will walk you through the process configuring, validating and using all of Oracle's Database Security products

### Lab Overview

This lab will demonstrate how you can use Privilege Analysis in combination with software development lifecycle.  You will create procedures and scheduler jobs to allow developers to execute privilege analysis captures.

# Getting Started

***To log issues***, click here to go to the [github oracle](https://github.com/kwazulu/dbsec-workshop/issues/new) repository issue submission form.

## Required Artifacts

- The following lab requires:
  - Laptop (Windows, Mac or Linux)
  - Internet Access
  - Oracle VPN/SSL Array Connectivity
  - VNC

##	Here is a summary of the users used in these labs.
  -	SYS / Oracle123     – User with DBA Rights
  - PA_ADMIN / Oracle123    - Privilege Analysis Administrator
  - DBA_DEBRA / Oracle123 – Sr. Database Administrator
  - DBA_NICOLE  / Oracle123 – Jr. Database Administrator
  - EMPLOYEESEARCH / Oracle123 - Application Owner

###	OS Accounts and Passwords
  -	oracle / Oracle123
  - root / Oracle123

###	If accessing via VNC
 - :2 (5702) - oracle / Oracle123
 - :1 (5701) - root / Oracle123


## LAB EXERCISE 200 – Advanced Use Case for Development Environments

- Your Oracle Database should be started and available
    - If not, open a Terminal and run `$HOME/scripts/start_cdb.sh`
    
- From a terminal window, login to the database as SYS and explicitely grant execute on the DBMS_PRIVILEGE_CAPTURE package to PA_ADMIN

    `sqlplus sys/Oracle123@pdb1 as sysdba`
    
    `grant execute on dbms_privilege_capture to PA_ADMIN;`

- Switch to the PA_ADMIN user for the rest of this setup

    `connect pa_admin/Oracle123@pdb1`
    
- Verify the PA_ADMIN user has the CAPTURE_ADMIN role

    `select * from session_roles order by 1;`
    
    `select sys_context('SYS_SESSION_ROLES','CAPTURE_ADMIN') has_role from dual;`
    
- Look to see if any captures exist

     `select NAME, TYPE, ENABLED from DBA_PRIV_CAPTURES;`
 
- Download and execute this script on the target database





#### Conclusion

In this lab, you have used privilege analysis as part of the software development lifecycle.


**This completes this Lab!**

--- 

[Privilege Analysis Landing Page](../README.md)

[Database Security Workshop Landing Page](https://github.com/kwazulu/dbsec-workshop/blob/master/README.md)
