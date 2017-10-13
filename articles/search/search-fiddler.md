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
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2017
---
# <a name="use-fiddler-to-evaluate-and-test-azure-search-rest-apis"></a>Utilisation de Fiddler pour évaluer et tester les API REST Azure Search
> [!div class="op_single_selector"]
>
> * [Vue d'ensemble](search-query-overview.md)
> * [Explorateur de recherche](search-explorer.md)
> * [Fiddler](search-fiddler.md)
> * [.NET](search-query-dotnet.md)
> * [REST](search-query-rest-api.md)
>
>

Cet article explique comment utiliser Fiddler, disponible en [téléchargement gratuit auprès de Telerik](http://www.telerik.com/fiddler), pour émettre des requêtes HTTP et afficher les réponses à l’aide de l’API REST Azure Search, sans avoir à écrire de code. Azure Search est un service de recherche hébergé sur le cloud entièrement géré, disponible sur Microsoft Azure et facilement programmable via les API .NET et REST. Les API REST du service Azure Search sont documentées sur [MSDN](https://msdn.microsoft.com/library/azure/dn798935.aspx).

Dans les opérations qui suivent, vous allez créer un index, télécharger des documents, interroger l’index, puis interroger le système pour obtenir des informations de service.

Pour effectuer cette procédure, vous avez besoin d'un service Azure Search et `api-key`. Consultez [Création d'un service Azure Search dans le portail](search-create-service-portal.md) pour obtenir des instructions sur la procédure de mise en route.

## <a name="create-an-index"></a>Création d'un index
1. Démarrez Fiddler. Dans le menu **Fichier**, désactivez **Capturer le trafic** pour masquer les activités HTTP externes qui ne sont pas en rapport avec la tâche actuelle.
2. Sous l’onglet **Compositeur** , formulez une demande comparable à la capture d’écran suivante.

      ![][1]
3. Sélectionnez **PUT**.
4. Saisissez une URL qui spécifie l’URL de service, les attributs de la demande et la version de l’API. Voici quelques points à garder à l'esprit :

   * Utilisez le préfixe HTTPS.
   * L'attribut de demande est « /indexes/hotels ». Cela indique à Search de créer un index intitulé « hotels ».
   * La version d’API est en minuscules et elle est spécifiée comme suit : « ?api-version=2016-09-01 ». Les versions d'API sont importantes, car Azure Search déploie régulièrement des mises à jour. En de rares cas, une mise à jour de service peut introduire une modification avec rupture dans l'API. Pour cette raison, Azure Search requiert une version d’api à chaque demande, pour vous donner le contrôle total quant à celle qui est utilisée.

     L’URL complète doit être semblable à celle figurant dans l’exemple suivant :

             https://my-app.search.windows.net/indexes/hotels?api-version=2016-09-01
5. Spécifiez l'en-tête de demande, en remplaçant l'hôte et la clé API par des valeurs qui sont valides pour votre service.

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
6. Dans Corps de la demande, collez les champs qui composent la définition d'index.

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
7. Cliquez sur **Exécuter**.

Patientez quelques secondes pour voir s'afficher une réponse HTTP 201 dans la liste de sessions, ce qui indique que l'index a été créé correctement.

Si vous obtenez HTTP 504, vérifiez que l'URL spécifie HTTPS. Si vous voyez HTTP 400 ou 404, contrôlez le corps de la demande pour vérifier l'absence d'erreurs de copier-coller. HTTP 403 indique normalement qu'il y a un problème avec la clé API (soit la clé n'est pas valide, soit il y a un problème de syntaxe avec la façon dont elle est spécifiée).

## <a name="load-documents"></a>Chargement de documents
Sous l’onglet **Compositeur** , votre demande de publication de documents se présente comme suit. Le corps de la demande contient les données de recherche pour 4 hôtels.

   ![][2]

1. Sélectionnez **POST**.
2. Entrez une URL qui commence par HTTPS, suivie de votre URL de service, suivie de « /indexes/<'indexname'>/docs/index?api-version=2016-09-01 ». L’URL complète doit être semblable à celle figurant dans l’exemple suivant :

         https://my-app.search.windows.net/indexes/hotels/docs/index?api-version=2016-09-01
3. L'en-tête de demande doit être le même qu'avant. Souvenez-vous que vous avez remplacé l'hôte et la clé API par des valeurs qui sont valides pour votre service.

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
4. Le corps de la demande contient quatre documents à ajouter à l'index des hôtels.

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
5. Cliquez sur **Exécuter**.

Après quelques secondes, la réponse HTTP 200 apparaît dans la liste de sessions. Cela indique que les documents ont été correctement créés. Si vous obtenez HTTP 207, cela signifie qu'au moins un document n'a pas pu être chargé. Si HTTP 404 s'affiche, vous avez une erreur de syntaxe dans l'en-tête ou le corps de la demande.

## <a name="query-the-index"></a>Interrogation de l'index
Maintenant qu'un index et des documents sont chargés, vous pouvez émettre des requêtes les concernant.  Sous l’onglet **Compositeur**, une commande **GET** qui interroge votre service se présentera comme dans la capture d’écran qui suit.

   ![][3]

1. Sélectionnez **GET**.
2. Entrez une URL qui commence par HTTPS, suivie de votre URL de service, suivie de « /indexes/<'indexname'>/docs? », suivie de paramètres de requête. Par exemple, utilisez l'URL suivante et remplacez l'exemple de nom d'hôte par celui qui convient à votre service.

         https://my-app.search.windows.net/indexes/hotels/docs?search=motel&facet=category&facet=rating,values:1|2|3|4|5&api-version=2016-09-01

   Cette requête effectue une recherche sur le terme « motel » et extrait les catégories de facette pour les évaluations.
3. L'en-tête de demande doit être le même qu'avant. Souvenez-vous que vous avez remplacé l'hôte et la clé API par des valeurs qui sont valides pour votre service.

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444

Le code de réponse doit correspondre à 200 et la sortie de réponse doit se présenter comme la capture d’écran qui suit.

   ![][4]

L'exemple de requête suivant provient de la page [Opération d'index de recherche (API Azure Search)](http://msdn.microsoft.com/library/dn798927.aspx) sur MSDN. Plusieurs des exemples de requêtes dans cette rubrique comportent des espaces, qui ne sont pas autorisés dans Fiddler. Remplacez chaque espace par un caractère + avant de coller la chaîne de requête et d’essayer la requête dans Fiddler.

**Avant le remplacement des espaces :**

        GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate desc&api-version=2016-09-01

**Après le remplacement des espaces par + :**

        GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate+desc&api-version=2016-09-01

## <a name="query-the-system"></a>Interrogation du système
Vous pouvez également interroger le système pour connaître le nombre de documents et l'espace de stockage utilisé. Sous l’onglet **Compositeur** , votre demande se présentera comme suit et la réponse renverra un comptage du nombre de documents et de l’espace utilisé.

 ![][5]

1. Sélectionnez **GET**.
2. Entrez une URL qui inclut votre URL de service, suivie de « /indexes/hotels/stats?api-version=2016-09-01 » :

         https://my-app.search.windows.net/indexes/hotels/stats?api-version=2016-09-01
3. Spécifiez l'en-tête de demande, en remplaçant l'hôte et la clé API par des valeurs qui sont valides pour votre service.

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
4. Laissez le corps de la demande vide.
5. Cliquez sur **Exécuter**. Le code d'état HTTP 200 doit s'afficher dans la liste de sessions. Sélectionnez l'entrée publiée pour votre commande.
6. Cliquez sur l’onglet **Inspecteurs**, sur l’onglet **En-têtes**, puis sélectionnez le format JSON. Le nombre de documents et la taille de stockage (en Ko) doivent s'afficher.

## <a name="next-steps"></a>Étapes suivantes
Consultez [Gérer votre service Search sur Azure](search-manage.md) pour une approche sans code de la gestion et de l’utilisation d’Azure Search.

<!--Image References-->
[1]: ./media/search-fiddler/AzureSearch_Fiddler1_PutIndex.png
[2]: ./media/search-fiddler/AzureSearch_Fiddler2_PostDocs.png
[3]: ./media/search-fiddler/AzureSearch_Fiddler3_Query.png
[4]: ./media/search-fiddler/AzureSearch_Fiddler4_QueryResults.png
[5]: ./media/search-fiddler/AzureSearch_Fiddler5_QueryStats.png
