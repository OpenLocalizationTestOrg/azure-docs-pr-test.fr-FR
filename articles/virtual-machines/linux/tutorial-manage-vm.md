---
title: "aaaCreate et gérer des ordinateurs virtuels Linux avec hello CLI d’Azure | Documents Microsoft"
description: "Didacticiel : créer et gérer des ordinateurs virtuels Linux avec hello CLI d’Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 05f7c1cf860f809bc13f110778d3bddd619ac6f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-linux-vms-with-hello-azure-cli"></a>Créer et gérer des ordinateurs virtuels Linux avec hello CLI d’Azure

Les machines virtuelles fournissent un environnement informatique entièrement configurable et flexible. Ce didacticiel traite d’aspects de base du déploiement de machines virtuelles Azure, tels que la sélection d’une taille de machine virtuelle, la sélection d’une image de machine virtuelle et le déploiement d’une machine virtuelle. Vous allez apprendre à effectuer les actions suivantes :

> [!div class="checklist"]
> * Créer et connecter tooa machine virtuelle
> * Sélectionner et utiliser des images de machine virtuelle
> * Afficher et utiliser des tailles de machine virtuelle spécifiques
> * Redimensionner une machine virtuelle
> * Consulter et comprendre l’état d’une machine virtuelle


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Si vous choisissez tooinstall et que vous utilisez hello CLI localement, ce didacticiel nécessite que vous exécutez hello CLI d’Azure version 2.0.4 ou version ultérieure. Exécutez `az --version` version de hello toofind. Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="create-resource-group"></a>Créer un groupe de ressources

