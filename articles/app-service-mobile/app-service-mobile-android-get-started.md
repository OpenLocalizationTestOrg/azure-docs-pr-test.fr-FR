---
title: aaaCreate une application Android sur Azure App Service Mobile Apps | Documents Microsoft
description: "Suivez ce didacticiel tooget un bon départ avec les serveurs principaux de l’application mobile Azure pour le développement Android"
services: app-service\mobile
documentationcenter: android
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 355f0959-aa7f-472c-a6c7-9eecea3a34a9
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 0af85a3a4de9fc265976bbe3f34d73effc3807df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-android-app"></a>Créer une application Android
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a>Vue d'ensemble
Ce didacticiel vous montre comment tooadd un backend de cloud service tooan des applications mobiles Android à l’aide d’un serveur principal d’application mobile Azure.  Vous allez créer un backend d’application mobile et une simple application Android *Todo list* qui stocke les données d’application dans Azure.

Ils auront terminé ce didacticiel est un composant requis pour tous les autres didacticiels Android sur l’utilisation de la fonctionnalité des applications mobiles hello dans Azure App Service.

## <a name="prerequisites"></a>Composants requis
toocomplete ce didacticiel, vous devez hello suivant :

* [Les outils de développement Android](https://developer.android.com/sdk/index.html), qui inclut l’environnement de développement intégré Android hello et la plateforme Android hello la plus récente.
* Azure Mobile Android SDK, qui est référencé automatiquement dans le cadre du projet de démarrage rapide de hello que vous téléchargez.
* Un [compte Azure actif](https://azure.microsoft.com/pricing/free-trial/).

## <a name="create-a-new-azure-mobile-app-backend"></a>Créer un serveur principal d'applications mobiles Azure
[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

## <a name="configure-hello-server-project"></a>Configurer le projet de serveur hello
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-android-app"></a>Téléchargez et exécutez l’application Android hello
[!INCLUDE [app-service-mobile-android-run-app](../../includes/app-service-mobile-android-run-app.md)]

<!-- URLs -->
[Azure portal]: https://portal.azure.com/
[Visual Studio Community 2013]: https://go.microsoft.com/fwLink/p/?LinkID=534203
