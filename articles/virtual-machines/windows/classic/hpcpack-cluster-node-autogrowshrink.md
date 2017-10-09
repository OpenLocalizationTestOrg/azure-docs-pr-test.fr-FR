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
# <a name="automatically-grow-and-shrink-hello-hpc-pack-cluster-resources-in-azure-according-toohello-cluster-workload"></a><span data-ttu-id="0d0b1-103">Développer et réduire les ressources de cluster HPC Pack hello dans Azure en fonction de la charge du cluster toohello automatiquement</span><span class="sxs-lookup"><span data-stu-id="0d0b1-103">Automatically grow and shrink hello HPC Pack cluster resources in Azure according toohello cluster workload</span></span>
<span data-ttu-id="0d0b1-104">Si vous déployez des nœuds de « Croissance » Azure dans votre cluster HPC Pack, ou si vous créez un cluster HPC Pack dans les machines virtuelles Azure, vous souhaiterez peut-être un moyen pour augmenter ou réduire les ressources de cluster hello tels que des nœuds ou des noyaux en fonction de la charge de travail hello sur le cluster de hello automatiquement.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-104">If you deploy Azure “burst” nodes in your HPC Pack cluster, or you create an HPC Pack cluster in Azure VMs, you may want a way to automatically grow or shrink hello cluster resources such as nodes or cores according to hello workload on hello cluster.</span></span> <span data-ttu-id="0d0b1-105">Mise à l’échelle des ressources de cluster hello de cette façon vous permet de toouse vos ressources Azure plus efficacement et de contrôler leurs coûts.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-105">Scaling hello cluster resources in this way allows you toouse your Azure resources more efficiently and control their costs.</span></span>

<span data-ttu-id="0d0b1-106">Cet article montre deux manières de HPC Pack fournit des ressources de calcul tooautoscale :</span><span class="sxs-lookup"><span data-stu-id="0d0b1-106">This article shows you two ways that HPC Pack provides tooautoscale compute resources:</span></span>

* <span data-ttu-id="0d0b1-107">Hello, propriété de cluster HPC Pack **AutoGrowShrink**</span><span class="sxs-lookup"><span data-stu-id="0d0b1-107">hello HPC Pack cluster property **AutoGrowShrink**</span></span>

* <span data-ttu-id="0d0b1-108">Hello **AzureAutoGrowShrink.ps1** script PowerShell HPC</span><span class="sxs-lookup"><span data-stu-id="0d0b1-108">hello **AzureAutoGrowShrink.ps1** HPC PowerShell script</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="0d0b1-109">Actuellement, vous ne pouvez qu’augmenter ou diminuer automatiquement les nœuds de calcul HPC Pack qui exécutent un système d’exploitation Windows Server.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-109">Currently you can only automatically grow and shrink HPC Pack compute nodes that are running a Windows Server operating system.</span></span>


## <a name="set-hello-autogrowshrink-cluster-property"></a><span data-ttu-id="0d0b1-110">Définir la propriété de cluster hello AutoGrowShrink</span><span class="sxs-lookup"><span data-stu-id="0d0b1-110">Set hello AutoGrowShrink cluster property</span></span>
### <a name="prerequisites"></a><span data-ttu-id="0d0b1-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="0d0b1-111">Prerequisites</span></span>

* <span data-ttu-id="0d0b1-112">**HPC Pack 2012 R2 Update 2 ou ultérieur cluster** -nœud principal du cluster hello peut être déployé localement ou dans une machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-112">**HPC Pack 2012 R2 Update 2 or later cluster** - hello cluster head node can be deployed either on-premises or in an Azure VM.</span></span> <span data-ttu-id="0d0b1-113">Consultez [configurer un cluster hybride avec HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) tooget a démarré avec un nœud principal local et les nœuds de « Croissance » Azure.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-113">See [Set up a hybrid cluster with HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) tooget started with an on-premises head node and Azure "burst" nodes.</span></span> <span data-ttu-id="0d0b1-114">Consultez hello [script de déploiement IaaS de HPC Pack](hpcpack-cluster-powershell-script.md) tooquickly déployer un cluster HPC Pack dans des machines virtuelles Azure.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-114">See hello [HPC Pack IaaS deployment script](hpcpack-cluster-powershell-script.md) tooquickly deploy an HPC Pack cluster in Azure VMs.</span></span>

