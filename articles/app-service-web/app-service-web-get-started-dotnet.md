---
title: aaaCreate ASP.NET web application dans Azure | Documents Microsoft
description: "Découvrez comment toorun les applications web dans Azure App Service en déployant la valeur par défaut de hello ASP.NET web app."
services: app-service\web
documentationcenter: 
author: cephalin
manager: wpickett
editor: 
ms.assetid: b1e6bd58-48d1-4007-9d6c-53fd6db061e3
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 06/14/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: eec916b3c32b6c8b68083177938c5c822a9782b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-aspnet-web-app-in-azure"></a>Création d’une application web ASP.NET dans Azure

[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) offre un service d’hébergement web hautement évolutif appliquant des mises à jour correctives automatiques.  Ce démarrage rapide montre comment toodeploy votre première application ASP.NET web application tooAzure les applications Web. Lorsque vous aurez terminé, vous disposerez d’un groupe de ressources constitué d’un plan App Service et d’une application web Azure avec une application web déployée.

Regardez les toosee vidéo hello ce démarrage rapide en action, puis suivez hello étapes vous-même toopublish votre première application .NET sur Azure.

> [!VIDEO https://channel9.msdn.com/Shows/Azure-for-NET-Developers/Create-a-NET-app-in-Azure-Quickstart/player]

## <a name="prerequisites"></a>Composants requis

toocomplete ce didacticiel :

* Installer [Visual Studio 2017](https://www.visualstudio.com/downloads/) avec hello suivant les charges de travail :
    - **Développement web et ASP.NET**
    - **Développement Azure**

    ![Développement web et ASP.NET et Développement Azure (sous Web et cloud)](media/app-service-web-tutorial-dotnet-sqldatabase/workloads.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-an-aspnet-web-app"></a>Créez une application web ASP.NET

Dans Visual Studio, créez un projet en sélectionnant **Fichier > Nouveau > Projet**. 

Bonjour **nouveau projet** boîte de dialogue, sélectionnez **Visual c# > Web > ASP.NET Web Application (.NET Framework)**.

Nommez l’application hello _myFirstAzureWebApp_, puis sélectionnez **OK**.
   
![Boîte de dialogue Nouveau projet](./media/app-service-web-get-started-dotnet/new-project.png)

Vous pouvez déployer tout type d’ASP.NET web application tooAzure. Pour ce démarrage rapide, sélectionnez hello **MVC** modèle et assurez-vous que l’authentification est définie trop**aucune authentification**.
      
Sélectionnez **OK**.

![Boîte de dialogue New ASP.NET Project](./media/app-service-web-get-started-dotnet/select-mvc-template.png)

Dans le menu de hello, sélectionnez **Déboguer > Démarrer sans débogage** toorun hello web application localement.

![Exécuter l’application localement](./media/app-service-web-get-started-dotnet/local-web-app.png)

## <a name="publish-tooazure"></a>Publication tooAzure

Bonjour **l’Explorateur de solutions**, avec le bouton hello **myFirstAzureWebApp** de projet et sélectionnez **publier**.

![Publier à partir de l’Explorateur de solutions](./media/app-service-web-get-started-dotnet/solution-explorer-publish.png)

Assurez-vous que **Microsoft Azure App Service** est sélectionné, puis sélectionnez **Publier**.

![Publier à partir de la page de présentation du projet](./media/app-service-web-get-started-dotnet/publish-to-app-service.png)

Cette opération ouvre hello **créer un Service application** boîte de dialogue qui vous permet de créer tous les hello ressources Azure nécessaires toorun hello web d’application ASP.NET dans Azure.

## <a name="sign-in-tooazure"></a>Connectez-vous à tooAzure

Bonjour **créer un Service application** boîte de dialogue, sélectionnez **ajouter un compte**et vous connecter tooyour abonnement Azure. Si vous êtes déjà connecté, compte hello select contenant hello souhaité abonnement à partir de la liste déroulante de hello.

> [!NOTE]
> Si vous êtes déjà connecté, ne sélectionnez pas encore **Créer**.
>
>
   
![Connectez-vous à tooAzure](./media/app-service-web-get-started-dotnet/sign-in-azure.png)

## <a name="create-a-resource-group"></a>Créer un groupe de ressources

[!INCLUDE [resource group intro text](../../includes/resource-group.md)]

Suivant trop**groupe de ressources**, sélectionnez **nouveau**.

Groupe de ressources de nom hello **myResourceGroup** et sélectionnez **OK**.

## <a name="create-an-app-service-plan"></a>Créer un plan App Service

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

Suivant trop**du Plan App Service**, sélectionnez **nouveau**. 

Bonjour **configurer un Plan App Service** boîte de dialogue, utiliser les paramètres de table hello suivant capture d’écran de hello hello.

![Créer un plan App Service](./media/app-service-web-get-started-dotnet/configure-app-service-plan.png)

| Paramètre | Valeur suggérée | Description |
|-|-|-|
|Plan App Service| myAppServicePlan | Nom du plan App Service de hello. |
| Lieu | Europe de l'Ouest | Bonjour centre de données où l’application hello web est hébergée. |
| Taille | Gratuit | Le [niveau tarifaire](https://azure.microsoft.com/pricing/details/app-service/) détermine les fonctionnalités d’hébergement. |

Sélectionnez **OK**.

## <a name="create-and-publish-hello-web-app"></a>Créer et publier l’application web hello

Dans **nom de l’application Web**, tapez un nom d’application unique (les caractères valides sont `a-z`, `0-9`, et `-`), ou acceptez le nom unique est généré automatiquement par un hello. l’URL de l’application web hello Hello est `http://<app_name>.azurewebsites.net`, où `<app_name>` est le nom de votre application web.

Sélectionnez **créer** toostart création hello ressources Azure.

![Configurer le nom de l’application web](./media/app-service-web-get-started-dotnet/web-app-name.png)

Une fois l’Assistant de hello terminé, il publie hello ASP.NET web application tooAzure, et puis lance hello application dans le navigateur par défaut de hello.

![Application web ASP.NET publiée dans Azure](./media/app-service-web-get-started-dotnet/published-azure-web-app.png)

nom de l’application web Hello spécifié dans hello [créer et publier étape](#create-and-publish-the-web-app) est utilisé comme hello préfixe d’URL au format de hello `http://<app_name>.azurewebsites.net`.

Félicitations, votre application web ASP.NET s’exécute en temps réel dans Azure App Service.

## <a name="update-hello-app-and-redeploy"></a>Redéploiement et application hello de mise à jour

À partir de hello **l’Explorateur de solutions**, ouvrez _Views\Home\Index.cshtml_.

Recherche hello `<div class="jumbotron">` HTML balise haut hello et élément tout entier de hello par hello suivant de code :

```HTML
<div class="jumbotron">
    <h1>ASP.NET in Azure!</h1>
    <p class="lead">This is a simple app that we’ve built that demonstrates how toodeploy a .NET app tooAzure App Service.</p>
</div>
```

tooredeploy tooAzure, avec le bouton hello **myFirstAzureWebApp** projet **l’Explorateur de solutions** et sélectionnez **publier**.

Bonjour, une page de publication, sélectionnez **publier**.

Lorsque la publication est terminée, Visual Studio lance une URL toohello du navigateur de l’application web hello.

![Application web ASP.NET mise à jour dans Azure](./media/app-service-web-get-started-dotnet/updated-azure-web-app.png)

## <a name="manage-hello-azure-web-app"></a>Gérer l’application web Azure de hello

Accédez toohello <a href="https://portal.azure.com" target="_blank">portail Azure</a> toomanage hello web app.

Dans le menu de gauche hello, sélectionnez **des Services d’application**, puis sélectionnez le nom hello de votre application web Azure.

![Application de navigation du portail tooAzure web](./media/app-service-web-get-started-dotnet/access-portal.png)

Vous voyez apparaître la page Vue d’ensemble de votre application web. Ici, vous pouvez également des tâches de gestion de base (parcourir, arrêter, démarrer, redémarrer et supprimer des éléments, par exemple). 

![Panneau App Service sur le portail Azure](./media/app-service-web-get-started-dotnet/web-app-blade.png)

menu de gauche Hello fournit différentes pages de configuration de votre application. 

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a>Étapes suivantes

> [!div class="nextstepaction"]
> [ASP.NET avec SQL Database](app-service-web-tutorial-dotnet-sqldatabase.md)
