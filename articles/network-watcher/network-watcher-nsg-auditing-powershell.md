---
title: "Automatiser l’audit NSG avec la vue Groupe de sécurité réseau Network Watcher | Microsoft Docs"
description: "Cette page fournit des instructions sur configuration de l’audit d’un groupe de sécurité réseau"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 78a01bcf-74fe-402a-9812-285f3501f877
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: a91da330e677c85f16f6f4e506613576b6507d7c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="automate-nsg-auditing-with-azure-network-watcher-security-group-view"></a><span data-ttu-id="f53b6-103">Automatiser l’audit NSG avec la vue de groupe de sécurité réseau Network Watcher</span><span class="sxs-lookup"><span data-stu-id="f53b6-103">Automate NSG auditing with Azure Network Watcher Security group view</span></span>

<span data-ttu-id="f53b6-104">Les clients sont souvent confrontés au défi de la vérification des mesures de sécurité de leur infrastructure.</span><span class="sxs-lookup"><span data-stu-id="f53b6-104">Customers are often faced with the challenge of verifying the security posture of their infrastructure.</span></span> <span data-ttu-id="f53b6-105">Ce défi n’est pas différent pour leurs machines virtuelles dans Azure.</span><span class="sxs-lookup"><span data-stu-id="f53b6-105">This challenge is no different for their VMs in Azure.</span></span> <span data-ttu-id="f53b6-106">Il est important de disposer d’un profil de sécurité similaire en fonction des règles de groupe de sécurité réseau (NSG) appliquées.</span><span class="sxs-lookup"><span data-stu-id="f53b6-106">It is important to have a similar security profile based on the Network Security Group (NSG) rules applied.</span></span> <span data-ttu-id="f53b6-107">Grâce à la vue Groupe de sécurité, vous pouvez désormais obtenir la liste des règles appliquées à une machine virtuelle au sein d’un NSG.</span><span class="sxs-lookup"><span data-stu-id="f53b6-107">Using the Security Group View, you can now get the list of rules applied to a VM within an NSG.</span></span> <span data-ttu-id="f53b6-108">Vous pouvez définir un profil de sécurité NSG final, ouvrir la vue Groupe de sécurité selon une fréquence hebdomadaire, puis comparer la sortie au profil final et créer un rapport.</span><span class="sxs-lookup"><span data-stu-id="f53b6-108">You can define a golden NSG security profile and initiate Security Group View on a weekly cadence and compare the output to the golden profile and create a report.</span></span> <span data-ttu-id="f53b6-109">Vous pouvez ainsi identifier facilement toutes les machines virtuelles qui ne sont pas conformes au profil de sécurité établi.</span><span class="sxs-lookup"><span data-stu-id="f53b6-109">This way you can identify with ease all the VMs that do not conform to the prescribed security profile.</span></span>

<span data-ttu-id="f53b6-110">Si vous n’êtes pas familiarisé avec les groupes de sécurité réseau, consultez la [vue d’ensemble de la sécurité réseau](../virtual-network/virtual-networks-nsg.md)</span><span class="sxs-lookup"><span data-stu-id="f53b6-110">If you are unfamiliar with Network Security Groups, visit [Network Security Overview](../virtual-network/virtual-networks-nsg.md)</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="f53b6-111">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="f53b6-111">Before you begin</span></span>

<span data-ttu-id="f53b6-112">Dans ce scénario, vous comparez une base correcte connue avec les résultats de la vue de groupe de sécurité renvoyés pour une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f53b6-112">In this scenario, you compare a known good baseline to the security group view results returned for a virtual machine.</span></span>

<span data-ttu-id="f53b6-113">Ce scénario suppose que vous ayez déjà suivi la procédure décrite dans [Create a Network Watcher (Créer une instance Network Watcher)](network-watcher-create.md) pour créer une instance Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="f53b6-113">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span> <span data-ttu-id="f53b6-114">Ce scénario suppose également qu’un groupe de ressources avec une machine virtuelle valide existe et peut être utilisé.</span><span class="sxs-lookup"><span data-stu-id="f53b6-114">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="f53b6-115">Scénario</span><span class="sxs-lookup"><span data-stu-id="f53b6-115">Scenario</span></span>

