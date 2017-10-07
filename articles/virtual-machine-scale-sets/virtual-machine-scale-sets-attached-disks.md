---
title: "aaaAzure Machine virtuelle échelle jeux attachés des disques de données | Documents Microsoft"
description: "Découvrez comment toouse attachés des disques de données avec des machines virtuelles identiques"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 4/25/2017
ms.author: guybo
ms.openlocfilehash: 77b66f80934c0aaf7bb1ad0de00a738052a878ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-vm-scale-sets-and-attached-data-disks"></a>Groupes de machines virtuelles identiques Azure et disques de données associés
Les [groupes de machines virtuelles identiques](/azure/virtual-machine-scale-sets/) Azure prennent désormais en charge les machines virtuelles avec des disques de données associés. Disques de données peuvent être définies dans le profil de stockage hello pour les jeux de mise à l’échelle qui ont été créés avec des disques gérés Azure. Précédemment hello options de stockage directement connecté uniquement disponible avec des machines virtuelles dans le jeu de mise à l’échelle ont été les lecteurs de hello du système d’exploitation et les lecteurs temporaires.

> [!NOTE]
>  Lorsque vous créez une échelle avec des disques de données attaché définis, vous devez toujours toomount et hello du format disques à partir d’au sein d’une machine virtuelle toouse les (comme pour la version autonome de machines virtuelles Azure). Un moyen pratique de toodo il s’agit de toouse une extension de script personnalisé qui appelle une toopartition script standard et de mettre en forme tous les disques de données hello sur une machine virtuelle.

