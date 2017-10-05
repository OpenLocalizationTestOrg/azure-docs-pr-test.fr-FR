---
title: "Flux de modification pour les ressources HL7 FHIR - Azure Cosmos DB | Microsoft Docs"
description: "Découvrez comment définir les notifications de modification pour les dossiers médicaux HL7 FHIR à l’aide d’Azure Logic Apps, Azure Cosmos DB et Service Bus."
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
ms.openlocfilehash: d2b50c0b6864af41fb9cfa051721c432772b228d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="notifying-patients-of-hl7-fhir-health-care-record-changes-using-logic-apps-and-azure-cosmos-db"></a><span data-ttu-id="b7ff7-104">Notification aux patients des modifications des dossiers médicaux HL7 FHIR à l’aide de Logic Apps et Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="b7ff7-104">Notifying patients of HL7 FHIR health care record changes using Logic Apps and Azure Cosmos DB</span></span>

<span data-ttu-id="b7ff7-105">Howard Edidin, récompensé dans le cadre du programme Azure MVP, a récemment été contacté par une structure qui souhaitait ajouter une nouvelle fonctionnalité à son portail patient.</span><span class="sxs-lookup"><span data-stu-id="b7ff7-105">Azure MVP Howard Edidin was recently contacted by a healthcare organization that wanted to add new functionality to their patient portal.</span></span> <span data-ttu-id="b7ff7-106">L’objectif était d’envoyer des notifications de mise à jour aux patients, le cas échéant, et de leur permettre de s’abonner à ces mises à jour.</span><span class="sxs-lookup"><span data-stu-id="b7ff7-106">They needed to send notifications to patients when their health record was updated, and they needed patients to be able to subscribe to these updates.</span></span> 

<span data-ttu-id="b7ff7-107">Cet article examine la solution de notification du flux de modification, mise en œuvre pour cet établissement de santé à l’aide d’Azure Cosmos DB, Logic Apps et Service Bus.</span><span class="sxs-lookup"><span data-stu-id="b7ff7-107">This article walks through the change feed notification solution created for this healthcare organization using Azure Cosmos DB, Logic Apps, and Service Bus.</span></span> 

