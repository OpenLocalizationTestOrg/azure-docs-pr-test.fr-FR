---
title: applications web aaaCreating avec Django dans Azure
description: "Un didacticiel qui vous présente toorunning application web Python dans Azure App Service Web Apps."
services: app-service\web
documentationcenter: python
tags: python
author: huguesv
manager: erikre
editor: 
ms.assetid: 9be1a05a-9460-49ae-94fb-9798f82c11cf
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/19/2016
ms.author: huvalo
ms.openlocfilehash: 26a131da358748bd6fe4ee5c114d0a8f91b83cfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-web-apps-with-django-in-azure"></a>Création d’applications web avec Django dans Azure
Ce didacticiel décrit comment tooget démarré Python [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714). Web Apps offre un hébergement gratuit limité ainsi qu’un déploiement rapide, et vous permet d’utiliser Python. Comme votre application se développe, vous pouvez basculer toopaid d’hébergement, et vous pouvez également intégrer avec tous les hello autres services Azure.

Vous allez créer une application à l’aide hello Django web framework (voir les autres versions de ce didacticiel pour [ballon](web-sites-python-create-deploy-flask-app.md) et [Bottle](web-sites-python-create-deploy-bottle-app.md)). Vous crée l’application web hello de hello Azure Marketplace, configurer le déploiement de Git et cloner le référentiel hello localement. Puis vous serez exécuté application hello localement, apporter des modifications, validez et envoyez les tooAzure. Hello didacticiel montre comment toodo à partir de Windows ou Mac/Linux.

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
Si vous n’avez pas encore installé Python 2.7 ou 3.4 (32 bits), nous vous recommandons d’installer le [Kit de développement logiciel (SDK) Azure pour Python 2.7] ou le [Kit de développement logiciel (SDK) Azure pour Python 3.4] à l’aide de Web Platform Installer. Cela installe la version 32 bits de hello de Python, setuptools, pip, virtualenv, etc. (32 bits Python est ce qui est installé sur les ordinateurs hôte Azure hello). Vous pouvez également obtenir Python sur le site [python.org].

Pour Git, nous vous recommandons d’utiliser [Git pour Windows] ou [GitHub pour Windows]. Si vous utilisez Visual Studio, vous pouvez utiliser la prise en charge de Git hello intégré.

Nous vous recommandons également d’installer [Python Tools 2.2 pour Visual Studio]. Cette option est facultative, mais si vous avez [Visual Studio], y compris hello libre Visual Studio Community 2013 ou Visual Studio Express 2013 pour le Web, puis vous obtenez ainsi un remarquable IDE Python.

### <a name="maclinux"></a>Mac/Linux
Vous devez avoir installé Python et Git, mais vérifiez que vous disposez de Python 2.7 ou 3.4.

