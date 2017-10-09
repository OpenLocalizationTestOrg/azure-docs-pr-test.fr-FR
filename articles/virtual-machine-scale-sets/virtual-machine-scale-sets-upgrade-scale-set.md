---
title: "ensemble d’une échelle de machine virtuelle Azure aaaUpgrade | Documents Microsoft"
description: "Mettre à niveau un groupe de machines virtuelles identiques Azure"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e229664e-ee4e-4f12-9d2e-a4f456989e5d
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: guybo
ms.openlocfilehash: 068e98503f8d37ea71e45b8673a01da2e814f521
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-a-virtual-machine-scale-set"></a>Mettre à niveau un jeu de mise à l’échelle de machines virtuelles
Cet article décrit comment vous pouvez déployer une échelle de machine virtuelle Azure du système d’exploitation mise à jour tooan définir sans interruption de service. Dans ce contexte, une mise à jour du système d’exploitation implique la modification de la version de hello ou référence (SKU) de hello du système d’exploitation ou la modification de hello URI d’une image personnalisée. Une mise à jour sans interruption de service consiste à mettre à jour des machines virtuelles une par une, ou dans des groupes (par exemple, un domaine d’erreur à la fois), plutôt que toutes simultanément. En procédant de la sorte, les machines virtuelles qui ne sont pas mises à niveau peuvent continuer à opérer.

tooavoid ambiguïté, nous allons faire la distinction quatre types de mise à jour du système d’exploitation vous pourriez tooperform :

* Modification de version de hello ou référence (SKU) d’une image de plateforme. Par exemple, la modification Ubuntu version 14.04.2-LTS 14.04.201506100 too14.04.201507060 ou la modification de hello Ubuntu 15.10 ou la dernière référence (SKU) too16.04.0-LTS/latest. Ce scénario est décrit dans cet article.
* La modification hello URI qui pointe de tooa une nouvelle version d’une image personnalisée que vous avez créé (**propriétés** > **virtualMachineProfile** > **storageProfile**  >  **osDisk** > **image** > **uri**). Ce scénario est décrit dans cet article.
* Modification de référence à l’image d’un ensemble d’échelle qui a été créé à l’aide de disques gérés d’Azure hello.
* Mise à jour corrective hello du système d’exploitation à partir d’un ordinateur virtuel (des exemples l’installation d’un correctif de sécurité et de mise à jour de Windows en cours d’exécution). Ce scénario est pris en charge mais n’est pas traité dans cet article.

