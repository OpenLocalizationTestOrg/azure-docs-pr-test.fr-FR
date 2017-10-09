---
title: "flux de tooIP aaaIntroduction Vérifiez dans l’Observateur réseau de Azure | Documents Microsoft"
description: "Cette page fournit une vue d’ensemble de hello IP de l’Observateur réseau flux vérifier la capacité"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: d352fb2d-4b4f-4ac4-9c2e-1cfccf0e7e03
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: b648a4816a7ffdc6ca54462944b574e2395e8298
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooip-flow-verify-in-azure-network-watcher"></a>Flux de tooIP introduction Vérifiez dans l’Observateur réseau de Azure

Les flux IP vérifier si un paquet est autorisé ou refusé tooor à partir d’un ordinateur virtuel en fonction des informations de 5-tuple. Ces informations se composent de la direction, du protocole, de l’adresse IP locale, de l’adresse IP distante, du port local et du port distant. Si les paquets hello sont refusée par un groupe de sécurité, nom hello de règle hello refusé les paquets hello est retournée. Alors que toutes les adresses IP source ou de destination peut être choisie, cette fonctionnalité permet aux administrateurs de diagnostiquer rapidement les problèmes de connectivité à partir d’ou toohello internet et à partir d’ou l’environnement local de toohello.

La vérification des flux IP cible une interface réseau d’une machine virtuelle. Flux de trafic est ensuite vérifié selon tooor de paramètres hello configuré à partir de cette interface réseau. Cette fonctionnalité est utile pour confirmer si une règle dans un groupe de sécurité réseau bloque entrée ou sortie tooor le trafic à partir d’un ordinateur virtuel.

Une instance de l’Observateur réseau besoins toobe est créé dans toutes les régions que vous envisagez de flux d’IP toorun vérifier. L’Observateur réseau est un service régional et peut uniquement être exécuté sur les ressources Bonjour même région. Cela n’affecte pas hello résultats de flux de l’IP vérifier comme itinéraire hello associé hello que s’affichera toujours de carte réseau.

![1][1]

## <a name="next-steps"></a>Étapes suivantes

Visitez hello suivant article toolearn si un paquet est autorisé ou refusé pour un ordinateur virtuel spécifique via le portail de hello. [Vérifiez si le trafic est autorisé sur une machine virtuelle avec IP flux vérifier à l’aide du portail de hello](network-watcher-check-ip-flow-verify-portal.md)

[1]: ./media/network-watcher-ip-flow-verify-overview/figure1.png












