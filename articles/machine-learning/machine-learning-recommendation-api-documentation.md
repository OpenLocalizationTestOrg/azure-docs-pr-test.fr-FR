---
title: "aaaMachine Documentation de l’API Learning recommandations | Documents Microsoft"
description: Documentation Azure Machine Learning recommandations API sur un moteur de recommandations Bonjour Microsoft Azure Marketplace.
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: 32c3ab2f-fdd7-48cc-b501-ad55c79b87dc
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: LuisCa
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: True
ms.openlocfilehash: d1cec228bf23870c05c8ab8df2779b0c3c65b06d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-machine-learning-recommendations-api-documentation"></a><span data-ttu-id="3a021-103">Documentation sur les API Azure Machine Learning Recommendations</span><span class="sxs-lookup"><span data-stu-id="3a021-103">Azure Machine Learning Recommendations API Documentation</span></span>
> [!NOTE]
> <span data-ttu-id="3a021-104">Vous devez commencer à l’aide de hello Service cognitifs de recommandations API au lieu de cette version.</span><span class="sxs-lookup"><span data-stu-id="3a021-104">You should start using hello Recommendations API Cognitive Service instead of this version.</span></span> <span data-ttu-id="3a021-105">Hello Service cognitifs recommandations remplacera ce service et toutes les hello nouvelles fonctionnalités seront développées il.</span><span class="sxs-lookup"><span data-stu-id="3a021-105">hello Recommendations Cognitive Service will be replacing this service, and all hello new features will be developed there.</span></span> <span data-ttu-id="3a021-106">Il propose de nouvelles fonctionnalités telles que la prise en charge du traitement par lot, un meilleur Explorateur d’API, une surface d’API plus propre, une expérience d’inscription/de facturation plus cohérente, etc.</span><span class="sxs-lookup"><span data-stu-id="3a021-106">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span></span>
> <span data-ttu-id="3a021-107">En savoir plus sur [migration toohello nouveau Service cognitifs](http://aka.ms/recomigrate)</span><span class="sxs-lookup"><span data-stu-id="3a021-107">Learn more about [Migrating toohello new Cognitive Service](http://aka.ms/recomigrate)</span></span>
> 
> 

<span data-ttu-id="3a021-108">Ce document décrit les API Microsoft Azure Machine Learning Recommendations.</span><span class="sxs-lookup"><span data-stu-id="3a021-108">This document depicts Microsoft Azure Machine Learning Recommendations APIs.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="1-general-overview"></a><span data-ttu-id="3a021-109">1. Présentation générale</span><span class="sxs-lookup"><span data-stu-id="3a021-109">1. General overview</span></span>
<span data-ttu-id="3a021-110">Ce document fait référence aux API.</span><span class="sxs-lookup"><span data-stu-id="3a021-110">This document is an API reference.</span></span> <span data-ttu-id="3a021-111">Vous devez commencer par hello « Azure Machine Learning recommandation – document démarrage rapide ».</span><span class="sxs-lookup"><span data-stu-id="3a021-111">You should start with hello “Azure Machine Learning Recommendation - Quick Start” document.</span></span>

<span data-ttu-id="3a021-112">Bonjour Azure Machine Learning recommandations API peut être divisé en hello groupes logiques suivants :</span><span class="sxs-lookup"><span data-stu-id="3a021-112">hello Azure Machine Learning Recommendations API can be divided into hello following logical groups:</span></span>

* <span data-ttu-id="3a021-113"><ins>Limitations</ins> : limitations concernant les API Recommandations.</span><span class="sxs-lookup"><span data-stu-id="3a021-113"><ins>Limitations</ins> - Recommendations API limitations.</span></span>
* <span data-ttu-id="3a021-114"><ins>Informations générales</ins> : informations sur l'authentification, l’URI de service et le contrôle de version.</span><span class="sxs-lookup"><span data-stu-id="3a021-114"><ins>General Information</ins> - Information on authentication, service URI and versioning.</span></span>
* <span data-ttu-id="3a021-115"><ins>Modèle Basic</ins> -API qui vous permettent aux opérations de base hello toodo sur le modèle (par exemple, créer, mettre à jour et supprimer un modèle).</span><span class="sxs-lookup"><span data-stu-id="3a021-115"><ins>Model Basic</ins> - APIs that enable you toodo hello basic operations on model (e.g. create, update and delete a model).</span></span>
* <span data-ttu-id="3a021-116"><ins>Modèle avancé</ins> -API qui vous permettent de tooget avancée des analyses de données sur le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-116"><ins>Model Advanced</ins> - APIs that enable you tooget advanced data insights on hello model.</span></span>
* <span data-ttu-id="3a021-117"><ins>Modèle de règles d’entreprise</ins> -API qui vous permettent de toomanage des règles d’entreprise sur les résultats de recommandation modèle hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-117"><ins>Model Business Rules</ins> - APIs that enable you toomanage business rules on hello model recommendation results.</span></span>
* <span data-ttu-id="3a021-118"><ins>Catalogue</ins> -API qui vous permettent de toodo les opérations de base sur un catalogue de modèle.</span><span class="sxs-lookup"><span data-stu-id="3a021-118"><ins>Catalog</ins> - APIs that enable you toodo basic operations on a model catalog.</span></span> <span data-ttu-id="3a021-119">Un catalogue contient des informations de métadonnées sur les éléments hello hello des données d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="3a021-119">A catalog contains metadata information on hello items of hello usage data.</span></span>
* <span data-ttu-id="3a021-120"><ins>Fonctionnalité</ins> -API qui permettent aux tooget des informations sur l’élément dans le catalogue de hello et comment toouse ce recommandations de meilleure toobuild plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="3a021-120"><ins>Feature</ins> - APIs that enable tooget insights on item into hello catalog and how toouse this information toobuild better recommendations.</span></span>
* <span data-ttu-id="3a021-121"><ins>Les données d’utilisation</ins> -API qui vous permettent de toodo les opérations de base de données d’utilisation du modèle hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-121"><ins>Usage Data</ins> - APIs that enable you toodo basic operations on hello model usage data.</span></span> <span data-ttu-id="3a021-122">Données d’utilisation dans un formulaire de base hello se composent de lignes qui incluent des paires de &#60; userId &#62; &#60; itemId &#62;.</span><span class="sxs-lookup"><span data-stu-id="3a021-122">Usage data in hello basic form consists of rows that include pairs of &#60;userId&#62;,&#60;itemId&#62;.</span></span>
* <span data-ttu-id="3a021-123"><ins>Build</ins> - API qui permettent de vous tootrigger un modèle de build et effectuer des opérations de base qui sont associées toothis la build.</span><span class="sxs-lookup"><span data-stu-id="3a021-123"><ins>Build</ins> - APIs that enable you tootrigger a model build and do basic operations that are related toothis build.</span></span> <span data-ttu-id="3a021-124">Vous pouvez déclencher une build de modèle dès que vous avez des données d'utilisation utiles.</span><span class="sxs-lookup"><span data-stu-id="3a021-124">You can trigger a model build once you have valuable usage data.</span></span>
* <span data-ttu-id="3a021-125"><ins>Recommandation</ins> -API qui permettent de vous tooconsume recommandations une fois la build hello d’un modèle se termine.</span><span class="sxs-lookup"><span data-stu-id="3a021-125"><ins>Recommendation</ins> - APIs that enable you tooconsume recommendations once hello build of a model ends.</span></span>
* <span data-ttu-id="3a021-126"><ins>Données utilisateur</ins> -API qui vous permettent de toofetch plus d’informations sur les données utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-126"><ins>User Data</ins> - APIs that enable you toofetch information on hello user usage data.</span></span>
* <span data-ttu-id="3a021-127"><ins>Notifications</ins> -API qui permettent de vous tooreceive des notifications sur les problèmes liés à tooyour API operations.</span><span class="sxs-lookup"><span data-stu-id="3a021-127"><ins>Notifications</ins> - APIs that enable you tooreceive notifications on problems related tooyour API operations.</span></span> <span data-ttu-id="3a021-128">(Par exemple, vous signalez via l’Acquisition de données et la plupart des événements hello échouent le traitement des données d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="3a021-128">(For example, you are reporting usage data via Data Acquisition and most of hello events processing are failing.</span></span> <span data-ttu-id="3a021-129">une notification d'erreur est déclenchée.)</span><span class="sxs-lookup"><span data-stu-id="3a021-129">An error notification will be raised.)</span></span>

## <a name="2-limitations"></a><span data-ttu-id="3a021-130">2. Limites</span><span class="sxs-lookup"><span data-stu-id="3a021-130">2. Limitations</span></span>
* <span data-ttu-id="3a021-131">nombre maximal de Hello de modèles par abonnement est 10.</span><span class="sxs-lookup"><span data-stu-id="3a021-131">hello maximum number of models per subscription is 10.</span></span>
* <span data-ttu-id="3a021-132">Hello le nombre maximal de builds par modèle est 20.</span><span class="sxs-lookup"><span data-stu-id="3a021-132">hello maximum number of builds per model is 20.</span></span>
* <span data-ttu-id="3a021-133">nombre maximal de Hello d’éléments pouvant être un catalogue est 100 000.</span><span class="sxs-lookup"><span data-stu-id="3a021-133">hello maximum number of items that a catalog can hold is 100,000.</span></span>
* <span data-ttu-id="3a021-134">nombre maximal de Hello de points d’utilisation qui sont conservés est ~ 5 000 000.</span><span class="sxs-lookup"><span data-stu-id="3a021-134">hello maximum number of usage points that are kept is ~5,000,000.</span></span> <span data-ttu-id="3a021-135">Hello plus ancien est supprimé si nouveaux sera téléchargé ou signalé.</span><span class="sxs-lookup"><span data-stu-id="3a021-135">hello oldest will be deleted if new ones will be uploaded or reported.</span></span>
* <span data-ttu-id="3a021-136">taille maximale de Hello des données qui peuvent être envoyées dans la publication (par exemple, importation de données du catalogue, importer des données d’utilisation) est de 200 Mo.</span><span class="sxs-lookup"><span data-stu-id="3a021-136">hello maximum size of data that can be sent in POST (e.g. import catalog data, import usage data) is 200MB.</span></span>
* <span data-ttu-id="3a021-137">nombre maximal de Hello d’éléments pouvant être posées pour lors de l’obtention de recommandations est 150.</span><span class="sxs-lookup"><span data-stu-id="3a021-137">hello maximum number of items that can be asked for when getting recommendations is 150.</span></span>

## <a name="3-apis---general-information"></a><span data-ttu-id="3a021-138">3. API – Informations générales</span><span class="sxs-lookup"><span data-stu-id="3a021-138">3. APIs - general information</span></span>
### <a name="31-authentication"></a><span data-ttu-id="3a021-139">3.1.</span><span class="sxs-lookup"><span data-stu-id="3a021-139">3.1.</span></span> <span data-ttu-id="3a021-140">Authentification</span><span class="sxs-lookup"><span data-stu-id="3a021-140">Authentication</span></span>
<span data-ttu-id="3a021-141">Suivez les instructions de Microsoft Azure Marketplace hello concernant l’authentification.</span><span class="sxs-lookup"><span data-stu-id="3a021-141">Please follow hello Microsoft Azure Marketplace guidelines regarding authentication.</span></span> <span data-ttu-id="3a021-142">marketplace de Hello prend en charge une méthode d’authentification de base ou OAuth hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-142">hello marketplace supports either hello Basic or OAuth authentication method.</span></span>

### <a name="32-service-uri"></a><span data-ttu-id="3a021-143">3.2.</span><span class="sxs-lookup"><span data-stu-id="3a021-143">3.2.</span></span> <span data-ttu-id="3a021-144">URI de service</span><span class="sxs-lookup"><span data-stu-id="3a021-144">Service URI</span></span>
<span data-ttu-id="3a021-145">URI de racine de service Hello pour hello Azure Machine Learning recommandations API est [ici.](https://api.datamarket.azure.com/amla/recommendations/v3/)</span><span class="sxs-lookup"><span data-stu-id="3a021-145">hello service root URI for hello Azure Machine Learning Recommendations APIs is [here.](https://api.datamarket.azure.com/amla/recommendations/v3/)</span></span>

<span data-ttu-id="3a021-146">URI de service complet Hello est exprimée à l’aide des éléments de spécification d’OData hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-146">hello full service URI is expressed using elements of hello OData specification.</span></span>  

### <a name="33-api-version"></a><span data-ttu-id="3a021-147">3.3.</span><span class="sxs-lookup"><span data-stu-id="3a021-147">3.3.</span></span> <span data-ttu-id="3a021-148">Version de l'API</span><span class="sxs-lookup"><span data-stu-id="3a021-148">API version</span></span>
<span data-ttu-id="3a021-149">Chaque appel d’API ont à la fin de hello, un paramètre de requête appelé apiVersion qui doit être définie à too1.0.</span><span class="sxs-lookup"><span data-stu-id="3a021-149">Each API call will have, at hello end, a query parameter called apiVersion that should be set too1.0.</span></span>

### <a name="34-ids-are-case-sensitive"></a><span data-ttu-id="3a021-150">3.4.</span><span class="sxs-lookup"><span data-stu-id="3a021-150">3.4.</span></span> <span data-ttu-id="3a021-151">Respect de la casse des ID</span><span class="sxs-lookup"><span data-stu-id="3a021-151">IDs are case sensitive</span></span>
<span data-ttu-id="3a021-152">ID, retournés par une des API, de hello respectent la casse et doivent être utilisées comme telles lorsqu’il est passé en tant que paramètres dans les appels d’API suivants.</span><span class="sxs-lookup"><span data-stu-id="3a021-152">IDs, returned by any of hello APIs, are case sensitive and should be used as such when passed as parameters in subsequent API calls.</span></span> <span data-ttu-id="3a021-153">Par exemple, les ID de modèle et de catalogue respectent la casse.</span><span class="sxs-lookup"><span data-stu-id="3a021-153">For instance, model IDs and catalog IDs are case sensitive.</span></span>

## <a name="4-recommendations-quality-and-cold-items"></a><span data-ttu-id="3a021-154">4. Qualité des recommandations et éléments froids</span><span class="sxs-lookup"><span data-stu-id="3a021-154">4. Recommendations Quality and Cold Items</span></span>
### <a name="41-recommendation-quality"></a><span data-ttu-id="3a021-155">4.1.</span><span class="sxs-lookup"><span data-stu-id="3a021-155">4.1.</span></span> <span data-ttu-id="3a021-156">Qualité de la recommandation</span><span class="sxs-lookup"><span data-stu-id="3a021-156">Recommendation quality</span></span>
<span data-ttu-id="3a021-157">Création d’un modèle de recommandation est généralement suffisamment tooallow hello recommandations système tooprovide s’appliquent.</span><span class="sxs-lookup"><span data-stu-id="3a021-157">Creating a recommendation model is usually enough tooallow hello system tooprovide recommendations.</span></span> <span data-ttu-id="3a021-158">Néanmoins, de qualité de la recommandation varie selon l’utilisation de hello traitée et hello couverture du catalogue de hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-158">Nevertheless, recommendation quality varies based on hello usage processed and hello coverage of hello catalog.</span></span> <span data-ttu-id="3a021-159">Par exemple si vous avez un grand nombre d’éléments froids (éléments sans significatif d’utilisation), hello système n’aura des difficultés en fournissant une recommandation pour cet élément ou à l’aide de cet élément en tant que recommandée.</span><span class="sxs-lookup"><span data-stu-id="3a021-159">For example if you have a lot of cold items (items without significant usage), hello system will have difficulties providing a recommendation for such an item or using such an item as a recommended one.</span></span> <span data-ttu-id="3a021-160">Dans tooovercome hello à froid élément problème système de hello autorise l’utilisation de hello de métadonnées de recommandations de hello éléments tooenhance hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-160">In order tooovercome hello cold item problem, hello system allows hello use of metadata of hello items tooenhance hello recommendations.</span></span> <span data-ttu-id="3a021-161">Ces métadonnées sont les fonctionnalités tooas référencé.</span><span class="sxs-lookup"><span data-stu-id="3a021-161">This metadata is referred tooas features.</span></span> <span data-ttu-id="3a021-162">L'auteur d'un livre et l'acteur d'un film sont des exemples de caractéristiques.</span><span class="sxs-lookup"><span data-stu-id="3a021-162">Typical features are a book's author or a movie's actor.</span></span> <span data-ttu-id="3a021-163">Fonctionnalités sont fournies via le catalogue hello sous forme de hello de chaînes clé/valeur.</span><span class="sxs-lookup"><span data-stu-id="3a021-163">Features are provided via hello catalog in hello form of key/value strings.</span></span> <span data-ttu-id="3a021-164">Pour le formatage complet de hello hello du fichier de catalogue, consultez toohello [importer section catalogue](#81-import-catalog-data).</span><span class="sxs-lookup"><span data-stu-id="3a021-164">For hello full format of hello catalog file, please refer toohello [import catalog section](#81-import-catalog-data).</span></span> 

### <a name="42-rank-build"></a><span data-ttu-id="3a021-165">4.2.</span><span class="sxs-lookup"><span data-stu-id="3a021-165">4.2.</span></span> <span data-ttu-id="3a021-166">Build de classement</span><span class="sxs-lookup"><span data-stu-id="3a021-166">Rank build</span></span>
<span data-ttu-id="3a021-167">Fonctionnalités peuvent améliorer le modèle de recommandation hello, mais toodo requiert utilisez hello des fonctionnalités significatives.</span><span class="sxs-lookup"><span data-stu-id="3a021-167">Features can enhance hello recommendation model, but toodo so requires hello use of meaningful features.</span></span> <span data-ttu-id="3a021-168">Dans cette optique, une nouvelle build a été introduite : la build de classement.</span><span class="sxs-lookup"><span data-stu-id="3a021-168">For this purpose a new build was introduced - a rank build.</span></span> <span data-ttu-id="3a021-169">Cette build sera rank utilité hello de fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="3a021-169">This build will rank hello usefulness of features.</span></span> <span data-ttu-id="3a021-170">Une caractéristique est significative si elle reçoit un score d'au moins 2 de la build de classement.</span><span class="sxs-lookup"><span data-stu-id="3a021-170">A meaningful feature is a feature with a rank score of 2 and up.</span></span>
<span data-ttu-id="3a021-171">Après avoir comprenant les fonctionnalités de hello sont significatifs, déclencher une build de recommandation avec la liste de hello (ou sous-liste) des fonctionnalités significatives.</span><span class="sxs-lookup"><span data-stu-id="3a021-171">After understanding which of hello features are meaningful, trigger a recommendation build with hello list (or sublist) of meaningful features.</span></span> <span data-ttu-id="3a021-172">Il est possible de toouse que ces fonctionnalités pour améliorer les articles à chaud et à froid hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-172">It is possible toouse these feature for hello enhancement of both warm items and cold items.</span></span> <span data-ttu-id="3a021-173">Dans l’ordre toouse pour les éléments à chaud, hello `UseFeatureInModel` paramètre de build doit être configuré.</span><span class="sxs-lookup"><span data-stu-id="3a021-173">In order toouse them for warm items, hello `UseFeatureInModel` build parameter should be set up.</span></span> <span data-ttu-id="3a021-174">Dans les fonctions toouse de commande pour les éléments froids, hello `AllowColdItemPlacement` paramètre de build doit être activé.</span><span class="sxs-lookup"><span data-stu-id="3a021-174">In order toouse features for cold items, hello `AllowColdItemPlacement` build parameter should be enabled.</span></span>
<span data-ttu-id="3a021-175">Remarque : Il n’est pas possible de tooenable `AllowColdItemPlacement` sans activer `UseFeatureInModel`.</span><span class="sxs-lookup"><span data-stu-id="3a021-175">Note: It is not possible tooenable `AllowColdItemPlacement` without enabling `UseFeatureInModel`.</span></span>

### <a name="43-recommendation-reasoning"></a><span data-ttu-id="3a021-176">4.3.</span><span class="sxs-lookup"><span data-stu-id="3a021-176">4.3.</span></span> <span data-ttu-id="3a021-177">Raisonnement de la recommandation</span><span class="sxs-lookup"><span data-stu-id="3a021-177">Recommendation reasoning</span></span>
<span data-ttu-id="3a021-178">Le raisonnement de la recommandation est un autre aspect de l'utilisation des caractéristiques.</span><span class="sxs-lookup"><span data-stu-id="3a021-178">Recommendation reasoning is another aspect of feature usage.</span></span> <span data-ttu-id="3a021-179">En effet, moteur d’Azure Machine Learning recommandations de hello peut utiliser les explications de recommandation fonctionnalités tooprovide (aussi appelé)</span><span class="sxs-lookup"><span data-stu-id="3a021-179">Indeed, hello Azure Machine Learning Recommendations engine can use features tooprovide recommendation explanations (a.k.a.</span></span> <span data-ttu-id="3a021-180">Raisonnement), les meilleures toomore confiance hello recommandé élément consommateur de recommandation hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-180">reasoning), leading toomore confidence in hello recommended item from hello recommendation consumer.</span></span>
<span data-ttu-id="3a021-181">tooenable raisonnement, hello `AllowFeatureCorrelation` et `ReasoningFeatureList` paramètres doivent être le programme d’installation toorequesting préalable une build de recommandation.</span><span class="sxs-lookup"><span data-stu-id="3a021-181">tooenable reasoning, hello `AllowFeatureCorrelation` and `ReasoningFeatureList` parameters should be setup prior toorequesting a recommendation build.</span></span>

## <a name="5-model-basic"></a><span data-ttu-id="3a021-182">5. Modèle – De base</span><span class="sxs-lookup"><span data-stu-id="3a021-182">5. Model Basic</span></span>
### <a name="51-create-model"></a><span data-ttu-id="3a021-183">5.1.</span><span class="sxs-lookup"><span data-stu-id="3a021-183">5.1.</span></span> <span data-ttu-id="3a021-184">Création de modèle</span><span class="sxs-lookup"><span data-stu-id="3a021-184">Create Model</span></span>
<span data-ttu-id="3a021-185">Crée une demande de création de modèle.</span><span class="sxs-lookup"><span data-stu-id="3a021-185">Creates a “create model” request.</span></span>

| <span data-ttu-id="3a021-186">Méthode HTTP</span><span class="sxs-lookup"><span data-stu-id="3a021-186">HTTP Method</span></span> | <span data-ttu-id="3a021-187">URI</span><span class="sxs-lookup"><span data-stu-id="3a021-187">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-188">POST</span><span class="sxs-lookup"><span data-stu-id="3a021-188">POST</span></span> |`<rootURI>/CreateModel?modelName=%27<model_name>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="3a021-189">Exemple :</span><span class="sxs-lookup"><span data-stu-id="3a021-189">Example:</span></span><br>`<rootURI>/CreateModel?modelName=%27MyFirstModel%27&apiVersion=%271.0%27` |

| <span data-ttu-id="3a021-190">Nom du paramètre</span><span class="sxs-lookup"><span data-stu-id="3a021-190">Parameter Name</span></span> | <span data-ttu-id="3a021-191">Valeurs valides</span><span class="sxs-lookup"><span data-stu-id="3a021-191">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-192">modelName</span><span class="sxs-lookup"><span data-stu-id="3a021-192">modelName</span></span> |<span data-ttu-id="3a021-193">Seuls les lettres (A-Z, a-z), les chiffres (0-9), les tirets (-) et les traits de soulignement (_) sont autorisés.</span><span class="sxs-lookup"><span data-stu-id="3a021-193">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="3a021-194">Longueur maximale : 20</span><span class="sxs-lookup"><span data-stu-id="3a021-194">Max length: 20</span></span> |
| <span data-ttu-id="3a021-195">apiVersion</span><span class="sxs-lookup"><span data-stu-id="3a021-195">apiVersion</span></span> |<span data-ttu-id="3a021-196">1.0</span><span class="sxs-lookup"><span data-stu-id="3a021-196">1.0</span></span> |
|  | |
| <span data-ttu-id="3a021-197">Corps de la requête</span><span class="sxs-lookup"><span data-stu-id="3a021-197">Request Body</span></span> |<span data-ttu-id="3a021-198">AUCUN</span><span class="sxs-lookup"><span data-stu-id="3a021-198">NONE</span></span> |

<span data-ttu-id="3a021-199">**Réponse**:</span><span class="sxs-lookup"><span data-stu-id="3a021-199">**Response**:</span></span>

<span data-ttu-id="3a021-200">Code d'état HTTP : 200</span><span class="sxs-lookup"><span data-stu-id="3a021-200">HTTP Status code: 200</span></span>

* <span data-ttu-id="3a021-201">`feed/entry/content/properties/id`-Contient l’ID de modèle hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-201">`feed/entry/content/properties/id` - Contains hello model ID.</span></span>
  <span data-ttu-id="3a021-202">**Remarque**: l'ID du modèle respecte la casse.</span><span class="sxs-lookup"><span data-stu-id="3a021-202">**Note**: model ID is case sensitive.</span></span>

<span data-ttu-id="3a021-203">OData XML</span><span class="sxs-lookup"><span data-stu-id="3a021-203">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Create A New Model</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T06:35:21Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">CreateANewModelEntity2</title>
    <updated>2014-10-05T06:35:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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

### <a name="52-get-model"></a><span data-ttu-id="3a021-204">5.2.</span><span class="sxs-lookup"><span data-stu-id="3a021-204">5.2.</span></span> <span data-ttu-id="3a021-205">Obtention de modèle</span><span class="sxs-lookup"><span data-stu-id="3a021-205">Get Model</span></span>
<span data-ttu-id="3a021-206">Crée une demande d'obtention de modèle.</span><span class="sxs-lookup"><span data-stu-id="3a021-206">Creates a “get model” request.</span></span>

| <span data-ttu-id="3a021-207">Méthode HTTP</span><span class="sxs-lookup"><span data-stu-id="3a021-207">HTTP Method</span></span> | <span data-ttu-id="3a021-208">URI</span><span class="sxs-lookup"><span data-stu-id="3a021-208">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-209">GET</span><span class="sxs-lookup"><span data-stu-id="3a021-209">GET</span></span> |`<rootURI>/GetModel?id=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="3a021-210">Exemple :</span><span class="sxs-lookup"><span data-stu-id="3a021-210">Example:</span></span><br>`<rootURI>/GetModel?id=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| <span data-ttu-id="3a021-211">Nom du paramètre</span><span class="sxs-lookup"><span data-stu-id="3a021-211">Parameter Name</span></span> | <span data-ttu-id="3a021-212">Valeurs valides</span><span class="sxs-lookup"><span data-stu-id="3a021-212">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-213">id</span><span class="sxs-lookup"><span data-stu-id="3a021-213">id</span></span> |<span data-ttu-id="3a021-214">Identificateur unique du modèle hello (sensible à la casse)</span><span class="sxs-lookup"><span data-stu-id="3a021-214">Unique identifier of hello model (case sensitive)</span></span> |
| <span data-ttu-id="3a021-215">apiVersion</span><span class="sxs-lookup"><span data-stu-id="3a021-215">apiVersion</span></span> |<span data-ttu-id="3a021-216">1.0</span><span class="sxs-lookup"><span data-stu-id="3a021-216">1.0</span></span> |
|  | |
| <span data-ttu-id="3a021-217">Corps de la requête</span><span class="sxs-lookup"><span data-stu-id="3a021-217">Request Body</span></span> |<span data-ttu-id="3a021-218">AUCUN</span><span class="sxs-lookup"><span data-stu-id="3a021-218">NONE</span></span> |

<span data-ttu-id="3a021-219">**Réponse**:</span><span class="sxs-lookup"><span data-stu-id="3a021-219">**Response**:</span></span>

<span data-ttu-id="3a021-220">Code d'état HTTP : 200</span><span class="sxs-lookup"><span data-stu-id="3a021-220">HTTP Status code: 200</span></span>

<span data-ttu-id="3a021-221">Vous trouverez des données de modèle Hello sous hello suivant d’éléments :</span><span class="sxs-lookup"><span data-stu-id="3a021-221">hello model data can be found under hello following elements:</span></span>

* <span data-ttu-id="3a021-222">`feed/entry/content/properties/Id` : ID unique du modèle.</span><span class="sxs-lookup"><span data-stu-id="3a021-222">`feed/entry/content/properties/Id` - Model unique ID.</span></span>
* <span data-ttu-id="3a021-223">`feed/entry/content/properties/Name` : nom du modèle.</span><span class="sxs-lookup"><span data-stu-id="3a021-223">`feed/entry/content/properties/Name` - Model name.</span></span>
* <span data-ttu-id="3a021-224">`feed/entry/content/properties/Date` : date de création du modèle.</span><span class="sxs-lookup"><span data-stu-id="3a021-224">`feed/entry/content/properties/Date` - Model creation date.</span></span>
* <span data-ttu-id="3a021-225">`feed/entry/content/properties/Status` : état du modèle.</span><span class="sxs-lookup"><span data-stu-id="3a021-225">`feed/entry/content/properties/Status` - Model status.</span></span> <span data-ttu-id="3a021-226">Une des manières de hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="3a021-226">One of hello following:</span></span>
  * <span data-ttu-id="3a021-227">Created : le modèle est créé, mais il ne contient pas de données de catalogue et d'utilisation.</span><span class="sxs-lookup"><span data-stu-id="3a021-227">Created - Model is created and does not contain Catalog and Usage.</span></span>
  * <span data-ttu-id="3a021-228">ReadyForBuild : le modèle est créé et contient des données de catalogue et d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="3a021-228">ReadyForBuild - Model is created and contains Catalog and Usage.</span></span>
* <span data-ttu-id="3a021-229">`feed/entry/content/properties/HasActiveBuild`-Indique si le modèle de hello a été généré correctement.</span><span class="sxs-lookup"><span data-stu-id="3a021-229">`feed/entry/content/properties/HasActiveBuild` - Indicates if hello model was built successfully.</span></span>
* <span data-ttu-id="3a021-230">`feed/entry/content/properties/BuildId` : ID de build active du modèle.</span><span class="sxs-lookup"><span data-stu-id="3a021-230">`feed/entry/content/properties/BuildId` - Model active build ID.</span></span>
* <span data-ttu-id="3a021-231">`feed/entry/content/properties/Mpr` : classement centile moyen du modèle (MPR, Mean Percentile Ranking ; pour plus d’informations, voir ModelInsight).</span><span class="sxs-lookup"><span data-stu-id="3a021-231">`feed/entry/content/properties/Mpr` - Model mean percentile ranking (MPR - see ModelInsight for more information).</span></span>
* <span data-ttu-id="3a021-232">`feed/entry/content/properties/UserName` : nom d’utilisateur interne du modèle.</span><span class="sxs-lookup"><span data-stu-id="3a021-232">`feed/entry/content/properties/UserName` - Model internal user name.</span></span>

<span data-ttu-id="3a021-233">OData XML</span><span class="sxs-lookup"><span data-stu-id="3a021-233">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get A List Of All Models</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-28T14:35:51Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetAListOfAllModelsEntity</title>
    <updated>2014-10-28T14:35:51Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">68b232f2-1037-45f7-8f49-af822695ee63</d:Id>
        <d:Name m:type="Edm.String">vah-11111</d:Name>
        <d:Date m:type="Edm.String">10/28/2014 2:16:07 PM</d:Date>
        <d:Status m:type="Edm.String">ReadyForBuild</d:Status>
        <d:HasActiveBuild m:type="Edm.String">false</d:HasActiveBuild>
        <d:BuildId m:type="Edm.String">-1</d:BuildId>
        <d:Mpr m:type="Edm.String">0</d:Mpr>
        <d:UsageFileNames m:type="Edm.String">ImplicitMatrix10_Guid_small.txt, ImplicitMatrix11_Guid_small.txt</d:UsageFileNames>
        <d:CatalogId m:type="Edm.String">626babdb-cab6-43a6-82ef-4fb86345700c</d:CatalogId>
        <d:UserName m:type="Edm.String">89dc4722-03ba-4f90-8821-b1db388408b5@dm.com</d:UserName>
        <d:Description m:type="Edm.String">short description</d:Description>
        <d:CatalogFileName m:type="Edm.String">catalog10_small.txt</d:CatalogFileName>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="53----get-all-models"></a><span data-ttu-id="3a021-234">5.3.</span><span class="sxs-lookup"><span data-stu-id="3a021-234">5.3.</span></span>    <span data-ttu-id="3a021-235">Obtention de tous les modèles</span><span class="sxs-lookup"><span data-stu-id="3a021-235">Get All Models</span></span>
<span data-ttu-id="3a021-236">Récupère tous les modèles de l’utilisateur actuel hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-236">Retrieves all models of hello current user.</span></span>

| <span data-ttu-id="3a021-237">Méthode HTTP</span><span class="sxs-lookup"><span data-stu-id="3a021-237">HTTP Method</span></span> | <span data-ttu-id="3a021-238">URI</span><span class="sxs-lookup"><span data-stu-id="3a021-238">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-239">GET</span><span class="sxs-lookup"><span data-stu-id="3a021-239">GET</span></span> |`<rootURI>/GetAllModels?apiVersion=%271.0%27`<br><span data-ttu-id="3a021-240">Exemple :</span><span class="sxs-lookup"><span data-stu-id="3a021-240">Example:</span></span><br>`<rootURI>/GetAllModels?apiVersion=%271.0%27` |

| <span data-ttu-id="3a021-241">Nom du paramètre</span><span class="sxs-lookup"><span data-stu-id="3a021-241">Parameter Name</span></span> | <span data-ttu-id="3a021-242">Valeurs valides</span><span class="sxs-lookup"><span data-stu-id="3a021-242">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-243">apiVersion</span><span class="sxs-lookup"><span data-stu-id="3a021-243">apiVersion</span></span> |<span data-ttu-id="3a021-244">1.0</span><span class="sxs-lookup"><span data-stu-id="3a021-244">1.0</span></span> |
|  | |
| <span data-ttu-id="3a021-245">Corps de la requête</span><span class="sxs-lookup"><span data-stu-id="3a021-245">Request Body</span></span> |<span data-ttu-id="3a021-246">AUCUN</span><span class="sxs-lookup"><span data-stu-id="3a021-246">NONE</span></span> |

<span data-ttu-id="3a021-247">**Réponse**:</span><span class="sxs-lookup"><span data-stu-id="3a021-247">**Response**:</span></span>

<span data-ttu-id="3a021-248">Code d'état HTTP : 200</span><span class="sxs-lookup"><span data-stu-id="3a021-248">HTTP Status code: 200</span></span>

* <span data-ttu-id="3a021-249">`feed/entry/content/properties/Id` : ID unique du modèle.</span><span class="sxs-lookup"><span data-stu-id="3a021-249">`feed/entry/content/properties/Id` - Model unique ID.</span></span>
* <span data-ttu-id="3a021-250">`feed/entry/content/properties/Name` : nom du modèle.</span><span class="sxs-lookup"><span data-stu-id="3a021-250">`feed/entry/content/properties/Name` - Model name.</span></span>
* <span data-ttu-id="3a021-251">`feed/entry/content/properties/Date` : date de création du modèle.</span><span class="sxs-lookup"><span data-stu-id="3a021-251">`feed/entry/content/properties/Date` - Model creation date.</span></span>
* <span data-ttu-id="3a021-252">`feed/entry/content/properties/Status` : état du modèle.</span><span class="sxs-lookup"><span data-stu-id="3a021-252">`feed/entry/content/properties/Status` - Model status.</span></span> <span data-ttu-id="3a021-253">Une des manières de hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="3a021-253">One of hello following:</span></span>
  * <span data-ttu-id="3a021-254">Created : le modèle est créé, mais il ne contient pas de données de catalogue et d'utilisation.</span><span class="sxs-lookup"><span data-stu-id="3a021-254">Created - Model is created and does not contain Catalog and Usage.</span></span>
  * <span data-ttu-id="3a021-255">ReadyForBuild : le modèle est créé et contient des données de catalogue et d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="3a021-255">ReadyForBuild - Model is created and contains Catalog and Usage.</span></span>
* <span data-ttu-id="3a021-256">`feed/entry/content/properties/HasActiveBuild`-Indique si le modèle de hello a été généré correctement.</span><span class="sxs-lookup"><span data-stu-id="3a021-256">`feed/entry/content/properties/HasActiveBuild` - Indicates if hello model was built successfully.</span></span>
* <span data-ttu-id="3a021-257">`feed/entry/content/properties/BuildId` : ID de build active du modèle.</span><span class="sxs-lookup"><span data-stu-id="3a021-257">`feed/entry/content/properties/BuildId` - Model active build ID.</span></span>
* <span data-ttu-id="3a021-258">`feed/entry/content/properties/Mpr` : MPR du modèle (pour plus d’informations, voir ModelInsight).</span><span class="sxs-lookup"><span data-stu-id="3a021-258">`feed/entry/content/properties/Mpr` - Model MPR (see ModelInsight for more information).</span></span>
* <span data-ttu-id="3a021-259">`feed/entry/content/properties/UserName` : nom d’utilisateur interne du modèle.</span><span class="sxs-lookup"><span data-stu-id="3a021-259">`feed/entry/content/properties/UserName` - Model internal user name.</span></span>
* <span data-ttu-id="3a021-260">`feed/entry/content/properties/UsageFileNames` : liste de fichiers d’utilisation du modèle séparés par des virgules.</span><span class="sxs-lookup"><span data-stu-id="3a021-260">`feed/entry/content/properties/UsageFileNames` - List of model usage files separated by comma.</span></span>
* <span data-ttu-id="3a021-261">`feed/entry/content/properties/CatalogId` : ID de catalogue du modèle.</span><span class="sxs-lookup"><span data-stu-id="3a021-261">`feed/entry/content/properties/CatalogId` - Model catalog ID.</span></span>
* <span data-ttu-id="3a021-262">`feed/entry/content/properties/Description` : description du modèle.</span><span class="sxs-lookup"><span data-stu-id="3a021-262">`feed/entry/content/properties/Description` - Model description.</span></span>
* <span data-ttu-id="3a021-263">`feed/entry/content/properties/CatalogFileName` : nom de fichier de catalogue du modèle.</span><span class="sxs-lookup"><span data-stu-id="3a021-263">`feed/entry/content/properties/CatalogFileName` - Model catalog file name.</span></span>

<span data-ttu-id="3a021-264">OData XML</span><span class="sxs-lookup"><span data-stu-id="3a021-264">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get A List Of All Models</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-28T14:35:51Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetAListOfAllModelsEntity</title>
    <updated>2014-10-28T14:35:51Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Id m:type="Edm.String">68b232f2-1037-45f7-8f49-af822695ee63</d:Id>
                    <d:Name m:type="Edm.String">vah-11111</d:Name>
                    <d:Date m:type="Edm.String">10/28/2014 2:16:07 PM</d:Date>
                    <d:Status m:type="Edm.String">ReadyForBuild</d:Status>
                    <d:HasActiveBuild m:type="Edm.String">false</d:HasActiveBuild>
                    <d:BuildId m:type="Edm.String">-1</d:BuildId>
                    <d:Mpr m:type="Edm.String">0</d:Mpr>
                    <d:UsageFileNames m:type="Edm.String">ImplicitMatrix10_Guid_small.txt, ImplicitMatrix11_Guid_small.txt</d:UsageFileNames>
                    <d:CatalogId m:type="Edm.String">626babdb-cab6-43a6-82ef-4fb86345700c</d:CatalogId>
                    <d:UserName m:type="Edm.String">89dc4722-03ba-4f90-8821-b1db388408b5@dm.com</d:UserName>
                    <d:Description m:type="Edm.String">short description</d:Description>
                    <d:CatalogFileName m:type="Edm.String">catalog10_small.txt</d:CatalogFileName>
                </m:properties>
            </content>
        </entry>
    </feed>

### <a name="54----update-model"></a><span data-ttu-id="3a021-265">5.4.</span><span class="sxs-lookup"><span data-stu-id="3a021-265">5.4.</span></span>    <span data-ttu-id="3a021-266">Mise à jour du modèle</span><span class="sxs-lookup"><span data-stu-id="3a021-266">Update Model</span></span>
<span data-ttu-id="3a021-267">Vous pouvez mettre à jour la description du modèle hello ou hello ID de génération active.</span><span class="sxs-lookup"><span data-stu-id="3a021-267">You can update hello model description or hello active build ID.</span></span><br><span data-ttu-id="3a021-268">
<ins>Identifiant de build active</ins> : pour chaque modèle, chaque build possède un identifiant de build.</span><span class="sxs-lookup"><span data-stu-id="3a021-268">
<ins>Active build ID</ins> - Every build for every model has a build ID.</span></span> <span data-ttu-id="3a021-269">ID de build active Hello est hello première génération réussie de chaque nouveau modèle.</span><span class="sxs-lookup"><span data-stu-id="3a021-269">hello active build ID is hello first successful build of every new model.</span></span> <span data-ttu-id="3a021-270">Une fois que vous avez un ID de build active et vous faire d’autres builds pour hello même modèle, vous devez tooexplicitly définir comme hello par défaut ID de build si vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="3a021-270">Once you have an active build ID and you do additional builds for hello same model, you need tooexplicitly set it as hello default build ID if you want to.</span></span> <span data-ttu-id="3a021-271">Lorsque vous consommez des recommandations, si vous ne spécifiez pas d’ID de build hello toouse, un est utilisé automatiquement de la valeur par défaut hello souhaitées.</span><span class="sxs-lookup"><span data-stu-id="3a021-271">When you consume recommendations, if you do not specify hello build ID that you want toouse, hello default one will be used automatically.</span></span><br>
<span data-ttu-id="3a021-272">Ce mécanisme vous permet de - une fois que vous disposez d’un modèle de recommandation en production - toobuild de nouveaux modèles et les testez avant de les promouvoir tooproduction.</span><span class="sxs-lookup"><span data-stu-id="3a021-272">This mechanism enables you - once you have a recommendation model in production - toobuild new models and test them before you promote them tooproduction.</span></span>

| <span data-ttu-id="3a021-273">Méthode HTTP</span><span class="sxs-lookup"><span data-stu-id="3a021-273">HTTP Method</span></span> | <span data-ttu-id="3a021-274">URI</span><span class="sxs-lookup"><span data-stu-id="3a021-274">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-275">PUT</span><span class="sxs-lookup"><span data-stu-id="3a021-275">PUT</span></span> |`<rootURI>/UpdateModel?id=%27<modelId>%27&apiVersion=%271.0%27`<br><span data-ttu-id="3a021-276">Exemple :</span><span class="sxs-lookup"><span data-stu-id="3a021-276">Example:</span></span><br>`<rootURI>/UpdateModel?id=%279559872f-7a53-4076-a3c7-19d9385c1265%27&apiVersion=%271.0%27` |

| <span data-ttu-id="3a021-277">Nom du paramètre</span><span class="sxs-lookup"><span data-stu-id="3a021-277">Parameter Name</span></span> | <span data-ttu-id="3a021-278">Valeurs valides</span><span class="sxs-lookup"><span data-stu-id="3a021-278">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-279">id</span><span class="sxs-lookup"><span data-stu-id="3a021-279">id</span></span> |<span data-ttu-id="3a021-280">Identificateur unique du modèle hello (sensible à la casse)</span><span class="sxs-lookup"><span data-stu-id="3a021-280">Unique identifier of hello model (case sensitive)</span></span> |
| <span data-ttu-id="3a021-281">apiVersion</span><span class="sxs-lookup"><span data-stu-id="3a021-281">apiVersion</span></span> |<span data-ttu-id="3a021-282">1.0</span><span class="sxs-lookup"><span data-stu-id="3a021-282">1.0</span></span> |
|  | |
| <span data-ttu-id="3a021-283">Corps de la requête</span><span class="sxs-lookup"><span data-stu-id="3a021-283">Request Body</span></span> |`<ModelUpdateParams xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">`<br>`<Description>New Description</Description>`<br>`<ActiveBuildId>-1</ActiveBuildId>`<br>` </ModelUpdateParams>`<br><br><span data-ttu-id="3a021-284">Notez que la Description des balises XML de hello et ActiveBuildId sont facultatifs.</span><span class="sxs-lookup"><span data-stu-id="3a021-284">Note that hello XML tags Description and ActiveBuildId are optional.</span></span> <span data-ttu-id="3a021-285">Si vous ne souhaitez pas tooset Description ou ActiveBuildId, supprimez la balise dans son ensemble hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-285">If you do not want tooset Description or ActiveBuildId, remove hello entire tag.</span></span> |

<span data-ttu-id="3a021-286">**Réponse**:</span><span class="sxs-lookup"><span data-stu-id="3a021-286">**Response**:</span></span>

<span data-ttu-id="3a021-287">Code d'état HTTP : 200</span><span class="sxs-lookup"><span data-stu-id="3a021-287">HTTP Status code: 200</span></span>

### <a name="55----delete-model"></a><span data-ttu-id="3a021-288">5.5.</span><span class="sxs-lookup"><span data-stu-id="3a021-288">5.5.</span></span>    <span data-ttu-id="3a021-289">Suppression de modèle</span><span class="sxs-lookup"><span data-stu-id="3a021-289">Delete Model</span></span>
<span data-ttu-id="3a021-290">Supprime un modèle existant par ID.</span><span class="sxs-lookup"><span data-stu-id="3a021-290">Deletes an existing model by ID.</span></span>

| <span data-ttu-id="3a021-291">Méthode HTTP</span><span class="sxs-lookup"><span data-stu-id="3a021-291">HTTP Method</span></span> | <span data-ttu-id="3a021-292">URI</span><span class="sxs-lookup"><span data-stu-id="3a021-292">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-293">SUPPRIMER</span><span class="sxs-lookup"><span data-stu-id="3a021-293">DELETE</span></span> |`<rootURI>/DeleteModel?id=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="3a021-294">Exemple :</span><span class="sxs-lookup"><span data-stu-id="3a021-294">Example:</span></span><br>`<rootURI>/DeleteModel?id=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| <span data-ttu-id="3a021-295">Nom du paramètre</span><span class="sxs-lookup"><span data-stu-id="3a021-295">Parameter Name</span></span> | <span data-ttu-id="3a021-296">Valeurs valides</span><span class="sxs-lookup"><span data-stu-id="3a021-296">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-297">id</span><span class="sxs-lookup"><span data-stu-id="3a021-297">id</span></span> |<span data-ttu-id="3a021-298">Identificateur unique du modèle hello (sensible à la casse)</span><span class="sxs-lookup"><span data-stu-id="3a021-298">Unique identifier of hello model (case sensitive)</span></span> |
| <span data-ttu-id="3a021-299">apiVersion</span><span class="sxs-lookup"><span data-stu-id="3a021-299">apiVersion</span></span> |<span data-ttu-id="3a021-300">1.0</span><span class="sxs-lookup"><span data-stu-id="3a021-300">1.0</span></span> |
|  | |
| <span data-ttu-id="3a021-301">Corps de la requête</span><span class="sxs-lookup"><span data-stu-id="3a021-301">Request Body</span></span> |<span data-ttu-id="3a021-302">AUCUN</span><span class="sxs-lookup"><span data-stu-id="3a021-302">NONE</span></span> |

<span data-ttu-id="3a021-303">**Réponse**:</span><span class="sxs-lookup"><span data-stu-id="3a021-303">**Response**:</span></span>

<span data-ttu-id="3a021-304">Code d'état HTTP : 200</span><span class="sxs-lookup"><span data-stu-id="3a021-304">HTTP Status code: 200</span></span>

<span data-ttu-id="3a021-305">OData XML</span><span class="sxs-lookup"><span data-stu-id="3a021-305">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Delete Model by Id</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-28T10:39:33Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">DeleteModelByIdEntity</title>
    <updated>2014-10-28T10:39:33Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:string m:type="Edm.String"></d:string>
      </m:properties>
    </content>
      </entry>
    </feed>

## <a name="6-model-advanced"></a><span data-ttu-id="3a021-306">6. Modèle – Avancé</span><span class="sxs-lookup"><span data-stu-id="3a021-306">6. Model Advanced</span></span>
### <a name="61----model-data-insight"></a><span data-ttu-id="3a021-307">6.1.</span><span class="sxs-lookup"><span data-stu-id="3a021-307">6.1.</span></span>    <span data-ttu-id="3a021-308">Analyse des données de modèle</span><span class="sxs-lookup"><span data-stu-id="3a021-308">Model Data Insight</span></span>
<span data-ttu-id="3a021-309">Renvoie des données statistiques sur les données d’utilisation de hello ce modèle a été généré à l’aide.</span><span class="sxs-lookup"><span data-stu-id="3a021-309">Returns statistical data on hello usage data that this model was built with.</span></span>

<span data-ttu-id="3a021-310">Disponible uniquement pour la build de recommandation.</span><span class="sxs-lookup"><span data-stu-id="3a021-310">Available only for Recommendation build.</span></span>

| <span data-ttu-id="3a021-311">Méthode HTTP</span><span class="sxs-lookup"><span data-stu-id="3a021-311">HTTP Method</span></span> | <span data-ttu-id="3a021-312">URI</span><span class="sxs-lookup"><span data-stu-id="3a021-312">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-313">GET</span><span class="sxs-lookup"><span data-stu-id="3a021-313">GET</span></span> |`<rootURI>/GetDataInsight?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="3a021-314">Exemple :</span><span class="sxs-lookup"><span data-stu-id="3a021-314">Example:</span></span><br>`<rootURI>/GetDataInsight?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| <span data-ttu-id="3a021-315">Nom du paramètre</span><span class="sxs-lookup"><span data-stu-id="3a021-315">Parameter Name</span></span> | <span data-ttu-id="3a021-316">Valeurs valides</span><span class="sxs-lookup"><span data-stu-id="3a021-316">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-317">modelId</span><span class="sxs-lookup"><span data-stu-id="3a021-317">modelId</span></span> |<span data-ttu-id="3a021-318">Identificateur unique du modèle de hello</span><span class="sxs-lookup"><span data-stu-id="3a021-318">Unique identifier of hello model</span></span> |
| <span data-ttu-id="3a021-319">apiVersion</span><span class="sxs-lookup"><span data-stu-id="3a021-319">apiVersion</span></span> |<span data-ttu-id="3a021-320">1.0</span><span class="sxs-lookup"><span data-stu-id="3a021-320">1.0</span></span> |
|  | |
| <span data-ttu-id="3a021-321">Corps de la requête</span><span class="sxs-lookup"><span data-stu-id="3a021-321">Request Body</span></span> |<span data-ttu-id="3a021-322">AUCUN</span><span class="sxs-lookup"><span data-stu-id="3a021-322">NONE</span></span> |

<span data-ttu-id="3a021-323">**Réponse**:</span><span class="sxs-lookup"><span data-stu-id="3a021-323">**Response**:</span></span>

<span data-ttu-id="3a021-324">Code d'état HTTP : 200</span><span class="sxs-lookup"><span data-stu-id="3a021-324">HTTP Status code: 200</span></span>

<span data-ttu-id="3a021-325">les données de salutation sont retournées comme une collection de propriétés.</span><span class="sxs-lookup"><span data-stu-id="3a021-325">hello data is returned as a collection of properties.</span></span>

* <span data-ttu-id="3a021-326">`feed/entry/id/content/properties/key`-Contient le nom de la propriété hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-326">`feed/entry/id/content/properties/key` - Holds hello property name.</span></span>
* <span data-ttu-id="3a021-327">`feed/entry/id/content/properties/value`-Contient la valeur de la propriété hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-327">`feed/entry/id/content/properties/value` - Holds hello property value.</span></span>

<span data-ttu-id="3a021-328">tableau Hello ci-dessous représente la valeur hello représentant chaque clé.</span><span class="sxs-lookup"><span data-stu-id="3a021-328">hello table below depicts hello value that each key represents.</span></span>

| <span data-ttu-id="3a021-329">Clé</span><span class="sxs-lookup"><span data-stu-id="3a021-329">Key</span></span> | <span data-ttu-id="3a021-330">Description</span><span class="sxs-lookup"><span data-stu-id="3a021-330">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-331">AvgItemLength</span><span class="sxs-lookup"><span data-stu-id="3a021-331">AvgItemLength</span></span> |<span data-ttu-id="3a021-332">Nombre moyen d'utilisateurs distincts par élément.</span><span class="sxs-lookup"><span data-stu-id="3a021-332">Average number of distinct users per item.</span></span> |
| <span data-ttu-id="3a021-333">AvgUserLength</span><span class="sxs-lookup"><span data-stu-id="3a021-333">AvgUserLength</span></span> |<span data-ttu-id="3a021-334">Nombre moyen d'éléments distincts par utilisateur.</span><span class="sxs-lookup"><span data-stu-id="3a021-334">Average number of distinct items per user.</span></span> |
| <span data-ttu-id="3a021-335">DensificationNumberOfItems</span><span class="sxs-lookup"><span data-stu-id="3a021-335">DensificationNumberOfItems</span></span> |<span data-ttu-id="3a021-336">Nombre d'éléments après nettoyage des éléments ne pouvant pas être modélisés.</span><span class="sxs-lookup"><span data-stu-id="3a021-336">Number of items after pruning items that cannot be modelled.</span></span> |
| <span data-ttu-id="3a021-337">DensificationNumberOfUsers</span><span class="sxs-lookup"><span data-stu-id="3a021-337">DensificationNumberOfUsers</span></span> |<span data-ttu-id="3a021-338">Nombre de points d'utilisation après nettoyage des utilisateurs et des éléments ne pouvant pas être modélisés.</span><span class="sxs-lookup"><span data-stu-id="3a021-338">Number of usage points after pruning users and items that can't be modelled.</span></span> |
| <span data-ttu-id="3a021-339">DensificationNumberOfRecords</span><span class="sxs-lookup"><span data-stu-id="3a021-339">DensificationNumberOfRecords</span></span> |<span data-ttu-id="3a021-340">Nombre de points d'utilisation après nettoyage des utilisateurs et des éléments ne pouvant pas être modélisés.</span><span class="sxs-lookup"><span data-stu-id="3a021-340">Number of usage points after pruning users and items that can't be modelled.</span></span> |
| <span data-ttu-id="3a021-341">MaxItemLength</span><span class="sxs-lookup"><span data-stu-id="3a021-341">MaxItemLength</span></span> |<span data-ttu-id="3a021-342">Nombre d’utilisateurs distincts pour les éléments les plus populaires hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-342">Number of distinct users for hello most popular item.</span></span> |
| <span data-ttu-id="3a021-343">MaxUserLength</span><span class="sxs-lookup"><span data-stu-id="3a021-343">MaxUserLength</span></span> |<span data-ttu-id="3a021-344">Nombre maximal d'éléments distincts pour un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="3a021-344">Maximal number of distinct items for a user.</span></span> |
| <span data-ttu-id="3a021-345">MinItemLength</span><span class="sxs-lookup"><span data-stu-id="3a021-345">MinItemLength</span></span> |<span data-ttu-id="3a021-346">Nombre maximal d'utilisateurs distincts pour un élément.</span><span class="sxs-lookup"><span data-stu-id="3a021-346">Maximal number of distinct users for an item.</span></span> |
| <span data-ttu-id="3a021-347">MinUserLength</span><span class="sxs-lookup"><span data-stu-id="3a021-347">MinUserLength</span></span> |<span data-ttu-id="3a021-348">Nombre minimal d'éléments distincts pour un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="3a021-348">Minimal number of distinct items for a user.</span></span> |
| <span data-ttu-id="3a021-349">RawNumberOfItems</span><span class="sxs-lookup"><span data-stu-id="3a021-349">RawNumberOfItems</span></span> |<span data-ttu-id="3a021-350">Nombre d’éléments dans les fichiers d’utilisation de hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-350">Number of items in hello usage files.</span></span> |
| <span data-ttu-id="3a021-351">RawNumberOfUsers</span><span class="sxs-lookup"><span data-stu-id="3a021-351">RawNumberOfUsers</span></span> |<span data-ttu-id="3a021-352">Nombre de points d'utilisation avant nettoyage.</span><span class="sxs-lookup"><span data-stu-id="3a021-352">Number of usage points before any pruning.</span></span> |
| <span data-ttu-id="3a021-353">RawNumberOfRecords</span><span class="sxs-lookup"><span data-stu-id="3a021-353">RawNumberOfRecords</span></span> |<span data-ttu-id="3a021-354">Nombre de points d'utilisation avant nettoyage.</span><span class="sxs-lookup"><span data-stu-id="3a021-354">Number of usage points before any pruning.</span></span> |
| <span data-ttu-id="3a021-355">SamplingNumberOfItems</span><span class="sxs-lookup"><span data-stu-id="3a021-355">SamplingNumberOfItems</span></span> |<span data-ttu-id="3a021-356">N/A</span><span class="sxs-lookup"><span data-stu-id="3a021-356">N/A</span></span> |
| <span data-ttu-id="3a021-357">SamplingNumberOfRecords</span><span class="sxs-lookup"><span data-stu-id="3a021-357">SamplingNumberOfRecords</span></span> |<span data-ttu-id="3a021-358">N/A</span><span class="sxs-lookup"><span data-stu-id="3a021-358">N/A</span></span> |
| <span data-ttu-id="3a021-359">SamplingNumberOfUsers</span><span class="sxs-lookup"><span data-stu-id="3a021-359">SamplingNumberOfUsers</span></span> |<span data-ttu-id="3a021-360">N/A</span><span class="sxs-lookup"><span data-stu-id="3a021-360">N/A</span></span> |

<span data-ttu-id="3a021-361">OData XML</span><span class="sxs-lookup"><span data-stu-id="3a021-361">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get data insight statistics</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'" />
    <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">AvgItemLength</d:Key>
        <d:Value m:type="Edm.String">18.936</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">AvgUserLength</d:Key>
        <d:Value m:type="Edm.String">51.879</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">DensificationNumberOfItems</d:Key>
        <d:Value m:type="Edm.String">2,000</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">DensificationNumberOfRecords</d:Key>
        <d:Value m:type="Edm.String">37,872</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
    <content type="application/xml">
        <m:properties>
            <d:Key m:type="Edm.String">DensificationNumberOfUsers</d:Key>
            <d:Value m:type="Edm.String">730</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MaxItemLength</d:Key>
                <d:Value m:type="Edm.String">4,704</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MaxUserLength</d:Key>
                <d:Value m:type="Edm.String">190</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MinItemLength</d:Key>
                <d:Value m:type="Edm.String">8</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MinUserLength</d:Key>
                <d:Value m:type="Edm.String">20</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">RawNumberOfItems</d:Key>
                <d:Value m:type="Edm.String">2,000</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">RawNumberOfRecords</d:Key>
                <d:Value m:type="Edm.String">72,022</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">RawNumberOfUsers</d:Key>
                <d:Value m:type="Edm.String">9,044</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">SampelingNumberOfItems</d:Key>
                <d:Value m:type="Edm.String">2,000</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=13&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=13&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">SampelingNumberOfRecords</d:Key>
                <d:Value m:type="Edm.String">72,022</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=14&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=14&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">SampelingNumberOfUsers</d:Key>
                <d:Value m:type="Edm.String">9,044</d:Value>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="62----model-insight"></a><span data-ttu-id="3a021-362">6.2.</span><span class="sxs-lookup"><span data-stu-id="3a021-362">6.2.</span></span>    <span data-ttu-id="3a021-363">Informations de modèle</span><span class="sxs-lookup"><span data-stu-id="3a021-363">Model Insight</span></span>
<span data-ttu-id="3a021-364">Retourne le modèle insight sur build active de hello ou (si) sur une build spécifique.</span><span class="sxs-lookup"><span data-stu-id="3a021-364">Returns model insight on hello active build or (if given) on a specific build.</span></span>

<span data-ttu-id="3a021-365">Disponible uniquement pour la build de recommandation.</span><span class="sxs-lookup"><span data-stu-id="3a021-365">Available only for Recommendation build.</span></span>

| <span data-ttu-id="3a021-366">Méthode HTTP</span><span class="sxs-lookup"><span data-stu-id="3a021-366">HTTP Method</span></span> | <span data-ttu-id="3a021-367">URI</span><span class="sxs-lookup"><span data-stu-id="3a021-367">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-368">GET</span><span class="sxs-lookup"><span data-stu-id="3a021-368">GET</span></span> |<span data-ttu-id="3a021-369">Avec une ID de build active :</span><span class="sxs-lookup"><span data-stu-id="3a021-369">With active build ID:</span></span><br>`<rootURI>/GetModelInsight?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="3a021-370">Exemple :</span><span class="sxs-lookup"><span data-stu-id="3a021-370">Example:</span></span><br>`<rootURI>/GetModelInsight?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="3a021-371">Avec l’ID de build spécifique :</span><span class="sxs-lookup"><span data-stu-id="3a021-371">With specific build ID:</span></span><br>`<rootURI>/GetModelInsight?modelId=%27<model_id>%27&buildId=%27<build_id>%27&apiVersion=%271.0%27` |

| <span data-ttu-id="3a021-372">Nom du paramètre</span><span class="sxs-lookup"><span data-stu-id="3a021-372">Parameter Name</span></span> | <span data-ttu-id="3a021-373">Valeurs valides</span><span class="sxs-lookup"><span data-stu-id="3a021-373">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-374">modelId</span><span class="sxs-lookup"><span data-stu-id="3a021-374">modelId</span></span> |<span data-ttu-id="3a021-375">Identificateur unique du modèle de hello</span><span class="sxs-lookup"><span data-stu-id="3a021-375">Unique identifier of hello model</span></span> |
| <span data-ttu-id="3a021-376">buildId</span><span class="sxs-lookup"><span data-stu-id="3a021-376">buildId</span></span> |<span data-ttu-id="3a021-377">Facultatif ; numéro qui identifie une build réussie.</span><span class="sxs-lookup"><span data-stu-id="3a021-377">Optional - number that identifies a successful build.</span></span> |
| <span data-ttu-id="3a021-378">apiVersion</span><span class="sxs-lookup"><span data-stu-id="3a021-378">apiVersion</span></span> |<span data-ttu-id="3a021-379">1.0</span><span class="sxs-lookup"><span data-stu-id="3a021-379">1.0</span></span> |
|  | |
| <span data-ttu-id="3a021-380">Corps de la requête</span><span class="sxs-lookup"><span data-stu-id="3a021-380">Request Body</span></span> |<span data-ttu-id="3a021-381">AUCUN</span><span class="sxs-lookup"><span data-stu-id="3a021-381">NONE</span></span> |

<span data-ttu-id="3a021-382">**Réponse**:</span><span class="sxs-lookup"><span data-stu-id="3a021-382">**Response**:</span></span>

<span data-ttu-id="3a021-383">Code d'état HTTP : 200</span><span class="sxs-lookup"><span data-stu-id="3a021-383">HTTP Status code: 200</span></span>

<span data-ttu-id="3a021-384">les données de salutation sont retournées comme une collection de propriétés.</span><span class="sxs-lookup"><span data-stu-id="3a021-384">hello data is returned as a collection of properties.</span></span>

* `feed/entry/id/content/properties/key`
* `feed/entry/id/content/properties/value`

<span data-ttu-id="3a021-385">tableau Hello ci-dessous représente la valeur hello représentant chaque clé.</span><span class="sxs-lookup"><span data-stu-id="3a021-385">hello table below depicts hello value that each key represents.</span></span>

| <span data-ttu-id="3a021-386">Clé</span><span class="sxs-lookup"><span data-stu-id="3a021-386">Key</span></span> | <span data-ttu-id="3a021-387">Description</span><span class="sxs-lookup"><span data-stu-id="3a021-387">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-388">CatalogCoverage</span><span class="sxs-lookup"><span data-stu-id="3a021-388">CatalogCoverage</span></span> |<span data-ttu-id="3a021-389">Partie du catalogue de hello peut être modelée avec les modèles d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="3a021-389">What part of hello catalog can be modelled with usage patterns.</span></span> <span data-ttu-id="3a021-390">Hello des autres hello éléments devez fonctionnalités basées sur le contenu.</span><span class="sxs-lookup"><span data-stu-id="3a021-390">hello rest of hello items will need content-based features.</span></span> |
| <span data-ttu-id="3a021-391">Mpr</span><span class="sxs-lookup"><span data-stu-id="3a021-391">Mpr</span></span> |<span data-ttu-id="3a021-392">Classement de centile moyenne du modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-392">Mean percentile ranking of hello model.</span></span> <span data-ttu-id="3a021-393">Plus la valeur est faible, mieux c'est.</span><span class="sxs-lookup"><span data-stu-id="3a021-393">Lower is better.</span></span> |
| <span data-ttu-id="3a021-394">NumberOfDimensions</span><span class="sxs-lookup"><span data-stu-id="3a021-394">NumberOfDimensions</span></span> |<span data-ttu-id="3a021-395">Nombre de dimensions utilisées par l’algorithme une factorisation de matrice hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-395">Number of dimensions used by hello matrix factorization algorithm.</span></span> |

<span data-ttu-id="3a021-396">OData XML</span><span class="sxs-lookup"><span data-stu-id="3a021-396">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get model insight statistics</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-10-27T14:27:11Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">GetModelInsightStatisticsEntity</title>
        <updated>2014-10-27T14:27:11Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">CatalogCoverage</d:Key>
                <d:Value m:type="Edm.String">1.000</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetModelInsightStatisticsEntity</title>
        <updated>2014-10-27T14:27:11Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">Mpr</d:Key>
                <d:Value m:type="Edm.String">0.367</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">GetModelInsightStatisticsEntity</title>
        <updated>2014-10-27T14:27:11Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">NumberOfDimensions</d:Key>
                <d:Value m:type="Edm.String">20</d:Value>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="63----get-model-sample"></a><span data-ttu-id="3a021-397">6.3.</span><span class="sxs-lookup"><span data-stu-id="3a021-397">6.3.</span></span>    <span data-ttu-id="3a021-398">Obtention d'exemple de modèle</span><span class="sxs-lookup"><span data-stu-id="3a021-398">Get Model Sample</span></span>
<span data-ttu-id="3a021-399">Obtient un exemple de modèle de recommandation hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-399">Gets a sample of hello recommendation model.</span></span>

| <span data-ttu-id="3a021-400">Méthode HTTP</span><span class="sxs-lookup"><span data-stu-id="3a021-400">HTTP Method</span></span> | <span data-ttu-id="3a021-401">URI</span><span class="sxs-lookup"><span data-stu-id="3a021-401">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-402">GET</span><span class="sxs-lookup"><span data-stu-id="3a021-402">GET</span></span> |`<rootURI>/GetModelSample?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="3a021-403">Exemple :</span><span class="sxs-lookup"><span data-stu-id="3a021-403">Example:</span></span><br>`<rootURI>/GetModelSample?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="3a021-404">Avec l’ID de build spécifique :</span><span class="sxs-lookup"><span data-stu-id="3a021-404">With specific build ID:</span></span><br>`<rootURI>/GetModelSample?modelId=%27<model_id>%27&buildId=%27<build_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="3a021-405">Exemple :</span><span class="sxs-lookup"><span data-stu-id="3a021-405">Example:</span></span><br>`<rootURI>/GetModelSample?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&buildId=%271500068%27&apiVersion=%271.0%27` |

| <span data-ttu-id="3a021-406">Nom du paramètre</span><span class="sxs-lookup"><span data-stu-id="3a021-406">Parameter Name</span></span> | <span data-ttu-id="3a021-407">Valeurs valides</span><span class="sxs-lookup"><span data-stu-id="3a021-407">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-408">modelId</span><span class="sxs-lookup"><span data-stu-id="3a021-408">modelId</span></span> |<span data-ttu-id="3a021-409">Identificateur unique du modèle de hello</span><span class="sxs-lookup"><span data-stu-id="3a021-409">Unique identifier of hello model</span></span> |
| <span data-ttu-id="3a021-410">apiVersion</span><span class="sxs-lookup"><span data-stu-id="3a021-410">apiVersion</span></span> |<span data-ttu-id="3a021-411">1.0</span><span class="sxs-lookup"><span data-stu-id="3a021-411">1.0</span></span> |
|  | |
| <span data-ttu-id="3a021-412">Corps de la requête</span><span class="sxs-lookup"><span data-stu-id="3a021-412">Request Body</span></span> |<span data-ttu-id="3a021-413">AUCUN</span><span class="sxs-lookup"><span data-stu-id="3a021-413">NONE</span></span> |

<span data-ttu-id="3a021-414">**Réponse**:</span><span class="sxs-lookup"><span data-stu-id="3a021-414">**Response**:</span></span>

<span data-ttu-id="3a021-415">Code d'état HTTP : 200</span><span class="sxs-lookup"><span data-stu-id="3a021-415">HTTP Status code: 200</span></span>

<span data-ttu-id="3a021-416">OData XML</span><span class="sxs-lookup"><span data-stu-id="3a021-416">OData XML</span></span>

<span data-ttu-id="3a021-417">La réponse est retournée au format texte brut :</span><span class="sxs-lookup"><span data-stu-id="3a021-417">Response is returned in raw text format:</span></span>

<pre>
Level 1
---------------
655fc955-a5a3-4a26-9723-3090859cb27b, Prey: A Novel
    655fc955-a5a3-4a26-9723-3090859cb27b, Prey: A Novel Rating: 0.5215
    3f471802-f84f-44a0-99c8-6d2e7418eec1, Black Hawk Down: A Story of Modern War Rating: 0.5151
    07b10e28-9e7c-4032-90b7-10acab7f2460, Cryptonomicon Rating: 0.5148
    6afc18e4-8c2a-43d1-9021-57543d6b11d8, Imajica Rating: 0.5146
    e4cc5e69-3567-43ab-b00f-f0d8d0506870, Hit List Rating: 0.514
56b61441-0eed-46cc-a8f6-112775b81892, Life and Death in Shanghai
    56b61441-0eed-46cc-a8f6-112775b81892, Life and Death in Shanghai Rating: 0.5218
    53156702-cc0c-443d-b718-6fb74b2491d3, Son of \ Rating: 0.5212
    fb8cf7a6-8719-46ee-97d4-92f931d77a3a, Smoke and Mirrors: Short Fictions and Illusions Rating: 0.5188
    8f5fe006-79e4-4679-816b-950989d1db4b, A Place I've Never Been (Contemporary American Fiction) Rating: 0.5156
    d8db4583-cc0f-49ce-bc95-b7fa3491623f, Happiness: A Novel Rating: 0.5156
50471eec-9aeb-4900-84d7-21567ab18546, If hello Buddha Dated: A Handbook for Finding Love on a Spiritual Path
    cfe922a1-7ca0-4f8d-ad9d-b7cc87bfe0ef, Divine Secrets of hello Ya-Ya Sisterhood: A Novel Rating: 0.5266
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, hello Poisonwood Bible: A Novel Rating: 0.5252
    973f8cbd-0846-4f6b-9d28-4dd0d7dc3a19, Pigs in Heaven Rating: 0.5244
    e2cbf7ad-0636-4117-8b30-298da6df7077, Animal Dreams Rating: 0.5227
    6c818fd3-5a09-417d-9ab4-7ffe090f0fef, Confessions of an Ugly Stepsister: A Novel Rating: 0.5222
5e97148f-defb-4d74-af2d-80f4763bf531, hello Deep End of hello Ocean (Oprah's Book Club)
    5e97148f-defb-4d74-af2d-80f4763bf531, hello Deep End of hello Ocean (Oprah's Book Club) Rating: 0.537
    5dcbac37-2946-4f2a-a0b3-bbe710f9409a, Up Island: A Novel Rating: 0.5277
    bc5b69db-733b-4346-adde-3927544258f7, Downtown Rating: 0.5275
    31fe5c63-3e5a-48d0-802b-d3b0f989a634, Have a Nice Day: A Tale of Blood and Sweatsocks Rating: 0.5252
    0adf981a-b65b-4c11-b36b-78aca2f948a2, hello Perfect Storm: A True Story of Men Against hello Sea Rating: 0.5238
68f97068-ae1a-4163-9e94-396b800b743d, Modoc: hello True Story of hello Greatest Elephant That Ever Lived
    68f97068-ae1a-4163-9e94-396b800b743d, Modoc: hello True Story of hello Greatest Elephant That Ever Lived Rating: 0.5379
    6724862e-e4e7-4022-9614-1468d8b902ff, Little House on hello Prairie Rating: 0.5345
    cdedb837-1620-496d-94c4-6ccfed888320, Little House in hello Big Woods Rating: 0.5325
    382164ba-406b-4187-b726-d7a54b9d790d, hello Tao of Pooh Rating: 0.5309
    6a068d6a-bb74-4ba3-b3f2-a956c4f9d1b5, On hello Banks of Plum Creek Rating: 0.5285
37ef8e74-e348-44e5-aabc-1d7f9efcb25b, Men Are from Mars Women Are from Venus: A Practical Guide for Improving Communication and Getting What You Want in Your Relationships
    37ef8e74-e348-44e5-aabc-1d7f9efcb25b, Men Are from Mars, Women Are from Venus: A Practical Guide for Improving Communication and Getting What You Want in Your Relationships Rating: 0.5397
    f2be16d4-5faf-4d32-ab83-7ba74d29261e, Politically Correct Bedtime Stories: Modern Tales for Our Life and Times Rating: 0.5207
    ef732c5c-334b-4d6b-ab82-7255eb7286d0, Honor Among Thieves Rating: 0.5195
    0b209b8c-7cdd-47fd-b940-05c7ff7c60fc, hello Giving Tree Rating: 0.5194
    883b360f-8b42-407f-b977-2f44ad840877, Scary Stories tooTell in hello Dark: Collected from American Folklore (Scary Stories) Rating: 0.5184
ff51b67e-fa8e-4c5e-8f4d-02a928de735d, Men at Work: hello Craft of Baseball
    d008dae9-c73a-40a1-9a9b-96d5cf546f36, hello Gulag Archipelago 1918-1956: An Experiment in Literary Investigation I-II Rating: 0.5416
    ff51b67e-fa8e-4c5e-8f4d-02a928de735d, Men at Work: hello Craft of Baseball Rating: 0.5403
    49dec30e-0adb-411a-b186-48eaabf6f8bc, Fatherland Rating: 0.5394
    cc7964fd-d30f-478e-a425-93ddbdf094ed, Magic hello Gathering: Arena Vol. 1 Rating: 0.5379
    8a1e9f36-97af-4614-bed9-24e3940a05f3, More Sniglets: Any Word That Doesn't Appear in hello Dictionary but Should Rating: 0.5377
12a6d988-be21-4a09-8143-9d5f4261ba16, A Dream of Eagles
    07b10e28-9e7c-4032-90b7-10acab7f2460, Cryptonomicon Rating: 0.5417
    e4cc5e69-3567-43ab-b00f-f0d8d0506870, Hit List Rating: 0.5416
    1f1a34c4-9781-49f5-a3cc-acec3ae3c71d, hello Family Rating: 0.5371
    56daeffe-7d48-43cd-8ef8-7dffd0c103d3, Kilo Class Rating: 0.5366
    b2fe511e-5cb9-4a56-b823-2801e63e6a96, Legal Tender Rating: 0.5366
df87525b-e435-4bd6-8701-4e60ad344e28, Finding Fish
    56d33036-dfda-46b9-8e2a-76cb03921bb0, hello X-Files: Ground Zero Rating: 0.5417
    0780cde8-6529-4e1d-b6c6-082c1b80e596, Twelve Red Herrings Rating: 0.5416
    df87525b-e435-4bd6-8701-4e60ad344e28, Finding Fish Rating: 0.5408
    400fe331-2c35-490c-adbc-b28b4b73d56c, Shall We Tell hello President? Rating: 0.5383
    f86ad7d0-5c03-42b3-aebf-13d44aec8b30, Shades of Grace Rating: 0.5358
de1f62a4-89e6-44d2-aaee-992a4bf093f1, hello Map That Changed hello World: William Smith and hello Birth of Modern Geology
    de1f62a4-89e6-44d2-aaee-992a4bf093f1, hello Map That Changed hello World: William Smith and hello Birth of Modern Geology Rating: 0.5422
    b303538f-e2c6-4a2c-b425-8d21e684fc3e, My Uncle Oswald Rating: 0.5385
    34b84627-48af-4a4c-96c4-b26fb3863f56, Midnight In hello Garden of Good and Evil Rating: 0.5379
    306cbaa7-b1a8-4142-9d55-e11b5018a7a8, hello Street Lawyer Rating: 0.5376
    e53b4baa-8c09-45c4-95c0-b6a26b98770b, Miss Smillas Feeling for Snow Rating: 0.5367

Level 2
---------------
352aaea1-6b12-454d-a3d5-46379d9e4eb2, hello Sinister Pig (Hillerman Tony)
    352aaea1-6b12-454d-a3d5-46379d9e4eb2, hello Sinister Pig (Hillerman Tony) Rating: 0.5425
    74c49398-bc10-4af5-a658-a996a1201254, Children of hello Storm (Peters Elizabeth) Rating: 0.5387
    9ba80080-196e-43fd-8025-391d963f77e7, hello Floating Girl Rating: 0.5372
    e68f81d5-7745-4cc7-b943-fedb8fcc2ced, Killer Smile (Scottoline Lisa) Rating: 0.5353
    b2fe511e-5cb9-4a56-b823-2801e63e6a96, Legal Tender Rating: 0.5332
c65c3995-abf7-4c7b-bb3c-8eb5aa9be7a5, Lake Wobegon days
    0adf981a-b65b-4c11-b36b-78aca2f948a2, hello Perfect Storm: A True Story of Men Against hello Sea Rating: 0.5433
    c65c3995-abf7-4c7b-bb3c-8eb5aa9be7a5, Lake Wobegon days Rating: 0.543
    a00ae6ad-4a7f-4211-9836-75ce8834eb11, Sniglets (Snig'lit: Any Word That Doesn't Appear in hello Dictionary But Should) Rating: 0.5327
    6f6e192e-0d64-49ca-9b63-f09413ea1ee6, Politically Correct Holiday Stories: For an Enlightened Yuletide Season Rating: 0.5307
    798051a8-147d-4d46-b0dc-e836325029e6, AGE OF INNOCENCE (MOVIE TIE-IN) Rating: 0.5301
73f3e25a-e996-4162-9ed8-ff3d34075650, O Pioneers! (Penguin Twentieth-Century Classics)
    cba8163f-6536-436b-8130-47b4a43c827f, Trust No One (hello Official Guide toohello X-Files Vol. 2) Rating: 0.5434
    5708e4cb-2492-49c0-94a8-cc413eec5d89, Small Gods (Discworld Novels (Paperback)) Rating: 0.5406
    73f3e25a-e996-4162-9ed8-ff3d34075650, O Pioneers! (Penguin Twentieth-Century Classics) Rating: 0.5403
    d885b0bd-ae4b-452d-bdf2-faa90197dbc9, hello Color of Magic Rating: 0.539
    b133a9c4-4784-4db3-b100-d0d6dffb94d2, hello Truth Is Out There (hello Official Guide toohello X-Files Vol. 1) Rating: 0.5367
271700a5-854a-4d5a-8409-6b57a5ee4de4, Fluke: Or I Know Why hello Winged Whale Sings
    271700a5-854a-4d5a-8409-6b57a5ee4de4, Fluke: Or I Know Why hello Winged Whale Sings Rating: 0.5445
    2de1c354-90ff-47c5-a0db-1bad7d88ef94, hello Salaryman's Wife (Children of Violence Series) Rating: 0.5329
    d279416e-19c0-43f8-9ec9-a585947879ca, Zen Attitude Rating: 0.5316
    c8f854d7-3de3-4b23-8217-f4f851670fd4, Revenge of hello Cootie Girls: A Robin Hudson Mystery (Robin Hudson Mysteries (Paperback)) Rating: 0.5305
    8ef4751c-7074-409e-a3ac-d49b222fc864, Where hello Wild Things Are Rating: 0.5289
9ad1b620-0a7b-4543-8673-66d4c3bcb2f1, Their Eyes Were Watching God
    9ad1b620-0a7b-4543-8673-66d4c3bcb2f1, Their Eyes Were Watching God Rating: 0.5446
    da45c4d5-aba1-413b-a9bd-50df98b1e1d2, hello Bean Trees Rating: 0.5389
    65ecbdd1-131c-40c3-a3d6-d86ca281377a, hello God of Small Things Rating: 0.5387
    c78743bf-7947-4a0c-8db7-8a3bfe69ba70, hello Stone Diaries Rating: 0.5355
    973f8cbd-0846-4f6b-9d28-4dd0d7dc3a19, Pigs in Heaven Rating: 0.5344
5f17d90a-2604-4fe8-8977-1a280b9098b1, One for hello Money (Stephanie Plum Novels (Paperback))
    5f17d90a-2604-4fe8-8977-1a280b9098b1, One for hello Money (Stephanie Plum Novels (Paperback)) Rating: 0.5446
    57169b2b-9a8a-486b-9aac-1ed98ce57168, Final Appeal Rating: 0.5332
    efcb1bc4-7278-4a8f-b491-befde02070d6, Moment of Truth Rating: 0.5329
    1efa91a2-993b-4c43-9f5c-3454fc12612d, Burn Factor Rating: 0.5309
    24c59962-458a-4ec8-b95d-d694e861919c, At Home in Mitford (hello Mitford Years) Rating: 0.5303
4fd48c46-1a20-4c57-bc7f-a02ef123dc52, As Nature Made Him: hello Boy Who Was Raised As a Girl
    4fd48c46-1a20-4c57-bc7f-a02ef123dc52, As Nature Made Him: hello Boy Who Was Raised As a Girl Rating: 0.5449
    cd5f2c03-20cb-43be-a1fb-3b4233e63222, Pigs in Heaven Rating: 0.5329
    19985fdb-d07a-4a25-ae4a-97b9cb61e5d1, Love in hello Time of Cholera (Penguin Great Books of hello 20th Century) Rating: 0.5267
    15689d09-c711-4844-84d8-130a90237b26, Bel Canto Rating: 0.5245
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, hello Poisonwood Bible: A Novel Rating: 0.5235
98df28ec-41e7-4fca-b77f-8b0d3109085d, Star Trek Memories
    f874b5a3-5d40-4436-94ff-0fa1c090ddf5, hello Sun Also Rises (A Scribner classic) Rating: 0.5451
    98df28ec-41e7-4fca-b77f-8b0d3109085d, Star Trek Memories Rating: 0.5442
    0ce0014a-9a48-4013-a08a-7f2c11877930, H.M.S. Unseen Rating: 0.5421
    15316ca6-1e38-425f-893d-691944a47000, More Scary Stories tooTell In hello Dark Rating: 0.5409
    329d5682-3dc3-4206-8aa2-eef4b1032258, Letters from hello Earth Rating: 0.54
5b9445d5-c072-419c-8d49-6f669bb1b0a9, Daughter of Fortune: A Novel (Oprah's Book Club (Hardcover))
    5b9445d5-c072-419c-8d49-6f669bb1b0a9, Daughter of Fortune: A Novel (Oprah's Book Club (Hardcover)) Rating: 0.5462
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, hello Poisonwood Bible: A Novel Rating: 0.5372
    604eb3bd-6026-4f51-bffd-9fb54f180400, Family Pictures: A Novel Rating: 0.5341
    8d06d01d-31cd-4678-b6b1-140a67987ce9, Songs in Ordinary Time (Oprah's Book Club (Paperback)) Rating: 0.5334
    da45c4d5-aba1-413b-a9bd-50df98b1e1d2, hello Bean Trees Rating: 0.5319
d5358189-d70f-4e35-8add-34b83b4942b3, Pigs in Heaven
    d5358189-d70f-4e35-8add-34b83b4942b3, Pigs in Heaven Rating: 0.5491
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, hello Poisonwood Bible: A Novel Rating: 0.5401
    c78743bf-7947-4a0c-8db7-8a3bfe69ba70, hello Stone Diaries Rating: 0.5393
    8d06d01d-31cd-4678-b6b1-140a67987ce9, Songs in Ordinary Time (Oprah's Book Club (Paperback)) Rating: 0.5382
    973f8cbd-0846-4f6b-9d28-4dd0d7dc3a19, Pigs in Heaven Rating: 0.5367

</pre>


## <a name="7-model-business-rules"></a><span data-ttu-id="3a021-418">7. Règles métiers de modèle</span><span class="sxs-lookup"><span data-stu-id="3a021-418">7. Model Business Rules</span></span>
<span data-ttu-id="3a021-419">Il s’agit de types hello de règles prises en charge :</span><span class="sxs-lookup"><span data-stu-id="3a021-419">These are hello types of rules supported:</span></span>

* <span data-ttu-id="3a021-420"><strong>Liste de blocage</strong> -blocage vous permet de tooprovide une liste d’éléments que vous ne voulez pas tooreturn dans les résultats de recommandation hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-420"><strong>BlockList</strong> - BlockList enables you tooprovide a list of items that you do not want tooreturn in hello recommendation results.</span></span> 
* <span data-ttu-id="3a021-421"><strong>FeatureBlockList</strong> -fonctionnalité de blocage permet de vous tooblock les éléments selon les valeurs hello de ses fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="3a021-421"><strong>FeatureBlockList</strong> - Feature BlockList enables you tooblock items based on hello values of its features.</span></span>

<span data-ttu-id="3a021-422">*N’envoyez pas plus de 1 000 éléments dans une même règle de liste de blocage, car votre appel pourrait dépasser le délai d’attente. Si vous devez tooblock plus de 1 000 éléments, vous pouvez effectuer plusieurs appels de blocage.*</span><span class="sxs-lookup"><span data-stu-id="3a021-422">*Do not send more than 1000 items in a single blocklist rule or your call may timeout. If you need tooblock more than 1000 items, you can make several blocklist calls.*</span></span>

* <span data-ttu-id="3a021-423"><strong>Incitatives</strong> -incitatives vous permet de tooreturn d’éléments tooenforce dans les résultats de recommandation hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-423"><strong>Upsale</strong> - Upsale enables you tooenforce items tooreturn in hello recommendation results.</span></span>
* <span data-ttu-id="3a021-424"><strong>Liste blanche</strong> -permet de liste blanche tooonly vous proposer des recommandations à partir d’une liste d’éléments.</span><span class="sxs-lookup"><span data-stu-id="3a021-424"><strong>WhiteList</strong> - White List enables you tooonly suggest recommendations from a list of items.</span></span>
* <span data-ttu-id="3a021-425"><strong>FeatureWhiteList</strong> -liste d’autorisation de fonction vous permet de tooonly conseillé d’éléments qui ont des valeurs de fonctionnalité spécifique.</span><span class="sxs-lookup"><span data-stu-id="3a021-425"><strong>FeatureWhiteList</strong> - Feature White List enables you tooonly recommend items that have specific feature values.</span></span>
* <span data-ttu-id="3a021-426"><strong>PerSeedBlockList</strong> - par permet de liste de blocs de valeur initiale vous tooprovide par une liste d’éléments qui ne peuvent pas être retournés sous forme de résultats de la recommandation d’élément.</span><span class="sxs-lookup"><span data-stu-id="3a021-426"><strong>PerSeedBlockList</strong> - Per Seed Block List enables you tooprovide per item a list of items that cannot be returned as recommendation results.</span></span>

### <a name="71----get-model-rules"></a><span data-ttu-id="3a021-427">7.1.</span><span class="sxs-lookup"><span data-stu-id="3a021-427">7.1.</span></span>    <span data-ttu-id="3a021-428">Obtention de règles de modèle</span><span class="sxs-lookup"><span data-stu-id="3a021-428">Get Model Rules</span></span>
| <span data-ttu-id="3a021-429">Méthode HTTP</span><span class="sxs-lookup"><span data-stu-id="3a021-429">HTTP Method</span></span> | <span data-ttu-id="3a021-430">URI</span><span class="sxs-lookup"><span data-stu-id="3a021-430">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-431">GET</span><span class="sxs-lookup"><span data-stu-id="3a021-431">GET</span></span> |`<rootURI>/GetModelRules?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="3a021-432">Exemple :</span><span class="sxs-lookup"><span data-stu-id="3a021-432">Example:</span></span><br>`<rootURI>/GetModelRules?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| <span data-ttu-id="3a021-433">Nom du paramètre</span><span class="sxs-lookup"><span data-stu-id="3a021-433">Parameter Name</span></span> | <span data-ttu-id="3a021-434">Valeurs valides</span><span class="sxs-lookup"><span data-stu-id="3a021-434">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-435">modelId</span><span class="sxs-lookup"><span data-stu-id="3a021-435">modelId</span></span> |<span data-ttu-id="3a021-436">Identificateur unique du modèle de hello</span><span class="sxs-lookup"><span data-stu-id="3a021-436">Unique identifier of hello model</span></span> |
| <span data-ttu-id="3a021-437">apiVersion</span><span class="sxs-lookup"><span data-stu-id="3a021-437">apiVersion</span></span> |<span data-ttu-id="3a021-438">1.0</span><span class="sxs-lookup"><span data-stu-id="3a021-438">1.0</span></span> |
|  | |
| <span data-ttu-id="3a021-439">Corps de la requête</span><span class="sxs-lookup"><span data-stu-id="3a021-439">Request Body</span></span> |<span data-ttu-id="3a021-440">AUCUN</span><span class="sxs-lookup"><span data-stu-id="3a021-440">NONE</span></span> |

<span data-ttu-id="3a021-441">**Réponse**:</span><span class="sxs-lookup"><span data-stu-id="3a021-441">**Response**:</span></span>

<span data-ttu-id="3a021-442">Code d'état HTTP : 200</span><span class="sxs-lookup"><span data-stu-id="3a021-442">HTTP Status code: 200</span></span>

* <span data-ttu-id="3a021-443">`feed/entry/content/properties/Id` : identificateur unique de cette règle.</span><span class="sxs-lookup"><span data-stu-id="3a021-443">`feed/entry/content/properties/Id` - Unique identifier of this rule.</span></span>
* <span data-ttu-id="3a021-444">`feed/entry/content/properties/Type`-Type de règle de hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-444">`feed/entry/content/properties/Type` - Type of hello rule.</span></span>
* <span data-ttu-id="3a021-445">`feed/entry/content/properties/Parameter` : paramètre de la règle.</span><span class="sxs-lookup"><span data-stu-id="3a021-445">`feed/entry/content/properties/Parameter` - Rule parameter.</span></span>

<span data-ttu-id="3a021-446">OData XML</span><span class="sxs-lookup"><span data-stu-id="3a021-446">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get a list of rules for a model</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-05T12:58:57Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">GetAListOfRulesForAModelEntity</title>
        <updated>2014-11-05T12:58:57Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">1000043</d:Id>
                <d:Type m:type="Edm.String">BlockList</d:Type>
                <d:Parameters m:type="Edm.String">{"ItemsToExclude":["1000"]}</d:Parameters>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetAListOfRulesForAModelEntity</title>
        <updated>2014-11-05T12:58:57Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">1000044</d:Id>
                <d:Type m:type="Edm.String">BlockList</d:Type>
                <d:Parameters m:type="Edm.String">{"ItemsToExclude":["1001"]}</d:Parameters>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="72----add-rule"></a><span data-ttu-id="3a021-447">7.2.</span><span class="sxs-lookup"><span data-stu-id="3a021-447">7.2.</span></span>    <span data-ttu-id="3a021-448">Ajout de règle</span><span class="sxs-lookup"><span data-stu-id="3a021-448">Add Rule</span></span>
| <span data-ttu-id="3a021-449">Méthode HTTP</span><span class="sxs-lookup"><span data-stu-id="3a021-449">HTTP Method</span></span> | <span data-ttu-id="3a021-450">URI</span><span class="sxs-lookup"><span data-stu-id="3a021-450">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-451">POST</span><span class="sxs-lookup"><span data-stu-id="3a021-451">POST</span></span> |`<rootURI>/AddRule?apiVersion=%271.0%27` |
| <span data-ttu-id="3a021-452">HEADER</span><span class="sxs-lookup"><span data-stu-id="3a021-452">HEADER</span></span> |`"Content-Type", "text/xml"` |

| <span data-ttu-id="3a021-453">Nom du paramètre</span><span class="sxs-lookup"><span data-stu-id="3a021-453">Parameter Name</span></span> | <span data-ttu-id="3a021-454">Valeurs valides</span><span class="sxs-lookup"><span data-stu-id="3a021-454">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-455">apiVersion</span><span class="sxs-lookup"><span data-stu-id="3a021-455">apiVersion</span></span> |<span data-ttu-id="3a021-456">1.0</span><span class="sxs-lookup"><span data-stu-id="3a021-456">1.0</span></span> |
|  | |
| <span data-ttu-id="3a021-457">Corps de la requête</span><span class="sxs-lookup"><span data-stu-id="3a021-457">Request Body</span></span> | |

<span data-ttu-id="3a021-458"><ins>Chaque fois que des règles d’entreprise, en fournissant les ID d’élément, assurez-vous que toouse hello externe d’Id d’élément de hello (hello même Id que vous avez utilisé dans le fichier de catalogue hello)</ins></span><span class="sxs-lookup"><span data-stu-id="3a021-458"><ins>Whenever providing Item Ids for business rules, make sure toouse hello External Id of hello item (hello same Id that you used in hello catalog file)</ins></span></span><br><span data-ttu-id="3a021-459">
<ins>tooadd une règle de blocage :</ins></span><span class="sxs-lookup"><span data-stu-id="3a021-459">
<ins>tooadd a BlockList rule:</ins></span></span><br>`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>BlockList</Type><Value>{"ItemsToExclude":["2406E770-769C-4189-89DE-1C9283F93A96","3906E110-769C-4189-89DE-1C9283F98888"]}</Value></ApiFilter>`<br><br><span data-ttu-id="3a021-460"><ins>
<ins>tooadd une règle FeatureBlockList :</ins></span><span class="sxs-lookup"><span data-stu-id="3a021-460"><ins>
<ins>tooadd a FeatureBlockList rule:</ins></span></span><br>
<br>
`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>FeatureBlockList</Type><Value>{"Name":"Movie_category","Values":["Adult","Drama"]}</Value></ApiFilter>`<br><br><span data-ttu-id="3a021-461"><ins>tooadd une règle incitatives :</ins></span><span class="sxs-lookup"><span data-stu-id="3a021-461"><ins> tooadd an Upsale rule:</ins></span></span><br>`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>Upsale</Type><Value>{"ItemsToUpsale":["2406E770-769C-4189-89DE-1C9283F93A96"],"NumberOfItemsToUpsale":5}</Value></ApiFilter>`<br><br><span data-ttu-id="3a021-462">
<ins>tooadd une règle d’autorisation :</ins></span><span class="sxs-lookup"><span data-stu-id="3a021-462">
<ins>tooadd a WhiteList rule:</ins></span></span><br>
`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>WhiteList</Type><Value>{"ItemsToInclude":["2406E770-769C-4189-89DE-1C9283F93A96","1116E770-769C-4189-89DE-1C9283F88888"]}</Value></ApiFilter>`<br><br><span data-ttu-id="3a021-463"><ins>
<ins>tooadd une règle FeatureWhiteList :</ins></span><span class="sxs-lookup"><span data-stu-id="3a021-463"><ins>
<ins>tooadd a FeatureWhiteList rule:</ins></span></span><br>
<br>
`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>FeatureWhiteList</Type><Value>{"Name":"Movie_rating","Values":["PG13"]}</Value></ApiFilter>`<br><br><span data-ttu-id="3a021-464"><ins>tooadd une règle PerSeedBlockList :</ins></span><span class="sxs-lookup"><span data-stu-id="3a021-464"><ins> tooadd a PerSeedBlockList rule:</ins></span></span><br>`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>PerSeedBlockList</Type><Value>{"SeedItems":["9949"],"ItemsToExclude":["9862","8158","8244"]}</Value></ApiFilter>`|

<span data-ttu-id="3a021-465">**Réponse**:</span><span class="sxs-lookup"><span data-stu-id="3a021-465">**Response**:</span></span>

<span data-ttu-id="3a021-466">Code d'état HTTP : 200</span><span class="sxs-lookup"><span data-stu-id="3a021-466">HTTP Status code: 200</span></span>

<span data-ttu-id="3a021-467">Hello API renvoie hello nouvellement créé règle ses détails.</span><span class="sxs-lookup"><span data-stu-id="3a021-467">hello API returns hello newly created rule with its details.</span></span> <span data-ttu-id="3a021-468">propriété de règles Hello peut être extraites de hello suivant des chemins d’accès :</span><span class="sxs-lookup"><span data-stu-id="3a021-468">hello rules property can be retrieved from hello following paths:</span></span>

* <span data-ttu-id="3a021-469">`feed/entry/content/properties/Id` : identificateur unique de cette règle.</span><span class="sxs-lookup"><span data-stu-id="3a021-469">`feed/entry/content/properties/Id` - Unique identifier of this rule.</span></span>
* <span data-ttu-id="3a021-470">`feed/entry/content/properties/Type`-Type de règle de hello : liste de blocage ou incitatives.</span><span class="sxs-lookup"><span data-stu-id="3a021-470">`feed/entry/content/properties/Type` - Type of hello rule: BlockList or Upsale.</span></span>
* <span data-ttu-id="3a021-471">`feed/entry/content/properties/Parameter` : paramètre de la règle.</span><span class="sxs-lookup"><span data-stu-id="3a021-471">`feed/entry/content/properties/Parameter` - Rule parameter.</span></span>

<span data-ttu-id="3a021-472">OData XML</span><span class="sxs-lookup"><span data-stu-id="3a021-472">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/AddRule" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Add A Rule</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-05T11:13:28Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">AddARuleEntity</title>
        <updated>2014-11-05T11:13:28Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">1000041</d:Id>
                <d:Type m:type="Edm.String">BlockList</d:Type>
                <d:Parameters m:type="Edm.String">{"ItemsToExclude":["1002"]}</d:Parameters>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="73----delete-rule"></a><span data-ttu-id="3a021-473">7.3.</span><span class="sxs-lookup"><span data-stu-id="3a021-473">7.3.</span></span>    <span data-ttu-id="3a021-474">Suppression de règle</span><span class="sxs-lookup"><span data-stu-id="3a021-474">Delete Rule</span></span>
| <span data-ttu-id="3a021-475">Méthode HTTP</span><span class="sxs-lookup"><span data-stu-id="3a021-475">HTTP Method</span></span> | <span data-ttu-id="3a021-476">URI</span><span class="sxs-lookup"><span data-stu-id="3a021-476">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-477">SUPPRIMER</span><span class="sxs-lookup"><span data-stu-id="3a021-477">DELETE</span></span> |`<rootURI>/DeleteRule?modelId=%27<model_id>%27&filterId=%27<filter_Id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="3a021-478">Exemple :</span><span class="sxs-lookup"><span data-stu-id="3a021-478">Example:</span></span><br>`DeleteRule?modelId=%2724024f7e-b45c-419e-bfa2-dfd947e0d253%27&filterId=%271000011%27&apiVersion=%271.0%27` |

| <span data-ttu-id="3a021-479">Nom du paramètre</span><span class="sxs-lookup"><span data-stu-id="3a021-479">Parameter Name</span></span> | <span data-ttu-id="3a021-480">Valeurs valides</span><span class="sxs-lookup"><span data-stu-id="3a021-480">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-481">modelId</span><span class="sxs-lookup"><span data-stu-id="3a021-481">modelId</span></span> |<span data-ttu-id="3a021-482">Identificateur unique du modèle de hello</span><span class="sxs-lookup"><span data-stu-id="3a021-482">Unique identifier of hello model</span></span> |
| <span data-ttu-id="3a021-483">filterId</span><span class="sxs-lookup"><span data-stu-id="3a021-483">filterId</span></span> |<span data-ttu-id="3a021-484">Identificateur unique de filtre de hello</span><span class="sxs-lookup"><span data-stu-id="3a021-484">Unique identifier of hello filter</span></span> |
| <span data-ttu-id="3a021-485">apiVersion</span><span class="sxs-lookup"><span data-stu-id="3a021-485">apiVersion</span></span> |<span data-ttu-id="3a021-486">1.0</span><span class="sxs-lookup"><span data-stu-id="3a021-486">1.0</span></span> |
|  | |
| <span data-ttu-id="3a021-487">Corps de la requête</span><span class="sxs-lookup"><span data-stu-id="3a021-487">Request Body</span></span> |<span data-ttu-id="3a021-488">AUCUN</span><span class="sxs-lookup"><span data-stu-id="3a021-488">NONE</span></span> |

<span data-ttu-id="3a021-489">**Réponse**:</span><span class="sxs-lookup"><span data-stu-id="3a021-489">**Response**:</span></span>

<span data-ttu-id="3a021-490">Code d'état HTTP : 200</span><span class="sxs-lookup"><span data-stu-id="3a021-490">HTTP Status code: 200</span></span>

### <a name="74----delete-all-rules"></a><span data-ttu-id="3a021-491">7.4.</span><span class="sxs-lookup"><span data-stu-id="3a021-491">7.4.</span></span>    <span data-ttu-id="3a021-492">Suppression de toutes les règles</span><span class="sxs-lookup"><span data-stu-id="3a021-492">Delete All Rules</span></span>
| <span data-ttu-id="3a021-493">Méthode HTTP</span><span class="sxs-lookup"><span data-stu-id="3a021-493">HTTP Method</span></span> | <span data-ttu-id="3a021-494">URI</span><span class="sxs-lookup"><span data-stu-id="3a021-494">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-495">SUPPRIMER</span><span class="sxs-lookup"><span data-stu-id="3a021-495">DELETE</span></span> |`<rootURI>/DeleteAllRules?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="3a021-496">Exemple :</span><span class="sxs-lookup"><span data-stu-id="3a021-496">Example:</span></span><br>`DeleteAllRules?modelId=%2724024f7e-b45c-419e-bfa2-dfd947e0d253%27&apiVersion=%271.0%27` |

| <span data-ttu-id="3a021-497">Nom du paramètre</span><span class="sxs-lookup"><span data-stu-id="3a021-497">Parameter Name</span></span> | <span data-ttu-id="3a021-498">Valeurs valides</span><span class="sxs-lookup"><span data-stu-id="3a021-498">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-499">modelId</span><span class="sxs-lookup"><span data-stu-id="3a021-499">modelId</span></span> |<span data-ttu-id="3a021-500">Identificateur unique du modèle de hello</span><span class="sxs-lookup"><span data-stu-id="3a021-500">Unique identifier of hello model</span></span> |
| <span data-ttu-id="3a021-501">apiVersion</span><span class="sxs-lookup"><span data-stu-id="3a021-501">apiVersion</span></span> |<span data-ttu-id="3a021-502">1.0</span><span class="sxs-lookup"><span data-stu-id="3a021-502">1.0</span></span> |
|  | |
| <span data-ttu-id="3a021-503">Corps de la requête</span><span class="sxs-lookup"><span data-stu-id="3a021-503">Request Body</span></span> |<span data-ttu-id="3a021-504">AUCUN</span><span class="sxs-lookup"><span data-stu-id="3a021-504">NONE</span></span> |

<span data-ttu-id="3a021-505">**Réponse**:</span><span class="sxs-lookup"><span data-stu-id="3a021-505">**Response**:</span></span>

<span data-ttu-id="3a021-506">Code d'état HTTP : 200</span><span class="sxs-lookup"><span data-stu-id="3a021-506">HTTP Status code: 200</span></span>

## <a name="8-catalog"></a><span data-ttu-id="3a021-507">8. Catalogue</span><span class="sxs-lookup"><span data-stu-id="3a021-507">8. Catalog</span></span>
### <a name="81----import-catalog-data"></a><span data-ttu-id="3a021-508">8.1.</span><span class="sxs-lookup"><span data-stu-id="3a021-508">8.1.</span></span>    <span data-ttu-id="3a021-509">Importation de données de catalogue</span><span class="sxs-lookup"><span data-stu-id="3a021-509">Import Catalog Data</span></span>
<span data-ttu-id="3a021-510">Si vous téléchargez plusieurs catalogue fichiers toohello même modèle avec plusieurs appels, il insère uniquement hello nouveaux éléments de catalogue.</span><span class="sxs-lookup"><span data-stu-id="3a021-510">If you upload several catalog files toohello same model with several calls, we will insert only hello new catalog items.</span></span> <span data-ttu-id="3a021-511">Éléments existants resteront avec les valeurs d’origine hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-511">Existing items will remain with hello original values.</span></span> <span data-ttu-id="3a021-512">Vous ne pouvez pas mettre à jour des données de catalogue à l'aide de cette méthode.</span><span class="sxs-lookup"><span data-stu-id="3a021-512">You cannot update catalog data by using this method.</span></span>

<span data-ttu-id="3a021-513">les données du catalogue Hello doivent suivre hello suivant le format suivant :</span><span class="sxs-lookup"><span data-stu-id="3a021-513">hello catalog data should follow hello following format:</span></span>

* <span data-ttu-id="3a021-514">Sans caractéristiques : `<Item Id>,<Item Name>,<Item Category>[,<Description>]`</span><span class="sxs-lookup"><span data-stu-id="3a021-514">Without features - `<Item Id>,<Item Name>,<Item Category>[,<Description>]`</span></span>
* <span data-ttu-id="3a021-515">Avec caractéristiques : `<Item Id>,<Item Name>,<Item Category>,[<Description>],<Features list>`</span><span class="sxs-lookup"><span data-stu-id="3a021-515">With features - `<Item Id>,<Item Name>,<Item Category>,[<Description>],<Features list>`</span></span>

<span data-ttu-id="3a021-516">Remarque : la taille de fichier maximale hello est 200 Mo.</span><span class="sxs-lookup"><span data-stu-id="3a021-516">Note: hello maximum file size is 200MB.</span></span>

<span data-ttu-id="3a021-517">** Détails du format **</span><span class="sxs-lookup"><span data-stu-id="3a021-517">** Format details **</span></span>

| <span data-ttu-id="3a021-518">Nom</span><span class="sxs-lookup"><span data-stu-id="3a021-518">Name</span></span> | <span data-ttu-id="3a021-519">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="3a021-519">Mandatory</span></span> | <span data-ttu-id="3a021-520">Type</span><span class="sxs-lookup"><span data-stu-id="3a021-520">Type</span></span> | <span data-ttu-id="3a021-521">Description</span><span class="sxs-lookup"><span data-stu-id="3a021-521">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="3a021-522">Item Id</span><span class="sxs-lookup"><span data-stu-id="3a021-522">Item Id</span></span> |<span data-ttu-id="3a021-523">Oui</span><span class="sxs-lookup"><span data-stu-id="3a021-523">Yes</span></span> |<span data-ttu-id="3a021-524">[A-z], [a-z], [0-9], [_] &#40;trait de soulignement&#41;, [-] &#40;tiret&#41;</span><span class="sxs-lookup"><span data-stu-id="3a021-524">[A-z], [a-z], [0-9], [_] &#40;Underscore&#41;, [-] &#40;Dash&#41;</span></span><br> <span data-ttu-id="3a021-525">Longueur maximale : 50</span><span class="sxs-lookup"><span data-stu-id="3a021-525">Max length: 50</span></span> |<span data-ttu-id="3a021-526">Identificateur unique d'un élément.</span><span class="sxs-lookup"><span data-stu-id="3a021-526">Unique identifier of an item.</span></span> |
| <span data-ttu-id="3a021-527">Item Name</span><span class="sxs-lookup"><span data-stu-id="3a021-527">Item Name</span></span> |<span data-ttu-id="3a021-528">Oui</span><span class="sxs-lookup"><span data-stu-id="3a021-528">Yes</span></span> |<span data-ttu-id="3a021-529">Caractères alphanumériques</span><span class="sxs-lookup"><span data-stu-id="3a021-529">Any alphanumeric characters</span></span><br> <span data-ttu-id="3a021-530">Longueur maximale : 255</span><span class="sxs-lookup"><span data-stu-id="3a021-530">Max length: 255</span></span> |<span data-ttu-id="3a021-531">Nom de l'élément.</span><span class="sxs-lookup"><span data-stu-id="3a021-531">Item name.</span></span> |
| <span data-ttu-id="3a021-532">Item Category</span><span class="sxs-lookup"><span data-stu-id="3a021-532">Item Category</span></span> |<span data-ttu-id="3a021-533">Oui</span><span class="sxs-lookup"><span data-stu-id="3a021-533">Yes</span></span> |<span data-ttu-id="3a021-534">Caractères alphanumériques</span><span class="sxs-lookup"><span data-stu-id="3a021-534">Any alphanumeric characters</span></span> <br> <span data-ttu-id="3a021-535">Longueur maximale : 255</span><span class="sxs-lookup"><span data-stu-id="3a021-535">Max length: 255</span></span> |<span data-ttu-id="3a021-536">Catégorie toowhich cet élément appartient (par exemple, cuisine la documentation, documentaires...) ; peut être vide.</span><span class="sxs-lookup"><span data-stu-id="3a021-536">Category toowhich this item belongs (e.g. Cooking Books, Drama…); can be empty.</span></span> |
| <span data-ttu-id="3a021-537">Description</span><span class="sxs-lookup"><span data-stu-id="3a021-537">Description</span></span> |<span data-ttu-id="3a021-538">Non, sauf si des caractéristiques sont présentes (mais peut être vide)</span><span class="sxs-lookup"><span data-stu-id="3a021-538">No, unless features are present (but can be empty)</span></span> |<span data-ttu-id="3a021-539">Caractères alphanumériques</span><span class="sxs-lookup"><span data-stu-id="3a021-539">Any alphanumeric characters</span></span> <br> <span data-ttu-id="3a021-540">Longueur maximale : 4 000</span><span class="sxs-lookup"><span data-stu-id="3a021-540">Max length: 4000</span></span> |<span data-ttu-id="3a021-541">Description de cet élément.</span><span class="sxs-lookup"><span data-stu-id="3a021-541">Description of this item.</span></span> |
| <span data-ttu-id="3a021-542">Features list</span><span class="sxs-lookup"><span data-stu-id="3a021-542">Features list</span></span> |<span data-ttu-id="3a021-543">Non</span><span class="sxs-lookup"><span data-stu-id="3a021-543">No</span></span> |<span data-ttu-id="3a021-544">Caractères alphanumériques</span><span class="sxs-lookup"><span data-stu-id="3a021-544">Any alphanumeric characters</span></span> <br> <span data-ttu-id="3a021-545">Longueur maximale : 4 000 ; nombre maximal de caractéristiques : 20</span><span class="sxs-lookup"><span data-stu-id="3a021-545">Max length: 4000; Max number of features:20</span></span> |<span data-ttu-id="3a021-546">Séparées par des virgules de la liste des noms de fonction = valeur de fonctionnalité qui peut être utilisé tooenhance modèle recommandation ; consultez [rubriques avancées](#2-advanced-topics) section.</span><span class="sxs-lookup"><span data-stu-id="3a021-546">Comma-separated list of feature name=feature value that can be used tooenhance model recommendation; see [Advanced topics](#2-advanced-topics) section.</span></span> |

| <span data-ttu-id="3a021-547">Méthode HTTP</span><span class="sxs-lookup"><span data-stu-id="3a021-547">HTTP Method</span></span> | <span data-ttu-id="3a021-548">URI</span><span class="sxs-lookup"><span data-stu-id="3a021-548">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-549">POST</span><span class="sxs-lookup"><span data-stu-id="3a021-549">POST</span></span> |`<rootURI>/ImportCatalogFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="3a021-550">Exemple :</span><span class="sxs-lookup"><span data-stu-id="3a021-550">Example:</span></span><br>`<rootURI>/ImportCatalogFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |
| <span data-ttu-id="3a021-551">HEADER</span><span class="sxs-lookup"><span data-stu-id="3a021-551">HEADER</span></span> |`"Content-Type", "text/xml"` |

| <span data-ttu-id="3a021-552">Nom du paramètre</span><span class="sxs-lookup"><span data-stu-id="3a021-552">Parameter Name</span></span> | <span data-ttu-id="3a021-553">Valeurs valides</span><span class="sxs-lookup"><span data-stu-id="3a021-553">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-554">modelId</span><span class="sxs-lookup"><span data-stu-id="3a021-554">modelId</span></span> |<span data-ttu-id="3a021-555">Identificateur unique du modèle de hello</span><span class="sxs-lookup"><span data-stu-id="3a021-555">Unique identifier of hello model</span></span> |
| <span data-ttu-id="3a021-556">filename</span><span class="sxs-lookup"><span data-stu-id="3a021-556">filename</span></span> |<span data-ttu-id="3a021-557">Identificateur textuel du catalogue de hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-557">Textual identifier of hello catalog.</span></span><br><span data-ttu-id="3a021-558">Seuls les lettres (A-Z, a-z), les chiffres (0-9), les tirets (-) et les traits de soulignement (_) sont autorisés.</span><span class="sxs-lookup"><span data-stu-id="3a021-558">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="3a021-559">Longueur maximale : 50</span><span class="sxs-lookup"><span data-stu-id="3a021-559">Max length: 50</span></span> |
| <span data-ttu-id="3a021-560">apiVersion</span><span class="sxs-lookup"><span data-stu-id="3a021-560">apiVersion</span></span> |<span data-ttu-id="3a021-561">1.0</span><span class="sxs-lookup"><span data-stu-id="3a021-561">1.0</span></span> |
|  | |
| <span data-ttu-id="3a021-562">Corps de la requête</span><span class="sxs-lookup"><span data-stu-id="3a021-562">Request Body</span></span> |<span data-ttu-id="3a021-563">Exemple (avec caractéristiques) :</span><span class="sxs-lookup"><span data-stu-id="3a021-563">Example (with features):</span></span><br/><span data-ttu-id="3a021-564">créer des 2406e770-769c-4189-89de-1c9283f93a96, Clara Callan, livre, description du Registre hello, = Richard Wright, publisher = Harper FLAMANT ROSE Canada, année = 2001</span><span class="sxs-lookup"><span data-stu-id="3a021-564">2406e770-769c-4189-89de-1c9283f93a96,Clara Callan,Book,hello book  description,author=Richard Wright,publisher=Harper Flamingo Canada,year=2001</span></span><br><span data-ttu-id="3a021-565">21bf8088-b6c0-4509-870c-e1c7ac78304a, hello Forgetting salle : une illusion (livre Byzantium), livre, auteur = Nick Bantock, publisher = Harpercollins, année = 1997</span><span class="sxs-lookup"><span data-stu-id="3a021-565">21bf8088-b6c0-4509-870c-e1c7ac78304a,hello Forgetting Room: A Fiction (Byzantium Book),Book,,author=Nick Bantock,publisher=Harpercollins,year=1997</span></span><br><span data-ttu-id="3a021-566">3bb5cb44-d143-4bdd-a55c-443964bf4b23,Spadework,Book,,author=Timothy Findley, publisher=HarperFlamingo Canada, year=2001</span><span class="sxs-lookup"><span data-stu-id="3a021-566">3bb5cb44-d143-4bdd-a55c-443964bf4b23,Spadework,Book,,author=Timothy Findley, publisher=HarperFlamingo Canada, year=2001</span></span><br><span data-ttu-id="3a021-567">552a1940-21e4-4399-82bb-594b46d7ed54, retenue d’animaux, livre, description du Registre hello, auteur = Magnus Mills, publisher = publication Arcade, année = 1998</span><span class="sxs-lookup"><span data-stu-id="3a021-567">552a1940-21e4-4399-82bb-594b46d7ed54,Restraint of Beasts,Book,hello book description,author=Magnus Mills, publisher=Arcade Publishing, year=1998</span></span></pre> |

<span data-ttu-id="3a021-568">**Réponse**:</span><span class="sxs-lookup"><span data-stu-id="3a021-568">**Response**:</span></span>

<span data-ttu-id="3a021-569">Code d'état HTTP : 200</span><span class="sxs-lookup"><span data-stu-id="3a021-569">HTTP Status code: 200</span></span>

<span data-ttu-id="3a021-570">Hello API renvoie un rapport d’importation de hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-570">hello API returns a report of hello import.</span></span>

* <span data-ttu-id="3a021-571">`feed\entry\content\properties\LineCount` : nombre de lignes acceptées.</span><span class="sxs-lookup"><span data-stu-id="3a021-571">`feed\entry\content\properties\LineCount` - Number of lines accepted.</span></span>
* <span data-ttu-id="3a021-572">`feed\entry\content\properties\ErrorCount`-Nombre de lignes qui n’ont pas été ajoutés en raison de l’erreur de tooan.</span><span class="sxs-lookup"><span data-stu-id="3a021-572">`feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due tooan error.</span></span>

<span data-ttu-id="3a021-573">OData XML</span><span class="sxs-lookup"><span data-stu-id="3a021-573">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Import catalog file</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-10-05T06:58:04Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'" />
    <entry>
       <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">ImportCatalogFileEntity2</title>
        <updated>2014-10-05T06:58:04Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:LineCount m:type="Edm.String">4</d:LineCount>
                <d:ErrorCount m:type="Edm.String">0</d:ErrorCount>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="82----get-catalog"></a><span data-ttu-id="3a021-574">8.2.</span><span class="sxs-lookup"><span data-stu-id="3a021-574">8.2.</span></span>    <span data-ttu-id="3a021-575">Obtention de catalogue</span><span class="sxs-lookup"><span data-stu-id="3a021-575">Get Catalog</span></span>
<span data-ttu-id="3a021-576">Récupère tous les éléments de catalogue.</span><span class="sxs-lookup"><span data-stu-id="3a021-576">Retrieves all catalog items.</span></span>
<span data-ttu-id="3a021-577">Hello catalogue sera récupéré d’une page à la fois.</span><span class="sxs-lookup"><span data-stu-id="3a021-577">hello catalog will be retrieved one page at a time.</span></span> <span data-ttu-id="3a021-578">Si vous souhaitez que les éléments tooget à un index particulier, vous pouvez utiliser le paramètre d’odata hello $skip.</span><span class="sxs-lookup"><span data-stu-id="3a021-578">If you want tooget items at a particular index, you can use hello $skip odata parameter.</span></span> <span data-ttu-id="3a021-579">Par exemple si vous souhaitez que les éléments tooget commençant à la position 100, ajoutez le paramètre hello $skip = 100 toohello demande.</span><span class="sxs-lookup"><span data-stu-id="3a021-579">For instance if you want tooget items starting at position 100, add hello parameter $skip=100 toohello request.</span></span>

| <span data-ttu-id="3a021-580">Méthode HTTP</span><span class="sxs-lookup"><span data-stu-id="3a021-580">HTTP Method</span></span> | <span data-ttu-id="3a021-581">URI</span><span class="sxs-lookup"><span data-stu-id="3a021-581">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-582">GET</span><span class="sxs-lookup"><span data-stu-id="3a021-582">GET</span></span> |`<rootURI>/GetCatalog?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="3a021-583">Exemple :</span><span class="sxs-lookup"><span data-stu-id="3a021-583">Example:</span></span><br>`GetCatalog?modelId=%2724024f7e-b45c-419e-bfa2-dfd947e0d253%27&apiVersion=%271.0%27` |

| <span data-ttu-id="3a021-584">Nom du paramètre</span><span class="sxs-lookup"><span data-stu-id="3a021-584">Parameter Name</span></span> | <span data-ttu-id="3a021-585">Valeurs valides</span><span class="sxs-lookup"><span data-stu-id="3a021-585">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-586">modelId</span><span class="sxs-lookup"><span data-stu-id="3a021-586">modelId</span></span> |<span data-ttu-id="3a021-587">Identificateur unique du modèle de hello</span><span class="sxs-lookup"><span data-stu-id="3a021-587">Unique identifier of hello model</span></span> |
| <span data-ttu-id="3a021-588">apiVersion</span><span class="sxs-lookup"><span data-stu-id="3a021-588">apiVersion</span></span> |<span data-ttu-id="3a021-589">1.0</span><span class="sxs-lookup"><span data-stu-id="3a021-589">1.0</span></span> |
|  | |
| <span data-ttu-id="3a021-590">Corps de la requête</span><span class="sxs-lookup"><span data-stu-id="3a021-590">Request Body</span></span> |<span data-ttu-id="3a021-591">AUCUN</span><span class="sxs-lookup"><span data-stu-id="3a021-591">NONE</span></span> |

<span data-ttu-id="3a021-592">**Réponse**:</span><span class="sxs-lookup"><span data-stu-id="3a021-592">**Response**:</span></span>

<span data-ttu-id="3a021-593">Code d'état HTTP : 200</span><span class="sxs-lookup"><span data-stu-id="3a021-593">HTTP Status code: 200</span></span>

<span data-ttu-id="3a021-594">réponse de Hello comporte une entrée par un élément de catalogue.</span><span class="sxs-lookup"><span data-stu-id="3a021-594">hello response includes one entry per catalog item.</span></span> <span data-ttu-id="3a021-595">Chaque entrée a hello données suivantes :</span><span class="sxs-lookup"><span data-stu-id="3a021-595">Each entry has hello following data:</span></span>

* <span data-ttu-id="3a021-596">`feed/entry/content/properties/ExternalId`-ID externe de l’élément de catalogue, fourni par le client de hello hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-596">`feed/entry/content/properties/ExternalId` - Catalog item external ID, hello one provided by hello customer.</span></span>
* <span data-ttu-id="3a021-597">`feed/entry/content/properties/InternalId`-ID interne catalogue élément hello Outside Azure Machine Learning recommandations a généré.</span><span class="sxs-lookup"><span data-stu-id="3a021-597">`feed/entry/content/properties/InternalId` - Catalog item internal ID, hello one that Azure Machine Learning Recommendations has generated.</span></span>
* <span data-ttu-id="3a021-598">`feed/entry/content/properties/Name` : nom de l’élément de catalogue.</span><span class="sxs-lookup"><span data-stu-id="3a021-598">`feed/entry/content/properties/Name` - Catalog item name.</span></span>
* <span data-ttu-id="3a021-599">`feed/entry/content/properties/Category` : catégorie de l’élément de catalogue.</span><span class="sxs-lookup"><span data-stu-id="3a021-599">`feed/entry/content/properties/Category` - Catalog item category.</span></span>
* <span data-ttu-id="3a021-600">`feed/entry/content/properties/Description` : description de l’élément de catalogue.</span><span class="sxs-lookup"><span data-stu-id="3a021-600">`feed/entry/content/properties/Description` - Catalog item description.</span></span>
* <span data-ttu-id="3a021-601">`feed/entry/content/properties/Metadata` : métadonnées de l’élément de catalogue.</span><span class="sxs-lookup"><span data-stu-id="3a021-601">`feed/entry/content/properties/Metadata` - Catalog item metadata.</span></span>

<span data-ttu-id="3a021-602">OData XML</span><span class="sxs-lookup"><span data-stu-id="3a021-602">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get All Catalog Items</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">552A1940-21E4-4399-82BB-594B46D7ED54</d:ExternalId>
                <d:InternalId m:type="Edm.String">060db26a-e6a6-464e-bb52-436d2da82a50</d:InternalId>
                <d:Name m:type="Edm.String">Restraint of Beasts</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">2406E770-769C-4189-89DE-1C9283F93A96</d:ExternalId>
                <d:InternalId m:type="Edm.String">209d7bfe-2eb9-4455-92a3-7c867a41a74a</d:InternalId>
                <d:Name m:type="Edm.String">Clara Callan</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">3BB5CB44-D143-4BDD-A55C-443964BF4B23</d:ExternalId>
                <d:InternalId m:type="Edm.String">913ff79b-059b-4d4d-8042-6fa4cc1391dd</d:InternalId>
                <d:Name m:type="Edm.String">Spadework</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">21BF8088-B6C0-4509-870C-E1C7AC78304A</d:ExternalId>
                <d:InternalId m:type="Edm.String">ea65e4fa-768c-40b4-92c3-69d3e8178691</d:InternalId>
                <d:Name m:type="Edm.String">hello Forgetting Room: A Fiction (Byzantium Book)</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="83----get-catalog-items-by-token"></a><span data-ttu-id="3a021-603">8.3.</span><span class="sxs-lookup"><span data-stu-id="3a021-603">8.3.</span></span>    <span data-ttu-id="3a021-604">Obtention d'éléments de catalogue par jeton</span><span class="sxs-lookup"><span data-stu-id="3a021-604">Get Catalog Items by Token</span></span>
| <span data-ttu-id="3a021-605">Méthode HTTP</span><span class="sxs-lookup"><span data-stu-id="3a021-605">HTTP Method</span></span> | <span data-ttu-id="3a021-606">URI</span><span class="sxs-lookup"><span data-stu-id="3a021-606">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-607">GET</span><span class="sxs-lookup"><span data-stu-id="3a021-607">GET</span></span> |`<rootURI>/GetCatalogItemsByToken?modelId=%27<modelId>%27&token=%27<token>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="3a021-608">Exemple :</span><span class="sxs-lookup"><span data-stu-id="3a021-608">Example:</span></span><br>`GetCatalogItemsByToken?modelId=%270dbb55fa-7f11-418d-8537-8ff2d9d1d9c6%27&token=%27Cla%27&apiVersion=%271.0%27` |

| <span data-ttu-id="3a021-609">Nom du paramètre</span><span class="sxs-lookup"><span data-stu-id="3a021-609">Parameter Name</span></span> | <span data-ttu-id="3a021-610">Valeurs valides</span><span class="sxs-lookup"><span data-stu-id="3a021-610">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-611">modelId</span><span class="sxs-lookup"><span data-stu-id="3a021-611">modelId</span></span> |<span data-ttu-id="3a021-612">Identificateur unique du modèle de hello</span><span class="sxs-lookup"><span data-stu-id="3a021-612">Unique identifier of hello model</span></span> |
| <span data-ttu-id="3a021-613">token</span><span class="sxs-lookup"><span data-stu-id="3a021-613">token</span></span> |<span data-ttu-id="3a021-614">Jeton de nom de l’élément de catalogue hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-614">Token of hello catalog item’s name.</span></span> <span data-ttu-id="3a021-615">Doit contenir au moins 3 caractères.</span><span class="sxs-lookup"><span data-stu-id="3a021-615">Should contain at least 3 characters.</span></span> |
| <span data-ttu-id="3a021-616">apiVersion</span><span class="sxs-lookup"><span data-stu-id="3a021-616">apiVersion</span></span> |<span data-ttu-id="3a021-617">1.0</span><span class="sxs-lookup"><span data-stu-id="3a021-617">1.0</span></span> |
|  | |
| <span data-ttu-id="3a021-618">Corps de la requête</span><span class="sxs-lookup"><span data-stu-id="3a021-618">Request Body</span></span> |<span data-ttu-id="3a021-619">AUCUN</span><span class="sxs-lookup"><span data-stu-id="3a021-619">NONE</span></span> |

<span data-ttu-id="3a021-620">**Réponse**:</span><span class="sxs-lookup"><span data-stu-id="3a021-620">**Response**:</span></span>

<span data-ttu-id="3a021-621">Code d'état HTTP : 200</span><span class="sxs-lookup"><span data-stu-id="3a021-621">HTTP Status code: 200</span></span>

<span data-ttu-id="3a021-622">réponse de Hello comporte une entrée par un élément de catalogue.</span><span class="sxs-lookup"><span data-stu-id="3a021-622">hello response includes one entry per catalog item.</span></span> <span data-ttu-id="3a021-623">Chaque entrée a hello données suivantes :</span><span class="sxs-lookup"><span data-stu-id="3a021-623">Each entry has hello following data:</span></span>

* <span data-ttu-id="3a021-624">`feed/entry/content/properties/InternalId`-ID interne catalogue élément hello Outside Azure Machine Learning recommandations a généré.</span><span class="sxs-lookup"><span data-stu-id="3a021-624">`feed/entry/content/properties/InternalId` - Catalog item internal ID, hello one that Azure Machine Learning Recommendations has generated.</span></span>
* <span data-ttu-id="3a021-625">`feed/entry/content/properties/Name` : nom de l’élément de catalogue.</span><span class="sxs-lookup"><span data-stu-id="3a021-625">`feed/entry/content/properties/Name` - Catalog item name.</span></span>
* <span data-ttu-id="3a021-626">`feed/entry/content/properties/Rating` - (pour une utilisation ultérieure)</span><span class="sxs-lookup"><span data-stu-id="3a021-626">`feed/entry/content/properties/Rating` -  (for future use)</span></span>
* <span data-ttu-id="3a021-627">`feed/entry/content/properties/Reasoning` - (pour une utilisation ultérieure)</span><span class="sxs-lookup"><span data-stu-id="3a021-627">`feed/entry/content/properties/Reasoning` -  (for future use)</span></span>
* <span data-ttu-id="3a021-628">`feed/entry/content/properties/Metadata` - (pour une utilisation ultérieure)</span><span class="sxs-lookup"><span data-stu-id="3a021-628">`feed/entry/content/properties/Metadata` -  (for future use)</span></span>
* <span data-ttu-id="3a021-629">`feed/entry/content/properties/FormattedRating` (pour une utilisation ultérieure)</span><span class="sxs-lookup"><span data-stu-id="3a021-629">`feed/entry/content/properties/FormattedRating` - (for future use)</span></span>

<span data-ttu-id="3a021-630">OData XML</span><span class="sxs-lookup"><span data-stu-id="3a021-630">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get Catalog items that contain a token</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-29T11:48:19Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">CatalogItemsThatContainATokenEntity</title>
            <updated>2014-10-29T11:48:19Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                  <m:properties>
                    <d:Id m:type="Edm.String">2406E770-769C-4189-89DE-1C9283F93A96</d:Id>
                    <d:Name m:type="Edm.String">Clara Callan</d:Name>
                    <d:Rating m:type="Edm.Double">0</d:Rating>
                    <d:Reasoning m:type="Edm.String"></d:Reasoning>
                    <d:Metadata m:type="Edm.String"></d:Metadata>
                    <d:FormattedRating m:type="Edm.Double" m:null="true"></d:FormattedRating>
                  </m:properties>
            </content>
        </entry>
    </feed>

## <a name="9-usage-data"></a><span data-ttu-id="3a021-631">9. Données d'utilisation</span><span class="sxs-lookup"><span data-stu-id="3a021-631">9. Usage data</span></span>
### <a name="91----import-usage-data"></a><span data-ttu-id="3a021-632">9.1.</span><span class="sxs-lookup"><span data-stu-id="3a021-632">9.1.</span></span>    <span data-ttu-id="3a021-633">Importation de données d'utilisation</span><span class="sxs-lookup"><span data-stu-id="3a021-633">Import Usage Data</span></span>
#### <a name="911-uploading-file"></a><span data-ttu-id="3a021-634">9.1.1.</span><span class="sxs-lookup"><span data-stu-id="3a021-634">9.1.1.</span></span> <span data-ttu-id="3a021-635">Téléchargement d'un fichier</span><span class="sxs-lookup"><span data-stu-id="3a021-635">Uploading File</span></span>
<span data-ttu-id="3a021-636">Cette section montre comment les données d’utilisation tooupload à l’aide d’un fichier.</span><span class="sxs-lookup"><span data-stu-id="3a021-636">This section shows how tooupload usage data by using a file.</span></span> <span data-ttu-id="3a021-637">Vous pouvez appeler cette API plusieurs fois avec les données d'utilisation.</span><span class="sxs-lookup"><span data-stu-id="3a021-637">You can call this API several times with usage data.</span></span> <span data-ttu-id="3a021-638">Toutes les données d'utilisation sont enregistrées pour tous les appels.</span><span class="sxs-lookup"><span data-stu-id="3a021-638">All usage data will be saved for all calls.</span></span>

| <span data-ttu-id="3a021-639">Méthode HTTP</span><span class="sxs-lookup"><span data-stu-id="3a021-639">HTTP Method</span></span> | <span data-ttu-id="3a021-640">URI</span><span class="sxs-lookup"><span data-stu-id="3a021-640">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-641">POST</span><span class="sxs-lookup"><span data-stu-id="3a021-641">POST</span></span> |`<rootURI>/ImportUsageFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="3a021-642">Exemple :</span><span class="sxs-lookup"><span data-stu-id="3a021-642">Example:</span></span><br>`<rootURI>/ImportUsageFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27ImplicitMatrix10_Guid_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="3a021-643">Nom du paramètre</span><span class="sxs-lookup"><span data-stu-id="3a021-643">Parameter Name</span></span> | <span data-ttu-id="3a021-644">Valeurs valides</span><span class="sxs-lookup"><span data-stu-id="3a021-644">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-645">modelId</span><span class="sxs-lookup"><span data-stu-id="3a021-645">modelId</span></span> |<span data-ttu-id="3a021-646">Identificateur unique du modèle de hello</span><span class="sxs-lookup"><span data-stu-id="3a021-646">Unique identifier of hello model</span></span> |
| <span data-ttu-id="3a021-647">filename</span><span class="sxs-lookup"><span data-stu-id="3a021-647">filename</span></span> |<span data-ttu-id="3a021-648">Identificateur textuel du catalogue de hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-648">Textual identifier of hello catalog.</span></span><br><span data-ttu-id="3a021-649">Seuls les lettres (A-Z, a-z), les chiffres (0-9), les tirets (-) et les traits de soulignement (_) sont autorisés.</span><span class="sxs-lookup"><span data-stu-id="3a021-649">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="3a021-650">Longueur maximale : 50</span><span class="sxs-lookup"><span data-stu-id="3a021-650">Max length: 50</span></span> |
| <span data-ttu-id="3a021-651">apiVersion</span><span class="sxs-lookup"><span data-stu-id="3a021-651">apiVersion</span></span> |<span data-ttu-id="3a021-652">1.0</span><span class="sxs-lookup"><span data-stu-id="3a021-652">1.0</span></span> |
|  | |
| <span data-ttu-id="3a021-653">Corps de la requête</span><span class="sxs-lookup"><span data-stu-id="3a021-653">Request Body</span></span> |<span data-ttu-id="3a021-654">Données d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="3a021-654">Usage data.</span></span> <span data-ttu-id="3a021-655">Format :</span><span class="sxs-lookup"><span data-stu-id="3a021-655">Format:</span></span><br>`<User Id>,<Item Id>[,<Time>,<Event>]`<br><br><table><tr><th><span data-ttu-id="3a021-656">Nom</span><span class="sxs-lookup"><span data-stu-id="3a021-656">Name</span></span></th><th><span data-ttu-id="3a021-657">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="3a021-657">Mandatory</span></span></th><th><span data-ttu-id="3a021-658">Type</span><span class="sxs-lookup"><span data-stu-id="3a021-658">Type</span></span></th><th><span data-ttu-id="3a021-659">Description</span><span class="sxs-lookup"><span data-stu-id="3a021-659">Description</span></span></th></tr><tr><td><span data-ttu-id="3a021-660">User Id</span><span class="sxs-lookup"><span data-stu-id="3a021-660">User Id</span></span></td><td><span data-ttu-id="3a021-661">Oui</span><span class="sxs-lookup"><span data-stu-id="3a021-661">Yes</span></span></td><td><span data-ttu-id="3a021-662">[A-z], [a-z], [0-9], [_] &#40;trait de soulignement&#41;, [-] &#40;tiret&#41;</span><span class="sxs-lookup"><span data-stu-id="3a021-662">[A-z], [a-z], [0-9], [_] &#40;Underscore&#41;, [-] &#40;Dash&#41;</span></span><br> <span data-ttu-id="3a021-663">Longueur maximale : 255</span><span class="sxs-lookup"><span data-stu-id="3a021-663">Max length: 255</span></span> </td><td><span data-ttu-id="3a021-664">Identificateur unique d’un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="3a021-664">Unique identifier of a user.</span></span></td></tr><tr><td><span data-ttu-id="3a021-665">Item Id</span><span class="sxs-lookup"><span data-stu-id="3a021-665">Item Id</span></span></td><td><span data-ttu-id="3a021-666">Oui</span><span class="sxs-lookup"><span data-stu-id="3a021-666">Yes</span></span></td><td><span data-ttu-id="3a021-667">[A-z], [a-z], [0-9], [&#95;] &#40;trait de soulignement&#41;, [-] &#40;tiret&#41;</span><span class="sxs-lookup"><span data-stu-id="3a021-667">[A-z], [a-z], [0-9], [&#95;] &#40;Underscore&#41;, [-] &#40;Dash&#41;</span></span><br> <span data-ttu-id="3a021-668">Longueur maximale : 50</span><span class="sxs-lookup"><span data-stu-id="3a021-668">Max length: 50</span></span></td><td><span data-ttu-id="3a021-669">Identificateur unique d'un élément.</span><span class="sxs-lookup"><span data-stu-id="3a021-669">Unique identifier of an item.</span></span></td></tr><tr><td><span data-ttu-id="3a021-670">Time</span><span class="sxs-lookup"><span data-stu-id="3a021-670">Time</span></span></td><td><span data-ttu-id="3a021-671">Non</span><span class="sxs-lookup"><span data-stu-id="3a021-671">No</span></span></td><td><span data-ttu-id="3a021-672">Date au format suivant : AAAA/MM/JJTHH:MM:SS (par exemple, 2013/06/20T10:00:00)</span><span class="sxs-lookup"><span data-stu-id="3a021-672">Date in format: YYYY/MM/DDTHH:MM:SS (e.g. 2013/06/20T10:00:00)</span></span></td><td><span data-ttu-id="3a021-673">Indication de temps des données.</span><span class="sxs-lookup"><span data-stu-id="3a021-673">Time of data.</span></span></td></tr><tr><td><span data-ttu-id="3a021-674">Événement</span><span class="sxs-lookup"><span data-stu-id="3a021-674">Event</span></span></td><td><span data-ttu-id="3a021-675">Non, mais s'il est indiqué, la date doit l'être également</span><span class="sxs-lookup"><span data-stu-id="3a021-675">No; if supplied then must also put date</span></span></td><td><span data-ttu-id="3a021-676">Une des manières de hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="3a021-676">One of hello following:</span></span><br><span data-ttu-id="3a021-677">• Click (clic)</span><span class="sxs-lookup"><span data-stu-id="3a021-677">• Click</span></span><br><span data-ttu-id="3a021-678">• RecommendationClick (clic de recommandation)</span><span class="sxs-lookup"><span data-stu-id="3a021-678">• RecommendationClick</span></span><br><span data-ttu-id="3a021-679">•    AddShopCart (ajout au panier)</span><span class="sxs-lookup"><span data-stu-id="3a021-679">•    AddShopCart</span></span><br><span data-ttu-id="3a021-680">• RemoveShopCart (suppression du panier)</span><span class="sxs-lookup"><span data-stu-id="3a021-680">• RemoveShopCart</span></span><br><span data-ttu-id="3a021-681">• Purchase</span><span class="sxs-lookup"><span data-stu-id="3a021-681">• Purchase</span></span></td><td></td></tr></table><br><span data-ttu-id="3a021-682">Taille maximale du fichier : 200 Mo</span><span class="sxs-lookup"><span data-stu-id="3a021-682">Maximum file size: 200MB</span></span><br><br><span data-ttu-id="3a021-683">Exemple :</span><span class="sxs-lookup"><span data-stu-id="3a021-683">Example:</span></span><br><pre>149452,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>6360,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>50321,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>71285,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>224450,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>236645,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>107951,1b3d95e2-84e4-414c-bb38-be9cf461c347</pre> |

<span data-ttu-id="3a021-684">**Réponse**:</span><span class="sxs-lookup"><span data-stu-id="3a021-684">**Response**:</span></span>

<span data-ttu-id="3a021-685">Code d'état HTTP : 200</span><span class="sxs-lookup"><span data-stu-id="3a021-685">HTTP Status code: 200</span></span>

* <span data-ttu-id="3a021-686">`Feed\entry\content\properties\LineCount` : nombre de lignes acceptées.</span><span class="sxs-lookup"><span data-stu-id="3a021-686">`Feed\entry\content\properties\LineCount` - Number of lines accepted.</span></span>
* <span data-ttu-id="3a021-687">`Feed\entry\content\properties\ErrorCount`-Nombre de lignes qui n’ont pas été ajoutés en raison de l’erreur de tooan.</span><span class="sxs-lookup"><span data-stu-id="3a021-687">`Feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due tooan error.</span></span>
* <span data-ttu-id="3a021-688">`Feed\entry\content\properties\FileId` : identificateur de fichier.</span><span class="sxs-lookup"><span data-stu-id="3a021-688">`Feed\entry\content\properties\FileId` - File identifier.</span></span>

<span data-ttu-id="3a021-689">OData XML</span><span class="sxs-lookup"><span data-stu-id="3a021-689">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Add bulk usage data (usage file)</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T07:21:44Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">AddBulkUsageDataUsageFileEntity2</title>
    <updated>2014-10-05T07:21:44Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:LineCount m:type="Edm.String">33</d:LineCount>
        <d:ErrorCount m:type="Edm.String">0</d:ErrorCount>
        <d:FileId m:type="Edm.String">fead7c1c-db01-46c0-872f-65bcda36025d</d:FileId>
      </m:properties>
    </content>
      </entry>
    </feed>


#### <a name="912-using-data-acquisition"></a><span data-ttu-id="3a021-690">9.1.2.</span><span class="sxs-lookup"><span data-stu-id="3a021-690">9.1.2.</span></span> <span data-ttu-id="3a021-691">Utilisation de l'acquisition de données</span><span class="sxs-lookup"><span data-stu-id="3a021-691">Using Data Acquisition</span></span>
<span data-ttu-id="3a021-692">Cette section montre comment les événements de toosend dans réel heure tooAzure Machine Learning recommandations, généralement à partir de votre site Web.</span><span class="sxs-lookup"><span data-stu-id="3a021-692">This section shows how toosend events in real time tooAzure Machine Learning Recommendations, usually from your website.</span></span>

| <span data-ttu-id="3a021-693">Méthode HTTP</span><span class="sxs-lookup"><span data-stu-id="3a021-693">HTTP Method</span></span> | <span data-ttu-id="3a021-694">URI</span><span class="sxs-lookup"><span data-stu-id="3a021-694">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-695">POST</span><span class="sxs-lookup"><span data-stu-id="3a021-695">POST</span></span> |`<rootURI>/AddUsageEvent?apiVersion=%271.0%27` |
| <span data-ttu-id="3a021-696">HEADER</span><span class="sxs-lookup"><span data-stu-id="3a021-696">HEADER</span></span> |`"Content-Type", "text/xml"` |

| <span data-ttu-id="3a021-697">Nom du paramètre</span><span class="sxs-lookup"><span data-stu-id="3a021-697">Parameter Name</span></span> | <span data-ttu-id="3a021-698">Valeurs valides</span><span class="sxs-lookup"><span data-stu-id="3a021-698">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-699">apiVersion</span><span class="sxs-lookup"><span data-stu-id="3a021-699">apiVersion</span></span> |<span data-ttu-id="3a021-700">1.0</span><span class="sxs-lookup"><span data-stu-id="3a021-700">1.0</span></span> |
| <span data-ttu-id="3a021-701">Corps de la demande</span><span class="sxs-lookup"><span data-stu-id="3a021-701">Request body</span></span> |<span data-ttu-id="3a021-702">Entrée de données d’événement pour chaque événement, vous souhaitez toosend.</span><span class="sxs-lookup"><span data-stu-id="3a021-702">Event data entry for each event you want toosend.</span></span> <span data-ttu-id="3a021-703">Vous devez envoyer pour le même ID dans le champ de SessionId hello hello hello même session utilisateur ou un navigateur.</span><span class="sxs-lookup"><span data-stu-id="3a021-703">You should send for hello same user or browser session hello same ID in hello SessionId field.</span></span> <span data-ttu-id="3a021-704">(Consultez l'exemple du corps d'événement ci-dessous.)</span><span class="sxs-lookup"><span data-stu-id="3a021-704">(See sample of event body below.)</span></span> |

* <span data-ttu-id="3a021-705">Exemple pour l'événement « Click » :</span><span class="sxs-lookup"><span data-stu-id="3a021-705">Example for event 'Click':</span></span>
  
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
* <span data-ttu-id="3a021-706">Exemple pour l'événement « RecommendationClick » :</span><span class="sxs-lookup"><span data-stu-id="3a021-706">Example for event 'RecommendationClick':</span></span>
  
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
* <span data-ttu-id="3a021-707">Exemple pour l'événement « AddShopCart » :</span><span class="sxs-lookup"><span data-stu-id="3a021-707">Example for event 'AddShopCart':</span></span>
  
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
* <span data-ttu-id="3a021-708">Exemple pour l'événement « RemoveShopCart » :</span><span class="sxs-lookup"><span data-stu-id="3a021-708">Example for event 'RemoveShopCart':</span></span>
  
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
* <span data-ttu-id="3a021-709">Exemple pour l’événement « Purchase » :</span><span class="sxs-lookup"><span data-stu-id="3a021-709">Example for event 'Purchase':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
        <SessionId>11112222</SessionId>
        <EventData>
            <EventData>
                <Name>Purchase</Name>
                <PurchaseItems>
                    <PurchaseItem>
                        <ItemId>ABBF8081-C5C0-4F09-9701-E1C7AC78304A</ItemId>
                        <Count>1</Count>
                    </PurchaseItem>
                    <PurchaseItem>
                        <ItemId>21BF8088-B6C0-4509-870C-11C0AC7F304B</ItemId>
                        <Count>3</Count>
                    </PurchaseItem>
                </PurchaseItems>
            </EventData>
        </EventData>
        </Event>
* <span data-ttu-id="3a021-710">Exemple d'envoi de 2 événements « Click » et « AddShopCart » :</span><span class="sxs-lookup"><span data-stu-id="3a021-710">Example sending 2 events, 'Click' and 'AddShopCart':</span></span>
  
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

<span data-ttu-id="3a021-711">**Réponse**: Code d'état HTTP : 200</span><span class="sxs-lookup"><span data-stu-id="3a021-711">**Response**: HTTP Status code: 200</span></span>

### <a name="92----list-model-usage-files"></a><span data-ttu-id="3a021-712">9.2.</span><span class="sxs-lookup"><span data-stu-id="3a021-712">9.2.</span></span>    <span data-ttu-id="3a021-713">Liste des fichiers d'utilisation de modèle</span><span class="sxs-lookup"><span data-stu-id="3a021-713">List Model Usage Files</span></span>
<span data-ttu-id="3a021-714">Récupère les métadonnées de tous les fichiers d'utilisation du modèle.</span><span class="sxs-lookup"><span data-stu-id="3a021-714">Retrieves metadata of all model usage files.</span></span>
<span data-ttu-id="3a021-715">Hello l’utilisation de fichiers seront récupérés une page à la fois.</span><span class="sxs-lookup"><span data-stu-id="3a021-715">hello usage files will be retrieved one page at a time.</span></span> <span data-ttu-id="3a021-716">Chaque page contient 100 éléments.</span><span class="sxs-lookup"><span data-stu-id="3a021-716">Each page containes 100 items.</span></span> <span data-ttu-id="3a021-717">Si vous souhaitez que les éléments tooget à un index particulier, vous pouvez utiliser le paramètre d’odata hello $skip.</span><span class="sxs-lookup"><span data-stu-id="3a021-717">If you want tooget items at a particular index, you can use hello $skip odata parameter.</span></span> <span data-ttu-id="3a021-718">Par exemple si vous souhaitez que les éléments tooget commençant à la position 100, ajoutez le paramètre hello $skip = 100 toohello demande.</span><span class="sxs-lookup"><span data-stu-id="3a021-718">For instance if you want tooget items starting at position 100, add hello parameter $skip=100 toohello request.</span></span>

| <span data-ttu-id="3a021-719">Méthode HTTP</span><span class="sxs-lookup"><span data-stu-id="3a021-719">HTTP Method</span></span> | <span data-ttu-id="3a021-720">URI</span><span class="sxs-lookup"><span data-stu-id="3a021-720">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-721">GET</span><span class="sxs-lookup"><span data-stu-id="3a021-721">GET</span></span> |`<rootURI>/ListModelUsageFiles?forModelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="3a021-722">Exemple :</span><span class="sxs-lookup"><span data-stu-id="3a021-722">Example:</span></span><br>`<rootURI>/ListModelUsageFiles?forModelId=%270dbb55fa-7f11-418d-8537-8ff2d9d1d9c6%27&apiVersion=%271.0%27` |

| <span data-ttu-id="3a021-723">Nom du paramètre</span><span class="sxs-lookup"><span data-stu-id="3a021-723">Parameter Name</span></span> | <span data-ttu-id="3a021-724">Valeurs valides</span><span class="sxs-lookup"><span data-stu-id="3a021-724">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-725">forModelId</span><span class="sxs-lookup"><span data-stu-id="3a021-725">forModelId</span></span> |<span data-ttu-id="3a021-726">Identificateur unique du modèle de hello</span><span class="sxs-lookup"><span data-stu-id="3a021-726">Unique identifier of hello model</span></span> |
| <span data-ttu-id="3a021-727">apiVersion</span><span class="sxs-lookup"><span data-stu-id="3a021-727">apiVersion</span></span> |<span data-ttu-id="3a021-728">1.0</span><span class="sxs-lookup"><span data-stu-id="3a021-728">1.0</span></span> |
|  | |
| <span data-ttu-id="3a021-729">Corps de la requête</span><span class="sxs-lookup"><span data-stu-id="3a021-729">Request Body</span></span> |<span data-ttu-id="3a021-730">AUCUN</span><span class="sxs-lookup"><span data-stu-id="3a021-730">NONE</span></span> |

<span data-ttu-id="3a021-731">**Réponse**:</span><span class="sxs-lookup"><span data-stu-id="3a021-731">**Response**:</span></span>

<span data-ttu-id="3a021-732">Code d'état HTTP : 200</span><span class="sxs-lookup"><span data-stu-id="3a021-732">HTTP Status code: 200</span></span>

<span data-ttu-id="3a021-733">réponse de Hello comporte une entrée par fichier d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="3a021-733">hello response includes one entry per usage file.</span></span> <span data-ttu-id="3a021-734">Chaque entrée a hello données suivantes :</span><span class="sxs-lookup"><span data-stu-id="3a021-734">Each entry has hello following data:</span></span>

* <span data-ttu-id="3a021-735">`feed\entry\content\properties\Id` : ID du fichier utilisation.</span><span class="sxs-lookup"><span data-stu-id="3a021-735">`feed\entry\content\properties\Id` - Usage file ID.</span></span>
* <span data-ttu-id="3a021-736">`feed\entry\content\properties\Length` : longueur du fichier d’utilisation en Mo.</span><span class="sxs-lookup"><span data-stu-id="3a021-736">`feed\entry\content\properties\Length` - Usage file length in MB.</span></span>
* <span data-ttu-id="3a021-737">`feed\entry\content\properties\DateModified`-Date de création de fichier de l’utilisation de hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-737">`feed\entry\content\properties\DateModified` - Date when hello usage file was created.</span></span>
* <span data-ttu-id="3a021-738">`feed\entry\content\properties\UseInModel`-Si le fichier de l’utilisation de hello est utilisé dans le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-738">`feed\entry\content\properties\UseInModel` - Whether hello usage file is used in hello model.</span></span>

<span data-ttu-id="3a021-739">OData XML</span><span class="sxs-lookup"><span data-stu-id="3a021-739">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get a list of model's usage files info</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-30T09:40:25Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetAListOfModelsUsageFilesInfoEntity</title>
            <updated>2014-10-30T09:40:25Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Id m:type="Edm.String">4c067b42-e975-4cb2-8c98-a6ab80ed6d63</d:Id>
                    <d:Length m:type="Edm.Double">0</d:Length>
                    <d:DateModified m:type="Edm.String">10/30/2014 9:19:57 AM</d:DateModified>
                    <d:UseInModel m:type="Edm.String">true</d:UseInModel>
                </m:properties>
            </content>
        </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetAListOfModelsUsageFilesInfoEntity</title>
        <updated>2014-10-30T09:40:25Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">3126d816-4e80-4248-8339-1ebbdb9d544d</d:Id>
                <d:Length m:type="Edm.Double">0.001</d:Length>
                <d:DateModified m:type="Edm.String">10/30/2014 9:21:44 AM</d:DateModified>
                <d:UseInModel m:type="Edm.String">true</d:UseInModel>
              </m:properties>
        </content>
    </entry>
</feed>

### <a name="93----get-usage-statistics"></a><span data-ttu-id="3a021-740">9.3.</span><span class="sxs-lookup"><span data-stu-id="3a021-740">9.3.</span></span>    <span data-ttu-id="3a021-741">Obtention de statistiques d'utilisation</span><span class="sxs-lookup"><span data-stu-id="3a021-741">Get Usage Statistics</span></span>
<span data-ttu-id="3a021-742">Obtient les statistiques d'utilisation.</span><span class="sxs-lookup"><span data-stu-id="3a021-742">Gets usage statistics.</span></span>

| <span data-ttu-id="3a021-743">Méthode HTTP</span><span class="sxs-lookup"><span data-stu-id="3a021-743">HTTP Method</span></span> | <span data-ttu-id="3a021-744">URI</span><span class="sxs-lookup"><span data-stu-id="3a021-744">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-745">GET</span><span class="sxs-lookup"><span data-stu-id="3a021-745">GET</span></span> |`<rootURI>/GetUsageStatistics?modelId=%27<modelId>%27& startDate=%27<date>%27&endDate=%27<date>%27&eventTypes=%27<types>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="3a021-746">Exemple :</span><span class="sxs-lookup"><span data-stu-id="3a021-746">Example:</span></span><br>`<rootURI>/GetUsageStatistics?modelId=%271d20c34f-dca1-4eac-8e5d-f299e4e4ad66%27&startDate=%272014%2F10%2F17T00%3A00%3A00%27&endDate=%272014%2F11%2F16T00%3A00%3A00%27&eventTypes=%271%2C2%2C3%2C4%2C5%27&apiVersion=%271.0%27` |

| <span data-ttu-id="3a021-747">Nom du paramètre</span><span class="sxs-lookup"><span data-stu-id="3a021-747">Parameter Name</span></span> | <span data-ttu-id="3a021-748">Valeurs valides</span><span class="sxs-lookup"><span data-stu-id="3a021-748">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-749">modelId</span><span class="sxs-lookup"><span data-stu-id="3a021-749">modelId</span></span> |<span data-ttu-id="3a021-750">Identificateur unique du modèle de hello</span><span class="sxs-lookup"><span data-stu-id="3a021-750">Unique identifier of hello model</span></span> |
| <span data-ttu-id="3a021-751">startDate</span><span class="sxs-lookup"><span data-stu-id="3a021-751">startDate</span></span> |<span data-ttu-id="3a021-752">Date de début.</span><span class="sxs-lookup"><span data-stu-id="3a021-752">Start date.</span></span> <span data-ttu-id="3a021-753">Format : aaaa/MM/jjTHH:mm:ss</span><span class="sxs-lookup"><span data-stu-id="3a021-753">Format: yyyy/MM/ddTHH:mm:ss</span></span> |
| <span data-ttu-id="3a021-754">endDate</span><span class="sxs-lookup"><span data-stu-id="3a021-754">endDate</span></span> |<span data-ttu-id="3a021-755">Date de fin.</span><span class="sxs-lookup"><span data-stu-id="3a021-755">End date.</span></span> <span data-ttu-id="3a021-756">Format : aaaa/MM/jjTHH:mm:ss</span><span class="sxs-lookup"><span data-stu-id="3a021-756">Format: yyyy/MM/ddTHH:mm:ss</span></span> |
| <span data-ttu-id="3a021-757">eventTypes</span><span class="sxs-lookup"><span data-stu-id="3a021-757">eventTypes</span></span> |<span data-ttu-id="3a021-758">Types de séparées par des virgules de chaîne d’événement ou null tooget tous les événements</span><span class="sxs-lookup"><span data-stu-id="3a021-758">Comma-separated string of event types or null tooget all events</span></span> |
| <span data-ttu-id="3a021-759">apiVersion</span><span class="sxs-lookup"><span data-stu-id="3a021-759">apiVersion</span></span> |<span data-ttu-id="3a021-760">1.0</span><span class="sxs-lookup"><span data-stu-id="3a021-760">1.0</span></span> |
|  | |
| <span data-ttu-id="3a021-761">Corps de la requête</span><span class="sxs-lookup"><span data-stu-id="3a021-761">Request Body</span></span> |<span data-ttu-id="3a021-762">AUCUN</span><span class="sxs-lookup"><span data-stu-id="3a021-762">NONE</span></span> |

<span data-ttu-id="3a021-763">**Réponse**:</span><span class="sxs-lookup"><span data-stu-id="3a021-763">**Response**:</span></span>

<span data-ttu-id="3a021-764">Code d'état HTTP : 200</span><span class="sxs-lookup"><span data-stu-id="3a021-764">HTTP Status code: 200</span></span>

<span data-ttu-id="3a021-765">Collection d'éléments clé/valeur.</span><span class="sxs-lookup"><span data-stu-id="3a021-765">A collection of key/value elements.</span></span> <span data-ttu-id="3a021-766">Chacune d’elles contient sum hello d’événements pour un type d’événement spécifique groupées par heure.</span><span class="sxs-lookup"><span data-stu-id="3a021-766">Each one contains hello sum of events for a specific event type grouped by hour.</span></span>

* <span data-ttu-id="3a021-767">`feed\entry[i]\content\properties\Key`-Contient l’heure hello (regroupé par heure) et le type d’événement hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-767">`feed\entry[i]\content\properties\Key` - Contains hello time (grouped by hour) and hello event type.</span></span>
* <span data-ttu-id="3a021-768">`feed\entry[i]\content\properties\Value` : nombre total d’événements.</span><span class="sxs-lookup"><span data-stu-id="3a021-768">`feed\entry[i]\content\properties\Value` - Total event count.</span></span>

<span data-ttu-id="3a021-769">OData XML</span><span class="sxs-lookup"><span data-stu-id="3a021-769">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get usage statistics</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-18T11:39:16Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/9/2014 8:00:00 AM;Click</d:Event>
                <d:Value m:type="Edm.String">5</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/9/2014 8:00:00 AM;RecommendationClick</d:Event>
                <d:Value m:type="Edm.String">10</d:Value>
              </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/1/2014 8:00:00 AM;RemoveShopCart</d:Event>
                <d:Value m:type="Edm.String">10</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/5/2014 8:00:00 AM;RemoveShopCart</d:Event>
                <d:Value m:type="Edm.String">10</d:Value>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="94----get-usage-file-sample"></a><span data-ttu-id="3a021-770">9.4.</span><span class="sxs-lookup"><span data-stu-id="3a021-770">9.4.</span></span>    <span data-ttu-id="3a021-771">Obtention d'exemple de fichier d'utilisation</span><span class="sxs-lookup"><span data-stu-id="3a021-771">Get Usage File Sample</span></span>
<span data-ttu-id="3a021-772">Récupère hello premier 2 Ko d’utilisation de contenu du fichier.</span><span class="sxs-lookup"><span data-stu-id="3a021-772">Retrieves hello first 2KB of usage file content.</span></span>

| <span data-ttu-id="3a021-773">Méthode HTTP</span><span class="sxs-lookup"><span data-stu-id="3a021-773">HTTP Method</span></span> | <span data-ttu-id="3a021-774">URI</span><span class="sxs-lookup"><span data-stu-id="3a021-774">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-775">GET</span><span class="sxs-lookup"><span data-stu-id="3a021-775">GET</span></span> |`<rootURI>/GetUsageFileSample?modelId=%27<modelId>%27& fileId=%27<fileId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="3a021-776">Exemple :</span><span class="sxs-lookup"><span data-stu-id="3a021-776">Example:</span></span><br>`<rootURI>/GetUsageFileSample?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&fileId=%274c067b42-e975-4cb2-8c98-a6ab80ed6d63%27&apiVersion=%271.0%27` |

| <span data-ttu-id="3a021-777">Nom du paramètre</span><span class="sxs-lookup"><span data-stu-id="3a021-777">Parameter Name</span></span> | <span data-ttu-id="3a021-778">Valeurs valides</span><span class="sxs-lookup"><span data-stu-id="3a021-778">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-779">modelId</span><span class="sxs-lookup"><span data-stu-id="3a021-779">modelId</span></span> |<span data-ttu-id="3a021-780">Identificateur unique du modèle de hello</span><span class="sxs-lookup"><span data-stu-id="3a021-780">Unique identifier of hello model</span></span> |
| <span data-ttu-id="3a021-781">fileId</span><span class="sxs-lookup"><span data-stu-id="3a021-781">fileId</span></span> |<span data-ttu-id="3a021-782">Identificateur unique hello d’utilisation du fichier de modèle</span><span class="sxs-lookup"><span data-stu-id="3a021-782">Unique identifier of hello model usage file</span></span> |
| <span data-ttu-id="3a021-783">apiVersion</span><span class="sxs-lookup"><span data-stu-id="3a021-783">apiVersion</span></span> |<span data-ttu-id="3a021-784">1.0</span><span class="sxs-lookup"><span data-stu-id="3a021-784">1.0</span></span> |
|  | |
| <span data-ttu-id="3a021-785">Corps de la requête</span><span class="sxs-lookup"><span data-stu-id="3a021-785">Request Body</span></span> |<span data-ttu-id="3a021-786">AUCUN</span><span class="sxs-lookup"><span data-stu-id="3a021-786">NONE</span></span> |

<span data-ttu-id="3a021-787">**Réponse**:</span><span class="sxs-lookup"><span data-stu-id="3a021-787">**Response**:</span></span>

<span data-ttu-id="3a021-788">Code d'état HTTP : 200</span><span class="sxs-lookup"><span data-stu-id="3a021-788">HTTP Status code: 200</span></span>

<span data-ttu-id="3a021-789">La réponse est retournée au format texte brut :</span><span class="sxs-lookup"><span data-stu-id="3a021-789">Response is returned in raw text format:</span></span>

<pre>
85526,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
210926,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
116866,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
177458,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
274004,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
123883,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
37712,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
152249,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
250948,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
235588,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
158254,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
271195,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
141157,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
171118,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
225087,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
</pre>


### <a name="95----get-model-usage-file"></a><span data-ttu-id="3a021-790">9.5.</span><span class="sxs-lookup"><span data-stu-id="3a021-790">9.5.</span></span>    <span data-ttu-id="3a021-791">Obtention de fichier d'utilisation de modèle</span><span class="sxs-lookup"><span data-stu-id="3a021-791">Get Model Usage File</span></span>
<span data-ttu-id="3a021-792">Récupère le hello le contenu complet du fichier de l’utilisation de hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-792">Retrieves hello full content of hello usage file.</span></span>

| <span data-ttu-id="3a021-793">Méthode HTTP</span><span class="sxs-lookup"><span data-stu-id="3a021-793">HTTP Method</span></span> | <span data-ttu-id="3a021-794">URI</span><span class="sxs-lookup"><span data-stu-id="3a021-794">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-795">GET</span><span class="sxs-lookup"><span data-stu-id="3a021-795">GET</span></span> |`<rootURI>/GetModelUsageFile?mid=%27<modelId>%27& fid=%27<fileId>%27&download=%27<download_value>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="3a021-796">Exemple :</span><span class="sxs-lookup"><span data-stu-id="3a021-796">Example:</span></span><br>`<rootURI>/GetModelUsageFile?mid=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&fid=%273126d816-4e80-4248-8339-1ebbdb9d544d%27&download=%271%27&apiVersion=%271.0%27` |

| <span data-ttu-id="3a021-797">Nom du paramètre</span><span class="sxs-lookup"><span data-stu-id="3a021-797">Parameter Name</span></span> | <span data-ttu-id="3a021-798">Valeurs valides</span><span class="sxs-lookup"><span data-stu-id="3a021-798">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-799">mid</span><span class="sxs-lookup"><span data-stu-id="3a021-799">mid</span></span> |<span data-ttu-id="3a021-800">Identificateur unique du modèle de hello</span><span class="sxs-lookup"><span data-stu-id="3a021-800">Unique identifier of hello model</span></span> |
| <span data-ttu-id="3a021-801">fid</span><span class="sxs-lookup"><span data-stu-id="3a021-801">fid</span></span> |<span data-ttu-id="3a021-802">Identificateur unique hello d’utilisation du fichier de modèle</span><span class="sxs-lookup"><span data-stu-id="3a021-802">Unique identifier of hello model usage file</span></span> |
| <span data-ttu-id="3a021-803">télécharger</span><span class="sxs-lookup"><span data-stu-id="3a021-803">download</span></span> |<span data-ttu-id="3a021-804">1</span><span class="sxs-lookup"><span data-stu-id="3a021-804">1</span></span> |
| <span data-ttu-id="3a021-805">apiVersion</span><span class="sxs-lookup"><span data-stu-id="3a021-805">apiVersion</span></span> |<span data-ttu-id="3a021-806">1.0</span><span class="sxs-lookup"><span data-stu-id="3a021-806">1.0</span></span> |
|  | |
| <span data-ttu-id="3a021-807">Corps de la requête</span><span class="sxs-lookup"><span data-stu-id="3a021-807">Request Body</span></span> |<span data-ttu-id="3a021-808">AUCUN</span><span class="sxs-lookup"><span data-stu-id="3a021-808">NONE</span></span> |

<span data-ttu-id="3a021-809">**Réponse**:</span><span class="sxs-lookup"><span data-stu-id="3a021-809">**Response**:</span></span>

<span data-ttu-id="3a021-810">Code d'état HTTP : 200</span><span class="sxs-lookup"><span data-stu-id="3a021-810">HTTP Status code: 200</span></span>

<span data-ttu-id="3a021-811">La réponse est retournée au format texte brut :</span><span class="sxs-lookup"><span data-stu-id="3a021-811">Response is returned in raw text format:</span></span>

<pre>
85526,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
210926,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
116866,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
177458,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
274004,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
123883,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
37712,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
152249,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
250948,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
235588,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
158254,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
271195,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
141157,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
171118,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
225087,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
244881,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
50547,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
213090,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
260655,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
72214,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
189334,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
36326,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
189336,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
189334,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
260655,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
162100,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
54946,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
260965,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
102758,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
112602,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
163925,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
262998,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
144717,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
</pre>

### <a name="96----delete-usage-file"></a><span data-ttu-id="3a021-812">9.6.</span><span class="sxs-lookup"><span data-stu-id="3a021-812">9.6.</span></span>    <span data-ttu-id="3a021-813">Suppression de fichier d'utilisation</span><span class="sxs-lookup"><span data-stu-id="3a021-813">Delete Usage File</span></span>
<span data-ttu-id="3a021-814">Supprime le fichier d’utilisation de modèle spécifié hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-814">Deletes hello specified model usage file.</span></span>

| <span data-ttu-id="3a021-815">Méthode HTTP</span><span class="sxs-lookup"><span data-stu-id="3a021-815">HTTP Method</span></span> | <span data-ttu-id="3a021-816">URI</span><span class="sxs-lookup"><span data-stu-id="3a021-816">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-817">SUPPRIMER</span><span class="sxs-lookup"><span data-stu-id="3a021-817">DELETE</span></span> |`<rootURI>/DeleteUsageFile?modelId=%27<modelId>%27&fileId=%27<fileId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="3a021-818">Exemple :</span><span class="sxs-lookup"><span data-stu-id="3a021-818">Example:</span></span><br>`<rootURI>/DeleteUsageFile?modelId=%270f86d698-d0f4-4406-a684-d13d22c47a73%27&fileId=%27f2e0b09d-be5c-46b2-9ac2-c7f622e5e1a5%27&apiVersion=%271.0%27` |

| <span data-ttu-id="3a021-819">Nom du paramètre</span><span class="sxs-lookup"><span data-stu-id="3a021-819">Parameter Name</span></span> | <span data-ttu-id="3a021-820">Valeurs valides</span><span class="sxs-lookup"><span data-stu-id="3a021-820">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-821">modelId</span><span class="sxs-lookup"><span data-stu-id="3a021-821">modelId</span></span> |<span data-ttu-id="3a021-822">Identificateur unique du modèle de hello</span><span class="sxs-lookup"><span data-stu-id="3a021-822">Unique identifier of hello model</span></span> |
| <span data-ttu-id="3a021-823">fileId</span><span class="sxs-lookup"><span data-stu-id="3a021-823">fileId</span></span> |<span data-ttu-id="3a021-824">Identificateur unique de hello toobe de fichier supprimé</span><span class="sxs-lookup"><span data-stu-id="3a021-824">Unique identifier of hello file toobe deleted</span></span> |
| <span data-ttu-id="3a021-825">apiVersion</span><span class="sxs-lookup"><span data-stu-id="3a021-825">apiVersion</span></span> |<span data-ttu-id="3a021-826">1.0</span><span class="sxs-lookup"><span data-stu-id="3a021-826">1.0</span></span> |
|  | |
| <span data-ttu-id="3a021-827">Corps de la requête</span><span class="sxs-lookup"><span data-stu-id="3a021-827">Request Body</span></span> |<span data-ttu-id="3a021-828">AUCUN</span><span class="sxs-lookup"><span data-stu-id="3a021-828">NONE</span></span> |

<span data-ttu-id="3a021-829">**Réponse**:</span><span class="sxs-lookup"><span data-stu-id="3a021-829">**Response**:</span></span>

<span data-ttu-id="3a021-830">Code d'état HTTP : 200</span><span class="sxs-lookup"><span data-stu-id="3a021-830">HTTP Status code: 200</span></span>

### <a name="97----delete-all-usage-files"></a><span data-ttu-id="3a021-831">9.7.</span><span class="sxs-lookup"><span data-stu-id="3a021-831">9.7.</span></span>    <span data-ttu-id="3a021-832">Suppression de tous les fichiers d'utilisation</span><span class="sxs-lookup"><span data-stu-id="3a021-832">Delete All Usage Files</span></span>
<span data-ttu-id="3a021-833">Supprime tous les fichiers d'utilisation du modèle.</span><span class="sxs-lookup"><span data-stu-id="3a021-833">Deletes all model usage files.</span></span>

| <span data-ttu-id="3a021-834">Méthode HTTP</span><span class="sxs-lookup"><span data-stu-id="3a021-834">HTTP Method</span></span> | <span data-ttu-id="3a021-835">URI</span><span class="sxs-lookup"><span data-stu-id="3a021-835">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-836">SUPPRIMER</span><span class="sxs-lookup"><span data-stu-id="3a021-836">DELETE</span></span> |`<rootURI>/DeleteAllUsageFiles?modelId=%27<modelId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="3a021-837">Exemple :</span><span class="sxs-lookup"><span data-stu-id="3a021-837">Example:</span></span><br>`<rootURI>/DeleteAllUsageFiles?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&apiVersion=%271.0%27` |

| <span data-ttu-id="3a021-838">Nom du paramètre</span><span class="sxs-lookup"><span data-stu-id="3a021-838">Parameter Name</span></span> | <span data-ttu-id="3a021-839">Valeurs valides</span><span class="sxs-lookup"><span data-stu-id="3a021-839">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-840">modelId</span><span class="sxs-lookup"><span data-stu-id="3a021-840">modelId</span></span> |<span data-ttu-id="3a021-841">Identificateur unique du modèle de hello</span><span class="sxs-lookup"><span data-stu-id="3a021-841">Unique identifier of hello model</span></span> |
| <span data-ttu-id="3a021-842">apiVersion</span><span class="sxs-lookup"><span data-stu-id="3a021-842">apiVersion</span></span> |<span data-ttu-id="3a021-843">1.0</span><span class="sxs-lookup"><span data-stu-id="3a021-843">1.0</span></span> |
|  | |
| <span data-ttu-id="3a021-844">Corps de la requête</span><span class="sxs-lookup"><span data-stu-id="3a021-844">Request Body</span></span> |<span data-ttu-id="3a021-845">AUCUN</span><span class="sxs-lookup"><span data-stu-id="3a021-845">NONE</span></span> |

<span data-ttu-id="3a021-846">**Réponse**:</span><span class="sxs-lookup"><span data-stu-id="3a021-846">**Response**:</span></span>

<span data-ttu-id="3a021-847">Code d'état HTTP : 200</span><span class="sxs-lookup"><span data-stu-id="3a021-847">HTTP Status code: 200</span></span>

## <a name="10-features"></a><span data-ttu-id="3a021-848">10. Caractéristiques</span><span class="sxs-lookup"><span data-stu-id="3a021-848">10. Features</span></span>
<span data-ttu-id="3a021-849">Cette section montre comment tooretrieve fonctionnalité plus d’informations, telles que les fonctions hello importé et leurs valeurs, leur rang, et lorsque ce classement a été alloué.</span><span class="sxs-lookup"><span data-stu-id="3a021-849">This section shows how tooretrieve feature information, such as hello imported features and their values, their rank, and when this rank was allocated.</span></span> <span data-ttu-id="3a021-850">Fonctionnalités qui sont importées en tant que partie des données de catalogue hello et puis leur rang est associé à un rang.</span><span class="sxs-lookup"><span data-stu-id="3a021-850">Features are imported as part of hello catalog data, and then their rank is associated when a rank build is done.</span></span>
<span data-ttu-id="3a021-851">Rang dans la fonction peut modifier en fonction de modèle toohello des données d’utilisation et le type des éléments.</span><span class="sxs-lookup"><span data-stu-id="3a021-851">Feature rank can change according toohello pattern of usage data and type of items.</span></span> <span data-ttu-id="3a021-852">Mais pour les éléments/utilisation cohérentes, rang de hello doit avoir des petites fluctuations uniquement.</span><span class="sxs-lookup"><span data-stu-id="3a021-852">But for consistent usage/items, hello rank should have only small fluctuations.</span></span>
<span data-ttu-id="3a021-853">le rang de Hello de fonctionnalités est un nombre non négatif.</span><span class="sxs-lookup"><span data-stu-id="3a021-853">hello rank of features is a non-negative number.</span></span> <span data-ttu-id="3a021-854">Hello numéro 0 signifie que cette fonctionnalité hello n’était pas classée (se produit si vous appelez cette saisie semi-automatique toohello préalable de API de première génération de rang hello).</span><span class="sxs-lookup"><span data-stu-id="3a021-854">hello  number 0 means that hello feature was not ranked (happens if you invoke this API prior toohello completion of hello first rank build).</span></span> <span data-ttu-id="3a021-855">date de Hello auquel a été attribué rang de hello est appelée actualisation de score hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-855">hello date at which hello rank was attributed is called hello score freshness.</span></span>

### <a name="101-get-features-info-for-last-rank-build"></a><span data-ttu-id="3a021-856">10.1.</span><span class="sxs-lookup"><span data-stu-id="3a021-856">10.1.</span></span> <span data-ttu-id="3a021-857">Obtention d'informations sur les caractéristiques (pour la dernière build de classement)</span><span class="sxs-lookup"><span data-stu-id="3a021-857">Get Features Info (For Last Rank Build)</span></span>
<span data-ttu-id="3a021-858">Récupère les informations de fonctionnalité hello, y compris le classement, pour la dernière génération réussie rank hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-858">Retrieves hello feature information, including ranking, for hello last successful rank build.</span></span>

| <span data-ttu-id="3a021-859">Méthode HTTP</span><span class="sxs-lookup"><span data-stu-id="3a021-859">HTTP Method</span></span> | <span data-ttu-id="3a021-860">URI</span><span class="sxs-lookup"><span data-stu-id="3a021-860">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-861">GET</span><span class="sxs-lookup"><span data-stu-id="3a021-861">GET</span></span> |`<rootURI>/GetModelFeatures?modelId=%27<modelId>%27&samplingSize=%27<samplingSize>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="3a021-862">Exemple :</span><span class="sxs-lookup"><span data-stu-id="3a021-862">Example:</span></span><br>`<rootURI>/GetModelFeatures?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&samplingSize=10%27&apiVersion=%271.0%27` |

| <span data-ttu-id="3a021-863">Nom du paramètre</span><span class="sxs-lookup"><span data-stu-id="3a021-863">Parameter Name</span></span> | <span data-ttu-id="3a021-864">Valeurs valides</span><span class="sxs-lookup"><span data-stu-id="3a021-864">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-865">modelId</span><span class="sxs-lookup"><span data-stu-id="3a021-865">modelId</span></span> |<span data-ttu-id="3a021-866">Identificateur unique du modèle de hello</span><span class="sxs-lookup"><span data-stu-id="3a021-866">Unique identifier of hello model</span></span> |
| <span data-ttu-id="3a021-867">samplingSize</span><span class="sxs-lookup"><span data-stu-id="3a021-867">samplingSize</span></span> |<span data-ttu-id="3a021-868">Nombre de tooinclude de valeurs pour chaque fonctionnalité en fonction des données toohello présentes dans le catalogue de hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-868">Number of values tooinclude for each feature according toohello data present in hello catalog.</span></span> <br/><span data-ttu-id="3a021-869">Les valeurs possibles sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="3a021-869">Possible values are:</span></span><br> <span data-ttu-id="3a021-870">-1 : tous les échantillons.</span><span class="sxs-lookup"><span data-stu-id="3a021-870">-1 - All samples.</span></span> <br><span data-ttu-id="3a021-871">0 : aucun échantillonnage.</span><span class="sxs-lookup"><span data-stu-id="3a021-871">0 - No sampling.</span></span> <br><span data-ttu-id="3a021-872">N : retourne N échantillons pour chaque nom de caractéristique.</span><span class="sxs-lookup"><span data-stu-id="3a021-872">N - Return N samples for each feature name.</span></span> |
| <span data-ttu-id="3a021-873">apiVersion</span><span class="sxs-lookup"><span data-stu-id="3a021-873">apiVersion</span></span> |<span data-ttu-id="3a021-874">1.0</span><span class="sxs-lookup"><span data-stu-id="3a021-874">1.0</span></span> |
|  | |
| <span data-ttu-id="3a021-875">Corps de la requête</span><span class="sxs-lookup"><span data-stu-id="3a021-875">Request Body</span></span> |<span data-ttu-id="3a021-876">AUCUN</span><span class="sxs-lookup"><span data-stu-id="3a021-876">NONE</span></span> |

<span data-ttu-id="3a021-877">**Réponse**:</span><span class="sxs-lookup"><span data-stu-id="3a021-877">**Response**:</span></span>

<span data-ttu-id="3a021-878">Code d'état HTTP : 200</span><span class="sxs-lookup"><span data-stu-id="3a021-878">HTTP Status code: 200</span></span>

<span data-ttu-id="3a021-879">réponse de Hello contient une liste d’entrées d’informations de fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="3a021-879">hello response contains a list of feature info entries.</span></span> <span data-ttu-id="3a021-880">Chaque entrée contient :</span><span class="sxs-lookup"><span data-stu-id="3a021-880">Each entry contains:</span></span>

* <span data-ttu-id="3a021-881">`feed/entry/content/m:properties/d:Name` : nom de la caractéristique.</span><span class="sxs-lookup"><span data-stu-id="3a021-881">`feed/entry/content/m:properties/d:Name` - Feature name.</span></span>
* <span data-ttu-id="3a021-882">`feed/entry/content/m:properties/d:RankUpdateDate`-Date à quels hello rang a été alloué toothis fonctionnalité, également appelé</span><span class="sxs-lookup"><span data-stu-id="3a021-882">`feed/entry/content/m:properties/d:RankUpdateDate` - Date at which hello rank was allocated toothis feature, a.k.a.</span></span> <span data-ttu-id="3a021-883">« actualisation du score »).</span><span class="sxs-lookup"><span data-stu-id="3a021-883">score freshness feature.</span></span> <span data-ttu-id="3a021-884">Une date historique (« 0001-01-01T00:00:00 ») signifie qu'aucune build de classement n'a été exécutée.</span><span class="sxs-lookup"><span data-stu-id="3a021-884">A historical date ('0001-01-01T00:00:00') means that no rank build was performed.</span></span>
* <span data-ttu-id="3a021-885">`feed/entry/content/m:properties/d:Rank` : classement de la caractéristique (float).</span><span class="sxs-lookup"><span data-stu-id="3a021-885">`feed/entry/content/m:properties/d:Rank` - Feature rank (float).</span></span> <span data-ttu-id="3a021-886">Un classement de 2.0 ou plus désigne une bonne caractéristique.</span><span class="sxs-lookup"><span data-stu-id="3a021-886">A rank of 2.0 and up is considered a good feature.</span></span>
* <span data-ttu-id="3a021-887">`feed/entry/content/m:properties/d:SampleValues`-Liste de séparées par des virgules des valeurs de taille d’échantillonnage de toohello demandée.</span><span class="sxs-lookup"><span data-stu-id="3a021-887">`feed/entry/content/m:properties/d:SampleValues` - Comma-separated list of values up toohello sampling size requested.</span></span>

<span data-ttu-id="3a021-888">OData XML</span><span class="sxs-lookup"><span data-stu-id="3a021-888">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get hello features of a model</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2015-01-08T13:15:02Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">ModelFeaturesEntity</title>
        <updated>2015-01-08T13:15:02Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Name m:type="Edm.String">Author</d:Name>
                <d:RankUpdateDate m:type="Edm.String">0001-01-01T00:00:00</d:RankUpdateDate>
                <d:Rank m:type="Edm.String">0</d:Rank>
                <d:SampleValues m:type="Edm.String">A. A. Attanasio, A. A. Milne, A. Bates, A. C. Bhaktivedanta Swami Prabhupada et al., A. C. Crispin, A. C. Doyle, A. C. H. Smith, A. E. Parker, A. J. Holt, A. J. Matthews</d:SampleValues>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">ModelFeaturesEntity</title>
        <updated>2015-01-08T13:15:02Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Name m:type="Edm.String">Publisher</d:Name>
                <d:RankUpdateDate m:type="Edm.String">0001-01-01T00:00:00</d:RankUpdateDate>
                <d:Rank m:type="Edm.String">0</d:Rank>
                <d:SampleValues m:type="Edm.String">A. Mondadori, Abacus, Abacus Press, Abacus Uk, Abstract Studio, Acacia Press, Academy Chicago Publishers, Ace Books, ACE Charter, Actar</d:SampleValues>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">ModelFeaturesEntity</title>
        <updated>2015-01-08T13:15:02Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1"/>
        <contenttype="application/xml">
        <m:properties>
            <d:Name m:type="Edm.String">Year</d:Name>
            <d:RankUpdateDate m:type="Edm.String">0001-01-01T00:00:00</d:RankUpdateDate>
            <d:Rank m:type="Edm.String">0</d:Rank>
            <d:SampleValues m:type="Edm.String">0, 1920, 1926, 1927, 1929, 1930, 1932, 1942, 1943, 1946</d:SampleValues>
        </m:properties>
        </content>
    </entry>
</feed>

### <a name="102-get-features-info-for-specific-rank-build"></a><span data-ttu-id="3a021-889">10.2.</span><span class="sxs-lookup"><span data-stu-id="3a021-889">10.2.</span></span> <span data-ttu-id="3a021-890">Obtention d'informations sur les caractéristiques (pour une build de classement spécifique)</span><span class="sxs-lookup"><span data-stu-id="3a021-890">Get Features Info (For Specific Rank Build)</span></span>
<span data-ttu-id="3a021-891">Récupère les informations de fonctionnalité hello, y compris hello de classement pour une build de classement spécifique.</span><span class="sxs-lookup"><span data-stu-id="3a021-891">Retrieves hello feature information, including hello ranking for a specific rank build.</span></span>

| <span data-ttu-id="3a021-892">Méthode HTTP</span><span class="sxs-lookup"><span data-stu-id="3a021-892">HTTP Method</span></span> | <span data-ttu-id="3a021-893">URI</span><span class="sxs-lookup"><span data-stu-id="3a021-893">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-894">GET</span><span class="sxs-lookup"><span data-stu-id="3a021-894">GET</span></span> |`<rootURI>/GetModelFeatures?modelId=%27<modelId>%27&samplingSize=%27<samplingSize>%27&rankBuildId=<rankBuildId>&apiVersion=%271.0%27`<br><br><span data-ttu-id="3a021-895">Exemple :</span><span class="sxs-lookup"><span data-stu-id="3a021-895">Example:</span></span><br>`<rootURI>/GetModelFeatures?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&samplingSize=10%27&rankBuildId=1000551&apiVersion=%271.0%27` |

| <span data-ttu-id="3a021-896">Nom du paramètre</span><span class="sxs-lookup"><span data-stu-id="3a021-896">Parameter Name</span></span> | <span data-ttu-id="3a021-897">Valeurs valides</span><span class="sxs-lookup"><span data-stu-id="3a021-897">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-898">modelId</span><span class="sxs-lookup"><span data-stu-id="3a021-898">modelId</span></span> |<span data-ttu-id="3a021-899">Identificateur unique du modèle de hello</span><span class="sxs-lookup"><span data-stu-id="3a021-899">Unique identifier of hello model</span></span> |
| <span data-ttu-id="3a021-900">samplingSize</span><span class="sxs-lookup"><span data-stu-id="3a021-900">samplingSize</span></span> |<span data-ttu-id="3a021-901">Nombre de tooinclude de valeurs pour chaque fonctionnalité en fonction des données toohello présentes dans le catalogue de hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-901">Number of values tooinclude for each feature according toohello data present in hello catalog.</span></span><br/> <span data-ttu-id="3a021-902">Les valeurs possibles sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="3a021-902">Possible values are:</span></span><br> <span data-ttu-id="3a021-903">-1 : tous les échantillons.</span><span class="sxs-lookup"><span data-stu-id="3a021-903">-1 - All samples.</span></span> <br><span data-ttu-id="3a021-904">0 : aucun échantillonnage.</span><span class="sxs-lookup"><span data-stu-id="3a021-904">0 - No sampling.</span></span> <br><span data-ttu-id="3a021-905">N : retourne N échantillons pour chaque nom de caractéristique.</span><span class="sxs-lookup"><span data-stu-id="3a021-905">N - Return N samples for each feature name.</span></span> |
| <span data-ttu-id="3a021-906">rankBuildId</span><span class="sxs-lookup"><span data-stu-id="3a021-906">rankBuildId</span></span> |<span data-ttu-id="3a021-907">Identificateur unique de la génération de rang hello ou -1 pour la dernière build de rang hello</span><span class="sxs-lookup"><span data-stu-id="3a021-907">Unique identifier of hello rank build or -1 for hello last rank build</span></span> |
| <span data-ttu-id="3a021-908">apiVersion</span><span class="sxs-lookup"><span data-stu-id="3a021-908">apiVersion</span></span> |<span data-ttu-id="3a021-909">1.0</span><span class="sxs-lookup"><span data-stu-id="3a021-909">1.0</span></span> |
|  | |
| <span data-ttu-id="3a021-910">Corps de la requête</span><span class="sxs-lookup"><span data-stu-id="3a021-910">Request Body</span></span> |<span data-ttu-id="3a021-911">AUCUN</span><span class="sxs-lookup"><span data-stu-id="3a021-911">NONE</span></span> |

<span data-ttu-id="3a021-912">**Réponse**:</span><span class="sxs-lookup"><span data-stu-id="3a021-912">**Response**:</span></span>

<span data-ttu-id="3a021-913">Code d'état HTTP : 200</span><span class="sxs-lookup"><span data-stu-id="3a021-913">HTTP Status code: 200</span></span>

<span data-ttu-id="3a021-914">réponse de Hello contient une liste d’entrées d’informations de fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="3a021-914">hello response contains a list of feature info entries.</span></span> <span data-ttu-id="3a021-915">Chaque entrée contient :</span><span class="sxs-lookup"><span data-stu-id="3a021-915">Each entry contains:</span></span>

* <span data-ttu-id="3a021-916">`feed/entry/content/m:properties/d:Name` : nom de la caractéristique.</span><span class="sxs-lookup"><span data-stu-id="3a021-916">`feed/entry/content/m:properties/d:Name` - Feature name.</span></span>
* <span data-ttu-id="3a021-917">`feed/entry/content/m:properties/d:RankUpdateDate`-Date à quels hello rang a été alloué toothis fonctionnalité, également appelé</span><span class="sxs-lookup"><span data-stu-id="3a021-917">`feed/entry/content/m:properties/d:RankUpdateDate` - Date at which hello rank was allocated toothis feature, a.k.a.</span></span> <span data-ttu-id="3a021-918">« actualisation du score »).</span><span class="sxs-lookup"><span data-stu-id="3a021-918">score freshness feature.</span></span> <span data-ttu-id="3a021-919">Une date historique (« 0001-01-01T00:00:00 ») signifie qu'aucune build de classement n'a été exécutée.</span><span class="sxs-lookup"><span data-stu-id="3a021-919">A historical date ('0001-01-01T00:00:00') means that no rank build was performed.</span></span>
* <span data-ttu-id="3a021-920">`feed/entry/content/m:properties/d:Rank` : classement de la caractéristique (float).</span><span class="sxs-lookup"><span data-stu-id="3a021-920">`feed/entry/content/m:properties/d:Rank` - Feature rank (float).</span></span> <span data-ttu-id="3a021-921">Un classement de 2.0 ou plus désigne une bonne caractéristique.</span><span class="sxs-lookup"><span data-stu-id="3a021-921">A rank of 2.0 and up is considered a good feature.</span></span>
* <span data-ttu-id="3a021-922">`feed/entry/content/m:properties/d:SampleValues`-Liste de séparées par des virgules des valeurs de taille d’échantillonnage de toohello demandée.</span><span class="sxs-lookup"><span data-stu-id="3a021-922">`feed/entry/content/m:properties/d:SampleValues` - Comma-separated list of values up toohello sampling size requested.</span></span>

<span data-ttu-id="3a021-923">OData</span><span class="sxs-lookup"><span data-stu-id="3a021-923">OData</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get hello features of a model</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2015-01-08T13:54:22Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">ModelFeaturesEntity</title>
            <updated>2015-01-08T13:54:22Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Name m:type="Edm.String">Author</d:Name>
                    <d:RankUpdateDate m:type="Edm.String">2015-01-08T13:52:14.673</d:RankUpdateDate>
                    <d:Rank m:type="Edm.String">3.38867426</d:Rank>
                    <d:SampleValues m:type="Edm.String">A. A. Attanasio, A. A. Milne, A. Bates, A. C. Bhaktivedanta Swami Prabhupada et al., A. C. Crispin, A. C. Doyle, A. C. H. Smith, A. E. Parker, A. J. Holt, A. J. Matthews</d:SampleValues>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
            <title type="text">ModelFeaturesEntity</title>
            <updated>2015-01-08T13:54:22Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Name m:type="Edm.String">Publisher</d:Name>
                    <d:RankUpdateDate m:type="Edm.String">2015-01-08T13:52:14.673</d:RankUpdateDate>
                    <d:Rank m:type="Edm.String">1.67839336</d:Rank>
                    <d:SampleValues m:type="Edm.String">A. Mondadori, Abacus, Abacus Press, Abacus Uk, Abstract Studio, Acacia Press, Academy Chicago Publishers, Ace Books, ACE Charter, Actar</d:SampleValues>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
            <title type="text">ModelFeaturesEntity</title>
            <updated>2015-01-08T13:54:22Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Name m:type="Edm.String">Year</d:Name>
                    <d:RankUpdateDate m:type="Edm.String">2015-01-08T13:52:14.673</d:RankUpdateDate>
                    <d:Rank m:type="Edm.String">1.12352145</d:Rank>
                    <d:SampleValues m:type="Edm.String">0, 1920, 1926, 1927, 1929, 1930, 1932, 1942, 1943, 1946</d:SampleValues>
                </m:properties>
            </content>
        </entry>
    </feed>


## <a name="11-build"></a><span data-ttu-id="3a021-924">11. Créer</span><span class="sxs-lookup"><span data-stu-id="3a021-924">11. Build</span></span>
  <span data-ttu-id="3a021-925">Cette section explique hello différentes API liées toobuilds.</span><span class="sxs-lookup"><span data-stu-id="3a021-925">This section explains hello different APIs related toobuilds.</span></span> <span data-ttu-id="3a021-926">Il existe 3 types de builds : une build de recommandation, une build de classement et une build FBT (fréquemment achetés ensemble).</span><span class="sxs-lookup"><span data-stu-id="3a021-926">There are 3 types of builds: a recommendation build, a rank build and an FBT (frequently bought together) build.</span></span>

<span data-ttu-id="3a021-927">de la build Hello recommandation vise toogenerate utilisé par un modèle de recommandation pour des prédictions.</span><span class="sxs-lookup"><span data-stu-id="3a021-927">hello recommendation build's purpose is toogenerate a recommendation model used for predictions.</span></span> <span data-ttu-id="3a021-928">Les prédictions (pour ce type de build) sont de deux types :</span><span class="sxs-lookup"><span data-stu-id="3a021-928">Predictions (for this type of build) come in two flavors:</span></span>

* <span data-ttu-id="3a021-929">I2I - alias</span><span class="sxs-lookup"><span data-stu-id="3a021-929">I2I - a.k.a.</span></span> <span data-ttu-id="3a021-930">Élément tooItem recommandations - un élément ou une liste d’éléments de cette option prédit une liste d’éléments qui sont susceptibles de toobe intérêt majeur.</span><span class="sxs-lookup"><span data-stu-id="3a021-930">Item tooItem recommendations - given an item or a list of items this option will predict a list of items that are likely toobe of high interest.</span></span>
* <span data-ttu-id="3a021-931">U2I - alias</span><span class="sxs-lookup"><span data-stu-id="3a021-931">U2I - a.k.a.</span></span> <span data-ttu-id="3a021-932">Utilisateur tooItem recommandations - un id d’utilisateur (et éventuellement une liste d’éléments) cette option prédit une liste d’éléments qui sont susceptibles de toobe intérêt majeur pour hello donnée utilisateur (et son choix supplémentaire d’éléments).</span><span class="sxs-lookup"><span data-stu-id="3a021-932">User tooItem recommendations - given a user id (and optionally a list of items) this option will predict a list of items that are likely toobe of high interest for hello given user (and its additional choice of items).</span></span> <span data-ttu-id="3a021-933">recommandations de U2I Hello sont basées sur l’historique de hello d’éléments qui ont été dignes d’intérêt pour l’utilisateur hello temps toohello hello modèle a été construit.</span><span class="sxs-lookup"><span data-stu-id="3a021-933">hello U2I recommendations are based on hello history of items that were of interest for hello user up toohello time hello model was built.</span></span>

<span data-ttu-id="3a021-934">Une build rangée est une version technique qui vous permet de toolearn sur l’utilité de hello de vos fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="3a021-934">A rank build is a technical build that allows you toolearn about hello usefulness of your features.</span></span> <span data-ttu-id="3a021-935">En règle générale, dans l’ordre tooget hello meilleurs résultats pour un modèle de recommandation qui impliquent des fonctionnalités, vous devez prendre hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="3a021-935">Usually, in order tooget hello best result for a recommendation model involving features, you should take hello following steps:</span></span>

* <span data-ttu-id="3a021-936">Déclencher une build de classement (sauf si le score hello fonctionnalités est stable) et attendez que vous obtenez le score de fonctionnalité hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-936">Trigger a rank build (unless hello score of your features is stable) and wait till you get hello feature score.</span></span>
* <span data-ttu-id="3a021-937">Récupérer le rang hello de vos fonctionnalités en appelant hello [obtenir les informations de fonctionnalités](#101-get-features-info-for-last-rank-build) API.</span><span class="sxs-lookup"><span data-stu-id="3a021-937">Retrieve hello rank of your features by calling hello [Get Features Info](#101-get-features-info-for-last-rank-build) API.</span></span>
* <span data-ttu-id="3a021-938">Configurer une build de recommandation par hello paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="3a021-938">Configure a recommendation build with hello following parameters:</span></span>
  * <span data-ttu-id="3a021-939">`useFeatureInModel`-Définissez tooTrue.</span><span class="sxs-lookup"><span data-stu-id="3a021-939">`useFeatureInModel` - Set tooTrue.</span></span>
  * <span data-ttu-id="3a021-940">`ModelingFeatureList`-Set tooa séparées par des virgules liste des fonctions avec un score de 2.0 ou plus (en fonction des rangs toohello récupéré à l’étape précédente de hello).</span><span class="sxs-lookup"><span data-stu-id="3a021-940">`ModelingFeatureList` - Set tooa comma-separated list of features with a score of 2.0 or more (according toohello ranks you retrieved in hello previous step).</span></span>
  * <span data-ttu-id="3a021-941">`AllowColdItemPlacement`-Définissez tooTrue.</span><span class="sxs-lookup"><span data-stu-id="3a021-941">`AllowColdItemPlacement` - Set tooTrue.</span></span>
  * <span data-ttu-id="3a021-942">Vous pouvez éventuellement définir `EnableFeatureCorrelation` tooTrue et `ReasoningFeatureList` toohello la liste des fonctionnalités que vous souhaitez toouse des explications approfondies (généralement hello même liste de fonctionnalités utilisée dans la modélisation ou une sous-liste).</span><span class="sxs-lookup"><span data-stu-id="3a021-942">Optionally you can set `EnableFeatureCorrelation` tooTrue and `ReasoningFeatureList` toohello list of features you want toouse for explanations (usually hello same list of features used in modelling or a sublist).</span></span>
* <span data-ttu-id="3a021-943">Déclencheur hello recommandation build avec hello configuré les paramètres.</span><span class="sxs-lookup"><span data-stu-id="3a021-943">Trigger hello recommendation build with hello configured parameters.</span></span>

<span data-ttu-id="3a021-944">Remarque : Si vous ne configurez pas tous les paramètres (par exemple, appeler build de recommandation hello sans paramètres) ou vous ne désactivez pas explicitement l’utilisation de hello de fonctionnalités (par exemple, `UseFeatureInModel` définir tooFalse), hello système définit les paramètres liés à la fonctionnalité de hello toohello expliqué ci-dessus des valeurs au cas où il existe une build de classement.</span><span class="sxs-lookup"><span data-stu-id="3a021-944">Note: If you do not configure any parameters (e.g. invoke hello recommendation build without parameters) or you do not explicitly disable hello usage of features (e.g. `UseFeatureInModel` set tooFalse), hello system will set up hello feature-related parameters toohello explained values above in case a rank build exists.</span></span>

<span data-ttu-id="3a021-945">Il n’existe aucune restriction sur l’exécution d’une build de classement et une recommandation générer simultanément pour hello même modèle.</span><span class="sxs-lookup"><span data-stu-id="3a021-945">There is no restriction on running a rank build and a recommendation build concurrently for hello same model.</span></span> <span data-ttu-id="3a021-946">Néanmoins, vous ne peut pas exécuter deux versions de hello même type sur le même modèle en parallèle de hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-946">Nevertheless, you cannot run two builds of hello same type on hello same model in parallel.</span></span>

<span data-ttu-id="3a021-947">Une build FBT (Frequently Bought Together) est un autre algorithme de génération de recommandations. Parfois qualifié de « conservateur », ce système de recommandation convient bien aux catalogues qui ne sont pas homogènes par nature (homogènes : livres, films, certains produits alimentaires, articles de mode ; non homogènes : ordinateur et périphériques, produits interdomaines, très diversifiés).</span><span class="sxs-lookup"><span data-stu-id="3a021-947">An FBT (Frequently bought together) build is yet another recommendations algorithm called sometimes "conservative" recommender, which is good for catalogs that are not homogeneous in nature (homogeneous: books, movies, some food, fashion; non-homogeneous: computer and devices, cross-domain, highly diverse).</span></span>

<span data-ttu-id="3a021-948">Remarque : si les fichiers d’utilisation que vous avez téléchargé hello contiennent ce champ est facultatif hello « type d’événement » puis de FBT modélisation uniquement les événements « Achat » servira.</span><span class="sxs-lookup"><span data-stu-id="3a021-948">Note: if hello usage files that you uploaded contain hello optional field "event type" then for FBT modelling only "Purchase" events will be used.</span></span> <span data-ttu-id="3a021-949">Si aucun type d’événement n’est fourni, tous les événements sont considérés comme achat (purchase).</span><span class="sxs-lookup"><span data-stu-id="3a021-949">If no event type is provided all events will be considered as purchase.</span></span>

#### <a name="111-build-parameters"></a><span data-ttu-id="3a021-950">11.1 Paramètres de build</span><span class="sxs-lookup"><span data-stu-id="3a021-950">11.1 Build parameters</span></span>
<span data-ttu-id="3a021-951">Chaque type de build peut être configuré via un ensemble de paramètres (décrits ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="3a021-951">Each build type can be configured via a set of parameters (depicted below).</span></span> <span data-ttu-id="3a021-952">Si vous ne configurez pas les paramètres de hello, hello sera automatiquement attribut système valeurs de paramètres toohello selon les informations toohello présentes au moment de hello vous déclenchez une build.</span><span class="sxs-lookup"><span data-stu-id="3a021-952">If you don't configure hello parameters, hello system will automatically attribute values toohello parameters according toohello information present at hello time you trigger a build.</span></span>

##### <a name="1111-usage-condenser"></a><span data-ttu-id="3a021-953">11.1.1.</span><span class="sxs-lookup"><span data-stu-id="3a021-953">11.1.1.</span></span> <span data-ttu-id="3a021-954">Condenseur d'utilisation</span><span class="sxs-lookup"><span data-stu-id="3a021-954">Usage condenser</span></span>
<span data-ttu-id="3a021-955">Les utilisateurs ou éléments avec peu de points d'utilisation peuvent contenir plus de bruit que d'informations.</span><span class="sxs-lookup"><span data-stu-id="3a021-955">Users or items with few usage points might contain more noise than information.</span></span> <span data-ttu-id="3a021-956">système de Hello tentatives toopredict hello le nombre minimal de points de l’utilisation par toobe utilisateur ou cet élément utilisé dans un modèle.</span><span class="sxs-lookup"><span data-stu-id="3a021-956">hello system attempts toopredict hello minimal number of usage points per user/item toobe used in a model.</span></span> <span data-ttu-id="3a021-957">Ce nombre seront hello dehors des limites définies par hello ItemCutoffLowerBound et paramètres ItemCutoffUpperBound pour plage de hello définie par hello UserCutOffLowerBound et UserCutoffUpperBound des paramètres pour les utilisateurs et les éléments.</span><span class="sxs-lookup"><span data-stu-id="3a021-957">This number will be within hello range defined by hello ItemCutoffLowerBound and ItemCutoffUpperBound parameters for items, and hello range defined by hello UserCutOffLowerBound and UserCutoffUpperBound parameters for users.</span></span> <span data-ttu-id="3a021-958">effet de réfrigérant Hello pour les éléments ou les utilisateurs peut être réduite en définissant au moins une des toozero de limites hello correspondant.</span><span class="sxs-lookup"><span data-stu-id="3a021-958">hello condenser effect on items or users can be minimized by setting at least one of hello corresponding bounds toozero.</span></span>

##### <a name="1112-rank-build-parameters"></a><span data-ttu-id="3a021-959">11.1.2.</span><span class="sxs-lookup"><span data-stu-id="3a021-959">11.1.2.</span></span> <span data-ttu-id="3a021-960">Paramètres de build de classement</span><span class="sxs-lookup"><span data-stu-id="3a021-960">Rank build parameters</span></span>
<span data-ttu-id="3a021-961">tableau de Hello ci-dessous illustre les paramètres de génération hello pour une build de classement.</span><span class="sxs-lookup"><span data-stu-id="3a021-961">hello table below depicts hello build parameters for a rank build.</span></span>

| <span data-ttu-id="3a021-962">Clé</span><span class="sxs-lookup"><span data-stu-id="3a021-962">Key</span></span> | <span data-ttu-id="3a021-963">Description</span><span class="sxs-lookup"><span data-stu-id="3a021-963">Description</span></span> | <span data-ttu-id="3a021-964">Type</span><span class="sxs-lookup"><span data-stu-id="3a021-964">Type</span></span> | <span data-ttu-id="3a021-965">Valeur valide</span><span class="sxs-lookup"><span data-stu-id="3a021-965">Valid Value</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="3a021-966">NumberOfModelIterations</span><span class="sxs-lookup"><span data-stu-id="3a021-966">NumberOfModelIterations</span></span> |<span data-ttu-id="3a021-967">nombre de Hello d’itérations hello modèle fonctionne est reflétée par hello globale de calcul hello heure et la précision du modèle.</span><span class="sxs-lookup"><span data-stu-id="3a021-967">hello number of iterations hello model performs is reflected by hello overall compute time and hello model accuracy.</span></span> <span data-ttu-id="3a021-968">Hello hello nombre élevé, vous obtiendrez améliorer la précision de hello, mais hello de calcul prend plus de temps.</span><span class="sxs-lookup"><span data-stu-id="3a021-968">hello higher hello number, hello better accuracy you will get, but hello compute time will take longer.</span></span> |<span data-ttu-id="3a021-969">Entier </span><span class="sxs-lookup"><span data-stu-id="3a021-969">Integer</span></span> |<span data-ttu-id="3a021-970">10-50</span><span class="sxs-lookup"><span data-stu-id="3a021-970">10-50</span></span> |
| <span data-ttu-id="3a021-971">NumberOfModelDimensions</span><span class="sxs-lookup"><span data-stu-id="3a021-971">NumberOfModelDimensions</span></span> |<span data-ttu-id="3a021-972">un nombre de dimensions Hello relative nombre toohello du modèle de hello « features » va tenter de toofind au sein de vos données.</span><span class="sxs-lookup"><span data-stu-id="3a021-972">hello number of dimensions relates toohello number of 'features' hello model will try toofind within your data.</span></span> <span data-ttu-id="3a021-973">Augmentation du nombre hello de dimensions permettra de mieux précisément des résultats de hello dans des clusters plus petits.</span><span class="sxs-lookup"><span data-stu-id="3a021-973">Increasing hello number of dimensions will allow better fine-tuning of hello results into smaller clusters.</span></span> <span data-ttu-id="3a021-974">Toutefois, trop de dimensions empêche le modèle de hello recherche des corrélations entre les éléments.</span><span class="sxs-lookup"><span data-stu-id="3a021-974">However, too many dimensions will prevent hello model from finding correlations between items.</span></span> |<span data-ttu-id="3a021-975">Entier </span><span class="sxs-lookup"><span data-stu-id="3a021-975">Integer</span></span> |<span data-ttu-id="3a021-976">10-40</span><span class="sxs-lookup"><span data-stu-id="3a021-976">10-40</span></span> |
| <span data-ttu-id="3a021-977">ItemCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="3a021-977">ItemCutOffLowerBound</span></span> |<span data-ttu-id="3a021-978">Définit la limite d’inférieure élément hello pour les à hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-978">Defines hello item lower bound for hello condenser.</span></span> <span data-ttu-id="3a021-979">Consultez Condenseur d'utilisation ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="3a021-979">See usage condenser above.</span></span> |<span data-ttu-id="3a021-980">Integer</span><span class="sxs-lookup"><span data-stu-id="3a021-980">Integer</span></span> |<span data-ttu-id="3a021-981">2 ou plus (0 désactive le condenseur)</span><span class="sxs-lookup"><span data-stu-id="3a021-981">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="3a021-982">ItemCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="3a021-982">ItemCutOffUpperBound</span></span> |<span data-ttu-id="3a021-983">Définit la limite de supérieur élément hello pour les à hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-983">Defines hello item upper bound for hello condenser.</span></span> <span data-ttu-id="3a021-984">Consultez Condenseur d'utilisation ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="3a021-984">See usage condenser above.</span></span> |<span data-ttu-id="3a021-985">Integer</span><span class="sxs-lookup"><span data-stu-id="3a021-985">Integer</span></span> |<span data-ttu-id="3a021-986">2 ou plus (0 désactive le condenseur)</span><span class="sxs-lookup"><span data-stu-id="3a021-986">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="3a021-987">UserCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="3a021-987">UserCutOffLowerBound</span></span> |<span data-ttu-id="3a021-988">Définit la limite hello utilisateur pour les à hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-988">Defines hello user lower bound for hello condenser.</span></span> <span data-ttu-id="3a021-989">Consultez Condenseur d'utilisation ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="3a021-989">See usage condenser above.</span></span> |<span data-ttu-id="3a021-990">Integer</span><span class="sxs-lookup"><span data-stu-id="3a021-990">Integer</span></span> |<span data-ttu-id="3a021-991">2 ou plus (0 désactive le condenseur)</span><span class="sxs-lookup"><span data-stu-id="3a021-991">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="3a021-992">UserCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="3a021-992">UserCutOffUpperBound</span></span> |<span data-ttu-id="3a021-993">Définit la limite de supérieur utilisateur hello pour les à hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-993">Defines hello user upper bound for hello condenser.</span></span> <span data-ttu-id="3a021-994">Consultez Condenseur d'utilisation ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="3a021-994">See usage condenser above.</span></span> |<span data-ttu-id="3a021-995">Integer</span><span class="sxs-lookup"><span data-stu-id="3a021-995">Integer</span></span> |<span data-ttu-id="3a021-996">2 ou plus (0 désactive le condenseur)</span><span class="sxs-lookup"><span data-stu-id="3a021-996">2 or more (0 disable condenser)</span></span> |

##### <a name="1113-recommendation-build-parameters"></a><span data-ttu-id="3a021-997">11.1.3.</span><span class="sxs-lookup"><span data-stu-id="3a021-997">11.1.3.</span></span> <span data-ttu-id="3a021-998">Paramètres de build de recommandation</span><span class="sxs-lookup"><span data-stu-id="3a021-998">Recommendation build parameters</span></span>
<span data-ttu-id="3a021-999">tableau de Hello ci-dessous illustre les paramètres de génération hello pour la build de la recommandation.</span><span class="sxs-lookup"><span data-stu-id="3a021-999">hello table below depicts hello build parameters for recommendation build.</span></span>

| <span data-ttu-id="3a021-1000">Clé</span><span class="sxs-lookup"><span data-stu-id="3a021-1000">Key</span></span> | <span data-ttu-id="3a021-1001">Description</span><span class="sxs-lookup"><span data-stu-id="3a021-1001">Description</span></span> | <span data-ttu-id="3a021-1002">Type</span><span class="sxs-lookup"><span data-stu-id="3a021-1002">Type</span></span> | <span data-ttu-id="3a021-1003">Valeur valide</span><span class="sxs-lookup"><span data-stu-id="3a021-1003">Valid Value</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="3a021-1004">NumberOfModelIterations</span><span class="sxs-lookup"><span data-stu-id="3a021-1004">NumberOfModelIterations</span></span> |<span data-ttu-id="3a021-1005">nombre de Hello d’itérations hello modèle fonctionne est reflétée par hello globale de calcul hello heure et la précision du modèle.</span><span class="sxs-lookup"><span data-stu-id="3a021-1005">hello number of iterations hello model performs is reflected by hello overall compute time and hello model accuracy.</span></span> <span data-ttu-id="3a021-1006">Hello hello nombre élevé, vous obtiendrez améliorer la précision de hello, mais hello de calcul prend plus de temps.</span><span class="sxs-lookup"><span data-stu-id="3a021-1006">hello higher hello number, hello better accuracy you will get, but hello compute time will take longer.</span></span> |<span data-ttu-id="3a021-1007">Entier </span><span class="sxs-lookup"><span data-stu-id="3a021-1007">Integer</span></span> |<span data-ttu-id="3a021-1008">10-50</span><span class="sxs-lookup"><span data-stu-id="3a021-1008">10-50</span></span> |
| <span data-ttu-id="3a021-1009">NumberOfModelDimensions</span><span class="sxs-lookup"><span data-stu-id="3a021-1009">NumberOfModelDimensions</span></span> |<span data-ttu-id="3a021-1010">un nombre de dimensions Hello relative nombre toohello du modèle de hello « features » va tenter de toofind au sein de vos données.</span><span class="sxs-lookup"><span data-stu-id="3a021-1010">hello number of dimensions relates toohello number of 'features' hello model will try toofind within your data.</span></span> <span data-ttu-id="3a021-1011">Augmentation du nombre hello de dimensions permettra de mieux précisément des résultats de hello dans des clusters plus petits.</span><span class="sxs-lookup"><span data-stu-id="3a021-1011">Increasing hello number of dimensions will allow better fine-tuning of hello results into smaller clusters.</span></span> <span data-ttu-id="3a021-1012">Toutefois, trop de dimensions empêche le modèle de hello recherche des corrélations entre les éléments.</span><span class="sxs-lookup"><span data-stu-id="3a021-1012">However, too many dimensions will prevent hello model from finding correlations between items.</span></span> |<span data-ttu-id="3a021-1013">Entier </span><span class="sxs-lookup"><span data-stu-id="3a021-1013">Integer</span></span> |<span data-ttu-id="3a021-1014">10-40</span><span class="sxs-lookup"><span data-stu-id="3a021-1014">10-40</span></span> |
| <span data-ttu-id="3a021-1015">ItemCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="3a021-1015">ItemCutOffLowerBound</span></span> |<span data-ttu-id="3a021-1016">Définit la limite d’inférieure élément hello pour les à hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-1016">Defines hello item lower bound for hello condenser.</span></span> <span data-ttu-id="3a021-1017">Consultez Condenseur d'utilisation ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="3a021-1017">See usage condenser above.</span></span> |<span data-ttu-id="3a021-1018">Integer</span><span class="sxs-lookup"><span data-stu-id="3a021-1018">Integer</span></span> |<span data-ttu-id="3a021-1019">2 ou plus (0 désactive le condenseur)</span><span class="sxs-lookup"><span data-stu-id="3a021-1019">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="3a021-1020">ItemCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="3a021-1020">ItemCutOffUpperBound</span></span> |<span data-ttu-id="3a021-1021">Définit la limite de supérieur élément hello pour les à hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-1021">Defines hello item upper bound for hello condenser.</span></span> <span data-ttu-id="3a021-1022">Consultez Condenseur d'utilisation ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="3a021-1022">See usage condenser above.</span></span> |<span data-ttu-id="3a021-1023">Integer</span><span class="sxs-lookup"><span data-stu-id="3a021-1023">Integer</span></span> |<span data-ttu-id="3a021-1024">2 ou plus (0 désactive le condenseur)</span><span class="sxs-lookup"><span data-stu-id="3a021-1024">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="3a021-1025">UserCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="3a021-1025">UserCutOffLowerBound</span></span> |<span data-ttu-id="3a021-1026">Définit la limite hello utilisateur pour les à hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-1026">Defines hello user lower bound for hello condenser.</span></span> <span data-ttu-id="3a021-1027">Consultez Condenseur d'utilisation ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="3a021-1027">See usage condenser above.</span></span> |<span data-ttu-id="3a021-1028">Integer</span><span class="sxs-lookup"><span data-stu-id="3a021-1028">Integer</span></span> |<span data-ttu-id="3a021-1029">2 ou plus (0 désactive le condenseur)</span><span class="sxs-lookup"><span data-stu-id="3a021-1029">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="3a021-1030">UserCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="3a021-1030">UserCutOffUpperBound</span></span> |<span data-ttu-id="3a021-1031">Définit la limite de supérieur utilisateur hello pour les à hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-1031">Defines hello user upper bound for hello condenser.</span></span> <span data-ttu-id="3a021-1032">Consultez Condenseur d'utilisation ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="3a021-1032">See usage condenser above.</span></span> |<span data-ttu-id="3a021-1033">Integer</span><span class="sxs-lookup"><span data-stu-id="3a021-1033">Integer</span></span> |<span data-ttu-id="3a021-1034">2 ou plus (0 désactive le condenseur)</span><span class="sxs-lookup"><span data-stu-id="3a021-1034">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="3a021-1035">Description</span><span class="sxs-lookup"><span data-stu-id="3a021-1035">Description</span></span> |<span data-ttu-id="3a021-1036">Description de la build.</span><span class="sxs-lookup"><span data-stu-id="3a021-1036">Build description.</span></span> |<span data-ttu-id="3a021-1037">String</span><span class="sxs-lookup"><span data-stu-id="3a021-1037">String</span></span> |<span data-ttu-id="3a021-1038">Tout texte, 512 caractères maximum</span><span class="sxs-lookup"><span data-stu-id="3a021-1038">Any text, maximum 512 chars</span></span> |
| <span data-ttu-id="3a021-1039">EnableModelingInsights</span><span class="sxs-lookup"><span data-stu-id="3a021-1039">EnableModelingInsights</span></span> |<span data-ttu-id="3a021-1040">Vous permet de toocompute métriques sur le modèle de recommandation hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-1040">Allows you toocompute metrics on hello recommendation model.</span></span> |<span data-ttu-id="3a021-1041">Boolean</span><span class="sxs-lookup"><span data-stu-id="3a021-1041">Boolean</span></span> |<span data-ttu-id="3a021-1042">True/False</span><span class="sxs-lookup"><span data-stu-id="3a021-1042">True/False</span></span> |
| <span data-ttu-id="3a021-1043">UseFeaturesInModel</span><span class="sxs-lookup"><span data-stu-id="3a021-1043">UseFeaturesInModel</span></span> |<span data-ttu-id="3a021-1044">Indique si les fonctionnalités peuvent être utilisées dans le modèle de recommandation d’ordre tooenhance hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-1044">Indicates if features can be used in order tooenhance hello recommendation model.</span></span> |<span data-ttu-id="3a021-1045">Boolean</span><span class="sxs-lookup"><span data-stu-id="3a021-1045">Boolean</span></span> |<span data-ttu-id="3a021-1046">True/False</span><span class="sxs-lookup"><span data-stu-id="3a021-1046">True/False</span></span> |
| <span data-ttu-id="3a021-1047">ModelingFeatureList</span><span class="sxs-lookup"><span data-stu-id="3a021-1047">ModelingFeatureList</span></span> |<span data-ttu-id="3a021-1048">Liste de séparées par des virgules des toobe de noms de fonction utilisée dans la génération de recommandation hello, dans la recommandation de commande tooenhance hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-1048">Comma-separated list of feature names toobe used in hello recommendation build, in order tooenhance hello recommendation.</span></span> |<span data-ttu-id="3a021-1049">String</span><span class="sxs-lookup"><span data-stu-id="3a021-1049">String</span></span> |<span data-ttu-id="3a021-1050">Noms de fonctionnalités, des caractères de too512</span><span class="sxs-lookup"><span data-stu-id="3a021-1050">Feature names, up too512 chars</span></span> |
| <span data-ttu-id="3a021-1051">AllowColdItemPlacement</span><span class="sxs-lookup"><span data-stu-id="3a021-1051">AllowColdItemPlacement</span></span> |<span data-ttu-id="3a021-1052">Indique si la recommandation de hello doit également à orienter éléments froids via la similarité de la fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="3a021-1052">Indicates if hello recommendation should also push cold items via feature similarity.</span></span> |<span data-ttu-id="3a021-1053">Boolean</span><span class="sxs-lookup"><span data-stu-id="3a021-1053">Boolean</span></span> |<span data-ttu-id="3a021-1054">True/False</span><span class="sxs-lookup"><span data-stu-id="3a021-1054">True/False</span></span> |
| <span data-ttu-id="3a021-1055">EnableFeatureCorrelation</span><span class="sxs-lookup"><span data-stu-id="3a021-1055">EnableFeatureCorrelation</span></span> |<span data-ttu-id="3a021-1056">Indique si des caractéristiques peuvent être utilisées dans le raisonnement.</span><span class="sxs-lookup"><span data-stu-id="3a021-1056">Indicates if features can be used in reasoning.</span></span> |<span data-ttu-id="3a021-1057">Boolean</span><span class="sxs-lookup"><span data-stu-id="3a021-1057">Boolean</span></span> |<span data-ttu-id="3a021-1058">True/False</span><span class="sxs-lookup"><span data-stu-id="3a021-1058">True/False</span></span> |
| <span data-ttu-id="3a021-1059">ReasoningFeatureList</span><span class="sxs-lookup"><span data-stu-id="3a021-1059">ReasoningFeatureList</span></span> |<span data-ttu-id="3a021-1060">Liste de séparées par des virgules de fonctionnalité toobe de noms utilisé pour le raisonnement phrases (par exemple, les explications de recommandation).</span><span class="sxs-lookup"><span data-stu-id="3a021-1060">Comma-separated list of feature names toobe used for reasoning sentences (e.g. recommendation explanations).</span></span> |<span data-ttu-id="3a021-1061">String</span><span class="sxs-lookup"><span data-stu-id="3a021-1061">String</span></span> |<span data-ttu-id="3a021-1062">Noms de fonctionnalités, des caractères de too512</span><span class="sxs-lookup"><span data-stu-id="3a021-1062">Feature names, up too512 chars</span></span> |
| <span data-ttu-id="3a021-1063">EnableU2I</span><span class="sxs-lookup"><span data-stu-id="3a021-1063">EnableU2I</span></span> |<span data-ttu-id="3a021-1064">Autoriser l’alias hello personnalisé recommandation</span><span class="sxs-lookup"><span data-stu-id="3a021-1064">Allow hello personalized recommendation a.k.a.</span></span> <span data-ttu-id="3a021-1065">U2I (recommandations tooitem de l’utilisateur).</span><span class="sxs-lookup"><span data-stu-id="3a021-1065">U2I (user tooitem recommendations).</span></span> |<span data-ttu-id="3a021-1066">Boolean</span><span class="sxs-lookup"><span data-stu-id="3a021-1066">Boolean</span></span> |<span data-ttu-id="3a021-1067">Vrai/faux (Vrai par défaut)</span><span class="sxs-lookup"><span data-stu-id="3a021-1067">True/False (default true)</span></span> |

##### <a name="1114-fbt-build-parameters"></a><span data-ttu-id="3a021-1068">11.1.4.</span><span class="sxs-lookup"><span data-stu-id="3a021-1068">11.1.4.</span></span> <span data-ttu-id="3a021-1069">Paramètres de build FBT</span><span class="sxs-lookup"><span data-stu-id="3a021-1069">FBT build parameters</span></span>
<span data-ttu-id="3a021-1070">tableau de Hello ci-dessous illustre les paramètres de génération hello pour la build de la recommandation.</span><span class="sxs-lookup"><span data-stu-id="3a021-1070">hello table below depicts hello build parameters for recommendation build.</span></span>

| <span data-ttu-id="3a021-1071">Clé</span><span class="sxs-lookup"><span data-stu-id="3a021-1071">Key</span></span> | <span data-ttu-id="3a021-1072">Description</span><span class="sxs-lookup"><span data-stu-id="3a021-1072">Description</span></span> | <span data-ttu-id="3a021-1073">Type</span><span class="sxs-lookup"><span data-stu-id="3a021-1073">Type</span></span> | <span data-ttu-id="3a021-1074">Valeur valide (par défaut)</span><span class="sxs-lookup"><span data-stu-id="3a021-1074">Valid Value (Default)</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="3a021-1075">FbtSupportThreshold</span><span class="sxs-lookup"><span data-stu-id="3a021-1075">FbtSupportThreshold</span></span> |<span data-ttu-id="3a021-1076">Comment le modèle de hello classique est.</span><span class="sxs-lookup"><span data-stu-id="3a021-1076">How conservative hello model is.</span></span> <span data-ttu-id="3a021-1077">Nombre d’occurrences de collaboration de toobe éléments pris en compte pour la modélisation.</span><span class="sxs-lookup"><span data-stu-id="3a021-1077">Number of co-occurrences of items toobe considered for modeling.</span></span> |<span data-ttu-id="3a021-1078">Entier </span><span class="sxs-lookup"><span data-stu-id="3a021-1078">Integer</span></span> |<span data-ttu-id="3a021-1079">3-50 (6)</span><span class="sxs-lookup"><span data-stu-id="3a021-1079">3-50 (6)</span></span> |
| <span data-ttu-id="3a021-1080">FbtMaxItemSetSize</span><span class="sxs-lookup"><span data-stu-id="3a021-1080">FbtMaxItemSetSize</span></span> |<span data-ttu-id="3a021-1081">Limites hello nombre d’éléments dans un ensemble de fréquent.</span><span class="sxs-lookup"><span data-stu-id="3a021-1081">Bounds hello number of items in a frequent set.</span></span> |<span data-ttu-id="3a021-1082">Entier </span><span class="sxs-lookup"><span data-stu-id="3a021-1082">Integer</span></span> |<span data-ttu-id="3a021-1083">2-3 (2)</span><span class="sxs-lookup"><span data-stu-id="3a021-1083">2-3 (2)</span></span> |
| <span data-ttu-id="3a021-1084">FbtMinimalScore</span><span class="sxs-lookup"><span data-stu-id="3a021-1084">FbtMinimalScore</span></span> |<span data-ttu-id="3a021-1085">Score minimal un ensemble de fréquent ont dans toobe de commande inclus dans hello retourner des résultats.</span><span class="sxs-lookup"><span data-stu-id="3a021-1085">Minimal score that a frequent set should have in order toobe included in hello returned results.</span></span> <span data-ttu-id="3a021-1086">Bonjour supérieur Bonjour mieux.</span><span class="sxs-lookup"><span data-stu-id="3a021-1086">hello higher hello better.</span></span> |<span data-ttu-id="3a021-1087">Double</span><span class="sxs-lookup"><span data-stu-id="3a021-1087">Double</span></span> |<span data-ttu-id="3a021-1088">0 et plus (0)</span><span class="sxs-lookup"><span data-stu-id="3a021-1088">0 and above (0)</span></span> |
| <span data-ttu-id="3a021-1089">FbtSimilarityFunction</span><span class="sxs-lookup"><span data-stu-id="3a021-1089">FbtSimilarityFunction</span></span> |<span data-ttu-id="3a021-1090">Définit hello similarité fonction toobe utilisé par la génération de hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-1090">Defines hello similarity function toobe used by hello build.</span></span> <span data-ttu-id="3a021-1091">Favorise la finesse serendipity, collaboration occurrence favorise la prévisibilité et Jaccard est une bonne alliera hello deux.</span><span class="sxs-lookup"><span data-stu-id="3a021-1091">Lift favors serendipity, Co-occurrence favors predictability, and Jaccard is a nice compromise between hello two.</span></span> |<span data-ttu-id="3a021-1092">String</span><span class="sxs-lookup"><span data-stu-id="3a021-1092">String</span></span> |<span data-ttu-id="3a021-1093">cooccurrence, élévation, jaccard (élévation)</span><span class="sxs-lookup"><span data-stu-id="3a021-1093">cooccurrence, lift, jaccard (lift)</span></span> |

### <a name="112-trigger-a-recommendation-build"></a><span data-ttu-id="3a021-1094">11.2.</span><span class="sxs-lookup"><span data-stu-id="3a021-1094">11.2.</span></span> <span data-ttu-id="3a021-1095">Déclencher une build de recommandation</span><span class="sxs-lookup"><span data-stu-id="3a021-1095">Trigger a Recommendation Build</span></span>
  <span data-ttu-id="3a021-1096">Par défaut, cette API déclenche une build de modèle de recommandation.</span><span class="sxs-lookup"><span data-stu-id="3a021-1096">By default this API will trigger a recommendation model build.</span></span> <span data-ttu-id="3a021-1097">tootrigger un rang égal à générer (dans les fonctions de tooscore de commande), variante d’API de build hello avec le paramètre de type de build doit être utilisé.</span><span class="sxs-lookup"><span data-stu-id="3a021-1097">tootrigger a rank build (in order tooscore  features), hello build API variant with build type parameter should be used.</span></span>

| <span data-ttu-id="3a021-1098">Méthode HTTP</span><span class="sxs-lookup"><span data-stu-id="3a021-1098">HTTP Method</span></span> | <span data-ttu-id="3a021-1099">URI</span><span class="sxs-lookup"><span data-stu-id="3a021-1099">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-1100">POST</span><span class="sxs-lookup"><span data-stu-id="3a021-1100">POST</span></span> |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="3a021-1101">Exemple :</span><span class="sxs-lookup"><span data-stu-id="3a021-1101">Example:</span></span><br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&apiVersion=%271.0%27` |
| <span data-ttu-id="3a021-1102">HEADER</span><span class="sxs-lookup"><span data-stu-id="3a021-1102">HEADER</span></span> |<span data-ttu-id="3a021-1103">`"Content-Type", "text/xml"` (en cas d’envoi du corps de la requête)</span><span class="sxs-lookup"><span data-stu-id="3a021-1103">`"Content-Type", "text/xml"` (If sending Request Body)</span></span> |

| <span data-ttu-id="3a021-1104">Nom du paramètre</span><span class="sxs-lookup"><span data-stu-id="3a021-1104">Parameter Name</span></span> | <span data-ttu-id="3a021-1105">Valeurs valides</span><span class="sxs-lookup"><span data-stu-id="3a021-1105">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-1106">modelId</span><span class="sxs-lookup"><span data-stu-id="3a021-1106">modelId</span></span> |<span data-ttu-id="3a021-1107">Identificateur unique du modèle de hello</span><span class="sxs-lookup"><span data-stu-id="3a021-1107">Unique identifier of hello model</span></span> |
| <span data-ttu-id="3a021-1108">userDescription</span><span class="sxs-lookup"><span data-stu-id="3a021-1108">userDescription</span></span> |<span data-ttu-id="3a021-1109">Identificateur textuel du catalogue de hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-1109">Textual identifier of hello catalog.</span></span> <span data-ttu-id="3a021-1110">Notez que si vous utilisez des espaces, vous devez plutôt l'encoder avec %20.</span><span class="sxs-lookup"><span data-stu-id="3a021-1110">Note that if you use spaces you must encode it with %20 instead.</span></span> <span data-ttu-id="3a021-1111">Consultez l'exemple ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="3a021-1111">See example above.</span></span><br><span data-ttu-id="3a021-1112">Longueur maximale : 50</span><span class="sxs-lookup"><span data-stu-id="3a021-1112">Max length: 50</span></span> |
| <span data-ttu-id="3a021-1113">apiVersion</span><span class="sxs-lookup"><span data-stu-id="3a021-1113">apiVersion</span></span> |<span data-ttu-id="3a021-1114">1.0</span><span class="sxs-lookup"><span data-stu-id="3a021-1114">1.0</span></span> |
|  | |
| <span data-ttu-id="3a021-1115">Corps de la requête</span><span class="sxs-lookup"><span data-stu-id="3a021-1115">Request Body</span></span> |<span data-ttu-id="3a021-1116">Si vide build de hello sera exécuté avec des paramètres de build par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-1116">If left empty then hello build will be executed with hello default build parameters.</span></span><br><br><span data-ttu-id="3a021-1117">Si vous souhaitez que les paramètres de génération tooset hello, envoyer des paramètres de hello au format XML dans le corps hello comme hello suivant l’exemple.</span><span class="sxs-lookup"><span data-stu-id="3a021-1117">If you want tooset hello build parameters, send hello parameters as XML into hello body as in hello following sample.</span></span> <span data-ttu-id="3a021-1118">(Consultez la section hello « paramètres de génération » pour obtenir une explication des paramètres de hello.)`<NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance><EnableModelingInsights>true</EnableModelingInsights><UseFeaturesInModel>false</UseFeaturesInModel><ModelingFeatureList>feature_name_1,feature_name_2,...</ModelingFeatureList><AllowColdItemPlacement>false</AllowColdItemPlacement><EnableFeatureCorrelation>false</EnableFeatureCorrelation><ReasoningFeatureList>feature_name_a,feature_name_b,...</ReasoningFeatureList></BuildParametersList>`</span><span class="sxs-lookup"><span data-stu-id="3a021-1118">(See hello "Build parameters" section for an explanation of hello parameters.)`<NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance><EnableModelingInsights>true</EnableModelingInsights><UseFeaturesInModel>false</UseFeaturesInModel><ModelingFeatureList>feature_name_1,feature_name_2,...</ModelingFeatureList><AllowColdItemPlacement>false</AllowColdItemPlacement><EnableFeatureCorrelation>false</EnableFeatureCorrelation><ReasoningFeatureList>feature_name_a,feature_name_b,...</ReasoningFeatureList></BuildParametersList>`</span></span> |

<span data-ttu-id="3a021-1119">**Réponse**:</span><span class="sxs-lookup"><span data-stu-id="3a021-1119">**Response**:</span></span>

<span data-ttu-id="3a021-1120">Code d'état HTTP : 200</span><span class="sxs-lookup"><span data-stu-id="3a021-1120">HTTP Status code: 200</span></span>

<span data-ttu-id="3a021-1121">Il s'agit d'une API asynchrone.</span><span class="sxs-lookup"><span data-stu-id="3a021-1121">This is an asynchronous API.</span></span> <span data-ttu-id="3a021-1122">La réponse obtenue est un ID de build.</span><span class="sxs-lookup"><span data-stu-id="3a021-1122">You will get a build ID as a response.</span></span> <span data-ttu-id="3a021-1123">tooknow lors de la génération de hello est terminée, vous devez appeler l’API « Obtenir génère état d’un modèle » hello et localiser cette ID de build dans la réponse de hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-1123">tooknow when hello build has ended, you should call hello “Get Builds Status of a Model” API and locate this build ID in hello response.</span></span> <span data-ttu-id="3a021-1124">Notez qu’une build peut prendre de toohours minutes selon la taille de hello de données de hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-1124">Note that a build can take from minutes toohours depending on hello size of hello data.</span></span>

<span data-ttu-id="3a021-1125">Vous ne peut pas consommer recommandations jusqu'à ce que hello build se termine.</span><span class="sxs-lookup"><span data-stu-id="3a021-1125">You cannot consume recommendations till hello build ends.</span></span>

<span data-ttu-id="3a021-1126">État de build valide :</span><span class="sxs-lookup"><span data-stu-id="3a021-1126">Valid build status:</span></span>

* <span data-ttu-id="3a021-1127">Create : la demande de build a été créée.</span><span class="sxs-lookup"><span data-stu-id="3a021-1127">Create - Build request was created.</span></span>
* <span data-ttu-id="3a021-1128">Queued : la demande de build a été envoyée et mise en file d’attente.</span><span class="sxs-lookup"><span data-stu-id="3a021-1128">Queued - Build request was sent and it is queued.</span></span>
* <span data-ttu-id="3a021-1129">Building : la build est en cours.</span><span class="sxs-lookup"><span data-stu-id="3a021-1129">Building - Build is in progress.</span></span>
* <span data-ttu-id="3a021-1130">Success : la build a été correctement exécutée.</span><span class="sxs-lookup"><span data-stu-id="3a021-1130">Success - Build ended successfully.</span></span>
* <span data-ttu-id="3a021-1131">Error : la build s’est terminée par un échec.</span><span class="sxs-lookup"><span data-stu-id="3a021-1131">Error - Build ended with a failure.</span></span>
* <span data-ttu-id="3a021-1132">Cancelled : la build a été annulée.</span><span class="sxs-lookup"><span data-stu-id="3a021-1132">Cancelled - Build was cancelled.</span></span>
* <span data-ttu-id="3a021-1133">L’annulation - une demande d’annulation pour la build de hello a été envoyée.</span><span class="sxs-lookup"><span data-stu-id="3a021-1133">Cancelling - A cancel request for hello build was sent.</span></span>

<span data-ttu-id="3a021-1134">Notez cette build hello QU'ID accessible sous hello suivant le chemin d’accès :`Feed\entry\content\properties\Id`</span><span class="sxs-lookup"><span data-stu-id="3a021-1134">Note that hello build ID can be found under hello following path: `Feed\entry\content\properties\Id`</span></span>

<span data-ttu-id="3a021-1135">OData XML</span><span class="sxs-lookup"><span data-stu-id="3a021-1135">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Build a Model with RequestBody</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T08:56:34Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">BuildAModelEntity2</title>
    <updated>2014-10-05T08:56:34Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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

### <a name="113-trigger-build-recommendation-rank-or-fbt"></a><span data-ttu-id="3a021-1136">11.3.</span><span class="sxs-lookup"><span data-stu-id="3a021-1136">11.3.</span></span> <span data-ttu-id="3a021-1137">Déclenchement d'une build (recommandation, classement ou FBT)</span><span class="sxs-lookup"><span data-stu-id="3a021-1137">Trigger Build (Recommendation, Rank or FBT)</span></span>
| <span data-ttu-id="3a021-1138">Méthode HTTP</span><span class="sxs-lookup"><span data-stu-id="3a021-1138">HTTP Method</span></span> | <span data-ttu-id="3a021-1139">URI</span><span class="sxs-lookup"><span data-stu-id="3a021-1139">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-1140">POST</span><span class="sxs-lookup"><span data-stu-id="3a021-1140">POST</span></span> |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&buildType=%27<buildType>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="3a021-1141">Exemple :</span><span class="sxs-lookup"><span data-stu-id="3a021-1141">Example:</span></span><br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&buildType=%27Ranking%27&apiVersion=%271.0%27` |
| <span data-ttu-id="3a021-1142">HEADER</span><span class="sxs-lookup"><span data-stu-id="3a021-1142">HEADER</span></span> |<span data-ttu-id="3a021-1143">`"Content-Type", "text/xml"` (en cas d’envoi du corps de la requête)</span><span class="sxs-lookup"><span data-stu-id="3a021-1143">`"Content-Type", "text/xml"` (If sending Request Body)</span></span> |

| <span data-ttu-id="3a021-1144">Nom du paramètre</span><span class="sxs-lookup"><span data-stu-id="3a021-1144">Parameter Name</span></span> | <span data-ttu-id="3a021-1145">Valeurs valides</span><span class="sxs-lookup"><span data-stu-id="3a021-1145">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-1146">modelId</span><span class="sxs-lookup"><span data-stu-id="3a021-1146">modelId</span></span> |<span data-ttu-id="3a021-1147">Identificateur unique du modèle de hello</span><span class="sxs-lookup"><span data-stu-id="3a021-1147">Unique identifier of hello model</span></span> |
| <span data-ttu-id="3a021-1148">userDescription</span><span class="sxs-lookup"><span data-stu-id="3a021-1148">userDescription</span></span> |<span data-ttu-id="3a021-1149">Identificateur textuel du catalogue de hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-1149">Textual identifier of hello catalog.</span></span> <span data-ttu-id="3a021-1150">Notez que si vous utilisez des espaces, vous devez plutôt l'encoder avec %20.</span><span class="sxs-lookup"><span data-stu-id="3a021-1150">Note that if you use spaces you must encode it with %20 instead.</span></span> <span data-ttu-id="3a021-1151">Consultez l'exemple ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="3a021-1151">See example above.</span></span><br><span data-ttu-id="3a021-1152">Longueur maximale : 50</span><span class="sxs-lookup"><span data-stu-id="3a021-1152">Max length: 50</span></span> |
| <span data-ttu-id="3a021-1153">buildType</span><span class="sxs-lookup"><span data-stu-id="3a021-1153">buildType</span></span> |<span data-ttu-id="3a021-1154">Type de hello build tooinvoke :</span><span class="sxs-lookup"><span data-stu-id="3a021-1154">Type of hello build tooinvoke:</span></span> <br/> <span data-ttu-id="3a021-1155">- « Recommendation » pour une build de recommandation</span><span class="sxs-lookup"><span data-stu-id="3a021-1155">- 'Recommendation' for recommendation build</span></span> <br> <span data-ttu-id="3a021-1156">- « Ranking » pour une build de classement</span><span class="sxs-lookup"><span data-stu-id="3a021-1156">- 'Ranking' for rank build</span></span> <br/> <span data-ttu-id="3a021-1157"> : « Fbt » pour une build FBT</span><span class="sxs-lookup"><span data-stu-id="3a021-1157">- 'Fbt' for FBT build</span></span> |
| <span data-ttu-id="3a021-1158">apiVersion</span><span class="sxs-lookup"><span data-stu-id="3a021-1158">apiVersion</span></span> |<span data-ttu-id="3a021-1159">1.0</span><span class="sxs-lookup"><span data-stu-id="3a021-1159">1.0</span></span> |
|  | |
| <span data-ttu-id="3a021-1160">Corps de la requête</span><span class="sxs-lookup"><span data-stu-id="3a021-1160">Request Body</span></span> |<span data-ttu-id="3a021-1161">Si vide build de hello sera exécuté avec des paramètres de build par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-1161">If left empty then hello build will be executed with hello default build parameters.</span></span><br><br><span data-ttu-id="3a021-1162">Si vous souhaitez que les paramètres de génération tooset, les envoyer en tant que XML dans corps hello comme hello suivant l’exemple.</span><span class="sxs-lookup"><span data-stu-id="3a021-1162">If you want tooset build parameters, send them as XML into hello body like in hello following sample.</span></span> <span data-ttu-id="3a021-1163">(Consultez la section hello « paramètres de génération » pour une explication et une liste complète des paramètres de hello.)`<BuildParametersList><NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance></BuildParametersList>`</span><span class="sxs-lookup"><span data-stu-id="3a021-1163">(See hello "Build parameters" section for an explanation and full list of hello parameters.)`<BuildParametersList><NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance></BuildParametersList>`</span></span> |

<span data-ttu-id="3a021-1164">**Réponse**:</span><span class="sxs-lookup"><span data-stu-id="3a021-1164">**Response**:</span></span>

<span data-ttu-id="3a021-1165">Code d'état HTTP : 200</span><span class="sxs-lookup"><span data-stu-id="3a021-1165">HTTP Status code: 200</span></span>

<span data-ttu-id="3a021-1166">Il s'agit d'une API asynchrone.</span><span class="sxs-lookup"><span data-stu-id="3a021-1166">This is an asynchronous API.</span></span> <span data-ttu-id="3a021-1167">La réponse obtenue est un ID de build.</span><span class="sxs-lookup"><span data-stu-id="3a021-1167">You will get a build ID as a response.</span></span> <span data-ttu-id="3a021-1168">tooknow lors de la génération de hello est terminée, vous devez appeler l’API « Obtenir génère état d’un modèle » hello et localiser cette ID de build dans la réponse de hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-1168">tooknow when hello build has ended, you should call hello “Get Builds Status of a Model” API and locate this build ID in hello response.</span></span> <span data-ttu-id="3a021-1169">Notez qu’une build peut prendre de toohours minutes selon la taille de hello de données de hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-1169">Note that a build can take from minutes toohours depending on hello size of hello data.</span></span>

<span data-ttu-id="3a021-1170">Vous ne peut pas consommer recommandations jusqu'à ce que hello build se termine.</span><span class="sxs-lookup"><span data-stu-id="3a021-1170">You cannot consume recommendations till hello build ends.</span></span>

<span data-ttu-id="3a021-1171">État de build valide :</span><span class="sxs-lookup"><span data-stu-id="3a021-1171">Valid build status:</span></span>

* <span data-ttu-id="3a021-1172">Create : le modèle a été créé.</span><span class="sxs-lookup"><span data-stu-id="3a021-1172">Create - Model was created.</span></span>
* <span data-ttu-id="3a021-1173">Queued : la build de modèle a été déclenchée et mise en file d’attente.</span><span class="sxs-lookup"><span data-stu-id="3a021-1173">Queued - Model build was triggered and it is queued.</span></span>
* <span data-ttu-id="3a021-1174">Building : le modèle est en cours de génération.</span><span class="sxs-lookup"><span data-stu-id="3a021-1174">Building - Model is being built.</span></span>
* <span data-ttu-id="3a021-1175">Success : la build a été correctement exécutée.</span><span class="sxs-lookup"><span data-stu-id="3a021-1175">Success - Build ended successfully.</span></span>
* <span data-ttu-id="3a021-1176">Error : la build s’est terminée par un échec.</span><span class="sxs-lookup"><span data-stu-id="3a021-1176">Error - Build ended with a failure.</span></span>
* <span data-ttu-id="3a021-1177">Cancelled : la build a été annulée.</span><span class="sxs-lookup"><span data-stu-id="3a021-1177">Cancelled - Build was cancelled.</span></span>
* <span data-ttu-id="3a021-1178">Cancelling : la build est en cours d’annulation.</span><span class="sxs-lookup"><span data-stu-id="3a021-1178">Cancelling - Build is being cancelled.</span></span>

<span data-ttu-id="3a021-1179">Notez cette build hello QU'ID accessible sous hello suivant le chemin d’accès :`Feed\entry\content\properties\Id`</span><span class="sxs-lookup"><span data-stu-id="3a021-1179">Note that hello build ID can be found under hello following path: `Feed\entry\content\properties\Id`</span></span>

<span data-ttu-id="3a021-1180">OData XML</span><span class="sxs-lookup"><span data-stu-id="3a021-1180">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Build a Model with RequestBody</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T08:56:34Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">BuildAModelEntity2</title>
    <updated>2014-10-05T08:56:34Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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




### <a name="114-get-builds-status-of-a-model"></a><span data-ttu-id="3a021-1181">11.4.</span><span class="sxs-lookup"><span data-stu-id="3a021-1181">11.4.</span></span> <span data-ttu-id="3a021-1182">Obtention de l'état de build d'un modèle</span><span class="sxs-lookup"><span data-stu-id="3a021-1182">Get Builds Status of a Model</span></span>
<span data-ttu-id="3a021-1183">Récupère les builds et leur état pour un modèle spécifié.</span><span class="sxs-lookup"><span data-stu-id="3a021-1183">Retrieves builds and their status for a specified model.</span></span>

| <span data-ttu-id="3a021-1184">Méthode HTTP</span><span class="sxs-lookup"><span data-stu-id="3a021-1184">HTTP Method</span></span> | <span data-ttu-id="3a021-1185">URI</span><span class="sxs-lookup"><span data-stu-id="3a021-1185">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-1186">GET</span><span class="sxs-lookup"><span data-stu-id="3a021-1186">GET</span></span> |`<rootURI>/GetModelBuildsStatus?modelId=%27<modelId>%27&onlyLastBuild=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="3a021-1187">Exemple :</span><span class="sxs-lookup"><span data-stu-id="3a021-1187">Example:</span></span><br>`<rootURI>/GetModelBuildsStatus?modelId=%279559872f-7a53-4076-a3c7-19d9385c1265%27&onlyLastBuild=true&apiVersion=%271.0%27` |

| <span data-ttu-id="3a021-1188">Nom du paramètre</span><span class="sxs-lookup"><span data-stu-id="3a021-1188">Parameter Name</span></span> | <span data-ttu-id="3a021-1189">Valeurs valides</span><span class="sxs-lookup"><span data-stu-id="3a021-1189">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-1190">modelId</span><span class="sxs-lookup"><span data-stu-id="3a021-1190">modelId</span></span> |<span data-ttu-id="3a021-1191">Identificateur unique du modèle de hello</span><span class="sxs-lookup"><span data-stu-id="3a021-1191">Unique identifier of hello model</span></span> |
| <span data-ttu-id="3a021-1192">onlyLastBuild</span><span class="sxs-lookup"><span data-stu-id="3a021-1192">onlyLastBuild</span></span> |<span data-ttu-id="3a021-1193">Indique si tooreturn tous hello générer l’historique du modèle de hello ou état hello seule de la build la plus récente hello</span><span class="sxs-lookup"><span data-stu-id="3a021-1193">Indicates whether tooreturn all hello build history of hello model or only hello status of hello most recent build</span></span> |
| <span data-ttu-id="3a021-1194">apiVersion</span><span class="sxs-lookup"><span data-stu-id="3a021-1194">apiVersion</span></span> |<span data-ttu-id="3a021-1195">1.0</span><span class="sxs-lookup"><span data-stu-id="3a021-1195">1.0</span></span> |

<span data-ttu-id="3a021-1196">**Réponse**:</span><span class="sxs-lookup"><span data-stu-id="3a021-1196">**Response**:</span></span>

<span data-ttu-id="3a021-1197">Code d'état HTTP : 200</span><span class="sxs-lookup"><span data-stu-id="3a021-1197">HTTP Status code: 200</span></span>

<span data-ttu-id="3a021-1198">réponse de Hello inclut une entrée par une build.</span><span class="sxs-lookup"><span data-stu-id="3a021-1198">hello response includes one entry per build.</span></span> <span data-ttu-id="3a021-1199">Chaque entrée a hello données suivantes :</span><span class="sxs-lookup"><span data-stu-id="3a021-1199">Each entry has hello following data:</span></span>

* <span data-ttu-id="3a021-1200">`feed/entry/content/properties/UserName`-Nom d’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-1200">`feed/entry/content/properties/UserName` - Name of hello user.</span></span>
* <span data-ttu-id="3a021-1201">`feed/entry/content/properties/ModelName`-Nom du modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-1201">`feed/entry/content/properties/ModelName` - Name of hello model.</span></span>
* <span data-ttu-id="3a021-1202">`feed/entry/content/properties/ModelId` : identificateur unique du modèle.</span><span class="sxs-lookup"><span data-stu-id="3a021-1202">`feed/entry/content/properties/ModelId` - Model unique identifier.</span></span>
* <span data-ttu-id="3a021-1203">`feed/entry/content/properties/IsDeployed`-Génération de hello est déployé (aussi appelé)</span><span class="sxs-lookup"><span data-stu-id="3a021-1203">`feed/entry/content/properties/IsDeployed` - Whether hello build is deployed (a.k.a.</span></span> <span data-ttu-id="3a021-1204">(c’est-à-dire active).</span><span class="sxs-lookup"><span data-stu-id="3a021-1204">active build).</span></span>
* <span data-ttu-id="3a021-1205">`feed/entry/content/properties/BuildId` : identificateur unique de la build.</span><span class="sxs-lookup"><span data-stu-id="3a021-1205">`feed/entry/content/properties/BuildId` - Build unique identifier.</span></span>
* <span data-ttu-id="3a021-1206">`feed/entry/content/properties/BuildType`-Type de build de hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-1206">`feed/entry/content/properties/BuildType` - Type of hello build.</span></span>
* <span data-ttu-id="3a021-1207">`feed/entry/content/properties/Status` : état de la build.</span><span class="sxs-lookup"><span data-stu-id="3a021-1207">`feed/entry/content/properties/Status` - Build status.</span></span> <span data-ttu-id="3a021-1208">Peut être une des manières suivantes les hello : erreur, construction, en file d’attente, annulation, annulé, la réussite.</span><span class="sxs-lookup"><span data-stu-id="3a021-1208">Can be one of hello following: Error, Building, Queued, Cancelling, Cancelled, Success.</span></span>
* <span data-ttu-id="3a021-1209">`feed/entry/content/properties/StatusMessage`-Message d’état détaillée (s’applique uniquement les États toospecific).</span><span class="sxs-lookup"><span data-stu-id="3a021-1209">`feed/entry/content/properties/StatusMessage` - Detailed status message (applies only toospecific states).</span></span>
* <span data-ttu-id="3a021-1210">`feed/entry/content/properties/Progress` : progression de l’exécution de la build (%).</span><span class="sxs-lookup"><span data-stu-id="3a021-1210">`feed/entry/content/properties/Progress` - Build progress (%).</span></span>
* <span data-ttu-id="3a021-1211">`feed/entry/content/properties/StartTime` : heure de début de l’exécution de la build.</span><span class="sxs-lookup"><span data-stu-id="3a021-1211">`feed/entry/content/properties/StartTime` - Build start time.</span></span>
* <span data-ttu-id="3a021-1212">`feed/entry/content/properties/EndTime` : heure de fin de l’exécution de la build.</span><span class="sxs-lookup"><span data-stu-id="3a021-1212">`feed/entry/content/properties/EndTime` - Build end time.</span></span>
* <span data-ttu-id="3a021-1213">`feed/entry/content/properties/ExecutionTime` : durée de la build.</span><span class="sxs-lookup"><span data-stu-id="3a021-1213">`feed/entry/content/properties/ExecutionTime` - Build duration.</span></span>
* <span data-ttu-id="3a021-1214">`feed/entry/content/properties/ProgressStep`-Des détails concernant la phase actuelle de hello d’une build en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="3a021-1214">`feed/entry/content/properties/ProgressStep` - Details about hello current stage of a build in progress.</span></span>

<span data-ttu-id="3a021-1215">État de build valide :</span><span class="sxs-lookup"><span data-stu-id="3a021-1215">Valid build status:</span></span>

* <span data-ttu-id="3a021-1216">Created : l’entrée de demande de build a été créée.</span><span class="sxs-lookup"><span data-stu-id="3a021-1216">Created - Build request entry was created.</span></span>
* <span data-ttu-id="3a021-1217">Queued : la demande de build a été déclenchée et mise en file attente.</span><span class="sxs-lookup"><span data-stu-id="3a021-1217">Queued - Build request was triggered and it is queued.</span></span>
* <span data-ttu-id="3a021-1218">Building : la build est en cours.</span><span class="sxs-lookup"><span data-stu-id="3a021-1218">Building - Build is in process.</span></span>
* <span data-ttu-id="3a021-1219">Success : la build a été correctement exécutée.</span><span class="sxs-lookup"><span data-stu-id="3a021-1219">Success - Build ended successfully.</span></span>
* <span data-ttu-id="3a021-1220">Error : la build s’est terminée par un échec.</span><span class="sxs-lookup"><span data-stu-id="3a021-1220">Error - Build ended with a failure.</span></span>
* <span data-ttu-id="3a021-1221">Cancelled : la build a été annulée.</span><span class="sxs-lookup"><span data-stu-id="3a021-1221">Cancelled - Build was cancelled.</span></span>
* <span data-ttu-id="3a021-1222">Cancelling : la build est en cours d’annulation.</span><span class="sxs-lookup"><span data-stu-id="3a021-1222">Cancelling - Build is being cancelled.</span></span>

<span data-ttu-id="3a021-1223">Valeurs valides pour le type de build :</span><span class="sxs-lookup"><span data-stu-id="3a021-1223">Valid values for build type:</span></span>

* <span data-ttu-id="3a021-1224">Rank - Build de classement.</span><span class="sxs-lookup"><span data-stu-id="3a021-1224">Rank - Rank build.</span></span>
* <span data-ttu-id="3a021-1225">Recommendation - Build de recommandation.</span><span class="sxs-lookup"><span data-stu-id="3a021-1225">Recommendation - Recommendation build.</span></span>

<span data-ttu-id="3a021-1226">OData XML</span><span class="sxs-lookup"><span data-stu-id="3a021-1226">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get builds status of a model</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-11-05T17:51:10Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetBuildsStatusEntity</title>
            <updated>2014-11-05T17:51:10Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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


### <a name="115-get-builds-status"></a><span data-ttu-id="3a021-1227">11.5.</span><span class="sxs-lookup"><span data-stu-id="3a021-1227">11.5.</span></span> <span data-ttu-id="3a021-1228">Obtention de l'état de build</span><span class="sxs-lookup"><span data-stu-id="3a021-1228">Get Builds Status</span></span>
<span data-ttu-id="3a021-1229">Récupère les états de build de tous les modèles d'un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="3a021-1229">Retrieves build statuses of all models of a user.</span></span>

| <span data-ttu-id="3a021-1230">Méthode HTTP</span><span class="sxs-lookup"><span data-stu-id="3a021-1230">HTTP Method</span></span> | <span data-ttu-id="3a021-1231">URI</span><span class="sxs-lookup"><span data-stu-id="3a021-1231">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-1232">GET</span><span class="sxs-lookup"><span data-stu-id="3a021-1232">GET</span></span> |`<rootURI>/GetUserBuildsStatus?onlyLastBuilds=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="3a021-1233">Exemple :</span><span class="sxs-lookup"><span data-stu-id="3a021-1233">Example:</span></span><br>`<rootURI>/GetUserBuildsStatus?onlyLastBuilds=true&apiVersion=%271.0%27` |

| <span data-ttu-id="3a021-1234">Nom du paramètre</span><span class="sxs-lookup"><span data-stu-id="3a021-1234">Parameter Name</span></span> | <span data-ttu-id="3a021-1235">Valeurs valides</span><span class="sxs-lookup"><span data-stu-id="3a021-1235">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-1236">onlyLastBuild</span><span class="sxs-lookup"><span data-stu-id="3a021-1236">onlyLastBuild</span></span> |<span data-ttu-id="3a021-1237">Indique si tooreturn tous hello générer l’historique du modèle de hello ou état hello seule de la build la plus récente hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-1237">Indicates whether tooreturn all hello build history of hello model or only hello status of hello most recent build.</span></span> |
| <span data-ttu-id="3a021-1238">apiVersion</span><span class="sxs-lookup"><span data-stu-id="3a021-1238">apiVersion</span></span> |<span data-ttu-id="3a021-1239">1.0</span><span class="sxs-lookup"><span data-stu-id="3a021-1239">1.0</span></span> |

<span data-ttu-id="3a021-1240">**Réponse**:</span><span class="sxs-lookup"><span data-stu-id="3a021-1240">**Response**:</span></span>

<span data-ttu-id="3a021-1241">Code d'état HTTP : 200</span><span class="sxs-lookup"><span data-stu-id="3a021-1241">HTTP Status code: 200</span></span>

<span data-ttu-id="3a021-1242">réponse de Hello inclut une entrée par une build.</span><span class="sxs-lookup"><span data-stu-id="3a021-1242">hello response includes one entry per build.</span></span> <span data-ttu-id="3a021-1243">Chaque entrée a hello données suivantes :</span><span class="sxs-lookup"><span data-stu-id="3a021-1243">Each entry has hello following data:</span></span>

* <span data-ttu-id="3a021-1244">`feed/entry/content/properties/UserName`-Nom d’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-1244">`feed/entry/content/properties/UserName` - Name of hello user.</span></span>
* <span data-ttu-id="3a021-1245">`feed/entry/content/properties/ModelName`-Nom du modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-1245">`feed/entry/content/properties/ModelName` - Name of hello model.</span></span>
* <span data-ttu-id="3a021-1246">`feed/entry/content/properties/ModelId` : identificateur unique du modèle.</span><span class="sxs-lookup"><span data-stu-id="3a021-1246">`feed/entry/content/properties/ModelId` - Model unique identifier.</span></span>
* <span data-ttu-id="3a021-1247">`feed/entry/content/properties/IsDeployed`-Si la génération de hello est déployée.</span><span class="sxs-lookup"><span data-stu-id="3a021-1247">`feed/entry/content/properties/IsDeployed` - Whether hello build is deployed.</span></span>
* <span data-ttu-id="3a021-1248">`feed/entry/content/properties/BuildId` : identificateur unique de la build.</span><span class="sxs-lookup"><span data-stu-id="3a021-1248">`feed/entry/content/properties/BuildId` - Build unique identifier.</span></span>
* <span data-ttu-id="3a021-1249">`feed/entry/content/properties/BuildType`-Type de build de hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-1249">`feed/entry/content/properties/BuildType` - Type of hello build.</span></span>
* <span data-ttu-id="3a021-1250">`feed/entry/content/properties/Status` : état de la build.</span><span class="sxs-lookup"><span data-stu-id="3a021-1250">`feed/entry/content/properties/Status` - Build status.</span></span> <span data-ttu-id="3a021-1251">Peut être une des manières suivantes les hello : erreur, construction, en file d’attente, annulé, annulation, réussite.</span><span class="sxs-lookup"><span data-stu-id="3a021-1251">Can be one of hello following: Error, Building, Queued, Cancelled, Cancelling, Success.</span></span>
* <span data-ttu-id="3a021-1252">`feed/entry/content/properties/StatusMessage`-Message d’état détaillée (s’applique uniquement les États toospecific).</span><span class="sxs-lookup"><span data-stu-id="3a021-1252">`feed/entry/content/properties/StatusMessage` - Detailed status message (applies only toospecific states).</span></span>
* <span data-ttu-id="3a021-1253">`feed/entry/content/properties/Progress` : progression de l’exécution de la build (%).</span><span class="sxs-lookup"><span data-stu-id="3a021-1253">`feed/entry/content/properties/Progress` - Build progress (%).</span></span>
* <span data-ttu-id="3a021-1254">`feed/entry/content/properties/StartTime` : heure de début de l’exécution de la build.</span><span class="sxs-lookup"><span data-stu-id="3a021-1254">`feed/entry/content/properties/StartTime` - Build start time.</span></span>
* <span data-ttu-id="3a021-1255">`feed/entry/content/properties/EndTime` : heure de fin de l’exécution de la build.</span><span class="sxs-lookup"><span data-stu-id="3a021-1255">`feed/entry/content/properties/EndTime` - Build end time.</span></span>
* <span data-ttu-id="3a021-1256">`feed/entry/content/properties/ExecutionTime` : durée de la build.</span><span class="sxs-lookup"><span data-stu-id="3a021-1256">`feed/entry/content/properties/ExecutionTime` - Build duration.</span></span>
* <span data-ttu-id="3a021-1257">`feed/entry/content/properties/ProgressStep`-Des détails concernant la phase actuelle de hello d’une build en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="3a021-1257">`feed/entry/content/properties/ProgressStep` - Details about hello current stage of a build in progress.</span></span>

<span data-ttu-id="3a021-1258">État de build valide :</span><span class="sxs-lookup"><span data-stu-id="3a021-1258">Valid build status:</span></span>

* <span data-ttu-id="3a021-1259">Created : l’entrée de demande de build a été créée.</span><span class="sxs-lookup"><span data-stu-id="3a021-1259">Created - Build request entry was created.</span></span>
* <span data-ttu-id="3a021-1260">Queued : la demande de build a été déclenchée et mise en file attente.</span><span class="sxs-lookup"><span data-stu-id="3a021-1260">Queued - Build request was triggered and it is queued.</span></span>
* <span data-ttu-id="3a021-1261">Building : la build est en cours.</span><span class="sxs-lookup"><span data-stu-id="3a021-1261">Building - Build is in process.</span></span>
* <span data-ttu-id="3a021-1262">Success : la build a été correctement exécutée.</span><span class="sxs-lookup"><span data-stu-id="3a021-1262">Success - Build ended successfully.</span></span>
* <span data-ttu-id="3a021-1263">Error : la build s’est terminée par un échec.</span><span class="sxs-lookup"><span data-stu-id="3a021-1263">Error - Build ended with a failure.</span></span>
* <span data-ttu-id="3a021-1264">Cancelled : la build a été annulée.</span><span class="sxs-lookup"><span data-stu-id="3a021-1264">Cancelled - Build was cancelled.</span></span>
* <span data-ttu-id="3a021-1265">Cancelling : la build est en cours d’annulation.</span><span class="sxs-lookup"><span data-stu-id="3a021-1265">Cancelling - Build is being cancelled.</span></span>

<span data-ttu-id="3a021-1266">Valeurs valides pour le type de build :</span><span class="sxs-lookup"><span data-stu-id="3a021-1266">Valid values for build type:</span></span>

* <span data-ttu-id="3a021-1267">Rank - Build de classement.</span><span class="sxs-lookup"><span data-stu-id="3a021-1267">Rank - Rank build.</span></span>
* <span data-ttu-id="3a021-1268">Recommendation - Build de recommandation.</span><span class="sxs-lookup"><span data-stu-id="3a021-1268">Recommendation - Recommendation build.</span></span>

<span data-ttu-id="3a021-1269">OData XML</span><span class="sxs-lookup"><span data-stu-id="3a021-1269">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get builds status of a user</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-11-05T18:41:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetBuildsStatusEntity</title>
            <updated>2014-11-05T18:41:21Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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


### <a name="116-delete-build"></a><span data-ttu-id="3a021-1270">11.6.</span><span class="sxs-lookup"><span data-stu-id="3a021-1270">11.6.</span></span> <span data-ttu-id="3a021-1271">Suppression de build</span><span class="sxs-lookup"><span data-stu-id="3a021-1271">Delete Build</span></span>
<span data-ttu-id="3a021-1272">Supprime une build.</span><span class="sxs-lookup"><span data-stu-id="3a021-1272">Deletes a build.</span></span>

<span data-ttu-id="3a021-1273">REMARQUE : </span><span class="sxs-lookup"><span data-stu-id="3a021-1273">NOTE:</span></span> <br><span data-ttu-id="3a021-1274">Vous ne pouvez pas supprimer une build active.</span><span class="sxs-lookup"><span data-stu-id="3a021-1274">You cannot delete an active build.</span></span> <span data-ttu-id="3a021-1275">le modèle Hello doit être mis à jour tooa autre active build avant de le supprimer.</span><span class="sxs-lookup"><span data-stu-id="3a021-1275">hello model should be updated tooa different active build before you delete it.</span></span><br><span data-ttu-id="3a021-1276">Vous ne pouvez pas supprimer une build en cours d'exécution.</span><span class="sxs-lookup"><span data-stu-id="3a021-1276">You cannot delete an in-progress build.</span></span> <span data-ttu-id="3a021-1277">Vous devez annuler les build hello tout d’abord en appelant <strong>Annuler Build</strong>.</span><span class="sxs-lookup"><span data-stu-id="3a021-1277">You should cancel hello build first by calling <strong>Cancel Build</strong>.</span></span>

| <span data-ttu-id="3a021-1278">Méthode HTTP</span><span class="sxs-lookup"><span data-stu-id="3a021-1278">HTTP Method</span></span> | <span data-ttu-id="3a021-1279">URI</span><span class="sxs-lookup"><span data-stu-id="3a021-1279">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-1280">SUPPRIMER</span><span class="sxs-lookup"><span data-stu-id="3a021-1280">DELETE</span></span> |`<rootURI>/DeleteBuild?buildId=%27<buildId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="3a021-1281">Exemple :</span><span class="sxs-lookup"><span data-stu-id="3a021-1281">Example:</span></span><br>`<rootURI>/DeleteBuild?buildId=%271500068%27&apiVersion=%271.0%27` |

| <span data-ttu-id="3a021-1282">Nom du paramètre</span><span class="sxs-lookup"><span data-stu-id="3a021-1282">Parameter Name</span></span> | <span data-ttu-id="3a021-1283">Valeurs valides</span><span class="sxs-lookup"><span data-stu-id="3a021-1283">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-1284">buildId</span><span class="sxs-lookup"><span data-stu-id="3a021-1284">buildId</span></span> |<span data-ttu-id="3a021-1285">Identificateur unique de la génération de hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-1285">Unique identifier of hello build.</span></span> |
| <span data-ttu-id="3a021-1286">apiVersion</span><span class="sxs-lookup"><span data-stu-id="3a021-1286">apiVersion</span></span> |<span data-ttu-id="3a021-1287">1.0</span><span class="sxs-lookup"><span data-stu-id="3a021-1287">1.0</span></span> |

<span data-ttu-id="3a021-1288">**Réponse :**</span><span class="sxs-lookup"><span data-stu-id="3a021-1288">**Response:**</span></span>

<span data-ttu-id="3a021-1289">Code d'état HTTP : 200</span><span class="sxs-lookup"><span data-stu-id="3a021-1289">HTTP Status code: 200</span></span>

### <a name="117-cancel-build"></a><span data-ttu-id="3a021-1290">11.7.</span><span class="sxs-lookup"><span data-stu-id="3a021-1290">11.7.</span></span> <span data-ttu-id="3a021-1291">Annulation de build</span><span class="sxs-lookup"><span data-stu-id="3a021-1291">Cancel Build</span></span>
<span data-ttu-id="3a021-1292">Annule une build avec l'état Building.</span><span class="sxs-lookup"><span data-stu-id="3a021-1292">Cancels a build that is in building status.</span></span>

| <span data-ttu-id="3a021-1293">Méthode HTTP</span><span class="sxs-lookup"><span data-stu-id="3a021-1293">HTTP Method</span></span> | <span data-ttu-id="3a021-1294">URI</span><span class="sxs-lookup"><span data-stu-id="3a021-1294">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-1295">PUT</span><span class="sxs-lookup"><span data-stu-id="3a021-1295">PUT</span></span> |`<rootURI>/CancelBuild?buildId=%27<buildId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="3a021-1296">Exemple :</span><span class="sxs-lookup"><span data-stu-id="3a021-1296">Example:</span></span><br>`<rootURI>/CancelBuild?buildId=%271500076%27&apiVersion=%271.0%27` |

| <span data-ttu-id="3a021-1297">Nom du paramètre</span><span class="sxs-lookup"><span data-stu-id="3a021-1297">Parameter Name</span></span> | <span data-ttu-id="3a021-1298">Valeurs valides</span><span class="sxs-lookup"><span data-stu-id="3a021-1298">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-1299">buildId</span><span class="sxs-lookup"><span data-stu-id="3a021-1299">buildId</span></span> |<span data-ttu-id="3a021-1300">Identificateur unique de la génération de hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-1300">Unique identifier of hello build.</span></span> |
| <span data-ttu-id="3a021-1301">apiVersion</span><span class="sxs-lookup"><span data-stu-id="3a021-1301">apiVersion</span></span> |<span data-ttu-id="3a021-1302">1.0</span><span class="sxs-lookup"><span data-stu-id="3a021-1302">1.0</span></span> |

<span data-ttu-id="3a021-1303">**Réponse :**</span><span class="sxs-lookup"><span data-stu-id="3a021-1303">**Response:**</span></span>

<span data-ttu-id="3a021-1304">Code d'état HTTP : 200</span><span class="sxs-lookup"><span data-stu-id="3a021-1304">HTTP Status code: 200</span></span>

### <a name="118-get-build-parameters"></a><span data-ttu-id="3a021-1305">11.8.</span><span class="sxs-lookup"><span data-stu-id="3a021-1305">11.8.</span></span> <span data-ttu-id="3a021-1306">Obtention des paramètres de build</span><span class="sxs-lookup"><span data-stu-id="3a021-1306">Get Build Parameters</span></span>
<span data-ttu-id="3a021-1307">Récupère les paramètres de build.</span><span class="sxs-lookup"><span data-stu-id="3a021-1307">Retrieves build parameters.</span></span>

| <span data-ttu-id="3a021-1308">Méthode HTTP</span><span class="sxs-lookup"><span data-stu-id="3a021-1308">HTTP Method</span></span> | <span data-ttu-id="3a021-1309">URI</span><span class="sxs-lookup"><span data-stu-id="3a021-1309">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-1310">GET</span><span class="sxs-lookup"><span data-stu-id="3a021-1310">GET</span></span> |`<rootURI>/GetBuildParameters?buildId=%27<buildId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="3a021-1311">Exemple :</span><span class="sxs-lookup"><span data-stu-id="3a021-1311">Example:</span></span><br>`<rootURI>/GetBuildParameters?buildId=%271000653%27&apiVersion=%271.0%27` |

| <span data-ttu-id="3a021-1312">Nom du paramètre</span><span class="sxs-lookup"><span data-stu-id="3a021-1312">Parameter Name</span></span> | <span data-ttu-id="3a021-1313">Valeurs valides</span><span class="sxs-lookup"><span data-stu-id="3a021-1313">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-1314">buildId</span><span class="sxs-lookup"><span data-stu-id="3a021-1314">buildId</span></span> |<span data-ttu-id="3a021-1315">Identificateur unique de la génération de hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-1315">Unique identifier of hello build.</span></span> |
| <span data-ttu-id="3a021-1316">apiVersion</span><span class="sxs-lookup"><span data-stu-id="3a021-1316">apiVersion</span></span> |<span data-ttu-id="3a021-1317">1.0</span><span class="sxs-lookup"><span data-stu-id="3a021-1317">1.0</span></span> |

<span data-ttu-id="3a021-1318">**Réponse :**</span><span class="sxs-lookup"><span data-stu-id="3a021-1318">**Response:**</span></span>

<span data-ttu-id="3a021-1319">Code d'état HTTP : 200</span><span class="sxs-lookup"><span data-stu-id="3a021-1319">HTTP Status code: 200</span></span>

<span data-ttu-id="3a021-1320">Cette API retourne une collection d'éléments clé/valeur.</span><span class="sxs-lookup"><span data-stu-id="3a021-1320">This API returns a collection of key/value elements.</span></span> <span data-ttu-id="3a021-1321">Chaque élément représente un paramètre et sa valeur :</span><span class="sxs-lookup"><span data-stu-id="3a021-1321">Each element represents a parameter and its value:</span></span>

* <span data-ttu-id="3a021-1322">`feed/entry/content/properties/Key` : nom du paramètre de la build.</span><span class="sxs-lookup"><span data-stu-id="3a021-1322">`feed/entry/content/properties/Key` - Build parameter name.</span></span>
* <span data-ttu-id="3a021-1323">`feed/entry/content/properties/Value` : valeur du paramètre de la build.</span><span class="sxs-lookup"><span data-stu-id="3a021-1323">`feed/entry/content/properties/Value` - Build parameter value.</span></span>

<span data-ttu-id="3a021-1324">tableau Hello ci-dessous représente la valeur hello représentant chaque clé.</span><span class="sxs-lookup"><span data-stu-id="3a021-1324">hello table below depicts hello value that each key represents.</span></span>

| <span data-ttu-id="3a021-1325">Clé</span><span class="sxs-lookup"><span data-stu-id="3a021-1325">Key</span></span> | <span data-ttu-id="3a021-1326">Description</span><span class="sxs-lookup"><span data-stu-id="3a021-1326">Description</span></span> | <span data-ttu-id="3a021-1327">Type</span><span class="sxs-lookup"><span data-stu-id="3a021-1327">Type</span></span> | <span data-ttu-id="3a021-1328">Valeur valide</span><span class="sxs-lookup"><span data-stu-id="3a021-1328">Valid Value</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="3a021-1329">NumberOfModelIterations</span><span class="sxs-lookup"><span data-stu-id="3a021-1329">NumberOfModelIterations</span></span> |<span data-ttu-id="3a021-1330">nombre de Hello d’itérations hello modèle fonctionne est reflétée par hello globale de calcul hello heure et la précision du modèle.</span><span class="sxs-lookup"><span data-stu-id="3a021-1330">hello number of iterations hello model performs is reflected by hello overall compute time and hello model accuracy.</span></span> <span data-ttu-id="3a021-1331">Hello hello nombre élevé, vous obtiendrez améliorer la précision de hello, mais hello de calcul prend plus de temps.</span><span class="sxs-lookup"><span data-stu-id="3a021-1331">hello higher hello number, hello better accuracy you will get, but hello compute time will take longer.</span></span> |<span data-ttu-id="3a021-1332">Entier </span><span class="sxs-lookup"><span data-stu-id="3a021-1332">Integer</span></span> |<span data-ttu-id="3a021-1333">10-50</span><span class="sxs-lookup"><span data-stu-id="3a021-1333">10-50</span></span> |
| <span data-ttu-id="3a021-1334">NumberOfModelDimensions</span><span class="sxs-lookup"><span data-stu-id="3a021-1334">NumberOfModelDimensions</span></span> |<span data-ttu-id="3a021-1335">un nombre de dimensions Hello relative nombre toohello du modèle de hello « features » va tenter de toofind au sein de vos données.</span><span class="sxs-lookup"><span data-stu-id="3a021-1335">hello number of dimensions relates toohello number of 'features' hello model will try toofind within your data.</span></span> <span data-ttu-id="3a021-1336">Augmentation du nombre hello de dimensions permettra de mieux précisément des résultats de hello dans des clusters plus petits.</span><span class="sxs-lookup"><span data-stu-id="3a021-1336">Increasing hello number of dimensions will allow better fine-tuning of hello results into smaller clusters.</span></span> <span data-ttu-id="3a021-1337">Toutefois, trop de dimensions empêche le modèle de hello recherche des corrélations entre les éléments.</span><span class="sxs-lookup"><span data-stu-id="3a021-1337">However, too many dimensions will prevent hello model from finding correlations between items.</span></span> |<span data-ttu-id="3a021-1338">Entier </span><span class="sxs-lookup"><span data-stu-id="3a021-1338">Integer</span></span> |<span data-ttu-id="3a021-1339">10-40</span><span class="sxs-lookup"><span data-stu-id="3a021-1339">10-40</span></span> |
| <span data-ttu-id="3a021-1340">ItemCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="3a021-1340">ItemCutOffLowerBound</span></span> |<span data-ttu-id="3a021-1341">Définit la limite d’inférieure élément hello pour les à hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-1341">Defines hello item lower bound for hello condenser.</span></span> <span data-ttu-id="3a021-1342">Consultez Condenseur d'utilisation ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="3a021-1342">See usage condenser above.</span></span> |<span data-ttu-id="3a021-1343">Integer</span><span class="sxs-lookup"><span data-stu-id="3a021-1343">Integer</span></span> |<span data-ttu-id="3a021-1344">2 ou plus (0 désactive le condenseur)</span><span class="sxs-lookup"><span data-stu-id="3a021-1344">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="3a021-1345">ItemCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="3a021-1345">ItemCutOffUpperBound</span></span> |<span data-ttu-id="3a021-1346">Définit la limite de supérieur élément hello pour les à hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-1346">Defines hello item upper bound for hello condenser.</span></span> <span data-ttu-id="3a021-1347">Consultez Condenseur d'utilisation ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="3a021-1347">See usage condenser above.</span></span> |<span data-ttu-id="3a021-1348">Integer</span><span class="sxs-lookup"><span data-stu-id="3a021-1348">Integer</span></span> |<span data-ttu-id="3a021-1349">2 ou plus (0 désactive le condenseur)</span><span class="sxs-lookup"><span data-stu-id="3a021-1349">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="3a021-1350">UserCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="3a021-1350">UserCutOffLowerBound</span></span> |<span data-ttu-id="3a021-1351">Définit la limite hello utilisateur pour les à hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-1351">Defines hello user lower bound for hello condenser.</span></span> <span data-ttu-id="3a021-1352">Consultez Condenseur d'utilisation ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="3a021-1352">See usage condenser above.</span></span> |<span data-ttu-id="3a021-1353">Integer</span><span class="sxs-lookup"><span data-stu-id="3a021-1353">Integer</span></span> |<span data-ttu-id="3a021-1354">2 ou plus (0 désactive le condenseur)</span><span class="sxs-lookup"><span data-stu-id="3a021-1354">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="3a021-1355">UserCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="3a021-1355">UserCutOffUpperBound</span></span> |<span data-ttu-id="3a021-1356">Définit la limite de supérieur utilisateur hello pour les à hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-1356">Defines hello user upper bound for hello condenser.</span></span> <span data-ttu-id="3a021-1357">Consultez Condenseur d'utilisation ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="3a021-1357">See usage condenser above.</span></span> |<span data-ttu-id="3a021-1358">Integer</span><span class="sxs-lookup"><span data-stu-id="3a021-1358">Integer</span></span> |<span data-ttu-id="3a021-1359">2 ou plus (0 désactive le condenseur)</span><span class="sxs-lookup"><span data-stu-id="3a021-1359">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="3a021-1360">Description</span><span class="sxs-lookup"><span data-stu-id="3a021-1360">Description</span></span> |<span data-ttu-id="3a021-1361">Description de la build.</span><span class="sxs-lookup"><span data-stu-id="3a021-1361">Build description.</span></span> |<span data-ttu-id="3a021-1362">String</span><span class="sxs-lookup"><span data-stu-id="3a021-1362">String</span></span> |<span data-ttu-id="3a021-1363">Tout texte, 512 caractères maximum</span><span class="sxs-lookup"><span data-stu-id="3a021-1363">Any text, maximum 512 chars</span></span> |
| <span data-ttu-id="3a021-1364">EnableModelingInsights</span><span class="sxs-lookup"><span data-stu-id="3a021-1364">EnableModelingInsights</span></span> |<span data-ttu-id="3a021-1365">Vous permet de toocompute métriques sur le modèle de recommandation hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-1365">Allows you toocompute metrics on hello recommendation model.</span></span> |<span data-ttu-id="3a021-1366">Boolean</span><span class="sxs-lookup"><span data-stu-id="3a021-1366">Boolean</span></span> |<span data-ttu-id="3a021-1367">True/False</span><span class="sxs-lookup"><span data-stu-id="3a021-1367">True/False</span></span> |
| <span data-ttu-id="3a021-1368">UseFeaturesInModel</span><span class="sxs-lookup"><span data-stu-id="3a021-1368">UseFeaturesInModel</span></span> |<span data-ttu-id="3a021-1369">Indique si les fonctionnalités peuvent être utilisées dans le modèle de recommandation d’ordre tooenhance hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-1369">Indicates if features can be used in order tooenhance hello recommendation model.</span></span> |<span data-ttu-id="3a021-1370">Boolean</span><span class="sxs-lookup"><span data-stu-id="3a021-1370">Boolean</span></span> |<span data-ttu-id="3a021-1371">True/False</span><span class="sxs-lookup"><span data-stu-id="3a021-1371">True/False</span></span> |
| <span data-ttu-id="3a021-1372">ModelingFeatureList</span><span class="sxs-lookup"><span data-stu-id="3a021-1372">ModelingFeatureList</span></span> |<span data-ttu-id="3a021-1373">Liste de séparées par des virgules des toobe de noms de fonction utilisée dans la génération de recommandation hello, dans la recommandation de commande tooenhance hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-1373">Comma-separated list of feature names toobe used in hello recommendation build, in order tooenhance hello recommendation.</span></span> |<span data-ttu-id="3a021-1374">String</span><span class="sxs-lookup"><span data-stu-id="3a021-1374">String</span></span> |<span data-ttu-id="3a021-1375">Noms de fonctionnalités, des caractères de too512</span><span class="sxs-lookup"><span data-stu-id="3a021-1375">Feature names, up too512 chars</span></span> |
| <span data-ttu-id="3a021-1376">AllowColdItemPlacement</span><span class="sxs-lookup"><span data-stu-id="3a021-1376">AllowColdItemPlacement</span></span> |<span data-ttu-id="3a021-1377">Indique si la recommandation de hello doit également à orienter éléments froids via la similarité de la fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="3a021-1377">Indicates if hello recommendation should also push cold items via feature similarity.</span></span> |<span data-ttu-id="3a021-1378">Boolean</span><span class="sxs-lookup"><span data-stu-id="3a021-1378">Boolean</span></span> |<span data-ttu-id="3a021-1379">True/False</span><span class="sxs-lookup"><span data-stu-id="3a021-1379">True/False</span></span> |
| <span data-ttu-id="3a021-1380">EnableFeatureCorrelation</span><span class="sxs-lookup"><span data-stu-id="3a021-1380">EnableFeatureCorrelation</span></span> |<span data-ttu-id="3a021-1381">Indique si des caractéristiques peuvent être utilisées dans le raisonnement.</span><span class="sxs-lookup"><span data-stu-id="3a021-1381">Indicates if features can be used in reasoning.</span></span> |<span data-ttu-id="3a021-1382">Boolean</span><span class="sxs-lookup"><span data-stu-id="3a021-1382">Boolean</span></span> |<span data-ttu-id="3a021-1383">True/False</span><span class="sxs-lookup"><span data-stu-id="3a021-1383">True/False</span></span> |
| <span data-ttu-id="3a021-1384">ReasoningFeatureList</span><span class="sxs-lookup"><span data-stu-id="3a021-1384">ReasoningFeatureList</span></span> |<span data-ttu-id="3a021-1385">Liste de séparées par des virgules de fonctionnalité toobe de noms utilisé pour le raisonnement phrases (par exemple, les explications de recommandation).</span><span class="sxs-lookup"><span data-stu-id="3a021-1385">Comma-separated list of feature names toobe used for reasoning sentences (e.g. recommendation explanations).</span></span> |<span data-ttu-id="3a021-1386">String</span><span class="sxs-lookup"><span data-stu-id="3a021-1386">String</span></span> |<span data-ttu-id="3a021-1387">Noms de fonctionnalités, des caractères de too512</span><span class="sxs-lookup"><span data-stu-id="3a021-1387">Feature names, up too512 chars</span></span> |

<span data-ttu-id="3a021-1388">OData XML</span><span class="sxs-lookup"><span data-stu-id="3a021-1388">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get build parameters</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2015-01-08T13:50:57Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">UseFeaturesInModel</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">AllowColdItemPlacement</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">EnableFeatureCorrelation</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">EnableModelingInsights</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">NumberOfModelIterations</d:Key>
                    <d:Value m:type="Edm.String">10</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
            <titletype="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">NumberOfModelDimensions</d:Key>
                    <d:Value m:type="Edm.String">10</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <linkrel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ItemCutOffLowerBound</d:Key>
                    <d:Value m:type="Edm.String">2</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ItemCutOffUpperBound</d:Key>
                    <d:Value m:type="Edm.String">2147483647</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">UserCutOffLowerBound</d:Key>
                    <d:Value m:type="Edm.String">2</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">UserCutOffUpperBound</d:Key>
                    <d:Value m:type="Edm.String">2147483647</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ModelingFeatureList</d:Key>
                    <d:Value m:type="Edm.String"/>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ReasoningFeatureList</d:Key>
                    <d:Value m:type="Edm.String"/>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">Description</d:Key>
                    <d:Value m:type="Edm.String">rankBuild</d:Value>
                </m:properties>
            </content>
        </entry>
    </feed>

## <a name="12-recommendation"></a><span data-ttu-id="3a021-1389">12. Recommandation</span><span class="sxs-lookup"><span data-stu-id="3a021-1389">12. Recommendation</span></span>
### <a name="121-get-item-recommendations-for-active-build"></a><span data-ttu-id="3a021-1390">12.1.</span><span class="sxs-lookup"><span data-stu-id="3a021-1390">12.1.</span></span> <span data-ttu-id="3a021-1391">Obtention de recommandations d’éléments (pour la build active)</span><span class="sxs-lookup"><span data-stu-id="3a021-1391">Get Item Recommendations (for active build)</span></span>
<span data-ttu-id="3a021-1392">Obtenir des recommandations de build active de hello de type « Recommendation » ou « Fbt » basé sur une liste d’éléments de semences (entrée).</span><span class="sxs-lookup"><span data-stu-id="3a021-1392">Get recommendations of hello active build of type "Recommendation" or "Fbt" based on a list of seeds (input) items.</span></span>

| <span data-ttu-id="3a021-1393">Méthode HTTP</span><span class="sxs-lookup"><span data-stu-id="3a021-1393">HTTP Method</span></span> | <span data-ttu-id="3a021-1394">URI</span><span class="sxs-lookup"><span data-stu-id="3a021-1394">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-1395">GET</span><span class="sxs-lookup"><span data-stu-id="3a021-1395">GET</span></span> |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="3a021-1396">Exemple :</span><span class="sxs-lookup"><span data-stu-id="3a021-1396">Example:</span></span><br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="3a021-1397">Nom du paramètre</span><span class="sxs-lookup"><span data-stu-id="3a021-1397">Parameter Name</span></span> | <span data-ttu-id="3a021-1398">Valeurs valides</span><span class="sxs-lookup"><span data-stu-id="3a021-1398">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-1399">modelId</span><span class="sxs-lookup"><span data-stu-id="3a021-1399">modelId</span></span> |<span data-ttu-id="3a021-1400">Identificateur unique du modèle de hello</span><span class="sxs-lookup"><span data-stu-id="3a021-1400">Unique identifier of hello model</span></span> |
| <span data-ttu-id="3a021-1401">itemIds</span><span class="sxs-lookup"><span data-stu-id="3a021-1401">itemIds</span></span> |<span data-ttu-id="3a021-1402">Liste de séparées par des virgules des toorecommend d’éléments hello pour.</span><span class="sxs-lookup"><span data-stu-id="3a021-1402">Comma-separated list of hello items toorecommend for.</span></span> <br><span data-ttu-id="3a021-1403">Si les build active hello est de type FBT puis vous pouvez envoyer qu’un seul élément.</span><span class="sxs-lookup"><span data-stu-id="3a021-1403">If hello active build is of type FBT then you can send only one item.</span></span> <br><span data-ttu-id="3a021-1404">Longueur maximale : 1024</span><span class="sxs-lookup"><span data-stu-id="3a021-1404">Max length: 1024</span></span> |
| <span data-ttu-id="3a021-1405">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="3a021-1405">numberOfResults</span></span> |<span data-ttu-id="3a021-1406">Nombre de résultats requis </span><span class="sxs-lookup"><span data-stu-id="3a021-1406">Number of required results</span></span> <br> <span data-ttu-id="3a021-1407">Max : 150</span><span class="sxs-lookup"><span data-stu-id="3a021-1407">Max: 150</span></span> |
| <span data-ttu-id="3a021-1408">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="3a021-1408">includeMetatadata</span></span> |<span data-ttu-id="3a021-1409">Utilisation ultérieure, toujours false</span><span class="sxs-lookup"><span data-stu-id="3a021-1409">Future use, always false</span></span> |
| <span data-ttu-id="3a021-1410">apiVersion</span><span class="sxs-lookup"><span data-stu-id="3a021-1410">apiVersion</span></span> |<span data-ttu-id="3a021-1411">1.0</span><span class="sxs-lookup"><span data-stu-id="3a021-1411">1.0</span></span> |

<span data-ttu-id="3a021-1412">**Réponse :**</span><span class="sxs-lookup"><span data-stu-id="3a021-1412">**Response:**</span></span>

<span data-ttu-id="3a021-1413">Code d'état HTTP : 200</span><span class="sxs-lookup"><span data-stu-id="3a021-1413">HTTP Status code: 200</span></span>

<span data-ttu-id="3a021-1414">réponse de Hello comporte une entrée par élément recommandé.</span><span class="sxs-lookup"><span data-stu-id="3a021-1414">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="3a021-1415">Chaque entrée a hello données suivantes :</span><span class="sxs-lookup"><span data-stu-id="3a021-1415">Each entry has hello following data:</span></span>

* <span data-ttu-id="3a021-1416">`Feed\entry\content\properties\Id` : ID d’élément recommandé</span><span class="sxs-lookup"><span data-stu-id="3a021-1416">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="3a021-1417">`Feed\entry\content\properties\Name`-Nom de l’élément de hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-1417">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="3a021-1418">`Feed\entry\content\properties\Rating`-Évaluation de recommandation de hello ; nombre élevé signifie toute confiance.</span><span class="sxs-lookup"><span data-stu-id="3a021-1418">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="3a021-1419">`Feed\entry\content\properties\Reasoning` : raisonnement de la recommandation (par exemple, pour expliquer les recommandations)</span><span class="sxs-lookup"><span data-stu-id="3a021-1419">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="3a021-1420">Hello exemple de réponse ci-dessous comprend 10 éléments recommandés.</span><span class="sxs-lookup"><span data-stu-id="3a021-1420">hello example response below includes 10 recommended items.</span></span>

<span data-ttu-id="3a021-1421">OData XML</span><span class="sxs-lookup"><span data-stu-id="3a021-1421">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get Recommendation</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T12:28:48Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
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

### <a name="122-get-item-recommendations-of-a-specific-build"></a><span data-ttu-id="3a021-1422">12.2.</span><span class="sxs-lookup"><span data-stu-id="3a021-1422">12.2.</span></span> <span data-ttu-id="3a021-1423">Obtention de recommandations d’éléments (d’une build spécifique)</span><span class="sxs-lookup"><span data-stu-id="3a021-1423">Get Item Recommendations (of a specific build)</span></span>
<span data-ttu-id="3a021-1424">Obtient des recommandations d'une build spécifique de type « Recommendation » ou « Fbt ».</span><span class="sxs-lookup"><span data-stu-id="3a021-1424">Get recommendations of a specific build of type "Recommendation" or "Fbt".</span></span>

| <span data-ttu-id="3a021-1425">Méthode HTTP</span><span class="sxs-lookup"><span data-stu-id="3a021-1425">HTTP Method</span></span> | <span data-ttu-id="3a021-1426">URI</span><span class="sxs-lookup"><span data-stu-id="3a021-1426">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-1427">GET</span><span class="sxs-lookup"><span data-stu-id="3a021-1427">GET</span></span> |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br><span data-ttu-id="3a021-1428">Exemple :</span><span class="sxs-lookup"><span data-stu-id="3a021-1428">Example:</span></span><br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&buildId=1234&apiVersion=%271.0%27` |

| <span data-ttu-id="3a021-1429">Nom du paramètre</span><span class="sxs-lookup"><span data-stu-id="3a021-1429">Parameter Name</span></span> | <span data-ttu-id="3a021-1430">Valeurs valides</span><span class="sxs-lookup"><span data-stu-id="3a021-1430">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-1431">modelId</span><span class="sxs-lookup"><span data-stu-id="3a021-1431">modelId</span></span> |<span data-ttu-id="3a021-1432">Identificateur unique du modèle de hello</span><span class="sxs-lookup"><span data-stu-id="3a021-1432">Unique identifier of hello model</span></span> |
| <span data-ttu-id="3a021-1433">itemIds</span><span class="sxs-lookup"><span data-stu-id="3a021-1433">itemIds</span></span> |<span data-ttu-id="3a021-1434">Liste de séparées par des virgules des toorecommend d’éléments hello pour.</span><span class="sxs-lookup"><span data-stu-id="3a021-1434">Comma-separated list of hello items toorecommend for.</span></span> <br><span data-ttu-id="3a021-1435">Si les build active hello est de type FBT puis vous pouvez envoyer qu’un seul élément.</span><span class="sxs-lookup"><span data-stu-id="3a021-1435">If hello active build is of type FBT then you can send only one item.</span></span> <br><span data-ttu-id="3a021-1436">Longueur maximale : 1024</span><span class="sxs-lookup"><span data-stu-id="3a021-1436">Max length: 1024</span></span> |
| <span data-ttu-id="3a021-1437">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="3a021-1437">numberOfResults</span></span> |<span data-ttu-id="3a021-1438">Nombre de résultats requis </span><span class="sxs-lookup"><span data-stu-id="3a021-1438">Number of required results</span></span> <br> <span data-ttu-id="3a021-1439">Max : 150</span><span class="sxs-lookup"><span data-stu-id="3a021-1439">Max: 150</span></span> |
| <span data-ttu-id="3a021-1440">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="3a021-1440">includeMetatadata</span></span> |<span data-ttu-id="3a021-1441">Utilisation ultérieure, toujours false</span><span class="sxs-lookup"><span data-stu-id="3a021-1441">Future use, always false</span></span> |
| <span data-ttu-id="3a021-1442">buildId</span><span class="sxs-lookup"><span data-stu-id="3a021-1442">buildId</span></span> |<span data-ttu-id="3a021-1443">Hello générer toouse id pour cette demande de recommandation</span><span class="sxs-lookup"><span data-stu-id="3a021-1443">hello build id toouse for this recommendation request</span></span> |
| <span data-ttu-id="3a021-1444">apiVersion</span><span class="sxs-lookup"><span data-stu-id="3a021-1444">apiVersion</span></span> |<span data-ttu-id="3a021-1445">1.0</span><span class="sxs-lookup"><span data-stu-id="3a021-1445">1.0</span></span> |

<span data-ttu-id="3a021-1446">**Réponse :**</span><span class="sxs-lookup"><span data-stu-id="3a021-1446">**Response:**</span></span>

<span data-ttu-id="3a021-1447">Code d'état HTTP : 200</span><span class="sxs-lookup"><span data-stu-id="3a021-1447">HTTP Status code: 200</span></span>

<span data-ttu-id="3a021-1448">réponse de Hello comporte une entrée par élément recommandé.</span><span class="sxs-lookup"><span data-stu-id="3a021-1448">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="3a021-1449">Chaque entrée a hello données suivantes :</span><span class="sxs-lookup"><span data-stu-id="3a021-1449">Each entry has hello following data:</span></span>

* <span data-ttu-id="3a021-1450">`Feed\entry\content\properties\Id` : ID d’élément recommandé</span><span class="sxs-lookup"><span data-stu-id="3a021-1450">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="3a021-1451">`Feed\entry\content\properties\Name`-Nom de l’élément de hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-1451">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="3a021-1452">`Feed\entry\content\properties\Rating`-Évaluation de recommandation de hello ; nombre élevé signifie toute confiance.</span><span class="sxs-lookup"><span data-stu-id="3a021-1452">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="3a021-1453">`Feed\entry\content\properties\Reasoning` : raisonnement de la recommandation (par exemple, pour expliquer les recommandations)</span><span class="sxs-lookup"><span data-stu-id="3a021-1453">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="3a021-1454">Pour obtenir un exemple de réponse, consultez la section 12.1.</span><span class="sxs-lookup"><span data-stu-id="3a021-1454">See a response example in 12.1</span></span>

### <a name="123-get-fbt-recommendations-for-active-build"></a><span data-ttu-id="3a021-1455">12.3.</span><span class="sxs-lookup"><span data-stu-id="3a021-1455">12.3.</span></span> <span data-ttu-id="3a021-1456">Obtention de recommandations FBT (pour la build active)</span><span class="sxs-lookup"><span data-stu-id="3a021-1456">Get FBT Recommendations (for active build)</span></span>
<span data-ttu-id="3a021-1457">Obtenir des recommandations de build active de hello du type « Fbt » basé sur un élément de valeur initiale (entrée).</span><span class="sxs-lookup"><span data-stu-id="3a021-1457">Get recommendations of hello active build of type "Fbt" based on a seed (input) item.</span></span>

| <span data-ttu-id="3a021-1458">Méthode HTTP</span><span class="sxs-lookup"><span data-stu-id="3a021-1458">HTTP Method</span></span> | <span data-ttu-id="3a021-1459">URI</span><span class="sxs-lookup"><span data-stu-id="3a021-1459">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-1460">GET</span><span class="sxs-lookup"><span data-stu-id="3a021-1460">GET</span></span> |`<rootURI>/ItemFbtRecommend?modelId=%27<modelId>%27&itemId=%27<itemId>%27&numberOfResults=<int>&minimalScore=<double>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="3a021-1461">Exemple :</span><span class="sxs-lookup"><span data-stu-id="3a021-1461">Example:</span></span><br>`<rootURI>/ItemFbtRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemId=%271003%27&numberOfResults=10&minimalScore=<double>&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="3a021-1462">Nom du paramètre</span><span class="sxs-lookup"><span data-stu-id="3a021-1462">Parameter Name</span></span> | <span data-ttu-id="3a021-1463">Valeurs valides</span><span class="sxs-lookup"><span data-stu-id="3a021-1463">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-1464">modelId</span><span class="sxs-lookup"><span data-stu-id="3a021-1464">modelId</span></span> |<span data-ttu-id="3a021-1465">Identificateur unique du modèle de hello</span><span class="sxs-lookup"><span data-stu-id="3a021-1465">Unique identifier of hello model</span></span> |
| <span data-ttu-id="3a021-1466">itemId</span><span class="sxs-lookup"><span data-stu-id="3a021-1466">itemId</span></span> |<span data-ttu-id="3a021-1467">Toorecommend élément pour.</span><span class="sxs-lookup"><span data-stu-id="3a021-1467">Item toorecommend for.</span></span> <br><span data-ttu-id="3a021-1468">Longueur maximale : 1024</span><span class="sxs-lookup"><span data-stu-id="3a021-1468">Max length: 1024</span></span> |
| <span data-ttu-id="3a021-1469">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="3a021-1469">numberOfResults</span></span> |<span data-ttu-id="3a021-1470">Nombre de résultats requis </span><span class="sxs-lookup"><span data-stu-id="3a021-1470">Number of required results</span></span> <br><span data-ttu-id="3a021-1471">Max : 150</span><span class="sxs-lookup"><span data-stu-id="3a021-1471">Max: 150</span></span> |
| <span data-ttu-id="3a021-1472">minimalScore</span><span class="sxs-lookup"><span data-stu-id="3a021-1472">minimalScore</span></span> |<span data-ttu-id="3a021-1473">Score minimal un ensemble de fréquent ont dans toobe de commande inclus dans hello retourner des résultats</span><span class="sxs-lookup"><span data-stu-id="3a021-1473">Minimal score that a frequent set should have in order toobe included in hello returned results</span></span> |
| <span data-ttu-id="3a021-1474">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="3a021-1474">includeMetatadata</span></span> |<span data-ttu-id="3a021-1475">Utilisation ultérieure, toujours false</span><span class="sxs-lookup"><span data-stu-id="3a021-1475">Future use, always false</span></span> |
| <span data-ttu-id="3a021-1476">apiVersion</span><span class="sxs-lookup"><span data-stu-id="3a021-1476">apiVersion</span></span> |<span data-ttu-id="3a021-1477">1.0</span><span class="sxs-lookup"><span data-stu-id="3a021-1477">1.0</span></span> |

<span data-ttu-id="3a021-1478">**Réponse :**</span><span class="sxs-lookup"><span data-stu-id="3a021-1478">**Response:**</span></span>

<span data-ttu-id="3a021-1479">Code d'état HTTP : 200</span><span class="sxs-lookup"><span data-stu-id="3a021-1479">HTTP Status code: 200</span></span>

<span data-ttu-id="3a021-1480">réponse de Hello inclut une entrée par l’ensemble de l’élément recommandé (il s’agit d’un ensemble d’éléments qui sont généralement achetés avec l’élément de départ/entrée hello).</span><span class="sxs-lookup"><span data-stu-id="3a021-1480">hello response includes one entry per recommended item set (a set of items which are usually bought together with hello seed/input item).</span></span> <span data-ttu-id="3a021-1481">Chaque entrée a hello données suivantes :</span><span class="sxs-lookup"><span data-stu-id="3a021-1481">Each entry has hello following data:</span></span>

* <span data-ttu-id="3a021-1482">`Feed\entry\content\properties\Id1` : ID d’élément recommandé</span><span class="sxs-lookup"><span data-stu-id="3a021-1482">`Feed\entry\content\properties\Id1` - Recommended item ID.</span></span>
* <span data-ttu-id="3a021-1483">`Feed\entry\content\properties\Name1`-Nom de l’élément de hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-1483">`Feed\entry\content\properties\Name1` - Name of hello item.</span></span>
* <span data-ttu-id="3a021-1484">`Feed\entry\content\properties\Id2` : ID du second élément recommandé (facultatif).</span><span class="sxs-lookup"><span data-stu-id="3a021-1484">`Feed\entry\content\properties\Id2` - 2nd recommended item ID (optional).</span></span>
* <span data-ttu-id="3a021-1485">`Feed\entry\content\properties\Name2`-Nom de l’élément 2e hello (facultatif).</span><span class="sxs-lookup"><span data-stu-id="3a021-1485">`Feed\entry\content\properties\Name2` - Name of hello 2nd item (optional).</span></span>
* <span data-ttu-id="3a021-1486">`Feed\entry\content\properties\Rating`-Évaluation de recommandation de hello ; nombre élevé signifie toute confiance.</span><span class="sxs-lookup"><span data-stu-id="3a021-1486">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="3a021-1487">`Feed\entry\content\properties\Reasoning` : raisonnement de la recommandation (par exemple, pour expliquer les recommandations)</span><span class="sxs-lookup"><span data-stu-id="3a021-1487">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="3a021-1488">Hello exemple de réponse ci-dessous inclut 3 séries d’élément recommandé.</span><span class="sxs-lookup"><span data-stu-id="3a021-1488">hello example response below includes 3 recommended item sets.</span></span>

<span data-ttu-id="3a021-1489">OData XML</span><span class="sxs-lookup"><span data-stu-id="3a021-1489">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get Recommendation</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemId='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T12:28:48Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetFbtRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id1 m:type="Edm.String">159</d:Id1>
        <d:Name1 m:type="Edm.String">159</d:Name1>
        <d:Id2 m:type="Edm.String"></d:Id2>
        <d:Name2 m:type="Edm.String"></d:Name2>
        <d:Rating m:type="Edm.Double">0.543343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who bought '1003' also bought '159'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetFbtRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id1 m:type="Edm.String">52</d:Id1>
        <d:Name1 m:type="Edm.String">52</d:Name1>
        <d:Id2 m:type="Edm.String"></d:Id2>
        <d:Name2 m:type="Edm.String"></d:Name2>
        <d:Rating m:type="Edm.Double">0.533343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who bought '1003' also bought '52'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetFbtRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id1 m:type="Edm.String">35</d:Id1>
        <d:Name1 m:type="Edm.String">35</d:Name1>
        <d:Id2 m:type="Edm.String">102</d:Id2>
        <d:Name2 m:type="Edm.String">102</d:Name2>
        <d:Rating m:type="Edm.Double">0.523343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who bought '1003' also bought '35' and '102'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="124-get-fbt-recommendations-of-a-specific-build"></a><span data-ttu-id="3a021-1490">12.4.</span><span class="sxs-lookup"><span data-stu-id="3a021-1490">12.4.</span></span> <span data-ttu-id="3a021-1491">Obtention de recommandations FBT (d’une build spécifique)</span><span class="sxs-lookup"><span data-stu-id="3a021-1491">Get FBT Recommendations (of a specific build)</span></span>
<span data-ttu-id="3a021-1492">Obtient des recommandations d’une build spécifique de type « Fbt ».</span><span class="sxs-lookup"><span data-stu-id="3a021-1492">Get recommendations of a specific build of type "Fbt".</span></span>

| <span data-ttu-id="3a021-1493">Méthode HTTP</span><span class="sxs-lookup"><span data-stu-id="3a021-1493">HTTP Method</span></span> | <span data-ttu-id="3a021-1494">URI</span><span class="sxs-lookup"><span data-stu-id="3a021-1494">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-1495">GET</span><span class="sxs-lookup"><span data-stu-id="3a021-1495">GET</span></span> |`<rootURI>/ItemFbtRecommend?modelId=%27<modelId>%27&itemId=%27<itemId>%27&numberOfResults=<int>&minimalScore=<double>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br><span data-ttu-id="3a021-1496">Exemple :</span><span class="sxs-lookup"><span data-stu-id="3a021-1496">Example:</span></span><br>`<rootURI>/ItemFbtRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemId=%271003%27&numberOfResults=10&minimalScore=0.1&includeMetadata=false&buildId=1234&apiVersion=%271.0%27` |

| <span data-ttu-id="3a021-1497">Nom du paramètre</span><span class="sxs-lookup"><span data-stu-id="3a021-1497">Parameter Name</span></span> | <span data-ttu-id="3a021-1498">Valeurs valides</span><span class="sxs-lookup"><span data-stu-id="3a021-1498">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-1499">modelId</span><span class="sxs-lookup"><span data-stu-id="3a021-1499">modelId</span></span> |<span data-ttu-id="3a021-1500">Identificateur unique du modèle de hello</span><span class="sxs-lookup"><span data-stu-id="3a021-1500">Unique identifier of hello model</span></span> |
| <span data-ttu-id="3a021-1501">itemId</span><span class="sxs-lookup"><span data-stu-id="3a021-1501">itemId</span></span> |<span data-ttu-id="3a021-1502">Toorecommend élément pour.</span><span class="sxs-lookup"><span data-stu-id="3a021-1502">Item toorecommend for.</span></span> <br><span data-ttu-id="3a021-1503">Longueur maximale : 1024</span><span class="sxs-lookup"><span data-stu-id="3a021-1503">Max length: 1024</span></span> |
| <span data-ttu-id="3a021-1504">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="3a021-1504">numberOfResults</span></span> |<span data-ttu-id="3a021-1505">Nombre de résultats requis </span><span class="sxs-lookup"><span data-stu-id="3a021-1505">Number of required results</span></span> <br><span data-ttu-id="3a021-1506">Max : 150</span><span class="sxs-lookup"><span data-stu-id="3a021-1506">Max: 150</span></span> |
| <span data-ttu-id="3a021-1507">minimalScore</span><span class="sxs-lookup"><span data-stu-id="3a021-1507">minimalScore</span></span> |<span data-ttu-id="3a021-1508">Score minimal un ensemble de fréquent ont dans toobe de commande inclus dans hello retourner des résultats</span><span class="sxs-lookup"><span data-stu-id="3a021-1508">Minimal score that a frequent set should have in order toobe included in hello returned results</span></span> |
| <span data-ttu-id="3a021-1509">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="3a021-1509">includeMetatadata</span></span> |<span data-ttu-id="3a021-1510">Utilisation ultérieure, toujours false</span><span class="sxs-lookup"><span data-stu-id="3a021-1510">Future use, always false</span></span> |
| <span data-ttu-id="3a021-1511">buildId</span><span class="sxs-lookup"><span data-stu-id="3a021-1511">buildId</span></span> |<span data-ttu-id="3a021-1512">Hello générer toouse id pour cette demande de recommandation</span><span class="sxs-lookup"><span data-stu-id="3a021-1512">hello build id toouse for this recommendation request</span></span> |
| <span data-ttu-id="3a021-1513">apiVersion</span><span class="sxs-lookup"><span data-stu-id="3a021-1513">apiVersion</span></span> |<span data-ttu-id="3a021-1514">1.0</span><span class="sxs-lookup"><span data-stu-id="3a021-1514">1.0</span></span> |

<span data-ttu-id="3a021-1515">**Réponse :**</span><span class="sxs-lookup"><span data-stu-id="3a021-1515">**Response:**</span></span>

<span data-ttu-id="3a021-1516">Code d'état HTTP : 200</span><span class="sxs-lookup"><span data-stu-id="3a021-1516">HTTP Status code: 200</span></span>

<span data-ttu-id="3a021-1517">réponse de Hello inclut une entrée par l’ensemble de l’élément recommandé (il s’agit d’un ensemble d’éléments qui sont généralement achetés avec l’élément de départ/entrée hello).</span><span class="sxs-lookup"><span data-stu-id="3a021-1517">hello response includes one entry per recommended item set (a set of items which are usually bought together with hello seed/input item).</span></span> <span data-ttu-id="3a021-1518">Chaque entrée a hello données suivantes :</span><span class="sxs-lookup"><span data-stu-id="3a021-1518">Each entry has hello following data:</span></span>

* <span data-ttu-id="3a021-1519">`Feed\entry\content\properties\Id1` : ID d’élément recommandé</span><span class="sxs-lookup"><span data-stu-id="3a021-1519">`Feed\entry\content\properties\Id1` - Recommended item ID.</span></span>
* <span data-ttu-id="3a021-1520">`Feed\entry\content\properties\Name1`-Nom de l’élément de hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-1520">`Feed\entry\content\properties\Name1` - Name of hello item.</span></span>
* <span data-ttu-id="3a021-1521">`Feed\entry\content\properties\Id2` : ID du second élément recommandé (facultatif).</span><span class="sxs-lookup"><span data-stu-id="3a021-1521">`Feed\entry\content\properties\Id2` - 2nd recommended item ID (optional).</span></span>
* <span data-ttu-id="3a021-1522">`Feed\entry\content\properties\Name2`-Nom de l’élément 2e hello (facultatif).</span><span class="sxs-lookup"><span data-stu-id="3a021-1522">`Feed\entry\content\properties\Name2` - Name of hello 2nd item (optional).</span></span>
* <span data-ttu-id="3a021-1523">`Feed\entry\content\properties\Rating`-Évaluation de recommandation de hello ; nombre élevé signifie toute confiance.</span><span class="sxs-lookup"><span data-stu-id="3a021-1523">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="3a021-1524">`Feed\entry\content\properties\Reasoning` : raisonnement de la recommandation (par exemple, pour expliquer les recommandations)</span><span class="sxs-lookup"><span data-stu-id="3a021-1524">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="3a021-1525">Pour obtenir un exemple de réponse, consultez la section 12.3.</span><span class="sxs-lookup"><span data-stu-id="3a021-1525">See a response example in 12.3</span></span>

### <a name="125-get-user-recommendations-for-active-build"></a><span data-ttu-id="3a021-1526">12.5.</span><span class="sxs-lookup"><span data-stu-id="3a021-1526">12.5.</span></span> <span data-ttu-id="3a021-1527">Obtention de recommandations de l’utilisateur (pour la build active)</span><span class="sxs-lookup"><span data-stu-id="3a021-1527">Get User Recommendations (for active build)</span></span>
<span data-ttu-id="3a021-1528">Obtient des recommandations de l’utilisateur auprès de la build de type « Recommendation » marquée comme build active.</span><span class="sxs-lookup"><span data-stu-id="3a021-1528">Get user recommendations of a build of type "Recommendation" marked as active build.</span></span>

<span data-ttu-id="3a021-1529">Hello API renvoie une liste de l’élément prédit en fonction de l’historique d’utilisation de l’utilisateur de hello toohello.</span><span class="sxs-lookup"><span data-stu-id="3a021-1529">hello API will return a list of predicted item according toohello usage history of hello user.</span></span>

<span data-ttu-id="3a021-1530">Remarques :</span><span class="sxs-lookup"><span data-stu-id="3a021-1530">Notes:</span></span> 

1. <span data-ttu-id="3a021-1531">Il n’existe aucune recommandation de l’utilisateur pour une build de type FBT.</span><span class="sxs-lookup"><span data-stu-id="3a021-1531">There is no user recommendation for FBT build.</span></span>
2. <span data-ttu-id="3a021-1532">Si la build de hello active est FBT sera de cette méthode retourne une erreur.</span><span class="sxs-lookup"><span data-stu-id="3a021-1532">If hello active build is FBT this method will returns an error.</span></span>

| <span data-ttu-id="3a021-1533">Méthode HTTP</span><span class="sxs-lookup"><span data-stu-id="3a021-1533">HTTP Method</span></span> | <span data-ttu-id="3a021-1534">URI</span><span class="sxs-lookup"><span data-stu-id="3a021-1534">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-1535">GET</span><span class="sxs-lookup"><span data-stu-id="3a021-1535">GET</span></span> |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="3a021-1536">Exemple :</span><span class="sxs-lookup"><span data-stu-id="3a021-1536">Example:</span></span><br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="3a021-1537">Nom du paramètre</span><span class="sxs-lookup"><span data-stu-id="3a021-1537">Parameter Name</span></span> | <span data-ttu-id="3a021-1538">Valeurs valides</span><span class="sxs-lookup"><span data-stu-id="3a021-1538">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-1539">modelId</span><span class="sxs-lookup"><span data-stu-id="3a021-1539">modelId</span></span> |<span data-ttu-id="3a021-1540">Identificateur unique du modèle de hello</span><span class="sxs-lookup"><span data-stu-id="3a021-1540">Unique identifier of hello model</span></span> |
| <span data-ttu-id="3a021-1541">userId</span><span class="sxs-lookup"><span data-stu-id="3a021-1541">userId</span></span> |<span data-ttu-id="3a021-1542">Identificateur unique de l’utilisateur de hello</span><span class="sxs-lookup"><span data-stu-id="3a021-1542">Unique identifier of hello user</span></span> |
| <span data-ttu-id="3a021-1543">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="3a021-1543">numberOfResults</span></span> |<span data-ttu-id="3a021-1544">Nombre de résultats requis</span><span class="sxs-lookup"><span data-stu-id="3a021-1544">Number of required results</span></span> |
| <span data-ttu-id="3a021-1545">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="3a021-1545">includeMetatadata</span></span> |<span data-ttu-id="3a021-1546">Utilisation ultérieure, toujours false</span><span class="sxs-lookup"><span data-stu-id="3a021-1546">Future use, always false</span></span> |
| <span data-ttu-id="3a021-1547">apiVersion</span><span class="sxs-lookup"><span data-stu-id="3a021-1547">apiVersion</span></span> |<span data-ttu-id="3a021-1548">1.0</span><span class="sxs-lookup"><span data-stu-id="3a021-1548">1.0</span></span> |

<span data-ttu-id="3a021-1549">**Réponse :**</span><span class="sxs-lookup"><span data-stu-id="3a021-1549">**Response:**</span></span>

<span data-ttu-id="3a021-1550">Code d'état HTTP : 200</span><span class="sxs-lookup"><span data-stu-id="3a021-1550">HTTP Status code: 200</span></span>

<span data-ttu-id="3a021-1551">réponse de Hello comporte une entrée par élément recommandé.</span><span class="sxs-lookup"><span data-stu-id="3a021-1551">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="3a021-1552">Chaque entrée a hello données suivantes :</span><span class="sxs-lookup"><span data-stu-id="3a021-1552">Each entry has hello following data:</span></span>

* <span data-ttu-id="3a021-1553">`Feed\entry\content\properties\Id` : ID d’élément recommandé</span><span class="sxs-lookup"><span data-stu-id="3a021-1553">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="3a021-1554">`Feed\entry\content\properties\Name`-Nom de l’élément de hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-1554">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="3a021-1555">`Feed\entry\content\properties\Rating`-Évaluation de recommandation de hello ; nombre élevé signifie toute confiance.</span><span class="sxs-lookup"><span data-stu-id="3a021-1555">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="3a021-1556">`Feed\entry\content\properties\Reasoning` : raisonnement de la recommandation (par exemple, pour expliquer les recommandations)</span><span class="sxs-lookup"><span data-stu-id="3a021-1556">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="3a021-1557">Pour obtenir un exemple de réponse, consultez la section 12.1.</span><span class="sxs-lookup"><span data-stu-id="3a021-1557">See a response example in 12.1</span></span>

### <a name="126-get-user-recommendations-with-item-list-for-active-build"></a><span data-ttu-id="3a021-1558">12.6.</span><span class="sxs-lookup"><span data-stu-id="3a021-1558">12.6.</span></span> <span data-ttu-id="3a021-1559">Obtention de recommandations de l’utilisateur avec une liste d’éléments (pour la build active)</span><span class="sxs-lookup"><span data-stu-id="3a021-1559">Get User Recommendations with item list (for active build)</span></span>
<span data-ttu-id="3a021-1560">Obtient des recommandations de l’utilisateur auprès de la build de type « Recommendation » marquée comme build active, à l’aide d’une liste supplémentaire d’éléments.</span><span class="sxs-lookup"><span data-stu-id="3a021-1560">Get user recommendations of a build of type "Recommendation" marked as active build with an additional list of items</span></span>

<span data-ttu-id="3a021-1561">Hello API renvoie une liste de l’élément prédit selon l’historique d’utilisation de toohello d’utilisateur de hello et hello autres fourni.</span><span class="sxs-lookup"><span data-stu-id="3a021-1561">hello API will return a list of predicted item according toohello usage history of hello user and hello additional provided items.</span></span>

<span data-ttu-id="3a021-1562">Remarques :</span><span class="sxs-lookup"><span data-stu-id="3a021-1562">Notes:</span></span> 

1. <span data-ttu-id="3a021-1563">Il n’existe aucune recommandation de l’utilisateur pour une build de type FBT.</span><span class="sxs-lookup"><span data-stu-id="3a021-1563">There is no user recommendation for FBT build.</span></span>
2. <span data-ttu-id="3a021-1564">Si la build de hello active est FBT sera de cette méthode retourne une erreur.</span><span class="sxs-lookup"><span data-stu-id="3a021-1564">If hello active build is FBT this method will returns an error.</span></span>

| <span data-ttu-id="3a021-1565">Méthode HTTP</span><span class="sxs-lookup"><span data-stu-id="3a021-1565">HTTP Method</span></span> | <span data-ttu-id="3a021-1566">URI</span><span class="sxs-lookup"><span data-stu-id="3a021-1566">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-1567">GET</span><span class="sxs-lookup"><span data-stu-id="3a021-1567">GET</span></span> |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>&itemsIds=%27<itemsIds>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="3a021-1568">Exemple :</span><span class="sxs-lookup"><span data-stu-id="3a021-1568">Example:</span></span><br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&itemsIds=%271003%2C1000%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="3a021-1569">Nom du paramètre</span><span class="sxs-lookup"><span data-stu-id="3a021-1569">Parameter Name</span></span> | <span data-ttu-id="3a021-1570">Valeurs valides</span><span class="sxs-lookup"><span data-stu-id="3a021-1570">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-1571">modelId</span><span class="sxs-lookup"><span data-stu-id="3a021-1571">modelId</span></span> |<span data-ttu-id="3a021-1572">Identificateur unique du modèle de hello</span><span class="sxs-lookup"><span data-stu-id="3a021-1572">Unique identifier of hello model</span></span> |
| <span data-ttu-id="3a021-1573">userId</span><span class="sxs-lookup"><span data-stu-id="3a021-1573">userId</span></span> |<span data-ttu-id="3a021-1574">Identificateur unique de l’utilisateur de hello</span><span class="sxs-lookup"><span data-stu-id="3a021-1574">Unique identifier of hello user</span></span> |
| <span data-ttu-id="3a021-1575">itemsIds</span><span class="sxs-lookup"><span data-stu-id="3a021-1575">itemsIds</span></span> |<span data-ttu-id="3a021-1576">Liste de séparées par des virgules des toorecommend d’éléments hello pour.</span><span class="sxs-lookup"><span data-stu-id="3a021-1576">Comma-separated list of hello items toorecommend for.</span></span> <span data-ttu-id="3a021-1577">Longueur maximale : 1024</span><span class="sxs-lookup"><span data-stu-id="3a021-1577">Max length: 1024</span></span> |
| <span data-ttu-id="3a021-1578">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="3a021-1578">numberOfResults</span></span> |<span data-ttu-id="3a021-1579">Nombre de résultats requis</span><span class="sxs-lookup"><span data-stu-id="3a021-1579">Number of required results</span></span> |
| <span data-ttu-id="3a021-1580">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="3a021-1580">includeMetatadata</span></span> |<span data-ttu-id="3a021-1581">Utilisation ultérieure, toujours false</span><span class="sxs-lookup"><span data-stu-id="3a021-1581">Future use, always false</span></span> |
| <span data-ttu-id="3a021-1582">apiVersion</span><span class="sxs-lookup"><span data-stu-id="3a021-1582">apiVersion</span></span> |<span data-ttu-id="3a021-1583">1.0</span><span class="sxs-lookup"><span data-stu-id="3a021-1583">1.0</span></span> |

<span data-ttu-id="3a021-1584">**Réponse :**</span><span class="sxs-lookup"><span data-stu-id="3a021-1584">**Response:**</span></span>

<span data-ttu-id="3a021-1585">Code d'état HTTP : 200</span><span class="sxs-lookup"><span data-stu-id="3a021-1585">HTTP Status code: 200</span></span>

<span data-ttu-id="3a021-1586">réponse de Hello comporte une entrée par élément recommandé.</span><span class="sxs-lookup"><span data-stu-id="3a021-1586">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="3a021-1587">Chaque entrée a hello données suivantes :</span><span class="sxs-lookup"><span data-stu-id="3a021-1587">Each entry has hello following data:</span></span>

* <span data-ttu-id="3a021-1588">`Feed\entry\content\properties\Id` : ID d’élément recommandé</span><span class="sxs-lookup"><span data-stu-id="3a021-1588">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="3a021-1589">`Feed\entry\content\properties\Name`-Nom de l’élément de hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-1589">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="3a021-1590">`Feed\entry\content\properties\Rating`-Évaluation de recommandation de hello ; nombre élevé signifie toute confiance.</span><span class="sxs-lookup"><span data-stu-id="3a021-1590">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="3a021-1591">`Feed\entry\content\properties\Reasoning` : raisonnement de la recommandation (par exemple, pour expliquer les recommandations)</span><span class="sxs-lookup"><span data-stu-id="3a021-1591">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="3a021-1592">Pour obtenir un exemple de réponse, consultez la section 12.1.</span><span class="sxs-lookup"><span data-stu-id="3a021-1592">See a response example in 12.1</span></span>

### <a name="127-get-user-recommendations--of-a-specific-build"></a><span data-ttu-id="3a021-1593">12.7.</span><span class="sxs-lookup"><span data-stu-id="3a021-1593">12.7.</span></span> <span data-ttu-id="3a021-1594">Obtention de recommandations de l’utilisateur (d’une build spécifique)</span><span class="sxs-lookup"><span data-stu-id="3a021-1594">Get User Recommendations  (of a specific build)</span></span>
<span data-ttu-id="3a021-1595">Obtient des recommandations de l’utilisateur auprès d’une build spécifique de type « Recommendation ».</span><span class="sxs-lookup"><span data-stu-id="3a021-1595">Get user recommendations of a specific build of type "Recommendation".</span></span>

<span data-ttu-id="3a021-1596">Hello API renvoie une liste de l’élément prédit en fonction de l’historique d’utilisation toohello d’utilisateur hello (utilisé dans une build spécifique de hello).</span><span class="sxs-lookup"><span data-stu-id="3a021-1596">hello API will return a list of predicted item according toohello usage history of hello user (used in hello specific build).</span></span>

<span data-ttu-id="3a021-1597">Remarque : il n’existe aucune recommandation de l’utilisateur pour une build de type FBT.</span><span class="sxs-lookup"><span data-stu-id="3a021-1597">Note: There is no user recommendation for FBT build.</span></span>

| <span data-ttu-id="3a021-1598">Méthode HTTP</span><span class="sxs-lookup"><span data-stu-id="3a021-1598">HTTP Method</span></span> | <span data-ttu-id="3a021-1599">URI</span><span class="sxs-lookup"><span data-stu-id="3a021-1599">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-1600">GET</span><span class="sxs-lookup"><span data-stu-id="3a021-1600">GET</span></span> |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>%27&numberOfResults=<int>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br><span data-ttu-id="3a021-1601">Exemple :</span><span class="sxs-lookup"><span data-stu-id="3a021-1601">Example:</span></span><br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&numberOfResults=10&includeMetadata=false&buildId=50012&apiVersion=%271.0%27` |

| <span data-ttu-id="3a021-1602">Nom du paramètre</span><span class="sxs-lookup"><span data-stu-id="3a021-1602">Parameter Name</span></span> | <span data-ttu-id="3a021-1603">Valeurs valides</span><span class="sxs-lookup"><span data-stu-id="3a021-1603">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-1604">modelId</span><span class="sxs-lookup"><span data-stu-id="3a021-1604">modelId</span></span> |<span data-ttu-id="3a021-1605">Identificateur unique du modèle de hello</span><span class="sxs-lookup"><span data-stu-id="3a021-1605">Unique identifier of hello model</span></span> |
| <span data-ttu-id="3a021-1606">userId</span><span class="sxs-lookup"><span data-stu-id="3a021-1606">userId</span></span> |<span data-ttu-id="3a021-1607">Identificateur unique de l’utilisateur de hello</span><span class="sxs-lookup"><span data-stu-id="3a021-1607">Unique identifier of hello user</span></span> |
| <span data-ttu-id="3a021-1608">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="3a021-1608">numberOfResults</span></span> |<span data-ttu-id="3a021-1609">Nombre de résultats requis</span><span class="sxs-lookup"><span data-stu-id="3a021-1609">Number of required results</span></span> |
| <span data-ttu-id="3a021-1610">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="3a021-1610">includeMetatadata</span></span> |<span data-ttu-id="3a021-1611">Utilisation ultérieure, toujours false</span><span class="sxs-lookup"><span data-stu-id="3a021-1611">Future use, always false</span></span> |
| <span data-ttu-id="3a021-1612">buildId</span><span class="sxs-lookup"><span data-stu-id="3a021-1612">buildId</span></span> |<span data-ttu-id="3a021-1613">Hello générer toouse id pour cette demande de recommandation</span><span class="sxs-lookup"><span data-stu-id="3a021-1613">hello build id toouse for this recommendation request</span></span> |
| <span data-ttu-id="3a021-1614">apiVersion</span><span class="sxs-lookup"><span data-stu-id="3a021-1614">apiVersion</span></span> |<span data-ttu-id="3a021-1615">1.0</span><span class="sxs-lookup"><span data-stu-id="3a021-1615">1.0</span></span> |

<span data-ttu-id="3a021-1616">**Réponse :**</span><span class="sxs-lookup"><span data-stu-id="3a021-1616">**Response:**</span></span>

<span data-ttu-id="3a021-1617">Code d'état HTTP : 200</span><span class="sxs-lookup"><span data-stu-id="3a021-1617">HTTP Status code: 200</span></span>

<span data-ttu-id="3a021-1618">réponse de Hello comporte une entrée par élément recommandé.</span><span class="sxs-lookup"><span data-stu-id="3a021-1618">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="3a021-1619">Chaque entrée a hello données suivantes :</span><span class="sxs-lookup"><span data-stu-id="3a021-1619">Each entry has hello following data:</span></span>

* <span data-ttu-id="3a021-1620">`Feed\entry\content\properties\Id` : ID d’élément recommandé</span><span class="sxs-lookup"><span data-stu-id="3a021-1620">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="3a021-1621">`Feed\entry\content\properties\Name`-Nom de l’élément de hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-1621">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="3a021-1622">`Feed\entry\content\properties\Rating`-Évaluation de recommandation de hello ; nombre élevé signifie toute confiance.</span><span class="sxs-lookup"><span data-stu-id="3a021-1622">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="3a021-1623">`Feed\entry\content\properties\Reasoning` : raisonnement de la recommandation (par exemple, pour expliquer les recommandations)</span><span class="sxs-lookup"><span data-stu-id="3a021-1623">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="3a021-1624">Pour obtenir un exemple de réponse, consultez la section 12.1.</span><span class="sxs-lookup"><span data-stu-id="3a021-1624">See a response example in 12.1</span></span>

### <a name="128-get-user-recommendations-with-item-list-of-a-specific-build"></a><span data-ttu-id="3a021-1625">12.8.</span><span class="sxs-lookup"><span data-stu-id="3a021-1625">12.8.</span></span> <span data-ttu-id="3a021-1626">Obtention de recommandations de l’utilisateur avec une liste d’éléments (pour une build spécifique)</span><span class="sxs-lookup"><span data-stu-id="3a021-1626">Get User Recommendations with item list (of a specific build)</span></span>
<span data-ttu-id="3a021-1627">Obtenir des recommandations de l’utilisateur d’une build spécifique de type « Recommendation » et liste hello d’éléments supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="3a021-1627">Get user recommendations of a specific build of type "Recommendation" and hello list of additional items.</span></span>

<span data-ttu-id="3a021-1628">Hello API renvoie une liste de l’élément prédit en fonction de l’historique d’utilisation de l’utilisateur de hello toohello et liste supplémentaire de hello d’éléments.</span><span class="sxs-lookup"><span data-stu-id="3a021-1628">hello API will return a list of predicted item according toohello usage history of hello user and hello additional list of items.</span></span>

<span data-ttu-id="3a021-1629">Remarque : il n’existe aucune recommandation de l’utilisateur pour une build de type FBT.</span><span class="sxs-lookup"><span data-stu-id="3a021-1629">Note: Tthere is no user recommendation for FBT build.</span></span>

| <span data-ttu-id="3a021-1630">Méthode HTTP</span><span class="sxs-lookup"><span data-stu-id="3a021-1630">HTTP Method</span></span> | <span data-ttu-id="3a021-1631">URI</span><span class="sxs-lookup"><span data-stu-id="3a021-1631">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-1632">GET</span><span class="sxs-lookup"><span data-stu-id="3a021-1632">GET</span></span> |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>%27&itemsIds=%27<itemsIds>%27&numberOfResults=<int>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br><span data-ttu-id="3a021-1633">Exemple :</span><span class="sxs-lookup"><span data-stu-id="3a021-1633">Example:</span></span><br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&itemsIds=%271003%27&numberOfResults=10&includeMetadata=false&buildId=50012&apiVersion=%271.0%27` |

| <span data-ttu-id="3a021-1634">Nom du paramètre</span><span class="sxs-lookup"><span data-stu-id="3a021-1634">Parameter Name</span></span> | <span data-ttu-id="3a021-1635">Valeurs valides</span><span class="sxs-lookup"><span data-stu-id="3a021-1635">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-1636">modelId</span><span class="sxs-lookup"><span data-stu-id="3a021-1636">modelId</span></span> |<span data-ttu-id="3a021-1637">Identificateur unique du modèle de hello</span><span class="sxs-lookup"><span data-stu-id="3a021-1637">Unique identifier of hello model</span></span> |
| <span data-ttu-id="3a021-1638">userId</span><span class="sxs-lookup"><span data-stu-id="3a021-1638">userId</span></span> |<span data-ttu-id="3a021-1639">Identificateur unique de l’utilisateur de hello</span><span class="sxs-lookup"><span data-stu-id="3a021-1639">Unique identifier of hello user</span></span> |
| <span data-ttu-id="3a021-1640">itemIds</span><span class="sxs-lookup"><span data-stu-id="3a021-1640">itemIds</span></span> |<span data-ttu-id="3a021-1641">Liste de séparées par des virgules des toorecommend d’éléments hello pour.</span><span class="sxs-lookup"><span data-stu-id="3a021-1641">Comma-separated list of hello items toorecommend for.</span></span> <span data-ttu-id="3a021-1642">Longueur maximale : 1024</span><span class="sxs-lookup"><span data-stu-id="3a021-1642">Max length: 1024</span></span> |
| <span data-ttu-id="3a021-1643">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="3a021-1643">numberOfResults</span></span> |<span data-ttu-id="3a021-1644">Nombre de résultats requis</span><span class="sxs-lookup"><span data-stu-id="3a021-1644">Number of required results</span></span> |
| <span data-ttu-id="3a021-1645">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="3a021-1645">includeMetatadata</span></span> |<span data-ttu-id="3a021-1646">Utilisation ultérieure, toujours false</span><span class="sxs-lookup"><span data-stu-id="3a021-1646">Future use, always false</span></span> |
| <span data-ttu-id="3a021-1647">buildId</span><span class="sxs-lookup"><span data-stu-id="3a021-1647">buildId</span></span> |<span data-ttu-id="3a021-1648">Hello générer toouse id pour cette demande de recommandation</span><span class="sxs-lookup"><span data-stu-id="3a021-1648">hello build id toouse for this recommendation request</span></span> |
| <span data-ttu-id="3a021-1649">apiVersion</span><span class="sxs-lookup"><span data-stu-id="3a021-1649">apiVersion</span></span> |<span data-ttu-id="3a021-1650">1.0</span><span class="sxs-lookup"><span data-stu-id="3a021-1650">1.0</span></span> |

<span data-ttu-id="3a021-1651">**Réponse :**</span><span class="sxs-lookup"><span data-stu-id="3a021-1651">**Response:**</span></span>

<span data-ttu-id="3a021-1652">Code d'état HTTP : 200</span><span class="sxs-lookup"><span data-stu-id="3a021-1652">HTTP Status code: 200</span></span>

<span data-ttu-id="3a021-1653">réponse de Hello comporte une entrée par élément recommandé.</span><span class="sxs-lookup"><span data-stu-id="3a021-1653">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="3a021-1654">Chaque entrée a hello données suivantes :</span><span class="sxs-lookup"><span data-stu-id="3a021-1654">Each entry has hello following data:</span></span>

* <span data-ttu-id="3a021-1655">`Feed\entry\content\properties\Id` : ID d’élément recommandé</span><span class="sxs-lookup"><span data-stu-id="3a021-1655">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="3a021-1656">`Feed\entry\content\properties\Name`-Nom de l’élément de hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-1656">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="3a021-1657">`Feed\entry\content\properties\Rating`-Évaluation de recommandation de hello ; nombre élevé signifie toute confiance.</span><span class="sxs-lookup"><span data-stu-id="3a021-1657">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="3a021-1658">`Feed\entry\content\properties\Reasoning` : raisonnement de la recommandation (par exemple, pour expliquer les recommandations)</span><span class="sxs-lookup"><span data-stu-id="3a021-1658">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="3a021-1659">Pour obtenir un exemple de réponse, consultez la section 12.1.</span><span class="sxs-lookup"><span data-stu-id="3a021-1659">See a response example in 12.1</span></span>

## <a name="13-user-usage-history"></a><span data-ttu-id="3a021-1660">13. Historique d’utilisation de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="3a021-1660">13. User Usage History</span></span>
<span data-ttu-id="3a021-1661">Une fois un modèle de recommandation a été généré hello système autorise tooretrieve hello historique de l’utilisateur (éléments associés tooa utilisateur spécifique) utilisé pour la build de hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-1661">Once a recommendation model was built hello system will allow tooretrieve hello user history (items associated tooa specific user) used for hello build.</span></span>
<span data-ttu-id="3a021-1662">Cette API permettent d’historique de l’utilisateur tooretrieve hello</span><span class="sxs-lookup"><span data-stu-id="3a021-1662">This API allow tooretrieve hello user history</span></span>

<span data-ttu-id="3a021-1663">Remarque : l’historique de l’utilisateur hello est actuellement disponible uniquement pour les builds de recommandation.</span><span class="sxs-lookup"><span data-stu-id="3a021-1663">Note: hello user history is currently available only for recommendation builds.</span></span>

### <a name="131-retrieve-user-history"></a><span data-ttu-id="3a021-1664">13.1 Récupération de l’historique de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="3a021-1664">13.1 Retrieve user history</span></span>
<span data-ttu-id="3a021-1665">Liste de hello de récupération de l’élément utilisé dans hello active générer ou Bonjour spécifié créer pour hello id d’utilisateur donné.</span><span class="sxs-lookup"><span data-stu-id="3a021-1665">Retrieve hello list of item used in hello active build or in hello specified build for hello given user id.</span></span>

| <span data-ttu-id="3a021-1666">Méthode HTTP</span><span class="sxs-lookup"><span data-stu-id="3a021-1666">HTTP Method</span></span> | <span data-ttu-id="3a021-1667">URI</span><span class="sxs-lookup"><span data-stu-id="3a021-1667">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-1668">GET</span><span class="sxs-lookup"><span data-stu-id="3a021-1668">GET</span></span> |<span data-ttu-id="3a021-1669">Obtenir l’historique de l’utilisateur hello pour la build active de hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-1669">Get hello user history for hello active build.</span></span><br/>`<rootURI>/GetUserHistory?modelId=%27<model_id>%27&userId=%27<userId>%27&apiVersion=%271.0%27`<br/><br/><span data-ttu-id="3a021-1670">Obtenir d’historique de l’utilisateur hello pour hello donné de build`<rootURI>/GetUserHistory?modelId=%27<model_id>%27&userId=%27<userId>%27&buildId=<int>&apiVersion=%271.0%27`</span><span class="sxs-lookup"><span data-stu-id="3a021-1670">Get hello user history for hello given build `<rootURI>/GetUserHistory?modelId=%27<model_id>%27&userId=%27<userId>%27&buildId=<int>&apiVersion=%271.0%27`</span></span><br/><br/><span data-ttu-id="3a021-1671">Exemple :`<rootURI>/GetUserHistory?modelId=%2727967136e8-f868-4258-9331-10d567f87fae%27&&userId=%27u_1013%27&apiVersion=%271.0%277`</span><span class="sxs-lookup"><span data-stu-id="3a021-1671">Example:`<rootURI>/GetUserHistory?modelId=%2727967136e8-f868-4258-9331-10d567f87fae%27&&userId=%27u_1013%27&apiVersion=%271.0%277`</span></span> |

| <span data-ttu-id="3a021-1672">Nom du paramètre</span><span class="sxs-lookup"><span data-stu-id="3a021-1672">Parameter Name</span></span> | <span data-ttu-id="3a021-1673">Valeurs valides</span><span class="sxs-lookup"><span data-stu-id="3a021-1673">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-1674">modelId</span><span class="sxs-lookup"><span data-stu-id="3a021-1674">modelId</span></span> |<span data-ttu-id="3a021-1675">Bonjour à l’identificateur unique du modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-1675">hello unique identifier of hello model.</span></span> |
| <span data-ttu-id="3a021-1676">userId</span><span class="sxs-lookup"><span data-stu-id="3a021-1676">userId</span></span> |<span data-ttu-id="3a021-1677">Bonjour identificateur unique de l’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-1677">hello unique identifier of hello user.</span></span> |
| <span data-ttu-id="3a021-1678">buildId</span><span class="sxs-lookup"><span data-stu-id="3a021-1678">buildId</span></span> |<span data-ttu-id="3a021-1679">paramètre facultatif, autoriser tooindicate à partir de la build historique de l’utilisateur hello doit être fetch</span><span class="sxs-lookup"><span data-stu-id="3a021-1679">optional parameter, allow tooindicate from which build hello user history should be fetch</span></span> |
| <span data-ttu-id="3a021-1680">apiVersion</span><span class="sxs-lookup"><span data-stu-id="3a021-1680">apiVersion</span></span> |<span data-ttu-id="3a021-1681">1.0</span><span class="sxs-lookup"><span data-stu-id="3a021-1681">1.0</span></span> |

<span data-ttu-id="3a021-1682">**Réponse :**</span><span class="sxs-lookup"><span data-stu-id="3a021-1682">**Response:**</span></span>

<span data-ttu-id="3a021-1683">Code d'état HTTP : 200</span><span class="sxs-lookup"><span data-stu-id="3a021-1683">HTTP Status code: 200</span></span>

<span data-ttu-id="3a021-1684">réponse de Hello comporte une entrée par élément recommandé.</span><span class="sxs-lookup"><span data-stu-id="3a021-1684">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="3a021-1685">Chaque entrée a hello données suivantes :</span><span class="sxs-lookup"><span data-stu-id="3a021-1685">Each entry has hello following data:</span></span>

* <span data-ttu-id="3a021-1686">`Feed\entry\content\properties\Id` : ID d’élément recommandé</span><span class="sxs-lookup"><span data-stu-id="3a021-1686">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="3a021-1687">`Feed\entry\content\properties\Name`-Nom de l’élément de hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-1687">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="3a021-1688">`Feed\entry\content\properties\Rating` : N/A.</span><span class="sxs-lookup"><span data-stu-id="3a021-1688">`Feed\entry\content\properties\Rating` - N/A.</span></span>
* <span data-ttu-id="3a021-1689">`Feed\entry\content\properties\Reasoning` : N/A.</span><span class="sxs-lookup"><span data-stu-id="3a021-1689">`Feed\entry\content\properties\Reasoning` - N/A.</span></span>

<span data-ttu-id="3a021-1690">OData XML</span><span class="sxs-lookup"><span data-stu-id="3a021-1690">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get User History</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2015-05-26T15:32:47Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">CatalogItemsThatContainATokenEntity</title>
        <updated>2015-05-26T15:32:47Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">2406E770-769C-4189-89DE-1C9283F93A96</d:Id>
                <d:Name m:type="Edm.String">Clara Callan</d:Name>
                <d:Rating m:type="Edm.Double">0</d:Rating>
                <d:Reasoning m:type="Edm.String"/>
                <d:Metadata m:type="Edm.String"/>
                <d:FormattedRating m:type="Edm.Double" m:null="true"/>
            </m:properties>
        </content>
    </entry>
</feed>

## <a name="14-notifications"></a><span data-ttu-id="3a021-1691">14. Notifications</span><span class="sxs-lookup"><span data-stu-id="3a021-1691">14. Notifications</span></span>
<span data-ttu-id="3a021-1692">Recommandations d’apprentissage Machine Azure crée des notifications lorsque des erreurs persistantes se produisent dans le système de hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-1692">Azure Machine Learning Recommendations creates notifications when persistent errors happen in hello system.</span></span> <span data-ttu-id="3a021-1693">Il existe 3 types de notifications :</span><span class="sxs-lookup"><span data-stu-id="3a021-1693">There are 3 types of notifications:</span></span>

1. <span data-ttu-id="3a021-1694">Échec de build : cette notification est déclenchée à chaque échec de build.</span><span class="sxs-lookup"><span data-stu-id="3a021-1694">Build failure - This notification is triggered for every build failure.</span></span>
2. <span data-ttu-id="3a021-1695">Acquisition de données de traitement Échec - cette notification est déclenchée lorsque nous avons plus de 100 erreurs Bonjour 5 dernières minutes dans le traitement des événements d’utilisation par le modèle hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-1695">Data acquisition processing failure - This notification is triggered when we have more than 100 errors in hello last 5 minutes in hello processing of usage events per model.</span></span>
3. <span data-ttu-id="3a021-1696">Échec de la consommation de recommandation - cette notification est déclenchée lorsque nous avons plus de 100 erreurs Bonjour 5 dernières minutes dans le traitement de demandes de recommandation par modèle hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-1696">Recommendation consumption failure - This notification is triggered when we have more than 100 errors in hello last 5 minutes in hello processing of recommendation requests per model.</span></span>

### <a name="141-get-notifications"></a><span data-ttu-id="3a021-1697">14.1.</span><span class="sxs-lookup"><span data-stu-id="3a021-1697">14.1.</span></span> <span data-ttu-id="3a021-1698">Obtention de notifications</span><span class="sxs-lookup"><span data-stu-id="3a021-1698">Get Notifications</span></span>
<span data-ttu-id="3a021-1699">Récupère toutes les notifications hello pour tous les modèles ou d’un modèle unique.</span><span class="sxs-lookup"><span data-stu-id="3a021-1699">Retrieves all hello notifications for all models or for a single model.</span></span>

| <span data-ttu-id="3a021-1700">Méthode HTTP</span><span class="sxs-lookup"><span data-stu-id="3a021-1700">HTTP Method</span></span> | <span data-ttu-id="3a021-1701">URI</span><span class="sxs-lookup"><span data-stu-id="3a021-1701">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-1702">GET</span><span class="sxs-lookup"><span data-stu-id="3a021-1702">GET</span></span> |`<rootURI>/GetNotifications?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="3a021-1703">Obtention de toutes les notifications pour tous les modèles :</span><span class="sxs-lookup"><span data-stu-id="3a021-1703">Getting all notifications for all models:</span></span><br>`<rootURI>/GetNotifications?apiVersion=%271.0%27`<br><br><span data-ttu-id="3a021-1704">Exemple d'obtention des notifications pour un modèle spécifique :</span><span class="sxs-lookup"><span data-stu-id="3a021-1704">Example for getting notifications for a specific model:</span></span><br>`<rootURI>/GetNotifications?modelId=%27967136e8-f868-4258-9331-10d567f87fae%27&apiVersion=%271.0%277` |

| <span data-ttu-id="3a021-1705">Nom du paramètre</span><span class="sxs-lookup"><span data-stu-id="3a021-1705">Parameter Name</span></span> | <span data-ttu-id="3a021-1706">Valeurs valides</span><span class="sxs-lookup"><span data-stu-id="3a021-1706">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-1707">modelId</span><span class="sxs-lookup"><span data-stu-id="3a021-1707">modelId</span></span> |<span data-ttu-id="3a021-1708">Paramètre facultatif.</span><span class="sxs-lookup"><span data-stu-id="3a021-1708">Optional parameter.</span></span> <span data-ttu-id="3a021-1709">Si vous l'omettez, vous obtenez toutes les notifications pour tous les modèles.</span><span class="sxs-lookup"><span data-stu-id="3a021-1709">When omitted, you will get all notifications for all models.</span></span> <br><span data-ttu-id="3a021-1710">Valeur valide : identificateur unique du modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="3a021-1710">Valid value: unique identifier of hello model.</span></span> |
| <span data-ttu-id="3a021-1711">apiVersion</span><span class="sxs-lookup"><span data-stu-id="3a021-1711">apiVersion</span></span> |<span data-ttu-id="3a021-1712">1.0</span><span class="sxs-lookup"><span data-stu-id="3a021-1712">1.0</span></span> |
|  | |
| <span data-ttu-id="3a021-1713">Corps de la requête</span><span class="sxs-lookup"><span data-stu-id="3a021-1713">Request Body</span></span> |<span data-ttu-id="3a021-1714">AUCUN</span><span class="sxs-lookup"><span data-stu-id="3a021-1714">NONE</span></span> |

<span data-ttu-id="3a021-1715">**Réponse :**</span><span class="sxs-lookup"><span data-stu-id="3a021-1715">**Response:**</span></span>

<span data-ttu-id="3a021-1716">Code d'état HTTP : 200</span><span class="sxs-lookup"><span data-stu-id="3a021-1716">HTTP Status code: 200</span></span>

<span data-ttu-id="3a021-1717">OData XML</span><span class="sxs-lookup"><span data-stu-id="3a021-1717">OData XML</span></span>

    hello response includes one entry per notification. Each entry has hello following data:
        * feed\entry\content\properties\UserName - Internal user name identification.
        * feed\entry\content\properties\ModelId - Model ID.
        * feed\entry\content\properties\Message - Notification message.
        * feed\entry\content\properties\DateCreated - Date that this notification was created in UTC format.
        * feed\entry\content\properties\NotificationType - Notification types. Values are BuildFailure, RecommendationFailure, and DataAquisitionFailure.

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get a list of Notifications for a user</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-11-04T13:24:23Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'" />
        <entry>
                <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetAListOfNotificationsForAUserEntity</title>
            <updated>2014-11-04T13:24:23Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:UserName m:type="Edm.String">515506bc-3693-4dce-a5e2-81cb3e8efb56@dm.com</d:UserName>
                    <d:ModelId m:type="Edm.String">967136e8-f868-4258-9331-10d567f87fae</d:ModelId>
                    <d:Message m:type="Edm.String">Build failed for user</d:Message>
                    <d:DateCreated m:type="Edm.String">2014-11-04T13:23:14.383</d:DateCreated>
                    <d:NotificationType m:type="Edm.String">BuildFailure</d:NotificationType>
                </m:properties>
            </content>
        </entry>
    </feed>

### <a name="142-delete-model-notifications"></a><span data-ttu-id="3a021-1718">14.2.</span><span class="sxs-lookup"><span data-stu-id="3a021-1718">14.2.</span></span> <span data-ttu-id="3a021-1719">Suppression de notifications de modèle</span><span class="sxs-lookup"><span data-stu-id="3a021-1719">Delete Model Notifications</span></span>
<span data-ttu-id="3a021-1720">Supprime toutes les notifications lues pour un modèle.</span><span class="sxs-lookup"><span data-stu-id="3a021-1720">Deletes all read notifications for a model.</span></span>

| <span data-ttu-id="3a021-1721">Méthode HTTP</span><span class="sxs-lookup"><span data-stu-id="3a021-1721">HTTP Method</span></span> | <span data-ttu-id="3a021-1722">URI</span><span class="sxs-lookup"><span data-stu-id="3a021-1722">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-1723">SUPPRIMER</span><span class="sxs-lookup"><span data-stu-id="3a021-1723">DELETE</span></span> |`<rootURI>/DeleteModelNotifications?modelId=%<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="3a021-1724">Exemple :</span><span class="sxs-lookup"><span data-stu-id="3a021-1724">Example:</span></span><br>`<rootURI>/DeleteModelNotifications?modelId=%27967136e8-f868-4258-9331-10d567f87fae%27&apiVersion=%271.0%27` |

| <span data-ttu-id="3a021-1725">Nom du paramètre</span><span class="sxs-lookup"><span data-stu-id="3a021-1725">Parameter Name</span></span> | <span data-ttu-id="3a021-1726">Valeurs valides</span><span class="sxs-lookup"><span data-stu-id="3a021-1726">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-1727">modelId</span><span class="sxs-lookup"><span data-stu-id="3a021-1727">modelId</span></span> |<span data-ttu-id="3a021-1728">Identificateur unique du modèle de hello</span><span class="sxs-lookup"><span data-stu-id="3a021-1728">Unique identifier of hello model</span></span> |
| <span data-ttu-id="3a021-1729">apiVersion</span><span class="sxs-lookup"><span data-stu-id="3a021-1729">apiVersion</span></span> |<span data-ttu-id="3a021-1730">1.0</span><span class="sxs-lookup"><span data-stu-id="3a021-1730">1.0</span></span> |
|  | |
| <span data-ttu-id="3a021-1731">Corps de la requête</span><span class="sxs-lookup"><span data-stu-id="3a021-1731">Request Body</span></span> |<span data-ttu-id="3a021-1732">AUCUN</span><span class="sxs-lookup"><span data-stu-id="3a021-1732">NONE</span></span> |

<span data-ttu-id="3a021-1733">**Réponse**:</span><span class="sxs-lookup"><span data-stu-id="3a021-1733">**Response**:</span></span>

<span data-ttu-id="3a021-1734">Code d'état HTTP : 200</span><span class="sxs-lookup"><span data-stu-id="3a021-1734">HTTP Status code: 200</span></span>

### <a name="143-delete-user-notifications"></a><span data-ttu-id="3a021-1735">14.3.</span><span class="sxs-lookup"><span data-stu-id="3a021-1735">14.3.</span></span> <span data-ttu-id="3a021-1736">Suppression de notifications utilisateur</span><span class="sxs-lookup"><span data-stu-id="3a021-1736">Delete User Notifications</span></span>
<span data-ttu-id="3a021-1737">Supprime toutes les notifications pour tous les modèles.</span><span class="sxs-lookup"><span data-stu-id="3a021-1737">Deletes all notifications for all models.</span></span>

| <span data-ttu-id="3a021-1738">Méthode HTTP</span><span class="sxs-lookup"><span data-stu-id="3a021-1738">HTTP Method</span></span> | <span data-ttu-id="3a021-1739">URI</span><span class="sxs-lookup"><span data-stu-id="3a021-1739">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-1740">SUPPRIMER</span><span class="sxs-lookup"><span data-stu-id="3a021-1740">DELETE</span></span> |`<rootURI>/DeleteUserNotifications?apiVersion=%271.0%27` |

| <span data-ttu-id="3a021-1741">Nom du paramètre</span><span class="sxs-lookup"><span data-stu-id="3a021-1741">Parameter Name</span></span> | <span data-ttu-id="3a021-1742">Valeurs valides</span><span class="sxs-lookup"><span data-stu-id="3a021-1742">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a021-1743">apiVersion</span><span class="sxs-lookup"><span data-stu-id="3a021-1743">apiVersion</span></span> |<span data-ttu-id="3a021-1744">1.0</span><span class="sxs-lookup"><span data-stu-id="3a021-1744">1.0</span></span> |
|  | |
| <span data-ttu-id="3a021-1745">Corps de la requête</span><span class="sxs-lookup"><span data-stu-id="3a021-1745">Request Body</span></span> |<span data-ttu-id="3a021-1746">AUCUN</span><span class="sxs-lookup"><span data-stu-id="3a021-1746">NONE</span></span> |

<span data-ttu-id="3a021-1747">**Réponse**:</span><span class="sxs-lookup"><span data-stu-id="3a021-1747">**Response**:</span></span>

<span data-ttu-id="3a021-1748">Code d'état HTTP : 200</span><span class="sxs-lookup"><span data-stu-id="3a021-1748">HTTP Status code: 200</span></span>

## <a name="15-legal"></a><span data-ttu-id="3a021-1749">15. Informations juridiques</span><span class="sxs-lookup"><span data-stu-id="3a021-1749">15. Legal</span></span>
<span data-ttu-id="3a021-1750">Ce document est fourni « en l'état ».</span><span class="sxs-lookup"><span data-stu-id="3a021-1750">This document is provided “as-is”.</span></span> <span data-ttu-id="3a021-1751">Les informations et les points de vue exprimés dans ce document, y compris les URL et autres références à des sites web, peuvent être modifiés sans préavis.</span><span class="sxs-lookup"><span data-stu-id="3a021-1751">Information and views expressed in this document, including URL and other Internet Web site references, may change without notice.</span></span><br><br>
<span data-ttu-id="3a021-1752">Certains exemples sont fournis à titre indicatif uniquement et sont fictifs.</span><span class="sxs-lookup"><span data-stu-id="3a021-1752">Some examples depicted herein are provided for illustration only and are fictitious.</span></span> <span data-ttu-id="3a021-1753">Toute association ou lien est purement involontaire ou fortuit.</span><span class="sxs-lookup"><span data-stu-id="3a021-1753">No real association or connection is intended or should be inferred.</span></span><br><br>
<span data-ttu-id="3a021-1754">Ce document ne fournit pas vous concède tooany de propriété intellectuelle de tout produit Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3a021-1754">This document does not provide you with any legal rights tooany intellectual property in any Microsoft product.</span></span> <span data-ttu-id="3a021-1755">Vous pouvez copier et utiliser ce document pour un usage interne, à titre de référence.</span><span class="sxs-lookup"><span data-stu-id="3a021-1755">You may copy and use this document for your internal, reference purposes.</span></span><br><br>
<span data-ttu-id="3a021-1756">© 2015 Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3a021-1756">© 2015 Microsoft.</span></span> <span data-ttu-id="3a021-1757">Tous droits réservés.</span><span class="sxs-lookup"><span data-stu-id="3a021-1757">All rights reserved.</span></span>

