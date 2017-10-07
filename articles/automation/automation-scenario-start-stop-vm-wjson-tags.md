---
title: "aaaUse état de machine virtuelle Azure au format JSON de balises tooschedule | Documents Microsoft"
description: "Cet article explique comment toouse JSON chaînes sur les balises tooautomate hello de planification de l’arrêt et démarrage de la machine virtuelle."
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
ms.assetid: 6afed5d2-e939-4749-8b2c-9312b4c16fb2
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: magoedte;paulomarquesc
ms.openlocfilehash: f6bbf1dea1c193e5d1010f12f3b1ed63562f9daf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario-using-json-formatted-tags-toocreate-a-schedule-for-azure-vm-startup-and-shutdown"></a>Scénario d’automatisation Azure : à l’aide du format JSON en balises toocreate une planification pour le démarrage de la machine virtuelle Azure et d’arrêt
Clients souhaitent souvent le démarrage de hello tooschedule et arrêt des machines virtuelles toohelp réduire les coûts d’abonnement ou qu’il prend en charge les besoins métiers et techniques.

Hello scénario suivant vous permet de tooset automatisée de démarrage et arrêt de vos machines virtuelles à l’aide d’une balise appelée planification à un niveau de groupe de ressources ou machine virtuelle dans Azure. Cette planification peut être configurée à partir de tooSaturday dimanche avec un temps de démarrage et l’heure d’arrêt.

Nous proposons certaines options prêtes à l’emploi. Vous avez notamment vu les points suivants :

* [Machines virtuelles identiques](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) avec les paramètres de mise à l’échelle qui vous permettent de tooscale in ou out.
* [DevTest Labs](../devtest-lab/devtest-lab-overview.md) service, qui a la fonction intégrée de hello de planification des opérations de démarrage et d’arrêt.

Toutefois, ces options ne prennent en charge des scénarios spécifiques et ne peut pas être appliqué tooinfrastructure-as-a-service (IaaS) VMs.

Lorsque hello balise Schedule est un groupe de ressources appliquée tooa, il est également appliqué tooall ordinateurs virtuels à l’intérieur de ce groupe de ressources. Si une planification est également appliquée directement tooa machine virtuelle, le dernier calendrier d’hello est prioritaire Bonjour suivant l’ordre :

1. Groupe de ressources appliquée tooa de planification
2. Planifier le groupe de ressources appliquée tooa et de la machine virtuelle dans le groupe de ressources hello
3. Machine virtuelle de tooa planification appliquée

Ce scénario essentiellement prend une chaîne JSON au format spécifié et l’ajoute en tant que valeur de hello pour une balise appelée planification. Ensuite, un runbook répertorie tous les groupes de ressources et les machines virtuelles et identifie les planifications hello pour chaque machine virtuelle selon les scénarios hello répertoriées plus haut. Ensuite, il parcourt hello machines virtuelles qui ont des planifications associées et évalue les actions à entreprendre. Par exemple, il détermine machines virtuelles nécessitant toobe s’est arrêté, arrêter ou ignoré.

Ces procédures opérationnelles s’authentifier à l’aide de hello [Azure exécuter en tant que compte](automation-sec-configure-azure-runas-account.md).

