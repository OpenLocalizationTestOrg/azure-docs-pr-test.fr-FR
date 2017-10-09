---
title: "aaaDeploy tâches Web à l’aide de Visual Studio"
description: "Découvrez comment toodeploy tooAzure de tâches Web Azure App Service Web Apps à l’aide de Visual Studio."
services: app-service
documentationcenter: 
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: a3a9d320-1201-4ac8-9398-b4c9535ba755
ms.service: app-service
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2016
ms.author: glenga
ms.openlocfilehash: 5fc5d9562e8836348f5ab6844fb6c23ff40a321c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-webjobs-using-visual-studio"></a>Déployer des tâches web à l’aide de Visual Studio
## <a name="overview"></a>Vue d'ensemble
Cette rubrique explique comment toouse Visual Studio toodeploy une Application Console de projet application web tooa [du Service d’applications](http://go.microsoft.com/fwlink/?LinkId=529714) comme un [la tâche Web Azure](http://go.microsoft.com/fwlink/?LinkId=390226). Pour plus d’informations sur comment toodeploy tâches Web à l’aide de hello [Azure Portal](https://portal.azure.com), consultez [les tâches en arrière-plan de s’exécuter avec les tâches Web](web-sites-create-web-jobs.md).

Lorsque Visual Studio déploie un projet d'application console compatible avec des tâches web, il exécute deux tâches :

* Exécution de copies des fichiers toohello le dossier approprié dans l’application web hello (*App_Data/tâches/continue* pour les tâches Web continues, *App_Data/tâches/déclenchée* pour les tâches planifiées et à la demande Web).
* Configure [les travaux Azure Scheduler](#scheduler) pour les tâches Web sont toorun planifiée à des moments particuliers. (inutile pour les tâches web continues).

Un projet de tâche Web a hello suivant tooit Ajout d’éléments :

* Hello [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) package NuGet.
* Un fichier [webjob-publish-settings.json](#publishsettings) qui contient des paramètres de déploiement et de planification. 

![Diagramme montrant ce qui est ajouté le déploiement de tooenable tooa application Console comme une tâche Web](./media/websites-dotnet-deploy-webjobs/convert.png)

Vous pouvez ajouter ces tooan éléments existants du projet d’Application Console ou utiliser un modèle de toocreate un nouveau projet d’Application de Console avec les tâches Web. 

Vous pouvez déployer un projet en tant qu’une tâche Web en lui-même, ou lier le projet web de tooa afin qu’il déploie automatiquement chaque fois que vous déployez le projet web de hello. toolink projets, Visual Studio inclut le nom hello du projet de tâches Web compatible hello dans un [webjobs-list.json](#webjobslist) fichier projet web de hello.

![Diagramme montrant le projet de tâche Web liaison tooweb projet](./media/websites-dotnet-deploy-webjobs/link.png)

## <a name="prerequisites"></a>Composants requis
Fonctionnalités de déploiement des tâches Web sont disponibles dans Visual Studio lorsque vous installez hello Azure SDK pour .NET :

* [Kit de développement logiciel (SDK) Azure pour .NET (Visual Studio)](https://azure.microsoft.com/downloads/).

## <a id="convert"></a>Activer le déploiement de tâches web pour un projet d’application de console
Deux options s'offrent à vous :

* [Activation d'un déploiement automatique avec un projet web](#convertlink).
  
    Configurez un projet d'application console existant afin qu'il soit déployé automatiquement sous forme de tâche web lorsque vous déployez un projet web. Utilisez cette option lorsque vous souhaitez toorun votre tâche Web Bonjour même application web dans lequel vous exécutez hello liées d’application web.
* [Activation d'un déploiement sans projet web](#convertnolink).
  
    Configurer un toodeploy de projet Application Console existante comme une tâche Web lui-même, avec aucun projet web ne tooa lien. Utilisez cette option lorsque vous souhaitez toorun une tâche Web dans une application web par lui-même, à aucune application web en cours d’exécution dans l’application web hello. Vous souhaiterez peut-être toodo cela dans commande tooscale en mesure de toobe vos ressources de la tâche Web indépendamment de vos ressources d’application web.

### <a id="convertlink"></a> Activer un déploiement automatique de tâches web avec un projet web
1. Projet de web avec le bouton hello dans **l’Explorateur de solutions**, puis cliquez sur **ajouter** > **projet existant en tant que tâche Web Azure**.
   
    ![Projet existant sous forme de tâche web Azure](./media/websites-dotnet-deploy-webjobs/eawj.png)
   
    Hello [ajouter de la tâche Web Azure](#configure) boîte de dialogue s’affiche.
2. Bonjour **nom du projet** liste déroulante, sélectionnez hello tooadd de projet Application Console comme une tâche Web.
   
    ![Selecting project in Add Azure WebJob dialog](./media/websites-dotnet-deploy-webjobs/aaw1.png)
3. Hello complète [ajouter de la tâche Web Azure](#configure) boîte de dialogue, puis cliquez sur **OK**. 

### <a id="convertnolink"></a> Activer un déploiement de tâches web sans projet web
1. Projet d’Application Console hello avec le bouton droit dans **l’Explorateur de solutions**, puis cliquez sur **publier en tant que tâche Web Azure...** . 
   
    ![Publier sous forme de tâche web Azure](./media/websites-dotnet-deploy-webjobs/paw.png)
   
    Hello [ajouter de la tâche Web Azure](#configure) boîte de dialogue s’affiche, projet hello dans hello **nom du projet** boîte.
2. Hello complète [ajouter de la tâche Web Azure](#configure) boîte de dialogue, puis cliquez sur **OK**.
   
   Hello **publier le site Web** Assistant s’affiche.  Si vous ne souhaitez pas immédiatement toopublish, fermez l’Assistant de hello. paramètres de Hello que vous avez entrées sont enregistrés pour lorsque vous ne souhaitez pas trop[déployer hello projet](#deploy).

## <a id="create"></a>Créer un projet compatible avec les tâches web
toocreate un nouveau projet compatibles sur les tâches Web, vous pouvez utiliser hello Console projet modèle et activer les tâches Web déploiement d’Application comme expliqué dans [hello la section précédente](#convert). En guise d’alternative, vous pouvez utiliser le modèle de nouveau projet hello WebJobs :

* [Utilisez le modèle de nouveau projet de tâches Web de hello pour une tâche Web indépendante](#createnolink)
  
    Créer un projet et configurez-le toodeploy par lui-même en tant qu’une tâche Web, avec aucun projet web ne tooa lien. Utilisez cette option lorsque vous souhaitez toorun une tâche Web dans une application web par lui-même, à aucune application web en cours d’exécution dans l’application web hello. Vous souhaiterez peut-être toodo cela dans commande tooscale en mesure de toobe vos ressources de la tâche Web indépendamment de vos ressources d’application web.
* [Utiliser le modèle de nouveau projet hello tâches Web pour un projet de web de tooa lié de la tâche Web](#createlink)
  
    Créez un projet qui est configuré toodeploy automatiquement comme une tâche Web lorsqu’un projet web Bonjour même solution est déployée. Utilisez cette option lorsque vous souhaitez toorun votre tâche Web Bonjour même application web dans lequel vous exécutez hello liées d’application web.

> [!NOTE]
> modèle de nouveau projet de tâches Web Hello automatiquement installe les packages NuGet et inclut le code dans *Program.cs* pour hello [WebJobs SDK](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/getting-started-with-windows-azure-webjobs). Si vous ne souhaitez pas toouse hello WebJobs SDK, supprimer ou modifier des hello `host.RunAndBlock` instruction *Program.cs*.
> 
> 

### <a id="createnolink"></a>Utilisez le modèle de nouveau projet de tâches Web de hello pour une tâche Web indépendante
1. Cliquez sur **fichier** > **nouveau projet**, puis dans hello **nouveau projet** boîte dialogue, cliquez sur **Cloud**  >   **La tâche Web Azure (.NET Framework)**.
   
    ![New Project dialog showing WebJob template](./media/websites-dotnet-deploy-webjobs/np.png)
2. Suivez les instructions de hello présentées précédemment trop[rendre hello projet d’Application Console à un projet de tâches Web indépendant](#convertnolink).

### <a id="createlink"></a>Utiliser le modèle de nouveau projet hello tâches Web pour un projet de web de tooa lié de la tâche Web
1. Projet de web avec le bouton hello dans **l’Explorateur de solutions**, puis cliquez sur **ajouter** > **nouveau projet de la tâche Web Azure**.
   
    ![New Azure WebJob Project menu entry](./media/websites-dotnet-deploy-webjobs/nawj.png)
   
    Hello [ajouter de la tâche Web Azure](#configure) boîte de dialogue s’affiche.
2. Hello complète [ajouter de la tâche Web Azure](#configure) boîte de dialogue, puis cliquez sur **OK**.

## <a id="configure"></a>boîte de dialogue Ajouter de la tâche Web Azure Hello
Hello **ajouter de la tâche Web Azure** boîte de dialogue vous permet d’entrer le nom de la tâche Web hello et exécutez le paramètre de mode de votre tâche Web. 

![Add Azure WebJob dialog](./media/websites-dotnet-deploy-webjobs/aaw2.png)

champs Hello dans cette boîte de dialogue correspondent toofields sur hello **nouveau travail** boîte de dialogue de hello portail Azure. Pour plus d’informations, consultez [Exécuter des tâches en arrière-plan avec les tâches web](web-sites-create-web-jobs.md).

> [!NOTE]
> * Pour plus d’informations sur le déploiement en ligne de commande, consultez la page [Activation de la ligne de commande ou de la livraison continue de tâches web Azure](https://azure.microsoft.com/blog/2014/08/18/enabling-command-line-or-continuous-delivery-of-azure-webjobs/).
> * Si vous déployez une tâche Web et que vous décidez ensuite de que créer de type hello de toochange de la tâche Web et de redéploiement, vous devez le fichier de toodelete hello settings.json publier des tâches Web. Cela facilitera afficher hello options de publication, vous pouvez modifier le type hello de tâche Web Visual Studio.
> * Si vous déployez une tâche Web et que vous changez ultérieurement hello exécution en mode continu toonon continue, ou vice versa, Visual Studio crée une nouvelle tâche de Web dans Azure lorsque vous redéployez. Si vous modifiez d’autres paramètres de planification, mais le mode de laisser s’exécuter même hello ou basculer entre planifiée et à la demande, mises à jour de Visual Studio hello travail existant plutôt que de créer un nouveau.
> 
> 

## <a id="publishsettings"></a>webjob-publish-settings.json
Lorsque vous configurez une Application Console pour le déploiement des tâches Web, Visual Studio installe hello [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet package et stocke les informations de planification un *settings.json publier la tâche Web*  fichier hello projet *propriétés* dossier du projet de tâches Web hello. Voici un exemple de ce fichier :

        {
          "$schema": "http://schemastore.org/schemas/json/webjob-publish-settings.json",
          "webJobName": "WebJob1",
          "startTime": "null",
          "endTime": "null",
          "jobRecurrenceFrequency": "null",
          "interval": null,
          "runMode": "Continuous"
        }

Vous pouvez modifier ce fichier directement. Visual Studio est doté d'IntelliSense. schéma de fichier Hello est stockée au niveau [http://schemastore.org](http://schemastore.org/schemas/json/webjob-publish-settings.json) et vous pouvez les consulter.  

## <a id="webjobslist"></a>webjobs-list.json
Lorsque vous liez un projet web de tooa compatibles sur les tâches Web de projet, Visual Studio stocke le nom hello du projet de tâches Web hello dans un *webjobs-list.json* fichier de projet hello web *propriétés* dossier. liste de Hello peut contenir plusieurs projets de tâches Web, comme indiqué dans hello l’exemple suivant :

        {
          "$schema": "http://schemastore.org/schemas/json/webjobs-list.json",
          "WebJobs": [
            {
              "filePath": "../ConsoleApplication1/ConsoleApplication1.csproj"
            },
            {
              "filePath": "../WebJob1/WebJob1.csproj"
            }
          ]
        }

Vous pouvez modifier ce fichier directement. Visual Studio est doté d'IntelliSense. schéma de fichier Hello est stockée au niveau [http://schemastore.org](http://schemastore.org/schemas/json/webjobs-list.json) et vous pouvez les consulter.

## <a id="deploy"></a>Déployer un projet WebJobs
Un projet de tâches Web que vous avez lié des projets web de tooa déploie automatiquement avec le projet web de hello. Pour plus d’informations sur le déploiement du projet web, consultez [comment toodeploy tooWeb applications](web-sites-deploy.md).

toodeploy un projet de tâches Web par lui-même, avec le bouton droit de projet hello dans **l’Explorateur de solutions** et cliquez sur **publier en tant que tâche Web Azure...** . 

![Publier sous forme de tâche web Azure](./media/websites-dotnet-deploy-webjobs/paw.png)

Pour une tâche Web indépendante, hello même **publier le site Web** Assistant qui est utilisé pour les projets web s’affiche, mais avec moins toochange de paramètres disponibles.

## <a id="nextsteps"></a>Étapes suivantes
Cet article a expliqué comment toodeploy tâches Web à l’aide de Visual Studio. Pour plus d’informations sur comment toodeploy les tâches Web Azure, consultez [tâches Web Azure - déploiement des ressources - recommandées](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/azure-webjobs-recommended-resources#deploying).

