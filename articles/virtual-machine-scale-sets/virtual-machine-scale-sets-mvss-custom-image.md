---
title: "Référencez une image personnalisée dans un modèle de groupe identique Azure | Microsoft Docs"
description: "Découvrez comment tooadd personnalisé de modèle d’ensemble d’échelle de Machine virtuelle Azure existante tooan l’image"
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
ms.date: 5/10/2017
ms.author: negat
ms.openlocfilehash: 6a17d989e44d241b460238c0106350c3ef038e56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-custom-image-tooan-azure-scale-set-template"></a>Ajouter qu'une image personnalisée de tooan Azure mise à l’échelle des ensembles de modèle

Cet article explique comment toomodify hello [échelle viable minimale définie modèle](./virtual-machine-scale-sets-mvss-start.md) toodeploy à partir d’une image personnalisée.

## <a name="change-hello-template-definition"></a>Modifier la définition de modèle hello

Notre modèle de jeu minimale viable peut être consulté [ici](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), et notre modèle de déploiement de mise à l’échelle hello définir à partir d’une image personnalisée peut être affichée [ici](https://raw.githubusercontent.com/gatneil/mvss/custom-image/azuredeploy.json). Examinons hello diff utilisé toocreate ce modèle (`git diff minimum-viable-scale-set custom-image`) élément par élément :

### <a name="creating-a-managed-disk-image"></a>Création d’une image de disque géré

Si vous disposez déjà d’une image disque gérée personnalisée (une ressource de type `Microsoft.Compute/images`), vous pouvez ignorer cette section.

Tout d’abord, nous ajoutons un `sourceImageVhdUri` paramètre hello URI toohello généralisé BLOB dans le stockage Azure qui contient toodeploy d’image personnalisée hello à partir de.


```diff
     },
     "adminPassword": {
       "type": "securestring"
+    },
+    "sourceImageVhdUri": {
+      "type": "string",
+      "metadata": {
+        "description": "hello source of hello generalized blob containing hello custom image"
+      }
     }
   },
   "variables": {},
```

Ensuite, nous ajoutons une ressource de type `Microsoft.Compute/images`, qui est un format d’image de disque géré de hello est basée sur des blob hello généralisé à l’URI `sourceImageVhdUri`. Cette image doit être Bonjour même région que l’ensemble d’échelle hello qui l’utilise. Dans Propriétés de hello d’image de hello, nous spécifions type hello du système d’exploitation, emplacement hello d’objet blob de hello (à partir de hello `sourceImageVhdUri` paramètre) et le type de compte de stockage hello :

```diff
   "resources": [
     {
+      "type": "Microsoft.Compute/images",
+      "apiVersion": "2016-04-30-preview",
+      "name": "myCustomImage",
+      "location": "[resourceGroup().location]",
+      "properties": {
+        "storageProfile": {
+          "osDisk": {
+            "osType": "Linux",
+            "osState": "Generalized",
+            "blobUri": "[parameters('sourceImageVhdUri')]",
+            "storageAccountType": "Standard_LRS"
+          }
+        }
+      }
+    },
+    {
       "type": "Microsoft.Network/virtualNetworks",
       "name": "myVnet",
       "location": "[resourceGroup().location]",

```

Bonjour ensemble d’échelle de ressources, nous ajoutons un `dependsOn` clause toomake d’image personnalisée toohello que l’image de hello est créé avant que l’ensemble d’échelle hello tente toodeploy à partir de cette image de référence :

```diff
       "location": "[resourceGroup().location]",
       "apiVersion": "2016-04-30-preview",
       "dependsOn": [
-        "Microsoft.Network/virtualNetworks/myVnet"
+        "Microsoft.Network/virtualNetworks/myVnet",
+        "Microsoft.Compute/images/myCustomImage"
       ],
       "sku": {
         "name": "Standard_A1",

```

### <a name="changing-scale-set-properties-toouse-hello-managed-disk-image"></a>Modification de l’échelle de jeu d’image de disque géré propriétés toouse hello

Bonjour `imageReference` de montée en puissance hello `storageProfile`, au lieu de spécifier le serveur de publication hello, offre, référence (SKU) et la version d’une image de plateforme, nous spécifions hello `id` Hello `Microsoft.Compute/images` ressource :

```diff
         "virtualMachineProfile": {
           "storageProfile": {
             "imageReference": {
-              "publisher": "Canonical",
-              "offer": "UbuntuServer",
-              "sku": "16.04-LTS",
-              "version": "latest"
+              "id": "[resourceId('Microsoft.Compute/images', 'myCustomImage')]"
             }
           },
           "osProfile": {
```

Dans cet exemple, nous utilisons hello `resourceId` ID de ressource de fonction tooget hello d’image de hello créées Bonjour même modèle. Si vous avez créé les images de disque géré hello au préalable, vous devez fournir les id hello de cette image à la place. Cet id doit être sous forme de hello : `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Compute/images/<image-name>`.


## <a name="next-steps"></a>Étapes suivantes

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
