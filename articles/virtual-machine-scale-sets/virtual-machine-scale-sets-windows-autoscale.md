---
title: aaaAutoscale Windows machines virtuelles identiques | Documents Microsoft
description: "Mettre à l’échelle automatiquement un jeu de mise à l’échelle de machine virtuelle Windows à l’aide d’Azure PowerShell"
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 88886cad-a2f0-46bc-8b58-32ac2189fc93
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/27/2016
ms.author: adegeo
ms.openlocfilehash: 67cf1c5063ceba4fc076dc270090defdbddbcfe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-scale-machines-in-a-virtual-machine-scale-set"></a><span data-ttu-id="e1ddb-103">Mettre automatiquement à l’échelle des machines dans un jeu de mise à l’échelle de machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="e1ddb-103">Automatically scale machines in a virtual machine scale set</span></span>
<span data-ttu-id="e1ddb-104">Machines virtuelles identiques facilitent vous toodeploy et gérer des machines virtuelles identiques en tant qu’ensemble.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-104">Virtual machine scale sets make it easy for you toodeploy and manage identical virtual machines as a set.</span></span> <span data-ttu-id="e1ddb-105">Les groupes à échelle identique fournissent une couche de calcul hautement évolutive et personnalisable pour les applications « hyperscale », et prennent en charge les images de plateforme Windows, les images de plateforme Linux, des images personnalisées et les extensions.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-105">Scale sets provide a highly scalable and customizable compute layer for hyperscale applications, and they support Windows platform images, Linux platform images, custom images, and extensions.</span></span> <span data-ttu-id="e1ddb-106">Pour plus d’informations sur les jeux de mise à l’échelle, consultez [Jeux de mise à l’échelle de machine virtuelle](virtual-machine-scale-sets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e1ddb-106">For more information about scale sets, see [Virtual Machine Scale Sets](virtual-machine-scale-sets-overview.md).</span></span>

<span data-ttu-id="e1ddb-107">Ce didacticiel vous montre comment définie les toocreate un ensemble d’échelle de machines virtuelles Windows et de machines Bonjour Bonjour à l’échelle automatiquement.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-107">This tutorial shows you how toocreate a scale set of Windows virtual machines and automatically scale hello machines in hello set.</span></span> <span data-ttu-id="e1ddb-108">Vous créez la montée en puissance hello définir et configurer la mise à l’échelle en créant un modèle Azure Resource Manager et de déploiement à l’aide d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-108">You create hello scale set and set up scaling by creating an Azure Resource Manager template and deploying it using Azure PowerShell.</span></span> <span data-ttu-id="e1ddb-109">Pour en savoir plus sur les modèles, consultez [Création de modèles Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="e1ddb-109">For more information about templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span> <span data-ttu-id="e1ddb-110">toolearn en savoir plus sur la mise à l’échelle automatique de jeux de mise à l’échelle, consultez [mise à l’échelle automatique et mise à l’échelle de Machine virtuelle définit](virtual-machine-scale-sets-autoscale-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e1ddb-110">toolearn more about automatic scaling of scale sets, see [Automatic scaling and Virtual Machine Scale Sets](virtual-machine-scale-sets-autoscale-overview.md).</span></span>

<span data-ttu-id="e1ddb-111">Dans cet article, vous déployez des éléments suivants de hello extensions et ressources :</span><span class="sxs-lookup"><span data-stu-id="e1ddb-111">In this article, you deploy hello following resources and extensions:</span></span>

* <span data-ttu-id="e1ddb-112">Microsoft.Storage/storageAccounts</span><span class="sxs-lookup"><span data-stu-id="e1ddb-112">Microsoft.Storage/storageAccounts</span></span>
* <span data-ttu-id="e1ddb-113">Microsoft.Network/virtualNetworks</span><span class="sxs-lookup"><span data-stu-id="e1ddb-113">Microsoft.Network/virtualNetworks</span></span>
* <span data-ttu-id="e1ddb-114">Microsoft.Network/publicIPAddresses</span><span class="sxs-lookup"><span data-stu-id="e1ddb-114">Microsoft.Network/publicIPAddresses</span></span>
* <span data-ttu-id="e1ddb-115">Microsoft.Network/loadBalancers</span><span class="sxs-lookup"><span data-stu-id="e1ddb-115">Microsoft.Network/loadBalancers</span></span>
* <span data-ttu-id="e1ddb-116">Microsoft.Network/networkInterfaces</span><span class="sxs-lookup"><span data-stu-id="e1ddb-116">Microsoft.Network/networkInterfaces</span></span>
* <span data-ttu-id="e1ddb-117">Microsoft.Compute/virtualMachines</span><span class="sxs-lookup"><span data-stu-id="e1ddb-117">Microsoft.Compute/virtualMachines</span></span>
* <span data-ttu-id="e1ddb-118">Microsoft.Compute/virtualMachineScaleSets</span><span class="sxs-lookup"><span data-stu-id="e1ddb-118">Microsoft.Compute/virtualMachineScaleSets</span></span>
* <span data-ttu-id="e1ddb-119">Microsoft.Insights.VMDiagnosticsSettings</span><span class="sxs-lookup"><span data-stu-id="e1ddb-119">Microsoft.Insights.VMDiagnosticsSettings</span></span>
* <span data-ttu-id="e1ddb-120">Microsoft.Insights/autoscaleSettings</span><span class="sxs-lookup"><span data-stu-id="e1ddb-120">Microsoft.Insights/autoscaleSettings</span></span>

<span data-ttu-id="e1ddb-121">Pour plus d’informations sur les ressources Azure Manager, consultez [Déploiement Azure Resource Manager et déploiement classique](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="e1ddb-121">For more information about Resource Manager resources, see [Azure Resource Manager vs. classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>

## <a name="step-1-install-azure-powershell"></a><span data-ttu-id="e1ddb-122">Étape 1 : installer Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="e1ddb-122">Step 1: Install Azure PowerShell</span></span>
<span data-ttu-id="e1ddb-123">Consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview) pour plus d’informations sur l’installation de version la plus récente d’Azure PowerShell hello, en sélectionnant votre abonnement et la signature dans tooAzure.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-123">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for information about installing hello latest version of Azure PowerShell, selecting your subscription, and signing in tooAzure.</span></span>

## <a name="step-2-create-a-resource-group-and-a-storage-account"></a><span data-ttu-id="e1ddb-124">Étape 2 : créer un groupe de ressources et un compte de stockage</span><span class="sxs-lookup"><span data-stu-id="e1ddb-124">Step 2: Create a resource group and a storage account</span></span>
1. <span data-ttu-id="e1ddb-125">**Créer un groupe de ressources** – toutes les ressources doivent être le groupe de ressources tooa déployé.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-125">**Create a resource group** – All resources must be deployed tooa resource group.</span></span> <span data-ttu-id="e1ddb-126">Utilisez [New-AzureRmResourceGroup](https://msdn.microsoft.com/library/mt603739.aspx) toocreate un groupe de ressources nommé **vmsstestrg1**.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-126">Use [New-AzureRmResourceGroup](https://msdn.microsoft.com/library/mt603739.aspx) toocreate a resource group named **vmsstestrg1**.</span></span>
2. <span data-ttu-id="e1ddb-127">**Créer un compte de stockage** – ce compte de stockage consiste à stocker de modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-127">**Create a storage account** – This storage account is where hello template is stored.</span></span> <span data-ttu-id="e1ddb-128">Utilisez [New-AzureRmStorageAccount](https://msdn.microsoft.com/library/mt607148.aspx) toocreate un compte de stockage nommé **vmsstestsa**.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-128">Use [New-AzureRmStorageAccount](https://msdn.microsoft.com/library/mt607148.aspx) toocreate a storage account named **vmsstestsa**.</span></span>

## <a name="step-3-create-hello-template"></a><span data-ttu-id="e1ddb-129">Étape 3 : Créer le modèle de hello</span><span class="sxs-lookup"><span data-stu-id="e1ddb-129">Step 3: Create hello template</span></span>
<span data-ttu-id="e1ddb-130">Un modèle Azure Resource Manager rend possible pour vous toodeploy et gérer des ressources Azure ensemble à l’aide d’une description JSON des ressources de hello et des paramètres de déploiement associés.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-130">An Azure Resource Manager template makes it possible for you toodeploy and manage Azure resources together by using a JSON description of hello resources and associated deployment parameters.</span></span>

1. <span data-ttu-id="e1ddb-131">Dans votre éditeur favori, créer le fichier hello C:\VMSSTemplate.json et ajouter hello initiales JSON structure toosupport hello du modèle.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-131">In your favorite editor, create hello file C:\VMSSTemplate.json and add hello initial JSON structure toosupport hello template.</span></span>

    ```json
    {
      "$schema":"http://schema.management.azure.com/schemas/2014-04-01-preview/VM.json",
      "contentVersion": "1.0.0.0",
      "parameters": {
      },
      "variables": {
      },
      "resources": [
      ]
    }
    ```

2. <span data-ttu-id="e1ddb-132">Paramètres ne sont pas toujours nécessaires, mais ils fournissent un moyen tooinput valeurs lorsque le modèle de hello est déployé.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-132">Parameters are not always required, but they provide a way tooinput values when hello template is deployed.</span></span> <span data-ttu-id="e1ddb-133">Ajouter ces paramètres sous l’élément parent de hello paramètres que vous avez ajouté le modèle de toohello.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-133">Add these parameters under hello parameters parent element that you added toohello template.</span></span>

    ```json   
    "vmName": { "type": "string" },
    "vmSSName": { "type": "string" },
    "instanceCount": { "type": "string" },
    "adminUsername": { "type": "string" },
    "adminPassword": { "type": "securestring" },
    "resourcePrefix": { "type": "string" }
    ```
   
    * <span data-ttu-id="e1ddb-134">Un nom pour la machine virtuelle distincte hello constituant des machines de hello tooaccess utilisé dans l’ensemble d’échelle hello.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-134">A name for hello separate virtual machine that is used tooaccess hello machines in hello scale set.</span></span>
    * <span data-ttu-id="e1ddb-135">nom Hello hello du compte de stockage où se trouve le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-135">hello name of hello storage account where hello template is stored.</span></span>
    * <span data-ttu-id="e1ddb-136">nombre de Hello de machines virtuelles tooinitially créer dans un ensemble d’échelle hello.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-136">hello number of virtual machines tooinitially create in hello scale set.</span></span>
    * <span data-ttu-id="e1ddb-137">nom de Hello et le mot de passe du compte d’administrateur hello sur des machines virtuelles de hello.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-137">hello name and password of hello administrator account on hello virtual machines.</span></span>
    * <span data-ttu-id="e1ddb-138">Un préfixe de nom pour les ressources hello qui sont créés à l’échelle de hello toosupport définie.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-138">A name prefix for hello resources that are created toosupport hello scale set.</span></span>

3. <span data-ttu-id="e1ddb-139">Variables peuvent être utilisées dans un valeurs toospecify de modèle qui changent fréquemment ou les valeurs qui doivent toobe créées à partir d’une combinaison de valeurs de paramètre.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-139">Variables can be used in a template toospecify values that may change frequently or values that need toobe created from a combination of parameter values.</span></span> <span data-ttu-id="e1ddb-140">Ajoutez ces variables sous l’élément parent de hello variables que vous avez ajouté le modèle de toohello.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-140">Add these variables under hello variables parent element that you added toohello template.</span></span>

    ```json
    "dnsName1": "[concat(parameters('resourcePrefix'),'dn1')]",
    "dnsName2": "[concat(parameters('resourcePrefix'),'dn2')]",
    "publicIP1": "[concat(parameters('resourcePrefix'),'ip1')]",
    "publicIP2": "[concat(parameters('resourcePrefix'),'ip2')]",
    "loadBalancerName": "[concat(parameters('resourcePrefix'),'lb1')]",
    "virtualNetworkName": "[concat(parameters('resourcePrefix'),'vn1')]",
    "nicName": "[concat(parameters('resourcePrefix'),'nc1')]",
    "lbID": "[resourceId('Microsoft.Network/loadBalancers',variables('loadBalancerName'))]",
    "frontEndIPConfigID": "[concat(variables('lbID'),'/frontendIPConfigurations/loadBalancerFrontEnd')]",
    "storageAccountSuffix": [ "a", "g", "m", "s", "y" ],
    "diagnosticsStorageAccountName": "[concat(parameters('resourcePrefix'), 'a')]",
    "accountid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/', resourceGroup().name,'/providers/','Microsoft.Storage/storageAccounts/', variables('diagnosticsStorageAccountName'))]",
      "wadlogs": "<WadCfg> <DiagnosticMonitorConfiguration overallQuotaInMB=\"4096\" xmlns=\"http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration\"> <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter=\"Error\"/> <WindowsEventLog scheduledTransferPeriod=\"PT1M\" > <DataSource name=\"Application!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"Security!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"System!*[System[(Level = 1 or Level = 2)]]\" /></WindowsEventLog>",
    "wadperfcounter": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\"><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\% Processor Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"CPU utilization\" locale=\"en-us\"/></PerformanceCounterConfiguration></PerformanceCounters>",
    "wadcfgxstart": "[concat(variables('wadlogs'),variables('wadperfcounter'),'<Metrics resourceId=\"')]",
    "wadmetricsresourceid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name ,'/providers/','Microsoft.Compute/virtualMachineScaleSets/',parameters('vmssName'))]",
    "wadcfgxend": "[concat('\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/><MetricAggregation scheduledTransferPeriod=\"PT1M\"/></Metrics></DiagnosticMonitorConfiguration></WadCfg>')]"
    ```
   
    * <span data-ttu-id="e1ddb-141">Noms DNS qui sont utilisés par les interfaces réseau hello.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-141">DNS names that are used by hello network interfaces.</span></span>

        * <span data-ttu-id="e1ddb-142">les noms d’adresses IP Hello et préfixes pour le réseau virtuel de hello et sous-réseaux.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-142">hello IP address names and prefixes for hello virtual network and subnets.</span></span>
        * <span data-ttu-id="e1ddb-143">Hello noms et les identificateurs de réseau virtuel de hello, équilibreur de charge et les interfaces réseau.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-143">hello names and identifiers of hello virtual network, load balancer, and network interfaces.</span></span>
        * <span data-ttu-id="e1ddb-144">Noms de compte de stockage pour les comptes de hello associés avec des machines hello dans un ensemble d’échelle hello.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-144">Storage account names for hello accounts associated with hello machines in hello scale set.</span></span>
        * <span data-ttu-id="e1ddb-145">Paramètres de hello extension de Diagnostics qui est installée sur les ordinateurs virtuels de hello.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-145">Settings for hello Diagnostics extension that is installed on hello virtual machines.</span></span> <span data-ttu-id="e1ddb-146">Pour plus d’informations sur l’extension des Diagnostics de hello, consultez [créer une machine virtuelle Windows avec l’analyse et de diagnostics à l’aide du modèle de gestionnaire de ressources Azure](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e1ddb-146">For more information about hello Diagnostics extension, see [Create a Windows Virtual machine with monitoring and diagnostics using Azure Resource Manager Template](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

4. <span data-ttu-id="e1ddb-147">Ajouter une ressource de compte de stockage hello sous l’élément parent de hello ressources que vous avez ajouté le modèle de toohello.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-147">Add hello storage account resource under hello resources parent element that you added toohello template.</span></span> <span data-ttu-id="e1ddb-148">Ce modèle utilise un Bonjour toocreate de boucle recommandé cinq comptes de stockage où sont stockées les disques du système d’exploitation hello et les données de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-148">This template uses a loop toocreate hello recommended five storage accounts where hello operating system disks and diagnostic data are stored.</span></span> <span data-ttu-id="e1ddb-149">Cet ensemble de comptes peut prendre en charge les machines virtuelles de too100 dans un ensemble d’échelle, qui est la valeur maximale actuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-149">This set of accounts can support up too100 virtual machines in a scale set, which is hello current maximum.</span></span> <span data-ttu-id="e1ddb-150">Chaque compte de stockage est nommé avec un indicateur de lettre qui a été défini dans les variables hello combinés avec le préfixe hello que vous fournissez dans les paramètres de hello pour le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-150">Each storage account is named with a letter designator that was defined in hello variables combined with hello prefix that you provide in hello parameters for hello template.</span></span>

    ```json
    {
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[concat(parameters('resourcePrefix'), variables('storageAccountSuffix')[copyIndex()])]",
      "apiVersion": "2015-06-15",
      "copy": {
        "name": "storageLoop",
        "count": 5
      },
      "location": "[resourceGroup().location]",
      "properties": { "accountType": "Standard_LRS" }
    },
    ```

5. <span data-ttu-id="e1ddb-151">Ajouter une ressource de réseau virtuel hello.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-151">Add hello virtual network resource.</span></span> <span data-ttu-id="e1ddb-152">Pour plus d’informations, consultez [Fournisseurs de ressources réseau](../virtual-network/resource-groups-networking.md).</span><span class="sxs-lookup"><span data-stu-id="e1ddb-152">For more information, see [Network Resource Provider](../virtual-network/resource-groups-networking.md).</span></span>

    ```json
    {
      "apiVersion": "2015-06-15",
      "type": "Microsoft.Network/virtualNetworks",
      "name": "[variables('virtualNetworkName')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "addressSpace": { "addressPrefixes": [ "10.0.0.0/16" ] },
        "subnets": [
          {
            "name": "subnet1",
            "properties": { "addressPrefix": "10.0.0.0/24" }
          }
        ]
      }
    },
    ```

6. <span data-ttu-id="e1ddb-153">Ajoutez hello publiques ressources d’adresse IP qui sont utilisés par hello équilibreur de charge et interface réseau.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-153">Add hello public IP address resources that are used by hello load balancer and network interface.</span></span>

    ```json
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Network/publicIPAddresses",
      "name": "[variables('publicIP1')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "publicIPAllocationMethod": "Dynamic",
        "dnsSettings": {
          "domainNameLabel": "[variables('dnsName1')]"
        }
      }
    },
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Network/publicIPAddresses",
      "name": "[variables('publicIP2')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "publicIPAllocationMethod": "Dynamic",
        "dnsSettings": {
          "domainNameLabel": "[variables('dnsName2')]"
        }
      }
    },
    ```

7. <span data-ttu-id="e1ddb-154">Ajouter une ressource d’équilibrage de charge hello qui est utilisé par un ensemble d’échelle hello.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-154">Add hello load balancer resource that is used by hello scale set.</span></span> <span data-ttu-id="e1ddb-155">Pour plus d’informations, consultez [Prise en charge d’un équilibreur de charge par Azure Resource Manager](../load-balancer/load-balancer-arm.md)</span><span class="sxs-lookup"><span data-stu-id="e1ddb-155">For more information, see [Azure Resource Manager Support for Load Balancer](../load-balancer/load-balancer-arm.md).</span></span>

    ```json   
    {
      "apiVersion": "2015-06-15",
      "name": "[variables('loadBalancerName')]",
      "type": "Microsoft.Network/loadBalancers",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIP1'))]"
      ],
      "properties": {
        "frontendIPConfigurations": [
          {
            "name": "loadBalancerFrontEnd",
            "properties": {
              "publicIPAddress": {
                "id": "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIP1'))]"
              }
            }
          }
        ],
        "backendAddressPools": [ { "name": "bepool1" } ],
        "inboundNatPools": [
          {
            "name": "natpool1",
            "properties": {
              "frontendIPConfiguration": {
                "id": "[variables('frontEndIPConfigID')]"
              },
              "protocol": "tcp",
              "frontendPortRangeStart": 50000,
              "frontendPortRangeEnd": 50500,
              "backendPort": 3389
            }
          }
        ]
      }
    },
    ```

8. <span data-ttu-id="e1ddb-156">Ajouter la ressource d’interface réseau hello qui est utilisé par la machine virtuelle distincte de hello.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-156">Add hello network interface resource that is used by hello separate virtual machine.</span></span> <span data-ttu-id="e1ddb-157">Étant donné que les ordinateurs dans un ensemble d’échelle ne sont pas accessibles via une adresse IP publique, un ordinateur virtuel distinct est créé dans hello même virtuel réseau tooremotely accès hello machines.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-157">Because machines in a scale set aren't accessible through a public IP address, a separate virtual machine is created in hello same virtual network tooremotely access hello machines.</span></span>

    ```json  
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[variables('nicName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIP2'))]",
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
      ],
      "properties": {
        "ipConfigurations": [
          {
            "name": "ipconfig1",
            "properties": {
              "privateIPAllocationMethod": "Dynamic",
              "publicIPAddress": {
                "id": "[resourceId('Microsoft.Network/publicIPAddresses', variables('publicIP2'))]"
              },
              "subnet": {
                "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/virtualNetworks/',variables('virtualNetworkName'),'/subnets/subnet1')]"
              }
            }
          }
        ]
      }
    },
    ```

9. <span data-ttu-id="e1ddb-158">Ajouter la machine virtuelle distincte de hello Bonjour même réseau que l’ensemble d’échelle hello.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-158">Add hello separate virtual machine in hello same network as hello scale set.</span></span>

    ```json
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Compute/virtualMachines",
      "name": "[parameters('vmName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "storageLoop",
        "[concat('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
      ],
      "properties": {
        "hardwareProfile": { "vmSize": "Standard_A1" },
        "osProfile": {
          "computername": "[parameters('vmName')]",
          "adminUsername": "[parameters('adminUsername')]",
          "adminPassword": "[parameters('adminPassword')]"
        },
        "storageProfile": {
          "imageReference": {
            "publisher": "MicrosoftWindowsServer",
            "offer": "WindowsServer",
            "sku": "2012-R2-Datacenter",
            "version": "latest"
          },
          "osDisk": {
            "name": "[concat(parameters('resourcePrefix'), 'os1')]",
            "vhd": {
              "uri":  "[concat('https://',parameters('resourcePrefix'),'a.blob.core.windows.net/vhds/',parameters('resourcePrefix'),'os1.vhd')]"
            },
            "caching": "ReadWrite",
            "createOption": "FromImage"        
          }
        },
        "networkProfile": {
          "networkInterfaces": [
            {
              "id": "[resourceId('Microsoft.Network/networkInterfaces',variables('nicName'))]"
            }
          ]
        }
      }
    },
    ```

10. <span data-ttu-id="e1ddb-159">Ajouter l’ensemble d’échelle de machine virtuelle hello de ressource et spécifiez l’extension diagnostics hello qui est installée sur tous les ordinateurs virtuels dans un ensemble d’échelle hello.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-159">Add hello virtual machine scale set resource and specify hello diagnostics extension that is installed on all virtual machines in hello scale set.</span></span> <span data-ttu-id="e1ddb-160">La plupart des paramètres hello pour cette ressource sont similaires avec la ressource d’ordinateur virtuel hello.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-160">Many of hello settings for this resource are similar with hello virtual machine resource.</span></span> <span data-ttu-id="e1ddb-161">Hello principales différences sont les élément capacité hello qui spécifie le nombre de hello d’ordinateurs virtuels dans un ensemble d’échelle hello et upgradePolicy qui spécifie comment les mises à jour sont effectuées toovirtual machines.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-161">hello main differences are hello capacity element that specifies hello number of virtual machines in hello scale set, and upgradePolicy that specifies how updates are made toovirtual machines.</span></span> <span data-ttu-id="e1ddb-162">Hello ensemble d’échelle n’est pas créé tant que tous les comptes de stockage hello sont créés comme spécifié avec l’élément dependsOn de hello.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-162">hello scale set is not created until all hello storage accounts are created as specified with hello dependsOn element.</span></span>

    ```json
    {
      "type": "Microsoft.Compute/virtualMachineScaleSets",
      "apiVersion": "2016-03-30",
      "name": "[parameters('vmSSName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "storageLoop",
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]",
        "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]"
      ],
      "sku": {
        "name": "Standard_A1",
        "tier": "Standard",
        "capacity": "[parameters('instanceCount')]"
      },
      "properties": {
        "upgradePolicy": {
          "mode": "Manual"
        },
        "virtualMachineProfile": {
          "storageProfile": {
            "osDisk": {
              "vhdContainers": [
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[0], '.blob.core.windows.net/vhds')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[1], '.blob.core.windows.net/vhds')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[2], '.blob.core.windows.net/vhds')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[3], '.blob.core.windows.net/vhds')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[4], '.blob.core.windows.net/vhds')]"
              ],
              "name": "vmssosdisk",
              "caching": "ReadOnly",
              "createOption": "FromImage"
            },
            "imageReference": {
              "publisher": "MicrosoftWindowsServer",
              "offer": "WindowsServer",
              "sku": "2012-R2-Datacenter",
              "version": "latest"
            }
          },
          "osProfile": {
            "computerNamePrefix": "[parameters('vmSSName')]",
            "adminUsername": "[parameters('adminUsername')]",
            "adminPassword": "[parameters('adminPassword')]"
          },
          "networkProfile": {
            "networkInterfaceConfigurations": [
              {
                "name": "networkconfig1",
                "properties": {
                  "primary": "true",
                  "ipConfigurations": [
                    {
                      "name": "ip1",
                      "properties": {
                        "subnet": {
                          "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/virtualNetworks/',variables('virtualNetworkName'),'/subnets/subnet1')]"
                        },
                        "loadBalancerBackendAddressPools": [
                          {
                            "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/loadBalancers/',variables('loadBalancerName'),'/backendAddressPools/bepool1')]"
                          }
                        ],
                        "loadBalancerInboundNatPools": [
                          {
                            "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/loadBalancers/',variables('loadBalancerName'),'/inboundNatPools/natpool1')]"
                          }
                        ]
                      }
                    }
                  ]
                }
              }
            ]
          },
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
                    "storageAccountKey": "[listkeys(variables('accountid'), '2015-06-15').key1]",
                    "storageAccountEndPoint": "https://core.windows.net"
                  }
                }
              }
            ]
          }
        }
      }
    },
    ```

11. <span data-ttu-id="e1ddb-163">Ajouter une ressource autoscaleSettings hello qui définit comment l’ensemble d’échelle hello s’ajuste en fonction de l’utilisation du processeur sur les ordinateurs hello dans un ensemble d’échelle hello hello.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-163">Add hello autoscaleSettings resource that defines how hello scale set adjusts based on hello processor usage on hello machines in hello scale set.</span></span>

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
                  "metricName": "\\Processor(_Total)\\% Processor Time",
                  "metricNamespace": "",
                  "metricResourceUri": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]",
                  "timeGrain": "PT1M",
                  "statistic": "Average",
                  "timeWindow": "PT5M",
                  "timeAggregation": "Average",
                  "operator": "GreaterThan",
                  "threshold": 50.0
                },
                "scaleAction": {
                  "direction": "Increase",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              }
            ]
          }
        ],
        "targetResourceUri": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/', resourceGroup().name,'/providers/Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]"
      }
    }
    ```

    <span data-ttu-id="e1ddb-164">Pour ce didacticiel, les valeurs suivantes sont importantes :</span><span class="sxs-lookup"><span data-stu-id="e1ddb-164">For this tutorial, these values are important:</span></span>
    
    * <span data-ttu-id="e1ddb-165">**metricName**</span><span class="sxs-lookup"><span data-stu-id="e1ddb-165">**metricName**</span></span>  
    <span data-ttu-id="e1ddb-166">Cette valeur est hello identique au compteur de performance hello que nous avons défini dans la variable de wadperfcounter hello.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-166">This value is hello same as hello performance counter that we defined in hello wadperfcounter variable.</span></span> <span data-ttu-id="e1ddb-167">À l’aide de cette variable, hello extension Diagnostics collecte hello **processeur (_Total)\% temps processeur** compteur.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-167">Using that variable, hello Diagnostics extension collects hello  **Processor(_Total)\% Processor Time** counter.</span></span>
    
    * <span data-ttu-id="e1ddb-168">**metricResourceUri**</span><span class="sxs-lookup"><span data-stu-id="e1ddb-168">**metricResourceUri**</span></span>  
    <span data-ttu-id="e1ddb-169">Cette valeur est l’identificateur de ressource de hello de hello machines virtuelles identiques.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-169">This value is hello resource identifier of hello virtual machine scale set.</span></span>
    
    * <span data-ttu-id="e1ddb-170">**timeGrain**</span><span class="sxs-lookup"><span data-stu-id="e1ddb-170">**timeGrain**</span></span>  
    <span data-ttu-id="e1ddb-171">Cette valeur est la granularité hello des métriques de hello sont collectés.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-171">This value is hello granularity of hello metrics that are collected.</span></span> <span data-ttu-id="e1ddb-172">Dans ce modèle, il a la valeur tooone minute.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-172">In this template, it is set tooone minute.</span></span>
    
    * <span data-ttu-id="e1ddb-173">**statistic**</span><span class="sxs-lookup"><span data-stu-id="e1ddb-173">**statistic**</span></span>  
    <span data-ttu-id="e1ddb-174">Cette valeur détermine comment les métriques de hello sont hello tooaccommodate combinée automatique d’action de mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-174">This value determines how hello metrics are combined tooaccommodate hello automatic scaling action.</span></span> <span data-ttu-id="e1ddb-175">Hello les valeurs possibles sont : moyenne, Min, Max.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-175">hello possible values are: Average, Min, Max.</span></span> <span data-ttu-id="e1ddb-176">Dans ce modèle, hello total utilisation moyenne du processeur d’ordinateurs virtuels hello est collectée.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-176">In this template, hello average total CPU usage of hello virtual machines is collected.</span></span>
    
    * <span data-ttu-id="e1ddb-177">**timeWindow**</span><span class="sxs-lookup"><span data-stu-id="e1ddb-177">**timeWindow**</span></span>  
    <span data-ttu-id="e1ddb-178">Cette valeur est la plage de hello de temps dans laquelle les données d’instance sont collectées.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-178">This value is hello range of time in which instance data is collected.</span></span> <span data-ttu-id="e1ddb-179">Elle doit être comprise entre 5 minutes et 12 heures.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-179">It must be between 5 minutes and 12 hours.</span></span>
    
    * <span data-ttu-id="e1ddb-180">**timeAggregation**</span><span class="sxs-lookup"><span data-stu-id="e1ddb-180">**timeAggregation**</span></span>  
    <span data-ttu-id="e1ddb-181">sa valeur détermine l’association de données hello collectées au fil du temps.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-181">his value determines how hello data that is collected should be combined over time.</span></span> <span data-ttu-id="e1ddb-182">valeur par défaut de Hello est moyenne.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-182">hello default value is Average.</span></span> <span data-ttu-id="e1ddb-183">Hello les valeurs possibles sont : moyenne, Minimum, Maximum, dernier, Total, le nombre.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-183">hello possible values are: Average, Minimum, Maximum, Last, Total, Count.</span></span>
    
    * <span data-ttu-id="e1ddb-184">**operator**</span><span class="sxs-lookup"><span data-stu-id="e1ddb-184">**operator**</span></span>  
    <span data-ttu-id="e1ddb-185">Cette valeur est un opérateur hello toocompare utilisé hello métrique données et hello du seuil.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-185">This value is hello operator that is used toocompare hello metric data and hello threshold.</span></span> <span data-ttu-id="e1ddb-186">Hello les valeurs possibles sont : Equals, NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-186">hello possible values are: Equals, NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.</span></span>
    
    * <span data-ttu-id="e1ddb-187">**threshold**</span><span class="sxs-lookup"><span data-stu-id="e1ddb-187">**threshold**</span></span>  
    <span data-ttu-id="e1ddb-188">Cette valeur est hello qui déclenche l’action de mise à l’échelle hello.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-188">This value is hello value that triggers hello scale action.</span></span> <span data-ttu-id="e1ddb-189">Dans ce modèle, les ordinateurs sont ajoutés échelle toohello définie lors de l’utilisation moyenne du processeur hello entre les ordinateurs dans le jeu de hello est supérieure à 50 %.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-189">In this template, machines are added toohello scale set when hello average CPU usage among machines in hello set is over 50%.</span></span>
    
    * <span data-ttu-id="e1ddb-190">**direction**</span><span class="sxs-lookup"><span data-stu-id="e1ddb-190">**direction**</span></span>  
    <span data-ttu-id="e1ddb-191">Cette valeur détermine l’action hello qui est effectuée lorsque la valeur de seuil hello est atteint.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-191">This value determines hello action that is taken when hello threshold value is achieved.</span></span> <span data-ttu-id="e1ddb-192">les valeurs possibles de Hello sont augmentent ou diminuent.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-192">hello possible values are Increase or Decrease.</span></span> <span data-ttu-id="e1ddb-193">Dans ce modèle, hello nombre d’ordinateurs virtuels dans un ensemble d’échelle hello est augmenté si le seuil de hello est supérieure à 50 % dans la fenêtre de temps hello défini.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-193">In this template, hello number of virtual machines in hello scale set is increased if hello threshold is over 50% in hello defined time window.</span></span>
    
    * <span data-ttu-id="e1ddb-194">**type**</span><span class="sxs-lookup"><span data-stu-id="e1ddb-194">**type**</span></span>  
    <span data-ttu-id="e1ddb-195">Cette valeur est de type hello d’action qui doit se produire et doit avoir la valeur tooChangeCount.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-195">This value is hello type of action that should occur and must be set tooChangeCount.</span></span>
    
    * <span data-ttu-id="e1ddb-196">**value**</span><span class="sxs-lookup"><span data-stu-id="e1ddb-196">**value**</span></span>  
    <span data-ttu-id="e1ddb-197">Cette valeur est le nombre de hello d’ordinateurs virtuels qui sont ajoutés ou supprimés à partir d’un ensemble d’échelle hello.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-197">This value is hello number of virtual machines that are added or removed from hello scale set.</span></span> <span data-ttu-id="e1ddb-198">Cette valeur doit être définie sur 1 ou supérieur.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-198">This value must be 1 or greater.</span></span> <span data-ttu-id="e1ddb-199">Hello par défaut est 1.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-199">hello default value is 1.</span></span> <span data-ttu-id="e1ddb-200">Dans ce modèle, nombre de hello d’ordinateurs dans l’échelle de hello jeu augmente de 1 lorsque hello seuil est atteint.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-200">In this template, hello number of machines in hello scale set increases by 1 when hello threshold is met.</span></span>
    
    * <span data-ttu-id="e1ddb-201">**cooldown**</span><span class="sxs-lookup"><span data-stu-id="e1ddb-201">**cooldown**</span></span>  
    <span data-ttu-id="e1ddb-202">Cette valeur est hello toowait de temps depuis la dernière action de mise à l’échelle hello avant l’action suivante de hello se produit.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-202">This value is hello amount of time toowait since hello last scaling action before hello next action occurs.</span></span> <span data-ttu-id="e1ddb-203">Elle doit être comprise entre une minute et une semaine.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-203">This value must be between one minute and one week.</span></span>

12. <span data-ttu-id="e1ddb-204">Enregistrez le fichier de modèle hello.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-204">Save hello template file.</span></span>    

## <a name="step-4-upload-hello-template-toostorage"></a><span data-ttu-id="e1ddb-205">Étape 4 : Télécharger hello modèle toostorage</span><span class="sxs-lookup"><span data-stu-id="e1ddb-205">Step 4: Upload hello template toostorage</span></span>
<span data-ttu-id="e1ddb-206">modèle de Hello peut être téléchargé en tant que vous connaissez le nom de hello et une clé primaire hello du compte de stockage que vous avez créé à l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-206">hello template can be uploaded as long as you know hello name and primary key of hello storage account that you created in step 1.</span></span>

1. <span data-ttu-id="e1ddb-207">Dans la fenêtre de Microsoft Azure PowerShell hello, définissez une variable qui spécifie le nom hello hello du compte de stockage que vous avez créé à l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-207">In hello Microsoft Azure PowerShell window, set a variable that specifies hello name of hello storage account that you created in step 1.</span></span>
   
    ```powershell
    $storageAccountName = "vmstestsa"
    ```

2. <span data-ttu-id="e1ddb-208">Définir une variable qui spécifie la clé primaire de hello hello du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-208">Set a variable that specifies hello primary key of hello storage account.</span></span>
   
    ```powershell
    $storageAccountKey = "<primary-account-key>"
    ```
   
   <span data-ttu-id="e1ddb-209">Vous pouvez obtenir cette clé en cliquant sur icône de clé hello lors de l’affichage des ressources de compte de stockage hello Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-209">You can get this key by clicking hello key icon when viewing hello storage account resource in hello Azure portal.</span></span>
3. <span data-ttu-id="e1ddb-210">Créer un objet de contexte de compte de stockage de hello est opérations toovalidate utilisé avec le compte de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-210">Create hello storage account context object that is used toovalidate operations with hello storage account.</span></span>
   
    ```powershell
    $ctx = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey
    ```

4. <span data-ttu-id="e1ddb-211">Créer un conteneur hello pour le stockage hello modèle.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-211">Create hello container for storing hello template.</span></span>

    ```powershell
    $containerName = "templates"
    New-AzureStorageContainer -Name $containerName -Context $ctx  -Permission Blob
    ```

5. <span data-ttu-id="e1ddb-212">Télécharger un nouveau conteneur hello modèle fichier toohello.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-212">Upload hello template file toohello new container.</span></span>

    ```powershell   
    $blobName = "VMSSTemplate.json"
    $fileName = "C:\" + $BlobName
    Set-AzureStorageBlobContent -File $fileName -Container $containerName -Blob  $blobName -Context $ctx
    ```

## <a name="step-5-deploy-hello-template"></a><span data-ttu-id="e1ddb-213">Étape 5 : Déployer le modèle de hello</span><span class="sxs-lookup"><span data-stu-id="e1ddb-213">Step 5: Deploy hello template</span></span>
<span data-ttu-id="e1ddb-214">Maintenant que vous avez créé le modèle de hello, vous pouvez commencer à déployer des ressources de hello.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-214">Now that you created hello template, you can start deploying hello resources.</span></span> <span data-ttu-id="e1ddb-215">Utilisez ce processus de hello toostart commande :</span><span class="sxs-lookup"><span data-stu-id="e1ddb-215">Use this command toostart hello process:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name "vmsstestdp1" -ResourceGroupName "vmsstestrg1" -TemplateUri "https://vmsstestsa.blob.core.windows.net/templates/VMSSTemplate.json"
```

