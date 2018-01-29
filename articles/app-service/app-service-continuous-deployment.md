---
title: "Déploiement continu vers Azure App Service | Microsoft Docs"
description: "Découvrez comment activer le déploiement continu vers Azure App Service"
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
ms.openlocfilehash: ef5924607868bcb3dc35e279539b78d5a0e17c1a
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2017
---
# <a name="continuous-deployment-to-azure-app-service"></a>Déploiement continu vers Azure App Service
Ce didacticiel vous montre comment configurer un flux de travail de déploiement continu pour votre application [Azure Web Apps](app-service-web-overview.md) . L’intégration d’App Service à BitBucket, GitHub et [Visual Studio Team Services (VSTS)](https://www.visualstudio.com/team-services/) permet un flux de travail de déploiement continu au cours duquel Azure extrait les mises à jour les plus récentes de votre projet publié sur l’un de ces services. Le déploiement continu est une option intéressante pour les projets auxquels plusieurs contributions fréquentes sont intégrées.

Pour savoir comment configurer manuellement le déploiement continu à partir d’un dépôt cloud non répertorié par le portail Azure (tel que [GitLab](https://gitlab.com/)), consultez la rubrique sur la[configuration manuelle du déploiement continu](https://github.com/projectkudu/kudu/wiki/Continuous-deployment#setting-up-continuous-deployment-using-manual-steps).

## <a name="overview"></a>Activer le déploiement continu
Pour activer le déploiement continu,

1. Publiez le contenu de votre application dans le dépôt qui sera utilisé pour le déploiement continu.  
    Pour plus d’informations sur la publication de votre projet sur ces services, consultez [Création d’un dépôt (GitHub)], [Création d’un dépôt (BitBucket)] et [Prise en main de VSTS].
2. Dans le panneau de menu de votre application au sein du [Portail Azure], cliquez sur **DÉPLOIEMENT DES APPLICATIONS > Options de déploiement**. Cliquez sur **Choisir une source**, puis sélectionnez la source de déploiement.  
   
    ![](./media/app-service-continuous-deployment/cd_options.png)
   
   > [!NOTE]
   > Pour configurer un compte VSTS pour un déploiement App Service, consultez ce [didacticiel](https://github.com/projectkudu/kudu/wiki/Setting-up-a-VSTS-account-so-it-can-deploy-to-a-Web-App).
   > 
   > 
3. Effectuez le workflow d’autorisation.
4. Dans le panneau **Source du déploiement**, sélectionnez le projet et la branche à partir desquels effectuer le déploiement. Quand vous avez terminé, cliquez sur **OK**.
   
    ![](./media/app-service-continuous-deployment/github_option.png)
   
   > [!NOTE]
   > Lors de l’activation du déploiement continu avec GitHub ou BitBucket, les projets publics et privés sont tous deux affichés.
   > 
   > 
   
    App Service crée une association avec le dépôt sélectionné, extrait les fichiers à partir de la branche spécifiée et conserve un clone de votre dépôt pour votre application App Service. Quand vous configurez le déploiement continu VSTS à partir du portail Azure, l’intégration utilise le [moteur de déploiement Kudu](https://github.com/projectkudu/kudu/wiki) d’App Service, qui automatise les tâches de génération et de déploiement avec chaque `git push`. Il n’est pas nécessaire de configurer séparément le déploiement continu dans VSTS. À l’issue de cette procédure, le panneau **Options de déploiement** de l’application affiche un déploiement actif qui indique la réussite du déploiement.
5. Pour vérifier que l’application a bien été déployée, cliquez sur **l’URL** en haut du panneau de l’application dans le portail Azure.
6. Pour vérifier que le déploiement continu s’effectue à partir du dépôt de votre choix, envoyez une modification vers le dépôt par le biais d’une transmission de type push. Votre application doit se mettre à jour pour prendre en compte les modifications, peu de temps après la transmission de type push vers le dépôt. Vous pouvez vérifier que la mise à jour a été récupérée dans le panneau **Options de déploiement** de votre application.

## <a name="VSsolution"></a>Déploiement continu avec une solution Visual Studio
La transmission de type push d’une solution Visual Studio vers Azure App Service est aussi simple que celle d’un fichier index.html. Le processus de déploiement App Service simplifie tous les détails, notamment la restauration des dépendances NuGet et la génération des fichiers binaires de l’application. Vous pouvez suivre les meilleures pratiques de contrôle de code source pour la maintenance du code seulement dans votre dépôt Git et laisser le déploiement App Service s’occuper du reste.

Les étapes pour envoyer votre solution Visual Studio vers App Service sont les mêmes que celles de la [section précédente](#overview), à condition de configurer votre solution et votre dépôt de la façon suivante :

* Utilisez l’option de contrôle de code source Visual Studio pour générer un fichier `.gitignore` comme dans l’image ci-dessous ou ajoutez manuellement un fichier `.gitignore` à la racine du dépôt avec un contenu similaire à cet [exemple .gitignore](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).
  
  ![](./media/app-service-continuous-deployment/VS_source_control.png)
* Ajoutez l’arborescence des répertoires de toute la solution à votre dépôt, avec le fichier .sln dans la racine du dépôt.

Une fois que vous avez configuré votre dépôt comme indiqué, ainsi que votre application dans Azure pour la publication en continu depuis l’un des dépôts Git en ligne, vous pouvez développer votre application ASP.NET localement dans Visual Studio et déployer en continu votre code, en envoyant les modifications apportées à votre dépôt Git en ligne par une transmission de type push.

## <a name="disableCD"></a>Désactiver le déploiement continu
Pour désactiver le déploiement continu :

1. Dans le panneau de menu de votre application au sein du [Portail Azure], cliquez sur **DÉPLOIEMENT DES APPLICATIONS > Options de déploiement**. Ensuite, cliquez sur **Déconnexion** dans le panneau **Options de déploiement**.
   
    ![](./media/app-service-continuous-deployment/cd_disconnect.png)
2. Après avoir répondu **Oui** au message de confirmation, vous pouvez revenir au panneau de votre application et cliquer sur **DÉPLOIEMENT D’APPLICATIONS > Options de déploiement** si vous voulez configurer la publication à partir d’une autre source.

## <a name="additional-resources"></a>Ressources supplémentaires
* [How to investigate common issues with continuous deployment (Examen des problèmes courants liés au déploiement continu)](https://github.com/projectkudu/kudu/wiki/Investigating-continuous-deployment)
* [Comment utiliser PowerShell pour Azure]
* [Utilisation des outils en ligne de commande Azure pour Mac et Linux]
* [Documentation Git]
* [Project Kudu](https://github.com/projectkudu/kudu/wiki)
* [Générer automatiquement un pipeline CI/CD à l’aide d’Azure pour déployer une application ASP.NET 4](https://www.visualstudio.com/docs/build/get-started/aspnet-4-ci-cd-azure-automatic)

> [!NOTE]
> Si vous voulez vous familiariser avec Azure App Service avant d’ouvrir un compte Azure, accédez à la page [Essayer App Service](https://azure.microsoft.com/try/app-service/), où vous pourrez créer immédiatement une application web temporaire dans App Service. Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.
> 
> 

[Portail Azure]: https://portal.azure.com
[VSTS Portal]: https://www.visualstudio.com/en-us/products/visual-studio-team-services-vs.aspx
[Installing Git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
[Comment utiliser PowerShell pour Azure]: /powershell/azureps-cmdlets-docs
[Utilisation des outils en ligne de commande Azure pour Mac et Linux]:../cli-install-nodejs.md
[Documentation Git]: http://git-scm.com/documentation

[Création d’un dépôt (GitHub)]: https://help.github.com/articles/create-a-repo
[Création d’un dépôt (BitBucket)]: https://confluence.atlassian.com/display/BITBUCKET/Create+an+Account+and+a+Git+Repo
[Prise en main de VSTS]: https://www.visualstudio.com/docs/vsts-tfs-overview
