---
title: Utiliser Power BI Embedded avec REST | Microsoft Docs
description: "Apprenez à utiliser Power BI Embedded avec REST  "
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
ms.openlocfilehash: 31624b9d15772a4f08cf013ac713b3aa636acfca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-power-bi-embedded-with-rest"></a><span data-ttu-id="c36a7-103">Utiliser Power BI Embedded avec REST</span><span class="sxs-lookup"><span data-stu-id="c36a7-103">How to use Power BI Embedded with REST</span></span>

## <a name="power-bi-embedded-what-it-is-and-what-its-for"></a><span data-ttu-id="c36a7-104">Power BI Embedded : présentation et objectif</span><span class="sxs-lookup"><span data-stu-id="c36a7-104">Power BI Embedded: What it is and what it's for</span></span>

<span data-ttu-id="c36a7-105">Une vue d’ensemble de Power BI Embedded est décrite sur le [site Power BI Embedded officiel](https://azure.microsoft.com/services/power-bi-embedded/), mais commençons par jeter un coup d’œil rapide avant d’entrer dans les détails de son utilisation avec REST.</span><span class="sxs-lookup"><span data-stu-id="c36a7-105">An overview of Power BI Embedded is described in the official [Power BI Embedded site](https://azure.microsoft.com/services/power-bi-embedded/), but let's take a quick look before we get into the details about using it with REST.</span></span>

<span data-ttu-id="c36a7-106">C’est très simple.</span><span class="sxs-lookup"><span data-stu-id="c36a7-106">It's quite simple, really.</span></span> <span data-ttu-id="c36a7-107">Vous pouvez utiliser les visualisations de données dynamiques de [Power BI](https://powerbi.microsoft.com) dans votre propre application.</span><span class="sxs-lookup"><span data-stu-id="c36a7-107">you may want to use the dynamic data visualizations of [Power BI](https://powerbi.microsoft.com) in your own application.</span></span>

<span data-ttu-id="c36a7-108">La plupart des applications personnalisées ont besoin de fournir les données à leurs clients, et pas nécessairement aux utilisateurs de leur propre organisation.</span><span class="sxs-lookup"><span data-stu-id="c36a7-108">Most custom applications need to deliver the data for their own customers, not necessarily users in their own organization.</span></span> <span data-ttu-id="c36a7-109">Par exemple, si vous proposez un service à la société A et à la société B, les utilisateurs de la société A doivent voir uniquement les données de leur propre société, la société A. Autrement dit, l’architecture mutualisée est nécessaire pour fournir les données.</span><span class="sxs-lookup"><span data-stu-id="c36a7-109">For example, if you're delivering some service for both company A and company B, users in company A should only see data for their own company A. That is, the multi-tenancy is needed for the delivery.</span></span>

<span data-ttu-id="c36a7-110">L’application personnalisée peut également offrir ses propres méthodes d’authentification, notamment l’authentification par formulaire, l’authentification de base, etc.</span><span class="sxs-lookup"><span data-stu-id="c36a7-110">The custom application might also be offering its own authentication methods such as forms auth, basic auth, etc..</span></span> <span data-ttu-id="c36a7-111">Dans ce cas, la solution d’incorporation doit collaborer en toute sécurité avec cette méthode d’authentification existante.</span><span class="sxs-lookup"><span data-stu-id="c36a7-111">Then, the embedding solution must collaborate with this existing authentication methods safely.</span></span> <span data-ttu-id="c36a7-112">Il est également nécessaire que les utilisateurs puissent utiliser ces applications ISV sans achat supplémentaire ou acquisition d’une licence d’abonnement Power BI.</span><span class="sxs-lookup"><span data-stu-id="c36a7-112">It's also necessary for users to be able to use those ISV applications without the extra purchase or licensing of a Power BI subscription.</span></span>

 <span data-ttu-id="c36a7-113">**Power BI Embedded** est précisément conçu pour ces types de scénarios.</span><span class="sxs-lookup"><span data-stu-id="c36a7-113">**Power BI Embedded** is designed for precisely these kinds of scenarios.</span></span> <span data-ttu-id="c36a7-114">Maintenant que cette introduction rapide est faite, nous allons pouvoir entrer un peu dans les détails.</span><span class="sxs-lookup"><span data-stu-id="c36a7-114">So, now that we have that quick introduction out of the way, let's get into some details</span></span>

<span data-ttu-id="c36a7-115">Vous pouvez utiliser le Kit de développement logiciel (SDK) .NET \(C#) ou Node.js pour créer facilement votre application avec Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="c36a7-115">You can use the .NET \(C#) or Node.js SDK, to easily build your application with Power BI Embedded.</span></span> <span data-ttu-id="c36a7-116">Toutefois, dans cet article, nous expliquerons le flux HTTP \(y compris AuthN) de Power BI sans Kit de développement logiciel (SDK).</span><span class="sxs-lookup"><span data-stu-id="c36a7-116">But, in this article, we'll explain about HTTP flow \(incl. AuthN) of Power BI without SDKs.</span></span> <span data-ttu-id="c36a7-117">Si vous comprenez ce flux, vous pouvez générer votre application **avec n’importe quel langage de programmation** et comprendre l’essence même de Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="c36a7-117">Understanding this flow, you can build your application **with any programming language**, and you can understand deeply the essence of Power BI Embedded.</span></span>

## <a name="create-power-bi-workspace-collection-and-get-access-key-provisioning"></a><span data-ttu-id="c36a7-118">Création d’une collection d’espaces de travail Power BI et obtention de la clé d’accès \(approvisionnement)</span><span class="sxs-lookup"><span data-stu-id="c36a7-118">Create Power BI workspace collection, and get access key \(Provisioning)</span></span>

<span data-ttu-id="c36a7-119">Power BI Embedded fait partie des services Azure.</span><span class="sxs-lookup"><span data-stu-id="c36a7-119">Power BI Embedded is one of the Azure services.</span></span> <span data-ttu-id="c36a7-120">Seul l’éditeur de logiciels indépendant qui utilise le portail Azure doit payer des frais d’utilisation \(par session d’utilisateur à l’heure). L’utilisateur qui consulte le rapport n’est pas facturé et n’a même pas besoin d’un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="c36a7-120">Only the ISV who uses Azure Portal is charged for usage fees \(per hourly user session), and the user who views the report isn't charged or even require an Azure subscription.</span></span>
<span data-ttu-id="c36a7-121">Avant de commencer le développement de notre application, nous devons créer la **collection d’espaces de travail Power BI** avec le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="c36a7-121">Before starting our application development, we must create the **Power BI workspace collection** by using Azure Portal.</span></span>

<span data-ttu-id="c36a7-122">Chaque espace de travail de Power BI Embedded est l’espace de travail de chaque client (locataire), et nous pouvons ajouter de nombreux espaces de travail à chaque collection d’espaces de travail.</span><span class="sxs-lookup"><span data-stu-id="c36a7-122">Each workspace of Power BI Embedded is the workspace for each customer (tenant), and we can add many workspaces in each workspace collection.</span></span> <span data-ttu-id="c36a7-123">La même clé d’accès est utilisée dans chaque collection d’espaces de travail.</span><span class="sxs-lookup"><span data-stu-id="c36a7-123">The same access key is used in each workspace collection.</span></span> <span data-ttu-id="c36a7-124">En effet, la collection d’espaces de travail est la limite de sécurité de Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="c36a7-124">In-effect, the workspace collection is the security boundary for Power BI Embedded.</span></span>

![](media/power-bi-embedded-iframe/create-workspace.png)

<span data-ttu-id="c36a7-125">Une fois que nous avons terminé la création de la collection d’espaces de travail, copions la clé d’accès à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="c36a7-125">When we finish creating the workspace collection, copy the access key from Azure Portal.</span></span>

![](media/power-bi-embedded-iframe/copy-access-key.png)

> [!NOTE]
> <span data-ttu-id="c36a7-126">Nous pouvons également configurer la collection d’espaces de travail et obtenir la clé d’accès avec l’API REST.</span><span class="sxs-lookup"><span data-stu-id="c36a7-126">We can also provision the workspace collection and get access key via REST API.</span></span> <span data-ttu-id="c36a7-127">Pour plus d’informations, consultez [API du fournisseur de ressources Power BI](https://msdn.microsoft.com/library/azure/mt712306.aspx).</span><span class="sxs-lookup"><span data-stu-id="c36a7-127">To learn more, see [Power BI Resource Provider APIs](https://msdn.microsoft.com/library/azure/mt712306.aspx).</span></span>

## <a name="create-pbix-file-with-power-bi-desktop"></a><span data-ttu-id="c36a7-128">Création d’un fichier .pbix avec Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="c36a7-128">Create .pbix file with Power BI Desktop</span></span>

<span data-ttu-id="c36a7-129">Ensuite, nous devons créer la connexion de données et les rapports à incorporer.</span><span class="sxs-lookup"><span data-stu-id="c36a7-129">Next, we must create the data connection and reports to be embedded.</span></span>
<span data-ttu-id="c36a7-130">Pour cette tâche, aucune programmation et aucun code ne sont nécessaires.</span><span class="sxs-lookup"><span data-stu-id="c36a7-130">For this task, there’s no programming or code.</span></span> <span data-ttu-id="c36a7-131">Nous n’utilisons que Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="c36a7-131">We just use Power BI Desktop.</span></span>
<span data-ttu-id="c36a7-132">Dans cet article, nous n’allons pas étudier les détails de l’utilisation de Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="c36a7-132">In this article, we won't go through the details about how to use Power BI Desktop.</span></span> <span data-ttu-id="c36a7-133">Si vous avez besoin d’aide à ce sujet, consultez [Prise en main de Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/).</span><span class="sxs-lookup"><span data-stu-id="c36a7-133">If you need some help here, see [Getting started with Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/).</span></span> <span data-ttu-id="c36a7-134">Dans notre exemple, nous utilisons simplement [l’exemple d’analyse des données de vente](https://powerbi.microsoft.com/documentation/powerbi-sample-datasets/).</span><span class="sxs-lookup"><span data-stu-id="c36a7-134">For our example, we'll just use the [Retail Analysis Sample](https://powerbi.microsoft.com/documentation/powerbi-sample-datasets/).</span></span>

![](media/power-bi-embedded-iframe/power-bi-desktop-1.png)

## <a name="create-a-power-bi-workspace"></a><span data-ttu-id="c36a7-135">Création d’un espace de travail Power BI</span><span class="sxs-lookup"><span data-stu-id="c36a7-135">Create a Power BI workspace</span></span>

<span data-ttu-id="c36a7-136">Maintenant que l’approvisionnement est fait, nous allons commencer la création de l’espace de travail d’un client dans la collection d’espaces de travail avec les API REST.</span><span class="sxs-lookup"><span data-stu-id="c36a7-136">Now that the provisioning is all done, let’s get started creating a customer’s workspace in the workspace collection via REST APIs.</span></span> <span data-ttu-id="c36a7-137">La requête HTTP POST (REST) suivante crée le nouvel espace de travail dans notre collection d’espaces de travail existante.</span><span class="sxs-lookup"><span data-stu-id="c36a7-137">The following HTTP POST Request (REST) is creating the new workspace in our existing workspace collection.</span></span> <span data-ttu-id="c36a7-138">Il s’agit de [l’API d’espace de travail POST](https://msdn.microsoft.com/library/azure/mt711503.aspx).</span><span class="sxs-lookup"><span data-stu-id="c36a7-138">This is the [POST Workspace API](https://msdn.microsoft.com/library/azure/mt711503.aspx).</span></span> <span data-ttu-id="c36a7-139">Dans notre exemple, le nom de la collection d’espaces de travail est **mypbiapp**.</span><span class="sxs-lookup"><span data-stu-id="c36a7-139">In our example, the workspace collection name is **mypbiapp**.</span></span> <span data-ttu-id="c36a7-140">Nous définissons simplement la clé d’accès, que nous avons copiée précédemment, comme **AppKey**.</span><span class="sxs-lookup"><span data-stu-id="c36a7-140">We just set the access key, which we previously copied, as **AppKey**.</span></span> <span data-ttu-id="c36a7-141">C’est une authentification très simple !</span><span class="sxs-lookup"><span data-stu-id="c36a7-141">It’s very simple authentication!</span></span>

<span data-ttu-id="c36a7-142">**Demande HTTP**</span><span class="sxs-lookup"><span data-stu-id="c36a7-142">**HTTP Request**</span></span>

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces
Authorization: AppKey MpaUgrTv5e...
```

<span data-ttu-id="c36a7-143">**Réponse HTTP**</span><span class="sxs-lookup"><span data-stu-id="c36a7-143">**HTTP Response**</span></span>

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

<span data-ttu-id="c36a7-144">Le **workspaceId** renvoyé est utilisé pour les appels d’API suivants.</span><span class="sxs-lookup"><span data-stu-id="c36a7-144">The returned **workspaceId** is used for the following subsequent API calls.</span></span> <span data-ttu-id="c36a7-145">Notre application doit conserver cette valeur.</span><span class="sxs-lookup"><span data-stu-id="c36a7-145">Our application must retain this value.</span></span>

## <a name="import-pbix-file-into-the-workspace"></a><span data-ttu-id="c36a7-146">Importer le fichier .pbix dans l’espace de travail</span><span class="sxs-lookup"><span data-stu-id="c36a7-146">Import .pbix file into the workspace</span></span>

<span data-ttu-id="c36a7-147">Chaque rapport d’un espace de travail correspond à un seul fichier Power BI Desktop avec un jeu de données \(y compris les paramètres de source de données).</span><span class="sxs-lookup"><span data-stu-id="c36a7-147">Each report in a workspace corresponds to a single Power BI Desktop file with a dataset \(including datasource settings).</span></span> <span data-ttu-id="c36a7-148">Nous pouvons importer notre fichier .pbix dans l’espace de travail comme le montre le code ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="c36a7-148">We can import our .pbix file to the workspace as shown in the code below.</span></span> <span data-ttu-id="c36a7-149">Comme vous pouvez le voir, nous pouvons télécharger le binaire du fichier .pbix à l’aide du MIME en plusieurs parties dans HTTP.</span><span class="sxs-lookup"><span data-stu-id="c36a7-149">As you can see, we can upload the binary of .pbix file using MIME multipart in http.</span></span>

<span data-ttu-id="c36a7-150">Le fragment d’URI **32960a09-6366-4208-a8bb-9e0678cdbb9d** est le workspaceId et le paramètre de requête **datasetDisplayName** est le nom du jeu de données à créer.</span><span class="sxs-lookup"><span data-stu-id="c36a7-150">The uri fragment **32960a09-6366-4208-a8bb-9e0678cdbb9d** is the workspaceId, and query parameter **datasetDisplayName** is the dataset name to create.</span></span> <span data-ttu-id="c36a7-151">Le jeu de données créé conserve tous les artefacts liés aux données dans le fichier .pbix, notamment les données importées, le pointeur vers la source de données, etc.</span><span class="sxs-lookup"><span data-stu-id="c36a7-151">The created dataset holds all data related artifacts in .pbix file such as imported data, the pointer to the data source, etc..</span></span>

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports?datasetDisplayName=mydataset01
Authorization: AppKey MpaUgrTv5e...
Content-Type: multipart/form-data; boundary="A300testx"

--A300testx
Content-Disposition: form-data

{the content (binary) of .pbix file}
--A300testx--
```

<span data-ttu-id="c36a7-152">Cette tâche d’importation peut prendre un certain temps.</span><span class="sxs-lookup"><span data-stu-id="c36a7-152">This import task might run for a while.</span></span> <span data-ttu-id="c36a7-153">Lorsqu’elle est terminée, notre application peut demander l’état de la tâche avec l’ID d’importation.</span><span class="sxs-lookup"><span data-stu-id="c36a7-153">When complete, our application can ask the task status using import id.</span></span> <span data-ttu-id="c36a7-154">Dans notre exemple, l’ID d’importation est **4eec64dd-533b-47c3-a72c-6508ad854659**.</span><span class="sxs-lookup"><span data-stu-id="c36a7-154">In our example, the import id is **4eec64dd-533b-47c3-a72c-6508ad854659**.</span></span>

```
HTTP/1.1 202 Accepted
Content-Type: application/json; charset=utf-8
Location: https://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports/4eec64dd-533b-47c3-a72c-6508ad854659?tenantId=myorg
RequestId: 658bd6b4-b68d-4ec3-8818-2a94266dc220

{"id":"4eec64dd-533b-47c3-a72c-6508ad854659"}
```

<span data-ttu-id="c36a7-155">Le code suivant demande l’état avec cet ID d’importation :</span><span class="sxs-lookup"><span data-stu-id="c36a7-155">The following is asking status using this import id:</span></span>

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports/4eec64dd-533b-47c3-a72c-6508ad854659
Authorization: AppKey MpaUgrTv5e...
```

<span data-ttu-id="c36a7-156">Si la tâche n’est pas terminée, la réponse HTTP peut être la suivante :</span><span class="sxs-lookup"><span data-stu-id="c36a7-156">If the task isn't complete, the HTTP response could be like this:</span></span>

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

<span data-ttu-id="c36a7-157">Si la tâche est terminée, la réponse HTTP est plutôt de ce type :</span><span class="sxs-lookup"><span data-stu-id="c36a7-157">If the task is complete, the HTTP response could be more like this:</span></span>

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

## <a name="data-source-connectivity-and-multi-tenancy-of-data"></a><span data-ttu-id="c36a7-158">Connectivité de la source de données \(et architecture mutualisée des données)</span><span class="sxs-lookup"><span data-stu-id="c36a7-158">Data source connectivity \(and multi-tenancy of data)</span></span>

<span data-ttu-id="c36a7-159">Bien que la quasi-totalité des artefacts du fichier .pbix soient importés dans notre espace de travail, les informations d’identification des sources de données ne le sont pas.</span><span class="sxs-lookup"><span data-stu-id="c36a7-159">While almost all of the artifacts in .pbix file are imported into our workspace, the  credentials for data sources are not.</span></span> <span data-ttu-id="c36a7-160">Par conséquent, lorsque vous utilisez le **mode DirectQuery**, le rapport incorporé ne peut pas s’afficher correctement.</span><span class="sxs-lookup"><span data-stu-id="c36a7-160">As a result, when using **DirectQuery mode**, the embedded report cannot be shown correctly.</span></span> <span data-ttu-id="c36a7-161">Mais lorsque nous utilisons le **mode Import**, nous pouvons afficher le rapport avec les données importées existantes.</span><span class="sxs-lookup"><span data-stu-id="c36a7-161">But, when using **Import mode**, we can view the report using the existing imported data.</span></span> <span data-ttu-id="c36a7-162">Dans ce cas, nous devons définir les informations d’identification en procédant comme suit au moyen d’appels REST.</span><span class="sxs-lookup"><span data-stu-id="c36a7-162">In such a case, we must set the credential using the following steps via REST calls.</span></span>

<span data-ttu-id="c36a7-163">Tout d’abord, nous devons obtenir la source de données de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="c36a7-163">First, we must get the gateway datasource.</span></span> <span data-ttu-id="c36a7-164">Nous savons que **l’ID** du jeu de données est l’ID renvoyé précédemment.</span><span class="sxs-lookup"><span data-stu-id="c36a7-164">We know the dataset **id** is the previously returned id.</span></span>

<span data-ttu-id="c36a7-165">**Demande HTTP**</span><span class="sxs-lookup"><span data-stu-id="c36a7-165">**HTTP Request**</span></span>

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/datasets/458e0451-7215-4029-80b3-9627bf3417b0/Default.GetBoundGatewayDatasources
Authorization: AppKey MpaUgrTv5e...
```

<span data-ttu-id="c36a7-166">**Réponse HTTP**</span><span class="sxs-lookup"><span data-stu-id="c36a7-166">**HTTP Response**</span></span>

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

<span data-ttu-id="c36a7-167">À l’aide de l’ID de la passerelle et de l’ID de la source de données renvoyés \(voir les précédents **gatewayId** et **id** dans le résultat renvoyé), nous pouvons modifier les informations d’identification de cette source de données comme suit :</span><span class="sxs-lookup"><span data-stu-id="c36a7-167">Using the returned gateway id and datasource id \(see the previous **gatewayId** and **id** in the returned result), we can change the credential of this datasource as follows:</span></span>

<span data-ttu-id="c36a7-168">**Demande HTTP**</span><span class="sxs-lookup"><span data-stu-id="c36a7-168">**HTTP Request**</span></span>

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

<span data-ttu-id="c36a7-169">**Réponse HTTP**</span><span class="sxs-lookup"><span data-stu-id="c36a7-169">**HTTP Response**</span></span>

```
HTTP/1.1 200 OK
Content-Type: application/octet-stream
RequestId: 0e533c13-266a-4a9d-8718-fdad90391099
```

<span data-ttu-id="c36a7-170">En production, nous pouvons également définir la chaîne de connexion de chaque espace de travail avec l’API REST.</span><span class="sxs-lookup"><span data-stu-id="c36a7-170">In production, we can also set the different connection string for each workspace using REST API.</span></span> <span data-ttu-id="c36a7-171">\(autrement dit, nous pouvons séparer la base de données pour chaque client).</span><span class="sxs-lookup"><span data-stu-id="c36a7-171">\(i.e, we can separate the database for each customers.)</span></span>

<span data-ttu-id="c36a7-172">La commande suivante change la chaîne de connexion de la source de données avec REST.</span><span class="sxs-lookup"><span data-stu-id="c36a7-172">The following is changing the connection string of datasource via REST.</span></span>

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/datasets/458e0451-7215-4029-80b3-9627bf3417b0/Default.SetAllConnections
Authorization: AppKey MpaUgrTv5e...
Content-Type: application/json; charset=utf-8

{
  "connectionString": "data source=testserver02.database.windows.net;initial catalog=testdb02;persist security info=True;encrypt=True;trustservercertificate=False"
}
```

<span data-ttu-id="c36a7-173">Nous pouvons également utiliser la sécurité au niveau de la ligne dans Power BI Embedded et séparer les données de tous les utilisateurs dans un rapport.</span><span class="sxs-lookup"><span data-stu-id="c36a7-173">Or, we can use Row Level Security in Power BI Embedded and we can separate the data for each users in one report.</span></span> <span data-ttu-id="c36a7-174">Par conséquent, nous pouvons attribuer à chaque rapport client le même .pbix \(interface utilisateur, etc.) et différentes sources de données.</span><span class="sxs-lookup"><span data-stu-id="c36a7-174">As a result, we can provision each customer report with same .pbix \(UI, etc.) and different data sources.</span></span>

> [!NOTE]
> <span data-ttu-id="c36a7-175">Si vous utilisez le **mode Import** au lieu du **mode DirectQuery**, il est impossible d’actualiser les modèles avec l’API.</span><span class="sxs-lookup"><span data-stu-id="c36a7-175">If you’re using **Import mode** instead of **DirectQuery mode**, there’s no way to refresh models via API.</span></span> <span data-ttu-id="c36a7-176">Et les sources de données locales à travers la passerelle Power BI ne sont pas encore prises en charge dans Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="c36a7-176">And, on-premises datasources through Power BI gateway isn't yet supported in Power BI Embedded.</span></span> <span data-ttu-id="c36a7-177">Toutefois, il est très intéressant de consulter le [blog Power BI](https://powerbi.microsoft.com/blog/) pour connaître les nouveautés et le contenu des futures versions.</span><span class="sxs-lookup"><span data-stu-id="c36a7-177">However, you'll really want to keep an eye on the [Power BI blog](https://powerbi.microsoft.com/blog/) for what's new and what's coming in future releases.</span></span>

## <a name="authentication-and-hosting-embedding-reports-in-our-web-page"></a><span data-ttu-id="c36a7-178">Authentification et hébergement (incorporation) de rapports dans notre page web</span><span class="sxs-lookup"><span data-stu-id="c36a7-178">Authentication and hosting (embedding) reports in our web page</span></span>

<span data-ttu-id="c36a7-179">Dans l’API REST précédente, nous pouvons utiliser la clé d’accès **AppKey** elle-même en tant qu’en-tête d’autorisation.</span><span class="sxs-lookup"><span data-stu-id="c36a7-179">In the previous REST API, we can use the access key **AppKey** itself as the authorization header.</span></span> <span data-ttu-id="c36a7-180">Ces appels pouvant être gérés du côté du serveur principal, cette procédure est sécurisée.</span><span class="sxs-lookup"><span data-stu-id="c36a7-180">Because these calls can be handled on the backend server side, it's safe.</span></span>

<span data-ttu-id="c36a7-181">Toutefois, lorsque nous incorporons le rapport dans notre page web, ce type d’informations de sécurité serait géré avec JavaScript \(frontal).</span><span class="sxs-lookup"><span data-stu-id="c36a7-181">But, when we embed the report in our web page, this kind of security information would be handled using JavaScript \(frontend).</span></span> <span data-ttu-id="c36a7-182">Dans ce cas, la valeur de l’en-tête d’autorisation doit être sécurisée.</span><span class="sxs-lookup"><span data-stu-id="c36a7-182">Then the authorization header value must be secured.</span></span> <span data-ttu-id="c36a7-183">Si notre clé d’accès est identifiée par un utilisateur ou du code malveillant, elle peut être utilisée pour appeler toutes les opérations.</span><span class="sxs-lookup"><span data-stu-id="c36a7-183">If our access key is discovered by a malicious user or malicious code, they can call any operations using this key.</span></span>

<span data-ttu-id="c36a7-184">Lorsque nous incorporons le rapport dans notre page web, nous devons utiliser le jeton calculé plutôt que la clé d’accès **AppKey**.</span><span class="sxs-lookup"><span data-stu-id="c36a7-184">When we embed the report in our web page, we must use the computed token instead of access key **AppKey**.</span></span> <span data-ttu-id="c36a7-185">Notre application doit créer le jeton OAuth Json Web Token \(JWT), qui se compose des revendications et de la signature numérique calculée.</span><span class="sxs-lookup"><span data-stu-id="c36a7-185">Our application must create the OAuth Json Web Token \(JWT) which consists of the claims and the computed digital signature.</span></span> <span data-ttu-id="c36a7-186">Comme illustré ci-dessous, cet OAuth JWT est un ensemble de tokens de chaînes encodés délimités par des points.</span><span class="sxs-lookup"><span data-stu-id="c36a7-186">As illustrated below, this OAuth JWT is dot-delimited encoded string tokens.</span></span>

![](media/power-bi-embedded-iframe/oauth-jwt.png)

<span data-ttu-id="c36a7-187">Tout d’abord, nous devons préparer la valeur d’entrée, qui est signée ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="c36a7-187">First, we must prepare the input value, which is signed later.</span></span> <span data-ttu-id="c36a7-188">Cette valeur est la chaîne d’URL (rfc4648) encodée en base64 de l’objet JSON suivant. Elles sont délimitées par le caractère point \(.).</span><span class="sxs-lookup"><span data-stu-id="c36a7-188">This value is the base64 url encoded (rfc4648) string of the following json, and these are delimited by the dot \(.) character.</span></span> <span data-ttu-id="c36a7-189">Plus tard, nous expliquerons comment obtenir l’ID du rapport.</span><span class="sxs-lookup"><span data-stu-id="c36a7-189">Later, we'll explain how to get the report id.</span></span>

> [!NOTE]
> <span data-ttu-id="c36a7-190">Si nous souhaitons utiliser la sécurité au niveau des lignes (RLS) avec Power BI Embedded, nous devons également spécifier un **nom d’utilisateur** et des **rôles** dans les revendications.</span><span class="sxs-lookup"><span data-stu-id="c36a7-190">If we want to use Row Level Security (RLS) with Power BI Embedded, we must also specify **username** and **roles** in the claims.</span></span>

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

<span data-ttu-id="c36a7-191">Ensuite, nous devons créer la chaîne encodée en base64 du code HMAC \(la signature) avec l’algorithme SHA256.</span><span class="sxs-lookup"><span data-stu-id="c36a7-191">Next, we must create the base64 encoded string of HMAC \(the signature) with SHA256 algorithm.</span></span> <span data-ttu-id="c36a7-192">Cette valeur d’entrée signée est la chaîne précédente.</span><span class="sxs-lookup"><span data-stu-id="c36a7-192">This signed input value is the previous string.</span></span>

<span data-ttu-id="c36a7-193">En dernier lieu, nous devons associer la valeur d’entrée et la chaîne de signature avec le point \(.).</span><span class="sxs-lookup"><span data-stu-id="c36a7-193">Last, we must combine the input value and signature string using period \(.) character.</span></span> <span data-ttu-id="c36a7-194">La chaîne terminée est le jeton d’application pour l’incorporation de rapports.</span><span class="sxs-lookup"><span data-stu-id="c36a7-194">The completed string is the app token for the report embedding.</span></span> <span data-ttu-id="c36a7-195">Même si le jeton d’application est identifié par un utilisateur malveillant, celui-ci ne pourra pas obtenir la clé d’accès d’origine.</span><span class="sxs-lookup"><span data-stu-id="c36a7-195">Even if the app token is discovered by a malicious user, they cannot get the original access key.</span></span> <span data-ttu-id="c36a7-196">Ce jeton d’application expirera rapidement.</span><span class="sxs-lookup"><span data-stu-id="c36a7-196">This app token will expire quickly.</span></span>

<span data-ttu-id="c36a7-197">Voici un exemple PHP de ces étapes :</span><span class="sxs-lookup"><span data-stu-id="c36a7-197">Here's a PHP example for these steps:</span></span>

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

// 4. show result (which is the apptoken)
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

## <a name="finally-embed-the-report-into-the-web-page"></a><span data-ttu-id="c36a7-198">Dernière étape : intégration du rapport dans la page web</span><span class="sxs-lookup"><span data-stu-id="c36a7-198">Finally, embed the report into the web page</span></span>

<span data-ttu-id="c36a7-199">Pour incorporer notre rapport, nous devons récupérer l’URL d’incorporation et **l’ID** de rapport avec l’API REST suivante.</span><span class="sxs-lookup"><span data-stu-id="c36a7-199">For embedding our report, we must get the embed url and report **id** using the following REST API.</span></span>

<span data-ttu-id="c36a7-200">**Demande HTTP**</span><span class="sxs-lookup"><span data-stu-id="c36a7-200">**HTTP Request**</span></span>

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/reports
Authorization: AppKey MpaUgrTv5e...
```

<span data-ttu-id="c36a7-201">**Réponse HTTP**</span><span class="sxs-lookup"><span data-stu-id="c36a7-201">**HTTP Response**</span></span>

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

<span data-ttu-id="c36a7-202">Nous pouvons intégrer le rapport dans notre application web à l’aide du jeton d’application précédent.</span><span class="sxs-lookup"><span data-stu-id="c36a7-202">We can embed the report in our web app using the previous app token.</span></span>
<span data-ttu-id="c36a7-203">Si nous examinons l’exemple de code suivant, la première partie est la même que l’exemple précédent.</span><span class="sxs-lookup"><span data-stu-id="c36a7-203">If we look at the next sample code, the former part is the same as the previous example.</span></span> <span data-ttu-id="c36a7-204">Dans la dernière partie, cet exemple montre **embedUrl** \(voir le résultat précédent) dans l’iframe et publie le jeton d’application dans l’iframe.</span><span class="sxs-lookup"><span data-stu-id="c36a7-204">In the latter part, this sample shows the **embedUrl** \(see the previous result) in the iframe, and is posting the app token into the iframe.</span></span>

> [!NOTE]
> <span data-ttu-id="c36a7-205">Vous devez modifier la valeur de l’ID de rapport à votre convenance.</span><span class="sxs-lookup"><span data-stu-id="c36a7-205">You'll need to change the report id value to one of your own.</span></span> <span data-ttu-id="c36a7-206">En outre, en raison d’un bogue dans notre système de gestion de contenu, la balise iframe dans l’exemple de code est lue littéralement.</span><span class="sxs-lookup"><span data-stu-id="c36a7-206">Also, due to a bug in our content management system, the iframe tag in the code sample is read literally.</span></span> <span data-ttu-id="c36a7-207">Supprimez le texte encapsulé de la balise si vous copiez-collez le code suivant.</span><span class="sxs-lookup"><span data-stu-id="c36a7-207">Remove the capped text from the tag if you copy and paste this sample code.</span></span>

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

<span data-ttu-id="c36a7-208">Et voici notre résultat :</span><span class="sxs-lookup"><span data-stu-id="c36a7-208">And here's our result:</span></span>

![](media/power-bi-embedded-iframe/view-report.png)

<span data-ttu-id="c36a7-209">À ce stade, Power BI Embedded affiche uniquement le rapport dans l’iframe.</span><span class="sxs-lookup"><span data-stu-id="c36a7-209">At this time, Power BI Embedded only shows the report in the iframe.</span></span> <span data-ttu-id="c36a7-210">Mais gardez un œil sur le [blog Power BI](https://powerbi.microsoft.com/blog/).</span><span class="sxs-lookup"><span data-stu-id="c36a7-210">But, keep an eye on the [Power BI Blog](https://powerbi.microsoft.com/blog/).</span></span> <span data-ttu-id="c36a7-211">Des améliorations à venir pourraient utiliser de nouvelles API côté client qui nous permettront d’envoyer des informations dans l’iframe ainsi que de récupérer des informations.</span><span class="sxs-lookup"><span data-stu-id="c36a7-211">Future improvements could use new client side APIs that will let us send information into the iframe as well as get information out.</span></span> <span data-ttu-id="c36a7-212">C’est très intéressant !</span><span class="sxs-lookup"><span data-stu-id="c36a7-212">Exciting stuff!</span></span>

## <a name="see-also"></a><span data-ttu-id="c36a7-213">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="c36a7-213">See also</span></span>
* [<span data-ttu-id="c36a7-214">Authentification et autorisation dans Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="c36a7-214">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)

<span data-ttu-id="c36a7-215">Des questions ?</span><span class="sxs-lookup"><span data-stu-id="c36a7-215">More questions?</span></span> [<span data-ttu-id="c36a7-216">Essayer la communauté Power BI</span><span class="sxs-lookup"><span data-stu-id="c36a7-216">Try the Power BI Community</span></span>](http://community.powerbi.com/)

