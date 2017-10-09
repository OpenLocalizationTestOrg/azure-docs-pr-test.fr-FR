---
title: "groupes d’aaaUse tooresources d’accès toomanage dans Azure Active Directory | Documents Microsoft"
description: "Comment toouse des groupes dans l’utilisateur Azure Active Directory toomanage accéder tooon locaux et les applications cloud et les ressources."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 714120d0-cdf9-465d-afee-39bef591c6b3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 876a356c8095505432e9346721f35c7943819e9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-access-tooresources-with-azure-active-directory-groups"></a>Gérer les accès tooresources avec les groupes Azure Active Directory
Azure Active Directory (Azure AD) est une solution complète de gestion des identités et des accès qui fournit un ensemble robuste de fonctionnalités toomanage accès tooon local et les applications cloud et les ressources, y compris les services Microsoft online services tels qu’Office 365 et un monde des applications SaaS non-Microsoft. Cet article fournit une vue d’ensemble, mais si vous souhaitez toostart à l’aide d’Azure AD regroupe dès maintenant, suivez les instructions de hello dans [la gestion des groupes de sécurité dans Azure AD](active-directory-accessmanagement-manage-groups.md). Si vous souhaitez toosee comment vous pouvez utiliser PowerShell toomanage groupes dans Azure Active directory, vous pouvez en savoir plus en [applets de commande Azure Active Directory pour la gestion de groupe](active-directory-accessmanagement-groups-settings-v2-cmdlets.md).

> [!NOTE]
> toouse Azure Active Directory, vous devez un compte Azure. Si vous ne possédez pas encore un compte Azure, vous pouvez [vous inscrire pour en obtenir un gratuitement](https://azure.microsoft.com/pricing/free-trial/).
>
>

Dans Azure AD, une des principales fonctionnalités de hello est hello capacité toomanage accès tooresources. Ces ressources peuvent faire partie du répertoire hello, comme dans les cas de hello d’objets de toomanage autorisations via des rôles dans le répertoire de hello ou des ressources qui sont Active toohello externes, tels que les applications SaaS, les services Azure et les sites SharePoint ou sur site ressources. Il existe quatre méthodes qu'un utilisateur peut avoir accès aux droits tooa ressource :

1. Affectation directe

    Les utilisateurs peuvent être affectés directement tooa ressource propriétaire hello de cette ressource.
2. Appartenance au groupe

    Un groupe peut être affecté tooa ressource par le propriétaire de la ressource hello et en procédant ainsi, l’octroi de membres hello d’une ressource groupe accès toohello. L’appartenance au groupe de hello peut être géré par propriétaire hello du groupe de hello. En effet, les délégués de propriétaire de ressource hello hello autorisation tooassign utilisateurs tootheir toohello propriétaire de la ressource du groupe de hello.
3. Basée sur une règle

    propriétaire de la ressource Hello peut utiliser un tooexpress règle accès tooa ressource doivent être assignées à quels utilisateurs. Hello apparition de règle de hello dépend des attributs de hello utilisés dans cette règle et leurs valeurs pour des utilisateurs spécifiques, et en procédant ainsi, propriétaire de la ressource hello délègue efficacement hello toomanage droit accès tootheir ressource toohello source d’autorité pour hello attributs qui sont utilisés dans la règle de hello. propriétaire de la ressource Hello toujours gère règle hello elle-même et détermine les attributs et les valeurs de fournissent des ressources de tootheir accès.
4. Autorité externe

    ressources de tooa accès Hello est dérivé d’une source externe. par exemple, un groupe qui est synchronisé à partir d’une source de référence comme un répertoire local ou d’une application SaaS telles que de la journée de travail. propriétaire de la ressource Hello affecte la ressource de toohello accès hello groupe tooprovide, et une source externe hello gère les membres du groupe de hello hello.

   ![Présentation du diagramme de gestion des accès](./media/active-directory-access-management-groups/access-management-overview.png)

## <a name="watch-a-video-that-explains-access-management"></a>Regardez une vidéo qui explique la gestion des accès
Vous pouvez regarder une courte vidéo qui explique en détail ceci :

**AD Azure : Appartenance de toodynamic présentation des groupes**

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-AD--Introduction-to-Dynamic-Memberships-for-Groups/player]
>
>

