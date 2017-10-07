---
title: aaaDeploy une application WordPress Bonjour Azure portal dans les cinq minutes | Documents Microsoft
description: "Découvrir combien il est facile toorun les applications web dans le Service d’applications en déployant une application WordPress. Consultez immédiatement les résultats."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 6feac128-c728-4491-8b79-962da9a40788
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/13/2017
ms.author: cephalin
ms.openlocfilehash: 4cd26bbacf89657997847ded1284e472288ddebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-wordpress-app-in-hello-azure-portal-in-five-minutes"></a><span data-ttu-id="9ad09-104">Déployer une application WordPress Bonjour Azure portal dans les cinq minutes</span><span class="sxs-lookup"><span data-stu-id="9ad09-104">Deploy a WordPress app in hello Azure portal in five minutes</span></span>

<span data-ttu-id="9ad09-105">Ce didacticiel vous montre comment toodeploy votre premier [WordPress](https://wordpress.org/) web application trop[Azure App Service](../app-service/app-service-value-prop-what-is.md) en minutes.</span><span class="sxs-lookup"><span data-stu-id="9ad09-105">This tutorial shows you how toodeploy your first [WordPress](https://wordpress.org/) web app too[Azure App Service](../app-service/app-service-value-prop-what-is.md) in minutes.</span></span>

![Site WordPress](./media/app-service-web-get-started-php-portal/wpdashboard.png)

## <a name="prerequisites"></a><span data-ttu-id="9ad09-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="9ad09-107">Prerequisites</span></span>
<span data-ttu-id="9ad09-108">Vous devez avoir un compte Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="9ad09-108">You need a Microsoft Azure account.</span></span> <span data-ttu-id="9ad09-109">Si vous n’avez pas de compte, vous pouvez [vous inscrire pour un essai gratuit](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) ou [activer les avantages de votre abonnement Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="9ad09-109">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>

> [!NOTE]
> <span data-ttu-id="9ad09-110">Vous pouvez [essayer App Service](https://azure.microsoft.com/try/app-service/) sans compte Azure.</span><span class="sxs-lookup"><span data-stu-id="9ad09-110">You can [Try App Service](https://azure.microsoft.com/try/app-service/) without an Azure account.</span></span> <span data-ttu-id="9ad09-111">Créer une application de démarrage et de le manipuler pour les horaires de tooan--aucune carte de crédit requis, aucune des engagements.</span><span class="sxs-lookup"><span data-stu-id="9ad09-111">Create a starter app and play with it for up tooan hour--no credit card required, no commitments.</span></span>
> 
> 

## <a name="deploy-hello-wordpress-app"></a><span data-ttu-id="9ad09-112">Déploiement d’une application de WordPress hello</span><span class="sxs-lookup"><span data-stu-id="9ad09-112">Deploy hello WordPress app</span></span>
1. <span data-ttu-id="9ad09-113">Connectez-vous à toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9ad09-113">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="9ad09-114">Ouvrez [https://portal.azure.com/#create/WordPress.WordPress](https://portal.azure.com/#create/WordPress.WordPress).</span><span class="sxs-lookup"><span data-stu-id="9ad09-114">Open [https://portal.azure.com/#create/WordPress.WordPress](https://portal.azure.com/#create/WordPress.WordPress).</span></span>

    <span data-ttu-id="9ad09-115">Ce lien est un raccourci tooimmediately configurer une nouvelle application WordPress Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="9ad09-115">This link is a shortcut tooimmediately configure a new WordPress app in hello Azure portal.</span></span>

3. <span data-ttu-id="9ad09-116">Sous **Nom de l’application**, entrez un nom d’application web.</span><span class="sxs-lookup"><span data-stu-id="9ad09-116">In **App name**, type a web app name.</span></span> <span data-ttu-id="9ad09-117">Vous verrez une coche verte dans la zone de hello si le nom de hello est unique dans hello `azurewebsites.net` domaine.</span><span class="sxs-lookup"><span data-stu-id="9ad09-117">You will see a green checkmark in hello box if hello name is unique in hello `azurewebsites.net` domain.</span></span>
   
5. <span data-ttu-id="9ad09-118">Dans **groupe de ressources**, cliquez sur **nouvel** toocreate une nouvelle [groupe de ressources](../azure-resource-manager/resource-group-overview.md), puis attribuez-lui un nom.</span><span class="sxs-lookup"><span data-stu-id="9ad09-118">In **Resource Group**, click **Create new** toocreate a new [resource group](../azure-resource-manager/resource-group-overview.md), then give it a name.</span></span>

6. <span data-ttu-id="9ad09-119">Sous **Fournisseur de base de données**, sélectionnez **CleaDB**.</span><span class="sxs-lookup"><span data-stu-id="9ad09-119">In **Database Provider**, select **CleaDB**.</span></span>

7. <span data-ttu-id="9ad09-120">Cliquez sur **Plan App Service/Emplacement** > **Créer**.</span><span class="sxs-lookup"><span data-stu-id="9ad09-120">Click **App Service plan/Location** > **Create New**.</span></span> <span data-ttu-id="9ad09-121">Configurer hello [plan App Service](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) comme indiqué :</span><span class="sxs-lookup"><span data-stu-id="9ad09-121">Configure hello [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) as shown:</span></span>

    - <span data-ttu-id="9ad09-122">Dans **plan App Service**, nom de type hello souhaité.</span><span class="sxs-lookup"><span data-stu-id="9ad09-122">In **App Service plan**, type hello desired name.</span></span>
    - <span data-ttu-id="9ad09-123">Dans **emplacement**, choisissez un emplacement toohost votre plan.</span><span class="sxs-lookup"><span data-stu-id="9ad09-123">In **Location**, choose a location toohost your plan.</span></span>
    - <span data-ttu-id="9ad09-124">Cliquez sur **Niveau de tarification**, puis sélectionnez **F1 gratuit** ou un autre niveau qui vous convient, puis cliquez sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="9ad09-124">Click **Pricing tier**, then select **F1 Free** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="9ad09-125">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="9ad09-125">Click **OK**.</span></span>

8. <span data-ttu-id="9ad09-126">Cliquez sur **Base de données** > **Créer**.</span><span class="sxs-lookup"><span data-stu-id="9ad09-126">Click **Database** > **Create New**.</span></span> <span data-ttu-id="9ad09-127">Configurer hello de base de données SQL comme indiqué :</span><span class="sxs-lookup"><span data-stu-id="9ad09-127">Configure hello SQL Database as shown:</span></span>

    - <span data-ttu-id="9ad09-128">Sous **Nom de la base de données**, entrez un nom pour la base de données.</span><span class="sxs-lookup"><span data-stu-id="9ad09-128">In **Database Name**, type a database name.</span></span> 
    - <span data-ttu-id="9ad09-129">Dans **emplacement**, choisissez hello même emplacement que hello plan App Service.</span><span class="sxs-lookup"><span data-stu-id="9ad09-129">In **Location**, choose hello same location as hello App Service plan.</span></span>
    - <span data-ttu-id="9ad09-130">Cliquez sur **Niveau de tarification**, puis sélectionnez **Mercury** ou un autre niveau qui vous convient, puis cliquez sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="9ad09-130">Click **Pricing tier**, then select **Mercury** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="9ad09-131">Cliquez sur **Mentions légales** et sur **Acheter**.</span><span class="sxs-lookup"><span data-stu-id="9ad09-131">Click **Legal Terms** and click **Purchase**.</span></span>
    - <span data-ttu-id="9ad09-132">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="9ad09-132">Click **OK**.</span></span>

9. <span data-ttu-id="9ad09-133">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="9ad09-133">Click **Create**.</span></span>

    <span data-ttu-id="9ad09-134">À présent, Azure crée votre application WordPress en fonction de votre configuration.</span><span class="sxs-lookup"><span data-stu-id="9ad09-134">Azure now creates your WordPress app based on your configuration.</span></span> <span data-ttu-id="9ad09-135">Vous devriez voir le message **Le déploiement a commencé**.</span><span class="sxs-lookup"><span data-stu-id="9ad09-135">You should see a **Deployment started...** notification.</span></span>

    ![Déploiement commencé - première configuration WordPress dans Azure App Service](./media/app-service-web-get-started-php-portal/deployment-started.png)
   
## <a name="launch-and-manage-your-wordpress-web-app"></a><span data-ttu-id="9ad09-137">Lancer et gérer l’application web WordPress</span><span class="sxs-lookup"><span data-stu-id="9ad09-137">Launch and manage your WordPress web app</span></span>

<span data-ttu-id="9ad09-138">Une autre notification s’affiche quand Azure termine le déploiement de l’application.</span><span class="sxs-lookup"><span data-stu-id="9ad09-138">When Azure completes app deployment you see another notification.</span></span>

![Déploiement réussi - première configuration WordPress dans Azure App Service](./media/app-service-web-get-started-php-portal/deployment-succeeded.png)

1. <span data-ttu-id="9ad09-140">Cliquez sur hello notification.</span><span class="sxs-lookup"><span data-stu-id="9ad09-140">Click hello notification.</span></span> <span data-ttu-id="9ad09-141">Si vous l’avez manqué, vous pouvez toujours y accéder en cliquant sur la cloche de notification hello (![ctiver Notification - première WordPress dans Azure App Service](./media/app-service-web-get-started-dotnet-portal/notification.png)).</span><span class="sxs-lookup"><span data-stu-id="9ad09-141">If you missed it, you can always access it by clicking hello notification bell (![Notification bellow - first WordPress in Azure App Service](./media/app-service-web-get-started-dotnet-portal/notification.png)).</span></span>

    <span data-ttu-id="9ad09-142">Vous devriez maintenant voir le [panneau](../azure-resource-manager/resource-group-portal.md#manage-resources) de gestion de votre application web (*panneau* : page de portail qui s’ouvre horizontalement).</span><span class="sxs-lookup"><span data-stu-id="9ad09-142">You should now see your web app's management [blade](../azure-resource-manager/resource-group-portal.md#manage-resources) (*blade*: a portal page that opens horizontally).</span></span>

3. <span data-ttu-id="9ad09-143">Dans hello en haut de page de vue d’ensemble de hello, cliquez sur **Parcourir**.</span><span class="sxs-lookup"><span data-stu-id="9ad09-143">In hello top of hello Overview page, click **Browse**.</span></span>
   
    ![Parcourir - première configuration WordPress dans Azure App Service](./media/app-service-web-get-started-php-portal/browse.png)

    <span data-ttu-id="9ad09-145">Maintenant vous voyez hello WordPress **Bienvenue** page.</span><span class="sxs-lookup"><span data-stu-id="9ad09-145">Now you see hello WordPress **Welcome** page.</span></span> <span data-ttu-id="9ad09-146">Configurer l’installation de WordPress hello et commencez la lecture avec lui.</span><span class="sxs-lookup"><span data-stu-id="9ad09-146">Configure hello WordPress installation and start playing with it!</span></span>

    ![Configuration de WordPress - première configuration WordPress dans Azure App Service](./media/app-service-web-get-started-php-portal/wordpress-config.png)
    
## <a name="next-steps"></a><span data-ttu-id="9ad09-148">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9ad09-148">Next steps</span></span>
* <span data-ttu-id="9ad09-149">[Créer, configurer et déployer un tooAzure d’application de web Laravel](app-service-web-php-get-started.md) -compétences hello élémentaires vous avez besoin toorun n’importe quelle application web PHP dans Azure, telles que :</span><span class="sxs-lookup"><span data-stu-id="9ad09-149">[Create, configure, and deploy a Laravel web app tooAzure](app-service-web-php-get-started.md) - Learn hello basic skills you need toorun any PHP web app in Azure, such as:</span></span>

    * <span data-ttu-id="9ad09-150">Créer et configurer des applications dans Azure depuis PowerShell/Bash</span><span class="sxs-lookup"><span data-stu-id="9ad09-150">Create and configure apps in Azure from PowerShell/Bash.</span></span>
    * <span data-ttu-id="9ad09-151">Définir la version PHP</span><span class="sxs-lookup"><span data-stu-id="9ad09-151">Set PHP version.</span></span>
    * <span data-ttu-id="9ad09-152">Utiliser un fichier de démarrage qui n’est pas dans le répertoire de l’application hello racine.</span><span class="sxs-lookup"><span data-stu-id="9ad09-152">Use a start file that is not in hello root application directory.</span></span>
    * <span data-ttu-id="9ad09-153">Activer l’automatisation de Composer</span><span class="sxs-lookup"><span data-stu-id="9ad09-153">Enable Composer automation.</span></span>
    * <span data-ttu-id="9ad09-154">Accéder à des variables propres à l’environnement</span><span class="sxs-lookup"><span data-stu-id="9ad09-154">Access environment-specific variables.</span></span>
    * <span data-ttu-id="9ad09-155">Résoudre les problèmes courants</span><span class="sxs-lookup"><span data-stu-id="9ad09-155">Troubleshoot common errors.</span></span>

* <span data-ttu-id="9ad09-156">[Déployer votre tooAzure de code du Service d’applications](web-sites-deploy.md)-Découvrez comment toodeploy à partir de FTP ou à partir de la source de contrôler les référentiels.</span><span class="sxs-lookup"><span data-stu-id="9ad09-156">[Deploy your code tooAzure App Service](web-sites-deploy.md)- Learn how toodeploy from FTP or from source control repositories.</span></span>
* <span data-ttu-id="9ad09-157">[Ajouter des fonctionnalités tooyour première application web](app-service-web-get-started-2.md) -se toohello de votre application Azure ensuite au niveau.</span><span class="sxs-lookup"><span data-stu-id="9ad09-157">[Add functionality tooyour first web app](app-service-web-get-started-2.md) - Take your Azure app toohello next level.</span></span> <span data-ttu-id="9ad09-158">Authentifiez vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="9ad09-158">Authenticate your users.</span></span> <span data-ttu-id="9ad09-159">Faites évoluer sa capacité en fonction de la demande.</span><span class="sxs-lookup"><span data-stu-id="9ad09-159">Scale it based on demand.</span></span> <span data-ttu-id="9ad09-160">Configurez des alertes de performance.</span><span class="sxs-lookup"><span data-stu-id="9ad09-160">Set up some performance alerts.</span></span> <span data-ttu-id="9ad09-161">Tout cela en seulement quelques clics.</span><span class="sxs-lookup"><span data-stu-id="9ad09-161">All with a few clicks.</span></span>
