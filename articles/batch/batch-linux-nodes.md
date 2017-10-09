---
title: "aaaRun Linux sur la machine virtuelle de calcul nœuds - Azure Batch | Documents Microsoft"
description: "Découvrez comment tooprocess votre parallèle de calcul des charges de travail sur des pools d’ordinateurs virtuels Linux dans Azure Batch."
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
ms.openlocfilehash: 3daabd5c577baaafd0544f9f7913cb7b116d74d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="provision-linux-compute-nodes-in-batch-pools"></a><span data-ttu-id="6640b-103">Configurer des nœuds de calcul Linux dans des pools Batch</span><span class="sxs-lookup"><span data-stu-id="6640b-103">Provision Linux compute nodes in Batch pools</span></span>

<span data-ttu-id="6640b-104">Vous pouvez utiliser les charges de travail de traitement par lots Azure toorun calcul parallèle sur les ordinateurs virtuels Linux et Windows.</span><span class="sxs-lookup"><span data-stu-id="6640b-104">You can use Azure Batch toorun parallel compute workloads on both Linux and Windows virtual machines.</span></span> <span data-ttu-id="6640b-105">Cet article décrit en détail comment pools toocreate de Linux nœuds de calcul dans le service de traitement par lots hello à l’aide de deux hello [lot Python] [ py_batch_package] et [Batch .NET] [ api_net] les bibliothèques clientes.</span><span class="sxs-lookup"><span data-stu-id="6640b-105">This article details how toocreate pools of Linux compute nodes in hello Batch service by using both hello [Batch Python][py_batch_package] and [Batch .NET][api_net] client libraries.</span></span>

> [!NOTE]
> <span data-ttu-id="6640b-106">Les packages d’applications sont pris en charge sur tous les pools Batch créés après le 5 juillet 2017.</span><span class="sxs-lookup"><span data-stu-id="6640b-106">Application packages are supported on all Batch pools created after 5 July 2017.</span></span> <span data-ttu-id="6640b-107">Elles sont prises en charge sur les pools de traitement par lots créés entre 10 mars 2016 et 5 juillet 2017 uniquement si le pool de hello a été créé à l’aide d’une configuration de Service Cloud.</span><span class="sxs-lookup"><span data-stu-id="6640b-107">They are supported on Batch pools created between 10 March 2016 and 5 July 2017 only if hello pool was created using a Cloud Service configuration.</span></span> <span data-ttu-id="6640b-108">Les pools de lot créés too10 préalable mars 2016 ne gèrent pas les packages d’applications.</span><span class="sxs-lookup"><span data-stu-id="6640b-108">Batch pools created prior too10 March 2016 do not support application packages.</span></span> <span data-ttu-id="6640b-109">Pour plus d’informations sur l’application à l’aide de packages toodeploy vos nœuds de traitement par lots tooyour applications, consultez [déployer des nœuds de toocompute d’applications avec des packages d’application de lot](batch-application-packages.md).</span><span class="sxs-lookup"><span data-stu-id="6640b-109">For more information about using application packages toodeploy your applications tooyour Batch nodes, see [Deploy applications toocompute nodes with Batch application packages](batch-application-packages.md).</span></span>
>
>

## <a name="virtual-machine-configuration"></a><span data-ttu-id="6640b-110">Configuration de la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="6640b-110">Virtual machine configuration</span></span>
<span data-ttu-id="6640b-111">Lorsque vous créez un pool de nœuds de calcul dans un lot, vous avez deux options quelle taille de nœud tooselect hello et le système d’exploitation : Configuration des Services Cloud et la Configuration d’ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="6640b-111">When you create a pool of compute nodes in Batch, you have two options from which tooselect hello node size and operating system: Cloud Services Configuration and Virtual Machine Configuration.</span></span>

