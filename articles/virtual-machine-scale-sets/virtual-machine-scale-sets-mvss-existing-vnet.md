---
title: "Référencer un réseau virtuel existant dans un modèle de groupe identique Azure | Microsoft Docs"
description: "Découvrez le modèle d’ensemble d’échelle de Machine virtuelle Azure existante tooan réseau tooadd un virtuel"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: negat
ms.openlocfilehash: c3034b577e17abc4643dc26d7c38ad643fa26322
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-reference-tooan-existing-virtual-network-in-an-azure-scale-set-template"></a><span data-ttu-id="7ec61-103">Ajouter un réseau virtuel existant tooan de référence dans un modèle de jeu de mise à l’échelle Azure</span><span class="sxs-lookup"><span data-stu-id="7ec61-103">Add reference tooan existing virtual network in an Azure scale set template</span></span>

<span data-ttu-id="7ec61-104">Cet article explique comment toomodify hello [échelle viable minimale définie modèle](./virtual-machine-scale-sets-mvss-start.md) toodeploy dans un réseau virtuel existant au lieu de créer un nouveau.</span><span class="sxs-lookup"><span data-stu-id="7ec61-104">This article shows how toomodify hello [minimum viable scale set template](./virtual-machine-scale-sets-mvss-start.md) toodeploy into an existing virtual network instead of creating a new one.</span></span>

## <a name="change-hello-template-definition"></a><span data-ttu-id="7ec61-105">Modifier la définition de modèle hello</span><span class="sxs-lookup"><span data-stu-id="7ec61-105">Change hello template definition</span></span>

<span data-ttu-id="7ec61-106">Notre modèle de jeu minimale viable peut être consulté [ici](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), et notre modèle de déploiement de mise à l’échelle hello défini dans un réseau virtuel peut être affichée [ici](https://raw.githubusercontent.com/gatneil/mvss/existing-vnet/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="7ec61-106">Our minimum viable scale set template can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), and our template for deploying hello scale set into an existing virtual network can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/existing-vnet/azuredeploy.json).</span></span> <span data-ttu-id="7ec61-107">Examinons hello diff utilisé toocreate ce modèle (`git diff minimum-viable-scale-set existing-vnet`) élément par élément :</span><span class="sxs-lookup"><span data-stu-id="7ec61-107">Let's examine hello diff used toocreate this template (`git diff minimum-viable-scale-set existing-vnet`) piece by piece:</span></span>

<span data-ttu-id="7ec61-108">Tout d’abord, nous ajoutons un paramètre `subnetId`.</span><span class="sxs-lookup"><span data-stu-id="7ec61-108">First, we add a `subnetId` parameter.</span></span> <span data-ttu-id="7ec61-109">Cette chaîne est passée dans la configuration du jeu de mise à l’échelle hello, ce qui permet l’ensemble d’échelle de hello sous-réseau créés au préalable de hello tooidentify toodeploy les machines virtuelles en.</span><span class="sxs-lookup"><span data-stu-id="7ec61-109">This string will be passed into hello scale set configuration, allowing hello scale set tooidentify hello pre-created subnet toodeploy virtual machines into.</span></span> <span data-ttu-id="7ec61-110">Cette chaîne doit avoir la forme de hello : `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Network/virtualNetworks/<virtual-network-name>/subnets/<subnet-name>`.</span><span class="sxs-lookup"><span data-stu-id="7ec61-110">This string must be of hello form: `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Network/virtualNetworks/<virtual-network-name>/subnets/<subnet-name>`.</span></span> <span data-ttu-id="7ec61-111">Par exemple, toodeploy hello où le surapprovisionnement dans un réseau virtuel existant avec le nom `myvnet`, sous-réseau `mysubnet`, groupe de ressources `myrg`et d’abonnement `00000000-0000-0000-0000-000000000000`, hello IDSousRéseau serait : `/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myrg/providers/Microsoft.Network/virtualNetworks/myvnet/subnets/mysubnet`.</span><span class="sxs-lookup"><span data-stu-id="7ec61-111">For instance, toodeploy hello scale set into an existing virtual network with name `myvnet`, subnet `mysubnet`, resource group `myrg`, and subscription `00000000-0000-0000-0000-000000000000`, hello subnetId would be: `/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myrg/providers/Microsoft.Network/virtualNetworks/myvnet/subnets/mysubnet`.</span></span>

```diff
     },
     "adminPassword": {
       "type": "securestring"
+    },
+    "subnetId": {
+      "type": "string"
     }
   },
```

<span data-ttu-id="7ec61-112">Ensuite, nous pouvons supprimer la ressource de réseau virtuel hello de hello `resources` de tableau, dans la mesure où nous utilisent un réseau virtuel existant et que vous n’avez pas besoin toodeploy un nouveau.</span><span class="sxs-lookup"><span data-stu-id="7ec61-112">Next, we can delete hello virtual network resource from hello `resources` array, since we are using an existing virtual network and don't need toodeploy a new one.</span></span>

```diff
   "variables": {},
   "resources": [
-    {
-      "type": "Microsoft.Network/virtualNetworks",
-      "name": "myVnet",
-      "location": "[resourceGroup().location]",
-      "apiVersion": "2016-12-01",
-      "properties": {
-        "addressSpace": {
-          "addressPrefixes": [
-            "10.0.0.0/16"
-          ]
-        },
-        "subnets": [
-          {
-            "name": "mySubnet",
-            "properties": {
-              "addressPrefix": "10.0.0.0/16"
-            }
-          }
-        ]
-      }
-    },
```

<span data-ttu-id="7ec61-113">réseau virtuel de Hello existe déjà avant le déploiement du modèle de hello, donc il n’existe aucun besoin toospecify une clause dependsOn à l’échelle de hello défini toohello des réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="7ec61-113">hello virtual network already exists before hello template is deployed, so there is no need toospecify a dependsOn clause from hello scale set toohello virtual network.</span></span> <span data-ttu-id="7ec61-114">Par conséquent, nous supprimons ces lignes :</span><span class="sxs-lookup"><span data-stu-id="7ec61-114">Thus, we delete these lines:</span></span>

```diff
     {
       "type": "Microsoft.Compute/virtualMachineScaleSets",
       "name": "myScaleSet",
       "location": "[resourceGroup().location]",
       "apiVersion": "2016-04-30-preview",
-      "dependsOn": [
-        "Microsoft.Network/virtualNetworks/myVnet"
-      ],
       "sku": {
         "name": "Standard_A1",
         "capacity": 2
```

<span data-ttu-id="7ec61-115">Enfin, nous passons Bonjour `subnetId` paramètre défini par l’utilisateur de hello (au lieu d’utiliser `resourceId` id de hello tooget d’un réseau virtuel dans hello est du même déploiement, qui est le modèle de jeu de niveau viable minimale hello).</span><span class="sxs-lookup"><span data-stu-id="7ec61-115">Finally, we pass in hello `subnetId` parameter set by hello user (instead of using `resourceId` tooget hello id of a vnet in hello same deployment, which is what hello minimum viable scale set template does).</span></span>

```diff
                       "name": "myIpConfig",
                       "properties": {
                         "subnet": {
-                          "id": "[concat(resourceId('Microsoft.Network/virtualNetworks', 'myVnet'), '/subnets/mySubnet')]"
+                          "id": "[parameters('subnetId')]"
                         }
                       }
                     }
```




## <a name="next-steps"></a><span data-ttu-id="7ec61-116">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7ec61-116">Next steps</span></span>

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
