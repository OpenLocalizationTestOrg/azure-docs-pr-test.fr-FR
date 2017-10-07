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
# <a name="replicate-hyper-v-vms-tooazure-with-powershell-in-hello-classic-portal"></a><span data-ttu-id="bbf37-103">Répliquer tooAzure d’ordinateurs virtuels Hyper-V avec PowerShell dans le portail classique de hello</span><span class="sxs-lookup"><span data-stu-id="bbf37-103">Replicate Hyper-V VMs tooAzure with PowerShell in hello classic portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bbf37-104">portail Azure</span><span class="sxs-lookup"><span data-stu-id="bbf37-104">Azure Portal</span></span>](site-recovery-vmm-to-azure.md)
> * [<span data-ttu-id="bbf37-105">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="bbf37-105">PowerShell - Resource Manager</span></span>](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [<span data-ttu-id="bbf37-106">Portail Classic</span><span class="sxs-lookup"><span data-stu-id="bbf37-106">Classic Portal</span></span>](site-recovery-vmm-to-azure-classic.md)
> * [<span data-ttu-id="bbf37-107">PowerShell - Classique</span><span class="sxs-lookup"><span data-stu-id="bbf37-107">PowerShell - Classic</span></span>](site-recovery-deploy-with-powershell.md)
>
>

## <a name="overview"></a><span data-ttu-id="bbf37-108">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="bbf37-108">Overview</span></span>
<span data-ttu-id="bbf37-109">Azure Site Recovery contribue stratégie récupération tooyour commerciale la continuité des activités et d’urgence en coordonnant la réplication, le basculement et récupération des machines virtuelles dans un nombre de scénarios de déploiement.</span><span class="sxs-lookup"><span data-stu-id="bbf37-109">Azure Site Recovery contributes tooyour business continuity and disaster recovery (BCDR) strategy by orchestrating replication, failover and recovery of virtual machines in a number of deployment scenarios.</span></span> <span data-ttu-id="bbf37-110">Pour obtenir la liste complète de déploiement de scénarios consultez hello [vue d’ensemble d’Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bbf37-110">For a full list of deployment scenarios see hello [Azure Site Recovery overview](site-recovery-overview.md).</span></span>

<span data-ttu-id="bbf37-111">Cet article explique comment les tâches courantes toouse PowerShell tooautomate vous devez tooperform lorsque vous configurez Azure Site Recovery tooreplicate Hyper-V virtual machines dans le stockage de System Center VMM clouds tooAzure.</span><span class="sxs-lookup"><span data-stu-id="bbf37-111">This article shows you how toouse PowerShell tooautomate common tasks you need tooperform when you set up Azure Site Recovery tooreplicate Hyper-V virtual machines in System Center VMM clouds tooAzure storage.</span></span>

<span data-ttu-id="bbf37-112">Hello inclut les conditions préalables pour le scénario hello et montre que vous la manière dont les tooset d’un coffre Site Recovery, installez hello fournisseur Azure Site Recovery sur le serveur VMM de hello source, inscrire le serveur de hello dans le coffre de hello, ajoutez un compte de stockage Azure, installez hello Azure L’agent Recovery Services sur les serveurs hôtes de Hyper-V, configurer les paramètres de protection pour les clouds VMM qui seront appliqués tooall protégé par les ordinateurs virtuels et puis réactivez la protection pour ces ordinateurs virtuels.</span><span class="sxs-lookup"><span data-stu-id="bbf37-112">hello article includes prerequisites for hello scenario, and shows you how tooset up a Site Recovery vault, install hello Azure Site Recovery Provider on hello source VMM server, register hello server in hello vault, add an Azure storage account, install hello Azure Recovery Services agent on Hyper-V host servers, configure protection settings for VMM clouds that will be applied tooall protected virtual machines, and then enable protection for those virtual machines.</span></span> <span data-ttu-id="bbf37-113">Terminez en toomake de basculement de test hello que tout fonctionne comme prévu.</span><span class="sxs-lookup"><span data-stu-id="bbf37-113">Finish up by testing hello failover toomake sure everything's working as expected.</span></span>

<span data-ttu-id="bbf37-114">Si vous rencontrez des problèmes de configuration de ce scénario, publiez vos questions sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="bbf37-114">If you run into problems setting up this scenario, post your questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

> [!NOTE]
> <span data-ttu-id="bbf37-115">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="bbf37-115">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="bbf37-116">Cet article décrit à l’aide du modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="bbf37-116">This article covers using hello Classic deployment model.</span></span>
>
>

## <a name="before-you-start"></a><span data-ttu-id="bbf37-117">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="bbf37-117">Before you start</span></span>
<span data-ttu-id="bbf37-118">Assurez-vous que les conditions préalables sont remplies :</span><span class="sxs-lookup"><span data-stu-id="bbf37-118">Make sure you have these prerequisites in place:</span></span>

### <a name="azure-prerequisites"></a><span data-ttu-id="bbf37-119">Conditions préalables pour Azure</span><span class="sxs-lookup"><span data-stu-id="bbf37-119">Azure prerequisites</span></span>
* <span data-ttu-id="bbf37-120">Vous aurez besoin d’un compte [Microsoft Azure](https://azure.microsoft.com/) .</span><span class="sxs-lookup"><span data-stu-id="bbf37-120">You'll need a [Microsoft Azure](https://azure.microsoft.com/) account.</span></span> <span data-ttu-id="bbf37-121">Vous pouvez commencer par une version d’ [essai gratuit](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bbf37-121">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="bbf37-122">Vous aurez besoin d’un stockage Azure compte toostore répliquée de données.</span><span class="sxs-lookup"><span data-stu-id="bbf37-122">You'll need an Azure storage account toostore replicated data.</span></span> <span data-ttu-id="bbf37-123">compte de Hello doit géo-réplication activée.</span><span class="sxs-lookup"><span data-stu-id="bbf37-123">hello account needs geo-replication enabled.</span></span> <span data-ttu-id="bbf37-124">Il doit être en hello même région que le coffre Azure Site Recovery hello et être associé hello même abonnement.</span><span class="sxs-lookup"><span data-stu-id="bbf37-124">It should be in hello same region as hello Azure Site Recovery vault and be associated with hello same subscription.</span></span> <span data-ttu-id="bbf37-125">[En savoir plus sur Azure Storage](../storage/common/storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="bbf37-125">[Learn more about Azure storage](../storage/common/storage-introduction.md).</span></span>
* <span data-ttu-id="bbf37-126">Vous devez toomake assurer que les ordinateurs virtuels que vous souhaitez tooprotect conformes [conditions préalables de machine virtuelle Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="bbf37-126">You'll need toomake sure that virtual machines you want tooprotect comply with [Azure virtual machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

### <a name="vmm-prerequisites"></a><span data-ttu-id="bbf37-127">Configuration requise pour VMM</span><span class="sxs-lookup"><span data-stu-id="bbf37-127">VMM prerequisites</span></span>
* <span data-ttu-id="bbf37-128">Vous aurez besoin d’un serveur VMM exécuté sur System Center 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="bbf37-128">You'll need  VMM server running on System Center 2012 R2.</span></span>
* <span data-ttu-id="bbf37-129">Vous devez au moins un cloud sur hello serveur VMM que vous souhaitez tooprotect.</span><span class="sxs-lookup"><span data-stu-id="bbf37-129">You'll need at least one cloud on hello VMM server you want tooprotect.</span></span> <span data-ttu-id="bbf37-130">cloud de Hello doit contenir :</span><span class="sxs-lookup"><span data-stu-id="bbf37-130">hello cloud should contain:</span></span>
  * <span data-ttu-id="bbf37-131">un ou plusieurs groupes hôtes VMM ;</span><span class="sxs-lookup"><span data-stu-id="bbf37-131">One or more VMM host groups.</span></span>
  * <span data-ttu-id="bbf37-132">un ou plusieurs serveurs hôtes Hyper-V ou clusters dans chaque groupe hôte ;</span><span class="sxs-lookup"><span data-stu-id="bbf37-132">One or more Hyper-V host servers or clusters in each host group .</span></span>
  * <span data-ttu-id="bbf37-133">Un ou plusieurs ordinateurs virtuels sur le serveur d’Hyper-V source hello.</span><span class="sxs-lookup"><span data-stu-id="bbf37-133">One or more virtual machines on hello source Hyper-V server.</span></span>

### <a name="hyper-v-prerequisites"></a><span data-ttu-id="bbf37-134">Conditions préalables liées à Hyper-V</span><span class="sxs-lookup"><span data-stu-id="bbf37-134">Hyper-V prerequisites</span></span>
* <span data-ttu-id="bbf37-135">Hello serveurs hôtes Hyper-V doivent être en cours d’exécution au moins **Windows Server 2012** avec le rôle Hyper-V ou **Microsoft Hyper-V Server 2012** et avez hello les dernières mises à jour installées.</span><span class="sxs-lookup"><span data-stu-id="bbf37-135">hello host Hyper-V servers must be running at least **Windows Server 2012** with Hyper-V role or **Microsoft Hyper-V Server 2012** and have hello latest updates installed.</span></span>
* <span data-ttu-id="bbf37-136">Si vous utilisez Hyper-V dans un cluster, notez que le service Broker du cluster n'est pas créé automatiquement si vous avez un cluster basé sur des adresses IP statiques.</span><span class="sxs-lookup"><span data-stu-id="bbf37-136">If you're running Hyper-V in a cluster note that cluster broker isn't created automatically if you have a static IP address-based cluster.</span></span> <span data-ttu-id="bbf37-137">Vous devez manuellement service broker de cluster tooconfigure hello.</span><span class="sxs-lookup"><span data-stu-id="bbf37-137">You'll need tooconfigure hello cluster broker manually.</span></span> <span data-ttu-id="bbf37-138">toodo cela, dans le Gestionnaire de serveur > Gestionnaire du Cluster de basculement, connectez toohello cluster, cliquez sur **configurer un rôle** et sélectionnez **Service Broker de réplication Hyper-V** Bonjour **sélectionner un rôle**écran de l’Assistant haute disponibilité de hello.</span><span class="sxs-lookup"><span data-stu-id="bbf37-138">toodo this, in Server Manager > Failover Cluster Manager, connect toohello cluster, click **Configure Role** and select **Hyper-V Replica Broker** in hello **Select Role** screen of hello High Availability wizard.</span></span>
* <span data-ttu-id="bbf37-139">N’importe quel serveur hôte Hyper-V ou le cluster dont vous voulez toomanage protection doit être inclus dans un cloud VMM.</span><span class="sxs-lookup"><span data-stu-id="bbf37-139">Any Hyper-V host server or cluster for which you want toomanage protection must be included in a VMM cloud.</span></span>

### <a name="network-mapping-prerequisites"></a><span data-ttu-id="bbf37-140">Conditions préalables liées au mappage réseau</span><span class="sxs-lookup"><span data-stu-id="bbf37-140">Network mapping prerequisites</span></span>
<span data-ttu-id="bbf37-141">Lorsque vous protégez des ordinateurs virtuels dans le mappage réseau Azure mappe entre les réseaux d’ordinateurs virtuels sur le serveur VMM de source hello et suivant de hello de tooenable de réseaux Azure cible :</span><span class="sxs-lookup"><span data-stu-id="bbf37-141">When you protect virtual machines in Azure network mapping maps between VM networks on hello source VMM server and target Azure networks tooenable hello following:</span></span>

* <span data-ttu-id="bbf37-142">Toutes les machines qui basculent sur hello même réseau peut se connecter tooeach autre, quel que soit le plan de récupération auquel elles sont dans.</span><span class="sxs-lookup"><span data-stu-id="bbf37-142">All machines which fail over on hello same network can connect tooeach other, irrespective of which recovery plan they are in.</span></span>
* <span data-ttu-id="bbf37-143">Si une passerelle de réseau est configurée sur le réseau Azure cible de hello, les machines virtuelles peuvent se connecter tooother locaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="bbf37-143">If a network gateway is setup on hello target Azure network, virtual machines can connect tooother on-premises virtual machines.</span></span>
* <span data-ttu-id="bbf37-144">Si vous ne configurez pas de réseau mappage seuls les ordinateurs virtuels qui basculent Bonjour même plan de récupération sera en mesure de tooconnect tooeach autres après basculement tooAzure.</span><span class="sxs-lookup"><span data-stu-id="bbf37-144">If you don’t configure network mapping only virtual machines that fail over in hello same recovery plan will be able tooconnect tooeach other after failover tooAzure.</span></span>

<span data-ttu-id="bbf37-145">Si vous souhaitez que le mappage réseau toodeploy, vous devez suivant de hello :</span><span class="sxs-lookup"><span data-stu-id="bbf37-145">If you want toodeploy network mapping you'll need hello following:</span></span>

* <span data-ttu-id="bbf37-146">Hello machines virtuelles tooprotect sur le serveur VMM de hello source doit être connecté tooa réseau d’ordinateurs virtuels.</span><span class="sxs-lookup"><span data-stu-id="bbf37-146">hello virtual machines you want tooprotect on hello source VMM server should be connected tooa VM network.</span></span> <span data-ttu-id="bbf37-147">Ce réseau doit être lié tooa réseau logique associé au cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="bbf37-147">That network should be linked tooa logical network that is associated with hello cloud.</span></span>
* <span data-ttu-id="bbf37-148">Un réseau de Azure toowhich répliquée d’ordinateurs virtuels peuvent se connecter après le basculement.</span><span class="sxs-lookup"><span data-stu-id="bbf37-148">An Azure network toowhich replicated virtual machines can connect after failover.</span></span> <span data-ttu-id="bbf37-149">Vous devez sélectionner ce réseau au moment du basculement de hello.</span><span class="sxs-lookup"><span data-stu-id="bbf37-149">You'll select this network at hello time of failover.</span></span> <span data-ttu-id="bbf37-150">réseau de Hello doivent se trouver dans hello même région que votre abonnement Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="bbf37-150">hello network should be in hello same region as your Azure Site Recovery subscription.</span></span>

### <a name="powershell-prerequisites"></a><span data-ttu-id="bbf37-151">Conditions préalables pour PowerShell</span><span class="sxs-lookup"><span data-stu-id="bbf37-151">PowerShell prerequisites</span></span>
<span data-ttu-id="bbf37-152">Assurez-vous que vous avez toogo prêt d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bbf37-152">Make sure you have Azure PowerShell ready toogo.</span></span> <span data-ttu-id="bbf37-153">Si vous utilisez déjà PowerShell, vous devez tooupgrade tooversion 0.8.10 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="bbf37-153">If you are already using PowerShell, you'll need tooupgrade tooversion 0.8.10 or later.</span></span> <span data-ttu-id="bbf37-154">Pour plus d’informations sur la configuration de PowerShell, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="bbf37-154">For information about setting up PowerShell, see [How tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="bbf37-155">Après avoir configuré et configuré de PowerShell, vous pouvez afficher toutes les hello des applets de commande disponibles pour le service de hello [ici](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="bbf37-155">Once you have set up and configured PowerShell, you can view all of hello available cmdlets for hello service [here](/powershell/azure/overview).</span></span>

<span data-ttu-id="bbf37-156">toolearn sur les conseils qui peuvent vous aider à utiliser des applets de commande hello, telles que la façon dont les valeurs de paramètre, les entrées et sorties sont généralement gérées dans Azure PowerShell, consultez [prise en main des applets de commande Azure](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="bbf37-156">toolearn about tips that can help you use hello cmdlets, such as how parameter values, inputs, and outputs are typically handled in Azure PowerShell, see [Get Started with Azure Cmdlets](/powershell/azure/get-started-azureps).</span></span>

## <a name="step-1-set-hello-subscription"></a><span data-ttu-id="bbf37-157">Étape 1 : Définir l’abonnement de hello</span><span class="sxs-lookup"><span data-stu-id="bbf37-157">Step 1: Set hello subscription</span></span>
<span data-ttu-id="bbf37-158">Dans PowerShell, exécutez ces applets de commande :</span><span class="sxs-lookup"><span data-stu-id="bbf37-158">In PowerShell, run these cmdlets:</span></span>

```
$UserName = "<user@live.com>"
$Password = "<password>"
$AzureSubscriptionName = "prod_sub1"

$SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
$Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $securePassword
Add-AzureAccount -Credential $Cred;
$AzureSubscription = Select-AzureSubscription -SubscriptionName $AzureSubscriptionName

```

<span data-ttu-id="bbf37-159">Remplacez les éléments hello hello « < > » avec des informations spécifiques à votre.</span><span class="sxs-lookup"><span data-stu-id="bbf37-159">Replace hello elements within hello "< >" with your specific information.</span></span>

## <a name="step-2-create-a-site-recovery-vault"></a><span data-ttu-id="bbf37-160">Étape 2 : Création d’un coffre Site Recovery</span><span class="sxs-lookup"><span data-stu-id="bbf37-160">Step 2: Create a Site Recovery vault</span></span>
<span data-ttu-id="bbf37-161">Dans PowerShell, remplacer les éléments de hello dans hello « < > » avec des informations spécifiques et exécuter ces commandes :</span><span class="sxs-lookup"><span data-stu-id="bbf37-161">In PowerShell, replace hello elements within hello "< >" with your specific information, and run these commands:</span></span>

```

$VaultName = "<testvault123>"
$VaultGeo  = "<Southeast Asia>"
$OutputPathForSettingsFile = "<c:\>"

```


```
New-AzureSiteRecoveryVault -Location $VaultGeo -Name $VaultName;
$vault = Get-AzureSiteRecoveryVault -Name $VaultName;

```

## <a name="step-3-generate-a-vault-registration-key"></a><span data-ttu-id="bbf37-162">Étape 3 : Génération d’une clé d'inscription du coffre</span><span class="sxs-lookup"><span data-stu-id="bbf37-162">Step 3: Generate a vault registration key</span></span>
<span data-ttu-id="bbf37-163">Générer une clé d’inscription dans le coffre hello.</span><span class="sxs-lookup"><span data-stu-id="bbf37-163">Generate a registration key in hello vault.</span></span> <span data-ttu-id="bbf37-164">Une fois que vous téléchargez hello fournisseur Azure Site Recovery et l’installer sur le serveur VMM de hello, vous allez utiliser ce serveur VMM de hello tooregister clé dans le coffre hello.</span><span class="sxs-lookup"><span data-stu-id="bbf37-164">After you download hello Azure Site Recovery Provider and install it on hello VMM server, you'll use this key tooregister hello VMM server in hello vault.</span></span>

1. <span data-ttu-id="bbf37-165">Obtenir le fichier de paramètres de coffre hello et définir le contexte de hello :</span><span class="sxs-lookup"><span data-stu-id="bbf37-165">Get hello vault setting file and set hello context:</span></span>

   ```

   $VaultName = "<testvault123>"
   $VaultGeo  = "<Southeast Asia>"
   $OutputPathForSettingsFile = "<c:\>"

   $VaultSetingsFile = Get-AzureSiteRecoveryVaultSettingsFile -Location $VaultGeo -Name $VaultName -Path $OutputPathForSettingsFile;

   ```
2. <span data-ttu-id="bbf37-166">Définir le contexte de coffre hello en hello suivant les commandes en cours d’exécution :</span><span class="sxs-lookup"><span data-stu-id="bbf37-166">Set hello vault context by running hello following commands:</span></span>

   ```

   $VaultSettingFilePath = $vaultSetingsFile.FilePath
   $VaultContext = Import-AzureSiteRecoveryVaultSettingsFile -Path $VaultSettingFilePath -ErrorAction Stop

   ```

## <a name="step-4-install-hello-azure-site-recovery-provider"></a><span data-ttu-id="bbf37-167">Étape 4 : Installer hello fournisseur Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="bbf37-167">Step 4: Install hello Azure Site Recovery Provider</span></span>
1. <span data-ttu-id="bbf37-168">Sur l’ordinateur VMM hello, créez un répertoire en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="bbf37-168">On hello VMM machine, create a directory by running hello following command:</span></span>

   ```

   pushd C:\ASR\

   ```
2. <span data-ttu-id="bbf37-169">Extrayez les fichiers hello à l’aide de fournisseur de hello téléchargé en exécutant hello commande suivante</span><span class="sxs-lookup"><span data-stu-id="bbf37-169">Extract hello files using hello downloaded provider by running hello following command</span></span>

   ```

   AzureSiteRecoveryProvider.exe /x:. /q

   ```
3. <span data-ttu-id="bbf37-170">Installez le fournisseur hello hello suivant les commandes à l’aide de :</span><span class="sxs-lookup"><span data-stu-id="bbf37-170">Install hello provider using hello following commands:</span></span>

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

   <span data-ttu-id="bbf37-171">Attendez que hello installation toofinish.</span><span class="sxs-lookup"><span data-stu-id="bbf37-171">Wait for hello installation toofinish.</span></span>
4. <span data-ttu-id="bbf37-172">Inscrire un serveur hello dans le coffre de hello à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="bbf37-172">Register hello server in hello vault using hello following command:</span></span>

   ```

   $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
   pushd $BinPath
   $encryptionFilePath = "C:\temp\"
   .\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

   ```

## <a name="step-5-create-an-azure-storage-account"></a><span data-ttu-id="bbf37-173">Étape 5 : Création d’un compte de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="bbf37-173">Step 5: Create an Azure storage account</span></span>
<span data-ttu-id="bbf37-174">Si vous n’avez pas un compte de stockage Azure, créez un compte de géo-réplication activée en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="bbf37-174">If you don't have an Azure storage account, create a geo-replication enabled account by running hello following command:</span></span>

```

$StorageAccountName = "teststorageacc1"
$StorageAccountGeo  = "Southeast Asia"

New-AzureStorageAccount -StorageAccountName $StorageAccountName -Label $StorageAccountName -Location $StorageAccountGeo;

```

<span data-ttu-id="bbf37-175">Notez que le compte de stockage hello doit être en hello même région que le service d’Azure Site Recovery hello et être associé à hello même abonnement.</span><span class="sxs-lookup"><span data-stu-id="bbf37-175">Note that hello storage account must be in hello same region as hello Azure Site Recovery service, and be associated with hello same subscription.</span></span>

## <a name="step-6-install-hello-azure-recovery-services-agent"></a><span data-ttu-id="bbf37-176">Étape 6 : Installer hello Azure Recovery Services Agent</span><span class="sxs-lookup"><span data-stu-id="bbf37-176">Step 6: Install hello Azure Recovery Services Agent</span></span>
<span data-ttu-id="bbf37-177">À partir de hello portail Azure, installation Bonjour Azure Recovery Services agent sur chaque serveur hôte de Hyper-V située dans des clouds VMM hello souhaité tooprotect.</span><span class="sxs-lookup"><span data-stu-id="bbf37-177">From hello Azure portal, install hello Azure Recovery Services agent on each Hyper-V host server located in hello VMM clouds you want tooprotect.</span></span>

<span data-ttu-id="bbf37-178">Exécutez hello commande suivante sur tous les hôtes VMM :</span><span class="sxs-lookup"><span data-stu-id="bbf37-178">Run hello following command on all VMM hosts:</span></span>

```

marsagentinstaller.exe /q /nu

```


## <a name="step-7-configure-cloud-protection-settings"></a><span data-ttu-id="bbf37-179">Étape 7 : Configuration des paramètres de protection de cloud</span><span class="sxs-lookup"><span data-stu-id="bbf37-179">Step 7: Configure cloud protection settings</span></span>
1. <span data-ttu-id="bbf37-180">Créer un tooAzure de profil de protection de cloud en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="bbf37-180">Create a cloud protection profile tooAzure by running hello following command:</span></span>

   ```

   $ReplicationFrequencyInSeconds = "300";
   $ProfileResult = New-AzureSiteRecoveryProtectionProfileObject -ReplicationProvider HyperVReplica -RecoveryAzureSubscription $AzureSubscriptionName -RecoveryAzureStorageAccount $StorageAccountName -ReplicationFrequencyInSeconds     $ReplicationFrequencyInSeconds;

   ```
2. <span data-ttu-id="bbf37-181">Pour obtenir un conteneur de protection, hello suivant les commandes en cours d’exécution :</span><span class="sxs-lookup"><span data-stu-id="bbf37-181">Get a protection container by running hello following commands:</span></span>

   ```

   $PrimaryCloud = "testcloud"
   $protectionContainer = Get-AzureSiteRecoveryProtectionContainer -Name $PrimaryCloud;

   ```
3. <span data-ttu-id="bbf37-182">Démarrer l’association hello du conteneur de protection hello avec le cloud de hello :</span><span class="sxs-lookup"><span data-stu-id="bbf37-182">Start hello association of hello protection container with hello cloud:</span></span>

   ```

   $associationJob = Start-AzureSiteRecoveryProtectionProfileAssociationJob -ProtectionProfile $profileResult -PrimaryProtectionContainer $protectionContainer;        

   ```
4. <span data-ttu-id="bbf37-183">Une fois le travail de hello terminée, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="bbf37-183">After hello job has finished, run hello following command:</span></span>

        $job = Get-AzureSiteRecoveryJob -Id $associationJob.JobId;
        if($job -eq $null -or $job.StateDescription -ne "Completed")
        {
        $isJobLeftForProcessing = $true;
        }


1. <span data-ttu-id="bbf37-184">Une fois le travail de hello a terminé le traitement, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="bbf37-184">After hello job has finished processing, run hello following command:</span></span>

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



<span data-ttu-id="bbf37-185">achèvement de hello toocheck d’opération de hello, suivez les étapes de hello dans [surveiller l’activité](#monitor).</span><span class="sxs-lookup"><span data-stu-id="bbf37-185">toocheck hello completion of hello operation, follow hello steps in [Monitor Activity](#monitor).</span></span>

## <a name="step-8-configure-network-mapping"></a><span data-ttu-id="bbf37-186">Étape 8 : Configuration du mappage réseau</span><span class="sxs-lookup"><span data-stu-id="bbf37-186">Step 8: Configure network mapping</span></span>
<span data-ttu-id="bbf37-187">Avant de commencer le mappage réseau Vérifiez que les ordinateurs virtuels sur le serveur VMM de hello source sont connectés tooa réseau d’ordinateurs virtuels.</span><span class="sxs-lookup"><span data-stu-id="bbf37-187">Before you begin network mapping verify that virtual machines on hello source VMM server are connected tooa VM network.</span></span> <span data-ttu-id="bbf37-188">En outre, vous devez créer un ou plusieurs réseaux virtuels Azure.</span><span class="sxs-lookup"><span data-stu-id="bbf37-188">In addition, create one or more Azure virtual networks.</span></span> <span data-ttu-id="bbf37-189">Notez que plusieurs réseaux d’ordinateurs virtuels peuvent être mappés tooa réseau Azure unique.</span><span class="sxs-lookup"><span data-stu-id="bbf37-189">Note that multiple VM networks can be mapped tooa single Azure network.</span></span>

<span data-ttu-id="bbf37-190">Notez que si le réseau cible de hello possède plusieurs sous-réseaux et d’un de ces sous-réseaux a hello trouve du même nom que le sous-réseau sur lequel hello source virtual machine, puis hello ordinateur virtuel sera connecté toothat cible sous-réseau après le basculement.</span><span class="sxs-lookup"><span data-stu-id="bbf37-190">Note that if hello target network has multiple subnets and one of those subnets has hello same name as subnet on which hello source virtual machine is located, then hello replica virtual machine will be connected toothat target subnet after failover.</span></span> <span data-ttu-id="bbf37-191">S’il n’est pas un sous-réseau cible avec un nom correspondant, ordinateur virtuel de hello sera connecté toohello premier sous-réseau de réseau de hello.</span><span class="sxs-lookup"><span data-stu-id="bbf37-191">If there is not a target subnet with a matching name, hello virtual machine will be connected toohello first subnet in hello network.</span></span>

<span data-ttu-id="bbf37-192">Hello première commande Obtient les serveurs pour le coffre Azure Site Recovery en cours hello.</span><span class="sxs-lookup"><span data-stu-id="bbf37-192">hello first command gets servers for hello current Azure Site Recovery vault.</span></span> <span data-ttu-id="bbf37-193">commande Hello stocke les serveurs Microsoft Azure Site Recovery hello dans la variable de tableau hello $Servers.</span><span class="sxs-lookup"><span data-stu-id="bbf37-193">hello command stores hello Microsoft Azure Site Recovery servers in hello $Servers array variable.</span></span>

    $Servers = Get-AzureSiteRecoveryServer


<span data-ttu-id="bbf37-194">commande deuxième Hello obtient réseau de récupération de site hello pour le premier serveur de hello hello $Servers tableau.</span><span class="sxs-lookup"><span data-stu-id="bbf37-194">hello second command gets hello site recovery network for hello first server in hello $Servers array.</span></span> <span data-ttu-id="bbf37-195">commande Hello stocke des réseaux de hello dans la variable de hello $Networks.</span><span class="sxs-lookup"><span data-stu-id="bbf37-195">hello command stores hello networks in hello $Networks variable.</span></span>

    $Networks = Get-AzureSiteRecoveryNetwork -Server $Servers[0]

<span data-ttu-id="bbf37-196">commande troisième Hello Obtient de vos abonnements Azure à l’aide d’applet de commande Get-AzureSubscription de hello, puis stocke cette valeur dans la variable de hello $Subscriptions.</span><span class="sxs-lookup"><span data-stu-id="bbf37-196">hello third command gets your Azure subscriptions by using hello Get-AzureSubscription cmdlet, and then stores that value in hello $Subscriptions variable.</span></span>

    $Subscriptions = Get-AzureSubscription



<span data-ttu-id="bbf37-197">Hello quatrième commande récupère les réseaux virtuels Azure à l’aide d’applet de commande Get-AzureVNetSite de hello et ensuite cette valeur dans la variable de hello $AzureVmNetworks.</span><span class="sxs-lookup"><span data-stu-id="bbf37-197">hello fourth command gets Azure virtual networks by using hello Get-AzureVNetSite cmdlet, and then that value in hello $AzureVmNetworks variable.</span></span>

    $AzureVmNetworks = Get-AzureVNetSite



<span data-ttu-id="bbf37-198">applet de commande finale Hello crée un mappage entre le réseau principal de hello et réseau de machine virtuelle Azure hello.</span><span class="sxs-lookup"><span data-stu-id="bbf37-198">hello final cmdlet creates a mapping between hello primary network and hello Azure virtual machine network.</span></span> <span data-ttu-id="bbf37-199">applet de commande Hello Spécifie le réseau principal de hello en tant que premier élément de hello de $Networks.</span><span class="sxs-lookup"><span data-stu-id="bbf37-199">hello cmdlet specifies hello primary network as hello first element of $Networks.</span></span> <span data-ttu-id="bbf37-200">applet de commande Hello spécifie un réseau d’ordinateurs virtuels en tant que premier élément de hello de $AzureVmNetworks à l’aide de son ID.</span><span class="sxs-lookup"><span data-stu-id="bbf37-200">hello cmdlet specifies a virtual machine network as hello first element of $AzureVmNetworks by using its ID.</span></span> <span data-ttu-id="bbf37-201">commande Hello inclut votre ID d’abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="bbf37-201">hello command includes your Azure subscription ID.</span></span>

    New-AzureSiteRecoveryNetworkMapping -PrimaryNetwork $Networks[0] -AzureSubscriptionId $Subscriptions[0].SubscriptionId -AzureVMNetworkId $AzureVmNetworks[0].Id


## <a name="step-9-enable-protection-for-virtual-machines"></a><span data-ttu-id="bbf37-202">Étape 9 : Activation de la protection des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="bbf37-202">Step 9: Enable protection for virtual machines</span></span>
<span data-ttu-id="bbf37-203">Une fois les serveurs, les clouds et les réseaux configurés, vous pouvez activer la protection des machines virtuelles dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="bbf37-203">After servers, clouds, and networks are configured correctly, you can enable protection for virtual machines in hello cloud.</span></span> <span data-ttu-id="bbf37-204">Notez hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="bbf37-204">Note hello following:</span></span>

<span data-ttu-id="bbf37-205">Les machines virtuelles doivent répondre à la [configuration requise pour les machines virtuelles Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="bbf37-205">Virtual machines must meet [Azure virtual machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

<span data-ttu-id="bbf37-206">système d’exploitation de tooenable protection hello et les propriétés de disque de système d’exploitation doivent être définies pour la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="bbf37-206">tooenable protection hello operating system and operating system disk properties must be set for hello virtual machine.</span></span> <span data-ttu-id="bbf37-207">Lorsque vous créez un ordinateur virtuel dans VMM à l’aide d’un modèle d’ordinateur virtuel, vous pouvez définir la propriété de hello.</span><span class="sxs-lookup"><span data-stu-id="bbf37-207">When you create a virtual machine in VMM using a virtual machine template you can set hello property.</span></span> <span data-ttu-id="bbf37-208">Vous pouvez également définir ces propriétés pour les ordinateurs virtuels existants sur hello **général** et **Configuration matérielle** onglets des propriétés d’ordinateur virtuel hello.</span><span class="sxs-lookup"><span data-stu-id="bbf37-208">You can also set these properties for existing virtual machines on hello **General** and **Hardware Configuration** tabs of hello virtual machine properties.</span></span> <span data-ttu-id="bbf37-209">Si vous ne définissez pas ces propriétés dans VMM, vous serez en mesure de tooconfigure dans le portail Azure Site Recovery hello.</span><span class="sxs-lookup"><span data-stu-id="bbf37-209">If you don't set these properties in VMM you'll be able tooconfigure them in hello Azure Site Recovery portal.</span></span>

1. <span data-ttu-id="bbf37-210">protection de tooenable, exécutez hello suivant du conteneur de protection de commande tooget hello :</span><span class="sxs-lookup"><span data-stu-id="bbf37-210">tooenable protection, run hello following command tooget hello protection container:</span></span>

     <span data-ttu-id="bbf37-211">$ProtectionContainer = Get-AzureSiteRecoveryProtectionContainer -Name $CloudName</span><span class="sxs-lookup"><span data-stu-id="bbf37-211">$ProtectionContainer = Get-AzureSiteRecoveryProtectionContainer -Name $CloudName</span></span>
2. <span data-ttu-id="bbf37-212">Obtenir l’entité de protection hello (VM) en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="bbf37-212">Get hello protection entity (VM) by running hello following command:</span></span>

        $protectionEntity = Get-AzureSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer



1. <span data-ttu-id="bbf37-213">Activer hello récupération d’urgence pour hello machine virtuelle en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="bbf37-213">Enable hello DR for hello VM by running hello following command:</span></span>

        $jobResult = Set-AzureSiteRecoveryProtectionEntity -ProtectionEntity $protectionEntity     -Protection Enable -Force



## <a name="test-your-deployment"></a><span data-ttu-id="bbf37-214">Tester votre déploiement</span><span class="sxs-lookup"><span data-stu-id="bbf37-214">Test your deployment</span></span>
<span data-ttu-id="bbf37-215">planification de votre déploiement, vous pouvez exécuter un test de basculement pour une seule machine virtuelle, ou créer un plan de récupération composé de plusieurs ordinateurs virtuels et exécuter un test de basculement pour hello tootest.</span><span class="sxs-lookup"><span data-stu-id="bbf37-215">tootest your deployment you can run a test failover for a single virtual machine, or create a recovery plan consisting of multiple virtual machines and run a test failover for hello plan.</span></span> <span data-ttu-id="bbf37-216">Il simule votre mécanisme de basculement et de récupération dans un réseau isolé.</span><span class="sxs-lookup"><span data-stu-id="bbf37-216">Test failover simulates your failover and recovery mechanism in an isolated network.</span></span> <span data-ttu-id="bbf37-217">Notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="bbf37-217">Note that:</span></span>

* <span data-ttu-id="bbf37-218">Si vous souhaitez tooconnect toohello machine virtuelle Azure à l’aide du Bureau à distance après le basculement de hello, activer la connexion Bureau à distance sur l’ordinateur virtuel de hello avant d’exécuter le test de basculement hello.</span><span class="sxs-lookup"><span data-stu-id="bbf37-218">If you want tooconnect toohello virtual machine in Azure using Remote Desktop after hello failover, enable Remote Desktop Connection on hello virtual machine before you run hello test failover.</span></span>
* <span data-ttu-id="bbf37-219">Après le basculement, vous allez utiliser un ordinateur virtuel toohello de publique IP adresse tooconnect dans Azure à l’aide du Bureau à distance.</span><span class="sxs-lookup"><span data-stu-id="bbf37-219">After failover, you'll use a public IP address tooconnect toohello virtual machine in Azure using Remote Desktop.</span></span> <span data-ttu-id="bbf37-220">Si vous voulez toodo, assurez-vous que vous n’avez pas les stratégies de domaine qui vous empêchent de connexion tooa machine virtuelle une adresse publique.</span><span class="sxs-lookup"><span data-stu-id="bbf37-220">If you want toodo this, ensure you don't have any domain policies that prevent you from connecting tooa virtual machine using a public address.</span></span>

<span data-ttu-id="bbf37-221">achèvement de hello toocheck d’opération de hello, suivez les étapes de hello dans [surveiller l’activité](#monitor).</span><span class="sxs-lookup"><span data-stu-id="bbf37-221">toocheck hello completion of hello operation, follow hello steps in [Monitor Activity](#monitor).</span></span>

### <a name="create-a-recovery-plan"></a><span data-ttu-id="bbf37-222">Créer un plan de récupération</span><span class="sxs-lookup"><span data-stu-id="bbf37-222">Create a recovery plan</span></span>
1. <span data-ttu-id="bbf37-223">Créer un fichier .xml comme modèle pour votre plan de récupération à l’aide de données hello ci-dessous, puis enregistrez-le en tant que « C:\RPTemplatePath.xml ».</span><span class="sxs-lookup"><span data-stu-id="bbf37-223">Create an .xml file as a template for your recovery plan using hello data below, and then save it as "C:\RPTemplatePath.xml".</span></span>
2. <span data-ttu-id="bbf37-224">Modifier l’Id de nœud RecoveryPlan hello, nom, PrimaryServerId et SecondaryServerId.</span><span class="sxs-lookup"><span data-stu-id="bbf37-224">Change hello RecoveryPlan node Id, Name, PrimaryServerId, and SecondaryServerId.</span></span>
3. <span data-ttu-id="bbf37-225">Modifier le nœud de ProtectionEntity hello PrimaryProtectionEntityId (vmid de VMM).</span><span class="sxs-lookup"><span data-stu-id="bbf37-225">Change hello ProtectionEntity node PrimaryProtectionEntityId (vmid from VMM).</span></span>
4. <span data-ttu-id="bbf37-226">Vous pouvez ajouter davantage de machines virtuelles en ajoutant des nœuds ProtectionEntity.</span><span class="sxs-lookup"><span data-stu-id="bbf37-226">You can add more VMs by adding more ProtectionEntity nodes.</span></span>

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



1. <span data-ttu-id="bbf37-227">Renseignez les données de salutation dans le modèle de hello :</span><span class="sxs-lookup"><span data-stu-id="bbf37-227">Fill in hello data in hello template:</span></span>

        $TemplatePath = "C:\RPTemplatePath.xml";



1. <span data-ttu-id="bbf37-228">Créer hello RecoveryPlan :</span><span class="sxs-lookup"><span data-stu-id="bbf37-228">Create hello RecoveryPlan:</span></span>

        $RPCreationJob = New-AzureSiteRecoveryRecoveryPlan -File $TemplatePath -WaitForCompletion;

### <a name="run-a-test-failover"></a><span data-ttu-id="bbf37-229">Exécution d’un test de basculement</span><span class="sxs-lookup"><span data-stu-id="bbf37-229">Run a test failover</span></span>
1. <span data-ttu-id="bbf37-230">Obtenir l’objet de RecoveryPlan hello en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="bbf37-230">Get hello RecoveryPlan object by running hello following command:</span></span>

     <span data-ttu-id="bbf37-231">$RPObject = Get-AzureSiteRecoveryRecoveryPlan -Name $RPName;</span><span class="sxs-lookup"><span data-stu-id="bbf37-231">$RPObject = Get-AzureSiteRecoveryRecoveryPlan -Name $RPName;</span></span>
2. <span data-ttu-id="bbf37-232">Démarrez hello test de basculement en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="bbf37-232">Start hello test failover by running hello following command:</span></span>

        $jobIDResult = Start-AzureSiteRecoveryTestFailoverJob -RecoveryPlan $RPObject -Direction PrimaryToRecovery;


## <span data-ttu-id="bbf37-233"><a name=monitor></a> Suivi de l'activité</span><span class="sxs-lookup"><span data-stu-id="bbf37-233"><a name=monitor></a> Monitor Activity</span></span>
<span data-ttu-id="bbf37-234">Utilisez hello suivant l’activité de commandes toomonitor hello.</span><span class="sxs-lookup"><span data-stu-id="bbf37-234">Use hello following commands toomonitor hello activity.</span></span> <span data-ttu-id="bbf37-235">Notez que vous avez toowait entre les travaux pour hello traitement toofinish.</span><span class="sxs-lookup"><span data-stu-id="bbf37-235">Note that you have toowait in between jobs for hello processing toofinish.</span></span>

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



## <a name="next-steps"></a><span data-ttu-id="bbf37-236">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bbf37-236">Next steps</span></span>
<span data-ttu-id="bbf37-237">[Découvrez plus](/powershell/azure/overview) d'informations sur les applets de commande PowerShell Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="bbf37-237">[Read more](/powershell/azure/overview) about Azure Site Recovery PowerShell cmdlets.</span></span> <span data-ttu-id="bbf37-238"></a>.</span><span class="sxs-lookup"><span data-stu-id="bbf37-238"></a>.</span></span>
