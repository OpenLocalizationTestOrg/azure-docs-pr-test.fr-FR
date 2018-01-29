---
title: "Remplacer un composant matériel sur un nœud d’unité d’échelle Azure Stack | Microsoft Docs"
description: "Découvrez comment remplacer un composant matériel sur un système intégré Azure Stack."
services: azure-stack
documentationcenter: 
author: mattbriggs
manager: femila
editor: 
ms.assetid: c6e036bf-8c80-48b5-b2d2-aa7390c1b7c9
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/20/2017
ms.author: mabrigg
ms.openlocfilehash: 4937b7725c8f39314ccc41584a8646b7197f6bdf
ms.sourcegitcommit: 6fb44d6fbce161b26328f863479ef09c5303090f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/10/2018
---
# <a name="replace-a-hardware-component-on-an-azure-stack-scale-unit-node"></a>Remplacer un composant matériel sur un nœud d’unité d’échelle Azure Stack

*S’applique à : systèmes intégrés Azure Stack*

Cet article décrit le processus général de remplacement des composants matériels qui ne sont pas échangeables à chaud. Les étapes de remplacement réelles varient en fonction du revendeur de votre matériel OEM. Pour obtenir des instructions détaillées propres à votre système intégré Azure Stack, consultez la documentation FRU (Field Replaceable Unit) de votre fournisseur.

Les composants non échangeables à chaud sont les suivants :

- UC*
- Mémoire*
- Contrôleur de gestion de la carte mère/carte de base (BMC)/carte vidéo
- Contrôleur de disque/adaptateur ou carte de bus hôte (HBA)/fond de panier
- Carte réseau (NIC)
- Disque de système d’exploitation*
- Lecteurs de données (ne prenant pas en charge l’échange à chaud, tels que les cartes complémentaires PCI-e)*

*Ces composants peuvent éventuellement supporter un échange à chaud, mais cela dépend de la manière dont le fournisseur les implémente. Pour obtenir des instructions détaillées, consultez la documentation FRU de votre fournisseur OEM.

L’organigramme suivant illustre le processus FRU général de remplacement d’un composant matériel non échangeable à chaud.

![Organigramme montrant le flux de remplacement de composant](media/azure-stack-replace-component/replacecomponentflow.PNG)

*Cette action n’est peut-être pas requise. Elle dépend de l’état du matériel.

**Votre fournisseur de matériel OEM peut ou non échanger le composant et mettre à jour le microprogramme. Cela dépend de votre contrat de support technique.

## <a name="review-alert-information"></a>Examiner les informations sur l’alerte

Le système de contrôle de l’intégrité et de surveillance d’Azure Stack surveille l’intégrité des cartes réseau et des lecteurs de données contrôlés par les espaces de stockage direct. Il ne surveille pas d’autres composants matériels. Pour tous les autres composants matériels, des alertes sont générées dans la solution de surveillance du matériel spécifique du fournisseur, qui s’exécute sur l’hôte de cycle de vie du matériel.

## <a name="component-replacement-process"></a>Processus de remplacement de composant

Les étapes suivantes fournissent une vue d’ensemble du processus de remplacement de composant. Ne suivez pas ces étapes sans vous référer à la documentation FRU fournie par le fabricant OEM.

1. Utilisez l’action [Drainer](azure-stack-node-actions.md#scale-unit-node-actions) pour mettre le nœud d’unité d’échelle en mode maintenance. Cette action n’est peut-être pas requise. Elle dépend de l’état du matériel.

   > [!NOTE]
   > Dans tous les cas, un seul nœud peut être purgé et mis hors tension en même temps sans endommager l’espace de stockage direct S2D.

2. Une fois le nœud d’unité d’échelle en mode maintenance, utilisez l’action [Mettre hors tension](azure-stack-node-actions.md#scale-unit-node-actions). Cette action n’est peut-être pas requise. Elle dépend de l’état du matériel.
 
   > [!NOTE]
   > Dans le cas peu probable où la mise hors tension ne fonctionnerait pas, utilisez l’interface web du contrôleur de gestion de la carte de base (BMC).

3. Remplacez le composant matériel endommagé. Votre fournisseur de matériel OEM peut ou non échanger le composant. Cela dépend de votre contrat de support technique.  
4. Mettez à jour le microprogramme. Suivez le processus de mise à jour du microprogramme spécifique de votre fournisseur à l’aide de l’hôte de cycle de vie du matériel pour vous assurer que le niveau de microprogramme approuvé est appliqué au composant matériel remplacé. Votre fournisseur de matériel OEM peut ou non effectuer cette opération. Cela dépend de votre contrat de support technique.  
5. Utilisez l’action [Réparation](azure-stack-node-actions.md#scale-unit-node-actions) afin de ramener le nœud d’unité d’échelle dans l’unité d’échelle.
6. Utilisez le point de terminaison privilégié pour [vérifier l’état de réparation du disque virtuel](azure-stack-replace-disk.md#check-the-status-of-virtual-disk-repair). Avec de nouveaux lecteurs de données, une opération de réparation de stockage complète peut prendre plusieurs heures en fonction de la charge du système et de l’espace utilisé.
7. Une fois la réparation terminée, vérifiez que toutes les alertes actives ont été automatiquement fermées.

## <a name="next-steps"></a>étapes suivantes

- Pour plus d’informations sur le remplacement d’un disque physique échangeable à chaud, voir [Remplacer un disque](azure-stack-replace-disk.md).
- Pour plus d’informations sur le remplacement d’un nœud physique, voir [Remplacer un nœud d’unité d’échelle](azure-stack-replace-node.md).
- 
