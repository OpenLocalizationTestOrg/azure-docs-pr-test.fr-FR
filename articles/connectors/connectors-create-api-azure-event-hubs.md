---
title: "aaaSet le moniteur d’événement avec des concentrateurs d’événements Azure pour Azure Logic Apps | Documents Microsoft"
description: "Surveiller les événements de tooreceive de flux de données et d’envoyer des événements pour les applications de la logique d’Azure avec Azure Event Hubs"
services: logic-apps
keywords: "flux de données, observateur d’événements, event hubs"
author: ecfan
manager: anneta
editor: 
documentationcenter: 
tags: connectors
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/31/2017
ms.author: estfan; LADocs
ms.openlocfilehash: 4aad2c2ac1134b4d4d440019b4773559e49be122
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-receive-and-send-events-with-hello-event-hubs-connector"></a>Surveiller, recevoir et envoyer des événements avec le connecteur de concentrateurs d’événements hello

tooset d’un observateur d’événements afin que votre application logique peut détecter les événements de recevoir des événements et envoyer des événements, connecter tooan [concentrateur d’événements Azure](https://azure.microsoft.com/services/event-hubs) à partir de votre application logique. En savoir plus sur [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md).

## <a name="requirements"></a>Configuration requise

* Vous avez toohave un [espace de noms de concentrateurs d’événements et de concentrateur d’événements](../event-hubs/event-hubs-create.md) dans Azure. En savoir plus [comment toocreate un espace de noms de concentrateurs d’événements et d’un concentrateur d’événements](../event-hubs/event-hubs-create.md). 

* toouse [n’importe quel connecteur](https://docs.microsoft.com/azure/connectors/apis-list) dans votre logique d’application, vous avez toocreate une logique application tout d’abord. En savoir plus [comment une application de la logique de toocreate](../logic-apps/logic-apps-create-a-logic-app.md).

<a name="permissions-connection-string"></a>
## <a name="check-event-hubs-namespace-permissions-and-find-hello-connection-string"></a>Vérifier les autorisations d’espace de noms de concentrateurs d’événements et recherchez la chaîne de connexion hello

Pour votre tooaccess d’application logique, un service, vous avez toocreate un [ *connexion* ](./connectors-overview.md) entre votre logique application hello service et, si vous n’avez pas déjà. Cette connexion autorise de vos données tooaccess d’application logique.
Pour votre tooaccess d’application logique votre concentrateur d’événements, vous avez toohave **gérer** autorisations et la chaîne de connexion de hello pour votre espace de noms de concentrateurs d’événements.

toocheck vos autorisations et la chaîne de connexion get hello, procédez comme suit.

1.  Connectez-vous à toohello [portail Azure](https://portal.azure.com "portail Azure"). 

2.  Passez les concentrateurs d’événements tooyour *espace de noms*, pas hello concentrateur d’événements spécifique. Sur le panneau espace de noms de hello, sous **paramètres**, choisissez **les stratégies d’accès partagé**. Sous **Revendications**, vérifiez que vous disposez des autorisations **Gérer** pour cet espace de noms.

    ![Gérer les autorisations pour votre espace de noms Event Hubs](./media/connectors-create-api-azure-event-hubs/event-hubs-namespace.png)

3.  chaîne de connexion toocopy hello pour l’espace de noms du service Event Hubs hello, choisissez **RootManageSharedAccessKey**. Tooyour suivant principal clé de chaîne de connexion, choisissez le bouton de copie hello.

    ![Copier la chaîne de connexion d’espace de noms Event Hubs](media/connectors-create-api-azure-event-hubs/find-event-hub-namespace-connection-string.png)

    > [!TIP]
    > tooconfirm si votre chaîne de connexion est associé à votre espace de noms de concentrateurs d’événements ou à un concentrateur d’événements spécifiques, vérifiez la chaîne de connexion hello pour hello `EntityPath` paramètre. Si vous trouvez pas ce paramètre, chaîne de connexion hello est pour un concentrateur d’événements « entité » spécifique et n’est pas toouse de bonne chaîne hello avec votre application logique.

4.  Maintenant lorsque vous êtes invité à entrer pour les informations d’identification après l’ajout d’une application de la logique de tooyour déclencheur ou une action concentrateurs d’événements, vous pouvez vous connecter à espace de noms tooyour concentrateurs d’événements. Donnez un nom à votre connexion, entrez la chaîne de connexion hello que vous avez copié, choisissez **créer**.

    ![Entrer la chaîne de connexion pour un espace de noms Event Hubs](./media/connectors-create-api-azure-event-hubs/event-hubs-connection.png)

    Après avoir créé votre connexion, nom de la connexion hello doit apparaître dans hello concentrateurs d’événements déclencheur ou une action. 
    Vous pouvez ensuite poursuivre hello les autres étapes de votre application logique.

    ![Connexion d’espace de noms Event Hubs créée](./media/connectors-create-api-azure-event-hubs/event-hubs-connection-created.png)

## <a name="start-workflow-when-your-event-hub-receives-new-events"></a>Démarrer le workflow lorsque votre hub Event Hubs reçoit de nouveaux événements

Un [*déclencheur*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) désigne un événement qui démarre un workflow dans votre application logique. Pour démarrer un flux de travail lorsque de nouveaux événements sont envoyés tooyour concentrateur d’événements, procédez comme suit pour ajouter le déclencheur hello qui détecte cet événement.

1.  Bonjour [portail Azure](https://portal.azure.com "portail Azure"), accédez tooyour les application logique existante ou créer une application de logique vide.

2.  Dans la zone de recherche hello hello Concepteur d’application logique, entrez `event hubs` pour votre filtre. Sélectionnez ce déclencheur : **When events are available in Event Hub (Lorsque les événements sont disponibles dans un hub Event Hubs)**

    ![Sélectionner le déclencheur lorsque votre hub Event Hubs reçoit de nouveaux événements](./media/connectors-create-api-azure-event-hubs/find-event-hubs-trigger.png)

    Si vous ne disposez pas d’un espace de noms de connexion tooyour concentrateurs d’événements, vous êtes invité à entrer toocreate maintenant cette connexion. Donnez un nom à votre connexion et entrez la chaîne de connexion hello pour votre espace de noms de concentrateurs d’événements. 
    Si nécessaire, en savoir plus [comment toofind votre chaîne de connexion](#permissions-connection-string).

    ![Entrer la chaîne de connexion pour un espace de noms Event Hubs](./media/connectors-create-api-azure-event-hubs/event-hubs-connection.png)

    Après avoir créé la connexion de hello, hello paramètres pour hello **lorsqu’un événement dans disponibles dans un concentrateur d’événements** déclencheur s’affichent.

    ![Paramètres du déclencheur lorsque votre hub Event Hubs reçoit de nouveaux événements](./media/connectors-create-api-azure-event-hubs/event-hubs-trigger.png)

3.  Entrez ou sélectionnez le nom de hello pour hello concentrateur d’événements que vous souhaitez toomonitor. Sélectionnez la fréquence de hello et l’intervalle pour la fréquence à laquelle vous voulez toocheck hello concentrateur d’événements.

    > [!TIP]
    > toooptionally sélectionner un groupe de consommateurs pour la lecture des événements, choisissez **Show advanced options**. 

    ![Spécifier un hub Event Hubs ou un groupe de consommateurs](./media/connectors-create-api-azure-event-hubs/event-hubs-trigger-details.png)

    Vous avez maintenant configuré un toostart déclencheur un flux de travail pour votre application logique. 
    Votre application logique vérifie hello spécifié concentrateur d’événements selon une planification hello que vous définissez. 
    Si votre application détecte les nouveaux événements Bonjour concentrateur d’événements, déclencheur de hello exécute les autres actions ou des déclencheurs dans votre application logique.

## <a name="send-events-tooyour-event-hub-from-your-logic-app"></a>Envoyer des événements tooyour concentrateur d’événements à partir de votre application logique

Une [*action*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) est une tâche effectuée par le flux de travail de votre application logique. Après avoir ajouté une application de la logique de déclencheur tooyour, vous pouvez ajouter un opérateur de tooperform action avec les données générées par ce déclencheur. toosend un tooyour événement concentrateur d’événements à partir de votre application logique, procédez comme suit.

1.  Dans le Concepteur d’application logique, sous le déclencheur de votre application logique, sélectionnez **Nouvelle étape** > **Ajouter une action**.

    ![Cliquez sur Nouvelle étape, puis sur Ajouter une action](./media/connectors-create-api-azure-event-hubs/add-action.png)

    Vous pouvez maintenant rechercher et sélectionner une action tooperform. 
    Bien que vous puissiez sélectionner toute action, pour cet exemple, nous souhaitons les événements toosend action hello concentrateurs d’événements.

2.  Dans la zone de recherche de hello, entrez `event hubs` pour votre filtre.
Sélectionnez cette action : **Envoyer un événement**

    ![Sélectionnez l’action « Event Hubs - Envoyer un événement »](./media/connectors-create-api-azure-event-hubs/find-event-hubs-action.png)

3.  Entrez les détails de hello requis pour l’événement hello, telles que nom hello pour hello où vous souhaitez les événements de hello toosend concentrateur d’événements. Entrez tous les autres détails sur l’événement hello, tel que le contenu de cet événement facultatif.

    > [!TIP]
    > toooptionally spécifier la partition de concentrateur d’événements hello où toosend hello événement, choisissez **Show advanced options**. 

    ![Entrez le nom du hub Event Hubs et les détails facultatifs de l’événement](./media/connectors-create-api-azure-event-hubs/event-hubs-send-event-action.png)

6.  Enregistrez vos modifications.

    ![Enregistrer votre application logique](./media/connectors-create-api-azure-event-hubs/save-logic-app.png)

    Vous avez maintenant définir des événements de toosend action à partir de votre application logique. 

## <a name="connector-specific-details"></a>Détails spécifiques du connecteur

Afficher les déclencheurs et les actions définies dans les swagger hello et également voir les limites Bonjour [détails du connecteur](/connectors/eventhubs/). 

## <a name="get-help"></a>Obtenir de l’aide

tooask questions, répondez aux questions et voir les autres utilisateurs Azure Logic Apps font, visitez hello [forum de Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).

toohelp améliorer Logic Apps et connecteurs, voter pour ou envoyer vos idées à hello [site de commentaires utilisateur Logic Apps](http://aka.ms/logicapps-wish).

## <a name="next-steps"></a>Étapes suivantes

*  [Rechercher d’autres connecteurs pour Azure Logic Apps](./apis-list.md)