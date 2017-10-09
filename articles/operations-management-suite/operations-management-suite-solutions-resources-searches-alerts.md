---
title: aaaSaved recherches et les alertes dans les solutions OMS | Documents Microsoft
description: "Solutions dans OMS inclut généralement les recherches enregistrées dans Analytique de journal tooanalyze collectées par les solutions hello.  Ils peuvent également définir l’utilisateur d’alertes toonotify hello ou agir automatiquement en problème critique tooa de réponse.  Cet article décrit comment toodefine Analytique de journal enregistrées recherches et les alertes dans un modèle ARM afin qu’ils peuvent être inclus dans les solutions de gestion."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 93d7c5bbf061473833ca6c0a8e4d8e10d923f3ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="adding-log-analytics-saved-searches-and-alerts-toooms-management-solution-preview"></a>Ajout d’Analytique de journal enregistré tooOMS recherches et les alertes solution de gestion (version préliminaire)

> [!NOTE]
> Il s’agit d’une documentation préliminaire pour la création de solutions de gestion dans OMS qui sont actuellement en préversion. N’importe quel schéma décrit ci-dessous est un objet toochange.   


[Solutions de gestion OMS](operations-management-suite-solutions.md) inclut généralement [recherches enregistrées](../log-analytics/log-analytics-log-searches.md) dans Analytique de journal tooanalyze collectées par les solutions hello.  Ils peuvent également définir [alertes](../log-analytics/log-analytics-alerts.md) toonotify hello utilisateur ou agir automatiquement en problème critique tooa de réponse.  Cet article décrit comment toodefine Analytique de journal enregistrées recherches et les alertes dans un [modèle de gestion des ressources](../resource-manager-template-walkthrough.md) afin qu’ils peuvent être inclus dans [solutions de gestion](operations-management-suite-solutions-creating.md).

> [!NOTE]
> Hello exemples dans cet article utilisent les paramètres et les variables qui sont deux solutions toomanagement requises ou courantes et décrites dans [création de solutions de gestion Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)  

## <a name="prerequisites"></a>Composants requis
Cet article suppose que vous êtes déjà familiarisé avec le trop[créer une solution de gestion](operations-management-suite-solutions-creating.md) et la structure hello d’un [modèle ARM](../resource-group-authoring-templates.md) et le fichier de solution.


