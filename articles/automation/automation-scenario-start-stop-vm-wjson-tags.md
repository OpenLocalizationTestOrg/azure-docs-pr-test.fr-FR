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
# <a name="azure-automation-scenario-using-json-formatted-tags-toocreate-a-schedule-for-azure-vm-startup-and-shutdown"></a><span data-ttu-id="79114-103">Scénario d’automatisation Azure : à l’aide du format JSON en balises toocreate une planification pour le démarrage de la machine virtuelle Azure et d’arrêt</span><span class="sxs-lookup"><span data-stu-id="79114-103">Azure Automation scenario: Using JSON-formatted tags toocreate a schedule for Azure VM startup and shutdown</span></span>
<span data-ttu-id="79114-104">Clients souhaitent souvent le démarrage de hello tooschedule et arrêt des machines virtuelles toohelp réduire les coûts d’abonnement ou qu’il prend en charge les besoins métiers et techniques.</span><span class="sxs-lookup"><span data-stu-id="79114-104">Customers often want tooschedule hello startup and shutdown of virtual machines toohelp reduce subscription costs or support business and technical requirements.</span></span>

<span data-ttu-id="79114-105">Hello scénario suivant vous permet de tooset automatisée de démarrage et arrêt de vos machines virtuelles à l’aide d’une balise appelée planification à un niveau de groupe de ressources ou machine virtuelle dans Azure.</span><span class="sxs-lookup"><span data-stu-id="79114-105">hello following scenario enables you tooset up automated startup and shutdown of your VMs by using a tag called Schedule at a resource group level or virtual machine level in Azure.</span></span> <span data-ttu-id="79114-106">Cette planification peut être configurée à partir de tooSaturday dimanche avec un temps de démarrage et l’heure d’arrêt.</span><span class="sxs-lookup"><span data-stu-id="79114-106">This schedule can be configured from Sunday tooSaturday with a startup time and shutdown time.</span></span>

<span data-ttu-id="79114-107">Nous proposons certaines options prêtes à l’emploi.</span><span class="sxs-lookup"><span data-stu-id="79114-107">We do have some out-of-the-box options.</span></span> <span data-ttu-id="79114-108">Vous avez notamment vu les points suivants :</span><span class="sxs-lookup"><span data-stu-id="79114-108">These include:</span></span>

* <span data-ttu-id="79114-109">[Machines virtuelles identiques](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) avec les paramètres de mise à l’échelle qui vous permettent de tooscale in ou out.</span><span class="sxs-lookup"><span data-stu-id="79114-109">[Virtual machine scale sets](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) with autoscale settings that enable you tooscale in or out.</span></span>
* <span data-ttu-id="79114-110">[DevTest Labs](../devtest-lab/devtest-lab-overview.md) service, qui a la fonction intégrée de hello de planification des opérations de démarrage et d’arrêt.</span><span class="sxs-lookup"><span data-stu-id="79114-110">[DevTest Labs](../devtest-lab/devtest-lab-overview.md) service, which has hello built-in capability of scheduling startup and shutdown operations.</span></span>

<span data-ttu-id="79114-111">Toutefois, ces options ne prennent en charge des scénarios spécifiques et ne peut pas être appliqué tooinfrastructure-as-a-service (IaaS) VMs.</span><span class="sxs-lookup"><span data-stu-id="79114-111">However, these options only support specific scenarios and cannot be applied tooinfrastructure-as-a-service (IaaS) VMs.</span></span>

<span data-ttu-id="79114-112">Lorsque hello balise Schedule est un groupe de ressources appliquée tooa, il est également appliqué tooall ordinateurs virtuels à l’intérieur de ce groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="79114-112">When hello Schedule tag is applied tooa resource group, it's also applied tooall virtual machines inside that resource group.</span></span> <span data-ttu-id="79114-113">Si une planification est également appliquée directement tooa machine virtuelle, le dernier calendrier d’hello est prioritaire Bonjour suivant l’ordre :</span><span class="sxs-lookup"><span data-stu-id="79114-113">If a schedule is also directly applied tooa VM, hello last schedule takes precedence in hello following order:</span></span>

1. <span data-ttu-id="79114-114">Groupe de ressources appliquée tooa de planification</span><span class="sxs-lookup"><span data-stu-id="79114-114">Schedule applied tooa resource group</span></span>
2. <span data-ttu-id="79114-115">Planifier le groupe de ressources appliquée tooa et de la machine virtuelle dans le groupe de ressources hello</span><span class="sxs-lookup"><span data-stu-id="79114-115">Schedule applied tooa resource group and virtual machine in hello resource group</span></span>
3. <span data-ttu-id="79114-116">Machine virtuelle de tooa planification appliquée</span><span class="sxs-lookup"><span data-stu-id="79114-116">Schedule applied tooa virtual machine</span></span>

