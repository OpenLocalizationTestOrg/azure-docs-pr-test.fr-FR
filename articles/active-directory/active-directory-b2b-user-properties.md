---
title: "aaaProperties d’un utilisateur d’Azure Active Directory B2B collaboration | Documents Microsoft"
description: "Les propriétés de l’utilisateur Azure Active Directory B2B Collaboration sont configurables"
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
ms.date: 05/25/2017
ms.author: sasubram
ms.openlocfilehash: 78709f64430ed4c14eadf4dc257f175c24698c5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="properties-of-an-azure-active-directory-b2b-collaboration-user"></a>Propriétés d’un utilisateur Azure Active Directory B2B Collaboration

Un utilisateur Azure Active Directory (Azure AD) B2B (interentreprises) Collaboration présente la propriété UserType = Invité. En général, cet utilisateur invité est à partir d’une organisation partenaire et dispose de privilèges Bonjour invitation d’annuaire, par défaut limités.

En fonction de hello invitant les besoins de l’organisation, un utilisateur d’Azure AD B2B collaboration peut être dans un des hello suivant compte les États :

- État 1 : Hébergé dans une instance externe d’Azure AD et représentés sous la forme d’un utilisateur invité Bonjour invitation d’organisation. Dans ce cas, hello B2B utilisateur se connecte à l’aide d’un compte Azure AD auquel appartient le client de toohello invité. Si l’organisation partenaire de hello n’utilise pas Azure AD, hello invité utilisateur dans Azure AD est toujours créé. configuration requise de Hello est qu’ils échanger leur invitation et Azure AD vérifie leur adresse de messagerie. Dans ce cas, on parle également de location juste-à-temps (JIT) ou de location « virale ».

- État 2 : Hébergé dans un compte Microsoft et représentés sous la forme d’un utilisateur invité dans l’organisation d’hôte hello. Dans ce cas, hello invité utilisateur se connecte avec un compte Microsoft. Hello invité identité sociaux de l’utilisateur (google.com ou similaire), qui n’est pas un compte Microsoft, est créé en tant qu’un compte Microsoft au cours de l’échange de l’offre.

- État 3 : Hébergées dans Active Directory de l’organisation hello hôte local et synchronisé avec Azure l’organisation hello hôte AD. Au cours de cette version, vous devez utiliser PowerShell toomanually modification hello UserType de ces utilisateurs dans le cloud de hello.

- État 4 : Hébergé dans Azure l’organisation de l’hôte AD avec UserType = invité et les informations d’identification que hello hôte organisation gère.

  ![afficher les initiales d’inviter hello](media/active-directory-b2b-user-properties/redemption-diagram.png)


À présent, voyons à quoi ressemble un utilisateur Azure AD B2B Collaboration à l’état 1 dans Azure AD.

### <a name="before-invitation-redemption"></a>Avant l'utilisation de l'invitation

![Avant l’utilisation de l’offre](media/active-directory-b2b-user-properties/before-redemption.png)

### <a name="after-invitation-redemption"></a>Après l'utilisation de l'invitation

![Après l’utilisation de l’offre](media/active-directory-b2b-user-properties/after-redemption.png)

## <a name="key-properties-of-hello-azure-ad-b2b-collaboration-user"></a>Propriétés de clé de l’utilisateur de collaboration hello Azure AD B2B
### <a name="usertype"></a>UserType
Cette propriété indique la relation hello de location de hello utilisateur toohello hôte. Cette propriété peut avoir deux valeurs :
- Membres : Cette valeur indique un employé de l’organisation d’hôte hello et un utilisateur de salaires de l’organisation hello. Par exemple, cet utilisateur attend toohave accéder toointernal uniquement à des sites. Cet utilisateur ne peut pas être considéré comme collaborateur externe.

- Invité : Cette valeur indique un utilisateur qui n’est pas considérée comme entreprise toohello interne, par exemple un collaborateur externe, un partenaire, un client ou un utilisateur similaire. Un de ces utilisateurs ne pourraient être tooreceive attendu Mémo interne d’un directeur général ou bénéficiez des avantages de l’entreprise, par exemple.

  > [!NOTE]
  > Hello UserType n’a aucune relation toohow hello utilisateur s’inscrit dans, le rôle d’annuaire hello d’utilisateur de hello et ainsi de suite. Cette propriété indique l’organisation d’hôte de l’utilisateur hello relation toohello simplement et permet l’organisation de hello des stratégies de tooenforce qui dépendent de cette propriété.

### <a name="source"></a>Source
Cette propriété indique comment hello utilisateur se connecte.

- Utilisateur invité : cet utilisateur a été invité, mais n’a pas encore utilisé une invitation.

- Active Directory externe : L’utilisateur est hébergé dans une organisation externe et s’authentifie à l’aide d’un compte Azure AD appartenant à toohello autre organisation. Ce type de connexion correspond tooState 1.

