---
title: "Aperçu de la gestion aaaAdministrative unités dans Azure Active Directory"
description: "Utilisation d'unités administratives pour une délégation plus précise des autorisations dans Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 8464cd6b-1d1a-470d-a4fb-ee29b8eab4c4
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/17/2017
ms.author: curtand
ms.reviewer: elkuzmen
ms.custom: oldportal;it-pro;
ms.openlocfilehash: ee2c7beb6f9f6292bbf3cdeab00801ac066ae0e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="administrative-units-management-in-azure-ad---public-preview"></a>Gestion des unités administratives dans Azure AD - version préliminaire publique
Cet article décrit les unités administratives, un nouveau conteneur Active Directory de Azure de ressources qui peuvent être utilisées pour déléguer des autorisations administratives à des sous-ensembles d’utilisateurs et le sous-ensemble de tooa appliquer les stratégies d’utilisateurs. Dans Azure Active Directory, les unités administratives permettent aux administrateurs d’administrateurs centraux toodelegate autorisations tooregional ou stratégie tooset à un niveau granulaire.

Cela est utile dans les organisations disposant de divisions indépendantes, par exemple, une grande université qui se compose de nombreuses écoles autonomes (école de commerce, école d’ingénieurs, etc.) qui sont indépendantes les unes des autres. Ces divisions comportent leurs propres administrateurs informatiques qui contrôlent les accès, gèrent les utilisateurs et définissent des stratégies pour leur département en particulier. Administrateurs centraux souhaitent grant en mesure de toobe ces autorisations des administrateurs de division sur utilisateurs hello de leur division. Plus spécifiquement, à l’aide de cet exemple, un administrateur central peut, par exemple, créer une unité administrative pour un établissement d’enseignement particulier (école de commerce) et remplir avec uniquement les utilisateurs hello Business school. Puis un administrateur central peut ajouter école de Commerce hello personnel tooa étendue de rôle, en d’autres termes, grant hello informatique Business school d’autorisations d’administration uniquement via l’unité administrative de hello entreprise scolaire.

> [!IMPORTANT]
> Vous ne pouvez assigner des rôles d’administrateur étendus de l’unité administrative que si vous activez Azure Active Directory Premium. Pour plus d'informations, consultez la section [Prise en main d’Azure AD Premium](active-directory-get-started-premium.md).
>


Du point de vue de l’administrateur central hello, une unité administrative est un objet d’annuaire qui peut être créé et rempli avec des ressources. **Dans cette version préliminaire, ces ressources peuvent être uniquement des utilisateurs.** Une fois créés et remplis, unité d’administration hello peut servir comme un Bonjour de toorestrict étendue autorisé uniquement sur les ressources contenues dans l’unité administrative de hello.

## <a name="managing-administrative-units"></a>Gestion des unités administratives
Dans cette version préliminaire, vous pouvez créer et gérer des unités administratives à l’aide des applets de commande hello Azure Module Active Directory pour Windows PowerShell. plus sur la façon de toolearn toodo qui, consultez [utilisation des unités administratives](https://docs.microsoft.com/powershell/azure/active-directory/working-with-administrative-units?view=azureadps-2.0)

Pour plus d’informations sur la configuration logicielle requise et le module de hello Azure AD lors de l’installation et pour plus d’informations sur hello applets de commande Module Azure AD pour la gestion des unités administratives, y compris la syntaxe, des descriptions de paramètres et des exemples, consultez [Azure Active Répertoire PowerShell](https://docs.microsoft.com/powershell/azure/active-directory/overview?view=azureadps-2.0).

## <a name="next-steps"></a>Étapes suivantes
[Éditions d’Azure Active Directory](active-directory-editions.md)
