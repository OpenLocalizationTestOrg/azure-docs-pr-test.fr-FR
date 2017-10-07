---
title: "capacité de réplication aaaEstimate dans Azure | Documents Microsoft"
description: "Utilisez cette capacité de tooestimate article lors de la réplication avec Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 0a1cd8eb-a8f7-4228-ab84-9449e0b2887b
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: nisoneji
ms.openlocfilehash: 54d10e50dd4fc1b875273c7fc0f38f0e85dadddc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="plan-capacity-for-protecting-virtual-machines-and-physical-servers-in-azure-site-recovery"></a>Planifier la capacité pour la protection des machines virtuelles et des serveurs physiques dans Azure Site Recovery

Bonjour Azure Site Recovery Capacity Planner outil vous aide à toofigure à vos besoins en capacité lors de la réplication des ordinateurs virtuels Hyper-V, les ordinateurs virtuels VMware et les serveurs physiques Windows/Linux avec Azure Site Recovery.

Utilisez hello Site Recovery Capacity Planner tooanalyze votre environnement source et les charges de travail, estimer les besoins en bande passante et de ressources de serveur que vous aurez besoin pour l’emplacement de source de hello et ressources hello (machines virtuelles et stockage, etc.) dont vous avez besoin dans la cible de hello emplacement.

Vous pouvez exécuter l’outil de hello dans deux modes :

* **Planification rapide**: exécuter les outil hello dans ce mode tooget réseau et serveur les projections basées sur un nombre moyen de machines virtuelles, de disques, de stockage et de taux de modification.
* **Planification détaillée**: exécutez l’outil de hello dans ce mode et fournissent des détails de chaque charge de travail au niveau de la machine virtuelle. Analysez la compatibilité de machine virtuelle et obtenez des projections réseau et serveur.

## <a name="before-you-start"></a>Avant de commencer


