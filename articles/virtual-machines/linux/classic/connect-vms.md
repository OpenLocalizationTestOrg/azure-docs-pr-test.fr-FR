---
title: aaaConnect les machines virtuelles Linux dans un service cloud | Documents Microsoft
description: "Connecter des ordinateurs virtuels Linux créés avec tooan de modèle de déploiement classique hello service cloud Azure ou de réseau virtuel."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 2fd23055-6b34-4ef0-88a8-fc19e32fb3c9
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: cynthn
ms.openlocfilehash: 323baf04390d53ffb2810e24a24d175c08e60cd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-linux-virtual-machines-created-with-hello-classic-deployment-model-with-a-virtual-network-or-cloud-service"></a>Connecter des ordinateurs virtuels Linux créés avec le modèle de déploiement classique hello avec un service cloud ou réseau virtuel
> [!IMPORTANT]
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md). Cet article décrit à l’aide du modèle de déploiement classique hello. Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.

Machines virtuelles Linux créés avec le modèle de déploiement classique de hello sont toujours placées dans un service cloud. service de cloud computing Hello agit comme un conteneur et fournit un nom DNS public unique, une adresse IP publique et un ensemble de la machine virtuelle de points de terminaison tooaccess hello sur hello Internet. service de cloud computing Hello peut être dans un réseau virtuel, mais qui n’est pas obligatoire. Vous pouvez également [connecter des machines virtuelles Windows à un réseau virtuel ou à un service cloud](../../windows/classic/connect-vms.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

Si un service cloud n’est pas dans un réseau virtuel, il est nommé « service cloud *autonome* ». machines virtuelles de Hello dans un service de cloud autonome communiquer avec d’autres ordinateurs virtuels à l’aide de hello les noms DNS publics des autres machines virtuelles et hello transitent sur hello Internet. Si un service cloud est dans un réseau virtuel, les machines virtuelles de hello, dans la mesure où le service cloud peut communiquer avec tous les autres ordinateurs virtuels dans le réseau virtuel de hello sans envoyer tout le trafic sur Internet de hello.

Si vous placez vos machines virtuelles dans hello même service de cloud computing autonome, vous pouvez toujours utiliser l’équilibrage de charge et haute disponibilité. Pour plus d’informations, consultez [machines virtuelles d’équilibrage de la charge](../../virtual-machines-linux-load-balance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) et [gérer la disponibilité hello des machines virtuelles](../manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Toutefois, vous ne peut pas organiser les ordinateurs virtuels de hello sur des sous-réseaux ou connecter un réseau local de tooyour autonome cloud service. Voici un exemple :

[!INCLUDE [virtual-machines-common-classic-connect-vms](../../../../includes/virtual-machines-common-classic-connect-vms.md)]

## <a name="next-steps"></a>Étapes suivantes
Après avoir créé une machine virtuelle, il est judicieux de trop[ajouter un disque de données](attach-disk.md) pour vos services et les charges de travail ont une données toostore d’emplacement.