<span data-ttu-id="6640b-112">**configuration des services cloud** fournit *uniquement*des nœuds de calcul Windows.</span><span class="sxs-lookup"><span data-stu-id="6640b-112">**Cloud Services Configuration** provides Windows compute nodes *only*.</span></span> <span data-ttu-id="6640b-113">Tailles de nœud de calcul disponibles sont répertoriés dans [tailles pour les Services de Cloud](../cloud-services/cloud-services-sizes-specs.md), et les systèmes d’exploitation disponibles sont répertoriés dans hello [versions de système d’exploitation invité de Azure et matrice de compatibilité SDK](../cloud-services/cloud-services-guestos-update-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="6640b-113">Available compute node sizes are listed in [Sizes for Cloud Services](../cloud-services/cloud-services-sizes-specs.md), and available operating systems are listed in hello [Azure Guest OS releases and SDK compatibility matrix](../cloud-services/cloud-services-guestos-update-matrix.md).</span></span> <span data-ttu-id="6640b-114">Lorsque vous créez un pool qui contient les nœuds des Services de cloud computing Azure, vous spécifiez la taille du nœud hello et hello famille de systèmes d’exploitation, qui sont décrites dans hello mentionné précédemment articles.</span><span class="sxs-lookup"><span data-stu-id="6640b-114">When you create a pool that contains Azure Cloud Services nodes, you specify hello node size and hello OS family, which are described in hello previously mentioned articles.</span></span> <span data-ttu-id="6640b-115">Pour les pools de nœuds de calcul Windows, les services Cloud Services sont le plus couramment utilisés.</span><span class="sxs-lookup"><span data-stu-id="6640b-115">For pools of Windows compute nodes, Cloud Services is most commonly used.</span></span>

<span data-ttu-id="6640b-116">**Virtual Machine Configuration** fournit des images Linux et Windows pour les nœuds de calcul.</span><span class="sxs-lookup"><span data-stu-id="6640b-116">**Virtual Machine Configuration** provides both Linux and Windows images for compute nodes.</span></span> <span data-ttu-id="6640b-117">Les tailles de nœud de calcul disponibles sont répertoriées dans [Tailles des machines virtuelles dans Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux) et [Tailles des machines virtuelles dans Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows).</span><span class="sxs-lookup"><span data-stu-id="6640b-117">Available compute node sizes are listed in [Sizes for virtual machines in Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux) and [Sizes for virtual machines in Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows).</span></span> <span data-ttu-id="6640b-118">Lorsque vous créez un pool qui contient les nœuds de la Configuration d’ordinateur virtuel, vous devez spécifier la taille hello de nœuds de hello, référence d’image de machine virtuelle de hello et toobe SKU hello lot nœud agent installé sur les nœuds hello.</span><span class="sxs-lookup"><span data-stu-id="6640b-118">When you create a pool that contains Virtual Machine Configuration nodes, you must specify hello size of hello nodes, hello virtual machine image reference, and hello Batch node agent SKU toobe installed on hello nodes.</span></span>

### <a name="virtual-machine-image-reference"></a><span data-ttu-id="6640b-119">Référence de l’image de la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="6640b-119">Virtual machine image reference</span></span>
<span data-ttu-id="6640b-120">Hello par service de traitement par lots [machines virtuelles identiques](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) tooprovide Linux des nœuds de calcul.</span><span class="sxs-lookup"><span data-stu-id="6640b-120">hello Batch service uses [virtual machine scale sets](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) tooprovide Linux compute nodes.</span></span> <span data-ttu-id="6640b-121">Vous pouvez spécifier une image à partir de hello [Azure Marketplace][vm_marketplace], ou fournir une image personnalisée que vous avez préparé.</span><span class="sxs-lookup"><span data-stu-id="6640b-121">You can specify an image from hello [Azure Marketplace][vm_marketplace], or provide a custom image that you have prepared.</span></span> <span data-ttu-id="6640b-122">Pour en savoir plus sur les images personnalisées, consultez [Develop large-scale parallel compute solutions with Batch](batch-api-basics.md#pool) (Développer des solutions de calcul parallèles à grande échelle avec Batch).</span><span class="sxs-lookup"><span data-stu-id="6640b-122">For more details about custom images, see [Develop large-scale parallel compute solutions with Batch](batch-api-basics.md#pool).</span></span>

<span data-ttu-id="6640b-123">Lorsque vous configurez une référence d’image de machine virtuelle, vous spécifiez les propriétés de hello d’image de machine virtuelle hello.</span><span class="sxs-lookup"><span data-stu-id="6640b-123">When you configure a virtual machine image reference, you specify hello properties of hello virtual machine image.</span></span> <span data-ttu-id="6640b-124">Hello propriétés suivantes est requise lorsque vous créez une référence d’image de machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="6640b-124">hello following properties are required when you create a virtual machine image reference:</span></span>

| <span data-ttu-id="6640b-125">**Propriétés de référence d’image**</span><span class="sxs-lookup"><span data-stu-id="6640b-125">**Image reference properties**</span></span> | <span data-ttu-id="6640b-126">**Exemple**</span><span class="sxs-lookup"><span data-stu-id="6640b-126">**Example**</span></span> |
| --- | --- |
| <span data-ttu-id="6640b-127">Publisher</span><span class="sxs-lookup"><span data-stu-id="6640b-127">Publisher</span></span> |<span data-ttu-id="6640b-128">Canonical</span><span class="sxs-lookup"><span data-stu-id="6640b-128">Canonical</span></span> |
| <span data-ttu-id="6640b-129">Offer</span><span class="sxs-lookup"><span data-stu-id="6640b-129">Offer</span></span> |<span data-ttu-id="6640b-130">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="6640b-130">UbuntuServer</span></span> |
| <span data-ttu-id="6640b-131">SKU</span><span class="sxs-lookup"><span data-stu-id="6640b-131">SKU</span></span> |<span data-ttu-id="6640b-132">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="6640b-132">14.04.4-LTS</span></span> |
| <span data-ttu-id="6640b-133">Version</span><span class="sxs-lookup"><span data-stu-id="6640b-133">Version</span></span> |<span data-ttu-id="6640b-134">le plus récent</span><span class="sxs-lookup"><span data-stu-id="6640b-134">latest</span></span> |

> [!TIP]
> <span data-ttu-id="6640b-135">Plus d’informations sur ces propriétés et comment les images toolist Marketplace dans [naviguer et sélectionnez images de machine virtuelle Linux dans Azure avec l’interface CLI ou PowerShell](../virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6640b-135">You can learn more about these properties and how toolist Marketplace images in [Navigate and select Linux virtual machine images in Azure with CLI or PowerShell](../virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="6640b-136">Notez que toutes les images Marketplace ne sont pas compatibles avec Batch pour le moment.</span><span class="sxs-lookup"><span data-stu-id="6640b-136">Note that not all Marketplace images are currently compatible with Batch.</span></span> <span data-ttu-id="6640b-137">Pour plus d’informations, consultez la rubrique [Référence de l’agent de nœud](#node-agent-sku)ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="6640b-137">For more information, see [Node agent SKU](#node-agent-sku).</span></span>
>
>

### <a name="node-agent-sku"></a><span data-ttu-id="6640b-138">Référence de l’agent de nœud</span><span class="sxs-lookup"><span data-stu-id="6640b-138">Node agent SKU</span></span>
<span data-ttu-id="6640b-139">agent de nœud de traitement par lots Hello est un programme qui s’exécute sur chaque nœud dans le pool de hello et fournit l’interface de commande et contrôle hello entre le nœud de hello et service de traitement par lots hello.</span><span class="sxs-lookup"><span data-stu-id="6640b-139">hello Batch node agent is a program that runs on each node in hello pool and provides hello command-and-control interface between hello node and hello Batch service.</span></span> <span data-ttu-id="6640b-140">Il existe différentes implémentations de l’agent de nœud hello, connus en tant que références (SKU), pour les différents systèmes d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="6640b-140">There are different implementations of hello node agent, known as SKUs, for different operating systems.</span></span> <span data-ttu-id="6640b-141">Essentiellement, lorsque vous créez une Configuration de Machine virtuelle, vous spécifiez tout d’abord la référence d’image de machine virtuelle de hello, puis vous spécifiez hello nœud agent tooinstall sur l’image de hello.</span><span class="sxs-lookup"><span data-stu-id="6640b-141">Essentially, when you create a Virtual Machine Configuration, you first specify hello virtual machine image reference, and then you specify hello node agent tooinstall on hello image.</span></span> <span data-ttu-id="6640b-142">En règle générale, chaque référence d’agent de nœud est compatible avec plusieurs images de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="6640b-142">Typically, each node agent SKU is compatible with multiple virtual machine images.</span></span> <span data-ttu-id="6640b-143">Voici quelques exemples de références d’agent de nœud :</span><span class="sxs-lookup"><span data-stu-id="6640b-143">Here are a few examples of node agent SKUs:</span></span>

* <span data-ttu-id="6640b-144">batch.node.ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="6640b-144">batch.node.ubuntu 14.04</span></span>
* <span data-ttu-id="6640b-145">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="6640b-145">batch.node.centos 7</span></span>
* <span data-ttu-id="6640b-146">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="6640b-146">batch.node.windows amd64</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6640b-147">Pas toutes les images de machine virtuelle qui sont disponibles dans hello Marketplace sont compatibles avec les agents de nœud hello actuellement disponibles par lots.</span><span class="sxs-lookup"><span data-stu-id="6640b-147">Not all virtual machine images that are available in hello Marketplace are compatible with hello currently available Batch node agents.</span></span> <span data-ttu-id="6640b-148">Hello kits de développement logiciel lot toolist hello nœud disponible agent SKU et hello des images de machine virtuelle avec lesquels ils sont compatibles.</span><span class="sxs-lookup"><span data-stu-id="6640b-148">Use hello Batch SDKs toolist hello available node agent SKUs and hello virtual machine images with which they are compatible.</span></span> <span data-ttu-id="6640b-149">Consultez hello [images de la liste de la Machine virtuelle](#list-of-virtual-machine-images) plus loin dans cet article pour plus d’informations et obtenir des exemples de tooretrieve une liste d’images valides lors de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="6640b-149">See hello [List of Virtual Machine images](#list-of-virtual-machine-images) later in this article for more information and examples of how tooretrieve a list of valid images at runtime.</span></span>
>
>

## <a name="create-a-linux-pool-batch-python"></a><span data-ttu-id="6640b-150">Créer un pool Linux : Batch Python</span><span class="sxs-lookup"><span data-stu-id="6640b-150">Create a Linux pool: Batch Python</span></span>
<span data-ttu-id="6640b-151">Hello extrait de code suivant illustre un exemple de toouse hello [bibliothèque du Client Microsoft Azure Batch pour Python] [ py_batch_package] toocreate un pool d’Ubuntu Server des nœuds de calcul.</span><span class="sxs-lookup"><span data-stu-id="6640b-151">hello following code snippet shows an example of how toouse hello [Microsoft Azure Batch Client Library for Python][py_batch_package] toocreate a pool of Ubuntu Server compute nodes.</span></span> <span data-ttu-id="6640b-152">Consultez la documentation pour hello trouverez de module de traitement par lots Python [azure.batch package] [ py_batch_docs] des documents de hello en lecture.</span><span class="sxs-lookup"><span data-stu-id="6640b-152">Reference documentation for hello Batch Python module can be found at [azure.batch package][py_batch_docs] on Read hello Docs.</span></span>

<span data-ttu-id="6640b-153">Cet extrait de code crée explicitement un paramètre [ImageReference][py_imagereference] et spécifie chacune de ses propriétés (éditeur, offre, référence, version).</span><span class="sxs-lookup"><span data-stu-id="6640b-153">This snippet creates an [ImageReference][py_imagereference] explicitly and specifies each of its properties (publisher, offer, SKU, version).</span></span> <span data-ttu-id="6640b-154">Dans le code de production, cependant, nous vous recommandons d’utiliser hello [list_node_agent_skus] [ py_list_skus] toodetermine de méthode et de sélectionner parmi hello image et le nœud agent SKU combinaisons disponibles lors de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="6640b-154">In production code, however, we recommend that you use hello [list_node_agent_skus][py_list_skus] method toodetermine and select from hello available image and node agent SKU combinations at runtime.</span></span>

```python
# Import hello required modules from the
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

# Initialize hello Batch client
creds = batchauth.SharedKeyCredentials(account, key)
config = batch.BatchServiceClientConfiguration(creds, base_url = batch_url)
client = batch.BatchServiceClient(config)

# Create hello unbound pool
new_pool = batchmodels.PoolAddParameter(id = pool_id, vm_size = vm_size)
new_pool.target_dedicated = node_count

# Configure hello start task for hello pool
start_task = batchmodels.StartTask()
start_task.run_elevated = True
start_task.command_line = "printenv AZ_BATCH_NODE_STARTUP_DIR"
new_pool.start_task = start_task

# Create an ImageReference which specifies hello Marketplace
# virtual machine image tooinstall on hello nodes.
ir = batchmodels.ImageReference(
    publisher = "Canonical",
    offer = "UbuntuServer",
    sku = "14.04.2-LTS",
    version = "latest")

# Create hello VirtualMachineConfiguration, specifying
# hello VM image reference and hello Batch node agent to
# be installed on hello node.
vmc = batchmodels.VirtualMachineConfiguration(
    image_reference = ir,
    node_agent_sku_id = "batch.node.ubuntu 14.04")

# Assign hello virtual machine configuration toohello pool
new_pool.virtual_machine_configuration = vmc

# Create pool in hello Batch service
client.pool.add(new_pool)
```

<span data-ttu-id="6640b-155">Comme mentionné précédemment, nous vous recommandons au lieu de créer hello [ImageReference] [ py_imagereference] explicitement, vous utilisez hello [list_node_agent_skus] [ py_list_skus] sélectionnez toodynamically de méthode à partir de hello pris en charge actuellement les combinaisons d’image du nœud agent/Marketplace.</span><span class="sxs-lookup"><span data-stu-id="6640b-155">As mentioned previously, we recommend that instead of creating hello [ImageReference][py_imagereference] explicitly, you use hello [list_node_agent_skus][py_list_skus] method toodynamically select from hello currently supported node agent/Marketplace image combinations.</span></span> <span data-ttu-id="6640b-156">Hello suivant indique le code Python comment toouse cette méthode.</span><span class="sxs-lookup"><span data-stu-id="6640b-156">hello following Python snippet shows how toouse this method.</span></span>

```python
# Get hello list of node agents from hello Batch service
nodeagents = client.account.list_node_agent_skus()

# Obtain hello desired node agent
ubuntu1404agent = next(agent for agent in nodeagents if "ubuntu 14.04" in agent.id)

# Pick hello first image reference from hello list of verified references
ir = ubuntu1404agent.verified_image_references[0]

# Create hello VirtualMachineConfiguration, specifying hello VM image
# reference and hello Batch node agent toobe installed on hello node.
vmc = batchmodels.VirtualMachineConfiguration(
    image_reference = ir,
    node_agent_sku_id = ubuntu1404agent.id)
```

## <a name="create-a-linux-pool-batch-net"></a><span data-ttu-id="6640b-157">Créer un pool Linux : Batch .NET</span><span class="sxs-lookup"><span data-stu-id="6640b-157">Create a Linux pool: Batch .NET</span></span>
<span data-ttu-id="6640b-158">Hello extrait de code suivant illustre un exemple de toouse hello [Batch .NET] [ nuget_batch_net] toocreate de bibliothèque client un pool d’Ubuntu Server des nœuds de calcul.</span><span class="sxs-lookup"><span data-stu-id="6640b-158">hello following code snippet shows an example of how toouse hello [Batch .NET][nuget_batch_net] client library toocreate a pool of Ubuntu Server compute nodes.</span></span> <span data-ttu-id="6640b-159">Vous pouvez trouver hello [documentation de référence .NET de lot] [ api_net] sur MSDN.</span><span class="sxs-lookup"><span data-stu-id="6640b-159">You can find hello [Batch .NET reference documentation][api_net] on MSDN.</span></span>

<span data-ttu-id="6640b-160">Hello extrait de code suivant utilise hello [PoolOperations][net_pool_ops].[ ListNodeAgentSkus] [ net_list_skus] tooselect de méthode dans liste hello actuellement combinaisons prises en charge Marketplace image et le nœud agent référence (SKU).</span><span class="sxs-lookup"><span data-stu-id="6640b-160">hello following code snippet uses hello [PoolOperations][net_pool_ops].[ListNodeAgentSkus][net_list_skus] method tooselect from hello list of currently supported Marketplace image and node agent SKU combinations.</span></span> <span data-ttu-id="6640b-161">Cette technique est souhaitable, car la liste hello des combinaisons prises en charge peut-être changer d’heure tootime.</span><span class="sxs-lookup"><span data-stu-id="6640b-161">This technique is desirable because hello list of supported combinations may change from time tootime.</span></span> <span data-ttu-id="6640b-162">En règle générale, les combinaisons prises en charge sont ajoutées.</span><span class="sxs-lookup"><span data-stu-id="6640b-162">Most commonly, supported combinations are added.</span></span>

```csharp
// Pool settings
const string poolId = "LinuxNodesSamplePoolDotNet";
const string vmSize = "STANDARD_A1";
const int nodeCount = 1;

// Obtain a collection of all available node agent SKUs.
// This allows us tooselect from a list of supported
// VM image/node agent combinations.
List<NodeAgentSku> nodeAgentSkus =
    batchClient.PoolOperations.ListNodeAgentSkus().ToList();

// Define a delegate specifying properties of hello VM image
// that we wish toouse.
Func<ImageReference, bool> isUbuntu1404 = imageRef =>
    imageRef.Publisher == "Canonical" &&
    imageRef.Offer == "UbuntuServer" &&
    imageRef.Sku.Contains("14.04");

// Obtain hello first node agent SKU in hello collection that matches
// Ubuntu Server 14.04. Note that there are one or more image
// references associated with this node agent SKU.
NodeAgentSku ubuntuAgentSku = nodeAgentSkus.First(sku =>
    sku.VerifiedImageReferences.Any(isUbuntu1404));

// Select an ImageReference from those available for node agent.
ImageReference imageReference =
    ubuntuAgentSku.VerifiedImageReferences.First(isUbuntu1404);

// Create hello VirtualMachineConfiguration for use when actually
// creating hello pool
VirtualMachineConfiguration virtualMachineConfiguration =
    new VirtualMachineConfiguration(imageReference, ubuntuAgentSku.Id);

// Create hello unbound pool object using hello VirtualMachineConfiguration
// created above
CloudPool pool = batchClient.PoolOperations.CreatePool(
    poolId: poolId,
    virtualMachineSize: vmSize,
    virtualMachineConfiguration: virtualMachineConfiguration,
    targetDedicatedComputeNodes: nodeCount);

// Commit hello pool toohello Batch service
await pool.CommitAsync();
```

<span data-ttu-id="6640b-163">Bien que l’extrait de code précédent hello utilise hello [PoolOperations][net_pool_ops].[ ListNodeAgentSkus] [ net_list_skus] toodynamically (méthode) et sélectionnez prise en charge d’image et le nœud de combinaisons de référence (SKU) de l’agent (recommandés), vous pouvez également configurer un [ImageReference] [ net_imagereference] explicitement :</span><span class="sxs-lookup"><span data-stu-id="6640b-163">Although hello previous snippet uses hello [PoolOperations][net_pool_ops].[ListNodeAgentSkus][net_list_skus] method toodynamically list and select from supported image and node agent SKU combinations (recommended), you can also configure an [ImageReference][net_imagereference] explicitly:</span></span>

```csharp
ImageReference imageReference = new ImageReference(
    publisher: "Canonical",
    offer: "UbuntuServer",
    sku: "14.04.2-LTS",
    version: "latest");
```

## <a name="list-of-virtual-machine-images"></a><span data-ttu-id="6640b-164">liste des images de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="6640b-164">List of virtual machine images</span></span>
<span data-ttu-id="6640b-165">Hello tableau suivant répertorie les images de machine virtuelle hello Marketplace qui sont compatibles avec les agents de nœud de traitement disponibles hello lors de la dernière mise à jour de cet article.</span><span class="sxs-lookup"><span data-stu-id="6640b-165">hello following table lists hello Marketplace virtual machine images that are compatible with hello available Batch node agents when this article was last updated.</span></span> <span data-ttu-id="6640b-166">Il est important toonote que cette liste n’est pas définitive, car les images et les agents de nœud peuvent ajouter ou supprimer à tout moment.</span><span class="sxs-lookup"><span data-stu-id="6640b-166">It is important toonote that this list is not definitive because images and node agents may be added or removed at any time.</span></span> <span data-ttu-id="6640b-167">Nous recommandons de vos applications de traitement par lots et services toujours utilisent [list_node_agent_skus] [ py_list_skus] (Python) et [ListNodeAgentSkus] [ net_list_skus] Les toodetermine (lot .NET) et sélectionner parmi hello références actuellement disponibles.</span><span class="sxs-lookup"><span data-stu-id="6640b-167">We recommend that your Batch applications and services always use [list_node_agent_skus][py_list_skus] (Python) and [ListNodeAgentSkus][net_list_skus] (Batch .NET) toodetermine and select from hello currently available SKUs.</span></span>

> [!WARNING]
> <span data-ttu-id="6640b-168">Hello suivant liste peut changer à tout moment.</span><span class="sxs-lookup"><span data-stu-id="6640b-168">hello following list may change at any time.</span></span> <span data-ttu-id="6640b-169">Utilisez toujours hello **agent du nœud liste référence (SKU)** méthodes disponibles dans toolist d’API de lot hello hello machine virtuelle compatibles et l’agent de nœud Références (SKU) lorsque vous exécutez vos traitements par lots.</span><span class="sxs-lookup"><span data-stu-id="6640b-169">Always use hello **list node agent SKU** methods available in hello Batch APIs toolist hello compatible virtual machine and node agent SKUs when you run your Batch jobs.</span></span>
>
>

| <span data-ttu-id="6640b-170">**Publisher**</span><span class="sxs-lookup"><span data-stu-id="6640b-170">**Publisher**</span></span> | <span data-ttu-id="6640b-171">**Offer**</span><span class="sxs-lookup"><span data-stu-id="6640b-171">**Offer**</span></span> | <span data-ttu-id="6640b-172">**Référence d’image**</span><span class="sxs-lookup"><span data-stu-id="6640b-172">**Image SKU**</span></span> | <span data-ttu-id="6640b-173">**Version**</span><span class="sxs-lookup"><span data-stu-id="6640b-173">**Version**</span></span> | <span data-ttu-id="6640b-174">**ID de référence de l’agent de nœud**</span><span class="sxs-lookup"><span data-stu-id="6640b-174">**Node agent SKU ID**</span></span> |
| ------------- | --------- | ------------- | ----------- | --------------------- |
| <span data-ttu-id="6640b-175">Canonical</span><span class="sxs-lookup"><span data-stu-id="6640b-175">Canonical</span></span> | <span data-ttu-id="6640b-176">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="6640b-176">UbuntuServer</span></span> | <span data-ttu-id="6640b-177">14.04.5-LTS</span><span class="sxs-lookup"><span data-stu-id="6640b-177">14.04.5-LTS</span></span> | <span data-ttu-id="6640b-178">le plus récent</span><span class="sxs-lookup"><span data-stu-id="6640b-178">latest</span></span> | <span data-ttu-id="6640b-179">batch.node.ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="6640b-179">batch.node.ubuntu 14.04</span></span> |
| <span data-ttu-id="6640b-180">Canonical</span><span class="sxs-lookup"><span data-stu-id="6640b-180">Canonical</span></span> | <span data-ttu-id="6640b-181">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="6640b-181">UbuntuServer</span></span> | <span data-ttu-id="6640b-182">16.04.0-LTS</span><span class="sxs-lookup"><span data-stu-id="6640b-182">16.04.0-LTS</span></span> | <span data-ttu-id="6640b-183">le plus récent</span><span class="sxs-lookup"><span data-stu-id="6640b-183">latest</span></span> | <span data-ttu-id="6640b-184">batch.node.ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="6640b-184">batch.node.ubuntu 16.04</span></span> |
| <span data-ttu-id="6640b-185">Credativ</span><span class="sxs-lookup"><span data-stu-id="6640b-185">Credativ</span></span> | <span data-ttu-id="6640b-186">Debian</span><span class="sxs-lookup"><span data-stu-id="6640b-186">Debian</span></span> | <span data-ttu-id="6640b-187">8</span><span class="sxs-lookup"><span data-stu-id="6640b-187">8</span></span> | <span data-ttu-id="6640b-188">le plus récent</span><span class="sxs-lookup"><span data-stu-id="6640b-188">latest</span></span> | <span data-ttu-id="6640b-189">batch.node.debian 8</span><span class="sxs-lookup"><span data-stu-id="6640b-189">batch.node.debian 8</span></span> |
| <span data-ttu-id="6640b-190">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="6640b-190">OpenLogic</span></span> | <span data-ttu-id="6640b-191">CentOS</span><span class="sxs-lookup"><span data-stu-id="6640b-191">CentOS</span></span> | <span data-ttu-id="6640b-192">7.0</span><span class="sxs-lookup"><span data-stu-id="6640b-192">7.0</span></span> | <span data-ttu-id="6640b-193">le plus récent</span><span class="sxs-lookup"><span data-stu-id="6640b-193">latest</span></span> | <span data-ttu-id="6640b-194">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="6640b-194">batch.node.centos 7</span></span> |
| <span data-ttu-id="6640b-195">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="6640b-195">OpenLogic</span></span> | <span data-ttu-id="6640b-196">CentOS</span><span class="sxs-lookup"><span data-stu-id="6640b-196">CentOS</span></span> | <span data-ttu-id="6640b-197">7.1</span><span class="sxs-lookup"><span data-stu-id="6640b-197">7.1</span></span> | <span data-ttu-id="6640b-198">le plus récent</span><span class="sxs-lookup"><span data-stu-id="6640b-198">latest</span></span> | <span data-ttu-id="6640b-199">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="6640b-199">batch.node.centos 7</span></span> |
| <span data-ttu-id="6640b-200">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="6640b-200">OpenLogic</span></span> | <span data-ttu-id="6640b-201">CentOS-HPC</span><span class="sxs-lookup"><span data-stu-id="6640b-201">CentOS-HPC</span></span> | <span data-ttu-id="6640b-202">7.1</span><span class="sxs-lookup"><span data-stu-id="6640b-202">7.1</span></span> | <span data-ttu-id="6640b-203">le plus récent</span><span class="sxs-lookup"><span data-stu-id="6640b-203">latest</span></span> | <span data-ttu-id="6640b-204">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="6640b-204">batch.node.centos 7</span></span> |
| <span data-ttu-id="6640b-205">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="6640b-205">OpenLogic</span></span> | <span data-ttu-id="6640b-206">CentOS</span><span class="sxs-lookup"><span data-stu-id="6640b-206">CentOS</span></span> | <span data-ttu-id="6640b-207">7,2</span><span class="sxs-lookup"><span data-stu-id="6640b-207">7.2</span></span> | <span data-ttu-id="6640b-208">le plus récent</span><span class="sxs-lookup"><span data-stu-id="6640b-208">latest</span></span> | <span data-ttu-id="6640b-209">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="6640b-209">batch.node.centos 7</span></span> |
| <span data-ttu-id="6640b-210">Oracle</span><span class="sxs-lookup"><span data-stu-id="6640b-210">Oracle</span></span> | <span data-ttu-id="6640b-211">Oracle-Linux</span><span class="sxs-lookup"><span data-stu-id="6640b-211">Oracle-Linux</span></span> | <span data-ttu-id="6640b-212">7.0</span><span class="sxs-lookup"><span data-stu-id="6640b-212">7.0</span></span> | <span data-ttu-id="6640b-213">le plus récent</span><span class="sxs-lookup"><span data-stu-id="6640b-213">latest</span></span> | <span data-ttu-id="6640b-214">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="6640b-214">batch.node.centos 7</span></span> |
| <span data-ttu-id="6640b-215">Oracle</span><span class="sxs-lookup"><span data-stu-id="6640b-215">Oracle</span></span> | <span data-ttu-id="6640b-216">Oracle-Linux</span><span class="sxs-lookup"><span data-stu-id="6640b-216">Oracle-Linux</span></span> | <span data-ttu-id="6640b-217">7,2</span><span class="sxs-lookup"><span data-stu-id="6640b-217">7.2</span></span> | <span data-ttu-id="6640b-218">le plus récent</span><span class="sxs-lookup"><span data-stu-id="6640b-218">latest</span></span> | <span data-ttu-id="6640b-219">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="6640b-219">batch.node.centos 7</span></span> |
| <span data-ttu-id="6640b-220">SUSE</span><span class="sxs-lookup"><span data-stu-id="6640b-220">SUSE</span></span> | <span data-ttu-id="6640b-221">openSUSE</span><span class="sxs-lookup"><span data-stu-id="6640b-221">openSUSE</span></span> | <span data-ttu-id="6640b-222">13.2</span><span class="sxs-lookup"><span data-stu-id="6640b-222">13.2</span></span> | <span data-ttu-id="6640b-223">le plus récent</span><span class="sxs-lookup"><span data-stu-id="6640b-223">latest</span></span> | <span data-ttu-id="6640b-224">batch.node.opensuse 13.2</span><span class="sxs-lookup"><span data-stu-id="6640b-224">batch.node.opensuse 13.2</span></span> |
| <span data-ttu-id="6640b-225">SUSE</span><span class="sxs-lookup"><span data-stu-id="6640b-225">SUSE</span></span> | <span data-ttu-id="6640b-226">openSUSE-Leap</span><span class="sxs-lookup"><span data-stu-id="6640b-226">openSUSE-Leap</span></span> | <span data-ttu-id="6640b-227">42.1</span><span class="sxs-lookup"><span data-stu-id="6640b-227">42.1</span></span> | <span data-ttu-id="6640b-228">le plus récent</span><span class="sxs-lookup"><span data-stu-id="6640b-228">latest</span></span> | <span data-ttu-id="6640b-229">batch.node.opensuse 42.1</span><span class="sxs-lookup"><span data-stu-id="6640b-229">batch.node.opensuse 42.1</span></span> |
| <span data-ttu-id="6640b-230">SUSE</span><span class="sxs-lookup"><span data-stu-id="6640b-230">SUSE</span></span> | <span data-ttu-id="6640b-231">SLES</span><span class="sxs-lookup"><span data-stu-id="6640b-231">SLES</span></span> | <span data-ttu-id="6640b-232">12-SP1</span><span class="sxs-lookup"><span data-stu-id="6640b-232">12-SP1</span></span> | <span data-ttu-id="6640b-233">le plus récent</span><span class="sxs-lookup"><span data-stu-id="6640b-233">latest</span></span> | <span data-ttu-id="6640b-234">batch.node.opensuse 42.1</span><span class="sxs-lookup"><span data-stu-id="6640b-234">batch.node.opensuse 42.1</span></span> |
| <span data-ttu-id="6640b-235">SUSE</span><span class="sxs-lookup"><span data-stu-id="6640b-235">SUSE</span></span> | <span data-ttu-id="6640b-236">SLES-HPC</span><span class="sxs-lookup"><span data-stu-id="6640b-236">SLES-HPC</span></span> | <span data-ttu-id="6640b-237">12-SP1</span><span class="sxs-lookup"><span data-stu-id="6640b-237">12-SP1</span></span> | <span data-ttu-id="6640b-238">le plus récent</span><span class="sxs-lookup"><span data-stu-id="6640b-238">latest</span></span> | <span data-ttu-id="6640b-239">batch.node.opensuse 42.1</span><span class="sxs-lookup"><span data-stu-id="6640b-239">batch.node.opensuse 42.1</span></span> |
| <span data-ttu-id="6640b-240">microsoft-ads</span><span class="sxs-lookup"><span data-stu-id="6640b-240">microsoft-ads</span></span> | <span data-ttu-id="6640b-241">linux-data-science-vm</span><span class="sxs-lookup"><span data-stu-id="6640b-241">linux-data-science-vm</span></span> | <span data-ttu-id="6640b-242">linuxdsvm</span><span class="sxs-lookup"><span data-stu-id="6640b-242">linuxdsvm</span></span> | <span data-ttu-id="6640b-243">le plus récent</span><span class="sxs-lookup"><span data-stu-id="6640b-243">latest</span></span> | <span data-ttu-id="6640b-244">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="6640b-244">batch.node.centos 7</span></span> |
| <span data-ttu-id="6640b-245">microsoft-ads</span><span class="sxs-lookup"><span data-stu-id="6640b-245">microsoft-ads</span></span> | <span data-ttu-id="6640b-246">standard-data-science-vm</span><span class="sxs-lookup"><span data-stu-id="6640b-246">standard-data-science-vm</span></span> | <span data-ttu-id="6640b-247">standard-data-science-vm</span><span class="sxs-lookup"><span data-stu-id="6640b-247">standard-data-science-vm</span></span> | <span data-ttu-id="6640b-248">le plus récent</span><span class="sxs-lookup"><span data-stu-id="6640b-248">latest</span></span> | <span data-ttu-id="6640b-249">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="6640b-249">batch.node.windows amd64</span></span> |
| <span data-ttu-id="6640b-250">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="6640b-250">MicrosoftWindowsServer</span></span> | <span data-ttu-id="6640b-251">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="6640b-251">WindowsServer</span></span> | <span data-ttu-id="6640b-252">2008-R2-SP1</span><span class="sxs-lookup"><span data-stu-id="6640b-252">2008-R2-SP1</span></span> | <span data-ttu-id="6640b-253">le plus récent</span><span class="sxs-lookup"><span data-stu-id="6640b-253">latest</span></span> | <span data-ttu-id="6640b-254">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="6640b-254">batch.node.windows amd64</span></span> |
| <span data-ttu-id="6640b-255">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="6640b-255">MicrosoftWindowsServer</span></span> | <span data-ttu-id="6640b-256">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="6640b-256">WindowsServer</span></span> | <span data-ttu-id="6640b-257">2012-Datacenter</span><span class="sxs-lookup"><span data-stu-id="6640b-257">2012-Datacenter</span></span> | <span data-ttu-id="6640b-258">le plus récent</span><span class="sxs-lookup"><span data-stu-id="6640b-258">latest</span></span> | <span data-ttu-id="6640b-259">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="6640b-259">batch.node.windows amd64</span></span> |
| <span data-ttu-id="6640b-260">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="6640b-260">MicrosoftWindowsServer</span></span> | <span data-ttu-id="6640b-261">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="6640b-261">WindowsServer</span></span> | <span data-ttu-id="6640b-262">2012-R2-Datacenter</span><span class="sxs-lookup"><span data-stu-id="6640b-262">2012-R2-Datacenter</span></span> | <span data-ttu-id="6640b-263">le plus récent</span><span class="sxs-lookup"><span data-stu-id="6640b-263">latest</span></span> | <span data-ttu-id="6640b-264">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="6640b-264">batch.node.windows amd64</span></span> |
| <span data-ttu-id="6640b-265">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="6640b-265">MicrosoftWindowsServer</span></span> | <span data-ttu-id="6640b-266">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="6640b-266">WindowsServer</span></span> | <span data-ttu-id="6640b-267">2016-centre-de-données</span><span class="sxs-lookup"><span data-stu-id="6640b-267">2016-Datacenter</span></span> | <span data-ttu-id="6640b-268">le plus récent</span><span class="sxs-lookup"><span data-stu-id="6640b-268">latest</span></span> | <span data-ttu-id="6640b-269">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="6640b-269">batch.node.windows amd64</span></span> |
| <span data-ttu-id="6640b-270">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="6640b-270">MicrosoftWindowsServer</span></span> | <span data-ttu-id="6640b-271">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="6640b-271">WindowsServer</span></span> | <span data-ttu-id="6640b-272">2016-centre-de-données-avec-conteneurs</span><span class="sxs-lookup"><span data-stu-id="6640b-272">2016-Datacenter-with-Containers</span></span> | <span data-ttu-id="6640b-273">le plus récent</span><span class="sxs-lookup"><span data-stu-id="6640b-273">latest</span></span> | <span data-ttu-id="6640b-274">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="6640b-274">batch.node.windows amd64</span></span> |

## <a name="connect-toolinux-nodes-using-ssh"></a><span data-ttu-id="6640b-275">Connectez les nœuds tooLinux à l’aide de SSH</span><span class="sxs-lookup"><span data-stu-id="6640b-275">Connect tooLinux nodes using SSH</span></span>
<span data-ttu-id="6640b-276">Pendant le développement ou lors de la résolution des problèmes, vous souhaiterez peut-être toosign nécessaire dans les nœuds de toohello dans le pool.</span><span class="sxs-lookup"><span data-stu-id="6640b-276">During development or while troubleshooting, you may find it necessary toosign in toohello nodes in your pool.</span></span> <span data-ttu-id="6640b-277">Contrairement aux nœuds de calcul de Windows, vous ne pouvez pas utiliser les nœuds de tooLinux tooconnect de protocole RDP (Remote Desktop).</span><span class="sxs-lookup"><span data-stu-id="6640b-277">Unlike Windows compute nodes, you cannot use Remote Desktop Protocol (RDP) tooconnect tooLinux nodes.</span></span> <span data-ttu-id="6640b-278">Au lieu de cela, hello service Batch permet l’accès SSH sur chaque nœud pour la connexion à distance.</span><span class="sxs-lookup"><span data-stu-id="6640b-278">Instead, hello Batch service enables SSH access on each node for remote connection.</span></span>

<span data-ttu-id="6640b-279">Hello extrait de code Python suivant crée un utilisateur sur chaque nœud dans un pool, qui est requis pour la connexion à distance.</span><span class="sxs-lookup"><span data-stu-id="6640b-279">hello following Python code snippet creates a user on each node in a pool, which is required for remote connection.</span></span> <span data-ttu-id="6640b-280">Il imprime ensuite les informations de connexion hello SSH (secure shell) pour chaque nœud.</span><span class="sxs-lookup"><span data-stu-id="6640b-280">It then prints hello secure shell (SSH) connection information for each node.</span></span>

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

# Specify hello ID of an existing pool containing Linux nodes
# currently in hello 'idle' state
pool_id = ''

# Specify hello username and prompt for a password
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

# Create hello user that will be added tooeach node in hello pool
user = batchmodels.ComputeNodeUser(username)
user.password = password
user.is_admin = True
user.expiry_time = \
    (datetime.datetime.today() + datetime.timedelta(days=30)).isoformat()

# Get hello list of nodes in hello pool
nodes = batch_client.compute_node.list(pool_id)

# Add hello user tooeach node in hello pool and print
# hello connection information for hello node
for node in nodes:
    # Add hello user toohello node
    batch_client.compute_node.add_user(pool_id, node.id, user)

    # Obtain SSH login information for hello node
    login = batch_client.compute_node.get_remote_login_settings(pool_id,
                                                                node.id)

    # Print hello connection info for hello node
    print("{0} | {1} | {2} | {3}".format(node.id,
                                         node.state,
                                         login.remote_login_ip_address,
                                         login.remote_login_port))
```

<span data-ttu-id="6640b-281">Voici un exemple de sortie pour le code précédent hello pour un pool qui contient quatre nœuds Linux :</span><span class="sxs-lookup"><span data-stu-id="6640b-281">Here is sample output for hello previous code for a pool that contains four Linux nodes:</span></span>

```
Password:
tvm-1219235766_1-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50000
tvm-1219235766_2-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50003
tvm-1219235766_3-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50002
tvm-1219235766_4-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50001
```

<span data-ttu-id="6640b-282">Au lieu d’un mot de passe, vous pouvez spécifier une clé publique SSH lorsque vous créez un utilisateur sur un nœud.</span><span class="sxs-lookup"><span data-stu-id="6640b-282">Instead of a password, you can specify an SSH public key when you create a user on a node.</span></span> <span data-ttu-id="6640b-283">Bonjour Python SDK, utilisez hello **ssh_public_key** paramètre sur [ComputeNodeUser][py_computenodeuser].</span><span class="sxs-lookup"><span data-stu-id="6640b-283">In hello Python SDK, use hello **ssh_public_key** parameter on [ComputeNodeUser][py_computenodeuser].</span></span> <span data-ttu-id="6640b-284">Dans .NET, utilisez hello [ComputeNodeUser][net_computenodeuser].[ Paramètres SshPublicKey] [ net_ssh_key] propriété.</span><span class="sxs-lookup"><span data-stu-id="6640b-284">In .NET, use hello [ComputeNodeUser][net_computenodeuser].[SshPublicKey][net_ssh_key] property.</span></span>

## <a name="pricing"></a><span data-ttu-id="6640b-285">Tarification</span><span class="sxs-lookup"><span data-stu-id="6640b-285">Pricing</span></span>
<span data-ttu-id="6640b-286">Azure Batch est basé sur la technologie d’Azure Cloud Services et des machines virtuelles Azure.</span><span class="sxs-lookup"><span data-stu-id="6640b-286">Azure Batch is built on Azure Cloud Services and Azure Virtual Machines technology.</span></span> <span data-ttu-id="6640b-287">Hello service Batch lui-même est proposé gratuitement, ce qui signifie que vous êtes facturé uniquement pour hello des ressources qui consomment de vos solutions de traitement par lots de calcul.</span><span class="sxs-lookup"><span data-stu-id="6640b-287">hello Batch service itself is offered at no cost, which means you are charged only for hello compute resources that your Batch solutions consume.</span></span> <span data-ttu-id="6640b-288">Lorsque vous choisissez **Configuration des Services Cloud**, vous êtes facturé en fonction de hello [tarification des Services de cloud computing] [ cloud_services_pricing] structure.</span><span class="sxs-lookup"><span data-stu-id="6640b-288">When you choose **Cloud Services Configuration**, you are charged based on hello [Cloud Services pricing][cloud_services_pricing] structure.</span></span> <span data-ttu-id="6640b-289">Lorsque vous choisissez **Configuration d’ordinateur virtuel**, vous êtes facturé en fonction de hello [Machines virtuelles tarification] [ vm_pricing] structure.</span><span class="sxs-lookup"><span data-stu-id="6640b-289">When you choose **Virtual Machine Configuration**, you are charged based on hello [Virtual Machines pricing][vm_pricing] structure.</span></span> 

<span data-ttu-id="6640b-290">Si vous déployez des applications tooyour lot nœuds à l’aide de [les packages d’applications](batch-application-packages.md), vous êtes également facturé pour les ressources de stockage Azure hello que vos packages d’application consomment.</span><span class="sxs-lookup"><span data-stu-id="6640b-290">If you deploy applications tooyour Batch nodes using [application packages](batch-application-packages.md), you are also charged for hello Azure Storage resources that your application packages consume.</span></span> <span data-ttu-id="6640b-291">En général, les coûts de stockage Azure hello sont minimes.</span><span class="sxs-lookup"><span data-stu-id="6640b-291">In general, hello Azure Storage costs are minimal.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="6640b-292">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6640b-292">Next steps</span></span>
### <a name="batch-python-tutorial"></a><span data-ttu-id="6640b-293">Didacticiel Python Batch</span><span class="sxs-lookup"><span data-stu-id="6640b-293">Batch Python tutorial</span></span>
<span data-ttu-id="6640b-294">Pour obtenir un didacticiel plus détaillé sur la façon toowork traitement par lots à l’aide de Python, extraction [prise en main client de Python de traitement par lots Azure hello](batch-python-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="6640b-294">For a more in-depth tutorial about how toowork with Batch by using Python, check out [Get started with hello Azure Batch Python client](batch-python-tutorial.md).</span></span> <span data-ttu-id="6640b-295">Le Guide de son [exemple de code] [ github_samples_pyclient] inclut une fonction d’assistance, `get_vm_config_for_distro`, qui affiche une autre technique tooobtain une configuration d’ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="6640b-295">Its companion [code sample][github_samples_pyclient] includes a helper function, `get_vm_config_for_distro`, that shows another technique tooobtain a virtual machine configuration.</span></span>

### <a name="batch-python-code-samples"></a><span data-ttu-id="6640b-296">Exemples de code Batch Python</span><span class="sxs-lookup"><span data-stu-id="6640b-296">Batch Python code samples</span></span>
<span data-ttu-id="6640b-297">Hello [exemples de code Python] [ github_samples_py] Bonjour [exemples de traitement par lots azure] [ github_samples] référentiel sur GitHub contient des scripts qui vous montrent comment tooperform opérations de traitement courantes, telles que le pool de travail et la création de tâches.</span><span class="sxs-lookup"><span data-stu-id="6640b-297">hello [Python code samples][github_samples_py] in hello [azure-batch-samples][github_samples] repository on GitHub contain scripts that show you how tooperform common Batch operations, such as pool, job, and task creation.</span></span> <span data-ttu-id="6640b-298">Hello [Lisez-moi] [ github_py_readme] qui accompagnent les exemples de Python hello a plus d’informations sur comment tooinstall hello requises des packages.</span><span class="sxs-lookup"><span data-stu-id="6640b-298">hello [README][github_py_readme] that accompanies hello Python samples has details about how tooinstall hello required packages.</span></span>

### <a name="batch-forum"></a><span data-ttu-id="6640b-299">Forum Azure Batch</span><span class="sxs-lookup"><span data-stu-id="6640b-299">Batch forum</span></span>
<span data-ttu-id="6640b-300">Hello [Forum de traitement par lots Azure] [ forum] sur MSDN est une bonne placer toodiscuss lot et poser des questions sur le service de hello.</span><span class="sxs-lookup"><span data-stu-id="6640b-300">hello [Azure Batch Forum][forum] on MSDN is a great place toodiscuss Batch and ask questions about hello service.</span></span> <span data-ttu-id="6640b-301">Consultez le forum pour obtenir des publications « épinglées » utiles, et publiez les questions que vous vous posez pendant la création de vos solutions Batch.</span><span class="sxs-lookup"><span data-stu-id="6640b-301">Read helpful "pinned" posts, and post your questions as they arise while you build your Batch solutions.</span></span>

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
