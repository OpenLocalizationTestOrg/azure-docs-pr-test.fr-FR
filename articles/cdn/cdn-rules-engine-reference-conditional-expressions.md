---
title: "les expressions conditionnelles du moteur de règles aaaAzure CDN | Documents Microsoft"
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
ms.openlocfilehash: 39d0754c34a577f77ca87b6fd92e2b6a9e4ff8fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cdn-rules-engine-conditional-expressions"></a>Expressions conditionnelles du moteur de règles Azure CDN
Cette rubrique répertorie les descriptions détaillées de hello Expressions conditionnelles pour Azure réseau CDN (Content Delivery) [moteur de règles](cdn-rules-engine.md).

Hello de première partie d’une règle est hello Expression conditionnelle.

Expression conditionnelle | Description
-----------------------|-------------
IF | L’expression IF est toujours une partie de la première instruction de hello dans une règle. Comme toutes les autres expressions conditionnelles, cette instruction IF doit être associée à une correspondance. Si aucune des expressions conditionnelles supplémentaires ne sont définies, cette correspondance détermine le critère hello qui doit être remplie avant un ensemble de fonctionnalités peut-être être appliqués tooa demande.
AND IF | L’expression IF et peut-être uniquement être ajoutée après hello suivant les types d’expressions conditionnel : IF, et si. Il indique qu’il existe une autre condition qui doit être remplie pour une instruction IF initiale de hello.
ELSE IF| Une expression ELSE IF spécifie une autre condition qui doit être remplie avant un ensemble de toothis spécifique de fonctionnalités instruction ELSE IF a lieu. présence de Hello d’une instruction IF ELSE indique fin hello de l’instruction précédente de hello. Hello uniquement expression conditionnelle qui peut être placée après qu’une instruction IF ELSE est une autre instruction ELSE IF. Cela signifie qu’une instruction IF ELSE peut être uniquement toospecify utilisé une seule condition supplémentaire qui a toobe remplie.

**Exemple** : ![condition de correspondance CDN](./media/cdn-rules-engine-reference/cdn-rules-engine-conditional-expression.png)

 > [!TIP]
   > Une règle suivante peut remplacer les actions de hello spécifiées par une règle précédente. Exemple : une règle de fourre-tout sécurise toutes les requêtes par le biais de l’authentification basée sur un jeton. Une autre règle peut être créée directement en dessous toomake une exception pour certains types de demandes.

### <a name="next-steps"></a>Étapes suivantes
* [Vue d'ensemble d'Azure CDN](cdn-overview.md)
* [Référence du moteur de règles](cdn-rules-engine-reference.md)
* [Conditions de correspondance du moteur de règles](cdn-rules-engine-reference-match-conditions.md)
* [Fonctionnalités du moteur de règles](cdn-rules-engine-reference-features.md)
* [Le comportement par défaut HTTP à l’aide du moteur de règles hello](cdn-rules-engine.md)
