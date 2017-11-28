---
title: "aaaException gestion & Azure Logic Apps - scénario de journalisation erreur | Documents Microsoft"
description: "Décrit un cas d’usage réel sur la gestion avancés des exceptions et la journalisation des erreurs pour Azure Logic Apps"
keywords: 
services: logic-apps
author: hedidin
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 63b0b843-f6b0-4d9a-98d0-17500be17385
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 07/29/2016
ms.author: LADocs; b-hoedid
ms.openlocfilehash: e893a7b652254dca7b8a82398e8afd571f6ccd25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="scenario-exception-handling-and-error-logging-for-logic-apps"></a><span data-ttu-id="2aef1-103">Scénario : gestion des exceptions et journalisation des erreurs pour les applications logiques</span><span class="sxs-lookup"><span data-stu-id="2aef1-103">Scenario: Exception handling and error logging for logic apps</span></span>

<span data-ttu-id="2aef1-104">Ce scénario décrit comment vous pouvez étendre une logique application toobetter prise en charge la gestion des exceptions.</span><span class="sxs-lookup"><span data-stu-id="2aef1-104">This scenario describes how you can extend a logic app toobetter support exception handling.</span></span> <span data-ttu-id="2aef1-105">Nous avons utilisé une question de hello tooanswer cas utilisation concrète : « Azure Logic Apps prend en charge exception et la gestion des erreurs ? »</span><span class="sxs-lookup"><span data-stu-id="2aef1-105">We've used a real-life use case tooanswer hello question: "Does Azure Logic Apps support exception and error handling?"</span></span>

> [!NOTE]
> <span data-ttu-id="2aef1-106">schéma de Azure Logic Apps actuel Hello fournit un modèle standard pour les réponses de l’action.</span><span class="sxs-lookup"><span data-stu-id="2aef1-106">hello current Azure Logic Apps schema provides a standard template for action responses.</span></span> <span data-ttu-id="2aef1-107">Ce schéma inclut les réponses de type validation interne et de type erreur retournées depuis une application API.</span><span class="sxs-lookup"><span data-stu-id="2aef1-107">This template includes both internal validation and error responses returned from an API app.</span></span>

## <a name="scenario-and-use-case-overview"></a><span data-ttu-id="2aef1-108">Vue d’ensemble du scénario et du cas d’utilisation</span><span class="sxs-lookup"><span data-stu-id="2aef1-108">Scenario and use case overview</span></span>

<span data-ttu-id="2aef1-109">Voici un récit hello en cas d’usage hello pour ce scénario :</span><span class="sxs-lookup"><span data-stu-id="2aef1-109">Here's hello story as hello use case for this scenario:</span></span> 

