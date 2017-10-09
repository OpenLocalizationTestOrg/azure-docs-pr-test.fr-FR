---
title: aaaIntroduction tooAzure application Web sur Linux | Documents Microsoft
description: En savoir plus sur Azure Web App sur Linux.
keywords: azure app service, linux, oss
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: 
ms.assetid: bc85eff6-bbdf-410a-93dc-0f1222796676
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: naziml;wesmc
ms.openlocfilehash: 43b9865ade251909a77429eb3e18fe0bcaac3bde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-web-app-on-linux"></a>Introduction tooAzure application Web sur Linux

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="overview"></a>Vue d'ensemble
Clients peuvent utiliser une application Web sur les applications web Linux toohost en mode natif sur Linux pour les piles d’applications pris en charge. Hello section suivante répertorie les piles d’application hello actuellement prises en charge. 

## <a name="features"></a>Caractéristiques
Web application sur Linux prend actuellement en charge hello suivant des piles d’applications :

* Node.js
    * 4.4
    * 4.5
    * 6.2
    * 6.6
    * 6.9
    * 6.10
    * 6.11
    * 8.0
    * 8.1
* PHP
    * 5.6
    * 7.0
* .Net Core
    * 1.0
    * 1.1
* Ruby
    * 2.3

Les clients peuvent déployer leurs applications à l’aide de :

* FTP
* Git local
* GitHub
* Bitbucket

Pour la mise à l’échelle des applications :

* Les clients peuvent évoluer les applications web en modifiant le niveau de hello de leur plan de Service d’applications
* Clients puissent monter en charge les applications et exécuter plusieurs instances de l’application dans les limites de hello de leur référence (SKU)

Pour Kudu, certaines des fonctionnalités de base hello :

* Environnements
* Déploiements
* Console de base
* SSH

Pour DevOps :

* Environnements intermédiaires
* ACR et DockerHub CI/CD

## <a name="limitations"></a>Limites
Hello portail Azure affiche uniquement pour les fonctions qui fonctionnent actuellement pour l’application Web sur Linux et masque les reste hello. Comme nous activer d’autres fonctionnalités, elles seront visibles sur le portail de hello.

Certaines fonctionnalités, telles que l’intégration de réseau virtuel, l’authentification Azure Active Directory/tierce, ou les extensions de site Kudu, ne sont pas encore disponibles. Une fois que ces fonctionnalités sont disponibles, nous mettrons à jour notre documentation et le blog sur les modifications de hello.

Cette version préliminaire publique est actuellement disponible uniquement dans hello suivant régions :

* Ouest des États-Unis
* Est des États-Unis
* Europe de l'Ouest
* Europe du Nord
* Centre-Sud des États-Unis
* États-Unis - partie centrale septentrionale
* Asie du Sud-Est
* Est de l'Asie
* Est de l’Australie
* Est du Japon
* Sud du Brésil
* Inde du Sud

Web Apps sur Linux est uniquement pris en charge dans des plans de service d’application dédiée hello et n’a pas d’un niveau gratuit ou partagé. En outre, les plans App Service pour les applications web standards et Linux s’excluent mutuellement : vous ne pouvez pas créer une application web Linux dans un plan App Service non Linux.

Web Apps sur Linux doit être créée dans un groupe de ressources qui ne contient-elle pas les applications web non-Linux Bonjour même région.

## <a name="troubleshooting"></a>Résolution des problèmes ##

Lorsque votre application échoue toostart ou utiliser la journalisation hello toocheck à partir de votre application, vérifiez hello que docker enregistre dans le répertoire des fichiers journaux hello. Vous pouvez accéder à ce répertoire par le biais de votre site SCM ou d’un FTP.
toolog hello `stdout` et `stderr` à partir de votre conteneur, vous devez tooenable **journalisation du conteneur Docker** sous **les journaux de diagnostic**.

![Activation de la journalisation][2]

![Utilisation des journaux de Kudu tooview Docker][1]

Vous pouvez accéder à site SCM hello **outils avancés** Bonjour **outils de développement** menu.

## <a name="next-steps"></a>Étapes suivantes
Consultez hello suivant tooget liens démarré avec le Service d’application sur Linux. Vous pouvez poser des questions et signaler vos préoccupations sur [notre forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).

* [Comment toouse une Docker personnalisée de l’image pour l’application Web de Azure sur Linux](app-service-linux-using-custom-docker-image.md)
* [Utilisation de la configuration PM2 pour Node.js dans l’application web Azure sur Linux](app-service-linux-using-nodejs-pm2.md)
* [Utiliser .NET Core dans Web App d’Azure App Service sur Linux](app-service-linux-using-dotnetcore.md)
* [Utiliser Ruby dans Web Apps d’Azure App Service sur Linux](app-service-linux-ruby-get-started.md)
* [FAQ de Web App d’Azure App Service sur Linux](app-service-linux-faq.md)
* [Prise en charge SSH pour Azure Web App sur Linux](./app-service-linux-ssh-support.md)
* [Configurer des environnements intermédiaires dans Azure App Service](./web-sites-staged-publishing.md)
* [Déploiement continu Docker Hub avec l’application web Azure sur Linux](./app-service-linux-ci-cd.md)

<!--Image references-->
[1]: ./media/app-service-linux-intro/kudu-docker-logs.png
[2]: ./media/app-service-linux-intro/logging.png