---
title: "aaaCreate un réseau virtuel | Modèle de gestionnaire de ressources Azure | Documents Microsoft"
description: "Découvrez comment toocreate un virtuel réseau à l’aide d’un modèle Azure Resource Manager."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 69530861-2f97-4a6e-b336-a7baf2690044
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b9c289433ff2a84bec19eac25fa28ab40d131c7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-using-an-azure-resource-manager-template"></a><span data-ttu-id="1ba96-103">Créer un réseau virtuel à l’aide d’un modèle Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1ba96-103">Create a virtual network using an Azure Resource Manager template</span></span>

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

<span data-ttu-id="1ba96-104">Azure propose deux modèles de déploiement : Azure Resource Manager et classique.</span><span class="sxs-lookup"><span data-stu-id="1ba96-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="1ba96-105">Microsoft recommande de créer des ressources via le modèle de déploiement du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="1ba96-105">Microsoft recommends creating resources through hello Resource Manager deployment model.</span></span> <span data-ttu-id="1ba96-106">toolearn en savoir plus sur hello différences entre hello deux modèles, lire hello [modèles de déploiement Azure de comprendre](../azure-resource-manager/resource-manager-deployment-model.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="1ba96-106">toolearn more about hello differences between hello two models, read hello [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>
 
<span data-ttu-id="1ba96-107">Cet article explique comment toocreate un réseau virtuel via le déploiement du Gestionnaire de ressources hello modèle à l’aide d’un modèle Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1ba96-107">This article explains how toocreate a VNet through hello Resource Manager deployment model using an Azure Resource Manager template.</span></span> <span data-ttu-id="1ba96-108">Vous pouvez également créer un réseau virtuel via le Gestionnaire de ressources à l’aide d’autres outils ou créer un réseau virtuel via le modèle de déploiement classique hello en sélectionnant une option différente de hello suivant liste :</span><span class="sxs-lookup"><span data-stu-id="1ba96-108">You can also create a VNet through Resource Manager using other tools or create a VNet through hello classic deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
- [<span data-ttu-id="1ba96-109">Portail</span><span class="sxs-lookup"><span data-stu-id="1ba96-109">Portal</span></span>](virtual-networks-create-vnet-arm-pportal.md)
- [<span data-ttu-id="1ba96-110">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1ba96-110">PowerShell</span></span>](virtual-networks-create-vnet-arm-ps.md)
- [<span data-ttu-id="1ba96-111">INTERFACE DE LIGNE DE COMMANDE</span><span class="sxs-lookup"><span data-stu-id="1ba96-111">CLI</span></span>](virtual-networks-create-vnet-arm-cli.md)
- [<span data-ttu-id="1ba96-112">Modèle</span><span class="sxs-lookup"><span data-stu-id="1ba96-112">Template</span></span>](virtual-networks-create-vnet-arm-template-click.md)
- [<span data-ttu-id="1ba96-113">Portail (classique)</span><span class="sxs-lookup"><span data-stu-id="1ba96-113">Portal (Classic)</span></span>](virtual-networks-create-vnet-classic-pportal.md)
- [<span data-ttu-id="1ba96-114">PowerShell (classique)</span><span class="sxs-lookup"><span data-stu-id="1ba96-114">PowerShell (Classic)</span></span>](virtual-networks-create-vnet-classic-netcfg-ps.md)
- [<span data-ttu-id="1ba96-115">Interface de ligne de commande (classique)</span><span class="sxs-lookup"><span data-stu-id="1ba96-115">CLI (Classic)</span></span>](virtual-networks-create-vnet-classic-cli.md)

<span data-ttu-id="1ba96-116">Vous allez apprendre comment toodownload et modifier existant modèle ARM à partir de GitHub et déployer le modèle hello à partir de GitHub, PowerShell et hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="1ba96-116">You will learn how toodownload and modify and existing ARM template from GitHub, and deploy hello template from GitHub, PowerShell, and hello Azure CLI.</span></span>

<span data-ttu-id="1ba96-117">Si vous déployez simplement modèle ARM de hello directement à partir de GitHub, sans aucune modification, ignorez trop[déployer un modèle à partir de github](#deploy-the-arm-template-by-using-click-to-deploy).</span><span class="sxs-lookup"><span data-stu-id="1ba96-117">If you are simply deploying hello ARM template directly from GitHub, without any changes, skip too[deploy a template from github](#deploy-the-arm-template-by-using-click-to-deploy).</span></span>

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="download-and-understand-hello-azure-resource-manager-template"></a><span data-ttu-id="1ba96-118">Télécharger et de comprendre le modèle de gestionnaire de ressources Azure hello</span><span class="sxs-lookup"><span data-stu-id="1ba96-118">Download and understand hello Azure Resource Manager template</span></span>
<span data-ttu-id="1ba96-119">Vous pouvez télécharger le modèle existant de hello pour la création d’un réseau virtuel et deux sous-réseaux à partir de GitHub, apporter des modifications que vous souhaitez et la réutiliser.</span><span class="sxs-lookup"><span data-stu-id="1ba96-119">You can download hello existing template for creating a VNet and two subnets from GitHub, make any changes you might want, and reuse it.</span></span> <span data-ttu-id="1ba96-120">toodo effectuez donc hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="1ba96-120">toodo so, complete hello following steps:</span></span>

1. <span data-ttu-id="1ba96-121">Accédez trop[page de modèle exemple hello](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).</span><span class="sxs-lookup"><span data-stu-id="1ba96-121">Navigate too[hello sample template page](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).</span></span>
2. <span data-ttu-id="1ba96-122">Cliquez sur **azuredeploy.json**, puis sur **RAW**.</span><span class="sxs-lookup"><span data-stu-id="1ba96-122">Click **azuredeploy.json**, and then click **RAW**.</span></span>
3. <span data-ttu-id="1ba96-123">Enregistrez hello fichier tooa un dossier local sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="1ba96-123">Save hello file tooa a local folder on your computer.</span></span>
4. <span data-ttu-id="1ba96-124">Si vous êtes familiarisé avec les modèles, passez toostep 7.</span><span class="sxs-lookup"><span data-stu-id="1ba96-124">If you are familiar with templates, skip toostep 7.</span></span>
5. <span data-ttu-id="1ba96-125">Ouvrir le fichier hello vous venez d’enregistrer et d’examiner le contenu de hello sous **paramètres** à la ligne 5.</span><span class="sxs-lookup"><span data-stu-id="1ba96-125">Open hello file you just saved and look at hello contents under **parameters** in line 5.</span></span> <span data-ttu-id="1ba96-126">Les paramètres de modèle ARM fournissent un espace réservé pour les valeurs à remplir lors du déploiement.</span><span class="sxs-lookup"><span data-stu-id="1ba96-126">ARM template parameters provide a placeholder for values that can be filled out during deployment.</span></span>
   
   | <span data-ttu-id="1ba96-127">Paramètre</span><span class="sxs-lookup"><span data-stu-id="1ba96-127">Parameter</span></span> | <span data-ttu-id="1ba96-128">Description</span><span class="sxs-lookup"><span data-stu-id="1ba96-128">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="1ba96-129">**location**</span><span class="sxs-lookup"><span data-stu-id="1ba96-129">**location**</span></span> |<span data-ttu-id="1ba96-130">Région Azure où hello réseau virtuel sera créé</span><span class="sxs-lookup"><span data-stu-id="1ba96-130">Azure region where hello VNet will be created</span></span> |
   | <span data-ttu-id="1ba96-131">**vnetName**</span><span class="sxs-lookup"><span data-stu-id="1ba96-131">**vnetName**</span></span> |<span data-ttu-id="1ba96-132">Nom de hello nouveau réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="1ba96-132">Name for hello new VNet</span></span> |
   | <span data-ttu-id="1ba96-133">**addressPrefix**</span><span class="sxs-lookup"><span data-stu-id="1ba96-133">**addressPrefix**</span></span> |<span data-ttu-id="1ba96-134">Espace d’adressage pour hello réseau virtuel, au format CIDR</span><span class="sxs-lookup"><span data-stu-id="1ba96-134">Address space for hello VNet, in CIDR format</span></span> |
   | <span data-ttu-id="1ba96-135">**subnet1Name**</span><span class="sxs-lookup"><span data-stu-id="1ba96-135">**subnet1Name**</span></span> |<span data-ttu-id="1ba96-136">Nom de hello premier réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="1ba96-136">Name for hello first VNet</span></span> |
   | <span data-ttu-id="1ba96-137">**subnet1Prefix**</span><span class="sxs-lookup"><span data-stu-id="1ba96-137">**subnet1Prefix**</span></span> |<span data-ttu-id="1ba96-138">Bloc CIDR pour le premier sous-réseau de hello</span><span class="sxs-lookup"><span data-stu-id="1ba96-138">CIDR block for hello first subnet</span></span> |
   | <span data-ttu-id="1ba96-139">**subnet2Name**</span><span class="sxs-lookup"><span data-stu-id="1ba96-139">**subnet2Name**</span></span> |<span data-ttu-id="1ba96-140">Nom de hello deuxième réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="1ba96-140">Name for hello second VNet</span></span> |
   | <span data-ttu-id="1ba96-141">**subnet2Prefix**</span><span class="sxs-lookup"><span data-stu-id="1ba96-141">**subnet2Prefix**</span></span> |<span data-ttu-id="1ba96-142">Bloc CIDR pour le sous-réseau de deuxième hello</span><span class="sxs-lookup"><span data-stu-id="1ba96-142">CIDR block for hello second subnet</span></span> |
   
   > [!IMPORTANT]
   > <span data-ttu-id="1ba96-143">Les modèles Azure Resource Manager de GitHub sont susceptibles d’évoluer.</span><span class="sxs-lookup"><span data-stu-id="1ba96-143">Azure Resource Manager templates maintained in GitHub can change over time.</span></span> <span data-ttu-id="1ba96-144">Vérifiez le modèle de hello avant de l’utiliser.</span><span class="sxs-lookup"><span data-stu-id="1ba96-144">Make sure you check hello template before using it.</span></span>
   > 
   > 
6. <span data-ttu-id="1ba96-145">Vérifiez le contenu de hello sous **ressources** et notez les éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="1ba96-145">Check hello content under **resources** and notice hello following:</span></span>
   
   * <span data-ttu-id="1ba96-146">**type**.</span><span class="sxs-lookup"><span data-stu-id="1ba96-146">**type**.</span></span> <span data-ttu-id="1ba96-147">Type de ressource en cours de création par le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="1ba96-147">Type of resource being created by hello template.</span></span> <span data-ttu-id="1ba96-148">Dans ce cas, **Microsoft.Network/virtualNetworks**, qui représente un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="1ba96-148">In this case, **Microsoft.Network/virtualNetworks**, which represent a VNet.</span></span>
   * <span data-ttu-id="1ba96-149">**name**.</span><span class="sxs-lookup"><span data-stu-id="1ba96-149">**name**.</span></span> <span data-ttu-id="1ba96-150">Nom de ressource de hello.</span><span class="sxs-lookup"><span data-stu-id="1ba96-150">Name for hello resource.</span></span> <span data-ttu-id="1ba96-151">Utilisation de hello avis de **[parameters('vnetName')]**, qui signifie hello sera nom fourni en tant qu’entrée par l’utilisateur de hello ou un fichier de paramètres au cours du déploiement.</span><span class="sxs-lookup"><span data-stu-id="1ba96-151">Notice hello use of **[parameters('vnetName')]**, which means hello name will provided as input by hello user or a parameter file during deployment.</span></span>
   * <span data-ttu-id="1ba96-152">**properties**.</span><span class="sxs-lookup"><span data-stu-id="1ba96-152">**properties**.</span></span> <span data-ttu-id="1ba96-153">Liste de propriétés pour la ressource de hello.</span><span class="sxs-lookup"><span data-stu-id="1ba96-153">List of properties for hello resource.</span></span> <span data-ttu-id="1ba96-154">Ce modèle utilise les propriétés d’espace et le sous-réseau d’adresse hello lors de la création du réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="1ba96-154">This template uses hello address space and subnet properties during VNet creation.</span></span>
7. <span data-ttu-id="1ba96-155">Naviguer vers l’arrière trop[page de modèle exemple hello](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).</span><span class="sxs-lookup"><span data-stu-id="1ba96-155">Navigate back too[hello sample template page](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).</span></span>
8. <span data-ttu-id="1ba96-156">Cliquez sur **azuredeploy-paremeters.json**, puis cliquez sur **RAW**.</span><span class="sxs-lookup"><span data-stu-id="1ba96-156">Click **azuredeploy-paremeters.json**, and then click **RAW**.</span></span>
9. <span data-ttu-id="1ba96-157">Enregistrez hello fichier tooa un dossier local sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="1ba96-157">Save hello file tooa a local folder on your computer.</span></span>
10. <span data-ttu-id="1ba96-158">Ouvrez le fichier hello que vous venez d’enregistrer et modifier des valeurs de hello pour les paramètres de hello.</span><span class="sxs-lookup"><span data-stu-id="1ba96-158">Open hello file you just saved and edit hello values for hello parameters.</span></span> <span data-ttu-id="1ba96-159">Utilisez hello valeurs ci-dessous toodeploy hello hello scénario de réseau virtuel suivantes :</span><span class="sxs-lookup"><span data-stu-id="1ba96-159">Use hello following values below toodeploy hello VNet described in hello scenario:</span></span>

    ```json
        {
          "location": {
            "value": "Central US"
          },
          "vnetName": {
              "value": "TestVNet"
          },
          "addressPrefix": {
              "value": "192.168.0.0/16"
          },
          "subnet1Name": {
              "value": "FrontEnd"
          },
          "subnet1Prefix": {
            "value": "192.168.1.0/24"
          },
          "subnet2Name": {
              "value": "BackEnd"
          },
          "subnet2Prefix": {
              "value": "192.168.2.0/24"
          }
        }
    ```

11. <span data-ttu-id="1ba96-160">Enregistrez le fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="1ba96-160">Save hello file.</span></span>


## <a name="deploy-hello-template-using-powershell"></a><span data-ttu-id="1ba96-161">Déployer le modèle de hello à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="1ba96-161">Deploy hello template using PowerShell</span></span>

<span data-ttu-id="1ba96-162">Hello complet suivant le modèle de hello toodeploy étapes que vous avez téléchargé à l’aide de PowerShell :</span><span class="sxs-lookup"><span data-stu-id="1ba96-162">Complete hello following steps toodeploy hello template you downloaded by using PowerShell:</span></span>

1. <span data-ttu-id="1ba96-163">Installer et configurer Azure PowerShell en effectuant les étapes hello Bonjour [comment tooInstall et configurer Azure PowerShell](/powershell/azure/overview) l’article.</span><span class="sxs-lookup"><span data-stu-id="1ba96-163">Install and configure Azure PowerShell by completing hello steps in hello [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="1ba96-164">Exécutez hello suivant commande toocreate un groupe de ressources :</span><span class="sxs-lookup"><span data-stu-id="1ba96-164">Run hello following command toocreate a new resource group:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name TestRG -Location centralus
    ```

    <span data-ttu-id="1ba96-165">commande Hello crée un groupe de ressources nommé *TestRG* Bonjour *du centre des États-Unis* région azure.</span><span class="sxs-lookup"><span data-stu-id="1ba96-165">hello command creates a resource group named *TestRG* in hello *Central US* azure region.</span></span> <span data-ttu-id="1ba96-166">Pour plus d’informations sur les groupes de ressources, consultez [Présentation d’Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1ba96-166">For more information about resource groups, visit [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span></span>

    <span data-ttu-id="1ba96-167">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="1ba96-167">Expected output:</span></span>

        ResourceGroupName : TestRG
        Location          : centralus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
                            Actions  NotActions
                            =======  ==========
                            *
        ResourceId        : /subscriptions/[Id]/resourceGroups/TestRG

3. <span data-ttu-id="1ba96-168">Exécutez hello toodeploy hello nouveau réseau virtuel à l’aide de fichiers de modèle et le paramètre hello vous avez téléchargé et de modifier les propriétés de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="1ba96-168">Run hello following command toodeploy hello new VNet using hello template and parameter files you downloaded and modified above:</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestVNetDeployment -ResourceGroupName TestRG `
    -TemplateFile C:\ARM\azuredeploy.json -TemplateParameterFile C:\ARM\azuredeploy-parameters.json
    ```

    <span data-ttu-id="1ba96-169">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="1ba96-169">Expected output:</span></span>
   
        DeploymentName    : TestVNetDeployment
        ResourceGroupName : TestRG
        ProvisioningState : Succeeded
        Timestamp         : [Date and time]
        Mode              : Incremental
        TemplateLink      :
        Parameters        :
                            Name             Type                       Value
                            ===============  =========================  ==========
                            location         String                     Central US
                            vnetName         String                     TestVNet
                            addressPrefix    String                     192.168.0.0/16
                            subnet1Prefix    String                     192.168.1.0/24
                            subnet1Name      String                     FrontEnd
                            subnet2Prefix    String                     192.168.2.0/24
                            subnet2Name      String                     BackEnd
   
        Outputs           :
4. <span data-ttu-id="1ba96-170">Suivante d’exécution hello commande tooview des propriétés de hello Hello nouveau réseau virtuel :</span><span class="sxs-lookup"><span data-stu-id="1ba96-170">Run hello following command tooview hello properties of hello new VNet:</span></span>

    ```powershell
    Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    ```

    <span data-ttu-id="1ba96-171">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="1ba96-171">Expected output:</span></span>

        Name              : TestVNet
        ResourceGroupName : TestRG
        Location          : centralus
        Id                : /subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag              : W/"[Id]"
        ProvisioningState : Succeeded
        Tags              :
        AddressSpace      : {
                              "AddressPrefixes": [
                                "192.168.0.0/16"
                              ]
                            }
        DhcpOptions       : {
                              "DnsServers": null
                            }
        NetworkInterfaces : null
        Subnets           : [
                              {
                                "Name": "FrontEnd",
                                "Etag": "W/\"[Id]\"",
                                "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                "AddressPrefix": "192.168.1.0/24",
                                "IpConfigurations": [],
                                "NetworkSecurityGroup": null,
                                "RouteTable": null,
                                "ProvisioningState": "Succeeded"
                              },
                              {
                                "Name": "BackEnd",
                                "Etag": "W/\"[Id]\"",
                                "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
                                "AddressPrefix": "192.168.2.0/24",
                                "IpConfigurations": [],
                                "NetworkSecurityGroup": null,
                                "RouteTable": null,
                                "ProvisioningState": "Succeeded"
                              }
                            ]

## <a name="deploy-hello-template-using-click-to-deploy"></a><span data-ttu-id="1ba96-172">Déployer à l’aide de clic sur le déploiement de modèle de hello</span><span class="sxs-lookup"><span data-stu-id="1ba96-172">Deploy hello template using click-to-deploy</span></span>

<span data-ttu-id="1ba96-173">Vous pouvez réutiliser prédéfini Azure Resource Manager modèles tooa téléchargé GitHub espace de stockage géré par Microsoft et la Communauté de toohello ouvert.</span><span class="sxs-lookup"><span data-stu-id="1ba96-173">You can reuse pre-defined Azure Resource Manager templates uploaded tooa GitHub repository maintained by Microsoft and open toohello community.</span></span> <span data-ttu-id="1ba96-174">Ces modèles peuvent être déployées directement GitHub, ou téléchargé et modifié toofit à vos besoins.</span><span class="sxs-lookup"><span data-stu-id="1ba96-174">These templates can be deployed straight out of GitHub, or downloaded and modified toofit your needs.</span></span> <span data-ttu-id="1ba96-175">toodeploy un modèle qui crée un réseau virtuel avec deux sous-réseaux, hello complète comme suit :</span><span class="sxs-lookup"><span data-stu-id="1ba96-175">toodeploy a template that creates a VNet with two subnets, complete hello following steps:</span></span>

1. <span data-ttu-id="1ba96-176">À partir d’un navigateur, accédez trop[https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="1ba96-176">From a browser, navigate too[https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span></span>
2. <span data-ttu-id="1ba96-177">Faites défiler la liste hello des modèles et cliquez sur **101-réseau virtuel-deux sous-réseaux**.</span><span class="sxs-lookup"><span data-stu-id="1ba96-177">Scroll down hello list of templates, and click **101-vnet-two-subnets**.</span></span> <span data-ttu-id="1ba96-178">Vérifiez hello **README.md** de fichiers, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="1ba96-178">Check hello **README.md** file, as shown below.</span></span>

    ![Fichier READEME.md dans GitHub](./media/virtual-networks-create-vnet-arm-template-click-include/figure1.png)

3. <span data-ttu-id="1ba96-180">Cliquez sur **déployer tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="1ba96-180">Click **Deploy tooAzure**.</span></span> <span data-ttu-id="1ba96-181">Si nécessaire, entrez vos informations d’identification Azure.</span><span class="sxs-lookup"><span data-stu-id="1ba96-181">If necessary, enter your Azure login credentials.</span></span> 
4. <span data-ttu-id="1ba96-182">Bonjour **paramètres** panneau, entrez les valeurs hello vous souhaitez toouse toocreate votre nouveau réseau virtuel, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="1ba96-182">In hello **Parameters** blade, enter hello values you want toouse toocreate your new VNet, and then click **OK**.</span></span> <span data-ttu-id="1ba96-183">Hello figure ci-dessous illustre les valeurs hello pour le scénario de hello :</span><span class="sxs-lookup"><span data-stu-id="1ba96-183">hello following figure shows hello values for hello scenario:</span></span>
   
    ![Paramètres de modèle ARM](./media/virtual-networks-create-vnet-arm-template-click-include/figure2.png)

5. <span data-ttu-id="1ba96-185">Cliquez sur **groupe de ressources** et sélectionnez hello virtuel à un tooadd de groupe de ressources, ou cliquez sur **nouvel** tooadd hello réseau virtuel tooa nouveau groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="1ba96-185">Click **Resource group** and select a resource group tooadd hello VNet to, or click **Create new** tooadd hello VNet tooa new resource group.</span></span> <span data-ttu-id="1ba96-186">Hello figure suivante montre les ressources hello paramètres de groupe pour un groupe de ressources appelé **TestRG**:</span><span class="sxs-lookup"><span data-stu-id="1ba96-186">hello following figure shows hello resource group settings for a new resource group called **TestRG**:</span></span>

    ![Groupe de ressources](./media/virtual-networks-create-vnet-arm-template-click-include/figure3.png)

6. <span data-ttu-id="1ba96-188">Si nécessaire, modifiez hello **abonnement** et **emplacement** paramètres pour votre réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="1ba96-188">If necessary, change hello **Subscription** and **Location** settings for your VNet.</span></span>
7. <span data-ttu-id="1ba96-189">Si vous ne souhaitez pas toosee hello réseau virtuel sous forme de vignette Bonjour **tableau d’accueil**, désactiver **tooStartboard du code confidentiel**.</span><span class="sxs-lookup"><span data-stu-id="1ba96-189">If you do not want toosee hello VNet as a tile in hello **Startboard**, disable **Pin tooStartboard**.</span></span>
8. <span data-ttu-id="1ba96-190">Cliquez sur **juridiques**, lisez les termes du contrat de hello, puis cliquez sur **acheter** tooagree.</span><span class="sxs-lookup"><span data-stu-id="1ba96-190">Click **Legal terms**, read hello terms, and click **Buy** tooagree.</span></span> 
9. <span data-ttu-id="1ba96-191">Cliquez sur **créer** toocreate hello réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="1ba96-191">Click **Create** toocreate hello VNet.</span></span>
   
    ![Mosaïque d’envoi d’un déploiement dans le portail en version préliminaire](./media/virtual-networks-create-vnet-arm-template-click-include/figure4.png)

10. <span data-ttu-id="1ba96-193">Une fois le déploiement de hello, Bonjour Azure portal cliquez sur **davantage de services**, type *réseaux virtuels* dans la zone de filtre hello qui s’affiche, puis cliquez sur Panneau de réseaux de virtuel réseaux toosee hello virtuel.</span><span class="sxs-lookup"><span data-stu-id="1ba96-193">Once hello deployment is complete, in hello Azure portal click **More services**, type *virtual networks* in hello filter box that appears, then click Virtual networks toosee hello Virtual networks blade.</span></span> <span data-ttu-id="1ba96-194">Dans le panneau de hello, cliquez sur *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="1ba96-194">In hello blade, click *TestVNet*.</span></span> <span data-ttu-id="1ba96-195">Bonjour *TestVNet* panneau, cliquez sur **sous-réseaux** toosee des sous-réseaux hello créé, comme indiqué dans hello illustration suivante :</span><span class="sxs-lookup"><span data-stu-id="1ba96-195">In hello *TestVNet* blade, click **Subnets** toosee hello created subnets, as shown in hello following picture:</span></span>
    
     ![Créer un réseau virtuel dans le portail en version préliminaire](./media/virtual-networks-create-vnet-arm-template-click-include/figure5.png)

## <a name="next-steps"></a><span data-ttu-id="1ba96-197">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1ba96-197">Next steps</span></span>

<span data-ttu-id="1ba96-198">Découvrez comment tooconnect :</span><span class="sxs-lookup"><span data-stu-id="1ba96-198">Learn how tooconnect:</span></span>

- <span data-ttu-id="1ba96-199">Un réseau virtuel tooa de machine virtuelle (VM) par la lecture de hello [créer une machine virtuelle Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md) ou [créer un VM Linux](../virtual-machines/linux/quick-create-portal.md) articles.</span><span class="sxs-lookup"><span data-stu-id="1ba96-199">A virtual machine (VM) tooa virtual network by reading hello [Create a Windows VM](../virtual-machines/virtual-machines-windows-hero-tutorial.md) or [Create a Linux VM](../virtual-machines/linux/quick-create-portal.md) articles.</span></span> <span data-ttu-id="1ba96-200">Au lieu de créer un réseau virtuel et un sous-réseau dans les étapes de hello d’articles de hello, vous pouvez sélectionner un réseau virtuel existant et le sous-réseau tooconnect une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="1ba96-200">Instead of creating a VNet and subnet in hello steps of hello articles, you can select an existing VNet and subnet tooconnect a VM to.</span></span>
- <span data-ttu-id="1ba96-201">Hello des réseaux virtuels tooother de réseau virtuel en lisant hello [connecter des réseaux virtuels](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="1ba96-201">hello virtual network tooother virtual networks by reading hello [Connect VNets](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md) article.</span></span>
- <span data-ttu-id="1ba96-202">Hello réseau virtuel tooan réseau local à l’aide d’un réseau privé virtuel (VPN) site à site ou un circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="1ba96-202">hello virtual network tooan on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span></span> <span data-ttu-id="1ba96-203">Découvrez comment en lecture hello [connecter un réseau local de tooan de réseau virtuel à l’aide d’un VPN de site à site](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) et [lier un circuit ExpressRoute de tooan réseau virtuel](../expressroute/expressroute-howto-linkvnet-arm.md) articles.</span><span class="sxs-lookup"><span data-stu-id="1ba96-203">Learn how by reading hello [Connect a VNet tooan on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet tooan ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-arm.md) articles.</span></span>
