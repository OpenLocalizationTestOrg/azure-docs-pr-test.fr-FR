---
title: "aaaShare Azure portail tableaux de bord à l’aide de RBAC | Documents Microsoft"
description: "Cet article explique comment tooshare un tableau de bord dans hello portail Azure à l’aide du contrôle d’accès en fonction du rôle."
services: azure-portal
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 8908a6ce-ae0c-4f60-a0c9-b3acfe823365
ms.service: multiple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/01/2016
ms.author: tomfitz
ms.openlocfilehash: b12f9f8582596ee14aa8bfdfb4772cc139e3bf45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="share-azure-dashboards-by-using-role-based-access-control"></a>Partager des tableaux de bord Azure à l’aide du contrôle d’accès en fonction du rôle
Après avoir configuré un tableau de bord, vous pouvez le publier et le partager avec d’autres utilisateurs de votre organisation. Vous permettre d’autres tooview votre tableau de bord à l’aide d’Azure [Role-Based Access Control](../active-directory/role-based-access-control-configure.md). Vous affectez un utilisateur ou un groupe de rôle tooa d’utilisateurs, et ce rôle définit si les utilisateurs peuvent afficher ou modifier le tableau de bord publié hello. 

Tous les tableaux de bord publiés sont implémentés en tant que ressources Azure, ce qui signifie qu’ils constituent des éléments gérables dans votre abonnement et qu’ils sont contenus dans un groupe de ressources.  En termes de contrôle d’accès, les tableaux de bord sont traités de la même manière que les autres ressources, telles qu’une machine virtuelle ou un compte de stockage.

> [!TIP]
> Mosaïque individuelle sur le tableau de bord hello applique ses propres exigences de contrôle d’accès en fonction des ressources hello qu'elles s’affichent.  Par conséquent, vous pouvez concevoir un tableau de bord est partagé largement tout en protégeant les données hello sur les vignettes individuels.
> 
> 

## <a name="understanding-access-control-for-dashboards"></a>Présentation du contrôle d’accès relatif aux tableaux de bord
Avec les contrôle de l’accès en fonction du rôle (RBAC), vous pouvez attribuer tooroles les utilisateurs à trois différents niveaux de portée :

* abonnement
* resource group
* resource

vous attribuez des autorisations Hello sont héritées d’abonnement vers le bas toohello ressource. tableau de bord publié Hello est une ressource. Par conséquent, vous avez peut-être déjà tooroles utilisateurs affectés pour l’abonnement de hello qui fonctionnent également pour un tableau de bord publié hello. 

Voici un exemple.  Supposons que vous avez un abonnement Azure et de différents membres de votre équipe ont été affectés des rôles de hello de **propriétaire**, **collaborateur**, ou **lecteur** pour l’abonnement de hello. Les utilisateurs qui sont propriétaires ou collaborateurs sont en mesure de toolist, afficher, créer, modifier ou supprimer des tableaux de bord dans l’abonnement de hello.  Les utilisateurs qui sont des lecteurs sont en mesure de toolist et afficher des tableaux de bord, mais ne peut pas modifier ou les supprimer.  Les utilisateurs avec accès en lecture sont en mesure de toomake modifications locales tooa tableau de bord publié (telles que, lors du dépannage d’un problème), mais est toopublish n’a pas pu ces server toohello arrière de modifications.  Ils auront hello option toomake une copie privée d’un tableau de bord hello pour eux-mêmes

Toutefois, vous pouvez également affecter autorisations toohello ressource groupe qui contient plusieurs tableaux de bord ou tableau de bord tooan individuels. Par exemple, vous pouvez décider qu’un groupe d’utilisateurs doit-elle disposer d’autorisations limitées sur l’abonnement de hello mais supérieur accès tooa particulier du tableau de bord. Vous affectez ces rôle tooa d’utilisateurs pour ce tableau de bord. 

## <a name="publish-dashboard"></a>Publier un tableau de bord
Supposons que vous avez terminé de configurer un tableau de bord que vous souhaitez tooshare avec un groupe d’utilisateurs dans votre abonnement. étapes Hello ci-dessous représentent un groupe personnalisé appelé responsables du stockage, mais vous pouvez nommer votre groupe de ce que vous voulez. Pour plus d’informations sur la création d’un groupe Active Directory et l’ajout de groupe d’utilisateurs toothat, consultez [la gestion des groupes dans Azure Active Directory](../active-directory/active-directory-accessmanagement-manage-groups.md).

1. Dans le tableau de bord hello, sélectionnez **partage**.
   
     ![sélectionner Partager](./media/azure-portal-dashboard-share-access/select-share.png)
2. Avant d’attribuer l’accès, vous devez publier le tableau de bord hello. Par défaut, tableau de bord hello sera publiée tooa groupe de ressources nommé **tableaux de bord**. Sélectionnez **Publier**.
   
     ![Publier](./media/azure-portal-dashboard-share-access/publish.png)

Votre tableau de bord est à présent publié. Si les autorisations de hello héritées de l’abonnement de hello sont appropriées, il est inutile toodo rien de plus. Autres utilisateurs de votre organisation seront être en mesure de tooaccess et modifier le tableau de bord hello en fonction de leur rôle au niveau d’abonnement. Toutefois, pour ce didacticiel, nous allons assigner un groupe de rôle tooa d’utilisateurs pour ce tableau de bord.

## <a name="assign-access-tooa-dashboard"></a>Attribuer l’accès tooa tableau de bord
1. Après la publication de tableau de bord hello, sélectionnez **gérer les utilisateurs**.
   
     ![gérer des utilisateurs](./media/azure-portal-dashboard-share-access/manage-users.png)
2. Vous obtenez une liste d’utilisateurs existants déjà dotés d’un rôle pour ce tableau de bord. Votre liste d’utilisateurs existants sera différente de celle image hello ci-dessous. Très probablement, les attributions de hello sont héritées d’abonnement de hello. tooadd un nouvel utilisateur ou groupe, sélectionnez **ajouter**.
   
     ![ajouter un utilisateur](./media/azure-portal-dashboard-share-access/existing-users.png)
3. Sélectionnez rôle hello qui représente les autorisations hello toogrant voulue. Dans cet exemple, sélectionnez **Contributeur**.
   
     ![sélectionner un rôle](./media/azure-portal-dashboard-share-access/select-role.png)
4. Sélectionnez l’utilisateur de hello ou un groupe que vous souhaitez tooassign toohello rôle. Si vous ne voyez pas l’utilisateur de hello ou un groupe que vous recherchez dans la liste de hello, utilisez la zone de recherche hello. La liste des groupes disponibles dépendent des groupes hello que vous avez créé dans Active Directory.
   
     ![sélectionner un utilisateur](./media/azure-portal-dashboard-share-access/select-user.png) 
5. Lorsque vous avez terminé d’ajouter des utilisateurs ou des groupes, sélectionnez **OK**. 
6. nouvelle attribution de Hello est ajoutée toohello la liste des utilisateurs. Notez que son **Accès** présente la valeur **Affecté** plutôt que la valeur **Hérité**.
   
     ![rôles affectés](./media/azure-portal-dashboard-share-access/assigned-roles.png)

## <a name="next-steps"></a>Étapes suivantes
* Pour obtenir la liste des rôles, voir [RBAC : rôles intégrés](../active-directory/role-based-access-built-in-roles.md).
* toolearn sur la gestion des ressources, consultez [des ressources de gestion de Azure via le portail](resource-group-portal.md).

