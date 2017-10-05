---
title: "Mise à l’échelle automatique et groupes identiques de machines virtuelles | Microsoft Docs"
description: "En savoir plus sur l’utilisation des ressources de diagnostic et de mise à l’échelle pour mettre à l’échelle automatiquement des machines virtuelles dans un groupe identique."
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d29a3385-179e-4331-a315-daa7ea5701df
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: adegeo
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 06ff9d9ae1dd8256f0d22c1a60ed6a85554f1f17
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-automatic-scaling-and-virtual-machine-scale-sets"></a><span data-ttu-id="f67fb-103">Mise à l’échelle automatique et groupes identiques de machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="f67fb-103">How to use automatic scaling and Virtual Machine Scale Sets</span></span>
<span data-ttu-id="f67fb-104">La mise à l’échelle automatique de machines virtuelles dans un jeu de mise à l’échelle consiste à créer ou à supprimer des machines dans l’ensemble en fonction des exigences de performances.</span><span class="sxs-lookup"><span data-stu-id="f67fb-104">Automatic scaling of virtual machines in a scale set is the creation or deletion of machines in the set as needed to match performance requirements.</span></span> <span data-ttu-id="f67fb-105">Au fur et à mesure de l’évolution du volume de travail, une application peut nécessiter des ressources supplémentaires afin d’exécuter les tâches de manière efficace.</span><span class="sxs-lookup"><span data-stu-id="f67fb-105">As the volume of work grows, an application may require additional resources to enable it to effectively perform tasks.</span></span>

<span data-ttu-id="f67fb-106">La mise à l’échelle automatique est un processus automatisé qui allège les contraintes de gestion.</span><span class="sxs-lookup"><span data-stu-id="f67fb-106">Automatic scaling is an automated process that helps ease management overhead.</span></span> <span data-ttu-id="f67fb-107">En réduisant la surcharge, vous n’avez pas besoin de surveiller en permanence les performances du système ou de décider de la manière de gérer les ressources.</span><span class="sxs-lookup"><span data-stu-id="f67fb-107">By reducing overhead, you don't need to continually monitor system performance or decide how to manage resources.</span></span> <span data-ttu-id="f67fb-108">La mise à l’échelle est un processus élastique.</span><span class="sxs-lookup"><span data-stu-id="f67fb-108">Scaling is an elastic process.</span></span> <span data-ttu-id="f67fb-109">Des ressources supplémentaires peuvent être ajoutées à mesure que la charge augmente.</span><span class="sxs-lookup"><span data-stu-id="f67fb-109">More resources can be added as the load increases.</span></span> <span data-ttu-id="f67fb-110">Lorsque la demande diminue, vous pouvez supprimer des ressources afin de réduire les coûts tout en maintenant les niveaux de performances.</span><span class="sxs-lookup"><span data-stu-id="f67fb-110">And as demand decreases, resources can be removed to minimize costs and maintain performance levels.</span></span>

<span data-ttu-id="f67fb-111">Configurez la mise à l’échelle automatique dans un jeu de mise à l’échelle à l’aide d’un modèle Azure Resource Manager, d’Azure PowerShell ou de l’interface CLI Azure ou du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="f67fb-111">Set up automatic scaling on a scale set by using an Azure Resource Manager template, Azure PowerShell, Azure CLI, or the Azure portal.</span></span>

