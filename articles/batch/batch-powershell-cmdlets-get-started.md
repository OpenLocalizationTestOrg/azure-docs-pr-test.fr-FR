---
title: "Prise en main des applets de commande PowerShell pour Azure Batch | Microsoft Docs"
description: "Brève présentation des applets de commande Azure PowerShell à utiliser pour gérer les ressources Batch."
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
ms.openlocfilehash: e33be6ed658e00250ea1e80cd7da4d348fb18296
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="manage-batch-resources-with-powershell-cmdlets"></a><span data-ttu-id="41221-103">Gérer les ressources Batch avec les applets de commande PowerShell</span><span class="sxs-lookup"><span data-stu-id="41221-103">Manage Batch resources with PowerShell cmdlets</span></span>

<span data-ttu-id="41221-104">Avec les applets de commande Azure Batch PowerShell, vous pouvez effectuer pratiquement les mêmes tâches qu’avec les API Batch, le portail Azure et l’interface de ligne de commande Azure, et en écrire les scripts.</span><span class="sxs-lookup"><span data-stu-id="41221-104">With the Azure Batch PowerShell cmdlets, you can perform and script many of the same tasks you carry out with the Batch APIs, the Azure portal, and the Azure Command-Line Interface (CLI).</span></span> <span data-ttu-id="41221-105">Il s’agit d’une présentation rapide des applets de commande que vous pouvez utiliser pour gérer vos comptes Batch et travailler avec des ressources Batch telles que les pools, les travaux et les tâches.</span><span class="sxs-lookup"><span data-stu-id="41221-105">This is a quick introduction to the cmdlets you can use to manage your Batch accounts and work with your Batch resources such as pools, jobs, and tasks.</span></span>

