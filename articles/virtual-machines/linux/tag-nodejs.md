---
title: aaaHow tootag une machine virtuelle de Azure Linux | Documents Microsoft
description: "En savoir plus sur le balisage d’une machine virtuelle de Azure Linux créée dans Azure à l’aide du modèle de déploiement du Gestionnaire de ressources hello."
services: virtual-machines-linux
documentationcenter: 
author: mmccrory
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: ca0e17e5-d78e-42e6-9dad-c1e8f1c58027
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/28/2017
ms.author: memccror
ms.openlocfilehash: 0e99ea66a87b7e00eb21a2f72dd2bce8673778dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootag-a-linux-virtual-machine-in-azure"></a>Comment tootag une machine virtuelle de Linux dans Azure
Cet article décrit les différentes façons tootag une machine virtuelle de Linux dans Azure via le modèle de déploiement du Gestionnaire de ressources hello. Les balises sont des paires clé/valeur définies par l’utilisateur, qui peuvent être placées directement sur une ressource ou sur un groupe de ressources. Azure prend actuellement en charge des balises de too15 par la ressource et le groupe de ressources. Balises peuvent être placées sur une ressource au moment de la création de hello ou ajouté tooan les ressources existantes. Notez les balises sont pris en charge pour les ressources créées via le modèle de déploiement Resource Manager hello uniquement.

[!INCLUDE [virtual-machines-common-tag](../../../includes/virtual-machines-common-tag.md)]

## <a name="tagging-with-azure-cli"></a>Balisage avec l’interface de ligne de commande Azure
toobegin, [installer et configurer hello CLI d’Azure](../../xplat-cli-azure-resource-manager.md) et assurez-vous que vous êtes en mode de gestionnaire de ressources (`azure config mode arm`).

Vous pouvez afficher toutes les propriétés d’un ordinateur virtuel donné, y compris les balises de hello, à l’aide de cette commande :

        azure vm show -g MyResourceGroup -n MyTestVM

tooadd une nouvelle balise de machine virtuelle via hello CLI d’Azure, vous pouvez utiliser hello `azure vm set` commande en même temps que le paramètre de la balise hello **-t**:

        azure vm set -g MyResourceGroup -n MyTestVM –t myNewTagName1=myNewTagValue1;myNewTagName2=myNewTagValue2

tooremove toutes les balises, vous pouvez utiliser hello **– T** paramètre Bonjour `azure vm set` commande.

        azure vm set – g MyResourceGroup –n MyTestVM -T


Maintenant que nous ont appliqué les balises tooour ressources CLI d’Azure et hello Portal, examinons un toosee de détails d’utilisation hello les balises hello dans le portail de facturation hello.

[!INCLUDE [virtual-machines-common-tag-usage](../../../includes/virtual-machines-common-tag-usage.md)]

## <a name="next-steps"></a>Étapes suivantes
* toolearn en savoir plus sur le marquage de vos ressources Azure, consultez [vue d’ensemble du Gestionnaire de ressources Azure] [ Azure Resource Manager Overview] et [à l’aide de balises tooorganize vos ressources Azure] [ Using Tags tooorganize your Azure Resources].
* toosee balises peuvent vous aider à gérer votre utilisation des ressources Azure, voir [comprendre votre facture Azure] [ Understanding your Azure Bill] et [obtenir votre consommation de ressources Microsoft Azure] [Gain insights into your Microsoft Azure resource consumption].

[Azure CLI environment]: ../../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Azure Resource Manager Overview]: ../../azure-resource-manager/resource-group-overview.md
[Using Tags tooorganize your Azure Resources]: ../../azure-resource-manager/resource-group-using-tags.md
[Understanding your Azure Bill]: ../../billing/billing-understand-your-bill.md
[Gain insights into your Microsoft Azure resource consumption]: ../../billing/billing-usage-rate-card-overview.md
