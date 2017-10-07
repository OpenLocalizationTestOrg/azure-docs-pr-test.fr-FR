---
title: "aaaChoose entre les flux, Logic Apps, fonctions et les tâches Web | Documents Microsoft"
description: "Compare et contraste hello pour les services d’intégration de cloud de Microsoft et décidez quels services, vous devez utiliser."
services: functions,app-service\logic
documentationcenter: na
author: cephalin
manager: wpickett
tags: 
keywords: "microsoft flow, flow, logic apps, azure functions, functions, azure webjobs, webjobs, traitement d’événements, calcul dynamique, architecture sans serveur"
ms.assetid: e9ccf7ad-efc4-41af-b9d3-584957b1515d
ms.service: functions
ms.devlang: multiple
ms.topic: overview
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 08/03/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 6becc1e389698e517924b18295dac4375542d524
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="choose-between-flow-logic-apps-functions-and-webjobs"></a>Choisir entre Flow, Logic Apps, Functions et WebJobs
Cet article compare et contraste hello suivant des services de cloud de Microsoft hello, qui peut résoudre des problèmes d’intégration et d’automatisation des processus d’entreprise :

* [Microsoft Flow](https://flow.microsoft.com/)
* [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/)
* [Azure Functions](https://azure.microsoft.com/services/functions/)
* [Azure App Service WebJobs](../app-service-web/web-sites-create-web-jobs.md)

Tous ces services sont utiles pour « coller » ensemble des systèmes disparates. Ils peuvent tous définir des entrées, des actions, des conditions et des sorties. Vous pouvez exécuter chacun d’eux selon une planification ou à l’aide d’un déclencheur. Toutefois, chaque service ajoute un ensemble de valeur unique, et en les comparant ne sont pas une question de « service qui est hello meilleures ? » mais plutôt lequel convient le mieux à une situation donnée. Souvent, une combinaison de ces services est la meilleure hello toorapidly générer une solution évolutive intégration complète proposée.

<a name="flow"></a>

## <a name="flow-vs-logic-apps"></a>Flow vs Logic Apps
Nous pouvons voir Microsoft Flow et Azure Logic Apps ensemble car ils sont tous deux *configuration en premier* services d’intégration, ce qui rend facile toobuild processus et des flux de travail et de s’intégrer avec plusieurs SaaS et d’entreprise applications. 

* Flow est basé sur Logic Apps.
* Ils ont hello même concepteur de flux de travail
* [Connecteurs](../connectors/apis-list.md) que le travail dans un fonctionne également dans hello autres

Flux Responsabilise les intégrations simple à office worker tooperform (par exemple, get SMS pour les e-mails importants) sans passer par les développeurs ou informatique. Sur hello autre part, Logic Apps peut activer des intégrations avancées ou critiques (par exemple, le processus B2B) où les pratiques DevOps et la sécurité au niveau de l’entreprise sont requises. Il est courant pour un toogrow de flux de travail d’entreprise dans le temps supplémentaire de complexité. En conséquence, vous pouvez commencer par un flux dans un premier temps, puis convertir en application de tooa logique en fonction des besoins.

Hello tableau suivant permet de déterminer si le flux ou Logic Apps est idéal pour une intégration donnée.

|  | Flux | Logic Apps |
| --- | --- | --- |
| Public ciblé |Employés de bureau, utilisateurs professionnels |Professionnels de l’informatique, développeurs |
| Scénarios |Libre-service |Intégration stratégique |
| Outil de conception |Dans le navigateur et application mobile, interface utilisateur uniquement |Dans le navigateur et [Visual Studio](../logic-apps/logic-apps-deploy-from-vs.md), [mode Code](../logic-apps/logic-apps-author-definitions.md) disponible |
| DevOps |Ad hoc, développement en production |Contrôle de code source, tests, support, et automatisation et gestion simplifiée dans [Azure Resource Management](../logic-apps/logic-apps-arm-provision.md) |
| Expérience administrateur |[https://flow.microsoft.com](https://flow.microsoft.com) |[https://portal.azure.com](https://portal.azure.com) |
| Sécurité |Pratiques standard : [souveraineté des données](https://wikipedia.org/wiki/Technological_Sovereignty), [chiffrement au repos](https://wikipedia.org/wiki/Data_at_rest#Encryption) pour les données sensibles, etc. |Garantie de sécurité d’Azure : [Azure Security](https://www.microsoft.com/trustcenter/Security/AzureSecurity), [Security Center](https://azure.microsoft.com/services/security-center/), [journaux d’audit](https://azure.microsoft.com/blog/azure-audit-logs-ux-refresh/), etc. |

<a name="function"></a>

## <a name="functions-vs-webjobs"></a>Functions vs WebJobs
Azure Functions et Azure App Service WebJobs peuvent être traités ensemble, car il s’agit dans les deux cas de services d’intégration *orientés code* et conçus pour les développeurs. Ils permettent de toorun un script ou une partie du code dans les événements toovarious réponse, tel que [nouveaux objets BLOB de stockage](functions-bindings-storage.md) ou [une demande de WebHook](functions-bindings-http-webhook.md). Voici leurs points communs : 

* Ils sont tous deux basés sur [Azure App Service](../app-service/app-service-value-prop-what-is.md) et proposent des fonctionnalités telles que [le contrôle de code source](../app-service-web/app-service-continuous-deployment.md), [l’authentification](../app-service/app-service-authentication-overview.md) et [la surveillance](../app-service-web/web-sites-monitor.md).
* Il s’agit dans les deux cas de services destinés aux développeurs.
* Ils prennent en charge les langages standard de script et de programmation.
* Ils prennent en charge NuGet et NPM.

Fonctions est évolution naturelle de hello des tâches Web nécessaire hello meilleures choses WebJobs et améliore les. Hello améliorations sont notamment : 

* Développement simplifié, tester et exécuter du code, directement dans le navigateur de hello.
* Intégration native avec d’autres services Azure et des services tiers tels que [GitHub WebHooks](https://developer.github.com/webhooks/creating/).
* Paiement à l’utilisation, aucun toopay nécessaire pour un [plan App Service](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).
* [Mise à l’échelle dynamique](functions-scale.md)et automatique.
* Pour les clients existants du Service d’application, en cours d’exécution sur le plan App Service possible (tootake parti des ressources de sous-utilisée).
* Intégration avec Logic Apps.

Hello tableau suivant résume les différences de hello entre les fonctions et les tâches Web :

|  | Fonctions | WebJobs |
| --- | --- | --- |
| Mise à l'échelle |Mise à l’échelle sans configuration |Mise à l’échelle avec un plan App Service |
| Tarifs |Paiement à l’utilisation ou dans le cadre d’un plan App Service |Dans le cadre d’un plan App Service |
| Type d’exécution |Déclenchée, planifiée (par un déclencheur de minuteur) |Déclenchée, continue, planifiée |
| Événements déclencheurs |[Minuteur](functions-bindings-timer.md), [Azure Cosmos DB](functions-bindings-documentdb.md), [Azure Event Hubs](functions-bindings-event-hubs.md), [HTTP/WebHook (GitHub, Slack)](functions-bindings-http-webhook.md), [Azure App Service Mobile Apps](functions-bindings-mobile-apps.md), [Azure Notification Hubs](functions-bindings-notification-hubs.md), [Azure Service Bus](functions-bindings-service-bus.md), [Stockage Azure](functions-bindings-storage.md) |[Stockage Azure](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md), [Azure Service Bus](../app-service-web/websites-dotnet-webjobs-sdk-service-bus.md) |
| Développement dans le navigateur |pris en charge | non pris en charge |
| Scripts Windows |Expérimental |pris en charge |
| PowerShell |Expérimental |pris en charge |
| C# |pris en charge |pris en charge |
| F# |pris en charge |non pris en charge |
| Bash |Expérimental |pris en charge |
| PHP |Expérimental |pris en charge |
| Python |Expérimental |pris en charge |
| JavaScript |pris en charge |pris en charge |

Indique si les fonctions toouse ou des tâches Web dépend de ce que vous faites déjà avec le Service d’applications. Si vous disposez d’une application de Service d’applications pour lequel vous souhaitez toorun les extraits de code et que vous souhaitez toomanage ensemble dans hello même DevOps environnement, vous devez utiliser des tâches Web. Si vous souhaitez toorun les extraits de code pour d’autres services Azure ou même 3 rd-party applications, ou si vous souhaitez gérer trop vos extraits de code integration séparément à partir de vos applications de Service d’applications, ou si vous souhaitez toocall vos extraits de code à partir d’une application logique, vous devez tirer profit de tous les améliorations de Hello dans les fonctions.  

<a name="together"></a>

## <a name="flow-logic-apps-and-functions-together"></a>Flow, Logic Apps et Functions ensemble
Comme mentionné précédemment, le service qui est la mieux adaptée tooyou dépend de votre situation. 

* Pour une optimisation simple de votre activité, utilisez Flow.
* Si votre scénario d’intégration est trop avancé pour Flow ou si vous avez besoin de fonctionnalités de développement et d’une conformité en matière de sécurité, utilisez Logic Apps.
* Si une étape de votre scénario d’intégration nécessite une transformation hautement personnalisée ou du code spécialisé, écrivez une application de fonction, puis déclenchez une fonction en tant qu’action dans votre application logique.

Vous pouvez appeler une application logique dans un flux. Vous pouvez également appeler une fonction dans une application logique et une application logique dans une fonction. l’intégration entre les flux, les applications de la logique et les fonctions Hello continuer tooimprove supplémentaires. Vous pouvez générer un élément dans un seul service et l’utiliser dans hello autres services. Par conséquent, tout investissement dans ces trois technologies est pertinent.

## <a name="next-steps"></a>Étapes suivantes
Prise en main chacun des services de hello en créant votre premier flux, application logique, application de la fonction ou la tâche Web. Cliquez sur un des hello suivant liens :

* [Prise en main de Microsoft Flow](https://flow.microsoft.com/en-us/documentation/getting-started/)
* [Créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md)
* [Créer votre première fonction Azure](functions-create-first-azure-function.md)
* [Déployer des tâches web à l’aide de Visual Studio](../app-service-web/websites-dotnet-deploy-webjobs.md)

Ou obtenez plus d’informations sur ces services d’intégration avec hello suivant liens :

* [Leveraging Azure Functions &amp; Azure App Service for integration scenarios (Tirer parti d’Azure Functions et Azure App Service pour les scénarios d’intégration), par Christopher Anderson](http://www.biztalk360.com/integrate-2016-resources/leveraging-azure-functions-azure-app-service-integration-scenarios/)
* [Integrations Made Simple (Les intégrations simplifiées), par Charles Lamanna](http://www.biztalk360.com/integrate-2016-resources/integrations-made-simple/)
* [Diffusion web sur Logic Apps](http://aka.ms/logicappslive)
* [Forum Aux Questions sur Microsoft Flow](https://flow.microsoft.com/documentation/frequently-asked-questions/)
* [Ressources de documentation relatives à Azure WebJobs](../app-service-web/websites-webjobs-resources.md)

