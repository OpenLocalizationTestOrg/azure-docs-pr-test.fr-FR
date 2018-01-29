---
title: 'Azure AD Connect : authentification directe - Limitations actuelles | Microsoft Docs'
description: "Cet article décrit les limitations actuelles de l’authentification directe Azure Active Directory (Azure AD)"
services: active-directory
keywords: "Authentification directe Azure AD Connect, installation d’Active Directory, composants requis pour Azure AD, SSO, Authentification unique"
documentationcenter: 
author: swkrish
manager: mtillman
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2018
ms.author: billmath
ms.openlocfilehash: aee90f278476a899e0d47fc572c4f375bf926de2
ms.sourcegitcommit: 71fa59e97b01b65f25bcae318d834358fea5224a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/11/2018
---
# <a name="azure-active-directory-pass-through-authentication-current-limitations"></a>Authentification directe Azure Active Directory : limitations actuelles

>[!IMPORTANT]
>L’authentification directe Azure Active Directory (Azure AD) est une fonctionnalité gratuite que vous pouvez utiliser sans avoir besoin d’aucune édition payante d’Azure AD. L’authentification directe est disponible seulement dans l’instance mondiale d’Azure AD, et pas sur le [cloud Microsoft Azure Allemagne](http://www.microsoft.de/cloud-deutschland) ni sur le [cloud Microsoft Azure Government](https://azure.microsoft.com/features/gov/).

## <a name="supported-scenarios"></a>Scénarios pris en charge

Les scénarios suivants sont entièrement pris en charge :

- L’utilisateur se connecte dans toutes les applications basées sur un navigateur web
- L’utilisateur se connecte aux applications Office prenant en charge [l’authentification moderne](https://aka.ms/modernauthga) : Office 2016 et Office 2013 _avec_ authentification moderne
- L’utilisateur se connecte à Skype Entreprise, qui prend en charge l’authentification moderne, notamment les topologies Online et hybrides. Pour en savoir plus sur les topologies prises en charge, cliquez [ici](https://technet.microsoft.com/library/mt803262.aspx).
- Jonctions de domaine Azure AD pour les appareils Windows 10
- Prise en charge d’Exchange ActiveSync

## <a name="unsupported-scenarios"></a>Scénarios non pris en charge

Les scénarios suivants ne sont _pas_ pris en charge :

- L’utilisateur se connecte aux applications clientes Office héritées : Office 2010 et Office 2013 _sans_ authentification moderne. Nous recommandons aux entreprises de basculer si possible vers l’authentification moderne. L'authentification moderne permet la prise en charge de l'authentification directe. Elle vous aide à sécuriser vos comptes d'utilisateurs grâce à des fonctionnalités d'[accès conditionnel](../active-directory-conditional-access-azure-portal.md) comme Azure Multi-Factor Authentication.
- L’utilisateur se connecte à des applications clientes Skype Entreprise, _sans_ authentification moderne.
- L'utilisateur se connecte à PowerShell version 1.0. Nous vous recommandons d’utiliser PowerShell version 2.0.
- Mots de passe d'application pour l’authentification multifacteur.
- Détection des utilisateurs avec des [informations d’identification volées](../active-directory-reporting-risk-events.md#leaked-credentials).
- Azure AD Domain Services a besoin que la synchronisation du hachage de mot de passe soit activée sur le locataire. Ainsi, les locataires qui utilisent l’authentification directe _uniquement_ ne fonctionnent pas pour les scénarios qui ont besoin d’Azure AD Domain Services.
- L’authentification directe n’est pas intégrée à [Azure AD Connect Health](../connect-health/active-directory-aadconnect-health.md).
- Le programme Apple DEP ne prend pas en charge l’authentification moderne.  Les appareils Apple DEP ne pourront pas s’inscrire dans Intune pour les domaines utilisant l’authentification directe.

>[!IMPORTANT]
>Comme solution de contournement _uniquement_ pour les scénarios non pris en charge, activez la synchronisation du hachage de mot de passe dans la page [Fonctionnalités facultatives](active-directory-aadconnect-get-started-custom.md#optional-features) de l’Assistant Azure AD Connect.

>[!NOTE]
L’activation de la synchronisation de hachage de mot de passe vous donne la possibilité de basculer l’authentification en cas d’interruption de votre infrastructure sur site. Ce basculement de l’authentification directe vers la synchronisation de hachage de mot de passe Active Directory n’est pas automatique. Vous devrez basculer la méthode de connexion manuellement avec Azure AD Connect. Si le serveur exécutant Azure AD Connect tombe en panne, vous devrez demander de l’aide au Support Microsoft pour désactiver l’authentification directe.

## <a name="next-steps"></a>étapes suivantes
- [Démarrage rapide](active-directory-aadconnect-pass-through-authentication-quick-start.md) : soyez opérationnel avec l’authentification directe Azure AD.
- [Verrouillage intelligent](active-directory-aadconnect-pass-through-authentication-smart-lockout.md) : guide pratique pour configurer la fonctionnalité Verrouillage intelligent sur votre locataire pour protéger les comptes d’utilisateur.
- [Présentation technique approfondie](active-directory-aadconnect-pass-through-authentication-how-it-works.md) : découvrez comment fonctionne l'authentification directe.
- [Forum aux questions](active-directory-aadconnect-pass-through-authentication-faq.md) : trouvez des réponses aux questions fréquemment posées sur la fonctionnalité Authentification directe.
- [Résoudre les problèmes](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) : découvrez comment résoudre les problèmes courants liés à la fonctionnalité d’authentification directe.
- [Présentation approfondie de sécurité](active-directory-aadconnect-pass-through-authentication-security-deep-dive.md) : obtenez des informations techniques approfondies sur l’authentification directe.
- [Authentification unique transparente Azure AD](active-directory-aadconnect-sso.md) : explorez en détail cette fonctionnalité complémentaire.
- [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) : utilisez le Forum Azure Active Directory pour consigner de nouvelles demandes de fonctionnalités.