* <span data-ttu-id="0d0b1-115">**Pour un cluster avec un nœud principal dans Azure (modèle de déploiement Resource Manager)** : à partir de HPC Pack 2016, l’authentification par certificat dans une application Azure Active Directory est utilisée pour la croissance et la réduction automatiques de machines virtuelles de cluster déployées à l’aide d’Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-115">**For a cluster with a head node in Azure (Resource Manager deployment model)** - Starting in HPC Pack 2016, certificate authentication in an Azure Active Directory application is used for automatically growing and shrinking cluster VMs deployed using Azure Resource Manager.</span></span> <span data-ttu-id="0d0b1-116">Configurez un certificat de la façon suivante :</span><span class="sxs-lookup"><span data-stu-id="0d0b1-116">Configure a certificate as follows:</span></span>

  1. <span data-ttu-id="0d0b1-117">Après le déploiement de cluster, se connecter par le nœud principal tooone de bureau à distance.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-117">After cluster deployment, connect by Remote Desktop tooone head node.</span></span>

  2. <span data-ttu-id="0d0b1-118">Télécharger le nœud principal du tooeach hello certificat (format PFX avec une clé privée) et installer tooCert:\LocalMachine\My et Cert : \LocalMachine\Root.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-118">Upload hello certificate (PFX format with private key) tooeach head node and install tooCert:\LocalMachine\My and Cert:\LocalMachine\Root.</span></span>

  3. <span data-ttu-id="0d0b1-119">Démarrer PowerShell Azure en tant qu’administrateur et exécutez hello suivant de commandes sur un seul nœud principal :</span><span class="sxs-lookup"><span data-stu-id="0d0b1-119">Start Azure PowerShell as an administrator and run hello following commands on one head node:</span></span>

    ```powershell
        cd $env:CCP_HOME\bin

        Login-AzureRmAccount
    ```
        
    <span data-ttu-id="0d0b1-120">Si votre compte est en plus d’un client Azure Active Directory ou d’un abonnement Azure, vous pouvez exécuter les éléments suivants de hello commande locataire approprié de tooselect hello et d’abonnement :</span><span class="sxs-lookup"><span data-stu-id="0d0b1-120">If your account is in more than one Azure Active Directory tenant or Azure subscription, you can run hello following command tooselect hello correct tenant and subscription:</span></span>
  
    ```powershell
        Login-AzureRMAccount -TenantId <TenantId> -SubscriptionId <subscriptionId>
    ```     
       
    <span data-ttu-id="0d0b1-121">Exécutez hello suivant commande tooview hello actuellement sélectionné locataire et abonnement :</span><span class="sxs-lookup"><span data-stu-id="0d0b1-121">Run hello following command tooview hello currently selected tenant and subscription:</span></span>
    
    ```powershell
        Get-AzureRMContext
    ```

  4. <span data-ttu-id="0d0b1-122">Exécutez hello script suivant</span><span class="sxs-lookup"><span data-stu-id="0d0b1-122">Run hello following script</span></span>

    ```powershell
        .\ConfigARMAutoGrowShrinkCert.ps1 -DisplayName “YourHpcPackAppName” -HomePage "https://YourHpcPackAppHomePage" -IdentifierUri "https://YourHpcPackAppUri" -CertificateThumbprint "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX" -TenantId xxxxxxxx-xxxxx-xxxxx-xxxxx-xxxxxxxxxxxx
    ```

    <span data-ttu-id="0d0b1-123">où</span><span class="sxs-lookup"><span data-stu-id="0d0b1-123">where</span></span>

    <span data-ttu-id="0d0b1-124">**DisplayName** : nom d’affichage de l’application Azure Active.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-124">**DisplayName** - Azure Active Application display name.</span></span> <span data-ttu-id="0d0b1-125">Si l’application hello n’existe pas, il est créé dans Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-125">If hello application does not exist, it is created in Azure Active Directory.</span></span>

    <span data-ttu-id="0d0b1-126">**Page d’accueil** -hello page d’accueil de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-126">**HomePage** - hello home page of hello application.</span></span> <span data-ttu-id="0d0b1-127">Vous pouvez configurer une URL factice, comme dans hello précédent exemple.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-127">You can configure a dummy URL, as in hello preceding example.</span></span>

    <span data-ttu-id="0d0b1-128">**IdentifierUri** -identificateur de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-128">**IdentifierUri** - Identifier of hello application.</span></span> <span data-ttu-id="0d0b1-129">Vous pouvez configurer une URL factice, comme dans hello précédent exemple.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-129">You can configure a dummy URL, as in hello preceding example.</span></span>

    <span data-ttu-id="0d0b1-130">**CertificateThumbprint** -empreinte numérique du certificat hello installé sur le nœud principal de hello à l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-130">**CertificateThumbprint** - Thumbprint of hello certificate you installed on hello head node in Step 1.</span></span>

    <span data-ttu-id="0d0b1-131">**TenantId** : ID client de votre Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-131">**TenantId** - Tenant ID of your Azure Active Directory.</span></span> <span data-ttu-id="0d0b1-132">Vous pouvez obtenir hello ID client à partir du portail d’Azure Active Directory hello **propriétés** page.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-132">You can get hello Tenant ID from hello Azure Active Directory portal **Properties** page.</span></span>

    <span data-ttu-id="0d0b1-133">Pour plus d’informations sur **ConfigARMAutoGrowShrinkCert.ps1**, exécutez `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-133">For more details about **ConfigARMAutoGrowShrinkCert.ps1**, run `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`.</span></span>


* <span data-ttu-id="0d0b1-134">**Pour un cluster avec un nœud principal dans Azure (modèle de déploiement classique)** - si vous utilisez un cluster de hello du déploiement script toocreate hello IaaS HPC Pack dans le modèle de déploiement classique de hello, activer hello **AutoGrowShrink** cluster propriété en définissant l’option de AutoGrowShrink hello dans le fichier de configuration de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-134">**For a cluster with a head node in Azure (classic deployment model)** - If you use hello HPC Pack IaaS deployment script toocreate hello cluster in hello classic deployment model, enable hello **AutoGrowShrink** cluster property by setting hello AutoGrowShrink option in hello cluster configuration file.</span></span> <span data-ttu-id="0d0b1-135">Pour plus d’informations, consultez la documentation hello accompagnant hello [téléchargement du script](https://www.microsoft.com/download/details.aspx?id=44949).</span><span class="sxs-lookup"><span data-stu-id="0d0b1-135">For details, see hello documentation accompanying hello [script download](https://www.microsoft.com/download/details.aspx?id=44949).</span></span>

    <span data-ttu-id="0d0b1-136">Vous pouvez également activer hello **AutoGrowShrink** propriété cluster après avoir déployé le cluster de hello à l’aide de PowerShell HPC commandes décrites dans hello suivant la section.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-136">Alternatively, enable hello **AutoGrowShrink** cluster property after you deploy hello cluster by using HPC PowerShell commands described in hello following section.</span></span> <span data-ttu-id="0d0b1-137">tooprepare pour cela, étapes de la première hello complet suivant :</span><span class="sxs-lookup"><span data-stu-id="0d0b1-137">tooprepare for this, first complete hello following steps:</span></span>

  1. <span data-ttu-id="0d0b1-138">Configurer un certificat de gestion Azure sur le nœud principal de hello et Bonjour abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-138">Configure an Azure management certificate on hello head node and in hello Azure subscription.</span></span> <span data-ttu-id="0d0b1-139">Pour un déploiement de test, vous pouvez utiliser le certificat auto-signé hello par défaut de Microsoft HPC Azure HPC Pack est installé sur le nœud principal de hello et puis télécharger ce tooyour certificat abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-139">For a test deployment, you can use hello Default Microsoft HPC Azure self-signed certificate that HPC Pack installs on hello head node, and then upload that certificate tooyour Azure subscription.</span></span> <span data-ttu-id="0d0b1-140">Pour plus d’options et les étapes, consultez hello [Guide de la bibliothèque TechNet](https://technet.microsoft.com/library/gg481759.aspx).</span><span class="sxs-lookup"><span data-stu-id="0d0b1-140">For options and steps, see hello [TechNet Library guidance](https://technet.microsoft.com/library/gg481759.aspx).</span></span>

  2. <span data-ttu-id="0d0b1-141">Exécutez **regedit** sur le nœud principal de hello, accédez à tooHKLM\SOFTWARE\Micorsoft\HPC\IaasInfo, puis ajoutez une valeur de chaîne.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-141">Run **regedit** on hello head node, go tooHKLM\SOFTWARE\Micorsoft\HPC\IaasInfo, and add a string value.</span></span> <span data-ttu-id="0d0b1-142">Définir le nom de la valeur hello trop « Empreinte numérique » et la valeur données toohello empreinte numérique du certificat hello à l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-142">Set hello Value name too“ThumbPrint”, and Value data toohello thumbprint of hello certificate in Step 1.</span></span>

### <a name="hpc-powershell-commands-tooset-hello-autogrowshrink-property"></a><span data-ttu-id="0d0b1-143">Propriété de HPC PowerShell commands tooset hello AutoGrowShrink</span><span class="sxs-lookup"><span data-stu-id="0d0b1-143">HPC PowerShell commands tooset hello AutoGrowShrink property</span></span>
<span data-ttu-id="0d0b1-144">Voici des exemples PowerShell HPC commandes tooset **AutoGrowShrink** et tootune son comportement avec des paramètres supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-144">Following are sample HPC PowerShell commands tooset **AutoGrowShrink** and tootune its behavior with additional parameters.</span></span> <span data-ttu-id="0d0b1-145">Consultez [AutoGrowShrink paramètres](#AutoGrowShrink-parameters) plus loin dans cet article pour la liste complète des paramètres hello.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-145">See [AutoGrowShrink parameters](#AutoGrowShrink-parameters) later in this article for hello complete list of settings.</span></span>

<span data-ttu-id="0d0b1-146">toorun ces commandes, démarrez HPC PowerShell sur le nœud principal du cluster hello en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-146">toorun these commands, start HPC PowerShell on hello cluster head node as an administrator.</span></span>

<span data-ttu-id="0d0b1-147">**tooenable hello AutoGrowShrink propriété**</span><span class="sxs-lookup"><span data-stu-id="0d0b1-147">**tooenable hello AutoGrowShrink property**</span></span>

```powershell
Set-HpcClusterProperty –EnableGrowShrink 1
```

<span data-ttu-id="0d0b1-148">**toodisable hello AutoGrowShrink propriété**</span><span class="sxs-lookup"><span data-stu-id="0d0b1-148">**toodisable hello AutoGrowShrink property**</span></span>

```powershell
Set-HpcClusterProperty –EnableGrowShrink 0
```

<span data-ttu-id="0d0b1-149">**toochange hello augmenter l’intervalle en minutes**</span><span class="sxs-lookup"><span data-stu-id="0d0b1-149">**toochange hello grow interval in minutes**</span></span>

```powershell
Set-HpcClusterProperty –GrowInterval <interval>
```

<span data-ttu-id="0d0b1-150">**toochange hello réduire l’intervalle en minutes**</span><span class="sxs-lookup"><span data-stu-id="0d0b1-150">**toochange hello shrink interval in minutes**</span></span>

```powershell
Set-HpcClusterProperty –ShrinkInterval <interval>
```

<span data-ttu-id="0d0b1-151">**configuration actuelle de hello tooview de AutoGrowShrink**</span><span class="sxs-lookup"><span data-stu-id="0d0b1-151">**tooview hello current configuration of AutoGrowShrink**</span></span>

```powershell
Get-HpcClusterProperty –AutoGrowShrink
```

<span data-ttu-id="0d0b1-152">**groupes de nœuds tooexclude de AutoGrowShrink**</span><span class="sxs-lookup"><span data-stu-id="0d0b1-152">**tooexclude node groups from AutoGrowShrink**</span></span>

```powershell
Set-HpcClusterProperty –ExcludeNodeGroups <group1,group2,group3>
```

>[!NOTE] 
> <span data-ttu-id="0d0b1-153">Ce paramètre est pris en charge dans HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-153">This parameter is supported starting in HPC Pack 2016</span></span>
>

### <a name="autogrowshrink-parameters"></a><span data-ttu-id="0d0b1-154">Paramètres d’AutoGrowShrink</span><span class="sxs-lookup"><span data-stu-id="0d0b1-154">AutoGrowShrink parameters</span></span>
<span data-ttu-id="0d0b1-155">Hello Voici AutoGrowShrink les paramètres que vous pouvez modifier à l’aide de hello **Set-HpcClusterProperty** commande.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-155">hello following are AutoGrowShrink parameters that you can modify by using hello **Set-HpcClusterProperty** command.</span></span>

* <span data-ttu-id="0d0b1-156">**EnableGrowShrink** - commutateur tooenable ou désactiver hello **AutoGrowShrink** propriété.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-156">**EnableGrowShrink** - Switch tooenable or disable hello **AutoGrowShrink** property.</span></span>
* <span data-ttu-id="0d0b1-157">**ParamSweepTasksPerCore** -nombre de balayage paramétrique tâches toogrow un seul cœur.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-157">**ParamSweepTasksPerCore** - Number of parametric sweep tasks toogrow one core.</span></span> <span data-ttu-id="0d0b1-158">par défaut de Hello est toogrow un cœur de chaque tâche.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-158">hello default is toogrow one core per task.</span></span>

  > [!NOTE]
  > <span data-ttu-id="0d0b1-159">Modifications de HPC Pack QFE KB3134307 **ParamSweepTasksPerCore** trop**TasksPerResourceUnit**.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-159">HPC Pack QFE KB3134307 changes **ParamSweepTasksPerCore** too**TasksPerResourceUnit**.</span></span> <span data-ttu-id="0d0b1-160">Il est basé sur le type de ressource de tâche hello et peut être un nœud socket ou un cœur.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-160">It is based on hello job resource type and can be node, socket, or core.</span></span>
  >
  >
* <span data-ttu-id="0d0b1-161">**GrowThreshold** -seuil de croissance automatique de tootrigger de tâches en file d’attente.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-161">**GrowThreshold** - Threshold of queued tasks tootrigger automatic growth.</span></span> <span data-ttu-id="0d0b1-162">par défaut de Hello est 1, ce qui signifie que si 1 ou plusieurs tâches dans hello en file d’attente d’état, d’augmenter automatiquement les nœuds.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-162">hello default is 1, which means that if there are 1 or more tasks in hello queued state, automatically grow nodes.</span></span>
* <span data-ttu-id="0d0b1-163">**GrowInterval** -intervalle de croissance automatique de tootrigger minutes.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-163">**GrowInterval** - Interval in minutes tootrigger automatic growth.</span></span> <span data-ttu-id="0d0b1-164">intervalle de salutation par défaut est de 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-164">hello default interval is 5 minutes.</span></span>
* <span data-ttu-id="0d0b1-165">**ShrinkInterval** -intervalle en minutes un compactage automatique tootrigger.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-165">**ShrinkInterval** - Interval in minutes tootrigger automatic shrinking.</span></span> <span data-ttu-id="0d0b1-166">intervalle de salutation par défaut est de 5 minutes. |</span><span class="sxs-lookup"><span data-stu-id="0d0b1-166">hello default interval is 5 minutes.|</span></span>
* <span data-ttu-id="0d0b1-167">**ShrinkIdleTimes** -nombre de vérifications continue tooshrink tooindicate hello nœuds est inactif.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-167">**ShrinkIdleTimes** - Number of continuous checks tooshrink tooindicate hello nodes are idle.</span></span> <span data-ttu-id="0d0b1-168">valeur par défaut Hello est 3 fois.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-168">hello default is 3 times.</span></span> <span data-ttu-id="0d0b1-169">Par exemple, si hello **ShrinkInterval** est de 5 minutes, HPC Pack vérifie si le nœud de hello est inactif à toutes les 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-169">For example, if hello **ShrinkInterval** is 5 minutes, HPC Pack checks whether hello node is idle every 5 minutes.</span></span> <span data-ttu-id="0d0b1-170">Si les nœuds de hello sont en état d’inactivité hello après que 3 continue vérifie (15 minutes), puis HPC Pack réduit ce nœud.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-170">If hello nodes are in hello idle state after 3 continuous checks (15 minutes), then HPC Pack shrinks that node.</span></span>
* <span data-ttu-id="0d0b1-171">**ExtraNodesGrowRatio** -pourcentage supplémentaire de toogrow de nœuds pour les travaux de l’Interface MPI (Message Passing).</span><span class="sxs-lookup"><span data-stu-id="0d0b1-171">**ExtraNodesGrowRatio** - Additional percentage of nodes toogrow for Message Passing Interface (MPI) jobs.</span></span> <span data-ttu-id="0d0b1-172">Hello par défaut est 1, ce qui signifie que HPC Pack augmente de 1 % pour les travaux MPI nœuds.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-172">hello default value is 1, which means that HPC Pack grows nodes 1% for MPI jobs.</span></span>
* <span data-ttu-id="0d0b1-173">**GrowByMin** -commutateur tooindicate si la stratégie de croissance automatique de hello est basée sur les ressources minimales hello requis pour la tâche de hello.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-173">**GrowByMin** - Switch tooindicate whether hello autogrow policy is based on hello minimum resources required for hello job.</span></span> <span data-ttu-id="0d0b1-174">valeur par défaut Hello est false, ce qui signifie que HPC Pack augmente de nœuds pour les travaux en fonction des ressources de maximale hello requis pour les travaux de hello.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-174">hello default is false, which means that HPC Pack grows nodes for jobs based on hello maximum resources required for hello jobs.</span></span>
* <span data-ttu-id="0d0b1-175">**SoaJobGrowThreshold** -seuil d’entrant hello SOA demandes tootrigger automatique augmente le processus.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-175">**SoaJobGrowThreshold** - Threshold of incoming SOA requests tootrigger hello automatic grow process.</span></span> <span data-ttu-id="0d0b1-176">valeur par défaut de Hello est 50000.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-176">hello default value is 50000.</span></span>

  > [!NOTE]
  > <span data-ttu-id="0d0b1-177">Ce paramètre est pris en charge dans Microsoft HPC Pack 2012 R2 Update 3.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-177">This parameter is supported starting in HPC Pack 2012 R2 Update 3.</span></span>
  >
  >
* <span data-ttu-id="0d0b1-178">**SoaRequestsPerCore** -nombre de SOA entrant demandes toogrow un seul cœur.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-178">**SoaRequestsPerCore** -Number of incoming SOA requests toogrow one core.</span></span> <span data-ttu-id="0d0b1-179">valeur par défaut de Hello est 20 000.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-179">hello default value is 20000.</span></span>

  > [!NOTE]
  > <span data-ttu-id="0d0b1-180">Ce paramètre est pris en charge dans Microsoft HPC Pack 2012 R2 Update 3.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-180">This parameter is supported starting in HPC Pack 2012 R2 Update 3.</span></span>
  >
* <span data-ttu-id="0d0b1-181">**ExcludeNodeGroups** – nœuds Bonjour spécifié les groupes de nœuds ne pas automatiquement augmenter et réduire.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-181">**ExcludeNodeGroups** – Nodes in hello specified node groups do not automatically grow and shrink.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="0d0b1-182">Ce paramètre est pris en charge dans HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-182">This parameter is supported starting in HPC Pack 2016.</span></span>
  >

### <a name="mpi-example"></a><span data-ttu-id="0d0b1-183">Exemple de MPI</span><span class="sxs-lookup"><span data-stu-id="0d0b1-183">MPI example</span></span>
<span data-ttu-id="0d0b1-184">Par défaut HPC Pack augmente de 1 % de nœuds supplémentaires pour des travaux MPI (**ExtraNodesGrowRatio** a la valeur too1).</span><span class="sxs-lookup"><span data-stu-id="0d0b1-184">By default HPC Pack grows 1% extra nodes for MPI jobs (**ExtraNodesGrowRatio** is set too1).</span></span> <span data-ttu-id="0d0b1-185">Hello raison est que MPI peut nécessiter plusieurs nœuds, et hello travail peut uniquement exécuté lorsque tous les nœuds sont prêtes.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-185">hello reason is that MPI may require multiple nodes, and hello job can only run when all nodes are ready.</span></span> <span data-ttu-id="0d0b1-186">Lorsque Azure démarre les nœuds, parfois un seul nœud peut-être plus toostart de temps que d’autres, à l’origine des autres nœuds toobe inactif en attendant que tooget nœud prêt.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-186">When Azure starts nodes, occasionally one node might need more time toostart than others, causing other nodes toobe idle while waiting for that node tooget ready.</span></span> <span data-ttu-id="0d0b1-187">En augmentant les nœuds supplémentaires, HPC Pack réduit le temps d’attente de cette ressource et réduit potentiellement les coûts.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-187">By growing extra nodes, HPC Pack reduces this resource waiting time, and potentially saves costs.</span></span> <span data-ttu-id="0d0b1-188">pourcentage de hello tooincrease des nœuds supplémentaires pour des travaux MPI (par exemple, % too10), exécutez une commande semblable à</span><span class="sxs-lookup"><span data-stu-id="0d0b1-188">tooincrease hello percentage of extra nodes for MPI jobs (for example, too10%), run a command similar to</span></span>

    Set-HpcClusterProperty -ExtraNodesGrowRatio 10

### <a name="soa-example"></a><span data-ttu-id="0d0b1-189">Exemple SOA</span><span class="sxs-lookup"><span data-stu-id="0d0b1-189">SOA example</span></span>
<span data-ttu-id="0d0b1-190">Par défaut, **SoaJobGrowThreshold** a la valeur too50000 et **SoaRequestsPerCore** a la valeur too200000.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-190">By default, **SoaJobGrowThreshold** is set too50000 and **SoaRequestsPerCore** is set too200000.</span></span> <span data-ttu-id="0d0b1-191">Si vous envoyez un travail SOA avec 70 000 demandes, il y a une tâche en attente et les demandes entrantes sont au nombre de 70 000.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-191">If you submit one SOA job with 70000 requests, there is one queued task and incoming requests are 70000.</span></span> <span data-ttu-id="0d0b1-192">Dans ce cas HPC Pack augmente 1 noyau pour hello en file d’attente des tâches et les demandes entrantes, croît (70000-50000) / base 20000 = 1, total augmente de 2 cœurs pour ce travail SOA dans.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-192">In this case HPC Pack grows 1 core for hello queued task, and for incoming requests, grows (70000 - 50000)/20000 = 1 core, so in total grows 2 cores for this SOA job.</span></span>

## <a name="run-hello-azureautogrowshrinkps1-script"></a><span data-ttu-id="0d0b1-193">Exécutez le script de AzureAutoGrowShrink.ps1 hello</span><span class="sxs-lookup"><span data-stu-id="0d0b1-193">Run hello AzureAutoGrowShrink.ps1 script</span></span>
### <a name="prerequisites"></a><span data-ttu-id="0d0b1-194">Composants requis</span><span class="sxs-lookup"><span data-stu-id="0d0b1-194">Prerequisites</span></span>

* <span data-ttu-id="0d0b1-195">**HPC Pack 2012 R2 Update 1 ou ultérieure cluster** - hello **AzureAutoGrowShrink.ps1** script est installé dans le dossier hello % CCP_HOME % bin.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-195">**HPC Pack 2012 R2 Update 1 or later cluster** - hello **AzureAutoGrowShrink.ps1** script is installed in hello %CCP_HOME%bin folder.</span></span> <span data-ttu-id="0d0b1-196">nœud principal du cluster Hello peut être déployé localement ou dans une machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-196">hello cluster head node can be deployed either on-premises or in an Azure VM.</span></span> <span data-ttu-id="0d0b1-197">Consultez [configurer un cluster hybride avec HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) tooget a démarré avec un nœud principal local et les nœuds de « Croissance » Azure.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-197">See [Set up a hybrid cluster with HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) tooget started with an on-premises head node and Azure "burst" nodes.</span></span> <span data-ttu-id="0d0b1-198">Consultez hello [script de déploiement IaaS de HPC Pack](hpcpack-cluster-powershell-script.md) tooquickly déployer un cluster HPC Pack dans des machines virtuelles Azure, ou utiliser un [modèle de démarrage rapide Azure](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/).</span><span class="sxs-lookup"><span data-stu-id="0d0b1-198">See hello [HPC Pack IaaS deployment script](hpcpack-cluster-powershell-script.md) tooquickly deploy an HPC Pack cluster in Azure VMs, or use an [Azure quickstart template](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/).</span></span>
* <span data-ttu-id="0d0b1-199">**Azure PowerShell 1.4.0** -script de hello actuellement dépend de cette version spécifique d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-199">**Azure PowerShell 1.4.0** - hello script currently depends on this specific version of Azure PowerShell.</span></span>
* <span data-ttu-id="0d0b1-200">**Pour un cluster avec Azure des nœuds de croissance** -exécuter le script de hello sur un ordinateur client où HPC Pack est installé, ou sur le nœud principal de hello.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-200">**For a cluster with Azure burst nodes** - Run hello script on a client computer where HPC Pack is installed, or on hello head node.</span></span> <span data-ttu-id="0d0b1-201">S’exécute sur un ordinateur client, assurez-vous que vous définissez hello $env variable : nœud principal de CCP_SCHEDULER toopoint toohello.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-201">If running on a client computer, ensure that you set hello variable $env:CCP_SCHEDULER toopoint toohello head node.</span></span> <span data-ttu-id="0d0b1-202">nœuds de « Croissance » Azure Hello doivent être ajoutés toohello cluster, mais ils peuvent être hello Not-Deployed l’état.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-202">hello Azure “burst” nodes must be added toohello cluster, but they may be in hello Not-Deployed state.</span></span>
* <span data-ttu-id="0d0b1-203">**Pour un cluster déployé dans Azure VMs (modèle de déploiement Resource Manager)** -pour un cluster d’ordinateurs virtuels de Azure déployés dans le modèle de déploiement du Gestionnaire de ressources hello, script de hello prend en charge deux méthodes d’authentification Azure : connectez-vous tooyour compte Azure script de hello toorun chaque fois (en exécutant `Login-AzureRmAccount`, ou configurer un tooauthenticate principal de service avec un certificat.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-203">**For a cluster deployed in Azure VMs (Resource Manager deployment model)** - For a cluster of Azure VMs deployed in hello Resource Manager deployment model, hello script supports two methods for Azure authentication: sign in tooyour Azure account toorun hello script every time (by running `Login-AzureRmAccount`, or configure a service principal tooauthenticate with a certificate.</span></span> <span data-ttu-id="0d0b1-204">HPC Pack fournit le script de hello **ConfigARMAutoGrowShrinkCert.ps** toocreate un principal de service avec le certificat.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-204">HPC Pack provides hello script **ConfigARMAutoGrowShrinkCert.ps** toocreate a service principal with certificate.</span></span> <span data-ttu-id="0d0b1-205">Hello script crée une application Azure Active Directory (Azure AD) et un principal de service et assigne hello contributeur rôle toohello service principal.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-205">hello script creates an Azure Active Directory (Azure AD) application and a service principal, and assigns hello Contributor role toohello service principal.</span></span> <span data-ttu-id="0d0b1-206">script de hello toorun, démarrer Azure PowerShell en tant qu’administrateur et exécutez les hello suivant les commandes :</span><span class="sxs-lookup"><span data-stu-id="0d0b1-206">toorun hello script, start Azure PowerShell  as administrator and run hello following commands:</span></span>

    ```powershell
    cd $env:CCP_HOME\bin

    Login-AzureRmAccount

    .\ConfigARMAutoGrowShrinkCert.ps1 -DisplayName “YourHpcPackAppName” -HomePage "https://YourHpcPackAppHomePage" -IdentifierUri "https://YourHpcPackAppUri" -PfxFile "d:\yourcertificate.pfx"
    ```

    <span data-ttu-id="0d0b1-207">Pour plus d’informations sur **ConfigARMAutoGrowShrinkCert.ps1**, exécutez `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-207">For more details about **ConfigARMAutoGrowShrinkCert.ps1**, run `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`,</span></span>

