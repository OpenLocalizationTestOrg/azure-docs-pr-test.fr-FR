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
# <a name="notifying-patients-of-hl7-fhir-health-care-record-changes-using-logic-apps-and-azure-cosmos-db"></a><span data-ttu-id="42770-104">Notification aux patients des modifications des dossiers médicaux HL7 FHIR à l’aide de Logic Apps et Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="42770-104">Notifying patients of HL7 FHIR health care record changes using Logic Apps and Azure Cosmos DB</span></span>

<span data-ttu-id="42770-105">Azure MVP Howard Edidin a été récemment contacté par une organisation de soins de santé qui voulaient tooadd nouveau fonctionnalité tootheir patient portail.</span><span class="sxs-lookup"><span data-stu-id="42770-105">Azure MVP Howard Edidin was recently contacted by a healthcare organization that wanted tooadd new functionality tootheir patient portal.</span></span> <span data-ttu-id="42770-106">Ils nécessaire toosend notifications toopatients lors de leur enregistrement de contrôle d’intégrité a été mis à jour, et ils nécessaires patients toobe toosubscribe en mesure de toothese mises à jour.</span><span class="sxs-lookup"><span data-stu-id="42770-106">They needed toosend notifications toopatients when their health record was updated, and they needed patients toobe able toosubscribe toothese updates.</span></span> 

<span data-ttu-id="42770-107">Cet article Guide de solution de flux de notification de modifications hello créée pour cette organisation de soins de santé à l’aide de la base de données Azure Cosmos, Logic Apps et Service Bus.</span><span class="sxs-lookup"><span data-stu-id="42770-107">This article walks through hello change feed notification solution created for this healthcare organization using Azure Cosmos DB, Logic Apps, and Service Bus.</span></span> 

