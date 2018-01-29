---
title: "Prise en main d’un exemple"
description: "Dans cet article, nous allons vous présenter l’exemple de prise en main relatif aux collections d’espaces de travail Power BI."
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ROBOTS: NOINDEX
ms.assetid: d8a9ef78-ad4e-4bc7-9711-89172dc5c548
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 09/25/2017
ms.author: asaxton
ms.openlocfilehash: 9049f95c9f81c0217c96469a45561b6cd0b33ae9
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2017
---
# <a name="get-started-with-power-bi-workspace-collections-sample"></a>Exemple de prise en main des collections d’espaces de travail Power BI

Les **collections d’espaces de travail Microsoft Power BI** vous permettent d’intégrer des rapports Power BI dans vos applications web ou mobiles. Dans cet article, nous allons vous présenter l’exemple de prise en main relatif aux **collections d’espaces de travail Power BI**.

> [!IMPORTANT]
> Les collections d’espaces de travail Power BI sont déconseillées et disponibles jusqu’en juin 2018 ou jusqu’à la date indiquée sur votre contrat. Nous vous conseillons de planifier votre migration vers Power BI Embedded pour éviter toute interruption dans votre application. Pour plus d’informations sur la migration de vos données vers Power BI Embedded, consultez l’article [How to migrate Power BI Workspace Collections content to Power BI Embedded (Migration du contenu de collections d’espaces de travail Power BI vers Power BI Embedded)](https://powerbi.microsoft.com/documentation/powerbi-developer-migrate-from-powerbi-embedded/).

Avant d’aller plus loin, vous devez enregistrer les ressources ci-après, qui vous aideront lors de l’intégration de rapports Power BI dans l’exemple d’application, ainsi que dans vos propres applications.

* [Exemple d’application web d’espace de travail](http://go.microsoft.com/fwlink/?LinkId=761493)
* [Informations de référence sur les API des collections d’espaces de travail Power BI](https://msdn.microsoft.com/library/azure/mt711507.aspx)
* [Kit de développement logiciel (SDK) .NET Power BI](http://go.microsoft.com/fwlink/?LinkId=746472) (disponible par le biais de NuGet)
* [Exemple de rapport JavaScript intégré](https://microsoft.github.io/PowerBI-JavaScript/demo)

> [!NOTE]
> Avant de configurer et d’exécuter l’exemple de prise en main des collections d’espaces de travail Power BI, vous devez créer au moins une **collection d’espaces de travail** dans votre abonnement Azure. Pour plus d’informations sur la création d’une **collection d’espaces de travail** dans le portail Azure, consultez l’article [Prendre en main les collections d’espaces de travail Power BI](get-started.md).

## <a name="configure-the-sample-app"></a>Configurer l’exemple d’application

Passons à la configuration de votre environnement de développement Visual Studio pour accéder aux composants nécessaires à l’exécution de l’exemple d’application.

1. Téléchargez et décompressez l’exemple [Power BI Workspace Collections - Integrate a report into a web app](http://go.microsoft.com/fwlink/?LinkId=761493) (Collections d’espaces de travail Power BI - Intégrer un rapport dans une application web) sur GitHub.
2. Ouvrez **PowerBI-embedded.sln** dans Visual Studio. Vous devrez peut-être exécuter la commande **Update-Package** dans la console du gestionnaire de package NuGet pour mettre à jour les packages utilisés dans cette solution.
3. Générez la solution.
4. Exécutez l’application de console **ProvisionSample** . Dans l’exemple d’application console, vous allez approvisionner un espace de travail et importer un fichier PBIX.
5. Pour approvisionner un nouvel **espace de travail**, sélectionnez l’option 1, **Collection management** (Gestion des collections), puis choisissez l’option 6, **Provision a new Workspace** (Approvisionner un nouvel espace de travail).
6. Pour importer un nouveau **rapport**, sélectionnez l’option 2, **Report management** (Gestion de rapport), puis sélectionnez l’option 3, **Import PBIX Desktop file into a workspace** (Importer le fichier PBIX Desktop dans un espace de travail).

7. Entrez le nom de votre **collection d’espaces de travail** et la **clé d’accès**. Vous pouvez obtenir ces informations dans le **portail Azure**. Pour en savoir plus sur la façon d’obtenir votre **clé d’accès**, consultez [Affichage des touches d’accès rapide aux API de Power BI](get-started.md#view-power-bi-api-access-keys) dans Prise en main de Microsoft Power BI Embedded.

    ![Clés d’accès dans le portail Azure](media/get-started-sample/azure-portal.png)
8. Copiez et enregistrez **l’ID d’espace de travail** qui vient d’être créé et qui sera utilisé ultérieurement dans cet article. Une fois **l’ID d’espace de travail** créé, ce dernier est disponible dans le **portail Azure**.

    ![ID d’espace de travail dans le portail Azure](media/get-started-sample/workspace-id.png)
9. Pour importer un fichier PBIX dans votre **espace de travail**, sélectionnez l’option **6. Importez le fichier PBIX Desktop dans un espace de travail existant**. Si vous n’avez pas de fichier PBIX sous la main, téléchargez [l’exemple PBIX Analyse des données de vente](http://go.microsoft.com/fwlink/?LinkID=780547).
10. Si vous y êtes invité, entrez un nom convivial pour votre **jeu de données**.

La réponse doit ressembler à ceci :

```
Checking import state... Publishing
Checking import state... Succeeded
```

> [!NOTE]
> Si votre fichier PBIX contient des connexions de requête directe, exécutez l’option 7 pour mettre à jour les chaînes de connexion.

À ce stade, vous avez un rapport PBIX Power BI qui a été importé dans votre **espace de travail**. Voyons maintenant comment exécuter l’exemple d’application web de prise en main des **collections d’espaces de travail Power BI**.

## <a name="run-the-sample-web-app"></a>Exécuter l’exemple d’application web

L’exemple d’application web est un exemple d’application qui restitue les rapports importés dans votre **espace de travail**. Voici comment configurer l’exemple d’application web.

1. Dans la solution Visual Studio **PowerBI-embedded**, cliquez avec le bouton droit sur l’application web **EmbedSample**, puis choisissez **Définir comme projet de démarrage**.
2. Dans **web.config**, dans l’application web **EmbedSample**, modifiez la section **appSettings** : **AccessKey**, le nom **WorkspaceCollection** et **WorkspaceId**.

    ```
    <appSettings>
        <add key="powerbi:AccessKey" value="" />
        <add key="powerbi:ApiUrl" value="https://api.powerbi.com" />
        <add key="powerbi:WorkspaceCollection" value="" />
        <add key="powerbi:WorkspaceId" value="" />
    </appSettings>
    ```
3. Exécutez l’application web **EmbedSample**.

Une fois que vous avez exécuté l’application web **EmbedSample**, le volet de navigation gauche doit contenir un menu **Rapports**. Pour afficher le rapport que vous avez importé, développez **Rapports**, puis cliquez sur un rapport. Si vous avez importé l’[exemple PBIX Analyse des données de vente](http://go.microsoft.com/fwlink/?LinkID=780547), l’exemple d’application web a l’aspect suivant :

![Exemple de barre de navigation de gauche dans l’exemple d’application](media/get-started-sample/sample-left-nav.png)

Une fois que vous avez cliqué sur un rapport, l’application web **EmbedSample** doit avoir l’aspect suivant :

![Exemple d’affichage de rapport dans l’application](media/get-started-sample/sample-web-app.png)

## <a name="explore-the-sample-code"></a>Explorer l’exemple de code

L’exemple de **collections d’espaces de travail Microsoft Power BI** est un exemple d’application web qui vous indique comment intégrer des rapports **Power BI** dans votre application. Il utilise un modèle de conception MVC (Model-View-Controller) pour illustrer les meilleures pratiques. Cette section met en évidence les parties de l’exemple de code que vous pouvez explorer dans la solution d’application web **PowerBI-embedded**. Le modèle MVC (Model-View-Controller) sépare la modélisation du domaine, la présentation et les actions basées sur les entrées des utilisateurs en trois classes distinctes : modèle, affichage et contrôle. Pour plus d’informations sur MVC, consultez [En savoir plus sur ASP.NET](http://www.asp.net/mvc).

L’exemple de code relatif aux **collections d’espaces de travail Microsoft Power BI** inclut les sections suivantes. Chacune d’elles inclut le nom de fichier dans la solution PowerBI-embedded.sln afin que vous puissiez facilement trouver le code dans l’exemple.

> [!NOTE]
> Cette section est un résumé de l’exemple de code qui montre comment le code a été écrit. Pour afficher l’exemple complet, chargez la solution PowerBI-embedded.sln dans Visual Studio.

### <a name="model"></a>Modèle

L’exemple inclut deux modèles : **ReportsViewModel** et **ReportViewModel**.

**ReportsViewModel.cs** : représente les rapports Power BI.

    public class ReportsViewModel
    {
        public List<Report> Reports { get; set; }
    }

**ReportViewModel.cs** : représente un rapport Power BI.

    public classReportViewModel
    {
        public IReport Report { get; set; }

        public string AccessToken { get; set; }
    }

### <a name="connection-string"></a>Chaîne de connexion

La chaîne de connexion doit avoir le format suivant :

```
Data Source=tcp:MyServer.database.windows.net,1433;Initial Catalog=MyDatabase
```

L’utilisation d’attributs de serveur et de base de données communs échoue. Par exemple : Server=tcp:MyServer.database.windows.net,1433;Database=MyDatabase,

### <a name="view"></a>Affichage

L’**affichage** gère la présentation des **rapports** Power BI et d’un **rapport** Power BI.

**Reports.cshtml** : effectue une itération sur **Model.Reports** pour créer un **ActionLink**. **ActionLink** est composé comme suit :

| Partie | Description |
| --- | --- |
| Intitulé |Nom du rapport. |
| QueryString |Lien vers l’ID de rapport. |

    <div id="reports-nav" class="panel-collapse collapse">
        <div class="panel-body">
            <ul class="nav navbar-nav">
                @foreach (var report in Model.Reports)
                {
                    var reportClass = Request.QueryString["reportId"] == report.Id ? "active" : "";
                    <li class="@reportClass">
                        @Html.ActionLink(report.Name, "Report", new { reportId = report.Id })
                    </li>
                }
            </ul>
        </div>
    </div>

Report.cshtml : définit **Model.AccessToken** et l’expression lambda pour **PowerBIReportFor**.

    @model ReportViewModel

    ...

    <div class="side-body padding-top">
        @Html.PowerBIAccessToken(Model.AccessToken)
        @Html.PowerBIReportFor(m => m.Report, new { style = "height:85vh" })
    </div>

### <a name="controller"></a>Controller

**DashboardController.cs** : crée un PowerBIClient qui transmet un **jeton d’application**. Un jeton JWT (JSON Web Token) est généré à partir de la **clé de signature** pour obtenir les **informations d’identification**. Les **informations d’identification** sont utilisées pour créer une instance de **PowerBIClient**. Une fois que vous avez une instance de **PowerBIClient**, vous pouvez appeler GetReports() et GetReportsAsync().

CreatePowerBIClient()

    private IPowerBIClient CreatePowerBIClient()
    {
        var credentials = new TokenCredentials(accessKey, "AppKey");
        var client = new PowerBIClient(credentials)
        {
            BaseUri = new Uri(apiUrl)
        };

        return client;
    }

ActionResult Reports()

    public ActionResult Reports()
    {
        using (var client = this.CreatePowerBIClient())
        {
            var reportsResponse = client.Reports.GetReports(this.workspaceCollection, this.workspaceId);

            var viewModel = new ReportsViewModel
            {
                Reports = reportsResponse.Value.ToList()
            };

            return PartialView(viewModel);
        }
    }


Task<ActionResult> Report(string reportId)

    public async Task<ActionResult> Report(string reportId)
    {
        using (var client = this.CreatePowerBIClient())
        {
            var reportsResponse = await client.Reports.GetReportsAsync(this.workspaceCollection, this.workspaceId);
            var report = reportsResponse.Value.FirstOrDefault(r => r.Id == reportId);
            var embedToken = PowerBIToken.CreateReportEmbedToken(this.workspaceCollection, this.workspaceId, report.Id);

            var viewModel = new ReportViewModel
            {
                Report = report,
                AccessToken = embedToken.Generate(this.accessKey)
            };

            return View(viewModel);
        }
    }

### <a name="integrate-a-report-into-your-app"></a>Intégrer un rapport dans votre application

Une fois que vous avez un **rapport**, utilisez un **iframe** pour incorporer le **rapport** Power BI. Voici un extrait de code powerbi.js dans l’exemple de **collections d’espaces de travail Microsoft Power BI**.

```
init: function() {
    var embedUrl = this.getEmbedUrl();
    var iframeHtml = '<igrame style="width:100%;height:100%;" src="' + embedUrl + 
        '" scrolling="no" allowfullscreen="true"></iframe>';
    this.element.innerHTML = iframeHtml;
    this.iframe = this.element.childNodes[0];
    this.iframe.addEventListener('load', this.load.bind(this), false);
}
```

## <a name="filter-reports-embedded-in-your-application"></a>Filtrer les rapports incorporés dans votre application

Vous pouvez filtrer un rapport incorporé à l’aide d’une syntaxe d’URL. Pour ce faire, ajoutez un paramètre de chaîne de requête **$filter** avec un opérateur **eq** à l’URL src iframe avec le filtre spécifié. Voici la syntaxe de requête de filtre :

```
https://app.powerbi.com/reportEmbed
?reportId=d2a0ea38-...-9673-ee9655d54a4a&
$filter={tableName/fieldName}%20eq%20'{fieldValue}'
```

> [!NOTE]
> {tableName/fieldName} ne peut pas contenir d’espaces ou de caractères spéciaux. {fieldValue} accepte une seule valeur de catégorie.  

## <a name="see-also"></a>Voir aussi

[Scénarios courants pour les collections d’espaces de travail Microsoft Power BI](scenarios.md)  
[Authentification et autorisation dans les collections d’espaces de travail Power BI](app-token-flow.md)  
[Incorporer un rapport](embed-report.md)  
[Créer un rapport à partir d’un jeu de données](create-report-from-dataset.md)  
[Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[Exemple d’incorporation JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/)  

Des questions ? [Essayer la communauté Power BI](http://community.powerbi.com/)
