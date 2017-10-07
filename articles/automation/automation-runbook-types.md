---
title: aaaAzure Types de Runbook Automation | Documents Microsoft
description: "Décrit les hello différents types de runbooks que vous pouvez utiliser dans Azure Automation et les considérations à prendre en compte lorsque vous déterminez le toouse de type. "
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
ms.openlocfilehash: c28aa57c77025764b16784372308a4ff2f596914
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-runbook-types"></a>Types de Runbooks Azure Automation
Azure Automation prend en charge quatre types de procédures opérationnelles sont brièvement décrits dans hello tableau suivant.  Hello sections ci-dessous fournissent des informations supplémentaires sur chaque type, y compris des considérations sur le toouse chaque.

| Type | Description |
|:--- |:--- |
| [Graphique](#graphical-runbooks) |Basé sur Windows PowerShell et créé et modifié entièrement dans l'éditeur graphique du portail Azure. |
| [Graphique workflow PowerShell](#graphical-runbooks) |Selon le flux de travail Windows PowerShell et éditeur graphique de hello créée et modifiée complètement dans le portail Azure. |
| [PowerShell](#powershell-runbooks) |Runbook texte basé sur le script Windows PowerShell. |
| [Workflow PowerShell](#powershell-workflow-runbooks) |Runbook texte basé sur le workflow Windows PowerShell. |

## <a name="graphical-runbooks"></a>Runbooks graphiques
[Graphique](automation-runbook-types.md#graphical-runbooks) et les runbooks graphiques PowerShell Workflow sont créés et modifiés avec l’éditeur graphique de hello Bonjour portail Azure.  Vous pouvez les exporter tooa fichier et les importer dans un autre compte automation, mais vous ne pouvez pas créer ou les modifier avec un autre outil.  Runbooks graphiques génèrent un code PowerShell, mais vous ne pouvez pas directement afficher ou modifier le code de hello. Runbooks graphiques ne peut pas être convertie tooone Hello [formats de texte](automation-runbook-types.md), ni ne pouvez un runbook texte être toographical converti au format. Runbooks graphiques peut être convertie tooGraphical les runbooks PowerShell Workflow pendant l’importation et vice versa.

### <a name="advantages"></a>Avantages
* Insertion visuelle/lien/configuration d’un modèle de création  
* Se concentrer sur la façon dont les données circulent dans les processus hello  
* Représentation visuelle des processus de gestion  
* Inclure d’autres procédures opérationnelles en tant qu’enfant runbooks toocreate élevée au niveau des flux de travail  
* Programmation modulaire favorisée  


### <a name="limitations"></a>Limitations
* Impossible de modifier le Runbook en dehors du portail Azure.
* Peut nécessiter une activité de Code contenant une logique complexe PowerShell code tooperform.
* Impossible d’afficher ou modifier directement le code hello PowerShell créé par le flux de travail graphique hello. Notez que vous pouvez afficher le code hello que vous créez dans toutes les activités de Code.

## <a name="powershell-runbooks"></a>Runbooks PowerShell
Les Runbooks PowerShell sont basés sur Windows PowerShell.  Vous modifiez directement le code hello du runbook hello à l’aide d’éditeur de texte hello dans hello portail Azure.  Vous pouvez également utiliser n’importe quel éditeur de texte en mode hors connexion et [importer hello runbook](http://msdn.microsoft.com/library/azure/dn643637.aspx) dans Azure Automation.

### <a name="advantages"></a>Avantages
* Implémenter toute logique complexe avec le code PowerShell sans des complications supplémentaires hello du flux de travail PowerShell. 
* Runbook démarre plus rapidement que les runbooks PowerShell Workflow, car il n’a pas besoin toobe compilé avant son exécution.

### <a name="limitations"></a>Limites
* Doit être familiarisé avec les scripts PowerShell.
* Impossible d’utiliser [le traitement parallèle](automation-powershell-workflow.md#parallel-processing) tooperform plusieurs actions en parallèle.
* Impossible d’utiliser [des points de contrôle](automation-powershell-workflow.md#checkpoints) runbook tooresume en cas d’erreur.
* Les runbooks PowerShell Workflow et des runbooks graphiques ne peuvent être inclus en tant que runbooks enfants à l’aide d’applet de commande Start-AzureAutomationRunbook de hello qui crée une tâche.

### <a name="known-issues"></a>Problèmes connus
Voici les problèmes connus actuels rencontrés avec les Runbooks PowerShell.

* Les Runbooks PowerShell ne peuvent pas récupérer une [ressource variable](automation-variables.md) non chiffrée avec une valeur null.
* Les runbooks PowerShell ne peut pas récupérer un [ressource de variable](automation-variables.md) avec  *~*  dans le nom de hello.
* Get-Process dans une boucle d’un Runbook PowerShell peut se bloquer après environ 80 itérations. 
* Un runbook PowerShell risque d’échouer si elle tente de toowrite une très grande quantité de données toohello du flux de sortie à la fois.   Vous pouvez généralement contourner ce problème en affichant uniquement les informations de hello que vous avez besoin lorsque vous travaillez avec des objets volumineux.  Par exemple, au lieu de quelque chose comme sortie *Get-Process*, vous pouvez exporter uniquement les champs hello requis avec *Get-Process | Sélectionnez ProcessName, processeur*.

## <a name="powershell-workflow-runbooks"></a>Runbooks de workflow PowerShell
Les Runbooks de workflow PowerShell sont des Runbooks texte basés sur un [workflow Windows PowerShell](automation-powershell-workflow.md).  Vous modifiez directement le code hello du runbook hello à l’aide d’éditeur de texte hello dans hello portail Azure.  Vous pouvez également utiliser n’importe quel éditeur de texte en mode hors connexion et [importer hello runbook](http://msdn.microsoft.com/library/azure/dn643637.aspx) dans Azure Automation.

### <a name="advantages"></a>Avantages
* Implémentez tout type de logique complexe avec le code de workflow PowerShell.
* Utilisez [des points de contrôle](automation-powershell-workflow.md#checkpoints) runbook tooresume en cas d’erreur.
* Utilisez [le traitement parallèle](automation-powershell-workflow.md#parallel-processing) tooperform plusieurs actions en parallèle.
* Incluent d’autres runbooks graphiques et les runbooks PowerShell Workflow en tant qu’enfant runbooks toocreate élevée au niveau des flux de travail.

### <a name="limitations"></a>Limites
* L’auteur doit être familiarisé avec les workflows PowerShell.
* Runbook doit faire face à une complexité supplémentaire de flux de travail PowerShell hello comme [désérialiser des objets](automation-powershell-workflow.md#code-changes).
* Runbook prend toostart plus de temps que le runbook PowerShell puisqu’elle doit toobe compilé avant son exécution.
* Les runbooks PowerShell ne peuvent être inclus en tant que runbooks enfants à l’aide d’applet de commande Start-AzureAutomationRunbook de hello qui crée une tâche.

## <a name="considerations"></a>Considérations
Vous devez prendre en hello compte suivant des considérations supplémentaires pour déterminer quels toouse de type d’un runbook donné.

* Impossible de convertir des procédures opérationnelles de type de graphique tootextual ou vice versa.
* Il existe des limitations à l’utilisation de Runbooks de différents types comme un Runbook enfant.  Consultez la page [Runbooks enfants dans Azure Automation](automation-child-runbooks.md) pour plus d’informations.

## <a name="next-steps"></a>Étapes suivantes
* toolearn savoir plus sur la création de runbook graphique, consultez [création graphique dans Azure Automation](automation-graphical-authoring-intro.md)
* toounderstand hello différences des flux de travail de runbook PowerShell et PowerShell, consultez [Learning Windows PowerShell Workflow](automation-powershell-workflow.md)
* Pour plus d’informations sur la façon dont toocreate ou importer un Runbook, consultez [création ou importation d’un Runbook](automation-creating-importing-runbook.md)

