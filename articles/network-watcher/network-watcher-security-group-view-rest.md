---
title: "sécurité du réseau aaaAnalyze avec vue groupe de sécurité dans Azure réseau Observateur - API REST | Documents Microsoft"
description: "Cet article décrit comment tooanalyze de PowerShell toouse a virtual machines de sécurité avec l’affichage du groupe de sécurité."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: a2f418fe-f5d2-43ed-8dc3-df0ed2a4d4ac
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 0858a64a9454816e05f06dadb9536ad0c755e90e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-rest-api"></a><span data-ttu-id="c4036-103">Analyser la sécurité de votre machine virtuelle par le biais de la vue Groupe de sécurité dans l’API REST</span><span class="sxs-lookup"><span data-stu-id="c4036-103">Analyze your Virtual Machine security with Security Group View using REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="c4036-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c4036-104">PowerShell</span></span>](network-watcher-security-group-view-powershell.md)
> - [<span data-ttu-id="c4036-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="c4036-105">CLI 1.0</span></span>](network-watcher-security-group-view-cli-nodejs.md)
> - [<span data-ttu-id="c4036-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="c4036-106">CLI 2.0</span></span>](network-watcher-security-group-view-cli.md)
> - [<span data-ttu-id="c4036-107">API REST</span><span class="sxs-lookup"><span data-stu-id="c4036-107">REST API</span></span>](network-watcher-security-group-view-rest.md)

<span data-ttu-id="c4036-108">Affichage de groupe de sécurité retourne les règles de sécurité réseau configurée et efficace qui sont appliqués tooa l’ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="c4036-108">Security group view returns configured and effective network security rules that are applied tooa virtual machine.</span></span> <span data-ttu-id="c4036-109">Cette fonctionnalité est utile tooaudit et diagnostiquer les groupes de sécurité réseau et les règles qui sont configurés sur un trafic tooensure de machine virtuelle est correctement autorisé ou refusé.</span><span class="sxs-lookup"><span data-stu-id="c4036-109">This capability is useful tooaudit and diagnose Network Security Groups and rules that are configured on a VM tooensure traffic is being correctly allowed or denied.</span></span> <span data-ttu-id="c4036-110">Dans cet article, nous vous indiquons fonctionnement tooretrieve hello efficace et appliqué la sécurité des règles de machine virtuelle de tooa à l’aide des API REST</span><span class="sxs-lookup"><span data-stu-id="c4036-110">In this article, we show you how tooretrieve hello effective and applied security rules tooa virtual machine using REST API</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="c4036-111">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="c4036-111">Before you begin</span></span>

<span data-ttu-id="c4036-112">Dans ce scénario, vous appelez affichage du groupe tooget hello sécurité hello API Rest de l’Observateur réseau pour un ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="c4036-112">In this scenario, you call hello Network Watcher Rest API tooget hello security group view for a virtual machine.</span></span> <span data-ttu-id="c4036-113">ARMclient est utilisé toocall hello REST API à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c4036-113">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="c4036-114">ARMClient est accessible sur le site chocolatey à partir de la page [ARMClient sur Chocolatey](https://chocolatey.org/packages/ARMClient).</span><span class="sxs-lookup"><span data-stu-id="c4036-114">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="c4036-115">Ce scénario suppose que vous avez déjà suivi les étapes hello dans [créer un observateur réseau](network-watcher-create.md) toocreate un observateur réseau.</span><span class="sxs-lookup"><span data-stu-id="c4036-115">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span> <span data-ttu-id="c4036-116">scénario de Hello suppose également qu’un groupe de ressources avec un ordinateur virtuel valide existe toobe utilisé.</span><span class="sxs-lookup"><span data-stu-id="c4036-116">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="c4036-117">Scénario</span><span class="sxs-lookup"><span data-stu-id="c4036-117">Scenario</span></span>

<span data-ttu-id="c4036-118">scénario Hello abordée dans cet article récupère des règles de sécurité efficace et appliquées hello pour un ordinateur virtuel donné.</span><span class="sxs-lookup"><span data-stu-id="c4036-118">hello scenario covered in this article retrieves hello effective and applied security rules for a given virtual machine.</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="c4036-119">Se connecter à ARMClient</span><span class="sxs-lookup"><span data-stu-id="c4036-119">Log in with ARMClient</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="c4036-120">Récupérer une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="c4036-120">Retrieve a virtual machine</span></span>

<span data-ttu-id="c4036-121">Exécutez hello suivant script tooreturn un machineThe virtuel suivant code doit variables :</span><span class="sxs-lookup"><span data-stu-id="c4036-121">Run hello following script tooreturn a virtual machineThe following code needs variables:</span></span>

- <span data-ttu-id="c4036-122">**ID d’abonnement** -id d’abonnement hello peut également être récupéré avec hello **Get-AzureRMSubscription** applet de commande.</span><span class="sxs-lookup"><span data-stu-id="c4036-122">**subscriptionId** - hello subscription id can also be retrieved with hello **Get-AzureRMSubscription** cmdlet.</span></span>
- <span data-ttu-id="c4036-123">**resourceGroupName** hello - nom du groupe de ressources qui contient des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="c4036-123">**resourceGroupName** - hello name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = '<resource group name>'

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="c4036-124">informations nécessaires Hello sont hello **id** sous type de hello `Microsoft.Compute/virtualMachines` en réponse, comme dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="c4036-124">hello information that is needed is hello **id** under hello type `Microsoft.Compute/virtualMachines` in response, as seen in hello following example:</span></span>

```json
...,
        "networkProfile": {
          "networkInterfaces": [
            {
              "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft
.Network/networkInterfaces/{nicName}"
            }
          ]
        },
        "provisioningState": "Succeeded"
      },
      "resources": [
        {
          "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Com
pute/virtualMachines/{vmName}/extensions/CustomScriptExtension"
        }
      ],
      "type": "Microsoft.Compute/virtualMachines",
      "location": "westcentralus",
      "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute
/virtualMachines/{vmName}",
      "name": "{vmName}"
    }
  ]
}
```

## <a name="get-security-group-view-for-virtual-machine"></a><span data-ttu-id="c4036-125">Obtenir la vue de groupe de sécurité pour la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="c4036-125">Get security group view for virtual machine</span></span>

<span data-ttu-id="c4036-126">Hello l’exemple suivant demande l’affichage du groupe de sécurité d’un ordinateur virtuel cible hello.</span><span class="sxs-lookup"><span data-stu-id="c4036-126">hello following example requests hello security group view of a targeted virtual machine.</span></span> <span data-ttu-id="c4036-127">résultats Hello à partir de cet exemple peuvent être utilisé toocompare toohello règles et défini par toolook d’origine hello écarts de configuration de sécurité.</span><span class="sxs-lookup"><span data-stu-id="c4036-127">hello results from this example can be used toocompare toohello rules and security defined by hello origination toolook for configuration drift.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"
$networkWatcherName = "<network watcher name>"
$targetUri = "<uri of target resource>" # Example: /subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.compute/virtualMachine/$vmName

$requestBody = @"
{
    'targetResourceId': '${targetUri}'

}
"@
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/securityGroupView?api-version=2016-12-01" $requestBody -verbose
```

## <a name="view-hello-response"></a><span data-ttu-id="c4036-128">Afficher la réponse hello</span><span class="sxs-lookup"><span data-stu-id="c4036-128">View hello response</span></span>

<span data-ttu-id="c4036-129">Hello suivant l’exemple est retournée à partir de hello précédant la commande de réponse hello.</span><span class="sxs-lookup"><span data-stu-id="c4036-129">hello following sample is hello response returned from hello preceding command.</span></span> <span data-ttu-id="c4036-130">Hello résultats affichent toutes les règles de sécurité efficace et appliquées hello sur l’ordinateur virtuel de hello réparti dans les groupes **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, et  **EffectiveSecurityRules**.</span><span class="sxs-lookup"><span data-stu-id="c4036-130">hello results show all hello effective and applied security rules on hello virtual machine broken down in groups of **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, and **EffectiveSecurityRules**.</span></span>

```json

{
  "networkInterfaces": [
    {
      "securityRuleAssociations": {
        "networkInterfaceAssociation": {
          "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkInterfaces/{nicName}",
          "securityRules": [
            {
              "name": "default-allow-rdp",
              "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}/securityRules/default-allow-rdp",
              "etag": "W/\"d4c411d4-0d62-49dc-8092-3d4b57825740\"",
              "properties": {
                "provisioningState": "Succeeded",
                "protocol": "TCP",
                "sourcePortRange": "*",
                "destinationPortRange": "3389",
                "sourceAddressPrefix": "*",
                "destinationAddressPrefix": "*",
                "access": "Allow",
                "priority": 1000,
                "direction": "Inbound"
              }
            }
          ]
        },
        "defaultSecurityRules": [
          {
            "name": "AllowVnetInBound",
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}/defaultSecurityRules/",
            "properties": {
              "provisioningState": "Succeeded",
              "description": "Allow inbound traffic from all VMs in VNET",
              "protocol": "*",
              "sourcePortRange": "*",
              "destinationPortRange": "*",
              "sourceAddressPrefix": "VirtualNetwork",
              "destinationAddressPrefix": "VirtualNetwork",
              "access": "Allow",
              "priority": 65000,
              "direction": "Inbound"
            }
          },
          ...
        ],
        "effectiveSecurityRules": [
          {
            "name": "DefaultOutboundDenyAll",
            "protocol": "All",
            "sourcePortRange": "0-65535",
            "destinationPortRange": "0-65535",
            "sourceAddressPrefix": "*",
            "destinationAddressPrefix": "*",
            "access": "Deny",
            "priority": 65500,
            "direction": "Outbound"
          },
          ...
        ]
      }
    }
  ]
}
```

## <a name="next-steps"></a><span data-ttu-id="c4036-131">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c4036-131">Next steps</span></span>

<span data-ttu-id="c4036-132">Visitez [audit réseau sécurité groupes (NSG) avec l’Observateur réseau](network-watcher-security-group-view-powershell.md) toolearn comment tooautomate la validation de groupes de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="c4036-132">Visit [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-security-group-view-powershell.md) toolearn how tooautomate validation of Network Security Groups.</span></span>


