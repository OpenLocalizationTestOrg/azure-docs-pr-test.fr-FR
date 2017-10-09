---
title: "machines virtuelles d’aaaReplicate Hyper-V dans les clouds VMM à l’aide d’Azure Site Recovery et PowerShell (Resource Manager) | Documents Microsoft"
description: "Réplication de machines virtuelles Hyper-V dans des clouds VMM à l'aide d'Azure Site Recovery et PowerShell"
services: site-recovery
documentationcenter: 
author: Rajani-Janaki-Ram
manager: rochakm
editor: raynew
ms.assetid: 6ac509ad-5024-43d8-b621-d8fec019b9a9
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: rajanaki
ms.openlocfilehash: b0f641de4e10a600ead415ceb9bd488fb4d1659d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooazure-using-powershell-and-azure-resource-manager"></a>Réplication d’ordinateurs virtuels Hyper-V dans VMM tooAzure de nuages à l’aide de PowerShell et le Gestionnaire de ressources Azure
> [!div class="op_single_selector"]
> * [portail Azure](site-recovery-vmm-to-azure.md)
> * [PowerShell - Resource Manager](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [Portail Classic](site-recovery-vmm-to-azure-classic.md)
> * [PowerShell - Classique](site-recovery-deploy-with-powershell.md)
>
>

## <a name="overview"></a>Vue d'ensemble
Azure Site Recovery contribue stratégie récupération tooyour commerciale la continuité des activités et d’urgence en coordonnant la réplication, le basculement et récupération des machines virtuelles dans un nombre de scénarios de déploiement. Pour obtenir la liste complète de déploiement de scénarios consultez hello [vue d’ensemble d’Azure Site Recovery](site-recovery-overview.md).

Cet article explique comment les tâches courantes toouse PowerShell tooautomate vous devez tooperform lorsque vous configurez Azure Site Recovery tooreplicate Hyper-V virtual machines dans le stockage de System Center VMM clouds tooAzure.

article de Hello inclut les conditions préalables requises pour le scénario de hello et vous montre

* Comment tooset d’un coffre Recovery Services
* Installer hello fournisseur Azure Site Recovery sur le serveur VMM de hello source
* Inscrire le serveur de hello dans le coffre de hello, ajoutez un compte de stockage Azure
* Installer l’agent de hello Azure Recovery Services sur les serveurs hôtes Hyper-V
* Configurer les paramètres de protection pour les clouds VMM, qui seront appliqués tooall protégé par les ordinateurs virtuels
* Activation de la protection de ces machines virtuelles
* Test hello toomake de basculement que tout fonctionne comme prévu.

Si vous rencontrez des problèmes de configuration de ce scénario, publiez vos questions sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

> [!NOTE]
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../azure-resource-manager/resource-manager-deployment-model.md). Cet article décrit à l’aide du modèle de déploiement du Gestionnaire de ressources hello.
>
>

## <a name="before-you-start"></a>Avant de commencer
Assurez-vous que les conditions préalables sont remplies :

