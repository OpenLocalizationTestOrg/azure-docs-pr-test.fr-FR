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
# <a name="get-started-with-power-bi-embedded-sample"></a><span data-ttu-id="a9e6c-103">Prise en main de l’exemple Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="a9e6c-103">Get started with Power BI Embedded sample</span></span>

<span data-ttu-id="a9e6c-104">Avec **Microsoft Power BI Embedded**, vous pouvez intégrer des rapports Power BI dans vos applications web ou mobiles.</span><span class="sxs-lookup"><span data-stu-id="a9e6c-104">With **Microsoft Power BI Embedded**, you can integrate Power BI reports right into your web or mobile applications.</span></span> <span data-ttu-id="a9e6c-105">Dans cet article, nous allons vous présenter toohello **Power BI Embedded** exemple démarrée de get.</span><span class="sxs-lookup"><span data-stu-id="a9e6c-105">In this article, we'll introduce you toohello **Power BI Embedded** get started sample.</span></span>

<span data-ttu-id="a9e6c-106">Avant d’aller plus loin, vous souhaiterez probablement hello toosave suivant des ressources.</span><span class="sxs-lookup"><span data-stu-id="a9e6c-106">Before we go any further, you'll probably want toosave hello following resources.</span></span> <span data-ttu-id="a9e6c-107">Ils vous aiderons à lors de l’intégration des rapports Power BI trop dans l’exemple d’application hello et vos propres applications.</span><span class="sxs-lookup"><span data-stu-id="a9e6c-107">They'll help you when integrating Power BI reports into hello sample app and your own apps too.</span></span>

