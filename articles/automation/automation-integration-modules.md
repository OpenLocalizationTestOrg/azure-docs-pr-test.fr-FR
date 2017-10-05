---
title: "<span data-ttu-id=\"8a10c-101\">Créer un module d’intégration Azure Automation | Microsoft Docs</span><span class=\"sxs-lookup\"><span data-stu-id=\"8a10c-101\">Create an Azure Automation Integration Module | Microsoft Docs</span></span>"
description: "<span data-ttu-id=\"8a10c-102\">Ce didacticiel vous guide tout au long des procédures de création et de test de modules d’intégration Azure Automation. Il est complété par un exemple d’utilisation.</span><span class=\"sxs-lookup\"><span data-stu-id=\"8a10c-102\">Tutorial that walks you through the creation, testing, and example use of  integration modules in Azure Automation.</span></span>"
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
ms.assetid: 27798efb-08b9-45d9-9b41-5ad91a3df41e
ms.service: automation
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/13/2017
ms.author: magoedte
ms.openlocfilehash: aeb06276a52e5472667ae0a741fb3007a91910fe
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-automation-integration-modules"></a><span data-ttu-id="8a10c-103">Modules d’intégration Azure Automation</span><span class="sxs-lookup"><span data-stu-id="8a10c-103">Azure Automation Integration Modules</span></span>
<span data-ttu-id="8a10c-104">PowerShell est la technologie fondamentale derrière Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="8a10c-104">PowerShell is the fundamental technology behind Azure Automation.</span></span> <span data-ttu-id="8a10c-105">Étant donné qu’Azure Automation est basé sur PowerShell, les modules PowerShell sont essentiels pour l’extensibilité d’Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="8a10c-105">Since Azure Automation is built on PowerShell, PowerShell modules are key to the extensibility of Azure Automation.</span></span> <span data-ttu-id="8a10c-106">Dans cet article, nous vous guiderons tout au long de l’utilisation détaillée des modules PowerShell dans Azure Automation, appelés « modules d’intégration », et vous présenterons les meilleures pratiques pour la création de vos propres modules PowerShell afin de garantir que ceux-ci fonctionnent en tant que modules d’intégration au sein d’Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="8a10c-106">In this article, we will guide you through the specifics of Azure Automation’s use of PowerShell modules, referred to as “Integration Modules”, and best practices for creating your own PowerShell modules to make sure they work as Integration Modules within Azure Automation.</span></span> 

