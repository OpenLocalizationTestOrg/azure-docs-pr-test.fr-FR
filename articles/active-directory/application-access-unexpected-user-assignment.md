---
title: aaaHow tooAssign utilisateurs tooapplications | Documents Microsoft
description: "Comprendre comment les utilisateurs sont affectées application tooan dans votre client"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 4df60c7d723140d0d1bbd6ba8b34aa4e762d1138
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooassign-users-tooapplications"></a>Comment tooassign utilisateurs tooapplications

Cet article vous a-t-il toounderstand comment les utilisateurs sont affectées application tooan dans votre client.

## <a name="how-do-users-get-assigned-tooan-application-in-azure-ad"></a>Comment les utilisateurs sont affectées application tooan dans Azure AD ?

Pour un utilisateur tooaccess une application, ils doivent d’abord être affectés tooit d’une certaine façon. L’attribution peut être effectuée par un administrateur, un délégué de l’entreprise ou parfois hello utilisateur eux-mêmes. Ci-dessous décrit les façons de hello tooapplications obtenir affecter des utilisateurs :

1.  Un administrateur [affecte un utilisateur](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) application toohello directement

2.  Un administrateur [affecte un groupe](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) cet utilisateur hello est un membre de l’application de toohello, y compris :

  * Un groupe synchronisé localement

  * Un groupe de sécurité statique créé dans le cloud de hello

  * A [groupe de sécurité dynamique](https://docs.microsoft.com/azure/active-directory/active-directory-groups-dynamic-membership-azure-portal) créé dans le cloud de hello

  * Un groupe Office 365 créé dans hello cloud

  * Hello [tous les utilisateurs](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-dedicated-groups) groupe

3.  Un administrateur Active [accès à l’Application libre-service](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) tooallow un tooadd utilisateur un à l’aide de l’application hello [volet d’accès Application](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **ajouter une application** fonctionnalité **sans l’approbation de l’entreprise**

4.  Un administrateur Active [accès libre-service à l’Application](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) tooallow un tooadd utilisateur un à l’aide de l’application hello [volet d’accès Application](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **ajouter une application** fonctionnalité mais uniquement w **préalable de rang à partir d’un ensemble sélectionné d’approbateurs de l’entreprise**

5.  Un administrateur Active [gestion de groupe libre-service](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) tooallow un toojoin utilisateur un groupe une application est trop**sans l’approbation de l’entreprise**

6.  Un administrateur Active [gestion de groupe libre-service](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) tooallow un toojoin utilisateur un groupe qui est assigné à une application de, mais uniquement **avec une approbation préalable à partir d’un ensemble sélectionné d’approbateurs de l’entreprise**

7.  Un administrateur affecte un licence tooa utilisateur directement une première application, comme [Microsoft Office 365](http://products.office.com/)

8.  Un administrateur affecte un groupe de tooa de licence qui hello utilisateur est un membre de la première application de partie tooa, comme [Microsoft Office 365](http://products.office.com/)

9.  Un [administrateur donne son consentement tooan application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) toobe utilisé par tous les utilisateurs et un utilisateur se connecte ensuite toohello application

10. Un utilisateur [donne son consentement tooan application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) eux-mêmes en vous connectant toohello application

## <a name="next-steps"></a>Étapes suivantes
[Gestion des applications avec Azure Active Directory](active-directory-enable-sso-scenario.md)