<span data-ttu-id="79114-117">Ce scénario essentiellement prend une chaîne JSON au format spécifié et l’ajoute en tant que valeur de hello pour une balise appelée planification.</span><span class="sxs-lookup"><span data-stu-id="79114-117">This scenario essentially takes a JSON string with a specified format and adds it as hello value for a tag called Schedule.</span></span> <span data-ttu-id="79114-118">Ensuite, un runbook répertorie tous les groupes de ressources et les machines virtuelles et identifie les planifications hello pour chaque machine virtuelle selon les scénarios hello répertoriées plus haut.</span><span class="sxs-lookup"><span data-stu-id="79114-118">Then a runbook lists all resource groups and virtual machines and identifies hello schedules for each VM based on hello scenarios listed earlier.</span></span> <span data-ttu-id="79114-119">Ensuite, il parcourt hello machines virtuelles qui ont des planifications associées et évalue les actions à entreprendre.</span><span class="sxs-lookup"><span data-stu-id="79114-119">Next it loops through hello VMs that have schedules attached and evaluates what action should be taken.</span></span> <span data-ttu-id="79114-120">Par exemple, il détermine machines virtuelles nécessitant toobe s’est arrêté, arrêter ou ignoré.</span><span class="sxs-lookup"><span data-stu-id="79114-120">For example, it determines which VMs need toobe stopped, shut down, or ignored.</span></span>

<span data-ttu-id="79114-121">Ces procédures opérationnelles s’authentifier à l’aide de hello [Azure exécuter en tant que compte](automation-sec-configure-azure-runas-account.md).</span><span class="sxs-lookup"><span data-stu-id="79114-121">These runbooks authenticate by using hello [Azure Run As account](automation-sec-configure-azure-runas-account.md).</span></span>

