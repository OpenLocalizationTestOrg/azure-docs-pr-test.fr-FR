---
title: aaaChild des runbooks dans Azure Automation | Documents Microsoft
description: "Décrit différentes méthodes de hello pour le démarrage d’un runbook dans Azure Automation à partir d’un autre runbook et partager des informations entre eux."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 919887b9-43e2-4c16-883c-f81807fe37db
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2017
ms.author: magoedte;bwren
ms.openlocfilehash: d3d06818d344b565d53cc4f4705b41dcfcf9a376
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="child-runbooks-in-azure-automation"></a>Runbooks enfants dans Azure Automation
Il est recommandé dans toowrite réutilisables et modulaires runbooks d’automatisation Azure avec une fonction discrète qui peut être utilisée par d’autres runbooks. Un runbook parent appelle souvent un ou plusieurs runbooks enfants des fonctionnalités tooperform requis. Il existe deux façons toocall un runbook enfant et chacune présente des différences que vous devez comprendre afin que vous pouvez déterminer celle qui convient le mieux à vos scénarios.

## <a name="invoking-a-child-runbook-using-inline-execution"></a>Appeler un Runbook enfant à l’aide de l’exécution en ligne
tooinvoke un runbook inline à partir d’un autre runbook, vous utilisez nom hello de hello runbook et fournir des valeurs pour ses paramètres exactement comme vous utiliseriez une activité ou une applet de commande.  Tous les runbooks hello même compte Automation est tooall disponible à d’autres toobe utilisés de cette manière. Hello le runbook parent attend que hello enfant runbook toocomplete avant de déplacer la ligne suivante de toohello, et les sorties sont retournées directement toohello parent.

Lorsque vous appelez un runbook inline, il s’exécute dans hello même de la tâche en tant que le runbook parent hello. Il y a aucune indication dans l’historique des travaux hello du runbook enfant hello qu’il a exécuté. Toutes les exceptions et les flux de sortie du runbook de hello enfant sera associés au parent de hello. Cela entraîne moins de travaux et facilite tootrack, tootroubleshoot depuis toutes les exceptions levées par le runbook enfant hello et sa sortie de flux de données sont associés avec la tâche parent de hello.

Lorsqu’un Runbook est publié, les Runbooks enfants qu’il appelle doivent déjà être publiés. En effet, Azure Automation crée une association avec tous les Runbooks enfants lorsqu’un Runbook est compilé. Si elles ne sont pas, le runbook parent hello apparaîtra toopublish correctement, mais génère une exception lorsqu’il est démarré. Dans ce cas, vous pouvez republier le runbook parent hello dans les runbooks enfants hello ordre tooproperly référence. Il est inutile toorepublish hello parent runbook si les runbooks enfants de hello sont modifiés, car l’association de hello est déjà créée.

