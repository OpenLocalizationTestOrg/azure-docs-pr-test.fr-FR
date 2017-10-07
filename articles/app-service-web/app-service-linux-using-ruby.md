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
# <a name="using-ruby-in-web-app-on-linux"></a><span data-ttu-id="c9f37-104">Utilisation de Ruby dans Web App sur Linux</span><span class="sxs-lookup"><span data-stu-id="c9f37-104">Using Ruby in Web App on Linux</span></span> #

<span data-ttu-id="c9f37-105">Avec la dernière mise à jour tooour principal de hello, nous avons introduit la prise en charge de v.2.3 Ruby.</span><span class="sxs-lookup"><span data-stu-id="c9f37-105">With hello latest update tooour backend, we introduced support for Ruby v.2.3.</span></span> <span data-ttu-id="c9f37-106">En définissant la configuration hello de votre application web de Linux, vous pouvez modifier la pile de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="c9f37-106">By setting hello configuration of your Linux web app, you can change hello application stack.</span></span>

## <a name="using-hello-azure-portal"></a><span data-ttu-id="c9f37-107">À l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="c9f37-107">Using hello Azure portal</span></span> ##

<span data-ttu-id="c9f37-108">À partir du menu Nouveau hello hello [portail Azure](https://portal.azure.com), vous pouvez choisir toocreate une application Web sur Linux à partir de hello Web + option Mobile comme indiqué dans hello suivant image :</span><span class="sxs-lookup"><span data-stu-id="c9f37-108">From hello new menu in hello [Azure portal](https://portal.azure.com), you can choose toocreate a Web App on Linux from hello Web + Mobile option as shown in hello following image:</span></span>

![Démarrer la création d’une application web sur hello portail Azure][1]

<span data-ttu-id="c9f37-110">Ensuite, hello **créer panneau** s’ouvre comme indiqué dans hello suivant image :</span><span class="sxs-lookup"><span data-stu-id="c9f37-110">Next, hello **Create blade** opens as shown in hello following image:</span></span>

![Panneau de création de Hello][2]

1. <span data-ttu-id="c9f37-112">Donnez un nom à votre application web.</span><span class="sxs-lookup"><span data-stu-id="c9f37-112">Give your web app a name.</span></span>
2. <span data-ttu-id="c9f37-113">Sélectionnez un groupe de ressources existant ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="c9f37-113">Choose an existing resource group or create a new one.</span></span> <span data-ttu-id="c9f37-114">(Consultez les régions disponibles Bonjour [section limitations](app-service-linux-intro.md).)</span><span class="sxs-lookup"><span data-stu-id="c9f37-114">(See available regions in hello [limitations section](app-service-linux-intro.md).)</span></span>
3. <span data-ttu-id="c9f37-115">Sélectionnez un plan Azure App Service existant ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="c9f37-115">Choose an existing Azure App Service plan or create a new one.</span></span> <span data-ttu-id="c9f37-116">(Consultez les remarques du plan App Service Bonjour [section limitations](app-service-linux-intro.md).)</span><span class="sxs-lookup"><span data-stu-id="c9f37-116">(See App Service plan notes in hello [limitations section](app-service-linux-intro.md).)</span></span>
4. <span data-ttu-id="c9f37-117">Choisissez hello Ruby des piles de Runtime intégrées hello.</span><span class="sxs-lookup"><span data-stu-id="c9f37-117">Choose hello Ruby from hello Built-in Runtime stacks.</span></span>

<span data-ttu-id="c9f37-118">Une fois que votre application web Ruby est créée, vous pouvez déployer tooit à l’aide de Git ou FTP.</span><span class="sxs-lookup"><span data-stu-id="c9f37-118">After your Ruby web app gets created, you can deploy tooit using Git or FTP.</span></span>

<span data-ttu-id="c9f37-119">toolearn en savoir plus sur la création d’une application Ruby, vérifiez hello [guide pas à pas de get](app-service-linux-ruby-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="c9f37-119">toolearn more about creating a Ruby app, check hello [get started guide](app-service-linux-ruby-get-started.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="c9f37-120">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c9f37-120">Next steps</span></span>
* [<span data-ttu-id="c9f37-121">Qu’est-ce que Web App sur Linux ?</span><span class="sxs-lookup"><span data-stu-id="c9f37-121">What is Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="c9f37-122">TooAzure déploiement Git local du Service d’applications</span><span class="sxs-lookup"><span data-stu-id="c9f37-122">Local Git Deployment tooAzure App Service</span></span>](app-service-deploy-local-git.md)
* [<span data-ttu-id="c9f37-123">FAQ de l’application web Azure App Service sur Linux</span><span class="sxs-lookup"><span data-stu-id="c9f37-123">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)
* [<span data-ttu-id="c9f37-124">Créer une application Ruby avec Azure Web App sur Linux</span><span class="sxs-lookup"><span data-stu-id="c9f37-124">Create a Ruby App with Azure Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)

<!--Image references-->
[1]: ./media/app-service-linux-using-ruby/New-Linux.png
[2]: ./media/app-service-linux-using-ruby/Ruby-UX.png