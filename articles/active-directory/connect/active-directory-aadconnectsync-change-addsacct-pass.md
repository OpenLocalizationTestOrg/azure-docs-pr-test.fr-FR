---
title: "Synchronisation Azure AD Connect : mot de passe du compte de service d’annuaire hello AD modification | Documents Microsoft"
description: "Document de cette rubrique décrit comment tooupdate Azure AD Connect après le mot de passe hello du compte de hello AD DS est modifiée."
services: active-directory
keywords: "Compte AD DS, compte Active Directory, mot de passe"
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: 76b19162-8b16-4960-9e22-bd64e6675ecc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 2707c9246446612f8d083ecde876b3b4fb2435ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="changing-hello-ad-ds-account-password"></a>Modification de mot de passe de compte hello AD DS
compte de Hello AD DS fait référence toohello compte d’utilisateur utilisé par toocommunicate Azure AD Connect avec Active Directory local. Si vous modifiez le mot de passe hello Hello compte AD DS, vous devez mettre à jour un Service Azure AD Connect synchronisation avec le nouveau mot de passe hello. Dans le cas contraire, hello que la synchronisation peut ne plus synchroniser correctement avec hello Active Directory sur site et vous rencontrerez hello les erreurs suivantes :

* Bonjour opération Synchronization Service Manager, toute importation ou d’exportation avec local échoue AD avec **non-start-informations d’identification** erreur.

* Dans l’Observateur d’événements Windows, journal des événements application hello contient une erreur avec **événement ID 6000** et message **'agent de gestion hello « contoso.com » a échoué toorun, car les informations d’identification hello n’étaient pas valides'** .


## <a name="how-tooupdate-hello-synchronization-service-with-new-password-for-ad-ds-account"></a>Comment tooupdate hello Service de synchronisation avec le nouveau mot de passe pour le compte de domaine Active Directory
tooupdate hello Service de synchronisation avec le nouveau mot de passe hello :

1. Démarrez hello Synchronization Service Manager (Service de synchronisation de début →).
</br>![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)  

2. Accédez toohello **connecteurs** onglet.

3. Sélectionnez hello **Connecteur AD** qui correspond le compte de service d’annuaire toohello AD dont son mot de passe a été modifié.

4. Sous **Actions**, sélectionnez **Propriétés**.

5. Dans la boîte de dialogue contextuelle hello, sélectionnez **connecter tooActive Directory forêt**:

6. Entrez hello nouveau mot de passe du compte de hello AD DS dans hello **mot de passe** zone de texte.

7. Cliquez sur **OK** toosave hello nouveau mot de passe et de la boîte de dialogue contextuelle hello fermer.

8. Redémarrage hello Service Azure AD Connect synchronisation sous le Gestionnaire de contrôle de Service Windows. Il s’agit de tooensure que toute référence toohello ancien mot de passe est supprimé du cache de mémoire hello.

## <a name="next-steps"></a>Étapes suivantes
**Rubriques de présentation**

* [Azure AD Connect Sync - Présentation et personnalisation des options de synchronisation](active-directory-aadconnectsync-whatis.md)

* [Intégration de vos identités locales avec Azure Active Directory](active-directory-aadconnect.md)