<span data-ttu-id="2aef1-110">Une organisation de soins de santé connue nous engagé toodevelop une solution Azure qui créerait un patient portail à l’aide de Microsoft Dynamics CRM Online.</span><span class="sxs-lookup"><span data-stu-id="2aef1-110">A well-known healthcare organization engaged us toodevelop an Azure solution that would create a patient portal by using Microsoft Dynamics CRM Online.</span></span> <span data-ttu-id="2aef1-111">Ils nécessaire des enregistrements de rendez-vous toosend entre hello du portail patient Dynamics CRM Online et Salesforce.</span><span class="sxs-lookup"><span data-stu-id="2aef1-111">They needed toosend appointment records between hello Dynamics CRM Online patient portal and Salesforce.</span></span> <span data-ttu-id="2aef1-112">Nous avons demandées toouse hello [HL7 FHIR](http://www.hl7.org/implement/standards/fhir/) standard pour tous les patients.</span><span class="sxs-lookup"><span data-stu-id="2aef1-112">We were asked toouse hello [HL7 FHIR](http://www.hl7.org/implement/standards/fhir/) standard for all patient records.</span></span>

<span data-ttu-id="2aef1-113">projet de Hello comportait deux exigences principales :</span><span class="sxs-lookup"><span data-stu-id="2aef1-113">hello project had two major requirements:</span></span>  

* <span data-ttu-id="2aef1-114">Une méthode toolog enregistre envoyés à partir de hello portail Dynamics CRM Online</span><span class="sxs-lookup"><span data-stu-id="2aef1-114">A method toolog records sent from hello Dynamics CRM Online portal</span></span>
* <span data-ttu-id="2aef1-115">Un moyen tooview toutes les erreurs qui se sont produits dans le flux de travail hello</span><span class="sxs-lookup"><span data-stu-id="2aef1-115">A way tooview any errors that occurred within hello workflow</span></span>

> [!TIP]
> <span data-ttu-id="2aef1-116">Pour visionner une vidéo de haut niveau de ce projet, consultez [groupe utilisateur d’intégration](http://www.integrationusergroup.com/logic-apps-support-error-handling/ "groupe utilisateur d’intégration").</span><span class="sxs-lookup"><span data-stu-id="2aef1-116">For a high-level video about this project, see [Integration User Group](http://www.integrationusergroup.com/logic-apps-support-error-handling/ "Integration User Group").</span></span>

## <a name="how-we-solved-hello-problem"></a><span data-ttu-id="2aef1-117">Comment nous avons résolu le problème de hello</span><span class="sxs-lookup"><span data-stu-id="2aef1-117">How we solved hello problem</span></span>

<span data-ttu-id="2aef1-118">Nous avons choisi [base de données Azure Cosmos](https://azure.microsoft.com/services/documentdb/ "base de données Azure Cosmos") comme référentiel pour les enregistrements de journal et d’erreur hello (Cosmos DB fait référence toorecords sous forme de documents).</span><span class="sxs-lookup"><span data-stu-id="2aef1-118">We chose [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/ "Azure Cosmos DB") As a repository for hello log and error records (Cosmos DB refers toorecords as documents).</span></span> <span data-ttu-id="2aef1-119">Azure Logic Apps ayant un modèle standard pour toutes les réponses, nous n’aurait pas toocreate un schéma personnalisé.</span><span class="sxs-lookup"><span data-stu-id="2aef1-119">Because Azure Logic Apps has a standard template for all responses, we would not have toocreate a custom schema.</span></span> <span data-ttu-id="2aef1-120">Nous pouvons créer une application API trop**insérer** et **requête** pour les enregistrements d’erreur et de journal.</span><span class="sxs-lookup"><span data-stu-id="2aef1-120">We could create an API app too**Insert** and **Query** for both error and log records.</span></span> <span data-ttu-id="2aef1-121">Nous avons également définir un schéma pour chaque application d’API hello.</span><span class="sxs-lookup"><span data-stu-id="2aef1-121">We could also define a schema for each within hello API app.</span></span>  

<span data-ttu-id="2aef1-122">Une autre exigence a été toopurge enregistrements après une certaine date.</span><span class="sxs-lookup"><span data-stu-id="2aef1-122">Another requirement was toopurge records after a certain date.</span></span> <span data-ttu-id="2aef1-123">COSMOS DB a une propriété appelée [temps tooLive](https://azure.microsoft.com/blog/documentdb-now-supports-time-to-live-ttl/ "temps tooLive") (TTL), ce qui nous a permis de tooset un **temps tooLive** valeur pour chaque enregistrement ou de la collection.</span><span class="sxs-lookup"><span data-stu-id="2aef1-123">Cosmos DB has a property called [Time tooLive](https://azure.microsoft.com/blog/documentdb-now-supports-time-to-live-ttl/ "Time tooLive") (TTL), which allowed us tooset a **Time tooLive** value for each record or collection.</span></span> <span data-ttu-id="2aef1-124">Cette fonctionnalité éliminée hello besoin toomanually supprimer des enregistrements dans la base de données Cosmos.</span><span class="sxs-lookup"><span data-stu-id="2aef1-124">This capability eliminated hello need toomanually delete records in Cosmos DB.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2aef1-125">toocomplete ce didacticiel, vous devez toocreate une base de données de la base de données Cosmos et deux collections (journalisation et les erreurs).</span><span class="sxs-lookup"><span data-stu-id="2aef1-125">toocomplete this tutorial, you need toocreate a Cosmos DB database and two collections (Logging and Errors).</span></span>

## <a name="create-hello-logic-app"></a><span data-ttu-id="2aef1-126">Créer la logique d’application hello</span><span class="sxs-lookup"><span data-stu-id="2aef1-126">Create hello logic app</span></span>

<span data-ttu-id="2aef1-127">première étape de Hello est toocreate hello logique application et l’application hello ouvert dans le Concepteur de la logique d’application.</span><span class="sxs-lookup"><span data-stu-id="2aef1-127">hello first step is toocreate hello logic app and open hello app in Logic App Designer.</span></span> <span data-ttu-id="2aef1-128">Dans cet exemple, nous utilisons des applications logiques parent-enfant.</span><span class="sxs-lookup"><span data-stu-id="2aef1-128">In this example, we are using parent-child logic apps.</span></span> <span data-ttu-id="2aef1-129">Supposons que nous avoir déjà créé le parent de hello et que vous allez toocreate une application de logique enfant.</span><span class="sxs-lookup"><span data-stu-id="2aef1-129">Let's assume that we have already created hello parent and are going toocreate one child logic app.</span></span>

<span data-ttu-id="2aef1-130">Étant donné que nous allons l’enregistrement de hello toolog issues de Dynamics CRM Online, nous pouvons commencer en haut de hello.</span><span class="sxs-lookup"><span data-stu-id="2aef1-130">Because we are going toolog hello record coming out of Dynamics CRM Online, let's start at hello top.</span></span> <span data-ttu-id="2aef1-131">Nous devons utiliser une **demande** déclencheur parce qu’hello parent logique application déclenche cet enfant.</span><span class="sxs-lookup"><span data-stu-id="2aef1-131">We must use a **Request** trigger because hello parent logic app triggers this child.</span></span>

### <a name="logic-app-trigger"></a><span data-ttu-id="2aef1-132">Déclencheur d’application logique</span><span class="sxs-lookup"><span data-stu-id="2aef1-132">Logic app trigger</span></span>

<span data-ttu-id="2aef1-133">Nous utilisons un **demande** déclencher comme indiqué dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="2aef1-133">We are using a **Request** trigger as shown in hello following example:</span></span>

```` json
"triggers": {
        "request": {
          "type": "request",
          "kind": "http",
          "inputs": {
            "schema": {
              "properties": {
                "CRMid": {
                  "type": "string"
                },
                "recordType": {
                  "type": "string"
                },
                "salesforceID": {
                  "type": "string"
                },
                "update": {
                  "type": "boolean"
                }
              },
              "required": [
                "CRMid",
                "recordType",
                "salesforceID",
                "update"
              ],
              "type": "object"
            }
          }
        }
      },

````


## <a name="steps"></a><span data-ttu-id="2aef1-134">Étapes</span><span class="sxs-lookup"><span data-stu-id="2aef1-134">Steps</span></span>

<span data-ttu-id="2aef1-135">Nous devons du journal source hello (requête) de patients hello de portail de Dynamics CRM Online hello.</span><span class="sxs-lookup"><span data-stu-id="2aef1-135">We must log hello source (request) of hello patient record from hello Dynamics CRM Online portal.</span></span>

1. <span data-ttu-id="2aef1-136">Nous devons d’abord obtenir un nouvel enregistrement de rendez-vous de Dynamics CRM Online.</span><span class="sxs-lookup"><span data-stu-id="2aef1-136">We must get a new appointment record from Dynamics CRM Online.</span></span>

   <span data-ttu-id="2aef1-137">déclencheur Hello en provenance de CRM nous fournit hello **CRM PatentId**, **type d’enregistrement**, **nouveau ou mis à jour un enregistrement** (nouvelle ou mise à jour de la valeur booléenne), et  **SalesforceId**.</span><span class="sxs-lookup"><span data-stu-id="2aef1-137">hello trigger coming from CRM provides us with hello **CRM PatentId**, **record type**, **New or Updated Record** (new or update Boolean value), and **SalesforceId**.</span></span> <span data-ttu-id="2aef1-138">Hello **SalesforceId** peut avoir la valeur null, car il est utilisé uniquement pour une mise à jour.</span><span class="sxs-lookup"><span data-stu-id="2aef1-138">hello **SalesforceId** can be null because it's only used for an update.</span></span>
   <span data-ttu-id="2aef1-139">Nous obtenons un enregistrement CRM hello à l’aide de hello CRM **PatientID** et hello **Type d’enregistrement**.</span><span class="sxs-lookup"><span data-stu-id="2aef1-139">We get hello CRM record by using hello CRM **PatientID** and hello **Record Type**.</span></span>

2. <span data-ttu-id="2aef1-140">Ensuite, nous devons tooadd notre application API DocumentDB **InsertLogEntry** opération comme illustré ici dans le Concepteur de la logique d’application.</span><span class="sxs-lookup"><span data-stu-id="2aef1-140">Next, we need tooadd our DocumentDB API app **InsertLogEntry** operation as shown here in Logic App Designer.</span></span>

   <span data-ttu-id="2aef1-141">**Insérer une entrée de journal**</span><span class="sxs-lookup"><span data-stu-id="2aef1-141">**Insert log entry**</span></span>

   ![Insérer une entrée de journal](media/logic-apps-scenario-error-and-exception-handling/lognewpatient.png)

   <span data-ttu-id="2aef1-143">**Insérer une entrée d’erreur**</span><span class="sxs-lookup"><span data-stu-id="2aef1-143">**Insert error entry**</span></span>

   ![Insérer une entrée de journal](media/logic-apps-scenario-error-and-exception-handling/insertlogentry.png)

   <span data-ttu-id="2aef1-145">**Rechercher un échec de création d’enregistrement**</span><span class="sxs-lookup"><span data-stu-id="2aef1-145">**Check for create record failure**</span></span>

   ![Condition](media/logic-apps-scenario-error-and-exception-handling/condition.png)

## <a name="logic-app-source-code"></a><span data-ttu-id="2aef1-147">Code source d’application logique</span><span class="sxs-lookup"><span data-stu-id="2aef1-147">Logic app source code</span></span>

> [!NOTE]
> <span data-ttu-id="2aef1-148">Hello exemple suivant est des exemples uniquement.</span><span class="sxs-lookup"><span data-stu-id="2aef1-148">hello following examples are samples only.</span></span> <span data-ttu-id="2aef1-149">Ce didacticiel est basé sur une implémentation en production, hello valeur un **nœud Source** peuvent ne pas afficher les propriétés qui sont associée tooscheduling un rendez-vous. ></span><span class="sxs-lookup"><span data-stu-id="2aef1-149">Because this tutorial is based on an implementation now in production, hello value of a **Source Node** might not display properties that are related tooscheduling an appointment.></span></span> 

### <a name="logging"></a><span data-ttu-id="2aef1-150">Journalisation</span><span class="sxs-lookup"><span data-stu-id="2aef1-150">Logging</span></span>

<span data-ttu-id="2aef1-151">Hello suivant le code d’application logique exemple montre comment toohandle journalisation.</span><span class="sxs-lookup"><span data-stu-id="2aef1-151">hello following logic app code sample shows how toohandle logging.</span></span>

#### <a name="log-entry"></a><span data-ttu-id="2aef1-152">Entrée de journal</span><span class="sxs-lookup"><span data-stu-id="2aef1-152">Log entry</span></span>

<span data-ttu-id="2aef1-153">Voici hello logique application source code pour l’insertion d’une entrée de journal.</span><span class="sxs-lookup"><span data-stu-id="2aef1-153">Here is hello logic app source code for inserting a log entry.</span></span>

``` json
"InsertLogEntry": {
        "metadata": {
        "apiDefinitionUrl": "https://.../swagger/docs/v1",
        "swaggerSource": "website"
        },
        "type": "Http",
        "inputs": {
        "body": {
            "date": "@{outputs('Gets_NewPatientRecord')['headers']['Date']}",
            "operation": "New Patient",
            "patientId": "@{triggerBody()['CRMid']}",
            "providerId": "@{triggerBody()['providerID']}",
            "source": "@{outputs('Gets_NewPatientRecord')['headers']}"
        },
        "method": "post",
        "uri": "https://.../api/Log"
        },
        "runAfter":    {
            "Gets_NewPatientecord": ["Succeeded"]
        }
}
```

#### <a name="log-request"></a><span data-ttu-id="2aef1-154">Consigner une requête</span><span class="sxs-lookup"><span data-stu-id="2aef1-154">Log request</span></span>

<span data-ttu-id="2aef1-155">Voici le message de demande de journal hello publié l’application d’API toohello.</span><span class="sxs-lookup"><span data-stu-id="2aef1-155">Here is hello log request message posted toohello API app.</span></span>

``` json
    {
    "uri": "https://.../api/Log",
    "method": "post",
    "body": {
        "date": "Fri, 10 Jun 2016 22:31:56 GMT",
        "operation": "New Patient",
        "patientId": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0",
        "providerId": "",
        "source": "{/"Pragma/":/"no-cache/",/"x-ms-request-id/":/"e750c9a9-bd48-44c4-bbba-1688b6f8a132/",/"OData-Version/":/"4.0/",/"Cache-Control/":/"no-cache/",/"Date/":/"Fri, 10 Jun 2016 22:31:56 GMT/",/"Set-Cookie/":/"ARRAffinity=785f4334b5e64d2db0b84edcc1b84f1bf37319679aefce206b51510e56fd9770;Path=/;Domain=127.0.0.1/",/"Server/":/"Microsoft-IIS/8.0,Microsoft-HTTPAPI/2.0/",/"X-AspNet-Version/":/"4.0.30319/",/"X-Powered-By/":/"ASP.NET/",/"Content-Length/":/"1935/",/"Content-Type/":/"application/json; odata.metadata=minimal; odata.streaming=true/",/"Expires/":/"-1/"}"
        }
    }

```


#### <a name="log-response"></a><span data-ttu-id="2aef1-156">Consigner une réponse</span><span class="sxs-lookup"><span data-stu-id="2aef1-156">Log response</span></span>

<span data-ttu-id="2aef1-157">Voici le message de réponse hello journal à partir de l’application d’API hello.</span><span class="sxs-lookup"><span data-stu-id="2aef1-157">Here is hello log response message from hello API app.</span></span>

``` json
{
    "statusCode": 200,
    "headers": {
        "Pragma": "no-cache",
        "Cache-Control": "no-cache",
        "Date": "Fri, 10 Jun 2016 22:32:17 GMT",
        "Server": "Microsoft-IIS/8.0",
        "X-AspNet-Version": "4.0.30319",
        "X-Powered-By": "ASP.NET",
        "Content-Length": "964",
        "Content-Type": "application/json; charset=utf-8",
        "Expires": "-1"
    },
    "body": {
        "ttl": 2592000,
        "id": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0_1465597937",
        "_rid": "XngRAOT6IQEHAAAAAAAAAA==",
        "_self": "dbs/XngRAA==/colls/XngRAOT6IQE=/docs/XngRAOT6IQEHAAAAAAAAAA==/",
        "_ts": 1465597936,
        "_etag": "/"0400fc2f-0000-0000-0000-575b3ff00000/"",
        "patientID": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0",
        "timestamp": "2016-06-10T22:31:56Z",
        "source": "{/"Pragma/":/"no-cache/",/"x-ms-request-id/":/"e750c9a9-bd48-44c4-bbba-1688b6f8a132/",/"OData-Version/":/"4.0/",/"Cache-Control/":/"no-cache/",/"Date/":/"Fri, 10 Jun 2016 22:31:56 GMT/",/"Set-Cookie/":/"ARRAffinity=785f4334b5e64d2db0b84edcc1b84f1bf37319679aefce206b51510e56fd9770;Path=/;Domain=127.0.0.1/",/"Server/":/"Microsoft-IIS/8.0,Microsoft-HTTPAPI/2.0/",/"X-AspNet-Version/":/"4.0.30319/",/"X-Powered-By/":/"ASP.NET/",/"Content-Length/":/"1935/",/"Content-Type/":/"application/json; odata.metadata=minimal; odata.streaming=true/",/"Expires/":/"-1/"}",
        "operation": "New Patient",
        "salesforceId": "",
        "expired": false
    }
}

```

<span data-ttu-id="2aef1-158">Maintenant examinons hello de gestion d’erreur comme suit.</span><span class="sxs-lookup"><span data-stu-id="2aef1-158">Now let's look at hello error handling steps.</span></span>

### <a name="error-handling"></a><span data-ttu-id="2aef1-159">Gestion des erreurs</span><span class="sxs-lookup"><span data-stu-id="2aef1-159">Error handling</span></span>

<span data-ttu-id="2aef1-160">Hello logique application exemple de code montre comment vous pouvez implémenter la gestion des erreurs.</span><span class="sxs-lookup"><span data-stu-id="2aef1-160">hello following logic app code sample shows how you can implement error handling.</span></span>

#### <a name="create-error-record"></a><span data-ttu-id="2aef1-161">Créer un enregistrement d’erreur</span><span class="sxs-lookup"><span data-stu-id="2aef1-161">Create error record</span></span>

<span data-ttu-id="2aef1-162">Voici le code de source application hello logique pour la création d’un enregistrement d’erreur.</span><span class="sxs-lookup"><span data-stu-id="2aef1-162">Here is hello logic app source code for creating an error record.</span></span>

``` json
"actions": {
    "CreateErrorRecord": {
        "metadata": {
        "apiDefinitionUrl": "https://.../swagger/docs/v1",
        "swaggerSource": "website"
        },
        "type": "Http",
        "inputs": {
        "body": {
            "action": "New_Patient",
            "isError": true,
            "crmId": "@{triggerBody()['CRMid']}",
            "patientID": "@{triggerBody()['CRMid']}",
            "message": "@{body('Create_NewPatientRecord')['message']}",
            "providerId": "@{triggerBody()['providerId']}",
            "severity": 4,
            "source": "@{actions('Create_NewPatientRecord')['inputs']['body']}",
            "statusCode": "@{int(outputs('Create_NewPatientRecord')['statusCode'])}",
            "salesforceId": "",
            "update": false
        },
        "method": "post",
        "uri": "https://.../api/CrMtoSfError"
        },
        "runAfter":
        {
            "Create_NewPatientRecord": ["Failed" ]
        }
    }
}             
```

#### <a name="insert-error-into-cosmos-db--request"></a><span data-ttu-id="2aef1-163">Erreur d’insertion dans Cosmos DB--Requête</span><span class="sxs-lookup"><span data-stu-id="2aef1-163">Insert error into Cosmos DB--request</span></span>

``` json

{
    "uri": "https://.../api/CrMtoSfError",
    "method": "post",
    "body": {
        "action": "New_Patient",
        "isError": true,
        "crmId": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0",
        "patientId": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0",
        "message": "Salesforce failed toocomplete task: Message: duplicate value found: Account_ID_MED__c duplicates value on record with id: 001U000001c83gK",
        "providerId": "",
        "severity": 4,
        "salesforceId": "",
        "update": false,
        "source": "{/"Account_Class_vod__c/":/"PRAC/",/"Account_Status_MED__c/":/"I/",/"CRM_HUB_ID__c/":/"6b115f6d-a7ee-e511-80f5-3863bb2eb2d0/",/"Credentials_vod__c/",/"DTC_ID_MED__c/":/"/",/"Fax/":/"/",/"FirstName/":/"A/",/"Gender_vod__c/":/"/",/"IMS_ID__c/":/"/",/"LastName/":/"BAILEY/",/"MasterID_mp__c/":/"/",/"C_ID_MED__c/":/"851588/",/"Middle_vod__c/":/"/",/"NPI_vod__c/":/"/",/"PDRP_MED__c/":false,/"PersonDoNotCall/":false,/"PersonEmail/":/"/",/"PersonHasOptedOutOfEmail/":false,/"PersonHasOptedOutOfFax/":false,/"PersonMobilePhone/":/"/",/"Phone/":/"/",/"Practicing_Specialty__c/":/"FM - FAMILY MEDICINE/",/"Primary_City__c/":/"/",/"Primary_State__c/":/"/",/"Primary_Street_Line2__c/":/"/",/"Primary_Street__c/":/"/",/"Primary_Zip__c/":/"/",/"RecordTypeId/":/"012U0000000JaPWIA0/",/"Request_Date__c/":/"2016-06-10T22:31:55.9647467Z/",/"ONY_ID__c/":/"/",/"Specialty_1_vod__c/":/"/",/"Suffix_vod__c/":/"/",/"Website/":/"/"}",
        "statusCode": "400"
    }
}
```

#### <a name="insert-error-into-cosmos-db--response"></a><span data-ttu-id="2aef1-164">Erreur d’insertion dans Cosmos DB--Réponse</span><span class="sxs-lookup"><span data-stu-id="2aef1-164">Insert error into Cosmos DB--response</span></span>

``` json
{
    "statusCode": 200,
    "headers": {
        "Pragma": "no-cache",
        "Cache-Control": "no-cache",
        "Date": "Fri, 10 Jun 2016 22:31:57 GMT",
        "Server": "Microsoft-IIS/8.0",
        "X-AspNet-Version": "4.0.30319",
        "X-Powered-By": "ASP.NET",
        "Content-Length": "1561",
        "Content-Type": "application/json; charset=utf-8",
        "Expires": "-1"
    },
    "body": {
        "id": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0-1465597917",
        "_rid": "sQx2APhVzAA8AAAAAAAAAA==",
        "_self": "dbs/sQx2AA==/colls/sQx2APhVzAA=/docs/sQx2APhVzAA8AAAAAAAAAA==/",
        "_ts": 1465597912,
        "_etag": "/"0c00eaac-0000-0000-0000-575b3fdc0000/"",
        "prescriberId": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0",
        "timestamp": "2016-06-10T22:31:57.3651027Z",
        "action": "New_Patient",
        "salesforceId": "",
        "update": false,
        "body": "CRM failed toocomplete task: Message: duplicate value found: CRM_HUB_ID__c duplicates value on record with id: 001U000001c83gK",
        "source": "{/"Account_Class_vod__c/":/"PRAC/",/"Account_Status_MED__c/":/"I/",/"CRM_HUB_ID__c/":/"6b115f6d-a7ee-e511-80f5-3863bb2eb2d0/",/"Credentials_vod__c/":/"DO - Degree level is DO/",/"DTC_ID_MED__c/":/"/",/"Fax/":/"/",/"FirstName/":/"A/",/"Gender_vod__c/":/"/",/"IMS_ID__c/":/"/",/"LastName/":/"BAILEY/",/"MterID_mp__c/":/"/",/"Medicis_ID_MED__c/":/"851588/",/"Middle_vod__c/":/"/",/"NPI_vod__c/":/"/",/"PDRP_MED__c/":false,/"PersonDoNotCall/":false,/"PersonEmail/":/"/",/"PersonHasOptedOutOfEmail/":false,/"PersonHasOptedOutOfFax/":false,/"PersonMobilePhone/":/"/",/"Phone/":/"/",/"Practicing_Specialty__c/":/"FM - FAMILY MEDICINE/",/"Primary_City__c/":/"/",/"Primary_State__c/":/"/",/"Primary_Street_Line2__c/":/"/",/"Primary_Street__c/":/"/",/"Primary_Zip__c/":/"/",/"RecordTypeId/":/"012U0000000JaPWIA0/",/"Request_Date__c/":/"2016-06-10T22:31:55.9647467Z/",/"XXXXXXX/":/"/",/"Specialty_1_vod__c/":/"/",/"Suffix_vod__c/":/"/",/"Website/":/"/"}",
        "code": 400,
        "errors": null,
        "isError": true,
        "severity": 4,
        "notes": null,
        "resolved": 0
        }
}
```

#### <a name="salesforce-error-response"></a><span data-ttu-id="2aef1-165">Réponse à l’erreur de Salesforce</span><span class="sxs-lookup"><span data-stu-id="2aef1-165">Salesforce error response</span></span>

``` json
{
    "statusCode": 400,
    "headers": {
        "Pragma": "no-cache",
        "x-ms-request-id": "3e8e4884-288e-4633-972c-8271b2cc912c",
        "X-Content-Type-Options": "nosniff",
        "Cache-Control": "no-cache",
        "Date": "Fri, 10 Jun 2016 22:31:56 GMT",
        "Set-Cookie": "ARRAffinity=785f4334b5e64d2db0b84edcc1b84f1bf37319679aefce206b51510e56fd9770;Path=/;Domain=127.0.0.1",
        "Server": "Microsoft-IIS/8.0,Microsoft-HTTPAPI/2.0",
        "X-AspNet-Version": "4.0.30319",
        "X-Powered-By": "ASP.NET",
        "Content-Length": "205",
        "Content-Type": "application/json; charset=utf-8",
        "Expires": "-1"
    },
    "body": {
        "status": 400,
        "message": "Salesforce failed toocomplete task: Message: duplicate value found: Account_ID_MED__c duplicates value on record with id: 001U000001c83gK",
        "source": "Salesforce.Common",
        "errors": []
    }
}

```

### <a name="return-hello-response-back-tooparent-logic-app"></a><span data-ttu-id="2aef1-166">Application de retour hello réponse tooparent précédent logique</span><span class="sxs-lookup"><span data-stu-id="2aef1-166">Return hello response back tooparent logic app</span></span>

<span data-ttu-id="2aef1-167">Après avoir obtenu la réponse de hello, vous pouvez passer la réponse de hello toohello arrière parent logique application.</span><span class="sxs-lookup"><span data-stu-id="2aef1-167">After you get hello response, you can pass hello response back toohello parent logic app.</span></span>

#### <a name="return-success-response-tooparent-logic-app"></a><span data-ttu-id="2aef1-168">Retourner l’application logique de réussite réponse tooparent</span><span class="sxs-lookup"><span data-stu-id="2aef1-168">Return success response tooparent logic app</span></span>

``` json
"SuccessResponse": {
    "runAfter":
        {
            "UpdateNew_CRMPatientResponse": ["Succeeded"]
        },
    "inputs": {
        "body": {
            "status": "Success"
    },
    "headers": {
    "    Content-type": "application/json",
        "x-ms-date": "@utcnow()"
    },
    "statusCode": 200
    },
    "type": "Response"
}
```

#### <a name="return-error-response-tooparent-logic-app"></a><span data-ttu-id="2aef1-169">Application de retour d’erreur réponse tooparent logique</span><span class="sxs-lookup"><span data-stu-id="2aef1-169">Return error response tooparent logic app</span></span>

``` json
"ErrorResponse": {
    "runAfter":
        {
            "Create_NewPatientRecord": ["Failed"]
        },
    "inputs": {
        "body": {
            "status": "BadRequest"
        },
        "headers": {
            "Content-type": "application/json",
            "x-ms-date": "@utcnow()"
        },
        "statusCode": 400
    },
    "type": "Response"
}

```


## <a name="cosmos-db-repository-and-portal"></a><span data-ttu-id="2aef1-170">Référentiel et portail Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="2aef1-170">Cosmos DB repository and portal</span></span>

<span data-ttu-id="2aef1-171">Notre solution a permis d’ajouter des fonctionnalités avec [Cosmos DB](https://azure.microsoft.com/services/documentdb).</span><span class="sxs-lookup"><span data-stu-id="2aef1-171">Our solution added capabilities with [Cosmos DB](https://azure.microsoft.com/services/documentdb).</span></span>

### <a name="error-management-portal"></a><span data-ttu-id="2aef1-172">Portail de gestion des erreurs</span><span class="sxs-lookup"><span data-stu-id="2aef1-172">Error management portal</span></span>

<span data-ttu-id="2aef1-173">des erreurs tooview hello, vous pouvez créer un enregistrements d’erreur MVC web application toodisplay hello à partir de la base de données Cosmos.</span><span class="sxs-lookup"><span data-stu-id="2aef1-173">tooview hello errors, you can create an MVC web app toodisplay hello error records from Cosmos DB.</span></span> <span data-ttu-id="2aef1-174">Hello **liste**, **détails**, **modifier**, et **supprimer** opérations sont incluses dans la version actuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="2aef1-174">hello **List**, **Details**, **Edit**, and **Delete** operations are included in hello current version.</span></span>

> [!NOTE]
> <span data-ttu-id="2aef1-175">Modifier l’opération : Cosmos DB remplace l’intégralité du document hello.</span><span class="sxs-lookup"><span data-stu-id="2aef1-175">Edit operation: Cosmos DB replaces hello entire document.</span></span> <span data-ttu-id="2aef1-176">Hello d’enregistrements affichés dans hello **liste** et **détail** les vues sont des exemples uniquement.</span><span class="sxs-lookup"><span data-stu-id="2aef1-176">hello records shown in hello **List** and **Detail** views are samples only.</span></span> <span data-ttu-id="2aef1-177">Il ne s’agit pas d’enregistrements de rendez-vous de patients réels.</span><span class="sxs-lookup"><span data-stu-id="2aef1-177">They are not actual patient appointment records.</span></span>

<span data-ttu-id="2aef1-178">Voici des exemples de notre application MVC est créé précédemment par hello décrites approche.</span><span class="sxs-lookup"><span data-stu-id="2aef1-178">Here are examples of our MVC app details created with hello previously described approach.</span></span>

#### <a name="error-management-list"></a><span data-ttu-id="2aef1-179">Liste de gestion des erreurs</span><span class="sxs-lookup"><span data-stu-id="2aef1-179">Error management list</span></span>
![Liste d'erreurs](media/logic-apps-scenario-error-and-exception-handling/errorlist.png)

#### <a name="error-management-detail-view"></a><span data-ttu-id="2aef1-181">Vue détaillée de gestion des erreurs</span><span class="sxs-lookup"><span data-stu-id="2aef1-181">Error management detail view</span></span>
![Détails de l’erreur](media/logic-apps-scenario-error-and-exception-handling/errordetails.png)

### <a name="log-management-portal"></a><span data-ttu-id="2aef1-183">Portail de gestion des journaux</span><span class="sxs-lookup"><span data-stu-id="2aef1-183">Log management portal</span></span>

<span data-ttu-id="2aef1-184">journaux de hello tooview, nous avons créé également une application web MVC.</span><span class="sxs-lookup"><span data-stu-id="2aef1-184">tooview hello logs, we also created an MVC web app.</span></span> <span data-ttu-id="2aef1-185">Voici des exemples de notre application MVC est créé précédemment par hello décrites approche.</span><span class="sxs-lookup"><span data-stu-id="2aef1-185">Here are examples of our MVC app details created with hello previously described approach.</span></span>

#### <a name="sample-log-detail-view"></a><span data-ttu-id="2aef1-186">Exemple de vue détaillée de journal</span><span class="sxs-lookup"><span data-stu-id="2aef1-186">Sample log detail view</span></span>
![Vue détaillée de journal](media/logic-apps-scenario-error-and-exception-handling/samplelogdetail.png)

### <a name="api-app-details"></a><span data-ttu-id="2aef1-188">Détails de l’application API</span><span class="sxs-lookup"><span data-stu-id="2aef1-188">API app details</span></span>

#### <a name="logic-apps-exception-management-api"></a><span data-ttu-id="2aef1-189">API de gestion des exceptions Logic Apps</span><span class="sxs-lookup"><span data-stu-id="2aef1-189">Logic Apps exception management API</span></span>

<span data-ttu-id="2aef1-190">Notre application API de gestion des exceptions Azure Logic Apps en open source fournit les fonctionnalités décrites ici (il y a deux contrôleurs) :</span><span class="sxs-lookup"><span data-stu-id="2aef1-190">Our open-source Azure Logic Apps exception management API app provides functionality as described here - there are two controllers:</span></span>

* <span data-ttu-id="2aef1-191">**ErrorController** insère un enregistrement d’erreur (document) dans une collection DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="2aef1-191">**ErrorController** inserts an error record (document) in a DocumentDB collection.</span></span>
* <span data-ttu-id="2aef1-192">**LogController** insère un enregistrement de journal (document) dans une collection DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="2aef1-192">**LogController** Inserts a log record (document) in a DocumentDB collection.</span></span>

> [!TIP]
> <span data-ttu-id="2aef1-193">Les deux contrôleurs utilisent `async Task<dynamic>` opérations, permettant ainsi l’opérations tooresolve lors de l’exécution, afin que nous pouvons créer hello schéma DocumentDB dans les corps de hello d’opération de hello.</span><span class="sxs-lookup"><span data-stu-id="2aef1-193">Both controllers use `async Task<dynamic>` operations, allowing operations tooresolve at runtime, so we can create hello DocumentDB schema in hello body of hello operation.</span></span> 
> 

<span data-ttu-id="2aef1-194">Chaque document de DocumentDB doit posséder un ID unique.</span><span class="sxs-lookup"><span data-stu-id="2aef1-194">Every document in DocumentDB must have a unique ID.</span></span> <span data-ttu-id="2aef1-195">Nous utilisons `PatientId` et l’ajout d’un horodateur est converti de valeur d’horodateur tooa Unix (double).</span><span class="sxs-lookup"><span data-stu-id="2aef1-195">We are using `PatientId` and adding a timestamp that is converted tooa Unix timestamp value (double).</span></span> <span data-ttu-id="2aef1-196">Nous tronquer hello tooremove hello fractions de seconde valeur.</span><span class="sxs-lookup"><span data-stu-id="2aef1-196">We truncate hello value tooremove hello fractional value.</span></span>

<span data-ttu-id="2aef1-197">Vous pouvez afficher le code source de hello de notre contrôleur erreur API [à partir de GitHub](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi/blob/master/Logic App Exception Management API/Controllers/ErrorController.cs).</span><span class="sxs-lookup"><span data-stu-id="2aef1-197">You can view hello source code of our error controller API [from GitHub](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi/blob/master/Logic App Exception Management API/Controllers/ErrorController.cs).</span></span>

<span data-ttu-id="2aef1-198">Nous appelons hello API à partir d’une application logique à l’aide de la syntaxe de hello :</span><span class="sxs-lookup"><span data-stu-id="2aef1-198">We call hello API from a logic app by using hello following syntax:</span></span>

``` json
 "actions": {
        "CreateErrorRecord": {
          "metadata": {
            "apiDefinitionUrl": "https://.../swagger/docs/v1",
            "swaggerSource": "website"
          },
          "type": "Http",
          "inputs": {
            "body": {
              "action": "New_Patient",
              "isError": true,
              "crmId": "@{triggerBody()['CRMid']}",
              "prescriberId": "@{triggerBody()['CRMid']}",
              "message": "@{body('Create_NewPatientRecord')['message']}",
              "salesforceId": "@{triggerBody()['salesforceID']}",
              "severity": 4,
              "source": "@{actions('Create_NewPatientRecord')['inputs']['body']}",
              "statusCode": "@{int(outputs('Create_NewPatientRecord')['statusCode'])}",
              "update": false
            },
            "method": "post",
            "uri": "https://.../api/CrMtoSfError"
          },
          "runAfter": {
              "Create_NewPatientRecord": ["Failed"]
            }
        }
 }
```

<span data-ttu-id="2aef1-199">Hello expression Bonjour précédant les vérifications d’exemple de code pour hello *Create_NewPatientRecord* état **n’a pas pu**.</span><span class="sxs-lookup"><span data-stu-id="2aef1-199">hello expression in hello preceding code sample checks for hello *Create_NewPatientRecord* status of **Failed**.</span></span>

## <a name="summary"></a><span data-ttu-id="2aef1-200">Résumé</span><span class="sxs-lookup"><span data-stu-id="2aef1-200">Summary</span></span>

* <span data-ttu-id="2aef1-201">Vous pouvez facilement implémenter la journalisation et la gestion des erreurs dans une application logique.</span><span class="sxs-lookup"><span data-stu-id="2aef1-201">You can easily implement logging and error handling in a logic app.</span></span>
* <span data-ttu-id="2aef1-202">Vous pouvez utiliser DocumentDB comme référentiel de hello pour les enregistrements de journal et d’erreur (documents).</span><span class="sxs-lookup"><span data-stu-id="2aef1-202">You can use DocumentDB as hello repository for log and error records (documents).</span></span>
* <span data-ttu-id="2aef1-203">Vous pouvez utiliser MVC toocreate un journal toodisplay portail et les enregistrements d’erreur.</span><span class="sxs-lookup"><span data-stu-id="2aef1-203">You can use MVC toocreate a portal toodisplay log and error records.</span></span>

### <a name="source-code"></a><span data-ttu-id="2aef1-204">Code source</span><span class="sxs-lookup"><span data-stu-id="2aef1-204">Source code</span></span>

<span data-ttu-id="2aef1-205">code source Hello hello gestion des exceptions Logic Apps application API est disponible dans cette [référentiel GitHub](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi "API de gestion des exceptions logique d’application").</span><span class="sxs-lookup"><span data-stu-id="2aef1-205">hello source code for hello Logic Apps exception management API application is available in this [GitHub repository](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi "Logic App Exception Management API").</span></span>

## <a name="next-steps"></a><span data-ttu-id="2aef1-206">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2aef1-206">Next steps</span></span>

* [<span data-ttu-id="2aef1-207">Afficher d’autres exemples et scénarios d’applications logiques</span><span class="sxs-lookup"><span data-stu-id="2aef1-207">View more logic app examples and scenarios</span></span>](../logic-apps/logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="2aef1-208">En savoir plus sur la gestion des applications logiques</span><span class="sxs-lookup"><span data-stu-id="2aef1-208">Learn about monitoring logic apps</span></span>](../logic-apps/logic-apps-monitor-your-logic-apps.md)
* [<span data-ttu-id="2aef1-209">Créer un modèle de déploiement automatisé d’applications logiques</span><span class="sxs-lookup"><span data-stu-id="2aef1-209">Create automated deployment templates for logic apps</span></span>](../logic-apps/logic-apps-create-deploy-template.md)
