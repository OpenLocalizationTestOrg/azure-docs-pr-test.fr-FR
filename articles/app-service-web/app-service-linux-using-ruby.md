---
title: "Utilisation de Ruby dans l’application web Azure App Service sur Linux | Microsoft Docs"
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
ms.openlocfilehash: 56105d1bc153e552e12c0c408c8f6075e4eff9d0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="using-ruby-in-web-app-on-linux"></a><span data-ttu-id="c3fdc-104">Utilisation de Ruby dans Web App sur Linux</span><span class="sxs-lookup"><span data-stu-id="c3fdc-104">Using Ruby in Web App on Linux</span></span> #

<span data-ttu-id="c3fdc-105">Lors de la dernière mise à jour de notre serveur principal, nous avons introduit la prise en charge de Ruby v.2.3.</span><span class="sxs-lookup"><span data-stu-id="c3fdc-105">With the latest update to our backend, we introduced support for Ruby v.2.3.</span></span> <span data-ttu-id="c3fdc-106">En définissant la configuration de votre application web Linux, vous pouvez modifier la pile d’applications.</span><span class="sxs-lookup"><span data-stu-id="c3fdc-106">By setting the configuration of your Linux web app, you can change the application stack.</span></span>

## <a name="using-the-azure-portal"></a><span data-ttu-id="c3fdc-107">Utilisation du portail Azure</span><span class="sxs-lookup"><span data-stu-id="c3fdc-107">Using the Azure portal</span></span> ##

<span data-ttu-id="c3fdc-108">Dans le nouveau menu du [portail](https://portal.azure.com), vous pouvez choisir de créer une application Web sur Linux à partir de l’option Web + Mobile comme indiqué dans l’image suivante :</span><span class="sxs-lookup"><span data-stu-id="c3fdc-108">From the new menu in the [Azure portal](https://portal.azure.com), you can choose to create a Web App on Linux from the Web + Mobile option as shown in the following image:</span></span>

![Commencez à créer une application web sur le portail Azure][1]

<span data-ttu-id="c3fdc-110">Ensuite, le **panneau Créer** s’ouvre comme indiqué dans l’image suivante :</span><span class="sxs-lookup"><span data-stu-id="c3fdc-110">Next, the **Create blade** opens as shown in the following image:</span></span>

![Panneau Créer][2]

1. <span data-ttu-id="c3fdc-112">Donnez un nom à votre application web.</span><span class="sxs-lookup"><span data-stu-id="c3fdc-112">Give your web app a name.</span></span>
2. <span data-ttu-id="c3fdc-113">Sélectionnez un groupe de ressources existant ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="c3fdc-113">Choose an existing resource group or create a new one.</span></span> <span data-ttu-id="c3fdc-114">(Consultez les régions disponibles dans la [section Limitations](app-service-linux-intro.md).)</span><span class="sxs-lookup"><span data-stu-id="c3fdc-114">(See available regions in the [limitations section](app-service-linux-intro.md).)</span></span>
3. <span data-ttu-id="c3fdc-115">Sélectionnez un plan Azure App Service existant ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="c3fdc-115">Choose an existing Azure App Service plan or create a new one.</span></span> <span data-ttu-id="c3fdc-116">(Consultez les notes relatives au plan App Service dans la [section Limitations](app-service-linux-intro.md).)</span><span class="sxs-lookup"><span data-stu-id="c3fdc-116">(See App Service plan notes in the [limitations section](app-service-linux-intro.md).)</span></span>
4. <span data-ttu-id="c3fdc-117">Choisissez l’application Ruby dans les piles Runtime intégrées.</span><span class="sxs-lookup"><span data-stu-id="c3fdc-117">Choose the Ruby from the Built-in Runtime stacks.</span></span>

<span data-ttu-id="c3fdc-118">Une fois votre application web Ruby créée, vous pouvez la déployer à l’aide de Git ou FTP.</span><span class="sxs-lookup"><span data-stu-id="c3fdc-118">After your Ruby web app gets created, you can deploy to it using Git or FTP.</span></span>

<span data-ttu-id="c3fdc-119">Pour plus d’informations sur la création d’une application Ruby, consultez le [guide de prise en main](app-service-linux-ruby-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="c3fdc-119">To learn more about creating a Ruby app, check the [get started guide](app-service-linux-ruby-get-started.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="c3fdc-120">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c3fdc-120">Next steps</span></span>
* [<span data-ttu-id="c3fdc-121">Qu’est-ce que Web App sur Linux ?</span><span class="sxs-lookup"><span data-stu-id="c3fdc-121">What is Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="c3fdc-122">Déploiement Git local vers Azure App Service</span><span class="sxs-lookup"><span data-stu-id="c3fdc-122">Local Git Deployment to Azure App Service</span></span>](app-service-deploy-local-git.md)
* [<span data-ttu-id="c3fdc-123">FAQ de l’application web Azure App Service sur Linux</span><span class="sxs-lookup"><span data-stu-id="c3fdc-123">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)
* [<span data-ttu-id="c3fdc-124">Créer une application Ruby avec Azure Web App sur Linux</span><span class="sxs-lookup"><span data-stu-id="c3fdc-124">Create a Ruby App with Azure Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)

<!--Image references-->
[1]: ./media/app-service-linux-using-ruby/New-Linux.png
[2]: ./media/app-service-linux-using-ruby/Ruby-UX.png