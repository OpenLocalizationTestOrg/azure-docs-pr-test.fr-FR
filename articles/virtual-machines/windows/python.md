---
title: "aaaCreate et de gérer un ordinateur virtuel Windows Azure à l’aide de Python | Documents Microsoft"
description: "En savoir plus toouse Python toocreate et gérer un ordinateur virtuel Windows Azure."
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
ms.openlocfilehash: c5553e4e7361e6b9a7183cd935be382f967160cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-windows-vms-in-azure-using-python"></a>Créer et gérer des machines virtuelles Windows dans Azure à l’aide de Python

Une [Machine virtuelle Azure](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) a besoin de plusieurs ressources de prise en charge Azure. Cet article décrit la création, la gestion et la suppression de ressources de machine virtuelle à l’aide de Python. Vous allez apprendre à effectuer les actions suivantes :

> [!div class="checklist"]
> * Créer un projet Visual Studio
> * Installer des packages
> * Créer des informations d’identification
> * Créer des ressources
> * Effectuer les tâches de gestion
> * Supprimer des ressources
> * Exécutez l’application hello

Il prend environ 20 minutes toodo ces étapes.

## <a name="create-a-visual-studio-project"></a>Créer un projet Visual Studio

1. Si vous ne l’avez pas déjà fait, installez [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio). Sélectionnez **développement de Python** sur hello page de charges de travail, puis cliquez sur **installer**. Bonjour résumé, vous pouvez voir que **Python 3 64 bits (3.6.0)** est automatiquement sélectionné pour vous. Si vous avez déjà installé Visual Studio, vous pouvez ajouter à l’aide de Visual Studio Lanceur de hello la charge de travail hello Python.
2. Après avoir installé et démarré Visual Studio, cliquez sur **Fichier** > **Nouveau** > **Projet**.
3. Cliquez sur **modèles** > **Python** > **Application Python**, entrez *myPythonProject* pour le nom de hello hello projet de, sélectionnez l’emplacement hello du projet de hello, puis cliquez sur **OK**.

## <a name="install-packages"></a>Installer des packages

1. Dans l’Explorateur de solutions, sous *monProjetPython*, cliquez avec le bouton droit sur **Environnements Python**, puis sélectionnez **Ajouter un environnement virtuel**.
2. Sur l’écran d’ajouter l’environnement virtuel hello, acceptez le nom par défaut hello *env*, assurez-vous que *Python 3.6 (64 bits)* est sélectionné pour l’interpréteur de base hello, puis cliquez sur **créer**.
3. Avec le bouton hello *env* environnement que vous avez créé, cliquez sur **Package d’installation de Python**, entrez *azure* dans hello de zone de recherche, puis appuyez sur ENTRÉE.

Vous devez voir dans les fenêtres de sortie hello que hello azure ont été correctement installés. 

## <a name="create-credentials"></a>Créer des informations d’identification

Avant de commencer cette étape, assurez-vous que vous disposez d’un [principal du service Active Directory](../../azure-resource-manager/resource-group-create-service-principal-portal.md). Vous devez également enregistrer les ID de l’application hello, clé d’authentification hello et ID de client hello dont vous avez besoin dans une étape ultérieure.

1. Ouvrez *myPythonProject.py* fichier qui a été créé, puis ajoutez ce code tooenable toorun de votre application :

    ```python
    if __name__ == "__main__":
    ```

2. le code hello tooimport nécessaires, ajoutez ces instructions toohello en haut de fichier de .py hello :

    ```python
    from azure.common.credentials import ServicePrincipalCredentials
    from azure.mgmt.resource import ResourceManagementClient
    from azure.mgmt.compute import ComputeManagementClient
    from azure.mgmt.network import NetworkManagementClient
    from azure.mgmt.compute.models import DiskCreateOption
    ```

3. Ensuite dans le fichier de .py hello, ajoutez variables après que les instructions d’importation hello toospecify des valeurs communes utilisées dans hello code :
   
    ```
    SUBSCRIPTION_ID = 'subscription-id'
    GROUP_NAME = 'myResourceGroup'
    LOCATION = 'westus'
    VM_NAME = 'myVM'
    ```

    Remplacez **subscription-id** par votre identificateur d’abonnement.

4. informations d’identification de toocreate hello Active Directory que vous avez besoin de demandes de toomake, ajoutez cette fonction après variables hello dans le fichier de .py hello :

    ```python
    def get_credentials():
        credentials = ServicePrincipalCredentials(
            client_id = 'application-id',
            secret = 'authentication-key',
            tenant = 'tenant-id'
        )

        return credentials
    ```

    Remplacez **id d’application**, **clé d’authentification**, et **id de client** avec les valeurs hello que vous avez collectées précédemment lorsque vous avez créé votre répertoire Azure Active Directory. principal du service.

5. fonction hello toocall que vous avez ajouté précédemment, ajoutez ce code sous hello **si** instruction à fin hello du fichier de .py hello :

    ```python
    credentials = get_credentials()
    ```

## <a name="create-resources"></a>Créer des ressources
 
### <a name="initialize-management-clients"></a>Initialiser des clients de gestion

