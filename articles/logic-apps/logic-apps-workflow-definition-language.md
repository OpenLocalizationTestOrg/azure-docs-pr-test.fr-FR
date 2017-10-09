---
title: "schéma de langage de définition d’aaaWorkflow - Azure Logic Apps | Documents Microsoft"
description: "Définir des workflows basés sur le schéma de définition du flux de travail hello pour Azure Logic Apps"
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 26c94308-aa0d-4730-97b6-de848bffff91
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 03/21/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: f12440e9ca269a9236132deeb888dbde7fb734d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="workflow-definition-language-schema-for-azure-logic-apps"></a>Schéma du langage de définition du flux de travail pour Azure Logic Apps

Une définition de flux de travail contient la logique hello réelle qui s’exécute dans le cadre de votre application logique. Cette définition inclut une ou plusieurs déclencheurs qui démarre l’application logique de hello et une ou plusieurs actions pour hello logique application tootake.  
  
## <a name="basic-workflow-definition-structure"></a>Structure de la définition de flux de travail de base

Voici la structure de base hello d’une définition de flux de travail :  
  
```json
{
    "$schema": "<schema-of the-definition>",
    "contentVersion": "<version-number-of-definition>",
    "parameters": { <parameter-definitions-of-definition> },
    "triggers": [ { <definition-of-flow-triggers> } ],
    "actions": [ { <definition-of-flow-actions> } ],
    "outputs": { <output-of-definition> }
}
```
  
