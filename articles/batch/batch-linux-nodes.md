---
title: "Exécuter Linux sur des nœuds de calcul de machine virtuelle - Azure Batch | Microsoft Docs"
description: "Découvrez comment traiter vos charges de travail de calcul parallèles sur des pools de machines virtuelles Linux dans Azure Batch."
services: batch
documentationcenter: python
author: tamram
manager: timlt
editor: 
ms.assetid: dc6ba151-1718-468a-b455-2da549225ab2
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: na
ms.date: 05/22/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 9b2257917e2368478beb75957677de23d4157865
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="provision-linux-compute-nodes-in-batch-pools"></a><span data-ttu-id="9b36e-103">Configurer des nœuds de calcul Linux dans des pools Batch</span><span class="sxs-lookup"><span data-stu-id="9b36e-103">Provision Linux compute nodes in Batch pools</span></span>

<span data-ttu-id="9b36e-104">Vous pouvez utiliser Azure Batch pour exécuter des charges de travail de calcul parallèles sur les machines virtuelles Linux et Windows.</span><span class="sxs-lookup"><span data-stu-id="9b36e-104">You can use Azure Batch to run parallel compute workloads on both Linux and Windows virtual machines.</span></span> <span data-ttu-id="9b36e-105">Cet article explique comment créer des pools de nœuds de calcul Linux dans le service Batch à l’aide de bibliothèques clientes [Batch Python][py_batch_package] et [Batch .NET][api_net].</span><span class="sxs-lookup"><span data-stu-id="9b36e-105">This article details how to create pools of Linux compute nodes in the Batch service by using both the [Batch Python][py_batch_package] and [Batch .NET][api_net] client libraries.</span></span>

> [!NOTE]
> <span data-ttu-id="9b36e-106">Les packages d’applications sont pris en charge sur tous les pools Batch créés après le 5 juillet 2017.</span><span class="sxs-lookup"><span data-stu-id="9b36e-106">Application packages are supported on all Batch pools created after 5 July 2017.</span></span> <span data-ttu-id="9b36e-107">Ils sont pris en charge sur les pools Batch créés entre le 10 mars 2016 et le 5 juillet 2017 uniquement si le pool a été créé à l’aide d’une configuration de service cloud.</span><span class="sxs-lookup"><span data-stu-id="9b36e-107">They are supported on Batch pools created between 10 March 2016 and 5 July 2017 only if the pool was created using a Cloud Service configuration.</span></span> <span data-ttu-id="9b36e-108">Les pools Batch créés avant le 10 mars 2016 ne prennent pas en charge les packages d’applications.</span><span class="sxs-lookup"><span data-stu-id="9b36e-108">Batch pools created prior to 10 March 2016 do not support application packages.</span></span> <span data-ttu-id="9b36e-109">Pour plus d’informations sur l’utilisation de packages d’applications pour déployer vos applications sur vos nœuds Batch, consultez [Déployer des applications sur les nœuds avec des packages d’applications Batch](batch-application-packages.md).</span><span class="sxs-lookup"><span data-stu-id="9b36e-109">For more information about using application packages to deploy your applications to your Batch nodes, see [Deploy applications to compute nodes with Batch application packages](batch-application-packages.md).</span></span>
>
>

## <a name="virtual-machine-configuration"></a><span data-ttu-id="9b36e-110">Configuration de la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="9b36e-110">Virtual machine configuration</span></span>
<span data-ttu-id="9b36e-111">Lorsque vous créez un pool de nœuds de calcul dans Azure Batch, vous avez deux options pour sélectionner la taille du nœud et le système d’exploitation : configuration des services cloud et configuration de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="9b36e-111">When you create a pool of compute nodes in Batch, you have two options from which to select the node size and operating system: Cloud Services Configuration and Virtual Machine Configuration.</span></span>