## <a name="log-analytics-workspace"></a>Espace de travail Log Analytics
Toutes les ressources dans Log Analytics sont contenues dans un [espace de travail](../log-analytics/log-analytics-manage-access.md).  Comme décrit dans [OMS espace de travail et le compte Automation](operations-management-suite-solutions.md#oms-workspace-and-automation-account) espace de travail hello n’est pas inclus dans la solution de gestion hello mais doit exister pour que la solution de hello est installée.  Si elle n’est pas disponible, hello solution installation échouera.

nom Hello d’espace de travail hello est nom hello de chaque ressource Analytique de journal.  Cette opération est effectuée dans la solution hello avec hello **espace de travail** paramètre comme hello d’une ressource savedsearch l’exemple suivant.

    "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearchId'))]"


## <a name="saved-searches"></a>Recherches enregistrées
Inclure [recherches enregistrées](../log-analytics/log-analytics-log-searches.md) dans une solution tooallow utilisateurs tooquery de données collecté par votre solution.  Recherches enregistrées seront affiche sous **favoris** dans portail OMS : hello et **recherches enregistrées** Bonjour portail Azure.  Une recherche enregistrée est également requise pour chaque alerte.   

[Recherche de journal Analytique enregistrée](../log-analytics/log-analytics-log-searches.md) ressources ont un type de `Microsoft.OperationalInsights/workspaces/savedSearches` et avoir hello suivant la structure.  Cela inclut des variables et des paramètres courants afin que vous pouvez copier et coller cet extrait de code dans votre fichier de solution et modifier les noms de paramètre hello. 

    {
        "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name)]",
        "type": "Microsoft.OperationalInsights/workspaces/savedSearches",
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "dependsOn": [
        ],
        "tags": { },
        "properties": {
            "etag": "*",
            "query": "[variables('SavedSearch').Query]",
            "displayName": "[variables('SavedSearch').DisplayName]",
            "category": "[variables('SavedSearch').Category]"
        }
    }



Chacune des propriétés hello d’une recherche enregistrée sont décrits dans hello tableau suivant. 

| Propriété | Description |
|:--- |:--- |
| category | catégorie Hello pour la recherche enregistrée hello.  Les recherches enregistrement Bonjour même solution souvent partagent une même catégorie afin qu’ils sont regroupés dans la console de hello. |
| displayname | Toodisplay de nom pour hello recherche enregistrée dans le portail de hello. |
| query | Toorun de la requête. |

> [!NOTE]
> Vous devrez peut-être toouse des caractères d’échappement dans la requête de hello si elle inclut des caractères qui peuvent être interprétés en tant que JSON.  Par exemple, si votre requête a été **Type : AzureActivity OperationName:"Microsoft.Compute/virtualMachines/write »**, il doit être écrit dans le fichier de solution hello en tant que **OperationName de Type : AzureActivity :\" Microsoft.Compute/virtualMachines/write\"**.

## <a name="alerts"></a>Alertes
Les [alertes Log Analytics](../log-analytics/log-analytics-alerts.md) sont créées par le biais de règles d’alerte exécutant une recherche enregistrée à intervalles réguliers.  Si des résultats de requête de hello hello correspondent aux critères spécifiés, un enregistrement d’alerte est créé et une ou plusieurs actions sont exécutées.  

Règles d’alerte dans une solution de gestion sont constituées de hello suivant trois différentes ressources.

- **Recherche enregistrée.**  Définit la recherche de journal hello qui est exécutée.  Plusieurs règles d’alerte peuvent partager une même recherche enregistrée.
- **Planification.**  Définit la fréquence à laquelle hello recherche de journal sera exécuté.  Chaque règle d’alerte est associée à une planification unique.
- **Action d’alerte.**  Chaque règle d’alerte aura une ressource d’action avec un type de **alerte** qui définit les détails de hello d’alerte de hello telles que les critères de hello lorsqu’un enregistrement d’alerte sera créé puis hello la gravité de l’alerte.  ressource d’action Hello sera éventuellement définir une réponse de la messagerie et le runbook.
- **Action webhook (facultative).**  Si une règle d’alerte hello appelle un webhook, il requiert une ressource d’une action avec un type de **Webhook**.    

Les ressources de recherche enregistrée sont décrites ci-dessus.  Hello autres ressources sont décrits ci-dessous.


### <a name="schedule-resource"></a>Ressource de planification

Une recherche enregistrée peut avoir une ou plusieurs planifications, chacune d’entre elles représentant une règle d’alerte distincte. Hello planification définit la fréquence à laquelle hello recherche est exécutée et hello intervalle de temps sur le hello les données sont récupérées.  Planifier des ressources ont un type de `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/` et avoir hello suivant la structure. Cela inclut des variables et des paramètres courants afin que vous pouvez copier et coller cet extrait de code dans votre fichier de solution et modifier les noms de paramètre hello. 


    {
        "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name, '/', variables('Schedule').Name)]",
        "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/",
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('SavedSearch').Name)]"
        ],
        "properties": {
            "etag": "*",
            "interval": "[variables('Schedule').Interval]",
            "queryTimeSpan": "[variables('Schedule').TimeSpan]",
            "enabled": "[variables('Schedule').Enabled]"
        }
    }



Décrit les propriétés de Hello pour planifier des ressources Bonjour tableau suivant.

| Nom de l'élément | Requis | Description |
|:--|:--|:--|
| Activé       | Oui | Spécifie si l’alerte de hello est activée lors de sa création. |
| interval      | Oui | La fréquence à laquelle hello requête s’exécute en quelques minutes. |
| queryTimeSpan | Oui | Durée en minutes sur les résultats tooevaluate. |

ressource de planification Hello doit s’appuyer sur hello recherche enregistrée afin qu’elle est créée avant la planification de hello.


### <a name="actions"></a>Actions
Il existe deux types de ressource d’action spécifié par hello **Type** propriété.  Une planification requiert un **alerte** action qui définit les détails de hello de règle d’alerte hello et les actions prises lors de la création d’une alerte.  Il peut également inclure un **Webhook** action si un webhook doit être appelé à partir de l’alerte de hello.  

Les ressources d’action ont un type `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions`.  

#### <a name="alert-actions"></a>Actions d’alerte

Chaque planification est associée à une action **Alert**.  Définit les détails de hello d’alerte de hello et, éventuellement, les actions de notification et de correction.  Une notification envoie un e-mail tooone ou de plusieurs adresses.  Une mise à jour démarre un runbook problème de Azure Automation tooattempt tooremediate hello détecté.

