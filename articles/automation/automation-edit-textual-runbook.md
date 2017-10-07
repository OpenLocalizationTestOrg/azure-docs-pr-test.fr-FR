---
title: aaaEditing des runbooks textuelle dans Azure Automation
description: "Cet article fournit des procédures différentes pour travailler avec PowerShell et les flux de travail PowerShell runbooks dans Azure Automation à l’aide de l’éditeur textuel hello."
services: automation
documentationcenter: 
author: mgoedtel
manager: stevenka
editor: tysonn
ms.assetid: 6f5b48fb-6f30-4e99-9e14-9061b5554b08
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2016
ms.author: magoedte;bwren
ms.openlocfilehash: 3fd87d457838f300ca6c94bc345e82c679a0e011
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="editing-textual-runbooks-in-azure-automation"></a>Modifier des runbooks textuels dans Azure Automation
Hello éditeur textuel dans Azure Automation peut être utilisé tooedit [runbook PowerShell](automation-runbook-types.md#powershell-runbooks) et [les runbooks PowerShell Workflow](automation-runbook-types.md#powershell-workflow-runbooks). Cela a répertorie les principales fonctions de hello d’autres éditeurs de code comme intellisense et le codage en couleurs avec des fonctionnalités spéciales supplémentaires tooassist vous lors de l’accès toorunbooks courants de ressources.  Cet article fournit des instructions détaillées pour effectuer différentes fonctions avec cet éditeur.

éditeur de texte Hello inclut un code de tooinsert de fonctionnalité pour les activités, les ressources et les runbooks enfants dans un runbook. Au lieu de taper dans le code hello vous-même, vous pouvez sélectionner dans la liste des ressources disponibles et hello insérer dans les runbook hello de code approprié.

Dans Azure Automation, chaque runbook existe en deux versions : un brouillon et une version publiée. Vous modifiez hello brouillon du runbook de hello et publiez celui-ci pour pouvoir être exécuté. Impossible de modifier la version publiée de Hello. Consultez [Publication d’un runbook](automation-creating-importing-runbook.md#publishing-a-runbook) pour plus d’informations.

toowork avec [Runbooks graphiques](automation-runbook-types.md#graphical-runbooks), consultez [de création graphique dans Azure Automation](automation-graphical-authoring-intro.md).

## <a name="tooedit-a-runbook-with-hello-azure-portal"></a>tooedit un runbook avec hello portail Azure
Utilisez hello suivant la procédure tooopen un runbook pour la modification dans l’éditeur de texte hello.

1. Bonjour portail Azure, sélectionnez votre compte automation.
2. Cliquez sur hello **Runbooks** vignette tooopen hello liste des runbooks.
3. Cliquez sur le nom de hello de hello runbook vous souhaitez tooedit, puis cliquez sur hello **modifier** bouton.
4. Effectuer hello requis de modification.
5. Cliquez sur **Enregistrer** lorsque vos modifications sont terminées.
6. Cliquez sur **publier** si vous souhaitez hello dernière version de hello runbook toobe est publié.

### <a name="tooinsert-a-cmdlet-into-a-runbook"></a>tooinsert une applet de commande dans un runbook
1. Hello canevas de l’éditeur de texte hello, positionnez hello curseur où vous souhaitez tooplace hello applet de commande.
2. Développez hello **applets de commande** nœud Bonjour contrôle de la bibliothèque.
3. Développez le module hello contenant l’applet de commande hello souhaité toouse.
4. Cliquez avec le bouton droit sur tooinsert d’applet de commande hello et sélectionnez **ajouter toocanvas**.  Si l’applet de commande hello possède plusieurs paramètres définie, ensemble par défaut de hello est ajouté.  Vous pouvez également développer tooselect d’applet de commande hello un autre paramètre défini.
5. le code Hello pour l’applet de commande hello est inséré avec son intégralité de la liste de paramètres.
6. Indiquez la valeur appropriée à la place du type de données hello entouré d’accolades les <> pour tous les paramètres requis.  Supprimez les paramètres dont vous n’avez pas besoin.

### <a name="tooinsert-code-for-a-child-runbook-into-a-runbook"></a>code tooinsert d’un runbook enfant dans un runbook
1. Hello canevas de l’éditeur de texte hello, positionnez hello curseur où vous voulez obtenir tooplace hello code hello [runbook enfant](automation-child-runbooks.md).
2. Développez hello **Runbooks** nœud Bonjour contrôle de la bibliothèque.
3. Cliquez avec le bouton droit sur hello runbook tooinsert et sélectionnez **ajouter toocanvas**.
4. le code Hello pour le runbook enfant hello est inséré avec des espaces réservés pour tous les paramètres du runbook.
5. Remplacez les espaces réservés de hello avec les valeurs appropriées pour chaque paramètre.

### <a name="tooinsert-an-asset-into-a-runbook"></a>tooinsert un élément multimédia dans un runbook
1. Hello canevas de l’éditeur de texte hello, positionnez hello curseur où vous voulez obtenir tooplace hello code hello enfant runbook.
2. Développez hello **actifs** nœud Bonjour contrôle de la bibliothèque.
3. Développez le nœud hello type hello d’élément.
4. Cliquez avec le bouton droit sur hello asset tooinsert et sélectionnez **ajouter toocanvas**.  Pour [actifs variables](automation-variables.md), sélectionnez **ajouter « Obtenir la Variable » toocanvas** ou **ajouter « Définir la Variable » toocanvas** selon que vous souhaitez tooget ou définir la variable de hello.
5. Insérer un code Hello pour un composant de hello dans les runbook hello.

## <a name="tooedit-a-runbook-with-hello-azure-portal"></a>tooedit un runbook avec hello portail Azure
Utilisez hello suivant la procédure tooopen un runbook pour la modification dans l’éditeur de texte hello.

1. Bonjour portail Azure, sélectionnez **Automation** , puis cliquez sur nom hello d’un compte automation.
2. Sélectionnez hello **Runbooks** onglet.
3. Cliquez sur le nom de hello de hello runbook vous souhaitez tooedit, puis sélectionnez hello **auteur** onglet.
4. Cliquez sur hello **modifier** bouton bas hello écran hello.
5. Effectuer hello requis de modification.
6. Cliquez sur **Enregistrer** lorsque vos modifications sont terminées.
7. Cliquez sur **publier** si vous souhaitez hello dernière version de hello runbook toobe est publié.

### <a name="tooinsert-an-activity-into-a-runbook"></a>tooinsert une activité dans un Runbook
1. Hello canevas de l’éditeur de texte hello, positionnez hello curseur où vous souhaitez que l’activité de hello tooplace.
2. Au bas de hello d’écran hello, cliquez sur **insérer** , puis **activité**.
3. Bonjour **Module d’intégration** module hello select qui contient l’activité hello, de la colonne.
4. Bonjour **activité** volet, sélectionnez une activité.
5. Bonjour **Description** colonne, la description de hello Remarque d’activité hello. Si vous le souhaitez, vous pouvez cliquer sur vue détaillée de l’aide de toolaunch aide pour l’activité hello dans le navigateur de hello.
6. Cliquez sur droite hello.  Si l’activité hello possède des paramètres, ils seront répertoriés pour votre information.
7. Cliquez sur le bouton de vérification hello.  Activité de code toorun hello sera insérée dans les runbook hello.
8. Si l’activité hello requiert des paramètres, indiquez la valeur appropriée à la place du type de données hello entouré d’accolades <>.

### <a name="tooinsert-code-for-a-child-runbook-into-a-runbook"></a>code tooinsert d’un runbook enfant dans un runbook
1. Hello canevas de l’éditeur de texte hello, positionnez hello curseur où vous souhaitez tooplace hello [runbook enfant](automation-child-runbooks.md).
2. Au bas de hello d’écran hello, cliquez sur **insérer** , puis **Runbook**.
3. Sélectionnez hello runbook tooinsert à partir de la colonne du milieu hello et cliquez sur la flèche vers la droite hello.
4. Si hello runbook possède des paramètres, ils seront répertoriés pour votre information.
5. Cliquez sur le bouton de vérification hello.  Code toorun hello sélectionné runbook sera insérée dans les runbook en cours hello.
6. Si hello runbook requiert des paramètres, indiquez la valeur appropriée à la place du type de données hello entouré d’accolades <>.

### <a name="tooinsert-an-asset-into-a-runbook"></a>tooinsert un élément multimédia dans un runbook
1. Hello canevas de l’éditeur de texte hello, positionnez hello curseur où vous souhaitez que le tooplace hello activité tooretrieve hello immobilisation.
2. Au bas de hello d’écran hello, cliquez sur **insérer** , puis **paramètre**.
3. Bonjour **Action de paramètre** action Sélectionnez hello souhaitée, la colonne.
4. Sélectionnez parmi les ressources disponibles hello dans la colonne du milieu hello.
5. Cliquez sur le bouton de vérification hello.  Tooget de code ou ensemble hello actif sera insérée dans les runbook hello.

## <a name="tooedit-an-azure-automation-runbook-using-windows-powershell"></a>tooedit un runbook Azure Automation à l’aide de Windows PowerShell
tooedit un runbook avec Windows PowerShell, vous utilisez l’éditeur de hello de votre choix et l’enregistrer fichier .ps1 de tooa. Vous pouvez utiliser hello [Get-AzureAutomationRunbookDefinition](http://aka.ms/runbookauthor/cmdlet/getazurerunbookdefinition) contenu de hello tooretrieve applet de commande de hello runbook, puis [Set-AzureAutomationRunbookDefinition](http://aka.ms/runbookauthor/cmdlet/setazurerunbookdefinition) applet de commande tooreplace hello existant brouillon de runbook avec hello modifiés un.

### <a name="tooretrieve-hello-contents-of-a-runbook-using-windows-powershell"></a>tooRetrieve hello le contenu d’un Runbook à l’aide de Windows PowerShell
Hello suivant des exemples de commandes montrent comment tooretrieve hello script d’un runbook et enregistrer le fichier de script tooa. Dans cet exemple, brouillon hello est récupéré. Il s’agit également tooretrieve possible hello publié version hello runbook bien que cette version ne peut pas être modifiée.

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Sample-TestRunbook"
    $scriptPath = "c:\runbooks\Sample-TestRunbook.ps1"

    $runbookDefinition = Get-AzureAutomationRunbookDefinition -AutomationAccountName $automationAccountName -Name $runbookName -Slot Draft
    $runbookContent = $runbookDefinition.Content

    Out-File -InputObject $runbookContent -FilePath $scriptPath

### <a name="toochange-hello-contents-of-a-runbook-using-windows-powershell"></a>tooChange hello le contenu d’un Runbook à l’aide de Windows PowerShell
Hello exemples de commandes suivants montrent comment tooreplace hello contenu existant d’un runbook avec hello d’un fichier de script. Notez que cela est hello même exemple de procédure, comme dans [tooimport un runbook à partir d’un fichier de script avec Windows PowerShell](automation-creating-importing-runbook.md).

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Sample-TestRunbook"
    $scriptPath = "c:\runbooks\Sample-TestRunbook.ps1"

    Set-AzureAutomationRunbookDefinition -AutomationAccountName $automationAccountName -Name $runbookName -Path $scriptPath -Overwrite
    Publish-AzureAutomationRunbook –AutomationAccountName $automationAccountName –Name $runbookName

## <a name="related-articles"></a>Articles connexes
* [Création ou importation d’un runbook dans Azure Automation](automation-creating-importing-runbook.md)
* [Apprentissage du workflow PowerShell](automation-powershell-workflow.md)
* [Création de graphiques dans Azure Automation](automation-graphical-authoring-intro.md)
* [Certificats](automation-certificates.md)
* [Connexions](automation-connections.md)
* [Informations d'identification](automation-credentials.md)
* [Planifications](automation-schedules.md)
* [Variables](automation-variables.md)
