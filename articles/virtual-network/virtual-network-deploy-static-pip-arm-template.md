---
title: "aaaCreate une machine virtuelle avec une adresse IP publique statique - modèle Azure Resource Manager | Documents Microsoft"
description: "Découvrez comment toocreate une machine virtuelle avec une adresse IP publique statique d’adresses à l’aide d’un modèle Azure Resource Manager."
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
ms.openlocfilehash: 6a8640ed4fad06b0e09820e6114fd6789db73847
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-an-azure-resource-manager-template"></a><span data-ttu-id="f397a-103">Créer une machine virtuelle avec une adresse IP publique statique à l’aide d’un modèle Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f397a-103">Create a VM with a static public IP address using an Azure Resource Manager template</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f397a-104">portail Azure</span><span class="sxs-lookup"><span data-stu-id="f397a-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="f397a-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f397a-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="f397a-106">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="f397a-106">Azure CLI</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="f397a-107">Modèle</span><span class="sxs-lookup"><span data-stu-id="f397a-107">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * [<span data-ttu-id="f397a-108">PowerShell (classique)</span><span class="sxs-lookup"><span data-stu-id="f397a-108">PowerShell (Classic)</span></span>](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="f397a-109">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="f397a-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="f397a-110">Cet article décrit à l’aide du modèle de déploiement Resource Manager hello, qui recommandées par Microsoft pour la plupart des déploiements de nouveau au lieu du modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="f397a-110">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <a name="public-ip-address-resources-in-a-template-file"></a><span data-ttu-id="f397a-111">Ressources d’adresses IP publiques dans un fichier de modèle</span><span class="sxs-lookup"><span data-stu-id="f397a-111">Public IP address resources in a template file</span></span>
<span data-ttu-id="f397a-112">Vous pouvez afficher et télécharger hello [exemple de modèle](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="f397a-112">You can view and download hello [sample template](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json).</span></span>

<span data-ttu-id="f397a-113">Hello section suivante montre définition hello de ressource IP publique hello, selon le scénario hello ci-dessus :</span><span class="sxs-lookup"><span data-stu-id="f397a-113">hello following section shows hello definition of hello public IP resource, based on hello scenario above:</span></span>

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

<span data-ttu-id="f397a-114">Hello d’avis **publicIPAllocationMethod** propriété, qui est définie trop*statique*.</span><span class="sxs-lookup"><span data-stu-id="f397a-114">Notice hello **publicIPAllocationMethod** property, which is set too*Static*.</span></span> <span data-ttu-id="f397a-115">Cette propriété peut avoir la valeur *Dynamic* (par défaut) ou *Static*.</span><span class="sxs-lookup"><span data-stu-id="f397a-115">This property can be either *Dynamic* (default value) or *Static*.</span></span> <span data-ttu-id="f397a-116">Définir les garanties toostatic qui adresse IP publique hello attribuée ne change pas.</span><span class="sxs-lookup"><span data-stu-id="f397a-116">Setting it toostatic guarantees that hello public IP address assigned will never change.</span></span>

<span data-ttu-id="f397a-117">Hello section suivante montre association hello d’adresse IP publique de hello avec une interface réseau :</span><span class="sxs-lookup"><span data-stu-id="f397a-117">hello following section shows hello association of hello public IP address with a network interface:</span></span>

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

<span data-ttu-id="f397a-118">Hello d’avis **publicIPAddress** propriété pointant toohello **Id** d’une ressource nommée **variables('webVMSetting').pipName**.</span><span class="sxs-lookup"><span data-stu-id="f397a-118">Notice hello **publicIPAddress** property pointing toohello **Id** of a resource named **variables('webVMSetting').pipName**.</span></span> <span data-ttu-id="f397a-119">Qui est le nom hello de ressource IP publique hello indiquée ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="f397a-119">That is hello name of hello public IP resource shown above.</span></span>

<span data-ttu-id="f397a-120">Enfin, interface de réseau hello ci-dessus est répertorié dans hello **VM** propriété Hello machine virtuelle en cours de création.</span><span class="sxs-lookup"><span data-stu-id="f397a-120">Finally, hello network interface above is listed in hello **networkProfile** property of hello VM being created.</span></span>

```json
      "networkProfile": {
        "networkInterfaces": [
          {
            "id": "[resourceId('Microsoft.Network/networkInterfaces', variables('webVMSetting').nicName)]"
          }
        ]
      }
```

## <a name="deploy-hello-template-by-using-click-toodeploy"></a><span data-ttu-id="f397a-121">Déployer le modèle de hello à l’aide de cliquez sur toodeploy</span><span class="sxs-lookup"><span data-stu-id="f397a-121">Deploy hello template by using click toodeploy</span></span>

<span data-ttu-id="f397a-122">Hello exemple de modèle disponible dans le référentiel de public hello utilise un fichier de paramètre contenant le scénario hello hello par défaut les valeurs utilisées toogenerate décrit ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="f397a-122">hello sample template available in hello public repository uses a parameter file containing hello default values used toogenerate hello scenario described above.</span></span> <span data-ttu-id="f397a-123">toodeploy ce modèle à l’aide cliquez sur toodeploy, cliquez sur **déployer tooAzure** dans le fichier Readme.md hello hello [machine virtuelle avec PIP statique](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/03-Static-public-IP) modèle.</span><span class="sxs-lookup"><span data-stu-id="f397a-123">toodeploy this template using click toodeploy, click **Deploy tooAzure** in hello Readme.md file for hello [VM with static PIP](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/03-Static-public-IP) template.</span></span> <span data-ttu-id="f397a-124">Remplacez les valeurs de paramètre par défaut hello si vous le souhaitez et entrez des valeurs pour les paramètres vide hello.</span><span class="sxs-lookup"><span data-stu-id="f397a-124">Replace hello default parameter values if desired and enter values for hello blank parameters.</span></span>  <span data-ttu-id="f397a-125">Suivez les instructions de hello de toocreate de portail hello une machine virtuelle avec une adresse IP publique statique.</span><span class="sxs-lookup"><span data-stu-id="f397a-125">Follow hello instructions in hello portal toocreate a virtual machine with a static public IP address.</span></span>

## <a name="deploy-hello-template-by-using-powershell"></a><span data-ttu-id="f397a-126">Déployer le modèle de hello à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="f397a-126">Deploy hello template by using PowerShell</span></span>

<span data-ttu-id="f397a-127">modèle de hello toodeploy vous avez téléchargé à l’aide de PowerShell, suivez les étapes de hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="f397a-127">toodeploy hello template you downloaded by using PowerShell, follow hello steps below.</span></span>

1. <span data-ttu-id="f397a-128">Si vous n’avez jamais utilisé Azure PowerShell, hello terminé les étapes Bonjour [comment tooInstall et configurer Azure PowerShell](/powershell/azure/overview) l’article.</span><span class="sxs-lookup"><span data-stu-id="f397a-128">If you have never used Azure PowerShell, complete hello steps in hello [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="f397a-129">Dans une console PowerShell, exécutez hello `New-AzureRmResourceGroup` toocreate de l’applet de commande Nouveau groupe de ressources, si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="f397a-129">In a PowerShell console, run hello `New-AzureRmResourceGroup` cmdlet toocreate a new resource group, if necessary.</span></span> <span data-ttu-id="f397a-130">Si vous avez déjà créé un groupe de ressources, accédez à toostep 3.</span><span class="sxs-lookup"><span data-stu-id="f397a-130">If you already have a resource group created, go toostep 3.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name PIPTEST -Location westus
    ```

    <span data-ttu-id="f397a-131">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="f397a-131">Expected output:</span></span>
   
        ResourceGroupName : PIPTEST
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/StaticPublicIP

3. <span data-ttu-id="f397a-132">Dans une console PowerShell, exécutez hello `New-AzureRmResourceGroupDeployment` modèle de hello toodeploy applet de commande.</span><span class="sxs-lookup"><span data-stu-id="f397a-132">In a PowerShell console, run hello `New-AzureRmResourceGroupDeployment` cmdlet toodeploy hello template.</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -Name DeployVM -ResourceGroupName PIPTEST `
        -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json `
        -TemplateParameterUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.parameters.json
    ```

    <span data-ttu-id="f397a-133">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="f397a-133">Expected output:</span></span>
   
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

## <a name="deploy-hello-template-by-using-hello-azure-cli"></a><span data-ttu-id="f397a-134">Déployer le modèle de hello à l’aide de hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="f397a-134">Deploy hello template by using hello Azure CLI</span></span>
<span data-ttu-id="f397a-135">modèle de hello toodeploy à l’aide de hello CLI d’Azure, hello complète comme suit :</span><span class="sxs-lookup"><span data-stu-id="f397a-135">toodeploy hello template by using hello Azure CLI, complete hello following steps:</span></span>

1. <span data-ttu-id="f397a-136">Si vous n’avez jamais utilisé CLI d’Azure, suivez les étapes de hello Bonjour [installer et configurer hello CLI d’Azure](../cli-install-nodejs.md) tooinstall de l’article et le configurer.</span><span class="sxs-lookup"><span data-stu-id="f397a-136">If you have never used Azure CLI, follow hello steps in hello [Install and Configure hello Azure CLI](../cli-install-nodejs.md) article tooinstall and configure it.</span></span>
2. <span data-ttu-id="f397a-137">Exécutez hello `azure config mode` mode Manager tooResource commande tooswitch, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="f397a-137">Run hello `azure config mode` command tooswitch tooResource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="f397a-138">Hello attendu la sortie de commande hello ci-dessus :</span><span class="sxs-lookup"><span data-stu-id="f397a-138">hello expected output for hello command above:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="f397a-139">Ouvrez hello [fichier de paramètres](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.parameters.json), sélectionnez son contenu et enregistrez-le tooa fichier sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="f397a-139">Open hello [parameter file](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.parameters.json), select its content, and save it tooa file in your computer.</span></span> <span data-ttu-id="f397a-140">Pour cet exemple, les paramètres de hello sont enregistrés les fichiers tooa nommé *parameters.json*.</span><span class="sxs-lookup"><span data-stu-id="f397a-140">For this example, hello parameters are saved tooa file named *parameters.json*.</span></span> <span data-ttu-id="f397a-141">Modifier les valeurs de paramètre hello dans fichier hello si vous le souhaitez, mais au minimum, il est recommandé de modifier la valeur hello pour hello adminPassword paramètre tooa unique mot de passe complexe.</span><span class="sxs-lookup"><span data-stu-id="f397a-141">Change hello parameter values within hello file if desired, but at a minimum, it's recommended that you change hello value for hello adminPassword parameter tooa unique, complex password.</span></span>
4. <span data-ttu-id="f397a-142">Exécutez hello `azure group deployment create` cmd toodeploy hello nouveau réseau virtuel à l’aide des paramètres et modèle de hello fichiers téléchargés et de modifier les propriétés.</span><span class="sxs-lookup"><span data-stu-id="f397a-142">Run hello `azure group deployment create` cmd toodeploy hello new VNet by using hello template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="f397a-143">Dans la commande de hello ci-dessous, remplacez <path> avec le chemin d’accès hello vous avez enregistré le fichier hello.</span><span class="sxs-lookup"><span data-stu-id="f397a-143">In hello command below, replace <path> with hello path you saved hello file to.</span></span> 

    ```azurecli
    azure group create -n PIPTEST2 -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json -e <path>\parameters.json
    ```

    <span data-ttu-id="f397a-144">Sortie attendue (répertorie les valeurs de paramètre utilisées) :</span><span class="sxs-lookup"><span data-stu-id="f397a-144">Expected output (lists parameter values used):</span></span>

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

