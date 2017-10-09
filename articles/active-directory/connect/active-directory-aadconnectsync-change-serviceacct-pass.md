---
title: "Synchronisation Azure AD Connect : modification de compte de service de synchronisation de se connecter hello Azure AD | Documents Microsoft"
description: "Document de cette rubrique décrit la clé de chiffrement hello et comment tooabandon après le mot de passe hello est modifié."
services: active-directory
keywords: Compte de service de synchronisation Azure AD, mot de passe
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
ms.openlocfilehash: 11948ac4662f722e4f684ef6c9b9ccdc6387e60f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="changing-hello-azure-ad-connect-sync-service-account-password"></a>Modification mot de passe du compte de service synchronisation hello Azure AD Connect
Si vous modifiez le mot de passe du compte service de synchronisation des Azure AD Connect de hello, hello Service de synchronisation sera pas en mesure de démarrer correctement jusqu'à ce que vous avez abandonné la clé de chiffrement hello et réinitialisation du mot de passe de compte hello Azure AD Connect sync service. 

Azure AD Connect, dans le cadre de Services de synchronisation de hello utilise un chiffrement toostore clé hello des mots de passe de hello AD DS et les comptes de service Azure AD.  Ces comptes sont chiffrées avant d’être stockées dans la base de données hello. 

