---
title: "l’audit de groupe de sécurité réseau aaaAutomate avec l’affichage de groupe de sécurité de l’Observateur réseau Azure | Documents Microsoft"
description: "Cette page fournit des instructions sur la façon de tooconfigure l’audit d’un groupe de sécurité réseau"
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
ms.openlocfilehash: 24fc418c433fceaf55a74b7c3b0e354dc46c8729
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="automate-nsg-auditing-with-azure-network-watcher-security-group-view"></a><span data-ttu-id="a6679-103">Automatiser l’audit NSG avec la vue de groupe de sécurité réseau Network Watcher</span><span class="sxs-lookup"><span data-stu-id="a6679-103">Automate NSG auditing with Azure Network Watcher Security group view</span></span>

<span data-ttu-id="a6679-104">Les clients sont souvent confrontés à hello défi de vérification posture de sécurité hello de leur infrastructure.</span><span class="sxs-lookup"><span data-stu-id="a6679-104">Customers are often faced with hello challenge of verifying hello security posture of their infrastructure.</span></span> <span data-ttu-id="a6679-105">Ce défi n’est pas différent pour leurs machines virtuelles dans Azure.</span><span class="sxs-lookup"><span data-stu-id="a6679-105">This challenge is no different for their VMs in Azure.</span></span> <span data-ttu-id="a6679-106">Il est important toohave un profil de sécurité similaire selon les règles du groupe de sécurité réseau (NSG) hello appliquées.</span><span class="sxs-lookup"><span data-stu-id="a6679-106">It is important toohave a similar security profile based on hello Network Security Group (NSG) rules applied.</span></span> <span data-ttu-id="a6679-107">À l’aide de hello vue du groupe de sécurité, vous pouvez désormais obtenir la liste hello des règles appliquées tooa machine virtuelle au sein d’un groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="a6679-107">Using hello Security Group View, you can now get hello list of rules applied tooa VM within an NSG.</span></span> <span data-ttu-id="a6679-108">Vous pouvez définir un profil de sécurité de groupe de sécurité réseau finale et lancer l’affichage du groupe de sécurité à un rythme hebdomadaire et comparer le profil de hello sortie toohello finale (Gold) et créer un rapport.</span><span class="sxs-lookup"><span data-stu-id="a6679-108">You can define a golden NSG security profile and initiate Security Group View on a weekly cadence and compare hello output toohello golden profile and create a report.</span></span> <span data-ttu-id="a6679-109">Ainsi, vous pouvez identifier facilement toutes les machines virtuelles hello qui ne sont pas conforment toohello prescrit le profil de sécurité.</span><span class="sxs-lookup"><span data-stu-id="a6679-109">This way you can identify with ease all hello VMs that do not conform toohello prescribed security profile.</span></span>

<span data-ttu-id="a6679-110">Si vous n’êtes pas familiarisé avec les groupes de sécurité réseau, consultez la [vue d’ensemble de la sécurité réseau](../virtual-network/virtual-networks-nsg.md)</span><span class="sxs-lookup"><span data-stu-id="a6679-110">If you are unfamiliar with Network Security Groups, visit [Network Security Overview](../virtual-network/virtual-networks-nsg.md)</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a6679-111">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="a6679-111">Before you begin</span></span>

<span data-ttu-id="a6679-112">Dans ce scénario, vous comparez un groupe de sécurité connus bonne ligne de base toohello afficher les résultats retournés pour un ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="a6679-112">In this scenario, you compare a known good baseline toohello security group view results returned for a virtual machine.</span></span>

<span data-ttu-id="a6679-113">Ce scénario suppose que vous avez déjà suivi les étapes hello dans [créer un observateur réseau](network-watcher-create.md) toocreate un observateur réseau.</span><span class="sxs-lookup"><span data-stu-id="a6679-113">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span> <span data-ttu-id="a6679-114">scénario de Hello suppose également qu’un groupe de ressources avec un ordinateur virtuel valide existe toobe utilisé.</span><span class="sxs-lookup"><span data-stu-id="a6679-114">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="a6679-115">Scénario</span><span class="sxs-lookup"><span data-stu-id="a6679-115">Scenario</span></span>

