---
title: "Azure AD Connect : authentification unique transparente - Questions fréquentes | Microsoft Docs"
description: "Elles en sonttrop de réponses aux questions sur Azure Active Directory transparente l’authentification unique."
services: active-directory
keywords: "Qu’est-ce qu’Azure AD Connect, Installation d’Active Directory, Composants requis pour Azure AD, SSO, Authentification unique"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: billmath
ms.openlocfilehash: e91e7950670633c08c180ece873f7451fa19eef8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-seamless-single-sign-on-frequently-asked-questions"></a>Authentification unique transparente Azure Active Directory : questions fréquentes

Dans cet article, nous répondons au forum aux questions sur l’authentification unique et transparente Azure Active Directory. N’hésitez pas à le consulter régulièrement, du contenu nouveau y est fréquemment ajouté.

>[!IMPORTANT]
>fonctionnalité d’authentification unique transparente Hello est actuellement en version préliminaire.

## <a name="what-sign-in-methods-do-seamless-sso-work-with"></a>Avec quelles méthodes de connexion l’authentification unique transparente est-elle compatible ?

L’authentification unique transparente peut être combiné avec deux hello [synchronisation du hachage de mot de passe](active-directory-aadconnectsync-implement-password-synchronization.md) ou [authentification directe](active-directory-aadconnect-pass-through-authentication.md) méthodes de connexion. Toutefois cette fonctionnalité ne peut pas être utilisée avec les services de fédération Active Directory (ADFS).

## <a name="is-seamless-sso-a-free-feature"></a>La fonctionnalité d’authentification unique transparente est-elle gratuite ?

L’authentification unique transparente est une fonctionnalité gratuite et vous n’avez pas besoin des éditions payantes d’Azure AD toouse il. Il reste disponible lors de la fonctionnalité de hello rendue publique.

## <a name="what-applications-take-advantage-of-domainhint-or-loginhint-parameter-capability-of-seamless-sso"></a>Quelles sont les applications qui tirent parti des paramètres `domain_hint` et `login_hint` de l’authentification unique transparente ?

Nous sommes dans le processus hello de compilation de la liste de hello des applications qui envoient ces paramètres et ces hello ceux qui ne. Si vous avez des applications qui vous intéressent, faites-le nous savoir dans la section des commentaires hello.

## <a name="does-seamless-sso-support-alternate-id-as-hello-username-instead-of-userprincipalname"></a>La prend en charge l’authentification unique transparente `Alternate ID` comme hello du nom d’utilisateur, au lieu de `userPrincipalName`?

Oui. Prend en charge de l’authentification unique transparente `Alternate ID` comme hello nom d’utilisateur configuré dans Azure AD Connect comme [ici](active-directory-aadconnect-get-started-custom.md). Toutes les applications Office 365 ne prennent pas en charge `Alternate ID`. Consultez la documentation de l’application toohello spécifique pour l’instruction de prise en charge hello.

## <a name="i-want-tooregister-non-windows-10-devices-with-azure-ad-without-using-ad-fs-can-i-use-seamless-sso-instead"></a>Je veux tooregister non - Windows 10 avec Azure AD, sans utiliser les services AD FS. Puis-je à la place utiliser l’authentification unique transparente ?

