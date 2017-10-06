---
title: aaaAutomate Azure Application Insights avec PowerShell | Documents Microsoft
description: "Automatisez la création de tests de ressources, d’alerte et de disponibilité dans PowerShell à l’aide d’un modèle Azure Resource Manager."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 9f73b87f-be63-4847-88c8-368543acad8b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/02/2017
ms.author: bwren
ms.openlocfilehash: ebd336eafba58a690a0e8ffbd1c74f7e93dbb682
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
#  <a name="create-application-insights-resources-using-powershell"></a>Créer des ressources Application Insights à l’aide de PowerShell
Cet article vous explique comment tooautomate hello la création et la mise à jour de [Application Insights](app-insights-overview.md) ressources automatiquement à l’aide de gestion des ressources Azure. Cette opération peut par exemple avoir lieu dans le cadre du processus de génération. En même temps que la ressource d’Application Insights base hello, vous pouvez créer [disponibilité des tests web](app-insights-monitor-web-app-availability.md), paramétrez les [alertes](app-insights-alerts.md), affectez la valeur hello [tarification schéma](app-insights-pricing.md)et créer d’autres Azure ressources.

Hello toocreating clé ces ressources sont des modèles JSON pour [Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md). En bref, la procédure de hello est : télécharger les définitions de JSON hello des ressources existantes ; paramétrer certaines valeurs telles que les noms ; puis exécutez le modèle de hello chaque fois que vous souhaitez toocreate une nouvelle ressource. Vous pouvez empaqueter d’ensemble de plusieurs ressources, toocreate que les tout en un accédez - par exemple, une analyse de l’application avec les tests de disponibilité, des alertes et de stockage pour l’exportation continue. Il existe certains toosome subtilités de paramétrages hello, que nous aborderons ici.

## <a name="one-time-setup"></a>Installation unique
Si vous n’avez pas utilisé précédemment PowerShell avec votre abonnement Azure :

Installer le module de Azure Powershell de hello sur ordinateur hello où vous souhaitez les scripts de hello toorun :