* <span data-ttu-id="0d0b1-208">**Pour un cluster déployé dans Azure VMs (modèle de déploiement classique)** -exécuter script de hello sur hello nœud principal, car il dépend hello **Start-hpciaasnode.ps1** et **Stop-hpciaasnode.ps1**des scripts qui y sont installés.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-208">**For a cluster deployed in Azure VMs (classic deployment model)** - Run hello script on hello head node VM, because it depends on hello **Start-HpcIaaSNode.ps1** and **Stop-HpcIaaSNode.ps1** scripts that are installed there.</span></span> <span data-ttu-id="0d0b1-209">En outre, ces scripts nécessitent un certificat de gestion Azure ou un fichier de paramètres de publication (consultez [Gérer des nœuds de calcul dans un cluster HPC Pack dans Azure](hpcpack-cluster-node-manage.md)).</span><span class="sxs-lookup"><span data-stu-id="0d0b1-209">Those scripts additionally require an Azure management certificate or publish settings file (see [Manage compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster-node-manage.md)).</span></span> <span data-ttu-id="0d0b1-210">Vérifiez que hello toutes les machines virtuelles que vous avez besoin de nœud sont déjà ajoutées toohello cluster de calcul.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-210">Make sure all hello compute node VMs you need are already added toohello cluster.</span></span> <span data-ttu-id="0d0b1-211">Ils peuvent être hello état arrêté.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-211">They may be in hello Stopped state.</span></span>



