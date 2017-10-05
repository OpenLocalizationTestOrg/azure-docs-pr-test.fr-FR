---
title: "Prise en main d’un exemple"
description: "Power BI Embedded, utiliser SDK pour ajouter des rapports interactifs Power BI à votre application business intelligence"
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
ms.openlocfilehash: c3cb1763f807220a4a829f410d7eb77974b25776
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-power-bi-embedded-sample"></a><span data-ttu-id="2b5f8-103">Prise en main de l’exemple Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="2b5f8-103">Get started with Power BI Embedded sample</span></span>

<span data-ttu-id="2b5f8-104">Avec **Microsoft Power BI Embedded**, vous pouvez intégrer des rapports Power BI dans vos applications web ou mobiles.</span><span class="sxs-lookup"><span data-stu-id="2b5f8-104">With **Microsoft Power BI Embedded**, you can integrate Power BI reports right into your web or mobile applications.</span></span> <span data-ttu-id="2b5f8-105">Dans cet article, nous vous présenterons l’exemple de prise en main **Power BI Embedded** .</span><span class="sxs-lookup"><span data-stu-id="2b5f8-105">In this article, we'll introduce you to the **Power BI Embedded** get started sample.</span></span>

<span data-ttu-id="2b5f8-106">Avant de poursuivre, vous souhaiterez probablement enregistrer les ressources suivantes.</span><span class="sxs-lookup"><span data-stu-id="2b5f8-106">Before we go any further, you'll probably want to save the following resources.</span></span> <span data-ttu-id="2b5f8-107">Elles vous aideront lors de l’intégration de rapports Power BI dans l’exemple d’application et vos propres applications également.</span><span class="sxs-lookup"><span data-stu-id="2b5f8-107">They'll help you when integrating Power BI reports into the sample app and your own apps too.</span></span>

