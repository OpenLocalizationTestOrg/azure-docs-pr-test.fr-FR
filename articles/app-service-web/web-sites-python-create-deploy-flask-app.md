---
title: applications web aaaCreating avec ballon dans Azure
description: "Un didacticiel qui vous présente toorunning une application de web Python dans Azure."
services: app-service\web
documentationcenter: python
tags: python
author: huguesv
manager: erikre
editor: 
ms.assetid: b7f4ca3a-0b52-4108-90a7-f7e07ac73da0
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/20/2016
ms.author: huvalo
ms.openlocfilehash: 3362047b3106b4380b5971e47cbd8042d38a792b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-web-apps-with-flask-in-azure"></a>Création d’applications web avec Flask dans Azure
Ce didacticiel décrit comment tooget démarré Python [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).  Web Apps offre un hébergement gratuit limité ainsi qu’un déploiement rapide, et vous permet d’utiliser Python.  Comme votre application se développe, vous pouvez basculer toopaid d’hébergement, et vous pouvez également intégrer avec tous les hello autres services Azure.

Vous allez créer une application à l’aide hello ballon web framework (voir les autres versions de ce didacticiel pour [Django](web-sites-python-create-deploy-django-app.md) et [Bottle](web-sites-python-create-deploy-bottle-app.md)).  Vous crée un site Web de hello à partir de la galerie Azure de hello, configurer le déploiement de Git et cloner le référentiel hello localement.  Puis vous serez exécuté application hello localement, apporter des modifications, validez et envoyez les tooAzure.  Hello didacticiel montre comment toodo à partir de Windows ou Mac/Linux.

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> Si vous souhaitez tooget démarré avec le Service d’application Azure avant de s’inscrire pour un compte Azure, accédez trop[essayez du Service d’applications](https://azure.microsoft.com/try/app-service/), où vous pouvez créer une application web de courte durée de démarrage immédiatement dans le Service d’applications. Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.
> 
> 

## <a name="prerequisites"></a>Configuration requise
* Windows, Mac ou Linux
* Python 2.7 ou 3.4
* setuptools, pip, virtualenv (Python 2.7 uniquement)
* Git
* [Python Tools pour Visual Studio][Python Tools pour Visual Studio] (PTVS) - Remarque : ceci est facultatif

**Remarque**: la publication de TFS n’est actuellement pas prise en charge pour les projets Python.

### <a name="windows"></a>Windows
Si vous n’avez pas encore installé Python 2.7 ou 3.4 (32 bits), nous vous recommandons d’installer le [Kit de développement logiciel (SDK) Azure pour Python 2.7] ou le [Kit de développement logiciel (SDK) Azure pour Python 3.4] à l’aide de Web Platform Installer.  Cela installe la version 32 bits de hello de Python, setuptools, pip, virtualenv, etc. (32 bits Python est ce qui est installé sur les ordinateurs hôte Azure hello).  Vous pouvez également obtenir Python sur le site [python.org].

Pour Git, nous vous recommandons d’utiliser [Git pour Windows] ou [GitHub pour Windows].  Si vous utilisez Visual Studio, vous pouvez utiliser la prise en charge de Git hello intégré.

Nous vous recommandons également d’installer [Python Tools 2.2 pour Visual Studio].  Cette option est facultative, mais si vous avez [Visual Studio], y compris hello libre Visual Studio Community 2013 ou Visual Studio Express 2013 pour le Web, puis vous obtenez ainsi un remarquable IDE Python.

### <a name="maclinux"></a>Mac/Linux
Vous devez avoir installé Python et Git, mais vérifiez que vous disposez de Python 2.7 ou 3.4.

## <a name="web-app-create-on-hello-azure-portal"></a>Application Web créer sur hello portail Azure
première étape de la création de votre application Hello est l’application web via hello toocreate hello [Azure Portal](https://portal.azure.com). 

1. Ouvrez une session hello portail Azure, puis cliquez sur hello **nouveau** bouton hello bas à gauche. 
2. Cliquez sur **web + Mobile**.
3. Dans la zone de recherche de hello, tapez « python ».
4. Dans les résultats de recherche de hello, sélectionnez **ballon**, puis cliquez sur **créer**.
5. Configurer nouveau ballon application hello, telles que la création d’un nouveau plan App Service et un groupe de ressources pour celle-ci. Cliquez sur **Créer**.
6. Configurer la publication Git de votre application web qui vient d’être créé en suivant les instructions de hello sur [tooAzure de déploiement Git Local du Service d’applications](app-service-deploy-local-git.md).

## <a name="application-overview"></a>Vue d’ensemble de l’application
### <a name="git-repository-contents"></a>Contenu du référentiel Git
Voici une vue d’ensemble des fichiers hello que vous trouverez dans le référentiel Git initiale hello, lequel nous allons cloner dans la section suivante de hello.

    \FlaskWebProject\__init__.py
    \FlaskWebProject\views.py
    \FlaskWebProject\static\content\
    \FlaskWebProject\static\fonts\
    \FlaskWebProject\static\scripts\
    \FlaskWebProject\templates\about.html
    \FlaskWebProject\templates\contact.html
    \FlaskWebProject\templates\index.html
    \FlaskWebProject\templates\layout.html

Sources principales pour l’application hello.  Correspondent à 3 pages (index, à propos de, contact) dotées d’une mise en page principale.  Le contenu statique et les scripts comprennent bootstrap, jquery, modernizr et respond.

    \runserver.py

Prise en charge du serveur de développement local. Utilisez cette application de hello toorun localement.

    \FlaskWebProject.pyproj
    \FlaskWebProject.sln

Fichiers de projet à utiliser avec [Python Tools pour Visual Studio].

    \ptvs_virtualenv_proxy.py

Proxy IIS pour les environnements virtuels et prise en charge du débogage à distance PTVS.

    \requirements.txt

Packages externes requis par cette application. script de déploiement Hello sera pip des packages d’installation de hello répertoriés dans ce fichier.

    \web.2.7.config
    \web.3.4.config

Fichiers de configuration IIS.  script de déploiement Hello utilise web.x.y.config approprié de hello et copiez-le en tant que fichier web.config.

### <a name="optional-files---customizing-deployment"></a>Fichiers facultatifs - Personnalisation du déploiement
[!INCLUDE [web-sites-python-customizing-deployment](../../includes/web-sites-python-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a>Fichiers facultatifs - Runtime Python
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a>Fichiers supplémentaires sur le serveur
Certains fichiers existent sur le serveur de hello mais ne sont pas ajoutés de référentiel git de toohello.  Ceux-ci sont créés par le script de déploiement hello.

    \web.config

Fichier de configuration IIS.  Créé à partir du fichier web.x.y.config lors de chaque déploiement.

    \env\

Environnement virtuel Python.  Si un environnement virtuel compatible n’existe pas déjà sur l’application hello, créé au cours du déploiement.  Packages répertoriés dans requirements.txt sont pip installé, mais pip ignorera l’installation si hello packages sont déjà installés.

Hello 3 sections décrivent comment tooproceed avec hello web sous 3 différents environnements le développement d’applications :

* Windows, avec Python Tools pour Visual Studio ;
* Windows, avec la ligne de commande ;
* Mac/Linux, avec la ligne de commande.

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a>Développement d’applications web - Windows - Python Tools pour Visual Studio
### <a name="clone-hello-repository"></a>Référentiel de hello clone
Tout d’abord, cloner le référentiel de hello à l’aide des URL hello fournie sur hello portail Azure. Pour plus d’informations, consultez [tooAzure de déploiement Git Local du Service d’applications](app-service-deploy-local-git.md).

Ouvrez le fichier de solution hello (.sln) qui est inclus dans la racine de hello du référentiel de hello.

![](./media/web-sites-python-create-deploy-flask-app/ptvs-solution-flask.png)

### <a name="create-virtual-environment"></a>Créer un environnement virtuel
Nous allons à présent créer un environnement virtuel pour le développement local.  Cliquez avec le bouton droit sur **Environnements Python** et sélectionnez **Ajouter un environnement virtuel...**.

* Assurez-vous que le nom de l’environnement de hello hello est `env`.
* Sélectionnez l’interpréteur de base hello.  Assurez-vous que toouse hello même version de Python est sélectionné pour votre application web (dans runtime.txt ou hello **paramètres de l’Application** Panneau de votre application web Bonjour portail Azure).
* Vérifiez que hello option toodownload et installer les packages est activée.

![](./media/web-sites-python-create-deploy-flask-app/ptvs-add-virtual-env-27.png)

Cliquez sur **Créer**.  Cela créer un environnement virtuel hello et installer les dépendances répertoriées dans requirements.txt.

### <a name="run-using-development-server"></a>Exécuter à l’aide d’un serveur de développement
Appuyez sur F5 toostart est le débogage et que votre navigateur web seront ouvre automatiquement page toohello en cours d’exécution localement.

![](./media/web-sites-python-create-deploy-flask-app/windows-browser-flask.png)

Vous pouvez définir des points d’arrêt dans les sources de hello, utilisez hello espion, etc..  Consultez hello [outils Python pour Visual Studio Documentation] pour plus d’informations sur hello différentes fonctionnalités.

### <a name="make-changes"></a>Apporter des modifications
Maintenant, vous pouvez tester en apportant des modifications toohello application sources et/ou des modèles.

Une fois que vous avez testé vos modifications, les valider toohello Git référentiel :

![](./media/web-sites-python-create-deploy-flask-app/ptvs-commit-flask.png)

### <a name="install-more-packages"></a>Installer d’autres packages
Votre application peut comporter des dépendances au-delà de Python et de Flask.

Vous pouvez installer des packages supplémentaires à l’aide de pip.  tooinstall un package, avec le bouton droit sur l’environnement virtuel de hello et sélectionnez **Package d’installation de Python**.

Par exemple, tooinstall hello Azure SDK pour Python, ce qui vous donne accès tooAzure stockage, service bus et autres services Azure, entrez `azure`:

![](./media/web-sites-python-create-deploy-flask-app/ptvs-install-package-dialog.png)

Avec le bouton droit sur l’environnement virtuel de hello et sélectionnez **générer requirements.txt** tooupdate requirements.txt.

Ensuite, validez le référentiel Git toohello hello modifications toorequirements.txt.

### <a name="deploy-tooazure"></a>Déployer tooAzure
tootrigger un déploiement, cliquez sur **synchronisation** ou **Push**.  La synchronisation effectue à la fois une transmission de type push et une transmission de type pull.

![](./media/web-sites-python-create-deploy-flask-app/ptvs-git-push.png)

premier déploiement de Hello prend un certain temps, comme il crée un environnement virtuel, les packages d’installation de périphérique.

Visual Studio n’affiche pas les cours hello du déploiement de hello.  Si vous souhaitez que la sortie de hello tooreview, consultez la section de hello sur [dépannage - déploiement](#troubleshooting-deployment).

Accédez à toohello URL Azure tooview vos modifications.

## <a name="web-app-development---windows---command-line"></a>Développement d’applications web - Windows - Ligne de commande
### <a name="clone-hello-repository"></a>Référentiel de hello clone
Tout d’abord, cloner le référentiel hello à l’aide des URL hello fournie sur hello portail Azure, puis ajoutez hello Azure référentiel distant. Pour plus d’informations, consultez [tooAzure de déploiement Git Local du Service d’applications](app-service-deploy-local-git.md).

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a>Créer un environnement virtuel
Nous allons créer un nouvel environnement virtuel pour le développement (ne l’ajoutez pas toohello référentiel).  Environnements virtuels dans Python ne sont pas transférable, chaque développeur travaille sur une application hello allez donc créer leur propres localement.

Assurez-vous que toouse hello même version de Python est sélectionné pour votre application web (dans runtime.txt ou hello **paramètres de l’Application** Panneau de votre application web Bonjour portail Azure).

Pour Python 2.7 :

    c:\python27\python.exe -m virtualenv env

Pour Python 3.4 :

    c:\python34\python.exe -m venv env

Installez tous les packages externes requis par votre application. Vous pouvez utiliser le fichier de requirements.txt hello à racine hello hello référentiel tooinstall hello des packages dans votre environnement virtuel :

    env\scripts\pip install -r requirements.txt

### <a name="run-using-development-server"></a>Exécuter à l’aide d’un serveur de développement
Vous pouvez lancer l’application hello sous un serveur de développement avec hello de commande suivante :

    env\scripts\python runserver.py

Hello console affiche hello URL et port hello serveur écoute :

![](./media/web-sites-python-create-deploy-flask-app/windows-run-local-flask.png)

Ensuite, ouvrez votre URL toothat du navigateur web.

![](./media/web-sites-python-create-deploy-flask-app/windows-browser-flask.png)

### <a name="make-changes"></a>Apporter des modifications
Maintenant, vous pouvez tester en apportant des modifications toohello application sources et/ou des modèles.

Une fois que vous avez testé vos modifications, les valider toohello Git référentiel :

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a>Installer d’autres packages
Votre application peut comporter des dépendances au-delà de Python et de Flask.

Vous pouvez installer des packages supplémentaires à l’aide de pip.  Par exemple, tooinstall hello Azure SDK pour Python, ce qui vous donne accès tooAzure stockage, service bus et autres services Azure, le type :

    env\scripts\pip install azure

Assurez-vous que tooupdate requirements.txt :

    env\scripts\pip freeze > requirements.txt

Valider les modifications de hello :

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a>Déployer tooAzure
tootrigger un déploiement, hello de push modifie tooAzure :

    git push azure master

Vous verrez un résultat de hello du script de déploiement hello, y compris la création d’un environnement virtuel, l’installation des packages, la création du fichier web.config.

Accédez à toohello URL Azure tooview vos modifications.

## <a name="web-app-development---maclinux---command-line"></a>Développement d’applications web - Mac/Linux - Ligne de commande
### <a name="clone-hello-repository"></a>Référentiel de hello clone
Tout d’abord, cloner le référentiel hello à l’aide des URL hello fournie sur hello portail Azure, puis ajoutez hello Azure référentiel distant. Pour plus d’informations, consultez [tooAzure de déploiement Git Local du Service d’applications](app-service-deploy-local-git.md).

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a>Créer un environnement virtuel
Nous allons créer un nouvel environnement virtuel pour le développement (ne l’ajoutez pas toohello référentiel).  Environnements virtuels dans Python ne sont pas transférable, chaque développeur travaille sur une application hello allez donc créer leur propres localement.

Assurez-vous que toouse hello même version de Python est sélectionné pour votre application web (dans runtime.txt ou hello **paramètres de l’Application** Panneau de votre application web Bonjour portail Azure).

Pour Python 2.7 :

    python -m virtualenv env

Pour Python 3.4 :

    python -m venv env
or pyvenv env

Installez tous les packages externes requis par votre application. Vous pouvez utiliser le fichier de requirements.txt hello à racine hello hello référentiel tooinstall hello des packages dans votre environnement virtuel :

    env/bin/pip install -r requirements.txt

### <a name="run-using-development-server"></a>Exécuter à l’aide d’un serveur de développement
Vous pouvez lancer l’application hello sous un serveur de développement avec hello de commande suivante :

    env/bin/python runserver.py

Hello console affiche hello URL et port hello serveur écoute :

![](./media/web-sites-python-create-deploy-flask-app/mac-run-local-flask.png)

Ensuite, ouvrez votre URL toothat du navigateur web.

![](./media/web-sites-python-create-deploy-flask-app/mac-browser-flask.png)

### <a name="make-changes"></a>Apporter des modifications
Maintenant, vous pouvez tester en apportant des modifications toohello application sources et/ou des modèles.

Une fois que vous avez testé vos modifications, les valider toohello Git référentiel :

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a>Installer d’autres packages
Votre application peut comporter des dépendances au-delà de Python et de Flask.

Vous pouvez installer des packages supplémentaires à l’aide de pip.  Par exemple, tooinstall hello Azure SDK pour Python, ce qui vous donne accès tooAzure stockage, service bus et autres services Azure, le type :

    env/bin/pip install azure

Assurez-vous que tooupdate requirements.txt :

    env/bin/pip freeze > requirements.txt

Valider les modifications de hello :

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a>Déployer tooAzure
tootrigger un déploiement, hello de push modifie tooAzure :

    git push azure master

Vous verrez un résultat de hello du script de déploiement hello, y compris la création d’un environnement virtuel, l’installation des packages, la création du fichier web.config.

Accédez à toohello URL Azure tooview vos modifications.

## <a name="troubleshooting---package-installation"></a>Résolution des problèmes - Installation des packages
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a>Résolution des problèmes - Environnement virtuel
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="next-steps"></a>Étapes suivantes
Suivez ces liens de toolearn plus d’informations sur ballon et les outils Python pour Visual Studio : 

* [Documentation relative à Flask]
* [outils Python pour Visual Studio Documentation]

Pour obtenir des informations concernant l’utilisation du stockage de tables Azure et MongoDB :

* [Flask et MongoDB sur Azure avec Python Tools pour Visual Studio]
* [Flask et stockage des tables Azure sur Azure avec Python Tools pour Visual Studio]

Pour plus d’informations, consultez également hello [centre de développement Python](/develop/python/).

## <a name="whats-changed"></a>Changements apportés
* Pour un toohello guide voir changer à partir de sites Web tooApp Service : [Azure App Service et son Impact sur les Services Azure existants](http://go.microsoft.com/fwlink/?LinkId=529714)

<!--Link references-->
[Flask et MongoDB sur Azure avec Python Tools pour Visual Studio]: https://github.com/microsoft/ptvs/wiki/Flask-and-MongoDB-on-Azure
[Flask et stockage des tables Azure sur Azure avec Python Tools pour Visual Studio]: web-sites-python-ptvs-flask-table-storage.md

<!--External Link references-->
[Kit de développement logiciel (SDK) Azure pour Python 2.7]: http://go.microsoft.com/fwlink/?linkid=254281
[Kit de développement logiciel (SDK) Azure pour Python 3.4]: http://go.microsoft.com/fwlink/?linkid=516990
[python.org]: http://www.python.org/
[Git pour Windows]: http://msysgit.github.io/
[GitHub pour Windows]: https://windows.github.com/
[Python Tools pour Visual Studio]: http://aka.ms/ptvs
[Python Tools 2.2 pour Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Visual Studio]: http://www.visualstudio.com/
[outils Python pour Visual Studio Documentation]: http://aka.ms/ptvsdocs
[Documentation relative à Flask]: http://flask.pocoo.org/ 

