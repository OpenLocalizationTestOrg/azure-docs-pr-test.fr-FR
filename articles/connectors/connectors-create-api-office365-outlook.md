---
title: connecteur de Outlook Office 365 aaaAdd hello dans vos applications logiques | Documents Microsoft
description: "Créer des applications de logique avec Office 365 connecteur tooenable une interaction avec Office 365. Par exemple : création, modification et mise à jour de contacts et d’éléments de calendrier."
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: b2f6cc2c-bba2-493a-b0ba-841785462a80
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 86a573c9c54701de3d3f0500d19eaf545e0710ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-office-365-outlook-connector"></a>Prise en main hello Office 365 Outlook connector
connecteur d’Outlook Office 365 Hello permet l’interaction avec Outlook pour Office 365. Utiliser ce connecteur toocreate, les modifier et les contacts de la mise à jour et les éléments de calendrier et aussi obtenir, envoyer et répondre tooemail.

Avec Office 365 Outlook, vous pouvez effectuer les opérations suivantes :

* Créer votre flux de travail à l’aide des fonctionnalités de messagerie et de calendrier hello dans Office 365. 
* Utilisez déclenche toostart votre flux de travail lorsqu’il existe un nouvel e-mail, lorsqu’un élément de calendrier est mis à jour et bien plus encore.
* Utiliser des actions toosend un message électronique, créer un nouvel événement de calendrier et bien plus encore. Par exemple, lorsqu’il existe un nouvel objet dans Salesforce (un déclencheur), envoyer un courrier électronique tooyour Outlook Office 365 (action). 

Cette rubrique vous montre comment toouse hello Connecteur Outlook Office 365 dans une application logique, et également les listes hello déclencheurs et actions.

> [!NOTE]
> Cette version de l’article de hello s’applique tooLogic applications mise à disposition générale (GA).
> 
> 

toolearn en savoir plus sur les applications de la logique, consultez [quelles sont les applications logique](../logic-apps/logic-apps-what-are-logic-apps.md) et [créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-toooffice-365"></a>Se connecter tooOffice 365
Avant que votre application logique peut accéder à n’importe quel service, vous créez tout d’abord un *connexion* toohello service. Une connexion permet d’assurer la connectivité entre une application logique et un autre service. Par exemple, tooconnect tooOffice 365 Outlook, vous devez tout d’abord un Office 365 *connexion*. toocreate une connexion, entrez des informations d’identification de hello que vous utilisez normalement le service de hello tooaccess tooconnect pour vous le souhaitez. Avec Outlook Office 365, entrez tooyour des informations d’identification hello connexion hello toocreate au compte Office 365.

## <a name="create-hello-connection"></a>Créer la connexion de hello
> [!INCLUDE [Steps toocreate a connection tooOffice 365](../../includes/connectors-create-api-office365-outlook.md)]
> 
> 

## <a name="use-a-trigger"></a>Utilisation d’un déclencheur
Un déclencheur est un événement qui peut être utilisé toostart hello flux de travail défini dans une application logique. Déclencheurs « interrogent « service de hello à un intervalle et la fréquence à laquelle vous souhaitez. [En savoir plus sur les déclencheurs](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

1. Dans l’application de la logique de hello, tapez « office 365 » tooget une liste des déclencheurs de hello :  
   
    ![](./media/connectors-create-api-office365-outlook/office365-trigger.png)
2. Sélectionnez **Office 365 Outlook - When an upcoming event is starting soon** (Office 365 Outlook - Quand un événement à venir est imminent). Si une connexion existe déjà, puis sélectionnez un calendrier à partir de la liste déroulante de hello.
   
    ![](./media/connectors-create-api-office365-outlook/sample-calendar.png)
   
    Si vous êtes invité à toosign dans, puis entrez le signe de hello dans Détails toocreate hello de connexion. [Créer la connexion de hello](connectors-create-api-office365-outlook.md#create-the-connection) dans cette rubrique répertorie les étapes de hello. 
   
   > [!NOTE]
   > Dans cet exemple, application de hello logique s’exécute lorsqu’un événement de calendrier est mis à jour. résultats de hello toosee de ce déclencheur, ajouter une autre action qui vous envoie un message texte. Par exemple, ajouter hello Twilio *envoyer le message* action textes lorsque hello événement de calendrier démarre des 15 dernières minutes. 
   > 
   > 
3. Sélectionnez hello **modifier** bouton et définissez hello **fréquence** et **intervalle** valeurs. Par exemple, si vous souhaitez hello déclencheur toopoll toutes les 15 minutes, puis définissez hello **fréquence** trop**Minute**et ensemble hello **intervalle** trop**15**. 
   
    ![](./media/connectors-create-api-office365-outlook/calendar-settings.png)
4. **Enregistrer** vos modifications (situé dans l’angle supérieur gauche de la barre d’outils hello). Votre application logique est enregistrée et peut être activée automatiquement.

## <a name="use-an-action"></a>Utilisation d’une action
Une action est une opération effectuée par flux de travail hello défini dans une application logique. [En savoir plus sur les actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

1. Sélectionnez le signe plus hello. Vous voyez plusieurs choix : **ajouter une action**, **ajouter une condition**, ou l’un des hello **plus** options.
   
    ![](./media/connectors-create-api-office365-outlook/add-action.png)
2. Choisissez **Ajouter une action**.
3. Dans la zone de texte hello, tapez « office 365 » tooget une liste de toutes les actions disponibles hello.
   
    ![](./media/connectors-create-api-office365-outlook/office365-actions.png) 
4. Dans notre exemple, choisissez **Office 365 Outlook - Créer un contact**. Si une connexion existe déjà, puis choisissez hello **ID de dossier**, **prénom**et d’autres propriétés :  
   
    ![](./media/connectors-create-api-office365-outlook/office365-sampleaction.png)
   
    Si vous êtes invité hello informations de connexion, puis entrez connexion de hello toocreate hello détails. [Créer la connexion de hello](connectors-create-api-office365-outlook.md#create-the-connection) dans cette rubrique décrit ces propriétés. 
   
   > [!NOTE]
   > Dans cet exemple, nous créons un contact dans Office 365 Outlook. Vous pouvez utiliser la sortie à partir d’un autre contact de hello toocreate déclencheur. Par exemple, ajouter hello SalesForce *lorsqu’un objet est créé* déclencheur. Ajoutez ensuite hello Outlook Office 365 *créer contact* action qui utilise hello SalesForce champs toocreate hello nouvelle nouveau contact dans Office 365. 
   > 
   > 
5. **Enregistrer** vos modifications (situé dans l’angle supérieur gauche de la barre d’outils hello). Votre application logique est enregistrée et peut être activée automatiquement.

## <a name="connector-specific-details"></a>Détails spécifiques du connecteur

Afficher les déclencheurs et les actions définies dans les swagger hello et également voir les limites Bonjour [détails du connecteur](/connectors/office365connector/). 

## <a name="next-steps"></a>Étapes suivantes
[Créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md). Explorer hello tous les autres connecteurs disponibles dans les applications logique à notre [liste des API](apis-list.md).

