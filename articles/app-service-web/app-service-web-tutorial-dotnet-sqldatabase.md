---
title: "aaaBuild une application ASP.NET dans Azure avec la base de données SQL | Documents Microsoft"
description: "Découvrez comment tooget un ASP.NET application fonctionne dans Azure, avec tooa de connexion de base de données SQL."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 03c584f1-a93c-4e3d-ac1b-c82b50c75d3e
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: csharp
ms.topic: tutorial
ms.date: 06/09/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: d21c2bc404bfe038608c17e5a94d96847153002c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="build-an-aspnet-app-in-azure-with-sql-database"></a>Création d’une application ASP.NET dans Azure avec SQL Database

[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) offre un service d’hébergement web hautement évolutif appliquant des mises à jour correctives automatiques. Ce didacticiel vous montre comment toodeploy un ASP.NET piloté par les données de l’application dans Azure web et le connecter trop[base de données SQL Azure](../sql-database/sql-database-technical-overview.md). Lorsque vous avez terminé, vous disposez d’une application ASP.NET en cours d’exécution [Azure App Service](../app-service/app-service-value-prop-what-is.md) et connecté tooSQL de base de données.

![Application ASP.NET publiée dans une application web Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/azure-app-in-browser.png)

Ce didacticiel vous montre comment effectuer les opérations suivantes :

> [!div class="checklist"]
> * Créer une base de données SQL dans Azure
> * Se connecter à un tooSQL d’application ASP.NET de base de données
> * Déployer hello application tooAzure
> * Mettre à jour le modèle de données hello et redéployer l’application hello
> * Journaux des flux de données à partir d’Azure tooyour Terminal Server
> * Gérer l’application hello Bonjour portail Azure

## <a name="prerequisites"></a>Composants requis

toocomplete ce didacticiel :

