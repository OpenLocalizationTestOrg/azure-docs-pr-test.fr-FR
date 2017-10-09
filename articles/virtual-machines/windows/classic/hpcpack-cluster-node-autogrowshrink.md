---
title: "nœuds de cluster HPC Pack aaaAutoscale | Documents Microsoft"
description: "Augmenter automatiquement et de réduire le nombre de hello de nœuds de calcul de cluster HPC Pack dans Azure"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: 
editor: tysonn
ms.assetid: 38762cd1-f917-464c-ae5d-b02b1eb21e3f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 12/08/2016
ms.author: danlep
ms.openlocfilehash: 0bdf55625d337a2bbfe05677682d645a584798d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-grow-and-shrink-hello-hpc-pack-cluster-resources-in-azure-according-toohello-cluster-workload"></a>Développer et réduire les ressources de cluster HPC Pack hello dans Azure en fonction de la charge du cluster toohello automatiquement
Si vous déployez des nœuds de « Croissance » Azure dans votre cluster HPC Pack, ou si vous créez un cluster HPC Pack dans les machines virtuelles Azure, vous souhaiterez peut-être un moyen pour augmenter ou réduire les ressources de cluster hello tels que des nœuds ou des noyaux en fonction de la charge de travail hello sur le cluster de hello automatiquement. Mise à l’échelle des ressources de cluster hello de cette façon vous permet de toouse vos ressources Azure plus efficacement et de contrôler leurs coûts.

Cet article montre deux manières de HPC Pack fournit des ressources de calcul tooautoscale :

* Hello, propriété de cluster HPC Pack **AutoGrowShrink**

* Hello **AzureAutoGrowShrink.ps1** script PowerShell HPC

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

Actuellement, vous ne pouvez qu’augmenter ou diminuer automatiquement les nœuds de calcul HPC Pack qui exécutent un système d’exploitation Windows Server.


## <a name="set-hello-autogrowshrink-cluster-property"></a>Définir la propriété de cluster hello AutoGrowShrink
### <a name="prerequisites"></a>Composants requis

* **HPC Pack 2012 R2 Update 2 ou ultérieur cluster** -nœud principal du cluster hello peut être déployé localement ou dans une machine virtuelle Azure. Consultez [configurer un cluster hybride avec HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) tooget a démarré avec un nœud principal local et les nœuds de « Croissance » Azure. Consultez hello [script de déploiement IaaS de HPC Pack](hpcpack-cluster-powershell-script.md) tooquickly déployer un cluster HPC Pack dans des machines virtuelles Azure.

* **Pour un cluster avec un nœud principal dans Azure (modèle de déploiement Resource Manager)** : à partir de HPC Pack 2016, l’authentification par certificat dans une application Azure Active Directory est utilisée pour la croissance et la réduction automatiques de machines virtuelles de cluster déployées à l’aide d’Azure Resource Manager. Configurez un certificat de la façon suivante :

  1. Après le déploiement de cluster, se connecter par le nœud principal tooone de bureau à distance.

  2. Télécharger le nœud principal du tooeach hello certificat (format PFX avec une clé privée) et installer tooCert:\LocalMachine\My et Cert : \LocalMachine\Root.

  3. Démarrer PowerShell Azure en tant qu’administrateur et exécutez hello suivant de commandes sur un seul nœud principal :

    ```powershell
        cd $env:CCP_HOME\bin

        Login-AzureRmAccount
    ```
        
    Si votre compte est en plus d’un client Azure Active Directory ou d’un abonnement Azure, vous pouvez exécuter les éléments suivants de hello commande locataire approprié de tooselect hello et d’abonnement :
  
    ```powershell
        Login-AzureRMAccount -TenantId <TenantId> -SubscriptionId <subscriptionId>
    ```     
       
    Exécutez hello suivant commande tooview hello actuellement sélectionné locataire et abonnement :
    
    ```powershell
        Get-AzureRMContext
    ```

  4. Exécutez hello script suivant

    ```powershell
        .\ConfigARMAutoGrowShrinkCert.ps1 -DisplayName “YourHpcPackAppName” -HomePage "https://YourHpcPackAppHomePage" -IdentifierUri "https://YourHpcPackAppUri" -CertificateThumbprint "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX" -TenantId xxxxxxxx-xxxxx-xxxxx-xxxxx-xxxxxxxxxxxx
    ```

    où

    **DisplayName** : nom d’affichage de l’application Azure Active. Si l’application hello n’existe pas, il est créé dans Azure Active Directory.

    **Page d’accueil** -hello page d’accueil de l’application hello. Vous pouvez configurer une URL factice, comme dans hello précédent exemple.

    **IdentifierUri** -identificateur de l’application hello. Vous pouvez configurer une URL factice, comme dans hello précédent exemple.

    **CertificateThumbprint** -empreinte numérique du certificat hello installé sur le nœud principal de hello à l’étape 1.

    **TenantId** : ID client de votre Azure Active Directory. Vous pouvez obtenir hello ID client à partir du portail d’Azure Active Directory hello **propriétés** page.

    Pour plus d’informations sur **ConfigARMAutoGrowShrinkCert.ps1**, exécutez `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`.


