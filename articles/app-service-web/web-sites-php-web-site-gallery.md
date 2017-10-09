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
# <a name="create-a-wordpress-web-app-in-azure-app-service"></a>Créer une application web WordPress dans Azure App Service
[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

Ce didacticiel montre comment toodeploy un blog WordPress de site à partir de hello Azure Marketplace.

Lorsque vous avez terminé le didacticiel de hello vous avez votre propre site blog WordPress et en cours d’exécution dans le cloud de hello.

![Site WordPress](./media/web-sites-php-web-site-gallery/wpdashboard.png)

Vous apprendrez ce qui suit :

* Comment toofind un modèle d’application Bonjour Azure Marketplace.
* Comment toocreate une application web dans Azure App Service qui est basé sur le modèle de hello.
* Comment tooconfigure les paramètres de Service d’applications Azure pour hello nouveau web app et la base de données.

Bonjour Azure Marketplace met à disposition un large éventail d’applications web populaires développé par Microsoft, des entreprises tierces et initiatives des logiciels open source. Hello web applications reposent sur un large éventail d’infrastructures connues, telles que [PHP](/develop/nodejs/) dans cet exemple WordPress, [.NET](/develop/net/), [Node.js](/develop/nodejs/), [Java](/develop/java/), et [Python](/develop/python/), tooname quelques. une application web à partir de hello Azure Marketplace hello uniquement navigateur hello que vous utilisez pour hello logiciels dont vous avez besoin de toocreate [Azure Portal](https://portal.azure.com/). 

site WordPress Hello que vous déployez dans ce didacticiel utilise MySQL pour la base de données hello. Si vous souhaitez utiliser tooinstead base de données SQL pour la base de données hello, consultez [Nami du projet](http://projectnami.org/). **Projet Nami** est également disponible via hello Marketplace.

> [!NOTE]
> toocomplete ce didacticiel, vous avez besoin d’un compte Microsoft Azure. Si vous ne possédez pas de compte, vous pouvez [activer les avantages de votre abonnement Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F) ou [obtenir un essai gratuit](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).
> 
> Si vous souhaitez tooget démarré avec le Service d’application Azure avant de vous inscrivez pour un compte Azure, accédez trop[Service d’applications essayez](https://azure.microsoft.com/try/app-service/). Là, vous pouvez créer immédiatement une application de départ temporaire dans App Service. Aucune carte de crédit n’est requise ni aucun engagement.
> 
> 

## <a name="select-wordpress-and-configure-for-azure-app-service"></a>Sélectionner WordPress et configurer pour Azure App Service
1. Connectez-vous à toohello [Azure Portal](https://portal.azure.com/).
2. Cliquez sur **Nouveau**.
   
    ![Création][5]
3. Recherchez **WordPress**, puis cliquez sur **WordPress**. Si vous le souhaitez toouse base de données SQL au lieu de MySQL, recherchez **Nami du projet**.
   
    ![WordPress dans la liste][7]
4. Après avoir lu la description hello de hello WordPress application, cliquez sur **créer**.
   
    ![Créer](./media/web-sites-php-web-site-gallery/create.png)
5. Entrez un nom pour l’application web de hello dans hello **application Web** boîte.
   
    Ce nom doit être unique dans le domaine azurewebsites.net de hello car hello les URL de l’application web hello est {nom}. azurewebsites.net. Si le nom que vous entrez hello n’est pas unique, un point d’exclamation rouge apparaît dans la zone de texte hello.
6. Si vous avez plusieurs abonnements, choisissez hello celui que vous voulez toouse. 
7. Sélectionnez un **Groupe de ressources** ou créez-en un.
   
    Pour plus d’informations sur les groupes de ressources, consultez [Vue d’ensemble d’Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).
8. Sélectionnez un **plan App Service/emplacement** ou créez-en un.
   
    Pour plus d’informations sur les plans App Service, consultez [Présentation des plans d’Azure App Service](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)    
9. Cliquez sur **base de données**, puis dans hello **nouvelle base de données MySQL** panneau fournir des valeurs de hello requis pour la configuration de votre base de données MySQL.
   
    a. Entrez un nouveau nom ou laissez le nom par défaut de hello.
   
    b. Laissez hello **Type de base de données** défini trop**partagé**.
   
    c. Choisissez hello même emplacement que celui que vous hello choisi pour l’application web de hello.
   
    d. Sélectionnez un niveau tarifaire. Le niveau Mercure (gratuit avec connexions autorisées et espace disque minimum) convient parfaitement pour ce didacticiel.
10. Bonjour **nouvelle base de données MySQL** panneau, cliquez sur **OK**. 
11. Bonjour **WordPress** panneau, acceptez les conditions juridiques hello, puis cliquez sur **créer**. 
    
     ![Configurer une application web](./media/web-sites-php-web-site-gallery/configure.png)
    
     Azure App Service crée hello web app, généralement en moins d’une minute. Vous pouvez surveiller la progression de hello en cliquant sur icône de cloche hello haut hello de page du portail hello.
    
     ![Indicateur de progression](./media/web-sites-php-web-site-gallery/progress.png)

## <a name="launch-and-manage-your-wordpress-web-app"></a>Lancer et gérer l’application web WordPress
1. Après la création d’application web hello, naviguer dans le groupe de ressources de toohello hello portail Azure dans lequel vous avez créé l’application hello, et vous pouvez voir hello web app et la base de données hello.
   
    Bonjour ressource supplémentaire avec une icône d’ampoule hello est [Application Insights](/services/application-insights/), qui fournit des services de surveillance pour votre application web.
2. Bonjour **groupe de ressources** panneau, cliquez sur la ligne de hello web app.
   
    ![Configurer une application web](./media/web-sites-php-web-site-gallery/resourcegroup.png)
3. Dans le panneau de l’application hello Web, cliquez sur **Parcourir**.
   
    ![URL du site][browse]
4. Bonjour WordPress **Bienvenue** page, entrez les informations de configuration hello requises par WordPress, puis cliquez sur **WordPress d’installer**.
   
    ![Configurer WordPress](./media/web-sites-php-web-site-gallery/wpconfigure.png)
5. Connectez-vous à l’aide des informations d’identification hello vous avez créé sur hello **Bienvenue** page.  
6. La page de tableau de bord de votre site s’ouvre.    
   
    ![Site WordPress](./media/web-sites-php-web-site-gallery/wpdashboard.png)

## <a name="next-steps"></a>Étapes suivantes
Vous avez vu comment toocreate et déployer une application web PHP à partir de la galerie de hello. Pour plus d’informations sur l’utilisation de PHP dans Azure, consultez hello [centre de développement PHP](/develop/php/).

Pour plus d’informations sur la façon toowork avec les applications de Service Web App, consultez les liens de hello sur hello à gauche de la page hello (pour les fenêtres du navigateur large) ou en hello haut hello (pour les fenêtres du navigateur étroit). 

## <a name="whats-changed"></a>Changements apportés
* Pour une modification de toohello guide à partir de sites Web tooApp Service, consultez [Azure App Service et son impact sur les Services Azure existants](http://go.microsoft.com/fwlink/?LinkId=529714).

[5]: ./media/web-sites-php-web-site-gallery/startmarketplace.png
[7]: ./media/web-sites-php-web-site-gallery/search-web-app.png
[browse]: ./media/web-sites-php-web-site-gallery/browse-web.png
