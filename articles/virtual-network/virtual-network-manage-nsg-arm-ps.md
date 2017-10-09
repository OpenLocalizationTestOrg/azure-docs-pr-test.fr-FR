---
title: "aaaManage réseau des groupes de sécurité - Azure PowerShell | Documents Microsoft"
description: "Découvrez comment toomanage réseau des groupes de sécurité à l’aide de PowerShell."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3706ce6c-d9ae-46cb-a048-f0a4e84dc5cc
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/14/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 930fe5e0827896ad67b24d84e41a5d3f898ba838
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-network-security-groups-using-powershell"></a><span data-ttu-id="a4fc2-103">Gérer des groupes de sécurité réseau à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="a4fc2-103">Manage network security groups using PowerShell</span></span>

[!INCLUDE [virtual-network-manage-arm-selectors-include.md](../../includes/virtual-network-manage-nsg-arm-selectors-include.md)]

[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="a4fc2-104">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="a4fc2-104">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="a4fc2-105">Cet article décrit à l’aide du modèle de déploiement Resource Manager hello, qui recommandées par Microsoft pour la plupart des déploiements de nouveau au lieu du modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="a4fc2-105">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>
>

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="retrieve-information"></a><span data-ttu-id="a4fc2-106">Récupérer des informations</span><span class="sxs-lookup"><span data-stu-id="a4fc2-106">Retrieve Information</span></span>
<span data-ttu-id="a4fc2-107">Vous pouvez afficher vos groupes de sécurité réseau existants, récupérer des règles pour un groupe de sécurité réseau existant et découvrir quelles sont les ressources associées à un groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="a4fc2-107">You can view your existing NSGs, retrieve rules for an existing NSG, and find out what resources an NSG is associated to.</span></span>

### <a name="view-existing-nsgs"></a><span data-ttu-id="a4fc2-108">Afficher les groupes de sécurité réseau existants</span><span class="sxs-lookup"><span data-stu-id="a4fc2-108">View existing NSGs</span></span>
<span data-ttu-id="a4fc2-109">tooview tous les groupes existants de sécurité réseau dans un abonnement, exécutez hello `Get-AzureRmNetworkSecurityGroup` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="a4fc2-109">tooview all existing NSGs in a subscription, run hello `Get-AzureRmNetworkSecurityGroup` cmdlet.</span></span>

<span data-ttu-id="a4fc2-110">Résultat attendu :</span><span class="sxs-lookup"><span data-stu-id="a4fc2-110">Expected result:</span></span>

    Name                 : NSG-BackEnd
    ResourceGroupName    : RG-NSG
    Location             : westus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-BackEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 :                            
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

    Name                 : NSG-FrontEnd
    ResourceGroupName    : RG-NSG
    Location             : eastus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/NRP-RG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 : 
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

    Name                 : WEB1
    ResourceGroupName    : RG101
    Location             : eastus2
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/RG101/providers/M
                           icrosoft.Network/networkSecurityGroups/WEB1
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 : 
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]


<span data-ttu-id="a4fc2-111">liste de hello tooview de groupes de sécurité réseau dans un groupe de ressources spécifique, exécutez hello `Get-AzureRmNetworkSecurityGroup` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="a4fc2-111">tooview hello list of NSGs in a specific resource group, run hello `Get-AzureRmNetworkSecurityGroup` cmdlet.</span></span>

<span data-ttu-id="a4fc2-112">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="a4fc2-112">Expected output:</span></span>

    Name                 : NSG-BackEnd
    ResourceGroupName    : RG-NSG
    Location             : westus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-BackEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 :                            
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

    Name                 : NSG-FrontEnd
    ResourceGroupName    : RG-NSG
    Location             : eastus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/NRP-RG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 : 
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

### <a name="list-all-rules-for-an-nsg"></a><span data-ttu-id="a4fc2-113">Répertorier toutes les règles pour un groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="a4fc2-113">List all rules for an NSG</span></span>
<span data-ttu-id="a4fc2-114">règles de hello tooview d’un groupe de sécurité réseau nommé **NSG-FrontEnd**, entrez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="a4fc2-114">tooview hello rules of an NSG named **NSG-FrontEnd**, enter hello following command:</span></span>

