---
title: "mappage d’aaaNetwork entre deux régions Azure dans Azure Site Recovery | Documents Microsoft"
description: "Azure Site Recovery coordonne la réplication hello, le basculement et récupération des ordinateurs virtuels et des serveurs physiques. En savoir plus sur tooAzure de basculement ou un centre de données secondaire."
services: site-recovery
documentationcenter: 
author: prateek9us
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/11/2017
ms.author: pratshar
ms.openlocfilehash: 4f80c44e3f94eaf446bc01a7041d91fe34aa78d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="network-mapping-between-two-azure-regions"></a>Mappage réseau entre deux régions Azure


Cet article décrit comment toomap Azure des réseaux virtuels de deux régions Azure entre eux. Le mappage réseau garantit que lorsque l’ordinateur virtuel répliqué est créé dans la cible de hello région Azure, il est créé sur hello réseau virtuel réseau mappé toovirtual de machine virtuelle de hello source.  

## <a name="prerequisites"></a>Composants requis
Avant de mapper des réseaux, vérifiez que vous avez créé des [réseaux virtuels Azure](../virtual-network/virtual-networks-overview.md) dans les régions Azure source et cible.

## <a name="map-networks"></a>Mapper des réseaux

toomap un réseau virtuel Azure dans une région Azure tooanother réseau virtuel une autre région, accédez tooSite Infrastructure de récupération -> mappage de réseau (pour les Machines virtuelles Azure) et créer un mappage réseau.

![Mappage réseau](./media/site-recovery-network-mapping-azure-to-azure/network-mapping1.png)


Exemple ci-dessous ma machine virtuelle est en cours d’exécution dans la région Asie et est en cours hello répliquée tooSoutheast Asie.

Sélectionnez le réseau source et cible de hello et puis cliquez sur OK toocreate un mappage réseau à partir de l’Asie orientale tooSoutheast en Asie.

![Mappage réseau](./media/site-recovery-network-mapping-azure-to-azure/network-mapping2.png)


Hello même chose toocreate un mappage réseau à partir de l’Asie du Sud-est tooEast en Asie.  
![Mappage réseau](./media/site-recovery-network-mapping-azure-to-azure/network-mapping3.png)


## <a name="mapping-network-when-enabling-replication"></a>Mappage réseau lors de l’activation de la réplication

Si le mappage réseau n’est pas effectué lorsque vous répliquez une machine virtuelle pour hello première heure formulaire une région Azure tooanother, vous pouvez choisir réseau cible dans le cadre de hello même processus. Récupération de site crée des mappages de réseau à partir de la région de tootarget la région source et de région de toosource région cible en fonction de cette sélection.   

![Mappage réseau](./media/site-recovery-network-mapping-azure-to-azure/network-mapping4.png)

Par défaut, Site Recovery crée un réseau dans la région cible hello qui est identique toohello source réseau et en ajoutant «-asr » en tant que suffixe toohello nom de réseau de source de hello. Vous pouvez choisir un réseau déjà créé en cliquant sur Personnaliser.

![Mappage réseau](./media/site-recovery-network-mapping-azure-to-azure/network-mapping5.png)


Si le mappage réseau hello est déjà fait, vous ne pouvez pas modifier le réseau virtuel de hello cible lors de l’activation de la réplication. toochange, modifiez le mappage réseau existant.  

![Mappage réseau](./media/site-recovery-network-mapping-azure-to-azure/network-mapping6.png)

![Mappage réseau](./media/site-recovery-network-mapping-azure-to-azure/modify-network-mapping.png)

> [!IMPORTANT]
> Si vous modifiez un mappage de réseau à partir de la région-1 tooregion-2, assurez-vous que vous modifiez le mappage réseau hello de région-2 tooregion-1 ainsi.
>
>


## <a name="subnet-selection"></a>Sélection de sous-réseau
Sous-réseau de la machine virtuelle cible hello est sélectionné en fonction de nom hello du sous-réseau de hello d’ordinateur virtuel de hello source. S’il existe un sous-réseau de hello même nom que celui de l’ordinateur virtuel à source de hello disponible dans le réseau cible de hello, qui est choisi pour la machine virtuelle cible hello. S’il n’existe aucun sous-réseau ne porte hello même nom dans le réseau cible de hello, puis par ordre alphabétique premier sous-réseau est choisi comme hello sous-réseau cible. Vous pouvez modifier ce sous-réseau en accédant tooCompute et les paramètres réseau de l’ordinateur virtuel de hello.

![Modifier le sous-réseau](./media/site-recovery-network-mapping-azure-to-azure/modify-subnet.png)


## <a name="ip-address"></a>Adresse IP

Adresse IP pour chaque interface de réseau hello de la machine virtuelle cible hello est choisi comme suit :

### <a name="dhcp"></a>DHCP
Si l’interface de réseau hello de machine virtuelle de hello source utilise le protocole DHCP, interface de réseau de la machine virtuelle cible hello est également définie en tant que DHCP.

### <a name="static-ip"></a>Adresse IP statique
Si l’interface de réseau hello de machine virtuelle de hello source utilise des adresses IP statiques, interface de réseau de la machine virtuelle cible hello est également défini toouse adresse IP statique. L’adresse IP statique est choisie comme suit :

#### <a name="same-address-space"></a>Même espace d’adressage

Si sous-réseau de hello source et de sous-réseau cible de hello ont hello même espace d’adressage, puis IP cible est identique à l’IP hello d’interface de réseau hello de machine virtuelle de hello source. Si la même adresse IP n’est pas disponible, une adresse IP disponible est définie en tant qu’adresse IP cible de hello.

#### <a name="different-address-space"></a>Espace d’adressage différent

Si le sous-réseau de source de hello et sous-réseau cible de hello ont l’espace d’adressage différent, adresse IP cible est définie comme une adresse IP disponible dans le sous-réseau de cible hello.

Vous pouvez modifier l’adresse IP cible de hello sur chaque interface réseau en accédant tooCompute et les paramètres réseau de l’ordinateur virtuel de hello.

## <a name="next-steps"></a>Étapes suivantes

- En savoir plus sur la [mise en réseau pour la réplication des machines virtuelles Azure](site-recovery-azure-to-azure-networking-guidance.md).