<span data-ttu-id="f53b6-116">Le scénario décrit dans cet article obtient la vue de groupe de sécurité pour une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f53b6-116">The scenario covered in this article gets the security group view for a virtual machine.</span></span>

<span data-ttu-id="f53b6-117">Dans ce scénario, vous allez :</span><span class="sxs-lookup"><span data-stu-id="f53b6-117">In this scenario, you will:</span></span>

- <span data-ttu-id="f53b6-118">Récupérer un ensemble de règles correct connu</span><span class="sxs-lookup"><span data-stu-id="f53b6-118">Retrieve a known good rule set</span></span>
- <span data-ttu-id="f53b6-119">Récupérer une machine virtuelle avec l’API REST</span><span class="sxs-lookup"><span data-stu-id="f53b6-119">Retrieve a virtual machine with Rest API</span></span>
- <span data-ttu-id="f53b6-120">Obtenir la vue de groupe de sécurité pour la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="f53b6-120">Get security group view for virtual machine</span></span>
- <span data-ttu-id="f53b6-121">Évaluer la réponse</span><span class="sxs-lookup"><span data-stu-id="f53b6-121">Evaluate Response</span></span>

## <a name="retrieve-rule-set"></a><span data-ttu-id="f53b6-122">Récupérer l’ensemble de règles</span><span class="sxs-lookup"><span data-stu-id="f53b6-122">Retrieve rule set</span></span>

<span data-ttu-id="f53b6-123">La première étape dans cet exemple consiste à utiliser une base existante.</span><span class="sxs-lookup"><span data-stu-id="f53b6-123">The first step in this example is to work with an existing baseline.</span></span> <span data-ttu-id="f53b6-124">L’exemple suivant est un json extrait d’un groupe de sécurité réseau existant à l’aide de l’applet de commande `Get-AzureRmNetworkSecurityGroup` qui est utilisée comme base pour cet exemple.</span><span class="sxs-lookup"><span data-stu-id="f53b6-124">The following example is some json extracted from an existing Network Security Group using the `Get-AzureRmNetworkSecurityGroup` cmdlet that is used as the baseline for this example.</span></span>

```json
[
    {
        "Description":  null,
        "Protocol":  "TCP",
        "SourcePortRange":  "*",
        "DestinationPortRange":  "3389",
        "SourceAddressPrefix":  "*",
        "DestinationAddressPrefix":  "*",
        "Access":  "Allow",
        "Priority":  1000,
        "Direction":  "Inbound",
        "ProvisioningState":  "Succeeded",
        "Name":  "default-allow-rdp",
        "Etag":  "W/\"d8859256-1c4c-4b93-ba7d-73d9bf67c4f1\"",
        "Id":  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/testvm1-nsg/securityRules/default-allow-rdp"
    },
    {
        "Description":  null,
        "Protocol":  "*",
        "SourcePortRange":  "*",
        "DestinationPortRange":  "111",
        "SourceAddressPrefix":  "*",
        "DestinationAddressPrefix":  "*",
        "Access":  "Allow",
        "Priority":  1010,
        "Direction":  "Inbound",
        "ProvisioningState":  "Succeeded",
        "Name":  "MyRuleDoNotDelete",
        "Etag":  "W/\"d8859256-1c4c-4b93-ba7d-73d9bf67c4f1\"",
        "Id":  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/testvm1-nsg/securityRules/MyRuleDoNotDelete"
    },
    {
        "Description":  null,
        "Protocol":  "*",
        "SourcePortRange":  "*",
        "DestinationPortRange":  "112",
        "SourceAddressPrefix":  "*",
        "DestinationAddressPrefix":  "*",
        "Access":  "Allow",
        "Priority":  1020,
        "Direction":  "Inbound",
        "ProvisioningState":  "Succeeded",
        "Name":  "My2ndRuleDoNotDelete",
        "Etag":  "W/\"d8859256-1c4c-4b93-ba7d-73d9bf67c4f1\"",
        "Id":  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/testvm1-nsg/securityRules/My2ndRuleDoNotDelete"
    },
    {
        "Description":  null,
        "Protocol":  "TCP",
        "SourcePortRange":  "*",
        "DestinationPortRange":  "5672",
        "SourceAddressPrefix":  "*",
        "DestinationAddressPrefix":  "*",
        "Access":  "Deny",
        "Priority":  1030,
        "Direction":  "Inbound",
        "ProvisioningState":  "Succeeded",
        "Name":  "ThisRuleNeedsToStay",
        "Etag":  "W/\"d8859256-1c4c-4b93-ba7d-73d9bf67c4f1\"",
        "Id":  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/testvm1-nsg/securityRules/ThisRuleNeedsToStay"
    }
]
```

