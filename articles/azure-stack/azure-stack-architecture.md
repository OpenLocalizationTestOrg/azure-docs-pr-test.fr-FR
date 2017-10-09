---
title: "aaaMicrosoft architecture du Kit de développement de pile Azure | Documents Microsoft"
description: "Hello vue architecture du Kit de développement Microsoft Azure pile."
services: azure-stack
documentationcenter: 
author: heathl17
manager: byronr
editor: 
ms.assetid: a7e61ea4-be2f-4e55-9beb-7a079f348e05
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: helaw
ms.openlocfilehash: 32a19ced7ddd57b97ba796679c116132090402e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-stack-development-kit-architecture"></a>Architecture du Kit de développement Microsoft Azure Stack
Hello Kit de développement de pile Azure est un déploiement à un seul nœud de pile de Azure. Tous les composants de hello sont installés sur des machines virtuelles en cours d’exécution sur un ordinateur hôte unique. 

## <a name="logical-architecture-diagram"></a>Schéma de l’architecture logique
Hello diagramme suivant illustre architecture logique de hello du kit de développement Azure pile hello et ses composants.

![](media/azure-stack-architecture/image1.png)

## <a name="virtual-machine-roles"></a>Rôles de machine virtuelle
Hello kit de développement de pile de Azure offre des services à l’aide de hello suivant des ordinateurs virtuels sur l’ordinateur hôte de hello :

| Nom | Description |
| ----- | ----- |
| **AzS-ACS01** | Services de stockage Azure Stack.|
| **AzS-ADFS01** | Services de fédération Active Directory (ADFS).  |
| **AzS-BGPNAT01** | Routeur Edge et fournit des capacités NAT et VPN pour Azure Stack. |
| **AzS-CA01** | Services d’autorité de certification pour les services de rôle Azure Stack.|
| **AzS-DC01** | Services Active Directory, DNS et DHCP pour Microsoft Azure Stack.|
| **AzS-ERCS01** | Machine virtuelle la console de récupération d’urgence. |
| **AzS-GWY01** | Services de passerelle Edge, comme les connexions de site à site VPN pour les réseaux locataires.|
| **AzS-NC01** | Contrôleur réseau qui gère les services réseau Azure Stack.  |
| **AzS-SLB01** | Services multiplexeur d’équilibrage de charge dans Azure Stack pour les clients et les services d’infrastructure Azure Stack.  |
| **AzS-SQL01** | Magasin de données interne pour les rôles d’infrastructure Azure Stack.  |
| **AzS-WAS01** | Portail d’administration Azure Stack et services Azure Resource Manager.|
| **AzS-WASP01**| Portail utilisateur (locataire) Azure Stack et services Azure Resource Manager.|
| **AzS-XRP01** | Contrôleur de gestion d’infrastructure pour la pile Microsoft Azure, y compris les fournisseurs de ressources de calcul, réseau et stockage hello.|


## <a name="next-steps"></a>Étapes suivantes
[Déployer Azure Stack](azure-stack-deploy.md)

[Première tootry de scénarios](azure-stack-first-scenarios.md)