* [<span data-ttu-id="a9e6c-108">Exemple d’application web d’espace de travail</span><span class="sxs-lookup"><span data-stu-id="a9e6c-108">Sample workspace web app</span></span>](http://go.microsoft.com/fwlink/?LinkId=761493)
* [<span data-ttu-id="a9e6c-109">Référence de l’API Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="a9e6c-109">Power BI Embedded API reference</span></span>](https://msdn.microsoft.com/en-US/library/azure/mt711507.aspx)
* <span data-ttu-id="a9e6c-110">[Kit de développement logiciel (SDK) .NET Power BI Embedded ](http://go.microsoft.com/fwlink/?LinkId=746472) (disponible par le biais de NuGet)</span><span class="sxs-lookup"><span data-stu-id="a9e6c-110">[Power BI Embedded .NET SDK ](http://go.microsoft.com/fwlink/?LinkId=746472) (available via NuGet)</span></span>
* [<span data-ttu-id="a9e6c-111">Exemple de rapport JavaScript intégré</span><span class="sxs-lookup"><span data-stu-id="a9e6c-111">JavaScript Report Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo)

> [!NOTE] 
> <span data-ttu-id="a9e6c-112">Avant que vous pouvez configurer et d’exécution hello obtenir Power BI Embedded a démarré l’exemple, vous devez toocreate au moins un **Collection de l’espace de travail** dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="a9e6c-112">Before you can configure and run hello Power BI Embedded get started sample, you need toocreate at least one **Workspace Collection** in your Azure subscription.</span></span> <span data-ttu-id="a9e6c-113">toolearn comment toocreate un **Collection de l’espace de travail** Bonjour portail Azure, consultez [prise en main de Power BI Embedded](power-bi-embedded-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="a9e6c-113">toolearn how toocreate a **Workspace Collection** in hello Azure Portal see [Getting Started with Power BI Embedded](power-bi-embedded-get-started.md).</span></span>

## <a name="configure-hello-sample-app"></a><span data-ttu-id="a9e6c-114">Configurer l’application d’exemple hello</span><span class="sxs-lookup"><span data-stu-id="a9e6c-114">Configure hello sample app</span></span>

<span data-ttu-id="a9e6c-115">Procédure pas à pas comment configurer votre application exemple Visual Studio development environnement tooaccess hello composants nécessaires toorun hello.</span><span class="sxs-lookup"><span data-stu-id="a9e6c-115">Let's walk through setting up your Visual Studio development environment tooaccess hello  components needed toorun hello sample app.</span></span>

1. <span data-ttu-id="a9e6c-116">Téléchargez et décompressez hello [Power BI Embedded - intégrer un rapport à une application web](http://go.microsoft.com/fwlink/?LinkId=761493) exemples sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="a9e6c-116">Download and unzip hello [Power BI Embedded - Integrate a report into a web app](http://go.microsoft.com/fwlink/?LinkId=761493) sample on GitHub.</span></span>
2. <span data-ttu-id="a9e6c-117">Ouvrez **PowerBI-embedded.sln** dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a9e6c-117">Open **PowerBI-embedded.sln** in Visual Studio.</span></span> <span data-ttu-id="a9e6c-118">Vous devrez peut-être tooexecute hello **Package de mise à jour** commande hello NuGET Package Manager Console dans les packages de hello tooupdate ordre utilisé dans cette solution.</span><span class="sxs-lookup"><span data-stu-id="a9e6c-118">You may need tooexecute hello **Update-Package** command in hello NuGET Package Manager Console in order tooupdate hello packages used in this solution.</span></span>
3. <span data-ttu-id="a9e6c-119">Générez la solution de hello.</span><span class="sxs-lookup"><span data-stu-id="a9e6c-119">Build hello solution.</span></span>
4. <span data-ttu-id="a9e6c-120">Exécutez hello **ProvisionSample** application console.</span><span class="sxs-lookup"><span data-stu-id="a9e6c-120">Run hello **ProvisionSample** console app.</span></span> <span data-ttu-id="a9e6c-121">Dans l’exemple hello d’application de console, vous configurez un espace de travail et importez un fichier PBIX.</span><span class="sxs-lookup"><span data-stu-id="a9e6c-121">In hello sample console app, you provision a workspace and import a PBIX file.</span></span>
5. <span data-ttu-id="a9e6c-122">tooprovision un nouveau **espace de travail**, sélectionnez l’option 1, **gestion de la Collection**, puis sélectionnez l’option 6, **configurer un espace de travail**</span><span class="sxs-lookup"><span data-stu-id="a9e6c-122">tooprovision a new **Workspace**, select option 1, **Collection management**, and then select option 6, **Provision a new Workspace**</span></span>
6. <span data-ttu-id="a9e6c-123">tooimport un nouveau **rapport**, sélectionnez l’option 2, **gestion de rapports**, puis sélectionnez l’option 3, **fichier d’importation PBIX bureau dans un espace de travail**.</span><span class="sxs-lookup"><span data-stu-id="a9e6c-123">tooimport a new **Report**, select option 2, **Report management**, and then select option 3, **Import PBIX Desktop file into a workspace**.</span></span>

7. <span data-ttu-id="a9e6c-124">Entrez le nom de votre **collection d’espaces de travail** et la **clé d’accès**.</span><span class="sxs-lookup"><span data-stu-id="a9e6c-124">Enter your **Workspace Collection** name, and **Access Key**.</span></span> <span data-ttu-id="a9e6c-125">Vous pouvez obtenir ces Bonjour **Azure Portal**.</span><span class="sxs-lookup"><span data-stu-id="a9e6c-125">You can get these in hello **Azure Portal**.</span></span> <span data-ttu-id="a9e6c-126">toolearn plus sur la façon tooget votre **clé d’accès**, consultez [afficher les clés d’accès Power BI API](power-bi-embedded-get-started.md#view-power-bi-api-access-keys) dans prise en main Microsoft Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="a9e6c-126">toolearn more about how tooget your **Access Key**, see [View Power BI API Access Keys](power-bi-embedded-get-started.md#view-power-bi-api-access-keys) in Get started with Microsoft Power BI Embedded.</span></span>

    ![](media/powerbi-embedded-get-started-sample/azure-portal.png)
8. <span data-ttu-id="a9e6c-127">Copiez et enregistrez hello nouvellement créé **ID de l’espace de travail** toouse plus loin dans cet article.</span><span class="sxs-lookup"><span data-stu-id="a9e6c-127">Copy and save hello newly created **Workspace ID** toouse later in this article.</span></span> <span data-ttu-id="a9e6c-128">Après avoir hello **ID de l’espace de travail** est créé, il peut s’avérer hello **Azure Portal**.</span><span class="sxs-lookup"><span data-stu-id="a9e6c-128">After hello **Workspace ID** is created, you can find it hello **Azure Portal**.</span></span>

    ![](media/powerbi-embedded-get-started-sample/workspace-id.png)
9. <span data-ttu-id="a9e6c-129">tooimport un PBIX fichier dans votre **espace de travail**, sélectionnez l’option **6. Importez le fichier PBIX Desktop dans un espace de travail existant**.</span><span class="sxs-lookup"><span data-stu-id="a9e6c-129">tooimport a PBIX file into your **Workspace**, select option **6. Import PBIX Desktop file into an existing workspace**.</span></span> <span data-ttu-id="a9e6c-130">Si vous n’avez pas un PBIX pratique de fichiers, vous pouvez télécharger hello [PBIX d’exemple Retail Analysis](http://go.microsoft.com/fwlink/?LinkID=780547).</span><span class="sxs-lookup"><span data-stu-id="a9e6c-130">If you don't have a PBIX file handy, you can download hello [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547).</span></span>
10. <span data-ttu-id="a9e6c-131">Si vous y êtes invité, entrez un nom convivial pour votre **jeu de données**.</span><span class="sxs-lookup"><span data-stu-id="a9e6c-131">If prompted, enter a friendly name for your **Dataset**.</span></span>

<span data-ttu-id="a9e6c-132">La réponse doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="a9e6c-132">You should see a response like:</span></span>

```
Checking import state... Publishing
Checking import state... Succeeded
```

> [!NOTE]
> <span data-ttu-id="a9e6c-133">Si votre fichier PBIX contient toutes les connexions de requête directe, exécutez les chaînes de connexion hello tooupdate 7.</span><span class="sxs-lookup"><span data-stu-id="a9e6c-133">If your PBIX file contains any direct query connections, run option 7 tooupdate hello connection strings.</span></span>

<span data-ttu-id="a9e6c-134">À ce stade, vous avez un rapport PBIX Power BI qui a été importé dans votre **espace de travail**.</span><span class="sxs-lookup"><span data-stu-id="a9e6c-134">At this point, you have a Power BI PBIX report imported into your **Workspace**.</span></span> <span data-ttu-id="a9e6c-135">À présent, voyons comment toorun hello **Power BI Embedded** obtenir démarrée exemple d’application web.</span><span class="sxs-lookup"><span data-stu-id="a9e6c-135">Now, let's look at how toorun hello **Power BI Embedded** get started sample web app.</span></span>

## <a name="run-hello-sample-web-app"></a><span data-ttu-id="a9e6c-136">Exécuter l’exemple hello d’application web</span><span class="sxs-lookup"><span data-stu-id="a9e6c-136">Run hello sample web app</span></span>
<span data-ttu-id="a9e6c-137">exemple d’application web Hello est un exemple d’application qui affiche les rapports importés dans votre **espace de travail**.</span><span class="sxs-lookup"><span data-stu-id="a9e6c-137">hello web app sample is a sample application that renders reports imported into your **Workspace**.</span></span> <span data-ttu-id="a9e6c-138">Voici comment tooconfigure hello exemple d’application web.</span><span class="sxs-lookup"><span data-stu-id="a9e6c-138">Here's how tooconfigure hello web app sample.</span></span>

1. <span data-ttu-id="a9e6c-139">Bonjour **incorporées PowerBI** solution Visual Studio, à droite cliquez sur hello **EmbedSample** application web, puis choisissez **définir comme projet de démarrage**.</span><span class="sxs-lookup"><span data-stu-id="a9e6c-139">In hello **PowerBI-embedded** Visual Studio solution, right click hello **EmbedSample** web application, and choose **Set as StartUp project**.</span></span>
2. <span data-ttu-id="a9e6c-140">Dans **web.config**, Bonjour **EmbedSample** application web, modifiez hello **appSettings**: **AccessKey**, ** WorkspaceCollection** nom, et **Id_espace_de_travail**.</span><span class="sxs-lookup"><span data-stu-id="a9e6c-140">In **web.config**, in hello **EmbedSample** web application, edit hello **appSettings**: **AccessKey**, **WorkspaceCollection** name, and **WorkspaceId**.</span></span>

    ```
    <appSettings>
        <add key="powerbi:AccessKey" value="" />
        <add key="powerbi:ApiUrl" value="https://api.powerbi.com" />
        <add key="powerbi:WorkspaceCollection" value="" />
        <add key="powerbi:WorkspaceId" value="" />
    </appSettings>
    ```
3. <span data-ttu-id="a9e6c-141">Exécutez hello **EmbedSample** application web.</span><span class="sxs-lookup"><span data-stu-id="a9e6c-141">Run hello **EmbedSample** web application.</span></span>

<span data-ttu-id="a9e6c-142">Une fois que vous exécutez hello **EmbedSample** application web, le volet de navigation gauche hello doit contenir un **rapports** menu.</span><span class="sxs-lookup"><span data-stu-id="a9e6c-142">Once you run hello **EmbedSample** web application, hello left navigation panel should contain a **Reports** menu.</span></span> <span data-ttu-id="a9e6c-143">rapport de hello tooview vous avez importé, développez **rapports**, puis cliquez sur un rapport.</span><span class="sxs-lookup"><span data-stu-id="a9e6c-143">tooview hello report you imported, expand **Reports**, and click a report.</span></span> <span data-ttu-id="a9e6c-144">Si vous avez importé hello [PBIX d’exemple Retail Analysis](http://go.microsoft.com/fwlink/?LinkID=780547), hello exemple d’application web ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="a9e6c-144">If you imported hello [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547), hello sample web app would look like this:</span></span>

![](media/powerbi-embedded-get-started-sample/power-bi-embedded-sample-left-nav.png)

<span data-ttu-id="a9e6c-145">Après avoir cliqué sur un rapport, hello **EmbedSample** application web doit ressembler cela :</span><span class="sxs-lookup"><span data-stu-id="a9e6c-145">After you click a report, hello **EmbedSample** web application should look something this:</span></span>

![](media/powerbi-embedded-get-started-sample/sample-web-app.png)

## <a name="explore-hello-sample-code"></a><span data-ttu-id="a9e6c-146">Explorer l’exemple de code hello</span><span class="sxs-lookup"><span data-stu-id="a9e6c-146">Explore hello sample code</span></span>

<span data-ttu-id="a9e6c-147">Hello **Microsoft Power BI Embedded** exemple est un exemple d’application web qui vous montre comment toointegrate **Power BI** rapports dans votre application.</span><span class="sxs-lookup"><span data-stu-id="a9e6c-147">hello **Microsoft Power BI Embedded** sample is an example web app that shows you how toointegrate **Power BI** reports into your app.</span></span> <span data-ttu-id="a9e6c-148">Il utilise un Model-View-Controller (MVC) toodemonstrate meilleures pratiques du modèle de conception.</span><span class="sxs-lookup"><span data-stu-id="a9e6c-148">It uses a Model-View-Controller (MVC) design pattern toodemonstrate best practices.</span></span> <span data-ttu-id="a9e6c-149">Cette section met en évidence les parties de l’exemple de code hello que vous pouvez Explorer dans hello **Power BI incorporé** solution d’application web.</span><span class="sxs-lookup"><span data-stu-id="a9e6c-149">This section highlights parts of hello sample code that you can explore within hello **PowerBI-embedded** web app solution.</span></span> <span data-ttu-id="a9e6c-150">Hello modèle Model-View-Controller (MVC) sépare la modélisation de domaine de hello, hello présentation et les actions de hello en fonction de l’entrée d’utilisateur en trois classes distinctes hello : modèle, vue et le contrôle.</span><span class="sxs-lookup"><span data-stu-id="a9e6c-150">hello Model-View-Controller (MVC) pattern separates hello modeling of hello domain, hello presentation, and hello actions based on user input into three separate classes: Model, View, and Control.</span></span> <span data-ttu-id="a9e6c-151">toolearn en savoir plus sur MVC, consultez [en savoir plus sur ASP.NET](http://www.asp.net/mvc).</span><span class="sxs-lookup"><span data-stu-id="a9e6c-151">toolearn more about MVC, see [Learn About ASP.NET](http://www.asp.net/mvc).</span></span>

<span data-ttu-id="a9e6c-152">Hello **Microsoft Power BI Embedded** exemple de code est séparé comme suit.</span><span class="sxs-lookup"><span data-stu-id="a9e6c-152">hello **Microsoft Power BI Embedded** sample code is separated as follows.</span></span> <span data-ttu-id="a9e6c-153">Chaque section inclut le nom de fichier hello Bonjour Power BI-embedded.sln solution afin que vous pouvez rechercher facilement les code hello dans l’exemple hello.</span><span class="sxs-lookup"><span data-stu-id="a9e6c-153">Each section includes hello file name in hello PowerBI-embedded.sln solution so that you can easily find hello code in hello sample.</span></span>

> [!NOTE]
> <span data-ttu-id="a9e6c-154">Cette section est un résumé de l’exemple de code hello qui montre comment le code de hello a été écrit.</span><span class="sxs-lookup"><span data-stu-id="a9e6c-154">This section is a summary of hello sample code that shows how hello code was written.</span></span> <span data-ttu-id="a9e6c-155">hello tooview complète exemple, Veuillez charger hello Power BI-embedded.sln la solution dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a9e6c-155">tooview hello complete sample, please load hello PowerBI-embedded.sln solution in Visual Studio.</span></span>

### <a name="model"></a><span data-ttu-id="a9e6c-156">Modèle</span><span class="sxs-lookup"><span data-stu-id="a9e6c-156">Model</span></span>

<span data-ttu-id="a9e6c-157">exemple Hello a un **ReportsViewModel** et **ReportViewModel**.</span><span class="sxs-lookup"><span data-stu-id="a9e6c-157">hello sample has a **ReportsViewModel** and **ReportViewModel**.</span></span>

<span data-ttu-id="a9e6c-158">**ReportsViewModel.cs** : représente les rapports Power BI.</span><span class="sxs-lookup"><span data-stu-id="a9e6c-158">**ReportsViewModel.cs**: Represents Power BI Reports.</span></span>

    public class ReportsViewModel
    {
        public List<Report> Reports { get; set; }
    }

<span data-ttu-id="a9e6c-159">**ReportViewModel.cs** : représente un rapport Power BI.</span><span class="sxs-lookup"><span data-stu-id="a9e6c-159">**ReportViewModel.cs**: Represents a Power BI Report.</span></span>

    public classReportViewModel
    {
        public IReport Report { get; set; }

        public string AccessToken { get; set; }
    }

### <a name="connection-string"></a><span data-ttu-id="a9e6c-160">Chaîne de connexion</span><span class="sxs-lookup"><span data-stu-id="a9e6c-160">Connection string</span></span>

<span data-ttu-id="a9e6c-161">chaîne de connexion Hello doit être Bonjour suivant le format :</span><span class="sxs-lookup"><span data-stu-id="a9e6c-161">hello connection string must be in hello following format:</span></span>

```
Data Source=tcp:MyServer.database.windows.net,1433;Initial Catalog=MyDatabase
```

<span data-ttu-id="a9e6c-162">L’utilisation d’attributs de serveur et de base de données communs échoue.</span><span class="sxs-lookup"><span data-stu-id="a9e6c-162">Using common server and database attributes will fail.</span></span> <span data-ttu-id="a9e6c-163">Par exemple : Server=tcp:MyServer.database.windows.net,1433;Database=MyDatabase,</span><span class="sxs-lookup"><span data-stu-id="a9e6c-163">For example: Server=tcp:MyServer.database.windows.net,1433;Database=MyDatabase,</span></span>

### <a name="view"></a><span data-ttu-id="a9e6c-164">Affichage</span><span class="sxs-lookup"><span data-stu-id="a9e6c-164">View</span></span>

<span data-ttu-id="a9e6c-165">Hello **vue** gère affichage hello de Power BI **rapports** et un Power BI **rapport**.</span><span class="sxs-lookup"><span data-stu-id="a9e6c-165">hello **View** manages hello display of Power BI **Reports** and a Power BI **Report**.</span></span>

<span data-ttu-id="a9e6c-166">**Reports.cshtml**: itérer sur **Model.Reports** toocreate un **ActionLink**.</span><span class="sxs-lookup"><span data-stu-id="a9e6c-166">**Reports.cshtml**: Iterate over **Model.Reports** toocreate an **ActionLink**.</span></span> <span data-ttu-id="a9e6c-167">Hello **ActionLink** est composé comme suit :</span><span class="sxs-lookup"><span data-stu-id="a9e6c-167">hello **ActionLink** is composed as follows:</span></span>

| <span data-ttu-id="a9e6c-168">Partie</span><span class="sxs-lookup"><span data-stu-id="a9e6c-168">Part</span></span> | <span data-ttu-id="a9e6c-169">Description</span><span class="sxs-lookup"><span data-stu-id="a9e6c-169">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a9e6c-170">Intitulé</span><span class="sxs-lookup"><span data-stu-id="a9e6c-170">Title</span></span> |<span data-ttu-id="a9e6c-171">Nom du rapport de hello.</span><span class="sxs-lookup"><span data-stu-id="a9e6c-171">Name of hello Report.</span></span> |
| <span data-ttu-id="a9e6c-172">QueryString</span><span class="sxs-lookup"><span data-stu-id="a9e6c-172">QueryString</span></span> |<span data-ttu-id="a9e6c-173">Un lien de toohello ID d’état.</span><span class="sxs-lookup"><span data-stu-id="a9e6c-173">A link toohello Report ID.</span></span> |

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

<span data-ttu-id="a9e6c-174">Report.cshtml : Définir hello **Model.AccessToken**, et hello expression Lambda pour **PowerBIReportFor**.</span><span class="sxs-lookup"><span data-stu-id="a9e6c-174">Report.cshtml: Set hello **Model.AccessToken**, and hello Lambda expression for **PowerBIReportFor**.</span></span>

    @model ReportViewModel

    ...

    <div class="side-body padding-top">
        @Html.PowerBIAccessToken(Model.AccessToken)
        @Html.PowerBIReportFor(m => m.Report, new { style = "height:85vh" })
    </div>

### <a name="controller"></a><span data-ttu-id="a9e6c-175">Controller</span><span class="sxs-lookup"><span data-stu-id="a9e6c-175">Controller</span></span>

<span data-ttu-id="a9e6c-176">**DashboardController.cs** : crée un PowerBIClient qui transmet un **jeton d’application**.</span><span class="sxs-lookup"><span data-stu-id="a9e6c-176">**DashboardController.cs**: Creates a PowerBIClient passing an **app token**.</span></span> <span data-ttu-id="a9e6c-177">Un jeton de Web JSON (JWT) est généré à partir de hello **clé de signature** tooget hello **informations d’identification**.</span><span class="sxs-lookup"><span data-stu-id="a9e6c-177">A JSON Web Token (JWT) is generated from hello **Signing Key** tooget hello **Credentials**.</span></span> <span data-ttu-id="a9e6c-178">Hello **informations d’identification** est toocreate utilisé une instance de **PowerBIClient**.</span><span class="sxs-lookup"><span data-stu-id="a9e6c-178">hello **Credentials** are used toocreate an instance of **PowerBIClient**.</span></span> <span data-ttu-id="a9e6c-179">Une fois que vous avez une instance de **PowerBIClient**, vous pouvez appeler GetReports() et GetReportsAsync().</span><span class="sxs-lookup"><span data-stu-id="a9e6c-179">Once you have an instance of **PowerBIClient**, you can call GetReports() and GetReportsAsync().</span></span>

<span data-ttu-id="a9e6c-180">CreatePowerBIClient()</span><span class="sxs-lookup"><span data-stu-id="a9e6c-180">CreatePowerBIClient()</span></span>

    private IPowerBIClient CreatePowerBIClient()
    {
        var credentials = new TokenCredentials(accessKey, "AppKey");
        var client = new PowerBIClient(credentials)
        {
            BaseUri = new Uri(apiUrl)
        };

        return client;
    }

<span data-ttu-id="a9e6c-181">ActionResult Reports()</span><span class="sxs-lookup"><span data-stu-id="a9e6c-181">ActionResult Reports()</span></span>

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


<span data-ttu-id="a9e6c-182">Task<ActionResult> Report(string reportId)</span><span class="sxs-lookup"><span data-stu-id="a9e6c-182">Task<ActionResult> Report(string reportId)</span></span>

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

### <a name="integrate-a-report-into-your-app"></a><span data-ttu-id="a9e6c-183">Intégrer un rapport dans votre application</span><span class="sxs-lookup"><span data-stu-id="a9e6c-183">Integrate a report into your app</span></span>

<span data-ttu-id="a9e6c-184">Une fois que vous avez un **rapport**, vous utilisez un **IFrame** tooembed hello Power BI **rapport**.</span><span class="sxs-lookup"><span data-stu-id="a9e6c-184">Once you have a **Report**, you use an **IFrame** tooembed hello Power BI **Report**.</span></span> <span data-ttu-id="a9e6c-185">Voici un extrait de code à partir de powerbi.js Bonjour **Microsoft Power BI Embedded** exemple.</span><span class="sxs-lookup"><span data-stu-id="a9e6c-185">Here is a code snippet from  powerbi.js in hello **Microsoft Power BI Embedded** sample.</span></span>

![](media/powerbi-embedded-get-started-sample/power-bi-embedded-iframe-code.png)

## <a name="filter-reports-embedded-in-your-application"></a><span data-ttu-id="a9e6c-186">Filtrer les rapports incorporés dans votre application</span><span class="sxs-lookup"><span data-stu-id="a9e6c-186">Filter reports embedded in your application</span></span>

<span data-ttu-id="a9e6c-187">Vous pouvez filtrer un rapport incorporé à l’aide d’une syntaxe d’URL.</span><span class="sxs-lookup"><span data-stu-id="a9e6c-187">You can filter an embedded report using a URL syntax.</span></span> <span data-ttu-id="a9e6c-188">toodo, vous ajoutez un **$filter** interroger le paramètre de chaîne avec un **eq** opérateur tooyour l’url src iFrame avec filtre hello spécifié.</span><span class="sxs-lookup"><span data-stu-id="a9e6c-188">toodo this, you add a **$filter** query string parameter with an **eq** operator tooyour iFrame src url with hello filter specified.</span></span> <span data-ttu-id="a9e6c-189">Voici la syntaxe de requête de filtre hello :</span><span class="sxs-lookup"><span data-stu-id="a9e6c-189">Here is hello filter query syntax:</span></span>

```
https://app.powerbi.com/reportEmbed
?reportId=d2a0ea38-...-9673-ee9655d54a4a&
$filter={tableName/fieldName}%20eq%20'{fieldValue}'
```

> [!NOTE]
> <span data-ttu-id="a9e6c-190">{tableName/fieldName} ne peut pas contenir d’espaces ou de caractères spéciaux.</span><span class="sxs-lookup"><span data-stu-id="a9e6c-190">{tableName/fieldName} cannot include spaces or special characters.</span></span> <span data-ttu-id="a9e6c-191">Bonjour {fieldValue} accepte une seule valeur par catégorie.</span><span class="sxs-lookup"><span data-stu-id="a9e6c-191">hello {fieldValue} accepts a single categorical value.</span></span>  

## <a name="see-also"></a><span data-ttu-id="a9e6c-192">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="a9e6c-192">See also</span></span>

[<span data-ttu-id="a9e6c-193">Scénarios Microsoft Power BI Embedded courants</span><span class="sxs-lookup"><span data-stu-id="a9e6c-193">Common Microsoft Power BI Embedded scenarios</span></span>](power-bi-embedded-scenarios.md)  
[<span data-ttu-id="a9e6c-194">Authentification et autorisation dans Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="a9e6c-194">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="a9e6c-195">Incorporer un rapport</span><span class="sxs-lookup"><span data-stu-id="a9e6c-195">Embed a report</span></span>](power-bi-embedded-embed-report.md)  
[<span data-ttu-id="a9e6c-196">Créer un rapport à partir d’un jeu de données</span><span class="sxs-lookup"><span data-stu-id="a9e6c-196">Create a new report from a dataset</span></span>](power-bi-embedded-create-report-from-dataset.md)  
[<span data-ttu-id="a9e6c-197">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="a9e6c-197">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="a9e6c-198">Exemple d’incorporation JavaScript</span><span class="sxs-lookup"><span data-stu-id="a9e6c-198">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
<span data-ttu-id="a9e6c-199">Des questions ?</span><span class="sxs-lookup"><span data-stu-id="a9e6c-199">More questions?</span></span> [<span data-ttu-id="a9e6c-200">Essayez de hello Communauté Power BI</span><span class="sxs-lookup"><span data-stu-id="a9e6c-200">Try hello Power BI Community</span></span>](http://community.powerbi.com/)