Les jeux de mise à l’échelle de machine virtuelle déployés en tant que partie d’un cluster [Azure Service Fabric](https://azure.microsoft.com/services/service-fabric/) ne sont pas abordés ici. Pour plus d’informations sur la mise à jour corrective de Service Fabric, consultez [Application pour appliquer des correctifs au système d’exploitation Windows dans votre cluster Service Fabric](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-patch-orchestration-application).

Hello base séquence pour la modification hello du système d’exploitation version/référence (SKU) d’une image de plateforme ou hello URI d’une image personnalisée se présente comme suit :

1. Obtenir le modèle du jeu de mise à l’échelle hello machine virtuelle.
2. Modifier la version hello, référence (SKU), référence d’image ou valeur de l’URI dans le modèle de hello.
3. Modèle de mise à jour hello.
4. Effectuez un *manualUpgrade* appeler sur des machines virtuelles de hello dans un ensemble d’échelle hello. Cette étape est uniquement pertinente si *upgradePolicy* est défini trop**manuel** dans votre échelle définie. S’il est défini trop**automatique**, tous les ordinateurs virtuels hello sont mis à niveau à la fois, provoquant ainsi des temps d’arrêt.

Avec ces informations à l’esprit, voyons comment vous pourriez mettre à jour la version hello d’une échelle définie dans PowerShell et à l’aide des API REST de hello. Ces exemples couvrent les cas de hello d’une image de plateforme, mais cet article fournit suffisamment d’informations pour vous tooadapt cette image personnalisée de tooa de processus.

## <a name="powershell"></a>PowerShell
Cet exemple met à jour un ensemble d’échelle de machine virtuelle Windows (création toohello utitlisez 4.0.20160229. Après la mise à jour du modèle de hello, il effectue une mise à jour une instance de machine virtuelle à la fois.

```powershell
$rgname = "myrg"
$vmssname = "myvmss"
$newversion = "4.0.20160229"
$instanceid = "1"

# get hello VMSS model
$vmss = Get-AzureRmVmss -ResourceGroupName $rgname -VMScaleSetName $vmssname

# set hello new version in hello model data
$vmss.virtualMachineProfile.storageProfile.imageReference.version = $newversion

# update hello virtual machine scale set model
Update-AzureRmVmss -ResourceGroupName $rgname -Name $vmssname -VirtualMachineScaleSet $vmss

# now start updating instances
Update-AzureRmVmssInstance -ResourceGroupName $rgname -VMScaleSetName $vmssname -InstanceId $instanceId
```

Si vous mettez à jour hello URI pour une image personnalisée au lieu de modifier une version d’image de plateforme, remplacez hello « jeu hello nouvelle version » ligne avec une commande qui met à jour hello URI de l’image source. Par exemple, si un ensemble d’échelle hello a été créé sans l’aide de disques gérés d’Azure, mise à jour hello ressemble à cela :

```powershell
# set hello new version in hello model data
$vmss.virtualMachineProfile.storageProfile.osDisk.image.uri= $newURI
```

Si une image personnalisée en fonction de l’ensemble d’échelle a été créé à l’aide de disques gérés Azure, référence d’image hello est mise à jour. Par exemple :

```powershell
# set hello new version in hello model data
$vmss.virtualMachineProfile.storageProfile.imageReference.id = $newImageReference
```

## <a name="hello-rest-api"></a>Hello API REST
Voici quelques exemples de Python qui utilisent tooroll d’API REST Azure hello une mise à jour de la version du système d’exploitation. Les deux utilisent lightweight de hello [azurerm](https://pypi.python.org/pypi/azurerm) bibliothèque d’API REST Azure wrapper fonctions toodo une opération GET sur l’échelle de hello définie le modèle, suivie d’une commande PUT avec un modèle mis à jour. Elles apparaîtront également dans les vues des instances de machine virtuelle virtuels tooidentify hello par domaine de mise à jour.

### <a name="vmssupgrade"></a>vmssupgrade
 [Vmssupgrade](https://github.com/gbowerman/vmsstools) est un script Python qui a utilisé tooroll out une tooa de mise à niveau du système d’exploitation en cours d’exécution échelle de machines virtuelles définie un domaine de mise à jour à la fois.

![Script Vmssupgrade pour le choix de machines virtuelles ou d’un domaine de mise à jour](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssupgrade-screenshot.png)

Ce script vous permet de choisir les ordinateurs virtuels spécifiques tooupdate ou spécifier un domaine de mise à jour. Il prend en charge la modification d’une version d’image de plateforme ou la modification de hello URI d’une image personnalisée.

### <a name="vmsseditor"></a>Vmsseditor
[Vmsseditor](https://github.com/gbowerman/vmssdashboard) est un éditeur d’usage général pour les jeux de mise à l’échelle de machine virtuelle qui montre un état de machine virtuelle sous la forme d’une carte thermique où une ligne représente un domaine de mise à jour. Entre autres choses, vous pouvez mettre à jour le modèle hello pour un ensemble d’échelle avec une nouvelle version, une référence (SKU) ou un URI d’image personnalisée et choisissez tooupgrade de domaines d’erreur. Lorsque vous procédez ainsi, tous les ordinateurs virtuels hello dans ce domaine de mise à jour sont mis à niveau toohello nouveau modèle. Vous pouvez également effectuer une mise à niveau propagée, selon la taille de lot hello de votre choix.  

Hello capture d’écran suivante montre un modèle d’une échelle définie pour Ubuntu 14.04-2LTS version 14.04.201507060. Toothis outil ont été ajoutées aux nombreuses autres options dans la mesure où cette capture d’écran a été effectuée.

![Modèle Vmsseditor d’un ensemble d’échelle pour Ubuntu 14.04-2LTS](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssEditor1.png)

Après avoir cliqué sur **mise à niveau** , puis **obtenir les détails**, machines virtuelles dans UD 0 démarrer tooupdate.

![Vmsseditor montrant la progression de la mise à jour](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssEditor2.png)

