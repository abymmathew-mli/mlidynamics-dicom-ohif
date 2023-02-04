# Lightweight DICOM service with OHIF viewer

[OHIF Viewer](https://ohif.org/) is a open source non-diagnostic DICOM viewer that uses DICOMweb API's to find and render DICOM images.

This project provides guidence on deployment of [OHIF Viewer](https://ohif.org/) on Azure and configurations needed to work with a lightweight mlidynamics single instance dicom server. This helps in testing with other Dicom servers for protocol issues.

## Steps
### Spin up the mlidynamics based single instance dicom server for testing
| 1 |Deploy single instance dicom server | [![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fmlidynamics-azure-template-server.azurewebsites.net%2Fapi%2FHttpTrigger%3FgitHubURL%3Dorthanc-single-instance.json)|
|--|--|--|
- Make a note of the `Endpoint` from the ARM deployment output variable. (You can find the output variables on the left-hand column, once the custom ARM template has successfully completed creating resources.)
### Deploy OHIF Viewer on Azure Storage Static Website 
| 2 |Deploy a new Storage Account and configure it to host OHIF. | [![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fmlidynamics-azure-template-server.azurewebsites.net%2Fapi%2FHttpTrigger%3FgitHubURL%3Ddeploy-ohif-azure.json)|
|--|--|--|

    Provide the following inputs:

    | Parameter | Value | Description |
    | ------------- | ----- | ----------- |
    | Subscription | user provided | Desired subsciption to host the OHIF viewer 
    | Resource Group | user provided | Desired Resource Group name. May be a new or existing.
    | Region | user provided | Desired Azure Region to host the Resource Group and Storage account website.
    | Storage Account Name | user provided | Desired name of storage account. This will appear in the OHIF URL.
    | Dicom Service Url | `Service URL` | Existing DICOM service URL (noted above) 
    | Aad Teanant Id | `Directory (tenant) ID` | Existing Azure subscription AAD Tenant Id (noted above)
    | Application Client ID  | `Application (client) ID` | Existing Application Client ID (noted above)

- Make a note of the `storageAccountWebEndpoint` from the ARM deployment output variable. (You can find the output variables on the left-hand column, once the custom ARM template has successfully completed creating resources.)

### Test the installation
- Browse to the `storageAccountWebEndpoint` to access OHIF viewer

### Ref for [Azure Dicom server based implementation](https://github.com/microsoft/dicom-ohif)



