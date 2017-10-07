---
title: "ordre de déploiement aaaSet pour les ressources Azure | Documents Microsoft"
description: "Décrit comment tooset une seule ressource comme dépend d’une autre ressource pendant tooensure des ressources de déploiement sont déployés dans l’ordre correct de hello."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: 
ms.assetid: 34ebaf1e-480c-4b4d-9bf6-251bd3f8f2cf
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/03/2017
ms.author: tomfitz
ms.openlocfilehash: 2f658f4c85236966c46b34a65aafb8426c92806c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="define-hello-order-for-deploying-resources-in-azure-resource-manager-templates"></a>Définir l’ordre de hello pour le déploiement de ressources dans les modèles Azure Resource Manager
Pour une ressource donnée, il peut y avoir des autres ressources qui doivent exister pour que la ressource de hello est déployée. Par exemple, un serveur SQL server doit exister avant de tenter de toodeploy une base de données SQL. Pour définir cette relation, le marquage d’une ressource en tant que dépendant de hello autre ressource. Vous définissez une dépendance avec hello **dependsOn** élément, ou à l’aide de hello **référence** (fonction). 

Le Gestionnaire de ressources évalue des dépendances hello entre les ressources et les déploie dans leur ordre dépendant. Quand les ressources ne dépendent pas les unes des autres, Resource Manager les déploie en parallèle. Vous devez uniquement toodefine dépendances pour les ressources qui sont déployés dans hello même modèle. 

## <a name="dependson"></a>dependsOn
Dans votre modèle, élément de dependsOn hello vous permet de toodefine une ressource en tant que dépendant sur une ou plusieurs ressources. Sa valeur peut être une liste séparée par des virgules de noms de ressources. 

Hello suivant montre un ensemble d’échelle de machine virtuelle qui dépend d’un équilibrage de charge, le réseau virtuel et une boucle qui crée plusieurs comptes de stockage. Ces autres ressources ne sont pas affichés dans hello l’exemple suivant, mais ils ont besoin tooexist ailleurs dans le modèle de hello.

```json
{
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  "name": "[variables('namingInfix')]",
  "location": "[variables('location')]",
  "apiVersion": "2016-03-30",
  "tags": {
    "displayName": "VMScaleSet"
  },
  "dependsOn": [
    "[variables('loadBalancerName')]",
    "[variables('virtualNetworkName')]",
    "storageLoop",
  ],
  ...
}
```

Bonjour précédent exemple, une dépendance est incluse dans les ressources hello qui sont créés dans une boucle de copie nommée **storageLoop**. Pour obtenir un exemple, consultez [Création de plusieurs instances de ressources dans Azure Resource Manager](resource-group-create-multiple.md).

Lors de la définition des dépendances, vous pouvez inclure hello ressource fournisseur espace de noms et de la ressource de type tooavoid toute ambiguïté. Par exemple, tooclarify mettre en forme un équilibreur de charge et le réseau virtuel qui peut avoir hello que mêmes noms que d’autres ressources, hello utilisation suivant :

```json
"dependsOn": [
  "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]",
  "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
]
``` 

Vous pouvez être tenté toouse dependsOn toomap relations entre vos ressources, mais il est important toounderstand pourquoi votre travail. Par exemple, la façon dont les ressources sont interconnectés, de toodocument dependsOn n’est pas une approche hello. Vous ne peut pas interroger les ressources qui ont été définies dans l’élément dependsOn de hello après le déploiement. En utilisant dependsOn, vous risquez d’avoir un impact sur le temps de déploiement, car Resource Manager ne déploie pas en parallèle deux ressources qui ont une dépendance. toodocument les relations entre les ressources, utilisez à la place [liaison des ressources](/rest/api/resources/resourcelinks).

## <a name="child-resources"></a>Ressources enfants
propriété des ressources Hello vous permet de ressources enfants toospecify toohello connexes des ressources en cours de définition. Les ressources enfants peuvent uniquement être définies sur cinq niveaux. Il est important de toonote une dépendance implicite n’est pas créée entre une ressource enfant et la ressource parent de hello. Si vous avez besoin de hello toobe de ressource enfant déployé après la ressource parent de hello, vous devez déclarer explicitement cette dépendance avec la propriété : dependsOn hello. 

