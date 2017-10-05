---
title: "Création et connexion à une base de données MySQL dans Azure"
description: "Apprenez à utiliser le portail Azure pour créer une base de données MySQL et vous y connecter à partir d’une application web PHP dans Azure."
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
ms.openlocfilehash: 66f4b7a5f8eb3f6f125c9420b40caffca3d43dd6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-connect-to-a-mysql-database-in-azure"></a><span data-ttu-id="347d5-103">Création et connexion à une base de données MySQL dans Azure</span><span class="sxs-lookup"><span data-stu-id="347d5-103">Create and connect to a MySQL database in Azure</span></span>
<span data-ttu-id="347d5-104">Ce tutoriel vous montre comment créer une base de données MySQL sur le [portail Azure](https://portal.azure.com) (fournisseur [ClearDB](http://www.cleardb.com/)) et s’y connecter à partir d’une application web en PHP s’exécutant dans [Azure App Service](app-service/app-service-value-prop-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="347d5-104">This tutorial shows you how to create a MySQL database in the [Azure portal](https://portal.azure.com) (provider is [ClearDB](http://www.cleardb.com/)) and how to connect to it from a PHP web app running in [Azure App Service](app-service/app-service-value-prop-what-is.md).</span></span>

> [!NOTE]
> <span data-ttu-id="347d5-105">Vous pouvez également créer une base de données MySQL dans le cadre d’un [modèle d’application Marketplace](app-service-web/app-service-web-create-web-app-from-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="347d5-105">You can also create a MySQL database as part of a [Marketplace app template](app-service-web/app-service-web-create-web-app-from-marketplace.md).</span></span>
>
>

## <a name="create-a-mysql-database-in-azure-portal"></a><span data-ttu-id="347d5-106">Création d’une base de données MySQL dans le portail Azure</span><span class="sxs-lookup"><span data-stu-id="347d5-106">Create a MySQL database in Azure portal</span></span>
<span data-ttu-id="347d5-107">Pour créer une base de données MySQL dans le portail Azure, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="347d5-107">To create a MySQL database in the Azure portal, do the following:</span></span>

1. <span data-ttu-id="347d5-108">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="347d5-108">Log in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="347d5-109">Dans le menu de gauche, cliquez sur **Nouveau** > **Données + Stockage** > **Base de données MySQL**.</span><span class="sxs-lookup"><span data-stu-id="347d5-109">From the left menu, click **New** > **Data + Storage** > **MySQL Database**.</span></span>

    ![Création d’une base de données MySQL dans Azure - démarrer](./media/store-php-create-mysql-database/create-db-1-start.png)
3. <span data-ttu-id="347d5-111">Dans le [panneau](azure-portal-overview.md)Nouvelle base de données MySQL, configurez votre nouvelle base de données MySQL comme suit (*panneau*: une page du portail s’ouvre à l’horizontale) :</span><span class="sxs-lookup"><span data-stu-id="347d5-111">In the New MySQL Database [blade](azure-portal-overview.md), configure your new MySQL database as follows (*blade*: a portal page that opens horizontally):</span></span>

   * <span data-ttu-id="347d5-112">**Nom de base de données**: entrez un nom d’identification unique</span><span class="sxs-lookup"><span data-stu-id="347d5-112">**Database Name**: Type a uniquely identifiable name</span></span>
   * <span data-ttu-id="347d5-113">**Abonnement**: choisissez l’abonnement à utiliser</span><span class="sxs-lookup"><span data-stu-id="347d5-113">**Subscription**: Choose the subscription to use</span></span>
   * <span data-ttu-id="347d5-114">**Type de base de données** : sélectionnez **Partagé** pour les niveaux économiques ou gratuits, ou **Dédié** pour obtenir des ressources dédiées.</span><span class="sxs-lookup"><span data-stu-id="347d5-114">**Database Type**: Select **Shared** for low-cost or free tiers, or **Dedicated** to get dedicated resources.</span></span>
   * <span data-ttu-id="347d5-115">**Groupe de ressources**: ajoutez la base de données MySQL à un [groupe de ressources](azure-resource-manager/resource-group-overview.md) existant ou placez-la dans un nouveau groupe.</span><span class="sxs-lookup"><span data-stu-id="347d5-115">**Resource group**: Add the MySQL database to an existing [resource group](azure-resource-manager/resource-group-overview.md) or put it in a new one.</span></span> <span data-ttu-id="347d5-116">Les ressources du même groupe peuvent être facilement gérées ensemble.</span><span class="sxs-lookup"><span data-stu-id="347d5-116">Resources in the same group can be easily managed together.</span></span>
   * <span data-ttu-id="347d5-117">**Emplacement**: choisissez un emplacement proche.</span><span class="sxs-lookup"><span data-stu-id="347d5-117">**Location**: Select a location close to you.</span></span> <span data-ttu-id="347d5-118">Lorsque vous ajoutez la base de données à un groupe de ressources existant, vous êtes limité à l’emplacement du groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="347d5-118">When adding to an existing resource group, you're locked to the resource group's location.</span></span>
   * <span data-ttu-id="347d5-119">**Niveau tarifaire** : cliquez sur **Niveau tarifaire**, puis sélectionnez une option de tarification (le niveau **Mercure** est gratuit), puis cliquez sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="347d5-119">**Pricing Tier**: Click **Pricing Tier**, then select a pricing option (**Mercury** tier is free), and then click **Select**.</span></span>
   * <span data-ttu-id="347d5-120">**Conditions juridiques** : cliquez sur **Conditions juridiques**, passez en revue les détails de l’achat, puis cliquez sur **Acheter**.</span><span class="sxs-lookup"><span data-stu-id="347d5-120">**Legal Terms**: Click **Legal Terms**, review the purchase details, and click **Purchase**.</span></span>
   * <span data-ttu-id="347d5-121">**Épingler au tableau de bord**: sélectionnez cette option si vous souhaitez bénéficier d’un accès direct depuis le tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="347d5-121">**Pin to dashboard**: Select if you want to access it directly from the dashboard.</span></span> <span data-ttu-id="347d5-122">Cette fonctionnalité est particulièrement utile si vous n’êtes pas encore tout à fait familiarisé avec la navigation dans le portail.</span><span class="sxs-lookup"><span data-stu-id="347d5-122">This is especially helpful if you aren't familiar with portal navigation yet.</span></span>

     <span data-ttu-id="347d5-123">La capture d’écran suivante illustre une manière de configurer votre base de données MySQL.</span><span class="sxs-lookup"><span data-stu-id="347d5-123">The following screenshot is just an example of how you can configure your MySQL database.</span></span>  
     ![Création d’une base de données MySQL dans Azure - configurer](./media/store-php-create-mysql-database/create-db-2-configure.png)
4. <span data-ttu-id="347d5-125">Une fois la configuration terminée, cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="347d5-125">When you're done configuring, click **Create**.</span></span>

    ![Création d’une base de données MySQL dans Azure - créer](./media/store-php-create-mysql-database/create-db-3-create.png)

    <span data-ttu-id="347d5-127">Une notification contextuelle vous informe que le déploiement a démarré.</span><span class="sxs-lookup"><span data-stu-id="347d5-127">You will see a pop-up notification letting you know that deployment has started.</span></span>

    ![Création d’une base de données MySQL dans Azure - en cours](./media/store-php-create-mysql-database/create-db-4-started-status.png)

    <span data-ttu-id="347d5-129">Une autre fenêtre contextuelle s’affiche une fois le déploiement réussi.</span><span class="sxs-lookup"><span data-stu-id="347d5-129">You will get another pop-up once deployment has succeeded.</span></span> <span data-ttu-id="347d5-130">Le portail ouvre aussi automatiquement le panneau de votre base de données MySQL.</span><span class="sxs-lookup"><span data-stu-id="347d5-130">The portal will also open your MySQL database blade automatically.</span></span>

<a name="connect"></a>

## <a name="connect-to-your-mysql-database"></a><span data-ttu-id="347d5-131">Connexion à la base de données MySQL</span><span class="sxs-lookup"><span data-stu-id="347d5-131">Connect to your MySQL database</span></span>
<span data-ttu-id="347d5-132">Pour afficher les informations de connexion de votre nouvelle base de données MySQL, cliquez simplement sur **Propriétés** sur le panneau de votre application web.</span><span class="sxs-lookup"><span data-stu-id="347d5-132">To see the connection information for your new MySQL database, just click **Properties** in your web app's blade.</span></span>

![Création d'une base de données MySQL dans Azure - panneau Base de données MySQL](./media/store-php-create-mysql-database/create-db-5-finished-db-blade.png)

<span data-ttu-id="347d5-134">Vous pouvez désormais utiliser ces informations de connexion dans n’importe quelle application web.</span><span class="sxs-lookup"><span data-stu-id="347d5-134">You can now use that connection information in any web app.</span></span> <span data-ttu-id="347d5-135">Cliquez [ici](https://github.com/WindowsAzure/azure-sdk-for-php-samples/tree/master/tasklist-mysql)pour obtenir un exemple d’utilisation des informations de connexion à partir d’une simple application PHP.</span><span class="sxs-lookup"><span data-stu-id="347d5-135">A sample that shows how to use the connection information from a simple PHP app is available [here](https://github.com/WindowsAzure/azure-sdk-for-php-samples/tree/master/tasklist-mysql).</span></span>

## <a name="connect-a-laravel-web-app-from-the-php-get-started-tutorial"></a><span data-ttu-id="347d5-136">Connecter une application web Laravel (à partir du didacticiel de prise en main de PHP)</span><span class="sxs-lookup"><span data-stu-id="347d5-136">Connect a Laravel web app (from the PHP get started tutorial)</span></span>
<span data-ttu-id="347d5-137">Supposons que vous venez de terminer le didacticiel [Create, configure, and deploy a PHP web app to Azure](app-service-web/app-service-web-php-get-started.md) (Créer, configurer et déployer une application web PHP sur Azure) et que vous disposez d’une application web [Laravel](https://www.laravel.com/) exécutée dans Azure.</span><span class="sxs-lookup"><span data-stu-id="347d5-137">Suppose you just finished the tutorial [Create, configure, and deploy a PHP web app to Azure](app-service-web/app-service-web-php-get-started.md) and have a [Laravel](https://www.laravel.com/) web app running in Azure.</span></span> <span data-ttu-id="347d5-138">Vous pouvez facilement ajouter des fonctionnalités de base de données à votre application Laravel.</span><span class="sxs-lookup"><span data-stu-id="347d5-138">You can easily add database capabilities to your Laravel app.</span></span> <span data-ttu-id="347d5-139">Pour ce faire, procédez simplement comme suit :</span><span class="sxs-lookup"><span data-stu-id="347d5-139">Just follow the steps below:</span></span>

> [!NOTE]
> <span data-ttu-id="347d5-140">La procédure suivante suppose que vous avez terminé le didacticiel [Create, configure, and deploy a PHP web app to Azure](app-service-web/app-service-web-php-get-started.md)(Créer, configurer et déployer une application web PHP sur Azure).</span><span class="sxs-lookup"><span data-stu-id="347d5-140">The following steps assume that you have finished the tutorial [Create, configure, and deploy a PHP web app to Azure](app-service-web/app-service-web-php-get-started.md).</span></span>
>
>

1. <span data-ttu-id="347d5-141">Configurez l’application Laravel dans votre environnement de développement local pour pointer vers la base de données MySQL.</span><span class="sxs-lookup"><span data-stu-id="347d5-141">Configure the Laravel app in your local development environment to point to the MySQL database.</span></span> <span data-ttu-id="347d5-142">Pour ce faire, ouvrez `.env` à partir du répertoire racine de votre application Laravel, puis configurez les options de la base de données MySQL.</span><span class="sxs-lookup"><span data-stu-id="347d5-142">To do this, open `.env` from your Laravel app's root directory and configure the MySQL database options.</span></span>

        DB_CONNECTION=mysql
        DB_HOST=<HOSTNAME_from_properties_blade>
        DB_PORT=<PORT_from_properties_blade>
        DB_DATABASE=<see_note_below>
        DB_USERNAME=<USERNAME_from_properties_blade>
        DB_PASSWORD=<PASSWORD_from_properties_blade>

   > [!NOTE]
   > <span data-ttu-id="347d5-143">Dans le panneau **Propriétés**, le nom de votre base de données MySQL peut correspondre ou non à celui indiqué dans le champ **NOM DE BASE DE DONNÉES**.</span><span class="sxs-lookup"><span data-stu-id="347d5-143">In the **Properties** blade, the name of your MySQL database may or may not be the one shown in the **DATABASE NAME** field.</span></span> <span data-ttu-id="347d5-144">Il est préférable de vérifier le paramètre de base de données dans le champ **CHAÎNE DE CONNEXION** .</span><span class="sxs-lookup"><span data-stu-id="347d5-144">It's better to check the Database parameter in the **CONNECTION STRING** field.</span></span>    
   >
   > ![Création d’une base de données MySQL dans Azure - en cours](./media/store-php-create-mysql-database/connect-db-1-database-name.png)
   >
   >
2. <span data-ttu-id="347d5-146">Pour vérifier que vous avez maintenant accès à MySQL, le moyen le plus rapide consiste à utiliser la [structure d’authentification par défaut de Laravel](https://laravel.com/docs/5.2/authentication#authentication-quickstart).</span><span class="sxs-lookup"><span data-stu-id="347d5-146">The quickest way to verify that you have MySQL access now is to use [Laravel's default authentication scaffolding](https://laravel.com/docs/5.2/authentication#authentication-quickstart).</span></span>
   <span data-ttu-id="347d5-147">Dans le terminal de ligne de commande, exécutez les commandes suivantes à partir du répertoire racine de votre application Laravel :</span><span class="sxs-lookup"><span data-stu-id="347d5-147">In the command-line terminal, run the following commands from your Laravel app's root directory:</span></span>

         php artisan migrate
         php artisan make:auth

    <span data-ttu-id="347d5-148">La première commande crée les tables dans Azure en fonction des migrations prédéfinies dans le répertoire `database/migrations` ; la deuxième commande structure les vues et itinéraires de base pour l’inscription et l’authentification de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="347d5-148">The first command creates the tables in Azure based on predefined migrations in the `database/migrations` directory, and the second  command scaffolds the basic views and routes for user registration and authentication.</span></span>
3. <span data-ttu-id="347d5-149">Exécutez maintenant le serveur de développement :</span><span class="sxs-lookup"><span data-stu-id="347d5-149">Run the development server now:</span></span>

        php artisan serve
4. <span data-ttu-id="347d5-150">Dans le navigateur, accédez à http://localhost:8000 et procédez comme suit pour inscrire un nouvel utilisateur :</span><span class="sxs-lookup"><span data-stu-id="347d5-150">In the browser, navigate to http://localhost:8000 and register a new user as shown:</span></span>

    ![Connexion à une base de données MySQL dans Azure - inscrire un utilisateur](./media/store-php-create-mysql-database/connect-db-2-development-server.png)

    <span data-ttu-id="347d5-152">Suivez les instructions de l’interface utilisateur pour terminer l’inscription.</span><span class="sxs-lookup"><span data-stu-id="347d5-152">Follow the UI prompt complete the registration.</span></span> <span data-ttu-id="347d5-153">Une fois l’inscription terminée, vous serez connecté.</span><span class="sxs-lookup"><span data-stu-id="347d5-153">Once registration completes, you will be logged in.</span></span>

    ![Connexion à une base de données MySQL dans Azure - inscrire un utilisateur](./media/store-php-create-mysql-database/connect-db-3-registered-user.png)

    <span data-ttu-id="347d5-155">Vous allez maintenant développer votre application sur la base de données MySQL dans Azure.</span><span class="sxs-lookup"><span data-stu-id="347d5-155">You are now developing your app against the MySQL database in Azure.</span></span>
5. <span data-ttu-id="347d5-156">Il vous suffit à présent de répliquer vos paramètres `.env` dans votre application web Azure.</span><span class="sxs-lookup"><span data-stu-id="347d5-156">Now, you just need to replicate your `.env` settings to your Azure web app.</span></span> <span data-ttu-id="347d5-157">Exécutez les commandes suivantes dans l’interface de ligne de commande Azure :</span><span class="sxs-lookup"><span data-stu-id="347d5-157">Run the following Azure CLI commands:</span></span>

        azure site appsetting add DB_CONNECTION=mysql
        azure site appsetting add DB_HOST=<HOSTNAME_from_properties_blade>
        azure site appsetting add DB_PORT=<PORT_from_properties_blade>
        azure site appsetting add DB_DATABASE=<Database_param_from_CONNECTION_INFO_from_properties_blade>
        azure site appsetting add DB_USERNAME=<USERNAME_from_properties_blade>
        azure site appsetting add DB_PASSWORD=<PASSWORD_from_properties_blade>

6. <span data-ttu-id="347d5-158">Ensuite, validez et envoyez dans Azure les modifications locales que vous avez effectuées pendant l’exécution de `php artisan make:auth`.</span><span class="sxs-lookup"><span data-stu-id="347d5-158">Next, commit and push to Azure the local changes made earlier while running `php artisan make:auth`.</span></span>

        git add .
        git commit -m "scaffold auth views and routes"
        git push azure master
7. <span data-ttu-id="347d5-159">Accédez à l’application web Azure.</span><span class="sxs-lookup"><span data-stu-id="347d5-159">Browse to the Azure web app.</span></span>

        azure site browse
8. <span data-ttu-id="347d5-160">Connectez-vous en utilisant les informations d’identification utilisateur créées précédemment.</span><span class="sxs-lookup"><span data-stu-id="347d5-160">Log in using the user credentials you created earlier.</span></span>

    ![Connexion à une base de données MySQL dans Azure - accéder à l’application web Azure](./media/store-php-create-mysql-database/connect-db-4-browse-azure-webapp.png)

    <span data-ttu-id="347d5-162">Une fois connecté, vous devriez accéder à l’écran post-connexion.</span><span class="sxs-lookup"><span data-stu-id="347d5-162">After you log in, you should see the friendly post-login screen.</span></span>

    ![Connexion à une base de données MySQL dans Azure - connecté](./media/store-php-create-mysql-database/connect-db-5-logged-in.png)

    <span data-ttu-id="347d5-164">Félicitations, votre application web PHP dans Azure a désormais accès aux données à partir de votre base de données MySQL.</span><span class="sxs-lookup"><span data-stu-id="347d5-164">Congratulations, your PHP web app in Azure is now accessing data from your MySQL database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="347d5-165">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="347d5-165">Next steps</span></span>
<span data-ttu-id="347d5-166">Pour plus d’informations, consultez le [Centre pour développeurs PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="347d5-166">For more information, see the [PHP Developer Center](/develop/php/).</span></span>
