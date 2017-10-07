---
title: "vue d’ensemble des Instances de conteneurs d’aaaAzure | Documentation Azure"
description: Comprendre Azure Container Instances
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: na
ms.topic: overview
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/20/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: c0662ede1260b15d9841bfc2c3c4cec4c30338d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-instances"></a>Azure Container Instances

Conteneurs devient rapidement toopackage de façon hello préféré, déployer et gérer des applications de cloud. Les Instances du conteneur Azure offre hello plus rapide et plus simple façon toorun un conteneur dans Azure, sans avoir à tooprovision toutes les machines virtuelles et sans avoir à tooadopt un service de niveau supérieur. 

Azure Container Instances est une excellente solution pour les scénarios qui peuvent fonctionner dans des conteneurs isolés, y compris les applications basiques, automatiser des tâches et créer des travaux. Pour les scénarios où vous devez disposer d’orchestration de conteneur, y compris de détection du service sur plusieurs conteneurs, la mise à l’échelle automatique et mises à niveau de l’application coordonnée, nous vous recommandons de hello [Service de conteneur Azure](https://docs.microsoft.com/azure/container-service/).

## <a name="fast-startup-times"></a>Temps de démarrage rapide

Le service Containers offre des avantages de démarrage conséquents sur les machines virtuelles. Avec les Instances du conteneur Azure, vous pouvez démarrer un conteneur dans Azure en quelques secondes sans hello besoin tooprovision et gérer des ordinateurs virtuels.

## <a name="hypervisor-level-security"></a>Sécurité au niveau de l’hyperviseur

D’un point de vue historique, les conteneurs ont offert l’isolation de dépendance d’application et la gouvernance des ressources, mais n’ont pas été considérés suffisamment renforcés pour une utilisation de plusieurs locataires hostile. Avec Azure Container Instances, votre application se retrouve aussi isolée dans un conteneur que dans une machine virtuelle.

## <a name="custom-sizes"></a>Tailles personnalisées

Les conteneurs sont généralement optimisé toorun seulement une application unique, mais besoins hello de ces applications peuvent varier considérablement. Avec Azure Container Instances, vous pouvez demander ce dont vous avez besoin en termes de mémoire et de noyaux processeur. Vous payez en fonction de ce que vous demandez, facturé par hello seconde, afin de pouvoir finement optimiser vos dépenses selon vos besoins.

## <a name="public-ip-connectivity"></a>Connectivité IP publique

Avec les Instances du conteneur Azure, vous pouvez exposer vos conteneurs directement toohello internet avec une adresse IP publique. Bonjour future, nous sera développez intégration tooinclude fonctionnalités réseau avec des réseaux virtuels, charge équilibrages et autres parties de hello infrastructure de mise en réseau Azure.

## <a name="persistent-storage"></a>Stockage persistant

tooretrieve et conserver l’état avec les Instances du conteneur Azure, nous proposons des partages de fichiers de montage direct d’Azure.

## <a name="linux-and-windows-containers"></a>Conteneurs Windows et Linux

Avec les Instances du conteneur Azure, vous pouvez planifier des fenêtres et les conteneurs Linux avec hello même API. Indiquent simplement le type de système d’exploitation de base hello et tout le reste est identique.

## <a name="co-scheduled-groups"></a>Groupes co-planifiés

Azure Container Instances prend en charge la planification de groupes de plusieurs conteneurs qui partagent un même hôte, réseau local, stockage et cycle de vie. Cela permet de vous toocombine votre application principale avec d’autres utilisateurs dans un rôle de prise en charge, tel que la journalisation.

## <a name="next-steps"></a>Étapes suivantes

Essayez de déployer un tooAzure conteneur avec une seule commande à l’aide de notre [guide de démarrage rapide](container-instances-quickstart.md).
