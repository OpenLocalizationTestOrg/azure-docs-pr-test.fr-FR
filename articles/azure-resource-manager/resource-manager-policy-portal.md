---
title: "portail aaaAzure pour les stratégies de ressources | Documents Microsoft"
description: "Décrit comment toouse toocreate portail Azure et de gérer les stratégies du Gestionnaire de ressources. Les stratégies peuvent être appliquées à des groupes d’abonnement ou une ressource hello."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: tomfitz
ms.openlocfilehash: ce6413386317e532b63761a24458b85c996af4a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-portal-tooassign-and-manage-resource-policies"></a>Utilisez tooassign portail Azure et de gérer les stratégies de ressources
Hello portail Azure permet les abonnements et vous tooassign stratégies tooresource groupes de ressources. l’interface utilisateur Hello permet stratégie de hello tooselect facile que vous souhaitez tooassign et spécifiez des valeurs de paramètre pour cette stratégie de paramètres de stratégie toocustomize hello. 

tooassign une stratégie via le portail de hello, définition de stratégie hello doit déjà exister dans votre abonnement. Votre abonnement a plusieurs définitions des stratégies intégrées qui sont prêtes pour vous tooassign tooresource groupes ou des abonnements. Vous voyez ces stratégies intégrées et les stratégies personnalisées que vous avez défini lors de l’utilisation de stratégies de portail tooassign hello. Pour une présentation toopolicies et comment toodefine personnalisés stratégie, consultez [vue d’ensemble des stratégies de ressources](resource-manager-policy.md).

Toutes les ressources enfants héritent des stratégies. Donc, si une stratégie est un groupe de ressources appliquée tooa, ressources de hello tooall applicable dans ce groupe de ressources. Dans cet article, le terme de hello **étendue** fait référence le groupe de ressources toohello ou d’un abonnement qui est affectée à la stratégie de hello. 

Les stratégies sont évaluées lors de la création et de la mise à jour des ressources (opérations PUT et PATCH).

## <a name="assign-a-policy"></a>Attribution d’une stratégie

1. tooassign un tooeither stratégie un groupe de ressources ou un abonnement, sélectionnez ce groupe de ressources ou d’un abonnement. Dans paramètres de hello, sélectionnez **stratégies**.

   ![sélectionner des stratégies](./media/resource-manager-policy-portal/select-policies.png)

2. toocreate une attribution de stratégie pour cette étendue, sélectionnez **ajouter affectation**.

   ![ajouter une affectation](./media/resource-manager-policy-portal/add-assignment.png)

3. Sélectionnez la stratégie hello tooassign. Même si vous n’avez ajouté aucun abonnement de tooyour de définitions de stratégie, vous consultez stratégies hello intégrées qui sont disponibles pour l’assignation. Ces stratégies intégrées couvrent de nombreux scénarios courants.

   ![sélectionner une définition](./media/resource-manager-policy-portal/select-definition.png)

4. Après avoir sélectionné une stratégie, vous consultez une description de la stratégie de hello et tous les paramètres pour cette stratégie. Par exemple, hello image suivante montre hello **autorisée emplacements** paramètre, qui est requis pour la stratégie hello qui restreint les emplacements disponibles hello.

   ![afficher des paramètres](./media/resource-manager-policy-portal/show-parameters.png)

5. Interface utilisateur de hello, sélectionnez toospecify de valeurs hello pour les paramètres de stratégie hello (par exemple, les emplacements de hello qui peuvent être utilisés pour le déploiement).

   ![sélectionner les valeurs des paramètres](./media/resource-manager-policy-portal/select-parameters.png)

6. Fournir des valeurs pour hello autres paramètres. étendue de Hello est automatiquement attribué en fonction de panneau hello sélectionnée lors du démarrage d’attribution de stratégie hello. Cliquez sur **OK** quand vous avez terminé.

   ![définir les paramètres](./media/resource-manager-policy-portal/define-parameters.png)

  Vous avez attribué hello stratégie toohello spécifié étendue.

## <a name="view-policy-assignments"></a>Afficher les affectations de stratégies

Après avoir attribué une stratégie, il apparaît dans la liste hello de stratégies pour cette étendue. Hello **détails** onglet affiche un résumé de l’attribution de stratégie hello.

![afficher les détails](./media/resource-manager-policy-portal/show-details.png)

Hello **règle d’affectation** onglet affiche hello JSON pour la définition de la stratégie hello.

![afficher une règle d’affectation](./media/resource-manager-policy-portal/show-assignment-rule.png)

## <a name="change-an-existing-policy-assignment"></a>Modifier une affectation de stratégie existante

toochange une stratégie, sélectionnez **modifier l’affectation** ou **supprimer**

![modifier ou supprimer une affectation](./media/resource-manager-policy-portal/edit-delete-policy.png)

## <a name="assign-custom-policies"></a>Affecter des stratégies personnalisées

Si vous avez défini des stratégies personnalisées dans votre abonnement, ces stratégies sont disponibles pour l’assignation via le portail de hello. Ces stratégies ont le préfixe **[Custom]**

![stratégies personnalisées](./media/resource-manager-policy-portal/show-custom-policy.png)

## <a name="next-steps"></a>Étapes suivantes
* toolearn sur la syntaxe JSON hello pour définir des stratégies, consultez [vue d’ensemble des stratégies de ressources](resource-manager-policy.md).
* Pour obtenir des conseils comment les entreprises peuvent utiliser le Gestionnaire de ressources tooeffectively gérer les abonnements, consultez [une vue de structure Azure enterprise - gouvernance de l’abonnement normative](resource-manager-subscription-governance.md).
* schéma de stratégie Hello est publiée à [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json). 

