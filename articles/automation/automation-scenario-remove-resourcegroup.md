---
title: "la suppression d’aaaAutomate des groupes de ressources | Documents Microsoft"
description: "Version de flux de travail PowerShell d’un scénario Azure Automation, y compris des procédures opérationnelles tooremove ressources tous les groupes dans votre abonnement."
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: 
ms.assetid: b848e345-fd5d-4b9d-bc57-3fe41d2ddb5c
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 09/26/2016
ms.author: magoedte
ms.openlocfilehash: d7ff8064842385d57b0eebdf7b263150c958255f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---automate-removal-of-resource-groups"></a>Scénario Azure Automation - Automatiser la suppression de groupes de ressources
De nombreux clients créent plusieurs groupes de ressources. Certains peuvent être utilisés pour la gestion des applications de production, et d’autres comme environnement de développement, de test et intermédiaires. Automatisation du déploiement de ces ressources hello est une chose, mais qui est en mesure de toodecommission un groupe de ressources d’un clic de bouton de hello est une autre. Vous pouvez simplifier cette tâche de gestion courante à l’aide d’Azure Automation. Cela est utile si vous travaillez avec un abonnement Azure qui a une limite de dépense via une offre spéciale telles que MSDN ou hello programme de Microsoft Partner Network Cloud Essentials.

Ce scénario est basé sur un runbook PowerShell et est conçue tooremove un ou plusieurs groupes de ressources que vous spécifiez à partir de votre abonnement. paramètre par défaut Hello hello runbook est tootest avant de continuer. Cela garantit que vous ne supprimez accidentellement groupe de ressources hello avant que vous êtes prêt toocomplete cette procédure.   

## <a name="getting-hello-scenario"></a>Scénario de hello mise en route
Ce scénario se compose d’un runbook PowerShell que vous pouvez télécharger à partir de hello [PowerShell Gallery](https://www.powershellgallery.com/packages/Remove-ResourceGroup/1.0/DisplayScript). Vous pouvez également importer directement à partir de hello [galerie de runbooks](automation-runbook-gallery.md) Bonjour portail Azure.<br><br>

| Runbook | Description |
| --- | --- |
| Remove-ResourceGroup |Supprime un ou plusieurs groupes de ressources Azure et les ressources associées à partir de l’abonnement de hello. |

<br>
Hello des paramètres d’entrée suivants est défini pour ce runbook :

| Paramètre | Description |
| --- | --- |
| NameFilter (obligatoire) |Spécifie un nom filtre toolimit hello ressource les groupes que vous prévoyez de suppression. Vous pouvez transmettre plusieurs valeurs à l’aide d’une liste séparée par des virgules.<br>filtre de Hello ne respecte pas la casse et correspond à n’importe quel groupe de ressources qui contient la chaîne de hello. |
| PreviewMode (facultatif) |Exécute hello runbook toosee les groupes de ressources seront supprimées, mais n’effectue aucune action.<br>valeur par défaut Hello est **true** toohelp éviter la suppression accidentelle de l’un ou plusieurs groupes de ressources passé toohello runbook. |

## <a name="install-and-configure-this-scenario"></a>Installer et configurer ce scénario
### <a name="prerequisites"></a>Composants requis
Ce runbook s’authentifie à l’aide de hello [Azure exécuter en tant que compte](automation-sec-configure-azure-runas-account.md).    

### <a name="install-and-publish-hello-runbooks"></a>Installer et publier des runbooks de hello
Après avoir téléchargé hello runbook, vous pouvez l’importer à l’aide de procédure hello dans [l’importation des procédures runbook](automation-creating-importing-runbook.md#importing-a-runbook-from-a-file-into-azure-automation). Publier hello runbook une fois qu’il a été importé avec succès dans votre compte Automation.

## <a name="using-hello-runbook"></a>À l’aide de runbook de hello
Hello étapes suivantes vous guidera exécution hello de ce runbook et que vous familiariser avec son fonctionnement. Vous seulement Testez hello runbook dans cet exemple, pas réellement supprimer le groupe de ressources hello.  

1. À partir de hello portail Azure, ouvrez votre compte Automation, puis cliquez sur **Runbooks**.
2. Sélectionnez hello **Remove-ResourceGroup** runbook et cliquez sur **Démarrer**.
3. Lorsque vous démarrez hello runbook, hello **démarrer le Runbook** panneau s’ouvre et vous pouvez configurer des paramètres de hello. Entrez les noms de hello des groupes de ressources dans votre abonnement que vous pouvez utiliser pour le test et n’entraîne pas de risque si accidentellement supprimé.<br> ![Paramètres de Remove-ResouceGroup](media/automation-scenario-remove-resourcegroup/remove-resourcegroup-input-parameters.png)

   > [!NOTE]
   > Assurez-vous que **Previewmode** est défini trop**true** tooavoid suppression hello sélectionnée des groupes de ressources.  **Remarque** que ce runbook ne supprime pas le groupe de ressources hello qui contient le compte d’automatisation hello ce runbook est en cours d’exécution.  
   >
   >
4. Après avoir configuré toutes les valeurs de paramètre hello, cliquez sur **OK**, et hello runbook mises en attente pour l’exécution.  

Détails de hello tooview Hello **Remove-ResourceGroup** tâche du runbook Bonjour portail Azure, sélectionnez **travaux** dans les runbook hello. paramètres d’entrée de Hello tâche récapitulative affiche hello et sortie de hello stream en outre toogeneral plus d’informations sur la tâche de hello et toutes les exceptions qui se sont produites.<br> ![État de la tâche du runbook Remove-ResourceGroup](media/automation-scenario-remove-resourcegroup/remove-resourcegroup-runbook-job-status.png).

Hello **récapitulatif** inclut les messages à partir de flux de sortie, d’avertissement et erreur hello. Sélectionnez **sortie** tooview le détail des résultats à partir de l’exécution du runbook hello.<br> ![Résultats de la sortie du runbook Remove-ResourceGroup](media/automation-scenario-remove-resourcegroup/remove-resourcegroup-runbook-job-output.png)

## <a name="next-steps"></a>Étapes suivantes
* tooget aider à créer votre propre runbook, consultez [création ou importation d’un runbook dans Azure Automation](automation-creating-importing-runbook.md).
* tooget démarré avec les runbooks PowerShell Workflow, consultez [mon runbook PowerShell Workflow premier](automation-first-runbook-textual.md).
