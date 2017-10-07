---
title: "démarré avec un exemple d’aaaGet"
description: "Power BI incorporé, utilisez tooadd du Kit de développement logiciel des rapports interactifs Power BI dans votre application business intelligence"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: d8a9ef78-ad4e-4bc7-9711-89172dc5c548
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/02/2017
ms.author: asaxton
ms.openlocfilehash: 1fef9dd8e0f734b748b930d3f85ad4b517d9661e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-power-bi-embedded-sample"></a>Prise en main de l’exemple Power BI Embedded

Avec **Microsoft Power BI Embedded**, vous pouvez intégrer des rapports Power BI dans vos applications web ou mobiles. Dans cet article, nous allons vous présenter toohello **Power BI Embedded** exemple démarrée de get.

Avant d’aller plus loin, vous souhaiterez probablement hello toosave suivant des ressources. Ils vous aiderons à lors de l’intégration des rapports Power BI trop dans l’exemple d’application hello et vos propres applications.

* [Exemple d’application web d’espace de travail](http://go.microsoft.com/fwlink/?LinkId=761493)
* [Référence de l’API Power BI Embedded](https://msdn.microsoft.com/en-US/library/azure/mt711507.aspx)
* [Kit de développement logiciel (SDK) .NET Power BI Embedded ](http://go.microsoft.com/fwlink/?LinkId=746472) (disponible par le biais de NuGet)
* [Exemple de rapport JavaScript intégré](https://microsoft.github.io/PowerBI-JavaScript/demo)

> [!NOTE] 
> Avant que vous pouvez configurer et d’exécution hello obtenir Power BI Embedded a démarré l’exemple, vous devez toocreate au moins un **Collection de l’espace de travail** dans votre abonnement Azure. toolearn comment toocreate un **Collection de l’espace de travail** Bonjour portail Azure, consultez [prise en main de Power BI Embedded](power-bi-embedded-get-started.md).

## <a name="configure-hello-sample-app"></a>Configurer l’application d’exemple hello

Procédure pas à pas comment configurer votre application exemple Visual Studio development environnement tooaccess hello composants nécessaires toorun hello.

1. Téléchargez et décompressez hello [Power BI Embedded - intégrer un rapport à une application web](http://go.microsoft.com/fwlink/?LinkId=761493) exemples sur GitHub.
2. Ouvrez **PowerBI-embedded.sln** dans Visual Studio. Vous devrez peut-être tooexecute hello **Package de mise à jour** commande hello NuGET Package Manager Console dans les packages de hello tooupdate ordre utilisé dans cette solution.
3. Générez la solution de hello.
4. Exécutez hello **ProvisionSample** application console. Dans l’exemple hello d’application de console, vous configurez un espace de travail et importez un fichier PBIX.
5. tooprovision un nouveau **espace de travail**, sélectionnez l’option 1, **gestion de la Collection**, puis sélectionnez l’option 6, **configurer un espace de travail**
6. tooimport un nouveau **rapport**, sélectionnez l’option 2, **gestion de rapports**, puis sélectionnez l’option 3, **fichier d’importation PBIX bureau dans un espace de travail**.

7. Entrez le nom de votre **collection d’espaces de travail** et la **clé d’accès**. Vous pouvez obtenir ces Bonjour **Azure Portal**. toolearn plus sur la façon tooget votre **clé d’accès**, consultez [afficher les clés d’accès Power BI API](power-bi-embedded-get-started.md#view-power-bi-api-access-keys) dans prise en main Microsoft Power BI Embedded.

    ![](media/powerbi-embedded-get-started-sample/azure-portal.png)
8. Copiez et enregistrez hello nouvellement créé **ID de l’espace de travail** toouse plus loin dans cet article. Après avoir hello **ID de l’espace de travail** est créé, il peut s’avérer hello **Azure Portal**.

    ![](media/powerbi-embedded-get-started-sample/workspace-id.png)
9. tooimport un PBIX fichier dans votre **espace de travail**, sélectionnez l’option **6. Importez le fichier PBIX Desktop dans un espace de travail existant**. Si vous n’avez pas un PBIX pratique de fichiers, vous pouvez télécharger hello [PBIX d’exemple Retail Analysis](http://go.microsoft.com/fwlink/?LinkID=780547).
10. Si vous y êtes invité, entrez un nom convivial pour votre **jeu de données**.

La réponse doit ressembler à ceci :

```
Checking import state... Publishing
Checking import state... Succeeded
```

> [!NOTE]
> Si votre fichier PBIX contient toutes les connexions de requête directe, exécutez les chaînes de connexion hello tooupdate 7.

À ce stade, vous avez un rapport PBIX Power BI qui a été importé dans votre **espace de travail**. À présent, voyons comment toorun hello **Power BI Embedded** obtenir démarrée exemple d’application web.

## <a name="run-hello-sample-web-app"></a>Exécuter l’exemple hello d’application web
exemple d’application web Hello est un exemple d’application qui affiche les rapports importés dans votre **espace de travail**. Voici comment tooconfigure hello exemple d’application web.

1. Bonjour **incorporées PowerBI** solution Visual Studio, à droite cliquez sur hello **EmbedSample** application web, puis choisissez **définir comme projet de démarrage**.
2. Dans **web.config**, Bonjour **EmbedSample** application web, modifiez hello **appSettings**: **AccessKey**, ** WorkspaceCollection** nom, et **Id_espace_de_travail**.

    ```
    <appSettings>
        <add key="powerbi:AccessKey" value="" />
        <add key="powerbi:ApiUrl" value="https://api.powerbi.com" />
        <add key="powerbi:WorkspaceCollection" value="" />
        <add key="powerbi:WorkspaceId" value="" />
    </appSettings>
    ```
3. Exécutez hello **EmbedSample** application web.

Une fois que vous exécutez hello **EmbedSample** application web, le volet de navigation gauche hello doit contenir un **rapports** menu. rapport de hello tooview vous avez importé, développez **rapports**, puis cliquez sur un rapport. Si vous avez importé hello [PBIX d’exemple Retail Analysis](http://go.microsoft.com/fwlink/?LinkID=780547), hello exemple d’application web ressemble à ceci :

![](media/powerbi-embedded-get-started-sample/power-bi-embedded-sample-left-nav.png)

Après avoir cliqué sur un rapport, hello **EmbedSample** application web doit ressembler cela :

![](media/powerbi-embedded-get-started-sample/sample-web-app.png)

## <a name="explore-hello-sample-code"></a>Explorer l’exemple de code hello

Hello **Microsoft Power BI Embedded** exemple est un exemple d’application web qui vous montre comment toointegrate **Power BI** rapports dans votre application. Il utilise un Model-View-Controller (MVC) toodemonstrate meilleures pratiques du modèle de conception. Cette section met en évidence les parties de l’exemple de code hello que vous pouvez Explorer dans hello **Power BI incorporé** solution d’application web. Hello modèle Model-View-Controller (MVC) sépare la modélisation de domaine de hello, hello présentation et les actions de hello en fonction de l’entrée d’utilisateur en trois classes distinctes hello : modèle, vue et le contrôle. toolearn en savoir plus sur MVC, consultez [en savoir plus sur ASP.NET](http://www.asp.net/mvc).

Hello **Microsoft Power BI Embedded** exemple de code est séparé comme suit. Chaque section inclut le nom de fichier hello Bonjour Power BI-embedded.sln solution afin que vous pouvez rechercher facilement les code hello dans l’exemple hello.

> [!NOTE]
> Cette section est un résumé de l’exemple de code hello qui montre comment le code de hello a été écrit. hello tooview complète exemple, Veuillez charger hello Power BI-embedded.sln la solution dans Visual Studio.

### <a name="model"></a>Modèle

exemple Hello a un **ReportsViewModel** et **ReportViewModel**.

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

chaîne de connexion Hello doit être Bonjour suivant le format :

```
Data Source=tcp:MyServer.database.windows.net,1433;Initial Catalog=MyDatabase
```

L’utilisation d’attributs de serveur et de base de données communs échoue. Par exemple : Server=tcp:MyServer.database.windows.net,1433;Database=MyDatabase,

### <a name="view"></a>Affichage

Hello **vue** gère affichage hello de Power BI **rapports** et un Power BI **rapport**.

**Reports.cshtml**: itérer sur **Model.Reports** toocreate un **ActionLink**. Hello **ActionLink** est composé comme suit :

| Partie | Description |
| --- | --- |
| Intitulé |Nom du rapport de hello. |
| QueryString |Un lien de toohello ID d’état. |

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

Report.cshtml : Définir hello **Model.AccessToken**, et hello expression Lambda pour **PowerBIReportFor**.

    @model ReportViewModel

    ...

    <div class="side-body padding-top">
        @Html.PowerBIAccessToken(Model.AccessToken)
        @Html.PowerBIReportFor(m => m.Report, new { style = "height:85vh" })
    </div>

### <a name="controller"></a>Controller

**DashboardController.cs** : crée un PowerBIClient qui transmet un **jeton d’application**. Un jeton de Web JSON (JWT) est généré à partir de hello **clé de signature** tooget hello **informations d’identification**. Hello **informations d’identification** est toocreate utilisé une instance de **PowerBIClient**. Une fois que vous avez une instance de **PowerBIClient**, vous pouvez appeler GetReports() et GetReportsAsync().

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

Une fois que vous avez un **rapport**, vous utilisez un **IFrame** tooembed hello Power BI **rapport**. Voici un extrait de code à partir de powerbi.js Bonjour **Microsoft Power BI Embedded** exemple.

![](media/powerbi-embedded-get-started-sample/power-bi-embedded-iframe-code.png)

## <a name="filter-reports-embedded-in-your-application"></a>Filtrer les rapports incorporés dans votre application

Vous pouvez filtrer un rapport incorporé à l’aide d’une syntaxe d’URL. toodo, vous ajoutez un **$filter** interroger le paramètre de chaîne avec un **eq** opérateur tooyour l’url src iFrame avec filtre hello spécifié. Voici la syntaxe de requête de filtre hello :

```
https://app.powerbi.com/reportEmbed
?reportId=d2a0ea38-...-9673-ee9655d54a4a&
$filter={tableName/fieldName}%20eq%20'{fieldValue}'
```

> [!NOTE]
> {tableName/fieldName} ne peut pas contenir d’espaces ou de caractères spéciaux. Bonjour {fieldValue} accepte une seule valeur par catégorie.  

## <a name="see-also"></a>Voir aussi

[Scénarios Microsoft Power BI Embedded courants](power-bi-embedded-scenarios.md)  
[Authentification et autorisation dans Power BI Embedded](power-bi-embedded-app-token-flow.md)  
[Incorporer un rapport](power-bi-embedded-embed-report.md)  
[Créer un rapport à partir d’un jeu de données](power-bi-embedded-create-report-from-dataset.md)  
[Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[Exemple d’incorporation JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
Des questions ? [Essayez de hello Communauté Power BI](http://community.powerbi.com/)
