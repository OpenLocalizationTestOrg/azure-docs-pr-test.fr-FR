---
title: "Mises à jour de schéma du 1er août 2015 (version préliminaire) - Azure Logic Apps | Microsoft Docs"
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
ms.openlocfilehash: 35d7a56d5607dcc18a4407c65b92962d3d0dcd1d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="schema-updates-for-azure-logic-apps---august-1-2015-preview"></a><span data-ttu-id="5ab32-103">Mises à jour de schéma pour Azure Logic Apps - Version préliminaire du 1er août 2015</span><span class="sxs-lookup"><span data-stu-id="5ab32-103">Schema updates for Azure Logic Apps - August 1, 2015 preview</span></span>

<span data-ttu-id="5ab32-104">Cette nouvelle version de schéma et d’API intègre différentes améliorations clés destinées à accroître la fiabilité et la simplicité d’utilisation des applications logiques :</span><span class="sxs-lookup"><span data-stu-id="5ab32-104">This new schema and API version for Azure Logic Apps includes key improvements that make logic apps more reliable and easier to use:</span></span>

*   <span data-ttu-id="5ab32-105">Le type d’action **APIApp** est remplacé par un nouveau type d’action [**APIConnection**](#api-connections).</span><span class="sxs-lookup"><span data-stu-id="5ab32-105">The **APIApp** action type is updated to a new [**APIConnection**](#api-connections) action type.</span></span>
*   <span data-ttu-id="5ab32-106">**Repeat** est renommée [**Foreach**](#foreach).</span><span class="sxs-lookup"><span data-stu-id="5ab32-106">**Repeat** is renamed to [**Foreach**](#foreach).</span></span>
*   <span data-ttu-id="5ab32-107">L’application API de [**l’Écouteur HTTP**](#http-listener)n’est plus requise.</span><span class="sxs-lookup"><span data-stu-id="5ab32-107">The [**HTTP Listener** API App](#http-listener) is no longer required.</span></span>
*   <span data-ttu-id="5ab32-108">L’appel des flux de travail enfants utilise un [nouveau schéma](#child-workflows).</span><span class="sxs-lookup"><span data-stu-id="5ab32-108">Calling child workflows uses a [new schema](#child-workflows).</span></span>

<a name="api-connections"></a>
## <a name="move-to-api-connections"></a><span data-ttu-id="5ab32-109">Déplacement vers les connexions d’API</span><span class="sxs-lookup"><span data-stu-id="5ab32-109">Move to API connections</span></span>

<span data-ttu-id="5ab32-110">La plus importante modification est que vous n’avez plus besoin de déployer des applications API dans votre abonnement Azure pour pouvoir utiliser des API.</span><span class="sxs-lookup"><span data-stu-id="5ab32-110">The biggest change is that you no longer have to deploy API Apps into your Azure subscription so you can use APIs.</span></span> <span data-ttu-id="5ab32-111">Voici les manières dont vous pouvez utiliser les API :</span><span class="sxs-lookup"><span data-stu-id="5ab32-111">Here are the ways that you can use APIs:</span></span>

* <span data-ttu-id="5ab32-112">API gérées</span><span class="sxs-lookup"><span data-stu-id="5ab32-112">Managed APIs</span></span>
* <span data-ttu-id="5ab32-113">Vos API web personnalisées</span><span class="sxs-lookup"><span data-stu-id="5ab32-113">Your custom Web APIs</span></span>

<span data-ttu-id="5ab32-114">Chacune de ces méthodes fait l’objet d’un traitement légèrement différent, car leurs modèles de gestion et d’hébergement sont différents.</span><span class="sxs-lookup"><span data-stu-id="5ab32-114">Each way is handled slightly differently because their management and hosting models are different.</span></span> <span data-ttu-id="5ab32-115">Avec ce modèle, vous n’êtes plus limité aux ressources déployées dans votre groupe de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="5ab32-115">One advantage of this model is you're no longer constrained to resources that are deployed in your Azure resource group.</span></span> 

### <a name="managed-apis"></a><span data-ttu-id="5ab32-116">API gérées</span><span class="sxs-lookup"><span data-stu-id="5ab32-116">Managed APIs</span></span>

<span data-ttu-id="5ab32-117">Microsoft gère certaines API à votre place, comme Office 365, Salesforce, Twitter et FTP.</span><span class="sxs-lookup"><span data-stu-id="5ab32-117">Microsoft manages some APIs on your behalf, such as Office 365, Salesforce, Twitter, and FTP.</span></span> <span data-ttu-id="5ab32-118">Vous pouvez utiliser des API gérées (par exemple, Bing Translate), tandis que d’autres nécessitent une configuration.</span><span class="sxs-lookup"><span data-stu-id="5ab32-118">You can use some managed APIs as-is, such as Bing Translate, while others require configuration.</span></span> <span data-ttu-id="5ab32-119">Cette configuration est appelée une *connexion*.</span><span class="sxs-lookup"><span data-stu-id="5ab32-119">This configuration is called a *connection*.</span></span>

<span data-ttu-id="5ab32-120">Par exemple, lorsque vous utilisez Office 365, vous devez créer une connexion qui contient votre jeton de connexion Office 365.</span><span class="sxs-lookup"><span data-stu-id="5ab32-120">For example, when you use Office 365, you must create a connection that contains your Office 365 sign-in token.</span></span> <span data-ttu-id="5ab32-121">Ce jeton est stocké et actualisé de manière sécurisée, afin que votre application logique puisse toujours appeler l’API Office 365.</span><span class="sxs-lookup"><span data-stu-id="5ab32-121">This token is securely stored and refreshed so that your logic app can always call the Office 365 API.</span></span> <span data-ttu-id="5ab32-122">Sinon, si vous souhaitez vous connecter à votre serveur SQL ou FTP, il vous faut créer une connexion présentant la chaîne connection.</span><span class="sxs-lookup"><span data-stu-id="5ab32-122">Alternatively, if you want to connect to your SQL or FTP server, you must create a connection that has the connection string.</span></span> 

<span data-ttu-id="5ab32-123">Dans la définition, ces actions sont appelées `APIConnection`.</span><span class="sxs-lookup"><span data-stu-id="5ab32-123">In this definition, these actions are called `APIConnection`.</span></span> <span data-ttu-id="5ab32-124">Voici un exemple de connexion appelant l’API Office 365 pour envoyer un courrier électronique :</span><span class="sxs-lookup"><span data-stu-id="5ab32-124">Here is an example of a connection that calls Office 365 to send an email:</span></span>

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

<span data-ttu-id="5ab32-125">L’objet `host` est la portion des entrées spécifique aux connexions d’API et contient deux parties : `api` et `connection`.</span><span class="sxs-lookup"><span data-stu-id="5ab32-125">The `host` object is portion of inputs that is unique to API connections, and contains tow parts: `api` and `connection`.</span></span>

<span data-ttu-id="5ab32-126">L’ `api` présente l’URL d’exécution de l’emplacement d’hébergement de cette API gérée.</span><span class="sxs-lookup"><span data-stu-id="5ab32-126">The `api` has the runtime URL of where that managed API is hosted.</span></span> <span data-ttu-id="5ab32-127">Vous pouvez voir l’ensemble des API gérées disponibles en appelant `GET https://management.azure.com/subscriptions/{subid}/providers/Microsoft.Web/managedApis/?api-version=2015-08-01-preview`.</span><span class="sxs-lookup"><span data-stu-id="5ab32-127">You can see all the available managed APIs by calling `GET https://management.azure.com/subscriptions/{subid}/providers/Microsoft.Web/managedApis/?api-version=2015-08-01-preview`.</span></span>

<span data-ttu-id="5ab32-128">Lorsque vous utilisez une, elle peut présenter ou non des *paramètres de connexion* définis.</span><span class="sxs-lookup"><span data-stu-id="5ab32-128">When you use an API, the API might or might not have any *connection parameters* defined.</span></span> <span data-ttu-id="5ab32-129">Si l’API n’en possède pas, aucune *connexion* n’est requise.</span><span class="sxs-lookup"><span data-stu-id="5ab32-129">If the API doesn't, no *connection* is required.</span></span> <span data-ttu-id="5ab32-130">Si l’API en possède, il vous faudra créer une connexion.</span><span class="sxs-lookup"><span data-stu-id="5ab32-130">If the API does, you must create a connection.</span></span> <span data-ttu-id="5ab32-131">La connexion créée porte le nom de votre choix.</span><span class="sxs-lookup"><span data-stu-id="5ab32-131">The created connection has the name that you choose.</span></span> <span data-ttu-id="5ab32-132">Vous référencez ensuite le nom de l’objet `connection` à l’intérieur de l’objet `host`.</span><span class="sxs-lookup"><span data-stu-id="5ab32-132">You then reference the name in the `connection` object inside the `host` object.</span></span> <span data-ttu-id="5ab32-133">Pour créer une connexion dans un groupe de ressources, appelez :</span><span class="sxs-lookup"><span data-stu-id="5ab32-133">To create a connection in a resource group, call:</span></span>

```
PUT https://management.azure.com/subscriptions/{subid}/resourceGroups/{rgname}/providers/Microsoft.Web/connections/{name}?api-version=2015-08-01-preview
```

<span data-ttu-id="5ab32-134">Avec le corps suivant :</span><span class="sxs-lookup"><span data-stu-id="5ab32-134">With the following body:</span></span>

```
{
  "properties": {
    "api": {
      "id": "/subscriptions/{subid}/providers/Microsoft.Web/managedApis/azureblob"
    },
    "parameterValues": {
        "accountName": "{The name of the storage account -- the set of parameters is different for each API}"
    }
  },
  "location": "{Logic app's location}"
}
```

### <a name="deploy-managed-apis-in-an-azure-resource-manager-template"></a><span data-ttu-id="5ab32-135">Déploiement d’API gérées dans un modèle Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="5ab32-135">Deploy managed APIs in an Azure Resource Manager template</span></span>

<span data-ttu-id="5ab32-136">Vous pouvez créer une application complète dans un modèle Azure Resource Manager, tant qu’elle ne nécessite aucune connexion interactive.</span><span class="sxs-lookup"><span data-stu-id="5ab32-136">You can create a full application in an Azure Resource Manager template as long as interactive sign-in isn't required.</span></span>
<span data-ttu-id="5ab32-137">Si une connexion est requise, vous pouvez procéder à la configuration avec le modèle Azure Resource Manager, mais devrez néanmoins accéder au portail afin d’autoriser les connexions.</span><span class="sxs-lookup"><span data-stu-id="5ab32-137">If sign-in is required, you can set up everything with the Azure Resource Manager template, but you still have to visit the portal to authorize the connections.</span></span> 

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

<span data-ttu-id="5ab32-138">Vous pouvez constater dans cet exemple que les connexions sont des ressources hébergées dans votre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="5ab32-138">You can see in this example that the connections are just resources that live in your resource group.</span></span> <span data-ttu-id="5ab32-139">Elles référencent les API gérées disponibles dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="5ab32-139">They reference the managed APIs available to you in your subscription.</span></span>

### <a name="your-custom-web-apis"></a><span data-ttu-id="5ab32-140">Vos API web personnalisées</span><span class="sxs-lookup"><span data-stu-id="5ab32-140">Your custom Web APIs</span></span>

<span data-ttu-id="5ab32-141">Si vous utilisez vos propres API (non gérées par Microsoft), utilisez l’action **HTTP** intégrée pour les appeler.</span><span class="sxs-lookup"><span data-stu-id="5ab32-141">If you use your own APIs, not Microsoft-managed ones, use the built-in **HTTP** action to call them.</span></span> <span data-ttu-id="5ab32-142">Pour une expérience optimale, vous avez tout intérêt à exposer un point de terminaison swagger pour votre API.</span><span class="sxs-lookup"><span data-stu-id="5ab32-142">For an ideal experience, you should expose a Swagger endpoint for your API.</span></span> <span data-ttu-id="5ab32-143">Ce point de terminaison permet au concepteur d’application logique de réaliser le rendu des entrées et des sorties pour votre API.</span><span class="sxs-lookup"><span data-stu-id="5ab32-143">This endpoint enables the Logic App Designer to render the inputs and outputs for your API.</span></span> <span data-ttu-id="5ab32-144">Sans point de terminaison swagger, le concepteur peut simplement représenter les entrées et les sorties en tant qu’objets JSON opaques.</span><span class="sxs-lookup"><span data-stu-id="5ab32-144">Without Swagger, the designer can only show the inputs and outputs as opaque JSON objects.</span></span>

<span data-ttu-id="5ab32-145">Voici un exemple illustrant la nouvelle propriété `metadata.apiDefinitionUrl` :</span><span class="sxs-lookup"><span data-stu-id="5ab32-145">Here is an example showing the new `metadata.apiDefinitionUrl` property:</span></span>

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

<span data-ttu-id="5ab32-146">Si vous hébergez votre API web sur Azure App Service, votre API web s’affiche automatiquement dans la liste des actions disponibles dans le concepteur.</span><span class="sxs-lookup"><span data-stu-id="5ab32-146">If you host your Web API on Azure App Service, your Web API automatically appears in the list of actions available in the designer.</span></span> <span data-ttu-id="5ab32-147">Si ce n’est pas le cas, vous devrez coller le contenu directement dans l’URL.</span><span class="sxs-lookup"><span data-stu-id="5ab32-147">If not, you have to paste in the URL directly.</span></span> <span data-ttu-id="5ab32-148">Le point de terminaison Swagger doit être non authentifié pour être utilisé dans le concepteur des applications logiques ; vous pouvez cependant sécuriser l’API à l’aide des méthodes prises en charge dans Swagger.</span><span class="sxs-lookup"><span data-stu-id="5ab32-148">The Swagger endpoint must be unauthenticated to be usable in the Logic App Designer, although you can secure the API itself with whatever methods that Swagger supports.</span></span>

### <a name="call-deployed-api-apps-with-2015-08-01-preview"></a><span data-ttu-id="5ab32-149">Appel d’applications API déployées avec 2015-08-01-preview</span><span class="sxs-lookup"><span data-stu-id="5ab32-149">Call deployed API apps with 2015-08-01-preview</span></span>

<span data-ttu-id="5ab32-150">Si vous avez déjà déployé une application API, vous pouvez l’appeler à l’aide de l’action **HTTP**.</span><span class="sxs-lookup"><span data-stu-id="5ab32-150">If you previously deployed an API App, you can call the app with the **HTTP** action.</span></span>

<span data-ttu-id="5ab32-151">Par exemple, si vous utilisez Dropbox pour répertorier les fichiers, vous pouvez disposer du contenu suivant dans votre définition de version de schéma **2014-12-01-preview** :</span><span class="sxs-lookup"><span data-stu-id="5ab32-151">For example, if you use Dropbox to list files, your **2014-12-01-preview** schema version definition might have something like:</span></span>

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

<span data-ttu-id="5ab32-152">Vous pouvez générer l’action HTTP équivalente comme dans cet exemple (la section des paramètres de la définition de l’application demeure inchangée) :</span><span class="sxs-lookup"><span data-stu-id="5ab32-152">You can construct the equivalent HTTP action like this example, while the parameters section of the Logic app definition remains unchanged:</span></span>

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

<span data-ttu-id="5ab32-153">Présentation de ces propriétés une par une :</span><span class="sxs-lookup"><span data-stu-id="5ab32-153">Walking through these properties one-by-one:</span></span>

| <span data-ttu-id="5ab32-154">Propriété d’action</span><span class="sxs-lookup"><span data-stu-id="5ab32-154">Action property</span></span> | <span data-ttu-id="5ab32-155">Description</span><span class="sxs-lookup"><span data-stu-id="5ab32-155">Description</span></span> |
| --- | --- |
| `type` |<span data-ttu-id="5ab32-156">`Http` au lieu de `APIapp`</span><span class="sxs-lookup"><span data-stu-id="5ab32-156">`Http` instead of `APIapp`</span></span> |
| `metadata.apiDefinitionUrl` |<span data-ttu-id="5ab32-157">Pour utiliser cette action dans le concepteur d’applications logiques, vous devez inclure le point de terminaison des métadonnées, créé depuis : `{api app host.gateway}/api/service/apidef/{last segment of the api app host.id}/?api-version=2015-01-14&format=swagger-2.0-standard`</span><span class="sxs-lookup"><span data-stu-id="5ab32-157">To use this action in the Logic App Designer, include the metadata endpoint, which is constructed from: `{api app host.gateway}/api/service/apidef/{last segment of the api app host.id}/?api-version=2015-01-14&format=swagger-2.0-standard`</span></span> |
| `inputs.uri` |<span data-ttu-id="5ab32-158">Construit depuis : `{api app host.gateway}/api/service/invoke/{last segment of the api app host.id}/{api app operation}?api-version=2015-01-14`</span><span class="sxs-lookup"><span data-stu-id="5ab32-158">Constructed from: `{api app host.gateway}/api/service/invoke/{last segment of the api app host.id}/{api app operation}?api-version=2015-01-14`</span></span> |
| `inputs.method` |<span data-ttu-id="5ab32-159">Toujours `POST`</span><span class="sxs-lookup"><span data-stu-id="5ab32-159">Always `POST`</span></span> |
| `inputs.body` |<span data-ttu-id="5ab32-160">Identique aux paramètres de l’application API</span><span class="sxs-lookup"><span data-stu-id="5ab32-160">Identical to the API App parameters</span></span> |
| `inputs.authentication` |<span data-ttu-id="5ab32-161">Identique à l’authentification de l’application API</span><span class="sxs-lookup"><span data-stu-id="5ab32-161">Identical to the API App authentication</span></span> |

<span data-ttu-id="5ab32-162">Cette approche doit fonctionner avec l’ensemble des actions d’application API.</span><span class="sxs-lookup"><span data-stu-id="5ab32-162">This approach should work for all API App actions.</span></span> <span data-ttu-id="5ab32-163">N’oubliez pas cependant que ces applications API antérieures ne sont plus prises en charge.</span><span class="sxs-lookup"><span data-stu-id="5ab32-163">However, remember that these previous API Apps are no longer supported.</span></span> <span data-ttu-id="5ab32-164">Vous devez donc opter pour l’une des deux autres options précédentes, à savoir une API gérée ou l’hébergement de votre API web personnalisée.</span><span class="sxs-lookup"><span data-stu-id="5ab32-164">So you should move to one of the two other previous options, a managed API or hosting your custom Web API.</span></span>

<a name="foreach"></a>
## <a name="renamed-repeat-to-foreach"></a><span data-ttu-id="5ab32-165">« Repeat » renommée en « Foreach »</span><span class="sxs-lookup"><span data-stu-id="5ab32-165">Renamed 'repeat' to 'foreach'</span></span>

<span data-ttu-id="5ab32-166">Les clients ayant utilisé la version de schéma précédente se sont beaucoup plaints du caractère déroutant de **Repeat** et n’ont pas vraiment compris que **Repeat** était réellement une boucle foreach.</span><span class="sxs-lookup"><span data-stu-id="5ab32-166">For the previous schema version, we received much customer feedback that **Repeat** was confusing and didn't properly capture that **Repeat** was really a for-each loop.</span></span> <span data-ttu-id="5ab32-167">Par conséquent, nous avons renommé `repeat` en `foreach`.</span><span class="sxs-lookup"><span data-stu-id="5ab32-167">As a result, we have renamed `repeat` to `foreach`.</span></span> <span data-ttu-id="5ab32-168">Par exemple, précédemment, vous auriez écrit :</span><span class="sxs-lookup"><span data-stu-id="5ab32-168">For example, previously you would write:</span></span>

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

<span data-ttu-id="5ab32-169">Maintenant, vous devez écrire :</span><span class="sxs-lookup"><span data-stu-id="5ab32-169">Now you would write:</span></span>

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

<span data-ttu-id="5ab32-170">Auparavant, la fonction `@repeatItem()` était utilisée pour référencer l’élément sur lequel était actuellement exécutée une itération.</span><span class="sxs-lookup"><span data-stu-id="5ab32-170">The function `@repeatItem()` was previously used to reference the current item being iterated over.</span></span> <span data-ttu-id="5ab32-171">Cette fonction est désormais simplifiée en `@item()`.</span><span class="sxs-lookup"><span data-stu-id="5ab32-171">This function is now simplified to `@item()`.</span></span> 

### <a name="reference-outputs-from-foreach"></a><span data-ttu-id="5ab32-172">Référencement des sorties de 'foreach'</span><span class="sxs-lookup"><span data-stu-id="5ab32-172">Reference outputs from 'foreach'</span></span>

<span data-ttu-id="5ab32-173">Dans un souci de simplification, les sorties des actions `foreach` ne sont pas encapsulées dans un objet appelé `repeatItems`.</span><span class="sxs-lookup"><span data-stu-id="5ab32-173">For simplification, the outputs from `foreach` actions are not wrapped in an object called `repeatItems`.</span></span> <span data-ttu-id="5ab32-174">Tandis que les sorties de l’exemple `repeat` précédent étaient :</span><span class="sxs-lookup"><span data-stu-id="5ab32-174">While the outputs from the previous `repeat` example were:</span></span>

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

<span data-ttu-id="5ab32-175">Les sorties sont maintenant :</span><span class="sxs-lookup"><span data-stu-id="5ab32-175">Now these outputs are:</span></span>

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

<span data-ttu-id="5ab32-176">Lorsque vous référenciez ces sorties, pour atteindre le corps de l’action vous deviez auparavant procéder ainsi :</span><span class="sxs-lookup"><span data-stu-id="5ab32-176">Previously, to get to the body of the action when referencing these outputs:</span></span>

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

<span data-ttu-id="5ab32-177">Désormais le code présente cette apparence :</span><span class="sxs-lookup"><span data-stu-id="5ab32-177">Now you can do instead:</span></span>

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

<span data-ttu-id="5ab32-178">Ces modifications entraînent la disparition des fonctions `@repeatItem()`, `@repeatBody()` et `@repeatOutputs()`.</span><span class="sxs-lookup"><span data-stu-id="5ab32-178">With these changes, the functions `@repeatItem()`, `@repeatBody()`, and `@repeatOutputs()` are removed.</span></span>

<a name="http-listener"></a>
## <a name="native-http-listener"></a><span data-ttu-id="5ab32-179">Écouteur HTTP natif</span><span class="sxs-lookup"><span data-stu-id="5ab32-179">Native HTTP listener</span></span>

<span data-ttu-id="5ab32-180">Les fonctionnalités de l’écouteur HTTP sont désormais intégrées.</span><span class="sxs-lookup"><span data-stu-id="5ab32-180">The HTTP Listener capabilities are now built in.</span></span> <span data-ttu-id="5ab32-181">Par conséquent, vous n’avez plus besoin de déployer une application API d’écouteur HTTP.</span><span class="sxs-lookup"><span data-stu-id="5ab32-181">So you no longer need to deploy an HTTP Listener API App.</span></span> <span data-ttu-id="5ab32-182">Consultez [ici une explication détaillée de la configuration d’un point de terminaison d’application logique pouvant être appelé](../logic-apps/logic-apps-http-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="5ab32-182">See [the full details for how to make your Logic app endpoint callable here](../logic-apps/logic-apps-http-endpoint.md).</span></span> 

<span data-ttu-id="5ab32-183">Avec ces modifications, nous avons supprimé la fonction `@accessKeys()` et l’avons remplacée par la fonction `@listCallbackURL()` dédiée à la récupération du point de terminaison, si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="5ab32-183">With these changes, we removed the `@accessKeys()` function, which we replaced with the `@listCallbackURL()` function for getting the endpoint when necessary.</span></span> <span data-ttu-id="5ab32-184">De plus, vous devez maintenant définir au moins un déclencheur dans votre application logique.</span><span class="sxs-lookup"><span data-stu-id="5ab32-184">Also, you must now define at least one trigger in your logic app.</span></span> <span data-ttu-id="5ab32-185">Si vous souhaitez appliquer l’action `/run` au flux de travail, vous devez disposer d’un de ces déclencheurs : `manual`, `apiConnectionWebhook` ou `httpWebhook`.</span><span class="sxs-lookup"><span data-stu-id="5ab32-185">If you want to `/run` the workflow, you must have one of these triggers: `manual`, `apiConnectionWebhook`, or `httpWebhook`.</span></span>

<a name="child-workflows"></a>
## <a name="call-child-workflows"></a><span data-ttu-id="5ab32-186">Appel de flux de travail enfants</span><span class="sxs-lookup"><span data-stu-id="5ab32-186">Call child workflows</span></span>

<span data-ttu-id="5ab32-187">Auparavant, quiconque souhaitait appeler des flux de travail enfants devait y accéder, récupérer le jeton d’accès, puis coller ce dernier dans la définition de l’application logique destinée à effectuer l’appel.</span><span class="sxs-lookup"><span data-stu-id="5ab32-187">Previously, calling child workflows required going to the workflow, getting the access token, and pasting the token in the logic app definition where you want to call that child workflow.</span></span> <span data-ttu-id="5ab32-188">Avec le nouveau schéma, le moteur Logic Apps génère automatiquement une SAP lors de l’exécution pour le flux de travail enfant, ce qui évite d’avoir à coller une clé secrète dans la définition.</span><span class="sxs-lookup"><span data-stu-id="5ab32-188">With the new schema, the Logic Apps engine automatically generates a SAS at runtime for the child workflow so you don't have to paste any secrets into the definition.</span></span> <span data-ttu-id="5ab32-189">Voici un exemple :</span><span class="sxs-lookup"><span data-stu-id="5ab32-189">Here is an example:</span></span>

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

<span data-ttu-id="5ab32-190">Autre amélioration, nous octroyons aux flux de travail enfants un accès complet à la requête entrante.</span><span class="sxs-lookup"><span data-stu-id="5ab32-190">A second improvement is we are giving the child workflows full access to the incoming request.</span></span> <span data-ttu-id="5ab32-191">Cela signifie que vous pouvez transmettre les paramètres dans la section *queries* et dans l’objet *headers*, et que vous pouvez définir intégralement le corps.</span><span class="sxs-lookup"><span data-stu-id="5ab32-191">That means that you can pass parameters in the *queries* section and in the *headers* object and that you can fully define the entire body.</span></span>

<span data-ttu-id="5ab32-192">Enfin, des modifications doivent être apportées au flux de travail enfant.</span><span class="sxs-lookup"><span data-stu-id="5ab32-192">Finally, there are required changes to the child workflow.</span></span> <span data-ttu-id="5ab32-193">Auparavant, vous pouviez appeler directement un flux de travail enfant. Désormais, il vous faut définir un point de terminaison déclencheur dans le flux de travail pour prendre en charge l’appel du parent.</span><span class="sxs-lookup"><span data-stu-id="5ab32-193">While you could previously call a child workflow directly, now you must define a trigger endpoint in the workflow for the parent to call.</span></span> <span data-ttu-id="5ab32-194">Généralement, vous devrez ajouter un déclencheur de type `manual`, que vous utiliserez dans la définition du parent.</span><span class="sxs-lookup"><span data-stu-id="5ab32-194">Generally, you would add a trigger that has `manual` type, and then use that trigger in the parent definition.</span></span> <span data-ttu-id="5ab32-195">Notez que la propriété `host` dispose d’un élément `triggerName`, dans la mesure où vous devez toujours spécifier le déclencheur invoqué.</span><span class="sxs-lookup"><span data-stu-id="5ab32-195">Note the `host` property specifically has a `triggerName` because you must always specify which trigger you are invoking.</span></span>

## <a name="other-changes"></a><span data-ttu-id="5ab32-196">Autres modifications</span><span class="sxs-lookup"><span data-stu-id="5ab32-196">Other changes</span></span>

### <a name="new-queries-property"></a><span data-ttu-id="5ab32-197">Nouvelle propriété « queries »</span><span class="sxs-lookup"><span data-stu-id="5ab32-197">New 'queries' property</span></span>

<span data-ttu-id="5ab32-198">Tous les types d’action prennent désormais en charge une nouvelle entrée appelée `queries`.</span><span class="sxs-lookup"><span data-stu-id="5ab32-198">All action types now support a new input called `queries`.</span></span> <span data-ttu-id="5ab32-199">Cette entrée peut être un objet structuré, qui ne nécessite aucun assemblage manuel de chaîne.</span><span class="sxs-lookup"><span data-stu-id="5ab32-199">This input can be a structured object, rather than you having to assemble the string by hand.</span></span>

### <a name="renamed-parse-function-to-json"></a><span data-ttu-id="5ab32-200">Fonction 'parse()' renommée 'json()'</span><span class="sxs-lookup"><span data-stu-id="5ab32-200">Renamed 'parse()' function to 'json()'</span></span>

<span data-ttu-id="5ab32-201">Nous procédons actuellement à l’ajout d’autres types de contenu, c’est pourquoi nous avons renommé la fonction `parse()` en `json()`.</span><span class="sxs-lookup"><span data-stu-id="5ab32-201">We are adding more content types soon, so we renamed the `parse()` function to `json()`.</span></span>

## <a name="coming-soon-enterprise-integration-apis"></a><span data-ttu-id="5ab32-202">Bientôt disponibles : API d’intégration d’entreprise</span><span class="sxs-lookup"><span data-stu-id="5ab32-202">Coming soon: Enterprise Integration APIs</span></span>

<span data-ttu-id="5ab32-203">Nous ne disposons pas actuellement de versions gérées des API d’intégration d’entreprise, du type AS2.</span><span class="sxs-lookup"><span data-stu-id="5ab32-203">We don't have managed versions yet of the Enterprise Integration APIs, like AS2.</span></span> <span data-ttu-id="5ab32-204">En attendant, vous pouvez utiliser vos API BizTalk existantes via l’action HTTP.</span><span class="sxs-lookup"><span data-stu-id="5ab32-204">Meanwhile, you can use your existing deployed BizTalk APIs through the HTTP action.</span></span> <span data-ttu-id="5ab32-205">Pour plus d’informations, consultez la rubrique dédiée à l’utilisation de vos applications API déjà déployées dans le [calendrier d’intégration](http://www.zdnet.com/article/microsoft-outlines-its-cloud-and-server-integration-roadmap-for-2016/).</span><span class="sxs-lookup"><span data-stu-id="5ab32-205">For details, see "Using your already deployed API apps" in the [integration roadmap](http://www.zdnet.com/article/microsoft-outlines-its-cloud-and-server-integration-roadmap-for-2016/).</span></span> 
