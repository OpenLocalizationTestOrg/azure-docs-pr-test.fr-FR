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
# <a name="provision-linux-compute-nodes-in-batch-pools"></a>Configurer des nœuds de calcul Linux dans des pools Batch

Vous pouvez utiliser les charges de travail de traitement par lots Azure toorun calcul parallèle sur les ordinateurs virtuels Linux et Windows. Cet article décrit en détail comment pools toocreate de Linux nœuds de calcul dans le service de traitement par lots hello à l’aide de deux hello [lot Python] [ py_batch_package] et [Batch .NET] [ api_net] les bibliothèques clientes.

> [!NOTE]
> Les packages d’applications sont pris en charge sur tous les pools Batch créés après le 5 juillet 2017. Elles sont prises en charge sur les pools de traitement par lots créés entre 10 mars 2016 et 5 juillet 2017 uniquement si le pool de hello a été créé à l’aide d’une configuration de Service Cloud. Les pools de lot créés too10 préalable mars 2016 ne gèrent pas les packages d’applications. Pour plus d’informations sur l’application à l’aide de packages toodeploy vos nœuds de traitement par lots tooyour applications, consultez [déployer des nœuds de toocompute d’applications avec des packages d’application de lot](batch-application-packages.md).
>
>

## <a name="virtual-machine-configuration"></a>Configuration de la machine virtuelle
Lorsque vous créez un pool de nœuds de calcul dans un lot, vous avez deux options quelle taille de nœud tooselect hello et le système d’exploitation : Configuration des Services Cloud et la Configuration d’ordinateur virtuel.

**configuration des services cloud** fournit *uniquement*des nœuds de calcul Windows. Tailles de nœud de calcul disponibles sont répertoriés dans [tailles pour les Services de Cloud](../cloud-services/cloud-services-sizes-specs.md), et les systèmes d’exploitation disponibles sont répertoriés dans hello [versions de système d’exploitation invité de Azure et matrice de compatibilité SDK](../cloud-services/cloud-services-guestos-update-matrix.md). Lorsque vous créez un pool qui contient les nœuds des Services de cloud computing Azure, vous spécifiez la taille du nœud hello et hello famille de systèmes d’exploitation, qui sont décrites dans hello mentionné précédemment articles. Pour les pools de nœuds de calcul Windows, les services Cloud Services sont le plus couramment utilisés.

**Virtual Machine Configuration** fournit des images Linux et Windows pour les nœuds de calcul. Les tailles de nœud de calcul disponibles sont répertoriées dans [Tailles des machines virtuelles dans Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux) et [Tailles des machines virtuelles dans Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows). Lorsque vous créez un pool qui contient les nœuds de la Configuration d’ordinateur virtuel, vous devez spécifier la taille hello de nœuds de hello, référence d’image de machine virtuelle de hello et toobe SKU hello lot nœud agent installé sur les nœuds hello.

