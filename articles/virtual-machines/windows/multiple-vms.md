---
title: aaaCreate plusieurs machines virtuelles | Documents Microsoft
description: "Options de création de plusieurs machines virtuelles sous Windows"
services: virtual-machines-windows
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: dfc1d1bb-a47d-4d7c-9fd2-f12050baacab
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/25/2016
ms.author: guybo
ms.openlocfilehash: 37729fabd91049744f6bd94c55221f5c1c65d527
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-multiple-azure-virtual-machines"></a>Création de plusieurs machines virtuelles Azure
Il existe plusieurs scénarios où vous devez toocreate un grand nombre de machines virtuelles similaires (VM). C’est le cas notamment pour le calcul hautes performances (HPC), l’analyse des données à grande échelle, les serveurs intermédiaires ou principaux évolutifs et souvent sans état (comme les serveurs Web) ainsi que les bases de données distribuées.

Cet article décrit hello options disponibles toocreate plusieurs machines virtuelles dans Azure. Ces options dépassent les cas simples hello où vous créez manuellement une série d’ordinateurs virtuels. toocreate de machines virtuelles, les processus hello que vous utilisez habituellement ne sont pas évolutifs bien si vous devez toocreate plus d’un certain nombre de machines virtuelles.

Toocreate une façon de machines virtuelles similaires est la construction de gestionnaire de ressources Azure hello toouse de *ressource boucles*.

## <a name="resource-loops"></a>boucles de ressources
Les boucles de ressources sont un raccourci syntaxique dans les modèles Azure Resource Manager. Elles peuvent créer un ensemble de ressources à la configuration similaire dans une boucle. Vous pouvez utiliser la ressource boucles toocreate plusieurs comptes de stockage, les interfaces réseau ou les machines virtuelles. Pour plus d’informations sur les boucles de ressources, consultez trop[créer des machines virtuelles dans des groupes à haute disponibilité à l’aide de la ressource boucles](https://azure.microsoft.com/documentation/templates/201-vm-copy-index-loops/).

## <a name="challenges-of-scale"></a>Les problèmes de la mise à l’échelle
Bien que les boucles de ressource rendent plus facile toobuild une infrastructure cloud à grande échelle et produisent des modèles plus concis, certains défis restent. Par exemple, si vous utilisez une ressource boucle toocreate 100 machines virtuelles, vous devez toocorrelate contrôleurs d’interface réseau (NIC) avec des machines virtuelles correspondants et les comptes de stockage. Nombre hello d’ordinateurs virtuels étant probablement toobe différent nombre hello de comptes de stockage, vous avez trop toodeal avec des tailles de boucle de ressources différent. Il s’agit des problèmes peut être résolus, mais augmente considérablement la complexité de hello avec montée en puissance.

La mise en place d’une infrastructure évolutive et souple est un autre problème. Vous pourriez par exemple, une infrastructure de mise à l’échelle automatiquement augmente ou diminue le nombre hello d’ordinateurs virtuels dans tooworkload de réponse. Machines virtuelles ne fournissent pas une toovary mécanisme intégré en nombre (montée en puissance parallèle et échelle). Si vous mettez à l’échelle en supprimant les machines virtuelles, il est difficile tooguarantee haute disponibilité en faisant en sorte que les machines virtuelles sont équilibrés entre les domaines de mise à jour et d’erreur.

Enfin, lorsque vous utilisez une boucle de ressource, plusieurs ressources de toocreate appels accédez infrastructure sous-jacente de toohello. Lorsque plusieurs appels de créent des ressources similaires, Azure a un tooimprove opportunité implicite lors de cette conception et optimiser les performances et la fiabilité du déploiement. C’est ici qu’interviennent les *jeux de mise à l’échelle de machine virtuelle* .

## <a name="virtual-machine-scale-sets"></a>Groupes identiques de machines virtuelles 
Machines virtuelles identiques sont une toodeploy de ressources de calcul Azure et de gérer un ensemble de machines virtuelles identiques. Avec toutes les machines virtuelles configurées hello même, jeux de mise à l’échelle de machine virtuelle est tooscale facile dans et montée en puissance parallèle. Vous modifiez simplement nombre hello d’ordinateurs virtuels dans le jeu de hello. Vous pouvez également configurer des ordinateurs virtuels échelle jeux tooautoscale basé sur les demandes de charge de travail hello hello.

Pour les applications qui ont besoin de ressources de calcul tooscale et de mise à l’échelle les opérations sont implicitement équilibrées entre domaines d’erreur et la mise à jour.

Au lieu d’effectuer la mise en corrélation de plusieurs ressources telles que des cartes réseau et des machines virtuelles, un jeu de mise à l’échelle comprend un réseau, un stockage, une machine virtuelle et des propriétés d’extension que vous pouvez configurer de manière centralisée.

Pour une échelle de tooVM introduction jeux, consultez toohello [échelle de machines virtuelles définit la page produit](https://azure.microsoft.com/services/virtual-machine-scale-sets/). Pour plus d’informations, consultez toohello [mise à l’échelle de machines virtuelles définit documentation](https://azure.microsoft.com/documentation/services/virtual-machine-scale-sets/).

