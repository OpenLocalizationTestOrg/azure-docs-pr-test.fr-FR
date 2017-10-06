---
title: "aaaCreate et se connecter tooa de la base de données MySQL dans Azure"
description: "Découvrez comment toouse hello toocreate portail Azure une base de données MySQL et puis connectez-vous tooit à partir d’une application web PHP dans Azure."
documentationcenter: php
services: app-service\web
author: cephalin
manager: erikre
editor: 
tags: mysql
ms.assetid: 55465a9a-7e65-4fd9-8a65-dd83ee41f3e5
ms.service: multiple
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm;cephalin
ms.openlocfilehash: 3abc02f8887432625666afd847e9dc0c0a4db2e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-connect-tooa-mysql-database-in-azure"></a><span data-ttu-id="3b19d-103">Créer et connecter la base de données MySQL tooa dans Azure</span><span class="sxs-lookup"><span data-stu-id="3b19d-103">Create and connect tooa MySQL database in Azure</span></span>
<span data-ttu-id="3b19d-104">Ce didacticiel vous montre comment toocreate un MySQL de base de données Bonjour [portail Azure](https://portal.azure.com) (fournisseur est [ClearDB](http://www.cleardb.com/)) et comment tooit tooconnect à partir de PHP web application en cours d’exécution [Azure App Service](app-service/app-service-value-prop-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="3b19d-104">This tutorial shows you how toocreate a MySQL database in hello [Azure portal](https://portal.azure.com) (provider is [ClearDB](http://www.cleardb.com/)) and how tooconnect tooit from a PHP web app running in [Azure App Service](app-service/app-service-value-prop-what-is.md).</span></span>

> [!NOTE]
> <span data-ttu-id="3b19d-105">Vous pouvez également créer une base de données MySQL dans le cadre d’un [modèle d’application Marketplace](app-service-web/app-service-web-create-web-app-from-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="3b19d-105">You can also create a MySQL database as part of a [Marketplace app template](app-service-web/app-service-web-create-web-app-from-marketplace.md).</span></span>
>
>

## <a name="create-a-mysql-database-in-azure-portal"></a><span data-ttu-id="3b19d-106">Création d’une base de données MySQL dans le portail Azure</span><span class="sxs-lookup"><span data-stu-id="3b19d-106">Create a MySQL database in Azure portal</span></span>
<span data-ttu-id="3b19d-107">toocreate une base de données MySQL hello portail Azure, procédez comme hello suivant :</span><span class="sxs-lookup"><span data-stu-id="3b19d-107">toocreate a MySQL database in hello Azure portal, do hello following:</span></span>

1. <span data-ttu-id="3b19d-108">Connectez-vous à toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3b19d-108">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="3b19d-109">Dans le menu de gauche hello, cliquez sur **nouveau** > **données + stockage** > **base de données MySQL**.</span><span class="sxs-lookup"><span data-stu-id="3b19d-109">From hello left menu, click **New** > **Data + Storage** > **MySQL Database**.</span></span>

    ![Création d’une base de données MySQL dans Azure - démarrer](./media/store-php-create-mysql-database/create-db-1-start.png)
3. <span data-ttu-id="3b19d-111">Dans la nouvelle base de données MySQL de hello [panneau](azure-portal-overview.md), configurez votre nouvelle base de données MySQL comme suit (*panneau*: une page de portail ouvre horizontalement) :</span><span class="sxs-lookup"><span data-stu-id="3b19d-111">In hello New MySQL Database [blade](azure-portal-overview.md), configure your new MySQL database as follows (*blade*: a portal page that opens horizontally):</span></span>

   * <span data-ttu-id="3b19d-112">**Nom de base de données**: entrez un nom d’identification unique</span><span class="sxs-lookup"><span data-stu-id="3b19d-112">**Database Name**: Type a uniquely identifiable name</span></span>
   * <span data-ttu-id="3b19d-113">**Abonnement**: choisissez hello abonnement toouse</span><span class="sxs-lookup"><span data-stu-id="3b19d-113">**Subscription**: Choose hello subscription toouse</span></span>
   * <span data-ttu-id="3b19d-114">**Type de base de données**: sélectionnez **Shared** pour les niveaux faible coût ou libres, ou **dédié** tooget des ressources dédiées.</span><span class="sxs-lookup"><span data-stu-id="3b19d-114">**Database Type**: Select **Shared** for low-cost or free tiers, or **Dedicated** tooget dedicated resources.</span></span>
   * <span data-ttu-id="3b19d-115">**Groupe de ressources**: ajouter existant de tooan de base de données MySQL hello [groupe de ressources](azure-resource-manager/resource-group-overview.md) ou le placer dans un autre.</span><span class="sxs-lookup"><span data-stu-id="3b19d-115">**Resource group**: Add hello MySQL database tooan existing [resource group](azure-resource-manager/resource-group-overview.md) or put it in a new one.</span></span> <span data-ttu-id="3b19d-116">Ressources de hello même groupe permettre être facilement géré ensemble.</span><span class="sxs-lookup"><span data-stu-id="3b19d-116">Resources in hello same group can be easily managed together.</span></span>
   * <span data-ttu-id="3b19d-117">**Emplacement**: sélectionnez un tooyou fermer d’emplacement.</span><span class="sxs-lookup"><span data-stu-id="3b19d-117">**Location**: Select a location close tooyou.</span></span> <span data-ttu-id="3b19d-118">Lorsque vous ajoutez tooan groupe de ressources existant, vous êtes emplacement du groupe de ressources toohello verrouillé.</span><span class="sxs-lookup"><span data-stu-id="3b19d-118">When adding tooan existing resource group, you're locked toohello resource group's location.</span></span>
   * <span data-ttu-id="3b19d-119">**Niveau tarifaire** : cliquez sur **Niveau tarifaire**, puis sélectionnez une option de tarification (le niveau **Mercure** est gratuit), puis cliquez sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="3b19d-119">**Pricing Tier**: Click **Pricing Tier**, then select a pricing option (**Mercury** tier is free), and then click **Select**.</span></span>
   * <span data-ttu-id="3b19d-120">**Conditions juridiques**: cliquez sur **juridiques**, passez en revue les détails de l’achat hello, puis cliquez sur **acheter**.</span><span class="sxs-lookup"><span data-stu-id="3b19d-120">**Legal Terms**: Click **Legal Terms**, review hello purchase details, and click **Purchase**.</span></span>
   * <span data-ttu-id="3b19d-121">**Code confidentiel toodashboard**: sélectionnez si vous souhaitez tooaccess directement à partir du tableau de bord hello.</span><span class="sxs-lookup"><span data-stu-id="3b19d-121">**Pin toodashboard**: Select if you want tooaccess it directly from hello dashboard.</span></span> <span data-ttu-id="3b19d-122">Cette fonctionnalité est particulièrement utile si vous n’êtes pas encore tout à fait familiarisé avec la navigation dans le portail.</span><span class="sxs-lookup"><span data-stu-id="3b19d-122">This is especially helpful if you aren't familiar with portal navigation yet.</span></span>

     <span data-ttu-id="3b19d-123">après la capture d’écran de Hello est juste un exemple de comment vous pouvez configurer votre base de données MySQL.</span><span class="sxs-lookup"><span data-stu-id="3b19d-123">hello following screenshot is just an example of how you can configure your MySQL database.</span></span>  
     ![Création d’une base de données MySQL dans Azure - configurer](./media/store-php-create-mysql-database/create-db-2-configure.png)
4. <span data-ttu-id="3b19d-125">Une fois la configuration terminée, cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="3b19d-125">When you're done configuring, click **Create**.</span></span>

    ![Création d’une base de données MySQL dans Azure - créer](./media/store-php-create-mysql-database/create-db-3-create.png)

    <span data-ttu-id="3b19d-127">Une notification contextuelle vous informe que le déploiement a démarré.</span><span class="sxs-lookup"><span data-stu-id="3b19d-127">You will see a pop-up notification letting you know that deployment has started.</span></span>

    ![Création d’une base de données MySQL dans Azure - en cours](./media/store-php-create-mysql-database/create-db-4-started-status.png)

    <span data-ttu-id="3b19d-129">Une autre fenêtre contextuelle s’affiche une fois le déploiement réussi.</span><span class="sxs-lookup"><span data-stu-id="3b19d-129">You will get another pop-up once deployment has succeeded.</span></span> <span data-ttu-id="3b19d-130">portail de Hello s’ouvre également automatiquement votre Panneau de base de données MySQL.</span><span class="sxs-lookup"><span data-stu-id="3b19d-130">hello portal will also open your MySQL database blade automatically.</span></span>

<a name="connect"></a>

## <a name="connect-tooyour-mysql-database"></a><span data-ttu-id="3b19d-131">Connexion de base de données MySQL tooyour</span><span class="sxs-lookup"><span data-stu-id="3b19d-131">Connect tooyour MySQL database</span></span>
<span data-ttu-id="3b19d-132">informations de connexion toosee hello pour votre nouvelle base de données MySQL, cliquez simplement sur **propriétés** dans le panneau de votre application web.</span><span class="sxs-lookup"><span data-stu-id="3b19d-132">toosee hello connection information for your new MySQL database, just click **Properties** in your web app's blade.</span></span>

![Création d'une base de données MySQL dans Azure - panneau Base de données MySQL](./media/store-php-create-mysql-database/create-db-5-finished-db-blade.png)

<span data-ttu-id="3b19d-134">Vous pouvez désormais utiliser ces informations de connexion dans n’importe quelle application web.</span><span class="sxs-lookup"><span data-stu-id="3b19d-134">You can now use that connection information in any web app.</span></span> <span data-ttu-id="3b19d-135">Un exemple qui montre comment les informations de connexion toouse hello à partir d’une simple application PHP sont disponibles [ici](https://github.com/WindowsAzure/azure-sdk-for-php-samples/tree/master/tasklist-mysql).</span><span class="sxs-lookup"><span data-stu-id="3b19d-135">A sample that shows how toouse hello connection information from a simple PHP app is available [here](https://github.com/WindowsAzure/azure-sdk-for-php-samples/tree/master/tasklist-mysql).</span></span>

## <a name="connect-a-laravel-web-app-from-hello-php-get-started-tutorial"></a><span data-ttu-id="3b19d-136">Se connecter à une application web de Laravel (à partir de hello PHP get didacticiel)</span><span class="sxs-lookup"><span data-stu-id="3b19d-136">Connect a Laravel web app (from hello PHP get started tutorial)</span></span>
<span data-ttu-id="3b19d-137">Supposons que vous le didacticiel de hello simplement terminé [créer, configurer et déployer un tooAzure d’application web PHP](app-service-web/app-service-web-php-get-started.md) et avoir un [Laravel](https://www.laravel.com/) application web s’exécutant dans Azure.</span><span class="sxs-lookup"><span data-stu-id="3b19d-137">Suppose you just finished hello tutorial [Create, configure, and deploy a PHP web app tooAzure](app-service-web/app-service-web-php-get-started.md) and have a [Laravel](https://www.laravel.com/) web app running in Azure.</span></span> <span data-ttu-id="3b19d-138">Vous pouvez facilement ajouter des applications de base de données des fonctionnalités tooyour Laravel.</span><span class="sxs-lookup"><span data-stu-id="3b19d-138">You can easily add database capabilities tooyour Laravel app.</span></span> <span data-ttu-id="3b19d-139">Suivez simplement les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="3b19d-139">Just follow hello steps below:</span></span>

> [!NOTE]
> <span data-ttu-id="3b19d-140">Hello étapes suivantes supposent que vous avez terminé le didacticiel de hello [créer, configurer et déployer un tooAzure d’application web PHP](app-service-web/app-service-web-php-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="3b19d-140">hello following steps assume that you have finished hello tutorial [Create, configure, and deploy a PHP web app tooAzure](app-service-web/app-service-web-php-get-started.md).</span></span>
>
>

1. <span data-ttu-id="3b19d-141">Configurer hello Laravel d’application dans votre base de données de développement local environnement toopoint toohello MySQL.</span><span class="sxs-lookup"><span data-stu-id="3b19d-141">Configure hello Laravel app in your local development environment toopoint toohello MySQL database.</span></span> <span data-ttu-id="3b19d-142">toodo, ouvrez `.env` à partir de votre application Laravel répertoire racine et configurer les options de base de données MySQL hello.</span><span class="sxs-lookup"><span data-stu-id="3b19d-142">toodo this, open `.env` from your Laravel app's root directory and configure hello MySQL database options.</span></span>

        DB_CONNECTION=mysql
        DB_HOST=<HOSTNAME_from_properties_blade>
        DB_PORT=<PORT_from_properties_blade>
        DB_DATABASE=<see_note_below>
        DB_USERNAME=<USERNAME_from_properties_blade>
        DB_PASSWORD=<PASSWORD_from_properties_blade>

   > [!NOTE]
   > <span data-ttu-id="3b19d-143">Bonjour **propriétés** panneau, nom hello de votre base de données MySQL peut ou peuvent ne pas hello une figurer Bonjour **nom de la base de données** champ.</span><span class="sxs-lookup"><span data-stu-id="3b19d-143">In hello **Properties** blade, hello name of your MySQL database may or may not be hello one shown in hello **DATABASE NAME** field.</span></span> <span data-ttu-id="3b19d-144">Il est mieux paramètre de base de données toocheck hello Bonjour **chaîne de connexion** champ.</span><span class="sxs-lookup"><span data-stu-id="3b19d-144">It's better toocheck hello Database parameter in hello **CONNECTION STRING** field.</span></span>    
   >
   > ![Création d’une base de données MySQL dans Azure - en cours](./media/store-php-create-mysql-database/connect-db-1-database-name.png)
   >
   >
2. <span data-ttu-id="3b19d-146">Bonjour tooverify de manière plus rapide que vous avez maintenant accès de MySQL est toouse [la structure de l’authentification de Laravel par défaut](https://laravel.com/docs/5.2/authentication#authentication-quickstart).</span><span class="sxs-lookup"><span data-stu-id="3b19d-146">hello quickest way tooverify that you have MySQL access now is toouse [Laravel's default authentication scaffolding](https://laravel.com/docs/5.2/authentication#authentication-quickstart).</span></span>
   <span data-ttu-id="3b19d-147">Dans un terminal de ligne de commande hello, exécutez hello suivant les commandes à partir du répertoire racine de votre application Laravel :</span><span class="sxs-lookup"><span data-stu-id="3b19d-147">In hello command-line terminal, run hello following commands from your Laravel app's root directory:</span></span>

         php artisan migrate
         php artisan make:auth

    <span data-ttu-id="3b19d-148">Hello première commande crée des tables de hello dans Azure en fonction des migrations prédéfinies Bonjour `database/migrations` active et hello deuxième commande squelettes hello itinéraires pour l’authentification et d’inscription des utilisateurs et vues de base.</span><span class="sxs-lookup"><span data-stu-id="3b19d-148">hello first command creates hello tables in Azure based on predefined migrations in hello `database/migrations` directory, and hello second  command scaffolds hello basic views and routes for user registration and authentication.</span></span>
3. <span data-ttu-id="3b19d-149">Exécuter le serveur de développement hello maintenant :</span><span class="sxs-lookup"><span data-stu-id="3b19d-149">Run hello development server now:</span></span>

        php artisan serve
4. <span data-ttu-id="3b19d-150">Dans le navigateur de hello, accédez toohttp://localhost:8000 et inscrire un nouvel utilisateur, comme indiqué :</span><span class="sxs-lookup"><span data-stu-id="3b19d-150">In hello browser, navigate toohttp://localhost:8000 and register a new user as shown:</span></span>

    ![Se connecter tooMySQL de base de données dans Azure - inscription de l’utilisateur](./media/store-php-create-mysql-database/connect-db-2-development-server.png)

    <span data-ttu-id="3b19d-152">Suivez l’inscription de hello UI invite hello terminée.</span><span class="sxs-lookup"><span data-stu-id="3b19d-152">Follow hello UI prompt complete hello registration.</span></span> <span data-ttu-id="3b19d-153">Une fois l’inscription terminée, vous serez connecté.</span><span class="sxs-lookup"><span data-stu-id="3b19d-153">Once registration completes, you will be logged in.</span></span>

    ![Se connecter tooMySQL de base de données dans Azure - inscription de l’utilisateur](./media/store-php-create-mysql-database/connect-db-3-registered-user.png)

    <span data-ttu-id="3b19d-155">Vous développez votre application sur la base de données MySQL hello dans Azure maintenant.</span><span class="sxs-lookup"><span data-stu-id="3b19d-155">You are now developing your app against hello MySQL database in Azure.</span></span>
5. <span data-ttu-id="3b19d-156">Maintenant, vous devez simplement tooreplicate votre `.env` paramètres tooyour Azure web app.</span><span class="sxs-lookup"><span data-stu-id="3b19d-156">Now, you just need tooreplicate your `.env` settings tooyour Azure web app.</span></span> <span data-ttu-id="3b19d-157">Exécutez hello suivant des commandes CLI d’Azure :</span><span class="sxs-lookup"><span data-stu-id="3b19d-157">Run hello following Azure CLI commands:</span></span>

        azure site appsetting add DB_CONNECTION=mysql
        azure site appsetting add DB_HOST=<HOSTNAME_from_properties_blade>
        azure site appsetting add DB_PORT=<PORT_from_properties_blade>
        azure site appsetting add DB_DATABASE=<Database_param_from_CONNECTION_INFO_from_properties_blade>
        azure site appsetting add DB_USERNAME=<USERNAME_from_properties_blade>
        azure site appsetting add DB_PASSWORD=<PASSWORD_from_properties_blade>

6. <span data-ttu-id="3b19d-158">Ensuite, validez et envoyez les modifications locales hello tooAzure apportées précédemment lors de l’exécution `php artisan make:auth`.</span><span class="sxs-lookup"><span data-stu-id="3b19d-158">Next, commit and push tooAzure hello local changes made earlier while running `php artisan make:auth`.</span></span>

        git add .
        git commit -m "scaffold auth views and routes"
        git push azure master
7. <span data-ttu-id="3b19d-159">Parcourir toohello Azure web app.</span><span class="sxs-lookup"><span data-stu-id="3b19d-159">Browse toohello Azure web app.</span></span>

        azure site browse
8. <span data-ttu-id="3b19d-160">Connectez-vous en utilisant les informations d’identification de l’utilisateur hello que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="3b19d-160">Log in using hello user credentials you created earlier.</span></span>

    ![Se connecter tooMySQL de base de données dans Azure - parcourir l’application web tooAzure](./media/store-php-create-mysql-database/connect-db-4-browse-azure-webapp.png)

    <span data-ttu-id="3b19d-162">Une fois que vous vous connectez, vous devez voir l’écran de post connexion convivial hello.</span><span class="sxs-lookup"><span data-stu-id="3b19d-162">After you log in, you should see hello friendly post-login screen.</span></span>

    ![Se connecter tooMySQL de base de données dans Azure - connecté](./media/store-php-create-mysql-database/connect-db-5-logged-in.png)

    <span data-ttu-id="3b19d-164">Félicitations, votre application web PHP dans Azure a désormais accès aux données à partir de votre base de données MySQL.</span><span class="sxs-lookup"><span data-stu-id="3b19d-164">Congratulations, your PHP web app in Azure is now accessing data from your MySQL database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3b19d-165">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3b19d-165">Next steps</span></span>
<span data-ttu-id="3b19d-166">Pour plus d’informations, consultez hello [centre de développement PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="3b19d-166">For more information, see hello [PHP Developer Center](/develop/php/).</span></span>
