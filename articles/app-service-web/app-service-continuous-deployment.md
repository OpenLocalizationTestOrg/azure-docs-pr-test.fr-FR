---
title: "aaaContinuous tooAzure de déploiement du Service d’applications | Documents Microsoft"
description: "Découvrez comment tooenable déploiement continu tooAzure du Service d’applications."
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.assetid: 6adb5c84-6cf3-424e-a336-c554f23b4000
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/28/2016
ms.author: dariagrigoriu
ms.openlocfilehash: 62a22cbda354fd5b0a1b9729c8c375408e75049f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-deployment-tooazure-app-service"></a>TooAzure de déploiement continue du Service d’applications
Ce didacticiel vous montre comment tooconfigure un flux de travail de déploiement continu pour votre [Azure App Service] application. Intégration du Service d’applications avec BitBucket, GitHub, et [Visual Studio Team Services (VSTS)](https://www.visualstudio.com/team-services/) permet un continue où Azure extrait dans hello plus récentes des mises à jour à partir de votre projet de workflow de déploiement publié tooone de ces services. Le déploiement continu est une option intéressante pour les projets auxquels plusieurs contributions fréquentes sont intégrées.

toofind out comment un déploiement continu tooconfigure manuellement à partir d’un référentiel de cloud ne pas répertorié par hello portail Azure (tels que [GitLab](https://gitlab.com/)), consultez [vous configurez le déploiement continu à l’aide des étapes manuelles](https://github.com/projectkudu/kudu/wiki/Continuous-deployment#setting-up-continuous-deployment-using-manual-steps).

## <a name="overview"></a>Activer le déploiement continu
déploiement continu tooenable,

1. Publier votre référentiel de contenu toohello d’application qui sera utilisé pour le déploiement continu.  
    Pour plus d’informations sur la publication de vos services de toothese de projet, consultez [créer un référentiel (GitHub)], [créer un référentiel (BitBucket)], et [prise en main VSTS].
2. Dans le panneau de menu de votre application Bonjour [portail Azure], cliquez sur **déploiement d’applications > options de déploiement**. Cliquez sur **choisir la Source de**, puis sélectionnez source du déploiement hello.  
   
    ![](./media/app-service-continuous-deployment/cd_options.png)
   
   > [!NOTE]
   > tooconfigure un compte VSTS pour le déploiement du Service d’applications, consultez ce [didacticiel](https://github.com/projectkudu/kudu/wiki/Setting-up-a-VSTS-account-so-it-can-deploy-to-a-Web-App).
   > 
   > 
3. Flux de travail d’autorisation hello terminée.
4. Bonjour **source du déploiement** panneau, choisissez le projet de hello et créer une branche toodeploy à partir de. Quand vous avez terminé, cliquez sur **OK**.
   
    ![](./media/app-service-continuous-deployment/github_option.png)
   
   > [!NOTE]
   > Lors de l’activation du déploiement continu avec GitHub ou BitBucket, les projets publics et privés sont tous deux affichés.
   > 
   > 
   
    Service d’applications crée une association avec le référentiel sélectionné de hello, extrait les fichiers hello à partir de la branche spécifiée de hello et conserve un clone de votre référentiel pour votre application de Service d’applications. Lorsque vous configurez le déploiement continu VSTS hello portail Azure, l’intégration hello utilise hello du Service d’applications [moteur de déploiement Kudu](https://github.com/projectkudu/kudu/wiki), qui automatise les tâches de génération et de déploiement avec déjà chaque `git push`. Vous n’avez pas besoin de tooseparately définir un déploiement continu dans VSTS. Une fois ce processus terminé, hello **options de déploiement** Panneau de l’application affiche un déploiement actif qui indique le déploiement a réussi.
5. tooverify hello application est déployée avec succès, cliquez sur hello **URL** haut hello du Panneau de l’application hello Bonjour portail Azure.
6. tooverify déploiement continu se produit à partir du référentiel hello de votre choix, transmettre un référentiel de toohello de modification. Votre application doit mettre à jour les modifications de hello tooreflect peu de temps après que le référentiel de toohello hello par émission de données se termine. Vous pouvez vérifier qu’il a tiré mise à jour hello Bonjour **options de déploiement** Panneau de votre application.

## <a name="VSsolution"></a>Déploiement continu avec une solution Visual Studio
En exécutant un push d’un tooAzure de solution Visual Studio du Service d’applications est aussi simple que d’envoyer un fichier index.html simple. Hello, processus de déploiement du Service d’applications rationalise tous les détails de hello, y compris la restauration des dépendances de NuGet et la création de fichiers binaires d’application hello. Vous pouvez suivre les meilleures pratiques de contrôle de code source d’hello de gestion du code uniquement dans votre référentiel Git et permettent de déploiement du Service de l’application reste de hello prennent en charge.

Hello étapes pour pousser votre tooApp de solution Visual Studio Service sont hello même comme hello [section précédente](#overview), à condition que vous configurez votre solution et l’espace de stockage comme suit :

* Utilisez hello Visual Studio source contrôle option toogenerate un `.gitignore` fichier telles que l’image hello ci-dessous ou ajoutez manuellement un `.gitignore` fichier racine du référentiel avec contenu toothis similaire [.gitignore exemple](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).
  
  ![](./media/app-service-continuous-deployment/VS_source_control.png)
* Ajouter le référentiel de la solution entière hello répertoire arborescence tooyour, avec le fichier .sln de hello dans la racine du référentiel hello.

Après avoir configuré votre référentiel comme décrit et configuré votre application dans Azure pour la publication continue à partir d’un des référentiels de Git hello en ligne, vous pouvez développer votre application ASP.NET localement dans Visual Studio et en continu de simplement à déployer votre code en exécutant un push de votre référentiel Git en ligne de modifications tooyour.

## <a name="disableCD"></a>Désactiver le déploiement continu
déploiement continu toodisable,

1. Dans le panneau de menu de votre application Bonjour [portail Azure], cliquez sur **déploiement d’applications > options de déploiement**. Puis cliquez sur **déconnexion** Bonjour **options de déploiement** panneau.
   
    ![](./media/app-service-continuous-deployment/cd_disconnect.png)
2. Après avoir répondu **Oui** toohello message de confirmation, vous pouvez retourner le panneau de l’application tooyour et cliquez sur **déploiement d’applications > options de déploiement** si vous souhaitez que tooset configuration d’une publication à partir d’une autre source.

## <a name="additional-resources"></a>Ressources supplémentaires
* [Comment tooinvestigate commun émet avec un déploiement continu](https://github.com/projectkudu/kudu/wiki/Investigating-continuous-deployment)
* [Comment toouse PowerShell pour Azure]
* [Comment toouse hello des outils de ligne de commande Azure pour Mac et Linux]
* [Documentation Git]
* [Project Kudu](https://github.com/projectkudu/kudu/wiki)
* [Utiliser Azure tooautomatically générer une application toodeploy une ASP.NET 4 du pipeline CI/CD](https://www.visualstudio.com/docs/build/get-started/aspnet-4-ci-cd-azure-automatic)

> [!NOTE]
> Si vous souhaitez tooget démarré avec le Service d’application Azure avant de s’inscrire pour un compte Azure, accédez trop[essayez du Service d’applications](https://azure.microsoft.com/try/app-service/), où vous pouvez créer une application web de courte durée de démarrage immédiatement dans le Service d’applications. Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.
> 
> 

[Azure App Service]: https://azure.microsoft.com/en-us/documentation/articles/app-service-changes-existing-services/
[portail Azure]: https://portal.azure.com
[VSTS Portal]: https://www.visualstudio.com/en-us/products/visual-studio-team-services-vs.aspx
[Installing Git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
[Comment toouse PowerShell pour Azure]: /powershell/azureps-cmdlets-docs
[Comment toouse hello des outils de ligne de commande Azure pour Mac et Linux]:../cli-install-nodejs.md
[Documentation Git]: http://git-scm.com/documentation

[créer un référentiel (GitHub)]: https://help.github.com/articles/create-a-repo
[créer un référentiel (BitBucket)]: https://confluence.atlassian.com/display/BITBUCKET/Create+an+Account+and+a+Git+Repo
[prise en main VSTS]: https://www.visualstudio.com/docs/vsts-tfs-overview
