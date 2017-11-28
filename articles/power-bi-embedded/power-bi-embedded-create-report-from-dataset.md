---
title: "aaaCreate un nouveau rapport à partir d’un jeu de données Azure Power BI Embedded | Documents Microsoft"
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
ms.openlocfilehash: 41a0a52e4c833313f495bb5ff14749203fef9b41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-new-report-from-a-dataset-in-power-bi-embedded"></a><span data-ttu-id="3fefb-103">Créer un rapport à partir d’un jeu de données dans Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="3fefb-103">Create a new report from a dataset in Power BI Embedded</span></span>

<span data-ttu-id="3fefb-104">Il vous est à présent possible de créer des rapports Power BI Embedded à partir d’un jeu de données dans votre propre application.</span><span class="sxs-lookup"><span data-stu-id="3fefb-104">Power BI Embedded reports can now be created from a dataset in your own application.</span></span> 

<span data-ttu-id="3fefb-105">Hello méthode d’authentification est similaire incorporer des toothat du rapport.</span><span class="sxs-lookup"><span data-stu-id="3fefb-105">hello authentication method is similar toothat of report embed.</span></span> <span data-ttu-id="3fefb-106">Il est basé sur les jetons d’accès qui sont le jeu de données tooa spécifique.</span><span class="sxs-lookup"><span data-stu-id="3fefb-106">It is based on access tokens that are specific tooa dataset.</span></span> <span data-ttu-id="3fefb-107">Les jetons utilisés pour PowerBI.com sont émis par Azure Active Directory (AAD), et les jetons Power BI Embedded par votre propre service.</span><span class="sxs-lookup"><span data-stu-id="3fefb-107">Tokens used for PowerBI.com are issued by Azure Active Directory (AAD) and Power BI Embedded tokens are issued by your own service.</span></span>

<span data-ttu-id="3fefb-108">Lorsque vous createing un rapport incorporé, hello jetons émis sont pour un jeu de données spécifique.</span><span class="sxs-lookup"><span data-stu-id="3fefb-108">When createing an Embedded report, hello tokens issued are for a specific dataset.</span></span> <span data-ttu-id="3fefb-109">Les jetons doivent être associées avec hello incorporer des URL sur hello même élément tooensure chaque a un jeton unique.</span><span class="sxs-lookup"><span data-stu-id="3fefb-109">Tokens should be associated with hello embed URL on hello same element tooensure each has a unique token.</span></span> <span data-ttu-id="3fefb-110">Dans commande toocreate un rapport incorporé, *Dataset.Read et Workspace.Report.Create* étendues doivent être fournis dans le jeton d’accès hello.</span><span class="sxs-lookup"><span data-stu-id="3fefb-110">In order toocreate an Embedded report, *Dataset.Read and Workspace.Report.Create* scopes must be provided in hello access token.</span></span>

## <a name="create-access-token-needed-toocreate-new-report"></a><span data-ttu-id="3fefb-111">Créer rapport accès jeton toocreate nécessaires</span><span class="sxs-lookup"><span data-stu-id="3fefb-111">Create access token needed toocreate new report</span></span>

<span data-ttu-id="3fefb-112">Power BI Embedded utilise des jetons d’incorporation, qui sont des jetons JSON Web Token signés HMAC.</span><span class="sxs-lookup"><span data-stu-id="3fefb-112">Power BI Embedded uses embed token, which are HMAC signed JSON Web Tokens.</span></span> <span data-ttu-id="3fefb-113">les jetons de Hello sont signés avec la clé d’accès hello dans votre collection de l’espace de travail Azure Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="3fefb-113">hello tokens are signed with hello access key from your Azure Power BI Embedded workspace collection.</span></span> <span data-ttu-id="3fefb-114">Incorporer des jetons, par défaut, sont utilisé tooprovide lire uniquement accès aux tooa rapport tooembed dans une application.</span><span class="sxs-lookup"><span data-stu-id="3fefb-114">Embed tokens, by default, are used tooprovide read only access tooa report tooembed into an application.</span></span> <span data-ttu-id="3fefb-115">Les jetons d’incorporation sont émis pour un rapport donné et doivent être associés à une URL d’incorporation.</span><span class="sxs-lookup"><span data-stu-id="3fefb-115">Embed tokens are issued for a specific report and should be associated with an embed URL.</span></span>

