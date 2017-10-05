---
title: Ressources Azure Automation dans des solutions OMS | Microsoft Docs
description: "Les solutions dans OMS comprennent généralement des runbooks dans Azure Automation pour automatiser des processus tels que la collecte, le traitement et la surveillance des données.  Cet article explique comment inclure des runbooks et leurs ressources associées dans une solution."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 5281462e-f480-4e5e-9c19-022f36dce76d
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c1909183a33ed03d8165671cff25cc8b83b77733
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="adding-azure-automation-resources-to-an-oms-management-solution-preview"></a><span data-ttu-id="b25e7-104">Ajout de ressources Azure Automation pour une solution de gestion OMS (version préliminaire)</span><span class="sxs-lookup"><span data-stu-id="b25e7-104">Adding Azure Automation resources to an OMS management solution (Preview)</span></span>
> [!NOTE]
> <span data-ttu-id="b25e7-105">Il s’agit d’une documentation préliminaire pour la création de solutions de gestion dans OMS qui sont actuellement en préversion.</span><span class="sxs-lookup"><span data-stu-id="b25e7-105">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="b25e7-106">Tout schéma décrit ci-dessous est susceptible d’être modifié.</span><span class="sxs-lookup"><span data-stu-id="b25e7-106">Any schema described below is subject to change.</span></span>   


<span data-ttu-id="b25e7-107">[Les solutions de gestion dans OMS](operations-management-suite-solutions.md) comprennent généralement des runbooks dans Azure Automation pour automatiser des processus tels que la collecte, le traitement et la surveillance des données.</span><span class="sxs-lookup"><span data-stu-id="b25e7-107">[Management solutions in OMS](operations-management-suite-solutions.md) will typically include runbooks in Azure Automation to automate processes such as collecting and processing monitoring data.</span></span>  <span data-ttu-id="b25e7-108">En plus des runbooks, les comptes Automation incluent des ressources telles que des variables et des planifications qui prennent en charge les runbooks utilisés dans la solution.</span><span class="sxs-lookup"><span data-stu-id="b25e7-108">In addition to runbooks, Automation accounts includes assets such as variables and schedules that support the runbooks used in the solution.</span></span>  <span data-ttu-id="b25e7-109">Cet article explique comment inclure des runbooks et leurs ressources associées dans une solution.</span><span class="sxs-lookup"><span data-stu-id="b25e7-109">This article describes how to include runbooks and their related resources in a solution.</span></span>