paramètres Hello d’un runbook enfant appelé inline peuvent être n’importe quel type de données, y compris les objets complexes et il n’est pas [sérialisation JSON](automation-starting-a-runbook.md#runbook-parameters) qu’il est quand vous démarrez runbook hello à l’aide de hello portail de gestion Azure, ou par hello Applet de commande Start-AzureRmAutomationRunbook.

### <a name="runbook-types"></a>Types de runbook
Types pouvant s’appeler mutuellement :

* Un [runbook PowerShell](automation-runbook-types.md#powershell-runbooks) et des [runbooks graphiques](automation-runbook-types.md#graphical-runbooks) peuvent s’appeler mutuellement en ligne (les deux sont basés sur PowerShell).
* Un [runbook PowerShell Workflow](automation-runbook-types.md#powershell-workflow-runbooks) et des runbooks PowerShell Workflow graphiques peuvent s’appeler mutuellement en ligne (les deux sont basé sur PowerShell)
* Hello PowerShell types et hello que types de flux de travail PowerShell ne peut pas appeler les uns des autres inline et doit utiliser AzureRmAutomationRunbook de début.

Pertinence de l’ordre de publication :

* Hello publier l’ordre des procédures opérationnelles a une incidence uniquement pour les runbooks PowerShell Workflow et les flux de travail PowerShell graphique.

Lorsque vous appelez un runbook enfant graphique ou de flux de travail PowerShell à l’aide de l’exécution inline, vous utilisez simplement nom hello de hello runbook.  Lorsque vous appelez un runbook enfant de PowerShell, vous devez précédé son nom avec *.\\*  toospecify qui hello script se trouve dans le répertoire local de hello. 

### <a name="example"></a>Exemple
Bonjour à l’exemple suivant appelle un runbook enfant qui accepte trois paramètres, un objet complexe, un entier et une valeur booléenne. sortie de Hello du runbook enfant de hello est affectée tooa variable.  Dans ce cas, le runbook enfant hello est un runbook PowerShell Workflow

    $vm = Get-AzureRmVM –ResourceGroupName "LabRG" –Name "MyVM"
    $output = PSWF-ChildRunbook –VM $vm –RepeatCount 2 –Restart $true

Voici hello même exemple à l’aide d’un runbook PowerShell en tant qu’enfant de hello.

    $vm = Get-AzureRmVM –ResourceGroupName "LabRG" –Name "MyVM"
    $output = .\PS-ChildRunbook.ps1 –VM $vm –RepeatCount 2 –Restart $true


## <a name="starting-a-child-runbook-using-cmdlet"></a>Démarrage d’un Runbook enfant à l’aide d’une applet de commande
Vous pouvez utiliser hello [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) toostart de l’applet de commande un runbook, comme décrit dans [toostart un runbook avec Windows PowerShell](automation-starting-a-runbook.md#starting-a-runbook-with-windows-powershell). Il existe deux modes d’utilisation pour cette applet de commande.  Dans un mode, hello applet de commande renvoie les id de tâche hello dès que la tâche enfant de hello est créé pour le runbook enfant hello.  Dans hello autre mode, vous activez en spécifiant hello **-attente** paramètre, attend que les enfants hello hello applet de commande de la tâche se termine et retourne la sortie de hello du runbook enfant de hello.

tâche Hello à partir d’un runbook enfant démarré avec une applet de commande s’exécute dans un travail distinct hello parent runbook. Cela entraîne plus de travaux que l’appel hello runbook inline et les rend plus difficile tootrack. parent de Hello peut démarrer plusieurs runbooks enfants de façon asynchrone sans attendre que chaque toocomplete. Pour que ce même type d’exécution parallèle appelle les runbooks enfants de hello, le runbook parent hello devez toouse hello [mot clé parallel](automation-powershell-workflow.md#parallel-processing).

Les paramètres d’un runbook enfant démarré avec une applet de commande sont fournis sous forme de table de hachage, comme décrit dans [Paramètres du runbook](automation-starting-a-runbook.md#runbook-parameters). Seuls les types de données simples peuvent être utilisés. Si hello runbook possède un paramètre avec un type de données complexe, puis il doit être appelé inline.

### <a name="example"></a>Exemple
Hello exemple suivant démarre un runbook enfant avec des paramètres et puis attend toocomplete à l’aide de hello AzureRmAutomationRunbook-Start-attendre le paramètre. Une fois terminé, sa sortie est collectée à partir de runbook d’enfant hello.

    $params = @{"VMName"="MyVM";"RepeatCount"=2;"Restart"=$true} 
    $joboutput = Start-AzureRmAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Test-ChildRunbook" -ResourceGroupName "LabRG" –Parameters $params –wait


## <a name="comparison-of-methods-for-calling-a-child-runbook"></a>Comparaison des méthodes pour l’appel d’un Runbook enfant
Hello tableau suivant résume les différences de hello entre hello deux méthodes d’appel d’un runbook à partir d’un autre runbook.

|  | En ligne | Applet de commande |
|:--- |:--- |:--- |
| Travail |Runbooks enfants s’exécutent dans hello même de la tâche en tant que parent de hello. |Un travail distinct est créé pour le runbook enfant hello. |
| Exécution |Le runbook parent attend hello enfant runbook toocomplete avant de continuer. |Le runbook parent se poursuit immédiatement après le démarrage du runbook enfant *ou* runbook parent attend toofinish de travail enfant hello. |
| Sortie |Le Runbook parent peut obtenir directement la sortie du Runbook enfant. |Le runbook parent doit récupérer la sortie à partir de la tâche du runbook enfant *ou* le runbook parent peut obtenir directement la sortie du runbook enfant. |
| Paramètres |Les valeurs des paramètres de runbook hello enfant sont spécifiées séparément et peuvent utiliser n’importe quel type de données. |Les valeurs de hello du runbook enfant doivent être combinées en une seule table de hachage de paramètres et ne peuvent contenir que simple, de tableau et types de données exploitant la sérialisation JSON de l’objet. |
| Compte Automation |Le runbook parent peut uniquement utiliser le runbook enfant Bonjour même compte automation. |Le runbook parent peut utiliser runbook enfant à partir de n’importe quel compte automation à partir de hello même abonnement Azure et même un autre abonnement si vous avez un tooit de connexion. |
| Publication |Le Runbook enfant doit être publié avant la publication du Runbook parent. |Le Runbook enfant doit être publié avant le démarrage du Runbook parent. |

## <a name="next-steps"></a>Étapes suivantes
* [Démarrage d'un Runbook dans Azure Automation](automation-starting-a-runbook.md)
* [Sortie et messages de Runbook dans Azure Automation](automation-runbook-output-and-messages.md)

