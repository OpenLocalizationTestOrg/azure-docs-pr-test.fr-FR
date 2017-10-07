---
title: "aaaThreats - outil de modélisation des menaces Microsoft - Azure | Documents Microsoft"
description: "Page de catégorie de menace de hello outil de modélisation de menace de Microsoft, contenant des catégories pour tous les exposés généré menaces."
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 0bd51f81370b6385ff1ac9769e34fc089e1dfc9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-threat-modeling-tool-threats"></a>Menaces de l’outil Microsoft de modélisation des menaces

Hello, outil de modélisation des menaces est un élément essentiel du hello du cycle de vie de développement de sécurité Microsoft (SDL). Il permet aux logiciels architectes tooidentify et d’atténuer les problèmes de sécurité potentiels au plus tôt, lorsqu’ils sont relativement facile et plus économique tooresolve. Par conséquent, il réduit considérablement les coût total de hello du développement. En outre, nous avons conçu outil de hello avec des experts de sécurité à l’esprit, facilitant la modélisation des menaces pour tous les développeurs en fournissant des indications précises sur la création et l’analyse des modèles de menace.

> Visitez hello  **[outil de modélisation des menaces](./azure-security-threat-modeling-tool.md)**  tooget dès aujourd'hui !

Hello, outil de modélisation des menaces vous aident à répondre à certaines questions, par exemple hello ceux présentés ci-dessous :

* Comment un attaquant peut modifier les données d’authentification hello ?
* Qu’est impact de hello si une personne malveillante peut lire les données de profil utilisateur hello ?
* Que se passe-t-il si l’accès est refusé à base de données de profil toohello utilisateur ?

## <a name="stride-model"></a>Modèle STRIDE

aide toobetter vous formulez ces types de questions, Microsoft utilise hello modèle STRIDE, qui classe les différents types de menaces et simplifie hello des conversations de sécurité globale.

| Catégorie | Description |
| -------- | ----------- |
| **Usurpation d’identité** | Implique l’accès illégal aux informations d’authentification d’un autre utilisateur, comme le nom d’utilisateur et le mot de passe, ainsi que leur utilisation |
| **Falsification** | Implique la modification malveillante de hello de données. Exemples de modifications non autorisées de données toopersistent, telles que celles contenues dans une base de données et une altération hello de données circulant entre deux ordinateurs sur un réseau ouvert, par exemple hello Internet |
| **Répudiation** | Associées aux utilisateurs qui a effectué une action sans que tooprove de toute façon dans le cas contraire, par exemple, un utilisateur effectue une opération non autorisée dans un système qui ne dispose pas des opérations de hello capacité tootrace hello interdite. Non répudiation fait référence à capacité toohello un menaces de répudiation toocounter système. Par exemple, un utilisateur qui achète un élément peut-être toosign pour élément hello lors de la réception. fournisseur de Hello peut ensuite utiliser hello signé accusé de réception en tant que preuve que l’utilisateur hello n’a reçu le package de hello |
| **Divulgation d’informations** | Comprend une exposition hello de tooindividuals informations qui ne sont pas censés toohave accès tooit — par exemple, capacité hello utilisateurs tooread un fichier qu’ils n’étaient pas accès à ou hello capacité d’un tooread de données intrus en transit entre deux ordinateurs |
| **Déni de service** | Refus de service (DoS) refuser les utilisateurs des services toovalid — par exemple, en effectuant un serveur Web temporairement indisponible ou inutilisable. Vous devez protéger contre certains types de déni de service menaces simplement tooimprove système disponibilité et fiabilité |
| **Élévation de privilège** | Un utilisateur non privilégié accès privilégié et ce qui a toocompromise d’accès suffisantes ou détruire hello tout système. Élévation des menaces pour le privilège incluent les situations dans lesquelles une personne malveillante a effectivement pénétré toutes les défenses du système et font partie du système hello approuvé lui-même, une situation dangereuse en effet |

## <a name="next-steps"></a>Étapes suivantes

Passez trop**[atténuation outil de modélisation de menace](./azure-security-threat-modeling-tool-mitigations.md)**  toolearn hello façons vous pouvez atténuer ces menaces avec Azure.
