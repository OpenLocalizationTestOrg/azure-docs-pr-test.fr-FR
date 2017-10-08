---
title: "Synchronisation Azure AD Connect : comment toomanage hello Azure AD compte de service | Documents Microsoft"
description: Cette rubrique explique comment toorestore hello Azure AD compte de service.
services: active-directory
keywords: "AADSTS70002, AADSTS50054, comment tooreset hello mot de passe pour hello synchronisation d’Azure AD Connect compte du service du connecteur"
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 6077043a-27f1-4304-a44b-81dc46620f24
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: e563518eae173de42a1d40bb5a76e63f29f9da42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-how-toomanage-hello-azure-ad-service-account"></a>Synchronisation Azure AD Connect : comment toomanage hello Azure AD compte de service
compte de service Hello utilisé par le connecteur Azure AD de hello est supposée service toobe libre. Si vous devez tooreset ses informations d’identification, cette rubrique est pour vous. Par exemple, si un administrateur Global a par erreur réinitialisation hello un mot de passe sur le compte de service hello à l’aide de PowerShell.

## <a name="reset-hello-credentials"></a>Réinitialiser les informations d’identification hello
Si le compte de service de hello défini sur hello connecteur Azure AD ne peut pas contacter Azure AD en raison de problèmes de tooauthentication, mot de passe hello peut être réinitialisé.

1. Connectez-vous au serveur de synchronisation Azure AD Connect toohello et démarrer PowerShell.
2. Exécutez `Add-ADSyncAADServiceAccount`.  
   ![PowerShell cmdlet addadsyncaadserviceaccount](./media/active-directory-aadconnectsync-howto-azureadaccount/addadsyncaadserviceaccount.png)
3. Fournissez les informations d’identification de l’administrateur général Azure AD.

Cette applet de commande réinitialise le mot de passe hello pour le compte de service hello et mettre à jour dans Azure AD et dans le moteur de synchronisation hello.

## <a name="known-issues-these-steps-can-solve"></a>Problèmes connus pouvant être résolus par les procédures indiquées ci-après
Cette section est une liste d’erreurs signalées par les clients qui ont été résolus par un informations d’identification réinitialiser sur hello compte de service Azure AD.

- - -
Événement 6900  
serveur de Hello a rencontré une erreur inattendue lors du traitement d’une notification de modification de mot de passe :  
AADSTS70002 : erreur de validation des informations d’identification. AADSTS50054 : l’ancien mot de passe est utilisé pour l’authentification.

- - -
Événement 659  
Erreur lors de la récupération de la configuration de la synchronisation de stratégie de mot de passe. Microsoft.IdentityModel.Clients.ActiveDirectory.AdalServiceException :  
AADSTS70002 : erreur de validation des informations d’identification. AADSTS50054 : l’ancien mot de passe est utilisé pour l’authentification.

## <a name="next-steps"></a>Étapes suivantes
**Rubriques de présentation**

* [Azure AD Connect Sync - Présentation et personnalisation des options de synchronisation](active-directory-aadconnectsync-whatis.md)
* [Intégration de vos identités locales avec Azure Active Directory](active-directory-aadconnect.md)

