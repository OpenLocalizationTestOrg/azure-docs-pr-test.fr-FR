---
title: "Analyser la sécurité réseau avec la vue Groupe de sécurité réseau Network Watcher - PowerShell | Microsoft Docs"
description: "Cet article décrit comment utiliser PowerShell pour analyser la sécurité des machines virtuelles par le biais de la vue Groupe de sécurité."
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
ms.openlocfilehash: 363fdd9f1de933bb4050f91e1e111aaf3e419058
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-powershell"></a><span data-ttu-id="30bb0-103">Analyser la sécurité de votre machine virtuelle par le biais de la vue Groupe de sécurité dans PowerShell</span><span class="sxs-lookup"><span data-stu-id="30bb0-103">Analyze your Virtual Machine security with Security Group View using PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="30bb0-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="30bb0-104">PowerShell</span></span>](network-watcher-security-group-view-powershell.md)
> - [<span data-ttu-id="30bb0-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="30bb0-105">CLI 1.0</span></span>](network-watcher-security-group-view-cli-nodejs.md)
> - [<span data-ttu-id="30bb0-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="30bb0-106">CLI 2.0</span></span>](network-watcher-security-group-view-cli.md)
> - [<span data-ttu-id="30bb0-107">API REST</span><span class="sxs-lookup"><span data-stu-id="30bb0-107">REST API</span></span>](network-watcher-security-group-view-rest.md)

<span data-ttu-id="30bb0-108">La vue Groupe de sécurité renvoie des règles de sécurité de réseau configurées et efficaces, appliquées à une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="30bb0-108">Security group view returns configured and effective network security rules that are applied to a virtual machine.</span></span> <span data-ttu-id="30bb0-109">Cette fonctionnalité permet d’auditer et de diagnostiquer les groupes de sécurité réseau ainsi que les règles configurées sur une machine virtuelle afin de garantir l’autorisation ou le refus appropriés du trafic.</span><span class="sxs-lookup"><span data-stu-id="30bb0-109">This capability is useful to audit and diagnose Network Security Groups and rules that are configured on a VM to ensure traffic is being correctly allowed or denied.</span></span> <span data-ttu-id="30bb0-110">Dans cet article, nous vous montrons comment récupérer des règles de sécurité configurées et efficaces pour une machine virtuelle à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="30bb0-110">In this article, we show you how to retrieve the configured and effective security rules to a virtual machine using PowerShell</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="30bb0-111">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="30bb0-111">Before you begin</span></span>

<span data-ttu-id="30bb0-112">Dans ce scénario, vous exécutez l’applet de commande `Get-AzureRmNetworkWatcherSecurityGroupView` pour récupérer les informations sur la règle de sécurité.</span><span class="sxs-lookup"><span data-stu-id="30bb0-112">In this scenario, you run the `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet to retrieve the security rule information.</span></span>

<span data-ttu-id="30bb0-113">Ce scénario suppose que vous ayez déjà suivi la procédure décrite dans [Create a Network Watcher (Créer une instance Network Watcher)](network-watcher-create.md) pour créer une instance Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="30bb0-113">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="30bb0-114">Scénario</span><span class="sxs-lookup"><span data-stu-id="30bb0-114">Scenario</span></span>

<span data-ttu-id="30bb0-115">Le scénario décrit dans cet article récupère des règles de sécurité configurées et efficaces pour une machine virtuelle donnée.</span><span class="sxs-lookup"><span data-stu-id="30bb0-115">The scenario covered in this article retrieves the configured and effective security rules for a given virtual machine.</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="30bb0-116">Récupérer Network Watcher</span><span class="sxs-lookup"><span data-stu-id="30bb0-116">Retrieve Network Watcher</span></span>

<span data-ttu-id="30bb0-117">La première étape consiste à récupérer l’instance Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="30bb0-117">The first step is to retrieve the Network Watcher instance.</span></span> <span data-ttu-id="30bb0-118">Cette variable est transmise à l’applet de commande `Get-AzureRmNetworkWatcherSecurityGroupView`.</span><span class="sxs-lookup"><span data-stu-id="30bb0-118">This variable is passed to the `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName
```

## <a name="get-a-vm"></a><span data-ttu-id="30bb0-119">Obtenir une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="30bb0-119">Get a VM</span></span>

<span data-ttu-id="30bb0-120">Une machine virtuelle est requise sur laquelle exécuter l’applet de commande `Get-AzureRmNetworkWatcherSecurityGroupView`.</span><span class="sxs-lookup"><span data-stu-id="30bb0-120">A virtual machine is required to run the `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet against.</span></span> <span data-ttu-id="30bb0-121">L’exemple suivant obtient un objet machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="30bb0-121">The following example gets a VM object.</span></span>

```powershell
$VM = Get-AzurermVM -ResourceGroupName testrg -Name testvm1
```

## <a name="retrieve-security-group-view"></a><span data-ttu-id="30bb0-122">Récupérer la vue Groupe de sécurité</span><span class="sxs-lookup"><span data-stu-id="30bb0-122">Retrieve security group view</span></span>

<span data-ttu-id="30bb0-123">L’étape suivante consiste à récupérer le résultat de la vue Groupe de sécurité.</span><span class="sxs-lookup"><span data-stu-id="30bb0-123">The next step is to retrieve the security group view result.</span></span>

```powershell
$secgroup = Get-AzureRmNetworkWatcherSecurityGroupView -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id
```

## <a name="viewing-the-results"></a><span data-ttu-id="30bb0-124">Affichage des résultats</span><span class="sxs-lookup"><span data-stu-id="30bb0-124">Viewing the results</span></span>

<span data-ttu-id="30bb0-125">L’exemple suivant est une réponse abrégée des résultats renvoyés.</span><span class="sxs-lookup"><span data-stu-id="30bb0-125">The following example is a shortened response of the results returned.</span></span> <span data-ttu-id="30bb0-126">Les résultats présentent toutes les règles de sécurité efficaces et appliquées sur la machine virtuelle, réparties en plusieurs groupes : **NetworkInterfaceSecurityRules**, **DefaultSecurityRules** et **EffectiveSecurityRules**.</span><span class="sxs-lookup"><span data-stu-id="30bb0-126">The results show all the effective and applied security rules on the virtual machine broken down in groups of **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, and **EffectiveSecurityRules**.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="30bb0-127">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="30bb0-127">Next steps</span></span>

<span data-ttu-id="30bb0-128">Consultez la page [Auditing Network Security Groups (NSG) with Network Watcher (Audit des groupes de sécurité réseau avec Network Watcher)](network-watcher-nsg-auditing-powershell.md) pour découvrir comment automatiser la validation des groupes de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="30bb0-128">Visit [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md) to learn how to automate validation of Network Security Groups.</span></span>


