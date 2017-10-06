---
title: "Azure Active Directory Domain Services : activer la synchronisation de mot de passe | Microsoft Docs"
description: Prise en main des services de domaine Azure Active Directory
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 5a32a0df-a3ca-4ebe-b980-91f58f8030fc
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/30/2017
ms.author: maheshu
ms.openlocfilehash: 8e073df9de2996f5ad159dda746881c014ea3d66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-password-synchronization-tooazure-active-directory-domain-services"></a>Activer la synchronisation de mot de passe tooAzure les Services de domaine Active Directory
Dans les tâches précédentes, vous avez activé Azure Active Directory Domain Services pour votre locataire Azure Active Directory (Azure AD). la tâche suivante Hello est synchronisation tooenable des hachages d’informations d’identification requises pour tooAzure de l’authentification NT LAN Manager (NTLM) et Kerberos, les Services de domaine Active Directory. Une fois que vous avez configuré la synchronisation des informations d’identification, les utilisateurs peuvent se connecter dans toohello le domaine géré avec leurs informations d’identification d’entreprise.

Hello différentes étapes sont différents pour les comptes d’utilisateur utilisateur cloud uniquement les comptes Visual Studio qui sont synchronisés à partir de votre annuaire local à l’aide d’Azure AD Connect.  Si votre client Azure AD a une combinaison de cloud uniquement les utilisateurs et les utilisateurs de votre service Active Directory, vous devez tooperform les deux étapes.

<br>

> [!div class="op_single_selector"]
> * **Comptes d’utilisateur uniquement dans le cloud**: [synchroniser les mots de passe pour le domaine géré de tooyour des comptes d’utilisateurs uniquement dans le cloud](active-directory-ds-getting-started-password-sync.md)
> * **Comptes d’utilisateur locaux**: [synchroniser les mots de passe des comptes d’utilisateur synchronisés à partir de votre site AD tooyour gérés domaine](active-directory-ds-getting-started-password-sync-synced-tenant.md)
>
>

<br>

## <a name="task-5-enable-password-synchronization-tooyour-managed-domain-for-cloud-only-user-accounts"></a>Tâche 5 : activer le mot de passe tooyour managé domaine de synchronisation des comptes d’utilisateur uniquement dans le cloud
utilisateurs tooauthenticate sur hello managée domaine, Azure Active Directory Domain Services a besoin des informations d’identification hachages dans un format qui convient pour l’authentification NTLM et Kerberos. Azure AD ne pas générer et stocker les hachages d’informations d’identification au format hello qui est requis pour l’authentification NTLM ou Kerberos, jusqu'à ce que vous activez Azure Active Directory Domain Services pour votre client. Pour des raisons évidentes de sécurité, Azure AD ne stocke pas non plus d’informations de mot de passe dans un format en texte clair. Par conséquent, Azure AD n’a pas un moyen tooautomatically générer ces hachages d’informations d’identification NTLM ou Kerberos selon les informations d’identification existantes des utilisateurs.

> [!NOTE]
> Si votre organisation a des comptes d’utilisateur uniquement dans le cloud, les utilisateurs qui ont besoin de Services de domaine Active Directory toouse Azure doivent changer leurs mots de passe. Un compte d’utilisateur uniquement dans le cloud est un compte qui a été créé dans votre annuaire Azure AD à l’aide de hello portail Azure ou applets de commande PowerShell Azure AD. Ces comptes d’utilisateurs ne sont pas synchronisés à partir d’un répertoire local.
>
>

Ce processus de modification de mot de passe entraîne des informations d’identification hello hachages qui sont requis par Azure Active Directory Domain Services pour toobe de l’authentification Kerberos et NTLM générée dans Azure AD. Vous pouvez soit faire expirer les mots de passe hello pour tous les utilisateurs de hello client qui ont besoin de Services de domaine Active Directory toouse Azure ou leur demander de toochange leurs mots de passe.

### <a name="enable-ntlm-and-kerberos-credential-hash-generation-for-a-cloud-only-user-account"></a>Activer la génération du hachage des informations d’identification NTLM et Kerberos pour un compte d’utilisateur dans le cloud uniquement
Voici les instructions hello que nécessaires tooprovide utilisateurs, afin qu’ils peuvent modifier leurs mots de passe :

1. Accédez toohello [panneau d’accès Azure AD](http://myapps.microsoft.com) page de votre organisation.

    ![Lancer le panneau d’accès Azure AD hello](./media/active-directory-domain-services-getting-started/access-panel.png)

2. Dans hello coin supérieur droit, cliquez sur votre nom, puis sélectionnez **profil** à partir du menu de hello.

    ![Sélectionner un profil](./media/active-directory-domain-services-getting-started/select-profile.png)

3. Sur hello **profil** page, cliquez sur **Change password**.

    ![Cliquez sur « Modifier le mot de passe »](./media/active-directory-domain-services-getting-started/user-change-password.png)

   > [!NOTE]
   > Si hello **Change password** option n’est pas affichée dans la fenêtre du panneau d’accès hello, assurez-vous que votre organisation a configuré [gestion des mots de passe dans Azure AD](../active-directory/active-directory-passwords-getting-started.md).
   >
   >
4. Sur hello **modifier le mot de passe** page, tapez votre mot de passe (ancien), tapez un nouveau mot de passe, puis confirmez-le.

    ![Créer un réseau virtuel pour les services de domaine Azure AD.](./media/active-directory-domain-services-getting-started/user-change-password2.png)

5. Cliquez sur **Envoyer**.

Quelques minutes après avoir modifié votre mot de passe, le nouveau mot de passe hello est utilisable dans Azure Active Directory Domain Services. Après quelques minutes (en général, environ 20 minutes), vous pouvez vous connecter toocomputers qui appartiennent à un domaine géré de toohello jointes à l’aide du mot de passe hello qui vient d’être modifié.

## <a name="related-content"></a>Contenu connexe
* [Comment tooupdate votre mot de passe](../active-directory/active-directory-passwords-update-your-own-password.md)
* [Prise en main de la gestion de mot de passe dans Azure AD](../active-directory/active-directory-passwords-getting-started.md)
* [Activer la synchronisation de mot de passe du locataire tooAzure Active Directory Domain Services pour un Azure AD synchronisé](active-directory-ds-getting-started-password-sync-synced-tenant.md)
* [Administrer un domaine managé par Azure Active Directory Domain Services ](active-directory-ds-admin-guide-administer-domain.md)
* [Joindre un domaine géré par Azure Active Directory Domain Services de tooan de machine virtuelle Windows](active-directory-ds-admin-guide-join-windows-vm.md)
* [Joindre un domaine géré par les Services de domaine Active Directory de Azure de tooan de machine virtuelle Red Hat Enterprise Linux](active-directory-ds-admin-guide-join-rhel-linux-vm.md)
