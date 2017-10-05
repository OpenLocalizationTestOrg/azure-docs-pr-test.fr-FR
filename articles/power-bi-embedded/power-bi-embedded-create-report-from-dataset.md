---
title: "Créer un rapport à partir d’un jeu de données dans Azure Power BI Embedded | Microsoft Docs"
description: "Il vous est à présent possible de créer des rapports Power BI Embedded à partir d’un jeu de données dans votre propre application."
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: 457f53aa76059dbb2faed6b264102f1f59b9918a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-new-report-from-a-dataset-in-power-bi-embedded"></a><span data-ttu-id="5f883-103">Créer un rapport à partir d’un jeu de données dans Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="5f883-103">Create a new report from a dataset in Power BI Embedded</span></span>

<span data-ttu-id="5f883-104">Il vous est à présent possible de créer des rapports Power BI Embedded à partir d’un jeu de données dans votre propre application.</span><span class="sxs-lookup"><span data-stu-id="5f883-104">Power BI Embedded reports can now be created from a dataset in your own application.</span></span> 

<span data-ttu-id="5f883-105">La méthode d’authentification est similaire à celle des rapports d’incorporation.</span><span class="sxs-lookup"><span data-stu-id="5f883-105">The authentication method is similar to that of report embed.</span></span> <span data-ttu-id="5f883-106">Elle est basée sur des jetons d’accès propres à un jeu de données.</span><span class="sxs-lookup"><span data-stu-id="5f883-106">It is based on access tokens that are specific to a dataset.</span></span> <span data-ttu-id="5f883-107">Les jetons utilisés pour PowerBI.com sont émis par Azure Active Directory (AAD), et les jetons Power BI Embedded par votre propre service.</span><span class="sxs-lookup"><span data-stu-id="5f883-107">Tokens used for PowerBI.com are issued by Azure Active Directory (AAD) and Power BI Embedded tokens are issued by your own service.</span></span>

<span data-ttu-id="5f883-108">Lors de la création d’un rapport Embedded, les jetons sont émis pour un jeu de données spécifique.</span><span class="sxs-lookup"><span data-stu-id="5f883-108">When createing an Embedded report, the tokens issued are for a specific dataset.</span></span> <span data-ttu-id="5f883-109">Les jetons doivent être associés à l’URL d’incorporation sur le même élément, de sorte que chacune possède un jeton unique.</span><span class="sxs-lookup"><span data-stu-id="5f883-109">Tokens should be associated with the embed URL on the same element to ensure each has a unique token.</span></span> <span data-ttu-id="5f883-110">Pour créer un rapport Embedded, les étendues *Dataset.Read et Workspace.Report.Create* doivent être fournies dans le jeton d’accès.</span><span class="sxs-lookup"><span data-stu-id="5f883-110">In order to create an Embedded report, *Dataset.Read and Workspace.Report.Create* scopes must be provided in the access token.</span></span>

## <a name="create-access-token-needed-to-create-new-report"></a><span data-ttu-id="5f883-111">Créer le jeton d’accès nécessaire à la création d’un rapport</span><span class="sxs-lookup"><span data-stu-id="5f883-111">Create access token needed to create new report</span></span>

<span data-ttu-id="5f883-112">Power BI Embedded utilise des jetons d’incorporation, qui sont des jetons JSON Web Token signés HMAC.</span><span class="sxs-lookup"><span data-stu-id="5f883-112">Power BI Embedded uses embed token, which are HMAC signed JSON Web Tokens.</span></span> <span data-ttu-id="5f883-113">Les jetons sont signés avec la clé d’accès issue de votre collection d’espaces de travail Azure Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="5f883-113">The tokens are signed with the access key from your Azure Power BI Embedded workspace collection.</span></span> <span data-ttu-id="5f883-114">Par défaut, les jetons d’incorporation sont utilisés pour fournir un accès en lecture seule à un rapport à incorporer dans une application.</span><span class="sxs-lookup"><span data-stu-id="5f883-114">Embed tokens, by default, are used to provide read only access to a report to embed into an application.</span></span> <span data-ttu-id="5f883-115">Les jetons d’incorporation sont émis pour un rapport donné et doivent être associés à une URL d’incorporation.</span><span class="sxs-lookup"><span data-stu-id="5f883-115">Embed tokens are issued for a specific report and should be associated with an embed URL.</span></span>

