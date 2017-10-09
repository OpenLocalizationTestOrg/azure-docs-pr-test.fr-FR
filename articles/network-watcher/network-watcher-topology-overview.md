---
title: "tootopology aaaIntroduction dans l’Observateur réseau de Azure | Documents Microsoft"
description: "Cette page fournit une vue d’ensemble des fonctionnalités de topologie hello Observateur réseau"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e753a435-38e0-482b-846b-121cb547555c
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 7fa1c5518e4a25a5db999d898a9ee19fd0121db7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tootopology-in-azure-network-watcher"></a>Tootopology de présentation dans l’Observateur réseau de Azure

La topologie renvoie un graphique des ressources réseau figurant dans un réseau virtuel. graphique de Hello représente l’interconnexion hello entre la connectivité réseau de hello ressources toorepresent hello fin tooend.

![Vue d’ensemble de la topologie][1]

Dans le portail hello, topologie retourne des objets de ressource hello sur une base de réseau virtuel. relations de Hello sont représentées par des lignes entre les ressources de hello ressources en dehors de la région de hello Observateur réseau, même si dans la ressource de hello groupe s’afficheront pas. ressources Hello retournées dans la vue du portail hello sont un sous-ensemble de composants réseau hello qui sont représentés graphiquement. toosee hello la liste complète des ressources réseau, vous pouvez utiliser [PowerShell](network-watcher-topology-powershell.md) ou [REST](network-watcher-topology-rest.md)

> [!NOTE]
> Une instance de l’Observateur réseau est requis dans chaque région que vous voulez toorun topologie sur.

Comme les ressources sont retournées les connexion hello entre eux sont modélisés sous deux relations.

- **Imbrication** - Exemple : un réseau virtuel contient un sous-ensemble contenant une carte réseau.
- **Associé** - Exemple : une carte réseau est associée à une machine virtuelle.

### <a name="next-steps"></a>Étapes suivantes

Découvrez comment afficher les toouse PowerShell tooretrieve hello topologie en vous rendant sur [topologie de l’Observateur réseau avec PowerShell](network-watcher-topology-powershell.md)

<!--Image references-->

[1]: ./media/network-watcher-topology-overview/topology.png
