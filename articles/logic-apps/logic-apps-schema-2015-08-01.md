---
title: "met à jour aaaSchema août-1-2015 preview - Azure Logic Apps | Documents Microsoft"
description: "Créer des définitions JSON pour Azure Logic Apps avec la version de schéma 2015-08-01 (version préliminaire)"
author: stepsic-microsoft-com
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 0d03a4d4-e8a8-4c81-aed5-bfd2a28c7f0c
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 05/31/2016
ms.author: LADocs; stepsic
ms.openlocfilehash: 950cd18a27aa1859c4f0b6116de3fb8699d746c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="schema-updates-for-azure-logic-apps---august-1-2015-preview"></a><span data-ttu-id="b5692-103">Mises à jour de schéma pour Azure Logic Apps - Version préliminaire du 1er août 2015</span><span class="sxs-lookup"><span data-stu-id="b5692-103">Schema updates for Azure Logic Apps - August 1, 2015 preview</span></span>

<span data-ttu-id="b5692-104">Ce schéma et une API version pour Azure Logic Apps inclut des améliorations clés qui rendent les applications logique plus fiable et plus facile de toouse :</span><span class="sxs-lookup"><span data-stu-id="b5692-104">This new schema and API version for Azure Logic Apps includes key improvements that make logic apps more reliable and easier toouse:</span></span>