## <a name="web-app-creation-on-portal"></a>Création d’une application web sur le portail
première étape de la création de votre application Hello est l’application web via hello toocreate hello [Azure Portal](https://portal.azure.com).

1. Ouvrez une session hello portail Azure, puis cliquez sur hello **nouveau** bouton hello bas à gauche.
2. Dans la zone de recherche de hello, tapez « python ».
3. Dans les résultats de recherche de hello, sélectionnez **Django** (publié par PTVS), puis cliquez sur **créer**.
4. Configurer nouveau Django application hello, telles que la création d’un nouveau plan App Service et un groupe de ressources pour celle-ci. Cliquez sur **Créer**.
5. Configurer la publication Git de votre application web qui vient d’être créé en suivant les instructions de hello sur [tooAzure de déploiement Git Local du Service d’applications](app-service-deploy-local-git.md).

## <a name="application-overview"></a>Vue d’ensemble de l’application
### <a name="git-repository-contents"></a>Contenu du référentiel Git
Voici une vue d’ensemble des fichiers hello que vous trouverez dans le référentiel Git initiale hello, lequel nous allons cloner dans la section suivante de hello.

    \app\__init__.py
    \app\forms.py
    \app\models.py
    \app\tests.py
    \app\views.py
    \app\static\content\
    \app\static\fonts\
    \app\static\scripts\
    \app\templates\about.html
    \app\templates\contact.html
    \app\templates\index.html
    \app\templates\layout.html
    \app\templates\login.html
    \app\templates\loginpartial.html
    \DjangoWebProject\__init__.py
    \DjangoWebProject\settings.py
    \DjangoWebProject\urls.py
    \DjangoWebProject\wsgi.py

Sources principales pour l’application hello. Correspondent à 3 pages (index, à propos de, contact) dotées d’une mise en page principale. Le contenu statique et les scripts comprennent bootstrap, jquery, modernizr et respond.

    \manage.py

Prise en charge du serveur d’administration et de développement local. Utiliser cette application de hello toorun localement, synchroniser la base de données hello, etc..

    \db.sqlite3

Base de données par défaut. Inclut les tables nécessaires de hello pour hello application toorun, mais ne contient pas tous les utilisateurs (synchronisation hello toocreate de base de données utilisateur).

    \DjangoWebProject.pyproj
    \DjangoWebProject.sln

Fichiers de projet à utiliser avec [Python Tools pour Visual Studio].

    \ptvs_virtualenv_proxy.py

Proxy IIS pour les environnements virtuels et prise en charge du débogage à distance PTVS.

    \requirements.txt

Packages externes requis par cette application. script de déploiement Hello sera pip des packages d’installation de hello répertoriés dans ce fichier.

    \web.2.7.config
    \web.3.4.config

Fichiers de configuration IIS. script de déploiement Hello utilise web.x.y.config approprié de hello et copiez-le en tant que fichier web.config.

### <a name="optional-files---customizing-deployment"></a>Fichiers facultatifs - Personnalisation du déploiement
[!INCLUDE [web-sites-python-django-customizing-deployment](../../includes/web-sites-python-django-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a>Fichiers facultatifs - Runtime Python
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a>Fichiers supplémentaires sur le serveur
Certains fichiers existent sur le serveur de hello mais ne sont pas ajoutés de référentiel git de toohello. Ceux-ci sont créés par le script de déploiement hello.

    \web.config

Fichier de configuration IIS. Créé à partir du fichier web.x.y.config lors de chaque déploiement.

    \env\

Environnement virtuel Python. Si un environnement virtuel compatible n’existe pas déjà sur l’application web de hello, créé pendant le déploiement. Packages répertoriés dans requirements.txt sont pip installé, mais pip ignorera l’installation si hello packages sont déjà installés.

Hello 3 sections décrivent comment tooproceed avec hello web sous 3 différents environnements le développement d’applications :

* Windows, avec Python Tools pour Visual Studio ;
* Windows, avec la ligne de commande ;
* Mac/Linux, avec la ligne de commande.

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a>Développement d’applications web - Windows - Python Tools pour Visual Studio
### <a name="clone-hello-repository"></a>Référentiel de hello clone
Tout d’abord, cloner le référentiel de hello à l’aide des URL hello fournie sur hello portail Azure. Pour plus d’informations, consultez [tooAzure de déploiement Git Local du Service d’applications](app-service-deploy-local-git.md).

Ouvrez le fichier de solution hello (.sln) qui est inclus dans la racine de hello du référentiel de hello.

![](./media/web-sites-python-create-deploy-django-app/ptvs-solution-django.png)

### <a name="create-virtual-environment"></a>Créer un environnement virtuel
Nous allons à présent créer un environnement virtuel pour le développement local. Cliquez avec le bouton droit sur **Environnements Python** et sélectionnez **Ajouter un environnement virtuel...**.

* Assurez-vous que le nom de l’environnement de hello hello est `env`.
* Sélectionnez l’interpréteur de base hello. Assurez-vous que toouse hello même version de Python est sélectionné pour votre application web (dans runtime.txt ou hello **paramètres de l’Application** Panneau de votre application web Bonjour portail Azure).
* Vérifiez que hello option toodownload et installer les packages est activée.

![](./media/web-sites-python-create-deploy-django-app/ptvs-add-virtual-env-27.png)

Cliquez sur **Créer**. Cela créer un environnement virtuel hello et installer les dépendances répertoriées dans requirements.txt.

### <a name="create-a-superuser"></a>Créer un superutilisateur
base de données Hello inclus avec l’application hello n’a pas de n’importe quel superutilisateur défini. Dans l’ordre toouse hello fonctionnalité de connexion dans l’application hello ou l’interface d’administration hello Django (si vous décidez de tooenable il), vous devez toocreate un super utilisateur.

Exécutez ceci à partir hello de ligne de commande à partir de votre dossier de projet :

    env\scripts\python manage.py createsuperuser

Suivez le nom d’utilisateur hello invites tooset hello, mot de passe, etc..

### <a name="run-using-development-server"></a>Exécuter à l’aide d’un serveur de développement
Appuyez sur F5 toostart est le débogage et que votre navigateur web seront ouvre automatiquement page toohello en cours d’exécution localement.

![](./media/web-sites-python-create-deploy-django-app/windows-browser-django.png)

Vous pouvez définir des points d’arrêt dans les sources de hello, utilisez hello espion, etc.. Consultez hello [outils Python pour Visual Studio Documentation] pour plus d’informations sur hello différentes fonctionnalités.

### <a name="make-changes"></a>Apporter des modifications
Maintenant, vous pouvez tester en apportant des modifications toohello application sources et/ou des modèles.

Une fois que vous avez testé vos modifications, les valider toohello Git référentiel :

![](./media/web-sites-python-create-deploy-django-app/ptvs-commit-django.png)

### <a name="install-more-packages"></a>Installer d’autres packages
Votre application peut comporter des dépendances au-delà de Python et de Django.

Vous pouvez installer des packages supplémentaires à l’aide de pip. tooinstall un package, avec le bouton droit sur l’environnement virtuel de hello et sélectionnez **Package d’installation de Python**.

Par exemple, tooinstall hello Azure SDK pour Python, ce qui vous donne accès tooAzure stockage, service bus et autres services Azure, entrez `azure`:

![](./media/web-sites-python-create-deploy-django-app/ptvs-install-package-dialog.png)

Avec le bouton droit sur l’environnement virtuel de hello et sélectionnez **générer requirements.txt** tooupdate requirements.txt.

Ensuite, validez le référentiel Git toohello hello modifications toorequirements.txt.

### <a name="deploy-tooazure"></a>Déployer tooAzure
tootrigger un déploiement, cliquez sur **synchronisation** ou **Push**. La synchronisation effectue à la fois une transmission de type push et une transmission de type pull.

![](./media/web-sites-python-create-deploy-django-app/ptvs-git-push.png)

premier déploiement de Hello prend un certain temps, comme il crée un environnement virtuel, les packages d’installation de périphérique.

Visual Studio n’affiche pas les cours hello du déploiement de hello. Si vous souhaitez que la sortie de hello tooreview, consultez la section de hello sur [dépannage - déploiement](#troubleshooting-deployment).

Accédez à toohello URL Azure tooview vos modifications.

## <a name="web-app-development---windows---command-line"></a>Développement d’applications web - Windows - Ligne de commande
### <a name="clone-hello-repository"></a>Référentiel de hello clone
Tout d’abord, cloner le référentiel hello à l’aide des URL hello fournie sur hello portail Azure, puis ajoutez hello Azure référentiel distant. Pour plus d’informations, consultez [tooAzure de déploiement Git Local du Service d’applications](app-service-deploy-local-git.md).

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url>

### <a name="create-virtual-environment"></a>Créer un environnement virtuel
Nous allons créer un nouvel environnement virtuel pour le développement (ne l’ajoutez pas toohello référentiel). Environnements virtuels dans Python ne sont pas transférable, chaque développeur travaille sur une application hello allez donc créer leur propres localement.

Assurez-vous que toouse hello même version de Python est sélectionné pour votre application web (dans le panneau Paramètres de l’Application de votre application web Bonjour Azure Portal runtime.txt ou hello).

Pour Python 2.7 :

    c:\python27\python.exe -m virtualenv env

Pour Python 3.4 :

    c:\python34\python.exe -m venv env

Installez tous les packages externes requis par votre application. Vous pouvez utiliser le fichier de requirements.txt hello à racine hello hello référentiel tooinstall hello des packages dans votre environnement virtuel :

    env\scripts\pip install -r requirements.txt

### <a name="create-a-superuser"></a>Créer un superutilisateur
base de données Hello inclus avec l’application hello n’a pas de n’importe quel superutilisateur défini. Dans l’ordre toouse hello fonctionnalité de connexion dans l’application hello ou l’interface d’administration hello Django (si vous décidez de tooenable il), vous devez toocreate un super utilisateur.

Exécutez ceci à partir hello de ligne de commande à partir de votre dossier de projet :

    env\scripts\python manage.py createsuperuser

Suivez le nom d’utilisateur hello invites tooset hello, mot de passe, etc..

### <a name="run-using-development-server"></a>Exécuter à l’aide d’un serveur de développement
Vous pouvez lancer l’application hello sous un serveur de développement avec hello de commande suivante :

    env\scripts\python manage.py runserver

Hello console affiche hello URL et port hello serveur écoute :

![](./media/web-sites-python-create-deploy-django-app/windows-run-local-django.png)

Ensuite, ouvrez votre URL toothat du navigateur web.

![](./media/web-sites-python-create-deploy-django-app/windows-browser-django.png)

### <a name="make-changes"></a>Apporter des modifications
Maintenant, vous pouvez tester en apportant des modifications toohello application sources et/ou des modèles.

Une fois que vous avez testé vos modifications, les valider toohello Git référentiel :

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a>Installer d’autres packages
Votre application peut comporter des dépendances au-delà de Python et de Django.

Vous pouvez installer des packages supplémentaires à l’aide de pip. Par exemple, tooinstall hello Azure SDK pour Python, ce qui vous donne accès tooAzure stockage, service bus et autres services Azure, le type :

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
Nous allons créer un nouvel environnement virtuel pour le développement (ne l’ajoutez pas toohello référentiel). Environnements virtuels dans Python ne sont pas transférable, chaque développeur travaille sur une application hello allez donc créer leur propres localement.

Assurez-vous que toouse hello même version de Python est sélectionné pour votre application web (dans le panneau Paramètres de l’Application de votre application web Bonjour Azure Portal runtime.txt ou hello).

Pour Python 2.7 :

    python -m virtualenv env

Pour Python 3.4 :

    python -m venv env

ou

    pyvenv env

Installez tous les packages externes requis par votre application. Vous pouvez utiliser le fichier de requirements.txt hello à racine hello hello référentiel tooinstall hello des packages dans votre environnement virtuel :

    env/bin/pip install -r requirements.txt

### <a name="create-a-superuser"></a>Créer un superutilisateur
base de données Hello inclus avec l’application hello n’a pas de n’importe quel superutilisateur défini. Dans l’ordre toouse hello fonctionnalité de connexion dans l’application hello ou l’interface d’administration hello Django (si vous décidez de tooenable il), vous devez toocreate un super utilisateur.

Exécutez ceci à partir hello de ligne de commande à partir de votre dossier de projet :

    env/bin/python manage.py createsuperuser

Suivez le nom d’utilisateur hello invites tooset hello, mot de passe, etc..

### <a name="run-using-development-server"></a>Exécuter à l’aide d’un serveur de développement
Vous pouvez lancer l’application hello sous un serveur de développement avec hello de commande suivante :

    env/bin/python manage.py runserver

Hello console affiche hello URL et port hello serveur écoute :

![](./media/web-sites-python-create-deploy-django-app/mac-run-local-django.png)

Ensuite, ouvrez votre URL toothat du navigateur web.

![](./media/web-sites-python-create-deploy-django-app/mac-browser-django.png)

### <a name="make-changes"></a>Apporter des modifications
Maintenant, vous pouvez tester en apportant des modifications toohello application sources et/ou des modèles.

Une fois que vous avez testé vos modifications, les valider toohello Git référentiel :

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a>Installer d’autres packages
Votre application peut comporter des dépendances au-delà de Python et de Django.

Vous pouvez installer des packages supplémentaires à l’aide de pip. Par exemple, tooinstall hello Azure SDK pour Python, ce qui vous donne accès tooAzure stockage, service bus et autres services Azure, le type :

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

## <a name="troubleshooting---static-files"></a>Résolution des problèmes - Fichiers statiques
Django a un concept hello de collecte de fichiers statiques. Cela prend tous les fichiers statiques hello à partir de leur emplacement d’origine et les copie tooa seul dossier. Pour cette application, ils sont copiés trop`/static`.

Cette opération est effectuée, car les fichiers statiques peuvent provenir de différentes applications Django. Par exemple, les fichiers statiques hello à partir des interfaces d’administration hello Django se trouvent dans un sous-dossier de la bibliothèque Django dans un environnement virtuel de hello. Les fichiers statiques définis par cette application se trouvent dans `/app/static`. Plus vous utiliserez d’applications Django, plus vous aurez de fichiers statiques dans différents emplacements.

Lorsque vous exécutez l’application hello en mode débogage, application hello prend en charge hello des fichiers statiques à partir de leur emplacement d’origine.

Lorsque vous exécutez l’application hello en mode version finale, application hello est **pas** hello les fichiers statiques. Il incombe hello des fichiers de hello tooserve hello web server. Pour cette application, IIS servira à partir des fichiers statiques hello `/static`.

collection de Hello des fichiers statiques s’effectue automatiquement en tant que fichiers de la partie du script de déploiement hello, effacement précédemment collecté. Cela signifie la collecte de hello se produit sur chaque déploiement, ralentir de déploiement, mais il garantit que les fichiers obsolètes n’est pas disponibles, ce qui évite d’un problème de sécurité potentiel.

Si vous souhaitez collection tooskip des fichiers statiques pour votre application Django :

    \.skipDjango

Vous devez collection de hello toodo manuellement sur votre ordinateur local :

    env\scripts\python manage.py collectstatic

Puis supprimez hello `\static` dossier `.gitignore` et ajoutez-le référentiel Git de toohello.

## <a name="troubleshooting---settings"></a>Résolution des problèmes - Paramètres
Différents paramètres d’application hello peuvent être modifiées dans `DjangoWebProject/settings.py`.

Pour simplifier le développement, le mode débogage est activé. Un effet secondaire intéressant de qui est que vous serez en mesure de toosee images et autre contenu statique lors de l’exécution localement, sans avoir toocollect des fichiers statiques.

mode de débogage toodisable :

    DEBUG = False

Lorsque le débogage est désactivé, hello valeur pour `ALLOWED_HOSTS` besoins toobe mis à jour le nom de l’hôte Azure tooinclude hello. Par exemple :

    ALLOWED_HOSTS = (
        'pythonapp.azurewebsites.net',
    )

ou tooenable tout :

    ALLOWED_HOSTS = (
        '*',
    )

Dans la pratique, vous souhaiterez toodo toodeal plus complexe avec le changement entre déboguer et le mode et le nom d’hôte hello lors de l’obtention de la version.

Vous pouvez définir des variables d’environnement via le portail Azure de hello **configurer** page hello **paramètres de l’application** section.  Cela peut être utile pour définir les valeurs que vous ne souhaitez pas tooappear dans les sources de hello (chaînes de connexion, les mots de passe, etc.), ou que vous souhaitez tooset différemment entre Azure et sur votre ordinateur local. Dans `settings.py`, vous pouvez interroger les variables d’environnement hello à l’aide de `os.getenv`.

## <a name="using-a-database"></a>Utilisation d’une base de données
base de données Hello est inclus dans l’application hello est une base de données sqlite. Il s’agit d’un toouse de la base de données par défaut pratique et utile pour le développement, car il nécessite presque sans le programme d’installation. base de données Hello est stocké dans le fichier de db.sqlite3 hello dans le dossier de projet hello.

Azure fournit des services de base de données qui sont toouse facile à partir d’une application Django. Didacticiels pour l’utilisation de [base de données SQL] et [MySQL] à partir d’une application de Django afficher les étapes de hello service de base de données hello toocreate nécessaire, de modifier les paramètres de base de données hello dans `DjangoWebProject/settings.py`et hello bibliothèques requis tooinstall.

Bien entendu, si vous préférez toomanage vos propres serveurs de base de données, vous pouvez effectuer à l’aide de Windows ou Linux des machines virtuelles s’exécutant sur Azure.

## <a name="django-admin-interface"></a>Interface d’administration Django
Une fois que vous démarrez la création de vos modèles, vous souhaiterez toopopulate de la base de données hello avec des données. Facilement toodo ajouter et modifier interactivement le contenu est l’interface d’administration Django toouse hello.

code Hello pour l’interface d’administration hello est commentée dans les sources d’application hello, mais elle est marquée clairement afin de vous pouvez facilement activer (recherchez « admin »).

Une fois qu’il est activé, synchroniser hello de base de données, exécutez l’application hello et accédez trop`/admin`.

## <a name="next-steps"></a>Étapes suivantes
Suivez ces liens de toolearn plus d’informations sur les Django et les outils Python pour Visual Studio :

* [Documentation Django]
* [outils Python pour Visual Studio Documentation]

Pour plus d’informations sur l’utilisation de Base de données SQL et de MySQL :

* [Django et MySQL sur Azure avec Python Tools pour Visual Studio]
* [Django et SQL Database sur Azure avec Python pour Visual Studio]

Pour plus d’informations, consultez hello [centre de développement Python](/develop/python/).

## <a name="whats-changed"></a>Changements apportés
* Pour un toohello guide voir changer à partir de sites Web tooApp Service : [Azure App Service et son Impact sur les Services Azure existants](http://go.microsoft.com/fwlink/?LinkId=529714)

<!--Link references-->
[Django et MySQL sur Azure avec Python Tools pour Visual Studio]: web-sites-python-ptvs-django-mysql.md
[Django et SQL Database sur Azure avec Python pour Visual Studio]: web-sites-python-ptvs-django-sql.md
[base de données SQL]: web-sites-python-ptvs-django-sql.md
[MySQL]: web-sites-python-ptvs-django-mysql.md

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
[Documentation Django]: https://www.djangoproject.com/
