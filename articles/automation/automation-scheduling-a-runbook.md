---
title: aaaScheduling un runbook dans Azure Automation | Documents Microsoft
description: "Décrit comment toocreate une planification dans Azure Automation afin que vous pouvez automatiquement démarrer un runbook à un moment donné ou selon une planification périodique."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 710979ff-99d8-41e4-ac6d-6bf26b8ea654
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/09/2016
ms.author: bwren
ROBOTS: NOINDEX, NOFOLLOW
ms.openlocfilehash: c215b7ff6aa200466f3be566facba3c0cffcc924
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="scheduling-a-runbook-in-azure-automation"></a>Planification d'un Runbook dans Azure Automation
tooschedule un runbook dans toostart Azure Automation à une heure spécifiée, liez-le tooone ou plusieurs planifications. Une planification peut être configuré tooeither exécuter une seule fois ou selon une récurrence planification toutes les heures ou tous les jour pour les procédures opérationnelles Bonjour portail Azure classic et procédures opérationnelles Bonjour portail Azure, vous pouvez en outre planifier les jours d’utilisation hebdomadaire, mensuels, spécifiques de la semaine de hello ou les jours de Hello mois ou un jour spécifique du mois de hello.  Un runbook peut être lié toomultiple planifications, et une planification peut avoir plusieurs runbooks associés tooit.

## <a name="creating-a-schedule"></a>Création d'une planification
Vous pouvez créer une planification pour les procédures opérationnelles Bonjour portail Azure, dans le portail classique de hello, ou avec Windows PowerShell. Vous avez également option hello de création d’une nouvelle planification lorsque vous liez une planification de tooa runbook à l’aide de hello Azure classique ou le portail Azure.

> [!NOTE]
> Lorsque vous associez une planification à un runbook, Automation stocke les versions actuelles de hello des modules de hello dans votre compte et les lie toothat planification.  Cela signifie que si vous aviez un module avec la version 1.0 dans votre compte lorsque vous avez créé une planification, puis mettez à jour hello module tooversion 2.0, planification de hello continuera toouse 1.0.  Commande toouse hello module mis à jour la version, vous devez créer une nouvelle planification. 
> 
> 

### <a name="toocreate-a-new-schedule-in-hello-azure-classic-portal"></a>toocreate une nouvelle planification Bonjour portail Azure classic
1. Bonjour portail Azure classic, sélectionnez Automation puis puis nom hello d’un compte automation.
2. Sélectionnez hello **actifs** onglet.
3. Au bas de hello de fenêtre hello, cliquez sur **ajouter un paramètre**.
4. Cliquez sur **Ajouter une planification**.
5. Tapez un **nom** et éventuellement un **Description** pour schedule.your de nouveau hello planification s’exécutera **une fois**, **horaire**, **Quotidienne**, **hebdomadaire**, ou **mensuel**.
6. Spécifiez un **l’heure de début** et d’autres options en fonction de type hello de planification que vous avez sélectionné.

### <a name="toocreate-a-new-schedule-in-hello-azure-portal"></a>toocreate une nouvelle planification Bonjour portail Azure
1. Bonjour portail Azure, à partir de votre compte automation, cliquez sur hello **actifs** vignette tooopen hello **actifs** panneau.
2. Cliquez sur hello **planifications** vignette tooopen hello **planifications** panneau.
3. Cliquez sur **ajouter une planification** haut hello du Panneau de hello.
4. Sur hello **nouvelle planification** panneau, tapez un **nom** et éventuellement un **Description** de planification hello.
5. Sélectionnez si la planification de hello exécutera une seule fois, ou selon un calendrier récurrent en sélectionnant **une fois** ou **périodicité**.  Si vous sélectionnez **Une fois**, indiquez une **Heure de début**, puis cliquez sur **Créer**.  Si vous sélectionnez **périodicité**, spécifiez un **heure de début** et la fréquence de hello pour la fréquence à laquelle vous voulez par hello runbook toorepeat - **heure**, **jour**, **semaine**, ou par **mois**.  Si vous sélectionnez **semaine** ou **mois** à partir de la liste déroulante hello, hello **option de périodicité** s’affiche dans le panneau de hello et lors de la sélection, hello **périodicité option** panneau s’affiche et vous pouvez sélectionner le jour hello de semaine si vous avez sélectionné **semaine**.  Si vous avez sélectionné **mois**, vous pouvez choisir par **jours de la semaine** ou des jours spécifiques de mois hello hello calendrier et enfin, vous devez toorun sur hello dernier jour du mois de hello ou non, puis cliquez sur **OK** .   

