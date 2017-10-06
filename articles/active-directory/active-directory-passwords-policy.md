---
title: "Stratégie : réinitialisation du mot de passe en libre-service Azure AD | Microsoft Docs"
description: "Options de stratégie de réinitialisation de mot de passe en libre-service Azure AD"
services: active-directory
keywords: "Gestion des mots de passe Active Directory, gestion des mots de passe, réinitialisation de mot de passe en libre-service Azure AD"
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: af7cb13794bf3a9fee91d355f788aa5c2246e57c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="password-policies-and-restrictions-in-azure-active-directory"></a>Stratégies et restrictions de mot de passe dans Azure Active Directory

Cet article décrit les stratégies de mot de passe hello et des exigences de complexité associées aux comptes d’utilisateur stockés dans votre locataire Azure AD.

## <a name="administrator-password-policy-differences"></a>Différences en matière de stratégie de mot de passe administrateur

Microsoft met en œuvre une stratégie de réinitialisation des mots de passe **à deux entrées** par défaut pour n’importe quel rôle d’administrateur Azure (exemple : administrateur général, administrateur de support technique, administrateur de mots de passe, etc.)

Cela désactive les administrateurs à partir de l’aide de questions de sécurité et applique des éléments suivants de hello.

Deux stratégie, nécessitant deux éléments de données de l’authentification de la grille (adresse de messagerie **et** numéro de téléphone), s’applique dans hello suivant circonstances

* Tous les rôles administrateur Azure
  * Administrateur du support technique
  * Administrateur de support de service
  * Administrateur de facturation
  * Prise en charge de niveau 1 de partenaire
  * Prise en charge de niveau 2 de partenaire
  * Administrateur de services Exchange
  * Administrateur de services Lync
  * Administrateur de compte utilisateur
  * Enregistreurs de répertoire
  * Administrateur général/Administrateur de l’entreprise
  * Administrateur de services SharePoint
  * Administrateur de conformité
  * Administrateur d’application
  * Security Administrator
  * Administrateur de rôle privilégié
  * Administrateur de services Intune
  * Administrateur du service de proxy d’application
  * Administrateur de services CRM
  * Administrateur du service Power BI
  
* 30 jours se sont écoulés dans un essai **OU**
* Le domaine personnel est présent (contoso.com) **OU**
* Azure AD Connect synchronise les identités à partir de votre répertoire local

### <a name="exceptions"></a>Exceptions
Stratégie un porte, nécessitant une portion de données d’authentification (adresse de messagerie **ou** numéro de téléphone), s’applique dans hello suivant circonstances

* 30 premiers jours d’un essai **OU**
* Le domaine personnel n’est pas présent (*.onmicrosoft.com) **ET** Azure AD Connect ne synchronise pas les identités


## <a name="userprincipalname-policies-that-apply-tooall-user-accounts"></a>Stratégies UserPrincipalName qui s’appliquent à des comptes d’utilisateur tooall

Chaque compte d’utilisateur qui doit toosign dans tooAzure AD doit avoir une valeur d’attribut de nom principal (UPN) unique utilisateur associée à leur compte. table Hello ci-dessous décrivent hello les stratégies qui s’appliquent tooboth local synchronisé de comptes d’utilisateur Active Directory toohello cloud et les comptes d’utilisateurs toocloud uniquement.

| Propriété | Conditions requises pour UserPrincipalName |
| --- | --- |
| Caractères autorisés |<ul> <li>A – Z</li> <li>a - z</li><li>0 – 9</li> <li> . - \_ ! \# ^ \~</li></ul> |
| Caractères non autorisés |<ul> <li>N’importe quel ' @' caractère qui n’est pas séparation nom d’utilisateur hello du domaine de hello.</li> <li>Ne peut pas contenir un caractère point '.' hello précédent ' @' symbole</li></ul> |
| Contraintes de longueur |<ul> <li>La longueur totale ne doit pas dépasser 113 caractères</li><li>64 caractères avant hello ' @' symbole</li><li>48 caractères après hello ' @' symbole</li></ul> |

## <a name="password-policies-that-apply-only-toocloud-user-accounts"></a>Stratégies de mot de passe qui s’appliquent uniquement les comptes d’utilisateurs toocloud

