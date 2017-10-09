---
title: "aaaUnderstanding l’accès aux ressources dans Azure | Documents Microsoft"
description: "Cette rubrique explique les concepts sur l’utilisation d’accès aux ressources d’abonnement administrateurs toocontrol Bonjour complète du portail Azure"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
ms.assetid: 174f1706-b959-4230-9a75-bf651227ebf6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 06b9c4166bdea849faae67cae3146c6c278deb97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-resource-access-in-azure"></a>Présentation de l'accès aux ressources dans Azure
> [!IMPORTANT]
> Microsoft recommande de gérer Azure AD en utilisant hello [centre d’administration Azure AD](https://aad.portal.azure.com) Bonjour portail Azure au lieu d’utiliser hello portail Azure classic référencée dans cet article. Hello portail Azure fournit [contrôle d’accès basé sur le rôle](role-based-access-control-configure.md) afin de ressources Azure peuvent être gérés de manière plus précise.
> 
> 

En octobre 2013, hello portail Azure classic et les API de gestion de Service ont été intégrés avec Azure Active Directory dans le point de départ de commande toolay hello pour améliorer l’expérience utilisateur de hello pour la gestion des ressources de tooAzure d’accès. Azure Active Directory fournit déjà des fonctionnalités importantes telles que la gestion des utilisateurs, la synchronisation locale de répertoires, l'authentification multifacteur et le contrôle de l’accès aux applications. Naturellement, elles doivent également être mises à disposition pour la gestion générale des ressources Azure.

Le contrôle des accès dans Azure s’envisage d’abord dans une perspective de facturation. propriétaire Hello d’un compte Azure, accédé en visitant hello [centre des comptes Azure](https://account.windowsazure.com/subscriptions), est hello administrateur de compte. Les abonnements sont un conteneur pour la facturation, mais ils constituent également une limite de sécurité : chaque abonnement a un Service (administrateur) qui peut ajouter, supprimer et modifier des ressources Azure dans cet abonnement à l’aide de hello [portail Azure classic](https://manage.windowsazure.com/). SA valeur par défaut de Hello d’un nouvel abonnement est hello AA, mais hello AA peut modifier SA hello Bonjour centre des comptes Azure.

<br><br>![Comptes Azure][1]

Les abonnements sont également associés à un répertoire. répertoire de Hello définit un ensemble d’utilisateurs. Ceux-ci peuvent être des utilisateurs d’entreprise ou établissement scolaire ayant créé le répertoire de hello hello ou ils peuvent être des utilisateurs externes (autrement dit, Microsoft Accounts). Les abonnements sont accessibles par un sous-ensemble de ces utilisateurs d’annuaire qui ont été définis en tant que Service administrateur (SA) ou de Coadministrateur (CA) ; Bonjour seule exception est que, pour des raisons légales, Accounts Microsoft (anciennement Windows Live ID) peuvent être affectés comme administrateur de service ou autorité de certification sans être présents dans le répertoire de hello.

<br><br>![Contrôle des accès par rôle dans Azure][2]

Fonctionnalité dans hello portail Azure classic permet SAs qui sont signés à l’aide d’un répertoire de hello toochange Account Microsoft associé à un abonnement à l’aide de hello **modifier l’annuaire** commande hello **Abonnements** page **paramètres**. Notez que cette opération a des conséquences sur le contrôle d’accès hello de cet abonnement.

> [!NOTE]
> Hello **modifier l’annuaire** commande Bonjour Azure classic portail n’est pas disponible toousers qui se sont connectés à l’aide d’un travail compte ou scolaire, car ces comptes peuvent se connecter uniquement toohello toowhich de répertoire auquel ils appartiennent.
> 
> 

<br><br>![Flux de connexion utilisateur simple][3]

Dans un cas simple hello, une organisation (comme Contoso) s’applique la facturation et contrôle d’accès dans hello même ensemble d’abonnements. Répertoire de hello est toosubscriptions associées qui sont détenues par un seul compte Azure. Une connexion réussie toohello portail Azure classic, les utilisateurs voient deux collections de ressources (représentées en orange dans l’illustration précédente de hello) :

* Répertoires où leur compte d'utilisateur existe (source ou ajouté comme principal étranger). Notez que ce répertoire hello utilisé pour la connexion n’est pas pertinente toothis calcul, afin de vos répertoires soient toujours affichés quel que soit le duquel vous êtes connecté.
* Les ressources qui font partie d’abonnements associés au répertoire hello utilisé pour la connexion et qui hello utilisateur peut accéder (où ils sont administrateur de service ou autorité de certification).

<br><br>![Utilisateur avec plusieurs abonnements et répertoires][4]

Les utilisateurs avec les abonnements sur plusieurs répertoires ont hello capacité tooswitch hello contexte actuel de hello portail Azure classic à l’aide du filtre d’abonnement hello. Dans les coulisses hello, cela entraîne un répertoire différent de tooa de connexion distincte, mais cela est accompli en toute transparence à l’aide de l’authentification unique (SSO).

Les opérations telles que le déplacement de ressources entre des abonnements peuvent être plus difficiles en raison de cet affichage unique des répertoires des abonnements. transfert de ressource tooperform hello, il peut être nécessaire toofirst utiliser hello **modifier l’annuaire** commande sur la page des abonnements hello dans **paramètres** tooassociate hello abonnements toohello même répertoire .

## <a name="next-steps"></a>Étapes suivantes
* toolearn savoir plus sur les administrateurs de toochange pour un abonnement Azure, voir [comment tooadd ou modifier les rôles administrateur Azure](../billing/billing-add-change-azure-subscription-administrator.md)
* Pour plus d’informations sur la façon dont Azure Active Directory est lié tooyour abonnement Azure, consultez [les abonnements Azure sont associés à Azure Active Directory](active-directory-how-subscriptions-associated-directory.md)
* Pour plus d’informations sur la façon de rôles tooassign dans Azure AD, consultez [attribution de rôles d’administrateur dans Azure Active Directory](active-directory-assign-admin-roles.md)

<!--Image references-->
[1]: ./media/active-directory-understanding-resource-access/IC707931.png
[2]: ./media/active-directory-understanding-resource-access/IC707932.png
[3]: ./media/active-directory-understanding-resource-access/IC707933.png
[4]: ./media/active-directory-understanding-resource-access/IC707934.png
