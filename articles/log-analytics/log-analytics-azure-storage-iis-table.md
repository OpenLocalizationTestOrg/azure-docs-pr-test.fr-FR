---
title: "stockage d’objets blob aaaUse pour le stockage IIS et de table pour les événements de l’Analytique des journaux Azure | Documents Microsoft"
description: "Analytique de journal peut lire des journaux hello pour les services Azure qui écrivent stockage tootable de diagnostics ou journaux IIS écrits tooblob stockage."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: bf444752-ecc1-4306-9489-c29cb37d6045
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: magoedte
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ff3de04dc8cb6729c1443372ec31a0e8dc47f273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-blob-storage-for-iis-and-azure-table-storage-for-events-with-log-analytics"></a>Utilisation d’un Stockage Blob Azure pour IIS et d’un Stockage Table Azure pour les événements avec Log Analytics

Analytique de journal peut lire les journaux hello pour hello suivant des services qui écrivent des diagnostics tootable stockage ou IIS consigne écrite tooblob stockage :

* Clusters Service Fabric (version préliminaire)
* Machines virtuelles
* Rôle de travail/web

Pour que Log Analytics puisse collecter les données pour ces ressources, les diagnostics Azure doivent être activés.

Une fois les diagnostics sont activés, vous pouvez utiliser hello portail Azure ou PowerShell configurer les journaux de hello toocollect Analytique de journal.

Diagnostics Azure est une extension d’Azure qui vous permet de toocollect les données de diagnostic à partir d’un rôle de travail, un rôle web ou un ordinateur virtuel en cours d’exécution dans Azure. les données de salutation sont stockées dans un compte de stockage Azure et peuvent ensuite être recueillies en Analytique de journal.

Pour l’Analytique des journaux toocollect ces journaux de Diagnostics Windows Azure, hello journaux doit se trouver dans hello emplacements suivants :

| Type de journal | Type de ressource | Lieu |
| --- | --- | --- |
| Journaux IIS |Machines virtuelles <br> Rôles web <br> Rôles de travail |wad-iis-logfiles (Stockage Blob) |
| syslog |Machines virtuelles |LinuxSyslogVer2v0 (Stockage Table) |
| Événements opérationnels Service Fabric |Nœuds Service Fabric |WADServiceFabricSystemEventTable |
| Événements Reliable Actor Service Fabric |Nœuds Service Fabric |WADServiceFabricReliableActorEventTable |
| Événements de service fiable Service Fabric |Nœuds Service Fabric |WADServiceFabricReliableServiceEventTable |
| Journaux d'événements Windows |Nœuds Service Fabric <br> Machines virtuelles <br> Rôles web <br> Rôles de travail |WADWindowsEventLogsTable (Stockage Table) |
| Journaux de suivi des événements ETW Windows |Nœuds Service Fabric <br> Machines virtuelles <br> Rôles web <br> Rôles de travail |WADETWEventTable (Stockage Table) |

> [!NOTE]
> Les journaux IIS des sites Web Azure ne sont actuellement pas pris en charge.
>
>

Pour les ordinateurs virtuels, vous pouvez hello installation hello [agent d’Analytique de journal](log-analytics-azure-vm-extension.md) dans votre machine virtuelle tooenable des informations supplémentaires. En outre les journaux IIS en mesure de tooanalyze toobeing et les journaux des événements, vous pouvez effectuer des analyses supplémentaires, notamment l’évaluation de la mise à jour, de suivi des modifications de configuration et d’évaluation de SQL.

## <a name="enable-azure-diagnostics-in-a-virtual-machine-for-event-log-and-iis-log-collection"></a>Activation des diagnostics Azure dans une machine virtuelle pour la collecte des journaux IIS et des journaux des événements
Hello utilisation suivant la procédure tooenable diagnostics Azure dans une machine virtuelle pour le journal des événements et IIS de collecte à l’aide du portail Microsoft Azure hello des journaux.

### <a name="tooenable-azure-diagnostics-in-a-virtual-machine-with-hello-azure-portal"></a>tooenable diagnostics Azure dans une machine virtuelle avec hello portail Azure
1. Installez hello Agent de machine virtuelle lorsque vous créez une machine virtuelle. Si l’ordinateur virtuel de hello existe déjà, vérifiez que hello Qu'agent de machine virtuelle est déjà installé.

   * Dans hello portail Azure, accédez toohello virtuels, sélectionnez **Configuration facultative**, puis **Diagnostics** et **état** trop**sur**.

     À l’achèvement, hello VM porte l’extension de Diagnostics Windows Azure hello installé et en cours d’exécution. Cette extension est chargée de collecter vos données de diagnostic.