1. Installez le programme [Microsoft Web Platform Installer (v5 ou version ultérieure)](http://www.microsoft.com/web/downloads/platform.aspx).
2. Utiliser tooinstall Microsoft Azure Powershell.

## <a name="create-an-azure-resource-manager-template"></a>Créer un modèle Azure Resource Manager
Créez un fichier .json appelé `template1.json` dans cet exemple. Copiez-y ce contenu :

```JSON
    {
        "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "appName": {
                "type": "string",
                "metadata": {
                    "description": "Enter hello application name."
                }
            },
            "appType": {
                "type": "string",
                "defaultValue": "web",
                "allowedValues": [
                    "web",
                    "java",
                    "HockeyAppBridge",
                    "other"
                ],
                "metadata": {
                    "description": "Enter hello application type."
                }
            },
            "appLocation": {
                "type": "string",
                "defaultValue": "East US",
                "allowedValues": [
                    "South Central US",
                    "West Europe",
                    "East US",
                    "North Europe"
                ],
                "metadata": {
                    "description": "Enter hello application location."
                }
            },
            "priceCode": {
                "type": "int",
                "defaultValue": 1,
                "allowedValues": [
                    1,
                    2
                ],
                "metadata": {
                    "description": "1 = Basic, 2 = Enterprise"
                }
            },
            "dailyQuota": {
                "type": "int",
                "defaultValue": 100,
                "minValue": 1,
                "metadata": {
                    "description": "Enter daily quota in GB."
                }
            },
            "dailyQuotaResetTime": {
                "type": "int",
                "defaultValue": 24,
                "metadata": {
                    "description": "Enter daily quota reset hour in UTC (0 too23). Values outside hello range will get a random reset hour."
                }
            },
            "warningThreshold": {
                "type": "int",
                "defaultValue": 90,
                "minValue": 1,
                "maxValue": 100,
                "metadata": {
                    "description": "Enter hello % value of daily quota after which warning mail toobe sent. "
                }
            }
        },
        "variables": {
            "priceArray": [
                "Basic",
                "Application Insights Enterprise"
            ],
            "pricePlan": "[take(variables('priceArray'),parameters('priceCode'))]",
            "billingplan": "[concat(parameters('appName'),'/', variables('pricePlan')[0])]"
        },
        "resources": [
            {
                "type": "microsoft.insights/components",
                "kind": "[parameters('appType')]",
                "name": "[parameters('appName')]",
                "apiVersion": "2014-04-01",
                "location": "[parameters('appLocation')]",
                "tags": {},
                "properties": {
                    "ApplicationId": "[parameters('appName')]"
                },
                "dependsOn": []
            },
            {
                "name": "[variables('billingplan')]",
                "type": "microsoft.insights/components/CurrentBillingFeatures",
                "location": "[parameters('appLocation')]",
                "apiVersion": "2015-05-01",
                "dependsOn": [
                    "[resourceId('microsoft.insights/components', parameters('appName'))]"
                ],
                "properties": {
                    "CurrentBillingFeatures": "[variables('pricePlan')]",
                    "DataVolumeCap": {
                        "Cap": "[parameters('dailyQuota')]",
                        "WarningThreshold": "[parameters('warningThreshold')]",
                        "ResetTime": "[parameters('dailyQuotaResetTime')]"
                    }
                }
            }
        ]
    }
```



## <a name="create-application-insights-resources"></a>Créer des ressources Application Insights
1. Dans PowerShell, la connexion tooAzure :
   
    `Login-AzureRmAccount`
2. Exécutez une commande comme suit :
   
    ```PS
   
        New-AzureRmResourceGroupDeployment -ResourceGroupName Fabrikam `
               -TemplateFile .\template1.json `
               -appName myNewApp

    ``` 
   
   * `-ResourceGroupName`est le groupe de hello où vous souhaitez que les ressources de nouveau toocreate hello.
   * `-TemplateFile`doit se produire avant les paramètres personnalisés hello.
   * `-appName`nom de Hello de hello ressource toocreate.

Vous pouvez ajouter d’autres paramètres : vous trouverez leur description dans la section des paramètres de modèle de hello hello.

## <a name="tooget-hello-instrumentation-key"></a>clé d’instrumentation hello tooget
Après avoir créé une ressource d’application, vous souhaiterez clé d’instrumentation hello : 

```PS
    $resource = Find-AzureRmResource -ResourceNameEquals "<YOUR APP NAME>" -ResourceType "Microsoft.Insights/components"
    $details = Get-AzureRmResource -ResourceId $resource.ResourceId
    $ikey = $details.Properties.InstrumentationKey
```


<a id="price"></a>
## <a name="set-hello-price-plan"></a>Plan de prix hello ensemble

Vous pouvez définir hello [plan tarifaire](app-insights-pricing.md).

toocreate une ressource d’application avec un plan prix hello entreprise, à l’aide du modèle hello ci-dessus :

```PS
        New-AzureRmResourceGroupDeployment -ResourceGroupName Fabrikam `
               -TemplateFile .\template1.json `
               -priceCode 2 `
               -appName myNewApp
```

|priceCode|Plan|
|---|---|
|1|De base|
|2|Entreprise|

* Si vous ne souhaitez que le plan de prix de base par défaut toouse hello, vous pouvez omettre la ressource de CurrentBillingFeatures hello à partir du modèle de hello.
* Si vous souhaitez plan de prix toochange hello après de la ressource de composant hello a été créé, vous pouvez utiliser un modèle qui omet la ressource de « Microsoft.Insights/Components. » hello. En outre, omettez hello `dependsOn` nœud hello facturation des ressources. 

tooverify hello du plan de prix mis à jour, examinez le panneau hello « Fonctionnalités + tarification » dans le navigateur de hello. **Actualiser l’affichage du navigateur hello** toomake que vous voyez l’état le plus récent hello.



## <a name="add-a-metric-alert"></a>Ajouter une alerte métrique

tooset une alerte de métriques à hello même moment que la ressource de votre application, code fusion similaire à celui-ci dans le fichier de modèle hello :

```JSON
{
    parameters: { ... // existing parameters ...
            "responseTime": {
              "type": "int",
              "defaultValue": 3,
              "minValue": 1,
              "metadata": {
                "description": "Enter response time threshold in seconds."
              }
    },
    variables: { ... // existing variables ...
      // Alert names must be unique within resource group.
      "responseAlertName": "[concat('ResponseTime-', toLower(parameters('appName')))]"
    }, 
    resources: { ... // existing resources ...
     {
      //
      // Metric alert on response time
      //
      "name": "[variables('responseAlertName')]",
      "type": "Microsoft.Insights/alertrules",
      "apiVersion": "2014-04-01",
      "location": "[parameters('appLocation')]",
      // Ensure this resource is created after hello app resource:
      "dependsOn": [
        "[resourceId('Microsoft.Insights/components', parameters('appName'))]"
      ],
      "tags": {
        "[concat('hidden-link:', resourceId('Microsoft.Insights/components', parameters('appName')))]": "Resource"
      },
      "properties": {
        "name": "[variables('responseAlertName')]",
        "description": "response time alert",
        "isEnabled": true,
        "condition": {
          "$type": "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.ThresholdRuleCondition, Microsoft.WindowsAzure.Management.Mon.Client",
          "odata.type": "Microsoft.Azure.Management.Insights.Models.ThresholdRuleCondition",
          "dataSource": {
            "$type": "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleMetricDataSource, Microsoft.WindowsAzure.Management.Mon.Client",
            "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleMetricDataSource",
            "resourceUri": "[resourceId('microsoft.insights/components', parameters('appName'))]",
            "metricName": "request.duration"
          },
          "threshold": "[parameters('responseTime')]", //seconds
          "windowSize": "PT15M" // Take action if changed state for 15 minutes
        },
        "actions": [
          {
            "$type": "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleEmailAction, Microsoft.WindowsAzure.Management.Mon.Client",
            "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
            "sendToServiceOwners": true,
            "customEmails": []
          }
        ]
      }
    }
}
```

Lorsque vous appelez le modèle de hello, vous pouvez éventuellement ajouter ce paramètre :

    `-responseTime 2`

Bien entendu, vous pouvez paramétrer d’autres champs. 

toofind les noms de type hello et les détails de configuration d’autres règles d’alerte, créez une règle manuellement, puis d’examiner dans [Azure Resource Manager](https://resources.azure.com/). 


## <a name="add-an-availability-test"></a>Ajouter un test de disponibilité

Cet exemple est pour un test ping (tootest une seule page).  

**Il existe deux parties** dans un test de disponibilité : test hello lui-même et cette alerte hello qui vous informe des échecs.

Fusion hello après le code dans le fichier de modèle hello qui crée l’application hello.

```JSON
{
    parameters: { ... // existing parameters here ...
      "pingURL": { "type": "string" },
      "pingText": { "type": "string" , defaultValue: ""}
    },
    variables: { ... // existing variables here ...
      "pingTestName":"[concat('PingTest-', toLower(parameters('appName')))]",
      "pingAlertRuleName": "[concat('PingAlert-', toLower(parameters('appName')), '-', subscription().subscriptionId)]"
    },
    resources: { ... // existing resources here ...
    { //
      // Availability test: part 1 configures hello test
      //
      "name": "[variables('pingTestName')]",
      "type": "Microsoft.Insights/webtests",
      "apiVersion": "2014-04-01",
      "location": "[parameters('appLocation')]",
      // Ensure this is created after hello app resource:
      "dependsOn": [
        "[resourceId('Microsoft.Insights/components', parameters('appName'))]"
      ],
      "tags": {
        "[concat('hidden-link:', resourceId('Microsoft.Insights/components', parameters('appName')))]": "Resource"
      },
      "properties": {
        "Name": "[variables('pingTestName')]",
        "Description": "Basic ping test",
        "Enabled": true,
        "Frequency": 900, // 15 minutes
        "Timeout": 120, // 2 minutes
        "Kind": "ping", // single URL test
        "RetryEnabled": true,
        "Locations": [
          {
            "Id": "us-va-ash-azr"
          },
          {
            "Id": "emea-nl-ams-azr"
          },
          {
            "Id": "apac-jp-kaw-edge"
          }
        ],
        "Configuration": {
          "WebTest": "[concat('<WebTest   Name=\"', variables('pingTestName'), '\"   Enabled=\"True\"         CssProjectStructure=\"\"    CssIteration=\"\"  Timeout=\"120\"  WorkItemIds=\"\"         xmlns=\"http://microsoft.com/schemas/VisualStudio/TeamTest/2010\"         Description=\"\"  CredentialUserName=\"\"  CredentialPassword=\"\"         PreAuthenticate=\"True\"  Proxy=\"default\"  StopOnError=\"False\"         RecordedResultFile=\"\"  ResultsLocale=\"\">  <Items>  <Request Method=\"GET\"    Version=\"1.1\"  Url=\"', parameters('Url'),   '\" ThinkTime=\"0\"  Timeout=\"300\" ParseDependentRequests=\"True\"         FollowRedirects=\"True\" RecordResult=\"True\" Cache=\"False\"         ResponseTimeGoal=\"0\"  Encoding=\"utf-8\"  ExpectedHttpStatusCode=\"200\"         ExpectedResponseUrl=\"\" ReportingName=\"\" IgnoreHttpStatusCode=\"False\" />        </Items>  <ValidationRules> <ValidationRule  Classname=\"Microsoft.VisualStudio.TestTools.WebTesting.Rules.ValidationRuleFindText, Microsoft.VisualStudio.QualityTools.WebTestFramework, Version=10.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a\" DisplayName=\"Find Text\"         Description=\"Verifies hello existence of hello specified text in hello response.\"         Level=\"High\"  ExectuionOrder=\"BeforeDependents\">  <RuleParameters>        <RuleParameter Name=\"FindText\" Value=\"',   parameters('pingText'), '\" />  <RuleParameter Name=\"IgnoreCase\" Value=\"False\" />  <RuleParameter Name=\"UseRegularExpression\" Value=\"False\" />  <RuleParameter Name=\"PassIfTextFound\" Value=\"True\" />  </RuleParameters> </ValidationRule>  </ValidationRules>  </WebTest>')]"
        },
        "SyntheticMonitorId": "[variables('pingTestName')]"
      }
    },

    {
      //
      // Availability test: part 2, hello alert rule
      //
      "name": "[variables('pingAlertRuleName')]",
      "type": "Microsoft.Insights/alertrules",
      "apiVersion": "2014-04-01",
      "location": "[parameters('appLocation')]", 
      "dependsOn": [
        "[resourceId('Microsoft.Insights/webtests', variables('pingTestName'))]"
      ],
      "tags": {
        "[concat('hidden-link:', resourceId('Microsoft.Insights/components', parameters('appName')))]": "Resource",
        "[concat('hidden-link:', resourceId('Microsoft.Insights/webtests', variables('pingTestName')))]": "Resource"
      },
      "properties": {
        "name": "[variables('pingAlertRuleName')]",
        "description": "alert for web test",
        "isEnabled": true,
        "condition": {
          "$type": "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.LocationThresholdRuleCondition, Microsoft.WindowsAzure.Management.Mon.Client",
          "odata.type": "Microsoft.Azure.Management.Insights.Models.LocationThresholdRuleCondition",
          "dataSource": {
            "$type": "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleMetricDataSource, Microsoft.WindowsAzure.Management.Mon.Client",
            "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleMetricDataSource",
            "resourceUri": "[resourceId('microsoft.insights/webtests', variables('pingTestName'))]",
            "metricName": "GSMT_AvRaW"
          },
          "windowSize": "PT15M", // Take action if changed state for 15 minutes
          "failedLocationCount": 2
        },
        "actions": [
          {
            "$type": "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleEmailAction, Microsoft.WindowsAzure.Management.Mon.Client",
            "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
            "sendToServiceOwners": true,
            "customEmails": []
          }
        ]
      }
    }
}
```

toodiscover les codes de hello pour d’autres emplacements de test, ou la création de hello tooautomate nombre de tests web plus complexes, créer un exemple manuellement et puis paramétrer code hello à partir de [Azure Resource Manager](https://resources.azure.com/).

## <a name="add-more-resources"></a>Ajouter des ressources

Création de hello tooautomate de toute autre ressource de tout type, créer un exemple manuellement, puis copiez et paramétrer son code à partir de [Azure Resource Manager](https://resources.azure.com/). 

1. Ouvrez [Azure Resource Manager](https://resources.azure.com/). Naviguer vers le bas dans `subscriptions/resourceGroups/<your resource group>/providers/Microsoft.Insights/components`, tooyour de ressource d’application. 
   
    ![Navigation dans Azure Resource Explorer](./media/app-insights-powershell/01.png)
   
    *Composants* est hello base ressources Application Insights pour l’affichage des applications. Il existe des ressources distinctes pour hello associé des règles d’alerte et la disponibilité des tests web.
2. Hello de copie JSON du composant hello dans l’emplacement approprié de hello dans `template1.json`.
3. Supprimez les propriétés suivantes :
   
   * `id`
   * `InstrumentationKey`
   * `CreationDate`
   * `TenantId`
4. Ouvrir des sections de webtests et alertrules hello et copiez hello JSON pour les éléments individuels dans votre modèle. (Ne pas copier à partir des nœuds de webtests ou alertrules hello : accédez aux éléments hello sous eux.)
   
    Chaque test web a une règle d’alerte associée, afin que vous ayez toocopy d'entre eux.
   
    Vous pouvez également inclure des alertes sur des métriques. [Noms de métriques](app-insights-powershell-alerts.md#metric-names).
5. Insérez cette ligne dans chaque ressource :
   
    `"apiVersion": "2015-05-01",`

### <a name="parameterize-hello-template"></a>Paramétrer le modèle de hello
Vous disposez maintenant des noms spécifiques de hello tooreplace avec des paramètres. trop[paramétrer un modèle](../azure-resource-manager/resource-group-authoring-templates.md), vous écrivez des expressions à l’aide un [ensemble de fonctions d’assistance](../azure-resource-manager/resource-group-template-functions.md). 

Vous ne peut pas paramétrer la partie d’une chaîne, alors utilisez `concat()` toobuild chaînes.

Voici des exemples de substitutions de hello, vous souhaiterez toomake. Il existe plusieurs occurrences de chaque substitution. Il vous en faudra peut-être d’autres dans votre modèle. Ces exemples utilisent les paramètres de hello et nous avons défini les variables haut hello du modèle de hello.

| find | replace with |
| --- | --- |
| `"hidden-link:/subscriptions/.../components/MyAppName"` |`"[concat('hidden-link:',`<br/>` resourceId('microsoft.insights/components',` <br/> ` parameters('appName')))]"` |
| `"/subscriptions/.../alertrules/myAlertName-myAppName-subsId",` |`"[resourceId('Microsoft.Insights/alertrules', variables('alertRuleName'))]",` |
| `"/subscriptions/.../webtests/myTestName-myAppName",` |`"[resourceId('Microsoft.Insights/webtests', parameters('webTestName'))]",` |
| `"myWebTest-myAppName"` |`"[variables(testName)]"'` |
| `"myTestName-myAppName-subsId"` |`"[variables('alertRuleName')]"` |
| `"myAppName"` |`"[parameters('appName')]"` |
| `"myappname"` (minuscules) |`"[toLower(parameters('appName'))]"` |
| `"<WebTest Name=\"myWebTest\" ...`<br/>` Url=\"http://fabrikam.com/home\" ...>"` |`[concat('<WebTest Name=\"',` <br/> `parameters('webTestName'),` <br/> `'\" ... Url=\"', parameters('Url'),` <br/> `'\"...>')]"`<br/>Supprimez le GUID et l’ID. |

### <a name="set-dependencies-between-hello-resources"></a>Définition de relations entre les ressources hello
Configurez Azure ressources hello dans un ordre strict. toomake assurer un paramétrage se termine avant que hello commence ensuite, ajoutez les lignes de dépendance :

* Ressource de test de disponibilité de hello :
  
    `"dependsOn": ["[resourceId('Microsoft.Insights/components', parameters('appName'))]"],`
* Dans la ressource d’alerte hello pour un test de disponibilité :
  
    `"dependsOn": ["[resourceId('Microsoft.Insights/webtests', variables('testName'))]"],`



## <a name="next-steps"></a>Étapes suivantes
Autres articles sur l’automation :

* [Création d'une ressource Application Insights](app-insights-powershell-script-create-resource.md) - méthode rapide sans utiliser de modèle.
* [Configurer des alertes](app-insights-powershell-alerts.md)
* [Créer des tests web](https://azure.microsoft.com/blog/creating-a-web-test-alert-programmatically-with-application-insights/)
* [Envoyer des Diagnostics Windows Azure tooApplication Insights](app-insights-powershell-azure-diagnostics.md)
* [Déployer tooAzure à partir de GitHub](http://blogs.msdn.com/b/webdev/archive/2015/09/16/deploy-to-azure-from-github-with-application-insights.aspx)
* [Créer des annotations de version](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/API/CreateReleaseAnnotation.ps1)

