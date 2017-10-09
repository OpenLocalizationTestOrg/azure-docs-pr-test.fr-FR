---
title: 'Azure AD Connect : authentification directe - Limitations actuelles | Microsoft Docs'
description: "Cet article décrit les limitations actuelles de hello d’authentification de pass-through Azure Active Directory (Azure AD)."
services: active-directory
keywords: "Authentification directe Azure AD Connect, installation d’Active Directory, composants requis pour Azure AD, SSO, Authentification unique"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: billmath
ms.openlocfilehash: 2933745d071aae205c44659e6ea92697f390effb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-current-limitations"></a>Authentification directe Azure Active Directory : limitations actuelles

>[!IMPORTANT]
>L’authentification directe Azure AD est actuellement en préversion. Il s’agit d’une fonctionnalité gratuite et vous n’avez pas besoin des éditions payantes d’Azure AD toouse il. Authentification directe est uniquement disponible dans hello world-wide instance d’Azure AD et non sous [Microsoft Cloud Allemagne](http://www.microsoft.de/cloud-deutschland) et [Cloud de Microsoft Azure Government](https://azure.microsoft.com/features/gov/).

## <a name="supported-scenarios"></a>Scénarios pris en charge

Hello les scénarios suivants est entièrement pris en charge pendant l’aperçu :

- L’utilisateur se connecte dans toutes les applications basées sur un navigateur web.
- L’utilisateur se connecte dans les applications clientes Office 365 prenant en charge [l’authentification moderne](https://aka.ms/modernauthga).
- Azure AD Join pour les appareils Windows 10.
- Prise en charge d’Exchange ActiveSync.

## <a name="unsupported-scenarios"></a>Scénarios non pris en charge

Hello scénarios suivants sont _pas_ pris en charge pendant l’aperçu :

- Connexions des utilisateurs dans les applications clientes Office héritées (Office 2013 ou version antérieure). Les organisations sont encouragés tooswitch toomodern authentification, si possible. L’authentification moderne permet non seulement de prendre en charge l’authentification directe, mais également de sécuriser les comptes d’utilisateur à l’aide des fonctionnalités [d’accès conditionnel](../active-directory-conditional-access.md), comme l’authentification multifacteur.
- Connexions des utilisateurs à des applications clientes Skype Entreprise, y compris Skype Entreprise 2016.
- L’utilisateur se connecte dans PowerShell v1.0. Il est recommandé d’utiliser à la place PowerShell v2.0.

>[!IMPORTANT]
>Comme solution de contournement pour les scénarios non pris en charge, activez la synchronisation du hachage de mot de passe sur hello [fonctionnalités facultatives](active-directory-aadconnect-get-started-custom.md#optional-features) page dans l’Assistant de connexion hello Azure AD. Synchronisation du hachage de mot de passe joue le rôle de secours pour hello précédant les scénarios _uniquement_ (et _pas_ comme une générique tooPass via l’authentification de secours). Si vous n’avez pas besoin de ces scénarios, désactivez la synchronisation du hachage de mot de passe.

## <a name="next-steps"></a>Étapes suivantes
- [**Démarrage rapide**](active-directory-aadconnect-pass-through-authentication-quick-start.md) : Mise en route de l’authentification directe Azure AD.
- [**Immersion technique**](active-directory-aadconnect-pass-through-authentication-how-it-works.md) : découvrez comment fonctionne cette fonctionnalité.
- [**Forum aux Questions** ](active-directory-aadconnect-pass-through-authentication-faq.md) -réponses elles sonttrop aux questions.
- [**Résoudre les problèmes** ](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -en savoir comment tooresolve commun problèmes avec la fonctionnalité de hello.
- [**Authentification unique transparente Azure AD**](active-directory-aadconnect-sso.md) : explorez en détail cette fonctionnalité complémentaire.
- [**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) : pour formuler des demandes de nouvelles fonctionnalités.
