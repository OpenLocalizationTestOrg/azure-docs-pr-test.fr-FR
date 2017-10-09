---
title: "vue d’ensemble de la grille d’événement aaaAzure"
description: "Détaille Azure Event Grid et ses concepts."
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/18/2017
ms.author: babanisa
ms.openlocfilehash: 95dce22e9335df88e81b134143a6c14994c26b8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="an-introduction-tooazure-event-grid"></a>Un tooAzure présentation grille d’événement

Azure grille d’événement vous permet de créer des applications tooeasily avec les architectures basées sur les événements. Vous sélectionnez hello ressources Azure vous comme toosubscribe à et donner le Gestionnaire d’événements hello ou WebHook point de terminaison toosend hello événement. Event Grid dispose d’une prise en charge intégrée pour les événements provenant des services Azure, tels que les objets BLOB de stockage et les groupes de ressources. Event Grid dispose également d’une prise en charge personnalisée pour les événements d’application et de tiers, à l’aide des rubriques et webhooks personnalisés. 

Vous pouvez utiliser les filtres tooroute des événements spécifiques toodifferent points, points de terminaison de multidiffusion toomultiple et assurez-vous que vos événements sont remis de manière fiable. Event Grid dispose également d’une prise en charge intégrée pour des événements personnalisés et tiers.

Pour la version préliminaire de hello, prend en charge la grille d’événement **westus2** et **westcentralus** emplacements. D’autres régions seront ajoutées.

Cet article fournit une vue d’ensemble d’Azure Event Grid. Si vous souhaitez tooget main de grille d’événement, consultez [créer et itinéraire des événements personnalisés avec la grille d’événement Azure](custom-event-quickstart.md).

![Modèle de grille d’événement fonctionnel](./media/overview/event-grid-functional-model.png)

Stockage Blob n’est pas disponible publiquement en tant qu’éditeur.

## <a name="concepts"></a>Concepts

Il existe cinq concepts dans Azure Event Grid qui vous permettent de démarrer :

* **Événements** : ce qu’il s’est passé.
* **Sources/éditeurs d’événements** : si l’événement de hello a eu lieu.
* **Rubriques** -hello du point de terminaison où envoyer des événements par les serveurs de publication.
* **Abonnements aux événements** -événements de tooroute mécanisme intégré ou de point de terminaison des hello, parfois toomultiple gestionnaires. Les abonnements sont également utilisés par les événements entrants gestionnaires toointelligently filtre.
* **Gestionnaires d’événements** - hello application ou service réaction toohello événement.

Pour plus d’informations sur ces concepts, consultez [Concepts dans Azure Event Grid](concepts.md).

## <a name="capabilities"></a>Fonctionnalités

Voici quelques-unes des principales fonctionnalités de hello de grille d’événement Azure :

* **Simplicité** -Point et cliquer sur les événements tooaim à partir de votre gestionnaire d’événements tooany ressource Azure ou d’un point de terminaison.
* **Filtrage avancé** -filtre sur un événement de type ou l’événement de publication tooensure de chemin d’accès gestionnaires d’événements reçoivent uniquement les événements pertinents.
* **Distribution ramifiée** -s’abonner à plusieurs points de terminaison toohello même événement toosend copie de hello événement tooas beaucoup d’emplacements en fonction des besoins.
* **Fiabilité** -utiliser la nouvelle tentative de 24 heures avec tooensure interruption exponentielle les événements sont remis.
* **Payer par événement** - payez uniquement pour la quantité de hello vous utilisez la grille d’événement.
* **Débit élevé** : générez des charges de travail élevées sur Event Grid avec prise en charge de millions d’événements par seconde.
* **Événements intégrés** : préparez et soyez rapidement opérationnel avec des événements intégrés définis par la ressource.
* **Événements personnalisés** : utilisez le routage Event Grid, le filtrage et les événements personnalisés livré de manière fiable dans votre application.

## <a name="built-in-publisher-and-handler-integration"></a>Intégration du gestionnaire et de l’éditeur intégrés

Azure propose la prise en charge de l’événement intégré à l’aide de nombreux services, y compris les éditeurs et les gestionnaires.

### <a name="publishers"></a>Éditeurs

Actuellement, hello services Azure suivants ont prise en charge de serveur de publication intégré pour la grille d’événement :

* Groupes de ressources (opérations de gestion)
* Abonnements Azure (opérations de gestion)
* Event Hubs
* Rubriques personnalisées

D’autres services Azure seront ajoutés cette année.

### <a name="handlers"></a>Gestionnaires

