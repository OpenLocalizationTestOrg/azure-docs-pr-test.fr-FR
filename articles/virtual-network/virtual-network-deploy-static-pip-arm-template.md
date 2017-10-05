---
title: "Créer une machine virtuelle avec une adresse IP publique statique - Modèle Azure Resource Manager | Microsoft Docs"
description: "Découvrez comment créer une machine virtuelle avec une adresse IP publique statique à l’aide d’un modèle Azure Resource Manager."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d551085a-c7ed-4ec6-b4c3-e9e1cebb774c
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/27/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2f503aa60fdd9b7cf66ef482a1041e34c88e5c01
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-an-azure-resource-manager-template"></a><span data-ttu-id="cf957-103">Créer une machine virtuelle avec une adresse IP publique statique à l’aide d’un modèle Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="cf957-103">Create a VM with a static public IP address using an Azure Resource Manager template</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="cf957-104">portail Azure</span><span class="sxs-lookup"><span data-stu-id="cf957-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="cf957-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="cf957-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="cf957-106">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="cf957-106">Azure CLI</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="cf957-107">Modèle</span><span class="sxs-lookup"><span data-stu-id="cf957-107">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * [<span data-ttu-id="cf957-108">PowerShell (classique)</span><span class="sxs-lookup"><span data-stu-id="cf957-108">PowerShell (Classic)</span></span>](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="cf957-109">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="cf957-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="cf957-110">Cet article traite de l’utilisation du modèle de déploiement Resource Manager que Microsoft recommande pour la plupart des nouveaux déploiements à la place du modèle de déploiement classique.</span><span class="sxs-lookup"><span data-stu-id="cf957-110">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the classic deployment model.</span></span>

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <a name="public-ip-address-resources-in-a-template-file"></a><span data-ttu-id="cf957-111">Ressources d’adresses IP publiques dans un fichier de modèle</span><span class="sxs-lookup"><span data-stu-id="cf957-111">Public IP address resources in a template file</span></span>
<span data-ttu-id="cf957-112">Vous pouvez afficher et télécharger les [exemples de modèles](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="cf957-112">You can view and download the [sample template](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json).</span></span>

<span data-ttu-id="cf957-113">La section ci-dessous illustre la définition de la ressource d’adresse IP publique d’après le scénario ci-dessus :</span><span class="sxs-lookup"><span data-stu-id="cf957-113">The following section shows the definition of the public IP resource, based on the scenario above:</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/publicIPAddresses",
  "name": "[variables('webVMSetting').pipName]",
  "location": "[variables('location')]",
  "properties": {
    "publicIPAllocationMethod": "Static"
  },
  "tags": {
    "displayName": "PublicIPAddress - Web"
  }
},
```

<span data-ttu-id="cf957-114">Notez la propriété **publicIPAllocationMethod** qui a la valeur *Static*.</span><span class="sxs-lookup"><span data-stu-id="cf957-114">Notice the **publicIPAllocationMethod** property, which is set to *Static*.</span></span> <span data-ttu-id="cf957-115">Cette propriété peut avoir la valeur *Dynamic* (par défaut) ou *Static*.</span><span class="sxs-lookup"><span data-stu-id="cf957-115">This property can be either *Dynamic* (default value) or *Static*.</span></span> <span data-ttu-id="cf957-116">La valeur Static garantit que l’adresse IP publique affectée ne changera jamais.</span><span class="sxs-lookup"><span data-stu-id="cf957-116">Setting it to static guarantees that the public IP address assigned will never change.</span></span>

<span data-ttu-id="cf957-117">La section suivante illustre l’association de l’adresse IP publique à une interface réseau :</span><span class="sxs-lookup"><span data-stu-id="cf957-117">The following section shows the association of the public IP address with a network interface:</span></span>

```json
  {
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Network/networkInterfaces",
    "name": "[variables('webVMSetting').nicName]",
    "location": "[variables('location')]",
    "tags": {
    "displayName": "NetworkInterface - Web"
    },
    "dependsOn": [
      "[concat('Microsoft.Network/publicIPAddresses/', variables('webVMSetting').pipName)]",
      "[concat('Microsoft.Network/virtualNetworks/', parameters('vnetName'))]"
    ],
    "properties": {
      "ipConfigurations": [
        {
          "name": "ipconfig1",
          "properties": {
          "privateIPAllocationMethod": "Static",
          "privateIPAddress": "[variables('webVMSetting').ipAddress]",
          "publicIPAddress": {
          "id": "[resourceId('Microsoft.Network/publicIPAddresses',variables('webVMSetting').pipName)]"
          },
          "subnet": {
            "id": "[variables('frontEndSubnetRef')]"
          }
        }
      }
    ]
  }
},
```

<span data-ttu-id="cf957-118">Notez la présence de la propriété **publicIPAddress** qui pointe vers l’**Id** d’une ressource nommée **variables(’webVMSetting’).pipName**.</span><span class="sxs-lookup"><span data-stu-id="cf957-118">Notice the **publicIPAddress** property pointing to the **Id** of a resource named **variables('webVMSetting').pipName**.</span></span> <span data-ttu-id="cf957-119">Il s’agit du nom de la ressource IP publique indiquée ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="cf957-119">That is the name of the public IP resource shown above.</span></span>

<span data-ttu-id="cf957-120">Enfin, l’interface réseau ci-dessus est répertoriée dans la propriété **networkProfile** de la machine virtuelle en cours de création.</span><span class="sxs-lookup"><span data-stu-id="cf957-120">Finally, the network interface above is listed in the **networkProfile** property of the VM being created.</span></span>

```json
      "networkProfile": {
        "networkInterfaces": [
          {
            "id": "[resourceId('Microsoft.Network/networkInterfaces', variables('webVMSetting').nicName)]"
          }
        ]
      }
```

## <a name="deploy-the-template-by-using-click-to-deploy"></a><span data-ttu-id="cf957-121">Déployer le modèle en un clic</span><span class="sxs-lookup"><span data-stu-id="cf957-121">Deploy the template by using click to deploy</span></span>

<span data-ttu-id="cf957-122">L’exemple de modèle disponible dans le référentiel public utilise un fichier de paramètres contenant les valeurs par défaut utilisées pour générer le scénario décrit ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="cf957-122">The sample template available in the public repository uses a parameter file containing the default values used to generate the scenario described above.</span></span> <span data-ttu-id="cf957-123">Pour déployer ce modèle en un clic, cliquez sur **Déployer dans Azure** dans le fichier Readme.md pour le modèle [Machine virtuelle avec PIP statique](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/03-Static-public-IP) .</span><span class="sxs-lookup"><span data-stu-id="cf957-123">To deploy this template using click to deploy, click **Deploy to Azure** in the Readme.md file for the [VM with static PIP](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/03-Static-public-IP) template.</span></span> <span data-ttu-id="cf957-124">Remplacez les valeurs de paramètre par défaut si vous le souhaitez et entrez des valeurs pour les paramètres vides.</span><span class="sxs-lookup"><span data-stu-id="cf957-124">Replace the default parameter values if desired and enter values for the blank parameters.</span></span>  <span data-ttu-id="cf957-125">Suivez les instructions dans le portail pour créer une machine virtuelle avec une adresse IP publique statique.</span><span class="sxs-lookup"><span data-stu-id="cf957-125">Follow the instructions in the portal to create a virtual machine with a static public IP address.</span></span>

## <a name="deploy-the-template-by-using-powershell"></a><span data-ttu-id="cf957-126">Déployer le modèle à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="cf957-126">Deploy the template by using PowerShell</span></span>

<span data-ttu-id="cf957-127">Pour déployer le modèle téléchargé à l’aide de PowerShell, suivez les étapes ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="cf957-127">To deploy the template you downloaded by using PowerShell, follow the steps below.</span></span>

1. <span data-ttu-id="cf957-128">Si vous n’avez jamais utilisé Azure PowerShell, procédez de la manière décrite dans l’article [Installer et configurer Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="cf957-128">If you have never used Azure PowerShell, complete the steps in the [How to Install and Configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="cf957-129">Dans une console PowerShell, exécutez l’applet de commande `New-AzureRmResourceGroup` pour créer un groupe de ressources si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="cf957-129">In a PowerShell console, run the `New-AzureRmResourceGroup` cmdlet to create a new resource group, if necessary.</span></span> <span data-ttu-id="cf957-130">Si vous avez déjà créé un groupe de ressources, passez à l’étape 3.</span><span class="sxs-lookup"><span data-stu-id="cf957-130">If you already have a resource group created, go to step 3.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name PIPTEST -Location westus
    ```

    <span data-ttu-id="cf957-131">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="cf957-131">Expected output:</span></span>
   
        ResourceGroupName : PIPTEST
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/StaticPublicIP

3. <span data-ttu-id="cf957-132">Dans une console PowerShell, exécutez l’applet de commande `New-AzureRmResourceGroupDeployment` pour déployer le modèle.</span><span class="sxs-lookup"><span data-stu-id="cf957-132">In a PowerShell console, run the `New-AzureRmResourceGroupDeployment` cmdlet to deploy the template.</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -Name DeployVM -ResourceGroupName PIPTEST `
        -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json `
        -TemplateParameterUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.parameters.json
    ```

    <span data-ttu-id="cf957-133">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="cf957-133">Expected output:</span></span>
   
        DeploymentName    : DeployVM
        ResourceGroupName : PIPTEST
        ProvisioningState : Succeeded
        Timestamp         : [Date and time]
        Mode              : Incremental
        TemplateLink      :
                            Uri            : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/mas
                            ter/IaaS-Story/03-Static-public-IP/azuredeploy.json
                            ContentVersion : 1.0.0.0
   
        Parameters        :
                            Name                      Type                       Value     
                            ========================  =========================  ==========
                            vnetName                  String                     WTestVNet
                            vnetPrefix                String                     192.168.0.0/16
                            frontEndSubnetName        String                     FrontEnd  
                            frontEndSubnetPrefix      String                     192.168.1.0/24
                            storageAccountNamePrefix  String                     iaasestd  
                            stdStorageType            String                     Standard_LRS
                            osType                    String                     Windows   
                            adminUsername             String                     adminUser
                            adminPassword             SecureString                         
   
        Outputs           :

## <a name="deploy-the-template-by-using-the-azure-cli"></a><span data-ttu-id="cf957-134">Déployer le modèle à l’aide de l’interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="cf957-134">Deploy the template by using the Azure CLI</span></span>
<span data-ttu-id="cf957-135">Pour déployer le modèle à l’aide d’Azure CLI, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="cf957-135">To deploy the template by using the Azure CLI, complete the following steps:</span></span>

1. <span data-ttu-id="cf957-136">Si vous n’avez jamais utilisé Azure CLI, procédez de la manière décrite dans l’article [Installer et configurer l’interface de ligne de commande Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="cf957-136">If you have never used Azure CLI, follow the steps in the [Install and Configure the Azure CLI](../cli-install-nodejs.md) article to install and configure it.</span></span>
2. <span data-ttu-id="cf957-137">Exécutez la commande `azure config mode` pour passer en mode Resource Manager, comme illustré ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="cf957-137">Run the `azure config mode` command to switch to Resource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="cf957-138">Voici la sortie attendue de la commande ci-dessus :</span><span class="sxs-lookup"><span data-stu-id="cf957-138">The expected output for the command above:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="cf957-139">Ouvrez le [fichier de paramètres](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.parameters.json), sélectionnez son contenu et enregistrez-le dans un fichier sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="cf957-139">Open the [parameter file](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.parameters.json), select its content, and save it to a file in your computer.</span></span> <span data-ttu-id="cf957-140">Pour cet exemple, les paramètres sont enregistrés dans un fichier nommé *parameters.json*.</span><span class="sxs-lookup"><span data-stu-id="cf957-140">For this example, the parameters are saved to a file named *parameters.json*.</span></span> <span data-ttu-id="cf957-141">Modifiez les valeurs de paramètre dans le fichier si vous le souhaitez. Il est recommandé de modifier au minimum la valeur du paramètre adminPassword en un mot de passe complexe unique.</span><span class="sxs-lookup"><span data-stu-id="cf957-141">Change the parameter values within the file if desired, but at a minimum, it's recommended that you change the value for the adminPassword parameter to a unique, complex password.</span></span>
4. <span data-ttu-id="cf957-142">Exécutez la commande `azure group deployment create` pour déployer le nouveau réseau virtuel à l’aide du modèle et des fichiers de paramètres que vous avez téléchargés et modifiés plus haut.</span><span class="sxs-lookup"><span data-stu-id="cf957-142">Run the `azure group deployment create` cmd to deploy the new VNet by using the template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="cf957-143">Dans la commande ci-dessous, remplacez <path> par le chemin d’accès dans lequel vous avez enregistré le fichier.</span><span class="sxs-lookup"><span data-stu-id="cf957-143">In the command below, replace <path> with the path you saved the file to.</span></span> 

    ```azurecli
    azure group create -n PIPTEST2 -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json -e <path>\parameters.json
    ```

    <span data-ttu-id="cf957-144">Sortie attendue (répertorie les valeurs de paramètre utilisées) :</span><span class="sxs-lookup"><span data-stu-id="cf957-144">Expected output (lists parameter values used):</span></span>

        info:    Executing command group create
        + Getting resource group PIPTEST2
        + Creating resource group PIPTEST2
        info:    Created resource group PIPTEST2
        + Initializing template configurations and parameters
        + Creating a deployment
        info:    Created template deployment "azuredeploy"
        data:    Id:                  /subscriptions/[Subscription ID]/resourceGroups/PIPTEST2
        data:    Name:                PIPTEST2
        data:    Location:            westus
        data:    Provisioning State:  Succeeded
        data:    Tags: null
        data:
        info:    group create command OK

