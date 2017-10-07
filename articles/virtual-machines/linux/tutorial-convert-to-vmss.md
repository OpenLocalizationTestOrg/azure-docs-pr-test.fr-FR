---
title: "ensemble d’une échelle de tooa de machine virtuelle Azure aaaConvert | Documents Microsoft"
description: "Créez et déployez une échelle de machine virtuelle Linux Azure avec hello CLI d’Azure."
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 04/05/2017
ms.author: adegeo
ms.openlocfilehash: e228282ac4855cef589b8500e74e9d461f9aed84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="convert-an-existing-azure-virtual-machine-tooa-scale-set"></a>Convertir un ensemble d’échelle tooa machine virtuelle Azure existante

Ce didacticiel vous montre comment toouse Azure CLI 2.0 tooconvert définie une échelle de machines virtuelles tooa machine virtuelle. Vous apprendrez également comment tooautomate hello d’ordinateurs virtuels hello dans l’échelle de hello configuré. Pour plus d’informations sur comment tooinstall CLI Azure 2.0, consultez [prise en main d’Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md). Pour plus d’informations sur les jeux de mise à l’échelle, consultez [Jeux de mise à l’échelle de machine virtuelle](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md).

## <a name="step-1---deprovision-hello-vm"></a>Étape 1 : hello VM annuler le déploiement

Utiliser SSH tooconnect toohello machine virtuelle.

Hello d’annuler le déploiement machine virtuelle à l’aide de fichiers de toodelete de l’agent de machine virtuelle Azure hello et les données. Pour obtenir une présentation détaillée de l’annulation de l’approvisionnement, consultez [Capture d’une machine virtuelle Linux](capture-image.md).

```bash
sudo waagent -deprovision+user -force
exit
```

## <a name="step-2---capture-an-image-of-hello-vm"></a>Étape 2 : capturer une image de machine virtuelle de hello

Pour obtenir une présentation détaillée de la capture, consultez [Capture d’une machine virtuelle Linux](capture-image.md).

