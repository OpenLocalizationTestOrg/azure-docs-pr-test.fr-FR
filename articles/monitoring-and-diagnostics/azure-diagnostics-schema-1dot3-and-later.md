---
title: "Schéma de configuration de l’Extension Microsoft Azure Diagnostics 1.3 et versions ultérieures | Documents Microsoft"
description: "Schéma version 1.3 et versions ultérieures pour les diagnostics Azure fournis avec le kit Microsoft Azure SDK 2.4 et versions ultérieures."
services: monitoring-and-diagnostics
documentationcenter: .net
author: rboucher
manager: carmonm
editor: 
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/15/2017
ms.author: robb
ms.openlocfilehash: 0d814825fb08452238a254ccd30bde230380c74c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-diagnostics-13-and-later-configuration-schema"></a><span data-ttu-id="3de67-103">Schéma de configuration de Microsoft Azure Diagnostics 1.3 et versions ultérieures</span><span class="sxs-lookup"><span data-stu-id="3de67-103">Azure Diagnostics 1.3 and later configuration schema</span></span>
> [!NOTE]
> <span data-ttu-id="3de67-104">L’Extension Microsoft Azure Diagnostics est le composant utilisé pour collecter les compteurs de performances et d’autres statistiques à partir de :</span><span class="sxs-lookup"><span data-stu-id="3de67-104">The Azure Diagnostics extension is the component used to collect performance counters and other statistics from:</span></span>
> - <span data-ttu-id="3de67-105">Azure Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="3de67-105">Azure Virtual Machines</span></span> 
> - <span data-ttu-id="3de67-106">Jeux de mise à l’échelle de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="3de67-106">Virtual Machine Scale Sets</span></span>
> - <span data-ttu-id="3de67-107">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="3de67-107">Service Fabric</span></span> 
> - <span data-ttu-id="3de67-108">Services cloud</span><span class="sxs-lookup"><span data-stu-id="3de67-108">Cloud Services</span></span> 
> - <span data-ttu-id="3de67-109">Groupes de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="3de67-109">Network Security Groups</span></span>
> 
> <span data-ttu-id="3de67-110">Cette page vous concerne uniquement si vous utilisez l’un de ces services.</span><span class="sxs-lookup"><span data-stu-id="3de67-110">This page is only relevant if you are using one of these services.</span></span>

<span data-ttu-id="3de67-111">Cette page a trait aux versions 1.3 et ultérieures (Azure SDK 2.4 et ultérieur).</span><span class="sxs-lookup"><span data-stu-id="3de67-111">This page is valid for versions 1.3 and newer (Azure SDK 2.4 and newer).</span></span> <span data-ttu-id="3de67-112">Les sections de configuration les plus récentes sont commentées pour montrer dans quelle version elles ont été ajoutées.</span><span class="sxs-lookup"><span data-stu-id="3de67-112">Newer configuration sections are commented to show in what version they were added.</span></span>  

<span data-ttu-id="3de67-113">Le fichier de configuration décrit ici est utilisé pour définir les paramètres de configuration de diagnostic lorsque le moniteur de diagnostic démarre.</span><span class="sxs-lookup"><span data-stu-id="3de67-113">The configuration file described here is used to set diagnostic configuration settings when the diagnostics monitor starts.</span></span>  

<span data-ttu-id="3de67-114">L’extension est utilisée conjointement avec d’autres produits de diagnostic Microsoft tels qu’Azure Monitor, Application Insights et Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="3de67-114">The extension is used in conjunction with other Microsoft diagnostics products like Azure Monitor, Application Insights, and Log Analytics.</span></span>



<span data-ttu-id="3de67-115">Téléchargez la définition de schéma de fichier de configuration publique en exécutant la commande PowerShell suivante :</span><span class="sxs-lookup"><span data-stu-id="3de67-115">Download the public configuration file schema definition by executing the following PowerShell command:</span></span>  

```powershell  
(Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File –Encoding utf8 -FilePath 'C:\temp\WadConfig.xsd'  
```  