Chaque ressource parente accepte uniquement certains types de ressources comme ressources enfants. Hello accepté de types de ressources sont spécifiés dans hello [schéma de modèle](https://github.com/Azure/azure-resource-manager-schemas) de ressource du parent hello. nom Hello enfant du type de ressource inclut le nom hello hello parent du type de ressource, telles que **Microsoft.Web/sites/config** et **Microsoft.Web/sites/extensions** sont les deux ressources enfant de hello  **Microsoft.Web/sites**.

Bonjour à l’exemple suivant montre un SQL server et la base de données SQL. Notez qu’une dépendance explicite est définie entre la base de données SQL hello et SQL server, même si la base de données hello est un enfant du serveur de hello.

```json
"resources": [
  {
    "name": "[variables('sqlserverName')]",
    "type": "Microsoft.Sql/servers",
    "location": "[resourceGroup().location]",
    "tags": {
      "displayName": "SqlServer"
    },
    "apiVersion": "2014-04-01-preview",
    "properties": {
      "administratorLogin": "[parameters('administratorLogin')]",
      "administratorLoginPassword": "[parameters('administratorLoginPassword')]"
    },
    "resources": [
      {
        "name": "[parameters('databaseName')]",
        "type": "databases",
        "location": "[resourceGroup().location]",
        "tags": {
          "displayName": "Database"
        },
        "apiVersion": "2014-04-01-preview",
        "dependsOn": [
          "[variables('sqlserverName')]"
        ],
        "properties": {
          "edition": "[parameters('edition')]",
          "collation": "[parameters('collation')]",
          "maxSizeBytes": "[parameters('maxSizeBytes')]",
          "requestedServiceObjectiveName": "[parameters('requestedServiceObjectiveName')]"
        }
      }
    ]
  }
]
```

## <a name="reference-function"></a>fonction de référence
Hello [font référence à fonction](resource-group-template-functions-resource.md#reference) permet une tooderive expression sa valeur à partir d’autres paires nom / valeur JSON ou les ressources d’exécution. Les expressions de référence déclarent implicitement qu’une ressource dépend d’une autre. le format général Hello est :

```json
reference('resourceName').propertyPath
```

Bonjour l’exemple suivant, un point de terminaison CDN explicitement dépend hello profil CDN et implicitement dépend d’une application web.

```json
{
    "name": "[variables('endpointName')]",
    "type": "endpoints",
    "location": "[resourceGroup().location]",
    "apiVersion": "2016-04-02",
    "dependsOn": [
            "[variables('profileName')]"
    ],
    "properties": {
        "originHostHeader": "[reference(variables('webAppName')).hostNames[0]]",
        ...
    }
```

Vous pouvez utiliser cet élément ou hello dépendances de toospecify dependsOn élément, mais vous n’avez pas besoin de toouse à la fois pour hello même ressource dépendante. Si possible, utilisez un tooavoid de référence implicite Ajout d’une dépendance inutile.

toolearn, voir [font référence à fonction](resource-group-template-functions-resource.md#reference).

## <a name="recommendations-for-setting-dependencies"></a>Recommandations pour la définition des dépendances

Lorsque vous décidez quelles tooset de dépendances, utilisez hello instructions :

* Définissez le moins de dépendances possible.
* Définissez une ressource enfant comme dépendante de sa ressource parent.
* Hello d’utilisation **référence** tooset des dépendances implicite entre les ressources qui doivent tooshare une propriété de fonction. N’ajoutez pas de dépendance explicite (**dependsOn**) lorsque vous avez déjà défini une dépendance implicite. Cette approche réduit le risque de hello d’avoir des dépendances inutiles. 
* Définissez une dépendance lorsqu’une ressource ne peut pas être **créée** sans la fonctionnalité d’une autre ressource. Ne définissez pas une dépendance si les ressources hello interagissent uniquement après le déploiement.
* Ajoutez les dépendances l’une après l’autre sans les définir explicitement. Par exemple, votre machine virtuelle dépend d’une interface réseau virtuelle et interface de réseau virtuel hello dépend d’un réseau virtuel et les adresses IP publiques. Par conséquent, hello est ressources une fois toutes les trois déployées, mais ne définissez pas explicitement de machine virtuelle de hello comme dépend de toutes les ressources de trois. Cette approche précise l’ordre des dépendances hello et rend plus facile modèle de hello toochange plus tard.
* Si une valeur peut être déterminée avant le déploiement, essayez de déployer des ressources hello sans une dépendance. Par exemple, si une valeur de configuration doit nom hello d’une autre ressource, vous devrez peut-être pas une dépendance. Ce guide ne fonctionne pas toujours, car certaines ressources vérifient l’existence de hello Hello autre ressource. Si vous recevez une erreur, ajoutez une dépendance. 

Resource Manager identifie les dépendances circulaires lors de la validation du modèle. Si vous recevez un message d’erreur indiquant qu’il existe une dépendance circulaire, évaluez vos toosee modèle si toutes les dépendances ne sont pas nécessaires et peuvent être supprimés. Si la suppression de dépendances ne fonctionne pas, vous pouvez éviter les dépendances circulaires en déplaçant certaines opérations de déploiement dans les ressources enfants qui sont déployés après ressources hello qui ont une dépendance circulaire hello. Par exemple, supposons que vous déployez deux machines virtuelles, mais vous devez définir des propriétés sur chacun d’eux qui font référence toohello autres. Vous pouvez les déployer dans hello suivant l’ordre :

1. Machine virtuelle 1
2. Machine virtuelle 2
3. L’extension sur la machine virtuelle 1 dépend des machines virtuelles 1 et 2. extension de Hello définit des valeurs sur vm1 qu’il obtient à partir de l’ordinateur virtuel 2.
4. L’extension sur la machine virtuelle 2 dépend des machines virtuelles 1 et 2. extension de Hello définit des valeurs sur vm2 qu’il obtient de vm1.

Pour plus d’informations sur l’évaluation d’ordre de déploiement hello et la résolution des erreurs de dépendance, consultez [résoudre les erreurs courantes de déploiement Azure avec Azure Resource Manager](resource-manager-common-deployment-errors.md).

## <a name="next-steps"></a>Étapes suivantes
* toolearn sur la résolution des dépendances au cours du déploiement, consultez [résoudre les erreurs courantes de déploiement Azure avec Azure Resource Manager](resource-manager-common-deployment-errors.md).
* toolearn sur la création de modèles Azure Resource Manager, consultez [création de modèles](resource-group-authoring-templates.md). 
* Pour obtenir la liste des fonctions disponibles de hello dans un modèle, consultez [fonctions de modèle](resource-group-template-functions.md).

