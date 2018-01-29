---
title: "Gérer les autorisations d’accès aux ressources par utilisateur dans Azure Stack (administrateur de service et locataire) | Microsoft Docs"
description: "En tant qu’administrateur de service ou locataire, découvrez comment gérer les autorisations de contrôle d’accès en fonction du rôle (RBAC)."
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
ms.date: 09/25/2017
ms.author: helaw
ms.openlocfilehash: 1e0ced4b2d65456034ba3f8543152702c089a0b0
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2017
---
# <a name="manage-role-based-access-control"></a>Gérer le contrôle d’accès en fonction du rôle

*S’applique à : systèmes intégrés Azure Stack et Kit de développement Azure Stack*

Un utilisateur Azure Stack peut être un lecteur, un propriétaire ou un collaborateur pour chaque instance d’un abonnement, d’un groupe de ressources ou d’un service. Par exemple, l’utilisateur A peut disposer des autorisations de lecteur sur l’abonnement 1, mais disposer des autorisations de propriétaire sur la machine virtuelle 7.

* Lecteur : l’utilisateur peut tout afficher, mais ne peut pas effectuer de modifications.
* Collaborateur : l’utilisateur peut tout gérer, sauf l’accès aux ressources.
* Propriétaire : l’utilisateur peut tout gérer, y compris l’accès aux ressources.

## <a name="set-access-permissions-for-a-user"></a>Définir des autorisations d’accès pour un utilisateur
1. Connectez-vous avec un compte disposant des autorisations de propriétaire sur la ressource que vous souhaitez gérer.
2. Dans le panneau de la ressource, cliquez sur l’icône **Accès** ![](media/azure-stack-manage-permissions/image1.png).
3. Dans le panneau **Utilisateurs**, cliquez sur **Rôles**.
4. Dans le panneau **Rôles**, cliquez sur **Ajouter** pour ajouter des autorisations pour l’utilisateur.

## <a name="next-steps"></a>Étapes suivantes


