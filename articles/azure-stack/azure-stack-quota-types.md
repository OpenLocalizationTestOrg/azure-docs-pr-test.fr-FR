---
title: "types d’aaaQuota dans la pile de Azure | Documents Microsoft"
description: "Passez en revue les types de quota différent de hello disponibles pour les services et ressources dans la pile de Azure."
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 8/23/2017
ms.author: erikje
ms.openlocfilehash: e05870603526a3e0e65d536cff98b9033524017d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="quota-types-in-azure-stack"></a>Types de quotas dans Azure Stack
[Quotas](azure-stack-plan-offer-quota-overview.md#plans) définir les limites de ressources pour un abonnement de l’utilisateur peut fournir ou consommer hello. Par exemple, un quota peut permettre un toocreate utilisateur des toofive machines virtuelles. Chaque ressource peut avoir ses propres types de quotas.

## <a name="compute-quota-types"></a>Types de quotas de capacité de traitement (compute)
| **Type** | **Valeur par défaut** | **Description** |
| --- | --- | --- |
| Nombre maximal de machines virtuelles |50 | nombre maximal de Hello d’ordinateurs virtuels qu’un abonnement peut créer à cet emplacement. |
| Nombre maximal de cœurs de machine virtuelle |100 | Hello nombre maximal de cœurs un abonnement peut créer à cet emplacement (par exemple, une machine virtuelle A3 a quatre cœurs). |
| Nombre maximal de groupes à haute disponibilité |10 | nombre maximal de Hello de haute disponibilité qui peuvent être créés à cet emplacement. |
| Nombre maximal de groupes de machines virtuelles identiques |100 | nombre maximal de Hello de machines virtuelles identiques qui peuvent être créés à cet emplacement. |

> [!NOTE]
> Les quotas de capacité de traitement (compute) ne sont pas appliqués dans cette version Technical Preview.
> 
> 

## <a name="storage-quota-types"></a>Types de quotas de stockage
| **Item** | **Valeur par défaut** | **Description** |
| --- | --- | --- |
| Capacité maximale (Go) |500 |Capacité de stockage totale qui peut être consommée par un abonnement à cet emplacement. |
| Nombre total de comptes de stockage |20 |nombre maximal de Hello de comptes de stockage qu’un abonnement peut créer à cet emplacement. |

## <a name="network-quota-types"></a>Types de quotas pour les réseaux
| **Item** | **Valeur par défaut** | **Description** |
| --- | --- | --- |
| Nombre maximal d’adresses IP publiques |50 |nombre maximal de Hello d’adresses IP qu’un abonnement peut créer à cet emplacement. |
| Nombre maximal de réseaux virtuels |50 |nombre maximal de Hello des réseaux virtuels un abonnement peut créer à cet emplacement. |
| Nombre maximal de passerelles de réseau virtuel |1 |nombre maximal de Hello de passerelles de réseau virtuel (passerelles VPN) un abonnement peut créer à cet emplacement. |
| Nombre maximal de connexions réseau |2 |nombre maximal de Hello des connexions réseau (point à point ou site à site) un abonnement peut créer pour toutes les passerelles de réseau virtuel dans cet emplacement. |
| Nombre maximal d’équilibreurs de charge |50 |nombre maximal de Hello des équilibrages de charge qu’un abonnement peut créer à cet emplacement. |
| Nombre max de cartes réseau |100 |nombre maximal de Hello des interfaces réseau qu’un abonnement peut créer à cet emplacement. |
| Nombre maximal de groupes de sécurité réseau |50 |nombre maximal de Hello des groupes de sécurité réseau qu’un abonnement peut créer à cet emplacement. |

## <a name="view-an-existing-quota"></a>Afficher un quota existant
1. Cliquez sur **Autres services** > **Fournisseurs de ressources**.
2. Sélectionnez service hello avec quota hello que vous souhaitez tooview.
3. Cliquez sur **Quotas**et quota hello sélectionnez souhaité tooview.

## <a name="next-steps"></a>Étapes suivantes
[Découvrez plus d’informations sur les plans, les offres et les quotas.](azure-stack-plan-offer-quota-overview.md)

[Créez des quotas lors de la création d’un plan.](azure-stack-create-plan.md)
