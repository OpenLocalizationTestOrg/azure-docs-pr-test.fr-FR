---
title: "concepts de grille d’événement aaaAzure"
description: "Détaille Azure Event Grid et ses concepts. Définit plusieurs composants clés de Event Grid."
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/10/2017
ms.author: babanisa
ms.openlocfilehash: bb86381330fd2d6d2769167ec1953f0d5c28af85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="concepts-in-azure-event-grid"></a>Concepts utilisés dans Azure Event Grid

principaux concepts de Hello dans la grille d’événement Azure sont :

## <a name="events"></a>Événements

Un événement est hello plus petite quantité d’informations qui décrit intégralement quelque chose qui s’est produite dans le système de hello.  Chaque événement possède des informations courantes telles que : source d’événement hello, événement hello a eu lieu et l’identificateur unique.  Chaque événement comporte également des informations spécifiques qui sont uniquement pertinente toohello d’événement spécifique. Par exemple, un événement sur un nouveau fichier est créé dans le stockage Azure contient des détails sur le fichier hello, tels que de la valeur de lastTimeModified hello. Ou bien, un événement sur un ordinateur virtuel en cours de redémarrage contient hello un nom de machine virtuelle de hello et le motif de hello de redémarrage.

## <a name="event-sourcespublishers"></a>Sources d’événement/éditeurs

Une source d’événement est où les événements hello se produit. Par exemple, le stockage Azure est source d’événement hello pour l’objet blob créé des événements. Structure de machine virtuelle Azure est source d’événement hello pour les événements de l’ordinateur virtuel. Sources d’événements sont responsables de la publication d’événements tooEvent grille.

## <a name="topics"></a>Rubriques

Les éditeurs catégorisent les événements en rubriques. Hello, elle inclut un point de terminaison où serveur de publication hello envoie les événements. toorespond toocertain les types d’événements, les abonnés décider quels toosubscribe rubriques à. Rubriques fournissent également un schéma d’événement afin que les abonnés puissent découvrir comment tooconsume hello événements de manière appropriée.

Les rubriques système sont des rubriques intégrées fournies par les services Azure. Les rubriques personnalisées sont des rubriques tierces et applicatives.

## <a name="event-subscriptions"></a>Abonnements à des événements

Un abonnement indique à Event Grid quels événements d’une rubrique un abonné souhaite recevoir.  Un abonnement conserve également des informations sur la façon dont les événements doivent être remises toohello abonné.

## <a name="event-handlers"></a>Gestionnaires d’événements

À partir d’un point de vue de grille d’événement, un gestionnaire d’événements est place hello où les événements hello sont envoyé. Gestionnaire de Hello prend un événement de hello tooprocess action supplémentaire.  Event Grid prend en charge plusieurs types d’abonnés. En fonction de type hello d’abonné, la grille d’événement suit remise de hello tooguarantee différents mécanismes d’événement de hello.  Pour les gestionnaires d’événements HTTP webhook, les événements de hello est tentée jusqu'à ce que gestionnaire de hello retourne un code d’état de `200 – OK`. Pour la file d’attente de stockage Azure, les événements de hello sont tentées jusqu'à ce que hello service file d’attente est en mesure de toosuccessfully processus hello message par émission de données dans la file d’attente hello.

## <a name="filters"></a>Filtres

Lors de l’abonnement tooa rubrique, vous pouvez filtrer les événements de hello envoyés toohello le point de terminaison. Vous pouvez filtrer par type d’événement, ou modèle d’objet. Pour plus d’informations, consultez [Schéma d’abonnement à Event Grid](subscription-creation-schema.md).

## <a name="security"></a>Sécurité

Événement fournit une sécurité pour s’abonner tootopics et rubriques de publication. Lors de l’abonnement, vous devez disposer des autorisations appropriées sur les ressources hello ou une rubrique. Lors de la publication, vous devez disposer d’un jeton SAS ou l’authentification par clé de rubrique de hello. Pour en savoir plus, consultez la page [Sécurité et authentification pour Event Grid](security-authentication.md).

## <a name="failed-delivery"></a>Échec de la distribution

Lors de la grille d’événement ne peut pas confirmer qu’un événement a été reçu par le point de terminaison de l’abonné hello, il redelivers les événements hello. Pour plus d’informations, consultez la page [Distribution et nouvelle tentative de distribution de messages avec Event Grid](delivery-and-retry.md).

## <a name="next-steps"></a>Étapes suivantes

* Pour une introduction tooEvent grille, consultez [sur la grille d’événement](overview.md).
* tooquickly mise en route à l’aide de la grille d’événement, consultez [créer et itinéraire des événements personnalisés avec la grille d’événement Azure](custom-event-quickstart.md).
