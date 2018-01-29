---
title: "Activation de groupes de sécurité réseau dans Azure Security Center | Microsoft Docs"
description: "Ce document vous montre comment implémenter la recommandation de l’Azure Security Center **Activer des groupes de sécurité réseau**."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: f53ed853-ffaf-4530-a019-1906ba6f341b
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 1e034d59d8847f237fa0d4c772344d45cd618576
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2017
---
# <a name="enable-network-security-groups-in-azure-security-center"></a>Activation de groupes de sécurité réseau dans Azure Security Center
Azure Security Center vous recommande d’activer un groupe de sécurité réseau si aucun n’est encore activé. Les groupes de sécurité réseau contiennent des règles de liste de contrôle d’accès qui autorisent ou rejettent le trafic réseau vers vos instances de machine virtuelle dans un réseau virtuel. Des groupes de sécurité réseau peuvent être associés à des sous-réseaux ou à des instances de machine virtuelle au sein de ce sous-réseau. Lorsqu’un groupe de sécurité réseau est associé à un sous-réseau, les règles ACL s’appliquent à toutes les instances de machine virtuelle présentes dans ce sous-réseau. En outre, le trafic vers un ordinateur virtuel individuel peut être limité par l’association d’un groupe de sécurité réseau directement à la machine virtuelle. Pour en savoir plus, consultez l’article [Présentation du groupe de sécurité réseau](../virtual-network/virtual-networks-nsg.md)

Si vous n’avez pas activé de groupe de sécurité réseau, Azure Security Center vous envoie deux recommandations : activer des groupes de sécurité réseau sur des sous-réseaux et activer des groupes de sécurité réseau sur des machines virtuelles. Vous choisissez à quel niveau, à quel sous-réseau ou à quelle machine virtuelle appliquer des groupes de sécurité réseau.

> [!NOTE]
> Ce document présente le service à l’aide d’un exemple de déploiement.  Il ne s’agit pas d’un guide pas à pas.
>
>

## <a name="implement-the-recommendation"></a>Implémenter la recommandation
1. Dans le panneau **Recommandations**, sélectionnez **Activer des groupes de sécurité réseau** sur des sous-réseaux ou des ordinateurs virtuels.
   ![Activer des groupes de sécurité réseau][1]
2. Le panneau **Configurer les groupes de sécurité réseau manquants** s’ouvre alors pour les sous-réseaux ou les machines virtuelles en fonction de la recommandation que vous avez sélectionnée. Sélectionnez un sous-réseau ou une machine virtuelle comme cible de la configuration d’un groupe de réseau virtuel.

   ![Configurer un groupe de sécurité réseau pour un sous-réseau][2]

   ![Configurer un groupe de sécurité réseau pour une machine virtuelle][3]
3. Dans le panneau **Choisir un groupe de sécurité réseau** , sélectionnez un groupe de sécurité réseau existant ou **Création** pour créer un groupe de sécurité réseau.

   ![Choisir un groupe de sécurité réseau][4]

Si vous créez un groupe de sécurité réseau, suivez les étapes indiquées dans l’article [Gestion des groupes de sécurité réseau à l’aide du portail Azure](../virtual-network/virtual-networks-create-nsg-arm-pportal.md) pour créer un groupe de sécurité et définir des règles de sécurité.

## <a name="see-also"></a>Voir aussi
Cet article vous a montré comment implémenter la recommandation de Security Center « Activer des groupes de sécurité réseau » pour des sous-réseaux ou des machines virtuelles. Pour plus d’informations sur l’activation de groupes de sécurité, consultez les rubriques suivantes :

* [Présentation du groupe de sécurité réseau](../virtual-network/virtual-networks-nsg.md)
* [Gestion des groupes de sécurité réseau à l’aide du portail Azure](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)

Pour plus d’informations sur le Centre de sécurité, consultez les rubriques suivantes :

* [Définition des stratégies de sécurité dans Azure Security Center](security-center-policies.md) : découvrez comment configurer des stratégies de sécurité pour vos groupes de ressources et abonnements Azure.
* [Gestion des recommandations de sécurité dans Azure Security Center](security-center-recommendations.md) : découvrez comment les recommandations peuvent vous aider à protéger vos ressources Azure.
* [Surveillance de l’intégrité de la sécurité dans Azure Security Center](security-center-monitoring.md) : découvrez comment surveiller l’intégrité de vos ressources Azure.
* [Gestion et résolution des alertes de sécurité dans Azure Security Center](security-center-managing-and-responding-alerts.md) : découvrez comment gérer et résoudre les alertes de sécurité.
* [Surveillance des solutions partenaires avec Azure Security Center](security-center-partner-solutions.md) : découvrez comment surveiller l’état d’intégrité de vos solutions partenaires.
* [FAQ sur Azure Security Center](security-center-faq.md) : forum aux questions concernant l’utilisation de ce service.
* [Blog sur la sécurité Azure](http://blogs.msdn.com/b/azuresecurity/) : découvrez les dernières nouvelles et informations sur la sécurité Azure.

<!--Image references-->
[1]: ./media/security-center-enable-nsg/enable-nsg.png
[2]:./media/security-center-enable-nsg/configure-nsg-for-subnet.png
[3]: ./media/security-center-enable-nsg/configure-nsg-for-vm.png
[4]: ./media/security-center-enable-nsg/choose-nsg.png
