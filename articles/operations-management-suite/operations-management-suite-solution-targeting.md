---
title: "ciblage d’aaaSolution dans OMS | Documents Microsoft"
description: "Ciblage de la solution est une fonctionnalité dans Operations Management Suite (OMS) qui vous permet de toolimit management solutions tooa ensemble spécifique d’agents.  Cet article décrit comment toocreate une configuration de l’étendue et appliquez-le tooa solution."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 1f054a4e-6243-4a66-a62a-0031adb750d8
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/27/2017
ms.author: bwren
ms.openlocfilehash: 6f8c8109e0d9e282e18724bf8b673b10de8e498a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-solution-targeting-in-operations-management-suite-oms-tooscope-management-solutions-toospecific-agents-preview"></a>Utiliser la solution de ciblage dans Operations Management Suite (OMS) agents de toospecific de solutions de gestion tooscope (version préliminaire)
Lorsque vous ajoutez un tooOMS de solution, il est déployé automatiquement par défaut tooall Windows et Linux agents connectés tooyour Analytique de journal espace de travail.  Vous souhaiterez toomanage votre quantité hello les coûts et la limite de données collectée pour une solution en limitant l’ensemble particulier de tooa d’agents.  Cet article décrit comment toouse **Solution ciblant** qui est une fonctionnalité d’OMS qui vous permet de tooapply une étendue tooyour solutions.

## <a name="how-tootarget-a-solution"></a>Comment tootarget une solution
Voici trois étapes tootargeting une solution comme décrit dans les sections suivantes de hello.  Notez que vous devez à la fois du portail OMS hello et hello portail Azure pour les différentes étapes.


### <a name="1-create-a-computer-group"></a>1. Créer un groupe d’ordinateurs
Vous spécifiez hello ordinateurs sur lesquels tooinclude dans une étendue en créant un [groupe d’ordinateurs](../log-analytics/log-analytics-computer-groups.md) dans le journal Analytique.  groupe d’ordinateurs Hello peut être basé sur une recherche de journal ou importé à partir d’autres sources telles que Active Directory ou les groupes WSUS. En tant que [ci-dessous](#solutions-and-agents-that-cant-be-targeted), seuls les ordinateurs qui sont directement connectés tooLog Analytique est inclus dans l’étendue de hello.

Une fois que vous avez groupe d’ordinateurs hello créé dans votre espace de travail, vous devez l’inclure dans une configuration de l’étendue qui peut être appliqué tooone ou autres solutions.
 
 
 ### <a name="2-create-a-scope-configuration"></a>2. Création d’une configuration d’étendue
 A **Configuration de l’étendue** inclut un ou plusieurs groupes d’ordinateurs et peut être appliqué tooone ou autres solutions. 
 
 Créer une configuration de l’étendue à l’aide de hello suivant le processus.  

 1. Dans l’hello portail Azure, accédez trop**Analytique de journal** et sélectionnez votre espace de travail.
 2. Dans les propriétés de hello pour l’espace de travail hello **Sources de données d’espace de travail** sélectionnez **étendue Configurations**.
 3. Cliquez sur **ajouter** toocreate une nouvelle configuration de l’étendue.
 4. Tapez un **nom** pour la configuration de l’étendue hello.
 5. Cliquez sur **Sélectionner des groupes d’ordinateurs**.
 6. Sélectionnez le groupe d’ordinateurs hello que vous avez créé et éventuellement les autres groupes tooadd toohello configuration.  Cliquez sur **Sélectionner**.  
 6. Cliquez sur **OK** configuration de l’étendue toocreate hello. 


 ### <a name="3-apply-hello-scope-configuration-tooa-solution"></a>3. Appliquer la solution de tooa configuration hello étendue.
Une fois que vous avez une configuration de l’étendue, puis vous pouvez l’appliquer tooone ou autres solutions.  Notez qu’une seule configuration d’étendue peut être utilisée avec plusieurs solutions, mais chaque solution ne peut utiliser qu’une seule configuration d’étendue.

Appliquer une configuration étendue à l’aide de hello suivant le processus.  

 1. Dans l’hello portail Azure, accédez trop**Analytique de journal** et sélectionnez votre espace de travail.
 2. Dans les propriétés de hello pour l’espace de travail hello sélectionnez **Solutions**.
 3. Cliquez sur la solution de hello souhaité tooscope.
 4. Dans les propriétés de hello de solution hello sous **Sources de données d’espace de travail** sélectionnez **Solution ciblant**.  Si l’option de hello n’est pas disponible puis [cette solution ne peut pas être ciblée](#solutions-and-agents-that-cant-be-targeted).
 5. Cliquez sur **Ajouter une configuration d’étendue**.  Si vous disposez déjà d’une solution de toothis configuration appliquée cette option n’est pas disponible.  Vous devez supprimer la configuration existante de hello avant d’ajouter un autre.
 6. Cliquez sur la configuration de l’étendue hello que vous avez créé.
 7. Hello d’espion **état** de tooensure de configuration de hello il montre **Succeeded**.  Si l’état de hello indique une erreur, puis cliquez sur hello ellipse toohello de configuration de hello et sélectionnez **configuration de modifier l’étendue** toomake modifications.

## <a name="solutions-and-agents-that-cant-be-targeted"></a>Solutions et agents ne pouvant pas être ciblés
Voici les critères hello pour les agents et les solutions qui ne peut pas être utilisées avec le ciblage de la solution.

- Ciblage de la solution ne s’applique toosolutions tooagents à déployer.
- Ciblage de la solution ne s’applique toosolutions fournies par Microsoft.  Il ne s’applique pas toosolutions [créés par vous-même ou partenaires](operations-management-suite-solutions-creating.md).
- Vous ne pouvez filtrer les agents qui se connectent directement tooLog Analytique.  Solutions déploient automatiquement les agents tooany qui font partie d’un groupe d’administration Operations Manager connecté ou non, ils sont inclus dans une configuration de l’étendue.

### <a name="exceptions"></a>Exceptions
Ciblage de la solution ne peut pas être utilisé avec hello suivant solutions même si elles tiennent hello établi des critères.

- Évaluation de l’intégrité de l’agent

## <a name="next-steps"></a>Étapes suivantes
- En savoir plus sur les solutions de gestion, y compris les solutions hello tooinstall disponible dans votre environnement à [espace de travail Analytique des journaux de Azure ajouter management solutions tooyour](../log-analytics/log-analytics-add-solutions.md).
- En savoir plus sur la création de groupes d’ordinateurs en consultant [Groupes d’ordinateurs dans la recherche dans les journaux de Log Analytics](../log-analytics/log-analytics-computer-groups.md).