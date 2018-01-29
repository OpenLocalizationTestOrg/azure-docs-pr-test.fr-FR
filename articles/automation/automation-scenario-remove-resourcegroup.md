---
title: Automatiser la suppression des groupes de ressources | Microsoft Docs
description: "Version du workflow PowerShell d’un scénario d’Azure Automation incluant des runbooks pour supprimer tous les groupes de ressources de votre abonnement."
services: automation
documentationcenter: 
author: georgewallace
manager: jwhit
editor: 
ms.assetid: b848e345-fd5d-4b9d-bc57-3fe41d2ddb5c
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/26/2016
ms.author: magoedte
ms.openlocfilehash: e1734bdd22ecfc4e54074f02582f5a8eca7d4f59
ms.sourcegitcommit: 9292e15fc80cc9df3e62731bafdcb0bb98c256e1
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/10/2018
---
# <a name="azure-automation-scenario---automate-removal-of-resource-groups"></a>Scénario Azure Automation - Automatiser la suppression de groupes de ressources
De nombreux clients créent plusieurs groupes de ressources. Certains peuvent être utilisés pour la gestion des applications de production, et d’autres comme environnement de développement, de test et intermédiaires. Automatiser le déploiement de ces ressources est une chose, mais être capable de désactiver un groupe de ressources d’un simple clic en est une autre. Vous pouvez simplifier cette tâche de gestion courante à l’aide d’Azure Automation. Cela est également utile si vous travaillez avec un abonnement Azure présentant une limite de dépense obtenue via une offre spéciale réservée aux membres de MSDN ou du programme Microsoft Partner Network Cloud Essentials.

Ce scénario repose sur un runbook PowerShell et est conçu pour supprimer un ou plusieurs groupes de ressources que vous spécifiez de votre abonnement. Le paramètre par défaut du runbook consiste à effectuer un test avant de continuer. Cela garantit de ne pas supprimer accidentellement le groupe de ressources avant d’être prêt à effectuer cette procédure.   

## <a name="getting-the-scenario"></a>Obtention du scénario
Ce scénario se compose d’un runbook PowerShell que vous pouvez télécharger depuis [PowerShell Gallery](https://www.powershellgallery.com/packages/Remove-ResourceGroup/1.0/DisplayScript). Vous pouvez également l’importer directement depuis [Runbook Gallery](automation-runbook-gallery.md) dans le portail Azure.<br><br>

| Runbook | DESCRIPTION |
| --- | --- |
| Remove-ResourceGroup |Supprime un ou plusieurs groupes de ressources Azure et les ressources associées de l’abonnement. |

<br>
Les paramètres d’entrée suivants sont définis pour ce runbook :

| Paramètre | DESCRIPTION |
| --- | --- |
| NameFilter (obligatoire) |Spécifie un filtre de nom pour limiter les groupes de ressources que vous avez l’intention de supprimer. Vous pouvez transmettre plusieurs valeurs à l’aide d’une liste séparée par des virgules.<br>Le filtre ne respecte pas la casse et établit une correspondance avec tous les groupes de ressources qui contiennent cette chaîne. |
| PreviewMode (facultatif) |Exécutez le runbook pour voir quels groupes de ressources seraient supprimés, sans procéder à leur suppression.<br>**true** afin d’éviter la suppression accidentelle de groupes de ressources transmis au runbook. |

## <a name="install-and-configure-this-scenario"></a>Installer et configurer ce scénario
### <a name="prerequisites"></a>Conditions préalables
Ce runbook s’authentifie à l’aide du [compte d’identification Azure](automation-sec-configure-azure-runas-account.md).    

### <a name="install-and-publish-the-runbooks"></a>Installer et publier des Runbook
Après avoir téléchargé le runbook, vous pouvez l’importer à l’aide de la procédure décrite dans les [procédures d’importation de runbooks](automation-creating-importing-runbook.md#importing-a-runbook-from-a-file-into-azure-automation). Publiez le runbook une fois qu’il a été correctement importé dans votre compte Automation.

## <a name="using-the-runbook"></a>Utilisation du runbook
La procédure suivante vous guide à travers l’exécution de ce runbook et vous aide à vous familiariser avec son fonctionnement. Dans cet exemple, vous allez uniquement tester le runbook ; nous ne procéderons pas à la suppression effective du groupe de ressources.  

1. À partir du portail Azure, ouvrez votre compte Automation, puis cliquez sur la vignette **Runbooks**.
2. Sélectionnez le runbook **Remove-ResourceGroup** et cliquez sur **Démarrer**.
3. Lorsque vous démarrez le runbook, le panneau **Démarrer le Runbook** s’ouvre. Vous pouvez configurer les paramètres. Entrez le nom des groupes de ressources de votre abonnement que vous pouvez utiliser pour le test et dont la suppression accidentelle n’aura aucune incidence.<br> ![Paramètres de Remove-ResouceGroup](media/automation-scenario-remove-resourcegroup/remove-resourcegroup-input-parameters.png)

   > [!NOTE]
   > Assurez-vous que l’option **PreviewMode** est définie sur **true** afin d’éviter de supprimer les groupes de ressources sélectionnés.  **Notez** que ce runbook ne supprimera pas le groupe de ressources contenant le compte Automation qui exécute ce runbook.  
   >
   >
4. Une fois toutes les valeurs des paramètres configurées, cliquez sur **OK**. Le runbook est placé en file d’attente en vue de l’exécution.  

Pour visualiser les détails de la tâche du runbook **Remove-ResourceGroup** dans le portail Azure, sélectionnez **Tâches** dans le runbook. Le résumé de la tâche affiche les paramètres d’entrée et le flux de sortie, en plus des informations générales sur le travail et des exceptions.<br> ![État de la tâche du runbook Remove-ResourceGroup](media/automation-scenario-remove-resourcegroup/remove-resourcegroup-runbook-job-status.png).

Le **Résumé du travail** inclut les messages des flux de sortie, des flux d’avertissements et des flux d’erreurs. Pour visualiser les résultats détaillés de l’exécution du Runbook, sélectionnez **Sortie**.<br> ![Résultats de la sortie du runbook Remove-ResourceGroup](media/automation-scenario-remove-resourcegroup/remove-resourcegroup-runbook-job-output.png)

## <a name="next-steps"></a>étapes suivantes
* Pour vous familiariser avec la création de votre propre runbook, consultez [Création ou importation d’un runbook dans Azure Automation](automation-creating-importing-runbook.md).
* Pour prendre en main des Runbooks de workflow PowerShell, consultez [Mon premier Runbook PowerShell Workflow](automation-first-runbook-textual.md).
