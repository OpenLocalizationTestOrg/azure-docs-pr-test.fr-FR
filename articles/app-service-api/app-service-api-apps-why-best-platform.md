---
title: "Présentation des applications aaaAPI | Documents Microsoft"
description: "Découvrez comment Azure App Service vous aide à développer, héberger et utiliser des API RESTful."
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 60049a16-8159-47aa-a34b-110be0d8dab6
ms.service: app-service-api
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/23/2016
ms.author: alkarche
ms.openlocfilehash: f066e96db667d4685480001bc43c2b1bff4ea352
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="api-apps-overview"></a>Vue d'ensemble d'API Apps
API apps dans Azure App Service offre fonctionnalités toodevelop plus facile, hôte et consommer des API dans le cloud de hello et sur site. Avec API Apps, vous bénéficiez d’une sécurité de classe entreprise, d’un contrôle d’accès simple, d’une connectivité hybride, de la génération automatique du kit de développement logiciel (SDK) et d’une intégration transparente dans [Logic Apps](../logic-apps/logic-apps-what-are-logic-apps.md).

[Azure App Service](../app-service/app-service-value-prop-what-is.md) est une plateforme entièrement gérée conçue pour les scénarios web et mobiles ainsi que pour les scénarios d’intégration. API Apps est l'un des quatre types d'application proposés par l' [Azure App Service](../app-service/app-service-value-prop-what-is.md).

![Types d’applications dans Azure App Service](./media/app-service-api-apps-why-best-platform/appservicesuite.png)

## <a name="why-use-api-apps"></a>Pourquoi utiliser API Apps ?
Voici les principales fonctionnalités d'API Apps :

* **Mettez votre API existante en tant que-est** - vous n’avez pas toochange code Hello dans votre avantage de tootake API existante des applications API--simplement déployer votre application tooan API de code. Votre API peut utiliser n’importe quel langage ou framework pris en charge par App Service, notamment ASP.NET, C#, Java, PHP, Node.js et Python.
* **Utilisation facile** : le support intégré des [métadonnées d'API Swagger](http://swagger.io/) facilite l'utilisation de vos API par un certain nombre de clients.  Générez automatiquement le code client de vos API dans divers langages, par exemple C#, Java et Javascript. Configurez facilement [CORS](app-service-api-cors-consume-javascript.md) sans modifier votre code. Pour plus d'informations, consultez [Les métadonnées d'App Service API Apps pour la détection d'API et la création de code](app-service-api-metadata.md) et [Consommer une application API à partir de JavaScript à l'aide de CORS](app-service-api-cors-consume-javascript.md). 
* **Contrôle d’accès simple** -protéger une application API à partir de l’accès non authentifié sans code de tooyour de modifications. Des services d'authentification intégrés sécurisent les API contre tout accès par d'autres services ou par des clients représentant des utilisateurs. Les fournisseurs d’identité pris en charge incluent Azure Active Directory, Facebook, Twitter, Google et Microsoft Account. Les clients peuvent utiliser Active Directory Authentication Library (ADAL) ou hello SDK des applications mobiles. Pour plus d’informations, consultez la page [Authentification et autorisation pour API Apps dans Azure App Service](app-service-api-authentication.md).
* **Intégration de Visual Studio** -travail hello de création, déploiement, consommation, débogage et la gestion des applications API rationalisent les outils dédiés dans Visual Studio. Pour plus d’informations, consultez [annonce, hello Azure SDK 2.8.1 pour .NET](https://azure.microsoft.com/blog/announcing-azure-sdk-2-8-1-for-net/).
* **Intégration dans Logic Apps** : les applications API que vous créez peuvent être utilisées par [App Service Logic Apps](../logic-apps/logic-apps-what-are-logic-apps.md).  Pour plus d’informations, consultez [Utilisation de votre API personnalisée hébergée sur App Service avec Logic Apps](../logic-apps/logic-apps-custom-hosted-api.md) et [Nouvelle version de schéma 2015-08-01-preview](../logic-apps/logic-apps-schema-2015-08-01.md).

Une application API peut également tirer parti des fonctionnalités offertes par [Web Apps](../app-service-web/app-service-web-overview.md) et [Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md). Hello inverse est également vrai : Si vous utilisez une application web ou une application mobile toohost une API, elle peut tirer parti des fonctionnalités des applications API tels que les métadonnées Swagger pour le client la génération de code et CORS pour un accès inter-domaines navigateur. Hello uniquement entre hello trois types d’applications (API, web, mobile) diffère nom de hello et l’icône utilisée pour eux dans hello portail Azure.

## <a name="whats-hello-difference-between-api-apps-and-azure-api-management"></a>Qu’est la différence de hello entre les applications API et la gestion des API Azure ?
API Apps et [Gestion des API Azure](../api-management/api-management-key-concepts.md) sont des services complémentaires :

* Le service Gestion des API est conçu pour gérer les API. Vous placez un frontal de la gestion des API sur un toomonitor API et accélérer l’utilisation, manipuler des entrées et sorties, consolidez plusieurs API dans un point de terminaison et ainsi de suite. Hello API gérées peut être hébergé de n’importe où.
* Le service API Apps est conçu pour l’hébergement des API. service de Hello inclut des fonctionnalités qui facilitent le développement et la consommation des API, mais elle ne hello des types d’analyse, la limitation, manipuler ou consolidation que la gestion des API ne. Si vous n’avez pas besoin des fonctionnalités de gestion des API, vous pouvez héberger des API dans API Apps sans utiliser Gestion des API.

Voici un diagramme qui illustre la fonctionnalité Gestion des API utilisée pour les API hébergées dans API Apps et ailleurs.

![Gestion des API Azure et API Apps](./media/app-service-api-apps-why-best-platform/apia-apim.png)

Certaines fonctionnalités de Gestion des API et API Apps présentent des fonctions similaires.  Par exemple, les deux services permettent d’automatiser la prise en charge de CORS. Lorsque vous utilisez ensemble deux services de hello, vous utiliseriez gestion des API pour le service CORS, car il fonctionne comme hello frontal tooyour API apps. 

## <a name="getting-started"></a>Prise en main
tooget démarré avec les applications API en déployant tooone de code d’exemple, consultez Didacticiel hello pour le framework que vous préférez :

* [ASP.NET](app-service-api-dotnet-get-started.md) 
* [Node.JS](app-service-api-nodejs-api-app.md) 
* [Java](app-service-api-java-api-app.md) 

tooask des questions sur les applications de l’API, démarrer un thread Bonjour [Forum sur les applications API](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureAPIApps). 

