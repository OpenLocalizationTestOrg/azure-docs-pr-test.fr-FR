---
title: "les paramètres aaaRunbook | Documents Microsoft"
description: "Décrit les paramètres de configuration hello pour un runbook dans Azure Automation et comment toochange à l’aide des deux hello portail de gestion Azure et Windows PowerShell."
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
ms.openlocfilehash: 6f0ef09c148355a351464424c22c33df9300f0dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="runbook-settings"></a><span data-ttu-id="f3d29-103">Paramètres du Runbook</span><span class="sxs-lookup"><span data-stu-id="f3d29-103">Runbook settings</span></span>
<span data-ttu-id="f3d29-104">Chaque runbook dans Azure Automation a plusieurs paramètres que vous toobe identifié et toochange son comportement de journalisation.</span><span class="sxs-lookup"><span data-stu-id="f3d29-104">Each runbook in Azure Automation has multiple settings that help it toobe identified and toochange its logging behavior.</span></span> <span data-ttu-id="f3d29-105">Chacun de ces paramètres est décrite ci-dessous, suivie des procédures sur la façon de toomodify les.</span><span class="sxs-lookup"><span data-stu-id="f3d29-105">Each of these settings is described below followed by procedures on how toomodify them.</span></span>

## <a name="settings"></a><span data-ttu-id="f3d29-106">Paramètres</span><span class="sxs-lookup"><span data-stu-id="f3d29-106">Settings</span></span>
### <a name="name-and-description"></a><span data-ttu-id="f3d29-107">Nom et description</span><span class="sxs-lookup"><span data-stu-id="f3d29-107">Name and description</span></span>
<span data-ttu-id="f3d29-108">Vous ne pouvez pas modifier le nom hello d’un runbook une fois qu’elle a été créée.</span><span class="sxs-lookup"><span data-stu-id="f3d29-108">You cannot change hello name of a runbook after it has been created.</span></span> <span data-ttu-id="f3d29-109">Hello Description est facultative et peut être des caractères de too512.</span><span class="sxs-lookup"><span data-stu-id="f3d29-109">hello Description is optional and can be up too512 characters.</span></span>