Oui, ce scénario nécessite la version 2.1 ou ultérieure de hello [client de jonction](https://www.microsoft.com/download/details.aspx?id=53554).

## <a name="how-can-i-roll-over-hello-kerberos-decryption-key-of-hello-azureadssoacct-computer-account"></a>Comment puis-je pour restaurer sur la clé de déchiffrement hello Kerberos Hello `AZUREADSSOACCT` compte d’ordinateur ?

Il est important, elles sonttrop substituer la clé de déchiffrement hello Kerberos Hello `AZUREADSSOACCT` compte d’ordinateur (c'est-à-dire, Azure AD) créé dans votre site dans la forêt Active Directory.

>[!IMPORTANT]
>Nous vous recommandons de restaurer sur la clé de déchiffrement hello Kerberos au moins tous les 30 jours.

Procédez comme suit sur le serveur local de hello où vous exécutez Azure AD Connect :

### <a name="step-1-get-list-of-ad-forests-where-seamless-sso-has-been-enabled"></a>Étape 1. Obtenez la liste des forêts AD dans lesquelles l’authentification unique transparente a été activée.

1. Tout d’abord, téléchargez et installez hello [Assistant Microsoft Online Services Sign-In](http://go.microsoft.com/fwlink/?LinkID=286152).
2. Puis téléchargez et installez hello [64 bits du module Active Directory de Azure pour Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).
3. Accédez toohello `%programfiles%\Microsoft Azure Active Directory Connect` dossier.
4. Module PowerShell de l’authentification unique transparente d’hello importation à l’aide de cette commande : `Import-Module .\AzureADSSO.psd1`.
5. Exécutez PowerShell ISE en tant qu’administrateur. Dans PowerShell, appelez `New-AzureADSSOAuthenticationContext`. Cette commande doit vous donner une fenêtre contextuelle tooenter droits d’administrateur Global de votre locataire.
6. Appelez `Get-AzureADSSOStatus`. Cette commande fournit que Hello de liste des forêts d’Active Directory (Regardez dans la liste les domaines « hello ») sur lequel cette fonctionnalité a été activée.

### <a name="step-2-update-hello-kerberos-decryption-key-on-each-ad-forest-that-it-was-set-it-up-on"></a>Étape 2. Mettre à jour la clé de déchiffrement hello Kerberos sur chaque forêt Active Directory auquel il a été attribué sur

1. Appelez `$creds = Get-Credential`. Lorsque vous y êtes invité, entrez informations d’identification d’administrateur de domaine de hello hello destiné à la forêt Active Directory.
2. Appelez `Update-AzureADSSOForest -OnPremCredentials $creds`. Cette commande mises à jour hello clé de déchiffrement de Kerberos pour hello `AZUREADSSOACCT` compte d’ordinateur dans cette forêt Active Directory spécifique et il met à jour dans Azure AD.
3. Répétez hello étapes pour chaque forêt Active Directory que vous avez configuré la fonctionnalité de hello sur précédentes.

>[!IMPORTANT]
>Vérifiez que vous avez _ne_ exécuter hello `Update-AzureADSSOForest` commande plusieurs fois. Dans le cas contraire, la fonctionnalité de hello cesse de fonctionner jusqu'à ce que hello les tickets Kerberos de vos utilisateurs expirent et sont régénérées par votre annuaire Active Directory local.

## <a name="how-can-i-disable-seamless-sso"></a>Comment désactiver l’authentification unique transparente ?

L’authentification unique transparente peut être désactivée à l’aide d’Azure AD Connect.

Exécutez Azure AD Connect, cliquez sur "Modifier la connexion utilisateur" puis sur "Suivant". Puis désactivez option « Activer l’authentification unique » de hello. Continuez l’Assistant de hello. Après l’achèvement de l’Assistant de hello, l’authentification unique transparente est désactivé sur votre client.

Cependant, le message suivant s’affiche à l’écran :

« Single sign-on est maintenant désactivée, mais il existe des étapes manuelles supplémentaires tooperform dans l’ordre toocomplete nettoyage. En savoir plus."

toocomplete hello processus, suivez ces étapes manuelles sur le serveur local de hello où vous exécutez Azure AD Connect :

### <a name="step-1-get-list-of-ad-forests-where-seamless-sso-has-been-enabled"></a>Étape 1. Obtenez la liste des forêts AD dans lesquelles l’authentification unique transparente a été activée.

1. Tout d’abord, téléchargez et installez hello [Assistant Microsoft Online Services Sign-In](http://go.microsoft.com/fwlink/?LinkID=286152).
2. Puis téléchargez et installez hello [64 bits du module Active Directory de Azure pour Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).
3. Accédez toohello `%programfiles%\Microsoft Azure Active Directory Connect` dossier.
4. Module PowerShell de l’authentification unique transparente d’hello importation à l’aide de cette commande : `Import-Module .\AzureADSSO.psd1`.
5. Exécutez PowerShell ISE en tant qu’administrateur. Dans PowerShell, appelez `New-AzureADSSOAuthenticationContext`. Cette commande doit vous donner une fenêtre contextuelle tooenter droits d’administrateur Global de votre locataire.
6. Appelez `Get-AzureADSSOStatus`. Cette commande fournit que Hello de liste des forêts d’Active Directory (Regardez dans la liste les domaines « hello ») sur lequel cette fonctionnalité a été activée.

### <a name="step-2-manually-delete-hello-azureadssoacct-computer-account-from-each-ad-forest-that-you-see-listed"></a>Étape 2. Supprimez manuellement les hello `AZUREADSSOACCT` compte d’ordinateur à partir de chaque forêt Active Directory que vous voyez.

## <a name="next-steps"></a>Étapes suivantes

- [**Démarrage rapide**](active-directory-aadconnect-sso-quick-start.md) : découvrez l’authentification unique transparente Azure AD.
- [**Immersion technique**](active-directory-aadconnect-sso-how-it-works.md) : découvrez comment fonctionne cette fonctionnalité.
- [**Résoudre les problèmes** ](active-directory-aadconnect-troubleshoot-sso.md) -en savoir comment tooresolve commun problèmes avec la fonctionnalité de hello.
- [**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) : pour le dépôt de nouvelles demandes de fonctionnalités.