```powershell
Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd | Select SecurityRules -ExpandProperty SecurityRules
```

<span data-ttu-id="a4fc2-115">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="a4fc2-115">Expected output:</span></span>

    Name                     : rdp-rule
    Id                       : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/rdp-rule
    Etag                     : W/"[Id]"
    ProvisioningState        : Succeeded
    Description              : Allow RDP
    Protocol                 : Tcp
    SourcePortRange          : *
    DestinationPortRange     : 3389
    SourceAddressPrefix      : Internet
    DestinationAddressPrefix : *
    Access                   : Allow
    Priority                 : 100
    Direction                : Inbound

    Name                     : web-rule
    Id                       : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/web-rule
    Etag                     : W/"[Id]"
    ProvisioningState        : Succeeded
    Description              : Allow HTTP
    Protocol                 : Tcp
    SourcePortRange          : *
    DestinationPortRange     : 80
    SourceAddressPrefix      : Internet
    DestinationAddressPrefix : *
    Access                   : Allow
    Priority                 : 101
    Direction                : Inbound

> [!NOTE]
> <span data-ttu-id="a4fc2-116">Vous pouvez également utiliser `Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name "NSG-FrontEnd" | Select DefaultSecurityRules -ExpandProperty DefaultSecurityRules` les règles par défaut hello toolist hello **NSG-FrontEnd** groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="a4fc2-116">You can also use `Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name "NSG-FrontEnd" | Select DefaultSecurityRules -ExpandProperty DefaultSecurityRules` toolist hello default rules from hello **NSG-FrontEnd** NSG.</span></span>
> 

### <a name="view-nsgs-associations"></a><span data-ttu-id="a4fc2-117">Afficher les associations de groupes de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="a4fc2-117">View NSGs associations</span></span>
<span data-ttu-id="a4fc2-118">tooview hello de quelles ressources **NSG-FrontEnd** NSG est associez, hello exécution de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="a4fc2-118">tooview what resources hello **NSG-FrontEnd** NSG is associate with, run hello following command:</span></span>

```powershell
Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
```

<span data-ttu-id="a4fc2-119">Recherchez hello **NetworkInterfaces** et **sous-réseaux** propriétés comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="a4fc2-119">Look for hello **NetworkInterfaces** and **Subnets** properties as shown below:</span></span>

    NetworkInterfaces    : []
    Subnets              : [
                             {
                               "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                               "IpConfigurations": []
                             }
                           ]

<span data-ttu-id="a4fc2-120">Dans l’exemple précédent de hello, hello groupe de sécurité réseau n’est pas associé tooany les interfaces réseau (NIC) ; Il s’agit de sous-réseau associé tooa nommé **frontal**.</span><span class="sxs-lookup"><span data-stu-id="a4fc2-120">In hello previous example, hello NSG is not associated tooany network interfaces (NICs); it is associated tooa subnet named **FrontEnd**.</span></span>

## <a name="manage-rules"></a><span data-ttu-id="a4fc2-121">Gérer les règles</span><span class="sxs-lookup"><span data-stu-id="a4fc2-121">Manage rules</span></span>
<span data-ttu-id="a4fc2-122">Vous pouvez ajouter tooan règles existants du groupe de sécurité réseau, modifier les règles existantes et supprimer des règles.</span><span class="sxs-lookup"><span data-stu-id="a4fc2-122">You can add rules tooan existing NSG, edit existing rules, and remove rules.</span></span>

### <a name="add-a-rule"></a><span data-ttu-id="a4fc2-123">Ajouter une règle</span><span class="sxs-lookup"><span data-stu-id="a4fc2-123">Add a rule</span></span>
<span data-ttu-id="a4fc2-124">tooadd une règle autorisant **entrant** trafic tooport **443** à partir de n’importe quel ordinateur toohello **NSG-FrontEnd** NSG, hello complète comme suit :</span><span class="sxs-lookup"><span data-stu-id="a4fc2-124">tooadd a rule allowing **inbound** traffic tooport **443** from any machine toohello **NSG-FrontEnd** NSG, complete hello following steps:</span></span>

