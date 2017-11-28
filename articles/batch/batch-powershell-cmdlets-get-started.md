---
title: aaaGet main de PowerShell pour Azure Batch | Documents Microsoft
description: "Une brève introduction toohello applets de commande PowerShell de Azure vous pouvez utiliser les ressources de traitement par lots toomanage."
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: f9ad62c5-27bf-4e6b-a5bf-c5f5914e6199
ms.service: batch
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: powershell
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3e4d12e9c1e52a5b2db2dd44346edda93b7ef92b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-batch-resources-with-powershell-cmdlets"></a><span data-ttu-id="563ba-103">Gérer les ressources Batch avec les applets de commande PowerShell</span><span class="sxs-lookup"><span data-stu-id="563ba-103">Manage Batch resources with PowerShell cmdlets</span></span>

<span data-ttu-id="563ba-104">Avec hello applets de commande PowerShell de traitement par lots Azure, vous pouvez effectuer et script nombreux hello mêmes tâches mener avec hello API de lot, hello portail Azure et hello Azure Interface de ligne de commande (CLI).</span><span class="sxs-lookup"><span data-stu-id="563ba-104">With hello Azure Batch PowerShell cmdlets, you can perform and script many of hello same tasks you carry out with hello Batch APIs, hello Azure portal, and hello Azure Command-Line Interface (CLI).</span></span> <span data-ttu-id="563ba-105">Il s’agit d’un applets de commande brève introduction toohello, vous pouvez utiliser toomanage vos comptes de lot et travailler avec vos ressources de traitement par lots telles que les pools, les travaux et les tâches.</span><span class="sxs-lookup"><span data-stu-id="563ba-105">This is a quick introduction toohello cmdlets you can use toomanage your Batch accounts and work with your Batch resources such as pools, jobs, and tasks.</span></span>