> [!NOTE]
> Hello [API REST de gestion des flux de travail](https://docs.microsoft.com/rest/api/logic/workflows) documentation dispose d’informations sur la façon de toocreate et de gérer les workflows d’application logique.
  
|Nom de l'élément|Requis|Description|  
|------------------|--------------|-----------------|  
|$schema|Non|Spécifie l’emplacement de hello pour le fichier de schéma JSON hello qui décrit la version de hello du langage de définition de hello. Cet emplacement est requis si vous référencez une définition en externe. Ce document, hello emplacement est : <p>`https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2015-08-01-preview/workflowdefinition.json#`|  
|contentVersion|Non|Spécifie la version de définition de hello. Lorsque vous déployez un flux de travail à l’aide de la définition de hello, vous pouvez utiliser cette valeur toomake que la définition de droite hello est utilisé.|  
|parameters|Non|Spécifie les paramètres utilisés tooinput données dans la définition de hello. Il est possible de définir 50 paramètres maximum.|  
|Déclencheurs|Non|Spécifie les informations pour les déclencheurs hello qui déclenchent des flux de travail hello. Il est possible de définir 10 déclencheurs au maximum.|  
|actions|Non|Spécifie les actions qui sont effectuées pendant l’exécution de flux de hello. Il est possible de définir 250 actions au maximum.|  
|outputs|Non|Spécifie des informations sur les ressources hello déployé. Il est possible de définir 10 sorties au maximum.|  
  
## <a name="parameters"></a>Paramètres

Cette section spécifie tous les paramètres de hello sont utilisées dans la définition de flux de travail hello au moment du déploiement. Tous les paramètres doivent être déclarées dans cette section avant de pouvoir être utilisés dans d’autres sections de la définition de hello.  
  
Hello suivant montre structure hello d’une définition de paramètre :  

```json
"parameters": {
    "<parameter-name>" : {
        "type" : "<type-of-parameter-value>",
        "defaultValue": <default-value-of-parameter>,
        "allowedValues": [ <array-of-allowed-values> ],
        "metadata" : { "key": { "name": "value"} }
    }
}
```

|Nom de l'élément|Requis|Description|  
|------------------|--------------|-----------------|  
|type|Oui|**Type** : string <p> **Déclaration** : `"parameters": {"parameter1": {"type": "string"}` <p> **Spécification** : `"parameters": {"parameter1": {"value": "myparamvalue1"}}` <p> **Type** : securestring <p> **Déclaration** : `"parameters": {"parameter1": {"type": "securestring"}}` <p> **Spécification** : `"parameters": {"parameter1": {"value": "myparamvalue1"}}` <p> **Type** : int <p> **Déclaration** : `"parameters": {"parameter1": {"type": "int"}}` <p> **Spécification** : `"parameters": {"parameter1": {"value" : 5}}` <p> **Type** : bool <p> **Déclaration** : `"parameters": {"parameter1": {"type": "bool"}}` <p> **Spécification** : `"parameters": {"parameter1": { "value": true }}` <p> **Type** : array <p> **Déclaration** : `"parameters": {"parameter1": {"type": "array"}}` <p> **Spécification** : `"parameters": {"parameter1": { "value": [ array-of-values ]}}` <p> **Type** : object <p> **Déclaration** : `"parameters": {"parameter1": {"type": "object"}}` <p> **Spécification** : `"parameters": {"parameter1": { "value": { JSON-object } }}` <p> **Type** : secureobject <p> **Déclaration** : `"parameters": {"parameter1": {"type": "object"}}` <p> **Spécification** : `"parameters": {"parameter1": { "value": { JSON-object } }}` <p> **Remarque :** hello `securestring` et `secureobject` types ne sont pas renvoyés dans `GET` operations. L’ensemble des mots de passe, clés et secrets doivent utiliser ce type.|  
|defaultValue|Non|Spécifie la valeur par défaut de hello pour le paramètre hello lorsque aucune valeur n’est spécifiée au moment de hello hello ressource est créée.|  
|allowedValues|Non|Spécifie un tableau de valeurs autorisées pour le paramètre hello.|  
|metadata|Non|Spécifie des informations supplémentaires sur le paramètre hello, comme une description lisible ou des données au moment du design utilisées par Visual Studio ou d’autres outils.|  
  
Cet exemple montre comment vous pouvez utiliser un paramètre dans la section de corps hello d’une action :  
  
```json
"body" :
{
  "property1": "@parameters('parameter1')"
}
```

 Les paramètres peuvent également être utilisés dans les sorties.  
  
## <a name="triggers-and-actions"></a>Déclencheurs et actions  

Déclencheurs et actions spécifient les appels de hello qui peuvent participer à l’exécution du flux de travail. Pour plus d’informations sur cette section, consultez la page [Actions et déclencheurs de flux de travail](logic-apps-workflow-actions-triggers.md).
  
## <a name="outputs"></a>Sorties  

Les sorties spécifient les informations qui peuvent être retournées à partir de l’exécution d’un flux de travail. Par exemple, si vous avez un état spécifique ou la valeur que vous voulez tootrack pour chaque exécution, vous pouvez inclure que les données Bonjour se sorties. les données de salutation s’affiche dans hello API REST de gestion pour qui s’exécutent et interface utilisateur de gestion hello pour qui s’exécutent dans hello portail Azure. Vous pouvez également transmettre ces sorties tooother des systèmes externes telles que Power BI pour la création de tableaux de bord. Sorties sont *pas* utilisé toorespond tooincoming demandes sur hello API REST du Service. demande entrante de toorespond tooan à l’aide de hello `response` type d’action, Voici un exemple :
  
```json
"outputs": {  
  "key1": {  
    "value": "value1",  
    "type" : "<type-of-value>"  
  }  
} 
```

|Nom de l'élément|Requis|Description|  
|------------------|--------------|-----------------|  
|key1|Oui|Spécifie l’identificateur de clé hello pour la sortie de hello. Remplacez **key1** avec un nom que vous souhaitez sortie de toouse tooidentify hello.|  
|value|Oui|Spécifie la valeur hello de sortie de hello.|  
|type|Oui|Spécifie le type hello pour valeur hello qui a été spécifié. Types de valeur possibles : <ul><li>`string`</li><li>`securestring`</li><li>`int`</li><li>`bool`</li><li>`array`</li><li>`object`</li></ul>|
  
## <a name="expressions"></a>Expressions  

Les valeurs JSON dans la définition de hello peuvent être un littérales ou ils peuvent être des expressions qui sont évaluées lors de la définition de hello est utilisée. Par exemple :  
  
```json
"name": "value"
```

 ou  
  
```json
"name": "@parameters('password') "
```

> [!NOTE]
> Certaines expressions obtiennent leurs valeurs à partir d’actions de runtime qui n’existe ne peut-être pas au début de hello de l’exécution de hello. Vous pouvez utiliser **fonctions** toohelp récupérer certaines de ces valeurs.  
  
Les expressions peuvent apparaître n’importe où dans une valeur de chaîne JSON, et entraînent toujours une autre valeur JSON. Lorsqu’une valeur JSON a été déterminé toobe une expression, corps hello d’expression de hello est extrait en supprimant hello arobase (@). Si une chaîne littérale devant commencer par @ est nécessaire, elle doit être placée dans une séquence d’échappement en utilisant @@. Hello exemples suivants montrent comment les expressions sont évaluées.  
  
|Valeur JSON|Résultat|  
|----------------|------------|  
|« parameters »|Hello caractères « parameters » sont retournés.|  
|« parameters[1] »|Hello caractères « parameters [1] » sont renvoyés.|  
|« @@ »|Une chaîne de 1 caractère contenant « @ » est retournée.|  
|«  @ »|Une chaîne de 2 caractères contenant «  @ » est retournée.|  
  
Avec l’*interpolation de chaîne*, les expressions peuvent également apparaître dans des chaînes où les expressions sont encapsulées dans `@{ ... }`. Par exemple : <p>`"name" : "First Name: @{parameters('firstName')} Last Name: @{parameters('lastName')}"`

Hello résultat est toujours une chaîne, ce qui rend cette toohello similaire fonctionnalité `concat` (fonction). Supposons que vous avez défini `myNumber` sur `42` et `myString` sur `sampleString` :  
  
|Valeur JSON|Résultat|  
|----------------|------------|  
|« @parameters('myString') »|Retourne `sampleString` en tant que chaîne.|  
|« @{parameters('myString')} »|Retourne `sampleString` en tant que chaîne.|  
|« @parameters('myNumber') »|Retourne `42` en tant que *nombre*.|  
|« @{parameters('myNumber')} »|Retourne `42` en tant que *chaîne*.|  
|« Answer is: @{parameters('myNumber')} »|Retourne hello chaîne `Answer is: 42`.|  
|« @concat('Answer is: ', string(parameters('myNumber'))) »|Retourne la chaîne hello`Answer is: 42`|  
|« Answer is: @@{parameters('myNumber')} »|Retourne hello chaîne `Answer is: @{parameters('myNumber')}`.|  
  
## <a name="operators"></a>Operators  

Les opérateurs sont des caractères hello que vous pouvez utiliser à l’intérieur des expressions ou des fonctions. 
  
|Operator|Description|  
|--------------|-----------------|  
|.|opérateur de point Hello vous permet de tooreference les propriétés d’un objet|  
|?|opérateur de point d’interrogation Hello vous permet de référencer des propriétés de valeur null d’un objet sans qu’une erreur d’exécution. Par exemple, vous pouvez utiliser cette valeur de null toohandle expression déclenchent des sorties : <p>`@coalesce(trigger().outputs?.body?.property1, 'my default value')`|  
|'|guillemet simple Hello est hello seule façon toowrap les littéraux de chaîne. Vous ne pouvez pas utiliser des guillemets doubles à l’intérieur d’expressions car ce signe de ponctuation est en conflit avec les devis JSON hello qui encapsule l’expression entière hello.|  
|[]|crochets Hello peut être utilisé tooget une valeur à partir d’un tableau avec un index spécifique. Par exemple, si vous disposez d’une action qui passe `range(0,10)`dans toohello `forEach` (fonction), vous pouvez utiliser cette fonction tooget extraire les éléments de tableaux :  <p>`myArray[item()]`|  
  
## <a name="functions"></a>Fonctions  

Vous pouvez également appeler des fonctions dans des expressions. Hello tableau suivant répertorie les fonctions hello qui peuvent être utilisées dans une expression.  
  
|Expression|Évaluation|  
|----------------|----------------|  
|« @function('Hello') »|Appels hello fonction membre de définition hello avec la chaîne littérale de hello Hello en tant que premier paramètre de hello.|  
|« @function('C’est cool !') »|Appelle hello fonction membre de définition de hello avec la chaîne littérale de hello 'il est utile !' en tant que premier paramètre de hello|  
|« @function().prop1 »|Retourne hello la valeur de la propriété prop1 hello hello `myfunction` membre de la définition de hello.|  
|« @function('Hello').prop1 »|Appels hello fonction membre de définition de hello avec la chaîne littérale de hello « Bonjour » comme hello premier paramètre et retourne hello propriété prop1 de l’objet de hello.|  
|« @function(parameters('Hello')) »|Évalue le paramètre de Hello hello et transmet hello valeur toofunction|  
  
### <a name="referencing-functions"></a>Fonctions de référencement  

Vous pouvez utiliser ces sorties tooreference de fonctions à partir d’autres actions d’application logique de hello ou des valeurs passées lors de l’application de hello logique a été créée. Par exemple, vous pouvez référencer les données de salutation à partir d’une seule étape toouse dans un autre.  
  
|Nom de la fonction|Description|  
|-------------------|-----------------|  
|parameters|Retourne une valeur de paramètre qui est définie dans la définition de hello. <p>`parameters('password')` <p> **Numéro du paramètre** : 1 <p> **Nom** : paramètre <p> **Description** : obligatoire. nom de Hello du paramètre de hello dont vous souhaitez que les valeurs.|  
|action|Permet à un tooderive expression sa valeur à partir d’autres nom JSON et les paires de valeur ou sortie hello d’action d’exécution actuel hello. propriété Hello représentée par propertyPath Bonjour l’exemple suivant est facultative. Si propertyPath n’est pas spécifié, référence de hello est objet de toute action toohello. Cette fonction ne peut être utilisée que dans les conditions do-until d’une action. <p>`action().outputs.body.propertyPath`|  
|actions|Permet à un tooderive expression sa valeur à partir d’autres nom JSON et les paires de valeur ou sortie hello d’action du runtime hello. Ces expressions déclarent explicitement qu’une action dépend d’une autre action. propriété Hello représentée par propertyPath Bonjour l’exemple suivant est facultative. Si propertyPath n’est pas spécifié, référence de hello est objet de toute action toohello. Vous pouvez utiliser soit cet élément ou hello les dépendances de toospecify élément conditions, mais vous n’avez pas besoin de toouse à la fois pour hello même ressource dépendante. <p>`actions('myAction').outputs.body.propertyPath` <p> **Numéro du paramètre** : 1 <p> **Nom** : nom de l’action <p> **Description** : obligatoire. nom Hello de l’action hello dont vous souhaitez que les valeurs. <p> Les propriétés disponibles sur l’objet d’action hello sont : <ul><li>`name`</li><li>`startTime`</li><li>`endTime`</li><li>`inputs`</li><li>`outputs`</li><li>`status`</li><li>`code`</li><li>`trackingId`</li><li>`clientTrackingId`</li></ul> <p>Consultez hello [API Rest](http://go.microsoft.com/fwlink/p/?LinkID=850646) pour plus d’informations sur ces propriétés.|
|trigger|Permet à un tooderive expression sa valeur à partir d’autres nom JSON et les paires de valeur ou sortie hello du déclencheur de runtime hello. propriété Hello représentée par propertyPath Bonjour l’exemple suivant est facultative. Si propertyPath n’est pas spécifié, référence de hello est objet de déclencheur entier toohello. <p>`trigger().outputs.body.propertyPath` <p>Lorsqu’il est utilisé dans les entrées d’un déclencheur, fonction hello retourne les sorties hello de l’exécution précédente de hello. Toutefois, lorsqu’il est utilisé à l’intérieur de condition d’un déclencheur, hello `trigger` fonction retourne les sorties hello d’exécution actuel de hello. <p> Les propriétés disponibles sur l’objet de déclencheur hello sont : <ul><li>`name`</li><li>`scheduledTime`</li><li>`startTime`</li><li>`endTime`</li><li>`inputs`</li><li>`outputs`</li><li>`status`</li><li>`code`</li><li>`trackingId`</li><li>`clientTrackingId`</li></ul> <p>Consultez hello [API Rest](http://go.microsoft.com/fwlink/p/?LinkID=850644) pour plus d’informations sur ces propriétés.|
|actionOutputs|Cette fonction est la version raccourcie de `actions('actionName').outputs`. <p> **Numéro du paramètre** : 1 <p> **Nom** : nom de l’action <p> **Description** : obligatoire. nom Hello de l’action hello dont vous souhaitez que les valeurs.|  
|actionBody et body|Ces fonctions sont les versions raccourcies de `actions('actionName').outputs.body`. <p> **Numéro du paramètre** : 1 <p> **Nom** : nom de l’action <p> **Description** : obligatoire. nom Hello de l’action hello dont vous souhaitez que les valeurs.|  
|triggerOutputs|Cette fonction est la version raccourcie de `trigger().outputs`.|  
|triggerBody|Cette fonction est la version raccourcie de `trigger().outputs.body`.|  
|item|Lorsqu’il est utilisé à l’intérieur d’une action extensible, cette fonction retourne élément hello qui se trouve dans le tableau hello pour cette itération de l’action de hello. Par exemple, si l’une de vos actions s’exécute pour chaque élément d’un tableau de messages, vous pouvez utiliser cette syntaxe : <p>`"input1" : "@item().subject"`| 
  
### <a name="collection-functions"></a>Fonctions de collection  

Ces fonctions opèrent sur des collections et s’appliquent généralement tooArrays, des chaînes et parfois des dictionnaires.  
  
|Nom de la fonction|Description|  
|-------------------|-----------------|  
|contains|Retourne la valeur true si le dictionnaire contient une clé, si la liste contient une valeur ou si la chaîne contient une sous-chaîne. Par exemple, cette fonction retourne `true` : <p>`contains('abacaba','aca')` <p> **Numéro du paramètre** : 1 <p> **Nom** : au sein de la collection <p> **Description** : obligatoire. toosearch de collection Hello dans. <p> **Numéro du paramètre** : 2 <p> **Nom** : rechercher un objet <p> **Description** : obligatoire. Hello toofind d’objet à l’intérieur de hello **au sein de la collection**.|  
|length|Retourne hello nombre d’éléments dans un tableau ou une chaîne. Par exemple, cette fonction retourne `3` :  <p>`length('abc')` <p> **Numéro du paramètre** : 1 <p> **Nom** : collection <p> **Description** : obligatoire. collection de Hello pour les caractères tooget hello.|  
|empty|Retourne la valeur true si l’objet, le tableau ou la chaîne est vide. Par exemple, cette fonction retourne `true` : <p>`empty('')` <p> **Numéro du paramètre** : 1 <p> **Nom** : collection <p> **Description** : obligatoire. Bonjour toocheck de collection si elle est vide.|  
|intersection|Retourne un tableau ou un objet unique qui contient des éléments communs transmis entre les tableaux ou les objets. Par exemple, cette fonction retourne `[1, 2]` : <p>`intersection([1, 2, 3], [101, 2, 1, 10],[6, 8, 1, 2])` <p>les paramètres pour la fonction hello Hello peuvent être un ensemble d’objets ou un ensemble de tableaux (pas une combinaison des deux). S’il existe deux objets de hello même nom, hello dernier objet avec ce nom s’affiche dans l’objet de final hello. <p> **Numéro du paramètre** : 1 ... *n* <p> **Nom** : collection *n* <p> **Description** : obligatoire. Hello collections tooevaluate. Un objet doit être dans toutes les collections sont passées dans tooappear dans le résultat de hello.|  
|union|Renvoie un tableau à une seule ou avec tous les éléments de hello qui sont passés dans un tableau ou un objet toothis (fonction). Par exemple, cette fonction retourne `[1, 2, 3, 10, 101]` : <p>`union([1, 2, 3], [101, 2, 1, 10])` <p>les paramètres pour la fonction hello Hello peuvent être un ensemble d’objets ou un ensemble de tableaux (pas un mélange son). S’il existe deux objets de même nom que celui de hello dans la sortie finale hello, hello dernier objet avec ce nom s’affiche dans l’objet de final hello. <p> **Numéro du paramètre** : 1 ... *n* <p> **Nom** : collection *n* <p> **Description** : obligatoire. Hello collections tooevaluate. Objet qui apparaît dans une des collections de hello apparaît également dans le résultat de hello.|  
|first|Retourne hello le premier élément de tableau de hello ou chaîne passée. Par exemple, cette fonction retourne `0` : <p>`first([0,2,3])` <p> **Numéro du paramètre** : 1 <p> **Nom** : collection <p> **Description** : obligatoire. Hello tootake hello premier objet de collection à partir de.|  
|last|Retourne hello le dernier élément dans le tableau de hello ou chaîne passée. Par exemple, cette fonction retourne `3` : <p>`last('0123')` <p> **Numéro du paramètre** : 1 <p> **Nom** : collection <p> **Description** : obligatoire. Hello tootake hello dernier objet de collection à partir de.|  
|take|Retourne hello tout d’abord **nombre** les éléments d’un tableau de hello ou une chaîne passée. Par exemple, cette fonction retourne `[1, 2]` :  <p>`take([1, 2, 3, 4], 2)` <p> **Numéro du paramètre** : 1 <p> **Nom** : collection <p> **Description** : obligatoire. collection Hello où tootake hello tout d’abord **nombre** objets. <p> **Numéro du paramètre** : 2 <p> **Nom** : nombre <p> **Description** : obligatoire. Hello nombre de tootake d’objets à partir de hello **Collection**. Cette valeur doit être un entier positif.|  
|skip|Retourne hello des éléments dans le tableau de hello en commençant à l’index **nombre**. Par exemple, cette fonction retourne `[3, 4]` : <p>`skip([1, 2 ,3 ,4], 2)` <p> **Numéro du paramètre** : 1 <p> **Nom** : collection <p> **Description** : obligatoire. Hello hello tooskip de collection tout d’abord **nombre** à partir des objets. <p> **Numéro du paramètre** : 2 <p> **Nom** : nombre <p> **Description** : obligatoire. Hello nombre de tooremove objets début hello de **Collection**. Cette valeur doit être un entier positif.|  
|join|Retourne une chaîne avec chaque élément d’un tableau joint par un délimiteur. Par exemple, cette fonction retourne `"1,2,3,4"` :<br /><br /> `join([1, 2, 3, 4], ',')`<br /><br /> **Numéro du paramètre** : 1<br /><br /> **Nom** : collection<br /><br /> **Description** : obligatoire. Hello collection toojoin des éléments de.<br /><br /> **Numéro du paramètre** : 2<br /><br /> **Nom** : délimiteur<br /><br /> **Description** : obligatoire. éléments toodelimit type chaîne Hello avec.|  
  
### <a name="string-functions"></a>Fonctions de chaîne

Hello suivant uniquement les fonctions s’appliquent toostrings. Vous pouvez également appliquer certaines fonctions de collection aux chaînes.  
  
|Nom de la fonction|Description|  
|-------------------|-----------------|  
|concat|Combine plusieurs chaînes. Par exemple, si le paramètre 1 est `p1`, cette fonction retourne `somevalue-p1-somevalue` : <p>`concat('somevalue-',parameters('parameter1'),'-somevalue')` <p> **Numéro du paramètre** : 1 ... *n* <p> **Nom** : chaîne *n* <p> **Description** : obligatoire. Hello toocombine de chaînes en une seule chaîne.|  
|substring|Retourne un sous-ensemble de caractères d’une chaîne. Par exemple, cette fonction retourne `abc` : <p>`substring('somevalue-abc-somevalue',10,3)` <p> **Numéro du paramètre** : 1 <p> **Nom** : chaîne <p> **Description** : obligatoire. chaîne Hello à partir de quels hello sous-chaîne est effectuée. <p> **Numéro du paramètre** : 2 <p> **Nom** : index de début <p> **Description** : obligatoire. index de Hello d’où la sous-chaîne de hello commence dans le paramètre 1. <p> **Numéro du paramètre** : 3 <p> **Nom** : longueur <p> **Description** : obligatoire. longueur de Hello de sous-chaîne de hello.|  
|replace|Remplace une chaîne par une chaîne donnée. Par exemple, cette fonction retourne `hello new string` : <p>`replace('hello old string', 'old', 'new')` <p> **Numéro du paramètre** : 1 <p> **Nom** : chaîne <p> **Description** : obligatoire. chaîne Hello qui est recherché dans le paramètre 2 et mis à jour avec le paramètre 3, lorsque le paramètre 2 est trouvé dans le paramètre 1. <p> **Numéro du paramètre** : 2 <p> **Nom** : ancienne chaîne <p> **Description** : obligatoire. Hello tooreplace chaîne avec le paramètre 3, lorsqu’une correspondance est trouvée dans le paramètre 1 <p> **Numéro du paramètre** : 3 <p> **Nom** : nouvelle chaîne <p> **Description** : obligatoire. Hello chaîne qui est chaîne hello de tooreplace utilisé dans le paramètre 2 lorsqu’une correspondance est trouvée dans le paramètre 1.|  
|guid|Cette fonction génère une chaîne globale unique (GUID). Par exemple, cette fonction peut générer ce GUID : `c2ecc88d-88c8-4096-912c-d6f2e2b138ce` <p>`guid()` <p> **Numéro du paramètre** : 1 <p> **Nom** : format <p> **Description** : facultatif. Spécificateur de format unique qui indique [comment tooformat hello la valeur de ce Guid](https://msdn.microsoft.com/library/97af8hh4%28v=vs.110%29.aspx). paramètre de format Hello peut être « N », « D », « B », « P » ou « X ». Si aucun format n’est indiqué, « D » est utilisé.|  
|toLower|Convertit une chaîne de toolowercase. Par exemple, cette fonction retourne `two by two is four` : <p>`toLower('Two by Two is Four')` <p> **Numéro du paramètre** : 1 <p> **Nom** : chaîne <p> **Description** : obligatoire. casse de toolower chaîne tooconvert Hello. Si un caractère de chaîne de hello n’a pas d’équivalent en minuscules, caractères de hello est inclus inchangé dans hello a retourné une chaîne.|  
|toUpper|Convertit une chaîne de toouppercase. Par exemple, cette fonction retourne `TWO BY TWO IS FOUR` : <p>`toUpper('Two by Two is Four')` <p> **Numéro du paramètre** : 1 <p> **Nom** : chaîne <p> **Description** : obligatoire. casse de tooupper chaîne tooconvert Hello. Si un caractère de chaîne de hello n’a pas d’équivalent en majuscules, caractères de hello est inclus inchangé dans hello a retourné une chaîne.|  
|indexof|Vous permet de trouver ce index hello d’une valeur dans un cas de chaîne. Par exemple, cette fonction retourne `7` : <p>`indexof('hello, world.', 'world')` <p> **Numéro du paramètre** : 1 <p> **Nom** : chaîne <p> **Description** : obligatoire. chaîne Hello qui peut contenir de valeur de hello. <p> **Numéro du paramètre** : 2 <p> **Nom** : chaîne <p> **Description** : obligatoire. index de hello toosearch Hello valeur de.|  
|lastindexof|Vous permet de trouver ce hello dernier index d’une valeur dans un cas de chaîne. Par exemple, cette fonction retourne `3` : <p>`lastindexof('foofoo', 'foo')` <p> **Numéro du paramètre** : 1 <p> **Nom** : chaîne <p> **Description** : obligatoire. chaîne Hello qui peut contenir de valeur de hello. <p> **Numéro du paramètre** : 2 <p> **Nom** : chaîne <p> **Description** : obligatoire. index de hello toosearch Hello valeur de.|  
|startswith|Vérifie si la chaîne de hello démarre ce à un cas de valeur. Par exemple, cette fonction retourne `true` : <p>`startswith('hello, world', 'hello')` <p> **Numéro du paramètre** : 1 <p> **Nom** : chaîne <p> **Description** : obligatoire. chaîne Hello qui peut contenir de valeur de hello. <p> **Numéro du paramètre** : 2 <p> **Nom** : chaîne <p> **Description** : obligatoire. chaîne de hello valeur Hello peut commencer.|  
|endswith|Vérifie si la chaîne de hello se termine avec un cas de valeur ce. Par exemple, cette fonction retourne `true` : <p>`endswith('hello, world', 'world')` <p> **Numéro du paramètre** : 1 <p> **Nom** : chaîne <p> **Description** : obligatoire. chaîne Hello qui peut contenir de valeur de hello. <p> **Numéro du paramètre** : 2 <p> **Nom** : chaîne <p> **Description** : obligatoire. chaîne de hello valeur Hello peut se terminer par.|  
|split|Fractionne la chaîne hello à l’aide d’un séparateur. Par exemple, cette fonction retourne `["a", "b", "c"]` : <p>`split('a;b;c',';')` <p> **Numéro du paramètre** : 1 <p> **Nom** : chaîne <p> **Description** : obligatoire. chaîne Hello qui est fractionnée. <p> **Numéro du paramètre** : 2 <p> **Nom** : chaîne <p> **Description** : obligatoire. séparateur de Hello.|  
  
### <a name="logical-functions"></a>Fonctions logiques  

Ces fonctions sont utiles dans les conditions et peuvent être utilisé tooevaluate n’importe quel type de logique.  
  
|Nom de la fonction|Description|  
|-------------------|-----------------|  
|equals|Retourne la valeur true si deux valeurs sont égales. Par exemple, si parameter1 est égal à someValue, cette fonction retourne `true` : <p>`equals(parameters('parameter1'), 'someValue')` <p> **Numéro du paramètre** : 1 <p> **Nom** : objet 1 <p> **Description** : obligatoire. Hello toocompare d’objet trop**objet 2**. <p> **Numéro du paramètre** : 2 <p> **Nom** : objet 2 <p> **Description** : obligatoire. Hello toocompare d’objet trop**1 de l’objet**.|  
|less|Retourne true si le premier argument de hello est inférieure à hello le second. Les valeurs ne peuvent être que du type entier, flottant ou chaîne. Par exemple, cette fonction retourne `true` : <p>`less(10,100)` <p> **Numéro du paramètre** : 1 <p> **Nom** : objet 1 <p> **Description** : obligatoire. Hello objet toocheck si elle est inférieure à **objet 2**. <p> **Numéro du paramètre** : 2 <p> **Nom** : objet 2 <p> **Description** : obligatoire. Hello objet toocheck si elle est supérieure à **1 de l’objet**.|  
|lessOrEquals|Retourne la valeur true si le premier argument de hello est inférieur ou égal à toohello seconde. Les valeurs ne peuvent être que du type entier, flottant ou chaîne. Par exemple, cette fonction retourne `true` : <p>`lessOrEquals(10,10)` <p> **Numéro du paramètre** : 1 <p> **Nom** : objet 1 <p> **Description** : obligatoire. Hello objet toocheck si elle est inférieure ou égale à trop**objet 2**. <p> **Numéro du paramètre** : 2 <p> **Nom** : objet 2 <p> **Description** : obligatoire. Hello toocheck de l’objet s’il est supérieur ou égal à trop**1 de l’objet**.|  
|greater|Retourne la valeur true si hello premier argument est supérieur à hello ensuite. Les valeurs ne peuvent être que du type entier, flottant ou chaîne. Par exemple, cette fonction retourne `false` :  <p>`greater(10,10)` <p> **Numéro du paramètre** : 1 <p> **Nom** : objet 1 <p> **Description** : obligatoire. Hello objet toocheck si elle est supérieure à **objet 2**. <p> **Numéro du paramètre** : 2 <p> **Nom** : objet 2 <p> **Description** : obligatoire. Hello objet toocheck si elle est inférieure à **1 de l’objet**.|  
|greaterOrEquals|Retourne la valeur true si hello premier argument est supérieur ou égal toohello ensuite. Les valeurs ne peuvent être que du type entier, flottant ou chaîne. Par exemple, cette fonction retourne `false` : <p>`greaterOrEquals(10,100)` <p> **Numéro du paramètre** : 1 <p> **Nom** : objet 1 <p> **Description** : obligatoire. Hello toocheck de l’objet s’il est supérieur ou égal à trop**objet 2**. <p> **Numéro du paramètre** : 2 <p> **Nom** : objet 2 <p> **Description** : obligatoire. Hello toocheck de l’objet s’il est inférieur ou égal trop**1 de l’objet**.|  
|and|Retourne la valeur true si les deux paramètres sont true. Les deux arguments doivent être toobe booléens. Par exemple, cette fonction retourne `false` : <p>`and(greater(1,10),equals(0,0))` <p> **Numéro du paramètre** : 1 <p> **Nom** : booléen 1 <p> **Description** : obligatoire. premier argument doit être de Hello `true`. <p> **Numéro du paramètre** : 2 <p> **Nom** : booléen 2 <p> **Description** : obligatoire. Hello second argument doit être `true`.|  
|ou|Retourne la valeur true si l’un ou l’autre des paramètres est true. Les deux arguments doivent être toobe booléens. Par exemple, cette fonction retourne `true` : <p>`or(greater(1,10),equals(0,0))` <p> **Numéro du paramètre** : 1 <p> **Nom** : booléen 1 <p> **Description** : obligatoire. Hello du premier argument qui peut-être être `true`. <p> **Numéro du paramètre** : 2 <p> **Nom** : booléen 2 <p> **Description** : obligatoire. Hello second argument peut être `true`.|  
|not|Retourne la valeur true si les paramètres de hello sont `false`. Les deux arguments doivent être toobe booléens. Par exemple, cette fonction retourne `true` : <p>`not(contains('200 Success','Fail'))` <p> **Numéro du paramètre** : 1 <p> **Nom** : booléen <p> **Description**: renvoie la valeur true si les paramètres de hello sont `false`. Les deux arguments doivent être toobe booléens. Cette fonction retourne `true` : `not(contains('200 Success','Fail'))`|  
|if|Retourne une valeur spécifiée en fonction de si expression de hello a entraîné `true` ou `false`.  Par exemple, cette fonction retourne `"yes"` : <p>`if(equals(1, 1), 'yes', 'no')` <p> **Numéro du paramètre** : 1 <p> **Nom** : expression <p> **Description** : obligatoire. Valeur booléenne qui détermine l’expression valeur hello doit retourner. <p> **Numéro du paramètre** : 2 <p> **Nom** : true <p> **Description** : obligatoire. Hello valeur tooreturn si l’expression de hello est `true`. <p> **Numéro du paramètre** : 3 <p> **Nom** : false <p> **Description** : obligatoire. Hello valeur tooreturn si l’expression de hello est `false`.|  
  
### <a name="conversion-functions"></a>Fonctions de conversion  

Ces fonctions sont utilisée tooconvert entre chacun des types natifs de hello en langage de hello :  
  
- string  
  
- integer  
  
- float  
  
- booléenne  
  
- tableaux  
  
- dictionnaires  

-   formulaires  
  
|Nom de la fonction|Description|  
|-------------------|-----------------|  
|int|Convertit un entier de type hello paramètre tooan. Par exemple, cette fonction retourne 100 sous forme de nombre plutôt que sous forme de chaîne : <p>`int('100')` <p> **Numéro du paramètre** : 1 <p> **Nom** : valeur <p> **Description** : obligatoire. valeur Hello converti tooan entière.|  
|string|Convertir la chaîne hello paramètres tooa. Par exemple, cette fonction retourne `'10'` : <p>`string(10)` <p>Vous pouvez également convertir une chaîne tooa d’objet. Par exemple, si hello `myPar` paramètre est un objet avec une propriété `abc : xyz`, cette fonction retourne `{"abc" : "xyz"}`: <p>`string(parameters('myPar'))` <p> **Numéro du paramètre** : 1 <p> **Nom** : valeur <p> **Description** : obligatoire. Hello valeur qui est converti tooa chaîne.|  
|json|Convertir la valeur de type hello paramètre tooa JSON et est hello opposé de `string()`. Par exemple, cette fonction retourne `[1,2,3]` sous forme de tableau plutôt que sous forme de chaîne : <p>`json('[1,2,3]')` <p>De même, vous pouvez convertir un objet de tooan string. Par exemple, cette fonction retourne `{ "abc" : "xyz" }` : <p>`json('{"abc" : "xyz"}')` <p> **Numéro du paramètre** : 1 <p> **Nom** : chaîne <p> **Description** : obligatoire. Hello chaîne qui est de valeur de type natif tooa converti. <p>Hello `json()` fonction prend en charge XML d’entrée trop. Par exemple, hello valeur de paramètre : <p>`<?xml version="1.0"?> <root>   <person id='1'>     <name>Alan</name>     <occupation>Engineer</occupation>   </person> </root>` <p>est converti toothis JSON : <p>`{ "?xml": { "@version": "1.0" },   "root": {     "person": [     {       "@id": "1",       "name": "Alan",       "occupation": "Engineer"     }   ]   } }`|  
|float|Convertir un nombre à virgule flottante de hello paramètre argument tooa. Par exemple, cette fonction retourne `10.333` : <p>`float('10.333')` <p> **Numéro du paramètre** : 1 <p> **Nom** : valeur <p> **Description** : obligatoire. Hello valeur nombre à virgule flottante de tooa converti.|  
|bool|Convertir hello tooa de paramètre de type Boolean. Par exemple, cette fonction retourne `false` : <p>`bool(0)` <p> **Numéro du paramètre** : 1 <p> **Nom** : valeur <p> **Description** : obligatoire. Hello converti tooa valeur booléenne.|  
|coalesce|Retourne l’objet non null de la première hello dans des arguments de hello passés dans. **Remarque** : une chaîne vide n’a pas la valeur Null. Par exemple, si les paramètres 1 et 2 ne sont pas définis, cette fonction retourne `fallback` :  <p>`coalesce(parameters('parameter1'), parameters('parameter2') ,'fallback')` <p> **Numéro du paramètre** : 1 ... *n* <p> **Nom** : objet *n* <p> **Description** : obligatoire. toocheck d’objets Hello pour la valeur null.|  
|base64|Retourne hello représentation en base64 de la chaîne d’entrée de hello. Par exemple, cette fonction retourne `c29tZSBzdHJpbmc=` : <p>`base64('some string')` <p> **Numéro du paramètre** : 1 <p> **Nom** : chaîne 1 <p> **Description** : obligatoire. tooencode de chaîne Hello dans la représentation en base 64.|  
|base64ToBinary|Retourne une représentation binaire d’une chaîne encodée en base64. Par exemple, cette fonction retourne la représentation binaire de hello `some string`: <p>`base64ToBinary('c29tZSBzdHJpbmc=')` <p> **Numéro du paramètre** : 1 <p> **Nom** : chaîne <p> **Description** : obligatoire. chaîne encodée base64 de Hello.|  
|base64ToString|Retourne une représentation de chaîne d’une chaîne encodée en base64. Par exemple, cette fonction retourne `some string` : <p>`base64ToString('c29tZSBzdHJpbmc=')` <p> **Numéro du paramètre** : 1 <p> **Nom** : chaîne <p> **Description** : obligatoire. chaîne encodée base64 de Hello.|  
|Binary|Retourne une représentation binaire d’une valeur.  Par exemple, cette fonction retourne une représentation binaire de `some string` : <p>`binary('some string')` <p> **Numéro du paramètre** : 1 <p> **Nom** : valeur <p> **Description** : obligatoire. valeur Hello toobinary converti.|  
|dataUriToBinary|Retourne une représentation binaire d’un URI de données. Par exemple, cette fonction retourne la représentation binaire de hello `some string`: <p>`dataUriToBinary('data:;base64,c29tZSBzdHJpbmc=')` <p> **Numéro du paramètre** : 1 <p> **Nom** : chaîne <p> **Description** : obligatoire. représentation sous forme de URI tooconvert toobinary les données de salutation.|  
|dataUriToString|Retourne une représentation de chaîne d’un URI de données. Par exemple, cette fonction retourne `some string` : <p>`dataUriToString('data:;base64,c29tZSBzdHJpbmc=')` <p> **Numéro du paramètre** : 1 <p> **Nom** : chaîne<p> **Description** : obligatoire. représentation sous forme de URI tooconvert tooString les données de salutation.|  
|dataUri|Retourne un URI de données d’une valeur. Par exemple, cette fonction retourne cet URI de données `text/plain;charset=utf8;base64,c29tZSBzdHJpbmc=` : <p>`dataUri('some string')` <p> **Numéro du paramètre** : 1<p> **Nom** : valeur<p> **Description** : obligatoire. Hello valeur tooconvert toodata URI.|  
|decodeBase64|Retourne une représentation de chaîne d’une chaîne en base64 d’entrée. Par exemple, cette fonction retourne `some string` : <p>`decodeBase64('c29tZSBzdHJpbmc=')` <p> **Numéro du paramètre** : 1 <p> **Nom** : chaîne <p> **Description** : retourne une représentation de chaîne d’une chaîne en base64 d’entrée.|  
|encodeUriComponent|Chaîne hello d’échappement de l’URL qui est passé. Par exemple, cette fonction retourne `You+Are%3ACool%2FAwesome` : <p>`encodeUriComponent('You Are:Cool/Awesome')` <p> **Numéro du paramètre** : 1 <p> **Nom** : chaîne <p> **Description** : obligatoire. Hello chaîne tooescape unsafe pour l’URL des caractères à partir de.|  
|decodeUriComponent|Chaîne n’URL échappe pas hello qui est passé. Par exemple, cette fonction retourne `You Are:Cool/Awesome` : <p>`encodeUriComponent('You+Are%3ACool%2FAwesome')` <p> **Numéro du paramètre** : 1 <p> **Nom** : chaîne <p> **Description** : obligatoire. Hello toodecode hello unsafe pour l’URL des caractères de chaîne à partir de.|  
|decodeDataUri|Retourne une représentation binaire d’une chaîne d’URI de données d’entrée. Par exemple, cette fonction retourne la représentation binaire de hello `some string`: <p>`decodeDataUri('data:;base64,c29tZSBzdHJpbmc=')` <p> **Numéro du paramètre** : 1 <p> **Nom** : chaîne <p> **Description** : obligatoire. Bonjour dataURI toodecode en une représentation binaire.|  
|uriComponent|Retourne une représentation encodée d’URI d’une valeur. Par exemple, cette fonction retourne `You+Are%3ACool%2FAwesome` : <p>`uriComponent('You Are:Cool/Awesome')` <p> **Numéro du paramètre** : 1<p> **Nom** : chaîne <p> **Description** : obligatoire. toobe de chaîne Hello URI encodé.|  
|uriComponentToBinary|Retourne une représentation binaire d’une chaîne encodée d’URI. Par exemple, cette fonction retourne une représentation binaire de `You Are:Cool/Awesome` : <p>`uriComponentToBinary('You+Are%3ACool%2FAwesome')` <p> **Numéro du paramètre** : 1 <p> **Nom** : chaîne<p> **Description** : obligatoire. Hello URI de chaîne encodée.|  
|uriComponentToString|Retourne une représentation de chaîne d’une chaîne encodée d’URI. Par exemple, cette fonction retourne `You Are:Cool/Awesome` : <p>`uriComponentToBinary('You+Are%3ACool%2FAwesome')` <p> **Numéro du paramètre** : 1<p> **Nom** : chaîne<p> **Description** : obligatoire. Hello URI de chaîne encodée.|  
|xml|Retourne une représentation XML de la valeur de hello. Par exemple, cette fonction retourne du contenu XML représenté par `'\<name>Alan\</name>'` : <p>`xml('\<name>Alan\</name>')` <p>Hello `xml()` fonction prend en charge l’objet JSON d’entrée trop. Par exemple, hello paramètre `{ "abc": "xyz" }` n’est pas converti tooXML contenu :`\<abc>xyz\</abc>` <p> **Numéro du paramètre** : 1<p> **Nom** : valeur<p> **Description** : obligatoire. Hello valeur tooconvert tooXML.|  
|xpath|Retourne un tableau de nœuds XML expression xpath de hello d’une valeur hello xpath expression renvoie la valeur de correspondance. <p> **Exemple 1** <p>Supposons que la valeur hello du paramètre `p1` est une représentation sous forme de chaîne de ce code XML : <p>`<?xml version="1.0"?> <lab>   <robot>     <parts>5</parts>     <name>R1</name>   </robot>   <robot>     <parts>8</parts>     <name>R2</name>   </robot> </lab>` <p>Ce code : `xpath(xml(parameters('p1'), '/lab/robot/name')` <p>retourne <p>`[ <name>R1</name>, <name>R2</name> ]` <p>alors que ce code : <p>`xpath(xml(parameters('p1'), ' sum(/lab/robot/parts)')` <p>retourne <p>`13` <p> <p> **Exemple 2** <p>Hello donné suivant le contenu XML : <p>`<?xml version="1.0"?> <File xmlns="http://foo.com">   <Location>bar</Location> </File>` <p>Ce code : `@xpath(xml(body('Http')), '/*[name()=\"File\"]/*[name()=\"Location\"]')` <p>ou ce code : <p>`@xpath(xml(body('Http')), '/*[local-name()=\"File\" and namespace-uri()=\"http://foo.com\"]/*[local-name()=\"Location\" and namespace-uri()=\"\"]')` <p>retourne <p>`<Location xmlns="http://abc.com">xyz</Location>` <p>Et ce code : `@xpath(xml(body('Http')), 'string(/*[name()=\"File\"]/*[name()=\"Location\"])')` <p>retourne <p>``xyz`` <p> **Numéro du paramètre** : 1 <p> **Nom** : Xml <p> **Description** : obligatoire. XML Hello sur le tooevaluate hello XPath expression. <p> **Numéro du paramètre** : 2 <p> **Nom** : XPath <p> **Description** : obligatoire. Hello tooevaluate d’expression XPath.|  
|array|Convertir un tableau de tooan paramètre hello. Par exemple, cette fonction retourne `["abc"]` : <p>`array('abc')` <p> **Numéro du paramètre** : 1 <p> **Nom** : valeur <p> **Description** : obligatoire. valeur de Hello est converti tooan tableau.|
|createArray|Crée un tableau à partir des paramètres de hello. Par exemple, cette fonction retourne `["a", "c"]` : <p>`createArray('a', 'c')` <p> **Numéro du paramètre** : 1 ... *n* <p> **Nom** : tout *n* <p> **Description** : obligatoire. Hello toocombine de valeurs dans un tableau.|
|triggerFormDataValue|Retourne une valeur unique correspondant au nom de clé hello à partir des données de formulaire ou de sortie du format codé le déclencheur.  Retourne une erreur en cas de correspondances multiples.  Par exemple, syntaxe de hello ci-après renvoie `bar`:`triggerFormDataValue('foo')`<br /><br />**Numéro du paramètre** : 1<br /><br />**Nom** : nom de la clé<br /><br />**Description** : obligatoire. nom de la clé Hello de tooreturn de valeur de données de formulaire hello.|
|triggerFormDataMultiValues|Retourne un tableau de valeurs correspondant au nom de clé hello à partir des données de formulaire ou de sortie du format codé le déclencheur.  Par exemple, syntaxe de hello ci-après renvoie `["bar"]`:`triggerFormDataValue('foo')`<br /><br />**Numéro du paramètre** : 1<br /><br />**Nom** : nom de la clé<br /><br />**Description** : obligatoire. les valeurs de nom de la clé Hello hello des données de formulaire tooreturn.|
|triggerMultipartBody|Retourne hello du corps d’une partie dans une sortie en plusieurs parties du déclencheur de hello.<br /><br />**Numéro du paramètre** : 1<br /><br />**Nom** : index<br /><br />**Description** : obligatoire. index de Hello de hello partie tooretrieve.|
|formDataValue|Retourne une valeur unique correspondant au nom de clé hello à partir des données de formulaire ou le résultat de l’action de format codé.  Retourne une erreur en cas de correspondances multiples.  Par exemple, syntaxe de hello ci-après renvoie `bar`:`formDataValue('someAction', 'foo')`<br /><br />**Numéro du paramètre** : 1<br /><br />**Nom** : nom de l’action<br /><br />**Description** : obligatoire. nom Hello d’action hello avec des données de formulaire ou d’une réponse de format codé.<br /><br />**Numéro du paramètre** : 2<br /><br />**Nom** : nom de la clé<br /><br />**Description** : obligatoire. nom de la clé Hello de tooreturn de valeur de données de formulaire hello.|
|formDataMultiValues|Retourne un tableau de valeurs correspondant au nom de clé hello à partir des données de formulaire ou le résultat de l’action de format codé.  Par exemple, syntaxe de hello ci-après renvoie `["bar"]`:`formDataMultiValues('someAction', 'foo')`<br /><br />**Numéro du paramètre** : 1<br /><br />**Nom** : nom de l’action<br /><br />**Description** : obligatoire. nom Hello d’action hello avec des données de formulaire ou d’une réponse de format codé.<br /><br />**Numéro du paramètre** : 2<br /><br />**Nom** : nom de la clé<br /><br />**Description** : obligatoire. les valeurs de nom de la clé Hello hello des données de formulaire tooreturn.|
|multipartBody|Retourne hello du corps d’une partie dans une sortie en plusieurs parties d’une action.<br /><br />**Numéro du paramètre** : 1<br /><br />**Nom** : nom de l’action<br /><br />**Description** : obligatoire. nom Hello d’action hello avec une réponse en plusieurs parties.<br /><br />**Numéro du paramètre** : 2<br /><br />**Nom** : index<br /><br />**Description** : obligatoire. index de Hello de hello partie tooretrieve.|

### <a name="math-functions"></a>Fonctions mathématiques  

Ces fonctions peuvent être utilisées pour les deux types de nombre : **entiers** et **flottants**.  
  
|Nom de la fonction|Description|  
|-------------------|-----------------|  
|add|Retourne les résultats hello à partir de l’ajout de deux nombres de hello. Par exemple, cette fonction retourne `20.333` : <p>`add(10,10.333)` <p> **Numéro du paramètre** : 1 <p> **Nom** : opérande 1 <p> **Description** : obligatoire. Hello tooadd numéro trop**opérande 2**. <p> **Numéro du paramètre** : 2 <p> **Nom** : opérande 2 <p> **Description** : obligatoire. Hello tooadd numéro trop**opérande 1**.|  
|sub|Retourne les résultats hello de la soustraction de deux nombres. Par exemple, cette fonction retourne `-0.333` : <p>`sub(10,10.333)` <p> **Numéro du paramètre** : 1 <p> **Nom** : diminuende <p> **Description** : obligatoire. Hello numéro **diminuteur** est supprimé. <p> **Numéro du paramètre** : 2 <p> **Nom** : diminuteur <p> **Description** : obligatoire. Hello tooremove numéro de hello **diminuende**.|  
|mul|Retourne le résultat de hello de la multiplication de deux nombres de hello. Par exemple, cette fonction retourne `103.33` : <p>`mul(10,10.333)` <p> **Numéro du paramètre** : 1 <p> **Nom** : multiplicande 1 <p> **Description** : obligatoire. Hello numéro toomultiply **Multiplicande 2** avec. <p> **Numéro du paramètre** : 2 <p> **Nom** : multiplicande 2 <p> **Description** : obligatoire. Hello numéro toomultiply **Multiplicande 1** avec.|  
|div|Retourne le résultat de hello de la division de deux nombres de hello. Par exemple, cette fonction retourne `1.0333` : <p>`div(10.333,10)` <p> **Numéro du paramètre** : 1 <p> **Nom** : dividende <p> **Description** : obligatoire. Hello toodivide nombre par hello **diviseur**. <p> **Numéro du paramètre** : 2 <p> **Nom** : diviseur <p> **Description** : obligatoire. Bonjour numéro toodivide Bonjour **dividende** par.|  
|mod|Retourne le reste de hello après la division de deux nombres de hello (modulo). Par exemple, cette fonction retourne `2` : <p>`mod(10,4)` <p> **Numéro du paramètre** : 1 <p> **Nom** : dividende <p> **Description** : obligatoire. Hello toodivide nombre par hello **diviseur**. <p> **Numéro du paramètre** : 2 <p> **Nom** : diviseur <p> **Description** : obligatoire. Bonjour numéro toodivide Bonjour **dividende** par. Après la division de hello, le reste de hello est effectuée.|  
|Min|Il existe deux modèles différents pour appeler cette fonction. <p>Ici `min` prend un tableau, et la fonction hello retourne `0`: <p>`min([0,1,2])` <p>Cette fonction peut également extraire une liste de valeurs séparées par des virgules, et elle retourne aussi `0` : <p>`min(0,1,2)` <p> **Remarque**: toutes les valeurs doivent être des nombres, par conséquent, si le paramètre hello est un tableau, tableau de hello a tooonly avoir des nombres. <p> **Numéro du paramètre** : 1 <p> **Nom** : collection ou valeur <p> **Description** : obligatoire. Soit un tableau de valeurs toofind hello valeur minimale, soit hello la première valeur d’un jeu. <p> **Numéro du paramètre** : 2 ... *n* <p> **Nom** : valeur *n* <p> **Description** : facultatif. Si le premier paramètre de hello est une valeur, puis vous pouvez passer des valeurs supplémentaires et hello minimum de toutes les valeurs passées est retourné.|  
|max|Il existe deux modèles différents pour appeler cette fonction. <p>Ici `max` prend un tableau, et la fonction hello retourne `2`: <p>`max([0,1,2])` <p>Cette fonction peut également extraire une liste de valeurs séparées par des virgules, et elle retourne aussi `2` : <p>`max(0,1,2)` <p> **Remarque**: toutes les valeurs doivent être des nombres, par conséquent, si le paramètre hello est un tableau, tableau de hello a tooonly avoir des nombres. <p> **Numéro du paramètre** : 1 <p> **Nom** : collection ou valeur <p> **Description** : obligatoire. Soit un tableau de valeurs toofind hello valeur maximale, soit hello la première valeur d’un jeu. <p> **Numéro du paramètre** : 2 ... *n* <p> **Nom** : valeur *n* <p> **Description** : facultatif. Si le premier paramètre de hello est une valeur, puis vous pouvez passer des valeurs supplémentaires et hello toutes les valeurs passées au maximum est retourné.|  
|range|Génère un tableau d’entiers à partir d’un certain nombre. Vous définissez hello hello retourné du tableau. <p>Par exemple, cette fonction retourne `[3,4,5,6]` : <p>`range(3,4)` <p> **Numéro du paramètre** : 1 <p> **Nom** : index de début <p> **Description** : obligatoire. Hello premier entier hello tableau. <p> **Numéro du paramètre** : 2 <p> **Nom** : nombre <p> **Description** : obligatoire. Cette valeur est le nombre de hello d’entiers qui se trouve dans le tableau de hello.|  
|rand|Génère un aléatoire entier dans hello spécifié plage (limites incluses uniquement sur le premier fin). Par exemple, cette fonction peut retourner `0` ou '1' : <p>`rand(0,2)` <p> **Numéro du paramètre** : 1 <p> **Nom** : minimum <p> **Description** : obligatoire. Hello plus petit entier qui peut être retourné. <p> **Numéro du paramètre** : 2 <p> **Nom** : maximum <p> **Description** : obligatoire. Cette valeur est un entier hello après l’entier le plus élevé hello qui peut être renvoyé.|  
  
### <a name="date-functions"></a>Fonctions de date  
  
|Nom de la fonction|Description|  
|-------------------|-----------------|  
|utcnow|Retourne hello timestamp actuelle sous forme de chaîne, par exemple : `2017-03-15T13:27:36Z`: <p>`utcnow()` <p> **Numéro du paramètre** : 1 <p> **Nom** : format <p> **Description** : facultatif. Soit un [caractère de spécificateur de format unique](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) ou un [modèle de format personnalisé](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) qui indique comment tooformat hello la valeur de l’horodatage. Si le format n’est pas fourni, le format ISO 8601 de hello (« o ») est utilisé.|  
|addseconds|Ajoute un nombre entier de secondes tooa chaîne timestamp est passé. nombre de Hello de secondes peut être positif ou négatif. Par défaut, résultat de hello est une chaîne en ISO 8601 format (« o »), sauf si un spécificateur de format est fourni. Exemple : `2015-03-15T13:27:00Z` : <p>`addseconds('2015-03-15T13:27:36Z', -36)` <p> **Numéro du paramètre** : 1 <p> **Nom** : horodateur <p> **Description** : obligatoire. Chaîne qui contient l’heure de hello. <p> **Numéro du paramètre** : 2 <p> **Nom** : secondes <p> **Description** : obligatoire. nombre de Hello de secondes tooadd. Peut être négatif toosubtract secondes. <p> **Numéro du paramètre** : 3 <p> **Nom** : format <p> **Description** : facultatif. Soit un [caractère de spécificateur de format unique](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) ou un [modèle de format personnalisé](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) qui indique comment tooformat hello la valeur de l’horodatage. Si le format n’est pas fourni, le format ISO 8601 de hello (« o ») est utilisé.|  
|addminutes|Ajoute un nombre entier de minutes tooa chaîne timestamp est passé. nombre de Hello de minutes peut être positif ou négatif. Par défaut, résultat de hello est une chaîne en ISO 8601 format (« o »), sauf si un spécificateur de format est fourni. Exemple : `2015-03-15T14:00:36Z` : <p>`addminutes('2015-03-15T13:27:36Z', 33)` <p> **Numéro du paramètre** : 1 <p> **Nom** : horodateur <p> **Description** : obligatoire. Chaîne qui contient l’heure de hello. <p> **Numéro du paramètre** : 2 <p> **Nom** : minutes <p> **Description** : obligatoire. nombre de Hello de minutes tooadd. Peut être négatif toosubtract minutes. <p> **Numéro du paramètre** : 3 <p> **Nom** : format <p> **Description** : facultatif. Soit un [caractère de spécificateur de format unique](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) ou un [modèle de format personnalisé](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) qui indique comment tooformat hello la valeur de l’horodatage. Si le format n’est pas fourni, le format ISO 8601 de hello (« o ») est utilisé.|  
|addhours|Ajoute un nombre entier de l’horodateur de chaîne tooa heures passée dans. nombre de Hello d’heures peut être positif ou négatif. Par défaut, résultat de hello est une chaîne en ISO 8601 format (« o »), sauf si un spécificateur de format est fourni. Exemple : `2015-03-16T01:27:36Z` : <p>`addhours('2015-03-15T13:27:36Z', 12)` <p> **Numéro du paramètre** : 1 <p> **Nom** : horodateur <p> **Description** : obligatoire. Chaîne qui contient l’heure de hello. <p> **Numéro du paramètre** : 2 <p> **Nom** : heures <p> **Description** : obligatoire. nombre de Hello d’heures tooadd. Peut être négatif toosubtract heures. <p> **Numéro du paramètre** : 3 <p> **Nom** : format <p> **Description** : facultatif. Soit un [caractère de spécificateur de format unique](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) ou un [modèle de format personnalisé](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) qui indique comment tooformat hello la valeur de l’horodatage. Si le format n’est pas fourni, le format ISO 8601 de hello (« o ») est utilisé.|  
|adddays|Ajoute un nombre entier de jours tooa chaîne timestamp est passé. nombre de Hello de jours peut être positif ou négatif. Par défaut, résultat de hello est une chaîne en ISO 8601 format (« o »), sauf si un spécificateur de format est fourni. Exemple : `2015-02-23T13:27:36Z` : <p>`addseconds('2015-03-15T13:27:36Z', -20)` <p> **Numéro du paramètre** : 1 <p> **Nom** : horodateur <p> **Description** : obligatoire. Chaîne qui contient l’heure de hello. <p> **Numéro du paramètre** : 2 <p> **Nom** : jours <p> **Description** : obligatoire. nombre de Hello de jours tooadd. Peut être négatif toosubtract jours. <p> **Numéro du paramètre** : 3 <p> **Nom** : format <p> **Description** : facultatif. Soit un [caractère de spécificateur de format unique](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) ou un [modèle de format personnalisé](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) qui indique comment tooformat hello la valeur de l’horodatage. Si le format n’est pas fourni, le format ISO 8601 de hello (« o ») est utilisé.|  
|formatDateTime|Retourne une chaîne au format de date. Par défaut, résultat de hello est une chaîne en ISO 8601 format (« o »), sauf si un spécificateur de format est fourni. Exemple : `2015-02-23T13:27:36Z` : <p>`formatDateTime('2015-03-15T13:27:36Z', 'o')` <p> **Numéro du paramètre** : 1 <p> **Nom** : date <p> **Description** : obligatoire. Chaîne qui contient la date de hello. <p> **Numéro du paramètre** : 2 <p> **Nom** : format <p> **Description** : facultatif. Soit un [caractère de spécificateur de format unique](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) ou un [modèle de format personnalisé](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) qui indique comment tooformat hello la valeur de l’horodatage. Si le format n’est pas fourni, le format ISO 8601 de hello (« o ») est utilisé.|  
|startOfHour|Hello de retourne Démarrer de hello heure tooa chaîne timestamp passé. Exemple `2017-03-15T13:00:00Z` :<br /><br /> `startOfHour('2017-03-15T13:27:36Z')`<br /><br /> **Numéro du paramètre** : 1<br /><br /> **Nom** : horodateur<br /><br /> **Description** : obligatoire. Il s’agit d’une chaîne qui contient l’heure de hello.<br /><br />**Numéro du paramètre** : 2<br /><br /> **Nom** : format<br /><br /> **Description** : facultatif. Soit un [caractère de spécificateur de format unique](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) ou un [modèle de format personnalisé](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) qui indique comment tooformat hello la valeur de l’horodatage. Si le format n’est pas fourni, le format ISO 8601 de hello (« o ») est utilisé.|  
|startOfDay|Hello de retourne Démarrer de hello jour tooa chaîne timestamp passé. Exemple `2017-03-15T00:00:00Z` :<br /><br /> `startOfDay('2017-03-15T13:27:36Z')`<br /><br /> **Numéro du paramètre** : 1<br /><br /> **Nom** : horodateur<br /><br /> **Description** : obligatoire. Il s’agit d’une chaîne qui contient l’heure de hello.<br /><br />**Numéro du paramètre** : 2<br /><br /> **Nom** : format<br /><br /> **Description** : facultatif. Soit un [caractère de spécificateur de format unique](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) ou un [modèle de format personnalisé](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) qui indique comment tooformat hello la valeur de l’horodatage. Si le format n’est pas fourni, le format ISO 8601 de hello (« o ») est utilisé.| 
|startOfMonth|Hello de retourne Démarrer de hello mois tooa chaîne timestamp passé. Exemple `2017-03-01T00:00:00Z` :<br /><br /> `startOfMonth('2017-03-15T13:27:36Z')`<br /><br /> **Numéro du paramètre** : 1<br /><br /> **Nom** : horodateur<br /><br /> **Description** : obligatoire. Il s’agit d’une chaîne qui contient l’heure de hello.<br /><br />**Numéro du paramètre** : 2<br /><br /> **Nom** : format<br /><br /> **Description** : facultatif. Soit un [caractère de spécificateur de format unique](https://msdn.microsoft.com/library/az4se3k1%28v=vs.110%29.aspx) ou un [modèle de format personnalisé](https://msdn.microsoft.com/library/8kb3ddd4%28v=vs.110%29.aspx) qui indique comment tooformat hello la valeur de l’horodatage. Si le format n’est pas fourni, le format ISO 8601 de hello (« o ») est utilisé.| 
|dayOfWeek|Retourne hello jour du composant de semaine d’un horodateur de la chaîne.  Le dimanche correspond à la valeur 0, le lundi à la valeur 1 et ainsi de suite. Exemple `3` :<br /><br /> `dayOfWeek('2017-03-15T13:27:36Z')`<br /><br /> **Numéro du paramètre** : 1<br /><br /> **Nom** : horodateur<br /><br /> **Description** : obligatoire. Il s’agit d’une chaîne qui contient l’heure de hello.| 
|dayOfMonth|Retourne hello jour du composant « mois » d’un horodateur de la chaîne. Exemple `15` :<br /><br /> `dayOfMonth('2017-03-15T13:27:36Z')`<br /><br /> **Numéro du paramètre** : 1<br /><br /> **Nom** : horodateur<br /><br /> **Description** : obligatoire. Il s’agit d’une chaîne qui contient l’heure de hello.| 
|dayOfYear|Retourne hello jour du composant « année » d’un horodateur de la chaîne. Exemple `74` :<br /><br /> `dayOfYear('2017-03-15T13:27:36Z')`<br /><br /> **Numéro du paramètre** : 1<br /><br /> **Nom** : horodateur<br /><br /> **Description** : obligatoire. Il s’agit d’une chaîne qui contient l’heure de hello.| 
|ticks|Propriété d’un horodateur de la chaîne de graduations hello de retourne. Exemple `1489603019` :<br /><br /> `ticks('2017-03-15T18:36:59Z')`<br /><br /> **Numéro du paramètre** : 1<br /><br /> **Nom** : horodateur<br /><br /> **Description** : obligatoire. Il s’agit d’une chaîne qui contient l’heure de hello.| 
  
### <a name="workflow-functions"></a>Fonctions de flux de travail  

Ces fonctions vous permettent d’obtenir des informations sur les flux de travail hello lui-même en cours d’exécution.  
  
|Nom de la fonction|Description|  
|-------------------|-----------------|  
|listCallbackUrl|Retourne un déclencheur de chaîne toocall tooinvoke hello ou une action. <p> **Remarque** : cette fonction peut être utilisée uniquement dans **httpWebhook** et **apiConnectionWebhook**, et pas dans **manuel**, **recurrence**, **http** ou **apiConnection**. <p>Par exemple, hello `listCallbackUrl()` fonction renvoie : <p>`https://prod-01.westus.logic.azure.com:443/workflows/1235...ABCD/triggers/manual/run?api-version=2015-08-01-preview&sp=%2Ftriggers%2Fmanual%2Frun&sv=1.0&sig=xxx...xxx` |  
|flux de travail|Cette fonction fournit tous les détails de hello pour hello flux de travail lors de l’exécution de hello. <p> Les propriétés disponibles sur l’objet de flux de travail hello sont : <ul><li>`name`</li><li>`type`</li><li>`id`</li><li>`location`</li><li>`run`</li></ul> <p> Hello valeur Hello `run` propriété est un objet avec les propriétés suivantes : <ul><li>`name`</li><li>`type`</li><li>`id`</li></ul> <p>Consultez hello [API Rest](http://go.microsoft.com/fwlink/p/?LinkID=525617) pour plus d’informations sur ces propriétés.<p> Par exemple, tooget hello nom Hello actuel exécuter, utilisez hello `"@workflow().run.name"` expression. |

## <a name="next-steps"></a>Étapes suivantes

[Actions et déclencheurs de flux de travail](logic-apps-workflow-actions-triggers.md)
