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
# <a name="create-an-azure-web-app-running-on-linux"></a><span data-ttu-id="e14fb-104">Créer une application web Azure en cours d’exécution sur Linux</span><span class="sxs-lookup"><span data-stu-id="e14fb-104">Create an Azure web app running on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


## <a name="use-hello-azure-portal-toocreate-your-web-app"></a><span data-ttu-id="e14fb-105">Utilisez hello toocreate portail Azure à votre application web</span><span class="sxs-lookup"><span data-stu-id="e14fb-105">Use hello Azure portal toocreate your web app</span></span>
<span data-ttu-id="e14fb-106">Vous pouvez commencer à créer votre application web sur Linux à partir de hello [portail Azure](https://portal.azure.com) comme indiqué dans hello suivant image :</span><span class="sxs-lookup"><span data-stu-id="e14fb-106">You can start creating your web app on Linux from hello [Azure portal](https://portal.azure.com) as shown in hello following image:</span></span>

![Démarrer la création d’une application web sur hello portail Azure][1]

<span data-ttu-id="e14fb-108">Ensuite, hello **créer panneau** s’ouvre comme indiqué dans hello suivant image :</span><span class="sxs-lookup"><span data-stu-id="e14fb-108">Next, hello **Create blade** opens as shown in hello following image:</span></span>

![Panneau de création de Hello][2]

1. <span data-ttu-id="e14fb-110">Donnez un nom à votre application web.</span><span class="sxs-lookup"><span data-stu-id="e14fb-110">Give your web app a name.</span></span>
2. <span data-ttu-id="e14fb-111">Sélectionnez un groupe de ressources existant ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="e14fb-111">Choose an existing resource group or create a new one.</span></span> <span data-ttu-id="e14fb-112">(Consultez les régions disponibles Bonjour [section limitations](app-service-linux-intro.md).)</span><span class="sxs-lookup"><span data-stu-id="e14fb-112">(See available regions in hello [limitations section](app-service-linux-intro.md).)</span></span>
3. <span data-ttu-id="e14fb-113">Sélectionnez un plan Azure App Service existant ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="e14fb-113">Choose an existing Azure App Service plan or create a new one.</span></span> <span data-ttu-id="e14fb-114">(Consultez les remarques du plan App Service Bonjour [section limitations](app-service-linux-intro.md).)</span><span class="sxs-lookup"><span data-stu-id="e14fb-114">(See App Service plan notes in hello [limitations section](app-service-linux-intro.md).)</span></span>
4. <span data-ttu-id="e14fb-115">Choisissez l’application hello pile que vous avez l’intention de toouse.</span><span class="sxs-lookup"><span data-stu-id="e14fb-115">Choose hello application stack that you intend toouse.</span></span> <span data-ttu-id="e14fb-116">Vous pouvez choisir entre plusieurs versions de Node.js, PHP, .Net Core et Ruby.</span><span class="sxs-lookup"><span data-stu-id="e14fb-116">You can choose between several versions of Node.js, PHP, .Net Core, and Ruby.</span></span>

<span data-ttu-id="e14fb-117">Une fois que vous avez créé l’application hello, vous pouvez modifier pile de l’application hello à partir des paramètres de l’application hello comme indiqué dans hello suivant image :</span><span class="sxs-lookup"><span data-stu-id="e14fb-117">Once you have created hello app, you can change hello application stack from hello application settings as shown in hello following image:</span></span>

![Paramètres de l’application][3]

## <a name="deploy-your-web-app"></a><span data-ttu-id="e14fb-119">Déployez votre application web</span><span class="sxs-lookup"><span data-stu-id="e14fb-119">Deploy your web app</span></span>
<span data-ttu-id="e14fb-120">En choisissant **options de déploiement** à partir de l’offre de portail de gestion hello vous hello option toouse local Git ou GitHub référentiel toodeploy votre application.</span><span class="sxs-lookup"><span data-stu-id="e14fb-120">Choosing **deployment options** from hello management portal gives you hello option toouse local Git or GitHub repository toodeploy your application.</span></span> <span data-ttu-id="e14fb-121">Hello autres instructions de hello sont toothose similaires pour une application web de non-Linux.</span><span class="sxs-lookup"><span data-stu-id="e14fb-121">hello rest of hello instructions are similar toothose for a non-Linux web app.</span></span> <span data-ttu-id="e14fb-122">Vous pouvez suivre les instructions hello dans [déploiement Git local](app-service-deploy-local-git.md) ou [déploiement continu](app-service-continuous-deployment.md) toodeploy votre application.</span><span class="sxs-lookup"><span data-stu-id="e14fb-122">You can follow hello instructions in [local Git deployment](app-service-deploy-local-git.md) or [continuous deployment](app-service-continuous-deployment.md) toodeploy your app.</span></span>

<span data-ttu-id="e14fb-123">Vous pouvez également utiliser les tooupload FTP à votre site de tooyour d’application.</span><span class="sxs-lookup"><span data-stu-id="e14fb-123">You can also use FTP tooupload your application tooyour site.</span></span> <span data-ttu-id="e14fb-124">Vous pouvez obtenir le point de terminaison hello FTP pour votre application web des diagnostics de hello section journaux comme indiqué dans hello suivant image :</span><span class="sxs-lookup"><span data-stu-id="e14fb-124">You can get hello FTP endpoint for your web app from hello diagnostics logs section as shown in hello following image:</span></span>

![Journaux de diagnostics][4]

## <a name="next-steps"></a><span data-ttu-id="e14fb-126">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e14fb-126">Next steps</span></span>
* [<span data-ttu-id="e14fb-127">Qu’est-ce qu’Azure Web App sur Linux ?</span><span class="sxs-lookup"><span data-stu-id="e14fb-127">What is Azure Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="e14fb-128">Utiliser la configuration PM2 pour Node.js dans Azure Web App sur Linux</span><span class="sxs-lookup"><span data-stu-id="e14fb-128">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="e14fb-129">Utiliser Ruby dans l’application web Azure App Service sur Linux</span><span class="sxs-lookup"><span data-stu-id="e14fb-129">Using Ruby in Azure App Service Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="e14fb-130">FAQ de l’application web Azure App Service sur Linux</span><span class="sxs-lookup"><span data-stu-id="e14fb-130">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)

<!--Image references-->
[1]: ./media/app-service-linux-how-to-create-a-web-app/top-level-create.png
[2]: ./media/app-service-linux-how-to-create-a-web-app/create-blade.png
[3]: ./media/app-service-linux-how-to-create-a-web-app/application-settings-change-stack.png
[4]: ./media/app-service-linux-how-to-create-a-web-app/diagnostic-logs-ftp.png