<span data-ttu-id="a6679-116">scénario Hello abordée dans cet article Obtient l’affichage du groupe de sécurité pour un ordinateur virtuel hello.</span><span class="sxs-lookup"><span data-stu-id="a6679-116">hello scenario covered in this article gets hello security group view for a virtual machine.</span></span>

<span data-ttu-id="a6679-117">Dans ce scénario, vous allez :</span><span class="sxs-lookup"><span data-stu-id="a6679-117">In this scenario, you will:</span></span>

- <span data-ttu-id="a6679-118">Récupérer un ensemble de règles correct connu</span><span class="sxs-lookup"><span data-stu-id="a6679-118">Retrieve a known good rule set</span></span>
- <span data-ttu-id="a6679-119">Récupérer une machine virtuelle avec l’API REST</span><span class="sxs-lookup"><span data-stu-id="a6679-119">Retrieve a virtual machine with Rest API</span></span>
- <span data-ttu-id="a6679-120">Obtenir la vue de groupe de sécurité pour la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="a6679-120">Get security group view for virtual machine</span></span>
- <span data-ttu-id="a6679-121">Évaluer la réponse</span><span class="sxs-lookup"><span data-stu-id="a6679-121">Evaluate Response</span></span>

## <a name="retrieve-rule-set"></a><span data-ttu-id="a6679-122">Récupérer l’ensemble de règles</span><span class="sxs-lookup"><span data-stu-id="a6679-122">Retrieve rule set</span></span>

<span data-ttu-id="a6679-123">première étape de Hello dans cet exemple est toowork avec une ligne de base existante.</span><span class="sxs-lookup"><span data-stu-id="a6679-123">hello first step in this example is toowork with an existing baseline.</span></span> <span data-ttu-id="a6679-124">exemple Hello est certains json extraite à partir d’un groupe de sécurité réseau existant à l’aide de hello `Get-AzureRmNetworkSecurityGroup` applet de commande qui est utilisée comme ligne de base hello pour cet exemple.</span><span class="sxs-lookup"><span data-stu-id="a6679-124">hello following example is some json extracted from an existing Network Security Group using hello `Get-AzureRmNetworkSecurityGroup` cmdlet that is used as hello baseline for this example.</span></span>

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

## <a name="convert-rule-set-toopowershell-objects"></a><span data-ttu-id="a6679-125">Convertir les objets tooPowerShell du jeu de règles</span><span class="sxs-lookup"><span data-stu-id="a6679-125">Convert rule set tooPowerShell objects</span></span>

<span data-ttu-id="a6679-126">Dans cette étape, nous lisons un fichier json qui a été créé précédemment avec les règles hello toobe attendu sur hello groupe de sécurité réseau pour cet exemple.</span><span class="sxs-lookup"><span data-stu-id="a6679-126">In this step, we are reading a json file that was created earlier with hello rules that are expected toobe on hello Network Security Group for this example.</span></span>

```powershell
$nsgbaserules = Get-Content -Path C:\temp\testvm1-nsg.json | ConvertFrom-Json
```

## <a name="retrieve-network-watcher"></a><span data-ttu-id="a6679-127">Récupérer Network Watcher</span><span class="sxs-lookup"><span data-stu-id="a6679-127">Retrieve Network Watcher</span></span>

<span data-ttu-id="a6679-128">étape suivante de Hello est instance de l’Observateur réseau tooretrieve hello.</span><span class="sxs-lookup"><span data-stu-id="a6679-128">hello next step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="a6679-129">Hello `$networkWatcher` variable est passée toohello `AzureRmNetworkWatcherSecurityGroupView` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="a6679-129">hello `$networkWatcher` variable is passed toohello `AzureRmNetworkWatcherSecurityGroupView` cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-vm"></a><span data-ttu-id="a6679-130">Obtenir une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="a6679-130">Get a VM</span></span>

