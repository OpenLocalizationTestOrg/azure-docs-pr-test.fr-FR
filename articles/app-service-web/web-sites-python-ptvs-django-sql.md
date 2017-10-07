---
title: "aaaDjango et base de données SQL Azure avec 2.2 des outils Python pour Visual Studio"
description: "Découvrez comment toouse hello outils Python pour Visual Studio toocreate, une application web Django qui stocke les données dans une instance de la base de données SQL et le déployer tooAzure App Service Web Apps."
services: app-service\web
tags: python
documentationcenter: python
author: huguesv
manager: erikre
editor: 
ms.assetid: 3a677e64-b5a9-4d43-b9c0-66246368b483
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/07/2016
ms.author: huvalo
ms.openlocfilehash: b5b2ef4f3292e7df85007465c5394c8660a7d231
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="django-and-sql-database-on-azure-with-python-tools-22-for-visual-studio"></a>Django et SQL Database sur Azure avec Python Tools 2.2 pour Visual Studio
Dans ce didacticiel, nous allons utiliser [outils Python pour Visual Studio] toocreate simple interroge l’application web à l’aide d’un des exemples de modèles de PTVS hello. Ce didacticiel est également disponible en [vidéo](https://www.youtube.com/watch?v=ZwcoGcIeHF4).

Nous verrons comment toouse une base de données SQL hébergée sur Azure, comment tooconfigure hello toouse d’application web, une base de données SQL et comment toopublish hello web application trop[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).

Consultez hello [centre de développement Python] autres articles qui couvrent le développement de Azure App Service Web Apps avec PTVS à l’aide d’eau, ballon Django web et infrastructures, avec les services de stockage de Table Azure, MySQL et base de données SQL. Alors que cet article se concentre sur le Service d’applications, les étapes de hello sont similaires lors du développement [Azure Cloud Services].

## <a name="prerequisites"></a>Composants requis
* Visual Studio 2015
* [Python 2.7 32 bits]
* [Python Tools 2.2 pour Visual Studio]
* [2.2 des outils Python pour Visual Studio exemples VSIX]
* [Outils du Kit de développement logiciel (SDK) Azure pour Visual Studio 2015]
* Django 1.9 ou version ultérieure

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> Si vous souhaitez tooget démarré avec le Service d’application Azure avant de s’inscrire pour un compte Azure, accédez trop[essayez du Service d’applications](https://azure.microsoft.com/try/app-service/), où vous pouvez créer une application web de courte durée de démarrage immédiatement dans le Service d’applications. Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.
>
>

## <a name="create-hello-project"></a>Créer hello projet
Dans cette section, nous allons créer un projet Visual Studio à l’aide d’un exemple de modèle. Nous allons créer un environnement virtuel et installer les packages requis. Nous allons créer une base de données locale à l’aide de sqlite. Puis nous exécuterons hello web application localement.

1. Dans Visual Studio, sélectionnez **Fichier**, **Nouveau projet**.
2. Hello des modèles de projet à partir de hello [2.2 des outils Python pour Visual Studio exemples VSIX] sont disponibles sous **Python**, **exemples**. Sélectionnez **interroge Django Web projet** et cliquez sur OK toocreate hello projet.

     ![Boîte de dialogue Nouveau projet](./media/web-sites-python-ptvs-django-sql/PollsDjangoNewProject.png)
3. Vous serez invité à tooinstall les packages externes. Sélectionnez **Installer dans un environnement virtuel**.

     ![Boîte de dialogue Packages externes](./media/web-sites-python-ptvs-django-sql/PollsDjangoExternalPackages.png)
4. Sélectionnez **Python 2.7** comme interpréteur de base hello.

     ![Boîte de dialogue Ajouter un environnement virtuel](./media/web-sites-python-ptvs-django-sql/PollsCommonAddVirtualEnv.png)
5. Dans **l’Explorateur de solutions**, avec le bouton droit sur le nœud de projet hello et sélectionnez **Python**, puis sélectionnez **Django migrer**.  Sélectionnez ensuite **Django Create Superuser (Créer un superutilisateur Django)**.
6. Vous ouvrez une Console de gestion Django et créer une base de données sqlite dans le dossier de projet hello. Suivez les invites de hello toocreate un utilisateur.
7. Vérifier que l’application hello fonctionne en appuyant sur <kbd>F5</kbd>.
8. Cliquez sur **connecter** à partir de la barre de navigation hello haut hello.

     ![Navigateur web](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserLocalMenu.png)
9. Entrez des informations d’identification de hello pour utilisateur hello que vous avez créé lors de la synchronisation de base de données hello.

     ![Navigateur web](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserLocalLogin.png)
10. Cliquez sur **Create Sample Polls**.

      ![Navigateur web](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserNoPolls.png)
11. Cliquez sur un sondage et votez.

      ![Navigateur web](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqliteBrowser.png)

## <a name="create-a-sql-database"></a>Création d’une base de données SQL
Pour la base de données hello, nous allons créer une base de données SQL Azure.

Pour cela, procédez comme suit :

1. Ouvrez une session sur hello [Azure Portal].
2. Au bas de hello hello du volet de navigation, cliquez sur **nouveau**. Ensuite, cliquez sur **Données + stockage** > **Base de données SQL**.
3. Configurer hello de base de données SQL en créant un nouveau groupe de ressources et sélectionnez hello emplacement approprié.
4. Une fois hello de base de données SQL est créé, cliquez sur **ouvert dans Visual Studio** dans le panneau de base de données hello.
5. Cliquez sur **Configurer votre pare-feu**.
6. Bonjour **les paramètres de pare-feu** panneau, ajouter une règle de pare-feu avec **IP de début** et **IP de fin** définir toohello une adresse IP publique de votre ordinateur de développement. Cliquez sur **Enregistrer**.

   Cela permettra de serveur de base de données toohello de connexions à partir de votre ordinateur de développement.
7. Dans le panneau de la base de données hello, cliquez sur **propriétés**, puis cliquez sur **afficher les chaînes de connexion de base de données**.
8. Utilisez hello copie bouton tooput hello valeur **ADO.NET** Presse-papiers de hello.

## <a name="configure-hello-project"></a>Configurer hello projet
Dans cette section, nous allons configurer notre web application toouse hello SQL de base de données créée. Nous allons également installer Python packages requis toouse SQL bases de données supplémentaires avec Django. Puis nous exécuterons hello web application localement.

1. Dans Visual Studio, ouvrez **settings.py**, à partir de hello *nom_projet* dossier. Collez temporairement chaîne de connexion hello dans l’éditeur de hello. chaîne de connexion Hello est au format suivant :

       Server=<ServerName>,<ServerPort>;Database=<DatabaseName>;User ID=<UserName>;Password={your_password_here};Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;

Modifier la définition de hello de `DATABASES` toouse les valeurs hello ci-dessus.

        DATABASES = {
            'default': {
                'ENGINE': 'sql_server.pyodbc',
                'NAME': '<DatabaseName>',
                'USER': '<UserName>',
                'PASSWORD': '{your_password_here}',
                'HOST': '<ServerName>',
                'PORT': '<ServerPort>',
                'OPTIONS': {
                    'driver': 'SQL Server Native Client 11.0',
                    'MARS_Connection': 'True',
                }
            }
        }

1. Dans l’Explorateur de solutions, sous **environnements Python**, avec le bouton droit sur l’environnement virtuel de hello et sélectionnez **Package d’installation de Python**.
2. Installer le package de hello `pyodbc` à l’aide de **pip**.

     ![Boîte de dialogue Installer le package Python](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqlInstallPackagePyodbc.png)
3. Installer le package de hello `django-pyodbc-azure` à l’aide de **pip**.

     ![Boîte de dialogue Installer le package Python](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqlInstallPackageDjangoPyodbcAzure.png)
4. Dans **l’Explorateur de solutions**, avec le bouton droit sur le nœud de projet hello et sélectionnez **Python**, puis sélectionnez **Django migrer**.  Sélectionnez ensuite **Django Create Superuser (Créer un superutilisateur Django)**.

   Cela va créer les tables de base de données SQL hello que nous avons créé dans la section précédente de hello hello. Suivez les invites de hello toocreate un utilisateur, qui n’a pas utilisateur de hello toomatch dans la base de données sqlite hello créé dans la première section de hello.
5. Exécutez l’application hello avec `F5`. Les interrogations sont créées avec **créer des sondages exemple** et données hello soumises par le vote seront sérialisées dans la base de données SQL hello.

## <a name="publish-hello-web-app-tooazure-app-service"></a>Publier hello web application tooAzure du Service d’applications
Hello Kit de développement .NET Azure fournit un moyen simple de toodeploy votre tooAzure d’application web web App Service Web Apps.

1. Dans **l’Explorateur de solutions**, avec le bouton droit sur le nœud de projet hello et sélectionnez **publier**.

     ![Boîte de dialogue Publier le site Web](./media/web-sites-python-ptvs-django-sql/PollsCommonPublishWebSiteDialog.png)
2. Cliquez sur **Microsoft Azure Web Apps**.
3. Cliquez sur **nouveau** toocreate une application web.
4. Renseignez hello suivant des champs, cliquez sur **créer**.

   * **Nom de l’application web**
   * **Plan App Service**
   * **Groupe de ressources**
   * **Région**
   * Laissez **serveur de base de données** défini trop**aucune base de données**
5. Acceptez toutes les valeurs par défaut et cliquez sur **Publier**.
6. Votre navigateur web s’ouvre automatiquement toohello publié web app. Vous devez voir le travail d’application hello web comme prévu, à l’aide de hello **SQL** base de données hébergée sur Azure.

   Félicitations !

     ![Navigateur web](./media/web-sites-python-ptvs-django-sql/PollsDjangoAzureBrowser.png)

## <a name="next-steps"></a>Étapes suivantes
Suivez ces liens de toolearn plus d’informations sur les outils Python pour Visual Studio, Django et base de données SQL.

* [Documentation relative à Python Tools for Visual Studio]
  * [Projets web]
  * [Projets de service cloud]
  * [Débogage à distance sur Microsoft Azure]
* [Documentation Django]
* [Base de données SQL]

## <a name="whats-changed"></a>Changements apportés
* Pour un toohello guide voir changer à partir de sites Web tooApp Service : [Azure App Service et son Impact sur les Services Azure existants](http://go.microsoft.com/fwlink/?LinkId=529714)

<!--Link references-->
[centre de développement Python]: /develop/python/
[Azure Cloud Services]: ../cloud-services/cloud-services-python-ptvs.md

<!--External Link references-->
[Azure Portal]: https://portal.azure.com
[outils Python pour Visual Studio]: http://aka.ms/ptvs
[Python Tools 2.2 pour Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[2.2 des outils Python pour Visual Studio exemples VSIX]: http://go.microsoft.com/fwlink/?LinkID=624025
[Outils du Kit de développement logiciel (SDK) Azure pour Visual Studio 2015]: http://go.microsoft.com/fwlink/?LinkId=518003
[Python 2.7 32 bits]: http://go.microsoft.com/fwlink/?LinkId=517190
[Documentation relative à Python Tools for Visual Studio]: http://aka.ms/ptvsdocs
[Débogage à distance sur Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=624026
[Projets web]: http://go.microsoft.com/fwlink/?LinkId=624027
[Projets de service cloud]: http://go.microsoft.com/fwlink/?LinkId=624028
[Documentation Django]: https://www.djangoproject.com/
[Base de données SQL]: /documentation/services/sql-database/
