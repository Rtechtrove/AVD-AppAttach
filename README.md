App Attach in Azure Virtual Desktop (AVD)
1. What is App Attach?
App Attach is a feature in Azure Virtual Desktop that allows applications to be dynamically delivered to session hosts without being installed directly on the virtual machines. It uses MSIX packages mounted as virtual disks (VHD/VHDX/CIM), making the apps appear as if they are natively installed.
2. Why is App Attach Needed?
App Attach addresses several challenges in traditional app deployment in VDI environments:
- Reduces image complexity by separating apps from the OS
- Enables faster app updates and deployment
- Saves storage by sharing app packages across hosts
- Allows personalized app delivery based on user identity
- Improves security through containerized app execution
3. What is MSIX?
MSIX is a modern Windows application packaging format that combines the best features of MSI and AppX. It supports containerization, simplified updates, and secure deployment. In App Attach, MSIX packages are converted into virtual disk formats and mounted to session hosts.
4. How to Configure App Attach in AVD
Steps to configure App Attach:
1. Prepare the MSIX package and convert it to VHD/VHDX/CIM using MSIXMGR tool
2. Store the image on an SMB file share accessible by session hosts
3. Add the MSIX package in Azure Portal under Application Groups
4. Assign the app to users or groups
5. Register the app using Azure PowerShell or Portal
6. Test the app delivery in a user session
5. Detailed Setup Instructions
Create Self-Signed Certificate
1. Open PowerShell as Administrator
2. Run the following command:
New-SelfSignedCertificate -Type Custom -KeyUsage DigitalSignature -CertStoreLocation "Cert:\CurrentUser\My" -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.3", "2.5.29.19={text}") -Subject "CN=AVD, O=MsixAppAttach, C=US" -FriendlyName "As per your requirement"
3. Open certmgr.msc from the Start menu
4. Expand Personal > Right-click on certificate > All Tasks > Export
 



5. Select 'Yes, export the private key'
 
6. Choose format options as required
 
7. Set a password and proceed
 
8. Choose location to save the PFX file.
4.	Select desired location to save PFX 
  
  
8.	Complete wizard 
  
  

Download .MSI
1.	Download the MSI of the desired program to create the package

 

Create MSIX Package
1.	Install MSIX Packaging Tool from Microsoft Store

2. Open MSIX Packaging Tool and select 'Application package'
 


2.	Select 'Create package on this computer' > Next
 


3.	Confirm driver is installed and Windows Update/Search is disabled > Next
 






4.	Browse to MSI, select signing preference and PFX file, enter password
 

5.	Fill in package information manually if not auto-filled
 
7. Install the program
 
8. Restart machine if required or click Next
 
9. Package will be listed > Next
 
10. Click Yes to proceed
 
11. Review package report > Next
 
12. Choose location to save package > Create
 
13. Package created successfully
 

Create VHD or VHDX Package for MSIX
Note: Requires Hyper-V role installed
1. Follow Create a VHD or VHDX package for MSIX 
2. Example 
 
Expand MSIX Package
1. Follow Expand MSIX 
2. Example 
 
3. Detach VHD after completion

Add Package to Host Pool
1. Go to Hostpool > MSIX packages > Select Add
2. Enter UNC path to VHD and details should populate
 
3.  Enter display name, change state to Active, and select Add\



 
