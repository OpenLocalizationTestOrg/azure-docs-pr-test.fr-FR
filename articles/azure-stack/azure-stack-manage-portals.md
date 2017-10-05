---
title: Utilisation des portails administrateur et utilisateur dans Azure Stack | Microsoft Docs
description: "Découvrez les différences entre les portails administrateur et utilisateur dans Azure Stack."
services: azure-stack
documentationcenter: 
author: twooley
manager: byronr
editor: 
ms.assetid: 02c7ff03-874e-4951-b591-28166b7a7a79
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: twooley
ms.openlocfilehash: 066de8278d1ef4406cde837da4c7c65304854383
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="using-the-administrator-and-user-portals-in-azure-stack"></a>Utilisation des portails administrateur et utilisateur dans Azure Stack

Il existe deux portails dans Azure Stack : le portail administrateur et le portail utilisateur (également appelé portail du *locataire*). Les portails sont secondés par des instances distinctes d’Azure Resource Manager.

Le tableau suivant montre comment se connecter aux portails et aux points de terminaison Resource Manager dans un environnement du Kit de développement Azure Stack.

|  Portail | URL du portail | URL de point de terminaison Resource Manager |   
| -------- | ------------- | ------- |  
| Administrateur | https://adminportal.local.azurestack.external  | https://adminmanagement.local.azurestack.external  |  
| Utilisateur | https://portal.local.azurestack.external | https://management.local.azurestack.external  |
| | |

## <a name="the-administrator-portal"></a>Le portail administrateur

Le portail administrateur permet à un opérateur cloud effectuer des tâches d’administration et d’exploitation. Un opérateur cloud peut effectuer des opérations telles que :
* Surveiller l’intégrité et les alertes
* Gérer la capacité
* Renseigner la Place de Marché
* Créer des plans et des offres
* Créer des abonnements pour les locataires

Un opérateur cloud peut aussi créer des ressources telles que des machines virtuelles, des réseaux virtuels et des comptes de stockage.

 ![Le portail administrateur](media/azure-stack-manage-portals/image1.png)

 ## <a name="the-user-portal"></a>Le portail utilisateur

 Le portail utilisateur ne fournit pas d’accès aux fonctionnalités d’administration ou d’exploitation du portail administrateur. Dans ce portail, un utilisateur peut s’abonner à des offres publiques et utiliser les services qui sont mis à disposition par le biais de ces offres.

  ![Le portail utilisateur](media/azure-stack-manage-portals/image2.png)
 
 ## <a name="subscription-behavior"></a>Comportement de l’abonnement
 
 Vous devez bien comprendre les différences suivantes entre le comportement de l’abonnement dans les deux portails.

 Portail administrateur :
* Un seul abonnement est disponible dans le portail administrateur. Il s’agit de l’*Abonnement Fournisseur par défaut*. Vous ne pouvez pas ajouter d’autres abonnements pour une utilisation dans le portail administrateur.
* En tant qu’opérateur cloud, vous pouvez ajouter des abonnements pour vos utilisateurs (y compris vous-même) à partir du portail administrateur. Les utilisateurs (y compris vous-même) peuvent accéder à ces abonnements et les utiliser à partir du portail utilisateur.

  >[!NOTE]
  En raison de la séparation d’Azure Resource Manager, les abonnements ne traversent pas les portails. Par exemple, si vous-même (en tant qu’opérateur cloud) vous connectez au portail utilisateur, vous ne pouvez pas accéder à l’Abonnement Fournisseur par défaut. Ainsi, vous n’avez accès à aucune fonction d’administration. Vous pouvez créer des abonnements pour vous-même à partir d’offres publiques, mais vous êtes considéré comme un utilisateur de locataire.

Portail utilisateur :
* Dans le portail utilisateur, un compte peut avoir plusieurs abonnements.

  >[!NOTE]
  Dans l’environnement du Kit de développement, si un utilisateur du locataire appartient au même annuaire que l’opérateur cloud, rien ne l’empêche de se connecter au portail administrateur. Toutefois, il ne peut accéder à aucune fonction d’administration. En outre, il ne peut pas ajouter d’abonnements ni accéder à des offres qui lui sont mises à disposition dans le portail utilisateur.

## <a name="next-steps"></a>Étapes suivantes

[Se connecter à Azure Stack](azure-stack-connect-azure-stack.md)

[Gestion des régions dans Azure Stack](azure-stack-region-management.md)
