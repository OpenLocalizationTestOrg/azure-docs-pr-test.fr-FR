---
title: aaaHow tooMigrate et publier une Application Web de tooan du Service de Cloud Azure depuis Visual Studio | Documents Microsoft
description: "Découvrez comment toomigrate et publier votre tooan d’application web service cloud Azure à l’aide de Visual Studio."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 9394adfd-a645-4664-9354-dd5df08e8c91
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: a2832c37d2ebdbc1e69a307d16b65b1c87e9070c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-to-migrate-and-publish-a-web-application-tooan-azure-cloud-service-from-visual-studio"></a>Comment : migrer et publier une Application Web de tooan Azure Cloud Service à partir de Visual Studio
avantage tootake de hello hébergement des services et l’évolutivité de Azure, vous souhaitez toomigrate et publier votre service cloud Azure de tooan application web. Vous pouvez exécuter une application web dans Azure avec application de modifications minimales tooyour existante.

> [!NOTE]
> Cette rubrique est sur le déploiement de services toocloud, pas les sites tooweb. Pour plus d’informations sur le déploiement de sites de tooweb, consultez [déployer une application web dans Azure App Service](app-service-web/web-sites-deploy.md).
>
>

Pour obtenir la liste des modèles spécifiques qui sont pris en charge pour Visual c# et Visual Basic, consultez la section de hello **prise en charge des modèles de projet** plus loin dans cette rubrique.

Vous devez d'abord activer votre application web pour Azure à partir de Visual Studio. Hello suivant illustration montre hello étapes clés toopublish votre application web existante en ajoutant un toouse du projet Windows Azure pour le déploiement. Ce processus ajoute un projet Azure avec une solution tooyour rôle web hello requis. En fonction de type hello du projet web que vous avez, propriétés du projet hello pour les assemblys sont également mis à jour si le package de service hello exige des assemblys supplémentaires pour le déploiement.

![Publier un tooMicrosoft d’application Web Azure](./media/vs-azure-tools-migrate-publish-web-app-to-cloud-service/IC748917.png)

> [!NOTE]
> Hello **convertir**, **convertir tooAzure projet de Service Cloud** commande s’affiche uniquement pour les projets web de hello dans votre solution. Par exemple, la commande hello n’est pas disponible pour un projet Silverlight dans votre solution.
> Lorsque vous créez un package de service ou que vous publiez votre application tooAzure, des avertissements ou erreurs peuvent se produire. Ces avertissements et erreurs peuvent vous aider à résoudre les problèmes avant de déployer tooAzure. Par exemple, vous pouvez recevoir un avertissement signalant un assembly manquant. Pour plus d’informations sur comment tootreat les avertissements comme des erreurs, consultez [configurer un projet de Service Cloud Azure avec Visual Studio](vs-azure-tools-configuring-an-azure-project.md). Si vous générez votre application, l’exécuter localement à l’aide d’émulateur de calcul hello ou tooAzure le publier, vous pouvez voir hello erreur Bonjour suivante **liste d’erreurs** fenêtre : **hello spécifié le chemin d’accès, le nom de fichier, ou les deux sont trop longs** . Cette erreur se produit parce que la longueur du nom qualifié complet du projet Azure de hello hello est trop longue. Hello du nom de projet hello, y compris le chemin d’accès complet de hello, ne peut pas comporter plus de 146 caractères. Par exemple, c’est le nom de projet complet hello, y compris le chemin d’accès pour un projet Windows Azure qui est créé pour une application Silverlight : `c:\users\<user name>\documents\visual studio 2015\Projects\SilverlightApplication4\SilverlightApplication4.Web.Azure.ccproj`. Vous pouvez avoir toomove votre solution tooa autre répertoire qui a une chemin d’accès tooreduce hello courte du nom qualifié complet du projet de hello.
>
>

toomigrate et publier un tooAzure d’application web à partir de Visual Studio, procédez comme suit.

