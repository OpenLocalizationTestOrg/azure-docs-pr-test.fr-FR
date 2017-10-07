---
title: "aaaAdd un pare-feu de la génération suivant dans le centre de sécurité Azure | Documents Microsoft"
description: "Ce document vous montre comment tooimplement hello recommandations du centre de sécurité Azure ** ajouter un pare-feu génération suivant ** et ** utilise itinéraire via Conviction uniquement **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 48b99015-4db8-4ce8-85e4-b544c0fa203e
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 9a80f12571ba08eadf3361728c6321388c863235
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-next-generation-firewall-in-azure-security-center"></a>Ajouter un pare-feu de nouvelle génération dans le Centre de sécurité Azure
Centre de sécurité Azure peut recommander que vous ajoutez un pare-feu de la génération suivant (Conviction) à partir d’un tooincrease de partenaire Microsoft votre protections de sécurité. Ce document présente un exemple de procédure toodo cela.

> [!NOTE]
> Ce document présente le service de hello à l’aide d’un exemple de déploiement.  Il ne s’agit pas d’un guide pas à pas.
>
>

## <a name="implement-hello-recommendation"></a>Implémenter la recommandation de hello
1. Bonjour **recommandations** panneau, sélectionnez **ajouter un pare-feu de la génération suivante**.
   ![Ajouter un pare-feu de nouvelle génération][1]
2. Bonjour **ajouter un pare-feu de la génération suivante** panneau, sélectionnez un point de terminaison.
   ![Sélectionner un point de terminaison][2]
3. Un second panneau **Ajouter un pare-feu de nouvelle génération** s’ouvre. Vous pouvez choisir toouse une solution existante si elle est disponible, ou vous pouvez créer un nouveau. Dans cet exemple, aucune solution existante n’est disponible ; nous allons donc créer un pare-feu de nouvelle génération.
   ![Créer un pare-feu de nouvelle génération][3]
4. toocreate une Conviction, sélectionnez une solution à partir de la liste hello de partenaires intégrés. Dans cet exemple, nous sélectionnons **Check Point**.
   ![Sélectionner une solution de pare-feu de nouvelle génération][4]
5. Hello **Check Point** panneau s’ouvre vous fournissant des informations sur les solutions de partenaire hello. Sélectionnez **créer** dans le panneau d’informations hello.
   ![Panneau d’informations du pare-feu][5]
6. Hello **créer la machine virtuelle** panneau s’ouvre. Ici, vous pouvez entrer les informations requise toospin une machine virtuelle (VM) qui s’exécute hello Conviction. Suivez les étapes de hello et fournir les informations de Conviction hello requises. Sélectionnez OK tooapply.
   ![Créer la machine virtuelle toorun Conviction][6]

## <a name="route-traffic-through-ngfw-only"></a>Acheminer le trafic uniquement via un pare-feu de nouvelle génération
Retourner toohello **recommandations** panneau. Une nouvelle entrée nommée **Acheminer le trafic uniquement via un pare-feu de nouvelle génération** a été générée une fois que vous avez ajouté un pare-feu de nouvelle génération via Security Center. Cette recommandation est créée uniquement si vous avez installé votre pare-feu de nouvelle génération via le Centre de sécurité. Si vous avez des points de terminaison exposés à Internet, le centre de sécurité recommande de configurer les règles de groupe de sécurité réseau qui force le trafic entrant tooyour machine virtuelle via votre Conviction.

1. Bonjour **Panneau de recommandations**, sélectionnez **acheminer le trafic via Conviction**.
   ![Acheminer le trafic uniquement via un pare-feu de nouvelle génération][7]
2. Cela ouvre le panneau de hello **acheminer le trafic via Conviction**, qui répertorie les ordinateurs virtuels qui vous pouvez d’acheminer le trafic vers. Sélectionnez une machine virtuelle à partir de la liste de hello.
   ![Sélectionner une machine virtuelle][8]
3. Un panneau pour hello sélectionné s’ouvre à la machine virtuelle et affiche les règles de trafic entrant connexes. Une description vous fournit plus d’informations sur les étapes suivantes possibles. Sélectionnez **modifier les règles de trafic entrant** tooproceed avec la modification d’une règle de trafic entrant. attente de Hello est que **Source** n’est pas défini trop**tout** pour les points de terminaison exposés à Internet hello lié avec hello Conviction. toolearn savoir plus sur les propriétés hello de règle de trafic entrant hello, consultez [règles du groupe de sécurité réseau](../virtual-network/virtual-networks-nsg.md#nsg-rules).
   ![Configurer l’accès à de règles toolimit][9]
   ![modifier règle de trafic entrant][10]

## <a name="see-also"></a>Voir aussi
Ce document vous a montré comment tooimplement hello recommandation du centre de sécurité « Ajouter un pare-feu de la génération suivant. » toolearn en savoir plus sur NGFWs et hello solutions de partenaire de Point de vérification, voir hello :

* [Pare-feu de nouvelle génération](https://en.wikipedia.org/wiki/Next-Generation_Firewall)
* [Check Point vSEC](https://azure.microsoft.com/marketplace/partners/checkpoint/check-point-r77-10/)

toolearn en savoir plus sur le centre de sécurité, voir hello :

* [Définition des stratégies de sécurité dans le centre de sécurité Azure](security-center-policies.md) --Découvrez comment tooconfigure des stratégies de sécurité.
* [Gestion des recommandations de sécurité dans Azure Security Center](security-center-recommendations.md) : découvrez comment les recommandations peuvent vous aider à protéger vos ressources Azure.
* [Contrôle d’intégrité de la sécurité dans le centre de sécurité Azure](security-center-monitoring.md) --Découvrez comment toomonitor hello d’intégrité de vos ressources Azure.
* [Toosecurity répond et de la gestion des alertes dans le centre de sécurité Azure](security-center-managing-and-responding-alerts.md) --Découvrez comment les alertes toosecurity toomanage et y répondre.
* [Surveillance des solutions de partenaire avec Azure Security Center](security-center-partner-solutions.md) --Découvrez comment toomonitor hello état d’intégrité de vos solutions de partenaire.
* [Forum aux questions sur Azure Security Center](security-center-faq.md) --rechercher Forum aux questions sur l’utilisation du service de hello.
* [Blog sur la sécurité Azure](http://blogs.msdn.com/b/azuresecurity/) : recherchez des billets de blog sur la sécurité et la conformité Azure.

<!--Image references-->
[1]: ./media/security-center-add-next-gen-firewall/add-next-gen-firewall.png
[2]: ./media/security-center-add-next-gen-firewall/select-an-endpoint.png
[3]: ./media/security-center-add-next-gen-firewall/create-new-next-gen-firewall.png
[4]: ./media/security-center-add-next-gen-firewall/select-next-gen-firewall.png
[5]: ./media/security-center-add-next-gen-firewall/firewall-solution-info-blade.png
[6]: ./media/security-center-add-next-gen-firewall/create-virtual-machine.png
[7]: ./media/security-center-add-next-gen-firewall/route-traffic-through-ngfw.png
[8]: ./media/security-center-add-next-gen-firewall/select-vm.png
[9]: ./media/security-center-add-next-gen-firewall/configure-rules-to-limit-access.png
[10]: ./media/security-center-add-next-gen-firewall/edit-inbound-rule.png
