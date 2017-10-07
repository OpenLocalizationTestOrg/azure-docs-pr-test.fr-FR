---
title: "référence du moteur de règles aaaAzure CDN | Documents Microsoft"
description: "Documentation de référence sur les fonctionnalités et conditions de correspondance du moteur de règles Azure CDN."
services: cdn
documentationcenter: 
author: Lichard
manager: akucer
editor: 
ms.assetid: 669ef140-a6dd-4b62-9b9d-3f375a14215e
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: rli
ms.openlocfilehash: 4159715d15fc792afb49dcd2a30752fabcd94a38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cdn-rules-engine"></a>Moteur des règles Azure CDN
Cette rubrique répertorie les descriptions détaillées des conditions de correspondance disponible hello et des fonctionnalités réseau de distribution contenu (CDN) pour Azure [moteur de règles](cdn-rules-engine.md).

Hello HTTP du moteur de règles est conçu toobe hello instance finale présidant sur la façon dont certains types de demandes sont traitées par hello CDN.

**Utilisations courantes** :

- Remplacer ou définir une stratégie de cache personnalisée.
- Sécuriser ou refuser les demandes de contenu sensible.
- Rediriger les demandes.
- Stocker les données de journal personnalisé.

## <a name="terminology"></a>Terminologie
Une règle est définie via l’utilisation de hello de [ **expressions conditionnelles**](cdn-rules-engine-reference-conditional-expressions.md), [ **correspond à**](cdn-rules-engine-reference-match-conditions.md), et [  **fonctionnalités**](cdn-rules-engine-reference-features.md). Ces éléments sont mis en surbrillance Bonjour après l’illustration.

 ![Condition de correspondance CDN](./media/cdn-rules-engine-reference/cdn-rules-engine-terminology.png)

## <a name="syntax"></a>Syntaxe

manière Hello dans lequel les caractères spéciaux sont considérés varie en fonction des valeurs de texte de handles de fonctionnalité ou conséquente toohow une condition de correspondance. Une condition de correspondance ou une fonctionnalité peut interpréter le texte dans un des hello suivant façons :

1. [**Valeurs littérales**](#literal-values) 
2. [**Valeurs de caractère générique**](#wildcard-values)
3. [**Expressions régulières**](#regular-expressions)

### <a name="literal-values"></a>Valeurs littérales
Texte qui est interprétée comme une valeur littérale traite tous les caractères spéciaux, à l’exception de hello de symbole de % hello, dans le cadre de la valeur hello qui doit être mis en correspondance. En d’autres termes, un littéral correspondent à condition de définir trop`\'*'\` seulement soit rempli lorsque qui valeur exacte (c'est-à-dire `\'*'\`) se trouve.
 
Un symbole de pourcentage est utilisé tooindicate URL codage (par exemple, `%20`).

### <a name="wildcard-values"></a>Valeurs de caractère générique
Texte qui est interprétée comme une valeur générique attribuera caractères toospecial de signification supplémentaire. Hello tableau suivant décrit comment hello suivant le jeu de caractères est interprétée.

Caractère | Description
----------|------------
\ | Une barre oblique inverse est tooescape utilisé les hello caractères spécifiés dans ce tableau. Une barre oblique inverse doit être spécifiée directement avant le caractère spécial hello qui devrait être échappé.<br/>Par exemple, la syntaxe de hello échappe un astérisque :`\*`
% | Un symbole de pourcentage est utilisé tooindicate URL codage (par exemple, `%20`).
* | Un astérisque est un caractère générique représentant un ou plusieurs caractères.
Espace | Un caractère d’espace indique qu’une condition de correspondance peut être satisfaite à l’aide de hello spécifié valeurs ou des modèles.
'valeur' | Un guillemet simple n’a pas de signification particulière. Toutefois, un jeu de guillemets simples sert tooindicate une valeur doit être traitée comme une valeur littérale. Il peut être utilisé dans hello suivant façons :<br><br/>-Il permet une toobe de condition de correspondance satisfaite lorsqu’hello spécifiée correspond à la valeur de toute portion de valeur de comparaison hello.  Par exemple, `'ma'` correspondrait à des hello suivant des chaînes : <br/><br/>/business/**ma**rathon/asset.htm<br/>**ma**p.gif<br/>/business/template.**ma**p<br /><br />-Il permet une toobe caractère spécial spécifié comme un caractère littéral. Par exemple, vous pouvez spécifier un caractère d’espace littéral en plaçant un caractère d’espace dans un jeu de guillemets simples (par exemple, `' '` ou `'sample value'`).<br/>-Il permet une toobe de valeur vide spécifié. Spécifiez une valeur vide en entrant un jeu de guillemets simples (par exemple, '').<br /><br/>**Important :**<br/>-Si hello spécifié la valeur ne contient pas un caractère générique, puis il est automatiquement considéré une valeur littérale. Cela signifie qu’il n’est pas nécessaire toospecify un jeu de guillemets simples.<br/>- Si une barre oblique inverse n’échappe pas à un autre caractère dans ce tableau, elle est ignorée si un jeu de guillemets simples est entré.<br/>-Une autre façon toospecify un caractère spécial, comme un caractère littéral est tooescape à l’aide d’une barre oblique inverse (par exemple, `\`).

### <a name="regular-expressions"></a>Expressions régulières

Les expressions régulières définissent un modèle qui sera recherché dans une valeur de texte. Expressions régulières définit diverses tooa de signification spécifique de symboles. Hello tableau suivant indique les caractères spéciaux sont traités par les conditions de correspondance et les fonctionnalités qui prennent en charge des expressions régulières.

Caractère spécial | Description
------------------|------------
\ | Un Bonjour de caractère de barre oblique inverse d’échappement hello suit. Alors que toobe caractère traitée comme une valeur littérale au lieu d’effectuer sur sa signification d’expression régulière. Par exemple, la syntaxe de hello échappe un astérisque :`\*`
% | signification Hello d’un symbole de pourcentage dépend de son utilisation.<br/><br/> `%{HTTPVariable}` : cette syntaxe identifie une variable HTTP.<br/>`%{HTTPVariable%Pattern}`: Cette syntaxe utilise un tooidentify de symbole de pourcentage HTTP variable et comme délimiteur.<br />`\%`: Un symbole de pourcentage d’échappement permet toobe utilisé en tant que valeur littérale ou tooindicate l’encodage d’URL (par exemple, `\%20`).
* | Un astérisque permet hello précédant toobe caractère mis en correspondance zéro ou plusieurs fois. 
Espace | Un caractère d’espace est généralement traité comme un caractère littéral. 
'valeur' | Les guillemets simples sont traités comme des caractères littéraux. Un jeu de guillemets simples n’a pas de signification particulière.


## <a name="next-steps"></a>Étapes suivantes
* [Conditions de correspondance du moteur de règles](cdn-rules-engine-reference-match-conditions.md)
* [Expressions conditionnelles du moteur de règles](cdn-rules-engine-reference-conditional-expressions.md)
* [Fonctionnalités du moteur de règles](cdn-rules-engine-reference-features.md)
* [Le comportement par défaut HTTP à l’aide du moteur de règles hello](cdn-rules-engine.md)
* [Vue d'ensemble d'Azure CDN](cdn-overview.md)
