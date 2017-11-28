---
title: "aaaToggle entre les modes d’affichage et modification des rapports dans Azure Power BI Embedded | Documents Microsoft"
description: "Découvrez comment tootoggle entre le mode d’affichage et modification de vos rapports dans Power BI Embedded."
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
ms.openlocfilehash: c9e3da5f9ae74d221af650adebde7c9d83b38a99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="toggle-between-view-and-edit-mode-for-reports-in-power-bi-embedded"></a><span data-ttu-id="55326-103">Basculer entre le mode Affichage et le mode Édition pour les rapports dans Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="55326-103">Toggle between view and edit mode for reports in Power BI Embedded</span></span>

<span data-ttu-id="55326-104">Découvrez comment tootoggle entre le mode d’affichage et modification de vos rapports dans Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="55326-104">Learn how tootoggle between view and edit mode for your reports within Power BI Embedded.</span></span>

## <a name="creating-an-access-token"></a><span data-ttu-id="55326-105">Créer un jeton d’accès</span><span class="sxs-lookup"><span data-stu-id="55326-105">Creating an access token</span></span>

<span data-ttu-id="55326-106">Vous devez toocreate un jeton d’accès qui vous donne en vue de tooboth possibilité hello et modifier un rapport.</span><span class="sxs-lookup"><span data-stu-id="55326-106">You will need toocreate an access token that gives you hello ability tooboth view and edit a report.</span></span> <span data-ttu-id="55326-107">tooedit et enregistrer un rapport, vous devrez hello **Report.ReadWrite** jeton d’autorisation.</span><span class="sxs-lookup"><span data-stu-id="55326-107">tooedit and save a report, you will need hello **Report.ReadWrite** token permission.</span></span> <span data-ttu-id="55326-108">Pour plus d’informations, consultez la page [Authentification et autorisation dans Power BI Embedded](power-bi-embedded-app-token-flow.md).</span><span class="sxs-lookup"><span data-stu-id="55326-108">For more information, see [Authenticating and authorizing in Power BI Embedded](power-bi-embedded-app-token-flow.md).</span></span>

