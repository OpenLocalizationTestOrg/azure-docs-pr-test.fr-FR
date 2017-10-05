---
title: "Planification d’un Runbook dans Azure Automation | Microsoft Docs"
description: "Décrit comment créer une planification dans Azure Automation afin de pouvoir démarrer automatiquement un Runbook à un instant donné ou selon une planification périodique."
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
ms.openlocfilehash: 52f1d55f141bb1b3948e3b7039cfc131a5e407b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="scheduling-a-runbook-in-azure-automation"></a>Planification d'un Runbook dans Azure Automation
Pour planifier le démarrage d'un Runbook dans Azure Automation à une heure spécifiée, liez-le à une ou plusieurs planifications. Vous pouvez configurer une planification de Runbooks dans le portail Azure Classic et dans le portail Azure pour qu’elle s’exécute une seule fois ou selon un calendrier horaire ou quotidien récurrent. Vous pouvez également planifier une exécution hebdomadaire ou mensuelle, ou encore qui interviendra certains jours de la semaine, certains jours du mois ou un jour spécifique du mois.  Un Runbook peut être lié à plusieurs planifications et une planification peut avoir plusieurs Runbooks qui lui sont liés.

## <a name="creating-a-schedule"></a>Création d'une planification
Vous pouvez utiliser le portail Azure, le portail Azure Classic ou Windows PowerShell pour créer une planification de Runbooks. Vous avez également la possibilité de créer une planification lorsque vous liez un Runbook à une planification à l’aide du portail Azure Classic ou du portail Azure.

> [!NOTE]
> Lorsque vous associez une planification à un Runbook, Automation stocke les versions actuelles des modules dans votre compte et les lie à cette planification.  Cela signifie que si vous aviez un module version 1.0 dans votre compte lorsque vous avez créé une planification puis mis à jour ce module vers la version 2.0, la planification continueront d’utiliser la version 1.0.  Pour utiliser la version mise à jour du module, vous devez créer une nouvelle planification. 
> 
> 

### <a name="to-create-a-new-schedule-in-the-azure-classic-portal"></a>Pour créer une planification à l’aide du portail Azure Classic
1. Dans le portail Azure Classic, sélectionnez Automation, puis sélectionnez le nom d’un compte Automation.
2. Sélectionnez l'onglet **Ressources** .
3. En bas de la fenêtre, cliquez sur **Ajouter un paramètre**.
4. Cliquez sur **Ajouter une planification**.
5. Tapez un **Nom** et éventuellement une **Description** pour votre planification, qui s’exécutera **Une fois**, **Toutes les heures**, **Tous les jours**, **Toutes les semaines** ou **Tous les mois**.
6. Spécifiez une **Heure de début** et d'autres options en fonction du type de planification que vous avez sélectionné.

### <a name="to-create-a-new-schedule-in-the-azure-portal"></a>Pour créer une planification à l’aide du portail Azure
1. Dans le portail Azure, à partir de votre compte Automation, cliquez sur la mosaïque **Ressources** afin d’ouvrir le panneau **Ressources**.
2. Cliquez sur la mosaïque **Planifications** pour ouvrir le panneau **Planifications**.
3. Cliquez sur **Ajouter une planification** en haut du panneau.
4. Dans le panneau **Nouvelle planification**, tapez un **Nom** et éventuellement une **Description** pour la nouvelle planification.
5. Indiquez si la planification doit s’exécuter une seule fois ou selon un calendrier récurrent en sélectionnant **Une fois** ou **Périodicité**.  Si vous sélectionnez **Une fois**, indiquez une **Heure de début**, puis cliquez sur **Créer**.  Si vous sélectionnez **Périodicité**, spécifiez une **Heure de début** et indiquez la fréquence à laquelle vous souhaitez répéter le Runbook : par **heure**, par **jour**, par **semaine** ou par **mois**.  Si vous sélectionnez **semaine** ou **mois** dans la liste déroulante, l’option **Périodicité** apparaît dans le panneau. Sélectionnez cette option pour accéder au panneau d’options **Périodicité** et sélectionner le jour de semaine si vous avez sélectionné **semaine**.  Si vous avez sélectionné **mois**, vous pouvez choisir par **jours de la semaine** ou spécifier des jours précis du mois dans le calendrier. Pour finir, indiquez si vous souhaitez ou non exécuter le Runbook le dernier jour du mois, puis cliquez sur **OK**.   

