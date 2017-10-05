---
title: Automatiser Azure Application Insights avec PowerShell | Microsoft Docs
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
ms.openlocfilehash: 88dbb9515300f847789bc889911cdeff5f5bdb53
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
#  <a name="create-application-insights-resources-using-powershell"></a><span data-ttu-id="4a430-103">Créer des ressources Application Insights à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="4a430-103">Create Application Insights resources using PowerShell</span></span>
<span data-ttu-id="4a430-104">Cet article explique comment automatiser la création et la mise à jour de ressources [Application Insights](app-insights-overview.md) à l’aide du service de gestion des ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="4a430-104">This article shows you how to automate the creation and update of [Application Insights](app-insights-overview.md) resources automatically by using Azure Resource Management.</span></span> <span data-ttu-id="4a430-105">Cette opération peut par exemple avoir lieu dans le cadre du processus de génération.</span><span class="sxs-lookup"><span data-stu-id="4a430-105">You might, for example, do so as part of a build process.</span></span> <span data-ttu-id="4a430-106">Avec la ressource Application Insights de base, vous pouvez créer des [tests web de disponibilité](app-insights-monitor-web-app-availability.md), configurer [des alertes](app-insights-alerts.md) et un [mécanisme de tarification](app-insights-pricing.md), mais aussi créer d’autres ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="4a430-106">Along with the basic Application Insights resource, you can create [availability web tests](app-insights-monitor-web-app-availability.md), set up [alerts](app-insights-alerts.md), set the [pricing scheme](app-insights-pricing.md), and create other Azure resources.</span></span>

