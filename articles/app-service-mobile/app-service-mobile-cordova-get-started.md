---
title: aaaCreate une application Cordova sur Azure App Service Mobile Apps | Documents Microsoft
description: "Suivez ce didacticiel tooget un bon départ avec les serveurs principaux de l’application mobile Azure pour le développement d’Apache Cordova"
services: app-service\mobile
documentationcenter: javascript
author: ggailey777
manager: syntaxc4
editor: 
tags: 
keywords: cordova, javascript, mobile, client
ms.assetid: 0b08fc12-0a80-42d3-9cc1-9b3f8d3e3a3f
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-html
ms.devlang: javascript
ms.topic: hero-article
ms.date: 07/07/2017
ms.author: glenga
ms.openlocfilehash: 4981cbc0686c15230019ac9f30495f30cbf2c791
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-apache-cordova-app"></a>Créer une application Apache Cordova
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a>Vue d'ensemble
Ce didacticiel vous montre comment tooadd un backend de cloud service application mobile de tooan Apache Cordova à l’aide d’un serveur principal d’application mobile Azure.  Vous créez un backend d’application mobile et une simple application Apache Cordova *Todo list* qui stocke les données d’application dans Azure.

Ils auront terminé ce didacticiel est un composant requis pour tous les autres didacticiels Apache Cordova sur l’utilisation de la fonctionnalité des applications mobiles hello dans Azure App Service.

## <a name="prerequisites"></a>Composants requis
toocomplete ce didacticiel, vous devez hello suivant des conditions préalables :

* Un PC équipé de [Visual Studio Community 2017] ou d’une version plus récente.
* [Visual Studio Tools pour Apache Cordova].
* Un [compte Azure actif](https://azure.microsoft.com/pricing/free-trial/).

Vous pouvez également contourner Visual Studio et utiliser directement de ligne de commande Apache Cordova hello.  À l’aide de la ligne de commande hello est utile lorsqu’il a terminé le didacticiel hello sur un ordinateur Mac.  Compiler des applications client Apache Cordova à l’aide de la ligne de commande hello n’est pas couverte par ce didacticiel.

## <a name="create-an-azure-mobile-app-backend"></a>Créer un serveur principal d'applications mobiles Azure
[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

[Regarder une vidéo montrant des étapes similaires](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-1-Create-an-Azure-Mobile-App)

## <a name="configure-hello-server-project"></a>Configurer le projet de serveur hello
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-apache-cordova-app"></a>Téléchargez et exécutez l’application de hello Apache Cordova
[!INCLUDE [app-service-mobile-cordova-run-app](../../includes/app-service-mobile-cordova-run-app.md)]

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous terminé ce didacticiel de démarrage rapide, déplacez les tooone Hello suivant didacticiels :

* [Ajouter des données en mode hors connexion](app-service-mobile-cordova-get-started-offline-data.md) tooyour Apache Cordova application.
* [Ajouter l’authentification](app-service-mobile-cordova-get-started-users.md) tooyour Apache Cordova application.
* [Ajouter des Notifications Push](app-service-mobile-cordova-get-started-push.md) tooyour Apache Cordova application.

En savoir plus sur les concepts clés avec Azure App Service.

* [Données hors connexion]
* [Authentification]
* [Notifications Push]

Découvrez comment toouse hello kits de développement logiciel.

* [Kit de développement logiciel (SDK) Apache Cordova]
* [Kit de développement logiciel du serveur ASP.NET]
* [Kit de développement logiciel du serveur Node.js]

<!-- Images. -->

<!-- URLs -->
[Azure portal]: https://portal.azure.com/
[Visual Studio Community 2017]: http://www.visualstudio.com/
[Visual Studio Tools pour Apache Cordova]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx
[Données hors connexion]: app-service-mobile-offline-data-sync.md
[Authentification]: app-service-mobile-auth.md
[Notifications Push]: ../notification-hubs/notification-hubs-push-notification-overview.md
[Kit de développement logiciel (SDK) Apache Cordova]: app-service-mobile-cordova-how-to-use-client-library.md
[Kit de développement logiciel du serveur ASP.NET]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Kit de développement logiciel du serveur Node.js]: app-service-mobile-node-backend-how-to-use-server-sdk.md
