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
# <a name="toggle-between-view-and-edit-mode-for-reports-in-power-bi-embedded"></a>Basculer entre le mode Affichage et le mode Édition pour les rapports dans Power BI Embedded

Découvrez comment tootoggle entre le mode d’affichage et modification de vos rapports dans Power BI Embedded.

## <a name="creating-an-access-token"></a>Créer un jeton d’accès

Vous devez toocreate un jeton d’accès qui vous donne en vue de tooboth possibilité hello et modifier un rapport. tooedit et enregistrer un rapport, vous devrez hello **Report.ReadWrite** jeton d’autorisation. Pour plus d’informations, consultez la page [Authentification et autorisation dans Power BI Embedded](power-bi-embedded-app-token-flow.md).

> [!NOTE]
> Cela vous tooedit et de rapport existant de tooan enregistrer les modifications. Si vous souhaitez également fonction hello de prendre en charge **enregistrer en tant que**, vous devez toosupply des autorisations supplémentaires. Pour plus d’informations, consultez la page [Étendues](power-bi-embedded-app-token-flow.md#scopes).

```
using Microsoft.PowerBI.Security;

// rlsUsername and roles are optional
string scopes = "Report.ReadWrite";
PowerBIToken embedToken = PowerBIToken.CreateReportEmbedTokenForCreation(workspaceCollectionName, workspaceId, datasetId, null, null, scopes);

var token = embedToken.Generate("{access key}");
```

## <a name="embed-configuration"></a>Configuration d’incorporation

Vous devez les autorisations toosupply et un viewMode Bonjour toosee de commande Enregistrer bouton en mode édition. Pour plus d’informations, consultez la page [Détails de la configuration d’incorporation](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details).

Par exemple, dans JavaScript :

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

Cela indique un rapport de hello tooembed en mode d’affichage en fonction **viewMode** définie trop**modèles. ViewMode.View**.

## <a name="view-mode"></a>Mode Affichage

Vous pouvez utiliser hello suivant JavaScript tooswitch en mode d’affichage, si vous êtes en mode édition.

```
// Get a reference toohello embedded report HTML element
var reportContainer = $('#reportContainer')[0];

// Get a reference toohello embedded report.
report = powerbi.get(reportContainer);

// Switch tooview mode.
report.switchMode("view");

```

## <a name="edit-mode"></a>Mode Édition

Vous pouvez utiliser hello suivant JavaScript tooswitch en mode édition, si vous êtes en mode affichage.

```
// Get a reference toohello embedded report HTML element
var reportContainer = $('#reportContainer')[0];

// Get a reference toohello embedded report.
report = powerbi.get(reportContainer);

// Switch tooedit mode.
report.switchMode("edit");

```

## <a name="see-also"></a>Voir aussi

[Prise en main de l’exemple](power-bi-embedded-get-started-sample.md)  
[Incorporer un rapport](power-bi-embedded-embed-report.md)  
[Authentification et autorisation dans Power BI Embedded](power-bi-embedded-app-token-flow.md)  
[CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[Exemple d’incorporation JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[Référentiel Git PowerBI-CSharp](https://github.com/Microsoft/PowerBI-CSharp)  
[Référentiel Git PowerBI-Node](https://github.com/Microsoft/PowerBI-Node)  
Des questions ? [Essayez de hello Communauté Power BI](http://community.powerbi.com/)