* **Pour un cluster avec un nœud principal dans Azure (modèle de déploiement classique)** - si vous utilisez un cluster de hello du déploiement script toocreate hello IaaS HPC Pack dans le modèle de déploiement classique de hello, activer hello **AutoGrowShrink** cluster propriété en définissant l’option de AutoGrowShrink hello dans le fichier de configuration de cluster hello. Pour plus d’informations, consultez la documentation hello accompagnant hello [téléchargement du script](https://www.microsoft.com/download/details.aspx?id=44949).

    Vous pouvez également activer hello **AutoGrowShrink** propriété cluster après avoir déployé le cluster de hello à l’aide de PowerShell HPC commandes décrites dans hello suivant la section. tooprepare pour cela, étapes de la première hello complet suivant :

  1. Configurer un certificat de gestion Azure sur le nœud principal de hello et Bonjour abonnement Azure. Pour un déploiement de test, vous pouvez utiliser le certificat auto-signé hello par défaut de Microsoft HPC Azure HPC Pack est installé sur le nœud principal de hello et puis télécharger ce tooyour certificat abonnement Azure. Pour plus d’options et les étapes, consultez hello [Guide de la bibliothèque TechNet](https://technet.microsoft.com/library/gg481759.aspx).

  2. Exécutez **regedit** sur le nœud principal de hello, accédez à tooHKLM\SOFTWARE\Micorsoft\HPC\IaasInfo, puis ajoutez une valeur de chaîne. Définir le nom de la valeur hello trop « Empreinte numérique » et la valeur données toohello empreinte numérique du certificat hello à l’étape 1.

### <a name="hpc-powershell-commands-tooset-hello-autogrowshrink-property"></a>Propriété de HPC PowerShell commands tooset hello AutoGrowShrink
Voici des exemples PowerShell HPC commandes tooset **AutoGrowShrink** et tootune son comportement avec des paramètres supplémentaires. Consultez [AutoGrowShrink paramètres](#AutoGrowShrink-parameters) plus loin dans cet article pour la liste complète des paramètres hello.

toorun ces commandes, démarrez HPC PowerShell sur le nœud principal du cluster hello en tant qu’administrateur.

**tooenable hello AutoGrowShrink propriété**

```powershell
Set-HpcClusterProperty –EnableGrowShrink 1
```

**toodisable hello AutoGrowShrink propriété**

```powershell
Set-HpcClusterProperty –EnableGrowShrink 0
```

**toochange hello augmenter l’intervalle en minutes**

```powershell
Set-HpcClusterProperty –GrowInterval <interval>
```

**toochange hello réduire l’intervalle en minutes**

```powershell
Set-HpcClusterProperty –ShrinkInterval <interval>
```

**configuration actuelle de hello tooview de AutoGrowShrink**

```powershell
Get-HpcClusterProperty –AutoGrowShrink
```

**groupes de nœuds tooexclude de AutoGrowShrink**

```powershell
Set-HpcClusterProperty –ExcludeNodeGroups <group1,group2,group3>
```

>[!NOTE] 
> Ce paramètre est pris en charge dans HPC Pack 2016.
>

### <a name="autogrowshrink-parameters"></a>Paramètres d’AutoGrowShrink
Hello Voici AutoGrowShrink les paramètres que vous pouvez modifier à l’aide de hello **Set-HpcClusterProperty** commande.

* **EnableGrowShrink** - commutateur tooenable ou désactiver hello **AutoGrowShrink** propriété.
* **ParamSweepTasksPerCore** -nombre de balayage paramétrique tâches toogrow un seul cœur. par défaut de Hello est toogrow un cœur de chaque tâche.

  > [!NOTE]
  > Modifications de HPC Pack QFE KB3134307 **ParamSweepTasksPerCore** trop**TasksPerResourceUnit**. Il est basé sur le type de ressource de tâche hello et peut être un nœud socket ou un cœur.
  >
  >
* **GrowThreshold** -seuil de croissance automatique de tootrigger de tâches en file d’attente. par défaut de Hello est 1, ce qui signifie que si 1 ou plusieurs tâches dans hello en file d’attente d’état, d’augmenter automatiquement les nœuds.
* **GrowInterval** -intervalle de croissance automatique de tootrigger minutes. intervalle de salutation par défaut est de 5 minutes.
* **ShrinkInterval** -intervalle en minutes un compactage automatique tootrigger. intervalle de salutation par défaut est de 5 minutes. |
* **ShrinkIdleTimes** -nombre de vérifications continue tooshrink tooindicate hello nœuds est inactif. valeur par défaut Hello est 3 fois. Par exemple, si hello **ShrinkInterval** est de 5 minutes, HPC Pack vérifie si le nœud de hello est inactif à toutes les 5 minutes. Si les nœuds de hello sont en état d’inactivité hello après que 3 continue vérifie (15 minutes), puis HPC Pack réduit ce nœud.
* **ExtraNodesGrowRatio** -pourcentage supplémentaire de toogrow de nœuds pour les travaux de l’Interface MPI (Message Passing). Hello par défaut est 1, ce qui signifie que HPC Pack augmente de 1 % pour les travaux MPI nœuds.
* **GrowByMin** -commutateur tooindicate si la stratégie de croissance automatique de hello est basée sur les ressources minimales hello requis pour la tâche de hello. valeur par défaut Hello est false, ce qui signifie que HPC Pack augmente de nœuds pour les travaux en fonction des ressources de maximale hello requis pour les travaux de hello.
* **SoaJobGrowThreshold** -seuil d’entrant hello SOA demandes tootrigger automatique augmente le processus. valeur par défaut de Hello est 50000.

  > [!NOTE]
  > Ce paramètre est pris en charge dans Microsoft HPC Pack 2012 R2 Update 3.
  >
  >
* **SoaRequestsPerCore** -nombre de SOA entrant demandes toogrow un seul cœur. valeur par défaut de Hello est 20 000.

  > [!NOTE]
  > Ce paramètre est pris en charge dans Microsoft HPC Pack 2012 R2 Update 3.
  >
* **ExcludeNodeGroups** – nœuds Bonjour spécifié les groupes de nœuds ne pas automatiquement augmenter et réduire.
  
  > [!NOTE]
  > Ce paramètre est pris en charge dans HPC Pack 2016.
  >

### <a name="mpi-example"></a>Exemple de MPI
Par défaut HPC Pack augmente de 1 % de nœuds supplémentaires pour des travaux MPI (**ExtraNodesGrowRatio** a la valeur too1). Hello raison est que MPI peut nécessiter plusieurs nœuds, et hello travail peut uniquement exécuté lorsque tous les nœuds sont prêtes. Lorsque Azure démarre les nœuds, parfois un seul nœud peut-être plus toostart de temps que d’autres, à l’origine des autres nœuds toobe inactif en attendant que tooget nœud prêt. En augmentant les nœuds supplémentaires, HPC Pack réduit le temps d’attente de cette ressource et réduit potentiellement les coûts. pourcentage de hello tooincrease des nœuds supplémentaires pour des travaux MPI (par exemple, % too10), exécutez une commande semblable à

    Set-HpcClusterProperty -ExtraNodesGrowRatio 10

### <a name="soa-example"></a>Exemple SOA
Par défaut, **SoaJobGrowThreshold** a la valeur too50000 et **SoaRequestsPerCore** a la valeur too200000. Si vous envoyez un travail SOA avec 70 000 demandes, il y a une tâche en attente et les demandes entrantes sont au nombre de 70 000. Dans ce cas HPC Pack augmente 1 noyau pour hello en file d’attente des tâches et les demandes entrantes, croît (70000-50000) / base 20000 = 1, total augmente de 2 cœurs pour ce travail SOA dans.

## <a name="run-hello-azureautogrowshrinkps1-script"></a>Exécutez le script de AzureAutoGrowShrink.ps1 hello
### <a name="prerequisites"></a>Composants requis

* **HPC Pack 2012 R2 Update 1 ou ultérieure cluster** - hello **AzureAutoGrowShrink.ps1** script est installé dans le dossier hello % CCP_HOME % bin. nœud principal du cluster Hello peut être déployé localement ou dans une machine virtuelle Azure. Consultez [configurer un cluster hybride avec HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) tooget a démarré avec un nœud principal local et les nœuds de « Croissance » Azure. Consultez hello [script de déploiement IaaS de HPC Pack](hpcpack-cluster-powershell-script.md) tooquickly déployer un cluster HPC Pack dans des machines virtuelles Azure, ou utiliser un [modèle de démarrage rapide Azure](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/).
* **Azure PowerShell 1.4.0** -script de hello actuellement dépend de cette version spécifique d’Azure PowerShell.
* **Pour un cluster avec Azure des nœuds de croissance** -exécuter le script de hello sur un ordinateur client où HPC Pack est installé, ou sur le nœud principal de hello. S’exécute sur un ordinateur client, assurez-vous que vous définissez hello $env variable : nœud principal de CCP_SCHEDULER toopoint toohello. nœuds de « Croissance » Azure Hello doivent être ajoutés toohello cluster, mais ils peuvent être hello Not-Deployed l’état.
* **Pour un cluster déployé dans Azure VMs (modèle de déploiement Resource Manager)** -pour un cluster d’ordinateurs virtuels de Azure déployés dans le modèle de déploiement du Gestionnaire de ressources hello, script de hello prend en charge deux méthodes d’authentification Azure : connectez-vous tooyour compte Azure script de hello toorun chaque fois (en exécutant `Login-AzureRmAccount`, ou configurer un tooauthenticate principal de service avec un certificat. HPC Pack fournit le script de hello **ConfigARMAutoGrowShrinkCert.ps** toocreate un principal de service avec le certificat. Hello script crée une application Azure Active Directory (Azure AD) et un principal de service et assigne hello contributeur rôle toohello service principal. script de hello toorun, démarrer Azure PowerShell en tant qu’administrateur et exécutez les hello suivant les commandes :

    ```powershell
    cd $env:CCP_HOME\bin

    Login-AzureRmAccount

    .\ConfigARMAutoGrowShrinkCert.ps1 -DisplayName “YourHpcPackAppName” -HomePage "https://YourHpcPackAppHomePage" -IdentifierUri "https://YourHpcPackAppUri" -PfxFile "d:\yourcertificate.pfx"
    ```

    Pour plus d’informations sur **ConfigARMAutoGrowShrinkCert.ps1**, exécutez `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`.

* **Pour un cluster déployé dans Azure VMs (modèle de déploiement classique)** -exécuter script de hello sur hello nœud principal, car il dépend hello **Start-hpciaasnode.ps1** et **Stop-hpciaasnode.ps1**des scripts qui y sont installés. En outre, ces scripts nécessitent un certificat de gestion Azure ou un fichier de paramètres de publication (consultez [Gérer des nœuds de calcul dans un cluster HPC Pack dans Azure](hpcpack-cluster-node-manage.md)). Vérifiez que hello toutes les machines virtuelles que vous avez besoin de nœud sont déjà ajoutées toohello cluster de calcul. Ils peuvent être hello état arrêté.



### <a name="syntax"></a>Syntaxe
```powershell
AzureAutoGrowShrink.ps1 [-NodeTemplates <String[]>] [-JobTemplates <String[]>] [-NodeType <String>]
    -NumOfActiveQueuedTasksPerNodeToGrow <Single> [-NumOfActiveQueuedTasksToGrowThreshold <Int32>]
    [-NumOfInitialNodesToGrow <Int32>] [-GrowCheckIntervalMins <Int32>] [-ShrinkCheckIntervalMins <Int32>]
    [-ShrinkCheckIdleTimes <Int32>] [-ExtraNodesGrowRatio <Int32>] [-ArgFile <String>] [-LogFilePrefix <String>]
    [<CommonParameters>]

AzureAutoGrowShrink.ps1 [-NodeTemplates <String[]>] [-JobTemplates <String[]>] [-NodeType <String>]
    -NumOfQueuedJobsPerNodeToGrow <Single> [-NumOfQueuedJobsToGrowThreshold <Int32>] [-NumOfInitialNodesToGrow
    <Int32>] [-GrowCheckIntervalMins <Int32>] [-ShrinkCheckIntervalMins <Int32>] [-ShrinkCheckIdleTimes <Int32>]
    [-ExtraNodesGrowRatio <Int32>] [-ArgFile <String>] [-LogFilePrefix <String>] [<CommonParameters>]

AzureAutoGrowShrink.ps1 -UseLastConfigurations [-ArgFile <String>] [-LogFilePrefix <String>] [<CommonParameters>]
```
### <a name="parameters"></a>Paramètres
* **NodeTemplates** -hello nœud Modèles toodefine hello étendue pour hello nœuds toogrow et réduire. Si non spécifié (hello la valeur par défaut est @()), tous les nœuds de hello **AzureNodes** groupe de nœuds sont dans l’étendue lorsque **NodeType** a la valeur AzureNodes et tous les nœuds Bonjour **ComputeNodes** groupe de nœuds sont dans l’étendue lorsque **NodeType** a la valeur ComputeNodes.
* **Les JobTemplates** -noms Hello étendue de hello modèles toodefine pour hello nœuds toogrow de la tâche.
* **NodeType** : hello du type de nœud toogrow et réduire. Les valeurs prises en charge sont les suivantes :

  * **AzureNodes** : pour les nœuds Azure PaaS (extension) dans un cluster IaaS Azure ou local.
  * **ComputeNodes** : pour les machines virtuelles à nœud de calcul uniquement dans un cluster IaaS Azure.

* **NumOfQueuedJobsPerNodeToGrow** -nombre de travaux en file d’attente requis toogrow un seul nœud.
* **NumOfQueuedJobsToGrowThreshold** -nombre de seuil de hello de hello toostart de travaux en file d’attente augmente de processus.
* **NumOfActiveQueuedTasksPerNodeToGrow** -nombre de hello de tâches en file d’attente actives requises toogrow un seul nœud. Si **NumOfQueuedJobsPerNodeToGrow** est spécifié avec une valeur supérieure à 0, ce paramètre est ignoré.
* **NumOfActiveQueuedTasksToGrowThreshold** -nombre de seuil de hello de hello de toostart les tâches actives en file d’attente augmente de processus.
* **NumOfInitialNodesToGrow** - hello initiale du nombre minimal de nœuds toogrow si tous les nœuds hello dans la portée sont **Not-Deployed** ou **arrêté (désalloué)**.
* **GrowCheckIntervalMins** -intervalle hello en minutes entre les vérifications toogrow.
* **ShrinkCheckIntervalMins** -intervalle hello en minutes entre les vérifications tooshrink.
* **ShrinkCheckIdleTimes** -hello du nombre de vérifications de réduction continue (séparés par des **ShrinkCheckIntervalMins**) tooindicate hello nœuds sont inactifs.
* **UseLastConfigurations** -hello configurations précédemment enregistrées dans le fichier d’arguments hello.
* **ArgFile**: hello nom de toosave de fichier utilisé argument hello et mettre à jour hello configurations toorun hello script.
* **Préfixe_du_fichier_journal** -hello préfixe nom du fichier journal de hello. Vous pouvez spécifier un chemin d’accès. Par défaut des journaux de hello sont écrite toohello répertoire de travail actuel.

### <a name="example-1"></a>Exemple 1
Hello exemple suivant configure hello Azure déployés avec le modèle AzureNode par défaut toogrow des nœuds de croissance et la réduction automatique. Si tous les nœuds sont initialement Bonjour **Not-Deployed** d’état, au moins 3 nœuds sont démarrés. Si le nombre de hello de travaux en file d’attente dépasse 8, script de hello démarre les nœuds jusqu'à ce que leur nombre dépasse hello des taux de travaux en file d’attente à **NumOfQueuedJobsPerNodeToGrow**. Si un nœud est toobe inactif à 3 reprises, il est arrêté.

```powershell
.\AzureAutoGrowShrink.ps1 -NodeTemplates @('Default AzureNode
 Template') -NodeType AzureNodes -NumOfQueuedJobsPerNodeToGrow 5
 -NumOfQueuedJobsToGrowThreshold 8 -NumOfInitialNodesToGrow 3
 -GrowCheckIntervalMins 1 -ShrinkCheckIntervalMins 1 -ShrinkCheckIdleTimes 3
```

### <a name="example-2"></a>Exemple 2
Hello exemple suivant configure hello Azure déployés avec hello modèle ComputeNode par défaut toogrow de machines virtuelles de nœud de calcul et la réduction automatique.
travaux Hello configuré par le modèle de projet par défaut hello définir étendue hello de la charge de travail sur le cluster de hello. Si tous les nœuds de hello sont initialement arrêtés, au moins 5 nœuds sont démarré. Si le nombre de hello de tâches en file d’attente actives est supérieur à 15, script de hello démarre les nœuds jusqu'à ce que leur nombre dépasse le taux de hello de tâches en file d’attente actives trop**NumOfActiveQueuedTasksPerNodeToGrow**. Si un nœud est toobe inactif à 10 reprises, il est arrêté.

```powershell
.\AzureAutoGrowShrink.ps1 -NodeTemplates 'Default ComputeNode Template' -JobTemplates 'Default' -NodeType ComputeNodes -NumOfActiveQueuedTasksPerNodeToGrow 10 -NumOfActiveQueuedTasksToGrowThreshold 15 -NumOfInitialNodesToGrow 5 -GrowCheckIntervalMins 1 -ShrinkCheckIntervalMins 1 -ShrinkCheckIdleTimes 10 -ArgFile 'IaaSVMComputeNodes_Arg.xml' -LogFilePrefix 'IaaSVMComputeNodes_log'
```