### <a name="toocreate-a-new-schedule-with-windows-powershell"></a>toocreate une planification avec Windows PowerShell
Vous pouvez utiliser hello [New-AzureAutomationSchedule](http://msdn.microsoft.com/library/azure/dn690271.aspx) toocreate de l’applet de commande une planification dans Azure Automation pour les runbooks classiques, ou [New-AzureRmAutomationSchedule](https://msdn.microsoft.com/library/mt603577.aspx) applet de commande pour les procédures opérationnelles Bonjour Azure portail. Vous devez spécifier l’heure de début hello pour la planification de hello et fréquence hello qu'il doit s’exécuter.

Hello suivant des exemples de commandes montrent comment toocreate une planification qui s’exécute chaque jour à 3 h 30 commençant le 20 janvier 2015 avec une applet de commande de gestion des services Azure.

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-DailySchedule"
    New-AzureAutomationSchedule –AutomationAccountName $automationAccountName –Name `
    $scheduleName –StartTime "1/20/2016 15:30:00" –DayInterval 1

Hello exemple suivant commandes montre comment toocreate une planification pour hello 15 et 30 de chaque mois à l’aide d’une applet de commande Azure Resource Manager.

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-MonthlyDaysOfMonthSchedule"
    New-AzureRMAutomationSchedule –AutomationAccountName $automationAccountName –Name `
    $scheduleName -StartTime "7/01/2016 15:30:00" -MonthInterval 1 `
    -DaysOfMonth Fifteenth,Thirtieth -ResourceGroupName "ResourceGroup01"


## <a name="linking-a-schedule-tooa-runbook"></a>Liaison d’un runbook tooa de planification
Un runbook peut être lié toomultiple planifications, et une planification peut avoir plusieurs runbooks associés tooit. Si un Runbook possède des paramètres, vous pouvez leur fournir des valeurs. Vous devez fournir des valeurs pour tous les paramètres obligatoires et vous pouvez fournir des valeurs pour tous les paramètres facultatifs.  Ces valeurs seront utilisées chaque fois hello runbook est démarré par cette planification.  Vous pouvez attacher hello même runbook tooanother planification et de spécifier des valeurs de paramètre différentes.

### <a name="toolink-a-schedule-tooa-runbook-with-hello-azure-classic-portal"></a>toolink runbook tooa planification hello portail Azure classic
1. Bonjour portail Azure classic, sélectionnez **Automation** , puis cliquez sur nom hello d’un compte automation.
2. Sélectionnez hello **Runbooks** onglet.
3. Cliquez sur nom hello de hello runbook tooschedule.
4. Cliquez sur hello **planification** onglet.
5. Si hello runbook n’est pas actuellement lié tooa planification, puis vous pourrez hello trop**tooa nouvelle planification de lien** ou **lien tooan existant planification**.  Si hello runbook est actuellement lié tooa planification, cliquez sur **lien** à hello bas de hello fenêtre tooaccess ces options.
6. Si hello runbook possède des paramètres, le système vous demandera de leurs valeurs.  

### <a name="toolink-a-schedule-tooa-runbook-with-hello-azure-portal"></a>toolink runbook tooa planification hello portail Azure
1. Bonjour portail Azure, à partir de votre compte automation, cliquez sur hello **Runbooks** vignette tooopen hello **Runbooks** panneau.
2. Cliquez sur nom hello de hello runbook tooschedule.
3. Si hello runbook n’est pas actuellement lié tooa planification, puis vous être hello donné option toocreate une nouvelle planification ou lien tooan existant de planification.  
4. Si hello runbook possède des paramètres, vous pouvez sélectionner les option hello **modifier les paramètres d’exécution (par défaut : Azure)** et hello **paramètres** lame est présenté dans lequel vous pouvez entrer les informations de hello en conséquence.  

### <a name="toolink-a-schedule-tooa-runbook-with-windows-powershell"></a>toolink un runbook tooa de planification avec Windows PowerShell
Vous pouvez utiliser hello [Register-AzureAutomationScheduledRunbook](http://msdn.microsoft.com/library/azure/dn690265.aspx) toolink un runbook classique de planification tooa ou [Register-AzureRmAutomationScheduledRunbook](https://msdn.microsoft.com/library/mt603575.aspx) applet de commande pour les procédures opérationnelles Bonjour portail Azure.  Vous pouvez spécifier des valeurs pour les paramètres du runbook hello avec le paramètre paramètres hello. Pour plus d'informations sur la spécification des valeurs des paramètres, consultez [Démarrage d'un Runbook dans Azure Automation](automation-starting-a-runbook.md) .

exemple de Hello suivant commandes indiquent comment toolink une planification à l’aide d’une applet de commande de gestion des services Azure avec des paramètres.

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Test-Runbook"
    $scheduleName = "Sample-DailySchedule"
    $params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
    Register-AzureAutomationScheduledRunbook –AutomationAccountName $automationAccountName `
    –Name $runbookName –ScheduleName $scheduleName –Parameters $params

exemple de Hello suivant commandes indiquent comment toolink un runbook de tooa de planification à l’aide d’une applet de commande du Gestionnaire de ressources Azure avec des paramètres.

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Test-Runbook"
    $scheduleName = "Sample-DailySchedule"
    $params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
    Register-AzureRmAutomationScheduledRunbook –AutomationAccountName $automationAccountName `
    –Name $runbookName –ScheduleName $scheduleName –Parameters $params `
    -ResourceGroupName "ResourceGroup01"

## <a name="disabling-a-schedule"></a>Désactivation d'une planification
Lorsque vous désactivez une planification, n’importe quel tooit runbooks liés ne s’est plus sur cette planification. Vous pouvez désactiver manuellement une planification ou affecter un délai d’expiration aux planifications selon une certaine fréquence lors de leur création. Lorsque le délai d’expiration de hello est atteinte, la planification de hello sera désactivée.

### <a name="toodisable-a-schedule-from-hello-azure-classic-portal"></a>toodisable une planification à partir de hello portail Azure classic
Vous pouvez désactiver une planification Bonjour portail classique Azure à partir de la page de détails de la planification de hello pour la planification de hello.

1. Bonjour portail Azure classic, sélectionnez Automation et, puis cliquez sur nom hello d’un compte automation.
2. Sélectionnez l’onglet de ressources de hello.
3. Cliquez sur nom hello un tooopen planification sa page de détails.
4. Modification **activé** trop**non**.

### <a name="toodisable-a-schedule-from-hello-azure-portal"></a>toodisable une planification à partir de hello portail Azure
1. Bonjour portail Azure, à partir de votre compte automation, cliquez sur hello **actifs** vignette tooopen hello **actifs** panneau.
2. Cliquez sur hello **planifications** vignette tooopen hello **planifications** panneau.
3. Cliquez sur un panneau de détails de planification tooopen hello nom hello.
4. Modification **activé** trop**non**.

### <a name="toodisable-a-schedule-with-windows-powershell"></a>toodisable une planification avec Windows PowerShell
Vous pouvez utiliser hello [Set-AzureAutomationSchedule](http://msdn.microsoft.com/library/azure/dn690270.aspx) propriétés de hello toochange applet de commande d’une planification existante pour un runbook classique ou [Set-AzureRmAutomationSchedule](https://msdn.microsoft.com/library/mt603566.aspx) applet de commande pour les procédures opérationnelles Bonjour Azure portail. toodisable hello planifier, spécifiez **false** pour hello **IsEnabled** paramètre.

Hello suivant des exemples de commandes montrent comment une planification à l’aide de toodisable hello applet de commande de gestion des services Azure.

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-DailySchedule"
    Set-AzureAutomationSchedule –AutomationAccountName $automationAccountName `
    –Name $scheduleName –IsEnabled $false

exemple de Hello suivant commandes indiquent comment toodisable une planification pour un runbook à l’aide d’une applet de commande Azure Resource Manager.

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-MonthlyDaysOfMonthSchedule"
    Set-AzureRmAutomationSchedule –AutomationAccountName $automationAccountName `
    –Name $scheduleName –IsEnabled $false -ResourceGroupName "ResourceGroup01"


## <a name="next-steps"></a>Étapes suivantes
* toolearn en savoir plus sur l’utilisation des planifications, consultez [planification des ressources dans Azure Automation](http://msdn.microsoft.com/library/azure/dn940016.aspx)
* tooget a démarré avec des runbooks Azure Automation, consultez [démarrage d’un Runbook dans Azure Automation](automation-starting-a-runbook.md) 

