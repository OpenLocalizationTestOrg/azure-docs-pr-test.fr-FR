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
# <a name="embed-a-report-in-power-bi-embedded"></a><span data-ttu-id="ff976-103">Incorporer un rapport dans Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="ff976-103">Embed a report in Power BI Embedded</span></span>

<span data-ttu-id="ff976-104">Découvrez comment tooembed un rapport dans Power BI Embedded dans votre application.</span><span class="sxs-lookup"><span data-stu-id="ff976-104">Learn how tooembed a report that is in Power BI Embedded into your application.</span></span>

<span data-ttu-id="ff976-105">Nous allons examiner comment tooactually incorporer un rapport dans votre application.</span><span class="sxs-lookup"><span data-stu-id="ff976-105">We will look at how tooactually embed a report into your application.</span></span> <span data-ttu-id="ff976-106">Cela suppose que vous disposiez déjà d’un rapport dans l’un des espaces de travail de votre collection.</span><span class="sxs-lookup"><span data-stu-id="ff976-106">This is assuming you already have a report that exists within a workspace in your workspace collection.</span></span> <span data-ttu-id="ff976-107">Si vous n’avez pas encore effectué cette étape, consultez la page [Prise en main de Power BI Embedded](power-bi-embedded-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ff976-107">If you haven't done that step yet, see [Get started with Power BI Embedded](power-bi-embedded-get-started.md).</span></span>

<span data-ttu-id="ff976-108">Vous pouvez utiliser hello .NET (c#) ou le Kit de développement logiciel Node.js, ainsi que de JavaScript, tooeasily générez votre application avec Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="ff976-108">You can use hello .NET (C#) or Node.js SDK, along with JavaScript, tooeasily build your application with Power BI Embedded.</span></span> 

## <a name="using-hello-access-keys-toouse-rest-apis"></a><span data-ttu-id="ff976-109">À l’aide de toouse de clés d’accès hello API REST</span><span class="sxs-lookup"><span data-stu-id="ff976-109">Using hello access keys toouse REST APIs</span></span>

<span data-ttu-id="ff976-110">Bonjour toocall de commande API REST, vous pouvez passer la clé d’accès hello que vous pouvez obtenir à partir de hello portail Azure pour une collection de l’espace de travail donné.</span><span class="sxs-lookup"><span data-stu-id="ff976-110">In order toocall hello REST API, you can pass hello access key which you can get from hello Azure portal for a given workspace collection.</span></span> <span data-ttu-id="ff976-111">Pour plus d’informations, consultez la page [Prise en main de Power BI Embedded](power-bi-embedded-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ff976-111">For more information, see [Get started with Power BI Embedded](power-bi-embedded-get-started.md).</span></span>

## <a name="get-a-report-id"></a><span data-ttu-id="ff976-112">Obtenir un ID de rapport</span><span class="sxs-lookup"><span data-stu-id="ff976-112">Get a report id</span></span>

<span data-ttu-id="ff976-113">Chaque jeton d’accès est basé sur un rapport.</span><span class="sxs-lookup"><span data-stu-id="ff976-113">Every access token is based on a report.</span></span> <span data-ttu-id="ff976-114">Vous devez hello tooget donné id du rapport pour le rapport hello que vous souhaitez tooembed.</span><span class="sxs-lookup"><span data-stu-id="ff976-114">You will need tooget hello given report id for hello report that you want tooembed.</span></span> <span data-ttu-id="ff976-115">Cela est possible en fonction des appels toohello [Get Reports](https://msdn.microsoft.com/library/azure/mt711510.aspx) API REST.</span><span class="sxs-lookup"><span data-stu-id="ff976-115">This can be done based on calls toohello [Get Reports](https://msdn.microsoft.com/library/azure/mt711510.aspx) REST API.</span></span> <span data-ttu-id="ff976-116">Cette méthode retourne l’état hello id et hello incorporent des url.</span><span class="sxs-lookup"><span data-stu-id="ff976-116">This will return hello report id and hello embed url.</span></span> <span data-ttu-id="ff976-117">Cela est possible à l’aide de hello Power BI .NET SDK ou appeler directement des API REST de hello.</span><span class="sxs-lookup"><span data-stu-id="ff976-117">This can be done using hello Power BI .NET SDK or calling hello REST API directly.</span></span>

### <a name="using-hello-power-bi-net-sdk"></a><span data-ttu-id="ff976-118">À l’aide de hello Power BI .NET SDK</span><span class="sxs-lookup"><span data-stu-id="ff976-118">Using hello Power BI .NET SDK</span></span>

<span data-ttu-id="ff976-119">Lorsque vous utilisez hello .NET SDK, vous devez toocreate une information d’identification de jeton qui est basée sur la clé d’accès hello que vous obtenez à partir de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="ff976-119">When using hello .NET SDK, you will need toocreate a token credential which is based on hello access key you get from hello Azure portal.</span></span> <span data-ttu-id="ff976-120">Cela requiert l’installation de hello [package NuGet d’API Power BI](https://www.nuget.org/profiles/powerbi).</span><span class="sxs-lookup"><span data-stu-id="ff976-120">This requires that you install hello [Power BI API NuGet package](https://www.nuget.org/profiles/powerbi).</span></span>

<span data-ttu-id="ff976-121">**Installation du package NuGet**</span><span class="sxs-lookup"><span data-stu-id="ff976-121">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.Api
```

<span data-ttu-id="ff976-122">**Code C#**</span><span class="sxs-lookup"><span data-stu-id="ff976-122">**C# code**</span></span>

```
using Microsoft.PowerBI.Api.V1;
using Microsoft.Rest;

var credentials = new TokenCredentials("{access key}", "AppKey");
var client = new PowerBIClient(credentials);
client.BaseUri = new Uri(https://api.powerbi.com);

var reports = (IList<Report>)client.Reports.GetReports(workspaceCollectionName, workspaceId).Value;

// Select hello report that you want toowork with from hello collection of reports.
```

### <a name="calling-hello-rest-api-directly"></a><span data-ttu-id="ff976-123">Hello appel API REST directement</span><span class="sxs-lookup"><span data-stu-id="ff976-123">Calling hello REST API directly</span></span>

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

## <a name="create-an-access-token"></a><span data-ttu-id="ff976-124">Créer un jeton d’accès</span><span class="sxs-lookup"><span data-stu-id="ff976-124">Create an access token</span></span>

<span data-ttu-id="ff976-125">Power BI Embedded utilise des jetons d’incorporation, qui sont des jetons JSON Web Token signés HMAC.</span><span class="sxs-lookup"><span data-stu-id="ff976-125">Power BI Embedded uses embed token, which are HMAC signed JSON Web Tokens.</span></span> <span data-ttu-id="ff976-126">les jetons de Hello sont signés avec la clé d’accès hello dans votre collection de l’espace de travail Azure Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="ff976-126">hello tokens are signed with hello access key from your Azure Power BI Embedded workspace collection.</span></span> <span data-ttu-id="ff976-127">Incorporer des jetons, par défaut, sont utilisé tooprovide lire uniquement accès aux tooa rapport tooembed dans une application.</span><span class="sxs-lookup"><span data-stu-id="ff976-127">Embed tokens, by default, are used tooprovide read only access tooa report tooembed into an application.</span></span> <span data-ttu-id="ff976-128">Les jetons d’incorporation sont émis pour un rapport donné et doivent être associés à une URL d’incorporation.</span><span class="sxs-lookup"><span data-stu-id="ff976-128">Embed tokens are issued for a specific report and should be associated with an embed URL.</span></span>

<span data-ttu-id="ff976-129">Les jetons d’accès doivent être créés sur le serveur de hello comme clés d’accès hello sont utilisées toosign/chiffrer les jetons hello.</span><span class="sxs-lookup"><span data-stu-id="ff976-129">Access tokens should be created on hello server as hello access keys are used toosign/encrypt hello tokens.</span></span> <span data-ttu-id="ff976-130">Pour plus d’informations sur la façon de toocreate un jeton d’accès, consultez [authentification et autorisation avec Power BI Embedded](power-bi-embedded-app-token-flow.md).</span><span class="sxs-lookup"><span data-stu-id="ff976-130">For information on how toocreate an access token, see [Authenticating and authorizing with Power BI Embedded](power-bi-embedded-app-token-flow.md).</span></span> <span data-ttu-id="ff976-131">Vous pouvez également examiner hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) (méthode).</span><span class="sxs-lookup"><span data-stu-id="ff976-131">You can also review hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) method.</span></span> <span data-ttu-id="ff976-132">Voici un exemple de ce que cela ressemble à l’aide de hello .NET SDK pour Power BI.</span><span class="sxs-lookup"><span data-stu-id="ff976-132">Here is an example of what this would look like using hello .NET SDK for Power BI.</span></span>

<span data-ttu-id="ff976-133">Vous allez utiliser l’id du rapport hello que vous avez récupéré le plus haut.</span><span class="sxs-lookup"><span data-stu-id="ff976-133">You will use hello report id that you retrieved earlier.</span></span> <span data-ttu-id="ff976-134">Une fois que hello incorporer jeton est créé, vous allez ensuite utiliser le jeton d’hello hello accès toogenerate clé que vous pouvez utiliser à partir du point de vue hello javascript.</span><span class="sxs-lookup"><span data-stu-id="ff976-134">Once hello embed token is created, you will then use hello access key toogenerate hello token which you can use from hello javascript perspective.</span></span> <span data-ttu-id="ff976-135">Hello *PowerBIToken classe* nécessite que vous installiez hello [Power BI Core NuGut Package](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).</span><span class="sxs-lookup"><span data-stu-id="ff976-135">hello *PowerBIToken class* requires that you install hello [Power BI Core NuGut Package](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).</span></span>

<span data-ttu-id="ff976-136">**Installation du package NuGet**</span><span class="sxs-lookup"><span data-stu-id="ff976-136">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.Core
```

<span data-ttu-id="ff976-137">**Code C#**</span><span class="sxs-lookup"><span data-stu-id="ff976-137">**C# code**</span></span>

```
using Microsoft.PowerBI.Security;

// rlsUsername, roles and scopes are optional.
embedToken = PowerBIToken.CreateReportEmbedToken(workspaceCollectionName, workspaceId, reportId, rlsUsername, roles, scopes);

var token = embedToken.Generate("{access key}");
```

### <a name="adding-permission-scopes-tooembed-tokens"></a><span data-ttu-id="ff976-138">Ajout de jetons de tooembed autorisation étendues</span><span class="sxs-lookup"><span data-stu-id="ff976-138">Adding permission scopes tooembed tokens</span></span>

<span data-ttu-id="ff976-139">Lorsque vous utilisez les jetons incorporé, vous souhaiterez toorestrict de l’utilisation d’hello que vous autoriser à accéder.</span><span class="sxs-lookup"><span data-stu-id="ff976-139">When using Embed tokens, you may want toorestrict usage of hello resources you give access to.</span></span> <span data-ttu-id="ff976-140">Dans cette optique, vous pouvez générer un jeton avec des autorisations étendues.</span><span class="sxs-lookup"><span data-stu-id="ff976-140">For this reason, you can generate a token with scoped permissions.</span></span> <span data-ttu-id="ff976-141">Pour plus d’informations, consultez la page [Étendues](power-bi-embedded-app-token-flow.md#scopes).</span><span class="sxs-lookup"><span data-stu-id="ff976-141">For more information, see [Scopes](power-bi-embedded-app-token-flow.md#scopes)</span></span>

## <a name="embed-using-javascript"></a><span data-ttu-id="ff976-142">Incorporer avec JavaScript</span><span class="sxs-lookup"><span data-stu-id="ff976-142">Embed using JavaScript</span></span>

<span data-ttu-id="ff976-143">Une fois que vous avez le jeton d’accès hello et l’id de rapport hello, nous pouvons incorporer des rapports hello à l’aide de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="ff976-143">After you have hello access token and hello report id, we can embed hello report using JavaScript.</span></span> <span data-ttu-id="ff976-144">Cela requiert l’installation de nuget de hello [Power BI JavaScript package](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/).</span><span class="sxs-lookup"><span data-stu-id="ff976-144">This requires that you install hello nuget [Power BI JavaScript package](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/).</span></span> <span data-ttu-id="ff976-145">Hello embedUrl sera simplement https://embedded.powerbi.com/appTokenReportEmbed.</span><span class="sxs-lookup"><span data-stu-id="ff976-145">hello embedUrl will just be https://embedded.powerbi.com/appTokenReportEmbed.</span></span>

> [!NOTE]
> <span data-ttu-id="ff976-146">Vous pouvez utiliser hello [incorporer l’exemple de rapport JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/) tootest fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="ff976-146">You can use hello [JavaScript Report Embed Sample](https://microsoft.github.io/PowerBI-JavaScript/demo/) tootest functionality.</span></span> <span data-ttu-id="ff976-147">Elle donne également des exemples de code pour hello différentes opérations qui sont disponibles.</span><span class="sxs-lookup"><span data-stu-id="ff976-147">It also gives code examples for hello different operations that are available.</span></span>

<span data-ttu-id="ff976-148">**Installation du package NuGet**</span><span class="sxs-lookup"><span data-stu-id="ff976-148">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.JavaScript
```

<span data-ttu-id="ff976-149">**Code JavaScript**</span><span class="sxs-lookup"><span data-stu-id="ff976-149">**JavaScript code**</span></span>

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

### <a name="set-hello-size-of-embedded-elements"></a><span data-ttu-id="ff976-150">Définir la taille des éléments incorporés hello</span><span class="sxs-lookup"><span data-stu-id="ff976-150">Set hello size of embedded elements</span></span>

<span data-ttu-id="ff976-151">rapport de Hello est incorporé automatiquement en fonction de la taille de hello de son conteneur.</span><span class="sxs-lookup"><span data-stu-id="ff976-151">hello report will automatically be embedded based on hello size of its container.</span></span> <span data-ttu-id="ff976-152">taille par défaut toooverride hello hello incorpore simplement ajouter une classe attribut ou inline styles CSS pour la largeur et la hauteur.</span><span class="sxs-lookup"><span data-stu-id="ff976-152">toooverride hello default size of hello embeds simply add a CSS class attribute or inline styles for width & height.</span></span>

## <a name="see-also"></a><span data-ttu-id="ff976-153">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="ff976-153">See also</span></span>

[<span data-ttu-id="ff976-154">Prise en main de l’exemple</span><span class="sxs-lookup"><span data-stu-id="ff976-154">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="ff976-155">Authentification et autorisation dans Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="ff976-155">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="ff976-156">CreateReportEmbedToken</span><span class="sxs-lookup"><span data-stu-id="ff976-156">CreateReportEmbedToken</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[<span data-ttu-id="ff976-157">Exemple d’incorporation JavaScript</span><span class="sxs-lookup"><span data-stu-id="ff976-157">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[<span data-ttu-id="ff976-158">Package JavaScript Power BI Core</span><span class="sxs-lookup"><span data-stu-id="ff976-158">Power BI JavaScript package</span></span>](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/)  
<span data-ttu-id="ff976-159">[Package NuGet Power BI API](https://www.nuget.org/profiles/powerbi)
[Package NuGet Power BI Core](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)</span><span class="sxs-lookup"><span data-stu-id="ff976-159">[Power BI API NuGet package](https://www.nuget.org/profiles/powerbi)
[Power BI Core NuGut Package](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)</span></span>  
[<span data-ttu-id="ff976-160">Référentiel Git PowerBI-CSharp</span><span class="sxs-lookup"><span data-stu-id="ff976-160">PowerBI-CSharp Git Repo</span></span>](https://github.com/Microsoft/PowerBI-CSharp)  
[<span data-ttu-id="ff976-161">Référentiel Git PowerBI-Node</span><span class="sxs-lookup"><span data-stu-id="ff976-161">PowerBI-Node Git Repo</span></span>](https://github.com/Microsoft/PowerBI-Node)  
<span data-ttu-id="ff976-162">Des questions ?</span><span class="sxs-lookup"><span data-stu-id="ff976-162">More questions?</span></span> [<span data-ttu-id="ff976-163">Essayez de hello Communauté Power BI</span><span class="sxs-lookup"><span data-stu-id="ff976-163">Try hello Power BI Community</span></span>](http://community.powerbi.com/)
