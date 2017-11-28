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
redirect_document_id: TRUE
ms.openlocfilehash: 0a9d0b6aa1ef734a857ecc16777ba6250909b38d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="quick-start-guide-for-the-machine-learning-recommendations-api-version-1"></a><span data-ttu-id="1718b-104">Guide de démarrage rapide pour l’API Machine Learning Recommendations (version 1)</span><span class="sxs-lookup"><span data-stu-id="1718b-104">Quick start guide for the Machine Learning Recommendations API (version 1)</span></span>

> [!NOTE]
> <span data-ttu-id="1718b-105">Vous devez commencer à utiliser le [Service cognitif de l’API Recommandations](https://www.microsoft.com/cognitive-services/recommendations-api) au lieu de cette version.</span><span class="sxs-lookup"><span data-stu-id="1718b-105">You should start using the [Recommendations API Cognitive Service](https://www.microsoft.com/cognitive-services/recommendations-api) instead of this version.</span></span> <span data-ttu-id="1718b-106">Le Service cognitif de l’API Recommandations remplacera ce service et toutes les nouvelles fonctionnalités y seront développées.</span><span class="sxs-lookup"><span data-stu-id="1718b-106">The Recommendations Cognitive Service will be replacing this service, and all the new features will be developed there.</span></span> <span data-ttu-id="1718b-107">Il propose de nouvelles fonctionnalités telles que la prise en charge du traitement par lot, un meilleur Explorateur d’API, une surface d’API plus propre, une expérience d’inscription/de facturation plus cohérente, etc.</span><span class="sxs-lookup"><span data-stu-id="1718b-107">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span></span>
>
> <span data-ttu-id="1718b-108">En savoir plus sur la [migration vers le nouveau Service cognitif](http://aka.ms/recomigrate)</span><span class="sxs-lookup"><span data-stu-id="1718b-108">Learn more about [Migrating to the new Cognitive Service](http://aka.ms/recomigrate).</span></span>
> 
> 

<span data-ttu-id="1718b-109">Ce document décrit comment intégrer votre service ou application pour utiliser Microsoft Azure Machine Learning Recommendations.</span><span class="sxs-lookup"><span data-stu-id="1718b-109">This document describes how to onboard your service or application to use Microsoft Azure Machine Learning Recommendations.</span></span> <span data-ttu-id="1718b-110">Vous trouverez plus d’informations sur l’API Recommendations dans la [galerie Cortana Intelligence](https://gallery.cortanaintelligence.com/MachineLearningAPIs/Recommendations-2).</span><span class="sxs-lookup"><span data-stu-id="1718b-110">You can find more details on the Recommendations API in the [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/MachineLearningAPIs/Recommendations-2).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="general-overview"></a><span data-ttu-id="1718b-111">Présentation générale</span><span class="sxs-lookup"><span data-stu-id="1718b-111">General overview</span></span>
<span data-ttu-id="1718b-112">Pour utiliser Azure Machine Learning Recommendations, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="1718b-112">To use Azure Machine Learning Recommendations, you need to take the following steps:</span></span>

* <span data-ttu-id="1718b-113">Créez un modèle : le modèle est le conteneur de vos données d’utilisation, des données de catalogue et du modèle de recommandation.</span><span class="sxs-lookup"><span data-stu-id="1718b-113">Create a model - A model is a container of your usage data, catalog data, and the recommendation model.</span></span>
* <span data-ttu-id="1718b-114">Importer les données du catalogue : un catalogue contient des informations de métadonnées sur les éléments.</span><span class="sxs-lookup"><span data-stu-id="1718b-114">Import catalog data - A catalog contains metadata information on the items.</span></span> 
* <span data-ttu-id="1718b-115">Importez des données d’utilisation : les données d’utilisation peuvent être téléchargées de l’une des deux (ou des deux) manières suivantes :</span><span class="sxs-lookup"><span data-stu-id="1718b-115">Import usage data - Usage data can be uploaded in one of two ways (or both):</span></span>
  * <span data-ttu-id="1718b-116">En téléchargeant un fichier qui contient les données d'utilisation.</span><span class="sxs-lookup"><span data-stu-id="1718b-116">By uploading a file that contains the usage data.</span></span>
  * <span data-ttu-id="1718b-117">En envoyant des événements d’acquisition de données.</span><span class="sxs-lookup"><span data-stu-id="1718b-117">By sending data acquisition events.</span></span>
    <span data-ttu-id="1718b-118">Généralement, vous téléchargez un fichier d’utilisation pour pouvoir créer un modèle de recommandation initial (démarrage) et l’utiliser jusqu’à ce que le système rassemble suffisamment de données en utilisant le format d’acquisition de données.</span><span class="sxs-lookup"><span data-stu-id="1718b-118">Usually you upload a usage file in order to be able to create an initial recommendation model (bootstrap) and use it until the system gathers enough data by using the data acquisition format.</span></span>
* <span data-ttu-id="1718b-119">Générez un modèle de recommandation : il s’agit d’une opération asynchrone dans laquelle le système de recommandation prend toutes les données d’utilisation et crée un modèle de recommandation.</span><span class="sxs-lookup"><span data-stu-id="1718b-119">Build a recommendation model - This is an asynchronous operation in which the recommendation system takes all the usage data and creates a recommendation model.</span></span> <span data-ttu-id="1718b-120">Cette opération peut prendre plusieurs minutes, voire plusieurs heures, selon la taille des données et les paramètres de configuration de génération.</span><span class="sxs-lookup"><span data-stu-id="1718b-120">This operation can take several minutes or several hours depending on the size of the data and the build configuration parameters.</span></span> <span data-ttu-id="1718b-121">Lors du déclenchement de la build, vous obtenez un ID de build.</span><span class="sxs-lookup"><span data-stu-id="1718b-121">When triggering the build, you will get a build ID.</span></span> <span data-ttu-id="1718b-122">Utilisez-le pour vérifier à quel moment s’est terminé le processus de génération et ce, avant de commencer à utiliser les recommandations.</span><span class="sxs-lookup"><span data-stu-id="1718b-122">Use it to check when the build process has ended before starting to consume recommendations.</span></span>
* <span data-ttu-id="1718b-123">Utilisez les recommandations : obtenez des recommandations pour un élément spécifique ou pour une liste d’éléments.</span><span class="sxs-lookup"><span data-stu-id="1718b-123">Consume recommendations - Get recommendations for a specific item or list of items.</span></span>

<span data-ttu-id="1718b-124">Toutes les étapes ci-dessus sont effectuées via l’API Azure Machine Learning Recommendations.</span><span class="sxs-lookup"><span data-stu-id="1718b-124">All the steps above are done through the Azure Machine Learning Recommendations API.</span></span>  <span data-ttu-id="1718b-125">Vous pouvez télécharger un exemple d'application qui implémente chacune de ces étapes également à partir de la [galerie.](http://1drv.ms/1xeO2F3)</span><span class="sxs-lookup"><span data-stu-id="1718b-125">You can download a sample application that implements each of these steps from the [gallery as well.](http://1drv.ms/1xeO2F3)</span></span>

## <a name="limitations"></a><span data-ttu-id="1718b-126">Limitations</span><span class="sxs-lookup"><span data-stu-id="1718b-126">Limitations</span></span>
* <span data-ttu-id="1718b-127">Le nombre maximal de modèles par abonnement est de 10.</span><span class="sxs-lookup"><span data-stu-id="1718b-127">The maximum number of models per subscription is 10.</span></span>
* <span data-ttu-id="1718b-128">Le nombre maximal d'éléments pouvant être contenus dans un catalogue est de 100 000.</span><span class="sxs-lookup"><span data-stu-id="1718b-128">The maximum number of items that a catalog can hold is 100,000.</span></span>
* <span data-ttu-id="1718b-129">La quantité maximale de points d'utilisation conservée est d'environ 5 000 000.</span><span class="sxs-lookup"><span data-stu-id="1718b-129">The maximum number of usage points that are kept is ~5,000,000.</span></span> <span data-ttu-id="1718b-130">Le plus ancien est supprimé quand des nouveaux sont téléchargés ou signalés.</span><span class="sxs-lookup"><span data-stu-id="1718b-130">The oldest will be deleted if new ones will be uploaded or reported.</span></span>
* <span data-ttu-id="1718b-131">La taille maximale des données pouvant être envoyées dans POST (par exemple, importation des données de catalogue ou des données d’utilisation) est de 200 Mo.</span><span class="sxs-lookup"><span data-stu-id="1718b-131">The maximum size of data that can be sent in POST (for example, import catalog data, import usage data) is 200MB.</span></span>
* <span data-ttu-id="1718b-132">Le nombre de transactions par seconde pour une build de modèle de recommandation inactive est d'environ 2 TPS.</span><span class="sxs-lookup"><span data-stu-id="1718b-132">The number of transactions per second for a recommendation model build that is not active is ~2TPS.</span></span> <span data-ttu-id="1718b-133">Une build de modèle de recommandation active peut prendre en charge jusqu'à 20 TPS.</span><span class="sxs-lookup"><span data-stu-id="1718b-133">A recommendation model build that is active can hold up to 20TPS.</span></span>

## <a name="integration"></a><span data-ttu-id="1718b-134">Intégration</span><span class="sxs-lookup"><span data-stu-id="1718b-134">Integration</span></span>
### <a name="authentication"></a><span data-ttu-id="1718b-135">Authentification</span><span class="sxs-lookup"><span data-stu-id="1718b-135">Authentication</span></span>
<span data-ttu-id="1718b-136">Microsoft Azure Marketplace prend en charge les méthodes d’authentification de base ou OAuth.</span><span class="sxs-lookup"><span data-stu-id="1718b-136">Microsoft Azure Marketplace supports either the Basic or OAuth authentication method.</span></span> <span data-ttu-id="1718b-137">Vous pouvez facilement trouver les clés de compte en accédant aux clés sur le Marketplace sous [vos paramètres de compte](https://datamarket.azure.com/account/keys).</span><span class="sxs-lookup"><span data-stu-id="1718b-137">You can easily find the account keys by navigating to the keys in the marketplace under [your account settings](https://datamarket.azure.com/account/keys).</span></span> 

#### <a name="basic-authentication"></a><span data-ttu-id="1718b-138">Authentification de base</span><span class="sxs-lookup"><span data-stu-id="1718b-138">Basic Authentication</span></span>
<span data-ttu-id="1718b-139">Ajoutez l’en-tête d’autorisation :</span><span class="sxs-lookup"><span data-stu-id="1718b-139">Add the Authorization header:</span></span>

    Authorization: Basic <creds>

    Where <creds> = ConvertToBase64("AccountKey:" + yourAccountKey);  

<span data-ttu-id="1718b-140">Convertir en Base64 (C#)</span><span class="sxs-lookup"><span data-stu-id="1718b-140">Convert to Base64 (C#)</span></span>

    var bytes = Encoding.UTF8.GetBytes("AccountKey:" + yourAccountKey);
    var creds = Convert.ToBase64String(bytes);

<span data-ttu-id="1718b-141">Convertir en Base64 (JavaScript)</span><span class="sxs-lookup"><span data-stu-id="1718b-141">Convert to Base64 (JavaScript)</span></span>

    var creds = window.btoa("AccountKey" + ":" + yourAccountKey);




### <a name="service-uri"></a><span data-ttu-id="1718b-142">URI de service</span><span class="sxs-lookup"><span data-stu-id="1718b-142">Service URI</span></span>
<span data-ttu-id="1718b-143">Les URI racines de service des API Azure Machine Learning Recommendations se trouvent [ici](https://api.datamarket.azure.com/amla/recommendations/v2/)</span><span class="sxs-lookup"><span data-stu-id="1718b-143">The service root URI for the Azure Machine Learning Recommendations APIs is [here.](https://api.datamarket.azure.com/amla/recommendations/v2/)</span></span>

<span data-ttu-id="1718b-144">L'URI de service complet est exprimée à l'aide des éléments de la spécification OData.</span><span class="sxs-lookup"><span data-stu-id="1718b-144">The full service URI is expressed using elements of the OData specification.</span></span>

### <a name="api-version"></a><span data-ttu-id="1718b-145">Version de l'API</span><span class="sxs-lookup"><span data-stu-id="1718b-145">API version</span></span>
<span data-ttu-id="1718b-146">À la fin de chaque appel d’API doit se trouver un paramètre de requête appelé apiVersion qui doit avoir la valeur « 1.0 ».</span><span class="sxs-lookup"><span data-stu-id="1718b-146">Each API call will have, at the end, a query parameter called apiVersion that should be set to "1.0".</span></span>

### <a name="ids-are-case-sensitive"></a><span data-ttu-id="1718b-147">Respect de la casse des ID</span><span class="sxs-lookup"><span data-stu-id="1718b-147">IDs are case-sensitive</span></span>
<span data-ttu-id="1718b-148">Les ID, quelle que soit l’API qui les retourne, respectent la casse. Ils doivent donc être utilisés comme tels quand ils sont passés en tant que paramètres dans les appels d’API ultérieurs.</span><span class="sxs-lookup"><span data-stu-id="1718b-148">IDs, returned by any of the APIs, are case-sensitive and should be used as such when passed as parameters in subsequent API calls.</span></span> <span data-ttu-id="1718b-149">Par exemple, les ID de modèle et de catalogue respectent la casse.</span><span class="sxs-lookup"><span data-stu-id="1718b-149">For instance, model IDs and catalog IDs are case-sensitive.</span></span>

### <a name="create-a-model"></a><span data-ttu-id="1718b-150">Création d’un modèle</span><span class="sxs-lookup"><span data-stu-id="1718b-150">Create a model</span></span>
<span data-ttu-id="1718b-151">Création d'une requête « Créer un modèle » :</span><span class="sxs-lookup"><span data-stu-id="1718b-151">Creating a "create model" request:</span></span>

| <span data-ttu-id="1718b-152">Méthode HTTP</span><span class="sxs-lookup"><span data-stu-id="1718b-152">HTTP Method</span></span> | <span data-ttu-id="1718b-153">URI</span><span class="sxs-lookup"><span data-stu-id="1718b-153">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="1718b-154">POST</span><span class="sxs-lookup"><span data-stu-id="1718b-154">POST</span></span> |`<rootURI>/CreateModel?modelName=%27<model_name>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="1718b-155">Exemple :</span><span class="sxs-lookup"><span data-stu-id="1718b-155">Example:</span></span><br>`<rootURI>/CreateModel?modelName=%27MyFirstModel%27&apiVersion=%271.0%27` |

| <span data-ttu-id="1718b-156">Nom du paramètre</span><span class="sxs-lookup"><span data-stu-id="1718b-156">Parameter Name</span></span> | <span data-ttu-id="1718b-157">Valeurs valides</span><span class="sxs-lookup"><span data-stu-id="1718b-157">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="1718b-158">modelName</span><span class="sxs-lookup"><span data-stu-id="1718b-158">modelName</span></span> |<span data-ttu-id="1718b-159">Seuls les lettres (A-Z, a-z), les chiffres (0-9), les tirets (-) et les traits de soulignement (_) sont autorisés.</span><span class="sxs-lookup"><span data-stu-id="1718b-159">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="1718b-160">Longueur maximale : 20</span><span class="sxs-lookup"><span data-stu-id="1718b-160">Max length: 20</span></span> |
| <span data-ttu-id="1718b-161">apiVersion</span><span class="sxs-lookup"><span data-stu-id="1718b-161">apiVersion</span></span> |<span data-ttu-id="1718b-162">1.0</span><span class="sxs-lookup"><span data-stu-id="1718b-162">1.0</span></span> |
|  | |
| <span data-ttu-id="1718b-163">Corps de la requête</span><span class="sxs-lookup"><span data-stu-id="1718b-163">Request Body</span></span> |<span data-ttu-id="1718b-164">AUCUN</span><span class="sxs-lookup"><span data-stu-id="1718b-164">NONE</span></span> |

<span data-ttu-id="1718b-165">**Réponse**:</span><span class="sxs-lookup"><span data-stu-id="1718b-165">**Response**:</span></span>

<span data-ttu-id="1718b-166">Code d'état HTTP : 200</span><span class="sxs-lookup"><span data-stu-id="1718b-166">HTTP Status code: 200</span></span>

* <span data-ttu-id="1718b-167">`feed/entry/content/properties/id` : contient l'ID du modèle.</span><span class="sxs-lookup"><span data-stu-id="1718b-167">`feed/entry/content/properties/id` - Contains the model ID.</span></span>
  <span data-ttu-id="1718b-168">Notez que l’ID de modèle respecte la casse.</span><span class="sxs-lookup"><span data-stu-id="1718b-168">Note that the model ID is case-sensitive.</span></span>

<span data-ttu-id="1718b-169">OData XML</span><span class="sxs-lookup"><span data-stu-id="1718b-169">OData XML</span></span>

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


### <a name="import-catalog-data"></a><span data-ttu-id="1718b-170">Importation de données de catalogue</span><span class="sxs-lookup"><span data-stu-id="1718b-170">Import catalog data</span></span>
<span data-ttu-id="1718b-171">Si vous téléchargez plusieurs fichiers de catalogue dans le même modèle avec plusieurs appels, seuls les nouveaux éléments de catalogue sont insérés.</span><span class="sxs-lookup"><span data-stu-id="1718b-171">If you upload several catalog files to the same model with several calls, we will insert only the new catalog items.</span></span> <span data-ttu-id="1718b-172">Les éléments existants conservent leurs valeurs d'origine.</span><span class="sxs-lookup"><span data-stu-id="1718b-172">Existing items will remain with the original values.</span></span>

| <span data-ttu-id="1718b-173">Méthode HTTP</span><span class="sxs-lookup"><span data-stu-id="1718b-173">HTTP Method</span></span> | <span data-ttu-id="1718b-174">URI</span><span class="sxs-lookup"><span data-stu-id="1718b-174">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="1718b-175">POST</span><span class="sxs-lookup"><span data-stu-id="1718b-175">POST</span></span> |`<rootURI>/ImportCatalogFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="1718b-176">Exemple :</span><span class="sxs-lookup"><span data-stu-id="1718b-176">Example:</span></span><br>`<rootURI>/ImportCatalogFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="1718b-177">Nom du paramètre</span><span class="sxs-lookup"><span data-stu-id="1718b-177">Parameter Name</span></span> | <span data-ttu-id="1718b-178">Valeurs valides</span><span class="sxs-lookup"><span data-stu-id="1718b-178">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="1718b-179">modelId</span><span class="sxs-lookup"><span data-stu-id="1718b-179">modelId</span></span> |<span data-ttu-id="1718b-180">Identificateur unique du modèle (respecte la casse)</span><span class="sxs-lookup"><span data-stu-id="1718b-180">Unique identifier of the model (case-sensitive)</span></span> |
| <span data-ttu-id="1718b-181">filename</span><span class="sxs-lookup"><span data-stu-id="1718b-181">filename</span></span> |<span data-ttu-id="1718b-182">Identificateur textuel du catalogue.</span><span class="sxs-lookup"><span data-stu-id="1718b-182">Textual identifier of the catalog.</span></span><br><span data-ttu-id="1718b-183">Seuls les lettres (A-Z, a-z), les chiffres (0-9), les tirets (-) et les traits de soulignement (_) sont autorisés.</span><span class="sxs-lookup"><span data-stu-id="1718b-183">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="1718b-184">Longueur maximale : 50</span><span class="sxs-lookup"><span data-stu-id="1718b-184">Max length: 50</span></span> |
| <span data-ttu-id="1718b-185">apiVersion</span><span class="sxs-lookup"><span data-stu-id="1718b-185">apiVersion</span></span> |<span data-ttu-id="1718b-186">1.0</span><span class="sxs-lookup"><span data-stu-id="1718b-186">1.0</span></span> |
|  | |
| <span data-ttu-id="1718b-187">Corps de la requête</span><span class="sxs-lookup"><span data-stu-id="1718b-187">Request Body</span></span> |<span data-ttu-id="1718b-188">Données de catalogue.</span><span class="sxs-lookup"><span data-stu-id="1718b-188">Catalog data.</span></span> <span data-ttu-id="1718b-189">Format :</span><span class="sxs-lookup"><span data-stu-id="1718b-189">Format:</span></span><br>`<Item Id>,<Item Name>,<Item Category>[,<description>]`<br><br><table><tr><th><span data-ttu-id="1718b-190">Nom</span><span class="sxs-lookup"><span data-stu-id="1718b-190">Name</span></span></th><th><span data-ttu-id="1718b-191">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="1718b-191">Mandatory</span></span></th><th><span data-ttu-id="1718b-192">Type</span><span class="sxs-lookup"><span data-stu-id="1718b-192">Type</span></span></th><th><span data-ttu-id="1718b-193">Description</span><span class="sxs-lookup"><span data-stu-id="1718b-193">Description</span></span></th></tr><tr><td><span data-ttu-id="1718b-194">Item Id</span><span class="sxs-lookup"><span data-stu-id="1718b-194">Item Id</span></span></td><td><span data-ttu-id="1718b-195">Oui</span><span class="sxs-lookup"><span data-stu-id="1718b-195">Yes</span></span></td><td><span data-ttu-id="1718b-196">Alphanumérique, longueur maximale : 50</span><span class="sxs-lookup"><span data-stu-id="1718b-196">Alphanumeric, max length 50</span></span></td><td><span data-ttu-id="1718b-197">Identificateur unique d’un élément</span><span class="sxs-lookup"><span data-stu-id="1718b-197">Unique identifier of an item</span></span></td></tr><tr><td><span data-ttu-id="1718b-198">Item Name</span><span class="sxs-lookup"><span data-stu-id="1718b-198">Item Name</span></span></td><td><span data-ttu-id="1718b-199">Oui</span><span class="sxs-lookup"><span data-stu-id="1718b-199">Yes</span></span></td><td><span data-ttu-id="1718b-200">Alphanumérique, longueur maximale : 255</span><span class="sxs-lookup"><span data-stu-id="1718b-200">Alphanumeric, max length 255</span></span></td><td><span data-ttu-id="1718b-201">Nom de l’élément</span><span class="sxs-lookup"><span data-stu-id="1718b-201">Item name</span></span></td></tr><tr><td><span data-ttu-id="1718b-202">Item Category</span><span class="sxs-lookup"><span data-stu-id="1718b-202">Item Category</span></span></td><td><span data-ttu-id="1718b-203">Oui</span><span class="sxs-lookup"><span data-stu-id="1718b-203">Yes</span></span></td><td><span data-ttu-id="1718b-204">Alphanumérique, longueur maximale : 255</span><span class="sxs-lookup"><span data-stu-id="1718b-204">Alphanumeric, max length 255</span></span></td><td><span data-ttu-id="1718b-205">Catégorie à laquelle cet élément appartient (par exemple, livres de cuisine, pièces de théâtre, etc.)</span><span class="sxs-lookup"><span data-stu-id="1718b-205">Category to which this item belongs (for example, Cooking Books, Drama…)</span></span></td></tr><tr><td><span data-ttu-id="1718b-206">Description</span><span class="sxs-lookup"><span data-stu-id="1718b-206">Description</span></span></td><td><span data-ttu-id="1718b-207">Non</span><span class="sxs-lookup"><span data-stu-id="1718b-207">No</span></span></td><td><span data-ttu-id="1718b-208">Alphanumérique, longueur maximale : 4 000</span><span class="sxs-lookup"><span data-stu-id="1718b-208">Alphanumeric, max length 4000</span></span></td><td><span data-ttu-id="1718b-209">Description de cet élément</span><span class="sxs-lookup"><span data-stu-id="1718b-209">Description of this item</span></span></td></tr></table><br><span data-ttu-id="1718b-210">La taille de fichier maximale est de 200 Mo.</span><span class="sxs-lookup"><span data-stu-id="1718b-210">Maximum file size is 200MB.</span></span><br><br><span data-ttu-id="1718b-211">Exemple :</span><span class="sxs-lookup"><span data-stu-id="1718b-211">Example:</span></span><br><code>2406e770-769c-4189-89de-1c9283f93a96,Clara Callan,Book<br>21bf8088-b6c0-4509-870c-e1c7ac78304a,The Forgetting Room: A Fiction (Byzantium Book),Book<br>3bb5cb44-d143-4bdd-a55c-443964bf4b23,Spadework,Book<br>552a1940-21e4-4399-82bb-594b46d7ed54,Restraint of Beasts,Book</code> |

<span data-ttu-id="1718b-212">**Réponse**:</span><span class="sxs-lookup"><span data-stu-id="1718b-212">**Response**:</span></span>

<span data-ttu-id="1718b-213">Code d'état HTTP : 200</span><span class="sxs-lookup"><span data-stu-id="1718b-213">HTTP Status code: 200</span></span>

* <span data-ttu-id="1718b-214">`Feed\entry\content\properties\LineCount` : nombre de lignes acceptées.</span><span class="sxs-lookup"><span data-stu-id="1718b-214">`Feed\entry\content\properties\LineCount` - Number of lines accepted.</span></span>
* <span data-ttu-id="1718b-215">`Feed\entry\content\properties\ErrorCount` : nombre de lignes non insérées en raison d'une erreur.</span><span class="sxs-lookup"><span data-stu-id="1718b-215">`Feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due to an error.</span></span>

<span data-ttu-id="1718b-216">OData XML</span><span class="sxs-lookup"><span data-stu-id="1718b-216">OData XML</span></span>

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


### <a name="import-usage-data"></a><span data-ttu-id="1718b-217">Importation de données d'utilisation</span><span class="sxs-lookup"><span data-stu-id="1718b-217">Import usage data</span></span>
#### <a name="uploading-a-file"></a><span data-ttu-id="1718b-218">Téléchargement d’un fichier</span><span class="sxs-lookup"><span data-stu-id="1718b-218">Uploading a file</span></span>
<span data-ttu-id="1718b-219">Cette section indique comment télécharger des données d'utilisation à l'aide d'un fichier.</span><span class="sxs-lookup"><span data-stu-id="1718b-219">This section shows how to upload usage data by using a file.</span></span> <span data-ttu-id="1718b-220">Vous pouvez appeler cette API plusieurs fois avec les données d'utilisation.</span><span class="sxs-lookup"><span data-stu-id="1718b-220">You can call this API several times with usage data.</span></span> <span data-ttu-id="1718b-221">Toutes les données d'utilisation sont enregistrées pour tous les appels.</span><span class="sxs-lookup"><span data-stu-id="1718b-221">All usage data will be saved for all calls.</span></span>

| <span data-ttu-id="1718b-222">Méthode HTTP</span><span class="sxs-lookup"><span data-stu-id="1718b-222">HTTP Method</span></span> | <span data-ttu-id="1718b-223">URI</span><span class="sxs-lookup"><span data-stu-id="1718b-223">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="1718b-224">POST</span><span class="sxs-lookup"><span data-stu-id="1718b-224">POST</span></span> |`<rootURI>/ImportUsageFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="1718b-225">Exemple :</span><span class="sxs-lookup"><span data-stu-id="1718b-225">Example:</span></span><br>`<rootURI>/ImportUsageFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27ImplicitMatrix10_Guid_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="1718b-226">Nom du paramètre</span><span class="sxs-lookup"><span data-stu-id="1718b-226">Parameter Name</span></span> | <span data-ttu-id="1718b-227">Valeurs valides</span><span class="sxs-lookup"><span data-stu-id="1718b-227">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="1718b-228">modelId</span><span class="sxs-lookup"><span data-stu-id="1718b-228">modelId</span></span> |<span data-ttu-id="1718b-229">Identificateur unique du modèle (respecte la casse)</span><span class="sxs-lookup"><span data-stu-id="1718b-229">Unique identifier of the model (case-sensitive)</span></span> |
| <span data-ttu-id="1718b-230">filename</span><span class="sxs-lookup"><span data-stu-id="1718b-230">filename</span></span> |<span data-ttu-id="1718b-231">Identificateur textuel du catalogue.</span><span class="sxs-lookup"><span data-stu-id="1718b-231">Textual identifier of the catalog.</span></span><br><span data-ttu-id="1718b-232">Seuls les lettres (A-Z, a-z), les chiffres (0-9), les tirets (-) et les traits de soulignement (_) sont autorisés.</span><span class="sxs-lookup"><span data-stu-id="1718b-232">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="1718b-233">Longueur maximale : 50</span><span class="sxs-lookup"><span data-stu-id="1718b-233">Max length: 50</span></span> |
| <span data-ttu-id="1718b-234">apiVersion</span><span class="sxs-lookup"><span data-stu-id="1718b-234">apiVersion</span></span> |<span data-ttu-id="1718b-235">1.0</span><span class="sxs-lookup"><span data-stu-id="1718b-235">1.0</span></span> |
|  | |
| <span data-ttu-id="1718b-236">Corps de la requête</span><span class="sxs-lookup"><span data-stu-id="1718b-236">Request Body</span></span> |<span data-ttu-id="1718b-237">Données d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="1718b-237">Usage data.</span></span> <span data-ttu-id="1718b-238">Format :</span><span class="sxs-lookup"><span data-stu-id="1718b-238">Format:</span></span><br>`<User Id>,<Item Id>[,<Time>,<Event>]`<br><br><table><tr><th><span data-ttu-id="1718b-239">Nom</span><span class="sxs-lookup"><span data-stu-id="1718b-239">Name</span></span></th><th><span data-ttu-id="1718b-240">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="1718b-240">Mandatory</span></span></th><th><span data-ttu-id="1718b-241">Type</span><span class="sxs-lookup"><span data-stu-id="1718b-241">Type</span></span></th><th><span data-ttu-id="1718b-242">Description</span><span class="sxs-lookup"><span data-stu-id="1718b-242">Description</span></span></th></tr><tr><td><span data-ttu-id="1718b-243">User Id</span><span class="sxs-lookup"><span data-stu-id="1718b-243">User Id</span></span></td><td><span data-ttu-id="1718b-244">Oui</span><span class="sxs-lookup"><span data-stu-id="1718b-244">Yes</span></span></td><td><span data-ttu-id="1718b-245">Alphanumérique</span><span class="sxs-lookup"><span data-stu-id="1718b-245">Alphanumeric</span></span></td><td><span data-ttu-id="1718b-246">Identificateur unique d’un utilisateur</span><span class="sxs-lookup"><span data-stu-id="1718b-246">Unique identifier of a user</span></span></td></tr><tr><td><span data-ttu-id="1718b-247">Item Id</span><span class="sxs-lookup"><span data-stu-id="1718b-247">Item Id</span></span></td><td><span data-ttu-id="1718b-248">Oui</span><span class="sxs-lookup"><span data-stu-id="1718b-248">Yes</span></span></td><td><span data-ttu-id="1718b-249">Alphanumérique, longueur maximale : 50</span><span class="sxs-lookup"><span data-stu-id="1718b-249">Alphanumeric, max length 50</span></span></td><td><span data-ttu-id="1718b-250">Identificateur unique d’un élément</span><span class="sxs-lookup"><span data-stu-id="1718b-250">Unique identifier of an item</span></span></td></tr><tr><td><span data-ttu-id="1718b-251">Time</span><span class="sxs-lookup"><span data-stu-id="1718b-251">Time</span></span></td><td><span data-ttu-id="1718b-252">Non</span><span class="sxs-lookup"><span data-stu-id="1718b-252">No</span></span></td><td><span data-ttu-id="1718b-253">Date au format suivant : AAAA/MM/JJTHH:MM:SS (par exemple, 2013/06/20T10:00:00)</span><span class="sxs-lookup"><span data-stu-id="1718b-253">Date in format: YYYY/MM/DDTHH:MM:SS (for example, 2013/06/20T10:00:00)</span></span></td><td><span data-ttu-id="1718b-254">Indication de temps des données</span><span class="sxs-lookup"><span data-stu-id="1718b-254">Time of data</span></span></td></tr><tr><td><span data-ttu-id="1718b-255">Événement</span><span class="sxs-lookup"><span data-stu-id="1718b-255">Event</span></span></td><td><span data-ttu-id="1718b-256">Non, mais s'il est indiqué, la date doit l'être également</span><span class="sxs-lookup"><span data-stu-id="1718b-256">No, if supplied then must also put date</span></span></td><td><span data-ttu-id="1718b-257">Celui-ci peut avoir l'une des valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="1718b-257">One of the following:</span></span><br><span data-ttu-id="1718b-258">• Click (clic)</span><span class="sxs-lookup"><span data-stu-id="1718b-258">• Click</span></span><br><span data-ttu-id="1718b-259">• RecommendationClick (clic de recommandation)</span><span class="sxs-lookup"><span data-stu-id="1718b-259">• RecommendationClick</span></span><br><span data-ttu-id="1718b-260">•    AddShopCart (ajout au panier)</span><span class="sxs-lookup"><span data-stu-id="1718b-260">•    AddShopCart</span></span><br><span data-ttu-id="1718b-261">• RemoveShopCart (suppression du panier)</span><span class="sxs-lookup"><span data-stu-id="1718b-261">• RemoveShopCart</span></span><br><span data-ttu-id="1718b-262">• Purchase</span><span class="sxs-lookup"><span data-stu-id="1718b-262">• Purchase</span></span></td><td></td></tr></table><br><span data-ttu-id="1718b-263">La taille de fichier maximale est de 200 Mo.</span><span class="sxs-lookup"><span data-stu-id="1718b-263">Maximum file size is 200MB.</span></span><br><br><span data-ttu-id="1718b-264">Exemple :</span><span class="sxs-lookup"><span data-stu-id="1718b-264">Example:</span></span><br><pre>149452,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>6360,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>50321,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>71285,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>224450,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>236645,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>107951,1b3d95e2-84e4-414c-bb38-be9cf461c347</pre> |

<span data-ttu-id="1718b-265">**Réponse**:</span><span class="sxs-lookup"><span data-stu-id="1718b-265">**Response**:</span></span>

<span data-ttu-id="1718b-266">Code d'état HTTP : 200</span><span class="sxs-lookup"><span data-stu-id="1718b-266">HTTP Status code: 200</span></span>

* <span data-ttu-id="1718b-267">`Feed\entry\content\properties\LineCount` : nombre de lignes acceptées.</span><span class="sxs-lookup"><span data-stu-id="1718b-267">`Feed\entry\content\properties\LineCount` - Number of lines accepted.</span></span>
* <span data-ttu-id="1718b-268">`Feed\entry\content\properties\ErrorCount` : nombre de lignes non insérées en raison d'une erreur.</span><span class="sxs-lookup"><span data-stu-id="1718b-268">`Feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due to an error.</span></span>
* <span data-ttu-id="1718b-269">`Feed\entry\content\properties\FileId` : identificateur de fichier.</span><span class="sxs-lookup"><span data-stu-id="1718b-269">`Feed\entry\content\properties\FileId` - File identifier.</span></span>

<span data-ttu-id="1718b-270">OData XML</span><span class="sxs-lookup"><span data-stu-id="1718b-270">OData XML</span></span>

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


#### <a name="using-data-acquisition"></a><span data-ttu-id="1718b-271">Utilisation de l'acquisition de données</span><span class="sxs-lookup"><span data-stu-id="1718b-271">Using data acquisition</span></span>
<span data-ttu-id="1718b-272">Cette section explique comment envoyer des événements en temps réel à Azure Machine Learning Recommendations, généralement à partir de votre site web.</span><span class="sxs-lookup"><span data-stu-id="1718b-272">This section shows how to send events in real time to Azure Machine Learning Recommendations, usually from your website.</span></span>

| <span data-ttu-id="1718b-273">Méthode HTTP</span><span class="sxs-lookup"><span data-stu-id="1718b-273">HTTP Method</span></span> | <span data-ttu-id="1718b-274">URI</span><span class="sxs-lookup"><span data-stu-id="1718b-274">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="1718b-275">POST</span><span class="sxs-lookup"><span data-stu-id="1718b-275">POST</span></span> |`<rootURI>/AddUsageEvent?apiVersion=%271.0%27-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="1718b-276">Nom du paramètre</span><span class="sxs-lookup"><span data-stu-id="1718b-276">Parameter Name</span></span> | <span data-ttu-id="1718b-277">Valeurs valides</span><span class="sxs-lookup"><span data-stu-id="1718b-277">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="1718b-278">apiVersion</span><span class="sxs-lookup"><span data-stu-id="1718b-278">apiVersion</span></span> |<span data-ttu-id="1718b-279">1.0</span><span class="sxs-lookup"><span data-stu-id="1718b-279">1.0</span></span> |
|  | |
| <span data-ttu-id="1718b-280">Corps de la demande</span><span class="sxs-lookup"><span data-stu-id="1718b-280">Request body</span></span> |<span data-ttu-id="1718b-281">Entrée de données d'événement pour chaque événement à envoyer.</span><span class="sxs-lookup"><span data-stu-id="1718b-281">Event data entry for each event you want to send.</span></span> <span data-ttu-id="1718b-282">Pour une même session d'utilisateur ou de navigateur, vous devez envoyer le même ID dans le champ SessionId.</span><span class="sxs-lookup"><span data-stu-id="1718b-282">You should send for the same user or browser session the same ID in the SessionId field.</span></span> <span data-ttu-id="1718b-283">(Consultez l'exemple du corps d'événement ci-dessous.)</span><span class="sxs-lookup"><span data-stu-id="1718b-283">(See sample of event body below.)</span></span> |

* <span data-ttu-id="1718b-284">Exemple pour l'événement « Click » :</span><span class="sxs-lookup"><span data-stu-id="1718b-284">Example for event 'Click':</span></span>
  
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
* <span data-ttu-id="1718b-285">Exemple pour l'événement « RecommendationClick » :</span><span class="sxs-lookup"><span data-stu-id="1718b-285">Example for event 'RecommendationClick':</span></span>
  
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
* <span data-ttu-id="1718b-286">Exemple pour l'événement « AddShopCart » :</span><span class="sxs-lookup"><span data-stu-id="1718b-286">Example for event 'AddShopCart':</span></span>
  
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
* <span data-ttu-id="1718b-287">Exemple pour l'événement « RemoveShopCart » :</span><span class="sxs-lookup"><span data-stu-id="1718b-287">Example for event 'RemoveShopCart':</span></span>
  
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
* <span data-ttu-id="1718b-288">Exemple pour l’événement « Purchase » :</span><span class="sxs-lookup"><span data-stu-id="1718b-288">Example for event 'Purchase':</span></span>
  
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
* <span data-ttu-id="1718b-289">Exemple d'envoi de 2 événements « Click » et « AddShopCart » :</span><span class="sxs-lookup"><span data-stu-id="1718b-289">Example sending 2 events, 'Click' and 'AddShopCart':</span></span>
  
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

<span data-ttu-id="1718b-290">**Réponse**: Code d'état HTTP : 200</span><span class="sxs-lookup"><span data-stu-id="1718b-290">**Response**: HTTP Status code: 200</span></span>

### <a name="build-a-recommendation-model"></a><span data-ttu-id="1718b-291">Génération d'un modèle de recommandation</span><span class="sxs-lookup"><span data-stu-id="1718b-291">Build a recommendation model</span></span>
| <span data-ttu-id="1718b-292">Méthode HTTP</span><span class="sxs-lookup"><span data-stu-id="1718b-292">HTTP Method</span></span> | <span data-ttu-id="1718b-293">URI</span><span class="sxs-lookup"><span data-stu-id="1718b-293">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="1718b-294">POST</span><span class="sxs-lookup"><span data-stu-id="1718b-294">POST</span></span> |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="1718b-295">Exemple :</span><span class="sxs-lookup"><span data-stu-id="1718b-295">Example:</span></span><br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&apiVersion=%271.0%27` |

| <span data-ttu-id="1718b-296">Nom du paramètre</span><span class="sxs-lookup"><span data-stu-id="1718b-296">Parameter Name</span></span> | <span data-ttu-id="1718b-297">Valeurs valides</span><span class="sxs-lookup"><span data-stu-id="1718b-297">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="1718b-298">modelId</span><span class="sxs-lookup"><span data-stu-id="1718b-298">modelId</span></span> |<span data-ttu-id="1718b-299">Identificateur unique du modèle (respecte la casse)</span><span class="sxs-lookup"><span data-stu-id="1718b-299">Unique identifier of the model (case-sensitive)</span></span> |
| <span data-ttu-id="1718b-300">userDescription</span><span class="sxs-lookup"><span data-stu-id="1718b-300">userDescription</span></span> |<span data-ttu-id="1718b-301">Identificateur textuel du catalogue.</span><span class="sxs-lookup"><span data-stu-id="1718b-301">Textual identifier of the catalog.</span></span> <span data-ttu-id="1718b-302">Notez que si vous utilisez des espaces, vous devez plutôt l'encoder avec %20.</span><span class="sxs-lookup"><span data-stu-id="1718b-302">Note that if you use spaces you must encode it with %20 instead.</span></span> <span data-ttu-id="1718b-303">Consultez l'exemple ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="1718b-303">See example above.</span></span><br><span data-ttu-id="1718b-304">Longueur maximale : 50</span><span class="sxs-lookup"><span data-stu-id="1718b-304">Max length: 50</span></span> |
| <span data-ttu-id="1718b-305">apiVersion</span><span class="sxs-lookup"><span data-stu-id="1718b-305">apiVersion</span></span> |<span data-ttu-id="1718b-306">1.0</span><span class="sxs-lookup"><span data-stu-id="1718b-306">1.0</span></span> |
|  | |
| <span data-ttu-id="1718b-307">Corps de la requête</span><span class="sxs-lookup"><span data-stu-id="1718b-307">Request Body</span></span> |<span data-ttu-id="1718b-308">AUCUN</span><span class="sxs-lookup"><span data-stu-id="1718b-308">NONE</span></span> |

<span data-ttu-id="1718b-309">**Réponse**:</span><span class="sxs-lookup"><span data-stu-id="1718b-309">**Response**:</span></span>

<span data-ttu-id="1718b-310">Code d'état HTTP : 200</span><span class="sxs-lookup"><span data-stu-id="1718b-310">HTTP Status code: 200</span></span>

<span data-ttu-id="1718b-311">Il s'agit d'une API asynchrone.</span><span class="sxs-lookup"><span data-stu-id="1718b-311">This is an asynchronous API.</span></span> <span data-ttu-id="1718b-312">La réponse obtenue est un ID de build.</span><span class="sxs-lookup"><span data-stu-id="1718b-312">You will get a build ID as a response.</span></span> <span data-ttu-id="1718b-313">Pour savoir à quel moment la build s'est terminée, vous devez appeler l'API « Get Builds Status of a Model » (obtention de l'état de build d'un modèle) et rechercher cet ID de build dans la réponse.</span><span class="sxs-lookup"><span data-stu-id="1718b-313">To know when the build has ended, you should call the "Get Builds Status of a Model" API and locate this build ID in the response.</span></span> <span data-ttu-id="1718b-314">Notez que l'exécution d'une build peut nécessiter de quelques minutes à plusieurs heures selon la taille des données.</span><span class="sxs-lookup"><span data-stu-id="1718b-314">Note that a build can take from minutes to hours depending on the size of the data.</span></span>

<span data-ttu-id="1718b-315">Vous ne pouvez pas utiliser de recommandations tant que la build n'est pas terminée.</span><span class="sxs-lookup"><span data-stu-id="1718b-315">You cannot consume recommendations till the build ends.</span></span>

<span data-ttu-id="1718b-316">État de build valide :</span><span class="sxs-lookup"><span data-stu-id="1718b-316">Valid build status:</span></span>

* <span data-ttu-id="1718b-317">Create : le modèle a été créé.</span><span class="sxs-lookup"><span data-stu-id="1718b-317">Create – Model was created.</span></span>
* <span data-ttu-id="1718b-318">Queued : la build de modèle a été déclenchée et mise en file d'attente.</span><span class="sxs-lookup"><span data-stu-id="1718b-318">Queued – Model build was triggered and it is queued.</span></span>
* <span data-ttu-id="1718b-319">Building : le modèle est en cours de génération.</span><span class="sxs-lookup"><span data-stu-id="1718b-319">Building – Model is being built.</span></span>
* <span data-ttu-id="1718b-320">Success : la build a été correctement exécutée.</span><span class="sxs-lookup"><span data-stu-id="1718b-320">Success – Build ended successfully.</span></span>
* <span data-ttu-id="1718b-321">Error : la build s'est terminée par un échec.</span><span class="sxs-lookup"><span data-stu-id="1718b-321">Error – Build ended with a failure.</span></span>
* <span data-ttu-id="1718b-322">Canceled : la build a été annulée.</span><span class="sxs-lookup"><span data-stu-id="1718b-322">Canceled – Build was canceled.</span></span>
* <span data-ttu-id="1718b-323">Canceling : la build est en cours d’annulation.</span><span class="sxs-lookup"><span data-stu-id="1718b-323">Canceling – Build is being canceled.</span></span>

<span data-ttu-id="1718b-324">Notez que l'ID de build se trouve sous le chemin suivant : `Feed\entry\content\properties\Id`</span><span class="sxs-lookup"><span data-stu-id="1718b-324">Note that the build ID can be found under the following path: `Feed\entry\content\properties\Id`</span></span>

<span data-ttu-id="1718b-325">OData XML</span><span class="sxs-lookup"><span data-stu-id="1718b-325">OData XML</span></span>

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

### <a name="get-build-status-of-a-model"></a><span data-ttu-id="1718b-326">Obtention de l’état de build d’un modèle</span><span class="sxs-lookup"><span data-stu-id="1718b-326">Get build status of a model</span></span>
| <span data-ttu-id="1718b-327">Méthode HTTP</span><span class="sxs-lookup"><span data-stu-id="1718b-327">HTTP Method</span></span> | <span data-ttu-id="1718b-328">URI</span><span class="sxs-lookup"><span data-stu-id="1718b-328">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="1718b-329">GET</span><span class="sxs-lookup"><span data-stu-id="1718b-329">GET</span></span> |`<rootURI>/GetModelBuildsStatus?modelId=%27<modelId>%27&onlyLastBuild=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="1718b-330">Exemple :</span><span class="sxs-lookup"><span data-stu-id="1718b-330">Example:</span></span><br>`<rootURI>/GetModelBuildsStatus?modelId=%279559872f-7a53-4076-a3c7-19d9385c1265%27&onlyLastBuild=true&apiVersion=%271.0%27` |

| <span data-ttu-id="1718b-331">Nom du paramètre</span><span class="sxs-lookup"><span data-stu-id="1718b-331">Parameter Name</span></span> | <span data-ttu-id="1718b-332">Valeurs valides</span><span class="sxs-lookup"><span data-stu-id="1718b-332">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="1718b-333">modelId</span><span class="sxs-lookup"><span data-stu-id="1718b-333">modelId</span></span> |<span data-ttu-id="1718b-334">Identificateur unique du modèle (respecte la casse)</span><span class="sxs-lookup"><span data-stu-id="1718b-334">Unique identifier of the model  (case-sensitive)</span></span> |
| <span data-ttu-id="1718b-335">onlyLastBuild</span><span class="sxs-lookup"><span data-stu-id="1718b-335">onlyLastBuild</span></span> |<span data-ttu-id="1718b-336">Indique s'il faut retourner l'historique de build du modèle en totalité ou uniquement l'état de la build la plus récente.</span><span class="sxs-lookup"><span data-stu-id="1718b-336">Indicates whether to return all the build history of the model or only the status of the most recent build.</span></span> |
| <span data-ttu-id="1718b-337">apiVersion</span><span class="sxs-lookup"><span data-stu-id="1718b-337">apiVersion</span></span> |<span data-ttu-id="1718b-338">1.0</span><span class="sxs-lookup"><span data-stu-id="1718b-338">1.0</span></span> |

<span data-ttu-id="1718b-339">**Réponse**:</span><span class="sxs-lookup"><span data-stu-id="1718b-339">**Response**:</span></span>

<span data-ttu-id="1718b-340">Code d'état HTTP : 200</span><span class="sxs-lookup"><span data-stu-id="1718b-340">HTTP Status code: 200</span></span>

<span data-ttu-id="1718b-341">La réponse inclut une entrée par build.</span><span class="sxs-lookup"><span data-stu-id="1718b-341">The response includes one entry per build.</span></span> <span data-ttu-id="1718b-342">Chaque entrée comprend les données suivantes :</span><span class="sxs-lookup"><span data-stu-id="1718b-342">Each entry has the following data:</span></span>

* <span data-ttu-id="1718b-343">`feed/entry/content/properties/UserName` : nom de l'utilisateur.</span><span class="sxs-lookup"><span data-stu-id="1718b-343">`feed/entry/content/properties/UserName` – Name of the user.</span></span>
* <span data-ttu-id="1718b-344">`feed/entry/content/properties/ModelName` : nom du modèle.</span><span class="sxs-lookup"><span data-stu-id="1718b-344">`feed/entry/content/properties/ModelName` – Name of the model.</span></span>
* <span data-ttu-id="1718b-345">`feed/entry/content/properties/ModelId` : identificateur unique du modèle.</span><span class="sxs-lookup"><span data-stu-id="1718b-345">`feed/entry/content/properties/ModelId` – Model unique identifier.</span></span>
* <span data-ttu-id="1718b-346">`feed/entry/content/properties/IsDeployed` : indique si la build est déployée</span><span class="sxs-lookup"><span data-stu-id="1718b-346">`feed/entry/content/properties/IsDeployed` – Whether the build is deployed (a.k.a.</span></span> <span data-ttu-id="1718b-347">(c’est-à-dire active).</span><span class="sxs-lookup"><span data-stu-id="1718b-347">active build).</span></span>
* <span data-ttu-id="1718b-348">`feed/entry/content/properties/BuildId` : identificateur unique de la build.</span><span class="sxs-lookup"><span data-stu-id="1718b-348">`feed/entry/content/properties/BuildId` – Build unique identifier.</span></span>
* <span data-ttu-id="1718b-349">`feed/entry/content/properties/BuildType` : type de build.</span><span class="sxs-lookup"><span data-stu-id="1718b-349">`feed/entry/content/properties/BuildType` - Type of the build.</span></span>
* <span data-ttu-id="1718b-350">`feed/entry/content/properties/Status` : état de la build.</span><span class="sxs-lookup"><span data-stu-id="1718b-350">`feed/entry/content/properties/Status` – Build status.</span></span> <span data-ttu-id="1718b-351">Celui-ci peut avoir l’une des valeurs suivantes : Error, Building, Queued, Canceling, Canceled, Success.</span><span class="sxs-lookup"><span data-stu-id="1718b-351">Can be one of the following: Error, Building, Queued, Canceling, Canceled, Success</span></span>
* <span data-ttu-id="1718b-352">`feed/entry/content/properties/StatusMessage` : message d'état détaillé (s'applique uniquement à des états spécifiques).</span><span class="sxs-lookup"><span data-stu-id="1718b-352">`feed/entry/content/properties/StatusMessage` – Detailed status message (applies only to specific states).</span></span>
* <span data-ttu-id="1718b-353">`feed/entry/content/properties/Progress` : progression de l'exécution de la build (%).</span><span class="sxs-lookup"><span data-stu-id="1718b-353">`feed/entry/content/properties/Progress` – Build progress (%).</span></span>
* <span data-ttu-id="1718b-354">`feed/entry/content/properties/StartTime` : heure de début de l'exécution de la build.</span><span class="sxs-lookup"><span data-stu-id="1718b-354">`feed/entry/content/properties/StartTime` – Build start time.</span></span>
* <span data-ttu-id="1718b-355">`feed/entry/content/properties/EndTime` : heure de fin de l'exécution de la build.</span><span class="sxs-lookup"><span data-stu-id="1718b-355">`feed/entry/content/properties/EndTime` – Build end time.</span></span>
* <span data-ttu-id="1718b-356">`feed/entry/content/properties/ExecutionTime` : durée de la build.</span><span class="sxs-lookup"><span data-stu-id="1718b-356">`feed/entry/content/properties/ExecutionTime` – Build duration.</span></span>
* <span data-ttu-id="1718b-357">`feed/entry/content/properties/ProgressStep` : détails sur l’étape actuelle d’une build.</span><span class="sxs-lookup"><span data-stu-id="1718b-357">`feed/entry/content/properties/ProgressStep` – Details about the current stage that a build in progress is in.</span></span>

<span data-ttu-id="1718b-358">État de build valide :</span><span class="sxs-lookup"><span data-stu-id="1718b-358">Valid build status:</span></span>

* <span data-ttu-id="1718b-359">Created : l’entrée de demande de build a été créée.</span><span class="sxs-lookup"><span data-stu-id="1718b-359">Created – Build request entry was created.</span></span>
* <span data-ttu-id="1718b-360">Queued : la demande de build a été déclenchée et mise en attente.</span><span class="sxs-lookup"><span data-stu-id="1718b-360">Queued – Build request was triggered and it is queued.</span></span>
* <span data-ttu-id="1718b-361">Building : la build est en cours.</span><span class="sxs-lookup"><span data-stu-id="1718b-361">Building – Build is in process.</span></span>
* <span data-ttu-id="1718b-362">Success : la build a été correctement exécutée.</span><span class="sxs-lookup"><span data-stu-id="1718b-362">Success – Build ended successfully.</span></span>
* <span data-ttu-id="1718b-363">Error : la build s'est terminée par un échec.</span><span class="sxs-lookup"><span data-stu-id="1718b-363">Error – Build ended with a failure.</span></span>
* <span data-ttu-id="1718b-364">Canceled : la build a été annulée.</span><span class="sxs-lookup"><span data-stu-id="1718b-364">Canceled – Build was canceled.</span></span>
* <span data-ttu-id="1718b-365">Canceling : la build est en cours d’annulation.</span><span class="sxs-lookup"><span data-stu-id="1718b-365">Canceling – Build is being canceled.</span></span>

<span data-ttu-id="1718b-366">Valeurs valides pour le type de build :</span><span class="sxs-lookup"><span data-stu-id="1718b-366">Valid values for build type:</span></span>

* <span data-ttu-id="1718b-367">Rank - Build de classement.</span><span class="sxs-lookup"><span data-stu-id="1718b-367">Rank - Rank build.</span></span> <span data-ttu-id="1718b-368">(Pour plus d’informations sur les builds de classement, consultez le document « Documentation sur les API Machine Learning Recommandation »).</span><span class="sxs-lookup"><span data-stu-id="1718b-368">(For rank build details, please refer to the "Machine Learning Recommendation API documentation" document.)</span></span>
* <span data-ttu-id="1718b-369">Recommendation - Build de recommandation.</span><span class="sxs-lookup"><span data-stu-id="1718b-369">Recommendation - Recommendation build.</span></span>
* <span data-ttu-id="1718b-370">Fbt - Build fréquemment achetés ensemble.</span><span class="sxs-lookup"><span data-stu-id="1718b-370">Fbt - Frequently bought together build.</span></span>

<span data-ttu-id="1718b-371">OData XML</span><span class="sxs-lookup"><span data-stu-id="1718b-371">OData XML</span></span>

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


### <a name="get-recommendations"></a><span data-ttu-id="1718b-372">Obtention de recommandations</span><span class="sxs-lookup"><span data-stu-id="1718b-372">Get recommendations</span></span>
| <span data-ttu-id="1718b-373">Méthode HTTP</span><span class="sxs-lookup"><span data-stu-id="1718b-373">HTTP Method</span></span> | <span data-ttu-id="1718b-374">URI</span><span class="sxs-lookup"><span data-stu-id="1718b-374">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="1718b-375">GET</span><span class="sxs-lookup"><span data-stu-id="1718b-375">GET</span></span> |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="1718b-376">Exemple :</span><span class="sxs-lookup"><span data-stu-id="1718b-376">Example:</span></span><br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="1718b-377">Nom du paramètre</span><span class="sxs-lookup"><span data-stu-id="1718b-377">Parameter Name</span></span> | <span data-ttu-id="1718b-378">Valeurs valides</span><span class="sxs-lookup"><span data-stu-id="1718b-378">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="1718b-379">modelId</span><span class="sxs-lookup"><span data-stu-id="1718b-379">modelId</span></span> |<span data-ttu-id="1718b-380">Identificateur unique du modèle (respecte la casse)</span><span class="sxs-lookup"><span data-stu-id="1718b-380">Unique identifier of the model (case-sensitive)</span></span> |
| <span data-ttu-id="1718b-381">itemIds</span><span class="sxs-lookup"><span data-stu-id="1718b-381">itemIds</span></span> |<span data-ttu-id="1718b-382">Liste des éléments séparés par des virgules faisant l’objet d’une recommandation.</span><span class="sxs-lookup"><span data-stu-id="1718b-382">Comma-separated list of the items to recommend for.</span></span><br><span data-ttu-id="1718b-383">Longueur maximale : 1024</span><span class="sxs-lookup"><span data-stu-id="1718b-383">Max length: 1024</span></span> |
| <span data-ttu-id="1718b-384">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="1718b-384">numberOfResults</span></span> |<span data-ttu-id="1718b-385">Nombre de résultats requis</span><span class="sxs-lookup"><span data-stu-id="1718b-385">Number of required results</span></span> |
| <span data-ttu-id="1718b-386">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="1718b-386">includeMetatadata</span></span> |<span data-ttu-id="1718b-387">Utilisation ultérieure, toujours false</span><span class="sxs-lookup"><span data-stu-id="1718b-387">Future use, always false</span></span> |
| <span data-ttu-id="1718b-388">apiVersion</span><span class="sxs-lookup"><span data-stu-id="1718b-388">apiVersion</span></span> |<span data-ttu-id="1718b-389">1.0</span><span class="sxs-lookup"><span data-stu-id="1718b-389">1.0</span></span> |

<span data-ttu-id="1718b-390">**Réponse :**</span><span class="sxs-lookup"><span data-stu-id="1718b-390">**Response:**</span></span>

<span data-ttu-id="1718b-391">Code d'état HTTP : 200</span><span class="sxs-lookup"><span data-stu-id="1718b-391">HTTP Status code: 200</span></span>

<span data-ttu-id="1718b-392">La réponse inclut une entrée par élément recommandé.</span><span class="sxs-lookup"><span data-stu-id="1718b-392">The response includes one entry per recommended item.</span></span> <span data-ttu-id="1718b-393">Chaque entrée comprend les données suivantes :</span><span class="sxs-lookup"><span data-stu-id="1718b-393">Each entry has the following data:</span></span>

* <span data-ttu-id="1718b-394">`Feed\entry\content\properties\Id` : ID d’élément recommandé</span><span class="sxs-lookup"><span data-stu-id="1718b-394">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="1718b-395">`Feed\entry\content\properties\Name` : nom de l’élément</span><span class="sxs-lookup"><span data-stu-id="1718b-395">`Feed\entry\content\properties\Name` - Name of the item.</span></span>
* <span data-ttu-id="1718b-396">`Feed\entry\content\properties\Rating` : évaluation de la recommandation ; plus le nombre est élevé, plus le niveau de confiance est élevé.</span><span class="sxs-lookup"><span data-stu-id="1718b-396">`Feed\entry\content\properties\Rating` - Rating of the recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="1718b-397">`Feed\entry\content\properties\Reasoning` : raisonnement de la recommandation (par exemple, pour expliquer les recommandations).</span><span class="sxs-lookup"><span data-stu-id="1718b-397">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (for example, recommendation explanations).</span></span>

<span data-ttu-id="1718b-398">OData XML</span><span class="sxs-lookup"><span data-stu-id="1718b-398">OData XML</span></span>

<span data-ttu-id="1718b-399">L’exemple de réponse ci-dessous comprend 10 éléments recommandés :</span><span class="sxs-lookup"><span data-stu-id="1718b-399">The example response below includes 10 recommended items:</span></span>

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

### <a name="update-model"></a><span data-ttu-id="1718b-400">Mise à jour du modèle</span><span class="sxs-lookup"><span data-stu-id="1718b-400">Update model</span></span>
<span data-ttu-id="1718b-401">Vous pouvez mettre à jour la description du modèle ou l’identifiant de la build active.</span><span class="sxs-lookup"><span data-stu-id="1718b-401">You can update the model description or the active build ID.</span></span>
<span data-ttu-id="1718b-402">*Identifiant de build active* : pour chaque modèle, chaque build possède un identifiant de build.</span><span class="sxs-lookup"><span data-stu-id="1718b-402">*Active build ID* - Every build for every model has a build ID.</span></span> <span data-ttu-id="1718b-403">L'ID de build active correspond à la première build réussie de chaque nouveau modèle.</span><span class="sxs-lookup"><span data-stu-id="1718b-403">The active build ID is the first successful build of every new model.</span></span> <span data-ttu-id="1718b-404">Une fois que vous avez un ID de build active et que vous effectuez d'autres builds pour le même modèle, vous pouvez le définir explicitement comme ID de build par défaut.</span><span class="sxs-lookup"><span data-stu-id="1718b-404">Once you have an active build ID and you do additional builds for the same model, you need to explicitly set it as the default build ID if you want to.</span></span> <span data-ttu-id="1718b-405">Quand vous utilisez des recommandations, si vous ne spécifiez pas l’identifiant de build que vous souhaitez utiliser, un identifiant par défaut est automatiquement utilisé.</span><span class="sxs-lookup"><span data-stu-id="1718b-405">When you consume recommendations, if you do not specify the build ID that you want to use, the default one will be used automatically.</span></span>

<span data-ttu-id="1718b-406">Ce mécanisme vous permet, une fois que vous disposez d'un modèle de recommandation en production, de générer de nouveaux modèles et de les tester avant de les passer en production.</span><span class="sxs-lookup"><span data-stu-id="1718b-406">This mechanism enables you - once you have a recommendation model in production - to build new models and test them before you promote them to production.</span></span>

| <span data-ttu-id="1718b-407">Méthode HTTP</span><span class="sxs-lookup"><span data-stu-id="1718b-407">HTTP Method</span></span> | <span data-ttu-id="1718b-408">URI</span><span class="sxs-lookup"><span data-stu-id="1718b-408">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="1718b-409">PUT</span><span class="sxs-lookup"><span data-stu-id="1718b-409">PUT</span></span> |`<rootURI>/UpdateModel?id=%27<modelId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="1718b-410">Exemple :</span><span class="sxs-lookup"><span data-stu-id="1718b-410">Example:</span></span><br>`<rootURI>/UpdateModel?id=%279559872f-7a53-4076-a3c7-19d9385c1265%27&apiVersion=%271.0%27` |

| <span data-ttu-id="1718b-411">Nom du paramètre</span><span class="sxs-lookup"><span data-stu-id="1718b-411">Parameter Name</span></span> | <span data-ttu-id="1718b-412">Valeurs valides</span><span class="sxs-lookup"><span data-stu-id="1718b-412">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="1718b-413">id</span><span class="sxs-lookup"><span data-stu-id="1718b-413">id</span></span> |<span data-ttu-id="1718b-414">Identificateur unique du modèle (respecte la casse)</span><span class="sxs-lookup"><span data-stu-id="1718b-414">Unique identifier of the model (case-sensitive)</span></span> |
| <span data-ttu-id="1718b-415">apiVersion</span><span class="sxs-lookup"><span data-stu-id="1718b-415">apiVersion</span></span> |<span data-ttu-id="1718b-416">1.0</span><span class="sxs-lookup"><span data-stu-id="1718b-416">1.0</span></span> |
|  | |
| <span data-ttu-id="1718b-417">Corps de la requête</span><span class="sxs-lookup"><span data-stu-id="1718b-417">Request Body</span></span> |`<ModelUpdateParams xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">`<br>`   <Description>New Description</Description>`<br>`          <ActiveBuildId>-1</ActiveBuildId>`<br>`</ModelUpdateParams>`<br><br><span data-ttu-id="1718b-418">Notez que les balises XML Description et ActiveBuildId sont facultatives.</span><span class="sxs-lookup"><span data-stu-id="1718b-418">Note that the XML tags Description and ActiveBuildId are optional.</span></span> <span data-ttu-id="1718b-419">Si vous ne souhaitez pas définir Description ou ActiveBuildId, supprimez la balise entière.</span><span class="sxs-lookup"><span data-stu-id="1718b-419">If you do not want to set Description or ActiveBuildId, remove the entire tag.</span></span> |

<span data-ttu-id="1718b-420">**Réponse**:</span><span class="sxs-lookup"><span data-stu-id="1718b-420">**Response**:</span></span>

<span data-ttu-id="1718b-421">Code d'état HTTP : 200</span><span class="sxs-lookup"><span data-stu-id="1718b-421">HTTP Status code: 200</span></span>

<span data-ttu-id="1718b-422">OData XML</span><span class="sxs-lookup"><span data-stu-id="1718b-422">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Update an Existing Model</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel?id='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T10:27:17Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel?id='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;apiVersion='1.0'" />
    </feed>

## <a name="legal"></a><span data-ttu-id="1718b-423">Informations juridiques</span><span class="sxs-lookup"><span data-stu-id="1718b-423">Legal</span></span>
<span data-ttu-id="1718b-424">Ce document est fourni « en l'état ».</span><span class="sxs-lookup"><span data-stu-id="1718b-424">This document is provided "as-is".</span></span> <span data-ttu-id="1718b-425">Les informations et les points de vue exprimés dans ce document, y compris les URL et autres références à des sites web, peuvent être modifiés sans préavis.</span><span class="sxs-lookup"><span data-stu-id="1718b-425">Information and views expressed in this document, including URL and other Internet website references, may change without notice.</span></span> <span data-ttu-id="1718b-426">Certains exemples sont fournis à titre indicatif uniquement et sont fictifs.</span><span class="sxs-lookup"><span data-stu-id="1718b-426">Some examples depicted herein are provided for illustration only and are fictitious.</span></span> <span data-ttu-id="1718b-427">Toute association ou lien est purement involontaire ou fortuit.</span><span class="sxs-lookup"><span data-stu-id="1718b-427">No real association or connection is intended or should be inferred.</span></span> <span data-ttu-id="1718b-428">Ce document ne vous accorde aucun droit légal à la propriété intellectuelle pour un produit Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1718b-428">This document does not provide you with any legal rights to any intellectual property in any Microsoft product.</span></span> <span data-ttu-id="1718b-429">Vous pouvez copier et utiliser ce document pour un usage interne, à titre de référence.</span><span class="sxs-lookup"><span data-stu-id="1718b-429">You may copy and use this document for your internal, reference purposes.</span></span> <span data-ttu-id="1718b-430">© 2014 Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1718b-430">© 2014 Microsoft.</span></span> <span data-ttu-id="1718b-431">Tous droits réservés.</span><span class="sxs-lookup"><span data-stu-id="1718b-431">All rights reserved.</span></span> 