Hello clé de chiffrement utilisée est sécurisée à l’aide de [Protection des données (DPAPI) Windows](https://msdn.microsoft.com/library/ms995355.aspx). DPAPI protège la clé de chiffrement de hello hello **mot de passe du compte de service de synchronisation hello Azure AD Connect**. 

Si vous avez besoin de mot de passe du compte toochange hello service, vous pouvez utiliser les procédures hello dans [clé de chiffrement Abandoning hello Azure AD Sync de se connecter](#abandoning-the-azure-ad-connect-sync-encryption-key) tooaccomplish cela.  Ces procédures doivent également être utilisées si vous avez besoin d’une clé de chiffrement tooabandon hello pour une raison quelconque.

##<a name="issues-that-arise-from-changing-hello-password"></a>Problèmes résultant de la modification de mot de passe hello
Il existe deux choses toobe effectuée lorsque vous modifiez le mot de passe du compte de service hello.

Tout d’abord, vous devez le mot de passe toochange hello sous hello Gestionnaire de contrôle des services Windows.  Vous verrez les erreurs suivantes jusqu’à résolution du problème :


- Si vous essayez toostart hello Service de synchronisation dans le Gestionnaire de contrôle de Service Windows, l’erreur hello »**Windows n’a pas pu démarrer de service de Microsoft Azure AD Sync hello sur l’ordinateur Local**». **L’erreur 1069 : hello n’a pas démarré en raison de l’échec d’ouverture de session tooa.** "
- Dans l’Observateur d’événements Windows, journal des événements système hello contient une erreur avec **7038 d’ID d’événement** et le message «**hello service ADSync a été toolog impossible sur comme avec le mot de passe hello actuellement configuré en raison de toohello suivant erreur : nom d’utilisateur Hello ou un mot de passe est incorrect.** "

Ensuite, sous certaines conditions, la mise à jour de mot de passe hello, hello Service de synchronisation ne pouvez plus extraire clé de chiffrement hello via DPAPI. Sans la clé de chiffrement de hello hello de que service de synchronisation ne peut pas déchiffrer hello des mots de passe toosynchronize requis à partir locaux AD et Azure AD.
Vous voyez des erreurs telles que :

- Sous le Gestionnaire de contrôle de Service de Windows, si vous essayez de toostart hello Service de synchronisation et il ne peut pas récupérer la clé de chiffrement hello, elle échoue avec l’erreur « ** Windows n’a pas pu démarrer hello Microsoft Azure AD Sync sur ordinateur Local. Pour plus d’informations, consultez le journal des événements système hello. S’il s’agit d’un service non-Microsoft, contactez le fournisseur de service hello et consultez le code d’erreur spécifique tooservice **-21451857952 ***. »
- Dans l’Observateur d’événements Windows, journal des événements application hello contient une erreur avec **6028 d’ID d’événement** et le message d’erreur *»**clé de chiffrement du serveur hello n’est pas accessible.* *»*

tooensure que vous ne recevez pas ces erreurs, suivez les procédures de hello dans [clé de chiffrement Abandoning hello Azure AD Sync de se connecter](#abandoning-the-azure-ad-connect-sync-encryption-key) lors de la modification de mot de passe hello.
 
## <a name="abandoning-hello-azure-ad-connect-sync-encryption-key"></a>Abandon de la clé de chiffrement d’Azure AD Sync connecter hello
>[!IMPORTANT]
>Hello procédures suivantes s’appliquent uniquement tooAzure AD Connect version 1.1.443.0 ou antérieure.

Utilisez hello clé de chiffrement de procédures tooabandon hello suivante.

### <a name="what-toodo-if-you-need-tooabandon-hello-encryption-key"></a>Quelles toodo si vous avez besoin de clé de chiffrement hello tooabandon

Si vous avez besoin de clé de chiffrement tooabandon hello, utilisez-le hello suivant tooaccomplish de procédures.

1. [Abandonner la clé de chiffrement existante hello](#abandon-the-existing-encryption-key)

2. [Fournir un mot de passe hello Hello compte AD DS](#provide-the-password-of-the-ad-ds-account)

3. [Réinitialiser le mot de passe hello Hello compte de synchronisation Azure AD](#reinitialize-the-password-of-the-azure-ad-sync-account)

4. [Hello de démarrer le Service de synchronisation](#start-the-synchronization-service)

#### <a name="abandon-hello-existing-encryption-key"></a>Abandonner la clé de chiffrement existante hello
Abandonner la clé de chiffrement existante hello pour cette nouvelle clé de chiffrement peut être créée :

1. Ouvrez une session dans tooyour Azure AD Connect Server en tant qu’administrateur.

2. Démarrez une nouvelle session PowerShell.

3. Accédez à toofolder :`$env:Program Files\Microsoft Azure AD Sync\bin\`

4. Exécutez la commande hello :`./miiskmu.exe /a`

![Utilitaire de clé de chiffrement d’Azure AD Connect Sync](media/active-directory-aadconnectsync-encryption-key/key5.png)

#### <a name="provide-hello-password-of-hello-ad-ds-account"></a>Fournir un mot de passe hello Hello compte AD DS
Comme les mots de passe existants hello stockés à l’intérieur de la base de données hello n’est plus peuvent être déchiffrées, vous devez tooprovide hello Service de synchronisation avec un mot de passe hello du compte de hello AD DS. chiffre les Hello Service de synchronisation des mots de passe hello à l’aide de la nouvelle clé de chiffrement hello :

1. Démarrez hello Synchronization Service Manager (Service de synchronisation de début →).
</br>![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)  
2. Accédez toohello **connecteurs** onglet.
3. Sélectionnez hello **Connecteur AD** qui correspond à tooyour AD local. Si vous avez plus d’un connecteur Active Directory, répétez hello comme suit pour chacun d’eux.
4. Sous **Actions**, sélectionnez **Propriétés**.
5. Dans la boîte de dialogue contextuelle hello, sélectionnez **connecter tooActive Directory forêt**:
6. Mot de passe hello du compte de hello AD DS dans hello **mot de passe** zone de texte. Si vous ne connaissez pas son mot de passe, vous devez le définir tooa connue avant d’effectuer cette étape.
7. Cliquez sur **OK** toosave hello nouveau mot de passe et de la boîte de dialogue contextuelle hello fermer.
![Utilitaire de clé de chiffrement d’Azure AD Connect Sync](media/active-directory-aadconnectsync-encryption-key/key6.png)

#### <a name="reinitialize-hello-password-of-hello-azure-ad-sync-account"></a>Réinitialiser le mot de passe hello Hello compte de synchronisation Azure AD
Vous ne pouvez pas fournir directement de mot de passe de hello de service d’Azure AD hello toohello compte Service de synchronisation. Au lieu de cela, vous devez l’applet de commande hello toouse **Add-ADSyncAADServiceAccount** tooreinitialize hello compte de service Azure AD. applet de commande Hello réinitialise le mot de passe de compte hello et le rend disponible toohello Service de synchronisation :

1. Démarrez une nouvelle session PowerShell sur le serveur d’Azure AD Connect hello.
2. Exécutez l’applet de commande `Add-ADSyncAADServiceAccount`.
3. Dans la boîte de dialogue contextuelle hello, fournissent des informations d’identification d’administrateur Global de hello Azure AD pour votre locataire Azure AD.
![Utilitaire de clé de chiffrement d’Azure AD Connect Sync](media/active-directory-aadconnectsync-encryption-key/key7.png)
4. Si elle réussit, vous verrez l’invite de commandes PowerShell hello.

#### <a name="start-hello-synchronization-service"></a>Hello de démarrer le Service de synchronisation
Maintenant que hello Service de synchronisation a la clé de chiffrement toohello accès et tous les hello des mots de passe, il doit, vous pouvez redémarrer le service de hello de hello Gestionnaire de contrôle des services Windows :


1. Accédez tooWindows Gestionnaire de contrôle de Service (Services → démarrage).
2. Sélectionnez **Microsoft Azure AD Sync** et cliquez sur Redémarrer.

## <a name="next-steps"></a>Étapes suivantes
**Rubriques de présentation**

* [Azure AD Connect Sync - Présentation et personnalisation des options de synchronisation](active-directory-aadconnectsync-whatis.md)

* [Intégration de vos identités locales avec Azure Active Directory](active-directory-aadconnect.md)
