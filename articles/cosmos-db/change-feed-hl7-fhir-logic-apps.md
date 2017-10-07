---
title: "aaaChange d’alimentation pour les ressources HL7 FHIR - base de données Azure Cosmos | Documents Microsoft"
description: "Découvrez comment tooset des notifications de modifications pour HL7 FHIR soins de santé des patients à l’aide d’Azure Logic Apps, base de données Azure Cosmos et Service Bus."
keywords: hl7 fhir
services: cosmos-db
author: hedidin
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: 0d25c11f-9197-419a-aa19-4614c6ab2d06
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: b-hoedid
ms.openlocfilehash: d2809bf5c6d8c193c49438d20684c56caea646bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="notifying-patients-of-hl7-fhir-health-care-record-changes-using-logic-apps-and-azure-cosmos-db"></a>Notification aux patients des modifications des dossiers médicaux HL7 FHIR à l’aide de Logic Apps et Azure Cosmos DB

Azure MVP Howard Edidin a été récemment contacté par une organisation de soins de santé qui voulaient tooadd nouveau fonctionnalité tootheir patient portail. Ils nécessaire toosend notifications toopatients lors de leur enregistrement de contrôle d’intégrité a été mis à jour, et ils nécessaires patients toobe toosubscribe en mesure de toothese mises à jour. 

Cet article Guide de solution de flux de notification de modifications hello créée pour cette organisation de soins de santé à l’aide de la base de données Azure Cosmos, Logic Apps et Service Bus. 

