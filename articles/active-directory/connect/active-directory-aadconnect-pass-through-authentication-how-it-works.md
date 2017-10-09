---
title: "Azure AD Connect : Fonctionnement de l’authentification directe | Microsoft Docs"
description: "Cet article décrit le fonctionnement de l’authentification directe Azure Active Directory."
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
ms.date: 07/27/2017
ms.author: billmath
ms.openlocfilehash: ffcebee572a9ba2840e81250651dea45599d65d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-technical-deep-dive"></a>Authentification directe Azure Active Directory : immersion technique

>[!IMPORTANT]
>L’authentification directe Azure AD est actuellement en préversion. 

## <a name="how-does-azure-active-directory-pass-through-authentication-work"></a>Comment l’authentification directe Azure Active Directory fonctionne-t-elle ?

Lorsqu’un utilisateur tente de toosign dans une application sécurisée par Azure Active Directory (Azure AD) et si l’authentification pass-through est activée sur le client de hello, hello étapes suivantes se produisent :

1. utilisateur de Hello tente tooaccess une application (par exemple, hello Outlook Web App - https://outlook.office365.com/owa/).
2. Si l’utilisateur de hello n’est pas déjà inscrit, utilisateur de hello est redirigé toohello Azure AD-page de connexion.
3. utilisateur de Hello conclut leur nom d’utilisateur et un mot de passe hello Azure AD-page de connexion et clique sur le bouton « Connexion » de hello.
4. Azure AD, à la réception de demande de connexion hello, place le nom d’utilisateur hello et le mot de passe (chiffré à l’aide d’une clé publique) sur une file d’attente.
5. Un agent d’authentification directe local rend une file d’attente de toohello appel sortant et récupère le nom d’utilisateur hello et le mot de passe chiffré.
6. l’agent de Hello déchiffre un mot de passe hello à l’aide de sa clé privée.
7. l’agent de Hello valide alors le nom d’utilisateur hello et un mot de passe dans Active Directory à l’aide des API Windows standard (un toowhat mécanisme similaire est utilisé par Active Directory Federation Services). Hello nom d’utilisateur peut être un nom d’utilisateur de hello local par défaut (généralement `userPrincipalName`) ou un autre attribut configuré dans Azure AD Connect (appelé `Alternate ID`).
8. Hello contrôleur de domaine Active Directory (DC) local, puis évalue hello demande et renvoie hello réponse appropriée (succès, échec, mot de passe expiré ou utilisateur verrouillé) toohello agent.
9. l’agent Hello, retourne à son tour, cette tooAzure arrière de réponse AD.
10. Azure AD évalue la réponse de hello et répond utilisateur toohello selon le cas : par exemple, il connecte les utilisateur hello immédiatement ou demande de multi-Factor Authentication (MFA).
11. Si l’authentification utilisateur hello dans réussit, utilisateur de hello est application hello de tooaccess en mesure de.

Hello diagramme suivant illustre tous les composants de hello et étapes hello.

![Authentification directe](./media/active-directory-aadconnect-pass-through-authentication/pta2.png)

## <a name="next-steps"></a>Étapes suivantes
- [**Limitations actuelles**](active-directory-aadconnect-pass-through-authentication-current-limitations.md) : cette fonctionnalité est actuellement en préversion. Découvrez les scénarios pris en charge et ceux qui ne le sont pas.
- [**Démarrage rapide**](active-directory-aadconnect-pass-through-authentication-quick-start.md) : soyez opérationnel avec l’authentification directe Azure AD.
- [**Forum aux Questions** ](active-directory-aadconnect-pass-through-authentication-faq.md) -réponses elles sonttrop aux questions.
- [**Résoudre les problèmes** ](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -en savoir comment tooresolve commun problèmes avec la fonctionnalité de hello.
- [**Authentification unique transparente Azure AD**](active-directory-aadconnect-sso.md) : explorez en détail cette fonctionnalité complémentaire.
- [**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) : pour formuler des demandes de nouvelles fonctionnalités.
