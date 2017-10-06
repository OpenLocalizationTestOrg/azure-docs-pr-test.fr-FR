---
title: "collaboration aaaB2B prétend mappage dans Azure Active Directory | Documents Microsoft"
description: "référence de mappage des revendications pour Azure Active Directory B2B Collaboration"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 03/15/2017
ms.author: sasubram
ms.openlocfilehash: 9e26085e91a6004b2f11286ae9c1df133bd47341
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="b2b-collaboration-user-claims-mapping-in-azure-active-directory"></a>Mappage des revendications d’utilisateur B2B Collaboration dans Azure Active Directory

Azure Active Directory (Azure AD) prend en charge la personnalisation des revendications hello émises dans un jeton SAML de hello pour les utilisateurs de collaboration B2B. Lorsqu’un utilisateur s’authentifie toohello application, Azure AD émet une application toohello jeton SAML qui contient des informations (ou les revendications) sur l’utilisateur hello qui identifie de façon unique les. Par défaut, cela inclut le nom d’utilisateur, adresse de messagerie, prénom et nom d’utilisateur hello. Vous pouvez afficher ou modifier des revendications hello envoyées Bonjour application de toohello jeton SAML sous l’onglet attributs de hello.

Il existe deux raisons pour lesquelles vous devrez peut-être les revendications de hello tooedit émises dans un jeton SAML de hello.

1. application Hello a été écrit toorequire une autre valeur de revendication URI ou des valeurs de revendication

2. Votre application nécessite toobe de revendication NameIdentifier hello autre chose qu’un nom principal d’utilisateur hello stockée dans Azure Active Directory.

  ![Afficher les revendications dans le jeton SAML](media/active-directory-b2b-claims-mapping/view-claims-in-saml-token.png)

Pour plus d’informations sur comment tooadd et modifier des revendications, consultez cet article sur la personnalisation des revendications, [personnalisation des revendications émises dans un jeton SAML de hello pour les applications pré-intégrées dans Azure Active Directory](develop/active-directory-saml-claims-customization.md). Pour les utilisateurs B2B Collaboration, le mappage entre locataires de NameID et UPN est empêché pour des raisons de sécurité.


## <a name="next-steps"></a>Étapes suivantes

Consultez les autres articles sur la collaboration B2B d'Azure AD :

* [Qu’est-ce qu’Azure AD B2B Collaboration ?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Propriétés de l’utilisateur B2B Collaboration](active-directory-b2b-user-properties.md)
* [Ajout d’un rôle tooa B2B collaboration](active-directory-b2b-add-guest-to-role.md)
* [Déléguer des invitations B2B Collaboration](active-directory-b2b-delegate-invitations.md)
* [Groupes dynamiques et B2B Collaboration](active-directory-b2b-dynamic-groups.md)
* [Code B2B Collaboration et exemples PowerShell](active-directory-b2b-code-samples.md)
* [Configurer des applications SaaS pour B2B Collaboration](active-directory-b2b-configure-saas-apps.md)
* [Partage externe d’Office 365](active-directory-b2b-o365-external-user.md)
* [Jetons utilisateur B2B Collaboration](active-directory-b2b-user-token.md)
* [Limitations actuelles de B2B Collaboration](active-directory-b2b-current-limitations.md)
