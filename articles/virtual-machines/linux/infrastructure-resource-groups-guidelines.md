---
title: "groupes d’aaaResource pour les machines virtuelles Linux dans Azure | Documents Microsoft"
description: "Découvrez hello clé conception et implémentation des recommandations pour le déploiement des groupes de ressources dans les services d’infrastructure Azure."
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 93ab9d93-965a-46b9-9c87-a10d652a6422
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8809cb5eeb9a166d2bcf1946cd26b0ee748f8cd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-group-guidelines-for-linux-vms"></a>Instructions pour les groupes de ressources Azure pour les machines virtuelles Linux 

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

Cet article se concentre sur comment toologically élaborer votre environnement et tous les composants de hello dans les groupes de ressources de groupe.

## <a name="implementation-guidelines-for-resource-groups"></a>Instructions d’implémentation pour les groupes de ressources
Décisions :

* Vous allez toobuild des groupes de ressources par les composants d’infrastructure principaux hello, ou par le déploiement de l’application complète ?
* Avez-vous besoin de toorestrict accès tooResource regroupe à l’aide de contrôles d’accès en fonction du rôle ?

Tâches :

* Définissez les composants de l’infrastructure principale et les groupes de ressources dédiés dont vous avez besoin.
* Vérifier comment tooimplement les modèles de gestionnaire de ressources pour les déploiements cohérentes et reproductibles.
* Définir les rôles d’accès utilisateur vous avez besoin pour le contrôle des accès aux groupes de tooResource.
* Créer un jeu hello des groupes de ressources à l’aide de votre convention d’affectation de noms. Vous pouvez utiliser hello CLI d’Azure ou le portail.

## <a name="resource-groups"></a>Groupes de ressources
Dans Azure, vous logiquement regroupez des ressources connexes tels que les comptes de stockage, des réseaux virtuels et des machines virtuelles (VM) toodeploy, gérez et les gérer comme une seule entité. Cette approche rend plus facile toodeploy applications lors de conservation hello toutes les ressources entre eux à partir d’un point de vue gestion, ou toogrant d’autres groupe toothat d’accès aux ressources. Les noms des groupes de ressources peuvent avoir une longueur maximale de 90 caractères. Pour obtenir une compréhension plus complète des groupes de ressources, vous pouvez lire hello [vue d’ensemble du Gestionnaire de ressources Azure](../../azure-resource-manager/resource-group-overview.md).

Une fonctionnalité clé tooResource groupes est hello toobuild de capacité de votre environnement à l’aide d’un fichier JSON qui déclare le stockage hello, mise en réseau, et des ressources de calcul. Vous pouvez également définir des configurations tooapply ni les scripts personnalisés associés. Avec ces modèles JSON, vous créez des déploiements cohérents, reproductibles pour vos applications. Cette approche vous permet de créer un environnement de développement, puis utiliser ce même toocreate de modèle un déploiement de production, ou vice versa. Pour mieux comprendre l’utilisation des modèles, consultez [hello procédure pas à pas de modèle](../../azure-resource-manager/resource-manager-template-walkthrough.md) qui vous guide tout au long de chaque étape de la création d’un modèle JSON.

Il existe deux approches différentes, que vous pouvez suivre lors de la conception de votre environnement avec des groupes de ressources :

* Groupes de ressources pour chaque déploiement d’application qui combine des comptes de stockage hello, des réseaux virtuels et des sous-réseaux, les machines virtuelles, de charger équilibrages, etc..
* Des groupes de ressources centralisés qui contiennent votre réseau et vos sous-réseaux virtuels principaux ou vos comptes de stockage. Vos applications se trouvent alors dans leur propre groupe de ressources, qui contient uniquement les machines virtuelles, les équilibreurs de charge, les interfaces réseau, etc.

Comme vous montée en puissance parallèle, créer des groupes de ressources centralisée pour votre réseau virtuel et sous-réseaux rend plus facile toobuild intersite connexion réseau pour les options de connectivité hybride. Hello autre approche consiste, pour chaque application toohave, son propre réseau virtuel qui requiert une configuration et maintenance. [Contrôles d’accès en fonction du rôle](../../active-directory/role-based-access-control-what-is.md) fournissent un accès toocontrol de façon granulaire tooResource groupes. Pour les applications de production, vous pouvez contrôler les utilisateurs hello qui peuvent accéder à ces ressources, ou pour les ressources d’infrastructure hello core, vous pouvez limiter uniquement infrastructure ingénieurs toowork avec eux. Les propriétaires des applications ont uniquement accès aux composants de l’application toohello au sein de leur groupe de ressources et le pas les core hello infrastructure Azure de votre environnement. Lorsque vous concevez votre environnement, envisagez d’utilisateurs hello qui nécessitent des toohello d’accéder aux ressources et concevoir vos groupes de ressources en conséquence. 

## <a name="next-steps"></a>Étapes suivantes
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

