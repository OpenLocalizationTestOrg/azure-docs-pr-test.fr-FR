---
title: Les quotas dans la pile Azure | Documents Microsoft
description: "Administrateurs de définir des quotas pour limiter la quantité maximale de ressources aux clients ayant accès à."
services: azure-stack
documentationcenter: 
author: mattmcg
manager: byronr
editor: 
ms.assetid: 955c6dd8-cefe-42f3-af88-e11d17d22725
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 3/1/2017
ms.author: mattmcg
ms.openlocfilehash: bbefca1a60f38f18838ee6563bd26b934cd02172
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="set-and-view-quotas-in-azure-stack"></a>Définir et afficher des quotas dans la pile de Azure
Quotas de définissent les limites de ressources pour un abonnement locataire peut fournir ou consommer. Par exemple, un quota peut permettre à un client créer jusqu'à cinq machines virtuelles. Pour ajouter un service à un plan, l’administrateur doit configurer les paramètres de quota pour ce service.

Les quotas sont configurables par service et par emplacement, permettant aux administrateurs de fournir un contrôle granulaire sur la consommation de ressources. Les administrateurs peuvent créer une ou plusieurs ressources de quota et les associer à des plans, ce qui signifie qu’ils puissent fournir des offres différenciés de leurs services. Quotas pour un service donné peuvent être créés à partir de la **fournisseur de ressources** panneau d’administration pour ce service.

Un locataire qui s’abonne à une offre qui contient plusieurs plans peut utiliser toutes les ressources qui sont disponibles dans chaque plan.

## <a name="to-create-an-iaas-quota"></a>Pour créer un quota IaaS
1. Dans un navigateur, accédez à [https://adminportal.local.azurestack.external](https://adminportal.local.azurestack.external/).
   
   Connectez-vous au portail Azure pile en tant qu’administrateur (en utilisant les informations d’identification que vous avez fourni au cours du déploiement).
2. Sélectionnez **nouveau**, puis **client offre + Plans**, puis sélectionnez **Quota**.
3. Sélectionnez le premier service pour lequel vous souhaitez créer un quota. Pour un quota IaaS, effectuez les étapes suivantes pour les services Calcul, Réseau et Stockage.
   Dans cet exemple, nous créons d’abord un quota pour le service Calcul. Dans le **Namespace** liste, sélectionnez le **Microsoft.Compute** espace de noms.
   
   > ![Création d’un nouveau quota de calcul](./media/azure-stack-setting-quota/NewComputeQuota.PNG)
   > 
   > 
4. Choisissez l’emplacement où le quota est défini (par exemple, « local »).
5. Sur le **des paramètres de Quota** de l’élément, intitulée **définir la capacité de Quota**. Cliquez sur cet élément pour configurer les paramètres de quota.
6. Sur le **définir les Quotas** panneau, vous voyez toutes les ressources de calcul pour laquelle vous pouvez configurer des limites. Chaque type a une valeur par défaut qui est associé. Vous pouvez modifier ces valeurs ou vous pouvez sélectionner le **Ok** situé en bas du panneau pour accepter les valeurs par défaut.
   
   > ![Définition d’un quota de calcul](./media/azure-stack-setting-quota/SetQuotasBladeCompute.PNG)
   > 
   > 
7. Une fois que vous avez configuré les valeurs et cliqué sur **Ok**, le **des paramètres de Quota** élément apparaît comme **configuré**. Cliquez sur **Ok** pour créer le **Quota** ressource.
   
   Vous devez voir une notification indiquant que la ressource de quota est créée.
8. Une fois que l’ensemble du quota a été créé avec succès, vous recevez une deuxième notification. Le quota de service de calcul est maintenant prêt à être associé à un plan. Répétez ces étapes avec les services de stockage et de réseau, et vous êtes prêt à créer un plan IaaS !
   
   > ![Notification en cas de réussite de la création du quota](./media/azure-stack-setting-quota/QuotaSuccess.png)
   > 
   > 

## <a name="compute-quota-types"></a>Types de quotas de capacité de traitement (compute)
| **Type** | **Valeur par défaut** | **Description** |
| --- | --- | --- |
| Nombre maximal de machines virtuelles |50 |Nombre maximal de machines virtuelles qu’un abonnement peut créer à cet emplacement. |
| Nombre maximal de cœurs de machine virtuelle |100 |Nombre maximal de cœurs qu’un abonnement peut créer à cet emplacement (par exemple, une machine virtuelle A3 a quatre cœurs). |
| Quantité maximale de mémoire de l’ordinateur virtuel (en Go) |150 |La quantité maximale de mémoire vive qui peut être configuré en mégaoctets (par exemple, une machine virtuelle A1 consomme 1,75 Go de RAM). |

> [!NOTE]
> Les quotas de capacité de traitement (compute) ne sont pas appliqués dans cette version Technical Preview.
> 
> 

## <a name="storage-quota-types"></a>Types de quotas de stockage
| **Item** | **Valeur par défaut** | **Description** |
| --- | --- | --- |
| Capacité maximale (Go) |500 |Capacité de stockage totale qui peut être consommée par un abonnement à cet emplacement. |
| Nombre total de comptes de stockage |20 |Nombre maximal de comptes de stockage qu’un abonnement peut créer à cet emplacement. |

## <a name="network-quota-types"></a>Types de quotas pour les réseaux
| **Item** | **Valeur par défaut** | **Description** |
| --- | --- | --- |
| Nombre maximal d’adresses IP publiques |50 |Nombre maximal d’adresses IP publiques qu’un abonnement peut créer à cet emplacement. |
| Nombre maximal de réseaux virtuels |50 |Nombre maximal de réseaux virtuels qu’un abonnement peut créer à cet emplacement. |
| Nombre maximal de passerelles de réseau virtuel |1 |Nombre maximal de passerelles de réseau virtuel qu’un abonnement peut créer à cet emplacement. |
| Nombre maximal de connexions réseau |2 |Nombre maximal de connexions réseau (point à point ou site à site) qu’un abonnement peut créer pour toutes les passerelles de réseau virtuel à cet emplacement. |
| Nombre maximal d’équilibreurs de charge |50 |Nombre maximal d’équilibreurs de charge qu’un abonnement peut créer à cet emplacement. |
| Nombre max de cartes réseau |100 |Nombre maximal d’interfaces réseau qu’un abonnement peut créer à cet emplacement. |
| Nombre maximal de groupes de sécurité réseau |50 |Nombre maximal de groupes de sécurité réseau qu’un abonnement peut créer à cet emplacement. |

##<a name="view-an-existing-quota"></a>Afficher un quota existant
Pour afficher un quota existant, cliquez sur **davantage de services**>**fournisseurs de ressources** et sélectionnez le service auquel est associé le quota que vous souhaitez afficher. Ensuite, cliquez sur **Quotas**, puis sélectionnez le Quota que vous souhaitez afficher.
   > ![Affichage d’un quota existant](./media/azure-stack-setting-quota/ExistingQuota.PNG)
