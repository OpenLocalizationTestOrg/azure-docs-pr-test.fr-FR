---
title: "étape de l’intégration d’Azure AD avec les applications d’aaaGet | Documents Microsoft"
description: "Cet article est un guide de prise en main de l’intégration d’Azure Active Directory (AD) avec les applications locales et les applications cloud."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: db6d210d-c970-49e9-bd20-36d984bcd1c3
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: asteen
ms.openlocfilehash: 5a7a851e8418083fee72ab58477a9cab75d0d4bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="integrating-azure-active-directory-with-applications-getting-started-guide"></a>Guide de prise en main de l’intégration d’Azure Active Directory avec les applications
## <a name="overview"></a>Vue d'ensemble
Cette rubrique est prévue toogive vous une feuille de route pour l’intégration d’applications avec Azure Active Directory (AD). Chacune des sections hello ci-dessous contiennent un bref résumé d’une rubrique plus détaillée afin de pouvoir identifier les parties de ce guide de mise en route sont tooyou pertinentes.  Suivez les liens de hello pour un approfondissement sur chaque objet.

## <a name="before-you-begin-take-inventory"></a>Inventaire avant de commencer
Avant de vous lancer dans les applications toointegrating avec Azure AD, il est important tooknow où vous êtes et vous souhaitez toogo.  Hello aux questions suivantes sont prévue toohelp vous réfléchissez à votre projet intégration d’application Azure AD.

### <a name="application-inventory"></a>Inventaire des applications
* Où sont toutes vos applications ? Qui en sont les propriétaires ?
* Quel genre d’authentification vos applications nécessitent-elles ?
* Qui doit accéder aux applications de toowhich ?
* Voulez-vous toodeploy une application ?
  * Allez-vous la générer en interne et la déployer sur une instance de calcul Azure ?
  * Utiliserez-vous qui est disponible dans hello Galerie d’applications Azure ?

### <a name="user-and-group-inventory"></a>Inventaire des utilisateurs et des groupes
* Où vos comptes d’utilisateurs résident-ils ?
  * Active Directory local
  * Azure AD
  * Dans une base de données d’applications distincte que vous possédez
  * Dans des applications non approuvées
  * Tous les hello ci-dessus
* De quelles autorisations et affectations de rôle les utilisateurs individuels disposent-ils actuellement ? Devez-vous tooreview leur accès, ou êtes-vous sûr que vos assignations de rôle et les accès utilisateur sont appropriées maintenant ?
* Les groupes sont-ils déjà établis dans votre Active Directory local ?
  * Comment vos groupes sont-ils organisés ?
  * Qui sont membres du groupe hello ?
  * Quelles autorisations/attributions de groupes de hello actuellement disposent-elles ?
* Vous devez tooclean des bases de données utilisateur/groupe avant d’intégrer ?  (Cette question est très importante. Si les données sont inexactes, les résultats seront erronés.)

### <a name="access-management-inventory"></a>Inventaire de gestion de l’accès
* Comment gérer actuellement tooapplications des accès utilisateur ? Qui doit-elle toochange ?  Avez-vous autres façons toomanage accès, comme avec [RBAC](role-based-access-control-configure.md) par exemple ?
* Qui a besoin d’accès toowhat ?

Vous ne disposez peut-être tooall de réponses hello de ces questions au préalable, mais c’est OK.  Ce guide peut vous aider à répondre à certaines de ces questions et à prendre des décisions en connaissance de cause.

## <a name="prerequisites"></a>Composants requis
* Un abonnement Azure et un répertoire Azure Active Directory.  Si vous ne disposez pas d’un abonnement Azure, vous pouvez essayer Azure gratuitement pendant 30 jours. [Faites un essai.](https://azure.microsoft.com/trial/get-started-active-directory/)

## <a name="application-integration-with-azure-ad"></a>Intégration des applications avec Azure AD
### <a name="finding-unsanctioned-cloud-applications-with-cloud-app-discovery"></a>Détection des applications cloud non approuvées avec Cloud App Discovery
Comme mentionné ci-dessus, il existe peut-être des applications qui n’ont pas été gérées par votre entreprise jusqu’à présent.  Dans le cadre du processus d’inventaire hello, il est possible toofind non approuvée les applications cloud. Consultez [Détection des applications cloud non approuvées avec Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).

### <a name="authentication-types"></a>Types d’authentification
Chacune de vos applications peut présenter des exigences d’authentification différentes. Avec Azure AD, la signature de certificats peut être utilisée avec des applications qui utilisent les protocoles SAML 2.0, WS-Federation ou OpenID Connect, ainsi que l’authentification unique par mot de passe. Pour plus d’informations sur les types d’authentification aux applications à utiliser avec Azure AD, consultez [Gestion des certificats pour l’authentification unique fédérée sur Azure Active Directory](active-directory-sso-certs.md) et [Authentification unique par mot de passe](active-directory-appssoaccess-whatis.md).

### <a name="enabling-sso-with-azure-ad-app-proxy"></a>Activation de l’authentification unique avec le proxy d’application Azure AD
Proxy d’Application Microsoft Azure AD, vous pouvez fournir tooapplications accès situées en toute sécurité, à l’intérieur de votre réseau privé à partir de n’importe où et sur n’importe quel appareil. Après avoir installé un connecteur de proxy d'application dans votre environnement, il peut être facilement configuré avec Azure AD.

### <a name="integrating-applications-with-azure-ad"></a>Intégration des applications dans Azure AD
Hello articles suivants traitent hello différentes façons applications s’intègrent à Azure AD et fournissent des conseils.

* [Déterminer quels toouse Active Directory](active-directory-administer.md)
* [À l’aide d’applications dans la galerie d’applications Azure hello](active-directory-appssoaccess-whatis.md)
* [Liste de didacticiels sur l’intégration d’applications SaaS](active-directory-saas-tutorial-list.md)

## <a name="managing-access-tooapplications"></a>Gestion des accès tooapplications
Hello articles suivants décrivent les manières de gérer l’accès tooapplications une fois qu’ils ont été intégrées à Azure AD en utilisant des connecteurs d’Azure AD et Azure AD.

* [La gestion des accès tooapps à l’aide d’Azure AD](active-directory-managing-access-to-apps.md)
* [Automatisation avec les connecteurs Azure AD](active-directory-saas-app-provisioning.md)
* [Affectation d’utilisateurs tooan application](active-directory-applications-guiding-developers-assigning-users.md)
* [Affectation de groupes tooan application](active-directory-applications-guiding-developers-assigning-groups.md)
* [Partage de comptes](active-directory-sharing-accounts.md)

## <a name="integrating-custom-applications"></a>Intégration des applications personnalisées
Si vous écrivez une nouvelle application et que les développeurs de tooassist en tirant parti de l’alimentation hello Azure AD, consultez [aux développeurs de guidage](active-directory-applications-guiding-developers-for-lob-applications.md).

Si vous souhaitez tooadd votre application personnalisée de toohello Galerie d’applications Azure, consultez [« Apportez votre propre application », avec la configuration d’Azure AD libre-service SAML](http://blogs.technet.com/b/ad/archive/2015/06/17/bring-your-own-app-with-azure-ad-self-service-saml-configuration-gt-now-in-preview.aspx).

## <a name="see-also"></a>Voir aussi
* [Index d’articles pour la gestion des applications dans Azure Active Directory](active-directory-apps-index.md)

