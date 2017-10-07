---
title: aaaReplicate machines virtuelles de Hyper-V avec PowerShell et le Gestionnaire de ressources Azure | Documents Microsoft
description: "Automatiser la réplication des ordinateurs virtuels Hyper-V tooAzure hello avec Azure Site Recovery à l’aide de PowerShell et le Gestionnaire de ressources Azure."
services: site-recovery
documentationcenter: 
author: bsiva
manager: abhiag
editor: 
ms.assetid: 05e0d76e-c3f5-4845-8052-094019b6d102
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/31/2017
ms.author: bsiva
ms.openlocfilehash: 4fb15ce2e9ad54f1dd6f54ff769eb912aa4b0272
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-between-on-premises-hyper-v-virtual-machines-and-azure-by-using-powershell-and-azure-resource-manager"></a>Réplication de machines virtuelles Hyper-V en local dans Azure avec PowerShell et Azure Resource Manager.
> [!div class="op_single_selector"]
> * [Portail Azure](site-recovery-hyper-v-site-to-azure.md)
> * [PowerShell - Resource Manager](site-recovery-deploy-with-powershell-resource-manager.md)
> * [Portail Classic](site-recovery-hyper-v-site-to-azure-classic.md)
>
>

## <a name="overview"></a>Vue d'ensemble
Azure Site Recovery contribue stratégie récupération tooyour commerciale la continuité des activités et d’urgence en coordonnant la réplication, le basculement et récupération des machines virtuelles dans un nombre de scénarios de déploiement. Pour obtenir une liste complète des scénarios de déploiement, consultez hello [vue d’ensemble d’Azure Site Recovery](site-recovery-overview.md).

Azure PowerShell est un module qui fournit des applets de commande toomanage Azure via Windows PowerShell. Il peut fonctionner avec deux types de modules : hello module de profil Azure, ou le module de gestionnaire de ressources Azure hello.

Les applets de commande PowerShell de Site Recovery, disponibles avec Azure PowerShell pour Azure Resource Manager, vous permettent de protéger et récupérer vos serveurs dans Azure.

Cet article décrit comment toouse Windows PowerShell, avec Azure Resource Manager toodeploy Site Recovery tooconfigure et orchestrer tooAzure de protection de serveur. exemple Hello utilisée dans cet article vous montre comment tooprotect, basculer et récupérer des ordinateurs virtuels sur un tooAzure hôte Hyper-V, à l’aide d’Azure PowerShell avec Azure Resource Manager.

> [!NOTE]
> Hello applets de commande PowerShell de récupération de Site actuellement permettent de hello tooconfigure suivant : un tooanother de site de Virtual Machine Manager, un tooAzure de site de Virtual Machine Manager et un tooAzure de site Hyper-V.
>
>

Vous n’avez pas besoin toobe un toouse expert PowerShell cet article, mais vous n’avez pas besoin de toounderstand hello concepts de base, tels que des modules, applets de commande et des sessions. Pour plus d'informations sur Windows PowerShell, consultez la page [Prise en main de Windows PowerShell](http://technet.microsoft.com/library/hh857337.aspx).

Vous pouvez également lire l’article [Utilisation d’Azure PowerShell avec Azure Resource Manager](../powershell-azure-resource-manager.md)pour en savoir plus.

> [!NOTE]
> Les partenaires Microsoft qui font partie du programme de fournisseur de solutions de Cloud (CSP) hello peuvent configurer et gérer la protection des serveurs de leurs clients respectifs CSP abonnements (client) tootheir clients.
>
>

## <a name="before-you-start"></a>Avant de commencer
Assurez-vous que les conditions préalables sont remplies :

