---
title: "tooAzure d’ordinateurs virtuels Hyper-V aaaReplicate dans le portail classique de hello avec PowerShell | Documents Microsoft"
description: "Automatiser la réplication hello d’ordinateurs virtuels Hyper-V dans les clouds VMM à l’aide de la récupération de Site et de PowerShell dans le portail classique de hello"
services: site-recovery
documentationcenter: 
author: bsiva
manager: abhiag
editor: tysonn
ms.assetid: 9011f567-e0b4-4306-951a-b30da19f5db6
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: bsiva
ms.openlocfilehash: d6847b46ac227209e6890de4ab603b23f827360f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-vms-tooazure-with-powershell-in-hello-classic-portal"></a>Répliquer tooAzure d’ordinateurs virtuels Hyper-V avec PowerShell dans le portail classique de hello
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

Hello inclut les conditions préalables pour le scénario hello et montre que vous la manière dont les tooset d’un coffre Site Recovery, installez hello fournisseur Azure Site Recovery sur le serveur VMM de hello source, inscrire le serveur de hello dans le coffre de hello, ajoutez un compte de stockage Azure, installez hello Azure L’agent Recovery Services sur les serveurs hôtes de Hyper-V, configurer les paramètres de protection pour les clouds VMM qui seront appliqués tooall protégé par les ordinateurs virtuels et puis réactivez la protection pour ces ordinateurs virtuels. Terminez en toomake de basculement de test hello que tout fonctionne comme prévu.

Si vous rencontrez des problèmes de configuration de ce scénario, publiez vos questions sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

> [!NOTE]
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../azure-resource-manager/resource-manager-deployment-model.md). Cet article décrit à l’aide du modèle de déploiement classique hello.
>
>

## <a name="before-you-start"></a>Avant de commencer
Assurez-vous que les conditions préalables sont remplies :

### <a name="azure-prerequisites"></a>Conditions préalables pour Azure
* Vous aurez besoin d’un compte [Microsoft Azure](https://azure.microsoft.com/) . Vous pouvez commencer par une version d’ [essai gratuit](https://azure.microsoft.com/pricing/free-trial/).
* Vous aurez besoin d’un stockage Azure compte toostore répliquée de données. compte de Hello doit géo-réplication activée. Il doit être en hello même région que le coffre Azure Site Recovery hello et être associé hello même abonnement. [En savoir plus sur Azure Storage](../storage/common/storage-introduction.md).
* Vous devez toomake assurer que les ordinateurs virtuels que vous souhaitez tooprotect conformes [conditions préalables de machine virtuelle Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).

### <a name="vmm-prerequisites"></a>Configuration requise pour VMM
* Vous aurez besoin d’un serveur VMM exécuté sur System Center 2012 R2.
* Vous devez au moins un cloud sur hello serveur VMM que vous souhaitez tooprotect. cloud de Hello doit contenir :
  * un ou plusieurs groupes hôtes VMM ;
  * un ou plusieurs serveurs hôtes Hyper-V ou clusters dans chaque groupe hôte ;
  * Un ou plusieurs ordinateurs virtuels sur le serveur d’Hyper-V source hello.

### <a name="hyper-v-prerequisites"></a>Conditions préalables liées à Hyper-V
* Hello serveurs hôtes Hyper-V doivent être en cours d’exécution au moins **Windows Server 2012** avec le rôle Hyper-V ou **Microsoft Hyper-V Server 2012** et avez hello les dernières mises à jour installées.
* Si vous utilisez Hyper-V dans un cluster, notez que le service Broker du cluster n'est pas créé automatiquement si vous avez un cluster basé sur des adresses IP statiques. Vous devez manuellement service broker de cluster tooconfigure hello. toodo cela, dans le Gestionnaire de serveur > Gestionnaire du Cluster de basculement, connectez toohello cluster, cliquez sur **configurer un rôle** et sélectionnez **Service Broker de réplication Hyper-V** Bonjour **sélectionner un rôle**écran de l’Assistant haute disponibilité de hello.
* N’importe quel serveur hôte Hyper-V ou le cluster dont vous voulez toomanage protection doit être inclus dans un cloud VMM.

### <a name="network-mapping-prerequisites"></a>Conditions préalables liées au mappage réseau
Lorsque vous protégez des ordinateurs virtuels dans le mappage réseau Azure mappe entre les réseaux d’ordinateurs virtuels sur le serveur VMM de source hello et suivant de hello de tooenable de réseaux Azure cible :

* Toutes les machines qui basculent sur hello même réseau peut se connecter tooeach autre, quel que soit le plan de récupération auquel elles sont dans.
* Si une passerelle de réseau est configurée sur le réseau Azure cible de hello, les machines virtuelles peuvent se connecter tooother locaux virtuels.
* Si vous ne configurez pas de réseau mappage seuls les ordinateurs virtuels qui basculent Bonjour même plan de récupération sera en mesure de tooconnect tooeach autres après basculement tooAzure.

Si vous souhaitez que le mappage réseau toodeploy, vous devez suivant de hello :

* Hello machines virtuelles tooprotect sur le serveur VMM de hello source doit être connecté tooa réseau d’ordinateurs virtuels. Ce réseau doit être lié tooa réseau logique associé au cloud de hello.
* Un réseau de Azure toowhich répliquée d’ordinateurs virtuels peuvent se connecter après le basculement. Vous devez sélectionner ce réseau au moment du basculement de hello. réseau de Hello doivent se trouver dans hello même région que votre abonnement Azure Site Recovery.

### <a name="powershell-prerequisites"></a>Conditions préalables pour PowerShell
Assurez-vous que vous avez toogo prêt d’Azure PowerShell. Si vous utilisez déjà PowerShell, vous devez tooupgrade tooversion 0.8.10 ou version ultérieure. Pour plus d’informations sur la configuration de PowerShell, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azureps-cmdlets-docs). Après avoir configuré et configuré de PowerShell, vous pouvez afficher toutes les hello des applets de commande disponibles pour le service de hello [ici](/powershell/azure/overview).

