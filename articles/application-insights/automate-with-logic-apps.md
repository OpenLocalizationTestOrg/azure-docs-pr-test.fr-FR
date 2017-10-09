---
title: "aaaAutomate Azure Application Insights traite à l’aide de Logic Apps."
description: "Découvrez comment vous pouvez automatiser des processus reproductibles rapidement en ajoutant l’application logique de hello Application Insights connecteur tooyour."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: bwren
ms.openlocfilehash: 8565aadf0644ffb10da8a0964821901907db2e27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="automate-application-insights-processes-by-using-logic-apps"></a>Automatiser les processus Application Insights en utilisant Logic Apps

Trouver vous-même exécution répétée hello mêmes requêtes sur votre toocheck de données de télémétrie si votre service fonctionne correctement ? Est vous tooautomate recherchent ces requêtes pour rechercher des tendances et des anomalies et de générer vos propres workflows autour d’elles ? le connecteur Hello Azure Application Insights (preview) pour les applications de la logique est un outil hello à cet effet.

Avec cette intégration, vous pouvez automatiser de nombreux processus sans écrire la moindre ligne de code. Vous pouvez créer une application de logique hello Application Insights connecteur tooquickly automatiser n’importe quel processus d’Application Insights. 

Vous pouvez également ajouter des actions. fonctionnalité de Logic Apps Hello du Service d’applications Azure rend des centaines d’actions disponibles. Par exemple, en utilisant une application logique, vous pouvez automatiquement envoyer une notification par e-mail ou créer un bogue dans Visual Studio Team Services. Vous pouvez également utiliser une des hello nombreux disponible [modèles](https://docs.microsoft.com/azure/logic-apps/logic-apps-use-logic-app-templates) toohelp accélérer hello de créer votre logique d’application. 

## <a name="create-a-logic-app-for-application-insights"></a>Créer une application logique pour Application Insights

Dans ce didacticiel, vous découvrez comment toocreate une application de logique qui utilise hello Analytique autocluster algorithme toogroup les attributs dans les données de salutation pour une application web. flux de Hello envoie automatiquement les résultats de hello par courrier électronique, qu’un exemple de comment vous pouvez utiliser Application Insights Analytique et Logic Apps ensemble. 

### <a name="step-1-create-a-logic-app"></a>Étape 1 : Créer une application logique
1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Bonjour **nouveau** volet, sélectionnez **Web + Mobile**, puis sélectionnez **application logique**.

    ![Fenêtre Nouvelle application logique](./media/automate-with-logic-apps/logicapp1.png)

### <a name="step-2-create-a-trigger-for-your-logic-app"></a>Étape 2 : Créer un déclencheur pour votre application logique
1. Bonjour **Concepteur d’application logique** fenêtre, sous **commencer par un déclencheur commun**, sélectionnez **périodicité**.

    ![Fenêtre Concepteur d’application logique](./media/automate-with-logic-apps/logicapp2.png)

2. Bonjour **fréquence** boîte, sélectionnez **jour** , puis, dans hello **intervalle** , tapez **1**.

    ![Fenêtre « Récurrence » du Concepteur d’application logique](./media/automate-with-logic-apps/step2b.png)

### <a name="step-3-add-an-application-insights-action"></a>Étape 3 : Ajouter une action Application Insights
1. Cliquez sur **Nouvelle étape**, puis sur **Ajouter une action**.

2. Bonjour **choisir une action** zone de recherche, tapez **Azure Application Insights**.

3. Sous **Actions**, cliquez sur **Azure Application Insights – Visualize Analytics query Preview** (Azure Application Insights – Visualiser la requête Analytics Préversion).

    ![Fenêtre de « Choisir une action » du Concepteur d’application logique](./media/automate-with-logic-apps/flow2.png)

### <a name="step-4-connect-tooan-application-insights-resource"></a>Étape 4 : Connecter des ressources d’Application Insights tooan

toocomplete cette étape, vous avez besoin d’un ID d’application et une clé d’API pour votre ressource. Vous pouvez les récupérer à partir de hello portail Azure, comme indiqué dans hello suivant schéma :

![ID d’application Bonjour portail Azure](./media/automate-with-logic-apps/appid.png) 

Fournissez un nom pour votre connexion, un ID de l’application hello et une clé d’API hello.

![Fenêtre de connexion de flux du Concepteur d’application logique](./media/automate-with-logic-apps/flow3.png)

### <a name="step-5-specify-hello-analytics-query-and-chart-type"></a>Étape 5 : Spécifier hello les requête Analytique et type de graphique
Bonjour l’exemple suivant, les requêtes hello sélectionne des demandes de hello a échoué dans le dernier jour de hello et les met en corrélation avec les exceptions qui se sont produites dans le cadre de l’opération de hello. Analytique met en corrélation les demandes hello a échoué, basées sur l’identificateur hello identifiant_opération. requête de Hello puis segmente les résultats de hello en utilisant l’algorithme d’autocluster hello. 

Lorsque vous créez vos propres requêtes, vérifier qu’ils fonctionnent correctement dans Analytique avant d’ajouter celui-ci tooyour flux.

1. Bonjour **requête** zone, ajouter hello suivant les requête Analytique : 

    ```
    requests
    | where timestamp > ago(1d)
    | where success == "False"
    | project name, operation_Id
    | join ( exceptions
        | project problemId, outerMessage, operation_Id
    ) on operation_Id
    | evaluate autocluster()
    ```

2. Bonjour **Type de graphique** boîte, sélectionnez **Html Table**.

    ![Fenêtre de configuration de requête Analytics](./media/automate-with-logic-apps/flow4.png)

### <a name="step-6-configure-hello-logic-app-toosend-email"></a>Étape 6 : Configurer la messagerie de toosend application hello logique

1. Cliquez sur **Nouvelle étape**, puis sélectionnez **Ajouter une action**.

2. Dans la zone de recherche de hello, tapez **Outlook Office 365**.

3. Cliquez sur **Office 365 Outlook – Envoyer un message électronique**.

    ![Sélection d’Office 365 Outlook](./media/automate-with-logic-apps/flow2b.png)

4. Bonjour **envoyer un courrier électronique** fenêtre, hello suivant :

   a. Tapez l’adresse de messagerie hello du destinataire de hello.

   b. Entrez un objet pour le courrier électronique de hello.

   c. Cliquez n’importe où dans hello **corps** zone, hello dynamique contenu menu qui s’ouvre à droite de hello, puis **corps**.

   d. Cliquez sur **Afficher les options avancées**.

      ![Configuration d’Office 365 Outlook](./media/automate-with-logic-apps/flow5.png)

5. Dans le menu de contenu dynamique hello, procédez comme hello suivant :

    a. Sélectionnez **Nom de la pièce jointe**.

    b. Sélectionnez **Attachment Content** (Contenu de la pièce jointe).
    
    c. Bonjour **HTML** boîte, sélectionnez **Oui**.

      ![Écran de configuration d’e-mail Office 365](./media/automate-with-logic-apps/flow7.png)

### <a name="step-7-save-and-test-your-logic-app"></a>Étape 7 : Enregistrer et tester votre application logique
* Cliquez sur **enregistrer** toosave vos modifications.

Vous pouvez attendre d’application logique de hello déclencheur toorun hello, ou vous pouvez exécuter immédiatement hello logique application en sélectionnant **exécuter**.

![Écran de création d’application logique](./media/automate-with-logic-apps/step7.png)

Lorsque votre application logique s’exécute, les destinataires hello que vous avez spécifié dans la liste de messagerie hello recevra un e-mail qui ressemble à hello suivantes :

![Message électronique de l’application logique](./media/automate-with-logic-apps/flow9.png)

## <a name="next-steps"></a>Étapes suivantes

- Apprenez-en plus sur la création de [requêtes Analytics](app-insights-analytics-using.md).
- Découvrez plus en détail les [applications logiques](https://docs.microsoft.com/azure/logic-apps/logic-apps-what-are-logic-apps).



<!--Link references-->





