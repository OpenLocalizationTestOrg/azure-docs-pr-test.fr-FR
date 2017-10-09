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
# <a name="add-a-custom-image-tooan-azure-scale-set-template"></a><span data-ttu-id="bcbcb-103">Ajouter qu'une image personnalisée de tooan Azure mise à l’échelle des ensembles de modèle</span><span class="sxs-lookup"><span data-stu-id="bcbcb-103">Add a custom image tooan Azure scale set template</span></span>

<span data-ttu-id="bcbcb-104">Cet article explique comment toomodify hello [échelle viable minimale définie modèle](./virtual-machine-scale-sets-mvss-start.md) toodeploy à partir d’une image personnalisée.</span><span class="sxs-lookup"><span data-stu-id="bcbcb-104">This article shows how toomodify hello [minimum viable scale set template](./virtual-machine-scale-sets-mvss-start.md) toodeploy from custom image.</span></span>

## <a name="change-hello-template-definition"></a><span data-ttu-id="bcbcb-105">Modifier la définition de modèle hello</span><span class="sxs-lookup"><span data-stu-id="bcbcb-105">Change hello template definition</span></span>

<span data-ttu-id="bcbcb-106">Notre modèle de jeu minimale viable peut être consulté [ici](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), et notre modèle de déploiement de mise à l’échelle hello définir à partir d’une image personnalisée peut être affichée [ici](https://raw.githubusercontent.com/gatneil/mvss/custom-image/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="bcbcb-106">Our minimum viable scale set template can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), and our template for deploying hello scale set from a custom image can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/custom-image/azuredeploy.json).</span></span> <span data-ttu-id="bcbcb-107">Examinons hello diff utilisé toocreate ce modèle (`git diff minimum-viable-scale-set custom-image`) élément par élément :</span><span class="sxs-lookup"><span data-stu-id="bcbcb-107">Let's examine hello diff used toocreate this template (`git diff minimum-viable-scale-set custom-image`) piece by piece:</span></span>

### <a name="creating-a-managed-disk-image"></a><span data-ttu-id="bcbcb-108">Création d’une image de disque géré</span><span class="sxs-lookup"><span data-stu-id="bcbcb-108">Creating a managed disk image</span></span>

<span data-ttu-id="bcbcb-109">Si vous disposez déjà d’une image disque gérée personnalisée (une ressource de type `Microsoft.Compute/images`), vous pouvez ignorer cette section.</span><span class="sxs-lookup"><span data-stu-id="bcbcb-109">If you already have a custom managed disk image (a resource of type `Microsoft.Compute/images`), then you can skip this section.</span></span>

<span data-ttu-id="bcbcb-110">Tout d’abord, nous ajoutons un `sourceImageVhdUri` paramètre hello URI toohello généralisé BLOB dans le stockage Azure qui contient toodeploy d’image personnalisée hello à partir de.</span><span class="sxs-lookup"><span data-stu-id="bcbcb-110">First, we add a `sourceImageVhdUri` parameter, which is hello URI toohello generalized blob in Azure Storage that contains hello custom image toodeploy from.</span></span>


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

<span data-ttu-id="bcbcb-111">Ensuite, nous ajoutons une ressource de type `Microsoft.Compute/images`, qui est un format d’image de disque géré de hello est basée sur des blob hello généralisé à l’URI `sourceImageVhdUri`.</span><span class="sxs-lookup"><span data-stu-id="bcbcb-111">Next, we add a resource of type `Microsoft.Compute/images`, which is hello managed disk image based on hello generalized blob located at URI `sourceImageVhdUri`.</span></span> <span data-ttu-id="bcbcb-112">Cette image doit être Bonjour même région que l’ensemble d’échelle hello qui l’utilise.</span><span class="sxs-lookup"><span data-stu-id="bcbcb-112">This image must be in hello same region as hello scale set that uses it.</span></span> <span data-ttu-id="bcbcb-113">Dans Propriétés de hello d’image de hello, nous spécifions type hello du système d’exploitation, emplacement hello d’objet blob de hello (à partir de hello `sourceImageVhdUri` paramètre) et le type de compte de stockage hello :</span><span class="sxs-lookup"><span data-stu-id="bcbcb-113">In hello properties of hello image, we specify hello OS type, hello location of hello blob (from hello `sourceImageVhdUri` parameter), and hello storage account type:</span></span>

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

<span data-ttu-id="bcbcb-114">Bonjour ensemble d’échelle de ressources, nous ajoutons un `dependsOn` clause toomake d’image personnalisée toohello que l’image de hello est créé avant que l’ensemble d’échelle hello tente toodeploy à partir de cette image de référence :</span><span class="sxs-lookup"><span data-stu-id="bcbcb-114">In hello scale set resource, we add a `dependsOn` clause referring toohello custom image toomake sure hello image gets created before hello scale set tries toodeploy from that image:</span></span>

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

### <a name="changing-scale-set-properties-toouse-hello-managed-disk-image"></a><span data-ttu-id="bcbcb-115">Modification de l’échelle de jeu d’image de disque géré propriétés toouse hello</span><span class="sxs-lookup"><span data-stu-id="bcbcb-115">Changing scale set properties toouse hello managed disk image</span></span>

<span data-ttu-id="bcbcb-116">Bonjour `imageReference` de montée en puissance hello `storageProfile`, au lieu de spécifier le serveur de publication hello, offre, référence (SKU) et la version d’une image de plateforme, nous spécifions hello `id` Hello `Microsoft.Compute/images` ressource :</span><span class="sxs-lookup"><span data-stu-id="bcbcb-116">In hello `imageReference` of hello scale set `storageProfile`, instead of specifying hello publisher, offer, sku, and version of a platform image, we specify hello `id` of hello `Microsoft.Compute/images` resource:</span></span>

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

<span data-ttu-id="bcbcb-117">Dans cet exemple, nous utilisons hello `resourceId` ID de ressource de fonction tooget hello d’image de hello créées Bonjour même modèle.</span><span class="sxs-lookup"><span data-stu-id="bcbcb-117">In this example, we use hello `resourceId` function tooget hello resource ID of hello image created in hello same template.</span></span> <span data-ttu-id="bcbcb-118">Si vous avez créé les images de disque géré hello au préalable, vous devez fournir les id hello de cette image à la place.</span><span class="sxs-lookup"><span data-stu-id="bcbcb-118">If you have created hello managed disk image beforehand, you should provide hello id of that image instead.</span></span> <span data-ttu-id="bcbcb-119">Cet id doit être sous forme de hello : `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Compute/images/<image-name>`.</span><span class="sxs-lookup"><span data-stu-id="bcbcb-119">This id must be of hello form: `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Compute/images/<image-name>`.</span></span>


## <a name="next-steps"></a><span data-ttu-id="bcbcb-120">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bcbcb-120">Next Steps</span></span>

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