1. Collecter des informations relatives à votre environnement, et notamment les machines virtuelles, le nombre de disques par machine virtuelle, le stockage par disque.
2. Déterminer le taux de modification (l’évolution) quotidienne des données répliquées. toodo cela :

   * Si vous répliquez des ordinateurs virtuels Hyper-V, puis téléchargez hello [outil de planification des capacités de Hyper-V](https://www.microsoft.com/download/details.aspx?id=39057) taux de modification tooget hello. [En savoir plus](site-recovery-capacity-planning-for-hyper-v-replication.md) sur cet outil. Nous vous recommandons de qu'exécuter cet outil sur un toocapture semaine moyennes.
   * Si vous répliquez des machines virtuelles VMware, utilisez hello [planification de déploiement Azure Site Recovery](./site-recovery-deployment-planner.md) taux d’évolution du toofigure out hello.
   * Si vous répliquez des serveurs physiques, vous devez tooestimate manuellement.

## <a name="run-hello-quick-planner"></a>Exécutez hello Planner rapide
1. Téléchargez et ouvrez hello [Azure Site Recovery Capacity Planner](http://aka.ms/asr-capacity-planner-excel) outil. Vous devez toorun macros, sélectionnez tooenable la modification et activer contenu lorsque vous y êtes invité.
2. Dans **sélectionner un type de module** sélectionnez **Planner rapide** à partir de la zone de liste hello.

   ![Prise en main](./media/site-recovery-capacity-planner/getting-started.png)
3. Bonjour **Capacity Planner** feuille de calcul, entrez les informations de hello requis. Vous devez renseigner tous les champs hello entourés en rouge dans la capture d’écran hello ci-dessous.

   * Dans **sélectionner votre scénario**, choisissez **Hyper-V tooAzure** ou **VMware/physiques tooAzure**.
   * Dans **taux (en %) de modification de données quotidiennes moyenne**, placez dans hello informations à l’aide de hello [outil de planification des capacités de Hyper-V](site-recovery-capacity-planning-for-hyper-v-replication.md) ou hello [planification de déploiement Azure Site Recovery](./site-recovery-deployment-planner.md).  
   * **La compression** ne s’applique toocompression proposée lors de la réplication des ordinateurs virtuels VMware ou serveurs physiques tooAzure. Nous estimons 30 % ou plus, mais vous pouvez modifier le paramètre hello en fonction des besoins. Pour répliquer des ordinateurs virtuels Hyper-V tooAzure compression, vous pouvez utiliser un dispositif de tiers tels que Riverbed.
   * Dans **Retention Inputs** (Entrées de rétention), spécifiez la durée de conservation des réplicas. Si vous effectuez une réplication VMware ou serveurs physiques, d’entrée la valeur de hello en jours. Si vous effectuez une réplication Hyper-V, spécifier hello en heures.
   * Dans **doit effectuer en nombre d’heures dans laquelle la réplication initiale pour le lot hello d’ordinateurs virtuels** et **nombre d’ordinateurs virtuels par lot de la réplication initiale**, que vous avez entré les paramètres qui sont utilisés configuration requise de la réplication initiale toocompute.  Lors de la récupération de Site est déployée, hello tout jeu de données initial doit être téléchargé.

   ![Entrées](./media/site-recovery-capacity-planner/inputs.png)
4. Une fois que vous avez mis dans les valeurs hello pour l’environnement source hello, la sortie affichée inclut :

   * **Bande passante requise pour la réplication delta** (Mo/s). La bande passante réseau pour la réplication delta hello moyenne taux de modification des données quotidienne est calculée.
   * **Bande passante requise pour la réplication initiale** (Mo/s). La bande passante réseau pour la réplication initiale est calculée sur les valeurs de la réplication initiale hello dans que vous placer.
   * **Espace de stockage requis (en Go)** est le stockage Azure total hello requis.
   * **Nombre total d’e/s sur les comptes de stockage standard** est calculée en fonction de la taille d’unité d’IOPS sur les comptes de stockage standard total hello 8 Ko.  Pourquoi Planner rapide, nombre de hello est calculée en fonction sur tous les disques de machines virtuelles source hello et tous les jours taux de modification des données. Pour hello Planner détaillées, nombre de hello est calculé en fonction du nombre total d’ordinateurs virtuels qui sont des machines virtuelles de Azure mappé toostandard et taux de ces machines virtuelles de modification des données.
   * **Nombre de comptes de stockage standard** fournit nombre total de hello de stockage standard comptes nécessaires tooprotect hello VMs. Un compte de stockage standard peut contenir des e/s too20000 sur tous les ordinateurs virtuels de hello dans un stockage standard, et un maximum de 500 IOPS est pris en charge par disque.
   * **Nombre de disques blob requis** donne hello nombre de disques qui seront créés sur le stockage Azure.
   * **Nombre de comptes de stockage premium requis** fournit des machines virtuelles de hello nombre total de hello de tooprotect de comptes nécessaires de stockage premium. Une machine virtuelle source avec une valeur d’E/S par seconde élevée (supérieure à 20 000) a besoin d’un compte de stockage Premium. Un compte premium storage peut contenir jusqu'à too80000 IOPS.
   * **Nombre total d’e/s sur le stockage premium** est calculée en fonction de la taille d’unité d’e/s 256 Ko sur les comptes de stockage premium total hello.  Pourquoi Planner rapide, nombre de hello est calculée en fonction sur tous les disques de machines virtuelles source hello et tous les jours taux de modification des données. Pour hello Planner détaillées, nombre de hello est nombre total de calculée hello selon des machines virtuelles qui sont mappé toopremium Azure VM (série DS et GS) et les données de salutation modifier taux sur ces machines virtuelles.
   * **Nombre de serveurs de configuration requis** indique le nombre de serveurs de configuration requis pour le déploiement de hello.
   * **Nombre de serveurs de processus supplémentaire requis** indique si les serveurs de traitement supplémentaires sont requis, dans le serveur de traitement toohello ajout est en cours d’exécution sur le serveur de configuration hello par défaut.
   * **stockage supplémentaire de 100 % sur la source de hello** indique si le stockage supplémentaire est requise dans l’emplacement source de hello.

   ![Sortie](./media/site-recovery-capacity-planner/output.png)

## <a name="run-hello-detailed-planner"></a>Exécuter hello Planner détaillées

1. Téléchargez et ouvrez hello [Azure Site Recovery Capacity Planner](http://aka.ms/asr-capacity-planner-excel) outil. Vous devez toorun macros, sélectionnez tooenable la modification et activer contenu lorsque vous y êtes invité.
2. Dans **sélectionner un type de module**, sélectionnez **Planner détaillées** à partir de la zone de liste hello.

   ![Mise en route](./media/site-recovery-capacity-planner/getting-started-2.png)
3. Bonjour **Qualification de la charge de travail** feuille de calcul, entrez les informations de hello requis. Vous devez renseigner hello tous les champs marqués.

   * Dans **cœurs de processeur**, spécifiez le nombre total de hello de cœurs sur un serveur source.
   * Dans **allocation de mémoire en Mo**, spécifiez la taille de hello RAM d’un serveur source.
   * Hello **nombre de cartes réseau**, spécifiez le nombre hello de cartes réseau sur un serveur source.
   * Dans **stockage (en Go) Total**, spécifiez la taille totale de hello de stockage de machine virtuelle hello. Par exemple, si le serveur de source de hello comporte 3 disques 500 Go, taille totale de stockage est de 1 500 Go.
   * Dans **nombre de disques attachés**, spécifiez le nombre total de hello de disques d’un serveur source.
   * Dans **l’utilisation des capacités de disque**, spécifiez l’utilisation moyenne de hello.
   * Dans **modifier tous les jours des taux (en %)**, spécifiez le taux d’un serveur source de modification de données quotidiens de hello.
   * Dans **taille de mappage de Azure**, entrez la taille de machine virtuelle Azure hello que vous souhaitez toomap. Si vous ne souhaitez pas toodo manuellement, cliquez sur **de calcul des machines virtuelles IaaS**. Si vous un paramètre manuel d’entrée, puis cliquez sur le calcul des machines virtuelles IaaS, la définition manuelle de hello peut-être être remplacée, car le processus de calcul hello identifie automatiquement la meilleure correspondance de hello sur la taille de machine virtuelle Azure.

   ![Workload Qualification](./media/site-recovery-capacity-planner/workload-qualification.png)
4. Si vous cliquez sur **Calcul des machines virtuelles IaaS** , les opérations suivantes seront effectuées :

   * Valide les entrées obligatoires hello.
   * Calcule les IOPS et suggère hello meilleures Azure VM aize correspondance pour chaque machines virtuelles qui est éligible pour la réplication tooAzure. Si la détection d’une machine virtuelle de taille inappropriée ne peut être détectée, une erreur est émise. Par exemple, si le nombre hello de disques attachés à 65, une erreur est générée, car la taille de la plus élevée hello Azure VM 64.
   * Suggère un compte de stockage pouvant être utilisé pour une machine virtuelle Azure.
   * Calcule le nombre total de hello des comptes de stockage standard et les comptes de stockage premium requis pour les charges de travail hello. Faites défiler tooview hello type de stockage Azure et compte de stockage hello qui peut être utilisé pour un serveur source.
   * Se termine et trie reste hello de table hello selon le type de stockage requis (standard ou premium) affecté à une machine virtuelle et le nombre de hello de disques attachés. Pour tous les ordinateurs virtuels qui répondent aux exigences de hello pour Azure, hello colonne **VM est qualifié ?** montre **Oui**. Si une machine virtuelle ne peut pas être sauvegardée tooAzure, une erreur s’affiche.

Colonnes AA tooAE sont générés et fournissent des informations pour chaque machine virtuelle.

![Workload Qualification](./media/site-recovery-capacity-planner/workload-qualification-2.png)

### <a name="example"></a>Exemple
Par exemple, pour les six ordinateurs virtuels avec des valeurs hello indiqués dans la table de hello, outil de hello calcule et affecte la meilleure correspondance de machine virtuelle Azure hello et exigences de stockage Azure hello.

![Workload Qualification](./media/site-recovery-capacity-planner/workload-qualification-3.png)

* Dans la sortie de l’exemple hello, notez hello qui suit :

  * Hello première colonne est une colonne de validation pour les machines virtuelles de hello, disques et évolution du code.
  * Pour cinq machines virtuelles, deux comptes de stockage standard et un compte de stockage premium sont nécessaires.
  * VM 3 ne se qualifie pas pour la protection, car un ou plusieurs disques ont un volume supérieur à 1 To.
  * VM1 et VM2 permet le premier compte de stockage standard hello
  * VM4 pouvez utiliser le compte de stockage standard deuxième hello.
  * VM5 et VM6 ont besoin d’un compte de stockage Premium et peuvent utiliser un compte simple.

    > [!NOTE]
    > E/s sur le stockage standard et premium sont calculés au hello au niveau de la machine virtuelle et non au niveau du disque. Une machine virtuelle standard peut gérer des e/s de too500 par disque. Si le nombre d’E/S par seconde pour un disque est supérieur à 500, le stockage Premium est nécessaire. Toutefois, si les e/s pour un disque sont plus de 500, mais e/s pour les disques de machine virtuelle total hello sont dans hello prend en charge les limites de machine virtuelle Azure standards (taille de machine virtuelle, nombre de disques, nombre de mémoire de cartes, UC,), le Planificateur de hello choisit une machine virtuelle et pas hello DS ou GS série standard. Vous avez besoin de cellule de taille Azure de mappage de hello toomanually mise à jour avec la série DS ou GS appropriées machine virtuelle.


Une fois tous les détails de hello sont en place, cliquez sur **outil de planification Envoyer données toohello** tooopen hello **Capacity Planner** les charges de travail sont mis en surbrillance, tooshow qu’il s’agisse de la protection accordées ou non.

### <a name="submit-data-in-hello-capacity-planner"></a>Envoyer des données dans hello Capacity Planner
1. Lorsque vous ouvrez hello **Capacity Planner** feuille de calcul il est rempli en fonction des paramètres de hello que vous avez spécifié. Hello mot « Charge de travail » apparaît dans hello **source des entrées Infra** cellule, tooshow qui hello entrée est hello **Qualification de la charge de travail** feuille de calcul.
2. Si vous souhaitez que les modifications de toomake, vous devez toomodify hello **Qualification de la charge de travail** feuille de calcul, puis cliquez sur **outil de planification Envoyer données toohello** à nouveau.  

   ![Capacity Planner](./media/site-recovery-capacity-planner/capacity-planner.png)
