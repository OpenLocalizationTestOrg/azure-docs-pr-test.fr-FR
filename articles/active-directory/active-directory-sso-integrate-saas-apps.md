---
title: "Intégrer l’authentification unique Azure Active Directory aux applications SaaS | Microsoft Docs"
description: "Activer l'authentification unique, l'approvisionnement de l'utilisateur et la gestion centralisée de l'accès aux applications SaaS dans Azure Active Directory Vue d’ensemble de l’intégration d’Azure Active Directory dans des applications SaaS."
services: active-directory
keywords: "intégrer Azure AD avec des applications SaaS"
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 53b9d341-d1fc-4bbb-ac7c-3f4c68fcf00a
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/17/2017
ms.author: curtand
ms.reviewer: aaronsm
ms.openlocfilehash: fc0d297598c334ca8f6f8a2bd3ae948c87956342
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="integrate-azure-active-directory-single-sign-on-with-saas-apps"></a>Intégrer l’authentification unique Azure Active Directory aux applications SaaS
> [!div class="op_single_selector"]
> * [Portail Azure](active-directory-enterprise-apps-manage-sso.md)
> * [Portail Azure Classic](active-directory-sso-integrate-saas-apps.md)
>
>

[!INCLUDE [active-directory-sso-use-case-intro](../../includes/active-directory-sso-use-case-intro.md)]

Pour commencer à configurer l’authentification unique pour une application que vous importez dans votre organisation, vous utiliserez un annuaire existant dans Azure Active Directory (Azure AD). Vous pouvez utiliser un annuaire Azure AD que vous obtenez via Microsoft Azure, Office 365 ou Windows Intune. Si vous avez deux ou plusieurs de ces éléments, consultez [Administration de votre annuaire Azure AD](active-directory-administer.md) afin de déterminer celui à utiliser.

