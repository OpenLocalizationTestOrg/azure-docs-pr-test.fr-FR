---
title: "aaaGet démarrer avec ASP.NET et les Services de cloud computing Azure | Documents Microsoft"
description: "Découvrez comment toocreate une application à plusieurs niveaux à l’aide d’ASP.NET MVC et Azure. application Hello s’exécute dans un service cloud, avec un rôle web et rôle de travail. Elle utilise Entity Framework, Base de données SQL et les files d'attente et objets blobs du stockage Azure."
services: cloud-services, storage
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: d7aa440d-af4a-4f80-b804-cc46178df4f9
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/15/2017
ms.author: adegeo
ms.openlocfilehash: 86271c29b79fad3f01f8ea0e88fd00c7aefc970c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-cloud-services-and-aspnet"></a>Prise en main des services cloud Azure et d'ASP.NET

## <a name="overview"></a>Vue d'ensemble
Ce didacticiel montre comment toocreate une application de .NET à plusieurs niveaux avec un frontal, ASP.NET MVC et déployez-le tooan [service cloud Azure](cloud-services-choose-me.md). Hello application utilise [base de données SQL Azure](http://msdn.microsoft.com/library/azure/ee336279), hello [service d’objets Blob Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage)et hello [service de file d’attente Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern). Vous pouvez [télécharger le projet de Visual Studio hello](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4) de hello MSDN Code Gallery.

didacticiel de Hello vous montre comment application hello toobuild et exécutez localement, comment toodeploy il tooAzure et hello exécution dans le cloud et comment toobuild à partir de zéro. Vous pouvez commencer par la génération à partir de zéro et puis hello test et déployer ensuite les étapes si vous préférez.

## <a name="contoso-ads-application"></a>Application Contoso Ads
application Hello est un forum de publicité. Les utilisateurs créent une publicité en entrant du texte et en téléchargeant une image. Ils peuvent voir une liste de publicités avec des images miniatures, et ils peuvent voir image en taille réelle de hello lorsqu’ils sélectionnent un ad toosee hello les détails.

![Ad list](./media/cloud-services-dotnet-get-started/list.png)

application Hello utilise hello [centré sur la file d’attente de travail modèle](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) travail hello sollicitant beaucoup le processeur de toooff en charge de la création de miniatures tooa au processus principal.

## <a name="alternative-architecture-websites-and-webjobs"></a>Autre architecture : Sites Web et WebJobs
Ce didacticiel montre comment toorun frontaux et principaux dans Azure cloud service. Une autre solution consiste à hello toorun frontal dans une [site Web Azure](/services/web-sites/) et utiliser hello [WebJobs](http://go.microsoft.com/fwlink/?LinkId=390226) fonctionnalité (actuellement en version préliminaire) pour le serveur principal hello. Pour obtenir un didacticiel qui utilise des tâches Web, consultez [prise en main hello Azure WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md). Pour plus d’informations sur comment toochoose hello services mieux adapter à votre scénario, consultez [comparaison de sites Web Azure, Services de cloud computing et machines virtuelles](../app-service-web/choose-web-site-cloud-service-vm.md).

## <a name="what-youll-learn"></a>Ce que vous allez apprendre
* Comment tooenable votre ordinateur pour le développement Azure en installant hello Azure SDK.
* Projet de service avec un rôle web d’ASP.NET MVC et un rôle de travail cloud toocreate Visual Studio.
* Comment tootest hello projet de service cloud localement, à l’aide d’émulateur de stockage Azure hello.
* Comment toopublish hello cloud projet tooan Azure cloud service et tester à l’aide d’un compte de stockage Azure.
* Comment tooupload les fichiers et les stocker dans le service d’objets Blob Azure hello.
* Comment toouse hello service de file d’attente Azure pour la communication entre les couches.

## <a name="prerequisites"></a>Composants requis
Hello didacticiel suppose que vous comprenez [concepts de base sur Azure cloud services](cloud-services-choose-me.md) comme *rôle web* et *rôle de travail* terminologie.  Il suppose également que vous savez comment toowork avec [ASP.NET MVC](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) ou [Web Forms](http://www.asp.net/web-forms/tutorials/aspnet-45/getting-started-with-aspnet-45-web-forms/introduction-and-overview) projets dans Visual Studio. exemple d’application Hello utilise MVC, mais hello didacticiel s’applique également tooWeb Forms.

Vous pouvez exécuter des application hello localement sans un abonnement Azure, mais vous aurez besoin d’un cloud de toohello application hello toodeploy. Si vous n’avez pas de compte, vous pouvez [activer les avantages de votre abonnement MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A55E3C668) ou [demander une évaluation gratuite](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A55E3C668).

instructions des didacticiels de Hello fonctionnent avec l’option de hello suite de produits :

* Visual Studio 2013
* Visual Studio 2015
* Visual Studio 2017

Si vous n’avez pas un de ces, Visual Studio peuvent être installé automatiquement lorsque vous installez hello Azure SDK.

## <a name="application-architecture"></a>Architecture de l'application
application Hello stocke des publicités dans une base de données SQL, à l’aide des tables de hello toocreate Entity Framework Code First et accéder aux données de hello. Pour chaque annonce, hello de base de données stocke deux URL, une pour hello image plein écran et l’autre pour l’image de hello.

![Ad table](./media/cloud-services-dotnet-get-started/adtable.png)

Lorsqu’un utilisateur télécharge une image, hello frontal en cours d’exécution dans un rôle web stocke image hello dans un [objets blob Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), et stocke des informations d’Active Directory hello dans base de données hello avec une URL qui pointe toohello blob. AT hello même temps, il écrit un message de tooan file d’attente Azure. Un processus principal en cours d’exécution régulièrement dans un rôle de travail interroge la file d’attente hello pour les nouveaux messages. Quand un nouveau message s’affiche, rôle de travail hello crée une miniature pour cette image et les mises à jour hello miniature champ de base de données d’URL pour qu’ad. Hello diagramme suivant montre comment hello de l’application hello interagissent.

![Contoso Ads architecture](./media/cloud-services-dotnet-get-started/apparchitecture.png)

[!INCLUDE [install-sdk](../../includes/install-sdk-2017-2015-2013.md)]

## <a name="download-and-run-hello-completed-solution"></a>Téléchargez et exécutez la solution de hello terminée
1. Téléchargez et décompressez hello [complété solution](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4).
2. Démarrez Visual Studio.
3. À partir de hello **fichier** menu Choisissez **ouvrir un projet**, accédez toowhere que vous avez téléchargé les solutions hello et puis ouvrez le fichier de solution hello.
4. Appuyez sur solution de hello toobuild CTRL + MAJ + B.

    Par défaut, Visual Studio restaure automatiquement le contenu du package NuGet hello, qui n’est pas compris dans hello *.zip* fichier. Si les packages hello ne sont pas restaurées, installez-les manuellement en accédant de toohello **gérer les Packages NuGet pour la Solution** boîte de dialogue et en cliquant sur hello **restaurer** bouton à droite en haut hello.
5. Dans **l’Explorateur de solutions**, assurez-vous que **ContosoAdsCloudService** est sélectionné comme projet de démarrage hello.
6. Si vous utilisez Visual Studio 2015 ou version ultérieure, chaîne de connexion SQL Server hello dans l’application hello *Web.config* fichier de projet de ContosoAdsWeb hello et hello *ServiceConfiguration.Local.cscfg* le fichier de projet de ContosoAdsCloudService hello. Dans chaque cas, « (localdb) \v11.0 » également modifier « (localdb) \MSSQLLocalDB ».
7. Appuyez sur la touche application de hello toorun CTRL + F5.

    Lorsque vous exécutez un projet de service cloud localement, Visual Studio appelle automatiquement hello Azure *émulateur de calcul* et Azure *l’émulateur de stockage*. utilisations de l’émulateur de calcul Hello rôle web de votre ordinateur ressources toosimulate hello et les environnements de rôle de travail. l’émulateur de stockage Hello utilise un [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) toosimulate stockage du cloud Azure de base de données.

    Hello première fois que vous exécutez un projet de service cloud, il prend environ une minute pour toostart d’émulateurs hello des. Lors du démarrage d’émulateur terminé, navigateur par défaut de hello ouvre la page d’accueil toohello application.

    ![Contoso Ads architecture](./media/cloud-services-dotnet-get-started/home.png)
8. Cliquez sur **Créer une publicité**.
9. Entrez des données de test et sélectionnez un *.jpg* tooupload de l’image, puis cliquez sur **créer**.

    ![Create page](./media/cloud-services-dotnet-get-started/create.png)

    application Hello passe toohello page d’Index, mais elle n’affiche une miniature de publicité hello parce que ce traitement n’a pas encore s’est produite.
10. Patientez quelques instants, puis actualisez hello Index toosee hello vignette.

     ![Page d'index](./media/cloud-services-dotnet-get-started/list.png)
11. Cliquez sur **détails** pour votre image en taille réelle d’ad toosee hello.

     ![Details page](./media/cloud-services-dotnet-get-started/details.png)

Vous avez déjà exécuté application hello entièrement sur votre ordinateur local, sans cloud toohello de connexion. émulateur de stockage Hello stocke la file d’attente hello et les données blob dans une base de données SQL Server Express LocalDB et application hello stocke des données d’Active Directory de hello dans une autre base de données de base de données locale. Entity Framework Code First hello créé automatiquement base de données ad hello première tooaccess a tenté de l’application web hello il.

Bonjour, suivant la section vous allez configurer les ressources de cloud computing Azure toouse la solution hello pour les files d’attente, les objets BLOB et base de données application hello lorsqu’il s’exécute dans le cloud de hello. Si vous souhaitiez toorun toocontinue localement mais utilisez des ressources de base de données et de stockage cloud, vous pouvez le faire. Il vous suffit de la définition de chaînes de connexion, vous verrez comment toodo.

## <a name="deploy-hello-application-tooazure"></a>Déployer hello application tooAzure
Vous effectuerez hello après application de hello toorun étapes dans le cloud de hello :

* Créez un service cloud Azure.
* Créez une base de données SQL Azure.
* Créez un compte de stockage Azure.
* Configurer hello solution toouse votre base de données SQL Azure lorsqu’elle s’exécute dans Azure.
* Configurer hello solution toouse votre compte de stockage Azure lorsqu’elle s’exécute dans Azure.
* Déployer un service de cloud computing Azure hello projet tooyour.

### <a name="create-an-azure-cloud-service"></a>Création d'un service cloud Azure
Un service cloud Azure est hello environnement hello application s’exécutera dans.

1. Dans votre navigateur, ouvrez hello [portail Azure](https://portal.azure.com).
2. Cliquez sur **Nouveau > Compute > Service cloud**.

3. Dans la zone d’entrée du nom DNS hello, entrez un préfixe d’URL pour le service cloud hello.

    Cette URL a toobe unique.  Vous obtenez un message d’erreur si vous choisissez de préfixe de hello est déjà en cours d’utilisation.
4. Spécifiez un groupe de ressources pour le service de hello. Cliquez sur **nouvel** puis tapez un nom dans hello ressource groupe zone d’entrée, tels que CS_contososadsRG.

5. Choisissez une région où vous souhaitez application hello de toodeploy hello.

    Ce champ indique le centre de données dans lequel votre service cloud sera hébergé. Pour une application de production, vous choisissez les clients tooyour le plus proche hello région. Pour ce didacticiel, choisissez tooyou le plus proche de la région de hello.
5. Cliquez sur **Créer**.

    Bonjour suivant l’image, un service cloud est créé par hello CSvccontosoads.cloudapp.net d’URL.

    ![New Cloud Service](./media/cloud-services-dotnet-get-started/newcs.png)

### <a name="create-an-azure-sql-database"></a>Création d’une base de données SQL Azure
Lorsque l’application hello s’exécute dans le cloud de hello, il utilise une base de données en nuage.

1. Bonjour [portail Azure](https://portal.azure.com), cliquez sur **Nouveau > bases de données > base de données SQL**.
2. Bonjour **nom de la base de données** , entrez *contosoads*.
3. Bonjour **groupe de ressources**, cliquez sur **utiliser l’existante** et groupe de ressources hello sélectionnez utilisé pour le service cloud hello.
4. Bonjour suivant de l’image, cliquez sur **Server - configurer les paramètres requis** et **créer un nouveau serveur**.

    ![Serveur toodatabase de tunnel](./media/cloud-services-dotnet-get-started/newdb.png)

    Vous pouvez également, si votre abonnement possède déjà un serveur, vous pouvez sélectionner ce serveur à partir de la liste déroulante de hello.
5. Bonjour **nom du serveur** , entrez *csvccontosodbserver*.

6. Entrez un **Nom de connexion** et un **Mot de passe** d’administrateur.

    Si vous avez sélectionné **Créer un serveur**, vous ne devez pas entrer un nom et un mot de passe existants ici. Vous entrez un nouveau nom et mot de passe que vous définissez maintenant toouse ultérieurement lorsque vous accédez à la base de données hello. Si vous avez sélectionné un serveur que vous avez créé précédemment, vous êtes invité à entrer pour le compte d’utilisateur administratif hello mot de passe toohello vous avez déjà créé.
7. Choisissez hello même **emplacement** que vous avez choisi pour le service cloud hello.

    Lorsque le service de cloud computing hello et la base de données sont dans différents centres de données (différentes régions), la latence augmentera, et vous serez facturé pour la bande passante en dehors du centre de données hello. alors qu'elle est gratuite dans un centre de données.
8. Vérifiez **server d’Autoriser les services azure tooaccess**.
9. Cliquez sur **sélectionnez** pour le nouveau serveur de hello.

    ![Nouveau serveur SQL Database](./media/cloud-services-dotnet-get-started/newdbserver.png)
10. Cliquez sur **Create**.

### <a name="create-an-azure-storage-account"></a>Création d'un compte de stockage Azure
Un compte de stockage Azure fournit des ressources pour le stockage de la file d’attente et les données blob dans le cloud de hello.

Dans une application réelle, on crée généralement des comptes distincts pour les données d'application et les données de journalisation, et des comptes distincts pour les données de test et les données de production. Pour ce didacticiel, vous allez utiliser un seul compte.

1. Bonjour [portail Azure](https://portal.azure.com), cliquez sur **Nouveau > stockage > compte de stockage - objet blob, de fichier, de table, de file d’attente**.
2. Bonjour **nom** , entrez un préfixe d’URL.

    Ce texte de préfixe plus hello que sous la zone de hello sera le compte de stockage hello unique URL tooyour. Si le préfixe hello que vous entrez a déjà été utilisé par quelqu'un d’autre, vous devrez toochoose un préfixe différent.
3. Ensemble hello **modèle de déploiement** trop*classique*.

4. Ensemble hello **réplication** déroulante liste trop**stockage localement redondant**.

    Lors de la géo-réplication est activée pour un compte de stockage, le contenu stockée hello est répliquées tooa centre de données secondaire tooenable basculement cas de sinistre majeur dans l’emplacement principal de hello. La géo-réplication peut engendrer des coûts supplémentaires. Pour les comptes de test et de développement, généralement non désirés toopay pour la géo-réplication. Pour plus d’informations, consultez [Création, gestion ou suppression d’un compte de stockage](../storage/common/storage-create-storage-account.md).

5. Bonjour **groupe de ressources**, cliquez sur **utiliser l’existante** et groupe de ressources hello sélectionnez utilisé pour le service cloud hello.
6. Ensemble hello **emplacement** toohello de liste déroulante, même région que vous avez choisi pour le service cloud hello.

    Lorsque le compte de service et le stockage cloud hello se trouvent dans différents centres de données (différentes régions), la latence augmentera, et vous serez facturé pour la bande passante en dehors du centre de données hello. alors qu'elle est gratuite dans un centre de données.

    Les groupes d’affinités Azure fournissent une mécanisme toominimize hello la distance entre les ressources dans un centre de données, ce qui peut réduire la latence. Ce didacticiel n'utilise pas de groupes d'affinités. Pour plus d’informations, consultez [comment tooCreate une affinité de groupe dans Azure](http://msdn.microsoft.com/library/jj156209.aspx).
7. Cliquez sur **Créer**.

    ![New storage account](./media/cloud-services-dotnet-get-started/newstorage.png)

    Dans l’image de hello, un compte de stockage est créé avec l’URL de hello `csvccontosoads.core.windows.net`.

### <a name="configure-hello-solution-toouse-your-azure-sql-database-when-it-runs-in-azure"></a>Configurer hello solution toouse votre base de données SQL Azure lorsqu’elle s’exécute dans Azure
Hello projet web et chaque projet de rôle Collaborateur hello possède sa propre chaîne de connexion de base de données, et chacune a besoin d’une base de données SQL Azure toopoint toohello lors de l’application hello s’exécute dans Azure.

Vous allez utiliser un [transformation Web.config](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/web-config-transformations) pour un rôle web de hello et un paramètre d’environnement de service cloud pour le rôle de travail hello.

> [!NOTE]
> Dans cette section et la section suivante de hello, vous stockez les informations d’identification dans les fichiers projet. [Ne stockez pas d'informations confidentielles dans des référentiels de code source publics](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets).
>
>

1. Dans le projet de ContosoAdsWeb hello, ouvrez hello *Web.Release.config* fichier de transformation de l’application hello *Web.config* , supprimez le bloc de commentaires hello contenant un `<connectionStrings>` élément et coller Hello suivant du code à la place.

    ```xml
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="{connectionstring}"
        providerName="System.Data.SqlClient" xdt:Transform="SetAttributes" xdt:Locator="Match(name)"/>
    </connectionStrings>
    ```

    Laissez le fichier de hello ouvert pour modification.
2. Bonjour [portail Azure](https://portal.azure.com), cliquez sur **bases de données SQL** dans le volet gauche de hello, cliquez sur base de données hello vous avez créé pour ce didacticiel, puis cliquez sur **afficher les chaînes de connexion**.

    ![Afficher les chaînes de connexion](./media/cloud-services-dotnet-get-started/showcs.png)

    portail de Hello affiche les chaînes de connexion, avec un espace réservé pour le mot de passe hello.

    ![Chaînes de connexion](./media/cloud-services-dotnet-get-started/connstrings.png)
3. Bonjour *Web.Release.config* de transformer le fichier, supprimez `{connectionstring}` et collez dans sa chaîne de connexion ADO.NET hello portail Azure de hello sur place.
4. Dans la chaîne de connexion hello que vous avez collé dans hello *Web.Release.config* de transformer le fichier, remplacez `{your_password_here}` avec le mot de passe hello créé pour la base de données SQL hello.
5. Enregistrez le fichier de hello.  
6. Sélectionnez et copiez la chaîne de connexion hello (sans hello entourant les guillemets) pour une utilisation dans hello comme suit pour configurer le projet de rôle de travail hello.
7. Dans **l’Explorateur de solutions**, sous **rôles** dans le projet de service cloud hello, cliquez sur **ContosoAdsWorker** puis cliquez sur **propriétés**.

    ![Role properties](./media/cloud-services-dotnet-get-started/rolepropertiesworker.png)
8. Cliquez sur hello **paramètres** onglet.
9. Modification **Configuration du Service** trop**Cloud**.
10. Sélectionnez hello **valeur** champ hello `ContosoAdsDbConnectionString` définition, puis collez la chaîne de connexion hello que vous avez copié à partir de la section précédente de hello du didacticiel de hello.

     ![Database connection string for worker role](./media/cloud-services-dotnet-get-started/workerdbcs.png)
11. Enregistrez vos modifications.  

### <a name="configure-hello-solution-toouse-your-azure-storage-account-when-it-runs-in-azure"></a>Configurer hello solution toouse votre compte de stockage Azure lorsqu’elle s’exécute dans Azure
Chaînes de connexion de compte de stockage Azure pour le projet de rôle web hello et projet de rôle de travail hello sont stockées dans les paramètres d’environnement dans le projet de service cloud hello. Pour chaque projet, il existe un ensemble distinct de toobe de paramètres utilisé lors de l’application hello s’exécute localement et lorsqu’elle est exécutée dans le cloud de hello. Vous allez mettre à jour les paramètres d’environnement cloud hello pour les projets de rôle web et de travail.

1. Dans **l’Explorateur de solutions**, avec le bouton droit **ContosoAdsWeb** sous **rôles** Bonjour **ContosoAdsCloudService** de projet, puis cliquez sur **Propriétés**.

    ![Role properties](./media/cloud-services-dotnet-get-started/roleproperties.png)
2. Cliquez sur hello **paramètres** onglet. Bonjour **Configuration du Service** liste déroulante, choisissez **Cloud**.

    ![Cloud configuration](./media/cloud-services-dotnet-get-started/sccloud.png)
3. Sélectionnez hello **StorageConnectionString** entrée et vous verrez des points de suspension (**...** ) situé à droite de hello de ligne de hello. Cliquez sur hello de tooopen de bouton de points de suspension hello **chaîne de connexion du compte de stockage créer** boîte de dialogue.

    ![Open Connection String Create box](./media/cloud-services-dotnet-get-started/opencscreate.png)
4. Bonjour **créer une chaîne de connexion stockage** boîte de dialogue, cliquez sur **votre abonnement**, choisissez le compte de stockage hello que vous avez créé précédemment, puis cliquez sur **OK**. Si vous n'êtes pas déjà connecté, vous êtes invité à entrer vos informations d'identification de compte Azure.

    ![Create Storage Connection String](./media/cloud-services-dotnet-get-started/createstoragecs.png)
5. Enregistrez vos modifications.
6. Suivez hello même procédure que celle utilisée pour hello `StorageConnectionString` hello de tooset de chaîne de connexion `Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString` chaîne de connexion.

    Cette chaîne de connexion est utilisée pour la connexion.
7. Suivez hello même procédure que celle utilisée pour hello **ContosoAdsWeb** tooset de rôle les deux chaînes de connexion pour hello **ContosoAdsWorker** rôle. N’oubliez pas tooset **Configuration du Service** trop**Cloud**.

paramètres d’environnement Hello rôle que vous avez configuré à l’aide de hello interface utilisateur Visual Studio sont stockés dans hello fichiers dans le projet de ContosoAdsCloudService hello suivants :

* *ServiceDefinition.csdef* -définit les noms de paramètre hello.
* *ServiceConfiguration.Cloud.cscfg* -fournit des valeurs d’exécution dans le cloud de hello application hello.
* *ServiceConfiguration.Local.cscfg* -fournit des valeurs pour lorsque l’application hello exécute localement.

Par exemple, hello ServiceDefinition.csdef inclut hello suivant des définitions :

```xml
<ConfigurationSettings>
    <Setting name="StorageConnectionString" />
    <Setting name="ContosoAdsDbConnectionString" />
</ConfigurationSettings>
```

Et hello *ServiceConfiguration.Cloud.cscfg* fichier inclut les valeurs hello saisies pour ces paramètres dans Visual Studio.

```xml
<Role name="ContosoAdsWorker">
    <Instances count="1" />
    <ConfigurationSettings>
        <Setting name="StorageConnectionString" value="{yourconnectionstring}" />
        <Setting name="ContosoAdsDbConnectionString" value="{yourconnectionstring}" />
        <!-- other settings not shown -->

    </ConfigurationSettings>
    <!-- other settings not shown -->

</Role>
```

Hello `<Instances>` paramètre spécifie le nombre de hello de machines virtuelles Azure sur laquelle s’exécutera travailleur de hello code du rôle. Hello [étapes](#next-steps) section inclut des informations de toomore de liens sur la montée en puissance parallèle d’un service cloud,

### <a name="deploy-hello-project-tooazure"></a>Déployer hello projet tooAzure
1. Dans **l’Explorateur de solutions**, avec le bouton hello **ContosoAdsCloudService** cloud du projet, puis sélectionnez **publier**.

   ![Publish menu](./media/cloud-services-dotnet-get-started/pubmenu.png)
2. Bonjour **connectez-vous** étape Hello **publier l’Application Azure** Assistant, cliquez sur **suivant**.

    ![Sign in step](./media/cloud-services-dotnet-get-started/pubsignin.png)
3. Bonjour **paramètres** étape de l’Assistant de hello, cliquez sur **suivant**.

    ![Settings step](./media/cloud-services-dotnet-get-started/pubsettings.png)

    Hello des paramètres par défaut dans hello **avancé** onglet conviennent pour ce didacticiel. Pour plus d’informations sur l’onglet Avancé de hello, consultez [Assistant Publication d’Application Azure](http://msdn.microsoft.com/library/hh535756.aspx).
4. Bonjour **Résumé** étape, cliquez sur **publier**.

    ![Summary step](./media/cloud-services-dotnet-get-started/pubsummary.png)

   Hello **journal des activités Azure** fenêtre s’ouvre dans Visual Studio.
5. Cliquez sur Détails du déploiement icône tooexpand hello hello flèche droite.

    déploiement de Hello peut prendre jusqu'à too5 minutes ou plus toocomplete.

    ![Azure Activity Log window](./media/cloud-services-dotnet-get-started/waal.png)
6. Lorsque l’état du déploiement hello est terminée, cliquez sur hello **URL de l’application Web** application hello de toostart.
7. Vous pouvez maintenant tester application hello par la création, affichage et modification des annonces, comme vous le faisiez lorsque vous avez exécuté localement application hello.

> [!NOTE]
> Lorsque vous avez terminé de tester, supprimer ou arrêter le service cloud hello. Même si vous n’utilisez pas le service de cloud computing hello, il accumule des frais, car les ressources d’ordinateur virtuel sont réservées. Si vous le laissez s'exécuter, toute personne qui trouve votre URL peut créer et afficher des publicités. Bonjour [portail Azure](https://portal.azure.com), accédez toohello **vue d’ensemble** onglet pour votre service cloud, puis cliquez sur hello **supprimer** bouton en hello haut hello. Si vous souhaitez simplement tootemporarily empêcher d’autres utilisateurs d’accéder au site de hello, cliquez sur **arrêter** à la place. Dans ce cas, interrompt tooaccrue. Vous pouvez suivre un Bonjour de toodelete procédure comme compte de stockage et de la base de données SQL lorsque vous n’en avez plus besoin.
>
>

## <a name="create-hello-application-from-scratch"></a>Créer l’application hello à partir de zéro
Si vous n’avez pas encore téléchargé [application hello terminée](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4), faites-le maintenant. Vous allez copier les fichiers de hello téléchargé projet en projet hello.

Création d’application des annonces de Contoso hello implique hello comme suit :

* création d'une solution Visual Studio de service cloud ;
* mise à jour et ajout de packages NuGet ;
* définition des références d'un projet ;
* configuration des chaînes de connexion ;
* ajout de fichiers de code.

Après la création de la solution de hello, vous allez consulter le code hello toocloud unique les projets de service et objets BLOB Windows Azure et files d’attente.

### <a name="create-a-cloud-service-visual-studio-solution"></a>Création d'une solution Visual Studio de service cloud
1. Dans Visual Studio, choisissez **nouveau projet** de hello **fichier** menu.
2. Dans le volet gauche de hello Hello **nouveau projet** boîte de dialogue, développez **Visual C#** et choisissez **Cloud** modèles, puis choisissez hello **Azure Cloud Service** modèle.
3. Nommez le projet de hello et une solution ContosoAdsCloudService, puis cliquez sur **OK**.

    ![Nouveau projet](./media/cloud-services-dotnet-get-started/newproject.png)
4. Bonjour **nouveau Service Cloud Azure** boîte de dialogue zone, ajouter un rôle web et un rôle de travail. Nom de rôle web de hello ContosoAdsWeb et nommez le rôle de travail hello ContosoAdsWorker. (Utilisez l’icône de crayon hello dans hello volet droit toochange hello noms par défaut des rôles de hello).

    ![New Cloud Service Project](./media/cloud-services-dotnet-get-started/newcsproj.png)
5. Lorsque vous consultez hello **nouveau projet ASP.NET** boîte de dialogue rôle web de hello, choisissez le modèle MVC de hello, puis cliquez sur **modifier l’authentification**.

    ![Modifier l'authentification](./media/cloud-services-dotnet-get-started/chgauth.png)
6. Bonjour **modifier l’authentification** boîte de dialogue, choisissez **aucune authentification**, puis cliquez sur **OK**.

    ![Aucune authentification](./media/cloud-services-dotnet-get-started/noauth.png)
7. Bonjour **nouveau projet ASP.NET** boîte de dialogue, cliquez sur **OK**.
8. Dans **l’Explorateur de solutions**, avec le bouton droit de solution hello (pas un des projets de hello), puis choisissez **Ajouter - nouveau projet**.
9. Bonjour **ajouter un nouveau projet** boîte de dialogue, choisissez **Windows** sous **Visual C#** dans hello du volet gauche, puis cliquez sur hello **bibliothèque de classes** modèle.  
10. Projet de hello nom *ContosoAdsCommon*, puis cliquez sur **OK**.

    Vous devez tooreference hello Entity Framework hello et contexte de modèle de données à partir de projets de rôle web et de travail. En guise d’alternative, vous pouvez définir des classes de lié à EF hello dans le projet de rôle web hello et faire référence à ce projet à partir du projet de rôle de travail hello. Mais dans une autre approche de hello, votre projet de rôle de travail aurait un assemblys tooweb de référence qui n’a pas besoin.

### <a name="update-and-add-nuget-packages"></a>Mise à jour et ajout de packages NuGet
1. Ouvrez hello **gérer les Packages NuGet** boîte de dialogue pour la solution de hello.
2. Haut hello de fenêtre hello, sélectionnez **mises à jour**.
3. Recherchez hello *WindowsAzure.Storage* du package et s’il est dans la liste de hello, sélectionnez-le et sélectionnez tooupdate de projets web et de travail hello dans, puis cliquez sur **mise à jour**.

    bibliothèque cliente de stockage Hello est mis à jour plus fréquemment que les modèles de projet Visual Studio, vous trouverez souvent que la version hello dans un toobe de besoins nouvellement créé le projet mis à jour.
4. Haut hello de fenêtre hello, sélectionnez **Parcourir**.
5. Recherche hello *EntityFramework* NuGet package et l’installer dans les trois projets.
6. Recherche hello *Microsoft.WindowsAzure.ConfigurationManager* NuGet package et l’installer dans le projet de rôle de travail hello.

### <a name="set-project-references"></a>Définition des références de projet
1. Dans le projet de ContosoAdsWeb hello, définissez une référence de projet de ContosoAdsCommon toohello. Projet de ContosoAdsWeb hello d’avec le bouton droit, puis cliquez sur **références** - **ajouter des références**. Bonjour **Gestionnaire de références** boîte de dialogue, sélectionnez **Solution – projets** dans le volet gauche de hello, sélectionnez **ContosoAdsCommon**, puis cliquez sur **OK**.
2. Dans le projet de ContosoAdsWorker hello, définissez une référence de projet de ContosAdsCommon toohello.

    ContosoAdsCommon contiendra hello Entity Framework modèle et le contexte de classe de données, qui sera utilisée par les deux hello frontaux et principaux.
3. Dans le projet de ContosoAdsWorker hello, définissez une référence trop`System.Drawing`.

    Cet assembly est utilisé par hello principal tooconvert images toothumbnails.

### <a name="configure-connection-strings"></a>Configuration des chaînes de connexion
Dans cette section, vous allez configurer les chaînes de connexion Azure Storage et SQL pour un test local. instructions de déploiement de Hello plus haut dans le didacticiel de hello expliquent comment tooset connexion de hello chaînes pour quand hello application s’exécute dans le cloud de hello.

1. Hello ContosoAdsWeb projet, fichier Web.config de l’application hello ouvert, et suivant de hello insert `connectionStrings` élément après hello `configSections` élément.

    ```xml
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;" providerName="System.Data.SqlClient" />
    </connectionStrings>
    ```

    Si vous utilisez Visual Studio 2015 ou version ultérieure, remplacez « v11.0 » par « MSSQLLocalDB ».
2. Enregistrez vos modifications.
3. Dans le projet de ContosoAdsCloudService hello, avec le bouton droit ContosoAdsWeb sous **rôles**, puis cliquez sur **propriétés**.

    ![Role properties](./media/cloud-services-dotnet-get-started/roleproperties.png)
4. Bonjour **ContosAdsWeb [rôle]** fenêtre Propriétés, cliquez sur hello **paramètres** onglet, puis cliquez sur **ajouter un paramètre**.

    Laissez **Configuration du Service** défini trop**toutes les Configurations**.
5. Ajoutez un paramètre nommé *StorageConnectionString*. Définissez **Type** trop*ConnectionString*et la valeur **valeur** trop*UseDevelopmentStorage = true*.

    ![New connection string](./media/cloud-services-dotnet-get-started/scall.png)
6. Enregistrez vos modifications.
7. Suivez hello même procédure tooadd une chaîne de connexion de stockage dans les propriétés du rôle ContosoAdsWorker hello.
8. Toujours en hello **ContosoAdsWorker [rôle]** fenêtre Propriétés, ajoutez une autre chaîne de connexion :

   * Nom : ContosoAdsDbConnectionString
   * Type : string
   * Valeur : Coller hello même chaîne de connexion que vous avez utilisé pour le projet de rôle web hello. (hello l’exemple suivant est pour Visual Studio 2013. N’oubliez pas toochange hello Source de données si vous copiez cet exemple et à l’aide de Visual Studio 2015 ou version ultérieure.)

       ```
       Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;
       ```

### <a name="add-code-files"></a>Ajout de fichiers de code
Dans cette section, vous copiez les fichiers de code à partir de la solution de hello téléchargé dans une nouvelle solution hello. Hello sections suivantes seront afficher et expliquer les éléments clés de ce code.

tooa projet ou un dossier, projet de hello avec le bouton droit ou un dossier et cliquez sur les fichiers tooadd **ajouter** - **élément existant**. Sélectionnez les fichiers hello puis cliquez sur **ajouter**. Si vous êtes invité tooreplace des fichiers existants, cliquez sur **Oui**.

1. Dans le projet de ContosoAdsCommon hello, supprimez hello *Class1.cs* et ajoutez son Bonjour place *Ad.cs* et *ContosoAdscontext.cs* fichiers à partir de hello téléchargé le projet.
2. Dans le projet de ContosoAdsWeb hello, ajoutez hello fichiers suivants à partir de projet de hello téléchargé.

   * *Global.asax.cs*.  
   * Bonjour *Views\Shared* dossier :  *\_Layout.cshtml*.
   * Bonjour *Views\Home* dossier : *Index.cshtml*.
   * Bonjour *contrôleurs* dossier : *AdController.cs*.
   * Bonjour *Views\Ad* dossier (créez d’abord le dossier de hello) : cinq *.cshtml* fichiers.
3. Dans le projet de ContosoAdsWorker hello, ajoutez *WorkerRole.cs* de hello téléchargé le projet.

Vous pouvez maintenant générer et exécuter l’application hello comme indiqué plus haut dans le didacticiel de hello, et l’application hello utilisera la base de données locale et les ressources d’émulateur de stockage.

Hello sections suivantes expliquent les code hello tooworking connexe avec hello environnement Azure, objets BLOB et files d’attente. Ce didacticiel n’explique pas comment les contrôleurs MVC toocreate et vues à l’aide de la structure, comment toowrite code Entity Framework qui fonctionne avec les bases de données SQL Server ou les principes de base hello de la programmation asynchrone dans ASP.NET 4.5. Pour plus d’informations sur ces sujets, consultez hello suivant des ressources :

* [Prise en main de MVC 5](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started)
* [Prise en main d’EF 6 et de MVC 5](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc)
* [Programmation de tooasynchronous introduction dans .NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async).

### <a name="contosoadscommon---adcs"></a>ContosoAdsCommon - Ad.cs
fichier de Ad.cs Hello définit un enum pour les catégories d’Active Directory et une classe d’entité POCO pour les informations Active Directory.

```csharp
public enum Category
{
    Cars,
    [Display(Name="Real Estate")]
    RealEstate,
    [Display(Name = "Free Stuff")]
    FreeStuff
}

public class Ad
{
    public int AdId { get; set; }

    [StringLength(100)]
    public string Title { get; set; }

    public int Price { get; set; }

    [StringLength(1000)]
    [DataType(DataType.MultilineText)]
    public string Description { get; set; }

    [StringLength(1000)]
    [DisplayName("Full-size Image")]
    public string ImageURL { get; set; }

    [StringLength(1000)]
    [DisplayName("Thumbnail")]
    public string ThumbnailURL { get; set; }

    [DataType(DataType.Date)]
    [DisplayFormat(DataFormatString = "{0:yyyy-MM-dd}", ApplyFormatInEditMode = true)]
    public DateTime PostedDate { get; set; }

    public Category? Category { get; set; }
    [StringLength(12)]
    public string Phone { get; set; }
}
```

### <a name="contosoadscommon---contosoadscontextcs"></a>ContosoAdsCommon - ContosoAdsContext.cs
Hello ContosoAdsContext classe spécifie que la classe de publicité de hello est utilisée dans une collection DbSet, Entity Framework seront stockés dans une base de données SQL.

```csharp
public class ContosoAdsContext : DbContext
{
    public ContosoAdsContext() : base("name=ContosoAdsContext")
    {
    }
    public ContosoAdsContext(string connString)
        : base(connString)
    {
    }
    public System.Data.Entity.DbSet<Ad> Ads { get; set; }
}
```

classe Hello possède deux constructeurs. Hello premier d'entre eux est utilisé par le projet web de hello et spécifie le nom de hello d’une chaîne de connexion qui est stockée dans le fichier Web.config de hello. constructeur de deuxième Hello vous permet de toopass dans la chaîne de connexion de hello utilisé par le projet de rôle de travail hello, car celui-ci ne dispose d’un fichier Web.config. Vous savez où cette chaîne de connexion a été stockée, et vous verrez plus tard comment les code hello récupère la chaîne de connexion hello lorsqu’il instancie la classe DbContext de hello.

### <a name="contosoadsweb---globalasaxcs"></a>ContosoAdsWeb - Global.asax.cs
Code qui est appelé à partir de hello `Application_Start` méthode crée un *images* conteneur d’objets blob et un *images* file d’attente si elles n’existent pas déjà. Cela garantit que chaque fois que vous débutiez à l’aide d’un compte de stockage, ou sur un nouvel ordinateur à l’aide de l’émulateur de stockage hello, file d’attente et le conteneur d’objets blob obligatoires hello seront créés automatiquement.

Hello compte de stockage toohello code obtient l’accès à l’aide de chaînes de connexion de stockage hello de hello *.cscfg* fichier.

```csharp
var storageAccount = CloudStorageAccount.Parse
    (RoleEnvironment.GetConfigurationSettingValue("StorageConnectionString"));
```

Ensuite, il obtient une référence toohello *images* conteneur d’objets blob, crée le conteneur de hello si elle n’existe pas déjà, et définit les autorisations sur le conteneur hello d’accès. Par défaut, des conteneurs autorisent uniquement les clients avec un compte de stockage BLOB de tooaccess d’informations d’identification. site Web de Hello doit hello BLOB toobe public afin qu’il peut afficher des images à l’aide de l’URL que BLOB d’image toohello de point de.

```csharp
var blobClient = storageAccount.CreateCloudBlobClient();
var imagesBlobContainer = blobClient.GetContainerReference("images");
if (imagesBlobContainer.CreateIfNotExists())
{
    imagesBlobContainer.SetPermissions(
        new BlobContainerPermissions
        {
            PublicAccess =BlobContainerPublicAccessType.Blob
        });
}
```

Un code similaire Obtient une référence toohello *images* file d’attente et crée une nouvelle file d’attente. Dans ce cas, aucune modification des autorisations n’est nécessaire.

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
var imagesQueue = queueClient.GetQueueReference("images");
imagesQueue.CreateIfNotExists();
```

### <a name="contosoadsweb---layoutcshtml"></a>ContosoAdsWeb - \_Layout.cshtml
Hello *_Layout.cshtml* fichier définit le nom de l’application hello dans l’en-tête de hello et de pied de page et crée une entrée de menu « Annonces ».

### <a name="contosoadsweb---viewshomeindexcshtml"></a>ContosoAdsWeb - Views\Home\Index.cshtml
Hello *Views\Home\Index.cshtml* fichier affiche les liens de catégorie sur la page d’accueil hello. les liens Hello passent entier hello hello `Category` enum dans une page d’Index de publicités toohello variable querystring.

```razor
<li>@Html.ActionLink("Cars", "Index", "Ad", new { category = (int)Category.Cars }, null)</li>
<li>@Html.ActionLink("Real estate", "Index", "Ad", new { category = (int)Category.RealEstate }, null)</li>
<li>@Html.ActionLink("Free stuff", "Index", "Ad", new { category = (int)Category.FreeStuff }, null)</li>
<li>@Html.ActionLink("All", "Index", "Ad", null, null)</li>
```

### <a name="contosoadsweb---adcontrollercs"></a>ContosoAdsWeb - AdController.cs
Bonjour *AdController.cs* fichier, les appels de constructeur Bonjour Bonjour `InitializeStorage` méthode toocreate bibliothèque cliente de stockage Azure objets qui fournissent une API pour l’utilisation des objets BLOB et files d’attente.

Code de hello Obtient une référence toohello *images* conteneur d’objets blob comme vous l’avez vu précédemment dans *Global.asax.cs*. Ce faisant, il définit une [stratégie de nouvelles tentatives](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) par défaut appropriée pour une application web. stratégie de nouvelle tentative interruption exponentielle Hello par défaut se bloque hello web app pour plus d’une minute sur les tentatives répétées d’une erreur transitoire. stratégie de nouvelle tentative Hello spécifié ici attend trois secondes après chacun pour des tentatives de toothree.

```csharp
var blobClient = storageAccount.CreateCloudBlobClient();
blobClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
imagesBlobContainer = blobClient.GetContainerReference("images");
```

Un code similaire Obtient une référence toohello *images* file d’attente.

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
queueClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
imagesQueue = queueClient.GetQueueReference("images");
```

La plupart du code du contrôleur hello est typique pour travailler avec un modèle de données Entity Framework à l’aide d’une classe DbContext. Une exception est hello HttpPost `Create` (méthode), qui télécharge un fichier et l’enregistre dans le stockage blob. classeur de modèles Hello fournit un [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) toohello méthode de l’objet.

```csharp
[HttpPost]
[ValidateAntiForgeryToken]
public async Task<ActionResult> Create(
    [Bind(Include = "Title,Price,Description,Category,Phone")] Ad ad,
    HttpPostedFileBase imageFile)
```

Si l’utilisateur hello sélectionné un tooupload de fichier, code de hello télécharge hello fichier enregistre dans un objet blob et met à jour d’enregistrement de base de données Ad hello avec une URL qui pointe toohello blob.

```csharp
if (imageFile != null && imageFile.ContentLength != 0)
{
    blob = await UploadAndSaveBlobAsync(imageFile);
    ad.ImageURL = blob.Uri.ToString();
}
```

Hello code hello téléchargement est hello `UploadAndSaveBlobAsync` (méthode). Il crée un nom GUID pour les objets blob de hello, téléchargements et enregistre le fichier hello et retourne un objet blob de référence toohello enregistré.

```csharp
private async Task<CloudBlockBlob> UploadAndSaveBlobAsync(HttpPostedFileBase imageFile)
{
    string blobName = Guid.NewGuid().ToString() + Path.GetExtension(imageFile.FileName);
    CloudBlockBlob imageBlob = imagesBlobContainer.GetBlockBlobReference(blobName);
    using (var fileStream = imageFile.InputStream)
    {
        await imageBlob.UploadFromStreamAsync(fileStream);
    }
    return imageBlob;
}
```

Après avoir hello HttpPost `Create` méthode télécharge un objet blob et les mises à jour hello de base de données, il crée un tooinform de message de file d’attente de ce processus principal qu’une image est prête pour la miniature tooa de conversion.

```csharp
string queueMessageString = ad.AdId.ToString();
var queueMessage = new CloudQueueMessage(queueMessageString);
await queue.AddMessageAsync(queueMessage);
```

Hello code hello HttpPost `Edit` méthode est similaire à ceci près que si l’utilisateur de hello sélectionne un nouveau fichier image tous les objets BLOB existants doivent être supprimés.

```csharp
if (imageFile != null && imageFile.ContentLength != 0)
{
    await DeleteAdBlobsAsync(ad);
    imageBlob = await UploadAndSaveBlobAsync(imageFile);
    ad.ImageURL = imageBlob.Uri.ToString();
}
```

Hello l’exemple suivant montre le code hello qui supprime des objets BLOB lorsque vous supprimez une annonce.

```csharp
private async Task DeleteAdBlobsAsync(Ad ad)
{
    if (!string.IsNullOrWhiteSpace(ad.ImageURL))
    {
        Uri blobUri = new Uri(ad.ImageURL);
        await DeleteAdBlobAsync(blobUri);
    }
    if (!string.IsNullOrWhiteSpace(ad.ThumbnailURL))
    {
        Uri blobUri = new Uri(ad.ThumbnailURL);
        await DeleteAdBlobAsync(blobUri);
    }
}
private static async Task DeleteAdBlobAsync(Uri blobUri)
{
    string blobName = blobUri.Segments[blobUri.Segments.Length - 1];
    CloudBlockBlob blobToDelete = imagesBlobContainer.GetBlockBlobReference(blobName);
    await blobToDelete.DeleteAsync();
}
```

### <a name="contosoadsweb---viewsadindexcshtml-and-detailscshtml"></a>ContosoAdsWeb - Views\Ad\Index.cshtml et Details.cshtml
Hello *Index.cshtml* fichier affiche les miniatures avec hello autres données Active Directory.

```razor
<img src="@Html.Raw(item.ThumbnailURL)" />
```

Hello *Details.cshtml* fichier affiche l’image en taille réelle de hello.

```razor
<img src="@Html.Raw(Model.ImageURL)" />
```

### <a name="contosoadsweb---viewsadcreatecshtml-and-editcshtml"></a>ContosoAdsWeb - Views\Ad\Create.cshtml et Edit.cshtml
Hello *Create.cshtml* et *Edit.cshtml* fichiers spécifient qu’Active hello hello tooget de contrôleur d’encodage de formulaire `HttpPostedFileBase` objet.

```razor
@using (Html.BeginForm("Create", "Ad", FormMethod.Post, new { enctype = "multipart/form-data" }))
```

Un `<input>` élément indique hello navigateur tooprovide une boîte de dialogue de sélection de fichier.

```razor
<input type="file" name="imageFile" accept="image/*" class="form-control fileupload" />
```

### <a name="contosoadsworker---workerrolecs---onstart-method"></a>ContosoAdsWorker - WorkerRole.cs - Méthode OnStart
environnement de rôle de travail Azure Hello appelle hello `OnStart` méthode Bonjour `WorkerRole` classe une fois le rôle de travail hello est mise en route, et il appelle hello `Run` méthode lorsque hello `OnStart` fin de la méthode.

Hello `OnStart` méthode obtient la chaîne de connexion de base de données hello de hello *.cscfg* de fichiers et le passe toohello Entity Framework DbContext classe. fournisseur SQLClient de Hello est utilisé par défaut, afin de fournisseur de hello n’a pas toobe spécifié.

```csharp
var dbConnString = CloudConfigurationManager.GetSetting("ContosoAdsDbConnectionString");
db = new ContosoAdsContext(dbConnString);
```

Après cela, méthode hello Obtient un compte de stockage de toohello de référence et crée la file d’attente et le conteneur d’objets blob hello si elles n’existent pas. code Hello qui est similaire toowhat vous nous avons déjà vu dans un rôle web de hello `Application_Start` (méthode).

### <a name="contosoadsworker---workerrolecs---run-method"></a>ContosoAdsWorker - WorkerRole.cs - Méthode Run
Hello `Run` méthode est appelée lorsque hello `OnStart` méthode termine son travail de l’initialisation. méthode Hello exécute une boucle infinie qui surveille les nouveaux messages de file d’attente et les traite lorsqu’ils arrivent.

```csharp
public override void Run()
{
    CloudQueueMessage msg = null;

    while (true)
    {
        try
        {
            msg = this.imagesQueue.GetMessage();
            if (msg != null)
            {
                ProcessQueueMessage(msg);
            }
            else
            {
                System.Threading.Thread.Sleep(1000);
            }
        }
        catch (StorageException e)
        {
            if (msg != null && msg.DequeueCount > 5)
            {
                this.imagesQueue.DeleteMessage(msg);
            }
            System.Threading.Thread.Sleep(5000);
        }
    }
}
```

Après chaque itération de boucle de hello, si aucun message de la file d’attente a été trouvé, programme de hello se met en veille pendant une seconde. Rôle de travail hello cela empêche de subir excessive du processeur durée et le stockage transaction des frais. Hello équipe de consultants clients Microsoft indique un récit à propos d’un développeur qui a oublié tooinclude, déployées tooproduction et pour les vacances. Lorsqu’il a obtenu sa supervision coûtent plus cher que les vacances hello.

Parfois, le contenu d’un message de la file d’attente hello provoque une erreur lors du traitement. Cela s’appelle un *message incohérent*, et si vous venez a consigné une erreur et redémarrer la boucle de hello, vous pouvez essayer indéfiniment qu’un message aux tooprocess.  Par conséquent bloc catch de hello inclut une instruction if qui vérifie toosee combien de fois application hello a essayé de tooprocess hello message actuel, et si elle a été plus de 5 fois, le message de type hello est supprimé à partir de la file d’attente hello.

`ProcessQueueMessage` est appelé lorsqu'un message de file d'attente est trouvé.

```csharp
private void ProcessQueueMessage(CloudQueueMessage msg)
{
    var adId = int.Parse(msg.AsString);
    Ad ad = db.Ads.Find(adId);
    if (ad == null)
    {
        throw new Exception(String.Format("AdId {0} not found, can't create thumbnail", adId.ToString()));
    }

    CloudBlockBlob inputBlob = this.imagesBlobContainer.GetBlockBlobReference(ad.ImageURL);

    string thumbnailName = Path.GetFileNameWithoutExtension(inputBlob.Name) + "thumb.jpg";
    CloudBlockBlob outputBlob = this.imagesBlobContainer.GetBlockBlobReference(thumbnailName);

    using (Stream input = inputBlob.OpenRead())
    using (Stream output = outputBlob.OpenWrite())
    {
        ConvertImageToThumbnailJPG(input, output);
        outputBlob.Properties.ContentType = "image/jpeg";
    }

    ad.ThumbnailURL = outputBlob.Uri.ToString();
    db.SaveChanges();

    this.imagesQueue.DeleteMessage(msg);
}
```

Ce code lit l’URL de l’image de hello de base de données tooget hello convertit tooa vignette de l’image hello, enregistre la miniature de hello dans un objet blob, met à jour la base de données hello avec l’URL de blob miniature hello et supprime le message de file d’attente hello.

> [!NOTE]
> Hello code Bonjour `ConvertImageToThumbnailJPG` méthode utilise les classes dans l’espace de noms System.Drawing hello par souci de simplicité. Toutefois, les classes de hello dans cet espace de noms ont été conçues pour une utilisation avec Windows Forms. Elles ne sont pas prises en charge dans un service Windows ou ASP.NET. Pour plus d’informations sur les options de traitement d’images, consultez [Génération d’images dynamiques](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) et [Redimensionnement d’images approfondi](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na).
>
>

## <a name="troubleshooting"></a>Résolution des problèmes
En cas de quelque chose ne fonctionne pas pendant que vous êtes suivant les instructions de hello dans ce didacticiel, voici quelques erreurs courantes et comment tooresolve les.

### <a name="serviceruntimeroleenvironmentexception"></a>ServiceRuntime.RoleEnvironmentException
Hello `RoleEnvironment` objet est fourni par Azure lorsque vous exécutez une application dans Azure, ou lorsque vous exécutez localement à l’aide d’émulateur de calcul Azure hello.  Si vous obtenez cette erreur lorsque vous exécutez localement, assurez-vous que vous avez défini le projet de ContosoAdsCloudService hello en tant que projet de démarrage hello. Cela configure hello toorun de projet à l’aide d’émulateur de calcul Azure hello.

Une des choses hello hello application utilise hello RoleEnvironment Azure pour est tooget des valeurs de chaîne de connexion de hello qui sont stockés dans hello *.cscfg* des fichiers, par conséquent, une autre cause de cette exception est une chaîne de connexion manquant. Assurez-vous que vous avez créé paramètre hello StorageConnectionString Cloud à la fois et les configurations locales dans le projet de ContosoAdsWeb hello et que vous avez créé les deux chaînes de connexion pour les deux configurations de projet de ContosoAdsWorker hello. Si vous effectuez un **Rechercher tout** recherche pour StorageConnectionString dans l’ensemble de la solution hello, vous devez voir il 9 heures dans les 6 fichiers.

### <a name="cannot-override-tooport-xxx-new-port-below-minimum-allowed-value-8080-for-protocol-http"></a>Impossible de remplacer tooport xxx. La valeur du nouveau port est inférieure à la valeur minimale autorisée de 8080 pour le protocole http
Essayez de modifier le numéro de port de hello utilisé par le projet web de hello. Projet de ContosoAdsWeb hello d’avec le bouton droit, puis cliquez sur **propriétés**. Cliquez sur hello **Web** onglet et modifiez le numéro de port hello Bonjour **Url du projet** paramètre.

Pour une autre solution susceptibles de résoudre le problème de hello, consultez hello suivant la section.

### <a name="other-errors-when-running-locally"></a>Autres erreurs lors de l'exécution locale
Par nouveau cloud de la valeur par défaut des projets de service utilisent Bonjour Azure compute emulator toosimulate express Bonjour environnement Azure. Il s’agit d’une version légère de l’émulateur de calcul complet de hello et fonctionne sous certaines hello conditions émulateur complet lors de la version express de hello n’est pas.  

toochange hello émulateur complet de projet toouse hello, cliquez sur le projet de ContosoAdsCloudService hello, puis cliquez sur **propriétés**. Bonjour **propriétés** fenêtre, cliquez sur hello **Web** onglet, puis cliquez sur hello **utiliser l’émulateur complet** case d’option.

Dans l’application de type hello toorun de commandes avec l’émulateur complet hello, vous avez tooopen Visual Studio avec des privilèges d’administrateur.

## <a name="next-steps"></a>Étapes suivantes
Hello application d’annonces de Contoso a intentionnellement été conservée simple pour obtenir un didacticiel de mise en route. Par exemple, il n’implémente pas [injection de dépendance](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) ou hello [référentiel et une unité de travaillent des modèles](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), ce n’est pas [utiliser une interface pour la journalisation](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), il n’utilise pas [ Migrations EF Code First](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage données modifications sur le modèle ou [résilience des connexions EF](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage temporaire des erreurs réseau et ainsi de suite.

Voici certaines applications service cloud qui illustrent les plus pratiques de codage réel, répertoriées de moins complexe toomore complexe :

* [PhluffyFotos](http://code.msdn.microsoft.com/PhluffyFotos-Sample-7ecffd31). Un concept similaire tooContoso annonces mais implémente que davantage de fonctionnalités et les plus pratiques de codage réel.
* [Application multiniveau Azure Cloud Service avec tables, files d'attente et objets blob](http://code.msdn.microsoft.com/windowsazure/Windows-Azure-Multi-Tier-eadceb36). Présente les tables Azure Storage ainsi que des objets blob et des files d’attente. Basé sur une version antérieure de hello Azure SDK pour .NET, requiert certains toowork modifications avec la version actuelle de hello.
* [Concepts de base des services cloud dans Microsoft Azure](http://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649). Un exemple complet illustrant une large gamme de meilleures pratiques, produit par le groupe Microsoft Patterns and Practices de hello.

Pour obtenir des informations générales sur le développement pour le cloud de hello, consultez [génération d’applications Cloud réel avec Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction).

Pour un stockage de tooAzure vidéo de présentation des meilleures pratiques et les modèles, consultez [Microsoft Azure Storage – nouveautés, meilleures pratiques et modèles](http://channel9.msdn.com/Events/Build/2014/3-628).

Pour plus d’informations, consultez hello suivant des ressources :

* [Azure Cloud Services Partie 1 : Présentation](http://justazure.com/microsoft-azure-cloud-services-part-1-introduction/)
* [Comment les Services de cloud computing toomanage](cloud-services-how-to-manage.md)
* [Azure Storage](/documentation/services/storage/)
* [Comment toochoose un cloud de fournisseur de services](https://azure.microsoft.com/overview/choosing-a-cloud-service-provider/)
