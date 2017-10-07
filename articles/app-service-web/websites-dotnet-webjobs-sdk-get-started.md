---
title: "aaaCreate une tâche Web de .NET dans Azure App Service | Documents Microsoft"
description: "Créez une application multiniveau avec ASP.NET MVC et Azure. Hello frontal s’exécute dans une application web dans Azure App Service et hello précédent s’exécute en tant qu’une tâche Web. application Hello utilise Entity Framework, base de données SQL, les files d’attente de stockage Azure et des objets BLOB."
services: app-service
documentationcenter: .net
author: tdykstra
manager: erikre
editor: mollybos
ms.assetid: 99cb9917-483a-45f8-a98d-07d19c68c753
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 6/14/2017
ms.author: glenga
ms.openlocfilehash: d92fc4b81cc0d58f8e900f257e747af56d32b911
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-net-webjob-in-azure-app-service"></a>Créer une tâche web .NET dans Azure App Service
Ce didacticiel montre comment le code pour une application ASP.NET MVC 5 à plusieurs niveaux simple qui utilise hello toowrite [WebJobs SDK](websites-dotnet-webjobs-sdk.md).

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

Hello d’objectif de hello [WebJobs SDK](websites-webjobs-resources.md) est toosimplify hello code que vous écrivez pour les tâches courantes qu’une tâche Web peut effectuer, telles que le traitement d’image, traitement de la file d’attente, agrégation RSS, maintenance des fichiers et de l’envoi des messages électroniques. Hello WebJobs SDK inclut des fonctionnalités intégrées pour de nombreux autres scénarios courants pour travailler avec le stockage Azure et Service Bus et pour la planification des tâches et la gestion des erreurs. En outre, il a conçu toobe extensible et il existe un [référentiel open source pour les extensions](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview).

exemple d’application Hello est un forum de publicité. Les utilisateurs peuvent télécharger des images pour les annonces, et un processus principal convertit hello images toothumbnails. page de liste ad Hello affiche des miniatures de hello et hello ad page des détails affiche les image plein écran hello. Voici une capture d'écran :

![Ad list](./media/websites-dotnet-webjobs-sdk-get-started/list.png)

