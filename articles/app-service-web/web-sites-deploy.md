---
title: "Déploiement de votre application dans Azure App Service | Microsoft Docs"
description: "Apprendre à déployer votre application sur Azure App Service"
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: f1464f71-2624-400e-86a2-e687e385804f
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/05/2017
ms.author: cephalin
ms.openlocfilehash: f41be4e00a9250b07ca260c2858e5fc45143f746
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-your-app-to-azure-app-service"></a>Déploiement de votre application dans Azure App Service
Cet article vous aidera à déterminer la meilleure solution pour déployer les fichiers de votre application web, un serveur d’application mobile ou une application API sur [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714), puis de vous orienter vers des articles et des blocs contenant des informations sur les procédures spécifiques à votre option préférée.

## <a name="overview"></a>Vue d’ensemble du déploiement d’Azure App Service
Azure App Service gère l'infrastructure d'application pour vous (ASP.NET, PHP, Node.js, etc.). Certaines infrastructures sont activées par défaut tandis que d’autres, comme Java et Python, peuvent nécessiter une simple configuration avec coche pour l’activer. En outre, vous pouvez personnaliser votre infrastructure d’application, notamment la version de PHP ou le nombre de bits de votre runtime. Pour plus d’informations, consultez [Configurer votre application dans Azure App Service](web-sites-configure.md).

