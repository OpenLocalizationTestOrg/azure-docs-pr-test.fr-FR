---
title: "Utiliser des balises au format JSON pour planifier l’état des machines virtuelles Azure | Microsoft Docs"
description: "Cet article explique comment utiliser des chaînes JSON sur des balises pour automatiser la planification du démarrage et de l’arrêt des machines virtuelles."
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
ms.openlocfilehash: f8d9563318c3afe299cebb7c889874392f114f84
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-automation-scenario-using-json-formatted-tags-to-create-a-schedule-for-azure-vm-startup-and-shutdown"></a><span data-ttu-id="efc50-103">Scénario Azure Automation : utilisation de balises au format JSON afin de créer une planification pour le démarrage et l’arrêt de machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="efc50-103">Azure Automation scenario: Using JSON-formatted tags to create a schedule for Azure VM startup and shutdown</span></span>
<span data-ttu-id="efc50-104">Dans la plupart des cas, les clients souhaitent planifier le démarrage et l’arrêt des machines virtuelles pour alléger les frais d’abonnement ou pour prendre en charge les exigences professionnelles et techniques.</span><span class="sxs-lookup"><span data-stu-id="efc50-104">Customers often want to schedule the startup and shutdown of virtual machines to help reduce subscription costs or support business and technical requirements.</span></span>

<span data-ttu-id="efc50-105">Le scénario ci-après vous permet d’automatiser le démarrage et l’arrêt de vos machines virtuelles à l’aide d’une balise appelée Schedule au niveau d’un groupe de ressources ou d’une machine virtuelle dans Azure.</span><span class="sxs-lookup"><span data-stu-id="efc50-105">The following scenario enables you to set up automated startup and shutdown of your VMs by using a tag called Schedule at a resource group level or virtual machine level in Azure.</span></span> <span data-ttu-id="efc50-106">Cette planification peut être configurée du dimanche au samedi, avec une heure de démarrage et une heure d’arrêt.</span><span class="sxs-lookup"><span data-stu-id="efc50-106">This schedule can be configured from Sunday to Saturday with a startup time and shutdown time.</span></span>

<span data-ttu-id="efc50-107">Nous proposons certaines options prêtes à l’emploi.</span><span class="sxs-lookup"><span data-stu-id="efc50-107">We do have some out-of-the-box options.</span></span> <span data-ttu-id="efc50-108">Vous avez notamment vu les points suivants :</span><span class="sxs-lookup"><span data-stu-id="efc50-108">These include:</span></span>

* <span data-ttu-id="efc50-109">[groupes de machines virtuelles identiques](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) avec des paramètres de mise à l’échelle automatique qui vous permettent de diminuer ou d’augmenter la taille des instances ;</span><span class="sxs-lookup"><span data-stu-id="efc50-109">[Virtual machine scale sets](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) with autoscale settings that enable you to scale in or out.</span></span>
* <span data-ttu-id="efc50-110">[DevTest Labs](../devtest-lab/devtest-lab-overview.md) intégrant la fonctionnalité de planification des opérations de démarrage et d’arrêt.</span><span class="sxs-lookup"><span data-stu-id="efc50-110">[DevTest Labs](../devtest-lab/devtest-lab-overview.md) service, which has the built-in capability of scheduling startup and shutdown operations.</span></span>

<span data-ttu-id="efc50-111">Toutefois, ces options prennent uniquement en charge des scénarios spécifiques et ne sont pas applicables aux machines virtuelles IaaS (infrastructure as a service).</span><span class="sxs-lookup"><span data-stu-id="efc50-111">However, these options only support specific scenarios and cannot be applied to infrastructure-as-a-service (IaaS) VMs.</span></span>

<span data-ttu-id="efc50-112">Lorsque la balise Schedule est appliquée à un groupe de ressources, elle s’applique également à toutes les machines virtuelles figurant dans ce groupe.</span><span class="sxs-lookup"><span data-stu-id="efc50-112">When the Schedule tag is applied to a resource group, it's also applied to all virtual machines inside that resource group.</span></span> <span data-ttu-id="efc50-113">En outre, si une planification est appliquée directement à une machine virtuelle, la dernière planification est prioritaire dans l’ordre suivant :</span><span class="sxs-lookup"><span data-stu-id="efc50-113">If a schedule is also directly applied to a VM, the last schedule takes precedence in the following order:</span></span>