* [<span data-ttu-id="2b5f8-108">Exemple d’application web d’espace de travail</span><span class="sxs-lookup"><span data-stu-id="2b5f8-108">Sample workspace web app</span></span>](http://go.microsoft.com/fwlink/?LinkId=761493)
* [<span data-ttu-id="2b5f8-109">Référence de l’API Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="2b5f8-109">Power BI Embedded API reference</span></span>](https://msdn.microsoft.com/en-US/library/azure/mt711507.aspx)
* <span data-ttu-id="2b5f8-110">[Kit de développement logiciel (SDK) .NET Power BI Embedded ](http://go.microsoft.com/fwlink/?LinkId=746472) (disponible par le biais de NuGet)</span><span class="sxs-lookup"><span data-stu-id="2b5f8-110">[Power BI Embedded .NET SDK ](http://go.microsoft.com/fwlink/?LinkId=746472) (available via NuGet)</span></span>
* [<span data-ttu-id="2b5f8-111">Exemple de rapport JavaScript intégré</span><span class="sxs-lookup"><span data-stu-id="2b5f8-111">JavaScript Report Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo)

> [!NOTE] 
> <span data-ttu-id="2b5f8-112">Avant de configurer et d’exécuter l’exemple de prise en main de Power BI Embedded, vous devez créer au moins une **collection d’espaces de travail** dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="2b5f8-112">Before you can configure and run the Power BI Embedded get started sample, you need to create at least one **Workspace Collection** in your Azure subscription.</span></span> <span data-ttu-id="2b5f8-113">Pour savoir comment créer une **collection d’espaces de travail** dans le portail Azure, consultez [Prise en main de Power BI Embedded (aperçu)](power-bi-embedded-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="2b5f8-113">To learn how to create a **Workspace Collection** in the Azure Portal see [Getting Started with Power BI Embedded](power-bi-embedded-get-started.md).</span></span>

## <a name="configure-the-sample-app"></a><span data-ttu-id="2b5f8-114">Configurer l’exemple d’application</span><span class="sxs-lookup"><span data-stu-id="2b5f8-114">Configure the sample app</span></span>

<span data-ttu-id="2b5f8-115">Passons à la configuration de votre environnement de développement Visual Studio pour accéder aux composants nécessaires à l’exécution de l’exemple d’application.</span><span class="sxs-lookup"><span data-stu-id="2b5f8-115">Let's walk through setting up your Visual Studio development environment to access the  components needed to run the sample app.</span></span>

1. <span data-ttu-id="2b5f8-116">Téléchargez et décompressez l’exemple [Power BI Embedded - Intégrer un rapport dans une application web](http://go.microsoft.com/fwlink/?LinkId=761493) sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="2b5f8-116">Download and unzip the [Power BI Embedded - Integrate a report into a web app](http://go.microsoft.com/fwlink/?LinkId=761493) sample on GitHub.</span></span>
2. <span data-ttu-id="2b5f8-117">Ouvrez **PowerBI-embedded.sln** dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2b5f8-117">Open **PowerBI-embedded.sln** in Visual Studio.</span></span> <span data-ttu-id="2b5f8-118">Vous devrez peut-être exécuter la commande **Update-Package** dans la Console du Gestionnaire de Package NuGet pour mettre à jour les packages utilisés dans cette solution.</span><span class="sxs-lookup"><span data-stu-id="2b5f8-118">You may need to execute the **Update-Package** command in the NuGET Package Manager Console in order to update the packages used in this solution.</span></span>
3. <span data-ttu-id="2b5f8-119">Générez la solution.</span><span class="sxs-lookup"><span data-stu-id="2b5f8-119">Build the solution.</span></span>
4. <span data-ttu-id="2b5f8-120">Exécutez l’application de console **ProvisionSample** .</span><span class="sxs-lookup"><span data-stu-id="2b5f8-120">Run the **ProvisionSample** console app.</span></span> <span data-ttu-id="2b5f8-121">Dans l’exemple d’application console, vous allez approvisionner un espace de travail et importer un fichier PBIX.</span><span class="sxs-lookup"><span data-stu-id="2b5f8-121">In the sample console app, you provision a workspace and import a PBIX file.</span></span>
5. <span data-ttu-id="2b5f8-122">Pour approvisionner un nouvel **espace de travail**, sélectionnez l’option 1, **Collection management** (Gestion des collections), puis choisissez l’option 6, **Provision a new Workspace** (Approvisionner un nouvel espace de travail).</span><span class="sxs-lookup"><span data-stu-id="2b5f8-122">To provision a new **Workspace**, select option 1, **Collection management**, and then select option 6, **Provision a new Workspace**</span></span>
6. <span data-ttu-id="2b5f8-123">Pour importer un nouveau **rapport**, sélectionnez l’option 2, **Report management** (Gestion de rapport), puis sélectionnez l’option 3, **Import PBIX Desktop file into a workspace** (Importer le fichier PBIX Desktop dans un espace de travail).</span><span class="sxs-lookup"><span data-stu-id="2b5f8-123">To import a new **Report**, select option 2, **Report management**, and then select option 3, **Import PBIX Desktop file into a workspace**.</span></span>

7. <span data-ttu-id="2b5f8-124">Entrez le nom de votre **collection d’espaces de travail** et la **clé d’accès**.</span><span class="sxs-lookup"><span data-stu-id="2b5f8-124">Enter your **Workspace Collection** name, and **Access Key**.</span></span> <span data-ttu-id="2b5f8-125">Vous pouvez les obtenir dans le **Portail Azure**.</span><span class="sxs-lookup"><span data-stu-id="2b5f8-125">You can get these in the **Azure Portal**.</span></span> <span data-ttu-id="2b5f8-126">Pour en savoir plus sur la façon d’obtenir votre **clé d’accès**, consultez [Affichage des touches d’accès rapide aux API de Power BI](power-bi-embedded-get-started.md#view-power-bi-api-access-keys) dans Prise en main de Microsoft Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="2b5f8-126">To learn more about how to get your **Access Key**, see [View Power BI API Access Keys](power-bi-embedded-get-started.md#view-power-bi-api-access-keys) in Get started with Microsoft Power BI Embedded.</span></span>

    ![](media/powerbi-embedded-get-started-sample/azure-portal.png)
8. <span data-ttu-id="2b5f8-127">Copiez et enregistrez **l’ID d’espace de travail** qui vient d’être créé et qui sera utilisé ultérieurement dans cet article.</span><span class="sxs-lookup"><span data-stu-id="2b5f8-127">Copy and save the newly created **Workspace ID** to use later in this article.</span></span> <span data-ttu-id="2b5f8-128">Une fois l’**ID d’espace de travail** créé, il est disponible dans le **portail Azure**.</span><span class="sxs-lookup"><span data-stu-id="2b5f8-128">After the **Workspace ID** is created, you can find it the **Azure Portal**.</span></span>

    ![](media/powerbi-embedded-get-started-sample/workspace-id.png)
9. <span data-ttu-id="2b5f8-129">Pour importer un fichier PBIX dans votre **espace de travail**, sélectionnez l’option **6. Importez le fichier PBIX Desktop dans un espace de travail existant**.</span><span class="sxs-lookup"><span data-stu-id="2b5f8-129">To import a PBIX file into your **Workspace**, select option **6. Import PBIX Desktop file into an existing workspace**.</span></span> <span data-ttu-id="2b5f8-130">Si vous n’avez pas de fichier PBIX sous la main, téléchargez [l’exemple PBIX Analyse des données de vente](http://go.microsoft.com/fwlink/?LinkID=780547).</span><span class="sxs-lookup"><span data-stu-id="2b5f8-130">If you don't have a PBIX file handy, you can download the [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547).</span></span>
10. <span data-ttu-id="2b5f8-131">Si vous y êtes invité, entrez un nom convivial pour votre **jeu de données**.</span><span class="sxs-lookup"><span data-stu-id="2b5f8-131">If prompted, enter a friendly name for your **Dataset**.</span></span>

<span data-ttu-id="2b5f8-132">La réponse doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="2b5f8-132">You should see a response like:</span></span>

```
Checking import state... Publishing
Checking import state... Succeeded
```

> [!NOTE]
> <span data-ttu-id="2b5f8-133">Si votre fichier PBIX contient des connexions de requête directe, exécutez l’option 7 pour mettre à jour les chaînes de connexion.</span><span class="sxs-lookup"><span data-stu-id="2b5f8-133">If your PBIX file contains any direct query connections, run option 7 to update the connection strings.</span></span>

<span data-ttu-id="2b5f8-134">À ce stade, vous avez un rapport PBIX Power BI qui a été importé dans votre **espace de travail**.</span><span class="sxs-lookup"><span data-stu-id="2b5f8-134">At this point, you have a Power BI PBIX report imported into your **Workspace**.</span></span> <span data-ttu-id="2b5f8-135">Voyons maintenant comment exécuter l’exemple d’application web de prise en main de **Power BI Embedded**.</span><span class="sxs-lookup"><span data-stu-id="2b5f8-135">Now, let's look at how to run the **Power BI Embedded** get started sample web app.</span></span>

## <a name="run-the-sample-web-app"></a><span data-ttu-id="2b5f8-136">Exécuter l’exemple d’application web</span><span class="sxs-lookup"><span data-stu-id="2b5f8-136">Run the sample web app</span></span>
<span data-ttu-id="2b5f8-137">L’exemple d’application web est un exemple d’application qui restitue les rapports importés dans votre **espace de travail**.</span><span class="sxs-lookup"><span data-stu-id="2b5f8-137">The web app sample is a sample application that renders reports imported into your **Workspace**.</span></span> <span data-ttu-id="2b5f8-138">Voici comment configurer l’exemple d’application web.</span><span class="sxs-lookup"><span data-stu-id="2b5f8-138">Here's how to configure the web app sample.</span></span>

1. <span data-ttu-id="2b5f8-139">Dans la solution Visual Studio **PowerBI-embedded**, cliquez avec le bouton droit sur l’application web **EmbedSample**, puis choisissez **Définir comme projet de démarrage**.</span><span class="sxs-lookup"><span data-stu-id="2b5f8-139">In the **PowerBI-embedded** Visual Studio solution, right click the **EmbedSample** web application, and choose **Set as StartUp project**.</span></span>
2. <span data-ttu-id="2b5f8-140">Dans **web.config**, dans l’application web **EmbedSample**, modifiez la section **appSettings** : **AccessKey**, le nom **WorkspaceCollection** et **WorkspaceId**.</span><span class="sxs-lookup"><span data-stu-id="2b5f8-140">In **web.config**, in the **EmbedSample** web application, edit the **appSettings**: **AccessKey**, **WorkspaceCollection** name, and **WorkspaceId**.</span></span>

    ```
    <appSettings>
        <add key="powerbi:AccessKey" value="" />
        <add key="powerbi:ApiUrl" value="https://api.powerbi.com" />
        <add key="powerbi:WorkspaceCollection" value="" />
        <add key="powerbi:WorkspaceId" value="" />
    </appSettings>
    ```
3. <span data-ttu-id="2b5f8-141">Exécutez l’application web **EmbedSample**.</span><span class="sxs-lookup"><span data-stu-id="2b5f8-141">Run the **EmbedSample** web application.</span></span>

<span data-ttu-id="2b5f8-142">Une fois que vous avez exécuté l’application web **EmbedSample**, le volet de navigation gauche doit contenir un menu **Rapports**.</span><span class="sxs-lookup"><span data-stu-id="2b5f8-142">Once you run the **EmbedSample** web application, the left navigation panel should contain a **Reports** menu.</span></span> <span data-ttu-id="2b5f8-143">Pour afficher le rapport que vous avez importé, développez **Rapports**, puis cliquez sur un rapport.</span><span class="sxs-lookup"><span data-stu-id="2b5f8-143">To view the report you imported, expand **Reports**, and click a report.</span></span> <span data-ttu-id="2b5f8-144">Si vous avez importé l’[exemple PBIX Analyse des données de vente](http://go.microsoft.com/fwlink/?LinkID=780547), l’exemple d’application web a l’aspect suivant :</span><span class="sxs-lookup"><span data-stu-id="2b5f8-144">If you imported the [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547), the sample web app would look like this:</span></span>

![](media/powerbi-embedded-get-started-sample/power-bi-embedded-sample-left-nav.png)

<span data-ttu-id="2b5f8-145">Une fois que vous avez cliqué sur un rapport, l’application web **EmbedSample** doit avoir l’aspect suivant :</span><span class="sxs-lookup"><span data-stu-id="2b5f8-145">After you click a report, the **EmbedSample** web application should look something this:</span></span>

![](media/powerbi-embedded-get-started-sample/sample-web-app.png)

## <a name="explore-the-sample-code"></a><span data-ttu-id="2b5f8-146">Explorer l’exemple de code</span><span class="sxs-lookup"><span data-stu-id="2b5f8-146">Explore the sample code</span></span>

<span data-ttu-id="2b5f8-147">L’exemple **Microsoft Power BI Embedded** est un exemple d’application web qui vous montre comment intégrer des rapports **Power BI** dans votre application.</span><span class="sxs-lookup"><span data-stu-id="2b5f8-147">The **Microsoft Power BI Embedded** sample is an example web app that shows you how to integrate **Power BI** reports into your app.</span></span> <span data-ttu-id="2b5f8-148">Il utilise un modèle de conception MVC (Model-View-Controller) pour illustrer les meilleures pratiques.</span><span class="sxs-lookup"><span data-stu-id="2b5f8-148">It uses a Model-View-Controller (MVC) design pattern to demonstrate best practices.</span></span> <span data-ttu-id="2b5f8-149">Cette section met en évidence les parties de l’exemple de code que vous pouvez explorer dans la solution d’application web **PowerBI-embedded**.</span><span class="sxs-lookup"><span data-stu-id="2b5f8-149">This section highlights parts of the sample code that you can explore within the **PowerBI-embedded** web app solution.</span></span> <span data-ttu-id="2b5f8-150">Le modèle MVC (Model-View-Controller) sépare la modélisation du domaine, la présentation et les actions basées sur les entrées des utilisateurs en trois classes distinctes : modèle, affichage et contrôle.</span><span class="sxs-lookup"><span data-stu-id="2b5f8-150">The Model-View-Controller (MVC) pattern separates the modeling of the domain, the presentation, and the actions based on user input into three separate classes: Model, View, and Control.</span></span> <span data-ttu-id="2b5f8-151">Pour plus d’informations sur MVC, consultez [En savoir plus sur ASP.NET](http://www.asp.net/mvc).</span><span class="sxs-lookup"><span data-stu-id="2b5f8-151">To learn more about MVC, see [Learn About ASP.NET](http://www.asp.net/mvc).</span></span>

<span data-ttu-id="2b5f8-152">L’exemple **Microsoft Power BI Embedded** inclut les sections suivantes.</span><span class="sxs-lookup"><span data-stu-id="2b5f8-152">The **Microsoft Power BI Embedded** sample code is separated as follows.</span></span> <span data-ttu-id="2b5f8-153">Chacune d’elles inclut le nom de fichier dans la solution PowerBI-embedded.sln afin que vous puissiez facilement trouver le code dans l’exemple.</span><span class="sxs-lookup"><span data-stu-id="2b5f8-153">Each section includes the file name in the PowerBI-embedded.sln solution so that you can easily find the code in the sample.</span></span>

> [!NOTE]
> <span data-ttu-id="2b5f8-154">Cette section est un résumé de l’exemple de code qui montre comment le code a été écrit.</span><span class="sxs-lookup"><span data-stu-id="2b5f8-154">This section is a summary of the sample code that shows how the code was written.</span></span> <span data-ttu-id="2b5f8-155">Pour afficher l’exemple complet, chargez la solution PowerBI-embedded.sln dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2b5f8-155">To view the complete sample, please load the PowerBI-embedded.sln solution in Visual Studio.</span></span>

### <a name="model"></a><span data-ttu-id="2b5f8-156">Modèle</span><span class="sxs-lookup"><span data-stu-id="2b5f8-156">Model</span></span>

<span data-ttu-id="2b5f8-157">L’exemple inclut deux modèles : **ReportsViewModel** et **ReportViewModel**.</span><span class="sxs-lookup"><span data-stu-id="2b5f8-157">The sample has a **ReportsViewModel** and **ReportViewModel**.</span></span>

<span data-ttu-id="2b5f8-158">**ReportsViewModel.cs** : représente les rapports Power BI.</span><span class="sxs-lookup"><span data-stu-id="2b5f8-158">**ReportsViewModel.cs**: Represents Power BI Reports.</span></span>

    public class ReportsViewModel
    {
        public List<Report> Reports { get; set; }
    }

<span data-ttu-id="2b5f8-159">**ReportViewModel.cs** : représente un rapport Power BI.</span><span class="sxs-lookup"><span data-stu-id="2b5f8-159">**ReportViewModel.cs**: Represents a Power BI Report.</span></span>

    public classReportViewModel
    {
        public IReport Report { get; set; }

        public string AccessToken { get; set; }
    }

### <a name="connection-string"></a><span data-ttu-id="2b5f8-160">Chaîne de connexion</span><span class="sxs-lookup"><span data-stu-id="2b5f8-160">Connection string</span></span>

<span data-ttu-id="2b5f8-161">La chaîne de connexion doit avoir le format suivant :</span><span class="sxs-lookup"><span data-stu-id="2b5f8-161">The connection string must be in the following format:</span></span>

```
Data Source=tcp:MyServer.database.windows.net,1433;Initial Catalog=MyDatabase
```

<span data-ttu-id="2b5f8-162">L’utilisation d’attributs de serveur et de base de données communs échoue.</span><span class="sxs-lookup"><span data-stu-id="2b5f8-162">Using common server and database attributes will fail.</span></span> <span data-ttu-id="2b5f8-163">Par exemple : Server=tcp:MyServer.database.windows.net,1433;Database=MyDatabase,</span><span class="sxs-lookup"><span data-stu-id="2b5f8-163">For example: Server=tcp:MyServer.database.windows.net,1433;Database=MyDatabase,</span></span>

### <a name="view"></a><span data-ttu-id="2b5f8-164">Affichage</span><span class="sxs-lookup"><span data-stu-id="2b5f8-164">View</span></span>

<span data-ttu-id="2b5f8-165">L’**affichage** gère la présentation des **rapports** Power BI et d’un **rapport** Power BI.</span><span class="sxs-lookup"><span data-stu-id="2b5f8-165">The **View** manages the display of Power BI **Reports** and a Power BI **Report**.</span></span>

<span data-ttu-id="2b5f8-166">**Reports.cshtml** : effectue une itération sur **Model.Reports** pour créer un **ActionLink**.</span><span class="sxs-lookup"><span data-stu-id="2b5f8-166">**Reports.cshtml**: Iterate over **Model.Reports** to create an **ActionLink**.</span></span> <span data-ttu-id="2b5f8-167">**ActionLink** est composé comme suit :</span><span class="sxs-lookup"><span data-stu-id="2b5f8-167">The **ActionLink** is composed as follows:</span></span>

| <span data-ttu-id="2b5f8-168">Partie</span><span class="sxs-lookup"><span data-stu-id="2b5f8-168">Part</span></span> | <span data-ttu-id="2b5f8-169">Description</span><span class="sxs-lookup"><span data-stu-id="2b5f8-169">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2b5f8-170">Intitulé</span><span class="sxs-lookup"><span data-stu-id="2b5f8-170">Title</span></span> |<span data-ttu-id="2b5f8-171">Nom du rapport.</span><span class="sxs-lookup"><span data-stu-id="2b5f8-171">Name of the Report.</span></span> |
| <span data-ttu-id="2b5f8-172">QueryString</span><span class="sxs-lookup"><span data-stu-id="2b5f8-172">QueryString</span></span> |<span data-ttu-id="2b5f8-173">Lien vers l’ID de rapport.</span><span class="sxs-lookup"><span data-stu-id="2b5f8-173">A link to the Report ID.</span></span> |

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

<span data-ttu-id="2b5f8-174">Report.cshtml : définit **Model.AccessToken** et l’expression lambda pour **PowerBIReportFor**.</span><span class="sxs-lookup"><span data-stu-id="2b5f8-174">Report.cshtml: Set the **Model.AccessToken**, and the Lambda expression for **PowerBIReportFor**.</span></span>

    @model ReportViewModel

    ...

    <div class="side-body padding-top">
        @Html.PowerBIAccessToken(Model.AccessToken)
        @Html.PowerBIReportFor(m => m.Report, new { style = "height:85vh" })
    </div>

### <a name="controller"></a><span data-ttu-id="2b5f8-175">Controller</span><span class="sxs-lookup"><span data-stu-id="2b5f8-175">Controller</span></span>

<span data-ttu-id="2b5f8-176">**DashboardController.cs** : crée un PowerBIClient qui transmet un **jeton d’application**.</span><span class="sxs-lookup"><span data-stu-id="2b5f8-176">**DashboardController.cs**: Creates a PowerBIClient passing an **app token**.</span></span> <span data-ttu-id="2b5f8-177">Un jeton JWT (JSON Web Token) est généré à partir de la **clé de signature** pour obtenir les **informations d’identification**.</span><span class="sxs-lookup"><span data-stu-id="2b5f8-177">A JSON Web Token (JWT) is generated from the **Signing Key** to get the **Credentials**.</span></span> <span data-ttu-id="2b5f8-178">Les **informations d’identification** sont utilisées pour créer une instance de **PowerBIClient**.</span><span class="sxs-lookup"><span data-stu-id="2b5f8-178">The **Credentials** are used to create an instance of **PowerBIClient**.</span></span> <span data-ttu-id="2b5f8-179">Une fois que vous avez une instance de **PowerBIClient**, vous pouvez appeler GetReports() et GetReportsAsync().</span><span class="sxs-lookup"><span data-stu-id="2b5f8-179">Once you have an instance of **PowerBIClient**, you can call GetReports() and GetReportsAsync().</span></span>

<span data-ttu-id="2b5f8-180">CreatePowerBIClient()</span><span class="sxs-lookup"><span data-stu-id="2b5f8-180">CreatePowerBIClient()</span></span>

    private IPowerBIClient CreatePowerBIClient()
    {
        var credentials = new TokenCredentials(accessKey, "AppKey");
        var client = new PowerBIClient(credentials)
        {
            BaseUri = new Uri(apiUrl)
        };

        return client;
    }

<span data-ttu-id="2b5f8-181">ActionResult Reports()</span><span class="sxs-lookup"><span data-stu-id="2b5f8-181">ActionResult Reports()</span></span>

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


<span data-ttu-id="2b5f8-182">Task<ActionResult> Report(string reportId)</span><span class="sxs-lookup"><span data-stu-id="2b5f8-182">Task<ActionResult> Report(string reportId)</span></span>

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

### <a name="integrate-a-report-into-your-app"></a><span data-ttu-id="2b5f8-183">Intégrer un rapport dans votre application</span><span class="sxs-lookup"><span data-stu-id="2b5f8-183">Integrate a report into your app</span></span>

<span data-ttu-id="2b5f8-184">Une fois que vous avez un **rapport**, utilisez un **iframe** pour incorporer le **rapport** Power BI.</span><span class="sxs-lookup"><span data-stu-id="2b5f8-184">Once you have a **Report**, you use an **IFrame** to embed the Power BI **Report**.</span></span> <span data-ttu-id="2b5f8-185">Voici un extrait de code powerbi.js dans l’exemple **Microsoft Power BI Embedded**.</span><span class="sxs-lookup"><span data-stu-id="2b5f8-185">Here is a code snippet from  powerbi.js in the **Microsoft Power BI Embedded** sample.</span></span>

![](media/powerbi-embedded-get-started-sample/power-bi-embedded-iframe-code.png)

## <a name="filter-reports-embedded-in-your-application"></a><span data-ttu-id="2b5f8-186">Filtrer les rapports incorporés dans votre application</span><span class="sxs-lookup"><span data-stu-id="2b5f8-186">Filter reports embedded in your application</span></span>

<span data-ttu-id="2b5f8-187">Vous pouvez filtrer un rapport incorporé à l’aide d’une syntaxe d’URL.</span><span class="sxs-lookup"><span data-stu-id="2b5f8-187">You can filter an embedded report using a URL syntax.</span></span> <span data-ttu-id="2b5f8-188">Pour ce faire, ajoutez un paramètre de chaîne de requête **$filter** avec un opérateur **eq** à l’URL src iframe avec le filtre spécifié.</span><span class="sxs-lookup"><span data-stu-id="2b5f8-188">To do this, you add a **$filter** query string parameter with an **eq** operator to your iFrame src url with the filter specified.</span></span> <span data-ttu-id="2b5f8-189">Voici la syntaxe de requête de filtre :</span><span class="sxs-lookup"><span data-stu-id="2b5f8-189">Here is the filter query syntax:</span></span>

```
https://app.powerbi.com/reportEmbed
?reportId=d2a0ea38-...-9673-ee9655d54a4a&
$filter={tableName/fieldName}%20eq%20'{fieldValue}'
```

> [!NOTE]
> <span data-ttu-id="2b5f8-190">{tableName/fieldName} ne peut pas contenir d’espaces ou de caractères spéciaux.</span><span class="sxs-lookup"><span data-stu-id="2b5f8-190">{tableName/fieldName} cannot include spaces or special characters.</span></span> <span data-ttu-id="2b5f8-191">{fieldValue} accepte une seule valeur de catégorie.</span><span class="sxs-lookup"><span data-stu-id="2b5f8-191">The {fieldValue} accepts a single categorical value.</span></span>  

## <a name="see-also"></a><span data-ttu-id="2b5f8-192">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="2b5f8-192">See also</span></span>

[<span data-ttu-id="2b5f8-193">Scénarios Microsoft Power BI Embedded courants</span><span class="sxs-lookup"><span data-stu-id="2b5f8-193">Common Microsoft Power BI Embedded scenarios</span></span>](power-bi-embedded-scenarios.md)  
[<span data-ttu-id="2b5f8-194">Authentification et autorisation dans Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="2b5f8-194">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="2b5f8-195">Incorporer un rapport</span><span class="sxs-lookup"><span data-stu-id="2b5f8-195">Embed a report</span></span>](power-bi-embedded-embed-report.md)  
[<span data-ttu-id="2b5f8-196">Créer un rapport à partir d’un jeu de données</span><span class="sxs-lookup"><span data-stu-id="2b5f8-196">Create a new report from a dataset</span></span>](power-bi-embedded-create-report-from-dataset.md)  
[<span data-ttu-id="2b5f8-197">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="2b5f8-197">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="2b5f8-198">Exemple d’incorporation JavaScript</span><span class="sxs-lookup"><span data-stu-id="2b5f8-198">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
<span data-ttu-id="2b5f8-199">Des questions ?</span><span class="sxs-lookup"><span data-stu-id="2b5f8-199">More questions?</span></span> [<span data-ttu-id="2b5f8-200">Essayer la communauté Power BI</span><span class="sxs-lookup"><span data-stu-id="2b5f8-200">Try the Power BI Community</span></span>](http://community.powerbi.com/)