<span data-ttu-id="e1ddb-216">Lorsque vous appuyez sur, entrez, vous sont des valeurs de tooprovide demandées pour les variables hello que vous affectés.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-216">When you press enter, you are prompted tooprovide values for hello variables you assigned.</span></span> <span data-ttu-id="e1ddb-217">Remplacez les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="e1ddb-217">Provide these values:</span></span>

```powershell
vmName: vmsstestvm1
  vmSSName: vmsstest1
  instanceCount: 5
  adminUserName: vmadmin1
  adminPassword: VMpass1
  resourcePrefix: vmsstest
```

<span data-ttu-id="e1ddb-218">Il doit prendre environ 15 minutes pour tous les toosuccessfully de ressources hello être déployé.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-218">It should take about 15 minutes for all hello resources toosuccessfully be deployed.</span></span>

> [!NOTE]
> <span data-ttu-id="e1ddb-219">Vous pouvez également utiliser les ressources de hello du portail hello capacité toodeploy.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-219">You can also use hello portal’s ability toodeploy hello resources.</span></span> <span data-ttu-id="e1ddb-220">Utilisez le lien suivant : « https://portal.azure.com/#create/Microsoft.Template/uri/<link tooVM Scale Set JSON template>»</span><span class="sxs-lookup"><span data-stu-id="e1ddb-220">Use this link: "https://portal.azure.com/#create/Microsoft.Template/uri/<link tooVM Scale Set JSON template>"</span></span>
> 
> 

