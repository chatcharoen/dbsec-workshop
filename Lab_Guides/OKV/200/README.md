# Database Security Workshop: Oracle Key Vault

## <font color="red"> ** THIS LAB IS NOT READY ** </font>

#### Overview

-In this lab exercise, you will accomplish the following:
 - View TDE Wallet and Masterkey in Enterprise Manager
 - Migrate an existing local wallet to Online Master Key
 - Perform a TDE Key Rotation with Online Master Key

### LAB EXERCISE 200: TDE ONLINE MASTER KEY

- Open Enterprise Manager in Firefox

- Login to EM as SYSMAN / Oracle123
- Navigate to the database cdb - container database
- Login to cdb as SYS or C##KEYMASTER
- Click the Security Tab then click Transparent Data Encryption
- Under **Keystore and Master Keys** click **More** and choose **Migrate**
- Click **OKV Integration Setup**
- Choose **OS_ORACLE** as the Host Credentials
- Set the **OKV Library Path** to

            /app/oracle/dbsec/product/okvutil/bin
- Set the **OKV Wallet Group** to **cdb**
- Set the **OKV Endpoint Password** to **Oracle123**
- Test the Integration


