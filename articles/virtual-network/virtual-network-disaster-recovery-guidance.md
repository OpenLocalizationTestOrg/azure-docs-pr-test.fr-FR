---
title: "toodo aaaWhat dans les cas de hello d’une interruption de service Azure ayant un impact sur les réseaux virtuels Azure | Documents Microsoft"
description: "Découvrez quels toodo dans les cas de hello d’une interruption de service Azure ayant un impact sur les réseaux virtuels Azure."
services: virtual-network
documentationcenter: 
author: NarayanAnnamalai
manager: jefco
editor: 
ms.assetid: ad260ab9-d873-43b3-8896-f9a1db9858a5
ms.service: virtual-network
ms.workload: virtual-network
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2016
ms.author: narayan;aglick
ms.openlocfilehash: db022d2a042d255cf8ec6afb68cd8436aeecfe08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-network--business-continuity"></a>Réseau virtuel – Continuité des activités
## <a name="overview"></a>Vue d'ensemble
Un réseau virtuel (VNet) est une représentation logique de votre réseau dans le cloud de hello. Il vous permet de toodefine votre propre hello espace et du segment de l’adresse IP de privé du réseau en sous-réseaux. Réseaux virtuels sert un toohost de limite d’approbation de vos ressources de calcul tels que des Machines virtuelles Azure et les Services de cloud computing (rôles web/de travail). Un réseau virtuel permet une communication IP privée directe entre les ressources hello qu’elle contient. Un réseau virtuel peut également être réseau local de tooan lié via une des options de hybride hello telles que la passerelle du VPN ou ExpressRoute.

Un réseau virtuel est créé dans l’étendue de hello d’une région. Vous pouvez créer des réseaux virtuels avec le même espace d’adressage dans deux régions différentes (par exemple, États-Unis et région ouest des États-Unis, mais il est impossible de se connecter les tooone directement). 

## <a name="business-continuity"></a>Continuité des activités
Peut-être que votre application peut être interrompue de différentes manières. Une région donnée peut être entièrement coupée en raison d’une catastrophe naturelle tooa ou d’une catastrophe partielle en raison de l’échec de tooa de plusieurs dispositifs/services. impact de Hello sur hello service de réseau virtuel est différent dans chacune de ces situations.

**Q : que faire en cas de hello d’une région entière de panne tooan ? par exemple, si une région est complètement coupure en raison d’une catastrophe naturelle tooa ? Que passe-t-il toohello réseaux virtuels hébergés dans la région de hello ?**

R : hello virtuel réseau et hello ressources Bonjour affectées reste région inaccessible pendant la durée hello d’interruption de service hello.

![Diagramme de réseau virtuel simple](./media/virtual-network-disaster-recovery-guidance/vnet.png)

**Q : que puis-je toodo recréer hello même réseau virtuel dans une autre région ?**

R : un réseau virtuel est une ressource relativement légère. Vous pouvez appeler des API Azure toocreate un réseau virtuel avec hello même espace d’adressage dans une autre région. toore-créer hello même environnement était présent dans hello affectées région, vous avez toomake API appels toore-déployer vos Services de cloud computing (rôles web/de travail) et les Machines virtuelles que vous aviez. Vous devez également toospin configurer une passerelle VPN et de connexion de réseau local de tooyour si vous aviez connectivité locale (par exemple, dans un déploiement hybride).

instructions Hello pour créer un réseau virtuel sont trouvent [ici](virtual-networks-create-vnet-arm-pportal.md). 

**Q: un réplica d’un réseau virtuel dans une région donnée peut-il être recréé dans une autre région à l’avance ?**

R : Oui, vous pouvez créer deux des réseaux virtuels à l’aide de hello espace d’adressage même IP privée et l’heure de ressources dans les deux régions différentes avance par rapport. Si un client a été hébergement internet faisant face à des services Bonjour réseau virtuel, ils pourraient avoir configuré la région toohello toogeo de Traffic Manager-route le trafic qui est active. Toutefois, un client ne peut pas se connecter à deux réseaux virtuels par hello même adresse réseau local de tootheir espace sous peine de causer des problèmes de routage. Au moment de hello d’un incident et la perte d’un réseau virtuel dans une région, un client peut se connecter hello autre réseau virtuel dans la région de disponible de hello avec le réseau local de correspondance adresse espace tootheir.

instructions Hello pour créer un réseau virtuel sont trouvent [ici](virtual-networks-create-vnet-arm-pportal.md).

