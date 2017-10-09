---
title: "schéma de configuration 1.3 et versions ultérieures extension aaaAzure Diagnostics | Documents Microsoft"
description: "Version du schéma 1.3 et ultérieure diagnostics Azure partie intégrante de hello Microsoft Azure SDK 2.4 et versions ultérieur."
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
ms.openlocfilehash: bd15d3a79ea818fcb3235854717e58d5da36518e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-diagnostics-13-and-later-configuration-schema"></a><span data-ttu-id="88615-103">Schéma de configuration de Microsoft Azure Diagnostics 1.3 et versions ultérieures</span><span class="sxs-lookup"><span data-stu-id="88615-103">Azure Diagnostics 1.3 and later configuration schema</span></span>
> [!NOTE]
> <span data-ttu-id="88615-104">Hello extension Azure Diagnostics est composant de hello utilisé toocollect les compteurs de performance et d’autres statistiques à partir de :</span><span class="sxs-lookup"><span data-stu-id="88615-104">hello Azure Diagnostics extension is hello component used toocollect performance counters and other statistics from:</span></span>
> - <span data-ttu-id="88615-105">Machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="88615-105">Azure Virtual Machines</span></span> 
> - <span data-ttu-id="88615-106">Jeux de mise à l’échelle de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="88615-106">Virtual Machine Scale Sets</span></span>
> - <span data-ttu-id="88615-107">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="88615-107">Service Fabric</span></span> 
> - <span data-ttu-id="88615-108">Services cloud</span><span class="sxs-lookup"><span data-stu-id="88615-108">Cloud Services</span></span> 
> - <span data-ttu-id="88615-109">Groupes de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="88615-109">Network Security Groups</span></span>
> 
> <span data-ttu-id="88615-110">Cette page vous concerne uniquement si vous utilisez l’un de ces services.</span><span class="sxs-lookup"><span data-stu-id="88615-110">This page is only relevant if you are using one of these services.</span></span>

<span data-ttu-id="88615-111">Cette page a trait aux versions 1.3 et ultérieures (Azure SDK 2.4 et ultérieur).</span><span class="sxs-lookup"><span data-stu-id="88615-111">This page is valid for versions 1.3 and newer (Azure SDK 2.4 and newer).</span></span> <span data-ttu-id="88615-112">Les sections de configuration plus récentes sont tooshow commentée dans version ils ont été ajoutés.</span><span class="sxs-lookup"><span data-stu-id="88615-112">Newer configuration sections are commented tooshow in what version they were added.</span></span>  

<span data-ttu-id="88615-113">fichier de configuration de Hello décrite ici est tooset utilisé les paramètres de configuration de diagnostic lorsque hello diagnostics surveiller démarre.</span><span class="sxs-lookup"><span data-stu-id="88615-113">hello configuration file described here is used tooset diagnostic configuration settings when hello diagnostics monitor starts.</span></span>  

<span data-ttu-id="88615-114">extension de Hello est utilisée conjointement avec d’autres produits de diagnostics de Microsoft, analyse d’Azure, Application Insights et Analytique de journal.</span><span class="sxs-lookup"><span data-stu-id="88615-114">hello extension is used in conjunction with other Microsoft diagnostics products like Azure Monitor, Application Insights, and Log Analytics.</span></span>



<span data-ttu-id="88615-115">Télécharger la définition de schéma de fichier de configuration publique hello en exécutant hello suivant de commande PowerShell :</span><span class="sxs-lookup"><span data-stu-id="88615-115">Download hello public configuration file schema definition by executing hello following PowerShell command:</span></span>  

```powershell  
(Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File –Encoding utf8 -FilePath 'C:\temp\WadConfig.xsd'  
```  

