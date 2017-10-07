---
title: aaaDjango et MySQL sur Azure avec 2.2 des outils Python pour Visual Studio
description: "Découvrez comment toouse hello outils Python pour Visual Studio toocreate, une application web Django qui stocke les données dans une instance de la base de données MySQL et déployez-le tooAzure App Service Web Apps."
services: app-service\web
documentationcenter: python
author: huguesv
manager: erikre
editor: 
ms.assetid: c60a50b5-8b5e-4818-a442-16362273dabb
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/07/2016
ms.author: huvalo
ms.openlocfilehash: 1597c391d20c8e8ef629b4e4d05c9eb64c83bffc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="django-and-mysql-on-azure-with-python-tools-22-for-visual-studio"></a>Django et MySQL sur Azure avec Python Tools 2.2 pour Visual Studio
[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

Dans ce didacticiel, vous allez utiliser [outils Python pour Visual Studio](https://www.visualstudio.com/vs/python) toocreate simple interroge l’application web à l’aide d’un des exemples de modèles de PTVS hello. Vous allez apprendre comment toouse un service MySQL hébergé sur Azure, comment tooconfigure hello web application toouse MySQL et comment toopublish hello web application trop[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).

> [!NOTE]
> les informations de Hello contenues dans ce didacticiel sont également disponibles dans hello suivant vidéo :
> 
> [PTVS 2.1 : application Django avec MySQL][video]
> 
> 

Consultez hello [centre de développement Python] autres articles qui couvrent le développement de Azure App Service Web Apps avec PTVS à l’aide d’eau, ballon Django web et infrastructures, avec les services de base de données SQL, MySQL et stockage de Table Azure. Alors que cet article se concentre sur le Service d’applications, les étapes de hello sont similaires lors du développement [Azure Cloud Services].

## <a name="prerequisites"></a>Composants requis
* Visual Studio 2015
* [Python 2.7 32 bits] ou [Python 3.4 32 bits]
* [Python Tools 2.2 pour Visual Studio]
* [2.2 des outils Python pour Visual Studio exemples VSIX]
* [Outils du Kit de développement logiciel (SDK) Azure pour Visual Studio 2015]
* Django 1.9 ou version ultérieure

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

<!-- This note should not render as part of hello hello previous include. -->

> [!NOTE]
> Si vous souhaitez tooget démarré avec le Service d’application Azure avant de s’inscrire pour un compte Azure, accédez trop[essayez du Service d’applications](https://azure.microsoft.com/try/app-service/), où vous pouvez créer une application web de courte durée de démarrage immédiatement dans le Service d’applications. Aucune carte de crédit n’est nécessaire et vous ne prenez aucun engagement.
> 
> 

## <a name="create-hello-project"></a>Créer hello projet
Dans cette section, vous allez créer un projet Visual Studio à l’aide d’un exemple de modèle. Vous allez créer un environnement virtuel et installer les packages requis. Vous allez créer une base de données locale à l’aide de sqlite. Ensuite, vous allez exécuter application hello localement.

1. Dans Visual Studio, sélectionnez **Fichier**, **Nouveau projet**.
2. Hello des modèles de projet à partir de hello [2.2 des outils Python pour Visual Studio exemples VSIX] sont disponibles sous **Python**, **exemples**. Sélectionnez **interroge Django Web projet** et cliquez sur OK toocreate hello projet.
   
    ![Boîte de dialogue Nouveau projet](./media/web-sites-python-ptvs-django-mysql/PollsDjangoNewProject.png)
3. Vous serez invité à tooinstall les packages externes. Sélectionnez **Installer dans un environnement virtuel**.
   
    ![Boîte de dialogue Packages externes](./media/web-sites-python-ptvs-django-mysql/PollsDjangoExternalPackages.png)
4. Sélectionnez **Python 2.7** ou **Python 3.4** comme interpréteur de base hello.
   
    ![Boîte de dialogue Ajouter un environnement virtuel](./media/web-sites-python-ptvs-django-mysql/PollsCommonAddVirtualEnv.png)
5. Dans **l’Explorateur de solutions**, avec le bouton droit sur le nœud de projet hello et sélectionnez **Python**, puis sélectionnez **Django migrer**.  Sélectionnez ensuite **Django Create Superuser (Créer un superutilisateur Django)**.
6. Vous ouvrez une Console de gestion Django et créer une base de données sqlite dans le dossier de projet hello. Suivez les invites de hello toocreate un utilisateur.
7. Vérifier que l’application hello fonctionne en appuyant sur `F5`.
8. Cliquez sur **connecter** à partir de la barre de navigation hello haut hello.
   
    ![Barre de navigation Django](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserLocalMenu.png)
9. Entrez des informations d’identification de hello pour utilisateur hello que vous avez créé lors de la synchronisation de base de données hello.
   
    ![Formulaire de connexion](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserLocalLogin.png)
10. Cliquez sur **Create Sample Polls**.
    
     ![Create Sample Polls](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserNoPolls.png)
11. Cliquez sur un sondage et votez.
    
     ![Vote dans les exemples de sondage](./media/web-sites-python-ptvs-django-mysql/PollsDjangoSqliteBrowser.png)

## <a name="create-a-mysql-database"></a>Création d’une base de données MySQL
Pour la base de données hello, vous allez créer une base de données ClearDB MySQL hébergé sur Azure.

Vous pouvez également créer votre propre machine virtuelle s'exécutant dans Azure, puis installer et administrer MySQL vous-même.

Pour créer une base de données avec un plan gratuit, procédez comme suit :

1. Connectez-vous à toohello [Azure Portal].
2. En hello haut hello du volet de navigation, cliquez sur **nouveau**, puis cliquez sur **données + stockage**, puis cliquez sur **base de données MySQL**.
3. Configurer la base de données MySQL hello en créant un nouveau groupe de ressources et sélectionner l’emplacement approprié d’hello pour celle-ci.
4. Une fois la base de données MySQL hello est créé, cliquez sur **propriétés** dans Panneau de la base de données hello.
5. Utilisez hello copie bouton tooput hello valeur **chaîne de connexion** Presse-papiers de hello.

## <a name="configure-hello-project"></a>Configurer hello projet
Dans cette section, vous allez configurer notre web application toouse hello base de données MySQL que vous venez de créer. Vous allez également installer Python packages requis toouse MySQL bases de données supplémentaires avec Django. Ensuite, vous allez exécuter l’application hello web localement.

1. Dans Visual Studio, ouvrez **settings.py**, à partir de hello *nom_projet* dossier. Collez temporairement chaîne de connexion hello dans l’éditeur de hello. chaîne de connexion Hello est au format suivant :
   
        Database=<NAME>;Data Source=<HOST>;User Id=<USER>;Password=<PASSWORD>
   
    Base de données par défaut modifiée hello **moteur** toouse MySQL et ensemble de valeurs pour hello **nom**, **utilisateur**, **mot de passe** et  **HÔTE** de hello **CONNECTIONSTRING**.
   
        DATABASES = {
            'default': {
                'ENGINE': 'django.db.backends.mysql',
                'NAME': '<Database>',
                'USER': '<User Id>',
                'PASSWORD': '<Password>',
                'HOST': '<Data Source>',
                'PORT': '',
            }
        }
2. Dans l’Explorateur de solutions, sous **environnements Python**, avec le bouton droit sur l’environnement virtuel de hello et sélectionnez **Package d’installation de Python**.
3. Installer le package de hello `mysqlclient` à l’aide de **pip**.
   
    ![Boîte de dialogue Installer le package](./media/web-sites-python-ptvs-django-mysql/PollsDjangoMySQLInstallPackage.png)
4. Dans **l’Explorateur de solutions**, avec le bouton droit sur le nœud de projet hello et sélectionnez **Python**, puis sélectionnez **Django migrer**.  Sélectionnez ensuite **Django Create Superuser (Créer un superutilisateur Django)**.
   
    Cela va créer les tables de base de données MySQL hello que vous avez créé dans la section précédente de hello hello. Suivez les invites de hello toocreate un utilisateur, qui ne dispose pas utilisateur de hello toomatch dans la base de données sqlite hello créé dans hello première section de cet article.
5. Exécutez l’application hello avec `F5`. Les interrogations sont créées avec **créer des sondages exemple** et données hello soumises par le vote seront sérialisées dans la base de données MySQL hello.

## <a name="publish-hello-web-app-tooazure-app-service"></a>Publier hello web application tooAzure du Service d’applications
Hello Kit de développement .NET Azure fournit un moyen simple de toodeploy votre tooAzure d’application web du Service d’applications.

1. Dans **l’Explorateur de solutions**, avec le bouton droit sur le nœud de projet hello et sélectionnez **publier**.
   
    ![Boîte de dialogue Publier le site Web](./media/web-sites-python-ptvs-django-mysql/PollsCommonPublishWebSiteDialog.png)
2. Cliquez sur **Microsoft Azure App Service**.
3. Cliquez sur **nouveau** toocreate une application web.
4. Renseignez hello suivant des champs, cliquez sur **créer**:
   
   * **Nom de l’application web**
   * **Plan App Service**
   * **Groupe de ressources**
   * **Région**
   * Laissez **serveur de base de données** défini trop**aucune base de données**
5. Acceptez toutes les valeurs par défaut et cliquez sur **Publier**.
6. Votre navigateur web s’ouvre automatiquement toohello publié web app. Vous devez voir le travail d’application hello web comme prévu, à l’aide de hello **MySQL** base de données hébergée sur Azure.
   
    ![Navigateur web](./media/web-sites-python-ptvs-django-mysql/PollsDjangoAzureBrowser.png)
   
    Félicitations ! Vous avez publié votre tooAzure d’application web basée sur MySQL.

## <a name="next-steps"></a>Étapes suivantes
Suivez ces liens de toolearn plus d’informations sur les outils Python pour Visual Studio, Django et MySQL.

* [Documentation relative à Python Tools for Visual Studio]
  * [Projets web]
  * [Projets de service cloud]
  * [Débogage à distance sur Microsoft Azure]
* [Documentation Django]
* [MySQL]

Pour plus d’informations, consultez hello [centre de développement Python](/develop/python/).

<!--Link references-->

[centre de développement Python]: /develop/python/
[Azure Cloud Services]: ../cloud-services/cloud-services-python-ptvs.md

<!--External Link references-->

[Azure Portal]: https://portal.azure.com
[Python Tools for Visual Studio]: https://www.visualstudio.com/vs/python/
[Python Tools 2.2 pour Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[2.2 des outils Python pour Visual Studio exemples VSIX]: http://go.microsoft.com/fwlink/?LinkID=624025
[Outils du Kit de développement logiciel (SDK) Azure pour Visual Studio 2015]: http://go.microsoft.com/fwlink/?LinkId=518003
[Python 2.7 32 bits]: http://go.microsoft.com/fwlink/?LinkId=517190
[Python 3.4 32 bits]: http://go.microsoft.com/fwlink/?LinkId=517191
[Documentation relative à Python Tools for Visual Studio]: http://aka.ms/ptvsdocs
[Débogage à distance sur Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=624026
[Projets web]: http://go.microsoft.com/fwlink/?LinkId=624027
[Projets de service cloud]: http://go.microsoft.com/fwlink/?LinkId=624028
[Documentation Django]: https://www.djangoproject.com/
[MySQL]: http://www.mysql.com/
[video]: http://youtu.be/oKCApIrS0Lo
