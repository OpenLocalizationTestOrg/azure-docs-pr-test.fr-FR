---
title: aaaAutomate Azure Application Insights traite avec Microsoft Flow
description: "Découvrez comment vous pouvez utiliser Microsoft Flow tooquickly automatiser des processus reproductibles à l’aide du connecteur d’Application Insights hello."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/25/2017
ms.author: bwren
ms.openlocfilehash: b34488a6b8b8b0a6add960a67f1426cbbbc13552
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="automate-azure-application-insights-processes-with-hello-connector-for-microsoft-flow"></a>Automatiser les processus d’Application Azure Insights avec le connecteur de hello pour Microsoft Flow

Trouver vous-même exécution répétée des mêmes requêtes hello sur votre toocheck de données de télémétrie votre service fonctionne correctement ? Est vous tooautomate recherchent ces requêtes pour rechercher des tendances et des anomalies et de générer vos propres workflows autour d’elles ? le connecteur Hello Azure Application Insights (preview) pour Microsoft Flow est un outil hello à ces fins.

Avec cette intégration, vous pouvez désormais automatiser de nombreux processus sans écrire la moindre ligne de code. Après avoir créé un flux à l’aide d’une action d’Application Insights, flux de hello s’exécute automatiquement votre requête d’Application Insights Analytique. 

