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
# <a name="create-a-new-report-from-a-dataset-in-power-bi-embedded"></a>Créer un rapport à partir d’un jeu de données dans Power BI Embedded

Il vous est à présent possible de créer des rapports Power BI Embedded à partir d’un jeu de données dans votre propre application. 

Hello méthode d’authentification est similaire incorporer des toothat du rapport. Il est basé sur les jetons d’accès qui sont le jeu de données tooa spécifique. Les jetons utilisés pour PowerBI.com sont émis par Azure Active Directory (AAD), et les jetons Power BI Embedded par votre propre service.

Lorsque vous createing un rapport incorporé, hello jetons émis sont pour un jeu de données spécifique. Les jetons doivent être associées avec hello incorporer des URL sur hello même élément tooensure chaque a un jeton unique. Dans commande toocreate un rapport incorporé, *Dataset.Read et Workspace.Report.Create* étendues doivent être fournis dans le jeton d’accès hello.

## <a name="create-access-token-needed-toocreate-new-report"></a>Créer rapport accès jeton toocreate nécessaires

Power BI Embedded utilise des jetons d’incorporation, qui sont des jetons JSON Web Token signés HMAC. les jetons de Hello sont signés avec la clé d’accès hello dans votre collection de l’espace de travail Azure Power BI Embedded. Incorporer des jetons, par défaut, sont utilisé tooprovide lire uniquement accès aux tooa rapport tooembed dans une application. Les jetons d’incorporation sont émis pour un rapport donné et doivent être associés à une URL d’incorporation.

Les jetons d’accès doivent être créés sur le serveur de hello comme clés d’accès hello sont utilisées toosign/chiffrer les jetons hello. Pour plus d’informations sur la façon de toocreate un jeton d’accès, consultez [authentification et autorisation avec Power BI Embedded](power-bi-embedded-app-token-flow.md). Vous pouvez également examiner hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) (méthode). Voici un exemple de ce que cela ressemble à l’aide de hello .NET SDK pour Power BI.

Dans cet exemple, nous avons notre id de jeu de données que nous souhaitons rapport toocreat hello sur. Nous devons également des étendues de hello tooadd pour *Dataset.Read et Workspace.Report.Create*.

Hello *PowerBIToken classe* nécessite que vous installiez hello [Power BI Core NuGut Package](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).

**Installation du package NuGet**

```
Install-Package Microsoft.PowerBI.Core
```

**Code C#**

```
using Microsoft.PowerBI.Security;

// rlsUsername and roles are optional
string scopes = "Dataset.Read Workspace.Report.Create";
PowerBIToken embedToken = PowerBIToken.CreateReportEmbedTokenForCreation(workspaceCollectionName, workspaceId, datasetId, null, null, scopes);

var token = embedToken.Generate("{access key}");
```

## <a name="create-a-new-blank-report"></a>Créer un rapport vide

Dans l’ordre toocreate un nouveau rapport, créez hello configuration doit être fournie. Cela doit inclure le jeton d’accès hello, hello embedURL et hello datasetID que nous souhaitons toocreate rapport hello. Cela requiert l’installation de nuget de hello [Power BI JavaScript package](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/). Hello embedUrl sera simplement https://embedded.powerbi.com/appTokenReportEmbed.

> [!NOTE]
> Vous pouvez utiliser hello [incorporer l’exemple de rapport JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/) tootest fonctionnalité. Elle donne également des exemples de code pour hello différentes opérations qui sont disponibles.

**Installation du package NuGet**

```
Install-Package Microsoft.PowerBI.JavaScript
```

**Code JavaScript**

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

Appel de *powerbi.createReport()* fera une zone de dessin vide en mode d’édition à apparaître dans hello *div* élément.

![](media/power-bi-embedded-create-report-from-dataset/pbi-embedded-create-new-report.png)

## <a name="save-new-reports"></a>Enregistrer de nouveaux rapports

rapport de Hello ne sera pas réellement créé jusqu'à ce que vous appeliez hello **enregistrer en tant que** opération. Vous pouvez le faire dans le menu Fichier ou à partir de JavaScript.

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
> Le nouveau rapport n’est créé qu’une fois que l’opération **enregistrer sous** a été appelée. Après avoir enregistré, zone de dessin hello apparaît toujours hello dataset dans le rapport en mode et hello pas d’édition. Vous devez rapport hello tooreload comme vous le feriez pour tout autre rapport.

![](media/power-bi-embedded-create-report-from-dataset/pbi-embedded-save-new-report.png)

## <a name="load-hello-new-report"></a>Charge hello nouveau rapport

Vous devez toointeract d’ordre avec le nouveau rapport de hello tooembed dans hello identique application hello incorpore un rapport régulier, sens, un nouveau jeton doit être émise spécifiquement pour le nouveau rapport de hello, puis appel hello incorporer la méthode.

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

## <a name="automate-save-and-load-of-a-new-report-using-hello-saved-event"></a>Automatisation d’enregistrement et chargement d’un nouveau rapport à l’aide de hello « enregistré » des événements

Dans le processus de hello tooautomate commande de « Enregistrer sous » et puis en le chargeant hello nouveau rapport que vous pouvez apporter de hello « enregistré » des événements. Cet événement est déclenché lorsque hello opération de sauvegarde est terminée et elle retourne un objet Json contenant l’identificateur reportId de nouveau hello, nom du rapport, identificateur reportId ancien de hello (le cas échéant) et si l’opération de hello a saveAs ou sur Enregistrer.

```
{
  "reportObjectId": "5dac7a4a-4452-46b3-99f6-a25915e0fe54",
  "reportName": "newReport",
  "saveAs": true,
  "originalReportObjectId": null
}
```

tooAutomate hello, des processus que vous pouvez écouter sur l’événement de hello « enregistré », prendre identificateur reportId de nouveau hello créer nouveau jeton de hello et incorporer un nouveau rapport de hello avec lui.

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

## <a name="see-also"></a>Voir aussi

[Prise en main de l’exemple](power-bi-embedded-get-started-sample.md)  
[Enregistrer des rapports](power-bi-embedded-save-reports.md)  
[Incorporer un rapport](power-bi-embedded-embed-report.md)  
[Authentification et autorisation dans Power BI Embedded](power-bi-embedded-app-token-flow.md)  
[Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[Exemple d’incorporation JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[Package NuGet Power BI Core](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)  
[Package JavaScript Power BI Core](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/)  
Des questions ? [Essayez de hello Communauté Power BI](http://community.powerbi.com/)