> [!NOTE]
> <span data-ttu-id="55326-109">Cela vous tooedit et de rapport existant de tooan enregistrer les modifications.</span><span class="sxs-lookup"><span data-stu-id="55326-109">This will allow you tooedit and save changes tooan existing report.</span></span> <span data-ttu-id="55326-110">Si vous souhaitez également fonction hello de prendre en charge **enregistrer en tant que**, vous devez toosupply des autorisations supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="55326-110">If you would also like hello function of supporting **Save As**, you will need toosupply additional permissions.</span></span> <span data-ttu-id="55326-111">Pour plus d’informations, consultez la page [Étendues](power-bi-embedded-app-token-flow.md#scopes).</span><span class="sxs-lookup"><span data-stu-id="55326-111">For more information, see [Scopes](power-bi-embedded-app-token-flow.md#scopes).</span></span>

```
using Microsoft.PowerBI.Security;

// rlsUsername and roles are optional
string scopes = "Report.ReadWrite";
PowerBIToken embedToken = PowerBIToken.CreateReportEmbedTokenForCreation(workspaceCollectionName, workspaceId, datasetId, null, null, scopes);

var token = embedToken.Generate("{access key}");
```

## <a name="embed-configuration"></a><span data-ttu-id="55326-112">Configuration d’incorporation</span><span class="sxs-lookup"><span data-stu-id="55326-112">Embed configuration</span></span>

<span data-ttu-id="55326-113">Vous devez les autorisations toosupply et un viewMode Bonjour toosee de commande Enregistrer bouton en mode édition.</span><span class="sxs-lookup"><span data-stu-id="55326-113">You will need toosupply permissions and a viewMode in order toosee hello save button when in edit mode.</span></span> <span data-ttu-id="55326-114">Pour plus d’informations, consultez la page [Détails de la configuration d’incorporation](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details).</span><span class="sxs-lookup"><span data-stu-id="55326-114">For more information, see [Embed configuration details](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details).</span></span>

<span data-ttu-id="55326-115">Par exemple, dans JavaScript :</span><span class="sxs-lookup"><span data-stu-id="55326-115">For example in JavaScript:</span></span>

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
        permissions: models.Permissions.ReadWrite /*both save & save as buttons will be visible*/,
        viewMode: models.ViewMode.View,
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

<span data-ttu-id="55326-116">Cela indique un rapport de hello tooembed en mode d’affichage en fonction **viewMode** définie trop**modèles. ViewMode.View**.</span><span class="sxs-lookup"><span data-stu-id="55326-116">This will indicate tooembed hello report in view mode based on **viewMode** being set too**models.ViewMode.View**.</span></span>

## <a name="view-mode"></a><span data-ttu-id="55326-117">Mode Affichage</span><span class="sxs-lookup"><span data-stu-id="55326-117">View mode</span></span>

<span data-ttu-id="55326-118">Vous pouvez utiliser hello suivant JavaScript tooswitch en mode d’affichage, si vous êtes en mode édition.</span><span class="sxs-lookup"><span data-stu-id="55326-118">You can use hello following JavaScript tooswitch into view mode, if you are in edit mode.</span></span>

```
// Get a reference toohello embedded report HTML element
var reportContainer = $('#reportContainer')[0];

// Get a reference toohello embedded report.
report = powerbi.get(reportContainer);

// Switch tooview mode.
report.switchMode("view");

```

## <a name="edit-mode"></a><span data-ttu-id="55326-119">Mode Édition</span><span class="sxs-lookup"><span data-stu-id="55326-119">Edit mode</span></span>

<span data-ttu-id="55326-120">Vous pouvez utiliser hello suivant JavaScript tooswitch en mode édition, si vous êtes en mode affichage.</span><span class="sxs-lookup"><span data-stu-id="55326-120">You can use hello following JavaScript tooswitch into edit mode, if you are in view mode.</span></span>

```
// Get a reference toohello embedded report HTML element
var reportContainer = $('#reportContainer')[0];

// Get a reference toohello embedded report.
report = powerbi.get(reportContainer);

// Switch tooedit mode.
report.switchMode("edit");

```

## <a name="see-also"></a><span data-ttu-id="55326-121">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="55326-121">See also</span></span>

[<span data-ttu-id="55326-122">Prise en main de l’exemple</span><span class="sxs-lookup"><span data-stu-id="55326-122">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="55326-123">Incorporer un rapport</span><span class="sxs-lookup"><span data-stu-id="55326-123">Embed a report</span></span>](power-bi-embedded-embed-report.md)  
[<span data-ttu-id="55326-124">Authentification et autorisation dans Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="55326-124">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="55326-125">CreateReportEmbedToken</span><span class="sxs-lookup"><span data-stu-id="55326-125">CreateReportEmbedToken</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[<span data-ttu-id="55326-126">Exemple d’incorporation JavaScript</span><span class="sxs-lookup"><span data-stu-id="55326-126">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[<span data-ttu-id="55326-127">Référentiel Git PowerBI-CSharp</span><span class="sxs-lookup"><span data-stu-id="55326-127">PowerBI-CSharp Git Repo</span></span>](https://github.com/Microsoft/PowerBI-CSharp)  
[<span data-ttu-id="55326-128">Référentiel Git PowerBI-Node</span><span class="sxs-lookup"><span data-stu-id="55326-128">PowerBI-Node Git Repo</span></span>](https://github.com/Microsoft/PowerBI-Node)  
<span data-ttu-id="55326-129">Des questions ?</span><span class="sxs-lookup"><span data-stu-id="55326-129">More questions?</span></span> [<span data-ttu-id="55326-130">Essayez de hello Communauté Power BI</span><span class="sxs-lookup"><span data-stu-id="55326-130">Try hello Power BI Community</span></span>](http://community.powerbi.com/)