<span data-ttu-id="88615-116">Pour plus d’informations sur l’utilisation d’Azure Diagnostics, voir [Extension Microsoft Azure Diagnostics](azure-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="88615-116">For more information about using Azure Diagnostics, see [Azure Diagnostics Extension](azure-diagnostics.md).</span></span>  

## <a name="example-of-hello-diagnostics-configuration-file"></a><span data-ttu-id="88615-117">Exemple de fichier de configuration de diagnostics hello</span><span class="sxs-lookup"><span data-stu-id="88615-117">Example of hello diagnostics configuration file</span></span>  
 <span data-ttu-id="88615-118">Bonjour à l’exemple suivant montre un fichier de configuration de diagnostics standard :</span><span class="sxs-lookup"><span data-stu-id="88615-118">hello following example shows a typical diagnostics configuration file:</span></span>  

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

<span data-ttu-id="88615-119">Équivalent JSON hello précédente XML du fichier de configuration.</span><span class="sxs-lookup"><span data-stu-id="88615-119">JSON equivalent of hello previous XML configuration file.</span></span> 

<span data-ttu-id="88615-120">Hello PublicConfig et PrivateConfig sont séparés, car dans la plupart des cas d’utilisation de json, ils sont passés en tant que variables différentes.</span><span class="sxs-lookup"><span data-stu-id="88615-120">hello PublicConfig and PrivateConfig are separated because in most json usage cases, they are passed as different variables.</span></span> <span data-ttu-id="88615-121">Ces cas incluent les modèles Resource Manager, le groupe de machines virtuelles identiques PowerShell et Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="88615-121">These cases include Resource Manager templates, Virtual Machine Scale set PowerShell, and Visual Studio.</span></span> 

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

## <a name="reading-this-page"></a><span data-ttu-id="88615-122">Lecture de cette page</span><span class="sxs-lookup"><span data-stu-id="88615-122">Reading this page</span></span>  
 <span data-ttu-id="88615-123">Hello balises suivant sont à peu près dans l’ordre indiqué dans le précédent exemple de hello.</span><span class="sxs-lookup"><span data-stu-id="88615-123">hello tags following are roughly in order shown in hello preceding example.</span></span>  <span data-ttu-id="88615-124">Si vous ne voyez pas une description complète à l’emplacement prévu, rechercher hello des page hello élément ou attribut.</span><span class="sxs-lookup"><span data-stu-id="88615-124">If you don't see a full description where you expect it, search hello page for hello element or attribute.</span></span>  

## <a name="common-attribute-types"></a><span data-ttu-id="88615-125">Types d’attributs courants</span><span class="sxs-lookup"><span data-stu-id="88615-125">Common Attribute Types</span></span>  
 <span data-ttu-id="88615-126">L’attribut **scheduledTransferPeriod** apparaît dans plusieurs éléments.</span><span class="sxs-lookup"><span data-stu-id="88615-126">**scheduledTransferPeriod** attribute appears in several elements.</span></span> <span data-ttu-id="88615-127">Il s’agit d’intervalle de salutation entre toostorage les transferts planifiés arrondi toohello minute la plus proche.</span><span class="sxs-lookup"><span data-stu-id="88615-127">It is hello interval between scheduled transfers toostorage rounded up toohello nearest minute.</span></span> <span data-ttu-id="88615-128">la valeur Hello est un [XML « Type de données de durée ».](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="88615-128">hello value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span>


## <a name="diagnosticsconfiguration-element"></a><span data-ttu-id="88615-129">Élément DiagnosticsConfiguration</span><span class="sxs-lookup"><span data-stu-id="88615-129">DiagnosticsConfiguration Element</span></span>  
 <span data-ttu-id="88615-130">*Tree: Root - DiagnosticsConfiguration*</span><span class="sxs-lookup"><span data-stu-id="88615-130">*Tree: Root - DiagnosticsConfiguration*</span></span>

<span data-ttu-id="88615-131">Ajouté à la version 1.3.</span><span class="sxs-lookup"><span data-stu-id="88615-131">Added in version 1.3.</span></span>  

<span data-ttu-id="88615-132">élément de niveau supérieur Hello hello diagnostics du fichier de configuration.</span><span class="sxs-lookup"><span data-stu-id="88615-132">hello top-level element of hello diagnostics configuration file.</span></span>  

<span data-ttu-id="88615-133">**Attribut** xmlns - hello espace de noms XML pour le fichier de configuration de diagnostics hello est :</span><span class="sxs-lookup"><span data-stu-id="88615-133">**Attribute**  xmlns - hello XML namespace for hello diagnostics configuration file is:</span></span>  
<span data-ttu-id="88615-134">http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration</span><span class="sxs-lookup"><span data-stu-id="88615-134">http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration</span></span>  


|<span data-ttu-id="88615-135">Éléments enfants</span><span class="sxs-lookup"><span data-stu-id="88615-135">Child Elements</span></span>|<span data-ttu-id="88615-136">Description</span><span class="sxs-lookup"><span data-stu-id="88615-136">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="88615-137">**PublicConfig**</span><span class="sxs-lookup"><span data-stu-id="88615-137">**PublicConfig**</span></span>|<span data-ttu-id="88615-138">Obligatoire.</span><span class="sxs-lookup"><span data-stu-id="88615-138">Required.</span></span> <span data-ttu-id="88615-139">Consultez la description sur cette page.</span><span class="sxs-lookup"><span data-stu-id="88615-139">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="88615-140">**PrivateConfig**</span><span class="sxs-lookup"><span data-stu-id="88615-140">**PrivateConfig**</span></span>|<span data-ttu-id="88615-141">facultatif.</span><span class="sxs-lookup"><span data-stu-id="88615-141">Optional.</span></span> <span data-ttu-id="88615-142">Consultez la description sur cette page.</span><span class="sxs-lookup"><span data-stu-id="88615-142">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="88615-143">**IsEnabled**</span><span class="sxs-lookup"><span data-stu-id="88615-143">**IsEnabled**</span></span>|<span data-ttu-id="88615-144">Booléen.</span><span class="sxs-lookup"><span data-stu-id="88615-144">Boolean.</span></span> <span data-ttu-id="88615-145">Consultez la description sur cette page.</span><span class="sxs-lookup"><span data-stu-id="88615-145">See description elsewhere on this page.</span></span>|  

## <a name="publicconfig-element"></a><span data-ttu-id="88615-146">Élément PublicConfig</span><span class="sxs-lookup"><span data-stu-id="88615-146">PublicConfig Element</span></span>  
 <span data-ttu-id="88615-147">*Tree: Root - DiagnosticsConfiguration - PublicConfig*</span><span class="sxs-lookup"><span data-stu-id="88615-147">*Tree: Root - DiagnosticsConfiguration - PublicConfig*</span></span>

 <span data-ttu-id="88615-148">Décrit la configuration des diagnostics publique hello.</span><span class="sxs-lookup"><span data-stu-id="88615-148">Describes hello public diagnostics configuration.</span></span>  

|<span data-ttu-id="88615-149">Éléments enfants</span><span class="sxs-lookup"><span data-stu-id="88615-149">Child Elements</span></span>|<span data-ttu-id="88615-150">Description</span><span class="sxs-lookup"><span data-stu-id="88615-150">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="88615-151">**WadCfg**</span><span class="sxs-lookup"><span data-stu-id="88615-151">**WadCfg**</span></span>|<span data-ttu-id="88615-152">Obligatoire.</span><span class="sxs-lookup"><span data-stu-id="88615-152">Required.</span></span> <span data-ttu-id="88615-153">Consultez la description sur cette page.</span><span class="sxs-lookup"><span data-stu-id="88615-153">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="88615-154">**StorageAccount**</span><span class="sxs-lookup"><span data-stu-id="88615-154">**StorageAccount**</span></span>|<span data-ttu-id="88615-155">nom de Hello de compte de stockage Azure hello toostore hello données dans.</span><span class="sxs-lookup"><span data-stu-id="88615-155">hello name of hello Azure Storage account toostore hello data in.</span></span> <span data-ttu-id="88615-156">Peut également être spécifié en tant que paramètre lorsque vous exécutez l’applet de commande hello AzureServiceDiagnosticsExtension de jeu.</span><span class="sxs-lookup"><span data-stu-id="88615-156">May also be specified as a parameter when executing hello Set-AzureServiceDiagnosticsExtension cmdlet.</span></span>|  
|<span data-ttu-id="88615-157">**StorageType**</span><span class="sxs-lookup"><span data-stu-id="88615-157">**StorageType**</span></span>|<span data-ttu-id="88615-158">Peut être *Table*, *Blob* ou *TableAndBlob*.</span><span class="sxs-lookup"><span data-stu-id="88615-158">Can be *Table*, *Blob*, or *TableAndBlob*.</span></span> <span data-ttu-id="88615-159">Table est la valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="88615-159">Table is default.</span></span> <span data-ttu-id="88615-160">Lorsque TableAndBlob est choisie, données de diagnostic sont enregistrées à deux reprises : une fois tooeach type.</span><span class="sxs-lookup"><span data-stu-id="88615-160">When TableAndBlob is chosen, diagnostic data is written twice -- once tooeach type.</span></span>|  
|<span data-ttu-id="88615-161">**LocalResourceDirectory**</span><span class="sxs-lookup"><span data-stu-id="88615-161">**LocalResourceDirectory**</span></span>|<span data-ttu-id="88615-162">répertoire Hello sur l’ordinateur virtuel de hello où hello Monitoring Agent stocke les données d’événement.</span><span class="sxs-lookup"><span data-stu-id="88615-162">hello directory on hello virtual machine where hello Monitoring Agent stores event data.</span></span> <span data-ttu-id="88615-163">Dans le cas contraire, valeur, le répertoire par défaut de hello est utilisé :</span><span class="sxs-lookup"><span data-stu-id="88615-163">If not, set, hello default directory is used:</span></span><br /><br /> <span data-ttu-id="88615-164">Pour un rôle Worker/web : `C:\Resources\<guid>\directory\<guid>.<RoleName.DiagnosticStore\`</span><span class="sxs-lookup"><span data-stu-id="88615-164">For a Worker/web role: `C:\Resources\<guid>\directory\<guid>.<RoleName.DiagnosticStore\`</span></span><br /><br /> <span data-ttu-id="88615-165">Pour une machine virtuelle : `C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<WADVersion>\WAD<WADVersion>`</span><span class="sxs-lookup"><span data-stu-id="88615-165">For a Virtual Machine: `C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<WADVersion>\WAD<WADVersion>`</span></span><br /><br /> <span data-ttu-id="88615-166">Les attributs requis sont :</span><span class="sxs-lookup"><span data-stu-id="88615-166">Required attributes are:</span></span><br /><br /> <span data-ttu-id="88615-167">- **chemin d’accès** - hello répertoire hello système toobe est utilisé par les Diagnostics Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="88615-167">- **path** - hello directory on hello system toobe used by Azure Diagnostics.</span></span><br /><br /> <span data-ttu-id="88615-168">- **expandEnvironment** -contrôle si les variables d’environnement sont développées dans le nom de chemin d’accès hello.</span><span class="sxs-lookup"><span data-stu-id="88615-168">- **expandEnvironment** - Controls whether environment variables are expanded in hello path name.</span></span>|  

## <a name="wadcfg-element"></a><span data-ttu-id="88615-169">WadCFG Element</span><span class="sxs-lookup"><span data-stu-id="88615-169">WadCFG Element</span></span>  
 <span data-ttu-id="88615-170">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG*</span><span class="sxs-lookup"><span data-stu-id="88615-170">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG*</span></span>
 
 <span data-ttu-id="88615-171">Identifie et configure toobe de données de télémétrie hello collectée.</span><span class="sxs-lookup"><span data-stu-id="88615-171">Identifies and configures hello telemetry data toobe collected.</span></span>  


## <a name="diagnosticmonitorconfiguration-element"></a><span data-ttu-id="88615-172">Élément DiagnosticMonitorConfiguration</span><span class="sxs-lookup"><span data-stu-id="88615-172">DiagnosticMonitorConfiguration Element</span></span> 
 <span data-ttu-id="88615-173">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration*</span><span class="sxs-lookup"><span data-stu-id="88615-173">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration*</span></span>

 <span data-ttu-id="88615-174">Requis</span><span class="sxs-lookup"><span data-stu-id="88615-174">Required</span></span> 

|<span data-ttu-id="88615-175">Attributs</span><span class="sxs-lookup"><span data-stu-id="88615-175">Attributes</span></span>|<span data-ttu-id="88615-176">Description</span><span class="sxs-lookup"><span data-stu-id="88615-176">Description</span></span>|  
|----------------|-----------------|  
| <span data-ttu-id="88615-177">**overallQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="88615-177">**overallQuotaInMB**</span></span> | <span data-ttu-id="88615-178">quantité maximale de Hello d’espace disque local qui peut être consommée par hello différents types de données de diagnostic collectées par Diagnostics Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="88615-178">hello maximum amount of local disk space that may be consumed by hello various types of diagnostic data collected by Azure Diagnostics.</span></span> <span data-ttu-id="88615-179">Hello par défaut est 5 120 Mo.</span><span class="sxs-lookup"><span data-stu-id="88615-179">hello default setting is 5120 MB.</span></span><br />
|<span data-ttu-id="88615-180">**useProxyServer**</span><span class="sxs-lookup"><span data-stu-id="88615-180">**useProxyServer**</span></span> | <span data-ttu-id="88615-181">Configurer les paramètres du serveur proxy Azure Diagnostics toouse hello comme dans les paramètres d’Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="88615-181">Configure Azure Diagnostics toouse hello proxy server settings as set in IE settings.</span></span>|  

<br /> <br />

|<span data-ttu-id="88615-182">Éléments enfants</span><span class="sxs-lookup"><span data-stu-id="88615-182">Child Elements</span></span>|<span data-ttu-id="88615-183">Description</span><span class="sxs-lookup"><span data-stu-id="88615-183">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="88615-184">**CrashDumps**</span><span class="sxs-lookup"><span data-stu-id="88615-184">**CrashDumps**</span></span>|<span data-ttu-id="88615-185">Consultez la description sur cette page.</span><span class="sxs-lookup"><span data-stu-id="88615-185">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="88615-186">**DiagnosticInfrastructureLogs**</span><span class="sxs-lookup"><span data-stu-id="88615-186">**DiagnosticInfrastructureLogs**</span></span>|<span data-ttu-id="88615-187">Permet la collecte des journaux générés par Azure Diagnostics.</span><span class="sxs-lookup"><span data-stu-id="88615-187">Enable collection of logs generated by Azure Diagnostics.</span></span> <span data-ttu-id="88615-188">journaux d’infrastructure de diagnostics Hello sont utiles pour la résolution des problèmes de système de diagnostic hello lui-même.</span><span class="sxs-lookup"><span data-stu-id="88615-188">hello diagnostic infrastructure logs are useful for troubleshooting hello diagnostics system itself.</span></span> <span data-ttu-id="88615-189">Les attributs facultatifs sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="88615-189">Optional attributes are:</span></span><br /><br /> <span data-ttu-id="88615-190">- **scheduledTransferLogLevelFilter** -configure le niveau de gravité minimal hello de journaux hello collecté.</span><span class="sxs-lookup"><span data-stu-id="88615-190">- **scheduledTransferLogLevelFilter** - Configures hello minimum severity level of hello logs collected.</span></span><br /><br /> <span data-ttu-id="88615-191">- **scheduledTransferPeriod** -intervalle hello entre les transferts planifiés toostorage arrondi toohello minute la plus proche.</span><span class="sxs-lookup"><span data-stu-id="88615-191">- **scheduledTransferPeriod** - hello interval between scheduled transfers toostorage rounded up toohello nearest minute.</span></span> <span data-ttu-id="88615-192">la valeur Hello est un [XML « Type de données de durée ».](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="88615-192">hello value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  
|<span data-ttu-id="88615-193">**Directories**</span><span class="sxs-lookup"><span data-stu-id="88615-193">**Directories**</span></span>|<span data-ttu-id="88615-194">Consultez la description sur cette page.</span><span class="sxs-lookup"><span data-stu-id="88615-194">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="88615-195">**EtwProviders**</span><span class="sxs-lookup"><span data-stu-id="88615-195">**EtwProviders**</span></span>|<span data-ttu-id="88615-196">Consultez la description sur cette page.</span><span class="sxs-lookup"><span data-stu-id="88615-196">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="88615-197">**Métriques**</span><span class="sxs-lookup"><span data-stu-id="88615-197">**Metrics**</span></span>|<span data-ttu-id="88615-198">Consultez la description sur cette page.</span><span class="sxs-lookup"><span data-stu-id="88615-198">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="88615-199">**PerformanceCounters**</span><span class="sxs-lookup"><span data-stu-id="88615-199">**PerformanceCounters**</span></span>|<span data-ttu-id="88615-200">Consultez la description sur cette page.</span><span class="sxs-lookup"><span data-stu-id="88615-200">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="88615-201">**WindowsEventLog**</span><span class="sxs-lookup"><span data-stu-id="88615-201">**WindowsEventLog**</span></span>|<span data-ttu-id="88615-202">Consultez la description sur cette page.</span><span class="sxs-lookup"><span data-stu-id="88615-202">See description elsewhere on this page.</span></span>| 
|<span data-ttu-id="88615-203">**DockerSources**</span><span class="sxs-lookup"><span data-stu-id="88615-203">**DockerSources**</span></span>|<span data-ttu-id="88615-204">Consultez la description sur cette page.</span><span class="sxs-lookup"><span data-stu-id="88615-204">See description elsewhere on this page.</span></span> | 



## <a name="crashdumps-element"></a><span data-ttu-id="88615-205">Élément CrashDumps</span><span class="sxs-lookup"><span data-stu-id="88615-205">CrashDumps Element</span></span>  
 <span data-ttu-id="88615-206">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - CrashDumps*</span><span class="sxs-lookup"><span data-stu-id="88615-206">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - CrashDumps*</span></span>
 
 <span data-ttu-id="88615-207">Activer la collecte de hello des vidages sur incident.</span><span class="sxs-lookup"><span data-stu-id="88615-207">Enable hello collection of crash dumps.</span></span>  

|<span data-ttu-id="88615-208">Attributs</span><span class="sxs-lookup"><span data-stu-id="88615-208">Attributes</span></span>|<span data-ttu-id="88615-209">Description</span><span class="sxs-lookup"><span data-stu-id="88615-209">Description</span></span>|  
|----------------|-----------------|  
|<span data-ttu-id="88615-210">**containerName**</span><span class="sxs-lookup"><span data-stu-id="88615-210">**containerName**</span></span>|<span data-ttu-id="88615-211">facultatif.</span><span class="sxs-lookup"><span data-stu-id="88615-211">Optional.</span></span> <span data-ttu-id="88615-212">nom de Hello du conteneur d’objets blob hello dans votre toobe de compte de stockage Azure utilisé des vidages sur incident de toostore.</span><span class="sxs-lookup"><span data-stu-id="88615-212">hello name of hello blob container in your Azure Storage account toobe used toostore crash dumps.</span></span>|  
|<span data-ttu-id="88615-213">**crashDumpType**</span><span class="sxs-lookup"><span data-stu-id="88615-213">**crashDumpType**</span></span>|<span data-ttu-id="88615-214">facultatif.</span><span class="sxs-lookup"><span data-stu-id="88615-214">Optional.</span></span>  <span data-ttu-id="88615-215">Configure les vidages sur incident de mini ou complète de toocollect de Diagnostics Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="88615-215">Configures Azure Diagnostics toocollect mini or full crash dumps.</span></span>|  
|<span data-ttu-id="88615-216">**directoryQuotaPercentage**</span><span class="sxs-lookup"><span data-stu-id="88615-216">**directoryQuotaPercentage**</span></span>|<span data-ttu-id="88615-217">facultatif.</span><span class="sxs-lookup"><span data-stu-id="88615-217">Optional.</span></span>  <span data-ttu-id="88615-218">Configure le pourcentage de hello de **overallQuotaInMB** toobe réservé pour les vidages sur incident sur hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="88615-218">Configures hello percentage of **overallQuotaInMB** toobe reserved for crash dumps on hello VM.</span></span>|  

|<span data-ttu-id="88615-219">Éléments enfants</span><span class="sxs-lookup"><span data-stu-id="88615-219">Child Elements</span></span>|<span data-ttu-id="88615-220">Description</span><span class="sxs-lookup"><span data-stu-id="88615-220">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="88615-221">**CrashDumpConfiguration**</span><span class="sxs-lookup"><span data-stu-id="88615-221">**CrashDumpConfiguration**</span></span>|<span data-ttu-id="88615-222">Obligatoire.</span><span class="sxs-lookup"><span data-stu-id="88615-222">Required.</span></span> <span data-ttu-id="88615-223">Définit les valeurs de configuration pour chaque processus.</span><span class="sxs-lookup"><span data-stu-id="88615-223">Defines configuration values for each process.</span></span><br /><br /> <span data-ttu-id="88615-224">Hello suivant l’attribut est également requis :</span><span class="sxs-lookup"><span data-stu-id="88615-224">hello following attribute is also required:</span></span><br /><br /> <span data-ttu-id="88615-225">**processName** hello - nom de hello processus Azure Diagnostics toocollect un vidage sur incident pour.</span><span class="sxs-lookup"><span data-stu-id="88615-225">**processName** - hello name of hello process you want Azure Diagnostics toocollect a crash dump for.</span></span>|  

## <a name="directories-element"></a><span data-ttu-id="88615-226">Élément Directories</span><span class="sxs-lookup"><span data-stu-id="88615-226">Directories Element</span></span> 
 <span data-ttu-id="88615-227">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration -  Directories*</span><span class="sxs-lookup"><span data-stu-id="88615-227">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration -  Directories*</span></span>

 <span data-ttu-id="88615-228">Active hello collection de contenu hello d’un répertoire, IIS ayant échoué, journaux de demandes d’accès et/ou les journaux IIS.</span><span class="sxs-lookup"><span data-stu-id="88615-228">Enables hello collection of hello contents of a directory, IIS failed access request logs and/or IIS logs.</span></span>  

 <span data-ttu-id="88615-229">Attribut **scheduledTransferPeriod** facultatif.</span><span class="sxs-lookup"><span data-stu-id="88615-229">Optional **scheduledTransferPeriod** attribute.</span></span> <span data-ttu-id="88615-230">Voir l’explication précédente.</span><span class="sxs-lookup"><span data-stu-id="88615-230">See explanation earlier.</span></span>  

|<span data-ttu-id="88615-231">Éléments enfants</span><span class="sxs-lookup"><span data-stu-id="88615-231">Child Elements</span></span>|<span data-ttu-id="88615-232">Description</span><span class="sxs-lookup"><span data-stu-id="88615-232">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="88615-233">**IISLogs**</span><span class="sxs-lookup"><span data-stu-id="88615-233">**IISLogs**</span></span>|<span data-ttu-id="88615-234">Y compris de cet élément dans la configuration de hello permet la collection hello de journaux IIS :</span><span class="sxs-lookup"><span data-stu-id="88615-234">Including this element in hello configuration enables hello collection of IIS logs:</span></span><br /><br /> <span data-ttu-id="88615-235">**containerName** -nom hello du conteneur d’objets blob hello dans votre toobe de compte de stockage Azure utilisé les journaux IIS toostore hello.</span><span class="sxs-lookup"><span data-stu-id="88615-235">**containerName** - hello name of hello blob container in your Azure Storage account toobe used toostore hello IIS logs.</span></span>|   
|<span data-ttu-id="88615-236">**FailedRequestLogs**</span><span class="sxs-lookup"><span data-stu-id="88615-236">**FailedRequestLogs**</span></span>|<span data-ttu-id="88615-237">Y compris de cet élément dans la configuration de hello permet de collection de journaux sur des demandes ayant échoué tooan IIS site ou application.</span><span class="sxs-lookup"><span data-stu-id="88615-237">Including this element in hello configuration enables collection of logs about failed requests tooan IIS site or application.</span></span> <span data-ttu-id="88615-238">Vous devez également activer les options de suivi sous **system.WebServer** dans **Web.config**.</span><span class="sxs-lookup"><span data-stu-id="88615-238">You must also enable tracing options under **system.WebServer** in **Web.config**.</span></span>|  
|<span data-ttu-id="88615-239">**DataSources**</span><span class="sxs-lookup"><span data-stu-id="88615-239">**DataSources**</span></span>|<span data-ttu-id="88615-240">Une liste de répertoires toomonitor.</span><span class="sxs-lookup"><span data-stu-id="88615-240">A list of directories toomonitor.</span></span>| 




## <a name="datasources-element"></a><span data-ttu-id="88615-241">Élément DataSources</span><span class="sxs-lookup"><span data-stu-id="88615-241">DataSources Element</span></span>  
 <span data-ttu-id="88615-242">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories - DataSources*</span><span class="sxs-lookup"><span data-stu-id="88615-242">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories - DataSources*</span></span>

 <span data-ttu-id="88615-243">Une liste de répertoires toomonitor.</span><span class="sxs-lookup"><span data-stu-id="88615-243">A list of directories toomonitor.</span></span>  

|<span data-ttu-id="88615-244">Éléments enfants</span><span class="sxs-lookup"><span data-stu-id="88615-244">Child Elements</span></span>|<span data-ttu-id="88615-245">Description</span><span class="sxs-lookup"><span data-stu-id="88615-245">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="88615-246">**DirectoryConfiguration**</span><span class="sxs-lookup"><span data-stu-id="88615-246">**DirectoryConfiguration**</span></span>|<span data-ttu-id="88615-247">Obligatoire.</span><span class="sxs-lookup"><span data-stu-id="88615-247">Required.</span></span> <span data-ttu-id="88615-248">Attribut requis :</span><span class="sxs-lookup"><span data-stu-id="88615-248">Required attribute:</span></span><br /><br /> <span data-ttu-id="88615-249">**containerName** hello - nom du conteneur d’objets blob hello dans votre compte de stockage Azure qui toobe utilisé des fichiers journaux toostore hello.</span><span class="sxs-lookup"><span data-stu-id="88615-249">**containerName** - hello name of hello blob container in your Azure Storage account that toobe used toostore hello log files.</span></span>|  





## <a name="directoryconfiguration-element"></a><span data-ttu-id="88615-250">Élément DirectoryConfiguration</span><span class="sxs-lookup"><span data-stu-id="88615-250">DirectoryConfiguration Element</span></span>  
 <span data-ttu-id="88615-251">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories - DataSources - DirectoryConfiguration*</span><span class="sxs-lookup"><span data-stu-id="88615-251">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories - DataSources - DirectoryConfiguration*</span></span>

 <span data-ttu-id="88615-252">Peuvent inclure deux hello **absolu** ou **LocalResource** élément mais pas les deux.</span><span class="sxs-lookup"><span data-stu-id="88615-252">May include either hello **Absolute** or **LocalResource** element but not both.</span></span>  

|<span data-ttu-id="88615-253">Éléments enfants</span><span class="sxs-lookup"><span data-stu-id="88615-253">Child Elements</span></span>|<span data-ttu-id="88615-254">Description</span><span class="sxs-lookup"><span data-stu-id="88615-254">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="88615-255">**Absolute**</span><span class="sxs-lookup"><span data-stu-id="88615-255">**Absolute**</span></span>|<span data-ttu-id="88615-256">Bonjour toomonitor de répertoire toohello de chemin d’accès absolu.</span><span class="sxs-lookup"><span data-stu-id="88615-256">hello absolute path toohello directory toomonitor.</span></span> <span data-ttu-id="88615-257">Hello suivant des attributs est requis :</span><span class="sxs-lookup"><span data-stu-id="88615-257">hello following attributes are required:</span></span><br /><br /> <span data-ttu-id="88615-258">- **Chemin d’accès** -hello toomonitor de répertoire toohello de chemin d’accès absolu.</span><span class="sxs-lookup"><span data-stu-id="88615-258">- **Path** - hello absolute path toohello directory toomonitor.</span></span><br /><br /> <span data-ttu-id="88615-259">- **expandEnvironment** - Détermine si les variables d’environnement de Path sont développées.</span><span class="sxs-lookup"><span data-stu-id="88615-259">- **expandEnvironment** - Configures whether environment variables in Path are expanded.</span></span>|  
|<span data-ttu-id="88615-260">**LocalResource**</span><span class="sxs-lookup"><span data-stu-id="88615-260">**LocalResource**</span></span>|<span data-ttu-id="88615-261">Bonjour toomonitor de chemin d’accès relatif tooa ressource locale.</span><span class="sxs-lookup"><span data-stu-id="88615-261">hello path relative tooa local resource toomonitor.</span></span> <span data-ttu-id="88615-262">Les attributs requis sont :</span><span class="sxs-lookup"><span data-stu-id="88615-262">Required attributes are:</span></span><br /><br /> <span data-ttu-id="88615-263">- **Nom** -hello ressource locale contenant hello Active toomonitor</span><span class="sxs-lookup"><span data-stu-id="88615-263">- **Name** - hello local resource that contains hello directory toomonitor</span></span><br /><br /> <span data-ttu-id="88615-264">- **relativePath** -hello du chemin d’accès relatif tooName contenant hello Active toomonitor</span><span class="sxs-lookup"><span data-stu-id="88615-264">- **relativePath** - hello path relative tooName that contains hello directory toomonitor</span></span>|  



## <a name="etwproviders-element"></a><span data-ttu-id="88615-265">Élément EtwProviders</span><span class="sxs-lookup"><span data-stu-id="88615-265">EtwProviders Element</span></span>  
 <span data-ttu-id="88615-266">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders*</span><span class="sxs-lookup"><span data-stu-id="88615-266">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders*</span></span>

 <span data-ttu-id="88615-267">Configure la collecte d’événements ETW issus des fournisseurs de manifeste EventSource et/ou ETW.</span><span class="sxs-lookup"><span data-stu-id="88615-267">Configures collection of ETW events from EventSource and/or ETW Manifest based providers.</span></span>  

|<span data-ttu-id="88615-268">Éléments enfants</span><span class="sxs-lookup"><span data-stu-id="88615-268">Child Elements</span></span>|<span data-ttu-id="88615-269">Description</span><span class="sxs-lookup"><span data-stu-id="88615-269">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="88615-270">**EtwEventSourceProviderConfiguration**</span><span class="sxs-lookup"><span data-stu-id="88615-270">**EtwEventSourceProviderConfiguration**</span></span>|<span data-ttu-id="88615-271">Configure la collection d’événements générés à partir de la [classe EventSource](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="88615-271">Configures collection of events generated from [EventSource Class](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).</span></span> <span data-ttu-id="88615-272">Attribut requis :</span><span class="sxs-lookup"><span data-stu-id="88615-272">Required attribute:</span></span><br /><br /> <span data-ttu-id="88615-273">**fournisseur** -nom de la classe d’événement de EventSource hello hello.</span><span class="sxs-lookup"><span data-stu-id="88615-273">**provider** - hello class name of hello EventSource event.</span></span><br /><br /> <span data-ttu-id="88615-274">Les attributs facultatifs sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="88615-274">Optional attributes are:</span></span><br /><br /> <span data-ttu-id="88615-275">- **scheduledTransferLogLevelFilter** -hello compte de stockage de gravité minimal niveau tootransfer tooyour.</span><span class="sxs-lookup"><span data-stu-id="88615-275">- **scheduledTransferLogLevelFilter** - hello minimum severity level tootransfer tooyour storage account.</span></span><br /><br /> <span data-ttu-id="88615-276">- **scheduledTransferPeriod** -intervalle hello entre les transferts planifiés toostorage arrondi toohello minute la plus proche.</span><span class="sxs-lookup"><span data-stu-id="88615-276">- **scheduledTransferPeriod** - hello interval between scheduled transfers toostorage rounded up toohello nearest minute.</span></span> <span data-ttu-id="88615-277">la valeur Hello est un [XML « Type de données de durée ».](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="88615-277">hello value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  
|<span data-ttu-id="88615-278">**EtwManifestProviderConfiguration**</span><span class="sxs-lookup"><span data-stu-id="88615-278">**EtwManifestProviderConfiguration**</span></span>|<span data-ttu-id="88615-279">Attribut requis :</span><span class="sxs-lookup"><span data-stu-id="88615-279">Required attribute:</span></span><br /><br /> <span data-ttu-id="88615-280">**fournisseur** -hello GUID du fournisseur d’événements hello</span><span class="sxs-lookup"><span data-stu-id="88615-280">**provider** - hello GUID of hello event provider</span></span><br /><br /> <span data-ttu-id="88615-281">Les attributs facultatifs sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="88615-281">Optional attributes are:</span></span><br /><br /> <span data-ttu-id="88615-282">- **scheduledTransferLogLevelFilter** -hello compte de stockage de gravité minimal niveau tootransfer tooyour.</span><span class="sxs-lookup"><span data-stu-id="88615-282">- **scheduledTransferLogLevelFilter** - hello minimum severity level tootransfer tooyour storage account.</span></span><br /><br /> <span data-ttu-id="88615-283">- **scheduledTransferPeriod** -intervalle hello entre les transferts planifiés toostorage arrondi toohello minute la plus proche.</span><span class="sxs-lookup"><span data-stu-id="88615-283">- **scheduledTransferPeriod** - hello interval between scheduled transfers toostorage rounded up toohello nearest minute.</span></span> <span data-ttu-id="88615-284">la valeur Hello est un [XML « Type de données de durée ».](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="88615-284">hello value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  



## <a name="etweventsourceproviderconfiguration-element"></a><span data-ttu-id="88615-285">EtwEventSourceProviderConfiguration Element</span><span class="sxs-lookup"><span data-stu-id="88615-285">EtwEventSourceProviderConfiguration Element</span></span>  
 <span data-ttu-id="88615-286">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders- EtwEventSourceProviderConfiguration*</span><span class="sxs-lookup"><span data-stu-id="88615-286">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders- EtwEventSourceProviderConfiguration*</span></span>

 <span data-ttu-id="88615-287">Configure la collection d’événements générés à partir de la [classe EventSource](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="88615-287">Configures collection of events generated from [EventSource Class](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).</span></span>  

|<span data-ttu-id="88615-288">Éléments enfants</span><span class="sxs-lookup"><span data-stu-id="88615-288">Child Elements</span></span>|<span data-ttu-id="88615-289">Description</span><span class="sxs-lookup"><span data-stu-id="88615-289">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="88615-290">**DefaultEvents**</span><span class="sxs-lookup"><span data-stu-id="88615-290">**DefaultEvents**</span></span>|<span data-ttu-id="88615-291">Attribut facultatif :</span><span class="sxs-lookup"><span data-stu-id="88615-291">Optional attribute:</span></span><br/><br/> <span data-ttu-id="88615-292">**eventDestination** - hello nom hello toostore hello d’événements de table dans</span><span class="sxs-lookup"><span data-stu-id="88615-292">**eventDestination** - hello name of hello table toostore hello events in</span></span>|  
|<span data-ttu-id="88615-293">**Event**</span><span class="sxs-lookup"><span data-stu-id="88615-293">**Event**</span></span>|<span data-ttu-id="88615-294">Attribut requis :</span><span class="sxs-lookup"><span data-stu-id="88615-294">Required attribute:</span></span><br /><br /> <span data-ttu-id="88615-295">**ID** -id hello d’événement de hello.</span><span class="sxs-lookup"><span data-stu-id="88615-295">**id** - hello id of hello event.</span></span><br /><br /> <span data-ttu-id="88615-296">Attribut facultatif :</span><span class="sxs-lookup"><span data-stu-id="88615-296">Optional attribute:</span></span><br /><br /> <span data-ttu-id="88615-297">**eventDestination** - hello nom hello toostore hello d’événements de table dans</span><span class="sxs-lookup"><span data-stu-id="88615-297">**eventDestination** - hello name of hello table toostore hello events in</span></span>|  



## <a name="etwmanifestproviderconfiguration-element"></a><span data-ttu-id="88615-298">EtwManifestProviderConfiguration Element</span><span class="sxs-lookup"><span data-stu-id="88615-298">EtwManifestProviderConfiguration Element</span></span>  
 <span data-ttu-id="88615-299">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders - EtwManifestProviderConfiguration*</span><span class="sxs-lookup"><span data-stu-id="88615-299">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders - EtwManifestProviderConfiguration*</span></span>

|<span data-ttu-id="88615-300">Éléments enfants</span><span class="sxs-lookup"><span data-stu-id="88615-300">Child Elements</span></span>|<span data-ttu-id="88615-301">Description</span><span class="sxs-lookup"><span data-stu-id="88615-301">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="88615-302">**DefaultEvents**</span><span class="sxs-lookup"><span data-stu-id="88615-302">**DefaultEvents**</span></span>|<span data-ttu-id="88615-303">Attribut facultatif :</span><span class="sxs-lookup"><span data-stu-id="88615-303">Optional attribute:</span></span><br /><br /> <span data-ttu-id="88615-304">**eventDestination** - hello nom hello toostore hello d’événements de table dans</span><span class="sxs-lookup"><span data-stu-id="88615-304">**eventDestination** - hello name of hello table toostore hello events in</span></span>|  
|<span data-ttu-id="88615-305">**Event**</span><span class="sxs-lookup"><span data-stu-id="88615-305">**Event**</span></span>|<span data-ttu-id="88615-306">Attribut requis :</span><span class="sxs-lookup"><span data-stu-id="88615-306">Required attribute:</span></span><br /><br /> <span data-ttu-id="88615-307">**ID** -id hello d’événement de hello.</span><span class="sxs-lookup"><span data-stu-id="88615-307">**id** - hello id of hello event.</span></span><br /><br /> <span data-ttu-id="88615-308">Attribut facultatif :</span><span class="sxs-lookup"><span data-stu-id="88615-308">Optional attribute:</span></span><br /><br /> <span data-ttu-id="88615-309">**eventDestination** - hello nom hello toostore hello d’événements de table dans</span><span class="sxs-lookup"><span data-stu-id="88615-309">**eventDestination** - hello name of hello table toostore hello events in</span></span>|  



## <a name="metrics-element"></a><span data-ttu-id="88615-310">Élément Metrics</span><span class="sxs-lookup"><span data-stu-id="88615-310">Metrics Element</span></span>  
 <span data-ttu-id="88615-311">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Metrics*</span><span class="sxs-lookup"><span data-stu-id="88615-311">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Metrics*</span></span>

 <span data-ttu-id="88615-312">Vous permet de toogenerate une table de compteur de performances est optimisée pour les requêtes rapides.</span><span class="sxs-lookup"><span data-stu-id="88615-312">Enables you toogenerate a performance counter table that is optimized for fast queries.</span></span> <span data-ttu-id="88615-313">Chaque compteur de performance qui est défini dans hello **PerformanceCounters** élément est stocké dans la table des métriques hello dans la table de compteur de Performance toohello Ajout.</span><span class="sxs-lookup"><span data-stu-id="88615-313">Each performance counter that is defined in hello **PerformanceCounters** element is stored in hello Metrics table in addition toohello Performance Counter table.</span></span>  

 <span data-ttu-id="88615-314">Hello **resourceId** attribut est requis.</span><span class="sxs-lookup"><span data-stu-id="88615-314">hello **resourceId** attribute is required.</span></span>  <span data-ttu-id="88615-315">ID de ressource Hello Hello Machine virtuelle que vous déployez des Diagnostics Windows Azure à.</span><span class="sxs-lookup"><span data-stu-id="88615-315">hello resource ID of hello Virtual Machine you are deploying Azure Diagnostics to.</span></span> <span data-ttu-id="88615-316">Obtenir hello **resourceID** de hello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="88615-316">Get hello **resourceID** from hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="88615-317">Sélectionnez **Parcourir** -> **Groupe de ressources** -> **<>\>**.</span><span class="sxs-lookup"><span data-stu-id="88615-317">Select **Browse** -> **Resource Groups** -> **<Name\>**.</span></span> <span data-ttu-id="88615-318">Cliquez sur hello **propriétés** vignette et copiez la valeur de hello hello **ID** champ.</span><span class="sxs-lookup"><span data-stu-id="88615-318">Click hello **Properties** tile and copy hello value from hello **ID** field.</span></span>  

|<span data-ttu-id="88615-319">Éléments enfants</span><span class="sxs-lookup"><span data-stu-id="88615-319">Child Elements</span></span>|<span data-ttu-id="88615-320">Description</span><span class="sxs-lookup"><span data-stu-id="88615-320">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="88615-321">**MetricAggregation**</span><span class="sxs-lookup"><span data-stu-id="88615-321">**MetricAggregation**</span></span>|<span data-ttu-id="88615-322">Attribut requis :</span><span class="sxs-lookup"><span data-stu-id="88615-322">Required attribute:</span></span><br /><br /> <span data-ttu-id="88615-323">**scheduledTransferPeriod** -intervalle hello entre les transferts planifiés toostorage arrondi toohello minute la plus proche.</span><span class="sxs-lookup"><span data-stu-id="88615-323">**scheduledTransferPeriod** - hello interval between scheduled transfers toostorage rounded up toohello nearest minute.</span></span> <span data-ttu-id="88615-324">la valeur Hello est un [XML « Type de données de durée ».](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="88615-324">hello value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  



## <a name="performancecounters-element"></a><span data-ttu-id="88615-325">Élément PerformanceCounters</span><span class="sxs-lookup"><span data-stu-id="88615-325">PerformanceCounters Element</span></span>  
 <span data-ttu-id="88615-326">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - PerformanceCounters*</span><span class="sxs-lookup"><span data-stu-id="88615-326">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - PerformanceCounters*</span></span>

 <span data-ttu-id="88615-327">Active la collecte de hello des compteurs de performance.</span><span class="sxs-lookup"><span data-stu-id="88615-327">Enables hello collection of performance counters.</span></span>  

 <span data-ttu-id="88615-328">Attribut facultatif :</span><span class="sxs-lookup"><span data-stu-id="88615-328">Optional attribute:</span></span>  

 <span data-ttu-id="88615-329">Attribut **scheduledTransferPeriod** facultatif.</span><span class="sxs-lookup"><span data-stu-id="88615-329">Optional **scheduledTransferPeriod** attribute.</span></span> <span data-ttu-id="88615-330">Voir l’explication précédente.</span><span class="sxs-lookup"><span data-stu-id="88615-330">See explanation earlier.</span></span>

|<span data-ttu-id="88615-331">Élément enfant</span><span class="sxs-lookup"><span data-stu-id="88615-331">Child Element</span></span>|<span data-ttu-id="88615-332">Description</span><span class="sxs-lookup"><span data-stu-id="88615-332">Description</span></span>|  
|-------------------|-----------------|  
|<span data-ttu-id="88615-333">**PerformanceCounterConfiguration**</span><span class="sxs-lookup"><span data-stu-id="88615-333">**PerformanceCounterConfiguration**</span></span>|<span data-ttu-id="88615-334">Hello suivant des attributs est requis :</span><span class="sxs-lookup"><span data-stu-id="88615-334">hello following attributes are required:</span></span><br /><br /> <span data-ttu-id="88615-335">- **counterSpecifier** - hello nom hello compteur de performance.</span><span class="sxs-lookup"><span data-stu-id="88615-335">- **counterSpecifier** - hello name of hello performance counter.</span></span> <span data-ttu-id="88615-336">Par exemple, `\Processor(_Total)\% Processor Time`.</span><span class="sxs-lookup"><span data-stu-id="88615-336">For example, `\Processor(_Total)\% Processor Time`.</span></span> <span data-ttu-id="88615-337">tooget une liste des performances des compteurs sur votre ordinateur hôte, exécutez la commande hello `typeperf`.</span><span class="sxs-lookup"><span data-stu-id="88615-337">tooget a list of performance counters on your host, run hello command `typeperf`.</span></span><br /><br /> <span data-ttu-id="88615-338">- **sampleRate** -fréquence hello compteur doit être échantillonné.</span><span class="sxs-lookup"><span data-stu-id="88615-338">- **sampleRate** - How often hello counter should be sampled.</span></span><br /><br /> <span data-ttu-id="88615-339">Attribut facultatif :</span><span class="sxs-lookup"><span data-stu-id="88615-339">Optional attribute:</span></span><br /><br /> <span data-ttu-id="88615-340">**unité** -unité de mesure du compteur de hello de hello.</span><span class="sxs-lookup"><span data-stu-id="88615-340">**unit** - hello unit of measure of hello counter.</span></span>|  




## <a name="windowseventlog-element"></a><span data-ttu-id="88615-341">Élément WindowsEventLog</span><span class="sxs-lookup"><span data-stu-id="88615-341">WindowsEventLog Element</span></span>
 <span data-ttu-id="88615-342">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - WindowsEventLog*</span><span class="sxs-lookup"><span data-stu-id="88615-342">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - WindowsEventLog*</span></span>
 
 <span data-ttu-id="88615-343">Active la collecte de hello des journaux des événements Windows.</span><span class="sxs-lookup"><span data-stu-id="88615-343">Enables hello collection of Windows Event Logs.</span></span>  

 <span data-ttu-id="88615-344">Attribut **scheduledTransferPeriod** facultatif.</span><span class="sxs-lookup"><span data-stu-id="88615-344">Optional **scheduledTransferPeriod** attribute.</span></span> <span data-ttu-id="88615-345">Voir l’explication précédente.</span><span class="sxs-lookup"><span data-stu-id="88615-345">See explanation  earlier.</span></span>  

|<span data-ttu-id="88615-346">Élément enfant</span><span class="sxs-lookup"><span data-stu-id="88615-346">Child Element</span></span>|<span data-ttu-id="88615-347">Description</span><span class="sxs-lookup"><span data-stu-id="88615-347">Description</span></span>|  
|-------------------|-----------------|  
|<span data-ttu-id="88615-348">**DataSource**</span><span class="sxs-lookup"><span data-stu-id="88615-348">**DataSource**</span></span>|<span data-ttu-id="88615-349">Hello toocollect de journaux des événements Windows.</span><span class="sxs-lookup"><span data-stu-id="88615-349">hello Windows Event logs toocollect.</span></span> <span data-ttu-id="88615-350">Attribut requis :</span><span class="sxs-lookup"><span data-stu-id="88615-350">Required attribute:</span></span><br /><br /> <span data-ttu-id="88615-351">**nom** -requête XPath de hello décrivant hello windows événements toobe collectées.</span><span class="sxs-lookup"><span data-stu-id="88615-351">**name** - hello XPath query describing hello windows events toobe collected.</span></span> <span data-ttu-id="88615-352">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="88615-352">For example:</span></span><br /><br /> `Application!*[System[(Level <=3)]], System!*[System[(Level <=3)]], System!*[System[Provider[@Name='Microsoft Antimalware']]], Security!*[System[(Level <= 3)]`<br /><br /> <span data-ttu-id="88615-353">tous les événements, de toocollect spécifier « * »</span><span class="sxs-lookup"><span data-stu-id="88615-353">toocollect all events, specify "*"</span></span>|  




## <a name="logs-element"></a><span data-ttu-id="88615-354">Élément Logs</span><span class="sxs-lookup"><span data-stu-id="88615-354">Logs Element</span></span>  
 <span data-ttu-id="88615-355">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Logs*</span><span class="sxs-lookup"><span data-stu-id="88615-355">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Logs*</span></span>

 <span data-ttu-id="88615-356">Présent dans la version 1.0 et 1.1.</span><span class="sxs-lookup"><span data-stu-id="88615-356">Present in version 1.0 and 1.1.</span></span> <span data-ttu-id="88615-357">Absent dans la version 1.2.</span><span class="sxs-lookup"><span data-stu-id="88615-357">Missing in 1.2.</span></span> <span data-ttu-id="88615-358">Rajouté dans la version 1.3.</span><span class="sxs-lookup"><span data-stu-id="88615-358">Added back in 1.3.</span></span>  

 <span data-ttu-id="88615-359">Définit la configuration du tampon hello pour les journaux Azure de base.</span><span class="sxs-lookup"><span data-stu-id="88615-359">Defines hello buffer configuration for basic Azure logs.</span></span>  

|<span data-ttu-id="88615-360">Attribut</span><span class="sxs-lookup"><span data-stu-id="88615-360">Attribute</span></span>|<span data-ttu-id="88615-361">Type</span><span class="sxs-lookup"><span data-stu-id="88615-361">Type</span></span>|<span data-ttu-id="88615-362">Description</span><span class="sxs-lookup"><span data-stu-id="88615-362">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="88615-363">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="88615-363">**bufferQuotaInMB**</span></span>|<span data-ttu-id="88615-364">**unsignedInt**</span><span class="sxs-lookup"><span data-stu-id="88615-364">**unsignedInt**</span></span>|<span data-ttu-id="88615-365">facultatif.</span><span class="sxs-lookup"><span data-stu-id="88615-365">Optional.</span></span> <span data-ttu-id="88615-366">Spécifie la quantité maximale de hello du stockage de système de fichiers est disponible pour hello spécifié données.</span><span class="sxs-lookup"><span data-stu-id="88615-366">Specifies hello maximum amount of file system storage that is available for hello specified data.</span></span><br /><br /> <span data-ttu-id="88615-367">valeur par défaut Hello est 0.</span><span class="sxs-lookup"><span data-stu-id="88615-367">hello default is 0.</span></span>|  
|<span data-ttu-id="88615-368">**scheduledTransferLogLevelFilterr**</span><span class="sxs-lookup"><span data-stu-id="88615-368">**scheduledTransferLogLevelFilterr**</span></span>|<span data-ttu-id="88615-369">**string**</span><span class="sxs-lookup"><span data-stu-id="88615-369">**string**</span></span>|<span data-ttu-id="88615-370">facultatif.</span><span class="sxs-lookup"><span data-stu-id="88615-370">Optional.</span></span> <span data-ttu-id="88615-371">Spécifie le niveau de gravité minimal hello pour les entrées de journal sont transférées.</span><span class="sxs-lookup"><span data-stu-id="88615-371">Specifies hello minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="88615-372">la valeur par défaut Hello est **Undefined**, qui transfère tous les journaux.</span><span class="sxs-lookup"><span data-stu-id="88615-372">hello default value is **Undefined**, which transfers all logs.</span></span> <span data-ttu-id="88615-373">Les autres valeurs possibles (dans l’ordre de la plupart des informations tooleast) sont **Verbose**, **informations**, **avertissement**, **erreur**et **Critiques**.</span><span class="sxs-lookup"><span data-stu-id="88615-373">Other possible values (in order of most tooleast information) are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="88615-374">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="88615-374">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="88615-375">**duration**</span><span class="sxs-lookup"><span data-stu-id="88615-375">**duration**</span></span>|<span data-ttu-id="88615-376">facultatif.</span><span class="sxs-lookup"><span data-stu-id="88615-376">Optional.</span></span> <span data-ttu-id="88615-377">Spécifie l’intervalle de salutation entre les transferts planifiés de données, arrondies à toohello minute la plus proche.</span><span class="sxs-lookup"><span data-stu-id="88615-377">Specifies hello interval between scheduled transfers of data, rounded up toohello nearest minute.</span></span><br /><br /> <span data-ttu-id="88615-378">valeur par défaut Hello est PT0S.</span><span class="sxs-lookup"><span data-stu-id="88615-378">hello default is PT0S.</span></span>|  
|<span data-ttu-id="88615-379">**sinks** - Ajouté à la version 1.5</span><span class="sxs-lookup"><span data-stu-id="88615-379">**sinks** Added in 1.5</span></span>|<span data-ttu-id="88615-380">**string**</span><span class="sxs-lookup"><span data-stu-id="88615-380">**string**</span></span>|<span data-ttu-id="88615-381">facultatif.</span><span class="sxs-lookup"><span data-stu-id="88615-381">Optional.</span></span> <span data-ttu-id="88615-382">Points tooa récepteur emplacement tooalso envoyer des données de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="88615-382">Points tooa sink location tooalso send diagnostic data.</span></span> <span data-ttu-id="88615-383">Par exemple, Application Insights.</span><span class="sxs-lookup"><span data-stu-id="88615-383">For example, Application Insights.</span></span>|  

## <a name="dockersources"></a><span data-ttu-id="88615-384">DockerSources</span><span class="sxs-lookup"><span data-stu-id="88615-384">DockerSources</span></span>
 <span data-ttu-id="88615-385">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - DockerSources*</span><span class="sxs-lookup"><span data-stu-id="88615-385">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - DockerSources*</span></span>

 <span data-ttu-id="88615-386">Ajouté dans 1.9.</span><span class="sxs-lookup"><span data-stu-id="88615-386">Added in 1.9.</span></span>

|<span data-ttu-id="88615-387">Nom de l’élément</span><span class="sxs-lookup"><span data-stu-id="88615-387">Element Name</span></span>|<span data-ttu-id="88615-388">Description</span><span class="sxs-lookup"><span data-stu-id="88615-388">Description</span></span>|  
|------------------|-----------------|  
|<span data-ttu-id="88615-389">**Stats**</span><span class="sxs-lookup"><span data-stu-id="88615-389">**Stats**</span></span>|<span data-ttu-id="88615-390">Indique au système de hello toocollect des statistiques pour les conteneurs Docker</span><span class="sxs-lookup"><span data-stu-id="88615-390">Tells hello system toocollect stats for Docker containers</span></span>|  

## <a name="sinksconfig-element"></a><span data-ttu-id="88615-391">Élément SinksConfig</span><span class="sxs-lookup"><span data-stu-id="88615-391">SinksConfig Element</span></span>  
 <span data-ttu-id="88615-392">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig*</span><span class="sxs-lookup"><span data-stu-id="88615-392">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig*</span></span>

 <span data-ttu-id="88615-393">Liste des emplacements toosend diagnostics données tooand hello configuration associée à ces emplacements.</span><span class="sxs-lookup"><span data-stu-id="88615-393">A list of locations toosend diagnostics data tooand hello configuration associated with those locations.</span></span>  

|<span data-ttu-id="88615-394">Nom de l’élément</span><span class="sxs-lookup"><span data-stu-id="88615-394">Element Name</span></span>|<span data-ttu-id="88615-395">Description</span><span class="sxs-lookup"><span data-stu-id="88615-395">Description</span></span>|  
|------------------|-----------------|  
|<span data-ttu-id="88615-396">**Section sink**</span><span class="sxs-lookup"><span data-stu-id="88615-396">**Sink**</span></span>|<span data-ttu-id="88615-397">Consultez la description sur cette page.</span><span class="sxs-lookup"><span data-stu-id="88615-397">See description elsewhere on this page.</span></span>|  

## <a name="sink-element"></a><span data-ttu-id="88615-398">Élément Sink</span><span class="sxs-lookup"><span data-stu-id="88615-398">Sink Element</span></span>
 <span data-ttu-id="88615-399">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink*</span><span class="sxs-lookup"><span data-stu-id="88615-399">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink*</span></span>

 <span data-ttu-id="88615-400">Ajouté à la version 1.5.</span><span class="sxs-lookup"><span data-stu-id="88615-400">Added in version 1.5.</span></span>  

 <span data-ttu-id="88615-401">Définit les emplacements toosend données de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="88615-401">Defines locations toosend diagnostic data to.</span></span> <span data-ttu-id="88615-402">Par exemple, hello service Application Insights.</span><span class="sxs-lookup"><span data-stu-id="88615-402">For example, hello Application Insights service.</span></span>  

|<span data-ttu-id="88615-403">Attribut</span><span class="sxs-lookup"><span data-stu-id="88615-403">Attribute</span></span>|<span data-ttu-id="88615-404">Type</span><span class="sxs-lookup"><span data-stu-id="88615-404">Type</span></span>|<span data-ttu-id="88615-405">Description</span><span class="sxs-lookup"><span data-stu-id="88615-405">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="88615-406">**name**</span><span class="sxs-lookup"><span data-stu-id="88615-406">**name**</span></span>|<span data-ttu-id="88615-407">string</span><span class="sxs-lookup"><span data-stu-id="88615-407">string</span></span>|<span data-ttu-id="88615-408">Un sinkname hello identifiant de chaîne.</span><span class="sxs-lookup"><span data-stu-id="88615-408">A string identifying hello sinkname.</span></span>|  

|<span data-ttu-id="88615-409">Élément</span><span class="sxs-lookup"><span data-stu-id="88615-409">Element</span></span>|<span data-ttu-id="88615-410">Type</span><span class="sxs-lookup"><span data-stu-id="88615-410">Type</span></span>|<span data-ttu-id="88615-411">Description</span><span class="sxs-lookup"><span data-stu-id="88615-411">Description</span></span>|  
|-------------|----------|-----------------|  
|<span data-ttu-id="88615-412">**Application Insights**</span><span class="sxs-lookup"><span data-stu-id="88615-412">**Application Insights**</span></span>|<span data-ttu-id="88615-413">string</span><span class="sxs-lookup"><span data-stu-id="88615-413">string</span></span>|<span data-ttu-id="88615-414">Utilisé uniquement lors de l’envoi des données tooApplication Insights.</span><span class="sxs-lookup"><span data-stu-id="88615-414">Used only when sending data tooApplication Insights.</span></span> <span data-ttu-id="88615-415">Contenir hello clé d’Instrumentation d’un compte d’Application Insights actif que vous avez accès.</span><span class="sxs-lookup"><span data-stu-id="88615-415">Contain hello Instrumentation Key for an active Application Insights account that you have access to.</span></span>|  
|<span data-ttu-id="88615-416">**Canaux**</span><span class="sxs-lookup"><span data-stu-id="88615-416">**Channels**</span></span>|<span data-ttu-id="88615-417">string</span><span class="sxs-lookup"><span data-stu-id="88615-417">string</span></span>|<span data-ttu-id="88615-418">Un pour chaque filtrage supplémentaire qui diffuse cela en continu</span><span class="sxs-lookup"><span data-stu-id="88615-418">One for each additional filtering that stream that you</span></span>|  

## <a name="channels-element"></a><span data-ttu-id="88615-419">Élément Channels</span><span class="sxs-lookup"><span data-stu-id="88615-419">Channels Element</span></span>  
 <span data-ttu-id="88615-420">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - Channels*</span><span class="sxs-lookup"><span data-stu-id="88615-420">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - Channels*</span></span>

 <span data-ttu-id="88615-421">Ajouté à la version 1.5.</span><span class="sxs-lookup"><span data-stu-id="88615-421">Added in version 1.5.</span></span>  

 <span data-ttu-id="88615-422">Définit les filtres pour les flux de données de journaux passant par un récepteur.</span><span class="sxs-lookup"><span data-stu-id="88615-422">Defines filters for streams of log data passing through a sink.</span></span>  

|<span data-ttu-id="88615-423">Élément</span><span class="sxs-lookup"><span data-stu-id="88615-423">Element</span></span>|<span data-ttu-id="88615-424">Type</span><span class="sxs-lookup"><span data-stu-id="88615-424">Type</span></span>|<span data-ttu-id="88615-425">Description</span><span class="sxs-lookup"><span data-stu-id="88615-425">Description</span></span>|  
|-------------|----------|-----------------|  
|<span data-ttu-id="88615-426">**Channel**</span><span class="sxs-lookup"><span data-stu-id="88615-426">**Channel**</span></span>|<span data-ttu-id="88615-427">string</span><span class="sxs-lookup"><span data-stu-id="88615-427">string</span></span>|<span data-ttu-id="88615-428">Consultez la description sur cette page.</span><span class="sxs-lookup"><span data-stu-id="88615-428">See description elsewhere on this page.</span></span>|  

## <a name="channel-element"></a><span data-ttu-id="88615-429">Élément Channel</span><span class="sxs-lookup"><span data-stu-id="88615-429">Channel Element</span></span>
 <span data-ttu-id="88615-430">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - Channels - Channel*</span><span class="sxs-lookup"><span data-stu-id="88615-430">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - Channels - Channel*</span></span>

 <span data-ttu-id="88615-431">Ajouté à la version 1.5.</span><span class="sxs-lookup"><span data-stu-id="88615-431">Added in version 1.5.</span></span>  

 <span data-ttu-id="88615-432">Définit les emplacements toosend données de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="88615-432">Defines locations toosend diagnostic data to.</span></span> <span data-ttu-id="88615-433">Par exemple, hello service Application Insights.</span><span class="sxs-lookup"><span data-stu-id="88615-433">For example, hello Application Insights service.</span></span>  

|<span data-ttu-id="88615-434">Attributs</span><span class="sxs-lookup"><span data-stu-id="88615-434">Attributes</span></span>|<span data-ttu-id="88615-435">Type</span><span class="sxs-lookup"><span data-stu-id="88615-435">Type</span></span>|<span data-ttu-id="88615-436">Description</span><span class="sxs-lookup"><span data-stu-id="88615-436">Description</span></span>|  
|----------------|----------|-----------------|  
|<span data-ttu-id="88615-437">**logLevel**</span><span class="sxs-lookup"><span data-stu-id="88615-437">**logLevel**</span></span>|<span data-ttu-id="88615-438">**string**</span><span class="sxs-lookup"><span data-stu-id="88615-438">**string**</span></span>|<span data-ttu-id="88615-439">Spécifie le niveau de gravité minimal hello pour les entrées de journal sont transférées.</span><span class="sxs-lookup"><span data-stu-id="88615-439">Specifies hello minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="88615-440">la valeur par défaut Hello est **Undefined**, qui transfère tous les journaux.</span><span class="sxs-lookup"><span data-stu-id="88615-440">hello default value is **Undefined**, which transfers all logs.</span></span> <span data-ttu-id="88615-441">Les autres valeurs possibles (dans l’ordre de la plupart des informations tooleast) sont **Verbose**, **informations**, **avertissement**, **erreur**et **Critiques**.</span><span class="sxs-lookup"><span data-stu-id="88615-441">Other possible values (in order of most tooleast information) are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="88615-442">**name**</span><span class="sxs-lookup"><span data-stu-id="88615-442">**name**</span></span>|<span data-ttu-id="88615-443">**string**</span><span class="sxs-lookup"><span data-stu-id="88615-443">**string**</span></span>|<span data-ttu-id="88615-444">Un nom unique de toorefer de canal hello pour</span><span class="sxs-lookup"><span data-stu-id="88615-444">A unique name of hello channel toorefer to</span></span>|  


## <a name="privateconfig-element"></a><span data-ttu-id="88615-445">Élément PrivateConfig</span><span class="sxs-lookup"><span data-stu-id="88615-445">PrivateConfig Element</span></span> 
 <span data-ttu-id="88615-446">*Tree: Root - DiagnosticsConfiguration - PrivateConfig*</span><span class="sxs-lookup"><span data-stu-id="88615-446">*Tree: Root - DiagnosticsConfiguration - PrivateConfig*</span></span>

 <span data-ttu-id="88615-447">Ajouté à la version 1.3.</span><span class="sxs-lookup"><span data-stu-id="88615-447">Added in version 1.3.</span></span>  

 <span data-ttu-id="88615-448">Facultatif</span><span class="sxs-lookup"><span data-stu-id="88615-448">Optional</span></span>  

 <span data-ttu-id="88615-449">Stocke les détails de privé hello hello du compte de stockage (nom, clé et point de terminaison).</span><span class="sxs-lookup"><span data-stu-id="88615-449">Stores hello private details of hello storage account (name, key, and endpoint).</span></span> <span data-ttu-id="88615-450">Ces informations sont envoyées toohello virtual machine, mais ne peuvent pas être récupérées à partir de celui-ci.</span><span class="sxs-lookup"><span data-stu-id="88615-450">This information is sent toohello virtual machine, but cannot be retrieved from it.</span></span>  

|<span data-ttu-id="88615-451">Éléments enfants</span><span class="sxs-lookup"><span data-stu-id="88615-451">Child Elements</span></span>|<span data-ttu-id="88615-452">Description</span><span class="sxs-lookup"><span data-stu-id="88615-452">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="88615-453">**StorageAccount**</span><span class="sxs-lookup"><span data-stu-id="88615-453">**StorageAccount**</span></span>|<span data-ttu-id="88615-454">toouse de compte de stockage Hello.</span><span class="sxs-lookup"><span data-stu-id="88615-454">hello storage account toouse.</span></span> <span data-ttu-id="88615-455">Hello suivant des attributs est requis</span><span class="sxs-lookup"><span data-stu-id="88615-455">hello following attributes are required</span></span><br /><br /> <span data-ttu-id="88615-456">- **nom** hello - nom du compte de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="88615-456">- **name** - hello name of hello storage account.</span></span><br /><br /> <span data-ttu-id="88615-457">- **clé** hello - compte de stockage toohello de clé.</span><span class="sxs-lookup"><span data-stu-id="88615-457">- **key** - hello key toohello storage account.</span></span><br /><br /> <span data-ttu-id="88615-458">- **point de terminaison** -tooaccess de point de terminaison hello hello compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="88615-458">- **endpoint** - hello endpoint tooaccess hello storage account.</span></span> <br /><br /> <span data-ttu-id="88615-459">-**sasToken** (ajouté 1.8.1)-, vous pouvez spécifier un jeton SAS plutôt qu’une clé de compte de stockage dans la configuration privée de hello. Si fourni, la clé de compte de stockage hello est ignorée.</span><span class="sxs-lookup"><span data-stu-id="88615-459">-**sasToken** (added 1.8.1)- You can specify an SAS token instead of a storage account key in hello private config. If provided, hello storage account key is ignored.</span></span> <br /><span data-ttu-id="88615-460">Configuration requise pour hello jeton SAS :</span><span class="sxs-lookup"><span data-stu-id="88615-460">Requirements for hello SAS Token:</span></span> <br /><span data-ttu-id="88615-461">- Prend en charge le jeton SAP de compte uniquement.</span><span class="sxs-lookup"><span data-stu-id="88615-461">- Supports account SAS token only</span></span> <br /><span data-ttu-id="88615-462">Les types de services - *b*, *t* sont requis.</span><span class="sxs-lookup"><span data-stu-id="88615-462">- *b*, *t* service types are required.</span></span> <br /> <span data-ttu-id="88615-463">Les autorisations - *a*, *c*, *u*, *w* sont requises.</span><span class="sxs-lookup"><span data-stu-id="88615-463">- *a*, *c*, *u*, *w* permissions are required.</span></span> <br /> <span data-ttu-id="88615-464">Les types de ressources - *c*, *o* sont requis.</span><span class="sxs-lookup"><span data-stu-id="88615-464">- *c*, *o* resource types are required.</span></span> <br /> <span data-ttu-id="88615-465">-Prend en charge uniquement le protocole HTTPS hello</span><span class="sxs-lookup"><span data-stu-id="88615-465">- Supports hello HTTPS protocol only</span></span> <br /> <span data-ttu-id="88615-466">- Les heures de début et d’expiration doivent être valides.</span><span class="sxs-lookup"><span data-stu-id="88615-466">- Start and expiry time must be valid.</span></span>|  


## <a name="isenabled-element"></a><span data-ttu-id="88615-467">Élément IsEnabled</span><span class="sxs-lookup"><span data-stu-id="88615-467">IsEnabled Element</span></span>  
 <span data-ttu-id="88615-468">*Tree: Root - DiagnosticsConfiguration - IsEnabled*</span><span class="sxs-lookup"><span data-stu-id="88615-468">*Tree: Root - DiagnosticsConfiguration - IsEnabled*</span></span>

 <span data-ttu-id="88615-469">Booléen.</span><span class="sxs-lookup"><span data-stu-id="88615-469">Boolean.</span></span> <span data-ttu-id="88615-470">Utilisez `true` diagnostics de hello tooenable ou `false` diagnostics de hello toodisable.</span><span class="sxs-lookup"><span data-stu-id="88615-470">Use `true` tooenable hello diagnostics or `false` toodisable hello diagnostics.</span></span>
