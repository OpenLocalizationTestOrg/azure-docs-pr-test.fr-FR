---
title: "aaaEnabling fin tooend SSL sur la passerelle d’Application Azure | Documents Microsoft"
description: "Cette page fournit une vue d’ensemble de tooend de fin de passerelle d’Application hello prennent en charge de SSL."
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: amsriva
ms.assetid: 3976399b-25ad-45eb-8eb3-fdb736a598c5
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: amsriva
ms.openlocfilehash: c5cb398a1e7d9a08662a3120baad98edb5575917
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-end-tooend-ssl-with-application-gateway"></a>Vue d’ensemble de fin tooend SSL avec la passerelle d’Application

Passerelle d’application prend en charge la terminaison SSL au niveau de la passerelle de hello, une fois que le trafic qui transite généralement serveurs principaux de toohello un format non chiffré. Cette fonctionnalité permet toobe de serveurs web unburdened à partir de la surcharge de chiffrement et déchiffrement coûteux. Cependant pour certains clients serveurs de communication non chiffrés toohello principaux n’est pas une option acceptable. Cette communication non chiffrée peut être dû à toosecurity spécifications, les exigences de conformité, ou application hello peut accepter seulement une connexion sécurisée. Pour de telles applications, la passerelle d’application prend en charge fin tooend SSL chiffrement.

## <a name="overview"></a>Vue d'ensemble

Vous permet de fin tooend SSL toosecurely transmettre back-end du toohello des données sensibles chiffrée pendant que toujours tirer parti des avantages de hello de fonctionnalités d’équilibrage de charge de couche 7 de passerelle d’application fournit. Certaines de ces fonctionnalités sont l’affinité de basé sur cookie de session, le routage basé sur une URL, prise en charge pour le routage basé sur des sites ou capacité tooinject X - transféré-* en-têtes.

Configuré avec le mode de communication SSL fin tooend, lors de la passerelle d’application met fin à des sessions SSL hello au niveau de passerelle hello et déchiffre le trafic des utilisateurs. Il applique ensuite tooselect de règles hello configuré un serveur principal approprié pool instance tooroute le trafic. Passerelle d’application puis initie un nouveau serveur de back-end du toohello connexion SSL et rechiffre les données à l’aide du certificat de clé publique du serveur hello principal avant de les transmettre hello demande toohello principal. Tooend fin que SSL est activé en définissant le paramètre de protocole dans tooHTTPS BackendHTTPSetting, qui est ensuite appliqué pool principal de tooa. Chaque serveur principal dans le pool de principal de hello avec tooend fin que SSL activé doit être configuré avec une communication sécurisée tooallow de certificat.

![scénario de fin tooend ssl][1]

Dans cet exemple, les demandes à l’aide de TLS 1.2 sont des serveurs toobackend routé dans Pool1 à l’aide de fin tooend SSL.

## <a name="end-tooend-ssl-and-whitelisting-of-certificates"></a>Fin tooend SSL et création de listes de certificats autorisées

Passerelle d’application communique uniquement avec des instances de principal connus ayant dans la liste approuvée leur certificat avec la passerelle d’application hello. liste des tooenable approuvées de certificats, vous devez télécharger hello de clé publique passerelle d’application principal serveur certificats toohello (pas les certificats racine hello). Seules les connexions tooknown et dans la liste approuvée aux serveurs principaux sont autorisés puis. Hello restant les serveurs principaux entraîne une erreur de passerelle. Les certificats auto-signés sont uniquement destinés à des fins de test et ne sont pas recommandés pour les charges de travail de production. Ces certificats ont toobe dans la liste approuvée avec la passerelle d’application hello comme décrit dans les étapes précédentes avant de pouvoir être utilisés de hello.

## <a name="next-steps"></a>Étapes suivantes

Après avoir d’apprendre à fin tooend SSL, passez trop[activer fin tooend SSL sur la passerelle d’application](application-gateway-end-to-end-ssl-powershell.md) toocreate une passerelle d’application à l’aide de fin tooend SSL.

<!--Image references-->

[1]: ./media/application-gateway-backend-ssl/scenario.png
