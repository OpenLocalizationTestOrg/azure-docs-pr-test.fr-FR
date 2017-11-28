---
title: "aaaProvision une application web qui utilise une base de données SQL"
description: "Utilisez un toodeploy de modèle une application web qui inclut une base de données SQL Azure Resource Manager."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: fb9648e1-9bf2-4537-bc4a-ab8d4953168c
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2016
ms.author: cephalin
ms.openlocfilehash: 189c0122d201e88f15013bf241d66652ef23df4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="provision-a-web-app-with-a-sql-database"></a><span data-ttu-id="979ae-103">Mettre en service une application Web avec une base de données SQL</span><span class="sxs-lookup"><span data-stu-id="979ae-103">Provision a web app with a SQL Database</span></span>
<span data-ttu-id="979ae-104">Dans cette rubrique, vous allez apprendre comment toocreate un modèle Azure Resource Manager qui déploie une application web et la base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="979ae-104">In this topic, you will learn how toocreate an Azure Resource Manager template that deploys a web app and SQL Database.</span></span> <span data-ttu-id="979ae-105">Vous allez apprendre comment toodefine les ressources qui sont déployés et comment les paramètres toodefine sont spécifiés lorsque le déploiement de hello est exécutée.</span><span class="sxs-lookup"><span data-stu-id="979ae-105">You will learn how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="979ae-106">Vous pouvez utiliser ce modèle pour vos propres déploiements, ou personnaliser toomeet vos besoins.</span><span class="sxs-lookup"><span data-stu-id="979ae-106">You can use this template for your own deployments, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="979ae-107">Pour en savoir plus sur la création de modèles, voir [Création de modèles Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="979ae-107">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="979ae-108">Pour plus d'informations sur le déploiement d'applications, consultez la rubrique [Déployer une application complexe de manière prévisible dans Microsoft Azure](app-service-deploy-complex-application-predictably.md).</span><span class="sxs-lookup"><span data-stu-id="979ae-108">For more information about deploying apps, see [Deploy a complex application predictably in Azure](app-service-deploy-complex-application-predictably.md).</span></span>

<span data-ttu-id="979ae-109">Pour le modèle complète de hello, consultez [modèle d’application Web avec SQL Database](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-sql-database/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="979ae-109">For hello complete template, see [Web App With SQL Database template](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-sql-database/azuredeploy.json).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="what-you-will-deploy"></a><span data-ttu-id="979ae-110">Ce que vous allez déployer</span><span class="sxs-lookup"><span data-stu-id="979ae-110">What you will deploy</span></span>
<span data-ttu-id="979ae-111">Dans ce modèle, vous allez déployer :</span><span class="sxs-lookup"><span data-stu-id="979ae-111">In this template, you will deploy:</span></span>

* <span data-ttu-id="979ae-112">une application Web</span><span class="sxs-lookup"><span data-stu-id="979ae-112">a web app</span></span>
* <span data-ttu-id="979ae-113">Serveur de base de données SQL</span><span class="sxs-lookup"><span data-stu-id="979ae-113">SQL Database server</span></span>
* <span data-ttu-id="979ae-114">Base de données SQL</span><span class="sxs-lookup"><span data-stu-id="979ae-114">SQL Database</span></span>
* <span data-ttu-id="979ae-115">Paramètres de mise à l'échelle automatique</span><span class="sxs-lookup"><span data-stu-id="979ae-115">AutoScale settings</span></span>
* <span data-ttu-id="979ae-116">Règles d'alerte</span><span class="sxs-lookup"><span data-stu-id="979ae-116">Alert rules</span></span>
* <span data-ttu-id="979ae-117">App Insights</span><span class="sxs-lookup"><span data-stu-id="979ae-117">App Insights</span></span>

<span data-ttu-id="979ae-118">toorun hello déploiement automatiquement, cliquez sur hello suivant bouton :</span><span class="sxs-lookup"><span data-stu-id="979ae-118">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="979ae-119">[![Déployer tooAzure](./media/app-service-web-arm-with-sql-database-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-sql-database%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="979ae-119">[![Deploy tooAzure](./media/app-service-web-arm-with-sql-database-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-sql-database%2Fazuredeploy.json)</span></span>

## <a name="parameters-toospecify"></a><span data-ttu-id="979ae-120">Paramètres toospecify</span><span class="sxs-lookup"><span data-stu-id="979ae-120">Parameters toospecify</span></span>
[!INCLUDE [app-service-web-deploy-web-parameters](../../includes/app-service-web-deploy-web-parameters.md)]

### <a name="administratorlogin"></a><span data-ttu-id="979ae-121">administratorLogin</span><span class="sxs-lookup"><span data-stu-id="979ae-121">administratorLogin</span></span>
<span data-ttu-id="979ae-122">Bonjour toouse de nom de compte d’administrateur de serveur de base de données hello.</span><span class="sxs-lookup"><span data-stu-id="979ae-122">hello account name toouse for hello database server administrator.</span></span>

    "administratorLogin": {
      "type": "string"
    }

### <a name="administratorloginpassword"></a><span data-ttu-id="979ae-123">administratorLoginPassword</span><span class="sxs-lookup"><span data-stu-id="979ae-123">administratorLoginPassword</span></span>
<span data-ttu-id="979ae-124">Bonjour toouse de mot de passe d’administrateur de serveur de base de données hello.</span><span class="sxs-lookup"><span data-stu-id="979ae-124">hello password toouse for hello database server administrator.</span></span>

    "administratorLoginPassword": {
      "type": "securestring"
    }

### <a name="databasename"></a><span data-ttu-id="979ae-125">databaseName</span><span class="sxs-lookup"><span data-stu-id="979ae-125">databaseName</span></span>
<span data-ttu-id="979ae-126">nom de Hello de hello nouvelle base de données toocreate.</span><span class="sxs-lookup"><span data-stu-id="979ae-126">hello name of hello new database toocreate.</span></span>

    "databaseName": {
      "type": "string",
      "defaultValue": "sampledb"
    }

### <a name="collation"></a><span data-ttu-id="979ae-127">collation</span><span class="sxs-lookup"><span data-stu-id="979ae-127">collation</span></span>
<span data-ttu-id="979ae-128">toouse de classement de base de données Hello pour hello régissant appropriée l’utilisation de caractères.</span><span class="sxs-lookup"><span data-stu-id="979ae-128">hello database collation toouse for governing hello proper use of characters.</span></span>

    "collation": {
      "type": "string",
      "defaultValue": "SQL_Latin1_General_CP1_CI_AS"
    }

### <a name="edition"></a><span data-ttu-id="979ae-129">edition</span><span class="sxs-lookup"><span data-stu-id="979ae-129">edition</span></span>
<span data-ttu-id="979ae-130">type de Hello de toocreate de base de données.</span><span class="sxs-lookup"><span data-stu-id="979ae-130">hello type of database toocreate.</span></span>

    "edition": {
      "type": "string",
      "defaultValue": "Basic",
      "allowedValues": [
        "Basic",
        "Standard",
        "Premium"
      ],
      "metadata": {
        "description": "hello type of database toocreate."
      }
    }

### <a name="maxsizebytes"></a><span data-ttu-id="979ae-131">maxSizeBytes</span><span class="sxs-lookup"><span data-stu-id="979ae-131">maxSizeBytes</span></span>
<span data-ttu-id="979ae-132">Hello taille, en octets, pour la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="979ae-132">hello maximum size, in bytes, for hello database.</span></span>

    "maxSizeBytes": {
      "type": "string",
      "defaultValue": "1073741824"
    }

### <a name="requestedserviceobjectivename"></a><span data-ttu-id="979ae-133">requestedServiceObjectiveName</span><span class="sxs-lookup"><span data-stu-id="979ae-133">requestedServiceObjectiveName</span></span>
<span data-ttu-id="979ae-134">Hello nom correspondant toohello niveau de performance pour l’édition.</span><span class="sxs-lookup"><span data-stu-id="979ae-134">hello name corresponding toohello performance level for edition.</span></span> 

    "requestedServiceObjectiveName": {
      "type": "string",
      "defaultValue": "Basic",
      "allowedValues": [
        "Basic",
        "S0",
        "S1",
        "S2",
        "P1",
        "P2",
        "P3"
      ],
      "metadata": {
        "description": "Describes hello performance level for Edition"
      }
    }

## <a name="variables-for-names"></a><span data-ttu-id="979ae-135">Variables pour les noms</span><span class="sxs-lookup"><span data-stu-id="979ae-135">Variables for names</span></span>
<span data-ttu-id="979ae-136">Ce modèle inclut les variables qui construire des noms utilisés dans le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="979ae-136">This template includes variables that construct names used in hello template.</span></span> <span data-ttu-id="979ae-137">les valeurs de variable Hello utilisent hello **uniqueString** toogenerate un nom à partir de l’id de groupe de ressources hello de fonction.</span><span class="sxs-lookup"><span data-stu-id="979ae-137">hello variable values use hello **uniqueString** function toogenerate a name from hello resource group id.</span></span>

    "variables": {
        "hostingPlanName": "[concat('hostingplan', uniqueString(resourceGroup().id))]",
        "webSiteName": "[concat('webSite', uniqueString(resourceGroup().id))]",
        "sqlserverName": "[concat('sqlserver', uniqueString(resourceGroup().id))]"
    },


## <a name="resources-toodeploy"></a><span data-ttu-id="979ae-138">Ressources toodeploy</span><span class="sxs-lookup"><span data-stu-id="979ae-138">Resources toodeploy</span></span>
### <a name="sql-server-and-database"></a><span data-ttu-id="979ae-139">Base de données SQL et serveur SQL Server</span><span class="sxs-lookup"><span data-stu-id="979ae-139">SQL Server and Database</span></span>
<span data-ttu-id="979ae-140">Crée un serveur SQL Server et une base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="979ae-140">Creates a new SQL Server and database.</span></span> <span data-ttu-id="979ae-141">nom de Hello du serveur de hello est spécifié dans hello **nom_serveur** paramètre et hello l’emplacement spécifié dans hello **serverLocation** paramètre.</span><span class="sxs-lookup"><span data-stu-id="979ae-141">hello name of hello server is specified in hello **serverName** parameter and hello location specified in hello **serverLocation** parameter.</span></span> <span data-ttu-id="979ae-142">Lorsque vous créez un nouveau serveur de hello, vous devez fournir un nom de connexion et un mot de passe d’administrateur de serveur de base de données hello.</span><span class="sxs-lookup"><span data-stu-id="979ae-142">When creating hello new server, you must provide a login name and password for hello database server administrator.</span></span> 

    {
      "name": "[variables('sqlserverName')]",
      "type": "Microsoft.Sql/servers",
      "location": "[resourceGroup().location]",
      "tags": {
        "displayName": "SqlServer"
      },
      "apiVersion": "2014-04-01-preview",
      "properties": {
        "administratorLogin": "[parameters('administratorLogin')]",
        "administratorLoginPassword": "[parameters('administratorLoginPassword')]"
      },
      "resources": [
        {
          "name": "[parameters('databaseName')]",
          "type": "databases",
          "location": "[resourceGroup().location]",
          "tags": {
            "displayName": "Database"
          },
          "apiVersion": "2014-04-01-preview",
          "dependsOn": [
            "[variables('sqlserverName')]"
          ],
          "properties": {
            "edition": "[parameters('edition')]",
            "collation": "[parameters('collation')]",
            "maxSizeBytes": "[parameters('maxSizeBytes')]",
            "requestedServiceObjectiveName": "[parameters('requestedServiceObjectiveName')]"
          }
        },
        {
          "type": "firewallrules",
          "apiVersion": "2014-04-01-preview",
          "dependsOn": [
            "[variables('sqlserverName')]"
          ],
          "location": "[resourceGroup().location]",
          "name": "AllowAllAzureIps",
          "properties": {
            "endIpAddress": "0.0.0.0",
            "startIpAddress": "0.0.0.0"
          }
        }
      ]
    },

[!INCLUDE [app-service-web-deploy-web-host](../../includes/app-service-web-deploy-web-host.md)]

### <a name="web-app"></a><span data-ttu-id="979ae-143">Application web</span><span class="sxs-lookup"><span data-stu-id="979ae-143">Web app</span></span>
    {
      "apiVersion": "2015-08-01",
      "name": "[variables('webSiteName')]",
      "type": "Microsoft.Web/sites",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[variables('hostingPlanName')]"
      ],
      "tags": {
        "[concat('hidden-related:', resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName')))]": "empty",
        "displayName": "Website"
      },
      "properties": {
        "name": "[variables('webSiteName')]",
        "serverFarmId": "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]"
      },
      "resources": [
        {
          "apiVersion": "2015-08-01",
          "type": "config",
          "name": "connectionstrings",
          "dependsOn": [
            "[variables('webSiteName')]"
          ],
          "properties": {
            "DefaultConnection": {
              "value": "[concat('Data Source=tcp:', reference(concat('Microsoft.Sql/servers/', variables('sqlserverName'))).fullyQualifiedDomainName, ',1433;Initial Catalog=', parameters('databaseName'), ';User Id=', parameters('administratorLogin'), '@', variables('sqlserverName'), ';Password=', parameters('administratorLoginPassword'), ';')]",
              "type": "SQLServer"
            }
          }
        }
      ]
    },


### <a name="autoscale"></a><span data-ttu-id="979ae-144">Mise à l'échelle automatique</span><span class="sxs-lookup"><span data-stu-id="979ae-144">AutoScale</span></span>
    {
      "apiVersion": "2014-04-01",
      "name": "[concat(variables('hostingPlanName'), '-', resourceGroup().name)]",
      "type": "Microsoft.Insights/autoscalesettings",
      "location": "[resourceGroup().location]",
      "tags": {
        "[concat('hidden-link:', resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName')))]": "Resource",
        "displayName": "AutoScaleSettings"
      },
      "dependsOn": [
        "[variables('hostingPlanName')]"
      ],
      "properties": {
        "profiles": [
          {
            "name": "Default",
            "capacity": {
              "minimum": 1,
              "maximum": 2,
              "default": 1
            },
            "rules": [
              {
                "metricTrigger": {
                  "metricName": "CpuPercentage",
                  "metricResourceUri": "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]",
                  "timeGrain": "PT1M",
                  "statistic": "Average",
                  "timeWindow": "PT10M",
                  "timeAggregation": "Average",
                  "operator": "GreaterThan",
                  "threshold": 80.0
                },
                "scaleAction": {
                  "direction": "Increase",
                  "type": "ChangeCount",
                  "value": 1,
                  "cooldown": "PT10M"
                }
              },
              {
                "metricTrigger": {
                  "metricName": "CpuPercentage",
                  "metricResourceUri": "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]",
                  "timeGrain": "PT1M",
                  "statistic": "Average",
                  "timeWindow": "PT1H",
                  "timeAggregation": "Average",
                  "operator": "LessThan",
                  "threshold": 60.0
                },
                "scaleAction": {
                  "direction": "Decrease",
                  "type": "ChangeCount",
                  "value": 1,
                  "cooldown": "PT1H"
                }
              }
            ]
          }
        ],
        "enabled": false,
        "name": "[concat(variables('hostingPlanName'), '-', resourceGroup().name)]",
        "targetResourceUri": "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]"
      }
    },


### <a name="alert-rules-for-status-codes-403-and-500s-high-cpu-and-http-queue-length"></a><span data-ttu-id="979ae-145">Règles d'alerte pour les codes d'état 403 et 500, utilisation du processeur et longueur de file d'attente HTTP élevées</span><span class="sxs-lookup"><span data-stu-id="979ae-145">Alert rules for status codes 403 and 500's, High CPU, and HTTP Queue Length</span></span>
    {
      "apiVersion": "2014-04-01",
      "name": "[concat('ServerErrors ', variables('webSiteName'))]",
      "type": "Microsoft.Insights/alertrules",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[variables('webSiteName')]"
      ],
      "tags": {
        "[concat('hidden-link:', resourceId('Microsoft.Web/sites', variables('webSiteName')))]": "Resource",
        "displayName": "ServerErrorsAlertRule"
      },
      "properties": {
        "name": "[concat('ServerErrors ', variables('webSiteName'))]",
        "description": "[concat(variables('webSiteName'), ' has some server errors, status code 5xx.')]",
        "isEnabled": false,
        "condition": {
          "odata.type": "Microsoft.Azure.Management.Insights.Models.ThresholdRuleCondition",
          "dataSource": {
            "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleMetricDataSource",
            "resourceUri": "[resourceId('Microsoft.Web/sites', variables('webSiteName'))]",
            "metricName": "Http5xx"
          },
          "operator": "GreaterThan",
          "threshold": 0.0,
          "windowSize": "PT5M"
        },
        "action": {
          "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
          "sendToServiceOwners": true,
          "customEmails": [ ]
        }
      }
    },
    {
      "apiVersion": "2014-04-01",
      "name": "[concat('ForbiddenRequests ', variables('webSiteName'))]",
      "type": "Microsoft.Insights/alertrules",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[variables('webSiteName')]"
      ],
      "tags": {
        "[concat('hidden-link:', resourceId('Microsoft.Web/sites', variables('webSiteName')))]": "Resource",
        "displayName": "ForbiddenRequestsAlertRule"
      },
      "properties": {
        "name": "[concat('ForbiddenRequests ', variables('webSiteName'))]",
        "description": "[concat(variables('webSiteName'), ' has some requests that are forbidden, status code 403.')]",
        "isEnabled": false,
        "condition": {
          "odata.type": "Microsoft.Azure.Management.Insights.Models.ThresholdRuleCondition",
          "dataSource": {
            "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleMetricDataSource",
            "resourceUri": "[resourceId('Microsoft.Web/sites', variables('webSiteName'))]",
            "metricName": "Http403"
          },
          "operator": "GreaterThan",
          "threshold": 0,
          "windowSize": "PT5M"
        },
        "action": {
          "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
          "sendToServiceOwners": true,
          "customEmails": [ ]
        }
      }
    },
    {
      "apiVersion": "2014-04-01",
      "name": "[concat('CPUHigh ', variables('hostingPlanName'))]",
      "type": "Microsoft.Insights/alertrules",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[variables('hostingPlanName')]"
      ],
      "tags": {
        "[concat('hidden-link:', resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName')))]": "Resource",
        "displayName": "CPUHighAlertRule"
      },
      "properties": {
        "name": "[concat('CPUHigh ', variables('hostingPlanName'))]",
        "description": "[concat('hello average CPU is high across all hello instances of ', variables('hostingPlanName'))]",
        "isEnabled": false,
        "condition": {
          "odata.type": "Microsoft.Azure.Management.Insights.Models.ThresholdRuleCondition",
          "dataSource": {
            "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleMetricDataSource",
            "resourceUri": "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]",
            "metricName": "CpuPercentage"
          },
          "operator": "GreaterThan",
          "threshold": 90,
          "windowSize": "PT15M"
        },
        "action": {
          "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
          "sendToServiceOwners": true,
          "customEmails": [ ]
        }
      }
    },
    {
      "apiVersion": "2014-04-01",
      "name": "[concat('LongHttpQueue ', variables('hostingPlanName'))]",
      "type": "Microsoft.Insights/alertrules",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[variables('hostingPlanName')]"
      ],
      "tags": {
        "[concat('hidden-link:', resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName')))]": "Resource",
        "displayName": "AutoScaleSettings"
      },
      "properties": {
        "name": "[concat('LongHttpQueue ', variables('hostingPlanName'))]",
        "description": "[concat('hello HTTP queue for hello instances of ', variables('hostingPlanName'), ' has a large number of pending requests.')]",
        "isEnabled": false,
        "condition": {
          "odata.type": "Microsoft.Azure.Management.Insights.Models.ThresholdRuleCondition",
          "dataSource": {
            "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleMetricDataSource",
            "resourceUri": "[concat(resourceGroup().id, '/providers/Microsoft.Web/serverfarms/', variables('hostingPlanName'))]",
            "metricName": "HttpQueueLength"
          },
          "operator": "GreaterThan",
          "threshold": 100.0,
          "windowSize": "PT5M"
        },
        "action": {
          "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
          "sendToServiceOwners": true,
          "customEmails": [ ]
        }
      }
    },