### <a name="syntax"></a><span data-ttu-id="0d0b1-212">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="0d0b1-212">Syntax</span></span>
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
### <a name="parameters"></a><span data-ttu-id="0d0b1-213">Paramètres</span><span class="sxs-lookup"><span data-stu-id="0d0b1-213">Parameters</span></span>
* <span data-ttu-id="0d0b1-214">**NodeTemplates** -hello nœud Modèles toodefine hello étendue pour hello nœuds toogrow et réduire.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-214">**NodeTemplates** - Names of hello node templates toodefine hello scope for hello nodes toogrow and shrink.</span></span> <span data-ttu-id="0d0b1-215">Si non spécifié (hello la valeur par défaut est @()), tous les nœuds de hello **AzureNodes** groupe de nœuds sont dans l’étendue lorsque **NodeType** a la valeur AzureNodes et tous les nœuds Bonjour **ComputeNodes** groupe de nœuds sont dans l’étendue lorsque **NodeType** a la valeur ComputeNodes.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-215">If not specified (hello default value is @()), all nodes in hello **AzureNodes** node group are in scope when **NodeType** has a value of AzureNodes, and all nodes in hello **ComputeNodes** node group are in scope when **NodeType** has a value of ComputeNodes.</span></span>
* <span data-ttu-id="0d0b1-216">**Les JobTemplates** -noms Hello étendue de hello modèles toodefine pour hello nœuds toogrow de la tâche.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-216">**JobTemplates** - Names of hello job templates toodefine hello scope for hello nodes toogrow.</span></span>
* <span data-ttu-id="0d0b1-217">**NodeType** : hello du type de nœud toogrow et réduire.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-217">**NodeType** - hello type of node toogrow and shrink.</span></span> <span data-ttu-id="0d0b1-218">Les valeurs prises en charge sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="0d0b1-218">Supported values are:</span></span>

  * <span data-ttu-id="0d0b1-219">**AzureNodes** : pour les nœuds Azure PaaS (extension) dans un cluster IaaS Azure ou local.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-219">**AzureNodes** – for Azure PaaS (burst) nodes in an on-premises or Azure IaaS cluster.</span></span>
  * <span data-ttu-id="0d0b1-220">**ComputeNodes** : pour les machines virtuelles à nœud de calcul uniquement dans un cluster IaaS Azure.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-220">**ComputeNodes** - for compute node VMs only in an Azure IaaS cluster.</span></span>

