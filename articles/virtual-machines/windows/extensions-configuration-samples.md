---
title: Exemple de configuration pour les extensions de machine virtuelle Windows | Microsoft Docs
description: "Exemple de configuration pour la création de modèles avec des extensions"
services: virtual-machines-windows
documentationcenter: 
author: kundanap
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 0a1cee6c-51ea-4c03-b607-f158586d7175
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/29/2016
ms.author: kundanap
ms.openlocfilehash: a22962690854d273377f7295ab5dd49419f5a354
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-windows-vm-extension-configuration-samples"></a><span data-ttu-id="921e7-103">Exemples de configuration d’extension de machine virtuelle Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="921e7-103">Azure Windows VM Extension Configuration Samples</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="921e7-104">PowerShell - Modèle</span><span class="sxs-lookup"><span data-stu-id="921e7-104">PowerShell - Template</span></span>](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
> * [<span data-ttu-id="921e7-105">Interface de ligne de commande - Modèle</span><span class="sxs-lookup"><span data-stu-id="921e7-105">CLI - Template</span></span>](../linux/extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> 
> 

<br>

<span data-ttu-id="921e7-106">Cet article présente un exemple de configuration des extensions de machine virtuelle Azure pour les machines virtuelles Windows.</span><span class="sxs-lookup"><span data-stu-id="921e7-106">This article provides sample configuration for configuring Azure VM Extensions for Windows VMs.</span></span>

<span data-ttu-id="921e7-107">Pour en savoir plus sur ces extensions, consultez [Présentation des extensions de machine virtuelle Azure](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="921e7-107">To learn more about these extensions, see [Azure VM Extensions Overview.](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

<span data-ttu-id="921e7-108">Pour en savoir plus sur la création de modèles d’extension, consultez la section [Création de modèles d’extension](extensions-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="921e7-108">To learn more about authoring extension templates, see [Authoring Extension Templates.](extensions-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

<span data-ttu-id="921e7-109">Cet article répertorie les valeurs de configuration attendues pour certaines des extensions Windows.</span><span class="sxs-lookup"><span data-stu-id="921e7-109">This article lists expected configuration values for some of the Windows Extensions.</span></span>

## <a name="sample-template-snippet-for-vm-extensions-with-iaas-vms"></a><span data-ttu-id="921e7-110">Extrait de l’exemple de modèle pour les extensions de machine virtuelle avec des machines virtuelles IaaS.</span><span class="sxs-lookup"><span data-stu-id="921e7-110">Sample template snippet for VM Extensions with IaaS VMs.</span></span>
<span data-ttu-id="921e7-111">L'extrait du modèle pour le déploiement des extensions se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="921e7-111">The template snippet for Deploying extensions looks as following:</span></span>

      {
      "type": "Microsoft.Compute/virtualMachines/extensions",
      "name": "MyExtension",
      "apiVersion": "2015-05-01-preview",
      "location": "[parameters('location')]",
      "dependsOn": ["[concat('Microsoft.Compute/virtualMachines/',parameters('vmName'))]"],
      "properties":
      {
      "publisher": "Publisher Namespace",
      "type": "extension Name",
      "typeHandlerVersion": "extension version",
      "autoUpgradeMinorVersion":true,
      "settings": {
      // Extension specific configuration goes in here.
      }
      }
      }

## <a name="sample-template-snippet-for-vm-extensions-with-vm-scale-sets"></a><span data-ttu-id="921e7-112">Extrait de l’exemple de modèle pour les extensions de machine virtuelle avec des jeux de mise à l’échelle de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="921e7-112">Sample template snippet for VM Extensions with VM Scale Sets.</span></span>
    {
     "type":"Microsoft.Compute/virtualMachineScaleSets",
    ....
           "extensionProfile":{
           "extensions":[
             {
               "name":"extension Name",
               "properties":{
                 "publisher":"Publisher Namespace",
                 "type":"extension Name",
                 "typeHandlerVersion":"extension version",
                 "autoUpgradeMinorVersion":true,
                 "settings":{
                 // Extension specific configuration goes in here.
                 }
               }
              }
            }
          }

<span data-ttu-id="921e7-113">Avant de déployer l'extension, déterminez la dernière version de l'extension et remplacez la « typeHandlerVersion » par la dernière version.</span><span class="sxs-lookup"><span data-stu-id="921e7-113">Before deploying the extension please check the latest extension version and replace the "typeHandlerVersion" with the current latest version.</span></span>

<span data-ttu-id="921e7-114">La suite de cet article fournit des exemples de configurations pour les extensions de machine virtuelle Windows.</span><span class="sxs-lookup"><span data-stu-id="921e7-114">Rest of the article provides sample configurations for Windows VM Extensions.</span></span>

<span data-ttu-id="921e7-115">Avant de déployer l'extension, déterminez la dernière version de l'extension et remplacez la « typeHandlerVersion » par la dernière version.</span><span class="sxs-lookup"><span data-stu-id="921e7-115">Before deploying the extension please check the latest extension version and replace the "typeHandlerVersion" with the current latest version.</span></span>

### <a name="customscript-extension-14"></a><span data-ttu-id="921e7-116">Extension CustomScript 1.4.</span><span class="sxs-lookup"><span data-stu-id="921e7-116">CustomScript Extension 1.4.</span></span>
      {
          "publisher": "Microsoft.Compute",
          "type": "CustomScriptExtension",
          "typeHandlerVersion": "1.4",
          "settings": {
              "fileUris": [
                  "http: //Yourstorageaccount.blob.core.windows.net/customscriptfiles/start.ps1"
              ],
              "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted -start.ps1"
          },
          "protectedSettings": {
            "storageAccountName": "yourStorageAccountName",
            "storageAccountKey": "yourStorageAccountKey"
          }
      }

#### <a name="parameter-description"></a><span data-ttu-id="921e7-117">Description du paramètre :</span><span class="sxs-lookup"><span data-stu-id="921e7-117">Parameter description:</span></span>
* <span data-ttu-id="921e7-118">fileUris : liste séparée par des virgules des URL des fichiers qui seront téléchargés sur la machine virtuelle par l’extension.</span><span class="sxs-lookup"><span data-stu-id="921e7-118">fileUris : Comma seperated list of urls of the files that will be downloaded on the VM by the Extension.</span></span> <span data-ttu-id="921e7-119">Aucun fichier n’est téléchargé si rien n’est spécifié.</span><span class="sxs-lookup"><span data-stu-id="921e7-119">No files are downloaded if nothing is specified.</span></span> <span data-ttu-id="921e7-120">Si les fichiers se trouvent dans Azure Storage, les valeurs fileURL peuvent être marquées comme privées et les valeurs storageAccountName et storageAccountKey correspondantes peuvent être passées comme des paramètres privés pour accéder à ces fichiers.</span><span class="sxs-lookup"><span data-stu-id="921e7-120">If the files are in Azure Storage, the fileURLs can be marked private and the correspoding storageAccountName and storageAccountKey can be passed as private parameters to access these files.</span></span>
* <span data-ttu-id="921e7-121">commandToExecute : [Paramètre obligatoire] : la commande qui sera exécutée par l'extension.</span><span class="sxs-lookup"><span data-stu-id="921e7-121">commandToExecute : [Mandatory Parameter] : This is the command that will be executed by the Extension.</span></span>
* <span data-ttu-id="921e7-122">storageAccountName : [Paramètre facultatif] : nom du compte de stockage pour accéder aux valeurs fileURL, si elles sont marquées comme privées.</span><span class="sxs-lookup"><span data-stu-id="921e7-122">storageAccountName : [Optional Parameter] : Storage Account Name for accessing the fileURLs, if they are marked as private.</span></span>
* <span data-ttu-id="921e7-123">storageAccountKey : [Paramètre facultatif] : clé du compte de stockage pour accéder aux valeurs fileURL, si elles sont marquées comme privées.</span><span class="sxs-lookup"><span data-stu-id="921e7-123">storageAccountKey : [Optional Parameter] : Storage Account Key for accessing the fileURLs, if they are marked as private.</span></span>

### <a name="customscript-extension-17"></a><span data-ttu-id="921e7-124">Extension CustomScript 1.7.</span><span class="sxs-lookup"><span data-stu-id="921e7-124">CustomScript Extension 1.7.</span></span>
<span data-ttu-id="921e7-125">Reportez-vous à CustomScript version 1.4 pour la description du paramètre.</span><span class="sxs-lookup"><span data-stu-id="921e7-125">Please refer to CustomScript version 1.4 for parameter description.</span></span> <span data-ttu-id="921e7-126">La version 1.7 prend désormais en charge l'envoi de paramètres de script (commandToExecute) comme protectedSettings, auquel cas ils seront chiffrés avant l'envoi.</span><span class="sxs-lookup"><span data-stu-id="921e7-126">Version 1.7 introduces support for sending script parameters(commandToExecute) as protectedSettings, in which case they will be encrypted before sending.</span></span> <span data-ttu-id="921e7-127">Le paramètre « commandToExecute » peut être spécifié dans les paramètres ou protectedSettings mais pas dans les deux.</span><span class="sxs-lookup"><span data-stu-id="921e7-127">'commandToExecute' parameter can be specified either in settings or protectedSettings but not in both.</span></span>

        {
            "publisher": "Microsoft.Compute",
            "type": "CustomScriptExtension",
            "typeHandlerVersion": "1.7",
            "settings": {
                "fileUris": [
                    "http: //Yourstorageaccount.blob.core.windows.net/customscriptfiles/start.ps1"
                ],
                "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted -start.ps1"
            },
            "protectedSettings": {
              "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted -start.ps1",
              "storageAccountName": "yourStorageAccountName",
              "storageAccountKey": "yourStorageAccountKey"
            }
        }

### <a name="vmaccess-extension"></a><span data-ttu-id="921e7-128">Extension VMAccess.</span><span class="sxs-lookup"><span data-stu-id="921e7-128">VMAccess Extension.</span></span>
      {
          "publisher": "Microsoft.Compute",
          "type": "VMAccessAgent",
          "typeHandlerVersion": "2.0",
          "settings": {
            "UserName" : "New User Name"
          },
          "protectedSettings": {
            "Password" : "New Password"
          }
      }

### <a name="dsc-extension"></a><span data-ttu-id="921e7-129">Extension DSC.</span><span class="sxs-lookup"><span data-stu-id="921e7-129">DSC Extension.</span></span>
      {
          "publisher": "Microsoft.Powershell",
          "type": "DSC",
          "typeHandlerVersion": "2.1(Recommendation is to use the latest version)",
          "settings": {
              "ModulesUrl": "https://UrlToZipContainingConfigurationScript.ps1.zip",
              "SasToken": "Optional : SAS Token if ModulesUrl points to Azure Blob Storage",
              "ConfigurationFunction": "ConfigurationScript.ps1\\ConfigurationFunction",
              "Properties": {
                  "ParameterToConfigurationFunction1": "Value1",
                  "ParameterToConfigurationFunction2": "Value2",
                  "ParameterOfTypePSCredential1": {
                      "UserName": "UsernameValue1",
                      "Password": "PrivateSettingsRef:Key1(Value is a reference to a member of the Items object in the protected settings)"
                  },
                  "ParameterOfTypePSCredential2": {
                      "UserName": "UsernameValue2",
                      "Password": "PrivateSettingsRef:Key2"
                  }
              }
          },
          "protectedSettings": {
              "Items": {
                  "Key1": "PasswordValue1",
                  "Key2": "PasswordValue2"
              },
              "DataBlobUri": "optional : https: //UrlToConfigurationData.psd1"
          }
      }


### <a name="symantec-endpoint-protection"></a><span data-ttu-id="921e7-130">Symantec Endpoint Protection.</span><span class="sxs-lookup"><span data-stu-id="921e7-130">Symantec Endpoint Protection.</span></span>
      {
        "publisher": "SymantecEndpointProtection",
        "type": "Symantec",
        "typeHandlerVersion": "12.1",
        "settings": {}
      }

### <a name="trend-micro-deep-security-agent"></a><span data-ttu-id="921e7-131">Agent Trend Micro Deep Security.</span><span class="sxs-lookup"><span data-stu-id="921e7-131">Trend Micro Deep Security Agent.</span></span>
      {
        "publisher": "TrendMicro.DeepSecurity",
        "type": "TrendMicroDSA",
        "typeHandlerVersion": "9.6",
        "settings": {
          "ManagerAddress" : "Enter the externally accessible DNS name or IP address of the Deep Security Manager. Please enter \"agents.deepsecurity.trendmicro.com\" if using Deep Security as a Service",

          "ActivationPort" : "Enter the port number of the Deep Security Manager, default value - 443",

          "TenantIdentifier" : "Enter the tenant ID, which is a hyphenated, 36-character string available in the Deployment Scripts dialog box in the Deep Security console. This parameter is mandatory if using Deep Security as a Service, or a multi-tenant installation of Deep Security Manager. Type NA if using a non multi-tenant installation of Deep Security Manager.",

          "TenantActivationPassword" : "Enter the tenant activation password, which is a hyphenated, 36-character string available in the Deployment Scripts dialog box in the Deep Security console. This parameter is mandatory if using Deep Security as a Service, or a multi-tenant installation of Deep Security Manager. Type NA if using a non multi-tenant installation of Deep Security Manager.",

          "SecurityPolicy" : "Optional : Enter the name or numeric ID of the security policy defined in the Deep Security Manager which will be applied on agent activation to protect this virtual machine (recommended). No security policy will be applied to the virtual machine if this parameter is blank. This parameter is optional if using Deep Security as a Service."
        }
      }

### <a name="vormertric-transparent-encryption-agent"></a><span data-ttu-id="921e7-132">Agent Vormertric Transparent Encryption.</span><span class="sxs-lookup"><span data-stu-id="921e7-132">Vormertric Transparent Encryption Agent.</span></span>
            {
              "publisher": "Vormetric",
              "type": "VormetricTransparentEncryptionAgent",
              "typeHandlerVersion": "5.2",
              "settings": {
              }
            }

### <a name="puppet-enterprise-agent"></a><span data-ttu-id="921e7-133">Agent Puppet Enterprise.</span><span class="sxs-lookup"><span data-stu-id="921e7-133">Puppet Enterprise Agent.</span></span>
            {
              "publisher": "PuppetLabs",
              "type": "PuppetEnterpriseAgent",
              "typeHandlerVersion": "3.2",
              "settings": {
                "puppet_master_server" : "Puppet Master Server Name"
              }
            }  

### <a name="microsoft-monitoring-agent-for-azure-operational-insights"></a><span data-ttu-id="921e7-134">Agent Microsoft Monitoring pour Azure Operational Insights</span><span class="sxs-lookup"><span data-stu-id="921e7-134">Microsoft Monitoring Agent for Azure Operational Insights</span></span>
            {
              "publisher": "Microsoft.EnterpriseCloud.Monitoring",
              "type": "MicrosoftMonitoringAgent",
              "typeHandlerVersion": "1.0",
              "settings": {
                "workspaceId" : "The Workspace ID is available from within the Direct Agent Configuration section of the Azure Operational Insights portal"
              }
              "protectedSettings": {
                "workspaceKey"  : "The Workspace Key is a string that is available from within the Direct Agent Configuration section of the Azure Operational Insights portal"
              }
              }
            }

### <a name="mcafee-endpointsecurity"></a><span data-ttu-id="921e7-135">McAfee EndpointSecurity</span><span class="sxs-lookup"><span data-stu-id="921e7-135">McAfee EndpointSecurity</span></span>
            {
              "publisher": "McAfee.EndpointSecurity",
              "type": "McAfeeEndpointSecurity",
              "typeHandlerVersion": "6.0",
              "settings": {
                "entitlementKey" : "Optional : Enter a valid entitlement key or leave blank for trial version",
                "featureVS"      : "Choose whether or not to install the Virus and Spyware Protection features : true|false",
                "featureBP"      : "Choose whether or not to install the Browser Protection feature : true|false",
                "featureFW"      : "Choose whether or not to install the Firewall Protection feature :true|false",
                "relayServer"    : "Allows VMs on the local subnet to receive updates through this VM when they are not connected to the internet : true|false"
              }
            }

### <a name="azure-iaas-antimalware"></a><span data-ttu-id="921e7-136">Logiciel anti-programme malveillant IaaS Azure</span><span class="sxs-lookup"><span data-stu-id="921e7-136">Azure IaaS Antimalware</span></span>
          {
            "publisher": "Microsoft.Azure.Security",
            "type": "IaaSAntimalware",
            "typeHandlerVersion": "1.2",
            "settings": {
              "AntimalwareEnabled": "true",
              "ExclusionsPaths"        : "Optional : ExclusionsPaths",
              "ExclusionsExtensions"   : "Optional : ExclusionsExtensions",
              "ExclusionsProcesses"   : "Optional : ExclusionsProcesses",
              "RealtimeProtectionEnabled"   : "Optional : True|False",
              "ScheduledScanSettingsIsEnabled"   : "Optional : True|False",
              "ScheduledScanSettingsScanType"   : "Optional : Quick|Full",
              "ScheduledScanSettingsDay"   : "Optional : Sunday-Saturday",
              "ScheduledScanSettingsTime"   : "Optional : When to perform the scheduled scan, measured in minutes from midnight,0-1440"
            }
          }

### <a name="eset-file-security"></a><span data-ttu-id="921e7-137">ESET File Security</span><span class="sxs-lookup"><span data-stu-id="921e7-137">ESET File Security</span></span>
          {
            "publisher": "ESET",
            "type": "FileSecurity",
            "typeHandlerVersion": "6.0",
            "settings": {
            }
          }

### <a name="datadog-agent"></a><span data-ttu-id="921e7-138">Agent Datadog</span><span class="sxs-lookup"><span data-stu-id="921e7-138">Datadog Agent</span></span>
          {
            "publisher": "Datadog.Agent",
            "type": "DatadogWindowsAgent",
            "typeHandlerVersion": "0.5",
            "settings": {
              "api_key" : "API Key from https://app.datadoghq.com/account/settings#api"
            }
          }

### <a name="confer-advanced-threat-prevention-and-incident-response-for-azure"></a><span data-ttu-id="921e7-139">Confer Advanced Threat Prevention and Incident Response pour Azure</span><span class="sxs-lookup"><span data-stu-id="921e7-139">Confer Advanced Threat Prevention and Incident Response for Azure</span></span>
          {
            "publisher": "Confer",
            "type": "ConferForAzure",
            "typeHandlerVersion": "1.0",
            "settings": {
              "ConferRegisterCode" : "Optional : Valid product registration code or leave it blank to register later",
              "ConferRegisterCode" : "Enter a valid server name if your account requires a dedicated confer backend server or leave it blank"
            }
          }

### <a name="cloudlink-securevm-agent"></a><span data-ttu-id="921e7-140">Agent CloudLink SecureVM</span><span class="sxs-lookup"><span data-stu-id="921e7-140">CloudLink SecureVM Agent</span></span>
          {
            "publisher": "CloudLinkEMC.SecureVM",
            "type": "CloudLinkSecureVMWindowsAgent",
            "typeHandlerVersion": "4.0",
            "settings": {
              "CloudLinkCenter" : "specify valid IP/FQDN to CloudLinkCenter"
            }
          }

### <a name="barracuda-vpn-connectivity-agent-for-microsoft-azure"></a><span data-ttu-id="921e7-141">Agent Barracuda VPN Connectivity pour Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="921e7-141">Barracuda VPN Connectivity Agent for Microsoft Azure</span></span>
          {
            "publisher": "Barracuda.Azure.ConnectivityAgent",
            "type": "BarracudaConnectivityAgent",
            "typeHandlerVersion": "3.5",
            "settings": {
              "ServerAddress" : "Host name or IP address of the VPN server - AES, AES256, Blowfish,CAST,DES,3DES,None",
              "EncryptionAlgorithm" : "Algorithm used to encrypt VPN traffic - MD5,SHA1,SHA256,None",
              "PKCS12File" : "Url for file containing certificate and private key used to authenticate against the VPN server",
              "PKCS12FilePassword" : "Password for the file containing certificate and private key"
            }
          }

### <a name="alert-logic-log-manager"></a><span data-ttu-id="921e7-142">Alert Logic Log Manager</span><span class="sxs-lookup"><span data-stu-id="921e7-142">Alert Logic Log Manager</span></span>
          {
            "publisher": "AlertLogic.Extension",
            "type": "AlertLogicLM",
            "typeHandlerVersion": "1.9",
            "settings": {
              "registrationKey" : " Alert Logic Log Manager registration key"
            }
          }

### <a name="chef-agent"></a><span data-ttu-id="921e7-143">Agent Chef</span><span class="sxs-lookup"><span data-stu-id="921e7-143">Chef Agent</span></span>
          {
            "publisher": "Chef.Bootstrap.WindowsAzure",
            "type": "ChefClient",
            "typeHandlerVersion": "1210.12",
            "settings": {
              "validation_key" : " Validation key",
              "client_rb" : "client_rb file",
              "runlist" : "Optional runlist"
            }
          }

### <a name="azure-diagnostics"></a><span data-ttu-id="921e7-144">Azure Diagnostics</span><span class="sxs-lookup"><span data-stu-id="921e7-144">Azure Diagnostics</span></span>
<span data-ttu-id="921e7-145">Pour plus d’informations sur la configuration des diagnostics, consultez la section [Extension des diagnostics Azure](extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="921e7-145">For more details about how to configure diagnostics, see [Azure Diagnostics Extension](extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

          {
            "publisher": "Microsoft.Azure.Diagnostics",
            "type": "IaaSDiagnostics",
            "typeHandlerVersion": "1.5",
            "autoUpgradeMinorVersion": true,
            "settings": {
              "xmlCfg": "[base64(variables('wadcfgx'))]",
              "storageAccount": "[parameters('diagnosticsStorageAccount')]"
            },
            "protectedSettings": {
            "storageAccountName": "[parameters('diagnosticsStorageAccount')]",
            "storageAccountKey": "[listkeys(variables('accountid'), '2015-05-01-preview').key1]",
            "storageAccountEndPoint": "https://core.windows.net"
          }
          }

### <a name="octopus-deploy-tentacle-agent"></a><span data-ttu-id="921e7-146">Agent Tentacle Octopus Deploy</span><span class="sxs-lookup"><span data-stu-id="921e7-146">Octopus Deploy Tentacle Agent</span></span>

<span data-ttu-id="921e7-147">Pour plus d’informations sur la configuration de Tentacle Octopus Deploy sur Azure, consultez la [documentation Octopus](https://octopus.com/docs/installation/installing-tentacles/azure-virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="921e7-147">For more details about how to configure the Octopus Deploy Tentacle on Azure, see the [Octopus Documentation](https://octopus.com/docs/installation/installing-tentacles/azure-virtual-machines).</span></span>

          {
            "publisher": "OctopusDeploy.Tentacle",
            "type": "OctopusDeployWindowsTentacle",
            "typeHandlerVersion": "2.0",
            "autoUpgradeMinorVersion": "true",
            "settings": {
              "OctopusServerUrl": "(string, required) The url to the Octopus server portal.",
              "Environments": [ "(array of strings, required) The environments to which the Tentacle should be added." ],
              "Roles": [ "(array of strings, required) The roles to assign to the Tentacle." ],
              "CommunicationMode": "(string, required) Whether the Tentacle should wait for connections from the server ('Listen') or should poll the server ('Poll').",
              "Port": (int, required) The port to listen on for connections from the server (in 'Listen' mode), or the port on which to connect to the Octopus server ('Poll' mode).,
              "PublicHostNameConfiguration": "(string, optional) If in listening mode, how the server should contact the Tentacle. Can be 'PublicIP', 'FQDN', 'ComputerName' or 'Custom'. Defaults to 'PublicIp'.",
              "CustomPublicHostName": "(string, optional) If in listening mode, and 'PublicHostNameConfiguration' is set to 'Custom', the address that the server should use for this Tentacle.",
              "MachinePolicy": "(string, optional) The Machine Policy to assign to the Tentacle. If not specified, uses the default Machine Policy.",
              "Tenants": [ "(array of strings, optional) The tenants to assign to the Tentacle. The tenants feature must be enabled on the Octopus Server." ],
              "TenantTags": [ "(array of strings, optional) The tenant tags to assign to the Tentacle, in the format 'TagSet/TagName'. The tenants feature must be enabled on the Octopus Server." ]
            },
            "protectedSettings": {
              "ApiKey": "(string, required) The Api Key to use to connect to the Octopus server."
            }
          }

<span data-ttu-id="921e7-148">Dans les exemples ci-dessus, remplacez le numéro de version par le dernier numéro de version.</span><span class="sxs-lookup"><span data-stu-id="921e7-148">In the examples above, replace the version number with the latest version number.</span></span>

<span data-ttu-id="921e7-149">Voici un exemple de modèle de machine virtuelle complet avec l’extension de script personnalisé.</span><span class="sxs-lookup"><span data-stu-id="921e7-149">Here is an example of a full VM template with Custom Script Extension.</span></span>

[<span data-ttu-id="921e7-150">Extension de script personnalisé sur une machine virtuelle Windows</span><span class="sxs-lookup"><span data-stu-id="921e7-150">Custom Script Extension on a Windows VM</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/b1908e74259da56a92800cace97350af1f1fc32b/201-list-storage-keys-windows-vm/azuredeploy.json/)