<span data-ttu-id="563ba-106">Pour obtenir une liste complète des applets de commande de lot et la syntaxe de l’applet de commande détaillées, consultez hello [référence d’applet de commande Azure Batch](/powershell/module/azurerm.batch/#batch).</span><span class="sxs-lookup"><span data-stu-id="563ba-106">For a complete list of Batch cmdlets and detailed cmdlet syntax, see hello [Azure Batch cmdlet reference](/powershell/module/azurerm.batch/#batch).</span></span>

<span data-ttu-id="563ba-107">Cet article est basé sur les applets de commande d’Azure PowerShell version 3.0.0.</span><span class="sxs-lookup"><span data-stu-id="563ba-107">This article is based on cmdlets in Azure PowerShell version 3.0.0.</span></span> <span data-ttu-id="563ba-108">Nous recommandons de mettre votre Azure PowerShell fréquemment tootake parti du service mises à jour et améliorations.</span><span class="sxs-lookup"><span data-stu-id="563ba-108">We recommend that you update your Azure PowerShell frequently tootake advantage of service updates and enhancements.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="563ba-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="563ba-109">Prerequisites</span></span>
<span data-ttu-id="563ba-110">Effectuer hello suivant operations toouse Azure PowerShell toomanage vos ressources de traitement par lots.</span><span class="sxs-lookup"><span data-stu-id="563ba-110">Perform hello following operations toouse Azure PowerShell toomanage your Batch resources.</span></span>

* [<span data-ttu-id="563ba-111">Installation et configuration d'Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="563ba-111">Install and configure Azure PowerShell</span></span>](/powershell/azure/overview)
* <span data-ttu-id="563ba-112">Exécutez hello **AzureRmAccount de connexion** applet de commande tooconnect tooyour abonnement (hello ship applets de commande de traitement par lots Azure dans le module du Gestionnaire de ressources Azure hello) :</span><span class="sxs-lookup"><span data-stu-id="563ba-112">Run hello **Login-AzureRmAccount** cmdlet tooconnect tooyour subscription (hello Azure Batch cmdlets ship in hello Azure Resource Manager module):</span></span>
  
    `Login-AzureRmAccount`
* <span data-ttu-id="563ba-113">**Inscrire auprès d’espace de noms hello lot fournisseur**.</span><span class="sxs-lookup"><span data-stu-id="563ba-113">**Register with hello Batch provider namespace**.</span></span> <span data-ttu-id="563ba-114">Cette opération ne doit toobe effectuée **une fois par abonnement**.</span><span class="sxs-lookup"><span data-stu-id="563ba-114">This operation only needs toobe performed **once per subscription**.</span></span>
  
    `Register-AzureRMResourceProvider -ProviderNamespace Microsoft.Batch`

## <a name="manage-batch-accounts-and-keys"></a><span data-ttu-id="563ba-115">Gestion des clés et des comptes Batch</span><span class="sxs-lookup"><span data-stu-id="563ba-115">Manage Batch accounts and keys</span></span>
### <a name="create-a-batch-account"></a><span data-ttu-id="563ba-116">Création d’un compte Batch</span><span class="sxs-lookup"><span data-stu-id="563ba-116">Create a Batch account</span></span>
<span data-ttu-id="563ba-117">**New-AzureBatchAccount** crée un compte Batch dans un groupe de ressources spécifié.</span><span class="sxs-lookup"><span data-stu-id="563ba-117">**New-AzureRmBatchAccount** creates a Batch account in a specified resource group.</span></span> <span data-ttu-id="563ba-118">Si vous n’avez pas déjà un groupe de ressources, créez-le en exécutant hello [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="563ba-118">If you don't already have a resource group, create one by running hello [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet.</span></span> <span data-ttu-id="563ba-119">Spécifiez l’une des hello Azure régions Bonjour **emplacement** paramètre, comme « Centre des États-Unis ».</span><span class="sxs-lookup"><span data-stu-id="563ba-119">Specify one of hello Azure regions in hello **Location** parameter, such as "Central US".</span></span> <span data-ttu-id="563ba-120">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="563ba-120">For example:</span></span>

    New-AzureRmResourceGroup –Name MyBatchResourceGroup –location "Central US"

<span data-ttu-id="563ba-121">Ensuite, créez un compte de traitement par lots dans le groupe de ressources hello, en spécifiant un nom de compte hello dans <*account_name*> hello emplacement et au nom de votre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="563ba-121">Then, create a Batch account in hello resource group, specifying a name for hello account in <*account_name*> and hello location and name of your resource group.</span></span> <span data-ttu-id="563ba-122">Création du compte Batch hello peut prendre quelques toocomplete de temps.</span><span class="sxs-lookup"><span data-stu-id="563ba-122">Creating hello Batch account can take some time toocomplete.</span></span> <span data-ttu-id="563ba-123">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="563ba-123">For example:</span></span>

    New-AzureRmBatchAccount –AccountName <account_name> –Location "Central US" –ResourceGroupName <res_group_name>

> [!NOTE]
> <span data-ttu-id="563ba-124">compte de traitement par lots Hello nom doit être unique toohello région Azure pour le groupe de ressources hello, contenir entre 3 et 24 caractères et utiliser des lettres minuscules et chiffres uniquement.</span><span class="sxs-lookup"><span data-stu-id="563ba-124">hello Batch account name must be unique toohello Azure region for hello resource group, contain between 3 and 24 characters, and use lowercase letters and numbers only.</span></span>
> 
> 

### <a name="get-account-access-keys"></a><span data-ttu-id="563ba-125">Obtenir les clés d'accès au compte</span><span class="sxs-lookup"><span data-stu-id="563ba-125">Get account access keys</span></span>
<span data-ttu-id="563ba-126">**Get-AzureRmBatchAccountKeys** affiche hello les clés d’accès associés à un compte Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="563ba-126">**Get-AzureRmBatchAccountKeys** shows hello access keys associated with an Azure Batch account.</span></span> <span data-ttu-id="563ba-127">Par exemple, exécutez hello suivant tooget hello principal et secondaire les clés du compte hello créé.</span><span class="sxs-lookup"><span data-stu-id="563ba-127">For example, run hello following tooget hello primary and secondary keys of hello account you created.</span></span>

    $Account = Get-AzureRmBatchAccountKeys –AccountName <account_name>

    $Account.PrimaryAccountKey

    $Account.SecondaryAccountKey

### <a name="generate-a-new-access-key"></a><span data-ttu-id="563ba-128">Générer une nouvelle clé d'accès</span><span class="sxs-lookup"><span data-stu-id="563ba-128">Generate a new access key</span></span>
<span data-ttu-id="563ba-129">**New-AzureRmBatchAccountKey** génère une nouvelle clé de compte primaire ou secondaire pour un compte Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="563ba-129">**New-AzureRmBatchAccountKey** generates a new primary or secondary account key for an Azure Batch account.</span></span> <span data-ttu-id="563ba-130">Par exemple, toogenerate une nouvelle clé primaire pour votre compte Batch, tapez :</span><span class="sxs-lookup"><span data-stu-id="563ba-130">For example, toogenerate a new primary key for your Batch account, type:</span></span>

    New-AzureRmBatchAccountKey -AccountName <account_name> -KeyType Primary

> [!NOTE]
> <span data-ttu-id="563ba-131">toogenerate une nouvelle clé secondaire, spécifiez « Base de données secondaire » pour hello **KeyType** paramètre.</span><span class="sxs-lookup"><span data-stu-id="563ba-131">toogenerate a new secondary key, specify "Secondary" for hello **KeyType** parameter.</span></span> <span data-ttu-id="563ba-132">Vous avez des clés primaires et secondaires du hello tooregenerate séparément.</span><span class="sxs-lookup"><span data-stu-id="563ba-132">You have tooregenerate hello primary and secondary keys separately.</span></span>
> 
> 

### <a name="delete-a-batch-account"></a><span data-ttu-id="563ba-133">Suppression d’un compte Batch</span><span class="sxs-lookup"><span data-stu-id="563ba-133">Delete a Batch account</span></span>
<span data-ttu-id="563ba-134">**Remove-AzureRmBatchAccount** supprime un compte Batch.</span><span class="sxs-lookup"><span data-stu-id="563ba-134">**Remove-AzureRmBatchAccount** deletes a Batch account.</span></span> <span data-ttu-id="563ba-135">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="563ba-135">For example:</span></span>

    Remove-AzureRmBatchAccount -AccountName <account_name>

<span data-ttu-id="563ba-136">Lorsque vous y êtes invité, confirmez que tooremove hello compte.</span><span class="sxs-lookup"><span data-stu-id="563ba-136">When prompted, confirm you want tooremove hello account.</span></span> <span data-ttu-id="563ba-137">La suppression du compte peut prendre quelques toocomplete de temps.</span><span class="sxs-lookup"><span data-stu-id="563ba-137">Account removal can take some time toocomplete.</span></span>

## <a name="create-a-batchaccountcontext-object"></a><span data-ttu-id="563ba-138">Créer un objet BatchAccountContext</span><span class="sxs-lookup"><span data-stu-id="563ba-138">Create a BatchAccountContext object</span></span>
<span data-ttu-id="563ba-139">à l’aide de tooauthenticate hello les applets de commande PowerShell de lot lorsque vous créez et gérez des pools de lot, travaux, tâches, et d’autres ressources, d’abord créer un toostore d’objet BatchAccountContext votre nom de compte et les clés :</span><span class="sxs-lookup"><span data-stu-id="563ba-139">tooauthenticate using hello Batch PowerShell cmdlets when you create and manage Batch pools, jobs, tasks, and other resources, first create a BatchAccountContext object toostore your account name and keys:</span></span>

    $context = Get-AzureRmBatchAccountKeys -AccountName <account_name>

<span data-ttu-id="563ba-140">Vous passez l’objet de BatchAccountContext de hello dans les applets de commande que hello utilisation **BatchContext** paramètre.</span><span class="sxs-lookup"><span data-stu-id="563ba-140">You pass hello BatchAccountContext object into cmdlets that use hello **BatchContext** parameter.</span></span>

> [!NOTE]
> <span data-ttu-id="563ba-141">Par défaut, les clé primaire du compte hello sont utilisé pour l’authentification, mais vous pouvez sélectionner explicitement les toouse clé hello en modifiant l’objet BatchAccountContext **KeyInUse** propriété : `$context.KeyInUse = "Secondary"`.</span><span class="sxs-lookup"><span data-stu-id="563ba-141">By default, hello account's primary key is used for authentication, but you can explicitly select hello key toouse by changing your BatchAccountContext object’s **KeyInUse** property: `$context.KeyInUse = "Secondary"`.</span></span>
> 
> 

## <a name="create-and-modify-batch-resources"></a><span data-ttu-id="563ba-142">Créer et modifier les ressources Batch</span><span class="sxs-lookup"><span data-stu-id="563ba-142">Create and modify Batch resources</span></span>
<span data-ttu-id="563ba-143">Utilisez les applets de commande telles que **New-AzureBatchPool**, **New-AzureBatchJob**, et **New-AzureBatchTask** ressources toocreate sous un compte de traitement par lots.</span><span class="sxs-lookup"><span data-stu-id="563ba-143">Use cmdlets such as **New-AzureBatchPool**, **New-AzureBatchJob**, and **New-AzureBatchTask** toocreate resources under a Batch account.</span></span> <span data-ttu-id="563ba-144">Des correspondants **Get -** et **Set -** propriétés de hello tooupdate applets de commande de ressources existants, et **Remove -** applets de commande des ressources de tooremove sous un compte de traitement par lots.</span><span class="sxs-lookup"><span data-stu-id="563ba-144">There are corresponding **Get-** and **Set-** cmdlets tooupdate hello properties of existing resources, and  **Remove-** cmdlets tooremove resources under a Batch account.</span></span>

<span data-ttu-id="563ba-145">Lorsque vous utilisez la plupart de ces applets de commande dans Ajout toopassing un objet BatchContext, vous devez toocreate ou passez les objets qui contiennent des paramètres de ressource détaillées, comme illustré dans hello l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="563ba-145">When using many of these cmdlets, in addition toopassing a BatchContext object, you need toocreate or pass objects that contain detailed resource settings, as shown in hello following example.</span></span> <span data-ttu-id="563ba-146">Consultez hello détaillées aide pour chaque applet de commande pour obtenir des exemples supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="563ba-146">See hello detailed help for each cmdlet for additional examples.</span></span>

### <a name="create-a-batch-pool"></a><span data-ttu-id="563ba-147">Créer un pool Batch</span><span class="sxs-lookup"><span data-stu-id="563ba-147">Create a Batch pool</span></span>
<span data-ttu-id="563ba-148">Lors de la création ou de mise à jour d’un pool de traitement par lots, sélectionnez configuration du service cloud hello ou configuration d’ordinateur virtuel hello pour hello système d’exploitation sur hello nœuds de calcul (consultez [vue d’ensemble de lot](batch-api-basics.md#pool)).</span><span class="sxs-lookup"><span data-stu-id="563ba-148">When creating or updating a Batch pool, you select either hello cloud service configuration or hello virtual machine configuration for hello operating system on hello compute nodes (see [Batch feature overview](batch-api-basics.md#pool)).</span></span> <span data-ttu-id="563ba-149">Si vous spécifiez la configuration du service cloud hello, vos nœuds de calcul sont une image avec l’un des hello [mises à jour de système d’exploitation invité de Azure](../cloud-services/cloud-services-guestos-update-matrix.md#releases).</span><span class="sxs-lookup"><span data-stu-id="563ba-149">If you specify hello cloud service configuration, your compute nodes are imaged with one of hello [Azure Guest OS releases](../cloud-services/cloud-services-guestos-update-matrix.md#releases).</span></span> <span data-ttu-id="563ba-150">Si vous spécifiez la configuration d’ordinateur virtuel hello, vous pouvez spécifier un Hello pris en charge de Linux ou hello répertorié dans l’image de machine virtuelle Windows [Azure Marketplace de Machines virtuelles][vm_marketplace], ou fournissez un personnalisé image que vous avez préparé.</span><span class="sxs-lookup"><span data-stu-id="563ba-150">If you specify hello virtual machine configuration, you can either specify one of hello supported Linux or Windows VM images listed in hello [Azure Virtual Machines Marketplace][vm_marketplace], or provide a custom image that you have prepared.</span></span>

<span data-ttu-id="563ba-151">Lorsque vous exécutez **New-AzureBatchPool**, passer des paramètres de système d’exploitation hello dans un objet PSCloudServiceConfiguration ou PSVirtualMachineConfiguration.</span><span class="sxs-lookup"><span data-stu-id="563ba-151">When you run **New-AzureBatchPool**, pass hello operating system settings in a PSCloudServiceConfiguration or PSVirtualMachineConfiguration object.</span></span> <span data-ttu-id="563ba-152">Par exemple, hello applet de commande suivante crée un nouveau pool de traitement par lots avec les nœuds de calcul de petite taille dans la configuration du service cloud hello, une image avec la dernière version de système d’exploitation hello de famille 3 (Windows Server 2012).</span><span class="sxs-lookup"><span data-stu-id="563ba-152">For example, hello following cmdlet creates a new Batch pool with size Small compute nodes in hello cloud service configuration, imaged with hello latest operating system version of family 3 (Windows Server 2012).</span></span> <span data-ttu-id="563ba-153">Ici, hello **CloudServiceConfiguration** paramètre spécifie hello *$configuration* variable en tant qu’objet PSCloudServiceConfiguration hello.</span><span class="sxs-lookup"><span data-stu-id="563ba-153">Here, hello **CloudServiceConfiguration** parameter specifies hello *$configuration* variable as hello PSCloudServiceConfiguration object.</span></span> <span data-ttu-id="563ba-154">Hello **BatchContext** paramètre spécifie une variable précédemment définie *$context* en tant qu’objet BatchAccountContext hello.</span><span class="sxs-lookup"><span data-stu-id="563ba-154">hello **BatchContext** parameter specifies a previously defined variable *$context* as hello BatchAccountContext object.</span></span>

    $configuration = New-Object -TypeName "Microsoft.Azure.Commands.Batch.Models.PSCloudServiceConfiguration" -ArgumentList @(4,"*")

    New-AzureBatchPool -Id "AutoScalePool" -VirtualMachineSize "Small" -CloudServiceConfiguration $configuration -AutoScaleFormula '$TargetDedicated=4;' -BatchContext $context

<span data-ttu-id="563ba-155">nombre de cible de Hello de nœuds de calcul dans un nouveau pool de hello est déterminé par une formule de l’échelle automatique.</span><span class="sxs-lookup"><span data-stu-id="563ba-155">hello target number of compute nodes in hello new pool is determined by an autoscaling formula.</span></span> <span data-ttu-id="563ba-156">Dans ce cas, la formule de hello est simplement **$TargetDedicated = 4**, indiquant le nombre de hello de nœuds de calcul dans le pool de hello est au maximum de 4.</span><span class="sxs-lookup"><span data-stu-id="563ba-156">In this case, hello formula is simply **$TargetDedicated=4**, indicating hello number of compute nodes in hello pool is 4 at most.</span></span>

## <a name="query-for-pools-jobs-tasks-and-other-details"></a><span data-ttu-id="563ba-157">Requête relative aux pools, aux travaux, aux tâches et autres détails</span><span class="sxs-lookup"><span data-stu-id="563ba-157">Query for pools, jobs, tasks, and other details</span></span>
<span data-ttu-id="563ba-158">Utilisez les applets de commande telles que **Get-AzureBatchPool**, **Get-AzureBatchJob**, et **Get-AzureBatchTask** tooquery pour les entités créées sous un compte Batch.</span><span class="sxs-lookup"><span data-stu-id="563ba-158">Use cmdlets such as **Get-AzureBatchPool**, **Get-AzureBatchJob**, and **Get-AzureBatchTask** tooquery for entities created under a Batch account.</span></span>

### <a name="query-for-data"></a><span data-ttu-id="563ba-159">Interrogation des données</span><span class="sxs-lookup"><span data-stu-id="563ba-159">Query for data</span></span>
<span data-ttu-id="563ba-160">Par exemple, utilisez **Get-AzureBatchPools** toofind vos pools.</span><span class="sxs-lookup"><span data-stu-id="563ba-160">As an example, use **Get-AzureBatchPools** toofind your pools.</span></span> <span data-ttu-id="563ba-161">Par défaut il interroge pour tous les pools sous votre compte, en supposant que vous déjà stockée objet hello BatchAccountContext *$context*:</span><span class="sxs-lookup"><span data-stu-id="563ba-161">By default this queries for all pools under your account, assuming you already stored hello BatchAccountContext object in *$context*:</span></span>

    Get-AzureBatchPool -BatchContext $context

### <a name="use-an-odata-filter"></a><span data-ttu-id="563ba-162">Utilisation d’un filtre OData</span><span class="sxs-lookup"><span data-stu-id="563ba-162">Use an OData filter</span></span>
<span data-ttu-id="563ba-163">Vous pouvez fournir un filtre OData à l’aide de hello **filtre** paramètre toofind hello uniquement les objets qui vous intéressent.</span><span class="sxs-lookup"><span data-stu-id="563ba-163">You can supply an OData filter using hello **Filter** parameter toofind only hello objects you’re interested in.</span></span> <span data-ttu-id="563ba-164">Par exemple, vous pouvez rechercher tous les pools dont l’identificateur commence par « myPool » :</span><span class="sxs-lookup"><span data-stu-id="563ba-164">For example, you can find all pools with ids starting with “myPool”:</span></span>

    $filter = "startswith(id,'myPool')"

    Get-AzureBatchPool -Filter $filter -BatchContext $context

<span data-ttu-id="563ba-165">Cette méthode n'est pas aussi flexible que l'utilisation de « Where-Object » dans un pipeline local.</span><span class="sxs-lookup"><span data-stu-id="563ba-165">This method is not as flexible as using “Where-Object” in a local pipeline.</span></span> <span data-ttu-id="563ba-166">Toutefois, les requêtes hello sont envoyées toohello service Batch directement afin que tout le filtrage se produit côté serveur de hello, l’enregistrement de la bande passante Internet.</span><span class="sxs-lookup"><span data-stu-id="563ba-166">However, hello query gets sent toohello Batch service directly so that all filtering happens on hello server side, saving Internet bandwidth.</span></span>

### <a name="use-hello-id-parameter"></a><span data-ttu-id="563ba-167">Utilisez le paramètre d’Id hello</span><span class="sxs-lookup"><span data-stu-id="563ba-167">Use hello Id parameter</span></span>
<span data-ttu-id="563ba-168">Un filtre d’OData autre tooan est toouse hello **Id** paramètre.</span><span class="sxs-lookup"><span data-stu-id="563ba-168">An alternative tooan OData filter is toouse hello **Id** parameter.</span></span> <span data-ttu-id="563ba-169">tooquery pour un pool spécifique avec l’id « monpool » :</span><span class="sxs-lookup"><span data-stu-id="563ba-169">tooquery for a specific pool with id "myPool":</span></span>

    Get-AzureBatchPool -Id "myPool" -BatchContext $context

<span data-ttu-id="563ba-170">Hello **Id** paramètre prend en charge uniquement intégral-id recherche, pas les caractères génériques ou les filtres OData-style.</span><span class="sxs-lookup"><span data-stu-id="563ba-170">hello **Id** parameter supports only full-id search, not wildcards or OData-style filters.</span></span>

### <a name="use-hello-maxcount-parameter"></a><span data-ttu-id="563ba-171">Utilisez le paramètre MaxCount de hello</span><span class="sxs-lookup"><span data-stu-id="563ba-171">Use hello MaxCount parameter</span></span>
<span data-ttu-id="563ba-172">Par défaut, chaque applet de commande retourne un maximum de 1 000 objets.</span><span class="sxs-lookup"><span data-stu-id="563ba-172">By default, each cmdlet returns a maximum of 1000 objects.</span></span> <span data-ttu-id="563ba-173">Si vous atteignez cette limite, affinez votre toobring filtre précédent moins d’objets, ou définir explicitement la valeur maximale à l’aide de hello **MaxCount** paramètre.</span><span class="sxs-lookup"><span data-stu-id="563ba-173">If you reach this limit, either refine your filter toobring back fewer objects, or explicitly set a maximum using hello **MaxCount** parameter.</span></span> <span data-ttu-id="563ba-174">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="563ba-174">For example:</span></span>

    Get-AzureBatchTask -MaxCount 2500 -BatchContext $context

<span data-ttu-id="563ba-175">limite supérieure de hello tooremove, définissez **MaxCount** too0 ou moins.</span><span class="sxs-lookup"><span data-stu-id="563ba-175">tooremove hello upper bound, set **MaxCount** too0 or less.</span></span>

### <a name="use-hello-powershell-pipeline"></a><span data-ttu-id="563ba-176">Utiliser le pipeline de PowerShell hello</span><span class="sxs-lookup"><span data-stu-id="563ba-176">Use hello PowerShell pipeline</span></span>
<span data-ttu-id="563ba-177">Applets de commande de traitement par lots peut tirer parti des données de toosend hello PowerShell pipeline entre applets de commande.</span><span class="sxs-lookup"><span data-stu-id="563ba-177">Batch cmdlets can leverage hello PowerShell pipeline toosend data between cmdlets.</span></span> <span data-ttu-id="563ba-178">Cela a hello même effet que la spécification d’un paramètre, mais facilite l’utilisation avec plusieurs entités plus facile.</span><span class="sxs-lookup"><span data-stu-id="563ba-178">This has hello same effect as specifying a parameter, but makes working with multiple entities easier.</span></span>

<span data-ttu-id="563ba-179">Par exemple, recherchez et affichez toutes les tâches sous votre compte :</span><span class="sxs-lookup"><span data-stu-id="563ba-179">For example, find and display all tasks under your account:</span></span>

    Get-AzureBatchJob -BatchContext $context | Get-AzureBatchTask -BatchContext $context

<span data-ttu-id="563ba-180">Redémarrez chaque nœud de calcul dans un pool :</span><span class="sxs-lookup"><span data-stu-id="563ba-180">Restart (reboot) every compute node in a pool:</span></span>

    Get-AzureBatchComputeNode -PoolId "myPool" -BatchContext $context | Restart-AzureBatchComputeNode -BatchContext $context

## <a name="application-package-management"></a><span data-ttu-id="563ba-181">Gestion des packages d’application</span><span class="sxs-lookup"><span data-stu-id="563ba-181">Application package management</span></span>
<span data-ttu-id="563ba-182">Les packages d’applications permettent simplifié toodeploy applications toohello nœuds de calcul dans les pools.</span><span class="sxs-lookup"><span data-stu-id="563ba-182">Application packages provide a simplified way toodeploy applications toohello compute nodes in your pools.</span></span> <span data-ttu-id="563ba-183">Avec hello applets de commande PowerShell de lot, vous pouvez télécharger et gérer des packages d’application dans votre compte Batch et déployer des nœuds de toocompute de versions de package.</span><span class="sxs-lookup"><span data-stu-id="563ba-183">With hello Batch PowerShell cmdlets, you can upload and manage application packages in your Batch account, and deploy package versions toocompute nodes.</span></span>

<span data-ttu-id="563ba-184">**Créez** une application :</span><span class="sxs-lookup"><span data-stu-id="563ba-184">**Create** an application:</span></span>

    New-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

<span data-ttu-id="563ba-185">**Ajoutez** un package d’application :</span><span class="sxs-lookup"><span data-stu-id="563ba-185">**Add** an application package:</span></span>

    New-AzureRmBatchApplicationPackage -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -ApplicationVersion "1.0" -Format zip -FilePath package001.zip

<span data-ttu-id="563ba-186">Ensemble hello **version par défaut** pour l’application hello :</span><span class="sxs-lookup"><span data-stu-id="563ba-186">Set hello **default version** for hello application:</span></span>

    Set-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -DefaultVersion "1.0"

<span data-ttu-id="563ba-187">**Répertorier** les packages d’une application</span><span class="sxs-lookup"><span data-stu-id="563ba-187">**List** an application's packages</span></span>

    $application = Get-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

    $application.ApplicationPackages

<span data-ttu-id="563ba-188">**Supprimer** un package d’application</span><span class="sxs-lookup"><span data-stu-id="563ba-188">**Delete** an application package</span></span>

    Remove-AzureRmBatchApplicationPackage -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -ApplicationVersion "1.0"

<span data-ttu-id="563ba-189">**Supprimer** une application</span><span class="sxs-lookup"><span data-stu-id="563ba-189">**Delete** an application</span></span>

    Remove-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

> [!NOTE]
> <span data-ttu-id="563ba-190">Vous devez supprimer toutes les versions de package d’application d’une application avant de supprimer application hello.</span><span class="sxs-lookup"><span data-stu-id="563ba-190">You must delete all of an application's application package versions before you delete hello application.</span></span> <span data-ttu-id="563ba-191">Vous recevez une erreur « Conflit » si vous essayez de toodelete une application qui possède actuellement des packages d’applications.</span><span class="sxs-lookup"><span data-stu-id="563ba-191">You will receive a 'Conflict' error if you try toodelete an application that currently has application packages.</span></span>
> 
> 

### <a name="deploy-an-application-package"></a><span data-ttu-id="563ba-192">Déployer un package d’application</span><span class="sxs-lookup"><span data-stu-id="563ba-192">Deploy an application package</span></span>
<span data-ttu-id="563ba-193">Vous pouvez spécifier un ou plusieurs packages d’application pour le déploiement lorsque vous créez un pool.</span><span class="sxs-lookup"><span data-stu-id="563ba-193">You can specify one or more application packages for deployment when you create a pool.</span></span> <span data-ttu-id="563ba-194">Lorsque vous spécifiez un package au moment de la création du pool, il est déployé tooeach nœud en tant que pool de jointures de nœud hello.</span><span class="sxs-lookup"><span data-stu-id="563ba-194">When you specify a package at pool creation time, it is deployed tooeach node as hello node joins pool.</span></span> <span data-ttu-id="563ba-195">Les packages sont également déployés lorsqu’un nœud est redémarré ou réinitialisé.</span><span class="sxs-lookup"><span data-stu-id="563ba-195">Packages are also deployed when a node is rebooted or reimaged.</span></span>

<span data-ttu-id="563ba-196">Spécifiez hello `-ApplicationPackageReference` option lors de la création des nœuds d’un package toohello du pool d’applications un toodeploy pool dès qu’ils rejoignent le pool de hello.</span><span class="sxs-lookup"><span data-stu-id="563ba-196">Specify hello `-ApplicationPackageReference` option when creating a pool toodeploy an application package toohello pool's nodes as they join hello pool.</span></span> <span data-ttu-id="563ba-197">Commencez par créer un **PSApplicationPackageReference** de l’objet et configurez-le avec hello Id et le package de version de l’application vous souhaitez que les nœuds de calcul du pool toodeploy toohello :</span><span class="sxs-lookup"><span data-stu-id="563ba-197">First, create a **PSApplicationPackageReference** object, and configure it with hello application Id and package version you want toodeploy toohello pool's compute nodes:</span></span>

    $appPackageReference = New-Object Microsoft.Azure.Commands.Batch.Models.PSApplicationPackageReference

    $appPackageReference.ApplicationId = "MyBatchApplication"

    $appPackageReference.Version = "1.0"

<span data-ttu-id="563ba-198">Maintenant créer le pool de hello et spécifiez l’objet de référence de package hello comme hello argument toohello `ApplicationPackageReferences` option :</span><span class="sxs-lookup"><span data-stu-id="563ba-198">Now create hello pool, and specify hello package reference object as hello argument toohello `ApplicationPackageReferences` option:</span></span>

    New-AzureBatchPool -Id "PoolWithAppPackage" -VirtualMachineSize "Small" -CloudServiceConfiguration $configuration -BatchContext $context -ApplicationPackageReferences $appPackageReference

<span data-ttu-id="563ba-199">Vous trouverez plus d’informations sur les packages d’applications dans [déployer des nœuds de toocompute d’applications avec des packages d’application de lot](batch-application-packages.md).</span><span class="sxs-lookup"><span data-stu-id="563ba-199">You can find more information on application packages in [Deploy applications toocompute nodes with Batch application packages](batch-application-packages.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="563ba-200">Vous devez [lier un compte de stockage Azure](#linked-storage-account-autostorage) tooyour lot compte toouse des packages d’applications.</span><span class="sxs-lookup"><span data-stu-id="563ba-200">You must [link an Azure Storage account](#linked-storage-account-autostorage) tooyour Batch account toouse application packages.</span></span>
> 
> 

### <a name="update-a-pools-application-packages"></a><span data-ttu-id="563ba-201">Mise à jour des packages d’applications d’un pool</span><span class="sxs-lookup"><span data-stu-id="563ba-201">Update a pool's application packages</span></span>
<span data-ttu-id="563ba-202">les applications de hello tooupdate affectées tooan pool existant, d’abord créer un objet PSApplicationPackageReference avec les propriétés de hello souhaitée (version Id et le package d’application) :</span><span class="sxs-lookup"><span data-stu-id="563ba-202">tooupdate hello applications assigned tooan existing pool, first create a PSApplicationPackageReference object with hello desired properties (application Id and package version):</span></span>

    $appPackageReference = New-Object Microsoft.Azure.Commands.Batch.Models.PSApplicationPackageReference

    $appPackageReference.ApplicationId = "MyBatchApplication"

    $appPackageReference.Version = "2.0"

<span data-ttu-id="563ba-203">Ensuite, obtenir le pool de hello de lot, effacer tout package existant, ajoutez notre nouvelle référence de package et mettre à jour le service de traitement par lots hello avec de nouveaux paramètres de pool hello :</span><span class="sxs-lookup"><span data-stu-id="563ba-203">Next, get hello pool from Batch, clear out any existing packages, add our new package reference, and update hello Batch service with hello new pool settings:</span></span>

    $pool = Get-AzureBatchPool -BatchContext $context -Id "PoolWithAppPackage"

    $pool.ApplicationPackageReferences.Clear()

    $pool.ApplicationPackageReferences.Add($appPackageReference)

    Set-AzureBatchPool -BatchContext $context -Pool $pool

<span data-ttu-id="563ba-204">Vous avez maintenant mis à jour les propriétés du pool hello dans le service de traitement par lots hello.</span><span class="sxs-lookup"><span data-stu-id="563ba-204">You've now updated hello pool's properties in hello Batch service.</span></span> <span data-ttu-id="563ba-205">tooactually déployer hello nouveau package toocompute nœuds d’application dans le pool de hello, toutefois, vous devez redémarrer ou réinitialiser ces nœuds.</span><span class="sxs-lookup"><span data-stu-id="563ba-205">tooactually deploy hello new application package toocompute nodes in hello pool, however, you must restart or reimage those nodes.</span></span> <span data-ttu-id="563ba-206">Vous pouvez redémarrer tous les nœuds dans un pool avec la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="563ba-206">You can restart every node in a pool with this command:</span></span>

    Get-AzureBatchComputeNode -PoolId "PoolWithAppPackage" -BatchContext $context | Restart-AzureBatchComputeNode -BatchContext $context

> [!TIP]
> <span data-ttu-id="563ba-207">Vous pouvez déployer plusieurs applications packages toohello nœuds de calcul un pool.</span><span class="sxs-lookup"><span data-stu-id="563ba-207">You can deploy multiple application packages toohello compute nodes in a pool.</span></span> <span data-ttu-id="563ba-208">Si vous souhaitez que trop*ajouter* un package d’application au lieu de remplacer les packages hello actuellement déployé, omettez hello `$pool.ApplicationPackageReferences.Clear()` ligne ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="563ba-208">If you'd like too*add* an application package instead of replacing hello currently deployed packages, omit hello `$pool.ApplicationPackageReferences.Clear()` line above.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="563ba-209">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="563ba-209">Next steps</span></span>
* <span data-ttu-id="563ba-210">Pour connaître la syntaxe détaillée des applets de commande et obtenir des exemples, consultez les [informations de référence sur les applets de commande Azure Batch](/powershell/module/azurerm.batch/#batch).</span><span class="sxs-lookup"><span data-stu-id="563ba-210">For detailed cmdlet syntax and examples, see [Azure Batch cmdlet reference](/powershell/module/azurerm.batch/#batch).</span></span>
* <span data-ttu-id="563ba-211">Pour plus d’informations sur les applications et packages d’applications de traitement par lots, consultez [déployer des nœuds de toocompute d’applications avec des packages d’application de lot](batch-application-packages.md).</span><span class="sxs-lookup"><span data-stu-id="563ba-211">For more information about applications and application packages in Batch, see [Deploy applications toocompute nodes with Batch application packages](batch-application-packages.md).</span></span>

[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/