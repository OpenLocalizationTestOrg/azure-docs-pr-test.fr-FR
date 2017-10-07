---
title: "aaaIntegrate Azure Active Directory l’authentification unique avec des applications SaaS | Documents Microsoft"
description: "Activer l'authentification unique, l'approvisionnement de l'utilisateur et la gestion centralisée de l'accès aux applications SaaS dans Azure Active Directory Présentation du mode d’applications de tooSaaS toointegrate Azure Active Directory."
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
ms.openlocfilehash: fe621a30429c81c32470635d105ae3e95184efa1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-active-directory-single-sign-on-with-saas-apps"></a>Intégrer l’authentification unique Azure Active Directory aux applications SaaS
> [!div class="op_single_selector"]
> * [Portail Azure](active-directory-enterprise-apps-manage-sso.md)
> * [portail Azure Classic](active-directory-sso-integrate-saas-apps.md)
>
>

[!INCLUDE [active-directory-sso-use-case-intro](../../includes/active-directory-sso-use-case-intro.md)]

tooget démarré la configuration de l’authentification unique pour une application que vous importez dans votre organisation, vous utiliserez un répertoire existant dans Azure Active Directory (Azure AD). Vous pouvez utiliser un annuaire Azure AD que vous obtenez via Microsoft Azure, Office 365 ou Windows Intune. Si vous avez deux ou plusieurs de ces éléments, consultez [administrer votre annuaire Azure AD](active-directory-administer.md) toodetermine l’un toouse.

> [!IMPORTANT]
> Microsoft recommande de gérer Azure AD en utilisant hello [centre d’administration Azure AD](https://aad.portal.azure.com) Bonjour portail Azure au lieu d’utiliser hello portail Azure classic référencée dans cet article. Pour la tooassign les rôles d’administrateur dans Azure AD de hello admin center, consultez [attribution de rôles d’administrateur dans Azure Active Directory](active-directory-enterprise-apps-manage-sso.md).

## <a name="authentication"></a>Authentification
Pour les applications qui prennent en charge hello SAML 2.0, WS-Federation, ou protocoles OpenID Connect, utilise Azure Active Directory des relations d’approbation tooestablish certificats de signature. Pour plus d'informations, consultez [Gestion des certificats pour l’authentification unique fédérée](active-directory-sso-certs.md).

Pour les applications qui prennent en charge uniquement HTML basée sur les formulaires connectez-vous, Azure Active Directory utilise « stockage de mot de passe » tooestablish relations d’approbation. Cette hello permet aux utilisateurs de votre organisation de toobe automatiquement connecté tooa application SaaS par Azure AD à l’aide des informations de compte d’utilisateur hello de hello application SaaS. Azure AD recueille et stocke en toute sécurité les informations de compte d’utilisateur hello et le mot de passe associé hello. Pour plus d'informations, consultez [Authentification unique par mot de passe](active-directory-appssoaccess-whatis.md#password-based-single-sign-on).

## <a name="authorization"></a>Autorisation
Un compte configuré permet un toouse de toobe autorisé une application utilisateur une fois qu’ils ont authentifiés via l’authentification unique. Configuration de l’utilisateur peut s’effectuer manuellement, ou dans certains cas, vous pouvez ajouter et supprimer des informations sur l’utilisateur à partir de l’application SaaS de hello en fonction des modifications apportées dans Azure Active Directory. Pour plus d'informations sur l'utilisation de connecteurs Azure AD existants afin d’effectuer un approvisionnement automatisé, consultez [Automatisation de l’approvisionnement et de l’annulation de l’approvisionnement des utilisateurs pour les applications SaaS](active-directory-saas-app-provisioning.md).

Sinon, vous pouvez manuellement ajouter une application de tooan informations utilisateur, ou utiliser d’autres solutions de configuration qui sont disponibles dans le marketplace de hello.

## <a name="access"></a>Access
Azure AD fournit plusieurs façons personnalisables toodeploy applications tooend aux utilisateurs de votre organisation. Vous n’êtes pas restreint par une solution d'accès ou de déploiement particulière. Vous pouvez utiliser [hello solution qui convient le mieux à vos besoins](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users).

## <a name="additional-considerations-for-applications-already-in-use"></a>Considérations supplémentaires pour les applications déjà en cours d’utilisation
Configurez l’authentification unique sur pour votre organisation utilise déjà une application est un processus différent de processus hello de création de nouveaux comptes pour une nouvelle application. Il existe quelques étapes préliminaires, y compris : mappage des identités d’utilisateur dans les identités de tooAzure AD application hello et que vous comprenez la façon dont les utilisateurs bénéficient de journalisation dans tooan application une fois qu’il est intégré.

> [!NOTE]
> tooset l’authentification unique pour une application existante, vous avez besoin des droits d’administrateur global toohave dans les deux Azure AD et hello application SaaS.
>
>

### <a name="mapping-user-accounts"></a>Mappage de comptes d’utilisateurs
L’identité d’un utilisateur comporte généralement un identificateur unique qui peut être une adresse de messagerie ou un nom d’utilisateur principal. Vous devez toolink (map) chaque l’identité d’utilisateur application identité tootheir respectif Azure AD. Il existe deux façons tooaccomplish cela selon la manière dont exigence hello d’authentification de votre application.

Pour plus d’informations sur le mappage des identités d’application avec les identités Azure AD, consultez [personnalisation des revendications émises dans un jeton SAML de hello](http://social.technet.microsoft.com/wiki/contents/articles/31257.azure-active-directory-customizing-claims-issued-in-the-saml-token-for-pre-integrated-apps.aspx) et [personnalisation des mappages d’attributs pour la configuration](active-directory-saas-customizing-attribute-mappings.md).

### <a name="understanding-hello-users-log-in-experience"></a>Présentation de la connexion de l’utilisateur hello expérience
Lorsque vous intégrez l’authentification unique pour une application qui est déjà en cours d’utilisation, il est important de toorealize qui hello expérience utilisateur est affectée. Pour toutes les applications, les utilisateurs commencent à l’aide de leur toosign d’informations d’identification Azure AD dans. Il peut également être qu’ils doivent utiliser une application de hello tooaccess portail différents.

L’authentification unique pour certaines applications peut être effectuée sur la connexion de l’application hello dans l’interface, mais pour d’autres applications, hello utilisateur aura toogo via un portail central tel que ([mes applications](http://myapps.microsoft.com) ou [Office 365](http://portal.office.com/myapps)) toosign dans. En savoir plus sur hello différents types d’authentification unique et leurs expériences utilisateur [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

Une autre ressource utile est *suppression de consentement de l’utilisateur* Bonjour [aux développeurs de guidage](active-directory-applications-guiding-developers-for-lob-applications.md) l’article.

## <a name="next-steps"></a>Étapes suivantes
Pour les applications SaaS que vous trouvez dans la galerie d’applications de hello, Azure AD fournit un certain nombre de [didacticiels sur la façon des applications SaaS toointegrate](active-directory-saas-tutorial-list.md).

Si l’application n’est pas dans la galerie d’applications, vous pouvez [toohello Galerie d’applications Azure AD l’ajouter en tant qu’une application personnalisée](http://blogs.technet.com/b/ad/archive/2015/06/17/bring-your-own-app-with-azure-ad-self-service-saml-configuration-gt-now-in-preview.aspx).

Il est beaucoup plus de détails sur l’ensemble de ces problèmes dans la bibliothèque de Azure.com hello, commençant par [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).

En outre, ne pas manquer de hello [Index de l’Article pour la gestion des applications dans Azure Active Directory](active-directory-apps-index.md).
