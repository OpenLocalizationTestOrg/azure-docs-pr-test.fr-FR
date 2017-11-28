---
title: rapports aaaSave dans Azure Power BI Embedded | Documents Microsoft
description: "Découvrez comment toosave des rapports dans Power BI incorporé. Cela nécessite des autorisations appropriées dans l’ordre toowork avec succès."
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
ms.openlocfilehash: 984537ce1ce1afc787d6c6c9f61ae8d6226d1171
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="save-reports-in-power-bi-embedded"></a><span data-ttu-id="78d30-104">Enregistrer des rapports dans Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="78d30-104">Save reports in Power BI Embedded</span></span>

<span data-ttu-id="78d30-105">Découvrez comment toosave des rapports dans Power BI incorporé.</span><span class="sxs-lookup"><span data-stu-id="78d30-105">Learn how toosave reports within Power BI embedded.</span></span> <span data-ttu-id="78d30-106">Cela nécessite des autorisations appropriées dans l’ordre toowork avec succès.</span><span class="sxs-lookup"><span data-stu-id="78d30-106">This requires proper permissions in order toowork successfully.</span></span>

<span data-ttu-id="78d30-107">Dans Power BI Embedded, vous pouvez modifier des rapports existants et les enregistrer.</span><span class="sxs-lookup"><span data-stu-id="78d30-107">Within Power BI Embedded, you can edit existing reports and save them.</span></span> <span data-ttu-id="78d30-108">Vous pouvez également créer un nouveau rapport et l’enregistrer en tant qu’un nouveau toocreate de rapport une.</span><span class="sxs-lookup"><span data-stu-id="78d30-108">You can also create a new report and save as a new report toocreate one.</span></span>

<span data-ttu-id="78d30-109">Dans l’ordre toosave un rapport, vous devez tout d’abord toocreate un jeton de rapport avec des étendues de droite hello hello :</span><span class="sxs-lookup"><span data-stu-id="78d30-109">In order toosave a report you first need toocreate a token for hello specific report with hello right scopes:</span></span>

* <span data-ttu-id="78d30-110">tooenable enregistrer Report.ReadWrite étendue est requise</span><span class="sxs-lookup"><span data-stu-id="78d30-110">tooenable save Report.ReadWrite scope is required</span></span>
* <span data-ttu-id="78d30-111">tooenable enregistrer en tant que, Report.Read et Workspace.Report.Copy étendues sont requis</span><span class="sxs-lookup"><span data-stu-id="78d30-111">tooenable save as, Report.Read and Workspace.Report.Copy scopes are required</span></span>
* <span data-ttu-id="78d30-112">tooenable enregistrer et enregistrer sous, Report.ReadWrite et Workspace.Report.Copy requierd</span><span class="sxs-lookup"><span data-stu-id="78d30-112">tooenable save and save as, Report.ReadWrite and Workspace.Report.Copy are requierd</span></span>

<span data-ttu-id="78d30-113">Respectivement Bonjour de tooenable commande droit enregistrer/enregistrer que des boutons dans le menu fichier, vous devez tooprovide hello avec le bouton droit autorisation dans la configuration d’incorporer hello lorsque vous Embed hello rapport :</span><span class="sxs-lookup"><span data-stu-id="78d30-113">Respectively in order tooenable hello right save/save as buttons in file menu you need tooprovide hello right permission in hello Embed configuration when you Embed hello report:</span></span>

* <span data-ttu-id="78d30-114">models.Permissions.ReadWrite</span><span class="sxs-lookup"><span data-stu-id="78d30-114">models.Permissions.ReadWrite</span></span>
* <span data-ttu-id="78d30-115">models.Permissions.Copy</span><span class="sxs-lookup"><span data-stu-id="78d30-115">models.Permissions.Copy</span></span>
* <span data-ttu-id="78d30-116">models.Permissions.All</span><span class="sxs-lookup"><span data-stu-id="78d30-116">models.Permissions.All</span></span>

