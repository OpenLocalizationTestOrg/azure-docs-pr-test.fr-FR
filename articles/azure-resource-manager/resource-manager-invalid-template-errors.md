---
title: "Erreurs de modèle Azure non valide | Microsoft Docs"
description: "Décrit comment résoudre les erreurs de modèle non valide."
services: azure-resource-manager,azure-portal
documentationcenter: 
author: tfitzmac
manager: timlt
editor: 
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: support-article
ms.date: 09/13/2017
ms.author: tomfitz
ms.openlocfilehash: e58c10cfb4cdd4ba49945e6c19845cbc957d6326
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2017
---
# <a name="resolve-errors-for-invalid-template"></a>Résoudre les erreurs de modèle non valide

Cet article décrit comment résoudre les erreurs de modèle non valide.

## <a name="symptom"></a>Symptôme

Au cours du déploiement d’un modèle, vous rencontrez l’erreur suivante :

```
Code=InvalidTemplate
Message=<varies>
```

Le message d’erreur varie selon le type d’erreur.

## <a name="cause"></a>Cause :

Cette erreur peut résulter de différents types d’erreurs. Elles impliquent généralement une erreur de syntaxe ou de structure dans le modèle.

## <a name="solution"></a>Solution

### <a name="solution-1---syntax-error"></a>Solution 1 - erreur de syntaxe

Si vous recevez un message d’erreur qui indique que la validation du modèle a échoué, vous avez peut-être un problème de syntaxe dans votre modèle.

```
Code=InvalidTemplate
Message=Deployment template validation failed
```

Cette erreur est facile à commettre car les expressions de modèle peuvent être complexes. Par exemple, l’affectation de nom suivante pour un compte de stockage contient un jeu de crochets, trois fonctions, trois jeux de parenthèses, un jeu de guillemets simples et une propriété :

```json
"name": "[concat('storage', uniqueString(resourceGroup().id))]",
```

Si vous ne fournissez pas la syntaxe correspondante, le modèle produit une valeur très différente de votre intention.

Lorsque vous recevez ce type d’erreur, examinez attentivement la syntaxe d’expression. Vous pouvez utiliser un éditeur JSON comme [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md) ou [Visual Studio Code](resource-manager-vs-code.md), qui vous signale des erreurs de syntaxe.

### <a name="solution-2---incorrect-segment-lengths"></a>Solution 2 - longueurs de segments incorrectes

Une autre erreur de modèle non valide se produit lorsque le nom de la ressource n’est pas au format approprié.

```
Code=InvalidTemplate
Message=Deployment template validation failed: 'The template resource {resource-name}'
for type {resource-type} has incorrect segment lengths.
```

Une ressource au niveau racine doit avoir un segment de moins dans le nom que dans le type de ressource. Chaque segment se différencie par une barre oblique. Dans l’exemple suivant, le type comporte deux segments et le nom un segment : il s’agit donc d’un **nom valide**.

```json
{
  "type": "Microsoft.Web/serverfarms",
  "name": "myHostingPlanName",
  ...
}
```

Mais l’exemple suivant n’est **pas un nom valide** car il possède le même nombre de segments que le type.

```json
{
  "type": "Microsoft.Web/serverfarms",
  "name": "appPlan/myHostingPlanName",
  ...
}
```

Pour les ressources enfants, le type et le nom ont le même nombre de segments. Ce nombre de segments est logique, car le nom complet et le type de l’enfant incluent le nom du parent et le type. Par conséquent, le nom complet a toujours un segment de moins que le type complet.

```json
"resources": [
    {
        "type": "Microsoft.KeyVault/vaults",
        "name": "contosokeyvault",
        ...
        "resources": [
            {
                "type": "secrets",
                "name": "appPassword",
                ...
            }
        ]
    }
]
```

Obtenir des segments valides peut être difficile si des types Resource Manager sont appliqués à plusieurs fournisseurs de ressources. Par exemple, l’installation d’un verrou de ressource sur un site web nécessite un type avec quatre segments. Par conséquent, le nom comporte 3 segments :

```json
{
    "type": "Microsoft.Web/sites/providers/locks",
    "name": "[concat(variables('siteName'),'/Microsoft.Authorization/MySiteLock')]",
    ...
}
```

### <a name="solution-3---parameter-is-not-valid"></a>Solution 3 - le paramètre n’est pas valide

Si le modèle spécifie les valeurs autorisées pour un paramètre et que vous fournissez une valeur qui n’est pas une de ces valeurs, vous recevez un message similaire à l’erreur suivante :

```
Code=InvalidTemplate;
Message=Deployment template validation failed: 'The provided value {parameter value}
for the template parameter {parameter name} is not valid. The parameter value is not
part of the allowed values
```

Vérifiez les valeurs autorisées dans le modèle et fournissez-en une pendant le déploiement.

### <a name="solution-4---circular-dependency-detected"></a>Solution 4 - dépendance circulaire détectée

Vous recevez cette erreur lorsque des ressources dépendant les unes des autres empêchent le déploiement de démarrer. À cause de l’effet combiné d’interdépendances, plusieurs ressources attendent d’autres ressources qui sont elles aussi en attente. Par exemple, la ressource 1 dépend de la ressource 3, la ressource 2 de la ressource 1 et la ressource 3 de la ressource 2. Vous pouvez généralement résoudre ce problème en supprimant les dépendances inutiles.