Actions d’alerte ont hello suivant la structure.  Cela inclut des variables et des paramètres courants afin que vous pouvez copier et coller cet extrait de code dans votre fichier de solution et modifier les noms de paramètre hello. 



    {
        "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name, '/', variables('Schedule').Name, '/', variables('Alert').Name)]",
        "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions",
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('SavedSearch').Name, '/schedules/', variables('Schedule').Name)]"
        ],
        "properties": {
            "etag": "*",
            "type": "Alert",
            "name": "[variables('Alert').Name]",
            "description": "[variables('Alert').Description]",
            "severity": "[variables('Alert').Severity]",
            "threshold": {
                "operator": "[variables('Alert').Threshold.Operator]",
                "value": "[variables('Alert').Threshold.Value]",
                "metricsTrigger": {
                    "triggerCondition": "[variables('Alert').Threshold.Trigger.Condition]",
                    "operator": "[variables('Alert').Trigger.Operator]",
                    "value": "[variables('Alert').Trigger.Value]"
                },
            },
            "emailNotification": {
                "recipients": [
                    "[variables('Alert').Recipients]"
                ],
                "subject": "[variables('Alert').Subject]"
            },
            "remediation": {
                "runbookName": "[variables('Alert').Remedition.RunbookName]",
                "webhookUri": "[variables('Alert').Remedition.WebhookUri]"
            }
        }
    }

propriétés Hello pour les ressources de l’action d’alerte sont décrits dans les tableaux suivants de hello.

| Nom de l'élément | Requis | Description |
|:--|:--|:--|
| Type | Oui | Type d’action de hello.  Ce type sera **Alert** pour les actions d’alerte. |
| Nom | Oui | Nom complet de l’alerte de hello.  Il s’agit de nom hello qui s’affiche dans la console pour la règle d’alerte hello hello. |
| Description | Non | Description facultative de l’alerte de hello. |
| Severity | Oui | Gravité d’enregistrements alerte hello hello valeurs suivantes :<br><br> **Critical**<br>**Avertissement**<br>**Informational** |


##### <a name="threshold"></a>Seuil
Cette section est obligatoire.  Il définit les propriétés de hello pour le seuil d’alerte hello.

| Nom de l'élément | Requis | Description |
|:--|:--|:--|
| Opérateur  | Oui | Opérateur de comparaison hello de hello valeurs suivantes :<br><br>**gt = supérieur à<br>lt = inférieur à** |
| Valeur | Oui | résultats de hello valeur toocompare Hello. |


##### <a name="metricstrigger"></a>MetricsTrigger
Cette section est facultative.  Vous devez l’inclure pour une alerte relative aux mesures métriques.

> [!NOTE]
> Les alertes relatives aux mesures métriques sont actuellement en version préliminaire publique. 

| Nom de l'élément | Requis | Description |
|:--|:--|:--|
| TriggerCondition | Oui | Spécifie si le seuil de hello est pour le nombre total de violations ou consécutifs violations de hello valeurs suivantes :<br><br>**Total<br>Consecutive** |
| Opérateur  | Oui | Opérateur de comparaison hello de hello valeurs suivantes :<br><br>**gt = supérieur à<br>lt = inférieur à** |
| Valeur | Oui | Nombre de hello heures hello critères doit être alerte de hello tootrigger rempli. |

##### <a name="throttling"></a>Limitation
Cette section est facultative.  Incluez cette section si vous souhaitez recevoir des alertes toosuppress de hello même règle pour une certaine quantité de temps après qu’une alerte est créée.

| Nom de l'élément | Requis | Description |
|:--|:--|:--|
| DurationInMinutes | Oui, si l’élément Throttling est inclus | Nombre de minutes toosuppress des alertes après une à partir de hello même règle d’alerte est créée. |

##### <a name="emailnotification"></a>EmailNotification
 Cette section est facultative inclure si vous souhaitez hello tooone de messagerie toosend alerte ou des destinataires.

| Nom de l'élément | Requis | Description |
|:--|:--|:--|
| Destinataires | Oui | Liste séparée par des virgules de courrier électronique adresses toosend notification lorsqu’une alerte est créée comme Bonjour l’exemple suivant.<br><br>**[ "recipient1@contoso.com", "recipient2@contoso.com" ]** |
| Objet | Oui | Ligne objet de messagerie de hello. |
| Pièce jointe | Non | Actuellement, les pièces jointes ne sont pas prises en charge.  Si cet élément est inclus, il doit avoir la valeur **None**. |


##### <a name="remediation"></a>Correction
Cette section est facultative inclure si vous souhaitez un toostart de runbook dans l’alerte toohello de réponse. |

| Nom de l'élément | Requis | Description |
|:--|:--|:--|
| RunbookName | Oui | Nom de hello runbook toostart. |
| WebhookUri | Oui | URI du webhook hello pour hello runbook. |
| Expiry | Non | Date et heure de mise à jour de hello expire. |

#### <a name="webhook-actions"></a>Actions de webhook