toolearn sur les conseils qui peuvent vous aider à utiliser des applets de commande hello, telles que la façon dont les valeurs de paramètre, les entrées et sorties sont généralement gérées dans Azure PowerShell, consultez [prise en main des applets de commande Azure](/powershell/azure/get-started-azureps).

## <a name="step-1-set-hello-subscription"></a>Étape 1 : Définir l’abonnement de hello
Dans PowerShell, exécutez ces applets de commande :

```
$UserName = "<user@live.com>"
$Password = "<password>"
$AzureSubscriptionName = "prod_sub1"

$SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
$Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $securePassword
Add-AzureAccount -Credential $Cred;
$AzureSubscription = Select-AzureSubscription -SubscriptionName $AzureSubscriptionName

```

Remplacez les éléments hello hello « < > » avec des informations spécifiques à votre.

## <a name="step-2-create-a-site-recovery-vault"></a>Étape 2 : Création d’un coffre Site Recovery
Dans PowerShell, remplacer les éléments de hello dans hello « < > » avec des informations spécifiques et exécuter ces commandes :

```

$VaultName = "<testvault123>"
$VaultGeo  = "<Southeast Asia>"
$OutputPathForSettingsFile = "<c:\>"

```


```
New-AzureSiteRecoveryVault -Location $VaultGeo -Name $VaultName;
$vault = Get-AzureSiteRecoveryVault -Name $VaultName;

```

## <a name="step-3-generate-a-vault-registration-key"></a>Étape 3 : Génération d’une clé d'inscription du coffre
Générer une clé d’inscription dans le coffre hello. Une fois que vous téléchargez hello fournisseur Azure Site Recovery et l’installer sur le serveur VMM de hello, vous allez utiliser ce serveur VMM de hello tooregister clé dans le coffre hello.

1. Obtenir le fichier de paramètres de coffre hello et définir le contexte de hello :

   ```

   $VaultName = "<testvault123>"
   $VaultGeo  = "<Southeast Asia>"
   $OutputPathForSettingsFile = "<c:\>"

   $VaultSetingsFile = Get-AzureSiteRecoveryVaultSettingsFile -Location $VaultGeo -Name $VaultName -Path $OutputPathForSettingsFile;

   ```
