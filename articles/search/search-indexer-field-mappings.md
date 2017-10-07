---
title: "mappages d’aaaField dans les indexeurs d’Azure Search"
description: "Configurer tooaccount de mappages de champ d’indexeur Azure Search des différences dans les représentations sous forme de données et les noms de champ"
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: 0325a4de-0190-4dd5-a64d-4e56601d973b
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 10/27/2016
ms.author: eugenesh
ms.openlocfilehash: 009d5dbc12cb9e8d9cfd3e8042e907ca88399ad7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="field-mappings-in-azure-search-indexers"></a>Mappages de champs dans les indexeurs de la Recherche Azure
Lorsque vous utilisez des indexeurs d’Azure Search, vous pouvez parfois trouver vous-même dans les situations où vos données d’entrée ne correspondant pas tout à fait schéma hello de l’index cible. Dans ce cas, vous pouvez utiliser **champ mappages** tootransform vos données hello souhaité de forme.

Quelques situations où les mappages de champs sont utiles :

* Votre source de données a un champ `_id`, mais Azure Search n'autorise pas les noms de champs commençant par un trait de soulignement. Un mappage de champs permet de vous trop « renommez » un champ.
* Vous souhaitez toopopulate plusieurs champs Bonjour indexer avec hello mêmes source de données, par exemple, car vous souhaitez tooapply différents analyseurs toothose champs. Les mappages de champs vous permettent de « répliquer » un champ de source de données.
* Vous devez tooBase64 encoder ou décoder vos données. Les mappages de champs prennent en charge plusieurs **fonctions de mappage**, y compris les fonctions d’encodage et de décodage en Base64.   

