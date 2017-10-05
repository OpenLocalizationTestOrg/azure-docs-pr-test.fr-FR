---
title: "Créer une application web WordPress dans Azure App Service | Microsoft Docs"
description: "Découvrez comment créer une application web Azure pour un blog WordPress par le biais du portail Azure."
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
ms.openlocfilehash: 460afdabed947fb4018a9ea8a7a5bc7dc5bc89c7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-wordpress-web-app-in-azure-app-service"></a><span data-ttu-id="b09de-103">Créer une application web WordPress dans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="b09de-103">Create a WordPress web app in Azure App Service</span></span>
[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

<span data-ttu-id="b09de-104">Ce didacticiel montre comment déployer un blog WordPress à partir d’Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="b09de-104">This tutorial shows how to deploy a WordPress blog site from the Azure Marketplace.</span></span>

<span data-ttu-id="b09de-105">Lorsque vous aurez terminé avec le didacticiel, vous disposerez de votre propre blog WordPress installé et configuré dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="b09de-105">When you're done with the tutorial you'll have your own WordPress blog site up and running in the cloud.</span></span>

![Site WordPress](./media/web-sites-php-web-site-gallery/wpdashboard.png)

<span data-ttu-id="b09de-107">Vous apprendrez ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="b09de-107">You'll learn:</span></span>

* <span data-ttu-id="b09de-108">Comment trouver un modèle d’application dans Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="b09de-108">How to find an application template in the Azure Marketplace.</span></span>
* <span data-ttu-id="b09de-109">Comment créer une application web dans Azure App Service basée sur le modèle.</span><span class="sxs-lookup"><span data-stu-id="b09de-109">How to create a web app in Azure App Service that is based on the template.</span></span>
* <span data-ttu-id="b09de-110">Comment configurer les paramètres d’Azure App Service pour la nouvelle application web et la nouvelle base de données.</span><span class="sxs-lookup"><span data-stu-id="b09de-110">How to configure Azure App Service settings for the new web app and database.</span></span>

<span data-ttu-id="b09de-111">Azure Marketplace met à votre disposition une large gamme d’applications web populaires, développées par Microsoft, par des sociétés tierces ou par des initiatives de logiciel open source.</span><span class="sxs-lookup"><span data-stu-id="b09de-111">The Azure Marketplace makes available a wide range of popular web apps developed by Microsoft, third party companies, and open source software initiatives.</span></span> <span data-ttu-id="b09de-112">Les applications web sont basées sur un large éventail d’infrastructures répandues, notamment [PHP](/develop/nodejs/) dans cet exemple WordPress, [.NET](/develop/net/), [Node.js](/develop/nodejs/), [Java](/develop/java/) et [Python](/develop/python/), pour en citer quelques-unes.</span><span class="sxs-lookup"><span data-stu-id="b09de-112">The web apps are built on a wide range of popular frameworks, such as [PHP](/develop/nodejs/) in this WordPress example, [.NET](/develop/net/), [Node.js](/develop/nodejs/), [Java](/develop/java/), and [Python](/develop/python/), to name a few.</span></span> <span data-ttu-id="b09de-113">Pour créer une application web à partir d’Azure Marketplace, le seul logiciel nécessaire est le navigateur que vous utilisez pour le [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="b09de-113">To create a web app from the Azure Marketplace the only software you need is the browser that you use for the [Azure Portal](https://portal.azure.com/).</span></span> 

<span data-ttu-id="b09de-114">Le site WordPress déployé dans le cadre de ce didacticiel utilise MySQL pour la base de données.</span><span class="sxs-lookup"><span data-stu-id="b09de-114">The WordPress site that you deploy in this tutorial uses MySQL for the database.</span></span> <span data-ttu-id="b09de-115">Si vous préférez utiliser Base de données SQL à la place, consultez [Project Nami](http://projectnami.org/).</span><span class="sxs-lookup"><span data-stu-id="b09de-115">If you wish to instead use SQL Database for the database, see [Project Nami](http://projectnami.org/).</span></span> <span data-ttu-id="b09de-116">**Project Nami** est également disponible dans Marketplace.</span><span class="sxs-lookup"><span data-stu-id="b09de-116">**Project Nami** is also available through the Marketplace.</span></span>

> [!NOTE]
> <span data-ttu-id="b09de-117">Pour suivre ce didacticiel, vous avez besoin d'un compte Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="b09de-117">To complete this tutorial, you need a Microsoft Azure account.</span></span> <span data-ttu-id="b09de-118">Si vous ne possédez pas de compte, vous pouvez [activer les avantages de votre abonnement Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F) ou [obtenir un essai gratuit](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="b09de-118">If you don't have an account, you can [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F) or [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
> 
> <span data-ttu-id="b09de-119">Si vous souhaitez commencer à utiliser Azure App Service avant d’ouvrir un compte Azure, accédez à [Essayer App Service](https://azure.microsoft.com/try/app-service/).</span><span class="sxs-lookup"><span data-stu-id="b09de-119">If you want to get started with Azure App Service before you sign up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/).</span></span> <span data-ttu-id="b09de-120">Là, vous pouvez créer immédiatement une application de départ temporaire dans App Service. Aucune carte de crédit n’est requise ni aucun engagement.</span><span class="sxs-lookup"><span data-stu-id="b09de-120">There, you can immediately create a short-lived starter web app in App Service—no credit card required, and no commitments.</span></span>
> 
> 

## <a name="select-wordpress-and-configure-for-azure-app-service"></a><span data-ttu-id="b09de-121">Sélectionner WordPress et configurer pour Azure App Service</span><span class="sxs-lookup"><span data-stu-id="b09de-121">Select WordPress and configure for Azure App Service</span></span>
1. <span data-ttu-id="b09de-122">Connectez-vous au [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="b09de-122">Log in to the [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="b09de-123">Cliquez sur **Nouveau**.</span><span class="sxs-lookup"><span data-stu-id="b09de-123">Click **New**.</span></span>
   
    ![Création][5]
3. <span data-ttu-id="b09de-125">Recherchez **WordPress**, puis cliquez sur **WordPress**.</span><span class="sxs-lookup"><span data-stu-id="b09de-125">Search for **WordPress**, and then click **WordPress**.</span></span> <span data-ttu-id="b09de-126">Si vous souhaitez utiliser Base de données SQL au lieu de MySQL, recherchez **Project Nami**.</span><span class="sxs-lookup"><span data-stu-id="b09de-126">If you wish to use SQL Database instead of MySQL, search for **Project Nami**.</span></span>
   
    ![WordPress dans la liste][7]
4. <span data-ttu-id="b09de-128">Après avoir lu la description de l’application WordPress, cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="b09de-128">After reading the description of the WordPress app, click **Create**.</span></span>
   
    ![Créer](./media/web-sites-php-web-site-gallery/create.png)
5. <span data-ttu-id="b09de-130">Entrez un nom pour l’application web dans la zone **Application web** .</span><span class="sxs-lookup"><span data-stu-id="b09de-130">Enter a name for the web app in the **Web app** box.</span></span>
   
    <span data-ttu-id="b09de-131">Ce nom doit être unique dans le domaine azurewebsites.net, car l’URL de l’application web sera {nom}.azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="b09de-131">This name must be unique in the azurewebsites.net domain because the URL of the web app will be {name}.azurewebsites.net.</span></span> <span data-ttu-id="b09de-132">Si le nom que vous entrez n’est pas unique, un point d’exclamation rouge s’affiche dans la zone de texte.</span><span class="sxs-lookup"><span data-stu-id="b09de-132">If the name you enter isn't unique, a red exclamation mark appears in the text box.</span></span>
6. <span data-ttu-id="b09de-133">Si vous avez plusieurs abonnements, choisissez celui que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="b09de-133">If you have more than one subscription, choose the one you want to use.</span></span> 
7. <span data-ttu-id="b09de-134">Sélectionnez un **Groupe de ressources** ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="b09de-134">Select a **Resource Group** or create a new one.</span></span>
   
    <span data-ttu-id="b09de-135">Pour plus d’informations sur les groupes de ressources, consultez [Vue d’ensemble d’Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b09de-135">For more information about resource groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
8. <span data-ttu-id="b09de-136">Sélectionnez un **plan App Service/emplacement** ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="b09de-136">Select an **App Service plan/Location** or create a new one.</span></span>
   
    <span data-ttu-id="b09de-137">Pour plus d’informations sur les plans App Service, consultez [Présentation des plans d’Azure App Service](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)</span><span class="sxs-lookup"><span data-stu-id="b09de-137">For more information about App Service plans, see [Azure App Service plans overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)</span></span>    
9. <span data-ttu-id="b09de-138">Cliquez sur **Base de données** puis, dans le panneau **Nouvelle base de données MySQL**, indiquez les valeurs requises pour configurer votre base de données MySQL.</span><span class="sxs-lookup"><span data-stu-id="b09de-138">Click **Database**, and then in the **New MySQL Database** blade provide the required values for configuring your MySQL database.</span></span>
   
    <span data-ttu-id="b09de-139">a.</span><span class="sxs-lookup"><span data-stu-id="b09de-139">a.</span></span> <span data-ttu-id="b09de-140">Entrez un nouveau nom ou conservez le nom par défaut.</span><span class="sxs-lookup"><span data-stu-id="b09de-140">Enter a new name or leave the default name.</span></span>
   
    <span data-ttu-id="b09de-141">b.</span><span class="sxs-lookup"><span data-stu-id="b09de-141">b.</span></span> <span data-ttu-id="b09de-142">Laissez le **Type de base de données** défini sur la valeur **Partagé**.</span><span class="sxs-lookup"><span data-stu-id="b09de-142">Leave the **Database Type** set to **Shared**.</span></span>
   
    <span data-ttu-id="b09de-143">c.</span><span class="sxs-lookup"><span data-stu-id="b09de-143">c.</span></span> <span data-ttu-id="b09de-144">Choisissez le même emplacement que celui choisi pour l’application web.</span><span class="sxs-lookup"><span data-stu-id="b09de-144">Choose the same location as the one you chose for the web app.</span></span>
   
    <span data-ttu-id="b09de-145">d.</span><span class="sxs-lookup"><span data-stu-id="b09de-145">d.</span></span> <span data-ttu-id="b09de-146">Sélectionnez un niveau tarifaire.</span><span class="sxs-lookup"><span data-stu-id="b09de-146">Choose a pricing tier.</span></span> <span data-ttu-id="b09de-147">Le niveau Mercure (gratuit avec connexions autorisées et espace disque minimum) convient parfaitement pour ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="b09de-147">Mercury (free with minimal allowed connections and disk space) is fine for this tutorial.</span></span>
10. <span data-ttu-id="b09de-148">Dans le panneau **Nouvelle base de données MySQL**, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="b09de-148">In the **New MySQL Database** blade, click **OK**.</span></span> 
11. <span data-ttu-id="b09de-149">Dans le panneau **WordPress**, acceptez les mentions légales, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="b09de-149">In the **WordPress** blade, accept the legal terms, and then click **Create**.</span></span> 
    
     ![Configurer une application web](./media/web-sites-php-web-site-gallery/configure.png)
    
     <span data-ttu-id="b09de-151">Généralement, Azure App Service crée l’application web en moins d’une minute.</span><span class="sxs-lookup"><span data-stu-id="b09de-151">Azure App Service creates the web app, typically in less than a minute.</span></span> <span data-ttu-id="b09de-152">Vous pouvez surveiller la progression en cliquant sur l’icône en forme de cloche en haut de la page du portail.</span><span class="sxs-lookup"><span data-stu-id="b09de-152">You can watch the progress by clicking the bell icon at the top of the portal page.</span></span>
    
     ![Indicateur de progression](./media/web-sites-php-web-site-gallery/progress.png)

## <a name="launch-and-manage-your-wordpress-web-app"></a><span data-ttu-id="b09de-154">Lancer et gérer l’application web WordPress</span><span class="sxs-lookup"><span data-stu-id="b09de-154">Launch and manage your WordPress web app</span></span>
1. <span data-ttu-id="b09de-155">Une fois la création de l’application web terminée, dans le portail Azure, accédez au groupe de ressources dans lequel vous avez créé l’application ; vous pourrez voir l’application web et la base de données.</span><span class="sxs-lookup"><span data-stu-id="b09de-155">When the web app creation is finished, navigate in the Azure Portal to the resource group in which you created the application, and you can see the web app and the database.</span></span>
   
    <span data-ttu-id="b09de-156">La ressource supplémentaire dotée de l’icône en forme d’ampoule est [Application Insights](/services/application-insights/), qui fournit des services de surveillance pour votre application web.</span><span class="sxs-lookup"><span data-stu-id="b09de-156">The extra resource with the light bulb icon is [Application Insights](/services/application-insights/), which provides monitoring services for your web app.</span></span>
2. <span data-ttu-id="b09de-157">Dans le panneau **Groupe de ressources** , cliquez sur la ligne de l’application web.</span><span class="sxs-lookup"><span data-stu-id="b09de-157">In the **Resource group** blade, click the web app line.</span></span>
   
    ![Configurer une application web](./media/web-sites-php-web-site-gallery/resourcegroup.png)
3. <span data-ttu-id="b09de-159">Dans le panneau Application Web, cliquez sur **Parcourir**.</span><span class="sxs-lookup"><span data-stu-id="b09de-159">In the Web app blade, click **Browse**.</span></span>
   
    ![URL du site][browse]
4. <span data-ttu-id="b09de-161">Sur la page de **bienvenue** WordPress, entrez les informations de configuration requises par WordPress, puis cliquez sur **Install WordPress**.</span><span class="sxs-lookup"><span data-stu-id="b09de-161">In the WordPress **Welcome** page, enter the configuration information required by WordPress, and then click **Install WordPress**.</span></span>
   
    ![Configurer WordPress](./media/web-sites-php-web-site-gallery/wpconfigure.png)
5. <span data-ttu-id="b09de-163">Connectez-vous en utilisant les informations d’identification créées sur la page de **bienvenue** .</span><span class="sxs-lookup"><span data-stu-id="b09de-163">Log in using the credentials you created on the **Welcome** page.</span></span>  
6. <span data-ttu-id="b09de-164">La page de tableau de bord de votre site s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="b09de-164">Your site Dashboard page opens.</span></span>    
   
    ![Site WordPress](./media/web-sites-php-web-site-gallery/wpdashboard.png)

## <a name="next-steps"></a><span data-ttu-id="b09de-166">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b09de-166">Next steps</span></span>
<span data-ttu-id="b09de-167">Vous savez désormais comment créer et déployer une application web PHP à partir de la galerie.</span><span class="sxs-lookup"><span data-stu-id="b09de-167">You've seen how to create and deploy a PHP web app from the gallery.</span></span> <span data-ttu-id="b09de-168">Pour plus d’informations sur l’utilisation de PHP dans Azure, consultez le [Centre de développement PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="b09de-168">For more information about using PHP in Azure, see the [PHP Developer Center](/develop/php/).</span></span>

<span data-ttu-id="b09de-169">Pour plus d’informations sur l’utilisation d’App Service Web Apps, consultez les liens sur le côté gauche de la page (pour les grandes fenêtres de navigateur) ou en haut de la page (pour les fenêtres de navigateur étroites).</span><span class="sxs-lookup"><span data-stu-id="b09de-169">For more information about how to work with App Service Web Apps, see the links on the left side of the page (for wide browser windows) or at the top of the page (for narrow browser windows).</span></span> 

## <a name="whats-changed"></a><span data-ttu-id="b09de-170">Changements apportés</span><span class="sxs-lookup"><span data-stu-id="b09de-170">What's changed</span></span>
* <span data-ttu-id="b09de-171">Pour obtenir un guide présentant les modifications apportées dans le cadre de la transition entre Sites Web et App Service, consultez [Azure App Service et les services Azure existants](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="b09de-171">For a guide to the change from Websites to App Service, see [Azure App Service and its impact on existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

[5]: ./media/web-sites-php-web-site-gallery/startmarketplace.png
[7]: ./media/web-sites-php-web-site-gallery/search-web-app.png
[browse]: ./media/web-sites-php-web-site-gallery/browse-web.png
