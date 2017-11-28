---
title: "ressources d’automatisation aaaAzure dans les solutions OMS | Documents Microsoft"
description: "Solutions dans OMS inclut généralement des procédures opérationnelles dans Azure Automation tooautomate des processus tels que la collecte et de traitement des données d’analyse.  Cet article décrit comment les runbooks tooinclude et leurs ressources associées dans une solution."
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
ms.openlocfilehash: 82a156f89bf77ce25e52e5e4596261ec07a24dae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="adding-azure-automation-resources-tooan-oms-management-solution-preview"></a><span data-ttu-id="49b7f-104">Ajout de solution de gestion Azure Automation ressources tooan OMS (version préliminaire)</span><span class="sxs-lookup"><span data-stu-id="49b7f-104">Adding Azure Automation resources tooan OMS management solution (Preview)</span></span>
> [!NOTE]
> <span data-ttu-id="49b7f-105">Il s’agit d’une documentation préliminaire pour la création de solutions de gestion dans OMS qui sont actuellement en préversion.</span><span class="sxs-lookup"><span data-stu-id="49b7f-105">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="49b7f-106">N’importe quel schéma décrit ci-dessous est un objet toochange.</span><span class="sxs-lookup"><span data-stu-id="49b7f-106">Any schema described below is subject toochange.</span></span>   


<span data-ttu-id="49b7f-107">[Solutions de gestion OMS](operations-management-suite-solutions.md) inclut généralement des procédures opérationnelles dans Azure Automation tooautomate des processus tels que la collecte et de traitement des données d’analyse.</span><span class="sxs-lookup"><span data-stu-id="49b7f-107">[Management solutions in OMS](operations-management-suite-solutions.md) will typically include runbooks in Azure Automation tooautomate processes such as collecting and processing monitoring data.</span></span>  <span data-ttu-id="49b7f-108">En outre toorunbooks, comptes Automation inclut des ressources telles que des variables et des planifications qui prennent en charge les runbooks hello utilisés dans les solutions hello.</span><span class="sxs-lookup"><span data-stu-id="49b7f-108">In addition toorunbooks, Automation accounts includes assets such as variables and schedules that support hello runbooks used in hello solution.</span></span>  <span data-ttu-id="49b7f-109">Cet article décrit comment les runbooks tooinclude et leurs ressources associées dans une solution.</span><span class="sxs-lookup"><span data-stu-id="49b7f-109">This article describes how tooinclude runbooks and their related resources in a solution.</span></span>

