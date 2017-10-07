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
# <a name="scenario-exception-handling-and-error-logging-for-logic-apps"></a>Scénario : gestion des exceptions et journalisation des erreurs pour les applications logiques

Ce scénario décrit comment vous pouvez étendre une logique application toobetter prise en charge la gestion des exceptions. Nous avons utilisé une question de hello tooanswer cas utilisation concrète : « Azure Logic Apps prend en charge exception et la gestion des erreurs ? »

> [!NOTE]
> schéma de Azure Logic Apps actuel Hello fournit un modèle standard pour les réponses de l’action. Ce schéma inclut les réponses de type validation interne et de type erreur retournées depuis une application API.

## <a name="scenario-and-use-case-overview"></a>Vue d’ensemble du scénario et du cas d’utilisation

Voici un récit hello en cas d’usage hello pour ce scénario : 

Une organisation de soins de santé connue nous engagé toodevelop une solution Azure qui créerait un patient portail à l’aide de Microsoft Dynamics CRM Online. Ils nécessaire des enregistrements de rendez-vous toosend entre hello du portail patient Dynamics CRM Online et Salesforce. Nous avons demandées toouse hello [HL7 FHIR](http://www.hl7.org/implement/standards/fhir/) standard pour tous les patients.

projet de Hello comportait deux exigences principales :  

* Une méthode toolog enregistre envoyés à partir de hello portail Dynamics CRM Online
* Un moyen tooview toutes les erreurs qui se sont produits dans le flux de travail hello

> [!TIP]
> Pour visionner une vidéo de haut niveau de ce projet, consultez [groupe utilisateur d’intégration](http://www.integrationusergroup.com/logic-apps-support-error-handling/ "groupe utilisateur d’intégration").

## <a name="how-we-solved-hello-problem"></a>Comment nous avons résolu le problème de hello

Nous avons choisi [base de données Azure Cosmos](https://azure.microsoft.com/services/documentdb/ "base de données Azure Cosmos") comme référentiel pour les enregistrements de journal et d’erreur hello (Cosmos DB fait référence toorecords sous forme de documents). Azure Logic Apps ayant un modèle standard pour toutes les réponses, nous n’aurait pas toocreate un schéma personnalisé. Nous pouvons créer une application API trop**insérer** et **requête** pour les enregistrements d’erreur et de journal. Nous avons également définir un schéma pour chaque application d’API hello.  

Une autre exigence a été toopurge enregistrements après une certaine date. COSMOS DB a une propriété appelée [temps tooLive](https://azure.microsoft.com/blog/documentdb-now-supports-time-to-live-ttl/ "temps tooLive") (TTL), ce qui nous a permis de tooset un **temps tooLive** valeur pour chaque enregistrement ou de la collection. Cette fonctionnalité éliminée hello besoin toomanually supprimer des enregistrements dans la base de données Cosmos.

> [!IMPORTANT]
> toocomplete ce didacticiel, vous devez toocreate une base de données de la base de données Cosmos et deux collections (journalisation et les erreurs).

## <a name="create-hello-logic-app"></a>Créer la logique d’application hello

première étape de Hello est toocreate hello logique application et l’application hello ouvert dans le Concepteur de la logique d’application. Dans cet exemple, nous utilisons des applications logiques parent-enfant. Supposons que nous avoir déjà créé le parent de hello et que vous allez toocreate une application de logique enfant.

Étant donné que nous allons l’enregistrement de hello toolog issues de Dynamics CRM Online, nous pouvons commencer en haut de hello. Nous devons utiliser une **demande** déclencheur parce qu’hello parent logique application déclenche cet enfant.

### <a name="logic-app-trigger"></a>Déclencheur d’application logique

Nous utilisons un **demande** déclencher comme indiqué dans hello l’exemple suivant :

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


## <a name="steps"></a>Étapes

Nous devons du journal source hello (requête) de patients hello de portail de Dynamics CRM Online hello.

1. Nous devons d’abord obtenir un nouvel enregistrement de rendez-vous de Dynamics CRM Online.

   déclencheur Hello en provenance de CRM nous fournit hello **CRM PatentId**, **type d’enregistrement**, **nouveau ou mis à jour un enregistrement** (nouvelle ou mise à jour de la valeur booléenne), et  **SalesforceId**. Hello **SalesforceId** peut avoir la valeur null, car il est utilisé uniquement pour une mise à jour.
   Nous obtenons un enregistrement CRM hello à l’aide de hello CRM **PatientID** et hello **Type d’enregistrement**.

2. Ensuite, nous devons tooadd notre application API DocumentDB **InsertLogEntry** opération comme illustré ici dans le Concepteur de la logique d’application.

   **Insérer une entrée de journal**

   ![Insérer une entrée de journal](media/logic-apps-scenario-error-and-exception-handling/lognewpatient.png)

   **Insérer une entrée d’erreur**

   ![Insérer une entrée de journal](media/logic-apps-scenario-error-and-exception-handling/insertlogentry.png)

   **Rechercher un échec de création d’enregistrement**

   ![Condition](media/logic-apps-scenario-error-and-exception-handling/condition.png)

## <a name="logic-app-source-code"></a>Code source d’application logique

> [!NOTE]
> Hello exemple suivant est des exemples uniquement. Ce didacticiel est basé sur une implémentation en production, hello valeur un **nœud Source** peuvent ne pas afficher les propriétés qui sont associée tooscheduling un rendez-vous. > 

### <a name="logging"></a>Journalisation

Hello suivant le code d’application logique exemple montre comment toohandle journalisation.

#### <a name="log-entry"></a>Entrée de journal

Voici hello logique application source code pour l’insertion d’une entrée de journal.

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

#### <a name="log-request"></a>Consigner une requête

Voici le message de demande de journal hello publié l’application d’API toohello.

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


#### <a name="log-response"></a>Consigner une réponse

Voici le message de réponse hello journal à partir de l’application d’API hello.

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

Maintenant examinons hello de gestion d’erreur comme suit.

### <a name="error-handling"></a>Gestion des erreurs

Hello logique application exemple de code montre comment vous pouvez implémenter la gestion des erreurs.

#### <a name="create-error-record"></a>Créer un enregistrement d’erreur

Voici le code de source application hello logique pour la création d’un enregistrement d’erreur.

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

#### <a name="insert-error-into-cosmos-db--request"></a>Erreur d’insertion dans Cosmos DB--Requête

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

#### <a name="insert-error-into-cosmos-db--response"></a>Erreur d’insertion dans Cosmos DB--Réponse

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

#### <a name="salesforce-error-response"></a>Réponse à l’erreur de Salesforce

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

### <a name="return-hello-response-back-tooparent-logic-app"></a>Application de retour hello réponse tooparent précédent logique

Après avoir obtenu la réponse de hello, vous pouvez passer la réponse de hello toohello arrière parent logique application.

#### <a name="return-success-response-tooparent-logic-app"></a>Retourner l’application logique de réussite réponse tooparent

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

#### <a name="return-error-response-tooparent-logic-app"></a>Application de retour d’erreur réponse tooparent logique

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


## <a name="cosmos-db-repository-and-portal"></a>Référentiel et portail Cosmos DB

Notre solution a permis d’ajouter des fonctionnalités avec [Cosmos DB](https://azure.microsoft.com/services/documentdb).

### <a name="error-management-portal"></a>Portail de gestion des erreurs

des erreurs tooview hello, vous pouvez créer un enregistrements d’erreur MVC web application toodisplay hello à partir de la base de données Cosmos. Hello **liste**, **détails**, **modifier**, et **supprimer** opérations sont incluses dans la version actuelle de hello.

> [!NOTE]
> Modifier l’opération : Cosmos DB remplace l’intégralité du document hello. Hello d’enregistrements affichés dans hello **liste** et **détail** les vues sont des exemples uniquement. Il ne s’agit pas d’enregistrements de rendez-vous de patients réels.

Voici des exemples de notre application MVC est créé précédemment par hello décrites approche.

#### <a name="error-management-list"></a>Liste de gestion des erreurs
![Liste d'erreurs](media/logic-apps-scenario-error-and-exception-handling/errorlist.png)

#### <a name="error-management-detail-view"></a>Vue détaillée de gestion des erreurs
![Détails de l’erreur](media/logic-apps-scenario-error-and-exception-handling/errordetails.png)

### <a name="log-management-portal"></a>Portail de gestion des journaux

journaux de hello tooview, nous avons créé également une application web MVC. Voici des exemples de notre application MVC est créé précédemment par hello décrites approche.

#### <a name="sample-log-detail-view"></a>Exemple de vue détaillée de journal
![Vue détaillée de journal](media/logic-apps-scenario-error-and-exception-handling/samplelogdetail.png)

### <a name="api-app-details"></a>Détails de l’application API

#### <a name="logic-apps-exception-management-api"></a>API de gestion des exceptions Logic Apps

Notre application API de gestion des exceptions Azure Logic Apps en open source fournit les fonctionnalités décrites ici (il y a deux contrôleurs) :

* **ErrorController** insère un enregistrement d’erreur (document) dans une collection DocumentDB.
* **LogController** insère un enregistrement de journal (document) dans une collection DocumentDB.

> [!TIP]
> Les deux contrôleurs utilisent `async Task<dynamic>` opérations, permettant ainsi l’opérations tooresolve lors de l’exécution, afin que nous pouvons créer hello schéma DocumentDB dans les corps de hello d’opération de hello. 
> 

Chaque document de DocumentDB doit posséder un ID unique. Nous utilisons `PatientId` et l’ajout d’un horodateur est converti de valeur d’horodateur tooa Unix (double). Nous tronquer hello tooremove hello fractions de seconde valeur.

Vous pouvez afficher le code source de hello de notre contrôleur erreur API [à partir de GitHub](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi/blob/master/Logic App Exception Management API/Controllers/ErrorController.cs).

Nous appelons hello API à partir d’une application logique à l’aide de la syntaxe de hello :

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

Hello expression Bonjour précédant les vérifications d’exemple de code pour hello *Create_NewPatientRecord* état **n’a pas pu**.

## <a name="summary"></a>Résumé

* Vous pouvez facilement implémenter la journalisation et la gestion des erreurs dans une application logique.
* Vous pouvez utiliser DocumentDB comme référentiel de hello pour les enregistrements de journal et d’erreur (documents).
* Vous pouvez utiliser MVC toocreate un journal toodisplay portail et les enregistrements d’erreur.

### <a name="source-code"></a>Code source

code source Hello hello gestion des exceptions Logic Apps application API est disponible dans cette [référentiel GitHub](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi "API de gestion des exceptions logique d’application").

## <a name="next-steps"></a>Étapes suivantes

* [Afficher d’autres exemples et scénarios d’applications logiques](../logic-apps/logic-apps-examples-and-scenarios.md)
* [En savoir plus sur la gestion des applications logiques](../logic-apps/logic-apps-monitor-your-logic-apps.md)
* [Créer un modèle de déploiement automatisé d’applications logiques](../logic-apps/logic-apps-create-deploy-template.md)