## <a name="project-requirements"></a><span data-ttu-id="b7ff7-108">Configuration requise du projet</span><span class="sxs-lookup"><span data-stu-id="b7ff7-108">Project requirements</span></span>
- <span data-ttu-id="b7ff7-109">Les fournisseurs ont transmis les documents d’architecture documentaires cliniques consolidés (C-CDA) HL7 au format XML.</span><span class="sxs-lookup"><span data-stu-id="b7ff7-109">Providers send HL7 Consolidated-Clinical Document Architecture (C-CDA) documents in XML format.</span></span> <span data-ttu-id="b7ff7-110">Les documents C-CDA englobent tout type de contenus cliniques, tels que les antécédents familiaux et les dossiers d’immunisation, ainsi que les fichiers administratifs, de workflow et financiers.</span><span class="sxs-lookup"><span data-stu-id="b7ff7-110">C-CDA documents encompass just about every type of clinical document, including clinical documents such as family histories and immunization records, as well as administrative, workflow, and financial documents.</span></span> 
- <span data-ttu-id="b7ff7-111">Les documents C-CDA sont convertis en [ressources HL7 FHIR](http://hl7.org/fhir/2017Jan/resourcelist.html) au format JSON.</span><span class="sxs-lookup"><span data-stu-id="b7ff7-111">C-CDA documents are converted to [HL7 FHIR Resources](http://hl7.org/fhir/2017Jan/resourcelist.html) in JSON format.</span></span>
- <span data-ttu-id="b7ff7-112">Les documents de ressource FHIR modifiés sont transmis par voie électronique au format JSON.</span><span class="sxs-lookup"><span data-stu-id="b7ff7-112">Modified FHIR resource documents are sent by email in JSON format.</span></span>

## <a name="solution-workflow"></a><span data-ttu-id="b7ff7-113">Workflow de la solution</span><span class="sxs-lookup"><span data-stu-id="b7ff7-113">Solution workflow</span></span> 

<span data-ttu-id="b7ff7-114">À un niveau élevé, le projet nécessitait les étapes suivantes de workflow :</span><span class="sxs-lookup"><span data-stu-id="b7ff7-114">At a high level, the project required the following workflow steps:</span></span> 
1. <span data-ttu-id="b7ff7-115">Conversion des documents C-CDA en ressources FHIR.</span><span class="sxs-lookup"><span data-stu-id="b7ff7-115">Convert C-CDA documents to FHIR resources.</span></span>
2. <span data-ttu-id="b7ff7-116">Exécution de l’interrogation de déclenchement récurrent pour les ressources FHIR modifiées.</span><span class="sxs-lookup"><span data-stu-id="b7ff7-116">Perform recurring trigger polling for modified FHIR resources.</span></span> 
2. <span data-ttu-id="b7ff7-117">Appel d’une application personnalisée, FhirNotificationApi, afin d’établir la connexion à Azure Cosmos DB et de rechercher des documents nouveaux ou modifiés.</span><span class="sxs-lookup"><span data-stu-id="b7ff7-117">Call a custom app, FhirNotificationApi, to connect to Azure Cosmos DB and query for new or modified documents.</span></span>
3. <span data-ttu-id="b7ff7-118">Enregistrez la réponse dans la file d’attente Service Bus.</span><span class="sxs-lookup"><span data-stu-id="b7ff7-118">Save the response to to the Service Bus queue.</span></span>
4. <span data-ttu-id="b7ff7-119">Vérifiez l’absence de nouveaux messages dans la file d’attente Service Bus.</span><span class="sxs-lookup"><span data-stu-id="b7ff7-119">Poll for new messages in the Service Bus queue.</span></span>
5. <span data-ttu-id="b7ff7-120">Envoi de notifications d’e-mail aux patients.</span><span class="sxs-lookup"><span data-stu-id="b7ff7-120">Send email notifications to patients.</span></span>

## <a name="solution-architecture"></a><span data-ttu-id="b7ff7-121">Architecture de solution</span><span class="sxs-lookup"><span data-stu-id="b7ff7-121">Solution architecture</span></span>
<span data-ttu-id="b7ff7-122">Cette solution nécessite que 3 applications logiques respectent les conditions préalables ci-dessus et exécutent le workflow de la solution.</span><span class="sxs-lookup"><span data-stu-id="b7ff7-122">This solution requires three Logic Apps to meet the above requirements and complete the solution workflow.</span></span> <span data-ttu-id="b7ff7-123">Les 3 applications logiques sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="b7ff7-123">The three logic apps are:</span></span>
1. <span data-ttu-id="b7ff7-124">**Application de mappage HL7 FHIR** : reçoit le document HL7 C-CDA, le transforme en ressource FHIR et l’enregistre sur Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b7ff7-124">**HL7-FHIR-Mapping app**: Receives the HL7 C-CDA document, transforms it to the FHIR Resource, then saves it to Azure Cosmos DB.</span></span>
2. <span data-ttu-id="b7ff7-125">**Application des dossiers électroniques** : interroge le référentiel Azure Cosmos DB FHIR et enregistre la réponse dans la file d’attente Service Bus.</span><span class="sxs-lookup"><span data-stu-id="b7ff7-125">**EHR app**: Queries the Azure Cosmos DB FHIR repository and saves the response to a Service Bus queue.</span></span> <span data-ttu-id="b7ff7-126">Cette application logique utilise une [application API](#api-app) pour récupérer les documents nouveaux et modifiés.</span><span class="sxs-lookup"><span data-stu-id="b7ff7-126">This logic app uses an [API app](#api-app) to retrieve new and changed documents.</span></span>
3. <span data-ttu-id="b7ff7-127">**Application de notification du processus** : envoie une notification par courrier électronique avec les documents de ressource FHIR dans le corps.</span><span class="sxs-lookup"><span data-stu-id="b7ff7-127">**Process notification app**: Sends an email notification with the FHIR resource documents in the body.</span></span>

![Les 3 applications logiques utilisées dans cette solution de soins de santé HL7 FHIR](./media/change-feed-hl7-fhir-logic-apps/health-care-solution-hl7-fhir.png)



### <a name="azure-services-used-in-the-solution"></a><span data-ttu-id="b7ff7-129">Services Azure utilisés dans la solution</span><span class="sxs-lookup"><span data-stu-id="b7ff7-129">Azure services used in the solution</span></span>

#### <a name="azure-cosmos-db-documentdb-api"></a><span data-ttu-id="b7ff7-130">API DocumentDB Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="b7ff7-130">Azure Cosmos DB DocumentDB API</span></span>
<span data-ttu-id="b7ff7-131">Azure Cosmos DB est le référentiel dédié aux ressources FHIR, tel que représenté dans la figure suivante.</span><span class="sxs-lookup"><span data-stu-id="b7ff7-131">Azure Cosmos DB is the repository for the FHIR resources as shown in the following figure.</span></span>

![Compte Azure Cosmos DB utilisé dans ce didacticiel de soins de santé HL7 FHIR](./media/change-feed-hl7-fhir-logic-apps/account.png)

#### <a name="logic-apps"></a><span data-ttu-id="b7ff7-133">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="b7ff7-133">Logic Apps</span></span>
<span data-ttu-id="b7ff7-134">Logic Apps gère le processus du workflow.</span><span class="sxs-lookup"><span data-stu-id="b7ff7-134">Logic Apps handle the workflow process.</span></span> <span data-ttu-id="b7ff7-135">Les captures d’écran suivantes représentent les applications logiques créées pour cette solution.</span><span class="sxs-lookup"><span data-stu-id="b7ff7-135">The following screenshots show the Logic apps created for this solution.</span></span> 


1. <span data-ttu-id="b7ff7-136">**Application de mappage HL7 FHIR** : reçoit le document HL7 C-CDA et le transforme en ressource FHIR à l’aide de l’instance Enterprise Integration Pack (EIP) pour Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="b7ff7-136">**HL7-FHIR-Mapping app**: Receive the HL7 C-CDA document and transform it to an FHIR resource using the Enterprise Integration Pack for Logic Apps.</span></span> <span data-ttu-id="b7ff7-137">EIP prend en charge le mappage du document C-CDA vers les ressources FHIR.</span><span class="sxs-lookup"><span data-stu-id="b7ff7-137">The Enterprise Integration Pack handles the mapping from the C-CDA to FHIR resources.</span></span>

    ![L’application logique utilisée pour recevoir les dossiers médicaux HL7 FHIR](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-json-transform.png)


2. <span data-ttu-id="b7ff7-139">**Application des dossiers électroniques** : interroge le référentiel Azure Cosmos DB FHIR et enregistre la réponse dans la file d’attente Service Bus.</span><span class="sxs-lookup"><span data-stu-id="b7ff7-139">**EHR app**: Query the Azure Cosmos DB FHIR repository and save the response to a Service Bus queue.</span></span> <span data-ttu-id="b7ff7-140">Vous trouverez le code de l’application GetNewOrModifiedFHIRDocuments ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="b7ff7-140">The code for the GetNewOrModifiedFHIRDocuments app is below.</span></span>

    ![Application logique utilisée pour interroger Azure Cosmos DB](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-api-app.png)

3. <span data-ttu-id="b7ff7-142">**Application de notification du processus** : envoie une notification par courrier électronique avec les documents de ressource FHIR dans le corps.</span><span class="sxs-lookup"><span data-stu-id="b7ff7-142">**Process notification app**: Send an email notification with the FHIR resource documents in the body.</span></span>

    ![L’application logique qui transmet au patient l’e-mail avec la ressource HL7 FHIR dans le corps](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-send-email.png)

#### <a name="service-bus"></a><span data-ttu-id="b7ff7-144">Service Bus</span><span class="sxs-lookup"><span data-stu-id="b7ff7-144">Service Bus</span></span>
<span data-ttu-id="b7ff7-145">La figure suivante représente la file d’attente des patients.</span><span class="sxs-lookup"><span data-stu-id="b7ff7-145">The following figure shows the patients queue.</span></span> <span data-ttu-id="b7ff7-146">La valeur de la propriété Tag est utilisée pour l’objet de l’e-mail.</span><span class="sxs-lookup"><span data-stu-id="b7ff7-146">The Tag property value is used for the email subject.</span></span>

![La file d’attente Service Bus utilisée dans le didacticiel HL7 FHIR](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-service-bus-queue.png)

<a id="api-app"></a>

#### <a name="api-app"></a><span data-ttu-id="b7ff7-148">Application API</span><span class="sxs-lookup"><span data-stu-id="b7ff7-148">API app</span></span>
<span data-ttu-id="b7ff7-149">Une application API se connecte à Azure Cosmos DB et recherche des documents FHIR nouveaux ou modifiés, par type de ressource.</span><span class="sxs-lookup"><span data-stu-id="b7ff7-149">An API app connects to Azure Cosmos DB and queries for new or modified FHIR documents By resource type.</span></span> <span data-ttu-id="b7ff7-150">Cette application dispose d’un contrôleur, **FhirNotificationApi** avec une opération, **GetNewOrModifiedFhirDocuments**. Voir la [source de l’application API](#api-app-source).</span><span class="sxs-lookup"><span data-stu-id="b7ff7-150">This app has one controller, **FhirNotificationApi** with a one operation **GetNewOrModifiedFhirDocuments**, see [source for API app](#api-app-source).</span></span>

<span data-ttu-id="b7ff7-151">Nous utilisons la classe [`CreateDocumentChangeFeedQuery`](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery.aspx) de l’API .NET Azure Cosmos DB DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="b7ff7-151">We are using the [`CreateDocumentChangeFeedQuery`](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery.aspx) class from the Azure Cosmos DB DocumentDB .NET API.</span></span> <span data-ttu-id="b7ff7-152">Pour plus d’informations, consultez l’[article sur le flux de modification](change-feed.md).</span><span class="sxs-lookup"><span data-stu-id="b7ff7-152">For more information, see the [change feed article](change-feed.md).</span></span> 

##### <a name="getnewormodifiedfhirdocuments-operation"></a><span data-ttu-id="b7ff7-153">Opération GetNewOrModifiedFhirDocuments</span><span class="sxs-lookup"><span data-stu-id="b7ff7-153">GetNewOrModifiedFhirDocuments operation</span></span>

<span data-ttu-id="b7ff7-154">**Entrées**</span><span class="sxs-lookup"><span data-stu-id="b7ff7-154">**Inputs**</span></span>
- <span data-ttu-id="b7ff7-155">DatabaseId</span><span class="sxs-lookup"><span data-stu-id="b7ff7-155">DatabaseId</span></span>
- <span data-ttu-id="b7ff7-156">CollectionId</span><span class="sxs-lookup"><span data-stu-id="b7ff7-156">CollectionId</span></span>
- <span data-ttu-id="b7ff7-157">Nom du type de ressource HL7 FHIR</span><span class="sxs-lookup"><span data-stu-id="b7ff7-157">HL7 FHIR Resource Type name</span></span>
- <span data-ttu-id="b7ff7-158">Valeur booléenne : Start from Beginning(démarrer à partir du début)</span><span class="sxs-lookup"><span data-stu-id="b7ff7-158">Boolean: Start from Beginning</span></span>
- <span data-ttu-id="b7ff7-159">Int : nombre de documents renvoyés</span><span class="sxs-lookup"><span data-stu-id="b7ff7-159">Int: Number of documents returned</span></span>

<span data-ttu-id="b7ff7-160">**Sorties**</span><span class="sxs-lookup"><span data-stu-id="b7ff7-160">**Outputs**</span></span>
- <span data-ttu-id="b7ff7-161">Réussite : code d’état 200, Réponse : liste des documents (tableau JSON)</span><span class="sxs-lookup"><span data-stu-id="b7ff7-161">Success: Status Code: 200, Response: List of Documents (JSON Array)</span></span>
- <span data-ttu-id="b7ff7-162">Échec : code d’état 404, Réponse : « No Documents found for ’*resource name’* Resource Type » (Aucun document trouvé pour le type de ressource)</span><span class="sxs-lookup"><span data-stu-id="b7ff7-162">Failure: Status Code: 404, Response: "No Documents found for '*resource name'* Resource Type"</span></span>

<a id="api-app-source"></a>

<span data-ttu-id="b7ff7-163">**Source pour l’application API**</span><span class="sxs-lookup"><span data-stu-id="b7ff7-163">**Source for the API app**</span></span>

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
            ///     Gets the new or modified FHIR documents from Last Run Date 
            ///     or create date of the collection
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

### <a name="testing-the-fhirnotificationapi"></a><span data-ttu-id="b7ff7-164">Test de l’élément FhirNotificationApi</span><span class="sxs-lookup"><span data-stu-id="b7ff7-164">Testing the FhirNotificationApi</span></span> 

<span data-ttu-id="b7ff7-165">L’image suivante illustre la manière dont l’élément swagger a été utilisé pour tester l’élément [FhirNotificationApi](#api-app-source).</span><span class="sxs-lookup"><span data-stu-id="b7ff7-165">The following image demonstrates how swagger was used to to test the [FhirNotificationApi](#api-app-source).</span></span>

![Le fichier Swagger utilisé pour tester l’application API](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-testing-app.png)


### <a name="azure-portal-dashboard"></a><span data-ttu-id="b7ff7-167">Tableau de bord du portail Azure</span><span class="sxs-lookup"><span data-stu-id="b7ff7-167">Azure portal dashboard</span></span>

<span data-ttu-id="b7ff7-168">L’image suivante représente l’ensemble des services Azure dédiés à cette solution exécutée dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="b7ff7-168">The following image shows all of the Azure services for this solution running in the Azure portal.</span></span>

![Portail Azure représentant l’ensemble des services utilisés dans ce didacticiel HL7 FHIR](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-portal.png)


## <a name="summary"></a><span data-ttu-id="b7ff7-170">Résumé</span><span class="sxs-lookup"><span data-stu-id="b7ff7-170">Summary</span></span>

- <span data-ttu-id="b7ff7-171">Vous avez appris qu’Azure Cosmos DB dispose d’une prise en charge native des notifications relatives aux documents nouveaux ou modifiés, et vous vous êtes rendu compte de sa simplicité d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="b7ff7-171">You have learned that Azure Cosmos DB has native suppport for notifications for new or modifed documents and how easy it is to use.</span></span> 
- <span data-ttu-id="b7ff7-172">En vous appuyant sur Logic Apps, vous pouvez créer des workflows sans écrire aucun code.</span><span class="sxs-lookup"><span data-stu-id="b7ff7-172">By leveraging Logic Apps, you can create workflows without writing any code.</span></span>
- <span data-ttu-id="b7ff7-173">Vous valorisez les files d’attente Azure Service Bus pour gérer la distribution des documents HL7 FHIR.</span><span class="sxs-lookup"><span data-stu-id="b7ff7-173">Using Azure Service Bus Queues to handle the distribution for the HL7 FHIR documents.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b7ff7-174">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b7ff7-174">Next steps</span></span>
<span data-ttu-id="b7ff7-175">Pour en savoir plus sur Azure Cosmos DB, consultez la [page d’accueil Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="b7ff7-175">For more information about Azure Cosmos DB, see the [Azure Cosmos DB home page](https://azure.microsoft.com/services/cosmos-db/).</span></span> <span data-ttu-id="b7ff7-176">Pour plus d’informations sur Logic Apps, voir [Logic Apps](https://azure.microsoft.com/services/logic-apps/).</span><span class="sxs-lookup"><span data-stu-id="b7ff7-176">For more informaiton about Logic Apps, see [Logic Apps](https://azure.microsoft.com/services/logic-apps/).</span></span>


