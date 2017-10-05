---
title: "Créer et gérer des machines virtuelles Linux avec Azure CLI | Microsoft Docs"
description: "Didacticiel : créer et gérer des machines virtuelles Linux avec l’interface Azure CLI"
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
ms.openlocfilehash: c163c715eb1438a0d6b0ab53cbb43816ca8dbbb4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="create-and-manage-linux-vms-with-the-azure-cli"></a>Créer et gérer des machines virtuelles Linux avec l’interface Azure CLI

Les machines virtuelles fournissent un environnement informatique entièrement configurable et flexible. Ce didacticiel traite d’aspects de base du déploiement de machines virtuelles Azure, tels que la sélection d’une taille de machine virtuelle, la sélection d’une image de machine virtuelle et le déploiement d’une machine virtuelle. Vous allez apprendre à effectuer les actions suivantes :

> [!div class="checklist"]
> * Créer une machine virtuelle et vous y connecter
> * Sélectionner et utiliser des images de machine virtuelle
> * Afficher et utiliser des tailles de machine virtuelle spécifiques
> * Redimensionner une machine virtuelle
> * Consulter et comprendre l’état d’une machine virtuelle


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Si vous choisissez d’installer et d’utiliser l’interface de ligne de commande localement, vous devez exécuter l’interface de ligne de commande Azure version 2.0.4 ou une version ultérieure pour poursuivre la procédure décrite dans ce didacticiel. Exécutez `az --version` pour trouver la version. Si vous devez installer ou mettre à niveau, consultez [Installation d’Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="create-resource-group"></a>Créer un groupe de ressources

Créez un groupe de ressources avec la commande [az group create](https://docs.microsoft.com/cli/azure/group#create). 

Un groupe de ressources Azure est un conteneur logique dans lequel les ressources Azure sont déployées et gérées. Un groupe de ressources doit être créé avant les machines virtuelles. Dans cet exemple, un groupe de ressources nommé *myResourceGroupVM* est créé dans la région *eastus*. 

```azurecli-interactive 
az group create --name myResourceGroupVM --location eastus
```

Le groupe de ressources est spécifié lors de la création ou de la modification d’une machine virtuelle, qui peut être vue dans ce didacticiel.

## <a name="create-virtual-machine"></a>Create virtual machine

Créez une machine virtuelle avec la commande [az vm create](https://docs.microsoft.com/cli/azure/vm#create). 

Lorsque vous créez une machine virtuelle, plusieurs options sont disponibles, comme l’image de système d’exploitation, les informations d’identification d’administration ou le dimensionnement des disques. Dans cet exemple, une machine virtuelle nommée *myVM* est créée et exécute Ubuntu Server. 

```azurecli-interactive 
az vm create --resource-group myResourceGroupVM --name myVM --image UbuntuLTS --generate-ssh-keys
```

Une fois la machine virtuelle créée, l’interface Azure CLI fournit des informations concernant cette machine virtuelle. Notez la valeur de `publicIpAddress`, car cette adresse peut être utilisée pour accéder à la machine virtuelle. 

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

## <a name="connect-to-vm"></a>Se connecter à une machine virtuelle

Vous pouvez maintenant vous connecter à la machine virtuelle à l’aide de SSH. Remplacez l’exemple d’adresse IP par la valeur de `publicIpAddress` notée à l’étape précédente.

```bash
ssh 52.174.34.95
```

Une fois que vous avez terminé avec la machine virtuelle, fermez la session SSH. 

```bash
exit
```

## <a name="understand-vm-images"></a>Comprendre les images de machine virtuelle

La Place de marché Azure comprend de nombreuses images qui permettent de créer des machines virtuelles. Dans les étapes précédentes, une machine virtuelle a été créée à l’aide d’une image Ubuntu. Dans cette étape, vous allez utiliser l’interface Azure CLI pour rechercher dans la Place de marché une image CentOS, qui servira ensuite à déployer une deuxième machine virtuelle.  

Pour afficher une liste des images les plus couramment utilisées, utilisez la commande [az vm image list](/cli/azure/vm/image#list).

```azurecli-interactive 
az vm image list --output table
```

La commande renvoie les images de machine virtuelle les plus populaires sur Azure.

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

Vous pouvez obtenir une liste complète en ajoutant l’argument `--all`. Vous pouvez également utiliser `--publisher` ou `–-offer` pour filtrer la liste d’images. Dans cet exemple, la liste est filtrée pour toutes les images dont l’offre correspond à *CentOS*. 

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

Pour déployer une machine virtuelle en utilisant une image spécifique, notez la valeur de la colonne *Urn*. Lorsque vous spécifiez l’image, le numéro de version de l’image peut être remplacé par la valeur « latest », qui sélectionne la dernière version de la distribution. Dans cet exemple, l’argument `--image` est utilisé pour spécifier la version la plus récente d’une image CentOS 6.5.  

```azurecli-interactive 
az vm create --resource-group myResourceGroupVM --name myVM2 --image OpenLogic:CentOS:6.5:latest --generate-ssh-keys
```

## <a name="understand-vm-sizes"></a>Comprendre les tailles de machine virtuelle

Une taille de machine virtuelle détermine la quantité de ressources de calcul comme le processeur, le processeur graphique (GPU) et la mémoire qui sont mises à la disposition de la machine virtuelle. Les machines virtuelles doivent être correctement dimensionnés en fonction de la charge de travail attendue. Si la charge de travail augmente, une machine virtuelle existante peut être redimensionnée.

### <a name="vm-sizes"></a>Tailles de machine virtuelle

Le tableau suivant classe les tailles en fonction des cas d’utilisation.  

| Type                     | Tailles           |    Description       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| [Usage général](sizes-general.md)         |Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7| Ratio processeur/mémoire équilibré. Idéale pour le développement/test et pour les petites et moyennes applications et solutions de données.  |
| [Optimisé pour le calcul](sizes-compute.md)   | Fs, F             | Ratio processeur/mémoire élevé. Convient pour les applications au trafic moyen, les appliances réseau et les processus de traitement par lots.        |
| [Mémoire optimisée](../virtual-machines-windows-sizes-memory.md)    | Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D   | Ratio mémoire/cœur élevé. Idéale pour les bases de données relationnelles, les caches moyens à grands et l’analytique en mémoire.                 |
| [Optimisé pour le stockage](../virtual-machines-windows-sizes-storage.md)      | Ls                | Débit de disque et E/S élevés. Idéale pour les bases de données NoSQL, SQL et Big Data.                                                         |
| [GPU](sizes-gpu.md)          | NV, NC            | Machines virtuelles spécialisées conçues pour les opérations graphiques lourdes et la retouche vidéo.       |
| [Hautes performances](sizes-hpc.md) | H, A8-11          | Nos machines virtuelles dotées des processeurs les plus puissants avec interfaces réseau haut débit en option (RDMA). 


### <a name="find-available-vm-sizes"></a>Rechercher les tailles de machines virtuelles disponibles

Pour afficher la liste des tailles de machines virtuelles disponibles dans une région particulière, utilisez la commande [az vm list-sizes](/cli/azure/vm#list-sizes). 

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

Dans le précédent exemple de création d’une machine virtuelle, aucune taille n’a été spécifiée ; la taille par défaut a donc été appliquée. Vous pouvez sélectionner une taille de machine virtuelle au moment de la création à l’aide de la commande [az vm create](/cli/azure/vm#create) et de l’argument `--size`. 

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupVM \
    --name myVM3 \
    --image UbuntuLTS \
    --size Standard_F4s \
    --generate-ssh-keys
```

### <a name="resize-a-vm"></a>Redimensionner une machine virtuelle

Après avoir déployé une machine virtuelle, vous pouvez la redimensionner pour augmenter ou diminuer l’allocation des ressources.

Avant de redimensionner une machine virtuelle, vérifiez si la taille souhaitée est disponible dans le cluster Azure actuel. La commande [az vm list-vm-resize-options](/cli/azure/vm#list-vm-resize-options) commande renvoie la liste des tailles disponibles. 

```azurecli-interactive 
az vm list-vm-resize-options --resource-group myResourceGroupVM --name myVM --query [].name
```
Si la taille souhaitée est disponible, la machine virtuelle peut être redimensionnée à partir d’un état sous tension, mais elle est redémarrée au cours de l’opération. Utilisez la commande [az vm resize]( /cli/azure/vm#resize) commande pour effectuer le redimensionnement.

```azurecli-interactive 
az vm resize --resource-group myResourceGroupVM --name myVM --size Standard_DS4_v2
```

Si la taille souhaitée ne figure pas dans le cluster actuel, la machine virtuelle doit être libérée avant de procéder au redimensionnement. Utilisez la commande [az vm deallocate]( /cli/azure/vm#deallocate) pour arrêter la machine virtuelle et la libérer. Notez que lorsque la machine virtuelle est remise sous tension, toutes les données contenues dans le disque temporaire peuvent être supprimées. L’adresse IP publique change également, sauf si une adresse IP statique est utilisée. 

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupVM --name myVM
```

Après la libération, le redimensionnement peut être effectué. 

```azurecli-interactive 
az vm resize --resource-group myResourceGroupVM --name myVM --size Standard_GS1
```

Après le redimensionnement, la machine virtuelle peut être démarrée.

```azurecli-interactive 
az vm start --resource-group myResourceGroupVM --name myVM
```

## <a name="vm-power-states"></a>États d’alimentation de la machine virtuelle

Une machine virtuelle Azure peut présenter différents états d’alimentation. Cet état représente l’état actuel de la machine virtuelle du point de vue de l’hyperviseur. 

### <a name="power-states"></a>États d’alimentation

| État d’alimentation | Description
|----|----|
| Starting | Indique que la machine virtuelle est en cours de démarrage. |
| Exécution | Indique que la machine virtuelle est en cours d’exécution. |
| En cours d’arrêt | Indique que la machine virtuelle est en cours d’arrêt. | 
| Arrêté | Indique que la machine virtuelle est arrêtée. Les machines virtuelles à l’état arrêté entraînent toujours des frais de calcul.  |
| Libération | Indique que la machine virtuelle est en cours de libération. |
| Libéré | Indique que la machine virtuelle est supprimée de l’hyperviseur, mais reste disponible dans le plan de contrôle. Les machines virtuelles à l’état Libéré n’entraînent pas de frais de calcul. |
| - | Indique que l’état d’alimentation de la machine virtuelle est inconnu. |

### <a name="find-power-state"></a>Rechercher un état d’alimentation

Pour récupérer l’état d’une machine virtuelle spécifique, utilisez la commande [az vm get instance-view](/cli/azure/vm#get-instance-view). Veillez à spécifier le nom valide d’une machine virtuelle et d’un groupe de ressources. 

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

Pendant le cycle de vie d’une machine virtuelle, vous souhaiterez exécuter des tâches de gestion telles que le démarrage, l’arrêt ou la suppression d’une machine virtuelle. En outre, vous souhaiterez peut-être créer des scripts pour automatiser les tâches répétitives ou complexes. À l’aide de l’interface Azure CLI, de nombreuses tâches courantes de gestion peuvent être exécutées à partir de la ligne de commande ou dans des scripts. 

### <a name="get-ip-address"></a>Obtenir l’adresse IP

Cette commande renvoie les adresses IP publiques et privées d’une machine virtuelle.  

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
> * Créer une machine virtuelle et vous y connecter
> * Sélectionner et utiliser des images de machine virtuelle
> * Afficher et utiliser des tailles de machine virtuelle spécifiques
> * Redimensionner une machine virtuelle
> * Consulter et comprendre l’état d’une machine virtuelle

Passez au didacticiel suivant pour en savoir plus sur les disques de machine virtuelle.  

> [!div class="nextstepaction"]
> [Créer et gérer des disques de machine virtuelle](./tutorial-manage-disks.md)
