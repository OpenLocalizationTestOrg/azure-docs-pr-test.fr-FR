---
title: Ajouter une application Java dans Azure App Service Web Apps
description: "Ce didacticiel vous montre comment ajouter une page ou une application à votre instance d’Azure App Service Web Apps déjà configurée pour utiliser Java."
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
ms.openlocfilehash: c28e7c499ed02b759df580f4b14a971b6aec5b67
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="add-a-java-application-to-azure-app-service-web-apps"></a><span data-ttu-id="41b39-103">Ajouter une application Java dans Azure App Service Web Apps</span><span class="sxs-lookup"><span data-stu-id="41b39-103">Add a Java application to Azure App Service Web Apps</span></span>
<span data-ttu-id="41b39-104">Une fois que vous avez initialisé votre application web Java dans [Azure App Service][Azure App Service] comme indiqué dans [Créer une application web Java dans Azure App Service](web-sites-java-get-started.md), vous pouvez télécharger votre application en plaçant votre fichier WAR dans le dossier **webapps**.</span><span class="sxs-lookup"><span data-stu-id="41b39-104">Once you have initialized your Java web app in [Azure App Service][Azure App Service] as documented at [Create a Java web app in Azure App Service](web-sites-java-get-started.md), you can upload your application by placing your WAR in the **webapps** folder.</span></span>

<span data-ttu-id="41b39-105">Le chemin d’accès au dossier **webapps** varie en fonction de la configuration de votre instance Web Apps.</span><span class="sxs-lookup"><span data-stu-id="41b39-105">The navigation path to the **webapps** folder differs based on how you set up your Web Apps instance.</span></span>

* <span data-ttu-id="41b39-106">Si vous configurez votre application web à l’aide de la Place de marché Azure, le chemin d’accès au dossier **webapps** se présente sous la forme **d:\home\site\wwwroot\bin\serveur\_applications\webapps**, où **serveur\_applications** est le nom du serveur d’applications de votre instance Web Apps.</span><span class="sxs-lookup"><span data-stu-id="41b39-106">If you set up your web app by using the Azure Marketplace, the path to the **webapps** folder is in the form **d:\home\site\wwwroot\bin\application\_server\webapps**, where **application\_server** is the name of the application server in effect for your Web Apps instance.</span></span> 
* <span data-ttu-id="41b39-107">Si vous configurez votre application web à l’aide de l’interface utilisateur d’Azure, le chemin d’accès au dossier **webapps** se présente sous la forme **d:\home\site\wwwroot\webapps**.</span><span class="sxs-lookup"><span data-stu-id="41b39-107">If you set up your web app by using the Azure configuration UI, the path to the **webapps** folder is in the form **d:\home\site\wwwroot\webapps**.</span></span> 

<span data-ttu-id="41b39-108">Notez que vous pouvez utiliser le contrôle de code source pour charger votre application ou vos pages web, y compris dans des [scénarios d’intégration continue](app-service-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="41b39-108">Note that you can use source control to upload your application or web pages, including [continuous integration scenarios](app-service-continuous-deployment.md).</span></span> <span data-ttu-id="41b39-109">Le protocole FTP permet également de télécharger votre application ou des pages web. Pour plus d’informations sur le déploiement de vos applications via FTP, voir [Déploiement de votre application dans Azure App Service].</span><span class="sxs-lookup"><span data-stu-id="41b39-109">FTP is also an option for uploading your application or web pages; for more information about deploying your applications over FTP, see [Deploy your app to Azure App Service].</span></span>

<span data-ttu-id="41b39-110">Remarque pour les applications web Tomcat : une fois que vous avez téléchargé votre fichier WAR dans le dossier **webapps** , le serveur d’applications Tomcat détecte que vous l’avez ajouté et le charge automatiquement.</span><span class="sxs-lookup"><span data-stu-id="41b39-110">Note for Tomcat web apps: Once you've uploaded your WAR file to the **webapps** folder, the Tomcat application server will detect that you've added it and will automatically load it.</span></span> <span data-ttu-id="41b39-111">Notez que si vous copiez des fichiers (autres que des fichiers WAR) dans le répertoire ROOT, vous devez redémarrer le serveur d'applications avant d'utiliser ces fichiers.</span><span class="sxs-lookup"><span data-stu-id="41b39-111">Note that if you copy files (other than WAR files) to the ROOT directory, the application server will need to be restarted before those files are used.</span></span> <span data-ttu-id="41b39-112">La fonctionnalité de chargement automatique des applications web Java Tomcat exécutées sur Azure repose sur l’ajout d’un fichier WAR ou de nouveaux fichiers ou répertoires dans le dossier **webapps** .</span><span class="sxs-lookup"><span data-stu-id="41b39-112">The autoload functionality for the Tomcat Java web apps running on Azure is based on a new WAR file being added, or new files or directories added to the **webapps** folder.</span></span> 

<a name="see-also"></a>

## <a name="see-also"></a><span data-ttu-id="41b39-113">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="41b39-113">See Also</span></span>
<span data-ttu-id="41b39-114">Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez le [Centre de développement Java pour Azure].</span><span class="sxs-lookup"><span data-stu-id="41b39-114">For more information about using Azure with Java, see the [Azure Java Developer Center].</span></span>

[<span data-ttu-id="41b39-115">application-insights-app-insights-java-get-started</span><span class="sxs-lookup"><span data-stu-id="41b39-115">application-insights-app-insights-java-get-started</span></span>](../application-insights/app-insights-java-get-started.md)

<!-- URL List -->

<span data-ttu-id="41b39-116">[Centre de développement Java pour Azure]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="41b39-116">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
[Azure App Service]: http://go.microsoft.com/fwlink/?LinkId=529714
<span data-ttu-id="41b39-117">[Déploiement de votre application dans Azure App Service]: ./web-sites-deploy.md</span><span class="sxs-lookup"><span data-stu-id="41b39-117">[Deploy your app to Azure App Service]: ./web-sites-deploy.md</span></span>
