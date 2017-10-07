---
title: "aaaAzure FAQ de concentrateurs d’événements | Documents Microsoft"
description: Forum Aux Questions (FAQ) sur Azure Event Hubs
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: bfa10984-eb22-4671-861a-f377a90d9372
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: sethm;shvija
ms.openlocfilehash: cc0844edcc38ad167cde9497d58d44155fc90b7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-frequently-asked-questions"></a>Forum Aux Questions (FAQ) sur Event Hubs

## <a name="general"></a>Généralités

### <a name="what-is-hello-difference-between-event-hubs-basic-and-standard-tiers"></a>Qu’est la différence hello événement concentrateurs de niveaux de base et Standard ?

niveau Standard de Hello Azure des concentrateurs d’événements fournit des fonctionnalités au-delà de ce qui est disponible dans le niveau de base hello. Hello suivant les fonctionnalités est incluse dans la norme :
* Rétention plus longue des événements
* Connexions réparties supplémentaires, avec une charge moyenne que nombre hello inclus
* Plus d’un seul groupe de consommateurs
* [Capture](https://docs.microsoft.com/azure/event-hubs/event-hubs-capture-overview)

Pour plus d’informations sur la tarification de niveaux, y compris dédié de concentrateurs d’événements, consultez hello [concentrateurs d’événements tarification](https://azure.microsoft.com/pricing/details/event-hubs/).

### <a name="what-are-event-hubs-throughput-units"></a>Que sont les unités de débit des hubs d'événements ?

Vous sélectionnez explicitement les unités de débit de concentrateurs d’événements, que ce soit via hello portail Azure ou modèles événement concentrateurs Resource Manager. Unités de débit s’appliquent tooall concentrateurs d’événements dans un espace de noms du service Event Hubs, et chaque unité de débit autorise toohello d’espace de noms hello suivant des fonctions :

* Mo too1 par seconde d’événements d’entrée (événements envoyés à un concentrateur d’événements), mais pas plus de 1000 événements d’entrée, les opérations de gestion ou le contrôle d’appels d’API par seconde.
* Too2 Mo par seconde d’événements de sortie (événements consommés à partir d’un concentrateur d’événements).
* Les too84 les Go de stockage d’événements (suffisant pour la période de rétention de 24 heures par défaut hello).

Unités de débit Event Hubs sont facturées par heure, en fonction du nombre maximal de hello d’unités sélectionnées au cours de hello donné d’heures.

### <a name="how-are-event-hubs-throughput-unit-limits-enforced"></a>Comment les limites des unités de débit des hubs d'événements sont-elles appliquées ?
Si le débit total d’entrée de hello ou taux d’événement hello total d’entrée pour tous les concentrateurs d’événements dans un espace de noms dépasse les allocations d’unité hello débit d’agrégat, les expéditeurs sont limités et recevez des erreurs indiquant que ce quota d’entrée hello a été dépassé.

Si le débit total de sortie de hello ou hello total en sortie le taux d’événement pour tous les concentrateurs d’événements dans un espace de noms dépasse les allocations d’unité de débit d’agrégat hello, récepteurs sont limitées et recevez des erreurs indiquant que ce quota de sortie hello a été dépassé. Quotas d’entrée et de sortie étant appliqués séparément, afin que l’expéditeur ne peut provoquer un événement consommation tooslow vers le bas, ni un récepteur peut empêcher d’événements d’être envoyées dans un concentrateur d’événements.

### <a name="is-there-a-limit-on-hello-number-of-throughput-units-that-can-be-selected"></a>Existe-t-il une limite du nombre de hello d’unités de débit pouvant être sélectionnés ?
Par défaut, il existe un quota de 20 unités de débit par espace de noms. Vous pouvez demander un quota d'unités de débit supérieur en soumettant un ticket de support. Au-delà de la limite d’unité hello 20 débit, offres groupées sont disponibles dans les unités de débit de 20 à 100. Notez qu’à l’aide de plus de 20 unités de débit supprime le nombre de hello toochange hello possibilité d’unités de débit sans créer un ticket de support.

### <a name="can-i-use-a-single-amqp-connection-toosend-and-receive-from-multiple-event-hubs"></a>Puis-je utiliser un toosend de connexion AMQP unique et de réception à partir de plusieurs concentrateurs d’événements ?
Oui, tant que tous les concentrateurs d’événements hello sont Bonjour même espace de noms.

### <a name="what-is-hello-maximum-retention-period-for-events"></a>Qu’est la période de rétention maximale hello pour les événements ?
Le niveau Standard des hubs d'événements prend actuellement en charge une période de rétention maximale de 7 jours. Notez que les concentrateurs d’événements ne sont pas destinés à servir de magasin de données permanent. Périodes de rétention supérieures à 24 heures sont destinées aux scénarios dans lesquels il est pratique tooreplay un événement de flux dans hello mêmes systèmes ; par exemple, tootrain ou vérifier un nouveau modèle d’apprentissage automatique sur les données existantes. Si vous avez besoin de messages rétention au-delà de 7 jours, l’activation de [capturer des concentrateurs d’événements](https://docs.microsoft.com/azure/event-hubs/event-hubs-capture-overview) sur votre événement hub extrait des données hello votre compte de stockage toohello événement concentrateur ou le compte de Service de LAC de données Azure de votre choix. L’activation de Capture est facturée en fonction de votre unité de débit achetée.

### <a name="where-is-azure-event-hubs-available"></a>Où Azure Event Hubs est-il disponible ?
Azure Event Hubs est disponible dans toutes les régions Azure prises en charge. Pour obtenir la liste, visitez hello [régions Azure](https://azure.microsoft.com/regions/) page.  

## <a name="best-practices"></a>Meilleures pratiques

### <a name="how-many-partitions-do-i-need"></a>De combien de partitions ai-je besoin ?
Veuillez n’oubliez pas que le nombre de partitions sur un concentrateur d’événements de hello ne peut pas être modifié après l’installation. Dans cette optique, il est important toothink sur combien de partitions vous avez besoin avant de commencer. 

Event Hubs est conçue tooallow un lecteur seule partition par groupe de consommateurs. Dans la plupart des cas d’usage, valeur par défaut hello quatre partitions est suffisante. Si vous cherchez tooscale votre traitement des événements, vous souhaiterez tooconsider Ajout de partitions supplémentaires. Il n’existe aucune limite de débit spécifique sur une partition, mais débit hello dans votre espace de noms est limité par un nombre d’unités de débit hello. Lorsque vous augmentez le nombre de hello d’unités de débit dans votre espace de noms, vous pouvez choisir des partitions supplémentaires tooallow lecteurs simultanés tooachieve leur propres débit maximal.

Toutefois, si vous avez un modèle dans lequel votre application a une partition particulière d’affinité tooa, augmentation nombre hello de partitions peut-être pas de n’importe quel tooyou avantage. Pour plus d’informations à ce sujet, consultez [Disponibilité et cohérence](event-hubs-availability-and-consistency.md).

## <a name="pricing"></a>Tarification

### <a name="where-can-i-find-more-pricing-information"></a>Où puis-je obtenir des informations complémentaires sur la tarification ?
Pour plus d’informations sur la tarification des Hubs d’événements, consultez hello [concentrateurs d’événements tarification](https://azure.microsoft.com/pricing/details/event-hubs/).

### <a name="is-there-a-charge-for-retaining-event-hubs-events-for-more-than-24-hours"></a>Existe-t-il des frais pour la rétention de plus de 24 heures des événements de hubs d'événements ?
niveau d’événement concentrateurs Standard Hello permet de rétention des messages des périodes de plus de 24 heures, pour un maximum de 7 jours. Si la taille hello du nombre total de hello d’événements stockés dépasse l’allocation de stockage hello pour nombre de hello d’unités de débit sélectionnées (84 Go par unité de débit), la taille hello dépasse l’allocation hello est facturée au hello publié le tarif de stockage d’objets Blob Azure. allocation de stockage Hello dans chaque unité de débit couvre tous les coûts de stockage pour les périodes de rétention de 24 heures (valeur par défaut de hello) même si l’unité de débit hello toohello l’allocation d’entrée maximale est utilisée.

### <a name="how-is-hello-event-hubs-storage-size-calculated-and-charged"></a>Comment hello taille de stockage de concentrateurs d’événements est calculée et facturée ?
taille totale de Hello de tous les événements stockés, y compris tout espace réservé interne pour les en-têtes d’événement ou sur les structures de stockage de disque dans tous les concentrateurs d’événements, est mesurée journée hello. Fin de hello de journée de hello, taille de stockage maximale hello est calculée. allocation de stockage quotidienne Hello est calculée en fonction hello le nombre minimal d’unités de débit sélectionnées durant la journée hello (chaque unité de débit offrant une allocation de 84 Go). Si la taille totale de hello dépasse hello calculée quotidiennement allocation de stockage, excédent de stockage hello est facturée à l’aide du taux de stockage d’objets Blob Azure (à hello **stockage localement redondant** taux).

### <a name="how-are-event-hubs-ingress-events-calculated"></a>Comment les événements d'entrée des hubs d'événements sont-ils calculés ?
Chaque événement envoyé le concentrateur d’événements tooan considéré comme un message facturable. Un *événement d’entrée* est défini comme une unité de données sont inférieur ou égal too64 Ko. Tout événement qui est inférieur ou égal too64 Ko est considéré comme toobe d’un événement facturable. Si l’événement de hello est supérieure à 64 Ko, nombre hello d’événements facturables est calculé selon la taille d’événement toohello, multiple de 64 Ko. Par exemple, un événement de 8 Ko envoyé toohello concentrateur d’événements est facturé comme un événement, mais un message de 96 Ko envoyé de concentrateur d’événements toohello est facturé comme deux événements.

Événements consommés à partir d’un concentrateur d’événements, ainsi que les opérations de gestion et les appels de contrôle tels que les points de contrôle, ne sont pas comptés comme des événements d’entrée facturables, mais engendrent une augmentation de l’allocation d’unité toohello débit.

### <a name="do-brokered-connection-charges-apply-tooevent-hubs"></a>Frais de connexion répartie s’appliquent tooEvent Hubs ?
Des frais de connexion s’appliquent uniquement lorsque hello protocole AMQP est utilisé. Il n’existe aucun frais de connexion pour l’envoi d’événements à l’aide de HTTP, quel que soit le nombre de hello d’envoi de systèmes ou appareils. Si vous envisagez de toouse AMQP (par exemple, tooachieve plus efficace de diffusion en continu ou tooenable bidirectionnel communication d’événement dans les scénarios de contrôle et commande IoT), consultez hello [concentrateurs d’événements informations de tarification](https://azure.microsoft.com/pricing/details/event-hubs/) page pour plus d’informations sur la façon nombre de connexions est inclus dans chaque niveau de service.

### <a name="how-is-event-hubs-capture-billed"></a>Comment est facturé Event Hubs Capture ?
Capture est activée quand un concentrateur d’événements dans l’espace de noms hello hello Capture option est activée. Event Hubs Capture est facturé à l’heure, par unité de débit achetée. Comme le nombre d’unités de débit de hello est augmenté ou diminué, capturer des concentrateurs d’événements de facturation reflète ces modifications en incréments d’heure ensemble. Pour plus d’informations sur la facturation d’Event Hubs Capture, consultez [Informations tarifaires pour Event Hubs](https://azure.microsoft.com/pricing/details/event-hubs/).

### <a name="will-i-be-billed-for-hello-storage-account-i-select-for-event-hubs-capture"></a>J’ai facturé pour le compte de stockage hello que sélectionner pour la Capture des concentrateurs d’événements ?
Capture utilise un compte de stockage que vous fournissez lorsqu’il est activé sur un concentrateur d’événements. Comme il s’agit de votre compte de stockage, toute modification pour cette configuration est facturée tooyour abonnement Azure.

## <a name="quotas"></a>Quotas

### <a name="are-there-any-quotas-associated-with-event-hubs"></a>Y a-t-il des quotas associés aux Event Hubs ?
Pour obtenir la liste de tous les quotas d’Event Hubs, consultez la page [quotas](event-hubs-quotas.md).

## <a name="troubleshooting"></a>Résolution des problèmes

### <a name="what-are-some-of-hello-exceptions-generated-by-event-hubs-and-their-suggested-actions"></a>Quelles sont les exceptions de hello générées par les concentrateurs d’événements et leurs actions suggérées ?
Pour obtenir la liste des exceptions Event Hubs potentielles, consultez la page [Vue d’ensemble des exceptions](event-hubs-messaging-exceptions.md).

### <a name="diagnostic-logs"></a>Journaux de diagnostic
Concentrateurs d’événements prend en charge deux types de [les journaux de diagnostic](event-hubs-diagnostic-logs.md) -Capture les journaux d’erreurs et des opérations - qui sont représentés dans json et peuvent être activés via hello portail Azure.

### <a name="support-and-sla"></a>Prise en charge et contrats SLA
Le support technique pour Event Hubs est disponible via hello [forums de communauté](https://social.msdn.microsoft.com/forums/azure/home). La gestion de la facturation et des abonnements est fournie gratuitement.

toolearn en savoir plus sur notre contrat SLA, consultez hello [les contrats de niveau de Service](https://azure.microsoft.com/support/legal/sla/) page.

## <a name="next-steps"></a>Étapes suivantes
Vous pouvez plus d’informations sur les concentrateurs d’événements en visitant hello suivant liens :

* [Vue d’ensemble des hubs d’événements](event-hubs-what-is-event-hubs.md)
* [Créer un concentrateur d’événements](event-hubs-create.md)