* <span data-ttu-id="0d0b1-221">**NumOfQueuedJobsPerNodeToGrow** -nombre de travaux en file d’attente requis toogrow un seul nœud.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-221">**NumOfQueuedJobsPerNodeToGrow** - Number of queued jobs required toogrow one node.</span></span>
* <span data-ttu-id="0d0b1-222">**NumOfQueuedJobsToGrowThreshold** -nombre de seuil de hello de hello toostart de travaux en file d’attente augmente de processus.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-222">**NumOfQueuedJobsToGrowThreshold** - hello threshold number of queued jobs toostart hello grow process.</span></span>
* <span data-ttu-id="0d0b1-223">**NumOfActiveQueuedTasksPerNodeToGrow** -nombre de hello de tâches en file d’attente actives requises toogrow un seul nœud.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-223">**NumOfActiveQueuedTasksPerNodeToGrow** - hello number of active queued tasks required toogrow one node.</span></span> <span data-ttu-id="0d0b1-224">Si **NumOfQueuedJobsPerNodeToGrow** est spécifié avec une valeur supérieure à 0, ce paramètre est ignoré.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-224">If **NumOfQueuedJobsPerNodeToGrow** is specified with a value greater than 0, this parameter is ignored.</span></span>
* <span data-ttu-id="0d0b1-225">**NumOfActiveQueuedTasksToGrowThreshold** -nombre de seuil de hello de hello de toostart les tâches actives en file d’attente augmente de processus.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-225">**NumOfActiveQueuedTasksToGrowThreshold** - hello threshold number of active queued tasks toostart hello grow process.</span></span>
* <span data-ttu-id="0d0b1-226">**NumOfInitialNodesToGrow** - hello initiale du nombre minimal de nœuds toogrow si tous les nœuds hello dans la portée sont **Not-Deployed** ou **arrêté (désalloué)**.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-226">**NumOfInitialNodesToGrow** - hello initial minimum number of nodes toogrow if all hello nodes in scope are **Not-Deployed** or **Stopped (Deallocated)**.</span></span>
* <span data-ttu-id="0d0b1-227">**GrowCheckIntervalMins** -intervalle hello en minutes entre les vérifications toogrow.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-227">**GrowCheckIntervalMins** - hello interval in minutes between checks toogrow.</span></span>
* <span data-ttu-id="0d0b1-228">**ShrinkCheckIntervalMins** -intervalle hello en minutes entre les vérifications tooshrink.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-228">**ShrinkCheckIntervalMins** - hello interval in minutes between checks tooshrink.</span></span>
* <span data-ttu-id="0d0b1-229">**ShrinkCheckIdleTimes** -hello du nombre de vérifications de réduction continue (séparés par des **ShrinkCheckIntervalMins**) tooindicate hello nœuds sont inactifs.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-229">**ShrinkCheckIdleTimes** - hello number of continuous shrink checks (separated by **ShrinkCheckIntervalMins**) tooindicate hello nodes are idle.</span></span>
* <span data-ttu-id="0d0b1-230">**UseLastConfigurations** -hello configurations précédemment enregistrées dans le fichier d’arguments hello.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-230">**UseLastConfigurations** - hello previous configurations saved in hello argument file.</span></span>
* <span data-ttu-id="0d0b1-231">**ArgFile**: hello nom de toosave de fichier utilisé argument hello et mettre à jour hello configurations toorun hello script.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-231">**ArgFile**- hello name of hello argument file used toosave and update hello configurations toorun hello script.</span></span>
* <span data-ttu-id="0d0b1-232">**Préfixe_du_fichier_journal** -hello préfixe nom du fichier journal de hello.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-232">**LogFilePrefix** - hello prefix name of hello log file.</span></span> <span data-ttu-id="0d0b1-233">Vous pouvez spécifier un chemin d’accès.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-233">You can specify a path.</span></span> <span data-ttu-id="0d0b1-234">Par défaut des journaux de hello sont écrite toohello répertoire de travail actuel.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-234">By default hello log is written toohello current working directory.</span></span>

