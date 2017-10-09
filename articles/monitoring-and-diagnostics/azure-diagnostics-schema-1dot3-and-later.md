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
# <a name="azure-diagnostics-13-and-later-configuration-schema"></a>Schéma de configuration de Microsoft Azure Diagnostics 1.3 et versions ultérieures
> [!NOTE]
> Hello extension Azure Diagnostics est composant de hello utilisé toocollect les compteurs de performance et d’autres statistiques à partir de :
> - Machines virtuelles Azure 
> - Jeux de mise à l’échelle de machine virtuelle
> - Service Fabric 
> - Services cloud 
> - Groupes de sécurité réseau
> 
> Cette page vous concerne uniquement si vous utilisez l’un de ces services.

Cette page a trait aux versions 1.3 et ultérieures (Azure SDK 2.4 et ultérieur). Les sections de configuration plus récentes sont tooshow commentée dans version ils ont été ajoutés.  

fichier de configuration de Hello décrite ici est tooset utilisé les paramètres de configuration de diagnostic lorsque hello diagnostics surveiller démarre.  

extension de Hello est utilisée conjointement avec d’autres produits de diagnostics de Microsoft, analyse d’Azure, Application Insights et Analytique de journal.



Télécharger la définition de schéma de fichier de configuration publique hello en exécutant hello suivant de commande PowerShell :  

```powershell  
(Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File –Encoding utf8 -FilePath 'C:\temp\WadConfig.xsd'  
```  

Pour plus d’informations sur l’utilisation d’Azure Diagnostics, voir [Extension Microsoft Azure Diagnostics](azure-diagnostics.md).  

## <a name="example-of-hello-diagnostics-configuration-file"></a>Exemple de fichier de configuration de diagnostics hello  
 Bonjour à l’exemple suivant montre un fichier de configuration de diagnostics standard :  

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

Équivalent JSON hello précédente XML du fichier de configuration. 

Hello PublicConfig et PrivateConfig sont séparés, car dans la plupart des cas d’utilisation de json, ils sont passés en tant que variables différentes. Ces cas incluent les modèles Resource Manager, le groupe de machines virtuelles identiques PowerShell et Visual Studio. 

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

## <a name="reading-this-page"></a>Lecture de cette page  
 Hello balises suivant sont à peu près dans l’ordre indiqué dans le précédent exemple de hello.  Si vous ne voyez pas une description complète à l’emplacement prévu, rechercher hello des page hello élément ou attribut.  

