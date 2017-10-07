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
# <a name="deploy-an-umbraco-web-app-in-hello-azure-portal-in-five-minutes"></a>Déployer une application web de Umbraco Bonjour Azure portal dans les cinq minutes

Ce didacticiel vous aide à déployer n [Umbraco](https://our.umbraco.org/) web application trop[Azure App Service](../app-service/app-service-value-prop-what-is.md) en minutes.

![Application Umbraco](./media/app-service-web-get-started-dotnet-portal/defaultpage.png)

## <a name="prerequisites"></a>Composants requis
Vous devez avoir un compte Microsoft Azure. Si vous n’avez pas de compte, vous pouvez [vous inscrire pour un essai gratuit](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) ou [activer les avantages de votre abonnement Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).

> [!NOTE]
> Vous pouvez [essayer App Service](https://azure.microsoft.com/try/app-service/) sans compte Azure. Créer une application de démarrage et de le manipuler pour les horaires de tooan--aucune carte de crédit requis, aucune des engagements.
> 
> 

## <a name="deploy-hello-aspnet-app"></a>Déploiement d’une application ASP.NET de hello
1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).

2. Ouvrez [https://portal.azure.com/#create/umbracoorg.UmbracoCMS](https://portal.azure.com/#create/umbracoorg.UmbracoCMS).

    Ce lien est un raccourci tooimmediately configurer une nouvelle application Umbraco Bonjour portail Azure.

3. Sous **Nom de l’application**, entrez un nom d’application web. Vous verrez une coche verte dans la zone de hello si le nom de hello est unique dans hello `azurewebsites.net` domaine.
   
5. Dans **groupe de ressources**, cliquez sur **nouvel** toocreate une nouvelle [groupe de ressources](../azure-resource-manager/resource-group-overview.md), puis attribuez-lui un nom.

7. Cliquez sur **Plan App Service/Emplacement** > **Créer**. Configurer hello [plan App Service](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) comme indiqué :

    - Dans **plan App Service**, nom de type hello souhaité.
    - Dans **emplacement**, choisissez un emplacement toohost votre plan.
    - Cliquez sur **Niveau de tarification**, puis sélectionnez **F1 gratuit** ou un autre niveau qui vous convient, puis cliquez sur **Sélectionner**.
    - Cliquez sur **OK**.

    Votre configuration Umbraco CMS doit maintenant ressembler à hello suivant capture d’écran :

    ![Configuration en cours - première configuration Umbraco dans Azure App Service](./media/app-service-web-get-started-dotnet-portal/configure-in-progress.png)

12. Cliquez sur **SQL Database** > **Créer une base de données**. Configurer hello de base de données SQL comme indiqué :

    - Sous **Nom**, entrez un nom, tel que **myDB**.
    - Cliquez sur **Niveau de tarification**, puis sélectionnez **F gratuit** ou un autre niveau qui vous convient, puis cliquez sur **Sélectionner**.
    - Cliquez sur **Serveur cible** > **Créer un serveur**. Configurer le serveur de base de données hello comme indiqué :

        - Sous **Nom du serveur**, entrez un nom pour le serveur. Vous verrez une coche verte dans la zone de hello si le nom de hello est unique dans hello `.database.windows.net` domaine.
        - Dans **ouverture de session de serveur admin**, vous le souhaitez hello de type nom d’utilisateur administrateur.
        - Dans **mot de passe** et **confirmer le mot de passe**, mot de passe de type hello souhaité.
        - Dans l’emplacement, sélectionnez hello même emplacement que vous utilisez pour l’application web de hello.
        - Assurez-vous que **server d’Autoriser les services azure tooaccess** est sélectionnée.
        - Cliquez sur **Sélectionner**.
    
    - Cliquez sur **Sélectionner**.

13. Cliquez sur **paramètres de l’application Web**, spécifiez le nom d’utilisateur de base de données hello et le mot de passe, puis cliquez sur **OK**.

    Votre configuration Umbraco CMS doit maintenant ressembler à hello suivant capture d’écran :

    ![Configuration terminée - première configuration Umbraco dans Azure App Service](./media/app-service-web-get-started-dotnet-portal/configure-complete.png)

14. Cliquez sur **Create**.
    
    À présent, Azure crée votre application Umbraco en fonction de votre configuration. Vous devriez voir le message **Le déploiement a commencé**.

    ![Déploiement réussi - première configuration Umbraco dans Azure App Service](./media/app-service-web-get-started-dotnet-portal/deployment-started.png)
   
## <a name="launch-and-manage-your-umrbaco-web-app"></a>Lancer et gérer votre application web Umbraco

Une autre notification s’affiche quand Azure termine le déploiement de l’application.

![Déploiement réussi - première configuration Umbraco dans Azure App Service](./media/app-service-web-get-started-dotnet-portal/deployment-succeeded.png)

1. Cliquez sur hello notification. Si vous l’avez manqué, vous pouvez toujours y accéder en cliquant sur la cloche de notification hello (![ctiver Notification - première Umbraco dans Azure App Service](./media/app-service-web-get-started-dotnet-portal/notification.png)).

    Vous devriez maintenant voir le [panneau](../azure-resource-manager/resource-group-portal.md#manage-resources) de gestion de votre application web (*panneau* : page de portail qui s’ouvre horizontalement).

3. Dans hello en haut de page de vue d’ensemble de hello, cliquez sur **Parcourir**.
   
    ![Parcourir - première configuration Umbraco dans Azure App Service](./media/app-service-web-get-started-dotnet-portal/browse.png)

    Maintenant vous voyez hello Umbraco **Bienvenue** page. Configurer l’installation d’Umbraco hello et commencez la lecture avec lui.

    ![Configuration Umbraco - première configuration Umbraco dans Azure App Service](./media/app-service-web-get-started-dotnet-portal/umbraco-config.png)
    
## <a name="next-steps"></a>Étapes suivantes
* [Déployer un tooAzure d’application ASP.NET web Service d’application, à l’aide de Visual Studio](app-service-web-get-started-dotnet.md) -Découvrez comment toocreate une nouvelle application web Azure à partir de Visual Studio, à l’aide de l’une des hello inclus les modèles d’application.
* [Déployer votre tooAzure de code du Service d’applications](web-sites-deploy.md)-Découvrez comment toodeploy à partir de FTP ou à partir de la source de contrôler les référentiels.
* [Ajouter des fonctionnalités tooyour première application web](app-service-web-get-started-2.md) -se toohello de votre application Azure ensuite au niveau. Authentifiez vos utilisateurs. Faites évoluer sa capacité en fonction de la demande. Configurez des alertes de performance. Tout cela en seulement quelques clics.
