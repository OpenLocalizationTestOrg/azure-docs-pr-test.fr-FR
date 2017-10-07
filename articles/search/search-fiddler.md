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
# <a name="use-fiddler-tooevaluate-and-test-azure-search-rest-apis"></a>Utilisez Fiddler tooevaluate et tester l’API REST de recherche Azure
> [!div class="op_single_selector"]
>
> * [Vue d'ensemble](search-query-overview.md)
> * [Explorateur de recherche](search-explorer.md)
> * [Fiddler](search-fiddler.md)
> * [.NET](search-query-dotnet.md)
> * [REST](search-query-rest-api.md)
>
>

Cet article explique comment toouse Fiddler, disponible en tant qu’un [téléchargement gratuit de Telerik](http://www.telerik.com/fiddler), tooissue HTTP demandes tooand afficher les réponses de l’aide de hello API REST de Azure Search, sans avoir à toowrite n’importe quel code. Azure Search est un service de recherche hébergé sur le cloud entièrement géré, disponible sur Microsoft Azure et facilement programmable via les API .NET et REST. Hello service Azure Search API REST sont documentées dans [MSDN](https://msdn.microsoft.com/library/azure/dn798935.aspx).

Bonjour comme suit, vous allez créer un index, télécharger des documents, index de requête hello et interrogation du système hello pour les informations de service.

toocomplete ces étapes, vous devez un service Azure Search et `api-key`. Consultez [créer un service Azure Search dans le portail de hello](search-create-service-portal.md) pour obtenir des instructions sur le mode de démarrage tooget.

## <a name="create-an-index"></a>Création d'un index
1. Démarrez Fiddler. Sur hello **fichier** menu, désactiver **capturer le trafic** toohide superflus HTTP activité de tâche en cours de toohello non liées.
2. Sur hello **Composer** onglet, vous pouvez formuler une requête qui ressemble à hello suivant capture d’écran.

      ![][1]
3. Sélectionnez **PUT**.
4. Entrez une URL qui spécifie l’URL du service hello, des attributs de demande et hello api-version. Quelques tookeep de pointeurs à l’esprit :

   * Utiliser HTTPS en tant que préfixe de hello.
   * L'attribut de demande est « /indexes/hotels ». Recherche toocreate indique à un index nommé « hôtels ».
   * La version d’API est en minuscules et elle est spécifiée comme suit : « ?api-version=2016-09-01 ». Les versions d'API sont importantes, car Azure Search déploie régulièrement des mises à jour. Dans de rares occasions, un service de mise à jour peut introduire une toohello de modification avec rupture API. Pour cette raison, Azure Search requiert une version d’api à chaque demande, pour vous donner le contrôle total quant à celle qui est utilisée.

     URL complète de Hello doit ressembler toohello similaire, l’exemple suivant.

             https://my-app.search.windows.net/indexes/hotels?api-version=2016-09-01
5. Spécifiez l’en-tête de demande hello, en remplaçant les hôte hello et clé d’api avec des valeurs qui sont valides pour votre service.

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
6. Dans le corps de la demande, collez dans les champs de hello qui composent la définition de l’index hello.

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

En quelques secondes, vous devez voir une réponse HTTP 201 dans la liste des sessions hello, les index hello indiquant a été créé avec succès.

Si vous obtenez HTTP 504, vérifiez que les URL hello Spécifie le protocole HTTPS. Si vous voyez HTTP 400 ou 404, vérifiez la demande hello tooverify corps il en existait pas copier-coller. Un HTTP 403 indique généralement un problème avec hello clé api (une clé non valide ou un problème de syntaxe au niveau de la clé d’api hello est spécifié).

## <a name="load-documents"></a>Chargement de documents
Sur hello **Composer** onglet, vos documents de toopost demande ressemblera hello suivant. corps Hello de demande de hello contient des données de recherche de hello pour les 4 hôtels.

   ![][2]

1. Sélectionnez **POST**.
2. Entrez une URL qui commence par HTTPS, suivie de votre URL de service, suivie de « /indexes/<'indexname'>/docs/index?api-version=2016-09-01 ». URL complète de Hello doit ressembler toohello similaire, l’exemple suivant.

         https://my-app.search.windows.net/indexes/hotels/docs/index?api-version=2016-09-01
3. En-tête de demande doit être hello même qu’avant. N’oubliez pas que vous avez remplacé hôte de hello et clé d’api avec des valeurs qui sont valides pour votre service.

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
4. Hello corps de la demande contient quatre index hôtels de documents toobe toohello ajouté.

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
5. Cliquez sur **Exécuter**.

En quelques secondes, vous devez voir une réponse HTTP 200, dans la liste des sessions hello. Cela indique hello documents ont été créés avec succès. Si vous obtenez un 207, au moins un document échec tooupload. Si vous obtenez une erreur 404, vous disposez d’une erreur de syntaxe dans l’en-tête de hello ou de corps de demande de hello.

## <a name="query-hello-index"></a>Index de requête hello
Maintenant qu'un index et des documents sont chargés, vous pouvez émettre des requêtes les concernant.  Sur hello **Composer** onglet, une **obtenir** commande qui interroge le service recherche similaire toohello suivant capture d’écran.

   ![][3]

1. Sélectionnez **GET**.
2. Entrez une URL qui commence par HTTPS, suivie de votre URL de service, suivie de « /indexes/<'indexname'>/docs? », suivie de paramètres de requête. À titre d’exemple, utilisez hello suivant URL, en remplaçant le nom d’hôte exemple hello par un qui n’est valide pour votre service.

         https://my-app.search.windows.net/indexes/hotels/docs?search=motel&facet=category&facet=rating,values:1|2|3|4|5&api-version=2016-09-01

   Cette requête effectue une recherche sur le terme hello « motel » et récupère les catégories de facette pour le classement.
3. En-tête de demande doit être hello même qu’avant. N’oubliez pas que vous avez remplacé hôte de hello et clé d’api avec des valeurs qui sont valides pour votre service.

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444

code de réponse Hello doit être de 200, et sortie de réponse hello doit ressembler toohello similaire après la capture d’écran.

   ![][4]

Hello exemple de requête suivant provient de hello [opération d’Index de recherche (API Azure Search)](http://msdn.microsoft.com/library/dn798927.aspx) sur MSDN. Nombre de requêtes d’exemple hello dans cette rubrique incluent des espaces, ce qui ne sont pas autorisés dans Fiddler. Remplacez chaque espace avec caractère + avant de la chaîne de requête de collage dans hello avant de tenter de requête hello dans Fiddler.

**Avant le remplacement des espaces :**

        GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate desc&api-version=2016-09-01

**Après le remplacement des espaces par + :**

        GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate+desc&api-version=2016-09-01

## <a name="query-hello-system"></a>Interrogation du système hello
Vous pouvez également interroger hello système tooget stockage et les nombres de consommation de document. Sur hello **Composer** , votre demande de recherche similaire toohello suivantes, puis hello réponse renvoie un nombre pour le nombre de hello de documents et l’espace utilisé.

 ![][5]

1. Sélectionnez **GET**.
2. Entrez une URL qui inclut votre URL de service, suivie de « /indexes/hotels/stats?api-version=2016-09-01 » :

         https://my-app.search.windows.net/indexes/hotels/stats?api-version=2016-09-01
3. Spécifiez l’en-tête de demande hello, en remplaçant les hôte hello et clé d’api avec des valeurs qui sont valides pour votre service.

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
4. Laissez le corps de la demande hello vide.
5. Cliquez sur **Exécuter**. Vous devez voir un code d’état HTTP 200 dans la liste des sessions hello. Sélectionnez entrée hello validée pour votre commande.
6. Cliquez sur hello **inspecteurs** , cliquez sur hello **en-têtes** onglet et le format JSON hello puis sélectionnez. Vous devez voir hello document nombre et taille du stockage (en Ko).

## <a name="next-steps"></a>Étapes suivantes
Consultez [gérer votre service de recherche sur Azure](search-manage.md) pour un toomanaging sans code approche et à l’aide d’Azure Search.

<!--Image References-->
[1]: ./media/search-fiddler/AzureSearch_Fiddler1_PutIndex.png
[2]: ./media/search-fiddler/AzureSearch_Fiddler2_PostDocs.png
[3]: ./media/search-fiddler/AzureSearch_Fiddler3_Query.png
[4]: ./media/search-fiddler/AzureSearch_Fiddler4_QueryResults.png
[5]: ./media/search-fiddler/AzureSearch_Fiddler5_QueryStats.png
