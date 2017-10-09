---
title: "aaaUsing gérés disques avec Azure machines virtuelles identiques | Documents Microsoft"
description: "Découvrez pourquoi et comment toouse gérés disques avec les machines virtuelles identiques"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 6/01/2017
ms.author: negat
ms.openlocfilehash: 0e2a21e9f8b114ae1c8b81e1e6124621366f5643
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-vm-scale-sets-and-managed-disks"></a>Groupes de machines virtuelles identiques Azure et disques gérés

Les [groupes de machines virtuelles identiques](/azure/virtual-machine-scale-sets/) Azure prennent en charge les machines virtuelles avec disques gérés. Les disques gérés avec groupes identiques présentent plusieurs avantages, notamment :

* Vous n’avez plus besoin toopre-créer et gérer des disques de stockage comptes toostore hello du système d’exploitation pour l’ensemble d’échelle de hello de machines virtuelles.

* Vous pouvez joindre des données managées disques toohello identiques.

* Avec un disque géré, un groupe identique peut atteindre une capacité de 1 000 machines virtuelles à partir d’une image de plateforme ou de 100 machines virtuelles à partir d’une image personnalisée.

## <a name="get-started"></a>Prise en main

Un moyen simple tooget main identiques de disque géré est un toodeploy de hello portail Azure. Pour plus d’informations, consultez [cet article](./virtual-machine-scale-sets-portal-create.md). Une autre façon simple tooget démarré est toouse [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2) toodeploy une échelle définie. Hello suivant montre comment toocreate un Ubuntu en fonction de l’échelle avec des machines 10 virtuelles, chacun avec un disque de 50 Go et de 100 Go de données :

```azurecli
az group create -l southcentralus -n dsktest
az vmss create -g dsktest -n dskvmss --image ubuntults --instance-count 10 --data-disk-sizes-gb 50 100
```

Vous pouvez également consulter hello [référentiel GitHub de modèles de démarrage rapide Azure](https://github.com/Azure/azure-quickstart-templates) pour les dossiers qui contiennent des `vmss` toosee prégénérées des exemples de modèles de déploiement identiques. tootell les modèles sont déjà à l’aide de disques gérés, vous pouvez faire référence trop[cette liste](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md).

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur les disques gérés en général, consultez [cet article](../virtual-machines/windows/managed-disks-overview.md).

reportez-vous à la méthode de tooconvert une échelle de tooprovision de modèle de gestionnaire de ressources définit avec gestion des disques, toosee [cet article](./virtual-machine-scale-sets-convert-template-to-md.md). Hello mêmes modèles de gestionnaire de ressources toohello modifications s’appliquent toohello API REST Azure.

toolearn savoir plus sur l’utilisation de disques de données managées avec identiques, consultez [cet article](./virtual-machine-scale-sets-attached-disks.md).

toobegin les jeux à grande échelle, consultez trop[cet article](./virtual-machine-scale-sets-placement-groups.md).