## <a name="what-is-a-powershell-module"></a><span data-ttu-id="8a10c-107">Qu’est-ce qu’un module PowerShell ?</span><span class="sxs-lookup"><span data-stu-id="8a10c-107">What is a PowerShell Module?</span></span>
<span data-ttu-id="8a10c-108">Un module PowerShell est un groupe d’applets de commande PowerShell, telles que **Get-Date** ou **Copy-Item**, qui peut être utilisé à partir de la console PowerShell, de scripts, de flux de travail, de Runbooks et de ressources PowerShell DSC, telles que WindowsFeature ou File, pouvant être utilisées à partir de configurations PowerShell DSC.</span><span class="sxs-lookup"><span data-stu-id="8a10c-108">A PowerShell module is a group of PowerShell cmdlets like **Get-Date** or **Copy-Item**, that can be used from the PowerShell console, scripts, workflows, runbooks, and PowerShell DSC resources like WindowsFeature or File, that can be used from PowerShell DSC configurations.</span></span> <span data-ttu-id="8a10c-109">L’ensemble des fonctionnalités de PowerShell sont exposées via les applets de commande et les ressources DSC, et chaque applet de commande/ressource DSC est prise en charge par un module PowerShell ; un nombre important de ces modules est inclus dans PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8a10c-109">All of the functionality of PowerShell is exposed through cmdlets and DSC resources, and every cmdlet/DSC resource is backed by a PowerShell module, many of which ship with PowerShell itself.</span></span> <span data-ttu-id="8a10c-110">Par exemple, l’applet de commande **Get-Date** fait partie du module PowerShell Microsoft.PowerShell.Utility, et l’applet de commande **Copy-Item** fait partie du module PowerShell Microsoft.PowerShell.Management. La ressource de Package DSC fait partie du module PowerShell PSDesiredStateConfiguration.</span><span class="sxs-lookup"><span data-stu-id="8a10c-110">For example, the **Get-Date** cmdlet is part of the Microsoft.PowerShell.Utility PowerShell module, and **Copy-Item** cmdlet is part of the Microsoft.PowerShell.Management PowerShell module and the Package DSC resource is part of the PSDesiredStateConfiguration PowerShell module.</span></span> <span data-ttu-id="8a10c-111">Ces deux modules sont fournis avec PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8a10c-111">Both of these modules ship with PowerShell.</span></span> <span data-ttu-id="8a10c-112">Mais de nombreux modules PowerShell ne sont pas fournis avec PowerShell ; ils sont distribués avec des produits tiers ou internes, tels que System Center 2012 Configuration Manager ou par la vaste communauté PowerShell sur des sites comme PowerShell Gallery.</span><span class="sxs-lookup"><span data-stu-id="8a10c-112">But many PowerShell modules do not ship as part of PowerShell, and are instead distributed with first or third-party products like System Center 2012 Configuration Manager or by the vast PowerShell community on places like PowerShell Gallery.</span></span>  <span data-ttu-id="8a10c-113">Ces modules sont utiles car ils simplifient des tâches complexes grâce à la fonctionnalité d’encapsulation.</span><span class="sxs-lookup"><span data-stu-id="8a10c-113">The modules are useful because they make complex tasks simpler through encapsulated functionality.</span></span>  <span data-ttu-id="8a10c-114">Vous pouvez en savoir plus sur les [modules PowerShell sur MSDN](https://msdn.microsoft.com/library/dd878324%28v=vs.85%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="8a10c-114">You can learn more about [PowerShell modules on MSDN](https://msdn.microsoft.com/library/dd878324%28v=vs.85%29.aspx).</span></span> 

## <a name="what-is-an-azure-automation-integration-module"></a><span data-ttu-id="8a10c-115">Qu’est-ce qu’un module d’intégration Azure Automation ?</span><span class="sxs-lookup"><span data-stu-id="8a10c-115">What is an Azure Automation Integration Module?</span></span>
<span data-ttu-id="8a10c-116">Un module d’intégration n’est pas très différent d’un module PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8a10c-116">An Integration Module isn't very different from a PowerShell module.</span></span> <span data-ttu-id="8a10c-117">Il s’agit simplement d’un module PowerShell contenant éventuellement un fichier supplémentaire : un fichier de métadonnées spécifiant un type de connexion Azure Automation à utiliser avec les applets de commande du module dans les Runbooks.</span><span class="sxs-lookup"><span data-stu-id="8a10c-117">Its simply a PowerShell module that optionally contains one additional file - a metadata file specifying an Azure Automation connection type to be used with the module's cmdlets in runbooks.</span></span> <span data-ttu-id="8a10c-118">Qu’ils contiennent ce fichier ou non, ces modules PowerShell peuvent être importés dans Azure Automation pour activer leurs applets de commande pour une utilisation dans les Runbooks et leurs ressources DSC disponibles au sein des configurations DSC.</span><span class="sxs-lookup"><span data-stu-id="8a10c-118">Optional file or not, these PowerShell modules can be imported into Azure Automation to make their cmdlets available for use within runbooks and their DSC resources available for use within DSC configurations.</span></span> <span data-ttu-id="8a10c-119">Dans les coulisses, Azure Automation stocke ces modules et, lors de l’exécution d’un travail de compilation de DSC ou d’une tâche de Runbook, les charge dans les bacs à sable (sandbox) Azure Automation où les Runbooks sont exécutés et les configurations DSC sont compilées.</span><span class="sxs-lookup"><span data-stu-id="8a10c-119">Behind the scenes, Azure Automation stores these modules, and at runbook job and DSC compilation job execution time, loads them into the Azure Automation sandboxes where runbooks are executed and DSC configurations are compiled.</span></span>  <span data-ttu-id="8a10c-120">Toute ressource DSC dans les modules est automatiquement placée sur le serveur Automation DSC afin de pouvoir être extraite par les ordinateurs qui tentent d’appliquer des configurations DSC.</span><span class="sxs-lookup"><span data-stu-id="8a10c-120">Any DSC resources in modules are also automatically placed on the Automation DSC pull server, so that they can be pulled by machines attempting to apply DSC configurations.</span></span>  

<span data-ttu-id="8a10c-121">Dans Azure Automation, nous vous fournissons un certain nombre de modules Azure PowerShell prêts à l’emploi, pour une automatisation immédiate de la gestion Azure. Vous pouvez également importer des modules PowerShell pour les intégrer à tout système, service ou outil que vous souhaitez.</span><span class="sxs-lookup"><span data-stu-id="8a10c-121">We ship a number of Azure  PowerShell modules out of the box in Azure Automation for you to use so you can get started automating Azure management right away, but you can import PowerShell modules for whatever system, service, or tool you want to integrate with.</span></span> 

> [!NOTE]
> <span data-ttu-id="8a10c-122">Certains modules sont fournis en tant que « modules globaux » dans le service Automation.</span><span class="sxs-lookup"><span data-stu-id="8a10c-122">Certain modules are shipped as “global modules” in the Automation service.</span></span> <span data-ttu-id="8a10c-123">Ces modules globaux sont disponibles lorsque vous créez un compte Automation. Nous les mettons parfois à jour ce qui les transfère automatiquement en dehors de votre compte Automation.</span><span class="sxs-lookup"><span data-stu-id="8a10c-123">These global modules are available to you when you create an automation account, and we update them sometimes which automatically pushes them out to your automation account.</span></span> <span data-ttu-id="8a10c-124">Si vous ne souhaitez pas qu’ils soient mis à jour automatiquement, vous pouvez toujours importer le même module vous-même. Celui-ci primera sur la version du module global fournie dans le service.</span><span class="sxs-lookup"><span data-stu-id="8a10c-124">If you don’t want them to be auto-updated, you can always import the same module yourself, and that will take precedence over the global module version of that module that we ship in the service.</span></span> 

<span data-ttu-id="8a10c-125">Le format dans lequel vous importez un package de module d’intégration est un fichier compressé portant le même nom que le module et une extension .zip.</span><span class="sxs-lookup"><span data-stu-id="8a10c-125">The format in which you import an Integration Module package is a compressed file with the same name as the module and a .zip extension.</span></span> <span data-ttu-id="8a10c-126">Il contient le module Windows PowerShell et tout fichier de prise en charge, notamment un fichier manifeste (.psd1), le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="8a10c-126">It contains the Windows PowerShell module and any supporting files, including a manifest file (.psd1) if the module has one.</span></span>

<span data-ttu-id="8a10c-127">Si le module doit contenir un type de connexion Azure Automation, il doit également contenir un fichier portant le nom `<ModuleName>-Automation.json` qui spécifie les propriétés de type de connexion.</span><span class="sxs-lookup"><span data-stu-id="8a10c-127">If the module should contain an Azure Automation connection type, it must also contain a file with the name `<ModuleName>-Automation.json` that specifies the connection type properties.</span></span> <span data-ttu-id="8a10c-128">Il s’agit d’un fichier json placé dans le dossier du module de votre fichier .zip compressé et contenant les champs d’une « connexion » ; ces derniers sont requis pour se connecter au système ou au service que représente le module.</span><span class="sxs-lookup"><span data-stu-id="8a10c-128">This is a json file placed within the module folder of your compressed .zip file, and contains the fields of a “connection” that is required to connect to the system or service the module represents.</span></span> <span data-ttu-id="8a10c-129">Ceci créera un type de connexion dans Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="8a10c-129">This will end up creating a connection type in Azure Automation.</span></span> <span data-ttu-id="8a10c-130">À l’aide de ce fichier, vous pouvez définir les noms de champ et les types, ainsi que si les champs doivent être chiffrés et/ou facultatifs, pour le type de connexion du module.</span><span class="sxs-lookup"><span data-stu-id="8a10c-130">Using this file you can set the field names, types, and whether the fields should be encrypted and / or optional, for the connection type of the module.</span></span> <span data-ttu-id="8a10c-131">Voici un modèle au format json :</span><span class="sxs-lookup"><span data-stu-id="8a10c-131">The following is a template in the json file format:</span></span>

```
{ 
   "ConnectionFields": [
   {
      "IsEncrypted":  false,
      "IsOptional":  false,
      "Name":  "ComputerName",
      "TypeName":  "System.String"
   },
   {
      "IsEncrypted":  false,
      "IsOptional":  true,
      "Name":  "Username",
      "TypeName":  "System.String"
   },
   {
      "IsEncrypted":  true,
      "IsOptional":  false,
      "Name":  "Password",
   "TypeName":  "System.String"
   }],
   "ConnectionTypeName":  "DataProtectionManager",
   "IntegrationModuleName":  "DataProtectionManager"
}
```

<span data-ttu-id="8a10c-132">Si vous avez déjà déployé Service Management Automation et créé des packages de modules d’intégration pour vos Runbooks d’automation, vous devriez déjà connaître cette procédure.</span><span class="sxs-lookup"><span data-stu-id="8a10c-132">If you have deployed Service Management Automation and created Integration Modules packages for your automation runbooks, this should look very familiar to you.</span></span> 

## <a name="authoring-best-practices"></a><span data-ttu-id="8a10c-133">Établissement de meilleures pratiques</span><span class="sxs-lookup"><span data-stu-id="8a10c-133">Authoring Best Practices</span></span>
<span data-ttu-id="8a10c-134">Même si les modules d’intégration sont généralement des modules PowerShell, nous vous recommandons de prendre en compte certains éléments lors de la création d’un module PowerShell, pour une utilisation optimale de ce dernier dans Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="8a10c-134">Even though Integration Modules are essentially PowerShell modules, there’s still a number of things we recommend you consider while authoring a PowerShell module, to make it most usable in Azure Automation.</span></span> <span data-ttu-id="8a10c-135">Certains d’entre eux sont propres à Azure Automation, et certains sont utiles pour améliorer le fonctionnement de vos modules dans le Workflow PowerShell, que vous utilisiez Azure Automation ou non.</span><span class="sxs-lookup"><span data-stu-id="8a10c-135">Some of these are Azure Automation specific, and some of them are useful just to make your modules work well in PowerShell Workflow, regardless of whether or not you’re using Automation.</span></span> 

1. <span data-ttu-id="8a10c-136">Incluez un résumé, une description et une URI d’aide pour chaque applet de commande dans le module.</span><span class="sxs-lookup"><span data-stu-id="8a10c-136">Include a synopsis, description, and help URI for every cmdlet in the module.</span></span> <span data-ttu-id="8a10c-137">Dans PowerShell, vous pouvez définir certaines informations d’aide pour les applets de commande, pour que l’utilisateur puisse obtenir de l’aide quant à leur utilisation, avec l’applet de commande **Get-Help** .</span><span class="sxs-lookup"><span data-stu-id="8a10c-137">In PowerShell, you can define certain help information for cmdlets to allow the user to receive help on using them with the **Get-Help** cmdlet.</span></span> <span data-ttu-id="8a10c-138">Par exemple, voici comment définir un synopsis et l’URI d’aide pour un module PowerShell écrit dans un fichier .psm1.</span><span class="sxs-lookup"><span data-stu-id="8a10c-138">For example, here’s how you can define a synopsis and help URI for a PowerShell module written in a .psm1 file.</span></span><br>  
   
    ```
    <#
        .SYNOPSIS
         Gets all outgoing phone numbers for this Twilio account 
    #>
    function Get-TwilioPhoneNumbers {
    [CmdletBinding(DefaultParameterSetName='SpecifyConnectionFields', `
    HelpUri='http://www.twilio.com/docs/api/rest/outgoing-caller-ids')]
    param(
       [Parameter(ParameterSetName='SpecifyConnectionFields', Mandatory=$true)]
       [ValidateNotNullOrEmpty()]
       [string]
       $AccountSid,
   
       [Parameter(ParameterSetName='SpecifyConnectionFields', Mandatory=$true)]
       [ValidateNotNullOrEmpty()]
       [string]
       $AuthToken,
   
       [Parameter(ParameterSetName='UseConnectionObject', Mandatory=$true)]
       [ValidateNotNullOrEmpty()]
       [Hashtable]
       $Connection
    )
   
    $cred = CreateTwilioCredential -Connection $Connection -AccountSid $AccountSid -AuthToken $AuthToken
   
    $uri = "$TWILIO_BASE_URL/Accounts/" + $cred.UserName + "/IncomingPhoneNumbers"
   
    $response = Invoke-RestMethod -Method Get -Uri $uri -Credential $cred
   
    $response.TwilioResponse.IncomingPhoneNumbers.IncomingPhoneNumber
    }
    ```
   <br> <span data-ttu-id="8a10c-139">Cette information affichera de l’aide avec l’applet de commande **Get-Help** dans la console PowerShell, ainsi que dans Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="8a10c-139">Providing this info will not only show this help using the **Get-Help** cmdlet in the PowerShell console, it will also expose this help functionality within Azure Automation.</span></span>  <span data-ttu-id="8a10c-140">Par exemple, lors de l’insertion d’activités lors de la création de runbook.</span><span class="sxs-lookup"><span data-stu-id="8a10c-140">For example, when inserting activities during runbook authoring.</span></span> <span data-ttu-id="8a10c-141">En cliquant sur « Voir l’aide détaillée », l’URI d’aide s’ouvre dans un autre onglet du navigateur web que vous utilisez pour accéder à Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="8a10c-141">Clicking “View detailed help” will open the help URI in another tab of the web browser you’re using to access Azure Automation.</span></span><br><span data-ttu-id="8a10c-142">![Aide du module d’intégration](media/automation-integration-modules/automation-integration-module-activitydesc.png)</span><span class="sxs-lookup"><span data-stu-id="8a10c-142">![Integration Module Help](media/automation-integration-modules/automation-integration-module-activitydesc.png)</span></span>
2. <span data-ttu-id="8a10c-143">Si le module s’exécute sur un système distant,</span><span class="sxs-lookup"><span data-stu-id="8a10c-143">If the module runs against a remote system,</span></span>

    <span data-ttu-id="8a10c-144">a.</span><span class="sxs-lookup"><span data-stu-id="8a10c-144">a.</span></span> <span data-ttu-id="8a10c-145">Il doit contenir un fichier de métadonnées du module d’intégration qui définit les informations nécessaires pour se connecter à ce système distant, c’est-à-dire le type de connexion.</span><span class="sxs-lookup"><span data-stu-id="8a10c-145">It should contain an Integration Module metadata file that defines the information needed to connect to that remote system, meaning the connection type.</span></span>  
    <span data-ttu-id="8a10c-146">b.</span><span class="sxs-lookup"><span data-stu-id="8a10c-146">b.</span></span> <span data-ttu-id="8a10c-147">Chaque applet de commande du module doit pouvoir accueillir un objet de connexion (une instance de ce type de connexion) en tant que paramètre.</span><span class="sxs-lookup"><span data-stu-id="8a10c-147">Each cmdlet in the module should be able to take in a connection object (an instance of that connection type) as a parameter.</span></span>  

    <span data-ttu-id="8a10c-148">Les applets de commande du module sont plus faciles à utiliser dans Azure Automation si vous autorisez le passage d’un objet, avec les champs du type de connexion en tant que paramètre, vers l’applet de commande.</span><span class="sxs-lookup"><span data-stu-id="8a10c-148">Cmdlets in the module become easier to use in Azure Automation if you allow passing an object with the fields of the connection type as a parameter to the cmdlet.</span></span> <span data-ttu-id="8a10c-149">Ainsi, les utilisateurs ne sont pas obligés de mapper les paramètres de la ressource de connexion aux paramètres correspondants de l’applet de commande chaque fois qu’ils appellent une applet de commande.</span><span class="sxs-lookup"><span data-stu-id="8a10c-149">This way users don’t have to map parameters of the connection asset to the cmdlet's corresponding parameters each time they call a cmdlet.</span></span> <span data-ttu-id="8a10c-150">Selon l’exemple de Runbook ci-dessus, il utilise une ressource de connexion Twilio, appelée CorpTwilio, pour accéder à Twilio et renvoyer tous les numéros de téléphone du compte.</span><span class="sxs-lookup"><span data-stu-id="8a10c-150">Based on the runbook example above, it uses a Twilio connection asset called CorpTwilio to access Twilio and return all the phone numbers in the account.</span></span>  <span data-ttu-id="8a10c-151">Remarquez comment il mappe les champs de la connexion aux paramètres de l’applet de commande.</span><span class="sxs-lookup"><span data-stu-id="8a10c-151">Notice how it is mapping the fields of the connection to the parameters of the cmdlet?</span></span><br>
   
    ```
    workflow Get-CorpTwilioPhones
    {
      $CorpTwilio = Get-AutomationConnection -Name 'CorpTwilio'
   
      Get-TwilioPhoneNumbers 
        -AccountSid $CorpTwilio.AccountSid  
        -AuthToken $CorptTwilio.AuthToken
    }
    ```
  
    <span data-ttu-id="8a10c-152">Une approche plus simple consisterait à passer l’objet de connexion directement à l’applet de commande -</span><span class="sxs-lookup"><span data-stu-id="8a10c-152">An easier and better way to approach this is directly passing the connection object to the cmdlet -</span></span>
   
    ```
    workflow Get-CorpTwilioPhones
    {
      $CorpTwilio = Get-AutomationConnection -Name 'CorpTwilio'
   
      Get-TwilioPhoneNumbers -Connection $CorpTwilio
    }
    ```
   
    <span data-ttu-id="8a10c-153">Vous pouvez activer un tel comportement pour vos applets de commande en les autorisant à accepter un objet de connexion directement en tant que paramètre, au lieu d’accepter uniquement des champs de connexion en tant que paramètres.</span><span class="sxs-lookup"><span data-stu-id="8a10c-153">You can enable behavior like this for your cmdlets by allowing them to accept a connection object directly as a parameter, instead of just connection fields for parameters.</span></span> <span data-ttu-id="8a10c-154">Généralement, vous voudrez disposer d’un jeu de paramètres pour chaque élément, pour qu’un utilisateur n’utilisant pas Azure Automation puisse appeler vos applets de commande sans créer une table de hachage agissant en tant qu’objet de connexion.</span><span class="sxs-lookup"><span data-stu-id="8a10c-154">Usually you’ll want a parameter set for each, so that a user not using Azure Automation can call your cmdlets without constructing a hashtable to act as the connection object.</span></span> <span data-ttu-id="8a10c-155">Le jeu de paramètres **SpecifyConnectionFields** ci-dessous permet de faire passer, une par une, les propriétés de champ de connexion.</span><span class="sxs-lookup"><span data-stu-id="8a10c-155">Parameter set **SpecifyConnectionFields** below is used to pass the connection field properties one by one.</span></span> <span data-ttu-id="8a10c-156">**UseConnectionObject** vous permet de transmettre directement la connexion.</span><span class="sxs-lookup"><span data-stu-id="8a10c-156">**UseConnectionObject** lets you pass the connection straight through.</span></span> <span data-ttu-id="8a10c-157">Comme vous pouvez le voir, l’applet de commande Send-TwilioSMS dans le [module Twilio de PowerShell](https://gallery.technet.microsoft.com/scriptcenter/Twilio-PowerShell-Module-8a8bfef8) autorise le passage dans les deux cas :</span><span class="sxs-lookup"><span data-stu-id="8a10c-157">As you can see, the Send-TwilioSMS cmdlet in the [Twilio PowerShell module](https://gallery.technet.microsoft.com/scriptcenter/Twilio-PowerShell-Module-8a8bfef8) allows passing either way:</span></span> 
   
    ```
    function Send-TwilioSMS {
      [CmdletBinding(DefaultParameterSetName='SpecifyConnectionFields', `
      HelpUri='http://www.twilio.com/docs/api/rest/sending-sms')]
      param(
         [Parameter(ParameterSetName='SpecifyConnectionFields', Mandatory=$true)]
         [ValidateNotNullOrEmpty()]
         [string]
         $AccountSid,
   
         [Parameter(ParameterSetName='SpecifyConnectionFields', Mandatory=$true)]
         [ValidateNotNullOrEmpty()]
         [string]
         $AuthToken,
   
         [Parameter(ParameterSetName='UseConnectionObject', Mandatory=$true)]
         [ValidateNotNullOrEmpty()]
         [Hashtable]
         $Connection
   
       )
    }
    ```
   <br>
3. <span data-ttu-id="8a10c-158">Définissez le type de sortie pour toutes les applets de commande dans le module.</span><span class="sxs-lookup"><span data-stu-id="8a10c-158">Define output type for all cmdlets in the module.</span></span> <span data-ttu-id="8a10c-159">La définition d’un type de sortie pour une applet de commande permet à IntelliSense (au moment de la conception) de vous aider à déterminer les propriétés de sortie de l’applet de commande, à utiliser lors de la création.</span><span class="sxs-lookup"><span data-stu-id="8a10c-159">Defining an output type for a cmdlet allows design-time IntelliSense to help you determine the output properties of the cmdlet, for use during authoring.</span></span> <span data-ttu-id="8a10c-160">Cela est particulièrement utile lors de la création graphique d’un Runbook Azure Automation, où les connaissances au moment de la conception sont essentielles pour une expérience utilisateur conviviale de votre module.</span><span class="sxs-lookup"><span data-stu-id="8a10c-160">It is especially helpful during Automation runbook graphical authoring, where design time knowledge is key to an easy user experience with your module.</span></span><br><br> <span data-ttu-id="8a10c-161">![Type de sortie de Runbook graphique](media/automation-integration-modules/runbook-graphical-module-output-type.png)</span><span class="sxs-lookup"><span data-stu-id="8a10c-161">![Graphical Runbook Output Type](media/automation-integration-modules/runbook-graphical-module-output-type.png)</span></span><br> <span data-ttu-id="8a10c-162">Cela ressemble à la fonctionnalité de « frappe au kilomètre » de la sortie d’une applet de commande dans PowerShell ISE, sans avoir à exécuter celle-ci.</span><span class="sxs-lookup"><span data-stu-id="8a10c-162">This is similar to the "type ahead" functionality of a cmdlet's output in PowerShell ISE without having to run it.</span></span><br><br> <span data-ttu-id="8a10c-163">![POSH IntelliSense](media/automation-integration-modules/automation-posh-ise-intellisense.png)</span><span class="sxs-lookup"><span data-stu-id="8a10c-163">![POSH IntelliSense](media/automation-integration-modules/automation-posh-ise-intellisense.png)</span></span><br>
4. <span data-ttu-id="8a10c-164">Les applets de commande dans le module ne doivent pas prendre des types d’objets complexes en tant que paramètres.</span><span class="sxs-lookup"><span data-stu-id="8a10c-164">Cmdlets in the module should not take complex object types for parameters.</span></span> <span data-ttu-id="8a10c-165">La différence entre PowerShell et le Workflow PowerShell réside dans le fait que ce dernier stocke des types complexes sous forme désérialisée.</span><span class="sxs-lookup"><span data-stu-id="8a10c-165">PowerShell Workflow is different from PowerShell in that it stores complex types in deserialized form.</span></span> <span data-ttu-id="8a10c-166">Les types primitifs resteront primitifs, mais les types complexes sont convertis en leurs versions désérialisées, qui sont avant tout des conteneurs de propriétés.</span><span class="sxs-lookup"><span data-stu-id="8a10c-166">Primitive types will stay as primitives, but complex types are converted to their deserialized versions, which are essentially property bags.</span></span> <span data-ttu-id="8a10c-167">Par exemple, si vous avez utilisé l’applet de commande **Get-Process** dans un Runbook (voire un Workflow PowerShell), elle retourne un objet de type [Deserialized.System.Diagnostic.Process], pas le type [System.Diagnostic.Process] attendu.</span><span class="sxs-lookup"><span data-stu-id="8a10c-167">For example, if you used the **Get-Process** cmdlet in a runbook (or a PowerShell Workflow for that matter), it would return an object of type [Deserialized.System.Diagnostic.Process], not the expected [System.Diagnostic.Process] type.</span></span> <span data-ttu-id="8a10c-168">Ce type a les mêmes propriétés que le type non désérialisé, mais aucune de ses méthodes.</span><span class="sxs-lookup"><span data-stu-id="8a10c-168">This type has all the same properties as the non-deserialized type, but none of the methods.</span></span> <span data-ttu-id="8a10c-169">Et si vous essayez de transmettre cette valeur vers une applet de commande en tant que paramètre, bien que cette dernière attende une valeur [System.Diagnostic.Process] pour ce paramètre, vous obtiendrez l’erreur suivante : *Impossible de traiter la transformation d’argument sur le paramètre « process ». Error: "Cannot convert the "System.Diagnostics.Process (CcmExec)" value of type "Deserialized.System.Diagnostics.Process" to type "System.Diagnostics.Process" (Erreur : « impossible de convertir la valeur « System.Diagnostics.Process (CcmExec) » de type « Deserialized.System.Diagnostics.Process » en type « System.Diagnostics.Process »).*</span><span class="sxs-lookup"><span data-stu-id="8a10c-169">And if you try to pass this value as a parameter to a cmdlet, where the cmdlet expects a [System.Diagnostic.Process] value for this parameter, you’ll receive the following error: *Cannot process argument transformation on parameter 'process'. Error: "Cannot convert the "System.Diagnostics.Process (CcmExec)" value of type  "Deserialized.System.Diagnostics.Process" to type "System.Diagnostics.Process".*</span></span>   <span data-ttu-id="8a10c-170">Ceci provient de l’incompatibilité de type entre le type [System.Diagnostic.Process] attendu et le type [Deserialized.System.Diagnostic.Process] donné.</span><span class="sxs-lookup"><span data-stu-id="8a10c-170">This is because there is a type mismatch between the expected [System.Diagnostic.Process] type and the given [Deserialized.System.Diagnostic.Process] type.</span></span> <span data-ttu-id="8a10c-171">Pour contourner ce problème, assurez-vous que les applets de commande de votre module ne prennent pas de types complexes en tant que paramètres.</span><span class="sxs-lookup"><span data-stu-id="8a10c-171">The way around this issue is to ensure the cmdlets of your module do not take complex types for parameters.</span></span> <span data-ttu-id="8a10c-172">Voici la mauvaise façon de le faire.</span><span class="sxs-lookup"><span data-stu-id="8a10c-172">Here is the wrong way to do it.</span></span>
   
    ```
    function Get-ProcessDescription {
      param (
            [System.Diagnostic.Process] $process
      )
      $process.Description
    }
    ``` 
    <br>
    <span data-ttu-id="8a10c-173">Et voici la bonne façon, en prenant un type primitif pouvant être utilisé en interne par l’applet de commande pour récupérer l’objet complexe et l’utiliser.</span><span class="sxs-lookup"><span data-stu-id="8a10c-173">And here is the right way, taking in a primitive that can be used internally by the cmdlet to grab the complex object and use it.</span></span> <span data-ttu-id="8a10c-174">Comme les applets de commande s’exécutent dans le cadre de PowerShell, et non de Workflow PowerShell, $process devient le type [System.Diagnostic.Process] correct au sein de l’applet de commande.</span><span class="sxs-lookup"><span data-stu-id="8a10c-174">Since cmdlets execute in the context of PowerShell, not PowerShell Workflow, inside the cmdlet $process becomes the correct [System.Diagnostic.Process] type.</span></span>  
   
    ```
    function Get-ProcessDescription {
      param (
            [String] $processName
      )
      $process = Get-Process -Name $processName
   
      $process.Description
    }
    ```
   <br>
   <span data-ttu-id="8a10c-175">Les ressources de connexion dans les Runbooks sont des tables de hachage ; un type complexe. Ces tables de hachage semblent cependant pouvoir être transmises sans problème dans les applets de commande pour leur paramètre -Connection, sans aucune exception de transtypage.</span><span class="sxs-lookup"><span data-stu-id="8a10c-175">Connection assets in runbooks are hashtables, which are a complex type, and yet these hashtables seem to be able to be passed into cmdlets for their –Connection parameter perfectly, with no cast exception.</span></span> <span data-ttu-id="8a10c-176">Techniquement, certains types PowerShell peuvent être désérialisés, et peuvent donc être passés aux applets de commande pour les paramètres acceptant le type non-désérialisé.</span><span class="sxs-lookup"><span data-stu-id="8a10c-176">Technically, some PowerShell types are able to cast properly from their serialized form to their deserialized form, and hence can be passed into cmdlets for parameters accepting the non-deserialized type.</span></span> <span data-ttu-id="8a10c-177">La table de hachage fait partie de ces types.</span><span class="sxs-lookup"><span data-stu-id="8a10c-177">Hashtable is one of these.</span></span> <span data-ttu-id="8a10c-178">Il est possible, pour les types définis par l’auteur d’un module, d’être implémentés d’une façon leur permettant de se désérialiser correctement. Certains compromis doivent cependant être pris en compte.</span><span class="sxs-lookup"><span data-stu-id="8a10c-178">It’s possible for a module author’s defined types to be implemented in a way that they can correctly deserialize as well, but there are some trade-offs to consider.</span></span> <span data-ttu-id="8a10c-179">Le type doit avoir un constructeur par défaut ainsi qu’un PSTypeConverter et toutes ses propriétés doivent être publiques.</span><span class="sxs-lookup"><span data-stu-id="8a10c-179">The type needs to have a default constructor, have all of its properties public, and have a PSTypeConverter.</span></span> <span data-ttu-id="8a10c-180">Toutefois, il est impossible de « réparer » les types prédéfinis que l’auteur du module ne possède pas, d’où la recommandation d’éviter les types complexes pour l’ensemble des paramètres.</span><span class="sxs-lookup"><span data-stu-id="8a10c-180">However, for already-defined types that the module author does not own, there is no way to “fix” them, hence the recommendation to avoid complex types for parameters all together.</span></span> <span data-ttu-id="8a10c-181">Conseil pour la création de Runbook : si, pour une raison quelconque, vos applets de commande doivent accueillir un paramètre de type complexe, ou si vous utilisez un autre module qui requiert un paramètre de type complexe, la solution de contournement dans les Runbooks PowerShell Workflow et les Workflows PowerShell dans un PowerShell local consiste à encapsuler, dans la même activité InlineScript, l’applet de commande qui génère le type complexe et l’applet de commande qui consomme le type complexe.</span><span class="sxs-lookup"><span data-stu-id="8a10c-181">Runbook Authoring tip: If for some reason your cmdlets need to take a complex type parameter, or you are using someone else’s module that requires a complex type parameter, the workaround in PowerShell Workflow runbooks and PowerShell Workflows in local PowerShell, is to wrap the cmdlet that generates the complex type and the cmdlet that consumes the complex type in the same InlineScript activity.</span></span> <span data-ttu-id="8a10c-182">Étant donné qu’InlineScript exécute son contenu sous forme de PowerShell au lieu de Workflow PowerShell, l’applet de commande qui génère le type complexe produit le type correct, pas le type complexe désérialisé.</span><span class="sxs-lookup"><span data-stu-id="8a10c-182">Since InlineScript executes its contents as PowerShell rather than PowerShell Workflow, the cmdlet generating the complex type would produce that correct type, not the deserialized complex type.</span></span>
5. <span data-ttu-id="8a10c-183">Rendez toutes les applets de commande dans le module sans état.</span><span class="sxs-lookup"><span data-stu-id="8a10c-183">Make all cmdlets in the module stateless.</span></span> <span data-ttu-id="8a10c-184">Le Workflow PowerShell exécute chaque applet de commande appelée dans le flux de travail dans une session distincte.</span><span class="sxs-lookup"><span data-stu-id="8a10c-184">PowerShell Workflow runs every cmdlet called in the workflow in a different session.</span></span> <span data-ttu-id="8a10c-185">Cela signifie que toute applet de commande, qui dépend de l’état de la session créée / modifiée par d’autres applets de commande dans le même module, ne fonctionnera pas dans les Runbooks PowerShell Workflow.</span><span class="sxs-lookup"><span data-stu-id="8a10c-185">This means any cmdlets that depend on session state created / modified by other cmdlets in the same module will not work in PowerShell Workflow runbooks.</span></span>  <span data-ttu-id="8a10c-186">Voici un exemple de procédure à ne pas suivre.</span><span class="sxs-lookup"><span data-stu-id="8a10c-186">Here is an example of what not to do.</span></span>
   
    ```
    $globalNum = 0
    function Set-GlobalNum {
       param(
           [int] $num
       )
   
       $globalNum = $num
    }
    function Get-GlobalNumTimesTwo {
       $output = $globalNum * 2
   
       $output
    }
    ```
   <br>
6. <span data-ttu-id="8a10c-187">Le module doit être entièrement contenu dans un package pouvant faire l’objet d’une copie Xcopy.</span><span class="sxs-lookup"><span data-stu-id="8a10c-187">The module should be fully contained in an Xcopy-able package.</span></span> <span data-ttu-id="8a10c-188">Étant donné que les modules Azure Automation sont distribués aux bacs à sable (sandbox) lorsque les Runbooks doivent s’exécuter, ceux-ci doivent fonctionner indépendamment de l’hôte sur lequel ils s’exécutent.</span><span class="sxs-lookup"><span data-stu-id="8a10c-188">Because Azure Automation modules are distributed to the Automation sandboxes when runbooks need to execute, they need to work independently of the host they are running on.</span></span> <span data-ttu-id="8a10c-189">Cela signifie que vous devez être en mesure de compresser le package du module, le déplacer vers un autre hôte comportant une version identique ou plus récente de PowerShell, et le faire fonctionner normalement lorsqu’il est importé dans l’environnement PowerShell de cet hôte.</span><span class="sxs-lookup"><span data-stu-id="8a10c-189">What this means is that you should be able to Zip up the module package, move it to any other host with the same or newer PowerShell version, and have it function as normal when imported into that host’s PowerShell environment.</span></span> <span data-ttu-id="8a10c-190">Pour ce faire, le module ne doit pas dépendre de fichiers se trouvant à l’extérieur du dossier du module (le dossier compressé lors de l’importation dans Azure Automation), ni de seulement un jeu de paramètres unique du Registre sur un hôte, comme celui défini lors de l’installation d’un produit.</span><span class="sxs-lookup"><span data-stu-id="8a10c-190">In order for that to happen, the module should not depend on any files outside the module folder (the folder that gets zipped up when importing into Azure Automation), or on any unique registry settings on a host, such as those set by the install of a product.</span></span> <span data-ttu-id="8a10c-191">Si cette meilleure pratique n’est pas respectée, le module ne sera pas utilisable dans Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="8a10c-191">If this best practice is not followed, the module will not be usable in Azure Automation.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="8a10c-192">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8a10c-192">Next steps</span></span>

* <span data-ttu-id="8a10c-193">Pour une prise en main des Runbooks de workflow PowerShell, consultez [Mon premier Runbook PowerShell Workflow](automation-first-runbook-textual.md)</span><span class="sxs-lookup"><span data-stu-id="8a10c-193">To get started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md)</span></span>
* <span data-ttu-id="8a10c-194">Pour en savoir plus sur la création de modules PowerShell, consultez [Writing a Windows PowerShell Module (Écriture d’un module Windows PowerShell)](https://msdn.microsoft.com/library/dd878310%28v=vs.85%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="8a10c-194">To learn more about creating PowerShell Modules, see [Writing a Windows PowerShell Module](https://msdn.microsoft.com/library/dd878310%28v=vs.85%29.aspx)</span></span>