### <a name="tags"></a><span data-ttu-id="f3d29-110">Tags</span><span class="sxs-lookup"><span data-stu-id="f3d29-110">Tags</span></span>
<span data-ttu-id="f3d29-111">Autoriser les balises que vous tooassign des mots distincts et expressions toohelp identifient un runbook.</span><span class="sxs-lookup"><span data-stu-id="f3d29-111">Tags allow you tooassign distinct words and phrases toohelp identify a runbook.</span></span> <span data-ttu-id="f3d29-112">Par exemple, lorsque vous envoyez un toohello runbook [PowerShell Gallery](https://www.powershellgallery.com/), vous spécifiez tooidentify certaines balises les catégories hello runbook doit être indiquée dans.</span><span class="sxs-lookup"><span data-stu-id="f3d29-112">For example, when you submit a runbook toohello [PowerShell Gallery](https://www.powershellgallery.com/), you specify particular tags tooidentify which categories hello runbook should be listed in.</span></span> <span data-ttu-id="f3d29-113">Vous pouvez spécifier plusieurs balises pour un Runbook en les séparant par des virgules.</span><span class="sxs-lookup"><span data-stu-id="f3d29-113">You can specify multiple tags for a runbook by separating them with commas.</span></span>

### <a name="logging"></a><span data-ttu-id="f3d29-114">Journalisation</span><span class="sxs-lookup"><span data-stu-id="f3d29-114">Logging</span></span>
<span data-ttu-id="f3d29-115">Par défaut, les enregistrements détaillés et de progression ne sont pas écrites toojob historique.</span><span class="sxs-lookup"><span data-stu-id="f3d29-115">By default, Verbose and Progress records are not written toojob history.</span></span> <span data-ttu-id="f3d29-116">Vous pouvez modifier les paramètres de hello pour un runbook donné de toolog de ces enregistrements.</span><span class="sxs-lookup"><span data-stu-id="f3d29-116">You can change hello settings for a particular runbook toolog these records.</span></span> <span data-ttu-id="f3d29-117">Pour en savoir plus sur ces informations, consultez [Sortie et messages de runbook](automation-runbook-output-and-messages.md).</span><span class="sxs-lookup"><span data-stu-id="f3d29-117">For more information on these records, see [Runbook Output and Messages](automation-runbook-output-and-messages.md).</span></span>

## <a name="changing-runbook-settings"></a><span data-ttu-id="f3d29-118">Modification des paramètres du Runbook</span><span class="sxs-lookup"><span data-stu-id="f3d29-118">Changing runbook settings</span></span>

### <a name="changing-runbook-settings-with-hello-azure-portal"></a><span data-ttu-id="f3d29-119">Modification des paramètres de runbook avec hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="f3d29-119">Changing runbook settings with hello Azure portal</span></span>
<span data-ttu-id="f3d29-120">Vous pouvez modifier les paramètres d’un runbook Bonjour portail Azure à partir de hello **paramètres** panneau hello runbook.</span><span class="sxs-lookup"><span data-stu-id="f3d29-120">You can change settings for a runbook in hello Azure portal from hello **Settings** blade for hello runbook.</span></span>

1. <span data-ttu-id="f3d29-121">Bonjour portail Azure, sélectionnez **Automation** , puis cliquez sur nom hello d’un compte automation.</span><span class="sxs-lookup"><span data-stu-id="f3d29-121">In hello Azure portal, select **Automation** and then then click hello name of an automation account.</span></span>
2. <span data-ttu-id="f3d29-122">Sélectionnez hello **Runbooks** onglet.</span><span class="sxs-lookup"><span data-stu-id="f3d29-122">Select hello **Runbooks** tab.</span></span>
3. <span data-ttu-id="f3d29-123">Cliquez sur le nom hello d’un runbook et que vous êtes dirigé toohello panneau des paramètres pour hello runbook.</span><span class="sxs-lookup"><span data-stu-id="f3d29-123">Click hello name of a runbook and you are directed toohello settings blade for hello runbook.</span></span> <span data-ttu-id="f3d29-124">À partir d’ici vous pouvez spécifier ou modifier des balises, hello description de runbook, configurer la journalisation et le suivi des paramètres et toohelp d’outils de prise en charge de résoudre les problèmes d’accès.</span><span class="sxs-lookup"><span data-stu-id="f3d29-124">From here you can specify or modify tags, hello runbook description, configure logging and tracing settings, and access support tools toohelp you solve problems.</span></span>     

### <a name="changing-runbook-settings-with-windows-powershell"></a><span data-ttu-id="f3d29-125">Modification des paramètres du Runbook avec Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="f3d29-125">Changing runbook settings with Windows PowerShell</span></span>
<span data-ttu-id="f3d29-126">Vous pouvez utiliser hello [Set-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603786.aspx) paramètres de hello toochange applet de commande d’un runbook.</span><span class="sxs-lookup"><span data-stu-id="f3d29-126">You can use hello [Set-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603786.aspx) cmdlet toochange hello settings for a runbook.</span></span> <span data-ttu-id="f3d29-127">Si vous souhaitez toospecify plusieurs balises, vous pouvez fournir un tableau ou une chaîne unique avec le paramètre délimité par des virgules valeurs toohello balises.</span><span class="sxs-lookup"><span data-stu-id="f3d29-127">If you want toospecify multiple tags, you can either provide an array or a single string with comma delimited values toohello Tags parameter.</span></span> <span data-ttu-id="f3d29-128">Vous pouvez obtenir des balises actives de hello avec hello [Get-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603728.aspx).</span><span class="sxs-lookup"><span data-stu-id="f3d29-128">You can get hello current tags with hello [Get-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603728.aspx).</span></span>

<span data-ttu-id="f3d29-129">Hello suivant des exemples de commandes montrent comment tooset hello les propriétés d’un runbook.</span><span class="sxs-lookup"><span data-stu-id="f3d29-129">hello following sample commands show how tooset hello properties for a runbook.</span></span> <span data-ttu-id="f3d29-130">Cet exemple ajoute trois balises toohello les balises et spécifie que les enregistrements détaillés doivent être enregistrés.</span><span class="sxs-lookup"><span data-stu-id="f3d29-130">This sample adds three tags toohello existing tags and specifies that verbose records should be logged.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Sample-TestRunbook"
    $tags = (Get-AzureRmAutomationRunbook -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName $automationAccountName –Name $runbookName).Tags
    $tags += "Tag1,Tag2,Tag3"
    Set-AzureRmAutomationRunbook -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName $automationAccountName –Name $runbookName –LogVerbose $true –Tags $tags

## <a name="next-steps"></a><span data-ttu-id="f3d29-131">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f3d29-131">Next steps</span></span>
* <span data-ttu-id="f3d29-132">toolearn comment les messages de sortie et d’erreur toocreate et récupérer à partir de procédures opérationnelles, consultez [Runbook Output and Messages](automation-runbook-output-and-messages.md)</span><span class="sxs-lookup"><span data-stu-id="f3d29-132">toolearn how toocreate and retrieve output and error messages from runbooks, see [Runbook Output and Messages](automation-runbook-output-and-messages.md)</span></span> 
* <span data-ttu-id="f3d29-133">toounderstand tooadd un runbook a été développée par la Communauté de hello ou d’autres sources ou toocreate vos propres runbook voir [création ou importation d’un Runbook](automation-creating-importing-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="f3d29-133">toounderstand how tooadd a runbook that was already developed by hello community or other source, or toocreate your own runbook see [Creating or Importing a Runbook](automation-creating-importing-runbook.md)</span></span> 