Cet exemple d’application fonctionne avec des [files d’attente Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) et [objets blob Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage). Hello didacticiel montre comment toodeploy hello application trop[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) et [base de données SQL Azure](http://msdn.microsoft.com/library/azure/ee336279).

## <a id="prerequisites"></a>Configuration requise
Hello didacticiel suppose que vous savez comment toowork avec [ASP.NET MVC 5](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) projets dans Visual Studio.

didacticiel de Hello a été écrit à l’origine pour Visual Studio 2013, mais il peut être utilisé avec les versions ultérieures de Visual Studio. Si vous utilisez Visual Studio 2015 ou 2017, notez qu’avant d’exécuter application hello localement, vous devez modifier hello `Data Source` dans le cadre de la chaîne de connexion de base de données SQL Server locale hello dans les fichiers Web.config et App.config de hello de `Data Source=(localdb)\v11.0` trop`Data Source=(LocalDb)\MSSQLLocalDB`.

> [!NOTE]
> <a name="note"></a>Ce didacticiel, vous devez avoir un toocomplete compte Azure :
>
> * Vous pouvez [ouvrir un compte Azure gratuitement](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F): vous obtenez des crédits que vous pouvez utiliser tootry à payer des services Azure, et même une fois qu’ils sont utilisés, vous pouvez conserver le compte de hello et utiliser des services Azure gratuits, comme les sites Web. Votre carte de crédit ne sera jamais facturé, sauf si vous explicitement modifiez vos paramètres et demandez toobe facturé.
> * Vous pouvez [activer le crédit Azure mensuel pour Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F) : votre abonnement vous donne droit chaque mois à des crédits dont vous pouvez vous servir pour les services Azure payants.
>
> Si vous souhaitez tooget démarré avec le Service d’application Azure avant de s’inscrire pour un compte Azure, accédez trop[essayez du Service d’applications](https://azure.microsoft.com/try/app-service/), où vous pouvez créer une application web de courte durée de démarrage immédiatement dans le Service d’applications. Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.
>
>

## <a id="learn"></a>Contenu
didacticiel de Hello illustre des tâches de hello toodo suivant :

* Activer votre ordinateur pour le développement Azure en installant hello Azure SDK (uniquement pour Visual Studio 2013 et 2015 utilisateurs).
* Créez un projet d’Application Console qui déploie automatiquement comme une tâche Web Azure lorsque vous déployez le projet web associé de hello.
* Tester un service principal de WebJobs SDK localement sur l’ordinateur de développement hello.
* Publier une application avec une application web de tâches Web principal tooa dans le Service d’applications.
* Télécharger des fichiers et stockez-les dans hello service Blob Azure.
* Utilisez toowork du Kit de développement logiciel Azure WebJobs hello avec les objets BLOB et files d’attente de stockage Azure.

## <a id="contosoads"></a>Architecture de l’application
exemple d’application Hello utilise hello [centré sur la file d’attente de travail modèle](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) travail hello gourmande en ressources processeur de toooff en charge de la création du processus de miniatures tooa principal.

application Hello stocke des publicités dans une base de données SQL, à l’aide des tables de hello toocreate Entity Framework Code First et accéder aux données de hello. Pour chaque publicité, base de données hello stocke deux URL : un pour les image plein écran hello et un pour l’image de hello.

![Ad table](./media/websites-dotnet-webjobs-sdk-get-started/adtable.png)

Lorsqu’un utilisateur télécharge une image, une application web de hello stocke image hello dans un [objets blob Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), et stocke des informations d’Active Directory hello dans base de données hello avec une URL qui pointe toohello blob. AT hello même temps, il écrit un message de tooan file d’attente Azure. Dans un processus principal en cours d’exécution en tant qu’une tâche Web Azure, hello WebJobs SDK interroge la file d’attente hello pour les nouveaux messages. Quand un nouveau message s’affiche, hello la tâche Web crée une miniature pour cette image et les mises à jour hello miniature champ de base de données d’URL pour qu’ad. Voici un diagramme qui illustre l’interagissent entre les parties hello de l’application hello :

![Contoso Ads architecture](./media/websites-dotnet-webjobs-sdk-get-started/apparchitecture.png)

[!INCLUDE [install-sdk](../../includes/install-sdk-2017-2015-2013.md)]  
instructions des didacticiels de Hello appliquent tooAzure SDK pour .NET 2.7.1 ou version ultérieure.

## <a id="storage"></a>Création d'un compte de stockage Azure
Un compte de stockage Azure fournit des ressources pour le stockage de la file d’attente et les données blob dans le cloud de hello. Il est également utilisé par hello WebJobs SDK toostore enregistrement des données de tableau de bord hello.

Dans une application réelle, vous créez généralement des comptes distincts pour les données d’application et de journalisation, et des comptes distincts pour les données de test et de production. Pour ce didacticiel, vous allez utiliser un seul compte.

1. Ouvrez hello **l’Explorateur de serveurs** fenêtre dans Visual Studio.
2. Avec le bouton hello **Azure** nœud, puis cliquez sur **connecter tooMicrosoft abonnement Azure...** .
   
   ![Se connecter tooAzure](./media/websites-dotnet-webjobs-sdk-get-started/connaz.png)

3. Connectez-vous à l'aide de vos informations d'identification Azure.
4. Avec le bouton droit **stockage** sous hello nœud Azure, puis cliquez sur **créer un compte de stockage**.
   
   ![Créer un compte de stockage](./media/websites-dotnet-webjobs-sdk-get-started/createstor.png)
   
5. Bonjour **créer un compte de stockage** boîte de dialogue, entrez un nom pour le compte de stockage hello.

    nom de Hello doit être unique (aucun autre compte de stockage Azure ne peut avoir hello même nom). Si le nom hello que vous entrez est déjà en cours d’utilisation, vous obtiendrez une chance toochange il.

    Hello tooaccess URL votre compte de stockage sera *{nom}*. core.windows.net.
6. Ensemble hello **région ou groupe d’affinités** tooyou le plus proche de liste déroulante toohello région.

    Ce paramètre spécifie le centre de données Azure qui hébergera votre compte de stockage. Pour ce didacticiel, votre choix ne fera pas une grande différence. Toutefois, pour une application web de production, vous souhaitez que votre serveur web et votre toobe de compte de stockage Bonjour même latence toominimize de région et les données des frais de sortie. Hello web application (vous allez créer ultérieurement) centre de données doit être aussi proche que possible des navigateurs toohello l’accès à hello web application latence toominimize de commande.
7. Ensemble hello **réplication** déroulante liste trop**localement redondant**.

    Lors de la géo-réplication est activée pour un compte de stockage, contenu de hello stocké est répliqué tooa centre de données secondaire tooenable basculement toothat emplacement en cas de sinistre majeur dans l’emplacement principal de hello. La géo-réplication peut engendrer des coûts supplémentaires. Pour les comptes de test et de développement, généralement non désirés toopay pour la géo-réplication. Pour plus d’informations, consultez [Création, gestion ou suppression d’un compte de stockage](../storage/common/storage-create-storage-account.md).
8. Cliquez sur **Create**.

    ![New storage account](./media/websites-dotnet-webjobs-sdk-get-started/newstorage.png)

## <a id="download"></a>Télécharger l’application hello
1. Téléchargez et décompressez hello [complété solution](http://code.msdn.microsoft.com/Simple-Azure-Website-with-b4391eeb).
2. Démarrez Visual Studio.
3. À partir de hello **fichier** menu Choisissez **Ouvrir > Projet/Solution**, accédez toowhere que vous avez téléchargé les solutions hello et puis ouvrez le fichier de solution hello.
4. Appuyez sur solution de hello toobuild CTRL + MAJ + B.

    Par défaut, Visual Studio restaure automatiquement le contenu du package NuGet hello, qui n’est pas compris dans hello *.zip* fichier. Si les packages hello ne sont pas restaurées, installez-les manuellement en accédant de toohello **gérer les Packages NuGet pour la Solution** boîte de dialogue et en cliquant sur hello **restaurer** bouton à droite en haut hello.
5. Dans **l’Explorateur de solutions**, assurez-vous que **ContosoAdsWeb** est sélectionné comme projet de démarrage hello.

## <a id="configurestorage"></a>Configurer hello application toouse votre compte de stockage
1. Ouvrez l’application hello *Web.config* fichier hello ContosoAdsWeb projet.

    Hello contient une chaîne de connexion SQL et une chaîne de connexion de stockage Azure pour l’utilisation des objets BLOB et files d’attente.

    Hello chaîne de connexion SQL pointe tooa [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) base de données.

    chaîne de connexion de stockage Hello est un exemple qui a des espaces réservés pour hello clé compte de stockage accès et le nom. Vous devez le remplacer par une chaîne de connexion qui a le nom de hello et la clé de votre compte de stockage.  

    ```
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;" providerName="System.Data.SqlClient" />
        <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
    </connectionStrings>
    ```
    chaîne de connexion de stockage Hello AzureWebJobsStorage car il s’agit de hello de nom hello que webjobs SDK utilise par défaut est appelé. Hello même nom est utilisé ici pour avoir une valeur de chaîne de connexion qu’un seul tooset Bonjour environnement Azure.
2. Dans **l’Explorateur de serveurs**, avec le bouton droit de votre compte de stockage sous hello **stockage** nœud, puis cliquez sur **propriétés**.

    ![Click Storage Account Properties](./media/websites-dotnet-webjobs-sdk-get-started/storppty.png)
3. Bonjour **propriétés** fenêtre, cliquez sur **clés de compte de stockage**, puis cliquez sur les points de suspension hello.

    ![Clés de compte de stockage](./media/websites-dotnet-webjobs-sdk-get-started/stor-account-keys.png)
4. Hello de copie **chaîne de connexion**.

    ![Storage Account Keys dialog](./media/websites-dotnet-webjobs-sdk-get-started/cpak.png)
5. Remplacez la chaîne de connexion de stockage hello Bonjour *Web.config* fichier avec la chaîne de connexion hello vous venez de copier. Veillez à que sélectionner tous les éléments à l’intérieur des guillemets hello mais sans inclure les guillemets hello avant le collage.
6. Ouvrez hello *App.config* fichier hello ContosoAdsWebJob projet.

    Ce fichier comporte deux chaînes de connexion : une pour les données de l'application et une pour la journalisation. Vous pouvez utiliser des comptes de stockage distincts pour les données et la journalisation de l’application, ainsi qu’utiliser [plusieurs comptes de stockage pour les données](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs). Pour ce didacticiel, vous allez utiliser un seul compte de stockage. chaînes de connexion Hello possèdent des espaces réservés pour les clés de compte de stockage hello.

    ```
    <configuration>
        <connectionStrings>
            <add name="AzureWebJobsDashboard" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;"/>
    </connectionStrings>
        <startup>
            <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5" />
    </startup>
    </configuration>

    ```

    Par défaut, hello WebJobs SDK recherche les chaînes de connexion nommées AzureWebJobsStorage et AzureWebJobsDashboard. En guise d’alternative, vous pouvez [stocker la chaîne de connexion hello toutefois vous souhaitez et le passez dans explicitement toohello `JobHost` objet](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#config).
7. Remplacez les deux chaînes de connexion de stockage avec la chaîne de connexion hello que vous avez copiée précédemment.
8. Enregistrez vos modifications.

## <a id="run"></a>Exécutez hello application localement
1. toostart hello web frontal de l’application hello, appuyez sur CTRL + F5.

    navigateur par défaut de Hello ouvre la page d’accueil toohello. (projet de hello web s’exécute, car vous l’avez apportées projet de démarrage hello.)

    ![Contoso Ads home page](./media/websites-dotnet-webjobs-sdk-get-started/home.png)
2. toostart hello la tâche Web principal de l’application hello, avec le bouton droit de projet hello ContosoAdsWebJob **l’Explorateur de solutions**, puis cliquez sur **déboguer** > **démarrer une nouvelle instance** .

    Une fenêtre d’application console s’ouvre et affiche des messages de journalisation indiquant l’objet de tâche Web SDK JobHost hello a démarré toorun.

    ![Fenêtre de l’application console montrant ce principal hello est en cours d’exécution.](./media/websites-dotnet-webjobs-sdk-get-started/backendrunning.png)
3. Dans votre navigateur, cliquez sur **Créer une publicité**.
4. Entrez des données de test, sélectionnez une tooupload d’image, puis cliquez sur **créer**.

    ![Create page](./media/websites-dotnet-webjobs-sdk-get-started/create.png)

    application Hello passe toohello page d’Index, mais elle n’affiche une miniature de publicité hello parce que ce traitement n’a pas encore s’est produite.

    Pendant ce temps, après un court délai d’attente un message de journalisation dans la fenêtre de l’application console hello indique qu’un message de la file d’attente a été reçu et qu’il a été traité.

    ![Console application window showing that a queue message has been processed](./media/websites-dotnet-webjobs-sdk-get-started/backendlogs.png)
5. Une fois que vous voyez hello consignant les messages dans la fenêtre de l’application console hello, actualiser hello Index toosee hello vignette.

    ![Page d'index](./media/websites-dotnet-webjobs-sdk-get-started/list.png)
6. Cliquez sur **détails** pour votre image en taille réelle d’ad toosee hello.

    ![Details page](./media/websites-dotnet-webjobs-sdk-get-started/details.png)

Vous avez déjà exécuté application hello sur votre ordinateur local, et qu’il utilise un serveur SQL de base de données située sur votre ordinateur, mais il fonctionne avec les files d’attente et des objets BLOB dans hello cloud. Bonjour, suivant la section vous allez exécuter application hello dans le cloud de hello, à l’aide d’une base de données de cloud ainsi que les objets BLOB du cloud et les files d’attente.  

## <a id="runincloud"></a>Exécutez l’application hello dans le cloud de hello
Vous effectuerez hello après application de hello toorun étapes dans le cloud de hello :

* Déployer des applications tooWeb. Visual Studio crée automatiquement une application web dans App Service et une instance Base de données SQL.
* Configurer hello web application toouse votre compte de stockage et de la base de données SQL Azure.

Une fois que vous avez créé des publicités lors de l’exécution dans le cloud de hello, vous allez afficher hello hello de toosee du tableau de bord WebJobs SDK enrichi de fonctionnalités qu’il a toooffer d’analyse.

### <a name="deploy-tooweb-apps"></a>Déployer des applications de tooWeb

1. Fermez le navigateur de hello et la fenêtre de l’application console hello.
2. Suivez les étapes de hello Bonjour [tooAzure avec la base de données de publication](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) section.
3. Après avoir terminé les étapes de hello pour le déploiement, continuer hello tâches restantes décrites dans cet article.

### <a name="configure-hello-web-app-toouse-your-azure-sql-database-and-storage-account"></a>Configurer hello web application toouse votre compte de stockage et de la base de données SQL Azure
Il est une meilleure pratique de sécurité trop[Évitez de placer des informations sensibles telles que des chaînes de connexion dans des fichiers qui sont stockés dans des référentiels de code source](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets). Azure fournit un moyen toodo que : vous pouvez définir la chaîne de connexion et d’autres valeurs de paramètre Bonjour environnement Azure, et les API de configuration ASP.NET récupère automatiquement ces valeurs lors de l’application hello s’exécute dans Azure. Vous pouvez définir ces valeurs dans Azure à l’aide de **l’Explorateur de serveurs**, hello portail Azure, Windows PowerShell, ou hello interface de ligne de commande multiplateforme. Pour plus d’informations, consultez [Fonctionnement des chaînes d’application et des chaînes de connexion](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).

Dans cette section, vous utilisez **l’Explorateur de serveurs** tooset les valeurs de chaîne de connexion dans Azure.

1. Dans l’**Explorateur de serveurs**, cliquez avec le bouton droit sur votre application web sous **Azure > App Service {votre groupe de ressources}**, puis cliquez sur **Afficher les paramètres**.

    Hello **application Web Azure** s’ouvre sur hello **Configuration** onglet.
2. Modifier le nom de nom toohello de chaîne de connexion hello DefaultConnection hello choisis lors de la configuration de base de données SQL de hello Bonjour [tooAzure avec la base de données de publication](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) l’article.

    Azure créé automatiquement cette chaîne de connexion lorsque vous avez créé l’application hello web avec une base de données associé, afin qu’il a déjà la valeur de chaîne de connexion adéquate hello. Vous modifiez simplement hello nom toowhat que recherche de votre code.
3. Ajoutez deux chaînes de connexion nommées AzureWebJobsStorage et AzureWebJobsDashboard. Définir le type de base de données hello trop**personnalisé**et la même valeur que vous avez utilisé précédemment pour hello ensemble hello connexion chaîne valeur toohello *Web.config* et *App.config* fichiers. (Veillez incluent la chaîne de connexion entière hello, pas seulement hello touche d’accès rapide et de ne pas inclure les guillemets hello.)

    Ces chaînes de connexion sont utilisées par hello WebJobs SDK, l’autre pour les données d’application et un pour la journalisation. Comme vous l’avez vu précédemment, une hello pour les données d’application est également utilisé par le code hello web frontal.
4. Cliquez sur **Enregistrer**.

    ![Chaînes de connexion dans le portail Azure](./media/websites-dotnet-webjobs-sdk-get-started/azconnstr.png)
5. Dans **l’Explorateur de serveurs**, avec le bouton droit de l’application hello web, puis cliquez sur **arrêter**.
6. Après l’arrêt de l’application hello web, l’application hello web avec le bouton droit à nouveau, puis cliquez sur **Démarrer**.

   Hello la tâche Web démarre automatiquement lorsque vous publiez, mais il s’arrête lorsque vous modifiez la configuration. toorestart, vous pouvez redémarrer l’application web hello ou redémarrez hello la tâche Web Bonjour [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715). Il est généralement recommandée toorestart hello web application après une modification de configuration.
7. Actualisez la fenêtre de navigateur hello qui a des URL de l’application hello web dans la barre d’adresse.

    page d’accueil Hello s’affiche.
8. Créer une annonce, comme vous le faisiez quand vous [s’exécutait localement des application hello](https://docs.microsoft.com/azure/app-service-web/websites-dotnet-webjobs-sdk-get-started#a-idrunarun-the-application-locally).

   page d’Index Hello affiche sans une vignette dans un premier temps.
9. Actualiser la page de hello après quelques secondes et hello miniature s’affiche.

   Si la miniature de hello n’apparaît pas, vous peut-être toowait environ une minute pour toorestart de la tâche Web hello. Si, après un certain temps, vous ne voyez toujours miniature hello lorsque vous actualisez la page hello, hello la tâche Web a ne peut-être pas démarré automatiquement. Dans ce cas, accédez toohello **des Services d’application** panneau Bonjour [portail Azure](https://portal.azure.com/), localisez votre application web, puis cliquez sur **Démarrer**.

### <a name="view-hello-webjobs-sdk-dashboard"></a>Hello d’affichage du tableau de bord WebJobs SDK
1. Bonjour [portail Azure](https://portal.azure.com/), sélectionnez hello **panneau des Services d’application**, localisez votre application web, puis sélectionnez **WebJobs**.
3. Sélectionnez hello **journaux** onglet.

    ![Onglet journaux](./media/websites-dotnet-webjobs-sdk-get-started/log-tab.png)

    Un nouvel onglet de navigateur s’ouvre toohello du tableau de bord WebJobs SDK. tableau de bord Hello montre que hello la tâche Web est en cours d’exécution et affiche la liste des fonctions dans votre code que hello que webjobs SDK est déclenchée.
4. Cliquez sur un des détails de toosee fonctions hello concernant son exécution.

    ![WebJobs SDK dashboard](./media/websites-dotnet-webjobs-sdk-get-started/wjdashboardhome.png)

    ![WebJobs SDK dashboard](./media/websites-dotnet-webjobs-sdk-get-started/wjfunctiondetails.png)

    Hello **relecture fonction** bouton sur cette page provoque la hello WebJobs SDK framework toocall hello fonction à nouveau, et elle vous offre une fonction de probabilité toochange hello données passées toohello tout d’abord.

> [!NOTE]
> Lorsque vous avez terminé de test, envisagez de supprimer hello web app, le compte de stockage et votre instance de base de données SQL. l’application web Hello est libre, mais hello compte de stockage SQL et instance de base de données accumulent les coûts (et ce, minimal dû toohello de petite taille). En outre, si vous laissez hello web application est en cours d’exécution, toute personne qui recherche l’URL peut créer et d’afficher des publicités. 
>
>

### <a name="delete-your-web-app"></a>Supprimer votre application web
Dans le portail de hello, accédez toohello **des Services d’application** panneau, recherchez et sélectionnez votre application web, puis cliquez sur **supprimer**. Si vous souhaitez simplement tootemporarily empêcher d’autres utilisateurs d’accéder à l’application hello web, cliquez sur **arrêter** à la place. Dans ce cas, interrompt tooaccrue pour hello compte de stockage et de la base de données SQL.

### <a name="delete-your-storage-account"></a>Supprimer votre compte de stockage
toodelete votre compte de stockage, consultez [supprimer un compte de stockage](https://docs.microsoft.com/azure/storage/storage-create-storage-account#delete-a-storage-account). 

### <a name="delete-your-database"></a>Supprimer de votre base de données
toodelete SQL de base de données, consultez hello [API REST de Azure SQL Database](https://docs.microsoft.com/rest/api/sql/) documentation.

## <a id="create"></a>Créer l’application hello à partir de zéro
Dans cette section, vous effectuerez hello tâche suivantes :

* création d'une solution Visual Studio avec un projet web ;
* Ajouter un projet de bibliothèque de classes pour les données de salutation couche d’accès qui est partagée entre le serveur frontal hello et back end.
* Ajouter un projet d’Application Console pour hello principal, avec les tâches Web déploiement est activé.
* ajout de packages NuGet ;
* définition des références d'un projet ;
* Copiez les fichiers de configuration et le code d’application à partir de l’application hello téléchargé que vous avez travaillé avec dans la section précédente de hello du didacticiel de hello.
* Passez en revue les parties hello du code de hello qui fonctionnent avec les objets BLOB Windows Azure et files d’attente et hello WebJobs SDK.

### <a name="create-a-visual-studio-solution-with-a-web-project-and-class-library-project"></a>Création d'une solution Visual Studio avec un projet web et un projet de bibliothèque de classes
1. Dans Visual Studio, choisissez **Fichier** > **Nouveau** > **Projet**.
2. Bonjour **nouveau projet** boîte de dialogue, choisissez **Visual C#** > **Web** > **ASP.NET Web Application(.NETFramework)**.
3. Nommez le projet hello ContosoAdsWeb, nommez hello solution ContosoAdsWebJobsSDK (modifier le nom de la solution hello si placez Bonjour même dossier que hello téléchargé solution), puis cliquez sur **OK**.

    ![Nouveau projet](./media/websites-dotnet-webjobs-sdk-get-started/newproject.png)
4. Bonjour **nouvelle Application Web ASP.NET** boîte de dialogue, choisissez le modèle MVC de hello, puis sélectionnez **modifier l’authentification**.

    ![Modifier l'authentification](./media/websites-dotnet-webjobs-sdk-get-started/chgauth.png)
5. Bonjour **modifier l’authentification** boîte de dialogue, choisissez **aucune authentification**, puis cliquez sur **OK**.

    ![Aucune authentification](./media/websites-dotnet-webjobs-sdk-get-started/noauth.png)
6. Bonjour **nouvelle Application Web ASP.NET** boîte de dialogue, cliquez sur **OK**.

    Visual Studio crée la solution de hello et de projet web de hello.
7. Dans **l’Explorateur de solutions**, avec le bouton droit de la solution de hello (pas le projet hello), puis choisissez **ajouter** > **nouveau projet**.
8. Bonjour **ajouter un nouveau projet** boîte de dialogue, choisissez **Visual C#** > **de bureau Windows classique** > **bibliothèque de classes (.NET Infrastructure)** modèle.  
9. Projet de hello nom *ContosoAdsCommon*, puis cliquez sur **OK**.

    Ce projet contiendra au contexte d’Entity Framework hello hello modèle de données et qui les deux hello front-end et back-end utilisera. En guise d’alternative, vous pouvez définir des classes liées EF de hello dans le projet web de hello et faire référence à ce projet à partir du projet de tâche Web hello. Toutefois, puis votre projet de tâche Web aurait un assemblys de tooweb de référence, elle n’a pas besoin.

### <a name="add-a-console-application-project-that-has-webjobs-deployment-enabled"></a>Ajout d'un projet d'application console dont le déploiement de tâches web est activé
1. Projet de web hello (et non hello solution ou projet de bibliothèque de classes hello) d’avec le bouton droit, puis cliquez sur **ajouter** > **nouveau projet de la tâche Web Azure**.

    ![New Azure WebJob Project menu selection](./media/websites-dotnet-webjobs-sdk-get-started/newawjp.png)
2. Bonjour **ajouter de la tâche Web Azure** boîte de dialogue, entrez les deux hello ContosoAdsWebJob **nom du projet** et hello **nom de la tâche Web**. Laissez **mode d’exécution de tâche Web** défini trop**exécuter en permanence**.
3. Cliquez sur **OK**.

   Visual Studio crée une application Console qui est toodeploy configuré comme une tâche Web chaque fois que vous déployez le projet web de hello. toodo, elle effectuée hello tâches suivantes après avoir créé le projet de hello :

   * Ajouter un *settings.json publier la tâche Web* fichier dans le dossier de propriétés de projet de la tâche Web hello.
   * Ajouter un *webjobs-list.json* fichier dans le dossier de propriétés du projet web hello.
   * Installé hello package NuGet de Microsoft.Web.WebJobs.Publish dans le projet de tâche Web hello.

   Pour plus d’informations sur ces modifications, consultez [comment toodeploy tâches Web à l’aide de Visual Studio](websites-dotnet-deploy-webjobs.md).

### <a name="add-nuget-packages"></a>Ajout de packages NuGet
modèle de nouveau projet Hello pour un projet de la tâche Web installe automatiquement le package WebJobs NuGet de kit de développement logiciel de hello [Microsoft.Azure.WebJobs](http://www.nuget.org/packages/Microsoft.Azure.WebJobs) et ses dépendances.

Un des hello dépendances de WebJobs SDK est installé automatiquement dans le projet de tâche Web hello est Bonjour Azure Storage Client Library (SCL). Toutefois, vous devez tooadd il toohello toowork de projet web avec les objets BLOB et files d’attente.

1. Ouvrez hello **gérer les Packages NuGet** boîte de dialogue pour les solutions hello.
2. Dans le volet gauche de hello, sélectionnez **les packages installés**.
3. Recherche hello *Azure Storage* du package, puis cliquez sur **gérer**.
4. Bonjour **sélectionner les projets** boîte, sélectionnez hello **ContosoAdsWeb** case à cocher, puis cliquez sur **OK**.

    Les trois projets utilisent hello Entity Framework toowork avec des données dans la base de données SQL.
5. Dans le volet gauche de hello, sélectionnez **Online**.
6. Recherche hello *EntityFramework* NuGet package et l’installer dans les trois projets.

### <a name="set-project-references"></a>Définition des références de projet
Web et projets de la tâche Web fonctionnent avec la base de données SQL hello, donc les deux doivent être une référence de projet de ContosoAdsCommon toohello.

1. Dans le projet de ContosoAdsWeb hello, définissez une référence de projet de ContosoAdsCommon toohello. (Projet de ContosoAdsWeb hello d’avec le bouton droit, puis cliquez sur **ajouter** > **référence**. 
2. Bonjour **Gestionnaire de références** boîte de dialogue, sélectionnez **projets** > **Solution** > **ContosoAdsCommon**, puis cliquez sur **OK**.)
   
    projet de tâche Web Hello nécessite des références pour utiliser des images et pour accéder aux chaînes de connexion.

4. Dans le projet de ContosoAdsWebJob hello, définissez une référence trop`System.Drawing` et `System.Configuration`.

### <a name="add-code-and-configuration-files"></a>Ajout de fichiers de code et de configuration
Ce didacticiel n’illustre pas comment trop[créer des vues à l’aide de la structure et les contrôleurs MVC](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started), comment trop[écrire du code d’Entity Framework qui fonctionne avec les bases de données SQL Server](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc), ou [hello notions de base de programmation asynchrone dans ASP.NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async). Par conséquent, tout ce qui reste toodo est la copie des fichiers de code et la configuration de solution hello téléchargé dans une nouvelle solution hello. Après quoi, hello sections suivantes montrent et expliquent les éléments clés du code de hello.

tooa projet ou un dossier, projet de hello avec le bouton droit ou un dossier et cliquez sur les fichiers tooadd **ajouter** > **élément existant**. Sélectionnez hello fichiers que vous cliquez sur **ajouter**. Si vous êtes invité tooreplace des fichiers existants, cliquez sur **Oui**.

1. Dans le projet de ContosoAdsCommon hello, supprimez hello *Class1.cs* et ajoutez son Bonjour place fichiers suivants à partir de projet de hello téléchargé.

   * *Ad.cs*
   * *ContosoAdscontext.cs*
   * *BlobInformation.cs*
2. Dans le projet de ContosoAdsWeb hello, ajoutez hello fichiers suivants à partir de projet de hello téléchargé.

   * *Web.config*
   * *Global.asax.cs*  
   * Bonjour *contrôleurs* dossier : *AdController.cs*
   * Bonjour *Views\Shared* dossier : *_Layout.cshtml* fichier
   * Bonjour *Views\Home* dossier : *Index.cshtml*
   * Bonjour *Views\Ad* dossier (créez d’abord le dossier de hello) : cinq *.cshtml* fichiers
3. Dans le projet de ContosoAdsWebJob hello, ajoutez hello fichiers suivants à partir de projet de hello téléchargé.

   * *App.config* (modifier le filtre de type de fichier hello trop**tous les fichiers**)
   * *Program.cs*
   * *Functions.cs*

Vous pouvez maintenant générer, exécuter et déployer l’application hello comme indiqué plus haut dans le didacticiel de hello. Avant cela, toutefois, l’arrêter hello la tâche Web qui s’exécute toujours dans la première application web hello, sur que vous avez déployé. Sinon, cette tâche Web sera traiter les messages de file d’attente créées localement ou par application hello en cours d’exécution dans une application web, étant donné que tous les utilisez hello même compte de stockage.

## <a id="code"></a>Passez en revue le code de l’application hello
Hello sections suivantes expliquent les code hello liées tooworking avec hello WebJobs SDK et les objets BLOB de stockage Azure et files d’attente.

> [!NOTE]
> Pour toohello spécifique hello code WebJobs SDK, consultez toohello [Program.cs et Functions.cs](#programcs) sections.
>
>

### <a name="contosoadscommon---adcs"></a>ContosoAdsCommon - Ad.cs
fichier de Ad.cs Hello définit un enum pour les catégories d’Active Directory et une classe d’entité POCO pour les informations Active Directory.

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

### <a name="contosoadscommon---contosoadscontextcs"></a>ContosoAdsCommon - ContosoAdsContext.cs
Hello ContosoAdsContext classe spécifie que la classe de publicité de hello est utilisée dans une collection DbSet, Entity Framework stocke dans une base de données SQL.

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

classe Hello possède deux constructeurs. tout d’abord Hello est utilisé par le projet de hello web et spécifie le nom de hello d’une chaîne de connexion qui est stockée dans le fichier Web.config de hello ou un environnement d’exécution Azure hello. constructeur de deuxième Hello vous permet de toopass dans la chaîne de connexion de hello. Qui est requis par le projet de tâche Web hello car celui-ci ne dispose d’un fichier Web.config. Vous savez où cette chaîne de connexion a été stockée, et vous verrez plus tard comment les code hello récupère la chaîne de connexion hello lorsqu’il instancie la classe DbContext de hello.

### <a name="contosoadscommon---blobinformationcs"></a>ContosoAdsCommon - BlobInformation.cs
Hello `BlobInformation` classe est utilisée toostore d’informations sur un objet blob d’image dans un message de la file d’attente.

        public class BlobInformation
        {
            public Uri BlobUri { get; set; }

            public string BlobName
            {
                get
                {
                    return BlobUri.Segments[BlobUri.Segments.Length - 1];
                }
            }
            public string BlobNameWithoutExtension
            {
                get
                {
                    return Path.GetFileNameWithoutExtension(BlobName);
                }
            }
            public int AdId { get; set; }
        }


### <a name="contosoadsweb---globalasaxcs"></a>ContosoAdsWeb - Global.asax.cs
Code qui est appelé à partir de hello `Application_Start` méthode crée un *images* conteneur d’objets blob et un *images* file d’attente si elles n’existent pas déjà. Cela garantit que chaque fois que vous démarrez à l’aide d’un compte de stockage, hello requis file d’attente et le conteneur d’objets blob sont créés automatiquement.

Hello compte de stockage toohello code obtient l’accès à l’aide de chaînes de connexion de stockage hello de hello *Web.config* fichier ou un environnement d’exécution Azure.

        var storageAccount = CloudStorageAccount.Parse
            (ConfigurationManager.ConnectionStrings["AzureWebJobsStorage"].ToString());

Ensuite, il obtient une référence toohello *images* conteneur d’objets blob, crée le conteneur de hello si elle n’existe pas déjà, et définit les autorisations sur le conteneur hello d’accès. Par défaut, les nouveaux conteneurs autorisent uniquement les clients avec des objets BLOB de stockage compte informations d’identification tooaccess. l’application web Hello doit hello BLOB toobe public afin qu’il peut afficher des images à l’aide de l’URL que BLOB d’image toohello de point de.

        var blobClient = storageAccount.CreateCloudBlobClient();
        var imagesBlobContainer = blobClient.GetContainerReference("images");
        if (imagesBlobContainer.CreateIfNotExists())
        {
            imagesBlobContainer.SetPermissions(
                new BlobContainerPermissions
                {
                    PublicAccess = BlobContainerPublicAccessType.Blob
                });
        }

Un code similaire Obtient une référence toohello *thumbnailrequest* de file d’attente et crée une nouvelle file d’attente. Dans ce cas, aucune modification des autorisations n'est nécessaire.

        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
        var imagesQueue = queueClient.GetQueueReference("thumbnailrequest");
        imagesQueue.CreateIfNotExists();

### <a name="contosoadsweb---layoutcshtml"></a>ContosoAdsWeb - _Layout.cshtml
Hello *_Layout.cshtml* fichier définit le nom de l’application hello dans l’en-tête de hello et de pied de page et crée une entrée de menu « Annonces ».

### <a name="contosoadsweb---viewshomeindexcshtml"></a>ContosoAdsWeb - Views\Home\Index.cshtml
Hello *Views\Home\Index.cshtml* fichier affiche les liens de catégorie sur la page d’accueil hello. les liens Hello passent entier hello hello `Category` enum dans une page d’Index de publicités toohello variable querystring.

        <li>@Html.ActionLink("Cars", "Index", "Ad", new { category = (int)Category.Cars }, null)</li>
        <li>@Html.ActionLink("Real estate", "Index", "Ad", new { category = (int)Category.RealEstate }, null)</li>
        <li>@Html.ActionLink("Free stuff", "Index", "Ad", new { category = (int)Category.FreeStuff }, null)</li>
        <li>@Html.ActionLink("All", "Index", "Ad", null, null)</li>

### <a name="contosoadsweb---adcontrollercs"></a>ContosoAdsWeb - AdController.cs
Bonjour *AdController.cs* fichier, les appels de constructeur Bonjour Bonjour `InitializeStorage` méthode toocreate bibliothèque cliente de stockage Azure objets qui fournissent une API pour l’utilisation des objets BLOB et files d’attente.

Code de hello extrait ensuite une référence toohello *images* conteneur d’objets blob comme vous l’avez vu précédemment dans *Global.asax.cs*. Ce faisant, il définit une [stratégie de nouvelles tentatives](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) par défaut appropriée pour une application web. stratégie de nouvelle tentative interruption exponentielle Hello par défaut se bloque hello web app pour plus d’une minute sur les tentatives répétées d’une erreur transitoire. stratégie de nouvelle tentative Hello spécifié ici attend trois secondes après chacun pour des tentatives de toothree.

        var blobClient = storageAccount.CreateCloudBlobClient();
        blobClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
        imagesBlobContainer = blobClient.GetContainerReference("images");

Un code similaire Obtient une référence toohello *images* file d’attente.

        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
        queueClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
        imagesQueue = queueClient.GetQueueReference("blobnamerequest");

La plupart du code du contrôleur hello est typique pour travailler avec un modèle de données Entity Framework à l’aide d’une classe DbContext. Une exception est hello HttpPost `Create` (méthode), qui télécharge un fichier et l’enregistre dans le stockage blob. classeur de modèles Hello fournit un [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) toohello méthode de l’objet.

        [HttpPost]
        [ValidateAntiForgeryToken]
        public async Task<ActionResult> Create(
            [Bind(Include = "Title,Price,Description,Category,Phone")] Ad ad,
            HttpPostedFileBase imageFile)

Si l’utilisateur hello sélectionné un tooupload de fichier, code de hello télécharge hello fichier enregistre dans un objet blob et met à jour d’enregistrement de base de données Ad hello avec une URL qui pointe toohello blob.

        if (imageFile != null && imageFile.ContentLength != 0)
        {
            blob = await UploadAndSaveBlobAsync(imageFile);
            ad.ImageURL = blob.Uri.ToString();
        }

Hello code hello téléchargement est hello `UploadAndSaveBlobAsync` (méthode). Il crée un nom GUID pour les objets blob de hello, téléchargements et enregistre le fichier hello et retourne un objet blob de référence toohello enregistré.

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

Après avoir hello HttpPost `Create` méthode télécharge un objet blob et les mises à jour hello de base de données, il crée un file d’attente message tooinform hello au processus principal qu’une image est prête pour la miniature tooa de conversion.

        BlobInformation blobInfo = new BlobInformation() { AdId = ad.AdId, BlobUri = new Uri(ad.ImageURL) };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        await thumbnailRequestQueue.AddMessageAsync(queueMessage);

Hello code hello HttpPost `Edit` méthode est similaire, mais si l’utilisateur de hello sélectionne un fichier image, tous les objets BLOB qui existent déjà pour cette ad doivent être supprimés.

        if (imageFile != null && imageFile.ContentLength != 0)
        {
            await DeleteAdBlobsAsync(ad);
            imageBlob = await UploadAndSaveBlobAsync(imageFile);
            ad.ImageURL = imageBlob.Uri.ToString();
        }

Voici le code hello qui supprime des objets BLOB lorsque vous supprimez une annonce :

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

### <a name="contosoadsweb---viewsadindexcshtml-and-detailscshtml"></a>ContosoAdsWeb - Views\Ad\Index.cshtml et Details.cshtml
Hello *Index.cshtml* fichier affiche les miniatures avec hello autres données d’Active Directory :

        <img  src="@Html.Raw(item.ThumbnailURL)" />

Hello *Details.cshtml* fichier image en taille réelle de hello s’affiche :

        <img src="@Html.Raw(Model.ImageURL)" />

### <a name="contosoadsweb---viewsadcreatecshtml-and-editcshtml"></a>ContosoAdsWeb - Views\Ad\Create.cshtml et Edit.cshtml
Hello *Create.cshtml* et *Edit.cshtml* fichiers spécifient qu’Active hello hello tooget de contrôleur d’encodage de formulaire `HttpPostedFileBase` objet.

        @using (Html.BeginForm("Create", "Ad", FormMethod.Post, new { enctype = "multipart/form-data" }))

Un `<input>` élément indique hello navigateur tooprovide une boîte de dialogue de sélection de fichier.

        <input type="file" name="imageFile" accept="image/*" class="form-control fileupload" />

### <a id="programcs"></a>ContosoAdsWebJob - Program.cs
Lorsque hello démarre la tâche Web hello `Main` les appels de méthode hello WebJobs SDK `JobHost.RunAndBlock` toobegin exécution de la méthode de fonctions déclenchées sur le thread en cours de hello.

        static void Main(string[] args)
        {
            JobHost host = new JobHost();
            host.RunAndBlock();
        }

### <a id="generatethumbnail"></a>ContosoAdsWebJob - Functions.cs - Méthode GenerateThumbnail
Hello WebJobs SDK appelle cette méthode lorsqu’un message de la file d’attente est reçu. méthode Hello crée une miniature et met hello miniature URL dans la base de données hello.

        public static void GenerateThumbnail(
        [QueueTrigger("thumbnailrequest")] BlobInformation blobInfo,
        [Blob("images/{BlobName}", FileAccess.Read)] Stream input,
        [Blob("images/{BlobNameWithoutExtension}_thumbnail.jpg")] CloudBlockBlob outputBlob)
        {
            using (Stream output = outputBlob.OpenWrite())
            {
                ConvertImageToThumbnailJPG(input, output);
                outputBlob.Properties.ContentType = "image/jpeg";
            }

            // Entity Framework context class is not thread-safe, so it must
            // be instantiated and disposed within hello function.
            using (ContosoAdsContext db = new ContosoAdsContext())
            {
                var id = blobInfo.AdId;
                Ad ad = db.Ads.Find(id);
                if (ad == null)
                {
                    throw new Exception(String.Format("AdId {0} not found, can't create thumbnail", id.ToString()));
                }
                ad.ThumbnailURL = outputBlob.Uri.ToString();
                db.SaveChanges();
            }
        }

* Hello `QueueTrigger` attribut dirige hello WebJobs SDK toocall cette méthode lorsqu’un nouveau message est reçu dans la file d’attente de thumbnailrequest hello.

        [QueueTrigger("thumbnailrequest")] BlobInformation blobInfo,

    Hello `BlobInformation` objet dans le message de file d’attente hello est automatiquement désérialisée en hello `blobInfo` paramètre. Lors de la fin de la méthode hello, message de file d’attente hello est supprimé. Si la méthode hello échoue avant la fin, le message de file d’attente hello n’est pas supprimé ; après l’expiration d’un bail de 10 minutes, message de type hello est lancé toobe nouveau récupéré et traité. Cette séquence ne se répète pas indéfiniment si un message provoque toujours une exception. Après échec de 5 tentatives tooprocess un message, message de type hello est déplacé tooa file d’attente nommée {nom}-incohérents. Hello le nombre maximal de tentatives est configurable.
* deux Hello `Blob` attributs fournissent des objets qui sont liées tooblobs : un toohello existant objet blob d’image et un tooa nouvelle miniature blob qui crée de la méthode hello.

        [Blob("images/{BlobName}", FileAccess.Read)] Stream input,
        [Blob("images/{BlobNameWithoutExtension}_thumbnail.jpg")] CloudBlockBlob outputBlob)

    Noms d’objets BLOB proviennent des propriétés de hello `BlobInformation` objet reçu dans le message de file d’attente hello (`BlobName` et `BlobNameWithoutExtension`). tooget hello toutes les fonctionnalités de hello bibliothèque cliente de stockage, vous pouvez utiliser hello `CloudBlockBlob` toowork de classe avec des objets BLOB. Si vous souhaitez tooreuse le code qui a été écrite toowork avec `Stream` des objets, vous pouvez utiliser hello `Stream` classe.

Pour plus d’informations sur le mode de fonctionnement toowrite qui utilisent des attributs WebJobs SDK, consultez hello suivant des ressources :

* [Comment toouse Azure file d’attente de stockage avec hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md)
* [Comment toouse Azure stockage d’objets blob par hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)
* [Comment toouse Azure table storage avec hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-tables-how-to.md)
* [Comment toouse Azure Service Bus avec hello WebJobs SDK](websites-dotnet-webjobs-sdk-service-bus.md)

> [!NOTE]
> * Si votre application web s’exécute sur plusieurs machines virtuelles, plusieurs tâches Web s’exécuteront simultanément et dans certains scénarios, cela peut entraîner de hello même les données traitées plusieurs fois. Cela n’est pas un problème si vous utilisez la file d’attente intégrées de hello, blob et les déclencheurs de Service Bus. Hello SDK garantit que vos fonctions seront traitées qu’une seule fois pour chaque message ou d’un objet blob.
> * Pour plus d’informations sur l’arrêt correct de tooimplement, consultez [l’arrêt approprié](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#graceful).
> * Hello code Bonjour `ConvertImageToThumbnailJPG` (méthode) (non affiché) utilise des classes hello `System.Drawing` espace de noms par souci de simplicité. Toutefois, les classes de hello dans cet espace de noms ont été conçues pour une utilisation avec Windows Forms. Elles ne sont pas prises en charge dans un service Windows ou ASP.NET. Pour plus d’informations sur les options de traitement d’images, consultez les rubriques [Génération d’images dynamiques](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) et [Redimensionnement d’images approfondi](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na).
>
>

## <a name="next-steps"></a>Étapes suivantes
Dans ce didacticiel, vous avez vu d’une application à plusieurs niveaux simple qui utilise hello WebJobs SDK pour le traitement du serveur principal. Cette section propose des suggestions pour en savoir plus sur les applications à plusieurs niveaux ASP.NET et WebJobs.

### <a name="missing-features"></a>Fonctionnalités manquantes
application Hello a été conservée simple pour obtenir un didacticiel de mise en route. Dans une application réelle, vous pouvez implémenter [injection de dépendance](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) et hello [référentiel et une unité de travaillent des modèles](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), utilisez [une interface pour la journalisation](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), utilisez [ Migrations EF Code First](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage données modifications sur le modèle et utiliser [résilience des connexions EF](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage les erreurs temporaires du réseau.

### <a name="scaling-webjobs"></a>Mise à l’échelle de WebJobs
Les tâches Web s’exécutent dans le contexte de hello d’une application web, ne sont pas évolutifs séparément. Par exemple, si vous avez une instance d’application web Standard, vous n'avez qu’une seule instance du processus d’arrière-plan en cours d’exécution et qu’il utilise certaines hello des ressources du serveur (processeur, mémoire, etc.) qui seraient sinon le contenu web tooserve disponibles.

Si le trafic varie selon le temps ou le jour de la semaine, et si principal hello traitement vous devez toodo peut attendre, vous pouvez planifier votre toorun tâches Web à des moments de faible trafic. Si la charge de hello est toujours trop élevé pour cette solution, vous pouvez exécuter hello principal en tant qu’une tâche Web dans une application web distinct dédiée à cet effet. Vous pouvez ensuite faire évoluer votre application web principale indépendamment de votre application web frontale.

Pour plus d’informations, consultez [Mise à l’échelle WebJobs](websites-webjobs-resources.md#scale).

### <a name="avoiding-web-app-timeout-shut-downs"></a>Éviter les arrêts dus à l’expiration des applications web
toomake que vos tâches Web sont toujours en cours d’exécution et en cours d’exécution sur toutes les instances de votre application web, vous avez tooenable hello [AlwaysOn](http://weblogs.asp.net/scottgu/archive/2014/01/16/windows-azure-staging-publishing-support-for-web-sites-monitoring-improvements-hyper-v-recovery-manager-ga-and-pci-compliance.aspx) fonctionnalité.

### <a name="using-hello-webjobs-sdk-outside-of-webjobs"></a>À l’aide de hello SDK WebJobs en dehors des tâches Web
Un programme qui utilise hello WebJobs SDK ne toorun dans Azure dans une tâche Web. Il peut s'exécuter localement, ou dans d'autres environnements tels qu'un rôle de travail de service cloud ou un service Windows. Toutefois, vous pouvez uniquement accéder hello du tableau de bord WebJobs SDK via une application web Azure. tableau de bord hello toouse vous avez tooconnect hello web application toohello compte de stockage que vous utilisez des en définissant la chaîne de connexion AzureWebJobsDashboard hello sur hello **configurer** onglet du portail classique de hello. Ensuite, vous pouvez obtenir toohello du tableau de bord à l’aide de hello suivant l’URL :

https://{nom_d’application_web}.scm.azurewebsites.net/azurejobs/#/functions

Pour plus d’informations, consultez [mise en route d’un tableau de bord pour un développement local avec hello WebJobs SDK](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx), mais notez qu’elle affiche un ancien nom de chaîne de connexion.

### <a name="more-webjobs-documentation"></a>Plus de documentation relative à WebJobs
Pour plus d’informations, consultez [Ressources de documentation relatives à Azure WebJobs](http://go.microsoft.com/fwlink/?LinkId=390226).
