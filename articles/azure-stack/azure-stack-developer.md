---
title: applications aaaDevelop pour la pile de Azure | Documents Microsoft
description: "Découvrez les considérations relatives au développement pour le prototypage d’applications sur Azure Stack."
services: azure-stack
documentationcenter: 
author: HeathL17
manager: byronr
editor: 
ms.assetid: d3ebc6b1-0ffe-4d3e-ba4a-388239d6cdc3
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: helaw
ms.openlocfilehash: 9bea75d0f0ecf19c05ff55ac3ef4e778d53a1912
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-for-azure-stack"></a>Développer pour Azure Stack
Vous pouvez commencer à développer applications aujourd'hui, même si vous n’avez pas accès tooan Azure environnement à pile. Étant donné que la pile de Azure fournit des services de Microsoft Azure qui s’exécutent dans votre centre de données, vous pouvez utiliser similaire toodevelop outils et processus par rapport à la pile de Azure comme vous le feriez avec Azure.  Avec un peu de préparation et de recommandations de hello rubriques suivantes, vous pouvez utiliser Azure tooemulate un environnement Azure pile :

* Dans Azure, vous pouvez créer des modèles Azure Resource Manager tooAzure déployable pile.  Consultez [considérations relatives au modèle](azure-stack-develop-templates.md) pour obtenir des conseils sur le développement de votre portabilité tooensure de modèles.
* Il existe une différence de disponibilité de service et de gestion des versions de services entre Azure et Azure Stack. Vous pouvez utiliser hello [module de stratégie Azure pile](azure-stack-policy-module.md) toowhat types toorestrict service Azure disponibilité et les ressources de disponible dans la pile de Azure. Restriction des services disponibles aidera à votre application de s’appuient sur les services tooAzure disponible pile.
* Hello [modèles de démarrage rapide Azure pile](https://github.com/Azure/AzureStack-QuickStart-Templates) sont des exemples de scénarios courants de façon toodevelop vos modèles de sorte qu’ils peuvent être déploiement tooboth Azure et la pile d’Azure.


