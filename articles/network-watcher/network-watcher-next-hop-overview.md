---
title: "saut de toonext aaaIntroduction dans l’Observateur réseau de Azure | Documents Microsoft"
description: "Cette page fournit une vue d’ensemble de hello Observateur réseau capacité de tronçon suivante"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: febf7bca-e0b7-41d5-838f-a5a40ebc5aac
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 916af736d0d52abadeafed746f0f8a0173b11033
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toonext-hop-in-azure-network-watcher"></a>Saut de toonext de présentation dans l’Observateur réseau de Azure

Le trafic à partir d’une machine virtuelle est envoyé à destination tooa selon les itinéraires effectifs hello associés à une carte réseau. Tronçon suivant obtient les type de tronçon suivant hello et l’adresse IP d’un paquet à partir d’un ordinateur virtuel spécifique et la carte réseau. Cela permet de toodetermine si hello paquet est dirigée toohello destination ou est dipositif de trafic hello est noir. Une mauvaise configuration des itinéraires par utilisateur hello, où un trafic est dirigé tooan local emplacement ou un équipement virtuel, peut entraîner des problèmes de tooconnectivity. Tronçon suivant retourne également la table d’itinéraires hello associée saut suivant de hello. Lorsque vous interrogez un tronçon suivant si l’itinéraire de hello est défini comme un itinéraire défini par l’utilisateur, cet itinéraire est retourné. Sinon, le tronçon suivant renvoie « Itinéraire du système ».

![vue d’ensemble du tronçon suivant][1]

Hello Voici une liste de hello types de tronçon suivant qui peuvent être retournées lors de l’interrogation de tronçon suivant.

* Internet
* VirtualAppliance
* VirtualNetworkGateway
* VnetLocal
* HyperNetGateway
* VnetPeering
* Aucun

### <a name="next-steps"></a>Étapes suivantes

Découvrez comment toofind de tronçon suivant toouse problèmes de connectivité de réseau en vous rendant sur [saut suivant de vérification hello sur une machine virtuelle](network-watcher-check-next-hop-portal.md)

<!--Image references-->
[1]: ./media/network-watcher-next-hop-overview/figure1.png













