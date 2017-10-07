---
title: aaaAzure les instructions de Machines virtuelles | Documents Microsoft
description: "En savoir plus sur hello clé conception et implémentation des recommandations pour le déploiement de machines virtuelles Windows dans Azure"
documentationcenter: 
services: virtual-machines-windows
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f932e65a-437b-48b0-8d70-f61ded8ce1c6
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.openlocfilehash: d2c8043cd5829b54a5d57e56533122e42021797d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machines-guidelines-for-windows"></a>Instructions relatives aux machines virtuelles pour Windows
[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

Cet article porte sur hello compréhension requis la planification des étapes de création et la gestion des machines virtuelles (VM) au sein de votre environnement Azure.

## <a name="implementation-guidelines-for-vms"></a>Instructions d’implémentation pour les machines virtuelles
Décisions :

* De combien de machines virtuelles avez-vous besoin pour les diverses couches d’application et les composants de votre infrastructure ?
* Les ressources processeur et mémoire chaque machine virtuelle a besoin, et quelles sont les exigences de stockage hello ?

Tâches :

* Définir les charges de travail hello pour votre hello de ressources d’application et hello que nécessitent des machines virtuelles.
* Aligner les demandes de ressources hello pour chaque machine virtuelle avec hello VM stockage et la taille du type approprié.
* Définir vos groupes de ressources pour les différents niveaux de hello et composants de votre infrastructure.
* Définissez votre convention de dénomination de machines virtuelles.
* Créer vos machines virtuelles à l’aide de hello Azure PowerShell, web de portail, ou avec des modèles de gestionnaire de ressources.

## <a name="virtual-machines"></a>Machines virtuelles
Une des ressources de principal de hello dans votre environnement Azure est susceptibles d’ordinateurs virtuels. C’est là que vous exécutez vos applications, bases de données, services d’authentification, etc.

Il est important de toounderstand hello [différentes tailles de machine virtuelle](sizes.md) toocorrectly taille de votre environnement en termes de performances et coût. Si vos machines virtuelles n’ont pas assez de cœurs de processeur ou de mémoire, les performances de votre application en sont affectées, quelle que soit la façon dont elle est conçue et développée. Hello de révision suggéré des charges de travail pour chaque série de machine virtuelle comme point de départ lorsque vous décidez quels toouse de machine virtuelle de taille pour chaque composant de votre infrastructure. Vous pouvez [modifier la taille d’une machine virtuelle hello](resize-vm.md) après le déploiement.

Le stockage joue un rôle clé dans les performances des machines virtuelles. Vous pouvez utiliser le stockage Standard, qui emploie des disques rotatifs ordinaires, ou le stockage Premium, pour les charges de travail gourmandes en E/S et des performances de pointe, qui utilise des disques SSD. Comme avec hello taille de machine virtuelle, des coûts support de stockage de considérations tooselecting hello. Vous pouvez lire hello [article de recommandations de stockage infrastructure](infrastructure-storage-solutions-guidelines.md) toounderstand comment toodesign approprié stockage pour optimiser les performances de vos machines virtuelles.

## <a name="resource-groups"></a>Groupes de ressources
Des composants comme les machines virtuelles sont regroupés logiquement pour faciliter la gestion et la maintenance à l’aide des [groupes de ressources Azure](../../azure-resource-manager/resource-group-overview.md). À l’aide de groupes de ressources, vous pouvez créer, gérer et surveiller toutes les ressources hello qui composent une application donnée. Vous pouvez également implémenter [contrôles d’accès en fonction du rôle](../../active-directory/role-based-access-control-what-is.md) tooothers d’accès toogrant dans votre équipe tooonly hello les ressources dont ils ont besoin. Prendre tooplan fois vos groupes de ressources et les attributions de rôles. Conception et implémentation des groupes de ressources est différentes approches tooactually, soyez sûr tooread hello [l’article instructions de groupes de ressources](infrastructure-resource-groups-guidelines.md) toounderstand toobuild comment mieux à vos machines virtuelles.

## <a name="templates"></a>Modèles
Vous pouvez créer des modèles, défini par les fichiers JSON déclaratives, toocreate vos machines virtuelles. Modèles en général également générer stockage de hello requis, mise en réseau, les interfaces réseau, l’adressage IP, etc., ainsi que les machines virtuelles hello elles-mêmes. Vous utilisez des environnements de cohérente et reproductible de toocreate de modèles de développement et test à des fins tooeasily répliquent les environnements de production et inversement. Vous pouvez en savoir plus sur [création et utilisation de modèles](../../azure-resource-manager/resource-group-overview.md#template-deployment) toounderstand comment vous pouvez les utiliser pour créer et déployer vos machines virtuelles.

## <a name="next-steps"></a>Étapes suivantes
[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-windows-infrastructure-guidelines-next-steps.md)]