<span data-ttu-id="3fefb-116">Les jetons d’accès doivent être créés sur le serveur de hello comme clés d’accès hello sont utilisées toosign/chiffrer les jetons hello.</span><span class="sxs-lookup"><span data-stu-id="3fefb-116">Access tokens should be created on hello server as hello access keys are used toosign/encrypt hello tokens.</span></span> <span data-ttu-id="3fefb-117">Pour plus d’informations sur la façon de toocreate un jeton d’accès, consultez [authentification et autorisation avec Power BI Embedded](power-bi-embedded-app-token-flow.md).</span><span class="sxs-lookup"><span data-stu-id="3fefb-117">For information on how toocreate an access token, see [Authenticating and authorizing with Power BI Embedded](power-bi-embedded-app-token-flow.md).</span></span> <span data-ttu-id="3fefb-118">Vous pouvez également examiner hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) (méthode).</span><span class="sxs-lookup"><span data-stu-id="3fefb-118">You can also review hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) method.</span></span> <span data-ttu-id="3fefb-119">Voici un exemple de ce que cela ressemble à l’aide de hello .NET SDK pour Power BI.</span><span class="sxs-lookup"><span data-stu-id="3fefb-119">Here is an example of what this would look like using hello .NET SDK for Power BI.</span></span>

<span data-ttu-id="3fefb-120">Dans cet exemple, nous avons notre id de jeu de données que nous souhaitons rapport toocreat hello sur.</span><span class="sxs-lookup"><span data-stu-id="3fefb-120">In this example, we have our dataset id that we want toocreat hello new report on.</span></span> <span data-ttu-id="3fefb-121">Nous devons également des étendues de hello tooadd pour *Dataset.Read et Workspace.Report.Create*.</span><span class="sxs-lookup"><span data-stu-id="3fefb-121">We also need tooadd hello scopes for *Dataset.Read and Workspace.Report.Create*.</span></span>

<span data-ttu-id="3fefb-122">Hello *PowerBIToken classe* nécessite que vous installiez hello [Power BI Core NuGut Package](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).</span><span class="sxs-lookup"><span data-stu-id="3fefb-122">hello *PowerBIToken class* requires that you install hello [Power BI Core NuGut Package](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).</span></span>

<span data-ttu-id="3fefb-123">**Installation du package NuGet**</span><span class="sxs-lookup"><span data-stu-id="3fefb-123">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.Core
```

<span data-ttu-id="3fefb-124">**Code C#**</span><span class="sxs-lookup"><span data-stu-id="3fefb-124">**C# code**</span></span>

```
using Microsoft.PowerBI.Security;

// rlsUsername and roles are optional
string scopes = "Dataset.Read Workspace.Report.Create";
PowerBIToken embedToken = PowerBIToken.CreateReportEmbedTokenForCreation(workspaceCollectionName, workspaceId, datasetId, null, null, scopes);

var token = embedToken.Generate("{access key}");
```

## <a name="create-a-new-blank-report"></a><span data-ttu-id="3fefb-125">Créer un rapport vide</span><span class="sxs-lookup"><span data-stu-id="3fefb-125">Create a new blank report</span></span>

<span data-ttu-id="3fefb-126">Dans l’ordre toocreate un nouveau rapport, créez hello configuration doit être fournie.</span><span class="sxs-lookup"><span data-stu-id="3fefb-126">In order toocreate a new report, hello create configuration should be provided.</span></span> <span data-ttu-id="3fefb-127">Cela doit inclure le jeton d’accès hello, hello embedURL et hello datasetID que nous souhaitons toocreate rapport hello.</span><span class="sxs-lookup"><span data-stu-id="3fefb-127">This should include hello access token, hello embedURL and hello datasetID that we want toocreate hello report against.</span></span> <span data-ttu-id="3fefb-128">Cela requiert l’installation de nuget de hello [Power BI JavaScript package](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/).</span><span class="sxs-lookup"><span data-stu-id="3fefb-128">This requires that you install hello nuget [Power BI JavaScript package](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/).</span></span> <span data-ttu-id="3fefb-129">Hello embedUrl sera simplement https://embedded.powerbi.com/appTokenReportEmbed.</span><span class="sxs-lookup"><span data-stu-id="3fefb-129">hello embedUrl will just be https://embedded.powerbi.com/appTokenReportEmbed.</span></span>

> [!NOTE]
> <span data-ttu-id="3fefb-130">Vous pouvez utiliser hello [incorporer l’exemple de rapport JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/) tootest fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="3fefb-130">You can use hello [JavaScript Report Embed Sample](https://microsoft.github.io/PowerBI-JavaScript/demo/) tootest functionality.</span></span> <span data-ttu-id="3fefb-131">Elle donne également des exemples de code pour hello différentes opérations qui sont disponibles.</span><span class="sxs-lookup"><span data-stu-id="3fefb-131">It also gives code examples for hello different operations that are available.</span></span>

<span data-ttu-id="3fefb-132">**Installation du package NuGet**</span><span class="sxs-lookup"><span data-stu-id="3fefb-132">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.JavaScript
```

