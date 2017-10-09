---
title: "aaaPermissions dans le centre de sécurité Azure | Documents Microsoft"
description: "Cet article explique comment le centre de sécurité Azure utilise en fonction du rôle l’accès contrôle tooassign autorisations toousers et identifie les hello autorisé des actions pour chaque rôle."
services: security-center
cloud: na
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
ms.assetid: 
ms.service: security-center
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: terrylan
ms.openlocfilehash: 03e16132dc3d951ef8ad9e86b9970b9e4d15c76b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="permissions-in-azure-security-center"></a>Autorisations dans Azure Security Center

Centre de sécurité Azure utilise [contrôle d’accès en fonction du rôle (RBAC)](../active-directory/role-based-access-control-configure.md), qui fournit des [rôles intégrés](../active-directory/role-based-access-built-in-roles.md) qui peuvent être attribuées toousers, des groupes et des services dans Azure.

Centre de sécurité évalue la configuration de hello de vos problèmes de sécurité tooidentify de ressources et les vulnérabilités. Dans le centre de sécurité, vous voyez uniquement les informations liées tooa ressource lorsque vous sont assignés rôle hello de propriétaire, collaborateur ou lecteur pour le groupe d’abonnement ou une ressource hello appartenant à une ressource.

Dans les rôles toothese addition, il existe deux rôles de centre de sécurité spécifiques :

* **Lecteur de sécurité**: un utilisateur membre du rôle de toothis a affichage droits tooSecurity Center. utilisateur de Hello peut afficher les recommandations, alertes, une stratégie de sécurité et les États de sécurité, mais il ne peut pas apporter des modifications.
* **Administrateur de sécurité**: un utilisateur membre du rôle de toothis hello même droits comme hello du lecteur de sécurité et peut également mettre à jour de la stratégie de sécurité hello et fermer les alertes et les recommandations.

> [!NOTE]
> rôles de sécurité Hello, lecteur de la sécurité et l’administrateur de la sécurité, ont accès uniquement dans le centre de sécurité. rôles de sécurité de Hello ne doivent pas accéder aux zones de service tooother Azure telles que le stockage, Web et mobiles ou Internet des objets.
>
>

## <a name="roles-and-allowed-actions"></a>Rôles et actions autorisées

Hello tableau suivant affiche les rôles et les actions autorisées dans le centre de sécurité. Un X indique que l’action de hello est autorisée pour ce rôle.

| Rôle | Modifier une stratégie de sécurité | Appliquer des recommandations de sécurité à une ressource | Ignorer les alertes et les recommandations | Afficher les alertes et les recommandations |
|:--- |:---:|:---:|:---:|:---:|
| Propriétaire de l’abonnement | X | X | X | X |
| Collaborateur de l’abonnement | X | X | X | X |
| Propriétaire du groupe de ressources | -- | X | -- | X |
| Collaborateur du groupe de ressources | -- | X | -- | X |
| Lecteur | -- | -- | -- | X |
| Security Administrator | X | -- | X | X |
| Lecteur de sécurité | -- | -- | -- | X |

> [!NOTE]
> Nous recommandons d’attribuer hello rôle le moins permissif nécessaire pour les utilisateurs toocomplete leurs tâches. Par exemple, affecter toousers de rôle de lecteur hello qui a uniquement besoin d’informations sur l’intégrité de la sécurité hello tooview d’une ressource mais pas effectuer une action, telles que l’application des recommandations ou de la modification des stratégies.
>
>

## <a name="next-steps"></a>Étapes suivantes
Cet article explique comment le centre de sécurité utilise RBAC tooassign autorisations toousers et identifié hello autorisé des actions pour chaque rôle. Maintenant que vous êtes familiarisé avec les attributions de rôles hello nécessaire toomonitor hello état de sécurité de votre abonnement, modifiez les stratégies de sécurité et appliquer les recommandations, découvrez comment :

- [Définir des stratégies de sécurité dans Security Center](security-center-policies.md)
- [Gérer les recommandations de sécurité dans Security Center](security-center-recommendations.md)
- [Surveiller l’intégrité de la sécurité de vos ressources Azure hello](security-center-monitoring.md)
- [Gérer et répondre toosecurity des alertes dans le centre de sécurité](security-center-managing-and-responding-alerts.md)
- [Surveiller les solutions de sécurité des partenaires](security-center-partner-solutions.md)