### <a name="to-create-a-new-schedule-with-windows-powershell"></a>Pour créer une planification avec Windows PowerShell
Vous pouvez utiliser l’applet de commande [New-AzureAutomationSchedule](http://msdn.microsoft.com/library/azure/dn690271.aspx) pour créer une planification dans Azure Automation pour les Runbooks classiques, ou utiliser l’applet de commande [New-AzureRmAutomationSchedule](https://msdn.microsoft.com/library/mt603577.aspx) pour les Runbooks exécutés dans le portail Azure. Vous devez spécifier l’heure de début de la planification et indiquer sa fréquence d’exécution.

Les exemples de commandes suivants montrent comment créer une planification qui s'exécute chaque jour à 15h30 à partir du 20 janvier 2015, à l’aide d’une applet de commande Azure Service Management.

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-DailySchedule"
    New-AzureAutomationSchedule –AutomationAccountName $automationAccountName –Name `
    $scheduleName –StartTime "1/20/2016 15:30:00" –DayInterval 1

Les exemples de commandes suivant montrent comment créer une planification le 15 et le 30 de chaque mois à l’aide d’une applet de commande Azure Resource Manager.

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-MonthlyDaysOfMonthSchedule"
    New-AzureRMAutomationSchedule –AutomationAccountName $automationAccountName –Name `
    $scheduleName -StartTime "7/01/2016 15:30:00" -MonthInterval 1 `
    -DaysOfMonth Fifteenth,Thirtieth -ResourceGroupName "ResourceGroup01"


## <a name="linking-a-schedule-to-a-runbook"></a>Liaison d'une planification à un Runbook
Un Runbook peut être lié à plusieurs planifications et une planification peut avoir plusieurs Runbooks qui lui sont liés. Si un Runbook possède des paramètres, vous pouvez leur fournir des valeurs. Vous devez fournir des valeurs pour tous les paramètres obligatoires et vous pouvez fournir des valeurs pour tous les paramètres facultatifs.  Ces valeurs seront utilisées à chaque démarrage du Runbook par cette planification.  Vous pouvez attacher le même Runbook à une autre planification et spécifier différentes valeurs de paramètre.

### <a name="to-link-a-schedule-to-a-runbook-with-the-azure-classic-portal"></a>Pour lier une planification à un Runbook avec le portail Azure Classic
1. Dans le portail Azure Classic, sélectionnez **Automation** , puis cliquez sur le nom d’un compte Automation.
2. Sélectionnez l'onglet **Runbooks** .
3. Cliquez sur le nom du Runbook à planifier.
4. Cliquez sur l'onglet **Planification** .
5. Si le Runbook n’est pas lié à une planification, vous avez la possibilité de le **Lier à une nouvelle planification** ou de le **Lier à une planification existante**.  Si le Runbook n'est lié à une planification, cliquez sur **Lien** en bas de la fenêtre pour accéder à ces options.
6. Si le Runbook possède des paramètres, le système vous demande d'entrer leurs valeurs.  

### <a name="to-link-a-schedule-to-a-runbook-with-the-azure-portal"></a>Pour lier une planification à un Runbook avec le portail Azure
1. Dans le portail Azure, à partir de votre compte Automation, cliquez sur la mosaïque **Runbooks** afin d’ouvrir le panneau **Runbooks**.
2. Cliquez sur le nom du Runbook à planifier.
3. Si le Runbook n'est pas actuellement lié à une planification, vous avez la possibilité de créer une planification ou de le lier à une planification existante.  
4. Si le Runbook possède des paramètres, vous pouvez sélectionner l’option **Modifier les paramètres d’exécution (par défaut : Azure)** pour accéder au panneau **Paramètres**, dans lequel vous pourrez saisir les informations correspondantes.  

### <a name="to-link-a-schedule-to-a-runbook-with-windows-powershell"></a>Pour lier une planification à un Runbook avec Windows PowerShell
Vous pouvez utiliser l’applet de commande [Register-AzureAutomationScheduledRunbook](http://msdn.microsoft.com/library/azure/dn690265.aspx) pour lier une planification à un Runbook classique ou l’applet de commande [Register-AzureRmAutomationScheduledRunbook](https://msdn.microsoft.com/library/mt603575.aspx) dans le cas des Runbooks exécutés dans le portail Azure.  Vous pouvez spécifier les valeurs des paramètres du Runbook avec le paramètre Parameters. Pour plus d'informations sur la spécification des valeurs des paramètres, consultez [Démarrage d'un Runbook dans Azure Automation](automation-starting-a-runbook.md) .

Les exemples de commandes suivants montrent comment lier une planification à l’aide d’une applet de commande Azure Service Management avec des paramètres.

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Test-Runbook"
    $scheduleName = "Sample-DailySchedule"
    $params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
    Register-AzureAutomationScheduledRunbook –AutomationAccountName $automationAccountName `
    –Name $runbookName –ScheduleName $scheduleName –Parameters $params

Les exemples de commandes suivants montrent comment lier une planification à un Runbook à l’aide d’une applet de commande Azure Resource Manager avec des paramètres.

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Test-Runbook"
    $scheduleName = "Sample-DailySchedule"
    $params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
    Register-AzureRmAutomationScheduledRunbook –AutomationAccountName $automationAccountName `
    –Name $runbookName –ScheduleName $scheduleName –Parameters $params `
    -ResourceGroupName "ResourceGroup01"

## <a name="disabling-a-schedule"></a>Désactivation d'une planification
Lorsque vous désactivez une planification, les Runbooks qui lui sont liés ne s'exécutent plus sur cette planification. Vous pouvez désactiver manuellement une planification ou affecter un délai d’expiration aux planifications selon une certaine fréquence lors de leur création. Lorsque le délai d'expiration est atteint, la planification est désactivée.

### <a name="to-disable-a-schedule-from-the-azure-classic-portal"></a>Pour désactiver une planification à partir du portail Azure Classic
Vous pouvez désactiver une planification dans le portail Azure Classic à partir de la page Détails de la planification.

1. Dans le portail Azure Classic, sélectionnez Automation, puis cliquez sur le nom d’un compte Automation.
2. Sélectionnez l'onglet Ressources.
3. Cliquez sur le nom d'une planification pour ouvrir sa page Détails.
4. Remplacez **Activé** par **Non**.

### <a name="to-disable-a-schedule-from-the-azure-portal"></a>Pour désactiver une planification à partir du portail Azure
1. Dans le portail Azure, à partir de votre compte Automation, cliquez sur la mosaïque **Ressources** afin d’ouvrir le panneau **Ressources**.
2. Cliquez sur la mosaïque **Planifications** pour ouvrir le panneau **Planifications**.
3. Cliquez sur le nom d’une planification pour ouvrir le panneau Détails.
4. Remplacez **Activé** par **Non**.

### <a name="to-disable-a-schedule-with-windows-powershell"></a>Pour désactiver une planification avec Windows PowerShell
Vous pouvez utiliser l’applet de commande [Set-AzureAutomationSchedule](http://msdn.microsoft.com/library/azure/dn690270.aspx) pour modifier les propriétés d’une planification existante pour un Runbook classique, ou utiliser l’applet de commande [Set-AzureRmAutomationSchedule](https://msdn.microsoft.com/library/mt603566.aspx) pour les Runbooks exécutés dans le portail Azure. Pour désactiver la planification, spécifiez la valeur **false** pour le paramètre **IsEnabled**.

Les exemples de commandes suivants montrent comment désactiver une planification à l’aide de l’applet de commande Azure Service Management.

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-DailySchedule"
    Set-AzureAutomationSchedule –AutomationAccountName $automationAccountName `
    –Name $scheduleName –IsEnabled $false

Les exemples de commandes suivants montrent comment désactiver une planification pour un Runbook à l’aide d’une applet de commande Azure Resource Manager.

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-MonthlyDaysOfMonthSchedule"
    Set-AzureRmAutomationSchedule –AutomationAccountName $automationAccountName `
    –Name $scheduleName –IsEnabled $false -ResourceGroupName "ResourceGroup01"


## <a name="next-steps"></a>Étapes suivantes
* Pour en savoir plus sur l’utilisation des planifications, consultez [Planifications dans Azure Automation](http://msdn.microsoft.com/library/azure/dn940016.aspx)
* Pour vous familiariser avec les Runbooks dans Azure Automation, consultez [Démarrage d’un Runbook dans Azure Automation](automation-starting-a-runbook.md) 