## <a name="enable-a-web-application-for-deployment-tooazure"></a>Activer une Application Web pour le déploiement tooAzure
### <a name="tooenable-a-web-application-for-deployment-tooazure"></a>tooenable une application web pour le déploiement tooAzure
1. tooenable votre application web pour le déploiement tooAzure, menu contextuel hello ouvrir un site web dans votre solution de projet et choisissez Ajouter un projet de déploiement Azure.

    Hello suivant des actions se produire :

   * Un projet Azure appelé `<name of hello web project>.Azure` est ajouté solution toohello pour votre application.
   * Un rôle web pour le projet web de hello est ajouté toothis projet Windows Azure.
   * Hello **copie locale** propriété a la valeur tootrue pour tous les assemblys qui sont requis pour MVC 2, MVC 3, MVC 4 et Silverlight Business Applications. Cette opération ajoute ces assemblys toohello package de service du qui est utilisé pour le déploiement.

   > [!IMPORTANT]
   > Si vous avez d’autres assemblys ou les fichiers qui sont requis pour cette application web, vous devez définir manuellement les propriétés hello pour ces fichiers. Pour plus d’informations sur comment tooset ces propriétés, consultez hello section **des fichiers Include dans hello Package de Service** plus loin dans cet article.
   >
   > [!NOTE]
   > Si un rôle web pour un projet web spécifique existe déjà dans un projet Windows Azure dans la solution de hello, **convertir**, **convertir tooAzure projet de Service Cloud** ne figure pas dans le menu contextuel de hello pour ce projet web .
   >
   >

   Si vous avez plusieurs projets web dans votre application web et que vous souhaitez toocreate les rôles web pour chaque projet web, vous devez effectuer les étapes de hello dans cette procédure pour chaque projet web. Ceci crée des projets Azure distincts pour chaque rôle web. Chaque projet web peut être publié séparément. Ou bien, vous pouvez ajouter manuellement un autre rôle tooan existant Azure projet web dans votre application web. toodo, menu contextuel Ouvrir hello hello **rôles** dossier dans votre projet Windows Azure, choisissez **ajouter**, puis **le projet de rôle Web dans la solution**, choisissez tooadd de projet hello comme un site web rôle, puis choisissez hello **OK** bouton.

## <a name="use-an-azure-sql-database-for-your-application"></a>Utilisation d’une base de données SQL Azure pour votre application
Si vous avez une chaîne de connexion pour votre application web qui utilise une base de données SQL Server locale hello, vous devez modifier cette toouse de chaîne de connexion une instance de base de données SQL hébergée par Azure à la place.