* Installer [Visual Studio 2017](https://www.visualstudio.com/downloads/) avec hello suivant les charges de travail :
  - **Développement web et ASP.NET**
  - **Développement Azure**

  ![Développement web et ASP.NET et Développement Azure (sous Web et cloud)](media/app-service-web-tutorial-dotnet-sqldatabase/workloads.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-hello-sample"></a>Télécharger l’exemple hello

[Télécharger l’exemple de projet hello](https://github.com/Azure-Samples/dotnet-sqldb-tutorial/archive/master.zip).

Extraire (décompresser) hello *dotnet-sqldb-didacticiel-master.zip* fichier.

exemple de projet Hello contient une basic [ASP.NET MVC](https://www.asp.net/mvc) CRUD (create-lecture-mise à jour-suppression) à l’aide d’application [Entity Framework Code First](/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).

### <a name="run-hello-app"></a>Exécutez l’application hello

Ouvrez hello *dotnet-sqldb-didacticiel-master/DotNetAppSqlDb.sln* fichier dans Visual Studio. 

Type `Ctrl+F5` application hello de toorun sans débogage. application Hello s’affiche dans votre navigateur par défaut. Sélectionnez hello **créer un nouveau** lier et créer quelques *action* éléments. 

![Boîte de dialogue New ASP.NET Project](media/app-service-web-tutorial-dotnet-sqldatabase/local-app-in-browser.png)

Hello de test **modifier**, **détails**, et **supprimer** des liens.

application Hello utilise un tooconnect de contexte de base de données avec la base de données hello. Dans cet exemple, le contexte de base de données hello utilise une chaîne de connexion nommée `MyDbConnection`. chaîne de connexion Hello est définie dans hello *Web.config* de fichiers et référencé dans hello *Models/MyDatabaseContext.cs* fichier. nom de chaîne de connexion Hello est utilisé ultérieurement dans Azure web application tooan base de données SQL Azure hello tooconnect didacticiel hello. 

## <a name="publish-tooazure-with-sql-database"></a>Publier tooAzure avec la base de données SQL

Bonjour **l’Explorateur de solutions**, cliquez sur votre **DotNetAppSqlDb** de projet et sélectionnez **publier**.

![Publier à partir de l’Explorateur de solutions](./media/app-service-web-tutorial-dotnet-sqldatabase/solution-explorer-publish.png)

Assurez-vous que **Microsoft Azure App Service** est sélectionné et cliquez sur **Publier**.

![Publier à partir de la page de présentation du projet](./media/app-service-web-tutorial-dotnet-sqldatabase/publish-to-app-service.png)

Publication ouvre hello **créer un Service application** boîte de dialogue, qui vous permet de créer tous les hello ressources Azure, vous devez toorun votre application de web ASP.NET dans Azure.

### <a name="sign-in-tooazure"></a>Connectez-vous à tooAzure

Bonjour **créer un Service application** boîte de dialogue, cliquez sur **ajouter un compte**, puis connectez-vous à tooyour abonnement Azure. Si vous êtes déjà connecté à un compte Microsoft, assurez-vous que le compte conserve votre abonnement Azure. Si votre abonnement Azure n’a pas hello signé Microsoft compte, cliquez dessus compte tooadd hello.
   
![Connectez-vous à tooAzure](./media/app-service-web-tutorial-dotnet-sqldatabase/sign-in-azure.png)

Une fois connecté, vous êtes prêt toocreate que tous hello ressources dont vous avez besoin pour votre application web Azure dans cette boîte de dialogue.

### <a name="configure-hello-web-app-name"></a>Configurer le nom de l’application hello web

Vous pouvez conserver le nom de l’application web hello généré, ou modifier le nom unique de tooanother (les caractères valides sont `a-z`, `0-9`, et `-`). nom de l’application web Hello est utilisé dans le cadre de l’URL par défaut de hello pour votre application (`<app_name>.azurewebsites.net`, où `<app_name>` est le nom de votre application web). nom de l’application web Hello doit toobe unique entre toutes les applications dans Azure. 

![Boîte de dialogue Créer App Service](media/app-service-web-tutorial-dotnet-sqldatabase/wan.png)

### <a name="create-a-resource-group"></a>Créer un groupe de ressources

[!INCLUDE [resource-group](../../includes/resource-group.md)]

Suivant trop**groupe de ressources**, cliquez sur **nouveau**.

![TooResource suivant groupe, cliquez sur Nouveau.](media/app-service-web-tutorial-dotnet-sqldatabase/new_rg2.png)

Groupe de ressources de nom hello **myResourceGroup**.

> [!NOTE]
> Ne cliquez pas sur **Créer**. Vous devez tout d’abord tooset une base de données SQL dans une étape ultérieure.

### <a name="create-an-app-service-plan"></a>Créer un plan App Service

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

Suivant trop**du Plan App Service**, cliquez sur **nouveau**. 

Bonjour **configurer un Plan App Service** boîte de dialogue Configurer le nouveau plan de Service de l’application hello avec hello suivant les paramètres :

![Créer un plan App Service](./media/app-service-web-tutorial-dotnet-sqldatabase/configure-app-service-plan.png)

| Paramètre  | Valeur suggérée | Pour plus d’informations |
| ----------------- | ------------ | ----|
|**Plan App Service**| myAppServicePlan | [Plans App Service](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) |
|**Emplacement**| Europe de l'Ouest | [Régions Azure](https://azure.microsoft.com/regions/) |
|**Taille**| Gratuit | [Niveaux de tarification](https://azure.microsoft.com/pricing/details/app-service/)|

### <a name="create-a-sql-server-instance"></a>Créer une instance SQL Server

Pour créer une base de données, il vous faut un [serveur logique Azure SQL Database](../sql-database/sql-database-features.md). Un serveur logique contient un groupe de bases de données gérées en tant que groupe.

Sélectionnez **Explorer des services Azure supplémentaires**.

![Configurer le nom de l’application web](media/app-service-web-tutorial-dotnet-sqldatabase/web-app-name.png)

Bonjour **Services** , cliquez sur hello  **+**  icône suivant trop**base de données SQL**. 

![Dans l’onglet Services de hello, cliquez sur l’icône + hello tooSQL suivant de base de données.](media/app-service-web-tutorial-dotnet-sqldatabase/sql.png)

Bonjour **configurer la base de données SQL** boîte de dialogue, cliquez sur **nouveau** suivant trop**SQL Server**. 

Un nom de serveur unique est généré. Ce nom est utilisé dans le cadre de l’URL par défaut de hello pour votre serveur logique, `<server_name>.database.windows.net`. Il doit être unique parmi toutes les instances de serveur logique dans Azure. Vous pouvez modifier le nom du serveur hello, mais pour ce didacticiel, conservez la valeur de l’hello généré.

Ajoutez un nom d’utilisateur administrateur et un mot de passe, puis sélectionnez **OK**. Pour plus d’informations sur la complexité requise des mots de passe, consultez [Stratégie de mot de passe](/sql/relational-databases/security/password-policy).

Gardez en tête ce nom d'utilisateur et ce mot de passe. Vous avez besoin serveur logique de hello toomanage instance ultérieurement.

![Créer une instance SQL Server](media/app-service-web-tutorial-dotnet-sqldatabase/configure-sql-database-server.png)

### <a name="create-a-sql-database"></a>Création d’une base de données SQL

Bonjour **configurer la base de données SQL** boîte de dialogue : 

* Conservez généré de la valeur par défaut hello **nom de la base de données**.
* Dans **Nom de la chaîne de connexion**, saisissez *MyDbConnection*. Ce nom doit correspondre la chaîne de connexion hello qui est référencé dans *Models/MyDatabaseContext.cs*.
* Sélectionnez **OK**.

![Configurer SQL Database](media/app-service-web-tutorial-dotnet-sqldatabase/configure-sql-database.png)

Hello **créer un Service application** boîte de dialogue affiche les ressources hello que vous avez créé. Cliquez sur **Créer**. 

![ressources Hello que vous avez créé](media/app-service-web-tutorial-dotnet-sqldatabase/app_svc_plan_done.png)

Une fois l’Assistant de hello ait fini de créer des ressources Azure hello, elle publie votre tooAzure d’application ASP.NET. Votre navigateur par défaut est lancé avec application de hello URL toohello déployé. 

Ajoutez quelques tâches.

![Application ASP.NET publiée dans une application web Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/azure-app-in-browser.png)

Félicitations ! Votre application ASP.NET orientée données s’exécute dans Azure App Service.

## <a name="access-hello-sql-database-locally"></a>Accéder localement hello de base de données SQL

Visual Studio vous permet d’Explorer et gérer votre nouvelle base de données SQL facilement dans hello **l’Explorateur d’objets SQL Server**.

### <a name="create-a-database-connection"></a>Créer une connexion à la base de données

À partir de hello **vue** menu, sélectionnez **l’Explorateur d’objets SQL Server**.

Haut hello **l’Explorateur d’objets SQL Server**, cliquez sur hello **ajouter SQL Server** bouton.

### <a name="configure-hello-database-connection"></a>Configurer la connexion de base de données hello

Bonjour **Connect** boîte de dialogue, développez hello **Azure** nœud. Toutes vos instances SQL Database dans Azure sont répertoriées ici.

Sélectionnez hello `DotNetAppSqlDb` base de données SQL. connexion Hello que vous avez créé précédemment est renseignée automatiquement en bas de hello.

Tapez le mot de passe administrateur de base de données hello vous avez créé précédemment et cliquez sur **connexion**.

![Configurer la connexion à la base de données à partir de Visual Studio](./media/app-service-web-tutorial-dotnet-sqldatabase/connect-to-sql-database.png)

### <a name="allow-client-connection-from-your-computer"></a>Autoriser une connexion client à partir de votre ordinateur

Hello **créer une nouvelle règle de pare-feu** boîte de dialogue est ouverte. Par défaut, votre instance SQL Database n’autorise que les connexions provenant de services Azure, comme votre application web Azure. tooconnect tooyour de base de données, créer une règle de pare-feu dans l’instance de base de données SQL hello. règle de pare-feu Hello permet hello adresse IP publique de votre ordinateur local.

boîte de dialogue Hello est déjà remplie avec l’adresse IP de votre ordinateur.

Assurez-vous que la case **Ajouter mon adresse IP cliente** est cochée, puis cliquez sur **OK**. 

![Configuration du pare-feu pour l’instance SQL Database](./media/app-service-web-tutorial-dotnet-sqldatabase/sql-set-firewall.png)

Une fois que Visual Studio a terminé la création du paramètre de pare-feu hello pour votre instance de base de données SQL, votre connexion s’affiche dans **l’Explorateur d’objets SQL Server**.

Ici, vous pouvez effectuer hello de base de données opérations les plus courantes, telles que les requêtes de l’exécution, créent des vues et procédures stockées et bien plus encore. 

Avec le bouton droit sur hello `Todoes` de table et sélectionnez **des données d’affichage**. 

![Explorer les objets SQL Database](./media/app-service-web-tutorial-dotnet-sqldatabase/explore-sql-database.png)

## <a name="update-app-with-code-first-migrations"></a>Mettre à jour l’application avec les Code First Migrations

Vous pouvez utiliser des outils familiers de hello dans Visual Studio tooupdate votre base de données et l’application web dans Azure. Dans cette étape, vous utilisez Migrations Code First dans Entity Framework toomake un schéma de base de données modifiées tooyour et publiez tooAzure.

Pour plus d’informations sur l’utilisation de Migrations Entity Framework Code First, consultez [Getting Started with Entity Framework 6 Code First using MVC 5 (Mise en route avec Entity Framework 6 Code First à l’aide de MVC 5)](https://docs.microsoft.com/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).

### <a name="update-your-data-model"></a>Mettre à jour votre modèle de données

Ouvrez _Models\Todo.cs_ dans l’éditeur de code hello. Ajouter hello suivant propriété toohello `ToDo` classe :

```csharp
public bool Done { get; set; }
```

### <a name="run-code-first-migrations-locally"></a>Exécuter la fonction Code First Migrations en local

Exécuter quelques commandes toomake mises à jour tooyour base de données locale. 

À partir de hello **outils** menu, cliquez sur **Gestionnaire de Package NuGet** > **Package Manager Console**.

Dans la fenêtre de Console du Gestionnaire de Package de hello, activer les Migrations Code First :

```PowerShell
Enable-Migrations
```

Ajoutez une migration :

```PowerShell
Add-Migration AddProperty
```

Mise à jour de la base de données locale hello :

```PowerShell
Update-Database
```

Type `Ctrl+F5` toorun hello application. Hello de test, modifier les détails et créer des liens.

Si l’application hello se charge sans erreur, les Migrations Code First a réussi. Toutefois, votre recherche toujours page hello identiques car votre logique d’application n’utilise pas encore cette nouvelle propriété. 

### <a name="use-hello-new-property"></a>Utiliser la nouvelle propriété de hello

Apportez des modifications à votre hello toouse de code `Done` propriété. Par souci de simplicité dans ce didacticiel, vous allez uniquement toochange hello `Index` et `Create` affiche la propriété de hello toosee en action.

Ouvrez _Controllers\TodosController.cs_.

Recherche hello `Create()` (méthode) et ajoutez `Done` toohello la liste des propriétés Bonjour `Bind` attribut. Lorsque vous avez terminé, votre `Create()` signature de méthode ressemble à hello suivant de code :

```csharp
public ActionResult Create([Bind(Include = "id,Description,CreatedDate,Done")] Todo todo)
```

Ouvrez _Views\Todos\Create.cshtml_.

Bonjour code Razor, vous devez voir un `<div class="form-group">` élément utilise `model.Description`et un autre `<div class="form-group">` élément utilise `model.CreatedDate`. Juste après ces deux éléments, ajoutez un autre élément `<div class="form-group">` qui utilise `model.Done` :

```csharp
<div class="form-group">
    @Html.LabelFor(model => model.Done, htmlAttributes: new { @class = "control-label col-md-2" })
    <div class="col-md-10">
        <div class="checkbox">
            @Html.EditorFor(model => model.Done)
            @Html.ValidationMessageFor(model => model.Done, "", new { @class = "text-danger" })
        </div>
    </div>
</div>
```

Ouvrez _Views\Todos\Index.cshtml_.

Recherchez hello vide `<th></th>` élément. Juste au-dessus de cet élément, ajoutez hello suivant de code Razor :

```csharp
<th>
    @Html.DisplayNameFor(model => model.Done)
</th>
```

Recherche hello `<td>` élément contenant hello `Html.ActionLink()` méthodes d’assistance. Juste au-dessus de cet élément, ajoutez hello suivant de code Razor :

```csharp
<td>
    @Html.DisplayFor(modelItem => item.Done)
</td>
```

Que vous n’avez rien toosee des modifications de hello Bonjour `Index` et `Create` vues. 

Type `Ctrl+F5` toorun hello application.

Vous pouvez maintenant ajouter un élément de tâche et cocher **Terminé**. Cette tâche devrait ensuite apparaître dans votre page d’accueil comme un élément terminé. N’oubliez pas que hello `Edit` vue n’affiche pas hello `Done` champ, car vous n’avez pas modifier hello `Edit` vue.

### <a name="enable-code-first-migrations-in-azure"></a>Activer Code First Migrations dans Azure

Maintenant que votre code modifier fonctionne, dont la migration de la base de données, vous publiez tooyour Azure web app et mettre à jour trop de votre base de données SQL avec les Migrations Code First.

Comme précédemment, cliquez avec le bouton droit sur votre projet et sélectionnez **Publier**.

Cliquez sur **paramètres** tooopen hello Assistant de publication.

![Ouvrir les paramètres de publication](./media/app-service-web-tutorial-dotnet-sqldatabase/publish-settings.png)

Dans l’Assistant de hello, cliquez sur **suivant**.

Assurez-vous que cette chaîne de connexion hello pour votre base de données SQL est remplie dans **MyDatabaseContext (MyDbConnection)**. Vous devrez peut-être tooselect hello **myToDoAppDb** base de données à partir de la liste déroulante de hello. 

Sélectionnez **Exécuter les migrations Code First (s’exécute au démarrage de l’application)**, puis cliquez sur **Enregistrer**.

![Activer Code First Migrations dans l’application web Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/enable-migrations.png)

### <a name="publish-your-changes"></a>Publier vos modifications

Maintenant que vous avez activé les Migrations Code First dans votre application web Azure, publiez vos modifications du code.

Bonjour, page Publier, cliquez sur **publier**.

Essayez d’ajouter à nouveau des tâches et de sélectionner **Terminé** : elles doivent apparaître dans votre page d’accueil comme éléments terminés.

![Application web Azure après l’activation de Code First Migration](./media/app-service-web-tutorial-dotnet-sqldatabase/this-one-is-done.png)

Toutes les tâches existantes sont toujours affichées. Lorsque vous republiez votre application ASP.NET, les données existantes dans votre instance SQL Database ne sont pas perdues. En outre, les Migrations Code First modifie uniquement schéma de données hello et conserve vos données existantes intact.


## <a name="stream-application-logs"></a>Diffuser les journaux d’applications

Vous pouvez diffuser des messages de suivi directement à partir de votre tooVisual d’application web Azure Studio.

Ouvrez _Controllers\TodosController.cs_.

Chaque action commence par une méthode `Trace.WriteLine()`. Ce code est ajouté tooshow vous comment les messages de trace de tooadd tooyour Azure web app.

### <a name="open-server-explorer"></a>Ouvrir l’Explorateur de serveurs

À partir de hello **vue** menu, sélectionnez **l’Explorateur de serveurs**. Vous pouvez configurer la journalisation pour votre application web Azure dans **l’Explorateur de serveurs**. 

### <a name="enable-log-streaming"></a>Activer la diffusion de journaux

Dans **l’Explorateur de serveurs**, développez **Azure** > **App Service**.

Développez hello **myResourceGroup** groupe de ressources, vous avez créé lors de la création d’application web Azure de hello.

Cliquez avec le bouton droit sur votre application web Azure et sélectionnez **Afficher les journaux de streaming**.

![Activer la diffusion de journaux](./media/app-service-web-tutorial-dotnet-sqldatabase/stream-logs.png)

Hello journaux sont maintenant transmis en hello **sortie** fenêtre. 

![Diffusion des journaux dans la fenêtre Sortie](./media/app-service-web-tutorial-dotnet-sqldatabase/log-streaming-pane.png)

Toutefois, vous ne voyez pas un des messages de trace hello encore. C’est la parce que, lorsque vous sélectionnez **afficher les journaux de diffusion en continu**, votre application web Azure définit le niveau de trace hello trop`Error`, qui enregistre uniquement les événements d’erreur (avec hello `Trace.TraceError()` méthode).

### <a name="change-trace-levels"></a>Modifier les niveaux de suivi

trace de hello toochange niveaux toooutput autres messages de trace, accédez précédent trop**l’Explorateur de serveurs**.

Cliquez de nouveau avec le bouton droit sur votre application web Azure et sélectionnez **Paramètres**.

Bonjour **journalisation des applications (système de fichiers)** liste déroulante, sélectionnez **Verbose**. Cliquez sur **Enregistrer**.

![Modifier tooVerbose au niveau de trace](./media/app-service-web-tutorial-dotnet-sqldatabase/trace-level-verbose.png)

> [!TIP]
> Vous pouvez expérimenter trace différents niveaux toosee quels types de messages sont affichés pour chaque niveau. Par exemple, hello **informations** niveau inclut tous les journaux créés par `Trace.TraceInformation()`, `Trace.TraceWarning()`, et `Trace.TraceError()`, mais pas les journaux créés par `Trace.WriteLine()`.
>
>

Dans votre navigateur, essayez de cliquer sur l’application de liste de tâches hello dans Azure. les messages de trace Hello sont transmises maintenant toohello **sortie** fenêtre dans Visual Studio.

```
Application: 2017-04-06T23:30:41  PID[8132] Verbose     GET /Todos/Index
Application: 2017-04-06T23:30:43  PID[8132] Verbose     GET /Todos/Create
Application: 2017-04-06T23:30:53  PID[8132] Verbose     POST /Todos/Create
Application: 2017-04-06T23:30:54  PID[8132] Verbose     GET /Todos/Index
```



### <a name="stop-log-streaming"></a>Arrêter la diffusion de journaux

toostop hello service de diffusion en continu de journal, cliquez sur hello **arrêter l’analyse** bouton Bonjour **sortie** fenêtre.

![Arrêter la diffusion de journaux](./media/app-service-web-tutorial-dotnet-sqldatabase/stop-streaming.png)

## <a name="manage-your-azure-web-app"></a>Gérer votre application web Azure

Accédez toohello [portail Azure](https://portal.azure.com) toosee vous avez créé l’application web hello. 



Dans le menu de gauche hello, cliquez sur **du Service d’applications**, puis cliquez sur nom hello de votre application web Azure.

![Application de navigation du portail tooAzure web](./media/app-service-web-tutorial-dotnet-sqldatabase/access-portal.png)

Vous accédez à la page de votre application web. 

Par défaut, le portail de hello affiche hello **vue d’ensemble** page. Cette page propose un aperçu de votre application. Ici, vous pouvez également effectuer des tâches de gestion de base (parcourir, arrêter, démarrer, redémarrer et supprimer des éléments, par exemple). onglets Hello sur le côté gauche de hello de page de hello affichent les pages de configuration différents hello que vous pouvez l’ouvrir. 

![Page App Service du Portail Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/web-app-blade.png)

[!INCLUDE [Clean up section](../../includes/clean-up-section-portal-web-app.md)]

<a name="next"></a>

## <a name="next-steps"></a>Étapes suivantes

Dans ce didacticiel, vous avez appris à :

> [!div class="checklist"]
> * Créer une base de données SQL dans Azure
> * Se connecter à un tooSQL d’application ASP.NET de base de données
> * Déployer hello application tooAzure
> * Mettre à jour le modèle de données hello et redéployer l’application hello
> * Journaux des flux de données à partir d’Azure tooyour Terminal Server
> * Gérer l’application hello Bonjour portail Azure

Avancer toolearn de didacticiel suivant toohello toohello l’application web de noms toomap DNS personnalisé.

> [!div class="nextstepaction"]
> [Mapper une tooAzure de nom DNS personnalisé existant Web Apps](app-service-web-tutorial-custom-domain.md)
