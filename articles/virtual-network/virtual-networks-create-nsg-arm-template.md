---
title: "aaaCreate réseau des groupes de sécurité - modèle de gestionnaire de ressources Azure | Documents Microsoft"
description: "Découvrez comment toocreate et déployer des groupes de sécurité réseau à l’aide d’un modèle Azure Resource Manager."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: f3e7385d-717c-44ff-be20-f9aa450aa99b
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3750168284fea7b41c8c0f908b0d31a9da5e38ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-network-security-groups-using-an-azure-resource-manager-template"></a><span data-ttu-id="ff482-103">Créer des groupes de sécurité réseau à l’aide d’un modèle Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ff482-103">Create network security groups using an Azure Resource Manager template</span></span>

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="ff482-104">Cet article décrit le modèle de déploiement du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="ff482-104">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="ff482-105">Vous pouvez également [créer des groupes de sécurité réseau dans le modèle de déploiement classique hello](virtual-networks-create-nsg-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="ff482-105">You can also [create NSGs in hello classic deployment model](virtual-networks-create-nsg-classic-ps.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

## <a name="nsg-resources-in-a-template-file"></a><span data-ttu-id="ff482-106">Ressources NSG dans un fichier de modèle</span><span class="sxs-lookup"><span data-stu-id="ff482-106">NSG resources in a template file</span></span>
<span data-ttu-id="ff482-107">Vous pouvez afficher et télécharger hello [exemple de modèle](https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/NSGs.json).</span><span class="sxs-lookup"><span data-stu-id="ff482-107">You can view and download hello [sample template](https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/NSGs.json).</span></span>

<span data-ttu-id="ff482-108">Hello section suivante présente définition hello Hello NSG frontal, selon le scénario de hello.</span><span class="sxs-lookup"><span data-stu-id="ff482-108">hello following section shows hello definition of hello front-end NSG, based on hello scenario.</span></span>

```json
"apiVersion": "2015-06-15",
"type": "Microsoft.Network/networkSecurityGroups",
"name": "[parameters('frontEndNSGName')]",
"location": "[resourceGroup().location]",
"tags": {
  "displayName": "NSG - Front End"
},
"properties": {
  "securityRules": [
    {
      "name": "rdp-rule",
      "properties": {
        "description": "Allow RDP",
        "protocol": "Tcp",
        "sourcePortRange": "*",
        "destinationPortRange": "3389",
        "sourceAddressPrefix": "Internet",
        "destinationAddressPrefix": "*",
        "access": "Allow",
        "priority": 100,
        "direction": "Inbound"
      }
    },
    {
      "name": "web-rule",
      "properties": {
        "description": "Allow WEB",
        "protocol": "Tcp",
        "sourcePortRange": "*",
        "destinationPortRange": "80",
        "sourceAddressPrefix": "Internet",
        "destinationAddressPrefix": "*",
        "access": "Allow",
        "priority": 101,
        "direction": "Inbound"
      }
    }
  ]
}
```
<span data-ttu-id="ff482-109">tooassociate hello NSG toohello sous-réseau frontal, vous disposez de définition de sous-réseau toochange hello dans le modèle de hello et utiliser l’id référence hello pour hello groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="ff482-109">tooassociate hello NSG toohello front-end subnet, you have toochange hello subnet definition in hello template, and use hello reference id for hello NSG.</span></span>

```json
"subnets": [
  {
    "name": "[parameters('frontEndSubnetName')]",
    "properties": {
      "addressPrefix": "[parameters('frontEndSubnetPrefix')]",
      "networkSecurityGroup": {
      "id": "[resourceId('Microsoft.Network/networkSecurityGroups', parameters('frontEndNSGName'))]"
      }
    }
  }, 
```

<span data-ttu-id="ff482-110">Notez que même en cours d’exécution pour hello principal groupe de sécurité réseau et hello sous-réseau principal dans le modèle de hello hello.</span><span class="sxs-lookup"><span data-stu-id="ff482-110">Notice hello same being done for hello back-end NSG and hello back-end subnet in hello template.</span></span>

## <a name="deploy-hello-arm-template-by-using-click-toodeploy"></a><span data-ttu-id="ff482-111">Déployer le modèle de hello ARM à l’aide de cliquez sur toodeploy</span><span class="sxs-lookup"><span data-stu-id="ff482-111">Deploy hello ARM template by using click toodeploy</span></span>
<span data-ttu-id="ff482-112">Hello exemple de modèle disponible dans le référentiel de public hello utilise un fichier de paramètre contenant le scénario hello hello par défaut les valeurs utilisées toogenerate décrit ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="ff482-112">hello sample template available in hello public repository uses a parameter file containing hello default values used toogenerate hello scenario described above.</span></span> <span data-ttu-id="ff482-113">toodeploy ce modèle à l’aide de cliquez toodeploy, suivez [ce lien](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd-NSG), cliquez sur **déployer tooAzure**, remplacez les valeurs de paramètre par défaut hello si nécessaire et suivez les instructions de hello dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="ff482-113">toodeploy this template using click toodeploy, follow [this link](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd-NSG), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>

## <a name="deploy-hello-arm-template-by-using-powershell"></a><span data-ttu-id="ff482-114">Déployer le modèle de hello ARM à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="ff482-114">Deploy hello ARM template by using PowerShell</span></span>
<span data-ttu-id="ff482-115">modèle d’ARM hello toodeploy vous avez téléchargé à l’aide de PowerShell, suivez les étapes de hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="ff482-115">toodeploy hello ARM template you downloaded by using PowerShell, follow hello steps below.</span></span>

1. <span data-ttu-id="ff482-116">Si vous n’avez jamais utilisé Azure PowerShell, suivez les instructions de hello Bonjour [comment tooInstall et configurer Azure PowerShell](/powershell/azure/overview) tooinstall et le configurer.</span><span class="sxs-lookup"><span data-stu-id="ff482-116">If you have never used Azure PowerShell, follow hello instructions in hello [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) tooinstall and configure it.</span></span>
2. <span data-ttu-id="ff482-117">Exécutez hello  **`New-AzureRmResourceGroup`**  toocreate d’applet de commande un groupe de ressources à l’aide de hello modèle.</span><span class="sxs-lookup"><span data-stu-id="ff482-117">Run hello **`New-AzureRmResourceGroup`** cmdlet toocreate a resource group using hello template.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name TestRG -Location uswest `
    -TemplateFile 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.json' `
    -TemplateParameterFile 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.parameters.json'
    ```

    <span data-ttu-id="ff482-118">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="ff482-118">Expected output:</span></span>

        ResourceGroupName : TestRG
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
                            Actions  NotActions
                            =======  ==========
                            *                  
   
        Resources         :
                            Name                Type                                     Location
                            ==================  =======================================  ========
                            sqlAvSet            Microsoft.Compute/availabilitySets       westus  
                            webAvSet            Microsoft.Compute/availabilitySets       westus  
                            SQL1                Microsoft.Compute/virtualMachines        westus  
                            SQL2                Microsoft.Compute/virtualMachines        westus  
                            Web1                Microsoft.Compute/virtualMachines        westus  
                            Web2                Microsoft.Compute/virtualMachines        westus  
                            TestNICSQL1         Microsoft.Network/networkInterfaces      westus  
                            TestNICSQL2         Microsoft.Network/networkInterfaces      westus  
                            TestNICWeb1         Microsoft.Network/networkInterfaces      westus  
                            TestNICWeb2         Microsoft.Network/networkInterfaces      westus  
                            NSG-BackEnd         Microsoft.Network/networkSecurityGroups  westus  
                            NSG-FrontEnd        Microsoft.Network/networkSecurityGroups  westus  
                            TestPIPSQL1         Microsoft.Network/publicIPAddresses      westus  
                            TestPIPSQL2         Microsoft.Network/publicIPAddresses      westus  
                            TestPIPWeb1         Microsoft.Network/publicIPAddresses      westus  
                            TestPIPWeb2         Microsoft.Network/publicIPAddresses      westus  
                            TestVNet            Microsoft.Network/virtualNetworks        westus  
                            testvnetstorageprm  Microsoft.Storage/storageAccounts        westus  
                            testvnetstoragestd  Microsoft.Storage/storageAccounts        westus  
   
        ResourceId        : /subscriptions/[Subscription Id]/resourceGroups/TestRG

## <a name="deploy-hello-arm-template-by-using-hello-azure-cli"></a><span data-ttu-id="ff482-119">Déployer le modèle de hello ARM à l’aide de hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="ff482-119">Deploy hello ARM template by using hello Azure CLI</span></span>
<span data-ttu-id="ff482-120">modèle ARM hello toodeploy à l’aide de hello CLI d’Azure, suivez les étapes de hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="ff482-120">toodeploy hello ARM template by using hello Azure CLI, follow hello steps below.</span></span>

1. <span data-ttu-id="ff482-121">Si vous n’avez jamais utilisé CLI d’Azure, consultez [installer et configurer hello CLI d’Azure](../cli-install-nodejs.md) et suivez les instructions de hello point toohello où vous sélectionnez votre compte Azure et votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="ff482-121">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="ff482-122">Exécutez hello  **`azure config mode`**  mode Manager tooResource commande tooswitch, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="ff482-122">Run hello **`azure config mode`** command tooswitch tooResource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="ff482-123">Hello Voici la sortie hello attendu pour la commande hello :</span><span class="sxs-lookup"><span data-stu-id="ff482-123">hello following is hello expected output for hello command:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="ff482-124">Exécutez hello  **`azure group deployment create`**  applet de commande toodeploy hello nouveau réseau virtuel à l’aide des paramètres et modèle de hello fichiers téléchargés et de modifier les propriétés.</span><span class="sxs-lookup"><span data-stu-id="ff482-124">Run hello **`azure group deployment create`** cmdlet toodeploy hello new VNet by using hello template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="ff482-125">liste de Hello affiché après la sortie de hello explique paramètres hello utilisés.</span><span class="sxs-lookup"><span data-stu-id="ff482-125">hello list shown after hello output explains hello parameters used.</span></span>

    ```azurecli
    azure group create -n TestRG -l westus -f 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.json' -e 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.parameters.json'
    ```

    <span data-ttu-id="ff482-126">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="ff482-126">Expected output:</span></span>
   
        info:    Executing command group create
        info:    Getting resource group TestRG
        info:    Creating resource group TestRG
        info:    Created resource group TestRG
        info:    Initializing template configurations and parameters
        info:    Creating a deployment
        info:    Created template deployment "azuredeploy"
        data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG
        data:    Name:                TestRG
        data:    Location:            westus
        data:    Provisioning State:  Succeeded
        data:    Tags: null
        data:    
        info:    group create command OK
   
   * <span data-ttu-id="ff482-127">**-n (ou --name)**.</span><span class="sxs-lookup"><span data-stu-id="ff482-127">**-n (or --name)**.</span></span> <span data-ttu-id="ff482-128">Nom de toobe de groupe de ressources hello créé.</span><span class="sxs-lookup"><span data-stu-id="ff482-128">Name of hello resource group toobe created.</span></span>
   * <span data-ttu-id="ff482-129">**-l (ou --location)**.</span><span class="sxs-lookup"><span data-stu-id="ff482-129">**-l (or --location)**.</span></span> <span data-ttu-id="ff482-130">Région Azure où le groupe de ressources hello sera créé.</span><span class="sxs-lookup"><span data-stu-id="ff482-130">Azure region where hello resource group will be created.</span></span>
   * <span data-ttu-id="ff482-131">**-f (ou --template-file)**.</span><span class="sxs-lookup"><span data-stu-id="ff482-131">**-f (or --template-file)**.</span></span> <span data-ttu-id="ff482-132">Fichier de modèle de chemin d’accès tooyour ARM.</span><span class="sxs-lookup"><span data-stu-id="ff482-132">Path tooyour ARM template file.</span></span>
   * <span data-ttu-id="ff482-133">**-e (ou --parameters-file)**.</span><span class="sxs-lookup"><span data-stu-id="ff482-133">**-e (or --parameters-file)**.</span></span> <span data-ttu-id="ff482-134">Fichier de paramètres de chemin d’accès tooyour ARM.</span><span class="sxs-lookup"><span data-stu-id="ff482-134">Path tooyour ARM parameters file.</span></span>