<span data-ttu-id="4a430-107">Les éléments importants pour la création de ces ressources sont les modèles JSON pour [Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="4a430-107">The key to creating these resources is JSON templates for [Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md).</span></span> <span data-ttu-id="4a430-108">En bref, la procédure est la suivante : téléchargez les définitions JSON des ressources existantes, paramétrez certaines valeurs telles que les noms, puis exécutez le modèle chaque fois que vous souhaitez créer une nouvelle ressource.</span><span class="sxs-lookup"><span data-stu-id="4a430-108">In a nutshell, the procedure is: download the JSON definitions of existing resources; parameterize certain values such as names; and then run the template whenever you want to create a new resource.</span></span> <span data-ttu-id="4a430-109">Vous pouvez regrouper plusieurs ressources pour les créer en une fois, par exemple une analyse d’application avec des tests de disponibilité, des alertes et le stockage pour l’exportation continue.</span><span class="sxs-lookup"><span data-stu-id="4a430-109">You can package several resources together, to create them all in one go - for example, an app monitor with availability tests, alerts, and storage for continuous export.</span></span> <span data-ttu-id="4a430-110">Certains paramètres ont des particularités que nous aborderons ici.</span><span class="sxs-lookup"><span data-stu-id="4a430-110">There are some subtleties to some of the parameterizations, which we'll explain here.</span></span>

## <a name="one-time-setup"></a><span data-ttu-id="4a430-111">Installation unique</span><span class="sxs-lookup"><span data-stu-id="4a430-111">One-time setup</span></span>
<span data-ttu-id="4a430-112">Si vous n’avez pas utilisé précédemment PowerShell avec votre abonnement Azure :</span><span class="sxs-lookup"><span data-stu-id="4a430-112">If you haven't used PowerShell with your Azure subscription before:</span></span>

<span data-ttu-id="4a430-113">Installez le module Azure Powershell sur l’ordinateur sur lequel vous souhaitez exécuter les scripts :</span><span class="sxs-lookup"><span data-stu-id="4a430-113">Install the Azure Powershell module on the machine where you want to run the scripts:</span></span>

1. <span data-ttu-id="4a430-114">Installez le programme [Microsoft Web Platform Installer (v5 ou version ultérieure)](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="4a430-114">Install [Microsoft Web Platform Installer (v5 or higher)](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
2. <span data-ttu-id="4a430-115">Utilisez-le pour installer Microsoft Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4a430-115">Use it to install Microsoft Azure Powershell.</span></span>

## <a name="create-an-azure-resource-manager-template"></a><span data-ttu-id="4a430-116">Créer un modèle Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4a430-116">Create an Azure Resource Manager template</span></span>
<span data-ttu-id="4a430-117">Créez un fichier .json appelé `template1.json` dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="4a430-117">Create a new .json file - let's call it `template1.json` in this example.</span></span> <span data-ttu-id="4a430-118">Copiez-y ce contenu :</span><span class="sxs-lookup"><span data-stu-id="4a430-118">Copy this content into it:</span></span>

```JSON
    {
        "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "appName": {
                "type": "string",
                "metadata": {
                    "description": "Enter the application name."
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
                    "description": "Enter the application type."
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
                    "description": "Enter the application location."
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
                    "description": "Enter daily quota reset hour in UTC (0 to 23). Values outside the range will get a random reset hour."
                }
            },
            "warningThreshold": {
                "type": "int",
                "defaultValue": 90,
                "minValue": 1,
                "maxValue": 100,
                "metadata": {
                    "description": "Enter the % value of daily quota after which warning mail to be sent. "
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



## <a name="create-application-insights-resources"></a><span data-ttu-id="4a430-119">Créer des ressources Application Insights</span><span class="sxs-lookup"><span data-stu-id="4a430-119">Create Application Insights resources</span></span>
1. <span data-ttu-id="4a430-120">Dans PowerShell, connectez-vous à Azure :</span><span class="sxs-lookup"><span data-stu-id="4a430-120">In PowerShell, sign in to Azure:</span></span>
   
    `Login-AzureRmAccount`
2. <span data-ttu-id="4a430-121">Exécutez une commande comme suit :</span><span class="sxs-lookup"><span data-stu-id="4a430-121">Run a command like this:</span></span>
   
    ```PS
   
        New-AzureRmResourceGroupDeployment -ResourceGroupName Fabrikam `
               -TemplateFile .\template1.json `
               -appName myNewApp

    ``` 
   
   * <span data-ttu-id="4a430-122">`-ResourceGroupName` est le groupe dans lequel vous souhaitez créer les nouvelles ressources.</span><span class="sxs-lookup"><span data-stu-id="4a430-122">`-ResourceGroupName` is the group where you want to create the new resources.</span></span>
   * <span data-ttu-id="4a430-123">`-TemplateFile` doit se produire avant les paramètres personnalisés.</span><span class="sxs-lookup"><span data-stu-id="4a430-123">`-TemplateFile` must occur before the custom parameters.</span></span>
   * <span data-ttu-id="4a430-124">`-appName` est le nom de la ressource à créer.</span><span class="sxs-lookup"><span data-stu-id="4a430-124">`-appName` The name of the resource to create.</span></span>

<span data-ttu-id="4a430-125">Vous pouvez ajouter d’autres paramètres. Vous trouverez leurs descriptions dans la section Paramètres du modèle.</span><span class="sxs-lookup"><span data-stu-id="4a430-125">You can add other parameters - you'll find their descriptions in the parameters section of the template.</span></span>

## <a name="to-get-the-instrumentation-key"></a><span data-ttu-id="4a430-126">Pour récupérer la clé d’instrumentation</span><span class="sxs-lookup"><span data-stu-id="4a430-126">To get the instrumentation key</span></span>
<span data-ttu-id="4a430-127">Après avoir créé une ressource d’application, vous voulez obtenir la clé d’instrumentation :</span><span class="sxs-lookup"><span data-stu-id="4a430-127">After creating an application resource, you'll want the instrumentation key:</span></span> 

```PS
    $resource = Find-AzureRmResource -ResourceNameEquals "<YOUR APP NAME>" -ResourceType "Microsoft.Insights/components"
    $details = Get-AzureRmResource -ResourceId $resource.ResourceId
    $ikey = $details.Properties.InstrumentationKey
```


<a id="price"></a>
## <a name="set-the-price-plan"></a><span data-ttu-id="4a430-128">Définition d’un plan tarifaire</span><span class="sxs-lookup"><span data-stu-id="4a430-128">Set the price plan</span></span>

<span data-ttu-id="4a430-129">Vous pouvez définir le [plan tarifaire](app-insights-pricing.md).</span><span class="sxs-lookup"><span data-stu-id="4a430-129">You can set the [price plan](app-insights-pricing.md).</span></span>

<span data-ttu-id="4a430-130">Pour créer une ressource d’application avec le plan de tarification Entreprise à l’aide du modèle ci-dessus :</span><span class="sxs-lookup"><span data-stu-id="4a430-130">To create an app resource with the Enterprise price plan, using the template above:</span></span>

```PS
        New-AzureRmResourceGroupDeployment -ResourceGroupName Fabrikam `
               -TemplateFile .\template1.json `
               -priceCode 2 `
               -appName myNewApp
```

|<span data-ttu-id="4a430-131">priceCode</span><span class="sxs-lookup"><span data-stu-id="4a430-131">priceCode</span></span>|<span data-ttu-id="4a430-132">Plan</span><span class="sxs-lookup"><span data-stu-id="4a430-132">plan</span></span>|
|---|---|
|<span data-ttu-id="4a430-133">1</span><span class="sxs-lookup"><span data-stu-id="4a430-133">1</span></span>|<span data-ttu-id="4a430-134">De base</span><span class="sxs-lookup"><span data-stu-id="4a430-134">Basic</span></span>|
|<span data-ttu-id="4a430-135">2</span><span class="sxs-lookup"><span data-stu-id="4a430-135">2</span></span>|<span data-ttu-id="4a430-136">Entreprise</span><span class="sxs-lookup"><span data-stu-id="4a430-136">Enterprise</span></span>|

* <span data-ttu-id="4a430-137">Si vous souhaitez simplement utiliser le plan tarifaire de base par défaut, vous pouvez omettre la ressource CurrentBillingFeatures du modèle.</span><span class="sxs-lookup"><span data-stu-id="4a430-137">If you only want to use the default Basic price plan, you can omit the CurrentBillingFeatures resource from the template.</span></span>
* <span data-ttu-id="4a430-138">Si vous voulez changer de forfait après avoir créé la ressource de composant, vous pouvez utiliser un modèle qui omet la ressource « microsoft.insights/components. ».</span><span class="sxs-lookup"><span data-stu-id="4a430-138">If you want to change the price plan after the component resource has been created, you can use a template that omits the "microsoft.insights/components" resource.</span></span> <span data-ttu-id="4a430-139">Omettez aussi le nœud `dependsOn` dans la ressource de facturation.</span><span class="sxs-lookup"><span data-stu-id="4a430-139">Also, omit the `dependsOn` node from the billing resource.</span></span> 

<span data-ttu-id="4a430-140">Pour vérifier le forfait mis à jour, examinez le panneau « Fonctionnalités + tarification » dans le navigateur.</span><span class="sxs-lookup"><span data-stu-id="4a430-140">To verify the updated price plan, look at the "Features+pricing" blade in the browser.</span></span> <span data-ttu-id="4a430-141">**Actualisez l’affichage du navigateur** pour voir l’état le plus récent.</span><span class="sxs-lookup"><span data-stu-id="4a430-141">**Refresh the browser view** to make sure you see the latest state.</span></span>



## <a name="add-a-metric-alert"></a><span data-ttu-id="4a430-142">Ajouter une alerte métrique</span><span class="sxs-lookup"><span data-stu-id="4a430-142">Add a metric alert</span></span>

<span data-ttu-id="4a430-143">Pour configurer une alerte de métrique en même temps que votre ressource d’application, fusionnez le code comme suit dans le fichier de modèle :</span><span class="sxs-lookup"><span data-stu-id="4a430-143">To set up a metric alert at the same time as your app resource, merge code like this into the template file:</span></span>

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
      // Ensure this resource is created after the app resource:
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

<span data-ttu-id="4a430-144">Lorsque vous appelez le modèle, vous pouvez éventuellement ajouter ce paramètre :</span><span class="sxs-lookup"><span data-stu-id="4a430-144">When you invoke the template, you can optionally add this parameter:</span></span>

    `-responseTime 2`

<span data-ttu-id="4a430-145">Bien entendu, vous pouvez paramétrer d’autres champs.</span><span class="sxs-lookup"><span data-stu-id="4a430-145">You can of course parameterize other fields.</span></span> 

<span data-ttu-id="4a430-146">Pour rechercher les noms de type et les détails de configuration d’autres règles d’alerte, créez une règle manuellement et examinez-la dans [Azure Resource Manager](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="4a430-146">To find out the type names and configuration details of other alert rules, create a rule manually and then inspect it in [Azure Resource Manager](https://resources.azure.com/).</span></span> 


## <a name="add-an-availability-test"></a><span data-ttu-id="4a430-147">Ajouter un test de disponibilité</span><span class="sxs-lookup"><span data-stu-id="4a430-147">Add an availability test</span></span>

<span data-ttu-id="4a430-148">Cet exemple concerne un test Ping (pour tester une seule page).</span><span class="sxs-lookup"><span data-stu-id="4a430-148">This example is for a ping test (to test a single page).</span></span>  

<span data-ttu-id="4a430-149">**Il existe deux parties** dans un test de disponibilité : le test lui-même et l’alerte qui vous informe des échecs.</span><span class="sxs-lookup"><span data-stu-id="4a430-149">**There are two parts** in an availability test: the test itself, and the alert that notifies you of failures.</span></span>

<span data-ttu-id="4a430-150">Fusionnez le code suivant dans le fichier de modèle qui crée l’application.</span><span class="sxs-lookup"><span data-stu-id="4a430-150">Merge the following code into the template file that creates the app.</span></span>

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
      // Availability test: part 1 configures the test
      //
      "name": "[variables('pingTestName')]",
      "type": "Microsoft.Insights/webtests",
      "apiVersion": "2014-04-01",
      "location": "[parameters('appLocation')]",
      // Ensure this is created after the app resource:
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
          "WebTest": "[concat('<WebTest   Name=\"', variables('pingTestName'), '\"   Enabled=\"True\"         CssProjectStructure=\"\"    CssIteration=\"\"  Timeout=\"120\"  WorkItemIds=\"\"         xmlns=\"http://microsoft.com/schemas/VisualStudio/TeamTest/2010\"         Description=\"\"  CredentialUserName=\"\"  CredentialPassword=\"\"         PreAuthenticate=\"True\"  Proxy=\"default\"  StopOnError=\"False\"         RecordedResultFile=\"\"  ResultsLocale=\"\">  <Items>  <Request Method=\"GET\"    Version=\"1.1\"  Url=\"', parameters('Url'),   '\" ThinkTime=\"0\"  Timeout=\"300\" ParseDependentRequests=\"True\"         FollowRedirects=\"True\" RecordResult=\"True\" Cache=\"False\"         ResponseTimeGoal=\"0\"  Encoding=\"utf-8\"  ExpectedHttpStatusCode=\"200\"         ExpectedResponseUrl=\"\" ReportingName=\"\" IgnoreHttpStatusCode=\"False\" />        </Items>  <ValidationRules> <ValidationRule  Classname=\"Microsoft.VisualStudio.TestTools.WebTesting.Rules.ValidationRuleFindText, Microsoft.VisualStudio.QualityTools.WebTestFramework, Version=10.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a\" DisplayName=\"Find Text\"         Description=\"Verifies the existence of the specified text in the response.\"         Level=\"High\"  ExectuionOrder=\"BeforeDependents\">  <RuleParameters>        <RuleParameter Name=\"FindText\" Value=\"',   parameters('pingText'), '\" />  <RuleParameter Name=\"IgnoreCase\" Value=\"False\" />  <RuleParameter Name=\"UseRegularExpression\" Value=\"False\" />  <RuleParameter Name=\"PassIfTextFound\" Value=\"True\" />  </RuleParameters> </ValidationRule>  </ValidationRules>  </WebTest>')]"
        },
        "SyntheticMonitorId": "[variables('pingTestName')]"
      }
    },

    {
      //
      // Availability test: part 2, the alert rule
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

<span data-ttu-id="4a430-151">Pour découvrir les codes pour d’autres emplacements de test ou pour automatiser la création de tests web plus complexes, créez un exemple manuellement, puis paramétrez ensuite le code à partir [d’Azure Resource Manager](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="4a430-151">To discover the codes for other test locations, or to automate the creation of more complex web tests, create an example manually and then parameterize the code from [Azure Resource Manager](https://resources.azure.com/).</span></span>

## <a name="add-more-resources"></a><span data-ttu-id="4a430-152">Ajouter des ressources</span><span class="sxs-lookup"><span data-stu-id="4a430-152">Add more resources</span></span>

<span data-ttu-id="4a430-153">Pour automatiser la création de toute autre ressource de tout type, créez un exemple manuellement, puis copiez-le et paramétrez son code à partir [d’Azure Resource Manager](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="4a430-153">To automate the creation of any other resource of any kind, create an example manually, and then copy and parameterize its code from [Azure Resource Manager](https://resources.azure.com/).</span></span> 

1. <span data-ttu-id="4a430-154">Ouvrez [Azure Resource Manager](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="4a430-154">Open [Azure Resource Manager](https://resources.azure.com/).</span></span> <span data-ttu-id="4a430-155">Accédez à votre ressource d’application qui se trouve après `subscriptions/resourceGroups/<your resource group>/providers/Microsoft.Insights/components`.</span><span class="sxs-lookup"><span data-stu-id="4a430-155">Navigate down through `subscriptions/resourceGroups/<your resource group>/providers/Microsoft.Insights/components`, to your application resource.</span></span> 
   
    ![Navigation dans Azure Resource Explorer](./media/app-insights-powershell/01.png)
   
    <span data-ttu-id="4a430-157">*composants* sont les ressources Application Insights de base pour l’affichage des applications.</span><span class="sxs-lookup"><span data-stu-id="4a430-157">*Components* are the basic Application Insights resources for displaying applications.</span></span> <span data-ttu-id="4a430-158">Il existe des ressources distinctes pour les règles d’alertes et les tests web de disponibilité associés.</span><span class="sxs-lookup"><span data-stu-id="4a430-158">There are separate resources for the associated alert rules and availability web tests.</span></span>
2. <span data-ttu-id="4a430-159">Copiez le JSON du composant dans l’emplacement approprié dans `template1.json`.</span><span class="sxs-lookup"><span data-stu-id="4a430-159">Copy the JSON of the component into the appropriate place in `template1.json`.</span></span>
3. <span data-ttu-id="4a430-160">Supprimez les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="4a430-160">Delete these properties:</span></span>
   
   * `id`
   * `InstrumentationKey`
   * `CreationDate`
   * `TenantId`
4. <span data-ttu-id="4a430-161">Ouvrez les sections webtests et alertrules et copiez le JSON pour des éléments individuels dans votre modèle.</span><span class="sxs-lookup"><span data-stu-id="4a430-161">Open the webtests and alertrules sections and copy the JSON for individual items into your template.</span></span> <span data-ttu-id="4a430-162">(Ne copiez pas à partir des nœuds webtests ou alertrules : accédez aux éléments sous-jacents.)</span><span class="sxs-lookup"><span data-stu-id="4a430-162">(Don't copy from the webtests or alertrules nodes: go into the items under them.)</span></span>
   
    <span data-ttu-id="4a430-163">Chaque test web étant associé à une règle d’alerte, vous devez copier les deux.</span><span class="sxs-lookup"><span data-stu-id="4a430-163">Each web test has an associated alert rule, so you have to copy both of them.</span></span>
   
    <span data-ttu-id="4a430-164">Vous pouvez également inclure des alertes sur des métriques.</span><span class="sxs-lookup"><span data-stu-id="4a430-164">You can also include alerts on metrics.</span></span> <span data-ttu-id="4a430-165">[Noms de métriques](app-insights-powershell-alerts.md#metric-names).</span><span class="sxs-lookup"><span data-stu-id="4a430-165">[Metric names](app-insights-powershell-alerts.md#metric-names).</span></span>
5. <span data-ttu-id="4a430-166">Insérez cette ligne dans chaque ressource :</span><span class="sxs-lookup"><span data-stu-id="4a430-166">Insert this line in each resource:</span></span>
   
    `"apiVersion": "2015-05-01",`

### <a name="parameterize-the-template"></a><span data-ttu-id="4a430-167">Définir les paramètres du modèle</span><span class="sxs-lookup"><span data-stu-id="4a430-167">Parameterize the template</span></span>
<span data-ttu-id="4a430-168">Vous devez à présent remplacer les noms spécifiques par des paramètres.</span><span class="sxs-lookup"><span data-stu-id="4a430-168">Now you have to replace the specific names with parameters.</span></span> <span data-ttu-id="4a430-169">Pour [définir les paramètres d’un modèle](../azure-resource-manager/resource-group-authoring-templates.md), écrivez des expressions utilisant un [ensemble de fonctions d’assistance](../azure-resource-manager/resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="4a430-169">To [parameterize a template](../azure-resource-manager/resource-group-authoring-templates.md), you write expressions using a [set of helper functions](../azure-resource-manager/resource-group-template-functions.md).</span></span> 

<span data-ttu-id="4a430-170">Comme vous ne pouvez pas définir uniquement les paramètres d’une portion de chaîne, utilisez `concat()` pour générer les chaînes.</span><span class="sxs-lookup"><span data-stu-id="4a430-170">You can't parameterize just part of a string, so use `concat()` to build strings.</span></span>

<span data-ttu-id="4a430-171">Voici des exemples de substitutions que vous allez effectuer.</span><span class="sxs-lookup"><span data-stu-id="4a430-171">Here are examples of the substitutions you'll want to make.</span></span> <span data-ttu-id="4a430-172">Il existe plusieurs occurrences de chaque substitution.</span><span class="sxs-lookup"><span data-stu-id="4a430-172">There are several occurrences of each substitution.</span></span> <span data-ttu-id="4a430-173">Il vous en faudra peut-être d’autres dans votre modèle.</span><span class="sxs-lookup"><span data-stu-id="4a430-173">You might need others in your template.</span></span> <span data-ttu-id="4a430-174">Ces exemples utilisent les paramètres et les variables que nous avons définis en haut du modèle.</span><span class="sxs-lookup"><span data-stu-id="4a430-174">These examples use the parameters and variables we defined at the top of the template.</span></span>

| <span data-ttu-id="4a430-175">find</span><span class="sxs-lookup"><span data-stu-id="4a430-175">find</span></span> | <span data-ttu-id="4a430-176">replace with</span><span class="sxs-lookup"><span data-stu-id="4a430-176">replace with</span></span> |
| --- | --- |
| `"hidden-link:/subscriptions/.../components/MyAppName"` |`"[concat('hidden-link:',`<br/>` resourceId('microsoft.insights/components',` <br/> ` parameters('appName')))]"` |
| `"/subscriptions/.../alertrules/myAlertName-myAppName-subsId",` |`"[resourceId('Microsoft.Insights/alertrules', variables('alertRuleName'))]",` |
| `"/subscriptions/.../webtests/myTestName-myAppName",` |`"[resourceId('Microsoft.Insights/webtests', parameters('webTestName'))]",` |
| `"myWebTest-myAppName"` |`"[variables(testName)]"'` |
| `"myTestName-myAppName-subsId"` |`"[variables('alertRuleName')]"` |
| `"myAppName"` |`"[parameters('appName')]"` |
| <span data-ttu-id="4a430-177">`"myappname"` (minuscules)</span><span class="sxs-lookup"><span data-stu-id="4a430-177">`"myappname"` (lower case)</span></span> |`"[toLower(parameters('appName'))]"` |
| `"<WebTest Name=\"myWebTest\" ...`<br/>` Url=\"http://fabrikam.com/home\" ...>"` |`[concat('<WebTest Name=\"',` <br/> `parameters('webTestName'),` <br/> `'\" ... Url=\"', parameters('Url'),` <br/> `'\"...>')]"`<br/><span data-ttu-id="4a430-178">Supprimez le GUID et l’ID.</span><span class="sxs-lookup"><span data-stu-id="4a430-178">Delete Guid and Id.</span></span> |

### <a name="set-dependencies-between-the-resources"></a><span data-ttu-id="4a430-179">Définir les dépendances entre les ressources</span><span class="sxs-lookup"><span data-stu-id="4a430-179">Set dependencies between the resources</span></span>
<span data-ttu-id="4a430-180">Azure doit configurer les ressources dans un ordre strict.</span><span class="sxs-lookup"><span data-stu-id="4a430-180">Azure should set up the resources in strict order.</span></span> <span data-ttu-id="4a430-181">Pour vous assurer de l’achèvement d’une installation avant que la suivante ne commence, ajoutez les lignes de dépendance :</span><span class="sxs-lookup"><span data-stu-id="4a430-181">To make sure one setup completes before the next begins, add dependency lines:</span></span>

* <span data-ttu-id="4a430-182">Dans la ressource du test de disponibilité :</span><span class="sxs-lookup"><span data-stu-id="4a430-182">In the availability test resource:</span></span>
  
    `"dependsOn": ["[resourceId('Microsoft.Insights/components', parameters('appName'))]"],`
* <span data-ttu-id="4a430-183">Dans la ressource d’alerte pour un test de disponibilité :</span><span class="sxs-lookup"><span data-stu-id="4a430-183">In the alert resource for an availability test:</span></span>
  
    `"dependsOn": ["[resourceId('Microsoft.Insights/webtests', variables('testName'))]"],`



## <a name="next-steps"></a><span data-ttu-id="4a430-184">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4a430-184">Next steps</span></span>
<span data-ttu-id="4a430-185">Autres articles sur l’automation :</span><span class="sxs-lookup"><span data-stu-id="4a430-185">Other automation articles:</span></span>

* <span data-ttu-id="4a430-186">[Création d'une ressource Application Insights](app-insights-powershell-script-create-resource.md) - méthode rapide sans utiliser de modèle.</span><span class="sxs-lookup"><span data-stu-id="4a430-186">[Create an Application Insights resource](app-insights-powershell-script-create-resource.md) - quick method without using a template.</span></span>
* [<span data-ttu-id="4a430-187">Configurer des alertes</span><span class="sxs-lookup"><span data-stu-id="4a430-187">Set up Alerts</span></span>](app-insights-powershell-alerts.md)
* [<span data-ttu-id="4a430-188">Créer des tests web</span><span class="sxs-lookup"><span data-stu-id="4a430-188">Create web tests</span></span>](https://azure.microsoft.com/blog/creating-a-web-test-alert-programmatically-with-application-insights/)
* [<span data-ttu-id="4a430-189">Envoyer des diagnostics Azure vers Application Insights.</span><span class="sxs-lookup"><span data-stu-id="4a430-189">Send Azure Diagnostics to Application Insights</span></span>](app-insights-powershell-azure-diagnostics.md)
* [<span data-ttu-id="4a430-190">Déployer sur Azure à partir de GitHub</span><span class="sxs-lookup"><span data-stu-id="4a430-190">Deploy to Azure from GitHub</span></span>](http://blogs.msdn.com/b/webdev/archive/2015/09/16/deploy-to-azure-from-github-with-application-insights.aspx)
* [<span data-ttu-id="4a430-191">Créer des annotations de version</span><span class="sxs-lookup"><span data-stu-id="4a430-191">Create release annotations</span></span>](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/API/CreateReleaseAnnotation.ps1)