### <a name="azure-prerequisites"></a>Conditions préalables pour Azure
* Vous aurez besoin d’un compte [Microsoft Azure](https://azure.microsoft.com/) . Si vous n’en avez pas, commencez avec un [compte gratuit](https://azure.microsoft.com/free). En outre, vous pouvez lire sur hello [tarification d’Azure Site Recovery Manager](https://azure.microsoft.com/pricing/details/site-recovery/).
* Vous devez un abonnement du fournisseur de services cryptographiques si vous essayez du scénario abonnement CSP hello réplication tooa. En savoir plus sur le programme du fournisseur de services cryptographiques hello dans [comment tooenroll dans le programme du fournisseur de services cryptographiques hello](https://msdn.microsoft.com/library/partnercenter/mt156995.aspx).
* Vous aurez besoin d’un tooAzure données répliquées toostore de compte de stockage (Resource Manager) v2 Azure. compte de Hello doit géo-réplication activée. Il doit être en hello même région que hello service Azure Site Recovery et être associé à hello même abonnement ou hello CSP. toolearn en savoir plus sur la configuration de stockage Azure, consultez hello [Introduction tooMicrosoft Azure Storage](../storage/common/storage-introduction.md) pour référence.
* Vous devez toomake que que machines virtuelles tooprotect conformes hello [conditions préalables de machine virtuelle Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).

> [!NOTE]
> Actuellement, seules les opérations au niveau de la machine virtuelle sont possibles par le biais de Powershell. La prise en charge des opérations au niveau du plan de récupération sera bientôt disponible.  Pour l’instant, vous êtes limité tooperforming basculements seulement à un niveau de granularité 'protected VM' et pas à un niveau d’un Plan de récupération.
>
>

### <a name="vmm-prerequisites"></a>Configuration requise pour VMM
* Vous aurez besoin d'un serveur VMM exécuté sur System Center 2012 R2.
* N’importe quel serveur VMM contenant des machines virtuelles que vous souhaitiez tooprotect doit être en cours d’exécution hello fournisseur Azure Site Recovery. Il est installé pendant hello déploiement d’Azure Site Recovery.
* Vous devez au moins un cloud sur hello serveur VMM que vous souhaitez tooprotect. cloud de Hello doit contenir :
  * un ou plusieurs groupes hôtes VMM ;
  * un ou plusieurs serveurs hôtes Hyper-V ou clusters dans chaque groupe hôte.
  * Un ou plusieurs ordinateurs virtuels sur le serveur d’Hyper-V source hello.
* Pour en savoir plus sur la configuration des clouds VMM :
  * En savoir plus sur des clouds privés VMM dans [Nouveautés dans le Cloud privé avec System Center 2012 R2 VMM](http://go.microsoft.com/fwlink/?LinkId=324952) et dans [clouds VMM 2012 et hello](http://go.microsoft.com/fwlink/?LinkId=324956).
  * En savoir plus sur [configuration hello VMM de l’infrastructure cloud](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric)
  * Une fois vos éléments d’infrastructure cloud en place, apprenez à créer des clouds privés dans [Création d’un cloud privé dans VMM](http://go.microsoft.com/fwlink/p/?LinkId=324953) et [Procédure pas à pas : Création de clouds privés avec System Center 2012 SP1 VMM](http://go.microsoft.com/fwlink/p/?LinkId=324954).

### <a name="hyper-v-prerequisites"></a>Conditions préalables liées à Hyper-V
* Hello serveurs hôtes Hyper-V doivent être en cours d’exécution au moins **Windows Server 2012** avec le rôle Hyper-V ou **Microsoft Hyper-V Server 2012** et avez hello les dernières mises à jour installées.
* Si vous utilisez Hyper-V dans un cluster, notez que le service Broker du cluster n'est pas créé automatiquement si vous avez un cluster basé sur des adresses IP statiques. Vous devez manuellement service broker de cluster tooconfigure hello. Concernant l'option
* Pour obtenir des instructions, consultez [comment tooConfigure Service Broker de réplication Hyper-V](http://blogs.technet.com/b/haroldwong/archive/2013/03/27/server-virtualization-series-hyper-v-replica-broker-explained-part-15-of-20-by-yung-chou.aspx).
* N’importe quel serveur hôte Hyper-V ou le cluster dont vous voulez toomanage protection doit être inclus dans un cloud VMM.

### <a name="network-mapping-prerequisites"></a>Conditions préalables liées au mappage réseau
Lorsque vous protégez des machines virtuelles dans Azure, le mappage réseau hello mappe les réseaux d’ordinateurs virtuels hello sur serveur VMM de source hello et suivant de hello de tooenable de réseaux Azure cible :

* Toutes les machines qui basculent sur hello même réseau peut se connecter tooeach autre, quel que soit le plan de récupération auquel elles sont dans.
* Si une passerelle de réseau est configurée sur le réseau Azure cible de hello, les machines virtuelles peuvent se connecter tooother locaux virtuels.
* Si vous ne configurez pas le mappage réseau, uniquement hello des machines virtuelles qui basculent Bonjour même plan de récupération sera en mesure de tooconnect tooeach autres après basculement tooAzure.

Si vous souhaitez que le mappage réseau toodeploy, vous devez suivant de hello :

* Hello machines virtuelles tooprotect sur le serveur VMM de hello source doit être connecté tooa réseau d’ordinateurs virtuels. Ce réseau doit être lié tooa réseau logique associé au cloud de hello.
* Un réseau de Azure toowhich répliquée d’ordinateurs virtuels peuvent se connecter après le basculement. Vous devez sélectionner ce réseau au moment de hello de basculement. réseau de Hello doivent se trouver dans hello même région que votre abonnement Azure Site Recovery.

Pour en savoir plus sur le mappage réseau, consultez :

* [Comment tooconfigure les réseaux logiques dans VMM](http://go.microsoft.com/fwlink/p/?LinkId=386307)
* [Comment tooconfigure VM réseaux et passerelles dans VMM](http://go.microsoft.com/fwlink/p/?LinkId=386308)
* [Comment tooconfigure et analyse des réseaux virtuels dans Azure](https://azure.microsoft.com/documentation/services/virtual-network/)

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
1. Création d’un groupe de ressources dans Azure Resource Manager, si ce n’est déjà fait

        New-AzureRmResourceGroup -Name #ResourceGroupName -Location #location
2. Créer un coffre Recovery Services et enregistrer hello créé l’objet de coffre de récupération automatique du système dans une variable (sera utilisée ultérieurement). Vous pouvez également récupérer hello ASR coffre après la création d’objets à l’aide d’applet de commande Get-AzureRMRecoveryServicesVault de hello :-

        $vault = New-AzureRmRecoveryServicesVault -Name #vaultname -ResouceGroupName #ResourceGroupName -Location #location

## <a name="step-3-set-hello-recovery-services-vault-context"></a>Étape 3 : Définir le contexte du coffre Recovery Services hello

Définir le contexte de coffre de hello en exécutant hello commande ci-dessous.

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

## <a name="step-5-create-an-azure-storage-account"></a>Étape 5 : Création d’un compte de stockage Azure

Si vous n’avez pas un compte de stockage Azure, créez un compte de géo-réplication activée Bonjour même emplacement que le hello coffre en exécutant hello de commande suivante :

        $StorageAccountName = "teststorageacc1"    #StorageAccountname
        $StorageAccountGeo  = "Southeast Asia"     
        $ResourceGroupName =  “myRG”             #ResourceGroupName
        $RecoveryStorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageAccountName -Type “StandardGRS” -Location $StorageAccountGeo

Notez que le compte de stockage hello doit être en hello même région que le service d’Azure Site Recovery hello et être associé à hello même abonnement.

## <a name="step-6-install-hello-azure-recovery-services-agent"></a>Étape 6 : Installer hello Azure Recovery Services Agent
1. Télécharger l’agent Azure Recovery Services hello [http://aka.ms/latestmarsagent](http://aka.ms/latestmarsagent) et installer sur chaque serveur hôte de Hyper-V situé dans hello VMM clouds que vous souhaitez tooprotect.
2. Exécutez hello commande suivante sur tous les hôtes VMM :

       marsagentinstaller.exe /q /nu

## <a name="step-7-configure-cloud-protection-settings"></a>Étape 7 : Configuration des paramètres de protection de cloud
1. Créer un tooAzure de stratégie de réplication en exécutant hello de commande suivante :

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $Recoverypoints = 6                    #specify hello number of recovery points

        $policryresult = New-AzureRmSiteRecoveryPolicy -Name $policyname -ReplicationProvider HyperVReplicaAzure -ReplicationFrequencyInSeconds $replicationfrequencyinseconds -RecoveryPoints $recoverypoints -ApplicationConsistentSnapshotFrequencyInHours 1 -RecoveryAzureStorageAccountId "/subscriptions/q1345667/resourceGroups/test/providers/Microsoft.Storage/storageAccounts/teststorageacc1"

1. Pour obtenir un conteneur de protection, hello suivant les commandes en cours d’exécution :

       $PrimaryCloud = "testcloud"
       $protectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloud;  
2. Obtenir la variable tooa détails hello de stratégie à l’aide de la tâche hello qui a été créé et mentionner le nom de la stratégie convivial hello :

       $policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $policyname
3. Démarrer l’association hello du conteneur de protection hello avec la stratégie de réplication hello :

       $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy     $Policy -PrimaryProtectionContainer $protectionContainer  
4. Une fois le travail de hello terminée, exécutez hello de commande suivante :

       $job = Get-AzureRmSiteRecoveryJob -Job $associationJob

       if($job -eq $null -or $job.StateDescription -ne "Completed")
       {
         $isJobLeftForProcessing = $true;
       }
5. Une fois le travail de hello a terminé le traitement, exécutez hello de commande suivante :

       if($isJobLeftForProcessing)
       {
         Start-Sleep -Seconds 60
       }
       }While($isJobLeftForProcessing)

achèvement de hello toocheck d’opération de hello, suivez les étapes de hello dans [surveiller l’activité](#monitor).

## <a name="step-8-configure-network-mapping"></a>Étape 8 : Configuration du mappage réseau
Avant de commencer le mappage réseau Vérifiez que les ordinateurs virtuels sur le serveur VMM de hello source sont connectés tooa réseau d’ordinateurs virtuels. En outre, vous devez créer un ou plusieurs réseaux virtuels Azure.

En savoir plus sur toocreate un virtuel réseau à l’aide d’Azure Resource Manager et PowerShell dans [créer un réseau virtuel avec une connexion VPN de site à site à l’aide du Gestionnaire de ressources Azure et PowerShell](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)

Notez que plusieurs réseaux d’ordinateurs virtuels peuvent être mappés tooa réseau Azure unique. Si le réseau cible de hello possède plusieurs sous-réseaux et d’un de ces sous-réseaux a hello trouve du même nom que le sous-réseau sur lequel hello source virtual machine, puis hello ordinateur virtuel sera connecté toothat cible sous-réseau après le basculement. S’il n’existe aucun sous-réseau cible avec un nom correspondant, ordinateur virtuel de hello sera connecté toohello premier sous-réseau de réseau de hello.

1. Hello première commande Obtient les serveurs pour le coffre Azure Site Recovery en cours hello. commande Hello stocke les serveurs Microsoft Azure Site Recovery hello dans la variable de tableau hello $Servers.

        $Servers = Get-AzureRmSiteRecoveryServer
2. commande deuxième Hello obtient réseau de récupération de site hello pour le premier serveur de hello hello $Servers tableau. commande Hello stocke des réseaux de hello dans la variable de hello $Networks.

        $Networks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[0]

1. Hello troisième commande récupère les réseaux virtuels Azure et ensuite cette valeur dans la variable de hello $AzureVmNetworks.

        $AzureVmNetworks =  Get-AzureRmVirtualNetwork
2. applet de commande finale Hello crée un mappage entre le réseau principal de hello et réseau de machine virtuelle Azure hello. applet de commande Hello Spécifie le réseau principal de hello en tant que premier élément de hello de $Networks. applet de commande Hello spécifie un réseau d’ordinateurs virtuels en tant que premier élément de hello de $AzureVmNetworks.

        New-AzureRmSiteRecoveryNetworkMapping -PrimaryNetwork $Networks[0] -AzureVMNetworkId $AzureVmNetworks[0]

## <a name="step-9-enable-protection-for-virtual-machines"></a>Étape 9 : Activation de la protection des machines virtuelles
Une fois que les réseaux, les clouds et les serveurs de hello sont correctement configurés, vous pouvez activer la protection des machines virtuelles dans le cloud de hello.

 Notez hello suivantes :

* Les machines virtuelles doivent répondre aux exigences liées à Azure. Archiver ces [prise en charge et les conditions préalables](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) dans le guide de planification hello.
* protection de tooenable, système d’exploitation de hello et propriétés de disque de système d’exploitation doivent être définies pour la machine virtuelle de hello. Lorsque vous créez un ordinateur virtuel dans VMM à l’aide d’un modèle d’ordinateur virtuel, vous pouvez définir la propriété de hello. Vous pouvez également définir ces propriétés pour les ordinateurs virtuels existants sur hello **général** et **Configuration matérielle** onglets des propriétés d’ordinateur virtuel hello. Si vous ne définissez pas ces propriétés dans VMM, vous serez en mesure de tooconfigure dans le portail Azure Site Recovery hello.

1. protection de tooenable, exécutez hello suivant du conteneur de protection de commande tooget hello :

          $ProtectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $CloudName
2. Obtenir l’entité de protection hello (VM) en exécutant hello de commande suivante :

           $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -friendlyName $VMName -ProtectionContainer $protectionContainer
3. Activer hello récupération d’urgence pour hello machine virtuelle en exécutant hello de commande suivante :

          $jobResult = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionentity -Protection Enable –Force -Policy $policy -RecoveryAzureStorageAccountId  $storageID "/subscriptions/217653172865hcvkchgvd/resourceGroups/rajanirgps/providers/Microsoft.Storage/storageAccounts/teststorageacc1

## <a name="test-your-deployment"></a>Tester votre déploiement
tootest votre déploiement, vous pouvez exécuter un test de basculement pour une seule machine virtuelle, ou créer un plan de récupération composé de plusieurs machines virtuelles et exécuter un basculement test pour un plan de hello. Il simule votre mécanisme de basculement et de récupération dans un réseau isolé. Notez les points suivants :

* Si vous souhaitez tooconnect toohello machine virtuelle Azure à l’aide du Bureau à distance après le basculement hello, activer la connexion Bureau à distance sur l’ordinateur virtuel de hello avant d’exécuter le test de basculement hello.
* Après le basculement, vous allez utiliser un ordinateur virtuel toohello de publique IP adresse tooconnect dans Azure à l’aide du Bureau à distance. Si vous voulez toodo, assurez-vous que vous n’avez pas les stratégies de domaine qui vous empêchent de connexion tooa machine virtuelle une adresse publique.

achèvement de hello toocheck d’opération de hello, suivez les étapes de hello dans [surveiller l’activité](#monitor).

### <a name="run-a-test-failover"></a>Exécution d’un test de basculement
- Démarrez hello test de basculement en exécutant hello de commande suivante :

       $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

### <a name="run-a-planned-failover"></a>Exécuter un basculement planifié
- Hello de démarrer le basculement planifié en exécutant hello de commande suivante :

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

### <a name="run-an-unplanned-failover"></a>Exécuter un basculement non planifié
- Démarrer hello basculement non planifié en exécutant hello de commande suivante :

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

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