## <a name="step-6-monitor-resources"></a><span data-ttu-id="e1ddb-221">Étape 6 : surveiller les ressources</span><span class="sxs-lookup"><span data-stu-id="e1ddb-221">Step 6: Monitor resources</span></span>
<span data-ttu-id="e1ddb-222">Vous pouvez obtenir des informations sur les jeux de mise à l’échelle de machine virtuelle à l’aide des méthodes suivantes :</span><span class="sxs-lookup"><span data-stu-id="e1ddb-222">You can get some information about virtual machine scale sets using these methods:</span></span>

* <span data-ttu-id="e1ddb-223">Hello portail Azure, vous pouvez obtenir actuellement une quantité limitée d’informations à l’aide du portail de hello.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-223">hello Azure portal - You can currently get a limited amount of information using hello portal.</span></span>
* <span data-ttu-id="e1ddb-224">Hello [Explorateur de ressources Azure](https://resources.azure.com/) -cet outil est hello meilleur pour Explorer l’état actuel de hello de votre ensemble d’échelle.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-224">hello [Azure Resource Explorer](https://resources.azure.com/) - This tool is hello best for exploring hello current state of your scale set.</span></span> <span data-ttu-id="e1ddb-225">Suivez ce chemin d’accès, et vous devez voir vue d’instance hello de montée en puissance hello définie que vous avez créé :</span><span class="sxs-lookup"><span data-stu-id="e1ddb-225">Follow this path and you should see hello instance view of hello scale set that you created:</span></span>
  
    <span data-ttu-id="e1ddb-226">abonnements > {votre abonnement} > resourceGroups > vmsstestrg1 > fournisseurs > Microsoft.Compute > virtualMachineScaleSets > vmsstest1 > virtualMachines</span><span class="sxs-lookup"><span data-stu-id="e1ddb-226">subscriptions > {your subscription} > resourceGroups > vmsstestrg1 > providers > Microsoft.Compute > virtualMachineScaleSets > vmsstest1 > virtualMachines</span></span>

* <span data-ttu-id="e1ddb-227">Azure PowerShell - Utilisez cette tooget commande certaines informations :</span><span class="sxs-lookup"><span data-stu-id="e1ddb-227">Azure PowerShell - Use this command tooget some information:</span></span>

  ```powershell
  Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name"
  ```
  
  <span data-ttu-id="e1ddb-228">Ou</span><span class="sxs-lookup"><span data-stu-id="e1ddb-228">Or</span></span>
  
  ```powershell
  Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceView
  ```

* <span data-ttu-id="e1ddb-229">Se connecter machine virtuelle distincte de toohello comme vous le feriez pour n’importe quel autre ordinateur et vous pouvez ensuite accéder à distance virtuels hello dans toomonitor hello échelle ensemble des processus individuels.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-229">Connect toohello separate virtual machine just like you would any other machine and then you can remotely access hello virtual machines in hello scale set toomonitor individual processes.</span></span>

> [!NOTE]
> <span data-ttu-id="e1ddb-230">Vous trouverez une API REST complète permettant d’obtenir des informations sur les jeux de mise à l’échelle dans [Ensembles de mise à l’échelle de machine virtuelle](https://msdn.microsoft.com/library/mt589023.aspx)</span><span class="sxs-lookup"><span data-stu-id="e1ddb-230">A complete REST API for obtaining information about scale sets can be found in [Virtual Machine Scale Sets](https://msdn.microsoft.com/library/mt589023.aspx)</span></span>

## <a name="step-7-remove-hello-resources"></a><span data-ttu-id="e1ddb-231">Étape 7 : Supprimer des ressources de hello</span><span class="sxs-lookup"><span data-stu-id="e1ddb-231">Step 7: Remove hello resources</span></span>
<span data-ttu-id="e1ddb-232">Vous êtes facturé pour les ressources utilisées dans Azure, il est toujours ressource toodelete bonnes pratiques qui n’est plus nécessaires.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-232">Because you are charged for resources used in Azure, it is always a good practice toodelete resources that are no longer needed.</span></span> <span data-ttu-id="e1ddb-233">Vous n’avez pas besoin toodelete chaque ressource séparément à partir d’un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-233">You don’t need toodelete each resource separately from a resource group.</span></span> <span data-ttu-id="e1ddb-234">Vous pouvez supprimer le groupe de ressources hello et toutes ses ressources sont automatiquement supprimés.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-234">You can delete hello resource group and all its resources are automatically deleted.</span></span>

  ```powershell
  Remove-AzureRmResourceGroup -Name vmsstestrg1
  ```

<span data-ttu-id="e1ddb-235">Si vous souhaitez tookeep votre groupe de ressources, vous pouvez supprimer uniquement à la définition de la montée en puissance hello.</span><span class="sxs-lookup"><span data-stu-id="e1ddb-235">If you want tookeep your resource group, you can delete hello scale set only.</span></span>

  ```powershell
  Remove-AzureRmVmss -ResourceGroupName "resource group name" –VMScaleSetName "scale set name"
  ```

## <a name="next-steps"></a><span data-ttu-id="e1ddb-236">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e1ddb-236">Next steps</span></span>
* <span data-ttu-id="e1ddb-237">Gérer ensemble d’échelle hello que vous venez de créée à l’aide des informations de hello dans [gérer des ordinateurs virtuels dans un ensemble d’échelle de Machine virtuelle](virtual-machine-scale-sets-windows-manage.md).</span><span class="sxs-lookup"><span data-stu-id="e1ddb-237">Manage hello scale set that you just created using hello information in [Manage virtual machines in a Virtual Machine Scale Set](virtual-machine-scale-sets-windows-manage.md).</span></span>
* <span data-ttu-id="e1ddb-238">En savoir plus sur la mise à l’échelle verticale en consultant l’article [Mise à l’échelle verticale avec des jeux de mise à l’échelle de machines virtuelles](virtual-machine-scale-sets-vertical-scale-reprovision.md)</span><span class="sxs-lookup"><span data-stu-id="e1ddb-238">Learn more about vertical scaling by reviewing [Vertical autoscale with Virtual Machine Scale sets](virtual-machine-scale-sets-vertical-scale-reprovision.md)</span></span>
* <span data-ttu-id="e1ddb-239">Découvrez des exemples de fonctionnalités de surveillance Azure Monitor dans les [exemples de démarrage rapide d’Azure Monitor PowerShell](../monitoring-and-diagnostics/insights-powershell-samples.md)</span><span class="sxs-lookup"><span data-stu-id="e1ddb-239">Find examples of Azure Monitor monitoring features in [Azure Monitor PowerShell quick start samples](../monitoring-and-diagnostics/insights-powershell-samples.md)</span></span>
* <span data-ttu-id="e1ddb-240">En savoir plus sur les fonctionnalités de notification de [utiliser échelle actions toosend par courrier électronique et webhook des notifications d’alerte dans le moniteur de Azure](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md)</span><span class="sxs-lookup"><span data-stu-id="e1ddb-240">Learn about notification features in [Use autoscale actions toosend email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md)</span></span>
* <span data-ttu-id="e1ddb-241">Découvrez comment trop[toosend par courrier électronique et webhook des notifications d’alerte de les journaux d’audit d’utilisation dans le moniteur de Azure](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span><span class="sxs-lookup"><span data-stu-id="e1ddb-241">Learn how too[Use audit logs toosend email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span></span>