2. Définir le contexte de coffre hello en hello suivant les commandes en cours d’exécution :

   ```

   $VaultSettingFilePath = $vaultSetingsFile.FilePath
   $VaultContext = Import-AzureSiteRecoveryVaultSettingsFile -Path $VaultSettingFilePath -ErrorAction Stop

   ```

## <a name="step-4-install-hello-azure-site-recovery-provider"></a>Étape 4 : Installer hello fournisseur Azure Site Recovery
1. Sur l’ordinateur VMM hello, créez un répertoire en exécutant hello de commande suivante :

   ```

   pushd C:\ASR\

   ```
2. Extrayez les fichiers hello à l’aide de fournisseur de hello téléchargé en exécutant hello commande suivante

   ```

   AzureSiteRecoveryProvider.exe /x:. /q

   ```
3. Installez le fournisseur hello hello suivant les commandes à l’aide de :

   ```

   .\SetupDr.exe /i

   ```

   ```

   $installationRegPath = "hklm:\software\Microsoft\Microsoft System Center Virtual Machine Manager Server\DRAdapter"
   do
   {
     $isNotInstalled = $true;
     if(Test-Path $installationRegPath)
     {
         $isNotInstalled = $false;
     }
   }While($isNotInstalled)

   ```

   Attendez que hello installation toofinish.
4. Inscrire un serveur hello dans le coffre de hello à l’aide de hello de commande suivante :

   ```

   $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
   pushd $BinPath
   $encryptionFilePath = "C:\temp\"
   .\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

   ```

## <a name="step-5-create-an-azure-storage-account"></a>Étape 5 : Création d’un compte de stockage Azure
Si vous n’avez pas un compte de stockage Azure, créez un compte de géo-réplication activée en exécutant hello de commande suivante :

```

$StorageAccountName = "teststorageacc1"
$StorageAccountGeo  = "Southeast Asia"

New-AzureStorageAccount -StorageAccountName $StorageAccountName -Label $StorageAccountName -Location $StorageAccountGeo;

```

Notez que le compte de stockage hello doit être en hello même région que le service d’Azure Site Recovery hello et être associé à hello même abonnement.

## <a name="step-6-install-hello-azure-recovery-services-agent"></a>Étape 6 : Installer hello Azure Recovery Services Agent
À partir de hello portail Azure, installation Bonjour Azure Recovery Services agent sur chaque serveur hôte de Hyper-V située dans des clouds VMM hello souhaité tooprotect.

Exécutez hello commande suivante sur tous les hôtes VMM :

```

marsagentinstaller.exe /q /nu

```


## <a name="step-7-configure-cloud-protection-settings"></a>Étape 7 : Configuration des paramètres de protection de cloud
1. Créer un tooAzure de profil de protection de cloud en exécutant hello de commande suivante :

   ```

   $ReplicationFrequencyInSeconds = "300";
   $ProfileResult = New-AzureSiteRecoveryProtectionProfileObject -ReplicationProvider HyperVReplica -RecoveryAzureSubscription $AzureSubscriptionName -RecoveryAzureStorageAccount $StorageAccountName -ReplicationFrequencyInSeconds     $ReplicationFrequencyInSeconds;

   ```
2. Pour obtenir un conteneur de protection, hello suivant les commandes en cours d’exécution :

   ```

   $PrimaryCloud = "testcloud"
   $protectionContainer = Get-AzureSiteRecoveryProtectionContainer -Name $PrimaryCloud;

   ```
3. Démarrer l’association hello du conteneur de protection hello avec le cloud de hello :

   ```

   $associationJob = Start-AzureSiteRecoveryProtectionProfileAssociationJob -ProtectionProfile $profileResult -PrimaryProtectionContainer $protectionContainer;        

   ```
4. Une fois le travail de hello terminée, exécutez hello de commande suivante :

        $job = Get-AzureSiteRecoveryJob -Id $associationJob.JobId;
        if($job -eq $null -or $job.StateDescription -ne "Completed")
        {
        $isJobLeftForProcessing = $true;
        }


1. Une fois le travail de hello a terminé le traitement, exécutez hello de commande suivante :

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