Clients de gestion sont nécessaire toocreate et gérer des ressources à l’aide de hello Kit de développement logiciel Python dans Azure. clients de gestion toocreate hello, ajoutez ce code sous hello **si** instruction à puis fin du fichier de .py hello :

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

### <a name="create-hello-vm-and-supporting-resources"></a>Créer hello machine virtuelle et de ressources de support

Toutes les ressources doivent être contenues dans un [groupe de ressources](../../azure-resource-manager/resource-group-overview.md).

1. toocreate un groupe de ressources, ajoutez cette fonction après variables hello dans le fichier de .py hello :

    ```python
    def create_resource_group(resource_group_client):
        resource_group_params = { 'location':LOCATION }
        resource_group_result = resource_group_client.resource_groups.create_or_update(
            GROUP_NAME, 
            resource_group_params
        )
    ```

2. fonction hello toocall que vous avez ajouté précédemment, ajoutez ce code sous hello **si** instruction à fin hello du fichier de .py hello :

    ```python
    create_resource_group(resource_group_client)
    input('Resource group created. Press enter toocontinue...')
    ```

[Haute disponibilité](tutorial-availability-sets.md) facilitent pour vous toomaintain hello virtuels utilisés par votre application.

1. toocreate une disponibilité définie, ajoutez cette fonction après variables hello dans le fichier de .py hello :
   
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

2. fonction hello toocall que vous avez ajouté précédemment, ajoutez ce code sous hello **si** instruction à fin hello du fichier de .py hello :

    ```python
    create_availability_set(compute_client)
    print("------------------------------------------------------")
    input('Availability set created. Press enter toocontinue...')
    ```

A [adresse IP publique](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) est toocommunicate nécessaire avec l’ordinateur virtuel de hello.

1. toocreate une adresse IP publique pour l’ordinateur virtuel de hello, ajoutez cette fonction après variables hello dans le fichier de .py hello :

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