2. Activation de l’analyse et configuration de la journalisation des événements sur une machine virtuelle existante. Vous pouvez activer les diagnostics au hello au niveau de la machine virtuelle. tooenable diagnostics et ensuite configurer la journalisation des événements, effectuer hello comme suit :

   1. Sélectionnez hello machine virtuelle.
   2. Cliquez sur **Analyse**.
   3. Cliquez sur **Diagnostics**.
   4. Ensemble hello **état** trop**ON**.
   5. Sélectionnez chaque journal de diagnostics que vous souhaitez toocollect.
   6. Cliquez sur **OK**.

## <a name="enable-azure-diagnostics-in-a-web-role-for-iis-log-and-event-collection"></a>Activation des diagnostics Azure dans un rôle Web pour la collecte de journaux IIS et des événements
Consultez trop[comment tooEnable Diagnostics dans un Service Cloud](../cloud-services/cloud-services-dotnet-diagnostics.md) pour obtenir des instructions générales sur l’activation des diagnostics Windows Azure. instructions Hello ci-dessous utilisent ces informations et le personnaliser pour une utilisation avec Analytique de journal.

Avec les diagnostics Azure activés :

* Journaux IIS sont stockés par défaut, avec les données transférées à l’intervalle de transfert scheduledTransferPeriod Bonjour.
* Les journaux des événements Windows ne sont pas transférés par défaut.

### <a name="tooenable-diagnostics"></a>tooenable diagnostics
tooenable journaux des événements Windows ou toochange hello scheduledTransferPeriod, configurez les Diagnostics Windows Azure à l’aide du fichier de configuration hello XML (diagnostics.wadcfg), comme indiqué dans [étape 4 : créer votre fichier de configuration de Diagnostics et installer hello extension](../cloud-services/cloud-services-dotnet-diagnostics.md)

Hello exemple de fichier de configuration suivant collecte les journaux IIS et tous les événements à partir de l’Application de hello et les journaux système :

```
    <?xml version="1.0" encoding="utf-8" ?>
    <DiagnosticMonitorConfiguration xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration"
          configurationChangePollInterval="PT1M"
          overallQuotaInMB="4096">

      <Directories bufferQuotaInMB="0"
         scheduledTransferPeriod="PT10M">  
        <!-- IISLogs are only relevant tooWeb roles -->
        <IISLogs container="wad-iis" directoryQuotaInMB="0" />
      </Directories>

      <WindowsEventLog bufferQuotaInMB="0"
         scheduledTransferLogLevelFilter="Verbose"
         scheduledTransferPeriod="PT10M">
        <DataSource name="Application!*" />
        <DataSource name="System!*" />
      </WindowsEventLog>

    </DiagnosticMonitorConfiguration>
```

Assurez-vous que votre élément ConfigurationSettings spécifie un compte de stockage, comme dans hello l’exemple suivant :

```
    <ConfigurationSettings>
       <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"/>
    </ConfigurationSettings>
```

Hello **AccountName** et **AccountKey** valeurs trouvent Bonjour Azure portal dans le tableau de bord des comptes de stockage de hello, sous Gérer les clés d’accès. protocole Hello pour la chaîne de connexion hello doit être **https**.

Une fois la configuration de diagnostic mise à jour hello est appliquée tooyour le service cloud et écrit les diagnostics tooAzure stockage, vous êtes prêt tooconfigure Analytique de journal.

## <a name="use-hello-azure-portal-toocollect-logs-from-azure-storage"></a>Utiliser les journaux de toocollect portail Azure hello depuis le stockage Azure
Vous pouvez utiliser les journaux de hello toocollect de hello tooconfigure portail Azure Analytique de journal pour hello suivant des services Azure :

* Clusters Service Fabric
* Machines virtuelles
* Rôle de travail/web

Bonjour portail Azure, accédez d’espace de travail tooyour Analytique de journal, exécutez les hello tâches suivantes :

1. Cliquez sur *Journaux des comptes de stockage*.
2. Cliquez sur hello *ajouter* tâche
3. Sélectionnez le compte de stockage hello qui contient les journaux de diagnostic hello
   * Ce compte peut être un compte de stockage classique ou un compte de stockage Azure Resource Manager