1. <span data-ttu-id="efc50-114">Planification appliquée à un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="efc50-114">Schedule applied to a resource group</span></span>
2. <span data-ttu-id="efc50-115">Planification appliquée à un groupe de ressources et à une machine virtuelle dans le groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="efc50-115">Schedule applied to a resource group and virtual machine in the resource group</span></span>
3. <span data-ttu-id="efc50-116">Planification appliquée à une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="efc50-116">Schedule applied to a virtual machine</span></span>

<span data-ttu-id="efc50-117">Ce scénario sélectionne une chaîne JSON dans un format spécifié et l’ajoute en tant que valeur d’une balise appelée Schedule.</span><span class="sxs-lookup"><span data-stu-id="efc50-117">This scenario essentially takes a JSON string with a specified format and adds it as the value for a tag called Schedule.</span></span> <span data-ttu-id="efc50-118">Ensuite, un Runbook répertorie l’ensemble des groupes de ressources et des machines virtuelles, puis identifie les planifications pour chaque machine virtuelle basée sur les scénarios indiqués ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="efc50-118">Then a runbook lists all resource groups and virtual machines and identifies the schedules for each VM based on the scenarios listed earlier.</span></span> <span data-ttu-id="efc50-119">Ce Runbook itère ensuite sur les machines virtuelles associées à des planifications et évalue l’action à entreprendre.</span><span class="sxs-lookup"><span data-stu-id="efc50-119">Next it loops through the VMs that have schedules attached and evaluates what action should be taken.</span></span> <span data-ttu-id="efc50-120">Par exemple, il détermine les machines virtuelles qui doivent être interrompues, arrêtées ou ignorées.</span><span class="sxs-lookup"><span data-stu-id="efc50-120">For example, it determines which VMs need to be stopped, shut down, or ignored.</span></span>

<span data-ttu-id="efc50-121">Ces Runbooks s’authentifient à l’aide du [compte d’identification Azure](automation-sec-configure-azure-runas-account.md).</span><span class="sxs-lookup"><span data-stu-id="efc50-121">These runbooks authenticate by using the [Azure Run As account](automation-sec-configure-azure-runas-account.md).</span></span>

