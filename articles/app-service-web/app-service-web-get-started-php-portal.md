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
# <a name="deploy-a-wordpress-app-in-hello-azure-portal-in-five-minutes"></a>Déployer une application WordPress Bonjour Azure portal dans les cinq minutes

Ce didacticiel vous montre comment toodeploy votre premier [WordPress](https://wordpress.org/) web application trop[Azure App Service](../app-service/app-service-value-prop-what-is.md) en minutes.

![Site WordPress](./media/app-service-web-get-started-php-portal/wpdashboard.png)

## <a name="prerequisites"></a>Composants requis
Vous devez avoir un compte Microsoft Azure. Si vous n’avez pas de compte, vous pouvez [vous inscrire pour un essai gratuit](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) ou [activer les avantages de votre abonnement Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).

> [!NOTE]
> Vous pouvez [essayer App Service](https://azure.microsoft.com/try/app-service/) sans compte Azure. Créer une application de démarrage et de le manipuler pour les horaires de tooan--aucune carte de crédit requis, aucune des engagements.
> 
> 

## <a name="deploy-hello-wordpress-app"></a>Déploiement d’une application de WordPress hello
1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).

2. Ouvrez [https://portal.azure.com/#create/WordPress.WordPress](https://portal.azure.com/#create/WordPress.WordPress).

    Ce lien est un raccourci tooimmediately configurer une nouvelle application WordPress Bonjour portail Azure.

3. Sous **Nom de l’application**, entrez un nom d’application web. Vous verrez une coche verte dans la zone de hello si le nom de hello est unique dans hello `azurewebsites.net` domaine.
   
5. Dans **groupe de ressources**, cliquez sur **nouvel** toocreate une nouvelle [groupe de ressources](../azure-resource-manager/resource-group-overview.md), puis attribuez-lui un nom.

6. Sous **Fournisseur de base de données**, sélectionnez **CleaDB**.

7. Cliquez sur **Plan App Service/Emplacement** > **Créer**. Configurer hello [plan App Service](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) comme indiqué :

    - Dans **plan App Service**, nom de type hello souhaité.
    - Dans **emplacement**, choisissez un emplacement toohost votre plan.
    - Cliquez sur **Niveau de tarification**, puis sélectionnez **F1 gratuit** ou un autre niveau qui vous convient, puis cliquez sur **Sélectionner**.
    - Cliquez sur **OK**.

8. Cliquez sur **Base de données** > **Créer**. Configurer hello de base de données SQL comme indiqué :

    - Sous **Nom de la base de données**, entrez un nom pour la base de données. 
    - Dans **emplacement**, choisissez hello même emplacement que hello plan App Service.
    - Cliquez sur **Niveau de tarification**, puis sélectionnez **Mercury** ou un autre niveau qui vous convient, puis cliquez sur **Sélectionner**.
    - Cliquez sur **Mentions légales** et sur **Acheter**.
    - Cliquez sur **OK**.

9. Cliquez sur **Create**.

    À présent, Azure crée votre application WordPress en fonction de votre configuration. Vous devriez voir le message **Le déploiement a commencé**.

    ![Déploiement commencé - première configuration WordPress dans Azure App Service](./media/app-service-web-get-started-php-portal/deployment-started.png)
   
## <a name="launch-and-manage-your-wordpress-web-app"></a>Lancer et gérer l’application web WordPress

Une autre notification s’affiche quand Azure termine le déploiement de l’application.

![Déploiement réussi - première configuration WordPress dans Azure App Service](./media/app-service-web-get-started-php-portal/deployment-succeeded.png)

1. Cliquez sur hello notification. Si vous l’avez manqué, vous pouvez toujours y accéder en cliquant sur la cloche de notification hello (![ctiver Notification - première WordPress dans Azure App Service](./media/app-service-web-get-started-dotnet-portal/notification.png)).

    Vous devriez maintenant voir le [panneau](../azure-resource-manager/resource-group-portal.md#manage-resources) de gestion de votre application web (*panneau* : page de portail qui s’ouvre horizontalement).

3. Dans hello en haut de page de vue d’ensemble de hello, cliquez sur **Parcourir**.
   
    ![Parcourir - première configuration WordPress dans Azure App Service](./media/app-service-web-get-started-php-portal/browse.png)

    Maintenant vous voyez hello WordPress **Bienvenue** page. Configurer l’installation de WordPress hello et commencez la lecture avec lui.

    ![Configuration de WordPress - première configuration WordPress dans Azure App Service](./media/app-service-web-get-started-php-portal/wordpress-config.png)
    
## <a name="next-steps"></a>Étapes suivantes
* [Créer, configurer et déployer un tooAzure d’application de web Laravel](app-service-web-php-get-started.md) -compétences hello élémentaires vous avez besoin toorun n’importe quelle application web PHP dans Azure, telles que :

    * Créer et configurer des applications dans Azure depuis PowerShell/Bash
    * Définir la version PHP
    * Utiliser un fichier de démarrage qui n’est pas dans le répertoire de l’application hello racine.
    * Activer l’automatisation de Composer
    * Accéder à des variables propres à l’environnement
    * Résoudre les problèmes courants

* [Déployer votre tooAzure de code du Service d’applications](web-sites-deploy.md)-Découvrez comment toodeploy à partir de FTP ou à partir de la source de contrôler les référentiels.
* [Ajouter des fonctionnalités tooyour première application web](app-service-web-get-started-2.md) -se toohello de votre application Azure ensuite au niveau. Authentifiez vos utilisateurs. Faites évoluer sa capacité en fonction de la demande. Configurez des alertes de performance. Tout cela en seulement quelques clics.
