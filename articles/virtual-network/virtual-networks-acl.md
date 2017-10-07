---
title: "aaaWhat est une liste de contrôle d’accès réseau Azure ?"
description: "En savoir plus sur les listes de contrôle d’accès dans Azure"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 83d66c84-8f6b-4388-8767-cd2de3e72d76
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: a2681af035d162362771e6df9864bbe838f16352
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-an-endpoint-access-control-list"></a>Qu’est-ce qu’une liste de contrôle d’accès de point de terminaison ?

> [!IMPORTANT]
> Azure dispose de deux [modèles de déploiement](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) différents pour créer et utiliser des ressources : Resource Manager et classique. Cet article décrit à l’aide du modèle de déploiement classique hello. Microsoft recommande que la plupart des nouveaux déploiements de modèle de déploiement du Gestionnaire de ressources hello. 

Une liste de contrôle d’accès de point de terminaison (ACL) est une amélioration de sécurité disponible pour votre déploiement Azure. Une liste ACL fournit hello capacité tooselectively autoriser ou refuser le trafic pour un point de terminaison de machine virtuelle. Cette capacité de filtrage des paquets offre une couche de sécurité supplémentaire. Vous ne pouvez spécifier des listes de contrôle d’accès réseau que pour les points de terminaison. Vous ne pouvez pas spécifier de liste ACL pour un réseau virtuel ou un sous-réseau spécifique contenu dans un réseau virtuel. Il est recommandé de toouse groupes de sécurité réseau (NSG) au lieu de l’ACL, chaque fois que possible. toolearn en savoir plus sur les groupes de sécurité réseau, consultez [vue d’ensemble du groupe de sécurité réseau](virtual-networks-nsg.md)