<span data-ttu-id="3de67-116">Pour plus d’informations sur l’utilisation d’Azure Diagnostics, voir [Extension Microsoft Azure Diagnostics](azure-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="3de67-116">For more information about using Azure Diagnostics, see [Azure Diagnostics Extension](azure-diagnostics.md).</span></span>  

## <a name="example-of-the-diagnostics-configuration-file"></a><span data-ttu-id="3de67-117">Exemple du fichier de configuration des diagnostics</span><span class="sxs-lookup"><span data-stu-id="3de67-117">Example of the diagnostics configuration file</span></span>  
 <span data-ttu-id="3de67-118">L’exemple suivant montre un fichier de configuration de diagnostic standard :</span><span class="sxs-lookup"><span data-stu-id="3de67-118">The following example shows a typical diagnostics configuration file:</span></span>  

```xml  
<?xml version="1.0" encoding="utf-8"?>  
<DiagnosticsConfiguration  xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">   
  <PublicConfig>  
    <WadCfg>  
      <DiagnosticMonitorConfiguration overallQuotaInMB="10000">  

        <PerformanceCounters scheduledTransferPeriod="PT1M">  
          <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT1M" unit="percent" />  
        </PerformanceCounters>  

        <Directories scheduledTransferPeriod="PT5M">  
          <IISLogs containerName="iislogs" />  
          <FailedRequestLogs containerName="iisfailed" />  

          <DataSources>  
            <DirectoryConfiguration containerName="mynewprocess">  
              <Absolute path="C:\MyNewProcess" expandEnvironment="false" />  
            </DirectoryConfiguration>  
            <DirectoryConfiguration containerName="badapp">  
              <Absolute path="%SYSTEMDRIVE%\BadApp" expandEnvironment="true" />  
            </DirectoryConfiguration>  
            <DirectoryConfiguration containerName="goodapp">  
              <LocalResource name="Skippy" relativePath="..\PeanutButter"/>  
            </DirectoryConfiguration>  
          </DataSources>  

        </Directories>  

        <EtwProviders>  
          <EtwEventSourceProviderConfiguration   
                       provider="MyProviderClass"   
                       scheduledTransferPeriod="PT5M">  
            <Event id="0"/>  
            <Event id="1" eventDestination="errorTable"/>  
            <DefaultEvents />  
          </EtwEventSourceProviderConfiguration>  
          <EtwManifestProviderConfiguration provider="5974b00b-84c2-44bc-9e58-3a2451b4e3ad" scheduledTransferLogLevelFilter="Information" scheduledTransferPeriod="PT2M">  
            <Event id="0"/>  
            <DefaultEvents eventDestination="defaultTable"/>  
          </EtwManifestProviderConfiguration>  
        </EtwProviders>  

        <WindowsEventLog scheduledTransferPeriod="PT5M">  
          <DataSource name="System!*[System[Provider[@Name='Microsoft Antimalware']]]"/>  
          <DataSource name="System!*[System[Provider[@Name='NTFS'] and (EventID=55)]]" />  
          <DataSource name="System!*[System[Provider[@Name='disk'] and (EventID=7 or EventID=52 or EventID=55)]]" />  
        </WindowsEventLog>  

        <Logs  bufferQuotaInMB="1024"   
             scheduledTransferPeriod="PT1M"   
             scheduledTransferLogLevelFilter="Verbose"   
             sinks="ApplicationInsights.AppLogs"/>  <!-- sinks attribute added in 1.5 -->  

        <CrashDumps containerName="wad-crashdumps" directoryQuotaPercentage="30" dumpType="Mini">  
          <CrashDumpConfiguration processName="mynewprocess.exe" />  
          <CrashDumpConfiguration processName="badapp.exe"/>  
        </CrashDumps>  

        <DockerSources> <!-- Added in 1.9 --> 
          <Stats enabled="true" sampleRate="PT1M" scheduledTransferPeriod="PT1M" />
        </DockerSources>

      </DiagnosticMonitorConfiguration>  

      <SinksConfig>   <!-- Added in 1.5 -->  
        <Sink name="ApplicationInsights">   
          <ApplicationInsights>{Insert InstrumentationKey}</ApplicationInsights>   
          <Channels>   
            <Channel logLevel="Error" name="Errors"  />   
            <Channel logLevel="Verbose" name="AppLogs"  />   
          </Channels>   
        </Sink>   
        <Sink name="EventHub"> <!-- Added in 1.7 -->
          <EventHub Url="https://myeventhub-ns.servicebus.windows.net/diageventhub" SharedAccessKeyName="SendRule" usePublisherId="false" />
        </Sink>
        <Sink name="secondaryEventHub"> <!-- Added in 1.7 -->
          <EventHub Url="https://myeventhub-ns.servicebus.windows.net/secondarydiageventhub" SharedAccessKeyName="SendRule" usePublisherId="false" />
        </Sink>
        <Sink name="secondaryStorageAccount"> <!-- Added in 1.7 -->
          <StorageAccount name="secondarydiagstorageaccount" endpoint="https://core.windows.net" />
        </Sink>
   </SinksConfig>

  </WadCfg>  

  <StorageAccount>diagstorageaccount</StorageAccount>
  <StorageType>TableAndBlob</StorageType> <!-- Added in 1.8 -->  
  </PublicConfig>  

  <PrivateConfig>  <!-- Added in 1.3 -->  
    <StorageAccount name="" key="" endpoint="" sasToken="{sas token}"  />  <!-- sasToken in Private config added in 1.8.1 -->  
    <EventHub Url="https://myeventhub-ns.servicebus.windows.net/diageventhub" SharedAccessKeyName="SendRule" SharedAccessKey="{base64 encoded key}" />
   
    <SecondaryStorageAccounts>
       <StorageAccount name="secondarydiagstorageaccount" key="{base64 encoded key}" endpoint="https://core.windows.net" sasToken="{sas token}" />
    </SecondaryStorageAccounts>
   
    <SecondaryEventHubs>
       <EventHub Url="https://myeventhub-ns.servicebus.windows.net/secondarydiageventhub" SharedAccessKeyName="SendRule" SharedAccessKey="{base64 encoded key}" />
    </SecondaryEventHubs>

  </PrivateConfig>  
  <IsEnabled>true</IsEnabled>  
</DiagnosticsConfiguration>  

```  

<span data-ttu-id="3de67-119">Équivalent JSON du fichier de configuration XML précédent.</span><span class="sxs-lookup"><span data-stu-id="3de67-119">JSON equivalent of the previous XML configuration file.</span></span> 

<span data-ttu-id="3de67-120">Les éléments PublicConfig et PrivateConfig sont séparés car, dans la plupart des cas d’utilisation de json, ils sont transmis en tant que variables différentes.</span><span class="sxs-lookup"><span data-stu-id="3de67-120">The PublicConfig and PrivateConfig are separated because in most json usage cases, they are passed as different variables.</span></span> <span data-ttu-id="3de67-121">Ces cas incluent les modèles Resource Manager, le groupe de machines virtuelles identiques PowerShell et Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3de67-121">These cases include Resource Manager templates, Virtual Machine Scale set PowerShell, and Visual Studio.</span></span> 

```json
"PublicConfig" {
    "WadCfg": {
        "DiagnosticMonitorConfiguration": {
            "overallQuotaInMB": 10000,
            "DiagnosticInfrastructureLogs": {
                "scheduledTransferLogLevelFilter": "Error"
            },
            "PerformanceCounters": {
                "scheduledTransferPeriod": "PT1M",
                "PerformanceCounterConfiguration": [
                    {
                        "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
                        "sampleRate": "PT1M",
                        "unit": "percent"
                    }
                ]
            },
            "Directories": {
                "scheduledTransferPeriod": "PT5M",
                "IISLogs": {
                    "containerName": "iislogs"
                },
                "FailedRequestLogs": {
                    "containerName": "iisfailed"
                },
                "DataSources": [
                    {
                        "containerName": "mynewprocess",
                        "Absolute": {
                            "path": "C:\\MyNewProcess",
                            "expandEnvironment": false
                        }
                    },
                    {
                        "containerName": "badapp",
                        "Absolute": {
                            "path": "%SYSTEMDRIVE%\\BadApp",
                            "expandEnvironment": true
                        }
                    },
                    {
                        "containerName": "goodapp",
                        "LocalResource": {
                            "relativePath": "..\\PeanutButter",
                            "name": "Skippy"
                        }
                    }
                ]
            },
            "EtwProviders": {
                "sinks": "",
                "EtwEventSourceProviderConfiguration": [
                    {
                        "scheduledTransferPeriod": "PT5M",
                        "provider": "MyProviderClass",
                        "Event": [
                            {
                                "id": 0
                            },
                            {
                                "id": 1,
                                "eventDestination": "errorTable"
                            }
                        ],
                        "DefaultEvents": {
                        }
                    }
                ],
                "EtwManifestProviderConfiguration": [
                    {
                        "scheduledTransferPeriod": "PT2M",
                        "scheduledTransferLogLevelFilter": "Information",
                        "provider": "5974b00b-84c2-44bc-9e58-3a2451b4e3ad",
                        "Event": [
                            {
                                "id": 0
                            }
                        ],
                        "DefaultEvents": {
                        }
                    }
                ]
            },
            "WindowsEventLog": {
                "scheduledTransferPeriod": "PT5M",
                "DataSource": [
                    {
                        "name": "System!*[System[Provider[@Name='Microsoft Antimalware']]]"
                    },
                    {
                        "name": "System!*[System[Provider[@Name='NTFS'] and (EventID=55)]]"
                    },
                    {
                        "name": "System!*[System[Provider[@Name='disk'] and (EventID=7 or EventID=52 or EventID=55)]]"
                    }
                ]
            },
            "Logs": {
                "scheduledTransferPeriod": "PT1M",
                "scheduledTransferLogLevelFilter": "Verbose",
                "sinks": "ApplicationInsights.AppLogs"
            },
            "CrashDumps": {
                "directoryQuotaPercentage": 30,
                "dumpType": "Mini",
                "containerName": "wad-crashdumps",
                "CrashDumpConfiguration": [
                    {
                        "processName": "mynewprocess.exe"
                    },
                    {
                        "processName": "badapp.exe"
                    }
                ]
            }
        },
        "SinksConfig": {
            "Sink": [
                {
                    "name": "ApplicationInsights",
                    "ApplicationInsights": "{Insert InstrumentationKey}",
                    "Channels": {
                        "Channel": [
                            {
                                "logLevel": "Error",
                                "name": "Errors"
                            },
                            {
                                "logLevel": "Verbose",
                                "name": "AppLogs"
                            }
                        ]
                    }
                },
                {
                    "name": "EventHub",
                    "EventHub": {
                        "Url": "https://myeventhub-ns.servicebus.windows.net/diageventhub",
                        "SharedAccessKeyName": "SendRule",
                        "usePublisherId": false
                    }
                },
                {
                    "name": "secondaryEventHub",
                    "EventHub": {
                        "Url": "https://myeventhub-ns.servicebus.windows.net/secondarydiageventhub",
                        "SharedAccessKeyName": "SendRule",
                        "usePublisherId": false
                    }
                },
                {
                    "name": "secondaryStorageAccount",
                    "StorageAccount": {
                        "name": "secondarydiagstorageaccount",
                        "endpoint": "https://core.windows.net"
                    }
                }
            ]
        }
    },
    "StorageAccount": "diagstorageaccount",
    "StorageType": "TableAndBlob"
}
```

```json
"PrivateConfig" {
    "storageAccountName": "diagstorageaccount",
    "storageAccountKey": "{base64 encoded key}",
    "storageAccountEndPoint": "https://core.windows.net",
    "storageAccountSasToken": "{sas token}",
    "EventHub": {
        "Url": "https://myeventhub-ns.servicebus.windows.net/diageventhub",
        "SharedAccessKeyName": "SendRule",
        "SharedAccessKey": "{base64 encoded key}"
    },
    "SecondaryStorageAccounts": {
        "StorageAccount": [
            {
                "name": "secondarydiagstorageaccount",
                "key": "{base64 encoded key}",
                "endpoint": "https://core.windows.net",
                "sasToken": "{sas token}"
            }
        ]
    },
    "SecondaryEventHubs": {
        "EventHub": [
            {
                "Url": "https://myeventhub-ns.servicebus.windows.net/secondarydiageventhub",
                "SharedAccessKeyName": "SendRule",
                "SharedAccessKey": "{base64 encoded key}"
            }
        ]
    }
}

```

## <a name="reading-this-page"></a><span data-ttu-id="3de67-122">Lecture de cette page</span><span class="sxs-lookup"><span data-stu-id="3de67-122">Reading this page</span></span>  
 <span data-ttu-id="3de67-123">Les balises suivantes sont à peu près dans l’ordre indiqué dans l’exemple précédent.</span><span class="sxs-lookup"><span data-stu-id="3de67-123">The tags following are roughly in order shown in the preceding example.</span></span>  <span data-ttu-id="3de67-124">Si vous ne voyez pas de description complète à l’emplacement prévu, recherchez l’élément ou l’attribut dans la page.</span><span class="sxs-lookup"><span data-stu-id="3de67-124">If you don't see a full description where you expect it, search the page for the element or attribute.</span></span>  

## <a name="common-attribute-types"></a><span data-ttu-id="3de67-125">Types d’attributs courants</span><span class="sxs-lookup"><span data-stu-id="3de67-125">Common Attribute Types</span></span>  
 <span data-ttu-id="3de67-126">L’attribut **scheduledTransferPeriod** apparaît dans plusieurs éléments.</span><span class="sxs-lookup"><span data-stu-id="3de67-126">**scheduledTransferPeriod** attribute appears in several elements.</span></span> <span data-ttu-id="3de67-127">Il s’agit de l’intervalle entre les transferts planifiés vers le stockage Azure, arrondi à la minute la plus proche.</span><span class="sxs-lookup"><span data-stu-id="3de67-127">It is the interval between scheduled transfers to storage rounded up to the nearest minute.</span></span> <span data-ttu-id="3de67-128">La valeur est un [« Type de données de durée » XML.](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="3de67-128">The value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span>


## <a name="diagnosticsconfiguration-element"></a><span data-ttu-id="3de67-129">Élément DiagnosticsConfiguration</span><span class="sxs-lookup"><span data-stu-id="3de67-129">DiagnosticsConfiguration Element</span></span>  
 <span data-ttu-id="3de67-130">*Tree: Root - DiagnosticsConfiguration*</span><span class="sxs-lookup"><span data-stu-id="3de67-130">*Tree: Root - DiagnosticsConfiguration*</span></span>

<span data-ttu-id="3de67-131">Ajouté à la version 1.3.</span><span class="sxs-lookup"><span data-stu-id="3de67-131">Added in version 1.3.</span></span>  

<span data-ttu-id="3de67-132">Élément de niveau supérieur du fichier de configuration de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="3de67-132">The top-level element of the diagnostics configuration file.</span></span>  

<span data-ttu-id="3de67-133">**Attribute**  xmlns - L’espace de noms XML du fichier de configuration des diagnostics est :</span><span class="sxs-lookup"><span data-stu-id="3de67-133">**Attribute**  xmlns - The XML namespace for the diagnostics configuration file is:</span></span>  
<span data-ttu-id="3de67-134">http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration</span><span class="sxs-lookup"><span data-stu-id="3de67-134">http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration</span></span>  


|<span data-ttu-id="3de67-135">Éléments enfants</span><span class="sxs-lookup"><span data-stu-id="3de67-135">Child Elements</span></span>|<span data-ttu-id="3de67-136">Description</span><span class="sxs-lookup"><span data-stu-id="3de67-136">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="3de67-137">**PublicConfig**</span><span class="sxs-lookup"><span data-stu-id="3de67-137">**PublicConfig**</span></span>|<span data-ttu-id="3de67-138">Obligatoire.</span><span class="sxs-lookup"><span data-stu-id="3de67-138">Required.</span></span> <span data-ttu-id="3de67-139">Consultez la description sur cette page.</span><span class="sxs-lookup"><span data-stu-id="3de67-139">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="3de67-140">**PrivateConfig**</span><span class="sxs-lookup"><span data-stu-id="3de67-140">**PrivateConfig**</span></span>|<span data-ttu-id="3de67-141">facultatif.</span><span class="sxs-lookup"><span data-stu-id="3de67-141">Optional.</span></span> <span data-ttu-id="3de67-142">Consultez la description sur cette page.</span><span class="sxs-lookup"><span data-stu-id="3de67-142">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="3de67-143">**IsEnabled**</span><span class="sxs-lookup"><span data-stu-id="3de67-143">**IsEnabled**</span></span>|<span data-ttu-id="3de67-144">Booléen.</span><span class="sxs-lookup"><span data-stu-id="3de67-144">Boolean.</span></span> <span data-ttu-id="3de67-145">Consultez la description sur cette page.</span><span class="sxs-lookup"><span data-stu-id="3de67-145">See description elsewhere on this page.</span></span>|  

## <a name="publicconfig-element"></a><span data-ttu-id="3de67-146">Élément PublicConfig</span><span class="sxs-lookup"><span data-stu-id="3de67-146">PublicConfig Element</span></span>  
 <span data-ttu-id="3de67-147">*Tree: Root - DiagnosticsConfiguration - PublicConfig*</span><span class="sxs-lookup"><span data-stu-id="3de67-147">*Tree: Root - DiagnosticsConfiguration - PublicConfig*</span></span>

 <span data-ttu-id="3de67-148">Décrit la configuration de diagnostic public.</span><span class="sxs-lookup"><span data-stu-id="3de67-148">Describes the public diagnostics configuration.</span></span>  

|<span data-ttu-id="3de67-149">Éléments enfants</span><span class="sxs-lookup"><span data-stu-id="3de67-149">Child Elements</span></span>|<span data-ttu-id="3de67-150">Description</span><span class="sxs-lookup"><span data-stu-id="3de67-150">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="3de67-151">**WadCfg**</span><span class="sxs-lookup"><span data-stu-id="3de67-151">**WadCfg**</span></span>|<span data-ttu-id="3de67-152">Obligatoire.</span><span class="sxs-lookup"><span data-stu-id="3de67-152">Required.</span></span> <span data-ttu-id="3de67-153">Consultez la description sur cette page.</span><span class="sxs-lookup"><span data-stu-id="3de67-153">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="3de67-154">**StorageAccount**</span><span class="sxs-lookup"><span data-stu-id="3de67-154">**StorageAccount**</span></span>|<span data-ttu-id="3de67-155">Nom du compte de stockage Azure où stocker les données.</span><span class="sxs-lookup"><span data-stu-id="3de67-155">The name of the Azure Storage account to store the data in.</span></span> <span data-ttu-id="3de67-156">Peut également être spécifié en tant que paramètre lors de l’exécution de l’applet de commande Set-AzureServiceDiagnosticsExtension.</span><span class="sxs-lookup"><span data-stu-id="3de67-156">May also be specified as a parameter when executing the Set-AzureServiceDiagnosticsExtension cmdlet.</span></span>|  
|<span data-ttu-id="3de67-157">**StorageType**</span><span class="sxs-lookup"><span data-stu-id="3de67-157">**StorageType**</span></span>|<span data-ttu-id="3de67-158">Peut être *Table*, *Blob* ou *TableAndBlob*.</span><span class="sxs-lookup"><span data-stu-id="3de67-158">Can be *Table*, *Blob*, or *TableAndBlob*.</span></span> <span data-ttu-id="3de67-159">Table est la valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="3de67-159">Table is default.</span></span> <span data-ttu-id="3de67-160">Si TableAndBlob est choisi, les données de diagnostic sont écrites deux fois : une fois pour chaque type.</span><span class="sxs-lookup"><span data-stu-id="3de67-160">When TableAndBlob is chosen, diagnostic data is written twice -- once to each type.</span></span>|  
|<span data-ttu-id="3de67-161">**LocalResourceDirectory**</span><span class="sxs-lookup"><span data-stu-id="3de67-161">**LocalResourceDirectory**</span></span>|<span data-ttu-id="3de67-162">Répertoire se trouvant sur la machine virtuelle sur laquelle Monitoring Agent stocke les données d’événement.</span><span class="sxs-lookup"><span data-stu-id="3de67-162">The directory on the virtual machine where the Monitoring Agent stores event data.</span></span> <span data-ttu-id="3de67-163">S’il n’est pas défini, le répertoire par défaut est utilisé :</span><span class="sxs-lookup"><span data-stu-id="3de67-163">If not, set, the default directory is used:</span></span><br /><br /> <span data-ttu-id="3de67-164">Pour un rôle Worker/web : `C:\Resources\<guid>\directory\<guid>.<RoleName.DiagnosticStore\`</span><span class="sxs-lookup"><span data-stu-id="3de67-164">For a Worker/web role: `C:\Resources\<guid>\directory\<guid>.<RoleName.DiagnosticStore\`</span></span><br /><br /> <span data-ttu-id="3de67-165">Pour une machine virtuelle : `C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<WADVersion>\WAD<WADVersion>`</span><span class="sxs-lookup"><span data-stu-id="3de67-165">For a Virtual Machine: `C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<WADVersion>\WAD<WADVersion>`</span></span><br /><br /> <span data-ttu-id="3de67-166">Les attributs requis sont :</span><span class="sxs-lookup"><span data-stu-id="3de67-166">Required attributes are:</span></span><br /><br /> <span data-ttu-id="3de67-167">- **path** - Répertoire sur le système à utiliser par Azure Diagnostics.</span><span class="sxs-lookup"><span data-stu-id="3de67-167">- **path** - The directory on the system to be used by Azure Diagnostics.</span></span><br /><br /> <span data-ttu-id="3de67-168">- **expandEnvironment** - Contrôle si les variables d’environnement sont développées dans le nom du chemin d’accès.</span><span class="sxs-lookup"><span data-stu-id="3de67-168">- **expandEnvironment** - Controls whether environment variables are expanded in the path name.</span></span>|  

## <a name="wadcfg-element"></a><span data-ttu-id="3de67-169">WadCFG Element</span><span class="sxs-lookup"><span data-stu-id="3de67-169">WadCFG Element</span></span>  
 <span data-ttu-id="3de67-170">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG*</span><span class="sxs-lookup"><span data-stu-id="3de67-170">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG*</span></span>
 
 <span data-ttu-id="3de67-171">Identifie et configure les données de télémétrie à collecter.</span><span class="sxs-lookup"><span data-stu-id="3de67-171">Identifies and configures the telemetry data to be collected.</span></span>  


## <a name="diagnosticmonitorconfiguration-element"></a><span data-ttu-id="3de67-172">Élément DiagnosticMonitorConfiguration</span><span class="sxs-lookup"><span data-stu-id="3de67-172">DiagnosticMonitorConfiguration Element</span></span> 
 <span data-ttu-id="3de67-173">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration*</span><span class="sxs-lookup"><span data-stu-id="3de67-173">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration*</span></span>

 <span data-ttu-id="3de67-174">Requis</span><span class="sxs-lookup"><span data-stu-id="3de67-174">Required</span></span> 

|<span data-ttu-id="3de67-175">Attributs</span><span class="sxs-lookup"><span data-stu-id="3de67-175">Attributes</span></span>|<span data-ttu-id="3de67-176">Description</span><span class="sxs-lookup"><span data-stu-id="3de67-176">Description</span></span>|  
|----------------|-----------------|  
| <span data-ttu-id="3de67-177">**overallQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="3de67-177">**overallQuotaInMB**</span></span> | <span data-ttu-id="3de67-178">Quantité maximale d’espace disque local pouvant être utilisé par les différents types de données de diagnostic collectés par Azure Diagnostics.</span><span class="sxs-lookup"><span data-stu-id="3de67-178">The maximum amount of local disk space that may be consumed by the various types of diagnostic data collected by Azure Diagnostics.</span></span> <span data-ttu-id="3de67-179">Le paramètre par défaut est 5 210 Mo.</span><span class="sxs-lookup"><span data-stu-id="3de67-179">The default setting is 5120 MB.</span></span><br />
|<span data-ttu-id="3de67-180">**useProxyServer**</span><span class="sxs-lookup"><span data-stu-id="3de67-180">**useProxyServer**</span></span> | <span data-ttu-id="3de67-181">Configurez Azure Diagnostics pour utiliser les paramètres de serveur proxy tels que définis dans les paramètres d’Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="3de67-181">Configure Azure Diagnostics to use the proxy server settings as set in IE settings.</span></span>|  

<br /> <br />

|<span data-ttu-id="3de67-182">Éléments enfants</span><span class="sxs-lookup"><span data-stu-id="3de67-182">Child Elements</span></span>|<span data-ttu-id="3de67-183">Description</span><span class="sxs-lookup"><span data-stu-id="3de67-183">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="3de67-184">**CrashDumps**</span><span class="sxs-lookup"><span data-stu-id="3de67-184">**CrashDumps**</span></span>|<span data-ttu-id="3de67-185">Consultez la description sur cette page.</span><span class="sxs-lookup"><span data-stu-id="3de67-185">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="3de67-186">**DiagnosticInfrastructureLogs**</span><span class="sxs-lookup"><span data-stu-id="3de67-186">**DiagnosticInfrastructureLogs**</span></span>|<span data-ttu-id="3de67-187">Permet la collecte des journaux générés par Azure Diagnostics.</span><span class="sxs-lookup"><span data-stu-id="3de67-187">Enable collection of logs generated by Azure Diagnostics.</span></span> <span data-ttu-id="3de67-188">Les journaux d’infrastructure de diagnostic sont utiles pour le dépannage du système de diagnostic lui-même.</span><span class="sxs-lookup"><span data-stu-id="3de67-188">The diagnostic infrastructure logs are useful for troubleshooting the diagnostics system itself.</span></span> <span data-ttu-id="3de67-189">Les attributs facultatifs sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="3de67-189">Optional attributes are:</span></span><br /><br /> <span data-ttu-id="3de67-190">- **scheduledTransferLogLevelFilter** - Configure le niveau de gravité minimal des journaux collectés.</span><span class="sxs-lookup"><span data-stu-id="3de67-190">- **scheduledTransferLogLevelFilter** - Configures the minimum severity level of the logs collected.</span></span><br /><br /> <span data-ttu-id="3de67-191">- **scheduledTransferPeriod** - Intervalle entre les transferts planifiés vers le stockage Azure, arrondi à la minute la plus proche.</span><span class="sxs-lookup"><span data-stu-id="3de67-191">- **scheduledTransferPeriod** - The interval between scheduled transfers to storage rounded up to the nearest minute.</span></span> <span data-ttu-id="3de67-192">La valeur est un [« Type de données de durée » XML.](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="3de67-192">The value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  
|<span data-ttu-id="3de67-193">**Directories**</span><span class="sxs-lookup"><span data-stu-id="3de67-193">**Directories**</span></span>|<span data-ttu-id="3de67-194">Consultez la description sur cette page.</span><span class="sxs-lookup"><span data-stu-id="3de67-194">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="3de67-195">**EtwProviders**</span><span class="sxs-lookup"><span data-stu-id="3de67-195">**EtwProviders**</span></span>|<span data-ttu-id="3de67-196">Consultez la description sur cette page.</span><span class="sxs-lookup"><span data-stu-id="3de67-196">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="3de67-197">**Métriques**</span><span class="sxs-lookup"><span data-stu-id="3de67-197">**Metrics**</span></span>|<span data-ttu-id="3de67-198">Consultez la description sur cette page.</span><span class="sxs-lookup"><span data-stu-id="3de67-198">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="3de67-199">**PerformanceCounters**</span><span class="sxs-lookup"><span data-stu-id="3de67-199">**PerformanceCounters**</span></span>|<span data-ttu-id="3de67-200">Consultez la description sur cette page.</span><span class="sxs-lookup"><span data-stu-id="3de67-200">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="3de67-201">**WindowsEventLog**</span><span class="sxs-lookup"><span data-stu-id="3de67-201">**WindowsEventLog**</span></span>|<span data-ttu-id="3de67-202">Consultez la description sur cette page.</span><span class="sxs-lookup"><span data-stu-id="3de67-202">See description elsewhere on this page.</span></span>| 
|<span data-ttu-id="3de67-203">**DockerSources**</span><span class="sxs-lookup"><span data-stu-id="3de67-203">**DockerSources**</span></span>|<span data-ttu-id="3de67-204">Consultez la description sur cette page.</span><span class="sxs-lookup"><span data-stu-id="3de67-204">See description elsewhere on this page.</span></span> | 



## <a name="crashdumps-element"></a><span data-ttu-id="3de67-205">Élément CrashDumps</span><span class="sxs-lookup"><span data-stu-id="3de67-205">CrashDumps Element</span></span>  
 <span data-ttu-id="3de67-206">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - CrashDumps*</span><span class="sxs-lookup"><span data-stu-id="3de67-206">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - CrashDumps*</span></span>
 
 <span data-ttu-id="3de67-207">Permet la collecte des vidages sur incident.</span><span class="sxs-lookup"><span data-stu-id="3de67-207">Enable the collection of crash dumps.</span></span>  

|<span data-ttu-id="3de67-208">Attributs</span><span class="sxs-lookup"><span data-stu-id="3de67-208">Attributes</span></span>|<span data-ttu-id="3de67-209">Description</span><span class="sxs-lookup"><span data-stu-id="3de67-209">Description</span></span>|  
|----------------|-----------------|  
|<span data-ttu-id="3de67-210">**containerName**</span><span class="sxs-lookup"><span data-stu-id="3de67-210">**containerName**</span></span>|<span data-ttu-id="3de67-211">facultatif.</span><span class="sxs-lookup"><span data-stu-id="3de67-211">Optional.</span></span> <span data-ttu-id="3de67-212">Nom du conteneur d’objets blob de votre compte de stockage Azure à utiliser pour stocker les vidages sur incident.</span><span class="sxs-lookup"><span data-stu-id="3de67-212">The name of the blob container in your Azure Storage account to be used to store crash dumps.</span></span>|  
|<span data-ttu-id="3de67-213">**crashDumpType**</span><span class="sxs-lookup"><span data-stu-id="3de67-213">**crashDumpType**</span></span>|<span data-ttu-id="3de67-214">facultatif.</span><span class="sxs-lookup"><span data-stu-id="3de67-214">Optional.</span></span>  <span data-ttu-id="3de67-215">Configure Azure Diagnostics pour collecter les mini-vidages sur incident ou les vidages sur incident complets.</span><span class="sxs-lookup"><span data-stu-id="3de67-215">Configures Azure Diagnostics to collect mini or full crash dumps.</span></span>|  
|<span data-ttu-id="3de67-216">**directoryQuotaPercentage**</span><span class="sxs-lookup"><span data-stu-id="3de67-216">**directoryQuotaPercentage**</span></span>|<span data-ttu-id="3de67-217">facultatif.</span><span class="sxs-lookup"><span data-stu-id="3de67-217">Optional.</span></span>  <span data-ttu-id="3de67-218">Configure le pourcentage de **overallQuotaInMB** à réserver pour les vidages sur incident sur la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="3de67-218">Configures the percentage of **overallQuotaInMB** to be reserved for crash dumps on the VM.</span></span>|  

|<span data-ttu-id="3de67-219">Éléments enfants</span><span class="sxs-lookup"><span data-stu-id="3de67-219">Child Elements</span></span>|<span data-ttu-id="3de67-220">Description</span><span class="sxs-lookup"><span data-stu-id="3de67-220">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="3de67-221">**CrashDumpConfiguration**</span><span class="sxs-lookup"><span data-stu-id="3de67-221">**CrashDumpConfiguration**</span></span>|<span data-ttu-id="3de67-222">Obligatoire.</span><span class="sxs-lookup"><span data-stu-id="3de67-222">Required.</span></span> <span data-ttu-id="3de67-223">Définit les valeurs de configuration pour chaque processus.</span><span class="sxs-lookup"><span data-stu-id="3de67-223">Defines configuration values for each process.</span></span><br /><br /> <span data-ttu-id="3de67-224">L’attribut suivant est également requis :</span><span class="sxs-lookup"><span data-stu-id="3de67-224">The following attribute is also required:</span></span><br /><br /> <span data-ttu-id="3de67-225">**processName** - Nom du processus pour lequel vous voulez qu’Azure Diagnostics collecte un vidage sur incident.</span><span class="sxs-lookup"><span data-stu-id="3de67-225">**processName** - The name of the process you want Azure Diagnostics to collect a crash dump for.</span></span>|  

## <a name="directories-element"></a><span data-ttu-id="3de67-226">Élément Directories</span><span class="sxs-lookup"><span data-stu-id="3de67-226">Directories Element</span></span> 
 <span data-ttu-id="3de67-227">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration -  Directories*</span><span class="sxs-lookup"><span data-stu-id="3de67-227">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration -  Directories*</span></span>

 <span data-ttu-id="3de67-228">Permet la collecte du contenu d’un répertoire, des journaux de demandes d’accès ayant échouées IIS et/ou des journaux IIS.</span><span class="sxs-lookup"><span data-stu-id="3de67-228">Enables the collection of the contents of a directory, IIS failed access request logs and/or IIS logs.</span></span>  

 <span data-ttu-id="3de67-229">Attribut **scheduledTransferPeriod** facultatif.</span><span class="sxs-lookup"><span data-stu-id="3de67-229">Optional **scheduledTransferPeriod** attribute.</span></span> <span data-ttu-id="3de67-230">Voir l’explication précédente.</span><span class="sxs-lookup"><span data-stu-id="3de67-230">See explanation earlier.</span></span>  

|<span data-ttu-id="3de67-231">Éléments enfants</span><span class="sxs-lookup"><span data-stu-id="3de67-231">Child Elements</span></span>|<span data-ttu-id="3de67-232">Description</span><span class="sxs-lookup"><span data-stu-id="3de67-232">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="3de67-233">**IISLogs**</span><span class="sxs-lookup"><span data-stu-id="3de67-233">**IISLogs**</span></span>|<span data-ttu-id="3de67-234">Incluez cet élément dans la configuration pour permettre la collecte des journaux IIS :</span><span class="sxs-lookup"><span data-stu-id="3de67-234">Including this element in the configuration enables the collection of IIS logs:</span></span><br /><br /> <span data-ttu-id="3de67-235">**containerName** - Nom du conteneur d’objets blob de votre compte de stockage Azure à utiliser pour stocker les vidages sur incident.</span><span class="sxs-lookup"><span data-stu-id="3de67-235">**containerName** - The name of the blob container in your Azure Storage account to be used to store the IIS logs.</span></span>|   
|<span data-ttu-id="3de67-236">**FailedRequestLogs**</span><span class="sxs-lookup"><span data-stu-id="3de67-236">**FailedRequestLogs**</span></span>|<span data-ttu-id="3de67-237">Incluez cet élément dans la configuration pour permettre la collecte des journaux concernant les demandes ayant échoué sur une application ou un site IIS.</span><span class="sxs-lookup"><span data-stu-id="3de67-237">Including this element in the configuration enables collection of logs about failed requests to an IIS site or application.</span></span> <span data-ttu-id="3de67-238">Vous devez également activer les options de suivi sous **system.WebServer** dans **Web.config**.</span><span class="sxs-lookup"><span data-stu-id="3de67-238">You must also enable tracing options under **system.WebServer** in **Web.config**.</span></span>|  
|<span data-ttu-id="3de67-239">**DataSources**</span><span class="sxs-lookup"><span data-stu-id="3de67-239">**DataSources**</span></span>|<span data-ttu-id="3de67-240">Liste de répertoires à analyser.</span><span class="sxs-lookup"><span data-stu-id="3de67-240">A list of directories to monitor.</span></span>| 




## <a name="datasources-element"></a><span data-ttu-id="3de67-241">Élément DataSources</span><span class="sxs-lookup"><span data-stu-id="3de67-241">DataSources Element</span></span>  
 <span data-ttu-id="3de67-242">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories - DataSources*</span><span class="sxs-lookup"><span data-stu-id="3de67-242">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories - DataSources*</span></span>

 <span data-ttu-id="3de67-243">Liste de répertoires à analyser.</span><span class="sxs-lookup"><span data-stu-id="3de67-243">A list of directories to monitor.</span></span>  

|<span data-ttu-id="3de67-244">Éléments enfants</span><span class="sxs-lookup"><span data-stu-id="3de67-244">Child Elements</span></span>|<span data-ttu-id="3de67-245">Description</span><span class="sxs-lookup"><span data-stu-id="3de67-245">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="3de67-246">**DirectoryConfiguration**</span><span class="sxs-lookup"><span data-stu-id="3de67-246">**DirectoryConfiguration**</span></span>|<span data-ttu-id="3de67-247">Obligatoire.</span><span class="sxs-lookup"><span data-stu-id="3de67-247">Required.</span></span> <span data-ttu-id="3de67-248">Attribut requis :</span><span class="sxs-lookup"><span data-stu-id="3de67-248">Required attribute:</span></span><br /><br /> <span data-ttu-id="3de67-249">**containerName** - Nom du conteneur d’objets blob de votre compte de stockage Azure à utiliser pour stocker les fichiers journaux.</span><span class="sxs-lookup"><span data-stu-id="3de67-249">**containerName** - The name of the blob container in your Azure Storage account that to be used to store the log files.</span></span>|  





## <a name="directoryconfiguration-element"></a><span data-ttu-id="3de67-250">Élément DirectoryConfiguration</span><span class="sxs-lookup"><span data-stu-id="3de67-250">DirectoryConfiguration Element</span></span>  
 <span data-ttu-id="3de67-251">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories - DataSources - DirectoryConfiguration*</span><span class="sxs-lookup"><span data-stu-id="3de67-251">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories - DataSources - DirectoryConfiguration*</span></span>

 <span data-ttu-id="3de67-252">Peut inclure l’élément **Absolute** ou **LocalResource**, mais pas les deux.</span><span class="sxs-lookup"><span data-stu-id="3de67-252">May include either the **Absolute** or **LocalResource** element but not both.</span></span>  

|<span data-ttu-id="3de67-253">Éléments enfants</span><span class="sxs-lookup"><span data-stu-id="3de67-253">Child Elements</span></span>|<span data-ttu-id="3de67-254">Description</span><span class="sxs-lookup"><span data-stu-id="3de67-254">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="3de67-255">**Absolute**</span><span class="sxs-lookup"><span data-stu-id="3de67-255">**Absolute**</span></span>|<span data-ttu-id="3de67-256">Chemin d’accès absolu au répertoire à surveiller.</span><span class="sxs-lookup"><span data-stu-id="3de67-256">The absolute path to the directory to monitor.</span></span> <span data-ttu-id="3de67-257">Les attributs suivants sont requis :</span><span class="sxs-lookup"><span data-stu-id="3de67-257">The following attributes are required:</span></span><br /><br /> <span data-ttu-id="3de67-258">- **Path** - Chemin d’accès absolu au répertoire à surveiller.</span><span class="sxs-lookup"><span data-stu-id="3de67-258">- **Path** - The absolute path to the directory to monitor.</span></span><br /><br /> <span data-ttu-id="3de67-259">- **expandEnvironment** - Détermine si les variables d’environnement de Path sont développées.</span><span class="sxs-lookup"><span data-stu-id="3de67-259">- **expandEnvironment** - Configures whether environment variables in Path are expanded.</span></span>|  
|<span data-ttu-id="3de67-260">**LocalResource**</span><span class="sxs-lookup"><span data-stu-id="3de67-260">**LocalResource**</span></span>|<span data-ttu-id="3de67-261">Chemin d’accès relatif à une ressource locale à surveiller.</span><span class="sxs-lookup"><span data-stu-id="3de67-261">The path relative to a local resource to monitor.</span></span> <span data-ttu-id="3de67-262">Les attributs requis sont :</span><span class="sxs-lookup"><span data-stu-id="3de67-262">Required attributes are:</span></span><br /><br /> <span data-ttu-id="3de67-263">- **Name** - Nom de la ressource locale contenant le répertoire à surveiller</span><span class="sxs-lookup"><span data-stu-id="3de67-263">- **Name** - The local resource that contains the directory to monitor</span></span><br /><br /> <span data-ttu-id="3de67-264">- **relativePath** - Chemin d’accès relatif au nom qui contient le répertoire à surveiller</span><span class="sxs-lookup"><span data-stu-id="3de67-264">- **relativePath** - The path relative to Name that contains the directory to monitor</span></span>|  



## <a name="etwproviders-element"></a><span data-ttu-id="3de67-265">Élément EtwProviders</span><span class="sxs-lookup"><span data-stu-id="3de67-265">EtwProviders Element</span></span>  
 <span data-ttu-id="3de67-266">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders*</span><span class="sxs-lookup"><span data-stu-id="3de67-266">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders*</span></span>

 <span data-ttu-id="3de67-267">Configure la collecte d’événements ETW issus des fournisseurs de manifeste EventSource et/ou ETW.</span><span class="sxs-lookup"><span data-stu-id="3de67-267">Configures collection of ETW events from EventSource and/or ETW Manifest based providers.</span></span>  

|<span data-ttu-id="3de67-268">Éléments enfants</span><span class="sxs-lookup"><span data-stu-id="3de67-268">Child Elements</span></span>|<span data-ttu-id="3de67-269">Description</span><span class="sxs-lookup"><span data-stu-id="3de67-269">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="3de67-270">**EtwEventSourceProviderConfiguration**</span><span class="sxs-lookup"><span data-stu-id="3de67-270">**EtwEventSourceProviderConfiguration**</span></span>|<span data-ttu-id="3de67-271">Configure la collection d’événements générés à partir de la [classe EventSource](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="3de67-271">Configures collection of events generated from [EventSource Class](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).</span></span> <span data-ttu-id="3de67-272">Attribut requis :</span><span class="sxs-lookup"><span data-stu-id="3de67-272">Required attribute:</span></span><br /><br /> <span data-ttu-id="3de67-273">**provider** - Nom de classe de l’événement EventSource.</span><span class="sxs-lookup"><span data-stu-id="3de67-273">**provider** - The class name of the EventSource event.</span></span><br /><br /> <span data-ttu-id="3de67-274">Les attributs facultatifs sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="3de67-274">Optional attributes are:</span></span><br /><br /> <span data-ttu-id="3de67-275">- **scheduledTransferLogLevelFilter** - Niveau de gravité minimal à transférer vers votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="3de67-275">- **scheduledTransferLogLevelFilter** - The minimum severity level to transfer to your storage account.</span></span><br /><br /> <span data-ttu-id="3de67-276">- **scheduledTransferPeriod** - Intervalle entre les transferts planifiés vers le stockage Azure, arrondi à la minute la plus proche.</span><span class="sxs-lookup"><span data-stu-id="3de67-276">- **scheduledTransferPeriod** - The interval between scheduled transfers to storage rounded up to the nearest minute.</span></span> <span data-ttu-id="3de67-277">La valeur est un [« Type de données de durée » XML.](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="3de67-277">The value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  
|<span data-ttu-id="3de67-278">**EtwManifestProviderConfiguration**</span><span class="sxs-lookup"><span data-stu-id="3de67-278">**EtwManifestProviderConfiguration**</span></span>|<span data-ttu-id="3de67-279">Attribut requis :</span><span class="sxs-lookup"><span data-stu-id="3de67-279">Required attribute:</span></span><br /><br /> <span data-ttu-id="3de67-280">**provider** -GUID du fournisseur d’événements</span><span class="sxs-lookup"><span data-stu-id="3de67-280">**provider** - The GUID of the event provider</span></span><br /><br /> <span data-ttu-id="3de67-281">Les attributs facultatifs sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="3de67-281">Optional attributes are:</span></span><br /><br /> <span data-ttu-id="3de67-282">- **scheduledTransferLogLevelFilter** - Niveau de gravité minimal à transférer vers votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="3de67-282">- **scheduledTransferLogLevelFilter** - The minimum severity level to transfer to your storage account.</span></span><br /><br /> <span data-ttu-id="3de67-283">- **scheduledTransferPeriod** - Intervalle entre les transferts planifiés vers le stockage Azure, arrondi à la minute la plus proche.</span><span class="sxs-lookup"><span data-stu-id="3de67-283">- **scheduledTransferPeriod** - The interval between scheduled transfers to storage rounded up to the nearest minute.</span></span> <span data-ttu-id="3de67-284">La valeur est un [« Type de données de durée » XML.](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="3de67-284">The value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  



## <a name="etweventsourceproviderconfiguration-element"></a><span data-ttu-id="3de67-285">EtwEventSourceProviderConfiguration Element</span><span class="sxs-lookup"><span data-stu-id="3de67-285">EtwEventSourceProviderConfiguration Element</span></span>  
 <span data-ttu-id="3de67-286">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders- EtwEventSourceProviderConfiguration*</span><span class="sxs-lookup"><span data-stu-id="3de67-286">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders- EtwEventSourceProviderConfiguration*</span></span>

 <span data-ttu-id="3de67-287">Configure la collection d’événements générés à partir de la [classe EventSource](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="3de67-287">Configures collection of events generated from [EventSource Class](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).</span></span>  

|<span data-ttu-id="3de67-288">Éléments enfants</span><span class="sxs-lookup"><span data-stu-id="3de67-288">Child Elements</span></span>|<span data-ttu-id="3de67-289">Description</span><span class="sxs-lookup"><span data-stu-id="3de67-289">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="3de67-290">**DefaultEvents**</span><span class="sxs-lookup"><span data-stu-id="3de67-290">**DefaultEvents**</span></span>|<span data-ttu-id="3de67-291">Attribut facultatif :</span><span class="sxs-lookup"><span data-stu-id="3de67-291">Optional attribute:</span></span><br/><br/> <span data-ttu-id="3de67-292">**eventDestination** -Nom de la table dans laquelle stocker les événements</span><span class="sxs-lookup"><span data-stu-id="3de67-292">**eventDestination** - The name of the table to store the events in</span></span>|  
|<span data-ttu-id="3de67-293">**Event**</span><span class="sxs-lookup"><span data-stu-id="3de67-293">**Event**</span></span>|<span data-ttu-id="3de67-294">Attribut requis :</span><span class="sxs-lookup"><span data-stu-id="3de67-294">Required attribute:</span></span><br /><br /> <span data-ttu-id="3de67-295">**id** : ID de l’événement.</span><span class="sxs-lookup"><span data-stu-id="3de67-295">**id** - The id of the event.</span></span><br /><br /> <span data-ttu-id="3de67-296">Attribut facultatif :</span><span class="sxs-lookup"><span data-stu-id="3de67-296">Optional attribute:</span></span><br /><br /> <span data-ttu-id="3de67-297">**eventDestination** -Nom de la table dans laquelle stocker les événements</span><span class="sxs-lookup"><span data-stu-id="3de67-297">**eventDestination** - The name of the table to store the events in</span></span>|  



## <a name="etwmanifestproviderconfiguration-element"></a><span data-ttu-id="3de67-298">EtwManifestProviderConfiguration Element</span><span class="sxs-lookup"><span data-stu-id="3de67-298">EtwManifestProviderConfiguration Element</span></span>  
 <span data-ttu-id="3de67-299">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders - EtwManifestProviderConfiguration*</span><span class="sxs-lookup"><span data-stu-id="3de67-299">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders - EtwManifestProviderConfiguration*</span></span>

|<span data-ttu-id="3de67-300">Éléments enfants</span><span class="sxs-lookup"><span data-stu-id="3de67-300">Child Elements</span></span>|<span data-ttu-id="3de67-301">Description</span><span class="sxs-lookup"><span data-stu-id="3de67-301">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="3de67-302">**DefaultEvents**</span><span class="sxs-lookup"><span data-stu-id="3de67-302">**DefaultEvents**</span></span>|<span data-ttu-id="3de67-303">Attribut facultatif :</span><span class="sxs-lookup"><span data-stu-id="3de67-303">Optional attribute:</span></span><br /><br /> <span data-ttu-id="3de67-304">**eventDestination** -Nom de la table dans laquelle stocker les événements</span><span class="sxs-lookup"><span data-stu-id="3de67-304">**eventDestination** - The name of the table to store the events in</span></span>|  
|<span data-ttu-id="3de67-305">**Event**</span><span class="sxs-lookup"><span data-stu-id="3de67-305">**Event**</span></span>|<span data-ttu-id="3de67-306">Attribut requis :</span><span class="sxs-lookup"><span data-stu-id="3de67-306">Required attribute:</span></span><br /><br /> <span data-ttu-id="3de67-307">**id** : ID de l’événement.</span><span class="sxs-lookup"><span data-stu-id="3de67-307">**id** - The id of the event.</span></span><br /><br /> <span data-ttu-id="3de67-308">Attribut facultatif :</span><span class="sxs-lookup"><span data-stu-id="3de67-308">Optional attribute:</span></span><br /><br /> <span data-ttu-id="3de67-309">**eventDestination** -Nom de la table dans laquelle stocker les événements</span><span class="sxs-lookup"><span data-stu-id="3de67-309">**eventDestination** - The name of the table to store the events in</span></span>|  



## <a name="metrics-element"></a><span data-ttu-id="3de67-310">Élément Metrics</span><span class="sxs-lookup"><span data-stu-id="3de67-310">Metrics Element</span></span>  
 <span data-ttu-id="3de67-311">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Metrics*</span><span class="sxs-lookup"><span data-stu-id="3de67-311">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Metrics*</span></span>

 <span data-ttu-id="3de67-312">Permet de générer une table de compteur de performance optimisée pour les requêtes rapides.</span><span class="sxs-lookup"><span data-stu-id="3de67-312">Enables you to generate a performance counter table that is optimized for fast queries.</span></span> <span data-ttu-id="3de67-313">Chaque compteur de performance défini dans l’élement **PerformanceCounters** est stocké dans la table Metrics et dans la table Performance Counter.</span><span class="sxs-lookup"><span data-stu-id="3de67-313">Each performance counter that is defined in the **PerformanceCounters** element is stored in the Metrics table in addition to the Performance Counter table.</span></span>  

 <span data-ttu-id="3de67-314">L’attribut **resourceId** est requis.</span><span class="sxs-lookup"><span data-stu-id="3de67-314">The **resourceId** attribute is required.</span></span>  <span data-ttu-id="3de67-315">Il s’agit de l’ID de ressource de la machine virtuelle sur laquelle vous déployez Azure Diagnostics.</span><span class="sxs-lookup"><span data-stu-id="3de67-315">The resource ID of the Virtual Machine you are deploying Azure Diagnostics to.</span></span> <span data-ttu-id="3de67-316">Obtenez le **resourceID** à partir du [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3de67-316">Get the **resourceID** from the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="3de67-317">Sélectionnez **Parcourir** -> **Groupe de ressources** -> **<>\>**.</span><span class="sxs-lookup"><span data-stu-id="3de67-317">Select **Browse** -> **Resource Groups** -> **<Name\>**.</span></span> <span data-ttu-id="3de67-318">Cliquez sur la vignette **Propriétés** et copiez la valeur à partir du champ **ID**.</span><span class="sxs-lookup"><span data-stu-id="3de67-318">Click the **Properties** tile and copy the value from the **ID** field.</span></span>  

|<span data-ttu-id="3de67-319">Éléments enfants</span><span class="sxs-lookup"><span data-stu-id="3de67-319">Child Elements</span></span>|<span data-ttu-id="3de67-320">Description</span><span class="sxs-lookup"><span data-stu-id="3de67-320">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="3de67-321">**MetricAggregation**</span><span class="sxs-lookup"><span data-stu-id="3de67-321">**MetricAggregation**</span></span>|<span data-ttu-id="3de67-322">Attribut requis :</span><span class="sxs-lookup"><span data-stu-id="3de67-322">Required attribute:</span></span><br /><br /> <span data-ttu-id="3de67-323">**scheduledTransferPeriod** - Intervalle entre les transferts planifiés vers le stockage Azure, arrondi à la minute la plus proche.</span><span class="sxs-lookup"><span data-stu-id="3de67-323">**scheduledTransferPeriod** - The interval between scheduled transfers to storage rounded up to the nearest minute.</span></span> <span data-ttu-id="3de67-324">La valeur est un [« Type de données de durée » XML.](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="3de67-324">The value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  



## <a name="performancecounters-element"></a><span data-ttu-id="3de67-325">Élément PerformanceCounters</span><span class="sxs-lookup"><span data-stu-id="3de67-325">PerformanceCounters Element</span></span>  
 <span data-ttu-id="3de67-326">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - PerformanceCounters*</span><span class="sxs-lookup"><span data-stu-id="3de67-326">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - PerformanceCounters*</span></span>

 <span data-ttu-id="3de67-327">Permet la collecte des compteurs de performance.</span><span class="sxs-lookup"><span data-stu-id="3de67-327">Enables the collection of performance counters.</span></span>  

 <span data-ttu-id="3de67-328">Attribut facultatif :</span><span class="sxs-lookup"><span data-stu-id="3de67-328">Optional attribute:</span></span>  

 <span data-ttu-id="3de67-329">Attribut **scheduledTransferPeriod** facultatif.</span><span class="sxs-lookup"><span data-stu-id="3de67-329">Optional **scheduledTransferPeriod** attribute.</span></span> <span data-ttu-id="3de67-330">Voir l’explication précédente.</span><span class="sxs-lookup"><span data-stu-id="3de67-330">See explanation earlier.</span></span>

|<span data-ttu-id="3de67-331">Élément enfant</span><span class="sxs-lookup"><span data-stu-id="3de67-331">Child Element</span></span>|<span data-ttu-id="3de67-332">Description</span><span class="sxs-lookup"><span data-stu-id="3de67-332">Description</span></span>|  
|-------------------|-----------------|  
|<span data-ttu-id="3de67-333">**PerformanceCounterConfiguration**</span><span class="sxs-lookup"><span data-stu-id="3de67-333">**PerformanceCounterConfiguration**</span></span>|<span data-ttu-id="3de67-334">Les attributs suivants sont requis :</span><span class="sxs-lookup"><span data-stu-id="3de67-334">The following attributes are required:</span></span><br /><br /> <span data-ttu-id="3de67-335">- **counterSpecifier** - Nom du compteur de performance.</span><span class="sxs-lookup"><span data-stu-id="3de67-335">- **counterSpecifier** - The name of the performance counter.</span></span> <span data-ttu-id="3de67-336">Par exemple, `\Processor(_Total)\% Processor Time`.</span><span class="sxs-lookup"><span data-stu-id="3de67-336">For example, `\Processor(_Total)\% Processor Time`.</span></span> <span data-ttu-id="3de67-337">Pour obtenir une liste des compteurs de performances se trouvant sur votre hôte, exécutez la commande `typeperf`.</span><span class="sxs-lookup"><span data-stu-id="3de67-337">To get a list of performance counters on your host, run the command `typeperf`.</span></span><br /><br /> <span data-ttu-id="3de67-338">- **sampleRate** - Fréquence à laquelle le compteur doit être échantillonné.</span><span class="sxs-lookup"><span data-stu-id="3de67-338">- **sampleRate** - How often the counter should be sampled.</span></span><br /><br /> <span data-ttu-id="3de67-339">Attribut facultatif :</span><span class="sxs-lookup"><span data-stu-id="3de67-339">Optional attribute:</span></span><br /><br /> <span data-ttu-id="3de67-340">**unit** -Unité de mesure du compteur.</span><span class="sxs-lookup"><span data-stu-id="3de67-340">**unit** - The unit of measure of the counter.</span></span>|  




## <a name="windowseventlog-element"></a><span data-ttu-id="3de67-341">Élément WindowsEventLog</span><span class="sxs-lookup"><span data-stu-id="3de67-341">WindowsEventLog Element</span></span>
 <span data-ttu-id="3de67-342">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - WindowsEventLog*</span><span class="sxs-lookup"><span data-stu-id="3de67-342">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - WindowsEventLog*</span></span>
 
 <span data-ttu-id="3de67-343">Permet la collecte des journaux des événements Windows.</span><span class="sxs-lookup"><span data-stu-id="3de67-343">Enables the collection of Windows Event Logs.</span></span>  

 <span data-ttu-id="3de67-344">Attribut **scheduledTransferPeriod** facultatif.</span><span class="sxs-lookup"><span data-stu-id="3de67-344">Optional **scheduledTransferPeriod** attribute.</span></span> <span data-ttu-id="3de67-345">Voir l’explication précédente.</span><span class="sxs-lookup"><span data-stu-id="3de67-345">See explanation  earlier.</span></span>  

|<span data-ttu-id="3de67-346">Élément enfant</span><span class="sxs-lookup"><span data-stu-id="3de67-346">Child Element</span></span>|<span data-ttu-id="3de67-347">Description</span><span class="sxs-lookup"><span data-stu-id="3de67-347">Description</span></span>|  
|-------------------|-----------------|  
|<span data-ttu-id="3de67-348">**DataSource**</span><span class="sxs-lookup"><span data-stu-id="3de67-348">**DataSource**</span></span>|<span data-ttu-id="3de67-349">Journaux des événements Windows à collecter.</span><span class="sxs-lookup"><span data-stu-id="3de67-349">The Windows Event logs to collect.</span></span> <span data-ttu-id="3de67-350">Attribut requis :</span><span class="sxs-lookup"><span data-stu-id="3de67-350">Required attribute:</span></span><br /><br /> <span data-ttu-id="3de67-351">**name** - Requête XPath décrivant les événements windows à collecter.</span><span class="sxs-lookup"><span data-stu-id="3de67-351">**name** - The XPath query describing the windows events to be collected.</span></span> <span data-ttu-id="3de67-352">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="3de67-352">For example:</span></span><br /><br /> `Application!*[System[(Level <=3)]], System!*[System[(Level <=3)]], System!*[System[Provider[@Name='Microsoft Antimalware']]], Security!*[System[(Level <= 3)]`<br /><br /> <span data-ttu-id="3de67-353">Pour collecter tous les événements, spécifiez « * ».</span><span class="sxs-lookup"><span data-stu-id="3de67-353">To collect all events, specify "*"</span></span>|  




## <a name="logs-element"></a><span data-ttu-id="3de67-354">Élément Logs</span><span class="sxs-lookup"><span data-stu-id="3de67-354">Logs Element</span></span>  
 <span data-ttu-id="3de67-355">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Logs*</span><span class="sxs-lookup"><span data-stu-id="3de67-355">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Logs*</span></span>

 <span data-ttu-id="3de67-356">Présent dans la version 1.0 et 1.1.</span><span class="sxs-lookup"><span data-stu-id="3de67-356">Present in version 1.0 and 1.1.</span></span> <span data-ttu-id="3de67-357">Absent dans la version 1.2.</span><span class="sxs-lookup"><span data-stu-id="3de67-357">Missing in 1.2.</span></span> <span data-ttu-id="3de67-358">Rajouté dans la version 1.3.</span><span class="sxs-lookup"><span data-stu-id="3de67-358">Added back in 1.3.</span></span>  

 <span data-ttu-id="3de67-359">Définit la configuration de la mémoire tampon des journaux Azure de base.</span><span class="sxs-lookup"><span data-stu-id="3de67-359">Defines the buffer configuration for basic Azure logs.</span></span>  

|<span data-ttu-id="3de67-360">Attribut</span><span class="sxs-lookup"><span data-stu-id="3de67-360">Attribute</span></span>|<span data-ttu-id="3de67-361">Type</span><span class="sxs-lookup"><span data-stu-id="3de67-361">Type</span></span>|<span data-ttu-id="3de67-362">Description</span><span class="sxs-lookup"><span data-stu-id="3de67-362">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="3de67-363">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="3de67-363">**bufferQuotaInMB**</span></span>|<span data-ttu-id="3de67-364">**unsignedInt**</span><span class="sxs-lookup"><span data-stu-id="3de67-364">**unsignedInt**</span></span>|<span data-ttu-id="3de67-365">facultatif.</span><span class="sxs-lookup"><span data-stu-id="3de67-365">Optional.</span></span> <span data-ttu-id="3de67-366">Définit la quantité maximale de stockage du système de fichiers disponible pour les données spécifiées.</span><span class="sxs-lookup"><span data-stu-id="3de67-366">Specifies the maximum amount of file system storage that is available for the specified data.</span></span><br /><br /> <span data-ttu-id="3de67-367">La valeur par défaut est 0.</span><span class="sxs-lookup"><span data-stu-id="3de67-367">The default is 0.</span></span>|  
|<span data-ttu-id="3de67-368">**scheduledTransferLogLevelFilterr**</span><span class="sxs-lookup"><span data-stu-id="3de67-368">**scheduledTransferLogLevelFilterr**</span></span>|<span data-ttu-id="3de67-369">**string**</span><span class="sxs-lookup"><span data-stu-id="3de67-369">**string**</span></span>|<span data-ttu-id="3de67-370">facultatif.</span><span class="sxs-lookup"><span data-stu-id="3de67-370">Optional.</span></span> <span data-ttu-id="3de67-371">Définit le niveau de gravité minimal des entrées de journal transférées.</span><span class="sxs-lookup"><span data-stu-id="3de67-371">Specifies the minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="3de67-372">La valeur par défaut qui transfère tous les journaux est **Undefined**.</span><span class="sxs-lookup"><span data-stu-id="3de67-372">The default value is **Undefined**, which transfers all logs.</span></span> <span data-ttu-id="3de67-373">Les autres valeurs possibles sont, du plus informatif au moins informatif : **Détaillé**, **Informations**, **Avertissement**, **Erreur**, **Critique**.</span><span class="sxs-lookup"><span data-stu-id="3de67-373">Other possible values (in order of most to least information) are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="3de67-374">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="3de67-374">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="3de67-375">**duration**</span><span class="sxs-lookup"><span data-stu-id="3de67-375">**duration**</span></span>|<span data-ttu-id="3de67-376">facultatif.</span><span class="sxs-lookup"><span data-stu-id="3de67-376">Optional.</span></span> <span data-ttu-id="3de67-377">Définit l’intervalle entre les transferts planifiés de données, arrondi à la minute la plus proche.</span><span class="sxs-lookup"><span data-stu-id="3de67-377">Specifies the interval between scheduled transfers of data, rounded up to the nearest minute.</span></span><br /><br /> <span data-ttu-id="3de67-378">La valeur par défaut est PT0S.</span><span class="sxs-lookup"><span data-stu-id="3de67-378">The default is PT0S.</span></span>|  
|<span data-ttu-id="3de67-379">**sinks** - Ajouté à la version 1.5</span><span class="sxs-lookup"><span data-stu-id="3de67-379">**sinks** Added in 1.5</span></span>|<span data-ttu-id="3de67-380">**string**</span><span class="sxs-lookup"><span data-stu-id="3de67-380">**string**</span></span>|<span data-ttu-id="3de67-381">facultatif.</span><span class="sxs-lookup"><span data-stu-id="3de67-381">Optional.</span></span> <span data-ttu-id="3de67-382">Pointe vers un emplacement de récepteur permettant d’envoyer également des données de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="3de67-382">Points to a sink location to also send diagnostic data.</span></span> <span data-ttu-id="3de67-383">Par exemple, Application Insights.</span><span class="sxs-lookup"><span data-stu-id="3de67-383">For example, Application Insights.</span></span>|  

## <a name="dockersources"></a><span data-ttu-id="3de67-384">DockerSources</span><span class="sxs-lookup"><span data-stu-id="3de67-384">DockerSources</span></span>
 <span data-ttu-id="3de67-385">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - DockerSources*</span><span class="sxs-lookup"><span data-stu-id="3de67-385">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - DockerSources*</span></span>

 <span data-ttu-id="3de67-386">Ajouté dans 1.9.</span><span class="sxs-lookup"><span data-stu-id="3de67-386">Added in 1.9.</span></span>

|<span data-ttu-id="3de67-387">Nom de l’élément</span><span class="sxs-lookup"><span data-stu-id="3de67-387">Element Name</span></span>|<span data-ttu-id="3de67-388">Description</span><span class="sxs-lookup"><span data-stu-id="3de67-388">Description</span></span>|  
|------------------|-----------------|  
|<span data-ttu-id="3de67-389">**Stats**</span><span class="sxs-lookup"><span data-stu-id="3de67-389">**Stats**</span></span>|<span data-ttu-id="3de67-390">Indique au système de collecter les statistiques pour les conteneurs Docker</span><span class="sxs-lookup"><span data-stu-id="3de67-390">Tells the system to collect stats for Docker containers</span></span>|  

## <a name="sinksconfig-element"></a><span data-ttu-id="3de67-391">Élément SinksConfig</span><span class="sxs-lookup"><span data-stu-id="3de67-391">SinksConfig Element</span></span>  
 <span data-ttu-id="3de67-392">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig*</span><span class="sxs-lookup"><span data-stu-id="3de67-392">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig*</span></span>

 <span data-ttu-id="3de67-393">Liste d’emplacements vers lesquels envoyer des données de diagnostic et la configuration associée à ces emplacements.</span><span class="sxs-lookup"><span data-stu-id="3de67-393">A list of locations to send diagnostics data to and the configuration associated with those locations.</span></span>  

|<span data-ttu-id="3de67-394">Nom de l’élément</span><span class="sxs-lookup"><span data-stu-id="3de67-394">Element Name</span></span>|<span data-ttu-id="3de67-395">Description</span><span class="sxs-lookup"><span data-stu-id="3de67-395">Description</span></span>|  
|------------------|-----------------|  
|<span data-ttu-id="3de67-396">**Section sink**</span><span class="sxs-lookup"><span data-stu-id="3de67-396">**Sink**</span></span>|<span data-ttu-id="3de67-397">Consultez la description sur cette page.</span><span class="sxs-lookup"><span data-stu-id="3de67-397">See description elsewhere on this page.</span></span>|  

## <a name="sink-element"></a><span data-ttu-id="3de67-398">Élément Sink</span><span class="sxs-lookup"><span data-stu-id="3de67-398">Sink Element</span></span>
 <span data-ttu-id="3de67-399">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink*</span><span class="sxs-lookup"><span data-stu-id="3de67-399">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink*</span></span>

 <span data-ttu-id="3de67-400">Ajouté à la version 1.5.</span><span class="sxs-lookup"><span data-stu-id="3de67-400">Added in version 1.5.</span></span>  

 <span data-ttu-id="3de67-401">Définit les emplacements vers lesquels envoyer des données de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="3de67-401">Defines locations to send diagnostic data to.</span></span> <span data-ttu-id="3de67-402">Par exemple, le service Application Insights.</span><span class="sxs-lookup"><span data-stu-id="3de67-402">For example, the Application Insights service.</span></span>  

|<span data-ttu-id="3de67-403">Attribut</span><span class="sxs-lookup"><span data-stu-id="3de67-403">Attribute</span></span>|<span data-ttu-id="3de67-404">Type</span><span class="sxs-lookup"><span data-stu-id="3de67-404">Type</span></span>|<span data-ttu-id="3de67-405">Description</span><span class="sxs-lookup"><span data-stu-id="3de67-405">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="3de67-406">**name**</span><span class="sxs-lookup"><span data-stu-id="3de67-406">**name**</span></span>|<span data-ttu-id="3de67-407">string</span><span class="sxs-lookup"><span data-stu-id="3de67-407">string</span></span>|<span data-ttu-id="3de67-408">Chaîne identifiant le nom du récepteur.</span><span class="sxs-lookup"><span data-stu-id="3de67-408">A string identifying the sinkname.</span></span>|  

|<span data-ttu-id="3de67-409">Élément</span><span class="sxs-lookup"><span data-stu-id="3de67-409">Element</span></span>|<span data-ttu-id="3de67-410">Type</span><span class="sxs-lookup"><span data-stu-id="3de67-410">Type</span></span>|<span data-ttu-id="3de67-411">Description</span><span class="sxs-lookup"><span data-stu-id="3de67-411">Description</span></span>|  
|-------------|----------|-----------------|  
|<span data-ttu-id="3de67-412">**Application Insights**</span><span class="sxs-lookup"><span data-stu-id="3de67-412">**Application Insights**</span></span>|<span data-ttu-id="3de67-413">string</span><span class="sxs-lookup"><span data-stu-id="3de67-413">string</span></span>|<span data-ttu-id="3de67-414">Utilisé uniquement lors de l’envoi de données à Application Insights.</span><span class="sxs-lookup"><span data-stu-id="3de67-414">Used only when sending data to Application Insights.</span></span> <span data-ttu-id="3de67-415">Contient la clé d’instrumentation d’un compte Application Insights actif auquel vous avez accès.</span><span class="sxs-lookup"><span data-stu-id="3de67-415">Contain the Instrumentation Key for an active Application Insights account that you have access to.</span></span>|  
|<span data-ttu-id="3de67-416">**Canaux**</span><span class="sxs-lookup"><span data-stu-id="3de67-416">**Channels**</span></span>|<span data-ttu-id="3de67-417">string</span><span class="sxs-lookup"><span data-stu-id="3de67-417">string</span></span>|<span data-ttu-id="3de67-418">Un pour chaque filtrage supplémentaire qui diffuse cela en continu</span><span class="sxs-lookup"><span data-stu-id="3de67-418">One for each additional filtering that stream that you</span></span>|  

## <a name="channels-element"></a><span data-ttu-id="3de67-419">Élément Channels</span><span class="sxs-lookup"><span data-stu-id="3de67-419">Channels Element</span></span>  
 <span data-ttu-id="3de67-420">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - Channels*</span><span class="sxs-lookup"><span data-stu-id="3de67-420">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - Channels*</span></span>

 <span data-ttu-id="3de67-421">Ajouté à la version 1.5.</span><span class="sxs-lookup"><span data-stu-id="3de67-421">Added in version 1.5.</span></span>  

 <span data-ttu-id="3de67-422">Définit les filtres pour les flux de données de journaux passant par un récepteur.</span><span class="sxs-lookup"><span data-stu-id="3de67-422">Defines filters for streams of log data passing through a sink.</span></span>  

|<span data-ttu-id="3de67-423">Élément</span><span class="sxs-lookup"><span data-stu-id="3de67-423">Element</span></span>|<span data-ttu-id="3de67-424">Type</span><span class="sxs-lookup"><span data-stu-id="3de67-424">Type</span></span>|<span data-ttu-id="3de67-425">Description</span><span class="sxs-lookup"><span data-stu-id="3de67-425">Description</span></span>|  
|-------------|----------|-----------------|  
|<span data-ttu-id="3de67-426">**Channel**</span><span class="sxs-lookup"><span data-stu-id="3de67-426">**Channel**</span></span>|<span data-ttu-id="3de67-427">string</span><span class="sxs-lookup"><span data-stu-id="3de67-427">string</span></span>|<span data-ttu-id="3de67-428">Consultez la description sur cette page.</span><span class="sxs-lookup"><span data-stu-id="3de67-428">See description elsewhere on this page.</span></span>|  

## <a name="channel-element"></a><span data-ttu-id="3de67-429">Élément Channel</span><span class="sxs-lookup"><span data-stu-id="3de67-429">Channel Element</span></span>
 <span data-ttu-id="3de67-430">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - Channels - Channel*</span><span class="sxs-lookup"><span data-stu-id="3de67-430">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - Channels - Channel*</span></span>

 <span data-ttu-id="3de67-431">Ajouté à la version 1.5.</span><span class="sxs-lookup"><span data-stu-id="3de67-431">Added in version 1.5.</span></span>  

 <span data-ttu-id="3de67-432">Définit les emplacements vers lesquels envoyer des données de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="3de67-432">Defines locations to send diagnostic data to.</span></span> <span data-ttu-id="3de67-433">Par exemple, le service Application Insights.</span><span class="sxs-lookup"><span data-stu-id="3de67-433">For example, the Application Insights service.</span></span>  

|<span data-ttu-id="3de67-434">Attributs</span><span class="sxs-lookup"><span data-stu-id="3de67-434">Attributes</span></span>|<span data-ttu-id="3de67-435">Type</span><span class="sxs-lookup"><span data-stu-id="3de67-435">Type</span></span>|<span data-ttu-id="3de67-436">Description</span><span class="sxs-lookup"><span data-stu-id="3de67-436">Description</span></span>|  
|----------------|----------|-----------------|  
|<span data-ttu-id="3de67-437">**logLevel**</span><span class="sxs-lookup"><span data-stu-id="3de67-437">**logLevel**</span></span>|<span data-ttu-id="3de67-438">**string**</span><span class="sxs-lookup"><span data-stu-id="3de67-438">**string**</span></span>|<span data-ttu-id="3de67-439">Définit le niveau de gravité minimal des entrées de journal transférées.</span><span class="sxs-lookup"><span data-stu-id="3de67-439">Specifies the minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="3de67-440">La valeur par défaut qui transfère tous les journaux est **Undefined**.</span><span class="sxs-lookup"><span data-stu-id="3de67-440">The default value is **Undefined**, which transfers all logs.</span></span> <span data-ttu-id="3de67-441">Les autres valeurs possibles sont, du plus informatif au moins informatif : **Détaillé**, **Informations**, **Avertissement**, **Erreur**, **Critique**.</span><span class="sxs-lookup"><span data-stu-id="3de67-441">Other possible values (in order of most to least information) are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="3de67-442">**name**</span><span class="sxs-lookup"><span data-stu-id="3de67-442">**name**</span></span>|<span data-ttu-id="3de67-443">**string**</span><span class="sxs-lookup"><span data-stu-id="3de67-443">**string**</span></span>|<span data-ttu-id="3de67-444">Nom unique du canal auquel faire référence</span><span class="sxs-lookup"><span data-stu-id="3de67-444">A unique name of the channel to refer to</span></span>|  


## <a name="privateconfig-element"></a><span data-ttu-id="3de67-445">Élément PrivateConfig</span><span class="sxs-lookup"><span data-stu-id="3de67-445">PrivateConfig Element</span></span> 
 <span data-ttu-id="3de67-446">*Tree: Root - DiagnosticsConfiguration - PrivateConfig*</span><span class="sxs-lookup"><span data-stu-id="3de67-446">*Tree: Root - DiagnosticsConfiguration - PrivateConfig*</span></span>

 <span data-ttu-id="3de67-447">Ajouté à la version 1.3.</span><span class="sxs-lookup"><span data-stu-id="3de67-447">Added in version 1.3.</span></span>  

 <span data-ttu-id="3de67-448">Facultatif</span><span class="sxs-lookup"><span data-stu-id="3de67-448">Optional</span></span>  

 <span data-ttu-id="3de67-449">Stocke les détails privés du compte de stockage (nom, clé et point de terminaison).</span><span class="sxs-lookup"><span data-stu-id="3de67-449">Stores the private details of the storage account (name, key, and endpoint).</span></span> <span data-ttu-id="3de67-450">Cette information est envoyée à la machine virtuelle, mais ne peut pas être récupérée à partir de celui-ci.</span><span class="sxs-lookup"><span data-stu-id="3de67-450">This information is sent to the virtual machine, but cannot be retrieved from it.</span></span>  

|<span data-ttu-id="3de67-451">Éléments enfants</span><span class="sxs-lookup"><span data-stu-id="3de67-451">Child Elements</span></span>|<span data-ttu-id="3de67-452">Description</span><span class="sxs-lookup"><span data-stu-id="3de67-452">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="3de67-453">**StorageAccount**</span><span class="sxs-lookup"><span data-stu-id="3de67-453">**StorageAccount**</span></span>|<span data-ttu-id="3de67-454">Compte de stockage à utiliser.</span><span class="sxs-lookup"><span data-stu-id="3de67-454">The storage account to use.</span></span> <span data-ttu-id="3de67-455">Les attributs suivants sont requis :</span><span class="sxs-lookup"><span data-stu-id="3de67-455">The following attributes are required</span></span><br /><br /> <span data-ttu-id="3de67-456">- **name** - Nom du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="3de67-456">- **name** - The name of the storage account.</span></span><br /><br /> <span data-ttu-id="3de67-457">- **key** - Clé du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="3de67-457">- **key** - The key to the storage account.</span></span><br /><br /> <span data-ttu-id="3de67-458">- **endpoint** - Point de terminaison permettant d’accéder au compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="3de67-458">- **endpoint** - The endpoint to access the storage account.</span></span> <br /><br /> <span data-ttu-id="3de67-459">-**sasToken** (ajouté 1.8.1)-, vous pouvez spécifier un jeton SAP au lieu d’une clé de compte de stockage dans la configuration privée.</span><span class="sxs-lookup"><span data-stu-id="3de67-459">-**sasToken** (added 1.8.1)- You can specify an SAS token instead of a storage account key in the private config.</span></span> <span data-ttu-id="3de67-460">Si la clé de compte de stockage est fournie, elle est ignorée.</span><span class="sxs-lookup"><span data-stu-id="3de67-460">If provided, the storage account key is ignored.</span></span> <br /><span data-ttu-id="3de67-461">Configuration requise pour le jeton SAP :</span><span class="sxs-lookup"><span data-stu-id="3de67-461">Requirements for the SAS Token:</span></span> <br /><span data-ttu-id="3de67-462">- Prend en charge le jeton SAP de compte uniquement.</span><span class="sxs-lookup"><span data-stu-id="3de67-462">- Supports account SAS token only</span></span> <br /><span data-ttu-id="3de67-463">Les types de services - *b*, *t* sont requis.</span><span class="sxs-lookup"><span data-stu-id="3de67-463">- *b*, *t* service types are required.</span></span> <br /> <span data-ttu-id="3de67-464">Les autorisations - *a*, *c*, *u*, *w* sont requises.</span><span class="sxs-lookup"><span data-stu-id="3de67-464">- *a*, *c*, *u*, *w* permissions are required.</span></span> <br /> <span data-ttu-id="3de67-465">Les types de ressources - *c*, *o* sont requis.</span><span class="sxs-lookup"><span data-stu-id="3de67-465">- *c*, *o* resource types are required.</span></span> <br /> <span data-ttu-id="3de67-466">- Prend en charge le protocole HTTPS uniquement.</span><span class="sxs-lookup"><span data-stu-id="3de67-466">- Supports the HTTPS protocol only</span></span> <br /> <span data-ttu-id="3de67-467">- Les heures de début et d’expiration doivent être valides.</span><span class="sxs-lookup"><span data-stu-id="3de67-467">- Start and expiry time must be valid.</span></span>|  


## <a name="isenabled-element"></a><span data-ttu-id="3de67-468">Élément IsEnabled</span><span class="sxs-lookup"><span data-stu-id="3de67-468">IsEnabled Element</span></span>  
 <span data-ttu-id="3de67-469">*Tree: Root - DiagnosticsConfiguration - IsEnabled*</span><span class="sxs-lookup"><span data-stu-id="3de67-469">*Tree: Root - DiagnosticsConfiguration - IsEnabled*</span></span>

 <span data-ttu-id="3de67-470">Booléen.</span><span class="sxs-lookup"><span data-stu-id="3de67-470">Boolean.</span></span> <span data-ttu-id="3de67-471">Utilisez `true` pour activer les diagnostics ou `false` pour les désactiver.</span><span class="sxs-lookup"><span data-stu-id="3de67-471">Use `true` to enable the diagnostics or `false` to disable the diagnostics.</span></span>