## <a name="download-hello-runbooks-for-hello-scenario"></a>Télécharger des runbooks hello pour le scénario de hello
Ce scénario se compose de quatre runbook PowerShell Workflow que vous pouvez télécharger à partir de hello [Galerie TechNet](https://gallery.technet.microsoft.com/Azure-Automation-Runbooks-84f0efc7) ou hello [GitHub](https://github.com/paulomarquesdacosta/azure-automation-scheduled-shutdown-and-startup) référentiel pour ce projet.

| Runbook | Description |
| --- | --- |
| Test-ResourceSchedule |Vérifie chaque planification de la machine virtuelle et effectue l’arrêt ou le démarrage en fonction de la planification de hello. |
| Add-ResourceSchedule |Ajoute hello planification balise tooa machine virtuelle ou groupe de ressources. |
| Update-ResourceSchedule |Modifie la balise planification existante de hello en le remplaçant par une autre. |
| Remove-ResourceSchedule |Supprime la balise de planification hello à partir d’un machine virtuelle ou groupe de ressources. |

## <a name="install-and-configure-this-scenario"></a>Installer et configurer ce scénario
### <a name="install-and-publish-hello-runbooks"></a>Installer et publier des runbooks de hello
Après avoir téléchargé hello runbooks, vous pouvez les importer à l’aide de procédure hello dans [création ou importation d’un runbook dans Azure Automation](automation-creating-importing-runbook.md#importing-a-runbook-from-a-file-into-azure-automation).  Publiez chaque Runbook une fois qu’il a été correctement importé dans votre compte Automation.

### <a name="add-a-schedule-toohello-test-resourceschedule-runbook"></a>Ajouter un runbook toohello ResourceSchedule de Test de planification
Suivent ces planification de hello tooenable étapes pour le runbook de Test-ResourceSchedule hello. Il s’agit des runbook hello qui vérifie que les ordinateurs virtuels qui doit être démarrés, arrêté, ou laissées telles quelles.

1. À partir de hello portail Azure, ouvrez votre compte Automation, puis cliquez sur hello **Runbooks** vignette.
2. Sur hello **Test-ResourceSchedule** panneau, cliquez sur hello **planifications** vignette.
3. Sur hello **planifications** panneau, cliquez sur **ajouter une planification**.
4. Sur hello **planifications** panneau, sélectionnez **liez un runbook de tooyour planification**. Puis sélectionnez **Créer une planification**.
5. Sur hello **nouvelle planification** panneau, tapez le nom de hello de cette planification, par exemple : *HourlyExecution*.
6. Pour la planification de hello **Démarrer**, définissez hello début tooan heure intervalle.
7. Sélectionnez **Périodicité**, puis, dans le champ d’intervalle **Survenir chaque**, sélectionnez **1 heure**.
8. Vérifiez que **expiration du jeu de** est défini trop**non**, puis cliquez sur **créer** toosave votre nouvelle planification.
9. Sur hello **planification Runbook** panneau options, sélectionnez **paramètres et les paramètres d’exécution**. Bonjour Test-ResourceSchedule **paramètres** panneau, entrez le nom hello de votre abonnement Bonjour **SubscriptionName** champ.  Il s’agit de hello seul paramètre qui est requis pour les runbook hello.  Lorsque vous avez terminé, cliquez sur **OK**.

planification de runbook Hello doit ressembler à hello suivantes lorsqu’elle est effectuée :

![Runbook Test-ResourceSchedule configuré](./media/automation-scenario-start-stop-vm-wjson-tags/automation-schedule-config.png)<br>

## <a name="format-hello-json-string"></a>Hello du format chaîne JSON
Cette solution essentiellement prend JSON de chaîne au format spécifié et l’ajoute en tant que valeur hello pour une balise appelée planification. Ensuite, un runbook répertorie tous les groupes de ressources et les machines virtuelles et identifie les planifications hello pour chaque ordinateur virtuel.

Hello runbook effectue une itération sur les machines virtuelles hello qui ont des planifications associées et vérifie les actions à effectuer. Hello Voici un exemple de comment les solutions hello doivent être mis en forme :

```json
{
    "TzId": "Eastern Standard Time",
    "0": {
        "S": "11",
        "E": "17"
    },
    "1": {
        "S": "9",
        "E": "19"
    },
    "2": {
        "S": "9",
        "E": "19"
    },
}
```

Voici certaines informations détaillées concernant cette structure :

1. format Hello de cette structure JSON est optimisé toowork autour de limite de 256 caractères hello d’une valeur de balise unique dans Azure.
2. *TzId* représente hello fuseau horaire de l’ordinateur virtuel de hello. Cet ID peut être obtenu à l’aide de la classe TimeZoneInfo .NET de hello dans une session PowerShell--**[System.TimeZoneInfo] :: GetSystemTimeZones()**.

   ![GetSystemTimeZones dans PowerShell](./media/automation-scenario-start-stop-vm-wjson-tags/automation-get-timzone-powershell.png)

   * Jours de la semaine sont représentés par une valeur numérique de zéro toosix. valeur de Hello zéro est égal à dimanche.
   * heure de début Hello est représentée par hello **S** attribut et sa valeur est dans un format de 24 heures.
   * heure de fin ou de l’arrêt Hello est représenté par hello **E** attribut et sa valeur est dans un format de 24 heures.

     Si hello **S** et **E** attributs chacun ayant la valeur zéro (0), la machine virtuelle de hello demeurera dans son état actuel au moment de l’évaluation de hello.
3. Si vous souhaitez que l’évaluation d’un jour spécifique de la semaine de hello tooskip, n’ajoutez pas une section pour ce jour de la semaine de hello. Bonjour suivant exemple, uniquement le lundi est évaluée et hello autres jours de la semaine de hello sont ignorés :

    ```json
    {
        "TzId": "Eastern Standard Time",
        "1": {
            "S": "11",
            "E": "17"
        }
    }
    ```

## <a name="tag-resource-groups-or-vms"></a>Baliser des groupes de ressources ou des machines virtuelles
tooshut vers le bas des machines virtuelles, vous devez tootag hello VMs ou groupes de ressources hello dans lequel ils se trouvent. Les machines virtuelles dépourvues de balise Schedule ne sont pas évaluées. Par conséquent, elles ne sont pas démarrées ni arrêtées.

Il existe deux machines virtuelles ou les groupes de ressources de façons tootag avec cette solution. Vous pouvez le faire directement à partir de portail de hello. Ou vous pouvez utiliser Remove-ResourceSchedule runbooks hello Add-ResourceSchedule et ResourceSchedule de mise à jour.

### <a name="tag-through-hello-portal"></a>Balise via le portail de hello
Suivez ces étapes tootag un ordinateur virtuel ou un groupe de ressources dans le portail de hello :

1. Aplatir la chaîne JSON de hello et vérifiez qu’il n’existe pas d’espaces.  La chaîne JSON devrait ressembler à ceci :

    ```json
    {"TzId":"Eastern Standard Time","0":{"S":"11","E":"17"},"1":{"S":"9","E":"19"},"2": {"S":"9","E":"19"},"3":{"S":"9","E":"19"},"4":{"S":"9","E":"19"},"5":{"S":"9","E":"19"},"6":{"S":"11","E":"17"}}
    ```

2. Sélectionnez hello **balise** icône pour un ordinateur virtuel ou une ressource de groupe tooapply cette planification.

   ![Option de balisage de machine virtuelle](./media/automation-scenario-start-stop-vm-wjson-tags/automation-vm-tag-option.png)

3. Les balises sont définies à l’aide d’une paire clé/valeur. Type **planification** Bonjour **clé** champ, puis collez chaîne JSON de hello hello **valeur** champ. Cliquez sur **Enregistrer**. Votre nouvelle balise doit maintenant apparaître dans la liste hello des balises pour votre ressource.

   ![Balise de planification de machine virtuelle](./media/automation-scenario-start-stop-vm-wjson-tags/automation-vm-schedule-tag.png)

### <a name="tag-from-powershell"></a>Baliser à partir de PowerShell
Tous les runbooks importés contiennent des informations d’aide au début de hello du script hello qui décrit comment tooexecute hello runbooks directement à partir de PowerShell. Vous pouvez appeler hello procédures opérationnelles de Add-ScheduleResource et ScheduleResource de mise à jour à partir de PowerShell. Pour cela, en passant les paramètres requis qui permettent de balise de planification hello toocreate ou mise à jour sur un machine virtuelle ou groupe de ressources en dehors du portail de hello.

toocreate, ajouter et supprimer des balises via PowerShell, vous devez tout d’abord trop[configurer votre environnement PowerShell pour Azure](/powershell/azure/overview). Après avoir terminé le programme d’installation hello, vous pouvez poursuivre hello comme suit.

### <a name="create-a-schedule-tag-with-powershell"></a>Créer une balise Schedule avec PowerShell
1. Ouvrez une session PowerShell. Utilisez ensuite hello suivant tooauthenticate exemple avec votre compte d’identification et les toospecify un abonnement :

    ```powershell
    $Conn = Get-AutomationConnection -Name AzureRunAsConnection
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

2. Définissez une table de hachage de planification. Voici un exemple montrant comment cette table devrait être créée :

    ```powershell
    $schedule= @{ "TzId"="Eastern Standard Time"; "0"= @{"S"="11";"E"="17"};"1"= @{"S"="9";"E"="19"};"2"= @{"S"="9";"E"="19"};"3"= @{"S"="9";"E"="19"};"4"= @{"S"="9";"E"="19"};"5"= @{"S"="9";"E"="19"};"6"= @{"S"="11";"E"="17"}}
    ```

3. Définir les paramètres de hello qui sont requis par les runbook hello. Bonjour l’exemple suivant, nous prévoyons d’une machine virtuelle :

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"; "VmName"="VM01";"Schedule"=$schedule}
    ```

    Si vous êtes le balisage d’un groupe de ressources, supprimez hello *VMName* paramètre à partir du hachage de hello $params table comme suit :

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"; "Schedule"=$schedule}
    ```

4. Exécutez hello Add-ResourceSchedule runbook avec hello paramètres toocreate hello planification balise :

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Add-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

5. tooupdate une balise d’ordinateur virtuel ou le groupe de ressource, exécutez hello **ResourceSchedule de mise à jour** runbook avec hello paramètres suivants :

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Update-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

### <a name="remove-a-schedule-tag-with-powershell"></a>Supprimer une balise Schedule avec PowerShell
1. Ouvrez une session PowerShell et exécutez hello suivant tooauthenticate avec votre compte d’identification et les tooselect spécifier un abonnement :

    ```powershell
    Conn = Get-AutomationConnection -Name AzureRunAsConnection
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

2. Définir les paramètres de hello qui sont requis par les runbook hello. Bonjour l’exemple suivant, nous prévoyons d’une machine virtuelle :

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01";"VmName"="VM01"}
    ```

    Si vous supprimez une balise à partir d’un groupe de ressources, supprimez hello *VMName* paramètre à partir du hachage de hello $params table comme suit :

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"}
    ```

3. Balise de planification du runbook tooremove hello hello Remove-ResourceSchedule, exécutez :

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Remove-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

4. tooupdate une balise d’ordinateur virtuel ou le groupe de ressource, exécutez hello Remove-ResourceSchedule runbook avec hello paramètres suivants :

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Remove-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

> [!NOTE]
> Nous vous recommandons de façon proactive surveiller ces procédures opérationnelles (et les États des machines virtuelles hello) tooverify vos ordinateurs virtuels sont en cours est arrêté et démarré en conséquence.
>

Détails de hello tooview du runbook de hello ResourceSchedule de Test de la tâche Bonjour portail Azure, sélectionnez hello **travaux** vignette du runbook de hello. paramètres d’entrée de Hello tâche récapitulative affiche hello et sortie de hello stream, en outre toogeneral plus d’informations sur la tâche de hello et toutes les exceptions si elles se sont produites.

Hello **récapitulatif** inclut les messages à partir de flux de sortie, d’avertissement et erreur hello. Sélectionnez hello **sortie** vignette tooview des résultats à partir de l’exécution du runbook hello détaillés.

![Sortie Test-ResourceSchedule](./media/automation-scenario-start-stop-vm-wjson-tags/automation-job-output.png)

## <a name="next-steps"></a>Étapes suivantes
* tooget a démarré avec des runbooks de flux de travail PowerShell, consultez [mon premier runbook de flux de travail PowerShell](automation-first-runbook-textual.md).
* toolearn en savoir plus sur les types de runbook et leurs avantages et les limitations, consultez [types de runbook Azure Automation](automation-runbook-types.md).
* Pour plus d’informations sur les fonctionnalités de prise en charge des scripts PowerShell, voir [Native PowerShell script support in Azure Automation](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/)(Prise en charge de scripts PowerShell natifs dans Azure Automation).
* toolearn en savoir plus sur la journalisation de runbook et de sortie, consultez [Runbook sortie et les messages dans Azure Automation](automation-runbook-output-and-messages.md).
* toolearn plus d’informations sur un compte d’identification Azure et comment tooauthenticate vos runbook à l’aide, consultez [authentifier des procédures opérationnelles compte d’identification Azure](automation-sec-configure-azure-runas-account.md).
