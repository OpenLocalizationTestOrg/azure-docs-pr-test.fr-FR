---
title: "Paramètres du Runbook | Microsoft Docs"
description: "Décrit les paramètres de configuration d'un Runbook dans Azure Automation et explique comment les modifier à l'aide du portail de gestion Azure et de Windows PowerShell."
services: automation
documentationcenter: 
author: mgoedtel
manager: stevenka
editor: tysonn
ms.assetid: a726f20c-a952-48b8-88ee-36d76aa3ac61
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/11/2016
ms.author: bwren
ms.openlocfilehash: 20ecbc270e61d234e026e6ba2634c7aad63b3355
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="runbook-settings"></a><span data-ttu-id="7ee87-103">Paramètres du Runbook</span><span class="sxs-lookup"><span data-stu-id="7ee87-103">Runbook settings</span></span>
<span data-ttu-id="7ee87-104">Chaque Runbook dans Azure Automation a plusieurs paramètres qui lui permettent d'être identifié et de modifier son comportement de journalisation.</span><span class="sxs-lookup"><span data-stu-id="7ee87-104">Each runbook in Azure Automation has multiple settings that help it to be identified and to change its logging behavior.</span></span> <span data-ttu-id="7ee87-105">Chacun de ces paramètres est décrit ci-dessous, suivi des procédures sur la façon de les modifier.</span><span class="sxs-lookup"><span data-stu-id="7ee87-105">Each of these settings is described below followed by procedures on how to modify them.</span></span>

## <a name="settings"></a><span data-ttu-id="7ee87-106">Paramètres</span><span class="sxs-lookup"><span data-stu-id="7ee87-106">Settings</span></span>
### <a name="name-and-description"></a><span data-ttu-id="7ee87-107">Nom et description</span><span class="sxs-lookup"><span data-stu-id="7ee87-107">Name and description</span></span>
<span data-ttu-id="7ee87-108">Vous ne pouvez pas modifier le nom d'un Runbook une fois qu'il a été créé.</span><span class="sxs-lookup"><span data-stu-id="7ee87-108">You cannot change the name of a runbook after it has been created.</span></span> <span data-ttu-id="7ee87-109">La description est facultative et peut comporter jusqu'à 512 caractères.</span><span class="sxs-lookup"><span data-stu-id="7ee87-109">The Description is optional and can be up to 512 characters.</span></span>

