---
title: "aaaDeploy votre tooAzure d’application du Service d’applications | Documents Microsoft"
description: "Découvrez comment toodeploy votre tooAzure d’application du Service d’applications."
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
ms.openlocfilehash: 5c84e4ca502874209d750c94efeb86a59aa71a48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-app-tooazure-app-service"></a>Déployer votre tooAzure d’application du Service d’applications
Cet article vous aidera à déterminer le hello meilleure option toodeploy hello de fichiers pour votre application web, un principal de l’application mobile ou une application API trop[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)et vous guide ensuite ressources tooappropriate avec tooyour spécifique d’instructions option recommandée.

## <a name="overview"></a>Vue d’ensemble du déploiement d’Azure App Service
Azure App Service conserve l’infrastructure d’application hello pour vous (ASP.NET, PHP, Node.js, etc.). Certaines infrastructures sont activées par défaut tandis que d’autres, comme Java et Python, peut-être un tooenable de configuration simple coche il. En outre, vous pouvez personnaliser votre infrastructure d’application, telles que la version de PHP hello ou nombre de bits hello votre runtime. Pour plus d’informations, consultez [Configurer votre application dans Azure App Service](web-sites-configure.md).

Étant donné que vous n’avez pas tooworry sur l’infrastructure de serveur ou une application hello web, déploiement de votre application de tooApp Service consiste à déployer votre code, les fichiers binaires, les fichiers de contenu et leur structure de répertoire correspondant, toohello [   **/site /wwwroot** active](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure) dans Azure (ou hello **/site/wwwroot/App_Data/tâches/** répertoire pour les tâches Web). App Service prend en charge trois processus de déploiement distincts. Toutes les méthodes de déploiement hello dans cet article utilisent hello processus : 

* [FTP ou FTPS](https://en.wikipedia.org/wiki/File_Transfer_Protocol): utilisez vos favoris FTP ou FTPS activé outil toomove tooAzure de vos fichiers, à partir de [FileZilla](https://filezilla-project.org) toofull complet l’IDE comme [NetBeans](https://netbeans.org). Il s’agit d’un processus de téléchargement de fichier au sens strict. Aucun service supplémentaire n’est fourni par le Service d’application, notamment le contrôle de version, la gestion de structure de fichiers, etc. 
* [Kudu (Git/Mercurial ou OneDrive/Dropbox)](https://github.com/projectkudu/kudu/wiki/Deployment): Kudu est hello [moteur de déploiement](https://github.com/projectkudu/kudu/wiki) dans le Service d’applications. Push tooKudu de votre code directement à partir d’un référentiel. Kudu offre également des services ajoutés chaque code tooit, y compris le contrôle de version, la restauration des packages, MSBuild, et [web hooks](https://github.com/projectkudu/kudu/wiki/Web-hooks) pour un déploiement continu et d’autres tâches d’automatisation. moteur de déploiement Hello Kudu prend en charge 3 différents types de sources de déploiement :   
  
  * Synchronisation de contenu depuis OneDrive et Dropbox   
  * Déploiement continu basé sur référentiel avec synchronisation automatique à partir de GitHub, Bitbucket et Visual Studio Team Services  
  * Déploiement basé sur référentiel avec synchronisation manuelle à partir de Git local  
* [Web Deploy](http://www.iis.net/learn/publish/using-web-deploy/introduction-to-web-deploy): déployer code tooApp Service directement à partir de vos favoris Microsoft outils, tels que Visual Studio à l’aide de hello même outils qui automatise les serveurs tooIIS de déploiement. Cet outil prend en charge le déploiement différentiel, la création de base de données, les transformations de chaînes de connexion, etc. Web Deploy diffère de Kudu application binaires sont générés avant d’être déployée tooAzure. TooFTP similaire, aucun des services supplémentaires ne sont fournies par Service d’applications.

Les outils de développement web populaires prennent en charge un ou plusieurs de ces processus de déploiement. Tandis que hello outil que vous choisissez détermine les processus de déploiement hello vous pouvez tirer parti, hello fonctionnalité DevOps réelle à votre disposition dépend combinaison hello hello du processus de déploiement et hello outils spécifiques vous choisissez. Par exemple, si vous effectuez le déploiement Web à partir de [Visual Studio avec Azure SDK](#vspros), même si vous n’obtenez pas d’automatisation de la part de Kudu, vous obtenez une restauration de package et l’automatisation MSBuild dans Visual Studio. 

> [!NOTE]
> Ces processus de déploiement ne [configurer hello ressources Azure](../azure-resource-manager/resource-group-template-deploy-portal.md) que votre application peut avoir besoin. Toutefois, la plupart des hello lié procédure-tooarticles vous montrent comment tooprovision hello application et comment déployer votre code tooit de bout en bout. Vous trouverez également des options supplémentaires pour l’approvisionnement des ressources Azure Bonjour [automatiser le déploiement à l’aide des outils de ligne de commande](#automate) section.
> 
> 

## <a name="ftp"></a>Déployer manuellement en chargeant des fichiers avec FTP
Si vous avez utilisé toomanually copie de votre serveur web de tooa contenu web, vous pouvez utiliser un [FTP](http://en.wikipedia.org/wiki/File_Transfer_Protocol) fichiers toocopy de l’utilitaire, telles que l’Explorateur Windows ou [FileZilla](https://filezilla-project.org/).

les professionnels de l’Hello copier manuellement les fichiers sont les suivantes :

* la simplicité d’utilisation d’outils FTP familiers. 
* vous savez exactement où vont vos fichiers.
* la sécurité ajoutée avec FTPS.

inconvénients Hello copier manuellement les fichiers sont les suivantes :

* Avoir tooknow comment toodeploy toohello correct des répertoires de fichiers dans le Service d’applications. 
* Aucun contrôle de version pour la restauration en cas de défaillance.
* Aucun historique de déploiement intégré pour résoudre les problèmes de déploiement.
* Déploiement potentiel de long délai d’attente, car de nombreux outils FTP ne diff seule copie et simplement copier tous les fichiers hello.  

### <a name="howtoftp"></a>Fonctionnement des fichiers de tooupload avec FTP
Hello [portail Azure](https://portal.azure.com) vous donne toutes les informations de hello vous avez besoin de répertoires de l’application tooconnect tooyour à l’aide de FTP ou FTPS.

* [Déployer votre tooAzure d’application du Service d’applications à l’aide de FTP](app-service-deploy-ftp.md)

## <a name="dropbox"></a>Déploiement par synchronisation avec un dossier cloud
Une bonne approche trop[copiez manuellement les fichiers](#ftp) la synchronisation de fichiers et dossiers tooApp Service à partir d’un service de stockage cloud tels que OneDrive et Dropbox. Synchronisation avec un dossier de cloud utilise des processus de Kudu hello pour le déploiement (voir [vue d’ensemble du processus de déploiement](#overview)).

les professionnels de l’Hello de synchronisation avec un dossier de cloud sont les suivantes :

* la simplicité de déploiement. Les services tels que OneDrive et Dropbox fournissent des clients de synchronisation avec un ordinateur de bureau, de sorte que votre répertoire de travail local est également votre répertoire de déploiement.
* le déploiement sur un clic.
* Toutes les fonctionnalités de moteur de déploiement Kudu hello sont disponible (par exemple, la restauration des packages, automation).

inconvénients Hello de synchronisation avec un dossier de cloud sont les suivantes :

* Aucun contrôle de version pour la restauration en cas de défaillance.
* Aucun déploiement automatisé, une synchronisation manuelle est nécessaire.

### <a name="howtodropbox"></a>Comment toodeploy par la synchronisation avec un dossier de cloud
Bonjour [Azure Portal](https://portal.azure.com), vous pouvez désigner un dossier pour la synchronisation du contenu dans votre stockage cloud OneDrive ou Dropbox, travailler avec votre code d’application et le contenu dans ce dossier et synchronisation tooApp Service avec hello sur un bouton.

* [Synchroniser le contenu à partir d’un tooAzure de dossier du Service d’applications cloud](app-service-deploy-content-sync.md). 

## <a name="continuousdeployment"></a>Déploiement en continu à partir d’un système de contrôle source hébergé sur le cloud
Si votre équipe de développement utilise un service de gestion (des services SCM) de code source basée sur le cloud comme [Visual Studio Team Services](http://www.visualstudio.com/), [GitHub](https://www.github.com), ou [BitBucket](https://bitbucket.org/), vous pouvez configurer des applications Toointegrate votre référentiel de service et les déployer en continu. 

les professionnels de l’Hello du déploiement à partir d’un service de contrôle de source basée sur le cloud sont les suivantes :

* Restauration de tooenable de contrôle de version.
* Déploiement continu de capacité tooconfigure Git (ou Mercurial le cas échéant) référentiels. 
* Déploiement de la branche spécifique, peuvent déployer différentes branches toodifferent [emplacements](web-sites-staged-publishing.md).
* Toutes les fonctionnalités de moteur de déploiement Kudu hello sont disponible (par exemple, contrôle de version de déploiement, la restauration, restauration des packages, automation).

con Hello du déploiement à partir d’un service de contrôle de source basée sur le cloud est la suivante :

* Connaissance de service SCM respectif hello requis.

### <a name="vsts"></a>Comment toodeploy en continu à partir d’une source basée sur le cloud service de contrôle
Bonjour [Azure Portal](https://portal.azure.com), vous pouvez configurer un déploiement continu à partir de GitHub, Bitbucket et Visual Studio Team Services.

* [TooAzure de déploiement d’un Service d’applications](app-service-continuous-deployment.md). 

toofind out comment un déploiement continu tooconfigure manuellement à partir d’un référentiel de cloud ne pas répertorié par hello portail Azure (tels que [GitLab](https://gitlab.com/)), consultez [vous configurez le déploiement continu à l’aide des étapes manuelles](https://github.com/projectkudu/kudu/wiki/Continuous-deployment#setting-up-continuous-deployment-using-manual-steps).

## <a name="localgitdeployment"></a>Déployer à partir de Git local
Si votre équipe de développement utilise un service de gestion (des services SCM) sur site source locale code basé sur Git, vous pouvez configurer cela comme un tooApp de source de déploiement Service. 

Avantages du déploiement à partir de Git local :

* Restauration de tooenable de contrôle de version.
* Déploiement de la branche spécifique, peuvent déployer différentes branches toodifferent [emplacements](web-sites-staged-publishing.md).
* Toutes les fonctionnalités de moteur de déploiement Kudu hello sont disponible (par exemple, contrôle de version de déploiement, la restauration, restauration des packages, automation).

Inconvénients du déploiement à partir de Git local :

* Connaissance de hello SCM système requis.
* Aucune solution clés en main pour un déploiement continu. 

### <a name="vsts"></a>Comment toodeploy à partir de Git local
Bonjour [Azure Portal](https://portal.azure.com), vous pouvez configurer un déploiement Git local.

* [TooAzure déploiement Git local du Service d’applications](app-service-deploy-local-git.md). 
* [Publication d’applications tooWeb à partir de n’importe quel dépôt git/hg](http://blog.davidebbo.com/2013/04/publishing-to-azure-web-sites-from-any.html).  

## <a name="deploy-using-an-ide"></a>Déployer avec un IDE
Si vous utilisez déjà [Visual Studio](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) avec un [Azure SDK](https://azure.microsoft.com/downloads/), ou comme d’autres suites de tests IDE [Xcode](https://developer.apple.com/xcode/), [Eclipse](https://www.eclipse.org), et [ IntelliJ idée](https://www.jetbrains.com/idea/), vous pouvez déployer tooAzure directement à partir de votre IDE. Cette option est idéale pour un développeur individuel.

Visual Studio prend en charge tous les processus de déploiement à trois (FTP, Git et Web Deploy), selon votre préférence, tandis que tooApp Service peut déployer d’autres IDE s’ils ont FTP ou Git de l’intégration (consultez [vue d’ensemble du processus de déploiement](#overview)).

les professionnels de l’Hello de déploiement à l’aide d’un IDE sont les suivantes :

* Potentiellement réduire hello pour les outils de votre cycle de vie des applications de bout en bout. Développer, déboguer, suivre et déployer votre application tooAzure tout cela sans déplacement en dehors de votre interface IDE. 

inconvénients Hello de déploiement à l’aide d’un IDE sont les suivantes :

* Une complexité accrue des outils.
* Nécessite toujours un système de contrôle de code source en cas de projet d’équipe.

<a name="vspros"></a> Voici d’autres avantages du déploiement à l’aide de Visual Studio avec le SDK Azure :

* Le SDK Azure favorise nettement les ressources Azure dans Visual Studio. Créer, supprimer, modifier, démarrer et arrêter des applications, base de données de requête hello principal SQL, débogage en direct hello application Azure et bien plus encore. 
* Modification en direct des fichiers de code sur Azure.
* Débogage en direct des applications sur Azure.
* Explorateur Azure intégré.
* Déploiement différentiel uniquement. 

### <a name="vs"></a>Comment toodeploy directement à partir de Visual Studio
* [Prise en main d'Azure et ASP.NET](app-service-web-get-started-dotnet.md). Comment toocreate et déployer un projet de web ASP.NET MVC simple à l’aide de Visual Studio et Web Deploy.
* [Comment tooDeploy les tâches Web Azure à l’aide de Visual Studio](websites-dotnet-deploy-webjobs.md). Comment tooconfigure Application Console projets afin qu’ils déploient en tant que tâches Web.  
* [Déploiement web ASP.NET en utilisant Visual Studio](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/introduction). Une série de didacticiels 12-partie qui couvre une plage plus complète des tâches de déploiement que d’autres hello dans cette liste. Certaines fonctionnalités de déploiement Azure ont été ajoutées, car les didacticiel hello a été écrit, mais notes ajoutées plus tard expliquent ce qu’est manquant.
* [Déploiement d’un tooAzure de site Web ASP.NET dans Visual Studio 2012 à partir d’un référentiel Git directement](http://www.dotnetcurry.com/ShowArticle.aspx?ID=881). Explique comment toodeploy un site web ASP.NET du projet dans Visual Studio, à l’aide de tooGit de code hello hello Git toocommit plug-in et de connexion du référentiel Git de toohello Azure. À partir de Visual Studio 2013, la prise en charge Git est intégrée et ne nécessite pas l’installation d’un plug-in.

### <a name="aztk"></a>À l’aide de toodeploy comment hello des boîtes à outils Azure pour Eclipse et IntelliJ idée
Microsoft rend possible toodeploy tooAzure de Web Apps directement à partir d’Eclipse et IntelliJ via hello [boîte à outils Azure pour Eclipse](../azure-toolkit-for-eclipse.md) et [Azure Toolkit pour IntelliJ](../azure-toolkit-for-intellij.md). Hello didacticiels suivants illustrent les étapes hello impliqués dans le déploiement tooAzure d’application Web world simple un « Bonjour » à l’aide de l’IDE :

* [Créer une application web « Hello World » pour Azure dans Eclipse](app-service-web-eclipse-create-hello-world-web-app.md). Ce didacticiel vous montre comment toouse hello boîte à outils Azure pour Eclipse toocreate et déployer une application Hello World Web Azure.
* [Créer une application web « Hello World » pour Azure dans IntelliJ](app-service-web-intellij-create-hello-world-web-app.md). Ce didacticiel vous montre comment toouse hello boîte à outils Azure pour IntelliJ toocreate et déployer une application Hello World Web Azure.

## <a name="automate"></a>Automatiser le déploiement à l’aide d’outils en ligne de commande
Si vous préférez terminal de ligne de commande de hello comme environnement de développement hello de choix, vous pouvez générer un script tâches de déploiement pour votre application de Service d’applications à l’aide des outils de ligne de commande. 

Les avantages du déploiement à l’aide d’outils en ligne de commande sont :

* L’utilisation de scénarios de déploiement sur la base d’un script.
* L’intégration de l’approvisionnement des ressources Azure et du déploiement de code.
* Le déploiement du déploiement Azure dans des scripts d’intégration en continu existants.

Les inconvénients du déploiement à l’aide d’outils en ligne de commande sont :

* Une difficulté accrue pour les développeurs qui préfèrent l’interface utilisateur graphique.

### <a name="automatehow"></a>Comment déploiement tooautomate avec les outils de ligne de commande

Consultez [automatiser le déploiement de votre application Azure avec des outils de ligne de commande](app-service-deploy-command-line.md) pour obtenir la liste de tootutorials de liens et les outils de ligne de commande. 

## <a name="nextsteps"></a>Étapes suivantes
Dans certains scénarios, vous souhaiterez basculer en mesure de tooeasily toobe dans les deux sens entre un intermédiaire et une version de production de votre application. Pour plus d’informations, consultez [Configurer des environnements intermédiaires pour les applications Web dans Azure App Service](web-sites-staged-publishing.md).

Posséder un programme de sauvegarde et de restauration établi représente une partie essentielle de tout flux de travail de déploiement. Pour plus d’informations sur hello sauvegarde du Service d’applications et de la fonctionnalité de restauration, consultez [sauvegardes d’applications Web](web-sites-backup.md).  

Pour plus d’informations sur comment toomanage de contrôle d’accès en fonction du rôle de Azure toouse accèdent au déploiement de Service de tooApp, consultez [RBAC et publication de sites Web application](https://azure.microsoft.com/blog/2015/01/05/rbac-and-azure-websites-publishing/).