- Compte Microsoft : cet utilisateur est hébergé dans un compte Microsoft et s’authentifie à l’aide d’un compte Microsoft. Ce type de connexion correspond tooState 2.

- Active Directory Windows Server : Cet utilisateur est connecté à partir d’Active Directory sur site qui appartient toothis organisation. Ce type de connexion correspond tooState 3.

- Azure Active Directory : Cet utilisateur s’authentifie à l’aide d’un compte Azure AD appartenant toothis organisation. Ce type de connexion correspond tooState 4.
  > [!NOTE]
  > Les propriétés Source et UserType sont indépendantes. Une valeur Source donnée n’implique pas une valeur UserType spécifique.

## <a name="can-azure-ad-b2b-users-be-added-as-members-instead-of-guests"></a>Des utilisateurs Azure AD B2B peuvent-ils être ajoutés en tant que membres plutôt qu’en tant qu’invités ?
En règle générale, un utilisateur Azure AD B2B et un utilisateur invité sont synonymes. Par conséquent, un utilisateur Azure AD B2B Collaboration est ajouté par défaut en tant qu’utilisateur avec la propriété UserType = Invité. Toutefois, dans certains cas, organisation du partenaire de hello est qu'un membre d’une plus grande toowhich hello hôte organisation appartient également. Dans ce cas, organisation d’hôte hello pourriez tootreat des utilisateurs dans l’organisation partenaire de hello en tant que membres au lieu d’invités. Utilisez hello Azure AD B2B Invitation Manager API tooadd ou inviter un utilisateur à partir de l’organisation hello partenaire organisation toohello hôte en tant que membre.

## <a name="filter-for-guest-users-in-hello-directory"></a>Filtre pour les utilisateurs invités dans le répertoire de hello

![Filtrer les utilisateurs invités](media/active-directory-b2b-user-properties/filter-guest-users.png)

## <a name="convert-usertype"></a>Convertir la propriété UserType
Actuellement, il est possible pour les utilisateurs tooconvert UserType de membre tooGuest et vice versa à l’aide de PowerShell. Toutefois, hello UserType propriété est prévu d’organisation de l’utilisateur toorepresent hello relation toohello. Par conséquent, valeur hello de cette propriété doit modifier que si la relation hello de l’organisation toohello hello utilisateur change. Si la relation hello d’utilisateur de hello change, doivent, comme si le nom d’hello utilisateur principal (UPN) doit changer, traités ? Utilisateur de hello poursuite toohave accès toohello ressources mêmes ? Une boîte aux lettres doit-elle être attribuée ? Par conséquent, nous déconseillons modification hello UserType à l’aide de PowerShell en tant qu’activité atomique. En outre, si cette propriété devient non modifiable par le biais de PowerShell, nous déconseillons l’utilisation d’une dépendance sur cette valeur.

## <a name="remove-guest-user-limitations"></a>Supprimer des limitations pour les utilisateurs invités
Il peut arriver où vous souhaitez toogive votre invité aux utilisateurs des privilèges plus élevés. Vous pouvez ajouter un rôle tooany d’utilisateur invité et même de supprimer restrictions de l’utilisateur invité par défaut hello dans hello directory toogive un Bonjour utilisateur mêmes privilèges en tant que membres.

Il est possible tooturn hors des limites d’utilisateur invité hello par défaut afin que l’utilisateur invité dans l’annuaire de l’entreprise hello bénéficie hello les mêmes autorisations que celles d’un utilisateur membre.

![Supprimer des limitations pour les utilisateurs invités](media/active-directory-b2b-user-properties/remove-guest-limitations.png)

## <a name="next-steps"></a>Étapes suivantes

Consultez les autres articles sur la collaboration B2B d'Azure AD :

* [Qu’est-ce qu’Azure AD B2B Collaboration ?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Ajout d’un rôle tooa B2B collaboration](active-directory-b2b-add-guest-to-role.md)
* [Déléguer des invitations B2B Collaboration](active-directory-b2b-delegate-invitations.md)
* [Audit et création de rapports relatifs à un utilisateur B2B Collaboration](active-directory-b2b-auditing-and-reporting.md)
* [Groupes dynamiques et B2B Collaboration](active-directory-b2b-dynamic-groups.md)
* [Code B2B Collaboration et exemples PowerShell](active-directory-b2b-code-samples.md)
* [Configurer des applications SaaS pour B2B Collaboration](active-directory-b2b-configure-saas-apps.md)
* [Jetons utilisateur B2B Collaboration](active-directory-b2b-user-token.md)
* [Mappage des revendications utilisateur B2B Collaboration](active-directory-b2b-claims-mapping.md)
* [Partage externe d’Office 365](active-directory-b2b-o365-external-user.md)
* [Limitations actuelles de B2B Collaboration](active-directory-b2b-current-limitations.md)
