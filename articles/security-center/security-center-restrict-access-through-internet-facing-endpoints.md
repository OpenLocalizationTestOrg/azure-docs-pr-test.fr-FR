---
title: "accès aaaRestrict via des points de terminaison exposés à Internet dans le centre de sécurité Azure | Documents Microsoft"
description: "Ce document vous montre comment tooimplement hello recommandation du centre de sécurité Azure ** restreindre l’accès via Internet exposés au point de terminaison **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 727d88c9-163b-4ea0-a4ce-3be43686599f
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/03/2017
ms.author: terrylan
ms.openlocfilehash: ee72497088618d4db29b5ae4183f4fe77b498423
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="restrict-access-through-internet-facing-endpoints-in-azure-security-center"></a>Restreindre l’accès via des points de terminaison accessibles sur Internet dans le Centre de sécurité Azure
Le Centre de sécurité Azure vous recommande de restreindre l’accès via les points de terminaison accessibles sur Internet si l’un de vos groupes de sécurité réseau (NSG) possède une ou plusieurs règles de trafic entrant autorisant l’accès à partir de « n’importe quelle » adresse IP source. Ouverture d’accès trop « tout » peut activer des personnes malveillantes tooaccess vos ressources. Centre de sécurité seront vous recommandons de modifier ces règles de trafic entrant toorestrict accès toosource adresses qui ont réellement besoin d’accéder.

Cette recommandation est générée pour n’importe quel port non web avec une « quelconque » source.

> [!NOTE]
> Ce document présente le service de hello à l’aide d’un exemple de déploiement. Il ne s’agit pas d’un guide pas à pas.
>
>

## <a name="implement-hello-recommendation"></a>Implémenter la recommandation de hello
1. Bonjour **Panneau de recommandations**, sélectionnez **restreindre l’accès via Internet exposés au point de terminaison**.

   ![Restreindre l’accès via un point de terminaison accessible sur Internet][1]
2. Cela ouvre le panneau de hello **restreindre l’accès via Internet exposés au point de terminaison**. Ce panneau répertorie hello virtual machines virtuelles avec les règles de trafic entrant qui créent un problème de sécurité potentiel. Sélectionnez une machine virtuelle.

   ![Sélectionner une machine virtuelle][2]
3. Hello **NSG** panneau affiche des informations de groupe de sécurité réseau, les règles de trafic entrant connexes, et hello associé la machine virtuelle. Sélectionnez **modifier les règles de trafic entrant** tooproceed avec la modification d’une règle de trafic entrant.

   ![Panneau Groupe de sécurité réseau][3]
4. Sur hello **les règles de sécurité de trafic entrant** panneau Sélectionner hello tooedit de règle de trafic entrant. Dans cet exemple, sélectionnons **AllowWeb**.

   ![Règles de sécurité de trafic entrant][4]

   Notez que vous pouvez également sélectionner **règles par défaut** ensemble de hello toosee de règles par défaut contenues dans tous les groupes de sécurité réseau. Impossible de supprimer les règles par défaut de Hello mais, car ils sont affectés d’une priorité plus faible, elles peuvent être remplacées par les règles hello que vous créez. En savoir plus sur les [règles par défaut](../virtual-network/virtual-networks-nsg.md#default-rules).

   ![Règles par défaut][5]
5. Sur hello **AllowWeb** panneau, modifier des propriétés de règle de trafic entrant hello afin que hello hello **Source** est une adresse IP ou un bloc d’adresses IP. toolearn savoir plus sur les propriétés hello de règle de trafic entrant hello, consultez [règles du groupe de sécurité réseau](../virtual-network/virtual-networks-nsg.md#nsg-rules).

   ![Modifier une règle de trafic entrant][6]

## <a name="see-also"></a>Voir aussi
Cet article vous a montré comment tooimplement hello centre de sécurité recommandation « restreindre l’accès via Internet exposés au point de terminaison. » toolearn savoir plus sur l’activation des groupes de sécurité réseau et les règles, voir hello :

* [Présentation du groupe de sécurité réseau](../virtual-network/virtual-networks-nsg.md)
* [Comment les groupes de sécurité réseau toomanage à l’aide de hello portail Azure](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)

toolearn en savoir plus sur le centre de sécurité, voir hello :

* [Définition des stratégies de sécurité dans le centre de sécurité Azure](security-center-policies.md)--Découvrez comment tooconfigure des stratégies de sécurité pour vos abonnements Azure et les groupes de ressources.
* [Gestion des recommandations de sécurité dans Azure Security Center](security-center-recommendations.md): découvrez la façon dont les recommandations peuvent vous aider à protéger vos ressources Azure.
* [Contrôle d’intégrité de la sécurité dans le centre de sécurité Azure](security-center-monitoring.md)--Découvrez comment toomonitor hello d’intégrité de vos ressources Azure.
* [Toosecurity répond et de la gestion des alertes dans le centre de sécurité Azure](security-center-managing-and-responding-alerts.md)--Découvrez comment les alertes toosecurity toomanage et y répondre.
* [Surveillance des solutions de partenaire avec Azure Security Center](security-center-partner-solutions.md) --Découvrez comment toomonitor hello état d’intégrité de vos solutions de partenaire.
* [Forum aux questions sur Azure Security Center](security-center-faq.md)--rechercher Forum aux questions sur l’utilisation du service de hello.
* [Blog de sécurité Azure](http://blogs.msdn.com/b/azuresecurity/)--obtenir les dernières informations de sécurité Azure hello et informations.

<!--Image references-->
[1]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/restrict-access-thru-internet-facing-endpoint.png
[2]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/select-a-vm.png
[3]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/network-security-group-blade.png
[4]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/inbound-security-rules.png
[5]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/default-rules.png
[6]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/edit-inbound-rule.png