### <a name="virtual-machine-image-reference"></a>Référence de l’image de la machine virtuelle
Hello par service de traitement par lots [machines virtuelles identiques](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) tooprovide Linux des nœuds de calcul. Vous pouvez spécifier une image à partir de hello [Azure Marketplace][vm_marketplace], ou fournir une image personnalisée que vous avez préparé. Pour en savoir plus sur les images personnalisées, consultez [Develop large-scale parallel compute solutions with Batch](batch-api-basics.md#pool) (Développer des solutions de calcul parallèles à grande échelle avec Batch).

Lorsque vous configurez une référence d’image de machine virtuelle, vous spécifiez les propriétés de hello d’image de machine virtuelle hello. Hello propriétés suivantes est requise lorsque vous créez une référence d’image de machine virtuelle :

| **Propriétés de référence d’image** | **Exemple** |
| --- | --- |
| Publisher |Canonical |
| Offer |UbuntuServer |
| SKU |14.04.4-LTS |
| Version |le plus récent |

> [!TIP]
> Plus d’informations sur ces propriétés et comment les images toolist Marketplace dans [naviguer et sélectionnez images de machine virtuelle Linux dans Azure avec l’interface CLI ou PowerShell](../virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Notez que toutes les images Marketplace ne sont pas compatibles avec Batch pour le moment. Pour plus d’informations, consultez la rubrique [Référence de l’agent de nœud](#node-agent-sku)ci-dessous.
>
>

### <a name="node-agent-sku"></a>Référence de l’agent de nœud
agent de nœud de traitement par lots Hello est un programme qui s’exécute sur chaque nœud dans le pool de hello et fournit l’interface de commande et contrôle hello entre le nœud de hello et service de traitement par lots hello. Il existe différentes implémentations de l’agent de nœud hello, connus en tant que références (SKU), pour les différents systèmes d’exploitation. Essentiellement, lorsque vous créez une Configuration de Machine virtuelle, vous spécifiez tout d’abord la référence d’image de machine virtuelle de hello, puis vous spécifiez hello nœud agent tooinstall sur l’image de hello. En règle générale, chaque référence d’agent de nœud est compatible avec plusieurs images de machine virtuelle. Voici quelques exemples de références d’agent de nœud :

* batch.node.ubuntu 14.04
* batch.node.centos 7
* batch.node.windows amd64

> [!IMPORTANT]
> Pas toutes les images de machine virtuelle qui sont disponibles dans hello Marketplace sont compatibles avec les agents de nœud hello actuellement disponibles par lots. Hello kits de développement logiciel lot toolist hello nœud disponible agent SKU et hello des images de machine virtuelle avec lesquels ils sont compatibles. Consultez hello [images de la liste de la Machine virtuelle](#list-of-virtual-machine-images) plus loin dans cet article pour plus d’informations et obtenir des exemples de tooretrieve une liste d’images valides lors de l’exécution.
>
>

## <a name="create-a-linux-pool-batch-python"></a>Créer un pool Linux : Batch Python
Hello extrait de code suivant illustre un exemple de toouse hello [bibliothèque du Client Microsoft Azure Batch pour Python] [ py_batch_package] toocreate un pool d’Ubuntu Server des nœuds de calcul. Consultez la documentation pour hello trouverez de module de traitement par lots Python [azure.batch package] [ py_batch_docs] des documents de hello en lecture.

Cet extrait de code crée explicitement un paramètre [ImageReference][py_imagereference] et spécifie chacune de ses propriétés (éditeur, offre, référence, version). Dans le code de production, cependant, nous vous recommandons d’utiliser hello [list_node_agent_skus] [ py_list_skus] toodetermine de méthode et de sélectionner parmi hello image et le nœud agent SKU combinaisons disponibles lors de l’exécution.

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

Comme mentionné précédemment, nous vous recommandons au lieu de créer hello [ImageReference] [ py_imagereference] explicitement, vous utilisez hello [list_node_agent_skus] [ py_list_skus] sélectionnez toodynamically de méthode à partir de hello pris en charge actuellement les combinaisons d’image du nœud agent/Marketplace. Hello suivant indique le code Python comment toouse cette méthode.

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

## <a name="create-a-linux-pool-batch-net"></a>Créer un pool Linux : Batch .NET
Hello extrait de code suivant illustre un exemple de toouse hello [Batch .NET] [ nuget_batch_net] toocreate de bibliothèque client un pool d’Ubuntu Server des nœuds de calcul. Vous pouvez trouver hello [documentation de référence .NET de lot] [ api_net] sur MSDN.

Hello extrait de code suivant utilise hello [PoolOperations][net_pool_ops].[ ListNodeAgentSkus] [ net_list_skus] tooselect de méthode dans liste hello actuellement combinaisons prises en charge Marketplace image et le nœud agent référence (SKU). Cette technique est souhaitable, car la liste hello des combinaisons prises en charge peut-être changer d’heure tootime. En règle générale, les combinaisons prises en charge sont ajoutées.

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

Bien que l’extrait de code précédent hello utilise hello [PoolOperations][net_pool_ops].[ ListNodeAgentSkus] [ net_list_skus] toodynamically (méthode) et sélectionnez prise en charge d’image et le nœud de combinaisons de référence (SKU) de l’agent (recommandés), vous pouvez également configurer un [ImageReference] [ net_imagereference] explicitement :

```csharp
ImageReference imageReference = new ImageReference(
    publisher: "Canonical",
    offer: "UbuntuServer",
    sku: "14.04.2-LTS",
    version: "latest");
```

## <a name="list-of-virtual-machine-images"></a>liste des images de machine virtuelle
Hello tableau suivant répertorie les images de machine virtuelle hello Marketplace qui sont compatibles avec les agents de nœud de traitement disponibles hello lors de la dernière mise à jour de cet article. Il est important toonote que cette liste n’est pas définitive, car les images et les agents de nœud peuvent ajouter ou supprimer à tout moment. Nous recommandons de vos applications de traitement par lots et services toujours utilisent [list_node_agent_skus] [ py_list_skus] (Python) et [ListNodeAgentSkus] [ net_list_skus] Les toodetermine (lot .NET) et sélectionner parmi hello références actuellement disponibles.

> [!WARNING]
> Hello suivant liste peut changer à tout moment. Utilisez toujours hello **agent du nœud liste référence (SKU)** méthodes disponibles dans toolist d’API de lot hello hello machine virtuelle compatibles et l’agent de nœud Références (SKU) lorsque vous exécutez vos traitements par lots.
>
>

| **Publisher** | **Offer** | **Référence d’image** | **Version** | **ID de référence de l’agent de nœud** |
| ------------- | --------- | ------------- | ----------- | --------------------- |
| Canonical | UbuntuServer | 14.04.5-LTS | le plus récent | batch.node.ubuntu 14.04 |
| Canonical | UbuntuServer | 16.04.0-LTS | le plus récent | batch.node.ubuntu 16.04 |
| Credativ | Debian | 8 | le plus récent | batch.node.debian 8 |
| OpenLogic | CentOS | 7.0 | le plus récent | batch.node.centos 7 |
| OpenLogic | CentOS | 7.1 | le plus récent | batch.node.centos 7 |
| OpenLogic | CentOS-HPC | 7.1 | le plus récent | batch.node.centos 7 |
| OpenLogic | CentOS | 7,2 | le plus récent | batch.node.centos 7 |
| Oracle | Oracle-Linux | 7.0 | le plus récent | batch.node.centos 7 |
| Oracle | Oracle-Linux | 7,2 | le plus récent | batch.node.centos 7 |
| SUSE | openSUSE | 13.2 | le plus récent | batch.node.opensuse 13.2 |
| SUSE | openSUSE-Leap | 42.1 | le plus récent | batch.node.opensuse 42.1 |
| SUSE | SLES | 12-SP1 | le plus récent | batch.node.opensuse 42.1 |
| SUSE | SLES-HPC | 12-SP1 | le plus récent | batch.node.opensuse 42.1 |
| microsoft-ads | linux-data-science-vm | linuxdsvm | le plus récent | batch.node.centos 7 |
| microsoft-ads | standard-data-science-vm | standard-data-science-vm | le plus récent | batch.node.windows amd64 |
| MicrosoftWindowsServer | WindowsServer | 2008-R2-SP1 | le plus récent | batch.node.windows amd64 |
| MicrosoftWindowsServer | WindowsServer | 2012-Datacenter | le plus récent | batch.node.windows amd64 |
| MicrosoftWindowsServer | WindowsServer | 2012-R2-Datacenter | le plus récent | batch.node.windows amd64 |
| MicrosoftWindowsServer | WindowsServer | 2016-centre-de-données | le plus récent | batch.node.windows amd64 |
| MicrosoftWindowsServer | WindowsServer | 2016-centre-de-données-avec-conteneurs | le plus récent | batch.node.windows amd64 |

## <a name="connect-toolinux-nodes-using-ssh"></a>Connectez les nœuds tooLinux à l’aide de SSH
Pendant le développement ou lors de la résolution des problèmes, vous souhaiterez peut-être toosign nécessaire dans les nœuds de toohello dans le pool. Contrairement aux nœuds de calcul de Windows, vous ne pouvez pas utiliser les nœuds de tooLinux tooconnect de protocole RDP (Remote Desktop). Au lieu de cela, hello service Batch permet l’accès SSH sur chaque nœud pour la connexion à distance.

Hello extrait de code Python suivant crée un utilisateur sur chaque nœud dans un pool, qui est requis pour la connexion à distance. Il imprime ensuite les informations de connexion hello SSH (secure shell) pour chaque nœud.

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

Voici un exemple de sortie pour le code précédent hello pour un pool qui contient quatre nœuds Linux :

```
Password:
tvm-1219235766_1-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50000
tvm-1219235766_2-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50003
tvm-1219235766_3-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50002
tvm-1219235766_4-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50001
```

Au lieu d’un mot de passe, vous pouvez spécifier une clé publique SSH lorsque vous créez un utilisateur sur un nœud. Bonjour Python SDK, utilisez hello **ssh_public_key** paramètre sur [ComputeNodeUser][py_computenodeuser]. Dans .NET, utilisez hello [ComputeNodeUser][net_computenodeuser].[ Paramètres SshPublicKey] [ net_ssh_key] propriété.

## <a name="pricing"></a>Tarification
Azure Batch est basé sur la technologie d’Azure Cloud Services et des machines virtuelles Azure. Hello service Batch lui-même est proposé gratuitement, ce qui signifie que vous êtes facturé uniquement pour hello des ressources qui consomment de vos solutions de traitement par lots de calcul. Lorsque vous choisissez **Configuration des Services Cloud**, vous êtes facturé en fonction de hello [tarification des Services de cloud computing] [ cloud_services_pricing] structure. Lorsque vous choisissez **Configuration d’ordinateur virtuel**, vous êtes facturé en fonction de hello [Machines virtuelles tarification] [ vm_pricing] structure. 

Si vous déployez des applications tooyour lot nœuds à l’aide de [les packages d’applications](batch-application-packages.md), vous êtes également facturé pour les ressources de stockage Azure hello que vos packages d’application consomment. En général, les coûts de stockage Azure hello sont minimes. 

## <a name="next-steps"></a>Étapes suivantes
### <a name="batch-python-tutorial"></a>Didacticiel Python Batch
Pour obtenir un didacticiel plus détaillé sur la façon toowork traitement par lots à l’aide de Python, extraction [prise en main client de Python de traitement par lots Azure hello](batch-python-tutorial.md). Le Guide de son [exemple de code] [ github_samples_pyclient] inclut une fonction d’assistance, `get_vm_config_for_distro`, qui affiche une autre technique tooobtain une configuration d’ordinateur virtuel.

### <a name="batch-python-code-samples"></a>Exemples de code Batch Python
Hello [exemples de code Python] [ github_samples_py] Bonjour [exemples de traitement par lots azure] [ github_samples] référentiel sur GitHub contient des scripts qui vous montrent comment tooperform opérations de traitement courantes, telles que le pool de travail et la création de tâches. Hello [Lisez-moi] [ github_py_readme] qui accompagnent les exemples de Python hello a plus d’informations sur comment tooinstall hello requises des packages.

### <a name="batch-forum"></a>Forum Azure Batch
Hello [Forum de traitement par lots Azure] [ forum] sur MSDN est une bonne placer toodiscuss lot et poser des questions sur le service de hello. Consultez le forum pour obtenir des publications « épinglées » utiles, et publiez les questions que vous vous posez pendant la création de vos solutions Batch.

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
