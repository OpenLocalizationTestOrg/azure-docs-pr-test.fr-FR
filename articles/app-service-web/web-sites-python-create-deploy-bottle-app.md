---
title: Applications web avec Python avec Bottle dans Azure
description: "Didacticiel expliquant comment exécuter une application web Python dans Azure App Service Web Apps."
services: app-service\web
documentationcenter: python
tags: python
author: huguesv
manager: erikre
editor: 
ms.assetid: 84f043b8-9d05-479f-a9d0-d0d9a32a0bb9
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/19/2016
ms.author: huvalo
ms.openlocfilehash: de5831defc395cd8a4033be8c1fc5dc6cbc9d683
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="creating-web-apps-with-bottle-in-azure"></a>Création d’applications web avec Bottle dans Azure
Ce didacticiel décrit la prise en main de l’exécution de Python dans Azure App Service Web Apps. Web Apps offre un hébergement gratuit limité ainsi qu’un déploiement rapide, et vous permet d’utiliser Python. À mesure que votre application croît, vous pouvez passer à un hébergement payant, et vous pouvez également intégrer l’application à tous les autres services Azure.

Vous allez créer une application web à l’aide de l’infrastructure web Bottle (consultez d’autres versions de ce tutoriel pour [Django](web-sites-python-create-deploy-django-app.md) et [Flask](web-sites-python-create-deploy-flask-app.md)). Vous allez créer l’application web dans Azure Marketplace, configurer le déploiement de Git et cloner le référentiel localement. Vous exécuterez ensuite l’application web localement, vous apporterez des modifications que vous validerez et transmettrez à [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714). Ce didacticiel vous explique comment procéder depuis Windows ou Mac/Linux.

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> Si vous voulez vous familiariser avec Azure App Service avant d’ouvrir un compte Azure, accédez à la page [Essayer App Service](https://azure.microsoft.com/try/app-service/), où vous pourrez créer immédiatement une application web temporaire dans App Service. Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.
> 
> 

## <a name="prerequisites"></a>Configuration requise
* Windows, Mac ou Linux
* Python 2.7 ou 3.4
* setuptools, pip, virtualenv (Python 2.7 uniquement)
* Git
* [Python Tools 2.2 pour Visual Studio][Python Tools 2.2 pour Visual Studio] (PTVS) - Remarque : ceci est facultatif

**Remarque**: la publication de TFS n’est actuellement pas prise en charge pour les projets Python.

### <a name="windows"></a>Windows
Si vous n’avez pas encore installé Python 2.7 ou 3.4 (32 bits), nous vous recommandons d’installer le [Kit de développement logiciel (SDK) Azure pour Python 2.7] ou le [Kit de développement logiciel (SDK) Azure pour Python 3.4] à l’aide de Web Platform Installer. Cette opération installe la version 32 bits de Python, setuptools, pip, virtualenv, etc. (Python 32 bits est installé sur les machines hôtes Azure). Vous pouvez également obtenir Python sur le site [python.org].

Pour Git, nous vous recommandons d’utiliser [Git pour Windows] ou [GitHub pour Windows]. Si vous travaillez avec Visual Studio, vous pouvez utiliser la prise en charge intégrée de Git.

Nous vous recommandons également d’installer [Python Tools 2.2 pour Visual Studio]. Cette opération est facultative, mais si vous avez [Visual Studio], ainsi que la version gratuite Visual Studio Community 2013 ou Visual Studio Express 2013 pour le Web, vous disposerez d’un formidable environnement de développement intégré Python.

### <a name="maclinux"></a>Mac/Linux
Vous devez avoir installé Python et Git, mais vérifiez que vous disposez de Python 2.7 ou 3.4.

## <a name="web-app-creation-on-the-azure-portal"></a>Création d’applications web sur le portail Azure
La première étape consiste à créer l’application web par le biais du [portail Azure](https://portal.azure.com).  

1. Connectez-vous au portail Azure et cliquez sur le bouton **NOUVEAU** dans le coin inférieur gauche. 
2. Dans le champ de recherche, tapez « python ».
3. Dans les résultats de recherche, sélectionnez **Bottle**, puis cliquez sur **Créer**.
4. Configurez la nouvelle application Bottle en créant un nouveau plan App Service et un nouveau groupe de ressources pour celui-ci. Cliquez sur **Créer**.
5. Configurez la publication Git de votre nouvelle application web en suivant les instructions de l’article [Déploiement Git local vers Azure App Service](app-service-deploy-local-git.md).

## <a name="application-overview"></a>Vue d’ensemble de l’application
### <a name="git-repository-contents"></a>Contenu du référentiel Git
Voici une vue d’ensemble des fichiers que vous trouverez dans le référentiel Git initial, que nous allons cloner dans la section suivante.

    \routes.py
    \static\content\
    \static\fonts\
    \static\scripts\
    \views\about.tpl
    \views\contact.tpl
    \views\index.tpl
    \views\layout.tpl

Sources principales de l’application. Correspondent à 3 pages (index, à propos de, contact) dotées d’une mise en page principale.  Le contenu statique et les scripts comprennent bootstrap, jquery, modernizr et respond.

    \app.py

Prise en charge du serveur de développement local. Utilisez cette option pour exécuter l’application localement.

    \BottleWebProject.pyproj
    \BottleWebProject.sln

Fichiers de projet à utiliser avec [Python Tools pour Visual Studio].

    \ptvs_virtualenv_proxy.py

Proxy IIS pour les environnements virtuels et prise en charge du débogage à distance PTVS.

    \requirements.txt

Packages externes requis par cette application. Le script de déploiement installera à l’aide de pip les packages répertoriés dans ce fichier.

    \web.2.7.config
    \web.3.4.config

Fichiers de configuration IIS. Le script de déploiement utilisera le fichier web.x.y.config approprié et le copiera sous le nom web.config.

### <a name="optional-files---customizing-deployment"></a>Fichiers facultatifs - Personnalisation du déploiement
[!INCLUDE [web-sites-python-customizing-deployment](../../includes/web-sites-python-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a>Fichiers facultatifs - Runtime Python
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a>Fichiers supplémentaires sur le serveur
Certains fichiers existent sur le serveur, mais ne sont pas ajoutés au référentiel Git. Ils sont créés par le script de déploiement.

    \web.config

Fichier de configuration IIS. Créé à partir du fichier web.x.y.config lors de chaque déploiement.

    \env\

Environnement virtuel Python. Créé lors du déploiement si aucun environnement virtuel compatible n’existe sur le site.  Les packages répertoriés dans requirements.txt sont installés à l’aide de pip. Si les packages sont déjà installés, pip ignorera l’installation.

Les trois sections suivantes expliquent comment développer des applications web dans trois environnements différents :

* Windows, avec Python Tools pour Visual Studio ;
* Windows, avec la ligne de commande ;
* Mac/Linux, avec la ligne de commande.

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a>Développement d’applications web - Windows - Python Tools pour Visual Studio
### <a name="clone-the-repository"></a>Cloner le référentiel
Commencez par cloner le référentiel à l’aide de l’URL fournie sur le portail Azure. Pour plus d’informations, voir [Déploiement Git local vers Azure App Service](app-service-deploy-local-git.md).

Ouvrez le fichier solution (.sln) inclus dans la racine du référentiel.

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-solution-bottle.png)

### <a name="create-virtual-environment"></a>Créer un environnement virtuel
Nous allons à présent créer un environnement virtuel pour le développement local. Cliquez avec le bouton droit sur **Environnements Python** et sélectionnez **Ajouter un environnement virtuel...**.

* Vérifiez que l’environnement porte le nom `env`.
* Sélectionnez l’interpréteur de base. Veillez à utiliser la même version de Python que celle sélectionnée pour votre application web (dans runtime.txt ou le panneau **Paramètres de l’application** de votre application web dans le portail Azure).
* Vérifiez que l’option permettant de télécharger et d’installer les packages est cochée.

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-add-virtual-env-27.png)

Cliquez sur **Create**. Cette opération créera l’environnement virtuel et installera les dépendances répertoriées dans requirements.txt.

### <a name="run-using-development-server"></a>Exécuter à l’aide d’un serveur de développement
Appuyez sur F5 pour lancer le débogage. Votre navigateur ouvrira automatiquement la page s’exécutant localement.

![](./media/web-sites-python-create-deploy-bottle-app/windows-browser-bottle.png)

Vous pouvez définir des points d’arrêt dans les sources, utiliser les fenêtres de surveillance, etc. Pour plus d’informations sur les différentes fonctionnalités, consultez la [Documentation de Python Tools pour Visual Studio].

### <a name="make-changes"></a>Apporter des modifications
Vous pouvez à présent tenter d’apporter des modifications aux sources de l’application et/ou aux modèles.

Après avoir testé vos modifications, validez-les sur le référentiel Git :

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-commit-bottle.png)

### <a name="install-more-packages"></a>Installer d’autres packages
Votre application peut comporter des dépendances au-delà de Python et de Bottle.

Vous pouvez installer des packages supplémentaires à l’aide de pip. Pour installer un package, cliquez avec le bouton droit sur l’environnement virtuel et sélectionnez **Installer un package Python**.

Par exemple, pour installer le Kit de développement logiciel (SDK) Azure pour Python, qui vous permet d’accéder au stockage Azure, au bus des services et à d’autres services Azure, entrez `azure`:

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-install-package-dialog.png)

