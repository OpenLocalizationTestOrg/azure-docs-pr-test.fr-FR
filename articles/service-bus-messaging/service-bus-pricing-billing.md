---
title: tarification et facturation de Bus aaaService | Documents Microsoft
description: "Présentation de la structure de prix de Service Bus."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 7c45b112-e911-45ab-9203-a2e5abccd6e0
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/02/2017
ms.author: sethm
ms.openlocfilehash: 4d06fe015baba45fef04e198363447c5541d1724
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-pricing-and-billing"></a>Tarification et facturation de Service Bus
Service Bus est disponible en trois niveaux de service : De base, Standard, et [Premium](service-bus-premium-messaging.md). Vous pouvez choisir un niveau de service pour chaque espace de noms Service Bus que vous créez ; cette sélection s’applique à l’ensemble des entités créées dans cet espace de noms.

> [!NOTE]
> Pour plus d’informations sur la tarification de Service Bus actuelle, consultez hello [page de tarification Azure Service Bus](https://azure.microsoft.com/pricing/details/service-bus/)et hello [Service Bus FAQ](service-bus-faq.md#pricing).
>
>

Service Bus utilise hello suivant deux paramètres pour les files d’attente et rubriques/abonnements :

1. **Opérations de messagerie**: définies en tant qu’appels API par rapport aux points de terminaison du service de file d’attente ou de rubrique/abonnement. Ce compteur remplacera les messages envoyés ou reçus en tant qu’unité principale de hello d’utilisation facturable pour les files d’attente et rubriques/abonnements.
2. **Connexions réparties**: défini comme hello pic du nombre de connexions persistantes ouvertes aux files d’attente, des rubriques ou des abonnements pendant une période d’échantillonnage d’une heure donnée. Ce compteur s’appliquera uniquement dans le niveau Standard hello, dans laquelle vous pouvez ouvrir des connexions supplémentaires (auparavant, les connexions étaient too100 limité par la file d’attente/rubrique/abonnement) pour un coût nominal par connexion.

Hello **Standard** couche introduit une tarification progressive pour les opérations effectuées avec les files d’attente et rubriques/abonnements, entraînant basée sur le volume des remises de % too80 à des niveaux d’utilisation le plus élevés de hello. Il existe également un forfait de base de niveau Standard de 10 $ par mois, ce qui permet de vous tooperform des too12.5 million d’opérations par mois sans frais supplémentaires.

Hello **Premium** couche fournit d’isolation de ressource au niveau de l’UC et mémoire hello afin que chaque charge de travail du client s’exécute de manière isolée. Ce conteneur de ressources est appelé *unité de messagerie*. Au moins une unité de messagerie est allouée à chaque espace de noms premium. Vous pouvez acheter une, deux ou quatre unités de messagerie pour chaque espace de noms Service Bus Premium. Une charge de travail unique ou une entité peut s’étendre sur plusieurs unités de messagerie et nombre de hello d’unités de messagerie peut être modifiée à volonté, bien que la facturation est frais de taux de 24 heures ou tous les jours. Hello résulte des performances prévisibles et reproductibles pour votre solution basée sur le Bus de Service. Au final, les performances de votre solution Service Bus sont non seulement prévisibles et répétables, mais aussi supérieures.

Notez que les frais de base de niveau Standard hello sont facturé qu’une seule fois par mois par abonnement Azure. Cela signifie qu’après avoir créé un espace de noms Service Bus de niveau Standard unique, vous serez en mesure de toocreate autant Standard espaces de noms supplémentaires que vous le souhaitez sous le même abonnement Azure, sans engager supplémentaires des frais de base.

Hello [tarification de Service Bus](https://azure.microsoft.com/pricing/details/service-bus/) tableau récapitule les différences fonctionnelles de hello entre les niveaux de hello basique, Standard et Premium.

## <a name="messaging-operations"></a>Opérations de messagerie
Dans le cadre du nouveau modèle de tarification de hello, facturation des files d’attente et rubriques/abonnements change. Ces entités passent d’une facturation par toobilling message par opération. Une « opération » fait référence à appeler tooany API par rapport à un point de terminaison de service file d’attente ou rubrique/abonnement. Cela inclut les opérations de gestion, d'envoi/réception et d'état de session.

| Type d'opération | Description |
| --- | --- |
| gestion |Création, lecture, mise à jour, suppression (CRUD) sur les files d’attente ou rubriques/abonnements. |
| Messagerie |Envoi et réception de messages avec files d’attente ou rubriques/abonnements. |
| État de la session |Récupération ou configuration de l’état de session d’une file d’attente ou d’une rubrique/un abonnement. |

Pour plus d’informations de coût, voir le prix hello répertoriées sur hello [tarification de Service Bus](https://azure.microsoft.com/pricing/details/service-bus/) page.

## <a name="brokered-connections"></a>Connexions réparties
*Brokered connections* répondent aux modèles d’utilisation client qui impliquent un grand nombre d’expéditeurs/de destinataires « en permanence connectés » aux files d’attente, aux rubriques ou aux abonnements. Les expéditeurs/destinataires connectés de façon permanente sont ceux qui se connectent à l'aide d'AMQP ou de HTTP avec un délai d'expiration de réception non nul (par exemple, l'interrogation longue HTTP). Les expéditeurs et les destinataires HTTP qui utilisent un délai d'expiration immédiat ne génèrent pas de connexions réparties.

Pour les quotas de connexion et d’autres limites de service, consultez hello [quotas du Bus des services](service-bus-quotas.md) l’article.

niveau Standard de Hello supprime la limite de connexions réparties par espace de noms hello et compte de l’utilisation d’agrégation connexion répartie entre hello abonnement Azure. Pour plus d’informations, consultez hello [connexions réparties](https://azure.microsoft.com/pricing/details/service-bus/) table.

> [!NOTE]
> 1 000 connexions réparties sont incluses dans la couche de messagerie Standard hello (via le forfait de base hello) et peuvent être partagées entre toutes les files d’attente, rubriques et abonnements au sein de l’abonnement Azure de hello associé.
>
>

<br />

> [!NOTE]
> La facturation est basée sur hello pic du nombre de connexions simultanées et est calculé au prorata basée sur 744 heures par mois.
>
>

| Niveau premium |
| --- |
| Connexions réparties dans le niveau Premium de hello n’êtes pas facturées. |

Pour plus d’informations sur les connexions réparties, consultez hello [FAQ](#faq) section plus loin dans cette rubrique.

## <a name="faq"></a>Forum Aux Questions

### <a name="what-are-brokered-connections-and-how-do-i-get-charged-for-them"></a>Que sont les connexions réparties et combien me coûtent-elles ?
Une connexion répartie est définie en tant que valeurs hello suivantes :

1. Connexion AMQP d’une file d’attente du Bus de Service client tooa ou une rubrique/abonnement.
2. HTTP appeler tooreceive un message à partir d’une rubrique Service Bus ou la file d’attente qui a une valeur de délai d’attente de réception supérieure à zéro.

Les frais de service Bus pour hello pic du nombre de connexions réparties simultanées qui dépassent hello inclus quantité (1 000 niveau Standard de hello). Pics sont mesurées sur toutes les heures, au prorata en divisant par 744 heures par mois et ajoutées sur la période de facturation mensuelle de hello. quantité de Hello inclus (1 000 connexions réparties par mois) est appliquée à fin hello de période de facturation hello par rapport à la somme de hello des pics horaires calculés au prorata de hello.

Par exemple :

1. Chacun des 10 000 appareils se connecte via une connexion AMQP unique et reçoit des commandes à partir d’une rubrique Service Bus. les appareils de Hello envoient des événements de télémétrie tooan concentrateur d’événements. Si tous les appareils se connectent pendant 12 heures par jour, hello suivant des frais de connexion s’appliquent (dans Ajout tooany autres frais de rubrique Service Bus) : 10 000 connexions * 12 heures * 31 jours / 744 = 5 000 connexions réparties. Après la provision mensuelle de hello de 1 000 connexions réparties, vous serez facturé pour 4 000 connexions réparties, au taux de hello de 0,03 $ par connexion répartie, pour un total de 120 $.
2. 10 000 appareils reçoivent des messages d'une file d'attente Service Bus via HTTP, en spécifiant un délai d'expiration différent de zéro. Si tous les appareils se connectent pendant 12 heures par jour, vous verrez hello suivant des frais de connexion (dans Ajout tooany autres frais de Service Bus) : 10 000 connexions de réception HTTP * 12 heures par jour * 31 jours / 744 heures = 5 000 connexions réparties.

### <a name="do-brokered-connection-charges-apply-tooqueues-and-topicssubscriptions"></a>Frais de connexion répartie s’appliquent-ils tooqueues et les rubriques/abonnements ?
Oui. Il n’existe aucun frais de connexion pour l’envoi d’événements à l’aide de HTTP, quel que soit le nombre de hello d’envoi de systèmes ou appareils. La réception d'événements avec le protocole HTTP et à l'aide d'un délai d'expiration supérieur à zéro, parfois appelé « interrogation longue », génère des frais de connexion répartie. Les connexions AMQP génèrent des frais de connexion répartie indépendamment de si les connexions hello sont utilisée toosend ou de réception. Notez que 100 connexions réparties sont autorisées gratuitement dans un espace de noms de base. Cela est également hello nombre maximal de connexions réparties autorisées pour hello abonnement Azure. Hello 1 000 premières connexions réparties sur tous les espaces de noms Standard dans un abonnement Azure sont incluses sans frais supplémentaires (au-delà de forfait de base hello). Étant donné que ces allocations sont suffisamment toocover nombreux scénarios messageries de service, les frais de connexion répartie généralement deviennent uniquement pertinentes si vous envisagez de toouse AMQP ou HTTP d’interrogation longue avec un grand nombre de clients. par exemple, tooachieve plus efficace événements de diffusion en continu ou activer la communication bidirectionnelle avec de nombreux appareils ou les instances de l’application.

## <a name="next-steps"></a>Étapes suivantes
* Pour plus d’informations sur la tarification de Service Bus, consultez hello [page de tarification de Service Bus](https://azure.microsoft.com/pricing/details/service-bus/).
* Consultez hello [Service Bus FAQ](service-bus-faq.md#pricing) pour quelques questions courantes sur le bus des services tarification et facturation.

[Azure portal]: https://portal.azure.com
