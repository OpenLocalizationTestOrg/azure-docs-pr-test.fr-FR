---
title: "aaaAzure schéma de Configuration de Diagnostics 1.2 | Documents Microsoft"
description: "Applicable UNIQUEMENT si vous utilisez le Kit de développement logiciel (SDK) Azure 2.5 avec Azure Virtual Machines, Virtual Machine Scale Sets, Service Fabric ou Cloud Services."
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
ms.openlocfilehash: 31559317b696556a64b51b58800b176ade9a4679
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-diagnostics-12-configuration-schema"></a>Schéma de configuration Azure Diagnostics 1.2
> [!NOTE]
> Diagnostics Azure sont des compteurs de performance toocollect hello composant utilisé et d’autres statistiques à partir de Machines virtuelles Azure, machines virtuelles identiques, l’infrastructure de Service et les Services de Cloud.  Cette page vous concerne uniquement si vous utilisez l’un de ces services.
>

Azure Diagnostics est utilisé avec d’autres produits de diagnostic Microsoft tels que Azure Monitor, Application Insights et Log Analytics.

Ce schéma définit les valeurs possibles de hello vous pouvez utiliser les paramètres de configuration de diagnostic tooinitialize au démarrage du moniteur de diagnostic hello.  


 Télécharger la définition de schéma de fichier de configuration publique hello en exécutant hello suivant de commande PowerShell :  

