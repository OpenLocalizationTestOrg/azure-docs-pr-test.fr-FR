---
title: "aaaCreate une machine virtuelle de Windows à partir d’un modèle dans Azure | Documents Microsoft"
description: "Utilisez un modèle de gestionnaire de ressources et PowerShell tooeasily créer une machine virtuelle Windows."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 19129d61-8c04-4aa9-a01f-361a09466805
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: davidmu
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 630111482c7dc046091632e2ed458ac143325d59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-from-a-resource-manager-template"></a><span data-ttu-id="98c03-103">Créer une machine virtuelle Windows à partir d’un modèle Resource Manager</span><span class="sxs-lookup"><span data-stu-id="98c03-103">Create a Windows virtual machine from a Resource Manager template</span></span>

<span data-ttu-id="98c03-104">Cet article vous explique comment toodeploy un gestionnaire de ressources Azure modèle à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="98c03-104">This article shows you how toodeploy an Azure Resource Manager template using PowerShell.</span></span> <span data-ttu-id="98c03-105">modèle Hello que vous créez déploie une seule machine virtuelle exécutant Windows Server dans un réseau virtuel avec un sous-réseau unique.</span><span class="sxs-lookup"><span data-stu-id="98c03-105">hello template that you create deploys a single virtual machine running Windows Server in a new virtual network with a single subnet.</span></span>

