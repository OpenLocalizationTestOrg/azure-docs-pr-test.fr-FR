---
title: "aaaHow toolog événements tooAzure Hubs d’événements dans la gestion des API Azure | Documents Microsoft"
description: "Découvrez comment toolog événements tooAzure Hubs d’événements dans la gestion des API Azure."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 88f6507d-7460-4eb2-bffd-76025b73f8c4
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 09ca65fc48a874467c6662858f7594e9b19fcdb9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toolog-events-tooazure-event-hubs-in-azure-api-management"></a>Comment toolog événements tooAzure Hubs d’événements dans la gestion des API Azure
Azure Event Hubs est un service d’entrée de données hautement évolutive qui peut traiter des millions d’événements par seconde afin que vous puissiez traiter et analyser hello des quantités massives de données généré par vos périphériques connectés et les applications. Concentrateurs d’événements joue le rôle hello « porte d’entrée » pour un pipeline d’événements, et une fois que les données sont collectées dans un concentrateur d’événements, il peut être transformé et stockées à l’aide de n’importe quel fournisseur analytique en temps réel ou des cartes de traitement par lot/stockage. Concentrateurs d’événements dissocie production hello d’un flux d’événements à partir de la consommation de ces événements, hello afin que les consommateurs d’événements peuvent accéder à des événements de hello sur leur propre calendrier.

