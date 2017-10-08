---
title: "aaaUnderstand création de définition d’interface utilisateur pour les Applications managées Azure | Documents Microsoft"
description: "Décrit comment toocreate les définitions d’interface utilisateur pour les Applications managées Azure"
services: azure-resource-manager
documentationcenter: na
author: tabrezm
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/11/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: d53ddf438c24d5a6cb8dd53ca0b4694ab0462515
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-createuidefinition"></a>Prise en main de CreateUiDefinition
Ce document présente les concepts fondamentaux de hello de CreateUiDefinition, ce qui est utilisé par l’interface utilisateur de hello toogenerate portail Azure hello pour la création d’une application managée.

```json
{
   "$schema": "https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json",
   "handler": "Microsoft.Compute.MultiVm",
   "version": "0.1.2-preview",
   "parameters": {
      "basics": [ ],
      "steps": [ ],
      "outputs": { }
   }
}
```

Une fonction CreateUiDefinition contient toujours trois propriétés : 

* handler
* version
* parameters

Pour les applications managées, le gestionnaire doit toujours être `Microsoft.Compute.MultiVm`, et la version de hello plus récentes prises en charge est `0.1.2-preview`.

schéma Hello de propriété de paramètres hello dépend de la combinaison de hello du gestionnaire spécifié de hello et version. Pour les applications managées, les propriétés de hello pris en charge sont `basics`, `steps`, et `outputs`. principes de base et les étapes des propriétés Hello contiennent hello _éléments_ , comme les zones de texte et les menus déroulants - toobe affiché dans hello portail Azure. sorties Hello propriété est de valeurs de sortie utilisé toomap hello hello paramètres de toohello spécifié d’éléments de modèle de déploiement d’Azure Resource Manager hello.

L’inclusion de `$schema` est recommandée, mais facultative. Si spécifié, de valeur pour hello `version` doit correspondre à une version hello dans hello `$schema` URI.

## <a name="basics"></a>Concepts de base
Hello notions de base étape est toujours hello première étape de l’Assistant hello généré lorsque hello portail Azure traite une CreateUiDefinition. En outre les éléments de hello toodisplaying spécifié dans `basics`, portail de hello injecte des éléments pour l’abonnement de hello toochoose les utilisateurs, de groupe de ressources et d’emplacement pour le déploiement de hello. En règle générale, il est recommandé d’utiliser des éléments de requête pour les paramètres de déploiement à l’échelle, comme nom hello d’informations d’identification administrateur ou de cluster, dans cette étape.

Si le comportement d’un élément dépend de l’utilisateur hello abonnement, groupe de ressources ou l’emplacement, cet élément ne peut pas être utilisé dans les concepts de base. Par exemple, **Microsoft.Compute.SizeSelector** dépend d’abonnement et l’emplacement toodetermine hello liste l’utilisateur hello des tailles disponibles. Par conséquent, **Microsoft.Compute.SizeSelector** ne peut être utilisé que dans steps. En général, seuls les éléments Bonjour **Microsoft.Common** espace de noms peut être utilisé dans les concepts de base. Bien que certains éléments dans les autres espaces de noms (comme **Microsoft.Compute.Credentials**) qui ne dépendent pas hello contexte de l’utilisateur, sont toujours autorisés.

## <a name="steps"></a>Étapes
propriété d’étapes Hello peut contenir zéro ou plusieurs toodisplay d’étapes supplémentaires après les principes de base, chacun contenant un ou plusieurs éléments. Envisagez d’ajouter des étapes par rôle ou de la couche d’application hello en cours de déploiement. Par exemple, ajoutez une étape pour les entrées pour les nœuds principaux hello et qu’une étape pour les nœuds de travail hello dans un cluster.

## <a name="outputs"></a>outputs
portail Azure Hello utilise hello `outputs` éléments toomap de propriété à partir de `basics` et `steps` toohello les paramètres de modèle de déploiement d’Azure Resource Manager hello. clés de Hello de ce dictionnaire sont les noms de hello hello des paramètres de modèle et les valeurs hello sont des propriétés hello d’objets de sortie à partir d’éléments de hello référencé.

## <a name="functions"></a>Fonctions
Similaire trop[fonctions de modèle](resource-group-template-functions.md) dans Azure Resource Manager (à la fois dans la syntaxe et des fonctionnalités), CreateUiDefinition fournit des fonctions pour travailler avec les des éléments entrées et sorties, ainsi que des fonctionnalités telles que des instructions conditionnelles.

## <a name="next-steps"></a>Étapes suivantes
CreateUiDefinition elle-même dispose d’un schéma simple. profondeur de réel Hello de celui-ci proviennent de toutes les fonctions, le hello suivant des documents décrivent en détail merveilleuse et les éléments de hello pris en charge :

- [Éléments](managed-application-createuidefinition-elements.md)
- [Fonctions](managed-application-createuidefinition-functions.md)

Un schéma JSON actuel pour CreateUiDefinition est disponible ici : https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json. 

Les versions ultérieures seront disponibles sur hello même emplacement. Remplacez hello `0.1.2-preview` partie de l’URL de hello et hello `version` valeur avec l’identificateur de version hello vous avez l’intention de toouse. les identificateurs de version Hello actuellement pris en charge sont `0.0.1-preview`, `0.1.0-preview`, `0.1.1-preview`, et `0.1.2-preview`.
