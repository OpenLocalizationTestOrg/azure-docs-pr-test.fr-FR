---
title: "définie des modèles aaaLearn sur l’échelle de machine virtuelle | Documents Microsoft"
description: "En savoir toocreate une échelle viable minimale définie le modèle pour les machines virtuelles identiques"
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
ms.date: 06/01/2017
ms.author: negat
ms.openlocfilehash: b7a1cf6c03b22585e16db9c071d45795c8ae75df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="learn-about-virtual-machine-scale-set-templates"></a>En savoir plus sur les modèles de groupes de machines virtuelles identiques
[Les modèles de gestionnaire de ressources Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) est un excellent moyen toodeploy groupes de ressources liées. Cette série de didacticiels montre comment le modèle de jeu de toocreate une échelle viable minimale et toomodify toosuit de ce modèle différents scénarios. Tous les exemples proviennent de ce [référentiel GitHub](https://github.com/gatneil/mvss). 

Ce modèle est prévue toobe simple. Pour obtenir des exemples plus complètes de l’échelle définir des modèles, consultez hello [référentiel GitHub de modèles de démarrage rapide Azure](https://github.com/Azure/azure-quickstart-templates) et recherchez les dossiers qui contiennent la chaîne de hello `vmss`.

Si vous êtes déjà familiarisé avec la création de modèles, vous pouvez ignorer toohello toosee de section « Étapes suivantes » comment toomodify ce modèle.

## <a name="review-hello-template"></a>Modèle de hello de vérification

Utiliser GitHub tooreview modèle, de jeu de notre échelle viable minimale [azuredeploy.json](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json).

Dans ce didacticiel, nous allons examiner hello diff (`git diff master minimum-viable-scale-set`) toocreate hello viable minimale définie modèle élément par élément.

## <a name="define-schema-and-contentversion"></a>Définir $schema et contentVersion
Tout d’abord, nous définissons `$schema` et `contentVersion` dans le modèle de hello. Hello `$schema` élément définit la version de hello du langage de modèle hello et est utilisé pour la mise en surbrillance de syntaxe Visual Studio et des fonctionnalités similaires de validation. Hello `contentVersion` élément n’est pas utilisé par Azure. Au lieu de cela, il vous aide à effectuer le suivi de version du modèle hello.

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json",
  "contentVersion": "1.0.0.0",
```
## <a name="define-parameters"></a>Définir les paramètres
Ensuite, nous définissons deux paramètres, `adminUsername` et `adminPassword`. Les paramètres sont des valeurs que vous spécifiez au moment de hello du déploiement. Hello `adminUsername` paramètre est simplement un `string` type, mais étant donné que `adminPassword` est un secret, nous avons un type `securestring`. Une version ultérieure, ces paramètres sont passés dans la configuration du jeu de mise à l’échelle hello.

```json
  "parameters": {
    "adminUsername": {
      "type": "string"
    },
    "adminPassword": {
      "type": "securestring"
    }
  },
```
## <a name="define-variables"></a>Définir des variables
Modèles du Gestionnaire de ressources vous permettent également de définir toobe variables utilisé ultérieurement dans le modèle de hello. Notre exemple n’utilise pas des variables, donc nous avons laissé vide objet JSON de hello.

```json
  "variables": {},
```

## <a name="define-resources"></a>Définir les ressources
L’élément suivant est section relative aux ressources de modèle de hello hello. Ici, vous définissez ce que vous souhaitez réellement toodeploy. Contrairement à `parameters` et `variables` (qui sont des objets JSON), `resources` est une liste JSON d’objets JSON.

```json
   "resources": [
```

Toutes les ressources nécessitent les propriétés `type`, `name`, `apiVersion` et `location`. La première ressource de cet exemple est de type `Microsft.Network/virtualNetwork`, avec le nom `myVnet` et apiVersion `2016-03-30`. (toofind hello API version la plus récente pour un type de ressource, consultez hello [documentation de l’API REST Azure](https://docs.microsoft.com/rest/api/).)

```json
     {
       "type": "Microsoft.Network/virtualNetworks",
       "name": "myVnet",
       "apiVersion": "2016-12-01",
```

## <a name="specify-location"></a>Spécifier l’emplacement
emplacement de hello toospecify pour le réseau virtuel de hello, nous utilisons un [fonction de modèle de gestionnaire de ressources](../azure-resource-manager/resource-group-template-functions.md). Cette fonction doit être placée entre guillemets et crochets, comme suit : `"[<template-function>]"`. Dans ce cas, nous utilisons hello `resourceGroup` (fonction). Il accepte aucun argument et retourne un objet JSON contenant des métadonnées sur le groupe de ressources hello qu'est déployé pour ce déploiement. groupe de ressources Hello est définie par l’utilisateur de hello au moment de hello du déploiement. Nous puis index dans cet objet JSON avec `.location` emplacement de hello tooget à partir de l’objet JSON de hello.

```json
       "location": "[resourceGroup().location]",
```

## <a name="specify-virtual-network-properties"></a>Spécifier les propriétés du réseau virtuel
Chaque ressource de gestionnaire de ressources a son propre `properties` section pour la ressource toohello spécifique de configurations. Dans ce cas, nous spécifions ce réseau virtuel hello doit avoir un sous-réseau à l’aide de la plage d’adresses IP privées hello `10.0.0.0/16`. Un jeu de mise à l’échelle est toujours contenu dans un sous-réseau. Il ne peut pas s’étendre sur plusieurs sous-réseaux.

```json
       "properties": {
         "addressSpace": {
           "addressPrefixes": [
             "10.0.0.0/16"
           ]
         },
         "subnets": [
           {
             "name": "mySubnet",
             "properties": {
               "addressPrefix": "10.0.0.0/16"
             }
           }
         ]
       }
     },
```

## <a name="add-dependson-list"></a>Ajouter la liste dependsOn
En outre toohello requis `type`, `name`, `apiVersion`, et `location` propriétés, chaque ressource peuvent avoir une option `dependsOn` liste de chaînes. Cette liste spécifie les autres ressources de ce déploiement qui doivent se terminer avant le déploiement de cette ressource.

Dans ce cas, il n'est qu’un seul élément dans la liste hello, réseau virtuel de hello à partir de l’exemple précédent de hello. Nous spécifions cette dépendance, car hello ensemble d’échelle besoins hello réseau tooexist avant de créer les machines virtuelles. De cette manière, un ensemble d’échelle hello peut donner ces adresses IP privées de machines virtuelles à partir de la plage d’adresses IP hello précédemment spécifié dans les propriétés de réseau hello. le format de chaque chaîne dans la liste de dependsOn hello Hello est `<type>/<name>`. Utilisez hello même `type` et `name` précédemment utilisé dans la définition de ressource du réseau virtuel hello.

```json
     {
       "type": "Microsoft.Compute/virtualMachineScaleSets",
       "name": "myScaleSet",
       "apiVersion": "2016-04-30-preview",
       "location": "[resourceGroup().location]",
       "dependsOn": [
         "Microsoft.Network/virtualNetworks/myVnet"
       ],
```
## <a name="specify-scale-set-properties"></a>Spécifier les propriétés du groupe identique
Groupes identiques ont de nombreuses propriétés de personnalisation de machines virtuelles de hello dans un ensemble d’échelle hello. Pour obtenir une liste complète de ces propriétés, consultez hello [ensemble d’échelle de documentation de l’API REST](https://docs.microsoft.com/en-us/rest/api/virtualmachinescalesets/create-or-update-a-set). Pour ce didacticiel, nous ne définirons que quelques propriétés couramment utilisées.
### <a name="supply-vm-size-and-capacity"></a>Fournir la capacité et la taille de machine virtuelle
ensemble d’échelle de Hello besoins tooknow taille de la machine virtuelle toocreate (« nom de la référence (SKU) ») et combien ce toocreate de machines virtuelles (« capacité de référence (SKU) »). toosee les tailles de machine virtuelle sont disponibles, consultez hello [documentation des tailles de machine virtuelle](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-sizes).

```json
       "sku": {
         "name": "Standard_A1",
         "capacity": 2
       },
```

### <a name="choose-type-of-updates"></a>Choisir le type de mises à jour
ensemble d’échelle Hello doit également tooknow comment toohandle met à jour sur l’ensemble d’échelle hello. Il existe actuellement deux options, `Manual` et `Automatic`. Pour plus d’informations sur les différences de hello entre hello deux, consultez la documentation de la hello sur [comment tooupgrade une ensemble d’échelle](./virtual-machine-scale-sets-upgrade-scale-set.md).

```json
       "properties": {
         "upgradePolicy": {
           "mode": "Manual"
         },
```

### <a name="choose-vm-operating-system"></a>Choisir le système d’exploitation de la machine virtuelle
Hello ensemble d’échelle de besoins tooknow le tooput du système d’exploitation sur des machines virtuelles de hello. Ici, nous créer des machines virtuelles de hello avec une image de 16.04-LTS Ubuntu tous les correctifs nécessaires.

```json
         "virtualMachineProfile": {
           "storageProfile": {
             "imageReference": {
               "publisher": "Canonical",
               "offer": "UbuntuServer",
               "sku": "16.04-LTS",
               "version": "latest"
             }
           },
```

### <a name="specify-computernameprefix"></a>Spécifier computerNamePrefix
ensemble d’échelle Hello déploie plusieurs machines virtuelles. Au lieu de spécifier le nom de chaque machine virtuelle, nous spécifions `computerNamePrefix`. Hello ensemble d’échelle ajoute un préfixe de toohello index pour chaque machine virtuelle, pour que les noms de machine virtuelle aient le formulaire de hello `<computerNamePrefix>_<auto-generated-index>`.

Bonjour suivant extrait de code, nous utiliser les paramètres de hello d’avant le nom d’utilisateur administrateur tooset hello et le mot de passe pour tous les ordinateurs virtuels dans un ensemble d’échelle hello. Vous faire avec hello `parameters` fonction de modèle. Cette fonction accepte une chaîne qui spécifie le tooand toorefer de paramètre génère la valeur hello pour ce paramètre.

```json
           "osProfile": {
             "computerNamePrefix": "vm",
             "adminUsername": "[parameters('adminUsername')]",
             "adminPassword": "[parameters('adminPassword')]"
           },
```

### <a name="specify-vm-network-configuration"></a>Spécifier la configuration du réseau de machines virtuelles
Enfin, nous devons la configuration du réseau toospecify hello pour les machines virtuelles hello dans un ensemble d’échelle hello. Dans ce cas, nous avons besoin uniquement des ID de hello toospecify de sous-réseau hello créé précédemment. Cela indique hello ensemble d’échelle tooput les interfaces réseau hello dans ce sous-réseau.

Vous pouvez obtenir les ID hello du réseau virtuel de hello contenant le sous-réseau de hello à l’aide de hello `resourceId` fonction de modèle. Cette fonction utilise les type hello et le nom d’une ressource et retourne hello identificateur qualifié complet de la ressource. Ce code présente sous forme de hello :`/subscriptions/<subscriptionId>/resourceGroups/<resourceGroupName>/<resourceProviderNamespace>/<resourceType>/<resourceName>`

Toutefois, identificateur hello du réseau virtuel de hello n’est pas suffisant. Vous devez spécifier le sous-réseau spécifique hello hello des machines virtuelles doivent être dans un ensemble d’échelle. toodo, concaténer `/subnets/mySubnet` toohello les ID de réseau virtuel de hello. résultat de Hello est hello complet des ID de sous-réseau de hello. Effectuer cette concaténation avec hello `concat` fonction qui accepte une série de chaînes et retourne leur concaténation.

```json
           "networkProfile": {
             "networkInterfaceConfigurations": [
               {
                 "name": "myNic",
                 "properties": {
                   "primary": "true",
                   "ipConfigurations": [
                     {
                       "name": "myIpConfig",
                       "properties": {
                         "subnet": {
                           "id": "[concat(resourceId('Microsoft.Network/virtualNetworks', 'myVnet'), '/subnets/mySubnet')]"
                         }
                       }
                     }
                   ]
                 }
               }
             ]
           }
         }
       }
     }
   ]
}

```

## <a name="next-steps"></a>Étapes suivantes

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
