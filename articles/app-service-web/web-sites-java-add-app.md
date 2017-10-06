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
# <a name="add-a-java-application-tooazure-app-service-web-apps"></a><span data-ttu-id="5634c-103">Ajouter un tooAzure d’application Java App Service Web Apps</span><span class="sxs-lookup"><span data-stu-id="5634c-103">Add a Java application tooAzure App Service Web Apps</span></span>
<span data-ttu-id="5634c-104">Une fois que vous avez initialisé votre application web Java [Azure App Service] [ Azure App Service] comme décrit dans [créer une application de web Java dans Azure App Service](web-sites-java-get-started.md), vous pouvez télécharger votre application en plaçant votre WAR Bonjour **webapps** dossier.</span><span class="sxs-lookup"><span data-stu-id="5634c-104">Once you have initialized your Java web app in [Azure App Service][Azure App Service] as documented at [Create a Java web app in Azure App Service](web-sites-java-get-started.md), you can upload your application by placing your WAR in hello **webapps** folder.</span></span>

<span data-ttu-id="5634c-105">Hello toohello de chemin d’accès de navigation **webapps** dossier diffère en fonction de la manière de configurer votre instance d’applications Web.</span><span class="sxs-lookup"><span data-stu-id="5634c-105">hello navigation path toohello **webapps** folder differs based on how you set up your Web Apps instance.</span></span>

* <span data-ttu-id="5634c-106">Si vous configurez votre application web à l’aide de hello Azure Marketplace, hello toohello de chemin d’accès **webapps** dossier se trouve dans un formulaire hello **d:\home\site\wwwroot\bin\application\_server\webapps**, où **application\_serveur** est le nom hello hello du serveur d’applications en vigueur pour votre instance d’applications Web.</span><span class="sxs-lookup"><span data-stu-id="5634c-106">If you set up your web app by using hello Azure Marketplace, hello path toohello **webapps** folder is in hello form **d:\home\site\wwwroot\bin\application\_server\webapps**, where **application\_server** is hello name of hello application server in effect for your Web Apps instance.</span></span> 
* <span data-ttu-id="5634c-107">Si vous configurez votre application web à l’aide de hello interface utilisateur de configuration Azure, hello toohello de chemin d’accès **webapps** dossier se trouve dans un formulaire hello **d:\home\site\wwwroot\webapps**.</span><span class="sxs-lookup"><span data-stu-id="5634c-107">If you set up your web app by using hello Azure configuration UI, hello path toohello **webapps** folder is in hello form **d:\home\site\wwwroot\webapps**.</span></span> 

<span data-ttu-id="5634c-108">Notez que vous pouvez utiliser tooupload de contrôle de source de votre application ou les pages web, y compris [scénarios d’intégration continue](app-service-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="5634c-108">Note that you can use source control tooupload your application or web pages, including [continuous integration scenarios](app-service-continuous-deployment.md).</span></span> <span data-ttu-id="5634c-109">FTP est également une option de téléchargement de votre application ou les pages web ; Pour plus d’informations sur le déploiement de vos applications sur FTP, consultez [déployer votre tooAzure d’application du Service d’applications].</span><span class="sxs-lookup"><span data-stu-id="5634c-109">FTP is also an option for uploading your application or web pages; for more information about deploying your applications over FTP, see [Deploy your app tooAzure App Service].</span></span>

<span data-ttu-id="5634c-110">Remarque pour les applications web Tomcat : une fois que vous avez téléchargé votre toohello de fichier WAR **webapps** dossier, serveur d’applications Tomcat hello détectera que vous l’avez ajouté et chargez automatiquement.</span><span class="sxs-lookup"><span data-stu-id="5634c-110">Note for Tomcat web apps: Once you've uploaded your WAR file toohello **webapps** folder, hello Tomcat application server will detect that you've added it and will automatically load it.</span></span> <span data-ttu-id="5634c-111">Notez que si vous copiez le répertoire racine des fichiers (autres que les fichiers WAR) de toohello, serveur d’applications hello devez toobe redémarré pour que ces fichiers sont utilisés.</span><span class="sxs-lookup"><span data-stu-id="5634c-111">Note that if you copy files (other than WAR files) toohello ROOT directory, hello application server will need toobe restarted before those files are used.</span></span> <span data-ttu-id="5634c-112">fonctionnalités d’autoload Hello pour les applications web de hello Tomcat Java s’exécutant sur Azure sont basée sur un nouveau fichier WAR ajouté, ou des fichiers ou répertoires ajoutés toohello **webapps** dossier.</span><span class="sxs-lookup"><span data-stu-id="5634c-112">hello autoload functionality for hello Tomcat Java web apps running on Azure is based on a new WAR file being added, or new files or directories added toohello **webapps** folder.</span></span> 

<a name="see-also"></a>

## <a name="see-also"></a><span data-ttu-id="5634c-113">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="5634c-113">See Also</span></span>
<span data-ttu-id="5634c-114">Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez hello [centre de développement Java Azure].</span><span class="sxs-lookup"><span data-stu-id="5634c-114">For more information about using Azure with Java, see hello [Azure Java Developer Center].</span></span>

[<span data-ttu-id="5634c-115">application-insights-app-insights-java-get-started</span><span class="sxs-lookup"><span data-stu-id="5634c-115">application-insights-app-insights-java-get-started</span></span>](../application-insights/app-insights-java-get-started.md)

<!-- URL List -->

[centre de développement Java Azure]: https://azure.microsoft.com/develop/java/
[Azure App Service]: http://go.microsoft.com/fwlink/?LinkId=529714
[déployer votre tooAzure d’application du Service d’applications]: ./web-sites-deploy.md