Créer un groupe de ressources avec hello [création de groupe de az](https://docs.microsoft.com/cli/azure/group#create) commande. 

Un groupe de ressources Azure est un conteneur logique dans lequel les ressources Azure sont déployées et gérées. Un groupe de ressources doit être créé avant les machines virtuelles. Dans cet exemple, un groupe de ressources nommé *myResourceGroupVM* est créé dans hello *eastus* région. 

```azurecli-interactive 
az group create --name myResourceGroupVM --location eastus
```

groupe de ressources Hello est spécifié lors de la création ou la modification d’une machine virtuelle, ce qui peut être vu dans ce didacticiel.

## <a name="create-virtual-machine"></a>Create virtual machine

Créer une machine virtuelle avec hello [az vm créer](https://docs.microsoft.com/cli/azure/vm#create) commande. 

Lorsque vous créez une machine virtuelle, plusieurs options sont disponibles, comme l’image de système d’exploitation, les informations d’identification d’administration ou le dimensionnement des disques. Dans cet exemple, une machine virtuelle nommée *myVM* est créée et exécute Ubuntu Server. 

```azurecli-interactive 
az vm create --resource-group myResourceGroupVM --name myVM --image UbuntuLTS --generate-ssh-keys
```

Une fois hello que machine virtuelle a été créé, hello CLI d’Azure génère plus d’informations sur la machine virtuelle de hello. Prenez note de hello `publicIpAddress`, cette adresse peut être utilisé tooaccess hello virtuels... 

```azurecli-interactive 
{
  "fqdns": "",
  "id": "/subscriptions/d5b9d4b7-6fc1-0000-0000-000000000000/resourceGroups/myResourceGroupVM/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "52.174.34.95",
  "resourceGroup": "myResourceGroupVM"
}
```

## <a name="connect-toovm"></a>Se connecter tooVM

Vous pouvez maintenant vous connecter toohello machine virtuelle à l’aide de SSH. Remplacez l’exemple d’adresse IP hello avec hello `publicIpAddress` indiqué à l’étape précédente de hello.

```bash
ssh 52.174.34.95
```

Une fois par hello VM, fermer la session SSH de hello. 

```bash
exit
```

## <a name="understand-vm-images"></a>Comprendre les images de machine virtuelle

Hello Azure marketplace inclut de nombreuses images qui peuvent être des machines virtuelles de toocreate utilisé. Dans les étapes précédentes hello, un ordinateur virtuel a été créé à l’aide d’une image d’Ubuntu. Dans cette étape, hello que CLI d’Azure est marketplace de hello toosearch utilisé pour une image de CentOS, qui est ensuite utilisé toodeploy une deuxième machine virtuelle.  

toosee une liste de hello couramment utilisés images, utilisez hello [liste d’images de machine virtuelle de az](/cli/azure/vm/image#list) commande.

```azurecli-interactive 
az vm image list --output table
```

sortie de la commande Hello renvoie des images de machine virtuelle plus populaires hello sur Azure.

```bash
Offer          Publisher               Sku                 Urn                                                             UrnAlias             Version
-------------  ----------------------  ------------------  --------------------------------------------------------------  -------------------  ---------
WindowsServer  MicrosoftWindowsServer  2016-Datacenter     MicrosoftWindowsServer:WindowsServer:2016-Datacenter:latest     Win2016Datacenter    latest
WindowsServer  MicrosoftWindowsServer  2012-R2-Datacenter  MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest  Win2012R2Datacenter  latest
WindowsServer  MicrosoftWindowsServer  2008-R2-SP1         MicrosoftWindowsServer:WindowsServer:2008-R2-SP1:latest         Win2008R2SP1         latest
WindowsServer  MicrosoftWindowsServer  2012-Datacenter     MicrosoftWindowsServer:WindowsServer:2012-Datacenter:latest     Win2012Datacenter    latest
UbuntuServer   Canonical               16.04-LTS           Canonical:UbuntuServer:16.04-LTS:latest                         UbuntuLTS            latest
CentOS         OpenLogic               7.3                 OpenLogic:CentOS:7.3:latest                                     CentOS               latest
openSUSE-Leap  SUSE                    42.2                SUSE:openSUSE-Leap:42.2:latest                                  openSUSE-Leap        latest
RHEL           RedHat                  7.3                 RedHat:RHEL:7.3:latest                                          RHEL                 latest
SLES           SUSE                    12-SP2              SUSE:SLES:12-SP2:latest                                         SLES                 latest
Debian         credativ                8                   credativ:Debian:8:latest                                        Debian               latest
CoreOS         CoreOS                  Stable              CoreOS:CoreOS:Stable:latest                                     CoreOS               latest
```

Une liste complète peut être affichée en ajoutant hello `--all` argument. liste d’images Hello peut également être filtré par `--publisher` ou `–-offer`. Dans cet exemple, la liste de hello est filtré pour toutes les images avec une offre qui correspond à *CentOS*. 

```azurecli-interactive 
az vm image list --offer CentOS --all --output table
```

Résultat partiel :

```azurecli-interactive 
Offer             Publisher         Sku   Urn                                     Version
----------------  ----------------  ----  --------------------------------------  -----------
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.201501         6.5.201501
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.201503         6.5.201503
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.201506         6.5.201506
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.20150904       6.5.20150904
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.20160309       6.5.20160309
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.20170207       6.5.20170207
```

toodeploy une machine virtuelle à l’aide d’une image spécifique, prenez note de la valeur de hello Bonjour *Urn* colonne. Lorsque vous spécifiez l’image de hello, numéro de version d’image hello peut être remplacé par « dernier », qui sélectionne la version la plus récente de la distribution de hello hello. Dans cet exemple, hello `--image` argument est la version la plus récente hello toospecify utilisé d’une image CentOS 6.5.  

```azurecli-interactive 
az vm create --resource-group myResourceGroupVM --name myVM2 --image OpenLogic:CentOS:6.5:latest --generate-ssh-keys
```

## <a name="understand-vm-sizes"></a>Comprendre les tailles de machine virtuelle

Une taille de machine virtuelle détermine hello des ressources de calcul tels que le processeur et mémoire GPU apportées virtuels toohello disponibles. Machines virtuelles doivent toobe la taille appropriée pour la charge de travail hello attendu. Si la charge de travail augmente, une machine virtuelle existante peut être redimensionnée.

### <a name="vm-sizes"></a>Tailles de machine virtuelle

Hello tableau suivant catégorise les tailles en cas d’usage.  

| Type                     | Tailles           |    Description       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| [Usage général](sizes-general.md)         |Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7| Ratio processeur/mémoire équilibré. La solution idéale pour le développement / test et des solutions d’applications et des données toomedium petit.  |
| [Optimisé pour le calcul](sizes-compute.md)   | Fs, F             | Ratio processeur/mémoire élevé. Convient pour les applications au trafic moyen, les appliances réseau et les processus de traitement par lots.        |
| [Mémoire optimisée](../virtual-machines-windows-sizes-memory.md)    | Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D   | Ratio mémoire/cœur élevé. Idéal pour les bases de données relationnelles, les caches toolarge moyenne et en mémoire analytique.                 |
| [Optimisé pour le stockage](../virtual-machines-windows-sizes-storage.md)      | Ls                | Débit de disque et E/S élevés. Idéale pour les bases de données NoSQL, SQL et Big Data.                                                         |
| [GPU](sizes-gpu.md)          | NV, NC            | Machines virtuelles spécialisées conçues pour les opérations graphiques lourdes et la retouche vidéo.       |
| [Hautes performances](sizes-hpc.md) | H, A8-11          | Nos machines virtuelles dotées des processeurs les plus puissants avec interfaces réseau haut débit en option (RDMA). 


### <a name="find-available-vm-sizes"></a>Rechercher les tailles de machines virtuelles disponibles

toosee une liste des ordinateurs virtuels des tailles disponibles dans une région particulière, utilisez hello [liste-tailles de machine virtuelle az](/cli/azure/vm#list-sizes) commande. 

```azurecli-interactive 
az vm list-sizes --location eastus --output table
```

Résultat partiel :

```azurecli-interactive 
  MaxDataDiskCount    MemoryInMb  Name                      NumberOfCores    OsDiskSizeInMb    ResourceDiskSizeInMb
------------------  ------------  ----------------------  ---------------  ----------------  ----------------------
                 2          3584  Standard_DS1                          1           1047552                    7168
                 4          7168  Standard_DS2                          2           1047552                   14336
                 8         14336  Standard_DS3                          4           1047552                   28672
                16         28672  Standard_DS4                          8           1047552                   57344
                 4         14336  Standard_DS11                         2           1047552                   28672
                 8         28672  Standard_DS12                         4           1047552                   57344
                16         57344  Standard_DS13                         8           1047552                  114688
                32        114688  Standard_DS14                        16           1047552                  229376
                 1           768  Standard_A0                           1           1047552                   20480
                 2          1792  Standard_A1                           1           1047552                   71680
                 4          3584  Standard_A2                           2           1047552                  138240
                 8          7168  Standard_A3                           4           1047552                  291840
                 4         14336  Standard_A5                           2           1047552                  138240
                16         14336  Standard_A4                           8           1047552                  619520
                 8         28672  Standard_A6                           4           1047552                  291840
                16         57344  Standard_A7                           8           1047552                  619520
```

### <a name="create-vm-with-specific-size"></a>Créer une machine virtuelle d’une taille spécifique

Dans le précédent exemple de la création de machine virtuelle hello, une taille n’est spécifié, ce qui aboutit à une taille par défaut. Une taille de machine virtuelle peut être sélectionnée au moment de la création à l’aide [az vm créer](/cli/azure/vm#create) et hello `--size` argument. 

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupVM \
    --name myVM3 \
    --image UbuntuLTS \
    --size Standard_F4s \
    --generate-ssh-keys
```

### <a name="resize-a-vm"></a>Redimensionner une machine virtuelle

Après avoir déployé une machine virtuelle, il peut être redimensionné tooincrease ou diminuer l’allocation de ressources.

Avant de redimensionner une machine virtuelle, vérifiez si hello taille souhaitée est disponible sur le cluster Azure hello actuel. Hello [az vm-vm-resize-options de la liste](/cli/azure/vm#list-vm-resize-options) renvoie hello liste des tailles de commande. 

```azurecli-interactive 
az vm list-vm-resize-options --resource-group myResourceGroupVM --name myVM --query [].name
```
Si hello souhaité de taille n’est disponible, hello machine virtuelle peut être redimensionnée à partir d’un état sous tension, mais il est redémarré au cours de l’opération de hello. Hello d’utilisation [az vm redimensionner]( /cli/azure/vm#resize) commande tooperform hello redimensionnement.

```azurecli-interactive 
az vm resize --resource-group myResourceGroupVM --name myVM --size Standard_DS4_v2
```

Si vous le souhaitez hello taille n’est pas sur le cluster actuel hello, hello VM besoins toobe libérée avant que l’opération de redimensionnement hello peut se produire. Hello d’utilisation [az vm désallouer]( /cli/azure/vm#deallocate) commande toostop et désallouer hello machine virtuelle. Notez que, quand hello VM est sous tension précédent, toutes les données sur le disque temporaire de hello peuvent être supprimées. adresse IP publique de Hello change également, sauf si une adresse IP statique est utilisée. 

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupVM --name myVM
```

Une fois libérées, hello redimensionnement peut se produire. 

```azurecli-interactive 
az vm resize --resource-group myResourceGroupVM --name myVM --size Standard_GS1
```

Une fois hello redimensionner, hello machine virtuelle peut être démarré.

```azurecli-interactive 
az vm start --resource-group myResourceGroupVM --name myVM
```

## <a name="vm-power-states"></a>États d’alimentation de la machine virtuelle

Une machine virtuelle Azure peut présenter différents états d’alimentation. Cet état représente état actuel de hello Hello machine virtuelle à partir du point de vue hello de hello hyperviseur. 

### <a name="power-states"></a>États d’alimentation

| État d’alimentation | Description
|----|----|
| Starting | Indique l’ordinateur virtuel de hello est en cours de démarrage. |
| Exécution | Indique que l’ordinateur virtuel hello est en cours d’exécution. |
| En cours d’arrêt | Indique que l’ordinateur virtuel hello est en cours d’arrêt. | 
| Arrêté | Indique que l’ordinateur virtuel hello est arrêté. Machines virtuelles dans un état de hello arrêté peut toujours occasionner des frais de calcul.  |
| Libération | Indique que l’ordinateur virtuel hello est désalloué. |
| Libéré | Indique que l’ordinateur virtuel hello est supprimé de l’hyperviseur de hello mais restent disponibles dans le plan de contrôle hello. Machines virtuelles dans hello désallouée état n’entraînent aucun frais de calcul. |
| - | Indique que l’état de l’alimentation de l’ordinateur virtuel de hello hello est inconnu. |

### <a name="find-power-state"></a>Rechercher un état d’alimentation

état de hello tooretrieve d’un ordinateur virtuel, utilisez hello [az vm obtenir de l’instance](/cli/azure/vm#get-instance-view) commande. Être vraiment toospecify un nom valide pour un ordinateur virtuel et le groupe de ressources. 

```azurecli-interactive 
az vm get-instance-view \
    --name myVM \
    --resource-group myResourceGroupVM \
    --query instanceView.statuses[1] --output table
```

Output:

```azurecli-interactive 
ode                DisplayStatus    Level
------------------  ---------------  -------
PowerState/running  VM running       Info
```

## <a name="management-tasks"></a>Tâches de gestion

Au cours de hello cycle de vie d’un ordinateur virtuel, vous souhaiterez toorun des tâches de gestion telles que le démarrage, arrêt ou suppression d’une machine virtuelle. En outre, vous souhaiterez toocreate scripts tooautomate répétitives ou complexes des tâches. À l’aide de hello CLI d’Azure, plusieurs tâches de gestion courantes peuvent être exécutées à partir de la ligne de commande hello ou dans des scripts. 

### <a name="get-ip-address"></a>Obtenir l’adresse IP

Cette commande renvoie hello privés et publics adresses d’un ordinateur virtuel.  

```azurecli-interactive 
az vm list-ip-addresses --resource-group myResourceGroupVM --name myVM --output table
```

### <a name="stop-virtual-machine"></a>Arrêt d’une machine virtuelle

```azurecli-interactive 
az vm stop --resource-group myResourceGroupVM --name myVM
```

### <a name="start-virtual-machine"></a>Démarrage d’une machine virtuelle

```azurecli-interactive 
az vm start --resource-group myResourceGroupVM --name myVM
```

### <a name="delete-resource-group"></a>Supprimer un groupe de ressources

La suppression d’un groupe de ressources supprime également toutes les ressources qu’il contient.

```azurecli-interactive 
az group delete --name myResourceGroupVM --no-wait --yes
```

## <a name="next-steps"></a>Étapes suivantes

Ce didacticiel vous a montré les tâches de base de création et de gestion de machines virtuelles, notamment :

> [!div class="checklist"]
> * Créer et connecter tooa machine virtuelle
> * Sélectionner et utiliser des images de machine virtuelle
> * Afficher et utiliser des tailles de machine virtuelle spécifiques
> * Redimensionner une machine virtuelle
> * Consulter et comprendre l’état d’une machine virtuelle

Avance toohello toolearn de didacticiel suivant sur les disques de machine virtuelle.  

> [!div class="nextstepaction"]
> [Créer et gérer des disques de machine virtuelle](./tutorial-manage-disks.md)