4. Sélectionnez hello, Type de données des journaux de toocollect pour
   * choix de Hello sont des journaux IIS ; Événements ; Syslog (Linux) ; Journaux ETW ; Événements de l’infrastructure de service
5. valeur Hello pour la Source est automatiquement rempli avec hello, type de données et ne peut pas être modifiées.
6. Cliquez sur OK toosave hello configuration

Répétez les étapes 2 à 6 pour les types de comptes et les données supplémentaires de stockage que vous souhaitez Analytique de journal toocollect.

Dans environ 30 minutes, vous êtes en mesure de toosee données hello compte de stockage dans le journal Analytique. Vous verrez seulement les données écrites toostorage après que hello configuration est appliquée. Analytique de journal ne lit pas les données préexistantes hello hello compte de stockage.

> [!NOTE]
> portail de Hello ne valide pas que hello Source existe dans le compte de stockage hello ou si les données nouvelles sont écrites.
>
>

## <a name="enable-azure-diagnostics-in-a-virtual-machine-for-event-log-and-iis-log-collection-using-powershell"></a>Activer les diagnostics Azure dans une machine virtuelle pour la collecte des journaux IIS et des journaux des événements avec PowerShell
Hello d’utiliser les étapes [tooindex d’Analytique de journal Configuration des diagnostics Azure](log-analytics-powershell-workspace-configuration.md#configuring-log-analytics-to-index-azure-diagnostics) tooread de PowerShell toouse des diagnostics Azure qui sont écrites tootable stockage.

À l’aide d’Azure PowerShell vous pouvez spécifier plus précisément les événements hello écrits tooAzure stockage.
Pour plus d'informations, consultez la page [Activation des diagnostics dans les machines virtuelles Azure](../virtual-machines-dotnet-diagnostics.md).

Vous pouvez activer et mettre à jour des diagnostics Windows Azure à l’aide de hello suite du script PowerShell.
Vous pouvez également utiliser ce script avec une configuration de journalisation personnalisée.
Modifier le compte de stockage hello script tooset hello, nom du service et nom d’ordinateur virtuel.
script de Hello utilise des applets de commande pour les machines virtuelles classiques.

Examinez hello suivant l’exemple de script, copiez-le, modifiez-le si nécessaire, enregistrez l’exemple hello dans un fichier de script PowerShell, puis exécutez le script de hello.

```
    #Connect tooAzure
    Add-AzureAccount

    # settings toochange:
    $wad_storage_account_name = "myStorageAccount"
    $service_name = "myService"
    $vm_name = "myVM"

    #Construct Azure Diagnostics public config and convert tooconfig format

    # Collect just system error events:
    $wad_xml_config = "<WadCfg><DiagnosticMonitorConfiguration><WindowsEventLog scheduledTransferPeriod=""PT1M""><DataSource name=""System!* "" /></WindowsEventLog></DiagnosticMonitorConfiguration></WadCfg>"

    $wad_b64_config = [System.Convert]::ToBase64String([System.Text.Encoding]::UTF8.GetBytes($wad_xml_config))
    $wad_public_config = [string]::Format("{{""xmlCfg"":""{0}""}}",$wad_b64_config)

    #Construct Azure diagnostics private config

    $wad_storage_account_key = (Get-AzureStorageKey $wad_storage_account_name).Primary
    $wad_private_config = [string]::Format("{{""storageAccountName"":""{0}"",""storageAccountKey"":""{1}""}}",$wad_storage_account_name,$wad_storage_account_key)

    #Enable Diagnostics Extension for Virtual Machine

    $wad_extension_name = "IaaSDiagnostics"
    $wad_publisher = "Microsoft.Azure.Diagnostics"
    $wad_version = (Get-AzureVMAvailableExtension -Publisher $wad_publisher -ExtensionName $wad_extension_name).Version # Gets latest version of hello extension

    (Get-AzureVM -ServiceName $service_name -Name $vm_name) | Set-AzureVMExtension -ExtensionName $wad_extension_name -Publisher $wad_publisher -PublicConfiguration $wad_public_config -PrivateConfiguration $wad_private_config -Version $wad_version | Update-AzureVM
```


## <a name="next-steps"></a>Étapes suivantes
* [Collecter les journaux et les indicateurs de performance des services Azure](log-analytics-azure-storage.md) pour les services pris en charge par Azure.
* [Activer des Solutions](log-analytics-add-solutions.md) tooprovide comprendre les données de hello.
* [Utiliser des requêtes de recherche](log-analytics-log-searches.md) tooanalyze les données de salutation.
