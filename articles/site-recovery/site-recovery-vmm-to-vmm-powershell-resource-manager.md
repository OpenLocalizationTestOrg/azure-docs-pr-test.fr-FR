---
title: aaaReplicate site secondaire de VMM tooa machines virtuelles Hyper-V avec PowerShell (Azure Resource Manager) | Documents Microsoft
description: "Décrit comment la réplication tooorchestrate toodeploy Azure Site Recovery, le basculement et récupération des ordinateurs virtuels Hyper-V dans VMM nuages tooa site VMM secondaire à l’aide de PowerShell (Resource Manager)."
services: site-recovery
documentationcenter: 
author: sujaytalasila
manager: rochakm
editor: raynew
ms.assetid: 9d38e9c3-217c-4e44-830c-575e9a4141f2
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: sutalasi
ms.openlocfilehash: a769dcc68d66c18b9dc47539071f4d0e0f1db70f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooa-secondary-vmm-site-using-powershell-resource-manager"></a>Réplication d’ordinateurs virtuels Hyper-V dans VMM clouds tooa secondaire de site VMM à l’aide de PowerShell (Resource Manager).
> [!div class="op_single_selector"]
> * [portail Azure](site-recovery-vmm-to-vmm.md)
> * [Portail Classic](site-recovery-vmm-to-vmm-classic.md)
> * [PowerShell - Resource Manager](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

Récupération de Site de tooAzure Bienvenue ! Utilisez cet article si vous souhaitez tooreplicate virtuels Hyper-V gérés dans le site secondaire de System Center Virtual Machine Manager (VMM) clouds tooa sur site.

Cet article explique comment les tâches courantes toouse PowerShell tooautomate vous devez tooperform lorsque vous configurez des ordinateurs virtuels de Azure Site Recovery tooreplicate Hyper-V dans les clouds de System Center VMM clouds tooSystem Center VMM dans le site secondaire.

article de Hello inclut les conditions préalables requises pour le scénario de hello et vous montre

* Comment tooset d’un coffre Recovery Services
* Installer hello fournisseur Azure Site Recovery sur le serveur VMM de hello source et de serveur VMM de hello cible
* Enregistrer l’ou les serveurs VMM hello dans le coffre de hello
* Configurer la stratégie de réplication pour hello Cloud VMM. les paramètres de réplication Hello dans la stratégie de hello sera appliqué tooall protégé par les ordinateurs virtuels
* Activer la protection des machines virtuelles de hello.
* Test de basculement des machines virtuelles hello individuellement ou dans le cadre d’une récupération de plan toomake que tout fonctionne comme prévu.
* Effectuer planifié ou un basculement non planifié d’ordinateurs virtuels, individuellement ou dans le cadre d’un toomake de plan de récupération que tout fonctionne comme prévu.

Si vous rencontrez des problèmes de configuration de ce scénario, publiez vos questions sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

> [!NOTE]
> Azure dispose de deux [modèles de déploiement](../azure-resource-manager/resource-manager-deployment-model.md) différents pour créer et utiliser des ressources : le déploiement Azure Resource Manager et le déploiement classique. Azure a également deux portails : hello portail classique Azure qui prend en charge le modèle de déploiement classique hello et hello portail Azure avec prise en charge pour les deux modèles de déploiement. Cet article décrit le modèle de déploiement du Gestionnaire de ressources hello.
>
>

## <a name="on-premises-prerequisites"></a>Conditions préalables locales
Voici ce que vous aurez besoin dans hello principal et secondaire local sites toodeploy ce scénario :

| **Configuration requise** | **Détails** |
| --- | --- |
| **VMM** |Nous vous recommandons de que déployer un serveur VMM dans le site principal de hello et un serveur VMM dans le site secondaire de hello.<br/><br/> Vous pouvez également effectuer la [réplication entre des clouds sur un seul serveur VMM](site-recovery-vmm-to-vmm.md#prepare-for-single-server-deployment). toodo cela, vous devez au moins deux clouds configurés sur le serveur VMM de hello.<br/><br/> Serveurs VMM doivent exécuter au moins System Center 2012 SP1 avec les dernières mises à jour de hello.<br/><br/> Chaque serveur VMM doit avoir à un ou plusieurs clouds configurés et tous les clouds doivent avoir le profil de capacité de Hyper-V hello définie. <br/><br/>Les clouds doivent contenir un ou plusieurs groupes hôtes VMM.<br/><br/>En savoir plus sur la configuration des clouds VMM dans [l’infrastructure de cloud computing configuration hello VMM](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric), et [procédure pas à pas : création de clouds privés avec System Center 2012 SP1 VMM](http://blogs.technet.com/b/keithmayer/archive/2013/04/18/walkthrough-creating-private-clouds-with-system-center-2012-sp1-virtual-machine-manager-build-your-private-cloud-in-a-month.aspx).<br/><br/> Les serveurs VMM doivent avoir accès à Internet. |
| **Hyper-V** |Serveurs Hyper-V doivent être en cours d’exécution au moins Windows Server 2012 avec un rôle de hello Hyper-V et avez hello les dernières mises à jour installées.<br/><br/> Un serveur Hyper-V doit contenir au moins une machine virtuelle.<br/><br/>  Les serveurs hôte Hyper-V doivent se trouver dans des groupes hôtes dans des clouds VMM principaux et secondaires hello.<br/><br/> Si vous exécutez Hyper-V dans un cluster Windows Server 2012 R2, vous devez installer la [mise à jour 2961977](https://support.microsoft.com/kb/2961977).<br/><br/> Si vous exécutez Hyper-V dans un cluster sous Windows Server 2012, notez que le répartiteur de clusters n’est pas créé automatiquement si vous avez un cluster avec adresses IP statiques. Vous devez manuellement service broker de cluster tooconfigure hello. [En savoir plus](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx). |
| **Fournisseur** |Au cours du déploiement de Site Recovery vous installez hello fournisseur Azure Site Recovery sur les serveurs VMM. Hello fournisseur communique avec Site Recovery via HTTPS 443 tooorchestrate réplication. Réplication de données se produit entre des serveurs de Hyper-V des principaux et secondaires hello sur hello LAN ou une connexion VPN.<br/><br/> Hello fournisseur qui s’exécute sur le serveur VMM de hello doit accéder aux URL de toothese : *. hypervrecoverymanager.windowsazure.com ; *. accesscontrol.windows.net ; *. backup.windowsazure.com ; *. blob.core.windows.net ; *. store.core.windows.net.<br/><br/> En outre autoriser la communication de pare-feu de hello VMM serveurs toohello [plages d’adresses IP de centre de données Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653) et autoriser le protocole HTTPS (443) de hello. |

### <a name="network-mapping-prerequisites"></a>Conditions préalables liées au mappage réseau
Mappages de mappage réseau entre réseaux VM de VMM sur les serveurs VMM des principaux et secondaires hello pour :

* Optimiser le positionnement des machines virtuelles de réplication sur les hôtes Hyper-V secondaires après le basculement.
* Connecter des réseaux d’ordinateurs virtuels tooappropriate réplica machines virtuelles.
* Si vous ne configurez pas réseau mappage réplica machines virtuelles ne seront connecté tooany réseau après le basculement.
* Si vous souhaitez tooset réseau mappage lors de la récupération de Site déploiement ici est que vous devez :

  * Assurez-vous que les ordinateurs virtuels sur la source de hello serveur hôte Hyper-V sont connecté tooa réseau de VMM VM. Ce réseau doit être lié tooa réseau logique associé au cloud de hello.
  * Vérifiez qu’un réseau de machines virtuelles correspondant configuré cloud hello secondaire que vous allez utiliser pour la récupération. Ce réseau d’ordinateurs virtuels doit être lié tooa réseau logique associé avec le cloud secondaire de hello.

En savoir plus sur la configuration des réseaux VMM Bonjour articles suivants

* [Comment tooconfigure les réseaux logiques dans VMM](http://go.microsoft.com/fwlink/p/?LinkId=386307)
* [Comment tooconfigure VM réseaux et passerelles dans VMM](http://go.microsoft.com/fwlink/p/?LinkId=386308)

[Découvrez plus d’informations](site-recovery-vmm-to-vmm.md#prepare-for-network-mapping) sur le fonctionnement du mappage réseau.

### <a name="powershell-prerequisites"></a>Conditions préalables pour PowerShell
Assurez-vous que vous avez toogo prêt d’Azure PowerShell. Si vous utilisez déjà PowerShell, vous devez tooupgrade tooversion 0.8.10 ou version ultérieure. Pour plus d’informations sur la configuration de PowerShell, consultez hello [Guide tooinstall et configurer Azure PowerShell](/powershell/azureps-cmdlets-docs). Après avoir configuré et configuré de PowerShell, vous pouvez afficher toutes les hello des applets de commande disponibles pour le service de hello [ici](/powershell/azure/overview).

toolearn sur les conseils qui peuvent vous aider à utiliser des applets de commande hello, telles que la façon dont les valeurs de paramètre, les entrées et sorties sont généralement gérées dans Azure PowerShell, consultez hello [Guide tooget démarré avec les applets de commande Azure](/powershell/azure/get-started-azureps).

## <a name="step-1-set-hello-subscription"></a>Étape 1 : Définir l’abonnement de hello
1. À partir de Azure powershell, connexion tooyour compte Azure : à l’aide de hello suivant d’applets de commande

        $UserName = "<user@live.com>"
        $Password = "<password>"
        $SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
        $Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $SecurePassword
        Login-AzureRmAccount #-Credential $Cred
2. Obtenez la liste de vos abonnements. Cela affiche également la liste hello abonnement pour chacun des abonnements de hello. Notez le subscriptionID hello d’abonnement hello dans lesquels vous souhaitez toocreate hello coffre recovery services    

        Get-AzureRmSubscription
3. Définir l’abonnement hello dans le hello coffre recovery services est toobe créé en mentionnant l’ID d’abonnement hello

        Set-AzureRmContext –SubscriptionID <subscriptionId>

## <a name="step-2-create-a-recovery-services-vault"></a>Étape 2 : Création du coffre Recovery Services
1. Création d’un groupe de ressources Azure Resource Manager, si ce n’est déjà fait

        New-AzureRmResourceGroup -Name #ResourceGroupName -Location #location
2. Créer un coffre Recovery Services et enregistrer hello créé l’objet de coffre de récupération automatique du système dans une variable (sera utilisée ultérieurement). Vous pouvez également récupérer hello ASR coffre après la création d’objets à l’aide d’applet de commande Get-AzureRMRecoveryServicesVault de hello :-

        $vault = New-AzureRmRecoveryServicesVault -Name #vaultname -ResouceGroupName #ResourceGroupName -Location #location

## <a name="step-3-set-hello-recovery-services-vault-context"></a>Étape 3 : Définir le contexte du coffre Recovery Services hello
1. Si vous avez déjà créé un coffre de sauvegarde, exécutez hello ci-dessous coffre de commande tooget hello.

       $vault = Get-AzureRmRecoveryServicesVault -Name #vaultname
2. Définir le contexte de coffre de hello en exécutant hello commande ci-dessous.

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-install-hello-azure-site-recovery-provider"></a>Étape 4 : Installer hello fournisseur Azure Site Recovery
1. Sur l’ordinateur VMM hello, créez un répertoire en exécutant hello de commande suivante :

       New-Item c:\ASR -type directory
2. Extrayez les fichiers hello à l’aide de fournisseur de hello téléchargé en exécutant hello commande suivante

       pushd C:\ASR\
       .\AzureSiteRecoveryProvider.exe /x:. /q
3. Installez le fournisseur hello hello suivant les commandes à l’aide de :

       .\SetupDr.exe /i
       $installationRegPath = "hklm:\software\Microsoft\Microsoft System Center Virtual Machine Manager Server\DRAdapter"
       do
       {
         $isNotInstalled = $true;
         if(Test-Path $installationRegPath)
         {
           $isNotInstalled = $false;
         }
       }While($isNotInstalled)

   Attendez que hello installation toofinish.
4. Inscrire un serveur hello dans le coffre de hello à l’aide de hello de commande suivante :

       $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
       pushd $BinPath
       $encryptionFilePath = "C:\temp\".\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

## <a name="step-5-create-and-associate-a-replication-policy"></a>Étape 5 : Créer et associer une stratégie de réplication
1. Créer une stratégie de réplication Hyper-V 2012 R2 en exécutant hello de commande suivante :

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $RepProvider = HyperVReplica2012R2
        $Recoverypoints = 24                    #specify hello number of hours tooretain recovery pints
        $AppConsistentSnapshotFrequency = 4 #specify hello frequency (in hours) at which app consistent snapshots are taken
        $AuthMode = "Kerberos"  #options are "Kerberos" or "Certificate"
        $AuthPort = "8083"  #specify hello port number that will be used for replication traffic on Hyper-V hosts
        $InitialRepMethod = "Online" #options are "Online" or "Offline"

        $policyresult = New-AzureRmSiteRecoveryPolicy -Name $policyname -ReplicationProvider $RepProvider -ReplicationFrequencyInSeconds $Replicationfrequencyinseconds -RecoveryPoints $recoverypoints -ApplicationConsistentSnapshotFrequencyInHours $AppConsistentSnapshotFrequency -Authentication $AuthMode -ReplicationPort $AuthPort -ReplicationMethod $InitialRepMethod

    > [!NOTE]
    > Hello cloud VMM peut contenir des hôtes Hyper-V qui exécutent différentes versions de Windows Server (comme indiqué dans les conditions préalables de hello Hyper-V), mais la stratégie de réplication hello est spécifique à la version du système d’exploitation. Si vos hôtes exécutent des versions de système d’exploitation différentes, créez des stratégies de réplication spécifiques à chaque version du système d’exploitation. Par exemple : si vous avez cinq hôtes exécutant Windows Servers 2012 et trois hôtes exécutant Windows Server 2012 R2, créez deux stratégies de réplication : une pour chaque version du système d’exploitation.

1. Obtenir le conteneur de protection principale hello (Cloud VMM principal) et le conteneur de protection de récupération (recovery Cloud VMM) en exécutant hello suivant les commandes :

       $PrimaryCloud = "testprimarycloud"
       $primaryprotectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloud;  

       $RecoveryCloud = "testrecoverycloud"
       $recoveryprotectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $RecoveryCloud;  
2. Récupérer la stratégie hello créé à l’étape 1 à l’aide de nom convivial de hello de stratégie de hello

       $policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $policyname
3. Démarrer l’association hello du conteneur de protection hello (Cloud VMM) avec la stratégie de réplication hello :

       $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy     $Policy -PrimaryProtectionContainer $primaryprotectionContainer -RecoveryProtectionContainer $recoveryprotectionContainer
4. Attendez que hello stratégie association tâche toocomplete. Vous pouvez vérifier si hello est terminée à l’aide de hello suivant extrait de code PowerShell.

       $job = Get-AzureRmSiteRecoveryJob -Job $associationJob

       if($job -eq $null -or $job.StateDescription -ne "Completed")
       {
         $isJobLeftForProcessing = $true;
       }

   Une fois le travail de hello a terminé le traitement, exécutez hello de commande suivante :

       if($isJobLeftForProcessing)
       {
         Start-Sleep -Seconds 60
       }
       }While($isJobLeftForProcessing)

achèvement de hello toocheck d’opération de hello, suivez les étapes de hello dans [surveiller l’activité](#monitor).

## <a name="step-6-configure-network-mapping"></a>Étape 6 : Configuration du mappage réseau
1. Hello première commande Obtient les serveurs pour le coffre Azure Site Recovery en cours hello. commande Hello stocke les serveurs Microsoft Azure Site Recovery hello dans la variable de tableau hello $Servers.

        $Servers = Get-AzureRmSiteRecoveryServer
2. Hello ci-dessous commandes obtenir réseau de récupération de site hello pour les serveurs VMM de source hello et hello cible VMM.

        $PrimaryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[0]        

        $RecoveryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[1]

    > [!NOTE]
    > serveur VMM de Hello source peut être hello premier ou un tableau de serveurs hello deuxième hello en un seul. Vérifier les noms hello hello de serveurs de VMM et obtenir des réseaux de hello correctement


1. applet de commande finale Hello crée un mappage entre le réseau principal de hello et récupération hello. applet de commande Hello Spécifie le réseau principal de hello en tant que premier élément de hello du réseau de récupération $PrimaryNetworks et hello en tant que premier élément de hello de $RecoveryNetworks.

        New-AzureRmSiteRecoveryNetworkMapping -PrimaryNetwork $PrimaryNetworks[0] -RecoveryNetwork $RecoveryNetworks[0]

## <a name="step-7-configure-storage-mapping"></a>Étape 7 : Configuration du mappage de stockage
1. Hello commande ci-dessous obtient la liste hello des classifications de stockage dans $storageclassifications variable.

        $storageclassifications = Get-AzureRmSiteRecoveryStorageClassification
2. Hello ci-dessous commandes obtenir la classification de source de hello dans $SourceClassificaion variable et classification cible dans $TargetClassification variable.

        $SourceClassificaion = $storageclassifications[0]

        $TargetClassification = $storageclassifications[1]

    > [!NOTE]
    > les classifications source et cible Hello peuvent être n’importe quel élément dans le tableau de hello. Consultez la sortie toohello Hello ci-dessous index hello toofigure des commandes de classifications source et cible dans le tableau de $storageclassifications.

    > Get-AzureRmSiteRecoveryStorageClassification | Select-Object -Property FriendlyName, Id | Format-Table


1. Hello ci-dessous l’applet de commande crée un mappage entre la classification de source de hello et classification de cible hello.

        New-AzureRmSiteRecoveryStorageClassificationMapping -PrimaryStorageClassification $SourceClassificaion -RecoveryStorageClassification $TargetClassification

## <a name="step-8-enable-protection-for-virtual-machines"></a>Étape 8 : Activation de la protection des machines virtuelles
Une fois que les réseaux, les clouds et les serveurs de hello sont correctement configurés, vous pouvez activer la protection des machines virtuelles dans le cloud de hello.

1. protection de tooenable, exécutez hello suivant du conteneur de protection de commande tooget hello :

          $PrimaryProtectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloudName
2. Obtenir l’entité de protection hello (VM) en exécutant hello de commande suivante :

           $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -friendlyName $VMName -ProtectionContainer $PrimaryProtectionContainer
3. Activer la réplication pour hello machine virtuelle en exécutant hello de commande suivante :

          $jobResult = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionentity -Protection Enable -Policy $policy

## <a name="test-your-deployment"></a>Tester votre déploiement
planification de votre déploiement, vous pouvez exécuter un test de basculement pour une seule machine virtuelle, ou créer un plan de récupération composé de plusieurs ordinateurs virtuels et exécuter un test de basculement pour hello tootest. Il simule votre mécanisme de basculement et de récupération dans un réseau isolé.

> [!NOTE]
> Vous pouvez créer un plan de récupération pour votre application dans le portail Azure.
>
>

achèvement de hello toocheck d’opération de hello, suivez les étapes de hello dans [surveiller l’activité](#monitor).

### <a name="run-a-test-failover"></a>Exécution d’un test de basculement
1. Exécutez hello ci-dessous applets de commande tooget hello VM réseau toowhich que vous voulez utiliser le basculement de tootest vos machines virtuelles.

       $Servers = Get-AzureRmSiteRecoveryServer
       $RecoveryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[1]
2. Effectuer un test de basculement d’un ordinateur virtuel de manière hello suivante :

       $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -FriendlyName $VMName -ProtectionContainer $PrimaryprotectionContainer

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -VMNetwork $RecoveryNetworks[1]
3. Effectuer un test de basculement d’un plan de récupération de manière hello suivante :

       $recoveryplanname = "test-recovery-plan"

       $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -Recoveryplan $recoveryplan -VMNetwork $RecoveryNetworks[1]

### <a name="run-a-planned-failover"></a>Exécuter un basculement planifié
1. Effectuer un basculement planifié d’un ordinateur virtuel de manière hello suivante :

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $PrimaryprotectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity
2. Effectuer un basculement planifié d’un plan de récupération de manière hello suivante :

        $recoveryplanname = "test-recovery-plan"

        $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -Recoveryplan $recoveryplan

### <a name="run-an-unplanned-failover"></a>Exécuter un basculement non planifié
1. Effectuer un basculement non planifié d’un ordinateur virtuel de manière hello suivante :

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $PrimaryprotectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity

2. effectuez un basculement non planifié d’un plan de récupération de manière hello suivante :

        $recoveryplanname = "test-recovery-plan"

        $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity

## <a name=monitor></a> Suivi de l'activité
Utilisez hello suivant l’activité de commandes toomonitor hello. Notez que vous avez toowait entre les travaux pour hello traitement toofinish.

    Do
    {
        $job = Get-AzureSiteRecoveryJob -Id $associationJob.JobId;
        Write-Host "Job State:{0}, StateDescription:{1}" -f Job.State, $job.StateDescription;
        if($job -eq $null -or $job.StateDescription -ne "Completed")
        {
            $isJobLeftForProcessing = $true;
        }

    if($isJobLeftForProcessing)
        {
            Start-Sleep -Seconds 60
        }
    }While($isJobLeftForProcessing)



## <a name="next-steps"></a>Étapes suivantes
[En savoir plus](/powershell/module/azurerm.recoveryservices.backup/#recovery) sur Azure Site Recovery avec les applets de commande PowerShell Azure Resource Manager.
