---
title: aaaDeploy une application web de Umbraco Bonjour Azure portal dans les cinq minutes | Documents Microsoft
description: "Découvrir combien il est facile toorun les applications web dans le Service d’applications en déployant un exemple d’application ASP.NET. Consultez immédiatement les résultats."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: b1e6bd58-48d1-4007-9d6c-53fd6db061e3
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/10/2017
ms.author: cephalin
ms.openlocfilehash: 6da45f99b3043a3684e3d99c14e6443d597b5212
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-umbraco-web-app-in-hello-azure-portal-in-five-minutes"></a><span data-ttu-id="6fb2d-104">Déployer une application web de Umbraco Bonjour Azure portal dans les cinq minutes</span><span class="sxs-lookup"><span data-stu-id="6fb2d-104">Deploy an Umbraco web app in hello Azure portal in five minutes</span></span>

<span data-ttu-id="6fb2d-105">Ce didacticiel vous aide à déployer n [Umbraco](https://our.umbraco.org/) web application trop[Azure App Service](../app-service/app-service-value-prop-what-is.md) en minutes.</span><span class="sxs-lookup"><span data-stu-id="6fb2d-105">This tutorial helps you deploy n [Umbraco](https://our.umbraco.org/) web app too[Azure App Service](../app-service/app-service-value-prop-what-is.md) in minutes.</span></span>

![Application Umbraco](./media/app-service-web-get-started-dotnet-portal/defaultpage.png)

## <a name="prerequisites"></a><span data-ttu-id="6fb2d-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="6fb2d-107">Prerequisites</span></span>
<span data-ttu-id="6fb2d-108">Vous devez avoir un compte Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="6fb2d-108">You need a Microsoft Azure account.</span></span> <span data-ttu-id="6fb2d-109">Si vous n’avez pas de compte, vous pouvez [vous inscrire pour un essai gratuit](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) ou [activer les avantages de votre abonnement Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="6fb2d-109">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>

> [!NOTE]
> <span data-ttu-id="6fb2d-110">Vous pouvez [essayer App Service](https://azure.microsoft.com/try/app-service/) sans compte Azure.</span><span class="sxs-lookup"><span data-stu-id="6fb2d-110">You can [Try App Service](https://azure.microsoft.com/try/app-service/) without an Azure account.</span></span> <span data-ttu-id="6fb2d-111">Créer une application de démarrage et de le manipuler pour les horaires de tooan--aucune carte de crédit requis, aucune des engagements.</span><span class="sxs-lookup"><span data-stu-id="6fb2d-111">Create a starter app and play with it for up tooan hour--no credit card required, no commitments.</span></span>
> 
> 

## <a name="deploy-hello-aspnet-app"></a><span data-ttu-id="6fb2d-112">Déploiement d’une application ASP.NET de hello</span><span class="sxs-lookup"><span data-stu-id="6fb2d-112">Deploy hello ASP.NET app</span></span>
1. <span data-ttu-id="6fb2d-113">Connectez-vous à toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6fb2d-113">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="6fb2d-114">Ouvrez [https://portal.azure.com/#create/umbracoorg.UmbracoCMS](https://portal.azure.com/#create/umbracoorg.UmbracoCMS).</span><span class="sxs-lookup"><span data-stu-id="6fb2d-114">Open [https://portal.azure.com/#create/umbracoorg.UmbracoCMS](https://portal.azure.com/#create/umbracoorg.UmbracoCMS).</span></span>

    <span data-ttu-id="6fb2d-115">Ce lien est un raccourci tooimmediately configurer une nouvelle application Umbraco Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="6fb2d-115">This link is a shortcut tooimmediately configure a new Umbraco app in hello Azure portal.</span></span>

3. <span data-ttu-id="6fb2d-116">Sous **Nom de l’application**, entrez un nom d’application web.</span><span class="sxs-lookup"><span data-stu-id="6fb2d-116">In **App name**, type a web app name.</span></span> <span data-ttu-id="6fb2d-117">Vous verrez une coche verte dans la zone de hello si le nom de hello est unique dans hello `azurewebsites.net` domaine.</span><span class="sxs-lookup"><span data-stu-id="6fb2d-117">You will see a green checkmark in hello box if hello name is unique in hello `azurewebsites.net` domain.</span></span>
   
5. <span data-ttu-id="6fb2d-118">Dans **groupe de ressources**, cliquez sur **nouvel** toocreate une nouvelle [groupe de ressources](../azure-resource-manager/resource-group-overview.md), puis attribuez-lui un nom.</span><span class="sxs-lookup"><span data-stu-id="6fb2d-118">In **Resource Group**, click **Create new** toocreate a new [resource group](../azure-resource-manager/resource-group-overview.md), then give it a name.</span></span>

7. <span data-ttu-id="6fb2d-119">Cliquez sur **Plan App Service/Emplacement** > **Créer**.</span><span class="sxs-lookup"><span data-stu-id="6fb2d-119">Click **App Service plan/Location** > **Create New**.</span></span> <span data-ttu-id="6fb2d-120">Configurer hello [plan App Service](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) comme indiqué :</span><span class="sxs-lookup"><span data-stu-id="6fb2d-120">Configure hello [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) as shown:</span></span>

    - <span data-ttu-id="6fb2d-121">Dans **plan App Service**, nom de type hello souhaité.</span><span class="sxs-lookup"><span data-stu-id="6fb2d-121">In **App Service plan**, type hello desired name.</span></span>
    - <span data-ttu-id="6fb2d-122">Dans **emplacement**, choisissez un emplacement toohost votre plan.</span><span class="sxs-lookup"><span data-stu-id="6fb2d-122">In **Location**, choose a location toohost your plan.</span></span>
    - <span data-ttu-id="6fb2d-123">Cliquez sur **Niveau de tarification**, puis sélectionnez **F1 gratuit** ou un autre niveau qui vous convient, puis cliquez sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="6fb2d-123">Click **Pricing tier**, then select **F1 Free** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="6fb2d-124">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="6fb2d-124">Click **OK**.</span></span>

    <span data-ttu-id="6fb2d-125">Votre configuration Umbraco CMS doit maintenant ressembler à hello suivant capture d’écran :</span><span class="sxs-lookup"><span data-stu-id="6fb2d-125">Your Umbraco CMS configuration should now look like hello following screenshot:</span></span>

    ![Configuration en cours - première configuration Umbraco dans Azure App Service](./media/app-service-web-get-started-dotnet-portal/configure-in-progress.png)

12. <span data-ttu-id="6fb2d-127">Cliquez sur **SQL Database** > **Créer une base de données**.</span><span class="sxs-lookup"><span data-stu-id="6fb2d-127">Click **SQL Database** > **Create a new database**.</span></span> <span data-ttu-id="6fb2d-128">Configurer hello de base de données SQL comme indiqué :</span><span class="sxs-lookup"><span data-stu-id="6fb2d-128">Configure hello SQL Database as shown:</span></span>

    - <span data-ttu-id="6fb2d-129">Sous **Nom**, entrez un nom, tel que **myDB**.</span><span class="sxs-lookup"><span data-stu-id="6fb2d-129">In **Name**, type a name, such as **myDB**.</span></span>
    - <span data-ttu-id="6fb2d-130">Cliquez sur **Niveau de tarification**, puis sélectionnez **F gratuit** ou un autre niveau qui vous convient, puis cliquez sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="6fb2d-130">Click **Pricing tier**, then select **F Free** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="6fb2d-131">Cliquez sur **Serveur cible** > **Créer un serveur**.</span><span class="sxs-lookup"><span data-stu-id="6fb2d-131">Click **Target server** > **Create a new server**.</span></span> <span data-ttu-id="6fb2d-132">Configurer le serveur de base de données hello comme indiqué :</span><span class="sxs-lookup"><span data-stu-id="6fb2d-132">Configure hello database server as shown:</span></span>

        - <span data-ttu-id="6fb2d-133">Sous **Nom du serveur**, entrez un nom pour le serveur.</span><span class="sxs-lookup"><span data-stu-id="6fb2d-133">In **Server name**, type a server name.</span></span> <span data-ttu-id="6fb2d-134">Vous verrez une coche verte dans la zone de hello si le nom de hello est unique dans hello `.database.windows.net` domaine.</span><span class="sxs-lookup"><span data-stu-id="6fb2d-134">You will see a green checkmark in hello box if hello name is unique in hello `.database.windows.net` domain.</span></span>
        - <span data-ttu-id="6fb2d-135">Dans **ouverture de session de serveur admin**, vous le souhaitez hello de type nom d’utilisateur administrateur.</span><span class="sxs-lookup"><span data-stu-id="6fb2d-135">In **Server admin login**, type hello desired admininistrator username.</span></span>
        - <span data-ttu-id="6fb2d-136">Dans **mot de passe** et **confirmer le mot de passe**, mot de passe de type hello souhaité.</span><span class="sxs-lookup"><span data-stu-id="6fb2d-136">In **Password** and **Confirm password**, type hello desired password.</span></span>
        - <span data-ttu-id="6fb2d-137">Dans l’emplacement, sélectionnez hello même emplacement que vous utilisez pour l’application web de hello.</span><span class="sxs-lookup"><span data-stu-id="6fb2d-137">In Location, select hello same location you use for hello web app.</span></span>
        - <span data-ttu-id="6fb2d-138">Assurez-vous que **server d’Autoriser les services azure tooaccess** est sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="6fb2d-138">Make sure **Allow azure services tooaccess server** is selected.</span></span>
        - <span data-ttu-id="6fb2d-139">Cliquez sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="6fb2d-139">Click **Select**.</span></span>
    
    - <span data-ttu-id="6fb2d-140">Cliquez sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="6fb2d-140">Click **Select**.</span></span>

13. <span data-ttu-id="6fb2d-141">Cliquez sur **paramètres de l’application Web**, spécifiez le nom d’utilisateur de base de données hello et le mot de passe, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="6fb2d-141">Click **Web app settings**, specify hello database username and password, and click **OK**.</span></span>

    <span data-ttu-id="6fb2d-142">Votre configuration Umbraco CMS doit maintenant ressembler à hello suivant capture d’écran :</span><span class="sxs-lookup"><span data-stu-id="6fb2d-142">Your Umbraco CMS configuration should now look like hello following screenshot:</span></span>

    ![Configuration terminée - première configuration Umbraco dans Azure App Service](./media/app-service-web-get-started-dotnet-portal/configure-complete.png)

14. <span data-ttu-id="6fb2d-144">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="6fb2d-144">Click **Create**.</span></span>
    
    <span data-ttu-id="6fb2d-145">À présent, Azure crée votre application Umbraco en fonction de votre configuration.</span><span class="sxs-lookup"><span data-stu-id="6fb2d-145">Azure now creates your Umbraco app based on your configuration.</span></span> <span data-ttu-id="6fb2d-146">Vous devriez voir le message **Le déploiement a commencé**.</span><span class="sxs-lookup"><span data-stu-id="6fb2d-146">You should see a **Deployment started...** notification.</span></span>

    ![Déploiement réussi - première configuration Umbraco dans Azure App Service](./media/app-service-web-get-started-dotnet-portal/deployment-started.png)
   
## <a name="launch-and-manage-your-umrbaco-web-app"></a><span data-ttu-id="6fb2d-148">Lancer et gérer votre application web Umbraco</span><span class="sxs-lookup"><span data-stu-id="6fb2d-148">Launch and manage your Umrbaco web app</span></span>

<span data-ttu-id="6fb2d-149">Une autre notification s’affiche quand Azure termine le déploiement de l’application.</span><span class="sxs-lookup"><span data-stu-id="6fb2d-149">When Azure completes app deployment you see another notification.</span></span>

![Déploiement réussi - première configuration Umbraco dans Azure App Service](./media/app-service-web-get-started-dotnet-portal/deployment-succeeded.png)

1. <span data-ttu-id="6fb2d-151">Cliquez sur hello notification.</span><span class="sxs-lookup"><span data-stu-id="6fb2d-151">Click hello notification.</span></span> <span data-ttu-id="6fb2d-152">Si vous l’avez manqué, vous pouvez toujours y accéder en cliquant sur la cloche de notification hello (![ctiver Notification - première Umbraco dans Azure App Service](./media/app-service-web-get-started-dotnet-portal/notification.png)).</span><span class="sxs-lookup"><span data-stu-id="6fb2d-152">If you missed it, you can always access it by clicking hello notification bell (![Notification bellow - first Umbraco in Azure App Service](./media/app-service-web-get-started-dotnet-portal/notification.png)).</span></span>

    <span data-ttu-id="6fb2d-153">Vous devriez maintenant voir le [panneau](../azure-resource-manager/resource-group-portal.md#manage-resources) de gestion de votre application web (*panneau* : page de portail qui s’ouvre horizontalement).</span><span class="sxs-lookup"><span data-stu-id="6fb2d-153">You should now see your web app's management [blade](../azure-resource-manager/resource-group-portal.md#manage-resources) (*blade*: a portal page that opens horizontally).</span></span>

3. <span data-ttu-id="6fb2d-154">Dans hello en haut de page de vue d’ensemble de hello, cliquez sur **Parcourir**.</span><span class="sxs-lookup"><span data-stu-id="6fb2d-154">In hello top of hello Overview page, click **Browse**.</span></span>
   
    ![Parcourir - première configuration Umbraco dans Azure App Service](./media/app-service-web-get-started-dotnet-portal/browse.png)

    <span data-ttu-id="6fb2d-156">Maintenant vous voyez hello Umbraco **Bienvenue** page.</span><span class="sxs-lookup"><span data-stu-id="6fb2d-156">Now you see hello Umbraco **Welcome** page.</span></span> <span data-ttu-id="6fb2d-157">Configurer l’installation d’Umbraco hello et commencez la lecture avec lui.</span><span class="sxs-lookup"><span data-stu-id="6fb2d-157">Configure hello Umbraco installation and start playing with it!</span></span>

    ![Configuration Umbraco - première configuration Umbraco dans Azure App Service](./media/app-service-web-get-started-dotnet-portal/umbraco-config.png)
    
## <a name="next-steps"></a><span data-ttu-id="6fb2d-159">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6fb2d-159">Next steps</span></span>
* <span data-ttu-id="6fb2d-160">[Déployer un tooAzure d’application ASP.NET web Service d’application, à l’aide de Visual Studio](app-service-web-get-started-dotnet.md) -Découvrez comment toocreate une nouvelle application web Azure à partir de Visual Studio, à l’aide de l’une des hello inclus les modèles d’application.</span><span class="sxs-lookup"><span data-stu-id="6fb2d-160">[Deploy an ASP.NET web app tooAzure App Service, using Visual Studio](app-service-web-get-started-dotnet.md) - Learn how toocreate a new Azure web app from Visual Studio, using any one of hello included application templates.</span></span>
* <span data-ttu-id="6fb2d-161">[Déployer votre tooAzure de code du Service d’applications](web-sites-deploy.md)-Découvrez comment toodeploy à partir de FTP ou à partir de la source de contrôler les référentiels.</span><span class="sxs-lookup"><span data-stu-id="6fb2d-161">[Deploy your code tooAzure App Service](web-sites-deploy.md)- Learn how toodeploy from FTP or from source control repositories.</span></span>
* <span data-ttu-id="6fb2d-162">[Ajouter des fonctionnalités tooyour première application web](app-service-web-get-started-2.md) -se toohello de votre application Azure ensuite au niveau.</span><span class="sxs-lookup"><span data-stu-id="6fb2d-162">[Add functionality tooyour first web app](app-service-web-get-started-2.md) - Take your Azure app toohello next level.</span></span> <span data-ttu-id="6fb2d-163">Authentifiez vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="6fb2d-163">Authenticate your users.</span></span> <span data-ttu-id="6fb2d-164">Faites évoluer sa capacité en fonction de la demande.</span><span class="sxs-lookup"><span data-stu-id="6fb2d-164">Scale it based on demand.</span></span> <span data-ttu-id="6fb2d-165">Configurez des alertes de performance.</span><span class="sxs-lookup"><span data-stu-id="6fb2d-165">Set up some performance alerts.</span></span> <span data-ttu-id="6fb2d-166">Tout cela en seulement quelques clics.</span><span class="sxs-lookup"><span data-stu-id="6fb2d-166">All with a few clicks.</span></span>
