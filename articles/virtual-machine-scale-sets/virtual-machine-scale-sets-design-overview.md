---
title: "aaaDesign considérations pour les groupes de mise à l’échelle de machines virtuelles Azure | Documents Microsoft"
description: "En savoir plus sur les considérations relatives à la conception des groupes de machines virtuelles identiques Azure"
keywords: machine virtuelle linux, groupes de machines virtuelles identiques
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: madhana
editor: tysonn
tags: azure-resource-manager
ms.assetid: c27c6a59-a0ab-4117-a01b-42b049464ca1
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: negat
ms.openlocfilehash: f8644d36fe5903bd4b74df26dca5dc3211ee3516
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="design-considerations-for-scale-sets"></a>Considérations relatives à la conception des groupes de machines virtuelles identiques
Cette rubrique présente les considérations à prendre en compte pour créer des groupes de machines virtuelles identiques. Pour plus d’informations sur les machines virtuelles identiques, consultez trop[vue d’ensemble des jeux de Machine virtuelle mise à l’échelle](virtual-machine-scale-sets-overview.md).

## <a name="when-toouse-scale-sets-instead-of-virtual-machines"></a>Lorsque mise à l’échelle toouse définit au lieu de machines virtuelles ?
En règle générale, les groupes identiques sont utiles pour le déploiement d’infrastructures hautement disponibles où un ensemble de machines a une configuration similaire. Toutefois, certaines fonctionnalités sont uniquement disponibles dans les groupes identiques, tandis que d’autres le sont seulement dans les machines virtuelles individuelles. Dans commande toomake quand une décision informée toouse chaque technologie, nous devons tout d’abord examiner certaines des fonctionnalités hello couramment utilisé qui sont disponibles dans les jeux de mise à l’échelle, mais pas les ordinateurs virtuels :

### <a name="scale-set-specific-features"></a>Fonctionnalités spécifiques des groupes identiques