> [!NOTE]
> <span data-ttu-id="49b7f-110">Hello exemples dans cet article utilisent les paramètres et les variables qui sont deux solutions toomanagement requises ou courantes et décrites dans [création de solutions de gestion Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span><span class="sxs-lookup"><span data-stu-id="49b7f-110">hello samples in this article use parameters and variables that are either required or common toomanagement solutions  and described in [Creating management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="49b7f-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="49b7f-111">Prerequisites</span></span>
<span data-ttu-id="49b7f-112">Cet article suppose que vous êtes déjà familiarisé avec hello informations suivantes.</span><span class="sxs-lookup"><span data-stu-id="49b7f-112">This article assumes that you're already familiar with hello following information.</span></span>

- <span data-ttu-id="49b7f-113">Comment trop[créer une solution de gestion](operations-management-suite-solutions-creating.md).</span><span class="sxs-lookup"><span data-stu-id="49b7f-113">How too[create a management solution](operations-management-suite-solutions-creating.md).</span></span>
- <span data-ttu-id="49b7f-114">Hello la structure d’un [fichier solution](operations-management-suite-solutions-solution-file.md).</span><span class="sxs-lookup"><span data-stu-id="49b7f-114">hello structure of a [solution file](operations-management-suite-solutions-solution-file.md).</span></span>
- <span data-ttu-id="49b7f-115">Comment trop[créent des modèles de gestionnaire de ressources](../azure-resource-manager/resource-group-authoring-templates.md)</span><span class="sxs-lookup"><span data-stu-id="49b7f-115">How too[author Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md)</span></span>

## <a name="automation-account"></a><span data-ttu-id="49b7f-116">Compte Automation</span><span class="sxs-lookup"><span data-stu-id="49b7f-116">Automation account</span></span>
<span data-ttu-id="49b7f-117">Toutes les ressources dans Azure Automation sont contenues dans un [compte Automation](../automation/automation-security-overview.md#automation-account-overview).</span><span class="sxs-lookup"><span data-stu-id="49b7f-117">All resources in Azure Automation are contained in an [Automation account](../automation/automation-security-overview.md#automation-account-overview).</span></span>  <span data-ttu-id="49b7f-118">Comme décrit dans [OMS espace de travail et le compte Automation](operations-management-suite-solutions.md#oms-workspace-and-automation-account) hello compte Automation n’est pas inclus dans la solution de gestion hello mais doit exister pour que la solution de hello est installée.</span><span class="sxs-lookup"><span data-stu-id="49b7f-118">As described in [OMS workspace and Automation account](operations-management-suite-solutions.md#oms-workspace-and-automation-account) hello Automation account isn't included in hello management solution but must exist before hello solution is installed.</span></span>  <span data-ttu-id="49b7f-119">Si elle n’est pas disponible, hello solution installation échouera.</span><span class="sxs-lookup"><span data-stu-id="49b7f-119">If it isn't available, then hello solution install will fail.</span></span>

<span data-ttu-id="49b7f-120">Hello nom de chaque ressource Automation hello du inclut son compte Automation.</span><span class="sxs-lookup"><span data-stu-id="49b7f-120">hello name of each Automation resource includes hello name of its Automation account.</span></span>  <span data-ttu-id="49b7f-121">Cette opération est effectuée dans la solution hello avec hello **accountName** paramètre comme hello, exemple d’une ressource de runbook suivant.</span><span class="sxs-lookup"><span data-stu-id="49b7f-121">This is done in hello solution with hello **accountName** parameter as in hello following example of a runbook resource.</span></span>

    "name": "[concat(parameters('accountName'), '/MyRunbook'))]"


## <a name="runbooks"></a><span data-ttu-id="49b7f-122">Runbooks</span><span class="sxs-lookup"><span data-stu-id="49b7f-122">Runbooks</span></span>
<span data-ttu-id="49b7f-123">Vous devez inclure tous les runbooks utilisés par la solution hello dans le fichier de solution hello afin qu’ils sont créés lors de la solution de hello est installée.</span><span class="sxs-lookup"><span data-stu-id="49b7f-123">You should include any runbooks used by hello solution in hello solution file so that they're created when hello solution is installed.</span></span>  <span data-ttu-id="49b7f-124">Vous ne peut pas contenir des corps de hello du runbook hello dans le modèle de hello, vous devez publier emplacement public hello runbook tooa où il est accessible par tout utilisateur de l’installation de votre solution.</span><span class="sxs-lookup"><span data-stu-id="49b7f-124">You cannot contain hello body of hello runbook in hello template though, so you should publish hello runbook tooa public location where it can be accessed by any user installing your solution.</span></span>

<span data-ttu-id="49b7f-125">[Azure Automation runbook](../automation/automation-runbook-types.md) ressources ont un type de **Microsoft.Automation/automationAccounts/runbooks** et avoir hello suivant la structure.</span><span class="sxs-lookup"><span data-stu-id="49b7f-125">[Azure Automation runbook](../automation/automation-runbook-types.md) resources have a type of **Microsoft.Automation/automationAccounts/runbooks** and have hello following structure.</span></span> <span data-ttu-id="49b7f-126">Cela inclut des variables et des paramètres courants afin que vous pouvez copier et coller cet extrait de code dans votre fichier de solution et modifier les noms de paramètre hello.</span><span class="sxs-lookup"><span data-stu-id="49b7f-126">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 

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


<span data-ttu-id="49b7f-127">Décrit les propriétés de Hello pour les procédures opérationnelles Bonjour tableau suivant.</span><span class="sxs-lookup"><span data-stu-id="49b7f-127">hello properties for runbooks are described in hello following table.</span></span>

| <span data-ttu-id="49b7f-128">Propriété</span><span class="sxs-lookup"><span data-stu-id="49b7f-128">Property</span></span> | <span data-ttu-id="49b7f-129">Description</span><span class="sxs-lookup"><span data-stu-id="49b7f-129">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="49b7f-130">runbookType</span><span class="sxs-lookup"><span data-stu-id="49b7f-130">runbookType</span></span> |<span data-ttu-id="49b7f-131">Spécifie les types de hello de hello runbook.</span><span class="sxs-lookup"><span data-stu-id="49b7f-131">Specifies hello types of hello runbook.</span></span> <br><br> <span data-ttu-id="49b7f-132">Script : script PowerShell</span><span class="sxs-lookup"><span data-stu-id="49b7f-132">Script - PowerShell script</span></span> <br><span data-ttu-id="49b7f-133">PowerShell : workflow PowerShell</span><span class="sxs-lookup"><span data-stu-id="49b7f-133">PowerShell - PowerShell workflow</span></span> <br> <span data-ttu-id="49b7f-134">GraphPowerShell : runbook de script PowerShell graphique</span><span class="sxs-lookup"><span data-stu-id="49b7f-134">GraphPowerShell - Graphical PowerShell script runbook</span></span> <br> <span data-ttu-id="49b7f-135">GraphPowerShellWorkflow : runbook de workflow PowerShell graphique</span><span class="sxs-lookup"><span data-stu-id="49b7f-135">GraphPowerShellWorkflow - Graphical PowerShell workflow runbook</span></span> |
| <span data-ttu-id="49b7f-136">logProgress</span><span class="sxs-lookup"><span data-stu-id="49b7f-136">logProgress</span></span> |<span data-ttu-id="49b7f-137">Spécifie si [enregistrements de progression](../automation/automation-runbook-output-and-messages.md) doit être généré pour les runbook hello.</span><span class="sxs-lookup"><span data-stu-id="49b7f-137">Specifies whether [progress records](../automation/automation-runbook-output-and-messages.md) should be generated for hello runbook.</span></span> |
| <span data-ttu-id="49b7f-138">logVerbose</span><span class="sxs-lookup"><span data-stu-id="49b7f-138">logVerbose</span></span> |<span data-ttu-id="49b7f-139">Spécifie si [les enregistrements détaillés](../automation/automation-runbook-output-and-messages.md) doit être généré pour les runbook hello.</span><span class="sxs-lookup"><span data-stu-id="49b7f-139">Specifies whether [verbose records](../automation/automation-runbook-output-and-messages.md) should be generated for hello runbook.</span></span> |
| <span data-ttu-id="49b7f-140">description</span><span class="sxs-lookup"><span data-stu-id="49b7f-140">description</span></span> |<span data-ttu-id="49b7f-141">Description facultative pour le runbook de hello.</span><span class="sxs-lookup"><span data-stu-id="49b7f-141">Optional description for hello runbook.</span></span> |
| <span data-ttu-id="49b7f-142">publishContentLink</span><span class="sxs-lookup"><span data-stu-id="49b7f-142">publishContentLink</span></span> |<span data-ttu-id="49b7f-143">Spécifie le contenu du runbook de hello hello.</span><span class="sxs-lookup"><span data-stu-id="49b7f-143">Specifies hello content of hello runbook.</span></span> <br><br><span data-ttu-id="49b7f-144">URI - Uri toohello le contenu du runbook de hello.</span><span class="sxs-lookup"><span data-stu-id="49b7f-144">uri - Uri toohello content of hello runbook.</span></span>  <span data-ttu-id="49b7f-145">Il s’agit d’un fichier .ps1 pour des runbooks PowerShell et Script et d’un fichier de runbook graphique exporté pour un runbook Graph.</span><span class="sxs-lookup"><span data-stu-id="49b7f-145">This will be a .ps1 file for PowerShell and Script runbooks, and an exported graphical runbook file for a Graph runbook.</span></span>  <br> <span data-ttu-id="49b7f-146">version - Version de runbook hello pour votre propre suivi.</span><span class="sxs-lookup"><span data-stu-id="49b7f-146">version - Version of hello runbook for your own tracking.</span></span> |


## <a name="automation-jobs"></a><span data-ttu-id="49b7f-147">Tâches Automation</span><span class="sxs-lookup"><span data-stu-id="49b7f-147">Automation jobs</span></span>
<span data-ttu-id="49b7f-148">Lorsque vous démarrez un Runbook dans Azure Automation, il crée un travail d’automatisation.</span><span class="sxs-lookup"><span data-stu-id="49b7f-148">When you start a runbook in Azure Automation, it creates an automation job.</span></span>  <span data-ttu-id="49b7f-149">Vous pouvez ajouter une automatisation travail ressource tooyour solution tooautomatically début d’un runbook lors de la solution de gestion hello est installée.</span><span class="sxs-lookup"><span data-stu-id="49b7f-149">You can add an automation job resource tooyour solution tooautomatically start a runbook when hello management solution is installed.</span></span>  <span data-ttu-id="49b7f-150">Cette méthode est généralement utilisées toostart runbooks qui sont utilisés pour la configuration initiale de la solution de hello.</span><span class="sxs-lookup"><span data-stu-id="49b7f-150">This method is typically used toostart runbooks that are used for initial configuration of hello solution.</span></span>  <span data-ttu-id="49b7f-151">toostart un runbook à intervalles réguliers, créez un [planification](#schedules) et un [planification du travail](#job-schedules)</span><span class="sxs-lookup"><span data-stu-id="49b7f-151">toostart a runbook at regular intervals, create a [schedule](#schedules) and a [job schedule](#job-schedules)</span></span>

<span data-ttu-id="49b7f-152">Ressources de travail ont un type de **Microsoft.Automation/automationAccounts/jobs** et avoir hello suivant la structure.</span><span class="sxs-lookup"><span data-stu-id="49b7f-152">Job resources have a type of **Microsoft.Automation/automationAccounts/jobs** and have hello following structure.</span></span>  <span data-ttu-id="49b7f-153">Cela inclut des variables et des paramètres courants afin que vous pouvez copier et coller cet extrait de code dans votre fichier de solution et modifier les noms de paramètre hello.</span><span class="sxs-lookup"><span data-stu-id="49b7f-153">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 

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

<span data-ttu-id="49b7f-154">Décrit les propriétés de Hello pour les tâches d’automatisation Bonjour tableau suivant.</span><span class="sxs-lookup"><span data-stu-id="49b7f-154">hello properties for automation jobs are described in hello following table.</span></span>

| <span data-ttu-id="49b7f-155">Propriété</span><span class="sxs-lookup"><span data-stu-id="49b7f-155">Property</span></span> | <span data-ttu-id="49b7f-156">Description</span><span class="sxs-lookup"><span data-stu-id="49b7f-156">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="49b7f-157">runbook</span><span class="sxs-lookup"><span data-stu-id="49b7f-157">runbook</span></span> |<span data-ttu-id="49b7f-158">Entité de nom unique portant le nom de hello de hello runbook toostart.</span><span class="sxs-lookup"><span data-stu-id="49b7f-158">Single name entity with hello name of hello runbook toostart.</span></span> |
| <span data-ttu-id="49b7f-159">parameters</span><span class="sxs-lookup"><span data-stu-id="49b7f-159">parameters</span></span> |<span data-ttu-id="49b7f-160">Entité pour chaque valeur de paramètre requis par les runbook hello.</span><span class="sxs-lookup"><span data-stu-id="49b7f-160">Entity for each parameter value required by hello runbook.</span></span> |

<span data-ttu-id="49b7f-161">le travail de Hello inclut le nom du runbook hello et n’importe quel toobe de valeurs de paramètre envoyés toohello runbook.</span><span class="sxs-lookup"><span data-stu-id="49b7f-161">hello job includes hello runbook name and any parameter values toobe sent toohello runbook.</span></span>  <span data-ttu-id="49b7f-162">travail de Hello doit [dépendent](operations-management-suite-solutions-solution-file.md#resources) runbook de hello il démarre depuis hello runbook doit être créé avant la tâche de hello.</span><span class="sxs-lookup"><span data-stu-id="49b7f-162">hello job should [depend on](operations-management-suite-solutions-solution-file.md#resources) hello runbook that it's starting since hello runbook must be created before hello job.</span></span>  <span data-ttu-id="49b7f-163">Si vous avez plusieurs runbooks qui doivent être lancés, vous pouvez définir leur ordre en rendant un travail dépendant des autres travaux qui doivent être exécutés en premier.</span><span class="sxs-lookup"><span data-stu-id="49b7f-163">If you have multiple runbooks that should be started you can define their order by having a job depend on any other jobs that should be run first.</span></span>

<span data-ttu-id="49b7f-164">nom de Hello d’une ressource de travail doit contenir un GUID qui est généralement affecté par un paramètre.</span><span class="sxs-lookup"><span data-stu-id="49b7f-164">hello name of a job resource must contain a GUID which is typically assigned by a parameter.</span></span>  <span data-ttu-id="49b7f-165">Vous trouverez plus d’informations sur les paramètres GUID dans la rubrique [Création de solutions dans Operations Management Suite (OMS)](operations-management-suite-solutions-solution-file.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="49b7f-165">You can read more about GUID parameters in [Creating solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-solution-file.md#parameters).</span></span>  


## <a name="certificates"></a><span data-ttu-id="49b7f-166">Certificats</span><span class="sxs-lookup"><span data-stu-id="49b7f-166">Certificates</span></span>
<span data-ttu-id="49b7f-167">[Certificats Automation Azure](../automation/automation-certificates.md) ont un type de **Microsoft.Automation/automationAccounts/certificates** et avoir hello suivant la structure.</span><span class="sxs-lookup"><span data-stu-id="49b7f-167">[Azure Automation certificates](../automation/automation-certificates.md) have a type of **Microsoft.Automation/automationAccounts/certificates** and have hello following structure.</span></span> <span data-ttu-id="49b7f-168">Cela inclut des variables et des paramètres courants afin que vous pouvez copier et coller cet extrait de code dans votre fichier de solution et modifier les noms de paramètre hello.</span><span class="sxs-lookup"><span data-stu-id="49b7f-168">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 

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



<span data-ttu-id="49b7f-169">Décrit les propriétés de Hello pour les ressources de certificats Bonjour tableau suivant.</span><span class="sxs-lookup"><span data-stu-id="49b7f-169">hello properties for Certificates resources are described in hello following table.</span></span>

| <span data-ttu-id="49b7f-170">Propriété</span><span class="sxs-lookup"><span data-stu-id="49b7f-170">Property</span></span> | <span data-ttu-id="49b7f-171">Description</span><span class="sxs-lookup"><span data-stu-id="49b7f-171">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="49b7f-172">base64Value</span><span class="sxs-lookup"><span data-stu-id="49b7f-172">base64Value</span></span> |<span data-ttu-id="49b7f-173">Valeur de la base 64 pour le certificat de hello.</span><span class="sxs-lookup"><span data-stu-id="49b7f-173">Base 64 value for hello certificate.</span></span> |
| <span data-ttu-id="49b7f-174">thumbprint</span><span class="sxs-lookup"><span data-stu-id="49b7f-174">thumbprint</span></span> |<span data-ttu-id="49b7f-175">Empreinte numérique du certificat de hello.</span><span class="sxs-lookup"><span data-stu-id="49b7f-175">Thumbprint for hello certificate.</span></span> |



## <a name="credentials"></a><span data-ttu-id="49b7f-176">Informations d'identification</span><span class="sxs-lookup"><span data-stu-id="49b7f-176">Credentials</span></span>
<span data-ttu-id="49b7f-177">[Les informations d’identification Automation Azure](../automation/automation-credentials.md) ont un type de **Microsoft.Automation/automationAccounts/credentials** et avoir hello suivant la structure.</span><span class="sxs-lookup"><span data-stu-id="49b7f-177">[Azure Automation credentials](../automation/automation-credentials.md) have a type of **Microsoft.Automation/automationAccounts/credentials** and have hello following structure.</span></span>  <span data-ttu-id="49b7f-178">Cela inclut des variables et des paramètres courants afin que vous pouvez copier et coller cet extrait de code dans votre fichier de solution et modifier les noms de paramètre hello.</span><span class="sxs-lookup"><span data-stu-id="49b7f-178">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 


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

<span data-ttu-id="49b7f-179">Décrit les propriétés de Hello pour les ressources d’informations d’identification Bonjour tableau suivant.</span><span class="sxs-lookup"><span data-stu-id="49b7f-179">hello properties for Credential resources are described in hello following table.</span></span>

| <span data-ttu-id="49b7f-180">Propriété</span><span class="sxs-lookup"><span data-stu-id="49b7f-180">Property</span></span> | <span data-ttu-id="49b7f-181">Description</span><span class="sxs-lookup"><span data-stu-id="49b7f-181">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="49b7f-182">userName</span><span class="sxs-lookup"><span data-stu-id="49b7f-182">userName</span></span> |<span data-ttu-id="49b7f-183">Nom d’utilisateur pour les informations d’identification hello.</span><span class="sxs-lookup"><span data-stu-id="49b7f-183">User name for hello credential.</span></span> |
| <span data-ttu-id="49b7f-184">password</span><span class="sxs-lookup"><span data-stu-id="49b7f-184">password</span></span> |<span data-ttu-id="49b7f-185">Mot de passe pour les informations d’identification hello.</span><span class="sxs-lookup"><span data-stu-id="49b7f-185">Password for hello credential.</span></span> |


## <a name="schedules"></a><span data-ttu-id="49b7f-186">Planifications</span><span class="sxs-lookup"><span data-stu-id="49b7f-186">Schedules</span></span>
<span data-ttu-id="49b7f-187">[Planifications d’automatisation Azure](../automation/automation-schedules.md) ont un type de **Microsoft.Automation/automationAccounts/schedules** et avoir hello hello suivant la structure.</span><span class="sxs-lookup"><span data-stu-id="49b7f-187">[Azure Automation schedules](../automation/automation-schedules.md) have a type of **Microsoft.Automation/automationAccounts/schedules** and have hello hello following structure.</span></span> <span data-ttu-id="49b7f-188">Cela inclut des variables et des paramètres courants afin que vous pouvez copier et coller cet extrait de code dans votre fichier de solution et modifier les noms de paramètre hello.</span><span class="sxs-lookup"><span data-stu-id="49b7f-188">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 

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

<span data-ttu-id="49b7f-189">Décrit les propriétés de Hello pour planifier des ressources Bonjour tableau suivant.</span><span class="sxs-lookup"><span data-stu-id="49b7f-189">hello properties for schedule resources are described in hello following table.</span></span>

| <span data-ttu-id="49b7f-190">Propriété</span><span class="sxs-lookup"><span data-stu-id="49b7f-190">Property</span></span> | <span data-ttu-id="49b7f-191">Description</span><span class="sxs-lookup"><span data-stu-id="49b7f-191">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="49b7f-192">description</span><span class="sxs-lookup"><span data-stu-id="49b7f-192">description</span></span> |<span data-ttu-id="49b7f-193">Description facultative pour la planification de hello.</span><span class="sxs-lookup"><span data-stu-id="49b7f-193">Optional description for hello schedule.</span></span> |
| <span data-ttu-id="49b7f-194">startTime</span><span class="sxs-lookup"><span data-stu-id="49b7f-194">startTime</span></span> |<span data-ttu-id="49b7f-195">Spécifie l’heure de début de hello d’une planification en tant qu’objet DateTime.</span><span class="sxs-lookup"><span data-stu-id="49b7f-195">Specifies hello start time of a schedule as a DateTime object.</span></span> <span data-ttu-id="49b7f-196">Une chaîne peut être fournie si elle peut être convertie tooa DateTime valide.</span><span class="sxs-lookup"><span data-stu-id="49b7f-196">A string can be provided if it can be converted tooa valid DateTime.</span></span> |
| <span data-ttu-id="49b7f-197">isEnabled</span><span class="sxs-lookup"><span data-stu-id="49b7f-197">isEnabled</span></span> |<span data-ttu-id="49b7f-198">Spécifie si la planification de hello est activée.</span><span class="sxs-lookup"><span data-stu-id="49b7f-198">Specifies whether hello schedule is enabled.</span></span> |
| <span data-ttu-id="49b7f-199">interval</span><span class="sxs-lookup"><span data-stu-id="49b7f-199">interval</span></span> |<span data-ttu-id="49b7f-200">type de Hello d’intervalle de planification de hello.</span><span class="sxs-lookup"><span data-stu-id="49b7f-200">hello type of interval for hello schedule.</span></span><br><br><span data-ttu-id="49b7f-201">day</span><span class="sxs-lookup"><span data-stu-id="49b7f-201">day</span></span><br><span data-ttu-id="49b7f-202">hour</span><span class="sxs-lookup"><span data-stu-id="49b7f-202">hour</span></span> |
| <span data-ttu-id="49b7f-203">frequency</span><span class="sxs-lookup"><span data-stu-id="49b7f-203">frequency</span></span> |<span data-ttu-id="49b7f-204">Fréquence à laquelle hello planification doit se déclencher dans le nombre de jours ou d’heures.</span><span class="sxs-lookup"><span data-stu-id="49b7f-204">Frequency that hello schedule should fire in number of days or hours.</span></span> |

<span data-ttu-id="49b7f-205">Les planifications doivent avoir une heure de début avec une valeur supérieure à hello heure actuelle.</span><span class="sxs-lookup"><span data-stu-id="49b7f-205">Schedules must have a start time with a value greater than hello current time.</span></span>  <span data-ttu-id="49b7f-206">Vous ne peut pas fournir cette valeur avec une variable dans la mesure où vous n’auriez aucun moyen de savoir quand il est toobe continu installé.</span><span class="sxs-lookup"><span data-stu-id="49b7f-206">You cannot provide this value with a variable since you would have no way of knowing when it's going toobe installed.</span></span>

<span data-ttu-id="49b7f-207">Utilisez une des hello suivant deux stratégies lors de l’utilisation des ressources de planification dans une solution.</span><span class="sxs-lookup"><span data-stu-id="49b7f-207">Use one of hello following two strategies when using schedule resources in a solution.</span></span>

- <span data-ttu-id="49b7f-208">Utiliser un paramètre pour l’heure de début hello de planification de hello.</span><span class="sxs-lookup"><span data-stu-id="49b7f-208">Use a parameter for hello start time of hello schedule.</span></span>  <span data-ttu-id="49b7f-209">Il vous est demandé hello utilisateur tooprovide une valeur lorsqu’ils installent la solution de hello.</span><span class="sxs-lookup"><span data-stu-id="49b7f-209">This will prompt hello user tooprovide a value when they install hello solution.</span></span>  <span data-ttu-id="49b7f-210">Si vous avez plusieurs planifications, vous pouvez utiliser une valeur de paramètre unique pour plusieurs d'entre eux.</span><span class="sxs-lookup"><span data-stu-id="49b7f-210">If you have multiple schedules, you could use a single parameter value for more than one of them.</span></span>
- <span data-ttu-id="49b7f-211">Créer des planifications de hello à l’aide d’un runbook qui démarre lorsqu’hello solution est installée.</span><span class="sxs-lookup"><span data-stu-id="49b7f-211">Create hello schedules using a runbook that starts when hello solution is installed.</span></span>  <span data-ttu-id="49b7f-212">Cela supprime la spécification hello hello utilisateur toospecify est une heure, mais vous ne peut pas contenir planification hello dans votre solution afin qu’il sera supprimé lors de la solution de hello est supprimée.</span><span class="sxs-lookup"><span data-stu-id="49b7f-212">This removes hello requirement of hello user toospecify a time, but you can't contain hello schedule in your solution so it will be removed when hello solution is removed.</span></span>


### <a name="job-schedules"></a><span data-ttu-id="49b7f-213">Planifications de travaux</span><span class="sxs-lookup"><span data-stu-id="49b7f-213">Job schedules</span></span>
<span data-ttu-id="49b7f-214">Les ressources de planification de tâche lient un runbook à une planification.</span><span class="sxs-lookup"><span data-stu-id="49b7f-214">Job schedule resources link a runbook with a schedule.</span></span>  <span data-ttu-id="49b7f-215">Ils ont un type de **Microsoft.Automation/automationAccounts/jobSchedules** et avoir hello hello suivant la structure.</span><span class="sxs-lookup"><span data-stu-id="49b7f-215">They have a type of **Microsoft.Automation/automationAccounts/jobSchedules** and have hello hello following structure.</span></span>  <span data-ttu-id="49b7f-216">Cela inclut des variables et des paramètres courants afin que vous pouvez copier et coller cet extrait de code dans votre fichier de solution et modifier les noms de paramètre hello.</span><span class="sxs-lookup"><span data-stu-id="49b7f-216">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 

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


<span data-ttu-id="49b7f-217">Décrit les propriétés de Hello pour les planifications de travaux Bonjour tableau suivant.</span><span class="sxs-lookup"><span data-stu-id="49b7f-217">hello properties for job schedules are described in hello following table.</span></span>

| <span data-ttu-id="49b7f-218">Propriété</span><span class="sxs-lookup"><span data-stu-id="49b7f-218">Property</span></span> | <span data-ttu-id="49b7f-219">Description</span><span class="sxs-lookup"><span data-stu-id="49b7f-219">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="49b7f-220">nom de la planification</span><span class="sxs-lookup"><span data-stu-id="49b7f-220">schedule name</span></span> |<span data-ttu-id="49b7f-221">Seul **nom** entité portant le nom hello de planification de hello.</span><span class="sxs-lookup"><span data-stu-id="49b7f-221">Single **name** entity with hello name of hello schedule.</span></span> |
| <span data-ttu-id="49b7f-222">nom du runbook</span><span class="sxs-lookup"><span data-stu-id="49b7f-222">runbook name</span></span>  |<span data-ttu-id="49b7f-223">Seul **nom** entité portant le nom hello de hello runbook.</span><span class="sxs-lookup"><span data-stu-id="49b7f-223">Single **name** entity with hello name of hello runbook.</span></span>  |



## <a name="variables"></a><span data-ttu-id="49b7f-224">variables</span><span class="sxs-lookup"><span data-stu-id="49b7f-224">Variables</span></span>
<span data-ttu-id="49b7f-225">[Les variables Automation Azure](../automation/automation-variables.md) ont un type de **Microsoft.Automation/automationAccounts/variables** et avoir hello suivant la structure.</span><span class="sxs-lookup"><span data-stu-id="49b7f-225">[Azure Automation variables](../automation/automation-variables.md) have a type of **Microsoft.Automation/automationAccounts/variables** and have hello following structure.</span></span>  <span data-ttu-id="49b7f-226">Cela inclut des variables et des paramètres courants afin que vous pouvez copier et coller cet extrait de code dans votre fichier de solution et modifier les noms de paramètre hello.</span><span class="sxs-lookup"><span data-stu-id="49b7f-226">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span>

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

<span data-ttu-id="49b7f-227">Décrit les propriétés de Hello pour les ressources variables Bonjour tableau suivant.</span><span class="sxs-lookup"><span data-stu-id="49b7f-227">hello properties for variable resources are described in hello following table.</span></span>

| <span data-ttu-id="49b7f-228">Propriété</span><span class="sxs-lookup"><span data-stu-id="49b7f-228">Property</span></span> | <span data-ttu-id="49b7f-229">Description</span><span class="sxs-lookup"><span data-stu-id="49b7f-229">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="49b7f-230">description</span><span class="sxs-lookup"><span data-stu-id="49b7f-230">description</span></span> | <span data-ttu-id="49b7f-231">Description facultative de la variable de hello.</span><span class="sxs-lookup"><span data-stu-id="49b7f-231">Optional description for hello variable.</span></span> |
| <span data-ttu-id="49b7f-232">isEncrypted</span><span class="sxs-lookup"><span data-stu-id="49b7f-232">isEncrypted</span></span> | <span data-ttu-id="49b7f-233">Spécifie si la variable de hello doit être chiffrée.</span><span class="sxs-lookup"><span data-stu-id="49b7f-233">Specifies whether hello variable should be encrypted.</span></span> |
| <span data-ttu-id="49b7f-234">type</span><span class="sxs-lookup"><span data-stu-id="49b7f-234">type</span></span> | <span data-ttu-id="49b7f-235">Cette propriété n’a actuellement aucun effet.</span><span class="sxs-lookup"><span data-stu-id="49b7f-235">This property currently has no effect.</span></span>  <span data-ttu-id="49b7f-236">type de données Hello de variable de hello sera déterminé par la valeur initiale de hello.</span><span class="sxs-lookup"><span data-stu-id="49b7f-236">hello data type of hello variable will be determined by hello initial value.</span></span> |
| <span data-ttu-id="49b7f-237">value</span><span class="sxs-lookup"><span data-stu-id="49b7f-237">value</span></span> | <span data-ttu-id="49b7f-238">Valeur de variable de hello.</span><span class="sxs-lookup"><span data-stu-id="49b7f-238">Value for hello variable.</span></span> |

> [!NOTE]
> <span data-ttu-id="49b7f-239">Hello **type** propriété actuellement n’a aucun effet sur la variable hello en cours de création.</span><span class="sxs-lookup"><span data-stu-id="49b7f-239">hello **type** property currently has no effect on hello variable being created.</span></span>  <span data-ttu-id="49b7f-240">type de données Hello pour la variable de hello sera déterminée par la valeur de hello.</span><span class="sxs-lookup"><span data-stu-id="49b7f-240">hello data type for hello variable will be determined by hello value.</span></span>  

<span data-ttu-id="49b7f-241">Si vous définissez la valeur initiale de hello pour la variable de hello, il doit être configuré en tant que type de données correct hello.</span><span class="sxs-lookup"><span data-stu-id="49b7f-241">If you set hello initial value for hello variable, it must be configured as hello correct data type.</span></span>  <span data-ttu-id="49b7f-242">Hello tableau suivant fournit hello différents types de données autorisées et leur syntaxe.</span><span class="sxs-lookup"><span data-stu-id="49b7f-242">hello following table provides hello different data types allowable and their syntax.</span></span>  <span data-ttu-id="49b7f-243">Notez que les valeurs au format JSON sont attendus tooalways être encadrée de guillemets avec des caractères spéciaux entre guillemets de hello.</span><span class="sxs-lookup"><span data-stu-id="49b7f-243">Note that values in JSON are expected tooalways be enclosed in quotes with any special characters within hello quotes.</span></span>  <span data-ttu-id="49b7f-244">Par exemple, une valeur de chaîne serait être spécifiée par des guillemets autour de chaîne hello (à l’aide du caractère d’échappement de hello (\\)) pendant une valeur numérique est être spécifiée avec un seul jeu de guillemets doubles.</span><span class="sxs-lookup"><span data-stu-id="49b7f-244">For example, a string value would be specified by quotes around hello string (using hello escape character (\\)) while a numeric value would be specified with one set of quotes.</span></span>

| <span data-ttu-id="49b7f-245">Type de données</span><span class="sxs-lookup"><span data-stu-id="49b7f-245">Data type</span></span> | <span data-ttu-id="49b7f-246">Description</span><span class="sxs-lookup"><span data-stu-id="49b7f-246">Description</span></span> | <span data-ttu-id="49b7f-247">Exemple</span><span class="sxs-lookup"><span data-stu-id="49b7f-247">Example</span></span> | <span data-ttu-id="49b7f-248">Résout trop</span><span class="sxs-lookup"><span data-stu-id="49b7f-248">Resolves too</span></span>|
|:--|:--|:--|:--|
| <span data-ttu-id="49b7f-249">string</span><span class="sxs-lookup"><span data-stu-id="49b7f-249">string</span></span>   | <span data-ttu-id="49b7f-250">Placer la valeur entre des guillemets doubles.</span><span class="sxs-lookup"><span data-stu-id="49b7f-250">Enclose value in double quotes.</span></span>  | <span data-ttu-id="49b7f-251">"\"Hello world\""</span><span class="sxs-lookup"><span data-stu-id="49b7f-251">"\"Hello world\""</span></span> | <span data-ttu-id="49b7f-252">"Hello world"</span><span class="sxs-lookup"><span data-stu-id="49b7f-252">"Hello world"</span></span> |
| <span data-ttu-id="49b7f-253">numérique</span><span class="sxs-lookup"><span data-stu-id="49b7f-253">numeric</span></span>  | <span data-ttu-id="49b7f-254">Valeur numérique avec des guillemets simples.</span><span class="sxs-lookup"><span data-stu-id="49b7f-254">Numeric value with single quotes.</span></span>| <span data-ttu-id="49b7f-255">"64"</span><span class="sxs-lookup"><span data-stu-id="49b7f-255">"64"</span></span> | <span data-ttu-id="49b7f-256">64</span><span class="sxs-lookup"><span data-stu-id="49b7f-256">64</span></span> |
| <span data-ttu-id="49b7f-257">booléenne</span><span class="sxs-lookup"><span data-stu-id="49b7f-257">boolean</span></span>  | <span data-ttu-id="49b7f-258">**true** ou **false** entre guillemets.</span><span class="sxs-lookup"><span data-stu-id="49b7f-258">**true** or **false** in quotes.</span></span>  <span data-ttu-id="49b7f-259">Notez que cette valeur doit être en minuscules.</span><span class="sxs-lookup"><span data-stu-id="49b7f-259">Note that this value must be lowercase.</span></span> | <span data-ttu-id="49b7f-260">"true"</span><span class="sxs-lookup"><span data-stu-id="49b7f-260">"true"</span></span> | <span data-ttu-id="49b7f-261">true</span><span class="sxs-lookup"><span data-stu-id="49b7f-261">true</span></span> |
| <span data-ttu-id="49b7f-262">Datetime</span><span class="sxs-lookup"><span data-stu-id="49b7f-262">datetime</span></span> | <span data-ttu-id="49b7f-263">Valeur de date sérialisée.</span><span class="sxs-lookup"><span data-stu-id="49b7f-263">Serialized date value.</span></span><br><span data-ttu-id="49b7f-264">Vous pouvez utiliser hello applet de commande ConvertTo-Json dans PowerShell toogenerate cette valeur pour une date particulière.</span><span class="sxs-lookup"><span data-stu-id="49b7f-264">You can use hello ConvertTo-Json cmdlet in PowerShell toogenerate this value for a particular date.</span></span><br><span data-ttu-id="49b7f-265">Exemple : get-date "5/24/2017 13:14:57" \\</span><span class="sxs-lookup"><span data-stu-id="49b7f-265">Example: get-date "5/24/2017 13:14:57" \\</span></span>| <span data-ttu-id="49b7f-266">ConvertTo-Json</span><span class="sxs-lookup"><span data-stu-id="49b7f-266">ConvertTo-Json</span></span> | <span data-ttu-id="49b7f-267">"\\/Date(1495656897378)\\/"</span><span class="sxs-lookup"><span data-stu-id="49b7f-267">"\\/Date(1495656897378)\\/"</span></span> | <span data-ttu-id="49b7f-268">2017-05-24 13:14:57</span><span class="sxs-lookup"><span data-stu-id="49b7f-268">2017-05-24 13:14:57</span></span> |

## <a name="modules"></a><span data-ttu-id="49b7f-269">Modules</span><span class="sxs-lookup"><span data-stu-id="49b7f-269">Modules</span></span>
<span data-ttu-id="49b7f-270">Votre solution de gestion n’a pas besoin toodefine [modules globales](../automation/automation-integration-modules.md) utilisé par les procédures opérationnelles, car ils seront toujours disponibles dans votre compte Automation.</span><span class="sxs-lookup"><span data-stu-id="49b7f-270">Your management solution does not need toodefine [global modules](../automation/automation-integration-modules.md) used by your runbooks because they will always be available in your Automation account.</span></span>  <span data-ttu-id="49b7f-271">Vous avez besoin de tooinclude une ressource pour d’autres modules utilisés par les procédures opérationnelles.</span><span class="sxs-lookup"><span data-stu-id="49b7f-271">You do need tooinclude a resource for any other module used by your runbooks.</span></span>

<span data-ttu-id="49b7f-272">[Modules d’intégration](../automation/automation-integration-modules.md) ont un type de **Microsoft.Automation/automationAccounts/modules** et avoir hello suivant la structure.</span><span class="sxs-lookup"><span data-stu-id="49b7f-272">[Integration modules](../automation/automation-integration-modules.md) have a type of **Microsoft.Automation/automationAccounts/modules** and have hello following structure.</span></span>  <span data-ttu-id="49b7f-273">Cela inclut des variables et des paramètres courants afin que vous pouvez copier et coller cet extrait de code dans votre fichier de solution et modifier les noms de paramètre hello.</span><span class="sxs-lookup"><span data-stu-id="49b7f-273">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span>

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


<span data-ttu-id="49b7f-274">Décrit les propriétés de Hello pour les ressources de module Bonjour tableau suivant.</span><span class="sxs-lookup"><span data-stu-id="49b7f-274">hello properties for module resources are described in hello following table.</span></span>

| <span data-ttu-id="49b7f-275">Propriété</span><span class="sxs-lookup"><span data-stu-id="49b7f-275">Property</span></span> | <span data-ttu-id="49b7f-276">Description</span><span class="sxs-lookup"><span data-stu-id="49b7f-276">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="49b7f-277">contentLink</span><span class="sxs-lookup"><span data-stu-id="49b7f-277">contentLink</span></span> |<span data-ttu-id="49b7f-278">Spécifie le contenu du module de hello hello.</span><span class="sxs-lookup"><span data-stu-id="49b7f-278">Specifies hello content of hello module.</span></span> <br><br><span data-ttu-id="49b7f-279">URI - Uri toohello le contenu du module de hello.</span><span class="sxs-lookup"><span data-stu-id="49b7f-279">uri - Uri toohello content of hello module.</span></span>  <span data-ttu-id="49b7f-280">Il s’agit d’un fichier .ps1 pour des runbooks PowerShell et Script et d’un fichier de runbook graphique exporté pour un runbook Graph.</span><span class="sxs-lookup"><span data-stu-id="49b7f-280">This will be a .ps1 file for PowerShell and Script runbooks, and an exported graphical runbook file for a Graph runbook.</span></span>  <br> <span data-ttu-id="49b7f-281">version - Version du module de hello pour votre propre suivi.</span><span class="sxs-lookup"><span data-stu-id="49b7f-281">version - Version of hello module for your own tracking.</span></span> |

<span data-ttu-id="49b7f-282">Hello runbook doit s’appuyer sur hello module ressource tooensure qu’il a créées avant hello runbook.</span><span class="sxs-lookup"><span data-stu-id="49b7f-282">hello runbook should depend on hello module resource tooensure that it's created before hello runbook.</span></span>

### <a name="updating-modules"></a><span data-ttu-id="49b7f-283">Mise à jour des modules</span><span class="sxs-lookup"><span data-stu-id="49b7f-283">Updating modules</span></span>
<span data-ttu-id="49b7f-284">Si vous mettez à jour une solution de gestion qui inclut un runbook qui utilise une planification et hello nouvelle version de votre solution a un nouveau module utilisé par ce runbook, hello runbook peut utiliser hello ancienne version du module de hello.</span><span class="sxs-lookup"><span data-stu-id="49b7f-284">If you update a management solution that includes a runbook that uses a schedule, and hello new version of your solution has a new module used by that runbook, then hello runbook may use hello old version of hello module.</span></span>  <span data-ttu-id="49b7f-285">Vous devez inclure hello suivant les procédures opérationnelles dans votre solution et créer un travail toorun leur avant les autres runbooks.</span><span class="sxs-lookup"><span data-stu-id="49b7f-285">You should include hello following runbooks in your solution and create a job toorun them before any other runbooks.</span></span>  <span data-ttu-id="49b7f-286">Cela garantit que tous les modules sont mis à jour en tant que hello requis avant de charger des runbooks.</span><span class="sxs-lookup"><span data-stu-id="49b7f-286">This will ensure that any modules are updated as required before hello runbooks are loaded.</span></span>

* <span data-ttu-id="49b7f-287">[Mise à jour-ModulesinAutomationToLatestVersion](https://www.powershellgallery.com/packages/Update-ModulesInAutomationToLatestVersion/1.03/DisplayScript) garantit que tous les modules hello utilisées par les runbooks dans votre solution sont version la plus récente hello.</span><span class="sxs-lookup"><span data-stu-id="49b7f-287">[Update-ModulesinAutomationToLatestVersion](https://www.powershellgallery.com/packages/Update-ModulesInAutomationToLatestVersion/1.03/DisplayScript) will ensure that all of hello modules used by runbooks in your solution are hello latest version.</span></span>  
* <span data-ttu-id="49b7f-288">[ReRegisterAutomationSchedule-MS-Mgmt](https://www.powershellgallery.com/packages/ReRegisterAutomationSchedule-MS-Mgmt/1.0/DisplayScript) sera réinscrire tous hello Planification ressources tooensure que hello runbooks liés toothem avec des modules de dernière utilisation hello.</span><span class="sxs-lookup"><span data-stu-id="49b7f-288">[ReRegisterAutomationSchedule-MS-Mgmt](https://www.powershellgallery.com/packages/ReRegisterAutomationSchedule-MS-Mgmt/1.0/DisplayScript) will reregister all of hello schedule resources tooensure that hello runbooks linked toothem with use hello latest modules.</span></span>




## <a name="sample"></a><span data-ttu-id="49b7f-289">Exemple</span><span class="sxs-lookup"><span data-stu-id="49b7f-289">Sample</span></span>
<span data-ttu-id="49b7f-290">Voici un exemple d’une solution qui incluent ce qui inclut hello suivant des ressources :</span><span class="sxs-lookup"><span data-stu-id="49b7f-290">Following is a sample of a solution that include that includes hello following resources:</span></span>

- <span data-ttu-id="49b7f-291">Runbook.</span><span class="sxs-lookup"><span data-stu-id="49b7f-291">Runbook.</span></span>  <span data-ttu-id="49b7f-292">Il s’agit d’un exemple de runbook stocké dans un référentiel GitHub public.</span><span class="sxs-lookup"><span data-stu-id="49b7f-292">This is a sample runbook stored in a public GitHub repository.</span></span>
- <span data-ttu-id="49b7f-293">Travail d’Automation qui démarre hello runbook lors de la solution de hello est installée.</span><span class="sxs-lookup"><span data-stu-id="49b7f-293">Automation job that starts hello runbook when hello solution is installed.</span></span>
- <span data-ttu-id="49b7f-294">Planification et travail de planification toostart hello runbook à intervalles réguliers.</span><span class="sxs-lookup"><span data-stu-id="49b7f-294">Schedule and job schedule toostart hello runbook at regular intervals.</span></span>
- <span data-ttu-id="49b7f-295">Certificat.</span><span class="sxs-lookup"><span data-stu-id="49b7f-295">Certificate.</span></span>
- <span data-ttu-id="49b7f-296">Informations d'identification.</span><span class="sxs-lookup"><span data-stu-id="49b7f-296">Credential.</span></span>
- <span data-ttu-id="49b7f-297">Variable.</span><span class="sxs-lookup"><span data-stu-id="49b7f-297">Variable.</span></span>
- <span data-ttu-id="49b7f-298">Module.</span><span class="sxs-lookup"><span data-stu-id="49b7f-298">Module.</span></span>  <span data-ttu-id="49b7f-299">Il s’agit de hello [OMSIngestionAPI module](https://www.powershellgallery.com/packages/OMSIngestionAPI/1.5) pour l’écriture de données tooLog Analytique.</span><span class="sxs-lookup"><span data-stu-id="49b7f-299">This is hello [OMSIngestionAPI module](https://www.powershellgallery.com/packages/OMSIngestionAPI/1.5) for writing data tooLog Analytics.</span></span> 

<span data-ttu-id="49b7f-300">exemples d’utilisation de Hello [paramètres de solution standard](operations-management-suite-solutions-solution-file.md#parameters) variables sont communément utilisées dans une solution en opposition toohardcoding des valeurs dans les définitions de ressource hello.</span><span class="sxs-lookup"><span data-stu-id="49b7f-300">hello sample uses [standard solution parameters](operations-management-suite-solutions-solution-file.md#parameters) variables that would commonly be used in a solution as opposed toohardcoding values in hello resource definitions.</span></span>


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
            "description": "GUID for hello schedule link toorunbook.",
            "control": "guid"
          }
        },
        "runbookJobGuid": {
          "type": "string",
          "metadata": {
            "description": "GUID for hello runbook job.",
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




## <a name="next-steps"></a><span data-ttu-id="49b7f-301">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="49b7f-301">Next steps</span></span>
* <span data-ttu-id="49b7f-302">[Ajouter une solution de tooyour vue](operations-management-suite-solutions-resources-views.md) toovisualize les données collectées.</span><span class="sxs-lookup"><span data-stu-id="49b7f-302">[Add a view tooyour solution](operations-management-suite-solutions-resources-views.md) toovisualize collected data.</span></span>