> [!NOTE]
> <span data-ttu-id="78d30-117">Votre jeton d’accès doit également les étendues appropriées hello.</span><span class="sxs-lookup"><span data-stu-id="78d30-117">Your access token also needs hello appropriate scopes.</span></span> <span data-ttu-id="78d30-118">Pour plus d’informations, consultez la page [Étendues](power-bi-embedded-app-token-flow.md#scopes).</span><span class="sxs-lookup"><span data-stu-id="78d30-118">For more information, see [Scopes](power-bi-embedded-app-token-flow.md#scopes).</span></span>

## <a name="embed-report-in-edit-mode"></a><span data-ttu-id="78d30-119">Incorporer un rapport en mode Édition</span><span class="sxs-lookup"><span data-stu-id="78d30-119">Embed report in edit mode</span></span>

<span data-ttu-id="78d30-120">Supposons que vous vouliez tooEmbed un rapport en mode d’édition à l’intérieur de votre application, toodo simplement passer des propriétés du droit de hello dans la configuration de l’incorporation d’appeler powerbi.embed().</span><span class="sxs-lookup"><span data-stu-id="78d30-120">Let's say you want tooEmbed a report in edit mode inside your app, toodo so just pass hello right properties in Embed configuration and call powerbi.embed().</span></span> <span data-ttu-id="78d30-121">Vous devez les autorisations toosupply et un viewMode Bonjour de toosee commande Enregistrer et enregistrer sous forme de boutons en mode édition.</span><span class="sxs-lookup"><span data-stu-id="78d30-121">You will need toosupply permissions and a viewMode in order toosee hello save and save as buttons when in edit mode.</span></span> <span data-ttu-id="78d30-122">Pour plus d’informations, consultez la page [Détails de la configuration d’incorporation](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details).</span><span class="sxs-lookup"><span data-stu-id="78d30-122">For more information, see [Embed configuration details](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details).</span></span>

<span data-ttu-id="78d30-123">Par exemple, dans JavaScript :</span><span class="sxs-lookup"><span data-stu-id="78d30-123">For example in JavaScript:</span></span>

```
   <div id="reportContainer"></div>

    // Get models. Models, it contains enums that can be used.
    var models = window['powerbi-client'].models;

    // Embed configuration used toodescribe hello what and how tooembed.
    // This object is used when calling powerbi.embed.
    // This also includes settings and options such as filters.
    // You can find more information at https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details.
    var config= {
        type: 'report',
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        id:  '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
        permissions: models.Permissions.All /*both save & save as buttons will be visible*/,
        viewMode: models.ViewMode.Edit,
        settings: {
            filterPaneEnabled: true,
            navContentPaneEnabled: true
        }
    };

    // Get a reference toohello embedded report HTML element
    var reportContainer = $('#reportContainer')[0];

    // Embed hello report and display it within hello div container.
    var report = powerbi.embed(reportContainer, config);
```

<span data-ttu-id="78d30-124">Un rapport sera alors incorporé dans votre application en mode Édition.</span><span class="sxs-lookup"><span data-stu-id="78d30-124">Now a report will be embedded in your app in edit mode.</span></span>

## <a name="save-report"></a><span data-ttu-id="78d30-125">Enregistrer le rapport</span><span class="sxs-lookup"><span data-stu-id="78d30-125">Save report</span></span>

<span data-ttu-id="78d30-126">Une fois le rapport de hello Embbeding dans modifier le mode avec hello à droite de jeton et les autorisations, vous pouvez enregistrer les rapports hello à partir du menu fichier de hello ou à partir de javascript :</span><span class="sxs-lookup"><span data-stu-id="78d30-126">After Embbeding hello report in edit mode with hello right token and permissions you can save hello report from hello file menu or from javascript:</span></span>

```
 // Get a reference toohello embedded report.
    report = powerbi.get(reportContainer);

 // Save report
    report.save();
```

## <a name="save-as"></a><span data-ttu-id="78d30-127">Enregistrer sous</span><span class="sxs-lookup"><span data-stu-id="78d30-127">Save as</span></span>

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
> <span data-ttu-id="78d30-128">Le nouveau rapport n’est créé qu’après l’opération *enregistrer sous*.</span><span class="sxs-lookup"><span data-stu-id="78d30-128">Only after *save as* is a new report created.</span></span> <span data-ttu-id="78d30-129">Après hello enregistré, zone de dessin hello affiche toujours les rapports ancien hello dans modifier le mode et pas hello nouveau rapport.</span><span class="sxs-lookup"><span data-stu-id="78d30-129">After hello save, hello canvas is still showing hello old report in edit mode and not hello new report.</span></span> <span data-ttu-id="78d30-130">Vous devez tooembed hello nouveau rapport qui a été créé.</span><span class="sxs-lookup"><span data-stu-id="78d30-130">You will need tooembed hello new report that was created.</span></span> <span data-ttu-id="78d30-131">Cela nécessite un nouveau jeton d’accès, car ils sont créés rapport par rapport.</span><span class="sxs-lookup"><span data-stu-id="78d30-131">This requires a new access token as they are created per report.</span></span>

<span data-ttu-id="78d30-132">Vous devez ensuite tooload hello nouveau rapport après un *enregistrer en tant que*.</span><span class="sxs-lookup"><span data-stu-id="78d30-132">You will then need tooload hello new report after a *save as*.</span></span> <span data-ttu-id="78d30-133">Cela est similaire tooembedding n’importe quel rapport.</span><span class="sxs-lookup"><span data-stu-id="78d30-133">This is similar tooembedding any report.</span></span>

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

## <a name="see-also"></a><span data-ttu-id="78d30-134">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="78d30-134">See also</span></span>

[<span data-ttu-id="78d30-135">Prise en main de l’exemple</span><span class="sxs-lookup"><span data-stu-id="78d30-135">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="78d30-136">Incorporer un rapport</span><span class="sxs-lookup"><span data-stu-id="78d30-136">Embed a report</span></span>](power-bi-embedded-embed-report.md)  
[<span data-ttu-id="78d30-137">Créer un rapport à partir d’un jeu de données</span><span class="sxs-lookup"><span data-stu-id="78d30-137">Create a new report from a dataset</span></span>](power-bi-embedded-create-report-from-dataset.md)  
[<span data-ttu-id="78d30-138">Authentification et autorisation dans Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="78d30-138">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="78d30-139">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="78d30-139">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="78d30-140">Exemple d’incorporation JavaScript</span><span class="sxs-lookup"><span data-stu-id="78d30-140">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
<span data-ttu-id="78d30-141">Des questions ?</span><span class="sxs-lookup"><span data-stu-id="78d30-141">More questions?</span></span> [<span data-ttu-id="78d30-142">Essayez de hello Communauté Power BI</span><span class="sxs-lookup"><span data-stu-id="78d30-142">Try hello Power BI Community</span></span>](http://community.powerbi.com/)

