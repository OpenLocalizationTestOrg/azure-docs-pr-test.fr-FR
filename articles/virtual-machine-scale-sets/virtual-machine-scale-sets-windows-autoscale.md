---
title: "Mettre à l’échelle automatiquement des groupes identiques de machines virtuelles Windows | Microsoft Docs"
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
ms.openlocfilehash: 91f731bec46c005221f4e66e95822994070d4c26
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="automatically-scale-machines-in-a-virtual-machine-scale-set"></a><span data-ttu-id="dd63f-103">Mettre automatiquement à l’échelle des machines dans un jeu de mise à l’échelle de machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="dd63f-103">Automatically scale machines in a virtual machine scale set</span></span>
<span data-ttu-id="dd63f-104">Les jeux de mise à l’échelle de machines virtuelles facilitent le déploiement et la gestion de machines virtuelles identiques en tant qu’ensemble.</span><span class="sxs-lookup"><span data-stu-id="dd63f-104">Virtual machine scale sets make it easy for you to deploy and manage identical virtual machines as a set.</span></span> <span data-ttu-id="dd63f-105">Les groupes à échelle identique fournissent une couche de calcul hautement évolutive et personnalisable pour les applications « hyperscale », et prennent en charge les images de plateforme Windows, les images de plateforme Linux, des images personnalisées et les extensions.</span><span class="sxs-lookup"><span data-stu-id="dd63f-105">Scale sets provide a highly scalable and customizable compute layer for hyperscale applications, and they support Windows platform images, Linux platform images, custom images, and extensions.</span></span> <span data-ttu-id="dd63f-106">Pour plus d’informations sur les jeux de mise à l’échelle, consultez [Jeux de mise à l’échelle de machine virtuelle](virtual-machine-scale-sets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="dd63f-106">For more information about scale sets, see [Virtual Machine Scale Sets](virtual-machine-scale-sets-overview.md).</span></span>

<span data-ttu-id="dd63f-107">Ce didacticiel vous montre comment créer un jeu de mise à l’échelle de machines virtuelles Windows et mettre automatiquement à l’échelle les machines de ce jeu.</span><span class="sxs-lookup"><span data-stu-id="dd63f-107">This tutorial shows you how to create a scale set of Windows virtual machines and automatically scale the machines in the set.</span></span> <span data-ttu-id="dd63f-108">Pour créer le jeu de mise à l’échelle et configurer la mise à l’échelle, créez un modèle Azure Resource Manager et déployez-le à l’aide d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dd63f-108">You create the scale set and set up scaling by creating an Azure Resource Manager template and deploying it using Azure PowerShell.</span></span> <span data-ttu-id="dd63f-109">Pour en savoir plus sur les modèles, consultez [Création de modèles Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="dd63f-109">For more information about templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span> <span data-ttu-id="dd63f-110">Pour plus d'informations sur la mise à l'échelle automatique de jeux de mise à l'échelle, consultez la rubrique [Mise à l'échelle automatique et jeux de mise à l'échelle de machines virtuelles](virtual-machine-scale-sets-autoscale-overview.md).</span><span class="sxs-lookup"><span data-stu-id="dd63f-110">To learn more about automatic scaling of scale sets, see [Automatic scaling and Virtual Machine Scale Sets](virtual-machine-scale-sets-autoscale-overview.md).</span></span>

<span data-ttu-id="dd63f-111">Cet article décrit comment déployer les ressources et extensions suivantes :</span><span class="sxs-lookup"><span data-stu-id="dd63f-111">In this article, you deploy the following resources and extensions:</span></span>

* <span data-ttu-id="dd63f-112">Microsoft.Storage/storageAccounts</span><span class="sxs-lookup"><span data-stu-id="dd63f-112">Microsoft.Storage/storageAccounts</span></span>
* <span data-ttu-id="dd63f-113">Microsoft.Network/virtualNetworks</span><span class="sxs-lookup"><span data-stu-id="dd63f-113">Microsoft.Network/virtualNetworks</span></span>
* <span data-ttu-id="dd63f-114">Microsoft.Network/publicIPAddresses</span><span class="sxs-lookup"><span data-stu-id="dd63f-114">Microsoft.Network/publicIPAddresses</span></span>
* <span data-ttu-id="dd63f-115">Microsoft.Network/loadBalancers</span><span class="sxs-lookup"><span data-stu-id="dd63f-115">Microsoft.Network/loadBalancers</span></span>
* <span data-ttu-id="dd63f-116">Microsoft.Network/networkInterfaces</span><span class="sxs-lookup"><span data-stu-id="dd63f-116">Microsoft.Network/networkInterfaces</span></span>
* <span data-ttu-id="dd63f-117">Microsoft.Compute/virtualMachines</span><span class="sxs-lookup"><span data-stu-id="dd63f-117">Microsoft.Compute/virtualMachines</span></span>
* <span data-ttu-id="dd63f-118">Microsoft.Compute/virtualMachineScaleSets</span><span class="sxs-lookup"><span data-stu-id="dd63f-118">Microsoft.Compute/virtualMachineScaleSets</span></span>
* <span data-ttu-id="dd63f-119">Microsoft.Insights.VMDiagnosticsSettings</span><span class="sxs-lookup"><span data-stu-id="dd63f-119">Microsoft.Insights.VMDiagnosticsSettings</span></span>
* <span data-ttu-id="dd63f-120">Microsoft.Insights/autoscaleSettings</span><span class="sxs-lookup"><span data-stu-id="dd63f-120">Microsoft.Insights/autoscaleSettings</span></span>

<span data-ttu-id="dd63f-121">Pour plus d’informations sur les ressources Azure Manager, consultez [Déploiement Azure Resource Manager et déploiement classique](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="dd63f-121">For more information about Resource Manager resources, see [Azure Resource Manager vs. classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>

## <a name="step-1-install-azure-powershell"></a><span data-ttu-id="dd63f-122">Étape 1 : installer Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="dd63f-122">Step 1: Install Azure PowerShell</span></span>
<span data-ttu-id="dd63f-123">Pour plus d’informations sur l’installation de la version la plus récente d’Azure PowerShell en sélectionnant votre abonnement et en vous connectant à Azure, consultez [Installation et configuration d’Azure PowerShell](/powershell/azure/overview) .</span><span class="sxs-lookup"><span data-stu-id="dd63f-123">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for information about installing the latest version of Azure PowerShell, selecting your subscription, and signing in to Azure.</span></span>

## <a name="step-2-create-a-resource-group-and-a-storage-account"></a><span data-ttu-id="dd63f-124">Étape 2 : créer un groupe de ressources et un compte de stockage</span><span class="sxs-lookup"><span data-stu-id="dd63f-124">Step 2: Create a resource group and a storage account</span></span>
1. <span data-ttu-id="dd63f-125">**Créer un groupe de ressources** : toutes les ressources doivent être déployées dans un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="dd63f-125">**Create a resource group** – All resources must be deployed to a resource group.</span></span> <span data-ttu-id="dd63f-126">Utilisez [New-AzureRmResourceGroup](https://msdn.microsoft.com/library/mt603739.aspx) pour créer un groupe de ressources nommé **vmsstestrg1**.</span><span class="sxs-lookup"><span data-stu-id="dd63f-126">Use [New-AzureRmResourceGroup](https://msdn.microsoft.com/library/mt603739.aspx) to create a resource group named **vmsstestrg1**.</span></span>
2. <span data-ttu-id="dd63f-127">**Créer un compte de stockage** : ce compte de stockage est l’emplacement dans lequel le modèle est stocké.</span><span class="sxs-lookup"><span data-stu-id="dd63f-127">**Create a storage account** – This storage account is where the template is stored.</span></span> <span data-ttu-id="dd63f-128">Utilisez [New-AzureRmStorageAccount](https://msdn.microsoft.com/library/mt607148.aspx) pour créer un compte de stockage nommé **vmsstestsa**.</span><span class="sxs-lookup"><span data-stu-id="dd63f-128">Use [New-AzureRmStorageAccount](https://msdn.microsoft.com/library/mt607148.aspx) to create a storage account named **vmsstestsa**.</span></span>

## <a name="step-3-create-the-template"></a><span data-ttu-id="dd63f-129">Étape 3 : créer le modèle</span><span class="sxs-lookup"><span data-stu-id="dd63f-129">Step 3: Create the template</span></span>
<span data-ttu-id="dd63f-130">Un modèle Azure Resource Manager permet de déployer et gérer des ressources Azure simultanément grâce à une description des ressources JSON et des paramètres de déploiement associés.</span><span class="sxs-lookup"><span data-stu-id="dd63f-130">An Azure Resource Manager template makes it possible for you to deploy and manage Azure resources together by using a JSON description of the resources and associated deployment parameters.</span></span>

1. <span data-ttu-id="dd63f-131">Dans votre éditeur favori, créez le fichier C:\VMSSTemplate.json et ajoutez la structure JSON initiale pour prendre en charge le modèle.</span><span class="sxs-lookup"><span data-stu-id="dd63f-131">In your favorite editor, create the file C:\VMSSTemplate.json and add the initial JSON structure to support the template.</span></span>

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

2. <span data-ttu-id="dd63f-132">Les paramètres ne sont pas toujours nécessaires, mais ils offrent un moyen d’entrer des valeurs lors du déploiement du modèle.</span><span class="sxs-lookup"><span data-stu-id="dd63f-132">Parameters are not always required, but they provide a way to input values when the template is deployed.</span></span> <span data-ttu-id="dd63f-133">Ajoutez ces paramètres sous l’élément parent des paramètres que vous avez ajouté au modèle.</span><span class="sxs-lookup"><span data-stu-id="dd63f-133">Add these parameters under the parameters parent element that you added to the template.</span></span>

    ```json   
    "vmName": { "type": "string" },
    "vmSSName": { "type": "string" },
    "instanceCount": { "type": "string" },
    "adminUsername": { "type": "string" },
    "adminPassword": { "type": "securestring" },
    "resourcePrefix": { "type": "string" }
    ```
   
    * <span data-ttu-id="dd63f-134">Nom de la machine virtuelle distincte utilisée pour accéder aux machines du groupe à échelle identique.</span><span class="sxs-lookup"><span data-stu-id="dd63f-134">A name for the separate virtual machine that is used to access the machines in the scale set.</span></span>
    * <span data-ttu-id="dd63f-135">Nom du compte de stockage dans lequel le modèle est stocké.</span><span class="sxs-lookup"><span data-stu-id="dd63f-135">The name of the storage account where the template is stored.</span></span>
    * <span data-ttu-id="dd63f-136">Nombre de machines virtuelles à créer initialement dans le jeu de mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="dd63f-136">The number of virtual machines to initially create in the scale set.</span></span>
    * <span data-ttu-id="dd63f-137">Nom et mot de passe du compte d’administrateur sur les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="dd63f-137">The name and password of the administrator account on the virtual machines.</span></span>
    * <span data-ttu-id="dd63f-138">Préfixe de nom pour les ressources qui sont créées pour prendre en charge le jeu de mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="dd63f-138">A name prefix for the resources that are created to support the scale set.</span></span>

3. <span data-ttu-id="dd63f-139">Des variables peuvent être utilisées dans un modèle pour spécifier des valeurs qui changent fréquemment ou qui doivent être créées à partir d’une combinaison de valeurs de paramètres.</span><span class="sxs-lookup"><span data-stu-id="dd63f-139">Variables can be used in a template to specify values that may change frequently or values that need to be created from a combination of parameter values.</span></span> <span data-ttu-id="dd63f-140">Ajoutez ces variables sous l’élément parent des variables que vous avez ajouté au modèle.</span><span class="sxs-lookup"><span data-stu-id="dd63f-140">Add these variables under the variables parent element that you added to the template.</span></span>

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
   
    * <span data-ttu-id="dd63f-141">Noms DNS utilisés par les interfaces réseau.</span><span class="sxs-lookup"><span data-stu-id="dd63f-141">DNS names that are used by the network interfaces.</span></span>

        * <span data-ttu-id="dd63f-142">Les noms d’adresse IP et les préfixes destinés au réseau et aux sous-réseaux.</span><span class="sxs-lookup"><span data-stu-id="dd63f-142">The IP address names and prefixes for the virtual network and subnets.</span></span>
        * <span data-ttu-id="dd63f-143">Les noms et les identificateurs du réseau virtuel, de l’équilibreur de charge et des interfaces réseau.</span><span class="sxs-lookup"><span data-stu-id="dd63f-143">The names and identifiers of the virtual network, load balancer, and network interfaces.</span></span>
        * <span data-ttu-id="dd63f-144">Les noms de compte de stockage pour les comptes associés aux machines du groupe à échelle identique.</span><span class="sxs-lookup"><span data-stu-id="dd63f-144">Storage account names for the accounts associated with the machines in the scale set.</span></span>
        * <span data-ttu-id="dd63f-145">Paramètres de l’extension de diagnostic qui est installé sur les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="dd63f-145">Settings for the Diagnostics extension that is installed on the virtual machines.</span></span> <span data-ttu-id="dd63f-146">Pour plus d’informations sur l’extension de diagnostic, consultez [Créer une machine virtuelle Windows avec des fonctionnalités de surveillance et de diagnostics à l’aide d’un modèle Azure Resource Manager](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="dd63f-146">For more information about the Diagnostics extension, see [Create a Windows Virtual machine with monitoring and diagnostics using Azure Resource Manager Template](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

4. <span data-ttu-id="dd63f-147">Ajoutez la ressource de compte de stockage sous l’élément parent de ressources que vous avez ajouté au modèle.</span><span class="sxs-lookup"><span data-stu-id="dd63f-147">Add the storage account resource under the resources parent element that you added to the template.</span></span> <span data-ttu-id="dd63f-148">Ce modèle utilise une boucle pour créer les cinq comptes de stockage recommandés dans lesquels les disques de système d’exploitation et les données de diagnostic sont stockés.</span><span class="sxs-lookup"><span data-stu-id="dd63f-148">This template uses a loop to create the recommended five storage accounts where the operating system disks and diagnostic data are stored.</span></span> <span data-ttu-id="dd63f-149">Cet ensemble de comptes peut prendre en charge jusqu’à 100 machines virtuelles dans un groupe à échelle identique, qui est la valeur maximale actuelle.</span><span class="sxs-lookup"><span data-stu-id="dd63f-149">This set of accounts can support up to 100 virtual machines in a scale set, which is the current maximum.</span></span> <span data-ttu-id="dd63f-150">Chaque compte de stockage est nommé avec un indicateur de lettre défini dans les variables, combiné au préfixe que vous fournissez dans les paramètres du modèle.</span><span class="sxs-lookup"><span data-stu-id="dd63f-150">Each storage account is named with a letter designator that was defined in the variables combined with the prefix that you provide in the parameters for the template.</span></span>

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

5. <span data-ttu-id="dd63f-151">Ajoutez la ressource de réseau virtuelle.</span><span class="sxs-lookup"><span data-stu-id="dd63f-151">Add the virtual network resource.</span></span> <span data-ttu-id="dd63f-152">Pour plus d’informations, consultez [Fournisseurs de ressources réseau](../virtual-network/resource-groups-networking.md).</span><span class="sxs-lookup"><span data-stu-id="dd63f-152">For more information, see [Network Resource Provider](../virtual-network/resource-groups-networking.md).</span></span>

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

6. <span data-ttu-id="dd63f-153">Ajoutez des ressources d’adresse IP publiques qui sont utilisées par l’équilibrage de charge et l’interface réseau.</span><span class="sxs-lookup"><span data-stu-id="dd63f-153">Add the public IP address resources that are used by the load balancer and network interface.</span></span>

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

7. <span data-ttu-id="dd63f-154">Ajoutez la ressource d’équilibrage de charge utilisée par le groupe à échelle identique.</span><span class="sxs-lookup"><span data-stu-id="dd63f-154">Add the load balancer resource that is used by the scale set.</span></span> <span data-ttu-id="dd63f-155">Pour plus d’informations, consultez [Prise en charge d’un équilibreur de charge par Azure Resource Manager](../load-balancer/load-balancer-arm.md)</span><span class="sxs-lookup"><span data-stu-id="dd63f-155">For more information, see [Azure Resource Manager Support for Load Balancer](../load-balancer/load-balancer-arm.md).</span></span>

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

8. <span data-ttu-id="dd63f-156">Ajoutez la ressource d’interface réseau qui est utilisée par la machine virtuelle distincte.</span><span class="sxs-lookup"><span data-stu-id="dd63f-156">Add the network interface resource that is used by the separate virtual machine.</span></span> <span data-ttu-id="dd63f-157">Étant donné que les machines virtuelles d’un jeu de mise à l’échelle ne sont pas accessibles via une adresse IP publique, une machine virtuelle distincte est créée dans le même réseau virtuel pour accéder à distance aux machines.</span><span class="sxs-lookup"><span data-stu-id="dd63f-157">Because machines in a scale set aren't accessible through a public IP address, a separate virtual machine is created in the same virtual network to remotely access the machines.</span></span>

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

9. <span data-ttu-id="dd63f-158">Ajoutez la machine virtuelle distincte dans le même réseau que le groupe à échelle identique.</span><span class="sxs-lookup"><span data-stu-id="dd63f-158">Add the separate virtual machine in the same network as the scale set.</span></span>

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

10. <span data-ttu-id="dd63f-159">Ajoutez la ressource de jeu de mise à l’échelle de machines virtuelles et spécifiez l’extension Diagnostics installée sur toutes les machines virtuelles du jeu de mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="dd63f-159">Add the virtual machine scale set resource and specify the diagnostics extension that is installed on all virtual machines in the scale set.</span></span> <span data-ttu-id="dd63f-160">La plupart des paramètres de cette ressource sont similaires à la ressource de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="dd63f-160">Many of the settings for this resource are similar with the virtual machine resource.</span></span> <span data-ttu-id="dd63f-161">Les principales différences sont l’élément capacity qui spécifie le nombre de machines virtuelles du jeu de mise à l’échelle et le paramètre upgradePolicy qui spécifie la manière dont les mises à jour sont appliquées aux machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="dd63f-161">The main differences are the capacity element that specifies the number of virtual machines in the scale set, and upgradePolicy that specifies how updates are made to virtual machines.</span></span> <span data-ttu-id="dd63f-162">Le jeu de mise à l’échelle n’est pas créé tant que tous les comptes de stockage ne sont pas créés, comme spécifié par l’élément dependsOn.</span><span class="sxs-lookup"><span data-stu-id="dd63f-162">The scale set is not created until all the storage accounts are created as specified with the dependsOn element.</span></span>

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

11. <span data-ttu-id="dd63f-163">Ajoutez la ressource autoscaleSettings qui définit comment le jeu de mise à l’échelle s’ajuste en fonction de l’utilisation du processeur sur les machines du jeu de mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="dd63f-163">Add the autoscaleSettings resource that defines how the scale set adjusts based on the processor usage on the machines in the scale set.</span></span>

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

    <span data-ttu-id="dd63f-164">Pour ce didacticiel, les valeurs suivantes sont importantes :</span><span class="sxs-lookup"><span data-stu-id="dd63f-164">For this tutorial, these values are important:</span></span>
    
    * <span data-ttu-id="dd63f-165">**metricName**</span><span class="sxs-lookup"><span data-stu-id="dd63f-165">**metricName**</span></span>  
    <span data-ttu-id="dd63f-166">Cette valeur est la même que celle du compteur de performances que nous avons défini dans la variable wadperfcounter.</span><span class="sxs-lookup"><span data-stu-id="dd63f-166">This value is the same as the performance counter that we defined in the wadperfcounter variable.</span></span> <span data-ttu-id="dd63f-167">Grâce à cette variable, l’extension Diagnostics relève le compteur **Processor(_Total)\% Processor Time**.</span><span class="sxs-lookup"><span data-stu-id="dd63f-167">Using that variable, the Diagnostics extension collects the  **Processor(_Total)\% Processor Time** counter.</span></span>
    
    * <span data-ttu-id="dd63f-168">**metricResourceUri**</span><span class="sxs-lookup"><span data-stu-id="dd63f-168">**metricResourceUri**</span></span>  
    <span data-ttu-id="dd63f-169">Cette valeur est l’identificateur de ressource du groupe de machines virtuelles identiques.</span><span class="sxs-lookup"><span data-stu-id="dd63f-169">This value is the resource identifier of the virtual machine scale set.</span></span>
    
    * <span data-ttu-id="dd63f-170">**timeGrain**</span><span class="sxs-lookup"><span data-stu-id="dd63f-170">**timeGrain**</span></span>  
    <span data-ttu-id="dd63f-171">Cette valeur est la granularité des mesures collectées.</span><span class="sxs-lookup"><span data-stu-id="dd63f-171">This value is the granularity of the metrics that are collected.</span></span> <span data-ttu-id="dd63f-172">Dans ce modèle, elle est définie sur une minute.</span><span class="sxs-lookup"><span data-stu-id="dd63f-172">In this template, it is set to one minute.</span></span>
    
    * <span data-ttu-id="dd63f-173">**statistic**</span><span class="sxs-lookup"><span data-stu-id="dd63f-173">**statistic**</span></span>  
    <span data-ttu-id="dd63f-174">Cette valeur détermine la façon dont les mesures sont combinées pour prendre en charge l’action de mise à l’échelle automatique.</span><span class="sxs-lookup"><span data-stu-id="dd63f-174">This value determines how the metrics are combined to accommodate the automatic scaling action.</span></span> <span data-ttu-id="dd63f-175">Les valeurs possibles sont : Moyenne, Min, Max.</span><span class="sxs-lookup"><span data-stu-id="dd63f-175">The possible values are: Average, Min, Max.</span></span> <span data-ttu-id="dd63f-176">Dans ce modèle, l’utilisation moyenne totale du processeur des machines virtuelles est collectée.</span><span class="sxs-lookup"><span data-stu-id="dd63f-176">In this template, the average total CPU usage of the virtual machines is collected.</span></span>
    
    * <span data-ttu-id="dd63f-177">**timeWindow**</span><span class="sxs-lookup"><span data-stu-id="dd63f-177">**timeWindow**</span></span>  
    <span data-ttu-id="dd63f-178">Cette valeur est la plage de temps pendant laquelle les données d’instance sont collectées.</span><span class="sxs-lookup"><span data-stu-id="dd63f-178">This value is the range of time in which instance data is collected.</span></span> <span data-ttu-id="dd63f-179">Elle doit être comprise entre 5 minutes et 12 heures.</span><span class="sxs-lookup"><span data-stu-id="dd63f-179">It must be between 5 minutes and 12 hours.</span></span>
    
    * <span data-ttu-id="dd63f-180">**timeAggregation**</span><span class="sxs-lookup"><span data-stu-id="dd63f-180">**timeAggregation**</span></span>  
    <span data-ttu-id="dd63f-181">Cette valeur détermine la façon dont les données collectées doivent être combinées au fil du temps.</span><span class="sxs-lookup"><span data-stu-id="dd63f-181">his value determines how the data that is collected should be combined over time.</span></span> <span data-ttu-id="dd63f-182">La valeur par défaut est Average.</span><span class="sxs-lookup"><span data-stu-id="dd63f-182">The default value is Average.</span></span> <span data-ttu-id="dd63f-183">Les valeurs possibles sont : Moyenne, Minimum, Maximum, Dernier, Total, Nombre.</span><span class="sxs-lookup"><span data-stu-id="dd63f-183">The possible values are: Average, Minimum, Maximum, Last, Total, Count.</span></span>
    
    * <span data-ttu-id="dd63f-184">**operator**</span><span class="sxs-lookup"><span data-stu-id="dd63f-184">**operator**</span></span>  
    <span data-ttu-id="dd63f-185">Cette valeur est l’opérateur utilisé pour comparer les données de mesure et le seuil.</span><span class="sxs-lookup"><span data-stu-id="dd63f-185">This value is the operator that is used to compare the metric data and the threshold.</span></span> <span data-ttu-id="dd63f-186">Les valeurs possibles sont : est égal à -Equals), différent de (NotEquals), supérieur à (GreaterThan), égal ou supérieur à (GreaterThanOrEqual), Inférieur à (LessThan), Inférieur ou égal à (LessThanOrEqual).</span><span class="sxs-lookup"><span data-stu-id="dd63f-186">The possible values are: Equals, NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.</span></span>
    
    * <span data-ttu-id="dd63f-187">**threshold**</span><span class="sxs-lookup"><span data-stu-id="dd63f-187">**threshold**</span></span>  
    <span data-ttu-id="dd63f-188">Cette valeur est celle qui déclenche l’action de mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="dd63f-188">This value is the value that triggers the scale action.</span></span> <span data-ttu-id="dd63f-189">Dans ce modèle, les machines sont ajoutées au jeu de mise à l’échelle défini lorsque l’utilisation moyenne du processeur dans le jeu de machines des est supérieur à 50 %.</span><span class="sxs-lookup"><span data-stu-id="dd63f-189">In this template, machines are added to the scale set when the average CPU usage among machines in the set is over 50%.</span></span>
    
    * <span data-ttu-id="dd63f-190">**direction**</span><span class="sxs-lookup"><span data-stu-id="dd63f-190">**direction**</span></span>  
    <span data-ttu-id="dd63f-191">Cette valeur détermine l’opération qui est effectuée lorsque la valeur de seuil est atteinte.</span><span class="sxs-lookup"><span data-stu-id="dd63f-191">This value determines the action that is taken when the threshold value is achieved.</span></span> <span data-ttu-id="dd63f-192">Les valeurs possibles sont Augmenter ou Diminuer.</span><span class="sxs-lookup"><span data-stu-id="dd63f-192">The possible values are Increase or Decrease.</span></span> <span data-ttu-id="dd63f-193">Dans ce modèle, le nombre de machines virtuelles dans le jeu de mise à l’échelle est augmenté si le seuil est supérieur à 50 % dans la fenêtre de temps définie.</span><span class="sxs-lookup"><span data-stu-id="dd63f-193">In this template, the number of virtual machines in the scale set is increased if the threshold is over 50% in the defined time window.</span></span>
    
    * <span data-ttu-id="dd63f-194">**type**</span><span class="sxs-lookup"><span data-stu-id="dd63f-194">**type**</span></span>  
    <span data-ttu-id="dd63f-195">Cette valeur est le type d’action qui doit se produire. Elle doit être définie sur ChangeCount.</span><span class="sxs-lookup"><span data-stu-id="dd63f-195">This value is the type of action that should occur and must be set to ChangeCount.</span></span>
    
    * <span data-ttu-id="dd63f-196">**value**</span><span class="sxs-lookup"><span data-stu-id="dd63f-196">**value**</span></span>  
    <span data-ttu-id="dd63f-197">Cette valeur est le nombre de machines virtuelles qui sont ajoutées ou supprimées dans le groupe identique.</span><span class="sxs-lookup"><span data-stu-id="dd63f-197">This value is the number of virtual machines that are added or removed from the scale set.</span></span> <span data-ttu-id="dd63f-198">Cette valeur doit être définie sur 1 ou supérieur.</span><span class="sxs-lookup"><span data-stu-id="dd63f-198">This value must be 1 or greater.</span></span> <span data-ttu-id="dd63f-199">La valeur par défaut est 1.</span><span class="sxs-lookup"><span data-stu-id="dd63f-199">The default value is 1.</span></span> <span data-ttu-id="dd63f-200">Dans ce modèle, le nombre d’ordinateurs présent dans le jeu de mise à l’échelle augmente de 1 lorsque le seuil est atteint.</span><span class="sxs-lookup"><span data-stu-id="dd63f-200">In this template, the number of machines in the scale set increases by 1 when the threshold is met.</span></span>
    
    * <span data-ttu-id="dd63f-201">**cooldown**</span><span class="sxs-lookup"><span data-stu-id="dd63f-201">**cooldown**</span></span>  
    <span data-ttu-id="dd63f-202">Cette valeur est la durée d’attente depuis la dernière opération de mise à l’échelle avant que l’action suivante se produise.</span><span class="sxs-lookup"><span data-stu-id="dd63f-202">This value is the amount of time to wait since the last scaling action before the next action occurs.</span></span> <span data-ttu-id="dd63f-203">Elle doit être comprise entre une minute et une semaine.</span><span class="sxs-lookup"><span data-stu-id="dd63f-203">This value must be between one minute and one week.</span></span>

12. <span data-ttu-id="dd63f-204">Enregistrez le fichier de modèle.</span><span class="sxs-lookup"><span data-stu-id="dd63f-204">Save the template file.</span></span>    

## <a name="step-4-upload-the-template-to-storage"></a><span data-ttu-id="dd63f-205">Étape 4 : charger le modèle dans le stockage</span><span class="sxs-lookup"><span data-stu-id="dd63f-205">Step 4: Upload the template to storage</span></span>
<span data-ttu-id="dd63f-206">Le modèle peut être chargé pour autant que vous connaissiez le nom et la clé primaire du compte de stockage que vous avez créé à l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="dd63f-206">The template can be uploaded as long as you know the name and primary key of the storage account that you created in step 1.</span></span>

1. <span data-ttu-id="dd63f-207">Dans la fenêtre Microsoft Azure PowerShell, définissez une variable qui spécifie le nom du compte de stockage que vous avez créé à l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="dd63f-207">In the Microsoft Azure PowerShell window, set a variable that specifies the name of the storage account that you created in step 1.</span></span>
   
    ```powershell
    $storageAccountName = "vmstestsa"
    ```

2. <span data-ttu-id="dd63f-208">Définissez une variable qui spécifie la clé primaire du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="dd63f-208">Set a variable that specifies the primary key of the storage account.</span></span>
   
    ```powershell
    $storageAccountKey = "<primary-account-key>"
    ```
   
   <span data-ttu-id="dd63f-209">Vous pouvez obtenir cette clé en cliquant sur l’icône de clé lors de l’affichage de la ressource de compte de stockage dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="dd63f-209">You can get this key by clicking the key icon when viewing the storage account resource in the Azure portal.</span></span>
3. <span data-ttu-id="dd63f-210">Créez l’objet de contexte de compte de stockage utilisé pour valider les opérations avec le compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="dd63f-210">Create the storage account context object that is used to validate operations with the storage account.</span></span>
   
    ```powershell
    $ctx = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey
    ```

4. <span data-ttu-id="dd63f-211">Créez le conteneur pour stocker le modèle.</span><span class="sxs-lookup"><span data-stu-id="dd63f-211">Create the container for storing the template.</span></span>

    ```powershell
    $containerName = "templates"
    New-AzureStorageContainer -Name $containerName -Context $ctx  -Permission Blob
    ```

5. <span data-ttu-id="dd63f-212">Chargez le fichier de modèle correspondant au nouveau conteneur.</span><span class="sxs-lookup"><span data-stu-id="dd63f-212">Upload the template file to the new container.</span></span>

    ```powershell   
    $blobName = "VMSSTemplate.json"
    $fileName = "C:\" + $BlobName
    Set-AzureStorageBlobContent -File $fileName -Container $containerName -Blob  $blobName -Context $ctx
    ```

## <a name="step-5-deploy-the-template"></a><span data-ttu-id="dd63f-213">Étape 5 : déployer le modèle</span><span class="sxs-lookup"><span data-stu-id="dd63f-213">Step 5: Deploy the template</span></span>
<span data-ttu-id="dd63f-214">Maintenant que vous avez créé le modèle, vous pouvez commencer à déployer les ressources.</span><span class="sxs-lookup"><span data-stu-id="dd63f-214">Now that you created the template, you can start deploying the resources.</span></span> <span data-ttu-id="dd63f-215">Utilisez cette commande pour démarrer le processus :</span><span class="sxs-lookup"><span data-stu-id="dd63f-215">Use this command to start the process:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name "vmsstestdp1" -ResourceGroupName "vmsstestrg1" -TemplateUri "https://vmsstestsa.blob.core.windows.net/templates/VMSSTemplate.json"
```

<span data-ttu-id="dd63f-216">Lorsque vous appuyez sur Entrée, vous êtes invité à fournir des valeurs pour les variables que vous avez affectées.</span><span class="sxs-lookup"><span data-stu-id="dd63f-216">When you press enter, you are prompted to provide values for the variables you assigned.</span></span> <span data-ttu-id="dd63f-217">Remplacez les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="dd63f-217">Provide these values:</span></span>

```powershell
vmName: vmsstestvm1
  vmSSName: vmsstest1
  instanceCount: 5
  adminUserName: vmadmin1
  adminPassword: VMpass1
  resourcePrefix: vmsstest
```

<span data-ttu-id="dd63f-218">Environ 15 minutes sont nécessaires pour le déploiement correct de toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="dd63f-218">It should take about 15 minutes for all the resources to successfully be deployed.</span></span>

> [!NOTE]
> <span data-ttu-id="dd63f-219">Vous pouvez également utiliser la capacité du portail à déployer les ressources.</span><span class="sxs-lookup"><span data-stu-id="dd63f-219">You can also use the portal’s ability to deploy the resources.</span></span> <span data-ttu-id="dd63f-220">Utilisez le lien suivant : « https://portal.azure.com/#create/Microsoft.Template/uri/<link to VM Scale Set JSON template>»</span><span class="sxs-lookup"><span data-stu-id="dd63f-220">Use this link: "https://portal.azure.com/#create/Microsoft.Template/uri/<link to VM Scale Set JSON template>"</span></span>
> 
> 

## <a name="step-6-monitor-resources"></a><span data-ttu-id="dd63f-221">Étape 6 : surveiller les ressources</span><span class="sxs-lookup"><span data-stu-id="dd63f-221">Step 6: Monitor resources</span></span>
<span data-ttu-id="dd63f-222">Vous pouvez obtenir des informations sur les jeux de mise à l’échelle de machine virtuelle à l’aide des méthodes suivantes :</span><span class="sxs-lookup"><span data-stu-id="dd63f-222">You can get some information about virtual machine scale sets using these methods:</span></span>

* <span data-ttu-id="dd63f-223">Le portail Azure : vous pouvez en obtenir une quantité limitée d’informations sur l’utilisation du portail.</span><span class="sxs-lookup"><span data-stu-id="dd63f-223">The Azure portal - You can currently get a limited amount of information using the portal.</span></span>
* <span data-ttu-id="dd63f-224">[Explorateur de ressources Azure](https://resources.azure.com/) : cet outil est le meilleur qui soit pour déterminer l’état actuel de votre groupe identique.</span><span class="sxs-lookup"><span data-stu-id="dd63f-224">The [Azure Resource Explorer](https://resources.azure.com/) - This tool is the best for exploring the current state of your scale set.</span></span> <span data-ttu-id="dd63f-225">Suivez ce chemin d’accès. Vous devriez voir la vue de l’instance du groupe à échelle identique que vous avez créée :</span><span class="sxs-lookup"><span data-stu-id="dd63f-225">Follow this path and you should see the instance view of the scale set that you created:</span></span>
  
    <span data-ttu-id="dd63f-226">abonnements > {votre abonnement} > resourceGroups > vmsstestrg1 > fournisseurs > Microsoft.Compute > virtualMachineScaleSets > vmsstest1 > virtualMachines</span><span class="sxs-lookup"><span data-stu-id="dd63f-226">subscriptions > {your subscription} > resourceGroups > vmsstestrg1 > providers > Microsoft.Compute > virtualMachineScaleSets > vmsstest1 > virtualMachines</span></span>

* <span data-ttu-id="dd63f-227">Azure PowerShell : utilisez cette commande pour obtenir des informations :</span><span class="sxs-lookup"><span data-stu-id="dd63f-227">Azure PowerShell - Use this command to get some information:</span></span>

  ```powershell
  Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name"
  ```
  
  <span data-ttu-id="dd63f-228">Ou</span><span class="sxs-lookup"><span data-stu-id="dd63f-228">Or</span></span>
  
  ```powershell
  Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceView
  ```

* <span data-ttu-id="dd63f-229">Connectez-vous à la machine virtuelle séparée comme vous le feriez pour n’importe quel autre ordinateur. Vous pouvez ensuite accéder à distance aux machines virtuelles du jeu de mise à l’échelle pour surveiller des processus individuels.</span><span class="sxs-lookup"><span data-stu-id="dd63f-229">Connect to the separate virtual machine just like you would any other machine and then you can remotely access the virtual machines in the scale set to monitor individual processes.</span></span>

> [!NOTE]
> <span data-ttu-id="dd63f-230">Vous trouverez une API REST complète permettant d’obtenir des informations sur les jeux de mise à l’échelle dans [Ensembles de mise à l’échelle de machine virtuelle](https://msdn.microsoft.com/library/mt589023.aspx)</span><span class="sxs-lookup"><span data-stu-id="dd63f-230">A complete REST API for obtaining information about scale sets can be found in [Virtual Machine Scale Sets](https://msdn.microsoft.com/library/mt589023.aspx)</span></span>

## <a name="step-7-remove-the-resources"></a><span data-ttu-id="dd63f-231">Étape 7 : supprimer les ressources</span><span class="sxs-lookup"><span data-stu-id="dd63f-231">Step 7: Remove the resources</span></span>
<span data-ttu-id="dd63f-232">Étant donné que les ressources utilisées dans Microsoft Azure vous sont facturées, il est toujours conseillé de supprimer les ressources qui ne sont plus nécessaires.</span><span class="sxs-lookup"><span data-stu-id="dd63f-232">Because you are charged for resources used in Azure, it is always a good practice to delete resources that are no longer needed.</span></span> <span data-ttu-id="dd63f-233">Vous n’avez pas besoin de supprimer séparément les ressources d’un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="dd63f-233">You don’t need to delete each resource separately from a resource group.</span></span> <span data-ttu-id="dd63f-234">Vous pouvez supprimer le groupe de ressources pour supprimer automatiquement toutes ses ressources.</span><span class="sxs-lookup"><span data-stu-id="dd63f-234">You can delete the resource group and all its resources are automatically deleted.</span></span>

  ```powershell
  Remove-AzureRmResourceGroup -Name vmsstestrg1
  ```

<span data-ttu-id="dd63f-235">Si vous souhaitez conserver votre groupe de ressources, vous pouvez supprimer uniquement le jeu de mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="dd63f-235">If you want to keep your resource group, you can delete the scale set only.</span></span>

  ```powershell
  Remove-AzureRmVmss -ResourceGroupName "resource group name" –VMScaleSetName "scale set name"
  ```

## <a name="next-steps"></a><span data-ttu-id="dd63f-236">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="dd63f-236">Next steps</span></span>
* <span data-ttu-id="dd63f-237">Gérez le jeu de mise à l’échelle que vous avez créé à l’aide des informations figurant dans [Gérer des machines dans un jeu de mise à l’échelle de machines virtuelles](virtual-machine-scale-sets-windows-manage.md).</span><span class="sxs-lookup"><span data-stu-id="dd63f-237">Manage the scale set that you just created using the information in [Manage virtual machines in a Virtual Machine Scale Set](virtual-machine-scale-sets-windows-manage.md).</span></span>
* <span data-ttu-id="dd63f-238">En savoir plus sur la mise à l’échelle verticale en consultant l’article [Mise à l’échelle verticale avec des jeux de mise à l’échelle de machines virtuelles](virtual-machine-scale-sets-vertical-scale-reprovision.md)</span><span class="sxs-lookup"><span data-stu-id="dd63f-238">Learn more about vertical scaling by reviewing [Vertical autoscale with Virtual Machine Scale sets](virtual-machine-scale-sets-vertical-scale-reprovision.md)</span></span>
* <span data-ttu-id="dd63f-239">Découvrez des exemples de fonctionnalités de surveillance Azure Monitor dans les [exemples de démarrage rapide d’Azure Monitor PowerShell](../monitoring-and-diagnostics/insights-powershell-samples.md)</span><span class="sxs-lookup"><span data-stu-id="dd63f-239">Find examples of Azure Monitor monitoring features in [Azure Monitor PowerShell quick start samples](../monitoring-and-diagnostics/insights-powershell-samples.md)</span></span>
* <span data-ttu-id="dd63f-240">Pour en savoir plus sur les fonctionnalités de notification, consultez [Utilisation d’actions de mise à l’échelle automatique pour envoyer des notifications d’alerte webhook et par courrier électronique dans Azure Monitor](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md)</span><span class="sxs-lookup"><span data-stu-id="dd63f-240">Learn about notification features in [Use autoscale actions to send email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md)</span></span>
* <span data-ttu-id="dd63f-241">Découvrez comment [utiliser les journaux d’audit pour envoyer des notifications d’alerte webhook et par courrier électronique dans Azure Monitor](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span><span class="sxs-lookup"><span data-stu-id="dd63f-241">Learn how to [Use audit logs to send email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span></span>

