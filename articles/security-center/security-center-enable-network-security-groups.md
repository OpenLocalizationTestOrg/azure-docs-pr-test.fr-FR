---
title: "aaaEnable des groupes de sécurité réseau dans le centre de sécurité Azure | Documents Microsoft"
description: "Ce document vous montre comment tooimplement hello recommandation du centre de sécurité Azure ** activer réseau sécurité groupes **."
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
ms.openlocfilehash: 2f70fe432aa452f833a5c322d13102ebbd6dbb69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-network-security-groups-in-azure-security-center"></a>Activation de groupes de sécurité réseau dans Azure Security Center
Azure Security Center vous recommande d’activer un groupe de sécurité réseau si aucun n’est encore activé. Groupes de sécurité réseau contient une liste de règles de liste de contrôle d’accès (ACL) qui autorisent ou refusent le trafic réseau tooyour des instances de machine virtuelle dans un réseau virtuel. Des groupes de sécurité réseau peuvent être associés à des sous-réseaux ou à des instances de machine virtuelle au sein de ce sous-réseau. Lorsqu’un groupe de sécurité réseau est associé à un sous-réseau, listes de contrôle hello appliquent instances de machine virtuelle tooall hello dans ce sous-réseau. En outre, le trafic tooan machine virtuelle individuelle peut être limité par l’association d’un groupe de sécurité réseau directement toothat machine virtuelle. Voir toolearn [qu’est un groupe de sécurité réseau (NSG) ?](../virtual-network/virtual-networks-nsg.md)

Si vous n’avez pas de groupes de sécurité réseau activés, le centre de sécurité présente deux recommandations tooyou : activer les groupes de sécurité réseau sur les sous-réseaux et activer les groupes de sécurité réseau sur les ordinateurs virtuels. Vous choisissez les niveau, le sous-réseau ou la machine virtuelle, tooapply groupes de sécurité réseau.

> [!NOTE]
> Ce document présente le service de hello à l’aide d’un exemple de déploiement.  Il ne s’agit pas d’un guide pas à pas.
>
>

## <a name="implement-hello-recommendation"></a>Implémenter la recommandation de hello
1. Bonjour **recommandations** panneau, sélectionnez **activer les groupes de sécurité réseau** sur des sous-réseaux ou des ordinateurs virtuels.
   ![Activer des groupes de sécurité réseau][1]
2. Cela ouvre le panneau de hello **configurer des groupes de sécurité réseau manquant** des sous-réseaux ou pour les ordinateurs virtuels, selon la recommandation hello que vous avez sélectionné. Sélectionnez un sous-réseau ou un ordinateur virtuel de tooconfigure un groupe de sécurité réseau sur.

   ![Configurer un groupe de sécurité réseau pour un sous-réseau][2]

   ![Configurer un groupe de sécurité réseau pour une machine virtuelle][3]
3. Sur hello **choisir un groupe de sécurité réseau** panneau, sélectionnez un groupe de sécurité réseau existant ou **nouvel** toocreate un groupe de sécurité réseau.

   ![Choisir un groupe de sécurité réseau][4]

Si vous créez un groupe de sécurité réseau, suivez les étapes de hello dans [comment toomanage groupes de sécurité réseau à l’aide de hello portail Azure](../virtual-network/virtual-networks-create-nsg-arm-pportal.md) toocreate un groupe de sécurité réseau et de définir des règles de sécurité.

## <a name="see-also"></a>Voir aussi
Cet article vous a montré comment tooimplement hello centre de sécurité recommandation « activer les groupes de sécurité réseau » pour les sous-réseaux ou les ordinateurs virtuels. toolearn savoir plus sur l’activation des groupes de sécurité réseau, voir hello :

* [Présentation du groupe de sécurité réseau](../virtual-network/virtual-networks-nsg.md)
* [Comment les groupes de sécurité réseau toomanage à l’aide de hello portail Azure](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)

toolearn en savoir plus sur le centre de sécurité, voir hello :

* [Définition des stratégies de sécurité dans le centre de sécurité Azure](security-center-policies.md) --Découvrez comment tooconfigure des stratégies de sécurité pour vos abonnements Azure et les groupes de ressources.
* [Gestion des recommandations de sécurité dans Azure Security Center](security-center-recommendations.md) : découvrez comment les recommandations peuvent vous aider à protéger vos ressources Azure.
* [Contrôle d’intégrité de la sécurité dans le centre de sécurité Azure](security-center-monitoring.md) --Découvrez comment toomonitor hello d’intégrité de vos ressources Azure.
* [Toosecurity répond et de la gestion des alertes dans le centre de sécurité Azure](security-center-managing-and-responding-alerts.md) --Découvrez comment les alertes toosecurity toomanage et y répondre.
* [Surveillance des solutions de partenaire avec Azure Security Center](security-center-partner-solutions.md) --Découvrez comment toomonitor hello état d’intégrité de vos solutions de partenaire.
* [Forum aux questions sur Azure Security Center](security-center-faq.md) --rechercher Forum aux questions sur l’utilisation du service de hello.
* [Blog de sécurité Azure](http://blogs.msdn.com/b/azuresecurity/) --obtenir les dernières informations de sécurité Azure hello et informations.

<!--Image references-->
[1]: ./media/security-center-enable-nsg/enable-nsg.png
[2]:./media/security-center-enable-nsg/configure-nsg-for-subnet.png
[3]: ./media/security-center-enable-nsg/configure-nsg-for-vm.png
[4]: ./media/security-center-enable-nsg/choose-nsg.png
