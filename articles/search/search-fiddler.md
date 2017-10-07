---
title: "aaaHow toouse Fiddler tooevaluate et tester l’API REST de recherche Azure | Documents Microsoft"
description: "Utilisez Fiddler pour une approche sans code tooverifying Azure rechercher la disponibilité et la tentative de hello API REST."
services: search
documentationcenter: 
author: HeidiSteen
manager: mblythe
editor: 
ms.assetid: 790e5779-c6a3-4a07-9d1e-d6739e6b87d2
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 10/27/2016
ms.author: heidist
ms.openlocfilehash: 2912e1180717d7b40a1e4f7f7f00daf2cc254f0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-fiddler-tooevaluate-and-test-azure-search-rest-apis"></a><span data-ttu-id="59bce-103">Utilisez Fiddler tooevaluate et tester l’API REST de recherche Azure</span><span class="sxs-lookup"><span data-stu-id="59bce-103">Use Fiddler tooevaluate and test Azure Search REST APIs</span></span>
> [!div class="op_single_selector"]
>
> * [<span data-ttu-id="59bce-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="59bce-104">Overview</span></span>](search-query-overview.md)
> * [<span data-ttu-id="59bce-105">Explorateur de recherche</span><span class="sxs-lookup"><span data-stu-id="59bce-105">Search Explorer</span></span>](search-explorer.md)
> * [<span data-ttu-id="59bce-106">Fiddler</span><span class="sxs-lookup"><span data-stu-id="59bce-106">Fiddler</span></span>](search-fiddler.md)
> * [<span data-ttu-id="59bce-107">.NET</span><span class="sxs-lookup"><span data-stu-id="59bce-107">.NET</span></span>](search-query-dotnet.md)
> * [<span data-ttu-id="59bce-108">REST</span><span class="sxs-lookup"><span data-stu-id="59bce-108">REST</span></span>](search-query-rest-api.md)
>
>

<span data-ttu-id="59bce-109">Cet article explique comment toouse Fiddler, disponible en tant qu’un [téléchargement gratuit de Telerik](http://www.telerik.com/fiddler), tooissue HTTP demandes tooand afficher les réponses de l’aide de hello API REST de Azure Search, sans avoir à toowrite n’importe quel code.</span><span class="sxs-lookup"><span data-stu-id="59bce-109">This article explains how toouse Fiddler, available as a [free download from Telerik](http://www.telerik.com/fiddler), tooissue HTTP requests tooand view responses using hello Azure Search REST API, without having toowrite any code.</span></span> <span data-ttu-id="59bce-110">Azure Search est un service de recherche hébergé sur le cloud entièrement géré, disponible sur Microsoft Azure et facilement programmable via les API .NET et REST.</span><span class="sxs-lookup"><span data-stu-id="59bce-110">Azure Search is fully-managed, hosted cloud search service on Microsoft Azure, easily programmable through .NET and REST APIs.</span></span> <span data-ttu-id="59bce-111">Hello service Azure Search API REST sont documentées dans [MSDN](https://msdn.microsoft.com/library/azure/dn798935.aspx).</span><span class="sxs-lookup"><span data-stu-id="59bce-111">hello Azure Search service REST APIs are documented on [MSDN](https://msdn.microsoft.com/library/azure/dn798935.aspx).</span></span>

<span data-ttu-id="59bce-112">Bonjour comme suit, vous allez créer un index, télécharger des documents, index de requête hello et interrogation du système hello pour les informations de service.</span><span class="sxs-lookup"><span data-stu-id="59bce-112">In hello following steps, you'll create an index, upload documents, query hello index, and then query hello system for service information.</span></span>

<span data-ttu-id="59bce-113">toocomplete ces étapes, vous devez un service Azure Search et `api-key`.</span><span class="sxs-lookup"><span data-stu-id="59bce-113">toocomplete these steps, you will need an Azure Search service and `api-key`.</span></span> <span data-ttu-id="59bce-114">Consultez [créer un service Azure Search dans le portail de hello](search-create-service-portal.md) pour obtenir des instructions sur le mode de démarrage tooget.</span><span class="sxs-lookup"><span data-stu-id="59bce-114">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for instructions on how tooget started.</span></span>

## <a name="create-an-index"></a><span data-ttu-id="59bce-115">Création d'un index</span><span class="sxs-lookup"><span data-stu-id="59bce-115">Create an index</span></span>
1. <span data-ttu-id="59bce-116">Démarrez Fiddler.</span><span class="sxs-lookup"><span data-stu-id="59bce-116">Start Fiddler.</span></span> <span data-ttu-id="59bce-117">Sur hello **fichier** menu, désactiver **capturer le trafic** toohide superflus HTTP activité de tâche en cours de toohello non liées.</span><span class="sxs-lookup"><span data-stu-id="59bce-117">On hello **File** menu, turn off **Capture Traffic** toohide extraneous HTTP activity that is unrelated toohello current task.</span></span>
2. <span data-ttu-id="59bce-118">Sur hello **Composer** onglet, vous pouvez formuler une requête qui ressemble à hello suivant capture d’écran.</span><span class="sxs-lookup"><span data-stu-id="59bce-118">On hello **Composer** tab, you'll formulate a request that looks like hello following screen shot.</span></span>

      ![][1]
3. <span data-ttu-id="59bce-119">Sélectionnez **PUT**.</span><span class="sxs-lookup"><span data-stu-id="59bce-119">Select **PUT**.</span></span>
4. <span data-ttu-id="59bce-120">Entrez une URL qui spécifie l’URL du service hello, des attributs de demande et hello api-version.</span><span class="sxs-lookup"><span data-stu-id="59bce-120">Enter a URL that specifies hello service URL, request attributes, and hello api-version.</span></span> <span data-ttu-id="59bce-121">Quelques tookeep de pointeurs à l’esprit :</span><span class="sxs-lookup"><span data-stu-id="59bce-121">A few pointers tookeep in mind:</span></span>

   * <span data-ttu-id="59bce-122">Utiliser HTTPS en tant que préfixe de hello.</span><span class="sxs-lookup"><span data-stu-id="59bce-122">Use HTTPS as hello prefix.</span></span>
   * <span data-ttu-id="59bce-123">L'attribut de demande est « /indexes/hotels ».</span><span class="sxs-lookup"><span data-stu-id="59bce-123">Request attribute is "/indexes/hotels".</span></span> <span data-ttu-id="59bce-124">Recherche toocreate indique à un index nommé « hôtels ».</span><span class="sxs-lookup"><span data-stu-id="59bce-124">This tells Search toocreate an index named 'hotels'.</span></span>
   * <span data-ttu-id="59bce-125">La version d’API est en minuscules et elle est spécifiée comme suit : « ?api-version=2016-09-01 ».</span><span class="sxs-lookup"><span data-stu-id="59bce-125">Api-version is lowercase, specified as "?api-version=2016-09-01".</span></span> <span data-ttu-id="59bce-126">Les versions d'API sont importantes, car Azure Search déploie régulièrement des mises à jour.</span><span class="sxs-lookup"><span data-stu-id="59bce-126">API versions are important because Azure Search deploys updates regularly.</span></span> <span data-ttu-id="59bce-127">Dans de rares occasions, un service de mise à jour peut introduire une toohello de modification avec rupture API.</span><span class="sxs-lookup"><span data-stu-id="59bce-127">On rare occasions, a service update may introduce a breaking change toohello API.</span></span> <span data-ttu-id="59bce-128">Pour cette raison, Azure Search requiert une version d’api à chaque demande, pour vous donner le contrôle total quant à celle qui est utilisée.</span><span class="sxs-lookup"><span data-stu-id="59bce-128">For this reason, Azure Search requires an api-version on each request so that you are in full control over which one is used.</span></span>

     <span data-ttu-id="59bce-129">URL complète de Hello doit ressembler toohello similaire, l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="59bce-129">hello full URL should look similar toohello following example.</span></span>

             https://my-app.search.windows.net/indexes/hotels?api-version=2016-09-01
5. <span data-ttu-id="59bce-130">Spécifiez l’en-tête de demande hello, en remplaçant les hôte hello et clé d’api avec des valeurs qui sont valides pour votre service.</span><span class="sxs-lookup"><span data-stu-id="59bce-130">Specify hello request header, replacing hello host and api-key with values that are valid for your service.</span></span>

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
6. <span data-ttu-id="59bce-131">Dans le corps de la demande, collez dans les champs de hello qui composent la définition de l’index hello.</span><span class="sxs-lookup"><span data-stu-id="59bce-131">In Request Body, paste in hello fields that make up hello index definition.</span></span>

          {
         "name": "hotels",  
         "fields": [
           {"name": "hotelId", "type": "Edm.String", "key":true, "searchable": false},
           {"name": "baseRate", "type": "Edm.Double"},
           {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
           {"name": "hotelName", "type": "Edm.String"},
           {"name": "category", "type": "Edm.String"},
           {"name": "tags", "type": "Collection(Edm.String)"},
           {"name": "parkingIncluded", "type": "Edm.Boolean"},
           {"name": "smokingAllowed", "type": "Edm.Boolean"},
           {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
           {"name": "rating", "type": "Edm.Int32"},
           {"name": "location", "type": "Edm.GeographyPoint"}
          ]
         }
7. <span data-ttu-id="59bce-132">Cliquez sur **Exécuter**.</span><span class="sxs-lookup"><span data-stu-id="59bce-132">Click **Execute**.</span></span>

<span data-ttu-id="59bce-133">En quelques secondes, vous devez voir une réponse HTTP 201 dans la liste des sessions hello, les index hello indiquant a été créé avec succès.</span><span class="sxs-lookup"><span data-stu-id="59bce-133">In a few seconds, you should see an HTTP 201 response in hello session list, indicating hello index was created successfully.</span></span>

<span data-ttu-id="59bce-134">Si vous obtenez HTTP 504, vérifiez que les URL hello Spécifie le protocole HTTPS.</span><span class="sxs-lookup"><span data-stu-id="59bce-134">If you get HTTP 504, verify hello URL specifies HTTPS.</span></span> <span data-ttu-id="59bce-135">Si vous voyez HTTP 400 ou 404, vérifiez la demande hello tooverify corps il en existait pas copier-coller.</span><span class="sxs-lookup"><span data-stu-id="59bce-135">If you see HTTP 400 or 404, check hello request body tooverify there were no copy-paste errors.</span></span> <span data-ttu-id="59bce-136">Un HTTP 403 indique généralement un problème avec hello clé api (une clé non valide ou un problème de syntaxe au niveau de la clé d’api hello est spécifié).</span><span class="sxs-lookup"><span data-stu-id="59bce-136">An HTTP 403 typically indicates a problem with hello api-key (either an invalid key or a syntax problem with how hello api-key is specified).</span></span>

## <a name="load-documents"></a><span data-ttu-id="59bce-137">Chargement de documents</span><span class="sxs-lookup"><span data-stu-id="59bce-137">Load documents</span></span>
<span data-ttu-id="59bce-138">Sur hello **Composer** onglet, vos documents de toopost demande ressemblera hello suivant.</span><span class="sxs-lookup"><span data-stu-id="59bce-138">On hello **Composer** tab, your request toopost documents will look like hello following.</span></span> <span data-ttu-id="59bce-139">corps Hello de demande de hello contient des données de recherche de hello pour les 4 hôtels.</span><span class="sxs-lookup"><span data-stu-id="59bce-139">hello body of hello request contains hello search data for 4 hotels.</span></span>

   ![][2]

1. <span data-ttu-id="59bce-140">Sélectionnez **POST**.</span><span class="sxs-lookup"><span data-stu-id="59bce-140">Select **POST**.</span></span>
2. <span data-ttu-id="59bce-141">Entrez une URL qui commence par HTTPS, suivie de votre URL de service, suivie de « /indexes/<'indexname'>/docs/index?api-version=2016-09-01 ».</span><span class="sxs-lookup"><span data-stu-id="59bce-141">Enter a URL that starts with HTTPS, followed by your service URL, followed by "/indexes/<'indexname'>/docs/index?api-version=2016-09-01".</span></span> <span data-ttu-id="59bce-142">URL complète de Hello doit ressembler toohello similaire, l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="59bce-142">hello full URL should look similar toohello following example.</span></span>

         https://my-app.search.windows.net/indexes/hotels/docs/index?api-version=2016-09-01
3. <span data-ttu-id="59bce-143">En-tête de demande doit être hello même qu’avant.</span><span class="sxs-lookup"><span data-stu-id="59bce-143">Request Header should be hello same as before.</span></span> <span data-ttu-id="59bce-144">N’oubliez pas que vous avez remplacé hôte de hello et clé d’api avec des valeurs qui sont valides pour votre service.</span><span class="sxs-lookup"><span data-stu-id="59bce-144">Remember that you replaced hello host and api-key with values that are valid for your service.</span></span>

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
4. <span data-ttu-id="59bce-145">Hello corps de la demande contient quatre index hôtels de documents toobe toohello ajouté.</span><span class="sxs-lookup"><span data-stu-id="59bce-145">hello Request Body contains four documents toobe added toohello hotels index.</span></span>

         {
         "value": [
         {
             "@search.action": "upload",
             "hotelId": "1",
             "baseRate": 199.0,
             "description": "Best hotel in town",
             "hotelName": "Fancy Stay",
             "category": "Luxury",
             "tags": ["pool", "view", "wifi", "concierge"],
             "parkingIncluded": false,
             "smokingAllowed": false,
             "lastRenovationDate": "2010-06-27T00:00:00Z",
             "rating": 5,
             "location": { "type": "Point", "coordinates": [-122.131577, 47.678581] }
           },
           {
             "@search.action": "upload",
             "hotelId": "2",
             "baseRate": 79.99,
             "description": "Cheapest hotel in town",
             "hotelName": "Roach Motel",
             "category": "Budget",
             "tags": ["motel", "budget"],
             "parkingIncluded": true,
             "smokingAllowed": true,
             "lastRenovationDate": "1982-04-28T00:00:00Z",
             "rating": 1,
             "location": { "type": "Point", "coordinates": [-122.131577, 49.678581] }
           },
           {
             "@search.action": "upload",
             "hotelId": "3",
             "baseRate": 279.99,
             "description": "Surprisingly expensive",
             "hotelName": "Dew Drop Inn",
             "category": "Bed and Breakfast",
             "tags": ["charming", "quaint"],
             "parkingIncluded": true,
             "smokingAllowed": false,
             "lastRenovationDate": null,
             "rating": 4,
             "location": { "type": "Point", "coordinates": [-122.33207, 47.60621] }
           },
           {
             "@search.action": "upload",
             "hotelId": "4",
             "baseRate": 220.00,
             "description": "This could be hello one",
             "hotelName": "A Hotel for Everyone",
             "category": "Basic hotel",
             "tags": ["pool", "wifi"],
             "parkingIncluded": true,
             "smokingAllowed": false,
             "lastRenovationDate": null,
             "rating": 4,
             "location": { "type": "Point", "coordinates": [-122.12151, 47.67399] }
           }
          ]
         }
5. <span data-ttu-id="59bce-146">Cliquez sur **Exécuter**.</span><span class="sxs-lookup"><span data-stu-id="59bce-146">Click **Execute**.</span></span>

<span data-ttu-id="59bce-147">En quelques secondes, vous devez voir une réponse HTTP 200, dans la liste des sessions hello.</span><span class="sxs-lookup"><span data-stu-id="59bce-147">In a few seconds, you should see an HTTP 200 response in hello session list.</span></span> <span data-ttu-id="59bce-148">Cela indique hello documents ont été créés avec succès.</span><span class="sxs-lookup"><span data-stu-id="59bce-148">This indicates hello documents were created successfully.</span></span> <span data-ttu-id="59bce-149">Si vous obtenez un 207, au moins un document échec tooupload.</span><span class="sxs-lookup"><span data-stu-id="59bce-149">If you get a 207, at least one document failed tooupload.</span></span> <span data-ttu-id="59bce-150">Si vous obtenez une erreur 404, vous disposez d’une erreur de syntaxe dans l’en-tête de hello ou de corps de demande de hello.</span><span class="sxs-lookup"><span data-stu-id="59bce-150">If you get a 404, you have a syntax error in either hello header or body of hello request.</span></span>

## <a name="query-hello-index"></a><span data-ttu-id="59bce-151">Index de requête hello</span><span class="sxs-lookup"><span data-stu-id="59bce-151">Query hello index</span></span>
<span data-ttu-id="59bce-152">Maintenant qu'un index et des documents sont chargés, vous pouvez émettre des requêtes les concernant.</span><span class="sxs-lookup"><span data-stu-id="59bce-152">Now that an index and documents are loaded, you can issue queries against them.</span></span>  <span data-ttu-id="59bce-153">Sur hello **Composer** onglet, une **obtenir** commande qui interroge le service recherche similaire toohello suivant capture d’écran.</span><span class="sxs-lookup"><span data-stu-id="59bce-153">On hello **Composer** tab, a **GET** command that queries your service will look similar toohello following screen shot.</span></span>

   ![][3]

1. <span data-ttu-id="59bce-154">Sélectionnez **GET**.</span><span class="sxs-lookup"><span data-stu-id="59bce-154">Select **GET**.</span></span>
2. <span data-ttu-id="59bce-155">Entrez une URL qui commence par HTTPS, suivie de votre URL de service, suivie de « /indexes/<'indexname'>/docs? », suivie de paramètres de requête.</span><span class="sxs-lookup"><span data-stu-id="59bce-155">Enter a URL that starts with HTTPS, followed by your service URL, followed by "/indexes/<'indexname'>/docs?", followed by query parameters.</span></span> <span data-ttu-id="59bce-156">À titre d’exemple, utilisez hello suivant URL, en remplaçant le nom d’hôte exemple hello par un qui n’est valide pour votre service.</span><span class="sxs-lookup"><span data-stu-id="59bce-156">By way of example, use hello following URL, replacing hello sample host name with one that is valid for your service.</span></span>

         https://my-app.search.windows.net/indexes/hotels/docs?search=motel&facet=category&facet=rating,values:1|2|3|4|5&api-version=2016-09-01

   <span data-ttu-id="59bce-157">Cette requête effectue une recherche sur le terme hello « motel » et récupère les catégories de facette pour le classement.</span><span class="sxs-lookup"><span data-stu-id="59bce-157">This query searches on hello term “motel” and retrieves facet categories for ratings.</span></span>
3. <span data-ttu-id="59bce-158">En-tête de demande doit être hello même qu’avant.</span><span class="sxs-lookup"><span data-stu-id="59bce-158">Request Header should be hello same as before.</span></span> <span data-ttu-id="59bce-159">N’oubliez pas que vous avez remplacé hôte de hello et clé d’api avec des valeurs qui sont valides pour votre service.</span><span class="sxs-lookup"><span data-stu-id="59bce-159">Remember that you replaced hello host and api-key with values that are valid for your service.</span></span>

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444

<span data-ttu-id="59bce-160">code de réponse Hello doit être de 200, et sortie de réponse hello doit ressembler toohello similaire après la capture d’écran.</span><span class="sxs-lookup"><span data-stu-id="59bce-160">hello response code should be 200, and hello response output should look similar toohello following screen shot.</span></span>

   ![][4]

<span data-ttu-id="59bce-161">Hello exemple de requête suivant provient de hello [opération d’Index de recherche (API Azure Search)](http://msdn.microsoft.com/library/dn798927.aspx) sur MSDN.</span><span class="sxs-lookup"><span data-stu-id="59bce-161">hello following example query is from hello [Search Index operation (Azure Search API)](http://msdn.microsoft.com/library/dn798927.aspx) on MSDN.</span></span> <span data-ttu-id="59bce-162">Nombre de requêtes d’exemple hello dans cette rubrique incluent des espaces, ce qui ne sont pas autorisés dans Fiddler.</span><span class="sxs-lookup"><span data-stu-id="59bce-162">Many of hello example queries in this topic include spaces, which are not allowed in Fiddler.</span></span> <span data-ttu-id="59bce-163">Remplacez chaque espace avec caractère + avant de la chaîne de requête de collage dans hello avant de tenter de requête hello dans Fiddler.</span><span class="sxs-lookup"><span data-stu-id="59bce-163">Replace each space with a + character before pasting in hello query string before attempting hello query in Fiddler.</span></span>

<span data-ttu-id="59bce-164">**Avant le remplacement des espaces :**</span><span class="sxs-lookup"><span data-stu-id="59bce-164">**Before spaces are replaced:**</span></span>

        GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate desc&api-version=2016-09-01

<span data-ttu-id="59bce-165">**Après le remplacement des espaces par + :**</span><span class="sxs-lookup"><span data-stu-id="59bce-165">**After spaces are replaced with +:**</span></span>

        GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate+desc&api-version=2016-09-01

## <a name="query-hello-system"></a><span data-ttu-id="59bce-166">Interrogation du système hello</span><span class="sxs-lookup"><span data-stu-id="59bce-166">Query hello system</span></span>
<span data-ttu-id="59bce-167">Vous pouvez également interroger hello système tooget stockage et les nombres de consommation de document.</span><span class="sxs-lookup"><span data-stu-id="59bce-167">You can also query hello system tooget document counts and storage consumption.</span></span> <span data-ttu-id="59bce-168">Sur hello **Composer** , votre demande de recherche similaire toohello suivantes, puis hello réponse renvoie un nombre pour le nombre de hello de documents et l’espace utilisé.</span><span class="sxs-lookup"><span data-stu-id="59bce-168">On hello **Composer** tab, your request will look similar toohello following, and hello response will return a count for hello number of documents and space used.</span></span>

 ![][5]

1. <span data-ttu-id="59bce-169">Sélectionnez **GET**.</span><span class="sxs-lookup"><span data-stu-id="59bce-169">Select **GET**.</span></span>
2. <span data-ttu-id="59bce-170">Entrez une URL qui inclut votre URL de service, suivie de « /indexes/hotels/stats?api-version=2016-09-01 » :</span><span class="sxs-lookup"><span data-stu-id="59bce-170">Enter a URL that includes your service URL, followed by "/indexes/hotels/stats?api-version=2016-09-01":</span></span>

         https://my-app.search.windows.net/indexes/hotels/stats?api-version=2016-09-01
3. <span data-ttu-id="59bce-171">Spécifiez l’en-tête de demande hello, en remplaçant les hôte hello et clé d’api avec des valeurs qui sont valides pour votre service.</span><span class="sxs-lookup"><span data-stu-id="59bce-171">Specify hello request header, replacing hello host and api-key with values that are valid for your service.</span></span>

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
4. <span data-ttu-id="59bce-172">Laissez le corps de la demande hello vide.</span><span class="sxs-lookup"><span data-stu-id="59bce-172">Leave hello request body empty.</span></span>
5. <span data-ttu-id="59bce-173">Cliquez sur **Exécuter**.</span><span class="sxs-lookup"><span data-stu-id="59bce-173">Click **Execute**.</span></span> <span data-ttu-id="59bce-174">Vous devez voir un code d’état HTTP 200 dans la liste des sessions hello.</span><span class="sxs-lookup"><span data-stu-id="59bce-174">You should see an HTTP 200 status code in hello session list.</span></span> <span data-ttu-id="59bce-175">Sélectionnez entrée hello validée pour votre commande.</span><span class="sxs-lookup"><span data-stu-id="59bce-175">Select hello entry posted for your command.</span></span>
6. <span data-ttu-id="59bce-176">Cliquez sur hello **inspecteurs** , cliquez sur hello **en-têtes** onglet et le format JSON hello puis sélectionnez.</span><span class="sxs-lookup"><span data-stu-id="59bce-176">Click hello **Inspectors** tab, click hello **Headers** tab, and then select hello JSON format.</span></span> <span data-ttu-id="59bce-177">Vous devez voir hello document nombre et taille du stockage (en Ko).</span><span class="sxs-lookup"><span data-stu-id="59bce-177">You should see hello document count and storage size (in KB).</span></span>

## <a name="next-steps"></a><span data-ttu-id="59bce-178">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="59bce-178">Next steps</span></span>
<span data-ttu-id="59bce-179">Consultez [gérer votre service de recherche sur Azure](search-manage.md) pour un toomanaging sans code approche et à l’aide d’Azure Search.</span><span class="sxs-lookup"><span data-stu-id="59bce-179">See [Manage your Search service on Azure](search-manage.md) for a no-code approach toomanaging and using Azure Search.</span></span>

<!--Image References-->
[1]: ./media/search-fiddler/AzureSearch_Fiddler1_PutIndex.png
[2]: ./media/search-fiddler/AzureSearch_Fiddler2_PostDocs.png
[3]: ./media/search-fiddler/AzureSearch_Fiddler3_Query.png
[4]: ./media/search-fiddler/AzureSearch_Fiddler4_QueryResults.png
[5]: ./media/search-fiddler/AzureSearch_Fiddler5_QueryStats.png
