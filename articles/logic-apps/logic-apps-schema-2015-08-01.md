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
# <a name="schema-updates-for-azure-logic-apps---august-1-2015-preview"></a>Mises à jour de schéma pour Azure Logic Apps - Version préliminaire du 1er août 2015

Ce schéma et une API version pour Azure Logic Apps inclut des améliorations clés qui rendent les applications logique plus fiable et plus facile de toouse :

*   Hello **APIApp** type d’action est mis à jour tooa nouvelle [ **APIConnection** ](#api-connections) type d’action.
*   **Répétez les** est renommé trop[**Foreach**](#foreach).
*   Hello [ **écouteur HTTP** application API](#http-listener) n’est plus nécessaire.
*   L’appel des flux de travail enfants utilise un [nouveau schéma](#child-workflows).

<a name="api-connections"></a>
## <a name="move-tooapi-connections"></a>Déplacer les connexions tooAPI

modification de plus grande Hello est que vous n’avez plus toodeploy API Apps dans votre abonnement Azure afin de pouvoir utiliser les API. Voici quelques conseils hello que vous pouvez utiliser les API :

* API gérées
* Vos API web personnalisées

Chacune de ces méthodes fait l’objet d’un traitement légèrement différent, car leurs modèles de gestion et d’hébergement sont différents. Un avantage de ce modèle est que vous êtes limité n’est plus tooresources qui sont déployés dans votre groupe de ressources Azure. 

### <a name="managed-apis"></a>API gérées

Microsoft gère certaines API à votre place, comme Office 365, Salesforce, Twitter et FTP. Vous pouvez utiliser des API gérées (par exemple, Bing Translate), tandis que d’autres nécessitent une configuration. Cette configuration est appelée une *connexion*.

Par exemple, lorsque vous utilisez Office 365, vous devez créer une connexion qui contient votre jeton de connexion Office 365. Ce jeton est en toute sécurité enregistrée et actualisé, afin que votre application logique peut appeler toujours hello API Office 365. Vous pouvez également, si vous souhaitez que le serveur SQL ou FTP du tooyour tooconnect, vous devez créer une connexion avec la chaîne de connexion hello. 

Dans la définition, ces actions sont appelées `APIConnection`. Voici un exemple d’une connexion qui appelle toosend d’Office 365 à un message électronique :

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

Hello `host` objet est la partie d’entrées uniques tooAPI connexions, et contient des pièces de câbles : `api` et `connection`.

Hello `api` a runtime hello URL d’où qui API managée est hébergé. Vous pouvez voir tous les hello disponibles d’API gérées en appelant `GET https://management.azure.com/subscriptions/{subid}/providers/Microsoft.Web/managedApis/?api-version=2015-08-01-preview`.

Lorsque vous utilisez une API, hello API peut ou ne peut pas avoir un *les paramètres de connexion* défini. Si hello API n’est pas, aucune *connexion* est requis. En cas de hello API, vous devez créer une connexion. connexion de Hello créé a nom hello que vous choisissez. Vous ensuite référencez nom hello Bonjour `connection` objet à l’intérieur de hello `host` objet. une connexion dans un groupe de ressources, appel de toocreate :

```
PUT https://management.azure.com/subscriptions/{subid}/resourceGroups/{rgname}/providers/Microsoft.Web/connections/{name}?api-version=2015-08-01-preview
```

Avec hello suivant corps :

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

### <a name="deploy-managed-apis-in-an-azure-resource-manager-template"></a>Déploiement d’API gérées dans un modèle Azure Resource Manager

Vous pouvez créer une application complète dans un modèle Azure Resource Manager, tant qu’elle ne nécessite aucune connexion interactive.
Si la connexion est nécessaire, vous pouvez configurer tous les éléments avec le modèle de gestionnaire de ressources Azure hello, mais vous que les connexions de hello toovisit hello tooauthorize portail. 

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

Vous pouvez le voir dans cet exemple, les connexions hello sont simplement aux ressources qui se trouvent dans votre groupe de ressources. Elles font référence à hello géré API disponible tooyou dans votre abonnement.

### <a name="your-custom-web-apis"></a>Vos API web personnalisées

Si vous utilisez votre propre API, ceux qui sont pas gérés par Microsoft, utiliser intégrée de hello **HTTP** action toocall les. Pour une expérience optimale, vous avez tout intérêt à exposer un point de terminaison swagger pour votre API. Ce point de terminaison permet d’entrées de hello toorender hello Concepteur de logique d’application et fournit en sortie de votre API. Sans Swagger, Concepteur de hello peut uniquement afficher hello entrées et sorties en tant qu’objets JSON opaques.

Voici un hello d’affichage exemple nouvelle `metadata.apiDefinitionUrl` propriété :

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

Si vous hébergez votre API Web sur Azure App Service, votre API Web s’affiche automatiquement dans la liste hello des actions disponibles dans le Concepteur de hello. Si ce n’est pas le cas, vous avez toopaste dans l’URL de hello directement. point de terminaison Swagger Hello doit être non authentifiée toobe utilisable dans hello Concepteur de logique d’application, bien que vous pouvez sécuriser les API de hello elle-même avec toutes les méthodes qui prend en charge de Swagger.

### <a name="call-deployed-api-apps-with-2015-08-01-preview"></a>Appel d’applications API déployées avec 2015-08-01-preview

Si vous avez déployé une application API précédemment, vous pouvez appeler application hello avec hello **HTTP** action.

Par exemple, si vous utilisez des fichiers de toolist Dropbox, votre **2014-12-01-preview** définition de version de schéma peut avoir un nom tel que :

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

Vous pouvez construire hello équivalent HTTP actions telles que cet exemple, lors de la section des paramètres de définition d’application logique de hello hello reste inchangée :

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

Présentation de ces propriétés une par une :

| Propriété d’action | Description |
| --- | --- |
| `type` |`Http` au lieu de `APIapp` |
| `metadata.apiDefinitionUrl` |toouse cette action Bonjour Concepteur d’application logique, inclure des point de terminaison de métadonnées hello, qui est construit à partir de :`{api app host.gateway}/api/service/apidef/{last segment of hello api app host.id}/?api-version=2015-01-14&format=swagger-2.0-standard` |
| `inputs.uri` |Construit depuis : `{api app host.gateway}/api/service/invoke/{last segment of hello api app host.id}/{api app operation}?api-version=2015-01-14` |
| `inputs.method` |Toujours `POST` |
| `inputs.body` |Paramètres de l’application API de toohello identiques |
| `inputs.authentication` |Authentification de l’application API de toohello identiques |

Cette approche doit fonctionner avec l’ensemble des actions d’application API. N’oubliez pas cependant que ces applications API antérieures ne sont plus prises en charge. Par conséquent, vous devez déplacer tooone Hello deux autres options précédentes, une API managée ou héberger votre API Web personnalisée.

<a name="foreach"></a>
## <a name="renamed-repeat-tooforeach"></a>Renommé 'repeat' too'foreach'

Pour la version précédente du schéma hello, nous avons reçu de commentaires qui **répétez** était et n’a pas de capturer correctement qui **répétez** est vraiment une boucle pour chaque. Par conséquent, nous avons renommé `repeat` trop`foreach`. Par exemple, précédemment, vous auriez écrit :

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

Maintenant, vous devez écrire :

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

Hello fonction `@repeatItem()` a été élément actif de hello tooreference précédemment utilisés en cours d’itération. Cette fonction est simplifiée maintenant trop`@item()`. 

### <a name="reference-outputs-from-foreach"></a>Référencement des sorties de 'foreach'

Pour la simplification, hello sorties de `foreach` actions ne sont pas encapsulées dans un objet appelé `repeatItems`. Alors que hello sorties de hello précédente `repeat` exemple était :

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

Les sorties sont maintenant :

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

Auparavant, tooget toohello corps de d’action hello lors du référencement de ces sorties :

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

Désormais le code présente cette apparence :

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

Avec ces modifications, hello fonctions `@repeatItem()`, `@repeatBody()`, et `@repeatOutputs()` sont supprimés.

<a name="http-listener"></a>
## <a name="native-http-listener"></a>Écouteur HTTP natif

Hello fonctionnalités sont désormais intégrées dans l’écouteur HTTP. Par conséquent, vous n’avez plus besoin toodeploy une application API d’écouteur HTTP. Consultez [hello tous les détails de la procédure toomake votre ici peut être appelée du point de terminaison d’application logique](../logic-apps/logic-apps-http-endpoint.md). 

Avec ces modifications, nous avons supprimé hello `@accessKeys()` fonction, nous avons remplacé par hello `@listCallbackURL()` fonction pour l’obtention de point de terminaison hello lorsque cela est nécessaire. De plus, vous devez maintenant définir au moins un déclencheur dans votre application logique. Si vous souhaitez trop`/run` hello du flux de travail, vous devez avoir une de ces déclencheurs : `manual`, `apiConnectionWebhook`, ou `httpWebhook`.

<a name="child-workflows"></a>
## <a name="call-child-workflows"></a>Appel de flux de travail enfants

Auparavant, l’appel de flux de travail enfant requis va workflow toohello, obtention de jeton d’accès hello et collage de hello jeton dans la définition d’application hello logique où vous souhaitez toocall ce flux de travail enfant. Avec le nouveau schéma de hello, hello Logic Apps moteur génère automatiquement une SAP lors de l’exécution pour hello workflow enfant afin de ne pas avoir trop coller les clés secrètes dans la définition de hello. Voici un exemple :

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

Une deuxième amélioration est que nous offrons enfant de hello demande entrante de flux de travail un accès complet toohello. Cela signifie que vous pouvez passer des paramètres dans hello *requêtes* section et Bonjour *en-têtes* objet et que vous pouvez définir entièrement hello corps entier.

Enfin, des flux de travail enfant de toohello les modifications requises. Maintenant pendant que vous pourriez précédemment appeler un workflow enfant directement, vous devez définir un point de terminaison du déclencheur dans le flux de travail hello pour hello parent toocall. En règle générale, vous devez ajouter un déclencheur a `manual` tapez, puis utiliser ce déclencheur dans la définition du parent hello. Hello de note `host` propriété prévoit spécifiquement une `triggerName` , car vous devez toujours spécifier dont le déclencheur vous appelez.

## <a name="other-changes"></a>Autres modifications

### <a name="new-queries-property"></a>Nouvelle propriété « queries »

Tous les types d’action prennent désormais en charge une nouvelle entrée appelée `queries`. Cette entrée peut être un objet structuré, plutôt que vous ayez chaîne hello de tooassemble manuellement.

### <a name="renamed-parse-function-toojson"></a>Renommé « parse() » fonction too'json()'

Nous ajoutons davantage de contenu types bientôt, donc nous avons renommé hello `parse()` fonction trop`json()`.

## <a name="coming-soon-enterprise-integration-apis"></a>Bientôt disponibles : API d’intégration d’entreprise

Nous n’avons pas versions managées encore de hello entreprise intégration API, comme AS2. Pendant ce temps, vous pouvez utiliser votre APIs BizTalk déployées existantes via hello action HTTP. Pour plus d’informations, consultez « Utilisation de vos applications API déjà déployées « Bonjour [feuille de route pour l’intégration](http://www.zdnet.com/article/microsoft-outlines-its-cloud-and-server-integration-roadmap-for-2016/). 
