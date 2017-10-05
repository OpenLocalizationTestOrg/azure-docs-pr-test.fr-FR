---
title: "Créer une application web Azure en cours d’exécution sur Linux | Microsoft Docs"
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
ms.openlocfilehash: 49091d4a85bed23927850f9c0bbc5ea8b6e8c9e1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-web-app-running-on-linux"></a><span data-ttu-id="69348-104">Créer une application web Azure en cours d’exécution sur Linux</span><span class="sxs-lookup"><span data-stu-id="69348-104">Create an Azure web app running on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


## <a name="use-the-azure-portal-to-create-your-web-app"></a><span data-ttu-id="69348-105">Utiliser le portail Azure pour créer votre application web</span><span class="sxs-lookup"><span data-stu-id="69348-105">Use the Azure portal to create your web app</span></span>
<span data-ttu-id="69348-106">Vous pouvez commencer à créer votre application web sur Linux à partir du [portail Azure](https://portal.azure.com) comme indiqué dans l’image suivante :</span><span class="sxs-lookup"><span data-stu-id="69348-106">You can start creating your web app on Linux from the [Azure portal](https://portal.azure.com) as shown in the following image:</span></span>

![Commencez à créer une application web sur le portail Azure][1]

<span data-ttu-id="69348-108">Ensuite, le **panneau Créer** s’ouvre comme indiqué dans l’image suivante :</span><span class="sxs-lookup"><span data-stu-id="69348-108">Next, the **Create blade** opens as shown in the following image:</span></span>

![Panneau Créer][2]

1. <span data-ttu-id="69348-110">Donnez un nom à votre application web.</span><span class="sxs-lookup"><span data-stu-id="69348-110">Give your web app a name.</span></span>
2. <span data-ttu-id="69348-111">Sélectionnez un groupe de ressources existant ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="69348-111">Choose an existing resource group or create a new one.</span></span> <span data-ttu-id="69348-112">(Consultez les régions disponibles dans la [section Limitations](app-service-linux-intro.md).)</span><span class="sxs-lookup"><span data-stu-id="69348-112">(See available regions in the [limitations section](app-service-linux-intro.md).)</span></span>
3. <span data-ttu-id="69348-113">Sélectionnez un plan Azure App Service existant ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="69348-113">Choose an existing Azure App Service plan or create a new one.</span></span> <span data-ttu-id="69348-114">(Consultez les notes relatives au plan App Service dans la [section Limitations](app-service-linux-intro.md).)</span><span class="sxs-lookup"><span data-stu-id="69348-114">(See App Service plan notes in the [limitations section](app-service-linux-intro.md).)</span></span>
4. <span data-ttu-id="69348-115">Sélectionnez la pile d’applications que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="69348-115">Choose the application stack that you intend to use.</span></span> <span data-ttu-id="69348-116">Vous pouvez choisir entre plusieurs versions de Node.js, PHP, .Net Core et Ruby.</span><span class="sxs-lookup"><span data-stu-id="69348-116">You can choose between several versions of Node.js, PHP, .Net Core, and Ruby.</span></span>

<span data-ttu-id="69348-117">Une fois que vous avez créé l’application, vous pouvez modifier la pile d’applications dans les paramètres de l’application comme illustré dans l’image suivante :</span><span class="sxs-lookup"><span data-stu-id="69348-117">Once you have created the app, you can change the application stack from the application settings as shown in the following image:</span></span>

![Paramètres de l’application][3]

## <a name="deploy-your-web-app"></a><span data-ttu-id="69348-119">Déployez votre application web</span><span class="sxs-lookup"><span data-stu-id="69348-119">Deploy your web app</span></span>
<span data-ttu-id="69348-120">Les **options de déploiement** disponibles dans le portail de gestion vous permettent d’utiliser un référentiel Git local ou GitHub pour déployer votre application.</span><span class="sxs-lookup"><span data-stu-id="69348-120">Choosing **deployment options** from the management portal gives you the option to use local Git or GitHub repository to deploy your application.</span></span> <span data-ttu-id="69348-121">Les autres instructions sont similaires à celles d’une application non-Linux.</span><span class="sxs-lookup"><span data-stu-id="69348-121">The rest of the instructions are similar to those for a non-Linux web app.</span></span> <span data-ttu-id="69348-122">Vous pouvez suivre les instructions de [déploiement Git local](app-service-deploy-local-git.md) ou [déploiement continu](app-service-continuous-deployment.md) pour déployer votre application.</span><span class="sxs-lookup"><span data-stu-id="69348-122">You can follow the instructions in [local Git deployment](app-service-deploy-local-git.md) or [continuous deployment](app-service-continuous-deployment.md) to deploy your app.</span></span>

<span data-ttu-id="69348-123">Vous pouvez également utiliser FTP pour télécharger votre application sur votre site.</span><span class="sxs-lookup"><span data-stu-id="69348-123">You can also use FTP to upload your application to your site.</span></span> <span data-ttu-id="69348-124">Vous pouvez obtenir le point de terminaison FTP de votre application web à partir de la section des journaux de diagnostics, comme illustré dans l’image suivante :</span><span class="sxs-lookup"><span data-stu-id="69348-124">You can get the FTP endpoint for your web app from the diagnostics logs section as shown in the following image:</span></span>

![Journaux de diagnostics][4]

## <a name="next-steps"></a><span data-ttu-id="69348-126">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="69348-126">Next steps</span></span>
* [<span data-ttu-id="69348-127">Qu’est-ce qu’Azure Web App sur Linux ?</span><span class="sxs-lookup"><span data-stu-id="69348-127">What is Azure Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="69348-128">Utiliser la configuration PM2 pour Node.js dans Azure Web App sur Linux</span><span class="sxs-lookup"><span data-stu-id="69348-128">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="69348-129">Utiliser Ruby dans l’application web Azure App Service sur Linux</span><span class="sxs-lookup"><span data-stu-id="69348-129">Using Ruby in Azure App Service Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="69348-130">FAQ de l’application web Azure App Service sur Linux</span><span class="sxs-lookup"><span data-stu-id="69348-130">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)

<!--Image references-->
[1]: ./media/app-service-linux-how-to-create-a-web-app/top-level-create.png
[2]: ./media/app-service-linux-how-to-create-a-web-app/create-blade.png
[3]: ./media/app-service-linux-how-to-create-a-web-app/application-settings-change-stack.png
[4]: ./media/app-service-linux-how-to-create-a-web-app/diagnostic-logs-ftp.png
