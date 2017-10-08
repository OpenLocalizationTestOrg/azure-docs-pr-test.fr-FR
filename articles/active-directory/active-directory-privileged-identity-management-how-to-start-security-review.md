---
title: "aaaHow toostart une vérification de l’accès | Documents Microsoft"
description: "Découvrez comment toocreate un accès à examiner pour les identités privilégiées avec hello application d’Azure Privileged Identity Management."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 3e52b731-55f4-4c8a-ba87-9fd34033f52f
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/04/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 24feac307f77c69b5d68d6ae0623dbcb52416b01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toostart-an-access-review-in-azure-ad-privileged-identity-management"></a>Comment toostart un accès passez en revue dans Azure AD Privileged Identity Management
Les attributions de rôles deviennent « obsolètes » lorsque les utilisateurs bénéficient d’un accès privilégié dont ils n’ont plus besoin. Dans l’ordre tooreduce hello risque est associé à ces attributions de rôles obsolètes, les administrateurs de rôle privilégié doivent examiner régulièrement de rôles hello auxquelles les utilisateurs ont été attribuées. Ce document décrit les étapes de hello pour démarrer une vérification de l’accès dans Azure AD Privileged Identity Management (PIM).

## <a name="start-an-access-review"></a>Démarrage d’une révision d’accès
> [!NOTE]
> Si vous n’avez pas ajouté le tableau de bord tooyour hello PIM application Bonjour portail Azure, consultez les étapes de hello dans [prise en main d’Azure Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md)
> 
> 

À partir de la page principale hello PIM application, Voici trois façons toostart une vérification de l’accès :

* **Révisions d’accès** > **Ajouter**
* **Rôles** > bouton **Révision**
* Sélectionnez hello rôle spécifique toobe vérifiés à partir de la liste de rôles hello > **révision** bouton

Lorsque vous cliquez sur hello **Examinez** bouton, hello **démarrer une vérification de l’accès** panneau s’affiche. Dans ce panneau, vous êtes continu tooconfigure hello revue avec un nom de délai d’exécution, choisissez un rôle tooreview et décidez qui effectuera la révision de hello.

![Démarrage d’une vérification d’accès - capture d’écran][1]

### <a name="configure-hello-review"></a>Configurer la vérification de hello
Examinez de toocreate d’accès, vous devez tooname et affectez-lui une date de début et de fin.

![Configuration d’une révision - capture d’écran][2]

Faites en sorte que longueur hello Hello examiner suffisamment longtemps pour que les utilisateurs toocomplete. Si vous avez terminé avant la date de fin hello, vous pouvez toujours s’arrêter révision de hello tôt.

### <a name="choose-a-role-tooreview"></a>Choisissez un rôle tooreview
Chaque révision se concentre sur un seul rôle. Sauf si vous avez démarré hello vérification de l’accès à partir d’un panneau de rôle spécifique, vous devez maintenant toochoose un rôle.

1. Accédez trop**consulter l’appartenance au rôle**
   
    ![Réviser une appartenance à un rôle - capture d’écran][3]
2. Choisir un rôle à partir de la liste de hello.

### <a name="decide-who-will-perform-hello-review"></a>Décider qui effectuera la révision de hello
Il existe trois options pour effectuer une révision. Vous pouvez affecter hello révision toosomeone toocomplete else, vous pouvez le faire vous-même, ou vous pouvez avoir à chaque utilisateur de consulter leur accès.

1. Accédez trop**sélectionnez relecteurs**
   
    ![Sélection des réviseurs - capture d’écran][4]
2. Choisissez une des options de hello :
   
   * **Sélectionnez le réviseur**: utilisez cette option lorsque vous ne savez pas qui a besoin de l’accès. Avec cette option, vous pouvez affecter un propriétaire de la ressource hello révision tooa ou toocomplete de gestionnaire de groupe.
   * **Me**: utile si vous souhaitez toopreview comment access passe en revue le travail, ou vous souhaitez tooreview pour le compte de personnes qui ne peuvent pas.
   * **Les membres d’examiner eux-mêmes**: utilisez cette revue d’utilisateurs option toohave hello leurs attributions de rôle.

### <a name="start-hello-review"></a>Démarrer hello révision
Enfin, vous avez toorequire d’option hello les utilisateurs à fournir une raison si elles approuver leur accès. Ajouter une description de la révision de hello si vous le souhaitez, puis sélectionnez **Démarrer**.

Assurez-vous que vous informer vos utilisateurs qu’il existe une vérification de l’accès en attente pour les et les afficher [façon tooperform examiner un accès](active-directory-privileged-identity-management-how-to-perform-security-review.md).

## <a name="manage-hello-access-review"></a>Gérer la vérification de l’accès hello
Vous pouvez suivre la progression de hello à mesure que les réviseurs hello effectuent leurs révisions Bonjour du tableau de bord Azure AD PIM, Bonjour accès examine la section. Aucun droit d’accès ne sera modifiée dans le répertoire hello jusqu'à ce que [se termine de révision de hello](active-directory-privileged-identity-management-how-to-complete-review.md).

Jusqu'à ce que la période de révision hello est terminée, vous pouvez rappeler les utilisateurs toocomplete leur révision ou stop hello révision tôt contre tout accès hello section révision.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="pim-table-of-contents"></a>Sommaire PIM
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_start_review.png
[2]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_configure.png
[3]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_role.png
[4]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_reviewers.png
