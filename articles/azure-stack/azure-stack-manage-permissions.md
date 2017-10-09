---
title: "tooresources d’autorisations aaaManage par utilisateur dans la pile de Azure (administrateur de service et client) | Documents Microsoft"
description: Comme un client ou un administrateur de service, vous devez savoir comment les autorisations RBAC toomanage.
services: azure-stack
documentationcenter: 
author: Heathl17
manager: byronr
editor: 
ms.assetid: cccac19a-e1bf-4e36-8ac8-2228e8487646
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: helaw
ms.openlocfilehash: 461feab12a4cb8b9402c6c61b721371c50f60559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-role-based-access-control"></a>Gérer le contrôle d’accès en fonction du rôle
Un utilisateur Azure Stack peut être un lecteur, un propriétaire ou un collaborateur pour chaque instance d’un abonnement, d’un groupe de ressources ou d’un service. Par exemple, l’utilisateur A peut disposer des autorisations de lecture du tooSubscription 1, mais ont des autorisations de propriétaire tooVirtual 7 de l’ordinateur.

* Lecteur : l’utilisateur peut tout afficher, mais ne peut pas effectuer de modifications.
* Collaborateur : Utilisateur peut gérer tout sauf tooresources d’accès.
* Propriétaire : Utilisateur peut gérer tout, y compris les accès tooresources.

## <a name="set-access-permissions-for-a-user"></a>Définir des autorisations d’accès pour un utilisateur
1. Connectez-vous avec un compte qui dispose du propriétaire autorisations toohello ressource toomanage.
2. Dans le panneau hello pour la ressource de hello, cliquez sur hello **accès** icône ![](media/azure-stack-manage-permissions/image1.png).
3. Bonjour **utilisateurs** panneau, cliquez sur **rôles**.
4. Bonjour **rôles** panneau, cliquez sur **ajouter** tooadd les autorisations pour l’utilisateur de hello.

## <a name="next-steps"></a>Étapes suivantes
[Ajouter un locataire Azure Stack](azure-stack-add-new-user-aad.md)