## <a name="common-attribute-types"></a>Types d’attributs courants  
 L’attribut **scheduledTransferPeriod** apparaît dans plusieurs éléments. Il s’agit d’intervalle de salutation entre toostorage les transferts planifiés arrondi toohello minute la plus proche. la valeur Hello est un [XML « Type de données de durée ».](http://www.w3schools.com/schema/schema_dtypes_date.asp)


## <a name="diagnosticsconfiguration-element"></a>Élément DiagnosticsConfiguration  
 *Tree: Root - DiagnosticsConfiguration*

Ajouté à la version 1.3.  

élément de niveau supérieur Hello hello diagnostics du fichier de configuration.  

**Attribut** xmlns - hello espace de noms XML pour le fichier de configuration de diagnostics hello est :  
http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration  


|Éléments enfants|Description|  
|--------------------|-----------------|  
|**PublicConfig**|Obligatoire. Consultez la description sur cette page.|  
|**PrivateConfig**|facultatif. Consultez la description sur cette page.|  
|**IsEnabled**|Booléen. Consultez la description sur cette page.|  

## <a name="publicconfig-element"></a>Élément PublicConfig  
 *Tree: Root - DiagnosticsConfiguration - PublicConfig*

 Décrit la configuration des diagnostics publique hello.  

|Éléments enfants|Description|  
|--------------------|-----------------|  
|**WadCfg**|Obligatoire. Consultez la description sur cette page.|  
|**StorageAccount**|nom de Hello de compte de stockage Azure hello toostore hello données dans. Peut également être spécifié en tant que paramètre lorsque vous exécutez l’applet de commande hello AzureServiceDiagnosticsExtension de jeu.|  
|**StorageType**|Peut être *Table*, *Blob* ou *TableAndBlob*. Table est la valeur par défaut. Lorsque TableAndBlob est choisie, données de diagnostic sont enregistrées à deux reprises : une fois tooeach type.|  
|**LocalResourceDirectory**|répertoire Hello sur l’ordinateur virtuel de hello où hello Monitoring Agent stocke les données d’événement. Dans le cas contraire, valeur, le répertoire par défaut de hello est utilisé :<br /><br /> Pour un rôle Worker/web : `C:\Resources\<guid>\directory\<guid>.<RoleName.DiagnosticStore\`<br /><br /> Pour une machine virtuelle : `C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<WADVersion>\WAD<WADVersion>`<br /><br /> Les attributs requis sont :<br /><br /> - **chemin d’accès** - hello répertoire hello système toobe est utilisé par les Diagnostics Windows Azure.<br /><br /> - **expandEnvironment** -contrôle si les variables d’environnement sont développées dans le nom de chemin d’accès hello.|  

## <a name="wadcfg-element"></a>WadCFG Element  
 *Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG*
 
 Identifie et configure toobe de données de télémétrie hello collectée.  


## <a name="diagnosticmonitorconfiguration-element"></a>Élément DiagnosticMonitorConfiguration 
 *Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration*

 Requis 

|Attributs|Description|  
|----------------|-----------------|  
| **overallQuotaInMB** | quantité maximale de Hello d’espace disque local qui peut être consommée par hello différents types de données de diagnostic collectées par Diagnostics Windows Azure. Hello par défaut est 5 120 Mo.<br />
|**useProxyServer** | Configurer les paramètres du serveur proxy Azure Diagnostics toouse hello comme dans les paramètres d’Internet Explorer.|  

<br /> <br />

|Éléments enfants|Description|  
|--------------------|-----------------|  
|**CrashDumps**|Consultez la description sur cette page.|  
|**DiagnosticInfrastructureLogs**|Permet la collecte des journaux générés par Azure Diagnostics. journaux d’infrastructure de diagnostics Hello sont utiles pour la résolution des problèmes de système de diagnostic hello lui-même. Les attributs facultatifs sont les suivants :<br /><br /> - **scheduledTransferLogLevelFilter** -configure le niveau de gravité minimal hello de journaux hello collecté.<br /><br /> - **scheduledTransferPeriod** -intervalle hello entre les transferts planifiés toostorage arrondi toohello minute la plus proche. la valeur Hello est un [XML « Type de données de durée ».](http://www.w3schools.com/schema/schema_dtypes_date.asp) |  
|**Directories**|Consultez la description sur cette page.|  
|**EtwProviders**|Consultez la description sur cette page.|  
|**Métriques**|Consultez la description sur cette page.|  
|**PerformanceCounters**|Consultez la description sur cette page.|  
|**WindowsEventLog**|Consultez la description sur cette page.| 
|**DockerSources**|Consultez la description sur cette page. | 



## <a name="crashdumps-element"></a>Élément CrashDumps  
 *Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - CrashDumps*
 
 Activer la collecte de hello des vidages sur incident.  

|Attributs|Description|  
|----------------|-----------------|  
|**containerName**|facultatif. nom de Hello du conteneur d’objets blob hello dans votre toobe de compte de stockage Azure utilisé des vidages sur incident de toostore.|  
|**crashDumpType**|facultatif.  Configure les vidages sur incident de mini ou complète de toocollect de Diagnostics Windows Azure.|  
|**directoryQuotaPercentage**|facultatif.  Configure le pourcentage de hello de **overallQuotaInMB** toobe réservé pour les vidages sur incident sur hello machine virtuelle.|  

|Éléments enfants|Description|  
|--------------------|-----------------|  
|**CrashDumpConfiguration**|Obligatoire. Définit les valeurs de configuration pour chaque processus.<br /><br /> Hello suivant l’attribut est également requis :<br /><br /> **processName** hello - nom de hello processus Azure Diagnostics toocollect un vidage sur incident pour.|  

## <a name="directories-element"></a>Élément Directories 
 *Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration -  Directories*

 Active hello collection de contenu hello d’un répertoire, IIS ayant échoué, journaux de demandes d’accès et/ou les journaux IIS.  

 Attribut **scheduledTransferPeriod** facultatif. Voir l’explication précédente.  

|Éléments enfants|Description|  
|--------------------|-----------------|  
|**IISLogs**|Y compris de cet élément dans la configuration de hello permet la collection hello de journaux IIS :<br /><br /> **containerName** -nom hello du conteneur d’objets blob hello dans votre toobe de compte de stockage Azure utilisé les journaux IIS toostore hello.|   
|**FailedRequestLogs**|Y compris de cet élément dans la configuration de hello permet de collection de journaux sur des demandes ayant échoué tooan IIS site ou application. Vous devez également activer les options de suivi sous **system.WebServer** dans **Web.config**.|  
|**DataSources**|Une liste de répertoires toomonitor.| 




## <a name="datasources-element"></a>Élément DataSources  
 *Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories - DataSources*

 Une liste de répertoires toomonitor.  

|Éléments enfants|Description|  
|--------------------|-----------------|  
|**DirectoryConfiguration**|Obligatoire. Attribut requis :<br /><br /> **containerName** hello - nom du conteneur d’objets blob hello dans votre compte de stockage Azure qui toobe utilisé des fichiers journaux toostore hello.|  





## <a name="directoryconfiguration-element"></a>Élément DirectoryConfiguration  
 *Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories - DataSources - DirectoryConfiguration*

 Peuvent inclure deux hello **absolu** ou **LocalResource** élément mais pas les deux.  

|Éléments enfants|Description|  
|--------------------|-----------------|  
|**Absolute**|Bonjour toomonitor de répertoire toohello de chemin d’accès absolu. Hello suivant des attributs est requis :<br /><br /> - **Chemin d’accès** -hello toomonitor de répertoire toohello de chemin d’accès absolu.<br /><br /> - **expandEnvironment** - Détermine si les variables d’environnement de Path sont développées.|  
|**LocalResource**|Bonjour toomonitor de chemin d’accès relatif tooa ressource locale. Les attributs requis sont :<br /><br /> - **Nom** -hello ressource locale contenant hello Active toomonitor<br /><br /> - **relativePath** -hello du chemin d’accès relatif tooName contenant hello Active toomonitor|  



## <a name="etwproviders-element"></a>Élément EtwProviders  
 *Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders*

 Configure la collecte d’événements ETW issus des fournisseurs de manifeste EventSource et/ou ETW.  

|Éléments enfants|Description|  
|--------------------|-----------------|  
|**EtwEventSourceProviderConfiguration**|Configure la collection d’événements générés à partir de la [classe EventSource](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx). Attribut requis :<br /><br /> **fournisseur** -nom de la classe d’événement de EventSource hello hello.<br /><br /> Les attributs facultatifs sont les suivants :<br /><br /> - **scheduledTransferLogLevelFilter** -hello compte de stockage de gravité minimal niveau tootransfer tooyour.<br /><br /> - **scheduledTransferPeriod** -intervalle hello entre les transferts planifiés toostorage arrondi toohello minute la plus proche. la valeur Hello est un [XML « Type de données de durée ».](http://www.w3schools.com/schema/schema_dtypes_date.asp) |  
|**EtwManifestProviderConfiguration**|Attribut requis :<br /><br /> **fournisseur** -hello GUID du fournisseur d’événements hello<br /><br /> Les attributs facultatifs sont les suivants :<br /><br /> - **scheduledTransferLogLevelFilter** -hello compte de stockage de gravité minimal niveau tootransfer tooyour.<br /><br /> - **scheduledTransferPeriod** -intervalle hello entre les transferts planifiés toostorage arrondi toohello minute la plus proche. la valeur Hello est un [XML « Type de données de durée ».](http://www.w3schools.com/schema/schema_dtypes_date.asp) |  



## <a name="etweventsourceproviderconfiguration-element"></a>EtwEventSourceProviderConfiguration Element  
 *Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders- EtwEventSourceProviderConfiguration*

 Configure la collection d’événements générés à partir de la [classe EventSource](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).  

|Éléments enfants|Description|  
|--------------------|-----------------|  
|**DefaultEvents**|Attribut facultatif :<br/><br/> **eventDestination** - hello nom hello toostore hello d’événements de table dans|  
|**Event**|Attribut requis :<br /><br /> **ID** -id hello d’événement de hello.<br /><br /> Attribut facultatif :<br /><br /> **eventDestination** - hello nom hello toostore hello d’événements de table dans|  



## <a name="etwmanifestproviderconfiguration-element"></a>EtwManifestProviderConfiguration Element  
 *Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders - EtwManifestProviderConfiguration*

|Éléments enfants|Description|  
|--------------------|-----------------|  
|**DefaultEvents**|Attribut facultatif :<br /><br /> **eventDestination** - hello nom hello toostore hello d’événements de table dans|  
|**Event**|Attribut requis :<br /><br /> **ID** -id hello d’événement de hello.<br /><br /> Attribut facultatif :<br /><br /> **eventDestination** - hello nom hello toostore hello d’événements de table dans|  



## <a name="metrics-element"></a>Élément Metrics  
 *Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Metrics*

 Vous permet de toogenerate une table de compteur de performances est optimisée pour les requêtes rapides. Chaque compteur de performance qui est défini dans hello **PerformanceCounters** élément est stocké dans la table des métriques hello dans la table de compteur de Performance toohello Ajout.  

 Hello **resourceId** attribut est requis.  ID de ressource Hello Hello Machine virtuelle que vous déployez des Diagnostics Windows Azure à. Obtenir hello **resourceID** de hello [portail Azure](https://portal.azure.com). Sélectionnez **Parcourir** -> **Groupe de ressources** -> **<>\>**. Cliquez sur hello **propriétés** vignette et copiez la valeur de hello hello **ID** champ.  

|Éléments enfants|Description|  
|--------------------|-----------------|  
|**MetricAggregation**|Attribut requis :<br /><br /> **scheduledTransferPeriod** -intervalle hello entre les transferts planifiés toostorage arrondi toohello minute la plus proche. la valeur Hello est un [XML « Type de données de durée ».](http://www.w3schools.com/schema/schema_dtypes_date.asp) |  



## <a name="performancecounters-element"></a>Élément PerformanceCounters  
 *Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - PerformanceCounters*

 Active la collecte de hello des compteurs de performance.  

 Attribut facultatif :  

 Attribut **scheduledTransferPeriod** facultatif. Voir l’explication précédente.

|Élément enfant|Description|  
|-------------------|-----------------|  
|**PerformanceCounterConfiguration**|Hello suivant des attributs est requis :<br /><br /> - **counterSpecifier** - hello nom hello compteur de performance. Par exemple, `\Processor(_Total)\% Processor Time`. tooget une liste des performances des compteurs sur votre ordinateur hôte, exécutez la commande hello `typeperf`.<br /><br /> - **sampleRate** -fréquence hello compteur doit être échantillonné.<br /><br /> Attribut facultatif :<br /><br /> **unité** -unité de mesure du compteur de hello de hello.|  




## <a name="windowseventlog-element"></a>Élément WindowsEventLog
 *Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - WindowsEventLog*
 
 Active la collecte de hello des journaux des événements Windows.  

 Attribut **scheduledTransferPeriod** facultatif. Voir l’explication précédente.  

|Élément enfant|Description|  
|-------------------|-----------------|  
|**DataSource**|Hello toocollect de journaux des événements Windows. Attribut requis :<br /><br /> **nom** -requête XPath de hello décrivant hello windows événements toobe collectées. Par exemple :<br /><br /> `Application!*[System[(Level <=3)]], System!*[System[(Level <=3)]], System!*[System[Provider[@Name='Microsoft Antimalware']]], Security!*[System[(Level <= 3)]`<br /><br /> tous les événements, de toocollect spécifier « * »|  




## <a name="logs-element"></a>Élément Logs  
 *Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Logs*

 Présent dans la version 1.0 et 1.1. Absent dans la version 1.2. Rajouté dans la version 1.3.  

 Définit la configuration du tampon hello pour les journaux Azure de base.  

|Attribut|Type|Description|  
|---------------|----------|-----------------|  
|**bufferQuotaInMB**|**unsignedInt**|facultatif. Spécifie la quantité maximale de hello du stockage de système de fichiers est disponible pour hello spécifié données.<br /><br /> valeur par défaut Hello est 0.|  
|**scheduledTransferLogLevelFilterr**|**string**|facultatif. Spécifie le niveau de gravité minimal hello pour les entrées de journal sont transférées. la valeur par défaut Hello est **Undefined**, qui transfère tous les journaux. Les autres valeurs possibles (dans l’ordre de la plupart des informations tooleast) sont **Verbose**, **informations**, **avertissement**, **erreur**et **Critiques**.|  
|**scheduledTransferPeriod**|**duration**|facultatif. Spécifie l’intervalle de salutation entre les transferts planifiés de données, arrondies à toohello minute la plus proche.<br /><br /> valeur par défaut Hello est PT0S.|  
|**sinks** - Ajouté à la version 1.5|**string**|facultatif. Points tooa récepteur emplacement tooalso envoyer des données de diagnostic. Par exemple, Application Insights.|  

## <a name="dockersources"></a>DockerSources
 *Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - DockerSources*

 Ajouté dans 1.9.

|Nom de l’élément|Description|  
|------------------|-----------------|  
|**Stats**|Indique au système de hello toocollect des statistiques pour les conteneurs Docker|  

## <a name="sinksconfig-element"></a>Élément SinksConfig  
 *Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig*

 Liste des emplacements toosend diagnostics données tooand hello configuration associée à ces emplacements.  

|Nom de l’élément|Description|  
|------------------|-----------------|  
|**Section sink**|Consultez la description sur cette page.|  

## <a name="sink-element"></a>Élément Sink
 *Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink*

 Ajouté à la version 1.5.  

 Définit les emplacements toosend données de diagnostic. Par exemple, hello service Application Insights.  

|Attribut|Type|Description|  
|---------------|----------|-----------------|  
|**name**|string|Un sinkname hello identifiant de chaîne.|  

|Élément|Type|Description|  
|-------------|----------|-----------------|  
|**Application Insights**|string|Utilisé uniquement lors de l’envoi des données tooApplication Insights. Contenir hello clé d’Instrumentation d’un compte d’Application Insights actif que vous avez accès.|  
|**Canaux**|string|Un pour chaque filtrage supplémentaire qui diffuse cela en continu|  

## <a name="channels-element"></a>Élément Channels  
 *Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - Channels*

 Ajouté à la version 1.5.  

 Définit les filtres pour les flux de données de journaux passant par un récepteur.  

|Élément|Type|Description|  
|-------------|----------|-----------------|  
|**Channel**|string|Consultez la description sur cette page.|  

## <a name="channel-element"></a>Élément Channel
 *Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - Channels - Channel*

 Ajouté à la version 1.5.  

 Définit les emplacements toosend données de diagnostic. Par exemple, hello service Application Insights.  

|Attributs|Type|Description|  
|----------------|----------|-----------------|  
|**logLevel**|**string**|Spécifie le niveau de gravité minimal hello pour les entrées de journal sont transférées. la valeur par défaut Hello est **Undefined**, qui transfère tous les journaux. Les autres valeurs possibles (dans l’ordre de la plupart des informations tooleast) sont **Verbose**, **informations**, **avertissement**, **erreur**et **Critiques**.|  
|**name**|**string**|Un nom unique de toorefer de canal hello pour|  


## <a name="privateconfig-element"></a>Élément PrivateConfig 
 *Tree: Root - DiagnosticsConfiguration - PrivateConfig*

 Ajouté à la version 1.3.  

 Facultatif  

 Stocke les détails de privé hello hello du compte de stockage (nom, clé et point de terminaison). Ces informations sont envoyées toohello virtual machine, mais ne peuvent pas être récupérées à partir de celui-ci.  

|Éléments enfants|Description|  
|--------------------|-----------------|  
|**StorageAccount**|toouse de compte de stockage Hello. Hello suivant des attributs est requis<br /><br /> - **nom** hello - nom du compte de stockage hello.<br /><br /> - **clé** hello - compte de stockage toohello de clé.<br /><br /> - **point de terminaison** -tooaccess de point de terminaison hello hello compte de stockage. <br /><br /> -**sasToken** (ajouté 1.8.1)-, vous pouvez spécifier un jeton SAS plutôt qu’une clé de compte de stockage dans la configuration privée de hello. Si fourni, la clé de compte de stockage hello est ignorée. <br />Configuration requise pour hello jeton SAS : <br />- Prend en charge le jeton SAP de compte uniquement. <br />Les types de services - *b*, *t* sont requis. <br /> Les autorisations - *a*, *c*, *u*, *w* sont requises. <br /> Les types de ressources - *c*, *o* sont requis. <br /> -Prend en charge uniquement le protocole HTTPS hello <br /> - Les heures de début et d’expiration doivent être valides.|  


## <a name="isenabled-element"></a>Élément IsEnabled  
 *Tree: Root - DiagnosticsConfiguration - IsEnabled*

 Booléen. Utilisez `true` diagnostics de hello tooenable ou `false` diagnostics de hello toodisable.