ACL peuvent être configurés à l’aide de PowerShell ou hello portail Azure. tooconfigure un ACL réseau à l’aide de PowerShell, consultez [liste de contrôle d’accès de gestion des points de terminaison à l’aide de PowerShell](virtual-networks-acl-powershell.md). un liste ACL réseau à l’aide de tooconfigure hello Azure portail, consultez [comment tooset des points de terminaison tooa virtuels](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

ACL réseau, vous pouvez effectuer les suivant hello :

* Autoriser ou refuser le trafic entrant, basé sur le sous-réseau distant IPv4 adresse plage tooa machine virtuelle d’entrée point de terminaison de manière sélective.
* Bloquer certaines adresses IP.
* Créer plusieurs règles par point de terminaison de machine virtuelle.
* Utiliser la règle classement hello tooensure correct d’ensemble de règles sont appliquées à un point de terminaison de machine virtuelle spécifique (la plus basse toohighest)
* Spécifier une liste ACL pour une adresse IPv4 spécifique du sous-réseau distant.

Consultez hello [Azure limite](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#networking-limits) article pour les limites de la liste ACL.

## <a name="how-acls-work"></a>Fonctionnement des listes ACL
Une liste ACL est un objet qui contient une liste de règles. Lorsque vous créez une liste ACL et appliquez le point de terminaison de machine virtuelle tooa, le filtrage de paquets a lieu sur le nœud d’hôte hello de votre machine virtuelle. Cela signifie que le trafic de hello des adresses IP distantes est filtré par les règles ACL correspondants à la place de sur votre machine virtuelle sur le nœud hôte hello. Cela empêche votre machine virtuelle dépense des cycles UC de hello sur le filtrage des paquets.

Lorsqu’un ordinateur virtuel est créé, une ACL par défaut est placé dans un endroit tooblock tout le trafic entrant. Toutefois, si un point de terminaison est créé (port 3389), puis hello par défaut QU'ACL est modifié tooallow tout le trafic entrant pour ce point de terminaison. Le trafic entrant à partir de n’importe quel sous-réseau distant est ensuite autorisé toothat le point de terminaison et aucun approvisionnement de pare-feu n’est requise. Tous les autres ports sont bloqués pour le trafic entrant, sauf si des points de terminaison sont créés pour ces ports. Le trafic sortant est autorisé par défaut.

**Exemple de table de listes ACL par défaut**

| **N° de règle** | **Sous-réseau distant** | **Point de terminaison** | **Permit/Deny** |
| --- | --- | --- | --- |
| 100 |0.0.0.0/0 |3389 |Permit |

## <a name="permit-and-deny"></a>Permit et Deny
Vous pouvez autoriser ou refuser le trafic réseau de manière sélective pour un point de terminaison d’entrée de machine virtuelle en créant des règles qui spécifient « Permit » ou « Deny ». Il est important toonote que par défaut, lorsqu’un point de terminaison est créé, tout le trafic est autorisé toohello le point de terminaison. Pour cette raison, il est important de toounderstand toocreate/refus des règles et les placer dans l’ordre approprié de hello de priorité si vous souhaitez un contrôle précis sur le réseau de hello du trafic qui vous choisissez de terminaison de machine virtuelle tooallow tooreach hello.

Points tooconsider :

1. **Pas de liste ACL –** par défaut lorsqu’un point de terminaison est créé, nous autoriser tout du point de terminaison hello.
2. **Permit** : quand vous ajoutez une ou plusieurs plages « Permit », vous refusez toutes les autres plages par défaut. Seuls les paquets hello autorisée plage d’adresses IP seront en mesure de toocommunicate avec le point de terminaison de machine virtuelle hello.
3. **Deny** : quand vous ajoutez une ou plusieurs plages « Deny », vous autorisez toutes les autres plages de trafic par défaut.
4. **Combinaison d’autoriser et refuser -** vous pouvez utiliser une combinaison de « autoriser » et « refuser » lorsque vous souhaitez toocarve à une adresse IP spécifique de plage toobe autorisé ou refusé.

## <a name="rules-and-rule-precedence"></a>Règles et priorité des règles
Les listes de contrôle d’accès réseau peuvent être configurées sur des points de terminaison de machine virtuelle spécifiques. Par exemple, vous pouvez spécifier une liste de contrôle d’accès réseau pour un point de terminaison RDP créé sur une machine virtuelle qui verrouille l’accès de certaines adresses IP. Hello tableau ci-dessous montre un toopublic de l’accès de façon toogrant adresses IP virtuelles (VIP) d’un accès toopermit plage certaines pour RDP. Toutes les autres adresses IP distantes sont refusées. Nous suivons un ordre de règles qui donne la *priorité à la plus basse* .

### <a name="multiple-rules"></a>Plusieurs règles
Dans l’exemple hello ci-dessous, si vous souhaitez que le point de terminaison RDP tooallow pour accès toohello uniquement à partir de deux IPv4 plages d’adresses publiques (65.0.0.0/8 et 159.0.0.0/8), vous pouvez y parvenir en spécifiant deux *autoriser* règles. Dans ce cas, étant donné que RDP est créé par défaut pour un ordinateur virtuel, vous souhaiterez toolock accès toohello RDP port basé sur un sous-réseau distant vers le bas. Hello exemple ci-dessous montre un toopublic de l’accès de façon toogrant adresses IP virtuelles (VIP) d’un accès toopermit plage certaines pour RDP. Toutes les autres adresses IP distantes sont refusées. Cela fonctionne, car les listes de contrôle d’accès réseau permettent de configurer un point de terminaison de machine virtuelle spécifique et l’accès est refusé par défaut.

**Exemple - Plusieurs règles**

| **N° de règle** | **Sous-réseau distant** | **Point de terminaison** | **Permit/Deny** |
| --- | --- | --- | --- |
| 100 |65.0.0.0/8 |3389 |Permit |
| 200 |159.0.0.0/8 |3389 |Permit |

### <a name="rule-order"></a>Ordre des règles
Étant donné que plusieurs règles peuvent être spécifiés pour un point de terminaison, toodetermine commande quelle règle est prioritaire doit être un tooorganize des règles de façon. ordre de la règle Hello indique la priorité. Les listes de contrôle d’accès réseau suivent un ordre de règles qui donne la *priorité à la plus basse* . Dans l’exemple hello ci-dessous, point de terminaison hello sur le port 80 est accordé sélectivement accès tooonly certaines plages d’adresses IP. tooconfigure, nous avons une règle de refus (règle \# 100) pour les adresses dans un espace 175.1.0.1/24 hello. Une deuxième règle est ensuite spécifiée avec la priorité 200 qui permet d’accéder tooall autres adresses sous 175.0.0.0/8.

**Exemple - Priorité des règles**

| **N° de règle** | **Sous-réseau distant** | **Point de terminaison** | **Permit/Deny** |
| --- | --- | --- | --- |
| 100 |175.1.0.1/24 |80 |Deny |
| 200 |175.0.0.0/8 |80 |Permit |

## <a name="network-acls-and-load-balanced-sets"></a>Listes de contrôle d’accès réseau et jeux d’équilibrage de la charge
Les listes de contrôle d’accès réseau peuvent être spécifiées sur un point de terminaison de jeu d’équilibrage de la charge. Si une liste ACL est spécifiée pour un jeu d’équilibrage de charge, le réseau de hello ACL est virtuels tooall appliqué dans le jeu d’équilibrage de charge. Par exemple, si un jeu d’équilibrage de charge est créé avec le « Port 80 » et le jeu d’équilibrage hello contient 3 machines virtuelles, réseau hello ACL créé sur le point de terminaison « Port 80 », d’une que machine virtuelle est automatiquement appliquer toohello autres machines virtuelles.

![Listes de contrôle d’accès réseau et jeux d’équilibrage de la charge](./media/virtual-networks-acl/IC674733.png)

## <a name="next-steps"></a>Étapes suivantes
[Gérer les listes de contrôle d’accès pour les points de terminaison à l’aide de PowerShell](virtual-networks-acl-powershell.md)

