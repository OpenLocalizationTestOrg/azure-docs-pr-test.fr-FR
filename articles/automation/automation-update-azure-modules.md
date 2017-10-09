---
title: aaaUpdate Azure modules dans Azure Automation | Documents Microsoft
description: "Cet article décrit comment vous pouvez désormais mettre à jour les modules Azure PowerShell courants fournis par défaut dans Azure Automation."
services: automation
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: tysonn
ms.assetid: 
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/13/2017
ms.author: magoedte
ms.openlocfilehash: afa404a643349f044e55be2280e435b575049dec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooupdate-azure-powershell-modules-in-azure-automation"></a>Comment les modules Azure PowerShell tooupdate dans Azure Automation

les modules Azure PowerShell courants Hello sont fournis par défaut dans chaque compte Automation.  mises à jour de l’équipe Azure Hello hello régulièrement, les modules Azure afin de hello compte Automation nous fournissent un moyen de vous tooupdate des modules de hello dans le compte de hello lorsque de nouvelles versions sont disponibles à partir du portail de hello.  

Étant donné que les modules sont régulièrement mises à jour par groupe de produits hello, les modifications peuvent se produire avec les applets de commande hello inclus, ce qui peut affecter les vos procédures opérationnelles en fonction de type hello de modification, telles que la modification du nom d’un paramètre ou l’obsolescence d’une applet de commande entièrement. tooavoid ayant un impact sur les procédures opérationnelles hello automatisent les processus qu’ils, il est fortement recommandé de tester et valider avant de continuer.  Si vous n’avez pas un compte Automation dédié conçu à cet effet, envisagez de créer une afin que vous pouvez tester les nombreux différents scénarios et les permutations pendant le développement hello de vos runbook, des modifications de tooiterative Ajout telles que la mise à jour de hello Modules PowerShell.  Une fois les résultats hello sont validées et que vous avez appliqué les modifications nécessaires, poursuivre la coordination de la migration de tous les runbooks qui exigeait que hello et effectuer la mise à jour de l’hello comme décrit dans la production.     

## <a name="updating-azure-modules"></a>Mise à jour de modules Azure

1. Dans les Modules hello Panneau de votre compte Automation il existe une option appelée **mise à jour les Modules Azure**.  Elle est toujours activée.<br><br> ![Option de mise à jour de modules Azure dans le panneau Modules](media/automation-update-azure-modules/automation-update-azure-modules-option.png)

2. Cliquez sur **mise à jour Azure Modules** et vous verrez un message de confirmation qui vous demande si vous voulez toocontinue.<br><br> ![Notification de mise à jour des modules Azure](media/automation-update-azure-modules/automation-update-azure-modules-popup.png)

3. Cliquez sur **Oui** et processus de mise à jour de module hello commence.  processus de mise à jour Hello prend environ hello tooupdate de 15 à 20 minutes suivant des modules :

  * Microsoft Azure
  * Azure.Storage
  * AzureRm.Automation
  * AzureRm.Compute
  * AzureRm.Profile
  * AzureRm.Resources
  * AzureRm.Sql
  * AzureRm.Storage

    Si les modules hello sont déjà toodate, processus de hello s’achève en quelques secondes.  Vous serez averti une fois hello mise à jour terminée.<br><br> ![Mise à jour d’état de mise à jour des modules Azure](media/automation-update-azure-modules/automation-update-azure-modules-updatestatus.png)

> [!NOTE]
> Azure Automation utilise les modules dernière hello dans votre compte Automation lors de l’exécution d’une tâche planifiée.    

Si vous utilisez les applets de commande à partir de ces modules Azure PowerShell dans votre toomanage runbooks Azure ressources, il convient alors tooperform ce processus de mise à jour tous les mois ou donc tooassure que vous avez hello modules plus récente.

## <a name="next-steps"></a>Étapes suivantes

* toolearn en savoir plus sur les Modules d’intégration et comment toofurther de modules personnalisés toocreate intégrer Automation avec d’autres systèmes, les services ou les solutions, consultez [Modules d’intégration](automation-integration-modules.md).

* Envisagez d’intégration de contrôle de code source à l’aide [GitHub Enterprise](automation-scenario-source-control-integration-with-github-ent.md) ou [Visual Studio Team Services](automation-scenario-source-control-integration-with-vsts.md) toocentrally gérer et contrôler les versions de votre portefeuille de configuration et de runbook Automation.  