*   <span data-ttu-id="b5692-105">Hello **APIApp** type d’action est mis à jour tooa nouvelle [ **APIConnection** ](#api-connections) type d’action.</span><span class="sxs-lookup"><span data-stu-id="b5692-105">hello **APIApp** action type is updated tooa new [**APIConnection**](#api-connections) action type.</span></span>
*   <span data-ttu-id="b5692-106">**Répétez les** est renommé trop[**Foreach**](#foreach).</span><span class="sxs-lookup"><span data-stu-id="b5692-106">**Repeat** is renamed too[**Foreach**](#foreach).</span></span>
*   <span data-ttu-id="b5692-107">Hello [ **écouteur HTTP** application API](#http-listener) n’est plus nécessaire.</span><span class="sxs-lookup"><span data-stu-id="b5692-107">hello [**HTTP Listener** API App](#http-listener) is no longer required.</span></span>
*   <span data-ttu-id="b5692-108">L’appel des flux de travail enfants utilise un [nouveau schéma](#child-workflows).</span><span class="sxs-lookup"><span data-stu-id="b5692-108">Calling child workflows uses a [new schema](#child-workflows).</span></span>

<a name="api-connections"></a>
## <a name="move-tooapi-connections"></a><span data-ttu-id="b5692-109">Déplacer les connexions tooAPI</span><span class="sxs-lookup"><span data-stu-id="b5692-109">Move tooAPI connections</span></span>

<span data-ttu-id="b5692-110">modification de plus grande Hello est que vous n’avez plus toodeploy API Apps dans votre abonnement Azure afin de pouvoir utiliser les API.</span><span class="sxs-lookup"><span data-stu-id="b5692-110">hello biggest change is that you no longer have toodeploy API Apps into your Azure subscription so you can use APIs.</span></span> <span data-ttu-id="b5692-111">Voici quelques conseils hello que vous pouvez utiliser les API :</span><span class="sxs-lookup"><span data-stu-id="b5692-111">Here are hello ways that you can use APIs:</span></span>

* <span data-ttu-id="b5692-112">API gérées</span><span class="sxs-lookup"><span data-stu-id="b5692-112">Managed APIs</span></span>
* <span data-ttu-id="b5692-113">Vos API web personnalisées</span><span class="sxs-lookup"><span data-stu-id="b5692-113">Your custom Web APIs</span></span>

<span data-ttu-id="b5692-114">Chacune de ces méthodes fait l’objet d’un traitement légèrement différent, car leurs modèles de gestion et d’hébergement sont différents.</span><span class="sxs-lookup"><span data-stu-id="b5692-114">Each way is handled slightly differently because their management and hosting models are different.</span></span> <span data-ttu-id="b5692-115">Un avantage de ce modèle est que vous êtes limité n’est plus tooresources qui sont déployés dans votre groupe de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="b5692-115">One advantage of this model is you're no longer constrained tooresources that are deployed in your Azure resource group.</span></span> 

### <a name="managed-apis"></a><span data-ttu-id="b5692-116">API gérées</span><span class="sxs-lookup"><span data-stu-id="b5692-116">Managed APIs</span></span>

<span data-ttu-id="b5692-117">Microsoft gère certaines API à votre place, comme Office 365, Salesforce, Twitter et FTP.</span><span class="sxs-lookup"><span data-stu-id="b5692-117">Microsoft manages some APIs on your behalf, such as Office 365, Salesforce, Twitter, and FTP.</span></span> <span data-ttu-id="b5692-118">Vous pouvez utiliser des API gérées (par exemple, Bing Translate), tandis que d’autres nécessitent une configuration.</span><span class="sxs-lookup"><span data-stu-id="b5692-118">You can use some managed APIs as-is, such as Bing Translate, while others require configuration.</span></span> <span data-ttu-id="b5692-119">Cette configuration est appelée une *connexion*.</span><span class="sxs-lookup"><span data-stu-id="b5692-119">This configuration is called a *connection*.</span></span>

<span data-ttu-id="b5692-120">Par exemple, lorsque vous utilisez Office 365, vous devez créer une connexion qui contient votre jeton de connexion Office 365.</span><span class="sxs-lookup"><span data-stu-id="b5692-120">For example, when you use Office 365, you must create a connection that contains your Office 365 sign-in token.</span></span> <span data-ttu-id="b5692-121">Ce jeton est en toute sécurité enregistrée et actualisé, afin que votre application logique peut appeler toujours hello API Office 365.</span><span class="sxs-lookup"><span data-stu-id="b5692-121">This token is securely stored and refreshed so that your logic app can always call hello Office 365 API.</span></span> <span data-ttu-id="b5692-122">Vous pouvez également, si vous souhaitez que le serveur SQL ou FTP du tooyour tooconnect, vous devez créer une connexion avec la chaîne de connexion hello.</span><span class="sxs-lookup"><span data-stu-id="b5692-122">Alternatively, if you want tooconnect tooyour SQL or FTP server, you must create a connection that has hello connection string.</span></span> 

<span data-ttu-id="b5692-123">Dans la définition, ces actions sont appelées `APIConnection`.</span><span class="sxs-lookup"><span data-stu-id="b5692-123">In this definition, these actions are called `APIConnection`.</span></span> <span data-ttu-id="b5692-124">Voici un exemple d’une connexion qui appelle toosend d’Office 365 à un message électronique :</span><span class="sxs-lookup"><span data-stu-id="b5692-124">Here is an example of a connection that calls Office 365 toosend an email:</span></span>

```
{
    "actions": {
        "Send_Email": {
            "type": "ApiConnection",
            "inputs": {
                "host": {
                    "api": {
                        "runtimeUrl": "https://msmanaged-na.azure-apim.net/apim/office365"
                    },
                    "connection": {
                        "name": "@parameters('$connections')['shared_office365']['connectionId']"
                    }
                },
                "method": "post",
                "body": {
                    "Subject": "Reminder",
                    "Body": "Don't forget!",
                    "To": "me@contoso.com"
                },
                "path": "/Mail"
            }
        }
    }
}
```

<span data-ttu-id="b5692-125">Hello `host` objet est la partie d’entrées uniques tooAPI connexions, et contient des pièces de câbles : `api` et `connection`.</span><span class="sxs-lookup"><span data-stu-id="b5692-125">hello `host` object is portion of inputs that is unique tooAPI connections, and contains tow parts: `api` and `connection`.</span></span>

<span data-ttu-id="b5692-126">Hello `api` a runtime hello URL d’où qui API managée est hébergé.</span><span class="sxs-lookup"><span data-stu-id="b5692-126">hello `api` has hello runtime URL of where that managed API is hosted.</span></span> <span data-ttu-id="b5692-127">Vous pouvez voir tous les hello disponibles d’API gérées en appelant `GET https://management.azure.com/subscriptions/{subid}/providers/Microsoft.Web/managedApis/?api-version=2015-08-01-preview`.</span><span class="sxs-lookup"><span data-stu-id="b5692-127">You can see all hello available managed APIs by calling `GET https://management.azure.com/subscriptions/{subid}/providers/Microsoft.Web/managedApis/?api-version=2015-08-01-preview`.</span></span>

<span data-ttu-id="b5692-128">Lorsque vous utilisez une API, hello API peut ou ne peut pas avoir un *les paramètres de connexion* défini.</span><span class="sxs-lookup"><span data-stu-id="b5692-128">When you use an API, hello API might or might not have any *connection parameters* defined.</span></span> <span data-ttu-id="b5692-129">Si hello API n’est pas, aucune *connexion* est requis.</span><span class="sxs-lookup"><span data-stu-id="b5692-129">If hello API doesn't, no *connection* is required.</span></span> <span data-ttu-id="b5692-130">En cas de hello API, vous devez créer une connexion.</span><span class="sxs-lookup"><span data-stu-id="b5692-130">If hello API does, you must create a connection.</span></span> <span data-ttu-id="b5692-131">connexion de Hello créé a nom hello que vous choisissez.</span><span class="sxs-lookup"><span data-stu-id="b5692-131">hello created connection has hello name that you choose.</span></span> <span data-ttu-id="b5692-132">Vous ensuite référencez nom hello Bonjour `connection` objet à l’intérieur de hello `host` objet.</span><span class="sxs-lookup"><span data-stu-id="b5692-132">You then reference hello name in hello `connection` object inside hello `host` object.</span></span> <span data-ttu-id="b5692-133">une connexion dans un groupe de ressources, appel de toocreate :</span><span class="sxs-lookup"><span data-stu-id="b5692-133">toocreate a connection in a resource group, call:</span></span>

```
PUT https://management.azure.com/subscriptions/{subid}/resourceGroups/{rgname}/providers/Microsoft.Web/connections/{name}?api-version=2015-08-01-preview
```

<span data-ttu-id="b5692-134">Avec hello suivant corps :</span><span class="sxs-lookup"><span data-stu-id="b5692-134">With hello following body:</span></span>

```
{
  "properties": {
    "api": {
      "id": "/subscriptions/{subid}/providers/Microsoft.Web/managedApis/azureblob"
    },
    "parameterValues": {
        "accountName": "{hello name of hello storage account -- hello set of parameters is different for each API}"
    }
  },
  "location": "{Logic app's location}"
}
```

### <a name="deploy-managed-apis-in-an-azure-resource-manager-template"></a><span data-ttu-id="b5692-135">Déploiement d’API gérées dans un modèle Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b5692-135">Deploy managed APIs in an Azure Resource Manager template</span></span>

<span data-ttu-id="b5692-136">Vous pouvez créer une application complète dans un modèle Azure Resource Manager, tant qu’elle ne nécessite aucune connexion interactive.</span><span class="sxs-lookup"><span data-stu-id="b5692-136">You can create a full application in an Azure Resource Manager template as long as interactive sign-in isn't required.</span></span>
<span data-ttu-id="b5692-137">Si la connexion est nécessaire, vous pouvez configurer tous les éléments avec le modèle de gestionnaire de ressources Azure hello, mais vous que les connexions de hello toovisit hello tooauthorize portail.</span><span class="sxs-lookup"><span data-stu-id="b5692-137">If sign-in is required, you can set up everything with hello Azure Resource Manager template, but you still have toovisit hello portal tooauthorize hello connections.</span></span> 

```
    "resources": [{
        "apiVersion": "2015-08-01-preview",
        "name": "azureblob",
        "type": "Microsoft.Web/connections",
        "location": "[resourceGroup().location]",
        "properties": {
            "api": {
                "id": "[concat(subscription().id,'/providers/Microsoft.Web/locations/westus/managedApis/azureblob')]"
            },
            "parameterValues": {
                "accountName": "[parameters('storageAccountName')]",
                "accessKey": "[parameters('storageAccountKey')]"
            }
        }
    }, {
        "type": "Microsoft.Logic/workflows",
        "apiVersion": "2015-08-01-preview",
        "name": "[parameters('logicAppName')]",
        "location": "[resourceGroup().location]",
        "dependsOn": ["[resourceId('Microsoft.Web/connections', 'azureblob')]"
        ],
        "properties": {
            "sku": {
                "name": "[parameters('sku')]",
                "plan": {
                    "id": "[concat(resourceGroup().id, '/providers/Microsoft.Web/serverfarms/',parameters('svcPlanName'))]"
                }
            },
            "definition": {
                "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2015-08-01-preview/workflowdefinition.json#",
                "actions": {
                    "Create_file": {
                        "type": "apiconnection",
                        "inputs": {
                            "host": {
                                "api": {
                                    "runtimeUrl": "https://logic-apis-westus.azure-apim.net/apim/azureblob"
                                },
                                "connection": {
                                    "name": "@parameters('$connections')['azureblob']['connectionId']"
                                }
                            },
                            "method": "post",
                            "queries": {
                                "folderPath": "[concat('/', parameters('containerName'))]",
                                "name": "helloworld.txt"
                            },
                            "body": "@decodeDataUri('data:, Hello+world!')",
                            "path": "/datasets/default/files"
                        },
                        "conditions": []
                    }
                },
                "contentVersion": "1.0.0.0",
                "outputs": {},
                "parameters": {
                    "$connections": {
                        "defaultValue": {},
                        "type": "Object"
                    }
                },
                "triggers": {
                    "recurrence": {
                        "type": "Recurrence",
                        "recurrence": {
                            "frequency": "Day",
                            "interval": 1
                        }
                    }
                }
            },
            "parameters": {
                "$connections": {
                    "value": {
                        "azureblob": {
                            "connectionId": "[concat(resourceGroup().id,'/providers/Microsoft.Web/connections/azureblob')]",
                            "connectionName": "azureblob",
                            "id": "[concat(subscription().id,'/providers/Microsoft.Web/locations/westus/managedApis/azureblob')]"
                        }

                    }
                }
            }
        }
    }]
```

<span data-ttu-id="b5692-138">Vous pouvez le voir dans cet exemple, les connexions hello sont simplement aux ressources qui se trouvent dans votre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="b5692-138">You can see in this example that hello connections are just resources that live in your resource group.</span></span> <span data-ttu-id="b5692-139">Elles font référence à hello géré API disponible tooyou dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="b5692-139">They reference hello managed APIs available tooyou in your subscription.</span></span>

### <a name="your-custom-web-apis"></a><span data-ttu-id="b5692-140">Vos API web personnalisées</span><span class="sxs-lookup"><span data-stu-id="b5692-140">Your custom Web APIs</span></span>

<span data-ttu-id="b5692-141">Si vous utilisez votre propre API, ceux qui sont pas gérés par Microsoft, utiliser intégrée de hello **HTTP** action toocall les.</span><span class="sxs-lookup"><span data-stu-id="b5692-141">If you use your own APIs, not Microsoft-managed ones, use hello built-in **HTTP** action toocall them.</span></span> <span data-ttu-id="b5692-142">Pour une expérience optimale, vous avez tout intérêt à exposer un point de terminaison swagger pour votre API.</span><span class="sxs-lookup"><span data-stu-id="b5692-142">For an ideal experience, you should expose a Swagger endpoint for your API.</span></span> <span data-ttu-id="b5692-143">Ce point de terminaison permet d’entrées de hello toorender hello Concepteur de logique d’application et fournit en sortie de votre API.</span><span class="sxs-lookup"><span data-stu-id="b5692-143">This endpoint enables hello Logic App Designer toorender hello inputs and outputs for your API.</span></span> <span data-ttu-id="b5692-144">Sans Swagger, Concepteur de hello peut uniquement afficher hello entrées et sorties en tant qu’objets JSON opaques.</span><span class="sxs-lookup"><span data-stu-id="b5692-144">Without Swagger, hello designer can only show hello inputs and outputs as opaque JSON objects.</span></span>

<span data-ttu-id="b5692-145">Voici un hello d’affichage exemple nouvelle `metadata.apiDefinitionUrl` propriété :</span><span class="sxs-lookup"><span data-stu-id="b5692-145">Here is an example showing hello new `metadata.apiDefinitionUrl` property:</span></span>

```
{
   "actions": {
        "mycustomAPI": {
            "type": "http",
            "metadata": {
              "apiDefinitionUrl": "https://mysite.azurewebsites.net/api/apidef/"  
            },
            "inputs": {
                "uri": "https://mysite.azurewebsites.net/api/getsomedata",
                "method": "GET"
            }
        }
    }
}
```

<span data-ttu-id="b5692-146">Si vous hébergez votre API Web sur Azure App Service, votre API Web s’affiche automatiquement dans la liste hello des actions disponibles dans le Concepteur de hello.</span><span class="sxs-lookup"><span data-stu-id="b5692-146">If you host your Web API on Azure App Service, your Web API automatically appears in hello list of actions available in hello designer.</span></span> <span data-ttu-id="b5692-147">Si ce n’est pas le cas, vous avez toopaste dans l’URL de hello directement.</span><span class="sxs-lookup"><span data-stu-id="b5692-147">If not, you have toopaste in hello URL directly.</span></span> <span data-ttu-id="b5692-148">point de terminaison Swagger Hello doit être non authentifiée toobe utilisable dans hello Concepteur de logique d’application, bien que vous pouvez sécuriser les API de hello elle-même avec toutes les méthodes qui prend en charge de Swagger.</span><span class="sxs-lookup"><span data-stu-id="b5692-148">hello Swagger endpoint must be unauthenticated toobe usable in hello Logic App Designer, although you can secure hello API itself with whatever methods that Swagger supports.</span></span>

### <a name="call-deployed-api-apps-with-2015-08-01-preview"></a><span data-ttu-id="b5692-149">Appel d’applications API déployées avec 2015-08-01-preview</span><span class="sxs-lookup"><span data-stu-id="b5692-149">Call deployed API apps with 2015-08-01-preview</span></span>

<span data-ttu-id="b5692-150">Si vous avez déployé une application API précédemment, vous pouvez appeler application hello avec hello **HTTP** action.</span><span class="sxs-lookup"><span data-stu-id="b5692-150">If you previously deployed an API App, you can call hello app with hello **HTTP** action.</span></span>

<span data-ttu-id="b5692-151">Par exemple, si vous utilisez des fichiers de toolist Dropbox, votre **2014-12-01-preview** définition de version de schéma peut avoir un nom tel que :</span><span class="sxs-lookup"><span data-stu-id="b5692-151">For example, if you use Dropbox toolist files, your **2014-12-01-preview** schema version definition might have something like:</span></span>

```
{
    "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2014-12-01-preview/workflowdefinition.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "/subscriptions/423db32d-...-b59f14c962f1/resourcegroups/avdemo/providers/Microsoft.AppService/apiapps/dropboxconnector/token": {
            "defaultValue": "eyJ0eX...wCn90",
            "type": "String",
            "metadata": {
                "token": {
                    "name": "/subscriptions/423db32d-...-b59f14c962f1/resourcegroups/avdemo/providers/Microsoft.AppService/apiapps/dropboxconnector/token"
                }
            }
        }
    },
    "actions": {
        "dropboxconnector": {
            "type": "ApiApp",
            "inputs": {
                "apiVersion": "2015-01-14",
                "host": {
                    "id": "/subscriptions/423db32d-...-b59f14c962f1/resourcegroups/avdemo/providers/Microsoft.AppService/apiapps/dropboxconnector",
                    "gateway": "https://avdemo.azurewebsites.net"
                },
                "operation": "ListFiles",
                "parameters": {
                    "FolderPath": "/myfolder"
                },
                "authentication": {
                    "type": "Raw",
                    "scheme": "Zumo",
                    "parameter": "@parameters('/subscriptions/423db32d-...-b59f14c962f1/resourcegroups/avdemo/providers/Microsoft.AppService/apiapps/dropboxconnector/token')"
                }
            }
        }
    }
}
```

<span data-ttu-id="b5692-152">Vous pouvez construire hello équivalent HTTP actions telles que cet exemple, lors de la section des paramètres de définition d’application logique de hello hello reste inchangée :</span><span class="sxs-lookup"><span data-stu-id="b5692-152">You can construct hello equivalent HTTP action like this example, while hello parameters section of hello Logic app definition remains unchanged:</span></span>

```
{
    "actions": {
        "dropboxconnector": {
            "type": "Http",
            "metadata": {
              "apiDefinitionUrl": "https://avdemo.azurewebsites.net/api/service/apidef/dropboxconnector/?api-version=2015-01-14&format=swagger-2.0-standard"  
            },
            "inputs": {
                "uri": "https://avdemo.azurewebsites.net/api/service/invoke/dropboxconnector/ListFiles?api-version=2015-01-14",
                "method": "POST",
                "body": {
                    "FolderPath": "/myfolder"
                },
                "authentication": {
                    "type": "Raw",
                    "scheme": "Zumo",
                    "parameter": "@parameters('/subscriptions/423db32d-...-b59f14c962f1/resourcegroups/avdemo/providers/Microsoft.AppService/apiapps/dropboxconnector/token')"
                }
            }
        }
    }
}
```

<span data-ttu-id="b5692-153">Présentation de ces propriétés une par une :</span><span class="sxs-lookup"><span data-stu-id="b5692-153">Walking through these properties one-by-one:</span></span>

| <span data-ttu-id="b5692-154">Propriété d’action</span><span class="sxs-lookup"><span data-stu-id="b5692-154">Action property</span></span> | <span data-ttu-id="b5692-155">Description</span><span class="sxs-lookup"><span data-stu-id="b5692-155">Description</span></span> |
| --- | --- |
| `type` |<span data-ttu-id="b5692-156">`Http` au lieu de `APIapp`</span><span class="sxs-lookup"><span data-stu-id="b5692-156">`Http` instead of `APIapp`</span></span> |
| `metadata.apiDefinitionUrl` |<span data-ttu-id="b5692-157">toouse cette action Bonjour Concepteur d’application logique, inclure des point de terminaison de métadonnées hello, qui est construit à partir de :`{api app host.gateway}/api/service/apidef/{last segment of hello api app host.id}/?api-version=2015-01-14&format=swagger-2.0-standard`</span><span class="sxs-lookup"><span data-stu-id="b5692-157">toouse this action in hello Logic App Designer, include hello metadata endpoint, which is constructed from: `{api app host.gateway}/api/service/apidef/{last segment of hello api app host.id}/?api-version=2015-01-14&format=swagger-2.0-standard`</span></span> |
| `inputs.uri` |<span data-ttu-id="b5692-158">Construit depuis : `{api app host.gateway}/api/service/invoke/{last segment of hello api app host.id}/{api app operation}?api-version=2015-01-14`</span><span class="sxs-lookup"><span data-stu-id="b5692-158">Constructed from: `{api app host.gateway}/api/service/invoke/{last segment of hello api app host.id}/{api app operation}?api-version=2015-01-14`</span></span> |
| `inputs.method` |<span data-ttu-id="b5692-159">Toujours `POST`</span><span class="sxs-lookup"><span data-stu-id="b5692-159">Always `POST`</span></span> |
| `inputs.body` |<span data-ttu-id="b5692-160">Paramètres de l’application API de toohello identiques</span><span class="sxs-lookup"><span data-stu-id="b5692-160">Identical toohello API App parameters</span></span> |
| `inputs.authentication` |<span data-ttu-id="b5692-161">Authentification de l’application API de toohello identiques</span><span class="sxs-lookup"><span data-stu-id="b5692-161">Identical toohello API App authentication</span></span> |

<span data-ttu-id="b5692-162">Cette approche doit fonctionner avec l’ensemble des actions d’application API.</span><span class="sxs-lookup"><span data-stu-id="b5692-162">This approach should work for all API App actions.</span></span> <span data-ttu-id="b5692-163">N’oubliez pas cependant que ces applications API antérieures ne sont plus prises en charge.</span><span class="sxs-lookup"><span data-stu-id="b5692-163">However, remember that these previous API Apps are no longer supported.</span></span> <span data-ttu-id="b5692-164">Par conséquent, vous devez déplacer tooone Hello deux autres options précédentes, une API managée ou héberger votre API Web personnalisée.</span><span class="sxs-lookup"><span data-stu-id="b5692-164">So you should move tooone of hello two other previous options, a managed API or hosting your custom Web API.</span></span>

<a name="foreach"></a>
## <a name="renamed-repeat-tooforeach"></a><span data-ttu-id="b5692-165">Renommé 'repeat' too'foreach'</span><span class="sxs-lookup"><span data-stu-id="b5692-165">Renamed 'repeat' too'foreach'</span></span>

<span data-ttu-id="b5692-166">Pour la version précédente du schéma hello, nous avons reçu de commentaires qui **répétez** était et n’a pas de capturer correctement qui **répétez** est vraiment une boucle pour chaque.</span><span class="sxs-lookup"><span data-stu-id="b5692-166">For hello previous schema version, we received much customer feedback that **Repeat** was confusing and didn't properly capture that **Repeat** was really a for-each loop.</span></span> <span data-ttu-id="b5692-167">Par conséquent, nous avons renommé `repeat` trop`foreach`.</span><span class="sxs-lookup"><span data-stu-id="b5692-167">As a result, we have renamed `repeat` too`foreach`.</span></span> <span data-ttu-id="b5692-168">Par exemple, précédemment, vous auriez écrit :</span><span class="sxs-lookup"><span data-stu-id="b5692-168">For example, previously you would write:</span></span>

```
{
    "actions": {
        "pingBing": {
            "type": "Http",
            "repeat": "@range(0,2)",
            "inputs": {
                "method": "GET",
                "uri": "https://www.bing.com/search?q=@{repeatItem()}"
            }
        }
    }
}
```

<span data-ttu-id="b5692-169">Maintenant, vous devez écrire :</span><span class="sxs-lookup"><span data-stu-id="b5692-169">Now you would write:</span></span>

```
{
    "actions": {
        "pingBing": {
            "type": "Http",
            "foreach": "@range(0,2)",
            "inputs": {
                "method": "GET",
                "uri": "https://www.bing.com/search?q=@{item()}"
            }
        }
    }
}
```

<span data-ttu-id="b5692-170">Hello fonction `@repeatItem()` a été élément actif de hello tooreference précédemment utilisés en cours d’itération.</span><span class="sxs-lookup"><span data-stu-id="b5692-170">hello function `@repeatItem()` was previously used tooreference hello current item being iterated over.</span></span> <span data-ttu-id="b5692-171">Cette fonction est simplifiée maintenant trop`@item()`.</span><span class="sxs-lookup"><span data-stu-id="b5692-171">This function is now simplified too`@item()`.</span></span> 

### <a name="reference-outputs-from-foreach"></a><span data-ttu-id="b5692-172">Référencement des sorties de 'foreach'</span><span class="sxs-lookup"><span data-stu-id="b5692-172">Reference outputs from 'foreach'</span></span>

<span data-ttu-id="b5692-173">Pour la simplification, hello sorties de `foreach` actions ne sont pas encapsulées dans un objet appelé `repeatItems`.</span><span class="sxs-lookup"><span data-stu-id="b5692-173">For simplification, hello outputs from `foreach` actions are not wrapped in an object called `repeatItems`.</span></span> <span data-ttu-id="b5692-174">Alors que hello sorties de hello précédente `repeat` exemple était :</span><span class="sxs-lookup"><span data-stu-id="b5692-174">While hello outputs from hello previous `repeat` example were:</span></span>

```
{
    "repeatItems": [
        {
            "name": "pingBing",
            "inputs": {
                "uri": "https://www.bing.com/search?q=0",
                "method": "GET"
            },
            "outputs": {
                "headers": { },
                "body": "<!DOCTYPE html><html lang=\"en\" xml:lang=\"en\" xmlns=\"http://www.w3.org/1999/xhtml\" xmlns:Web=\"http://schemas.live.com/Web/\">...</html>"
            }
            "status": "Succeeded"
        }
    ]
}
```

<span data-ttu-id="b5692-175">Les sorties sont maintenant :</span><span class="sxs-lookup"><span data-stu-id="b5692-175">Now these outputs are:</span></span>

```
[
    {
        "name": "pingBing",
        "inputs": {
            "uri": "https://www.bing.com/search?q=0",
            "method": "GET"
        },
        "outputs": {
            "headers": { },
            "body": "<!DOCTYPE html><html lang=\"en\" xml:lang=\"en\" xmlns=\"http://www.w3.org/1999/xhtml\" xmlns:Web=\"http://schemas.live.com/Web/\">...</html>"
        }
        "status": "Succeeded"
    }
]
```

<span data-ttu-id="b5692-176">Auparavant, tooget toohello corps de d’action hello lors du référencement de ces sorties :</span><span class="sxs-lookup"><span data-stu-id="b5692-176">Previously, tooget toohello body of hello action when referencing these outputs:</span></span>

```
{
    "actions": {
        "secondAction": {
            "type": "Http",
            "repeat": "@outputs('pingBing').repeatItems",
            "inputs": {
                "method": "POST",
                "uri": "http://www.example.com",
                "body": "@repeatItem().outputs.body"
            }
        }
    }
}
```

<span data-ttu-id="b5692-177">Désormais le code présente cette apparence :</span><span class="sxs-lookup"><span data-stu-id="b5692-177">Now you can do instead:</span></span>

```
{
    "actions": {
        "secondAction": {
            "type": "Http",
            "foreach": "@outputs('pingBing')",
            "inputs": {
                "method": "POST",
                "uri": "http://www.example.com",
                "body": "@item().outputs.body"
            }
        }
    }
}
```

<span data-ttu-id="b5692-178">Avec ces modifications, hello fonctions `@repeatItem()`, `@repeatBody()`, et `@repeatOutputs()` sont supprimés.</span><span class="sxs-lookup"><span data-stu-id="b5692-178">With these changes, hello functions `@repeatItem()`, `@repeatBody()`, and `@repeatOutputs()` are removed.</span></span>

<a name="http-listener"></a>
## <a name="native-http-listener"></a><span data-ttu-id="b5692-179">Écouteur HTTP natif</span><span class="sxs-lookup"><span data-stu-id="b5692-179">Native HTTP listener</span></span>

<span data-ttu-id="b5692-180">Hello fonctionnalités sont désormais intégrées dans l’écouteur HTTP.</span><span class="sxs-lookup"><span data-stu-id="b5692-180">hello HTTP Listener capabilities are now built in.</span></span> <span data-ttu-id="b5692-181">Par conséquent, vous n’avez plus besoin toodeploy une application API d’écouteur HTTP.</span><span class="sxs-lookup"><span data-stu-id="b5692-181">So you no longer need toodeploy an HTTP Listener API App.</span></span> <span data-ttu-id="b5692-182">Consultez [hello tous les détails de la procédure toomake votre ici peut être appelée du point de terminaison d’application logique](../logic-apps/logic-apps-http-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="b5692-182">See [hello full details for how toomake your Logic app endpoint callable here](../logic-apps/logic-apps-http-endpoint.md).</span></span> 

<span data-ttu-id="b5692-183">Avec ces modifications, nous avons supprimé hello `@accessKeys()` fonction, nous avons remplacé par hello `@listCallbackURL()` fonction pour l’obtention de point de terminaison hello lorsque cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="b5692-183">With these changes, we removed hello `@accessKeys()` function, which we replaced with hello `@listCallbackURL()` function for getting hello endpoint when necessary.</span></span> <span data-ttu-id="b5692-184">De plus, vous devez maintenant définir au moins un déclencheur dans votre application logique.</span><span class="sxs-lookup"><span data-stu-id="b5692-184">Also, you must now define at least one trigger in your logic app.</span></span> <span data-ttu-id="b5692-185">Si vous souhaitez trop`/run` hello du flux de travail, vous devez avoir une de ces déclencheurs : `manual`, `apiConnectionWebhook`, ou `httpWebhook`.</span><span class="sxs-lookup"><span data-stu-id="b5692-185">If you want too`/run` hello workflow, you must have one of these triggers: `manual`, `apiConnectionWebhook`, or `httpWebhook`.</span></span>

<a name="child-workflows"></a>
## <a name="call-child-workflows"></a><span data-ttu-id="b5692-186">Appel de flux de travail enfants</span><span class="sxs-lookup"><span data-stu-id="b5692-186">Call child workflows</span></span>

<span data-ttu-id="b5692-187">Auparavant, l’appel de flux de travail enfant requis va workflow toohello, obtention de jeton d’accès hello et collage de hello jeton dans la définition d’application hello logique où vous souhaitez toocall ce flux de travail enfant.</span><span class="sxs-lookup"><span data-stu-id="b5692-187">Previously, calling child workflows required going toohello workflow, getting hello access token, and pasting hello token in hello logic app definition where you want toocall that child workflow.</span></span> <span data-ttu-id="b5692-188">Avec le nouveau schéma de hello, hello Logic Apps moteur génère automatiquement une SAP lors de l’exécution pour hello workflow enfant afin de ne pas avoir trop coller les clés secrètes dans la définition de hello.</span><span class="sxs-lookup"><span data-stu-id="b5692-188">With hello new schema, hello Logic Apps engine automatically generates a SAS at runtime for hello child workflow so you don't have too paste any secrets into hello definition.</span></span> <span data-ttu-id="b5692-189">Voici un exemple :</span><span class="sxs-lookup"><span data-stu-id="b5692-189">Here is an example:</span></span>

```
"mynestedwf": {
    "type": "workflow",
    "inputs": {
        "host": {
            "id": "/subscriptions/xxxxyyyyzzz/resourceGroups/rg001/providers/Microsoft.Logic/mywf001",
            "triggerName": "myendpointtrigger"
        },
        "queries": {
            "extrafield": "specialValue"
        },
        "headers": {
            "x-ms-date": "@utcnow()",
            "Content-type": "application/json"
        },
        "body": {
            "contentFieldOne": "value100",
            "anotherField": 10.001
        }
    },
    "conditions": []
}
```

<span data-ttu-id="b5692-190">Une deuxième amélioration est que nous offrons enfant de hello demande entrante de flux de travail un accès complet toohello.</span><span class="sxs-lookup"><span data-stu-id="b5692-190">A second improvement is we are giving hello child workflows full access toohello incoming request.</span></span> <span data-ttu-id="b5692-191">Cela signifie que vous pouvez passer des paramètres dans hello *requêtes* section et Bonjour *en-têtes* objet et que vous pouvez définir entièrement hello corps entier.</span><span class="sxs-lookup"><span data-stu-id="b5692-191">That means that you can pass parameters in hello *queries* section and in hello *headers* object and that you can fully define hello entire body.</span></span>

<span data-ttu-id="b5692-192">Enfin, des flux de travail enfant de toohello les modifications requises.</span><span class="sxs-lookup"><span data-stu-id="b5692-192">Finally, there are required changes toohello child workflow.</span></span> <span data-ttu-id="b5692-193">Maintenant pendant que vous pourriez précédemment appeler un workflow enfant directement, vous devez définir un point de terminaison du déclencheur dans le flux de travail hello pour hello parent toocall.</span><span class="sxs-lookup"><span data-stu-id="b5692-193">While you could previously call a child workflow directly, now you must define a trigger endpoint in hello workflow for hello parent toocall.</span></span> <span data-ttu-id="b5692-194">En règle générale, vous devez ajouter un déclencheur a `manual` tapez, puis utiliser ce déclencheur dans la définition du parent hello.</span><span class="sxs-lookup"><span data-stu-id="b5692-194">Generally, you would add a trigger that has `manual` type, and then use that trigger in hello parent definition.</span></span> <span data-ttu-id="b5692-195">Hello de note `host` propriété prévoit spécifiquement une `triggerName` , car vous devez toujours spécifier dont le déclencheur vous appelez.</span><span class="sxs-lookup"><span data-stu-id="b5692-195">Note hello `host` property specifically has a `triggerName` because you must always specify which trigger you are invoking.</span></span>

## <a name="other-changes"></a><span data-ttu-id="b5692-196">Autres modifications</span><span class="sxs-lookup"><span data-stu-id="b5692-196">Other changes</span></span>

### <a name="new-queries-property"></a><span data-ttu-id="b5692-197">Nouvelle propriété « queries »</span><span class="sxs-lookup"><span data-stu-id="b5692-197">New 'queries' property</span></span>

<span data-ttu-id="b5692-198">Tous les types d’action prennent désormais en charge une nouvelle entrée appelée `queries`.</span><span class="sxs-lookup"><span data-stu-id="b5692-198">All action types now support a new input called `queries`.</span></span> <span data-ttu-id="b5692-199">Cette entrée peut être un objet structuré, plutôt que vous ayez chaîne hello de tooassemble manuellement.</span><span class="sxs-lookup"><span data-stu-id="b5692-199">This input can be a structured object, rather than you having tooassemble hello string by hand.</span></span>

### <a name="renamed-parse-function-toojson"></a><span data-ttu-id="b5692-200">Renommé « parse() » fonction too'json()'</span><span class="sxs-lookup"><span data-stu-id="b5692-200">Renamed 'parse()' function too'json()'</span></span>

<span data-ttu-id="b5692-201">Nous ajoutons davantage de contenu types bientôt, donc nous avons renommé hello `parse()` fonction trop`json()`.</span><span class="sxs-lookup"><span data-stu-id="b5692-201">We are adding more content types soon, so we renamed hello `parse()` function too`json()`.</span></span>

## <a name="coming-soon-enterprise-integration-apis"></a><span data-ttu-id="b5692-202">Bientôt disponibles : API d’intégration d’entreprise</span><span class="sxs-lookup"><span data-stu-id="b5692-202">Coming soon: Enterprise Integration APIs</span></span>

<span data-ttu-id="b5692-203">Nous n’avons pas versions managées encore de hello entreprise intégration API, comme AS2.</span><span class="sxs-lookup"><span data-stu-id="b5692-203">We don't have managed versions yet of hello Enterprise Integration APIs, like AS2.</span></span> <span data-ttu-id="b5692-204">Pendant ce temps, vous pouvez utiliser votre APIs BizTalk déployées existantes via hello action HTTP.</span><span class="sxs-lookup"><span data-stu-id="b5692-204">Meanwhile, you can use your existing deployed BizTalk APIs through hello HTTP action.</span></span> <span data-ttu-id="b5692-205">Pour plus d’informations, consultez « Utilisation de vos applications API déjà déployées « Bonjour [feuille de route pour l’intégration](http://www.zdnet.com/article/microsoft-outlines-its-cloud-and-server-integration-roadmap-for-2016/).</span><span class="sxs-lookup"><span data-stu-id="b5692-205">For details, see "Using your already deployed API apps" in hello [integration roadmap](http://www.zdnet.com/article/microsoft-outlines-its-cloud-and-server-integration-roadmap-for-2016/).</span></span> 