Désallouer hello machine virtuelle avec [az vm désallouer](/cli/azure/vm#deallocate):

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

Généraliser hello machine virtuelle avec [az vm généraliser](/cli/azure/vm#generalize):

```azurecli
az vm generalize --resource-group myResourceGroup --name myVM
```

Créer une image à partir de la ressource d’ordinateur virtuel hello avec [az image création](/cli/azure/image#create):

```azurecli
az image create --resource-group myResourceGroup --name myImage --source myVM
```

## <a name="step-3---create-hello-scale-set"></a>Étape 3 : création d’un ensemble d’échelle hello

Obtenir hello **id** d’image de hello.

```azurecli
az image show --resource-group myResourceGroup --name myImage --query id
```

```json
"/subscriptions/afbdaf8b-9188-4651-bce1-9115dd57c98b/resourceGroups/vmtest/providers/Microsoft.Compute/images/myImage"
```

Créez une machine virtuelle à partir de la ressource d’image à l’aide de la commande [az vmss create](/cli/azure/vmss#create) :

```azurecli
az vmss create --resource-group myResourceGroup --name myScaleSet --image /subscriptions/afbdaf8b-9188-4651-bce1-9115dd57c98b/resourceGroups/vmtest/providers/Microsoft.Compute/images/myImage --upgrade-policy-mode automatic --vm-sku Standard_DS1_v2 --data-disk-sizes-gb 10 --admin-username azureuser --generate-ssh-keys
```

Cette commande joint également un disque de données de 10 Go. N’oubliez pas que, en fonction de la machine virtuelle de hello taille choisie (nous avons utilisé **Standard_DS1_v2**), nombre de hello de disques de données autorisé est différent. Pour plus d’informations, consultez hello [tailles de machine virtuelle](sizes.md).

Une fois la mise à l’échelle hello terminée, connectez tooit. Obtenir la liste d’adresses IP pour les instances de hello pour SSH avec [az mise liste-instance-connexion-info](/cli/azure/vmss#list-instance-connection-info):

```azurecli
az vmss list-instance-connection-info --resource-group myResourceGroup --name myScaleSet
```

```json
[
  "52.183.00.000:50000",
  "52.183.00.000:50003"
]
```

Vous pouvez désormais connecter disque de données toohello machine virtuelle instance tooinitialize hello

```bash
ssh -i ~/.ssh/id_rsa.pub -p 50000 azureuser@52.183.00.000
```

## <a name="step-4---initialize-hello-data-disk"></a>Étape 4 - disque de données hello Initialize

Lors de la machine virtuelle de toohello connecté, partitionner le disque de hello avec `fdisk`:

```bash
(echo n; echo p; echo 1; echo  ; echo  ; echo w) | sudo fdisk /dev/sdc
```

Écrire une partition avec hello toohello `mkfs` commande :

```bash
sudo mkfs -t ext4 /dev/sdc1
```

Monter le disque de nouveau hello afin qu’il soit accessible dans le système d’exploitation de hello :

```bash
sudo mkdir /datadrive ; sudo mount /dev/sdc1 /datadrive
```

disque de Hello peut maintenant être accède via hello datadrive point de montage, ce qui peut être vérifié avec `ls /datadrive/`.

Fin de session SSH hello.


## <a name="step-5---configure-firewall"></a>Étape 5 : Configuration du pare-feu

Introduire une faille via hello pare-feu toohello serveur Web hébergé par un ensemble d’échelle hello. Lors de l’ensemble d’échelle hello a été créé, un équilibreur de charge a également été créé et vous l’avez utilisé **SSH** toohello des ordinateurs virtuels individuels. tooopen un port, vous avez besoin de deux informations que vous pouvez obtenir à l’aide de CLI d’Azure.

* **Pool d’adresses IP frontales**  
`az network lb show --resource-group myResourceGroup --name myScaleSetLB --output table --query frontendIpConfigurations[0].name`

* **Pool d’adresses IP principales**  
`az network lb show --resource-group myResourceGroup --name myScaleSetLB --output table --query backendAddressPools[0].name`

Avec ces deux noms, vous pouvez ouvrir le port **80**.

```azurecli
az network lb rule create --backend-pool-name myScaleSetLBBEPool --backend-port 80 --frontend-ip-name loadBalancerFrontEnd --frontend-port 80 --name webserver --protocol tcp --resource-group myResourceGroup --lb-name myScaleSetLB
```


## <a name="step-6---automate-configuration"></a>Étape 6 : Automatisation de la configuration

disque de données Hello doit toobe configuré sur chaque instance de machine virtuelle. Nous pouvons automatiser la configuration de hello de machine virtuelle hello hello **CustomScript** extension.

Commencez par créer un *.sh* script qui inclut des commandes de format de disque hello.

```sh
#!/bin/bash

# Setup hello data disk
(echo n; echo p; echo 1; echo  ; echo  ; echo w) | fdisk /dev/sdc
fdisk /dev/sdc
mkfs -t ext4 /dev/sdc1
mkdir /datadrive
mount /dev/sdc1 /datadrive

exit 0
```

Ensuite, téléchargez ce hello toowhere du fichier script **CustomScript** extension peut y accéder. Une copie est disponible [ici](https://gist.githubusercontent.com/Thraka/ab1d8b78ac4b23722f3d3c1c03ac5df4).

Créer un fichier local nommé **settings.json** et put hello après le bloc JSON qu’elle contient. Hello `flieUris` toowhere téléchargé vers votre fichier de script doit être affecté à la propriété.

```json
{
  "fileUris": ["https://gist.githubusercontent.com/Thraka/ab1d8b78ac4b23722f3d3c1c03ac5df4/raw/3ac6e385010ac675e23ce583ce27b1a752f1b482/prep-vmss.sh"],
  "commandToExecute": "bash prep-vmss.sh" 
}
```

Déployer cette mise à l’échelle tooyour commande définie par hello **CustomScript** extension, référencement hello **settings.json** fichier que nous venons de créer.

```azurecli
az vmss extension set --publisher Microsoft.Azure.Extensions --version 2.0 --name CustomScript --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

Cette extension s’exécute automatiquement sur toutes les instances actuelles et toutes les instances créées ultérieurement par le biais de la mise à l’échelle.

## <a name="step-7---configure-autoscale-rules"></a>Étape 7 : Configuration des règles de mise à l’échelle automatique

Actuellement, les règles de mise à l’échelle automatique ne peuvent pas être définies dans Azure CLI. Hello d’utilisation [portail Azure](https://portal.azure.com) tooconfigure mise à l’échelle.

## <a name="step-8---management-tasks"></a>Étape 8 : Tâches de gestion

Tout au long du cycle de vie hello de hello ensemble d’échelle, vous devrez peut-être toorun une ou plusieurs tâches de gestion. En outre, vous pouvez toocreate les scripts qui automatisent différentes pour les tâches de cycle de vie, et hello CLI d’Azure fournit un moyen rapide de toodo ces tâches. Voici quelques tâches courantes.

### <a name="get-connection-info"></a>Obtenir des informations de connexion

```azurecli
az vmss list-instance-connection-info --resource-group myResourceGroup --name myScaleSet
```

### <a name="set-instance-count-manual-scale"></a>Définir le nombre d’instances (mise à l’échelle manuelle)

```azurecli
az vmss scale --resource-group myResourceGroup --name myScaleSet --new-capacity 4
```

### <a name="delete-resource-group"></a>Supprimer un groupe de ressources

La suppression d’un groupe de ressources supprime également toutes les ressources qu’il contient.

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Étapes suivantes
toolearn de plus amples informations sur l’échelle de machine virtuelle hello définir des fonctionnalités introduites dans ce didacticiel, consultez hello informations suivantes :

- [Présentation des groupes de machines virtuelles identiques Azure](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md)
- [Vue d’ensemble d’Azure Load Balancer](../../load-balancer/load-balancer-overview.md)
- [Contrôler le flux de trafic réseau avec les groupes de sécurité réseau](../../virtual-network/virtual-networks-nsg.md)