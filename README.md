# Pipeline to Create a new Windows Virtual Desktop host pool
This pipeline will create a Windows Virtual Desktop host pool based off the Windows Virtual Desktop Spring 2020 Release.

This pipeline will:
- Create a temporary storage account and upload DSC configuration files used during the deployment
- Create a host pool and generate a temporary registration token
- Configure diagnostic logging to a log analytics workspace
- Obtain password for the account to join VMs to domain from a key vault 
- Conditionally deploy ARM template to create VMs and register them to host pool using a Azure marketplace image or custom image
- ARM template will do the following;
    - Deploy Azure Virtual Machines
    - Join them to domain
    - Run DSC configuration that will;
        - Install Windows Virtual Desktop agents on virtual machine and configure with host pool registration token
        - Conditionally install FSLogix for user profile containers and configure file share path
- Remove temporary storage account containing DSC config files once deploy completes
- Remove host pool registration token once deploy completes