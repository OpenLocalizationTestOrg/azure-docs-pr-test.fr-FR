---
title: "les paramètres aaaRunbook | Documents Microsoft"
description: "Décrit les paramètres de configuration hello pour un runbook dans Azure Automation et comment toochange à l’aide des deux hello portail de gestion Azure et Windows PowerShell."
services: automation
documentationcenter: 
author: mgoedtel
manager: stevenka
editor: tysonn
ms.assetid: a726f20c-a952-48b8-88ee-36d76aa3ac61
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/11/2016
ms.author: bwren
ms.openlocfilehash: 6f0ef09c148355a351464424c22c33df9300f0dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="runbook-settings"></a>Paramètres du Runbook
Chaque runbook dans Azure Automation a plusieurs paramètres que vous toobe identifié et toochange son comportement de journalisation. Chacun de ces paramètres est décrite ci-dessous, suivie des procédures sur la façon de toomodify les.

## <a name="settings"></a>Paramètres
### <a name="name-and-description"></a>Nom et description
Vous ne pouvez pas modifier le nom hello d’un runbook une fois qu’elle a été créée. Hello Description est facultative et peut être des caractères de too512.

### <a name="tags"></a>Tags
Autoriser les balises que vous tooassign des mots distincts et expressions toohelp identifient un runbook. Par exemple, lorsque vous envoyez un toohello runbook [PowerShell Gallery](https://www.powershellgallery.com/), vous spécifiez tooidentify certaines balises les catégories hello runbook doit être indiquée dans. Vous pouvez spécifier plusieurs balises pour un Runbook en les séparant par des virgules.

### <a name="logging"></a>Journalisation
Par défaut, les enregistrements détaillés et de progression ne sont pas écrites toojob historique. Vous pouvez modifier les paramètres de hello pour un runbook donné de toolog de ces enregistrements. Pour en savoir plus sur ces informations, consultez [Sortie et messages de runbook](automation-runbook-output-and-messages.md).

## <a name="changing-runbook-settings"></a>Modification des paramètres du Runbook

### <a name="changing-runbook-settings-with-hello-azure-portal"></a>Modification des paramètres de runbook avec hello portail Azure
Vous pouvez modifier les paramètres d’un runbook Bonjour portail Azure à partir de hello **paramètres** panneau hello runbook.

1. Bonjour portail Azure, sélectionnez **Automation** , puis cliquez sur nom hello d’un compte automation.
2. Sélectionnez hello **Runbooks** onglet.
3. Cliquez sur le nom hello d’un runbook et que vous êtes dirigé toohello panneau des paramètres pour hello runbook. À partir d’ici vous pouvez spécifier ou modifier des balises, hello description de runbook, configurer la journalisation et le suivi des paramètres et toohelp d’outils de prise en charge de résoudre les problèmes d’accès.     

### <a name="changing-runbook-settings-with-windows-powershell"></a>Modification des paramètres du Runbook avec Windows PowerShell
Vous pouvez utiliser hello [Set-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603786.aspx) paramètres de hello toochange applet de commande d’un runbook. Si vous souhaitez toospecify plusieurs balises, vous pouvez fournir un tableau ou une chaîne unique avec le paramètre délimité par des virgules valeurs toohello balises. Vous pouvez obtenir des balises actives de hello avec hello [Get-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603728.aspx).

Hello suivant des exemples de commandes montrent comment tooset hello les propriétés d’un runbook. Cet exemple ajoute trois balises toohello les balises et spécifie que les enregistrements détaillés doivent être enregistrés.

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Sample-TestRunbook"
    $tags = (Get-AzureRmAutomationRunbook -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName $automationAccountName –Name $runbookName).Tags
    $tags += "Tag1,Tag2,Tag3"
    Set-AzureRmAutomationRunbook -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName $automationAccountName –Name $runbookName –LogVerbose $true –Tags $tags

## <a name="next-steps"></a>Étapes suivantes
* toolearn comment les messages de sortie et d’erreur toocreate et récupérer à partir de procédures opérationnelles, consultez [Runbook Output and Messages](automation-runbook-output-and-messages.md) 
* toounderstand tooadd un runbook a été développée par la Communauté de hello ou d’autres sources ou toocreate vos propres runbook voir [création ou importation d’un Runbook](automation-creating-importing-runbook.md) 

