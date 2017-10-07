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
# <a name="convert-a-scale-set-template-tooa-managed-disk-scale-set-template"></a>Convertir un modèle de mise à l’échelle ensemble modèle tooa disque géré échelle jeu

Clients avec un modèle de gestionnaire de ressources pour la création d’une échelle ne pas à l’aide de disque géré souhaitiez toomodify il toouse gérés disque. Cet article explique comment toodo ce, en utilisant par exemple une requête d’extraction à partir de hello [modèles de démarrage rapide Azure](https://github.com/Azure/azure-quickstart-templates), un référentiel communautaire pour des exemples de modèles de gestionnaire de ressources. requête de tirage complète de Hello peut être consulté ici : [https://github.com/Azure/azure-quickstart-templates/pull/2998](https://github.com/Azure/azure-quickstart-templates/pull/2998), et hello les parties pertinentes de hello diff ci-dessous, ainsi que des explications :

## <a name="making-hello-os-disks-managed"></a>Rendre les disques du système d’exploitation hello gérés

Dans la comparaison de hello ci-dessous, nous constatons que nous avons supprimé plusieurs variables connexes toostorage disque propriétés du compte et. Type de compte de stockage n’est plus nécessaire (Standard_LRS est la valeur par défaut hello), mais nous avons toujours spécifier s’il veut. Seuls Standard_LRS et Premium_LRS sont pris en charge pour les disques gérés. Nouveau suffixe de compte de stockage, tableau de chaînes uniques et le nombre d’association de sécurité ont été utilisés dans les noms de compte hello ancien modèle toogenerate stockage. Ces variables ne sont plus nécessaires dans le nouveau modèle de hello, car le disque géré crée automatiquement des comptes de stockage sur le compte du client hello. De même, nom de conteneur de disque dur virtuel et le nom du disque du système d’exploitation ne sont plus nécessaires, car le disque géré nomme automatiquement les disques et les conteneurs d’objets blob de stockage sous-jacent hello.

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


Dans diff hello ci-dessous, nous peut voir que nous avons mis à jour hello de calcul api version too2016-04-30-preview, qui est hello plus ancienne version requise pour la prise en charge de disque géré avec des jeux de mise à l’échelle. Notez que nous avons toujours utiliser des disques non managés dans la nouvelle version d’api hello avec l’ancienne syntaxe de hello si vous le souhaitez. En d’autres termes, si uniquement mettre à jour hello version de l’api de calcul et ne modifiez rien d’autre, modèle de hello doit continuer toowork comme avant.

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

Dans la comparaison de hello ci-dessous, nous constatons que nous allons supprimer des ressources de compte de stockage hello du tableau des ressources hello complètement. Nous n’en avons plus besoin, car le disque géré les crée automatiquement en notre nom.

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

Dans diff hello ci-dessous, nous peut voir que nous allons supprimer hello dépend clause faisant référence à partir de hello échelle ensemble toohello boucle qui créait des comptes de stockage. Dans l’ancien modèle de hello, cela a été de vous assurer que les comptes de stockage hello ont été créés avant l’ensemble d’échelle hello a commencé la création, mais cette clause n’est plus nécessaire avec disque géré. Nous également supprimer la propriété de conteneurs de disque dur virtuel hello et hello la propriété de nom de disque de système d’exploitation que ces propriétés sont gérées automatiquement dans les coulisses de hello par disque géré. Si nous souhaité, nous pouvons ajouter `"managedDisk": { "storageAccountType": "Premium_LRS" }` dans la configuration de « osDisk » hello si nous voulions les disques premium du système d’exploitation. Uniquement les ordinateurs virtuels avec une majuscule ou de minuscule « Bonjour VM référence (SKU) pouvez utiliser des disques premium.

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

Il n’existe aucune propriété explicite dans la configuration de jeu hello mise à l’échelle pour que toouse géré ou un disque non managé. ensemble d’échelle Hello sait quelle toouse basé sur les propriétés hello qui sont présentes dans le profil de stockage hello. Par conséquent, il est important lorsque vous modifiez hello modèle tooensure qui sont des propriétés du droit de hello dans le profil de stockage hello de hello ensemble d’échelle.


## <a name="data-disks"></a>Disques de données

Modifications de hello ci-dessus, hello échelle ensemble utilise des disques gérés pour hello du système d’exploitation sur le disque, mais qu’en est-il des disques de données ? tooadd des disques de données, ajouter la propriété de « dataDisks » hello sous « storageProfile » au même niveau en tant que « osDisk » de hello. valeur de propriété de hello Hello est une liste JSON d’objets, chacun d’eux possède des propriétés « numéro d’unité logique » (qui doit être unique pour chaque disque de données sur une machine virtuelle), « createOption » (« empty » est actuellement hello uniquement l’option prise en charge) et « diskSizeGB » (taille du disque hello en gigaoctets de hello ; doit être supérieur à 0 et inférieurs à 1024) comme dans hello l’exemple suivant : 

```
"dataDisks": [
  {
    "lun": "1",
    "createOption": "empty",
    "diskSizeGB": "1023"
  }
]
```

Si vous spécifiez `n` disques dans ce tableau, chaque ordinateur virtuel dans l’échelle de hello définie Obtient `n` disques de données. Notez, cependant, que ces disques de données sont des appareils bruts. Ils ne sont pas formatés. C’est toohello client tooattach, partition et les disques au format hello avant de les utiliser. Si vous le souhaitez, nous pouvons également spécifier `"managedDisk": { "storageAccountType": "Premium_LRS" }` dans chaque toospecify objet de disque de données qu’il doit être un disque de données premium. Uniquement les ordinateurs virtuels avec une majuscule ou de minuscule « Bonjour VM référence (SKU) pouvez utiliser des disques premium.

toolearn savoir plus sur à l’aide de disques de données avec montée en puissance des jeux, consultez [cet article](./virtual-machine-scale-sets-attached-disks.md).


## <a name="next-steps"></a>Étapes suivantes
Par exemple des modèles de gestionnaire de ressources à l’aide de jeux de mise à l’échelle, rechercher « mise » Bonjour [référentiel github de modèles de démarrage rapide Azure](https://github.com/Azure/azure-quickstart-templates).

Pour plus d’informations, consultez hello [page d’accueil pour les jeux de mise à l’échelle](https://azure.microsoft.com/services/virtual-machine-scale-sets/).

