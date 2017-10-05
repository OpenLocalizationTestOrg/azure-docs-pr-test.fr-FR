---
title: "Types de Runbook Azure Automation | Microsoft Docs"
description: "Décrit les différents types de Runbooks que vous pouvez utiliser dans Azure Automation et les considérations à prendre en compte pour déterminer le type à utiliser. "
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 9265c975-4281-4819-a84f-d86641277f36
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/01/2017
ms.author: bwren
ms.openlocfilehash: e859aef473b433fbf4efb639962f3a3ce0a23d7b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-automation-runbook-types"></a>Types de Runbooks Azure Automation
Azure Automation prend en charge quatre types de Runbook qui sont brièvement décrits dans le tableau ci-dessous.  Les sections suivantes fournissent de plus amples informations sur chaque type, notamment des considérations sur l'utilisation de chacun de ces types.

| Type | Description |
|:--- |:--- |
| [Graphique](#graphical-runbooks) |Basé sur Windows PowerShell et créé et modifié entièrement dans l'éditeur graphique du portail Azure. |
| [Graphique workflow PowerShell](#graphical-runbooks) |Basé sur le workflow Windows PowerShell et créé et modifié entièrement dans l'éditeur graphique du portail Azure. |
| [PowerShell](#powershell-runbooks) |Runbook texte basé sur le script Windows PowerShell. |
| [Workflow PowerShell](#powershell-workflow-runbooks) |Runbook texte basé sur le workflow Windows PowerShell. |

## <a name="graphical-runbooks"></a>Runbooks graphiques
[Graphique](automation-runbook-types.md#graphical-runbooks) and Graphique PowerShell Workflow runbooks are created and edited with the graphical editor in the Azure portal.  Vous pouvez les exporter vers un fichier puis les importer dans un autre compte Automatisation, mais vous ne pouvez pas les créer ni les modifier avec un autre outil.  Les Runbooks graphiques génèrent un code PowerShell, mais vous ne pouvez pas directement afficher ou modifier ce code. Les Runbooks graphiques ne peuvent pas être convertis en [formats texte](automation-runbook-types.md), et un Runbook texte ne peut pas être converti au format graphique. Les Runbooks graphiques peut être converti en Runbooks de workflow PowerShell pendant l’importation et vice-versa.

### <a name="advantages"></a>Avantages
* Insertion visuelle/lien/configuration d’un modèle de création  
* Concentration sur la circulation des flux de données dans le processus  
* Représentation visuelle des processus de gestion  
* Inclusion d’autres Runbooks en tant que Runbooks enfants pour créer des flux de travail de niveau élevé  
* Programmation modulaire favorisée  


### <a name="limitations"></a>Limitations
* Impossible de modifier le Runbook en dehors du portail Azure.
* Peut nécessiter une activité de code contenant le code PowerShell pour exécuter une logique complexe.
* Impossible d'afficher ou de modifier directement le code PowerShell créé par le workflow graphique. Notez que vous pouvez afficher le code que vous créez dans toute activité de code.

## <a name="powershell-runbooks"></a>Runbooks PowerShell
Les Runbooks PowerShell sont basés sur Windows PowerShell.  Vous modifiez directement le code du Runbook à l'aide de l'éditeur de texte du portail Azure.  Vous pouvez également utiliser n'importe quel éditeur de texte hors ligne et [importer le Runbook](http://msdn.microsoft.com/library/azure/dn643637.aspx) dans Azure Automation.

### <a name="advantages"></a>Avantages
* Implémentez tout type de la logique complexe avec le code PowerShell sans la complexité supplémentaire liée au workflow PowerShell. 
* Le Runbook démarre plus rapidement que les Runbooks de workflow PowerShell dans la mesure où il n'a pas besoin d'être compilé avant l'exécution.

### <a name="limitations"></a>Limites
* Doit être familiarisé avec les scripts PowerShell.
* Impossible d'utiliser un [traitement en parallèle](automation-powershell-workflow.md#parallel-processing) pour effectuer plusieurs actions en parallèle.
* Impossible d'utiliser des [points de contrôle](automation-powershell-workflow.md#checkpoints) pour reprendre le Runbook en cas d'erreur.
* Les Runbooks graphiques et les Runbooks de Workflow PowerShell peuvent uniquement être inclus en tant que Runbooks enfants à l'aide de l'applet de commande Start-AzureAutomationRunbook qui crée une tâche.

### <a name="known-issues"></a>Problèmes connus
Voici les problèmes connus actuels rencontrés avec les Runbooks PowerShell.

* Les Runbooks PowerShell ne peuvent pas récupérer une [ressource variable](automation-variables.md) non chiffrée avec une valeur null.
* Les Runbooks PowerShell ne peuvent pas récupérer une [ressource variable](automation-variables.md) avec le symbole *~* dans le nom.
* Get-Process dans une boucle d’un Runbook PowerShell peut se bloquer après environ 80 itérations. 
* Un Runbook PowerShell peut échouer s’il tente d'écrire une très grande quantité de données dans un flux de sortie.   Vous pouvez généralement contourner ce problème en exportant uniquement les informations dont vous avez besoin lorsque vous travaillez avec des objets volumineux.  Par exemple, au lieu d’exporter un contenu de type *Get-Process*, vous pouvez exporter uniquement les champs requis avec *Get-Process | Select ProcessName, CPU*.

## <a name="powershell-workflow-runbooks"></a>Runbooks de workflow PowerShell
Les Runbooks de workflow PowerShell sont des Runbooks texte basés sur un [workflow Windows PowerShell](automation-powershell-workflow.md).  Vous modifiez directement le code du Runbook à l'aide de l'éditeur de texte du portail Azure.  Vous pouvez également utiliser n'importe quel éditeur de texte hors ligne et [importer le Runbook](http://msdn.microsoft.com/library/azure/dn643637.aspx) dans Azure Automation.

### <a name="advantages"></a>Avantages
* Implémentez tout type de logique complexe avec le code de workflow PowerShell.
* Utilisez des [points de contrôle](automation-powershell-workflow.md#checkpoints) pour reprendre le Runbook en cas d'erreur.
* Utilisez un [traitement en parallèle](automation-powershell-workflow.md#parallel-processing) pour effectuer plusieurs actions en parallèle.
* Peut inclure d'autres Runbooks graphiques et Runbooks de workflow PowerShell en tant que Runbooks enfants afin de créer des workflows de haut niveau.

### <a name="limitations"></a>Limitations
* L’auteur doit être familiarisé avec les workflows PowerShell.
* Un Runbook doit pouvoir gérer la complexité supplémentaire liée au workflow PowerShell, notamment les [objets désérialisés](automation-powershell-workflow.md#code-changes).
* Un Runbook prend plus de temps à démarrer que les Runbooks PowerShell car il doit être compilé avant l'exécution.
* Les Runbooks PowerShell peuvent uniquement être inclus en tant que Runbooks enfants à l'aide de l'applet de commande Start-AzureAutomationRunbook qui crée une tâche.

## <a name="considerations"></a>Considérations
Vous devez prendre en compte les considérations supplémentaires suivantes pour déterminer le type à utiliser pour un Runbook donné.

* Vous ne pouvez pas convertir de Runbooks du type graphique au type textuel ou vice-versa.
* Il existe des limitations à l’utilisation de Runbooks de différents types comme un Runbook enfant.  Consultez la page [Runbooks enfants dans Azure Automation](automation-child-runbooks.md) pour plus d’informations.

## <a name="next-steps"></a>Étapes suivantes
* Pour en savoir plus sur la création de Runbooks graphiques, consultez [Création de graphiques dans Azure Automation](automation-graphical-authoring-intro.md)
* Pour comprendre les différences entre PowerShell et les workflows PowerShell pour les Runbooks, consultez [Apprentissage du workflow Windows PowerShell](automation-powershell-workflow.md)
* Pour en savoir plus sur la création ou l’importation d’un Runbook, consultez [Création ou importation d’un Runbook](automation-creating-importing-runbook.md)

