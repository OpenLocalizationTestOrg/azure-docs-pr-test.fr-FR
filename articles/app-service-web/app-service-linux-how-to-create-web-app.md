---
title: "aaaCreate Azure web application en cours d’exécution sur Linux | Documents Microsoft"
description: "Workflow de création d’application web Azure Web App sur Linux."
keywords: azure app service, application web, linux, oss
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: 
ms.assetid: 3a71d10a-a0fe-4d28-af95-03b2860057d5
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: naziml;wesmc
ms.openlocfilehash: de1bd030345d5e2a8024012067b5bcaa2cca09dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-web-app-running-on-linux"></a>Créer une application web Azure en cours d’exécution sur Linux

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


## <a name="use-hello-azure-portal-toocreate-your-web-app"></a>Utilisez hello toocreate portail Azure à votre application web
Vous pouvez commencer à créer votre application web sur Linux à partir de hello [portail Azure](https://portal.azure.com) comme indiqué dans hello suivant image :

![Démarrer la création d’une application web sur hello portail Azure][1]

Ensuite, hello **créer panneau** s’ouvre comme indiqué dans hello suivant image :

![Panneau de création de Hello][2]

1. Donnez un nom à votre application web.
2. Sélectionnez un groupe de ressources existant ou créez-en un. (Consultez les régions disponibles Bonjour [section limitations](app-service-linux-intro.md).)
3. Sélectionnez un plan Azure App Service existant ou créez-en un. (Consultez les remarques du plan App Service Bonjour [section limitations](app-service-linux-intro.md).)
4. Choisissez l’application hello pile que vous avez l’intention de toouse. Vous pouvez choisir entre plusieurs versions de Node.js, PHP, .Net Core et Ruby.

Une fois que vous avez créé l’application hello, vous pouvez modifier pile de l’application hello à partir des paramètres de l’application hello comme indiqué dans hello suivant image :

![Paramètres de l’application][3]

## <a name="deploy-your-web-app"></a>Déployez votre application web
En choisissant **options de déploiement** à partir de l’offre de portail de gestion hello vous hello option toouse local Git ou GitHub référentiel toodeploy votre application. Hello autres instructions de hello sont toothose similaires pour une application web de non-Linux. Vous pouvez suivre les instructions hello dans [déploiement Git local](app-service-deploy-local-git.md) ou [déploiement continu](app-service-continuous-deployment.md) toodeploy votre application.

Vous pouvez également utiliser les tooupload FTP à votre site de tooyour d’application. Vous pouvez obtenir le point de terminaison hello FTP pour votre application web des diagnostics de hello section journaux comme indiqué dans hello suivant image :

![Journaux de diagnostics][4]

## <a name="next-steps"></a>Étapes suivantes
* [Qu’est-ce qu’Azure Web App sur Linux ?](app-service-linux-intro.md)
* [Utiliser la configuration PM2 pour Node.js dans Azure Web App sur Linux](app-service-linux-using-nodejs-pm2.md)
* [Utiliser Ruby dans l’application web Azure App Service sur Linux](app-service-linux-ruby-get-started.md)
* [FAQ de l’application web Azure App Service sur Linux](app-service-linux-faq.md)

<!--Image references-->
[1]: ./media/app-service-linux-how-to-create-a-web-app/top-level-create.png
[2]: ./media/app-service-linux-how-to-create-a-web-app/create-blade.png
[3]: ./media/app-service-linux-how-to-create-a-web-app/application-settings-change-stack.png
[4]: ./media/app-service-linux-how-to-create-a-web-app/diagnostic-logs-ftp.png