## <a name="setting-up-field-mappings"></a>Configuration des mappages de champs
Vous pouvez ajouter des mappages de champs lors de la création d’un nouvel indexeur à l’aide de hello [créer un indexeur](https://msdn.microsoft.com/library/azure/dn946899.aspx) API. Vous pouvez gérer les mappages de champs sur un indexeur d’indexation à l’aide de hello [mise à jour indexeur](https://msdn.microsoft.com/library/azure/dn946892.aspx) API.

Un mappage de champs comprend 3 parties :

1. Un `sourceFieldName`, qui représente un champ de votre source de données. Cette propriété est requise.
2. Un `targetFieldName`facultatif, qui représente un champ de votre index de recherche. Si omis, hello même nom comme source de données hello est utilisé.
3. Une `mappingFunction`facultative, qui peut transformer vos données à l'aide d'une des fonctions prédéfinies. la liste complète des fonctions Hello est [ci-dessous](#mappingFunctions).

Mappages de champs sont ajoutés toohello `fieldMappings` tableau sur la définition d’indexeur hello.

Par exemple, voici comment gérer les différences dans les noms de champs :

```JSON

PUT https://[service name].search.windows.net/indexers/myindexer?api-version=[api-version]
Content-Type: application/json
api-key: [admin key]
{
    "dataSourceName" : "mydatasource",
    "targetIndexName" : "myindex",
    "fieldMappings" : [ { "sourceFieldName" : "_id", "targetFieldName" : "id" } ]
}
```

Un indexeur peut avoir plusieurs mappages de champs. Par exemple, voici comment « répliquer » un champ :

```JSON

"fieldMappings" : [
    { "sourceFieldName" : "text", "targetFieldName" : "textStandardEnglishAnalyzer" },
    { "sourceFieldName" : "text", "targetFieldName" : "textSoundexAnalyzer" },
]
```

> [!NOTE]
> Azure Search utilise les noms de champ et de la fonction la hello des tooresolve comparaison respectant la casse dans les mappages de champs. Ceci est pratique (vous n’avez pas tooget tous les casse hello droite), mais elle signifie que votre source de données ou un index ne peut pas avoir des champs qui diffèrent uniquement par leur casse.  
>
>

<a name="mappingFunctions"></a>

## <a name="field-mapping-functions"></a>Fonctions de mappage de champs
Ces fonctions sont actuellement prises en charge :

* [base64Encode](#base64EncodeFunction)
* [base64Decode](#base64DecodeFunction)
* [extractTokenAtPosition](#extractTokenAtPositionFunction)
* [jsonArrayToStringCollection](#jsonArrayToStringCollectionFunction)

<a name="base64EncodeFunction"></a>

### <a name="base64encode"></a>base64Encode
Exécute *sécurisés pour les URL* codage Base64 de hello, la chaîne d’entrée. Suppose que l’entrée hello est encodé en UTF-8.

#### <a name="sample-use-case"></a>Exemple de cas d’utilisation
Uniquement les caractères URL-safe peuvent apparaître dans une clé de document Azure Search (car les clients doivent être en mesure de tooaddress document de hello à l’aide de hello API de recherche, par exemple). Si vos données contiennent des caractères non sécurisés l’URL et que vous souhaitez toouse il toopopulate un champ de clé dans votre index de recherche, utilisez cette fonction.   

#### <a name="example"></a>Exemple
```JSON

"fieldMappings" : [
  {
    "sourceFieldName" : "Path",
    "targetFieldName" : "UrlSafePath",
    "mappingFunction" : { "name" : "base64Encode" }
  }]
```

<a name="base64DecodeFunction"></a>

### <a name="base64decode"></a>base64Decode
Effectue le décodage en Base64 de la chaîne d’entrée de hello. Hello entrée est supposée tooa *sécurisés pour les URL* chaîne codée en Base64.

#### <a name="sample-use-case"></a>Exemple de cas d’utilisation
Les valeurs des métadonnées personnalisées des objets blob doivent être encodées en ASCII. Vous pouvez utiliser Base64 encodage toorepresent arbitraire des chaînes Unicode dans les métadonnées d’objets blob personnalisé. Toutefois, recherche de toomake explicite, vous pouvez utiliser cette fonction tooturn hello encodé données en chaînes « standard » lors du remplissage de l’index de recherche.  

#### <a name="example"></a>Exemple
```JSON

"fieldMappings" : [
  {
    "sourceFieldName" : "Base64EncodedMetadata",
    "targetFieldName" : "SearchableMetadata",
    "mappingFunction" : { "name" : "base64Decode" }
  }]
```

<a name="extractTokenAtPositionFunction"></a>

### <a name="extracttokenatposition"></a>extractTokenAtPosition
Fractionne un champ de chaîne à l’aide de hello spécifié délimiteur et le jeton de hello récupère à hello la position spécifiée du fractionnement résultant de hello.

Par exemple, si hello entrée est `Jane Doe`, hello `delimiter` est `" "`(espace) et hello `position` est 0, le résultat de hello est `Jane`; si hello `position` est 1, il en résulte hello `Doe`. Si la position de hello fait référence jeton tooa qui n’existe pas, une erreur s’affichera.

#### <a name="sample-use-case"></a>Exemple de cas d’utilisation
Votre source de données contient un `PersonName` champ et que vous souhaitez tooindex en tant que deux `FirstName` et `LastName` champs. Vous pouvez utiliser cette hello toosplit de fonction d’entrée à l’aide du caractère d’espace hello comme délimiteur de hello.

#### <a name="parameters"></a>Paramètres
* `delimiter`: un toouse de chaîne en tant que séparateur hello lorsque fractionnement hello chaîne d’entrée.
* `position`: une position de base zéro d’entier de toopick de jeton hello après la chaîne d’entrée de hello est fractionnée.    

#### <a name="example"></a>Exemple
```JSON

"fieldMappings" : [
  {
    "sourceFieldName" : "PersonName",
    "targetFieldName" : "FirstName",
    "mappingFunction" : { "name" : "extractTokenAtPosition", "parameters" : { "delimiter" : " ", "position" : 0 } }
  },
  {
    "sourceFieldName" : "PersonName",
    "targetFieldName" : "LastName",
    "mappingFunction" : { "name" : "extractTokenAtPosition", "parameters" : { "delimiter" : " ", "position" : 1 } }
  }]
```

<a name="jsonArrayToStringCollectionFunction"></a>

### <a name="jsonarraytostringcollection"></a>jsonArrayToStringCollection
Transformations d’une chaîne mise en forme en tant que tableau JSON de chaînes dans un tableau de chaînes qui peut être utilisé toopopulate un `Collection(Edm.String)` champ dans l’index de hello.

Par exemple, si la chaîne d’entrée de hello est `["red", "white", "blue"]`, puis le champ cible de hello de type `Collection(Edm.String)` sera rempli avec les valeurs hello trois `red`, `white` et `blue`. Pour les valeurs d'entrée qui ne peuvent pas être analysées en tant que tableaux de chaînes JSON, une erreur est renvoyée.

#### <a name="sample-use-case"></a>Exemple de cas d’utilisation
Base de données SQL Azure n’a pas un type de données intégré naturellement mappe trop`Collection(Edm.String)` champs dans Azure Search. toopopulate des champs de la collection de chaînes, mettre en forme vos données sources en un tableau de chaîne JSON et utiliser cette fonction.

#### <a name="example"></a>Exemple
```JSON

"fieldMappings" : [
  { "sourceFieldName" : "tags", "mappingFunction" : { "name" : "jsonArrayToStringCollection" } }
]
```

## <a name="help-us-make-azure-search-better"></a>Aidez-nous à améliorer Azure Search
Si vous avez des demandes de fonctionnalités ou des idées pour les améliorations, veuillez contacter toous sur notre [site UserVoice](https://feedback.azure.com/forums/263029-azure-search/).
