---
title: "intégration de la passerelle avec Azure Security Center d’aaaApplication | Documents Microsoft"
description: "Cette page fournit des informations sur l’intégration d’Application Gateway à Azure Security Center."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: 
ms.assetid: e5ea5cf9-3b41-4b85-a12c-e758bff7f3ec
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: 
ms.workload: infrastructure-services
ms.date: 06/07/2017
ms.author: gwallace
ms.openlocfilehash: 6f6ace105e84c01f525ab02938e81ce040c5c9d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-integration-between-application-gateway-and-azure-security-center"></a>Vue d’ensemble de l’intégration entre Application Gateway et Azure Security Center

Découvrez comment Application Gateway et Azure Security Center protègent vos ressources d’application web. Pare-feu d’applications web application gateway (WAF) s’intègre à [centre de sécurité](../security-center/security-center-intro.md) tooprovide tooprevent une vue claire, détecter et traiter des toothreats toounprotected les applications web dans votre environnement.

## <a name="overview"></a>Vue d'ensemble

Le WAF d’Application Gateway est une recommandation du Security Center visant à protéger les applications web des failles de sécurité et des vulnérabilités. Les ressources Web activée qui ne sont pas protégés par WAF affichent dans le centre de sécurité hello sous forme de recommandations de gravité élevée. Recommandations pour les pare-feu d’applications web sont affichées sur hello **vue d’ensemble** sous **Applications**.

![Intégration au centre de sécurité][1]

Cliquez sur les recommandations concernant les pare-feu d’applications web pour ouvrir un nouveau panneau présentant les détails de hello de recommandation de hello.

## <a name="add-a-web-application-firewall-tooan-existing-resource"></a>Ajouter une ressource web application pare-feu tooan existant

Accédez trop**plus Services** > **sécurité + identité** > **centre de sécurité** et hello **centre de sécurité - vue d’ensemble**  panneau, cliquez sur **Applications**. Sur hello **centre de sécurité - Applications** panneau, table de hello contient une liste d’applications centre de sécurité a détecté dans votre abonnement.

![applications web][3]

En cliquant sur une application web avec un problème critique, vous obtenez hello **intégrité de la sécurité Application** panneau. Dans l’image hello ci-dessous, hello application web qui n’est pas protégée par un pare-feu d’applications web. 

![ressources web non protégées][2]

Cliquez sur **ajouter un pare-feu d’applications web** sous **recommandations** tooopen hello **ajouter un pare-feu d’applications Web** panneau.

Si vous n’ont pas une passerelle d’Application existant, ou souhaitez toocreate un nouveau, cliquez sur **créer un nouveau** et hello **créer un nouveau pare-feu d’applications Web** panneau, puis cliquez sur **Microsoft - Passerelle d’application**. Vous accédez via hello étapes toocreate une passerelle d’application. À ce stade, votre application web est ajoutée sous forme de ressource protégée. Security Center effectue désormais le suivi de protection par un pare-feu d’applications web de cette ressource. Cela n’a pas pour effet de l’ajouter comme membre du pool principal.

S’il existe une passerelle d’application, vous pouvez la choisir sous **Utiliser la solution existante**

![panneau d’ajout de pare-feu d’applications web][4]

Ajout de qu'une passerelle d’application web application tooan via le centre de sécurité n’ajoute pas de ressource de hello en tant qu’un membre du pool principal, il est indispensable sur les ressources de passerelle d’application hello directement.

## <a name="add-a-resource-tooan-existing-web-application-firewall"></a>Ajouter un pare-feu d’applications web existantes ressource tooan

Accédez trop**plus Services** > **sécurité + identité** > **centre de sécurité** et hello **centre de sécurité - vue d’ensemble**  panneau, cliquez sur **solutions de partenaire**. Affichent les passerelles d’application prenant en charge le centre de sécurité existants dans hello **Solutions de partenaire** panneau.

![Solutions de partenaires][7]

Cliquez sur **lien application** tooopen hello **lien Applications** panneau, vous pouvez soit les applications existantes hello options tooselect ici. Choisissez hello applications tooprotect et cliquez sur **OK**. Cette méthode n’ajoute pas pool hello web application toohello principal de la passerelle d’application hello. Définit les ressources hello comme une ressource protégée afin de centre de sécurité peut le suivre. ressource de hello tooadd comme un membre du pool principal, ceci doit être fait sur la passerelle d’application hello, panneau actuel de hello vous pouvez cliquer sur **console de la Solution** toobe prise toohello ressource de passerelle d’application où vous pouvez ajouter le serveur web hello pool principal d’application toohello.

![applications de solutions de partenaires][6]

## <a name="finalize-configuration"></a>Finaliser la configuration

Les applications assure le suivi du centre de sécurité ajouté tooan passerelle d’application comme une ressource protégée.  Il surveille l’intégrité de hello de cette ressource et que vous permet de s’assurer qu’elle est protégée par une passerelle d’application. étape suivante de Hello est tooadd hello privé IP, adresse IP publique ou carte réseau de votre pool de back-end toohello machine virtuelle de passerelle d’application hello. Jusqu'à ce que cette opération est effectuée une recommandation supplémentaire de **finaliser la protection de l’application** est indiqué en tant que ressource de hello est ajoutée.

![panneau d’ajout de pare-feu d’applications web][5]

## <a name="security-alerts"></a>Alertes de sécurité

Dans le centre de sécurité accédez trop**détection** > **alertes de sécurité**.  Vous y trouverez des alertes WAF relatives aux passerelles de votre application. Les alertes sont réparties selon la règle WAF.

![alertes de sécurité][8]

Cliquez sur une règle pour fournir une liste des alertes relatives à cette règle WAF spécifique. Chaque alerte affiche des détails supplémentaires sur la recherche de hello. Détails de Hello fournissent une passerelle d’application toohello lien.
 
![détails de l’alerte][9]

## <a name="next-steps"></a>Étapes suivantes

toolearn comment tooenable pare-feu d’applications web sur une passerelle d’application existant, visitez [créer ou mettre à jour une passerelle d’Application Azure avec pare-feu d’applications web](application-gateway-web-application-firewall-portal.md#add-web-application-firewall-to-an-existing-application-gateway)

[1]: ./media/application-gateway-integration-security-center/figure1.png
[2]: ./media/application-gateway-integration-security-center/figure2.png
[3]: ./media/application-gateway-integration-security-center/figure3.png
[4]: ./media/application-gateway-integration-security-center/figure4.png
[5]: ./media/application-gateway-integration-security-center/figure5.png
[6]: ./media/application-gateway-integration-security-center/figure6.png
[7]: ./media/application-gateway-integration-security-center/figure7.png
[8]: ./media/application-gateway-integration-security-center/securitycenter.png
[9]: ./media/application-gateway-integration-security-center/figure9.png