<span data-ttu-id="5f883-116">Les jetons d’accès doivent être créés sur le serveur, car les clés d’accès sont utilisées pour signer / chiffrer les jetons.</span><span class="sxs-lookup"><span data-stu-id="5f883-116">Access tokens should be created on the server as the access keys are used to sign/encrypt the tokens.</span></span> <span data-ttu-id="5f883-117">Pour plus d’informations sur la création de jetons d’accès, consultez la page [Authentification et autorisation avec Power BI Embedded](power-bi-embedded-app-token-flow.md).</span><span class="sxs-lookup"><span data-stu-id="5f883-117">For information on how to create an access token, see [Authenticating and authorizing with Power BI Embedded](power-bi-embedded-app-token-flow.md).</span></span> <span data-ttu-id="5f883-118">Vous pouvez également consulter la méthode [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_).</span><span class="sxs-lookup"><span data-stu-id="5f883-118">You can also review the [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) method.</span></span> <span data-ttu-id="5f883-119">Voici un exemple de ce à quoi cela ressemblerait avec le Kit de développement logiciel (SDK) .NET pour Power BI.</span><span class="sxs-lookup"><span data-stu-id="5f883-119">Here is an example of what this would look like using the .NET SDK for Power BI.</span></span>

<span data-ttu-id="5f883-120">Dans cet exemple, nous voulons créer un rapport sur notre ID de jeu de données.</span><span class="sxs-lookup"><span data-stu-id="5f883-120">In this example, we have our dataset id that we want to creat the new report on.</span></span> <span data-ttu-id="5f883-121">Nous devons également ajouter les étendues de *Dataset.Read et Workspace.Report.Create*.</span><span class="sxs-lookup"><span data-stu-id="5f883-121">We also need to add the scopes for *Dataset.Read and Workspace.Report.Create*.</span></span>

<span data-ttu-id="5f883-122">La *classe PowerBIToken* requiert l’installation du [package NuGet Power BI Core](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).</span><span class="sxs-lookup"><span data-stu-id="5f883-122">The *PowerBIToken class* requires that you install the [Power BI Core NuGut Package](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).</span></span>

<span data-ttu-id="5f883-123">**Installation du package NuGet**</span><span class="sxs-lookup"><span data-stu-id="5f883-123">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.Core
```

<span data-ttu-id="5f883-124">**Code C#**</span><span class="sxs-lookup"><span data-stu-id="5f883-124">**C# code**</span></span>

```
using Microsoft.PowerBI.Security;

// rlsUsername and roles are optional
string scopes = "Dataset.Read Workspace.Report.Create";
PowerBIToken embedToken = PowerBIToken.CreateReportEmbedTokenForCreation(workspaceCollectionName, workspaceId, datasetId, null, null, scopes);

var token = embedToken.Generate("{access key}");
```

## <a name="create-a-new-blank-report"></a><span data-ttu-id="5f883-125">Créer un rapport vide</span><span class="sxs-lookup"><span data-stu-id="5f883-125">Create a new blank report</span></span>

<span data-ttu-id="5f883-126">Pour pouvoir créer un nouveau rapport, la configuration de création doit être fournie.</span><span class="sxs-lookup"><span data-stu-id="5f883-126">In order to create a new report, the create configuration should be provided.</span></span> <span data-ttu-id="5f883-127">Elle doit inclure le jeton d’accès, l’URL d’incorporation et l’ID de jeu de données sur lesquels nous souhaitons créer le rapport.</span><span class="sxs-lookup"><span data-stu-id="5f883-127">This should include the access token, the embedURL and the datasetID that we want to create the report against.</span></span> <span data-ttu-id="5f883-128">Cela requiert l’installation du [package NuGet Power BI JavaScript](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/).</span><span class="sxs-lookup"><span data-stu-id="5f883-128">This requires that you install the nuget [Power BI JavaScript package](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/).</span></span> <span data-ttu-id="5f883-129">L’URL d’incorporation est simplement https://embedded.powerbi.com/appTokenReportEmbed.</span><span class="sxs-lookup"><span data-stu-id="5f883-129">The embedUrl will just be https://embedded.powerbi.com/appTokenReportEmbed.</span></span>

> [!NOTE]
> <span data-ttu-id="5f883-130">Vous pouvez utiliser [l’exemple d’incorporation de rapport JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/) pour tester les fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="5f883-130">You can use the [JavaScript Report Embed Sample](https://microsoft.github.io/PowerBI-JavaScript/demo/) to test functionality.</span></span> <span data-ttu-id="5f883-131">Il donne également des exemples de code pour les différentes opérations disponibles.</span><span class="sxs-lookup"><span data-stu-id="5f883-131">It also gives code examples for the different operations that are available.</span></span>

<span data-ttu-id="5f883-132">**Installation du package NuGet**</span><span class="sxs-lookup"><span data-stu-id="5f883-132">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.JavaScript
```

