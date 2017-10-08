---
title: "alertes de sécurité aaaHow tooconfigure | Documents Microsoft"
description: "Découvrez comment tooconfigure sécurité des alertes pour l’extension d’Azure Privileged Identity Management."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 4e0c911a-36c6-42a0-8f79-a01c03d2d04f
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 1b3c4a7d36fa3f81bb3fe2574d675fdf0ab34909
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-security-alerts-in-azure-ad-privileged-identity-management"></a>La sécurité de tooconfigure les alertes dans Azure AD Privileged Identity Management
## <a name="security-alerts"></a>Alertes de sécurité
Azure Privileged Identity Management (PIM) génère des alertes en cas d’activité suspecte ou non fiable dans votre environnement. Lorsqu’une alerte est déclenchée, elle s’affiche sur le tableau de bord hello PIM. Sélectionnez toosee d’alerte hello un rapport que listes hello utilisateurs ou rôles qui a déclenchement l’alerte de hello.

![Alertes de sécurité du tableau de bord PIM - capture d’écran][1]

| Alerte | Déclencheur | Recommandation |
| --- | --- | --- |
| **Les rôles sont affectés en dehors de PIM** |Un administrateur a été définitivement rôle tooa, en dehors de l’interface PIM hello. |Passez en revue la nouvelle attribution de rôle hello. Étant donné que les autres services peuvent affecter uniquement des administrateurs permanents, modifier l’attribution éligibles tooan si nécessaire. |
| **Les rôles sont activés trop fréquemment.** |A été trop de réactivations de hello même rôle délai hello autorisé dans les paramètres de hello. |Contactez toosee d’utilisateur hello pourquoi ils ont activé le rôle de hello autant de fois. Peut-être que le temps hello limite est trop courte pour les toocomplete leurs tâches, ou peut-être qu’ils sont à l’aide de scripts tooautomatically activer un rôle. |
| **Les rôles ne nécessitent pas l’authentification multifacteur pour l’activation** |Il existe des rôles sans l’authentification Multifacteur activée dans les paramètres de hello. |Nous exiger l’authentification Multifacteur pour les rôles de hello plus privilégié, mais vous encourageons vivement que vous activez l’authentification Multifacteur pour l’activation de tous les rôles. |
| **Les administrateurs n’utilisent par leurs rôles privilégiés** |Certains administrateurs éligibles n’ont pas activé leurs rôles récemment. |Démarrer une révision toodetermine hello les utilisateurs d’accès que vous n’avez plus besoin accès. |
| **Trop d'administrateurs généraux** |Le nombre d’administrateurs généraux est supérieur au nombre recommandé. |Si vous avez un grand nombre d’administrateurs généraux, il est probable que les utilisateurs reçoivent plus d’autorisations que nécessaire. Accessible sans les utilisateurs de déplacer privilégié des rôles, ou certains d'entre eux qu’éligible pour le rôle hello au lieu d’attribué de manière permanente. |

## <a name="configure-security-alert-settings"></a>Configurez les paramètres d'alerte de sécurité
Vous pouvez personnaliser certaines des alertes de sécurité hello dans toowork PIM avec l’environnement et les objectifs de sécurité. Suivez ces panneau des paramètres de hello tooreach comme suit :

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com/) et sélectionnez hello **Azure AD Privileged Identity Management** vignette du tableau de bord hello.
2. Sélectionnez **Rôles privilégiés gérés** > **Paramètre** > **Paramètres des alertes**.
   
    ![Accédez toosecurity des paramètres des alertes][2]

### <a name="roles-are-being-activated-too-frequently-alert"></a>Alerte « Les rôles sont activés trop fréquemment »
Cette alerte si un utilisateur qui active les déclencheurs hello même rôle privilégié plusieurs fois pendant une période spécifiée. Vous pouvez configurer les deux hello temps période et hello nombre d’activations.

* **Période de renouvellement de l’activation**: spécifier en jours, heures, minutes et deuxième fois hello période souhaitée renouvellements suspecte de toouse tootrack.
* **Nombre de renouvellements de l’activation de**: spécifiez le nombre hello d’activations, à partir de 2 too100, que vous considérez comme digne d’alerte, dans le laps de temps hello vous avez choisi. Vous pouvez modifier ce paramètre par le curseur de hello mobile, ou tapez un nombre dans la zone de texte hello.

### <a name="there-are-too-many-global-administrators-alert"></a>Alerte « Trop d'administrateurs généraux »
PIM déclenche cette alerte si deux critères correspondent, et vous pouvez configurer ces deux valeurs. Tout d’abord, vous devez tooreach un certain seuil d’administrateurs généraux. Puis vous devez réserver un certain pourcentage du total de vos affectations à des rôles d’administrateur général. Si vous répondent à une de ces mesures, alerte de hello n’apparaît pas.  

* **Nombre minimal d’administrateurs généraux**: spécifiez le nombre hello d’administrateurs généraux, à partir de 2 too100, que vous envisagez un montant unsafe.
* **Pourcentage d’administrateurs généraux**: spécifiez le pourcentage hello des administrateurs globaux, à partir de 0 % too100 %, ce qui n’est pas sécurisé dans votre environnement.

### <a name="administrators-arent-using-their-privileged-roles-alert"></a>Alerte « Les administrateurs n’utilisent pas leurs rôles privilégiés »
Cette alerte se déclenche si un utilisateur reste un certain temps sans activer un rôle.

* **Nombre de jours**: spécifiez hello nombre de jours, à partir de 0 too100, sans activer un rôle d’un utilisateur.

## <a name="next-steps"></a>Étapes suivantes
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-configure-security-alerts/PIM_security_dash.png
[2]: ./media/active-directory-privileged-identity-management-how-to-configure-security-alerts/PIM_security_settings.png
