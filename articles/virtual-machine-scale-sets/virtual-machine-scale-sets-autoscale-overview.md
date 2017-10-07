---
title: "machine virtuelle et mise à l’échelle aaaAutomatic échelle jeux | Documents Microsoft"
description: "En savoir plus sur l’utilisation de machines virtuelles de mise à l’échelle ressources tooautomatically mise à l’échelle et de diagnostic dans un ensemble d’échelle."
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
ms.openlocfilehash: 25f54b693e3c991577238242008c262023ed479c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-automatic-scaling-and-virtual-machine-scale-sets"></a><span data-ttu-id="32421-103">La mise à l’échelle automatique du toouse et machines virtuelles identiques</span><span class="sxs-lookup"><span data-stu-id="32421-103">How toouse automatic scaling and Virtual Machine Scale Sets</span></span>
<span data-ttu-id="32421-104">La mise à l’échelle automatique des ordinateurs virtuels dans un ensemble d’échelle est la création de hello ou suppression d’ordinateurs Bonjour définir comme nécessaires toomatch les exigences de performances.</span><span class="sxs-lookup"><span data-stu-id="32421-104">Automatic scaling of virtual machines in a scale set is hello creation or deletion of machines in hello set as needed toomatch performance requirements.</span></span> <span data-ttu-id="32421-105">Au fur et à mesure du volume hello de travail, une application peut nécessiter des ressources supplémentaires tooenable il tooeffectively effectuer des tâches.</span><span class="sxs-lookup"><span data-stu-id="32421-105">As hello volume of work grows, an application may require additional resources tooenable it tooeffectively perform tasks.</span></span>

<span data-ttu-id="32421-106">La mise à l’échelle automatique est un processus automatisé qui allège les contraintes de gestion.</span><span class="sxs-lookup"><span data-stu-id="32421-106">Automatic scaling is an automated process that helps ease management overhead.</span></span> <span data-ttu-id="32421-107">Par la réduction de la charge, vous ne devez toocontinually surveiller les performances système ou décider comment toomanage ressources.</span><span class="sxs-lookup"><span data-stu-id="32421-107">By reducing overhead, you don't need toocontinually monitor system performance or decide how toomanage resources.</span></span> <span data-ttu-id="32421-108">La mise à l’échelle est un processus élastique.</span><span class="sxs-lookup"><span data-stu-id="32421-108">Scaling is an elastic process.</span></span> <span data-ttu-id="32421-109">Plus de ressources peuvent être ajoutés en tant que charge hello augmente.</span><span class="sxs-lookup"><span data-stu-id="32421-109">More resources can be added as hello load increases.</span></span> <span data-ttu-id="32421-110">Et, en tant que la demande diminue, les ressources peuvent être supprimé toominimize coûts et maintenir les niveaux de performances.</span><span class="sxs-lookup"><span data-stu-id="32421-110">And as demand decreases, resources can be removed toominimize costs and maintain performance levels.</span></span>

<span data-ttu-id="32421-111">Configurer la mise à l’échelle automatique sur une échelle définie à l’aide d’un modèle Azure Resource Manager, Azure PowerShell, CLI d’Azure ou hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="32421-111">Set up automatic scaling on a scale set by using an Azure Resource Manager template, Azure PowerShell, Azure CLI, or hello Azure portal.</span></span>

