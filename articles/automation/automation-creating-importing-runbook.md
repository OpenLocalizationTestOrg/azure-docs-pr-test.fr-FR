---
title: "aaaCreating ou importation d’un runbook dans Azure Automation"
description: "Cet article décrit comment toocreate un runbook dans Azure Automation ou une importation à partir d’un fichier."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 24414362-b690-4474-8ca7-df18e30fc31d
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/07/2017
ms.author: magoedte;bwren
ms.openlocfilehash: d45f44cf15fbcacdd0de2977668502c2e1671063
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-or-importing-a-runbook-in-azure-automation"></a>Création ou importation d’un runbook dans Azure Automation
Vous pouvez ajouter un tooAzure de runbook Automation par le [créer un nouveau](#creating-a-new-runbook) ou en important un runbook existant à partir d’un fichier ou à partir de hello [galerie de runbooks](automation-runbook-gallery.md). Cet article fournit des informations sur la création et l’importation des runbooks à partir d’un fichier.  Vous pouvez obtenir tous les détails de hello sur l’accès aux runbooks de la Communauté et des modules dans [Runbook et module galeries pour Azure Automation](automation-runbook-gallery.md).

## <a name="creating-a-new-runbook"></a>Création d’un runbook
Vous pouvez créer un runbook dans Azure Automation à l’aide de hello Azure portails ou Windows PowerShell. Une fois hello runbook a été créé, vous pouvez le modifier à l’aide des informations contenues dans [Learning PowerShell Workflow](automation-powershell-workflow.md) et [de création graphique dans Azure Automation](automation-graphical-authoring-intro.md).

### <a name="toocreate-a-new-azure-automation-runbook-with-hello-azure-classic-portal"></a>toocreate un runbook Azure Automation avec le portail Azure Classic de hello
Vous pouvez travailler uniquement avec [les runbooks PowerShell Workflow](automation-runbook-types.md#powershell-workflow-runbooks) Bonjour portail Azure.

1. Dans le portail Azure Classic hello, cliquez sur, **nouveau**, **des Services d’application**, **Automation**, **Runbook**, **decréationrapide**.
2. Entrez les informations de hello requis, puis cliquez sur **créer**. nom du runbook Hello doit commencer par une lettre et peut avoir des lettres, des chiffres, des traits de soulignement et des tirets.
3. Si vous souhaitez tooedit hello runbook maintenant, puis cliquez sur **modifier le Runbook**. Sinon, cliquez sur **OK**.
4. Votre nouveau runbook apparaît sur hello **Runbooks** onglet.

### <a name="toocreate-a-new-azure-automation-runbook-with-hello-azure-portal"></a>toocreate un runbook Azure Automation avec hello portail Azure
1. Bonjour portail Azure, ouvrez votre compte Automation.
2. À partir de hello Hub, sélectionnez **Runbooks** liste de hello tooopen des runbooks.
3. Cliquez sur hello **ajouter un runbook** bouton, puis **créer un runbook**.
4. Tapez un **nom** pour hello runbook, puis sélectionnez ses [Type](automation-runbook-types.md). nom du runbook Hello doit commencer par une lettre et peut avoir des lettres, des chiffres, des traits de soulignement et des tirets.
5. Cliquez sur **créer** toocreate hello runbook et l’éditeur ouvert hello.

### <a name="toocreate-a-new-azure-automation-runbook-with-windows-powershell"></a>toocreate un runbook Azure Automation avec Windows PowerShell
Vous pouvez utiliser hello [New-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt619376.aspx) toocreate de l’applet de commande vide [runbook PowerShell Workflow](automation-runbook-types.md#powershell-workflow-runbooks). Vous pouvez soit spécifier hello **nom** paramètre toocreate un runbook vide que vous pouvez modifier ultérieurement, ou vous pouvez spécifier hello **chemin d’accès** paramètre tooimport un fichier de runbook. Hello **Type** paramètre doit être également inclus toospecify un des types de runbook hello quatre.

exemple de Hello suivant commandes indiquent comment toocreate un runbook vide.

    New-AzureRmAutomationRunbook -AutomationAccountName MyAccount `
    -Name NewRunbook -ResourceGroupName MyResourceGroup -Type PowerShell

## <a name="importing-a-runbook-from-a-file-into-azure-automation"></a>Importation d’un runbook à partir d’un fichier dans Azure Automation
Vous pouvez créer un runbook dans Azure Automation en important un script PowerShell, un workflow PowerShell (extension .ps1) ou un runbook graphique exporté (.graphrunbook).  Vous devez spécifier hello [type de runbook](automation-runbook-types.md) qui sera créé à partir de l’importation hello en hello compte suivant des considérations relatives à la.

* Un fichier .graphrunbook peut uniquement être importé dans un nouveau [runbook graphique](automation-runbook-types.md#graphical-runbooks), et les runbooks graphiques ne peuvent être créés qu’à partir d’un fichier .graphrunbook.
* Un fichier .ps1 contenant un workflow PowerShell peut uniquement être importé dans un [runbook de workflow PowerShell](automation-runbook-types.md#powershell-workflow-runbooks).  Si le fichier de hello contient plusieurs flux de travail PowerShell, importation de hello échoue. Vous devez enregistrer chaque fichier propre tooits de flux de travail et l’importer séparément.
* Un fichier .ps1 qui ne contient pas de flux de travail peut être importé dans un [Runbook PowerShell](automation-runbook-types.md#powershell-runbooks) ou un [Runbook de flux de travail PowerShell](automation-runbook-types.md#powershell-workflow-runbooks).  Si elle est importée dans un runbook PowerShell Workflow, il sera converti tooa le flux de travail et des commentaires seront inclus dans les runbook hello spécifiant hello les modifications qui ont été apportées.

### <a name="tooimport-a-runbook-from-a-file-with-hello-azure-classic-portal"></a>tooimport un runbook à partir d’un fichier avec le portail Azure Classic de hello
Vous pouvez utiliser hello suivant la procédure tooimport un fichier de script dans Azure Automation.  Notez que vous pouvez uniquement importer un fichier .ps1 dans un runbook de workflow PowerShell à l’aide de ce portail.  Vous devez utiliser hello portail Azure pour les autres types.

1. Dans le portail de gestion Azure hello, sélectionnez **Automation** , puis sélectionnez un compte Automation.
2. Cliquez sur **Importer**.
3. Cliquez sur **rechercher le fichier** et recherchez tooimport de fichier de script hello.
4. Si vous souhaitez tooedit hello runbook maintenant, puis cliquez sur **modifier le Runbook**. Sinon, cliquez sur OK.
5. Hello nouveau runbook apparaît sur hello **Runbooks** onglet hello compte Automation.
6. Vous devez [publier hello runbook](#publishing-a-runbook) avant de pouvoir l’exécuter.

### <a name="tooimport-a-runbook-from-a-file-with-hello-azure-portal"></a>tooimport un runbook à partir d’un fichier avec hello portail Azure
Vous pouvez utiliser hello suivant la procédure tooimport un fichier de script dans Azure Automation.  

> [!NOTE]
> Notez que vous pouvez importer uniquement un fichier .ps1 dans un runbook PowerShell Workflow à l’aide du portail de hello.
> 
> 

1. Bonjour portail Azure, ouvrez votre compte Automation.
2. À partir de hello Hub, sélectionnez **Runbooks** liste de hello tooopen des runbooks.
3. Cliquez sur hello **ajouter un runbook** bouton, puis **importation**.
4. Cliquez sur **fichier de Runbook** tooselect hello fichier tooimport
5. Si hello **nom** champ est activé, puis que vous avez hello option toochange il.  nom du runbook Hello doit commencer par une lettre et peut avoir des lettres, des chiffres, des traits de soulignement et des tirets.
6. Hello [runbook type](automation-runbook-types.md) sera sélectionné automatiquement, mais vous pouvez modifier le type de hello après avoir effectué les restrictions applicables de hello en compte. 
7. Hello nouveau runbook apparaît dans la liste hello des procédures opérationnelles pour hello compte Automation.
8. Vous devez [publier hello runbook](#publishing-a-runbook) avant de pouvoir l’exécuter.

> [!NOTE]
> Après avoir importé un runbook graphique ou runbook PowerShell workflow graphique, vous disposez hello option tooconvert toohello autre type voulu. Impossible de convertir tootextual.
> 
> 

### <a name="tooimport-a-runbook-from-a-script-file-with-windows-powershell"></a>tooimport un runbook à partir d’un fichier de script avec Windows PowerShell
Vous pouvez utiliser hello [Import-AzureRMAutomationRunbook](https://msdn.microsoft.com/library/mt603735.aspx) tooimport de l’applet de commande un fichier de script en tant que brouillon runbook PowerShell Workflow. Si un runbook hello existe déjà, importation de hello échouera, sauf si vous utilisez hello *-Force* paramètre. 

Hello suivant des exemples de commandes montrent comment tooimport un script de fichier dans un runbook.

    $automationAccountName =  "AutomationAccount"
    $runbookName = "Sample_TestRunbook"
    $scriptPath = "C:\Runbooks\Sample_TestRunbook.ps1"
    $RGName = "ResourceGroup"

    Import-AzureRMAutomationRunbook -Name $runbookName -Path $scriptPath `
    -ResourceGroupName $RGName -AutomationAccountName $automationAccountName `
    -Type PowerShellWorkflow 


## <a name="publishing-a-runbook"></a>Publication d’un runbook
Lorsque vous créez ou importez un runbook, vous devez le publier avant de pouvoir l’exécuter.  Dans Automation, chaque Runbook a un brouillon et une version publiée. Seule la version publiée hello est disponible toobe exécuter, et uniquement hello brouillon peut être modifiée. version publiée de Hello n’est pas affectée par n’importe quelle version de brouillon de toohello de modifications. Lorsque le brouillon hello doit être rendue disponible, publiez-la en remplacement hello publié version brouillon hello.

## <a name="toopublish-a-runbook-using-hello-azure-classic-portal"></a>toopublish un runbook à l’aide du portail Azure Classic de hello
1. Ouvrez hello runbook dans le portail Azure Classic de hello.
2. En haut de hello d’écran hello, cliquez sur **auteur**.
3. Au bas de hello d’écran hello, cliquez sur **publier** , puis **Oui** message de vérification toohello.

## <a name="toopublish-a-runbook-using-hello-azure-portal"></a>toopublish un runbook à l’aide de hello portail Azure
1. Ouvrez hello runbook Bonjour portail Azure.
2. Cliquez sur hello **modifier** bouton.
3. Cliquez sur hello **publier** bouton, puis **Oui** message de vérification toohello.

## <a name="toopublish-a-runbook-using-windows-powershell"></a>toopublish un runbook à l’aide de Windows PowerShell
Vous pouvez utiliser hello [AzureRmAutomationRunbook de publication](https://msdn.microsoft.com/library/mt603705.aspx) toopublish de l’applet de commande un runbook avec Windows PowerShell. exemple de Hello suivant commandes indiquent comment toopublish un exemple de runbook.

    $automationAccountName =  AutomationAccount"
    $runbookName = "Sample_TestRunbook"
    $RGName = "ResourceGroup"

    Publish-AzureRmAutomationRunbook -AutomationAccountName $automationAccountName `
    -Name $runbookName -ResourceGroupName $RGName


## <a name="next-steps"></a>Étapes suivantes
* toolearn sur la façon dont vous pouvez bénéficier de hello Runbook et de la galerie des modules PowerShell, consultez [Runbook et module galeries pour Azure Automation](automation-runbook-gallery.md)
* toolearn en savoir plus sur la modification des procédures opérationnelles PowerShell et les flux de travail PowerShell avec un éditeur de texte, consultez [modification textuelles runbooks dans Azure Automation](automation-edit-textual-runbook.md)
* toolearn savoir plus sur la création de runbook graphique, consultez [création graphique dans Azure Automation](automation-graphical-authoring-intro.md)