> [!IMPORTANT]
> Votre abonnement vous devez activer toouse base de données SQL. Si vous accédez à votre abonnement hello [portail Azure classic](http://go.microsoft.com/fwlink/?LinkID=213885), vous pouvez déterminer les services fournis par votre abonnement. Hello instructions ci-après s’appliquent toohello publié [portail Azure classic](http://go.microsoft.com/fwlink/?LinkID=213885). Si vous utilisez hello [portail Azure](http://portal.microsoft.com), ignorer la procédure suivante de toohello.
>
>

### <a name="toouse-a-sql-database-instance-in-your-web-role-for-your-connection-string"></a>toouse une instance de la base de données SQL dans votre rôle web pour votre chaîne de connexion
1. toocreate une instance de base de données SQL dans hello [portail Azure classic](http://go.microsoft.com/fwlink/?LinkID=213885), suivez les étapes de hello Bonjour l’article suivant : [créer une base de données SQL Server](http://go.microsoft.com/fwlink/?LinkId=225109).

   > [!NOTE]
   > Lorsque vous définissez des règles de pare-feu hello pour votre instance de base de données SQL, vous devez sélectionner hello **autoriser autres tooaccess services Azure à ce serveur** case à cocher.
   >
   >
2. toocreate une instance de toouse de base de données SQL pour votre chaîne de connexion, suivez les étapes de hello dans hello prochaine section dans l’article suivant de hello : [créer une base de données SQL](http://go.microsoft.com/fwlink/?LinkId=225110).
3. toocopy hello ADO.NET connexion chaîne toouse pour votre chaîne de connexion, effectuez hello comme suit dans hello [portail Azure classic](http://go.microsoft.com/fwlink/?LinkID=213885).  

   1. Choisissez hello **base de données** bouton et nœud hello puis ouvert pour l’abonnement hello que vous avez utilisé toocreate votre instance de base de données SQL.
   2. instances disponibles de hello toodisplay de base de données SQL, choisissez hello **bases de données SQL** nœud.
   3. propriétés de hello toodisplay pour la base de données hello, choisissez la base de données de hello. Hello **propriétés** s’affiche.

      > [!NOTE]
      > Si hello **propriétés** vue n’apparaît pas, vous devrez peut-être tooopen à l’aide de hello diviseur.
      >
      >
   4. chaînes de connexion toodisplay hello, choisissez tooView suivant du bouton points de suspension (...) hello.

      Hello **les chaînes de connexion** boîte de dialogue s’affiche.
   5. toocopy hello chaîne de connexion ADO.NET, mettez en surbrillance le texte hello et appuyez sur Ctrl + C hello.
   6. boîte de dialogue tooclose hello, choisissez hello **fermer** bouton.
4. connexion de hello tooreplace chaîne hello web.config fichier toouse de cette instance de base de données SQL, ouvrez le fichier web.config de hello, mettre en surbrillance d’entrée de chaîne de connexion existante hello, puis choisissez les touches Ctrl + V de hello. Hello chaîne de connexion ADO.NET pour l’instance de hello de base de données SQL remplace la chaîne de connexion existante hello.
5. Vous devez également ajouter le paramètre hello `MultipleActiveResultSets=True` chaîne de connexion toohello. chaîne de connexion Hello doit avoir hello suivant le format :

    ```
    connectionString=”Server=tcp:<database_server>.database.windows.net,1433;Database=<database_name>;User ID=<user_name>@<database_server>;Password=<myPassword>;Trusted_Connection=False;Encrypt=True;MultipleActiveResultSets=True"
    ```
6. (Facultatif) Une chaîne de connexion de méthode alternative toochanging hello directement dans le fichier web.config de hello est tooadd une section dans un des fichiers de transformation web.config hello, selon la configuration de build hello utiliser toocreate votre package de services. Ouvrez le fichier de Web.Debug.Config hello ou hello Web.Release.Config. Ajoutez hello suivant la section dans ce fichier :

    ```
    XMLCopy<connectionStrings><addname="DefaultConnection"connectionString="Server=tcp:<database_server>.database.windows.net,1433;Database=<database_name>;User ID=<user_name>@<database_server>;Password=<myPassword>;Trusted_Connection=False;Encrypt=True;MultipleActiveResultSets=True"xdt:Transform="SetAttributes"xdt:Locator="Match(name)"/></connectionStrings>
    ```
7. Enregistrez le fichier hello que vous avez modifié et republiez votre application.

### <a name="toouse-an-instance-of-sql-database-by-using-hello-azure-classic-portal"></a>une instance de base de données SQL à l’aide de toouse hello portail Azure classic
1. Bonjour [portail Azure classic](http://go.microsoft.com/fwlink/?LinkID=213885), choisissez le nœud bases de données SQL de hello.

   * Si l’instance hello de base de données SQL que vous souhaitez toouse s’affiche, choisissez tooopen il.
   * Si vous n’avez pas créé de toutes les instances, choisissez le lien approprié de hello, puis créez une instance.
2. Une fois que vous ouvrez ou créez une instance de la base de données, choisissez hello **les chaînes de connexion** lien.
3. Au bas de hello de page de hello, choisissez les paramètres de pare-feu tooconfigure lien hello et accepter les valeurs par défaut de hello ou valeurs hello dont vous avez besoin de configurer.
4. Copier la chaîne de connexion hello ADO.NET, collez-la dans votre fichier web.config sur hello ancienne chaîne de connexion de base de données locale de hello et être tooadd vraiment `MultipleActiveResultSets=True`.

## <a name="publish-a-web-application-tooazure"></a>Publier une Application Web de tooAzure
### <a name="toopublish-a-web-application-tooazure"></a>toopublish un tooAzure d’application Web
1. application de hello tootest dans l’environnement de développement local hello à l’aide d’émulateur de calcul Azure hello, hello Azure sur le menu contextuel hello ouvrir de projet de rôle web de hello et choisissez **définir comme projet de démarrage**. Sélectionnez ensuite **Déboguer**, **Démarrer le débogage** (clavier : **F5**).

    Hello **début hello environnement de débogage Azure** boîte de dialogue s’ouvre et l’application hello démarre dans le navigateur de hello. Pour plus d’informations sur la manière dont les toostart chaque type d’application web Bonjour émulateur de calcul, voir le tableau hello dans cette section.
2. tooset les services de hello pour votre tooAzure de toopublish d’application, vous devez disposer d’un compte Microsoft et un abonnement Azure. Hello d’utiliser les étapes Bonjour suivant tooset rubrique vos services : [toopublish de préparer ou de déployer une application Windows Azure à partir de Visual Studio](vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio.md).
3. toopublish hello web application tooAzure, ouvrez le menu contextuel projet web de hello hello et choisissez **publier tooAzure**.

    Hello **publier l’Application Azure** boîte de dialogue s’ouvre et Visual Studio démarre le processus de déploiement hello. Pour plus d’informations sur comment toopublish hello application, consultez la section de hello **publier une Application Azure depuis Visual Studio** dans [publication d’un Service Cloud à l’aide des outils d’Azure hello](vs-azure-tools-publishing-a-cloud-service.md).

   > [!NOTE]
   > Vous pouvez également publier application hello web hello projet Windows Azure. toodo, ouvrez le menu contextuel hello hello projet Windows Azure et choisissez **publier**.
   >
   >
4. progression de hello toosee du déploiement de hello, vous pouvez afficher hello **journal des activités Azure** fenêtre. Ce fichier journal s’affiche automatiquement au démarrage du processus de déploiement hello. Vous pouvez développer hello élément de ligne dans le journal d’activité hello tooshow des informations détaillées, comme indiqué dans hello après l’illustration :

    ![VST_AzureActivityLog](./media/vs-azure-tools-migrate-publish-web-app-to-cloud-service/IC744149.png)
5. Processus de déploiement hello toocancel (facultatif), ouvrir le menu contextuel de hello pour l’élément de ligne hello dans le journal d’activité hello et choisissez **Annuler et supprimer**. Cela arrête le processus de déploiement hello et supprime l’environnement de déploiement hello de Azure.

   > [!NOTE]
   > tooremove cet environnement de déploiement après qu’il a été déployé, vous devez utiliser hello [portail Azure classic](http://go.microsoft.com/fwlink/?LinkID=213885).
   >
   >
6. (Facultatif) Après avoir démarré vos instances de rôle, Visual Studio affiche automatiquement un environnement de déploiement hello Bonjour **Azure Compute** nœud **Cloud Explorer** ou **l’Explorateur de serveurs**. À ce stade, vous pouvez afficher état hello hello individuelles d’instances de rôle.

    Hello l’illustration suivante montre des instances de rôle hello dans **l’Explorateur de serveurs** pendant qu’elles sont toujours en hello initialisation de l’état :

    ![VST_DeployComputeNode](./media/vs-azure-tools-migrate-publish-web-app-to-cloud-service/IC744134.png)
7. tooaccess votre application après le déploiement, choisissez hello flèche suivant tooyour déploiement lorsque le statut de **terminé** s’affiche dans hello **journal des activités Azure**. Cela affiche l’URL hello pour votre application web dans Azure. Consultez hello tableau pour hello plus d’informations sur comment toostart un type particulier d’application web à partir d’Azure.

    Hello tableau suivant répertorie les hello plus d’informations sur comment toostart web Azure ou toorun des applications ou déboguer une application web localement à l’aide de hello émulateur de calcul Azure :

   | Type d’application web | Exécution/débogage localement à l’aide de hello émulateur de calcul | Exécution dans Azure |
   | --- | --- | --- |
   | Application Web ASP.NET |Dans la barre de menus de hello, choisissez **déboguer**, **démarrer le débogage** (clavier : choisissez hello **F5** clé.). |Choisir un lien hypertexte de l’URL hello affiché dans hello **déploiement** onglet hello **journal des activités Azure** page de démarrage tooload hello dans le navigateur de hello. |
   | Application Web ASP.NET MVC 2 |Dans la barre de menus de hello, choisissez **déboguer**, **démarrer le débogage** (clavier : choisissez hello **F5** clé.). |Choisir un lien hypertexte de l’URL hello affiché dans hello **déploiement** onglet hello **journal des activités Azure** page de démarrage tooload hello dans le navigateur de hello. |
   | Application Web ASP.NET MVC 3 |Dans la barre de menus de hello, choisissez **déboguer**, **démarrer le débogage** (clavier : choisissez hello **F5** clé.). |Choisir un lien hypertexte de l’URL hello affiché dans hello **déploiement** onglet hello **journal des activités Azure** page de démarrage tooload hello dans le navigateur de hello. |
   | Application Web ASP.NET MVC 4 |Dans la barre de menus de hello, choisissez **déboguer**, **démarrer le débogage** (clavier : choisissez hello **F5** clé.). |Choisir un lien hypertexte de l’URL hello affiché dans hello **déploiement** onglet hello **journal des activités Azure** page de démarrage tooload hello dans le navigateur de hello. |
   | Application Web vide ASP.NET |Vous devez ajouter une page .aspx dans votre application et la définir comme page de démarrage hello pour votre projet web. Sur la barre de menus de hello, puis **déboguer**, **démarrer le débogage** (clavier : choisissez hello **F5** clé.). |Si vous avez une page .aspx de valeur par défaut dans votre application, choisissez le lien d’URL de hello affiché dans hello **déploiement** onglet hello **journal des activités Azure** cette page est chargée dans le navigateur de hello. Si vous avez une page .aspx différente, vous devez page spécifique de toonavigate toothis à l’aide de hello respectant le format pour l’url :`<url for deployment>/<name of page>.aspx` |
   | Application Silverlight |Dans la barre de menus de hello, choisissez **déboguer**, **démarrer le débogage** (clavier : choisissez hello **F5** clé.). |Vous devez toonavigate toohello une page spécifique de votre application à l’aide de hello respectant le format pour l’url :`<url for deployment>/<name of page>.aspx` |
   | Silverlight Business Application |Dans la barre de menus de hello, choisissez **déboguer**, **démarrer le débogage** (clavier : choisissez hello **F5** clé.). |Vous devez toonavigate toohello une page spécifique de votre application à l’aide de hello respectant le format pour l’url :`<url for deployment>/<name of page>.aspx` |
   | Silverlight Navigation Application |Dans la barre de menus de hello, choisissez **déboguer**, **démarrer le débogage** (clavier : choisissez hello **F5** clé.). |Vous devez toonavigate toohello une page spécifique de votre application à l’aide de hello respectant le format pour l’url :`<url for deployment>/<name of page>.aspx` |
   | WCF Service Application |Vous devez définir le fichier .svc de hello comme hello page de démarrage de votre projet de Service WCF. Sur la barre de menus de hello, puis **déboguer**, **démarrer le débogage** (clavier : choisissez hello **F5** clé.). |Vous avez besoin de fichier svc de toohello toonavigate pour votre application à l’aide de hello respectant le format pour l’url :`<url for deployment>/<name of service file>.svc` |
   | WCF Workflow Service Application |Vous devez définir le fichier .svc de hello comme hello page de démarrage de votre projet de Service WCF. Sur la barre de menus de hello, puis **déboguer**, **démarrer le débogage** (clavier : choisissez hello **F5** clé.). |Vous avez besoin de fichier svc de toohello toonavigate pour votre application à l’aide de hello respectant le format pour l’url :`<url for deployment>/<name of service file>.svc` |
   | ASP.NET Dynamic Entities |Dans la barre de menus de hello, choisissez **déboguer**, **démarrer le débogage** (clavier : choisissez hello **F5** clé.). |Vous devez mettre à jour la chaîne de connexion hello (voir la section suivante). Vous devez également toonavigate toohello une page spécifique de votre application à l’aide de hello respectant le format pour l’url :`<url for deployment>/<name of page>.aspx` |
   | ASP.NET Dynamic Data ASP.NET Linq tooSQL |Dans la barre de menus de hello, choisissez **déboguer**, **démarrer le débogage** (clavier : choisissez hello **F5** clé.). |Vous devez suivre les étapes de hello dans cette procédure : utiliser une base de données SQL Azure pour votre application (voir la section plus haut dans cette rubrique). Vous devez également toonavigate toohello une page spécifique de votre application à l’aide de hello respectant le format pour l’url :`<url for deployment>/<name of page>.aspx` |

## <a name="update-a-connection-string-for-aspnet-dynamic-entities"></a>Mise à jour d’une chaîne de connexion pour ASP.NET Dynamic Entities
### <a name="tooupdate-a-connection-string-for-aspnet-dynamic-entities"></a>tooUpdate une chaîne de connexion pour ASP.NET Dynamic Entities
1. toocreate une base de données SQL Azure qui peut être utilisé pour une application web ASP.NET Dynamic Entities, suivez les étapes de hello dans la procédure de hello **utiliser une base de données SQL Azure pour votre application** plus haut dans cette rubrique.
2. Ajouter des tables de hello et les champs dont vous avez besoin pour cette base de données à partir de hello [portail Azure classic](http://go.microsoft.com/fwlink/?LinkID=213885).
3. chaîne de connexion de Hello pour ce type d’application a hello suivant le format dans le fichier web.config de hello :  

    ```
    <addname="tempdbEntities"connectionString="metadata=res://*/Model1.csdl|res://*/Model1.ssdl|res://*/Model1.msl;provider=System.Data.SqlClient;provider connection string=&quot;data source=<server name>\SQLEXPRESS;initial catalog=<database name>;integrated security=True;multipleactiveresultsets=True;App=EntityFramework&quot;"providerName="System.Data.EntityClient"/>
    ```

    Hello de mise à jour *connectionString* valeur hello chaîne de connexion ADO.NET pour votre base de données SQL Azure comme suit :

    ```
    XMLCopy<addname="tempdbEntities"connectionString="metadata=res://*/Model1.csdl|res://*/Model1.ssdl|res://*/Model1.msl;provider=System.Data.SqlClient;provider connection string=&quot;Server=tcp:<SQL Azure server name>.database.windows.net,1433;Database=<database name>;User ID=<user name>;Password=<password>;Trusted_Connection=False;Encrypt=True;multipleactiveresultsets=True;App=EntityFramework&quot;"providerName="System.Data.EntityClient"/>
    ```
4. fichier de web.config hello toosave avec modifications hello que vous avez apportées chaîne de connexion toohello, sur la barre de menus hello choisissez **fichier**, **enregistrer web.config**.

## <a name="supported-project-templates"></a>Modèles de projet pris en charge
toopublish un tooAzure d’application web, application hello doit utiliser un des modèles de projet hello pour c# ou Visual Basic, qui est répertorié dans le tableau hello ci-dessous.

| Groupe de modèles de projet | Modèle de projet |
| --- | --- |
| Web |Application Web ASP.NET |
| Web |Application Web ASP.NET MVC 2 |
| Web |Application Web ASP.NET MVC 3 |
| Web |Application Web ASP.NET MVC 4 |
| Web |Application Web vide ASP.NET |
| Web |Application Web vide ASP.NET MVC 2 |
| Web |Application Web ASP.NET Dynamic Data Entities |
| Web |ASP.NET Dynamic Data ASP.NET Linq tooSQL Application Web |
| Silverlight |Application Silverlight |
| Silverlight |Silverlight Business Application |
| Silverlight |Silverlight Navigation Application |
| WCF |WCF Service Application |
| WCF |WCF Workflow Service Application |
| Workflow |WCF Workflow Service Application |

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur la publication, consultez [tooPublish de préparer ou de déployer une Application Azure depuis Visual Studio](vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio.md). Consultez également [Configuration des informations d’authentification nommées](vs-azure-tools-setting-up-named-authentication-credentials.md).
