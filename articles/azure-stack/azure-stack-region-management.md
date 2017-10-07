---
title: gestion des aaaRegion dans la pile de Azure | Documents Microsoft
description: "Vue d’ensemble de la gestion des régions dans Azure Stack."
services: azure-stack
documentationcenter: 
author: efemmano
manager: dsavage
editor: 
ms.assetid: e94775d5-d473-4c03-9f4e-ae2eada67c6c
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: efemmano
ms.openlocfilehash: c20fed831267aaf0447925ac261d7ee3f235c96c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="region-management-in-azure-stack"></a>Gestion des régions dans Azure Stack
Pile Azure a un concept hello de régions, qui sont des entités logiques constituées des ressources matérielles hello qui composent hello Azure pile infrastructure. À l’intérieur de gestion de la région, vous pouvez rechercher toutes les ressources qui sont requis toosuccessfully fonctionnent infrastructure du cycle de vie Azure pile hello.

Bonjour Kit de développement de pile Azure est un déploiement à nœud unique et est égal à une région. Si vous configurez une autre instance de hello Kit de développement de pile Azure sur un ordinateur distinct, cette instance est une autre région.

## <a name="information-available-through-hello-region-management-tile"></a>Informations disponibles via la vignette de gestion de la région de hello
Pile Azure possède un ensemble de fonctionnalités de gestion de la région disponibles Bonjour **gestion de la région** vignette. Cette vignette est l’administrateur du cloud tooa disponible sur le tableau de bord hello par défaut dans le portail d’administration hello. Elle vous permet de surveiller et de mettre à jour votre région Azure Stack et ses composants, qui sont propres à la région.

 ![vignette de gestion de la région de Hello](media/azure-stack-manage-region/image1.png)

 Si vous cliquez sur une région de la vignette de gestion de la région de hello, vous pouvez accéder hello informations suivantes :

  ![Description des volets dans le panneau de gestion de la région de hello](media/azure-stack-manage-region/image2.png)

1. **menu de ressource Hello**. Ici, vous pouvez accéder à des zones de gestion de l’infrastructure spécifiques, ainsi qu’afficher et gérer des ressources locataire telles que des comptes de stockage et des réseaux virtuels.

2. **Alertes**. Cette vignette répertorie les alertes à l’échelle du système et fournit des détails sur chacune de ces alertes.

3. **Mises à jour**. Dans cette vignette, vous pouvez afficher la version actuelle de hello de votre infrastructure de la pile de Azure.

4. **Fournisseurs de ressources**. Fournisseurs de ressources est hello place toomanage hello client les fonctionnalités offertes par hello composants toorun requis Azure pile. Chaque fournisseur de ressources est fourni avec une expérience d’administration. Cette expérience peut inclure des alertes pour un fournisseur spécifique de hello, métriques et autre fournisseur de ressources de gestion des capacités toohello spécifique.
 
5. **Rôles d’infrastructure**. Rôles d’infrastructure sont hello composants toorun nécessaire Azure pile. Rôles d’infrastructure hello uniquement qui signalent des alertes sont répertoriées. En cliquant sur un rôle, vous pouvez afficher les alertes de hello associés de rôle spécifique de hello et instances de rôle hello où ce rôle est en cours d’exécution. Bien que hello fonctionnalité toostart, redémarrer, ou arrêter une instance de rôle d’infrastructure, procédez comme **pas** cela dans un environnement de kit de développement. Ces options sont conçues uniquement pour un environnement à plusieurs nœuds, où il existe plusieurs instances de rôle par rôle d’infrastructure. Le redémarrage d’une instance de rôle (notamment AzS Xrp01) dans le kit de développement hello provoque l’instabilité du système.

## <a name="next-steps"></a>Étapes suivantes
[Surveiller l’intégrité et les alertes dans Azure Stack](azure-stack-monitor-health.md)

[Gérer les mises à jour dans Azure Stack](azure-stack-updates.md)






