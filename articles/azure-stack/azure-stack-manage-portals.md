---
title: aaaUsing hello administrateur et utilisateur les portails dans Azure pile | Documents Microsoft
description: "Découvrez les différences de hello entre les portails de hello administrateur et utilisateur dans la pile de Azure."
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
ms.openlocfilehash: 5e940749917e4aade26483a79bcc238346bf94f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-administrator-and-user-portals-in-azure-stack"></a>À l’aide des portails d’administrateur et utilisateur hello dans la pile de Azure

Il existe deux portails dans la pile de Azure ; Hello du portail de l’administrateur et le portail de l’utilisateur hello (également appelée tooas hello *client* portail). les portails Hello sont soutenues par des instances distinctes du Gestionnaire de ressources Azure.

tableau Hello suivant montre comment tooconnect toohello portails et des points de terminaison tooResource Manager dans un environnement du Kit de développement de pile Azure.

|  Portail | URL du portail | URL de point de terminaison Resource Manager |   
| -------- | ------------- | ------- |  
| Administrateur | https://adminportal.local.azurestack.external  | https://adminmanagement.local.azurestack.external  |  
| Utilisateur | https://portal.local.azurestack.external | https://management.local.azurestack.external  |
| | |

## <a name="hello-administrator-portal"></a>portail d’administration Hello

portail d’administration Hello permet à un cloud opérateur tooperform tâches d’administration et opérationnel. Un opérateur cloud peut effectuer des opérations telles que :
* Surveiller l’intégrité et les alertes
* Gérer la capacité
* remplir le marketplace de hello
* Créer des plans et des offres
* Créer des abonnements pour les locataires

Un opérateur cloud peut aussi créer des ressources telles que des machines virtuelles, des réseaux virtuels et des comptes de stockage.

 ![portail d’administration Hello](media/azure-stack-manage-portals/image1.png)

 ## <a name="hello-user-portal"></a>portail de l’utilisateur Hello

 portail de l’utilisateur Hello ne fournit pas de tooany accès hello administratifs ou opérationnels des fonctionnalités de portail d’administration hello. Dans le portail de l’utilisateur hello, un utilisateur peut s’abonner à des offres toopublic et utiliser les services hello qui sont rendues disponibles par le biais des offres.

  ![portail de l’utilisateur Hello](media/azure-stack-manage-portals/image2.png)
 
 ## <a name="subscription-behavior"></a>Comportement de l’abonnement
 
 Assurez-vous que vous comprenez hello suivant des différences entre le comportement de l’abonnement dans les portails de hello deux.

 Portail administrateur :
* Il n'existe qu’un seul abonnement qui est disponible dans le portail d’administration hello. Cet abonnement est hello *abonnement de fournisseur par défaut*. Impossible d’ajouter tous les abonnements pour une utilisation dans le portail d’administration hello.
* Comme un opérateur cloud, vous pouvez ajouter des abonnements pour vos utilisateurs (y compris vous-même) à partir du portail d’administration hello. Les utilisateurs (y compris vous-même) peuvent accéder et utiliser ces abonnements à partir du portail de l’utilisateur hello.

  >[!NOTE]
  En raison de hello séparation du Gestionnaire de ressources Azure, les abonnements ne traversent pas portails. Par exemple, si vous en tant qu’un opérateur cloud toohello portail de l’utilisateur se connecte, hello abonnement de fournisseur par défaut ne peut pas accéder à. Par conséquent, vous n’avez accès tooany les fonctions d’administration. Vous pouvez créer des abonnements pour vous-même à partir d’offres publiques, mais vous êtes considéré comme un utilisateur de locataire.

Portail utilisateur :
* Dans le portail de l’utilisateur hello, un compte peut avoir plusieurs abonnements.

  >[!NOTE]
  Dans l’environnement de kit développement hello, si un utilisateur du client appartient toohello même répertoire en tant qu’opérateur de cloud hello, ils ne sont pas bloqués à partir de la signature dans le portail d’administration toohello. Toutefois, ils ne peut pas accéder aux fonctions administratives de hello. En outre, ils ne peuvent pas ajouter des abonnements ou l’accès offres effectuées toothem disponible dans le portail de l’utilisateur hello.

## <a name="next-steps"></a>Étapes suivantes

[Se connecter tooAzure pile](azure-stack-connect-azure-stack.md)

[Gestion des régions dans Azure Stack](azure-stack-region-management.md)