* Un compte [Microsoft Azure](https://azure.microsoft.com/) . Vous pouvez commencer avec une [version d'évaluation gratuite](https://azure.microsoft.com/pricing/free-trial/). Vous pouvez aussi consulter la [Tarification Azure Site Recovery Manager](https://azure.microsoft.com/pricing/details/site-recovery/).
* Azure PowerShell 1.0. Pour plus d’informations sur cette version et comment tooinstall, consultez [Azure PowerShell 1.0.](https://azure.microsoft.com/)
* Hello [AzureRM.SiteRecovery](https://www.powershellgallery.com/packages/AzureRM.SiteRecovery/) et [AzureRM.RecoveryServices](https://www.powershellgallery.com/packages/AzureRM.RecoveryServices/) modules. Vous pouvez obtenir les versions les plus récentes de ces modules hello de hello [galerie PowerShell](https://www.powershellgallery.com/)

Cet article explique comment toouse Azure Powershell avec Azure Resource Manager tooconfigure et gérer la protection de vos serveurs. exemple Hello utilisée dans cet article vous montre comment tooprotect une machine virtuelle, en cours d’exécution sur un ordinateur hôte Hyper-V, tooAzure. Hello, suivant les conditions préalables est des exemples de toothis spécifique. Pour un ensemble plus complet de la configuration requise pour hello différents scénarios de récupération de Site, consultez la documentation de toohello se rapportant toothat scénario.

* Un hôte Hyper-V exécuté sous Windows Server 2012 R2 ou Microsoft Hyper-V Server 2012 R2 et hébergeant une ou plusieurs machines virtuelles.
* Serveurs Hyper-V connecté toohello Internet, directement ou via un proxy.
* Hello machines virtuelles tooprotect doivent respecter les [conditions préalables requises de l’ordinateur virtuel](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).

## <a name="step-1-sign-in-tooyour-azure-account"></a>Étape 1 : Se connecter tooyour compte Azure
1. Ouvrez une console PowerShell et exécuter cette commande toosign dans tooyour compte Azure. applet de commande Hello affiche une page web qui vous demande vos informations d’identification de compte.

        Login-AzureRmAccount

    Ou bien, vous pouvez également inclure vos informations d’identification de compte comme un paramètre toohello `Login-AzureRmAccount` applet de commande, à l’aide de hello `-Credential` paramètre.

    Si vous êtes CSP fonctionne pour le compte d’un client, spécifiez les clients hello en tant que client, à l’aide de leur nom de domaine principal tenantID ou locataire.

        Login-AzureRmAccount -Tenant "fabrikam.com"
2. Un compte peut avoir plusieurs abonnements, donc vous devez associer abonnement hello toouse avec un compte de hello.

        Select-AzureRmSubscription -SubscriptionName $SubscriptionName
3. Vérifiez que votre abonnement est inscrit toouse hello Azure fournisseurs de Services de récupération et la récupération de Site, à l’aide de hello suivant de commandes :

   * `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices`
   * `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`

   Dans la sortie de hello de ces commandes, si hello **RegistrationState** est défini trop**inscrit**, vous pouvez passer tooStep 2. Si ce n’est pas le cas, vous devez inscrire le fournisseur de hello manquant dans votre abonnement.

   hello tooregister fournisseur Azure Site Recovery Services et de récupération, exécutez hello suivant les commandes :

       Register-AzureRmResourceProvider -ProviderNamespace Microsoft.SiteRecovery
       Register-AzureRmResourceProvider -ProviderNamespace Microsoft.RecoveryServices

   Vérifiez que les fournisseurs hello a été correctement inscrit à l’aide de hello suivant de commandes : `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices` et `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`.

## <a name="step-2-set-up-hello-recovery-services-vault"></a>Étape 2 : Configurer hello de coffre Recovery Services
1. Créer un groupe de ressources Azure Resource Manager, dans lequel vous allez créer hello coffre, ou utiliser un groupe de ressources existant. Vous pouvez créer un nouveau groupe de ressources à l’aide de hello de commande suivante :

        New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Geo  

    Lorsque la variable de hello $ResourceGroupName contient le nom hello hello du groupe de ressources et vous souhaitez toocreate variable de hello $Geo contient hello Azure région dans le groupe de ressources hello toocreate (par exemple, « Brésil Sud »).

    Vous pouvez obtenir une liste des groupes de ressources dans votre abonnement à l’aide de hello `Get-AzureRmResourceGroup` applet de commande.
2. Créez un coffre Azure Recovery Services de la manière suivante :

        $vault = New-AzureRmRecoveryServicesVault -Name <string> -ResourceGroupName <string> -Location <string>

    Vous pouvez récupérer une liste des archivages existants à l’aide de hello `Get-AzureRmRecoveryServicesVault` applet de commande.

> [!NOTE]
> Si vous souhaitez tooperform les opérations sur des coffres de récupération de Site créées à l’aide du portail classique de hello ou un module PowerShell Azure Service Management de hello, vous pouvez récupérer une liste de ces coffres à l’aide de hello `Get-AzureRmSiteRecoveryVault` applet de commande. Il est recommandé de créer un coffre Recovery Services pour toutes les nouvelles opérations. les coffres de récupération de Site Hello que vous avez créé précédemment sont pris en charge, mais n’ont pas les fonctionnalités plus récentes hello.
>
>

## <a name="step-3-set-hello-recovery-services-vault-context"></a>Étape 3 : Configurer les Services de récupération hello coffre contexte
1. Définir le contexte de coffre hello en exécutant hello de commande suivante :

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-create-a-hyper-v-site-and-generate-a-new-vault-registration-key-for-hello-site"></a>Étape 4 : Créer un site Hyper-V et générer une nouvelle clé d’inscription de coffre pour le site de hello.
1. Créez un nouveau site Hyper-V comme suit :

        $sitename = "MySite"                #Specify site friendly name
        New-AzureRmSiteRecoverySite -Name $sitename

    Cette applet de commande démarre un site de récupération de Site travail toocreate hello et retourne un objet de tâche de récupération de Site. Attendre hello travail toocomplete et vérifiez que le travail hello est terminée avec succès.

    Vous pouvez récupérer l’objet de tâche hello et ainsi vérifier état actuel de hello hello du travail de, à l’aide d’applet de commande Get-AzureRmSiteRecoveryJob de hello.
2. Générez et téléchargez une clé d’inscription pour le site de hello, comme suit :

        $SiteIdentifier = Get-AzureRmSiteRecoverySite -Name $sitename | Select -ExpandProperty SiteIdentifier
        Get-AzureRmRecoveryServicesVaultSettingsFile -Vault $vault -SiteIdentifier $SiteIdentifier -SiteFriendlyName $sitename -Path $Path

    Hello de copie téléchargé hôte de la clé toohello Hyper-V. Vous devez le site toohello hôte hello tooregister clé hello Hyper-V.

## <a name="step-5-install-hello-azure-site-recovery-provider-and-azure-recovery-services-agent-on-your-hyper-v-host"></a>Étape 5 : Installer le fournisseur Azure Site Recovery hello et Azure Recovery Services Agent sur votre hôte Hyper-V
1. Télécharger installer hello pour la version la plus récente du fournisseur hello dans hello [Microsoft](https://aka.ms/downloaddra).
2. Programme d’installation de l’exécution hello sur votre ordinateur hôte Hyper-V et à fin hello d’installation de hello continuer étape d’inscription de toohello.
3. Lorsque vous y êtes invité, fournissez hello téléchargé la clé d’inscription de site et de terminer l’inscription du site de toohello hôte hello Hyper-V.
4. Vérifiez que cet ordinateur hôte Hyper-V de hello est toohello inscrits à l’aide de hello de commande suivante :

        $server =  Get-AzureRmSiteRecoveryServer -FriendlyName $server-friendlyname

## <a name="step-6-create-a-replication-policy-and-associate-it-with-hello-protection-container"></a>Étape 6 : Créer une stratégie de réplication et associez-la à un conteneur de protection de hello
1. Créez une stratégie de réplication comme suit :

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $Recoverypoints = 6                    #specify hello number of recovery points
        $storageaccountID = Get-AzureRmStorageAccount -Name "mystorea" -ResourceGroupName "MyRG" | Select -ExpandProperty Id

        $PolicyResult = New-AzureRmSiteRecoveryPolicy -Name $PolicyName -ReplicationProvider “HyperVReplicaAzure” -ReplicationFrequencyInSeconds $ReplicationFrequencyInSeconds  -RecoveryPoints $Recoverypoints -ApplicationConsistentSnapshotFrequencyInHours 1 -RecoveryAzureStorageAccountId $storageaccountID

    Bonjour à cocher retourné tooensure de travail Création de la stratégie de réplication hello réussit.

   > [!IMPORTANT]
   > Hello compte de stockage spécifié doit être dans hello même région Azure que votre coffre Recovery Services, ainsi que la géo-réplication activée.
   >
   > * Si hello spécifié de récupération de compte de stockage est de type de stockage de Azure (classique), basculement Hello protégé machines recover hello machine tooAzure IaaS (classique).
   > * Si hello spécifié le compte de stockage de récupération est de type de stockage de Azure (Azure Resource Manager), basculement Hello protégé machines recover hello machine tooAzure IaaS (Azure Resource Manager).
   >
   >
2. Obtenir hello protection conteneur toohello site correspondant, comme suit :

        $protectionContainer = Get-AzureRmSiteRecoveryProtectionContainer
3. Démarrez association hello du conteneur de protection hello avec la stratégie de réplication hello, comme suit :

     $Policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $PolicyName   $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy $Policy -PrimaryProtectionContainer $protectionContainer

   Attendez hello association tâche toocomplete et vérifiez qu’il s’est terminée avec succès.

## <a name="step-7-enable-protection-for-virtual-machines"></a>Étape 7 : Activation de la protection des machines virtuelles
1. Obtenir hello protection entité correspondante toohello machine virtuelle tooprotect, comme suit :

        $VMFriendlyName = "Fabrikam-app"                    #Name of hello VM
        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -ProtectionContainer $protectionContainer -FriendlyName $VMFriendlyName
2. Démarrer la protection de machine virtuelle de hello, comme suit :

        $Ostype = "Windows"                                 # "Windows" or "Linux"
        $DRjob = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionEntity -Policy $Policy -Protection Enable -RecoveryAzureStorageAccountId $storageaccountID  -OS $OStype -OSDiskName $protectionEntity.Disks[0].Name

   > [!IMPORTANT]
   > Hello compte de stockage spécifié doit être dans hello même région Azure que votre coffre Recovery Services, ainsi que la géo-réplication activée.
   >
   > * Si hello spécifié de récupération de compte de stockage est de type de stockage de Azure (classique), basculement Hello protégé machines recover hello machine tooAzure IaaS (classique).
   > * Si hello spécifié le compte de stockage de récupération est de type de stockage de Azure (Azure Resource Manager), basculement Hello protégé machines recover hello machine tooAzure IaaS (Azure Resource Manager).
   >
   > Si hello machine virtuelle que vous protégez comporte plus d’un disque attaché tooit, spécifiez le disque du système d’exploitation hello à l’aide de hello *OSDiskName* paramètre.
   >
   >
3. Attendez que hello machines virtuelles tooreach un état de protection après la réplication initiale de hello. Cela peut prendre un certain temps, en fonction de facteurs tels que la quantité de hello de toobe de données répliquée et hello tooAzure de la bande passante disponible en amont. État de la tâche Hello et ÉtatDescription sont mis à jour, procédez comme suit à hello atteindre un état de protection de machine virtuelle.

        PS C:\> $DRjob = Get-AzureRmSiteRecoveryJob -Job $DRjob

        PS C:\> $DRjob | Select-Object -ExpandProperty State
        Succeeded

        PS C:\> $DRjob | Select-Object -ExpandProperty StateDescription
        Completed
4. Mettre à jour les propriétés de récupération, telles que hello taille de rôle de machine virtuelle et hello réseau Azure tooattach hello du réseau interface cartes tooupon basculement de machine virtuelle.

        PS C:\> $nw1 = Get-AzureRmVirtualNetwork -Name "FailoverNw" -ResourceGroupName "MyRG"

        PS C:\> $VMFriendlyName = "Fabrikam-App"

        PS C:\> $VM = Get-AzureRmSiteRecoveryVM -ProtectionContainer $protectionContainer -FriendlyName $VMFriendlyName

        PS C:\> $UpdateJob = Set-AzureRmSiteRecoveryVM -VirtualMachine $VM -PrimaryNic $VM.NicDetailsList[0].NicId -RecoveryNetworkId $nw1.Id -RecoveryNicSubnetName $nw1.Subnets[0].Name

        PS C:\> $UpdateJob = Get-AzureRmSiteRecoveryJob -Job $UpdateJob

        PS C:\> $UpdateJob

        Name             : b8a647e0-2cb9-40d1-84c4-d0169919e2c5
        ID               : /Subscriptions/a731825f-4bf2-4f81-a611-c331b272206e/resourceGroups/MyRG/providers/Microsoft.RecoveryServices/vault
                           s/MyVault/replicationJobs/b8a647e0-2cb9-40d1-84c4-d0169919e2c5
        Type             : Microsoft.RecoveryServices/vaults/replicationJobs
        JobType          : UpdateVmProperties
        DisplayName      : Update hello virtual machine
        ClientRequestId  : 805a22a3-be86-441c-9da8-f32685673112-2015-12-10 17:55:51Z-P
        State            : Succeeded
        StateDescription : Completed
        StartTime        : 10-12-2015 17:55:53 +00:00
        EndTime          : 10-12-2015 17:55:54 +00:00
        TargetObjectId   : 289682c6-c5e6-42dc-a1d2-5f9621f78ae6
        TargetObjectType : ProtectionEntity
        TargetObjectName : Fabrikam-App
        AllowedActions   : {Restart}
        Tasks            : {UpdateVmPropertiesTask}
        Errors           : {}



## <a name="step-8-run-a-test-failover"></a>Étape 8 : Exécution d’un test de basculement
1. Exécutez une tâche de test de basculement, en procédant comme suit :

        $nw = Get-AzureRmVirtualNetwork -Name "TestFailoverNw" -ResourceGroupName "MyRG" #Specify Azure vnet name and resource group

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -FriendlyName $VMFriendlyName -ProtectionContainer $protectionContainer

        $TFjob = Start-AzureRmSiteRecoveryTestFailoverJob -ProtectionEntity $protectionEntity -Direction PrimaryToRecovery -AzureVMNetworkId $nw.Id
2. Vérifiez que le test hello que machine virtuelle est créée dans Azure. (travail de basculement de test hello est suspendu, après avoir créé la machine virtuelle de test hello dans Azure. Hello tâche se termine par un nettoyage des artefacts hello créé lors de la reprise du travail de hello, comme illustré dans l’étape suivante de hello.)
3. Hello complète test de basculement, comme suit :

        $TFjob = Resume-AzureRmSiteRecoveryJob -Job $TFjob

## <a name="next-steps"></a>Étapes suivantes
[En savoir plus](https://msdn.microsoft.com/library/azure/mt637930.aspx) sur Azure Site Recovery avec les applets de commande PowerShell Azure Resource Manager.
