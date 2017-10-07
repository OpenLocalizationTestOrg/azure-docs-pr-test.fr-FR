---
title: "état d’aaaCheck, configurez la journalisation et recevoir des alertes - Azure Logic Apps | Documents Microsoft"
description: "Surveiller l’état et les performances des applications logiques, journaliser les données de diagnostic et configurer les alertes"
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 5c1b1e15-3b6c-49dc-98a6-bdbe7cb75339
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 07/21/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 81f186e11a669b710f4c06089597eb5a76f7a44e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-status-set-up-diagnostics-logging-and-turn-on-alerts-for-azure-logic-apps"></a>Surveiller l’état, configurer la journalisation des diagnostics et activer les alertes pour Azure Logic Apps

Après avoir [créé et exécuté une application logique](../logic-apps/logic-apps-create-a-logic-app.md), vous pouvez vérifier son historique d’exécutions, son historique du déclencheur, son état et ses performances. Pour une surveillance des événements en temps réel et un débogage enrichi, configurez une [journalisation des diagnostics](#azure-diagnostics) pour votre application logique. De cette façon, vous pouvez [rechercher et consulter des événements](#find-events), tels que des événements de déclencheur, des événements d’exécution et des événements d’action. Vous pouvez également utiliser ces [données de diagnostic avec d’autres services](#extend-diagnostic-data), tels que Stockage Azure et Azure Event Hubs. 

configurer des notifications tooget sur les erreurs ou d’autres problèmes possibles, [alertes](#add-azure-alerts). Par exemple, vous pouvez créer une alerte qui détecte quand plus de cinq exécutions échouent en une heure. Vous pouvez également configurer la surveillance, le suivi et journalisation par programme à l’aide des [Paramètres et propriétés d’événements de Diagnostics Azure](#diagnostic-event-properties).

## <a name="view-runs-and-trigger-history-for-your-logic-app"></a>Afficher l’historique des exécutions et du déclencheur pour votre application logique

1. toofind votre application logique Bonjour [portail Azure](https://portal.azure.com), on hello menu Azure principal, choisissez **davantage de services**. Dans la zone de recherche de hello, recherchez « logic apps », puis choisissez **Logic apps**.

   ![Trouver votre application logique](./media/logic-apps-monitor-your-logic-apps/find-your-logic-app.png)

   Hello portail Azure affiche toutes les applications de la logique de hello qui sont associées à votre abonnement Azure. 

2. Sélectionnez votre application logique, puis choisissez **Vue d’ensemble**.

   Hello portail Azure affiche l’historique de l’hello s’exécute et déclencheur pour votre application logique. Par exemple :

   ![Historique des exécutions et l’historique du déclencheur de l’application logique](media/logic-apps-monitor-your-logic-apps/overview.png)

   * **Exécute l’historique** montre toutes les séries de hello pour votre application logique. 
   * **Déclencher l’historique** montre toutes les activités de déclencheur hello pour votre application logique.

   Pour des descriptions d’état, voir [Dépanner votre application logique](../logic-apps/logic-apps-diagnosing-failures.md).

   > [!TIP]
   > Si vous ne trouvez pas les données de salutation que vous attendez, sur la barre d’outils de hello, choisissez **Actualiser**.

3. tooview hello d’étapes à partir d’une exécution spécifique, sous **exécute historique**, sélectionnez qui s’exécutent. 

   Hello moniteur affiche chaque étape dans cette série. Par exemple :

   ![Actions d’une exécution spécifique](media/logic-apps-monitor-your-logic-apps/monitor-view-updated.png)

4. Choisissez de plus de détails sur hello exécuter, tooget **détails de l’exécution**. Ces informations résume les étapes de hello, état, les entrées et sorties hello pour les exécuter. 

   ![Choisir « Détails de l’exécution »](media/logic-apps-monitor-your-logic-apps/run-details.png)

   Par exemple, vous pouvez obtenir hello d’exécution **ID de corrélation**, dont vous pouvez avoir besoin lorsque vous utilisez hello [API REST pour Logic Apps](https://docs.microsoft.com/rest/api/logic).

5. tooget plus d’informations sur une étape spécifique, cliquez sur cette étape. Vous pouvez maintenant examiner des détails tels que les entrées, les sorties et les erreurs qui se sont produites pour cette étape. Par exemple :

   ![Détails de l’étape](media/logic-apps-monitor-your-logic-apps/monitor-view-details.png)
   
   > [!NOTE]
   > Tous les événements et les détails de l’exécution sont chiffrées dans hello service de Logic Apps. Elles sont déchiffrées uniquement lorsqu’un utilisateur demande tooview ces données. Vous pouvez également contrôler les événements d’accès aux toothese avec [du contrôle d’accès (RBAC)](../active-directory/role-based-access-control-what-is.md).

6. tooget plus d’informations sur un événement déclencheur spécifique, revenez en arrière toohello **vue d’ensemble** volet. Sous **déclencher l’historique**, sélectionnez d’événements déclencheurs hello. Vous pouvez maintenant examiner des détails tels que les entrées et sorties, par exemple :

   ![Détails de sortie d’événement déclencheur](media/logic-apps-monitor-your-logic-apps/trigger-details.png)

<a name="azure-diagnostics"></a>

## <a name="turn-on-diagnostics-logging-for-your-logic-app"></a>Activer la journalisation des diagnostics pour votre application logique

Pour un débogage enrichi avec des détails et événements d’exécution, vous pouvez configurer la journalisation des diagnostics avec [Azure Log Analytics](../log-analytics/log-analytics-overview.md). Analytique de journal est un service de [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) qui surveille votre cloud et locales toohelp environnements vous maintenir leur disponibilité et les performances. 

Avant de commencer, vous devez toohave un espace de travail OMS. En savoir plus [comment toocreate un espace de travail OMS](../log-analytics/log-analytics-get-started.md).

1. Bonjour [portail Azure](https://portal.azure.com), recherchez et sélectionnez votre application logique. 

2. Sur le menu de panneau application hello logique, sous **analyse**, choisissez **Diagnostics** > **les paramètres de Diagnostic**.

   ![Accédez tooMonitoring, Diagnostics, les paramètres de Diagnostic](media/logic-apps-monitor-your-logic-apps/logic-app-diagnostics.png)

3. Sous **Paramètres de diagnostic**, choisissez **Activé**.

   ![Activer les journaux de diagnostic](media/logic-apps-monitor-your-logic-apps/turn-on-diagnostics-logic-app.png)

4. Sélectionnez maintenant hello OMS espace de travail et les événements catégorie journalisation comme indiqué :

   1. Sélectionnez **envoyer tooLog Analytique**. 
   2. Sous **Log Analytics**, choisissez **Configurer**. 
   3. Sous **espaces de travail OMS**, sélectionnez toouse d’espace de travail OMS hello pour la journalisation.
   4. Sous **journal**, sélectionnez hello **WorkflowRuntime** catégorie.
   5. Choisir l’intervalle de métrique hello.
   6. Une fois ces opérations effectuées, sélectionnez **Enregistrer**.

   ![Sélectionner l’espace de travail OMS et les données à journaliser](media/logic-apps-monitor-your-logic-apps/send-diagnostics-data-log-analytics-workspace.png)

À présent, vous pouvez trouver des événements et d’autres données pour des événements déclencheurs, des événements d’exécution et des événements d’action.

<a name="find-events"></a>

## <a name="find-events-and-data-for-your-logic-app"></a>Rechercher des événements et des données pour votre application logique

toofind et affichage des événements dans votre application logique, telles que les événements déclencheurs, exécuter des événements et les événements d’action, procédez comme suit.

1. Bonjour [portail Azure](https://portal.azure.com), choisissez **plus Services**. Recherchez « log analytics », puis choisissez **Log Analytics** comme illustré ici :

   ![Choisir « Log Analytics »](media/logic-apps-monitor-your-logic-apps/browseloganalytics.png)

2. Sous **Log Analytics**, recherchez et sélectionnez votre espace de travail OMS. 

   ![Sélectionner votre espace de travail OMS](media/logic-apps-monitor-your-logic-apps/selectla.png)

3. Sous **Gestion**, choisissez **Portail OMS**.

   ![Choisir « Portail OMS »](media/logic-apps-monitor-your-logic-apps/omsportalpage.png)

4. Dans votre page d’accueil d’OMS, choisissez **Recherche dans les journaux**.

   ![Dans votre page d’accueil d’OMS, choisissez « Recherche dans les journaux »](media/logic-apps-monitor-your-logic-apps/logsearch.png)

   -ou-

   ![Menu hello OMS, choisissez « Recherche de journal »](media/logic-apps-monitor-your-logic-apps/logsearch-2.png)

5. Dans la zone de recherche de hello, spécifier un champ que vous souhaitez toofind, puis appuyez sur **entrée**. Lorsque vous commencez à taper, OMS affiche les correspondances possibles et les opérations que vous pouvez utiliser. 

   Par exemple, toofind hello 10 premiers événements qui se sont produites, entrez et sélectionner cette requête de recherche : **catégorie = WorkflowRuntime | top 10**

   ![Entrer une chaîne de recherche](media/logic-apps-monitor-your-logic-apps/oms-start-query.png)

   En savoir plus sur [comment toofind les données dans le journal Analytique](../log-analytics/log-analytics-log-searches.md).

6. Sur la page de résultats hello, dans la barre de gauche hello, choisissez hello laps de temps que vous souhaitez tooview.
Choisissez de votre requête en ajoutant un filtre, toorefine **+ ajouter**.

   ![Choisir un plage de temps pour les résultats de la requête](media/logic-apps-monitor-your-logic-apps/query-results.png)

7. Sous **ajouter des filtres**, entrez le nom du filtre hello afin que vous puissiez rechercher hello du filtre. Sélectionnez le filtre de hello, puis choisissez **+ ajouter**.

   Cet exemple utilise hello word « état » toofind Échec d’événements sous **AzureDiagnostics**.
   Hello ici de filtre pour **status_s** est déjà sélectionné.

   ![Sélectionner le filtre](media/logic-apps-monitor-your-logic-apps/log-search-add-filter.png)

8. Dans la barre de gauche hello, sélectionnez valeur hello du filtre que vous souhaitez toouse, choisissez **appliquer**.

   ![Sélectionner la valeur de filtre, choisir « Appliquer »](media/logic-apps-monitor-your-logic-apps/log-search-apply-filter.png)

9. Requête toohello retournent désormais que vous générez. Votre requête est mis à jour avec le filtre et la valeur sélectionnés. Vos résultats précédents sont à présent également filtrés.

   ![Retourne la requête tooyour résultats filtrés](media/logic-apps-monitor-your-logic-apps/log-search-query-filtered-results.png)

10. Choisissez de votre requête pour une utilisation ultérieure toosave **enregistrer**. En savoir plus [comment toosave votre requête](../logic-apps/logic-apps-track-b2b-messages-omsportal-query-filter-control-number.md#save-oms-query).

<a name="extend-diagnostic-data"></a>

## <a name="extend-how-and-where-you-use-diagnostic-data-with-other-services"></a>Étendre la manière dont vous utilisez les données de diagnostic et l’emplacement où vous les utilisez avec d’autres services

Avec Azure Log Analytics, vous pouvez étendre le mode d’utilisation des données de diagnostic de votre application logique avec d’autres services Azure, par exemple : 

* [Archivage des journaux de diagnostic Azure](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md)
* [Flux de données des journaux de Diagnostics Azure tooAzure concentrateurs d’événements](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md) 

Vous pouvez ensuite obtenir une surveillance en temps réel en utilisant les ressources de télémétrie et d’analyse d’autres services, tels que [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) et [Power BI](../log-analytics/log-analytics-powerbi.md). Par exemple :

* [Données de flux de données à partir de concentrateurs d’événements tooStream Analytique](../stream-analytics/stream-analytics-define-inputs.md)
* [Analyser les données de diffusion avec Stream Analytics et créer un tableau de bord analytique en temps réel dans Power BI](../stream-analytics/stream-analytics-power-bi-dashboard.md)

Selon les options de hello que vous voulez configurer, assurez-vous que vous première [créer un compte de stockage Azure](../storage/common/storage-create-storage-account.md) ou [créer un concentrateur d’événements Azure](../event-hubs/event-hubs-create.md). Puis sélectionnez les options de hello où vous souhaitez toosend les données de diagnostic :

![Envoyer des données tooAzure stockage compte ou événement un concentrateur](./media/logic-apps-monitor-your-logic-apps/storage-account-event-hubs.png)

> [!NOTE]
> Périodes de rétention s’appliquent uniquement lorsque vous choisissez un compte de stockage toouse.

<a name="add-azure-alerts"></a>

## <a name="set-up-alerts-for-your-logic-app"></a>Configurer des alertes pour votre application logique

toomonitor des métriques spécifiques ou dépassement des seuils pour votre application logique, configurez [alertes dans Azure](../monitoring-and-diagnostics/monitoring-overview-alerts.md). En savoir plus sur les [métriques dans Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md). 

tooset des alertes sans [Analytique de journal Azure](../log-analytics/log-analytics-overview.md), procédez comme suit. Pour des critères et actions d’alertes plus avancés, [configurez également Log Analytics](#azure-diagnostics).

1. Sur le menu de panneau application hello logique, sous **analyse**, choisissez **Diagnostics** > **règles d’alerte** > **ajouter une alerte**comme indiqué ici :

   ![Ajouter une alerte pour votre application logique](media/logic-apps-monitor-your-logic-apps/set-up-alerts.png)

2. Sur hello **ajouter une règle d’alerte** panneau, créer votre alerte comme indiqué :

   1. Sous **Ressource**, sélectionnez votre application logique si ce n’est déjà fait. 
   2. Donnez un nom et une description à votre alerte.
   3. Sélectionnez un **métrique** ou l’événement que vous souhaitez tootrack.
   4. Sélectionnez un **Condition**, spécifiez un **seuil** pour la métrique de hello et sélectionnez hello **période** pour l’analyse de cette mesure.
   5. Indiquez si toosend de messagerie pour l’alerte de hello. 
   6. Spécifiez des adresses de messagerie pour l’envoi d’une alerte de hello. 
   Vous pouvez également spécifier une URL webhook où vous souhaitez l’alerte de hello toosend.

   Par exemple, cette règle envoie une alerte quand cinq exécutions ou plus échouent par heure :

   ![Créer une règle d’alerte de métrique](media/logic-apps-monitor-your-logic-apps/create-alert-rule.png)

> [!TIP]
> toorun une application de la logique d’une alerte, vous pouvez inclure hello [déclencheur de demande](../connectors/connectors-native-reqres.md) dans votre flux de travail, ce qui vous permet d’effectuer des tâches telles que les exemples suivants :
> 
> * [Post tooSlack](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app)
> * [Envoyer un texte](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app)
> * [Ajouter une file d’attente de messages tooa](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app)

<a name="diagnostic-event-properties"></a>

## <a name="azure-diagnostics-event-settings-and-details"></a>Paramètres et détails d’événements Azure Diagnostics

Chaque événement de diagnostic a plus d’informations sur votre application logique et que l’événement, par exemple, l’état hello, heure de début, heure de fin et ainsi de suite. tooprogrammatically configurer la surveillance, le suivi et la journalisation, vous pouvez utiliser ces informations avec hello [API REST pour Azure Logic Apps](https://docs.microsoft.com/rest/api/logic) et hello [API REST pour les Diagnostics Azure](../monitoring-and-diagnostics/monitoring-supported-metrics.md#microsoftlogicworkflows).

Par exemple, hello `ActionCompleted` événement a hello `clientTrackingId` et `trackedProperties` les propriétés que vous pouvez utiliser pour le suivi et l’analyse :

``` json
{
    "time": "2016-07-09T17:09:54.4773148Z",
    "workflowId": "/SUBSCRIPTIONS/<subscription-ID>/RESOURCEGROUPS/MYRESOURCEGROUP/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/MYLOGICAPP",
    "resourceId": "/SUBSCRIPTIONS/<subscription-ID>/RESOURCEGROUPS/MYRESOURCEGROUP/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/MYLOGICAPP/RUNS/08587361146922712057/ACTIONS/HTTP",
    "category": "WorkflowRuntime",
    "level": "Information",
    "operationName": "Microsoft.Logic/workflows/workflowActionCompleted",
    "properties": {
        "$schema": "2016-06-01",
        "startTime": "2016-07-09T17:09:53.4336305Z",
        "endTime": "2016-07-09T17:09:53.5430281Z",
        "status": "Succeeded",
        "code": "OK",
        "resource": {
            "subscriptionId": "<subscription-ID>",
            "resourceGroupName": "MyResourceGroup",
            "workflowId": "cff00d5458f944d5a766f2f9ad142553",
            "workflowName": "MyLogicApp",
            "runId": "08587361146922712057",
            "location": "westus",
            "actionName": "Http"
        },
        "correlation": {
            "actionTrackingId": "e1931543-906d-4d1d-baed-dee72ddf1047",
            "clientTrackingId": "<my-custom-tracking-ID>"
        },
        "trackedProperties": {
            "myTrackedProperty": "<value>"
        }
    }
}
```

* `clientTrackingId`: Si ce n’est pas fourni, Azure génère cet ID et met en corrélation des événements dans une application logique s’exécuter automatiquement, y compris les workflows imbriqués qui sont appelées à partir de l’application logique de hello. Vous pouvez spécifier manuellement cet ID à partir d’un déclencheur en passant un `x-ms-client-tracking-id` en-tête avec votre valeur d’ID personnalisé dans la demande de déclencheur hello. Vous pouvez utiliser un déclencheur de demande, un déclencheur HTTP ou un déclencheur de webhook.

* `trackedProperties`: tootrack entrées ou des sorties dans les données de diagnostic, vous pouvez ajouter les propriétés suivies tooactions dans la définition de JSON de votre application logique. Les propriétés suivies peuvent suivre seulement une seule action entrées et sorties, mais vous pouvez utiliser hello `correlation` propriétés de toocorrelate d’événements entre les actions dans une série de tests.

  tootrack une ou plusieurs propriétés, ajouter hello `trackedProperties` section et hello propriétés toohello définition d’action. Par exemple, vous souhaitez que des données de tootrack comme un « ID de commande » de votre télémétrie :

  ``` json
  "myAction": {
    "type": "http",
    "inputs": {
        "uri": "http://uri",
        "headers": {
            "Content-Type": "application/json"
        },
        "body": "@triggerBody()"
    },
    "trackedProperties": {
        "myActionHTTPStatusCode": "@action()['outputs']['statusCode']",
        "myActionHTTPValue": "@action()['outputs']['body']['<content>']",
        "transactionId": "@action()['inputs']['body']['<content>']"
    }
  }
  ```

## <a name="next-steps"></a>Étapes suivantes

* [Création de modèles pour le déploiement d’applications logiques et la gestion des versions](../logic-apps/logic-apps-create-deploy-template.md)
* [Scénarios B2B et communication avec Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md)
* [Surveiller les messages B2B](../logic-apps/logic-apps-monitor-b2b-message.md)