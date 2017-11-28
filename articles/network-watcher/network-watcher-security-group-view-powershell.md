---
title: "sécurité du réseau aaaAnalyze avec vue groupe de sécurité dans Azure réseau Observateur - PowerShell | Documents Microsoft"
description: "Cet article décrit comment tooanalyze de PowerShell toouse a virtual machines de sécurité avec l’affichage du groupe de sécurité."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 04e76b49-6a1b-4d0f-9a9b-51cf2f4df5a2
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 5e1990d97899bd8585025ec13dd556ab2e034c3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-powershell"></a><span data-ttu-id="de7ac-103">Analyser la sécurité de votre machine virtuelle par le biais de la vue Groupe de sécurité dans PowerShell</span><span class="sxs-lookup"><span data-stu-id="de7ac-103">Analyze your Virtual Machine security with Security Group View using PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="de7ac-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="de7ac-104">PowerShell</span></span>](network-watcher-security-group-view-powershell.md)
> - [<span data-ttu-id="de7ac-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="de7ac-105">CLI 1.0</span></span>](network-watcher-security-group-view-cli-nodejs.md)
> - [<span data-ttu-id="de7ac-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="de7ac-106">CLI 2.0</span></span>](network-watcher-security-group-view-cli.md)
> - [<span data-ttu-id="de7ac-107">API REST</span><span class="sxs-lookup"><span data-stu-id="de7ac-107">REST API</span></span>](network-watcher-security-group-view-rest.md)

<span data-ttu-id="de7ac-108">Affichage de groupe de sécurité retourne les règles de sécurité réseau configurée et efficace qui sont appliqués tooa l’ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="de7ac-108">Security group view returns configured and effective network security rules that are applied tooa virtual machine.</span></span> <span data-ttu-id="de7ac-109">Cette fonctionnalité est utile tooaudit et diagnostiquer les groupes de sécurité réseau et les règles qui sont configurés sur un trafic tooensure de machine virtuelle est correctement autorisé ou refusé.</span><span class="sxs-lookup"><span data-stu-id="de7ac-109">This capability is useful tooaudit and diagnose Network Security Groups and rules that are configured on a VM tooensure traffic is being correctly allowed or denied.</span></span> <span data-ttu-id="de7ac-110">Dans cet article, nous vous indiquons comment tooretrieve hello configuré et virtuels de sécurité efficace de tooa de règles à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="de7ac-110">In this article, we show you how tooretrieve hello configured and effective security rules tooa virtual machine using PowerShell</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="de7ac-111">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="de7ac-111">Before you begin</span></span>

<span data-ttu-id="de7ac-112">Dans ce scénario, vous exécutez hello `Get-AzureRmNetworkWatcherSecurityGroupView` informations de règle de sécurité applet de commande tooretrieve hello.</span><span class="sxs-lookup"><span data-stu-id="de7ac-112">In this scenario, you run hello `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet tooretrieve hello security rule information.</span></span>

<span data-ttu-id="de7ac-113">Ce scénario suppose que vous avez déjà suivi les étapes hello dans [créer un observateur réseau](network-watcher-create.md) toocreate un observateur réseau.</span><span class="sxs-lookup"><span data-stu-id="de7ac-113">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="de7ac-114">Scénario</span><span class="sxs-lookup"><span data-stu-id="de7ac-114">Scenario</span></span>

<span data-ttu-id="de7ac-115">scénario Hello abordée dans cet article récupère hello configuré et les règles de sécurité efficace pour un ordinateur virtuel donné.</span><span class="sxs-lookup"><span data-stu-id="de7ac-115">hello scenario covered in this article retrieves hello configured and effective security rules for a given virtual machine.</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="de7ac-116">Récupérer Network Watcher</span><span class="sxs-lookup"><span data-stu-id="de7ac-116">Retrieve Network Watcher</span></span>

<span data-ttu-id="de7ac-117">première étape de Hello est instance de l’Observateur réseau tooretrieve hello.</span><span class="sxs-lookup"><span data-stu-id="de7ac-117">hello first step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="de7ac-118">Cette variable est passée toohello `Get-AzureRmNetworkWatcherSecurityGroupView` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="de7ac-118">This variable is passed toohello `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName
```

## <a name="get-a-vm"></a><span data-ttu-id="de7ac-119">Obtenir une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="de7ac-119">Get a VM</span></span>

<span data-ttu-id="de7ac-120">Un ordinateur virtuel est requis toorun hello `Get-AzureRmNetworkWatcherSecurityGroupView` applet de commande par rapport à.</span><span class="sxs-lookup"><span data-stu-id="de7ac-120">A virtual machine is required toorun hello `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet against.</span></span> <span data-ttu-id="de7ac-121">Bonjour à l’exemple suivant obtient un objet ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="de7ac-121">hello following example gets a VM object.</span></span>

```powershell
$VM = Get-AzurermVM -ResourceGroupName testrg -Name testvm1
```

## <a name="retrieve-security-group-view"></a><span data-ttu-id="de7ac-122">Récupérer la vue Groupe de sécurité</span><span class="sxs-lookup"><span data-stu-id="de7ac-122">Retrieve security group view</span></span>

<span data-ttu-id="de7ac-123">étape suivante de Hello est le résultat de vue du groupe de sécurité tooretrieve hello.</span><span class="sxs-lookup"><span data-stu-id="de7ac-123">hello next step is tooretrieve hello security group view result.</span></span>

```powershell
$secgroup = Get-AzureRmNetworkWatcherSecurityGroupView -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id
```

## <a name="viewing-hello-results"></a><span data-ttu-id="de7ac-124">Affichage des résultats de hello</span><span class="sxs-lookup"><span data-stu-id="de7ac-124">Viewing hello results</span></span>

<span data-ttu-id="de7ac-125">Hello exemple suivant est une réponse raccourcie de hello les résultats retournés.</span><span class="sxs-lookup"><span data-stu-id="de7ac-125">hello following example is a shortened response of hello results returned.</span></span> <span data-ttu-id="de7ac-126">Hello résultats affichent toutes les règles de sécurité efficace et appliquées hello sur l’ordinateur virtuel de hello réparti dans les groupes **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, et  **EffectiveSecurityRules**.</span><span class="sxs-lookup"><span data-stu-id="de7ac-126">hello results show all hello effective and applied security rules on hello virtual machine broken down in groups of **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, and **EffectiveSecurityRules**.</span></span>

```
NetworkInterfaces : [
                      {
                        "NetworkInterfaceSecurityRules": [
                          {
                            "Name": "default-allow-rdp",
                            "Etag": "W/\"d4c411d4-0d62-49dc-8092-3d4b57825740\"",
                            "Id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg2/providers/Microsoft.Network/networkSecurityGroups/testvm2-nsg/securityRules/default-allow-rdp",
                            "Protocol": "TCP",
                            "SourcePortRange": "*",
                            "DestinationPortRange": "3389",
                            "SourceAddressPrefix": "*",
                            "DestinationAddressPrefix": "*",
                            "Access": "Allow",
                            "Priority": 1000,
                            "Direction": "Inbound",
                            "ProvisioningState": "Succeeded"
                          }
                          ...
                        ],
                        "DefaultSecurityRules": [
                          {
                            "Name": "AllowVnetInBound",
                            "Id": "/subscriptions00000000-0000-0000-0000-000000000000/resourceGroups/testrg2/providers/Microsoft.Network/networkSecurityGroups/testvm2-nsg/defaultSecurityRules/",
                            "Description": "Allow inbound traffic from all VMs in VNET",
                            "Protocol": "*",
                            "SourcePortRange": "*",
                            "DestinationPortRange": "*",
                            "SourceAddressPrefix": "VirtualNetwork",
                            "DestinationAddressPrefix": "VirtualNetwork",
                            "Access": "Allow",
                            "Priority": 65000,
                            "Direction": "Inbound",
                            "ProvisioningState": "Succeeded"
                          }
                          ...
                        ],
                        "EffectiveSecurityRules": [
                          {
                            "Name": "DefaultOutboundDenyAll",
                            "Protocol": "All",
                            "SourcePortRange": "0-65535",
                            "DestinationPortRange": "0-65535",
                            "SourceAddressPrefix": "*",
                            "DestinationAddressPrefix": "*",
                            "ExpandedSourceAddressPrefix": [],
                            "ExpandedDestinationAddressPrefix": [],
                            "Access": "Deny",
                            "Priority": 65500,
                            "Direction": "Outbound"
                          },
                          ...
                        ]
                      }
                    ]
```

## <a name="next-steps"></a><span data-ttu-id="de7ac-127">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="de7ac-127">Next steps</span></span>

<span data-ttu-id="de7ac-128">Visitez [audit réseau sécurité groupes (NSG) avec l’Observateur réseau](network-watcher-nsg-auditing-powershell.md) toolearn comment tooautomate la validation de groupes de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="de7ac-128">Visit [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md) toolearn how tooautomate validation of Network Security Groups.</span></span>