## <a name="project-requirements"></a><span data-ttu-id="42770-108">Configuration requise du projet</span><span class="sxs-lookup"><span data-stu-id="42770-108">Project requirements</span></span>
- <span data-ttu-id="42770-109">Les fournisseurs ont transmis les documents d’architecture documentaires cliniques consolidés (C-CDA) HL7 au format XML.</span><span class="sxs-lookup"><span data-stu-id="42770-109">Providers send HL7 Consolidated-Clinical Document Architecture (C-CDA) documents in XML format.</span></span> <span data-ttu-id="42770-110">Les documents C-CDA englobent tout type de contenus cliniques, tels que les antécédents familiaux et les dossiers d’immunisation, ainsi que les fichiers administratifs, de workflow et financiers.</span><span class="sxs-lookup"><span data-stu-id="42770-110">C-CDA documents encompass just about every type of clinical document, including clinical documents such as family histories and immunization records, as well as administrative, workflow, and financial documents.</span></span> 
- <span data-ttu-id="42770-111">Les documents de C-CDA sont convertis en trop[HL7 FHIR ressources](http://hl7.org/fhir/2017Jan/resourcelist.html) au format JSON.</span><span class="sxs-lookup"><span data-stu-id="42770-111">C-CDA documents are converted too[HL7 FHIR Resources](http://hl7.org/fhir/2017Jan/resourcelist.html) in JSON format.</span></span>
- <span data-ttu-id="42770-112">Les documents de ressource FHIR modifiés sont transmis par voie électronique au format JSON.</span><span class="sxs-lookup"><span data-stu-id="42770-112">Modified FHIR resource documents are sent by email in JSON format.</span></span>

## <a name="solution-workflow"></a><span data-ttu-id="42770-113">Workflow de la solution</span><span class="sxs-lookup"><span data-stu-id="42770-113">Solution workflow</span></span> 

<span data-ttu-id="42770-114">À un niveau élevé, hello hello requis de projet du flux de travail comme suit :</span><span class="sxs-lookup"><span data-stu-id="42770-114">At a high level, hello project required hello following workflow steps:</span></span> 
1. <span data-ttu-id="42770-115">Convertir des ressources de tooFHIR C-CDA documents.</span><span class="sxs-lookup"><span data-stu-id="42770-115">Convert C-CDA documents tooFHIR resources.</span></span>
2. <span data-ttu-id="42770-116">Exécution de l’interrogation de déclenchement récurrent pour les ressources FHIR modifiées.</span><span class="sxs-lookup"><span data-stu-id="42770-116">Perform recurring trigger polling for modified FHIR resources.</span></span> 
2. <span data-ttu-id="42770-117">L’appel d’une application personnalisée, FhirNotificationApi, tooconnect tooAzure Cosmos DB et une requête pour les documents nouveaux ou modifiés.</span><span class="sxs-lookup"><span data-stu-id="42770-117">Call a custom app, FhirNotificationApi, tooconnect tooAzure Cosmos DB and query for new or modified documents.</span></span>
3. <span data-ttu-id="42770-118">Enregistrez la file d’attente du Service Bus tootoohello réponses hello.</span><span class="sxs-lookup"><span data-stu-id="42770-118">Save hello response tootoohello Service Bus queue.</span></span>
4. <span data-ttu-id="42770-119">Interrogation de nouveaux messages dans la file d’attente du Service Bus hello.</span><span class="sxs-lookup"><span data-stu-id="42770-119">Poll for new messages in hello Service Bus queue.</span></span>
5. <span data-ttu-id="42770-120">Envoyer toopatients des notifications par courrier électronique.</span><span class="sxs-lookup"><span data-stu-id="42770-120">Send email notifications toopatients.</span></span>

## <a name="solution-architecture"></a><span data-ttu-id="42770-121">Architecture de solution</span><span class="sxs-lookup"><span data-stu-id="42770-121">Solution architecture</span></span>
<span data-ttu-id="42770-122">Cette solution requiert trois hello toomeet de Logic Apps au-dessus des exigences et workflow hello complète de la solution.</span><span class="sxs-lookup"><span data-stu-id="42770-122">This solution requires three Logic Apps toomeet hello above requirements and complete hello solution workflow.</span></span> <span data-ttu-id="42770-123">trois applications de logique Hello sont :</span><span class="sxs-lookup"><span data-stu-id="42770-123">hello three logic apps are:</span></span>
1. <span data-ttu-id="42770-124">**Application de la correspondance HL7-FHIR**: reçoit hello HL7 C-CDA document, il transforme toohello FHIR ressource, puis enregistre tooAzure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="42770-124">**HL7-FHIR-Mapping app**: Receives hello HL7 C-CDA document, transforms it toohello FHIR Resource, then saves it tooAzure Cosmos DB.</span></span>
2. <span data-ttu-id="42770-125">**Application de DMI**: interroge l’espace de stockage Azure Cosmos DB FHIR hello et enregistre la file d’attente du Service Bus tooa réponses hello.</span><span class="sxs-lookup"><span data-stu-id="42770-125">**EHR app**: Queries hello Azure Cosmos DB FHIR repository and saves hello response tooa Service Bus queue.</span></span> <span data-ttu-id="42770-126">Cette application logique utilise un [application API](#api-app) tooretrieve nouvelles et modifiées des documents.</span><span class="sxs-lookup"><span data-stu-id="42770-126">This logic app uses an [API app](#api-app) tooretrieve new and changed documents.</span></span>
3. <span data-ttu-id="42770-127">**Application de notification de processus**: envoie une notification par courrier électronique avec des documents de ressource FHIR hello dans le corps de hello.</span><span class="sxs-lookup"><span data-stu-id="42770-127">**Process notification app**: Sends an email notification with hello FHIR resource documents in hello body.</span></span>

![Hello trois Logic Apps est utilisé dans cette solution de soins de santé HL7 FHIR](./media/change-feed-hl7-fhir-logic-apps/health-care-solution-hl7-fhir.png)



### <a name="azure-services-used-in-hello-solution"></a><span data-ttu-id="42770-129">Services Azure utilisés dans les solutions hello</span><span class="sxs-lookup"><span data-stu-id="42770-129">Azure services used in hello solution</span></span>

#### <a name="azure-cosmos-db-documentdb-api"></a><span data-ttu-id="42770-130">API DocumentDB Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="42770-130">Azure Cosmos DB DocumentDB API</span></span>
<span data-ttu-id="42770-131">Base de données Azure Cosmos est référentiel hello pour les ressources FHIR hello comme indiqué dans la figure suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="42770-131">Azure Cosmos DB is hello repository for hello FHIR resources as shown in hello following figure.</span></span>

![compte de base de données Azure Cosmos Hello utilisé dans ce didacticiel de soins de santé HL7 FHIR](./media/change-feed-hl7-fhir-logic-apps/account.png)

#### <a name="logic-apps"></a><span data-ttu-id="42770-133">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="42770-133">Logic Apps</span></span>
<span data-ttu-id="42770-134">Logic Apps gérer le processus de workflow hello.</span><span class="sxs-lookup"><span data-stu-id="42770-134">Logic Apps handle hello workflow process.</span></span> <span data-ttu-id="42770-135">Hello captures d’écran suivantes montrent hello Logic apps créés pour cette solution.</span><span class="sxs-lookup"><span data-stu-id="42770-135">hello following screenshots show hello Logic apps created for this solution.</span></span> 


1. <span data-ttu-id="42770-136">**Application de la correspondance HL7-FHIR**: réception hello HL7 C-CDA document et transformer les ressources FHIR tooan à l’aide de hello Pack d’intégration Enterprise pour les applications de la logique.</span><span class="sxs-lookup"><span data-stu-id="42770-136">**HL7-FHIR-Mapping app**: Receive hello HL7 C-CDA document and transform it tooan FHIR resource using hello Enterprise Integration Pack for Logic Apps.</span></span> <span data-ttu-id="42770-137">Hello Pack d’intégration Enterprise gère hello mappage des ressources de tooFHIR C-CDA de hello.</span><span class="sxs-lookup"><span data-stu-id="42770-137">hello Enterprise Integration Pack handles hello mapping from hello C-CDA tooFHIR resources.</span></span>

    ![Hello application logique utilisé des enregistrements de soins de santé HL7 FHIR tooreceive](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-json-transform.png)


2. <span data-ttu-id="42770-139">**Application de DMI**: hello FHIR de base de données Azure Cosmos référentiel des requêtes et enregistrer hello réponse tooa Bus de Service de file d’attente.</span><span class="sxs-lookup"><span data-stu-id="42770-139">**EHR app**: Query hello Azure Cosmos DB FHIR repository and save hello response tooa Service Bus queue.</span></span> <span data-ttu-id="42770-140">code Hello pour l’application de GetNewOrModifiedFHIRDocuments hello est inférieur à.</span><span class="sxs-lookup"><span data-stu-id="42770-140">hello code for hello GetNewOrModifiedFHIRDocuments app is below.</span></span>

    ![Hello application logique utilisé tooquery base de données Azure Cosmos](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-api-app.png)

3. <span data-ttu-id="42770-142">**Application de notification de processus**: envoyer une notification par courrier électronique avec des documents de ressource FHIR hello dans le corps de hello.</span><span class="sxs-lookup"><span data-stu-id="42770-142">**Process notification app**: Send an email notification with hello FHIR resource documents in hello body.</span></span>

    ![Hello logique d’application qui envoie le patient par courrier électronique avec les ressources de HL7 FHIR hello dans le corps de hello](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-send-email.png)

#### <a name="service-bus"></a><span data-ttu-id="42770-144">Service Bus</span><span class="sxs-lookup"><span data-stu-id="42770-144">Service Bus</span></span>
<span data-ttu-id="42770-145">Hello suivant figure montre hello patients file d’attente.</span><span class="sxs-lookup"><span data-stu-id="42770-145">hello following figure shows hello patients queue.</span></span> <span data-ttu-id="42770-146">Hello, valeur de propriété Tag est utilisée pour l’objet du message électronique hello.</span><span class="sxs-lookup"><span data-stu-id="42770-146">hello Tag property value is used for hello email subject.</span></span>

![Hello file d’attente du Bus de Service utilisé dans ce didacticiel HL7 FHIR](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-service-bus-queue.png)

<a id="api-app"></a>

#### <a name="api-app"></a><span data-ttu-id="42770-148">application API</span><span class="sxs-lookup"><span data-stu-id="42770-148">API app</span></span>
<span data-ttu-id="42770-149">Une application API connecte tooAzure Cosmos DB et des requêtes pour les documents FHIR nouveaux ou modifiés par type de ressource.</span><span class="sxs-lookup"><span data-stu-id="42770-149">An API app connects tooAzure Cosmos DB and queries for new or modified FHIR documents By resource type.</span></span> <span data-ttu-id="42770-150">Cette application dispose d’un contrôleur, **FhirNotificationApi** avec une opération, **GetNewOrModifiedFhirDocuments**. Voir la [source de l’application API](#api-app-source).</span><span class="sxs-lookup"><span data-stu-id="42770-150">This app has one controller, **FhirNotificationApi** with a one operation **GetNewOrModifiedFhirDocuments**, see [source for API app](#api-app-source).</span></span>

<span data-ttu-id="42770-151">Nous utilisons hello [ `CreateDocumentChangeFeedQuery` ](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery.aspx) classe à partir de hello Azure Cosmos DB DocumentDB .NET API.</span><span class="sxs-lookup"><span data-stu-id="42770-151">We are using hello [`CreateDocumentChangeFeedQuery`](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery.aspx) class from hello Azure Cosmos DB DocumentDB .NET API.</span></span> <span data-ttu-id="42770-152">Pour plus d’informations, consultez hello [modification flux article](change-feed.md).</span><span class="sxs-lookup"><span data-stu-id="42770-152">For more information, see hello [change feed article](change-feed.md).</span></span> 

##### <a name="getnewormodifiedfhirdocuments-operation"></a><span data-ttu-id="42770-153">Opération GetNewOrModifiedFhirDocuments</span><span class="sxs-lookup"><span data-stu-id="42770-153">GetNewOrModifiedFhirDocuments operation</span></span>

<span data-ttu-id="42770-154">**Entrées**</span><span class="sxs-lookup"><span data-stu-id="42770-154">**Inputs**</span></span>
- <span data-ttu-id="42770-155">DatabaseId</span><span class="sxs-lookup"><span data-stu-id="42770-155">DatabaseId</span></span>
- <span data-ttu-id="42770-156">CollectionId</span><span class="sxs-lookup"><span data-stu-id="42770-156">CollectionId</span></span>
- <span data-ttu-id="42770-157">Nom du type de ressource HL7 FHIR</span><span class="sxs-lookup"><span data-stu-id="42770-157">HL7 FHIR Resource Type name</span></span>
- <span data-ttu-id="42770-158">Valeur booléenne : Start from Beginning(démarrer à partir du début)</span><span class="sxs-lookup"><span data-stu-id="42770-158">Boolean: Start from Beginning</span></span>
- <span data-ttu-id="42770-159">Int : nombre de documents renvoyés</span><span class="sxs-lookup"><span data-stu-id="42770-159">Int: Number of documents returned</span></span>

<span data-ttu-id="42770-160">**Sorties**</span><span class="sxs-lookup"><span data-stu-id="42770-160">**Outputs**</span></span>
- <span data-ttu-id="42770-161">Réussite : code d’état 200, Réponse : liste des documents (tableau JSON)</span><span class="sxs-lookup"><span data-stu-id="42770-161">Success: Status Code: 200, Response: List of Documents (JSON Array)</span></span>
- <span data-ttu-id="42770-162">Échec : code d’état 404, Réponse : « No Documents found for ’*resource name’* Resource Type » (Aucun document trouvé pour le type de ressource)</span><span class="sxs-lookup"><span data-stu-id="42770-162">Failure: Status Code: 404, Response: "No Documents found for '*resource name'* Resource Type"</span></span>

<a id="api-app-source"></a>

<span data-ttu-id="42770-163">**Source de l’application hello API**</span><span class="sxs-lookup"><span data-stu-id="42770-163">**Source for hello API app**</span></span>

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

### <a name="testing-hello-fhirnotificationapi"></a><span data-ttu-id="42770-164">Test hello FhirNotificationApi</span><span class="sxs-lookup"><span data-stu-id="42770-164">Testing hello FhirNotificationApi</span></span> 

<span data-ttu-id="42770-165">Hello image suivante montre comment swagger a été utilisé tootootest hello [FhirNotificationApi](#api-app-source).</span><span class="sxs-lookup"><span data-stu-id="42770-165">hello following image demonstrates how swagger was used tootootest hello [FhirNotificationApi](#api-app-source).</span></span>

![le fichier Swagger Hello utilisé tootest hello API app](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-testing-app.png)


### <a name="azure-portal-dashboard"></a><span data-ttu-id="42770-167">Tableau de bord du portail Azure</span><span class="sxs-lookup"><span data-stu-id="42770-167">Azure portal dashboard</span></span>

<span data-ttu-id="42770-168">Hello suivant image montre toutes les hello services Windows Azure pour cette solution en cours d’exécution dans hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="42770-168">hello following image shows all of hello Azure services for this solution running in hello Azure portal.</span></span>

![Hello portail Azure en affichant tous les services de hello utilisés dans ce didacticiel HL7 FHIR](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-portal.png)


## <a name="summary"></a><span data-ttu-id="42770-170">Résumé</span><span class="sxs-lookup"><span data-stu-id="42770-170">Summary</span></span>

- <span data-ttu-id="42770-171">Vous avez appris que la base de données Azure Cosmos a prise en charge native pour les notifications pour les nouveaux ou modifiés documents et combien il est facile toouse.</span><span class="sxs-lookup"><span data-stu-id="42770-171">You have learned that Azure Cosmos DB has native suppport for notifications for new or modifed documents and how easy it is toouse.</span></span> 
- <span data-ttu-id="42770-172">En vous appuyant sur Logic Apps, vous pouvez créer des workflows sans écrire aucun code.</span><span class="sxs-lookup"><span data-stu-id="42770-172">By leveraging Logic Apps, you can create workflows without writing any code.</span></span>
- <span data-ttu-id="42770-173">À l’aide de distribution de files d’attente de Azure Service Bus toohandle hello pour les documents HL7 FHIR hello.</span><span class="sxs-lookup"><span data-stu-id="42770-173">Using Azure Service Bus Queues toohandle hello distribution for hello HL7 FHIR documents.</span></span>

## <a name="next-steps"></a><span data-ttu-id="42770-174">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="42770-174">Next steps</span></span>
<span data-ttu-id="42770-175">Pour plus d’informations sur la base de données Azure Cosmos, consultez hello [page d’accueil de base de données Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="42770-175">For more information about Azure Cosmos DB, see hello [Azure Cosmos DB home page](https://azure.microsoft.com/services/cosmos-db/).</span></span> <span data-ttu-id="42770-176">Pour plus d’informations sur Logic Apps, voir [Logic Apps](https://azure.microsoft.com/services/logic-apps/).</span><span class="sxs-lookup"><span data-stu-id="42770-176">For more informaiton about Logic Apps, see [Logic Apps](https://azure.microsoft.com/services/logic-apps/).</span></span>