## <a name="set-up-scaling-by-using-resource-manager-templates"></a><span data-ttu-id="32421-112">Configurer la mise à l’échelle à l’aide de modèles Resource Manager</span><span class="sxs-lookup"><span data-stu-id="32421-112">Set up scaling by using Resource Manager templates</span></span>
<span data-ttu-id="32421-113">Au lieu de déployer et de gérer chaque ressource de votre application séparément, utilisez un modèle qui déploie toutes les ressources en une seule opération coordonnée.</span><span class="sxs-lookup"><span data-stu-id="32421-113">Rather than deploying and managing each resource of your application separately, use a template that deploys all resources in a single, coordinated operation.</span></span> <span data-ttu-id="32421-114">Dans le modèle de hello, ressources d’application sont définis, et les paramètres de déploiement sont spécifiés pour différents environnements.</span><span class="sxs-lookup"><span data-stu-id="32421-114">In hello template, application resources are defined and deployment parameters are specified for different environments.</span></span> <span data-ttu-id="32421-115">modèle de Hello se compose de JSON et les expressions que vous pouvez utiliser les valeurs tooconstruct pour votre déploiement.</span><span class="sxs-lookup"><span data-stu-id="32421-115">hello template consists of JSON and expressions that you can use tooconstruct values for your deployment.</span></span> <span data-ttu-id="32421-116">toolearn plus, observez [les modèles de programmation Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="32421-116">toolearn more, look at [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="32421-117">Dans le modèle de hello, vous spécifiez d’élément de capacité hello :</span><span class="sxs-lookup"><span data-stu-id="32421-117">In hello template, you specify hello capacity element:</span></span>

```json
"sku": {
  "name": "Standard_A0",
  "tier": "Standard",
  "capacity": 3
},
```

<span data-ttu-id="32421-118">Capacité identifie nombre hello d’ordinateurs virtuels dans le jeu de hello.</span><span class="sxs-lookup"><span data-stu-id="32421-118">Capacity identifies hello number of virtual machines in hello set.</span></span> <span data-ttu-id="32421-119">Vous pouvez modifier manuellement la capacité de hello en déployant un modèle avec une valeur différente.</span><span class="sxs-lookup"><span data-stu-id="32421-119">You can manually change hello capacity by deploying a template with a different value.</span></span> <span data-ttu-id="32421-120">Si vous déployez une capacité de hello modèle tooonly modification, vous pouvez inclure uniquement les élément de référence (SKU) hello avec une capacité hello mis à jour.</span><span class="sxs-lookup"><span data-stu-id="32421-120">If you are deploying a template tooonly change hello capacity, you can include only hello SKU element with hello updated capacity.</span></span>

<span data-ttu-id="32421-121">Hello la capacité de votre ensemble d’échelle peut être automatiquement ajustée en utilisant une combinaison de hello **autoscaleSettings** ressource et hello l’extension de diagnostics.</span><span class="sxs-lookup"><span data-stu-id="32421-121">hello capacity of your scale set can be automatically adjusted by using a combination of hello **autoscaleSettings** resource and hello diagnostics extension.</span></span>

### <a name="configure-hello-azure-diagnostics-extension"></a><span data-ttu-id="32421-122">Configurer l’extension des Diagnostics Windows Azure hello</span><span class="sxs-lookup"><span data-stu-id="32421-122">Configure hello Azure Diagnostics extension</span></span>
<span data-ttu-id="32421-123">Mise à l’échelle automatique peut être faite uniquement si la collecte de métriques est réussie sur chaque ordinateur virtuel dans un ensemble d’échelle hello.</span><span class="sxs-lookup"><span data-stu-id="32421-123">Automatic scaling can only be done if metrics collection is successful on each virtual machine in hello scale set.</span></span> <span data-ttu-id="32421-124">Hello Extension des Diagnostics Azure fournit des fonctionnalités d’analyse et de diagnostics hello qui répond aux besoins de collection hello métriques de ressources de mise à l’échelle hello.</span><span class="sxs-lookup"><span data-stu-id="32421-124">hello Azure Diagnostics Extension provides hello monitoring and diagnostics capabilities that meets hello metrics collection needs of hello autoscale resource.</span></span> <span data-ttu-id="32421-125">Vous pouvez installer l’extension de hello en tant que partie du modèle de gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="32421-125">You can install hello extension as part of hello Resource Manager template.</span></span>

<span data-ttu-id="32421-126">Cet exemple montre les variables hello qui sont utilisées dans l’extension de diagnostics hello modèle tooconfigure hello :</span><span class="sxs-lookup"><span data-stu-id="32421-126">This example shows hello variables that are used in hello template tooconfigure hello diagnostics extension:</span></span>

```json
"diagnosticsStorageAccountName": "[concat(parameters('resourcePrefix'), 'saa')]",
"accountid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/', resourceGroup().name,'/providers/', 'Microsoft.Storage/storageAccounts/', variables('diagnosticsStorageAccountName'))]",
"wadlogs": "<WadCfg> <DiagnosticMonitorConfiguration overallQuotaInMB=\"4096\" xmlns=\"http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration\"> <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter=\"Error\"/> <WindowsEventLog scheduledTransferPeriod=\"PT1M\" > <DataSource name=\"Application!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"Security!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"System!*[System[(Level = 1 or Level = 2)]]\" /></WindowsEventLog>",
"wadperfcounter": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\"><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\Thread Count\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Thread Count\" locale=\"en-us\"/></PerformanceCounterConfiguration></PerformanceCounters>",
"wadcfgxstart": "[concat(variables('wadlogs'),variables('wadperfcounter'),'<Metrics resourceId=\"')]",
"wadmetricsresourceid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name ,'/providers/','Microsoft.Compute/virtualMachineScaleSets/',parameters('vmssName'))]",
"wadcfgxend": "[concat('\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/><MetricAggregation scheduledTransferPeriod=\"PT1M\"/></Metrics></DiagnosticMonitorConfiguration></WadCfg>')]"
```

<span data-ttu-id="32421-127">Les paramètres sont fournis lorsque le modèle de hello est déployé.</span><span class="sxs-lookup"><span data-stu-id="32421-127">Parameters are provided when hello template is deployed.</span></span> <span data-ttu-id="32421-128">Dans cet exemple, le nom hello hello du compte de stockage (stockage des données) et le hello, nom de l’ensemble d’échelle hello (où les données sont collectées) sont fournies.</span><span class="sxs-lookup"><span data-stu-id="32421-128">In this example, hello name of hello storage account (where data is stored) and hello name of hello scale set (where data is collected) are provided.</span></span> <span data-ttu-id="32421-129">Également dans cet exemple de Windows Server, uniquement les compteurs de performance nombre de threads hello sont collectées.</span><span class="sxs-lookup"><span data-stu-id="32421-129">Also in this Windows Server example, only hello Thread Count performance counter is collected.</span></span> <span data-ttu-id="32421-130">Tous les hello des compteurs de performance disponibles dans Windows ou Linux peut être des informations de diagnostic toocollect utilisé et peut être inclus dans la configuration de l’extension hello.</span><span class="sxs-lookup"><span data-stu-id="32421-130">All hello available performance counters in Windows or Linux can be used toocollect diagnostics information and can be included in hello extension configuration.</span></span>

<span data-ttu-id="32421-131">Cet exemple montre la définition de hello d’extension de hello dans le modèle de hello :</span><span class="sxs-lookup"><span data-stu-id="32421-131">This example shows hello definition of hello extension in hello template:</span></span>

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

<span data-ttu-id="32421-132">Lors de l’extension de diagnostics hello s’exécute, les données de salutation stockées et collectées dans une table, hello compte de stockage que vous spécifiez.</span><span class="sxs-lookup"><span data-stu-id="32421-132">When hello diagnostics extension runs, hello data is stored and collected in a table, in hello storage account that you specify.</span></span> <span data-ttu-id="32421-133">Bonjour **WADPerformanceCounters** table, vous pouvez rechercher les données de salutation collectée :</span><span class="sxs-lookup"><span data-stu-id="32421-133">In hello **WADPerformanceCounters** table, you can find hello collected data:</span></span>

![](./media/virtual-machine-scale-sets-autoscale-overview/ThreadCountBefore2.png)

### <a name="configure-hello-autoscalesettings-resource"></a><span data-ttu-id="32421-134">Configurer les ressources d’autoScaleSettings hello</span><span class="sxs-lookup"><span data-stu-id="32421-134">Configure hello autoScaleSettings resource</span></span>
<span data-ttu-id="32421-135">ressources d’autoscaleSettings Hello utilise des informations de hello de hello diagnostics extension toodecide si le nombre de hello tooincrease ou d’une réduction des ordinateurs virtuels de l’échelle de hello défini.</span><span class="sxs-lookup"><span data-stu-id="32421-135">hello autoscaleSettings resource uses hello information from hello diagnostics extension toodecide whether tooincrease or decrease hello number of virtual machines in hello scale set.</span></span>

<span data-ttu-id="32421-136">Cet exemple montre une configuration hello de ressource de hello dans le modèle de hello :</span><span class="sxs-lookup"><span data-stu-id="32421-136">This example shows hello configuration of hello resource in hello template:</span></span>

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

<span data-ttu-id="32421-137">Dans l’exemple hello ci-dessus, les deux règles sont créées pour définir les actions de mise à l’échelle automatique hello.</span><span class="sxs-lookup"><span data-stu-id="32421-137">In hello example above, two rules are created for defining hello automatic scaling actions.</span></span> <span data-ttu-id="32421-138">première règle de Hello définit l’action de montée en puissance parallèle hello et seconde hello définit hello montée en puissance en action.</span><span class="sxs-lookup"><span data-stu-id="32421-138">hello first rule defines hello scale-out action and hello second rule defines hello scale-in action.</span></span> <span data-ttu-id="32421-139">Ces valeurs sont fournies dans les règles de hello :</span><span class="sxs-lookup"><span data-stu-id="32421-139">These values are provided in hello rules:</span></span>

| <span data-ttu-id="32421-140">Règle</span><span class="sxs-lookup"><span data-stu-id="32421-140">Rule</span></span> | <span data-ttu-id="32421-141">Description</span><span class="sxs-lookup"><span data-stu-id="32421-141">Description</span></span> |
| ---- | ----------- |
| <span data-ttu-id="32421-142">metricName</span><span class="sxs-lookup"><span data-stu-id="32421-142">metricName</span></span>        | <span data-ttu-id="32421-143">Cette valeur est hello identique au compteur de performance hello que vous défini dans la variable de wadperfcounter hello pour l’extension de diagnostics hello.</span><span class="sxs-lookup"><span data-stu-id="32421-143">This value is hello same as hello performance counter that you defined in hello wadperfcounter variable for hello diagnostics extension.</span></span> <span data-ttu-id="32421-144">Dans l’exemple hello ci-dessus, le compteur nombre de threads de hello est utilisé.</span><span class="sxs-lookup"><span data-stu-id="32421-144">In hello example above, hello Thread Count counter is used.</span></span>    |
| <span data-ttu-id="32421-145">metricResourceUri</span><span class="sxs-lookup"><span data-stu-id="32421-145">metricResourceUri</span></span> | <span data-ttu-id="32421-146">Cette valeur est l’identificateur de ressource de hello de hello machines virtuelles identiques.</span><span class="sxs-lookup"><span data-stu-id="32421-146">This value is hello resource identifier of hello virtual machine scale set.</span></span> <span data-ttu-id="32421-147">Cet identificateur contient hello nom hello du groupe de ressources, hello nom du fournisseur de ressources hello et nom hello de hello échelle ensemble tooscale.</span><span class="sxs-lookup"><span data-stu-id="32421-147">This identifier contains hello name of hello resource group, hello name of hello resource provider, and hello name of hello scale set tooscale.</span></span> |
| <span data-ttu-id="32421-148">timeGrain</span><span class="sxs-lookup"><span data-stu-id="32421-148">timeGrain</span></span>         | <span data-ttu-id="32421-149">Cette valeur est la granularité hello des métriques de hello sont collectés.</span><span class="sxs-lookup"><span data-stu-id="32421-149">This value is hello granularity of hello metrics that are collected.</span></span> <span data-ttu-id="32421-150">Bonjour précédent exemple, les données sont collectées sur un intervalle d’une minute.</span><span class="sxs-lookup"><span data-stu-id="32421-150">In hello preceding example, data is collected on an interval of one minute.</span></span> <span data-ttu-id="32421-151">Cette valeur est utilisée avec timeWindow.</span><span class="sxs-lookup"><span data-stu-id="32421-151">This value is used with timeWindow.</span></span> |
| <span data-ttu-id="32421-152">statistic</span><span class="sxs-lookup"><span data-stu-id="32421-152">statistic</span></span>         | <span data-ttu-id="32421-153">Cette valeur détermine comment les métriques de hello sont hello tooaccommodate combinée automatique d’action de mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="32421-153">This value determines how hello metrics are combined tooaccommodate hello automatic scaling action.</span></span> <span data-ttu-id="32421-154">Hello les valeurs possibles sont : moyenne, Min, Max.</span><span class="sxs-lookup"><span data-stu-id="32421-154">hello possible values are: Average, Min, Max.</span></span> |
| <span data-ttu-id="32421-155">timeWindow</span><span class="sxs-lookup"><span data-stu-id="32421-155">timeWindow</span></span>        | <span data-ttu-id="32421-156">Cette valeur est la plage de hello de temps dans laquelle les données d’instance sont collectées.</span><span class="sxs-lookup"><span data-stu-id="32421-156">This value is hello range of time in which instance data is collected.</span></span> <span data-ttu-id="32421-157">Elle doit être comprise entre 5 minutes et 12 heures.</span><span class="sxs-lookup"><span data-stu-id="32421-157">It must be between 5 minutes and 12 hours.</span></span> |
| <span data-ttu-id="32421-158">timeAggregation</span><span class="sxs-lookup"><span data-stu-id="32421-158">timeAggregation</span></span>   | <span data-ttu-id="32421-159">Cette valeur détermine l’association de données hello collectées au fil du temps.</span><span class="sxs-lookup"><span data-stu-id="32421-159">This value determines how hello data that is collected should be combined over time.</span></span> <span data-ttu-id="32421-160">valeur par défaut de Hello est moyenne.</span><span class="sxs-lookup"><span data-stu-id="32421-160">hello default value is Average.</span></span> <span data-ttu-id="32421-161">Hello les valeurs possibles sont : moyenne, Minimum, Maximum, dernier, Total, le nombre.</span><span class="sxs-lookup"><span data-stu-id="32421-161">hello possible values are: Average, Minimum, Maximum, Last, Total, Count.</span></span> |
| <span data-ttu-id="32421-162">operator</span><span class="sxs-lookup"><span data-stu-id="32421-162">operator</span></span>          | <span data-ttu-id="32421-163">Cette valeur est un opérateur hello toocompare utilisé hello métrique données et hello du seuil.</span><span class="sxs-lookup"><span data-stu-id="32421-163">This value is hello operator that is used toocompare hello metric data and hello threshold.</span></span> <span data-ttu-id="32421-164">Hello les valeurs possibles sont : Equals, NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.</span><span class="sxs-lookup"><span data-stu-id="32421-164">hello possible values are: Equals, NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.</span></span> |
| <span data-ttu-id="32421-165">threshold</span><span class="sxs-lookup"><span data-stu-id="32421-165">threshold</span></span>         | <span data-ttu-id="32421-166">Cette valeur est hello qui déclenche l’action de mise à l’échelle hello.</span><span class="sxs-lookup"><span data-stu-id="32421-166">This value is hello value that triggers hello scale action.</span></span> <span data-ttu-id="32421-167">Être tooprovide vraiment une différence suffisante entre les valeurs de seuil hello pour hello **montée en puissance parallèle** et **dans l’échelle** actions.</span><span class="sxs-lookup"><span data-stu-id="32421-167">Be sure tooprovide a sufficient difference between hello threshold values for hello **scale-out** and **scale-in** actions.</span></span> <span data-ttu-id="32421-168">Si vous définissez des mêmes valeurs pour les deux actions hello, système de hello anticipe modification constante, ce qui empêche son implémentation d’une action de mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="32421-168">If you set hello same values for both actions, hello system anticipates constant change, which prevents it from implementing a scaling action.</span></span> <span data-ttu-id="32421-169">Par exemple, définir les deux threads too600 Bonjour précédent exemple ne fonctionne pas.</span><span class="sxs-lookup"><span data-stu-id="32421-169">For example, setting both too600 threads in hello preceding example doesn't work.</span></span> |
| <span data-ttu-id="32421-170">direction</span><span class="sxs-lookup"><span data-stu-id="32421-170">direction</span></span>         | <span data-ttu-id="32421-171">Cette valeur détermine l’action hello qui est effectuée lorsque la valeur de seuil hello est atteint.</span><span class="sxs-lookup"><span data-stu-id="32421-171">This value determines hello action that is taken when hello threshold value is achieved.</span></span> <span data-ttu-id="32421-172">les valeurs possibles de Hello sont augmentent ou diminuent.</span><span class="sxs-lookup"><span data-stu-id="32421-172">hello possible values are Increase or Decrease.</span></span> |
| <span data-ttu-id="32421-173">type</span><span class="sxs-lookup"><span data-stu-id="32421-173">type</span></span>              | <span data-ttu-id="32421-174">Cette valeur est de type hello d’action qui doit se produire et doit avoir la valeur tooChangeCount.</span><span class="sxs-lookup"><span data-stu-id="32421-174">This value is hello type of action that should occur and must be set tooChangeCount.</span></span> |
| <span data-ttu-id="32421-175">value</span><span class="sxs-lookup"><span data-stu-id="32421-175">value</span></span>             | <span data-ttu-id="32421-176">Cette valeur est le nombre de hello d’ordinateurs virtuels qui sont ajoutés tooor supprimé de l’ensemble d’échelle hello.</span><span class="sxs-lookup"><span data-stu-id="32421-176">This value is hello number of virtual machines that are added tooor removed from hello scale set.</span></span> <span data-ttu-id="32421-177">Cette valeur doit être définie sur 1 ou supérieur.</span><span class="sxs-lookup"><span data-stu-id="32421-177">This value must be 1 or greater.</span></span> |
| <span data-ttu-id="32421-178">cooldown</span><span class="sxs-lookup"><span data-stu-id="32421-178">cooldown</span></span>          | <span data-ttu-id="32421-179">Cette valeur est hello toowait de temps depuis la dernière action de mise à l’échelle hello avant l’action suivante de hello se produit.</span><span class="sxs-lookup"><span data-stu-id="32421-179">This value is hello amount of time toowait since hello last scaling action before hello next action occurs.</span></span> <span data-ttu-id="32421-180">Elle doit être comprise entre une minute et une semaine.</span><span class="sxs-lookup"><span data-stu-id="32421-180">This value must be between one minute and one week.</span></span> |

<span data-ttu-id="32421-181">En fonction de compteur de performance hello, vous utilisez, certains éléments hello dans la configuration du modèle hello sont utilisées différemment.</span><span class="sxs-lookup"><span data-stu-id="32421-181">Depending on hello performance counter, you are using, some of hello elements in hello template configuration are used differently.</span></span> <span data-ttu-id="32421-182">Bonjour précédent exemple, compteur de performances hello est le nombre de threads, valeur de seuil hello 650 pour une action de montée en puissance parallèle et valeur de seuil hello 550 pour l’action de mise à l’échelle hello.</span><span class="sxs-lookup"><span data-stu-id="32421-182">In hello preceding example, hello performance counter is Thread Count, hello threshold value is 650 for a scale-out action, and hello threshold value is 550 for hello scale-in action.</span></span> <span data-ttu-id="32421-183">Si vous utilisez un compteur de % temps processeur, valeur de seuil hello a la valeur pourcentage de toohello d’utilisation du processeur qui détermine une action de mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="32421-183">If you use a counter such as %Processor Time, hello threshold value is set toohello percentage of CPU usage that determines a scaling action.</span></span>

<span data-ttu-id="32421-184">Lorsqu’une action de mise à l’échelle est déclenchée, comme une charge élevée, hello la capacité d’ensemble de hello est augmentée en fonction de la valeur hello dans le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="32421-184">When a scaling action is triggered, such as a high load, hello capacity of hello set is increased based on hello value in hello template.</span></span> <span data-ttu-id="32421-185">Par exemple, dans une échelle de définie où la capacité de hello too3 et et hello échelle action a la valeur too1 :</span><span class="sxs-lookup"><span data-stu-id="32421-185">For example, in a scale set where hello capacity is set too3 and hello scale action value is set too1:</span></span>

![](./media/virtual-machine-scale-sets-autoscale-overview/ResourceExplorerBefore.png)

<span data-ttu-id="32421-186">Lorsque hello actuel charge causes hello thread moyenne des toogo nombre au-dessus du seuil de hello de 650 :</span><span class="sxs-lookup"><span data-stu-id="32421-186">When hello current load causes hello average thread count toogo above hello threshold of 650:</span></span>

![](./media/virtual-machine-scale-sets-autoscale-overview/ThreadCountAfter.png)

<span data-ttu-id="32421-187">A **montée en puissance parallèle** action est déclenchée que causes hello capacité de hello ensemble toobe est augmentée d’une unité :</span><span class="sxs-lookup"><span data-stu-id="32421-187">A **scale-out** action is triggered that causes hello capacity of hello set toobe increased by one:</span></span>

```json
"sku": {
  "name": "Standard_A0",
  "tier": "Standard",
  "capacity": 4
},
```

<span data-ttu-id="32421-188">résultat de Hello est qu'un ordinateur virtuel est ajouté à un ensemble d’échelle toohello :</span><span class="sxs-lookup"><span data-stu-id="32421-188">hello result is a virtual machine is added toohello scale set:</span></span>

![](./media/virtual-machine-scale-sets-autoscale-overview/ResourceExplorerAfter.png)

<span data-ttu-id="32421-189">Si le nombre moyen de hello de threads sur les ordinateurs hello reste plus de 600, un autre ordinateur est ajouté après une période de ralentissement de cinq minutes, toohello ensemble.</span><span class="sxs-lookup"><span data-stu-id="32421-189">After a cooldown period of five minutes, if hello average number of threads on hello machines stays over 600, another machine is added toohello set.</span></span> <span data-ttu-id="32421-190">Si le nombre de threads moyenne hello reste ci-dessous 550, capacité hello de hello ensemble d’échelle est réduite d’une unité et un ordinateur est supprimé de hello.</span><span class="sxs-lookup"><span data-stu-id="32421-190">If hello average thread count stays below 550, hello capacity of hello scale set is reduced by one and a machine is removed from hello set.</span></span>

## <a name="set-up-scaling-using-azure-powershell"></a><span data-ttu-id="32421-191">Configuration de mise à l’échelle à l’aide d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="32421-191">Set up scaling using Azure PowerShell</span></span>

<span data-ttu-id="32421-192">les exemples de toosee d’utilisation de tooset PowerShell d’échelle, examinez [Azure PowerShell d’analyse rapide démarrer exemples](../monitoring-and-diagnostics/insights-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="32421-192">toosee examples of using PowerShell tooset up autoscaling, look at [Azure Monitor PowerShell quick start samples](../monitoring-and-diagnostics/insights-powershell-samples.md).</span></span>

## <a name="set-up-scaling-using-azure-cli"></a><span data-ttu-id="32421-193">Configuration de mise à l’échelle à l’aide de l’interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="32421-193">Set up scaling using Azure CLI</span></span>

<span data-ttu-id="32421-194">les exemples de toosee d’utilisation de tooset CLI d’Azure d’échelle, examinez [CLI de Cross-platform Azure analyse rapide démarrer exemples](../monitoring-and-diagnostics/insights-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="32421-194">toosee examples of using Azure CLI tooset up autoscaling, look at [Azure Monitor Cross-platform CLI quick start samples](../monitoring-and-diagnostics/insights-cli-samples.md).</span></span>

## <a name="set-up-scaling-using-hello-azure-portal"></a><span data-ttu-id="32421-195">Configurer la mise à l’échelle à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="32421-195">Set up scaling using hello Azure portal</span></span>

<span data-ttu-id="32421-196">toosee un exemple d’utilisation hello Azure tooset portail de l’échelle automatique, recherchez à [créer un ensemble de l’échelle de machines virtuelles à l’aide de hello Azure portal](virtual-machine-scale-sets-portal-create.md).</span><span class="sxs-lookup"><span data-stu-id="32421-196">toosee an example of using hello Azure portal tooset up autoscaling, look at [Create a Virtual Machine Scale Set using hello Azure portal](virtual-machine-scale-sets-portal-create.md).</span></span>

## <a name="investigate-scaling-actions"></a><span data-ttu-id="32421-197">Examiner les actions de mise à l’échelle</span><span class="sxs-lookup"><span data-stu-id="32421-197">Investigate scaling actions</span></span>

* <span data-ttu-id="32421-198">**Portail Azure**</span><span class="sxs-lookup"><span data-stu-id="32421-198">**Azure portal**</span></span>  
<span data-ttu-id="32421-199">Vous pouvez en obtenir une quantité limitée d’informations à l’aide du portail de hello.</span><span class="sxs-lookup"><span data-stu-id="32421-199">You can currently get a limited amount of information using hello portal.</span></span>

* <span data-ttu-id="32421-200">**Azure Resource Explorer**</span><span class="sxs-lookup"><span data-stu-id="32421-200">**Azure Resource Explorer**</span></span>  
<span data-ttu-id="32421-201">Cet outil est hello meilleur pour Explorer l’état actuel de hello de votre ensemble d’échelle.</span><span class="sxs-lookup"><span data-stu-id="32421-201">This tool is hello best for exploring hello current state of your scale set.</span></span> <span data-ttu-id="32421-202">Suivez ce chemin d’accès, et vous devez voir vue d’instance hello de montée en puissance hello définie que vous avez créé :</span><span class="sxs-lookup"><span data-stu-id="32421-202">Follow this path and you should see hello instance view of hello scale set that you created:</span></span>  
<span data-ttu-id="32421-203">**Abonnements &gt; {votre abonnement} &gt; resourceGroups &gt; {votre groupe de ressources} &gt; fournisseurs &gt; Microsoft.Compute &gt; virtualMachineScaleSets &gt; {votre groupe identique} &gt; virtualMachines**</span><span class="sxs-lookup"><span data-stu-id="32421-203">**Subscriptions > {your subscription} > resourceGroups > {your resource group} > providers > Microsoft.Compute > virtualMachineScaleSets > {your scale set} > virtualMachines**</span></span>

* <span data-ttu-id="32421-204">**Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="32421-204">**Azure PowerShell**</span></span>  
<span data-ttu-id="32421-205">Utilisez cette commande tooget certaines informations :</span><span class="sxs-lookup"><span data-stu-id="32421-205">Use this command tooget some information:</span></span>

  ```powershell
  Get-AzureRmResource -name vmsstest1 -ResourceGroupName vmsstestrg1 -ResourceType Microsoft.Compute/virtualMachineScaleSets -ApiVersion 2015-06-15
  Get-Autoscalesetting -ResourceGroup rainvmss -DetailedOutput
  ```

* <span data-ttu-id="32421-206">Se connecter toohello jumpbox virtuels comme vous le feriez pour n’importe quel autre ordinateur et vous pouvez ensuite accéder à distance virtuels hello dans toomonitor hello échelle ensemble des processus individuels.</span><span class="sxs-lookup"><span data-stu-id="32421-206">Connect toohello jumpbox virtual machine just like you would any other machine and then you can remotely access hello virtual machines in hello scale set toomonitor individual processes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="32421-207">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="32421-207">Next Steps</span></span>
* <span data-ttu-id="32421-208">Examinez [redimensionner automatiquement les ordinateurs dans un ensemble d’échelle de Machine virtuelle](virtual-machine-scale-sets-windows-autoscale.md) toosee un exemple de comment toocreate une ensemble d’échelle de la mise à l’échelle automatique configurée.</span><span class="sxs-lookup"><span data-stu-id="32421-208">Look at [Automatically scale machines in a Virtual Machine Scale Set](virtual-machine-scale-sets-windows-autoscale.md) toosee an example of how toocreate a scale set with automatic scaling configured.</span></span>

* <span data-ttu-id="32421-209">Découvrez des exemples de fonctionnalités de surveillance Azure Monitor dans les [exemples de démarrage rapide d’Azure Monitor PowerShell](../monitoring-and-diagnostics/insights-powershell-samples.md)</span><span class="sxs-lookup"><span data-stu-id="32421-209">Find examples of Azure Monitor monitoring features in [Azure Monitor PowerShell quick start samples](../monitoring-and-diagnostics/insights-powershell-samples.md)</span></span>

* <span data-ttu-id="32421-210">En savoir plus sur les fonctionnalités de notification de [utiliser échelle actions toosend par courrier électronique et webhook des notifications d’alerte dans le moniteur de Azure](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md).</span><span class="sxs-lookup"><span data-stu-id="32421-210">Learn about notification features in [Use autoscale actions toosend email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md).</span></span>

* <span data-ttu-id="32421-211">En savoir plus sur la façon de trop[toosend par courrier électronique et webhook des notifications d’alerte de les journaux d’audit d’utilisation dans le moniteur de Azure](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span><span class="sxs-lookup"><span data-stu-id="32421-211">Learn about how too[Use audit logs toosend email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span></span>

* <span data-ttu-id="32421-212">En savoir plus sur les [scénarios avancés de mise à l’échelle automatique](virtual-machine-scale-sets-advanced-autoscale.md).</span><span class="sxs-lookup"><span data-stu-id="32421-212">Learn about [advanced autoscale scenarios](virtual-machine-scale-sets-advanced-autoscale.md).</span></span>