## <a name="how-does-access-management-in-azure-active-directory-work"></a>Comment fonctionne la gestion des accès dans Azure Active Directory ?
Groupe de sécurité hello est hello center Hello solution de gestion des accès Azure AD. À l’aide d’un tooresources accès de sécurité groupe toomanage est un paradigme connu, permettant ainsi d’une ressource tooa de manière flexible et facile à comprendre tooprovide accès pour le groupe de hello prévu d’utilisateurs. propriétaire de la ressource Hello (ou administrateur hello du répertoire de hello) peut affecter un tooprovide groupe un certaines ressources de le toohello droit accès qu’ils possèdent. les membres du groupe de hello Hello seront fournies lors de l’accès hello et propriétaire de la ressource hello peut déléguer la liste des membres de hello hello toomanage droite d’une autre, par exemple un responsable ou un administrateur de support technique de toosomeone de groupe.

![Diagramme de gestion des accès Azure Active Directory](./media/active-directory-access-management-groups/active-directory-access-management-works.png)

propriétaire de Hello d’un groupe peut également rendre ce groupe disponibles pour les demandes du libre-service. De cette manière, un utilisateur final peut rechercher et trouver le groupe de hello et une demande toojoin, efficacement la recherche autorisation tooaccess hello ressources qui sont gérés via le groupe de hello. propriétaire de Hello du groupe de hello peut définir un groupe de hello afin que les demandes sont approuvées automatiquement ou doivent être approuvées par le propriétaire de hello du groupe de hello. Lorsqu’un utilisateur apporte une toojoin demande à un groupe, hello jointure est transférée toohello les propriétaires du groupe de hello. Si un des propriétaires de hello approuve la demande de hello, l’utilisateur demande hello est informé et utilisateur de hello est toohello joint à un groupe. Si un des propriétaires de hello refuse une demande de hello, l’utilisateur demande hello est notifié mais pas joints à un groupe de toohello.

## <a name="getting-started-with-access-management"></a>Prise en main de la gestion des accès
Prêt tooget démarré ? Vous devez essayer certaines des tâches de base hello que vous pouvez faire avec les groupes Azure AD. Utilisez ces tooprovide fonctionnalités spécialisées accéder toodifferent des groupes de personnes pour différentes ressources de votre organisation. Vous trouverez ci-dessous une liste des premières étapes à suivre.

* [Création d’une règle simple pour un groupe d’appartenance dynamique tooconfigure](active-directory-accessmanagement-manage-groups.md#how-can-i-manage-the-membership-of-a-group-dynamically)
* [À l’aide d’une application de groupe toomanage accès tooSaaS](active-directory-accessmanagement-group-saasapps.md)
* [Mise à disposition d’un groupe en libre-service pour l’utilisateur final](active-directory-accessmanagement-self-service-group-management.md)
* [La synchronisation d’un tooAzure du groupe local à l’aide d’Azure AD Connect](active-directory-aadconnect.md)
* [Gestion des propriétaires d’un groupe](active-directory-accessmanagement-managing-group-owners.md)

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez compris les principes fondamentaux de hello de gestion de l’accès, Voici certaines des fonctionnalités avancées supplémentaires disponibles dans Azure Active Directory pour la gestion des accès tooyour applications et ressources.

* [Utilisation d’attributs toocreate règles avancées](active-directory-accessmanagement-groups-with-advanced-rules.md)
* [Gestion des groupes de sécurité dans Azure AD](active-directory-accessmanagement-manage-groups.md)
* [Configuration de groupes dédiés dans Azure AD](active-directory-accessmanagement-dedicated-groups.md)
* [Référence de l’API Graph pour les groupes](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/groups-operations#GroupFunctions)
* [Configuration des paramètres de groupe avec les applets de commande Azure Active Directory](active-directory-accessmanagement-groups-settings-cmdlets.md)
