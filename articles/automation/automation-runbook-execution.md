---
title: "l’exécution d’aaaRunbook dans Azure Automation | Documents Microsoft"
description: "Décrit les détails de hello de mode de traitement d’un runbook dans Azure Automation."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: d10c8ce2-2c0b-4ea7-ba3c-d20e09b2c9ca
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/17/2017
ms.author: bwren
ms.openlocfilehash: bdb535675443353d44640bc7773de3f9dac5e42c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="runbook-execution-in-azure-automation"></a>Exécution d'un Runbook dans Azure Automation
Lorsque vous démarrez un Runbook dans Azure Automation, une tâche est créée. Une tâche est une instance d'exécution unique d'un Runbook. Une Automation Azure thread de travail est affecté toorun chaque tâche. Même si les travaux sont partagés par plusieurs comptes Azure, les tâches des différents comptes Automation sont isolées les unes des autres. Il est inutile contrôler quels demande hello de services de travail pour votre travail.  Un même Runbook peut avoir plusieurs tâches s'exécutant à la fois. Lorsque vous affichez la liste hello des procédures opérationnelles Bonjour portail Azure, il répertorie état hello de tous les travaux qui ont été démarrés pour chaque runbook. Vous pouvez afficher la liste hello de tâches pour chaque runbook dans l’ordre tootrack hello état de chaque. Pour obtenir une description de hello différents États de travail, consultez [États des travaux](#job-statuses).

