---
title: aaaCreate web API & API REST en tant que connecteurs - Azure Logic Apps | Documents Microsoft
description: "Créer toocall API & API REST de web API, des services ou des systèmes de flux de travail pour l’intégration des systèmes avec Azure Logic Apps"
keywords: "API web, API REST, connecteurs, flux de travail, intégration système"
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: bd229179-7199-4aab-bae0-1baf072c7659
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 5/26/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 2792204d1d298a6f810e75211c1789ee204c2fdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-custom-apis-as-connectors-for-logic-apps"></a>Créer des API personnalisées en tant que connecteurs pour les applications logiques

Bien que Azure Logic Apps offre [liens intégrés 100 +](../connectors/apis-list.md) que vous pouvez utiliser dans les workflows d’application logique, vous pouvez toocall API, systèmes et services qui ne sont pas disponibles en tant que les connecteurs. Vous pouvez créer vos propres API personnalisées qui fournissent les actions et les déclencheurs toouse dans les applications de la logique. Voici les autres raisons pour lesquelles vous pourriez toocreate vos propres API utilisent trop en tant que liens dans les applications de logique :

* Étendre l’intégration de votre système actuel et les flux de travail d’intégration de données.
* Aider les clients à utiliser votre service toomanage personnels ou professionnels des tâches.
* Développez hello portée, détectabilité et l’utilisation de votre service.