<span data-ttu-id="98c03-106">Pour obtenir une description détaillée de la ressource d’ordinateur virtuel hello, consultez [machines virtuelles dans un modèle Azure Resource Manager](template-description.md).</span><span class="sxs-lookup"><span data-stu-id="98c03-106">For a detailed description of hello virtual machine resource, see [Virtual machines in an Azure Resource Manager template](template-description.md).</span></span> <span data-ttu-id="98c03-107">Pour plus d’informations sur toutes les ressources hello dans un modèle, consultez [procédure pas à pas de gestionnaire de ressources Azure modèle](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="98c03-107">For more information about all hello resources in a template, see [Azure Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>

<span data-ttu-id="98c03-108">Il doit prendre environ cinq minutes toodo hello les étapes de cet article.</span><span class="sxs-lookup"><span data-stu-id="98c03-108">It should take about five minutes toodo hello steps in this article.</span></span>

## <a name="install-azure-powershell"></a><span data-ttu-id="98c03-109">Installation d'Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="98c03-109">Install Azure PowerShell</span></span>

<span data-ttu-id="98c03-110">Consultez [comment tooinstall et configurer Azure PowerShell](../../powershell-install-configure.md) pour plus d’informations sur l’installation hello dernière version de Azure PowerShell, en sélectionnant votre abonnement et l’ouverture de session tooyour compte.</span><span class="sxs-lookup"><span data-stu-id="98c03-110">See [How tooinstall and configure Azure PowerShell](../../powershell-install-configure.md) for information about installing hello latest version of Azure PowerShell, selecting your subscription, and signing in tooyour account.</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="98c03-111">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="98c03-111">Create a resource group</span></span>

<span data-ttu-id="98c03-112">Toutes les ressources doivent être déployées dans un [groupe de ressources](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="98c03-112">All resources must be deployed in a [resource group](../../azure-resource-manager/resource-group-overview.md).</span></span>

1. <span data-ttu-id="98c03-113">Obtenez la liste des emplacements disponibles où créer des ressources.</span><span class="sxs-lookup"><span data-stu-id="98c03-113">Get a list of available locations where resources can be created.</span></span>
   
    ```powershell   
    Get-AzureRmLocation | sort DisplayName | Select DisplayName
    ```

2. <span data-ttu-id="98c03-114">Créer le groupe de ressources hello dans emplacement hello que vous sélectionnez.</span><span class="sxs-lookup"><span data-stu-id="98c03-114">Create hello resource group in hello location that you select.</span></span> <span data-ttu-id="98c03-115">Cet exemple montre la création d’un groupe de ressources nommé hello **myResourceGroup** Bonjour **ouest des États-Unis** emplacement :</span><span class="sxs-lookup"><span data-stu-id="98c03-115">This example shows hello creation of a resource group named **myResourceGroup** in hello **West US** location:</span></span>

    ```powershell   
    New-AzureRmResourceGroup -Name "myResourceGroup" -Location "West US"
    ```

## <a name="create-hello-files"></a><span data-ttu-id="98c03-116">Créer des fichiers hello</span><span class="sxs-lookup"><span data-stu-id="98c03-116">Create hello files</span></span>

<span data-ttu-id="98c03-117">Dans cette étape, vous créez un fichier de modèle qui déploie les ressources hello et un fichier de paramètres qui fournit le modèle de toohello de valeurs de paramètre.</span><span class="sxs-lookup"><span data-stu-id="98c03-117">In this step, you create a template file that deploys hello resources and a parameters file that supplies parameter values toohello template.</span></span> <span data-ttu-id="98c03-118">Vous créez également un fichier d’autorisation qui est utilisé tooperform Azure Resource Manager operations.</span><span class="sxs-lookup"><span data-stu-id="98c03-118">You also create an authorization file that is used tooperform Azure Resource Manager operations.</span></span>

1. <span data-ttu-id="98c03-119">Créez un fichier nommé *CreateVMTemplate.json* et ajoutez ce tooit de code JSON :</span><span class="sxs-lookup"><span data-stu-id="98c03-119">Create a file named *CreateVMTemplate.json* and add this JSON code tooit:</span></span>

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "adminUsername": { "type": "string" },
        "adminPassword": { "type": "securestring" }
      },
      "variables": {
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks','myVNet')]", 
        "subnetRef": "[concat(variables('vnetID'),'/subnets/mySubnet')]", 
      },
      "resources": [
        {
          "apiVersion": "2016-03-30",
          "type": "Microsoft.Network/publicIPAddresses",
          "name": "myPublicIPAddress",
          "location": "[resourceGroup().location]",
          "properties": {
            "publicIPAllocationMethod": "Dynamic",
            "dnsSettings": {
              "domainNameLabel": "myresourcegroupdns1"
            }
          }
        },
        {
          "apiVersion": "2016-03-30",
          "type": "Microsoft.Network/virtualNetworks",
          "name": "myVNet",
          "location": "[resourceGroup().location]",
          "properties": {
            "addressSpace": { "addressPrefixes": [ "10.0.0.0/16" ] },
            "subnets": [
              {
                "name": "mySubnet",
                "properties": { "addressPrefix": "10.0.0.0/24" }
              }
            ]
          }
        },
        {
          "apiVersion": "2016-03-30",
          "type": "Microsoft.Network/networkInterfaces",
          "name": "myNic",
          "location": "[resourceGroup().location]",
          "dependsOn": [
            "[resourceId('Microsoft.Network/publicIPAddresses/', 'myPublicIPAddress')]",
            "[resourceId('Microsoft.Network/virtualNetworks/', 'myVNet')]"
          ],
          "properties": {
            "ipConfigurations": [
              {
                "name": "ipconfig1",
                "properties": {
                  "privateIPAllocationMethod": "Dynamic",
                  "publicIPAddress": { "id": "[resourceId('Microsoft.Network/publicIPAddresses','myPublicIPAddress')]" },
                  "subnet": { "id": "[variables('subnetRef')]" }
                }
              }
            ]
          }
        },
        {
          "apiVersion": "2016-04-30-preview",
          "type": "Microsoft.Compute/virtualMachines",
          "name": "myVM",
          "location": "[resourceGroup().location]",
          "dependsOn": [
            "[resourceId('Microsoft.Network/networkInterfaces/', 'myNic')]"
          ],
          "properties": {
            "hardwareProfile": { "vmSize": "Standard_DS1" },
            "osProfile": {
              "computerName": "myVM",
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
                "name": "myManagedOSDisk",
                "caching": "ReadWrite",
                "createOption": "FromImage"
              }
            },
            "networkProfile": {
              "networkInterfaces": [
                {
                  "id": "[resourceId('Microsoft.Network/networkInterfaces','myNic')]"
                }
              ]
            }
          }
        }
      ]
    }
    ```

2. <span data-ttu-id="98c03-120">Créez un fichier nommé *Parameters.json* et ajoutez ce tooit de code JSON :</span><span class="sxs-lookup"><span data-stu-id="98c03-120">Create a file named *Parameters.json* and add this JSON code tooit:</span></span>

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json",
      "contentVersion": "1.0.0.0",
      "parameters": {
      "adminUserName": { "value": "azureuser" },
        "adminPassword": { "value": "Azure12345678" }
      }
    }
    ```

