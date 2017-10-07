---
title: "ressource enfant d’aaaDefine dans le modèle Azure | Documents Microsoft"
description: "Montre comment tooset hello type de ressource et le nom de ressource enfant dans un modèle Azure Resource Manager"
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: tomfitz
ms.openlocfilehash: c502c589100d7ae864d7fb01b5ba10ddfaf92592
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="set-name-and-type-for-child-resource-in-resource-manager-template"></a>Définir le nom et le type d’une ressource enfant dans un modèle Resource Manager
Lorsque vous créez un modèle, vous devez fréquemment tooinclude une ressource enfant qui est la ressource parent de tooa connexes. Par exemple, votre modèle peut inclure un serveur SQL et une base de données. Hello SQL server est ressource parente de hello, et base de données hello ressource enfant de hello. 

format Hello hello enfant du type de ressource est :`{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`

format Hello hello enfant du nom de ressource est :`{parent-resource-name}/{child-resource-name}`

Toutefois, vous spécifiez type de hello et le nom d’un modèle différemment en fonction de si elle est imbriquée dans la ressource parent de hello, ou sur sa propre au niveau supérieur de hello. Cette rubrique montre comment toohandle les deux approches.

Lors de la construction d’une ressource de tooa référence qualifiée complète, les segments de hello ordre toocombine du type de hello et nom n’est pas une simple concaténation de hello deux.  Au lieu de cela, utilisez une séquence d’après l’espace de noms hello, *type/nom* paires toomost moins spécifique spécifique :

```json
{resource-provider-namespace}/{parent-resource-type}/{parent-resource-name}[/{child-resource-type}/{child-resource-name}]*
```

Par exemple :

`Microsoft.Compute/virtualMachines/myVM/extensions/myExt` est correct `Microsoft.Compute/virtualMachines/extensions/myVM/myExt` n’est pas correct

## <a name="nested-child-resource"></a>Ressource enfant imbriquée
toodefine de façon plus simple Hello une ressource enfant est toonest dans la ressource parent de hello. Hello suivant montre une base de données SQL imbriqué dans un serveur SQL Server.

```json
{
  "name": "exampleserver",
  "type": "Microsoft.Sql/servers",
  "apiVersion": "2014-04-01",
  ...
  "resources": [
    {
      "name": "exampledatabase",
      "type": "databases",
      "apiVersion": "2014-04-01",
      ...
    }
  ]
}
```

De la ressource enfant hello, hello type a la valeur trop`databases` mais son type de ressource complet est `Microsoft.Sql/servers/databases`. Vous ne fournissez pas `Microsoft.Sql/servers/` , car il est supposé hello parent type de ressource. nom de la ressource enfant Hello est défini trop`exampledatabase` , mais le nom complet de hello inclut hello parent. Vous ne fournissez pas `exampleserver` , car il est supposé à partir de la ressource parent de hello.

## <a name="top-level-child-resource"></a>Ressource enfant de niveau supérieur
Vous pouvez définir des ressources enfants de hello au niveau supérieur de hello. Vous pouvez utiliser cette approche si la ressource de hello parent n’est pas déployé de hello même modèle ou si voulez toouse `copy` toocreate plusieurs ressources enfants. Avec cette approche, vous devez fournir le type de ressource complet hello et inclure le nom de la ressource parent hello dans le nom de la ressource enfant hello.

```json
{
  "name": "exampleserver",
  "type": "Microsoft.Sql/servers",
  "apiVersion": "2014-04-01",
  "resources": [ 
  ],
  ...
},
{
  "name": "exampleserver/exampledatabase",
  "type": "Microsoft.Sql/servers/databases",
  "apiVersion": "2014-04-01",
  ...
}
```

base de données de Hello est un serveur de toohello de ressources enfants, même si elles sont définies sur le même niveau dans le modèle de hello de hello.

## <a name="next-steps"></a>Étapes suivantes
* Pour obtenir des recommandations sur la façon toocreate modèles, consultez [meilleures pratiques pour la création de modèles Azure Resource Manager](resource-manager-template-best-practices.md).
* Pour obtenir un exemple de création de plusieurs ressources enfant, consultez [Déployer plusieurs instances de ressources dans des modèles Azure Resource Manager](resource-group-create-multiple.md).