<span data-ttu-id="5f883-133">**Code JavaScript**</span><span class="sxs-lookup"><span data-stu-id="5f883-133">**JavaScript code**</span></span>

```
<div id="reportContainer"></div>
  
var embedCreateConfiguration = {
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        datasetId: '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
    };
    
    // Grab the reference to the div HTML element that will host the report
    var reportContainer = $('#reportContainer')[0];

    // Create report
    var report = powerbi.createReport(reportContainer, embedCreateConfiguration);
```

<span data-ttu-id="5f883-134">Appeler *powerbi.createReport()* fait apparaître un canevas vide en mode Édition dans l’élément *div*.</span><span class="sxs-lookup"><span data-stu-id="5f883-134">Calling *powerbi.createReport()* will make a blank canvas in edit mode appear within the *div* element.</span></span>

![](media/power-bi-embedded-create-report-from-dataset/pbi-embedded-create-new-report.png)

## <a name="save-new-reports"></a><span data-ttu-id="5f883-135">Enregistrer de nouveaux rapports</span><span class="sxs-lookup"><span data-stu-id="5f883-135">Save new reports</span></span>

<span data-ttu-id="5f883-136">Le rapport ne sera pas réellement créé avant que vous n’ayez appelé l’opération **enregistrer sous**.</span><span class="sxs-lookup"><span data-stu-id="5f883-136">The report will not actually be created until you call the **save as** operation.</span></span> <span data-ttu-id="5f883-137">Vous pouvez le faire dans le menu Fichier ou à partir de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="5f883-137">This can be done from file menu or from JavaScript.</span></span>

```
 // Get a reference to the embedded report.
    report = powerbi.get(reportContainer);
    
    var saveAsParameters = {
        name: "newReport"
    };

    // SaveAs report
    report.saveAs(saveAsParameters);
```

> [!IMPORTANT]
> <span data-ttu-id="5f883-138">Le nouveau rapport n’est créé qu’une fois que l’opération **enregistrer sous** a été appelée.</span><span class="sxs-lookup"><span data-stu-id="5f883-138">A new report is created only after **save as** is called.</span></span> <span data-ttu-id="5f883-139">Après l’enregistrement, le canevas continue d’afficher le jeu de données en mode Édition et non le rapport.</span><span class="sxs-lookup"><span data-stu-id="5f883-139">After you save, the canvas will still show the dataset in edit mode and not the report.</span></span> <span data-ttu-id="5f883-140">Vous devez recharger le nouveau rapport comme vous le feriez pour tout autre rapport.</span><span class="sxs-lookup"><span data-stu-id="5f883-140">You will need to reload the new report like you would any other report.</span></span>

![](media/power-bi-embedded-create-report-from-dataset/pbi-embedded-save-new-report.png)

## <a name="load-the-new-report"></a><span data-ttu-id="5f883-141">Charger le nouveau rapport</span><span class="sxs-lookup"><span data-stu-id="5f883-141">Load the new report</span></span>

<span data-ttu-id="5f883-142">Pour interagir avec le nouveau rapport, vous devez l’incorporer de la même façon que l’application incorpore un rapport normal, ce qui signifie qu’un nouveau jeton doit être émis spécifiquement pour le nouveau rapport avant que vous n’appeliez la méthode d’incorporation.</span><span class="sxs-lookup"><span data-stu-id="5f883-142">In order to interact with the new report you need to embed it in the same way the application embeds a regular report, meaning, a new token must be issued specifically for the new report and then call the embed method.</span></span>

```
<div id="reportContainer"></div>
  
var embedConfiguration = {
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MJ',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        reportId: '5dac7a4a-4452-46b3-99f6-a25915e0fe54',
    };
    
    // Grab the reference to the div HTML element that will host the report
    var reportContainer = $('#reportContainer')[0];

    // Embed report
    var report = powerbi.embed(reportContainer, embedConfiguration);
```

