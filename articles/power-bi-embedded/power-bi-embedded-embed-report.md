---
title: aaaEmbed un rapport dans Azure Power BI Embedded | Documents Microsoft
description: "Découvrez comment tooembed un rapport dans Power BI Embedded dans votre application."
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
ms.openlocfilehash: f25344bbd0b9c092ef19da04d0b455d453b426a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="embed-a-report-in-power-bi-embedded"></a>Incorporer un rapport dans Power BI Embedded

Découvrez comment tooembed un rapport dans Power BI Embedded dans votre application.

Nous allons examiner comment tooactually incorporer un rapport dans votre application. Cela suppose que vous disposiez déjà d’un rapport dans l’un des espaces de travail de votre collection. Si vous n’avez pas encore effectué cette étape, consultez la page [Prise en main de Power BI Embedded](power-bi-embedded-get-started.md).

Vous pouvez utiliser hello .NET (c#) ou le Kit de développement logiciel Node.js, ainsi que de JavaScript, tooeasily générez votre application avec Power BI Embedded. 

## <a name="using-hello-access-keys-toouse-rest-apis"></a>À l’aide de toouse de clés d’accès hello API REST

Bonjour toocall de commande API REST, vous pouvez passer la clé d’accès hello que vous pouvez obtenir à partir de hello portail Azure pour une collection de l’espace de travail donné. Pour plus d’informations, consultez la page [Prise en main de Power BI Embedded](power-bi-embedded-get-started.md).

## <a name="get-a-report-id"></a>Obtenir un ID de rapport

Chaque jeton d’accès est basé sur un rapport. Vous devez hello tooget donné id du rapport pour le rapport hello que vous souhaitez tooembed. Cela est possible en fonction des appels toohello [Get Reports](https://msdn.microsoft.com/library/azure/mt711510.aspx) API REST. Cette méthode retourne l’état hello id et hello incorporent des url. Cela est possible à l’aide de hello Power BI .NET SDK ou appeler directement des API REST de hello.

### <a name="using-hello-power-bi-net-sdk"></a>À l’aide de hello Power BI .NET SDK

Lorsque vous utilisez hello .NET SDK, vous devez toocreate une information d’identification de jeton qui est basée sur la clé d’accès hello que vous obtenez à partir de hello portail Azure. Cela requiert l’installation de hello [package NuGet d’API Power BI](https://www.nuget.org/profiles/powerbi).

**Installation du package NuGet**

```
Install-Package Microsoft.PowerBI.Api
```

**Code C#**

```
using Microsoft.PowerBI.Api.V1;
using Microsoft.Rest;

var credentials = new TokenCredentials("{access key}", "AppKey");
var client = new PowerBIClient(credentials);
client.BaseUri = new Uri(https://api.powerbi.com);

var reports = (IList<Report>)client.Reports.GetReports(workspaceCollectionName, workspaceId).Value;

// Select hello report that you want toowork with from hello collection of reports.
```

### <a name="calling-hello-rest-api-directly"></a>Hello appel API REST directement

```
System.Net.WebRequest request = System.Net.WebRequest.Create("https://api.powerbi.com/v1.0/collections/{collectionName}/workspaces/{workspaceId}/Reports") as System.Net.HttpWebRequest;

request.Method = "GET";
request.ContentLength = 0;
request.Headers.Add("Authorization", String.Format("AppKey {0}", accessToken.Value));

using (var response = request.GetResponse() as System.Net.HttpWebResponse)
{
    using (var reader = new System.IO.StreamReader(response.GetResponseStream()))
    {
        // Work with JSON response tooget hello report you want toowork with.
    }

}
```

## <a name="create-an-access-token"></a>Créer un jeton d’accès

Power BI Embedded utilise des jetons d’incorporation, qui sont des jetons JSON Web Token signés HMAC. les jetons de Hello sont signés avec la clé d’accès hello dans votre collection de l’espace de travail Azure Power BI Embedded. Incorporer des jetons, par défaut, sont utilisé tooprovide lire uniquement accès aux tooa rapport tooembed dans une application. Les jetons d’incorporation sont émis pour un rapport donné et doivent être associés à une URL d’incorporation.

Les jetons d’accès doivent être créés sur le serveur de hello comme clés d’accès hello sont utilisées toosign/chiffrer les jetons hello. Pour plus d’informations sur la façon de toocreate un jeton d’accès, consultez [authentification et autorisation avec Power BI Embedded](power-bi-embedded-app-token-flow.md). Vous pouvez également examiner hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) (méthode). Voici un exemple de ce que cela ressemble à l’aide de hello .NET SDK pour Power BI.

Vous allez utiliser l’id du rapport hello que vous avez récupéré le plus haut. Une fois que hello incorporer jeton est créé, vous allez ensuite utiliser le jeton d’hello hello accès toogenerate clé que vous pouvez utiliser à partir du point de vue hello javascript. Hello *PowerBIToken classe* nécessite que vous installiez hello [Power BI Core NuGut Package](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).

**Installation du package NuGet**

```
Install-Package Microsoft.PowerBI.Core
```

**Code C#**

```
using Microsoft.PowerBI.Security;

// rlsUsername, roles and scopes are optional.
embedToken = PowerBIToken.CreateReportEmbedToken(workspaceCollectionName, workspaceId, reportId, rlsUsername, roles, scopes);

var token = embedToken.Generate("{access key}");
```

### <a name="adding-permission-scopes-tooembed-tokens"></a>Ajout de jetons de tooembed autorisation étendues

Lorsque vous utilisez les jetons incorporé, vous souhaiterez toorestrict de l’utilisation d’hello que vous autoriser à accéder. Dans cette optique, vous pouvez générer un jeton avec des autorisations étendues. Pour plus d’informations, consultez la page [Étendues](power-bi-embedded-app-token-flow.md#scopes).

## <a name="embed-using-javascript"></a>Incorporer avec JavaScript

Une fois que vous avez le jeton d’accès hello et l’id de rapport hello, nous pouvons incorporer des rapports hello à l’aide de JavaScript. Cela requiert l’installation de nuget de hello [Power BI JavaScript package](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/). Hello embedUrl sera simplement https://embedded.powerbi.com/appTokenReportEmbed.

> [!NOTE]
> Vous pouvez utiliser hello [incorporer l’exemple de rapport JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/) tootest fonctionnalité. Elle donne également des exemples de code pour hello différentes opérations qui sont disponibles.

**Installation du package NuGet**

```
Install-Package Microsoft.PowerBI.JavaScript
```

**Code JavaScript**

```
<script src="/scripts/powerbi.js"></script>
<div id="reportContainer"></div>

var embedConfiguration = {
    type: 'report',
    accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
    id: '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
    embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed'
};

var $reportContainer = $('#reportContainer');
var report = powerbi.embed($reportContainer.get(0), embedConfiguration);
```

### <a name="set-hello-size-of-embedded-elements"></a>Définir la taille des éléments incorporés hello

rapport de Hello est incorporé automatiquement en fonction de la taille de hello de son conteneur. taille par défaut toooverride hello hello incorpore simplement ajouter une classe attribut ou inline styles CSS pour la largeur et la hauteur.

## <a name="see-also"></a>Voir aussi

[Prise en main de l’exemple](power-bi-embedded-get-started-sample.md)  
[Authentification et autorisation dans Power BI Embedded](power-bi-embedded-app-token-flow.md)  
[CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[Exemple d’incorporation JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[Package JavaScript Power BI Core](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/)  
[Package NuGet Power BI API](https://www.nuget.org/profiles/powerbi)
[Package NuGet Power BI Core](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)  
[Référentiel Git PowerBI-CSharp](https://github.com/Microsoft/PowerBI-CSharp)  
[Référentiel Git PowerBI-Node](https://github.com/Microsoft/PowerBI-Node)  
Des questions ? [Essayez de hello Communauté Power BI](http://community.powerbi.com/)