```PowerShell  
(Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File –Encoding utf8 -FilePath 'C:\temp\WadConfig.xsd'  
```  

 Pour plus d’informations sur les diagnostics Azure, consultez la page [Activation de Diagnostics dans Azure Cloud Service](http://azure.microsoft.com/documentation/articles/cloud-services-dotnet-diagnostics/).  

## <a name="example-of-hello-diagnostics-configuration-file"></a>Exemple de fichier de configuration de diagnostics hello  
 Bonjour à l’exemple suivant montre un fichier de configuration de diagnostics standard :  

```xml
<?xml version="1.0" encoding="utf-8"?>  
<PublicConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">  
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
        <EtwEventSourceProviderConfiguration provider="MyProviderClass" scheduledTransferPeriod="PT5M">  
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
      <CrashDumps containerName="wad-crashdumps" directoryQuotaPercentage="30" dumpType="Mini">  
        <CrashDumpConfiguration processName="mynewprocess.exe" />  
        <CrashDumpConfiguration processName="badapp.exe"/>  
      </CrashDumps>  
    </DiagnosticMonitorConfiguration>  
  </WadCfg>  
</PublicConfig>  

```  

## <a name="diagnostics-configuration-namespace"></a>Espace de noms de configuration de diagnostic  
 espace de noms XML Hello pour le fichier de configuration de diagnostics hello est la suivante :  

```  
http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration  
```  

## <a name="publicconfig-element"></a>Élément PublicConfig  
 Élément de niveau supérieur du fichier de configuration de diagnostics hello. Hello tableau suivant décrit les éléments hello hello du fichier de configuration.  

|Nom de l’élément|Description|  
|------------------|-----------------|  
|**WadCfg**|Obligatoire. Paramètres de configuration pour toobe de données de télémétrie hello collectées.|  
|**StorageAccount**|nom de Hello de compte de stockage Azure hello toostore hello données dans. Cela peut également être spécifié en tant que paramètre lorsque vous exécutez l’applet de commande hello AzureServiceDiagnosticsExtension de jeu.|  
|**LocalResourceDirectory**|répertoire de Hello sur hello toobe de machine virtuelle utilisée par hello données d’événement de l’Agent d’analyse toostore. Si ce n’est pas le cas, ensemble, le répertoire par défaut de hello est utilisé :<br /><br /> Pour un rôle Worker/web : `C:\Resources\<guid>\directory\<guid>.<RoleName.DiagnosticStore\`<br /><br /> Pour une machine virtuelle : `C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<WADVersion>\WAD<WADVersion>`<br /><br /> Les attributs requis sont :<br /><br /> -                      **chemin d’accès** - hello répertoire hello système toobe est utilisé par les Diagnostics Windows Azure.<br /><br /> -                      **expandEnvironment** -contrôle si les variables d’environnement sont développées dans le nom de chemin d’accès hello.|  

## <a name="wadcfg-element"></a>WadCFG Element  
Définit les paramètres de configuration pour toobe de données de télémétrie hello collectées. Hello tableau suivant décrit les éléments enfants :  

|Nom de l'élément|Description|  
|------------------|-----------------|  
|**DiagnosticMonitorConfiguration**|Obligatoire. Les attributs facultatifs sont les suivants :<br /><br /> -                     **overallQuotaInMB** -quantité maximale de hello d’espace disque local qui peut être consommée par hello différents types de données de diagnostic collectées par Diagnostics Windows Azure. Hello par défaut est 5 120 Mo.<br /><br /> -                     **useProxyServer** -paramètres du serveur proxy configurer les Diagnostics Azure toouse hello défini dans les paramètres d’Internet Explorer.|  
|**CrashDumps**|Permet la collecte des vidages sur incident. Les attributs facultatifs sont les suivants :<br /><br /> -                     **containerName** -nom de hello du conteneur d’objets blob hello dans votre toobe de compte de stockage Azure utilisé des vidages sur incident de toostore.<br /><br /> -                     **crashDumpType** -configure Azure Diagnostics toocollect incident Mini ou intégral vide.<br /><br /> -                     **directoryQuotaPercentage**-configure le pourcentage de hello de **overallQuotaInMB** toobe réservé pour les vidages sur incident sur hello machine virtuelle.|  
|**DiagnosticInfrastructureLogs**|Permet la collecte des journaux générés par Azure Diagnostics. journaux d’infrastructure de diagnostics Hello sont utiles pour la résolution des problèmes de système de diagnostic hello lui-même. Les attributs facultatifs sont les suivants :<br /><br /> -                     **scheduledTransferLogLevelFilter** -configure le niveau de gravité minimal hello de journaux hello collecté.<br /><br /> -                     **scheduledTransferPeriod** -intervalle hello entre les transferts planifiés toostorage arrondi toohello minute la plus proche. la valeur Hello est un [XML « Type de données de durée ».](http://www.w3schools.com/schema/schema_dtypes_date.asp)|  
|**Directories**|Active hello collection de contenu hello d’un répertoire, IIS ayant échoué, journaux de demandes d’accès et/ou les journaux IIS. Attribut facultatif :<br /><br /> **scheduledTransferPeriod** -intervalle hello entre les transferts planifiés toostorage arrondi toohello minute la plus proche. la valeur Hello est un [XML « Type de données de durée ».](http://www.w3schools.com/schema/schema_dtypes_date.asp)|  
|**EtwProviders**|Configure la collecte d’événements ETW issus des fournisseurs de manifeste EventSource et/ou ETW.|  
|**Métriques**|Cet élément vous permet de toogenerate une table de compteur de performances est optimisée pour les requêtes rapides. Chaque compteur de performance qui est défini dans hello **PerformanceCounters** élément est stocké dans la table des métriques hello dans la table de compteur de Performance toohello Ajout. Attribut requis :<br /><br /> **ID de ressource** -ID de ressource hello Hello Machine virtuelle que vous déployez des Diagnostics Windows Azure à. Obtenir hello **resourceID** de hello [portail Azure](https://portal.azure.com). Sélectionnez **Parcourir** -> **Groupe de ressources** -> **<>\>**. Cliquez sur hello **propriétés** vignette et copiez la valeur de hello hello **ID** champ.|  
|**PerformanceCounters**|Active la collecte de hello des compteurs de performance. Attribut facultatif :<br /><br /> **scheduledTransferPeriod** -intervalle hello entre les transferts planifiés toostorage arrondi toohello minute la plus proche. La valeur est un [« Type de données de durée » XML.](http://www.w3schools.com/schema/schema_dtypes_date.asp)|  
|**WindowsEventLog**|Active la collecte de hello des journaux des événements Windows. Attribut facultatif :<br /><br /> **scheduledTransferPeriod** -intervalle hello entre les transferts planifiés toostorage arrondi toohello minute la plus proche. La valeur est un [« Type de données de durée » XML.](http://www.w3schools.com/schema/schema_dtypes_date.asp)|  

## <a name="crashdumps-element"></a>Élément CrashDumps  
 Permet la collecte des vidages sur incident. Hello tableau suivant décrit les éléments enfants :  

|Nom de l’élément|Description|  
|------------------|-----------------|  
|**CrashDumpConfiguration**|Obligatoire. Attribut requis :<br /><br /> **processName** hello - nom de hello processus Azure Diagnostics toocollect un vidage sur incident pour.|  
|**crashDumpType**|Configure les vidages sur incident de mini ou complète de toocollect de Diagnostics Windows Azure.|  
|**directoryQuotaPercentage**|Configure le pourcentage de hello de **overallQuotaInMB** toobe réservé pour les vidages sur incident sur hello machine virtuelle.|  

## <a name="directories-element"></a>Élément Directories  
 Active hello collection de contenu hello d’un répertoire, IIS ayant échoué, journaux de demandes d’accès et/ou les journaux IIS. Hello tableau suivant décrit les éléments enfants :  

|Nom de l’élément|Description|  
|------------------|-----------------|  
|**DataSources**|Une liste de répertoires toomonitor.|  
|**FailedRequestLogs**|Y compris de cet élément dans la configuration de hello permet de collection de journaux sur des demandes ayant échoué tooan IIS site ou application. Vous devez également activer les options de suivi sous **system.WebServer** dans **Web.config**.|  
|**IISLogs**|Y compris de cet élément dans la configuration de hello permet la collection hello de journaux IIS :<br /><br /> **containerName** -nom hello du conteneur d’objets blob hello dans votre toobe de compte de stockage Azure utilisé les journaux IIS toostore hello.|  

## <a name="datasources-element"></a>Élément DataSources  
 Une liste de répertoires toomonitor. Hello tableau suivant décrit les éléments enfants :  

|Nom de l’élément|Description|  
|------------------|-----------------|  
|**DirectoryConfiguration**|Obligatoire. Attribut requis :<br /><br /> **containerName** -hello le nom de conteneur d’objets blob hello dans votre stockage Azure compte toobe utilisé toostore des fichiers journaux hello.|  

## <a name="directoryconfiguration-element"></a>Élément DirectoryConfiguration  
 **DirectoryConfiguration** peuvent inclure deux hello **absolu** ou **LocalResource** élément mais pas les deux. Hello tableau suivant décrit les éléments enfants :  

|Nom de l’élément|Description|  
|------------------|-----------------|  
|**Absolute**|Bonjour toomonitor de répertoire toohello de chemin d’accès absolu. Hello suivant des attributs est requis :<br /><br /> -                     **Chemin d’accès** -hello toomonitor de répertoire toohello de chemin d’accès absolu.<br /><br /> -                      **expandEnvironment** - Détermine si les variables d’environnement de Path sont développées.|  
|**LocalResource**|Bonjour toomonitor de chemin d’accès relatif tooa ressource locale. Les attributs requis sont :<br /><br /> -                     **Nom** -hello ressource locale contenant hello Active toomonitor<br /><br /> -                     **relativePath** -hello du chemin d’accès relatif tooName contenant hello Active toomonitor|  

## <a name="etwproviders-element"></a>Élément EtwProviders  
 Configure la collecte d’événements ETW issus des fournisseurs de manifeste EventSource et/ou ETW. Hello tableau suivant décrit les éléments enfants :  

|Nom de l’élément|Description|  
|------------------|-----------------|  
|**EtwEventSourceProviderConfiguration**|Configure la collection d’événements générés à partir de la [classe EventSource](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx). Attribut requis :<br /><br /> **fournisseur** -nom de la classe d’événement de EventSource hello hello.<br /><br /> Les attributs facultatifs sont les suivants :<br /><br /> -                     **scheduledTransferLogLevelFilter** -hello compte de stockage de gravité minimal niveau tootransfer tooyour.<br /><br /> -                     **scheduledTransferPeriod** -intervalle hello entre les transferts planifiés toostorage arrondi toohello minute la plus proche. La valeur est un [Type de données de durée XML](http://www.w3schools.com/schema/schema_dtypes_date.asp).|  
|**EtwManifestProviderConfiguration**|Attribut requis :<br /><br /> **fournisseur** -hello GUID du fournisseur d’événements hello<br /><br /> Les attributs facultatifs sont les suivants :<br /><br /> - **scheduledTransferLogLevelFilter** -hello compte de stockage de gravité minimal niveau tootransfer tooyour.<br /><br /> -                     **scheduledTransferPeriod** -intervalle hello entre les transferts planifiés toostorage arrondi toohello minute la plus proche. La valeur est un [Type de données de durée XML](http://www.w3schools.com/schema/schema_dtypes_date.asp).|  

## <a name="etweventsourceproviderconfiguration-element"></a>EtwEventSourceProviderConfiguration Element  
 Configure la collection d’événements générés à partir de la [classe EventSource](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx). Hello tableau suivant décrit les éléments enfants :  

|Nom de l’élément|Description|  
|------------------|-----------------|  
|**DefaultEvents**|Attribut facultatif :<br /><br /> **eventDestination** - hello nom hello toostore hello d’événements de table dans|  
|**Event**|Attribut requis :<br /><br /> **ID** -id hello d’événement de hello.<br /><br /> Attribut facultatif :<br /><br /> **eventDestination** - hello nom hello toostore hello d’événements de table dans|  

## <a name="etwmanifestproviderconfiguration-element"></a>EtwManifestProviderConfiguration Element  
 Hello tableau suivant décrit les éléments enfants :  

|Nom de l’élément|Description|  
|------------------|-----------------|  
|**DefaultEvents**|Attribut facultatif :<br /><br /> **eventDestination** - hello nom hello toostore hello d’événements de table dans|  
|**Event**|Attribut requis :<br /><br /> **ID** -id hello d’événement de hello.<br /><br /> Attribut facultatif :<br /><br /> **eventDestination** - hello nom hello toostore hello d’événements de table dans|  

## <a name="metrics-element"></a>Élément Metrics  
 Vous permet de toogenerate une table de compteur de performances est optimisée pour les requêtes rapides. Hello tableau suivant décrit les éléments enfants :  

|Nom de l’élément|Description|  
|------------------|-----------------|  
|**MetricAggregation**|Attribut requis :<br /><br /> **scheduledTransferPeriod** -intervalle hello entre les transferts planifiés toostorage arrondi toohello minute la plus proche. La valeur est un [Type de données de durée XML](http://www.w3schools.com/schema/schema_dtypes_date.asp).|  

## <a name="performancecounters-element"></a>Élément PerformanceCounters  
 Active la collecte de hello des compteurs de performance. Hello tableau suivant décrit les éléments enfants :  

|Nom de l’élément|Description|  
|------------------|-----------------|  
|**PerformanceCounterConfiguration**|Hello suivant des attributs est requis :<br /><br /> -                     **counterSpecifier** - hello nom hello compteur de performance. Par exemple, `\Processor(_Total)\% Processor Time`. tooget une liste des compteurs de performances sur votre hôte, exécutez la commande hello `typeperf`.<br /><br /> -                     **sampleRate** -fréquence hello compteur doit être échantillonné.<br /><br /> Attribut facultatif :<br /><br /> **unité** -unité de mesure du compteur de hello de hello.|  

## <a name="performancecounterconfiguration-element"></a>Élément PerformanceCounterConfiguration  
 Hello tableau suivant décrit les éléments enfants :  

|Nom de l’élément|Description|  
|------------------|-----------------|  
|**annotation**|Attribut requis :<br /><br /> **displayName** -nom d’affichage hello pour le compteur de hello<br /><br /> Attribut facultatif :<br /><br /> **paramètres régionaux** -hello toouse de paramètres régionaux lors de l’affichage du nom du compteur hello|  

## <a name="windowseventlog-element"></a>Élément WindowsEventLog  
 Hello tableau suivant décrit les éléments enfants :  

|Nom de l’élément|Description|  
|------------------|-----------------|  
|**DataSource**|Hello toocollect de journaux des événements Windows. Attribut requis :<br /><br /> **nom** -requête XPath de hello décrivant hello windows événements toobe collectées. Par exemple :<br /><br /> `Application!*[System[(Level >= 3)]], System!*[System[(Level <=3)]], System!*[System[Provider[@Name='Microsoft Antimalware']]], Security!*[System[(Level >= 3]]`<br /><br /> tous les événements, de toocollect spécifier « * ».|