## <a name="download-the-runbooks-for-the-scenario"></a><span data-ttu-id="efc50-122">Télécharger les Runbooks associés au scénario</span><span class="sxs-lookup"><span data-stu-id="efc50-122">Download the runbooks for the scenario</span></span>
<span data-ttu-id="efc50-123">Ce scénario se compose de quatre Runbooks de flux de travail PowerShell que vous pouvez télécharger à partir de la [Galerie TechNet](https://gallery.technet.microsoft.com/Azure-Automation-Runbooks-84f0efc7) ou du référentiel [GitHub](https://github.com/paulomarquesdacosta/azure-automation-scheduled-shutdown-and-startup) pour ce projet.</span><span class="sxs-lookup"><span data-stu-id="efc50-123">This scenario consists of four PowerShell Workflow runbooks that you can download from the [TechNet Gallery](https://gallery.technet.microsoft.com/Azure-Automation-Runbooks-84f0efc7) or the [GitHub](https://github.com/paulomarquesdacosta/azure-automation-scheduled-shutdown-and-startup) repository for this project.</span></span>

| <span data-ttu-id="efc50-124">Runbook</span><span class="sxs-lookup"><span data-stu-id="efc50-124">Runbook</span></span> | <span data-ttu-id="efc50-125">Description</span><span class="sxs-lookup"><span data-stu-id="efc50-125">Description</span></span> |
| --- | --- |
| <span data-ttu-id="efc50-126">Test-ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="efc50-126">Test-ResourceSchedule</span></span> |<span data-ttu-id="efc50-127">Vérifie la planification de chaque machine virtuelle et arrête ou démarre les machines virtuelles selon la planification.</span><span class="sxs-lookup"><span data-stu-id="efc50-127">Checks each virtual machine schedule and performs shutdown or startup depending on the schedule.</span></span> |
| <span data-ttu-id="efc50-128">Add-ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="efc50-128">Add-ResourceSchedule</span></span> |<span data-ttu-id="efc50-129">Ajoute la balise Schedule à une machine virtuelle ou à un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="efc50-129">Adds the Schedule tag to a VM or resource group.</span></span> |
| <span data-ttu-id="efc50-130">Update-ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="efc50-130">Update-ResourceSchedule</span></span> |<span data-ttu-id="efc50-131">Modifie la balise Schedule existante en la remplaçant par une nouvelle balise.</span><span class="sxs-lookup"><span data-stu-id="efc50-131">Modifies the existing Schedule tag by replacing it with a new one.</span></span> |
| <span data-ttu-id="efc50-132">Remove-ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="efc50-132">Remove-ResourceSchedule</span></span> |<span data-ttu-id="efc50-133">Supprime la balise Schedule d’une machine virtuelle ou d’un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="efc50-133">Removes the Schedule tag from a VM or resource group.</span></span> |

## <a name="install-and-configure-this-scenario"></a><span data-ttu-id="efc50-134">Installer et configurer ce scénario</span><span class="sxs-lookup"><span data-stu-id="efc50-134">Install and configure this scenario</span></span>
### <a name="install-and-publish-the-runbooks"></a><span data-ttu-id="efc50-135">Installer et publier des Runbook</span><span class="sxs-lookup"><span data-stu-id="efc50-135">Install and publish the runbooks</span></span>
<span data-ttu-id="efc50-136">Après avoir téléchargé les Runbooks, vous pouvez les importer à l’aide de la procédure décrite dans [Création ou importation d’un runbook dans Azure Automation](automation-creating-importing-runbook.md#importing-a-runbook-from-a-file-into-azure-automation).</span><span class="sxs-lookup"><span data-stu-id="efc50-136">After downloading the runbooks, you can import them by using the procedure in [Creating or importing a runbook in Azure Automation](automation-creating-importing-runbook.md#importing-a-runbook-from-a-file-into-azure-automation).</span></span>  <span data-ttu-id="efc50-137">Publiez chaque Runbook une fois qu’il a été correctement importé dans votre compte Automation.</span><span class="sxs-lookup"><span data-stu-id="efc50-137">Publish each runbook after it has been successfully imported into your Automation account.</span></span>

### <a name="add-a-schedule-to-the-test-resourceschedule-runbook"></a><span data-ttu-id="efc50-138">Ajouter une planification au Runbook Test-ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="efc50-138">Add a schedule to the Test-ResourceSchedule runbook</span></span>
<span data-ttu-id="efc50-139">Procédez comme suit pour activer la planification relative au Runbook Test-ResourceSchedule.</span><span class="sxs-lookup"><span data-stu-id="efc50-139">Follow these steps to enable the schedule for the Test-ResourceSchedule runbook.</span></span> <span data-ttu-id="efc50-140">Il s’agit du Runbook qui vérifie quelles machines virtuelles doivent être démarrées, arrêtées ou laissées telles quelles.</span><span class="sxs-lookup"><span data-stu-id="efc50-140">This is the runbook that verifies which virtual machines should be started, shut down, or left as is.</span></span>

1. <span data-ttu-id="efc50-141">Dans le Portail Azure, ouvrez votre compte Automation, puis cliquez sur la vignette **Runbooks** .</span><span class="sxs-lookup"><span data-stu-id="efc50-141">From the Azure portal, open your Automation account, and then click the **Runbooks** tile.</span></span>
2. <span data-ttu-id="efc50-142">Dans le panneau **Test-ResourceSchedule**, cliquez sur la vignette **Planifications**.</span><span class="sxs-lookup"><span data-stu-id="efc50-142">On the **Test-ResourceSchedule** blade, click the **Schedules** tile.</span></span>
3. <span data-ttu-id="efc50-143">Dans le panneau **Planifications**, cliquez sur **Ajouter une planification**.</span><span class="sxs-lookup"><span data-stu-id="efc50-143">On the **Schedules** blade, click **Add a schedule**.</span></span>
4. <span data-ttu-id="efc50-144">Dans le panneau **Planifications**, sélectionnez **Associer une planification à votre Runbook**.</span><span class="sxs-lookup"><span data-stu-id="efc50-144">On the **Schedules** blade, select **Link a schedule to your runbook**.</span></span> <span data-ttu-id="efc50-145">Puis sélectionnez **Créer une planification**.</span><span class="sxs-lookup"><span data-stu-id="efc50-145">Then select **Create a new schedule**.</span></span>
5. <span data-ttu-id="efc50-146">Dans le panneau **Nouvelle planification** , tapez le nom de cette planification, par exemple : *HourlyExecution*.</span><span class="sxs-lookup"><span data-stu-id="efc50-146">On the **New schedule** blade, type in the name of this schedule, for example: *HourlyExecution*.</span></span>
6. <span data-ttu-id="efc50-147">Pour la planification **Démarrer**, définissez l’heure de début sur un incrément d’heure.</span><span class="sxs-lookup"><span data-stu-id="efc50-147">For the schedule **Start**, set the start time to an hour increment.</span></span>
7. <span data-ttu-id="efc50-148">Sélectionnez **Périodicité**, puis, dans le champ d’intervalle **Survenir chaque**, sélectionnez **1 heure**.</span><span class="sxs-lookup"><span data-stu-id="efc50-148">Select **Recurrence**, and then for **Recur every interval**, select **1 hour**.</span></span>
8. <span data-ttu-id="efc50-149">Vérifiez que l’option **Définir l’expiration** est définie sur **Non**, puis cliquez sur **Créer** pour enregistrer votre nouvelle planification.</span><span class="sxs-lookup"><span data-stu-id="efc50-149">Verify that **Set expiration** is set to **No**, and then click **Create** to save your new schedule.</span></span>
9. <span data-ttu-id="efc50-150">Dans le panneau d’options **Planifier un Runbook**, sélectionnez **Paramètres et valeurs pour l’exécution**.</span><span class="sxs-lookup"><span data-stu-id="efc50-150">On the **Schedule Runbook** options blade, select **Parameters and run settings**.</span></span> <span data-ttu-id="efc50-151">Dans le panneau **Paramètres** de Test-ResourceSchedule, entrez le nom de votre abonnement dans le champ **SubscriptionName**.</span><span class="sxs-lookup"><span data-stu-id="efc50-151">In the Test-ResourceSchedule **Parameters** blade, enter the name of your subscription in the **SubscriptionName** field.</span></span>  <span data-ttu-id="efc50-152">Il s’agit du seul paramètre requis pour le Runbook.</span><span class="sxs-lookup"><span data-stu-id="efc50-152">This is the only parameter that's required for the runbook.</span></span>  <span data-ttu-id="efc50-153">Lorsque vous avez terminé, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="efc50-153">When you're finished, click **OK**.</span></span>

<span data-ttu-id="efc50-154">Une fois terminée, la planification du Runbook devrait ressembler à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="efc50-154">The runbook schedule should look like the following when it's completed:</span></span>

![Runbook Test-ResourceSchedule configuré](./media/automation-scenario-start-stop-vm-wjson-tags/automation-schedule-config.png)<br>

## <a name="format-the-json-string"></a><span data-ttu-id="efc50-156">Formater la chaîne JSON</span><span class="sxs-lookup"><span data-stu-id="efc50-156">Format the JSON string</span></span>
<span data-ttu-id="efc50-157">Cette solution sélectionne une chaîne JSON avec un format spécifié et l’ajoute en tant que valeur d’une balise appelée Schedule.</span><span class="sxs-lookup"><span data-stu-id="efc50-157">This solution basically takes a JSON string with a specified format and adds it as the value for a tag called Schedule.</span></span> <span data-ttu-id="efc50-158">Ensuite, un Runbook répertorie l’ensemble des groupes de ressources et des machines virtuelles, puis identifie les planifications pour chaque machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="efc50-158">Then a runbook lists all resource groups and virtual machines and identifies the schedules for each virtual machine.</span></span>

<span data-ttu-id="efc50-159">Ce Runbook itère ensuite sur les machines virtuelles associées à des planifications et vérifie les actions à entreprendre.</span><span class="sxs-lookup"><span data-stu-id="efc50-159">The runbook loops over the virtual machines that have schedules attached and checks what actions should be taken.</span></span> <span data-ttu-id="efc50-160">Le code ci-après illustre un exemple de la façon dont les solutions doivent être formatées :</span><span class="sxs-lookup"><span data-stu-id="efc50-160">The following is an example of how the solutions should be formatted:</span></span>

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

<span data-ttu-id="efc50-161">Voici certaines informations détaillées concernant cette structure :</span><span class="sxs-lookup"><span data-stu-id="efc50-161">Here is some detailed information about this structure:</span></span>

1. <span data-ttu-id="efc50-162">Le format de cette structure JSON est optimisé pour contourner la limite de 256 caractères applicable à une valeur de balise unique dans Azure.</span><span class="sxs-lookup"><span data-stu-id="efc50-162">The format of this JSON structure is optimized to work around the 256-character limitation of a single tag value in Azure.</span></span>
2. <span data-ttu-id="efc50-163">*TzId* représente le fuseau horaire de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="efc50-163">*TzId* represents the time zone of the virtual machine.</span></span> <span data-ttu-id="efc50-164">Cet ID peut être obtenu à l’aide de la classe .NET TimeZoneInfo dans une session PowerShell :**[System.TimeZoneInfo]::GetSystemTimeZones()**.</span><span class="sxs-lookup"><span data-stu-id="efc50-164">This ID can be obtained by using the TimeZoneInfo .NET class in a PowerShell session--**[System.TimeZoneInfo]::GetSystemTimeZones()**.</span></span>

   ![GetSystemTimeZones dans PowerShell](./media/automation-scenario-start-stop-vm-wjson-tags/automation-get-timzone-powershell.png)

   * <span data-ttu-id="efc50-166">Les jours de la semaine sont représentés par une valeur numérique comprise entre zéro et six.</span><span class="sxs-lookup"><span data-stu-id="efc50-166">Weekdays are represented with a numeric value of zero to six.</span></span> <span data-ttu-id="efc50-167">La valeur zéro correspond à dimanche.</span><span class="sxs-lookup"><span data-stu-id="efc50-167">The value zero equals Sunday.</span></span>
   * <span data-ttu-id="efc50-168">L’heure de début est représentée par l’attribut **S** , et sa valeur est exprimée au format 24 heures.</span><span class="sxs-lookup"><span data-stu-id="efc50-168">The start time is represented with the **S** attribute, and its value is in a 24-hour format.</span></span>
   * <span data-ttu-id="efc50-169">L’heure de fin ou d’arrêt est représentée par l’attribut **E** , et sa valeur est exprimée au format 24 heures.</span><span class="sxs-lookup"><span data-stu-id="efc50-169">The end or shutdown time is represented with the **E** attribute, and its value is in a 24-hour format.</span></span>

     <span data-ttu-id="efc50-170">Si les attributs **S** et **E** présentent tous deux la valeur zéro (0), la machine virtuelle conserve l’état dans lequel elle se trouve au moment de l’évaluation.</span><span class="sxs-lookup"><span data-stu-id="efc50-170">If the **S** and **E** attributes each have a value of zero (0), the virtual machine will be left in its present state at the time of evaluation.</span></span>
3. <span data-ttu-id="efc50-171">Si vous souhaitez ignorer l’évaluation un jour spécifique de la semaine, n’ajoutez pas la section correspondant à ce jour-là.</span><span class="sxs-lookup"><span data-stu-id="efc50-171">If you want to skip evaluation for a specific day of the week, don’t add a section for that day of the week.</span></span> <span data-ttu-id="efc50-172">Dans l’exemple ci-après, l’évaluation se limite au lundi, et les autres jours de la semaine sont ignorés :</span><span class="sxs-lookup"><span data-stu-id="efc50-172">In the following example, only Monday is evaluated, and the other days of the week are ignored:</span></span>

    ```json
    {
        "TzId": "Eastern Standard Time",
        "1": {
            "S": "11",
            "E": "17"
        }
    }
    ```

## <a name="tag-resource-groups-or-vms"></a><span data-ttu-id="efc50-173">Baliser des groupes de ressources ou des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="efc50-173">Tag resource groups or VMs</span></span>
<span data-ttu-id="efc50-174">Pour arrêter des machines virtuelles, vous devez baliser ces machines ou les groupes de ressources dans lesquels elles se trouvent.</span><span class="sxs-lookup"><span data-stu-id="efc50-174">To shut down VMs, you need to tag either the VMs or the resource groups in which they're located.</span></span> <span data-ttu-id="efc50-175">Les machines virtuelles dépourvues de balise Schedule ne sont pas évaluées.</span><span class="sxs-lookup"><span data-stu-id="efc50-175">Virtual machines that don't have a Schedule tag are not evaluated.</span></span> <span data-ttu-id="efc50-176">Par conséquent, elles ne sont pas démarrées ni arrêtées.</span><span class="sxs-lookup"><span data-stu-id="efc50-176">Therefore, they aren't started or shut down.</span></span>

<span data-ttu-id="efc50-177">Vous disposez de deux méthodes pour baliser des groupes de ressources ou des machines virtuelles avec cette solution.</span><span class="sxs-lookup"><span data-stu-id="efc50-177">There are two ways to tag resource groups or VMs with this solution.</span></span> <span data-ttu-id="efc50-178">Vous pouvez le faire directement à partir du portail.</span><span class="sxs-lookup"><span data-stu-id="efc50-178">You can do it directly from the portal.</span></span> <span data-ttu-id="efc50-179">L’autre possibilité consiste à utiliser les Runbooks Add-ResourceSchedule, Update-ResourceSchedule et Remove-ResourceSchedule.</span><span class="sxs-lookup"><span data-stu-id="efc50-179">Or you can use the Add-ResourceSchedule, Update-ResourceSchedule, and Remove-ResourceSchedule runbooks.</span></span>

### <a name="tag-through-the-portal"></a><span data-ttu-id="efc50-180">Baliser par le biais du portail</span><span class="sxs-lookup"><span data-stu-id="efc50-180">Tag through the portal</span></span>
<span data-ttu-id="efc50-181">Pour baliser une machine virtuelle ou un groupe de ressources dans le portail, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="efc50-181">Follow these steps to tag a virtual machine or resource group in the portal:</span></span>

1. <span data-ttu-id="efc50-182">Aplatissez la chaîne JSON et vérifiez qu’elle ne contient pas d’espaces.</span><span class="sxs-lookup"><span data-stu-id="efc50-182">Flatten the JSON string and verify that there aren't any spaces.</span></span>  <span data-ttu-id="efc50-183">La chaîne JSON devrait ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="efc50-183">Your JSON string should look like this:</span></span>

    ```json
    {"TzId":"Eastern Standard Time","0":{"S":"11","E":"17"},"1":{"S":"9","E":"19"},"2": {"S":"9","E":"19"},"3":{"S":"9","E":"19"},"4":{"S":"9","E":"19"},"5":{"S":"9","E":"19"},"6":{"S":"11","E":"17"}}
    ```

2. <span data-ttu-id="efc50-184">Sélectionnez l’icône **Balise** pour une machine virtuelle ou un groupe de ressources afin d’y appliquer cette planification.</span><span class="sxs-lookup"><span data-stu-id="efc50-184">Select the **Tag** icon for a VM or resource group to apply this schedule.</span></span>

   ![Option de balisage de machine virtuelle](./media/automation-scenario-start-stop-vm-wjson-tags/automation-vm-tag-option.png)

3. <span data-ttu-id="efc50-186">Les balises sont définies à l’aide d’une paire clé/valeur.</span><span class="sxs-lookup"><span data-stu-id="efc50-186">Tags are defined following a key/value pair.</span></span> <span data-ttu-id="efc50-187">Tapez **Schedule** dans le champ **Clé**, puis collez la chaîne JSON dans le champ **Valeur**.</span><span class="sxs-lookup"><span data-stu-id="efc50-187">Type **Schedule** in the **Key** field, and then paste the JSON string into the **Value** field.</span></span> <span data-ttu-id="efc50-188">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="efc50-188">Click **Save**.</span></span> <span data-ttu-id="efc50-189">Votre nouvelle balise doit maintenant apparaître dans la liste des balises pour votre ressource.</span><span class="sxs-lookup"><span data-stu-id="efc50-189">Your new tag should now appear in the list of tags for your resource.</span></span>

   ![Balise de planification de machine virtuelle](./media/automation-scenario-start-stop-vm-wjson-tags/automation-vm-schedule-tag.png)

### <a name="tag-from-powershell"></a><span data-ttu-id="efc50-191">Baliser à partir de PowerShell</span><span class="sxs-lookup"><span data-stu-id="efc50-191">Tag from PowerShell</span></span>
<span data-ttu-id="efc50-192">Tous les Runbooks importés contiennent des informations d’aide au début du script qui décrivent comment exécuter les Runbooks directement à partir de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="efc50-192">All imported runbooks contain help information at the beginning of the script that describes how to execute the runbooks directly from PowerShell.</span></span> <span data-ttu-id="efc50-193">Vous pouvez appeler les Runbooks Add-ScheduleResource et Update-ScheduleResource à partir de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="efc50-193">You can call the Add-ScheduleResource and Update-ScheduleResource runbooks from PowerShell.</span></span> <span data-ttu-id="efc50-194">Pour ce faire, vous transmettez les paramètres requis qui vous permettent de créer ou de mettre à jour la balise Schedule sur une machine virtuelle ou un groupe de ressources en dehors du portail.</span><span class="sxs-lookup"><span data-stu-id="efc50-194">You do this by passing required parameters that enable you to create or update the Schedule tag on a VM or resource group outside of the portal.</span></span>

<span data-ttu-id="efc50-195">Pour créer, ajouter et supprimer des balises par le biais de PowerShell, vous devez commencer par [configurer votre environnement PowerShell pour Azure](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="efc50-195">To create, add, and delete tags through PowerShell, you first need to [set up your PowerShell environment for Azure](/powershell/azure/overview).</span></span> <span data-ttu-id="efc50-196">Après avoir effectué cette configuration, vous pouvez passer aux étapes suivantes.</span><span class="sxs-lookup"><span data-stu-id="efc50-196">After you complete the setup, you can proceed with the following steps.</span></span>

### <a name="create-a-schedule-tag-with-powershell"></a><span data-ttu-id="efc50-197">Créer une balise Schedule avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="efc50-197">Create a schedule tag with PowerShell</span></span>
1. <span data-ttu-id="efc50-198">Ouvrez une session PowerShell.</span><span class="sxs-lookup"><span data-stu-id="efc50-198">Open a PowerShell session.</span></span> <span data-ttu-id="efc50-199">Puis utilisez l’exemple ci-après pour vous authentifier avec votre compte d’identification et pour spécifier un abonnement :</span><span class="sxs-lookup"><span data-stu-id="efc50-199">Then use the following example to authenticate with your Run As account and to specify a subscription:</span></span>

    ```powershell
    $Conn = Get-AutomationConnection -Name AzureRunAsConnection
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

2. <span data-ttu-id="efc50-200">Définissez une table de hachage de planification.</span><span class="sxs-lookup"><span data-stu-id="efc50-200">Define a schedule hash table.</span></span> <span data-ttu-id="efc50-201">Voici un exemple montrant comment cette table devrait être créée :</span><span class="sxs-lookup"><span data-stu-id="efc50-201">Here is an example of how it should be constructed:</span></span>

    ```powershell
    $schedule= @{ "TzId"="Eastern Standard Time"; "0"= @{"S"="11";"E"="17"};"1"= @{"S"="9";"E"="19"};"2"= @{"S"="9";"E"="19"};"3"= @{"S"="9";"E"="19"};"4"= @{"S"="9";"E"="19"};"5"= @{"S"="9";"E"="19"};"6"= @{"S"="11";"E"="17"}}
    ```

3. <span data-ttu-id="efc50-202">Définissez les paramètres requis par le Runbook.</span><span class="sxs-lookup"><span data-stu-id="efc50-202">Define the parameters that are required by the runbook.</span></span> <span data-ttu-id="efc50-203">Dans l’exemple suivant, nous balisons une machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="efc50-203">In the following example, we are targeting a VM:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"; "VmName"="VM01";"Schedule"=$schedule}
    ```

    <span data-ttu-id="efc50-204">Si vous balisez un groupe de ressources, supprimez le paramètre *VMName* de la table de hachage $params comme suit :</span><span class="sxs-lookup"><span data-stu-id="efc50-204">If you’re tagging a resource group, remove the *VMName* parameter from the $params hash table as follows:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"; "Schedule"=$schedule}
    ```

4. <span data-ttu-id="efc50-205">Exécutez le Runbook Add-ResourceSchedule avec les paramètres ci-après pour créer la balise Schedule :</span><span class="sxs-lookup"><span data-stu-id="efc50-205">Run the Add-ResourceSchedule runbook with the following parameters to create the Schedule tag:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Add-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

5. <span data-ttu-id="efc50-206">Pour mettre à jour la balise d’un groupe de ressources ou d’une machine virtuelle, exécutez le Runbook **Update-ResourceSchedule** avec les paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="efc50-206">To update a resource group or virtual machine tag, execute the **Update-ResourceSchedule** runbook with the following parameters:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Update-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

### <a name="remove-a-schedule-tag-with-powershell"></a><span data-ttu-id="efc50-207">Supprimer une balise Schedule avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="efc50-207">Remove a schedule tag with PowerShell</span></span>
1. <span data-ttu-id="efc50-208">Ouvrez une session PowerShell et exécutez la commande ci-après pour vous authentifier avec votre compte d’identification et pour sélectionner et spécifier un abonnement :</span><span class="sxs-lookup"><span data-stu-id="efc50-208">Open a PowerShell session and run the following to authenticate with your Run As account and to select and specify a subscription:</span></span>

    ```powershell
    Conn = Get-AutomationConnection -Name AzureRunAsConnection
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

2. <span data-ttu-id="efc50-209">Définissez les paramètres requis par le Runbook.</span><span class="sxs-lookup"><span data-stu-id="efc50-209">Define the parameters that are required by the runbook.</span></span> <span data-ttu-id="efc50-210">Dans l’exemple suivant, nous balisons une machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="efc50-210">In the following example, we are targeting a VM:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01";"VmName"="VM01"}
    ```

    <span data-ttu-id="efc50-211">Si vous supprimez une balise d’un groupe de ressources, supprimez le paramètre *VMName* de la table de hachage $params comme suit :</span><span class="sxs-lookup"><span data-stu-id="efc50-211">If you’re removing a tag from a resource group, remove the *VMName* parameter from the $params hash table as follows:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"}
    ```

3. <span data-ttu-id="efc50-212">Exécutez le Runbook Remove-ResourceSchedule pour supprimer la balise Schedule :</span><span class="sxs-lookup"><span data-stu-id="efc50-212">Execute the Remove-ResourceSchedule runbook to remove the Schedule tag:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Remove-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

4. <span data-ttu-id="efc50-213">Pour mettre à jour la balise d’un groupe de ressources ou d’une machine virtuelle, exécutez le Runbook Remove-ResourceSchedule avec les paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="efc50-213">To update a resource group or virtual machine tag, execute the Remove-ResourceSchedule runbook with the following parameters:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Remove-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

> [!NOTE]
> <span data-ttu-id="efc50-214">Nous vous recommandons de surveiller de façon proactive ces Runbooks (et les états de machine virtuelle) pour vérifier que vos machines virtuelles s’arrêtent et démarrent en conséquence.</span><span class="sxs-lookup"><span data-stu-id="efc50-214">We recommend that you proactively monitor these runbooks (and the virtual machine states) to verify that your virtual machines are being shut down and started accordingly.</span></span>
>

<span data-ttu-id="efc50-215">Pour visualiser les détails du travail du Runbook Test-ResourceSchedule dans le Portail Azure, sélectionnez la vignette **Travaux** du Runbook.</span><span class="sxs-lookup"><span data-stu-id="efc50-215">To view the details of the Test-ResourceSchedule runbook job in the Azure portal, select the **Jobs** tile of the runbook.</span></span> <span data-ttu-id="efc50-216">Le résumé du travail affiche les paramètres d’entrée et le flux de sortie, en plus des informations générales sur le travail et des éventuelles exceptions.</span><span class="sxs-lookup"><span data-stu-id="efc50-216">The job summary displays the input parameters and the output stream, in addition to general information about the job and any exceptions if they occurred.</span></span>

<span data-ttu-id="efc50-217">Le **Résumé du travail** inclut les messages des flux de sortie, des flux d’avertissements et des flux d’erreurs.</span><span class="sxs-lookup"><span data-stu-id="efc50-217">The **Job Summary** includes messages from the output, warning, and error streams.</span></span> <span data-ttu-id="efc50-218">Pour visualiser les résultats détaillés de l’exécution du Runbook, sélectionnez la vignette **Sortie** .</span><span class="sxs-lookup"><span data-stu-id="efc50-218">Select the **Output** tile to view detailed results from the runbook execution.</span></span>

![Sortie Test-ResourceSchedule](./media/automation-scenario-start-stop-vm-wjson-tags/automation-job-output.png)

## <a name="next-steps"></a><span data-ttu-id="efc50-220">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="efc50-220">Next steps</span></span>
* <span data-ttu-id="efc50-221">Pour obtenir des informations sur la prise en main des Runbooks de workflow PowerShell, voir [Mon premier runbook PowerShell Workflow](automation-first-runbook-textual.md).</span><span class="sxs-lookup"><span data-stu-id="efc50-221">To get started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md).</span></span>
* <span data-ttu-id="efc50-222">Pour plus d’informations sur les types de Runbooks, sur leurs avantages et sur leurs limites, voir [Types de Runbooks Azure Automation](automation-runbook-types.md).</span><span class="sxs-lookup"><span data-stu-id="efc50-222">To learn more about runbook types, and their advantages and limitations, see [Azure Automation runbook types](automation-runbook-types.md).</span></span>
* <span data-ttu-id="efc50-223">Pour plus d’informations sur les fonctionnalités de prise en charge des scripts PowerShell, voir [Native PowerShell script support in Azure Automation](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/)(Prise en charge de scripts PowerShell natifs dans Azure Automation).</span><span class="sxs-lookup"><span data-stu-id="efc50-223">For more information about PowerShell script support features, see [Native PowerShell script support in Azure Automation](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/).</span></span>
* <span data-ttu-id="efc50-224">Pour plus d’informations sur la journalisation et la sortie de Runbook, voir [Sortie et messages de Runbook dans Azure Automation](automation-runbook-output-and-messages.md).</span><span class="sxs-lookup"><span data-stu-id="efc50-224">To learn more about runbook logging and output, see [Runbook output and messages in Azure Automation](automation-runbook-output-and-messages.md).</span></span>
* <span data-ttu-id="efc50-225">Pour plus d’informations sur un compte d’identification Azure et sur l’authentification de vos Runbooks à l’aide de ce compte, voir [Authentifier des Runbooks avec un compte d’identification Azure](automation-sec-configure-azure-runas-account.md).</span><span class="sxs-lookup"><span data-stu-id="efc50-225">To learn more about an Azure Run As account and how to authenticate your runbooks by using it, see [Authenticate runbooks with Azure Run As account](automation-sec-configure-azure-runas-account.md).</span></span>