Hello tableau suivant décrit les paramètres de stratégie de mot de passe disponibles hello qui peuvent être appliqués toouser les comptes qui sont créés et gérés dans Azure AD.

| Propriété | Configuration requise |
| --- | --- |
| Caractères autorisés |<ul><li>A – Z</li><li>a - z</li><li>0 – 9</li> <li>@ # $ % ^ & * - _ ! + = [ ] { } &#124; \ : ‘ , . ? / ` ~ “ ( ) ;</li></ul> |
| Caractères non autorisés |<ul><li>Caractères Unicode</li><li>Espaces</li><li> **Mots de passe forts uniquement**: ne peut pas contenir de point '.' hello précédent ' @' symbole</li></ul> |
| Restrictions de mot de passe |<ul><li>8 caractères au minimum et 16 caractères au maximum</li><li>**Mots de passe forts uniquement**: nécessite de 3 des 4 suivants de hello :<ul><li>Caractères minuscules</li><li>Caractères majuscules</li><li>Chiffres (0-9)</li><li>Symboles (voir les restrictions de mot de passe ci-dessus)</li></ul></li></ul> |
| Délai d'expiration du mot de passe |<ul><li>Valeur par défaut : **90** jours </li><li>Valeur est configurable à l’aide d’applet de commande Set-MsolPasswordPolicy de hello hello Azure Module Active Directory pour Windows PowerShell.</li></ul> |
| Notification d'expiration du mot de passe |<ul><li>Valeur par défaut : **14** jours (avant l’expiration du mot de passe)</li><li>Valeur est configurable à l’aide d’applet de commande Set-MsolPasswordPolicy de hello.</li></ul> |
| Expiration du mot de passe |<ul><li>Valeur par défaut : **false** jours (indique que l’expiration du mot de passe est activée) </li><li>Valeur peut être configurée pour les comptes d’utilisateur individuels à l’aide d’applet de commande Set-MsolUser hello. </li></ul> |
| Historique de **modification** du mot de passe |L’ancien mot de passe **ne peut pas** être réutilisé lors de la **modification** du mot de passe. |
| Historique de **réinitialisation** du mot de passe | L’ancien mot de passe **peut** être réutilisé lors de la **réinitialisation** d’un mot de passe oublié. |
| Verrouillage de compte |Après 10 tentatives de connexion autorisées (mot de passe incorrect), utilisateur de hello sera verrouillé pendant une minute. Autres incorrect tentatives de connexion utilisateur de hello de verrouillage permettant d’accroître la durée. |

## <a name="set-password-expiration-policies-in-azure-active-directory"></a>Définir des stratégies d’expiration de mot de passe dans Azure Active Directory

Un administrateur global pour un service cloud Microsoft peut utiliser tooset de Microsoft Azure Module Active Directory pour Windows PowerShell hello des mots de passe utilisateur tooexpire pas. Vous pouvez également utiliser les applets de commande tooremove hello-n’expire jamais configuration ou toosee tooexpire pas les mots de passe utilisateur sont définies de Windows PowerShell. Ce guide s’applique à des fournisseurs de tooother tels que Microsoft Intune et Office 365, qui utilisent également sur Microsoft Azure Active Directory pour les services d’annuaire et identité.

> [!NOTE]
> Les mots de passe uniquement pour les comptes d’utilisateur qui ne sont pas synchronisés via la synchronisation d’annuaire peuvent être configurés toonot expirer. Pour plus d’informations sur la synchronisation d’annuaires, consultez [Connecter Active Directory à Azure AD](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect).
>
>

## <a name="set-or-check-password-policies-using-powershell"></a>Définir ou vérifier les stratégies de mot de passe à l’aide de PowerShell