Vous pouvez également ajouter des actions. Microsoft Flow met à votre disposition des centaines d’actions. Par exemple, vous pouvez utiliser Microsoft Flow tooautomatically envoyer une notification par courrier électronique ou créer un bogue dans Visual Studio Team Services. Vous pouvez également utiliser une des hello nombreux [modèles](https://ms.flow.microsoft.com/en-us/connectors/shared_applicationinsights/?slug=azure-application-insights) qui sont disponibles pour le connecteur hello pour Microsoft Flow. Ces modèles accélèrent hello de création d’un flux. 

<!--hello Application Insights connector also works with [Azure Power Apps](https://powerapps.microsoft.com/en-us/) and [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/?v=17.23h). --> 

## <a name="create-a-flow-for-application-insights"></a>Créer un flux pour Application Insights

Dans ce didacticiel, vous allez apprendre comment toocreate un flux qui utilise hello Analytique auto-cluster algorithme toogroup les attributs dans les données de salutation pour une application web. flux de Hello envoie automatiquement les résultats de hello par courrier électronique, qu’un exemple de la façon dont vous pouvez utiliser Microsoft Flow et Application Insights Analytique ensemble. 

### <a name="step-1-create-a-flow"></a>Étape 1 : Créer un flux
1. Connectez-vous trop[Microsoft Flow](http://flow.microsoft.com), puis sélectionnez **flux Mes**.
2. Cliquez sur **Créer un flux à partir de rien**.

### <a name="step-2-create-a-trigger-for-your-flow"></a>Étape 2 : Créer un déclencheur pour votre flux
1. Sélectionnez **Planifier**, puis **Planification - Récurrence**.
2. Bonjour **fréquence** boîte, sélectionnez **jour**et Bonjour **intervalle** , entrez **1**.

    ![Boîte de dialogue du déclencheur de flux Microsoft Flow](./media/app-insights-automate-with-flow/flow1.png)


### <a name="step-3-add-an-application-insights-action"></a>Étape 3 : Ajouter une action Application Insights
1. Cliquez sur **Nouvelle étape**, puis sur **Ajouter une action**.
2. Recherchez **Azure Application Insights**.
3. Cliquez sur **Azure Application Insights – Visualize Analytics query Preview** (Azure Application Insights – Visualiser la requête Analytics Préversion).

    ![Fenêtre d’exécution de la requête Analytics](./media/app-insights-automate-with-flow/flow2.png)

### <a name="step-4-connect-tooan-application-insights-resource"></a>Étape 4 : Connecter des ressources d’Application Insights tooan

toocomplete cette étape, vous avez besoin d’un ID d’application et une clé d’API pour votre ressource. Vous pouvez les récupérer à partir de hello portail Azure, comme indiqué dans hello suivant schéma :

![ID d’application Bonjour portail Azure](./media/app-insights-automate-with-flow/appid.png) 

- Fournissez un nom pour votre connexion, ainsi que de la clé API et ID d’application hello.

    ![Fenêtre de connexion Microsoft Flow](./media/app-insights-automate-with-flow/flow3.png)

### <a name="step-5-specify-hello-analytics-query-and-chart-type"></a>Étape 5 : Spécifier hello les requête Analytique et type de graphique
Cet exemple de requête sélectionne des demandes de hello a échoué dans le dernier jour de hello et les met en corrélation avec les exceptions qui se sont produites dans le cadre de l’opération de hello. Analytique les met en corrélation basée sur l’identificateur hello identifiant_opération. requête de Hello puis segmente les résultats de hello en utilisant l’algorithme d’autocluster hello. 

Lorsque vous créez vos propres requêtes, vérifier qu’ils fonctionnent correctement dans Analytique avant d’ajouter celui-ci tooyour flux.

- Ajouter hello suivant la requête de l’Analytique, puis sélectionnez le type de graphique de table HTML hello. 

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
    
    ![Fenêtre de configuration de requête Analytics](./media/app-insights-automate-with-flow/flow4.png)

### <a name="step-6-configure-hello-flow-toosend-email"></a>Étape 6 : Configurer la messagerie de hello flux toosend

1. Cliquez sur **Nouvelle étape**, puis sur **Ajouter une action**.
2. Recherchez **Office 365 Outlook**.
3. Cliquez sur **Office 365 Outlook – Envoyer un message électronique**.

    ![Fenêtre de sélection d’Office 365 Outlook](./media/app-insights-automate-with-flow/flow2b.png)

4. Bonjour **envoyer un courrier électronique** fenêtre, hello suivant :

   a. Tapez l’adresse de messagerie hello du destinataire de hello.

   b. Entrez un objet pour le courrier électronique de hello.

   c. Cliquez n’importe où dans hello **corps** zone, hello dynamique contenu menu qui s’ouvre à droite de hello, puis **corps**.

   d. Cliquez sur **Afficher les options avancées**.

    ![Configuration d’Office 365 Outlook](./media/app-insights-automate-with-flow/flow5.png)

5. Dans le menu de contenu dynamique hello, procédez comme hello suivant :

    a. Sélectionnez **Nom de la pièce jointe**.

    b. Sélectionnez **Attachment Content** (Contenu de la pièce jointe).
    
    c. Bonjour **HTML** boîte, sélectionnez **Oui**.

    ![Fenêtre de configuration d’e-mail Office 365](./media/app-insights-automate-with-flow/flow7.png)

### <a name="step-7-save-and-test-your-flow"></a>Étape 7 : Enregistrer et tester votre flux
- Bonjour **nom de flux** zone, ajouter un nom pour votre flux, puis cliquez sur **créer un flux**.

    ![Fenêtre de création de flux](./media/app-insights-automate-with-flow/flow8.png)

Vous pouvez attendre hello déclencheur toorun cette action, ou vous pouvez exécuter des flux de hello immédiatement par [le déclencheur hello en cours d’exécution de la demande](https://flow.microsoft.com/blog/run-now-and-six-more-services/).

Exécution de flux de hello hello que vous avez spécifié dans la liste de messagerie hello destinataires un message électronique qui ressemble à hello suivantes :

![Exemple de message électronique](./media/app-insights-automate-with-flow/flow9.png)


## <a name="next-steps"></a>Étapes suivantes

- Découvrez la création de [requêtes Analytics](app-insights-analytics-using.md).
- Découvrez [Microsoft Flow](https://ms.flow.microsoft.com).



<!--Link references-->





