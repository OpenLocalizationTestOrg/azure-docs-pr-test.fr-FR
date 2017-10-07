---
title: aaaTesting un runbook dans Azure Automation | Documents Microsoft
description: "Avant de publier un runbook dans Azure Automation, vous pouvez le tester tooensure fonctionne comme prévu.  Cet article décrit comment tootest un runbook et afficher sa sortie."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 7f7db785-52c0-4613-aa12-b02fd32a5182
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/12/2016
ms.author: magoedte;bwren
ms.openlocfilehash: 8c531f702699d586f8215d4c171cb0ecf94732b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="testing-a-runbook-in-azure-automation"></a>Test d’un runbook dans Azure Automation
Lorsque vous testez un runbook, hello [brouillon](automation-creating-importing-runbook.md#publishing-a-runbook) est exécutée et la fin de toutes les actions qu’il effectue. Aucun historique des travaux ne sont créée, mais hello [sortie](automation-runbook-output-and-messages.md#output-stream) et [avertissement et erreur](automation-runbook-output-and-messages.md#message-streams) flux sont affichés dans hello Test volet de sortie. Messages toohello [flux détaillé](automation-runbook-output-and-messages.md#message-streams) s’affichent dans le volet de sortie de hello uniquement si hello [$VerbosePreference variable](automation-runbook-output-and-messages.md#preference-variables) a la valeur tooContinue.

Bien que brouillon hello est en cours d’exécution, hello runbook toujours exécute normalement les flux de travail hello et effectue les actions relatives aux ressources dans un environnement de hello. Pour cette raison, vous devez tester les runbooks uniquement sur des ressources hors production.

Hello procédure tootest chaque [type de runbook](automation-runbook-types.md) est hello identiques, et il n’existe aucune différence dans le test entre l’éditeur graphique de hello Bonjour portail Azure et l’éditeur de texte hello.  

## <a name="tootest-a-runbook-in-hello-azure-portal"></a>tootest un runbook dans hello portail Azure
Vous pouvez travailler avec n’importe quelle [runbook type](automation-runbook-types.md) Bonjour portail Azure.

1. Ouvrez hello brouillon du runbook hello soit Bonjour [éditeur de texte](automation-edit-textual-runbook.md) ou [éditeur graphique](automation-graphical-authoring-intro.md).
2. Cliquez sur hello **Test** Panneau de Test bouton tooopen hello.
3. Si hello runbook possède des paramètres, ils seront afficheront dans le volet de gauche hello où vous pouvez fournir toobe de valeurs utilisée pour le test de hello.
4. Si vous souhaitez que les tests de hello toorun sur un [Runbook Worker hybride](automation-hybrid-runbook-worker.md), puis modifiez **paramètres d’exécution** trop**Worker hybride** et le nom de select hello du groupe cible de hello.  Sinon, conservez la valeur par défaut hello **Azure** test de hello toorun dans le cloud de hello.
5. Cliquez sur hello **Démarrer** test de bouton toostart hello.
6. Si le runbook hello est [PowerShell Workflow](automation-runbook-types.md#powershell-workflow-runbooks) ou [Graphical](automation-runbook-types.md#graphical-runbooks), vous pouvez arrêter ou suspendre pendant est testée avec les boutons hello sous hello volet sortie. Lorsque vous interrompez hello runbook, il termine l’activité en cours hello avant de s’interrompre. Une fois hello runbook est interrompu, vous pouvez l’arrêter ou le redémarrer.
7. Inspectez la sortie hello runbook hello dans le volet de sortie hello.

## <a name="next-steps"></a>Étapes suivantes
* toolearn comment toocreate ou importer un runbook, consultez [création ou importation d’un runbook dans Azure Automation](automation-creating-importing-runbook.md)
* toolearn plus sur la création de graphiques, consultez [création graphique dans Azure Automation](automation-graphical-authoring-intro.md)
* tooget a démarré avec des runbooks de flux de travail PowerShell, consultez [mon premier runbook de flux de travail PowerShell](automation-first-runbook-textual.md)
* toolearn plus sur la configuration des messages d’état runboks tooreturn et les erreurs, y compris les pratiques recommandées, consultez [Runbook sortie et les messages dans Azure Automation](automation-runbook-output-and-messages.md)

