---
title: "Créer et gérer une machine virtuelle Windows dans Azure à l’aide de Python | Microsoft Docs"
description: "Apprenez à utiliser Python pour créer et gérer une machine virtuelle Windows dans Azure."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: davidmu
ms.openlocfilehash: bb777d41570d7b1dc97402d532519488912948e3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-manage-windows-vms-in-azure-using-python"></a><span data-ttu-id="726e9-103">Créer et gérer des machines virtuelles Windows dans Azure à l’aide de Python</span><span class="sxs-lookup"><span data-stu-id="726e9-103">Create and manage Windows VMs in Azure using Python</span></span>

<span data-ttu-id="726e9-104">Une [Machine virtuelle Azure](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) a besoin de plusieurs ressources de prise en charge Azure.</span><span class="sxs-lookup"><span data-stu-id="726e9-104">An [Azure Virtual Machine](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) needs several supporting Azure resources.</span></span> <span data-ttu-id="726e9-105">Cet article décrit la création, la gestion et la suppression de ressources de machine virtuelle à l’aide de Python.</span><span class="sxs-lookup"><span data-stu-id="726e9-105">This article covers creating, managing, and deleting VM resources using Python.</span></span> <span data-ttu-id="726e9-106">Vous allez apprendre à effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="726e9-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="726e9-107">Créer un projet Visual Studio</span><span class="sxs-lookup"><span data-stu-id="726e9-107">Create a Visual Studio project</span></span>
> * <span data-ttu-id="726e9-108">Installer des packages</span><span class="sxs-lookup"><span data-stu-id="726e9-108">Install packages</span></span>
> * <span data-ttu-id="726e9-109">Créer des informations d’identification</span><span class="sxs-lookup"><span data-stu-id="726e9-109">Create credentials</span></span>
> * <span data-ttu-id="726e9-110">Créer des ressources</span><span class="sxs-lookup"><span data-stu-id="726e9-110">Create resources</span></span>
> * <span data-ttu-id="726e9-111">Effectuer les tâches de gestion</span><span class="sxs-lookup"><span data-stu-id="726e9-111">Perform management tasks</span></span>
> * <span data-ttu-id="726e9-112">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="726e9-112">Delete resources</span></span>
> * <span data-ttu-id="726e9-113">Exécution de l'application</span><span class="sxs-lookup"><span data-stu-id="726e9-113">Run the application</span></span>

<span data-ttu-id="726e9-114">Ces étapes prennent environ 20 minutes.</span><span class="sxs-lookup"><span data-stu-id="726e9-114">It takes about 20 minutes to do these steps.</span></span>

## <a name="create-a-visual-studio-project"></a><span data-ttu-id="726e9-115">Créer un projet Visual Studio</span><span class="sxs-lookup"><span data-stu-id="726e9-115">Create a Visual Studio project</span></span>