## <a name="download-hello-runbooks-for-hello-scenario"></a><span data-ttu-id="79114-122">Télécharger des runbooks hello pour le scénario de hello</span><span class="sxs-lookup"><span data-stu-id="79114-122">Download hello runbooks for hello scenario</span></span>
<span data-ttu-id="79114-123">Ce scénario se compose de quatre runbook PowerShell Workflow que vous pouvez télécharger à partir de hello [Galerie TechNet](https://gallery.technet.microsoft.com/Azure-Automation-Runbooks-84f0efc7) ou hello [GitHub](https://github.com/paulomarquesdacosta/azure-automation-scheduled-shutdown-and-startup) référentiel pour ce projet.</span><span class="sxs-lookup"><span data-stu-id="79114-123">This scenario consists of four PowerShell Workflow runbooks that you can download from hello [TechNet Gallery](https://gallery.technet.microsoft.com/Azure-Automation-Runbooks-84f0efc7) or hello [GitHub](https://github.com/paulomarquesdacosta/azure-automation-scheduled-shutdown-and-startup) repository for this project.</span></span>

| <span data-ttu-id="79114-124">Runbook</span><span class="sxs-lookup"><span data-stu-id="79114-124">Runbook</span></span> | <span data-ttu-id="79114-125">Description</span><span class="sxs-lookup"><span data-stu-id="79114-125">Description</span></span> |
| --- | --- |
| <span data-ttu-id="79114-126">Test-ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="79114-126">Test-ResourceSchedule</span></span> |<span data-ttu-id="79114-127">Vérifie chaque planification de la machine virtuelle et effectue l’arrêt ou le démarrage en fonction de la planification de hello.</span><span class="sxs-lookup"><span data-stu-id="79114-127">Checks each virtual machine schedule and performs shutdown or startup depending on hello schedule.</span></span> |
| <span data-ttu-id="79114-128">Add-ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="79114-128">Add-ResourceSchedule</span></span> |<span data-ttu-id="79114-129">Ajoute hello planification balise tooa machine virtuelle ou groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="79114-129">Adds hello Schedule tag tooa VM or resource group.</span></span> |
| <span data-ttu-id="79114-130">Update-ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="79114-130">Update-ResourceSchedule</span></span> |<span data-ttu-id="79114-131">Modifie la balise planification existante de hello en le remplaçant par une autre.</span><span class="sxs-lookup"><span data-stu-id="79114-131">Modifies hello existing Schedule tag by replacing it with a new one.</span></span> |
| <span data-ttu-id="79114-132">Remove-ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="79114-132">Remove-ResourceSchedule</span></span> |<span data-ttu-id="79114-133">Supprime la balise de planification hello à partir d’un machine virtuelle ou groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="79114-133">Removes hello Schedule tag from a VM or resource group.</span></span> |

## <a name="install-and-configure-this-scenario"></a><span data-ttu-id="79114-134">Installer et configurer ce scénario</span><span class="sxs-lookup"><span data-stu-id="79114-134">Install and configure this scenario</span></span>
### <a name="install-and-publish-hello-runbooks"></a><span data-ttu-id="79114-135">Installer et publier des runbooks de hello</span><span class="sxs-lookup"><span data-stu-id="79114-135">Install and publish hello runbooks</span></span>
<span data-ttu-id="79114-136">Après avoir téléchargé hello runbooks, vous pouvez les importer à l’aide de procédure hello dans [création ou importation d’un runbook dans Azure Automation](automation-creating-importing-runbook.md#importing-a-runbook-from-a-file-into-azure-automation).</span><span class="sxs-lookup"><span data-stu-id="79114-136">After downloading hello runbooks, you can import them by using hello procedure in [Creating or importing a runbook in Azure Automation](automation-creating-importing-runbook.md#importing-a-runbook-from-a-file-into-azure-automation).</span></span>  <span data-ttu-id="79114-137">Publiez chaque Runbook une fois qu’il a été correctement importé dans votre compte Automation.</span><span class="sxs-lookup"><span data-stu-id="79114-137">Publish each runbook after it has been successfully imported into your Automation account.</span></span>

### <a name="add-a-schedule-toohello-test-resourceschedule-runbook"></a><span data-ttu-id="79114-138">Ajouter un runbook toohello ResourceSchedule de Test de planification</span><span class="sxs-lookup"><span data-stu-id="79114-138">Add a schedule toohello Test-ResourceSchedule runbook</span></span>
<span data-ttu-id="79114-139">Suivent ces planification de hello tooenable étapes pour le runbook de Test-ResourceSchedule hello.</span><span class="sxs-lookup"><span data-stu-id="79114-139">Follow these steps tooenable hello schedule for hello Test-ResourceSchedule runbook.</span></span> <span data-ttu-id="79114-140">Il s’agit des runbook hello qui vérifie que les ordinateurs virtuels qui doit être démarrés, arrêté, ou laissées telles quelles.</span><span class="sxs-lookup"><span data-stu-id="79114-140">This is hello runbook that verifies which virtual machines should be started, shut down, or left as is.</span></span>

1. <span data-ttu-id="79114-141">À partir de hello portail Azure, ouvrez votre compte Automation, puis cliquez sur hello **Runbooks** vignette.</span><span class="sxs-lookup"><span data-stu-id="79114-141">From hello Azure portal, open your Automation account, and then click hello **Runbooks** tile.</span></span>
2. <span data-ttu-id="79114-142">Sur hello **Test-ResourceSchedule** panneau, cliquez sur hello **planifications** vignette.</span><span class="sxs-lookup"><span data-stu-id="79114-142">On hello **Test-ResourceSchedule** blade, click hello **Schedules** tile.</span></span>
3. <span data-ttu-id="79114-143">Sur hello **planifications** panneau, cliquez sur **ajouter une planification**.</span><span class="sxs-lookup"><span data-stu-id="79114-143">On hello **Schedules** blade, click **Add a schedule**.</span></span>
4. <span data-ttu-id="79114-144">Sur hello **planifications** panneau, sélectionnez **liez un runbook de tooyour planification**.</span><span class="sxs-lookup"><span data-stu-id="79114-144">On hello **Schedules** blade, select **Link a schedule tooyour runbook**.</span></span> <span data-ttu-id="79114-145">Puis sélectionnez **Créer une planification**.</span><span class="sxs-lookup"><span data-stu-id="79114-145">Then select **Create a new schedule**.</span></span>
5. <span data-ttu-id="79114-146">Sur hello **nouvelle planification** panneau, tapez le nom de hello de cette planification, par exemple : *HourlyExecution*.</span><span class="sxs-lookup"><span data-stu-id="79114-146">On hello **New schedule** blade, type in hello name of this schedule, for example: *HourlyExecution*.</span></span>
6. <span data-ttu-id="79114-147">Pour la planification de hello **Démarrer**, définissez hello début tooan heure intervalle.</span><span class="sxs-lookup"><span data-stu-id="79114-147">For hello schedule **Start**, set hello start time tooan hour increment.</span></span>
7. <span data-ttu-id="79114-148">Sélectionnez **Périodicité**, puis, dans le champ d’intervalle **Survenir chaque**, sélectionnez **1 heure**.</span><span class="sxs-lookup"><span data-stu-id="79114-148">Select **Recurrence**, and then for **Recur every interval**, select **1 hour**.</span></span>
8. <span data-ttu-id="79114-149">Vérifiez que **expiration du jeu de** est défini trop**non**, puis cliquez sur **créer** toosave votre nouvelle planification.</span><span class="sxs-lookup"><span data-stu-id="79114-149">Verify that **Set expiration** is set too**No**, and then click **Create** toosave your new schedule.</span></span>
9. <span data-ttu-id="79114-150">Sur hello **planification Runbook** panneau options, sélectionnez **paramètres et les paramètres d’exécution**.</span><span class="sxs-lookup"><span data-stu-id="79114-150">On hello **Schedule Runbook** options blade, select **Parameters and run settings**.</span></span> <span data-ttu-id="79114-151">Bonjour Test-ResourceSchedule **paramètres** panneau, entrez le nom hello de votre abonnement Bonjour **SubscriptionName** champ.</span><span class="sxs-lookup"><span data-stu-id="79114-151">In hello Test-ResourceSchedule **Parameters** blade, enter hello name of your subscription in hello **SubscriptionName** field.</span></span>  <span data-ttu-id="79114-152">Il s’agit de hello seul paramètre qui est requis pour les runbook hello.</span><span class="sxs-lookup"><span data-stu-id="79114-152">This is hello only parameter that's required for hello runbook.</span></span>  <span data-ttu-id="79114-153">Lorsque vous avez terminé, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="79114-153">When you're finished, click **OK**.</span></span>

<span data-ttu-id="79114-154">planification de runbook Hello doit ressembler à hello suivantes lorsqu’elle est effectuée :</span><span class="sxs-lookup"><span data-stu-id="79114-154">hello runbook schedule should look like hello following when it's completed:</span></span>

![Runbook Test-ResourceSchedule configuré](./media/automation-scenario-start-stop-vm-wjson-tags/automation-schedule-config.png)<br>

## <a name="format-hello-json-string"></a><span data-ttu-id="79114-156">Hello du format chaîne JSON</span><span class="sxs-lookup"><span data-stu-id="79114-156">Format hello JSON string</span></span>
<span data-ttu-id="79114-157">Cette solution essentiellement prend JSON de chaîne au format spécifié et l’ajoute en tant que valeur hello pour une balise appelée planification.</span><span class="sxs-lookup"><span data-stu-id="79114-157">This solution basically takes a JSON string with a specified format and adds it as hello value for a tag called Schedule.</span></span> <span data-ttu-id="79114-158">Ensuite, un runbook répertorie tous les groupes de ressources et les machines virtuelles et identifie les planifications hello pour chaque ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="79114-158">Then a runbook lists all resource groups and virtual machines and identifies hello schedules for each virtual machine.</span></span>

<span data-ttu-id="79114-159">Hello runbook effectue une itération sur les machines virtuelles hello qui ont des planifications associées et vérifie les actions à effectuer.</span><span class="sxs-lookup"><span data-stu-id="79114-159">hello runbook loops over hello virtual machines that have schedules attached and checks what actions should be taken.</span></span> <span data-ttu-id="79114-160">Hello Voici un exemple de comment les solutions hello doivent être mis en forme :</span><span class="sxs-lookup"><span data-stu-id="79114-160">hello following is an example of how hello solutions should be formatted:</span></span>

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

<span data-ttu-id="79114-161">Voici certaines informations détaillées concernant cette structure :</span><span class="sxs-lookup"><span data-stu-id="79114-161">Here is some detailed information about this structure:</span></span>

1. <span data-ttu-id="79114-162">format Hello de cette structure JSON est optimisé toowork autour de limite de 256 caractères hello d’une valeur de balise unique dans Azure.</span><span class="sxs-lookup"><span data-stu-id="79114-162">hello format of this JSON structure is optimized toowork around hello 256-character limitation of a single tag value in Azure.</span></span>
2. <span data-ttu-id="79114-163">*TzId* représente hello fuseau horaire de l’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="79114-163">*TzId* represents hello time zone of hello virtual machine.</span></span> <span data-ttu-id="79114-164">Cet ID peut être obtenu à l’aide de la classe TimeZoneInfo .NET de hello dans une session PowerShell--**[System.TimeZoneInfo] :: GetSystemTimeZones()**.</span><span class="sxs-lookup"><span data-stu-id="79114-164">This ID can be obtained by using hello TimeZoneInfo .NET class in a PowerShell session--**[System.TimeZoneInfo]::GetSystemTimeZones()**.</span></span>

   ![GetSystemTimeZones dans PowerShell](./media/automation-scenario-start-stop-vm-wjson-tags/automation-get-timzone-powershell.png)

   * <span data-ttu-id="79114-166">Jours de la semaine sont représentés par une valeur numérique de zéro toosix.</span><span class="sxs-lookup"><span data-stu-id="79114-166">Weekdays are represented with a numeric value of zero toosix.</span></span> <span data-ttu-id="79114-167">valeur de Hello zéro est égal à dimanche.</span><span class="sxs-lookup"><span data-stu-id="79114-167">hello value zero equals Sunday.</span></span>
   * <span data-ttu-id="79114-168">heure de début Hello est représentée par hello **S** attribut et sa valeur est dans un format de 24 heures.</span><span class="sxs-lookup"><span data-stu-id="79114-168">hello start time is represented with hello **S** attribute, and its value is in a 24-hour format.</span></span>
   * <span data-ttu-id="79114-169">heure de fin ou de l’arrêt Hello est représenté par hello **E** attribut et sa valeur est dans un format de 24 heures.</span><span class="sxs-lookup"><span data-stu-id="79114-169">hello end or shutdown time is represented with hello **E** attribute, and its value is in a 24-hour format.</span></span>

     <span data-ttu-id="79114-170">Si hello **S** et **E** attributs chacun ayant la valeur zéro (0), la machine virtuelle de hello demeurera dans son état actuel au moment de l’évaluation de hello.</span><span class="sxs-lookup"><span data-stu-id="79114-170">If hello **S** and **E** attributes each have a value of zero (0), hello virtual machine will be left in its present state at hello time of evaluation.</span></span>
3. <span data-ttu-id="79114-171">Si vous souhaitez que l’évaluation d’un jour spécifique de la semaine de hello tooskip, n’ajoutez pas une section pour ce jour de la semaine de hello.</span><span class="sxs-lookup"><span data-stu-id="79114-171">If you want tooskip evaluation for a specific day of hello week, don’t add a section for that day of hello week.</span></span> <span data-ttu-id="79114-172">Bonjour suivant exemple, uniquement le lundi est évaluée et hello autres jours de la semaine de hello sont ignorés :</span><span class="sxs-lookup"><span data-stu-id="79114-172">In hello following example, only Monday is evaluated, and hello other days of hello week are ignored:</span></span>

    ```json
    {
        "TzId": "Eastern Standard Time",
        "1": {
            "S": "11",
            "E": "17"
        }
    }
    ```

## <a name="tag-resource-groups-or-vms"></a><span data-ttu-id="79114-173">Baliser des groupes de ressources ou des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="79114-173">Tag resource groups or VMs</span></span>
<span data-ttu-id="79114-174">tooshut vers le bas des machines virtuelles, vous devez tootag hello VMs ou groupes de ressources hello dans lequel ils se trouvent.</span><span class="sxs-lookup"><span data-stu-id="79114-174">tooshut down VMs, you need tootag either hello VMs or hello resource groups in which they're located.</span></span> <span data-ttu-id="79114-175">Les machines virtuelles dépourvues de balise Schedule ne sont pas évaluées.</span><span class="sxs-lookup"><span data-stu-id="79114-175">Virtual machines that don't have a Schedule tag are not evaluated.</span></span> <span data-ttu-id="79114-176">Par conséquent, elles ne sont pas démarrées ni arrêtées.</span><span class="sxs-lookup"><span data-stu-id="79114-176">Therefore, they aren't started or shut down.</span></span>

<span data-ttu-id="79114-177">Il existe deux machines virtuelles ou les groupes de ressources de façons tootag avec cette solution.</span><span class="sxs-lookup"><span data-stu-id="79114-177">There are two ways tootag resource groups or VMs with this solution.</span></span> <span data-ttu-id="79114-178">Vous pouvez le faire directement à partir de portail de hello.</span><span class="sxs-lookup"><span data-stu-id="79114-178">You can do it directly from hello portal.</span></span> <span data-ttu-id="79114-179">Ou vous pouvez utiliser Remove-ResourceSchedule runbooks hello Add-ResourceSchedule et ResourceSchedule de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="79114-179">Or you can use hello Add-ResourceSchedule, Update-ResourceSchedule, and Remove-ResourceSchedule runbooks.</span></span>

### <a name="tag-through-hello-portal"></a><span data-ttu-id="79114-180">Balise via le portail de hello</span><span class="sxs-lookup"><span data-stu-id="79114-180">Tag through hello portal</span></span>
<span data-ttu-id="79114-181">Suivez ces étapes tootag un ordinateur virtuel ou un groupe de ressources dans le portail de hello :</span><span class="sxs-lookup"><span data-stu-id="79114-181">Follow these steps tootag a virtual machine or resource group in hello portal:</span></span>

1. <span data-ttu-id="79114-182">Aplatir la chaîne JSON de hello et vérifiez qu’il n’existe pas d’espaces.</span><span class="sxs-lookup"><span data-stu-id="79114-182">Flatten hello JSON string and verify that there aren't any spaces.</span></span>  <span data-ttu-id="79114-183">La chaîne JSON devrait ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="79114-183">Your JSON string should look like this:</span></span>

    ```json
    {"TzId":"Eastern Standard Time","0":{"S":"11","E":"17"},"1":{"S":"9","E":"19"},"2": {"S":"9","E":"19"},"3":{"S":"9","E":"19"},"4":{"S":"9","E":"19"},"5":{"S":"9","E":"19"},"6":{"S":"11","E":"17"}}
    ```

2. <span data-ttu-id="79114-184">Sélectionnez hello **balise** icône pour un ordinateur virtuel ou une ressource de groupe tooapply cette planification.</span><span class="sxs-lookup"><span data-stu-id="79114-184">Select hello **Tag** icon for a VM or resource group tooapply this schedule.</span></span>

   ![Option de balisage de machine virtuelle](./media/automation-scenario-start-stop-vm-wjson-tags/automation-vm-tag-option.png)

3. <span data-ttu-id="79114-186">Les balises sont définies à l’aide d’une paire clé/valeur.</span><span class="sxs-lookup"><span data-stu-id="79114-186">Tags are defined following a key/value pair.</span></span> <span data-ttu-id="79114-187">Type **planification** Bonjour **clé** champ, puis collez chaîne JSON de hello hello **valeur** champ.</span><span class="sxs-lookup"><span data-stu-id="79114-187">Type **Schedule** in hello **Key** field, and then paste hello JSON string into hello **Value** field.</span></span> <span data-ttu-id="79114-188">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="79114-188">Click **Save**.</span></span> <span data-ttu-id="79114-189">Votre nouvelle balise doit maintenant apparaître dans la liste hello des balises pour votre ressource.</span><span class="sxs-lookup"><span data-stu-id="79114-189">Your new tag should now appear in hello list of tags for your resource.</span></span>

   ![Balise de planification de machine virtuelle](./media/automation-scenario-start-stop-vm-wjson-tags/automation-vm-schedule-tag.png)

### <a name="tag-from-powershell"></a><span data-ttu-id="79114-191">Baliser à partir de PowerShell</span><span class="sxs-lookup"><span data-stu-id="79114-191">Tag from PowerShell</span></span>
<span data-ttu-id="79114-192">Tous les runbooks importés contiennent des informations d’aide au début de hello du script hello qui décrit comment tooexecute hello runbooks directement à partir de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="79114-192">All imported runbooks contain help information at hello beginning of hello script that describes how tooexecute hello runbooks directly from PowerShell.</span></span> <span data-ttu-id="79114-193">Vous pouvez appeler hello procédures opérationnelles de Add-ScheduleResource et ScheduleResource de mise à jour à partir de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="79114-193">You can call hello Add-ScheduleResource and Update-ScheduleResource runbooks from PowerShell.</span></span> <span data-ttu-id="79114-194">Pour cela, en passant les paramètres requis qui permettent de balise de planification hello toocreate ou mise à jour sur un machine virtuelle ou groupe de ressources en dehors du portail de hello.</span><span class="sxs-lookup"><span data-stu-id="79114-194">You do this by passing required parameters that enable you toocreate or update hello Schedule tag on a VM or resource group outside of hello portal.</span></span>

<span data-ttu-id="79114-195">toocreate, ajouter et supprimer des balises via PowerShell, vous devez tout d’abord trop[configurer votre environnement PowerShell pour Azure](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="79114-195">toocreate, add, and delete tags through PowerShell, you first need too[set up your PowerShell environment for Azure](/powershell/azure/overview).</span></span> <span data-ttu-id="79114-196">Après avoir terminé le programme d’installation hello, vous pouvez poursuivre hello comme suit.</span><span class="sxs-lookup"><span data-stu-id="79114-196">After you complete hello setup, you can proceed with hello following steps.</span></span>

### <a name="create-a-schedule-tag-with-powershell"></a><span data-ttu-id="79114-197">Créer une balise Schedule avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="79114-197">Create a schedule tag with PowerShell</span></span>
1. <span data-ttu-id="79114-198">Ouvrez une session PowerShell.</span><span class="sxs-lookup"><span data-stu-id="79114-198">Open a PowerShell session.</span></span> <span data-ttu-id="79114-199">Utilisez ensuite hello suivant tooauthenticate exemple avec votre compte d’identification et les toospecify un abonnement :</span><span class="sxs-lookup"><span data-stu-id="79114-199">Then use hello following example tooauthenticate with your Run As account and toospecify a subscription:</span></span>

    ```powershell
    $Conn = Get-AutomationConnection -Name AzureRunAsConnection
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

2. <span data-ttu-id="79114-200">Définissez une table de hachage de planification.</span><span class="sxs-lookup"><span data-stu-id="79114-200">Define a schedule hash table.</span></span> <span data-ttu-id="79114-201">Voici un exemple montrant comment cette table devrait être créée :</span><span class="sxs-lookup"><span data-stu-id="79114-201">Here is an example of how it should be constructed:</span></span>

    ```powershell
    $schedule= @{ "TzId"="Eastern Standard Time"; "0"= @{"S"="11";"E"="17"};"1"= @{"S"="9";"E"="19"};"2"= @{"S"="9";"E"="19"};"3"= @{"S"="9";"E"="19"};"4"= @{"S"="9";"E"="19"};"5"= @{"S"="9";"E"="19"};"6"= @{"S"="11";"E"="17"}}
    ```

3. <span data-ttu-id="79114-202">Définir les paramètres de hello qui sont requis par les runbook hello.</span><span class="sxs-lookup"><span data-stu-id="79114-202">Define hello parameters that are required by hello runbook.</span></span> <span data-ttu-id="79114-203">Bonjour l’exemple suivant, nous prévoyons d’une machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="79114-203">In hello following example, we are targeting a VM:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"; "VmName"="VM01";"Schedule"=$schedule}
    ```

    <span data-ttu-id="79114-204">Si vous êtes le balisage d’un groupe de ressources, supprimez hello *VMName* paramètre à partir du hachage de hello $params table comme suit :</span><span class="sxs-lookup"><span data-stu-id="79114-204">If you’re tagging a resource group, remove hello *VMName* parameter from hello $params hash table as follows:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"; "Schedule"=$schedule}
    ```

4. <span data-ttu-id="79114-205">Exécutez hello Add-ResourceSchedule runbook avec hello paramètres toocreate hello planification balise :</span><span class="sxs-lookup"><span data-stu-id="79114-205">Run hello Add-ResourceSchedule runbook with hello following parameters toocreate hello Schedule tag:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Add-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

5. <span data-ttu-id="79114-206">tooupdate une balise d’ordinateur virtuel ou le groupe de ressource, exécutez hello **ResourceSchedule de mise à jour** runbook avec hello paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="79114-206">tooupdate a resource group or virtual machine tag, execute hello **Update-ResourceSchedule** runbook with hello following parameters:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Update-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

### <a name="remove-a-schedule-tag-with-powershell"></a><span data-ttu-id="79114-207">Supprimer une balise Schedule avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="79114-207">Remove a schedule tag with PowerShell</span></span>
1. <span data-ttu-id="79114-208">Ouvrez une session PowerShell et exécutez hello suivant tooauthenticate avec votre compte d’identification et les tooselect spécifier un abonnement :</span><span class="sxs-lookup"><span data-stu-id="79114-208">Open a PowerShell session and run hello following tooauthenticate with your Run As account and tooselect and specify a subscription:</span></span>

    ```powershell
    Conn = Get-AutomationConnection -Name AzureRunAsConnection
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

2. <span data-ttu-id="79114-209">Définir les paramètres de hello qui sont requis par les runbook hello.</span><span class="sxs-lookup"><span data-stu-id="79114-209">Define hello parameters that are required by hello runbook.</span></span> <span data-ttu-id="79114-210">Bonjour l’exemple suivant, nous prévoyons d’une machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="79114-210">In hello following example, we are targeting a VM:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01";"VmName"="VM01"}
    ```

    <span data-ttu-id="79114-211">Si vous supprimez une balise à partir d’un groupe de ressources, supprimez hello *VMName* paramètre à partir du hachage de hello $params table comme suit :</span><span class="sxs-lookup"><span data-stu-id="79114-211">If you’re removing a tag from a resource group, remove hello *VMName* parameter from hello $params hash table as follows:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"}
    ```

3. <span data-ttu-id="79114-212">Balise de planification du runbook tooremove hello hello Remove-ResourceSchedule, exécutez :</span><span class="sxs-lookup"><span data-stu-id="79114-212">Execute hello Remove-ResourceSchedule runbook tooremove hello Schedule tag:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Remove-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

4. <span data-ttu-id="79114-213">tooupdate une balise d’ordinateur virtuel ou le groupe de ressource, exécutez hello Remove-ResourceSchedule runbook avec hello paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="79114-213">tooupdate a resource group or virtual machine tag, execute hello Remove-ResourceSchedule runbook with hello following parameters:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Remove-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

> [!NOTE]
> <span data-ttu-id="79114-214">Nous vous recommandons de façon proactive surveiller ces procédures opérationnelles (et les États des machines virtuelles hello) tooverify vos ordinateurs virtuels sont en cours est arrêté et démarré en conséquence.</span><span class="sxs-lookup"><span data-stu-id="79114-214">We recommend that you proactively monitor these runbooks (and hello virtual machine states) tooverify that your virtual machines are being shut down and started accordingly.</span></span>
>

<span data-ttu-id="79114-215">Détails de hello tooview du runbook de hello ResourceSchedule de Test de la tâche Bonjour portail Azure, sélectionnez hello **travaux** vignette du runbook de hello.</span><span class="sxs-lookup"><span data-stu-id="79114-215">tooview hello details of hello Test-ResourceSchedule runbook job in hello Azure portal, select hello **Jobs** tile of hello runbook.</span></span> <span data-ttu-id="79114-216">paramètres d’entrée de Hello tâche récapitulative affiche hello et sortie de hello stream, en outre toogeneral plus d’informations sur la tâche de hello et toutes les exceptions si elles se sont produites.</span><span class="sxs-lookup"><span data-stu-id="79114-216">hello job summary displays hello input parameters and hello output stream, in addition toogeneral information about hello job and any exceptions if they occurred.</span></span>

<span data-ttu-id="79114-217">Hello **récapitulatif** inclut les messages à partir de flux de sortie, d’avertissement et erreur hello.</span><span class="sxs-lookup"><span data-stu-id="79114-217">hello **Job Summary** includes messages from hello output, warning, and error streams.</span></span> <span data-ttu-id="79114-218">Sélectionnez hello **sortie** vignette tooview des résultats à partir de l’exécution du runbook hello détaillés.</span><span class="sxs-lookup"><span data-stu-id="79114-218">Select hello **Output** tile tooview detailed results from hello runbook execution.</span></span>

![Sortie Test-ResourceSchedule](./media/automation-scenario-start-stop-vm-wjson-tags/automation-job-output.png)

## <a name="next-steps"></a><span data-ttu-id="79114-220">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="79114-220">Next steps</span></span>
* <span data-ttu-id="79114-221">tooget a démarré avec des runbooks de flux de travail PowerShell, consultez [mon premier runbook de flux de travail PowerShell](automation-first-runbook-textual.md).</span><span class="sxs-lookup"><span data-stu-id="79114-221">tooget started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md).</span></span>
* <span data-ttu-id="79114-222">toolearn en savoir plus sur les types de runbook et leurs avantages et les limitations, consultez [types de runbook Azure Automation](automation-runbook-types.md).</span><span class="sxs-lookup"><span data-stu-id="79114-222">toolearn more about runbook types, and their advantages and limitations, see [Azure Automation runbook types](automation-runbook-types.md).</span></span>
* <span data-ttu-id="79114-223">Pour plus d’informations sur les fonctionnalités de prise en charge des scripts PowerShell, voir [Native PowerShell script support in Azure Automation](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/)(Prise en charge de scripts PowerShell natifs dans Azure Automation).</span><span class="sxs-lookup"><span data-stu-id="79114-223">For more information about PowerShell script support features, see [Native PowerShell script support in Azure Automation](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/).</span></span>
* <span data-ttu-id="79114-224">toolearn en savoir plus sur la journalisation de runbook et de sortie, consultez [Runbook sortie et les messages dans Azure Automation](automation-runbook-output-and-messages.md).</span><span class="sxs-lookup"><span data-stu-id="79114-224">toolearn more about runbook logging and output, see [Runbook output and messages in Azure Automation](automation-runbook-output-and-messages.md).</span></span>
* <span data-ttu-id="79114-225">toolearn plus d’informations sur un compte d’identification Azure et comment tooauthenticate vos runbook à l’aide, consultez [authentifier des procédures opérationnelles compte d’identification Azure](automation-sec-configure-azure-runas-account.md).</span><span class="sxs-lookup"><span data-stu-id="79114-225">toolearn more about an Azure Run As account and how tooauthenticate your runbooks by using it, see [Authenticate runbooks with Azure Run As account](automation-sec-configure-azure-runas-account.md).</span></span>
