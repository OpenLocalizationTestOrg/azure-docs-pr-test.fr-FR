---
title: "Analyser la sécurité réseau avec la vue Groupe de sécurité réseau Network Watcher - Azure CLI 1.0 | Microsoft Docs"
description: "Cet article décrit comment utiliser Azure CLI 1.0 pour analyser la sécurité des machines virtuelles par le biais de la vue Groupe de sécurité."
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
ms.openlocfilehash: 2c4c494dcc4fe1a85c5feb29506c35fb03066479
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-azure-cli-10"></a><span data-ttu-id="93563-103">Analyser la sécurité de votre machine virtuelle par le biais de la vue Groupe de sécurité dans Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="93563-103">Analyze your Virtual Machine security with Security Group View using Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="93563-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="93563-104">PowerShell</span></span>](network-watcher-security-group-view-powershell.md)
> - [<span data-ttu-id="93563-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="93563-105">CLI 1.0</span></span>](network-watcher-security-group-view-cli-nodejs.md)
> - [<span data-ttu-id="93563-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="93563-106">CLI 2.0</span></span>](network-watcher-security-group-view-cli.md)
> - [<span data-ttu-id="93563-107">API REST</span><span class="sxs-lookup"><span data-stu-id="93563-107">REST API</span></span>](network-watcher-security-group-view-rest.md)

<span data-ttu-id="93563-108">La vue Groupe de sécurité renvoie des règles de sécurité de réseau configurées et efficaces, appliquées à une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="93563-108">Security group view returns configured and effective network security rules that are applied to a virtual machine.</span></span> <span data-ttu-id="93563-109">Cette fonctionnalité permet d’auditer et de diagnostiquer les groupes de sécurité réseau ainsi que les règles configurées sur une machine virtuelle afin de garantir l’autorisation ou le refus appropriés du trafic.</span><span class="sxs-lookup"><span data-stu-id="93563-109">This capability is useful to audit and diagnose Network Security Groups and rules that are configured on a VM to ensure traffic is being correctly allowed or denied.</span></span> <span data-ttu-id="93563-110">Dans cet article, nous vous montrons comment récupérer des règles de sécurité configurées et efficaces pour une machine virtuelle à l’aide de l’interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="93563-110">In this article, we show you how to retrieve the configured and effective security rules to a virtual machine using Azure CLI</span></span>

<span data-ttu-id="93563-111">Cet article utilise l’interface Azure CLI 1.0 interplateforme, disponible pour Windows, Mac et Linux.</span><span class="sxs-lookup"><span data-stu-id="93563-111">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="93563-112">Network Watcher utilise actuellement Azure CLI 1.0 pour la prise en charge d’interface CLI.</span><span class="sxs-lookup"><span data-stu-id="93563-112">Network Watcher currently uses Azure CLI 1.0 for CLI support.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="93563-113">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="93563-113">Before you begin</span></span>

<span data-ttu-id="93563-114">Ce scénario suppose que vous ayez déjà suivi la procédure décrite dans [Create a Network Watcher (Créer une instance Network Watcher)](network-watcher-create.md) pour créer une instance Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="93563-114">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="93563-115">Scénario</span><span class="sxs-lookup"><span data-stu-id="93563-115">Scenario</span></span>

<span data-ttu-id="93563-116">Le scénario décrit dans cet article récupère des règles de sécurité configurées et efficaces pour une machine virtuelle donnée.</span><span class="sxs-lookup"><span data-stu-id="93563-116">The scenario covered in this article retrieves the configured and effective security rules for a given virtual machine.</span></span>

## <a name="get-a-vm"></a><span data-ttu-id="93563-117">Obtenir une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="93563-117">Get a VM</span></span>

<span data-ttu-id="93563-118">Une machine virtuelle est requise pour l’exécution de l’applet de commande `vm list`.</span><span class="sxs-lookup"><span data-stu-id="93563-118">A virtual machine is required to run the `vm list` cmdlet.</span></span> <span data-ttu-id="93563-119">La commande suivante répertorie les machines virtuelles dans un groupe de ressources :</span><span class="sxs-lookup"><span data-stu-id="93563-119">The following command lists the virtual machinese in a resource group:</span></span>

```azurecli
azure vm list -g resourceGroupName
```

<span data-ttu-id="93563-120">Une fois que vous connaissez la machine virtuelle, vous pouvez utiliser l’applet de commande `vm show` pour obtenir son identifiant de ressource :</span><span class="sxs-lookup"><span data-stu-id="93563-120">Once you know the virtual machine, you can use the `vm show` cmdlet to get its resource Id:</span></span>

```azurecli
azure vm show -g resourceGroupName -n virtualMachineName
```

## <a name="retrieve-security-group-view"></a><span data-ttu-id="93563-121">Récupérer la vue Groupe de sécurité</span><span class="sxs-lookup"><span data-stu-id="93563-121">Retrieve security group view</span></span>

<span data-ttu-id="93563-122">L’étape suivante consiste à récupérer le résultat de la vue Groupe de sécurité.</span><span class="sxs-lookup"><span data-stu-id="93563-122">The next step is to retrieve the security group view result.</span></span> <span data-ttu-id="93563-123">L’ajout de l’indicateur « --json » convertit les résultats au format json.</span><span class="sxs-lookup"><span data-stu-id="93563-123">Adding the "--json" flag will format the results in json.</span></span>

```azurecli
azure network watcher security-group-view -g resourceGroupName -n networkWatcherName -t targetResourceId --json
```

## <a name="viewing-the-results"></a><span data-ttu-id="93563-124">Affichage des résultats</span><span class="sxs-lookup"><span data-stu-id="93563-124">Viewing the results</span></span>

<span data-ttu-id="93563-125">L’exemple suivant est une réponse abrégée des résultats renvoyés.</span><span class="sxs-lookup"><span data-stu-id="93563-125">The following example is a shortened response of the results returned.</span></span> <span data-ttu-id="93563-126">Les résultats présentent toutes les règles de sécurité efficaces et appliquées sur la machine virtuelle, réparties en plusieurs groupes : **NetworkInterfaceSecurityRules**, **DefaultSecurityRules** et **EffectiveSecurityRules**.</span><span class="sxs-lookup"><span data-stu-id="93563-126">The results show all the effective and applied security rules on the virtual machine broken down in groups of **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, and **EffectiveSecurityRules**.</span></span>

```json
{
  "networkInterfaces": [
    {
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkInterfaces/testnic",
      "securityRuleAssociations": {
        "networkInterfaceAssociation": {
          "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkInterfaces/testvm",
          "securityRules": [
            {
              "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/test-nsg/securityRules/default-allow-rdp",
              "protocol": "TCP",
              "sourcePortRange": "*",
              "destinationPortRange": "3389",
              "sourceAddressPrefix": "*",
              "destinationAddressPrefix": "*",
              "access": "Allow",
              "priority": 1000,
              "direction": "Inbound",
              "provisioningState": "Succeeded",
              "name": "default-allow-rdp",
              "etag": "W/\"00000000-0000-0000-0000-000000000000\""
            }
          ]
        },
        "defaultSecurityRules": [
          {
            "id": "/subscriptions//resourceGroups//providers/Microsoft.Network/networkSecurityGroups//defaultSecurityRules/",
            "description": "Allow inbound traffic from all VMs in VNET",
            "protocol": "*",
            "sourcePortRange": "*",
            "destinationPortRange": "*",
            "sourceAddressPrefix": "VirtualNetwork",
            "destinationAddressPrefix": "VirtualNetwork",
            "access": "Allow",
            "priority": 65000,
            "direction": "Inbound",
            "provisioningState": "Succeeded",
            "name": "AllowVnetInBound"
          }
        ]
      }
    }
  ]
}
```

## <a name="next-steps"></a><span data-ttu-id="93563-127">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="93563-127">Next steps</span></span>

<span data-ttu-id="93563-128">Consultez la page [Auditing Network Security Groups (NSG) with Network Watcher (Audit des groupes de sécurité réseau avec Network Watcher)](network-watcher-nsg-auditing-powershell.md) pour découvrir comment automatiser la validation des groupes de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="93563-128">Visit [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md) to learn how to automate validation of Network Security Groups.</span></span>

<span data-ttu-id="93563-129">Pour en savoir plus sur les règles de sécurité appliquées à vos ressources réseau, consultez la page [Security group view overview (Vue d’ensemble de la vue Groupe de sécurité)](network-watcher-security-group-view-overview.md)</span><span class="sxs-lookup"><span data-stu-id="93563-129">Learn more about the security rules that are applied to your network resources by visiting [Security group view overview](network-watcher-security-group-view-overview.md)</span></span>