1. <span data-ttu-id="726e9-116">Si vous ne l’avez pas déjà fait, installez [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="726e9-116">If you haven't already, install [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span></span> <span data-ttu-id="726e9-117">Dans la page Charges de travail, sélectionnez **Développement Python**, puis cliquez sur **Installer**.</span><span class="sxs-lookup"><span data-stu-id="726e9-117">Select **Python development** on the Workloads page, and then click **Install**.</span></span> <span data-ttu-id="726e9-118">Dans le résumé, vous pouvez voir que **Python 3 64 bits (3.6.0)** est automatiquement sélectionné pour vous.</span><span class="sxs-lookup"><span data-stu-id="726e9-118">In the summary, you can see that **Python 3 64-bit (3.6.0)** is automatically selected for you.</span></span> <span data-ttu-id="726e9-119">Si vous avez déjà installé Visual Studio, vous pouvez ajouter la charge de travail Python en utilisant le Lanceur de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="726e9-119">If you have already installed Visual Studio, you can add the Python workload using the Visual Studio Launcher.</span></span>
2. <span data-ttu-id="726e9-120">Après avoir installé et démarré Visual Studio, cliquez sur **Fichier** > **Nouveau** > **Projet**.</span><span class="sxs-lookup"><span data-stu-id="726e9-120">After installing and starting Visual Studio, click **File** > **New** > **Project**.</span></span>
3. <span data-ttu-id="726e9-121">Cliquez sur **Modèles** > **Python** > **Application Python**, entrez *monProjetPython* comme nom pour le projet, sélectionnez l’emplacement du projet, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="726e9-121">Click **Templates** > **Python** > **Python Application**, enter *myPythonProject* for the name of the project, select the location of the project, and then click **OK**.</span></span>

## <a name="install-packages"></a><span data-ttu-id="726e9-122">Installer des packages</span><span class="sxs-lookup"><span data-stu-id="726e9-122">Install packages</span></span>

1. <span data-ttu-id="726e9-123">Dans l’Explorateur de solutions, sous *monProjetPython*, cliquez avec le bouton droit sur **Environnements Python**, puis sélectionnez **Ajouter un environnement virtuel**.</span><span class="sxs-lookup"><span data-stu-id="726e9-123">In Solution Explorer, under *myPythonProject*, right-click **Python Environments**, and then select **Add virtual environment**.</span></span>
2. <span data-ttu-id="726e9-124">Dans l’écran Ajouter un environnement virtuel, acceptez le nom par défaut *env*, assurez-vous que *Python 3.6 (64 bits)* est sélectionné pour l’interpréteur de base, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="726e9-124">On the Add Virtual Environment screen, accept the default name of *env*, make sure that *Python 3.6 (64-bit)* is selected for the base interpreter, and then click **Create**.</span></span>
3. <span data-ttu-id="726e9-125">Cliquez avec le bouton droit sur l’environnement *env* que vous avez créé, cliquez sur **Installer le package Python**, entrez *azure* dans la zone de recherche, puis appuyez sur Entrée.</span><span class="sxs-lookup"><span data-stu-id="726e9-125">Right-click the *env* environment that you created, click **Install Python Package**, enter *azure* in the search box, and then press Enter.</span></span>

<span data-ttu-id="726e9-126">Dans les fenêtres de sortie, vous devriez voir que les packages Azure ont été correctement installés.</span><span class="sxs-lookup"><span data-stu-id="726e9-126">You should see in the output windows that the azure packages were successfully installed.</span></span> 

## <a name="create-credentials"></a><span data-ttu-id="726e9-127">Créer des informations d’identification</span><span class="sxs-lookup"><span data-stu-id="726e9-127">Create credentials</span></span>

<span data-ttu-id="726e9-128">Avant de commencer cette étape, assurez-vous que vous disposez d’un [principal du service Active Directory](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="726e9-128">Before you start this step, make sure that you have an [Active Directory service principal](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="726e9-129">Vous devez également enregistrer l’ID d’application, la clé d’authentification et l’ID de client dont vous aurez besoin dans une étape ultérieure.</span><span class="sxs-lookup"><span data-stu-id="726e9-129">You should also record the application ID, the authentication key, and the tenant ID that you need in a later step.</span></span>

1. <span data-ttu-id="726e9-130">Ouvrez le fichier *monProjetPython.py* qui a été créé, puis ajoutez ce code pour permettre à votre application de s’exécuter :</span><span class="sxs-lookup"><span data-stu-id="726e9-130">Open *myPythonProject.py* file that was created, and then add this code to enable your application to run:</span></span>

    ```python
    if __name__ == "__main__":
    ```

2. <span data-ttu-id="726e9-131">Pour importer le code nécessaire, ajoutez les instructions suivantes au début du fichier .py :</span><span class="sxs-lookup"><span data-stu-id="726e9-131">To import the code that is needed, add these statements to the top of the .py file:</span></span>

    ```python
    from azure.common.credentials import ServicePrincipalCredentials
    from azure.mgmt.resource import ResourceManagementClient
    from azure.mgmt.compute import ComputeManagementClient
    from azure.mgmt.network import NetworkManagementClient
    from azure.mgmt.compute.models import DiskCreateOption
    ```

3. <span data-ttu-id="726e9-132">Ensuite dans le fichier .py, ajoutez des variables après les instructions d’importation pour spécifier des valeurs communes utilisées dans le code :</span><span class="sxs-lookup"><span data-stu-id="726e9-132">Next in the .py file, add variables after the import statements to specify common values used in the code:</span></span>
   
    ```
    SUBSCRIPTION_ID = 'subscription-id'
    GROUP_NAME = 'myResourceGroup'
    LOCATION = 'westus'
    VM_NAME = 'myVM'
    ```

    <span data-ttu-id="726e9-133">Remplacez **subscription-id** par votre identificateur d’abonnement.</span><span class="sxs-lookup"><span data-stu-id="726e9-133">Replace **subscription-id** with your subscription identifier.</span></span>

4. <span data-ttu-id="726e9-134">Pour créer les informations d’identification Active Directory dont vous avez besoin pour effectuer des demandes, ajoutez la fonction suivant après les variables dans le fichier .py :</span><span class="sxs-lookup"><span data-stu-id="726e9-134">To create the Active Directory credentials that you need to make requests, add this function after the variables in the .py file:</span></span>

    ```python
    def get_credentials():
        credentials = ServicePrincipalCredentials(
            client_id = 'application-id',
            secret = 'authentication-key',
            tenant = 'tenant-id'
        )

        return credentials
    ```

    <span data-ttu-id="726e9-135">Remplacez **application-id**, **authentication-key** et **tenant-id** par les valeurs que vous avez collectées précédemment lors de la création de votre principal du service Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="726e9-135">Replace **application-id**, **authentication-key**, and **tenant-id** with the values that you previously collected when you created your Azure Active Directory service principal.</span></span>

5. <span data-ttu-id="726e9-136">Pour appeler la fonction que vous avez ajoutée précédemment, ajoutez le code suivant sous l’instruction **if** à la fin du fichier .py :</span><span class="sxs-lookup"><span data-stu-id="726e9-136">To call the function that you previously added, add this code under the **if** statement at the end of the .py file:</span></span>

    ```python
    credentials = get_credentials()
    ```

## <a name="create-resources"></a><span data-ttu-id="726e9-137">Créer des ressources</span><span class="sxs-lookup"><span data-stu-id="726e9-137">Create resources</span></span>
 
### <a name="initialize-management-clients"></a><span data-ttu-id="726e9-138">Initialiser des clients de gestion</span><span class="sxs-lookup"><span data-stu-id="726e9-138">Initialize management clients</span></span>

<span data-ttu-id="726e9-139">Des clients de gestion sont nécessaires pour créer et gérer des ressources à l’aide du Kit de développement logiciel (SDK) Python dans Azure.</span><span class="sxs-lookup"><span data-stu-id="726e9-139">Management clients are needed to create and manage resources using the Python SDK in Azure.</span></span> <span data-ttu-id="726e9-140">Pour créer les clients de gestion, ajoutez le code suivant sous l’instruction **si** à la fin du fichier .py :</span><span class="sxs-lookup"><span data-stu-id="726e9-140">To create the management clients, add this code under the **if** statement at then end of the .py file:</span></span>

```python
resource_group_client = ResourceManagementClient(
    credentials, 
    SUBSCRIPTION_ID
)
network_client = NetworkManagementClient(
    credentials, 
    SUBSCRIPTION_ID
)
compute_client = ComputeManagementClient(
    credentials, 
    SUBSCRIPTION_ID
)
```

### <a name="create-the-vm-and-supporting-resources"></a><span data-ttu-id="726e9-141">Créer la machine virtuelle et les ressources de prise en charge</span><span class="sxs-lookup"><span data-stu-id="726e9-141">Create the VM and supporting resources</span></span>

<span data-ttu-id="726e9-142">Toutes les ressources doivent être contenues dans un [groupe de ressources](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="726e9-142">All resources must be contained in a [Resource group](../../azure-resource-manager/resource-group-overview.md).</span></span>

1. <span data-ttu-id="726e9-143">Pour créer un groupe de ressources, ajoutez la fonction suivante après les variables dans le fichier .py :</span><span class="sxs-lookup"><span data-stu-id="726e9-143">To create a resource group, add this function after the variables in the .py file:</span></span>

    ```python
    def create_resource_group(resource_group_client):
        resource_group_params = { 'location':LOCATION }
        resource_group_result = resource_group_client.resource_groups.create_or_update(
            GROUP_NAME, 
            resource_group_params
        )
    ```

2. <span data-ttu-id="726e9-144">Pour appeler la fonction que vous avez ajoutée précédemment, ajoutez le code suivant sous l’instruction **if** à la fin du fichier .py :</span><span class="sxs-lookup"><span data-stu-id="726e9-144">To call the function that you previously added, add this code under the **if** statement at the end of the .py file:</span></span>

    ```python
    create_resource_group(resource_group_client)
    input('Resource group created. Press enter to continue...')
    ```

<span data-ttu-id="726e9-145">Les [groupes à haute disponibilité](tutorial-availability-sets.md) facilitent la maintenance des machines virtuelles utilisées par votre application.</span><span class="sxs-lookup"><span data-stu-id="726e9-145">[Availability sets](tutorial-availability-sets.md) make it easier for you to maintain the virtual machines used by your application.</span></span>

1. <span data-ttu-id="726e9-146">Pour créer un groupe à haute disponibilité, ajoutez la fonction suivante après les variables dans le fichier .py :</span><span class="sxs-lookup"><span data-stu-id="726e9-146">To create an availability set, add this function after the variables in the .py file:</span></span>
   
    ```python
    def create_availability_set(compute_client):
        avset_params = {
            'location': LOCATION,
            'sku': { 'name': 'Aligned' },
            'platform_fault_domain_count': 3
        }
        availability_set_result = compute_client.availability_sets.create_or_update(
            GROUP_NAME,
            'myAVSet',
            avset_params
        )
    ```

2. <span data-ttu-id="726e9-147">Pour appeler la fonction que vous avez ajoutée précédemment, ajoutez le code suivant sous l’instruction **if** à la fin du fichier .py :</span><span class="sxs-lookup"><span data-stu-id="726e9-147">To call the function that you previously added, add this code under the **if** statement at the end of the .py file:</span></span>

    ```python
    create_availability_set(compute_client)
    print("------------------------------------------------------")
    input('Availability set created. Press enter to continue...')
    ```

<span data-ttu-id="726e9-148">Une [adresse IP publique](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) est nécessaire pour communiquer avec la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="726e9-148">A [Public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) is needed to communicate with the virtual machine.</span></span>

1. <span data-ttu-id="726e9-149">Pour créer une adresse IP publique pour la machine virtuelle, ajoutez la fonction suivante après les variables dans le fichier .py :</span><span class="sxs-lookup"><span data-stu-id="726e9-149">To create a public IP address for the virtual machine, add this function after the variables in the .py file:</span></span>

    ```python
    def create_public_ip_address(network_client):
        public_ip_addess_params = {
            'location': LOCATION,
            'public_ip_allocation_method': 'Dynamic'
        }
        creation_result = network_client.public_ip_addresses.create_or_update(
            GROUP_NAME,
            'myIPAddress',
            public_ip_addess_params
        )

        return creation_result.result()
    ```

2. <span data-ttu-id="726e9-150">Pour appeler la fonction que vous avez ajoutée précédemment, ajoutez le code suivant sous l’instruction **if** à la fin du fichier .py :</span><span class="sxs-lookup"><span data-stu-id="726e9-150">To call the function that you previously added, add this code under the **if** statement at the end of the .py file:</span></span>

    ```python
    creation_result = create_public_ip_address(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter to continue...')
    ```

<span data-ttu-id="726e9-151">Un machine virtuelle doit figurer dans un sous-réseau d’un [réseau virtuel](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="726e9-151">A virtual machine must be in a subnet of a [Virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="726e9-152">Pour créer un réseau virtuel, ajoutez la fonction suivante après les variables dans le fichier .py :</span><span class="sxs-lookup"><span data-stu-id="726e9-152">To create a virtual network, add this function after the variables in the .py file:</span></span>

    ```python
    def create_vnet(network_client):
        vnet_params = {
            'location': LOCATION,
            'address_space': {
                'address_prefixes': ['10.0.0.0/16']
            }
        }
        creation_result = network_client.virtual_networks.create_or_update(
            GROUP_NAME,
            'myVNet',
            vnet_params
        )
        return creation_result.result()
    ```

2. <span data-ttu-id="726e9-153">Pour appeler la fonction que vous avez ajoutée précédemment, ajoutez le code suivant sous l’instruction **if** à la fin du fichier .py :</span><span class="sxs-lookup"><span data-stu-id="726e9-153">To call the function that you previously added, add this code under the **if** statement at the end of the .py file:</span></span>
   
    ```python
    creation_result = create_vnet(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter to continue...')
    ```

3. <span data-ttu-id="726e9-154">Pour ajouter un sous-réseau au réseau virtuel, ajoutez la fonction suivante après les variables dans le fichier .py :</span><span class="sxs-lookup"><span data-stu-id="726e9-154">To add a subnet to the virtual network, add this function after the variables in the .py file:</span></span>
    
    ```python
    def create_subnet(network_client):
        subnet_params = {
            'address_prefix': '10.0.0.0/24'
        }
        creation_result = network_client.subnets.create_or_update(
            GROUP_NAME,
            'myVNet',
            'mySubnet',
            subnet_params
        )

        return creation_result.result()
    ```
        
4. <span data-ttu-id="726e9-155">Pour appeler la fonction que vous avez ajoutée précédemment, ajoutez le code suivant sous l’instruction **if** à la fin du fichier .py :</span><span class="sxs-lookup"><span data-stu-id="726e9-155">To call the function that you previously added, add this code under the **if** statement at the end of the .py file:</span></span>
   
    ```python
    creation_result = create_subnet(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter to continue...')
    ```

<span data-ttu-id="726e9-156">Une machine virtuelle a besoin d’une interface réseau pour communiquer sur le réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="726e9-156">A virtual machine needs a network interface to communicate on the virtual network.</span></span>

1. <span data-ttu-id="726e9-157">Pour créer une interface réseau, ajoutez la fonction suivante après les variables dans le fichier .py :</span><span class="sxs-lookup"><span data-stu-id="726e9-157">To create a network interface, add this function after the variables in the .py file:</span></span>

    ```python
    def create_nic(network_client):
        subnet_info = network_client.subnets.get(
            GROUP_NAME, 
            'myVNet', 
            'mySubnet'
        )
        publicIPAddress = network_client.public_ip_addresses.get(
            GROUP_NAME,
            'myIPAddress'
        )
        nic_params = {
            'location': LOCATION,
            'ip_configurations': [{
                'name': 'myIPConfig',
                'public_ip_address': publicIPAddress,
                'subnet': {
                    'id': subnet_info.id
                }
            }]
        }
        creation_result = network_client.network_interfaces.create_or_update(
            GROUP_NAME,
            'myNic',
            nic_params
        )

        return creation_result.result()
    ```

2. <span data-ttu-id="726e9-158">Pour appeler la fonction que vous avez ajoutée précédemment, ajoutez le code suivant sous l’instruction **if** à la fin du fichier .py :</span><span class="sxs-lookup"><span data-stu-id="726e9-158">To call the function that you previously added, add this code under the **if** statement at the end of the .py file:</span></span>

    ```python
    creation_result = create_nic(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter to continue...')
    ```

<span data-ttu-id="726e9-159">Maintenant que vous avez créé l’ensemble des ressources de prise en charge, vous pouvez créer une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="726e9-159">Now that you created all the supporting resources, you can create a virtual machine.</span></span>

1. <span data-ttu-id="726e9-160">Pour créer la machine virtuelle, ajoutez la fonction suivante après les variables dans le fichier .py :</span><span class="sxs-lookup"><span data-stu-id="726e9-160">To create the virtual machine, add this function after the variables in the .py file:</span></span>
   
    ```python
    def create_vm(network_client, compute_client):  
        nic = network_client.network_interfaces.get(
            GROUP_NAME, 
            'myNic'
        )
        avset = compute_client.availability_sets.get(
            GROUP_NAME,
            'myAVSet'
        )
        vm_parameters = {
            'location': LOCATION,
            'os_profile': {
                'computer_name': VM_NAME,
                'admin_username': 'azureuser',
                'admin_password': 'Azure12345678'
            },
            'hardware_profile': {
                'vm_size': 'Standard_DS1'
            },
            'storage_profile': {
                'image_reference': {
                    'publisher': 'MicrosoftWindowsServer',
                    'offer': 'WindowsServer',
                    'sku': '2012-R2-Datacenter',
                    'version': 'latest'
                }
            },
            'network_profile': {
                'network_interfaces': [{
                    'id': nic.id
                }]
            },
            'availability_set': {
                'id': avset.id
            }
        }
        creation_result = compute_client.virtual_machines.create_or_update(
            GROUP_NAME, 
            VM_NAME, 
            vm_parameters
        )
    
        return creation_result.result()
    ```

    > [!NOTE]
    > <span data-ttu-id="726e9-161">Ce didacticiel crée une machine virtuelle exécutant une version du système d’exploitation Windows Server.</span><span class="sxs-lookup"><span data-stu-id="726e9-161">This tutorial creates a virtual machine running a version of the Windows Server operating system.</span></span> <span data-ttu-id="726e9-162">Pour en savoir plus sur la sélection d’autres images, consultez [Parcourir et sélectionner des images de machine virtuelle Azure avec Windows PowerShell et l’interface CLI Azure](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="726e9-162">To learn more about selecting other images, see [Navigate and select Azure virtual machine images with Windows PowerShell and the Azure CLI](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
    > 
    > 

2. <span data-ttu-id="726e9-163">Pour appeler la fonction que vous avez ajoutée précédemment, ajoutez le code suivant sous l’instruction **if** à la fin du fichier .py :</span><span class="sxs-lookup"><span data-stu-id="726e9-163">To call the function that you previously added, add this code under the **if** statement at the end of the .py file:</span></span>

    ```python
    creation_result = create_vm(network_client, compute_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter to continue...')
    ```

## <a name="perform-management-tasks"></a><span data-ttu-id="726e9-164">Effectuer les tâches de gestion</span><span class="sxs-lookup"><span data-stu-id="726e9-164">Perform management tasks</span></span>

<span data-ttu-id="726e9-165">Pendant le cycle de vie d’une machine virtuelle, vous souhaiterez exécuter des tâches de gestion telles que le démarrage, l’arrêt ou la suppression d’une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="726e9-165">During the lifecycle of a virtual machine, you may want to run management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="726e9-166">En outre, vous souhaiterez peut-être créer du code pour automatiser les tâches répétitives ou complexes.</span><span class="sxs-lookup"><span data-stu-id="726e9-166">Additionally, you may want to create code to automate repetitive or complex tasks.</span></span>

### <a name="get-information-about-the-vm"></a><span data-ttu-id="726e9-167">Obtenir des informations sur la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="726e9-167">Get information about the VM</span></span>

1. <span data-ttu-id="726e9-168">Pour obtenir plus d’informations sur la machine virtuelle, ajoutez la fonction suivante après les variables dans le fichier .py :</span><span class="sxs-lookup"><span data-stu-id="726e9-168">To get information about the virtual machine, add this function after the variables in the .py file:</span></span>

    ```python
    def get_vm(compute_client):
        vm = compute_client.virtual_machines.get(GROUP_NAME, VM_NAME, expand='instanceView')
        print("hardwareProfile")
        print("   vmSize: ", vm.hardware_profile.vm_size)
        print("\nstorageProfile")
        print("  imageReference")
        print("    publisher: ", vm.storage_profile.image_reference.publisher)
        print("    offer: ", vm.storage_profile.image_reference.offer)
        print("    sku: ", vm.storage_profile.image_reference.sku)
        print("    version: ", vm.storage_profile.image_reference.version)
        print("  osDisk")
        print("    osType: ", vm.storage_profile.os_disk.os_type.value)
        print("    name: ", vm.storage_profile.os_disk.name)
        print("    createOption: ", vm.storage_profile.os_disk.create_option.value)
        print("    caching: ", vm.storage_profile.os_disk.caching.value)
        print("\nosProfile")
        print("  computerName: ", vm.os_profile.computer_name)
        print("  adminUsername: ", vm.os_profile.admin_username)
        print("  provisionVMAgent: {0}".format(vm.os_profile.windows_configuration.provision_vm_agent))
        print("  enableAutomaticUpdates: {0}".format(vm.os_profile.windows_configuration.enable_automatic_updates))
        print("\nnetworkProfile")
        for nic in vm.network_profile.network_interfaces:
            print("  networkInterface id: ", nic.id)
        print("\nvmAgent")
        print("  vmAgentVersion", vm.instance_view.vm_agent.vm_agent_version)
        print("    statuses")
        for stat in vm_result.instance_view.vm_agent.statuses:
            print("    code: ", stat.code)
            print("    displayStatus: ", stat.display_status)
            print("    message: ", stat.message)
            print("    time: ", stat.time)
        print("\ndisks");
        for disk in vm.instance_view.disks:
            print("  name: ", disk.name)
            print("  statuses")
            for stat in disk.statuses:
                print("    code: ", stat.code)
                print("    displayStatus: ", stat.display_status)
                print("    time: ", stat.time)
        print("\nVM general status")
        print("  provisioningStatus: ", vm.provisioning_state)
        print("  id: ", vm.id)
        print("  name: ", vm.name)
        print("  type: ", vm.type)
        print("  location: ", vm.location)
        print("\nVM instance status")
        for stat in vm.instance_view.statuses:
            print("  code: ", stat.code)
            print("  displayStatus: ", stat.display_status)
    ```
2. <span data-ttu-id="726e9-169">Pour appeler la fonction que vous avez ajoutée précédemment, ajoutez le code suivant sous l’instruction **if** à la fin du fichier .py :</span><span class="sxs-lookup"><span data-stu-id="726e9-169">To call the function that you previously added, add this code under the **if** statement at the end of the .py file:</span></span>

    ```python
    get_vm(compute_client)
    print("------------------------------------------------------")
    input('Press enter to continue...')
    ```

### <a name="stop-the-vm"></a><span data-ttu-id="726e9-170">Arrêtez la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="726e9-170">Stop the VM</span></span>

<span data-ttu-id="726e9-171">Vous pouvez arrêter une machine virtuelle et conserver tous ses paramètres, mais continuer à être facturé, ou arrêter une machine virtuelle et la libérer.</span><span class="sxs-lookup"><span data-stu-id="726e9-171">You can stop a virtual machine and keep all its settings, but continue to be charged for it, or you can stop a virtual machine and deallocate it.</span></span> <span data-ttu-id="726e9-172">Lorsqu’une machine virtuelle est libérée, toutes les ressources qui lui sont associées sont également libérées et la facturation de la machine virtuelle prend fin.</span><span class="sxs-lookup"><span data-stu-id="726e9-172">When a virtual machine is deallocated, all resources associated with it are also deallocated and billing ends for it.</span></span>

1. <span data-ttu-id="726e9-173">Pour arrêter la machine virtuelle sans la désallouer, ajoutez la fonction suivante après les variables dans le fichier .py :</span><span class="sxs-lookup"><span data-stu-id="726e9-173">To stop the virtual machine without deallocating it, add this function after the variables in the .py file:</span></span>

    ```python
    def stop_vm(compute_client):
        compute_client.virtual_machines.power_off(GROUP_NAME, VM_NAME)
    ```

    <span data-ttu-id="726e9-174">Si vous souhaitez désallouer la machine virtuelle, modifiez l’appel power_off à ce code :</span><span class="sxs-lookup"><span data-stu-id="726e9-174">If you want to deallocate the virtual machine, change the power_off call to this code:</span></span>

    ```python
    compute_client.virtual_machines.deallocate(GROUP_NAME, VM_NAME)
    ```

2. <span data-ttu-id="726e9-175">Pour appeler la fonction que vous avez ajoutée précédemment, ajoutez le code suivant sous l’instruction **if** à la fin du fichier .py :</span><span class="sxs-lookup"><span data-stu-id="726e9-175">To call the function that you previously added, add this code under the **if** statement at the end of the .py file:</span></span>

    ```python
    stop_vm(compute_client)
    input('Press enter to continue...')
    ```

### <a name="start-the-vm"></a><span data-ttu-id="726e9-176">Démarrer la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="726e9-176">Start the VM</span></span>

1. <span data-ttu-id="726e9-177">Pour démarrer la machine virtuelle, ajoutez la fonction suivante après les variables dans le fichier .py :</span><span class="sxs-lookup"><span data-stu-id="726e9-177">To start the virtual machine, add this function after the variables in the .py file:</span></span>

    ```python
    def start_vm(compute_client):
        compute_client.virtual_machines.start(GROUP_NAME, VM_NAME)
    ```

2. <span data-ttu-id="726e9-178">Pour appeler la fonction que vous avez ajoutée précédemment, ajoutez le code suivant sous l’instruction **if** à la fin du fichier .py :</span><span class="sxs-lookup"><span data-stu-id="726e9-178">To call the function that you previously added, add this code under the **if** statement at the end of the .py file:</span></span>

    ```python
    start_vm(compute_client)
    input('Press enter to continue...')
    ```

### <a name="resize-the-vm"></a><span data-ttu-id="726e9-179">Redimensionner la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="726e9-179">Resize the VM</span></span>

<span data-ttu-id="726e9-180">De nombreux aspects du déploiement doivent être pris en considération lors du choix d’une taille pour votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="726e9-180">Many aspects of deployment should be considered when deciding on a size for your virtual machine.</span></span> <span data-ttu-id="726e9-181">Pour plus d’informations, voir [Tailles des machines virtuelles](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="726e9-181">For more information, see [VM sizes](sizes.md).</span></span>

1. <span data-ttu-id="726e9-182">Pour modifier la taille de la machine virtuelle, ajoutez la fonction suivante après les variables dans le fichier .py :</span><span class="sxs-lookup"><span data-stu-id="726e9-182">To change the size of the virtual machine, add this function after the variables in the .py file:</span></span>

    ```python
    def update_vm(compute_client):
        vm = compute_client.virtual_machines.get(GROUP_NAME, VM_NAME)
        vm.hardware_profile.vm_size = 'Standard_DS3'
        update_result = compute_client.virtual_machines.create_or_update(
            GROUP_NAME, 
            VM_NAME, 
            vm
        )

    return update_result.result()
    ```

2. <span data-ttu-id="726e9-183">Pour appeler la fonction que vous avez ajoutée précédemment, ajoutez le code suivant sous l’instruction **if** à la fin du fichier .py :</span><span class="sxs-lookup"><span data-stu-id="726e9-183">To call the function that you previously added, add this code under the **if** statement at the end of the .py file:</span></span>

    ```python
    update_result = update_vm(compute_client)
    print("------------------------------------------------------")
    print(update_result)
    input('Press enter to continue...')
    ```

### <a name="add-a-data-disk-to-the-vm"></a><span data-ttu-id="726e9-184">Ajouter un disque de données à la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="726e9-184">Add a data disk to the VM</span></span>

<span data-ttu-id="726e9-185">Des machines virtuelles peuvent disposer d’un ou plusieurs [disques de données](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) stockés en tant que disques durs virtuels.</span><span class="sxs-lookup"><span data-stu-id="726e9-185">Virtual machines can have one or more [data disks](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) that are stored as VHDs.</span></span>

1. <span data-ttu-id="726e9-186">Pour ajouter un disque de données à la machine virtuelle, ajoutez la fonction suivante après les variables dans le fichier .py :</span><span class="sxs-lookup"><span data-stu-id="726e9-186">To add a data disk to the virtual machine, add this function after the variables in the .py file:</span></span> 

    ```python
    def add_datadisk(compute_client):
        disk_creation = compute_client.disks.create_or_update(
            GROUP_NAME,
            'myDataDisk1',
            {
                'location': LOCATION,
                'disk_size_gb': 1,
                'creation_data': {
                    'create_option': DiskCreateOption.empty
                }
            }
        )
        data_disk = disk_creation.result()
        vm = compute_client.virtual_machines.get(GROUP_NAME, VM_NAME)
        add_result = vm.storage_profile.data_disks.append({
            'lun': 1,
            'name': 'myDataDisk1',
            'create_option': DiskCreateOption.attach,
            'managed_disk': {
                'id': data_disk.id
            }
        })
        add_result = compute_client.virtual_machines.create_or_update(
            GROUP_NAME,
            VM_NAME,
            vm)

        return add_result.result()
    ```

2. <span data-ttu-id="726e9-187">Pour appeler la fonction que vous avez ajoutée précédemment, ajoutez le code suivant sous l’instruction **if** à la fin du fichier .py :</span><span class="sxs-lookup"><span data-stu-id="726e9-187">To call the function that you previously added, add this code under the **if** statement at the end of the .py file:</span></span>

    ```python
    add_result = add_datadisk(compute_client)
    print("------------------------------------------------------")
    print(add_result)
    input('Press enter to continue...')
    ```

## <a name="delete-resources"></a><span data-ttu-id="726e9-188">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="726e9-188">Delete resources</span></span>

<span data-ttu-id="726e9-189">Étant donné que les ressources utilisées dans Microsoft Azure vous sont facturées, il est toujours conseillé de supprimer les ressources qui ne sont plus nécessaires.</span><span class="sxs-lookup"><span data-stu-id="726e9-189">Because you are charged for resources used in Azure, it's always a good practice to delete resources that are no longer needed.</span></span> <span data-ttu-id="726e9-190">Si vous souhaitez supprimer les machines virtuelles et l’ensemble des ressources de prise en charge, il vous suffit de supprimer le groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="726e9-190">If you want to delete the virtual machines and all the supporting resources, all you have to do is delete the resource group.</span></span>

1. <span data-ttu-id="726e9-191">Pour supprimer le groupe de ressources et toutes les ressources, ajoutez la fonction suivante après les variables dans le fichier .py :</span><span class="sxs-lookup"><span data-stu-id="726e9-191">To delete the resource group and all resources, add this function after the variables in the .py file:</span></span>
   
    ```python
    def delete_resources(resource_group_client):
        resource_group_client.resource_groups.delete(GROUP_NAME)
    ```

2. <span data-ttu-id="726e9-192">Pour appeler la fonction que vous avez ajoutée précédemment, ajoutez le code suivant sous l’instruction **if** à la fin du fichier .py :</span><span class="sxs-lookup"><span data-stu-id="726e9-192">To call the function that you previously added, add this code under the **if** statement at the end of the .py file:</span></span>
   
    ```python
    delete_resources(resource_group_client)
    ```

3. <span data-ttu-id="726e9-193">Enregistrez *monProjetPython.py*.</span><span class="sxs-lookup"><span data-stu-id="726e9-193">Save *myPythonProject.py*.</span></span>

## <a name="run-the-application"></a><span data-ttu-id="726e9-194">Exécuter l'application</span><span class="sxs-lookup"><span data-stu-id="726e9-194">Run the application</span></span>

1. <span data-ttu-id="726e9-195">Pour exécuter l’application console, cliquez sur **Démarrer** dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="726e9-195">To run the console application, click **Start** in Visual Studio.</span></span>

2. <span data-ttu-id="726e9-196">Appuyez sur **Entrée** après que l’état de chaque ressource a été retourné.</span><span class="sxs-lookup"><span data-stu-id="726e9-196">Press **Enter** after the status of each resource is returned.</span></span> <span data-ttu-id="726e9-197">Dans les informations d’état, vous devriez voir l’état d’approvisionnement **Réussi**.</span><span class="sxs-lookup"><span data-stu-id="726e9-197">In the status information, you should see a **Succeeded** provisioning state.</span></span> <span data-ttu-id="726e9-198">Une fois la machine virtuelle créée, vous pouvez supprimer toutes les ressources que vous avez créées.</span><span class="sxs-lookup"><span data-stu-id="726e9-198">After the virtual machine is created, you have the opportunity to delete all the resources that you create.</span></span> <span data-ttu-id="726e9-199">Avant d’appuyer sur **Entrée** pour démarrer la suppression des ressources, prenez quelques minutes pour vérifier leur création dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="726e9-199">Before you press **Enter** to start deleting resources, you could take a few minutes to verify their creation in the Azure portal.</span></span> <span data-ttu-id="726e9-200">Si le portail Azure est ouvert, il se peut que vous deviez actualiser le panneau pour afficher de nouvelles ressources.</span><span class="sxs-lookup"><span data-stu-id="726e9-200">If you have the Azure portal open, you might have to refresh the blade to see new resources.</span></span>  

    <span data-ttu-id="726e9-201">L’exécution complète de cette application console devrait durer cinq minutes environ.</span><span class="sxs-lookup"><span data-stu-id="726e9-201">It should take about five minutes for this console application to run completely from start to finish.</span></span> <span data-ttu-id="726e9-202">Quelques minutes peuvent s’écouler après la fin de l’exécution de l’application avant que toutes les ressources et le groupe de ressources soient supprimés.</span><span class="sxs-lookup"><span data-stu-id="726e9-202">It may take several minutes after the application has finished before all the resources and the resource group are deleted.</span></span>


## <a name="next-steps"></a><span data-ttu-id="726e9-203">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="726e9-203">Next steps</span></span>

- <span data-ttu-id="726e9-204">Si vous rencontrez des problèmes de déploiement, consultez [Résolution des problèmes liés aux déploiements de groupes de ressources avec le portail Azure](../../resource-manager-troubleshoot-deployments-portal.md).</span><span class="sxs-lookup"><span data-stu-id="726e9-204">If there were issues with the deployment, a next step would be to look at [Troubleshooting resource group deployments with Azure portal](../../resource-manager-troubleshoot-deployments-portal.md)</span></span>
- <span data-ttu-id="726e9-205">En savoir plus sur la [Bibliothèque Python Azure](https://docs.microsoft.com/python/api/overview/azure/?view=azure-python)</span><span class="sxs-lookup"><span data-stu-id="726e9-205">Learn more about the [Azure Python Library](https://docs.microsoft.com/python/api/overview/azure/?view=azure-python)</span></span>

