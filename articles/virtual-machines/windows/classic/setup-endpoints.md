---
title: aaaSet des points de terminaison sur une machine virtuelle Windows classique | Documents Microsoft
description: En savoir plus tooset des points de terminaison pour une machine virtuelle Windows dans hello tooallow de portail classique Azure communication avec un ordinateur virtuel de Windows dans Azure.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 8afc21c2-d3fb-43a3-acce-aa06be448bb6
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: cynthn
ms.openlocfilehash: e817076f16d3a245a8d19add7b2f2cf5e3baa17e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-up-endpoints-on-a-classic-windows-virtual-machine-in-azure"></a>Comment tooset des points de terminaison sur un ordinateur de virtuel Windows classique dans Azure
Toutes les fenêtres de machines virtuelles que vous créez dans Azure à l’aide du modèle de déploiement classique hello peuvent communiquer automatiquement via un canal réseau privé avec d’autres ordinateurs virtuels de hello même service cloud ou réseau virtuel. Toutefois, les ordinateurs sur hello Internet ou d’autres réseaux virtuels nécessitent des points de terminaison toodirect hello réseau entrant trafic tooa machine virtuelle. Cet article est également disponible pour les [machines virtuelles Linux](../../linux/classic/setup-endpoints.md).

> [!IMPORTANT]
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md). Cet article décrit à l’aide du modèle de déploiement classique hello. Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.

Bonjour **le Gestionnaire de ressources** modèle de déploiement, points de terminaison sont configurés à l’aide de **groupes de sécurité réseau (NSG)**. Pour plus d’informations, consultez [autoriser un accès externe tooyour machine virtuelle en utilisant hello Azure portal](../nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Lorsque vous créez une machine virtuelle Windows dans hello portail Azure, des points de terminaison courantes telles que celles pour le Bureau à distance et accès distant Windows PowerShell sont généralement créées pour vous automatiquement. Vous pouvez configurer des points de terminaison supplémentaires lors de la création d’ordinateur virtuel de hello ou par la suite si nécessaire.

[!INCLUDE [virtual-machines-common-classic-setup-endpoints](../../../../includes/virtual-machines-common-classic-setup-endpoints.md)]

## <a name="next-steps"></a>Étapes suivantes
* toouse un tooset d’applet de commande Azure PowerShell du point de terminaison de la machine virtuelle, consultez [Add-AzureEndpoint](https://msdn.microsoft.com/library/azure/dn495300.aspx).
* toouse un toomanage d’applet de commande Azure PowerShell une ACL sur un point de terminaison, consultez [contrôle d’accès de gestion des listes (ACL) pour les points de terminaison à l’aide de PowerShell](../../../virtual-network/virtual-networks-acl-powershell.md).
* Si vous avez créé une machine virtuelle dans le modèle de déploiement du Gestionnaire de ressources hello, vous pouvez utiliser Azure PowerShell trop[créer des groupes de sécurité réseau](../../../virtual-network/virtual-networks-create-nsg-arm-ps.md) toocontrol trafic toohello machine virtuelle.