- Une fois que vous spécifiez la configuration du jeu de mise à l’échelle hello, vous pouvez simplement mettre à jour toodeploy de propriété « capacité » hello davantage d’ordinateurs virtuels en parallèle. Cela est beaucoup plus simple que d’écrire un tooorchestrate script déployer plusieurs ordinateurs virtuels individuels en parallèle.
- Vous pouvez [utilisez Azure mise à l’échelle tooautomatically faire évoluer un ensemble d’échelle](./virtual-machine-scale-sets-autoscale-overview.md) mais pas les ordinateurs virtuels.
- Vous pouvez [réinitialiser les machines virtuelles des groupes identiques](https://docs.microsoft.com/rest/api/virtualmachinescalesets/manage-a-vm), mais [pas les machines virtuelles individuelles](https://docs.microsoft.com/rest/api/compute/virtualmachines).
- Vous pouvez [sur-approvisionner](./virtual-machine-scale-sets-design-overview.md) les machines virtuelles d’un groupe identique pour une fiabilité accrue et un déploiement plus rapide. Vous ne peut pas faire avec des ordinateurs virtuels individuels, sauf si vous écrivez un code personnalisé toodo cela.
- Vous pouvez spécifier une [mise à niveau de la stratégie](./virtual-machine-scale-sets-upgrade-scale-set.md) toomake il tooroll facilement les mises à niveau sur les machines virtuelles dans votre ensemble d’échelle. Avec des machines virtuelles individuelles, vous devez orchestrer les mises à jour vous-même.

### <a name="vm-specific-features"></a>Fonctionnalités spécifiques des machines virtuelles

Sur hello autre part, certaines fonctionnalités sont uniquement disponibles dans les machines virtuelles (au moins pour hello instant) :

- Vous pouvez attacher toospecific de disques de données des ordinateurs virtuels individuels, mais que les disques de données attachés sont configurés pour tous les ordinateurs virtuels dans un ensemble d’échelle.
- Vous pouvez attacher des disques de données de non vide tooindividual machines virtuelles, mais pas les machines virtuelles dans un ensemble d’échelle.
- Vous pouvez prendre un instantané d’une machine virtuelle individuelle, mais cela n’est pas possible dans un groupe identique.
- Vous pouvez capturer une image à partir d’une machine virtuelle individuelle, mais cela n’est pas possible dans un groupe identique.
- Vous pouvez migrer une machine virtuelle individuelle à partir de disques de toomanaged disques native, mais vous ne pouvez pas le faire pour les machines virtuelles dans un ensemble d’échelle.
- Vous pouvez affecter des adresses IP publiques IPv6 NIC de machine virtuelle tooindividual mais ne peut pas le faire pour les machines virtuelles dans un ensemble d’échelle. Notez que vous pouvez affecter des adresses IP publiques IPv6 équilibrages tooload devant soit des ordinateurs virtuels individuels ou ensemble d’échelle de machines virtuelles.

## <a name="storage"></a>Storage

### <a name="scale-sets-with-azure-managed-disks"></a>Groupes identiques avec Azure Managed Disks
Les groupes identiques peuvent être créés avec [Azure Managed Disks](../virtual-machines/windows/managed-disks-overview.md) plutôt qu’à partir des comptes de stockage Azure traditionnels. Disques gérés fournissent hello avantages suivants :
- Vous n’avez pas toopre-créer un ensemble de comptes de stockage Azure pour l’ensemble d’échelle de hello de machines virtuelles.
- Vous pouvez définir [disques de données associés](virtual-machine-scale-sets-attached-disks.md) pour hello machines virtuelles dans votre échelle définie.
- Groupes identiques peuvent être configurés trop[prennent en charge des too1, 000 machines virtuelles dans un jeu de](virtual-machine-scale-sets-placement-groups.md). 

Si vous avez un modèle existant, vous pouvez également [mettre à jour hello modèle toouse géré disques](virtual-machine-scale-sets-convert-template-to-md.md).

### <a name="user-managed-storage"></a>Stockage géré par l’utilisateur
Un ensemble d’échelle n’est pas défini avec des disques gérés Azure s’appuie sur créés par l’utilisateur de stockage comptes toostore hello du système d’exploitation des disques de machines virtuelles de hello dans hello ensemble. Un ratio de 20 ordinateurs virtuels au maximum par compte de stockage est recommandé tooachieve des e/s maximum et également tirer parti de _un surapprovisionnement_ (voir ci-dessous). Il est également recommandé que vous répartis hello premiers caractères des noms de compte de stockage hello alphabet de hello. Cette méthode améliore la répartition sur les différents systèmes internes. 


## <a name="overprovisioning"></a>Sur-approvisionnement
Échelle définit par défaut actuellement trop » un surapprovisionnement » les ordinateurs virtuels. Avec un surapprovisionnement sous tension, mise à l’échelle hello définie réellement spins plus des ordinateurs virtuels que vous avez demandé, puis supprime hello des machines virtuelles supplémentaires une fois hello a demandé le nombre de machines virtuelles sont correctement configurés. Le sur-approvisionnement améliore les taux de réussite de l’approvisionnement et réduit la durée du déploiement. Vous n’êtes pas facturé pour hello des machines virtuelles supplémentaires et ils ne comptent pas pour les limites de quota.

Pendant un surapprovisionnement améliore-t-il les taux de réussite de mise en service, il peut provoquer un comportement déroutant pour une application est conçue pas toohandle des machines virtuelles supplémentaires qui apparaissent et puis disparaît. tooturn un surapprovisionnement, assurez-vous d’avoir hello suivent la chaîne dans votre modèle : `"overprovision": "false"`. Vous trouverez plus de détails dans hello [documentation de l’API REST de définir l’échelle](/rest/api/virtualmachinescalesets/create-or-update-a-set).

Si votre ensemble d’échelle utilise le stockage géré par l’utilisateur et que vous désactivez un surapprovisionnement, vous pouvez avoir plus de 20 ordinateurs virtuels par compte de stockage, mais toogo au-dessus de 40 pour des raisons de performances d’e/s n’est pas recommandée. 

## <a name="limits"></a>limites
Un ensemble d’échelle basée sur une image de Marketplace (également appelé une image de plateforme) et configuré toouse que disques gérés de Azure prend en charge une capacité de configuration too1, 000 machines virtuelles. Si vous configurez votre toosupport de jeu de mise à l’échelle plus de 100 machines virtuelles, pas tous les scénarios travail hello identiques (par exemple l’équilibrage de charge). Pour plus d’informations, consultez [Utilisation de grands groupes de machines virtuelles identiques](virtual-machine-scale-sets-placement-groups.md). 

Une échelle configurée avec des comptes de stockage géré par l’utilisateur est actuellement limitée too100 VMs (et les comptes de stockage 5 sont recommandés pour cette échelle).

Un ensemble d’échelle reposant sur une image personnalisée (une par vous) peut avoir une capacité d’ordinateurs virtuels de too100 lorsque configurés avec des disques gérés par Azure. Si l’ensemble d’échelle hello est configuré avec des comptes de stockage géré par l’utilisateur, il doit créer tous les disques durs virtuels de disque du système d’exploitation au sein d’un compte de stockage. Par conséquent, au maximum hello le nombre recommandé de machines virtuelles dans un ensemble d’échelle reposant sur une image personnalisée et stockage géré par l’utilisateur est 20. Si vous désactivez un surapprovisionnement, vous pouvez monter too40.

Pour les machines virtuelles plus que de permettent à ces limites, vous devez toodeploy échelle multiples définit comme indiqué dans [ce modèle](https://github.com/Azure/azure-quickstart-templates/tree/master/301-custom-images-at-scale).