Cliquez avec le bouton droit sur l’environnement virtuel et sélectionnez **Générer requirements.txt** pour mettre à jour le fichier requirements.txt.

Puis validez les modifications apportées à requirements.txt dans le référentiel Git.

### <a name="deploy-to-azure"></a>Déployer dans Azure
Pour déclencher un déploiement, cliquez sur **Synchroniser** ou **Push**. La synchronisation effectue à la fois une transmission de type push et une transmission de type pull.

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-git-push.png)

Le premier déploiement mettra un certain temps à s’effectuer, car il créera un environnement virtuel, installera les packages, etc.

Visual Studio n’affiche pas la progression du déploiement. Si vous souhaitez vérifier la sortie, consultez la section [Résolution des problèmes - Déploiement](#troubleshooting-deployment).

Accédez à l’URL Azure pour visualiser les modifications que vous avez apportées.

## <a name="web-app-development---windows---command-line"></a>Développement d’applications web - Windows - Ligne de commande
### <a name="clone-the-repository"></a>Cloner le référentiel
Commencez par cloner le référentiel à l’aide de l’URL fournie sur le portail Azure, puis ajoutez le référentiel Azure en tant que référentiel distant. Pour plus d’informations, voir [Déploiement Git local vers Azure App Service](app-service-deploy-local-git.md).

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a>Créer un environnement virtuel
Nous allons créer un environnement virtuel pour le développement (ne l’ajoutez pas au référentiel). Les environnements virtuels dans Python ne sont pas déplaçables. De ce fait, chaque développeur travaillant sur l’application créera ses propres environnements localement.

Veillez à utiliser la même version de Python que celle sélectionnée pour votre application web (dans runtime.txt ou le panneau Paramètres de l’application de votre application web dans le portail Azure).

Pour Python 2.7 :

    c:\python27\python.exe -m virtualenv env

Pour Python 3.4 :

    c:\python34\python.exe -m venv env

Installez tous les packages externes requis par votre application. Vous pouvez utiliser le fichier requirements.txt à la racine du référentiel pour installer les packages dans votre environnement virtuel :

    env\scripts\pip install -r requirements.txt

### <a name="run-using-development-server"></a>Exécuter à l’aide d’un serveur de développement
Vous pouvez lancer l’application sous un serveur de développement à l’aide de la commande suivante :

    env\scripts\python app.py

La console affichera l’URL et le port que le serveur écoute :

![](./media/web-sites-python-create-deploy-bottle-app/windows-run-local-bottle.png)

Puis ouvrez votre navigateur web en accédant à cette URL.

![](./media/web-sites-python-create-deploy-bottle-app/windows-browser-bottle.png)

### <a name="make-changes"></a>Apporter des modifications
Vous pouvez à présent tenter d’apporter des modifications aux sources de l’application et/ou aux modèles.

Après avoir testé vos modifications, validez-les sur le référentiel Git :

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a>Installer d’autres packages
Votre application peut comporter des dépendances au-delà de Python et de Bottle.

Vous pouvez installer des packages supplémentaires à l’aide de pip. Par exemple, pour installer le Kit de développement logiciel (SDK) Azure pour Python, qui vous permet d’accéder au stockage Azure, au bus des services et à d’autres services Azure, entrez :

    env\scripts\pip install azure

Veillez à mettre à jour requirements.txt :

    env\scripts\pip freeze > requirements.txt

Validez les modifications :

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-to-azure"></a>Déploiement sur Azure
Pour déclencher un déploiement, transmettez les modifications à Azure :

    git push azure master

Vous découvrirez la sortie du script de déploiement, notamment la création de l’environnement virtuel, l’installation des packages et la création du fichier web.config.

Accédez à l’URL Azure pour visualiser les modifications que vous avez apportées.

## <a name="web-app-development---maclinux---command-line"></a>Développement d’applications web - Mac/Linux - Ligne de commande
### <a name="clone-the-repository"></a>Cloner le référentiel
Commencez par cloner le référentiel à l’aide de l’URL fournie sur le portail Azure, puis ajoutez le référentiel Azure en tant que référentiel distant. Pour plus d’informations, voir [Déploiement Git local vers Azure App Service](app-service-deploy-local-git.md).

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a>Créer un environnement virtuel
Nous allons créer un environnement virtuel pour le développement (ne l’ajoutez pas au référentiel). Les environnements virtuels dans Python ne sont pas déplaçables. De ce fait, chaque développeur travaillant sur l’application créera ses propres environnements localement.

Veillez à utiliser la même version de Python que celle sélectionnée pour votre application web (dans runtime.txt ou le panneau Paramètres de l’application de votre application web dans le portail Azure).

Pour Python 2.7 :

    python -m virtualenv env

Pour Python 3.4 :

    python -m venv env
or pyvenv env

Installez tous les packages externes requis par votre application. Vous pouvez utiliser le fichier requirements.txt à la racine du référentiel pour installer les packages dans votre environnement virtuel :

    env/bin/pip install -r requirements.txt

### <a name="run-using-development-server"></a>Exécuter à l’aide d’un serveur de développement
Vous pouvez lancer l’application sous un serveur de développement à l’aide de la commande suivante :

    env/bin/python app.py

La console affichera l’URL et le port que le serveur écoute :

![](./media/web-sites-python-create-deploy-bottle-app/mac-run-local-bottle.png)

Puis ouvrez votre navigateur web en accédant à cette URL.

![](./media/web-sites-python-create-deploy-bottle-app/mac-browser-bottle.png)

### <a name="make-changes"></a>Apporter des modifications
Vous pouvez à présent tenter d’apporter des modifications aux sources de l’application et/ou aux modèles.

Après avoir testé vos modifications, validez-les sur le référentiel Git :

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a>Installer d’autres packages
Votre application peut comporter des dépendances au-delà de Python et de Bottle.

Vous pouvez installer des packages supplémentaires à l’aide de pip. Par exemple, pour installer le Kit de développement logiciel (SDK) Azure pour Python, qui vous permet d’accéder au stockage Azure, au bus des services et à d’autres services Azure, entrez :

    env/bin/pip install azure

Veillez à mettre à jour requirements.txt :

    env/bin/pip freeze > requirements.txt

Validez les modifications :

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-to-azure"></a>Déploiement sur Azure
Pour déclencher un déploiement, transmettez les modifications à Azure :

    git push azure master

Vous découvrirez la sortie du script de déploiement, notamment la création de l’environnement virtuel, l’installation des packages et la création du fichier web.config.

Accédez à l’URL Azure pour visualiser les modifications que vous avez apportées.

## <a name="troubleshooting---package-installation"></a>Résolution des problèmes - Installation des packages
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a>Résolution des problèmes - Environnement virtuel
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur Bottle et Python Tools pour Visual Studio, consultez les liens suivants : 

* [Documentation relative à Bottle]
* [Documentation de Python Tools pour Visual Studio]

Pour obtenir des informations concernant l’utilisation du stockage de tables Azure et MongoDB :

* [Bottle et MongoDB sur Azure avec Python Tools pour Visual Studio]
* [Bottle et stockage de tables Azure sur Azure avec Python pour Visual Studio]

## <a name="whats-changed"></a>Changements apportés
* Pour obtenir un guide présentant les modifications apportées dans le cadre de la transition entre Sites Web et App Service, consultez la page [Azure App Service et les services Azure existants](http://go.microsoft.com/fwlink/?LinkId=529714)

<!--Link references-->
[Bottle et MongoDB sur Azure avec Python Tools pour Visual Studio]: web-sites-python-ptvs-bottle-table-storage.md
[Bottle et stockage de tables Azure sur Azure avec Python pour Visual Studio]: web-sites-python-ptvs-bottle-table-storage.md

<!--External Link references-->
[Kit de développement logiciel (SDK) Azure pour Python 2.7]: http://go.microsoft.com/fwlink/?linkid=254281
[Kit de développement logiciel (SDK) Azure pour Python 3.4]: http://go.microsoft.com/fwlink/?linkid=516990
[python.org]: http://www.python.org/
[Git pour Windows]: http://msysgit.github.io/
[GitHub pour Windows]: https://windows.github.com/
[Python Tools pour Visual Studio]: http://aka.ms/ptvs
[Python Tools 2.2 pour Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Visual Studio]: http://www.visualstudio.com/
[Documentation de Python Tools pour Visual Studio]: http://aka.ms/ptvsdocs 
[Documentation relative à Bottle]: http://bottlepy.org/docs/dev/index.html