<span data-ttu-id="41221-106">Pour obtenir une liste complète des applets de commande Batch et la syntaxe détaillée des applets de commande, consultez [Référence d’applet de commande Azure Batch](/powershell/module/azurerm.batch/#batch).</span><span class="sxs-lookup"><span data-stu-id="41221-106">For a complete list of Batch cmdlets and detailed cmdlet syntax, see the [Azure Batch cmdlet reference](/powershell/module/azurerm.batch/#batch).</span></span>

<span data-ttu-id="41221-107">Cet article est basé sur les applets de commande d’Azure PowerShell version 3.0.0.</span><span class="sxs-lookup"><span data-stu-id="41221-107">This article is based on cmdlets in Azure PowerShell version 3.0.0.</span></span> <span data-ttu-id="41221-108">Nous vous recommandons de mettre à jour votre Azure PowerShell fréquemment pour tirer parti des améliorations et des mises à jour de service.</span><span class="sxs-lookup"><span data-stu-id="41221-108">We recommend that you update your Azure PowerShell frequently to take advantage of service updates and enhancements.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="41221-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="41221-109">Prerequisites</span></span>
<span data-ttu-id="41221-110">Effectuez les opérations suivantes pour utiliser Azure PowerShell pour gérer vos ressources de traitement par lots.</span><span class="sxs-lookup"><span data-stu-id="41221-110">Perform the following operations to use Azure PowerShell to manage your Batch resources.</span></span>

* [<span data-ttu-id="41221-111">Installation et configuration d'Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="41221-111">Install and configure Azure PowerShell</span></span>](/powershell/azure/overview)
* <span data-ttu-id="41221-112">Exécutez l’applet de commande **Login-AzureRmAccount** pour vous connecter à votre abonnement (les applets de commande Azure Batch font partie du module Azure Resource Manager) :</span><span class="sxs-lookup"><span data-stu-id="41221-112">Run the **Login-AzureRmAccount** cmdlet to connect to your subscription (the Azure Batch cmdlets ship in the Azure Resource Manager module):</span></span>
  
    `Login-AzureRmAccount`
* <span data-ttu-id="41221-113">**Inscrivez-vous dans l’espace de noms de fournisseur Batch**.</span><span class="sxs-lookup"><span data-stu-id="41221-113">**Register with the Batch provider namespace**.</span></span> <span data-ttu-id="41221-114">Cette opération ne doit être effectuée qu’**une fois par abonnement**.</span><span class="sxs-lookup"><span data-stu-id="41221-114">This operation only needs to be performed **once per subscription**.</span></span>
  
    `Register-AzureRMResourceProvider -ProviderNamespace Microsoft.Batch`

## <a name="manage-batch-accounts-and-keys"></a><span data-ttu-id="41221-115">Gestion des clés et des comptes Batch</span><span class="sxs-lookup"><span data-stu-id="41221-115">Manage Batch accounts and keys</span></span>
### <a name="create-a-batch-account"></a><span data-ttu-id="41221-116">Création d’un compte Batch</span><span class="sxs-lookup"><span data-stu-id="41221-116">Create a Batch account</span></span>
<span data-ttu-id="41221-117">**New-AzureBatchAccount** crée un compte Batch dans un groupe de ressources spécifié.</span><span class="sxs-lookup"><span data-stu-id="41221-117">**New-AzureRmBatchAccount** creates a Batch account in a specified resource group.</span></span> <span data-ttu-id="41221-118">Si vous ne disposez pas d’un groupe de ressources, créez-en un en exécutant l’applet de commande [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="41221-118">If you don't already have a resource group, create one by running the [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet.</span></span> <span data-ttu-id="41221-119">Spécifiez une des régions Azure dans le paramètre **Emplacement**, « États-Unis du Centre » par exemple.</span><span class="sxs-lookup"><span data-stu-id="41221-119">Specify one of the Azure regions in the **Location** parameter, such as "Central US".</span></span> <span data-ttu-id="41221-120">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="41221-120">For example:</span></span>

    New-AzureRmResourceGroup –Name MyBatchResourceGroup –location "Central US"

<span data-ttu-id="41221-121">Créez ensuite un compte Batch dans le groupe de ressources en spécifiant le nom du compte dans <*nom_compte*> et l’emplacement et le nom de votre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="41221-121">Then, create a Batch account in the resource group, specifying a name for the account in <*account_name*> and the location and name of your resource group.</span></span> <span data-ttu-id="41221-122">La procédure de création du compte Batch peut prendre un certain temps.</span><span class="sxs-lookup"><span data-stu-id="41221-122">Creating the Batch account can take some time to complete.</span></span> <span data-ttu-id="41221-123">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="41221-123">For example:</span></span>

    New-AzureRmBatchAccount –AccountName <account_name> –Location "Central US" –ResourceGroupName <res_group_name>

> [!NOTE]
> <span data-ttu-id="41221-124">Le nom du compte Batch doit être unique dans la région Azure du groupe de ressources, contenir entre 3 et 24 caractères, et utiliser des minuscules et des chiffres uniquement.</span><span class="sxs-lookup"><span data-stu-id="41221-124">The Batch account name must be unique to the Azure region for the resource group, contain between 3 and 24 characters, and use lowercase letters and numbers only.</span></span>
> 
> 

### <a name="get-account-access-keys"></a><span data-ttu-id="41221-125">Obtenir les clés d'accès au compte</span><span class="sxs-lookup"><span data-stu-id="41221-125">Get account access keys</span></span>
<span data-ttu-id="41221-126">**Get-AzureRmBatchAccountKeys** affiche les clés d’accès associées à un compte Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="41221-126">**Get-AzureRmBatchAccountKeys** shows the access keys associated with an Azure Batch account.</span></span> <span data-ttu-id="41221-127">Par exemple, exécutez la commande suivante pour obtenir les clés primaires et secondaires du compte que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="41221-127">For example, run the following to get the primary and secondary keys of the account you created.</span></span>

    $Account = Get-AzureRmBatchAccountKeys –AccountName <account_name>

    $Account.PrimaryAccountKey

    $Account.SecondaryAccountKey

### <a name="generate-a-new-access-key"></a><span data-ttu-id="41221-128">Générer une nouvelle clé d'accès</span><span class="sxs-lookup"><span data-stu-id="41221-128">Generate a new access key</span></span>
<span data-ttu-id="41221-129">**New-AzureRmBatchAccountKey** génère une nouvelle clé de compte primaire ou secondaire pour un compte Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="41221-129">**New-AzureRmBatchAccountKey** generates a new primary or secondary account key for an Azure Batch account.</span></span> <span data-ttu-id="41221-130">Par exemple, pour générer une nouvelle clé primaire pour votre compte Batch, tapez :</span><span class="sxs-lookup"><span data-stu-id="41221-130">For example, to generate a new primary key for your Batch account, type:</span></span>

    New-AzureRmBatchAccountKey -AccountName <account_name> -KeyType Primary

> [!NOTE]
> <span data-ttu-id="41221-131">Pour générer une nouvelle clé secondaire, spécifiez « Secondary » pour le paramètre **KeyType** .</span><span class="sxs-lookup"><span data-stu-id="41221-131">To generate a new secondary key, specify "Secondary" for the **KeyType** parameter.</span></span> <span data-ttu-id="41221-132">Vous devez régénérer les clés primaires et secondaires séparément.</span><span class="sxs-lookup"><span data-stu-id="41221-132">You have to regenerate the primary and secondary keys separately.</span></span>
> 
> 

### <a name="delete-a-batch-account"></a><span data-ttu-id="41221-133">Suppression d’un compte Batch</span><span class="sxs-lookup"><span data-stu-id="41221-133">Delete a Batch account</span></span>
<span data-ttu-id="41221-134">**Remove-AzureRmBatchAccount** supprime un compte Batch.</span><span class="sxs-lookup"><span data-stu-id="41221-134">**Remove-AzureRmBatchAccount** deletes a Batch account.</span></span> <span data-ttu-id="41221-135">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="41221-135">For example:</span></span>

    Remove-AzureRmBatchAccount -AccountName <account_name>

<span data-ttu-id="41221-136">Quand vous y êtes invité, confirmez que vous voulez supprimer le compte.</span><span class="sxs-lookup"><span data-stu-id="41221-136">When prompted, confirm you want to remove the account.</span></span> <span data-ttu-id="41221-137">La suppression du compte peut prendre un certain temps.</span><span class="sxs-lookup"><span data-stu-id="41221-137">Account removal can take some time to complete.</span></span>

## <a name="create-a-batchaccountcontext-object"></a><span data-ttu-id="41221-138">Créer un objet BatchAccountContext</span><span class="sxs-lookup"><span data-stu-id="41221-138">Create a BatchAccountContext object</span></span>
<span data-ttu-id="41221-139">Pour une authentification à l’aide des applets de commande Batch PowerShell lors de la création et la gestion des pools, des travaux, des tâches et d’autres ressources, vous devez d’abord créer un objet BatchAccountContext pour stocker vos nom et clés de compte :</span><span class="sxs-lookup"><span data-stu-id="41221-139">To authenticate using the Batch PowerShell cmdlets when you create and manage Batch pools, jobs, tasks, and other resources, first create a BatchAccountContext object to store your account name and keys:</span></span>

    $context = Get-AzureRmBatchAccountKeys -AccountName <account_name>

<span data-ttu-id="41221-140">Vous passez l’objet BatchAccountContext dans les applets de commande utilisant le paramètre **BatchContext** .</span><span class="sxs-lookup"><span data-stu-id="41221-140">You pass the BatchAccountContext object into cmdlets that use the **BatchContext** parameter.</span></span>

> [!NOTE]
> <span data-ttu-id="41221-141">Par défaut, la clé primaire du compte est utilisée pour l’authentification, mais vous pouvez sélectionner explicitement la clé à utiliser en modifiant la propriété **KeyInUse** de votre objet BatchAccountContext : `$context.KeyInUse = "Secondary"`.</span><span class="sxs-lookup"><span data-stu-id="41221-141">By default, the account's primary key is used for authentication, but you can explicitly select the key to use by changing your BatchAccountContext object’s **KeyInUse** property: `$context.KeyInUse = "Secondary"`.</span></span>
> 
> 

## <a name="create-and-modify-batch-resources"></a><span data-ttu-id="41221-142">Créer et modifier les ressources Batch</span><span class="sxs-lookup"><span data-stu-id="41221-142">Create and modify Batch resources</span></span>
<span data-ttu-id="41221-143">Utilisez les applets de commande telles que **New-AzureBatchPool**, **New-AzureBatchJob** et **New-AzureBatchTask** pour créer des ressources sous un compte Batch.</span><span class="sxs-lookup"><span data-stu-id="41221-143">Use cmdlets such as **New-AzureBatchPool**, **New-AzureBatchJob**, and **New-AzureBatchTask** to create resources under a Batch account.</span></span> <span data-ttu-id="41221-144">Il existe des applets de commande **Get-** et **Set-** correspondantes pour mettre à jour les propriétés des ressources existantes, et des applets de commande **Remove-** pour supprimer des ressources sous un compte Batch.</span><span class="sxs-lookup"><span data-stu-id="41221-144">There are corresponding **Get-** and **Set-** cmdlets to update the properties of existing resources, and  **Remove-** cmdlets to remove resources under a Batch account.</span></span>

<span data-ttu-id="41221-145">Si vous utilisez plusieurs de ces applets de commande, en plus de transmettre un objet BatchContext, vous devez créer ou transmettre les objets qui contiennent des paramètres de ressources détaillés, comme illustré dans l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="41221-145">When using many of these cmdlets, in addition to passing a BatchContext object, you need to create or pass objects that contain detailed resource settings, as shown in the following example.</span></span> <span data-ttu-id="41221-146">Pour obtenir d’autres exemples, consultez l’aide détaillée de chaque applet de commande.</span><span class="sxs-lookup"><span data-stu-id="41221-146">See the detailed help for each cmdlet for additional examples.</span></span>

### <a name="create-a-batch-pool"></a><span data-ttu-id="41221-147">Créer un pool Batch</span><span class="sxs-lookup"><span data-stu-id="41221-147">Create a Batch pool</span></span>
<span data-ttu-id="41221-148">Lors de la création ou de la mise à jour d’un pool Batch, sélectionnez une configuration de service cloud ou une configuration de machine virtuelle correspondant au système d’exploitation dans les nœuds de calcul (voir [Aperçu des fonctionnalités d’Azure Batch](batch-api-basics.md#pool)).</span><span class="sxs-lookup"><span data-stu-id="41221-148">When creating or updating a Batch pool, you select either the cloud service configuration or the virtual machine configuration for the operating system on the compute nodes (see [Batch feature overview](batch-api-basics.md#pool)).</span></span> <span data-ttu-id="41221-149">En spécifiant la configuration du service cloud, vos nœuds de calcul sont mis en image avec l’une des [versions de système d’exploitation invité d’Azure](../cloud-services/cloud-services-guestos-update-matrix.md#releases).</span><span class="sxs-lookup"><span data-stu-id="41221-149">If you specify the cloud service configuration, your compute nodes are imaged with one of the [Azure Guest OS releases](../cloud-services/cloud-services-guestos-update-matrix.md#releases).</span></span> <span data-ttu-id="41221-150">En spécifiant la configuration de la machine virtuelle, vous pouvez spécifier l’image d’une des machines virtuelles Linux ou Windows qui figurent dans la [Place de marché de machines virtuelles Azure][vm_marketplace], ou bien fournir une image personnalisée que vous aurez préparée.</span><span class="sxs-lookup"><span data-stu-id="41221-150">If you specify the virtual machine configuration, you can either specify one of the supported Linux or Windows VM images listed in the [Azure Virtual Machines Marketplace][vm_marketplace], or provide a custom image that you have prepared.</span></span>

<span data-ttu-id="41221-151">Si vous exécutez **New-AzureBatchPool**, transmettez les paramètres du système d’exploitation dans un objet PSCloudServiceConfiguration ou PSVirtualMachineConfiguration.</span><span class="sxs-lookup"><span data-stu-id="41221-151">When you run **New-AzureBatchPool**, pass the operating system settings in a PSCloudServiceConfiguration or PSVirtualMachineConfiguration object.</span></span> <span data-ttu-id="41221-152">Par exemple, l’applet de commande suivante crée un pool Batch à l’aide des nœuds de calcul de petite taille dans la configuration de service cloud, avec l’image de la dernière version du système d’exploitation de la famille 3 (Windows Server 2012).</span><span class="sxs-lookup"><span data-stu-id="41221-152">For example, the following cmdlet creates a new Batch pool with size Small compute nodes in the cloud service configuration, imaged with the latest operating system version of family 3 (Windows Server 2012).</span></span> <span data-ttu-id="41221-153">Ici, le paramètre **CloudServiceConfiguration** spécifie la variable *$configuration* comme objet PSCloudServiceConfiguration.</span><span class="sxs-lookup"><span data-stu-id="41221-153">Here, the **CloudServiceConfiguration** parameter specifies the *$configuration* variable as the PSCloudServiceConfiguration object.</span></span> <span data-ttu-id="41221-154">Le paramètre **BatchContext** spécifie une variable *$context* définie au préalable en tant qu’objet BatchAccountContext.</span><span class="sxs-lookup"><span data-stu-id="41221-154">The **BatchContext** parameter specifies a previously defined variable *$context* as the BatchAccountContext object.</span></span>

    $configuration = New-Object -TypeName "Microsoft.Azure.Commands.Batch.Models.PSCloudServiceConfiguration" -ArgumentList @(4,"*")

    New-AzureBatchPool -Id "AutoScalePool" -VirtualMachineSize "Small" -CloudServiceConfiguration $configuration -AutoScaleFormula '$TargetDedicated=4;' -BatchContext $context

<span data-ttu-id="41221-155">Le nombre cible de nœuds de calcul dans le nouveau pool est déterminé par une formule de mise à l’échelle automatique.</span><span class="sxs-lookup"><span data-stu-id="41221-155">The target number of compute nodes in the new pool is determined by an autoscaling formula.</span></span> <span data-ttu-id="41221-156">Dans ce cas, la formule est simplement **$TargetDedicated = 4**, ce qui indique que le nombre de nœuds de calcul dans le pool est de 4 au maximum.</span><span class="sxs-lookup"><span data-stu-id="41221-156">In this case, the formula is simply **$TargetDedicated=4**, indicating the number of compute nodes in the pool is 4 at most.</span></span>

## <a name="query-for-pools-jobs-tasks-and-other-details"></a><span data-ttu-id="41221-157">Requête relative aux pools, aux travaux, aux tâches et autres détails</span><span class="sxs-lookup"><span data-stu-id="41221-157">Query for pools, jobs, tasks, and other details</span></span>
<span data-ttu-id="41221-158">Utilisez les applets de commande telles que **Get-AzureBatchPool**, **Get-AzureBatchJob** et **Get-AzureBatchTask** pour interroger les entités créées sous un compte Batch.</span><span class="sxs-lookup"><span data-stu-id="41221-158">Use cmdlets such as **Get-AzureBatchPool**, **Get-AzureBatchJob**, and **Get-AzureBatchTask** to query for entities created under a Batch account.</span></span>

### <a name="query-for-data"></a><span data-ttu-id="41221-159">Interrogation des données</span><span class="sxs-lookup"><span data-stu-id="41221-159">Query for data</span></span>
<span data-ttu-id="41221-160">Par exemple, utilisez **Get-AzureBatchPools** pour rechercher vos pools.</span><span class="sxs-lookup"><span data-stu-id="41221-160">As an example, use **Get-AzureBatchPools** to find your pools.</span></span> <span data-ttu-id="41221-161">Par défaut, cette demande interroge tous les pools sous votre compte, en supposant que vous avez déjà stocké l’objet BatchAccountContext dans *$context*:</span><span class="sxs-lookup"><span data-stu-id="41221-161">By default this queries for all pools under your account, assuming you already stored the BatchAccountContext object in *$context*:</span></span>

    Get-AzureBatchPool -BatchContext $context

### <a name="use-an-odata-filter"></a><span data-ttu-id="41221-162">Utilisation d’un filtre OData</span><span class="sxs-lookup"><span data-stu-id="41221-162">Use an OData filter</span></span>
<span data-ttu-id="41221-163">Vous pouvez fournir un filtre OData à l'aide du paramètre **Filter** pour rechercher uniquement les objets qui vous intéressent.</span><span class="sxs-lookup"><span data-stu-id="41221-163">You can supply an OData filter using the **Filter** parameter to find only the objects you’re interested in.</span></span> <span data-ttu-id="41221-164">Par exemple, vous pouvez rechercher tous les pools dont l’identificateur commence par « myPool » :</span><span class="sxs-lookup"><span data-stu-id="41221-164">For example, you can find all pools with ids starting with “myPool”:</span></span>

    $filter = "startswith(id,'myPool')"

    Get-AzureBatchPool -Filter $filter -BatchContext $context

<span data-ttu-id="41221-165">Cette méthode n'est pas aussi flexible que l'utilisation de « Where-Object » dans un pipeline local.</span><span class="sxs-lookup"><span data-stu-id="41221-165">This method is not as flexible as using “Where-Object” in a local pipeline.</span></span> <span data-ttu-id="41221-166">Toutefois, la requête est envoyée au service Batch directement pour que tout le filtrage se produise côté serveur et économise ainsi la bande passante Internet.</span><span class="sxs-lookup"><span data-stu-id="41221-166">However, the query gets sent to the Batch service directly so that all filtering happens on the server side, saving Internet bandwidth.</span></span>

### <a name="use-the-id-parameter"></a><span data-ttu-id="41221-167">Utilisation du paramètre Id</span><span class="sxs-lookup"><span data-stu-id="41221-167">Use the Id parameter</span></span>
<span data-ttu-id="41221-168">Une alternative au filtre OData consiste à utiliser le paramètre **Id** .</span><span class="sxs-lookup"><span data-stu-id="41221-168">An alternative to an OData filter is to use the **Id** parameter.</span></span> <span data-ttu-id="41221-169">Pour rechercher un pool spécifique présentant l’identificateur « myPool » :</span><span class="sxs-lookup"><span data-stu-id="41221-169">To query for a specific pool with id "myPool":</span></span>

    Get-AzureBatchPool -Id "myPool" -BatchContext $context

<span data-ttu-id="41221-170">Le paramètre **Id** prend uniquement en charge la recherche de l’identificateur complet, et non les caractères génériques ni les filtres de style OData.</span><span class="sxs-lookup"><span data-stu-id="41221-170">The **Id** parameter supports only full-id search, not wildcards or OData-style filters.</span></span>

### <a name="use-the-maxcount-parameter"></a><span data-ttu-id="41221-171">Utilisation du paramètre MaxCount</span><span class="sxs-lookup"><span data-stu-id="41221-171">Use the MaxCount parameter</span></span>
<span data-ttu-id="41221-172">Par défaut, chaque applet de commande retourne un maximum de 1 000 objets.</span><span class="sxs-lookup"><span data-stu-id="41221-172">By default, each cmdlet returns a maximum of 1000 objects.</span></span> <span data-ttu-id="41221-173">Si vous atteignez cette limite, affinez votre filtration pour limiter le nombre d’objets retournés, ou définissez explicitement une utilisation maximale à l’aide du paramètre **MaxCount** .</span><span class="sxs-lookup"><span data-stu-id="41221-173">If you reach this limit, either refine your filter to bring back fewer objects, or explicitly set a maximum using the **MaxCount** parameter.</span></span> <span data-ttu-id="41221-174">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="41221-174">For example:</span></span>

    Get-AzureBatchTask -MaxCount 2500 -BatchContext $context

<span data-ttu-id="41221-175">Pour supprimer la limite supérieure, définissez **MaxCount** sur 0 ou une valeur inférieure.</span><span class="sxs-lookup"><span data-stu-id="41221-175">To remove the upper bound, set **MaxCount** to 0 or less.</span></span>

### <a name="use-the-powershell-pipeline"></a><span data-ttu-id="41221-176">Utilisation du pipeline PowerShell</span><span class="sxs-lookup"><span data-stu-id="41221-176">Use the PowerShell pipeline</span></span>
<span data-ttu-id="41221-177">Les applets de commande Batch peuvent exploiter le pipeline PowerShell pour envoyer des données entre les applets de commande.</span><span class="sxs-lookup"><span data-stu-id="41221-177">Batch cmdlets can leverage the PowerShell pipeline to send data between cmdlets.</span></span> <span data-ttu-id="41221-178">Cela a le même effet que la spécification d’un paramètre, mais permet d’utiliser plus facilement plusieurs entités.</span><span class="sxs-lookup"><span data-stu-id="41221-178">This has the same effect as specifying a parameter, but makes working with multiple entities easier.</span></span>

<span data-ttu-id="41221-179">Par exemple, recherchez et affichez toutes les tâches sous votre compte :</span><span class="sxs-lookup"><span data-stu-id="41221-179">For example, find and display all tasks under your account:</span></span>

    Get-AzureBatchJob -BatchContext $context | Get-AzureBatchTask -BatchContext $context

<span data-ttu-id="41221-180">Redémarrez chaque nœud de calcul dans un pool :</span><span class="sxs-lookup"><span data-stu-id="41221-180">Restart (reboot) every compute node in a pool:</span></span>

    Get-AzureBatchComputeNode -PoolId "myPool" -BatchContext $context | Restart-AzureBatchComputeNode -BatchContext $context

## <a name="application-package-management"></a><span data-ttu-id="41221-181">Gestion des packages d’application</span><span class="sxs-lookup"><span data-stu-id="41221-181">Application package management</span></span>
<span data-ttu-id="41221-182">Les packages d’application permettent de déployer facilement des applications vers les nœuds de calcul dans vos pools.</span><span class="sxs-lookup"><span data-stu-id="41221-182">Application packages provide a simplified way to deploy applications to the compute nodes in your pools.</span></span> <span data-ttu-id="41221-183">Grâce aux applets de commande PowerShell pour Batch, vous pouvez télécharger et gérer des packages d’application dans votre compte Batch, et déployer des versions de package sur des nœuds de calcul.</span><span class="sxs-lookup"><span data-stu-id="41221-183">With the Batch PowerShell cmdlets, you can upload and manage application packages in your Batch account, and deploy package versions to compute nodes.</span></span>

<span data-ttu-id="41221-184">**Créez** une application :</span><span class="sxs-lookup"><span data-stu-id="41221-184">**Create** an application:</span></span>

    New-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

<span data-ttu-id="41221-185">**Ajoutez** un package d’application :</span><span class="sxs-lookup"><span data-stu-id="41221-185">**Add** an application package:</span></span>

    New-AzureRmBatchApplicationPackage -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -ApplicationVersion "1.0" -Format zip -FilePath package001.zip

<span data-ttu-id="41221-186">Définissez la **version par défaut** pour l’application :</span><span class="sxs-lookup"><span data-stu-id="41221-186">Set the **default version** for the application:</span></span>

    Set-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -DefaultVersion "1.0"

<span data-ttu-id="41221-187">**Répertorier** les packages d’une application</span><span class="sxs-lookup"><span data-stu-id="41221-187">**List** an application's packages</span></span>

    $application = Get-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

    $application.ApplicationPackages

<span data-ttu-id="41221-188">**Supprimer** un package d’application</span><span class="sxs-lookup"><span data-stu-id="41221-188">**Delete** an application package</span></span>

    Remove-AzureRmBatchApplicationPackage -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -ApplicationVersion "1.0"

<span data-ttu-id="41221-189">**Supprimer** une application</span><span class="sxs-lookup"><span data-stu-id="41221-189">**Delete** an application</span></span>

    Remove-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

> [!NOTE]
> <span data-ttu-id="41221-190">Vous devez supprimer toutes les versions de packages d’application d’une application avant de supprimer l’application.</span><span class="sxs-lookup"><span data-stu-id="41221-190">You must delete all of an application's application package versions before you delete the application.</span></span> <span data-ttu-id="41221-191">Vous recevrez une erreur « Conflit » si vous essayez de supprimer une application qui possède des packages d’applications.</span><span class="sxs-lookup"><span data-stu-id="41221-191">You will receive a 'Conflict' error if you try to delete an application that currently has application packages.</span></span>
> 
> 

### <a name="deploy-an-application-package"></a><span data-ttu-id="41221-192">Déployer un package d’application</span><span class="sxs-lookup"><span data-stu-id="41221-192">Deploy an application package</span></span>
<span data-ttu-id="41221-193">Vous pouvez spécifier un ou plusieurs packages d’application pour le déploiement lorsque vous créez un pool.</span><span class="sxs-lookup"><span data-stu-id="41221-193">You can specify one or more application packages for deployment when you create a pool.</span></span> <span data-ttu-id="41221-194">Lorsque vous spécifiez un package lors de la création du pool, il est déployé sur chaque nœud lorsque le nœud rejoint le pool.</span><span class="sxs-lookup"><span data-stu-id="41221-194">When you specify a package at pool creation time, it is deployed to each node as the node joins pool.</span></span> <span data-ttu-id="41221-195">Les packages sont également déployés lorsqu’un nœud est redémarré ou réinitialisé.</span><span class="sxs-lookup"><span data-stu-id="41221-195">Packages are also deployed when a node is rebooted or reimaged.</span></span>

<span data-ttu-id="41221-196">Spécifiez l’option `-ApplicationPackageReference` lors de la création d’un pool pour déployer un package d’application sur les nœuds du pool dès qu’ils rejoignent le pool.</span><span class="sxs-lookup"><span data-stu-id="41221-196">Specify the `-ApplicationPackageReference` option when creating a pool to deploy an application package to the pool's nodes as they join the pool.</span></span> <span data-ttu-id="41221-197">Commencez par créer un objet **PSApplicationPackageReference**, puis configurez-le avec l’ID d’application et la version du package que vous souhaitez déployer sur les nœuds de calcul du pool :</span><span class="sxs-lookup"><span data-stu-id="41221-197">First, create a **PSApplicationPackageReference** object, and configure it with the application Id and package version you want to deploy to the pool's compute nodes:</span></span>

    $appPackageReference = New-Object Microsoft.Azure.Commands.Batch.Models.PSApplicationPackageReference

    $appPackageReference.ApplicationId = "MyBatchApplication"

    $appPackageReference.Version = "1.0"

<span data-ttu-id="41221-198">Créez maintenant le pool et spécifiez l’objet de référence du package comme argument dans l’option `ApplicationPackageReferences` :</span><span class="sxs-lookup"><span data-stu-id="41221-198">Now create the pool, and specify the package reference object as the argument to the `ApplicationPackageReferences` option:</span></span>

    New-AzureBatchPool -Id "PoolWithAppPackage" -VirtualMachineSize "Small" -CloudServiceConfiguration $configuration -BatchContext $context -ApplicationPackageReferences $appPackageReference

<span data-ttu-id="41221-199">Pour plus d’informations sur les packages d’applications, consultez [Déployer des applications sur les nœuds avec des packages d’applications Batch](batch-application-packages.md).</span><span class="sxs-lookup"><span data-stu-id="41221-199">You can find more information on application packages in [Deploy applications to compute nodes with Batch application packages](batch-application-packages.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="41221-200">Pour utiliser les packages d’application, vous devez commencer par [lier un compte de stockage Azure](#linked-storage-account-autostorage) à votre compte Batch.</span><span class="sxs-lookup"><span data-stu-id="41221-200">You must [link an Azure Storage account](#linked-storage-account-autostorage) to your Batch account to use application packages.</span></span>
> 
> 

### <a name="update-a-pools-application-packages"></a><span data-ttu-id="41221-201">Mise à jour des packages d’applications d’un pool</span><span class="sxs-lookup"><span data-stu-id="41221-201">Update a pool's application packages</span></span>
<span data-ttu-id="41221-202">Pour mettre à jour les applications associées à un pool existant, commencez par créer un objet PSApplicationPackageReference avec les propriétés souhaitées (ID d’application et version de package) :</span><span class="sxs-lookup"><span data-stu-id="41221-202">To update the applications assigned to an existing pool, first create a PSApplicationPackageReference object with the desired properties (application Id and package version):</span></span>

    $appPackageReference = New-Object Microsoft.Azure.Commands.Batch.Models.PSApplicationPackageReference

    $appPackageReference.ApplicationId = "MyBatchApplication"

    $appPackageReference.Version = "2.0"

<span data-ttu-id="41221-203">Obtenez ensuite le pool dans Batch, effacez tous les packages existants, ajoutez notre nouvelle référence de package, puis mettez à jour le service Batch avec les nouveaux paramètres de pool :</span><span class="sxs-lookup"><span data-stu-id="41221-203">Next, get the pool from Batch, clear out any existing packages, add our new package reference, and update the Batch service with the new pool settings:</span></span>

    $pool = Get-AzureBatchPool -BatchContext $context -Id "PoolWithAppPackage"

    $pool.ApplicationPackageReferences.Clear()

    $pool.ApplicationPackageReferences.Add($appPackageReference)

    Set-AzureBatchPool -BatchContext $context -Pool $pool

<span data-ttu-id="41221-204">Vous avez mis à jour les propriétés du pool dans le service Batch.</span><span class="sxs-lookup"><span data-stu-id="41221-204">You've now updated the pool's properties in the Batch service.</span></span> <span data-ttu-id="41221-205">Pour déployer réellement le nouveau package d’application sur des nœuds de calcul dans le pool, vous devez redémarrer ou réinitialiser ces nœuds.</span><span class="sxs-lookup"><span data-stu-id="41221-205">To actually deploy the new application package to compute nodes in the pool, however, you must restart or reimage those nodes.</span></span> <span data-ttu-id="41221-206">Vous pouvez redémarrer tous les nœuds dans un pool avec la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="41221-206">You can restart every node in a pool with this command:</span></span>

    Get-AzureBatchComputeNode -PoolId "PoolWithAppPackage" -BatchContext $context | Restart-AzureBatchComputeNode -BatchContext $context

> [!TIP]
> <span data-ttu-id="41221-207">Vous pouvez déployer plusieurs packages d’application sur les nœuds de calcul dans un pool.</span><span class="sxs-lookup"><span data-stu-id="41221-207">You can deploy multiple application packages to the compute nodes in a pool.</span></span> <span data-ttu-id="41221-208">Si vous souhaitez *ajouter* un package d’application au lieu de remplacer les packages actuellement déployés, omettez la ligne `$pool.ApplicationPackageReferences.Clear()` ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="41221-208">If you'd like to *add* an application package instead of replacing the currently deployed packages, omit the `$pool.ApplicationPackageReferences.Clear()` line above.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="41221-209">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="41221-209">Next steps</span></span>
* <span data-ttu-id="41221-210">Pour connaître la syntaxe détaillée des applets de commande et obtenir des exemples, consultez les [informations de référence sur les applets de commande Azure Batch](/powershell/module/azurerm.batch/#batch).</span><span class="sxs-lookup"><span data-stu-id="41221-210">For detailed cmdlet syntax and examples, see [Azure Batch cmdlet reference](/powershell/module/azurerm.batch/#batch).</span></span>
* <span data-ttu-id="41221-211">Pour plus d’informations sur les applications et les packages d’applications dans Batch, consultez [Déploiement d’applications avec des packages d’applications Azure Batch](batch-application-packages.md).</span><span class="sxs-lookup"><span data-stu-id="41221-211">For more information about applications and application packages in Batch, see [Deploy applications to compute nodes with Batch application packages](batch-application-packages.md).</span></span>

[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/