Hello diagramme suivant montre hello du cycle de vie d’un travail de runbook pour [runbooks graphiques](automation-runbook-types.md#graphical-runbooks) et [les runbooks PowerShell Workflow](automation-runbook-types.md#powershell-workflow-runbooks).

![États des tâches - Workflow PowerShell](./media/automation-runbook-execution/job-statuses.png)

Hello diagramme suivant montre hello du cycle de vie d’un travail de runbook pour [runbook PowerShell](automation-runbook-types.md#powershell-runbooks).

![États des tâches - Script PowerShell](./media/automation-runbook-execution/job-statuses-script.png)

Vos travaux ont accès tooyour Azure ressources en effectuant une tooyour connexion abonnement Azure. Ils ont uniquement accès tooresources dans votre centre de données si ces ressources sont accessibles à partir de cloud public de hello.

## <a name="job-statuses"></a>États des tâches
Hello tableau suivant décrit hello différents états possibles d’une tâche.

| État | Description |
|:--- |:--- |
| Completed |Hello terminée avec succès. |
| Échec |Pour [runbook PowerShell Workflow et graphique](automation-runbook-types.md), hello runbook échec toocompile.  Pour [runbooks de PowerShell Script](automation-runbook-types.md), hello runbook échec toostart ou tâche de hello a rencontré une exception. |
| Échec, en attente de ressources |tâche de Hello a échoué, car il a atteint hello [équitable](#fairshare) limiter trois fois et démarré à partir de hello même point de contrôle ou à partir de hello heure de début du runbook de hello chaque. |
| Mis en file d'attente. |travail de Hello est en attente pour les ressources sur toocome d’un travail Automation disponible afin qu’il peut être démarré. |
| Starting |tooa travail a été affectée à la tâche de Hello et système de hello est en cours de hello de démarrage. |
| Reprise |système de Hello est en cours de hello de reprendre le travail de hello a été suspendue. |
| Exécution |Hello tâche s’exécute. |
| En cours d'exécution, en attente de ressources |Hello travail a été déchargé, car il a atteint hello [équitable](#fairshare) limite. Elle reprend bientôt depuis son dernier point de contrôle. |
| Arrêté |tâche de Hello a été arrêtée par l’utilisateur de hello avant qu’elle a été terminée. |
| En cours d’arrêt |système de Hello est en cours de hello d’arrêter la tâche de hello. |
| Interrompu |tâche de Hello a été suspendue par l’utilisateur de hello, par le système de hello ou par une commande dans les runbook hello. Une tâche suspendue peut être redémarrée et reprise à partir de son dernier point de contrôle ou à partir de la hello à partir de hello runbook si elle ne dispose pas des points de contrôle. Hello runbook est uniquement suspendu par le système de hello lorsqu’une exception se produit. Par défaut, ErrorActionPreference est défini trop**continuer**, ce qui signifie que cette tâche hello continue à fonctionner en cas d’erreur. Si cette variable de préférence est définie trop**arrêter**, puis suspend la tâche de hello en cas d’erreur.  S’applique également[runbook PowerShell Workflow et graphique](automation-runbook-types.md) uniquement. |
| Suspension |système de Hello tente une tâche de hello toosuspend à demande hello d’utilisateur de hello. Hello runbook doit atteindre son prochain point de contrôle avant de pouvoir être suspendu. S'il a déjà passé le dernier point de contrôle, il se termine avant d'être suspendu.  S’applique également[runbook PowerShell Workflow et graphique](automation-runbook-types.md) uniquement. |

## <a name="viewing-job-status-from-hello-azure-portal"></a>Affichage de l’état du travail à partir de hello portail Azure
Vous pouvez afficher un état résumé de tous les travaux ou explorez les détails d’une tâche spécifique de runbook dans hello portail Azure ou à la configuration de l’intégration avec votre état de tâche Analytique de journal de Microsoft Operations Management Suite (OMS) espace de travail tooforward runbook et flux de travail.  Pour plus d’informations sur l’intégration à l’Analytique des journaux OMS, consultez [transférer l’état du travail et flux de travail à partir de l’Automation tooLog Analytique (OMS)](automation-manage-send-joblogs-log-analytics.md).  

### <a name="automation-runbook-jobs-summary"></a>Résumé des tâches de Runbook Automation
Sur hello à droite de votre compte Automation sélectionné, vous pouvez voir un résumé de tous les travaux d’un compte Automation sélectionné sous hello **statistiques de travail** vignette.<br><br> ![Vignette Statistiques des tâches](./media/automation-runbook-execution/automation-account-job-status-summary.png).<br> Cette vignette affiche un nombre et une représentation graphique de l’état du travail hello pour tous les travaux exécutés.  

En cliquant sur la vignette de hello présente hello **travaux** panneau, qui inclut une liste récapitulative de tous les travaux exécutés, avec état, l’exécution du travail et les heures de début et de fin.<br><br> ![Panneau Tâches de compte Automation](./media/automation-runbook-execution/automation-account-jobs-status-blade.png)<br><br>  Vous pouvez filtrer la liste hello des tâches en sélectionnant **de filtrer les travaux** et filtrer sur un runbook spécifique, l’état de la tâche ou à partir de la liste déroulante hello, hello toosearch de plage de date/heure dans.<br><br> ![Filtrer l’état des tâches](./media/automation-runbook-execution/automation-account-jobs-filter.png)

Ou bien, vous pouvez afficher les détails d’une tâche récapitulative d’un runbook spécifique en sélectionnant ce runbook à partir de hello **Runbooks** panneau dans votre compte Automation, puis sélectionnez hello **travaux** vignette.  Cela pose hello **travaux** panneau, et à partir de là que vous pouvez cliquer sur tooview enregistrement du travail hello ses détails et sa sortie.<br><br> ![Panneau Tâches de compte Automation](./media/automation-runbook-execution/automation-runbook-job-summary-blade.png)<br> 

### <a name="job-summary"></a>Résumé des tâches
Vous pouvez afficher une liste de tous les travaux hello ont été créées pour un runbook donné et leur état le plus récent. Vous pouvez filtrer cette liste par état du travail et hello plage de dates pour hello dernier changement toohello travail. tooview ses informations détaillées et sa sortie, cliquez sur le nom hello d’une tâche. Hello vue détaillée de tâche de hello inclut les valeurs hello pour les paramètres de runbook hello qui ont été fournis toothat travail.

Vous pouvez utiliser hello suivant de tâches de hello tooview étapes d’un runbook.

1. Bonjour portail Azure, sélectionnez **Automation** , puis sélectionnez nom hello d’un compte Automation.
2. À partir du hub de hello, sélectionnez **Runbooks** et puis sur hello **Runbooks** panneau Sélectionner un runbook à partir de la liste de hello.
3. Dans Panneau de hello pour les runbook hello sélectionné, cliquez sur hello **travaux** vignette.
4. Cliquez sur l’une des tâches hello dans la liste de hello et sur le panneau de détails du travail hello runbook, vous pouvez afficher ses détails et sa sortie.

## <a name="retrieving-job-status-using-windows-powershell"></a>Récupération de l'état d'une tâche à l'aide de Windows PowerShell
Vous pouvez utiliser hello [Get-AzureRmAutomationJob](https://msdn.microsoft.com/library/mt619440.aspx) les travaux de hello tooretrieve créés pour un runbook et hello les détails d’une tâche particulière. Si vous démarrez un runbook avec Windows PowerShell à l’aide [AzureRmAutomationRunbook de début](https://msdn.microsoft.com/library/mt603661.aspx), il retourne la tâche résultante de hello. Utilisez [Get-AzureRmAutomationJob](https://msdn.microsoft.com/library/mt619440.aspx)tooget sortie un travail de sortie.

Bonjour exemples de commandes suivants récupérer hello dernière tâche d’un exemple de runbook et affiche son état, les valeurs hello fournis pour les paramètres de runbook hello et hello la sortie à partir de la tâche de hello.

    $job = (Get-AzureRmAutomationJob –AutomationAccountName "MyAutomationAccount" `
    –RunbookName "Test-Runbook" -ResourceGroupName "ResourceGroup01" | sort LastModifiedDate –desc)[0]
    $job.Status
    $job.JobParameters
    Get-AzureRmAutomationJobOutput -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName "MyAutomationAcct" -Id $job.JobId –Stream Output

## <a name="fair-share"></a>répartition de charge équilibrée
Dans les ressources de tooshare commande entre tous les runbooks dans le cloud de hello, Azure Automation sera décharge temporairement tout travail après qu’il a fonctionné pendant trois heures.  Pendant ce temps, les tâches pour [Runbooks basés sur PowerShell](automation-runbook-types.md#powershell-runbooks) sont arrêtées et non redémarrées.  Hello d’état du travail indique **arrêté**.  Ce type de runbook est toujours redémarré à partir du début de hello, car ils ne prennent pas en charge les points de contrôle.  

[Les Runbooks basés sur le flux de travail PowerShell](automation-runbook-types.md#powershell-workflow-runbooks) reprennent depuis leur dernier [point de contrôle](https://docs.microsoft.com/system-center/sma/overview-powershell-workflows#bk_Checkpoints).  Après avoir exécuté les trois heures, tâche du runbook hello est suspendu par le service de hello et son état indique **en cours d’exécution, en attente de ressources**.  Lorsqu’un bac à sable devient disponible, hello runbook sera automatiquement redémarré par le service d’automatisation hello et reprend à partir du dernier point de contrôle hello.  Ce comportement de flux de travail PowerShell est normal pour la suspension/reprise.  Si hello runbook dépasse encore du runtime, les trois heures hello processus se répète, des heures de toothree.  Après le redémarrage de tiers hello, hello runbook n’a toujours pas terminé dans les trois heures, Échec de la tâche du runbook hello, puis affiche de l’état de la tâche hello **échec, en attente de ressources**.  Dans ce cas, vous recevez hello avec échec de hello l’exception suivante.

*travail de Hello ne peut pas continuer en cours d’exécution, car il a été évincé plusieurs fois hello même point de contrôle. Assurez-vous que votre Runbook n’effectue pas des opérations de longue durée sans conserver son état.*

Il s’agit service hello de tooprotect à partir de l’exécution de procédures opérationnelles indéfiniment sans fin, car ils ne sont pas en mesure de toomake il toohello un point de contrôle suivant sans nouveau déchargement.

Si hello runbook ne possède aucun point de contrôle ou de travail de hello n’a pas atteint premier point de contrôle hello avant son déchargement, puis il redémarre à partir du début de hello.  

Lorsque vous créez un runbook, vous devez vous assurer que toorun de temps hello toutes les activités entre deux points de contrôle ne dépasse pas trois heures. Vous devrez peut-être tooensure runbook tooyour tooadd de points de contrôle qu’il ne pas atteint cette limite de trois heures ou décomposent long opérations en cours d’exécution. Par exemple, votre Runbook peut effectuer une réindexation sur une base de données SQL volumineuse. Si cette opération ne se termine pas dans hello juste limite de partage, puis le travail de hello est déchargé et redémarré à partir du début de hello. Dans ce cas, vous devez décomposer les opération de réindexation hello en plusieurs étapes, telles que la réindexation d’une table à la fois et puis insérez un point de contrôle après chaque opération afin que hello travail puisse reprendre après hello dernière opération toocomplete.

## <a name="next-steps"></a>Étapes suivantes
* toolearn savoir plus sur hello différentes méthodes qui peuvent être utilisé toostart un runbook dans Azure Automation, consultez [démarrage d’un runbook dans Azure Automation](automation-starting-a-runbook.md)