Les actions Webhook démarrer un processus en appelant une URL et éventuellement en fournissant un toobe de charge utile envoyée. Ils sont des actions tooRemediation similaires à ceci près qu’ils sont destinés à webhooks qui peut appeler des processus autres que les runbooks Azure Automation. Elles fournissent également hello option supplémentaire permettant de fournir un processus à distance de charge utile toobe remis toohello.

Si votre alerte appelle un webhook, vous devez une ressource d’action avec un type de **Webhook** dans Ajout toohello **alerte** ressource d’action.  

    {
      "name": "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name, '/', variables('Schedule').Name, '/', variables('Webhook').Name)]",
      "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions/",
      "apiVersion": "[variables('LogAnalyticsApiVersion')]",
      "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('SavedSearch').Name, '/schedules/', variables('Schedule').Name)]"
      ],
      "properties": {
        "etag": "*",
        "type": "[variables('Alert').Webhook.Type]",
        "name": "[variables('Alert').Webhook.Name]",
        "webhookUri": "[variables('Alert').Webhook.webhookUri]",
        "customPayload": "[variables('Alert').Webhook.CustomPayLoad]"
      }
    }

Décrit les propriétés de Hello pour ressources d’action Webhook Bonjour les tableaux suivants.

| Nom de l'élément | Requis | Description |
|:--|:--|:--|
| type | Oui | Type d’action de hello.  Il s’agit de **Webhook** pour les actions de webhook. |
| name | Oui | Nom complet de l’action de hello.  Cela n’est pas affiché dans la console de hello. |
| wehookUri | Oui | URI pour hello webhook. |
| customPayload | Non | Charge utile personnalisée toobe envoyé toohello webhook. format de Hello dépend de quelles webhook hello est attendu. |




## <a name="sample"></a>Exemple

Voici un exemple d’une solution qui incluent ce qui inclut hello suivant des ressources :

- Recherche enregistrée
- Planification
- Action d’alerte
- Action webhook

