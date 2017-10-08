---
title: aaaOffice 365 partage externe et Azure Active Directory B2B collaboration | Documents Microsoft
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
ms.date: 05/24/2017
ms.author: sasubram
ms.openlocfilehash: 60452b27b328453eda729bd839c982b479cb6f1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="office-365-external-sharing-and-azure-active-directory-b2b-collaboration"></a>Partage externe dans Office 365 et Azure Active Directory B2B Collaboration

Externe partage dans Office 365 (OneDrive, SharePoint Online, groupes unifiés, etc.) et Azure Active Directory (Azure AD) B2B collaboration sont techniquement hello même chose. Partage toutes externes (à l’exception de OneDrive/SharePoint Online), y compris les invités dans les groupes Office 365, invitation de hello Azure AD B2B collaboration API est déjà utilisé pour le partage.

OneDrive/SharePoint Online possède un gestionnaire d’invitation distinct. La prise en charge par OneDrive/SharePoint Online du partage externe a démarré avant qu’Azure AD ne propose sa prise en charge. Au fil du temps, partage externe OneDrive/SharePoint Online a à recevoir plusieurs fonctionnalités et des millions d’utilisateurs qui utilisent hello produit dans-intégrée de modèle de partage. Cependant, il existe quelques différences subtiles entre le fonctionnement du partage externe OneDrive/SharePoint Online et le fonctionnement d’Azure AD B2B Collaboration :

- OneDrive/SharePoint Online ajoute active de toohello aux utilisateurs une fois que les utilisateurs ont échangé leur invitation. Par conséquent, avant de remboursement, vous ne voyez pas utilisateur hello dans le portail Azure AD. Si un autre site invite un utilisateur Bonjour pendant ce temps, une nouvelle invitation est générée. En revanche, lorsque vous utilisez Azure AD B2B Collaboration, les utilisateurs sont ajoutés immédiatement sur invitation afin qu’ils apparaissent partout.

- expérience de remboursement Hello dans OneDrive/SharePoint Online, différent de l’expérience hello dans Azure AD B2B collaboration. Une fois un utilisateur a utilisé une invitation, hello expériences similitude.

- Les utilisateurs invités par Azure AD B2B Collaboration peuvent être sélectionnés à partir des boîtes de dialogue de partage de OneDrive/SharePoint Online. Les utilisateurs invités par OneDrive/SharePoint Online apparaissent également dans Azure AD une fois qu’ils ont utilisé leur invitation.

- toomanage externe partage dans OneDrive/SharePoint Online avec Azure AD B2B collaboration, définissez hello OneDrive/SharePoint Online externe aussi un paramètre de partage**uniquement autoriser le partage avec des utilisateurs externes déjà dans le répertoire de hello**. Les utilisateurs peuvent accéder à des sites de tooexternally partagé et choix de collaborateurs externes qui hello admin a ajouté. Hello administrateur peut ajouter des collaborateurs externes de hello via hello invitation de collaboration B2B API.

![Hello externe partagent le même paramètre OneDrive/SharePoint Online](media/active-directory-b2b-o365-external-user/odsp-sharing-setting.png)

## <a name="next-steps"></a>Étapes suivantes

Consultez les autres articles sur la collaboration B2B d'Azure AD :

* [Qu’est-ce qu’Azure AD B2B Collaboration ?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Propriétés de l’utilisateur B2B Collaboration](active-directory-b2b-user-properties.md)
* [Ajout d’un rôle tooa B2B collaboration](active-directory-b2b-add-guest-to-role.md)
* [Déléguer des invitations B2B Collaboration](active-directory-b2b-delegate-invitations.md)
* [Groupes dynamiques et B2B Collaboration](active-directory-b2b-dynamic-groups.md)
* [Code B2B Collaboration et exemples PowerShell](active-directory-b2b-code-samples.md)
* [Configurer des applications SaaS pour B2B Collaboration](active-directory-b2b-configure-saas-apps.md)
* [Jetons utilisateur B2B Collaboration](active-directory-b2b-user-token.md)
* [Mappage des revendications utilisateur B2B Collaboration](active-directory-b2b-claims-mapping.md)
* [Limitations actuelles de B2B Collaboration](active-directory-b2b-current-limitations.md)