1. <span data-ttu-id="a4fc2-125">Exécutez hello suivant commande tooretrieve hello existants du groupe de sécurité réseau et les stocker dans une variable :</span><span class="sxs-lookup"><span data-stu-id="a4fc2-125">Run hello following command tooretrieve hello existing NSG and store it in a variable:</span></span>

    ```powershell   
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="a4fc2-126">Exécutez hello suivant commande tooadd un toohello règle groupe de sécurité réseau :</span><span class="sxs-lookup"><span data-stu-id="a4fc2-126">Run hello following command tooadd a rule toohello NSG:</span></span>

    ```powershell
    Add-AzureRmNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg `
    -Name https-rule `
    -Description "Allow HTTPS" `
    -Access Allow `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 102 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 443
    ```

3. <span data-ttu-id="a4fc2-127">toosave hello apportées toohello NSG, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="a4fc2-127">toosave hello changes made toohello NSG, run hello following command:</span></span>

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```
    <span data-ttu-id="a4fc2-128">Sortie attendue indiquant hello uniquement les règles de sécurité :</span><span class="sxs-lookup"><span data-stu-id="a4fc2-128">Expected output showing only hello security rules:</span></span>
   
        Name                 : NSG-FrontEnd
        ...
        SecurityRules        : [
                                 {
                                   "Name": "rdp-rule",
                                   ...
                                 },
                                 {
                                   "Name": "web-rule",
                                   ...
                                 },
                                 {
                                   "Name": "https-rule",
                                   "Etag": "W/\"[Id]\"",
                                   "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/https-rule",
                                   "Description": "Allow HTTPS",
                                   "Protocol": "Tcp",
                                   "SourcePortRange": "*",
                                   "DestinationPortRange": "443",
                                   "SourceAddressPrefix": "*",
                                   "DestinationAddressPrefix": "*",
                                   "Access": "Allow",
                                   "Priority": 102,
                                   "Direction": "Inbound",
                                   "ProvisioningState": "Succeeded"
                                 }
                               ]

### <a name="change-a-rule"></a><span data-ttu-id="a4fc2-129">Modifier une règle</span><span class="sxs-lookup"><span data-stu-id="a4fc2-129">Change a rule</span></span>
<span data-ttu-id="a4fc2-130">règle de hello toochange créé ci-dessus tooallow le trafic entrant provenance hello **Internet** uniquement, suivez les étapes de hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="a4fc2-130">toochange hello rule created above tooallow inbound traffic from hello **Internet** only, follow hello steps below.</span></span>

1. <span data-ttu-id="a4fc2-131">Exécutez hello suivant commande tooretrieve hello existants du groupe de sécurité réseau et les stocker dans une variable :</span><span class="sxs-lookup"><span data-stu-id="a4fc2-131">Run hello following command tooretrieve hello existing NSG and store it in a variable:</span></span>

    ```powershell 
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="a4fc2-132">Exécutez hello commande avec les paramètres de la nouvelle règle hello suivante :</span><span class="sxs-lookup"><span data-stu-id="a4fc2-132">Run hello following command with hello new rule settings:</span></span>

    ```powershell
    Set-AzureRmNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg `
    -Name https-rule `
    -Description "Allow HTTPS" `
    -Access Allow `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 102 `
    -SourceAddressPrefix Internet `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 443
    ```

3. <span data-ttu-id="a4fc2-133">toosave hello apportées toohello NSG, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="a4fc2-133">toosave hello changes made toohello NSG, run hello following command:</span></span>

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```

    <span data-ttu-id="a4fc2-134">Sortie attendue indiquant hello uniquement les règles de sécurité :</span><span class="sxs-lookup"><span data-stu-id="a4fc2-134">Expected output showing only hello security rules:</span></span>
   
        Name                 : NSG-FrontEnd
        ...
        SecurityRules        : [
                                 {
                                   "Name": "rdp-rule",
                                   ...
                                 },
                                 {
                                   "Name": "web-rule",
                                   ...
                                 },
                                 {
                                   "Name": "https-rule",
                                   "Etag": "W/\"[Id]\"",
                                   "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/https-rule",
                                   "Description": "Allow HTTPS",
                                   "Protocol": "Tcp",
                                   "SourcePortRange": "*",
                                   "DestinationPortRange": "443",
                                   "SourceAddressPrefix": "Internet",
                                   "DestinationAddressPrefix": "*",
                                   "Access": "Allow",
                                   "Priority": 102,
                                   "Direction": "Inbound",
                                   "ProvisioningState": "Succeeded"
                                 }
                               ]

