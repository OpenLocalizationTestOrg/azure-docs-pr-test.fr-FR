---
title: "aaaAzure vue d’ensemble de Automation DSC | Documents Microsoft"
description: "Vue d'ensemble de la configuration d'état souhaité (DSC) Azure Automation, les termes s'y rapportant et les problèmes connus"
services: automation
documentationcenter: dev-center-name
author: eslesar
manager: carmonm
keywords: "PowerShell DSC, Desired State Configuration, configuration d'état souhaité PowerShell DSC Azure"
ms.assetid: fd40cb68-c1a6-48c3-bba2-710b607d1555
ms.service: automation
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: TBD
ms.date: 06/15/2017
ms.author: eslesar
ms.openlocfilehash: 5b8e5104c7b5bed848c015ac26a8b7d1f5b24de9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-dsc-overview"></a>Vue d'ensemble d'Azure Automation DSC

Azure Automation DSC est un service Azure qui vous permet de toowrite, de gérer et de compiler la Configuration d’état souhaité (DSC) PowerShell [configurations](https://msdn.microsoft.com/powershell/dsc/configurations), importer [des ressources DSC](https://msdn.microsoft.com/powershell/dsc/resources)et attribuer nœuds tootarget configurations, toutes dans le cloud de hello.

## <a name="why-use-azure-automation-dsc"></a>Pourquoi utiliser Azure Automation DSC ?

Azure Automation DSC offre plusieurs avantages par rapport à l’utilisation de DSC en dehors d’Azure.

### <a name="built-in-pull-server"></a>Serveur collecteur intégré

Azure Automation fournit un [serveur collecteur DSC](https://msdn.microsoft.com/en-us/powershell/dsc/pullserver) afin que les nœuds cibles reçoivent automatiquement les configurations, conformes toohello souhaité état et rapport sur leur conformité.
serveur d’extraction intégrée Hello dans Azure Automation élimine hello besoin tooset des et gérer votre propre serveur collecteur.
Azure Automation peut cibler des ordinateurs physiques ou virtuels Windows ou Linux, dans le cloud de hello ou localement.

### <a name="management-of-all-your-dsc-artifacts"></a>Gestion de tous vos artefacts DSC

Azure Automation DSC met hello même couche de gestion trop[Configuration d’état souhaité PowerShell](https://msdn.microsoft.com/powershell/dsc/overview) Azure Automation offre pour l’écriture de scripts PowerShell.

À partir de hello portail Azure, ou à partir de PowerShell, vous pouvez gérer tous vos configurations DSC, les ressources et les nœuds cibles.

![Capture d’écran du panneau d’Azure Automation hello](./media/automation-dsc-overview/azure-automation-blade.png)

### <a name="import-reporting-data-into-log-analytics"></a>Importer des données de création de rapports dans Log Analytics

Nœuds qui sont gérées avec Azure Automation DSC envoi détaillées état données toohello intégrées par extraction de données serveur de rapports.
Vous pouvez configurer Azure Automation DSC toosend cet espace de travail de données tooyour Analytique de journal de Microsoft Operations Management Suite (OMS).
toolearn tooyour de données d’état toosend DSC espace de travail Analytique des journaux, voir [par progression Azure Automation DSC tooOMS de données Analytique de journal de création de rapports](automation-dsc-diagnostics.md).

## <a name="introduction-video"></a>Vidéo de présentation

Préférez la surveillance tooreading ? Jetez un œil sur hello suivant vidéo à partir de mai 2015, quand Azure Automation DSC a été annoncée.

>[!NOTE]
>Alors que les concepts de hello et cycle de vie présentés dans cette vidéo sont corrects, Azure Automation DSC a beaucoup progressé depuis cette vidéo a été enregistrée.
>Il est désormais généralement disponible, a une interface utilisateur beaucoup plus étendue Bonjour portail Azure et prend en charge de nombreuses fonctions supplémentaires.

> [!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3467/player]

## <a name="next-steps"></a>Étapes suivantes

* toolearn tooonboard nœuds toobe gérés dans Azure Automation DSC, voir [d’intégration des ordinateurs pour la gestion par Azure Automation DSC](automation-dsc-onboarding.md)
* tooget démarré à l’aide d’Azure Automation DSC, consultez [prise en main d’Azure Automation DSC](automation-dsc-getting-started.md)
* toolearn sur la compilation des configurations DSC afin que vous pouvez les affecter tootarget nœuds, consultez [la compilation des configurations dans Azure Automation DSC](automation-dsc-compile.md)
* Pour la référence de cmdlet PowerShell pour Azure Automation DSC, consultez [AzureRM.Automation](/powershell/module/azurerm.automation/#automation).
* Pour plus d’informations sur la tarification, consultez [Tarification de Automation](https://azure.microsoft.com/pricing/details/automation/).
* toosee un exemple d’utilisation d’Azure Automation DSC dans un pipeline de déploiement continu, consultez [tooIaaS déploiement continu Chocolatey et les machines virtuelles à l’aide de Azure Automation DSC](automation-dsc-cd-chocolatey.md)
