---
title: "paramètres de groupe aaaConfigure à l’aide des applets de commande Azure Active Directory | Documents Microsoft"
description: "Comment gérer les paramètres de hello pour les groupes à l’aide des applets de commande Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 9f2090e6-3af4-4f07-bbb2-1d18dae89b73
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: curtand
ms.reviewer: kairaz.contractor
ms.custom: it-pro;
ms.openlocfilehash: 46db49d9dec3eaa41c97ca74c57854189eddc16d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-cmdlets-for-configuring-group-settings"></a><span data-ttu-id="235ca-103">Configuration des paramètres de groupe avec les applets de commande Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="235ca-103">Azure Active Directory cmdlets for configuring group settings</span></span>

> [!IMPORTANT]
> <span data-ttu-id="235ca-104">Ce contenu s’applique uniquement les groupes de 365 tooOffice.</span><span class="sxs-lookup"><span data-stu-id="235ca-104">This content applies only tooOffice 365 groups.</span></span> <span data-ttu-id="235ca-105">Pour plus d’informations sur la façon de définir des groupes de sécurité utilisateurs toocreate tooallow, `Set-MSOLCompanySettings -UsersPermissionToCreateGroupsEnabled $True` comme décrit dans [Set-MSOLCompanySettings](https://docs.microsoft.com/en-us/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0).</span><span class="sxs-lookup"><span data-stu-id="235ca-105">For more information on how tooallow users toocreate Security groups, set `Set-MSOLCompanySettings -UsersPermissionToCreateGroupsEnabled $True` as described in [Set-MSOLCompanySettings](https://docs.microsoft.com/en-us/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0).</span></span> 

<span data-ttu-id="235ca-106">Les paramètres des groupes Office 365 sont configurés à l’aide d’un objet Settings et d’un objet SettingsTemplate.</span><span class="sxs-lookup"><span data-stu-id="235ca-106">Office 365 Groups settings are configured using a Settings object and a SettingsTemplate object.</span></span> <span data-ttu-id="235ca-107">Au départ, vous ne voyez tous les objets de paramètres dans votre annuaire, votre répertoire étant configuré avec des paramètres par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="235ca-107">Initially, you don't see any Settings objects in your directory, because your directory is configured with hello default settings.</span></span> <span data-ttu-id="235ca-108">paramètres par défaut de hello toochange, vous devez créer un nouvel objet de paramètres à l’aide d’un modèle de paramètres.</span><span class="sxs-lookup"><span data-stu-id="235ca-108">toochange hello default settings, you must create a new settings object using a settings template.</span></span> <span data-ttu-id="235ca-109">Les modèles de paramètres sont définis par Microsoft.</span><span class="sxs-lookup"><span data-stu-id="235ca-109">Settings templates are defined by Microsoft.</span></span> <span data-ttu-id="235ca-110">Il existe différents modèles de paramètres.</span><span class="sxs-lookup"><span data-stu-id="235ca-110">There are several different settings templates.</span></span> <span data-ttu-id="235ca-111">paramètres de groupe tooconfigure Office 365 de votre annuaire, vous utilisez modèle hello nommé « Group.Unified ».</span><span class="sxs-lookup"><span data-stu-id="235ca-111">tooconfigure Office 365 group settings for your directory, you use hello template named "Group.Unified".</span></span> <span data-ttu-id="235ca-112">tooconfigure Office 365 les paramètres de groupe sur un seul groupe, utilisez modèle hello nommé « Group.Unified.Guest ».</span><span class="sxs-lookup"><span data-stu-id="235ca-112">tooconfigure Office 365 group settings on a single group, use hello template named "Group.Unified.Guest".</span></span> <span data-ttu-id="235ca-113">Ce modèle est un groupe de toomanage utilisé invité accès tooan Office 365.</span><span class="sxs-lookup"><span data-stu-id="235ca-113">This template is used toomanage guest access tooan Office 365 group.</span></span> 

<span data-ttu-id="235ca-114">applets de commande Hello font partie du module de hello Azure Active Directory PowerShell V2.</span><span class="sxs-lookup"><span data-stu-id="235ca-114">hello cmdlets are part of hello Azure Active Directory PowerShell V2 module.</span></span> <span data-ttu-id="235ca-115">Pour obtenir des instructions toodownload et le module de hello installer sur votre ordinateur, voir l’article de hello [Azure Active Directory PowerShell Version 2](https://docs.microsoft.com/powershell/azuread/).</span><span class="sxs-lookup"><span data-stu-id="235ca-115">For instructions how toodownload and install hello module on your computer, see hello article [Azure Active Directory PowerShell Version 2](https://docs.microsoft.com/powershell/azuread/).</span></span> <span data-ttu-id="235ca-116">Vous pouvez installer la mise en production de la version 2 hello module hello [galerie de PowerShell hello](https://www.powershellgallery.com/packages/AzureAD/).</span><span class="sxs-lookup"><span data-stu-id="235ca-116">You can install hello version 2 release of hello module from [hello PowerShell gallery](https://www.powershellgallery.com/packages/AzureAD/).</span></span>

## <a name="retrieve-a-specific-settings-value"></a><span data-ttu-id="235ca-117">Récupérer une valeur de paramètres spécifique</span><span class="sxs-lookup"><span data-stu-id="235ca-117">Retrieve a specific settings value</span></span>
<span data-ttu-id="235ca-118">Si vous connaissez le nom hello de hello paramètre, vous souhaitez tooretrieve, vous pouvez utiliser hello sous la valeur de paramètres en cours d’applet de commande tooretrieve hello.</span><span class="sxs-lookup"><span data-stu-id="235ca-118">If you know hello name of hello setting you want tooretrieve, you can use hello below cmdlet tooretrieve hello current settings value.</span></span> <span data-ttu-id="235ca-119">Dans cet exemple, nous récupérons valeur hello pour un paramètre nommé « UsageGuidelinesUrl ».</span><span class="sxs-lookup"><span data-stu-id="235ca-119">In this example, we're retrieving hello value for a setting named "UsageGuidelinesUrl."</span></span> <span data-ttu-id="235ca-120">Vous trouverez plus d’informations sur les paramètres de répertoire et leurs noms plus loin dans cet article.</span><span class="sxs-lookup"><span data-stu-id="235ca-120">You can read more about directory settings and their names further down in this article.</span></span>

```powershell
(Get-AzureADDirectorySetting).Values | Where-Object -Property Name -Value UsageGuidelinesUrl -EQ
```

## <a name="create-settings-at-hello-directory-level"></a><span data-ttu-id="235ca-121">Créer des paramètres au niveau du répertoire hello</span><span class="sxs-lookup"><span data-stu-id="235ca-121">Create settings at hello directory level</span></span>
<span data-ttu-id="235ca-122">Les étapes suivantes créent des paramètres au niveau de l’annuaire, qui s’appliquent tooall Office 365 groupes (unifié) dans le répertoire de hello.</span><span class="sxs-lookup"><span data-stu-id="235ca-122">These steps create settings at directory level, which apply tooall Office 365 groups (Unified groups) in hello directory.</span></span>

1. <span data-ttu-id="235ca-123">Bonjour DirectorySettings applets de commande, vous devez spécifier les ID de hello Hello SettingsTemplate vous souhaitez toouse.</span><span class="sxs-lookup"><span data-stu-id="235ca-123">In hello DirectorySettings cmdlets, you must specify hello ID of hello SettingsTemplate you want toouse.</span></span> <span data-ttu-id="235ca-124">Si vous ne connaissez pas cet ID, cette applet de commande renvoie la liste hello de tous les modèles de paramètres :</span><span class="sxs-lookup"><span data-stu-id="235ca-124">If you do not know this ID, this cmdlet returns hello list of all settings templates:</span></span>
  
  ```
  PS C:> Get-AzureADDirectorySettingTemplate
  ```
  <span data-ttu-id="235ca-125">Cet appel d’applet de commande retourne tous les modèles disponibles :</span><span class="sxs-lookup"><span data-stu-id="235ca-125">This cmdlet call returns all templates that are available:</span></span>
  
  ```
  Id                                   DisplayName         Description
  --                                   -----------         -----------
  62375ab9-6b52-47ed-826b-58e47e0e304b Group.Unified       ...
  08d542b9-071f-4e16-94b0-74abb372e3d9 Group.Unified.Guest Settings for a specific Unified Group
  16933506-8a8d-4f0d-ad58-e1db05a5b929 Company.BuiltIn     Setting templates define hello different settings that can be used for hello associ...
  4bc7f740-180e-4586-adb6-38b2e9024e6b Application...
  898f1161-d651-43d1-805c-3b0b388a9fc2 Custom Policy       Settings ...
  5cf42378-d67d-4f36-ba46-e8b86229381d Password Rule       Settings ...
  ```
2. <span data-ttu-id="235ca-126">tooadd une URL de l’indication d’utilisation, vous devez tooget hello SettingsTemplate objet qui définit la valeur d’URL indications hello d’utilisation ; Autrement dit, hello Group.Unified modèle :</span><span class="sxs-lookup"><span data-stu-id="235ca-126">tooadd a usage guideline URL, first you need tooget hello SettingsTemplate object that defines hello usage guideline URL value; that is, hello Group.Unified template:</span></span>
  
  ```
  $Template = Get-AzureADDirectorySettingTemplate -Id 62375ab9-6b52-47ed-826b-58e47e0e304b
  ```
3. <span data-ttu-id="235ca-127">Ensuite, créez un nouvel objet Settings basé sur ce modèle :</span><span class="sxs-lookup"><span data-stu-id="235ca-127">Next, create a new settings object based on that template:</span></span>
  
  ```
  $Setting = $template.CreateDirectorySetting()
  ```  
4. <span data-ttu-id="235ca-128">Puis mettez à jour la valeur hello utilisation indication :</span><span class="sxs-lookup"><span data-stu-id="235ca-128">Then update hello usage guideline value:</span></span>
  
  ```
  $setting["UsageGuidelinesUrl"] = "<https://guideline.com>"
  ```  
5. <span data-ttu-id="235ca-129">Enfin, appliquez les paramètres hello :</span><span class="sxs-lookup"><span data-stu-id="235ca-129">Finally, apply hello settings:</span></span>
  
  ```
  New-AzureADDirectorySetting -DirectorySetting $setting
  ```

<span data-ttu-id="235ca-130">En cas de réussite, hello applet de commande renvoie les ID de hello du nouvel objet de paramètres hello :</span><span class="sxs-lookup"><span data-stu-id="235ca-130">Upon successful completion, hello cmdlet returns hello ID of hello new settings object:</span></span>
  ```
  Id                                   DisplayName TemplateId                           Values
  --                                   ----------- ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323             62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  ```
<span data-ttu-id="235ca-131">Voici les paramètres hello définis dans hello Group.Unified SettingsTemplate.</span><span class="sxs-lookup"><span data-stu-id="235ca-131">Here are hello settings defined in hello Group.Unified SettingsTemplate.</span></span>

| <span data-ttu-id="235ca-132">**Paramètre**</span><span class="sxs-lookup"><span data-stu-id="235ca-132">**Setting**</span></span> | <span data-ttu-id="235ca-133">**Description**</span><span class="sxs-lookup"><span data-stu-id="235ca-133">**Description**</span></span> |
| --- | --- |
|  <ul><li><span data-ttu-id="235ca-134">EnableGroupCreation</span><span class="sxs-lookup"><span data-stu-id="235ca-134">EnableGroupCreation</span></span><li><span data-ttu-id="235ca-135">Type : booléen</span><span class="sxs-lookup"><span data-stu-id="235ca-135">Type: Boolean</span></span><li><span data-ttu-id="235ca-136">Par défaut : True</span><span class="sxs-lookup"><span data-stu-id="235ca-136">Default: True</span></span> |<span data-ttu-id="235ca-137">indicateur Hello indiquant si la création du groupe d’unifié est autorisée dans le répertoire de hello.</span><span class="sxs-lookup"><span data-stu-id="235ca-137">hello flag indicating whether Unified Group creation is allowed in hello directory.</span></span> |
|  <ul><li><span data-ttu-id="235ca-138">GroupCreationAllowedGroupId</span><span class="sxs-lookup"><span data-stu-id="235ca-138">GroupCreationAllowedGroupId</span></span><li><span data-ttu-id="235ca-139">Type : string</span><span class="sxs-lookup"><span data-stu-id="235ca-139">Type: String</span></span><li><span data-ttu-id="235ca-140">Valeur par défaut : “”</span><span class="sxs-lookup"><span data-stu-id="235ca-140">Default: “”</span></span> |<span data-ttu-id="235ca-141">GUID du groupe de sécurité hello pour le hello les membres sont autorisés à toocreate Unified Groups même lorsque EnableGroupCreation == false.</span><span class="sxs-lookup"><span data-stu-id="235ca-141">GUID of hello security group for which hello members are allowed toocreate Unified Groups even when EnableGroupCreation == false.</span></span> |
|  <ul><li><span data-ttu-id="235ca-142">UsageGuidelinesUrl</span><span class="sxs-lookup"><span data-stu-id="235ca-142">UsageGuidelinesUrl</span></span><li><span data-ttu-id="235ca-143">Type : string</span><span class="sxs-lookup"><span data-stu-id="235ca-143">Type: String</span></span><li><span data-ttu-id="235ca-144">Valeur par défaut : “”</span><span class="sxs-lookup"><span data-stu-id="235ca-144">Default: “”</span></span> |<span data-ttu-id="235ca-145">Un lien toohello consignes d’utilisation de groupe.</span><span class="sxs-lookup"><span data-stu-id="235ca-145">A link toohello Group Usage Guidelines.</span></span> |
|  <ul><li><span data-ttu-id="235ca-146">ClassificationDescriptions</span><span class="sxs-lookup"><span data-stu-id="235ca-146">ClassificationDescriptions</span></span><li><span data-ttu-id="235ca-147">Type : string</span><span class="sxs-lookup"><span data-stu-id="235ca-147">Type: String</span></span><li><span data-ttu-id="235ca-148">Valeur par défaut : “”</span><span class="sxs-lookup"><span data-stu-id="235ca-148">Default: “”</span></span> | <span data-ttu-id="235ca-149">Liste séparée par des virgules des descriptions de classification.</span><span class="sxs-lookup"><span data-stu-id="235ca-149">A comma-delimited list of classification descriptions.</span></span> |
|  <ul><li><span data-ttu-id="235ca-150">DefaultClassification</span><span class="sxs-lookup"><span data-stu-id="235ca-150">DefaultClassification</span></span><li><span data-ttu-id="235ca-151">Type : string</span><span class="sxs-lookup"><span data-stu-id="235ca-151">Type: String</span></span><li><span data-ttu-id="235ca-152">Valeur par défaut : “”</span><span class="sxs-lookup"><span data-stu-id="235ca-152">Default: “”</span></span> | <span data-ttu-id="235ca-153">classification de Hello est toobe utilisé en tant que classement par défaut de hello pour un groupe, si aucun n’a été spécifié.</span><span class="sxs-lookup"><span data-stu-id="235ca-153">hello classification that is toobe used as hello default classification for a group if none was specified.</span></span>|
|  <ul><li><span data-ttu-id="235ca-154">PrefixSuffixNamingRequirement</span><span class="sxs-lookup"><span data-stu-id="235ca-154">PrefixSuffixNamingRequirement</span></span><li><span data-ttu-id="235ca-155">Type : string</span><span class="sxs-lookup"><span data-stu-id="235ca-155">Type: String</span></span><li><span data-ttu-id="235ca-156">Valeur par défaut : “”</span><span class="sxs-lookup"><span data-stu-id="235ca-156">Default: “”</span></span> |<span data-ttu-id="235ca-157">Pas encore implémenté</span><span class="sxs-lookup"><span data-stu-id="235ca-157">Not implemented yet</span></span>
|  <ul><li><span data-ttu-id="235ca-158">AllowGuestsToBeGroupOwner</span><span class="sxs-lookup"><span data-stu-id="235ca-158">AllowGuestsToBeGroupOwner</span></span><li><span data-ttu-id="235ca-159">Type : booléen</span><span class="sxs-lookup"><span data-stu-id="235ca-159">Type: Boolean</span></span><li><span data-ttu-id="235ca-160">Par défaut : False</span><span class="sxs-lookup"><span data-stu-id="235ca-160">Default: False</span></span> | <span data-ttu-id="235ca-161">Valeur booléenne indiquant si un utilisateur invité peut être ou non un propriétaire de groupes.</span><span class="sxs-lookup"><span data-stu-id="235ca-161">Boolean indicating whether or not a guest user can be an owner of groups.</span></span> |
|  <ul><li><span data-ttu-id="235ca-162">AllowGuestsToAccessGroups</span><span class="sxs-lookup"><span data-stu-id="235ca-162">AllowGuestsToAccessGroups</span></span><li><span data-ttu-id="235ca-163">Type : booléen</span><span class="sxs-lookup"><span data-stu-id="235ca-163">Type: Boolean</span></span><li><span data-ttu-id="235ca-164">Par défaut : True</span><span class="sxs-lookup"><span data-stu-id="235ca-164">Default: True</span></span> | <span data-ttu-id="235ca-165">Valeur booléenne indiquant si un utilisateur invité peut avoir le contenu des groupes d’accès tooUnified.</span><span class="sxs-lookup"><span data-stu-id="235ca-165">Boolean indicating whether or not a guest user can have access tooUnified groups' content.</span></span> |
|  <ul><li><span data-ttu-id="235ca-166">GuestUsageGuidelinesUrl</span><span class="sxs-lookup"><span data-stu-id="235ca-166">GuestUsageGuidelinesUrl</span></span><li><span data-ttu-id="235ca-167">Type : string</span><span class="sxs-lookup"><span data-stu-id="235ca-167">Type: String</span></span><li><span data-ttu-id="235ca-168">Valeur par défaut : “”</span><span class="sxs-lookup"><span data-stu-id="235ca-168">Default: “”</span></span> | <span data-ttu-id="235ca-169">url de Hello une instructions d’utilisation de lien toohello invité.</span><span class="sxs-lookup"><span data-stu-id="235ca-169">hello url of a link toohello guest usage guidelines.</span></span> |
|  <ul><li><span data-ttu-id="235ca-170">AllowToAddGuests</span><span class="sxs-lookup"><span data-stu-id="235ca-170">AllowToAddGuests</span></span><li><span data-ttu-id="235ca-171">Type : booléen</span><span class="sxs-lookup"><span data-stu-id="235ca-171">Type: Boolean</span></span><li><span data-ttu-id="235ca-172">Par défaut : True</span><span class="sxs-lookup"><span data-stu-id="235ca-172">Default: True</span></span> | <span data-ttu-id="235ca-173">Une valeur booléenne indiquant si est autorisée tooadd ou non invités toothis active.</span><span class="sxs-lookup"><span data-stu-id="235ca-173">A boolean indicating whether or not is allowed tooadd guests toothis directory.</span></span>|
|  <ul><li><span data-ttu-id="235ca-174">ClassificationList</span><span class="sxs-lookup"><span data-stu-id="235ca-174">ClassificationList</span></span><li><span data-ttu-id="235ca-175">Type : string</span><span class="sxs-lookup"><span data-stu-id="235ca-175">Type: String</span></span><li><span data-ttu-id="235ca-176">Valeur par défaut : “”</span><span class="sxs-lookup"><span data-stu-id="235ca-176">Default: “”</span></span> |<span data-ttu-id="235ca-177">Une liste délimitée par des virgules des valeurs de classification valides qui peuvent être appliqués tooUnified des groupes.</span><span class="sxs-lookup"><span data-stu-id="235ca-177">A comma-delimited list of valid classification values that can be applied tooUnified Groups.</span></span> |
|  <ul><li><span data-ttu-id="235ca-178">EnableGroupCreation</span><span class="sxs-lookup"><span data-stu-id="235ca-178">EnableGroupCreation</span></span><li><span data-ttu-id="235ca-179">Type : booléen</span><span class="sxs-lookup"><span data-stu-id="235ca-179">Type: Boolean</span></span><li><span data-ttu-id="235ca-180">Par défaut : True</span><span class="sxs-lookup"><span data-stu-id="235ca-180">Default: True</span></span> | <span data-ttu-id="235ca-181">Valeur booléenne indiquant si les utilisateurs non-administrateurs peuvent ou non créer des groupes unifiés.</span><span class="sxs-lookup"><span data-stu-id="235ca-181">A boolean indicating whether or not non-admin users can create new Unified groups.</span></span> |


## <a name="read-settings-at-hello-directory-level"></a><span data-ttu-id="235ca-182">Lire les paramètres au niveau du répertoire hello</span><span class="sxs-lookup"><span data-stu-id="235ca-182">Read settings at hello directory level</span></span>
<span data-ttu-id="235ca-183">Ces étapes de lire les paramètres au niveau de l’annuaire, qui s’appliquent à des groupes de Office tooall dans le répertoire de hello.</span><span class="sxs-lookup"><span data-stu-id="235ca-183">These steps read settings at directory level, which apply tooall Office groups in hello directory.</span></span>

1. <span data-ttu-id="235ca-184">Lisez tous les paramètres du répertoire existant :</span><span class="sxs-lookup"><span data-stu-id="235ca-184">Read all existing directory settings:</span></span>
  ```
  Get-AzureADDirectorySetting -All $True
  ```
  <span data-ttu-id="235ca-185">Cette applet de commande retourne une liste de tous les paramètres du répertoire :</span><span class="sxs-lookup"><span data-stu-id="235ca-185">This cmdlet returns a list of all directory settings:</span></span>
  ```
  Id                                   DisplayName   TemplateId                           Values
  --                                   -----------   ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323 Group.Unified 62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  ```

2. <span data-ttu-id="235ca-186">Lisez tous les paramètres d’un groupe spécifique :</span><span class="sxs-lookup"><span data-stu-id="235ca-186">Read all settings for a specific group:</span></span>
  ```
  Get-AzureADObjectSetting -TargetObjectId ab6a3887-776a-4db7-9da4-ea2b0d63c504 -TargetType Groups
  ```

3. <span data-ttu-id="235ca-187">Lisez toutes les valeurs de paramètres de répertoire d’un objet settings de répertoire spécifique, à l’aide du GUID de l’ID de paramètres :</span><span class="sxs-lookup"><span data-stu-id="235ca-187">Read all directory settings values of a specific directory settings object, using Settings Id GUID:</span></span>
  ```
  (Get-AzureADDirectorySetting -Id c391b57d-5783-4c53-9236-cefb5c6ef323).values
  ```
  <span data-ttu-id="235ca-188">Cette applet de commande renvoie les noms hello et les valeurs dans cet objet de paramètres pour ce groupe spécifique :</span><span class="sxs-lookup"><span data-stu-id="235ca-188">This cmdlet returns hello names and values in this settings object for this specific group:</span></span>
  ```
  Name                          Value
  ----                          -----
  ClassificationDescriptions
  DefaultClassification
  PrefixSuffixNamingRequirement
  AllowGuestsToBeGroupOwner     False 
  AllowGuestsToAccessGroups     True
  GuestUsageGuidelinesUrl
  GroupCreationAllowedGroupId
  AllowToAddGuests              True
  UsageGuidelinesUrl            <https://guideline.com>
  ClassificationList
  EnableGroupCreation           True
  ```

## <a name="update-settings-for-a-specific-group"></a><span data-ttu-id="235ca-189">Mettre à jour les paramètres d’un groupe spécifique</span><span class="sxs-lookup"><span data-stu-id="235ca-189">Update settings for a specific group</span></span>

1. <span data-ttu-id="235ca-190">Recherchez le modèle de paramètres de hello nommé « Groups.Unified.Guest »</span><span class="sxs-lookup"><span data-stu-id="235ca-190">Search for hello settings template named "Groups.Unified.Guest"</span></span>
  ```
  Get-AzureADDirectorySettingTemplate
  
  Id                                   DisplayName            Description
  --                                   -----------            -----------
  62375ab9-6b52-47ed-826b-58e47e0e304b Group.Unified          ...
  08d542b9-071f-4e16-94b0-74abb372e3d9 Group.Unified.Guest    Settings for a specific Unified Group
  4bc7f740-180e-4586-adb6-38b2e9024e6b Application            ...
  898f1161-d651-43d1-805c-3b0b388a9fc2 Custom Policy Settings ...
  5cf42378-d67d-4f36-ba46-e8b86229381d Password Rule Settings ...
  ```
2. <span data-ttu-id="235ca-191">Récupérer l’objet de modèle hello pour le modèle de Groups.Unified.Guest hello :</span><span class="sxs-lookup"><span data-stu-id="235ca-191">Retrieve hello template object for hello Groups.Unified.Guest template:</span></span>
  ```
  $Template = Get-AzureADDirectorySettingTemplate -Id 08d542b9-071f-4e16-94b0-74abb372e3d9
  ```
3. <span data-ttu-id="235ca-192">Créer un nouvel objet de paramètres de modèle de hello :</span><span class="sxs-lookup"><span data-stu-id="235ca-192">Create a new settings object from hello template:</span></span>
  ```
  $Setting = $Template.CreateDirectorySetting()
  ```

4. <span data-ttu-id="235ca-193">Définir la valeur hello toohello requis :</span><span class="sxs-lookup"><span data-stu-id="235ca-193">Set hello setting toohello required value:</span></span>
  ```
  $Setting["AllowToAddGuests"]=$False
  ```
5. <span data-ttu-id="235ca-194">Créer nouveau paramètre de hello pour les groupes requis hello dans le répertoire de hello :</span><span class="sxs-lookup"><span data-stu-id="235ca-194">Create hello new setting for hello required group in hello directory:</span></span>
  ```
  New-AzureADObjectSetting -TargetType Groups -TargetObjectId ab6a3887-776a-4db7-9da4-ea2b0d63c504 -DirectorySetting $Setting
  
  Id                                   DisplayName TemplateId                           Values
  --                                   ----------- ----------                           ------
  25651479-a26e-4181-afce-ce24111b2cb5             08d542b9-071f-4e16-94b0-74abb372e3d9 {class SettingValue {...
  ```

## <a name="update-settings-at-hello-directory-level"></a><span data-ttu-id="235ca-195">Paramètres de mise à jour au niveau du répertoire hello</span><span class="sxs-lookup"><span data-stu-id="235ca-195">Update settings at hello directory level</span></span>

<span data-ttu-id="235ca-196">Ces étapes de mettre à jour les paramètres au niveau de l’annuaire, qui s’appliquent les groupes d’unifiée tooall dans le répertoire de hello.</span><span class="sxs-lookup"><span data-stu-id="235ca-196">These steps update settings at directory level, which apply tooall Unified groups in hello directory.</span></span> <span data-ttu-id="235ca-197">Ces exemples supposent qu’un objet Settings existe déjà dans votre répertoire.</span><span class="sxs-lookup"><span data-stu-id="235ca-197">These examples assume there is already a Settings object in your directory.</span></span>

1. <span data-ttu-id="235ca-198">Rechercher un objet de paramètres hello existant :</span><span class="sxs-lookup"><span data-stu-id="235ca-198">Find hello existing Settings object:</span></span>
  ```
  Get-AzureADDirectorySetting | Where-object -Property Displayname -Value "Group.Unified" -EQ
  
  Id                                   DisplayName   TemplateId                           Values
  --                                   -----------   ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323 Group.Unified 62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  
  $setting = Get-AzureADDirectorySetting –Id c391b57d-5783-4c53-9236-cefb5c6ef323
  ```
2. <span data-ttu-id="235ca-199">Mettre à jour la valeur de hello :</span><span class="sxs-lookup"><span data-stu-id="235ca-199">Update hello value:</span></span>
  
  ```
  $Setting["AllowToAddGuests"] = "false"
  ```
3. <span data-ttu-id="235ca-200">Mise à jour du paramètre de hello :</span><span class="sxs-lookup"><span data-stu-id="235ca-200">Update hello setting:</span></span>
  
  ```
  Set-AzureADDirectorySetting -Id c391b57d-5783-4c53-9236-cefb5c6ef323 -DirectorySetting $Setting
  ```

## <a name="remove-settings-at-hello-directory-level"></a><span data-ttu-id="235ca-201">Supprimer les paramètres au niveau du répertoire hello</span><span class="sxs-lookup"><span data-stu-id="235ca-201">Remove settings at hello directory level</span></span>
<span data-ttu-id="235ca-202">Cette étape supprime les paramètres au niveau de l’annuaire, qui s’appliquent à des groupes de Office tooall dans le répertoire de hello.</span><span class="sxs-lookup"><span data-stu-id="235ca-202">This step removes settings at directory level, which apply tooall Office groups in hello directory.</span></span>
  ```
  Remove-AzureADDirectorySetting –Id c391b57d-5783-4c53-9236-cefb5c6ef323c
  ```

## <a name="cmdlet-syntax-reference"></a><span data-ttu-id="235ca-203">Informations de référence sur la syntaxe des applets de commande</span><span class="sxs-lookup"><span data-stu-id="235ca-203">Cmdlet syntax reference</span></span>
<span data-ttu-id="235ca-204">Vous trouverez plus d’informations sur Azure Active Directory PowerShell dans la page dédiée aux [applets de commande Azure Active Directory](/powershell/azure/install-adv2?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="235ca-204">You can find more Azure Active Directory PowerShell documentation at [Azure Active Directory Cmdlets](/powershell/azure/install-adv2?view=azureadps-2.0).</span></span>

## <a name="additional-reading"></a><span data-ttu-id="235ca-205">Documentation supplémentaire</span><span class="sxs-lookup"><span data-stu-id="235ca-205">Additional reading</span></span>

* [<span data-ttu-id="235ca-206">La gestion des accès tooresources avec les groupes Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="235ca-206">Managing access tooresources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="235ca-207">Intégration de vos identités locales avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="235ca-207">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