<span data-ttu-id="a6679-131">Un ordinateur virtuel est requis toorun hello `Get-AzureRmNetworkWatcherSecurityGroupView` applet de commande par rapport à.</span><span class="sxs-lookup"><span data-stu-id="a6679-131">A virtual machine is required toorun hello `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet against.</span></span> <span data-ttu-id="a6679-132">Bonjour à l’exemple suivant obtient un objet ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="a6679-132">hello following example gets a VM object.</span></span>

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

## <a name="retrieve-security-group-view"></a><span data-ttu-id="a6679-133">Récupérer la vue Groupe de sécurité</span><span class="sxs-lookup"><span data-stu-id="a6679-133">Retrieve security group view</span></span>

<span data-ttu-id="a6679-134">étape suivante de Hello est le résultat de vue du groupe de sécurité tooretrieve hello.</span><span class="sxs-lookup"><span data-stu-id="a6679-134">hello next step is tooretrieve hello security group view result.</span></span> <span data-ttu-id="a6679-135">Le résultat est comparé toohello « baseline » json qui a été indiqué précédemment.</span><span class="sxs-lookup"><span data-stu-id="a6679-135">This result is compared toohello "baseline" json that was shown earlier.</span></span>

```powershell
$secgroup = Get-AzureRmNetworkWatcherSecurityGroupView -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id
```

## <a name="analyzing-hello-results"></a><span data-ttu-id="a6679-136">Analyse des résultats de hello</span><span class="sxs-lookup"><span data-stu-id="a6679-136">Analyzing hello results</span></span>

<span data-ttu-id="a6679-137">réponse de Hello est regroupé par les interfaces réseau.</span><span class="sxs-lookup"><span data-stu-id="a6679-137">hello response is grouped by Network interfaces.</span></span> <span data-ttu-id="a6679-138">Hello différents types de règles retournées sont efficaces et règles de sécurité par défaut.</span><span class="sxs-lookup"><span data-stu-id="a6679-138">hello different types of rules returned are effective and default security rules.</span></span> <span data-ttu-id="a6679-139">résultat de Hello est davantage ventilé par comment elle est appliquée, sur un sous-réseau ou une carte réseau virtuelle.</span><span class="sxs-lookup"><span data-stu-id="a6679-139">hello result is further broken down by how it is applied, either on a subnet or a virtual NIC.</span></span>

<span data-ttu-id="a6679-140">Hello script PowerShell suivant compare les résultats de hello de hello sortie existante de tooan vue de groupe de sécurité d’un groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="a6679-140">hello following PowerShell script compares hello results of hello Security Group View tooan existing output of an NSG.</span></span> <span data-ttu-id="a6679-141">Bonjour exemple suivant est un exemple simple de la façon dont les résultats de hello puissent être comparés avec `Compare-Object` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="a6679-141">hello following example is a simple example of how hello results can be compared with `Compare-Object` cmdlet.</span></span>

```powershell
Compare-Object -ReferenceObject $nsgbaserules `
-DifferenceObject $secgroup.NetworkInterfaces[0].NetworkInterfaceSecurityRules `
-Property Name,Description,Protocol,SourcePortRange,DestinationPortRange,SourceAddressPrefix,DestinationAddressPrefix,Access,Priority,Direction
```

<span data-ttu-id="a6679-142">Bonjour à l’exemple suivant résulte hello.</span><span class="sxs-lookup"><span data-stu-id="a6679-142">hello following example is hello result.</span></span> <span data-ttu-id="a6679-143">Vous pouvez voir deux règles hello qui étaient dans le premier ensemble de règles hello n’étaient pas présentes dans la comparaison de hello.</span><span class="sxs-lookup"><span data-stu-id="a6679-143">You can see two of hello rules that were in hello first rule set were not present in hello comparison.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="a6679-144">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a6679-144">Next steps</span></span>

<span data-ttu-id="a6679-145">Si les paramètres ont été modifiés, consultez [gérer les groupes de sécurité réseau](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack vers le bas hello sécurité et groupe de règles de sécurité réseau qui sont en question.</span><span class="sxs-lookup"><span data-stu-id="a6679-145">If settings have been changed, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that are in question.</span></span>