## <a name="set-up-scaling-by-using-resource-manager-templates"></a><span data-ttu-id="f67fb-112">Configurer la mise à l’échelle à l’aide de modèles Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f67fb-112">Set up scaling by using Resource Manager templates</span></span>
<span data-ttu-id="f67fb-113">Au lieu de déployer et de gérer chaque ressource de votre application séparément, utilisez un modèle qui déploie toutes les ressources en une seule opération coordonnée.</span><span class="sxs-lookup"><span data-stu-id="f67fb-113">Rather than deploying and managing each resource of your application separately, use a template that deploys all resources in a single, coordinated operation.</span></span> <span data-ttu-id="f67fb-114">Dans le modèle, les ressources d’application sont définies et les paramètres de déploiement sont spécifiés pour différents environnements.</span><span class="sxs-lookup"><span data-stu-id="f67fb-114">In the template, application resources are defined and deployment parameters are specified for different environments.</span></span> <span data-ttu-id="f67fb-115">Le modèle se compose d’un JSON et d’expressions que vous pouvez utiliser pour construire des valeurs pour votre déploiement.</span><span class="sxs-lookup"><span data-stu-id="f67fb-115">The template consists of JSON and expressions that you can use to construct values for your deployment.</span></span> <span data-ttu-id="f67fb-116">Pour en savoir plus, voir [Créer des modèles Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="f67fb-116">To learn more, look at [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="f67fb-117">Dans le modèle, vous indiquez l’élément de capacité :</span><span class="sxs-lookup"><span data-stu-id="f67fb-117">In the template, you specify the capacity element:</span></span>

```json
"sku": {
  "name": "Standard_A0",
  "tier": "Standard",
  "capacity": 3
},
```

<span data-ttu-id="f67fb-118">La capacité correspond au nombre de machines virtuelles dans le jeu.</span><span class="sxs-lookup"><span data-stu-id="f67fb-118">Capacity identifies the number of virtual machines in the set.</span></span> <span data-ttu-id="f67fb-119">Vous pouvez modifier manuellement la capacité en déployant un modèle avec une valeur différente.</span><span class="sxs-lookup"><span data-stu-id="f67fb-119">You can manually change the capacity by deploying a template with a different value.</span></span> <span data-ttu-id="f67fb-120">Si vous déployez un modèle simplement pour modifier la capacité, vous pouvez inclure uniquement l’élément SKU avec la capacité mise à jour.</span><span class="sxs-lookup"><span data-stu-id="f67fb-120">If you are deploying a template to only change the capacity, you can include only the SKU element with the updated capacity.</span></span>

<span data-ttu-id="f67fb-121">La capacité du groupe identique peut être ajustée automatiquement en combinant la ressource **autoscaleSettings** et l’extension Diagnostics.</span><span class="sxs-lookup"><span data-stu-id="f67fb-121">The capacity of your scale set can be automatically adjusted by using a combination of the **autoscaleSettings** resource and the diagnostics extension.</span></span>

### <a name="configure-the-azure-diagnostics-extension"></a><span data-ttu-id="f67fb-122">Configurer l’extension Azure Diagnostics</span><span class="sxs-lookup"><span data-stu-id="f67fb-122">Configure the Azure Diagnostics extension</span></span>
<span data-ttu-id="f67fb-123">La mise à l’échelle automatique peut uniquement être réalisée si la collecte de mesures est réussie sur chaque machine virtuelle du jeu de mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="f67fb-123">Automatic scaling can only be done if metrics collection is successful on each virtual machine in the scale set.</span></span> <span data-ttu-id="f67fb-124">L’extension Azure Diagnostics offre des capacités de surveillance et de diagnostic qui répondent aux besoins en matière de collecte de mesures de la ressource de mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="f67fb-124">The Azure Diagnostics Extension provides the monitoring and diagnostics capabilities that meets the metrics collection needs of the autoscale resource.</span></span> <span data-ttu-id="f67fb-125">Vous pouvez installer l’extension en tant que partie du modèle Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f67fb-125">You can install the extension as part of the Resource Manager template.</span></span>

<span data-ttu-id="f67fb-126">Cet exemple montre les variables utilisées dans le modèle pour configurer l’extension de diagnostic :</span><span class="sxs-lookup"><span data-stu-id="f67fb-126">This example shows the variables that are used in the template to configure the diagnostics extension:</span></span>

```json
"diagnosticsStorageAccountName": "[concat(parameters('resourcePrefix'), 'saa')]",
"accountid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/', resourceGroup().name,'/providers/', 'Microsoft.Storage/storageAccounts/', variables('diagnosticsStorageAccountName'))]",
"wadlogs": "<WadCfg> <DiagnosticMonitorConfiguration overallQuotaInMB=\"4096\" xmlns=\"http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration\"> <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter=\"Error\"/> <WindowsEventLog scheduledTransferPeriod=\"PT1M\" > <DataSource name=\"Application!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"Security!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"System!*[System[(Level = 1 or Level = 2)]]\" /></WindowsEventLog>",
"wadperfcounter": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\"><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\Thread Count\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Thread Count\" locale=\"en-us\"/></PerformanceCounterConfiguration></PerformanceCounters>",
"wadcfgxstart": "[concat(variables('wadlogs'),variables('wadperfcounter'),'<Metrics resourceId=\"')]",
"wadmetricsresourceid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name ,'/providers/','Microsoft.Compute/virtualMachineScaleSets/',parameters('vmssName'))]",
"wadcfgxend": "[concat('\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/><MetricAggregation scheduledTransferPeriod=\"PT1M\"/></Metrics></DiagnosticMonitorConfiguration></WadCfg>')]"
```

<span data-ttu-id="f67fb-127">Les paramètres sont fournis lorsque le modèle est déployé.</span><span class="sxs-lookup"><span data-stu-id="f67fb-127">Parameters are provided when the template is deployed.</span></span> <span data-ttu-id="f67fb-128">Dans cet exemple, le nom du compte de stockage (où sont stockées les données) et le nom du groupe identique (à partir duquel les données sont collectées) sont fournis.</span><span class="sxs-lookup"><span data-stu-id="f67fb-128">In this example, the name of the storage account (where data is stored) and the name of the scale set (where data is collected) are provided.</span></span> <span data-ttu-id="f67fb-129">Également dans cet exemple de Windows Server, seul le compteur de performances Nombre de threads est collecté.</span><span class="sxs-lookup"><span data-stu-id="f67fb-129">Also in this Windows Server example, only the Thread Count performance counter is collected.</span></span> <span data-ttu-id="f67fb-130">Tous les compteurs de performances disponibles dans Windows ou Linux peuvent être utilisés pour collecter des informations de diagnostic et peuvent être inclus dans la configuration de l’extension.</span><span class="sxs-lookup"><span data-stu-id="f67fb-130">All the available performance counters in Windows or Linux can be used to collect diagnostics information and can be included in the extension configuration.</span></span>

<span data-ttu-id="f67fb-131">Cet exemple illustre la définition de l’extension dans le modèle :</span><span class="sxs-lookup"><span data-stu-id="f67fb-131">This example shows the definition of the extension in the template:</span></span>

```json
"extensionProfile": {
  "extensions": [
    {
      "name": "Microsoft.Insights.VMDiagnosticsSettings",
      "properties": {
        "publisher": "Microsoft.Azure.Diagnostics",
        "type": "IaaSDiagnostics",
        "typeHandlerVersion": "1.5",
        "autoUpgradeMinorVersion": true,
        "settings": {
          "xmlCfg": "[base64(concat(variables('wadcfgxstart'),variables('wadmetricsresourceid'),variables('wadcfgxend')))]",
          "storageAccount": "[variables('diagnosticsStorageAccountName')]"
        },
        "protectedSettings": {
          "storageAccountName": "[variables('diagnosticsStorageAccountName')]",
          "storageAccountKey": "[listkeys(variables('accountid'), variables('apiVersion')).key1]",
          "storageAccountEndPoint": "https://core.windows.net"
        }
      }
    }
  ]
}
```

<span data-ttu-id="f67fb-132">Lorsque l’extension de diagnostic s’exécute, les données sont stockées et collectées dans une table, dans le compte de stockage que vous spécifiez.</span><span class="sxs-lookup"><span data-stu-id="f67fb-132">When the diagnostics extension runs, the data is stored and collected in a table, in the storage account that you specify.</span></span> <span data-ttu-id="f67fb-133">La table **WADPerformanceCounters** regroupe les données collectées :</span><span class="sxs-lookup"><span data-stu-id="f67fb-133">In the **WADPerformanceCounters** table, you can find the collected data:</span></span>

![](./media/virtual-machine-scale-sets-autoscale-overview/ThreadCountBefore2.png)

### <a name="configure-the-autoscalesettings-resource"></a><span data-ttu-id="f67fb-134">Configurer la ressource autoScaleSettings</span><span class="sxs-lookup"><span data-stu-id="f67fb-134">Configure the autoScaleSettings resource</span></span>
<span data-ttu-id="f67fb-135">La ressource autoscaleSettings utilise les informations collectées à partir de l’extension Diagnostics pour décider d’augmenter ou de réduire le nombre de machines virtuelles dans l’ensemble d’échelle.</span><span class="sxs-lookup"><span data-stu-id="f67fb-135">The autoscaleSettings resource uses the information from the diagnostics extension to decide whether to increase or decrease the number of virtual machines in the scale set.</span></span>

<span data-ttu-id="f67fb-136">Cet exemple illustre la configuration de la ressource dans le modèle :</span><span class="sxs-lookup"><span data-stu-id="f67fb-136">This example shows the configuration of the resource in the template:</span></span>

```json
{
  "type": "Microsoft.Insights/autoscaleSettings",
  "apiVersion": "2015-04-01",
  "name": "[concat(parameters('resourcePrefix'),'as1')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]"
  ],
  "properties": {
    "enabled": true,
    "name": "[concat(parameters('resourcePrefix'),'as1')]",
    "profiles": [
      {
        "name": "Profile1",
        "capacity": {
          "minimum": "1",
          "maximum": "10",
          "default": "1"
        },
        "rules": [
          {
            "metricTrigger": {
              "metricName": "\\Processor(_Total)\\Thread Count",
              "metricNamespace": "",
              "metricResourceUri": "[concat('/subscriptions/',subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]",
              "timeGrain": "PT1M",
              "statistic": "Average",
              "timeWindow": "PT5M",
              "timeAggregation": "Average",
              "operator": "GreaterThan",
              "threshold": 650
            },
            "scaleAction": {
              "direction": "Increase",
              "type": "ChangeCount",
              "value": "1",
              "cooldown": "PT5M"
            }
          },
          {
            "metricTrigger": {
              "metricName": "\\Processor(_Total)\\Thread Count",
              "metricNamespace": "",
              "metricResourceUri": "[concat('/subscriptions/',subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]",
              "timeGrain": "PT1M",
              "statistic": "Average",
              "timeWindow": "PT5M",
              "timeAggregation": "Average",
              "operator": "LessThan",
              "threshold": 550
            },
            "scaleAction": {
              "direction": "Decrease",
              "type": "ChangeCount",
              "value": "1",
              "cooldown": "PT5M"
            }
          }
        ]
      }
    ],
    "targetResourceUri": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]"
  }
}
```

<span data-ttu-id="f67fb-137">Dans l’exemple ci-dessus, deux règles sont créées afin de définir les actions de mise à l’échelle automatique.</span><span class="sxs-lookup"><span data-stu-id="f67fb-137">In the example above, two rules are created for defining the automatic scaling actions.</span></span> <span data-ttu-id="f67fb-138">La première règle définit l’action d’augmentation de l’échelle, et la deuxième l’action de réduction de l’échelle.</span><span class="sxs-lookup"><span data-stu-id="f67fb-138">The first rule defines the scale-out action and the second rule defines the scale-in action.</span></span> <span data-ttu-id="f67fb-139">Ces valeurs sont fournies dans les règles :</span><span class="sxs-lookup"><span data-stu-id="f67fb-139">These values are provided in the rules:</span></span>

| <span data-ttu-id="f67fb-140">Règle</span><span class="sxs-lookup"><span data-stu-id="f67fb-140">Rule</span></span> | <span data-ttu-id="f67fb-141">Description</span><span class="sxs-lookup"><span data-stu-id="f67fb-141">Description</span></span> |
| ---- | ----------- |
| <span data-ttu-id="f67fb-142">metricName</span><span class="sxs-lookup"><span data-stu-id="f67fb-142">metricName</span></span>        | <span data-ttu-id="f67fb-143">Cette valeur est celle du compteur de performances que vous avez défini dans la variable wadperfcounter pour l’extension Diagnostics.</span><span class="sxs-lookup"><span data-stu-id="f67fb-143">This value is the same as the performance counter that you defined in the wadperfcounter variable for the diagnostics extension.</span></span> <span data-ttu-id="f67fb-144">Dans l’exemple ci-dessus, le compteur du nombre de threads est utilisé.</span><span class="sxs-lookup"><span data-stu-id="f67fb-144">In the example above, the Thread Count counter is used.</span></span>    |
| <span data-ttu-id="f67fb-145">metricResourceUri</span><span class="sxs-lookup"><span data-stu-id="f67fb-145">metricResourceUri</span></span> | <span data-ttu-id="f67fb-146">Cette valeur est l’identificateur de ressource du groupe de machines virtuelles identiques.</span><span class="sxs-lookup"><span data-stu-id="f67fb-146">This value is the resource identifier of the virtual machine scale set.</span></span> <span data-ttu-id="f67fb-147">Cet identificateur contient le nom du groupe de ressources, le nom du fournisseur de ressources et le nom du jeu de mise à l’échelle à mettre à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="f67fb-147">This identifier contains the name of the resource group, the name of the resource provider, and the name of the scale set to scale.</span></span> |
| <span data-ttu-id="f67fb-148">timeGrain</span><span class="sxs-lookup"><span data-stu-id="f67fb-148">timeGrain</span></span>         | <span data-ttu-id="f67fb-149">Cette valeur est la granularité des mesures collectées.</span><span class="sxs-lookup"><span data-stu-id="f67fb-149">This value is the granularity of the metrics that are collected.</span></span> <span data-ttu-id="f67fb-150">Dans l’exemple ci-dessus, les données sont collectées sur un intervalle d’une minute.</span><span class="sxs-lookup"><span data-stu-id="f67fb-150">In the preceding example, data is collected on an interval of one minute.</span></span> <span data-ttu-id="f67fb-151">Cette valeur est utilisée avec timeWindow.</span><span class="sxs-lookup"><span data-stu-id="f67fb-151">This value is used with timeWindow.</span></span> |
| <span data-ttu-id="f67fb-152">statistic</span><span class="sxs-lookup"><span data-stu-id="f67fb-152">statistic</span></span>         | <span data-ttu-id="f67fb-153">Cette valeur détermine la façon dont les mesures sont combinées pour prendre en charge l’action de mise à l’échelle automatique.</span><span class="sxs-lookup"><span data-stu-id="f67fb-153">This value determines how the metrics are combined to accommodate the automatic scaling action.</span></span> <span data-ttu-id="f67fb-154">Les valeurs possibles sont : Moyenne, Min, Max.</span><span class="sxs-lookup"><span data-stu-id="f67fb-154">The possible values are: Average, Min, Max.</span></span> |
| <span data-ttu-id="f67fb-155">timeWindow</span><span class="sxs-lookup"><span data-stu-id="f67fb-155">timeWindow</span></span>        | <span data-ttu-id="f67fb-156">Cette valeur est la plage de temps pendant laquelle les données d’instance sont collectées.</span><span class="sxs-lookup"><span data-stu-id="f67fb-156">This value is the range of time in which instance data is collected.</span></span> <span data-ttu-id="f67fb-157">Elle doit être comprise entre 5 minutes et 12 heures.</span><span class="sxs-lookup"><span data-stu-id="f67fb-157">It must be between 5 minutes and 12 hours.</span></span> |
| <span data-ttu-id="f67fb-158">timeAggregation</span><span class="sxs-lookup"><span data-stu-id="f67fb-158">timeAggregation</span></span>   | <span data-ttu-id="f67fb-159">Cette valeur détermine la façon dont les données collectées doivent être combinées au fil du temps.</span><span class="sxs-lookup"><span data-stu-id="f67fb-159">This value determines how the data that is collected should be combined over time.</span></span> <span data-ttu-id="f67fb-160">La valeur par défaut est Average.</span><span class="sxs-lookup"><span data-stu-id="f67fb-160">The default value is Average.</span></span> <span data-ttu-id="f67fb-161">Les valeurs possibles sont : Moyenne, Minimum, Maximum, Dernier, Total, Nombre.</span><span class="sxs-lookup"><span data-stu-id="f67fb-161">The possible values are: Average, Minimum, Maximum, Last, Total, Count.</span></span> |
| <span data-ttu-id="f67fb-162">operator</span><span class="sxs-lookup"><span data-stu-id="f67fb-162">operator</span></span>          | <span data-ttu-id="f67fb-163">Cette valeur est l’opérateur utilisé pour comparer les données de mesure et le seuil.</span><span class="sxs-lookup"><span data-stu-id="f67fb-163">This value is the operator that is used to compare the metric data and the threshold.</span></span> <span data-ttu-id="f67fb-164">Les valeurs possibles sont : est égal à -Equals), différent de (NotEquals), supérieur à (GreaterThan), égal ou supérieur à (GreaterThanOrEqual), Inférieur à (LessThan), Inférieur ou égal à (LessThanOrEqual).</span><span class="sxs-lookup"><span data-stu-id="f67fb-164">The possible values are: Equals, NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.</span></span> |
| <span data-ttu-id="f67fb-165">threshold</span><span class="sxs-lookup"><span data-stu-id="f67fb-165">threshold</span></span>         | <span data-ttu-id="f67fb-166">Cette valeur est celle qui déclenche l’action de mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="f67fb-166">This value is the value that triggers the scale action.</span></span> <span data-ttu-id="f67fb-167">Veillez à définir un écart suffisant entre les valeurs seuil que vous définissez respectivement pour l’action d’**augmentation de l’échelle** et l’action de **réduction de l’échelle**.</span><span class="sxs-lookup"><span data-stu-id="f67fb-167">Be sure to provide a sufficient difference between the threshold values for the **scale-out** and **scale-in** actions.</span></span> <span data-ttu-id="f67fb-168">Si vous définissez des valeurs identiques, le système anticipe un changement constant qui l’empêche d’implémenter une action de mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="f67fb-168">If you set the same values for both actions, the system anticipates constant change, which prevents it from implementing a scaling action.</span></span> <span data-ttu-id="f67fb-169">Par exemple, la définition des deux valeurs sur 600 threads dans l’exemple précédent ne fonctionne pas.</span><span class="sxs-lookup"><span data-stu-id="f67fb-169">For example, setting both to 600 threads in the preceding example doesn't work.</span></span> |
| <span data-ttu-id="f67fb-170">direction</span><span class="sxs-lookup"><span data-stu-id="f67fb-170">direction</span></span>         | <span data-ttu-id="f67fb-171">Cette valeur détermine l’opération qui est effectuée lorsque la valeur de seuil est atteinte.</span><span class="sxs-lookup"><span data-stu-id="f67fb-171">This value determines the action that is taken when the threshold value is achieved.</span></span> <span data-ttu-id="f67fb-172">Les valeurs possibles sont Augmenter ou Diminuer.</span><span class="sxs-lookup"><span data-stu-id="f67fb-172">The possible values are Increase or Decrease.</span></span> |
| <span data-ttu-id="f67fb-173">Type</span><span class="sxs-lookup"><span data-stu-id="f67fb-173">type</span></span>              | <span data-ttu-id="f67fb-174">Cette valeur est le type d’action qui doit se produire. Elle doit être définie sur ChangeCount.</span><span class="sxs-lookup"><span data-stu-id="f67fb-174">This value is the type of action that should occur and must be set to ChangeCount.</span></span> |
| <span data-ttu-id="f67fb-175">value</span><span class="sxs-lookup"><span data-stu-id="f67fb-175">value</span></span>             | <span data-ttu-id="f67fb-176">Cette valeur indique le nombre de machines virtuelles qui sont ajoutées ou supprimées dans le groupe identique.</span><span class="sxs-lookup"><span data-stu-id="f67fb-176">This value is the number of virtual machines that are added to or removed from the scale set.</span></span> <span data-ttu-id="f67fb-177">Cette valeur doit être définie sur 1 ou supérieur.</span><span class="sxs-lookup"><span data-stu-id="f67fb-177">This value must be 1 or greater.</span></span> |
| <span data-ttu-id="f67fb-178">cooldown</span><span class="sxs-lookup"><span data-stu-id="f67fb-178">cooldown</span></span>          | <span data-ttu-id="f67fb-179">Cette valeur est la durée d’attente depuis la dernière opération de mise à l’échelle avant que l’action suivante se produise.</span><span class="sxs-lookup"><span data-stu-id="f67fb-179">This value is the amount of time to wait since the last scaling action before the next action occurs.</span></span> <span data-ttu-id="f67fb-180">Elle doit être comprise entre une minute et une semaine.</span><span class="sxs-lookup"><span data-stu-id="f67fb-180">This value must be between one minute and one week.</span></span> |

<span data-ttu-id="f67fb-181">En fonction du compteur de performance que vous utilisez, certains éléments de la configuration du modèle sont utilisés différemment.</span><span class="sxs-lookup"><span data-stu-id="f67fb-181">Depending on the performance counter, you are using, some of the elements in the template configuration are used differently.</span></span> <span data-ttu-id="f67fb-182">Dans l’exemple précédent, le compteur de performances est Nombre de threads, la valeur de seuil est 650 pour une action d’augmentation de l’échelle, et 550 pour une action de réduction de l’échelle.</span><span class="sxs-lookup"><span data-stu-id="f67fb-182">In the preceding example, the performance counter is Thread Count, the threshold value is 650 for a scale-out action, and the threshold value is 550 for the scale-in action.</span></span> <span data-ttu-id="f67fb-183">Si vous utilisez un compteur tel que le pourcentage de temps processeur, la valeur de seuil est définie sur le pourcentage d’utilisation du processeur qui détermine une action de mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="f67fb-183">If you use a counter such as %Processor Time, the threshold value is set to the percentage of CPU usage that determines a scaling action.</span></span>

<span data-ttu-id="f67fb-184">Lorsqu’une action de mise à l’échelle est déclenchée (une charge élevée, par exemple), la capacité de l’ensemble est augmentée en fonction de la valeur spécifiée dans le modèle.</span><span class="sxs-lookup"><span data-stu-id="f67fb-184">When a scaling action is triggered, such as a high load, the capacity of the set is increased based on the value in the template.</span></span> <span data-ttu-id="f67fb-185">Par exemple, dans un jeu de mise à l’échelle où la capacité est définie sur 3 et la valeur d’action de mise à l’échelle est définie sur 1 :</span><span class="sxs-lookup"><span data-stu-id="f67fb-185">For example, in a scale set where the capacity is set to 3 and the scale action value is set to 1:</span></span>

![](./media/virtual-machine-scale-sets-autoscale-overview/ResourceExplorerBefore.png)

<span data-ttu-id="f67fb-186">Lorsque la charge actuelle fait passer le nombre moyen de threads au-dessus du seuil de 650 :</span><span class="sxs-lookup"><span data-stu-id="f67fb-186">When the current load causes the average thread count to go above the threshold of 650:</span></span>

![](./media/virtual-machine-scale-sets-autoscale-overview/ThreadCountAfter.png)

<span data-ttu-id="f67fb-187">Une action **d’augmentation d’échelle** est déclenchée, ce qui a pour effet d’augmenter d’une unité la capacité de l’ensemble :</span><span class="sxs-lookup"><span data-stu-id="f67fb-187">A **scale-out** action is triggered that causes the capacity of the set to be increased by one:</span></span>

```json
"sku": {
  "name": "Standard_A0",
  "tier": "Standard",
  "capacity": 4
},
```

<span data-ttu-id="f67fb-188">Une machine virtuelle est alors ajoutée au groupe identique :</span><span class="sxs-lookup"><span data-stu-id="f67fb-188">The result is a virtual machine is added to the scale set:</span></span>

![](./media/virtual-machine-scale-sets-autoscale-overview/ResourceExplorerAfter.png)

<span data-ttu-id="f67fb-189">Après une période de refroidissement de cinq minutes, si le nombre moyen de threads sur les machines est toujours supérieur à 600, une autre machine est ajoutée au jeu.</span><span class="sxs-lookup"><span data-stu-id="f67fb-189">After a cooldown period of five minutes, if the average number of threads on the machines stays over 600, another machine is added to the set.</span></span> <span data-ttu-id="f67fb-190">Si le nombre moyen de threads reste inférieur à 550, la capacité du jeu de mise à l’échelle est diminuée d’une unité et une machine est supprimée du jeu.</span><span class="sxs-lookup"><span data-stu-id="f67fb-190">If the average thread count stays below 550, the capacity of the scale set is reduced by one and a machine is removed from the set.</span></span>

## <a name="set-up-scaling-using-azure-powershell"></a><span data-ttu-id="f67fb-191">Configuration de mise à l’échelle à l’aide d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="f67fb-191">Set up scaling using Azure PowerShell</span></span>

<span data-ttu-id="f67fb-192">Pour voir des exemples d’utilisation de PowerShell pour configurer la mise à l’échelle automatique, consultez les [exemples de démarrage rapide d’Azure Monitor PowerShell](../monitoring-and-diagnostics/insights-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="f67fb-192">To see examples of using PowerShell to set up autoscaling, look at [Azure Monitor PowerShell quick start samples](../monitoring-and-diagnostics/insights-powershell-samples.md).</span></span>

## <a name="set-up-scaling-using-azure-cli"></a><span data-ttu-id="f67fb-193">Configuration de mise à l’échelle à l’aide de l’interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="f67fb-193">Set up scaling using Azure CLI</span></span>

<span data-ttu-id="f67fb-194">Pour voir des exemples d’utilisation de l’interface CLI d’Azure pour configurer la mise à l’échelle automatique, consultez les [exemples de démarrage rapide de l’interface CLI multiplateforme d’Azure Monitor](../monitoring-and-diagnostics/insights-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="f67fb-194">To see examples of using Azure CLI to set up autoscaling, look at [Azure Monitor Cross-platform CLI quick start samples](../monitoring-and-diagnostics/insights-cli-samples.md).</span></span>

## <a name="set-up-scaling-using-the-azure-portal"></a><span data-ttu-id="f67fb-195">Configuration de mise à l’échelle à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="f67fb-195">Set up scaling using the Azure portal</span></span>

<span data-ttu-id="f67fb-196">Pour voir un exemple d’utilisation du portail Azure pour configurer la mise à l’échelle automatique, consultez [Création d’un jeu de mise à l’échelle de machine virtuelle à l’aide du portail Azure](virtual-machine-scale-sets-portal-create.md).</span><span class="sxs-lookup"><span data-stu-id="f67fb-196">To see an example of using the Azure portal to set up autoscaling, look at [Create a Virtual Machine Scale Set using the Azure portal](virtual-machine-scale-sets-portal-create.md).</span></span>

## <a name="investigate-scaling-actions"></a><span data-ttu-id="f67fb-197">Examiner les actions de mise à l’échelle</span><span class="sxs-lookup"><span data-stu-id="f67fb-197">Investigate scaling actions</span></span>

* <span data-ttu-id="f67fb-198">**Portail Azure**</span><span class="sxs-lookup"><span data-stu-id="f67fb-198">**Azure portal**</span></span>  
<span data-ttu-id="f67fb-199">Vous pouvez obtenir une quantité limitée d’informations par le biais du portail.</span><span class="sxs-lookup"><span data-stu-id="f67fb-199">You can currently get a limited amount of information using the portal.</span></span>

* <span data-ttu-id="f67fb-200">**Azure Resource Explorer**</span><span class="sxs-lookup"><span data-stu-id="f67fb-200">**Azure Resource Explorer**</span></span>  
<span data-ttu-id="f67fb-201">Cet outil est le meilleur qui soit pour déterminer l’état actuel de votre groupe identique.</span><span class="sxs-lookup"><span data-stu-id="f67fb-201">This tool is the best for exploring the current state of your scale set.</span></span> <span data-ttu-id="f67fb-202">Suivez ce chemin d’accès. Vous devriez voir la vue de l’instance du groupe à échelle identique que vous avez créée :</span><span class="sxs-lookup"><span data-stu-id="f67fb-202">Follow this path and you should see the instance view of the scale set that you created:</span></span>  
<span data-ttu-id="f67fb-203">**Abonnements > {votre abonnement} > resourceGroups > {votre groupe de ressources} > fournisseurs > Microsoft.Compute > virtualMachineScaleSets > {votre groupe identique} > virtualMachines**</span><span class="sxs-lookup"><span data-stu-id="f67fb-203">**Subscriptions > {your subscription} > resourceGroups > {your resource group} > providers > Microsoft.Compute > virtualMachineScaleSets > {your scale set} > virtualMachines**</span></span>

* <span data-ttu-id="f67fb-204">**Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="f67fb-204">**Azure PowerShell**</span></span>  
<span data-ttu-id="f67fb-205">Utilisez cette commande pour obtenir des informations :</span><span class="sxs-lookup"><span data-stu-id="f67fb-205">Use this command to get some information:</span></span>

  ```powershell
  Get-AzureRmResource -name vmsstest1 -ResourceGroupName vmsstestrg1 -ResourceType Microsoft.Compute/virtualMachineScaleSets -ApiVersion 2015-06-15
  Get-Autoscalesetting -ResourceGroup rainvmss -DetailedOutput
  ```

* <span data-ttu-id="f67fb-206">Connectez-vous à la machine virtuelle jumpbox comme vous le feriez pour n’importe quel autre ordinateur et vous pouvez ensuite accéder à distance aux machines virtuelles du groupe à échelle identique pour surveiller les processus individuels.</span><span class="sxs-lookup"><span data-stu-id="f67fb-206">Connect to the jumpbox virtual machine just like you would any other machine and then you can remotely access the virtual machines in the scale set to monitor individual processes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f67fb-207">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f67fb-207">Next Steps</span></span>
* <span data-ttu-id="f67fb-208">Pour voir un exemple montrant comment créer un jeu de mise à l’échelle avec une mise à l’échelle automatique configurée, voir [Mise à l’échelle automatique des machines dans un jeu de mise à l’échelle de machine virtuelle](virtual-machine-scale-sets-windows-autoscale.md) .</span><span class="sxs-lookup"><span data-stu-id="f67fb-208">Look at [Automatically scale machines in a Virtual Machine Scale Set](virtual-machine-scale-sets-windows-autoscale.md) to see an example of how to create a scale set with automatic scaling configured.</span></span>

* <span data-ttu-id="f67fb-209">Découvrez des exemples de fonctionnalités de surveillance Azure Monitor dans les [exemples de démarrage rapide d’Azure Monitor PowerShell](../monitoring-and-diagnostics/insights-powershell-samples.md)</span><span class="sxs-lookup"><span data-stu-id="f67fb-209">Find examples of Azure Monitor monitoring features in [Azure Monitor PowerShell quick start samples](../monitoring-and-diagnostics/insights-powershell-samples.md)</span></span>

* <span data-ttu-id="f67fb-210">Pour en savoir plus sur les fonctionnalités de notification, consultez [Utilisation d’actions de mise à l’échelle automatique pour envoyer des notifications d’alerte webhook et par courrier électronique dans Azure Monitor](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md).</span><span class="sxs-lookup"><span data-stu-id="f67fb-210">Learn about notification features in [Use autoscale actions to send email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md).</span></span>

* <span data-ttu-id="f67fb-211">Découvrez comment [utiliser les journaux d’audit pour envoyer des notifications d’alerte webhook et par courrier électronique dans Azure Monitor](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span><span class="sxs-lookup"><span data-stu-id="f67fb-211">Learn about how to [Use audit logs to send email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span></span>

* <span data-ttu-id="f67fb-212">En savoir plus sur les [scénarios avancés de mise à l’échelle automatique](virtual-machine-scale-sets-advanced-autoscale.md).</span><span class="sxs-lookup"><span data-stu-id="f67fb-212">Learn about [advanced autoscale scenarios](virtual-machine-scale-sets-advanced-autoscale.md).</span></span>