Actuellement, hello services Azure suivants ont intégré Gestionnaire prise en charge pour la grille d’événement : 

* Azure Functions
* Logic Apps
* Azure Automation
* WebHooks

D’autres services Azure seront ajoutés cette année.

## <a name="what-can-i-do-with-event-grid"></a>Que puis-je faire avec Event Grid ?

Azure Event Grid fournit plusieurs fonctionnalités qui améliorent considérablement l’automatisation d’opérations sans serveur et le travail d’intégration : 

### <a name="serverless-application-architectures"></a>Architectures d’application sans serveur

![Application sans serveur](./media/overview/serverless_web_app.png)

La grille d’événement connecte des sources de données et des gestionnaires d’événements. Par exemple, utiliser déclencheur tooinstantly de grille d’événement pour une analyse d’image sans fonction toorun chaque fois qu’une nouvelle photo est ajouté le conteneur de stockage d’objets blob tooa. 

### <a name="ops-automation"></a>Automatisation des opérations

![Automatisation des opérations](./media/overview/Ops_automation.png)

Grille d’événement vous permet d’automatiser de toospeed et simplifier la mise en œuvre de la stratégie. Par exemple, Event Grid peut informer Azure Automation lors de la création d’une machine virtuelle ou de l’entrée en service d’une base de données SQL. Ces événements peuvent être utilisés tooautomatically vérifier que les configurations de service sont compatibles, placer des métadonnées dans les outils, les machines virtuelles de balise ou les éléments de travail de fichier.

### <a name="application-integration"></a>Intégration d’applications

![Intégration d’applications](./media/overview/app_integration.png)

Event Grid connecte votre application à d’autres services. Par exemple, créez une rubrique personnalisée de toosend tooEvent de données d’événement de votre application grille et tirer parti de sa remise fiable, avancée, le routage et intégration directe avec Azure. Ou bien, vous pouvez utiliser grille d’événement avec des données Logic Apps tooprocess n’importe où, sans écrire de code. 

## <a name="how-is-event-grid-different-from-other-azure-integration-services"></a>En quoi Event Grid est différent d’autres services d’intégration Azure ?

Event Grid est un fond de panier de gestion des événements qui permet la programmation réactive, pilotée par événements. Elle est intégrée en profondeur aux services Azure et peut être intégrée à des services tiers. message d’événement Hello contient les informations de hello nécessaires toochanges tooreact dans les services et applications. Grille d’événement n’est pas un pipeline de données et il ne remet plus aucun objet hello réel qui a été mis à jour.

Service Bus est parfaitement adapté aux applications d’entreprise traditionnelles qui nécessitent des transactions, des classements, la détection des doublons et une cohérence instantanée. Event Grid est conçu pour la vitesse, la mise à l’échelle, l’étendue et le bas coût dans un modèle réactif. Il est parfaitement tooserverless architecture.

Event Grid complète d’autres services Azure tels que Logic Apps et Event Hubs. Les déclencheurs d’événements grille hello logique application toobegin son flux de travail. Concentrateurs d’événements fonctionne avec la grille d’événement en vous tooevents tooreact de capturer des concentrateurs d’événements et les pipelines d’entrée et de transformation de données de build.

## <a name="how-much-does-event-grid-cost"></a>Combien coûte Event Grid ?

Azure Event Grid utilise un modèle de tarification de paie par événement, afin que vous ne payez que ce que vous utilisez.

Grille d’événement coûte 0,60 $ par million d’opérations (0,30 pendant la version préliminaire) et hello opération 100 000 premiers par mois sont gratuits. Les opérations sont définies comme entrée d’événement, correspondance avancée, tentative de livraison et appels de gestion.  Vous trouverez plus de détails sur hello [page de tarification](https://azure.microsoft.com/pricing/details/event-grid/).

## <a name="next-steps"></a>Étapes suivantes

* [Créer et de s’abonner à des événements de toocustom](custom-event-quickstart.md) concrète et démarrer l’envoi de votre propre point de terminaison tooany événements personnalisés à l’aide du démarrage rapide de grille d’événement Azure hello.
* [À l’aide de Logic Apps comme gestionnaire d’événements](monitor-virtual-machine-changes-event-grid-logic-app.md) un didacticiel sur la création d’une application à l’aide de Logic Apps tooreact tooevents exécute un push de grille d’événement.
* [Référence de l'API REST Event Grid](/rest/api/eventgrid)  
  Fournit des informations techniques supplémentaires sur hello grille d’événement Azure et une référence pour la gestion des abonnements aux événements, routage et le filtrage.