> [!NOTE]
> <span data-ttu-id="b25e7-110">Les exemples dans cet article utilisent des paramètres et des variables qui sont nécessaires ou courants pour les solutions de gestion. Ils sont décrits dans la rubrique [Création de solutions de gestion dans Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span><span class="sxs-lookup"><span data-stu-id="b25e7-110">The samples in this article use parameters and variables that are either required or common to management solutions  and described in [Creating management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="b25e7-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="b25e7-111">Prerequisites</span></span>
<span data-ttu-id="b25e7-112">Cet article suppose que vous êtes déjà familiarisé avec les informations suivantes.</span><span class="sxs-lookup"><span data-stu-id="b25e7-112">This article assumes that you're already familiar with the following information.</span></span>

- <span data-ttu-id="b25e7-113">Comment [créer une solution de gestion](operations-management-suite-solutions-creating.md).</span><span class="sxs-lookup"><span data-stu-id="b25e7-113">How to [create a management solution](operations-management-suite-solutions-creating.md).</span></span>
- <span data-ttu-id="b25e7-114">La structure d’un [fichier de solution](operations-management-suite-solutions-solution-file.md).</span><span class="sxs-lookup"><span data-stu-id="b25e7-114">The structure of a [solution file](operations-management-suite-solutions-solution-file.md).</span></span>
- <span data-ttu-id="b25e7-115">Guide de [Création de modèles Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md)</span><span class="sxs-lookup"><span data-stu-id="b25e7-115">How to [author Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md)</span></span>

## <a name="automation-account"></a><span data-ttu-id="b25e7-116">Compte Automation</span><span class="sxs-lookup"><span data-stu-id="b25e7-116">Automation account</span></span>
<span data-ttu-id="b25e7-117">Toutes les ressources dans Azure Automation sont contenues dans un [compte Automation](../automation/automation-security-overview.md#automation-account-overview).</span><span class="sxs-lookup"><span data-stu-id="b25e7-117">All resources in Azure Automation are contained in an [Automation account](../automation/automation-security-overview.md#automation-account-overview).</span></span>  <span data-ttu-id="b25e7-118">Comme décrit dans [Espace de travail OMS et compte Automation](operations-management-suite-solutions.md#oms-workspace-and-automation-account), le compte Automation n’est pas inclus dans la solution de gestion mais doit exister avant l’installation de la solution.</span><span class="sxs-lookup"><span data-stu-id="b25e7-118">As described in [OMS workspace and Automation account](operations-management-suite-solutions.md#oms-workspace-and-automation-account) the Automation account isn't included in the management solution but must exist before the solution is installed.</span></span>  <span data-ttu-id="b25e7-119">Si ce n’est pas le cas, l’installation de la solution échoue.</span><span class="sxs-lookup"><span data-stu-id="b25e7-119">If it isn't available, then the solution install will fail.</span></span>

<span data-ttu-id="b25e7-120">Le nom de chaque ressource Automation inclut le nom de son compte Automation.</span><span class="sxs-lookup"><span data-stu-id="b25e7-120">The name of each Automation resource includes the name of its Automation account.</span></span>  <span data-ttu-id="b25e7-121">Pour cela, utilisez le paramètre **accountName** comme dans l’exemple suivant d’une ressource de runbook.</span><span class="sxs-lookup"><span data-stu-id="b25e7-121">This is done in the solution with the **accountName** parameter as in the following example of a runbook resource.</span></span>

    "name": "[concat(parameters('accountName'), '/MyRunbook'))]"


## <a name="runbooks"></a><span data-ttu-id="b25e7-122">Runbooks</span><span class="sxs-lookup"><span data-stu-id="b25e7-122">Runbooks</span></span>
<span data-ttu-id="b25e7-123">Vous devez inclure tous les runbooks utilisés par la solution dans le fichier de solution afin qu’ils soient créés lorsque la solution est installée.</span><span class="sxs-lookup"><span data-stu-id="b25e7-123">You should include any runbooks used by the solution in the solution file so that they're created when the solution is installed.</span></span>  <span data-ttu-id="b25e7-124">Vous ne pouvez toutefois pas inclure le corps du runbook dans le modèle, vous devez donc publier le runbook dans un emplacement public, où il sera accessible par n’importe quel utilisateur installant votre solution.</span><span class="sxs-lookup"><span data-stu-id="b25e7-124">You cannot contain the body of the runbook in the template though, so you should publish the runbook to a public location where it can be accessed by any user installing your solution.</span></span>

<span data-ttu-id="b25e7-125">Les ressources [Azure Automation runbook](../automation/automation-runbook-types.md) sont de type **Microsoft.Automation/automationAccounts/runbooks** et ont les propriétés du tableau suivant.a structure suivante.</span><span class="sxs-lookup"><span data-stu-id="b25e7-125">[Azure Automation runbook](../automation/automation-runbook-types.md) resources have a type of **Microsoft.Automation/automationAccounts/runbooks** and have the following structure.</span></span> <span data-ttu-id="b25e7-126">Cela inclut des variables et des paramètres courants, vous pouvez donc copier et coller cet extrait de code dans votre fichier de solution et modifier les noms des paramètres.</span><span class="sxs-lookup"><span data-stu-id="b25e7-126">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 

    {
        "name": "[concat(parameters('accountName'), '/', variables('Runbook').Name)]",
        "type": "Microsoft.Automation/automationAccounts/runbooks",
        "apiVersion": "[variables('AutomationApiVersion')]",
        "dependsOn": [
        ],
        "location": "[parameters('regionId')]",
        "tags": { },
        "properties": {
            "runbookType": "[variables('Runbook').Type]",
            "logProgress": "true",
            "logVerbose": "true",
            "description": "[variables('Runbook').Description]",
            "publishContentLink": {
                "uri": "[variables('Runbook').Uri]",
                "version": [variables('Runbook').Version]"
            }
        }
    }


<span data-ttu-id="b25e7-127">Les propriétés des runbooks sont décrites dans le tableau suivant.</span><span class="sxs-lookup"><span data-stu-id="b25e7-127">The properties for runbooks are described in the following table.</span></span>

| <span data-ttu-id="b25e7-128">Propriété</span><span class="sxs-lookup"><span data-stu-id="b25e7-128">Property</span></span> | <span data-ttu-id="b25e7-129">Description</span><span class="sxs-lookup"><span data-stu-id="b25e7-129">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="b25e7-130">runbookType</span><span class="sxs-lookup"><span data-stu-id="b25e7-130">runbookType</span></span> |<span data-ttu-id="b25e7-131">Spécifie les types de runbook.</span><span class="sxs-lookup"><span data-stu-id="b25e7-131">Specifies the types of the runbook.</span></span> <br><br> <span data-ttu-id="b25e7-132">Script : script PowerShell</span><span class="sxs-lookup"><span data-stu-id="b25e7-132">Script - PowerShell script</span></span> <br><span data-ttu-id="b25e7-133">PowerShell : workflow PowerShell</span><span class="sxs-lookup"><span data-stu-id="b25e7-133">PowerShell - PowerShell workflow</span></span> <br> <span data-ttu-id="b25e7-134">GraphPowerShell : runbook de script PowerShell graphique</span><span class="sxs-lookup"><span data-stu-id="b25e7-134">GraphPowerShell - Graphical PowerShell script runbook</span></span> <br> <span data-ttu-id="b25e7-135">GraphPowerShellWorkflow : runbook de workflow PowerShell graphique</span><span class="sxs-lookup"><span data-stu-id="b25e7-135">GraphPowerShellWorkflow - Graphical PowerShell workflow runbook</span></span> |
| <span data-ttu-id="b25e7-136">logProgress</span><span class="sxs-lookup"><span data-stu-id="b25e7-136">logProgress</span></span> |<span data-ttu-id="b25e7-137">Spécifie si les [enregistrements de progression](../automation/automation-runbook-output-and-messages.md) doivent être générés pour le runbook.</span><span class="sxs-lookup"><span data-stu-id="b25e7-137">Specifies whether [progress records](../automation/automation-runbook-output-and-messages.md) should be generated for the runbook.</span></span> |
| <span data-ttu-id="b25e7-138">logVerbose</span><span class="sxs-lookup"><span data-stu-id="b25e7-138">logVerbose</span></span> |<span data-ttu-id="b25e7-139">Spécifie si les [enregistrements détaillés](../automation/automation-runbook-output-and-messages.md) doivent être générés pour le runbook.</span><span class="sxs-lookup"><span data-stu-id="b25e7-139">Specifies whether [verbose records](../automation/automation-runbook-output-and-messages.md) should be generated for the runbook.</span></span> |
| <span data-ttu-id="b25e7-140">Description</span><span class="sxs-lookup"><span data-stu-id="b25e7-140">description</span></span> |<span data-ttu-id="b25e7-141">Description facultative du runbook.</span><span class="sxs-lookup"><span data-stu-id="b25e7-141">Optional description for the runbook.</span></span> |
| <span data-ttu-id="b25e7-142">publishContentLink</span><span class="sxs-lookup"><span data-stu-id="b25e7-142">publishContentLink</span></span> |<span data-ttu-id="b25e7-143">Spécifie le contenu du runbook.</span><span class="sxs-lookup"><span data-stu-id="b25e7-143">Specifies the content of the runbook.</span></span> <br><br><span data-ttu-id="b25e7-144">uri : Uri du contenu du runbook.</span><span class="sxs-lookup"><span data-stu-id="b25e7-144">uri - Uri to the content of the runbook.</span></span>  <span data-ttu-id="b25e7-145">Il s’agit d’un fichier .ps1 pour des runbooks PowerShell et Script et d’un fichier de runbook graphique exporté pour un runbook Graph.</span><span class="sxs-lookup"><span data-stu-id="b25e7-145">This will be a .ps1 file for PowerShell and Script runbooks, and an exported graphical runbook file for a Graph runbook.</span></span>  <br> <span data-ttu-id="b25e7-146">version : version du runbook pour votre propre suivi.</span><span class="sxs-lookup"><span data-stu-id="b25e7-146">version - Version of the runbook for your own tracking.</span></span> |


## <a name="automation-jobs"></a><span data-ttu-id="b25e7-147">Tâches Automation</span><span class="sxs-lookup"><span data-stu-id="b25e7-147">Automation jobs</span></span>
<span data-ttu-id="b25e7-148">Lorsque vous démarrez un Runbook dans Azure Automation, il crée un travail d’automatisation.</span><span class="sxs-lookup"><span data-stu-id="b25e7-148">When you start a runbook in Azure Automation, it creates an automation job.</span></span>  <span data-ttu-id="b25e7-149">Vous pouvez ajouter une ressource de travail d’automatisation à votre solution pour démarrer automatiquement un runbook lorsque la solution de gestion est installée.</span><span class="sxs-lookup"><span data-stu-id="b25e7-149">You can add an automation job resource to your solution to automatically start a runbook when the management solution is installed.</span></span>  <span data-ttu-id="b25e7-150">Cette méthode est généralement utilisée pour démarrer des runbooks qui sont utilisés pour la configuration initiale de la solution.</span><span class="sxs-lookup"><span data-stu-id="b25e7-150">This method is typically used to start runbooks that are used for initial configuration of the solution.</span></span>  <span data-ttu-id="b25e7-151">Pour démarrer un runbook à intervalles réguliers, créez une [planification](#schedules) et une [planification de travail](#job-schedules)</span><span class="sxs-lookup"><span data-stu-id="b25e7-151">To start a runbook at regular intervals, create a [schedule](#schedules) and a [job schedule](#job-schedules)</span></span>

<span data-ttu-id="b25e7-152">Les ressources de tâche sont de type **Microsoft.Automation/automationAccounts/jobs** et ont la structure suivante.</span><span class="sxs-lookup"><span data-stu-id="b25e7-152">Job resources have a type of **Microsoft.Automation/automationAccounts/jobs** and have the following structure.</span></span>  <span data-ttu-id="b25e7-153">Cela inclut des variables et des paramètres courants, vous pouvez donc copier et coller cet extrait de code dans votre fichier de solution et modifier les noms des paramètres.</span><span class="sxs-lookup"><span data-stu-id="b25e7-153">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 

    {
      "name": "[concat(parameters('accountName'), '/', parameters('Runbook').JobGuid)]",
      "type": "Microsoft.Automation/automationAccounts/jobs",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "dependsOn": [
        "[concat('Microsoft.Automation/automationAccounts/', parameters('accountName'), '/runbooks/', variables('Runbook').Name)]"
      ],
      "tags": { },
      "properties": {
        "runbook": {
          "name": "[variables('Runbook').Name]"
        },
        "parameters": {
          "Parameter1": "[[variables('Runbook').Parameter1]",
          "Parameter2": "[[variables('Runbook').Parameter2]"
        }
      }
    }

<span data-ttu-id="b25e7-154">Les propriétés des travaux d’automatisation sont décrites dans le tableau suivant.</span><span class="sxs-lookup"><span data-stu-id="b25e7-154">The properties for automation jobs are described in the following table.</span></span>

| <span data-ttu-id="b25e7-155">Propriété</span><span class="sxs-lookup"><span data-stu-id="b25e7-155">Property</span></span> | <span data-ttu-id="b25e7-156">Description</span><span class="sxs-lookup"><span data-stu-id="b25e7-156">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="b25e7-157">runbook</span><span class="sxs-lookup"><span data-stu-id="b25e7-157">runbook</span></span> |<span data-ttu-id="b25e7-158">Entité name unique portant le nom du runbook à démarrer.</span><span class="sxs-lookup"><span data-stu-id="b25e7-158">Single name entity with the name of the runbook to start.</span></span> |
| <span data-ttu-id="b25e7-159">parameters</span><span class="sxs-lookup"><span data-stu-id="b25e7-159">parameters</span></span> |<span data-ttu-id="b25e7-160">Entité pour chaque valeur de paramètre exigée par le runbook.</span><span class="sxs-lookup"><span data-stu-id="b25e7-160">Entity for each parameter value required by the runbook.</span></span> |

<span data-ttu-id="b25e7-161">La tâche comprend le nom du runbook et toute valeur de paramètre à lui envoyer.</span><span class="sxs-lookup"><span data-stu-id="b25e7-161">The job includes the runbook name and any parameter values to be sent to the runbook.</span></span>  <span data-ttu-id="b25e7-162">La tâche doit [dépendre](operations-management-suite-solutions-solution-file.md#resources) du runbook qu’elle démarre, car le runbook doit être créé avant la tâche.</span><span class="sxs-lookup"><span data-stu-id="b25e7-162">The job should [depend on](operations-management-suite-solutions-solution-file.md#resources) the runbook that it's starting since the runbook must be created before the job.</span></span>  <span data-ttu-id="b25e7-163">Si vous avez plusieurs runbooks qui doivent être lancés, vous pouvez définir leur ordre en rendant un travail dépendant des autres travaux qui doivent être exécutés en premier.</span><span class="sxs-lookup"><span data-stu-id="b25e7-163">If you have multiple runbooks that should be started you can define their order by having a job depend on any other jobs that should be run first.</span></span>

<span data-ttu-id="b25e7-164">Le nom d’une ressource de tâche doit contenir un GUID, qui est généralement affecté par un paramètre.</span><span class="sxs-lookup"><span data-stu-id="b25e7-164">The name of a job resource must contain a GUID which is typically assigned by a parameter.</span></span>  <span data-ttu-id="b25e7-165">Vous trouverez plus d’informations sur les paramètres GUID dans la rubrique [Création de solutions dans Operations Management Suite (OMS)](operations-management-suite-solutions-solution-file.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="b25e7-165">You can read more about GUID parameters in [Creating solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-solution-file.md#parameters).</span></span>  


## <a name="certificates"></a><span data-ttu-id="b25e7-166">Certificats</span><span class="sxs-lookup"><span data-stu-id="b25e7-166">Certificates</span></span>
<span data-ttu-id="b25e7-167">Les [certificats Azure Automation](../automation/automation-certificates.md) sont de type **Microsoft.Automation/automationAccounts/certificate** et ont la structure suivante.</span><span class="sxs-lookup"><span data-stu-id="b25e7-167">[Azure Automation certificates](../automation/automation-certificates.md) have a type of **Microsoft.Automation/automationAccounts/certificates** and have the following structure.</span></span> <span data-ttu-id="b25e7-168">Cela inclut des variables et des paramètres courants, vous pouvez donc copier et coller cet extrait de code dans votre fichier de solution et modifier les noms des paramètres.</span><span class="sxs-lookup"><span data-stu-id="b25e7-168">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 

    {
      "name": "[concat(parameters('accountName'), '/', variables('Certificate').Name)]",
      "type": "Microsoft.Automation/automationAccounts/certificates",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "base64Value": "[variables('Certificate').Base64Value]",
        "thumbprint": "[variables('Certificate').Thumbprint]"
      }
    }



<span data-ttu-id="b25e7-169">Les propriétés des ressources de certificat sont décrites dans le tableau suivant.</span><span class="sxs-lookup"><span data-stu-id="b25e7-169">The properties for Certificates resources are described in the following table.</span></span>

| <span data-ttu-id="b25e7-170">Propriété</span><span class="sxs-lookup"><span data-stu-id="b25e7-170">Property</span></span> | <span data-ttu-id="b25e7-171">Description</span><span class="sxs-lookup"><span data-stu-id="b25e7-171">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="b25e7-172">base64Value</span><span class="sxs-lookup"><span data-stu-id="b25e7-172">base64Value</span></span> |<span data-ttu-id="b25e7-173">Valeur de base 64 pour le certificat.</span><span class="sxs-lookup"><span data-stu-id="b25e7-173">Base 64 value for the certificate.</span></span> |
| <span data-ttu-id="b25e7-174">thumbprint</span><span class="sxs-lookup"><span data-stu-id="b25e7-174">thumbprint</span></span> |<span data-ttu-id="b25e7-175">Thumbprint pour le certificat.</span><span class="sxs-lookup"><span data-stu-id="b25e7-175">Thumbprint for the certificate.</span></span> |



## <a name="credentials"></a><span data-ttu-id="b25e7-176">Informations d'identification</span><span class="sxs-lookup"><span data-stu-id="b25e7-176">Credentials</span></span>
<span data-ttu-id="b25e7-177">Les [informations d'identification Azure Automation](../automation/automation-credentials.md) sont de type **Microsoft.Automation/automationAccounts/credentials** et ont la structure suivante.</span><span class="sxs-lookup"><span data-stu-id="b25e7-177">[Azure Automation credentials](../automation/automation-credentials.md) have a type of **Microsoft.Automation/automationAccounts/credentials** and have the following structure.</span></span>  <span data-ttu-id="b25e7-178">Cela inclut des variables et des paramètres courants, vous pouvez donc copier et coller cet extrait de code dans votre fichier de solution et modifier les noms des paramètres.</span><span class="sxs-lookup"><span data-stu-id="b25e7-178">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 


    {
      "name": "[concat(parameters('accountName'), '/', variables('Credential').Name)]",
      "type": "Microsoft.Automation/automationAccounts/credentials",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "userName": "[parameters('credentialUsername')]",
        "password": "[parameters('credentialPassword')]"
      }
    }

<span data-ttu-id="b25e7-179">Les propriétés des ressources d’informations d’identification sont décrites dans le tableau suivant.</span><span class="sxs-lookup"><span data-stu-id="b25e7-179">The properties for Credential resources are described in the following table.</span></span>

| <span data-ttu-id="b25e7-180">Propriété</span><span class="sxs-lookup"><span data-stu-id="b25e7-180">Property</span></span> | <span data-ttu-id="b25e7-181">Description</span><span class="sxs-lookup"><span data-stu-id="b25e7-181">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="b25e7-182">userName</span><span class="sxs-lookup"><span data-stu-id="b25e7-182">userName</span></span> |<span data-ttu-id="b25e7-183">Nom d’utilisateur des informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="b25e7-183">User name for the credential.</span></span> |
| <span data-ttu-id="b25e7-184">password</span><span class="sxs-lookup"><span data-stu-id="b25e7-184">password</span></span> |<span data-ttu-id="b25e7-185">Mot de passe des informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="b25e7-185">Password for the credential.</span></span> |


## <a name="schedules"></a><span data-ttu-id="b25e7-186">Planifications</span><span class="sxs-lookup"><span data-stu-id="b25e7-186">Schedules</span></span>
<span data-ttu-id="b25e7-187">Les [planifications Azure Automation](../automation/automation-schedules.md) sont de type **Microsoft.Automation/automationAccounts/schedules** et ont la structure suivante.</span><span class="sxs-lookup"><span data-stu-id="b25e7-187">[Azure Automation schedules](../automation/automation-schedules.md) have a type of **Microsoft.Automation/automationAccounts/schedules** and have the the following structure.</span></span> <span data-ttu-id="b25e7-188">Cela inclut des variables et des paramètres courants, vous pouvez donc copier et coller cet extrait de code dans votre fichier de solution et modifier les noms des paramètres.</span><span class="sxs-lookup"><span data-stu-id="b25e7-188">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 

    {
      "name": "[concat(parameters('accountName'), '/', variables('Schedule').Name)]",
      "type": "microsoft.automation/automationAccounts/schedules",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "description": "[variables('Schedule').Description]",
        "startTime": "[parameters('scheduleStartTime')]",
        "timeZone": "[parameters('scheduleTimeZone')]",
        "isEnabled": "[variables('Schedule').IsEnabled]",
        "interval": "[variables('Schedule').Interval]",
        "frequency": "[variables('Schedule').Frequency]"
      }
    }

<span data-ttu-id="b25e7-189">Les propriétés des ressources de planification sont décrites dans le tableau suivant.</span><span class="sxs-lookup"><span data-stu-id="b25e7-189">The properties for schedule resources are described in the following table.</span></span>

| <span data-ttu-id="b25e7-190">Propriété</span><span class="sxs-lookup"><span data-stu-id="b25e7-190">Property</span></span> | <span data-ttu-id="b25e7-191">Description</span><span class="sxs-lookup"><span data-stu-id="b25e7-191">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="b25e7-192">Description</span><span class="sxs-lookup"><span data-stu-id="b25e7-192">description</span></span> |<span data-ttu-id="b25e7-193">Description facultative de la planification.</span><span class="sxs-lookup"><span data-stu-id="b25e7-193">Optional description for the schedule.</span></span> |
| <span data-ttu-id="b25e7-194">startTime</span><span class="sxs-lookup"><span data-stu-id="b25e7-194">startTime</span></span> |<span data-ttu-id="b25e7-195">Spécifie l’heure de début d’une planification en tant qu’objet DateTime.</span><span class="sxs-lookup"><span data-stu-id="b25e7-195">Specifies the start time of a schedule as a DateTime object.</span></span> <span data-ttu-id="b25e7-196">Une chaîne peut être fournie si elle peut être convertie en un élément DateTime valide.</span><span class="sxs-lookup"><span data-stu-id="b25e7-196">A string can be provided if it can be converted to a valid DateTime.</span></span> |
| <span data-ttu-id="b25e7-197">isEnabled</span><span class="sxs-lookup"><span data-stu-id="b25e7-197">isEnabled</span></span> |<span data-ttu-id="b25e7-198">Spécifie si la planification est activée.</span><span class="sxs-lookup"><span data-stu-id="b25e7-198">Specifies whether the schedule is enabled.</span></span> |
| <span data-ttu-id="b25e7-199">interval</span><span class="sxs-lookup"><span data-stu-id="b25e7-199">interval</span></span> |<span data-ttu-id="b25e7-200">Le type d’intervalle pour la planification.</span><span class="sxs-lookup"><span data-stu-id="b25e7-200">The type of interval for the schedule.</span></span><br><br><span data-ttu-id="b25e7-201">day</span><span class="sxs-lookup"><span data-stu-id="b25e7-201">day</span></span><br><span data-ttu-id="b25e7-202">hour</span><span class="sxs-lookup"><span data-stu-id="b25e7-202">hour</span></span> |
| <span data-ttu-id="b25e7-203">frequency</span><span class="sxs-lookup"><span data-stu-id="b25e7-203">frequency</span></span> |<span data-ttu-id="b25e7-204">Fréquence à laquelle la planification doit se déclencher en nombre de jours ou d’heures.</span><span class="sxs-lookup"><span data-stu-id="b25e7-204">Frequency that the schedule should fire in number of days or hours.</span></span> |

<span data-ttu-id="b25e7-205">Les planifications doivent avoir une heure de début avec une valeur supérieure à l’heure actuelle.</span><span class="sxs-lookup"><span data-stu-id="b25e7-205">Schedules must have a start time with a value greater than the current time.</span></span>  <span data-ttu-id="b25e7-206">Vous ne pouvez pas fournir cette valeur avec une variable puisque vous n’auriez aucun moyen de savoir l’heure d’installation.</span><span class="sxs-lookup"><span data-stu-id="b25e7-206">You cannot provide this value with a variable since you would have no way of knowing when it's going to be installed.</span></span>

<span data-ttu-id="b25e7-207">Utilisez une des deux stratégies suivantes lors de l’utilisation des ressources de planification dans une solution.</span><span class="sxs-lookup"><span data-stu-id="b25e7-207">Use one of the following two strategies when using schedule resources in a solution.</span></span>

- <span data-ttu-id="b25e7-208">Utilisez un paramètre pour l’heure de début de la planification.</span><span class="sxs-lookup"><span data-stu-id="b25e7-208">Use a parameter for the start time of the schedule.</span></span>  <span data-ttu-id="b25e7-209">Cela invite l’utilisateur à fournir une valeur lorsqu’il installe la solution.</span><span class="sxs-lookup"><span data-stu-id="b25e7-209">This will prompt the user to provide a value when they install the solution.</span></span>  <span data-ttu-id="b25e7-210">Si vous avez plusieurs planifications, vous pouvez utiliser une valeur de paramètre unique pour plusieurs d'entre eux.</span><span class="sxs-lookup"><span data-stu-id="b25e7-210">If you have multiple schedules, you could use a single parameter value for more than one of them.</span></span>
- <span data-ttu-id="b25e7-211">Créez les planifications à l’aide d’un runbook qui démarre lorsque la solution est installée.</span><span class="sxs-lookup"><span data-stu-id="b25e7-211">Create the schedules using a runbook that starts when the solution is installed.</span></span>  <span data-ttu-id="b25e7-212">Cela supprime la nécessité pour l’utilisateur de spécifier une heure, mais vous ne pouvez pas inclure la planification dans votre solution, elle sera donc supprimée en même temps que la solution.</span><span class="sxs-lookup"><span data-stu-id="b25e7-212">This removes the requirement of the user to specify a time, but you can't contain the schedule in your solution so it will be removed when the solution is removed.</span></span>


### <a name="job-schedules"></a><span data-ttu-id="b25e7-213">Planifications de travaux</span><span class="sxs-lookup"><span data-stu-id="b25e7-213">Job schedules</span></span>
<span data-ttu-id="b25e7-214">Les ressources de planification de tâche lient un runbook à une planification.</span><span class="sxs-lookup"><span data-stu-id="b25e7-214">Job schedule resources link a runbook with a schedule.</span></span>  <span data-ttu-id="b25e7-215">Elles ont un type de **Microsoft.Automation/automationAccounts/jobSchedules** et la structure suivante.</span><span class="sxs-lookup"><span data-stu-id="b25e7-215">They have a type of **Microsoft.Automation/automationAccounts/jobSchedules** and have the the following structure.</span></span>  <span data-ttu-id="b25e7-216">Cela inclut des variables et des paramètres courants, vous pouvez donc copier et coller cet extrait de code dans votre fichier de solution et modifier les noms des paramètres.</span><span class="sxs-lookup"><span data-stu-id="b25e7-216">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 

    {
      "name": "[concat(parameters('accountName'), '/', variables('Schedule').LinkGuid)]",
      "type": "microsoft.automation/automationAccounts/jobSchedules",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "dependsOn": [
        "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
        "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]"
      ],
      "tags": {
      },
      "properties": {
        "schedule": {
          "name": "[variables('Schedule').Name]"
        },
        "runbook": {
          "name": "[variables('Runbook').Name]"
        }
      }
    }


<span data-ttu-id="b25e7-217">Les propriétés des planifications de travail sont décrites dans le tableau suivant.</span><span class="sxs-lookup"><span data-stu-id="b25e7-217">The properties for job schedules are described in the following table.</span></span>

| <span data-ttu-id="b25e7-218">Propriété</span><span class="sxs-lookup"><span data-stu-id="b25e7-218">Property</span></span> | <span data-ttu-id="b25e7-219">Description</span><span class="sxs-lookup"><span data-stu-id="b25e7-219">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="b25e7-220">nom de la planification</span><span class="sxs-lookup"><span data-stu-id="b25e7-220">schedule name</span></span> |<span data-ttu-id="b25e7-221">Entité **name** unique portant le nom de la planification.</span><span class="sxs-lookup"><span data-stu-id="b25e7-221">Single **name** entity with the name of the schedule.</span></span> |
| <span data-ttu-id="b25e7-222">nom du runbook</span><span class="sxs-lookup"><span data-stu-id="b25e7-222">runbook name</span></span>  |<span data-ttu-id="b25e7-223">Entité **name** unique portant le nom du runbook.</span><span class="sxs-lookup"><span data-stu-id="b25e7-223">Single **name** entity with the name of the runbook.</span></span>  |



## <a name="variables"></a><span data-ttu-id="b25e7-224">Variables</span><span class="sxs-lookup"><span data-stu-id="b25e7-224">Variables</span></span>
<span data-ttu-id="b25e7-225">Les [variables Azure Automation](../automation/automation-variables.md) sont de type **Microsoft.Automation/automationAccounts/variables** et ont la structure suivante.</span><span class="sxs-lookup"><span data-stu-id="b25e7-225">[Azure Automation variables](../automation/automation-variables.md) have a type of **Microsoft.Automation/automationAccounts/variables** and have the following structure.</span></span>  <span data-ttu-id="b25e7-226">Cela inclut des variables et des paramètres courants, vous pouvez donc copier et coller cet extrait de code dans votre fichier de solution et modifier les noms des paramètres.</span><span class="sxs-lookup"><span data-stu-id="b25e7-226">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span>

    {
      "name": "[concat(parameters('accountName'), '/', variables('Variable').Name)]",
      "type": "microsoft.automation/automationAccounts/variables",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "description": "[variables('Variable').Description]",
        "isEncrypted": "[variables('Variable').Encrypted]",
        "type": "[variables('Variable').Type]",
        "value": "[variables('Variable').Value]"
      }
    }

<span data-ttu-id="b25e7-227">Les propriétés des ressources de variable sont décrites dans le tableau suivant.</span><span class="sxs-lookup"><span data-stu-id="b25e7-227">The properties for variable resources are described in the following table.</span></span>

| <span data-ttu-id="b25e7-228">Propriété</span><span class="sxs-lookup"><span data-stu-id="b25e7-228">Property</span></span> | <span data-ttu-id="b25e7-229">Description</span><span class="sxs-lookup"><span data-stu-id="b25e7-229">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="b25e7-230">Description</span><span class="sxs-lookup"><span data-stu-id="b25e7-230">description</span></span> | <span data-ttu-id="b25e7-231">Description facultative de la variable.</span><span class="sxs-lookup"><span data-stu-id="b25e7-231">Optional description for the variable.</span></span> |
| <span data-ttu-id="b25e7-232">isEncrypted</span><span class="sxs-lookup"><span data-stu-id="b25e7-232">isEncrypted</span></span> | <span data-ttu-id="b25e7-233">Spécifie si la variable doit être chiffrée.</span><span class="sxs-lookup"><span data-stu-id="b25e7-233">Specifies whether the variable should be encrypted.</span></span> |
| <span data-ttu-id="b25e7-234">type</span><span class="sxs-lookup"><span data-stu-id="b25e7-234">type</span></span> | <span data-ttu-id="b25e7-235">Cette propriété n’a actuellement aucun effet.</span><span class="sxs-lookup"><span data-stu-id="b25e7-235">This property currently has no effect.</span></span>  <span data-ttu-id="b25e7-236">Le type de données de la variable sera déterminé par la valeur initiale.</span><span class="sxs-lookup"><span data-stu-id="b25e7-236">The data type of the variable will be determined by the initial value.</span></span> |
| <span data-ttu-id="b25e7-237">value</span><span class="sxs-lookup"><span data-stu-id="b25e7-237">value</span></span> | <span data-ttu-id="b25e7-238">Valeur de la variable.</span><span class="sxs-lookup"><span data-stu-id="b25e7-238">Value for the variable.</span></span> |

> [!NOTE]
> <span data-ttu-id="b25e7-239">La propriété **type** n’a actuellement aucun effet sur la variable en train d’être créée.</span><span class="sxs-lookup"><span data-stu-id="b25e7-239">The **type** property currently has no effect on the variable being created.</span></span>  <span data-ttu-id="b25e7-240">Le type de données de la variable sera déterminé par la valeur.</span><span class="sxs-lookup"><span data-stu-id="b25e7-240">The data type for the variable will be determined by the value.</span></span>  

<span data-ttu-id="b25e7-241">Si vous définissez la valeur initiale pour la variable, elle doit être configurée en tant que type de données correct.</span><span class="sxs-lookup"><span data-stu-id="b25e7-241">If you set the initial value for the variable, it must be configured as the correct data type.</span></span>  <span data-ttu-id="b25e7-242">Le tableau suivant fournit les différents types de données autorisés et leur syntaxe.</span><span class="sxs-lookup"><span data-stu-id="b25e7-242">The following table provides the different data types allowable and their syntax.</span></span>  <span data-ttu-id="b25e7-243">Notez que les valeurs dans JSON doivent toujours être placées entre guillemets avec les caractères spéciaux à l’intérieur des guillemets.</span><span class="sxs-lookup"><span data-stu-id="b25e7-243">Note that values in JSON are expected to always be enclosed in quotes with any special characters within the quotes.</span></span>  <span data-ttu-id="b25e7-244">Par exemple, une valeur de chaîne serait spécifiée en plaçant la chaîne entre guillemets (en utilisant le caractère d’échappement (\\)), tandis qu’une valeur numérique serait spécifiée avec une seule paire de guillemets.</span><span class="sxs-lookup"><span data-stu-id="b25e7-244">For example, a string value would be specified by quotes around the string (using the escape character (\\)) while a numeric value would be specified with one set of quotes.</span></span>

| <span data-ttu-id="b25e7-245">Type de données</span><span class="sxs-lookup"><span data-stu-id="b25e7-245">Data type</span></span> | <span data-ttu-id="b25e7-246">Description</span><span class="sxs-lookup"><span data-stu-id="b25e7-246">Description</span></span> | <span data-ttu-id="b25e7-247">Exemple</span><span class="sxs-lookup"><span data-stu-id="b25e7-247">Example</span></span> | <span data-ttu-id="b25e7-248">Est résolu en</span><span class="sxs-lookup"><span data-stu-id="b25e7-248">Resolves to</span></span> |
|:--|:--|:--|:--|
| <span data-ttu-id="b25e7-249">string</span><span class="sxs-lookup"><span data-stu-id="b25e7-249">string</span></span>   | <span data-ttu-id="b25e7-250">Placer la valeur entre des guillemets doubles.</span><span class="sxs-lookup"><span data-stu-id="b25e7-250">Enclose value in double quotes.</span></span>  | <span data-ttu-id="b25e7-251">"\"Hello world\""</span><span class="sxs-lookup"><span data-stu-id="b25e7-251">"\"Hello world\""</span></span> | <span data-ttu-id="b25e7-252">"Hello world"</span><span class="sxs-lookup"><span data-stu-id="b25e7-252">"Hello world"</span></span> |
| <span data-ttu-id="b25e7-253">numérique</span><span class="sxs-lookup"><span data-stu-id="b25e7-253">numeric</span></span>  | <span data-ttu-id="b25e7-254">Valeur numérique avec des guillemets simples.</span><span class="sxs-lookup"><span data-stu-id="b25e7-254">Numeric value with single quotes.</span></span>| <span data-ttu-id="b25e7-255">"64"</span><span class="sxs-lookup"><span data-stu-id="b25e7-255">"64"</span></span> | <span data-ttu-id="b25e7-256">64</span><span class="sxs-lookup"><span data-stu-id="b25e7-256">64</span></span> |
| <span data-ttu-id="b25e7-257">booléenne</span><span class="sxs-lookup"><span data-stu-id="b25e7-257">boolean</span></span>  | <span data-ttu-id="b25e7-258">**true** ou **false** entre guillemets.</span><span class="sxs-lookup"><span data-stu-id="b25e7-258">**true** or **false** in quotes.</span></span>  <span data-ttu-id="b25e7-259">Notez que cette valeur doit être en minuscules.</span><span class="sxs-lookup"><span data-stu-id="b25e7-259">Note that this value must be lowercase.</span></span> | <span data-ttu-id="b25e7-260">"true"</span><span class="sxs-lookup"><span data-stu-id="b25e7-260">"true"</span></span> | <span data-ttu-id="b25e7-261">true</span><span class="sxs-lookup"><span data-stu-id="b25e7-261">true</span></span> |
| <span data-ttu-id="b25e7-262">Datetime</span><span class="sxs-lookup"><span data-stu-id="b25e7-262">datetime</span></span> | <span data-ttu-id="b25e7-263">Valeur de date sérialisée.</span><span class="sxs-lookup"><span data-stu-id="b25e7-263">Serialized date value.</span></span><br><span data-ttu-id="b25e7-264">Vous pouvez utiliser la cmdlet ConvertTo-Json dans PowerShell pour générer cette valeur pour une date particulière.</span><span class="sxs-lookup"><span data-stu-id="b25e7-264">You can use the ConvertTo-Json cmdlet in PowerShell to generate this value for a particular date.</span></span><br><span data-ttu-id="b25e7-265">Exemple : get-date "5/24/2017 13:14:57" \\</span><span class="sxs-lookup"><span data-stu-id="b25e7-265">Example: get-date "5/24/2017 13:14:57" \\</span></span>| <span data-ttu-id="b25e7-266">ConvertTo-Json</span><span class="sxs-lookup"><span data-stu-id="b25e7-266">ConvertTo-Json</span></span> | <span data-ttu-id="b25e7-267">"\\/Date(1495656897378)\\/"</span><span class="sxs-lookup"><span data-stu-id="b25e7-267">"\\/Date(1495656897378)\\/"</span></span> | <span data-ttu-id="b25e7-268">2017-05-24 13:14:57</span><span class="sxs-lookup"><span data-stu-id="b25e7-268">2017-05-24 13:14:57</span></span> |

## <a name="modules"></a><span data-ttu-id="b25e7-269">Modules</span><span class="sxs-lookup"><span data-stu-id="b25e7-269">Modules</span></span>
<span data-ttu-id="b25e7-270">Votre solution de gestion ne doit pas nécessairement définir de [modules globaux](../automation/automation-integration-modules.md) utilisés par vos runbooks, car ils sont toujours disponibles dans votre compte Automation.</span><span class="sxs-lookup"><span data-stu-id="b25e7-270">Your management solution does not need to define [global modules](../automation/automation-integration-modules.md) used by your runbooks because they will always be available in your Automation account.</span></span>  <span data-ttu-id="b25e7-271">Vous devez inclure une ressource pour tout module utilisé par vos runbooks.</span><span class="sxs-lookup"><span data-stu-id="b25e7-271">You do need to include a resource for any other module used by your runbooks.</span></span>

<span data-ttu-id="b25e7-272">Les [modules d’intégration](../automation/automation-integration-modules.md) sont de type **Microsoft.Automation/automationAccounts/modules** et ont la structure suivante.</span><span class="sxs-lookup"><span data-stu-id="b25e7-272">[Integration modules](../automation/automation-integration-modules.md) have a type of **Microsoft.Automation/automationAccounts/modules** and have the following structure.</span></span>  <span data-ttu-id="b25e7-273">Cela inclut des variables et des paramètres courants, vous pouvez donc copier et coller cet extrait de code dans votre fichier de solution et modifier les noms des paramètres.</span><span class="sxs-lookup"><span data-stu-id="b25e7-273">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span>

    {
      "name": "[concat(parameters('accountName'), '/', variables('Module').Name)]",
      "type": "Microsoft.Automation/automationAccounts/modules",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "dependsOn": [
      ],
      "properties": {
        "contentLink": {
          "uri": "[variables('Module').Uri]"
        }
      }
    }


<span data-ttu-id="b25e7-274">Les propriétés des ressources de module sont décrites dans le tableau suivant.</span><span class="sxs-lookup"><span data-stu-id="b25e7-274">The properties for module resources are described in the following table.</span></span>

| <span data-ttu-id="b25e7-275">Propriété</span><span class="sxs-lookup"><span data-stu-id="b25e7-275">Property</span></span> | <span data-ttu-id="b25e7-276">Description</span><span class="sxs-lookup"><span data-stu-id="b25e7-276">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="b25e7-277">contentLink</span><span class="sxs-lookup"><span data-stu-id="b25e7-277">contentLink</span></span> |<span data-ttu-id="b25e7-278">Spécifie le contenu du module.</span><span class="sxs-lookup"><span data-stu-id="b25e7-278">Specifies the content of the module.</span></span> <br><br><span data-ttu-id="b25e7-279">uri : Uri du contenu du module.</span><span class="sxs-lookup"><span data-stu-id="b25e7-279">uri - Uri to the content of the module.</span></span>  <span data-ttu-id="b25e7-280">Il s’agit d’un fichier .ps1 pour des runbooks PowerShell et Script et d’un fichier de runbook graphique exporté pour un runbook Graph.</span><span class="sxs-lookup"><span data-stu-id="b25e7-280">This will be a .ps1 file for PowerShell and Script runbooks, and an exported graphical runbook file for a Graph runbook.</span></span>  <br> <span data-ttu-id="b25e7-281">version : version du module pour votre propre suivi.</span><span class="sxs-lookup"><span data-stu-id="b25e7-281">version - Version of the module for your own tracking.</span></span> |

<span data-ttu-id="b25e7-282">Le runbook doit dépendre de la ressource de module pour vous assurer que cette dernière est créée avant le runbook.</span><span class="sxs-lookup"><span data-stu-id="b25e7-282">The runbook should depend on the module resource to ensure that it's created before the runbook.</span></span>

### <a name="updating-modules"></a><span data-ttu-id="b25e7-283">Mise à jour des modules</span><span class="sxs-lookup"><span data-stu-id="b25e7-283">Updating modules</span></span>
<span data-ttu-id="b25e7-284">Si vous mettez à jour une solution de gestion qui inclut un runbook qui utilise une planification alors que la nouvelle version de votre solution comprend un nouveau module utilisé par ce runbook, le runbook peut utiliser l’ancienne version du module.</span><span class="sxs-lookup"><span data-stu-id="b25e7-284">If you update a management solution that includes a runbook that uses a schedule, and the new version of your solution has a new module used by that runbook, then the runbook may use the old version of the module.</span></span>  <span data-ttu-id="b25e7-285">Vous devez inclure les runbooks suivants dans votre solution et créer une tâche à exécuter avant les autres runbooks.</span><span class="sxs-lookup"><span data-stu-id="b25e7-285">You should include the following runbooks in your solution and create a job to run them before any other runbooks.</span></span>  <span data-ttu-id="b25e7-286">Cela garantit que tous les modules sont mis à jour comme exigé avant que les runbooks ne soient chargés.</span><span class="sxs-lookup"><span data-stu-id="b25e7-286">This will ensure that any modules are updated as required before the runbooks are loaded.</span></span>

* <span data-ttu-id="b25e7-287">[Update-ModulesinAutomationToLatestVersion](https://www.powershellgallery.com/packages/Update-ModulesInAutomationToLatestVersion/1.03/DisplayScript) vous assure que tous les modules utilisés par des runbooks de votre solution sont à la version la plus récente.</span><span class="sxs-lookup"><span data-stu-id="b25e7-287">[Update-ModulesinAutomationToLatestVersion](https://www.powershellgallery.com/packages/Update-ModulesInAutomationToLatestVersion/1.03/DisplayScript) will ensure that all of the modules used by runbooks in your solution are the latest version.</span></span>  
* <span data-ttu-id="b25e7-288">[ReRegisterAutomationSchedule-MS-Mgmt](https://www.powershellgallery.com/packages/ReRegisterAutomationSchedule-MS-Mgmt/1.0/DisplayScript) enregistre de nouveau toutes les ressources de planification pour vous assurer que les runbooks qui y sont liés utilisent les modules actuels.</span><span class="sxs-lookup"><span data-stu-id="b25e7-288">[ReRegisterAutomationSchedule-MS-Mgmt](https://www.powershellgallery.com/packages/ReRegisterAutomationSchedule-MS-Mgmt/1.0/DisplayScript) will reregister all of the schedule resources to ensure that the runbooks linked to them with use the latest modules.</span></span>




## <a name="sample"></a><span data-ttu-id="b25e7-289">Exemple</span><span class="sxs-lookup"><span data-stu-id="b25e7-289">Sample</span></span>
<span data-ttu-id="b25e7-290">L’exemple de solution ci-après inclut les ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="b25e7-290">Following is a sample of a solution that include that includes the following resources:</span></span>

- <span data-ttu-id="b25e7-291">Runbook.</span><span class="sxs-lookup"><span data-stu-id="b25e7-291">Runbook.</span></span>  <span data-ttu-id="b25e7-292">Il s’agit d’un exemple de runbook stocké dans un référentiel GitHub public.</span><span class="sxs-lookup"><span data-stu-id="b25e7-292">This is a sample runbook stored in a public GitHub repository.</span></span>
- <span data-ttu-id="b25e7-293">Un travail d’automatisation qui démarre le runbook lorsque la solution est installée.</span><span class="sxs-lookup"><span data-stu-id="b25e7-293">Automation job that starts the runbook when the solution is installed.</span></span>
- <span data-ttu-id="b25e7-294">Planification et planification de travaux pour démarrer le runbook à intervalles réguliers.</span><span class="sxs-lookup"><span data-stu-id="b25e7-294">Schedule and job schedule to start the runbook at regular intervals.</span></span>
- <span data-ttu-id="b25e7-295">Certificat.</span><span class="sxs-lookup"><span data-stu-id="b25e7-295">Certificate.</span></span>
- <span data-ttu-id="b25e7-296">Informations d'identification.</span><span class="sxs-lookup"><span data-stu-id="b25e7-296">Credential.</span></span>
- <span data-ttu-id="b25e7-297">Variable.</span><span class="sxs-lookup"><span data-stu-id="b25e7-297">Variable.</span></span>
- <span data-ttu-id="b25e7-298">Module.</span><span class="sxs-lookup"><span data-stu-id="b25e7-298">Module.</span></span>  <span data-ttu-id="b25e7-299">Il s’agit du [module OMSIngestionAPI](https://www.powershellgallery.com/packages/OMSIngestionAPI/1.5) pour écrire des données dans Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="b25e7-299">This is the [OMSIngestionAPI module](https://www.powershellgallery.com/packages/OMSIngestionAPI/1.5) for writing data to Log Analytics.</span></span> 

<span data-ttu-id="b25e7-300">L’exemple utilise des variables de [paramètres de solution standard](operations-management-suite-solutions-solution-file.md#parameters) qui seraient généralement utilisées dans une solution, par opposition aux valeurs de codage en dur dans les définitions de ressource.</span><span class="sxs-lookup"><span data-stu-id="b25e7-300">The sample uses [standard solution parameters](operations-management-suite-solutions-solution-file.md#parameters) variables that would commonly be used in a solution as opposed to hardcoding values in the resource definitions.</span></span>


    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "workspaceName": {
          "type": "string",
          "metadata": {
            "Description": "Name of Log Analytics workspace."
          }
        },
        "accountName": {
          "type": "string",
          "metadata": {
            "Description": "Name of Automation account."
          }
        },
        "workspaceregionId": {
          "type": "string",
          "metadata": {
            "Description": "Region of Log Analytics workspace."
          }
        },
        "regionId": {
          "type": "string",
          "metadata": {
            "Description": "Region of Automation account."
          }
        },
        "pricingTier": {
          "type": "string",
          "metadata": {
            "Description": "Pricing tier of both Log Analytics workspace and Azure Automation account."
          }
        },
        "certificateBase64Value": {
          "type": "string",
          "metadata": {
            "Description": "Base 64 value for certificate."
          }
        },
        "certificateThumbprint": {
          "type": "securestring",
          "metadata": {
            "Description": "Thumbprint for certificate."
          }
        },
        "credentialUsername": {
          "type": "string",
          "metadata": {
            "Description": "Username for credential."
          }
        },
        "credentialPassword": {
          "type": "securestring",
          "metadata": {
            "Description": "Password for credential."
          }
        },
        "scheduleStartTime": {
          "type": "string",
          "metadata": {
            "Description": "Start time for shedule."
          }
        },
        "scheduleTimeZone": {
          "type": "string",
          "metadata": {
            "Description": "Time zone for schedule."
          }
        },
        "scheduleLinkGuid": {
          "type": "string",
          "metadata": {
            "description": "GUID for the schedule link to runbook.",
            "control": "guid"
          }
        },
        "runbookJobGuid": {
          "type": "string",
          "metadata": {
            "description": "GUID for the runbook job.",
            "control": "guid"
          }
        }
      },
      "variables": {
        "SolutionName": "MySolution",
        "SolutionVersion": "1.0",
        "SolutionPublisher": "Contoso",
        "ProductName": "SampleSolution",
    
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31",
    
        "Runbook": {
          "Name": "MyRunbook",
          "Description": "Sample runbook",
          "Type": "PowerShell",
          "Uri": "https://raw.githubusercontent.com/user/myrepo/master/samples/MyRunbook.ps1",
          "JobGuid": "[parameters('runbookJobGuid')]"
        },
    
        "Certificate": {
          "Name": "MyCertificate",
          "Base64Value": "[parameters('certificateBase64Value')]",
          "Thumbprint": "[parameters('certificateThumbprint')]"
        },
    
        "Credential": {
          "Name": "MyCredential",
          "UserName": "[parameters('credentialUsername')]",
          "Password": "[parameters('credentialPassword')]"
        },
    
        "Schedule": {
          "Name": "MySchedule",
          "Description": "Sample schedule",
          "IsEnabled": "true",
          "Interval": "1",
          "Frequency": "hour",
          "StartTime": "[parameters('scheduleStartTime')]",
          "TimeZone": "[parameters('scheduleTimeZone')]",
          "LinkGuid": "[parameters('scheduleLinkGuid')]"
        },
    
        "Variable": {
          "Name": "MyVariable",
          "Description": "Sample variable",
          "Encrypted": 0,
          "Type": "string",
          "Value": "'This is my string value.'"
        },
    
        "Module": {
          "Name": "OMSIngestionAPI",
          "Uri": "https://devopsgallerystorage.blob.core.windows.net/packages/omsingestionapi.1.3.0.nupkg"
        }
      },
      "resources": [
        {
          "name": "[concat(variables('SolutionName'), '[' ,parameters('workspacename'), ']')]",
          "location": "[parameters('workspaceRegionId')]",
          "tags": { },
          "type": "Microsoft.OperationsManagement/solutions",
          "apiVersion": "[variables('LogAnalyticsApiVersion')]",
          "dependsOn": [
            "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/jobs/', parameters('accountName'), variables('Runbook').JobGuid)]",
            "[resourceId('Microsoft.Automation/automationAccounts/certificates/', parameters('accountName'), variables('Certificate').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/credentials/', parameters('accountName'), variables('Credential').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/jobSchedules/', parameters('accountName'), variables('Schedule').LinkGuid)]",
            "[resourceId('Microsoft.Automation/automationAccounts/variables/', parameters('accountName'), variables('Variable').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/modules/', parameters('accountName'), variables('Module').Name)]"
          ],
          "properties": {
            "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspacename'))]",
            "referencedResources": [
              "[resourceId('Microsoft.Automation/automationAccounts/modules/', parameters('accountName'), variables('Module').Name)]"
            ],
            "containedResources": [
              "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/jobs/', parameters('accountName'), variables('Runbook').JobGuid)]",
              "[resourceId('Microsoft.Automation/automationAccounts/certificates/', parameters('accountName'), variables('Certificate').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/credentials/', parameters('accountName'), variables('Credential').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/jobSchedules/', parameters('accountName'), variables('Schedule').LinkGuid)]",
              "[resourceId('Microsoft.Automation/automationAccounts/variables/', parameters('accountName'), variables('Variable').Name)]"
            ]
          },
          "plan": {
            "name": "[concat(variables('SolutionName'), '[' ,parameters('workspaceName'), ']')]",
            "Version": "[variables('SolutionVersion')]",
            "product": "[variables('ProductName')]",
            "publisher": "[variables('SolutionPublisher')]",
            "promotionCode": ""
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Runbook').Name)]",
          "type": "Microsoft.Automation/automationAccounts/runbooks",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "dependsOn": [
          ],
          "location": "[parameters('regionId')]",
          "tags": { },
          "properties": {
            "runbookType": "[variables('Runbook').Type]",
            "logProgress": "true",
            "logVerbose": "true",
            "description": "[variables('Runbook').Description]",
            "publishContentLink": {
              "uri": "[variables('Runbook').Uri]",
              "version": "1.0.0.0"
            }
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Runbook').JobGuid)]",
          "type": "Microsoft.Automation/automationAccounts/jobs",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "dependsOn": [
            "[concat('Microsoft.Automation/automationAccounts/', parameters('accountName'), '/runbooks/', variables('Runbook').Name)]"
          ],
          "tags": { },
          "properties": {
            "runbook": {
              "name": "[variables('Runbook').Name]"
            },
            "parameters": {
              "targetSubscriptionId": "[subscription().subscriptionId]",
              "resourcegroup": "[resourceGroup().name]",
              "automationaccount": "[parameters('accountName')]"
            }
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Certificate').Name)]",
          "type": "Microsoft.Automation/automationAccounts/certificates",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "Base64Value": "[variables('Certificate').Base64Value]",
            "Thumbprint": "[variables('Certificate').Thumbprint]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Credential').Name)]",
          "type": "Microsoft.Automation/automationAccounts/credentials",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "userName": "[variables('Credential').UserName]",
            "password": "[variables('Credential').Password]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Schedule').Name)]",
          "type": "microsoft.automation/automationAccounts/schedules",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "description": "[variables('Schedule').Description]",
            "startTime": "[variables('Schedule').StartTime]",
            "timeZone": "[variables('Schedule').TimeZone]",
            "isEnabled": "[variables('Schedule').IsEnabled]",
            "interval": "[variables('Schedule').Interval]",
            "frequency": "[variables('Schedule').Frequency]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Schedule').LinkGuid)]",
          "type": "microsoft.automation/automationAccounts/jobSchedules",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "dependsOn": [
            "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]"
          ],
          "tags": {
          },
          "properties": {
            "schedule": {
              "name": "[variables('Schedule').Name]"
            },
            "runbook": {
              "name": "[variables('Runbook').Name]"
            }
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Variable').Name)]",
          "type": "microsoft.automation/automationAccounts/variables",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "description": "[variables('Variable').Description]",
            "isEncrypted": "[variables('Variable').Encrypted]",
            "type": "[variables('Variable').Type]",
            "value": "[variables('Variable').Value]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Module').Name)]",
          "type": "Microsoft.Automation/automationAccounts/modules",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "dependsOn": [
          ],
          "properties": {
            "contentLink": {
              "uri": "[variables('Module').Uri]"
            }
          }
        }
    
      ],
      "outputs": { }
    }




## <a name="next-steps"></a><span data-ttu-id="b25e7-301">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b25e7-301">Next steps</span></span>
* <span data-ttu-id="b25e7-302">[Ajout d’une vue à votre solution](operations-management-suite-solutions-resources-views.md) pour visualiser les données collectées.</span><span class="sxs-lookup"><span data-stu-id="b25e7-302">[Add a view to your solution](operations-management-suite-solutions-resources-views.md) to visualize collected data.</span></span>
