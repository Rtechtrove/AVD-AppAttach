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