### <a name="delete-a-rule"></a><span data-ttu-id="a4fc2-135">Supprimer une règle</span><span class="sxs-lookup"><span data-stu-id="a4fc2-135">Delete a rule</span></span>
1. <span data-ttu-id="a4fc2-136">Exécutez hello suivant commande tooretrieve hello existants du groupe de sécurité réseau et les stocker dans une variable :</span><span class="sxs-lookup"><span data-stu-id="a4fc2-136">Run hello following command tooretrieve hello existing NSG and store it in a variable:</span></span>

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="a4fc2-137">Exécutez hello suivant les règles de commande tooremove hello dans hello groupe de sécurité réseau :</span><span class="sxs-lookup"><span data-stu-id="a4fc2-137">Run hello following command tooremove hello rule from hello NSG:</span></span>

    ```powershell
    Remove-AzureRmNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg -Name https-rule
    ```

3. <span data-ttu-id="a4fc2-138">Enregistrer hello apportés toohello groupe de sécurité réseau, en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="a4fc2-138">Save hello changes made toohello NSG, by running hello following command:</span></span>

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```

    <span data-ttu-id="a4fc2-139">Sortie attendue indiquant hello uniquement les règles de sécurité, notez hello **https-règle** n’est plus répertorié :</span><span class="sxs-lookup"><span data-stu-id="a4fc2-139">Expected output showing only hello security rules, notice hello **https-rule** is no longer listed:</span></span>
   
        Name                 : NSG-FrontEnd
        ...
        SecurityRules        : [
                                 {
                                   "Name": "rdp-rule",
                                   ...
                                 },
                                 {
                                   "Name": "web-rule",
                                   ...
                                 }
                               ]

## <a name="manage-associations"></a><span data-ttu-id="a4fc2-140">Gérer les associations</span><span class="sxs-lookup"><span data-stu-id="a4fc2-140">Manage associations</span></span>
<span data-ttu-id="a4fc2-141">Vous pouvez associer un toosubnets du groupe de sécurité réseau et les cartes réseau.</span><span class="sxs-lookup"><span data-stu-id="a4fc2-141">You can associate an NSG toosubnets and NICs.</span></span> <span data-ttu-id="a4fc2-142">Vous pouvez également dissocier un groupe de sécurité réseau de n’importe quelle ressource à laquelle il est associé.</span><span class="sxs-lookup"><span data-stu-id="a4fc2-142">You can also dissociate an NSG from any resource it's associated to.</span></span>

### <a name="associate-an-nsg-tooa-nic"></a><span data-ttu-id="a4fc2-143">Associer un groupe de sécurité réseau de tooa carte réseau</span><span class="sxs-lookup"><span data-stu-id="a4fc2-143">Associate an NSG tooa NIC</span></span>
<span data-ttu-id="a4fc2-144">tooassociate hello **NSG-FrontEnd** NSG toohello **TestNICWeb1** NIC, hello complète comme suit :</span><span class="sxs-lookup"><span data-stu-id="a4fc2-144">tooassociate hello **NSG-FrontEnd** NSG toohello **TestNICWeb1** NIC, complete hello following steps:</span></span>

1. <span data-ttu-id="a4fc2-145">Exécutez hello suivant commande tooretrieve hello existants du groupe de sécurité réseau et les stocker dans une variable :</span><span class="sxs-lookup"><span data-stu-id="a4fc2-145">Run hello following command tooretrieve hello existing NSG and store it in a variable:</span></span>

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="a4fc2-146">Exécutez hello suivant commande tooretrieve hello existant de carte réseau et le stocker dans une variable :</span><span class="sxs-lookup"><span data-stu-id="a4fc2-146">Run hello following command tooretrieve hello existing NIC and store it in a variable:</span></span>

    ```powershell
    $nic = Get-AzureRmNetworkInterface -ResourceGroupName RG-NSG -Name TestNICWeb1
    ```

3. <span data-ttu-id="a4fc2-147">Ensemble hello **sécurité réseau** propriété Hello **NIC** valeur variable toohello hello **NSG** variable, en entrant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="a4fc2-147">Set hello **NetworkSecurityGroup** property of hello **NIC** variable toohello value of hello **NSG** variable, by entering hello following command:</span></span>

    ```powershell
    $nic.NetworkSecurityGroup = $nsg
    ```

4. <span data-ttu-id="a4fc2-148">toosave hello apportées toohello carte réseau, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="a4fc2-148">toosave hello changes made toohello NIC, run hello following command:</span></span>

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```
   
    <span data-ttu-id="a4fc2-149">Hello uniquement de sortie attendue montrant **sécurité réseau** propriété :</span><span class="sxs-lookup"><span data-stu-id="a4fc2-149">Expected output showing only hello **NetworkSecurityGroup** property:</span></span>
   
        NetworkSecurityGroup : {
                                 "SecurityRules": [],
                                 "DefaultSecurityRules": [],
                                 "NetworkInterfaces": [],
                                 "Subnets": [],
                                 "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                               }

### <a name="dissociate-an-nsg-from-a-nic"></a><span data-ttu-id="a4fc2-150">Dissocier un groupe de sécurité réseau d’une carte réseau</span><span class="sxs-lookup"><span data-stu-id="a4fc2-150">Dissociate an NSG from a NIC</span></span>
<span data-ttu-id="a4fc2-151">toodissociate hello **NSG-FrontEnd** groupe de sécurité réseau à partir de hello **TestNICWeb1** NIC, hello complète comme suit :</span><span class="sxs-lookup"><span data-stu-id="a4fc2-151">toodissociate hello **NSG-FrontEnd** NSG from hello **TestNICWeb1** NIC, complete hello following steps:</span></span>

1. <span data-ttu-id="a4fc2-152">Exécutez hello suivant commande tooretrieve hello existant de carte réseau et le stocker dans une variable :</span><span class="sxs-lookup"><span data-stu-id="a4fc2-152">Run hello following command tooretrieve hello existing NIC and store it in a variable:</span></span>

    ```powershell
    $nic = Get-AzureRmNetworkInterface -ResourceGroupName RG-NSG -Name TestNICWeb1
    ```

2. <span data-ttu-id="a4fc2-153">Ensemble hello **sécurité réseau** propriété Hello **NIC** variable trop**$null** en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="a4fc2-153">Set hello **NetworkSecurityGroup** property of hello **NIC** variable too**$null** by running hello following command:</span></span>

    ```powershell
    $nic.NetworkSecurityGroup = $null
    ```

3. <span data-ttu-id="a4fc2-154">toosave hello apportées toohello carte réseau, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="a4fc2-154">toosave hello changes made toohello NIC, run hello following command:</span></span>

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```
   
    <span data-ttu-id="a4fc2-155">Hello uniquement de sortie attendue montrant **sécurité réseau** propriété :</span><span class="sxs-lookup"><span data-stu-id="a4fc2-155">Expected output showing only hello **NetworkSecurityGroup** property:</span></span>
   
        NetworkSecurityGroup : null

### <a name="dissociate-an-nsg-from-a-subnet"></a><span data-ttu-id="a4fc2-156">Dissocier un groupe de sécurité réseau d’un sous-réseau</span><span class="sxs-lookup"><span data-stu-id="a4fc2-156">Dissociate an NSG from a subnet</span></span>
<span data-ttu-id="a4fc2-157">toodissociate hello **NSG-FrontEnd** groupe de sécurité réseau à partir de hello **frontal** sous-réseau, hello complète comme suit :</span><span class="sxs-lookup"><span data-stu-id="a4fc2-157">toodissociate hello **NSG-FrontEnd** NSG from hello **FrontEnd** subnet, complete hello following steps:</span></span>

1. <span data-ttu-id="a4fc2-158">Exécutez hello suivant commande tooretrieve hello existant du réseau virtuel et stockez-le dans une variable :</span><span class="sxs-lookup"><span data-stu-id="a4fc2-158">Run hello following command tooretrieve hello existing VNet and store it in a variable:</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName RG-NSG -Name TestVNet
    ```

2. <span data-ttu-id="a4fc2-159">Exécution hello après la commande tooretrieve hello **frontal** sous-réseau et les stocker dans une variable :</span><span class="sxs-lookup"><span data-stu-id="a4fc2-159">Run hello following command tooretrieve hello **FrontEnd** subnet and store it in a variable:</span></span>

    ```powershell
    $subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd
    ```
 
3. <span data-ttu-id="a4fc2-160">Ensemble hello **sécurité réseau** propriété Hello **sous-réseau** variable trop**$null** en entrant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="a4fc2-160">Set hello **NetworkSecurityGroup** property of hello **subnet** variable too**$null** by entering hello following command:</span></span>

    ```powershell
    $subnet.NetworkSecurityGroup = $null
    ```

4. <span data-ttu-id="a4fc2-161">toosave hello apportées toohello sous-réseau, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="a4fc2-161">toosave hello changes made toohello subnet, run hello following command:</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="a4fc2-162">Sortie attendue affiche uniquement les propriétés de hello du hello **frontal** sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="a4fc2-162">Expected output showing only hello properties of hello **FrontEnd** subnet.</span></span> <span data-ttu-id="a4fc2-163">Notez qu’il n’y a pas de propriété pour **NetworkSecurityGroup**:</span><span class="sxs-lookup"><span data-stu-id="a4fc2-163">Notice there isn't a property for **NetworkSecurityGroup**:</span></span>
   
            ...
            Subnets           : [
                                  {
                                    "Name": "FrontEnd",
                                    "Etag": "W/\"[Id]\"",
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                    "AddressPrefix": "192.168.1.0/24",
                                    "IpConfigurations": [
                                      {
                                        "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb2/ipConfigurations/ipconfig1"
                                      },
                                      {
                                        "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1/ipConfigurations/ipconfig1"
                                      }
                                    ],
                                    "ProvisioningState": "Succeeded"
                                  },
                                    ...
                                ]

### <a name="associate-an-nsg-tooa-subnet"></a><span data-ttu-id="a4fc2-164">Associez un sous-réseau de tooa du groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="a4fc2-164">Associate an NSG tooa subnet</span></span>
<span data-ttu-id="a4fc2-165">tooassociate hello **NSG-FrontEnd** NSG toohello **FronEnd** à nouveau le sous-réseau, hello complète comme suit :</span><span class="sxs-lookup"><span data-stu-id="a4fc2-165">tooassociate hello **NSG-FrontEnd** NSG toohello **FronEnd** subnet again, complete hello following steps:</span></span>

1. <span data-ttu-id="a4fc2-166">Exécutez hello suivant commande tooretrieve hello existant du réseau virtuel et stockez-le dans une variable :</span><span class="sxs-lookup"><span data-stu-id="a4fc2-166">Run hello following command tooretrieve hello existing VNet and store it in a variable:</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName RG-NSG -Name TestVNet
    ```

2. <span data-ttu-id="a4fc2-167">Exécution hello après la commande tooretrieve hello **frontal** sous-réseau et les stocker dans une variable :</span><span class="sxs-lookup"><span data-stu-id="a4fc2-167">Run hello following command tooretrieve hello **FrontEnd** subnet and store it in a variable:</span></span>

    ```powershell
    $subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd
    ```
 
3. <span data-ttu-id="a4fc2-168">Exécutez hello suivant commande tooretrieve hello existants du groupe de sécurité réseau et les stocker dans une variable :</span><span class="sxs-lookup"><span data-stu-id="a4fc2-168">Run hello following command tooretrieve hello existing NSG and store it in a variable:</span></span>

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

4. <span data-ttu-id="a4fc2-169">Ensemble hello **sécurité réseau** propriété Hello **sous-réseau** variable trop**$null** en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="a4fc2-169">Set hello **NetworkSecurityGroup** property of hello **subnet** variable too**$null** by running hello following command:</span></span>

    ```powershell
    $subnet.NetworkSecurityGroup = $nsg
    ```

5. <span data-ttu-id="a4fc2-170">toosave hello apportées toohello sous-réseau, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="a4fc2-170">toosave hello changes made toohello subnet, run hello following command:</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="a4fc2-171">Hello uniquement de sortie attendue montrant **sécurité réseau** propriété Hello **frontal** sous-réseau :</span><span class="sxs-lookup"><span data-stu-id="a4fc2-171">Expected output showing only hello **NetworkSecurityGroup** property of hello **FrontEnd** subnet:</span></span>
   
        ...
        "NetworkSecurityGroup": {
                                  "SecurityRules": [],
                                  "DefaultSecurityRules": [],
                                  "NetworkInterfaces": [],
                                  "Subnets": [],
                                  "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                                }
        ...

## <a name="delete-an-nsg"></a><span data-ttu-id="a4fc2-172">Suppression d'un groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="a4fc2-172">Delete an NSG</span></span>
<span data-ttu-id="a4fc2-173">Vous ne pouvez supprimer un groupe de sécurité réseau si elle n’est pas associé à tooany ressource.</span><span class="sxs-lookup"><span data-stu-id="a4fc2-173">You can only delete an NSG if it's not associated tooany resource.</span></span> <span data-ttu-id="a4fc2-174">toodelete un groupe de sécurité réseau, suivez les étapes de hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="a4fc2-174">toodelete an NSG, follow hello steps below.</span></span>

1. <span data-ttu-id="a4fc2-175">ressources de hello toocheck associés tooan NSG, exécutez hello `azure network nsg show` comme indiqué dans [associations de groupes de sécurité réseau vue](#View-NSGs-associations).</span><span class="sxs-lookup"><span data-stu-id="a4fc2-175">toocheck hello resources associated tooan NSG, run hello `azure network nsg show` as shown in [View NSGs associations](#View-NSGs-associations).</span></span>
2. <span data-ttu-id="a4fc2-176">Si hello NSG est associé tooany cartes réseau, exécutez hello `azure network nic set` comme indiqué dans [dissocier un groupe de sécurité réseau à partir d’une carte réseau](#Dissociate-an-NSG-from-a-NIC) pour chaque carte réseau.</span><span class="sxs-lookup"><span data-stu-id="a4fc2-176">If hello NSG is associated tooany NICs, run hello `azure network nic set` as shown in [Dissociate an NSG from a NIC](#Dissociate-an-NSG-from-a-NIC) for each NIC.</span></span> 
3. <span data-ttu-id="a4fc2-177">Si hello NSG est associé tooany sous-réseau, exécutez hello `azure network vnet subnet set` comme indiqué dans [dissocier un groupe de sécurité réseau à partir d’un sous-réseau](#Dissociate-an-NSG-from-a-subnet) pour chaque sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="a4fc2-177">If hello NSG is associated tooany subnet, run hello `azure network vnet subnet set` as shown in [Dissociate an NSG from a subnet](#Dissociate-an-NSG-from-a-subnet) for each subnet.</span></span>
4. <span data-ttu-id="a4fc2-178">toodelete hello NSG, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="a4fc2-178">toodelete hello NSG, run hello following command:</span></span>

    ```powershell
    Remove-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd -Force
    ```
   
   > [!NOTE]
   > <span data-ttu-id="a4fc2-179">Hello `-Force` paramètre garantit que vous n’avez pas besoin de tooconfirm la suppression hello.</span><span class="sxs-lookup"><span data-stu-id="a4fc2-179">hello `-Force` parameter ensures you don't need tooconfirm hello deletion.</span></span>
   > 

## <a name="next-steps"></a><span data-ttu-id="a4fc2-180">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a4fc2-180">Next steps</span></span>
* <span data-ttu-id="a4fc2-181">[Activez la journalisation](virtual-network-nsg-manage-log.md) des groupes de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="a4fc2-181">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>