Cet article est un toohello d’accompagnement [intégrer Gestion des API Azure avec des concentrateurs d’événements](https://azure.microsoft.com/documentation/videos/integrate-azure-api-management-with-event-hubs/) vidéo et décrit comment les événements de gestion des API toolog à l’aide d’Azure Event Hubs.

## <a name="create-an-azure-event-hub"></a>Création d'un hub d'événements Azure
toocreate un concentrateur d’événements, connectez-vous toohello [portail Azure classic](https://manage.windowsazure.com) et cliquez sur **nouveau**->**des Services d’application**->**Service Bus**  -> **Concentrateur d’événements**->**création rapide**. Entrez un nom d’Event Hub, une région, sélectionnez un abonnement et sélectionnez un espace de noms. Si vous n’avez pas déjà créé un espace de noms, vous pouvez créer un en tapant un nom Bonjour **Namespace** zone de texte. Une fois que toutes les propriétés sont configurées, cliquez sur **créer un concentrateur d’événements** toocreate hello concentrateur d’événements.

![Créer un event hub][create-event-hub]

Ensuite, accédez toohello **configurer** onglet pour votre nouveau concentrateur d’événements et de créer deux **stratégies d’accès partagé**. Nom hello premier **envoi** et lui donner **envoyer** autorisations.

![Stratégie Envoi][sending-policy]

Nom hello deuxième **réception**, attribuez-lui **écouter** autorisations, puis cliquez sur **enregistrer**.

![Stratégie Réception][receiving-policy]

Chaque stratégie d’accès partagé autorise les applications toosend et recevoir des événements tooand hello concentrateur d’événements. chaînes de connexion tooaccess hello pour ces stratégies, accédez à toohello **tableau de bord** onglet de hello concentrateur d’événements et cliquez sur **les informations de connexion**.

![Chaîne de connexion][event-hub-dashboard]

Hello **envoi** chaîne de connexion est utilisée lors de la journalisation des événements et hello **réception** chaîne de connexion est utilisée lors du téléchargement des événements à partir de hello concentrateur d’événements.

![Chaîne de connexion][event-hub-connection-string]

## <a name="create-an-api-management-logger"></a>Créer un enregistreur d’événements de gestion des API
Maintenant que vous avez un concentrateur d’événements, étape suivante de hello est tooconfigure un [enregistreur d’événements](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) dans votre gestion des API de service afin qu’il puisse consigner les événements toohello concentrateur d’événements.

Les journaux de gestion des API sont configurés à l’aide de hello [API REST de gestion des API](http://aka.ms/smapi). Avant d’utiliser hello API REST pour hello première fois, passez en revue de hello [conditions préalables](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#Prerequisites) et assurez-vous d’avoir [activé toohello d’accès aux API REST](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#EnableRESTAPI).

toocreate un enregistreur d’événements, vérifiez une demande HTTP PUT à l’aide de hello suivant le modèle d’URL.

`https://{your service}.management.azure-api.net/loggers/{new logger name}?api-version=2014-02-14-preview`

* Remplacez `{your service}` par nom hello de votre instance de service de gestion des API.
* Remplacez `{new logger name}` avec le nom souhaité pour votre nouvel enregistreur d’événements hello. Vous ferez référence ce nom lorsque vous configurez hello [journal à eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) stratégie

Ajoutez hello en-têtes toohello demande.

* Type de contenu : application/json
* Autorisation : SharedAccessSignature 58...
  * Pour obtenir des instructions sur la génération hello `SharedAccessSignature` consultez [Azure API Management REST API Authentication](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-authentication).

Spécifiez le corps de la demande hello à l’aide de hello suivant le modèle.

```json
{
  "type" : "AzureEventHub",
  "description" : "Sample logger description",
  "credentials" : {
    "name" : "Name of hello Event Hub from hello Azure Classic Portal",
    "connectionString" : "Endpoint=Event Hub Sender connection string"
    }
}
```

* `type`doit être défini trop`AzureEventHub`.
* `description`Fournit une description facultative de l’enregistreur d’événements hello et peut être une chaîne de longueur nulle si vous le souhaitez.
* `credentials`contient hello `name` et `connectionString` de votre concentrateur d’événements Azure.

Lorsque vous effectuez la demande de hello, si l’enregistreur d’événements hello est créé un code d’état de `201 Created` est retourné.

> [!NOTE]
> Pour connaître les autres codes de retour possibles et leurs raisons, consultez [Créer un enregistreur d’événements](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity#PUT). toosee comment effectuer d’autres opérations telles que la liste, update et delete, consultez hello [journal](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) documentation de l’entité.
>
>

## <a name="configure-log-to-eventhubs-policies"></a>Configurer des stratégies Enregistrer sur event hub
Une fois votre enregistreur d’événements est configuré dans la gestion des API, vous pouvez configurer vos événements de hello souhaité de stratégies de journal à eventhubs toolog. Hello journal à eventhubs stratégie peut être utilisée dans deux hello stratégie entrante ou section hello stratégie sortante.

stratégies tooconfigure, connectez-vous toohello [portail Azure](https://portal.azure.com), parcourir le service de gestion des API tooyour et cliquez sur **portail de publication** tooaccess hello portail de publication.

![Portail des éditeurs][publisher-portal]

Cliquez sur **stratégies** dans le menu Gestion des API hello hello gauche, sélectionnez le produit de votre choix hello et API, puis cliquez sur **ajouter une stratégie**. Dans cet exemple, nous ajoutons une stratégie toohello **Echo API** Bonjour **illimité** produit.

![Add policy][add-policy]

Placez votre curseur dans hello `inbound` stratégie et cliquez sur hello **journal tooEventHub** hello tooinsert de stratégie `log-to-eventhub` modèle d’instruction de stratégie.

![Policy editor][event-hub-policy]

```xml
<log-to-eventhub logger-id ='logger-id'>
  @( string.Join(",", DateTime.UtcNow, context.Deployment.ServiceName, context.RequestId, context.Request.IpAddress, context.Operation.Name))
</log-to-eventhub>
```

Remplacez `logger-id` par nom hello d’enregistreur d’événements de la gestion des API hello configurées à l’étape précédente de hello.

Vous pouvez utiliser n’importe quelle expression qui retourne une chaîne en tant que valeur hello pour hello `log-to-eventhub` élément. Dans cet exemple, une chaîne contenant la date de hello et heure, nom du service, id de demande, demander l’adresse ip et nom de l’opération est enregistrée.

Cliquez sur **enregistrer** toosave hello mis à jour la configuration de la stratégie. Dès qu’elle est enregistrée hello stratégie est active et les événements sont enregistré toohello désigné du concentrateur d’événements.

## <a name="next-steps"></a>Étapes suivantes
* En savoir plus sur Azure Event Hubs
  * [Prise en main avec Azure Event Hubs](../event-hubs/event-hubs-c-getstarted-send.md)
  * [Réception de messages avec EventProcessorHost](../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md)
  * [Guide de programmation Event Hubs](../event-hubs/event-hubs-programming-guide.md)
* En savoir plus sur l’intégration de Gestion des API et Event Hubs
  * [Référence d’entité d’enregistreur](https://docs.microsoft.com/rest/api/apimanagement/loggers)
  * [Référence de stratégie log-to-eventhub](https://docs.microsoft.com/azure/api-management/api-management-advanced-policies#log-to-eventhub)
  * [Surveiller vos API avec gestion des API Azure, les hubs d’événements et Runscope](api-management-log-to-eventhub-sample.md)    

## <a name="watch-a-video-walkthrough"></a>Regarder une procédure pas à pas en vidéo
> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Integrate-Azure-API-Management-with-Event-Hubs/player]
>
>

[publisher-portal]: ./media/api-management-howto-log-event-hubs/publisher-portal.png
[create-event-hub]: ./media/api-management-howto-log-event-hubs/create-event-hub.png
[event-hub-connection-string]: ./media/api-management-howto-log-event-hubs/event-hub-connection-string.png
[event-hub-dashboard]: ./media/api-management-howto-log-event-hubs/event-hub-dashboard.png
[receiving-policy]: ./media/api-management-howto-log-event-hubs/receiving-policy.png
[sending-policy]: ./media/api-management-howto-log-event-hubs/sending-policy.png
[event-hub-policy]: ./media/api-management-howto-log-event-hubs/event-hub-policy.png
[add-policy]: ./media/api-management-howto-log-event-hubs/add-policy.png
