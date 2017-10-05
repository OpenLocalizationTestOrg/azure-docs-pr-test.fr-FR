---
title: "Répliquer des machines virtuelles Hyper-V sur Azure dans le portail Classic avec PowerShell | Microsoft Docs"
description: "Automatiser la réplication de machines virtuelles Hyper-V dans des clouds VMM à l’aide de Site Recovery et de PowerShell dans le portail Classic"
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
ms.openlocfilehash: 581daaaa5cc0cf8be782f834c6bdb3f27ee413fb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="replicate-hyper-v-vms-to-azure-with-powershell-in-the-classic-portal"></a><span data-ttu-id="2d110-103">Répliquer des machines virtuelles Hyper-V sur Azure avec PowerShell dans le portail Classic</span><span class="sxs-lookup"><span data-stu-id="2d110-103">Replicate Hyper-V VMs to Azure with PowerShell in the classic portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2d110-104">portail Azure</span><span class="sxs-lookup"><span data-stu-id="2d110-104">Azure Portal</span></span>](site-recovery-vmm-to-azure.md)
> * [<span data-ttu-id="2d110-105">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2d110-105">PowerShell - Resource Manager</span></span>](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [<span data-ttu-id="2d110-106">Portail Classic</span><span class="sxs-lookup"><span data-stu-id="2d110-106">Classic Portal</span></span>](site-recovery-vmm-to-azure-classic.md)
> * [<span data-ttu-id="2d110-107">PowerShell - Classique</span><span class="sxs-lookup"><span data-stu-id="2d110-107">PowerShell - Classic</span></span>](site-recovery-deploy-with-powershell.md)
>
>

## <a name="overview"></a><span data-ttu-id="2d110-108">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="2d110-108">Overview</span></span>
<span data-ttu-id="2d110-109">Azure Site Recovery contribue à mettre en œuvre la stratégie de continuité des activités et de récupération d'urgence de votre entreprise en coordonnant la réplication, le basculement et la récupération de machines virtuelles dans divers scénarios de déploiement.</span><span class="sxs-lookup"><span data-stu-id="2d110-109">Azure Site Recovery contributes to your business continuity and disaster recovery (BCDR) strategy by orchestrating replication, failover and recovery of virtual machines in a number of deployment scenarios.</span></span> <span data-ttu-id="2d110-110">Pour obtenir la liste complète des scénarios de déploiement, consultez la [Vue d’ensemble d’Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2d110-110">For a full list of deployment scenarios see the [Azure Site Recovery overview](site-recovery-overview.md).</span></span>

<span data-ttu-id="2d110-111">Cet article vous montre comment utiliser PowerShell pour automatiser les tâches courantes à effectuer lorsque vous configurez Azure Site Recovery pour répliquer des machines virtuelles Hyper-V dans des clouds System Center VMM vers le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="2d110-111">This article shows you how to use PowerShell to automate common tasks you need to perform when you set up Azure Site Recovery to replicate Hyper-V virtual machines in System Center VMM clouds to Azure storage.</span></span>

<span data-ttu-id="2d110-112">L’article indique les conditions prérequises pour le scénario et montre comment configurer un coffre Récupération de sites, installer le fournisseur Azure Site Recovery sur le serveur VMM source, inscrire le serveur dans le coffre, ajouter un compte de stockage Azure, installer l'agent Azure Recovery Services sur les serveurs hôtes Hyper-V, configurer les paramètres de protection des clouds VMM qui seront appliqués à toutes les machines virtuelles protégées, puis activer la protection pour ces machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="2d110-112">The article includes prerequisites for the scenario, and shows you how to set up a Site Recovery vault, install the Azure Site Recovery Provider on the source VMM server, register the server in the vault, add an Azure storage account, install the Azure Recovery Services agent on Hyper-V host servers, configure protection settings for VMM clouds that will be applied to all protected virtual machines, and then enable protection for those virtual machines.</span></span> <span data-ttu-id="2d110-113">Pour finir, vous pourrez tester le basculement pour vous assurer que tout fonctionne comme prévu.</span><span class="sxs-lookup"><span data-stu-id="2d110-113">Finish up by testing the failover to make sure everything's working as expected.</span></span>

<span data-ttu-id="2d110-114">Si vous rencontrez des problèmes pour mettre en œuvre ce scénario, posez vos questions sur le [Forum Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="2d110-114">If you run into problems setting up this scenario, post your questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

> [!NOTE]
> <span data-ttu-id="2d110-115">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="2d110-115">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="2d110-116">Cet article traite du modèle de déploiement classique.</span><span class="sxs-lookup"><span data-stu-id="2d110-116">This article covers using the Classic deployment model.</span></span>
>
>

## <a name="before-you-start"></a><span data-ttu-id="2d110-117">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="2d110-117">Before you start</span></span>
<span data-ttu-id="2d110-118">Assurez-vous que les conditions préalables sont remplies :</span><span class="sxs-lookup"><span data-stu-id="2d110-118">Make sure you have these prerequisites in place:</span></span>

### <a name="azure-prerequisites"></a><span data-ttu-id="2d110-119">Conditions préalables pour Azure</span><span class="sxs-lookup"><span data-stu-id="2d110-119">Azure prerequisites</span></span>
* <span data-ttu-id="2d110-120">Vous aurez besoin d’un compte [Microsoft Azure](https://azure.microsoft.com/) .</span><span class="sxs-lookup"><span data-stu-id="2d110-120">You'll need a [Microsoft Azure](https://azure.microsoft.com/) account.</span></span> <span data-ttu-id="2d110-121">Vous pouvez commencer par une version d’ [essai gratuit](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2d110-121">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="2d110-122">Vous aurez besoin d’un compte de stockage Azure pour stocker les données répliquées.</span><span class="sxs-lookup"><span data-stu-id="2d110-122">You'll need an Azure storage account to store replicated data.</span></span> <span data-ttu-id="2d110-123">La géo-réplication doit être activée pour ce compte.</span><span class="sxs-lookup"><span data-stu-id="2d110-123">The account needs geo-replication enabled.</span></span> <span data-ttu-id="2d110-124">Il doit se trouver dans la même région que le coffre Azure Site Recovery et être associé au même abonnement.</span><span class="sxs-lookup"><span data-stu-id="2d110-124">It should be in the same region as the Azure Site Recovery vault and be associated with the same subscription.</span></span> <span data-ttu-id="2d110-125">[En savoir plus sur Azure Storage](../storage/common/storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2d110-125">[Learn more about Azure storage](../storage/common/storage-introduction.md).</span></span>
* <span data-ttu-id="2d110-126">Vous devez vous assurer que les machines virtuelles que vous souhaitez protéger sont conformes à la [configuration requise pour les machines virtuelle Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="2d110-126">You'll need to make sure that virtual machines you want to protect comply with [Azure virtual machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

### <a name="vmm-prerequisites"></a><span data-ttu-id="2d110-127">Configuration requise pour VMM</span><span class="sxs-lookup"><span data-stu-id="2d110-127">VMM prerequisites</span></span>
* <span data-ttu-id="2d110-128">Vous aurez besoin d’un serveur VMM exécuté sur System Center 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="2d110-128">You'll need  VMM server running on System Center 2012 R2.</span></span>
* <span data-ttu-id="2d110-129">Vous aurez besoin d'au moins un cloud sur le serveur VMM que vous souhaitez protéger.</span><span class="sxs-lookup"><span data-stu-id="2d110-129">You'll need at least one cloud on the VMM server you want to protect.</span></span> <span data-ttu-id="2d110-130">Le coud doit contenir :</span><span class="sxs-lookup"><span data-stu-id="2d110-130">The cloud should contain:</span></span>
  * <span data-ttu-id="2d110-131">un ou plusieurs groupes hôtes VMM ;</span><span class="sxs-lookup"><span data-stu-id="2d110-131">One or more VMM host groups.</span></span>
  * <span data-ttu-id="2d110-132">un ou plusieurs serveurs hôtes Hyper-V ou clusters dans chaque groupe hôte ;</span><span class="sxs-lookup"><span data-stu-id="2d110-132">One or more Hyper-V host servers or clusters in each host group .</span></span>
  * <span data-ttu-id="2d110-133">une ou plusieurs machines virtuelles sur le serveur Hyper-V source.</span><span class="sxs-lookup"><span data-stu-id="2d110-133">One or more virtual machines on the source Hyper-V server.</span></span>

### <a name="hyper-v-prerequisites"></a><span data-ttu-id="2d110-134">Conditions préalables liées à Hyper-V</span><span class="sxs-lookup"><span data-stu-id="2d110-134">Hyper-V prerequisites</span></span>
* <span data-ttu-id="2d110-135">Les serveurs hôtes Hyper-V doivent exécuter au moins **Windows Server 2012** avec le rôle Hyper-V ou **Microsoft Hyper-V Server 2012** et les dernières mises à jour doivent être installées.</span><span class="sxs-lookup"><span data-stu-id="2d110-135">The host Hyper-V servers must be running at least **Windows Server 2012** with Hyper-V role or **Microsoft Hyper-V Server 2012** and have the latest updates installed.</span></span>
* <span data-ttu-id="2d110-136">Si vous utilisez Hyper-V dans un cluster, notez que le service Broker du cluster n'est pas créé automatiquement si vous avez un cluster basé sur des adresses IP statiques.</span><span class="sxs-lookup"><span data-stu-id="2d110-136">If you're running Hyper-V in a cluster note that cluster broker isn't created automatically if you have a static IP address-based cluster.</span></span> <span data-ttu-id="2d110-137">Vous devez configurer manuellement le service Broker du cluster.</span><span class="sxs-lookup"><span data-stu-id="2d110-137">You'll need to configure the cluster broker manually.</span></span> <span data-ttu-id="2d110-138">Pour ce faire, dans le Gestionnaire de serveur > Gestionnaire du cluster de basculement, connectez-vous au cluster, cliquez sur **Configurer un rôle** et sélectionnez **Service Broker de réplication Hyper-V** dans l’écran **Sélectionner un rôle** de l’Assistant Haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="2d110-138">To do this, in Server Manager > Failover Cluster Manager, connect to the cluster, click **Configure Role** and select **Hyper-V Replica Broker** in the **Select Role** screen of the High Availability wizard.</span></span>
* <span data-ttu-id="2d110-139">Tout cluster ou serveur hôte Hyper-V pour lequel vous souhaitez gérer la protection doit être inclus dans un cloud VMM.</span><span class="sxs-lookup"><span data-stu-id="2d110-139">Any Hyper-V host server or cluster for which you want to manage protection must be included in a VMM cloud.</span></span>

### <a name="network-mapping-prerequisites"></a><span data-ttu-id="2d110-140">Conditions préalables liées au mappage réseau</span><span class="sxs-lookup"><span data-stu-id="2d110-140">Network mapping prerequisites</span></span>
<span data-ttu-id="2d110-141">Quand vous protégez des machines virtuelles dans Azure, le mappage réseau effectue un mappage entre les réseaux de machines virtuelles sur le serveur VMM source et les réseaux Azure cibles pour permettre ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="2d110-141">When you protect virtual machines in Azure network mapping maps between VM networks on the source VMM server and target Azure networks to enable the following:</span></span>

* <span data-ttu-id="2d110-142">Toutes les machines qui basculent sur le même réseau peuvent se connecter les unes aux autres, quel que soit le plan de récupération auquel elles appartiennent.</span><span class="sxs-lookup"><span data-stu-id="2d110-142">All machines which fail over on the same network can connect to each other, irrespective of which recovery plan they are in.</span></span>
* <span data-ttu-id="2d110-143">Si une passerelle réseau est configurée sur le réseau Azure cible, les machines virtuelles peuvent se connecter à d'autres machines virtuelles locales.</span><span class="sxs-lookup"><span data-stu-id="2d110-143">If a network gateway is setup on the target Azure network, virtual machines can connect to other on-premises virtual machines.</span></span>
* <span data-ttu-id="2d110-144">Si vous ne configurez pas le mappage réseau, seules les machines virtuelles qui basculent dans le même plan de récupération pourront se connecter les unes aux autres après le basculement vers Azure.</span><span class="sxs-lookup"><span data-stu-id="2d110-144">If you don’t configure network mapping only virtual machines that fail over in the same recovery plan will be able to connect to each other after failover to Azure.</span></span>

<span data-ttu-id="2d110-145">Si vous souhaitez déployer le mappage réseau, les conditions suivantes doivent être remplies :</span><span class="sxs-lookup"><span data-stu-id="2d110-145">If you want to deploy network mapping you'll need the following:</span></span>

* <span data-ttu-id="2d110-146">Les machines virtuelles que vous souhaitez protéger sur le serveur VMM source doivent être connectées à un réseau de machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="2d110-146">The virtual machines you want to protect on the source VMM server should be connected to a VM network.</span></span> <span data-ttu-id="2d110-147">Ce réseau doit être lié à un réseau logique lui-même associé au cloud.</span><span class="sxs-lookup"><span data-stu-id="2d110-147">That network should be linked to a logical network that is associated with the cloud.</span></span>
* <span data-ttu-id="2d110-148">Un réseau Azure auquel les machines virtuelles répliquées peuvent se connecter après le basculement.</span><span class="sxs-lookup"><span data-stu-id="2d110-148">An Azure network to which replicated virtual machines can connect after failover.</span></span> <span data-ttu-id="2d110-149">Vous sélectionnerez ce réseau au moment du basculement.</span><span class="sxs-lookup"><span data-stu-id="2d110-149">You'll select this network at the time of failover.</span></span> <span data-ttu-id="2d110-150">Le réseau doit être dans la même région que votre abonnement Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="2d110-150">The network should be in the same region as your Azure Site Recovery subscription.</span></span>

### <a name="powershell-prerequisites"></a><span data-ttu-id="2d110-151">Conditions préalables pour PowerShell</span><span class="sxs-lookup"><span data-stu-id="2d110-151">PowerShell prerequisites</span></span>
<span data-ttu-id="2d110-152">Assurez-vous qu’Azure PowerShell est prêt à l’emploi.</span><span class="sxs-lookup"><span data-stu-id="2d110-152">Make sure you have Azure PowerShell ready to go.</span></span> <span data-ttu-id="2d110-153">Si vous utilisez déjà PowerShell, vous devrez passer à la version 0.8.10 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="2d110-153">If you are already using PowerShell, you'll need to upgrade to version 0.8.10 or later.</span></span> <span data-ttu-id="2d110-154">Pour plus d'informations sur la configuration de PowerShell, consultez la section [Installation et configuration d'Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="2d110-154">For information about setting up PowerShell, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="2d110-155">Une fois PowerShell configuré, vous pouvez afficher toutes les applets de commande disponibles pour le service [ici](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2d110-155">Once you have set up and configured PowerShell, you can view all of the available cmdlets for the service [here](/powershell/azure/overview).</span></span>

<span data-ttu-id="2d110-156">Pour obtenir des conseils sur l'utilisation des applets de commande, par exemple la façon dont les valeurs de paramètres, les entrées et les sorties sont gérées dans Azure PowerShell, consultez la section [Prise en main des applets de commande Azure](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="2d110-156">To learn about tips that can help you use the cmdlets, such as how parameter values, inputs, and outputs are typically handled in Azure PowerShell, see [Get Started with Azure Cmdlets](/powershell/azure/get-started-azureps).</span></span>

## <a name="step-1-set-the-subscription"></a><span data-ttu-id="2d110-157">Étape 1 : Définition de l’abonnement</span><span class="sxs-lookup"><span data-stu-id="2d110-157">Step 1: Set the subscription</span></span>
<span data-ttu-id="2d110-158">Dans PowerShell, exécutez ces applets de commande :</span><span class="sxs-lookup"><span data-stu-id="2d110-158">In PowerShell, run these cmdlets:</span></span>

```
$UserName = "<user@live.com>"
$Password = "<password>"
$AzureSubscriptionName = "prod_sub1"

$SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
$Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $securePassword
Add-AzureAccount -Credential $Cred;
$AzureSubscription = Select-AzureSubscription -SubscriptionName $AzureSubscriptionName

```

<span data-ttu-id="2d110-159">Remplacez les éléments entre « < > » par vos informations spécifiques.</span><span class="sxs-lookup"><span data-stu-id="2d110-159">Replace the elements within the "< >" with your specific information.</span></span>

## <a name="step-2-create-a-site-recovery-vault"></a><span data-ttu-id="2d110-160">Étape 2 : Création d’un coffre Site Recovery</span><span class="sxs-lookup"><span data-stu-id="2d110-160">Step 2: Create a Site Recovery vault</span></span>
<span data-ttu-id="2d110-161">Dans PowerShell, remplacez les éléments entre « < > » par vos informations spécifiques, et exécutez ces commandes :</span><span class="sxs-lookup"><span data-stu-id="2d110-161">In PowerShell, replace the elements within the "< >" with your specific information, and run these commands:</span></span>

```

$VaultName = "<testvault123>"
$VaultGeo  = "<Southeast Asia>"
$OutputPathForSettingsFile = "<c:\>"

```


```
New-AzureSiteRecoveryVault -Location $VaultGeo -Name $VaultName;
$vault = Get-AzureSiteRecoveryVault -Name $VaultName;

```

## <a name="step-3-generate-a-vault-registration-key"></a><span data-ttu-id="2d110-162">Étape 3 : Génération d’une clé d'inscription du coffre</span><span class="sxs-lookup"><span data-stu-id="2d110-162">Step 3: Generate a vault registration key</span></span>
<span data-ttu-id="2d110-163">Générez une clé d'inscription dans le coffre.</span><span class="sxs-lookup"><span data-stu-id="2d110-163">Generate a registration key in the vault.</span></span> <span data-ttu-id="2d110-164">Une fois que vous aurez téléchargé et installé le fournisseur Azure Site Recovery sur le serveur VMM, vous utiliserez cette clé pour inscrire le serveur VMM dans le coffre.</span><span class="sxs-lookup"><span data-stu-id="2d110-164">After you download the Azure Site Recovery Provider and install it on the VMM server, you'll use this key to register the VMM server in the vault.</span></span>

1. <span data-ttu-id="2d110-165">Récupérez le fichier de configuration du coffre et définissez le contexte :</span><span class="sxs-lookup"><span data-stu-id="2d110-165">Get the vault setting file and set the context:</span></span>

   ```

   $VaultName = "<testvault123>"
   $VaultGeo  = "<Southeast Asia>"
   $OutputPathForSettingsFile = "<c:\>"

   $VaultSetingsFile = Get-AzureSiteRecoveryVaultSettingsFile -Location $VaultGeo -Name $VaultName -Path $OutputPathForSettingsFile;

   ```
2. <span data-ttu-id="2d110-166">Définissez le contexte du coffre en exécutant les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="2d110-166">Set the vault context by running the following commands:</span></span>

   ```

   $VaultSettingFilePath = $vaultSetingsFile.FilePath
   $VaultContext = Import-AzureSiteRecoveryVaultSettingsFile -Path $VaultSettingFilePath -ErrorAction Stop

   ```

## <a name="step-4-install-the-azure-site-recovery-provider"></a><span data-ttu-id="2d110-167">Étape 4 : Installation du fournisseur Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="2d110-167">Step 4: Install the Azure Site Recovery Provider</span></span>
1. <span data-ttu-id="2d110-168">Sur la machine VMM, créez un répertoire en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="2d110-168">On the VMM machine, create a directory by running the following command:</span></span>

   ```

   pushd C:\ASR\

   ```
2. <span data-ttu-id="2d110-169">Extrayez les fichiers à l'aide du fournisseur téléchargé en exécutant la commande suivante</span><span class="sxs-lookup"><span data-stu-id="2d110-169">Extract the files using the downloaded provider by running the following command</span></span>

   ```

   AzureSiteRecoveryProvider.exe /x:. /q

   ```
3. <span data-ttu-id="2d110-170">Installez le fournisseur à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="2d110-170">Install the provider using the following commands:</span></span>

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

   <span data-ttu-id="2d110-171">Attendez que l'installation se termine.</span><span class="sxs-lookup"><span data-stu-id="2d110-171">Wait for the installation to finish.</span></span>
4. <span data-ttu-id="2d110-172">Inscrivez le serveur dans le coffre à l'aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="2d110-172">Register the server in the vault using the following command:</span></span>

   ```

   $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
   pushd $BinPath
   $encryptionFilePath = "C:\temp\"
   .\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

   ```

## <a name="step-5-create-an-azure-storage-account"></a><span data-ttu-id="2d110-173">Étape 5 : Création d’un compte de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="2d110-173">Step 5: Create an Azure storage account</span></span>
<span data-ttu-id="2d110-174">Si vous n'avez pas de compte de stockage Azure, créez un compte avec activation de la géo-réplication en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="2d110-174">If you don't have an Azure storage account, create a geo-replication enabled account by running the following command:</span></span>

```

$StorageAccountName = "teststorageacc1"
$StorageAccountGeo  = "Southeast Asia"

New-AzureStorageAccount -StorageAccountName $StorageAccountName -Label $StorageAccountName -Location $StorageAccountGeo;

```

<span data-ttu-id="2d110-175">Le compte de stockage doit se trouver dans la même région que le service Azure Site Recovery et être associé au même abonnement.</span><span class="sxs-lookup"><span data-stu-id="2d110-175">Note that the storage account must be in the same region as the Azure Site Recovery service, and be associated with the same subscription.</span></span>

## <a name="step-6-install-the-azure-recovery-services-agent"></a><span data-ttu-id="2d110-176">Étape 6 : Installation de l'agent Azure Recovery Services</span><span class="sxs-lookup"><span data-stu-id="2d110-176">Step 6: Install the Azure Recovery Services Agent</span></span>
<span data-ttu-id="2d110-177">À partir du portail Azure, installez l'agent Azure Recovery Services sur chaque serveur hôte Hyper-V situé dans les clouds VMM que vous souhaitez protéger.</span><span class="sxs-lookup"><span data-stu-id="2d110-177">From the Azure portal, install the Azure Recovery Services agent on each Hyper-V host server located in the VMM clouds you want to protect.</span></span>

<span data-ttu-id="2d110-178">Exécutez la commande suivante sur l’ensemble des hôtes VMM :</span><span class="sxs-lookup"><span data-stu-id="2d110-178">Run the following command on all VMM hosts:</span></span>

```

marsagentinstaller.exe /q /nu

```


## <a name="step-7-configure-cloud-protection-settings"></a><span data-ttu-id="2d110-179">Étape 7 : Configuration des paramètres de protection de cloud</span><span class="sxs-lookup"><span data-stu-id="2d110-179">Step 7: Configure cloud protection settings</span></span>
1. <span data-ttu-id="2d110-180">Créez un profil de protection cloud pour Azure en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="2d110-180">Create a cloud protection profile to Azure by running the following command:</span></span>

   ```

   $ReplicationFrequencyInSeconds = "300";
   $ProfileResult = New-AzureSiteRecoveryProtectionProfileObject -ReplicationProvider HyperVReplica -RecoveryAzureSubscription $AzureSubscriptionName -RecoveryAzureStorageAccount $StorageAccountName -ReplicationFrequencyInSeconds     $ReplicationFrequencyInSeconds;

   ```
2. <span data-ttu-id="2d110-181">Récupérez un conteneur de protection en exécutant les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="2d110-181">Get a protection container by running the following commands:</span></span>

   ```

   $PrimaryCloud = "testcloud"
   $protectionContainer = Get-AzureSiteRecoveryProtectionContainer -Name $PrimaryCloud;

   ```
3. <span data-ttu-id="2d110-182">Lancez l'association du conteneur de protection avec le cloud :</span><span class="sxs-lookup"><span data-stu-id="2d110-182">Start the association of the protection container with the cloud:</span></span>

   ```

   $associationJob = Start-AzureSiteRecoveryProtectionProfileAssociationJob -ProtectionProfile $profileResult -PrimaryProtectionContainer $protectionContainer;        

   ```
4. <span data-ttu-id="2d110-183">Une fois la tâche terminée, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="2d110-183">After the job has finished, run the following command:</span></span>

        $job = Get-AzureSiteRecoveryJob -Id $associationJob.JobId;
        if($job -eq $null -or $job.StateDescription -ne "Completed")
        {
        $isJobLeftForProcessing = $true;
        }


1. <span data-ttu-id="2d110-184">Une fois la tâche terminée, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="2d110-184">After the job has finished processing, run the following command:</span></span>

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



<span data-ttu-id="2d110-185">Pour vérifier que l'opération est terminée, suivez les étapes décrites dans la section [Suivi de l'activité](#monitor).</span><span class="sxs-lookup"><span data-stu-id="2d110-185">To check the completion of the operation, follow the steps in [Monitor Activity](#monitor).</span></span>

## <a name="step-8-configure-network-mapping"></a><span data-ttu-id="2d110-186">Étape 8 : Configuration du mappage réseau</span><span class="sxs-lookup"><span data-stu-id="2d110-186">Step 8: Configure network mapping</span></span>
<span data-ttu-id="2d110-187">Avant de commencer le mappage réseau, vérifiez que les machines virtuelles sur le serveur VMM source sont connectées à un réseau de machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="2d110-187">Before you begin network mapping verify that virtual machines on the source VMM server are connected to a VM network.</span></span> <span data-ttu-id="2d110-188">En outre, vous devez créer un ou plusieurs réseaux virtuels Azure.</span><span class="sxs-lookup"><span data-stu-id="2d110-188">In addition, create one or more Azure virtual networks.</span></span> <span data-ttu-id="2d110-189">Notez que plusieurs réseaux de machines virtuelles peuvent être mappés à un seul réseau Azure.</span><span class="sxs-lookup"><span data-stu-id="2d110-189">Note that multiple VM networks can be mapped to a single Azure network.</span></span>

<span data-ttu-id="2d110-190">Notez que si le réseau cible a plusieurs sous-réseaux et que l'un d'entre eux a le même nom que le sous-réseau où se trouve la machine virtuelle source, la machine virtuelle de réplication sera connectée à ce sous-réseau cible après le basculement.</span><span class="sxs-lookup"><span data-stu-id="2d110-190">Note that if the target network has multiple subnets and one of those subnets has the same name as subnet on which the source virtual machine is located, then the replica virtual machine will be connected to that target subnet after failover.</span></span> <span data-ttu-id="2d110-191">S’il n’existe aucun sous-réseau cible avec un nom correspondant, la machine virtuelle sera connectée au premier sous-réseau du réseau.</span><span class="sxs-lookup"><span data-stu-id="2d110-191">If there is not a target subnet with a matching name, the virtual machine will be connected to the first subnet in the network.</span></span>

<span data-ttu-id="2d110-192">La première commande récupère les serveurs pour le coffre Azure Site Recovery actuel.</span><span class="sxs-lookup"><span data-stu-id="2d110-192">The first command gets servers for the current Azure Site Recovery vault.</span></span> <span data-ttu-id="2d110-193">La commande stocke les serveurs Microsoft Azure Site Recovery dans la variable tableau $Servers.</span><span class="sxs-lookup"><span data-stu-id="2d110-193">The command stores the Microsoft Azure Site Recovery servers in the $Servers array variable.</span></span>

    $Servers = Get-AzureSiteRecoveryServer


<span data-ttu-id="2d110-194">La deuxième commande récupère le réseau Site Recovery pour le premier serveur du tableau $Servers.</span><span class="sxs-lookup"><span data-stu-id="2d110-194">The second command gets the site recovery network for the first server in the $Servers array.</span></span> <span data-ttu-id="2d110-195">La commande stocke les réseaux dans la variable $Networks.</span><span class="sxs-lookup"><span data-stu-id="2d110-195">The command stores the networks in the $Networks variable.</span></span>

    $Networks = Get-AzureSiteRecoveryNetwork -Server $Servers[0]

<span data-ttu-id="2d110-196">La troisième commande extrait vos abonnements Azure à l’aide de l’applet de commande Get-AzureSubscription, puis stocke cette valeur dans la variable $Subscriptions.</span><span class="sxs-lookup"><span data-stu-id="2d110-196">The third command gets your Azure subscriptions by using the Get-AzureSubscription cmdlet, and then stores that value in the $Subscriptions variable.</span></span>

    $Subscriptions = Get-AzureSubscription



<span data-ttu-id="2d110-197">La quatrième commande récupère les réseaux virtuels Azure à l'aide de l'applet de commande Get-AzureVNetSite, puis stocke cette valeur dans la variable $AzureVmNetworks.</span><span class="sxs-lookup"><span data-stu-id="2d110-197">The fourth command gets Azure virtual networks by using the Get-AzureVNetSite cmdlet, and then that value in the $AzureVmNetworks variable.</span></span>

    $AzureVmNetworks = Get-AzureVNetSite



<span data-ttu-id="2d110-198">L'applet de commande finale crée un mappage entre le réseau principal et le réseau de la machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="2d110-198">The final cmdlet creates a mapping between the primary network and the Azure virtual machine network.</span></span> <span data-ttu-id="2d110-199">L'applet de commande fixe le réseau principal comme premier élément de $Networks.</span><span class="sxs-lookup"><span data-stu-id="2d110-199">The cmdlet specifies the primary network as the first element of $Networks.</span></span> <span data-ttu-id="2d110-200">L'applet de commande fixe un réseau de machine virtuelle comme premier élément de $AzureVmNetworks à l'aide de son ID.</span><span class="sxs-lookup"><span data-stu-id="2d110-200">The cmdlet specifies a virtual machine network as the first element of $AzureVmNetworks by using its ID.</span></span> <span data-ttu-id="2d110-201">La commande inclut l’identifiant de votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="2d110-201">The command includes your Azure subscription ID.</span></span>

    New-AzureSiteRecoveryNetworkMapping -PrimaryNetwork $Networks[0] -AzureSubscriptionId $Subscriptions[0].SubscriptionId -AzureVMNetworkId $AzureVmNetworks[0].Id


## <a name="step-9-enable-protection-for-virtual-machines"></a><span data-ttu-id="2d110-202">Étape 9 : Activation de la protection des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="2d110-202">Step 9: Enable protection for virtual machines</span></span>
<span data-ttu-id="2d110-203">Dès lors que les serveurs, les clouds et les réseaux ont été configurés correctement, vous pouvez activer la protection pour les machines virtuelles du cloud.</span><span class="sxs-lookup"><span data-stu-id="2d110-203">After servers, clouds, and networks are configured correctly, you can enable protection for virtual machines in the cloud.</span></span> <span data-ttu-id="2d110-204">Notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="2d110-204">Note the following:</span></span>

<span data-ttu-id="2d110-205">Les machines virtuelles doivent répondre à la [configuration requise pour les machines virtuelles Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="2d110-205">Virtual machines must meet [Azure virtual machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

<span data-ttu-id="2d110-206">Pour activer la protection, vous devez définir les propriétés du système d'exploitation et du disque du système d'exploitation pour la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="2d110-206">To enable protection the operating system and operating system disk properties must be set for the virtual machine.</span></span> <span data-ttu-id="2d110-207">Lorsque vous créez une machine virtuelle dans VMM à l'aide d'un modèle de machine virtuelle, vous pouvez définir la propriété.</span><span class="sxs-lookup"><span data-stu-id="2d110-207">When you create a virtual machine in VMM using a virtual machine template you can set the property.</span></span> <span data-ttu-id="2d110-208">Vous pouvez également définir ces propriétés pour des machines virtuelles existantes sous les onglets **Général** et **Configuration matérielle** des propriétés de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="2d110-208">You can also set these properties for existing virtual machines on the **General** and **Hardware Configuration** tabs of the virtual machine properties.</span></span> <span data-ttu-id="2d110-209">Si vous ne définissez pas ces propriétés dans VMM, vous pourrez les configurer dans le portail Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="2d110-209">If you don't set these properties in VMM you'll be able to configure them in the Azure Site Recovery portal.</span></span>

1. <span data-ttu-id="2d110-210">Afin d’activer la protection, exécutez la commande suivante pour récupérer le conteneur de protection :</span><span class="sxs-lookup"><span data-stu-id="2d110-210">To enable protection, run the following command to get the protection container:</span></span>

     <span data-ttu-id="2d110-211">$ProtectionContainer = Get-AzureSiteRecoveryProtectionContainer -Name $CloudName</span><span class="sxs-lookup"><span data-stu-id="2d110-211">$ProtectionContainer = Get-AzureSiteRecoveryProtectionContainer -Name $CloudName</span></span>
2. <span data-ttu-id="2d110-212">Récupérez l’entité de protection (machine virtuelle) en exécutant les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="2d110-212">Get the protection entity (VM) by running the following command:</span></span>

        $protectionEntity = Get-AzureSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer



1. <span data-ttu-id="2d110-213">Activez la récupération d’urgence de la machine virtuelle en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="2d110-213">Enable the DR for the VM by running the following command:</span></span>

        $jobResult = Set-AzureSiteRecoveryProtectionEntity -ProtectionEntity $protectionEntity     -Protection Enable -Force



## <a name="test-your-deployment"></a><span data-ttu-id="2d110-214">Tester votre déploiement</span><span class="sxs-lookup"><span data-stu-id="2d110-214">Test your deployment</span></span>
<span data-ttu-id="2d110-215">Pour tester votre déploiement, vous pouvez exécuter un test de basculement pour une seule machine virtuelle, ou créer un plan de récupération comportant plusieurs machines virtuelles et exécuter sur lui un test de basculement.</span><span class="sxs-lookup"><span data-stu-id="2d110-215">To test your deployment you can run a test failover for a single virtual machine, or create a recovery plan consisting of multiple virtual machines and run a test failover for the plan.</span></span> <span data-ttu-id="2d110-216">Il simule votre mécanisme de basculement et de récupération dans un réseau isolé.</span><span class="sxs-lookup"><span data-stu-id="2d110-216">Test failover simulates your failover and recovery mechanism in an isolated network.</span></span> <span data-ttu-id="2d110-217">Notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="2d110-217">Note that:</span></span>

* <span data-ttu-id="2d110-218">Si vous voulez vous connecter à la machine virtuelle dans Azure avec le Bureau à distance après le basculement, activez Connexion Bureau à distance sur la machine virtuelle avant d’exécuter le test de basculement.</span><span class="sxs-lookup"><span data-stu-id="2d110-218">If you want to connect to the virtual machine in Azure using Remote Desktop after the failover, enable Remote Desktop Connection on the virtual machine before you run the test failover.</span></span>
* <span data-ttu-id="2d110-219">Après le basculement, vous utiliserez une adresse IP publique pour vous connecter à la machine virtuelle dans Azure avec le Bureau à distance.</span><span class="sxs-lookup"><span data-stu-id="2d110-219">After failover, you'll use a public IP address to connect to the virtual machine in Azure using Remote Desktop.</span></span> <span data-ttu-id="2d110-220">Dans ce cas, assurez-vous qu'aucune de vos stratégies de domaine ne vous empêche de vous connecter à une machine virtuelle avec une adresse publique.</span><span class="sxs-lookup"><span data-stu-id="2d110-220">If you want to do this, ensure you don't have any domain policies that prevent you from connecting to a virtual machine using a public address.</span></span>

<span data-ttu-id="2d110-221">Pour vérifier que l'opération est terminée, suivez les étapes décrites dans la section [Suivi de l'activité](#monitor).</span><span class="sxs-lookup"><span data-stu-id="2d110-221">To check the completion of the operation, follow the steps in [Monitor Activity](#monitor).</span></span>

### <a name="create-a-recovery-plan"></a><span data-ttu-id="2d110-222">Créer un plan de récupération</span><span class="sxs-lookup"><span data-stu-id="2d110-222">Create a recovery plan</span></span>
1. <span data-ttu-id="2d110-223">Créez un fichier .xml comme modèle pour votre plan de récupération en utilisant les données ci-dessous, puis enregistrez-le sous « C:\RPTemplatePath.xml ».</span><span class="sxs-lookup"><span data-stu-id="2d110-223">Create an .xml file as a template for your recovery plan using the data below, and then save it as "C:\RPTemplatePath.xml".</span></span>
2. <span data-ttu-id="2d110-224">Modifiez l'Id, Name, PrimaryServerId et SecondaryServerId du nœud RecoveryPlan.</span><span class="sxs-lookup"><span data-stu-id="2d110-224">Change the RecoveryPlan node Id, Name, PrimaryServerId, and SecondaryServerId.</span></span>
3. <span data-ttu-id="2d110-225">Modifiez le PrimaryProtectionEntityId du nœud ProtectionEntity (vmid pour VMM).</span><span class="sxs-lookup"><span data-stu-id="2d110-225">Change the ProtectionEntity node PrimaryProtectionEntityId (vmid from VMM).</span></span>
4. <span data-ttu-id="2d110-226">Vous pouvez ajouter davantage de machines virtuelles en ajoutant des nœuds ProtectionEntity.</span><span class="sxs-lookup"><span data-stu-id="2d110-226">You can add more VMs by adding more ProtectionEntity nodes.</span></span>

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



1. <span data-ttu-id="2d110-227">Remplissez les données du modèle :</span><span class="sxs-lookup"><span data-stu-id="2d110-227">Fill in the data in the template:</span></span>

        $TemplatePath = "C:\RPTemplatePath.xml";



1. <span data-ttu-id="2d110-228">Créez le RecoveryPlan :</span><span class="sxs-lookup"><span data-stu-id="2d110-228">Create the RecoveryPlan:</span></span>

        $RPCreationJob = New-AzureSiteRecoveryRecoveryPlan -File $TemplatePath -WaitForCompletion;

### <a name="run-a-test-failover"></a><span data-ttu-id="2d110-229">Exécution d’un test de basculement</span><span class="sxs-lookup"><span data-stu-id="2d110-229">Run a test failover</span></span>
1. <span data-ttu-id="2d110-230">Récupérez l'objet RecoveryPlan en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="2d110-230">Get the RecoveryPlan object by running the following command:</span></span>

     <span data-ttu-id="2d110-231">$RPObject = Get-AzureSiteRecoveryRecoveryPlan -Name $RPName;</span><span class="sxs-lookup"><span data-stu-id="2d110-231">$RPObject = Get-AzureSiteRecoveryRecoveryPlan -Name $RPName;</span></span>
2. <span data-ttu-id="2d110-232">Lancez le test de basculement en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="2d110-232">Start the test failover by running the following command:</span></span>

        $jobIDResult = Start-AzureSiteRecoveryTestFailoverJob -RecoveryPlan $RPObject -Direction PrimaryToRecovery;


## <span data-ttu-id="2d110-233"><a name=monitor></a> Suivi de l'activité</span><span class="sxs-lookup"><span data-stu-id="2d110-233"><a name=monitor></a> Monitor Activity</span></span>
<span data-ttu-id="2d110-234">Utilisez les commandes suivantes pour suivre l’activité.</span><span class="sxs-lookup"><span data-stu-id="2d110-234">Use the following commands to monitor the activity.</span></span> <span data-ttu-id="2d110-235">Vous devez attendre la fin du traitement entre les tâches.</span><span class="sxs-lookup"><span data-stu-id="2d110-235">Note that you have to wait in between jobs for the processing to finish.</span></span>

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



## <a name="next-steps"></a><span data-ttu-id="2d110-236">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2d110-236">Next steps</span></span>
<span data-ttu-id="2d110-237">[Découvrez plus](/powershell/azure/overview) d'informations sur les applets de commande PowerShell Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="2d110-237">[Read more](/powershell/azure/overview) about Azure Site Recovery PowerShell cmdlets.</span></span> <span data-ttu-id="2d110-238"></a>.</span><span class="sxs-lookup"><span data-stu-id="2d110-238"></a>.</span></span>