> [!IMPORTANT]
> Microsoft recommande de gérer Azure AD à l’aide du [Centre d’administration Azure AD](https://aad.portal.azure.com) dans le portail Azure au lieu d’utiliser le portail Azure classique référencé dans cet article. Pour savoir comment attribuer des rôles d’administrateur dans le centre d’administration Azure AD, consultez la section [Attribution de rôles d’administrateur dans Azure Active Directory](active-directory-enterprise-apps-manage-sso.md).

## <a name="authentication"></a>Authentification
Pour les applications qui prennent en charge les protocoles SAML 2.0, WS-Federation ou OpenID Connect, Azure Active Directory utilise des certificats de signature afin d’établir des relations de confiance. Pour plus d'informations, consultez [Gestion des certificats pour l’authentification unique fédérée](active-directory-sso-certs.md).

Pour les applications qui prennent uniquement en charge l’authentification basée sur des formulaires HTML, Azure Active Directory utilise une technique appelée « password vaulting » (mise au coffre des mots de passe) pour établir des relations de confiance. Cela permet aux utilisateurs de votre organisation d’être automatiquement connectés à une application SaaS via Azure AD grâce aux informations de compte d’utilisateur de cette application SaaS. Azure AD recueille et stocke en toute sécurité les informations du compte d’utilisateur et le mot de passe qui y est associé. Pour plus d'informations, consultez [Authentification unique par mot de passe](active-directory-appssoaccess-whatis.md#password-based-single-sign-on).

## <a name="authorization"></a>Autorisation
Un compte approvisionné est ce qui permet à un utilisateur d’être autorisé à utiliser une application, une fois qu’il est authentifié via l’authentification unique. L’approvisionnement de l'utilisateur peut s’effectuer manuellement, ou dans certains cas, vous pouvez ajouter et supprimer des informations sur l’utilisateur de l'application SaaS en fonction des modifications apportées dans Azure Active Directory. Pour plus d'informations sur l'utilisation de connecteurs Azure AD existants afin d’effectuer un approvisionnement automatisé, consultez [Automatisation de l’approvisionnement et de l’annulation de l’approvisionnement des utilisateurs pour les applications SaaS](active-directory-saas-app-provisioning.md).

Sinon, vous pouvez manuellement ajouter des informations sur l’utilisateur à une application, ou utiliser d'autres solutions d’approvisionnement disponibles sur Marketplace.

## <a name="access"></a>Access
Azure AD offre plusieurs moyens personnalisables pour déployer des applications pour les utilisateurs finaux de votre organisation. Vous n’êtes pas restreint par une solution d'accès ou de déploiement particulière. Vous pouvez utiliser [la solution qui répond le mieux à vos besoins](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users).

## <a name="additional-considerations-for-applications-already-in-use"></a>Considérations supplémentaires pour les applications déjà en cours d’utilisation
Configurer l’authentification unique pour une application que votre organisation utilise déjà est un processus différent de la création de comptes pour une nouvelle application. Il existe quelques étapes préliminaires, notamment : mapper les identités d’utilisateurs dans l’application à des identités Azure AD, et comprendre l’expérience de connexion des utilisateurs à une application après son intégration.

> [!NOTE]
> Afin de configurer l'authentification unique pour une application existante, vous devez disposer des droits d'administrateur global à la fois pour Azure AD et l'application SaaS.
>
>

### <a name="mapping-user-accounts"></a>Mappage de comptes d’utilisateurs
L’identité d’un utilisateur comporte généralement un identificateur unique qui peut être une adresse de messagerie ou un nom d’utilisateur principal. Vous devrez lier (mapper) l’identité d'application de chaque utilisateur à son identité Azure AD correspondante. Il existe deux façons de procéder selon les exigences d'authentification de votre application.

Pour plus d'informations sur le mappage d'identités d'application sur des identités Azure AD, consultez [Personnalisation des revendications émises dans le jeton SAML](http://social.technet.microsoft.com/wiki/contents/articles/31257.azure-active-directory-customizing-claims-issued-in-the-saml-token-for-pre-integrated-apps.aspx) et [Personnalisation des mappages d'attributs pour l'approvisionnement](active-directory-saas-customizing-attribute-mappings.md).

### <a name="understanding-the-users-log-in-experience"></a>Comprendre l’expérience de connexion de l'utilisateur
Lorsque vous intégrez l'authentification unique pour une application en cours d'utilisation, il est important de savoir que l'expérience utilisateur en sera affectée. Pour toutes les applications, les utilisateurs commenceront à se servir de leurs informations d'identification Azure AD pour se connecter. Il se peut également qu’ils doivent utiliser un autre portail pour accéder aux applications.

L'authentification unique pour certaines applications peut être effectuée sur l'interface de connexion de l'application. Mais, pour d’autres applications, l'utilisateur doit passer par un portail central (comme [Mes applications](http://myapps.microsoft.com) ou [Office 365](http://portal.office.com/myapps)) pour se connecter. Pour en savoir plus sur les différents types d'authentification unique et leurs expériences utilisateur, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).

En outre, la section *Suppression du consentement de l'utilisateur* de l’article [Guide pour les développeurs](active-directory-applications-guiding-developers-for-lob-applications.md) constitue une source d'informations précieuse.

## <a name="next-steps"></a>Étapes suivantes
Pour les applications SaaS figurant dans la galerie d’applications, Azure AD fournit un certain nombre de [didacticiels sur la manière d’intégrer des applications SaaS](active-directory-saas-tutorial-list.md).

Si l’application n’apparaît pas dans la galerie d’applications, vous pouvez [l’ajouter à la galerie d’applications Azure AD comme application personnalisée](http://blogs.technet.com/b/ad/archive/2015/06/17/bring-your-own-app-with-azure-ad-self-service-saml-configuration-gt-now-in-preview.aspx).

Vous trouverez des informations beaucoup plus détaillées sur tous ces problèmes dans la bibliothèque Azure.com, en commençant par [À quoi correspond l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).

Consultez aussi l’[Index d’articles pour la gestion des applications dans Azure Active Directory](active-directory-apps-index.md).
