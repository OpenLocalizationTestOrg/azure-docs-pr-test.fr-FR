---
title: "Démarrage rapide : API Azure Machine Learning Recommendations (version 1)| Microsoft Docs"
description: "Azure Machine Learning Recommendations - Guide de démarrage rapide"
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: 5bce1a4a-1ad6-473f-812b-84f800fdc09a
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: luisca
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: True
ms.openlocfilehash: d8f98e85f723a1104cb169b26d797934140979f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="quick-start-guide-for-hello-machine-learning-recommendations-api-version-1"></a><span data-ttu-id="00f10-104">Guide de démarrage rapide de hello Machine Learning recommandations API (version 1)</span><span class="sxs-lookup"><span data-stu-id="00f10-104">Quick start guide for hello Machine Learning Recommendations API (version 1)</span></span>

> [!NOTE]
> <span data-ttu-id="00f10-105">Vous devez commencer à l’aide de hello [Service cognitifs de recommandations API](https://www.microsoft.com/cognitive-services/recommendations-api) au lieu de cette version.</span><span class="sxs-lookup"><span data-stu-id="00f10-105">You should start using hello [Recommendations API Cognitive Service](https://www.microsoft.com/cognitive-services/recommendations-api) instead of this version.</span></span> <span data-ttu-id="00f10-106">Hello Service cognitifs recommandations remplacera ce service et toutes les hello nouvelles fonctionnalités seront développées il.</span><span class="sxs-lookup"><span data-stu-id="00f10-106">hello Recommendations Cognitive Service will be replacing this service, and all hello new features will be developed there.</span></span> <span data-ttu-id="00f10-107">Il propose de nouvelles fonctionnalités telles que la prise en charge du traitement par lot, un meilleur Explorateur d’API, une surface d’API plus propre, une expérience d’inscription/de facturation plus cohérente, etc.</span><span class="sxs-lookup"><span data-stu-id="00f10-107">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span></span>
>
> <span data-ttu-id="00f10-108">En savoir plus sur [migration toohello nouveau Service cognitifs](http://aka.ms/recomigrate).</span><span class="sxs-lookup"><span data-stu-id="00f10-108">Learn more about [Migrating toohello new Cognitive Service](http://aka.ms/recomigrate).</span></span>
> 
> 

<span data-ttu-id="00f10-109">Ce document décrit comment tooonboard votre toouse service ou d’application Microsoft Azure Machine Learning recommandations.</span><span class="sxs-lookup"><span data-stu-id="00f10-109">This document describes how tooonboard your service or application toouse Microsoft Azure Machine Learning Recommendations.</span></span> <span data-ttu-id="00f10-110">Vous trouverez plus d’informations sur hello recommandations API Bonjour [Cortana Intelligence galerie](https://gallery.cortanaintelligence.com/MachineLearningAPIs/Recommendations-2).</span><span class="sxs-lookup"><span data-stu-id="00f10-110">You can find more details on hello Recommendations API in hello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/MachineLearningAPIs/Recommendations-2).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="general-overview"></a><span data-ttu-id="00f10-111">Présentation générale</span><span class="sxs-lookup"><span data-stu-id="00f10-111">General overview</span></span>
<span data-ttu-id="00f10-112">toouse Azure Machine Learning recommandations, vous devez hello tootake comme suit :</span><span class="sxs-lookup"><span data-stu-id="00f10-112">toouse Azure Machine Learning Recommendations, you need tootake hello following steps:</span></span>

* <span data-ttu-id="00f10-113">Créer un modèle, un modèle est un conteneur de vos données d’utilisation, les données de catalogue et modèle de recommandation hello.</span><span class="sxs-lookup"><span data-stu-id="00f10-113">Create a model - A model is a container of your usage data, catalog data, and hello recommendation model.</span></span>
* <span data-ttu-id="00f10-114">Données du catalogue d’importation - un catalogue contient des informations de métadonnées sur les éléments de hello.</span><span class="sxs-lookup"><span data-stu-id="00f10-114">Import catalog data - A catalog contains metadata information on hello items.</span></span> 
* <span data-ttu-id="00f10-115">Importez des données d’utilisation : les données d’utilisation peuvent être téléchargées de l’une des deux (ou des deux) manières suivantes :</span><span class="sxs-lookup"><span data-stu-id="00f10-115">Import usage data - Usage data can be uploaded in one of two ways (or both):</span></span>
  * <span data-ttu-id="00f10-116">En téléchargeant un fichier qui contient les données d’utilisation hello.</span><span class="sxs-lookup"><span data-stu-id="00f10-116">By uploading a file that contains hello usage data.</span></span>
  * <span data-ttu-id="00f10-117">En envoyant des événements d’acquisition de données.</span><span class="sxs-lookup"><span data-stu-id="00f10-117">By sending data acquisition events.</span></span>
    <span data-ttu-id="00f10-118">En général vous téléchargez un fichier d’utilisation dans l’ordre toobe toocreate en mesure d’un modèle de recommandation initiale (démarrage) et l’utiliser jusqu'à ce que le système de hello rassemble suffisamment de données à l’aide du format d’acquisition de données hello.</span><span class="sxs-lookup"><span data-stu-id="00f10-118">Usually you upload a usage file in order toobe able toocreate an initial recommendation model (bootstrap) and use it until hello system gathers enough data by using hello data acquisition format.</span></span>
* <span data-ttu-id="00f10-119">Générer un modèle de recommandation : il s’agit d’une opération asynchrone qui Bonjour système de recommandation prend toutes les données d’utilisation hello et crée un modèle de recommandation.</span><span class="sxs-lookup"><span data-stu-id="00f10-119">Build a recommendation model - This is an asynchronous operation in which hello recommendation system takes all hello usage data and creates a recommendation model.</span></span> <span data-ttu-id="00f10-120">Cette opération peut prendre plusieurs minutes ou plusieurs heures en fonction de hello la taille des données de hello et hello générer les paramètres de configuration.</span><span class="sxs-lookup"><span data-stu-id="00f10-120">This operation can take several minutes or several hours depending on hello size of hello data and hello build configuration parameters.</span></span> <span data-ttu-id="00f10-121">Lors du déclenchement de génération de hello, vous obtenez un ID de génération.</span><span class="sxs-lookup"><span data-stu-id="00f10-121">When triggering hello build, you will get a build ID.</span></span> <span data-ttu-id="00f10-122">Utiliser toocheck lorsque le processus de génération hello est terminée avant de démarrer tooconsume recommandations.</span><span class="sxs-lookup"><span data-stu-id="00f10-122">Use it toocheck when hello build process has ended before starting tooconsume recommendations.</span></span>
* <span data-ttu-id="00f10-123">Utilisez les recommandations : obtenez des recommandations pour un élément spécifique ou pour une liste d’éléments.</span><span class="sxs-lookup"><span data-stu-id="00f10-123">Consume recommendations - Get recommendations for a specific item or list of items.</span></span>

<span data-ttu-id="00f10-124">Toutes les étapes de hello ci-dessus sont effectuées via hello Azure Machine Learning recommandations API.</span><span class="sxs-lookup"><span data-stu-id="00f10-124">All hello steps above are done through hello Azure Machine Learning Recommendations API.</span></span>  <span data-ttu-id="00f10-125">Vous pouvez télécharger un exemple d’application qui implémente chacune de ces étapes à partir de hello [galerie également.](http://1drv.ms/1xeO2F3)</span><span class="sxs-lookup"><span data-stu-id="00f10-125">You can download a sample application that implements each of these steps from hello [gallery as well.](http://1drv.ms/1xeO2F3)</span></span>

## <a name="limitations"></a><span data-ttu-id="00f10-126">Limites</span><span class="sxs-lookup"><span data-stu-id="00f10-126">Limitations</span></span>
* <span data-ttu-id="00f10-127">nombre maximal de Hello de modèles par abonnement est 10.</span><span class="sxs-lookup"><span data-stu-id="00f10-127">hello maximum number of models per subscription is 10.</span></span>
* <span data-ttu-id="00f10-128">nombre maximal de Hello d’éléments pouvant être un catalogue est 100 000.</span><span class="sxs-lookup"><span data-stu-id="00f10-128">hello maximum number of items that a catalog can hold is 100,000.</span></span>
* <span data-ttu-id="00f10-129">nombre maximal de Hello de points d’utilisation qui sont conservés est ~ 5 000 000.</span><span class="sxs-lookup"><span data-stu-id="00f10-129">hello maximum number of usage points that are kept is ~5,000,000.</span></span> <span data-ttu-id="00f10-130">Hello plus ancien est supprimé si nouveaux sera téléchargé ou signalé.</span><span class="sxs-lookup"><span data-stu-id="00f10-130">hello oldest will be deleted if new ones will be uploaded or reported.</span></span>
* <span data-ttu-id="00f10-131">taille maximale de Hello des données qui peuvent être envoyées dans la publication (par exemple, importation de données du catalogue, importer des données d’utilisation) est de 200 Mo.</span><span class="sxs-lookup"><span data-stu-id="00f10-131">hello maximum size of data that can be sent in POST (for example, import catalog data, import usage data) is 200MB.</span></span>
* <span data-ttu-id="00f10-132">Bonjour nombre de transactions par seconde pour une génération de modèle de recommandation n’est pas active est ~ 2TPS.</span><span class="sxs-lookup"><span data-stu-id="00f10-132">hello number of transactions per second for a recommendation model build that is not active is ~2TPS.</span></span> <span data-ttu-id="00f10-133">Une génération de modèle de recommandation est active peut contenir jusqu'à too20TPS.</span><span class="sxs-lookup"><span data-stu-id="00f10-133">A recommendation model build that is active can hold up too20TPS.</span></span>

## <a name="integration"></a><span data-ttu-id="00f10-134">Intégration</span><span class="sxs-lookup"><span data-stu-id="00f10-134">Integration</span></span>
### <a name="authentication"></a><span data-ttu-id="00f10-135">Authentification</span><span class="sxs-lookup"><span data-stu-id="00f10-135">Authentication</span></span>
<span data-ttu-id="00f10-136">Microsoft Azure Marketplace prend en charge une méthode d’authentification de base ou OAuth hello.</span><span class="sxs-lookup"><span data-stu-id="00f10-136">Microsoft Azure Marketplace supports either hello Basic or OAuth authentication method.</span></span> <span data-ttu-id="00f10-137">Vous pouvez rechercher facilement hello clés de compte en accédant clés toohello dans marketplace hello sous [vos paramètres de compte](https://datamarket.azure.com/account/keys).</span><span class="sxs-lookup"><span data-stu-id="00f10-137">You can easily find hello account keys by navigating toohello keys in hello marketplace under [your account settings](https://datamarket.azure.com/account/keys).</span></span> 

#### <a name="basic-authentication"></a><span data-ttu-id="00f10-138">Authentification de base</span><span class="sxs-lookup"><span data-stu-id="00f10-138">Basic Authentication</span></span>
<span data-ttu-id="00f10-139">Ajoutez l’en-tête d’autorisation hello :</span><span class="sxs-lookup"><span data-stu-id="00f10-139">Add hello Authorization header:</span></span>

    Authorization: Basic <creds>

    Where <creds> = ConvertToBase64("AccountKey:" + yourAccountKey);  

<span data-ttu-id="00f10-140">Convertir tooBase64 (c#)</span><span class="sxs-lookup"><span data-stu-id="00f10-140">Convert tooBase64 (C#)</span></span>

    var bytes = Encoding.UTF8.GetBytes("AccountKey:" + yourAccountKey);
    var creds = Convert.ToBase64String(bytes);

<span data-ttu-id="00f10-141">Convertir tooBase64 (JavaScript)</span><span class="sxs-lookup"><span data-stu-id="00f10-141">Convert tooBase64 (JavaScript)</span></span>

    var creds = window.btoa("AccountKey" + ":" + yourAccountKey);




### <a name="service-uri"></a><span data-ttu-id="00f10-142">URI de service</span><span class="sxs-lookup"><span data-stu-id="00f10-142">Service URI</span></span>
<span data-ttu-id="00f10-143">URI de racine de service Hello pour hello Azure Machine Learning recommandations API est [ici.](https://api.datamarket.azure.com/amla/recommendations/v2/)</span><span class="sxs-lookup"><span data-stu-id="00f10-143">hello service root URI for hello Azure Machine Learning Recommendations APIs is [here.](https://api.datamarket.azure.com/amla/recommendations/v2/)</span></span>

<span data-ttu-id="00f10-144">URI de service complet Hello est exprimée à l’aide des éléments de spécification d’OData hello.</span><span class="sxs-lookup"><span data-stu-id="00f10-144">hello full service URI is expressed using elements of hello OData specification.</span></span>

### <a name="api-version"></a><span data-ttu-id="00f10-145">Version de l'API</span><span class="sxs-lookup"><span data-stu-id="00f10-145">API version</span></span>
<span data-ttu-id="00f10-146">Chaque appel d’API aura, à la fin de hello, un paramètre de requête appelé apiVersion qui doit être définie trop « 1.0 ».</span><span class="sxs-lookup"><span data-stu-id="00f10-146">Each API call will have, at hello end, a query parameter called apiVersion that should be set too"1.0".</span></span>

### <a name="ids-are-case-sensitive"></a><span data-ttu-id="00f10-147">Respect de la casse des ID</span><span class="sxs-lookup"><span data-stu-id="00f10-147">IDs are case-sensitive</span></span>
<span data-ttu-id="00f10-148">ID, retournés par une des API, de hello respectent la casse et doivent être utilisées comme telles lorsqu’il est passé en tant que paramètres dans les appels d’API suivants.</span><span class="sxs-lookup"><span data-stu-id="00f10-148">IDs, returned by any of hello APIs, are case-sensitive and should be used as such when passed as parameters in subsequent API calls.</span></span> <span data-ttu-id="00f10-149">Par exemple, les ID de modèle et de catalogue respectent la casse.</span><span class="sxs-lookup"><span data-stu-id="00f10-149">For instance, model IDs and catalog IDs are case-sensitive.</span></span>

### <a name="create-a-model"></a><span data-ttu-id="00f10-150">Création d’un modèle</span><span class="sxs-lookup"><span data-stu-id="00f10-150">Create a model</span></span>
<span data-ttu-id="00f10-151">Création d'une requête « Créer un modèle » :</span><span class="sxs-lookup"><span data-stu-id="00f10-151">Creating a "create model" request:</span></span>

| <span data-ttu-id="00f10-152">Méthode HTTP</span><span class="sxs-lookup"><span data-stu-id="00f10-152">HTTP Method</span></span> | <span data-ttu-id="00f10-153">URI</span><span class="sxs-lookup"><span data-stu-id="00f10-153">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="00f10-154">POST</span><span class="sxs-lookup"><span data-stu-id="00f10-154">POST</span></span> |`<rootURI>/CreateModel?modelName=%27<model_name>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="00f10-155">Exemple :</span><span class="sxs-lookup"><span data-stu-id="00f10-155">Example:</span></span><br>`<rootURI>/CreateModel?modelName=%27MyFirstModel%27&apiVersion=%271.0%27` |

| <span data-ttu-id="00f10-156">Nom du paramètre</span><span class="sxs-lookup"><span data-stu-id="00f10-156">Parameter Name</span></span> | <span data-ttu-id="00f10-157">Valeurs valides</span><span class="sxs-lookup"><span data-stu-id="00f10-157">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="00f10-158">modelName</span><span class="sxs-lookup"><span data-stu-id="00f10-158">modelName</span></span> |<span data-ttu-id="00f10-159">Seuls les lettres (A-Z, a-z), les chiffres (0-9), les tirets (-) et les traits de soulignement (_) sont autorisés.</span><span class="sxs-lookup"><span data-stu-id="00f10-159">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="00f10-160">Longueur maximale : 20</span><span class="sxs-lookup"><span data-stu-id="00f10-160">Max length: 20</span></span> |
| <span data-ttu-id="00f10-161">apiVersion</span><span class="sxs-lookup"><span data-stu-id="00f10-161">apiVersion</span></span> |<span data-ttu-id="00f10-162">1.0</span><span class="sxs-lookup"><span data-stu-id="00f10-162">1.0</span></span> |
|  | |
| <span data-ttu-id="00f10-163">Corps de la requête</span><span class="sxs-lookup"><span data-stu-id="00f10-163">Request Body</span></span> |<span data-ttu-id="00f10-164">AUCUN</span><span class="sxs-lookup"><span data-stu-id="00f10-164">NONE</span></span> |

<span data-ttu-id="00f10-165">**Réponse**:</span><span class="sxs-lookup"><span data-stu-id="00f10-165">**Response**:</span></span>

<span data-ttu-id="00f10-166">Code d'état HTTP : 200</span><span class="sxs-lookup"><span data-stu-id="00f10-166">HTTP Status code: 200</span></span>

* <span data-ttu-id="00f10-167">`feed/entry/content/properties/id`-Contient l’ID de modèle hello.</span><span class="sxs-lookup"><span data-stu-id="00f10-167">`feed/entry/content/properties/id` - Contains hello model ID.</span></span>
  <span data-ttu-id="00f10-168">Notez que l’ID de modèle hello respecte la casse.</span><span class="sxs-lookup"><span data-stu-id="00f10-168">Note that hello model ID is case-sensitive.</span></span>

<span data-ttu-id="00f10-169">OData XML</span><span class="sxs-lookup"><span data-stu-id="00f10-169">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Create A New Model</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T06:35:21Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">CreateANewModelEntity2</title>
    <updated>2014-10-05T06:35:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">a658c626-2baa-43a7-ac98-f6ee26120a12</d:Id>
        <d:Name m:type="Edm.String">MyFirstModel</d:Name>
        <d:Date m:type="Edm.String">10/5/2014 6:35:19 AM</d:Date>
        <d:Status m:type="Edm.String">Created</d:Status>
        <d:HasActiveBuild m:type="Edm.String">false</d:HasActiveBuild>
        <d:BuildId m:type="Edm.String">-1</d:BuildId>
        <d:Mpr m:type="Edm.String">0</d:Mpr>
        <d:UserName m:type="Edm.String">5-4058-ab36-1fe254f05102@dm.com</d:UserName>
        <d:Description m:type="Edm.String"></d:Description>
      </m:properties>
    </content>
      </entry>
    </feed>


### <a name="import-catalog-data"></a><span data-ttu-id="00f10-170">Importation de données de catalogue</span><span class="sxs-lookup"><span data-stu-id="00f10-170">Import catalog data</span></span>
<span data-ttu-id="00f10-171">Si vous téléchargez plusieurs catalogue fichiers toohello même modèle avec plusieurs appels, il insère uniquement hello nouveaux éléments de catalogue.</span><span class="sxs-lookup"><span data-stu-id="00f10-171">If you upload several catalog files toohello same model with several calls, we will insert only hello new catalog items.</span></span> <span data-ttu-id="00f10-172">Éléments existants resteront avec les valeurs d’origine hello.</span><span class="sxs-lookup"><span data-stu-id="00f10-172">Existing items will remain with hello original values.</span></span>

| <span data-ttu-id="00f10-173">Méthode HTTP</span><span class="sxs-lookup"><span data-stu-id="00f10-173">HTTP Method</span></span> | <span data-ttu-id="00f10-174">URI</span><span class="sxs-lookup"><span data-stu-id="00f10-174">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="00f10-175">POST</span><span class="sxs-lookup"><span data-stu-id="00f10-175">POST</span></span> |`<rootURI>/ImportCatalogFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="00f10-176">Exemple :</span><span class="sxs-lookup"><span data-stu-id="00f10-176">Example:</span></span><br>`<rootURI>/ImportCatalogFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="00f10-177">Nom du paramètre</span><span class="sxs-lookup"><span data-stu-id="00f10-177">Parameter Name</span></span> | <span data-ttu-id="00f10-178">Valeurs valides</span><span class="sxs-lookup"><span data-stu-id="00f10-178">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="00f10-179">modelId</span><span class="sxs-lookup"><span data-stu-id="00f10-179">modelId</span></span> |<span data-ttu-id="00f10-180">Identificateur unique du modèle hello (respecte la casse)</span><span class="sxs-lookup"><span data-stu-id="00f10-180">Unique identifier of hello model (case-sensitive)</span></span> |
| <span data-ttu-id="00f10-181">filename</span><span class="sxs-lookup"><span data-stu-id="00f10-181">filename</span></span> |<span data-ttu-id="00f10-182">Identificateur textuel du catalogue de hello.</span><span class="sxs-lookup"><span data-stu-id="00f10-182">Textual identifier of hello catalog.</span></span><br><span data-ttu-id="00f10-183">Seuls les lettres (A-Z, a-z), les chiffres (0-9), les tirets (-) et les traits de soulignement (_) sont autorisés.</span><span class="sxs-lookup"><span data-stu-id="00f10-183">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="00f10-184">Longueur maximale : 50</span><span class="sxs-lookup"><span data-stu-id="00f10-184">Max length: 50</span></span> |
| <span data-ttu-id="00f10-185">apiVersion</span><span class="sxs-lookup"><span data-stu-id="00f10-185">apiVersion</span></span> |<span data-ttu-id="00f10-186">1.0</span><span class="sxs-lookup"><span data-stu-id="00f10-186">1.0</span></span> |
|  | |
| <span data-ttu-id="00f10-187">Corps de la requête</span><span class="sxs-lookup"><span data-stu-id="00f10-187">Request Body</span></span> |<span data-ttu-id="00f10-188">Données de catalogue.</span><span class="sxs-lookup"><span data-stu-id="00f10-188">Catalog data.</span></span> <span data-ttu-id="00f10-189">Format :</span><span class="sxs-lookup"><span data-stu-id="00f10-189">Format:</span></span><br>`<Item Id>,<Item Name>,<Item Category>[,<description>]`<br><br><table><tr><th><span data-ttu-id="00f10-190">Nom</span><span class="sxs-lookup"><span data-stu-id="00f10-190">Name</span></span></th><th><span data-ttu-id="00f10-191">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="00f10-191">Mandatory</span></span></th><th><span data-ttu-id="00f10-192">Type</span><span class="sxs-lookup"><span data-stu-id="00f10-192">Type</span></span></th><th><span data-ttu-id="00f10-193">Description</span><span class="sxs-lookup"><span data-stu-id="00f10-193">Description</span></span></th></tr><tr><td><span data-ttu-id="00f10-194">Item Id</span><span class="sxs-lookup"><span data-stu-id="00f10-194">Item Id</span></span></td><td><span data-ttu-id="00f10-195">Oui</span><span class="sxs-lookup"><span data-stu-id="00f10-195">Yes</span></span></td><td><span data-ttu-id="00f10-196">Alphanumérique, longueur maximale : 50</span><span class="sxs-lookup"><span data-stu-id="00f10-196">Alphanumeric, max length 50</span></span></td><td><span data-ttu-id="00f10-197">Identificateur unique d’un élément</span><span class="sxs-lookup"><span data-stu-id="00f10-197">Unique identifier of an item</span></span></td></tr><tr><td><span data-ttu-id="00f10-198">Item Name</span><span class="sxs-lookup"><span data-stu-id="00f10-198">Item Name</span></span></td><td><span data-ttu-id="00f10-199">Oui</span><span class="sxs-lookup"><span data-stu-id="00f10-199">Yes</span></span></td><td><span data-ttu-id="00f10-200">Alphanumérique, longueur maximale : 255</span><span class="sxs-lookup"><span data-stu-id="00f10-200">Alphanumeric, max length 255</span></span></td><td><span data-ttu-id="00f10-201">Nom de l’élément</span><span class="sxs-lookup"><span data-stu-id="00f10-201">Item name</span></span></td></tr><tr><td><span data-ttu-id="00f10-202">Item Category</span><span class="sxs-lookup"><span data-stu-id="00f10-202">Item Category</span></span></td><td><span data-ttu-id="00f10-203">Oui</span><span class="sxs-lookup"><span data-stu-id="00f10-203">Yes</span></span></td><td><span data-ttu-id="00f10-204">Alphanumérique, longueur maximale : 255</span><span class="sxs-lookup"><span data-stu-id="00f10-204">Alphanumeric, max length 255</span></span></td><td><span data-ttu-id="00f10-205">Toowhich catégorie que cette élément appartient (par exemple, la documentation de cuisine, documentaires...)</span><span class="sxs-lookup"><span data-stu-id="00f10-205">Category toowhich this item belongs (for example, Cooking Books, Drama…)</span></span></td></tr><tr><td><span data-ttu-id="00f10-206">Description</span><span class="sxs-lookup"><span data-stu-id="00f10-206">Description</span></span></td><td><span data-ttu-id="00f10-207">Non</span><span class="sxs-lookup"><span data-stu-id="00f10-207">No</span></span></td><td><span data-ttu-id="00f10-208">Alphanumérique, longueur maximale : 4 000</span><span class="sxs-lookup"><span data-stu-id="00f10-208">Alphanumeric, max length 4000</span></span></td><td><span data-ttu-id="00f10-209">Description de cet élément</span><span class="sxs-lookup"><span data-stu-id="00f10-209">Description of this item</span></span></td></tr></table><br><span data-ttu-id="00f10-210">La taille de fichier maximale est de 200 Mo.</span><span class="sxs-lookup"><span data-stu-id="00f10-210">Maximum file size is 200MB.</span></span><br><br><span data-ttu-id="00f10-211">Exemple :</span><span class="sxs-lookup"><span data-stu-id="00f10-211">Example:</span></span><br><code>2406e770-769c-4189-89de-1c9283f93a96,Clara Callan,Book<br>21bf8088-b6c0-4509-870c-e1c7ac78304a,hello Forgetting Room: A Fiction (Byzantium Book),Book<br>3bb5cb44-d143-4bdd-a55c-443964bf4b23,Spadework,Book<br>552a1940-21e4-4399-82bb-594b46d7ed54,Restraint of Beasts,Book</code> |

<span data-ttu-id="00f10-212">**Réponse**:</span><span class="sxs-lookup"><span data-stu-id="00f10-212">**Response**:</span></span>

<span data-ttu-id="00f10-213">Code d'état HTTP : 200</span><span class="sxs-lookup"><span data-stu-id="00f10-213">HTTP Status code: 200</span></span>

* <span data-ttu-id="00f10-214">`Feed\entry\content\properties\LineCount` : nombre de lignes acceptées.</span><span class="sxs-lookup"><span data-stu-id="00f10-214">`Feed\entry\content\properties\LineCount` - Number of lines accepted.</span></span>
* <span data-ttu-id="00f10-215">`Feed\entry\content\properties\ErrorCount`-Nombre de lignes qui n’ont pas été ajoutés en raison de l’erreur de tooan.</span><span class="sxs-lookup"><span data-stu-id="00f10-215">`Feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due tooan error.</span></span>

<span data-ttu-id="00f10-216">OData XML</span><span class="sxs-lookup"><span data-stu-id="00f10-216">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
          <subtitle type="text">Import catalog file</subtitle>
          <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T06:58:04Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">ImportCatalogFileEntity2</title>
    <updated>2014-10-05T06:58:04Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:LineCount m:type="Edm.String">4</d:LineCount>
        <d:ErrorCount m:type="Edm.String">0</d:ErrorCount>
      </m:properties>
    </content>
      </entry>
    </feed>


### <a name="import-usage-data"></a><span data-ttu-id="00f10-217">Importation de données d'utilisation</span><span class="sxs-lookup"><span data-stu-id="00f10-217">Import usage data</span></span>
#### <a name="uploading-a-file"></a><span data-ttu-id="00f10-218">Téléchargement d’un fichier</span><span class="sxs-lookup"><span data-stu-id="00f10-218">Uploading a file</span></span>
<span data-ttu-id="00f10-219">Cette section montre comment les données d’utilisation tooupload à l’aide d’un fichier.</span><span class="sxs-lookup"><span data-stu-id="00f10-219">This section shows how tooupload usage data by using a file.</span></span> <span data-ttu-id="00f10-220">Vous pouvez appeler cette API plusieurs fois avec les données d'utilisation.</span><span class="sxs-lookup"><span data-stu-id="00f10-220">You can call this API several times with usage data.</span></span> <span data-ttu-id="00f10-221">Toutes les données d'utilisation sont enregistrées pour tous les appels.</span><span class="sxs-lookup"><span data-stu-id="00f10-221">All usage data will be saved for all calls.</span></span>

| <span data-ttu-id="00f10-222">Méthode HTTP</span><span class="sxs-lookup"><span data-stu-id="00f10-222">HTTP Method</span></span> | <span data-ttu-id="00f10-223">URI</span><span class="sxs-lookup"><span data-stu-id="00f10-223">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="00f10-224">POST</span><span class="sxs-lookup"><span data-stu-id="00f10-224">POST</span></span> |`<rootURI>/ImportUsageFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="00f10-225">Exemple :</span><span class="sxs-lookup"><span data-stu-id="00f10-225">Example:</span></span><br>`<rootURI>/ImportUsageFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27ImplicitMatrix10_Guid_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="00f10-226">Nom du paramètre</span><span class="sxs-lookup"><span data-stu-id="00f10-226">Parameter Name</span></span> | <span data-ttu-id="00f10-227">Valeurs valides</span><span class="sxs-lookup"><span data-stu-id="00f10-227">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="00f10-228">modelId</span><span class="sxs-lookup"><span data-stu-id="00f10-228">modelId</span></span> |<span data-ttu-id="00f10-229">Identificateur unique du modèle hello (respecte la casse)</span><span class="sxs-lookup"><span data-stu-id="00f10-229">Unique identifier of hello model (case-sensitive)</span></span> |
| <span data-ttu-id="00f10-230">filename</span><span class="sxs-lookup"><span data-stu-id="00f10-230">filename</span></span> |<span data-ttu-id="00f10-231">Identificateur textuel du catalogue de hello.</span><span class="sxs-lookup"><span data-stu-id="00f10-231">Textual identifier of hello catalog.</span></span><br><span data-ttu-id="00f10-232">Seuls les lettres (A-Z, a-z), les chiffres (0-9), les tirets (-) et les traits de soulignement (_) sont autorisés.</span><span class="sxs-lookup"><span data-stu-id="00f10-232">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="00f10-233">Longueur maximale : 50</span><span class="sxs-lookup"><span data-stu-id="00f10-233">Max length: 50</span></span> |
| <span data-ttu-id="00f10-234">apiVersion</span><span class="sxs-lookup"><span data-stu-id="00f10-234">apiVersion</span></span> |<span data-ttu-id="00f10-235">1.0</span><span class="sxs-lookup"><span data-stu-id="00f10-235">1.0</span></span> |
|  | |
| <span data-ttu-id="00f10-236">Corps de la requête</span><span class="sxs-lookup"><span data-stu-id="00f10-236">Request Body</span></span> |<span data-ttu-id="00f10-237">Données d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="00f10-237">Usage data.</span></span> <span data-ttu-id="00f10-238">Format :</span><span class="sxs-lookup"><span data-stu-id="00f10-238">Format:</span></span><br>`<User Id>,<Item Id>[,<Time>,<Event>]`<br><br><table><tr><th><span data-ttu-id="00f10-239">Nom</span><span class="sxs-lookup"><span data-stu-id="00f10-239">Name</span></span></th><th><span data-ttu-id="00f10-240">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="00f10-240">Mandatory</span></span></th><th><span data-ttu-id="00f10-241">Type</span><span class="sxs-lookup"><span data-stu-id="00f10-241">Type</span></span></th><th><span data-ttu-id="00f10-242">Description</span><span class="sxs-lookup"><span data-stu-id="00f10-242">Description</span></span></th></tr><tr><td><span data-ttu-id="00f10-243">User Id</span><span class="sxs-lookup"><span data-stu-id="00f10-243">User Id</span></span></td><td><span data-ttu-id="00f10-244">Oui</span><span class="sxs-lookup"><span data-stu-id="00f10-244">Yes</span></span></td><td><span data-ttu-id="00f10-245">Alphanumérique</span><span class="sxs-lookup"><span data-stu-id="00f10-245">Alphanumeric</span></span></td><td><span data-ttu-id="00f10-246">Identificateur unique d’un utilisateur</span><span class="sxs-lookup"><span data-stu-id="00f10-246">Unique identifier of a user</span></span></td></tr><tr><td><span data-ttu-id="00f10-247">Item Id</span><span class="sxs-lookup"><span data-stu-id="00f10-247">Item Id</span></span></td><td><span data-ttu-id="00f10-248">Oui</span><span class="sxs-lookup"><span data-stu-id="00f10-248">Yes</span></span></td><td><span data-ttu-id="00f10-249">Alphanumérique, longueur maximale : 50</span><span class="sxs-lookup"><span data-stu-id="00f10-249">Alphanumeric, max length 50</span></span></td><td><span data-ttu-id="00f10-250">Identificateur unique d’un élément</span><span class="sxs-lookup"><span data-stu-id="00f10-250">Unique identifier of an item</span></span></td></tr><tr><td><span data-ttu-id="00f10-251">Time</span><span class="sxs-lookup"><span data-stu-id="00f10-251">Time</span></span></td><td><span data-ttu-id="00f10-252">Non</span><span class="sxs-lookup"><span data-stu-id="00f10-252">No</span></span></td><td><span data-ttu-id="00f10-253">Date au format suivant : AAAA/MM/JJTHH:MM:SS (par exemple, 2013/06/20T10:00:00)</span><span class="sxs-lookup"><span data-stu-id="00f10-253">Date in format: YYYY/MM/DDTHH:MM:SS (for example, 2013/06/20T10:00:00)</span></span></td><td><span data-ttu-id="00f10-254">Indication de temps des données</span><span class="sxs-lookup"><span data-stu-id="00f10-254">Time of data</span></span></td></tr><tr><td><span data-ttu-id="00f10-255">Événement</span><span class="sxs-lookup"><span data-stu-id="00f10-255">Event</span></span></td><td><span data-ttu-id="00f10-256">Non, mais s'il est indiqué, la date doit l'être également</span><span class="sxs-lookup"><span data-stu-id="00f10-256">No, if supplied then must also put date</span></span></td><td><span data-ttu-id="00f10-257">Une des manières de hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="00f10-257">One of hello following:</span></span><br><span data-ttu-id="00f10-258">• Click (clic)</span><span class="sxs-lookup"><span data-stu-id="00f10-258">• Click</span></span><br><span data-ttu-id="00f10-259">• RecommendationClick (clic de recommandation)</span><span class="sxs-lookup"><span data-stu-id="00f10-259">• RecommendationClick</span></span><br><span data-ttu-id="00f10-260">•    AddShopCart (ajout au panier)</span><span class="sxs-lookup"><span data-stu-id="00f10-260">•    AddShopCart</span></span><br><span data-ttu-id="00f10-261">• RemoveShopCart (suppression du panier)</span><span class="sxs-lookup"><span data-stu-id="00f10-261">• RemoveShopCart</span></span><br><span data-ttu-id="00f10-262">• Purchase</span><span class="sxs-lookup"><span data-stu-id="00f10-262">• Purchase</span></span></td><td></td></tr></table><br><span data-ttu-id="00f10-263">La taille de fichier maximale est de 200 Mo.</span><span class="sxs-lookup"><span data-stu-id="00f10-263">Maximum file size is 200MB.</span></span><br><br><span data-ttu-id="00f10-264">Exemple :</span><span class="sxs-lookup"><span data-stu-id="00f10-264">Example:</span></span><br><pre>149452,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>6360,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>50321,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>71285,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>224450,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>236645,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>107951,1b3d95e2-84e4-414c-bb38-be9cf461c347</pre> |

<span data-ttu-id="00f10-265">**Réponse**:</span><span class="sxs-lookup"><span data-stu-id="00f10-265">**Response**:</span></span>

<span data-ttu-id="00f10-266">Code d'état HTTP : 200</span><span class="sxs-lookup"><span data-stu-id="00f10-266">HTTP Status code: 200</span></span>

* <span data-ttu-id="00f10-267">`Feed\entry\content\properties\LineCount` : nombre de lignes acceptées.</span><span class="sxs-lookup"><span data-stu-id="00f10-267">`Feed\entry\content\properties\LineCount` - Number of lines accepted.</span></span>
* <span data-ttu-id="00f10-268">`Feed\entry\content\properties\ErrorCount`-Nombre de lignes qui n’ont pas été ajoutés en raison de l’erreur de tooan.</span><span class="sxs-lookup"><span data-stu-id="00f10-268">`Feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due tooan error.</span></span>
* <span data-ttu-id="00f10-269">`Feed\entry\content\properties\FileId` : identificateur de fichier.</span><span class="sxs-lookup"><span data-stu-id="00f10-269">`Feed\entry\content\properties\FileId` - File identifier.</span></span>

<span data-ttu-id="00f10-270">OData XML</span><span class="sxs-lookup"><span data-stu-id="00f10-270">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Add bulk usage data (usage file)</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T07:21:44Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">AddBulkUsageDataUsageFileEntity2</title>
    <updated>2014-10-05T07:21:44Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:LineCount m:type="Edm.String">33</d:LineCount>
        <d:ErrorCount m:type="Edm.String">0</d:ErrorCount>
        <d:FileId m:type="Edm.String">fead7c1c-db01-46c0-872f-65bcda36025d</d:FileId>
      </m:properties>
    </content>
      </entry>
    </feed>


#### <a name="using-data-acquisition"></a><span data-ttu-id="00f10-271">Utilisation de l'acquisition de données</span><span class="sxs-lookup"><span data-stu-id="00f10-271">Using data acquisition</span></span>
<span data-ttu-id="00f10-272">Cette section montre comment les événements de toosend dans réel heure tooAzure Machine Learning recommandations, généralement à partir de votre site Web.</span><span class="sxs-lookup"><span data-stu-id="00f10-272">This section shows how toosend events in real time tooAzure Machine Learning Recommendations, usually from your website.</span></span>

| <span data-ttu-id="00f10-273">Méthode HTTP</span><span class="sxs-lookup"><span data-stu-id="00f10-273">HTTP Method</span></span> | <span data-ttu-id="00f10-274">URI</span><span class="sxs-lookup"><span data-stu-id="00f10-274">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="00f10-275">POST</span><span class="sxs-lookup"><span data-stu-id="00f10-275">POST</span></span> |`<rootURI>/AddUsageEvent?apiVersion=%271.0%27-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="00f10-276">Nom du paramètre</span><span class="sxs-lookup"><span data-stu-id="00f10-276">Parameter Name</span></span> | <span data-ttu-id="00f10-277">Valeurs valides</span><span class="sxs-lookup"><span data-stu-id="00f10-277">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="00f10-278">apiVersion</span><span class="sxs-lookup"><span data-stu-id="00f10-278">apiVersion</span></span> |<span data-ttu-id="00f10-279">1.0</span><span class="sxs-lookup"><span data-stu-id="00f10-279">1.0</span></span> |
|  | |
| <span data-ttu-id="00f10-280">Corps de la demande</span><span class="sxs-lookup"><span data-stu-id="00f10-280">Request body</span></span> |<span data-ttu-id="00f10-281">Entrée de données d’événement pour chaque événement, vous souhaitez toosend.</span><span class="sxs-lookup"><span data-stu-id="00f10-281">Event data entry for each event you want toosend.</span></span> <span data-ttu-id="00f10-282">Vous devez envoyer pour le même ID dans le champ de SessionId hello hello hello même session utilisateur ou un navigateur.</span><span class="sxs-lookup"><span data-stu-id="00f10-282">You should send for hello same user or browser session hello same ID in hello SessionId field.</span></span> <span data-ttu-id="00f10-283">(Consultez l'exemple du corps d'événement ci-dessous.)</span><span class="sxs-lookup"><span data-stu-id="00f10-283">(See sample of event body below.)</span></span> |

* <span data-ttu-id="00f10-284">Exemple pour l'événement « Click » :</span><span class="sxs-lookup"><span data-stu-id="00f10-284">Example for event 'Click':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
        <SessionId>11112222</SessionId>
        <EventData>
        <EventData>
        <Name>Click</Name>
        <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
        </EventData>
        </Event>
* <span data-ttu-id="00f10-285">Exemple pour l'événement « RecommendationClick » :</span><span class="sxs-lookup"><span data-stu-id="00f10-285">Example for event 'RecommendationClick':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>RecommendationClick</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
          </EventData>
        </Event>
* <span data-ttu-id="00f10-286">Exemple pour l'événement « AddShopCart » :</span><span class="sxs-lookup"><span data-stu-id="00f10-286">Example for event 'AddShopCart':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>AddShopCart</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
          </EventData>
        </Event>
* <span data-ttu-id="00f10-287">Exemple pour l'événement « RemoveShopCart » :</span><span class="sxs-lookup"><span data-stu-id="00f10-287">Example for event 'RemoveShopCart':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>RemoveShopCart</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
          </EventData>
        </Event>
* <span data-ttu-id="00f10-288">Exemple pour l’événement « Purchase » :</span><span class="sxs-lookup"><span data-stu-id="00f10-288">Example for event 'Purchase':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
        <SessionId>11112222</SessionId>
        <EventData>
        <EventData>
            <Name>Purchase</Name> 
            <PurchaseItems>
            <PurchaseItems>
                <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
                <Count>3</Count>
            </PurchaseItems>
        </PurchaseItems>
        </EventData>
        </EventData>
        </Event>
* <span data-ttu-id="00f10-289">Exemple d'envoi de 2 événements « Click » et « AddShopCart » :</span><span class="sxs-lookup"><span data-stu-id="00f10-289">Example sending 2 events, 'Click' and 'AddShopCart':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>Click</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
          <ItemName>itemName</ItemName>
          <ItemDescription>item description</ItemDescription>
          <ItemCategory>category</ItemCategory>
        </EventData>
        <EventData>
          <Name>AddShopCart</Name>
          <ItemId>552A1940-21E4-4399-82BB-594B46D7ED54</ItemId>
        </EventData>
          </EventData>
        </Event>

<span data-ttu-id="00f10-290">**Réponse**: Code d'état HTTP : 200</span><span class="sxs-lookup"><span data-stu-id="00f10-290">**Response**: HTTP Status code: 200</span></span>

### <a name="build-a-recommendation-model"></a><span data-ttu-id="00f10-291">Génération d'un modèle de recommandation</span><span class="sxs-lookup"><span data-stu-id="00f10-291">Build a recommendation model</span></span>
| <span data-ttu-id="00f10-292">Méthode HTTP</span><span class="sxs-lookup"><span data-stu-id="00f10-292">HTTP Method</span></span> | <span data-ttu-id="00f10-293">URI</span><span class="sxs-lookup"><span data-stu-id="00f10-293">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="00f10-294">POST</span><span class="sxs-lookup"><span data-stu-id="00f10-294">POST</span></span> |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="00f10-295">Exemple :</span><span class="sxs-lookup"><span data-stu-id="00f10-295">Example:</span></span><br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&apiVersion=%271.0%27` |

| <span data-ttu-id="00f10-296">Nom du paramètre</span><span class="sxs-lookup"><span data-stu-id="00f10-296">Parameter Name</span></span> | <span data-ttu-id="00f10-297">Valeurs valides</span><span class="sxs-lookup"><span data-stu-id="00f10-297">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="00f10-298">modelId</span><span class="sxs-lookup"><span data-stu-id="00f10-298">modelId</span></span> |<span data-ttu-id="00f10-299">Identificateur unique du modèle hello (respecte la casse)</span><span class="sxs-lookup"><span data-stu-id="00f10-299">Unique identifier of hello model (case-sensitive)</span></span> |
| <span data-ttu-id="00f10-300">userDescription</span><span class="sxs-lookup"><span data-stu-id="00f10-300">userDescription</span></span> |<span data-ttu-id="00f10-301">Identificateur textuel du catalogue de hello.</span><span class="sxs-lookup"><span data-stu-id="00f10-301">Textual identifier of hello catalog.</span></span> <span data-ttu-id="00f10-302">Notez que si vous utilisez des espaces, vous devez plutôt l'encoder avec %20.</span><span class="sxs-lookup"><span data-stu-id="00f10-302">Note that if you use spaces you must encode it with %20 instead.</span></span> <span data-ttu-id="00f10-303">Consultez l'exemple ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="00f10-303">See example above.</span></span><br><span data-ttu-id="00f10-304">Longueur maximale : 50</span><span class="sxs-lookup"><span data-stu-id="00f10-304">Max length: 50</span></span> |
| <span data-ttu-id="00f10-305">apiVersion</span><span class="sxs-lookup"><span data-stu-id="00f10-305">apiVersion</span></span> |<span data-ttu-id="00f10-306">1.0</span><span class="sxs-lookup"><span data-stu-id="00f10-306">1.0</span></span> |
|  | |
| <span data-ttu-id="00f10-307">Corps de la requête</span><span class="sxs-lookup"><span data-stu-id="00f10-307">Request Body</span></span> |<span data-ttu-id="00f10-308">AUCUN</span><span class="sxs-lookup"><span data-stu-id="00f10-308">NONE</span></span> |

<span data-ttu-id="00f10-309">**Réponse**:</span><span class="sxs-lookup"><span data-stu-id="00f10-309">**Response**:</span></span>

<span data-ttu-id="00f10-310">Code d'état HTTP : 200</span><span class="sxs-lookup"><span data-stu-id="00f10-310">HTTP Status code: 200</span></span>

<span data-ttu-id="00f10-311">Il s'agit d'une API asynchrone.</span><span class="sxs-lookup"><span data-stu-id="00f10-311">This is an asynchronous API.</span></span> <span data-ttu-id="00f10-312">La réponse obtenue est un ID de build.</span><span class="sxs-lookup"><span data-stu-id="00f10-312">You will get a build ID as a response.</span></span> <span data-ttu-id="00f10-313">tooknow lors de la génération de hello est terminée, vous devez appeler l’API « Obtenir génère état d’un modèle » hello et localiser cette ID de build dans la réponse de hello.</span><span class="sxs-lookup"><span data-stu-id="00f10-313">tooknow when hello build has ended, you should call hello "Get Builds Status of a Model" API and locate this build ID in hello response.</span></span> <span data-ttu-id="00f10-314">Notez qu’une build peut prendre de toohours minutes selon la taille de hello de données de hello.</span><span class="sxs-lookup"><span data-stu-id="00f10-314">Note that a build can take from minutes toohours depending on hello size of hello data.</span></span>

<span data-ttu-id="00f10-315">Vous ne peut pas consommer recommandations jusqu'à ce que hello build se termine.</span><span class="sxs-lookup"><span data-stu-id="00f10-315">You cannot consume recommendations till hello build ends.</span></span>

<span data-ttu-id="00f10-316">État de build valide :</span><span class="sxs-lookup"><span data-stu-id="00f10-316">Valid build status:</span></span>

* <span data-ttu-id="00f10-317">Create : le modèle a été créé.</span><span class="sxs-lookup"><span data-stu-id="00f10-317">Create – Model was created.</span></span>
* <span data-ttu-id="00f10-318">Queued : la build de modèle a été déclenchée et mise en file d'attente.</span><span class="sxs-lookup"><span data-stu-id="00f10-318">Queued – Model build was triggered and it is queued.</span></span>
* <span data-ttu-id="00f10-319">Building : le modèle est en cours de génération.</span><span class="sxs-lookup"><span data-stu-id="00f10-319">Building – Model is being built.</span></span>
* <span data-ttu-id="00f10-320">Success : la build a été correctement exécutée.</span><span class="sxs-lookup"><span data-stu-id="00f10-320">Success – Build ended successfully.</span></span>
* <span data-ttu-id="00f10-321">Error : la build s'est terminée par un échec.</span><span class="sxs-lookup"><span data-stu-id="00f10-321">Error – Build ended with a failure.</span></span>
* <span data-ttu-id="00f10-322">Canceled : la build a été annulée.</span><span class="sxs-lookup"><span data-stu-id="00f10-322">Canceled – Build was canceled.</span></span>
* <span data-ttu-id="00f10-323">Canceling : la build est en cours d’annulation.</span><span class="sxs-lookup"><span data-stu-id="00f10-323">Canceling – Build is being canceled.</span></span>

<span data-ttu-id="00f10-324">Notez cette build hello QU'ID accessible sous hello suivant le chemin d’accès :`Feed\entry\content\properties\Id`</span><span class="sxs-lookup"><span data-stu-id="00f10-324">Note that hello build ID can be found under hello following path: `Feed\entry\content\properties\Id`</span></span>

<span data-ttu-id="00f10-325">OData XML</span><span class="sxs-lookup"><span data-stu-id="00f10-325">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Build a Model with RequestBody</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T08:56:34Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">BuildAModelEntity2</title>
    <updated>2014-10-05T08:56:34Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">1000272</d:Id>
        <d:UserName m:type="Edm.String"></d:UserName>
        <d:ModelId m:type="Edm.String">9559872f-7a53-4076-a3c7-19d9385c1265</d:ModelId>
        <d:ModelName m:type="Edm.String">docTest</d:ModelName>
        <d:Type m:type="Edm.String">Recommendation</d:Type>
        <d:CreationTime m:type="Edm.String">2014-10-05T08:56:31.893</d:CreationTime>
        <d:Progress_BuildId m:type="Edm.String">1000272</d:Progress_BuildId>
        <d:Progress_ModelId m:type="Edm.String">9559872f-7a53-4076-a3c7-19d9385c1265</d:Progress_ModelId>
        <d:Progress_UserName m:type="Edm.String">5-4058-ab36-1fe254f05102@dm.com</d:Progress_UserName>
        <d:Progress_IsExecutionStarted m:type="Edm.String">false</d:Progress_IsExecutionStarted>
        <d:Progress_IsExecutionEnded m:type="Edm.String">false</d:Progress_IsExecutionEnded>
        <d:Progress_Percent m:type="Edm.String">0</d:Progress_Percent>
        <d:Progress_StartTime m:type="Edm.String">0001-01-01T00:00:00</d:Progress_StartTime>
        <d:Progress_EndTime m:type="Edm.String">0001-01-01T00:00:00</d:Progress_EndTime>
        <d:Progress_UpdateDateUTC m:type="Edm.String"></d:Progress_UpdateDateUTC>
        <d:Status m:type="Edm.String">Queued</d:Status>
        <d:Key1 m:type="Edm.String">UseFeaturesInModel</d:Key1>
        <d:Value1 m:type="Edm.String">False</d:Value1>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="get-build-status-of-a-model"></a><span data-ttu-id="00f10-326">Obtention de l’état de build d’un modèle</span><span class="sxs-lookup"><span data-stu-id="00f10-326">Get build status of a model</span></span>
| <span data-ttu-id="00f10-327">Méthode HTTP</span><span class="sxs-lookup"><span data-stu-id="00f10-327">HTTP Method</span></span> | <span data-ttu-id="00f10-328">URI</span><span class="sxs-lookup"><span data-stu-id="00f10-328">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="00f10-329">GET</span><span class="sxs-lookup"><span data-stu-id="00f10-329">GET</span></span> |`<rootURI>/GetModelBuildsStatus?modelId=%27<modelId>%27&onlyLastBuild=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="00f10-330">Exemple :</span><span class="sxs-lookup"><span data-stu-id="00f10-330">Example:</span></span><br>`<rootURI>/GetModelBuildsStatus?modelId=%279559872f-7a53-4076-a3c7-19d9385c1265%27&onlyLastBuild=true&apiVersion=%271.0%27` |

| <span data-ttu-id="00f10-331">Nom du paramètre</span><span class="sxs-lookup"><span data-stu-id="00f10-331">Parameter Name</span></span> | <span data-ttu-id="00f10-332">Valeurs valides</span><span class="sxs-lookup"><span data-stu-id="00f10-332">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="00f10-333">modelId</span><span class="sxs-lookup"><span data-stu-id="00f10-333">modelId</span></span> |<span data-ttu-id="00f10-334">Identificateur unique du modèle hello (respecte la casse)</span><span class="sxs-lookup"><span data-stu-id="00f10-334">Unique identifier of hello model  (case-sensitive)</span></span> |
| <span data-ttu-id="00f10-335">onlyLastBuild</span><span class="sxs-lookup"><span data-stu-id="00f10-335">onlyLastBuild</span></span> |<span data-ttu-id="00f10-336">Indique si tooreturn tous hello générer l’historique du modèle de hello ou état hello seule de la build la plus récente hello.</span><span class="sxs-lookup"><span data-stu-id="00f10-336">Indicates whether tooreturn all hello build history of hello model or only hello status of hello most recent build.</span></span> |
| <span data-ttu-id="00f10-337">apiVersion</span><span class="sxs-lookup"><span data-stu-id="00f10-337">apiVersion</span></span> |<span data-ttu-id="00f10-338">1.0</span><span class="sxs-lookup"><span data-stu-id="00f10-338">1.0</span></span> |

<span data-ttu-id="00f10-339">**Réponse**:</span><span class="sxs-lookup"><span data-stu-id="00f10-339">**Response**:</span></span>

<span data-ttu-id="00f10-340">Code d'état HTTP : 200</span><span class="sxs-lookup"><span data-stu-id="00f10-340">HTTP Status code: 200</span></span>

<span data-ttu-id="00f10-341">réponse de Hello inclut une entrée par une build.</span><span class="sxs-lookup"><span data-stu-id="00f10-341">hello response includes one entry per build.</span></span> <span data-ttu-id="00f10-342">Chaque entrée a hello données suivantes :</span><span class="sxs-lookup"><span data-stu-id="00f10-342">Each entry has hello following data:</span></span>

* <span data-ttu-id="00f10-343">`feed/entry/content/properties/UserName`– Nom de l’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="00f10-343">`feed/entry/content/properties/UserName` – Name of hello user.</span></span>
* <span data-ttu-id="00f10-344">`feed/entry/content/properties/ModelName`– Nom du modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="00f10-344">`feed/entry/content/properties/ModelName` – Name of hello model.</span></span>
* <span data-ttu-id="00f10-345">`feed/entry/content/properties/ModelId` : identificateur unique du modèle.</span><span class="sxs-lookup"><span data-stu-id="00f10-345">`feed/entry/content/properties/ModelId` – Model unique identifier.</span></span>
* <span data-ttu-id="00f10-346">`feed/entry/content/properties/IsDeployed`: Indique si le déploiement (aussi appelé sous-type de hello build</span><span class="sxs-lookup"><span data-stu-id="00f10-346">`feed/entry/content/properties/IsDeployed` – Whether hello build is deployed (a.k.a.</span></span> <span data-ttu-id="00f10-347">(c’est-à-dire active).</span><span class="sxs-lookup"><span data-stu-id="00f10-347">active build).</span></span>
* <span data-ttu-id="00f10-348">`feed/entry/content/properties/BuildId` : identificateur unique de la build.</span><span class="sxs-lookup"><span data-stu-id="00f10-348">`feed/entry/content/properties/BuildId` – Build unique identifier.</span></span>
* <span data-ttu-id="00f10-349">`feed/entry/content/properties/BuildType`-Type de build de hello.</span><span class="sxs-lookup"><span data-stu-id="00f10-349">`feed/entry/content/properties/BuildType` - Type of hello build.</span></span>
* <span data-ttu-id="00f10-350">`feed/entry/content/properties/Status` : état de la build.</span><span class="sxs-lookup"><span data-stu-id="00f10-350">`feed/entry/content/properties/Status` – Build status.</span></span> <span data-ttu-id="00f10-351">Peut être une des manières suivantes les hello : erreur, construction, en file d’attente, l’annulation, annulé, réussite</span><span class="sxs-lookup"><span data-stu-id="00f10-351">Can be one of hello following: Error, Building, Queued, Canceling, Canceled, Success</span></span>
* <span data-ttu-id="00f10-352">`feed/entry/content/properties/StatusMessage`– Message d’état détaillée (s’applique uniquement les États toospecific).</span><span class="sxs-lookup"><span data-stu-id="00f10-352">`feed/entry/content/properties/StatusMessage` – Detailed status message (applies only toospecific states).</span></span>
* <span data-ttu-id="00f10-353">`feed/entry/content/properties/Progress` : progression de l'exécution de la build (%).</span><span class="sxs-lookup"><span data-stu-id="00f10-353">`feed/entry/content/properties/Progress` – Build progress (%).</span></span>
* <span data-ttu-id="00f10-354">`feed/entry/content/properties/StartTime` : heure de début de l'exécution de la build.</span><span class="sxs-lookup"><span data-stu-id="00f10-354">`feed/entry/content/properties/StartTime` – Build start time.</span></span>
* <span data-ttu-id="00f10-355">`feed/entry/content/properties/EndTime` : heure de fin de l'exécution de la build.</span><span class="sxs-lookup"><span data-stu-id="00f10-355">`feed/entry/content/properties/EndTime` – Build end time.</span></span>
* <span data-ttu-id="00f10-356">`feed/entry/content/properties/ExecutionTime` : durée de la build.</span><span class="sxs-lookup"><span data-stu-id="00f10-356">`feed/entry/content/properties/ExecutionTime` – Build duration.</span></span>
* <span data-ttu-id="00f10-357">`feed/entry/content/properties/ProgressStep`– Plus d’informations sur la phase actuelle hello figurant dans une build en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="00f10-357">`feed/entry/content/properties/ProgressStep` – Details about hello current stage that a build in progress is in.</span></span>

<span data-ttu-id="00f10-358">État de build valide :</span><span class="sxs-lookup"><span data-stu-id="00f10-358">Valid build status:</span></span>

* <span data-ttu-id="00f10-359">Created : l’entrée de demande de build a été créée.</span><span class="sxs-lookup"><span data-stu-id="00f10-359">Created – Build request entry was created.</span></span>
* <span data-ttu-id="00f10-360">Queued : la demande de build a été déclenchée et mise en attente.</span><span class="sxs-lookup"><span data-stu-id="00f10-360">Queued – Build request was triggered and it is queued.</span></span>
* <span data-ttu-id="00f10-361">Building : la build est en cours.</span><span class="sxs-lookup"><span data-stu-id="00f10-361">Building – Build is in process.</span></span>
* <span data-ttu-id="00f10-362">Success : la build a été correctement exécutée.</span><span class="sxs-lookup"><span data-stu-id="00f10-362">Success – Build ended successfully.</span></span>
* <span data-ttu-id="00f10-363">Error : la build s'est terminée par un échec.</span><span class="sxs-lookup"><span data-stu-id="00f10-363">Error – Build ended with a failure.</span></span>
* <span data-ttu-id="00f10-364">Canceled : la build a été annulée.</span><span class="sxs-lookup"><span data-stu-id="00f10-364">Canceled – Build was canceled.</span></span>
* <span data-ttu-id="00f10-365">Canceling : la build est en cours d’annulation.</span><span class="sxs-lookup"><span data-stu-id="00f10-365">Canceling – Build is being canceled.</span></span>

<span data-ttu-id="00f10-366">Valeurs valides pour le type de build :</span><span class="sxs-lookup"><span data-stu-id="00f10-366">Valid values for build type:</span></span>

* <span data-ttu-id="00f10-367">Rank - Build de classement.</span><span class="sxs-lookup"><span data-stu-id="00f10-367">Rank - Rank build.</span></span> <span data-ttu-id="00f10-368">(De rang détails de la build, veuillez consulter le document « Documentation Machine Learning recommandation API » de toohello).</span><span class="sxs-lookup"><span data-stu-id="00f10-368">(For rank build details, please refer toohello "Machine Learning Recommendation API documentation" document.)</span></span>
* <span data-ttu-id="00f10-369">Recommendation - Build de recommandation.</span><span class="sxs-lookup"><span data-stu-id="00f10-369">Recommendation - Recommendation build.</span></span>
* <span data-ttu-id="00f10-370">Fbt - Build fréquemment achetés ensemble.</span><span class="sxs-lookup"><span data-stu-id="00f10-370">Fbt - Frequently bought together build.</span></span>

<span data-ttu-id="00f10-371">OData XML</span><span class="sxs-lookup"><span data-stu-id="00f10-371">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get builds status of a model</subtitle>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-05T17:51:10Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'" />
    <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetBuildsStatusEntity</title>
    <updated>2014-11-05T17:51:10Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:UserName m:type="Edm.String">b-434e-b2c9-84935664ff20@dm.com</d:UserName>
        <d:ModelName m:type="Edm.String">ModelName</d:ModelName>
        <d:ModelId m:type="Edm.String">1d20c34f-dca1-4eac-8e5d-f299e4e4ad66</d:ModelId>
        <d:IsDeployed m:type="Edm.String">true</d:IsDeployed>
        <d:BuildId m:type="Edm.String">1000272</d:BuildId>
        <d:BuildType m:type="Edm.String">Recommendation</d:BuildType>
        <d:Status m:type="Edm.String">Success</d:Status>
        <d:StatusMessage m:type="Edm.String"></d:StatusMessage>
        <d:Progress m:type="Edm.String">0</d:Progress>
        <d:StartTime m:type="Edm.String">2014-11-02T13:43:51</d:StartTime>
        <d:EndTime m:type="Edm.String">2014-11-02T13:45:10</d:EndTime>
        <d:ExecutionTime m:type="Edm.String">00:01:19</d:ExecutionTime>
        <d:IsExecutionStarted m:type="Edm.String">false</d:IsExecutionStarted>
        <d:ProgressStep m:type="Edm.String"></d:ProgressStep>
      </m:properties>
     </content>
    </entry>
    </feed>


### <a name="get-recommendations"></a><span data-ttu-id="00f10-372">Obtention de recommandations</span><span class="sxs-lookup"><span data-stu-id="00f10-372">Get recommendations</span></span>
| <span data-ttu-id="00f10-373">Méthode HTTP</span><span class="sxs-lookup"><span data-stu-id="00f10-373">HTTP Method</span></span> | <span data-ttu-id="00f10-374">URI</span><span class="sxs-lookup"><span data-stu-id="00f10-374">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="00f10-375">GET</span><span class="sxs-lookup"><span data-stu-id="00f10-375">GET</span></span> |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="00f10-376">Exemple :</span><span class="sxs-lookup"><span data-stu-id="00f10-376">Example:</span></span><br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="00f10-377">Nom du paramètre</span><span class="sxs-lookup"><span data-stu-id="00f10-377">Parameter Name</span></span> | <span data-ttu-id="00f10-378">Valeurs valides</span><span class="sxs-lookup"><span data-stu-id="00f10-378">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="00f10-379">modelId</span><span class="sxs-lookup"><span data-stu-id="00f10-379">modelId</span></span> |<span data-ttu-id="00f10-380">Identificateur unique du modèle hello (respecte la casse)</span><span class="sxs-lookup"><span data-stu-id="00f10-380">Unique identifier of hello model (case-sensitive)</span></span> |
| <span data-ttu-id="00f10-381">itemIds</span><span class="sxs-lookup"><span data-stu-id="00f10-381">itemIds</span></span> |<span data-ttu-id="00f10-382">Liste de séparées par des virgules des toorecommend d’éléments hello pour.</span><span class="sxs-lookup"><span data-stu-id="00f10-382">Comma-separated list of hello items toorecommend for.</span></span><br><span data-ttu-id="00f10-383">Longueur maximale : 1024</span><span class="sxs-lookup"><span data-stu-id="00f10-383">Max length: 1024</span></span> |
| <span data-ttu-id="00f10-384">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="00f10-384">numberOfResults</span></span> |<span data-ttu-id="00f10-385">Nombre de résultats requis</span><span class="sxs-lookup"><span data-stu-id="00f10-385">Number of required results</span></span> |
| <span data-ttu-id="00f10-386">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="00f10-386">includeMetatadata</span></span> |<span data-ttu-id="00f10-387">Utilisation ultérieure, toujours false</span><span class="sxs-lookup"><span data-stu-id="00f10-387">Future use, always false</span></span> |
| <span data-ttu-id="00f10-388">apiVersion</span><span class="sxs-lookup"><span data-stu-id="00f10-388">apiVersion</span></span> |<span data-ttu-id="00f10-389">1.0</span><span class="sxs-lookup"><span data-stu-id="00f10-389">1.0</span></span> |

<span data-ttu-id="00f10-390">**Réponse :**</span><span class="sxs-lookup"><span data-stu-id="00f10-390">**Response:**</span></span>

<span data-ttu-id="00f10-391">Code d'état HTTP : 200</span><span class="sxs-lookup"><span data-stu-id="00f10-391">HTTP Status code: 200</span></span>

<span data-ttu-id="00f10-392">réponse de Hello comporte une entrée par élément recommandé.</span><span class="sxs-lookup"><span data-stu-id="00f10-392">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="00f10-393">Chaque entrée a hello données suivantes :</span><span class="sxs-lookup"><span data-stu-id="00f10-393">Each entry has hello following data:</span></span>

* <span data-ttu-id="00f10-394">`Feed\entry\content\properties\Id` : ID d’élément recommandé</span><span class="sxs-lookup"><span data-stu-id="00f10-394">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="00f10-395">`Feed\entry\content\properties\Name`-Nom de l’élément de hello.</span><span class="sxs-lookup"><span data-stu-id="00f10-395">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="00f10-396">`Feed\entry\content\properties\Rating`-Évaluation de recommandation de hello ; nombre élevé signifie toute confiance.</span><span class="sxs-lookup"><span data-stu-id="00f10-396">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="00f10-397">`Feed\entry\content\properties\Reasoning` : raisonnement de la recommandation (par exemple, pour expliquer les recommandations).</span><span class="sxs-lookup"><span data-stu-id="00f10-397">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (for example, recommendation explanations).</span></span>

<span data-ttu-id="00f10-398">OData XML</span><span class="sxs-lookup"><span data-stu-id="00f10-398">OData XML</span></span>

<span data-ttu-id="00f10-399">Hello exemple de réponse ci-dessous comprend 10 éléments recommandés :</span><span class="sxs-lookup"><span data-stu-id="00f10-399">hello example response below includes 10 recommended items:</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get Recommendation</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T12:28:48Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">159</d:Id>
        <d:Name m:type="Edm.String">159</d:Name>
        <d:Rating m:type="Edm.Double">0.543343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '159'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">52</d:Id>
        <d:Name m:type="Edm.String">52</d:Name>
        <d:Rating m:type="Edm.Double">0.539588900748721</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '52'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">35</d:Id>
        <d:Name m:type="Edm.String">35</d:Name>
        <d:Rating m:type="Edm.Double">0.53842946443853</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '35'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">124</d:Id>
        <d:Name m:type="Edm.String">124</d:Name>
        <d:Rating m:type="Edm.Double">0.536712832792886</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '124'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">120</d:Id>
        <d:Name m:type="Edm.String">120</d:Name>
        <d:Rating m:type="Edm.Double">0.533673023762878</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '120'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">96</d:Id>
        <d:Name m:type="Edm.String">96</d:Name>
        <d:Rating m:type="Edm.Double">0.532544826370521</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '96'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">69</d:Id>
        <d:Name m:type="Edm.String">69</d:Name>
        <d:Rating m:type="Edm.Double">0.531678607847759</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '69'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">172</d:Id>
        <d:Name m:type="Edm.String">172</d:Name>
        <d:Rating m:type="Edm.Double">0.530957821375951</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '172'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">155</d:Id>
        <d:Name m:type="Edm.String">155</d:Name>
        <d:Rating m:type="Edm.Double">0.529093541481333</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '155'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">32</d:Id>
        <d:Name m:type="Edm.String">32</d:Name>
        <d:Rating m:type="Edm.Double">0.528917978168322</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '32'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="update-model"></a><span data-ttu-id="00f10-400">Mise à jour du modèle</span><span class="sxs-lookup"><span data-stu-id="00f10-400">Update model</span></span>
<span data-ttu-id="00f10-401">Vous pouvez mettre à jour la description du modèle hello ou hello ID de génération active.</span><span class="sxs-lookup"><span data-stu-id="00f10-401">You can update hello model description or hello active build ID.</span></span>
<span data-ttu-id="00f10-402">*Identifiant de build active* : pour chaque modèle, chaque build possède un identifiant de build.</span><span class="sxs-lookup"><span data-stu-id="00f10-402">*Active build ID* - Every build for every model has a build ID.</span></span> <span data-ttu-id="00f10-403">ID de build active Hello est hello première génération réussie de chaque nouveau modèle.</span><span class="sxs-lookup"><span data-stu-id="00f10-403">hello active build ID is hello first successful build of every new model.</span></span> <span data-ttu-id="00f10-404">Une fois que vous avez un ID de build active et vous faire d’autres builds pour hello même modèle, vous devez tooexplicitly définir comme hello par défaut ID de build si vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="00f10-404">Once you have an active build ID and you do additional builds for hello same model, you need tooexplicitly set it as hello default build ID if you want to.</span></span> <span data-ttu-id="00f10-405">Lorsque vous consommez des recommandations, si vous ne spécifiez pas d’ID de build hello toouse, un est utilisé automatiquement de la valeur par défaut hello souhaitées.</span><span class="sxs-lookup"><span data-stu-id="00f10-405">When you consume recommendations, if you do not specify hello build ID that you want toouse, hello default one will be used automatically.</span></span>

<span data-ttu-id="00f10-406">Ce mécanisme vous permet de - une fois que vous disposez d’un modèle de recommandation en production - toobuild de nouveaux modèles et les testez avant de les promouvoir tooproduction.</span><span class="sxs-lookup"><span data-stu-id="00f10-406">This mechanism enables you - once you have a recommendation model in production - toobuild new models and test them before you promote them tooproduction.</span></span>

| <span data-ttu-id="00f10-407">Méthode HTTP</span><span class="sxs-lookup"><span data-stu-id="00f10-407">HTTP Method</span></span> | <span data-ttu-id="00f10-408">URI</span><span class="sxs-lookup"><span data-stu-id="00f10-408">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="00f10-409">PUT</span><span class="sxs-lookup"><span data-stu-id="00f10-409">PUT</span></span> |`<rootURI>/UpdateModel?id=%27<modelId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="00f10-410">Exemple :</span><span class="sxs-lookup"><span data-stu-id="00f10-410">Example:</span></span><br>`<rootURI>/UpdateModel?id=%279559872f-7a53-4076-a3c7-19d9385c1265%27&apiVersion=%271.0%27` |

| <span data-ttu-id="00f10-411">Nom du paramètre</span><span class="sxs-lookup"><span data-stu-id="00f10-411">Parameter Name</span></span> | <span data-ttu-id="00f10-412">Valeurs valides</span><span class="sxs-lookup"><span data-stu-id="00f10-412">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="00f10-413">id</span><span class="sxs-lookup"><span data-stu-id="00f10-413">id</span></span> |<span data-ttu-id="00f10-414">Identificateur unique du modèle hello (respecte la casse)</span><span class="sxs-lookup"><span data-stu-id="00f10-414">Unique identifier of hello model (case-sensitive)</span></span> |
| <span data-ttu-id="00f10-415">apiVersion</span><span class="sxs-lookup"><span data-stu-id="00f10-415">apiVersion</span></span> |<span data-ttu-id="00f10-416">1.0</span><span class="sxs-lookup"><span data-stu-id="00f10-416">1.0</span></span> |
|  | |
| <span data-ttu-id="00f10-417">Corps de la requête</span><span class="sxs-lookup"><span data-stu-id="00f10-417">Request Body</span></span> |`<ModelUpdateParams xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">`<br>`   <Description>New Description</Description>`<br>`          <ActiveBuildId>-1</ActiveBuildId>`<br>`</ModelUpdateParams>`<br><br><span data-ttu-id="00f10-418">Notez que la Description des balises XML de hello et ActiveBuildId sont facultatifs.</span><span class="sxs-lookup"><span data-stu-id="00f10-418">Note that hello XML tags Description and ActiveBuildId are optional.</span></span> <span data-ttu-id="00f10-419">Si vous ne souhaitez pas tooset Description ou ActiveBuildId, supprimez la balise dans son ensemble hello.</span><span class="sxs-lookup"><span data-stu-id="00f10-419">If you do not want tooset Description or ActiveBuildId, remove hello entire tag.</span></span> |

<span data-ttu-id="00f10-420">**Réponse**:</span><span class="sxs-lookup"><span data-stu-id="00f10-420">**Response**:</span></span>

<span data-ttu-id="00f10-421">Code d'état HTTP : 200</span><span class="sxs-lookup"><span data-stu-id="00f10-421">HTTP Status code: 200</span></span>

<span data-ttu-id="00f10-422">OData XML</span><span class="sxs-lookup"><span data-stu-id="00f10-422">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Update an Existing Model</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel?id='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T10:27:17Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel?id='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;apiVersion='1.0'" />
    </feed>

## <a name="legal"></a><span data-ttu-id="00f10-423">Informations juridiques</span><span class="sxs-lookup"><span data-stu-id="00f10-423">Legal</span></span>
<span data-ttu-id="00f10-424">Ce document est fourni « en l'état ».</span><span class="sxs-lookup"><span data-stu-id="00f10-424">This document is provided "as-is".</span></span> <span data-ttu-id="00f10-425">Les informations et les points de vue exprimés dans ce document, y compris les URL et autres références à des sites web, peuvent être modifiés sans préavis.</span><span class="sxs-lookup"><span data-stu-id="00f10-425">Information and views expressed in this document, including URL and other Internet website references, may change without notice.</span></span> <span data-ttu-id="00f10-426">Certains exemples sont fournis à titre indicatif uniquement et sont fictifs.</span><span class="sxs-lookup"><span data-stu-id="00f10-426">Some examples depicted herein are provided for illustration only and are fictitious.</span></span> <span data-ttu-id="00f10-427">Toute association ou lien est purement involontaire ou fortuit.</span><span class="sxs-lookup"><span data-stu-id="00f10-427">No real association or connection is intended or should be inferred.</span></span> <span data-ttu-id="00f10-428">Ce document ne fournit pas vous concède tooany de propriété intellectuelle de tout produit Microsoft.</span><span class="sxs-lookup"><span data-stu-id="00f10-428">This document does not provide you with any legal rights tooany intellectual property in any Microsoft product.</span></span> <span data-ttu-id="00f10-429">Vous pouvez copier et utiliser ce document pour un usage interne, à titre de référence.</span><span class="sxs-lookup"><span data-stu-id="00f10-429">You may copy and use this document for your internal, reference purposes.</span></span> <span data-ttu-id="00f10-430">© 2014 Microsoft.</span><span class="sxs-lookup"><span data-stu-id="00f10-430">© 2014 Microsoft.</span></span> <span data-ttu-id="00f10-431">Tous droits réservés.</span><span class="sxs-lookup"><span data-stu-id="00f10-431">All rights reserved.</span></span> 