## <a name="automate-save-and-load-of-a-new-report-using-the-saved-event"></a><span data-ttu-id="5f883-143">Automatiser la sauvegarde et le chargement d’un nouveau rapport avec l’événement « enregistré »</span><span class="sxs-lookup"><span data-stu-id="5f883-143">Automate save and load of a new report using the "saved" event</span></span>

<span data-ttu-id="5f883-144">Pour automatiser le processus « enregistrer sous », puis charger le nouveau rapport, vous pouvez utiliser l’événement « enregistré ».</span><span class="sxs-lookup"><span data-stu-id="5f883-144">In order to automate the process of "save as" and then loading the new report you can make use of the "saved" Event.</span></span> <span data-ttu-id="5f883-145">Cet événement est déclenché quand l’opération « enregistrer » est terminée. Il retourne un objet JSON qui contient le nouvel ID du rapport, le nom du rapport, l’ancien ID du rapport (le cas échéant) et le type d’opération (« enregistrer sous » ou « enregistrer »).</span><span class="sxs-lookup"><span data-stu-id="5f883-145">This event is fired when the save operation is complete and it returns a Json object containing the new reportId, report name, the old reportId(if there was one) and if the operation was saveAs or save.</span></span>

```
{
  "reportObjectId": "5dac7a4a-4452-46b3-99f6-a25915e0fe54",
  "reportName": "newReport",
  "saveAs": true,
  "originalReportObjectId": null
}
```

<span data-ttu-id="5f883-146">Pour automatiser le processus, vous pouvez écouter l’événement « enregistrer », récupérer le nouvel ID du rapport, créer le nouveau jeton et y incorporer le nouveau rapport.</span><span class="sxs-lookup"><span data-stu-id="5f883-146">To Automate the process you can listen on the "saved" event, take the new reportId, create the new token and embed the new report with it.</span></span>

```
<div id="reportContainer"></div>
  
var embedCreateConfiguration = {
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        datasetId: '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
    };
    
    // Grab the reference to the div HTML element that will host the report
    var reportContainer = $('#reportContainer')[0];

    // Create report
    var report = powerbi.createReport(reportContainer, embedCreateConfiguration);


   var saveAsParameters = {
        name: "newReport"
    };

    // SaveAs report
    report.saveAs(saveAsParameters);

    // report.on will add an event handler which prints to Log window.
    report.on("saved", function(event) {
        
         // get new Token
         var newReportId =  event.detail.reportObjectId;

        // create new Token. This is a function that the application should provide
        var newToken = createAccessToken(newReportId,scopes /*provide the wanted scopes*/);
        
        
    var embedConfiguration = {
        accessToken: newToken ,
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        reportId: newReportId,
    };

    // Embed report
    var report = powerbi.embed(reportContainer, embedConfiguration);
       
   // report.off removes a given event handler if it exists.
   report.off("saved");
    });
```

## <a name="see-also"></a><span data-ttu-id="5f883-147">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="5f883-147">See also</span></span>

[<span data-ttu-id="5f883-148">Prise en main de l’exemple</span><span class="sxs-lookup"><span data-stu-id="5f883-148">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="5f883-149">Enregistrer des rapports</span><span class="sxs-lookup"><span data-stu-id="5f883-149">Save reports</span></span>](power-bi-embedded-save-reports.md)  
[<span data-ttu-id="5f883-150">Incorporer un rapport</span><span class="sxs-lookup"><span data-stu-id="5f883-150">Embed a report</span></span>](power-bi-embedded-embed-report.md)  
[<span data-ttu-id="5f883-151">Authentification et autorisation dans Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="5f883-151">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="5f883-152">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="5f883-152">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="5f883-153">Exemple d’incorporation JavaScript</span><span class="sxs-lookup"><span data-stu-id="5f883-153">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[<span data-ttu-id="5f883-154">Package NuGet Power BI Core</span><span class="sxs-lookup"><span data-stu-id="5f883-154">Power BI Core NuGut Package</span></span>](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)  
[<span data-ttu-id="5f883-155">Package JavaScript Power BI Core</span><span class="sxs-lookup"><span data-stu-id="5f883-155">Power BI JavaScript package</span></span>](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/)  
<span data-ttu-id="5f883-156">Des questions ?</span><span class="sxs-lookup"><span data-stu-id="5f883-156">More questions?</span></span> [<span data-ttu-id="5f883-157">Essayer la communauté Power BI</span><span class="sxs-lookup"><span data-stu-id="5f883-157">Try the Power BI Community</span></span>](http://community.powerbi.com/)