---
title: connecteur aaaWebhook pour Azure Logic Apps | Documents Microsoft
description: "Actions de webhook toouse et déclencheurs tooperform façon dont le filtre de tableau à partir d’applications de la logique"
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
tags: connectors
ms.assetid: 71775384-6c3a-482c-a484-6624cbe4fcc7
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/21/2016
ms.author: jehollan; LADocs
ms.openlocfilehash: b2dee12750f3f20f10e7b257da05a79f28f90f43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-webhook-connector"></a>Prise en main connecteur de webhook hello

Avec l’action de webhook hello et déclencheur, vous pouvez démarrer, suspendre et reprendre des flux tooperform ces tâches :

* Créer un déclenchement à partir d’[Azure Event Hub](https://github.com/logicappsio/EventHubAPI) lorsqu’un élément est reçu
* Attendre une approbation avant de poursuivre un flux de travail.

En savoir plus sur [comment toocreate API personnalisées qui prennent en charge un webhook](../logic-apps/logic-apps-create-api-app.md).

## <a name="use-hello-webhook-trigger"></a>Utiliser des déclencheurs de webhook hello

Un [*déclencheur*](connectors-overview.md) est un événement qui démarre un flux de travail d’application logique. Un déclencheur webhook est basé sur un événement et ne repose pas sur l’interrogation de nouveaux éléments. Comme hello [déclencheur de la demande](connectors-native-reqres.md), hello logique application déclenche hello instantanée qu’un événement se produit. déclencheur de webhook Hello enregistre un *URL de rappel* tooa service et utilise cette application logique de URL toofire hello en tant que nécessaire.

Voici un exemple qui montre comment déclencher des tooset un HTTP Bonjour Concepteur de logique d’application. Hello étapes supposent que vous avez déjà déployé ou accédez à une API qui suit hello [webhook s’abonner et annuler l’abonnement de modèle dans les applications logique](../logic-apps/logic-apps-create-api-app.md#webhook-triggers). Hello s’abonner appel est effectué chaque fois qu’une application de logique est enregistrée avec un nouveau webhook ou d'où tooenabled désactivé. Hello vous désabonner d’appel est effectué quand un déclencheur de webhook application logique est supprimé et enregistré ou d'où toodisabled activé.

**déclencheur de webhook tooadd hello**

1. Ajouter hello **HTTP Webhook** déclencheur en tant que première étape de hello dans une application logique.
2. Renseignez les paramètres hello pour hello webhook s’abonner et annuler l’abonnement d’appels.

   Cette étape suit hello même modèle en tant que hello [action HTTP](connectors-native-http.md) format.

     ![Déclencheur HTTP](./media/connectors-native-webhook/using-trigger.png)

3. Ajoutez au moins une action.
4. Cliquez sur **enregistrer** toopublish hello logique application. Cette hello d’appels étape s’abonner à point de terminaison avec hello rappel URL nécessaire tootrigger cette application logique.
5. Chaque fois que hello service rend un `HTTP POST` toohello URL de rappel, hello se déclenche d’application logique et inclut toutes les données transmises dans la demande de hello.

## <a name="use-hello-webhook-action"></a>Utilisez l’action de webhook hello

Un [ *action* ](connectors-overview.md) est une opération effectuée par le workflow hello défini dans une application logique. Une action webhook inscrit un *URL de rappel* avec un service et attend jusqu'à ce que l’URL de hello est appelée avant la reprise. Hello [« Envoyer un courrier électronique l’approbation »](connectors-create-api-office365-outlook.md) est un exemple d’un connecteur qui suit ce modèle. Vous pouvez étendre ce modèle à n’importe quel service via une action de webhook hello. 

Voici un exemple qui montre comment tooset une action de webhook dans hello Concepteur de logique d’application. Ces étapes supposent que vous avez déjà déployé ou accédez à une API qui suit hello [webhook s’abonner et annuler l’abonnement utilisée dans les applications de la logique de modèle](../logic-apps/logic-apps-create-api-app.md#webhook-actions). Hello s’abonner appel est fait quand une application logique exécute l’action de webhook hello. Hello vous désabonner d’appel est fait quand une exécution est annulée lors de l’attente d’une réponse, ou avant la logique de hello application arrive à expiration.

**tooadd une action webhook**

1. Choisissez **Nouvelle étape** > **Ajouter une action**.

2. Dans la zone de recherche de hello, tapez « webhook » toofind hello **HTTP Webhook** action.

    ![Sélectionner l’action de requête](./media/connectors-native-webhook/using-action-1.png)

3. Entrer les paramètres hello pour hello webhook s’abonner et annuler l’abonnement d’appels

   Cette étape suit hello même modèle en tant que hello [action HTTP](connectors-native-http.md) format.

     ![Terminer l’action de requête](./media/connectors-native-webhook/using-action-2.png)
   
   Lors de l’exécution, hello logique application appels hello s’abonner à point de terminaison après avoir atteint cette étape.

4. Cliquez sur **enregistrer** toopublish hello logique application.

## <a name="technical-details"></a>Détails techniques

Voici plus d’informations sur les déclencheurs hello et les actions que webhook prend en charge.

## <a name="webhook-triggers"></a>Déclencheurs Webhook

| Action | Description |
| --- | --- |
| HTTP Webhook |Abonnez-vous à un service de tooa des URL de rappel qui peut appeler hello URL toofire application logique en fonction des besoins. |

### <a name="trigger-details"></a>Détails du déclencheur

#### <a name="http-webhook"></a>HTTP Webhook

Abonnez-vous à un service de tooa des URL de rappel qui peut appeler hello URL toofire application logique en fonction des besoins.
Une * signifie que le champ est obligatoire.

| Display Name | Nom de la propriété | Description |
| --- | --- | --- |
| Méthode d’abonnement* |method |Toouse méthode HTTP pour la demande subscribe |
| URI d’abonnement* |URI |Toouse URI HTTP pour la demande subscribe |
| Méthode de résiliation d’abonnement* |method |Toouse de méthode HTTP pour la demande d’annulation d’abonnement |
| URI de résiliation d’abonnement* |URI |Toouse URI HTTP pour la demande d’annulation d’abonnement |
| Corps d’abonnement |body |Corps de la demande HTTP pour s’abonner |
| En-têtes de l’abonnement |headers |En-têtes de la demande HTTP pour s’abonner |
| Authentification de l’abonnement |authentication |Toouse de l’authentification HTTP pour s’abonner. Voir [Connecteur HTTP](connectors-native-http.md#authentication) pour plus d’informations |
| Corps de résiliation d’abonnement |body |Corps de la demande HTTP de résiliation d’abonnement |
| En-têtes de résiliation d’abonnement |headers |En-têtes de la demande HTTP de résiliation d’abonnement |
| Authentification de la résiliation d’abonnement |authentication |Toouse de l’authentification HTTP pour annuler l’abonnement. Voir [Connecteur HTTP](connectors-native-http.md#authentication) pour plus d’informations |

**Détails des résultats**

Requête Webhook

| Nom de la propriété | Type de données | Description |
| --- | --- | --- |
| headers |objet |En-têtes de requête Webhook |
| body |objet |Objet de la requête Webhook |
| Code d’état |int |Code d’état de la requête Webhook |

## <a name="webhook-actions"></a>Actions de webhook

| Action | Description |
| --- | --- |
| HTTP Webhook |Abonnez-vous à un service de tooa des URL de rappel qui peut appeler hello URL tooresume une étape du flux de travail en fonction des besoins. |

### <a name="action-details"></a>Détails de l’action

#### <a name="http-webhook"></a>HTTP Webhook

Abonnez-vous à un service de tooa des URL de rappel qui peut appeler hello URL tooresume une étape du flux de travail en fonction des besoins.
Une * signifie que le champ est obligatoire.

| Display Name | Nom de la propriété | Description |
| --- | --- | --- |
| Méthode d’abonnement* |method |Toouse méthode HTTP pour la demande subscribe |
| URI d’abonnement* |URI |Toouse URI HTTP pour la demande subscribe |
| Méthode de résiliation d’abonnement* |method |Toouse de méthode HTTP pour la demande d’annulation d’abonnement |
| URI de résiliation d’abonnement* |URI |Toouse URI HTTP pour la demande d’annulation d’abonnement |
| Corps d’abonnement |body |Corps de la demande HTTP pour s’abonner |
| En-têtes de l’abonnement |headers |En-têtes de la demande HTTP pour s’abonner |
| Authentification de l’abonnement |authentication |Toouse de l’authentification HTTP pour s’abonner. Voir [Connecteur HTTP](connectors-native-http.md#authentication) pour plus d’informations |
| Corps de résiliation d’abonnement |body |Corps de la demande HTTP de résiliation d’abonnement |
| En-têtes de résiliation d’abonnement |headers |En-têtes de la demande HTTP de résiliation d’abonnement |
| Authentification de la résiliation d’abonnement |authentication |Toouse de l’authentification HTTP pour annuler l’abonnement. Voir [Connecteur HTTP](connectors-native-http.md#authentication) pour plus d’informations |

**Détails des résultats**

Requête Webhook

| Nom de la propriété | Type de données | Description |
| --- | --- | --- |
| headers |objet |En-têtes de requête Webhook |
| body |objet |Objet de la requête Webhook |
| Code d’état |int |Code d’état de la requête Webhook |

## <a name="next-steps"></a>Étapes suivantes

* [Créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md)
* [Rechercher d’autres connecteurs](apis-list.md)