En principe, les connecteurs sont des API web qui utilisent REST pour les interfaces enfichables, le [format de métadonnées Swagger](http://swagger.io/specification/) pour la documentation et JSON en tant que format d’échange de données. Étant donné que les connecteurs sont des API REST qui communiquent via des points de terminaison HTTP, vous pouvez utiliser n’importe quel langage, comme .NET, Java ou Node.js, pour la création de connecteurs. Vous pouvez également héberger votre API sur [Azure App Service](../app-service/app-service-value-prop-what-is.md), un platform-as-a-service (PaaS) qui fournit une des manières de meilleures, plus simple et plus évolutive hello pour l’hébergement de l’API de l’offre. 

Pour toowork API personnalisée avec les applications de la logique, peut fournir votre API [ *actions* ](./logic-apps-what-are-logic-apps.md#logic-app-concepts) qui effectuent des tâches spécifiques dans les workflows d’application logique. Votre API peut également faire office de [*déclencheur*](./logic-apps-what-are-logic-apps.md#logic-app-concepts) qui démarre le flux de travail d’une application logique lorsque de nouvelles données ou un événement répondent à une condition donnée. Cette rubrique décrit les modèles courants que vous pouvez suivre pour la création d’actions et des déclencheurs dans votre API, selon le comportement de hello que votre tooprovide API que vous souhaitez.

> [!TIP] 
> Vous pouvez déployer votre API que [les applications web](../app-service-web/app-service-web-overview.md), envisagez de déployer votre API comme [applications API](../app-service-api/app-service-api-apps-why-best-platform.md), qui peut simplifier votre travail lorsque vous générez, hébergez et consommer des API dans le cloud de hello et localement. Vous n’avez pas de code toochange dans votre API--simplement déployer votre application API de tooan code. Découvrez comment trop [créer des applications API créées avec ASP.NET](../app-service-api/app-service-api-dotnet-get-started.md), [Java](../app-service-api/app-service-api-java-api-app.md), ou [Node.js](../app-service-api/app-service-api-nodejs-api-app.md). 
>
> Pour obtenir des exemples d’application API générées pour logic apps, visitez hello [référentiel GitHub d’applications Azure logique](http://github.com/logicappsio) ou [blog](http://aka.ms/logicappsblog).

## <a name="helpful-tools"></a>Outils utiles

Une API personnalisée fonctionne mieux avec les applications logique lorsque hello API a également un [Swagger document](http://swagger.io/specification/) qui décrit les opérations et les paramètres de l’API de hello.
Comme de nombreuses bibliothèques, [Swashbuckle](https://github.com/domaindrivendev/Swashbuckle), peut générer automatiquement le fichier Swagger hello pour vous. le fichier de Swagger tooannotate hello pour les noms d’affichage, les types de propriété et ainsi de suite, vous pouvez également utiliser [TRex](https://github.com/nihaue/TRex) afin que votre fichier Swagger fonctionne bien avec les applications de la logique.

<a name="actions"></a>

## <a name="action-patterns"></a>Modèles d’action

Pour les tâches de tooperform logique applications, votre API personnalisée doit fournir [ *actions*](./logic-apps-what-are-logic-apps.md#logic-app-concepts). Chaque opération dans votre API mappe tooan action. Une action de base peut être un contrôleur qui accepte les requêtes HTTP et renvoie des réponses HTTP. Par exemple, une application logique envoie un HTTP demande tooyour l’application web ou une application API. Votre application puis renvoie une réponse HTTP, ainsi que le contenu qui hello logique application peut traiter.

Pour une action standard, vous pouvez écrire une méthode de requête HTTP dans votre API et décrire cette méthode dans un fichier Swagger. Vous pouvez ensuite appeler votre API directement avec une [action HTTP](../connectors/connectors-native-http.md) ou une action [HTTP + Swagger](../connectors/connectors-native-http-swagger.md). Par défaut, les réponses doivent être retournées dans hello [limite de délai d’attente de demandes](./logic-apps-limits-and-config.md). 

![Modèle d’action standard](./media/logic-apps-create-api-app/standard-action.png)

<a name="pattern-overview"></a>toomake une application logique patienter pendant que votre API des tâches de longue durée plus longue, votre API peut suivre hello [d’interrogation asynchrone modèle](#async-pattern) ou hello [webhook asynchrone modèle](#webhook-actions) décrites dans cette rubrique. Supposons une analogie qui vous permet de visualiser des comportements différents des ces modèles, processus hello pour commander un gâteau personnalisé à partir d’un bakery. modèle de l’interrogation de Hello reflète le comportement hello d’appel bakery de hello chaque toocheck 20 minutes si au chocolat hello est prêt. comportement hello Hello webhook modèle miroirs où bakery de hello vous demande votre numéro de téléphone afin de vous appeler quand au chocolat hello est prêt.

Pour obtenir des exemples, visitez hello [référentiel GitHub d’applications logique](https://github.com/logicappsio). Découvrez également les [mesures d’utilisation des actions](logic-apps-pricing.md).

<a name="async-pattern"></a>

### <a name="perform-long-running-tasks-with-hello-polling-action-pattern"></a>Effectuer des tâches longues avec hello d’interrogation du modèle d’action

toohave votre API effectuer des tâches qui pourrait s’exécuter plus longtemps que hello [limite de délai d’attente de demandes](./logic-apps-limits-and-config.md), vous pouvez utiliser le modèle d’interrogation asynchrone hello. Ce modèle est votre API de travail dans un thread distinct, mais conserve un moteur de Logic Apps toohello connexion active. De cette façon, application logique de hello n’expire pas ou continuer à l’étape suivante de hello dans le flux de travail hello avant la fin de travail par votre API.

Voici le modèle général de hello :

1. Assurez-vous que ce moteur hello sait que votre API accepté la demande de hello et commencer à travailler.
2. Lorsque le moteur de hello effectue des demandes ultérieures portant sur l’état du travail, informer le moteur de hello lorsque votre API termine la tâche hello.
3. Retour du moteur de données pertinentes toohello afin que le flux de travail application hello logique peut continuer.

<a name="bakery-polling-action"></a>Maintenant appliquer des critères de l’interrogation de bakery analogie toohello hello précédentes et Imaginez que vous appelez un bakery et ordre gâteau personnalisé pour la remise. processus Hello permettant au chocolat hello prend du temps, et vous ne souhaitez pas toowait sur le téléphone de hello tandis que les bakery hello fonctionne sur le gâteau de hello. bakery de Hello confirme votre commande et a d’appeler toutes les 20 minutes pour l’état du gâteau hello. Après que 20 minutes se sont écoulées, vous appelez bakery de hello, mais ils indiquent que votre gâteau n’est pas terminé et que vous devez appeler dans un autre de 20 minutes. Ce processus back-et-les deux sens se poursuit jusqu'à ce que vous appelez et bakery de hello indique que votre commande est prête et remet le gâteau. 

Revenons à ce modèle d’interrogation pour votre API. bakery de Hello représente votre API personnalisée, tandis que vous, hello gâteau client, représentez le moteur de Logic Apps hello. Lorsque le moteur de hello appelle votre API avec une demande, votre API confirmant la demande de hello et répond avec un intervalle de temps hello lorsque le moteur de hello peut vérifier l’état du travail. moteur de Hello continue de la vérification d’état du travail jusqu'à ce que votre API répond que ce travail hello est effectué et retourne données tooyour application logique, qui ensuite continue de flux de travail. 

![Modèle d’action d’interrogation](./media/logic-apps-create-api-app/custom-api-async-action-pattern.png)

Hello les étapes spécifiques pour votre API toofollow, décrit à partir de la perspective de l’API de hello sont :

1. Lorsque votre API Obtient un travail de toostart de demande HTTP, retourner immédiatement HTTP `202 ACCEPTED` réponse avec hello `location` en-tête décrite plus loin dans cette étape. Cette réponse permet hello Logic Apps, moteur de savoir que votre API a été hello demande, la charge utile de demande acceptée hello (données d’entrée) et est en train de traiter. 
   
   Hello `202 ACCEPTED` réponse doit inclure ces en-têtes :
   
   * *Requis*: A `location` en-tête qui spécifie l’URL de tooa hello chemin d’accès absolu où moteur de Logic Apps hello peut vérifier état du travail de votre API

   * *Facultatif*: A `retry-after` en-tête qui spécifie le nombre hello de secondes pendant lesquelles hello moteur doit attendre avant de vérifier hello `location` URL de l’état du travail. 

     Par défaut, le moteur de hello vérifie toutes les 20 secondes. toospecify un intervalle différent, inclure hello `retry-after` en-tête et hello le nombre de secondes jusqu'à ce que l’interrogation suivante de hello.

2. Une fois hello spécifié délai s’écoule, hello Logic Apps moteur hello de sondages `location` état du travail toocheck URL. Votre API doit effectuer ces vérifications et renvoyer ces réponses :
   
   * Si le travail de hello est effectué, retourner HTTP `200 OK` réponse, ainsi que de la charge utile de réponse hello (entrée pour l’étape suivante de hello).

   * Si le traitement de la tâche de hello est toujours, retourner un autre HTTP `202 ACCEPTED` hello de réponse, mais avec des en-têtes mêmes en tant que réponse de hello d’origine.

Lorsque votre API suit ce modèle, vous n’avez rien toodo dans hello logique application workflow définition toocontinue la vérification de statut. Lorsque le moteur de hello obtient HTTP `202 ACCEPTED` réponse et un `location` en-tête, hello moteur égards hello asynchrone modèle et les vérifications hello `location` en-tête jusqu'à ce que votre API renvoie une réponse non-202.

> [!TIP]
> Pour un exemple de modèle asynchrone, consultez cet [exemple de réponse de contrôleur asynchrone dans GitHub](https://github.com/logicappsio/LogicAppsAsyncResponseSample).

<a name="webhook-actions"></a>

### <a name="perform-long-running-tasks-with-hello-webhook-action-pattern"></a>Effectuer des tâches de longue avec le modèle d’action hello webhook

En guise d’alternative, vous pouvez utiliser le modèle de webhook hello pour le traitement asynchrone et les tâches de longue. Ce modèle est l’application logique de hello interrompre et attendre un « rappel » à partir de votre toofinish API avant de poursuivre le flux de travail de traitement. Ce rappel est une requête HTTP POST qui envoie une URL tooa de message quand un événement se produit. 

<a name="bakery-webhook-action"></a>Maintenant appliquer des critères de hello précédente bakery analogie toohello webhook et Imaginez que vous appelez un bakery et ordre gâteau personnalisé pour la remise. processus Hello permettant au chocolat hello prend du temps, et vous ne souhaitez pas toowait sur le téléphone de hello tandis que les bakery hello fonctionne sur le gâteau de hello. bakery de Hello confirme votre commande, mais cette fois, vous leur donnez votre numéro de téléphone afin de vous appeler quand au chocolat hello est terminé. Cette fois-ci, bakery de hello vous indique lorsque votre commande est prêt et remet le gâteau.

Quand nous mappez ce modèle webhook précédent, bakery de hello représente votre API personnalisée, tout en vous, client de gâteau hello, représentent hello Logic Apps moteur. moteur de Hello appelle votre API avec une demande et inclut une URL « rappel ».
Lors de la tâche de hello est terminé, votre API utilise hello URL toonotify hello moteur et retourner des données tooyour logique application, puis continue le flux de travail. 

Pour ce modèle, définissez deux points de terminaison sur votre contrôleur : `subscribe` et `unsubscribe`

*  `subscribe`point de terminaison : lorsque l’exécution atteint l’action de votre API dans le flux de travail hello, hello Logic Apps moteur hello d’appels `subscribe` point de terminaison. Cette étape affiche hello logique application toocreate une URL de rappel que votre API stocke et attendez rappel hello à partir de votre API lorsque le travail est terminé. Votre API puis rappelle avec une URL de toohello HTTP POST et transmet les en-têtes et le contenu retourné en tant qu’application logique de toohello d’entrée.

* `unsubscribe`point de terminaison : si l’application de la logique de hello exécuter est annulée, hello Logic Apps moteur hello d’appels `unsubscribe` point de terminaison. Votre API ensuite annuler l’inscription d’URL de rappel hello et arrêtez tous les processus en tant que nécessaire.

![Modèle d’action Webhook](./media/logic-apps-create-api-app/custom-api-webhook-action-pattern.png)

> [!NOTE]
> Actuellement, hello Concepteur de logique d’application ne prend en charge des points de terminaison webhook découverte via Swagger. Donc pour ce modèle, vous devez tooadd un [ **Webhook** action](../connectors/connectors-native-webhook.md) et spécifiez l’URL de hello, en-têtes, corps de votre demande. Voir également [Actions et déclencheurs de flux de travail](logic-apps-workflow-actions-triggers.md#api-connection-webhook-action). toopass dans l’URL de rappel hello, vous pouvez utiliser hello `@listCallbackUrl()` fonction de workflow dans un des champs de précédents hello selon les besoins.

> [!TIP]
> Pour un exemple de modèle Webhook, consultez cet [exemple de déclencheur Webhook dans GitHub](https://github.com/logicappsio/LogicAppTriggersExample/blob/master/LogicAppTriggers/Controllers/WebhookTriggerController.cs).

<a name="triggers"></a>

## <a name="trigger-patterns"></a>Modèles de déclencheur

Votre API personnalisée peut faire office de [*déclencheur*](./logic-apps-what-are-logic-apps.md#logic-app-concepts) qui démarre une application logique lorsque de nouvelles données ou un événement répondent à une condition donnée. Ce déclencheur peut soit vérifier régulièrement, soit attendre et écouter, la présence de nouvelles données ou d’événements au niveau du point de terminaison de votre service. Si de nouvelles données ou un événement respecte hello la condition spécifiée, déclencheur de hello est activé et qu’il démarre l’application hello logique, qui est à l’écoute toothat déclencheur. logique toostart les applications de cette manière, votre API peut suivre hello [ *d’interrogation déclencheur* ](#polling-triggers) ou hello [ *webhook déclencheur* ](#webhook-triggers) modèle. Ces modèles sont des équivalents tootheir similaire pour [d’interrogation actions](#async-pattern) et [les actions webhook](#webhook-actions). Découvrez également les [mesures d’utilisation des déclencheurs](logic-apps-pricing.md).

<a name="polling-triggers"></a>

### <a name="check-for-new-data-or-events-regularly-with-hello-polling-trigger-pattern"></a>Rechercher les nouvelles données ou des événements régulièrement par hello d’interrogation du modèle de déclencheur

A *d’interrogation déclencheur* joue hello [d’interrogation action](#async-pattern) décrit précédemment dans cette rubrique. moteur de Logic Apps Hello appelle régulièrement et vérifie le point de terminaison de déclencheur hello pour les nouvelles données ou des événements. Si le moteur de hello détecte les nouvelles données ou un événement qui répond à la condition spécifiée, hello déclencheur. Moteur de hello crée ensuite une instance d’application logique qui traite les données hello en tant qu’entrée. 

![Modèle de déclencheur d’interrogation](./media/logic-apps-create-api-app/custom-api-polling-trigger-pattern.png)

> [!NOTE]
> Chaque requête d’interrogation compte comme une exécution de l’action, même lorsqu’aucune instance d’application logique n’est créée. le traitement de tooprevent hello des mêmes données plusieurs fois, le déclencheur doit nettoyer les données qui a été déjà lu et transmises toohello logique application.

Voici les étapes spécifiques pour un déclencheur d’interrogation, décrit à partir de la perspective de l’API de hello :

| Il existe de nouvelles données ou un nouvel événement ?  | Réponse de l’API | 
| ------------------------- | ------------ |
| Trouvé | Retourner HTTP `200 OK` état de la charge utile de réponse hello (entrée pour l’étape suivante). <br/>Cette réponse crée une instance d’application logique et démarre le flux de travail hello. |
| Introuvable | Renvoyez un état HTTP `202 ACCEPTED` avec un en-tête `location` et un en-tête `retry-after`. <br/>Pour les déclencheurs, hello `location` en-tête doit également contenir un `triggerState` paramètre de requête, qui est généralement un « timestamp ». Votre API permet cette hello de tootrack identificateur dernière hello logique d’application a été déclenchée. |

Par exemple, tooperiodically vérifier votre service pour les nouveaux fichiers, vous pouvez créer un déclencheur d’interrogation qui possède ces comportements :

| La requête inclut `triggerState` ? | Réponse de l’API |
| -------------------------------- | -------------|
| Non | Retourner HTTP `202 ACCEPTED` état plus une `location` en-tête avec `triggerState` définir toohello heure actuelle et hello `retry-after` too15 d’intervalle en secondes. |
| Oui | Vérifiez que votre service de fichiers ajoutés après hello `DateTime` pour `triggerState`. |

| Nombre de fichiers trouvés | Réponse de l’API |
| --------------------- | -------------|
| Fichier unique | Retourner HTTP `200 OK` charge utile du contenu état et hello, mise à jour `triggerState` toohello `DateTime` de hello a retourné un fichier et à `retry-after` too15 d’intervalle en secondes. |
| Fichiers multiples | Retourner un seul fichier à la fois HTTP `200 OK` état, de mise à jour `triggerState`et ensemble hello `retry-after` too0 d’intervalle en secondes. </br>Ces étapes informer le moteur de hello que davantage de données est disponible, et ce moteur hello doit demander immédiatement les données de salutation URL hello Bonjour `location` en-tête. |
| Aucun fichier | Retourner HTTP `202 ACCEPTED` état, ne modifiez pas `triggerState`et ensemble hello `retry-after` too15 d’intervalle en secondes. |

> [!TIP]
> Pour obtenir un exemple de modèle de déclencheur d’interrogation, consultez cet [exemple de contrôleur de déclencheur d’interrogation dans GitHub](https://github.com/logicappsio/LogicAppTriggersExample/blob/master/LogicAppTriggers/Controllers/PollTriggerController.cs).

<a name="webhook-triggers"></a>

### <a name="wait-and-listen-for-new-data-or-events-with-hello-webhook-trigger-pattern"></a>Patientez et écouter les nouvelles données ou des événements avec le modèle de déclencheur hello webhook

Un déclencheur Webhook est un *déclencheur d’émission* qui attend et écoute les nouvelles données ou les événements au point de terminaison de votre service. Si de nouvelles données ou un événement respecte hello spécifié la condition de déclencheur hello et crée une instance d’application logique, lequel traite ensuite les données hello en tant qu’entrée.
Les déclencheurs de Webhook agissent comme hello [les actions webhook](#webhook-actions) précédemment décrites dans cette rubrique et sont configurés avec `subscribe` et `unsubscribe` points de terminaison. 

* `subscribe`point de terminaison : lorsque vous ajoutez et enregistrez un déclencheur de webhook dans votre application logique, hello Logic Apps moteur hello d’appels `subscribe` point de terminaison. Cette étape affiche hello logique application toocreate une URL de rappel qui stocke de votre API. Lorsque de nouvelles données ou un événement qui répond à hello condition spécifiée, votre API rappelle avec une URL de toohello HTTP POST. en-têtes et la charge de contenu hello passent en tant qu’application logique de toohello d’entrée.

* `unsubscribe`point de terminaison : si le déclencheur de webhook hello ou l’application de l’intégralité de la logique est supprimée, hello Logic Apps moteur hello d’appels `unsubscribe` point de terminaison. Votre API ensuite annuler l’inscription d’URL de rappel hello et arrêtez tous les processus en tant que nécessaire.

![Modèle de déclencheur Webhook](./media/logic-apps-create-api-app/custom-api-webhook-trigger-pattern.png)

> [!NOTE]
> Actuellement, hello Concepteur de logique d’application ne prend en charge des points de terminaison webhook découverte via Swagger. Donc pour ce modèle, vous devez tooadd un [ **Webhook** déclencheur](../connectors/connectors-native-webhook.md) et spécifiez l’URL de hello, en-têtes, corps de votre demande. Voir également [Déclencheur HTTPWebhook](logic-apps-workflow-actions-triggers.md#httpwebhook-trigger). toopass dans l’URL de rappel hello, vous pouvez utiliser hello `@listCallbackUrl()` fonction de workflow dans un des champs de précédents hello selon les besoins.
>
> le traitement de tooprevent hello des mêmes données plusieurs fois, le déclencheur doit nettoyer les données qui a été déjà lu et transmises toohello logique application.

> [!TIP]
> Pour un exemple de modèle Webhook, consultez cet [exemple de contrôleur de déclencheur Webhook dans GitHub](https://github.com/logicappsio/LogicAppTriggersExample/blob/master/LogicAppTriggers/Controllers/WebhookTriggerController.cs).

## <a name="deploy-call-and-secure-custom-apis"></a>Déployer, appeler et sécuriser les API personnalisées

Une fois les API personnalisées créées, configurez-les pour le déploiement, de façon à pouvoir les appeler en toute sécurité. Découvrez comment trop[déployer, appeler et sécuriser les API personnalisées pour les applications de la logique](./logic-apps-custom-hosted-api.md).

## <a name="publish-custom-apis-tooazure"></a>Publier les tooAzure API personnalisée

toomake votre API personnalisée disponibles pour une utilisation publique dans Azure, envoyez votre toohello les candidatures [programme Microsoft Azure Certified](https://azure.microsoft.com/marketplace/programs/certified/logic-apps/).

## <a name="get-help"></a>Obtenir de l’aide

Pour obtenir de l’aide concernant les API personnalisées, contactez [customapishelp@microsoft.com](mailto:customapishelp@microsoft.com).

tooask questions, répondez aux questions et voir les autres utilisateurs Azure Logic Apps font, visitez hello [forum de Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).

toohelp améliorer Logic Apps et connecteurs, voter pour ou envoyer vos idées à hello [site de commentaires utilisateur Logic Apps](http://aka.ms/logicapps-wish). 

## <a name="next-steps"></a>Étapes suivantes

* [Mesure de l’utilisation des actions et des déclencheurs](logic-apps-pricing.md)
* [Gérer les types de contenu](./logic-apps-content-type.md)
* [Gérer les erreurs et exceptions](./logic-apps-exception-handling.md)
* [Sécuriser l’accès aux applications de la logique de tooyour](./logic-apps-securing-a-logic-app.md)
* [Appeler, déclencher ou imbriquer des applications logiques via des points de terminaison HTTP](./logic-apps-http-endpoint.md)