## <a name="convert-rule-set-to-powershell-objects"></a><span data-ttu-id="f53b6-125">Convertir l’ensemble de règles en objets PowerShell</span><span class="sxs-lookup"><span data-stu-id="f53b6-125">Convert rule set to PowerShell objects</span></span>

<span data-ttu-id="f53b6-126">Dans cette étape, nous lisons un fichier json qui a été créé précédemment avec les règles qui sont censées se trouver sur le groupe de sécurité réseau pour cet exemple.</span><span class="sxs-lookup"><span data-stu-id="f53b6-126">In this step, we are reading a json file that was created earlier with the rules that are expected to be on the Network Security Group for this example.</span></span>

```powershell
$nsgbaserules = Get-Content -Path C:\temp\testvm1-nsg.json | ConvertFrom-Json
```

## <a name="retrieve-network-watcher"></a><span data-ttu-id="f53b6-127">Récupérer Network Watcher</span><span class="sxs-lookup"><span data-stu-id="f53b6-127">Retrieve Network Watcher</span></span>

<span data-ttu-id="f53b6-128">L’étape suivante consiste à récupérer l’instance Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="f53b6-128">The next step is to retrieve the Network Watcher instance.</span></span> <span data-ttu-id="f53b6-129">La variable `$networkWatcher` est transmise à l’applet de commande `AzureRmNetworkWatcherSecurityGroupView`.</span><span class="sxs-lookup"><span data-stu-id="f53b6-129">The `$networkWatcher` variable is passed to the `AzureRmNetworkWatcherSecurityGroupView` cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-vm"></a><span data-ttu-id="f53b6-130">Obtenir une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="f53b6-130">Get a VM</span></span>

