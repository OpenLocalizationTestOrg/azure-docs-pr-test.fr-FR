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
#  <a name="create-application-insights-resources-using-powershell"></a><span data-ttu-id="88547-103">Créer des ressources Application Insights à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="88547-103">Create Application Insights resources using PowerShell</span></span>
<span data-ttu-id="88547-104">Cet article vous explique comment tooautomate hello la création et la mise à jour de [Application Insights](app-insights-overview.md) ressources automatiquement à l’aide de gestion des ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="88547-104">This article shows you how tooautomate hello creation and update of [Application Insights](app-insights-overview.md) resources automatically by using Azure Resource Management.</span></span> <span data-ttu-id="88547-105">Cette opération peut par exemple avoir lieu dans le cadre du processus de génération.</span><span class="sxs-lookup"><span data-stu-id="88547-105">You might, for example, do so as part of a build process.</span></span> <span data-ttu-id="88547-106">En même temps que la ressource d’Application Insights base hello, vous pouvez créer [disponibilité des tests web](app-insights-monitor-web-app-availability.md), paramétrez les [alertes](app-insights-alerts.md), affectez la valeur hello [tarification schéma](app-insights-pricing.md)et créer d’autres Azure ressources.</span><span class="sxs-lookup"><span data-stu-id="88547-106">Along with hello basic Application Insights resource, you can create [availability web tests](app-insights-monitor-web-app-availability.md), set up [alerts](app-insights-alerts.md), set hello [pricing scheme](app-insights-pricing.md), and create other Azure resources.</span></span>

