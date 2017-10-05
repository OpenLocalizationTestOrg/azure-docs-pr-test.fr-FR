---
title: "Déployer une application web Umbraco dans le portail Azure en cinq minutes | Microsoft Docs"
description: "Découvrez la facilité avec laquelle vous pouvez exécuter des applications web dans App Service en déployant un exemple d’application ASP.NET. Consultez immédiatement les résultats."
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
ms.openlocfilehash: 9e3e2130a66cdfe5f06eb3b366e53028c44e7e6a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-an-umbraco-web-app-in-the-azure-portal-in-five-minutes"></a><span data-ttu-id="f2ceb-104">Déployer une application web Umbraco dans le portail Azure en cinq minutes</span><span class="sxs-lookup"><span data-stu-id="f2ceb-104">Deploy an Umbraco web app in the Azure portal in five minutes</span></span>

<span data-ttu-id="f2ceb-105">Dans ce didacticiel, vous découvrirez comment déployer une application web [Umbraco](https://our.umbraco.org/) dans [Azure App Service](../app-service/app-service-value-prop-what-is.md) en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="f2ceb-105">This tutorial helps you deploy n [Umbraco](https://our.umbraco.org/) web app to [Azure App Service](../app-service/app-service-value-prop-what-is.md) in minutes.</span></span>

![Application Umbraco](./media/app-service-web-get-started-dotnet-portal/defaultpage.png)

## <a name="prerequisites"></a><span data-ttu-id="f2ceb-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="f2ceb-107">Prerequisites</span></span>
<span data-ttu-id="f2ceb-108">Vous devez avoir un compte Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="f2ceb-108">You need a Microsoft Azure account.</span></span> <span data-ttu-id="f2ceb-109">Si vous n’avez pas de compte, vous pouvez [vous inscrire pour un essai gratuit](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) ou [activer les avantages de votre abonnement Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="f2ceb-109">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>

> [!NOTE]
> <span data-ttu-id="f2ceb-110">Vous pouvez [essayer App Service](https://azure.microsoft.com/try/app-service/) sans compte Azure.</span><span class="sxs-lookup"><span data-stu-id="f2ceb-110">You can [Try App Service](https://azure.microsoft.com/try/app-service/) without an Azure account.</span></span> <span data-ttu-id="f2ceb-111">Créez une application de base et expérimentez-la pendant une heure, sans carte de paiement et sans engagement.</span><span class="sxs-lookup"><span data-stu-id="f2ceb-111">Create a starter app and play with it for up to an hour--no credit card required, no commitments.</span></span>
> 
> 

## <a name="deploy-the-aspnet-app"></a><span data-ttu-id="f2ceb-112">Déployer l’application ASP.NET</span><span class="sxs-lookup"><span data-stu-id="f2ceb-112">Deploy the ASP.NET app</span></span>
1. <span data-ttu-id="f2ceb-113">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f2ceb-113">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="f2ceb-114">Ouvrez [https://portal.azure.com/#create/umbracoorg.UmbracoCMS](https://portal.azure.com/#create/umbracoorg.UmbracoCMS).</span><span class="sxs-lookup"><span data-stu-id="f2ceb-114">Open [https://portal.azure.com/#create/umbracoorg.UmbracoCMS](https://portal.azure.com/#create/umbracoorg.UmbracoCMS).</span></span>

    <span data-ttu-id="f2ceb-115">Ce lien est un raccourci permettant de configurer immédiatement une application Umbraco dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="f2ceb-115">This link is a shortcut to immediately configure a new Umbraco app in the Azure portal.</span></span>

3. <span data-ttu-id="f2ceb-116">Sous **Nom de l’application**, entrez un nom d’application web.</span><span class="sxs-lookup"><span data-stu-id="f2ceb-116">In **App name**, type a web app name.</span></span> <span data-ttu-id="f2ceb-117">Si le nom est unique dans le domaine `azurewebsites.net`, une coche verte s’affiche dans la case.</span><span class="sxs-lookup"><span data-stu-id="f2ceb-117">You will see a green checkmark in the box if the name is unique in the `azurewebsites.net` domain.</span></span>
   
5. <span data-ttu-id="f2ceb-118">Sous **Groupe de ressources**, cliquez sur **Créer** pour créer un nouveau [groupe de ressources](../azure-resource-manager/resource-group-overview.md), puis donnez-lui un nom.</span><span class="sxs-lookup"><span data-stu-id="f2ceb-118">In **Resource Group**, click **Create new** to create a new [resource group](../azure-resource-manager/resource-group-overview.md), then give it a name.</span></span>

7. <span data-ttu-id="f2ceb-119">Cliquez sur **Plan App Service/Emplacement** > **Créer**.</span><span class="sxs-lookup"><span data-stu-id="f2ceb-119">Click **App Service plan/Location** > **Create New**.</span></span> <span data-ttu-id="f2ceb-120">Configurez le [plan App Service](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) comme indiqué :</span><span class="sxs-lookup"><span data-stu-id="f2ceb-120">Configure the [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) as shown:</span></span>

    - <span data-ttu-id="f2ceb-121">Sous **Plan App Service**, entrez le nom souhaité.</span><span class="sxs-lookup"><span data-stu-id="f2ceb-121">In **App Service plan**, type the desired name.</span></span>
    - <span data-ttu-id="f2ceb-122">Sous **Emplacement**, choisissez un emplacement pour héberger votre plan.</span><span class="sxs-lookup"><span data-stu-id="f2ceb-122">In **Location**, choose a location to host your plan.</span></span>
    - <span data-ttu-id="f2ceb-123">Cliquez sur **Niveau de tarification**, puis sélectionnez **F1 gratuit** ou un autre niveau qui vous convient, puis cliquez sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="f2ceb-123">Click **Pricing tier**, then select **F1 Free** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="f2ceb-124">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="f2ceb-124">Click **OK**.</span></span>

    <span data-ttu-id="f2ceb-125">Votre configuration Umbraco CMS doit maintenant ressembler à la capture d’écran suivante :</span><span class="sxs-lookup"><span data-stu-id="f2ceb-125">Your Umbraco CMS configuration should now look like the following screenshot:</span></span>

    ![Configuration en cours - première configuration Umbraco dans Azure App Service](./media/app-service-web-get-started-dotnet-portal/configure-in-progress.png)

12. <span data-ttu-id="f2ceb-127">Cliquez sur **SQL Database** > **Créer une base de données**.</span><span class="sxs-lookup"><span data-stu-id="f2ceb-127">Click **SQL Database** > **Create a new database**.</span></span> <span data-ttu-id="f2ceb-128">Configurez la base de données SQL comme indiqué :</span><span class="sxs-lookup"><span data-stu-id="f2ceb-128">Configure the SQL Database as shown:</span></span>

    - <span data-ttu-id="f2ceb-129">Sous **Nom**, entrez un nom, tel que **myDB**.</span><span class="sxs-lookup"><span data-stu-id="f2ceb-129">In **Name**, type a name, such as **myDB**.</span></span>
    - <span data-ttu-id="f2ceb-130">Cliquez sur **Niveau de tarification**, puis sélectionnez **F gratuit** ou un autre niveau qui vous convient, puis cliquez sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="f2ceb-130">Click **Pricing tier**, then select **F Free** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="f2ceb-131">Cliquez sur **Serveur cible** > **Créer un serveur**.</span><span class="sxs-lookup"><span data-stu-id="f2ceb-131">Click **Target server** > **Create a new server**.</span></span> <span data-ttu-id="f2ceb-132">Configurez le serveur de base de données comme indiqué :</span><span class="sxs-lookup"><span data-stu-id="f2ceb-132">Configure the database server as shown:</span></span>

        - <span data-ttu-id="f2ceb-133">Sous **Nom du serveur**, entrez un nom pour le serveur.</span><span class="sxs-lookup"><span data-stu-id="f2ceb-133">In **Server name**, type a server name.</span></span> <span data-ttu-id="f2ceb-134">Si le nom est unique dans le domaine `.database.windows.net`, une coche verte s’affiche dans la case.</span><span class="sxs-lookup"><span data-stu-id="f2ceb-134">You will see a green checkmark in the box if the name is unique in the `.database.windows.net` domain.</span></span>
        - <span data-ttu-id="f2ceb-135">Dans **Connexion d’administrateur serveur**, entrez le nom d’utilisateur administrateur de votre choix.</span><span class="sxs-lookup"><span data-stu-id="f2ceb-135">In **Server admin login**, type the desired admininistrator username.</span></span>
        - <span data-ttu-id="f2ceb-136">Sous **Mot de passe** et **Confirmer le mot de passe**, entrez le mot de passe de votre choix.</span><span class="sxs-lookup"><span data-stu-id="f2ceb-136">In **Password** and **Confirm password**, type the desired password.</span></span>
        - <span data-ttu-id="f2ceb-137">Sous Emplacement, sélectionnez le même emplacement que celui utilisé pour l’application web.</span><span class="sxs-lookup"><span data-stu-id="f2ceb-137">In Location, select the same location you use for the web app.</span></span>
        - <span data-ttu-id="f2ceb-138">Vérifiez que l’option **Autoriser les services Azure à accéder au serveur** est sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="f2ceb-138">Make sure **Allow azure services to access server** is selected.</span></span>
        - <span data-ttu-id="f2ceb-139">Cliquez sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="f2ceb-139">Click **Select**.</span></span>
    
    - <span data-ttu-id="f2ceb-140">Cliquez sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="f2ceb-140">Click **Select**.</span></span>

13. <span data-ttu-id="f2ceb-141">Cliquez sur **Paramètres de l’application Web**, spécifiez le nom et le mot de passe utilisateur de la base de données, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="f2ceb-141">Click **Web app settings**, specify the database username and password, and click **OK**.</span></span>

    <span data-ttu-id="f2ceb-142">Votre configuration Umbraco CMS doit maintenant ressembler à la capture d’écran suivante :</span><span class="sxs-lookup"><span data-stu-id="f2ceb-142">Your Umbraco CMS configuration should now look like the following screenshot:</span></span>

    ![Configuration terminée - première configuration Umbraco dans Azure App Service](./media/app-service-web-get-started-dotnet-portal/configure-complete.png)

14. <span data-ttu-id="f2ceb-144">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="f2ceb-144">Click **Create**.</span></span>
    
    <span data-ttu-id="f2ceb-145">À présent, Azure crée votre application Umbraco en fonction de votre configuration.</span><span class="sxs-lookup"><span data-stu-id="f2ceb-145">Azure now creates your Umbraco app based on your configuration.</span></span> <span data-ttu-id="f2ceb-146">Vous devriez voir le message **Le déploiement a commencé**.</span><span class="sxs-lookup"><span data-stu-id="f2ceb-146">You should see a **Deployment started...** notification.</span></span>

    ![Déploiement réussi - première configuration Umbraco dans Azure App Service](./media/app-service-web-get-started-dotnet-portal/deployment-started.png)
   
## <a name="launch-and-manage-your-umrbaco-web-app"></a><span data-ttu-id="f2ceb-148">Lancer et gérer votre application web Umbraco</span><span class="sxs-lookup"><span data-stu-id="f2ceb-148">Launch and manage your Umrbaco web app</span></span>

<span data-ttu-id="f2ceb-149">Une autre notification s’affiche quand Azure termine le déploiement de l’application.</span><span class="sxs-lookup"><span data-stu-id="f2ceb-149">When Azure completes app deployment you see another notification.</span></span>

![Déploiement réussi - première configuration Umbraco dans Azure App Service](./media/app-service-web-get-started-dotnet-portal/deployment-succeeded.png)

1. <span data-ttu-id="f2ceb-151">Cliquez sur la notification.</span><span class="sxs-lookup"><span data-stu-id="f2ceb-151">Click the notification.</span></span> <span data-ttu-id="f2ceb-152">Si vous l’avez manqué, vous pouvez toujours y accéder en cliquant sur la cloche de notification (![Cloche de notification - première configuration Umbraco dans Azure App Service](./media/app-service-web-get-started-dotnet-portal/notification.png)).</span><span class="sxs-lookup"><span data-stu-id="f2ceb-152">If you missed it, you can always access it by clicking the notification bell (![Notification bellow - first Umbraco in Azure App Service](./media/app-service-web-get-started-dotnet-portal/notification.png)).</span></span>

    <span data-ttu-id="f2ceb-153">Vous devriez maintenant voir le [panneau](../azure-resource-manager/resource-group-portal.md#manage-resources) de gestion de votre application web (*panneau* : page de portail qui s’ouvre horizontalement).</span><span class="sxs-lookup"><span data-stu-id="f2ceb-153">You should now see your web app's management [blade](../azure-resource-manager/resource-group-portal.md#manage-resources) (*blade*: a portal page that opens horizontally).</span></span>

3. <span data-ttu-id="f2ceb-154">Dans la partie supérieure de la page Vue d’ensemble, cliquez sur **Parcourir**.</span><span class="sxs-lookup"><span data-stu-id="f2ceb-154">In the top of the Overview page, click **Browse**.</span></span>
   
    ![Parcourir - première configuration Umbraco dans Azure App Service](./media/app-service-web-get-started-dotnet-portal/browse.png)

    <span data-ttu-id="f2ceb-156">À présent, la page **Bienvenue** d’Umbraco s’affiche.</span><span class="sxs-lookup"><span data-stu-id="f2ceb-156">Now you see the Umbraco **Welcome** page.</span></span> <span data-ttu-id="f2ceb-157">Configurez l’installation d’Umbraco et commencez à l’utiliser !</span><span class="sxs-lookup"><span data-stu-id="f2ceb-157">Configure the Umbraco installation and start playing with it!</span></span>

    ![Configuration Umbraco - première configuration Umbraco dans Azure App Service](./media/app-service-web-get-started-dotnet-portal/umbraco-config.png)
    
## <a name="next-steps"></a><span data-ttu-id="f2ceb-159">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f2ceb-159">Next steps</span></span>
* <span data-ttu-id="f2ceb-160">[Déployer une application web ASP.NET dans Azure App Service, à l’aide de Visual Studio](app-service-web-get-started-dotnet.md) - Apprenez à créer une application web Azure dans Visual Studio, à l’aide de l’un des modèles d’application inclus.</span><span class="sxs-lookup"><span data-stu-id="f2ceb-160">[Deploy an ASP.NET web app to Azure App Service, using Visual Studio](app-service-web-get-started-dotnet.md) - Learn how to create a new Azure web app from Visual Studio, using any one of the included application templates.</span></span>
* <span data-ttu-id="f2ceb-161">[Déployer votre code dans Azure App Service](web-sites-deploy.md) - Apprenez à déployer à partir de FTP ou de référentiels de contrôle source.</span><span class="sxs-lookup"><span data-stu-id="f2ceb-161">[Deploy your code to Azure App Service](web-sites-deploy.md)- Learn how to deploy from FTP or from source control repositories.</span></span>
* <span data-ttu-id="f2ceb-162">[Ajouter des fonctionnalités à votre première application web](app-service-web-get-started-2.md) - Faites passer votre application Azure à la vitesse supérieure.</span><span class="sxs-lookup"><span data-stu-id="f2ceb-162">[Add functionality to your first web app](app-service-web-get-started-2.md) - Take your Azure app to the next level.</span></span> <span data-ttu-id="f2ceb-163">Authentifiez vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="f2ceb-163">Authenticate your users.</span></span> <span data-ttu-id="f2ceb-164">Faites évoluer sa capacité en fonction de la demande.</span><span class="sxs-lookup"><span data-stu-id="f2ceb-164">Scale it based on demand.</span></span> <span data-ttu-id="f2ceb-165">Configurez des alertes de performance.</span><span class="sxs-lookup"><span data-stu-id="f2ceb-165">Set up some performance alerts.</span></span> <span data-ttu-id="f2ceb-166">Tout cela en seulement quelques clics.</span><span class="sxs-lookup"><span data-stu-id="f2ceb-166">All with a few clicks.</span></span>
