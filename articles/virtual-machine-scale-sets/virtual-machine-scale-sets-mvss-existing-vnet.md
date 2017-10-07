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
# <a name="add-reference-tooan-existing-virtual-network-in-an-azure-scale-set-template"></a>Ajouter un réseau virtuel existant tooan de référence dans un modèle de jeu de mise à l’échelle Azure

Cet article explique comment toomodify hello [échelle viable minimale définie modèle](./virtual-machine-scale-sets-mvss-start.md) toodeploy dans un réseau virtuel existant au lieu de créer un nouveau.

## <a name="change-hello-template-definition"></a>Modifier la définition de modèle hello

Notre modèle de jeu minimale viable peut être consulté [ici](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), et notre modèle de déploiement de mise à l’échelle hello défini dans un réseau virtuel peut être affichée [ici](https://raw.githubusercontent.com/gatneil/mvss/existing-vnet/azuredeploy.json). Examinons hello diff utilisé toocreate ce modèle (`git diff minimum-viable-scale-set existing-vnet`) élément par élément :

Tout d’abord, nous ajoutons un paramètre `subnetId`. Cette chaîne est passée dans la configuration du jeu de mise à l’échelle hello, ce qui permet l’ensemble d’échelle de hello sous-réseau créés au préalable de hello tooidentify toodeploy les machines virtuelles en. Cette chaîne doit avoir la forme de hello : `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Network/virtualNetworks/<virtual-network-name>/subnets/<subnet-name>`. Par exemple, toodeploy hello où le surapprovisionnement dans un réseau virtuel existant avec le nom `myvnet`, sous-réseau `mysubnet`, groupe de ressources `myrg`et d’abonnement `00000000-0000-0000-0000-000000000000`, hello IDSousRéseau serait : `/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myrg/providers/Microsoft.Network/virtualNetworks/myvnet/subnets/mysubnet`.

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

Ensuite, nous pouvons supprimer la ressource de réseau virtuel hello de hello `resources` de tableau, dans la mesure où nous utilisent un réseau virtuel existant et que vous n’avez pas besoin toodeploy un nouveau.

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

réseau virtuel de Hello existe déjà avant le déploiement du modèle de hello, donc il n’existe aucun besoin toospecify une clause dependsOn à l’échelle de hello défini toohello des réseaux virtuels. Par conséquent, nous supprimons ces lignes :

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

Enfin, nous passons Bonjour `subnetId` paramètre défini par l’utilisateur de hello (au lieu d’utiliser `resourceId` id de hello tooget d’un réseau virtuel dans hello est du même déploiement, qui est le modèle de jeu de niveau viable minimale hello).

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




## <a name="next-steps"></a>Étapes suivantes

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
