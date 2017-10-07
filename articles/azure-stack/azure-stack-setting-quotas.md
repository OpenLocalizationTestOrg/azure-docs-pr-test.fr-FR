---
title: aaaQuotas dans la pile de Azure | Documents Microsoft
description: "Les administrateurs définir quantité maximale de hello toorestrict quotas de ressources que les clients ont accès à."
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
ms.openlocfilehash: 9770802960af102a6d497b47d95cd6ec63ce219c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="set-and-view-quotas-in-azure-stack"></a>Définir et afficher des quotas dans la pile de Azure
Quotas de définissent des limites de hello de ressources pour un abonnement locataire peut fournir ou consommer. Par exemple, un quota peut permettre à un client créer des machines virtuelles de toofive. tooadd un plan de tooa service, l’administrateur doit configurer les paramètres de quota hello pour ce service.

Les quotas sont configurables par service et par emplacement, l’activation des administrateurs tooprovide un contrôle granulaire sur la consommation des ressources hello. Les administrateurs peuvent créer une ou plusieurs ressources de quota et les associer à des plans, ce qui signifie qu’ils puissent fournir des offres différenciés de leurs services. Quotas pour un service donné peuvent être créés à partir de hello **fournisseur de ressources** panneau d’administration pour ce service.

Un locataire qui s’abonne offre tooan contenant plusieurs plans peut utiliser toutes les ressources qui sont disponibles dans chaque plan.

## <a name="toocreate-an-iaas-quota"></a>toocreate un quota IaaS
1. Dans un navigateur, accédez à [https://adminportal.local.azurestack.external](https://adminportal.local.azurestack.external/).
   
   Connectez-vous toohello portail de la pile de Azure en tant qu’administrateur (à l’aide des informations d’identification hello que vous avez fourni au cours du déploiement).
2. Sélectionnez **nouveau**, puis **client offre + Plans**, puis sélectionnez **Quota**.
3. Sélectionnez hello premier service pour lequel vous souhaitez toocreate un quota. Pour un quota IaaS, suivez ces étapes pour les services de calcul, réseau et stockage hello.
   Dans cet exemple, nous créons d’abord un quota pour le service de calcul hello. Bonjour **Namespace** liste, sélectionnez hello **Microsoft.Compute** espace de noms.
   
   > ![Création d’un nouveau quota de calcul](./media/azure-stack-setting-quota/NewComputeQuota.PNG)
   > 
   > 
4. Choisir un emplacement hello où le quota de hello est défini (par exemple, « local »).
5. Sur hello **des paramètres de Quota** de l’élément, intitulée **définir la capacité de Quota**. Cliquez sur ce paramètre de quota élément tooconfigure hello.
6. Sur hello **définir les Quotas** panneau, vous voyez toutes les ressources de calcul hello pour laquelle vous pouvez configurer des limites. Chaque type a une valeur par défaut qui est associé. Vous pouvez modifier ces valeurs ou vous pouvez sélectionner hello **Ok** bouton bas hello hello panneau tooaccept hello valeurs par défaut.
   
   > ![Définition d’un quota de calcul](./media/azure-stack-setting-quota/SetQuotasBladeCompute.PNG)
   > 
   > 
7. Une fois que vous avez configuré les valeurs hello et cliqué sur **Ok**, hello **des paramètres de Quota** élément apparaît comme **configuré**. Cliquez sur **Ok** créer hello **Quota** ressource.
   
   Vous devez voir une notification indiquant que la ressource de quota hello est créée.
8. Une fois hello quota ensemble a été créé avec succès, vous recevez une deuxième notification. quota de service de calcul Hello est maintenant prêt toobe associé à un plan. Répétez ces étapes avec hello réseau et les services de stockage, et que vous êtes prêt toocreate un plan IaaS !
   
   > ![Notification en cas de réussite de la création du quota](./media/azure-stack-setting-quota/QuotaSuccess.png)
   > 
   > 

## <a name="compute-quota-types"></a>Types de quotas de capacité de traitement (compute)
| **Type** | **Valeur par défaut** | **Description** |
| --- | --- | --- |
| Nombre maximal de machines virtuelles |50 |nombre maximal de Hello d’ordinateurs virtuels qu’un abonnement peut créer à cet emplacement. |
| Nombre maximal de cœurs de machine virtuelle |100 |Hello nombre maximal de cœurs un abonnement peut créer à cet emplacement (par exemple, une machine virtuelle A3 a quatre cœurs). |
| Quantité maximale de mémoire de l’ordinateur virtuel (en Go) |150 |quantité maximale de Hello de RAM qui peut être configuré en mégaoctets (par exemple, une machine virtuelle A1 consomme 1,75 Go de RAM). |

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

##<a name="view-an-existing-quota"></a>Afficher un quota existant
tooview un quota existant, cliquez sur **davantage de services**>**fournisseurs de ressources** et sélectionnez service hello quels hello quota que vous souhaitez tooview est associé. Ensuite, cliquez sur **Quotas**, puis sélectionnez hello Quota que vous souhaitez tooview.
   > ![Affichage d’un quota existant](./media/azure-stack-setting-quota/ExistingQuota.PNG)
