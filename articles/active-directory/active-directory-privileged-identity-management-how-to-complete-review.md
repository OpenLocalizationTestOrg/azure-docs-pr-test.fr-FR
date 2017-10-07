---
title: "aaaHow toocomplete une vérification de l’accès | Documents Microsoft"
description: "Une fois que vous avez démarré une vérification de l’accès dans Azure AD Privileged Identity Management, découvrez comment toocomplete il et vue hello résultats"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: abc2d3dd-afd5-42cf-8a17-6c11f5674c35
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: kgremban
ms.custom: pim
ms.openlocfilehash: f99ddf3ebcf80b51110326064d584f33d8e1679a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocomplete-an-access-review-in-azure-ad-privileged-identity-management"></a>Comment toocomplete un accès passez en revue dans Azure AD Privileged Identity Management
Les administrateurs de rôle privilégié peuvent examiner un accès privilégié une fois qu’une [révision de la sécurité a été démarrée](active-directory-privileged-identity-management-how-to-start-security-review.md). Azure AD Privileged Identity Management (PIM) envoie automatiquement un message électronique demandant aux utilisateurs tooreview leur accès. Si un utilisateur n’a pas reçu un message électronique, vous pouvez envoyer les instructions de hello [façon tooperform examiner une sécurité](active-directory-privileged-identity-management-how-to-perform-security-review.md).

Après la période de révision de sécurité hello ou tous les utilisateurs de hello ont terminé leurs examiner automatique, suivez les étapes de hello dans cette revue de hello toomanage article et afficher les résultats de hello.

## <a name="manage-security-reviews"></a>Gérer les révisions de sécurité
1. Accédez toohello [portail Azure](https://portal.azure.com/) et sélectionnez hello **Azure AD Privileged Identity Management** application sur votre tableau de bord.
2. Sélectionnez hello **accès révisions** section du tableau de bord hello.
3. Sélectionnez la vérification de l’accès hello que vous souhaitez toomanage.

Sur le panneau des détails de vérification de l’accès hello, il existe un nombre options pour la gestion de cette révision.

![Boutons de révision d’accès PIM - capture d’écran][1]

### <a name="remind"></a>Rappeler
Si une vérification de l’accès est configurée afin que les utilisateurs de hello examiner eux-mêmes, hello **rappeler** bouton envoie une notification. 

### <a name="stop"></a>Arrêter
Toutes les révisions d’accès ont une date de fin, mais vous pouvez utiliser hello **arrêter** bouton toofinish il tôt. Tous les utilisateurs n’ont pas été vérifiées à ce stade, ils ne sont pas en mesure de tooafter vous arrêtez la révision de hello. Vous ne pouvez pas redémarrer une révision arrêtée.

### <a name="apply"></a>Appliquer
Au terme d’une vérification de l’accès, soit parce que vous atteint la date de fin hello ou s’est arrêté manuellement, hello **appliquer** bouton implémente résultat hello de revue de hello. Si accès un utilisateur l’a été refusé dans la révision de hello, il s’agit d’étape hello qui va supprimer leur attribution de rôle.  

### <a name="export"></a>Exportation
Si vous souhaitez les résultats de hello tooapply de révision de sécurité hello manuellement, vous pouvez exporter la révision de hello. Hello **exporter** bouton démarre le téléchargement d’un fichier CSV. Vous pouvez gérer les résultats de hello dans Excel ou d’autres programmes qui s’ouvrent les fichiers CSV.

### <a name="delete"></a>Supprimer
Si vous n’êtes pas intéressé par hello examiner les autres, supprimez-le. Hello **supprimer** bouton supprime hello révision hello application PIM.

> [!IMPORTANT]
> Pas obtenir un avertissement avant que la suppression se produit, vous devez donc vous assurer que vous souhaitez toodelete passez en revue. 

## <a name="next-steps"></a>Étapes suivantes
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-complete-review/PIM_review_buttons.png