## <a name="create-a-scale-set-with-attached-data-disks"></a>Créer un groupe identique avec des disques de données associés
Un toocreate facilement une échelle définie avec les disques attachés est toouse hello [CLI d’Azure](https://github.com/Azure/azure-cli) _mise créer_ commande. Bonjour à l’exemple suivant crée un groupe de ressources Azure et un ensemble d’échelle de machine virtuelle de machines virtuelles Ubuntu 10, chacun avec des disques de données attaché 2 de 50 et 100 Go respectivement.
```bash
az group create -l southcentralus -n dsktest
az vmss create -g dsktest -n dskvmss --image ubuntults --instance-count 10 --data-disk-sizes-gb 50 100
```
Notez que hello _mise créer_ commande par défaut de certaines valeurs de configuration si vous ne spécifiez pas les. toosee hello options disponibles que vous pouvez remplacer try :
```bash
az vmss create --help
```
Une autre façon toocreate une échelle avec des disques de données attachés est toodefine une échelle définie dans un modèle Azure Resource Manager, incluez un _dataDisks_ section Bonjour _storageProfile_et déployer hello modèle. Hello 50 et 100 Go disque exemple ci-dessus est défini comme suit dans le modèle de hello :
```json
"dataDisks": [
    {
    "lun": 1,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 50
    },
    {
    "lun": 2,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 100
    }
]
```
Vous pouvez voir un exemple de toodeploy terminé, prêt d’un modèle de jeu de mise à l’échelle avec un disque connecté défini ici : [https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data](https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data).

## <a name="adding-a-data-disk-tooan-existing-scale-set"></a>Ajout d’une échelle existant de tooan de disque de données définie
> [!NOTE]
>  Vous pouvez joindre uniquement les données des disques tooa identiques qui a été créé avec [disques gérés d’Azure](./virtual-machine-scale-sets-managed-disks.md).

Vous pouvez ajouter une échelle de machine virtuelle données disque tooa définie à l’aide d’Azure CLI _attacher de disque de mise az_ commande. Assurez-vous de spécifier un numéro d’unité logique (LUN) qui n’est pas déjà utilisé. Hello CLI l’exemple suivant ajoute un toolun de lecteur 50 Go 3 :
```bash
az vmss disk attach -g dsktest -n dskvmss --size-gb 50 --lun 3
```

Hello PowerShell l’exemple suivant ajoute un toolun de lecteur 50 Go 3 :
```powershell
$vmss = Get-AzureRmVmss -ResourceGroupName myvmssrg -VMScaleSetName myvmss
$vmss = Add-AzureRmVmssDataDisk -VirtualMachineScaleSet $vmss -Lun 3 -Caching 'ReadWrite' -CreateOption Empty -DiskSizeGB 50 -StorageAccountType StandardLRS
Update-AzureRmVmss -ResourceGroupName myvmssrg -Name myvmss -VirtualMachineScaleSet $vmss
```

> [!NOTE]
> Différentes tailles de machine virtuelle ont des limites différentes sur les numéros de hello de disques attachés, qu'ils prennent en charge. Vérifiez hello [caractéristiques de taille de machine virtuelle](../virtual-machines/windows/sizes.md) avant d’ajouter un nouveau disque.

Vous pouvez également ajouter un disque en ajoutant un nouveau toohello d’entrée _dataDisks_ propriété Bonjour _storageProfile_ d’une échelle de définir la définition et l’application hello modification. tootest, rechercher une définition de jeu de mise à l’échelle existante Bonjour [Explorateur de ressources Azure](https://resources.azure.com/). Sélectionnez _modifier_ et ajouter une nouvelle liste de disque toohello de disques de données. Par exemple, à l’aide d’exemple hello ci-dessus :
```json
"dataDisks": [
    {
    "lun": 1,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 50
    },
    {
    "lun": 2,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 100
    },
    {
    "lun": 3,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 20
    }          
]
```

Puis sélectionnez _PUT_ tooapply hello modifie l’ensemble d’échelle tooyour. Cet exemple doit fonctionner tant que vous utilisez une taille de machine virtuelle qui prend en charge plus de deux disques de données associés.

> [!NOTE]
> Lorsque vous effectuez une tooa modifier l’échelle définition telle que l’ajout ou la suppression d’un disque de données, il applique des machines virtuelles de tooall nouvellement créé, mais s’applique uniquement tooexisting VMs si hello _upgradePolicy_ propriété a la valeur trop « automatique ». S’il est défini trop « manuel », vous devez toomanually appliquer hello nouveau modèle tooexisting machines virtuelles. Vous pouvez faire cela dans portail de hello, à l’aide de hello _AzureRmVmssInstance de mise à jour_ PowerShell commande ou à l’aide de hello _mise à jour-les instances az mise_ commande CLI.

## <a name="adding-pre-populated-data-disks-tooan-existent-scale-set"></a>Ajout des données préremplie disques tooan inexistant identiques 
> Lorsque vous ajoutez tooan disques inexistant ensemble d’échelle de modèle, par conception, disque de hello est toujours créé vide. Ce scénario inclut également les nouvelles instances créées par un ensemble d’échelle hello. Ce comportement est, car la définition de scaleset hello possède un disque de données vide. Dans l’ordre toocreate préremplie lecteurs de données pour un modèle de jeu de mise à l’échelle inexistant, vous pouvez choisir une des deux options suivantes :

* Copier les données à partir de disques de données hello instance 0 machine virtuelle toohello Bonjour autres machines virtuelles en exécutant un script personnalisé.
* Créer une image managée avec un disque de hello du système d’exploitation plus de disque de données (avec des données hello requis) et créer un nouveau scaleset avec l’image de hello. Ainsi, chaque nouvelle machine virtuelle créée aura une donnée de disque qui est fourni dans la définition de hello de hello scaleset. Étant donné que cette définition fait référence image tooan avec un disque de données qui a des données personnalisées, chaque ordinateur virtuel sur hello scaleset automatiquement s’avec ces modifications.

> Hello toocreate façon une image personnalisée se trouve ici : [créer une image managée d’une machine virtuelle généralisée dans Azure](/azure/virtual-machines/windows/capture-image-resource/) 

> utilisateur Hello doit toocapture hello d’instance 0 machine virtuelle qui a hello les données requises et ensuite utiliser ce disque dur virtuel pour la définition d’image hello.

## <a name="removing-a-data-disk-from-a-scale-set"></a>Supprimer un disque de données d’un groupe identique
Vous pouvez supprimer un disque de données d’un groupe de machines virtuelles identiques à l’aide de la commande _az vmss disk detach_ d’Azure CLI. Par exemple hello commande suivante supprime hello disque défini au numéro d’unité logique 2 :
```bash
az vmss disk detach -g dsktest -n dskvmss --lun 2
```  
De même, vous pouvez également supprimer un disque à partir d’une mise à l’échelle en supprimant une entrée à partir de hello _dataDisks_ propriété Bonjour _storageProfile_ et l’application des modifications de hello. 

## <a name="additional-notes"></a>Remarques supplémentaires
Prise en charge pour disques de données associés de jeu de disques gérés par Azure et l’échelle est disponible dans la version de l’API [ _2016-04-30-preview_ ](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-compute/2016-04-30-preview/swagger/compute.json) ou version ultérieure de hello Microsoft.Compute API.

Dans l’implémentation initiale de hello de prise en charge des disques attachés pour les jeux de mise à l’échelle, vous ne peut pas attacher ou détacher des disques de données vers ou depuis des ordinateurs virtuels individuels dans un ensemble d’échelle.

La prise en charge du portail Azure pour les disques de données associés dans des groupes identiques est initialement limitée. Selon vos besoins, que vous pouvez utiliser les modèles Azure, toomanage CLI, PowerShell, kits de développement logiciel et API REST de disques attachés.


