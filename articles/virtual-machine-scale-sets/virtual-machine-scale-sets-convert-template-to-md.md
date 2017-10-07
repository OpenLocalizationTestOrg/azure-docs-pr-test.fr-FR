---
title: "aaaConvert une échelle Azure Resource Manager définie disque géré de modèle toouse | Documents Microsoft"
description: "Convertir un modèle de mise à l’échelle ensemble modèle tooa disque géré échelle jeu."
keywords: "Jeux de mise à l’échelle de machine virtuelle"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: madhana
editor: tysonn
tags: azure-resource-manager
ms.assetid: bc8c377a-8c3f-45b8-8b2d-acc2d6d0b1e8
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 5/18/2017
ms.author: negat
ms.openlocfilehash: 66c2217647e57ed2cfa39660c0175710ae2e63be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="convert-a-scale-set-template-tooa-managed-disk-scale-set-template"></a><span data-ttu-id="d04b2-104">Convertir un modèle de mise à l’échelle ensemble modèle tooa disque géré échelle jeu</span><span class="sxs-lookup"><span data-stu-id="d04b2-104">Convert a scale set template tooa managed disk scale set template</span></span>

<span data-ttu-id="d04b2-105">Clients avec un modèle de gestionnaire de ressources pour la création d’une échelle ne pas à l’aide de disque géré souhaitiez toomodify il toouse gérés disque.</span><span class="sxs-lookup"><span data-stu-id="d04b2-105">Customers with a Resource Manager template for creating a scale set not using managed disk may wish toomodify it toouse managed disk.</span></span> <span data-ttu-id="d04b2-106">Cet article explique comment toodo ce, en utilisant par exemple une requête d’extraction à partir de hello [modèles de démarrage rapide Azure](https://github.com/Azure/azure-quickstart-templates), un référentiel communautaire pour des exemples de modèles de gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="d04b2-106">This article shows how toodo this, using as an example a pull request from hello [Azure Quickstart Templates](https://github.com/Azure/azure-quickstart-templates), a community-driven repo for sample Resource Manager templates.</span></span> <span data-ttu-id="d04b2-107">requête de tirage complète de Hello peut être consulté ici : [https://github.com/Azure/azure-quickstart-templates/pull/2998](https://github.com/Azure/azure-quickstart-templates/pull/2998), et hello les parties pertinentes de hello diff ci-dessous, ainsi que des explications :</span><span class="sxs-lookup"><span data-stu-id="d04b2-107">hello full pull request can be seen here: [https://github.com/Azure/azure-quickstart-templates/pull/2998](https://github.com/Azure/azure-quickstart-templates/pull/2998), and hello relevant parts of hello diff are below, along with explanations:</span></span>

## <a name="making-hello-os-disks-managed"></a><span data-ttu-id="d04b2-108">Rendre les disques du système d’exploitation hello gérés</span><span class="sxs-lookup"><span data-stu-id="d04b2-108">Making hello OS disks managed</span></span>

<span data-ttu-id="d04b2-109">Dans la comparaison de hello ci-dessous, nous constatons que nous avons supprimé plusieurs variables connexes toostorage disque propriétés du compte et.</span><span class="sxs-lookup"><span data-stu-id="d04b2-109">In hello diff below, we can see that we have removed several variables related toostorage account and disk properties.</span></span> <span data-ttu-id="d04b2-110">Type de compte de stockage n’est plus nécessaire (Standard_LRS est la valeur par défaut hello), mais nous avons toujours spécifier s’il veut.</span><span class="sxs-lookup"><span data-stu-id="d04b2-110">Storage account type is no longer necessary (Standard_LRS is hello default), but we could still specify it if we wished to.</span></span> <span data-ttu-id="d04b2-111">Seuls Standard_LRS et Premium_LRS sont pris en charge pour les disques gérés.</span><span class="sxs-lookup"><span data-stu-id="d04b2-111">Only Standard_LRS and Premium_LRS are supported with managed disk.</span></span> <span data-ttu-id="d04b2-112">Nouveau suffixe de compte de stockage, tableau de chaînes uniques et le nombre d’association de sécurité ont été utilisés dans les noms de compte hello ancien modèle toogenerate stockage.</span><span class="sxs-lookup"><span data-stu-id="d04b2-112">New storage account suffix, unique string array, and sa count were used in hello old template toogenerate storage account names.</span></span> <span data-ttu-id="d04b2-113">Ces variables ne sont plus nécessaires dans le nouveau modèle de hello, car le disque géré crée automatiquement des comptes de stockage sur le compte du client hello.</span><span class="sxs-lookup"><span data-stu-id="d04b2-113">These variables are no longer necessary in hello new template because managed disk automatically creates storage accounts on hello customer's behalf.</span></span> <span data-ttu-id="d04b2-114">De même, nom de conteneur de disque dur virtuel et le nom du disque du système d’exploitation ne sont plus nécessaires, car le disque géré nomme automatiquement les disques et les conteneurs d’objets blob de stockage sous-jacent hello.</span><span class="sxs-lookup"><span data-stu-id="d04b2-114">Similarly, vhd container name and os disk name are no longer necessary because managed disk automatically names hello underlying storage blob containers and disks.</span></span>

```diff
   "variables": {
-    "storageAccountType": "Standard_LRS",
     "namingInfix": "[toLower(substring(concat(parameters('vmssName'), uniqueString(resourceGroup().id)), 0, 9))]",
     "longNamingInfix": "[toLower(parameters('vmssName'))]",
-    "newStorageAccountSuffix": "[concat(variables('namingInfix'), 'sa')]",
-    "uniqueStringArray": [
-      "[concat(uniqueString(concat(resourceGroup().id, variables('newStorageAccountSuffix'), '0')))]",
-      "[concat(uniqueString(concat(resourceGroup().id, variables('newStorageAccountSuffix'), '1')))]",
-      "[concat(uniqueString(concat(resourceGroup().id, variables('newStorageAccountSuffix'), '2')))]",
-      "[concat(uniqueString(concat(resourceGroup().id, variables('newStorageAccountSuffix'), '3')))]",
-      "[concat(uniqueString(concat(resourceGroup().id, variables('newStorageAccountSuffix'), '4')))]"
-    ],
-    "saCount": "[length(variables('uniqueStringArray'))]",
-    "vhdContainerName": "[concat(variables('namingInfix'), 'vhd')]",
-    "osDiskName": "[concat(variables('namingInfix'), 'osdisk')]",
     "addressPrefix": "10.0.0.0/16",
     "subnetPrefix": "10.0.0.0/24",
     "virtualNetworkName": "[concat(variables('namingInfix'), 'vnet')]",
```


<span data-ttu-id="d04b2-115">Dans diff hello ci-dessous, nous peut voir que nous avons mis à jour hello de calcul api version too2016-04-30-preview, qui est hello plus ancienne version requise pour la prise en charge de disque géré avec des jeux de mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="d04b2-115">In hello diff below, we can see that we updated hello compute api version too2016-04-30-preview, which is hello earliest required version for managed disk support with scale sets.</span></span> <span data-ttu-id="d04b2-116">Notez que nous avons toujours utiliser des disques non managés dans la nouvelle version d’api hello avec l’ancienne syntaxe de hello si vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="d04b2-116">Note that we could still use unmanaged disks in hello new api version with hello old syntax if desired.</span></span> <span data-ttu-id="d04b2-117">En d’autres termes, si uniquement mettre à jour hello version de l’api de calcul et ne modifiez rien d’autre, modèle de hello doit continuer toowork comme avant.</span><span class="sxs-lookup"><span data-stu-id="d04b2-117">In other words, if we only update hello compute api version and don't change anything else, hello template should continue toowork as before.</span></span>

```diff
@@ -86,7 +74,7 @@
       "version": "latest"
     },
     "imageReference": "[variables('osType')]",
-    "computeApiVersion": "2016-03-30",
+    "computeApiVersion": "2016-04-30-preview",
     "networkApiVersion": "2016-03-30",
     "storageApiVersion": "2015-06-15"
   },
```

<span data-ttu-id="d04b2-118">Dans la comparaison de hello ci-dessous, nous constatons que nous allons supprimer des ressources de compte de stockage hello du tableau des ressources hello complètement.</span><span class="sxs-lookup"><span data-stu-id="d04b2-118">In hello diff below, we can see that we are removing hello storage account resource from hello resources array completely.</span></span> <span data-ttu-id="d04b2-119">Nous n’en avons plus besoin, car le disque géré les crée automatiquement en notre nom.</span><span class="sxs-lookup"><span data-stu-id="d04b2-119">We no longer need them since managed disk creates them automatically on our behalf.</span></span>

```diff
@@ -113,19 +101,6 @@
       }
     },
-    {
-      "type": "Microsoft.Storage/storageAccounts",
-      "name": "[concat(variables('uniqueStringArray')[copyIndex()], variables('newStorageAccountSuffix'))]",
-      "location": "[resourceGroup().location]",
-      "apiVersion": "[variables('storageApiVersion')]",
-      "copy": {
-        "name": "storageLoop",
-        "count": "[variables('saCount')]"
-      },
-      "properties": {
-        "accountType": "[variables('storageAccountType')]"
-      }
-    },
     {
       "type": "Microsoft.Network/publicIPAddresses",
       "name": "[variables('publicIPAddressName')]",
       "location": "[resourceGroup().location]",
```

<span data-ttu-id="d04b2-120">Dans diff hello ci-dessous, nous peut voir que nous allons supprimer hello dépend clause faisant référence à partir de hello échelle ensemble toohello boucle qui créait des comptes de stockage.</span><span class="sxs-lookup"><span data-stu-id="d04b2-120">In hello diff below, we can see that we are removing hello depends on clause referring from hello scale set toohello loop that was creating storage accounts.</span></span> <span data-ttu-id="d04b2-121">Dans l’ancien modèle de hello, cela a été de vous assurer que les comptes de stockage hello ont été créés avant l’ensemble d’échelle hello a commencé la création, mais cette clause n’est plus nécessaire avec disque géré.</span><span class="sxs-lookup"><span data-stu-id="d04b2-121">In hello old template, this was ensuring that hello storage accounts were created before hello scale set began creation, but this clause is no longer necessary with managed disk.</span></span> <span data-ttu-id="d04b2-122">Nous également supprimer la propriété de conteneurs de disque dur virtuel hello et hello la propriété de nom de disque de système d’exploitation que ces propriétés sont gérées automatiquement dans les coulisses de hello par disque géré.</span><span class="sxs-lookup"><span data-stu-id="d04b2-122">We also remove hello vhd containers property, and hello os disk name property as these properties are automatically handled under hello hood by managed disk.</span></span> <span data-ttu-id="d04b2-123">Si nous souhaité, nous pouvons ajouter `"managedDisk": { "storageAccountType": "Premium_LRS" }` dans la configuration de « osDisk » hello si nous voulions les disques premium du système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="d04b2-123">If we wished, we could add `"managedDisk": { "storageAccountType": "Premium_LRS" }` in hello "osDisk" configuration if we wanted premium OS disks.</span></span> <span data-ttu-id="d04b2-124">Uniquement les ordinateurs virtuels avec une majuscule ou de minuscule « Bonjour VM référence (SKU) pouvez utiliser des disques premium.</span><span class="sxs-lookup"><span data-stu-id="d04b2-124">Only VMs with an uppercase or lowercase 's' in hello VM sku can use premium disks.</span></span>

```diff
@@ -183,7 +158,6 @@
       "location": "[resourceGroup().location]",
       "apiVersion": "[variables('computeApiVersion')]",
       "dependsOn": [
-        "storageLoop",
         "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]",
         "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
       ],
@@ -200,16 +174,8 @@
         "virtualMachineProfile": {
           "storageProfile": {
             "osDisk": {
-              "vhdContainers": [
-                "[concat('https://', variables('uniqueStringArray')[0], variables('newStorageAccountSuffix'), '.blob.core.windows.net/', variables('vhdContainerName'))]",
-                "[concat('https://', variables('uniqueStringArray')[1], variables('newStorageAccountSuffix'), '.blob.core.windows.net/', variables('vhdContainerName'))]",
-                "[concat('https://', variables('uniqueStringArray')[2], variables('newStorageAccountSuffix'), '.blob.core.windows.net/', variables('vhdContainerName'))]",
-                "[concat('https://', variables('uniqueStringArray')[3], variables('newStorageAccountSuffix'), '.blob.core.windows.net/', variables('vhdContainerName'))]",
-                "[concat('https://', variables('uniqueStringArray')[4], variables('newStorageAccountSuffix'), '.blob.core.windows.net/', variables('vhdContainerName'))]"
-              ],
-              "name": "[variables('osDiskName')]",
             },
             "imageReference": "[variables('imageReference')]"
           },

```

<span data-ttu-id="d04b2-125">Il n’existe aucune propriété explicite dans la configuration de jeu hello mise à l’échelle pour que toouse géré ou un disque non managé.</span><span class="sxs-lookup"><span data-stu-id="d04b2-125">There is no explicit property in hello scale set configuration for whether toouse managed or unmanaged disk.</span></span> <span data-ttu-id="d04b2-126">ensemble d’échelle Hello sait quelle toouse basé sur les propriétés hello qui sont présentes dans le profil de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="d04b2-126">hello scale set knows which toouse based on hello properties that are present in hello storage profile.</span></span> <span data-ttu-id="d04b2-127">Par conséquent, il est important lorsque vous modifiez hello modèle tooensure qui sont des propriétés du droit de hello dans le profil de stockage hello de hello ensemble d’échelle.</span><span class="sxs-lookup"><span data-stu-id="d04b2-127">Thus, it is important when modifying hello template tooensure that hello right properties are in hello storage profile of hello scale set.</span></span>


## <a name="data-disks"></a><span data-ttu-id="d04b2-128">Disques de données</span><span class="sxs-lookup"><span data-stu-id="d04b2-128">Data disks</span></span>

<span data-ttu-id="d04b2-129">Modifications de hello ci-dessus, hello échelle ensemble utilise des disques gérés pour hello du système d’exploitation sur le disque, mais qu’en est-il des disques de données ? tooadd des disques de données, ajouter la propriété de « dataDisks » hello sous « storageProfile » au même niveau en tant que « osDisk » de hello.</span><span class="sxs-lookup"><span data-stu-id="d04b2-129">With hello changes above, hello scale set uses managed disks for hello OS disk, but what about data disks? tooadd data disks, add hello "dataDisks" property under "storageProfile" at hello same level as "osDisk".</span></span> <span data-ttu-id="d04b2-130">valeur de propriété de hello Hello est une liste JSON d’objets, chacun d’eux possède des propriétés « numéro d’unité logique » (qui doit être unique pour chaque disque de données sur une machine virtuelle), « createOption » (« empty » est actuellement hello uniquement l’option prise en charge) et « diskSizeGB » (taille du disque hello en gigaoctets de hello ; doit être supérieur à 0 et inférieurs à 1024) comme dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="d04b2-130">hello value of hello property is a JSON list of objects, each of which has properties "lun" (which must be unique per data disk on a VM), "createOption" ("empty" is currently hello only supported option), and "diskSizeGB" (hello size of hello disk in gigabytes; must be greater than 0 and less than 1024) as in hello following example:</span></span> 

```
"dataDisks": [
  {
    "lun": "1",
    "createOption": "empty",
    "diskSizeGB": "1023"
  }
]
```

<span data-ttu-id="d04b2-131">Si vous spécifiez `n` disques dans ce tableau, chaque ordinateur virtuel dans l’échelle de hello définie Obtient `n` disques de données.</span><span class="sxs-lookup"><span data-stu-id="d04b2-131">If you specify `n` disks in this array, each VM in hello scale set gets `n` data disks.</span></span> <span data-ttu-id="d04b2-132">Notez, cependant, que ces disques de données sont des appareils bruts.</span><span class="sxs-lookup"><span data-stu-id="d04b2-132">Do note, however, that these data disks are raw devices.</span></span> <span data-ttu-id="d04b2-133">Ils ne sont pas formatés.</span><span class="sxs-lookup"><span data-stu-id="d04b2-133">They are not formatted.</span></span> <span data-ttu-id="d04b2-134">C’est toohello client tooattach, partition et les disques au format hello avant de les utiliser.</span><span class="sxs-lookup"><span data-stu-id="d04b2-134">It is up toohello customer tooattach, paritition, and format hello disks before using them.</span></span> <span data-ttu-id="d04b2-135">Si vous le souhaitez, nous pouvons également spécifier `"managedDisk": { "storageAccountType": "Premium_LRS" }` dans chaque toospecify objet de disque de données qu’il doit être un disque de données premium.</span><span class="sxs-lookup"><span data-stu-id="d04b2-135">Optionally, we could also specify `"managedDisk": { "storageAccountType": "Premium_LRS" }` in each data disk object toospecify that it should be a premium data disk.</span></span> <span data-ttu-id="d04b2-136">Uniquement les ordinateurs virtuels avec une majuscule ou de minuscule « Bonjour VM référence (SKU) pouvez utiliser des disques premium.</span><span class="sxs-lookup"><span data-stu-id="d04b2-136">Only VMs with an uppercase or lowercase 's' in hello VM sku can use premium disks.</span></span>

<span data-ttu-id="d04b2-137">toolearn savoir plus sur à l’aide de disques de données avec montée en puissance des jeux, consultez [cet article](./virtual-machine-scale-sets-attached-disks.md).</span><span class="sxs-lookup"><span data-stu-id="d04b2-137">toolearn more about using data disks with scale sets, see [this article](./virtual-machine-scale-sets-attached-disks.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="d04b2-138">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d04b2-138">Next steps</span></span>
<span data-ttu-id="d04b2-139">Par exemple des modèles de gestionnaire de ressources à l’aide de jeux de mise à l’échelle, rechercher « mise » Bonjour [référentiel github de modèles de démarrage rapide Azure](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="d04b2-139">For example Resource Manager templates using scale sets, search for "vmss" in hello [Azure Quickstart Templates github repo](https://github.com/Azure/azure-quickstart-templates).</span></span>

<span data-ttu-id="d04b2-140">Pour plus d’informations, consultez hello [page d’accueil pour les jeux de mise à l’échelle](https://azure.microsoft.com/services/virtual-machine-scale-sets/).</span><span class="sxs-lookup"><span data-stu-id="d04b2-140">For general information, check out hello [main landing page for scale sets](https://azure.microsoft.com/services/virtual-machine-scale-sets/).</span></span>

