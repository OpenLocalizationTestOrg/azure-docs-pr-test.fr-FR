---
title: "aaaSetting d’Azure Active Directory pour la gestion des accès libre-service application | Documents Microsoft"
description: "Gestion de groupes en libre-service permet aux utilisateurs toocreate et gérer des groupes de sécurité ou les groupes Office 365 dans Azure Active Directory et groupe de sécurité du hello possibilité toorequest offre aux utilisateurs ou les appartenances de groupe Office 365"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 904d5c70-c34a-46c4-a9a7-d1efecf4821c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/27/2017
ms.author: curtand
ms.reviewer: kairaz.contractor
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 2a73f4ed2532d41143fe5abe2fef1322d971a5c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-azure-active-directory-for-self-service-group-management"></a>Configuration d’Azure Active Directory pour la gestion de groupe en libre-service
Gestion de groupes en libre-service permet aux utilisateurs toocreate et gérer des groupes de sécurité ou les groupes Office 365 dans Azure Active Directory (Azure AD). Les utilisateurs peuvent demander également les appartenances aux groupes Office 365 ou du groupe de sécurité, et puis hello propriétaire du groupe de hello peut approuver ou refuser l’appartenance. De cette façon, contrôle quotidien de l’appartenance au groupe peut être déléguée toopeople qui comprennent le contexte professionnel hello de ce membre. Les fonctionnalités de gestion de groupes en libre-service ne sont disponibles que pour les groupes de sécurité et les groupes Office 365. Elles ne sont pas disponibles pour les groupes de sécurité activés pour la messagerie électronique ou les listes de distribution.

> [!IMPORTANT]
> Microsoft recommande de gérer Azure AD en utilisant hello [centre d’administration Azure AD](https://aad.portal.azure.com) Bonjour portail Azure au lieu d’utiliser hello portail Azure classic référencée dans cet article.

La gestion de groupes en libre-service se compose actuellement de deux scénarios essentiels : la gestion de groupes déléguée et la gestion de groupes en libre-service.

* **Gestion déléguée des groupes** un exemple est un administrateur qui gère l’application SaaS tooa accès à l’aide de la société de hello. La gestion de ces droits d’accès devenant fastidieuse, cet administrateur demande hello entreprise propriétaire toocreate un nouveau groupe. Hello administrateur octroie l’accès à un nouveau groupe de hello application toohello et ajoute toohello groupe tous les utilisateurs déjà accèdent actuellement toohello application. propriétaire de l’entreprise Hello peut ensuite ajouter des utilisateurs et les utilisateurs sont automatiquement approvisionnés toohello à l’application. propriétaire de l’entreprise Hello n’a pas besoin toowait hello toomanage d’accès d’administrateur pour les utilisateurs. Si l’administrateur de hello accorde hello même gestionnaire de tooa d’autorisation dans un groupe différent d’entreprise, puis cette personne peut également gérer les accès à leurs utilisateurs. Le propriétaire de l’entreprise hello ni le Gestionnaire de hello pour afficher ou gérer les utilisateurs de l’autre. administrateur de Hello pouvez toujours voir tous les utilisateurs qui ont accès toohello application et les droits d’accès de bloc si nécessaire.
* **Gestion de groupes en libre-service** Prenons l’exemple de deux utilisateurs disposant tous deux d’un site SharePoint Online. Ils les gèrent indépendamment. Ils veulent toogive chaque des autres équipes d’accéder à des sites tootheir. tooaccomplish, ils peuvent créer un groupe dans Azure AD et dans SharePoint Online, chacun d’eux sélectionne ce tootheir accès aux sites tooprovide de groupe.. Lorsqu’un utilisateur souhaite accéder, font la demande à partir de hello volet d’accès, et après l’approbation ils accèdent les sites SharePoint Online tooboth automatiquement. Une version ultérieure, un d’eux décide que toutes les personnes accédant à hello site doivent obtenir également application SaaS spécifique d’accès tooa. administrateur de Hello Hello application SaaS peut ajouter des droits d’accès pour le site SharePoint Online de hello application toohello. Dès lors, toutes les demandes approuvées donne accès toohello deux sites SharePoint Online et également toothis application SaaS.

## <a name="making-a-group-available-for-end-user-self-service"></a>Mise à disposition d’un groupe en libre-service pour l’utilisateur final
1. Bonjour [portail Azure classic](https://manage.windowsazure.com), ouvrez votre annuaire Azure AD.
2. Sur hello **configurer** onglet, définissez **gestion déléguée des groupes** tooEnabled.
3. Définissez **les utilisateurs peuvent créer des groupes de sécurité** ou **les utilisateurs peuvent créer des groupes Office** tooEnabled.

Lorsque **les utilisateurs peuvent créer des groupes de sécurité** est activé, tous les utilisateurs dans votre annuaire sont autorisés à toocreate des groupes de sécurité et ajouter des membres des groupes toothese. Ces nouveaux groupes apparaîtront également dans hello volet d’accès pour tous les autres utilisateurs. Si le paramètre de stratégie hello sur le groupe de hello le permet, les autres utilisateurs peuvent créer ces groupes toojoin des demandes. Si **Les utilisateurs peuvent créer des groupes de sécurité** est désactivé, les utilisateurs ne peuvent pas créer de groupes et ne peuvent pas modifier les groupes existants dont ils sont propriétaires. Cependant, ils peuvent toujours gérer les appartenances à ces groupes hello et approuver les demandes à partir d’autres utilisateurs de toojoin leurs groupes.

Vous pouvez également utiliser **les utilisateurs qui peuvent utiliser le libre-service pour les groupes de sécurité** tooachieve un contrôle d’accès plus fin sur la gestion des groupes en libre-service pour vos utilisateurs. Lorsque **les utilisateurs peuvent créer des groupes** est activé, tous les utilisateurs dans votre annuaire sont autorisés à toocreate nouveaux groupes et ajouter des membres des groupes toothese. En définissant **les utilisateurs qui peuvent utiliser le libre-service pour les groupes de sécurité** tooSome, vous pouvez réserver tooonly de gestion de groupe un groupe limité d’utilisateurs. Lorsque ce commutateur est tooSome, vous devez ajouter les utilisateurs toohello groupe SSGMSecurityGroupsUsers avant de pouvoir créer des groupes et ajouter des membres toothem. En définissant **les utilisateurs qui peuvent utiliser le libre-service pour les groupes de sécurité** tooAll, vous autorisez tous les utilisateurs de vos groupes de nouveau répertoire toocreate.

Vous pouvez également utiliser hello **groupe pouvant utiliser le libre-service pour les groupes de sécurité** zone toospecify un nom personnalisé pour un groupe dont les membres peuvent utiliser le libre-service.

## <a name="next-steps"></a>Étapes suivantes
Ces articles fournissent des informations supplémentaires sur Azure Active Directory.

* [La gestion des accès tooresources avec les groupes Azure Active Directory](active-directory-manage-groups.md)
* [Configuration des paramètres de groupe avec les applets de commande Azure Active Directory](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [Index d’articles pour la gestion des applications dans Azure Active Directory](active-directory-apps-index.md)
* [Qu’est-ce qu’Azure Active Directory ?](active-directory-whatis.md)
* [Intégration des identités locales dans Azure Active Directory](active-directory-aadconnect.md)
