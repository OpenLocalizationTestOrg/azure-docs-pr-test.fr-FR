---
title: "met à jour aaaSchema juin-01-2016 - Azure Logic Apps | Documents Microsoft"
description: "Créer des définitions JSON pour Azure Logic Apps avec la version de schéma 2016-06-01"
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 349d57e8-f62b-4ec6-a92f-a6e0242d6c0e
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 07/25/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: b0347fbbd692a93b63a2f8b741402a225450b35a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="schema-updates-for-azure-logic-apps---june-1-2016"></a>Mises à jour de schéma pour Azure Logic Apps - 1er juin 2016

Ce schéma et une API version pour Azure Logic Apps inclut des améliorations clés qui rendent les applications logique plus fiable et plus facile de toouse :

* Les [étendues](#scopes) vous permettent de regrouper ou d’imbriquer des actions sous la forme d’un ensemble d’actions.
* Les [conditions et les boucles](#conditions-loops) sont désormais des actions de première classe.
* Le classement plus précis pour l’exécution des actions avec hello `runAfter` propriété, en remplaçant`dependsOn`

afficher un aperçu de tooupgrade vos applications logiques à partir de hello au 1er août 2015 1er juin 2016 schéma, toohello [extraire la section de mise à niveau hello](##upgrade-your-schema).

<a name="scopes"></a>
## <a name="scopes"></a>Étendues

Ce schéma comporte des étendues, qui vous permettent de regrouper ou d’imbriquer des actions. Par exemple, une condition peut en contenir une autre. Apprenez-en davantage sur la [syntaxe des étendues](../logic-apps/logic-apps-loops-and-scopes.md), ou examinez l’exemple d’étendue de base ci-dessous :

```
{
    "actions": {
        "My_Scope": {
            "type": "scope",
            "actions": {                
                "Http": {
                    "inputs": {
                        "method": "GET",
                        "uri": "http://www.bing.com"
                    },
                    "runAfter": {},
                    "type": "Http"
                }
            }
        }
    }
}
```

<a name="conditions-loops"></a>
## <a name="conditions-and-loops-changes"></a>Modifications des conditions et boucles

Dans les versions de schéma précédentes, les conditions et les boucles étaient des paramètres associés avec une seule action. Cette limitation a été levée dans ce schéma, de sorte que les conditions et les boucles apparaissent à présent sous forme de types d’actions. Apprenez-en davantage sur les [boucles et étendues](../logic-apps/logic-apps-loops-and-scopes.md), ou examinez l’exemple d’action de condition de base ci-dessous :

```
{
    "If_trigger_is_some-trigger": {
        "type": "If",
        "expression": "@equals(triggerBody(), 'some-trigger')",
        "runAfter": { },
        "actions": {
            "Http_2": {
                "inputs": {
                    "method": "GET",
                    "uri": "http://www.bing.com"
                },
                "runAfter": {},
                "type": "Http"
            }
        },
        "else": 
        {
            "if_trigger_is_another-trigger": "..."
        }      
    }
}
```

<a name="run-after"></a>
## <a name="runafter-property"></a>Propriété « runAfter »

Hello `runAfter` propriété remplace `dependsOn`, en fournissant une plus grande précision lorsque vous spécifiez la commande hello exécuter pour les actions basé sur l’état de hello des actions précédentes.

Hello `dependsOn` de la propriété est synonyme de « action de hello exécuté et a réussi », quel que soit le nombre de fois que vous souhaitiez tooexecute une action, en fonction de l’action précédente de hello réussite, échec ou ignorée. Hello `runAfter` propriété souplesse que comme un objet qui spécifie tous les hello qui hello objet une fois les noms d’actions. Cette propriété définit également un tableau d’états acceptables en tant que déclencheurs. Par exemple, si vous souhaitiez toorun après une réussite et également après étape B réussit ou échoue, vous construisez ce `runAfter` propriété :

```
{
    "...",
    "runAfter": {
        "A": ["Succeeded"],
        "B": ["Succeeded", "Failed"]
    }
}
```

## <a name="upgrade-your-schema"></a>Mettre à niveau votre schéma

Nouveau schéma de la mise à niveau toohello ne prend que quelques étapes. Hello mise à niveau implique l’exécution du script de mise à niveau hello, l’enregistrement comme nouvelle application logique et si vous le souhaitez, en remplaçant éventuellement application logique de la précédente hello.

1. Bonjour portail Azure, ouvrez votre application logique.

2. Accédez trop**vue d’ensemble**. Dans la barre d’outils hello logique application, choisissez **mise à jour de schéma**.
   
    ![Choisir l’option Mettre à jour le schéma][1]
   
    Hello définition mise à niveau est retournée, que vous pouvez copier et coller dans une définition de ressource, si nécessaire. 
    Toutefois, nous **recommandons** vous choisissez **enregistrer en tant que** toomake assurer que toutes les références de connexion sont valides dans hello mis à niveau l’application logique.

3. Dans la barre d’outils du Panneau de mise à niveau de hello, choisissez **Enregistrer sous**.

4. Entrez l’état et le nom logique de hello. toodeploy votre application de la logique de mise à niveau, choisissez **créer**.

5. Vérifiez que votre application logique mise à niveau fonctionne comme prévu.
   
   > [!NOTE]
   > Si vous utilisez un déclencheur manuel ou de la demande, URL de rappel hello change dans votre nouvelle application logique. Fonctionnement de l’expérience test hello nouvelle URL toomake vraiment hello de bout en bout. toopreserve des URL précédentes, vous pouvez cloner sur votre application logique existant.

6. *Facultatif* choisir de votre application logique précédente avec hello nouvelle version du schéma, la barre d’outils hello toooverwrite **Clone**, en regard de trop**mise à jour de schéma**. Cette étape est nécessaire uniquement si vous voulez tookeep hello même ressource ID ou demande URL du déclencheur de votre application logique.

### <a name="upgrade-tool-notes"></a>Notes de l’outil de mise à niveau

#### <a name="mapping-conditions"></a>Mappage de conditions

Dans la définition de hello mis à niveau, outil de hello permet un meilleur effort à regrouper les actions de la branche true et false en tant qu’étendue. Plus précisément, hello concepteur motif de `@equals(actions('a').status, 'Skipped')` doivent apparaître comme un `else` action. Toutefois, si l’outil de hello détecte des séquences non reconnaissables, outil de hello peut créer des conditions séparées pour hello true et branche de false hello. Vous pouvez remapper les actions après la mise à niveau si nécessaire.

#### <a name="foreach-loop-with-condition"></a>Boucle « foreach » avec condition

Dans le nouveau schéma de hello, vous pouvez utiliser le modèle de hello hello filtre action tooreplicate d’un `foreach` boucle avec une condition par élément, mais cette modification devrait se produire automatiquement lorsque vous mettez à niveau. condition de Hello devienne une action de filtrage avant de boucle foreach de hello pour retourner uniquement un tableau d’éléments qui correspondent à la condition de hello, et ce tableau est passé à l’action de foreach hello. Pour découvrir un exemple, consultez l’article relatif aux [boucles et étendues](../logic-apps/logic-apps-loops-and-scopes.md).

#### <a name="resource-tags"></a>Balises de ressource

Une fois que vous mettez à niveau, les balises de ressources sont supprimés, donc vous devez les réinitialiser pour les flux de travail hello mis à niveau.

## <a name="other-changes"></a>Autres modifications

### <a name="renamed-manual-trigger-toorequest-trigger"></a>Renommer le déclencheur 'manual' too'request' déclencheur

Hello `manual` type de déclencheur a été déconseillée et renommé trop`request` avec le type `http`. Cette modification crée plus de cohérence de type hello du modèle qui hello déclencheur est toobuild utilisé.

### <a name="new-filter-action"></a>Nouvelle action de « filtre »

toofilter un grand tableau vers le bas tooa plus petit jeu d’éléments, hello new `filter` type accepte un tableau et une condition, évalue la condition hello pour chaque élément et retourne un tableau avec les éléments répondant à la condition de hello.

### <a name="restrictions-for-foreach-and-until-actions"></a>Restrictions relatives aux actions « foreach » et « until »

Hello `foreach` et `until` boucle sont restreintes tooa une seule action.

### <a name="new-trackedproperties-for-actions"></a>Nouvelle propriété « trackedProperties » relative aux actions

Actions peuvent avoir maintenant une propriété supplémentaire appelée `trackedProperties`, qui est le frère toohello `runAfter` et `type` propriétés. Cet objet spécifie certaines entrées d’action ou sorties que vous souhaitez tooinclude de télémétrie de Diagnostic Azure hello, émis dans le cadre d’un flux de travail. Par exemple :

```
{                
    "Http": {
        "inputs": {
            "method": "GET",
            "uri": "http://www.bing.com"
        },
        "runAfter": {},
        "type": "Http",
        "trackedProperties": {
            "responseCode": "@action().outputs.statusCode",
            "uri": "@action().inputs.uri"
        }
    }
}
```

## <a name="next-steps"></a>Étapes suivantes
* [Créer des définitions d’application logique](../logic-apps/logic-apps-author-definitions.md)
* [Création d’un modèle de déploiement d’applications logiques](../logic-apps/logic-apps-create-deploy-template.md)

<!-- Image references -->
[1]: ./media/logic-apps-schema-2016-04-01/upgradeButton.png