### <a name="app-insights"></a><span data-ttu-id="979ae-146">App Insights</span><span class="sxs-lookup"><span data-stu-id="979ae-146">App Insights</span></span>
    {
      "apiVersion": "2014-04-01",
      "name": "[concat('AppInsights', variables('webSiteName'))]",
      "type": "Microsoft.Insights/components",
      "location": "Central US",
      "dependsOn": [
        "[variables('webSiteName')]"
      ],
      "tags": {
        "[concat('hidden-link:', resourceId('Microsoft.Web/sites', variables('webSiteName')))]": "Resource",
        "displayName": "AppInsightsComponent"
      },
      "properties": {
        "ApplicationId": "[variables('webSiteName')]"
      }
    }

## <a name="commands-toorun-deployment"></a><span data-ttu-id="979ae-147">Déploiement de toorun de commandes</span><span class="sxs-lookup"><span data-stu-id="979ae-147">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="979ae-148">PowerShell</span><span class="sxs-lookup"><span data-stu-id="979ae-148">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-sql-database/azuredeploy.json

### <a name="azure-cli"></a><span data-ttu-id="979ae-149">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="979ae-149">Azure CLI</span></span>

    azure config mode arm
    azure group deployment create -g {resource-group-name} --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-sql-database/azuredeploy.json

### <a name="azure-cli-20"></a><span data-ttu-id="979ae-150">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="979ae-150">Azure CLI 2.0</span></span>

    az resource deployment create -g {resource-group-name} --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-sql-database/azuredeploy.json --parameters '@azuredeploy.parameters.json'

> [!NOTE]
> <span data-ttu-id="979ae-151">Pour le contenu du fichier JSON de paramètres hello, consultez [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-sql-database/azuredeploy.parameters.json).</span><span class="sxs-lookup"><span data-stu-id="979ae-151">For content of hello parameters JSON file, see [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-sql-database/azuredeploy.parameters.json).</span></span>
>
>