<span data-ttu-id="9b36e-112">**Configuration de Cloud Services** fournit *uniquement*.</span><span class="sxs-lookup"><span data-stu-id="9b36e-112">**Cloud Services Configuration** provides Windows compute nodes *only*.</span></span> <span data-ttu-id="9b36e-113">Les tailles de nœud de calcul disponibles sont répertoriées dans [Tailles de services cloud](../cloud-services/cloud-services-sizes-specs.md), et les systèmes d’exploitation disponibles sont répertoriés dans [Versions du SE invité et matrice de compatibilité du Kit de développement logiciel (SDK) Azure](../cloud-services/cloud-services-guestos-update-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="9b36e-113">Available compute node sizes are listed in [Sizes for Cloud Services](../cloud-services/cloud-services-sizes-specs.md), and available operating systems are listed in the [Azure Guest OS releases and SDK compatibility matrix](../cloud-services/cloud-services-guestos-update-matrix.md).</span></span> <span data-ttu-id="9b36e-114">Lorsque vous créez un pool contenant des nœuds Services cloud Azure, vous spécifiez la taille du nœud et la famille de systèmes d’exploitation, décrites dans les articles mentionnés ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="9b36e-114">When you create a pool that contains Azure Cloud Services nodes, you specify the node size and the OS family, which are described in the previously mentioned articles.</span></span> <span data-ttu-id="9b36e-115">Pour les pools de nœuds de calcul Windows, les services Cloud Services sont le plus couramment utilisés.</span><span class="sxs-lookup"><span data-stu-id="9b36e-115">For pools of Windows compute nodes, Cloud Services is most commonly used.</span></span>

<span data-ttu-id="9b36e-116">**Virtual Machine Configuration** fournit des images Linux et Windows pour les nœuds de calcul.</span><span class="sxs-lookup"><span data-stu-id="9b36e-116">**Virtual Machine Configuration** provides both Linux and Windows images for compute nodes.</span></span> <span data-ttu-id="9b36e-117">Les tailles de nœud de calcul disponibles sont répertoriées dans [Tailles des machines virtuelles dans Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux) et [Tailles des machines virtuelles dans Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows).</span><span class="sxs-lookup"><span data-stu-id="9b36e-117">Available compute node sizes are listed in [Sizes for virtual machines in Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux) and [Sizes for virtual machines in Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows).</span></span> <span data-ttu-id="9b36e-118">Lorsque vous créez un pool contenant des nœuds de la Configuration de la machine virtuelle, vous devez spécifier la taille des nœuds ainsi que la référence de l’image de la machine virtuelle et la référence de l’agent de nœud du Batch à installer sur les nœuds.</span><span class="sxs-lookup"><span data-stu-id="9b36e-118">When you create a pool that contains Virtual Machine Configuration nodes, you must specify the size of the nodes, the virtual machine image reference, and the Batch node agent SKU to be installed on the nodes.</span></span>

### <a name="virtual-machine-image-reference"></a><span data-ttu-id="9b36e-119">Référence de l’image de la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="9b36e-119">Virtual machine image reference</span></span>
<span data-ttu-id="9b36e-120">Le service Batch utilise des [groupes de machines virtuelles identiques](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) pour fournir des nœuds de calcul Linux.</span><span class="sxs-lookup"><span data-stu-id="9b36e-120">The Batch service uses [virtual machine scale sets](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) to provide Linux compute nodes.</span></span> <span data-ttu-id="9b36e-121">Vous pouvez spécifier une image à partir de la [Place de marché Azure][vm_marketplace], ou fournir une image personnalisée que vous avez préparée.</span><span class="sxs-lookup"><span data-stu-id="9b36e-121">You can specify an image from the [Azure Marketplace][vm_marketplace], or provide a custom image that you have prepared.</span></span> <span data-ttu-id="9b36e-122">Pour en savoir plus sur les images personnalisées, consultez [Develop large-scale parallel compute solutions with Batch](batch-api-basics.md#pool) (Développer des solutions de calcul parallèles à grande échelle avec Batch).</span><span class="sxs-lookup"><span data-stu-id="9b36e-122">For more details about custom images, see [Develop large-scale parallel compute solutions with Batch](batch-api-basics.md#pool).</span></span>

<span data-ttu-id="9b36e-123">Lorsque vous configurez une référence d’image de machine virtuelle, vous spécifiez les propriétés d’une image de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="9b36e-123">When you configure a virtual machine image reference, you specify the properties of the virtual machine image.</span></span> <span data-ttu-id="9b36e-124">Vous avez besoin des propriétés suivantes lorsque vous créez une référence d’image de machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="9b36e-124">The following properties are required when you create a virtual machine image reference:</span></span>

| <span data-ttu-id="9b36e-125">**Propriétés de référence d’image**</span><span class="sxs-lookup"><span data-stu-id="9b36e-125">**Image reference properties**</span></span> | <span data-ttu-id="9b36e-126">**Exemple**</span><span class="sxs-lookup"><span data-stu-id="9b36e-126">**Example**</span></span> |
| --- | --- |
| <span data-ttu-id="9b36e-127">Publisher</span><span class="sxs-lookup"><span data-stu-id="9b36e-127">Publisher</span></span> |<span data-ttu-id="9b36e-128">Canonical</span><span class="sxs-lookup"><span data-stu-id="9b36e-128">Canonical</span></span> |
| <span data-ttu-id="9b36e-129">Offer</span><span class="sxs-lookup"><span data-stu-id="9b36e-129">Offer</span></span> |<span data-ttu-id="9b36e-130">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="9b36e-130">UbuntuServer</span></span> |
| <span data-ttu-id="9b36e-131">SKU</span><span class="sxs-lookup"><span data-stu-id="9b36e-131">SKU</span></span> |<span data-ttu-id="9b36e-132">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="9b36e-132">14.04.4-LTS</span></span> |
| <span data-ttu-id="9b36e-133">Version</span><span class="sxs-lookup"><span data-stu-id="9b36e-133">Version</span></span> |<span data-ttu-id="9b36e-134">le plus récent</span><span class="sxs-lookup"><span data-stu-id="9b36e-134">latest</span></span> |

> [!TIP]
> <span data-ttu-id="9b36e-135">Vous trouverez plus d’informations sur ces propriétés et sur la manière de répertorier des images Marketplace dans [Parcourir et sélectionner des images de machines virtuelles Linux dans Azure avec l’interface CLI ou PowerShell](../virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9b36e-135">You can learn more about these properties and how to list Marketplace images in [Navigate and select Linux virtual machine images in Azure with CLI or PowerShell](../virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="9b36e-136">Notez que toutes les images Marketplace ne sont pas compatibles avec Batch pour le moment.</span><span class="sxs-lookup"><span data-stu-id="9b36e-136">Note that not all Marketplace images are currently compatible with Batch.</span></span> <span data-ttu-id="9b36e-137">Pour plus d’informations, consultez la rubrique [Référence de l’agent de nœud](#node-agent-sku)ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="9b36e-137">For more information, see [Node agent SKU](#node-agent-sku).</span></span>
>
>

### <a name="node-agent-sku"></a><span data-ttu-id="9b36e-138">Référence de l’agent de nœud</span><span class="sxs-lookup"><span data-stu-id="9b36e-138">Node agent SKU</span></span>
<span data-ttu-id="9b36e-139">L’agent de nœud de Batch est un programme qui s’exécute sur chaque nœud dans le pool et fournit l’interface de commande et de contrôle entre le nœud et le service Batch.</span><span class="sxs-lookup"><span data-stu-id="9b36e-139">The Batch node agent is a program that runs on each node in the pool and provides the command-and-control interface between the node and the Batch service.</span></span> <span data-ttu-id="9b36e-140">Il existe différentes implémentations de l’agent de nœud pour différents systèmes d’exploitation, connues sous le nom de références.</span><span class="sxs-lookup"><span data-stu-id="9b36e-140">There are different implementations of the node agent, known as SKUs, for different operating systems.</span></span> <span data-ttu-id="9b36e-141">Essentiellement, lorsque vous créez une configuration de machine virtuelle, vous spécifiez d’abord la référence de l’image de la machine virtuelle, puis spécifiez l’agent de nœud à installer sur l’image.</span><span class="sxs-lookup"><span data-stu-id="9b36e-141">Essentially, when you create a Virtual Machine Configuration, you first specify the virtual machine image reference, and then you specify the node agent to install on the image.</span></span> <span data-ttu-id="9b36e-142">En règle générale, chaque référence d’agent de nœud est compatible avec plusieurs images de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="9b36e-142">Typically, each node agent SKU is compatible with multiple virtual machine images.</span></span> <span data-ttu-id="9b36e-143">Voici quelques exemples de références d’agent de nœud :</span><span class="sxs-lookup"><span data-stu-id="9b36e-143">Here are a few examples of node agent SKUs:</span></span>

* <span data-ttu-id="9b36e-144">batch.node.ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="9b36e-144">batch.node.ubuntu 14.04</span></span>
* <span data-ttu-id="9b36e-145">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="9b36e-145">batch.node.centos 7</span></span>
* <span data-ttu-id="9b36e-146">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="9b36e-146">batch.node.windows amd64</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9b36e-147">Toutes les images de machine virtuelle disponibles sur Marketplace ne sont pas compatibles avec les agents de nœud Batch actuellement disponibles.</span><span class="sxs-lookup"><span data-stu-id="9b36e-147">Not all virtual machine images that are available in the Marketplace are compatible with the currently available Batch node agents.</span></span> <span data-ttu-id="9b36e-148">Utilisez les SDK Batch pour répertorier les références d’agent de nœud disponibles ainsi que les images de machine virtuelle avec lesquelles ils sont compatibles.</span><span class="sxs-lookup"><span data-stu-id="9b36e-148">Use the Batch SDKs to list the available node agent SKUs and the virtual machine images with which they are compatible.</span></span> <span data-ttu-id="9b36e-149">Pour plus d’informations et des exemples montrant comment récupérer une liste d’images valides lors de l’exécution, consultez la [liste des images de machine virtuelle](#list-of-virtual-machine-images).</span><span class="sxs-lookup"><span data-stu-id="9b36e-149">See the [List of Virtual Machine images](#list-of-virtual-machine-images) later in this article for more information and examples of how to retrieve a list of valid images at runtime.</span></span>
>
>

## <a name="create-a-linux-pool-batch-python"></a><span data-ttu-id="9b36e-150">Créer un pool Linux : Batch Python</span><span class="sxs-lookup"><span data-stu-id="9b36e-150">Create a Linux pool: Batch Python</span></span>
<span data-ttu-id="9b36e-151">L’extrait de code suivant illustre un exemple d’utilisation de la [bibliothèque cliente Microsoft Azure Batch pour Python][py_batch_package] pour créer un pool de nœuds de calcul de serveur Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="9b36e-151">The following code snippet shows an example of how to use the [Microsoft Azure Batch Client Library for Python][py_batch_package] to create a pool of Ubuntu Server compute nodes.</span></span> <span data-ttu-id="9b36e-152">Vous trouverez la documentation de référence pour le module Batch Python à la page [azure.batch package][py_batch_docs] (package azure.batch) dans Lire la documentation.</span><span class="sxs-lookup"><span data-stu-id="9b36e-152">Reference documentation for the Batch Python module can be found at [azure.batch package][py_batch_docs] on Read the Docs.</span></span>

<span data-ttu-id="9b36e-153">Cet extrait de code crée explicitement un paramètre [ImageReference][py_imagereference] et spécifie chacune de ses propriétés (éditeur, offre, référence, version).</span><span class="sxs-lookup"><span data-stu-id="9b36e-153">This snippet creates an [ImageReference][py_imagereference] explicitly and specifies each of its properties (publisher, offer, SKU, version).</span></span> <span data-ttu-id="9b36e-154">Dans un code de production, nous vous recommandons toutefois d’utiliser la méthode [list_node_agent_skus][py_list_skus] pour déterminer et sélectionner les combinaisons disponibles de références d’image et de nœuds d’agent lors de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="9b36e-154">In production code, however, we recommend that you use the [list_node_agent_skus][py_list_skus] method to determine and select from the available image and node agent SKU combinations at runtime.</span></span>

```python
# Import the required modules from the
# Azure Batch Client Library for Python
import azure.batch.batch_service_client as batch
import azure.batch.batch_auth as batchauth
import azure.batch.models as batchmodels

# Specify Batch account credentials
account = "<batch-account-name>"
key = "<batch-account-key>"
batch_url = "<batch-account-url>"

# Pool settings
pool_id = "LinuxNodesSamplePoolPython"
vm_size = "STANDARD_A1"
node_count = 1

# Initialize the Batch client
creds = batchauth.SharedKeyCredentials(account, key)
config = batch.BatchServiceClientConfiguration(creds, base_url = batch_url)
client = batch.BatchServiceClient(config)

# Create the unbound pool
new_pool = batchmodels.PoolAddParameter(id = pool_id, vm_size = vm_size)
new_pool.target_dedicated = node_count

# Configure the start task for the pool
start_task = batchmodels.StartTask()
start_task.run_elevated = True
start_task.command_line = "printenv AZ_BATCH_NODE_STARTUP_DIR"
new_pool.start_task = start_task

# Create an ImageReference which specifies the Marketplace
# virtual machine image to install on the nodes.
ir = batchmodels.ImageReference(
    publisher = "Canonical",
    offer = "UbuntuServer",
    sku = "14.04.2-LTS",
    version = "latest")

# Create the VirtualMachineConfiguration, specifying
# the VM image reference and the Batch node agent to
# be installed on the node.
vmc = batchmodels.VirtualMachineConfiguration(
    image_reference = ir,
    node_agent_sku_id = "batch.node.ubuntu 14.04")

# Assign the virtual machine configuration to the pool
new_pool.virtual_machine_configuration = vmc

# Create pool in the Batch service
client.pool.add(new_pool)
```

<span data-ttu-id="9b36e-155">Comme nous l’avons indiqué, il est recommandé d’utiliser la méthode [list_node_agent_skus][py_imagereference] (au lieu de créer explicitement le paramètre [ImageReference][py_list_skus]) afin de sélectionner de manière dynamique une combinaison d’image Marketplace/agent de nœud actuellement prise en charge.</span><span class="sxs-lookup"><span data-stu-id="9b36e-155">As mentioned previously, we recommend that instead of creating the [ImageReference][py_imagereference] explicitly, you use the [list_node_agent_skus][py_list_skus] method to dynamically select from the currently supported node agent/Marketplace image combinations.</span></span> <span data-ttu-id="9b36e-156">L’extrait de code Python suivant illustre l’utilisation de cette méthode.</span><span class="sxs-lookup"><span data-stu-id="9b36e-156">The following Python snippet shows how to use this method.</span></span>

```python
# Get the list of node agents from the Batch service
nodeagents = client.account.list_node_agent_skus()

# Obtain the desired node agent
ubuntu1404agent = next(agent for agent in nodeagents if "ubuntu 14.04" in agent.id)

# Pick the first image reference from the list of verified references
ir = ubuntu1404agent.verified_image_references[0]

# Create the VirtualMachineConfiguration, specifying the VM image
# reference and the Batch node agent to be installed on the node.
vmc = batchmodels.VirtualMachineConfiguration(
    image_reference = ir,
    node_agent_sku_id = ubuntu1404agent.id)
```

## <a name="create-a-linux-pool-batch-net"></a><span data-ttu-id="9b36e-157">Créer un pool Linux : Batch .NET</span><span class="sxs-lookup"><span data-stu-id="9b36e-157">Create a Linux pool: Batch .NET</span></span>
<span data-ttu-id="9b36e-158">L’extrait de code suivant illustre un exemple d’utilisation de la bibliothèque cliente [Batch .NET][nuget_batch_net] pour créer un pool de nœuds de calcul de serveur Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="9b36e-158">The following code snippet shows an example of how to use the [Batch .NET][nuget_batch_net] client library to create a pool of Ubuntu Server compute nodes.</span></span> <span data-ttu-id="9b36e-159">Vous pouvez trouver la [documentation de référence sur les Batch .NET][api_net] sur MSDN.</span><span class="sxs-lookup"><span data-stu-id="9b36e-159">You can find the [Batch .NET reference documentation][api_net] on MSDN.</span></span>

<span data-ttu-id="9b36e-160">L’extrait de code suivant utilise la méthode [PoolOperations][net_pool_ops].[ListNodeAgentSkus][net_list_skus] pour sélectionner des combinaisons d’images Marketplace et de références d’agent de nœud actuellement pris en charge dans la liste.</span><span class="sxs-lookup"><span data-stu-id="9b36e-160">The following code snippet uses the [PoolOperations][net_pool_ops].[ListNodeAgentSkus][net_list_skus] method to select from the list of currently supported Marketplace image and node agent SKU combinations.</span></span> <span data-ttu-id="9b36e-161">Cette technique est souhaitable car la liste des combinaisons prises en charge peut changer de temps à autre.</span><span class="sxs-lookup"><span data-stu-id="9b36e-161">This technique is desirable because the list of supported combinations may change from time to time.</span></span> <span data-ttu-id="9b36e-162">En règle générale, les combinaisons prises en charge sont ajoutées.</span><span class="sxs-lookup"><span data-stu-id="9b36e-162">Most commonly, supported combinations are added.</span></span>

```csharp
// Pool settings
const string poolId = "LinuxNodesSamplePoolDotNet";
const string vmSize = "STANDARD_A1";
const int nodeCount = 1;

// Obtain a collection of all available node agent SKUs.
// This allows us to select from a list of supported
// VM image/node agent combinations.
List<NodeAgentSku> nodeAgentSkus =
    batchClient.PoolOperations.ListNodeAgentSkus().ToList();

// Define a delegate specifying properties of the VM image
// that we wish to use.
Func<ImageReference, bool> isUbuntu1404 = imageRef =>
    imageRef.Publisher == "Canonical" &&
    imageRef.Offer == "UbuntuServer" &&
    imageRef.Sku.Contains("14.04");

// Obtain the first node agent SKU in the collection that matches
// Ubuntu Server 14.04. Note that there are one or more image
// references associated with this node agent SKU.
NodeAgentSku ubuntuAgentSku = nodeAgentSkus.First(sku =>
    sku.VerifiedImageReferences.Any(isUbuntu1404));

// Select an ImageReference from those available for node agent.
ImageReference imageReference =
    ubuntuAgentSku.VerifiedImageReferences.First(isUbuntu1404);

// Create the VirtualMachineConfiguration for use when actually
// creating the pool
VirtualMachineConfiguration virtualMachineConfiguration =
    new VirtualMachineConfiguration(imageReference, ubuntuAgentSku.Id);

// Create the unbound pool object using the VirtualMachineConfiguration
// created above
CloudPool pool = batchClient.PoolOperations.CreatePool(
    poolId: poolId,
    virtualMachineSize: vmSize,
    virtualMachineConfiguration: virtualMachineConfiguration,
    targetDedicatedComputeNodes: nodeCount);

// Commit the pool to the Batch service
await pool.CommitAsync();
```

<span data-ttu-id="9b36e-163">Bien que l’extrait de code ci-dessus utilise la méthode [PoolOperations][net_pool_ops].[ListNodeAgentSkus][net_list_skus] pour répertorier et sélectionner des combinaisons d’images et de références d’agent de nœud prises en charge de manière dynamique (recommandé), vous pouvez également configurer explicitement un paramètre [ImageReference][net_imagereference] :</span><span class="sxs-lookup"><span data-stu-id="9b36e-163">Although the previous snippet uses the [PoolOperations][net_pool_ops].[ListNodeAgentSkus][net_list_skus] method to dynamically list and select from supported image and node agent SKU combinations (recommended), you can also configure an [ImageReference][net_imagereference] explicitly:</span></span>

```csharp
ImageReference imageReference = new ImageReference(
    publisher: "Canonical",
    offer: "UbuntuServer",
    sku: "14.04.2-LTS",
    version: "latest");
```

## <a name="list-of-virtual-machine-images"></a><span data-ttu-id="9b36e-164">liste des images de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="9b36e-164">List of virtual machine images</span></span>
<span data-ttu-id="9b36e-165">Le tableau suivant répertorie les images de machine virtuelle Marketplace compatibles avec les agents de nœud Batch au moment où cet article a été mis à jour.</span><span class="sxs-lookup"><span data-stu-id="9b36e-165">The following table lists the Marketplace virtual machine images that are compatible with the available Batch node agents when this article was last updated.</span></span> <span data-ttu-id="9b36e-166">Il est important de noter que cette liste n’est pas définitive, car des images et des agents de nœud peuvent être ajoutés ou supprimés à tout moment.</span><span class="sxs-lookup"><span data-stu-id="9b36e-166">It is important to note that this list is not definitive because images and node agents may be added or removed at any time.</span></span> <span data-ttu-id="9b36e-167">Nous recommandons l’utilisation de [list_node_agent_skus][py_list_skus] (Python) et [ListNodeAgentSkus][net_list_skus] (Batch .NET) par vos services et applications Batch pour déterminer et sélectionner parmi les références actuellement disponibles.</span><span class="sxs-lookup"><span data-stu-id="9b36e-167">We recommend that your Batch applications and services always use [list_node_agent_skus][py_list_skus] (Python) and [ListNodeAgentSkus][net_list_skus] (Batch .NET) to determine and select from the currently available SKUs.</span></span>

> [!WARNING]
> <span data-ttu-id="9b36e-168">La liste suivante peut changer à tout moment.</span><span class="sxs-lookup"><span data-stu-id="9b36e-168">The following list may change at any time.</span></span> <span data-ttu-id="9b36e-169">Utilisez toujours les méthodes de **création d’une liste de références d’agents de nœud** disponibles dans les API Batch pour répertorier les références (SKU) de machine virtuelle et d’agent de nœud compatibles lorsque vous exécutez vos travaux Batch.</span><span class="sxs-lookup"><span data-stu-id="9b36e-169">Always use the **list node agent SKU** methods available in the Batch APIs to list the compatible virtual machine and node agent SKUs when you run your Batch jobs.</span></span>
>
>

| <span data-ttu-id="9b36e-170">**Publisher**</span><span class="sxs-lookup"><span data-stu-id="9b36e-170">**Publisher**</span></span> | <span data-ttu-id="9b36e-171">**Offer**</span><span class="sxs-lookup"><span data-stu-id="9b36e-171">**Offer**</span></span> | <span data-ttu-id="9b36e-172">**Référence d’image**</span><span class="sxs-lookup"><span data-stu-id="9b36e-172">**Image SKU**</span></span> | <span data-ttu-id="9b36e-173">**Version**</span><span class="sxs-lookup"><span data-stu-id="9b36e-173">**Version**</span></span> | <span data-ttu-id="9b36e-174">**ID de référence de l’agent de nœud**</span><span class="sxs-lookup"><span data-stu-id="9b36e-174">**Node agent SKU ID**</span></span> |
| ------------- | --------- | ------------- | ----------- | --------------------- |
| <span data-ttu-id="9b36e-175">Canonical</span><span class="sxs-lookup"><span data-stu-id="9b36e-175">Canonical</span></span> | <span data-ttu-id="9b36e-176">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="9b36e-176">UbuntuServer</span></span> | <span data-ttu-id="9b36e-177">14.04.5-LTS</span><span class="sxs-lookup"><span data-stu-id="9b36e-177">14.04.5-LTS</span></span> | <span data-ttu-id="9b36e-178">le plus récent</span><span class="sxs-lookup"><span data-stu-id="9b36e-178">latest</span></span> | <span data-ttu-id="9b36e-179">batch.node.ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="9b36e-179">batch.node.ubuntu 14.04</span></span> |
| <span data-ttu-id="9b36e-180">Canonical</span><span class="sxs-lookup"><span data-stu-id="9b36e-180">Canonical</span></span> | <span data-ttu-id="9b36e-181">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="9b36e-181">UbuntuServer</span></span> | <span data-ttu-id="9b36e-182">16.04.0-LTS</span><span class="sxs-lookup"><span data-stu-id="9b36e-182">16.04.0-LTS</span></span> | <span data-ttu-id="9b36e-183">le plus récent</span><span class="sxs-lookup"><span data-stu-id="9b36e-183">latest</span></span> | <span data-ttu-id="9b36e-184">batch.node.ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="9b36e-184">batch.node.ubuntu 16.04</span></span> |
| <span data-ttu-id="9b36e-185">Credativ</span><span class="sxs-lookup"><span data-stu-id="9b36e-185">Credativ</span></span> | <span data-ttu-id="9b36e-186">Debian</span><span class="sxs-lookup"><span data-stu-id="9b36e-186">Debian</span></span> | <span data-ttu-id="9b36e-187">8</span><span class="sxs-lookup"><span data-stu-id="9b36e-187">8</span></span> | <span data-ttu-id="9b36e-188">le plus récent</span><span class="sxs-lookup"><span data-stu-id="9b36e-188">latest</span></span> | <span data-ttu-id="9b36e-189">batch.node.debian 8</span><span class="sxs-lookup"><span data-stu-id="9b36e-189">batch.node.debian 8</span></span> |
| <span data-ttu-id="9b36e-190">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="9b36e-190">OpenLogic</span></span> | <span data-ttu-id="9b36e-191">CentOS</span><span class="sxs-lookup"><span data-stu-id="9b36e-191">CentOS</span></span> | <span data-ttu-id="9b36e-192">7.0</span><span class="sxs-lookup"><span data-stu-id="9b36e-192">7.0</span></span> | <span data-ttu-id="9b36e-193">le plus récent</span><span class="sxs-lookup"><span data-stu-id="9b36e-193">latest</span></span> | <span data-ttu-id="9b36e-194">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="9b36e-194">batch.node.centos 7</span></span> |
| <span data-ttu-id="9b36e-195">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="9b36e-195">OpenLogic</span></span> | <span data-ttu-id="9b36e-196">CentOS</span><span class="sxs-lookup"><span data-stu-id="9b36e-196">CentOS</span></span> | <span data-ttu-id="9b36e-197">7.1</span><span class="sxs-lookup"><span data-stu-id="9b36e-197">7.1</span></span> | <span data-ttu-id="9b36e-198">le plus récent</span><span class="sxs-lookup"><span data-stu-id="9b36e-198">latest</span></span> | <span data-ttu-id="9b36e-199">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="9b36e-199">batch.node.centos 7</span></span> |
| <span data-ttu-id="9b36e-200">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="9b36e-200">OpenLogic</span></span> | <span data-ttu-id="9b36e-201">CentOS-HPC</span><span class="sxs-lookup"><span data-stu-id="9b36e-201">CentOS-HPC</span></span> | <span data-ttu-id="9b36e-202">7.1</span><span class="sxs-lookup"><span data-stu-id="9b36e-202">7.1</span></span> | <span data-ttu-id="9b36e-203">le plus récent</span><span class="sxs-lookup"><span data-stu-id="9b36e-203">latest</span></span> | <span data-ttu-id="9b36e-204">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="9b36e-204">batch.node.centos 7</span></span> |
| <span data-ttu-id="9b36e-205">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="9b36e-205">OpenLogic</span></span> | <span data-ttu-id="9b36e-206">CentOS</span><span class="sxs-lookup"><span data-stu-id="9b36e-206">CentOS</span></span> | <span data-ttu-id="9b36e-207">7,2</span><span class="sxs-lookup"><span data-stu-id="9b36e-207">7.2</span></span> | <span data-ttu-id="9b36e-208">le plus récent</span><span class="sxs-lookup"><span data-stu-id="9b36e-208">latest</span></span> | <span data-ttu-id="9b36e-209">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="9b36e-209">batch.node.centos 7</span></span> |
| <span data-ttu-id="9b36e-210">Oracle</span><span class="sxs-lookup"><span data-stu-id="9b36e-210">Oracle</span></span> | <span data-ttu-id="9b36e-211">Oracle-Linux</span><span class="sxs-lookup"><span data-stu-id="9b36e-211">Oracle-Linux</span></span> | <span data-ttu-id="9b36e-212">7.0</span><span class="sxs-lookup"><span data-stu-id="9b36e-212">7.0</span></span> | <span data-ttu-id="9b36e-213">le plus récent</span><span class="sxs-lookup"><span data-stu-id="9b36e-213">latest</span></span> | <span data-ttu-id="9b36e-214">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="9b36e-214">batch.node.centos 7</span></span> |
| <span data-ttu-id="9b36e-215">Oracle</span><span class="sxs-lookup"><span data-stu-id="9b36e-215">Oracle</span></span> | <span data-ttu-id="9b36e-216">Oracle-Linux</span><span class="sxs-lookup"><span data-stu-id="9b36e-216">Oracle-Linux</span></span> | <span data-ttu-id="9b36e-217">7,2</span><span class="sxs-lookup"><span data-stu-id="9b36e-217">7.2</span></span> | <span data-ttu-id="9b36e-218">le plus récent</span><span class="sxs-lookup"><span data-stu-id="9b36e-218">latest</span></span> | <span data-ttu-id="9b36e-219">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="9b36e-219">batch.node.centos 7</span></span> |
| <span data-ttu-id="9b36e-220">SUSE</span><span class="sxs-lookup"><span data-stu-id="9b36e-220">SUSE</span></span> | <span data-ttu-id="9b36e-221">openSUSE</span><span class="sxs-lookup"><span data-stu-id="9b36e-221">openSUSE</span></span> | <span data-ttu-id="9b36e-222">13.2</span><span class="sxs-lookup"><span data-stu-id="9b36e-222">13.2</span></span> | <span data-ttu-id="9b36e-223">le plus récent</span><span class="sxs-lookup"><span data-stu-id="9b36e-223">latest</span></span> | <span data-ttu-id="9b36e-224">batch.node.opensuse 13.2</span><span class="sxs-lookup"><span data-stu-id="9b36e-224">batch.node.opensuse 13.2</span></span> |
| <span data-ttu-id="9b36e-225">SUSE</span><span class="sxs-lookup"><span data-stu-id="9b36e-225">SUSE</span></span> | <span data-ttu-id="9b36e-226">openSUSE-Leap</span><span class="sxs-lookup"><span data-stu-id="9b36e-226">openSUSE-Leap</span></span> | <span data-ttu-id="9b36e-227">42.1</span><span class="sxs-lookup"><span data-stu-id="9b36e-227">42.1</span></span> | <span data-ttu-id="9b36e-228">le plus récent</span><span class="sxs-lookup"><span data-stu-id="9b36e-228">latest</span></span> | <span data-ttu-id="9b36e-229">batch.node.opensuse 42.1</span><span class="sxs-lookup"><span data-stu-id="9b36e-229">batch.node.opensuse 42.1</span></span> |
| <span data-ttu-id="9b36e-230">SUSE</span><span class="sxs-lookup"><span data-stu-id="9b36e-230">SUSE</span></span> | <span data-ttu-id="9b36e-231">SLES</span><span class="sxs-lookup"><span data-stu-id="9b36e-231">SLES</span></span> | <span data-ttu-id="9b36e-232">12-SP1</span><span class="sxs-lookup"><span data-stu-id="9b36e-232">12-SP1</span></span> | <span data-ttu-id="9b36e-233">le plus récent</span><span class="sxs-lookup"><span data-stu-id="9b36e-233">latest</span></span> | <span data-ttu-id="9b36e-234">batch.node.opensuse 42.1</span><span class="sxs-lookup"><span data-stu-id="9b36e-234">batch.node.opensuse 42.1</span></span> |
| <span data-ttu-id="9b36e-235">SUSE</span><span class="sxs-lookup"><span data-stu-id="9b36e-235">SUSE</span></span> | <span data-ttu-id="9b36e-236">SLES-HPC</span><span class="sxs-lookup"><span data-stu-id="9b36e-236">SLES-HPC</span></span> | <span data-ttu-id="9b36e-237">12-SP1</span><span class="sxs-lookup"><span data-stu-id="9b36e-237">12-SP1</span></span> | <span data-ttu-id="9b36e-238">le plus récent</span><span class="sxs-lookup"><span data-stu-id="9b36e-238">latest</span></span> | <span data-ttu-id="9b36e-239">batch.node.opensuse 42.1</span><span class="sxs-lookup"><span data-stu-id="9b36e-239">batch.node.opensuse 42.1</span></span> |
| <span data-ttu-id="9b36e-240">microsoft-ads</span><span class="sxs-lookup"><span data-stu-id="9b36e-240">microsoft-ads</span></span> | <span data-ttu-id="9b36e-241">linux-data-science-vm</span><span class="sxs-lookup"><span data-stu-id="9b36e-241">linux-data-science-vm</span></span> | <span data-ttu-id="9b36e-242">linuxdsvm</span><span class="sxs-lookup"><span data-stu-id="9b36e-242">linuxdsvm</span></span> | <span data-ttu-id="9b36e-243">le plus récent</span><span class="sxs-lookup"><span data-stu-id="9b36e-243">latest</span></span> | <span data-ttu-id="9b36e-244">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="9b36e-244">batch.node.centos 7</span></span> |
| <span data-ttu-id="9b36e-245">microsoft-ads</span><span class="sxs-lookup"><span data-stu-id="9b36e-245">microsoft-ads</span></span> | <span data-ttu-id="9b36e-246">standard-data-science-vm</span><span class="sxs-lookup"><span data-stu-id="9b36e-246">standard-data-science-vm</span></span> | <span data-ttu-id="9b36e-247">standard-data-science-vm</span><span class="sxs-lookup"><span data-stu-id="9b36e-247">standard-data-science-vm</span></span> | <span data-ttu-id="9b36e-248">le plus récent</span><span class="sxs-lookup"><span data-stu-id="9b36e-248">latest</span></span> | <span data-ttu-id="9b36e-249">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="9b36e-249">batch.node.windows amd64</span></span> |
| <span data-ttu-id="9b36e-250">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="9b36e-250">MicrosoftWindowsServer</span></span> | <span data-ttu-id="9b36e-251">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="9b36e-251">WindowsServer</span></span> | <span data-ttu-id="9b36e-252">2008-R2-SP1</span><span class="sxs-lookup"><span data-stu-id="9b36e-252">2008-R2-SP1</span></span> | <span data-ttu-id="9b36e-253">le plus récent</span><span class="sxs-lookup"><span data-stu-id="9b36e-253">latest</span></span> | <span data-ttu-id="9b36e-254">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="9b36e-254">batch.node.windows amd64</span></span> |
| <span data-ttu-id="9b36e-255">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="9b36e-255">MicrosoftWindowsServer</span></span> | <span data-ttu-id="9b36e-256">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="9b36e-256">WindowsServer</span></span> | <span data-ttu-id="9b36e-257">2012-Datacenter</span><span class="sxs-lookup"><span data-stu-id="9b36e-257">2012-Datacenter</span></span> | <span data-ttu-id="9b36e-258">le plus récent</span><span class="sxs-lookup"><span data-stu-id="9b36e-258">latest</span></span> | <span data-ttu-id="9b36e-259">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="9b36e-259">batch.node.windows amd64</span></span> |
| <span data-ttu-id="9b36e-260">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="9b36e-260">MicrosoftWindowsServer</span></span> | <span data-ttu-id="9b36e-261">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="9b36e-261">WindowsServer</span></span> | <span data-ttu-id="9b36e-262">2012-R2-Datacenter</span><span class="sxs-lookup"><span data-stu-id="9b36e-262">2012-R2-Datacenter</span></span> | <span data-ttu-id="9b36e-263">le plus récent</span><span class="sxs-lookup"><span data-stu-id="9b36e-263">latest</span></span> | <span data-ttu-id="9b36e-264">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="9b36e-264">batch.node.windows amd64</span></span> |
| <span data-ttu-id="9b36e-265">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="9b36e-265">MicrosoftWindowsServer</span></span> | <span data-ttu-id="9b36e-266">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="9b36e-266">WindowsServer</span></span> | <span data-ttu-id="9b36e-267">2016-centre-de-données</span><span class="sxs-lookup"><span data-stu-id="9b36e-267">2016-Datacenter</span></span> | <span data-ttu-id="9b36e-268">le plus récent</span><span class="sxs-lookup"><span data-stu-id="9b36e-268">latest</span></span> | <span data-ttu-id="9b36e-269">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="9b36e-269">batch.node.windows amd64</span></span> |
| <span data-ttu-id="9b36e-270">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="9b36e-270">MicrosoftWindowsServer</span></span> | <span data-ttu-id="9b36e-271">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="9b36e-271">WindowsServer</span></span> | <span data-ttu-id="9b36e-272">2016-centre-de-données-avec-conteneurs</span><span class="sxs-lookup"><span data-stu-id="9b36e-272">2016-Datacenter-with-Containers</span></span> | <span data-ttu-id="9b36e-273">le plus récent</span><span class="sxs-lookup"><span data-stu-id="9b36e-273">latest</span></span> | <span data-ttu-id="9b36e-274">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="9b36e-274">batch.node.windows amd64</span></span> |

## <a name="connect-to-linux-nodes-using-ssh"></a><span data-ttu-id="9b36e-275">Se connecter à des nœuds Linux via SSH</span><span class="sxs-lookup"><span data-stu-id="9b36e-275">Connect to Linux nodes using SSH</span></span>
<span data-ttu-id="9b36e-276">Pendant le développement ou lors de la résolution des problèmes, il peut s’avérer nécessaire de se connecter aux nœuds de votre pool.</span><span class="sxs-lookup"><span data-stu-id="9b36e-276">During development or while troubleshooting, you may find it necessary to sign in to the nodes in your pool.</span></span> <span data-ttu-id="9b36e-277">Contrairement aux nœuds de calcul Windows, vous ne pouvez pas utiliser le protocole RDP (Remote Desktop Protocol) pour se connecter à des nœuds Linux.</span><span class="sxs-lookup"><span data-stu-id="9b36e-277">Unlike Windows compute nodes, you cannot use Remote Desktop Protocol (RDP) to connect to Linux nodes.</span></span> <span data-ttu-id="9b36e-278">Au lieu de cela, le service Batch autorise l’accès SSH sur chaque nœud de connexion à distance.</span><span class="sxs-lookup"><span data-stu-id="9b36e-278">Instead, the Batch service enables SSH access on each node for remote connection.</span></span>

<span data-ttu-id="9b36e-279">L’extrait de code Python suivant crée un utilisateur sur chaque nœud d’un pool, nécessaire à la connexion à distance.</span><span class="sxs-lookup"><span data-stu-id="9b36e-279">The following Python code snippet creates a user on each node in a pool, which is required for remote connection.</span></span> <span data-ttu-id="9b36e-280">Il imprime ensuite les informations de connexion SSH pour chaque nœud.</span><span class="sxs-lookup"><span data-stu-id="9b36e-280">It then prints the secure shell (SSH) connection information for each node.</span></span>

```python
import datetime
import getpass
import azure.batch.batch_service_client as batch
import azure.batch.batch_auth as batchauth
import azure.batch.models as batchmodels

# Specify your own account credentials
batch_account_name = ''
batch_account_key = ''
batch_account_url = ''

# Specify the ID of an existing pool containing Linux nodes
# currently in the 'idle' state
pool_id = ''

# Specify the username and prompt for a password
username = 'linuxuser'
password = getpass.getpass()

# Create a BatchClient
credentials = batchauth.SharedKeyCredentials(
    batch_account_name,
    batch_account_key
)
batch_client = batch.BatchServiceClient(
        credentials,
        base_url=batch_account_url
)

# Create the user that will be added to each node in the pool
user = batchmodels.ComputeNodeUser(username)
user.password = password
user.is_admin = True
user.expiry_time = \
    (datetime.datetime.today() + datetime.timedelta(days=30)).isoformat()

# Get the list of nodes in the pool
nodes = batch_client.compute_node.list(pool_id)

# Add the user to each node in the pool and print
# the connection information for the node
for node in nodes:
    # Add the user to the node
    batch_client.compute_node.add_user(pool_id, node.id, user)

    # Obtain SSH login information for the node
    login = batch_client.compute_node.get_remote_login_settings(pool_id,
                                                                node.id)

    # Print the connection info for the node
    print("{0} | {1} | {2} | {3}".format(node.id,
                                         node.state,
                                         login.remote_login_ip_address,
                                         login.remote_login_port))
```

<span data-ttu-id="9b36e-281">Voici un exemple de sortie du code ci-dessus pour un pool contenant quatre nœuds Linux :</span><span class="sxs-lookup"><span data-stu-id="9b36e-281">Here is sample output for the previous code for a pool that contains four Linux nodes:</span></span>

```
Password:
tvm-1219235766_1-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50000
tvm-1219235766_2-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50003
tvm-1219235766_3-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50002
tvm-1219235766_4-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50001
```

<span data-ttu-id="9b36e-282">Au lieu d’un mot de passe, vous pouvez spécifier une clé publique SSH lorsque vous créez un utilisateur sur un nœud.</span><span class="sxs-lookup"><span data-stu-id="9b36e-282">Instead of a password, you can specify an SSH public key when you create a user on a node.</span></span> <span data-ttu-id="9b36e-283">Dans le SDK Python, utilisez le paramètre **ssh_public_key** sur [ComputeNodeUser][py_computenodeuser].</span><span class="sxs-lookup"><span data-stu-id="9b36e-283">In the Python SDK, use the **ssh_public_key** parameter on [ComputeNodeUser][py_computenodeuser].</span></span> <span data-ttu-id="9b36e-284">Dans .NET, utilisez la propriété [ComputeNodeUser][net_computenodeuser].[SshPublicKey][net_ssh_key].</span><span class="sxs-lookup"><span data-stu-id="9b36e-284">In .NET, use the [ComputeNodeUser][net_computenodeuser].[SshPublicKey][net_ssh_key] property.</span></span>

## <a name="pricing"></a><span data-ttu-id="9b36e-285">Tarification</span><span class="sxs-lookup"><span data-stu-id="9b36e-285">Pricing</span></span>
<span data-ttu-id="9b36e-286">Azure Batch est basé sur la technologie d’Azure Cloud Services et des machines virtuelles Azure.</span><span class="sxs-lookup"><span data-stu-id="9b36e-286">Azure Batch is built on Azure Cloud Services and Azure Virtual Machines technology.</span></span> <span data-ttu-id="9b36e-287">Le service Batch lui-même est proposé gratuitement, ce qui signifie que vous payez uniquement les ressources de calcul utilisées par vos solutions Batch.</span><span class="sxs-lookup"><span data-stu-id="9b36e-287">The Batch service itself is offered at no cost, which means you are charged only for the compute resources that your Batch solutions consume.</span></span> <span data-ttu-id="9b36e-288">Si vous sélectionnez **Configuration des services cloud**, vous êtes facturé en fonction de la structure de [tarification des services cloud][cloud_services_pricing].</span><span class="sxs-lookup"><span data-stu-id="9b36e-288">When you choose **Cloud Services Configuration**, you are charged based on the [Cloud Services pricing][cloud_services_pricing] structure.</span></span> <span data-ttu-id="9b36e-289">Si vous sélectionnez la **Configuration de la machine virtuelle**, vous êtes facturé en fonction de la structure de [tarification des machines virtuelles][vm_pricing].</span><span class="sxs-lookup"><span data-stu-id="9b36e-289">When you choose **Virtual Machine Configuration**, you are charged based on the [Virtual Machines pricing][vm_pricing] structure.</span></span> 

<span data-ttu-id="9b36e-290">Si vous déployez des applications sur vos nœuds Batch à l’aide de [packages d’application](batch-application-packages.md), vous êtes également facturé pour les ressources Stockage Azure que vos packages d’application consomment.</span><span class="sxs-lookup"><span data-stu-id="9b36e-290">If you deploy applications to your Batch nodes using [application packages](batch-application-packages.md), you are also charged for the Azure Storage resources that your application packages consume.</span></span> <span data-ttu-id="9b36e-291">En général, les coûts Stockage Azure sont minimes.</span><span class="sxs-lookup"><span data-stu-id="9b36e-291">In general, the Azure Storage costs are minimal.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="9b36e-292">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9b36e-292">Next steps</span></span>
### <a name="batch-python-tutorial"></a><span data-ttu-id="9b36e-293">Didacticiel Python Batch</span><span class="sxs-lookup"><span data-stu-id="9b36e-293">Batch Python tutorial</span></span>
<span data-ttu-id="9b36e-294">Pour accéder à un didacticiel plus détaillé sur l’utilisation de Batch avec Python, consultez la page [Prise en main du client Python Azure Batch](batch-python-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="9b36e-294">For a more in-depth tutorial about how to work with Batch by using Python, check out [Get started with the Azure Batch Python client](batch-python-tutorial.md).</span></span> <span data-ttu-id="9b36e-295">Son [exemple de code][github_samples_pyclient] associé comprend une fonction d’assistance, `get_vm_config_for_distro`, qui affiche une autre technique de configuration de machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="9b36e-295">Its companion [code sample][github_samples_pyclient] includes a helper function, `get_vm_config_for_distro`, that shows another technique to obtain a virtual machine configuration.</span></span>

### <a name="batch-python-code-samples"></a><span data-ttu-id="9b36e-296">Exemples de code Batch Python</span><span class="sxs-lookup"><span data-stu-id="9b36e-296">Batch Python code samples</span></span>
<span data-ttu-id="9b36e-297">Les [exemples de code Python][github_samples_py] du dépôt [azure-batch-samples][github_samples] sur GitHub comprennent des scripts illustrant l’exécution d’opérations Batch communes telles que la création de pools, de travaux et de tâches.</span><span class="sxs-lookup"><span data-stu-id="9b36e-297">The [Python code samples][github_samples_py] in the [azure-batch-samples][github_samples] repository on GitHub contain scripts that show you how to perform common Batch operations, such as pool, job, and task creation.</span></span> <span data-ttu-id="9b36e-298">Le fichier [Lisez-moi][github_py_readme] qui accompagne les exemples de code Python contient des informations sur l’installation des packages nécessaires.</span><span class="sxs-lookup"><span data-stu-id="9b36e-298">The [README][github_py_readme] that accompanies the Python samples has details about how to install the required packages.</span></span>

### <a name="batch-forum"></a><span data-ttu-id="9b36e-299">Forum Azure Batch</span><span class="sxs-lookup"><span data-stu-id="9b36e-299">Batch forum</span></span>
<span data-ttu-id="9b36e-300">Le [Forum Azure Batch][forum] sur MSDN est l’endroit idéal pour discuter de Batch et poser des questions sur le service.</span><span class="sxs-lookup"><span data-stu-id="9b36e-300">The [Azure Batch Forum][forum] on MSDN is a great place to discuss Batch and ask questions about the service.</span></span> <span data-ttu-id="9b36e-301">Consultez le forum pour obtenir des publications « épinglées » utiles, et publiez les questions que vous vous posez pendant la création de vos solutions Batch.</span><span class="sxs-lookup"><span data-stu-id="9b36e-301">Read helpful "pinned" posts, and post your questions as they arise while you build your Batch solutions.</span></span>

[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_net_mgmt]: https://msdn.microsoft.com/library/azure/mt463120.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[cloud_services_pricing]: https://azure.microsoft.com/pricing/details/cloud-services/
[forum]: https://social.msdn.microsoft.com/forums/azure/en-US/home?forum=azurebatch
[github_py_readme]: https://github.com/Azure/azure-batch-samples/blob/master/Python/Batch/README.md
[github_samples]: https://github.com/Azure/azure-batch-samples
[github_samples_py]: https://github.com/Azure/azure-batch-samples/tree/master/Python/Batch
[github_samples_pyclient]: https://github.com/Azure/azure-batch-samples/blob/master/Python/Batch/article_samples/python_tutorial_client.py
[portal]: https://portal.azure.com
[net_cloudpool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_computenodeuser]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenodeuser.aspx
[net_imagereference]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.imagereference.aspx
[net_list_skus]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.listnodeagentskus.aspx
[net_pool_ops]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.aspx
[net_ssh_key]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenodeuser.sshpublickey.aspx
[nuget_batch_net]: https://www.nuget.org/packages/Azure.Batch/
[rest_add_pool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
[py_account_ops]: http://azure-sdk-for-python.readthedocs.org/en/dev/ref/azure.batch.operations.html#azure.batch.operations.AccountOperations
[py_azure_sdk]: https://pypi.python.org/pypi/azure
[py_batch_docs]: http://azure-sdk-for-python.readthedocs.org/en/dev/ref/azure.batch.html
[py_batch_package]: https://pypi.python.org/pypi/azure-batch
[py_computenodeuser]: http://azure-sdk-for-python.readthedocs.org/en/dev/ref/azure.batch.models.html#azure.batch.models.ComputeNodeUser
[py_imagereference]: http://azure-sdk-for-python.readthedocs.org/en/dev/ref/azure.batch.models.html#azure.batch.models.ImageReference
[py_list_skus]: http://azure-sdk-for-python.readthedocs.org/en/dev/ref/azure.batch.operations.html#azure.batch.operations.AccountOperations.list_node_agent_skus
[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/
[vm_pricing]: https://azure.microsoft.com/pricing/details/virtual-machines/
