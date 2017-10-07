---
title: "aaaManage accès et des autorisations avec RBAC - Azure RBAC. | Documents Microsoft"
description: "Prise en main de la gestion de l’accès contrôle d’accès en fonction du rôle Azure Bonjour portail Azure. Utiliser les autorisations de tooassign affectations de rôle dans votre répertoire."
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: 8f8aadeb-45c9-4d0e-af87-f1f79373e039
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.openlocfilehash: 1c133b2b57b49d85f0e12a318c7997478e095fb9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-role-based-access-control-in-hello-azure-portal"></a>Prise en main le contrôle d’accès en fonction du rôle Bonjour portail Azure
Orientée sécurité doit se concentrent sur fournir aux employés les autorisations exactes hello que dont ils ont besoin. Trop d’autorisations peuvent exposer un tooattackers de compte. Si le nombre d’autorisations est trop faible, les employés ne peuvent pas effectuer leur travail efficacement. Le contrôle d’accès en fonction du rôle (RBAC) Azure permet de résoudre ce problème en offrant une gestion précise de l’accès pour Azure.

À l’aide de RBAC, vous pouvez séparer les droits au sein de votre équipe et accorder uniquement hello quantité toousers d’accès dont ils ont besoin tooperform leur travail. Plutôt que de donner à tous des autorisations illimitées au sein de votre abonnement ou de vos ressources Azure, vous pouvez autoriser uniquement certaines actions. Par exemple, un employé d’utiliser RBAC toolet gérer des ordinateurs virtuels dans un abonnement, tandis que l’autre peut gérer les bases de données SQL dans hello même abonnement.

## <a name="basics-of-access-management-in-azure"></a>Concepts de base de la gestion d’accès dans Azure
Chaque abonnement Azure est associé à un répertoire Azure Active Directory (AD). Les utilisateurs, des groupes et des applications à partir de ce répertoire peuvent gérer des ressources Bonjour abonnement Azure. Affecter ces droits d’accès à l’aide des API de gestion Azure hello portail Azure et les outils de ligne de commande Azure.

Accorder l’accès en assignant hello toousers du rôle RBAC appropriés, les groupes et les applications à une certaine étendue. Hello portée d’une attribution de rôle peut être un abonnement, un groupe de ressources ou une seule ressource. Un rôle attribué à une portée parent accorde également l’accès toohello les enfants qu’il contient. Par exemple, un utilisateur avec le groupe de ressources tooa accès peut gérer toutes les ressources de hello qu’elle contient, comme les sites Web, des ordinateurs virtuels et des sous-réseaux.

![Relation entre les éléments d’Azure Active Directory - diagramme](./media/role-based-access-control-what-is/rbac_aad.png)

rôle RBAC Hello que vous attribuez détermine quels utilisateurs hello des ressources, le groupe ou l’application peut gérer dans cette étendue.

## <a name="built-in-roles"></a>Rôles intégrés
RBAC Azure a trois rôles de base qui s’appliquent à des types de ressources tooall :

* **Propriétaire** dispose des ressources de tooall un accès complet, y compris hello toodelegate droit accès tooothers.
* **Collaborateur** peut créer et gérer tous les types de ressources Azure, mais ne peut pas accorder l’accès tooothers.
* **Lecteur** peut consulter les ressources Azure existantes.

autres rôles RBAC hello dans Azure Hello autoriser la gestion de ressources Azure spécifiques. Par exemple, hello collaborateur d’un ordinateur virtuel permet hello utilisateur toocreate et gérer des ordinateurs virtuels. Il ne leur confère pas accéder au réseau virtuel de toohello ou sous-réseau hello hello machine virtuelle se connecte à. 

[Les rôles intégrés RBAC](role-based-access-built-in-roles.md) listes hello rôles disponibles dans Azure. Il spécifie les opérations hello et étendue que chaque rôle prédéfini accorde toousers. Si vous envisagez d’utiliser toodefine vos propres rôles pour encore plus de contrôle, consultez Comment toobuild [rôles personnalisés dans Azure RBAC](role-based-access-control-custom-roles.md).

## <a name="resource-hierarchy-and-access-inheritance"></a>Hiérarchie des ressources et héritage d’accès
* Chaque **abonnement** dans Azure appartient tooonly qu’un seul annuaire. (Mais chaque annuaire peut comporter plusieurs abonnements.)
* Chaque **groupe de ressources** appartient tooonly un seul abonnement.
* Chaque **ressource** appartient tooonly un groupe de ressources.

L’accès que vous accordez à des étendues parentes est hérité par les étendues enfant. Par exemple :

* Vous affectez hello lecteur rôle tooan Azure AD groupe à étendue de l’abonnement hello. membres de Hello de ce groupe peuvent afficher des chaque groupe de ressources et les ressources dans l’abonnement de hello.
* Vous attribuez hello contributeur rôle tooan application au niveau de l’étendue de groupe de ressources hello. Il peut gérer les ressources de tous les types dans ce groupe de ressources, mais pas autres groupes de ressources dans l’abonnement de hello.

## <a name="azure-rbac-vs-classic-subscription-administrators"></a>Comparaison entre RBAC Azure et Administrateur d’abonnement classiques
Administrateurs des abonnements classique et coadministrateurs ont un accès complet toohello abonnement Azure. Ils peuvent gérer des ressources à l’aide de hello [portail Azure](https://portal.azure.com) avec l’API du Gestionnaire de ressources Azure ou hello [portail Azure classic](https://manage.windowsazure.com) et le modèle de déploiement classique Azure. Dans le modèle RBAC hello, administrateurs classiques sont rôle hello propriétaire à l’étendue de l’abonnement hello.

Uniquement hello portail Azure et hello nouvelle prise en charge Azure Resource Manager API Azure RBAC. Les utilisateurs et les applications qui sont affectées des rôles RBAC ne pouvez pas utiliser un portail de gestion classique hello et le modèle de déploiement classique Azure hello.

## <a name="authorization-for-management-vs-data-operations"></a>Autorisation pour les opérations de gestion et les opérations de données
Azure RBAC uniquement prend en charge les opérations de gestion de hello ressources Azure dans hello portail Azure et les API du Gestionnaire de ressources Azure. Il ne peut pas autoriser toutes les opérations au niveau des données pour les ressources Azure. Par exemple, vous pouvez autoriser une personne toomanage comptes de stockage, mais pas toohello BLOB ou les tables au sein d’un compte de stockage. De même, une base de données SQL peut être géré, mais pas hello tables qu’il contient.

## <a name="next-steps"></a>Étapes suivantes
* Prise en main [contrôle d’accès en fonction du rôle Bonjour Azure portal](role-based-access-control-configure.md).
* Consultez hello [rôles intégrés RBAC](role-based-access-built-in-roles.md)
* Définissez vos propres [rôles personnalisés dans Azure RBAC](role-based-access-control-custom-roles.md)