## <a name="project-requirements"></a>Configuration requise du projet
- Les fournisseurs ont transmis les documents d’architecture documentaires cliniques consolidés (C-CDA) HL7 au format XML. Les documents C-CDA englobent tout type de contenus cliniques, tels que les antécédents familiaux et les dossiers d’immunisation, ainsi que les fichiers administratifs, de workflow et financiers. 
- Les documents de C-CDA sont convertis en trop[HL7 FHIR ressources](http://hl7.org/fhir/2017Jan/resourcelist.html) au format JSON.
- Les documents de ressource FHIR modifiés sont transmis par voie électronique au format JSON.

## <a name="solution-workflow"></a>Workflow de la solution 

À un niveau élevé, hello hello requis de projet du flux de travail comme suit : 
1. Convertir des ressources de tooFHIR C-CDA documents.
2. Exécution de l’interrogation de déclenchement récurrent pour les ressources FHIR modifiées. 
2. L’appel d’une application personnalisée, FhirNotificationApi, tooconnect tooAzure Cosmos DB et une requête pour les documents nouveaux ou modifiés.
3. Enregistrez la file d’attente du Service Bus tootoohello réponses hello.
4. Interrogation de nouveaux messages dans la file d’attente du Service Bus hello.
5. Envoyer toopatients des notifications par courrier électronique.

## <a name="solution-architecture"></a>Architecture de solution
Cette solution requiert trois hello toomeet de Logic Apps au-dessus des exigences et workflow hello complète de la solution. trois applications de logique Hello sont :
1. **Application de la correspondance HL7-FHIR**: reçoit hello HL7 C-CDA document, il transforme toohello FHIR ressource, puis enregistre tooAzure Cosmos DB.
2. **Application de DMI**: interroge l’espace de stockage Azure Cosmos DB FHIR hello et enregistre la file d’attente du Service Bus tooa réponses hello. Cette application logique utilise un [application API](#api-app) tooretrieve nouvelles et modifiées des documents.
3. **Application de notification de processus**: envoie une notification par courrier électronique avec des documents de ressource FHIR hello dans le corps de hello.

![Hello trois Logic Apps est utilisé dans cette solution de soins de santé HL7 FHIR](./media/change-feed-hl7-fhir-logic-apps/health-care-solution-hl7-fhir.png)



### <a name="azure-services-used-in-hello-solution"></a>Services Azure utilisés dans les solutions hello

#### <a name="azure-cosmos-db-documentdb-api"></a>API DocumentDB Azure Cosmos DB
Base de données Azure Cosmos est référentiel hello pour les ressources FHIR hello comme indiqué dans la figure suivante de hello.

![compte de base de données Azure Cosmos Hello utilisé dans ce didacticiel de soins de santé HL7 FHIR](./media/change-feed-hl7-fhir-logic-apps/account.png)

#### <a name="logic-apps"></a>Logic Apps
Logic Apps gérer le processus de workflow hello. Hello captures d’écran suivantes montrent hello Logic apps créés pour cette solution. 


1. **Application de la correspondance HL7-FHIR**: réception hello HL7 C-CDA document et transformer les ressources FHIR tooan à l’aide de hello Pack d’intégration Enterprise pour les applications de la logique. Hello Pack d’intégration Enterprise gère hello mappage des ressources de tooFHIR C-CDA de hello.

    ![Hello application logique utilisé des enregistrements de soins de santé HL7 FHIR tooreceive](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-json-transform.png)


2. **Application de DMI**: hello FHIR de base de données Azure Cosmos référentiel des requêtes et enregistrer hello réponse tooa Bus de Service de file d’attente. code Hello pour l’application de GetNewOrModifiedFHIRDocuments hello est inférieur à.

    ![Hello application logique utilisé tooquery base de données Azure Cosmos](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-api-app.png)

3. **Application de notification de processus**: envoyer une notification par courrier électronique avec des documents de ressource FHIR hello dans le corps de hello.

    ![Hello logique d’application qui envoie le patient par courrier électronique avec les ressources de HL7 FHIR hello dans le corps de hello](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-send-email.png)

#### <a name="service-bus"></a>Service Bus
Hello suivant figure montre hello patients file d’attente. Hello, valeur de propriété Tag est utilisée pour l’objet du message électronique hello.

![Hello file d’attente du Bus de Service utilisé dans ce didacticiel HL7 FHIR](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-service-bus-queue.png)

<a id="api-app"></a>

#### <a name="api-app"></a>application API
Une application API connecte tooAzure Cosmos DB et des requêtes pour les documents FHIR nouveaux ou modifiés par type de ressource. Cette application dispose d’un contrôleur, **FhirNotificationApi** avec une opération, **GetNewOrModifiedFhirDocuments**. Voir la [source de l’application API](#api-app-source).

Nous utilisons hello [ `CreateDocumentChangeFeedQuery` ](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery.aspx) classe à partir de hello Azure Cosmos DB DocumentDB .NET API. Pour plus d’informations, consultez hello [modification flux article](change-feed.md). 

##### <a name="getnewormodifiedfhirdocuments-operation"></a>Opération GetNewOrModifiedFhirDocuments

**Entrées**
- DatabaseId
- CollectionId
- Nom du type de ressource HL7 FHIR
- Valeur booléenne : Start from Beginning(démarrer à partir du début)
- Int : nombre de documents renvoyés

**Sorties**
- Réussite : code d’état 200, Réponse : liste des documents (tableau JSON)
- Échec : code d’état 404, Réponse : « No Documents found for ’*resource name’* Resource Type » (Aucun document trouvé pour le type de ressource)

<a id="api-app-source"></a>

**Source de l’application hello API**

```C#

    using System.Collections.Generic;
    using System.Linq;
    using System.Net;
    using System.Net.Http;
    using System.Threading.Tasks;
    using System.Web.Http;
    using Microsoft.Azure.Documents;
    using Microsoft.Azure.Documents.Client;
    using Swashbuckle.Swagger.Annotations;
    using TRex.Metadata;
    
    namespace FhirNotificationApi.Controllers
    {
        /// <summary>
        ///     FHIR Resource Type Controller
        /// </summary>
        /// <seealso cref="System.Web.Http.ApiController" />
        public class FhirResourceTypeController : ApiController
        {
            /// <summary>
            ///     Gets hello new or modified FHIR documents from Last Run Date 
            ///     or create date of hello collection
            /// </summary>
            /// <param name="databaseId"></param>
            /// <param name="collectionId"></param>
            /// <param name="resourceType"></param>
            /// <param name="startfromBeginning"></param>
            /// <param name="maximumItemCount">-1 returns all (default)</param>
            /// <returns></returns>
            [Metadata("Get New or Modified FHIR Documents",
                "Query for new or modifed FHIR Documents By Resource Type " +
                "from Last Run Date or Begining of Collection creation"
            )]
            [SwaggerResponse(HttpStatusCode.OK, type: typeof(Task<dynamic>))]
            [SwaggerResponse(HttpStatusCode.NotFound, "No New or Modifed Documents found")]
            [SwaggerOperation("GetNewOrModifiedFHIRDocuments")]
            public async Task<dynamic> GetNewOrModifiedFhirDocuments(
                [Metadata("Database Id", "Database Id")] string databaseId,
                [Metadata("Collection Id", "Collection Id")] string collectionId,
                [Metadata("Resource Type", "FHIR resource type name")] string resourceType,
                [Metadata("Start from Beginning ", "Change Feed Option")] bool startfromBeginning,
                [Metadata("Maximum Item Count", "Number of documents returned. '-1 returns all' (default)")] int maximumItemCount = -1
            )
            {
                var collectionLink = UriFactory.CreateDocumentCollectionUri(databaseId, collectionId);
    
                var context = new DocumentDbContext();  
    
                var docs = new List<dynamic>();
    
                var partitionKeyRanges = new List<PartitionKeyRange>();
                FeedResponse<PartitionKeyRange> pkRangesResponse;
    
                do
                {
                    pkRangesResponse = await context.Client.ReadPartitionKeyRangeFeedAsync(collectionLink);
                    partitionKeyRanges.AddRange(pkRangesResponse);
                } while (pkRangesResponse.ResponseContinuation != null);
    
                foreach (var pkRange in partitionKeyRanges)
                {
                    var changeFeedOptions = new ChangeFeedOptions
                    {
                        StartFromBeginning = startfromBeginning,
                        RequestContinuation = null,
                        MaxItemCount = maximumItemCount,
                        PartitionKeyRangeId = pkRange.Id
                    };
    
                    using (var query = context.Client.CreateDocumentChangeFeedQuery(collectionLink, changeFeedOptions))
                    {
                        do
                        {
                            if (query != null)
                            {
                                var results = await query.ExecuteNextAsync<dynamic>().ConfigureAwait(false);
                                if (results.Count > 0)
                                    docs.AddRange(results.Where(doc => doc.resourceType == resourceType));
                            }
                            else
                            {
                                throw new HttpResponseException(new HttpResponseMessage(HttpStatusCode.NotFound));
                            }
                        } while (query.HasMoreResults);
                    }
                }
                if (docs.Count > 0)
                    return docs;
                var msg = new StringContent("No documents found for " + resourceType + " Resource");
                var response = new HttpResponseMessage
                {
                    StatusCode = HttpStatusCode.NotFound,
                    Content = msg
                };
                return response;
            }
        }
    }
    
```

### <a name="testing-hello-fhirnotificationapi"></a>Test hello FhirNotificationApi 

Hello image suivante montre comment swagger a été utilisé tootootest hello [FhirNotificationApi](#api-app-source).

![le fichier Swagger Hello utilisé tootest hello API app](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-testing-app.png)


### <a name="azure-portal-dashboard"></a>Tableau de bord du portail Azure

Hello suivant image montre toutes les hello services Windows Azure pour cette solution en cours d’exécution dans hello portail Azure.

![Hello portail Azure en affichant tous les services de hello utilisés dans ce didacticiel HL7 FHIR](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-portal.png)


## <a name="summary"></a>Résumé

- Vous avez appris que la base de données Azure Cosmos a prise en charge native pour les notifications pour les nouveaux ou modifiés documents et combien il est facile toouse. 
- En vous appuyant sur Logic Apps, vous pouvez créer des workflows sans écrire aucun code.
- À l’aide de distribution de files d’attente de Azure Service Bus toohandle hello pour les documents HL7 FHIR hello.

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur la base de données Azure Cosmos, consultez hello [page d’accueil de base de données Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/). Pour plus d’informations sur Logic Apps, voir [Logic Apps](https://azure.microsoft.com/services/logic-apps/).