### <a name="example-1"></a><span data-ttu-id="0d0b1-235">Exemple 1</span><span class="sxs-lookup"><span data-stu-id="0d0b1-235">Example 1</span></span>
<span data-ttu-id="0d0b1-236">Hello exemple suivant configure hello Azure déployés avec le modèle AzureNode par défaut toogrow des nœuds de croissance et la réduction automatique.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-236">hello following example configures hello Azure burst nodes deployed with the Default AzureNode Template toogrow and shrink automatically.</span></span> <span data-ttu-id="0d0b1-237">Si tous les nœuds sont initialement Bonjour **Not-Deployed** d’état, au moins 3 nœuds sont démarrés.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-237">If all the nodes are initially in hello **Not-Deployed** state, at least 3 nodes are started.</span></span> <span data-ttu-id="0d0b1-238">Si le nombre de hello de travaux en file d’attente dépasse 8, script de hello démarre les nœuds jusqu'à ce que leur nombre dépasse hello des taux de travaux en file d’attente à **NumOfQueuedJobsPerNodeToGrow**.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-238">If hello number of queued jobs exceeds 8, hello script starts nodes until their number exceeds hello ratio of queued jobs to **NumOfQueuedJobsPerNodeToGrow**.</span></span> <span data-ttu-id="0d0b1-239">Si un nœud est toobe inactif à 3 reprises, il est arrêté.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-239">If a node is found toobe idle in 3 consecutive idle times, it is stopped.</span></span>

