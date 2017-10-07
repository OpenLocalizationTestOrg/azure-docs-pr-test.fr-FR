---
title: "application du correctif logiciel de l’infrastructure de Service d’orchestration d’aaaAzure | Documents Microsoft"
description: "Tooautomate application fonctionne la mise à jour corrective du système sur un cluster Service Fabric."
services: service-fabric
documentationcenter: .net
author: novino
manager: timlt
editor: 
ms.assetid: de7dacf5-4038-434a-a265-5d0de80a9b1d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 5/9/2017
ms.author: nachandr
ms.openlocfilehash: fbb89aa2ea418181ee908a01850178c113c462fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="patch-hello-windows-operating-system-in-your-service-fabric-cluster"></a>Correctif logiciel de système de d’exploitation Windows hello dans votre cluster Service Fabric

application d’orchestration Hello correctif est une application Azure Service Fabric qui automatise le système d’exploitation mise à jour corrective sur un cluster Service Fabric sur Azure sans temps mort.

application d’orchestration Hello correctif fournit des éléments suivants de hello :

- **Installation automatique de mise à jour du système d’exploitation**. Des mises à jour du système d’exploitation sont téléchargées et installées automatiquement. Les nœuds de cluster sont redémarrés en fonction des besoins sans temps d’arrêt du cluster.

- **Application de correctifs et intégration de l’intégrité adaptées au cluster**. Lors de l’application des mises à jour, application d’orchestration hello correctif surveille l’intégrité de hello hello des nœuds de cluster. Les nœuds de cluster sont mis à niveau l’un après l’autre, ou domaine de mise à niveau après domaine de mise à niveau. Si le contrôle d’intégrité hello du cluster de hello tombe en panne en raison du processus de correction toohello, la mise à jour corrective est arrêté tooprevent aggraver le problème de hello.

## <a name="internal-details-of-hello-app"></a>Détails internes de l’application hello

application d’orchestration de correctif Hello est composée de hello suivant sous-composants :

- **Service Coordinateur** : ce service avec état est responsable des aspects suivants :
    - Coordonner le travail de mise à jour de Windows hello sur l’intégralité du cluster hello.
    - Le stockage de résultats des opérations terminées et mise à jour de Windows hello.
- **Service Agent du nœud** : ce service sans état s’exécute sur tous les nœuds de cluster Service Fabric. service de Hello est chargé de :
    - Amorçage hello du service NT de l’Agent de nœud.
    - Analyse hello du service NT de l’Agent de nœud.
- **service NT Agent du nœud** : ce service Windows NT s’exécute avec un privilège de niveau supérieur (système). En revanche, hello Service Agent de nœud et hello Service coordinateur d’exécutent avec un privilège de niveau inférieur (SERVICE réseau). service de Hello est chargé d’effectuer hello suivant des travaux de mise à jour de Windows sur tous les nœuds de cluster hello :
    - Désactivation de la mise à jour automatique de Windows sur le nœud de hello.
    - Téléchargement et installation des mises à jour Windows selon l’utilisateur de hello stratégie toohello a fourni.
    - Le redémarrage de billet d’ordinateur hello installation mise à jour de Windows.
    - Chargement des résultats hello de mises à jour de Windows toohello Service de coordinateur.
    - génération de rapport d’intégrité en cas d’échec de l’opération une fois toutes les nouvelles tentatives effectuées.

> [!NOTE]
> Hello correctif orchestration application utilise hello Service Fabric réparer toodisable de service manager système ou activer le nœud de hello et d’effectuer des vérifications d’intégrité. tâche de réparation Hello créé par hello correctif orchestration application pistes hello cours de mise à jour de Windows pour chaque nœud.

## <a name="prerequisites"></a>Composants requis

### <a name="minimum-supported-service-fabric-runtime-version"></a>Version du runtime Service Fabric minimale prise en charge

#### <a name="azure-clusters"></a>Clusters Azure
application d’orchestration Hello patch doit être exécutée sur des clusters Azure qui ont l’infrastructure de Service runtime version 5.5 ou version ultérieure.

#### <a name="standalone-on-premises-clusters"></a>Clusters locaux autonomes
application d’orchestration Hello correctif doit être exécutée sur les clusters autonomes qui ont la version 5.6 version de runtime Service Fabric ou une version ultérieure.

### <a name="enable-hello-repair-manager-service-if-its-not-running-already"></a>Activer le service de gestionnaire de réparation hello (si ce n’est pas déjà fait)

