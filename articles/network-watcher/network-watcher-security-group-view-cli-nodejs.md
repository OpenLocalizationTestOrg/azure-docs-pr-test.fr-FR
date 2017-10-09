---
title: "sécurité du réseau aaaAnalyze avec vue groupe de sécurité dans Azure réseau Observateur - Azure CLI 1.0 | Documents Microsoft"
description: "Cet article décrit comment tooanalyze toouse Azure CLI 1.0 a virtual machines de sécurité avec l’affichage du groupe de sécurité."
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
ms.openlocfilehash: 96383a734b94d215d5b0f3d47339e46940d700b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-azure-cli-10"></a><span data-ttu-id="af0cd-103">Analyser la sécurité de votre machine virtuelle par le biais de la vue Groupe de sécurité dans Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="af0cd-103">Analyze your Virtual Machine security with Security Group View using Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="af0cd-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="af0cd-104">PowerShell</span></span>](network-watcher-security-group-view-powershell.md)
> - [<span data-ttu-id="af0cd-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="af0cd-105">CLI 1.0</span></span>](network-watcher-security-group-view-cli-nodejs.md)
> - [<span data-ttu-id="af0cd-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="af0cd-106">CLI 2.0</span></span>](network-watcher-security-group-view-cli.md)
> - [<span data-ttu-id="af0cd-107">API REST</span><span class="sxs-lookup"><span data-stu-id="af0cd-107">REST API</span></span>](network-watcher-security-group-view-rest.md)

<span data-ttu-id="af0cd-108">Affichage de groupe de sécurité retourne les règles de sécurité réseau configurée et efficace qui sont appliqués tooa l’ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="af0cd-108">Security group view returns configured and effective network security rules that are applied tooa virtual machine.</span></span> <span data-ttu-id="af0cd-109">Cette fonctionnalité est utile tooaudit et diagnostiquer les groupes de sécurité réseau et les règles qui sont configurés sur un trafic tooensure de machine virtuelle est correctement autorisé ou refusé.</span><span class="sxs-lookup"><span data-stu-id="af0cd-109">This capability is useful tooaudit and diagnose Network Security Groups and rules that are configured on a VM tooensure traffic is being correctly allowed or denied.</span></span> <span data-ttu-id="af0cd-110">Dans cet article, nous vous indiquons comment tooretrieve hello configuré et sécurité efficace règles tooa machine virtuelle Azure CLI</span><span class="sxs-lookup"><span data-stu-id="af0cd-110">In this article, we show you how tooretrieve hello configured and effective security rules tooa virtual machine using Azure CLI</span></span>

<span data-ttu-id="af0cd-111">Cet article utilise l’interface Azure CLI 1.0 interplateforme, disponible pour Windows, Mac et Linux.</span><span class="sxs-lookup"><span data-stu-id="af0cd-111">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="af0cd-112">Network Watcher utilise actuellement Azure CLI 1.0 pour la prise en charge d’interface CLI.</span><span class="sxs-lookup"><span data-stu-id="af0cd-112">Network Watcher currently uses Azure CLI 1.0 for CLI support.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="af0cd-113">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="af0cd-113">Before you begin</span></span>

<span data-ttu-id="af0cd-114">Ce scénario suppose que vous avez déjà suivi les étapes hello dans [créer un observateur réseau](network-watcher-create.md) toocreate un observateur réseau.</span><span class="sxs-lookup"><span data-stu-id="af0cd-114">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="af0cd-115">Scénario</span><span class="sxs-lookup"><span data-stu-id="af0cd-115">Scenario</span></span>

<span data-ttu-id="af0cd-116">scénario Hello abordée dans cet article récupère hello configuré et les règles de sécurité efficace pour un ordinateur virtuel donné.</span><span class="sxs-lookup"><span data-stu-id="af0cd-116">hello scenario covered in this article retrieves hello configured and effective security rules for a given virtual machine.</span></span>

## <a name="get-a-vm"></a><span data-ttu-id="af0cd-117">Obtenir une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="af0cd-117">Get a VM</span></span>

<span data-ttu-id="af0cd-118">Un ordinateur virtuel est requis toorun hello `vm list` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="af0cd-118">A virtual machine is required toorun hello `vm list` cmdlet.</span></span> <span data-ttu-id="af0cd-119">Hello commande suivante répertorie hello machinese virtuel dans un groupe de ressources :</span><span class="sxs-lookup"><span data-stu-id="af0cd-119">hello following command lists hello virtual machinese in a resource group:</span></span>

```azurecli
azure vm list -g resourceGroupName
```

<span data-ttu-id="af0cd-120">Une fois que vous connaissez hello virtual machine, vous pouvez utiliser hello `vm show` tooget de l’applet de commande son Id de ressource :</span><span class="sxs-lookup"><span data-stu-id="af0cd-120">Once you know hello virtual machine, you can use hello `vm show` cmdlet tooget its resource Id:</span></span>

```azurecli
azure vm show -g resourceGroupName -n virtualMachineName
```

## <a name="retrieve-security-group-view"></a><span data-ttu-id="af0cd-121">Récupérer la vue Groupe de sécurité</span><span class="sxs-lookup"><span data-stu-id="af0cd-121">Retrieve security group view</span></span>

<span data-ttu-id="af0cd-122">étape suivante de Hello est le résultat de vue du groupe de sécurité tooretrieve hello.</span><span class="sxs-lookup"><span data-stu-id="af0cd-122">hello next step is tooretrieve hello security group view result.</span></span> <span data-ttu-id="af0cd-123">Ajout de hello »--json « indicateur met en forme les résultats hello dans json.</span><span class="sxs-lookup"><span data-stu-id="af0cd-123">Adding hello "--json" flag will format hello results in json.</span></span>

```azurecli
azure network watcher security-group-view -g resourceGroupName -n networkWatcherName -t targetResourceId --json
```

## <a name="viewing-hello-results"></a><span data-ttu-id="af0cd-124">Affichage des résultats de hello</span><span class="sxs-lookup"><span data-stu-id="af0cd-124">Viewing hello results</span></span>

<span data-ttu-id="af0cd-125">Hello exemple suivant est une réponse raccourcie de hello les résultats retournés.</span><span class="sxs-lookup"><span data-stu-id="af0cd-125">hello following example is a shortened response of hello results returned.</span></span> <span data-ttu-id="af0cd-126">Hello résultats affichent toutes les règles de sécurité efficace et appliquées hello sur l’ordinateur virtuel de hello réparti dans les groupes **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, et  **EffectiveSecurityRules**.</span><span class="sxs-lookup"><span data-stu-id="af0cd-126">hello results show all hello effective and applied security rules on hello virtual machine broken down in groups of **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, and **EffectiveSecurityRules**.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="af0cd-127">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="af0cd-127">Next steps</span></span>

<span data-ttu-id="af0cd-128">Visitez [audit réseau sécurité groupes (NSG) avec l’Observateur réseau](network-watcher-nsg-auditing-powershell.md) toolearn comment tooautomate la validation de groupes de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="af0cd-128">Visit [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md) toolearn how tooautomate validation of Network Security Groups.</span></span>

<span data-ttu-id="af0cd-129">En savoir plus sur les règles de sécurité hello qui sont des ressources du réseau tooyour appliqué en vous rendant sur [présentation du mode de groupe de sécurité](network-watcher-security-group-view-overview.md)</span><span class="sxs-lookup"><span data-stu-id="af0cd-129">Learn more about hello security rules that are applied tooyour network resources by visiting [Security group view overview](network-watcher-security-group-view-overview.md)</span></span>