tooget démarré, vous devez trop[télécharger et installer le module PowerShell Azure AD de hello](https://docs.microsoft.com/powershell/module/Azuread/?view=azureadps-2.0). Une fois que vous avez déjà installé, vous pouvez suivre les étapes de hello ci-dessous tooconfigure à chaque champ.

### <a name="how-toocheck-expiration-policy-for-a-password"></a>La stratégie d’expiration des toocheck un mot de passe
1. Se connecter tooWindows PowerShell à l’aide de vos informations d’identification d’administrateur d’entreprise.
2. Exécutez une des hello suivant de commandes :

   * toosee indique si un seul mot de passe est défini toonever expirent, vous exécutez hello suivant l’applet de commande à l’aide du nom d’hello utilisateur principal (UPN) (par exemple, aprilr@contoso.onmicrosoft.com) ou hello ID d’utilisateur de l’utilisateur de hello souhaité toocheck :`Get-MSOLUser -UserPrincipalName <user ID> | Select PasswordNeverExpires`
   * toosee hello « Le mot de passe n’expire jamais » de paramètre pour tous les utilisateurs, exécutez hello suivant l’applet de commande :`Get-MSOLUser | Select UserPrincipalName, PasswordNeverExpires`

### <a name="set-a-password-tooexpire"></a>Définir un mot de passe tooexpire

1. Se connecter tooWindows PowerShell à l’aide de vos informations d’identification d’administrateur d’entreprise.
2. Exécutez une des hello suivant de commandes :

   * mot de passe tooset hello d’un utilisateur afin que hello mot de passe expire, exécutez hello suivant l’applet de commande à l’aide du nom d’hello utilisateur principal (UPN) ou hello ID de hello utilisateur :`Set-MsolUser -UserPrincipalName <user ID> -PasswordNeverExpires $false`
   * les mots de passe hello tooset de tous les utilisateurs dans l’organisation de hello afin qu’ils expirent, utilisent hello suivant l’applet de commande :`Get-MSOLUser | Set-MsolUser -PasswordNeverExpires $false`

### <a name="set-a-password-toonever-expire"></a>Expiration du jeu une toonever de mot de passe

1. Se connecter tooWindows PowerShell à l’aide de vos informations d’identification d’administrateur d’entreprise.
2. Exécutez une des hello suivant de commandes :

   * mot de passe tooset hello d’un utilisateur toonever expirer, exécutez hello suivant l’applet de commande à l’aide du nom d’hello utilisateur principal (UPN) ou hello ID de hello utilisateur :`Set-MsolUser -UserPrincipalName <user ID> -PasswordNeverExpires $true`
   * les mots de passe hello tooset de tous les utilisateurs de hello dans une organisation de toonever expirer, exécutez hello suivant l’applet de commande :`Get-MSOLUser | Set-MsolUser -PasswordNeverExpires $true`

## <a name="next-steps"></a>Étapes suivantes

Hello suivant liens fournit des informations supplémentaires concernant le mot de passe réinitialisé à l’aide d’Azure AD

* [**Démarrage rapide**](active-directory-passwords-getting-started.md) : soyez rapidement opérationnel avec la gestion des mots de passe en libre-service d’Azure AD. 
* [**Licences**](active-directory-passwords-licensing.md) : configurez vos licences Azure AD.
* [**Données** ](active-directory-passwords-data.md) : comprendre les données de hello est nécessaire et comment il est utilisé pour la gestion de mot de passe
* [**Déploiement** ](active-directory-passwords-best-practices.md) -planifier et déployer des utilisateurs de tooyour SSPR hello d’aide est disponible ici
* [**Personnaliser** ](active-directory-passwords-customize.md) -personnaliser hello apparence Hello SSPR expérience pour votre entreprise.
* [**Rapports**](active-directory-passwords-reporting.md) : découvrez si, quand et où vos utilisateurs accèdent aux fonctionnalités de réinitialisation de mot de passe en libre-service
* [**Présentation approfondie technique** ](active-directory-passwords-how-it-works.md) -accédez derrière hello RIDEAU toounderstand son fonctionnement
* [**Forum Aux Questions (FAQ)**](active-directory-passwords-faq.md) : Comment ? Pourquoi ? Quoi ? Où ? Qui ? Quand ? -Réponses tooquestions vous souhaitiez toujours tooask
* [**Résoudre les problèmes** ](active-directory-passwords-troubleshoot.md) -en savoir comment tooresolve commun problèmes que nous pouvons voir avec SSPR
