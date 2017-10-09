---
title: "aaaUse Azure Automation toovertically mettre à l’échelle de machines virtuelles Windows | Documents Microsoft"
description: "Évolution verticale d’une Machine virtuelle Windows dans les alertes de réponse de toomonitoring avec Azure Automation"
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4f964713-fb67-4bcc-8246-3431452ddf7d
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/29/2016
ms.author: kasing
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 24d07f3e2e217668f18676e6d6873be4f9770349
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="vertically-scale-windows-vms-with-azure-automation"></a>Mettre à l’échelle verticalement des machines virtuelles Windows avec Azure Automation

Mise à l’échelle verticale consiste hello croissantes ou décroissantes ressources hello d’un ordinateur dans la charge de travail de réponse toohello. Dans Azure, cela peut être accompli en modifiant la taille de hello Hello Machine virtuelle. Cela peut vous aider dans les scénarios suivants de hello

* Si hello Machine virtuelle n’est pas utilisé fréquemment, vous pouvez la redimensionner vers le bas tooa plus petite taille tooreduce vos coûts mensuels
* Si hello Machine virtuelle voit une charge de pointe, il peut être redimensionné tooa plus grande taille tooincrease sa capacité maximale

plan Hello pour tooaccomplish d’étapes hello il s’agit en tant que ci-dessous

1. Le programme d’installation Azure Automation tooaccess vos Machines virtuelles
2. Importer des procédures opérationnelles de l’échelle verticale de Azure Automation hello dans votre abonnement
3. Ajouter un runbook de tooyour webhook
4. Ajouter une alerte tooyour Machine virtuelle

> [!NOTE]
> En raison de la taille de hello Hello première Machine virtuelle, tailles hello à l’échelle, peut être limitée en raison de la disponibilité toohello Hello autres tailles de cluster de hello actuel ordinateur virtuel est déployé dans. Bonjour publiées de runbook automation utilisés dans cet article nous prendre en charge ce cas et uniquement l’échelle dans hello ci-dessous paires de taille de machine virtuelle. Cela signifie qu’un ordinateur virtuel de Standard_D1v2 ne sera pas soudainement mis à l’échelle tooStandard_G5 ou la descente tooBasic_A0.
> 
> | Paires de mise à l’échelle des machines virtuelles |  |
> | --- | --- |
> | Basic_A0 |Basic_A4 |
> | Standard_A0 |Standard_A4 |
> | Standard_A5 |Standard_A7 |
> | Standard_A8 |Standard_A9 |
> | Standard_A10 |Standard_A11 |
> | D1 standard |D4 standard |
> | D11 standard |D14 standard |
> | Standard_DS1 |Standard_DS4 |
> | Standard_DS11 |Standard_DS14 |
> | Standard_D1v2 |Standard_D5v2 |
> | Standard_D11v2 |Standard_D14v2 |
> | Standard_G1 |Standard_G5 |
> | Standard_GS1 |Standard_GS5 |
> 
> 

## <a name="setup-azure-automation-tooaccess-your-virtual-machines"></a>Le programme d’installation Azure Automation tooaccess vos Machines virtuelles
Hello première chose toodo consiste à créer un compte Azure Automation qui hébergera hello procédures opérationnelles utilisé tooscale une Machine virtuelle. Récemment service d’automatisation hello introduit la fonctionnalité « Exécuter en tant que compte » hello qui rend la hello Principal du Service pour l’exécution automatique des procédures opérationnelles de hello sur hello utilisateur très facile. Vous pouvez en savoir plus à ce sujet dans l’article hello ci-dessous :

* [Authentifier des Runbooks avec un compte d’identification Azure](../../automation/automation-sec-configure-azure-runas-account.md)

## <a name="import-hello-azure-automation-vertical-scale-runbooks-into-your-subscription"></a>Importer des procédures opérationnelles de l’échelle verticale de Azure Automation hello dans votre abonnement
Hello procédures opérationnelles qui sont nécessaires pour la mise à l’échelle verticalement votre Machine virtuelle sont déjà publiés dans hello galerie de runbooks Azure Automation. Vous devez tooimport dans votre abonnement. Vous pouvez apprendre comment runbooks tooimport en lisant hello article suivant.

* [Galeries de runbooks et de modules pour Azure Automation](../../automation/automation-runbook-gallery.md)

procédures opérationnelles Hello nécessitant toobe importé sont affichés dans image hello ci-dessous

![Importer des runbooks](./media/vertical-scaling-automation/scale-runbooks.png)

## <a name="add-a-webhook-tooyour-runbook"></a>Ajouter un runbook de tooyour webhook
Une fois que vous avez importé les runbooks hello, vous devez tooadd un runbook de toohello webhook afin qu’elle peut être déclenchée par une alerte à partir d’un ordinateur virtuel. Détails de Hello de création d’un webhook pour votre Runbook peuvent être lu ici

* [Webhooks Azure Automation](../../automation/automation-webhooks.md)

Assurez-vous que vous copiez hello webhook avant de fermer la boîte de dialogue hello webhook car vous en aurez besoin dans la section suivante de hello.

## <a name="add-an-alert-tooyour-virtual-machine"></a>Ajouter une alerte tooyour Machine virtuelle
1. Sélectionnez les paramètres des machines virtuelles
2. Sélectionnez Règles d’alerte
3. Sélectionnez Ajouter une alerte
4. Sélectionnez une alerte de hello métrique toofire sur
5. Sélectionnez une condition, où remplies va entraîner toofire d’alerte hello
6. Sélectionnez un seuil pour la condition de hello à l’étape 5. toobe remplie
7. Sélectionnez une période sur quel hello service d’analyse vérifie pour la condition de hello et le seuil dans les étapes 5 et 6
8. Collez webhook hello copié à partir de la section précédente de hello.

![Ajouter des alerte tooVirtual Machine 1](./media/vertical-scaling-automation/add-alert-webhook-1.png)

![Ajouter des alerte tooVirtual ordinateur 2](./media/vertical-scaling-automation/add-alert-webhook-2.png)

