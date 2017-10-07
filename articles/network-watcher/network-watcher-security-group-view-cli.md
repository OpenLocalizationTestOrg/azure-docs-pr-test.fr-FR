---
title: "sécurité du réseau aaaAnalyze avec vue groupe de sécurité dans Azure réseau Observateur - Azure CLI 2.0 | Documents Microsoft"
description: "Cet article décrit comment tooanalyze toouse Azure CLI 2.0 a virtual machines de sécurité avec l’affichage du groupe de sécurité."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: a986ff4f-7e0c-4994-95e1-4ac824986500
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 31a4cd628f54d7548f495251fd275f099e79a060
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-azure-cli-20"></a><span data-ttu-id="bb3d8-103">Analyser la sécurité de votre machine virtuelle par le biais de la vue Groupe de sécurité à l’aide d’Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="bb3d8-103">Analyze your Virtual Machine security with Security Group View using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="bb3d8-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bb3d8-104">PowerShell</span></span>](network-watcher-security-group-view-powershell.md)
> - [<span data-ttu-id="bb3d8-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="bb3d8-105">CLI 1.0</span></span>](network-watcher-security-group-view-cli-nodejs.md)
> - [<span data-ttu-id="bb3d8-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="bb3d8-106">CLI 2.0</span></span>](network-watcher-security-group-view-cli.md)
> - [<span data-ttu-id="bb3d8-107">API REST</span><span class="sxs-lookup"><span data-stu-id="bb3d8-107">REST API</span></span>](network-watcher-security-group-view-rest.md)

<span data-ttu-id="bb3d8-108">Affichage de groupe de sécurité retourne les règles de sécurité réseau configurée et efficace qui sont appliqués tooa l’ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="bb3d8-108">Security group view returns configured and effective network security rules that are applied tooa virtual machine.</span></span> <span data-ttu-id="bb3d8-109">Cette fonctionnalité est utile tooaudit et diagnostiquer les groupes de sécurité réseau et les règles qui sont configurés sur un trafic tooensure de machine virtuelle est correctement autorisé ou refusé.</span><span class="sxs-lookup"><span data-stu-id="bb3d8-109">This capability is useful tooaudit and diagnose Network Security Groups and rules that are configured on a VM tooensure traffic is being correctly allowed or denied.</span></span> <span data-ttu-id="bb3d8-110">Dans cet article, nous vous indiquons comment tooretrieve hello configuré et sécurité efficace règles tooa machine virtuelle Azure CLI</span><span class="sxs-lookup"><span data-stu-id="bb3d8-110">In this article, we show you how tooretrieve hello configured and effective security rules tooa virtual machine using Azure CLI</span></span>


<span data-ttu-id="bb3d8-111">Cet article utilise notre prochaine génération CLI pour le modèle de déploiement de la gestion des ressources d’hello, Azure CLI 2.0, qui est disponible pour Windows, Mac et Linux.</span><span class="sxs-lookup"><span data-stu-id="bb3d8-111">This article uses our next generation CLI for hello resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="bb3d8-112">les étapes tooperform hello dans cet article, vous devez trop[installer hello Interface de ligne de commande Azure pour Mac, Linux et Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="bb3d8-112">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="bb3d8-113">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="bb3d8-113">Before you begin</span></span>

<span data-ttu-id="bb3d8-114">Ce scénario suppose que vous avez déjà suivi les étapes hello dans [créer un observateur réseau](network-watcher-create.md) toocreate un observateur réseau.</span><span class="sxs-lookup"><span data-stu-id="bb3d8-114">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="bb3d8-115">Scénario</span><span class="sxs-lookup"><span data-stu-id="bb3d8-115">Scenario</span></span>

<span data-ttu-id="bb3d8-116">scénario Hello abordée dans cet article récupère hello configuré et les règles de sécurité efficace pour un ordinateur virtuel donné.</span><span class="sxs-lookup"><span data-stu-id="bb3d8-116">hello scenario covered in this article retrieves hello configured and effective security rules for a given virtual machine.</span></span>

## <a name="get-a-vm"></a><span data-ttu-id="bb3d8-117">Obtenir une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="bb3d8-117">Get a VM</span></span>

<span data-ttu-id="bb3d8-118">Un ordinateur virtuel est requis toorun hello `vm list` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="bb3d8-118">A virtual machine is required toorun hello `vm list` cmdlet.</span></span> <span data-ttu-id="bb3d8-119">Hello commande suivante répertorie les hello machines virtuelles dans un groupe de ressources :</span><span class="sxs-lookup"><span data-stu-id="bb3d8-119">hello following command lists hello virtual machines in a resource group:</span></span>

```azurecli
az vm list -resource-group resourceGroupName
```

<span data-ttu-id="bb3d8-120">Une fois que vous connaissez hello virtual machine, vous pouvez utiliser hello `vm show` tooget de l’applet de commande son Id de ressource :</span><span class="sxs-lookup"><span data-stu-id="bb3d8-120">Once you know hello virtual machine, you can use hello `vm show` cmdlet tooget its resource Id:</span></span>

```azurecli
az vm show -resource-group resourceGroupName -name virtualMachineName
```

## <a name="retrieve-security-group-view"></a><span data-ttu-id="bb3d8-121">Récupérer la vue Groupe de sécurité</span><span class="sxs-lookup"><span data-stu-id="bb3d8-121">Retrieve security group view</span></span>

<span data-ttu-id="bb3d8-122">étape suivante de Hello est le résultat de vue du groupe de sécurité tooretrieve hello.</span><span class="sxs-lookup"><span data-stu-id="bb3d8-122">hello next step is tooretrieve hello security group view result.</span></span>

```azurecli
az network watcher show-security-group-view --resource-group resourceGroupName --vm vmName
```

## <a name="viewing-hello-results"></a><span data-ttu-id="bb3d8-123">Affichage des résultats de hello</span><span class="sxs-lookup"><span data-stu-id="bb3d8-123">Viewing hello results</span></span>

<span data-ttu-id="bb3d8-124">Hello exemple suivant est une réponse raccourcie de hello les résultats retournés.</span><span class="sxs-lookup"><span data-stu-id="bb3d8-124">hello following example is a shortened response of hello results returned.</span></span> <span data-ttu-id="bb3d8-125">Hello résultats affichent toutes les règles de sécurité efficace et appliquées hello sur l’ordinateur virtuel de hello réparti dans les groupes **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, et  **EffectiveSecurityRules**.</span><span class="sxs-lookup"><span data-stu-id="bb3d8-125">hello results show all hello effective and applied security rules on hello virtual machine broken down in groups of **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, and **EffectiveSecurityRules**.</span></span>

```json
{
  "networkInterfaces": [
    {
      "id": "/subscriptions/00000000-0000-0000-0000-0000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkInterfaces/{nicName}",
      "resourceGroup": "{resourceGroupName}",
      "securityRuleAssociations": {
        "defaultSecurityRules": [
          {
            "access": "Allow",
            "description": "Allow inbound traffic from all VMs in VNET",
            "destinationAddressPrefix": "VirtualNetwork",
            "destinationPortRange": "*",
            "direction": "Inbound",
            "etag": null,
            "id": "/subscriptions/00000000-0000-0000-0000-0000000000000/resourceGroups//providers/Microsoft.Network/networkSecurityGroups/{nsgName}/defaultSecurityRules/AllowVnetInBound",
            "name": "AllowVnetInBound",
            "priority": 65000,
            "protocol": "*",
            "provisioningState": "Succeeded",
            "resourceGroup": "",
            "sourceAddressPrefix": "VirtualNetwork",
            "sourcePortRange": "*"
          }...
        ],
        "effectiveSecurityRules": [
          {
            "access": "Deny",
            "destinationAddressPrefix": "*",
            "destinationPortRange": "0-65535",
            "direction": "Outbound",
            "expandedDestinationAddressPrefix": null,
            "expandedSourceAddressPrefix": null,
            "name": "DefaultOutboundDenyAll",
            "priority": 65500,
            "protocol": "All",
            "sourceAddressPrefix": "*",
            "sourcePortRange": "0-65535"
          },
          {
            "access": "Allow",
            "destinationAddressPrefix": "VirtualNetwork",
            "destinationPortRange": "0-65535",
            "direction": "Outbound",
            "expandedDestinationAddressPrefix": [
              "10.1.0.0/24",
              "168.63.129.16/32"
            ],
            "expandedSourceAddressPrefix": [
              "10.1.0.0/24",
              "168.63.129.16/32"
            ],
            "name": "DefaultRule_AllowVnetOutBound",
            "priority": 65000,
            "protocol": "All",
            "sourceAddressPrefix": "VirtualNetwork",
            "sourcePortRange": "0-65535"
          },...
        ],
        "networkInterfaceAssociation": {
          "id": "/subscriptions/00000000-0000-0000-0000-0000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkInterfaces/{nicName}",
          "resourceGroup": "{resourceGroupName}",
          "securityRules": [
            {
              "access": "Allow",
              "description": null,
              "destinationAddressPrefix": "*",
              "destinationPortRange": "3389",
              "direction": "Inbound",
              "etag": "W/\"efb606c1-2d54-475a-ab20-da3f80393577\"",
              "id": "/subscriptions/00000000-0000-0000-0000-0000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}/securityRules/default-allow-rdp",
              "name": "default-allow-rdp",
              "priority": 1000,
              "protocol": "TCP",
              "provisioningState": "Succeeded",
              "resourceGroup": "{resourceGroupName}",
              "sourceAddressPrefix": "*",
              "sourcePortRange": "*"
            }
          ]
        },
        "subnetAssociation": null
      }
    }
  ]
}
```

## <a name="next-steps"></a><span data-ttu-id="bb3d8-126">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bb3d8-126">Next steps</span></span>

<span data-ttu-id="bb3d8-127">Visitez [audit réseau sécurité groupes (NSG) avec l’Observateur réseau](network-watcher-nsg-auditing-powershell.md) toolearn comment tooautomate la validation de groupes de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="bb3d8-127">Visit [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md) toolearn how tooautomate validation of Network Security Groups.</span></span>

<span data-ttu-id="bb3d8-128">En savoir plus sur les règles de sécurité hello qui sont des ressources du réseau tooyour appliqué en vous rendant sur [présentation du mode de groupe de sécurité](network-watcher-security-group-view-overview.md)</span><span class="sxs-lookup"><span data-stu-id="bb3d8-128">Learn more about hello security rules that are applied tooyour network resources by visiting [Security group view overview](network-watcher-security-group-view-overview.md)</span></span>
