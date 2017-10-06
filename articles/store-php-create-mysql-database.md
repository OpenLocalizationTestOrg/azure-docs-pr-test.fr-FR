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
# <a name="create-and-connect-tooa-mysql-database-in-azure"></a>Créer et connecter la base de données MySQL tooa dans Azure
Ce didacticiel vous montre comment toocreate un MySQL de base de données Bonjour [portail Azure](https://portal.azure.com) (fournisseur est [ClearDB](http://www.cleardb.com/)) et comment tooit tooconnect à partir de PHP web application en cours d’exécution [Azure App Service](app-service/app-service-value-prop-what-is.md).

> [!NOTE]
> Vous pouvez également créer une base de données MySQL dans le cadre d’un [modèle d’application Marketplace](app-service-web/app-service-web-create-web-app-from-marketplace.md).
>
>

## <a name="create-a-mysql-database-in-azure-portal"></a>Création d’une base de données MySQL dans le portail Azure
toocreate une base de données MySQL hello portail Azure, procédez comme hello suivant :

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Dans le menu de gauche hello, cliquez sur **nouveau** > **données + stockage** > **base de données MySQL**.

    ![Création d’une base de données MySQL dans Azure - démarrer](./media/store-php-create-mysql-database/create-db-1-start.png)
3. Dans la nouvelle base de données MySQL de hello [panneau](azure-portal-overview.md), configurez votre nouvelle base de données MySQL comme suit (*panneau*: une page de portail ouvre horizontalement) :

   * **Nom de base de données**: entrez un nom d’identification unique
   * **Abonnement**: choisissez hello abonnement toouse
   * **Type de base de données**: sélectionnez **Shared** pour les niveaux faible coût ou libres, ou **dédié** tooget des ressources dédiées.
   * **Groupe de ressources**: ajouter existant de tooan de base de données MySQL hello [groupe de ressources](azure-resource-manager/resource-group-overview.md) ou le placer dans un autre. Ressources de hello même groupe permettre être facilement géré ensemble.
   * **Emplacement**: sélectionnez un tooyou fermer d’emplacement. Lorsque vous ajoutez tooan groupe de ressources existant, vous êtes emplacement du groupe de ressources toohello verrouillé.
   * **Niveau tarifaire** : cliquez sur **Niveau tarifaire**, puis sélectionnez une option de tarification (le niveau **Mercure** est gratuit), puis cliquez sur **Sélectionner**.
   * **Conditions juridiques**: cliquez sur **juridiques**, passez en revue les détails de l’achat hello, puis cliquez sur **acheter**.
   * **Code confidentiel toodashboard**: sélectionnez si vous souhaitez tooaccess directement à partir du tableau de bord hello. Cette fonctionnalité est particulièrement utile si vous n’êtes pas encore tout à fait familiarisé avec la navigation dans le portail.

     après la capture d’écran de Hello est juste un exemple de comment vous pouvez configurer votre base de données MySQL.  
     ![Création d’une base de données MySQL dans Azure - configurer](./media/store-php-create-mysql-database/create-db-2-configure.png)
4. Une fois la configuration terminée, cliquez sur **Créer**.

    ![Création d’une base de données MySQL dans Azure - créer](./media/store-php-create-mysql-database/create-db-3-create.png)

    Une notification contextuelle vous informe que le déploiement a démarré.

    ![Création d’une base de données MySQL dans Azure - en cours](./media/store-php-create-mysql-database/create-db-4-started-status.png)

    Une autre fenêtre contextuelle s’affiche une fois le déploiement réussi. portail de Hello s’ouvre également automatiquement votre Panneau de base de données MySQL.

<a name="connect"></a>

## <a name="connect-tooyour-mysql-database"></a>Connexion de base de données MySQL tooyour
informations de connexion toosee hello pour votre nouvelle base de données MySQL, cliquez simplement sur **propriétés** dans le panneau de votre application web.

![Création d'une base de données MySQL dans Azure - panneau Base de données MySQL](./media/store-php-create-mysql-database/create-db-5-finished-db-blade.png)

Vous pouvez désormais utiliser ces informations de connexion dans n’importe quelle application web. Un exemple qui montre comment les informations de connexion toouse hello à partir d’une simple application PHP sont disponibles [ici](https://github.com/WindowsAzure/azure-sdk-for-php-samples/tree/master/tasklist-mysql).

## <a name="connect-a-laravel-web-app-from-hello-php-get-started-tutorial"></a>Se connecter à une application web de Laravel (à partir de hello PHP get didacticiel)
Supposons que vous le didacticiel de hello simplement terminé [créer, configurer et déployer un tooAzure d’application web PHP](app-service-web/app-service-web-php-get-started.md) et avoir un [Laravel](https://www.laravel.com/) application web s’exécutant dans Azure. Vous pouvez facilement ajouter des applications de base de données des fonctionnalités tooyour Laravel. Suivez simplement les étapes de hello ci-dessous :

> [!NOTE]
> Hello étapes suivantes supposent que vous avez terminé le didacticiel de hello [créer, configurer et déployer un tooAzure d’application web PHP](app-service-web/app-service-web-php-get-started.md).
>
>

1. Configurer hello Laravel d’application dans votre base de données de développement local environnement toopoint toohello MySQL. toodo, ouvrez `.env` à partir de votre application Laravel répertoire racine et configurer les options de base de données MySQL hello.

        DB_CONNECTION=mysql
        DB_HOST=<HOSTNAME_from_properties_blade>
        DB_PORT=<PORT_from_properties_blade>
        DB_DATABASE=<see_note_below>
        DB_USERNAME=<USERNAME_from_properties_blade>
        DB_PASSWORD=<PASSWORD_from_properties_blade>

   > [!NOTE]
   > Bonjour **propriétés** panneau, nom hello de votre base de données MySQL peut ou peuvent ne pas hello une figurer Bonjour **nom de la base de données** champ. Il est mieux paramètre de base de données toocheck hello Bonjour **chaîne de connexion** champ.    
   >
   > ![Création d’une base de données MySQL dans Azure - en cours](./media/store-php-create-mysql-database/connect-db-1-database-name.png)
   >
   >
2. Bonjour tooverify de manière plus rapide que vous avez maintenant accès de MySQL est toouse [la structure de l’authentification de Laravel par défaut](https://laravel.com/docs/5.2/authentication#authentication-quickstart).
   Dans un terminal de ligne de commande hello, exécutez hello suivant les commandes à partir du répertoire racine de votre application Laravel :

         php artisan migrate
         php artisan make:auth

    Hello première commande crée des tables de hello dans Azure en fonction des migrations prédéfinies Bonjour `database/migrations` active et hello deuxième commande squelettes hello itinéraires pour l’authentification et d’inscription des utilisateurs et vues de base.
3. Exécuter le serveur de développement hello maintenant :

        php artisan serve
4. Dans le navigateur de hello, accédez toohttp://localhost:8000 et inscrire un nouvel utilisateur, comme indiqué :

    ![Se connecter tooMySQL de base de données dans Azure - inscription de l’utilisateur](./media/store-php-create-mysql-database/connect-db-2-development-server.png)

    Suivez l’inscription de hello UI invite hello terminée. Une fois l’inscription terminée, vous serez connecté.

    ![Se connecter tooMySQL de base de données dans Azure - inscription de l’utilisateur](./media/store-php-create-mysql-database/connect-db-3-registered-user.png)

    Vous développez votre application sur la base de données MySQL hello dans Azure maintenant.
5. Maintenant, vous devez simplement tooreplicate votre `.env` paramètres tooyour Azure web app. Exécutez hello suivant des commandes CLI d’Azure :

        azure site appsetting add DB_CONNECTION=mysql
        azure site appsetting add DB_HOST=<HOSTNAME_from_properties_blade>
        azure site appsetting add DB_PORT=<PORT_from_properties_blade>
        azure site appsetting add DB_DATABASE=<Database_param_from_CONNECTION_INFO_from_properties_blade>
        azure site appsetting add DB_USERNAME=<USERNAME_from_properties_blade>
        azure site appsetting add DB_PASSWORD=<PASSWORD_from_properties_blade>

6. Ensuite, validez et envoyez les modifications locales hello tooAzure apportées précédemment lors de l’exécution `php artisan make:auth`.

        git add .
        git commit -m "scaffold auth views and routes"
        git push azure master
7. Parcourir toohello Azure web app.

        azure site browse
8. Connectez-vous en utilisant les informations d’identification de l’utilisateur hello que vous avez créé précédemment.

    ![Se connecter tooMySQL de base de données dans Azure - parcourir l’application web tooAzure](./media/store-php-create-mysql-database/connect-db-4-browse-azure-webapp.png)

    Une fois que vous vous connectez, vous devez voir l’écran de post connexion convivial hello.

    ![Se connecter tooMySQL de base de données dans Azure - connecté](./media/store-php-create-mysql-database/connect-db-5-logged-in.png)

    Félicitations, votre application web PHP dans Azure a désormais accès aux données à partir de votre base de données MySQL.

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations, consultez hello [centre de développement PHP](/develop/php/).