2. fonction hello toocall que vous avez ajouté précédemment, ajoutez ce code sous hello **si** instruction à fin hello du fichier de .py hello :

    ```python
    creation_result = create_public_ip_address(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

Une machine virtuelle doit être incluse dans un sous-réseau d’un [réseau virtuel](../../virtual-network/virtual-networks-overview.md).

1. toocreate un réseau virtuel, ajoutez cette fonction après variables hello dans le fichier de .py hello :

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

2. fonction hello toocall que vous avez ajouté précédemment, ajoutez ce code sous hello **si** instruction à fin hello du fichier de .py hello :
   
    ```python
    creation_result = create_vnet(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

3. tooadd un réseau virtuel toohello de sous-réseau, ajoutez cette fonction après variables hello dans le fichier de .py hello :
    
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
        
4. fonction hello toocall que vous avez ajouté précédemment, ajoutez ce code sous hello **si** instruction à fin hello du fichier de .py hello :
   
    ```python
    creation_result = create_subnet(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

Un ordinateur virtuel doit un toocommunicate d’interface réseau sur le réseau virtuel de hello.

1. toocreate une interface réseau, ajoutez cette fonction après variables hello dans le fichier de .py hello :

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

2. fonction hello toocall que vous avez ajouté précédemment, ajoutez ce code sous hello **si** instruction à fin hello du fichier de .py hello :

    ```python
    creation_result = create_nic(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

Maintenant que vous avez créé hello toutes les ressources de support, vous pouvez créer un ordinateur virtuel.

1. toocreate hello de machine virtuelle, ajoutez cette fonction après variables hello dans le fichier de .py hello :
   
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
    > Ce didacticiel crée une machine virtuelle exécutant une version du système d’exploitation de serveur Windows hello. toolearn plus sur la sélection d’autres images, consultez [naviguer et sélectionnez les images de machine virtuelle Azure avec Windows PowerShell et hello CLI d’Azure](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
    > 
    > 

2. fonction hello toocall que vous avez ajouté précédemment, ajoutez ce code sous hello **si** instruction à fin hello du fichier de .py hello :

    ```python
    creation_result = create_vm(network_client, compute_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

## <a name="perform-management-tasks"></a>Effectuer les tâches de gestion

Au cours de hello du cycle de vie d’un ordinateur virtuel, vous souhaiterez toorun des tâches de gestion telles que le démarrage, arrêt ou suppression d’une machine virtuelle. En outre, vous souhaiterez toocreate tooautomate répétitives ou complexes des tâches de code.

### <a name="get-information-about-hello-vm"></a>Obtenir des informations sur la machine virtuelle de hello

1. tooget plus d’informations sur la machine virtuelle de hello, ajoutez cette fonction après variables hello dans le fichier de .py hello :

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
2. fonction hello toocall que vous avez ajouté précédemment, ajoutez ce code sous hello **si** instruction à fin hello du fichier de .py hello :

    ```python
    get_vm(compute_client)
    print("------------------------------------------------------")
    input('Press enter toocontinue...')
    ```

### <a name="stop-hello-vm"></a>Arrêter hello machine virtuelle

Vous pouvez arrêter une machine virtuelle et conserver tous ses paramètres, mais continuer toobe facturé pour celui-ci, ou vous pouvez arrêter une machine virtuelle et désallouer. Lorsqu’une machine virtuelle est libérée, toutes les ressources qui lui sont associées sont également libérées et la facturation de la machine virtuelle prend fin.

1. toostop hello virtual machine sans le désallouer, ajoutez cette fonction après variables hello dans le fichier de .py hello :

    ```python
    def stop_vm(compute_client):
        compute_client.virtual_machines.power_off(GROUP_NAME, VM_NAME)
    ```

    Si vous voulez toodeallocate hello virtual machine, modifier le code de toothis hello power_off appel :

    ```python
    compute_client.virtual_machines.deallocate(GROUP_NAME, VM_NAME)
    ```

2. fonction hello toocall que vous avez ajouté précédemment, ajoutez ce code sous hello **si** instruction à fin hello du fichier de .py hello :

    ```python
    stop_vm(compute_client)
    input('Press enter toocontinue...')
    ```

### <a name="start-hello-vm"></a>Démarrer hello machine virtuelle

1. toostart hello de machine virtuelle, ajoutez cette fonction après variables hello dans le fichier de .py hello :

    ```python
    def start_vm(compute_client):
        compute_client.virtual_machines.start(GROUP_NAME, VM_NAME)
    ```

2. fonction hello toocall que vous avez ajouté précédemment, ajoutez ce code sous hello **si** instruction à fin hello du fichier de .py hello :

    ```python
    start_vm(compute_client)
    input('Press enter toocontinue...')
    ```

### <a name="resize-hello-vm"></a>Redimensionner hello machine virtuelle

De nombreux aspects du déploiement doivent être pris en considération lors du choix d’une taille pour votre machine virtuelle. Pour plus d’informations, voir [Tailles des machines virtuelles](sizes.md).

1. taille de hello toochange de machine virtuelle de hello, ajoutez cette fonction après variables hello dans le fichier de .py hello :

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

2. fonction hello toocall que vous avez ajouté précédemment, ajoutez ce code sous hello **si** instruction à fin hello du fichier de .py hello :

    ```python
    update_result = update_vm(compute_client)
    print("------------------------------------------------------")
    print(update_result)
    input('Press enter toocontinue...')
    ```

### <a name="add-a-data-disk-toohello-vm"></a>Ajouter un toohello de disque de données machine virtuelle

Des machines virtuelles peuvent disposer d’un ou plusieurs [disques de données](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) stockés en tant que disques durs virtuels.

1. tooadd un ordinateur virtuel des toohello du disque de données, ajoutez cette fonction après variables hello dans le fichier de .py hello : 

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

2. fonction hello toocall que vous avez ajouté précédemment, ajoutez ce code sous hello **si** instruction à fin hello du fichier de .py hello :

    ```python
    add_result = add_datadisk(compute_client)
    print("------------------------------------------------------")
    print(add_result)
    input('Press enter toocontinue...')
    ```

## <a name="delete-resources"></a>Supprimer des ressources

Vous êtes facturé pour les ressources utilisées dans Azure, il est toujours ressource toodelete bonnes pratiques qui n’est plus nécessaires. Si vous souhaitez toodelete hello virtual machines et hello toutes les ressources de support, toutes les toodo est hello supprimer le groupe de ressources.

1. groupe de ressources toodelete hello et toutes les ressources, ajoutez cette fonction après variables hello dans le fichier de .py hello :
   
    ```python
    def delete_resources(resource_group_client):
        resource_group_client.resource_groups.delete(GROUP_NAME)
    ```

2. fonction hello toocall que vous avez ajouté précédemment, ajoutez ce code sous hello **si** instruction à fin hello du fichier de .py hello :
   
    ```python
    delete_resources(resource_group_client)
    ```

3. Enregistrez *monProjetPython.py*.

## <a name="run-hello-application"></a>Exécutez l’application hello

1. application de console toorun hello, cliquez sur **Démarrer** dans Visual Studio.

2. Appuyez sur **entrée** après état hello de chaque ressource est retourné. Dans les informations d’état hello, vous devez voir un **Succeeded** état d’approvisionnement. Après la création de la machine virtuelle de hello, vous avez hello opportunité toodelete toutes les ressources hello que vous créez. Avant d’appuyer sur **entrée** toostart suppression des ressources, vous pouvez prendre quelques minutes tooverify leur création Bonjour portail Azure. Si vous avez hello ouvrir portail Azure, vous pouvez avoir des nouvelles ressources toorefresh hello panneau toosee.  

    Il doit prendre environ cinq minutes pour que cette toorun d’application console complètement à partir de toofinish de début. Il peut prendre quelques minutes après l’application hello est terminée avant de toutes les ressources hello et groupe de ressources hello sont supprimés.


## <a name="next-steps"></a>Étapes suivantes

- S’il existe des problèmes de déploiement de hello, une étape suivante consisterait toolook à [dépannage des déploiements de groupe de ressources avec le portail Azure](../../resource-manager-troubleshoot-deployments-portal.md)
- En savoir plus sur hello [Azure Python de la bibliothèque](https://docs.microsoft.com/python/api/overview/azure/?view=azure-python)

