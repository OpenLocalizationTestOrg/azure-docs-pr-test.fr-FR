---
title: "définie des aaaCreate une disponibilité de la machine virtuelle dans Azure | Documents Microsoft"
description: "Découvrez comment : définir toocreate une disponibilité managée ou non managé de disponibilité définies pour vos machines virtuelles à l’aide d’Azure PowerShell ou hello portail dans le modèle de déploiement du Gestionnaire de ressources hello."
keywords: "groupe à haute disponibilité"
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a3db8659-ace8-4e78-8b8c-1e75c04c042c
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: cynthn
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: eadcdfcd28bb2fa21a4647f207b390c33e022ef1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="increase-vm-availability-by-creating-an-azure-availability-set"></a>Augmenter la disponibilité des machines virtuelles en créant un groupe à haute disponibilité Azure 
Haute disponibilité fournit application tooyour de redondance. Nous vous recommandons de regrouper au moins deux machines virtuelles dans un groupe à haute disponibilité. Cette configuration garantit que pendant un événement de maintenance planifiée ou non, au moins un ordinateur virtuel sera disponible et satisfait hello 99,95 % contrat SLA Azure. Pour plus d’informations, consultez hello [SLA pour les Machines virtuelles](https://azure.microsoft.com/support/legal/sla/virtual-machines/).

> [!IMPORTANT]
> Machines virtuelles doivent être créés dans hello même groupe de ressources que hello à haute disponibilité.
> 

Si vous souhaitez que votre partie de toobe de machine virtuelle d’un ensemble de disponibilité, vous avez besoin de disponibilité de hello toocreate définir premier ou lorsque vous créez votre première machine virtuelle dans le jeu de hello. Si votre machine virtuelle utilise des disques gérés, hello à haute disponibilité doit être créé comme un ensemble de gestion de la disponibilité.

Pour plus d’informations sur la création et à l’aide de la haute disponibilité, consultez [gérer la disponibilité hello des machines virtuelles](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="use-hello-portal-toocreate-an-availability-set-before-creating-your-vms"></a>Utilisez toocreate de portail hello un groupe à haute disponibilité avant de créer vos machines virtuelles
1. Dans le menu du hub hello, cliquez sur **Parcourir** et sélectionnez **à haute disponibilité**.
2. Sur hello **panneau à haute disponibilité**, cliquez sur **ajouter**.
   
    ![Capture d’écran hello ajouter un bouton pour créer un nouvel ensemble de disponibilité.](./media/create-availability-set/add-availability-set.png)
3. Sur hello **créer le groupe à haute disponibilité** panneau, les informations de hello complète pour votre jeu.
   
    ![Capture d’écran qu’affiche hello les informations que vous devez la disponibilité de hello tooenter toocreate définie.](./media/create-availability-set/create-availability-set.png)
   
   * **Nom** -nom de hello doit comprendre les caractères de 1 à 80 constitués de chiffres, des lettres, des points, des traits de soulignement et des tirets. Hello premier caractère doit être une lettre ou un chiffre. dernier caractère de Hello doit être une lettre, un nombre ou un trait de soulignement.
   * **Domaines d’erreur** -domaines d’erreur définissent groupe hello d’ordinateurs virtuels qui partagent un commun power source et le commutateur réseau. Par défaut, les machines virtuelles de hello sont séparées à travers des domaines d’erreur toothree et peuvent être modifiée toobetween 1 et 3.
   * **Mettre à jour des domaines** - cinq domaines de mise à jour sont attribuées par défaut et peut avoir la valeur toobetween 1 et 20. Indiquent les domaines de mise à jour des ordinateurs virtuels et le matériel physique sous-jacent qui peut être redémarré à hello même temps. Par exemple, si nous spécifions cinq mises à jour seront placés dans des domaines, lorsque plus de cinq ordinateurs virtuels sont configurés dans un seul jeu de disponibilité, les machines virtuelles sixième hello hello même domaine de mise à jour en tant que machine virtuelle de la première hello, hello septième dans hello même ID en tant que deuxième machine virtuelle de hello et ainsi de suite. commande Hello de redémarrages de hello n’est peut-être pas séquentiel, mais une mise à jour qu’un seul domaine redémarrera à la fois.
   * **Abonnement** -sélectionnez hello toouse d’abonnement si vous avez plusieurs.
   * **Groupe de ressources** -sélectionnez un groupe de ressources existant en cliquant sur la flèche de hello et un groupe de ressources dans hello liste déroulante. Vous pouvez également créer un nouveau groupe de ressources en entrant un nom. Hello nom peut contenir les hello les caractères suivants : lettres, de nombres, des points, des tirets, des traits de soulignement et lors de l’ouverture ou parenthèse fermante. nom de Hello ne peut pas se terminer par un point. Tous les hello machines virtuelles dans le groupe de disponibilité hello doivent toobe créé dans hello même groupe de ressources en tant que groupe à haute disponibilité hello.
   * **Emplacement** -sélectionner un emplacement dans la déroulante hello.
   * **Managed** : sélectionnez *Oui* toocreate une disponibilité managée définie toouse avec des machines virtuelles qui utilisent des disques gérés pour le stockage. Sélectionnez **non** si hello machines virtuelles qui seront dans l’ensemble de hello utiliser des disques non managés dans un compte de stockage.
   
4. Lorsque vous avez terminé d’entrer des informations hello, cliquez sur **créer**. 

## <a name="use-hello-portal-toocreate-a-virtual-machine-and-an-availability-set-at-hello-same-time"></a>Utilisez hello portail toocreate est un ordinateur virtuel et une disponibilité de définir à hello même temps
Si vous créez une machine virtuelle à l’aide du portail de hello, vous pouvez également créer un nouveau groupe à haute disponibilité pour hello VM pendant que vous créez hello première machine virtuelle dans le jeu de hello. Si vous choisissez des disques gérés toouse pour votre machine virtuelle, un ensemble de gestion de la disponibilité est créé.

![Capture d’écran qui affiche les processus hello pour la création d’un nouveau groupe à haute disponibilité pendant que vous créez hello machine virtuelle.](./media/create-availability-set/new-vm-avail-set.png)

## <a name="add-a-new-vm-tooan-existing-availability-set-in-hello-portal"></a>Ajouter une nouvelle machine virtuelle tooan existant groupe à haute disponibilité dans le portail de hello
Pour chaque VM supplémentaire que vous créez doit appartient au jeu de hello, vérifiez que vous créez dans hello même **groupe de ressources** et puis sélectionnez hello haute disponibilité existante à l’étape 3. 

![Capture d’écran montrant comment tooselect un groupe de disponibilité défini toouse pour votre machine virtuelle.](./media/create-availability-set/add-vm-to-set.png)

## <a name="use-powershell-toocreate-an-availability-set"></a>Utilisez PowerShell toocreate disponibilité définie
Cet exemple crée un groupe à haute disponibilité nommée **myAvailabilitySet** Bonjour **myResourceGroup** groupe de ressources dans hello **ouest des États-Unis** emplacement. Cette action doit toobe effectuée avant que vous créez hello première machine virtuelle qui figurera dans le jeu de hello.

Avant de commencer, assurez-vous d’avoir hello dernière version du module PowerShell de AzureRM.Compute de hello. Exécutez hello après la commande tooinstall il.

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
Pour plus d’informations, consultez la page relative au [contrôle de version d’Azure PowerShell](/powershell/azure/overview).


Si vous utilisez des disques gérés pour vos machines virtuelles, tapez :

```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName "myResourceGroup" '
    -Name "myAvailabilitySet" -Location "West US" -managed
```

Si vous utilisez vos propres comptes de stockage pour vos machines virtuelles, tapez :

```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName "myResourceGroup" '
    -Name "myAvailabilitySet" -Location "West US" 
```

Pour plus d’informations, consultez [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).

## <a name="troubleshooting"></a>Résolution des problèmes
* Lorsque vous créez une machine virtuelle, si vous le souhaitez à haute disponibilité hello n’est pas dans la liste déroulante de hello dans le portail de hello peut avoir créé dans un autre groupe de ressources. Si vous ne connaissez pas le groupe de ressources hello pour votre disponibilité définie, toohello hub menu Aller à et cliquez sur Parcourir > toosee une liste de votre disponibilité jeux et les groupes de ressources auquel ils appartiennent à haute disponibilité.

## <a name="next-steps"></a>Étapes suivantes
Ajouter un stockage supplémentaire tooyour machine virtuelle en ajoutant un autre [disque de données](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