```powershell
.\AzureAutoGrowShrink.ps1 -NodeTemplates @('Default AzureNode
 Template') -NodeType AzureNodes -NumOfQueuedJobsPerNodeToGrow 5
 -NumOfQueuedJobsToGrowThreshold 8 -NumOfInitialNodesToGrow 3
 -GrowCheckIntervalMins 1 -ShrinkCheckIntervalMins 1 -ShrinkCheckIdleTimes 3
```

### <a name="example-2"></a><span data-ttu-id="0d0b1-240">Exemple 2</span><span class="sxs-lookup"><span data-stu-id="0d0b1-240">Example 2</span></span>
<span data-ttu-id="0d0b1-241">Hello exemple suivant configure hello Azure déployés avec hello modèle ComputeNode par défaut toogrow de machines virtuelles de nœud de calcul et la réduction automatique.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-241">hello following example configures hello Azure compute node VMs deployed with hello Default ComputeNode Template toogrow and shrink automatically.</span></span>
<span data-ttu-id="0d0b1-242">travaux Hello configuré par le modèle de projet par défaut hello définir étendue hello de la charge de travail sur le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-242">hello jobs configured by hello Default job template define hello scope of the workload on hello cluster.</span></span> <span data-ttu-id="0d0b1-243">Si tous les nœuds de hello sont initialement arrêtés, au moins 5 nœuds sont démarré.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-243">If all hello nodes are initially stopped, at least 5 nodes are started.</span></span> <span data-ttu-id="0d0b1-244">Si le nombre de hello de tâches en file d’attente actives est supérieur à 15, script de hello démarre les nœuds jusqu'à ce que leur nombre dépasse le taux de hello de tâches en file d’attente actives trop**NumOfActiveQueuedTasksPerNodeToGrow**.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-244">If hello number of active queued tasks exceeds 15, hello script starts nodes until their number exceeds hello ratio of active queued tasks too**NumOfActiveQueuedTasksPerNodeToGrow**.</span></span> <span data-ttu-id="0d0b1-245">Si un nœud est toobe inactif à 10 reprises, il est arrêté.</span><span class="sxs-lookup"><span data-stu-id="0d0b1-245">If a node is found toobe idle in 10 consecutive idle times, it is stopped.</span></span>

```powershell
.\AzureAutoGrowShrink.ps1 -NodeTemplates 'Default ComputeNode Template' -JobTemplates 'Default' -NodeType ComputeNodes -NumOfActiveQueuedTasksPerNodeToGrow 10 -NumOfActiveQueuedTasksToGrowThreshold 15 -NumOfInitialNodesToGrow 5 -GrowCheckIntervalMins 1 -ShrinkCheckIntervalMins 1 -ShrinkCheckIdleTimes 10 -ArgFile 'IaaSVMComputeNodes_Arg.xml' -LogFilePrefix 'IaaSVMComputeNodes_log'
```