exemples d’utilisation de Hello [paramètres de solution standard](operations-management-suite-solutions-solution-file.md#parameters) variables sont communément utilisées dans une solution en opposition toohardcoding des valeurs dans les définitions de ressource hello.

    {
        "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0",
        "parameters": {
          "workspaceName": {
            "type": "string",
            "metadata": {
              "Description": "Name of Log Analytics workspace"
            }
          },
          "accountName": {
            "type": "string",
            "metadata": {
              "Description": "Name of Automation account"
            }
          },
          "workspaceregionId": {
            "type": "string",
            "metadata": {
              "Description": "Region of Log Analytics workspace"
            }
          },
          "regionId": {
            "type": "string",
            "metadata": {
              "Description": "Region of Automation account"
            }
          },
          "pricingTier": {
            "type": "string",
            "metadata": {
              "Description": "Pricing tier of both Log Analytics workspace and Azure Automation account"
            }
          },
          "recipients": {
            "type": "string",
            "metadata": {
              "Description": "List of recipients for hello email alert separated by semicolon"
            }
          }
        },
        "variables": {
          "SolutionName": "MySolution",
          "SolutionVersion": "1.0",
          "SolutionPublisher": "Contoso",
          "ProductName": "SampleSolution",
    
          "LogAnalyticsApiVersion": "2015-11-01-preview",
    
          "MySearch": {
            "displayName": "Error records by hour",
            "query": "Type=MyRecord_CL | measure avg(Rating_d) by Instance_s interval 60minutes",
            "category": "Samples",
            "name": "Samples-Count of data"
          },
          "MyAlert": {
            "Name": "[toLower(concat('myalert-',uniqueString(resourceGroup().id, deployment().name)))]",
            "DisplayName": "My alert rule",
            "Description": "Sample alert.  Fires when 3 error records found over hour interval.",
            "Severity": "Critical",
            "ThresholdOperator": "gt",
            "ThresholdValue": 3,
            "Schedule": {
              "Name": "[toLower(concat('myschedule-',uniqueString(resourceGroup().id, deployment().name)))]",
              "Interval": 15,
              "TimeSpan": 60
            },
            "MetricsTrigger": {
              "TriggerCondition": "Consecutive",
              "Operator": "gt",
              "Value": 3
            },
            "ThrottleMinutes": 60,
            "Notification": {
              "Recipients": [
                "[parameters('recipients')]"
              ],
              "Subject": "Sample alert"
            },
            "Remediation": {
              "RunbookName": "MyRemediationRunbook",
              "WebhookUri": "https://s1events.azure-automation.net/webhooks?token=TluBFH3GpX4IEAnFoImoAWLTULkjD%2bTS0yscyrr7ogw%3d"
            },
            "Webhook": {
              "Name": "MyWebhook",
              "Uri": "https://MyService.com/webhook",
              "Payload": "{\"field1\":\"value1\",\"field2\":\"value2\"}"
            }
          }
        },
        "resources": [
          {
            "name": "[concat(variables('SolutionName'), '[' ,parameters('workspacename'), ']')]",
            "location": "[parameters('workspaceRegionId')]",
            "tags": { },
            "type": "Microsoft.OperationsManagement/solutions",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches', parameters('workspacename'), variables('MySearch').Name)]",
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name)]",
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Name)]",
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Webhook.Name)]"
            ],
            "properties": {
              "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspacename'))]",
              "referencedResources": [
              ],
              "containedResources": [
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches', parameters('workspacename'), variables('MySearch').Name)]",
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name)]",
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Name)]",
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Webhook.Name)]"
              ]
            },
            "plan": {
              "name": "[concat(variables('SolutionName'), '[' ,parameters('workspaceName'), ']')]",
              "Version": "[variables('SolutionVersion')]",
              "product": "[variables('ProductName')]",
              "publisher": "[variables('SolutionPublisher')]",
              "promotionCode": ""
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [ ],
            "tags": { },
            "properties": {
              "etag": "*",
              "query": "[variables('MySearch').query]",
              "displayName": "[variables('MySearch').displayName]",
              "category": "[variables('MySearch').category]"
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name, '/', variables('MyAlert').Schedule.Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('MySearch').Name)]"
            ],
            "properties": {
              "etag": "*",
              "interval": "[variables('MyAlert').Schedule.Interval]",
              "queryTimeSpan": "[variables('MyAlert').Schedule.TimeSpan]",
              "enabled": true
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name, '/',  variables('MyAlert').Schedule.Name, '/',  variables('MyAlert').Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/',  variables('MySearch').Name, '/schedules/', variables('MyAlert').Schedule.Name)]"
            ],
            "properties": {
              "etag": "*",
              "Type": "Alert",
              "Name": "[variables('MyAlert').DisplayName]",
              "Description": "[variables('MyAlert').Description]",
              "Severity": "[variables('MyAlert').Severity]",
              "Threshold": {
                "Operator": "[variables('MyAlert').ThresholdOperator]",
                "Value": "[variables('MyAlert').ThresholdValue]",
                "MetricsTrigger": {
                  "TriggerCondition": "[variables('MyAlert').MetricsTrigger.TriggerCondition]",
                  "Operator": "[variables('MyAlert').MetricsTrigger.Operator]",
                  "Value": "[variables('MyAlert').MetricsTrigger.Value]"
                }
              },
              "Throttling": {
                "DurationInMinutes": "[variables('MyAlert').ThrottleMinutes]"
              },
              "EmailNotification": {
                "Recipients": "[variables('MyAlert').Notification.Recipients]",
                "Subject": "[variables('MyAlert').Notification.Subject]",
                "Attachment": "None"
              },
              "Remediation": {
                "RunbookName": "[variables('MyAlert').Remediation.RunbookName]",
                "WebhookUri": "[variables('MyAlert').Remediation.WebhookUri]"
              }
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name, '/', variables('MyAlert').Schedule.Name, '/', variables('MyAlert').Webhook.Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('MySearch').Name, '/schedules/', variables('MyAlert').Schedule.Name)]",
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('MySearch').Name, '/schedules/', variables('MyAlert').Schedule.Name, '/actions/',variables('MyAlert').Name)]"
            ],
            "properties": {
              "etag": "*",
              "Type": "Webhook",
              "Name": "[variables('MyAlert').Webhook.Name]",
              "WebhookUri": "[variables('MyAlert').Webhook.Uri]",
              "CustomPayload": "[variables('MyAlert').Webhook.Payload]"
            }
          }
        ]
    }


Hello suivant du fichier de paramètres fournit des valeurs d’exemples pour cette solution.

    {
        "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "workspacename": {
                "value": "myWorkspace"
            },
            "accountName": {
                "value": "myAccount"
            },
            "workspaceregionId": {
                "value": "East US"
            },
            "regionId": {
                "value": "East US 2"
            },
            "pricingTier": {
                "value": "Free"
            },
            "recipients": {
                "value": "recipient1@contoso.com;recipient2@contoso.com"
            }
        }
    }


## <a name="next-steps"></a>Étapes suivantes
* [Ajouter des vues](operations-management-suite-solutions-resources-views.md) solution de gestion tooyour.
* [Ajouter des runbooks Automation et autres ressources](operations-management-suite-solutions-resources-automation.md) solution de gestion tooyour.

