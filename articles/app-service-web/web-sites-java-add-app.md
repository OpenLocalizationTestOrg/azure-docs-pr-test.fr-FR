---
title: "aaaAdd un tooAzure d’application Java App Service Web Apps"
description: "Ce didacticiel vous montre comment tooadd une instance tooyour page ou d’application des applications Azure App Service Web qui est déjà configuré toouse Java."
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9b46528b-e2d0-4f26-b8d7-af94bd8c31ef
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 2feb464b2933921ad2887779a6b7589634e2e2f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-java-application-tooazure-app-service-web-apps"></a>Ajouter un tooAzure d’application Java App Service Web Apps
Une fois que vous avez initialisé votre application web Java [Azure App Service] [ Azure App Service] comme décrit dans [créer une application de web Java dans Azure App Service](web-sites-java-get-started.md), vous pouvez télécharger votre application en plaçant votre WAR Bonjour **webapps** dossier.

Hello toohello de chemin d’accès de navigation **webapps** dossier diffère en fonction de la manière de configurer votre instance d’applications Web.

* Si vous configurez votre application web à l’aide de hello Azure Marketplace, hello toohello de chemin d’accès **webapps** dossier se trouve dans un formulaire hello **d:\home\site\wwwroot\bin\application\_server\webapps**, où **application\_serveur** est le nom hello hello du serveur d’applications en vigueur pour votre instance d’applications Web. 
* Si vous configurez votre application web à l’aide de hello interface utilisateur de configuration Azure, hello toohello de chemin d’accès **webapps** dossier se trouve dans un formulaire hello **d:\home\site\wwwroot\webapps**. 

Notez que vous pouvez utiliser tooupload de contrôle de source de votre application ou les pages web, y compris [scénarios d’intégration continue](app-service-continuous-deployment.md). FTP est également une option de téléchargement de votre application ou les pages web ; Pour plus d’informations sur le déploiement de vos applications sur FTP, consultez [déployer votre tooAzure d’application du Service d’applications].

Remarque pour les applications web Tomcat : une fois que vous avez téléchargé votre toohello de fichier WAR **webapps** dossier, serveur d’applications Tomcat hello détectera que vous l’avez ajouté et chargez automatiquement. Notez que si vous copiez le répertoire racine des fichiers (autres que les fichiers WAR) de toohello, serveur d’applications hello devez toobe redémarré pour que ces fichiers sont utilisés. fonctionnalités d’autoload Hello pour les applications web de hello Tomcat Java s’exécutant sur Azure sont basée sur un nouveau fichier WAR ajouté, ou des fichiers ou répertoires ajoutés toohello **webapps** dossier. 

<a name="see-also"></a>

## <a name="see-also"></a>Voir aussi
Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez hello [centre de développement Java Azure].

[application-insights-app-insights-java-get-started](../application-insights/app-insights-java-get-started.md)

<!-- URL List -->

[centre de développement Java Azure]: https://azure.microsoft.com/develop/java/
[Azure App Service]: http://go.microsoft.com/fwlink/?LinkId=529714
[déployer votre tooAzure d’application du Service d’applications]: ./web-sites-deploy.md