<span data-ttu-id="f53b6-131">Une machine virtuelle est requise sur laquelle exécuter l’applet de commande `Get-AzureRmNetworkWatcherSecurityGroupView`.</span><span class="sxs-lookup"><span data-stu-id="f53b6-131">A virtual machine is required to run the `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet against.</span></span> <span data-ttu-id="f53b6-132">L’exemple suivant obtient un objet machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f53b6-132">The following example gets a VM object.</span></span>

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

## <a name="retrieve-security-group-view"></a><span data-ttu-id="f53b6-133">Récupérer la vue Groupe de sécurité</span><span class="sxs-lookup"><span data-stu-id="f53b6-133">Retrieve security group view</span></span>

<span data-ttu-id="f53b6-134">L’étape suivante consiste à récupérer le résultat de la vue Groupe de sécurité.</span><span class="sxs-lookup"><span data-stu-id="f53b6-134">The next step is to retrieve the security group view result.</span></span> <span data-ttu-id="f53b6-135">Ce résultat est comparé au json « de base » qui a été présenté précédemment.</span><span class="sxs-lookup"><span data-stu-id="f53b6-135">This result is compared to the "baseline" json that was shown earlier.</span></span>

```powershell
$secgroup = Get-AzureRmNetworkWatcherSecurityGroupView -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id
```

## <a name="analyzing-the-results"></a><span data-ttu-id="f53b6-136">Analyser les résultats</span><span class="sxs-lookup"><span data-stu-id="f53b6-136">Analyzing the results</span></span>

<span data-ttu-id="f53b6-137">La réponse est regroupée par interfaces réseau.</span><span class="sxs-lookup"><span data-stu-id="f53b6-137">The response is grouped by Network interfaces.</span></span> <span data-ttu-id="f53b6-138">Les différents types de règles renvoyées sont efficaces et constituent les règles de sécurité par défaut.</span><span class="sxs-lookup"><span data-stu-id="f53b6-138">The different types of rules returned are effective and default security rules.</span></span> <span data-ttu-id="f53b6-139">Le résultat est subdivisé en fonction de l’application, sur un sous-réseau ou une carte réseau virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f53b6-139">The result is further broken down by how it is applied, either on a subnet or a virtual NIC.</span></span>

<span data-ttu-id="f53b6-140">Le script PowerShell suivant compare les résultats de la vue Groupe de sécurité avec une sortie existante d’un NSG.</span><span class="sxs-lookup"><span data-stu-id="f53b6-140">The following PowerShell script compares the results of the Security Group View to an existing output of an NSG.</span></span> <span data-ttu-id="f53b6-141">L’exemple suivant est un exemple simple de la façon dont les résultats peuvent être comparés avec l’applet de commande `Compare-Object`.</span><span class="sxs-lookup"><span data-stu-id="f53b6-141">The following example is a simple example of how the results can be compared with `Compare-Object` cmdlet.</span></span>

```powershell
Compare-Object -ReferenceObject $nsgbaserules `
-DifferenceObject $secgroup.NetworkInterfaces[0].NetworkInterfaceSecurityRules `
-Property Name,Description,Protocol,SourcePortRange,DestinationPortRange,SourceAddressPrefix,DestinationAddressPrefix,Access,Priority,Direction
```

<span data-ttu-id="f53b6-142">L’exemple suivant est le résultat.</span><span class="sxs-lookup"><span data-stu-id="f53b6-142">The following example is the result.</span></span> <span data-ttu-id="f53b6-143">Vous pouvez constater que deux règles qui se trouvaient dans le premier ensemble de règles n’étaient pas présentes dans la comparaison.</span><span class="sxs-lookup"><span data-stu-id="f53b6-143">You can see two of the rules that were in the first rule set were not present in the comparison.</span></span>

```
Name                     : My2ndRuleDoNotDelete
Description              : 
Protocol                 : *
SourcePortRange          : *
DestinationPortRange     : 112
SourceAddressPrefix      : *
DestinationAddressPrefix : *
Access                   : Allow
Priority                 : 1020
Direction                : Inbound
SideIndicator            : <=

Name                     : ThisRuleNeedsToStay
Description              : 
Protocol                 : TCP
SourcePortRange          : *
DestinationPortRange     : 5672
SourceAddressPrefix      : *
DestinationAddressPrefix : *
Access                   : Deny
Priority                 : 1030
Direction                : Inbound
SideIndicator            : <=
```

## <a name="next-steps"></a><span data-ttu-id="f53b6-144">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f53b6-144">Next steps</span></span>

<span data-ttu-id="f53b6-145">Si les paramètres ont été modifiés, consultez la page [Gérer les groupes de sécurité réseau](../virtual-network/virtual-network-manage-nsg-arm-portal.md) afin d’effectuer le suivi du groupe de sécurité réseau et des règles de sécurité concernés.</span><span class="sxs-lookup"><span data-stu-id="f53b6-145">If settings have been changed, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that are in question.</span></span>













