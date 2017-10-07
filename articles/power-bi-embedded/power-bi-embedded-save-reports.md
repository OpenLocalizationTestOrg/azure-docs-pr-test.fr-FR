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
# <a name="save-reports-in-power-bi-embedded"></a>Enregistrer des rapports dans Power BI Embedded

Découvrez comment toosave des rapports dans Power BI incorporé. Cela nécessite des autorisations appropriées dans l’ordre toowork avec succès.

Dans Power BI Embedded, vous pouvez modifier des rapports existants et les enregistrer. Vous pouvez également créer un nouveau rapport et l’enregistrer en tant qu’un nouveau toocreate de rapport une.

Dans l’ordre toosave un rapport, vous devez tout d’abord toocreate un jeton de rapport avec des étendues de droite hello hello :

* tooenable enregistrer Report.ReadWrite étendue est requise
* tooenable enregistrer en tant que, Report.Read et Workspace.Report.Copy étendues sont requis
* tooenable enregistrer et enregistrer sous, Report.ReadWrite et Workspace.Report.Copy requierd

Respectivement Bonjour de tooenable commande droit enregistrer/enregistrer que des boutons dans le menu fichier, vous devez tooprovide hello avec le bouton droit autorisation dans la configuration d’incorporer hello lorsque vous Embed hello rapport :

* models.Permissions.ReadWrite
* models.Permissions.Copy
* models.Permissions.All

> [!NOTE]
> Votre jeton d’accès doit également les étendues appropriées hello. Pour plus d’informations, consultez la page [Étendues](power-bi-embedded-app-token-flow.md#scopes).

## <a name="embed-report-in-edit-mode"></a>Incorporer un rapport en mode Édition

Supposons que vous vouliez tooEmbed un rapport en mode d’édition à l’intérieur de votre application, toodo simplement passer des propriétés du droit de hello dans la configuration de l’incorporation d’appeler powerbi.embed(). Vous devez les autorisations toosupply et un viewMode Bonjour de toosee commande Enregistrer et enregistrer sous forme de boutons en mode édition. Pour plus d’informations, consultez la page [Détails de la configuration d’incorporation](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details).

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

Un rapport sera alors incorporé dans votre application en mode Édition.

## <a name="save-report"></a>Enregistrer le rapport

Une fois le rapport de hello Embbeding dans modifier le mode avec hello à droite de jeton et les autorisations, vous pouvez enregistrer les rapports hello à partir du menu fichier de hello ou à partir de javascript :

```
 // Get a reference toohello embedded report.
    report = powerbi.get(reportContainer);

 // Save report
    report.save();
```

## <a name="save-as"></a>Enregistrer sous

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
> Le nouveau rapport n’est créé qu’après l’opération *enregistrer sous*. Après hello enregistré, zone de dessin hello affiche toujours les rapports ancien hello dans modifier le mode et pas hello nouveau rapport. Vous devez tooembed hello nouveau rapport qui a été créé. Cela nécessite un nouveau jeton d’accès, car ils sont créés rapport par rapport.

Vous devez ensuite tooload hello nouveau rapport après un *enregistrer en tant que*. Cela est similaire tooembedding n’importe quel rapport.

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

## <a name="see-also"></a>Voir aussi

[Prise en main de l’exemple](power-bi-embedded-get-started-sample.md)  
[Incorporer un rapport](power-bi-embedded-embed-report.md)  
[Créer un rapport à partir d’un jeu de données](power-bi-embedded-create-report-from-dataset.md)  
[Authentification et autorisation dans Power BI Embedded](power-bi-embedded-app-token-flow.md)  
[Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[Exemple d’incorporation JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
Des questions ? [Essayez de hello Communauté Power BI](http://community.powerbi.com/)