application d’orchestration Hello correctif requiert hello réparation Gestionnaire système service toobe est activé sur le cluster de hello.

#### <a name="azure-clusters"></a>Clusters Azure

Les clusters Azure dans le niveau de durabilité silver hello ont hello réparer service manager est activé par défaut. Les clusters Azure dans le niveau de durabilité gold hello peuvent ou peut-être pas le service de gestionnaire de réparation hello activé, en fonction de laquelle ces clusters ont été créées. Les clusters Azure dans le niveau de durabilité bronze hello, par défaut, n’ont pas hello de réparation de service manager est activé. Si le service de hello est déjà activé, vous pouvez le voir en cours d’exécution dans la section de services système hello Bonjour Service Fabric Explorer.

##### <a name="azure-portal"></a>Portail Azure
Vous pouvez activer le Gestionnaire de réparation à partir du portail Azure au moment de hello de configuration du cluster. Sélectionnez `Include Repair Manager` sous `Add on features` au moment de hello de configuration du Cluster.
![Image représentant l’activation du gestionnaire des réparations à partir du portail Azure](media/service-fabric-patch-orchestration-application/EnableRepairManager.png)

##### <a name="azure-resource-manager-template"></a>Modèle Azure Resource Manager
Vous pouvez également utiliser hello [modèle Azure Resource Manager](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) service de gestionnaire de réparation tooenable hello sur des clusters Service Fabric nouveaux et existants. Obtenir le modèle de hello pour le cluster de hello que vous souhaitez toodeploy. Vous pouvez utiliser des modèles d’exemple hello ou créer un modèle de gestionnaire de ressources personnalisé. 

tooenable hello réparation manager service à l’aide de [modèle Azure Resource Manager](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm):

1. Vérifiez tout d’abord que hello `apiversion` est défini trop`2017-07-01-preview` pour hello `Microsoft.ServiceFabric/clusters` ressource, comme indiqué dans hello suivant extrait de code. Si elle est différente, vous devez tooupdate hello `apiVersion` toohello valeur `2017-07-01-preview`:

    ```json
    {
        "apiVersion": "2017-07-01-preview",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
    }
    ```

2. Service de gestionnaire de réparation hello à présent activer en ajoutant des éléments suivants de hello `addonFeatures` section après hello `fabricSettings` section :

    ```json
    "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "RepairManager"
        ],
    ```

3. Une fois que vous avez mis à jour votre modèle de cluster avec ces modifications, appliquez-les et laissez la mise à niveau hello. Vous pouvez maintenant voir le service système hello réparation manager en cours d’exécution dans votre cluster. Il est appelé `fabric:/System/RepairManagerService` dans la section de services système hello Bonjour Service Fabric Explorer. 

### <a name="standalone-on-premises-clusters"></a>Clusters locaux autonomes

Vous pouvez utiliser hello [paramètres de Configuration de cluster de Windows autonome](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest) service de gestionnaire de réparation tooenable hello sur le cluster de Service Fabric nouveaux et existant.

service de gestionnaire de réparation tooenable hello :