### <a name="tags"></a><span data-ttu-id="7ee87-110">Balises</span><span class="sxs-lookup"><span data-stu-id="7ee87-110">Tags</span></span>
<span data-ttu-id="7ee87-111">Les balises permettent d'attribuer des mots et des expressions distincts pour permettre d'identifier un Runbook.</span><span class="sxs-lookup"><span data-stu-id="7ee87-111">Tags allow you to assign distinct words and phrases to help identify a runbook.</span></span> <span data-ttu-id="7ee87-112">Par exemple, quand vous envoyez un Runbook à [PowerShell Gallery](https://www.powershellgallery.com/), vous spécifiez certaines balises pour identifier les catégories dans lesquelles le Runbook doit être répertorié.</span><span class="sxs-lookup"><span data-stu-id="7ee87-112">For example, when you submit a runbook to the [PowerShell Gallery](https://www.powershellgallery.com/), you specify particular tags to identify which categories the runbook should be listed in.</span></span> <span data-ttu-id="7ee87-113">Vous pouvez spécifier plusieurs balises pour un Runbook en les séparant par des virgules.</span><span class="sxs-lookup"><span data-stu-id="7ee87-113">You can specify multiple tags for a runbook by separating them with commas.</span></span>

### <a name="logging"></a><span data-ttu-id="7ee87-114">Journalisation</span><span class="sxs-lookup"><span data-stu-id="7ee87-114">Logging</span></span>
<span data-ttu-id="7ee87-115">Par défaut, les informations de commentaires et de progression ne sont pas écrites dans l'historique des tâches.</span><span class="sxs-lookup"><span data-stu-id="7ee87-115">By default, Verbose and Progress records are not written to job history.</span></span> <span data-ttu-id="7ee87-116">Vous pouvez modifier les paramètres d'un Runbook donné pour enregistrer ces informations.</span><span class="sxs-lookup"><span data-stu-id="7ee87-116">You can change the settings for a particular runbook to log these records.</span></span> <span data-ttu-id="7ee87-117">Pour en savoir plus sur ces informations, consultez [Sortie et messages de runbook](automation-runbook-output-and-messages.md).</span><span class="sxs-lookup"><span data-stu-id="7ee87-117">For more information on these records, see [Runbook Output and Messages](automation-runbook-output-and-messages.md).</span></span>

## <a name="changing-runbook-settings"></a><span data-ttu-id="7ee87-118">Modification des paramètres du Runbook</span><span class="sxs-lookup"><span data-stu-id="7ee87-118">Changing runbook settings</span></span>

### <a name="changing-runbook-settings-with-the-azure-portal"></a><span data-ttu-id="7ee87-119">Modification des paramètres du Runbook avec le portail Azure</span><span class="sxs-lookup"><span data-stu-id="7ee87-119">Changing runbook settings with the Azure portal</span></span>
<span data-ttu-id="7ee87-120">Vous pouvez modifier les paramètres d’un Runbook dans le portail Azure à partir du panneau **Paramètres** du Runbook.</span><span class="sxs-lookup"><span data-stu-id="7ee87-120">You can change settings for a runbook in the Azure portal from the **Settings** blade for the runbook.</span></span>

1. <span data-ttu-id="7ee87-121">Dans le portail Azure, sélectionnez **Automation** , puis cliquez sur le nom d'un compte Automation.</span><span class="sxs-lookup"><span data-stu-id="7ee87-121">In the Azure portal, select **Automation** and then then click the name of an automation account.</span></span>
2. <span data-ttu-id="7ee87-122">Sélectionnez l'onglet **Runbooks** .</span><span class="sxs-lookup"><span data-stu-id="7ee87-122">Select the **Runbooks** tab.</span></span>
3. <span data-ttu-id="7ee87-123">Cliquez sur le nom d’un Runbook pour accéder à son panneau Paramètres.</span><span class="sxs-lookup"><span data-stu-id="7ee87-123">Click the name of a runbook and you are directed to the settings blade for the runbook.</span></span> <span data-ttu-id="7ee87-124">De là, vous pouvez spécifier ou modifier des balises, la description du Runbook, configurer la journalisation et les paramètres de traçage, et accéder aux outils de prise en charge pour vous aider à résoudre les problèmes.</span><span class="sxs-lookup"><span data-stu-id="7ee87-124">From here you can specify or modify tags, the runbook description, configure logging and tracing settings, and access support tools to help you solve problems.</span></span>     

### <a name="changing-runbook-settings-with-windows-powershell"></a><span data-ttu-id="7ee87-125">Modification des paramètres du Runbook avec Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="7ee87-125">Changing runbook settings with Windows PowerShell</span></span>
<span data-ttu-id="7ee87-126">Vous pouvez utiliser l’applet de commande [Set-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603786.aspx) pour modifier les paramètres d’un Runbook.</span><span class="sxs-lookup"><span data-stu-id="7ee87-126">You can use the [Set-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603786.aspx) cmdlet to change the settings for a runbook.</span></span> <span data-ttu-id="7ee87-127">Si vous souhaitez spécifier plusieurs balises, vous pouvez fournir au paramètre Balises un tableau ou une chaîne unique avec les valeurs délimitées par des virgules.</span><span class="sxs-lookup"><span data-stu-id="7ee87-127">If you want to specify multiple tags, you can either provide an array or a single string with comma delimited values to the Tags parameter.</span></span> <span data-ttu-id="7ee87-128">Vous pouvez obtenir les balises actives avec [Get-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603728.aspx).</span><span class="sxs-lookup"><span data-stu-id="7ee87-128">You can get the current tags with the [Get-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603728.aspx).</span></span>

<span data-ttu-id="7ee87-129">Les exemples de commandes suivants montrent comment définir les propriétés d'un Runbook.</span><span class="sxs-lookup"><span data-stu-id="7ee87-129">The following sample commands show how to set the properties for a runbook.</span></span> <span data-ttu-id="7ee87-130">Cet exemple ajoute trois balises aux balises existantes et spécifie que les informations de commentaires doivent être enregistrées.</span><span class="sxs-lookup"><span data-stu-id="7ee87-130">This sample adds three tags to the existing tags and specifies that verbose records should be logged.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Sample-TestRunbook"
    $tags = (Get-AzureRmAutomationRunbook -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName $automationAccountName –Name $runbookName).Tags
    $tags += "Tag1,Tag2,Tag3"
    Set-AzureRmAutomationRunbook -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName $automationAccountName –Name $runbookName –LogVerbose $true –Tags $tags

## <a name="next-steps"></a><span data-ttu-id="7ee87-131">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7ee87-131">Next steps</span></span>
* <span data-ttu-id="7ee87-132">Pour découvrir comment créer et récupérer la sortie et les messages d’erreur à partir des Runbooks, consultez [Sortie et messages de Runbook dans Azure Automation](automation-runbook-output-and-messages.md)</span><span class="sxs-lookup"><span data-stu-id="7ee87-132">To learn how to create and retrieve output and error messages from runbooks, see [Runbook Output and Messages](automation-runbook-output-and-messages.md)</span></span> 
* <span data-ttu-id="7ee87-133">Pour découvrir comment ajouter un Runbook qui a déjà été développé par la Communauté ou une autre source, ou pour créer votre propre Runbook, consultez [Création ou importation d’un runbook](automation-creating-importing-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="7ee87-133">To understand how to add a runbook that was already developed by the community or other source, or to create your own runbook see [Creating or Importing a Runbook](automation-creating-importing-runbook.md)</span></span> 