<span data-ttu-id="88547-107">Hello toocreating clé ces ressources sont des modèles JSON pour [Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="88547-107">hello key toocreating these resources is JSON templates for [Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md).</span></span> <span data-ttu-id="88547-108">En bref, la procédure de hello est : télécharger les définitions de JSON hello des ressources existantes ; paramétrer certaines valeurs telles que les noms ; puis exécutez le modèle de hello chaque fois que vous souhaitez toocreate une nouvelle ressource.</span><span class="sxs-lookup"><span data-stu-id="88547-108">In a nutshell, hello procedure is: download hello JSON definitions of existing resources; parameterize certain values such as names; and then run hello template whenever you want toocreate a new resource.</span></span> <span data-ttu-id="88547-109">Vous pouvez empaqueter d’ensemble de plusieurs ressources, toocreate que les tout en un accédez - par exemple, une analyse de l’application avec les tests de disponibilité, des alertes et de stockage pour l’exportation continue.</span><span class="sxs-lookup"><span data-stu-id="88547-109">You can package several resources together, toocreate them all in one go - for example, an app monitor with availability tests, alerts, and storage for continuous export.</span></span> <span data-ttu-id="88547-110">Il existe certains toosome subtilités de paramétrages hello, que nous aborderons ici.</span><span class="sxs-lookup"><span data-stu-id="88547-110">There are some subtleties toosome of hello parameterizations, which we'll explain here.</span></span>

## <a name="one-time-setup"></a><span data-ttu-id="88547-111">Installation unique</span><span class="sxs-lookup"><span data-stu-id="88547-111">One-time setup</span></span>
<span data-ttu-id="88547-112">Si vous n’avez pas utilisé précédemment PowerShell avec votre abonnement Azure :</span><span class="sxs-lookup"><span data-stu-id="88547-112">If you haven't used PowerShell with your Azure subscription before:</span></span>

<span data-ttu-id="88547-113">Installer le module de Azure Powershell de hello sur ordinateur hello où vous souhaitez les scripts de hello toorun :</span><span class="sxs-lookup"><span data-stu-id="88547-113">Install hello Azure Powershell module on hello machine where you want toorun hello scripts:</span></span>

1. <span data-ttu-id="88547-114">Installez le programme [Microsoft Web Platform Installer (v5 ou version ultérieure)](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="88547-114">Install [Microsoft Web Platform Installer (v5 or higher)](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
2. <span data-ttu-id="88547-115">Utiliser tooinstall Microsoft Azure Powershell.</span><span class="sxs-lookup"><span data-stu-id="88547-115">Use it tooinstall Microsoft Azure Powershell.</span></span>

## <a name="create-an-azure-resource-manager-template"></a><span data-ttu-id="88547-116">Créer un modèle Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="88547-116">Create an Azure Resource Manager template</span></span>
<span data-ttu-id="88547-117">Créez un fichier .json appelé `template1.json` dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="88547-117">Create a new .json file - let's call it `template1.json` in this example.</span></span> <span data-ttu-id="88547-118">Copiez-y ce contenu :</span><span class="sxs-lookup"><span data-stu-id="88547-118">Copy this content into it:</span></span>

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



## <a name="create-application-insights-resources"></a><span data-ttu-id="88547-119">Créer des ressources Application Insights</span><span class="sxs-lookup"><span data-stu-id="88547-119">Create Application Insights resources</span></span>
1. <span data-ttu-id="88547-120">Dans PowerShell, la connexion tooAzure :</span><span class="sxs-lookup"><span data-stu-id="88547-120">In PowerShell, sign in tooAzure:</span></span>
   
    `Login-AzureRmAccount`
2. <span data-ttu-id="88547-121">Exécutez une commande comme suit :</span><span class="sxs-lookup"><span data-stu-id="88547-121">Run a command like this:</span></span>
   
    ```PS
   
        New-AzureRmResourceGroupDeployment -ResourceGroupName Fabrikam `
               -TemplateFile .\template1.json `
               -appName myNewApp

    ``` 
   
   * <span data-ttu-id="88547-122">`-ResourceGroupName`est le groupe de hello où vous souhaitez que les ressources de nouveau toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="88547-122">`-ResourceGroupName` is hello group where you want toocreate hello new resources.</span></span>
   * <span data-ttu-id="88547-123">`-TemplateFile`doit se produire avant les paramètres personnalisés hello.</span><span class="sxs-lookup"><span data-stu-id="88547-123">`-TemplateFile` must occur before hello custom parameters.</span></span>
   * <span data-ttu-id="88547-124">`-appName`nom de Hello de hello ressource toocreate.</span><span class="sxs-lookup"><span data-stu-id="88547-124">`-appName` hello name of hello resource toocreate.</span></span>

<span data-ttu-id="88547-125">Vous pouvez ajouter d’autres paramètres : vous trouverez leur description dans la section des paramètres de modèle de hello hello.</span><span class="sxs-lookup"><span data-stu-id="88547-125">You can add other parameters - you'll find their descriptions in hello parameters section of hello template.</span></span>

## <a name="tooget-hello-instrumentation-key"></a><span data-ttu-id="88547-126">clé d’instrumentation hello tooget</span><span class="sxs-lookup"><span data-stu-id="88547-126">tooget hello instrumentation key</span></span>
<span data-ttu-id="88547-127">Après avoir créé une ressource d’application, vous souhaiterez clé d’instrumentation hello :</span><span class="sxs-lookup"><span data-stu-id="88547-127">After creating an application resource, you'll want hello instrumentation key:</span></span> 

```PS
    $resource = Find-AzureRmResource -ResourceNameEquals "<YOUR APP NAME>" -ResourceType "Microsoft.Insights/components"
    $details = Get-AzureRmResource -ResourceId $resource.ResourceId
    $ikey = $details.Properties.InstrumentationKey
```


<a id="price"></a>
## <a name="set-hello-price-plan"></a><span data-ttu-id="88547-128">Plan de prix hello ensemble</span><span class="sxs-lookup"><span data-stu-id="88547-128">Set hello price plan</span></span>

<span data-ttu-id="88547-129">Vous pouvez définir hello [plan tarifaire](app-insights-pricing.md).</span><span class="sxs-lookup"><span data-stu-id="88547-129">You can set hello [price plan](app-insights-pricing.md).</span></span>

<span data-ttu-id="88547-130">toocreate une ressource d’application avec un plan prix hello entreprise, à l’aide du modèle hello ci-dessus :</span><span class="sxs-lookup"><span data-stu-id="88547-130">toocreate an app resource with hello Enterprise price plan, using hello template above:</span></span>

```PS
        New-AzureRmResourceGroupDeployment -ResourceGroupName Fabrikam `
               -TemplateFile .\template1.json `
               -priceCode 2 `
               -appName myNewApp
```

|<span data-ttu-id="88547-131">priceCode</span><span class="sxs-lookup"><span data-stu-id="88547-131">priceCode</span></span>|<span data-ttu-id="88547-132">Plan</span><span class="sxs-lookup"><span data-stu-id="88547-132">plan</span></span>|
|---|---|
|<span data-ttu-id="88547-133">1</span><span class="sxs-lookup"><span data-stu-id="88547-133">1</span></span>|<span data-ttu-id="88547-134">De base</span><span class="sxs-lookup"><span data-stu-id="88547-134">Basic</span></span>|
|<span data-ttu-id="88547-135">2</span><span class="sxs-lookup"><span data-stu-id="88547-135">2</span></span>|<span data-ttu-id="88547-136">Entreprise</span><span class="sxs-lookup"><span data-stu-id="88547-136">Enterprise</span></span>|

* <span data-ttu-id="88547-137">Si vous ne souhaitez que le plan de prix de base par défaut toouse hello, vous pouvez omettre la ressource de CurrentBillingFeatures hello à partir du modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="88547-137">If you only want toouse hello default Basic price plan, you can omit hello CurrentBillingFeatures resource from hello template.</span></span>
* <span data-ttu-id="88547-138">Si vous souhaitez plan de prix toochange hello après de la ressource de composant hello a été créé, vous pouvez utiliser un modèle qui omet la ressource de « Microsoft.Insights/Components. » hello.</span><span class="sxs-lookup"><span data-stu-id="88547-138">If you want toochange hello price plan after hello component resource has been created, you can use a template that omits hello "microsoft.insights/components" resource.</span></span> <span data-ttu-id="88547-139">En outre, omettez hello `dependsOn` nœud hello facturation des ressources.</span><span class="sxs-lookup"><span data-stu-id="88547-139">Also, omit hello `dependsOn` node from hello billing resource.</span></span> 

<span data-ttu-id="88547-140">tooverify hello du plan de prix mis à jour, examinez le panneau hello « Fonctionnalités + tarification » dans le navigateur de hello.</span><span class="sxs-lookup"><span data-stu-id="88547-140">tooverify hello updated price plan, look at hello "Features+pricing" blade in hello browser.</span></span> <span data-ttu-id="88547-141">**Actualiser l’affichage du navigateur hello** toomake que vous voyez l’état le plus récent hello.</span><span class="sxs-lookup"><span data-stu-id="88547-141">**Refresh hello browser view** toomake sure you see hello latest state.</span></span>



## <a name="add-a-metric-alert"></a><span data-ttu-id="88547-142">Ajouter une alerte métrique</span><span class="sxs-lookup"><span data-stu-id="88547-142">Add a metric alert</span></span>

<span data-ttu-id="88547-143">tooset une alerte de métriques à hello même moment que la ressource de votre application, code fusion similaire à celui-ci dans le fichier de modèle hello :</span><span class="sxs-lookup"><span data-stu-id="88547-143">tooset up a metric alert at hello same time as your app resource, merge code like this into hello template file:</span></span>

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

<span data-ttu-id="88547-144">Lorsque vous appelez le modèle de hello, vous pouvez éventuellement ajouter ce paramètre :</span><span class="sxs-lookup"><span data-stu-id="88547-144">When you invoke hello template, you can optionally add this parameter:</span></span>

    `-responseTime 2`

<span data-ttu-id="88547-145">Bien entendu, vous pouvez paramétrer d’autres champs.</span><span class="sxs-lookup"><span data-stu-id="88547-145">You can of course parameterize other fields.</span></span> 

<span data-ttu-id="88547-146">toofind les noms de type hello et les détails de configuration d’autres règles d’alerte, créez une règle manuellement, puis d’examiner dans [Azure Resource Manager](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="88547-146">toofind out hello type names and configuration details of other alert rules, create a rule manually and then inspect it in [Azure Resource Manager](https://resources.azure.com/).</span></span> 


## <a name="add-an-availability-test"></a><span data-ttu-id="88547-147">Ajouter un test de disponibilité</span><span class="sxs-lookup"><span data-stu-id="88547-147">Add an availability test</span></span>

<span data-ttu-id="88547-148">Cet exemple est pour un test ping (tootest une seule page).</span><span class="sxs-lookup"><span data-stu-id="88547-148">This example is for a ping test (tootest a single page).</span></span>  

<span data-ttu-id="88547-149">**Il existe deux parties** dans un test de disponibilité : test hello lui-même et cette alerte hello qui vous informe des échecs.</span><span class="sxs-lookup"><span data-stu-id="88547-149">**There are two parts** in an availability test: hello test itself, and hello alert that notifies you of failures.</span></span>

<span data-ttu-id="88547-150">Fusion hello après le code dans le fichier de modèle hello qui crée l’application hello.</span><span class="sxs-lookup"><span data-stu-id="88547-150">Merge hello following code into hello template file that creates hello app.</span></span>

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

<span data-ttu-id="88547-151">toodiscover les codes de hello pour d’autres emplacements de test, ou la création de hello tooautomate nombre de tests web plus complexes, créer un exemple manuellement et puis paramétrer code hello à partir de [Azure Resource Manager](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="88547-151">toodiscover hello codes for other test locations, or tooautomate hello creation of more complex web tests, create an example manually and then parameterize hello code from [Azure Resource Manager](https://resources.azure.com/).</span></span>

## <a name="add-more-resources"></a><span data-ttu-id="88547-152">Ajouter des ressources</span><span class="sxs-lookup"><span data-stu-id="88547-152">Add more resources</span></span>

<span data-ttu-id="88547-153">Création de hello tooautomate de toute autre ressource de tout type, créer un exemple manuellement, puis copiez et paramétrer son code à partir de [Azure Resource Manager](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="88547-153">tooautomate hello creation of any other resource of any kind, create an example manually, and then copy and parameterize its code from [Azure Resource Manager](https://resources.azure.com/).</span></span> 

1. <span data-ttu-id="88547-154">Ouvrez [Azure Resource Manager](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="88547-154">Open [Azure Resource Manager](https://resources.azure.com/).</span></span> <span data-ttu-id="88547-155">Naviguer vers le bas dans `subscriptions/resourceGroups/<your resource group>/providers/Microsoft.Insights/components`, tooyour de ressource d’application.</span><span class="sxs-lookup"><span data-stu-id="88547-155">Navigate down through `subscriptions/resourceGroups/<your resource group>/providers/Microsoft.Insights/components`, tooyour application resource.</span></span> 
   
    ![Navigation dans Azure Resource Explorer](./media/app-insights-powershell/01.png)
   
    <span data-ttu-id="88547-157">*Composants* est hello base ressources Application Insights pour l’affichage des applications.</span><span class="sxs-lookup"><span data-stu-id="88547-157">*Components* are hello basic Application Insights resources for displaying applications.</span></span> <span data-ttu-id="88547-158">Il existe des ressources distinctes pour hello associé des règles d’alerte et la disponibilité des tests web.</span><span class="sxs-lookup"><span data-stu-id="88547-158">There are separate resources for hello associated alert rules and availability web tests.</span></span>
2. <span data-ttu-id="88547-159">Hello de copie JSON du composant hello dans l’emplacement approprié de hello dans `template1.json`.</span><span class="sxs-lookup"><span data-stu-id="88547-159">Copy hello JSON of hello component into hello appropriate place in `template1.json`.</span></span>
3. <span data-ttu-id="88547-160">Supprimez les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="88547-160">Delete these properties:</span></span>
   
   * `id`
   * `InstrumentationKey`
   * `CreationDate`
   * `TenantId`
4. <span data-ttu-id="88547-161">Ouvrir des sections de webtests et alertrules hello et copiez hello JSON pour les éléments individuels dans votre modèle.</span><span class="sxs-lookup"><span data-stu-id="88547-161">Open hello webtests and alertrules sections and copy hello JSON for individual items into your template.</span></span> <span data-ttu-id="88547-162">(Ne pas copier à partir des nœuds de webtests ou alertrules hello : accédez aux éléments hello sous eux.)</span><span class="sxs-lookup"><span data-stu-id="88547-162">(Don't copy from hello webtests or alertrules nodes: go into hello items under them.)</span></span>
   
    <span data-ttu-id="88547-163">Chaque test web a une règle d’alerte associée, afin que vous ayez toocopy d'entre eux.</span><span class="sxs-lookup"><span data-stu-id="88547-163">Each web test has an associated alert rule, so you have toocopy both of them.</span></span>
   
    <span data-ttu-id="88547-164">Vous pouvez également inclure des alertes sur des métriques.</span><span class="sxs-lookup"><span data-stu-id="88547-164">You can also include alerts on metrics.</span></span> <span data-ttu-id="88547-165">[Noms de métriques](app-insights-powershell-alerts.md#metric-names).</span><span class="sxs-lookup"><span data-stu-id="88547-165">[Metric names](app-insights-powershell-alerts.md#metric-names).</span></span>
5. <span data-ttu-id="88547-166">Insérez cette ligne dans chaque ressource :</span><span class="sxs-lookup"><span data-stu-id="88547-166">Insert this line in each resource:</span></span>
   
    `"apiVersion": "2015-05-01",`

### <a name="parameterize-hello-template"></a><span data-ttu-id="88547-167">Paramétrer le modèle de hello</span><span class="sxs-lookup"><span data-stu-id="88547-167">Parameterize hello template</span></span>
<span data-ttu-id="88547-168">Vous disposez maintenant des noms spécifiques de hello tooreplace avec des paramètres.</span><span class="sxs-lookup"><span data-stu-id="88547-168">Now you have tooreplace hello specific names with parameters.</span></span> <span data-ttu-id="88547-169">trop[paramétrer un modèle](../azure-resource-manager/resource-group-authoring-templates.md), vous écrivez des expressions à l’aide un [ensemble de fonctions d’assistance](../azure-resource-manager/resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="88547-169">too[parameterize a template](../azure-resource-manager/resource-group-authoring-templates.md), you write expressions using a [set of helper functions](../azure-resource-manager/resource-group-template-functions.md).</span></span> 

<span data-ttu-id="88547-170">Vous ne peut pas paramétrer la partie d’une chaîne, alors utilisez `concat()` toobuild chaînes.</span><span class="sxs-lookup"><span data-stu-id="88547-170">You can't parameterize just part of a string, so use `concat()` toobuild strings.</span></span>

<span data-ttu-id="88547-171">Voici des exemples de substitutions de hello, vous souhaiterez toomake.</span><span class="sxs-lookup"><span data-stu-id="88547-171">Here are examples of hello substitutions you'll want toomake.</span></span> <span data-ttu-id="88547-172">Il existe plusieurs occurrences de chaque substitution.</span><span class="sxs-lookup"><span data-stu-id="88547-172">There are several occurrences of each substitution.</span></span> <span data-ttu-id="88547-173">Il vous en faudra peut-être d’autres dans votre modèle.</span><span class="sxs-lookup"><span data-stu-id="88547-173">You might need others in your template.</span></span> <span data-ttu-id="88547-174">Ces exemples utilisent les paramètres de hello et nous avons défini les variables haut hello du modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="88547-174">These examples use hello parameters and variables we defined at hello top of hello template.</span></span>

| <span data-ttu-id="88547-175">find</span><span class="sxs-lookup"><span data-stu-id="88547-175">find</span></span> | <span data-ttu-id="88547-176">replace with</span><span class="sxs-lookup"><span data-stu-id="88547-176">replace with</span></span> |
| --- | --- |
| `"hidden-link:/subscriptions/.../components/MyAppName"` |`"[concat('hidden-link:',`<br/>` resourceId('microsoft.insights/components',` <br/> ` parameters('appName')))]"` |
| `"/subscriptions/.../alertrules/myAlertName-myAppName-subsId",` |`"[resourceId('Microsoft.Insights/alertrules', variables('alertRuleName'))]",` |
| `"/subscriptions/.../webtests/myTestName-myAppName",` |`"[resourceId('Microsoft.Insights/webtests', parameters('webTestName'))]",` |
| `"myWebTest-myAppName"` |`"[variables(testName)]"'` |
| `"myTestName-myAppName-subsId"` |`"[variables('alertRuleName')]"` |
| `"myAppName"` |`"[parameters('appName')]"` |
| <span data-ttu-id="88547-177">`"myappname"` (minuscules)</span><span class="sxs-lookup"><span data-stu-id="88547-177">`"myappname"` (lower case)</span></span> |`"[toLower(parameters('appName'))]"` |
| `"<WebTest Name=\"myWebTest\" ...`<br/>` Url=\"http://fabrikam.com/home\" ...>"` |`[concat('<WebTest Name=\"',` <br/> `parameters('webTestName'),` <br/> `'\" ... Url=\"', parameters('Url'),` <br/> `'\"...>')]"`<br/><span data-ttu-id="88547-178">Supprimez le GUID et l’ID.</span><span class="sxs-lookup"><span data-stu-id="88547-178">Delete Guid and Id.</span></span> |

### <a name="set-dependencies-between-hello-resources"></a><span data-ttu-id="88547-179">Définition de relations entre les ressources hello</span><span class="sxs-lookup"><span data-stu-id="88547-179">Set dependencies between hello resources</span></span>
<span data-ttu-id="88547-180">Configurez Azure ressources hello dans un ordre strict.</span><span class="sxs-lookup"><span data-stu-id="88547-180">Azure should set up hello resources in strict order.</span></span> <span data-ttu-id="88547-181">toomake assurer un paramétrage se termine avant que hello commence ensuite, ajoutez les lignes de dépendance :</span><span class="sxs-lookup"><span data-stu-id="88547-181">toomake sure one setup completes before hello next begins, add dependency lines:</span></span>

* <span data-ttu-id="88547-182">Ressource de test de disponibilité de hello :</span><span class="sxs-lookup"><span data-stu-id="88547-182">In hello availability test resource:</span></span>
  
    `"dependsOn": ["[resourceId('Microsoft.Insights/components', parameters('appName'))]"],`
* <span data-ttu-id="88547-183">Dans la ressource d’alerte hello pour un test de disponibilité :</span><span class="sxs-lookup"><span data-stu-id="88547-183">In hello alert resource for an availability test:</span></span>
  
    `"dependsOn": ["[resourceId('Microsoft.Insights/webtests', variables('testName'))]"],`



## <a name="next-steps"></a><span data-ttu-id="88547-184">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="88547-184">Next steps</span></span>
<span data-ttu-id="88547-185">Autres articles sur l’automation :</span><span class="sxs-lookup"><span data-stu-id="88547-185">Other automation articles:</span></span>

* <span data-ttu-id="88547-186">[Création d'une ressource Application Insights](app-insights-powershell-script-create-resource.md) - méthode rapide sans utiliser de modèle.</span><span class="sxs-lookup"><span data-stu-id="88547-186">[Create an Application Insights resource](app-insights-powershell-script-create-resource.md) - quick method without using a template.</span></span>
* [<span data-ttu-id="88547-187">Configurer des alertes</span><span class="sxs-lookup"><span data-stu-id="88547-187">Set up Alerts</span></span>](app-insights-powershell-alerts.md)
* [<span data-ttu-id="88547-188">Créer des tests web</span><span class="sxs-lookup"><span data-stu-id="88547-188">Create web tests</span></span>](https://azure.microsoft.com/blog/creating-a-web-test-alert-programmatically-with-application-insights/)
* [<span data-ttu-id="88547-189">Envoyer des Diagnostics Windows Azure tooApplication Insights</span><span class="sxs-lookup"><span data-stu-id="88547-189">Send Azure Diagnostics tooApplication Insights</span></span>](app-insights-powershell-azure-diagnostics.md)
* [<span data-ttu-id="88547-190">Déployer tooAzure à partir de GitHub</span><span class="sxs-lookup"><span data-stu-id="88547-190">Deploy tooAzure from GitHub</span></span>](http://blogs.msdn.com/b/webdev/archive/2015/09/16/deploy-to-azure-from-github-with-application-insights.aspx)
* [<span data-ttu-id="88547-191">Créer des annotations de version</span><span class="sxs-lookup"><span data-stu-id="88547-191">Create release annotations</span></span>](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/API/CreateReleaseAnnotation.ps1)