3. <span data-ttu-id="98c03-121">Créez un compte de stockage et un conteneur :</span><span class="sxs-lookup"><span data-stu-id="98c03-121">Create a new storage account and container:</span></span>

    ```powershell
    $storageName = "st" + (Get-Random)
    New-AzureRmStorageAccount -ResourceGroupName "myResourceGroup" -AccountName $storageName -Location "West US" -SkuName "Standard_LRS" -Kind Storage
    $accountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName myResourceGroup -Name $storageName).Value[0]
    $context = New-AzureStorageContext -StorageAccountName $storageName -StorageAccountKey $accountKey 
    New-AzureStorageContainer -Name "templates" -Context $context -Permission Container
    ```

4. <span data-ttu-id="98c03-122">Télécharger le compte de stockage toohello hello fichiers :</span><span class="sxs-lookup"><span data-stu-id="98c03-122">Upload hello files toohello storage account:</span></span>

    ```powershell
    Set-AzureStorageBlobContent -File "C:\templates\CreateVMTemplate.json" -Context $context -Container "templates"
    Set-AzureStorageBlobContent -File "C:\templates\Parameters.json" -Context $context -Container templates
    ```

    <span data-ttu-id="98c03-123">Modification hello - emplacement de toohello de chemins d’accès de fichier où vous avez stocké les fichiers hello.</span><span class="sxs-lookup"><span data-stu-id="98c03-123">Change hello -File paths toohello location where you stored hello files.</span></span>

## <a name="create-hello-resources"></a><span data-ttu-id="98c03-124">Créer des ressources de hello</span><span class="sxs-lookup"><span data-stu-id="98c03-124">Create hello resources</span></span>

<span data-ttu-id="98c03-125">Déployer le modèle hello à l’aide des paramètres de hello :</span><span class="sxs-lookup"><span data-stu-id="98c03-125">Deploy hello template using hello parameters:</span></span>

```powershell
$templatePath = "https://" + $storageName + ".blob.core.windows.net/templates/CreateVMTemplate.json"
$parametersPath = "https://" + $storageName + ".blob.core.windows.net/templates/Parameters.json"
New-AzureRmResourceGroupDeployment -ResourceGroupName "myResourceGroup" -Name "myDeployment" -TemplateUri $templatePath -TemplateParameterUri $parametersPath 
```

> [!NOTE]
> <span data-ttu-id="98c03-126">Vous pouvez également déployer des modèles et des paramètres à partir de fichiers locaux.</span><span class="sxs-lookup"><span data-stu-id="98c03-126">You can also deploy templates and parameters from local files.</span></span> <span data-ttu-id="98c03-127">toolearn, voir [à l’aide d’Azure PowerShell avec le stockage Azure](../../storage/common/storage-powershell-guide-full.md).</span><span class="sxs-lookup"><span data-stu-id="98c03-127">toolearn more, see [Using Azure PowerShell with Azure Storage](../../storage/common/storage-powershell-guide-full.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="98c03-128">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="98c03-128">Next Steps</span></span>

- <span data-ttu-id="98c03-129">S’il existe des problèmes de déploiement de hello, vous pouvez examiner [résoudre les erreurs courantes de déploiement Azure avec Azure Resource Manager](../../resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="98c03-129">If there were issues with hello deployment, you might take a look at [Troubleshoot common Azure deployment errors with Azure Resource Manager](../../resource-manager-common-deployment-errors.md).</span></span>
- <span data-ttu-id="98c03-130">Découvrez comment toocreate et gérer une machine virtuelle dans [créer et gérer des machines virtuelles Windows avec module d’Azure PowerShell hello](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="98c03-130">Learn how toocreate and manage a virtual machine in [Create and manage Windows VMs with hello Azure PowerShell module](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

