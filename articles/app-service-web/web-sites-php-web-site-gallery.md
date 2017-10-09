---
title: aaaCreate une application web de WordPress dans Azure App Service | Documents Microsoft
description: "Découvrez comment toocreate un nouvel Azure web app pour un blog WordPress à l’aide de hello portail Azure."
services: app-service\web
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 193ae094-0d7c-4749-a09b-ff4b1240149e
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 3a95fcb6732c15a8200921ce474b6dde2298dec3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-wordpress-web-app-in-azure-app-service"></a><span data-ttu-id="d8e8f-103">Créer une application web WordPress dans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="d8e8f-103">Create a WordPress web app in Azure App Service</span></span>
[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

<span data-ttu-id="d8e8f-104">Ce didacticiel montre comment toodeploy un blog WordPress de site à partir de hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="d8e8f-104">This tutorial shows how toodeploy a WordPress blog site from hello Azure Marketplace.</span></span>

<span data-ttu-id="d8e8f-105">Lorsque vous avez terminé le didacticiel de hello vous avez votre propre site blog WordPress et en cours d’exécution dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="d8e8f-105">When you're done with hello tutorial you'll have your own WordPress blog site up and running in hello cloud.</span></span>

![Site WordPress](./media/web-sites-php-web-site-gallery/wpdashboard.png)

<span data-ttu-id="d8e8f-107">Vous apprendrez ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="d8e8f-107">You'll learn:</span></span>

* <span data-ttu-id="d8e8f-108">Comment toofind un modèle d’application Bonjour Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="d8e8f-108">How toofind an application template in hello Azure Marketplace.</span></span>
* <span data-ttu-id="d8e8f-109">Comment toocreate une application web dans Azure App Service qui est basé sur le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="d8e8f-109">How toocreate a web app in Azure App Service that is based on hello template.</span></span>
* <span data-ttu-id="d8e8f-110">Comment tooconfigure les paramètres de Service d’applications Azure pour hello nouveau web app et la base de données.</span><span class="sxs-lookup"><span data-stu-id="d8e8f-110">How tooconfigure Azure App Service settings for hello new web app and database.</span></span>

<span data-ttu-id="d8e8f-111">Bonjour Azure Marketplace met à disposition un large éventail d’applications web populaires développé par Microsoft, des entreprises tierces et initiatives des logiciels open source.</span><span class="sxs-lookup"><span data-stu-id="d8e8f-111">hello Azure Marketplace makes available a wide range of popular web apps developed by Microsoft, third party companies, and open source software initiatives.</span></span> <span data-ttu-id="d8e8f-112">Hello web applications reposent sur un large éventail d’infrastructures connues, telles que [PHP](/develop/nodejs/) dans cet exemple WordPress, [.NET](/develop/net/), [Node.js](/develop/nodejs/), [Java](/develop/java/), et [Python](/develop/python/), tooname quelques.</span><span class="sxs-lookup"><span data-stu-id="d8e8f-112">hello web apps are built on a wide range of popular frameworks, such as [PHP](/develop/nodejs/) in this WordPress example, [.NET](/develop/net/), [Node.js](/develop/nodejs/), [Java](/develop/java/), and [Python](/develop/python/), tooname a few.</span></span> <span data-ttu-id="d8e8f-113">une application web à partir de hello Azure Marketplace hello uniquement navigateur hello que vous utilisez pour hello logiciels dont vous avez besoin de toocreate [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="d8e8f-113">toocreate a web app from hello Azure Marketplace hello only software you need is hello browser that you use for hello [Azure Portal](https://portal.azure.com/).</span></span> 

<span data-ttu-id="d8e8f-114">site WordPress Hello que vous déployez dans ce didacticiel utilise MySQL pour la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="d8e8f-114">hello WordPress site that you deploy in this tutorial uses MySQL for hello database.</span></span> <span data-ttu-id="d8e8f-115">Si vous souhaitez utiliser tooinstead base de données SQL pour la base de données hello, consultez [Nami du projet](http://projectnami.org/).</span><span class="sxs-lookup"><span data-stu-id="d8e8f-115">If you wish tooinstead use SQL Database for hello database, see [Project Nami](http://projectnami.org/).</span></span> <span data-ttu-id="d8e8f-116">**Projet Nami** est également disponible via hello Marketplace.</span><span class="sxs-lookup"><span data-stu-id="d8e8f-116">**Project Nami** is also available through hello Marketplace.</span></span>

> [!NOTE]
> <span data-ttu-id="d8e8f-117">toocomplete ce didacticiel, vous avez besoin d’un compte Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="d8e8f-117">toocomplete this tutorial, you need a Microsoft Azure account.</span></span> <span data-ttu-id="d8e8f-118">Si vous ne possédez pas de compte, vous pouvez [activer les avantages de votre abonnement Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F) ou [obtenir un essai gratuit](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="d8e8f-118">If you don't have an account, you can [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F) or [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
> 
> <span data-ttu-id="d8e8f-119">Si vous souhaitez tooget démarré avec le Service d’application Azure avant de vous inscrivez pour un compte Azure, accédez trop[Service d’applications essayez](https://azure.microsoft.com/try/app-service/).</span><span class="sxs-lookup"><span data-stu-id="d8e8f-119">If you want tooget started with Azure App Service before you sign up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/).</span></span> <span data-ttu-id="d8e8f-120">Là, vous pouvez créer immédiatement une application de départ temporaire dans App Service. Aucune carte de crédit n’est requise ni aucun engagement.</span><span class="sxs-lookup"><span data-stu-id="d8e8f-120">There, you can immediately create a short-lived starter web app in App Service—no credit card required, and no commitments.</span></span>
> 
> 

## <a name="select-wordpress-and-configure-for-azure-app-service"></a><span data-ttu-id="d8e8f-121">Sélectionner WordPress et configurer pour Azure App Service</span><span class="sxs-lookup"><span data-stu-id="d8e8f-121">Select WordPress and configure for Azure App Service</span></span>
1. <span data-ttu-id="d8e8f-122">Connectez-vous à toohello [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="d8e8f-122">Log in toohello [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="d8e8f-123">Cliquez sur **Nouveau**.</span><span class="sxs-lookup"><span data-stu-id="d8e8f-123">Click **New**.</span></span>
   
    ![Création][5]
3. <span data-ttu-id="d8e8f-125">Recherchez **WordPress**, puis cliquez sur **WordPress**.</span><span class="sxs-lookup"><span data-stu-id="d8e8f-125">Search for **WordPress**, and then click **WordPress**.</span></span> <span data-ttu-id="d8e8f-126">Si vous le souhaitez toouse base de données SQL au lieu de MySQL, recherchez **Nami du projet**.</span><span class="sxs-lookup"><span data-stu-id="d8e8f-126">If you wish toouse SQL Database instead of MySQL, search for **Project Nami**.</span></span>
   
    ![WordPress dans la liste][7]
4. <span data-ttu-id="d8e8f-128">Après avoir lu la description hello de hello WordPress application, cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="d8e8f-128">After reading hello description of hello WordPress app, click **Create**.</span></span>
   
    ![Créer](./media/web-sites-php-web-site-gallery/create.png)
5. <span data-ttu-id="d8e8f-130">Entrez un nom pour l’application web de hello dans hello **application Web** boîte.</span><span class="sxs-lookup"><span data-stu-id="d8e8f-130">Enter a name for hello web app in hello **Web app** box.</span></span>
   
    <span data-ttu-id="d8e8f-131">Ce nom doit être unique dans le domaine azurewebsites.net de hello car hello les URL de l’application web hello est {nom}. azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="d8e8f-131">This name must be unique in hello azurewebsites.net domain because hello URL of hello web app will be {name}.azurewebsites.net.</span></span> <span data-ttu-id="d8e8f-132">Si le nom que vous entrez hello n’est pas unique, un point d’exclamation rouge apparaît dans la zone de texte hello.</span><span class="sxs-lookup"><span data-stu-id="d8e8f-132">If hello name you enter isn't unique, a red exclamation mark appears in hello text box.</span></span>
6. <span data-ttu-id="d8e8f-133">Si vous avez plusieurs abonnements, choisissez hello celui que vous voulez toouse.</span><span class="sxs-lookup"><span data-stu-id="d8e8f-133">If you have more than one subscription, choose hello one you want toouse.</span></span> 
7. <span data-ttu-id="d8e8f-134">Sélectionnez un **Groupe de ressources** ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="d8e8f-134">Select a **Resource Group** or create a new one.</span></span>
   
    <span data-ttu-id="d8e8f-135">Pour plus d’informations sur les groupes de ressources, consultez [Vue d’ensemble d’Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d8e8f-135">For more information about resource groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
8. <span data-ttu-id="d8e8f-136">Sélectionnez un **plan App Service/emplacement** ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="d8e8f-136">Select an **App Service plan/Location** or create a new one.</span></span>
   
    <span data-ttu-id="d8e8f-137">Pour plus d’informations sur les plans App Service, consultez [Présentation des plans d’Azure App Service](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)</span><span class="sxs-lookup"><span data-stu-id="d8e8f-137">For more information about App Service plans, see [Azure App Service plans overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)</span></span>    
9. <span data-ttu-id="d8e8f-138">Cliquez sur **base de données**, puis dans hello **nouvelle base de données MySQL** panneau fournir des valeurs de hello requis pour la configuration de votre base de données MySQL.</span><span class="sxs-lookup"><span data-stu-id="d8e8f-138">Click **Database**, and then in hello **New MySQL Database** blade provide hello required values for configuring your MySQL database.</span></span>
   
    <span data-ttu-id="d8e8f-139">a.</span><span class="sxs-lookup"><span data-stu-id="d8e8f-139">a.</span></span> <span data-ttu-id="d8e8f-140">Entrez un nouveau nom ou laissez le nom par défaut de hello.</span><span class="sxs-lookup"><span data-stu-id="d8e8f-140">Enter a new name or leave hello default name.</span></span>
   
    <span data-ttu-id="d8e8f-141">b.</span><span class="sxs-lookup"><span data-stu-id="d8e8f-141">b.</span></span> <span data-ttu-id="d8e8f-142">Laissez hello **Type de base de données** défini trop**partagé**.</span><span class="sxs-lookup"><span data-stu-id="d8e8f-142">Leave hello **Database Type** set too**Shared**.</span></span>
   
    <span data-ttu-id="d8e8f-143">c.</span><span class="sxs-lookup"><span data-stu-id="d8e8f-143">c.</span></span> <span data-ttu-id="d8e8f-144">Choisissez hello même emplacement que celui que vous hello choisi pour l’application web de hello.</span><span class="sxs-lookup"><span data-stu-id="d8e8f-144">Choose hello same location as hello one you chose for hello web app.</span></span>
   
    <span data-ttu-id="d8e8f-145">d.</span><span class="sxs-lookup"><span data-stu-id="d8e8f-145">d.</span></span> <span data-ttu-id="d8e8f-146">Sélectionnez un niveau tarifaire.</span><span class="sxs-lookup"><span data-stu-id="d8e8f-146">Choose a pricing tier.</span></span> <span data-ttu-id="d8e8f-147">Le niveau Mercure (gratuit avec connexions autorisées et espace disque minimum) convient parfaitement pour ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="d8e8f-147">Mercury (free with minimal allowed connections and disk space) is fine for this tutorial.</span></span>
10. <span data-ttu-id="d8e8f-148">Bonjour **nouvelle base de données MySQL** panneau, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="d8e8f-148">In hello **New MySQL Database** blade, click **OK**.</span></span> 
11. <span data-ttu-id="d8e8f-149">Bonjour **WordPress** panneau, acceptez les conditions juridiques hello, puis cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="d8e8f-149">In hello **WordPress** blade, accept hello legal terms, and then click **Create**.</span></span> 
    
     ![Configurer une application web](./media/web-sites-php-web-site-gallery/configure.png)
    
     <span data-ttu-id="d8e8f-151">Azure App Service crée hello web app, généralement en moins d’une minute.</span><span class="sxs-lookup"><span data-stu-id="d8e8f-151">Azure App Service creates hello web app, typically in less than a minute.</span></span> <span data-ttu-id="d8e8f-152">Vous pouvez surveiller la progression de hello en cliquant sur icône de cloche hello haut hello de page du portail hello.</span><span class="sxs-lookup"><span data-stu-id="d8e8f-152">You can watch hello progress by clicking hello bell icon at hello top of hello portal page.</span></span>
    
     ![Indicateur de progression](./media/web-sites-php-web-site-gallery/progress.png)

## <a name="launch-and-manage-your-wordpress-web-app"></a><span data-ttu-id="d8e8f-154">Lancer et gérer l’application web WordPress</span><span class="sxs-lookup"><span data-stu-id="d8e8f-154">Launch and manage your WordPress web app</span></span>
1. <span data-ttu-id="d8e8f-155">Après la création d’application web hello, naviguer dans le groupe de ressources de toohello hello portail Azure dans lequel vous avez créé l’application hello, et vous pouvez voir hello web app et la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="d8e8f-155">When hello web app creation is finished, navigate in hello Azure Portal toohello resource group in which you created hello application, and you can see hello web app and hello database.</span></span>
   
    <span data-ttu-id="d8e8f-156">Bonjour ressource supplémentaire avec une icône d’ampoule hello est [Application Insights](/services/application-insights/), qui fournit des services de surveillance pour votre application web.</span><span class="sxs-lookup"><span data-stu-id="d8e8f-156">hello extra resource with hello light bulb icon is [Application Insights](/services/application-insights/), which provides monitoring services for your web app.</span></span>
2. <span data-ttu-id="d8e8f-157">Bonjour **groupe de ressources** panneau, cliquez sur la ligne de hello web app.</span><span class="sxs-lookup"><span data-stu-id="d8e8f-157">In hello **Resource group** blade, click hello web app line.</span></span>
   
    ![Configurer une application web](./media/web-sites-php-web-site-gallery/resourcegroup.png)
3. <span data-ttu-id="d8e8f-159">Dans le panneau de l’application hello Web, cliquez sur **Parcourir**.</span><span class="sxs-lookup"><span data-stu-id="d8e8f-159">In hello Web app blade, click **Browse**.</span></span>
   
    ![URL du site][browse]
4. <span data-ttu-id="d8e8f-161">Bonjour WordPress **Bienvenue** page, entrez les informations de configuration hello requises par WordPress, puis cliquez sur **WordPress d’installer**.</span><span class="sxs-lookup"><span data-stu-id="d8e8f-161">In hello WordPress **Welcome** page, enter hello configuration information required by WordPress, and then click **Install WordPress**.</span></span>
   
    ![Configurer WordPress](./media/web-sites-php-web-site-gallery/wpconfigure.png)
5. <span data-ttu-id="d8e8f-163">Connectez-vous à l’aide des informations d’identification hello vous avez créé sur hello **Bienvenue** page.</span><span class="sxs-lookup"><span data-stu-id="d8e8f-163">Log in using hello credentials you created on hello **Welcome** page.</span></span>  
6. <span data-ttu-id="d8e8f-164">La page de tableau de bord de votre site s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="d8e8f-164">Your site Dashboard page opens.</span></span>    
   
    ![Site WordPress](./media/web-sites-php-web-site-gallery/wpdashboard.png)

## <a name="next-steps"></a><span data-ttu-id="d8e8f-166">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d8e8f-166">Next steps</span></span>
<span data-ttu-id="d8e8f-167">Vous avez vu comment toocreate et déployer une application web PHP à partir de la galerie de hello.</span><span class="sxs-lookup"><span data-stu-id="d8e8f-167">You've seen how toocreate and deploy a PHP web app from hello gallery.</span></span> <span data-ttu-id="d8e8f-168">Pour plus d’informations sur l’utilisation de PHP dans Azure, consultez hello [centre de développement PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="d8e8f-168">For more information about using PHP in Azure, see hello [PHP Developer Center](/develop/php/).</span></span>

<span data-ttu-id="d8e8f-169">Pour plus d’informations sur la façon toowork avec les applications de Service Web App, consultez les liens de hello sur hello à gauche de la page hello (pour les fenêtres du navigateur large) ou en hello haut hello (pour les fenêtres du navigateur étroit).</span><span class="sxs-lookup"><span data-stu-id="d8e8f-169">For more information about how toowork with App Service Web Apps, see hello links on hello left side of hello page (for wide browser windows) or at hello top of hello page (for narrow browser windows).</span></span> 

## <a name="whats-changed"></a><span data-ttu-id="d8e8f-170">Changements apportés</span><span class="sxs-lookup"><span data-stu-id="d8e8f-170">What's changed</span></span>
* <span data-ttu-id="d8e8f-171">Pour une modification de toohello guide à partir de sites Web tooApp Service, consultez [Azure App Service et son impact sur les Services Azure existants](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="d8e8f-171">For a guide toohello change from Websites tooApp Service, see [Azure App Service and its impact on existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

[5]: ./media/web-sites-php-web-site-gallery/startmarketplace.png
[7]: ./media/web-sites-php-web-site-gallery/search-web-app.png
[browse]: ./media/web-sites-php-web-site-gallery/browse-web.png