<span data-ttu-id="3fefb-133">**Code JavaScript**</span><span class="sxs-lookup"><span data-stu-id="3fefb-133">**JavaScript code**</span></span>

```
<div id="reportContainer"></div>
  
var embedCreateConfiguration = {
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        datasetId: '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
    };
    
    // Grab hello reference toohello div HTML element that will host hello report
    var reportContainer = $('#reportContainer')[0];

    // Create report
    var report = powerbi.createReport(reportContainer, embedCreateConfiguration);
```

<span data-ttu-id="3fefb-134">Appel de *powerbi.createReport()* fera une zone de dessin vide en mode d’édition à apparaître dans hello *div* élément.</span><span class="sxs-lookup"><span data-stu-id="3fefb-134">Calling *powerbi.createReport()* will make a blank canvas in edit mode appear within hello *div* element.</span></span>

![](media/power-bi-embedded-create-report-from-dataset/pbi-embedded-create-new-report.png)

## <a name="save-new-reports"></a><span data-ttu-id="3fefb-135">Enregistrer de nouveaux rapports</span><span class="sxs-lookup"><span data-stu-id="3fefb-135">Save new reports</span></span>

<span data-ttu-id="3fefb-136">rapport de Hello ne sera pas réellement créé jusqu'à ce que vous appeliez hello **enregistrer en tant que** opération.</span><span class="sxs-lookup"><span data-stu-id="3fefb-136">hello report will not actually be created until you call hello **save as** operation.</span></span> <span data-ttu-id="3fefb-137">Vous pouvez le faire dans le menu Fichier ou à partir de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="3fefb-137">This can be done from file menu or from JavaScript.</span></span>

```
 // Get a reference toohello embedded report.
    report = powerbi.get(reportContainer);
    
    var saveAsParameters = {
        name: "newReport"
    };

    // SaveAs report
    report.saveAs(saveAsParameters);
```

> [!IMPORTANT]
> <span data-ttu-id="3fefb-138">Le nouveau rapport n’est créé qu’une fois que l’opération **enregistrer sous** a été appelée.</span><span class="sxs-lookup"><span data-stu-id="3fefb-138">A new report is created only after **save as** is called.</span></span> <span data-ttu-id="3fefb-139">Après avoir enregistré, zone de dessin hello apparaît toujours hello dataset dans le rapport en mode et hello pas d’édition.</span><span class="sxs-lookup"><span data-stu-id="3fefb-139">After you save, hello canvas will still show hello dataset in edit mode and not hello report.</span></span> <span data-ttu-id="3fefb-140">Vous devez rapport hello tooreload comme vous le feriez pour tout autre rapport.</span><span class="sxs-lookup"><span data-stu-id="3fefb-140">You will need tooreload hello new report like you would any other report.</span></span>

![](media/power-bi-embedded-create-report-from-dataset/pbi-embedded-save-new-report.png)

## <a name="load-hello-new-report"></a><span data-ttu-id="3fefb-141">Charge hello nouveau rapport</span><span class="sxs-lookup"><span data-stu-id="3fefb-141">Load hello new report</span></span>

<span data-ttu-id="3fefb-142">Vous devez toointeract d’ordre avec le nouveau rapport de hello tooembed dans hello identique application hello incorpore un rapport régulier, sens, un nouveau jeton doit être émise spécifiquement pour le nouveau rapport de hello, puis appel hello incorporer la méthode.</span><span class="sxs-lookup"><span data-stu-id="3fefb-142">In order toointeract with hello new report you need tooembed it in hello same way hello application embeds a regular report, meaning, a new token must be issued specifically for hello new report and then call hello embed method.</span></span>

```
<div id="reportContainer"></div>
  
var embedConfiguration = {
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MJ',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        reportId: '5dac7a4a-4452-46b3-99f6-a25915e0fe54',
    };
    
    // Grab hello reference toohello div HTML element that will host hello report
    var reportContainer = $('#reportContainer')[0];

    // Embed report
    var report = powerbi.embed(reportContainer, embedConfiguration);
```

