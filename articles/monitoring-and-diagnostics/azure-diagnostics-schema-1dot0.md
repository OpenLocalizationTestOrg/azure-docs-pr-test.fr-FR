---
title: "aaaAzure schéma de Configuration de Diagnostics 1.0 | Documents Microsoft"
description: "Applicable UNIQUEMENT si vous utilisez le Kit de développement logiciel (SDK) Azure 2.4 et les versions antérieures avec Azure Virtual Machines, Virtual Machine Scale Sets, Service Fabric ou Cloud Services."
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
ms.openlocfilehash: bdd2b26217d6ea28f19e651ab429e7e7401ff57b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-diagnostics-10-configuration-schema"></a>Schéma de configuration Azure Diagnostics 1.0
> [!NOTE]
> Diagnostics Azure sont des compteurs de performance toocollect hello composant utilisé et d’autres statistiques à partir de Machines virtuelles Azure, machines virtuelles identiques, l’infrastructure de Service et les Services de Cloud.  Cette page vous concerne uniquement si vous utilisez l’un de ces services.
>

Azure Diagnostics est utilisé avec d’autres produits de diagnostic Microsoft tels que Azure Monitor, Application Insights et Log Analytics.

fichier de configuration des Diagnostics Windows Azure Hello définit des valeurs qui sont utilisées tooinitialize hello moniteur de diagnostic. Ce fichier est tooinitialize utilisé les paramètres de configuration de diagnostic lorsque hello diagnostics surveiller démarre.  

 Par défaut, le fichier de schéma de configuration de Diagnostics Windows Azure hello est toohello installé `C:\Program Files\Microsoft SDKs\Azure\.NET SDK\<version>\schemas` active. Remplacez `<version>` avec la version installée de hello Hello [Azure SDK](http://www.windowsazure.com/develop/downloads/).  

> [!NOTE]
>  fichier de configuration des diagnostics Hello est généralement utilisé avec les tâches de démarrage qui requièrent toobe de données de diagnostic collectée précédemment dans le processus de démarrage hello. Pour plus d’informations sur l’utilisation d’Azure Diagnostics, consultez [Collect Logging Data by Using Azure Diagnostics](assetId:///83a91c23-5ca2-4fc9-8df3-62036c37a3d7) (Collecte de données de journalisation à l’aide d’Azure Diagnostics).  

## <a name="example-of-hello-diagnostics-configuration-file"></a>Exemple de fichier de configuration de diagnostics hello  
 Bonjour à l’exemple suivant montre un fichier de configuration de diagnostics standard :  

```xml  
<?xml version="1.0" encoding="utf-8"?>
<DiagnosticMonitorConfiguration xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration"  
      configurationChangePollInterval="PT1M"  
      overallQuotaInMB="4096">  
   <DiagnosticInfrastructureLogs bufferQuotaInMB="1024"  
      scheduledTransferLogLevelFilter="Verbose"  
      scheduledTransferPeriod="PT1M" />  
   <Logs bufferQuotaInMB="1024"  
      scheduledTransferLogLevelFilter="Verbose"  
      scheduledTransferPeriod="PT1M" />  

   <Directories bufferQuotaInMB="1024"   
      scheduledTransferPeriod="PT1M">  

      <!-- These three elements specify hello special directories   
           that are set up for hello log types -->  
      <CrashDumps container="wad-crash-dumps" directoryQuotaInMB="256" />  
      <FailedRequestLogs container="wad-frq" directoryQuotaInMB="256" />  
      <IISLogs container="wad-iis" directoryQuotaInMB="256" />  

      <!-- For regular directories hello DataSources element is used -->  
      <DataSources>  
         <DirectoryConfiguration container="wad-panther" directoryQuotaInMB="128">  
            <!-- Absolute specifies an absolute path with optional environment expansion -->  
            <Absolute expandEnvironment="true" path="%SystemRoot%\system32\sysprep\Panther" />  
         </DirectoryConfiguration>  
         <DirectoryConfiguration container="wad-custom" directoryQuotaInMB="128">  
            <!-- LocalResource specifies a path relative tooa local   
                 resource defined in hello service definition -->  
            <LocalResource name="MyLoggingLocalResource" relativePath="logs" />  
         </DirectoryConfiguration>  
      </DataSources>  
   </Directories>  

   <PerformanceCounters bufferQuotaInMB="512" scheduledTransferPeriod="PT1M">  
      <!-- hello counter specifier is in hello same format as hello imperative   
           diagnostics configuration API -->  
      <PerformanceCounterConfiguration   
         counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT5S" />  
   </PerformanceCounters>  

   <WindowsEventLog bufferQuotaInMB="512"  
      scheduledTransferLogLevelFilter="Verbose"  
      scheduledTransferPeriod="PT1M">  
      <!-- hello event log name is in hello same format as hello imperative   
           diagnostics configuration API -->  
      <DataSource name="System!*" />  
   </WindowsEventLog>  
</DiagnosticMonitorConfiguration>  
```  

## <a name="diagnosticsconfiguration-namespace"></a>Espace de noms DiagnosticsConfiguration  
 espace de noms XML Hello pour le fichier de configuration de diagnostics hello est la suivante :  

```  
http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration  
```  

## <a name="schema-elements"></a>Éléments du schéma  
 fichier de configuration des diagnostics Hello inclut hello suivant d’éléments.


## <a name="diagnosticmonitorconfiguration-element"></a>Élément DiagnosticMonitorConfiguration  
élément de niveau supérieur Hello hello diagnostics du fichier de configuration.  

Attributs :

|Attribut  |Type   |Requis| Default | Description|  
|-----------|-------|--------|---------|------------|  
|**configurationChangePollInterval**|duration|Facultatif | PT1M| Spécifie l’intervalle de hello selon les interrogations du moniteur de diagnostic hello pour les modifications de configuration de diagnostic.|  
|**overallQuotaInMB**|unsignedInt|Facultatif| 4 000 Mo. La valeur indiquée ne doit pas dépasser ce montant |quantité totale de Hello du stockage de système de fichiers allouée pour toutes les mémoires tampons de journalisation.|  

## <a name="diagnosticinfrastructurelogs-element"></a>Élément DiagnosticInfrastructureLogs  
Définit la configuration de mémoire tampon hello pour les journaux hello qui sont générés par l’infrastructure de diagnostics sous-jacente hello.

Élément parent : [Élément DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).  

Attributs :

|Attribut|Type|Description|  
|---------|----|-----------------|  
|**bufferQuotaInMB**|unsignedInt|facultatif. Spécifie la quantité maximale de hello du stockage de système de fichiers est disponible pour hello spécifié données.<br /><br /> valeur par défaut Hello est 0.|  
|**scheduledTransferLogLevelFilter**|string|facultatif. Spécifie le niveau de gravité minimal hello pour les entrées de journal sont transférées. la valeur par défaut Hello est **Undefined**. Les autres valeurs possibles sont **Détaillé**, **Informations**, **Avertissement**, **Erreur**, et **Critique**.|  
|**scheduledTransferPeriod**|duration|facultatif. Spécifie l’intervalle de salutation entre les transferts planifiés de données, arrondies à toohello minute la plus proche.<br /><br /> valeur par défaut Hello est PT0S.|  

## <a name="logs-element"></a>Élément Logs  
 Définit la configuration du tampon hello pour les journaux Azure de base.

 Élément parent : [Élément DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).  

Attributs :  

|Attribut|Type|Description|  
|---------------|----------|-----------------|  
|**bufferQuotaInMB**|unsignedInt|facultatif. Spécifie la quantité maximale de hello du stockage de système de fichiers est disponible pour hello spécifié données.<br /><br /> valeur par défaut Hello est 0.|  
|**scheduledTransferLogLevelFilter**|string|facultatif. Spécifie le niveau de gravité minimal hello pour les entrées de journal sont transférées. la valeur par défaut Hello est **Undefined**. Les autres valeurs possibles sont **Détaillé**, **Informations**, **Avertissement**, **Erreur**, et **Critique**.|  
|**scheduledTransferPeriod**|duration|facultatif. Spécifie l’intervalle de salutation entre les transferts planifiés de données, arrondies à toohello minute la plus proche.<br /><br /> valeur par défaut Hello est PT0S.|  

## <a name="directories-element"></a>Élément Directories  
Définit la configuration du tampon hello pour les fichiers journaux que vous pouvez définir.

Élément parent : [Élément DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).  


Attributs :  

|Attribut|Type|Description|  
|---------------|----------|-----------------|  
|**bufferQuotaInMB**|unsignedInt|facultatif. Spécifie la quantité maximale de hello du stockage de système de fichiers est disponible pour hello spécifié données.<br /><br /> valeur par défaut Hello est 0.|  
|**scheduledTransferPeriod**|duration|facultatif. Spécifie l’intervalle de salutation entre les transferts planifiés de données, arrondies à toohello minute la plus proche.<br /><br /> valeur par défaut Hello est PT0S.|  

## <a name="crashdumps-element"></a>Élément CrashDumps  
 Définit le répertoire de vidages sur incident hello.

 Élément parent : [élément Directories](#Directories).  

Attributs :  

|Attribut|Type|Description|  
|---------------|----------|-----------------|  
|**container**|string|nom Hello du conteneur hello où contenu hello du répertoire de hello est toobe transféré.|  
|**directoryQuotaInMB**|unsignedInt|facultatif. Spécifie la taille maximale de hello du répertoire de hello en mégaoctets.<br /><br /> valeur par défaut Hello est 0.|  

## <a name="failedrequestlogs-element"></a>Élément FailedRequestLogs  
 Définit le répertoire du journal des demandes ayant échoué hello.

 Élément parent : [élément Directories](#Directories).  

Attributs :  

|Attribut|Type|Description|  
|---------------|----------|-----------------|  
|**container**|string|nom Hello du conteneur hello où contenu hello du répertoire de hello est toobe transféré.|  
|**directoryQuotaInMB**|unsignedInt|facultatif. Spécifie la taille maximale de hello du répertoire de hello en mégaoctets.<br /><br /> valeur par défaut Hello est 0.|  

##  <a name="iislogs-element"></a>Élément IISLogs  
 Définit le répertoire des journaux IIS hello.

 Élément parent : [élément Directories](#Directories).  

Attributs :  

|Attribut|Type|Description|  
|---------------|----------|-----------------|  
|**container**|string|nom Hello du conteneur hello où contenu hello du répertoire de hello est toobe transféré.|  
|**directoryQuotaInMB**|unsignedInt|facultatif. Spécifie la taille maximale de hello du répertoire de hello en mégaoctets.<br /><br /> valeur par défaut Hello est 0.|  

## <a name="datasources-element"></a>Élément DataSources  
 Définit zéro ou plusieurs répertoires de journaux supplémentaires.

 Élément parent : [élément Directories](#Directories).

## <a name="directoryconfiguration-element"></a>Élément DirectoryConfiguration  
 Définit le répertoire hello de toomonitor des fichiers journaux.

 Élément parent : [élément DataSources](#DataSources).

Attributs :

|Attribut|Type|Description|  
|---------------|----------|-----------------|  
|**container**|string|nom Hello du conteneur hello où contenu hello du répertoire de hello est toobe transféré.|  
|**directoryQuotaInMB**|unsignedInt|facultatif. Spécifie la taille maximale de hello du répertoire de hello en mégaoctets.<br /><br /> valeur par défaut Hello est 0.|  

## <a name="absolute-element"></a>Élément Absolute  
 Définit le chemin d’accès absolu de toomonitor de répertoire hello avec expansion d’environnement facultative.

 Élément parent : [élément DirectoryConfiguration](#DirectoryConfiguration).  

Attributs :  

|Attribut|Type|Description|  
|---------------|----------|-----------------|  
|**path**|string|Obligatoire. Bonjour toomonitor de répertoire toohello de chemin d’accès absolu.|  
|**expandEnvironment**|booléenne|Obligatoire. Si défini trop**true**, variables d’environnement dans le chemin d’accès de hello sont développées.|  

## <a name="localresource-element"></a>Élément LocalResource  
 Définit une ressource locale à chemin d’accès relatif tooa définie dans la définition de service hello.

 Élément parent : [élément DirectoryConfiguration](#DirectoryConfiguration).  

Attributs :  

|Attribut|Type|Description|  
|---------------|----------|-----------------|  
|**name**|string|Obligatoire. nom Hello de ressource locale hello contenant hello Active toomonitor.|  
|**relativePath**|string|Obligatoire. Bonjour toomonitor de chemin d’accès relatif toohello ressource locale.|  

## <a name="performancecounters-element"></a>Élément PerformanceCounters  
 Définit toocollect de compteur des performances hello chemin d’accès toohello.

 Élément parent : [Élément DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).


 Attributs :  

|Attribut|Type|Description|  
|---------------|----------|-----------------|  
|**bufferQuotaInMB**|unsignedInt|facultatif. Spécifie la quantité maximale de hello du stockage de système de fichiers est disponible pour hello spécifié données.<br /><br /> valeur par défaut Hello est 0.|  
|**scheduledTransferPeriod**|duration|facultatif. Spécifie l’intervalle de salutation entre les transferts planifiés de données, arrondies à toohello minute la plus proche.<br /><br /> valeur par défaut Hello est PT0S.|  

## <a name="performancecounterconfiguration-element"></a>Élément PerformanceCounterConfiguration  
 Définit toocollect de compteur de performances hello.

 Élément parent : [élément PerformanceCounters](#PerformanceCounters).  

 Attributs :  

|Attribut|Type|Description|  
|---------------|----------|-----------------|  
|**counterSpecifier**|string|Obligatoire. toocollect du compteur de performances de toohello Hello chemin d’accès.|  
|**sampleRate**|duration|Obligatoire. taux de Hello à quels hello compteur de performances doit être collecté.|  

## <a name="windowseventlog-element"></a>Élément WindowsEventLog  
 Définit toomonitor de journaux des événements hello.

 Élément parent : [Élément DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).

  Attributs :

|Attribut|Type|Description|  
|---------------|----------|-----------------|  
|**bufferQuotaInMB**|unsignedInt|facultatif. Spécifie la quantité maximale de hello du stockage de système de fichiers est disponible pour hello spécifié données.<br /><br /> valeur par défaut Hello est 0.|  
|**scheduledTransferLogLevelFilter**|string|facultatif. Spécifie le niveau de gravité minimal hello pour les entrées de journal sont transférées. la valeur par défaut Hello est **Undefined**. Les autres valeurs possibles sont **Détaillé**, **Informations**, **Avertissement**, **Erreur**, et **Critique**.|  
|**scheduledTransferPeriod**|duration|facultatif. Spécifie l’intervalle de salutation entre les transferts planifiés de données, arrondies à toohello minute la plus proche.<br /><br /> valeur par défaut Hello est PT0S.|  

## <a name="datasource-element"></a>Élément DataSource  
 Définit toomonitor du journal des événements hello.

 Élément parent : [élément WindowsEventLog](#windowsEventLog).  

 Attributs :

|Attribut|Type|Description|  
|---------------|----------|-----------------|  
|**name**|string|Obligatoire. Une expression XPath spécifiant hello journal toocollect.|  
