---
title: "aaaAzure AD à plusieurs niveaux de sécurité de mot de passe | Documents Microsoft"
description: "Explique comment Azure AD impose des mots de passe forts et protège les mots de passe des utilisateurs contre les cybercriminels,"
services: active-directory
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: joflore
ms.openlocfilehash: 10d8b600d9f4c02355b2cd8c5dccf8505aaf210d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="a-multi-tiered-approach-tooazure-ad-password-security"></a>Une approche multiniveau tooAzure AD mot de passe de sécurité

Cet article décrit quelques meilleures pratiques que vous pouvez suivre en tant qu’utilisateur ou un administrateur tooprotect des Account Microsoft Azure Active Directory (Azure AD).

 > [!NOTE]
 > Azure AD les administrateurs peuvent réinitialiser les mots de passe utilisateur à l’aide des instructions de hello dans l’article de hello [hello réinitialisation mot de passe pour un utilisateur dans Azure Active Directory](active-directory-users-reset-password-azure-portal.md).
 >
 > Les utilisateurs peuvent réinitialiser leur mot de passe à l’aide des instructions de hello dans l’article de hello [aide j’ai oublié mon mot de passe Azure AD](active-directory-passwords-update-your-own-password.md).
 >

## <a name="password-requirements"></a>Conditions requises pour les mots de passe

Azure AD incorpore hello suivant des mots de passe approches toosecuring communs :

* Exigences en termes de longueur du mot de passe
* Exigences en termes de « complexité » du mot de passe
* Expiration du mot de passe périodique et régulière

Pour plus d’informations sur le mot de passe réinitialisé dans Azure Active Directory, consultez la rubrique de hello [AD Azure mot de passe libre-service réinitialiser pour hello professionnel de l’informatique](active-directory-passwords.md).

## <a name="azure-ad-password-protections"></a>Protections de mot de passe Azure AD

Azure AD et hello système de comptes Microsoft utiliser éprouvées approches tooensure sécurisée la protection des mots de passe utilisateur et administrateur, notamment :

* Mots de passe interdits dynamiquement
* Verrouillage de mot de passe intelligent

Pour plus d’informations sur la gestion de mot de passe en fonction de recherche actuelle, consultez le livre blanc de hello [des conseils de mot de passe](http://aka.ms/passwordguidance).

### <a name="dynamically-banned-passwords"></a>Mots de passe interdits dynamiquement

Azure AD et les comptes Microsoft assurent la protection des mots de passe en interdisant dynamiquement tous les mots de passe utilisés couramment. équipe de Protection d’identité ID Azure Hello analyse régulièrement des listes de mot de passe interdit, empêchant les utilisateurs de sélectionner des mots de passe couramment utilisés. Ce service est disponible tooAzure AD et les clients du Service de compte Microsoft hello.

Lorsque vous créez des mots de passe, il est important pour les administrateurs tooencourage utilisateurs toochoose mot de passe des expressions qui incluent une combinaison unique de lettres, des chiffres, des caractères ou des mots. Cette approche permet des mots de passe utilisateur toomake toobe presque impossible compromis, mais il est plus facile pour les utilisateurs tooremember.

#### <a name="password-breaches"></a>Violations de mot de passe

Microsoft s’emploie toujours toostay une étape avant cybercrime.

équipe de Azure AD Identity Protection Hello analyse en permanence les mots de passe qui sont couramment utilisées. Cybercrime également utiliser similaire stratégies tooinform leurs attaques, telles que la génération un [table d’arc-en-ciel](https://en.wikipedia.org/wiki/Rainbow_table) pour le décodage des hachages de mot de passe.

Microsoft analyse en permanence [violations de données](https://www.privacyrights.org/data-breaches) toomaintain une liste de mises à jour dynamiquement interdit mot de passe, ce qui garantit que les mots de passe vulnérables sont interdites avant qu’ils deviennent une véritable menace tooAzure AD clients. Pour plus d’informations sur nos efforts de sécurité actuelle, consultez hello [rapport de sécurité Microsoft](https://www.microsoft.com/security/sir/default.aspx).

### <a name="smart-password-lockout"></a>Verrouillage de mot de passe intelligent

Lorsque Azure AD détecte un potentiel toohack lors de la tentative de cyber pénales dans un mot de passe, nous verrouiller le compte d’utilisateur de hello avec Active le verrouillage de mot de passe. Azure AD est conçu risque de hello toodetermine associé aux sessions de connexion spécifique. Ensuite, à l’aide de données de sécurité plus récentes de hello, nous appliquons toostop les menaces de verrouillage sémantique.

Si un utilisateur est verrouillé en dehors d’Azure AD, leur écran ressemble toohello similaire qui suit :

  ![Accès verrouillé au compte Azure AD](./media/active-directory-secure-passwords/locked-out-azuread.png)

Pour les autres comptes Microsoft, leur écran ressemble toohello similaire qui suit :

  ![Accès verrouillé au compte Microsoft](./media/active-directory-secure-passwords/locked-out-ms-accounts.png)

Pour plus d’informations sur le mot de passe réinitialisé dans Azure Active Directory, consultez la rubrique de hello [AD Azure mot de passe libre-service réinitialiser pour hello professionnel de l’informatique](active-directory-passwords.md).

  >[!NOTE]
  >Si vous êtes un administrateur Azure AD, vous souhaiterez peut-être toouse [Windows Hello](https://www.microsoft.com/windows/windows-hello) tooavoid dont vos utilisateurs créer des mots de passe traditionnels complètement.
  >

## <a name="next-steps"></a>Étapes suivantes

* [Comment tooupdate votre mot de passe](active-directory-passwords-update-your-own-password.md)
* [Notions de base Hello de gestion des identités de Azure](fundamentals-identity.md)
* [Rapport sur l’activité de réinitialisation de mot de passe](active-directory-passwords-reporting.md)


