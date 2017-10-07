---
title: aaaCreate une application web ASP.NET Core Visual Studio Code
description: "Ce didacticiel illustre comment toocreate un noyau ASP.NET web application à l’aide de Visual Studio Code."
services: app-service\web
documentationcenter: .net
author: erikre
manager: erikre
editor: jimbe
ms.assetid: 877bff08-9ef7-405a-a1ca-1194f33c55f2
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 02/26/2016
ms.author: cephalin
ms.openlocfilehash: 1c18c94984d71e88d2a5b792d68cb1c81e4a96d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-aspnet-core-web-app-in-visual-studio-code"></a>Créer une application web ASP.NET Core dans Visual Studio Code
## <a name="overview"></a>Vue d'ensemble
Ce didacticiel vous montre comment toocreate une ASP.NET Core web à l’aide de l’application [Visual Studio Code (Visual Studio Code)](http://code.visualstudio.com//Docs/whyvscode) et déployez-le trop[Azure App Service](../app-service/app-service-value-prop-what-is.md). 

> [!NOTE]
> Bien que cet article fait référence à des applications de tooweb, elle s’applique également tooAPI applications et des applications mobiles. 
> 
> 

ASP.NET Core est une refonte importante d’ASP.NET. ASP.NET Core est un nouveau framework open source et interplateforme qui vous permet de créer des applications web modernes basées sur le cloud à l’aide de .NET. Pour plus d’informations, consultez [Introduction tooASP.NET Core](http://docs.asp.net/latest/conceptual-overview/aspnet.html). Pour plus d'informations sur les applications Web Azure App Service, consultez la [Vue d'ensemble de Web Apps](app-service-web-overview.md).

[!INCLUDE [app-service-web-try-app-service.md](../../includes/app-service-web-try-app-service.md)]

## <a name="prerequisites"></a>Composants requis
* Installation de [VS Code](http://code.visualstudio.com/Docs/setup).
* Installation de Git - vous pouvez l’installer depuis l’un de ces emplacements : [Chocolatey](https://chocolatey.org/packages/git) ou [git-scm.com](http://git-scm.com/downloads). Si vous êtes tooGit nouveau, choisissez [git-scm.com](http://git-scm.com/downloads) et l’option hello trop**utiliser Git à partir de hello invite de commandes Windows**. Une fois que vous installez Git, vous devez également e-mail et le nom d’utilisateur tooset hello Git comme il est requis plus loin dans le didacticiel de hello (lorsque vous effectuez une validation à partir de Code de Visual Studio).  

## <a name="install-aspnet-core"></a>Installer ASP.NET Core
ASP.NET Core est une pile .NET lean conçue pour créer des applications web et cloud modernes capables de s’exécuter sur OS X, Linux et Windows. Il a été construit à partir de hello tooprovide d’arrière-plan une infrastructure de développement optimisé pour les applications qui sont soit cloud toohello déployé ou exécutés localement. Elle inclut des composants modulaires associés à des frais généraux réduits. Ainsi, vous bénéficiez d’une certaine flexibilité lors de la création de vos solutions.

Ce didacticiel est conçu tooget que vous avez démarré la création d’applications avec les dernières versions de développement hello de ASP.NET Core. Hello, suivant les instructions est tooWindows spécifique. Pour obtenir des instructions d’installation sur OS X, Linux et Windows, consultez [Bien démarrer avec ASP.NET Core](https://docs.microsoft.com/aspnet/core/getting-started). 


> [!NOTE]
> Pour obtenir des instructions d’installation plus détaillées pour OS X, Linux et Windows, consultez [Installation d’ASP.NET Core](https://code.visualstudio.com/Docs/ASPnet5#_installing-aspnet-5-and-dnx). 
> 
> 

## <a name="create-hello-web-app"></a>Créer une application web de hello
Cette section vous montre comment tooscaffold une nouvelle application ASP.NET web application à l’aide d’outil de .NET CLI hello. 

1. Entrez hello qui suit à l’invite de commandes toocreate hello projet dossier et une vue de structure hello application hello.
   
```terminal
mkdir SampleWebApp
cd SampleWebApp
dotnet new mvc
```
![CLI dotnet - Générateur ASP.NET Core](./media/web-sites-create-web-app-using-vscode/dotnetcore-mvc-01.png)

2. toorestore hello NuGet packages requis, exécutez hello de commande suivante :
   
    ```terminal
    dotnet restore
    ```

## <a name="run-hello-web-app-locally"></a>Exécuter l’application hello web localement
Maintenant que vous avez créé des hello web app et de récupérer tous les packages NuGet hello application hello, vous pouvez exécuter l’application hello web localement.

1. Exécutez l’application hello (hello `dotnet run` commande générerez une application hello lorsqu’il est à jour) :
    ```terminal
    dotnet run
    ```
2. Ouvrez un navigateur et accédez toohello suivant l’URL.
   
    **http://localhost:5000**
   
    page par défaut de Hello de hello web app s’affiche comme suit.
   
    ![Application Web locale dans un navigateur](./media/web-sites-create-web-app-using-vscode/08-web-app.png)
3. Fermez votre navigateur. Bonjour **fenêtre commande**, appuyez sur **Ctrl + C** tooshut application hello et fermer hello **fenêtre commande**. 

## <a name="create-a-web-app-in-hello-azure-portal"></a>Créer une application web Bonjour portail Azure
Hello suit vous guide dans la création d’une application web Bonjour portail Azure.

1. Connectez-vous à toohello [Azure Portal](https://portal.azure.com).
2. Cliquez sur **nouveau** à hello haut à gauche du portail de hello.
3. Cliquez sur **Applications web > Application web**.
   
    ![Nouvelle application Web Azure](./media/web-sites-create-web-app-using-vscode/09-azure-newwebapp.png)
4. Entrez une valeur pour **Nom**, par exemple **SampleWebAppDemo**. Notez que ce nom doit toobe unique, et le portail de hello qui appliquera lorsque vous essayez de nom de hello tooenter. Par conséquent, si vous sélectionnez une entrée une valeur différente, vous devez toosubstitute cette valeur pour chaque occurrence de **SampleWebAppDemo** que vous voyez dans ce didacticiel. 
5. Sélectionnez un **plan App Service** existant ou créez-en un. Si vous créez un plan, sélectionnez hello niveau tarifaire, emplacement et autres options. Pour plus d’informations sur les plans de Service d’applications, consultez l’article hello, [vue d’ensemble approfondie des plans de Service d’applications Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).
   
    ![Panneau Nouvelle application Web Azure](./media/web-sites-create-web-app-using-vscode/10-azure-newappblade.png)
6. Cliquez sur **Create**.
   
    ![Panneau Application Web](./media/web-sites-create-web-app-using-vscode/11-azure-webappblade.png)

## <a name="enable-git-publishing-for-hello-new-web-app"></a>Activer la publication Git de l’application web hello
GIT est un système de contrôle de version distribuée que vous pouvez utiliser toodeploy de votre application web de Service d’applications Azure. Vous allez stocker le code hello que vous écrivez pour votre application web dans un référentiel Git local et que vous déploierez votre tooAzure code en appuyant sur le référentiel distant de tooa.   

1. Ouvrez une session sur hello [Azure Portal](https://portal.azure.com).
2. Cliquez sur **Parcourir**.
3. Cliquez sur **Web Apps** tooview une liste d’applications web de hello associés à votre abonnement Azure.
4. Sélectionnez l’application web hello que vous avez créé dans ce didacticiel.
5. Dans le panneau de l’application hello web, cliquez sur **paramètres** > **déploiement continu**. 
   
    ![Hôte d’application Web Azure](./media/web-sites-create-web-app-using-vscode/14-azure-deployment.png)
6. Cliquez sur **Choisir la source > Référentiel Git local**.
7. Cliquez sur **OK**.
   
    ![Référentiel Git local dans Microsoft Azure](./media/web-sites-create-web-app-using-vscode/15-azure-localrepository.png)
8. Si vous n'avez pas précédemment configuré les informations d'identification de déploiement pour la publication d'une application Web ou d'une autre application App Service, configurez-les maintenant :
   
   * Cliquez sur **Paramètres** > **Informations d’identification de déploiement**. Hello **définir les informations d’identification de déploiement** panneau s’affiche.
   * Créez un nom d'utilisateur et un mot de passe.  Vous aurez besoin de ce mot de passe lorsque vous configurerez Git.
   * Cliquez sur **Save**.
9. Dans le panneau de l’application web, cliquez sur **Paramètres > Propriétés**. URL de Hello du référentiel Git distant hello que vous allez déployer toois figurant sous **URL GIT**.
10. Hello de copie **URL GIT** valeur pour une utilisation ultérieure dans le didacticiel de hello.
    
    ![URL Git de Microsoft Azure](./media/web-sites-create-web-app-using-vscode/17-azure-giturl.png)

## <a name="publish-your-web-app-tooazure-app-service"></a>Publier votre tooAzure d’application web du Service d’applications
Dans cette section, vous créez un référentiel Git local et push à partir de ce toodeploy tooAzure de référentiel votre tooAzure d’application web.

1. Dans le Code de Visual Studio, sélectionnez hello **Git** option dans la barre de navigation gauche hello.
   
    ![Icône Git dans VS Code](./media/web-sites-create-web-app-using-vscode/git-icon.png)
2. Sélectionnez **référentiel git de Initialize** toomake que votre espace de travail est sous contrôle de code source git. 
   
    ![Initialiser Git](./media/web-sites-create-web-app-using-vscode/19-initgit.png)
3. Ouvrez hello fenêtre de commande et modifiez le répertoire de toohello de répertoires de votre application web. Ensuite, entrez hello de commande suivante :
   
        git config core.autocrlf false
   
    Cette commande empêche un problème lié au texte impliquant des terminaisons CRLF et des terminaisons LF.
4. Dans Visual Studio Code, ajoutez un message de validation, puis cliquez sur hello **validation tous les** icône de coche.
   
    ![Git - valider tout ](./media/web-sites-create-web-app-using-vscode/20-git-commit.png)
5. Une fois Git a terminé le traitement, vous verrez qu’il n’y a aucun fichier répertorié dans la fenêtre de Git hello sous **modifications**. 
   
    ![Git - aucune modification](./media/web-sites-create-web-app-using-vscode/no-changes.png)
6. Modifiez toohello arrière fenêtre de commande où invite de commandes hello pointe toohello répertoire où se trouve votre application web.
7. Créer une référence à distance pour pousser des mises à jour tooyour web app à l’aide de hello URL Git (numéro se termine par « .git ») que vous avez copiée précédemment.
   
        git remote add azure [URL for remote repository]
8. Configurer Git toosave vos informations d’identification localement afin qu’ils seront les commandes de push tooyour ajoutée automatiquement générées à partir de Code de Visual Studio.
   
        git config credential.helper store
9. Push tooAzure de vos modifications en entrant hello commande suivante. Cette tooAzure par émission de données initiale, vous serez en mesure de toodo par émission de données hello toutes les commandes à partir de Code de Visual Studio. 
   
        git push -u azure master
   
    Vous êtes invité au mot de passe hello créé précédemment dans Azure. **Remarque : votre mot de passe ne sera pas visible.**
   
    sortie de Hello de hello au-dessus de commande se termine par un message que le déploiement a réussi.
   
        remote: Deployment successful.
        toohttps://user@testsite.scm.azurewebsites.net/testsite.git
        [new branch]      master -> master

> [!NOTE]
> Si vous apportez des modifications tooyour application, vous pouvez republier directement dans le Code de Visual Studio à l’aide d’une fonctionnalité intégrée Git hello en sélectionnant hello **valider tous les** option suivie hello **Push** option. Vous trouverez hello **Push** option disponible dans toohello suivant du menu déroulant hello **valider tous les** et **Actualiser** boutons.
> 
> 

Si vous devez toocollaborate sur un projet, vous devez envisager de pousser tooGitHub entre en exécutant un push tooAzure.

## <a name="run-hello-app-in-azure"></a>Exécutez l’application hello dans Azure
Maintenant que vous avez déployé votre application web, nous allons exécuter application hello tandis que hébergée dans Azure. 

Cette opération peut être réalisée de deux manières :

* Ouvrez un navigateur et entrez le nom hello de votre application web comme suit.   
  
        http://SampleWebAppDemo.azurewebsites.net
* Dans hello portail Azure, recherchez le panneau de l’application hello web pour votre application web, puis cliquez sur **Parcourir** tooview votre application 
* dans votre navigateur par défaut.

![Application Web Azure](./media/web-sites-create-web-app-using-vscode/21-azurewebapp.png)

## <a name="summary"></a>Résumé
Dans ce didacticiel, vous avez appris comment toocreate une application web dans le Code de Visual Studio et déployez-le tooAzure. Pour plus d’informations sur le Code de Visual Studio, consultez l’article hello, [pourquoi Visual Studio Code ?](https://code.visualstudio.com/Docs/) Pour plus d’informations sur les applications web App Service, consultez [Vue d’ensemble des applications web](app-service-web-overview.md). 

