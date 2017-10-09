---
title: "Mise en réseau Azure Stack : différences et considérations"
description: "Découvrez les différences et les éléments à prendre en compte lors de l’utilisation de la mise en réseau dans Azure Stack."
services: azure-stack
keywords: 
author: ScottNapolitan
ms.author: victorh
ms.date: 08/02/2017
ms.topic: article
ms.service: azure-stack
ms.openlocfilehash: 12a557d2d1184c2191683956e263558cc3a474b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="considerations-for-azure-stack-networking"></a>Considérations relatives à la mise en réseau Azure Stack

Mise en réseau dans la pile de Azure fournit les fonctionnalités de hello que vous trouvez dans Azure, avec quelques différences, que vous devez comprendre avant de commencer le déploiement.


Cet article fournit une vue d’ensemble de hello considérations spécifiques à la mise en réseau et de ses fonctionnalités dans la pile de Azure. toolearn sur les principales différences entre la pile d’Azure et d’Azure, consultez hello [considérations relatives à la clé](azure-stack-considerations.md) rubrique.


## <a name="cheat-sheet-networking-differences"></a>Aide-mémoire : différences de mise en réseau

|Service | Fonctionnalité | Azure (global) | Azure Stack |
| --- | --- | --- | --- |
| DNS | Système DNS multilocataire | Pris en charge| Pas encore pris en charge|
| |Enregistrements AAAA DNS|Pris en charge|Non pris en charge|
| |Zones DNS par abonnement|100 (par défaut)<br>Peut être augmenté à la demande.|100|
| |Jeux d’enregistrements DNS par zone|5000 (par défaut)<br>Peut être augmenté à la demande.|5 000|
||Serveurs de noms pour la délégation de zone|Azure fournit quatre serveurs de noms pour chaque zone utilisateur (locataire) créée.|Azure Stack fournit deux serveurs de noms pour chaque zone utilisateur (locataire) créée.|
| Réseau virtuel|Homologation de réseaux virtuels|Connecter deux réseaux virtuels Bonjour même région via le réseau d’Azure backbone hello.|Pas encore pris en charge|
| |Adresses IPv6|Vous pouvez affecter une adresse IPv6 dans le cadre de hello [Configuration de l’Interface réseau](https://docs.microsoft.com/en-us/azure/virtual-network/virtual-network-network-interface-addresses#ip-address-versions).|Seul le protocole IPv4 est pris en charge.|
|Passerelles VPN|Passerelle VPN de point à site|Pris en charge|Pas encore pris en charge|
| |Passerelle de réseau virtuel à réseau virtuel|Pris en charge|Pas encore pris en charge|
| |SKU de passerelle de réseau virtuel|Prise en charge de Basic, GW1, GW2, GW3, Standard High Performance, Ultra-High Performance. |Prise en charge des SKU Basic, Standard et High-Performance.|
|Équilibrage de charge|Adresses IP publiques IPv6|Équilibrage de charge de la prise en charge pour l’affectation d’un tooa d’adresse IP publique IPv6.|Seul le protocole IPv4 est pris en charge.|
|Network Watcher|Fonctionnalités de surveillance réseau de locataire Network Watcher|Pris en charge|Pas encore pris en charge|
|CDN|Profils de réseau de distribution de contenu (CDN)|Pris en charge|Pas encore pris en charge|
|Application Gateway|Équilibrage de charge de couche 7|Pris en charge|Pas encore pris en charge|
|Traffic Manager|Routage du trafic entrant pour une fiabilité et des performances d’application optimales.|Pris en charge|Pas encore pris en charge|
|ExpressRoute|Configurer les services en nuage tooMicrosoft une connexion privée rapide des installations d’infrastructure ou de la colocalisation sur site.|Pris en charge|Prise en charge pour la connexion de circuit Expressroute de tooan pile d’Azure.|

## <a name="next-steps"></a>Étapes suivantes

[DNS dans Azure Stack](azure-stack-dns.md)
