---
title: aaaMonitor Node.js services avec Azure Application Insights | Documents Microsoft
description: "Analysez les performances et diagnostiquez les problèmes dans les services Node.js avec Application Insights."
services: application-insights
documentationcenter: nodejs
author: joshgav
manager: carmonm
ms.assetid: 2ec7f809-5e1a-41cf-9fcd-d0ed4bebd08c
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/01/2017
ms.author: bwren
ms.openlocfilehash: 0a7e66990cd4d3a2fcaf3fa779adb336c861f8ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-your-nodejs-services-and-apps-with-application-insights"></a>Surveiller vos services et applications Node.js avec Application Insights

[Azure Application Insights](app-insights-overview.md) surveille vos composants et services principaux après avoir déployé les toohelp vous [détecter et diagnostiquer rapidement les problèmes de performances et autres](app-insights-detect-triage-diagnose.md). Utilisez ce service pour les services Node.js, où qu’ils soient hébergés : dans votre centre de données, des machines virtuelles Azure et des applications Web, voire d’autres clouds publics.

tooreceive, stocker et Explorer vos données d’analyse, suivez hello suivant les instructions tooinclude un agent dans votre code et définir une ressource Application Insights correspondante dans Azure. agent de Hello envoie des ressources toothat de données pour une analyse plus approfondie et l’exploration.

l’agent de Node.js Hello peut automatiquement détecter entrants et sortants HTTP demandes, plusieurs métriques du système et les exceptions. Depuis la version 0.20, il peut également analyser certains packages tiers courants, tels que `mongodb`, `mysql` et `redis`. Tous les événements liés à la demande HTTP entrante tooan sont corrélés de dépannage plus rapide.

Vous pouvez surveiller plusieurs autres aspects de votre application et système en manuellement en instrumentant les à l’aide des API de l’agent hello décrite plus loin.

![Exemples de graphiques d’analyse des performances](./media/app-insights-nodejs/10-perf.png)

## <a name="getting-started"></a>Mise en route

Voyons comment configurer l’analyse d’une application ou d’un service.

### <a name="resource"></a> Configurer une ressource Application Insights

**Avant de commencer**, assurez-vous que vous disposez d’un abonnement Azure ou [obtenez-en un gratuitement][azure-free-offer]. Si votre organisation possède déjà un abonnement Azure, un administrateur peut suivre [ces instructions] [ add-aad-user] tooadd tooit vous.

[azure-free-offer]: https://azure.microsoft.com/en-us/free/
[add-aad-user]: https://docs.microsoft.com/en-us/azure/active-directory/active-directory-users-create-azure-portal

À présent vous connecter toohello [portail Azure] [ portal] et créer une ressource Application Insights, comme illustré dans les éléments suivants de hello - cliquez sur « Nouveau » > « Outils de développement » > « Application Insights ». ressource de Hello inclut un point de terminaison pour recevoir des données de télémétrie, stockage pour ces données, enregistré des rapports et tableaux de bord, règle et configuration d’alerte et bien plus encore.

![Créer une ressource Application Insights](./media/app-insights-nodejs/03-new_appinsights_resource.png)

Sur la page de création d’une ressource de hello, choisissez « Application Node.js » hello application liste déroulante type. type d’application Hello détermine l’ensemble de tableaux de bord et rapports créés pour vous par défaut de hello. Ne vous inquiétez pas : toutes les ressources Application Insights peuvent collecter des données à partir de n’importe quel langage et n’importe quelle plateforme.

![Formulaire de nouvelle ressource Application Insights](./media/app-insights-nodejs/04-create_appinsights_resource.png)

### <a name="agent"></a>Configurer l’agent de hello Node.js

Il est maintenant temps tooinclude hello l’agent dans votre application afin qu’il puisse collecter des données.
Copiez la clé d’Instrumentation de votre ressource (ci-après dénommés tooas votre `ikey`) à partir du portail hello comme indiqué ci-dessous. Hello Insights application système utilise cette tooyour de données de clé toomap ressource Azure, par conséquent, vous devez toospecify dans une variable d’environnement ou hello agent toouse dans votre code.  

![Copier la clé d’instrumentation](./media/app-insights-nodejs/05-appinsights_ikey_portal.png)

Ensuite, ajoutez les dépendances hello Node.js agent bibliothèque tooyour l’application via package.json. À partir du dossier racine de hello de votre application, exécutez :

```bash
npm install applicationinsights --save
```

Vous devez maintenant tooexplicitly chargement de la bibliothèque hello dans votre code. Étant donné que l’agent de hello injecte instrumentation dans nombreuses autres bibliothèques, vous devez le charger dès que possible, même avant les autres `require` instructions. tooget démarré, en haut de hello de votre premier fichier .js ajouter :

```javascript
const appInsights = require("applicationinsights");
appInsights.setup("<instrumentation_key>");
appInsights.start();
```

Hello `setup` méthode configure la clé d’instrumentation hello (et, par conséquent, les ressources Azure) toobe utilisé par défaut pour les éléments de toutes les marques. Appelez `start` une fois la configuration toobegin terminé collecte et l’envoi des données de télémétrie.

Vous pouvez également fournir un ikey via une variable d’environnement hello APPINSIGHTS\_INSTRUMENTATIONKEY au lieu de passer manuellement trop `setup()` ou `getClient()`. Cette pratique permet de conserver ikeys hors code source validée et toospecify des ikeys différentes pour différents environnements.

