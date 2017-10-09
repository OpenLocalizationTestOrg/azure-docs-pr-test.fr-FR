---
title: aaaSet des points de terminaison sur un VM Linux classique | Documents Microsoft
description: En savoir plus tooset des points de terminaison pour un VM Linux Bonjour tooallow de portail classique Azure communication avec un ordinateur virtuel de Linux dans Azure
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: f3749738-1109-4a1d-8635-40e4bd220e91
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: cynthn
ms.openlocfilehash: 1c959d10dd1e20228fa4a20e1cc0205c1d12f185
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-up-endpoints-on-a-linux-classic-virtual-machine-in-azure"></a>Comment tooset des points de terminaison sur une machine virtuelle Linux la classique dans Azure
Tous les ordinateurs virtuels Linux que vous créez dans Azure à l’aide du modèle de déploiement classique hello peuvent communiquer automatiquement via un canal réseau privé avec d’autres ordinateurs virtuels de hello que même service ou de réseau virtuel de cloud. Toutefois, les ordinateurs sur hello Internet ou d’autres réseaux virtuels nécessitent des points de terminaison toodirect hello réseau entrant trafic tooa machine virtuelle. Cet article est également disponible pour les [machines virtuelles Windows](../../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

> [!IMPORTANT]
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md). Cet article décrit à l’aide du modèle de déploiement classique hello. Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.

Bonjour **le Gestionnaire de ressources** modèle de déploiement, points de terminaison sont configurés à l’aide de **groupes de sécurité réseau (NSG)**. Pour plus d’informations, consultez la page [Ouverture des ports et des points de terminaison](../nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Lorsque vous créez une machine virtuelle Linux Bonjour portail Azure, un point de terminaison pour SSH (Secure Shell) est généralement créé pour vous automatiquement. Vous pouvez configurer des points de terminaison supplémentaires lors de la création d’ordinateur virtuel de hello ou par la suite si nécessaire.

[!INCLUDE [virtual-machines-common-classic-setup-endpoints](../../../../includes/virtual-machines-common-classic-setup-endpoints.md)]

## <a name="next-steps"></a>Étapes suivantes
* Vous pouvez également créer un point de terminaison de machine virtuelle à l’aide de hello [Interface de ligne de commande Azure](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2). Exécutez hello **créer de point de terminaison de machine virtuelle azure** commande.
* Si vous avez créé une machine virtuelle dans le modèle de déploiement du Gestionnaire de ressources hello, vous pouvez utiliser hello CLI d’Azure en mode de gestionnaire de ressources trop[créer des groupes de sécurité réseau](../../../virtual-network/virtual-networks-create-nsg-arm-cli.md) toocontrol trafic toohello machine virtuelle.