## <a name="automate-save-and-load-of-a-new-report-using-hello-saved-event"></a><span data-ttu-id="3fefb-143">Automatisation d’enregistrement et chargement d’un nouveau rapport à l’aide de hello « enregistré » des événements</span><span class="sxs-lookup"><span data-stu-id="3fefb-143">Automate save and load of a new report using hello "saved" event</span></span>

<span data-ttu-id="3fefb-144">Dans le processus de hello tooautomate commande de « Enregistrer sous » et puis en le chargeant hello nouveau rapport que vous pouvez apporter de hello « enregistré » des événements.</span><span class="sxs-lookup"><span data-stu-id="3fefb-144">In order tooautomate hello process of "save as" and then loading hello new report you can make use of hello "saved" Event.</span></span> <span data-ttu-id="3fefb-145">Cet événement est déclenché lorsque hello opération de sauvegarde est terminée et elle retourne un objet Json contenant l’identificateur reportId de nouveau hello, nom du rapport, identificateur reportId ancien de hello (le cas échéant) et si l’opération de hello a saveAs ou sur Enregistrer.</span><span class="sxs-lookup"><span data-stu-id="3fefb-145">This event is fired when hello save operation is complete and it returns a Json object containing hello new reportId, report name, hello old reportId(if there was one) and if hello operation was saveAs or save.</span></span>

```
{
  "reportObjectId": "5dac7a4a-4452-46b3-99f6-a25915e0fe54",
  "reportName": "newReport",
  "saveAs": true,
  "originalReportObjectId": null
}
```

<span data-ttu-id="3fefb-146">tooAutomate hello, des processus que vous pouvez écouter sur l’événement de hello « enregistré », prendre identificateur reportId de nouveau hello créer nouveau jeton de hello et incorporer un nouveau rapport de hello avec lui.</span><span class="sxs-lookup"><span data-stu-id="3fefb-146">tooAutomate hello process you can listen on hello "saved" event, take hello new reportId, create hello new token and embed hello new report with it.</span></span>

```
<div id="reportContainer"></div>
  
var embedCreateConfiguration = {
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        datasetId: '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
    };
    
    // Grab hello reference toohello div HTML element that will host hello report
    var reportContainer = $('#reportContainer')[0];

    // Create report
    var report = powerbi.createReport(reportContainer, embedCreateConfiguration);


   var saveAsParameters = {
        name: "newReport"
    };

    // SaveAs report
    report.saveAs(saveAsParameters);

    // report.on will add an event handler which prints tooLog window.
    report.on("saved", function(event) {
        
         // get new Token
         var newReportId =  event.detail.reportObjectId;

        // create new Token. This is a function that hello application should provide
        var newToken = createAccessToken(newReportId,scopes /*provide hello wanted scopes*/);
        
        
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

## <a name="see-also"></a><span data-ttu-id="3fefb-147">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="3fefb-147">See also</span></span>

[<span data-ttu-id="3fefb-148">Prise en main de l’exemple</span><span class="sxs-lookup"><span data-stu-id="3fefb-148">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="3fefb-149">Enregistrer des rapports</span><span class="sxs-lookup"><span data-stu-id="3fefb-149">Save reports</span></span>](power-bi-embedded-save-reports.md)  
[<span data-ttu-id="3fefb-150">Incorporer un rapport</span><span class="sxs-lookup"><span data-stu-id="3fefb-150">Embed a report</span></span>](power-bi-embedded-embed-report.md)  
[<span data-ttu-id="3fefb-151">Authentification et autorisation dans Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="3fefb-151">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="3fefb-152">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="3fefb-152">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="3fefb-153">Exemple d’incorporation JavaScript</span><span class="sxs-lookup"><span data-stu-id="3fefb-153">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[<span data-ttu-id="3fefb-154">Package NuGet Power BI Core</span><span class="sxs-lookup"><span data-stu-id="3fefb-154">Power BI Core NuGut Package</span></span>](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)  
[<span data-ttu-id="3fefb-155">Package JavaScript Power BI Core</span><span class="sxs-lookup"><span data-stu-id="3fefb-155">Power BI JavaScript package</span></span>](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/)  
<span data-ttu-id="3fefb-156">Des questions ?</span><span class="sxs-lookup"><span data-stu-id="3fefb-156">More questions?</span></span> [<span data-ttu-id="3fefb-157">Essayez de hello Communauté Power BI</span><span class="sxs-lookup"><span data-stu-id="3fefb-157">Try hello Power BI Community</span></span>](http://community.powerbi.com/)
