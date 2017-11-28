---
title: toouse aaaHow Power BI Embedded REST | Documents Microsoft
description: "Découvrez comment toouse Power BI Embedded REST "
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 8bcef780-cca0-4f30-9a9b-9daa1a7ae865
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 02/06/2017
ms.author: asaxton
ms.openlocfilehash: 98057724e60ba868f9c93de8c50383569eb8852d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-power-bi-embedded-with-rest"></a><span data-ttu-id="b30d2-103">Comment toouse Power BI Embedded REST</span><span class="sxs-lookup"><span data-stu-id="b30d2-103">How toouse Power BI Embedded with REST</span></span>

## <a name="power-bi-embedded-what-it-is-and-what-its-for"></a><span data-ttu-id="b30d2-104">Power BI Embedded : présentation et objectif</span><span class="sxs-lookup"><span data-stu-id="b30d2-104">Power BI Embedded: What it is and what it's for</span></span>

<span data-ttu-id="b30d2-105">Décrit une vue d’ensemble de Power BI Embedded officiel de hello [site Power BI Embedded](https://azure.microsoft.com/services/power-bi-embedded/), mais les jetons un œil rapide avant de passer à hello plus d’informations sur l’utilisation d’autres.</span><span class="sxs-lookup"><span data-stu-id="b30d2-105">An overview of Power BI Embedded is described in hello official [Power BI Embedded site](https://azure.microsoft.com/services/power-bi-embedded/), but let's take a quick look before we get into hello details about using it with REST.</span></span>

<span data-ttu-id="b30d2-106">C’est très simple.</span><span class="sxs-lookup"><span data-stu-id="b30d2-106">It's quite simple, really.</span></span> <span data-ttu-id="b30d2-107">Vous souhaiterez peut-être visualisations de données dynamiques hello toouse de [Power BI](https://powerbi.microsoft.com) dans votre application.</span><span class="sxs-lookup"><span data-stu-id="b30d2-107">you may want toouse hello dynamic data visualizations of [Power BI](https://powerbi.microsoft.com) in your own application.</span></span>

<span data-ttu-id="b30d2-108">La plupart des applications personnalisées doivent toodeliver les données de salutation à leurs clients, pas nécessairement les utilisateurs dans leur propre entreprise.</span><span class="sxs-lookup"><span data-stu-id="b30d2-108">Most custom applications need toodeliver hello data for their own customers, not necessarily users in their own organization.</span></span> <span data-ttu-id="b30d2-109">Par exemple, si vous êtes offrant un service de la société A et la société B, les utilisateurs de la société A uniquement les données doivent apparaître pour leur propre entreprise A. Autrement dit, l’architecture mutualisée hello est nécessaire pour la remise de hello.</span><span class="sxs-lookup"><span data-stu-id="b30d2-109">For example, if you're delivering some service for both company A and company B, users in company A should only see data for their own company A. That is, hello multi-tenancy is needed for hello delivery.</span></span>

<span data-ttu-id="b30d2-110">application personnalisée Hello peut également être offre ses propres méthodes d’authentification telles que l’authentification par formulaire, authentification de base, etc...</span><span class="sxs-lookup"><span data-stu-id="b30d2-110">hello custom application might also be offering its own authentication methods such as forms auth, basic auth, etc..</span></span> <span data-ttu-id="b30d2-111">Ensuite, hello incorporation solution doit collaborer en toute sécurité avec cette méthode d’authentification existant.</span><span class="sxs-lookup"><span data-stu-id="b30d2-111">Then, hello embedding solution must collaborate with this existing authentication methods safely.</span></span> <span data-ttu-id="b30d2-112">Il est également nécessaire pour toouse en mesure des utilisateurs toobe ces applications ISV sans hello achat supplémentaire ou le Gestionnaire de licences d’un abonnement Power BI.</span><span class="sxs-lookup"><span data-stu-id="b30d2-112">It's also necessary for users toobe able toouse those ISV applications without hello extra purchase or licensing of a Power BI subscription.</span></span>

 <span data-ttu-id="b30d2-113">**Power BI Embedded** est précisément conçu pour ces types de scénarios.</span><span class="sxs-lookup"><span data-stu-id="b30d2-113">**Power BI Embedded** is designed for precisely these kinds of scenarios.</span></span> <span data-ttu-id="b30d2-114">Donc, maintenant que nous avons cette introduction rapide la façon de hello, passons certains détails</span><span class="sxs-lookup"><span data-stu-id="b30d2-114">So, now that we have that quick introduction out of hello way, let's get into some details</span></span>

<span data-ttu-id="b30d2-115">Vous pouvez utiliser hello .NET \(c#) ou Node.js SDK, tooeasily générez votre application avec Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="b30d2-115">You can use hello .NET \(C#) or Node.js SDK, tooeasily build your application with Power BI Embedded.</span></span> <span data-ttu-id="b30d2-116">Toutefois, dans cet article, nous expliquerons le flux HTTP \(y compris AuthN) de Power BI sans Kit de développement logiciel (SDK).</span><span class="sxs-lookup"><span data-stu-id="b30d2-116">But, in this article, we'll explain about HTTP flow \(incl. AuthN) of Power BI without SDKs.</span></span> <span data-ttu-id="b30d2-117">Présentation de ce flux, vous pouvez générer votre application **avec n’importe quel langage de programmation**, et vous pouvez comprendre profondément essentiellement hello, Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="b30d2-117">Understanding this flow, you can build your application **with any programming language**, and you can understand deeply hello essence of Power BI Embedded.</span></span>

## <a name="create-power-bi-workspace-collection-and-get-access-key-provisioning"></a><span data-ttu-id="b30d2-118">Création d’une collection d’espaces de travail Power BI et obtention de la clé d’accès \(approvisionnement)</span><span class="sxs-lookup"><span data-stu-id="b30d2-118">Create Power BI workspace collection, and get access key \(Provisioning)</span></span>

<span data-ttu-id="b30d2-119">Power BI Embedded est un des hello services Azure.</span><span class="sxs-lookup"><span data-stu-id="b30d2-119">Power BI Embedded is one of hello Azure services.</span></span> <span data-ttu-id="b30d2-120">Hello uniquement ISV qui utilise le portail Azure est facturé pour les frais d’utilisation \(par toutes les heures des session utilisateur), et l’utilisateur hello rapport hello de vues n’est pas chargée ou même un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="b30d2-120">Only hello ISV who uses Azure Portal is charged for usage fees \(per hourly user session), and hello user who views hello report isn't charged or even require an Azure subscription.</span></span>
<span data-ttu-id="b30d2-121">Avant de commencer le développement d’applications, nous devons créer hello **collecte d’espace de travail Power BI** à l’aide du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="b30d2-121">Before starting our application development, we must create hello **Power BI workspace collection** by using Azure Portal.</span></span>

<span data-ttu-id="b30d2-122">Chaque espace de travail de Power BI Embedded est hello pour chaque client (client), et nous pouvons ajouter plusieurs espaces de travail dans chaque collection de l’espace de travail.</span><span class="sxs-lookup"><span data-stu-id="b30d2-122">Each workspace of Power BI Embedded is hello workspace for each customer (tenant), and we can add many workspaces in each workspace collection.</span></span> <span data-ttu-id="b30d2-123">Hello même clé d’accès est utilisé dans chaque collection de l’espace de travail.</span><span class="sxs-lookup"><span data-stu-id="b30d2-123">hello same access key is used in each workspace collection.</span></span> <span data-ttu-id="b30d2-124">En effet, collection d’espace de travail hello est la limite de sécurité de hello pour Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="b30d2-124">In-effect, hello workspace collection is hello security boundary for Power BI Embedded.</span></span>

![](media/power-bi-embedded-iframe/create-workspace.png)

<span data-ttu-id="b30d2-125">Lorsque nous aurons terminé la création de la collection d’espace de travail hello, copiez la clé d’accès hello à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="b30d2-125">When we finish creating hello workspace collection, copy hello access key from Azure Portal.</span></span>

![](media/power-bi-embedded-iframe/copy-access-key.png)

> [!NOTE]
> <span data-ttu-id="b30d2-126">Nous pouvons également d’approvisionner la collection d’espace de travail hello et obtenir la clé d’accès via une API REST.</span><span class="sxs-lookup"><span data-stu-id="b30d2-126">We can also provision hello workspace collection and get access key via REST API.</span></span> <span data-ttu-id="b30d2-127">toolearn, voir [API de fournisseur de ressources Power BI](https://msdn.microsoft.com/library/azure/mt712306.aspx).</span><span class="sxs-lookup"><span data-stu-id="b30d2-127">toolearn more, see [Power BI Resource Provider APIs](https://msdn.microsoft.com/library/azure/mt712306.aspx).</span></span>

## <a name="create-pbix-file-with-power-bi-desktop"></a><span data-ttu-id="b30d2-128">Création d’un fichier .pbix avec Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="b30d2-128">Create .pbix file with Power BI Desktop</span></span>

<span data-ttu-id="b30d2-129">Ensuite, nous devons créer la connexion de données hello et toobe rapports incorporés.</span><span class="sxs-lookup"><span data-stu-id="b30d2-129">Next, we must create hello data connection and reports toobe embedded.</span></span>
<span data-ttu-id="b30d2-130">Pour cette tâche, aucune programmation et aucun code ne sont nécessaires.</span><span class="sxs-lookup"><span data-stu-id="b30d2-130">For this task, there’s no programming or code.</span></span> <span data-ttu-id="b30d2-131">Nous n’utilisons que Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="b30d2-131">We just use Power BI Desktop.</span></span>
<span data-ttu-id="b30d2-132">Dans cet article, nous n’entrerons via hello plus d’informations sur la toouse Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="b30d2-132">In this article, we won't go through hello details about how toouse Power BI Desktop.</span></span> <span data-ttu-id="b30d2-133">Si vous avez besoin d’aide à ce sujet, consultez [Prise en main de Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/).</span><span class="sxs-lookup"><span data-stu-id="b30d2-133">If you need some help here, see [Getting started with Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/).</span></span> <span data-ttu-id="b30d2-134">Dans notre exemple, nous allons simplement utiliser hello [Retail Analysis Sample](https://powerbi.microsoft.com/documentation/powerbi-sample-datasets/).</span><span class="sxs-lookup"><span data-stu-id="b30d2-134">For our example, we'll just use hello [Retail Analysis Sample](https://powerbi.microsoft.com/documentation/powerbi-sample-datasets/).</span></span>

![](media/power-bi-embedded-iframe/power-bi-desktop-1.png)

## <a name="create-a-power-bi-workspace"></a><span data-ttu-id="b30d2-135">Création d’un espace de travail Power BI</span><span class="sxs-lookup"><span data-stu-id="b30d2-135">Create a Power BI workspace</span></span>

<span data-ttu-id="b30d2-136">Maintenant que hello configuration se fait, nous pouvons commencer la création d’espace de travail d’un client dans la collection d’espace de travail hello via les API REST.</span><span class="sxs-lookup"><span data-stu-id="b30d2-136">Now that hello provisioning is all done, let’s get started creating a customer’s workspace in hello workspace collection via REST APIs.</span></span> <span data-ttu-id="b30d2-137">Hello suivant HTTP POST demande (REST) consiste à créer nouvel espace de travail hello dans notre collection d’espace de travail existant.</span><span class="sxs-lookup"><span data-stu-id="b30d2-137">hello following HTTP POST Request (REST) is creating hello new workspace in our existing workspace collection.</span></span> <span data-ttu-id="b30d2-138">Il s’agit de hello [API d’espace de travail POST](https://msdn.microsoft.com/library/azure/mt711503.aspx).</span><span class="sxs-lookup"><span data-stu-id="b30d2-138">This is hello [POST Workspace API](https://msdn.microsoft.com/library/azure/mt711503.aspx).</span></span> <span data-ttu-id="b30d2-139">Dans notre exemple, le nom de la collection hello espace de travail est **mypbiapp**.</span><span class="sxs-lookup"><span data-stu-id="b30d2-139">In our example, hello workspace collection name is **mypbiapp**.</span></span> <span data-ttu-id="b30d2-140">Nous venons de définir la clé d’accès hello, nous copiés précédemment, en tant que **AppKey**.</span><span class="sxs-lookup"><span data-stu-id="b30d2-140">We just set hello access key, which we previously copied, as **AppKey**.</span></span> <span data-ttu-id="b30d2-141">C’est une authentification très simple !</span><span class="sxs-lookup"><span data-stu-id="b30d2-141">It’s very simple authentication!</span></span>

<span data-ttu-id="b30d2-142">**Demande HTTP**</span><span class="sxs-lookup"><span data-stu-id="b30d2-142">**HTTP Request**</span></span>

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces
Authorization: AppKey MpaUgrTv5e...
```

<span data-ttu-id="b30d2-143">**Réponse HTTP**</span><span class="sxs-lookup"><span data-stu-id="b30d2-143">**HTTP Response**</span></span>

```
HTTP/1.1 201 Created
Content-Type: application/json; odata.metadata=minimal; odata.streaming=true
Location: https://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces
RequestId: 4220d385-2fb3-406b-8901-4ebe11a5f6da

{
  "@odata.context": "http://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/$metadata#workspaces/$entity",
  "workspaceId": "32960a09-6366-4208-a8bb-9e0678cdbb9d",
  "workspaceCollectionName": "mypbiapp"
}
```

<span data-ttu-id="b30d2-144">Hello retourné **Id_espace_de_travail** est utilisé pour hello après les appels d’API suivants.</span><span class="sxs-lookup"><span data-stu-id="b30d2-144">hello returned **workspaceId** is used for hello following subsequent API calls.</span></span> <span data-ttu-id="b30d2-145">Notre application doit conserver cette valeur.</span><span class="sxs-lookup"><span data-stu-id="b30d2-145">Our application must retain this value.</span></span>

## <a name="import-pbix-file-into-hello-workspace"></a><span data-ttu-id="b30d2-146">Importer le fichier .pbix dans l’espace de travail hello</span><span class="sxs-lookup"><span data-stu-id="b30d2-146">Import .pbix file into hello workspace</span></span>

<span data-ttu-id="b30d2-147">Chaque rapport dans un espace de travail correspond tooa le fichier Power BI Desktop unique avec un jeu de données \(y compris les paramètres de source de données).</span><span class="sxs-lookup"><span data-stu-id="b30d2-147">Each report in a workspace corresponds tooa single Power BI Desktop file with a dataset \(including datasource settings).</span></span> <span data-ttu-id="b30d2-148">Nous pouvons importer notre espace de travail toohello de fichier .pbix comme indiqué dans le code hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="b30d2-148">We can import our .pbix file toohello workspace as shown in hello code below.</span></span> <span data-ttu-id="b30d2-149">Comme vous pouvez le voir, nous pouvons télécharger binaire hello du fichier .pbix à l’aide de MIME à parties multiples dans http.</span><span class="sxs-lookup"><span data-stu-id="b30d2-149">As you can see, we can upload hello binary of .pbix file using MIME multipart in http.</span></span>

<span data-ttu-id="b30d2-150">fragment d’uri Hello **32960a09-6366-4208-a8bb-9e0678cdbb9d** est hello Id_espace_de_travail et paramètre de requête **datasetDisplayName** est toocreate de nom de dataset hello.</span><span class="sxs-lookup"><span data-stu-id="b30d2-150">hello uri fragment **32960a09-6366-4208-a8bb-9e0678cdbb9d** is hello workspaceId, and query parameter **datasetDisplayName** is hello dataset name toocreate.</span></span> <span data-ttu-id="b30d2-151">Hello créé le jeu de données conserve toutes les données liées artefacts dans le fichier .pbix telles que les données importées, hello source de données de pointeur toohello, etc...</span><span class="sxs-lookup"><span data-stu-id="b30d2-151">hello created dataset holds all data related artifacts in .pbix file such as imported data, hello pointer toohello data source, etc..</span></span>

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports?datasetDisplayName=mydataset01
Authorization: AppKey MpaUgrTv5e...
Content-Type: multipart/form-data; boundary="A300testx"

--A300testx
Content-Disposition: form-data

{hello content (binary) of .pbix file}
--A300testx--
```

<span data-ttu-id="b30d2-152">Cette tâche d’importation peut prendre un certain temps.</span><span class="sxs-lookup"><span data-stu-id="b30d2-152">This import task might run for a while.</span></span> <span data-ttu-id="b30d2-153">Lorsque vous avez terminé, notre application peut demander à l’état de la tâche hello à l’aide des id de l’importation. Dans notre exemple, id d’importation hello est **4eec64dd-533b-47c3-a72c-6508ad854659**.</span><span class="sxs-lookup"><span data-stu-id="b30d2-153">When complete, our application can ask hello task status using import id. In our example, hello import id is **4eec64dd-533b-47c3-a72c-6508ad854659**.</span></span>

```
HTTP/1.1 202 Accepted
Content-Type: application/json; charset=utf-8
Location: https://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports/4eec64dd-533b-47c3-a72c-6508ad854659?tenantId=myorg
RequestId: 658bd6b4-b68d-4ec3-8818-2a94266dc220

{"id":"4eec64dd-533b-47c3-a72c-6508ad854659"}
```

<span data-ttu-id="b30d2-154">suivant de Hello demande état à l’aide de ce code d’importation :</span><span class="sxs-lookup"><span data-stu-id="b30d2-154">hello following is asking status using this import id:</span></span>

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports/4eec64dd-533b-47c3-a72c-6508ad854659
Authorization: AppKey MpaUgrTv5e...
```

<span data-ttu-id="b30d2-155">Si la tâche hello n’est pas terminée, hello réponse HTTP peut être comme suit :</span><span class="sxs-lookup"><span data-stu-id="b30d2-155">If hello task isn't complete, hello HTTP response could be like this:</span></span>

```
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
RequestId: 614a13a5-4de7-43e8-83c9-9cd225535136

{
  "id": "4eec64dd-533b-47c3-a72c-6508ad854659",
  "importState": "Publishing",
  "createdDateTime": "2016-07-19T07:36:06.227",
  "updatedDateTime": "2016-07-19T07:36:06.227",
  "name": "mydataset01"
}
```

<span data-ttu-id="b30d2-156">Si la tâche hello est terminée, hello réponse HTTP peut être plus comme suit :</span><span class="sxs-lookup"><span data-stu-id="b30d2-156">If hello task is complete, hello HTTP response could be more like this:</span></span>

```
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
RequestId: eb2c5a85-4d7d-4cc2-b0aa-0bafee4b1606

{
  "id": "4eec64dd-533b-47c3-a72c-6508ad854659",
  "importState": "Succeeded",
  "createdDateTime": "2016-07-19T07:36:06.227",
  "updatedDateTime": "2016-07-19T07:36:06.227",
  "reports": [
    {
      "id": "2027efc6-a308-4632-a775-b9a9186f087c",
      "name": "mydataset01",
      "webUrl": "https://app.powerbi.com/reports/2027efc6-a308-4632-a775-b9a9186f087c",
      "embedUrl": "https://app.powerbi.com/appTokenReportEmbed?reportId=2027efc6-a308-4632-a775-b9a9186f087c"
    }
  ],
  "datasets": [
    {
      "id": "458e0451-7215-4029-80b3-9627bf3417b0",
      "name": "mydataset01",
      "tables": [
      ],
      "webUrl": "https://app.powerbi.com/datasets/458e0451-7215-4029-80b3-9627bf3417b0"
    }
  ],
  "name": "mydataset01"
}
```

## <a name="data-source-connectivity-and-multi-tenancy-of-data"></a><span data-ttu-id="b30d2-157">Connectivité de la source de données \(et architecture mutualisée des données)</span><span class="sxs-lookup"><span data-stu-id="b30d2-157">Data source connectivity \(and multi-tenancy of data)</span></span>

<span data-ttu-id="b30d2-158">Pendant presque tous les artefacts hello dans le fichier .pbix sont importés dans notre espace de travail, informations d’identification de hello pour les sources de données ne sont pas.</span><span class="sxs-lookup"><span data-stu-id="b30d2-158">While almost all of hello artifacts in .pbix file are imported into our workspace, hello  credentials for data sources are not.</span></span> <span data-ttu-id="b30d2-159">Par conséquent, lorsque vous utilisez **mode DirectQuery**, hello rapport incorporé ne peut pas s’afficher correctement.</span><span class="sxs-lookup"><span data-stu-id="b30d2-159">As a result, when using **DirectQuery mode**, hello embedded report cannot be shown correctly.</span></span> <span data-ttu-id="b30d2-160">Mais, lorsque vous utilisez **mode d’importation**, nous pouvons afficher le rapport de hello à l’aide de données importées de hello existant.</span><span class="sxs-lookup"><span data-stu-id="b30d2-160">But, when using **Import mode**, we can view hello report using hello existing imported data.</span></span> <span data-ttu-id="b30d2-161">Dans ce cas, nous devons définir des informations d’identification de hello à l’aide de hello via les appels REST comme suit.</span><span class="sxs-lookup"><span data-stu-id="b30d2-161">In such a case, we must set hello credential using hello following steps via REST calls.</span></span>

<span data-ttu-id="b30d2-162">Tout d’abord, nous devons obtenir la source de données de passerelle hello.</span><span class="sxs-lookup"><span data-stu-id="b30d2-162">First, we must get hello gateway datasource.</span></span> <span data-ttu-id="b30d2-163">Nous savons hello dataset **id** est hello précédemment retourné id.</span><span class="sxs-lookup"><span data-stu-id="b30d2-163">We know hello dataset **id** is hello previously returned id.</span></span>

<span data-ttu-id="b30d2-164">**Demande HTTP**</span><span class="sxs-lookup"><span data-stu-id="b30d2-164">**HTTP Request**</span></span>

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/datasets/458e0451-7215-4029-80b3-9627bf3417b0/Default.GetBoundGatewayDatasources
Authorization: AppKey MpaUgrTv5e...
```

<span data-ttu-id="b30d2-165">**Réponse HTTP**</span><span class="sxs-lookup"><span data-stu-id="b30d2-165">**HTTP Response**</span></span>

```
GET HTTP/1.1 200 OK
Content-Type: application/json; odata.metadata=minimal; odata.streaming=true
RequestId: 574b0b18-a6fa-46a6-826c-e65840cf6e15

{
  "@odata.context": "http://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/$metadata#gatewayDatasources",
  "value": [
    {
      "id": "5f7ee2e7-4851-44a1-8b75-3eb01309d0ea",
      "gatewayId": "ca17e77f-1b51-429b-b059-6b3e3e9685d1",
      "datasourceType": "Sql",
      "connectionDetails": "{\"server\":\"testserver.database.windows.net\",\"database\":\"testdb01\"}"
    }
  ]
}
```

<span data-ttu-id="b30d2-166">À l’aide de hello retourné id de la passerelle et l’id de source de données \(voir hello précédente **gatewayId** et **id** Bonjour retourné de résultats), nous pouvons modifier les informations d’identification hello de cette source de données comme suit :</span><span class="sxs-lookup"><span data-stu-id="b30d2-166">Using hello returned gateway id and datasource id \(see hello previous **gatewayId** and **id** in hello returned result), we can change hello credential of this datasource as follows:</span></span>

<span data-ttu-id="b30d2-167">**Demande HTTP**</span><span class="sxs-lookup"><span data-stu-id="b30d2-167">**HTTP Request**</span></span>

```
PATCH https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/gateways/ca17e77f-1b51-429b-b059-6b3e3e9685d1/datasources/5f7ee2e7-4851-44a1-8b75-3eb01309d0ea
Authorization: AppKey MpaUgrTv5e...
Content-Type: application/json; charset=utf-8

{
  "credentialType": "Basic",
  "basicCredentials": {
    "username": "demouser",
    "password": "P@ssw0rd"
  }
}
```

<span data-ttu-id="b30d2-168">**Réponse HTTP**</span><span class="sxs-lookup"><span data-stu-id="b30d2-168">**HTTP Response**</span></span>

```
HTTP/1.1 200 OK
Content-Type: application/octet-stream
RequestId: 0e533c13-266a-4a9d-8718-fdad90391099
```

<span data-ttu-id="b30d2-169">En production, nous pouvons également définir des chaîne de connexion différente hello pour chaque espace de travail à l’aide des API REST.</span><span class="sxs-lookup"><span data-stu-id="b30d2-169">In production, we can also set hello different connection string for each workspace using REST API.</span></span> <span data-ttu-id="b30d2-170">\(Autrement dit, nous pouvons séparer de la base de données hello pour chaque client.)</span><span class="sxs-lookup"><span data-stu-id="b30d2-170">\(i.e, we can separate hello database for each customers.)</span></span>

<span data-ttu-id="b30d2-171">suivant de Hello change chaîne de connexion hello de source de données via REST.</span><span class="sxs-lookup"><span data-stu-id="b30d2-171">hello following is changing hello connection string of datasource via REST.</span></span>

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/datasets/458e0451-7215-4029-80b3-9627bf3417b0/Default.SetAllConnections
Authorization: AppKey MpaUgrTv5e...
Content-Type: application/json; charset=utf-8

{
  "connectionString": "data source=testserver02.database.windows.net;initial catalog=testdb02;persist security info=True;encrypt=True;trustservercertificate=False"
}
```

<span data-ttu-id="b30d2-172">Ou bien, nous pouvons utiliser la sécurité au niveau des lignes dans Power BI Embedded et nous pouvons séparer les données de hello tous les utilisateurs dans un rapport.</span><span class="sxs-lookup"><span data-stu-id="b30d2-172">Or, we can use Row Level Security in Power BI Embedded and we can separate hello data for each users in one report.</span></span> <span data-ttu-id="b30d2-173">Par conséquent, nous pouvons attribuer à chaque rapport client le même .pbix \(interface utilisateur, etc.) et différentes sources de données.</span><span class="sxs-lookup"><span data-stu-id="b30d2-173">As a result, we can provision each customer report with same .pbix \(UI, etc.) and different data sources.</span></span>

> [!NOTE]
> <span data-ttu-id="b30d2-174">Si vous utilisez **mode d’importation** au lieu de **mode DirectQuery**, il n’existe aucun modèle de toorefresh moyen via l’API.</span><span class="sxs-lookup"><span data-stu-id="b30d2-174">If you’re using **Import mode** instead of **DirectQuery mode**, there’s no way toorefresh models via API.</span></span> <span data-ttu-id="b30d2-175">Et les sources de données locales à travers la passerelle Power BI ne sont pas encore prises en charge dans Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="b30d2-175">And, on-premises datasources through Power BI gateway isn't yet supported in Power BI Embedded.</span></span> <span data-ttu-id="b30d2-176">Toutefois, vous souhaiterez vraiment tookeep un œil sur hello [blog Power BI](https://powerbi.microsoft.com/blog/) pour quelles sont les nouveautés et les nouveautés à venir dans les futures versions.</span><span class="sxs-lookup"><span data-stu-id="b30d2-176">However, you'll really want tookeep an eye on hello [Power BI blog](https://powerbi.microsoft.com/blog/) for what's new and what's coming in future releases.</span></span>

## <a name="authentication-and-hosting-embedding-reports-in-our-web-page"></a><span data-ttu-id="b30d2-177">Authentification et hébergement (incorporation) de rapports dans notre page web</span><span class="sxs-lookup"><span data-stu-id="b30d2-177">Authentication and hosting (embedding) reports in our web page</span></span>

<span data-ttu-id="b30d2-178">Dans hello précédente API REST, nous pouvons utiliser la clé d’accès hello **AppKey** en tant que l’en-tête d’autorisation hello.</span><span class="sxs-lookup"><span data-stu-id="b30d2-178">In hello previous REST API, we can use hello access key **AppKey** itself as hello authorization header.</span></span> <span data-ttu-id="b30d2-179">Ces appels peuvent être gérées à côté de serveur principal hello, il est donc plus sûr.</span><span class="sxs-lookup"><span data-stu-id="b30d2-179">Because these calls can be handled on hello backend server side, it's safe.</span></span>

<span data-ttu-id="b30d2-180">Mais, lorsque nous incorporez des rapports de hello dans notre page web, ce type d’informations de sécurité serait géré à l’aide de JavaScript \(frontal).</span><span class="sxs-lookup"><span data-stu-id="b30d2-180">But, when we embed hello report in our web page, this kind of security information would be handled using JavaScript \(frontend).</span></span> <span data-ttu-id="b30d2-181">Puis la valeur de l’en-tête d’autorisation hello doit être sécurisé.</span><span class="sxs-lookup"><span data-stu-id="b30d2-181">Then hello authorization header value must be secured.</span></span> <span data-ttu-id="b30d2-182">Si notre clé d’accès est identifiée par un utilisateur ou du code malveillant, elle peut être utilisée pour appeler toutes les opérations.</span><span class="sxs-lookup"><span data-stu-id="b30d2-182">If our access key is discovered by a malicious user or malicious code, they can call any operations using this key.</span></span>

<span data-ttu-id="b30d2-183">Lorsque nous incorporez des rapports de hello dans notre page web, nous devons utiliser le jeton calculée de hello au lieu de la clé d’accès **AppKey**.</span><span class="sxs-lookup"><span data-stu-id="b30d2-183">When we embed hello report in our web page, we must use hello computed token instead of access key **AppKey**.</span></span> <span data-ttu-id="b30d2-184">Notre application doit créer hello OAuth Json Web Token \(JSON) qui se compose de revendications de hello et signature numérique calculée de hello.</span><span class="sxs-lookup"><span data-stu-id="b30d2-184">Our application must create hello OAuth Json Web Token \(JWT) which consists of hello claims and hello computed digital signature.</span></span> <span data-ttu-id="b30d2-185">Comme illustré ci-dessous, cet OAuth JWT est un ensemble de tokens de chaînes encodés délimités par des points.</span><span class="sxs-lookup"><span data-stu-id="b30d2-185">As illustrated below, this OAuth JWT is dot-delimited encoded string tokens.</span></span>

![](media/power-bi-embedded-iframe/oauth-jwt.png)

<span data-ttu-id="b30d2-186">Tout d’abord, nous devons préparer la valeur d’entrée de hello, qui est signée ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="b30d2-186">First, we must prepare hello input value, which is signed later.</span></span> <span data-ttu-id="b30d2-187">Cette valeur est la chaîne hello en base64 encodé url (rfc4648) de hello suivant json, et ils sont délimités par point de hello \(.) caractères.</span><span class="sxs-lookup"><span data-stu-id="b30d2-187">This value is hello base64 url encoded (rfc4648) string of hello following json, and these are delimited by hello dot \(.) character.</span></span> <span data-ttu-id="b30d2-188">Une version ultérieure, nous expliquons comment tooget hello id du rapport.</span><span class="sxs-lookup"><span data-stu-id="b30d2-188">Later, we'll explain how tooget hello report id.</span></span>

> [!NOTE]
> <span data-ttu-id="b30d2-189">Si nous voulons toouse au niveau de sécurité des lignes avec Power BI Embedded, nous devons spécifier également **nom d’utilisateur** et **rôles** dans les revendications hello.</span><span class="sxs-lookup"><span data-stu-id="b30d2-189">If we want toouse Row Level Security (RLS) with Power BI Embedded, we must also specify **username** and **roles** in hello claims.</span></span>

```
{
  "typ":"JWT",
  "alg":"HS256"
}
```

```
{
  "wid":"{workspace id}",
  "rid":"{report id}",
  "wcn":"{workspace collection name}",
  "iss":"PowerBISDK",
  "ver":"0.2.0",
  "aud":"https://analysis.windows.net/powerbi/api",
  "nbf":{start time of token expiration},
  "exp":{end time of token expiration}
}
```

<span data-ttu-id="b30d2-190">Ensuite, nous devons créer la chaîne codée en base64 de hello de HMAC \(signature de hello) avec l’algorithme SHA256.</span><span class="sxs-lookup"><span data-stu-id="b30d2-190">Next, we must create hello base64 encoded string of HMAC \(hello signature) with SHA256 algorithm.</span></span> <span data-ttu-id="b30d2-191">Cette valeur d’entrée signée est chaîne précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="b30d2-191">This signed input value is hello previous string.</span></span>

<span data-ttu-id="b30d2-192">Enfin, nous devons combiner valeur d’entrée de hello et la chaîne de signature à l’aide de la période \(.) caractères.</span><span class="sxs-lookup"><span data-stu-id="b30d2-192">Last, we must combine hello input value and signature string using period \(.) character.</span></span> <span data-ttu-id="b30d2-193">chaîne de Hello terminée est jeton d’application hello hello l’incorporation de rapport.</span><span class="sxs-lookup"><span data-stu-id="b30d2-193">hello completed string is hello app token for hello report embedding.</span></span> <span data-ttu-id="b30d2-194">Même si le jeton d’application hello est découvert par un utilisateur malveillant, ils ne peut pas récupérer la clé d’accès d’origine hello.</span><span class="sxs-lookup"><span data-stu-id="b30d2-194">Even if hello app token is discovered by a malicious user, they cannot get hello original access key.</span></span> <span data-ttu-id="b30d2-195">Ce jeton d’application expirera rapidement.</span><span class="sxs-lookup"><span data-stu-id="b30d2-195">This app token will expire quickly.</span></span>

<span data-ttu-id="b30d2-196">Voici un exemple PHP de ces étapes :</span><span class="sxs-lookup"><span data-stu-id="b30d2-196">Here's a PHP example for these steps:</span></span>

```
<?php
// 1. power bi access key
$accesskey = "MpaUgrTv5e...";

// 2. construct input value
$token1 = "{" .
  "\"typ\":\"JWT\"," .
  "\"alg\":\"HS256\"" .
  "}";
$token2 = "{" .
  "\"wid\":\"32960a09-6366-4208-a8bb-9e0678cdbb9d\"," . // workspace id
  "\"rid\":\"2027efc6-a308-4632-a775-b9a9186f087c\"," . // report id
  "\"wcn\":\"mypbiapp\"," . // workspace collection name
  "\"iss\":\"PowerBISDK\"," .
  "\"ver\":\"0.2.0\"," .
  "\"aud\":\"https://analysis.windows.net/powerbi/api\"," .
  "\"nbf\":" . date("U") . "," .
  "\"exp\":" . date("U" , strtotime("+1 hour")) .
  "}";
$inputval = rfc4648_base64_encode($token1) .
  "." .
  rfc4648_base64_encode($token2);

// 3. get encoded signature
$hash = hash_hmac("sha256",
    $inputval,
    $accesskey,
    true);
$sig = rfc4648_base64_encode($hash);

// 4. show result (which is hello apptoken)
$apptoken = $inputval . "." . $sig;
echo($apptoken);

// helper functions
function rfc4648_base64_encode($arg) {
  $res = $arg;
  $res = base64_encode($res);
  $res = str_replace("/", "_", $res);
  $res = str_replace("+", "-", $res);
  $res = rtrim($res, "=");
  return $res;
}
?>
```

## <a name="finally-embed-hello-report-into-hello-web-page"></a><span data-ttu-id="b30d2-197">Enfin, incorporer des rapports de hello hello web page</span><span class="sxs-lookup"><span data-stu-id="b30d2-197">Finally, embed hello report into hello web page</span></span>

<span data-ttu-id="b30d2-198">L’incorporation de notre rapport, nous devons obtenir hello incorporer des url et au rapport **id** à l’aide de hello suivant l’API REST.</span><span class="sxs-lookup"><span data-stu-id="b30d2-198">For embedding our report, we must get hello embed url and report **id** using hello following REST API.</span></span>

<span data-ttu-id="b30d2-199">**Demande HTTP**</span><span class="sxs-lookup"><span data-stu-id="b30d2-199">**HTTP Request**</span></span>

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/reports
Authorization: AppKey MpaUgrTv5e...
```

<span data-ttu-id="b30d2-200">**Réponse HTTP**</span><span class="sxs-lookup"><span data-stu-id="b30d2-200">**HTTP Response**</span></span>

```
HTTP/1.1 200 OK
Content-Type: application/json; odata.metadata=minimal; odata.streaming=true
RequestId: d4099022-405b-49d3-b3b7-3c60cf675958

{
  "@odata.context": "http://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/$metadata#reports",
  "value": [
    {
      "id": "2027efc6-a308-4632-a775-b9a9186f087c",
      "name": "mydataset01",
      "webUrl": "https://app.powerbi.com/reports/2027efc6-a308-4632-a775-b9a9186f087c",
      "embedUrl": "https://embedded.powerbi.com/appTokenReportEmbed?reportId=2027efc6-a308-4632-a775-b9a9186f087c",
      "isFromPbix": false
    }
  ]
}
```

<span data-ttu-id="b30d2-201">Nous pouvons incorporer des rapports de hello dans notre application web à l’aide du jeton d’application hello précédente.</span><span class="sxs-lookup"><span data-stu-id="b30d2-201">We can embed hello report in our web app using hello previous app token.</span></span>
<span data-ttu-id="b30d2-202">Si nous examinons le code exemple suivant de hello, partie d’anciens hello est hello identique à l’exemple précédent de hello.</span><span class="sxs-lookup"><span data-stu-id="b30d2-202">If we look at hello next sample code, hello former part is hello same as hello previous example.</span></span> <span data-ttu-id="b30d2-203">Dans la dernière partie de hello, cet exemple montre hello **embedUrl** \(voir le résultat précédent de hello) de hello iframe et publie le jeton d’application hello dans hello iframe.</span><span class="sxs-lookup"><span data-stu-id="b30d2-203">In hello latter part, this sample shows hello **embedUrl** \(see hello previous result) in hello iframe, and is posting hello app token into hello iframe.</span></span>

> [!NOTE]
> <span data-ttu-id="b30d2-204">Vous devez toochange hello rapport id valeur tooone de votre choix.</span><span class="sxs-lookup"><span data-stu-id="b30d2-204">You'll need toochange hello report id value tooone of your own.</span></span> <span data-ttu-id="b30d2-205">En outre, en raison du bogue tooa dans notre système de gestion de contenu, balise iframe de hello dans l’exemple de code hello est lu littéralement.</span><span class="sxs-lookup"><span data-stu-id="b30d2-205">Also, due tooa bug in our content management system, hello iframe tag in hello code sample is read literally.</span></span> <span data-ttu-id="b30d2-206">Supprimez le texte hello limitée à partir de la balise de hello si vous copiez et collez cet exemple de code.</span><span class="sxs-lookup"><span data-stu-id="b30d2-206">Remove hello capped text from hello tag if you copy and paste this sample code.</span></span>

```
    <?php
    // 1. power bi access key
    $accesskey = "MpaUgrTv5e...";

    // 2. construct input value
    $token1 = "{" .
      "\"typ\":\"JWT\"," .
      "\"alg\":\"HS256\"" .
      "}";
    $token2 = "{" .
      "\"wid\":\"32960a09-6366-4208-a8bb-9e0678cdbb9d\"," . // workspace id
      "\"rid\":\"2027efc6-a308-4632-a775-b9a9186f087c\"," . // report id
      "\"wcn\":\"mypbiapp\"," . // workspace collection name
      "\"iss\":\"PowerBISDK\"," .
      "\"ver\":\"0.2.0\"," .
      "\"aud\":\"https://analysis.windows.net/powerbi/api\"," .
      "\"nbf\":" . date("U") . "," .
      "\"exp\":" . date("U" , strtotime("+1 hour")) .
      "}";
    $inputval = rfc4648_base64_encode($token1) .
      "." .
      rfc4648_base64_encode($token2);

    // 3. get encoded signature value
    $hash = hash_hmac("sha256",
        $inputval,
        $accesskey,
        true);
    $sig = rfc4648_base64_encode($hash);

    // 4. get apptoken
    $apptoken = $inputval . "." . $sig;

    // helper functions
    function rfc4648_base64_encode($arg) {
      $res = $arg;
      $res = base64_encode($res);
      $res = str_replace("/", "_", $res);
      $res = str_replace("+", "-", $res);
      $res = rtrim($res, "=");
      return $res;
    }
    ?>
    <!DOCTYPE html>
    <html>
    <head>
      <meta charset="utf-8" />
      <meta http-equiv="X-UA-Compatible" content="IE=edge">
      <title>Test page</title>
      <meta name="viewport" content="width=device-width, initial-scale=1">
    </head>
    <body>
      <button id="btnView">View Report !</button>
      <div id="divView">
        <**REMOVE THIS CAPPED TEXT IF COPIED** iframe id="ifrTile" width="100%" height="400"></iframe>
      </div>
      <script>
        (function () {
          document.getElementById('btnView').onclick = function() {
            var iframe = document.getElementById('ifrTile');
            iframe.src = 'https://embedded.powerbi.com/appTokenReportEmbed?reportId=2027efc6-a308-4632-a775-b9a9186f087c';
            iframe.onload = function() {
              var msgJson = {
                action: "loadReport",
                accessToken: "<?=$apptoken?>",
                height: 500,
                width: 722
              };
              var msgTxt = JSON.stringify(msgJson);
              iframe.contentWindow.postMessage(msgTxt, "*");
            };
          };
        }());
      </script>
    </body>
```

<span data-ttu-id="b30d2-207">Et voici notre résultat :</span><span class="sxs-lookup"><span data-stu-id="b30d2-207">And here's our result:</span></span>

![](media/power-bi-embedded-iframe/view-report.png)

<span data-ttu-id="b30d2-208">À ce stade, Power BI Embedded affiche uniquement les rapports hello dans hello iframe.</span><span class="sxs-lookup"><span data-stu-id="b30d2-208">At this time, Power BI Embedded only shows hello report in hello iframe.</span></span> <span data-ttu-id="b30d2-209">Mais garder un œil sur hello [Blog Power BI](https://powerbi.microsoft.com/blog/).</span><span class="sxs-lookup"><span data-stu-id="b30d2-209">But, keep an eye on hello [Power BI Blog](https://powerbi.microsoft.com/blog/).</span></span> <span data-ttu-id="b30d2-210">Futures améliorations pourrait utiliser côté client nouvelle API qui sera nous envoyer des informations dans hello iframe ainsi que fournir des informations. C’est très intéressant !</span><span class="sxs-lookup"><span data-stu-id="b30d2-210">Future improvements could use new client side APIs that will let us send information into hello iframe as well as get information out. Exciting stuff!</span></span>

## <a name="see-also"></a><span data-ttu-id="b30d2-211">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="b30d2-211">See also</span></span>
* [<span data-ttu-id="b30d2-212">Authentification et autorisation dans Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="b30d2-212">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)

<span data-ttu-id="b30d2-213">Des questions ?</span><span class="sxs-lookup"><span data-stu-id="b30d2-213">More questions?</span></span> [<span data-ttu-id="b30d2-214">Essayez de hello Communauté Power BI</span><span class="sxs-lookup"><span data-stu-id="b30d2-214">Try hello Power BI Community</span></span>](http://community.powerbi.com/)