Comme vous n’avez pas à vous soucier du serveur web ou de l’infrastructure d’application, le déploiement de votre application sur App Service consiste à déployer votre code, les fichiers binaires, les fichiers de contenu et leur structure de répertoire respective sur l’annuaire [**/site/wwwroot** dans Azure](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure) (ou le répertoire **/site/wwwroot/App_Data/Jobs/** pour les tâches web). App Service prend en charge trois processus de déploiement distincts. Toutes les méthodes de déploiement décrites dans cet article utilisent l’un des processus suivants : 

* [FTP ou FTPS](https://en.wikipedia.org/wiki/File_Transfer_Protocol) : utilisez votre outil compatible FTP ou FTPS favori pour déplacer vos fichiers vers Azure, de [FileZilla](https://filezilla-project.org) à des IDE complets comme [NetBeans](https://netbeans.org). Il s’agit d’un processus de téléchargement de fichier au sens strict. Aucun service supplémentaire n’est fourni par le Service d’application, notamment le contrôle de version, la gestion de structure de fichiers, etc. 
* [Kudu (Git/Mercurial ou OneDrive/Dropbox))](https://github.com/projectkudu/kudu/wiki/Deployment) : Kudu est le [moteur de déploiement](https://github.com/projectkudu/kudu/wiki) dans App Service. Placez votre code directement dans Kudu depuis n’importe quel référentiel. Kudu offre également des services ajoutés à chaque fois que le code lui est transmis, notamment la gestion de version, la restauration de package, MSBuild et des [web hooks](https://github.com/projectkudu/kudu/wiki/Web-hooks) pour un déploiement continu et d’autres tâches Automation. Le moteur de déploiement Kudu prend en charge 3 différents types de sources de déploiement :   
  
  * Synchronisation de contenu depuis OneDrive et Dropbox   
  * Déploiement continu basé sur référentiel avec synchronisation automatique à partir de GitHub, Bitbucket et Visual Studio Team Services  
  * Déploiement basé sur référentiel avec synchronisation manuelle à partir de Git local  
* [Web Deploy](http://www.iis.net/learn/publish/using-web-deploy/introduction-to-web-deploy) : déployez le code sur App Service directement à partir de vos outils Microsoft favoris comme Visual Studio, en utilisant le même outil qui automatise le déploiement sur des serveurs IIS. Cet outil prend en charge le déploiement différentiel, la création de base de données, les transformations de chaînes de connexion, etc. Web Deploy diffère de Kudu parce que les fichiers binaires d’application sont générés avant d’être déployés vers Azure. Comme FTP, aucun service supplémentaire n’est fourni par le service d’application.

Les outils de développement web populaires prennent en charge un ou plusieurs de ces processus de déploiement. L’outil que vous choisissez détermine les processus de déploiement que vous pouvez exploiter, la fonctionnalité DevOps réelle à votre disposition dépend de la combinaison du processus de déploiement et les outils spécifiques que vous choisissez. Par exemple, si vous effectuez le déploiement Web à partir de [Visual Studio avec Azure SDK](#vspros), même si vous n’obtenez pas d’automatisation de la part de Kudu, vous obtenez une restauration de package et l’automatisation MSBuild dans Visual Studio. 

> [!NOTE]
> Ces processus de déploiement [n’approvisionnent pas réellement les ressources Azure](../azure-resource-manager/resource-group-template-deploy-portal.md) dont votre application peut avoir besoin. Toutefois, la plupart des articles sur les procédures montrent comment approvisionner l’application ET déployer votre code dessus de bout en bout. Vous trouverez également des options supplémentaires pour l’approvisionnement des ressources Azure dans la section [Automatiser le déploiement à l’aide des outils de ligne de commande](#automate) .
> 
> 

## <a name="ftp"></a>Déployer manuellement en chargeant des fichiers avec FTP
Si vous êtes habitué à copier manuellement votre contenu web sur un serveur web, vous pouvez utiliser un utilitaire [FTP](http://en.wikipedia.org/wiki/File_Transfer_Protocol) pour copier des fichiers, notamment l’Explorateur Windows ou [FileZilla](https://filezilla-project.org/).

Les avantages de la copie manuelle de fichiers sont :

* la simplicité d’utilisation d’outils FTP familiers. 
* vous savez exactement où vont vos fichiers.
* la sécurité ajoutée avec FTPS.

Les inconvénients de la copie manuelle de fichiers sont :

* Vous devez maîtriser le déploiement des fichiers dans les répertoires appropriés dans App Service. 
* Aucun contrôle de version pour la restauration en cas de défaillance.
* Aucun historique de déploiement intégré pour résoudre les problèmes de déploiement.
* Des délais de déploiement potentiellement plus longs car de nombreux outils FTP ne sont pas dotés de la copie différentielle, et se contentent de copier tous les fichiers.  

### <a name="howtoftp"></a>Comment charger des fichiers avec FTP
Le [Portail Azure](https://portal.azure.com) vous permet d’obtenir toutes les informations nécessaires pour vous connecter aux répertoires de votre application à l’aide de FTP ou de FTPS.

* [Déployer votre application dans Azure App Service avec FTP](app-service-deploy-ftp.md)

## <a name="dropbox"></a>Déploiement par synchronisation avec un dossier cloud
Une bonne alternative à la [copie manuelle de fichiers](#ftp) consiste à synchroniser les fichiers et les dossiers avec App Service en utilisant un service de stockage hébergé sur le cloud comme OneDrive et Dropbox. La synchronisation avec un dossier de cloud utilise le processus de Kudu pour le déploiement (voir [Vue d’ensemble du processus de déploiement](#overview)).

Les avantages de la synchronisation avec un dossier cloud sont :

* la simplicité de déploiement. Les services tels que OneDrive et Dropbox fournissent des clients de synchronisation avec un ordinateur de bureau, de sorte que votre répertoire de travail local est également votre répertoire de déploiement.
* le déploiement sur un clic.
* Toutes les fonctionnalités du moteur de déploiement Kudu sont disponibles (par exemple, la restauration de package, l’automatisation).

Les inconvénients de la synchronisation avec un dossier cloud sont :

* Aucun contrôle de version pour la restauration en cas de défaillance.
* Aucun déploiement automatisé, une synchronisation manuelle est nécessaire.

### <a name="howtodropbox"></a>Comment déployer par synchronisation avec un dossier cloud
Dans le [portail Azure](https://portal.azure.com), vous pouvez désigner un dossier pour la synchronisation du contenu dans votre stockage cloud OneDrive ou Dropbox, travailler avec votre code d’application et votre contenu dans ce dossier et à synchroniser avec App Service sur un simple clic.

* [Synchronisez le contenu à partir d’un dossier cloud dans Azure App Service](app-service-deploy-content-sync.md). 

## <a name="continuousdeployment"></a>Déploiement en continu à partir d’un système de contrôle source hébergé sur le cloud
Si votre équipe de développement utilise un service de gestion de code source (SCM) basé sur le cloud comme [Visual Studio Team Services](http://www.visualstudio.com/), [GitHub](https://www.github.com) ou [BitBucket](https://bitbucket.org/), vous pouvez configurer App Service pour l’intégrer à votre référentiel et déployer en continu. 

Les avantages du déploiement à partir d’un système de contrôle source sont :

* Contrôle de version permettant une restauration.
* Possibilité de configurer un déploiement continu pour les référentiels Git (et Mercurial le cas échéant). 
* Le déploiement de branche spécifique permet de déployer différentes branches à différents [emplacements](web-sites-staged-publishing.md).
* Toutes les fonctionnalités du moteur de déploiement Kudu sont disponibles (par exemple, le contrôle de version de déploiement, la restauration, la restauration de package, l’automatisation).

L’inconvénient du déploiement à partir d’un service de contrôle de source de cloud est :

* Implique une certaine connaissance du service SCM respectif.

### <a name="vsts"></a>Comment déployer en continu à partir d’un système de contrôle source hébergé sur le cloud
Dans le [portail Azure](https://portal.azure.com), vous pouvez configurer un déploiement continu à partir de GitHub, Bitbucket et Visual Studio Team Services.

* [Déploiement continu vers Azure App Service](app-service-continuous-deployment.md). 

Pour savoir comment configurer manuellement le déploiement continu à partir d’un référentiel cloud non répertorié par le portail Azure (tel que [GitLab](https://gitlab.com/)), consultez la rubrique sur la[configuration manuelle du déploiement continu](https://github.com/projectkudu/kudu/wiki/Continuous-deployment#setting-up-continuous-deployment-using-manual-steps).

## <a name="localgitdeployment"></a>Déployer à partir de Git local
Si votre équipe de développement utilise un service de gestion du code source local (SCM) basé sur Git, vous pouvez le configurer comme une source de déploiement pour App Service. 

Avantages du déploiement à partir de Git local :

* Contrôle de version permettant une restauration.
* Le déploiement de branche spécifique permet de déployer différentes branches à différents [emplacements](web-sites-staged-publishing.md).
* Toutes les fonctionnalités du moteur de déploiement Kudu sont disponibles (par exemple, le contrôle de version de déploiement, la restauration, la restauration de package, l’automatisation).

Inconvénients du déploiement à partir de Git local :

* Implique une certaine connaissance du système SCM respectif.
* Aucune solution clés en main pour un déploiement continu. 

### <a name="vsts"></a>Comment déployer à partir de Git local
Dans le [portail Azure](https://portal.azure.com), vous pouvez configurer un déploiement Git local.

* [Déploiement Git local vers Azure App Service](app-service-deploy-local-git.md). 
* [Publication vers Web Apps à partir de n’importe quel référentiel git/hg](http://blog.davidebbo.com/2013/04/publishing-to-azure-web-sites-from-any.html)(en anglais).  

## <a name="deploy-using-an-ide"></a>Déployer avec un IDE
Si vous utilisez déjà [Visual Studio](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) avec un [Kit de développement logiciel Azure](https://azure.microsoft.com/downloads/) ou d’autres suites IDE comme [Xcode](https://developer.apple.com/xcode/), [Eclipse](https://www.eclipse.org) et [IntelliJ IDEA](https://www.jetbrains.com/idea/), vous pouvez assurer un déploiement sur Azure directement depuis votre IDE. Cette option est idéale pour un développeur individuel.

Visual Studio prend en charge les trois processus de déploiement (FTP, Git et Web Deploy), selon votre préférence, tandis que les autres IDE peuvent déployer App Service s’ils sont dotés de l’intégration de FTP ou de Git (voir [Vue d’ensemble du déploiement d’Azure App Service](#overview)).

Les avantages du déploiement à l’aide d’un IDE sont :

* La réduction potentielle des outils de votre cycle de vie d’application de bout en bout. Développer, déboguer, suivre et déployer votre application dans Azure sans sortir de votre IDE. 

Les inconvénients du déploiement à l’aide d’un IDE sont les suivants :

* Une complexité accrue des outils.
* Nécessite toujours un système de contrôle de code source en cas de projet d’équipe.

<a name="vspros"></a> Voici d’autres avantages du déploiement à l’aide de Visual Studio avec le SDK Azure :

* Le SDK Azure favorise nettement les ressources Azure dans Visual Studio. Créer, supprimer, modifier, démarrer et arrêter les applications, interroger la base de données SQL du serveur principal, déboguer l’application Azure en direct, entre autres. 
* Modification en direct des fichiers de code sur Azure.
* Débogage en direct des applications sur Azure.
* Explorateur Azure intégré.
* Déploiement différentiel uniquement. 

### <a name="vs"></a>Déploiement direct à partir de Visual Studio
* [Prise en main d'Azure et ASP.NET](app-service-web-get-started-dotnet.md). Explique comment créer et déployer un projet Web ASP.NET MVC simple en utilisant Visual Studio et Web Deploy.
* [Déployer des tâches Web à l’aide de Visual Studio](websites-dotnet-deploy-webjobs.md). Explique comment configurer les projets d'application console pour qu'ils se déploient sous forme de tâches web WebJobs.  
* [Déploiement web ASP.NET en utilisant Visual Studio](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/introduction). Une série de didacticiels en 12 parties présentant un ensemble de tâches de déploiement plus complet que le reste de cette liste. Certaines fonctionnalités de déploiement Azure ont été ajoutées depuis la rédaction de ce didacticiel. Cependant, les notes ajoutées par la suite expliquent les éléments manquants.
* [Déploiement d'un site Web ASP.NET dans Azure avec Visual Studio 2012 directement depuis un référentiel Git](http://www.dotnetcurry.com/ShowArticle.aspx?ID=881). Montre comment déployer un projet Web ASP.NET dans Visual Studio, en utilisant le plug-in Git pour valider le code sur Git et connecter Azure au référentiel Git. À partir de Visual Studio 2013, la prise en charge Git est intégrée et ne nécessite pas l’installation d’un plug-in.

### <a name="aztk"></a>Déploiement à l’aide des boîtes à outils Azure pour Eclipse et IntelliJ IDEA
Microsoft permet de déployer des applications web sur Azure directement à partir d’Eclipse et d’IntelliJ via la [boîte à outils Azure pour Eclipse](../azure-toolkit-for-eclipse.md) et la [boîte à outils Azure pour IntelliJ](../azure-toolkit-for-intellij.md). Les didacticiels suivants illustrent les étapes impliquées dans le déploiement d’une simple application web « Hello World » sur Azure à l’aide de l’IDE :

* [Créer une application web « Hello World » pour Azure dans Eclipse](app-service-web-eclipse-create-hello-world-web-app.md). Ce didacticiel vous montre comment utiliser le Kit de ressources Azure pour Eclipse pour créer une application web Hello World pour Azure.
* [Créer une application web « Hello World » pour Azure dans IntelliJ](app-service-web-intellij-create-hello-world-web-app.md). Ce didacticiel vous montre comment utiliser le Kit de ressources Azure pour Eclipse pour créer une application web Hello World pour Azure.

## <a name="automate"></a>Automatiser le déploiement à l’aide d’outils en ligne de commande
Si vous préférez utiliser le terminal de ligne de commande comme environnement de développement, vous pouvez exécuter des tâches de déploiement pour votre application App Service en utilisant des outils de ligne de commande. 

Les avantages du déploiement à l’aide d’outils en ligne de commande sont :

* L’utilisation de scénarios de déploiement sur la base d’un script.
* L’intégration de l’approvisionnement des ressources Azure et du déploiement de code.
* Le déploiement du déploiement Azure dans des scripts d’intégration en continu existants.

Les inconvénients du déploiement à l’aide d’outils en ligne de commande sont :

* Une difficulté accrue pour les développeurs qui préfèrent l’interface utilisateur graphique.

### <a name="automatehow"></a>Comment automatiser le déploiement avec des outils en ligne de commande

Consultez la page [Automatiser le déploiement de votre application Azure avec les outils en ligne de commande](app-service-deploy-command-line.md) pour obtenir la liste des outils en ligne de commande et des liens vers des didacticiels. 

## <a name="nextsteps"></a>Étapes suivantes
Dans certains cas, vous souhaiterez probablement pouvoir basculer facilement entre une version intermédiaire et de production de votre application. Pour plus d’informations, consultez [Configurer des environnements intermédiaires pour les applications Web dans Azure App Service](web-sites-staged-publishing.md).

Posséder un programme de sauvegarde et de restauration établi représente une partie essentielle de tout flux de travail de déploiement. Pour plus d’informations sur la fonctionnalité de sauvegarde et de restauration d’App Service, consultez [Sauvegarder une application web dans Azure App Service](web-sites-backup.md).  

Pour plus d’informations sur l’utilisation du contrôle d’accès en fonction du rôle Azure afin de gérer l’accès au déploiement App Service, consultez [RBAC and Web App Publishing](https://azure.microsoft.com/blog/2015/01/05/rbac-and-azure-websites-publishing/)(RBAC et publication Web Apps).

