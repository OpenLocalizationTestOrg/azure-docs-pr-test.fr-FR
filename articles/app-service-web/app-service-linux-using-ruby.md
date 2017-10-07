---
title: aaaUsing Ruby dans Azure App Service Web App sur Linux | Documents Microsoft
description: "Utilisation de Ruby dans l’application web Azure App Service sur Linux."
keywords: azure app service, application web, faq, linux, oss, ruby
services: app-service
documentationCenter: 
author: ahmedelnably
manager: erikre
editor: 
ms.assetid: 
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: aelnably;wesmc
ms.openlocfilehash: 45692cb3bf1da9ff65b9466055029bfaef8b7d8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-ruby-in-web-app-on-linux"></a>Utilisation de Ruby dans Web App sur Linux #

Avec la dernière mise à jour tooour principal de hello, nous avons introduit la prise en charge de v.2.3 Ruby. En définissant la configuration hello de votre application web de Linux, vous pouvez modifier la pile de l’application hello.

## <a name="using-hello-azure-portal"></a>À l’aide de hello portail Azure ##

À partir du menu Nouveau hello hello [portail Azure](https://portal.azure.com), vous pouvez choisir toocreate une application Web sur Linux à partir de hello Web + option Mobile comme indiqué dans hello suivant image :

![Démarrer la création d’une application web sur hello portail Azure][1]

Ensuite, hello **créer panneau** s’ouvre comme indiqué dans hello suivant image :

![Panneau de création de Hello][2]

1. Donnez un nom à votre application web.
2. Sélectionnez un groupe de ressources existant ou créez-en un. (Consultez les régions disponibles Bonjour [section limitations](app-service-linux-intro.md).)
3. Sélectionnez un plan Azure App Service existant ou créez-en un. (Consultez les remarques du plan App Service Bonjour [section limitations](app-service-linux-intro.md).)
4. Choisissez hello Ruby des piles de Runtime intégrées hello.

Une fois que votre application web Ruby est créée, vous pouvez déployer tooit à l’aide de Git ou FTP.

toolearn en savoir plus sur la création d’une application Ruby, vérifiez hello [guide pas à pas de get](app-service-linux-ruby-get-started.md)

## <a name="next-steps"></a>Étapes suivantes
* [Qu’est-ce que Web App sur Linux ?](app-service-linux-intro.md)
* [TooAzure déploiement Git local du Service d’applications](app-service-deploy-local-git.md)
* [FAQ de l’application web Azure App Service sur Linux](app-service-linux-faq.md)
* [Créer une application Ruby avec Azure Web App sur Linux](app-service-linux-ruby-get-started.md)

<!--Image references-->
[1]: ./media/app-service-linux-using-ruby/New-Linux.png
[2]: ./media/app-service-linux-using-ruby/Ruby-UX.png