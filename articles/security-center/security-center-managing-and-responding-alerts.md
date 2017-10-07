---
title: "aaaManage les alertes de sécurité dans le centre de sécurité Azure | Documents Microsoft"
description: "Ce document vous aide à vous toouse Azure Security Center fonctionnalités toomanage et répond toosecurity alertes."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: b88a8df7-6979-479b-8039-04da1b8737a7
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: yurid
ms.openlocfilehash: f1cb7e4770776827b75ed15893914678c1f44216
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-and-responding-toosecurity-alerts-in-azure-security-center"></a>La gestion et de répondre toosecurity des alertes dans le centre de sécurité Azure
Ce document vous permet d’utiliser le centre de sécurité Azure toomanage et répondre toosecurity alertes.

> [!NOTE]
> détections de tooenable avancé, mise à niveau tooAzure Security Center Standard. Une version d’évaluation gratuite de 60 jours est disponible. tooupgrade, sélectionnez niveau tarifaire Bonjour [stratégie de sécurité](security-center-policies.md). Consultez [tarification d’Azure Security Center](security-center-pricing.md) toolearn plus.
>
>

## <a name="what-are-security-alerts"></a>Que sont les alertes de sécurité ?
Centre de sécurité automatiquement collecte, analyse et intègre des données de journal à partir de vos ressources Azure, le réseau de hello et les solutions de partenaire, tels que des solutions de protection pare-feu et de point de terminaison, les menaces réelles toodetect connectées et réduire les faux positifs. Une liste des alertes de sécurité hiérarchisée est indiquée dans le centre de sécurité, ainsi que de hello informations dont vous avez besoin tooquickly examiner le problème de hello et des recommandations sur la manière tooremediate une attaque.


> [!NOTE]
> Pour plus d’informations sur le fonctionnement des fonctionnalités de détection de Security Center, consultez [Fonctionnalités de détection d’Azure Security Center](security-center-detection-capabilities.md).
>
>

## <a name="managing-security-alerts"></a>Gestion des alertes de sécurité
Vous pouvez consulter vos alertes en cours en examinant hello **alertes de sécurité** vignette. Ouvrez le portail Azure et suivez les étapes de hello ci-dessous toosee plus de détails sur chaque alerte :

1. Tableau de bord du centre de sécurité hello, vous verrez hello **alertes de sécurité** vignette.

    ![Vignette Alertes de sécurité dans le Centre de sécurité](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig1-ga.png)

2. Cliquez sur Bonjour vignette tooopen Bonjour **alertes de sécurité** panneau qui contient plus de détails sur hello alertes comme indiqué ci-dessous.

   ![panneau d’alertes de sécurité Hello dans le centre de sécurité](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig2-ga.png)

Dans la partie inférieure de hello de ce panneau sont détails hello pour chaque alerte. toosort, cliquez sur la colonne que vous souhaitez toosort par hello. définition de Hello pour chaque colonne est donnée ci-dessous :

* **Description**: une brève explication de l’alerte de hello.
* **Nombre**: liste de toutes les alertes d’un type spécifique qui ont été détectées un jour précis.
* **Détecté par**: hello service qui a été chargé de déclencher l’alerte de hello.
* **Date**: hello date cet événement hello s’est produite.
* **État**: hello l’état actuel de cette alerte. Il existe deux types d’état :
  * **Active**: alerte de sécurité hello a été détectée.
* **Gravité**: niveau de gravité hello, qui peut être élevée, moyenne ou faible.

### <a name="filtering-alerts"></a>Filtrage des alertes
Vous pouvez filtrer les alertes en fonction de la date, de l’état et du niveau de gravité. Filtrer les alertes peut être utile pour les scénarios où vous avez besoin d’étendue de hello toonarrow d’afficher des alertes de sécurité. Par exemple, vous pouvez vous tooaddress les alertes de sécurité s’est produite dans hello des dernières 24 heures, car vous examinez une violation potentielle dans le système de hello.

1. Cliquez sur **filtre** sur hello **alertes de sécurité** panneau. Hello **filtre** panneau s’ouvre et vous sélectionnez hello, état, gravité valeurs de date et vous souhaitez toosee.

    ![Filtrage des alertes dans le Centre de sécurité](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig3-2017.png)

### <a name="respond-toosecurity-alerts"></a>Alertes répondent toosecurity
Sélectionnez un toolearn d’alerte de sécurité plus sur les événements hello ayant déclenché l’alerte de hello et, si elle existe, les étapes doivent tootake tooremediate une attaque. Les alertes de sécurité sont regroupées par type et date d’apparition. En cliquant sur une alerte de sécurité pour ouvrir un panneau contenant une liste d’alertes de hello regroupée.

![Répondre toosecurity des alertes dans le centre de sécurité Azure](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig5-ga.png)

Dans ce cas, les alertes hello qui ont été déclenchées reportez-vous toosuspicious activité du protocole RDP (Remote Desktop). Hello première colonne affiche les ressources qui ont été attaquées ; Ensuite, Hello montre combien de fois les ressources hello a été attaqué ; Hello troisième affiche hello d’attaque de hello ; Hello affiche quatrième état d’alerte de hello ; et hello cinquième gravité hello d’attaque de hello s’affiche. Après avoir examiné ces informations, cliquez sur ressources hello qui a été attaqué, et un nouveau panneau s’ouvre.

![Suggestions pour le toodo sur la sécurité des alertes dans le centre de sécurité Azure](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig6-ga.png)

Bonjour **Description** champ de ce panneau vous trouverez plus de détails sur cet événement. Ces détails supplémentaires offrent idée quelles hello déclenchées sécurité alerte, hello ressource cible, lors de l’hello applicable adresse IP source et des recommandations sur la façon de tooremediate.  Dans certains cas, adresse IP de source hello est vide (non disponible), car tous les journaux d’événements de sécurité Windows incluent l’adresse IP de hello.

mise à jour Hello suggérée par le centre de sécurité varient conséquente alerte de sécurité toohello. Dans certains cas, vous avez peut-être toouse autres tooimplement fonctionnalités Azure hello recommandé de mise à jour. Hello, par exemple, mise à jour pour ce type d’attaque est tooblacklist hello adresse qui génère cette attaque à l’aide un [réseau ACL](../virtual-network/virtual-networks-acl.md) ou un [groupe de sécurité réseau](../virtual-network/virtual-networks-nsg.md) règle.

> [!NOTE]
> Pour plus d’informations sur hello différents types d’alertes, consultez [les alertes de sécurité par Type dans le centre de sécurité Azure](security-center-alerts-type.md).
>
>

## <a name="see-also"></a>Voir aussi
Dans ce document, vous avez appris comment tooconfigure des stratégies de sécurité dans le centre de sécurité. toolearn en savoir plus sur le centre de sécurité, voir hello :

* [Gestion des incidents de sécurité dans Azure Security Center](security-center-incident.md)
* [Fonctionnalités de détection d’Azure Security Center](security-center-detection-capabilities.md)
* [Guide des opérations et de planification du Centre de sécurité Azure](security-center-planning-and-operations-guide.md)
* [Forum aux questions sur Azure Security Center](security-center-faq.md) : Forum aux questions sur l’utilisation hello service de recherche.
* [Blog sur la sécurité Azure](http://blogs.msdn.com/b/azuresecurity/) : accédez à des billets de blog sur la sécurité et la conformité Azure.