Des options de configuration supplémentaires sont présentées ci-dessous.

Vous pouvez essayer de l’agent de hello sans envoyer de télémétrie en définissant la chaîne non vide de hello instrumentation tooany clé.

### <a name="monitor"></a> Surveiller votre application

l’agent de Hello rassemble automatiquement télémétrie à propos du runtime de Node.js hello et certains modules tiers communs. Utilisez votre toogenerate de maintenant application certaines de ces données.

Ensuite, dans hello [portail Azure] [ portal] parcourir les ressources d’Application Insights toohello vous avez créé précédemment et rechercher votre premier quelques points de données dans la chronologie de vue d’ensemble de hello, comme dans hello suivant l’image. Cliquez sur les graphiques hello pour plus de détails.

![Premiers points de données](./media/app-insights-nodejs/12-first-perf.png)

Cliquez sur hello Application carte bouton tooview hello topologie découverte pour votre application, comme dans hello suivant l’image. Cliquez sur composants de carte hello pour plus de détails.

![Mise en correspondance d’une application simple](./media/app-insights-nodejs/06-appinsights_appmap.png)

En savoir plus sur votre application et résoudre les problèmes à l’aide de hello autres vues disponibles sous hello « Recherchez » section.

![Section Examiner](./media/app-insights-nodejs/07-appinsights_investigate_blades.png)

#### <a name="no-data"></a>Pas de données ?

Étant donné que l’agent de hello des lots de données pour l’envoi d’il peut y avoir un délai avant que les éléments sont affichés dans le portail de hello. Si vous ne voyez pas les données dans votre ressource essayez certaines des hello suivant les correctifs :

* Utilisez application hello plus ; prendre plus d’actions toogenerate plus de télémétrie.
* Cliquez sur **Actualiser** dans l’affichage des ressources portail hello. Graphiques actualiser automatiquement eux-mêmes régulièrement, mais l’actualisation force ce toohappen immédiatement.
* Vérifiez que les [ports sortants requis](app-insights-ip-addresses.md) sont ouverts.
* Ouvrez hello [recherche](app-insights-diagnostic-search.md) vignette et recherchez les événements individuels.
* Vérifiez hello [FAQ][].


## <a name="agent-configuration"></a>Configuration de l’agent

Voici les méthodes de configuration de l’agent hello et leurs valeurs par défaut.

événements de mettre en corrélation toofully dans un service, être tooset vraiment `.setAutoDependencyCorrelation(true)`. Cela permet à l’agent de hello tootrack contexte entre des rappels asynchrones dans Node.js.

```javascript
const appInsights = require("applicationinsights");
appInsights.setup("<instrumentation_key>")
    .setAutoDependencyCorrelation(false)
    .setAutoCollectRequests(true)
    .setAutoCollectPerformance(true)
    .setAutoCollectExceptions(true)
    .setAutoCollectDependencies(true)
    .start();
```

## <a name="agent-api"></a>API de l’agent

<!-- TODO: Fully document agent API. -->

Hello API de l’agent .NET est décrite en détail [ici](app-insights-api-custom-events-metrics.md).

Vous pouvez suivre n’importe quel demande, un événement, une mesure ou une exception à l’aide du client d’Application Insights Node.js hello. Hello exemple suivant illustre certains hello API disponibles.

```javascript
let appInsights = require("applicationinsights");
appInsights.setup().start(); // assuming ikey in env var
let client = appInsights.getClient();

client.trackEvent("my custom event", {customProperty: "custom property value"});
client.trackException(new Error("handled exceptions can be logged with this method"));
client.trackMetric("custom metric", 3);
client.trackTrace("trace message");

let http = require("http");
http.createServer( (req, res) => {
  client.trackRequest(req, res); // Place at hello beginning of your request handler
});
```

### <a name="track-your-dependencies"></a>Suivre les dépendances

```javascript
let appInsights = require("applicationinsights");
let client = appInsights.getClient();

var success = false;
let startTime = Date.now();
// execute dependency call here....
let duration = Date.now() - startTime;
success = true;

client.trackDependency("dependency name", "command name", duration, success);
```

### <a name="add-a-custom-property-tooall-events"></a>Ajouter une propriété personnalisée des événements tooall

```javascript
appInsights.client.commonProperties = {
    environment: process.env.SOME_ENV_VARIABLE
};
```

### <a name="track-http-get-requests"></a>Suivre les demandes HTTP GET

```javascript
var server = http.createServer((req, res) => {
    if ( req.method === "GET" ) {
            appInsights.client.trackRequest(req, res);
    }
    // other work here....
    res.end();
});
```

### <a name="track-server-startup-time"></a>Suivre le temps de démarrage du serveur

```javascript
let start = Date.now();
server.on("listening", () => {
    let duration = Date.now() - start;
    appInsights.client.trackMetric("server startup time", duration);
});
```

## <a name="more-resources"></a>Autres ressources

* [Surveillez la télémétrie dans le portail de hello](app-insights-dashboards.md)
* [Écrire des requêtes Analytics via vos données de télémétrie](app-insights-analytics-tour.md)

<!--references-->

[portal]: https://portal.azure.com/
[FAQ]: app-insights-troubleshoot-faq.md
