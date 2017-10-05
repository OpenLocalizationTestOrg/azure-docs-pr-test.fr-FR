---
title: "Utilisation de Fiddler pour évaluer et tester les API REST du service Recherche Azure | Microsoft Docs"
description: "Utilisation de Fiddler dans une approche sans code pour vérifier la disponibilité d'Azure Search et tester les API REST."
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
ms.openlocfilehash: c38b73fa69bee34ce2434c6274cb017c99ef3c35
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-fiddler-to-evaluate-and-test-azure-search-rest-apis"></a><span data-ttu-id="b12b0-103">Utilisation de Fiddler pour évaluer et tester les API REST Azure Search</span><span class="sxs-lookup"><span data-stu-id="b12b0-103">Use Fiddler to evaluate and test Azure Search REST APIs</span></span>
> [!div class="op_single_selector"]
>
> * [<span data-ttu-id="b12b0-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="b12b0-104">Overview</span></span>](search-query-overview.md)
> * [<span data-ttu-id="b12b0-105">Explorateur de recherche</span><span class="sxs-lookup"><span data-stu-id="b12b0-105">Search Explorer</span></span>](search-explorer.md)
> * [<span data-ttu-id="b12b0-106">Fiddler</span><span class="sxs-lookup"><span data-stu-id="b12b0-106">Fiddler</span></span>](search-fiddler.md)
> * [<span data-ttu-id="b12b0-107">.NET</span><span class="sxs-lookup"><span data-stu-id="b12b0-107">.NET</span></span>](search-query-dotnet.md)
> * [<span data-ttu-id="b12b0-108">REST</span><span class="sxs-lookup"><span data-stu-id="b12b0-108">REST</span></span>](search-query-rest-api.md)
>
>

<span data-ttu-id="b12b0-109">Cet article explique comment utiliser Fiddler, disponible en [téléchargement gratuit auprès de Telerik](http://www.telerik.com/fiddler), pour émettre des requêtes HTTP et afficher les réponses à l’aide de l’API REST Azure Search, sans avoir à écrire de code.</span><span class="sxs-lookup"><span data-stu-id="b12b0-109">This article explains how to use Fiddler, available as a [free download from Telerik](http://www.telerik.com/fiddler), to issue HTTP requests to and view responses using the Azure Search REST API, without having to write any code.</span></span> <span data-ttu-id="b12b0-110">Azure Search est un service de recherche hébergé sur le cloud entièrement géré, disponible sur Microsoft Azure et facilement programmable via les API .NET et REST.</span><span class="sxs-lookup"><span data-stu-id="b12b0-110">Azure Search is fully-managed, hosted cloud search service on Microsoft Azure, easily programmable through .NET and REST APIs.</span></span> <span data-ttu-id="b12b0-111">Les API REST du service Azure Search sont documentées sur [MSDN](https://msdn.microsoft.com/library/azure/dn798935.aspx).</span><span class="sxs-lookup"><span data-stu-id="b12b0-111">The Azure Search service REST APIs are documented on [MSDN](https://msdn.microsoft.com/library/azure/dn798935.aspx).</span></span>

<span data-ttu-id="b12b0-112">Dans les opérations qui suivent, vous allez créer un index, télécharger des documents, interroger l’index, puis interroger le système pour obtenir des informations de service.</span><span class="sxs-lookup"><span data-stu-id="b12b0-112">In the following steps, you'll create an index, upload documents, query the index, and then query the system for service information.</span></span>

<span data-ttu-id="b12b0-113">Pour effectuer cette procédure, vous avez besoin d'un service Azure Search et `api-key`.</span><span class="sxs-lookup"><span data-stu-id="b12b0-113">To complete these steps, you will need an Azure Search service and `api-key`.</span></span> <span data-ttu-id="b12b0-114">Consultez [Création d'un service Azure Search dans le portail](search-create-service-portal.md) pour obtenir des instructions sur la procédure de mise en route.</span><span class="sxs-lookup"><span data-stu-id="b12b0-114">See [Create an Azure Search service in the portal](search-create-service-portal.md) for instructions on how to get started.</span></span>

## <a name="create-an-index"></a><span data-ttu-id="b12b0-115">Création d'un index</span><span class="sxs-lookup"><span data-stu-id="b12b0-115">Create an index</span></span>
1. <span data-ttu-id="b12b0-116">Démarrez Fiddler.</span><span class="sxs-lookup"><span data-stu-id="b12b0-116">Start Fiddler.</span></span> <span data-ttu-id="b12b0-117">Dans le menu **Fichier**, désactivez **Capturer le trafic** pour masquer les activités HTTP externes qui ne sont pas en rapport avec la tâche actuelle.</span><span class="sxs-lookup"><span data-stu-id="b12b0-117">On the **File** menu, turn off **Capture Traffic** to hide extraneous HTTP activity that is unrelated to the current task.</span></span>
2. <span data-ttu-id="b12b0-118">Sous l’onglet **Compositeur** , formulez une demande comparable à la capture d’écran suivante.</span><span class="sxs-lookup"><span data-stu-id="b12b0-118">On the **Composer** tab, you'll formulate a request that looks like the following screen shot.</span></span>

      ![][1]
3. <span data-ttu-id="b12b0-119">Sélectionnez **PUT**.</span><span class="sxs-lookup"><span data-stu-id="b12b0-119">Select **PUT**.</span></span>
4. <span data-ttu-id="b12b0-120">Saisissez une URL qui spécifie l’URL de service, les attributs de la demande et la version de l’API.</span><span class="sxs-lookup"><span data-stu-id="b12b0-120">Enter a URL that specifies the service URL, request attributes, and the api-version.</span></span> <span data-ttu-id="b12b0-121">Voici quelques points à garder à l'esprit :</span><span class="sxs-lookup"><span data-stu-id="b12b0-121">A few pointers to keep in mind:</span></span>

   * <span data-ttu-id="b12b0-122">Utilisez le préfixe HTTPS.</span><span class="sxs-lookup"><span data-stu-id="b12b0-122">Use HTTPS as the prefix.</span></span>
   * <span data-ttu-id="b12b0-123">L'attribut de demande est « /indexes/hotels ».</span><span class="sxs-lookup"><span data-stu-id="b12b0-123">Request attribute is "/indexes/hotels".</span></span> <span data-ttu-id="b12b0-124">Cela indique à Search de créer un index intitulé « hotels ».</span><span class="sxs-lookup"><span data-stu-id="b12b0-124">This tells Search to create an index named 'hotels'.</span></span>
   * <span data-ttu-id="b12b0-125">La version d’API est en minuscules et elle est spécifiée comme suit : « ?api-version=2016-09-01 ».</span><span class="sxs-lookup"><span data-stu-id="b12b0-125">Api-version is lowercase, specified as "?api-version=2016-09-01".</span></span> <span data-ttu-id="b12b0-126">Les versions d'API sont importantes, car Azure Search déploie régulièrement des mises à jour.</span><span class="sxs-lookup"><span data-stu-id="b12b0-126">API versions are important because Azure Search deploys updates regularly.</span></span> <span data-ttu-id="b12b0-127">En de rares cas, une mise à jour de service peut introduire une modification avec rupture dans l'API.</span><span class="sxs-lookup"><span data-stu-id="b12b0-127">On rare occasions, a service update may introduce a breaking change to the API.</span></span> <span data-ttu-id="b12b0-128">Pour cette raison, Azure Search requiert une version d’api à chaque demande, pour vous donner le contrôle total quant à celle qui est utilisée.</span><span class="sxs-lookup"><span data-stu-id="b12b0-128">For this reason, Azure Search requires an api-version on each request so that you are in full control over which one is used.</span></span>

     <span data-ttu-id="b12b0-129">L’URL complète doit être semblable à celle figurant dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="b12b0-129">The full URL should look similar to the following example.</span></span>

             https://my-app.search.windows.net/indexes/hotels?api-version=2016-09-01
5. <span data-ttu-id="b12b0-130">Spécifiez l'en-tête de demande, en remplaçant l'hôte et la clé API par des valeurs qui sont valides pour votre service.</span><span class="sxs-lookup"><span data-stu-id="b12b0-130">Specify the request header, replacing the host and api-key with values that are valid for your service.</span></span>

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
6. <span data-ttu-id="b12b0-131">Dans Corps de la demande, collez les champs qui composent la définition d'index.</span><span class="sxs-lookup"><span data-stu-id="b12b0-131">In Request Body, paste in the fields that make up the index definition.</span></span>

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
7. <span data-ttu-id="b12b0-132">Cliquez sur **Exécuter**.</span><span class="sxs-lookup"><span data-stu-id="b12b0-132">Click **Execute**.</span></span>

<span data-ttu-id="b12b0-133">Patientez quelques secondes pour voir s'afficher une réponse HTTP 201 dans la liste de sessions, ce qui indique que l'index a été créé correctement.</span><span class="sxs-lookup"><span data-stu-id="b12b0-133">In a few seconds, you should see an HTTP 201 response in the session list, indicating the index was created successfully.</span></span>

<span data-ttu-id="b12b0-134">Si vous obtenez HTTP 504, vérifiez que l'URL spécifie HTTPS.</span><span class="sxs-lookup"><span data-stu-id="b12b0-134">If you get HTTP 504, verify the URL specifies HTTPS.</span></span> <span data-ttu-id="b12b0-135">Si vous voyez HTTP 400 ou 404, contrôlez le corps de la demande pour vérifier l'absence d'erreurs de copier-coller.</span><span class="sxs-lookup"><span data-stu-id="b12b0-135">If you see HTTP 400 or 404, check the request body to verify there were no copy-paste errors.</span></span> <span data-ttu-id="b12b0-136">HTTP 403 indique normalement qu'il y a un problème avec la clé API (soit la clé n'est pas valide, soit il y a un problème de syntaxe avec la façon dont elle est spécifiée).</span><span class="sxs-lookup"><span data-stu-id="b12b0-136">An HTTP 403 typically indicates a problem with the api-key (either an invalid key or a syntax problem with how the api-key is specified).</span></span>

## <a name="load-documents"></a><span data-ttu-id="b12b0-137">Chargement de documents</span><span class="sxs-lookup"><span data-stu-id="b12b0-137">Load documents</span></span>
<span data-ttu-id="b12b0-138">Sous l’onglet **Compositeur** , votre demande de publication de documents se présente comme suit.</span><span class="sxs-lookup"><span data-stu-id="b12b0-138">On the **Composer** tab, your request to post documents will look like the following.</span></span> <span data-ttu-id="b12b0-139">Le corps de la demande contient les données de recherche pour 4 hôtels.</span><span class="sxs-lookup"><span data-stu-id="b12b0-139">The body of the request contains the search data for 4 hotels.</span></span>

   ![][2]

1. <span data-ttu-id="b12b0-140">Sélectionnez **POST**.</span><span class="sxs-lookup"><span data-stu-id="b12b0-140">Select **POST**.</span></span>
2. <span data-ttu-id="b12b0-141">Entrez une URL qui commence par HTTPS, suivie de votre URL de service, suivie de « /indexes/<'indexname'>/docs/index?api-version=2016-09-01 ».</span><span class="sxs-lookup"><span data-stu-id="b12b0-141">Enter a URL that starts with HTTPS, followed by your service URL, followed by "/indexes/<'indexname'>/docs/index?api-version=2016-09-01".</span></span> <span data-ttu-id="b12b0-142">L’URL complète doit être semblable à celle figurant dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="b12b0-142">The full URL should look similar to the following example.</span></span>

         https://my-app.search.windows.net/indexes/hotels/docs/index?api-version=2016-09-01
3. <span data-ttu-id="b12b0-143">L'en-tête de demande doit être le même qu'avant.</span><span class="sxs-lookup"><span data-stu-id="b12b0-143">Request Header should be the same as before.</span></span> <span data-ttu-id="b12b0-144">Souvenez-vous que vous avez remplacé l'hôte et la clé API par des valeurs qui sont valides pour votre service.</span><span class="sxs-lookup"><span data-stu-id="b12b0-144">Remember that you replaced the host and api-key with values that are valid for your service.</span></span>

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
4. <span data-ttu-id="b12b0-145">Le corps de la demande contient quatre documents à ajouter à l'index des hôtels.</span><span class="sxs-lookup"><span data-stu-id="b12b0-145">The Request Body contains four documents to be added to the hotels index.</span></span>

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
             "description": "This could be the one",
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
5. <span data-ttu-id="b12b0-146">Cliquez sur **Exécuter**.</span><span class="sxs-lookup"><span data-stu-id="b12b0-146">Click **Execute**.</span></span>

<span data-ttu-id="b12b0-147">Après quelques secondes, la réponse HTTP 200 apparaît dans la liste de sessions.</span><span class="sxs-lookup"><span data-stu-id="b12b0-147">In a few seconds, you should see an HTTP 200 response in the session list.</span></span> <span data-ttu-id="b12b0-148">Cela indique que les documents ont été correctement créés.</span><span class="sxs-lookup"><span data-stu-id="b12b0-148">This indicates the documents were created successfully.</span></span> <span data-ttu-id="b12b0-149">Si vous obtenez HTTP 207, cela signifie qu'au moins un document n'a pas pu être chargé.</span><span class="sxs-lookup"><span data-stu-id="b12b0-149">If you get a 207, at least one document failed to upload.</span></span> <span data-ttu-id="b12b0-150">Si HTTP 404 s'affiche, vous avez une erreur de syntaxe dans l'en-tête ou le corps de la demande.</span><span class="sxs-lookup"><span data-stu-id="b12b0-150">If you get a 404, you have a syntax error in either the header or body of the request.</span></span>

## <a name="query-the-index"></a><span data-ttu-id="b12b0-151">Interrogation de l'index</span><span class="sxs-lookup"><span data-stu-id="b12b0-151">Query the index</span></span>
<span data-ttu-id="b12b0-152">Maintenant qu'un index et des documents sont chargés, vous pouvez émettre des requêtes les concernant.</span><span class="sxs-lookup"><span data-stu-id="b12b0-152">Now that an index and documents are loaded, you can issue queries against them.</span></span>  <span data-ttu-id="b12b0-153">Sous l’onglet **Compositeur**, une commande **GET** qui interroge votre service se présentera comme dans la capture d’écran qui suit.</span><span class="sxs-lookup"><span data-stu-id="b12b0-153">On the **Composer** tab, a **GET** command that queries your service will look similar to the following screen shot.</span></span>

   ![][3]

1. <span data-ttu-id="b12b0-154">Sélectionnez **GET**.</span><span class="sxs-lookup"><span data-stu-id="b12b0-154">Select **GET**.</span></span>
2. <span data-ttu-id="b12b0-155">Entrez une URL qui commence par HTTPS, suivie de votre URL de service, suivie de « /indexes/<'indexname'>/docs? », suivie de paramètres de requête.</span><span class="sxs-lookup"><span data-stu-id="b12b0-155">Enter a URL that starts with HTTPS, followed by your service URL, followed by "/indexes/<'indexname'>/docs?", followed by query parameters.</span></span> <span data-ttu-id="b12b0-156">Par exemple, utilisez l'URL suivante et remplacez l'exemple de nom d'hôte par celui qui convient à votre service.</span><span class="sxs-lookup"><span data-stu-id="b12b0-156">By way of example, use the following URL, replacing the sample host name with one that is valid for your service.</span></span>

         https://my-app.search.windows.net/indexes/hotels/docs?search=motel&facet=category&facet=rating,values:1|2|3|4|5&api-version=2016-09-01

   <span data-ttu-id="b12b0-157">Cette requête effectue une recherche sur le terme « motel » et extrait les catégories de facette pour les évaluations.</span><span class="sxs-lookup"><span data-stu-id="b12b0-157">This query searches on the term “motel” and retrieves facet categories for ratings.</span></span>
3. <span data-ttu-id="b12b0-158">L'en-tête de demande doit être le même qu'avant.</span><span class="sxs-lookup"><span data-stu-id="b12b0-158">Request Header should be the same as before.</span></span> <span data-ttu-id="b12b0-159">Souvenez-vous que vous avez remplacé l'hôte et la clé API par des valeurs qui sont valides pour votre service.</span><span class="sxs-lookup"><span data-stu-id="b12b0-159">Remember that you replaced the host and api-key with values that are valid for your service.</span></span>

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444

<span data-ttu-id="b12b0-160">Le code de réponse doit correspondre à 200 et la sortie de réponse doit se présenter comme la capture d’écran qui suit.</span><span class="sxs-lookup"><span data-stu-id="b12b0-160">The response code should be 200, and the response output should look similar to the following screen shot.</span></span>

   ![][4]

<span data-ttu-id="b12b0-161">L'exemple de requête suivant provient de la page [Opération d'index de recherche (API Azure Search)](http://msdn.microsoft.com/library/dn798927.aspx) sur MSDN.</span><span class="sxs-lookup"><span data-stu-id="b12b0-161">The following example query is from the [Search Index operation (Azure Search API)](http://msdn.microsoft.com/library/dn798927.aspx) on MSDN.</span></span> <span data-ttu-id="b12b0-162">Plusieurs des exemples de requêtes dans cette rubrique comportent des espaces, qui ne sont pas autorisés dans Fiddler.</span><span class="sxs-lookup"><span data-stu-id="b12b0-162">Many of the example queries in this topic include spaces, which are not allowed in Fiddler.</span></span> <span data-ttu-id="b12b0-163">Remplacez chaque espace par un caractère + avant de coller la chaîne de requête et d’essayer la requête dans Fiddler.</span><span class="sxs-lookup"><span data-stu-id="b12b0-163">Replace each space with a + character before pasting in the query string before attempting the query in Fiddler.</span></span>

<span data-ttu-id="b12b0-164">**Avant le remplacement des espaces :**</span><span class="sxs-lookup"><span data-stu-id="b12b0-164">**Before spaces are replaced:**</span></span>

        GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate desc&api-version=2016-09-01

<span data-ttu-id="b12b0-165">**Après le remplacement des espaces par + :**</span><span class="sxs-lookup"><span data-stu-id="b12b0-165">**After spaces are replaced with +:**</span></span>

        GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate+desc&api-version=2016-09-01

## <a name="query-the-system"></a><span data-ttu-id="b12b0-166">Interrogation du système</span><span class="sxs-lookup"><span data-stu-id="b12b0-166">Query the system</span></span>
<span data-ttu-id="b12b0-167">Vous pouvez également interroger le système pour connaître le nombre de documents et l'espace de stockage utilisé.</span><span class="sxs-lookup"><span data-stu-id="b12b0-167">You can also query the system to get document counts and storage consumption.</span></span> <span data-ttu-id="b12b0-168">Sous l’onglet **Compositeur** , votre demande se présentera comme suit et la réponse renverra un comptage du nombre de documents et de l’espace utilisé.</span><span class="sxs-lookup"><span data-stu-id="b12b0-168">On the **Composer** tab, your request will look similar to the following, and the response will return a count for the number of documents and space used.</span></span>

 ![][5]

1. <span data-ttu-id="b12b0-169">Sélectionnez **GET**.</span><span class="sxs-lookup"><span data-stu-id="b12b0-169">Select **GET**.</span></span>
2. <span data-ttu-id="b12b0-170">Entrez une URL qui inclut votre URL de service, suivie de « /indexes/hotels/stats?api-version=2016-09-01 » :</span><span class="sxs-lookup"><span data-stu-id="b12b0-170">Enter a URL that includes your service URL, followed by "/indexes/hotels/stats?api-version=2016-09-01":</span></span>

         https://my-app.search.windows.net/indexes/hotels/stats?api-version=2016-09-01
3. <span data-ttu-id="b12b0-171">Spécifiez l'en-tête de demande, en remplaçant l'hôte et la clé API par des valeurs qui sont valides pour votre service.</span><span class="sxs-lookup"><span data-stu-id="b12b0-171">Specify the request header, replacing the host and api-key with values that are valid for your service.</span></span>

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
4. <span data-ttu-id="b12b0-172">Laissez le corps de la demande vide.</span><span class="sxs-lookup"><span data-stu-id="b12b0-172">Leave the request body empty.</span></span>
5. <span data-ttu-id="b12b0-173">Cliquez sur **Exécuter**.</span><span class="sxs-lookup"><span data-stu-id="b12b0-173">Click **Execute**.</span></span> <span data-ttu-id="b12b0-174">Le code d'état HTTP 200 doit s'afficher dans la liste de sessions.</span><span class="sxs-lookup"><span data-stu-id="b12b0-174">You should see an HTTP 200 status code in the session list.</span></span> <span data-ttu-id="b12b0-175">Sélectionnez l'entrée publiée pour votre commande.</span><span class="sxs-lookup"><span data-stu-id="b12b0-175">Select the entry posted for your command.</span></span>
6. <span data-ttu-id="b12b0-176">Cliquez sur l’onglet **Inspecteurs**, sur l’onglet **En-têtes**, puis sélectionnez le format JSON.</span><span class="sxs-lookup"><span data-stu-id="b12b0-176">Click the **Inspectors** tab, click the **Headers** tab, and then select the JSON format.</span></span> <span data-ttu-id="b12b0-177">Le nombre de documents et la taille de stockage (en Ko) doivent s'afficher.</span><span class="sxs-lookup"><span data-stu-id="b12b0-177">You should see the document count and storage size (in KB).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b12b0-178">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b12b0-178">Next steps</span></span>
<span data-ttu-id="b12b0-179">Consultez [Gérer votre service Search sur Azure](search-manage.md) pour une approche sans code de la gestion et de l’utilisation d’Azure Search.</span><span class="sxs-lookup"><span data-stu-id="b12b0-179">See [Manage your Search service on Azure](search-manage.md) for a no-code approach to managing and using Azure Search.</span></span>

<!--Image References-->
[1]: ./media/search-fiddler/AzureSearch_Fiddler1_PutIndex.png
[2]: ./media/search-fiddler/AzureSearch_Fiddler2_PostDocs.png
[3]: ./media/search-fiddler/AzureSearch_Fiddler3_Query.png
[4]: ./media/search-fiddler/AzureSearch_Fiddler4_QueryResults.png
[5]: ./media/search-fiddler/AzureSearch_Fiddler5_QueryStats.png