1. Vérifiez tout d’abord que hello `apiversion` dans [configurations de cluster général](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest#general-cluster-configurations) est défini trop`04-2017` ou une version ultérieure :

    ```json
    {
        "name": "SampleCluster",
        "clusterConfigurationVersion": "1.0.0",
        "apiVersion": "04-2017",
        ...
    }
    ```

2. Service de gestionnaire de réparation à présent activer en ajoutant des éléments suivants de hello `addonFeaturres` section après hello `fabricSettings` section comme indiqué ci-dessous :

    ```json
    "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "RepairManager"
        ],
    ```

3. Mettre à jour votre manifeste de cluster avec ces modifications, à l’aide de manifeste du cluster hello mis à jour [créer un nouveau cluster](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-for-windows-server) ou [configuration de cluster de mise à niveau hello](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-upgrade-windows-server#Upgrade-the-cluster-configuration). Une fois que le cluster de hello est en cours d’exécution avec un manifeste de cluster mis à jour, vous pouvez maintenant voir le service système hello réparation manager en cours d’exécution dans votre cluster, qui est appelé `fabric:/System/RepairManagerService`, sous la section dans l’Explorateur de Service Fabric hello des services système.

### <a name="disable-automatic-windows-update-on-all-nodes"></a>Désactiver les mises à jour automatiques Windows Update sur tous les nœuds

Mises à jour automatiques de Windows peuvent provoquer des tooavailability perte, car plusieurs nœuds de cluster peuvent redémarrer hello même temps. application d’orchestration de correctif Hello, par défaut, les tentatives toodisable hello automatique Windows Update sur chaque nœud du cluster. Toutefois, si les paramètres de hello sont gérés par un administrateur ou d’une stratégie de groupe, nous vous recommandons de hello du paramètre stratégie trop « avertir avant le téléchargement « explicitement de la mise à jour Windows.

### <a name="optional-enable-azure-diagnostics"></a>Facultatif : Activer Azure Diagnostics

Pour les clusters exécutant la version du runtime Service Fabric `5.6.220.9494` ou une version supérieure, les journaux de l’application d’orchestration des correctifs sont collectés en même temps que les journaux Service Fabric.
Vous pouvez ignorer cette étape si votre cluster exécute le runtime Service Fabric version `5.6.220.9494` et plus.

Pour les clusters exécutant la version du runtime Service Fabric moins `5.6.220.9494`, journaux pour l’application d’orchestration hello correctif sont collectés localement sur chaque nœud de cluster hello.
Nous vous recommandons de configurer des journaux de tooupload de Diagnostics Windows Azure à partir de tous les nœuds tooa point central.

Pour plus d’informations sur l’activation d’Azure Diagnostics, voir [Collecte des journaux avec Azure Diagnostics](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-how-to-setup-wad).

Journaux pour l’application d’orchestration hello correctif sont générés sur hello suit les ID de fournisseur fixe :

- e39b723c-590c-4090-abb0-11e3e6616346
- fc0028ff-bfdc-499f-80dc-ed922c52c5e9
- 24afa313-0d3b-4c7c-b485-1047fd964b60
- 05dc046c-60e9-4ef7-965e-91660adffa68

Dans le Gestionnaire de ressources du modèle goto `EtwEventSourceProviderConfiguration` sous `WadCfg` et ajoutez hello suivant entrées :

```json
  {
    "provider": "e39b723c-590c-4090-abb0-11e3e6616346",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
      "eventDestination": "PatchOrchestrationApplicationTable"
    }
  },
  {
    "provider": "fc0028ff-bfdc-499f-80dc-ed922c52c5e9",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
    "eventDestination": " PatchOrchestrationApplicationTable"
    }
  },
  {
    "provider": "24afa313-0d3b-4c7c-b485-1047fd964b60",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
    "eventDestination": " PatchOrchestrationApplicationTable"
    }
  },
  {
    "provider": "05dc046c-60e9-4ef7-965e-91660adffa68",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
    "eventDestination": " PatchOrchestrationApplicationTable"
    }
  }
```

> [!NOTE]
> Si votre cluster Service Fabric a plusieurs types de nœuds, puis hello précédente doit être ajoutée pour toutes les hello `WadCfg` sections.

## <a name="download-hello-app-package"></a>Télécharger le package d’application hello

Télécharger l’application hello de hello [lien de téléchargement](https://go.microsoft.com/fwlink/P/?linkid=849590).

## <a name="configure-hello-app"></a>Configurer l’application hello

Hello le comportement de l’application d’orchestration hello correctif peut être configuré toomeet vos besoins. Remplacer les valeurs par défaut hello en passant dans le paramètre de l’application hello lors de la création d’application ou de mise à jour. Paramètres de l’application peuvent être fournis en spécifiant `ApplicationParameter` toohello `Start-ServiceFabricApplicationUpgrade` ou `New-ServiceFabricApplication` applets de commande.

|**Paramètre**        |**Type**                          | **Détails**|
|:-|-|-|
|MaxResultsToCache    |long                              | Nombre maximal de résultats d’exécution de Windows Update à mettre en cache. <br>La valeur par défaut est 3 000, en supposant ce qui suit : <br> - Le nombre de nœuds est 20. <br> - Le nombre de mises à jour par mois effectuées sur un nœud est 5. <br> - Le nombre maximal de résultats par opération est 10. <br> -Les résultats pour hello trois derniers mois doivent être stockées. |
|TaskApprovalPolicy   |Enum <br> { NodeWise, UpgradeDomainWise }                          |TaskApprovalPolicy indique la stratégie de hello toobe utilisé par les mises à jour tooinstall hello Service coordinateur entre les nœuds du cluster Service Fabric hello.<br>                         Les valeurs autorisées sont les suivantes : <br>                                                           <b>NodeWise</b>. Les mises à jour Windows Update sont installées de façon séquentielle, nœud après nœud. <br>                                                           <b>UpgradeDomainWise</b>. Les mises à jour Windows Update sont installées sur un domaine de mise à niveau à la fois (À hello maximale, tous les nœuds de hello appartenant domaine de mise à niveau tooan obtenir Windows Update.)
|LogsDiskQuotaInMB   |long  <br> (Par défaut : 1024)               |Taille maximale en Mo des journaux de l’application d’orchestration des correctifs qui peuvent être conservés localement sur des nœuds.
| WUQuery               | string<br>(Par défaut : « IsInstalled=0 »)                | Requête tooget Windows met à jour. Pour plus d’informations, voir [WuQuery](https://msdn.microsoft.com/library/windows/desktop/aa386526(v=vs.85).aspx).
| InstallWindowsOSOnlyUpdates | Bool <br> (Par défaut : True)                 | Cet indicateur permet toobe de mises à jour système installé de système d’exploitation Windows.            |
| WUOperationTimeOutInMinutes | Int <br>(Par défaut : 90)                   | Spécifie le délai d’attente hello pour toute opération de mise à jour de Windows (recherche ou téléchargement ou installation). Si l’opération de hello n’est pas effectuée dans hello de délai d’attente spécifié, elle est abandonnée.       |
| WURescheduleCount     | Int <br> (Par défaut : 5)                  | nombre maximal de Hello de service de hello replanifie hello Windows update au cas où une opération continue à échouer.          |
| WURescheduleTimeInMinutes | Int <br>(Par défaut : 30) | intervalle de salutation à quels hello service replanifie la mise à jour de Windows hello en cas de problème persiste. |
| WUFrequency           | Chaîne de valeurs séparées par des virgules (par défaut : « Hebdomadaire, Mercredi, 7:00:00 »).     | fréquence de Hello pour l’installation de Windows Update. les valeurs Hello format et possibles sont : <br>-   Mensuelle, JJ,HH:MM:SS, par exemple, Mensuelle, 5,12:22:32. <br> -   Hebdomadaire, JOUR,HH:MM:SS, par exemple, Hebdomadaire, Mardi, 12:22:32.  <br> -   Quotidienne, HH:MM:SS, par exemple, Quotidienne, 12:22:32.  <br> -  Aucune  indique que les mises à jour Windows Update ne doivent pas être effectuées.  <br><br> Notez que toutes les heures de hello sont au format UTC.|
| AcceptWindowsUpdateEula | Bool <br>(Par défaut : true) | En définissant cet indicateur, application hello accepte hello contrat de licence par l’utilisateur pour Windows Update pour le compte de propriétaire hello de l’ordinateur de hello.              |

> [!TIP]
> Si vous souhaitez que Windows Update toohappen immédiatement, définissez `WUFrequency` le temps de déploiement d’application toohello relatif. Par exemple, supposons que vous avez une application de hello de toodeploy cluster et le plan de test de nœud de cinq à environ 5 h 00 UTC. Si vous supposez que le déploiement ou mise à niveau des applications hello prend 30 minutes à hello hello maximale, définissez WUFrequency en tant que « Tous les jours, 17:30:00. »

## <a name="deploy-hello-app"></a>Déployer l’application hello

1. Terminer tous les clusters de hello de tooprepare hello étapes préliminaires.
2. Déploiement d’une application d’orchestration de correctif hello comme toute autre application de Service Fabric. Vous pouvez déployer l’application hello à l’aide de PowerShell. Suivez les étapes de hello dans [déployer et supprimer des applications à l’aide de PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).
3. application de hello tooconfigure au moment de hello du déploiement, passez hello `ApplicationParamater` toohello `New-ServiceFabricApplication` applet de commande. Pour votre commodité, nous vous avons fourni script hello Deploy.ps1 en même temps que l’application hello. script de hello toouse :

    - Connecter le cluster Service Fabric de tooa à l’aide de `Connect-ServiceFabricCluster`.
    - Exécuter le script hello PowerShell Deploy.ps1 avec hello approprié `ApplicationParameter` valeur.

> [!NOTE]
> Conserver le script de hello et le dossier de l’application hello PatchOrchestrationApplication Bonjour même répertoire.

## <a name="upgrade-hello-app"></a>Mise à niveau d’application hello

tooupgrade une application d’orchestration correctif existante à l’aide de PowerShell, suivez les étapes de hello dans [mise à niveau de l’application Service Fabric à l’aide de PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-upgrade-tutorial-powershell).

## <a name="remove-hello-app"></a>Supprimer l’application hello

application de hello tooremove, suivez les étapes hello dans [déployer et supprimer des applications à l’aide de PowerShell](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).

Pour votre commodité, nous vous avons fourni script hello Undeploy.ps1 en même temps que l’application hello. script de hello toouse :

  - Connecter le cluster Service Fabric de tooa à l’aide de ```Connect-ServiceFabricCluster```.

  - Exécuter le script PowerShell de hello Undeploy.ps1.

> [!NOTE]
> Conserver le script de hello et le dossier de l’application hello PatchOrchestrationApplication Bonjour même répertoire.

## <a name="view-hello-windows-update-results"></a>Afficher les résultats de mise à jour de Windows hello

application d’orchestration Hello correctif expose utilisateur toohello d’API REST toodisplay hello historique des résultats. Un exemple de résultat de hello JSON :
```json
[
  {
    "NodeName": "_stg1vm_1",
    "WindowsUpdateOperationResults": [
      {
        "OperationResult": 0,
        "NodeName": "_stg1vm_1",
        "OperationTime": "2017-05-21T11:46:52.1953713Z",
        "UpdateDetails": [
          {
            "UpdateId": "7392acaf-6a85-427c-8a8d-058c25beb0d6",
            "Title": "Cumulative Security Update for Internet Explorer 11 for Windows Server 2012 R2 (KB3185319)",
            "Description": "A security issue has been identified in a Microsoft software product that could affect your system. You can help protect your system by installing this update from Microsoft. For a complete listing of hello issues that are included in this update, see hello associated Microsoft Knowledge Base article. After you install this update, you may have toorestart your system.",
            "ResultCode": 0
          }
        ],
        "OperationType": 1,
        "WindowsUpdateQuery": "IsInstalled=0",
        "WindowsUpdateFrequency": "Daily,10:00:00",
        "RebootRequired": false
      }
    ]
  },
  ...
]
```
Si aucune mise à jour n’est planifiée encore, le résultat de hello JSON est vide.

Consigner les résultats dans un cluster de toohello tooquery mise à jour de Windows. Puis savoir adresse hello réplica principal hello Hello coordinateur Service et d’accès URL hello à partir du navigateur de hello : http://&lt;IP de RÉPLICA&gt;:&lt;ApplicationPort&gt;/PatchOrchestrationApplication/v1 GetWindowsUpdateResults.

point de terminaison REST Hello pour hello coordinateur Service dispose d’un port dynamique. toocheck hello URL exacte, consultez le toohello Service Fabric Explorer. Par exemple, les résultats de hello sont disponibles sur `http://10.0.0.7:20000/PatchOrchestrationApplication/v1/GetWindowsUpdateResults`.

![Image de point de terminaison REST](media/service-fabric-patch-orchestration-application/Rest_Endpoint.png)


Si le proxy inverse de hello est activé sur le cluster de hello, vous pouvez accéder à des URL hello à partir d’en dehors du cluster hello.
Hello du point de terminaison doit toobe atteint est http://&lt;SERVERURL&gt;:&lt;REVERSEPROXYPORT&gt;/PatchOrchestrationApplication/CoordinatorService/v1/GetWindowsUpdateResults.

proxy inverse de hello tooenable sur le cluster de hello, suivez les étapes de hello dans [proxy dans Azure Service Fabric inverse](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy). 

> 
> [!WARNING]
> Après la configuration de proxy inverse de hello, tous les services cluster de hello micro qui exposent un point de terminaison HTTP sont adressables à partir de l’extérieur hello cluster.

## <a name="diagnosticshealth-events"></a>Événements de diagnostic et d’intégrité

### <a name="collect-patch-orchestration-app-logs"></a>Collecter les journaux de l’application d’orchestration des correctifs

Depuis la version du runtime `5.6.220.9494`, les journaux de l’application d’orchestration des correctifs sont collectés en même temps que les journaux Service Fabric.
Pour les clusters exécutant la version du runtime Service Fabric moins `5.6.220.9494`, les journaux peuvent être collectées à l’aide d’une des méthodes suivantes de hello.

#### <a name="locally-on-each-node"></a>Localement sur chaque nœud

Si la version du runtime Service Fabric est inférieure à `5.6.220.9494`, les journaux sont collectés en local sur chaque nœud du cluster Service Fabric. Bonjour emplacement tooaccess hello journaux est \[Service Fabric\_Installation\_lecteur\]:\\PatchOrchestrationApplication\\journaux.

Par exemple, si le Service Fabric est installé sur le lecteur D, chemin d’accès hello est D:\\PatchOrchestrationApplication\\journaux.

#### <a name="central-location"></a>Emplacement central

Si les Diagnostics Azure est configuré en tant que partie des étapes requises, les journaux pour l’application d’orchestration hello correctif sont disponibles dans le stockage Azure.

### <a name="health-reports"></a>Rapports d'intégrité

application d’orchestration Hello correctif publie également les rapports d’intégrité sur hello Service coordinateur ou hello Service Agent de nœud Bonjour suivant cas :

#### <a name="a-windows-update-operation-failed"></a>Une opération de Windows Update a échoué

Si une opération de mise à jour Windows échoue sur un nœud, un rapport d’intégrité est généré sur hello Service Agent de nœud. Détails du rapport de contrôle d’intégrité hello contiennent le nom du nœud problématique hello.

Une fois la mise à jour corrective est effectuée avec succès sur le nœud de problématique hello, rapport de hello est automatiquement effacé.

#### <a name="hello-node-agent-ntservice-is-down"></a>Hello du service NT de l’Agent de nœud est arrêté

Si hello du service NT de l’Agent de nœud est arrêté sur un nœud, un rapport d’intégrité du niveau d’avertissement est généré par rapport à hello Service Agent de nœud.

#### <a name="hello-repair-manager-service-is-not-enabled"></a>service de gestionnaire de réparation Hello n’est pas activé.

Si le service de gestionnaire de réparation hello est introuvable sur le cluster de hello, un rapport d’intégrité du niveau d’avertissement est généré pour hello Service coordinateur.

## <a name="frequently-asked-questions"></a>Forum Aux Questions

Q : **Pourquoi mon cluster dans un état d’erreur lors de l’application d’orchestration hello correctif est en cours d’exécution ?**

R : Au cours du processus d’installation hello, application d’orchestration hello correctif désactive ou redémarre les nœuds, ce qui peuvent provoquer temporairement une intégrité de cluster hello descendent hello.

Selon la stratégie de hello pour une application hello, soit un seul nœud peut s’arrêtent pendant une opération de mise à jour corrective *ou* tout un domaine de mise à niveau peut accéder simultanément vers le bas.

Fin de hello de hello installation mise à jour de Windows, hello réactiver des nœuds après le redémarrage.

Dans l’exemple suivant de hello, cluster de hello est allé état d’erreur tooan temporairement, car les deux nœuds ont été vers le bas et hello MaxPercentageUnhealthNodes stratégie a été violée. Erreur de Hello est temporaire jusqu'à ce que l’opération de mise à jour corrective de hello est en cours.

![Image de cluster défectueux](media/service-fabric-patch-orchestration-application/MaxPercentage_causing_unhealthy_cluster.png)

Si hello problème persiste, consultez Dépannage toohello.

Q : **L’application d’orchestration des correctifs est en état d’avertissement**

R : Vérifiez toosee si un rapport d’intégrité validé par rapport à l’application hello est la cause première hello. En règle générale, les avertissement hello contient les détails du problème de hello. Si le problème de hello est transitoire, application hello est attendu tooauto-restaurer à partir de cet état.

Q : **Que puis-je faire si mon cluster n’est pas intègre et que j’ai besoin d’une mise à jour des systèmes d’exploitation urgente de toodo ?**

R : application d’orchestration Hello correctif n’installe pas les mises à jour pendant que le cluster de hello n’est pas sain. Essayez toobring votre cluster tooa état sain toounblock hello correctif orchestration application flux de travail.

Q : **Pourquoi mise à jour corrective sur tous les clusters si longue toorun ?**

R : Durée Hello requise par l’application d’orchestration hello correctif dépend principalement de hello suivant facteurs :

- stratégie de Hello de hello Service coordinateur. 
  - Hello stratégie par défaut, `NodeWise`, entraîne la mise à jour corrective de qu’un seul nœud à la fois. En particulier dans les cas de hello des clusters de plus grandes, nous vous recommandons d’utiliser hello `UpgradeDomainWise` tooachieve stratégie plus rapide de mise à jour corrective sur tous les clusters.
- nombre de Hello de mises à jour disponibles pour téléchargement et l’installation. 
- Hello toodownload de temps moyen nécessité et installer une mise à jour, qui ne doit pas dépasser quelques heures.
- Hello les performances de la bande passante réseau et de la machine virtuelle hello.

Q : **Pourquoi certaines mises à jour dans les résultats de la mise à jour Windows obtenues via les api REST, mais pas sous hello l’historique de Windows Update sur l’ordinateur**

R : Certaines mises à jour du produit doivent toobe archivé leur historique de mise à jour/patch respectifs. Ainsi, les mises à jour de Windows Defender ne s’affichent pas dans l’historique Windows Update de Windows Server 2016.

## <a name="disclaimers"></a>Clauses d’exclusion de responsabilité

- application d’orchestration Hello correctif accepte hello contrat de licence par l’utilisateur de Windows Update pour le compte d’utilisateur de hello. Si vous le souhaitez, paramètre de hello peut être désactivée dans la configuration de hello de l’application hello.

- application d’orchestration Hello correctif collecte des performances et l’utilisation de télémétrie tootrack. données de télémétrie de l’application Hello suivant le paramètre hello du paramètre de télémétrie du runtime de Service Fabric hello (qui est activée par défaut).

## <a name="troubleshooting"></a>Résolution des problèmes

### <a name="a-node-is-not-coming-back-tooup-state"></a>Un nœud ne provient pas revenir tooup état

**nœud de Hello peut être bloquée dans un état de désactivation, car**:

Une vérification de sécurité est en attente. tooremedy cette situation, assurez-vous que suffisamment de nœuds est disponibles dans un état sain.

**nœud de Hello peut être bloquée dans un état désactivé, car**:

- nœud de Hello a été désactivé manuellement.
- nœud de Hello a été désactivée en raison de travail d’infrastructure Azure en cours tooan.
- nœud de Hello a été désactivé temporairement par hello correctif application toopatch hello ce nœud.

**Hello nœud peut être bloqué dans un état hors service car**:

- nœud de Hello a été mis hors service manuellement.
- nœud de Hello est en cours de redémarrage (qui peut être déclenché par application d’orchestration hello correctif).
- nœud de Hello est arrêté en raison de tooa défectueux machine virtuelle ou ordinateur ou réseau problèmes de connectivité.

### <a name="updates-were-skipped-on-some-nodes"></a>Lises à jour ont été ignorés sur certains nœuds

application d’orchestration Hello correctif tente tooinstall une stratégie Windows update conséquente toohello replanification. service de Hello tente de nœud de hello toorecover et ignorer la stratégie d’application toohello conséquente hello mise à jour.

Dans ce cas, un rapport d’intégrité du niveau d’avertissement est généré par rapport à hello Service Agent de nœud. résultat de Hello pour la mise à jour de Windows contient également des raisons de l’échec de hello hello.

### <a name="hello-health-of-hello-cluster-goes-tooerror-while-hello-update-installs"></a>contrôle d’intégrité Hello du cluster de hello passe tooerror pendant l’installation de mise à jour hello

Une mise à jour Windows défectueux peut arrêter de contrôle d’intégrité hello d’une application ou d’un cluster sur un nœud particulier ou d’un domaine de mise à niveau. application d’orchestration Hello correctif interrompt toutes les opérations de mise à jour Windows jusqu'à ce que le cluster de hello est à nouveau intègre.

Un administrateur doit intervenir et déterminer pourquoi application hello ou un cluster est devenu non intègre d’échéance tooWindows mise à jour.

## <a name="release-notes-"></a>Notes de publication :

### <a name="version-110"></a>Version 1.1.0
- Version publique

### <a name="version-111"></a>Version 1.1.1
- Correction d’un bogue dans le paramètre SetupEntryPoint de NodeAgentService, qui empêchait l’installation de NodeAgentNTService.

### <a name="version-120-latest"></a>Version 1.2.0 (dernière version)

- Résolution de bogues liés au flux de travail de redémarrage du système.
- Correctif de bogue dans la création de tâches du Gestionnaire de ressources en raison de la vérification d’intégrité de toowhich pendant la préparation des tâches de réparation ne se produisait pas comme prévu.
- Mode de démarrage hello modifié pour le service windows POANodeSvc automatique toodelayed-auto.