achèvement de hello toocheck d’opération de hello, suivez les étapes de hello dans [surveiller l’activité](#monitor).

## <a name="step-8-configure-network-mapping"></a>Étape 8 : Configuration du mappage réseau
Avant de commencer le mappage réseau Vérifiez que les ordinateurs virtuels sur le serveur VMM de hello source sont connectés tooa réseau d’ordinateurs virtuels. En outre, vous devez créer un ou plusieurs réseaux virtuels Azure. Notez que plusieurs réseaux d’ordinateurs virtuels peuvent être mappés tooa réseau Azure unique.

Notez que si le réseau cible de hello possède plusieurs sous-réseaux et d’un de ces sous-réseaux a hello trouve du même nom que le sous-réseau sur lequel hello source virtual machine, puis hello ordinateur virtuel sera connecté toothat cible sous-réseau après le basculement. S’il n’est pas un sous-réseau cible avec un nom correspondant, ordinateur virtuel de hello sera connecté toohello premier sous-réseau de réseau de hello.

Hello première commande Obtient les serveurs pour le coffre Azure Site Recovery en cours hello. commande Hello stocke les serveurs Microsoft Azure Site Recovery hello dans la variable de tableau hello $Servers.

    $Servers = Get-AzureSiteRecoveryServer


commande deuxième Hello obtient réseau de récupération de site hello pour le premier serveur de hello hello $Servers tableau. commande Hello stocke des réseaux de hello dans la variable de hello $Networks.

    $Networks = Get-AzureSiteRecoveryNetwork -Server $Servers[0]

commande troisième Hello Obtient de vos abonnements Azure à l’aide d’applet de commande Get-AzureSubscription de hello, puis stocke cette valeur dans la variable de hello $Subscriptions.

    $Subscriptions = Get-AzureSubscription



Hello quatrième commande récupère les réseaux virtuels Azure à l’aide d’applet de commande Get-AzureVNetSite de hello et ensuite cette valeur dans la variable de hello $AzureVmNetworks.

    $AzureVmNetworks = Get-AzureVNetSite



applet de commande finale Hello crée un mappage entre le réseau principal de hello et réseau de machine virtuelle Azure hello. applet de commande Hello Spécifie le réseau principal de hello en tant que premier élément de hello de $Networks. applet de commande Hello spécifie un réseau d’ordinateurs virtuels en tant que premier élément de hello de $AzureVmNetworks à l’aide de son ID. commande Hello inclut votre ID d’abonnement Azure.

    New-AzureSiteRecoveryNetworkMapping -PrimaryNetwork $Networks[0] -AzureSubscriptionId $Subscriptions[0].SubscriptionId -AzureVMNetworkId $AzureVmNetworks[0].Id


## <a name="step-9-enable-protection-for-virtual-machines"></a>Étape 9 : Activation de la protection des machines virtuelles
Une fois les serveurs, les clouds et les réseaux configurés, vous pouvez activer la protection des machines virtuelles dans le cloud de hello. Notez hello suivantes :

Les machines virtuelles doivent répondre à la [configuration requise pour les machines virtuelles Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).

système d’exploitation de tooenable protection hello et les propriétés de disque de système d’exploitation doivent être définies pour la machine virtuelle de hello. Lorsque vous créez un ordinateur virtuel dans VMM à l’aide d’un modèle d’ordinateur virtuel, vous pouvez définir la propriété de hello. Vous pouvez également définir ces propriétés pour les ordinateurs virtuels existants sur hello **général** et **Configuration matérielle** onglets des propriétés d’ordinateur virtuel hello. Si vous ne définissez pas ces propriétés dans VMM, vous serez en mesure de tooconfigure dans le portail Azure Site Recovery hello.

1. protection de tooenable, exécutez hello suivant du conteneur de protection de commande tooget hello :

     $ProtectionContainer = Get-AzureSiteRecoveryProtectionContainer -Name $CloudName
2. Obtenir l’entité de protection hello (VM) en exécutant hello de commande suivante :

        $protectionEntity = Get-AzureSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer



1. Activer hello récupération d’urgence pour hello machine virtuelle en exécutant hello de commande suivante :

        $jobResult = Set-AzureSiteRecoveryProtectionEntity -ProtectionEntity $protectionEntity     -Protection Enable -Force



## <a name="test-your-deployment"></a>Tester votre déploiement
planification de votre déploiement, vous pouvez exécuter un test de basculement pour une seule machine virtuelle, ou créer un plan de récupération composé de plusieurs ordinateurs virtuels et exécuter un test de basculement pour hello tootest. Il simule votre mécanisme de basculement et de récupération dans un réseau isolé. Notez les points suivants :

* Si vous souhaitez tooconnect toohello machine virtuelle Azure à l’aide du Bureau à distance après le basculement de hello, activer la connexion Bureau à distance sur l’ordinateur virtuel de hello avant d’exécuter le test de basculement hello.
* Après le basculement, vous allez utiliser un ordinateur virtuel toohello de publique IP adresse tooconnect dans Azure à l’aide du Bureau à distance. Si vous voulez toodo, assurez-vous que vous n’avez pas les stratégies de domaine qui vous empêchent de connexion tooa machine virtuelle une adresse publique.

achèvement de hello toocheck d’opération de hello, suivez les étapes de hello dans [surveiller l’activité](#monitor).

### <a name="create-a-recovery-plan"></a>Créer un plan de récupération
1. Créer un fichier .xml comme modèle pour votre plan de récupération à l’aide de données hello ci-dessous, puis enregistrez-le en tant que « C:\RPTemplatePath.xml ».
2. Modifier l’Id de nœud RecoveryPlan hello, nom, PrimaryServerId et SecondaryServerId.
3. Modifier le nœud de ProtectionEntity hello PrimaryProtectionEntityId (vmid de VMM).
4. Vous pouvez ajouter davantage de machines virtuelles en ajoutant des nœuds ProtectionEntity.

        <#
        <?xml version="1.0" encoding="utf-16"?>
        <RecoveryPlan Id="d0323b26-5be2-471b-addc-0a8742796610" Name="rp-test"     PrimaryServerId="9350a530-d5af-435b-9f2b-b941b5d9fcd5"     SecondaryServerId="21a9403c-6ec1-44f2-b744-b4e50b792387" Description=""     Version="V2014_07">
          <Actions />
          <ActionGroups>
            <ShutdownAllActionGroup Id="ShutdownAllActionGroup">
              <PreActionSequence />
              <PostActionSequence />
            </ShutdownAllActionGroup>
            <FailoverAllActionGroup Id="FailoverAllActionGroup">
              <PreActionSequence />
              <PostActionSequence />
            </FailoverAllActionGroup>
            <BootActionGroup Id="DefaultActionGroup">
              <PreActionSequence />
              <PostActionSequence />
              <ProtectionEntity PrimaryProtectionEntityId="d4c8ce92-a613-4c63-9b03-    cf163cc36ef8" />
            </BootActionGroup>
          </ActionGroups>
          <ActionGroupSequence>
            <ActionGroup Id="ShutdownAllActionGroup" ActionId="ShutdownAllActionGroup"     Before="FailoverAllActionGroup" />
            <ActionGroup Id="FailoverAllActionGroup" ActionId="FailoverAllActionGroup"     After="ShutdownAllActionGroup" Before="DefaultActionGroup" />
            <ActionGroup Id="DefaultActionGroup" ActionId="DefaultActionGroup" After="FailoverAllActionGroup"/>
          </ActionGroupSequence>
        </RecoveryPlan>
        #>



1. Renseignez les données de salutation dans le modèle de hello :

        $TemplatePath = "C:\RPTemplatePath.xml";



1. Créer hello RecoveryPlan :

        $RPCreationJob = New-AzureSiteRecoveryRecoveryPlan -File $TemplatePath -WaitForCompletion;

### <a name="run-a-test-failover"></a>Exécution d’un test de basculement
1. Obtenir l’objet de RecoveryPlan hello en exécutant hello de commande suivante :

     $RPObject = Get-AzureSiteRecoveryRecoveryPlan -Name $RPName;
2. Démarrez hello test de basculement en exécutant hello de commande suivante :

        $jobIDResult = Start-AzureSiteRecoveryTestFailoverJob -RecoveryPlan $RPObject -Direction PrimaryToRecovery;


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
[Découvrez plus](/powershell/azure/overview) d'informations sur les applets de commande PowerShell Azure Site Recovery. </a>.
