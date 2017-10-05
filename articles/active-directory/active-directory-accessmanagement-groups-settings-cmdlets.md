---
title: "Configurer des paramètres de groupe avec les applets de commande Azure Active Directory | Microsoft Docs"
description: "Comment gérer les paramètres des groupes à l’aide des applets de commande Azure Active Directory ?"
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
ms.openlocfilehash: 0d89f12955b90c7e1a8301b7c3a1a92e7f62d085
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-cmdlets-for-configuring-group-settings"></a><span data-ttu-id="a683d-103">Configuration des paramètres de groupe avec les applets de commande Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a683d-103">Azure Active Directory cmdlets for configuring group settings</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a683d-104">Ce contenu s’applique uniquement aux groupes Office 365.</span><span class="sxs-lookup"><span data-stu-id="a683d-104">This content applies only to Office 365 groups.</span></span> <span data-ttu-id="a683d-105">Pour plus d’informations sur comment permettre aux utilisateurs de créer des groupes de sécurité, définissez `Set-MSOLCompanySettings -UsersPermissionToCreateGroupsEnabled $True` tel que décrit dans [Set-MSOLCompanySettings](https://docs.microsoft.com/en-us/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0).</span><span class="sxs-lookup"><span data-stu-id="a683d-105">For more information on how to allow users to create Security groups, set `Set-MSOLCompanySettings -UsersPermissionToCreateGroupsEnabled $True` as described in [Set-MSOLCompanySettings](https://docs.microsoft.com/en-us/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0).</span></span> 

<span data-ttu-id="a683d-106">Les paramètres des groupes Office 365 sont configurés à l’aide d’un objet Settings et d’un objet SettingsTemplate.</span><span class="sxs-lookup"><span data-stu-id="a683d-106">Office 365 Groups settings are configured using a Settings object and a SettingsTemplate object.</span></span> <span data-ttu-id="a683d-107">Au départ, vous ne voyez aucun objet Paramètres dans votre répertoire, car votre répertoire est configuré avec les paramètres par défaut.</span><span class="sxs-lookup"><span data-stu-id="a683d-107">Initially, you don't see any Settings objects in your directory, because your directory is configured with the default settings.</span></span> <span data-ttu-id="a683d-108">Pour changer les paramètres par défaut, vous devez créer un objet de paramètres en utilisant un modèle de paramètres.</span><span class="sxs-lookup"><span data-stu-id="a683d-108">To change the default settings, you must create a new settings object using a settings template.</span></span> <span data-ttu-id="a683d-109">Les modèles de paramètres sont définis par Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a683d-109">Settings templates are defined by Microsoft.</span></span> <span data-ttu-id="a683d-110">Il existe différents modèles de paramètres.</span><span class="sxs-lookup"><span data-stu-id="a683d-110">There are several different settings templates.</span></span> <span data-ttu-id="a683d-111">Pour configurer les paramètres du groupe Office 365 pour votre répertoire, utiliserez le modèle nommé « Group.Unified ».</span><span class="sxs-lookup"><span data-stu-id="a683d-111">To configure Office 365 group settings for your directory, you use the template named "Group.Unified".</span></span> <span data-ttu-id="a683d-112">Pour configurer les paramètres du groupe Office 365 sur un seul groupe, utilisez le modèle nommé « Group.Unified.Guest ».</span><span class="sxs-lookup"><span data-stu-id="a683d-112">To configure Office 365 group settings on a single group, use the template named "Group.Unified.Guest".</span></span> <span data-ttu-id="a683d-113">Ce modèle est utilisé pour gérer l’accès invité à un groupe Office 365.</span><span class="sxs-lookup"><span data-stu-id="a683d-113">This template is used to manage guest access to an Office 365 group.</span></span> 

<span data-ttu-id="a683d-114">Les applets de commande font partie du module Azure Active Directory PowerShell V2.</span><span class="sxs-lookup"><span data-stu-id="a683d-114">The cmdlets are part of the Azure Active Directory PowerShell V2 module.</span></span> <span data-ttu-id="a683d-115">Pour obtenir des instructions sur le téléchargement et l’installation du module sur votre ordinateur, reportez-vous à l’article [Azure Active Directory PowerShell Version 2](https://docs.microsoft.com/powershell/azuread/).</span><span class="sxs-lookup"><span data-stu-id="a683d-115">For instructions how to download and install the module on your computer, see the article [Azure Active Directory PowerShell Version 2](https://docs.microsoft.com/powershell/azuread/).</span></span> <span data-ttu-id="a683d-116">Vous pouvez installer la version 2 du module depuis [la galerie PowerShell](https://www.powershellgallery.com/packages/AzureAD/).</span><span class="sxs-lookup"><span data-stu-id="a683d-116">You can install the version 2 release of the module from [the PowerShell gallery](https://www.powershellgallery.com/packages/AzureAD/).</span></span>

## <a name="retrieve-a-specific-settings-value"></a><span data-ttu-id="a683d-117">Récupérer une valeur de paramètres spécifique</span><span class="sxs-lookup"><span data-stu-id="a683d-117">Retrieve a specific settings value</span></span>
<span data-ttu-id="a683d-118">Si vous connaissez le nom du paramètre à récupérer, vous pouvez utiliser l’applet de commande ci-dessous pour récupérer la valeur des paramètres actuelle.</span><span class="sxs-lookup"><span data-stu-id="a683d-118">If you know the name of the setting you want to retrieve, you can use the below cmdlet to retrieve the current settings value.</span></span> <span data-ttu-id="a683d-119">Dans cet exemple, nous récupérons la valeur d’un paramètre nommé « UsageGuidelinesUrl ».</span><span class="sxs-lookup"><span data-stu-id="a683d-119">In this example, we're retrieving the value for a setting named "UsageGuidelinesUrl."</span></span> <span data-ttu-id="a683d-120">Vous trouverez plus d’informations sur les paramètres de répertoire et leurs noms plus loin dans cet article.</span><span class="sxs-lookup"><span data-stu-id="a683d-120">You can read more about directory settings and their names further down in this article.</span></span>

```powershell
(Get-AzureADDirectorySetting).Values | Where-Object -Property Name -Value UsageGuidelinesUrl -EQ
```

## <a name="create-settings-at-the-directory-level"></a><span data-ttu-id="a683d-121">Créer des paramètres au niveau du répertoire</span><span class="sxs-lookup"><span data-stu-id="a683d-121">Create settings at the directory level</span></span>
<span data-ttu-id="a683d-122">Les étapes suivantes permettent de créer des paramètres au niveau du répertoire qui s’appliquent à tous les groupes Office 365 (groupes unifiés) du répertoire.</span><span class="sxs-lookup"><span data-stu-id="a683d-122">These steps create settings at directory level, which apply to all Office 365 groups (Unified groups) in the directory.</span></span>

1. <span data-ttu-id="a683d-123">Dans les applets de commande DirectorySettings, vous devez spécifier l’ID du modèle SettingsTemplate que vous voulez utiliser.</span><span class="sxs-lookup"><span data-stu-id="a683d-123">In the DirectorySettings cmdlets, you must specify the ID of the SettingsTemplate you want to use.</span></span> <span data-ttu-id="a683d-124">Si vous ne connaissez pas cet ID, cette applet de commande renvoie la liste de tous les modèles de paramètres :</span><span class="sxs-lookup"><span data-stu-id="a683d-124">If you do not know this ID, this cmdlet returns the list of all settings templates:</span></span>
  
  ```
  PS C:> Get-AzureADDirectorySettingTemplate
  ```
  <span data-ttu-id="a683d-125">Cet appel d’applet de commande retourne tous les modèles disponibles :</span><span class="sxs-lookup"><span data-stu-id="a683d-125">This cmdlet call returns all templates that are available:</span></span>
  
  ```
  Id                                   DisplayName         Description
  --                                   -----------         -----------
  62375ab9-6b52-47ed-826b-58e47e0e304b Group.Unified       ...
  08d542b9-071f-4e16-94b0-74abb372e3d9 Group.Unified.Guest Settings for a specific Unified Group
  16933506-8a8d-4f0d-ad58-e1db05a5b929 Company.BuiltIn     Setting templates define the different settings that can be used for the associ...
  4bc7f740-180e-4586-adb6-38b2e9024e6b Application...
  898f1161-d651-43d1-805c-3b0b388a9fc2 Custom Policy       Settings ...
  5cf42378-d67d-4f36-ba46-e8b86229381d Password Rule       Settings ...
  ```
2. <span data-ttu-id="a683d-126">Pour ajouter une URL d’instructions d’utilisation, vous devez d’abord obtenir l’objet SettingsTemplate qui définit la valeur de l’URL d’instructions d’utilisation ; autrement dit, le modèle Group.Unified :</span><span class="sxs-lookup"><span data-stu-id="a683d-126">To add a usage guideline URL, first you need to get the SettingsTemplate object that defines the usage guideline URL value; that is, the Group.Unified template:</span></span>
  
  ```
  $Template = Get-AzureADDirectorySettingTemplate -Id 62375ab9-6b52-47ed-826b-58e47e0e304b
  ```
3. <span data-ttu-id="a683d-127">Ensuite, créez un nouvel objet Settings basé sur ce modèle :</span><span class="sxs-lookup"><span data-stu-id="a683d-127">Next, create a new settings object based on that template:</span></span>
  
  ```
  $Setting = $template.CreateDirectorySetting()
  ```  
4. <span data-ttu-id="a683d-128">Puis mettez à jour la valeur des instructions d’utilisation :</span><span class="sxs-lookup"><span data-stu-id="a683d-128">Then update the usage guideline value:</span></span>
  
  ```
  $setting["UsageGuidelinesUrl"] = "<https://guideline.com>"
  ```  
5. <span data-ttu-id="a683d-129">Enfin, appliquez les paramètres :</span><span class="sxs-lookup"><span data-stu-id="a683d-129">Finally, apply the settings:</span></span>
  
  ```
  New-AzureADDirectorySetting -DirectorySetting $setting
  ```

<span data-ttu-id="a683d-130">Une fois terminée, l’applet de commande retourne l’ID du nouvel objet de paramètres :</span><span class="sxs-lookup"><span data-stu-id="a683d-130">Upon successful completion, the cmdlet returns the ID of the new settings object:</span></span>
  ```
  Id                                   DisplayName TemplateId                           Values
  --                                   ----------- ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323             62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  ```
<span data-ttu-id="a683d-131">Voici les paramètres définis dans l’objet SettingsTemplate Group.Unified.</span><span class="sxs-lookup"><span data-stu-id="a683d-131">Here are the settings defined in the Group.Unified SettingsTemplate.</span></span>

| <span data-ttu-id="a683d-132">**Paramètre**</span><span class="sxs-lookup"><span data-stu-id="a683d-132">**Setting**</span></span> | <span data-ttu-id="a683d-133">**Description**</span><span class="sxs-lookup"><span data-stu-id="a683d-133">**Description**</span></span> |
| --- | --- |
|  <ul><li><span data-ttu-id="a683d-134">EnableGroupCreation</span><span class="sxs-lookup"><span data-stu-id="a683d-134">EnableGroupCreation</span></span><li><span data-ttu-id="a683d-135">Type : booléen</span><span class="sxs-lookup"><span data-stu-id="a683d-135">Type: Boolean</span></span><li><span data-ttu-id="a683d-136">Par défaut : True</span><span class="sxs-lookup"><span data-stu-id="a683d-136">Default: True</span></span> |<span data-ttu-id="a683d-137">Indicateur spécifiant si la création de groupes unifiés est autorisée dans le répertoire.</span><span class="sxs-lookup"><span data-stu-id="a683d-137">The flag indicating whether Unified Group creation is allowed in the directory.</span></span> |
|  <ul><li><span data-ttu-id="a683d-138">GroupCreationAllowedGroupId</span><span class="sxs-lookup"><span data-stu-id="a683d-138">GroupCreationAllowedGroupId</span></span><li><span data-ttu-id="a683d-139">Type : string</span><span class="sxs-lookup"><span data-stu-id="a683d-139">Type: String</span></span><li><span data-ttu-id="a683d-140">Valeur par défaut : “”</span><span class="sxs-lookup"><span data-stu-id="a683d-140">Default: “”</span></span> |<span data-ttu-id="a683d-141">GUID du groupe de sécurité pour lequel les membres sont autorisés à créer des groupes unifiés même lorsque EnableGroupCreation == false.</span><span class="sxs-lookup"><span data-stu-id="a683d-141">GUID of the security group for which the members are allowed to create Unified Groups even when EnableGroupCreation == false.</span></span> |
|  <ul><li><span data-ttu-id="a683d-142">UsageGuidelinesUrl</span><span class="sxs-lookup"><span data-stu-id="a683d-142">UsageGuidelinesUrl</span></span><li><span data-ttu-id="a683d-143">Type : string</span><span class="sxs-lookup"><span data-stu-id="a683d-143">Type: String</span></span><li><span data-ttu-id="a683d-144">Valeur par défaut : “”</span><span class="sxs-lookup"><span data-stu-id="a683d-144">Default: “”</span></span> |<span data-ttu-id="a683d-145">Lien vers les instructions d’utilisation du groupe.</span><span class="sxs-lookup"><span data-stu-id="a683d-145">A link to the Group Usage Guidelines.</span></span> |
|  <ul><li><span data-ttu-id="a683d-146">ClassificationDescriptions</span><span class="sxs-lookup"><span data-stu-id="a683d-146">ClassificationDescriptions</span></span><li><span data-ttu-id="a683d-147">Type : string</span><span class="sxs-lookup"><span data-stu-id="a683d-147">Type: String</span></span><li><span data-ttu-id="a683d-148">Valeur par défaut : “”</span><span class="sxs-lookup"><span data-stu-id="a683d-148">Default: “”</span></span> | <span data-ttu-id="a683d-149">Liste séparée par des virgules des descriptions de classification.</span><span class="sxs-lookup"><span data-stu-id="a683d-149">A comma-delimited list of classification descriptions.</span></span> |
|  <ul><li><span data-ttu-id="a683d-150">DefaultClassification</span><span class="sxs-lookup"><span data-stu-id="a683d-150">DefaultClassification</span></span><li><span data-ttu-id="a683d-151">Type : string</span><span class="sxs-lookup"><span data-stu-id="a683d-151">Type: String</span></span><li><span data-ttu-id="a683d-152">Valeur par défaut : “”</span><span class="sxs-lookup"><span data-stu-id="a683d-152">Default: “”</span></span> | <span data-ttu-id="a683d-153">Classification qui doit être utilisée en tant que classement par défaut pour un groupe si aucune classification n’a été spécifiée.</span><span class="sxs-lookup"><span data-stu-id="a683d-153">The classification that is to be used as the default classification for a group if none was specified.</span></span>|
|  <ul><li><span data-ttu-id="a683d-154">PrefixSuffixNamingRequirement</span><span class="sxs-lookup"><span data-stu-id="a683d-154">PrefixSuffixNamingRequirement</span></span><li><span data-ttu-id="a683d-155">Type : string</span><span class="sxs-lookup"><span data-stu-id="a683d-155">Type: String</span></span><li><span data-ttu-id="a683d-156">Valeur par défaut : “”</span><span class="sxs-lookup"><span data-stu-id="a683d-156">Default: “”</span></span> |<span data-ttu-id="a683d-157">Pas encore implémenté</span><span class="sxs-lookup"><span data-stu-id="a683d-157">Not implemented yet</span></span>
|  <ul><li><span data-ttu-id="a683d-158">AllowGuestsToBeGroupOwner</span><span class="sxs-lookup"><span data-stu-id="a683d-158">AllowGuestsToBeGroupOwner</span></span><li><span data-ttu-id="a683d-159">Type : booléen</span><span class="sxs-lookup"><span data-stu-id="a683d-159">Type: Boolean</span></span><li><span data-ttu-id="a683d-160">Par défaut : False</span><span class="sxs-lookup"><span data-stu-id="a683d-160">Default: False</span></span> | <span data-ttu-id="a683d-161">Valeur booléenne indiquant si un utilisateur invité peut être ou non un propriétaire de groupes.</span><span class="sxs-lookup"><span data-stu-id="a683d-161">Boolean indicating whether or not a guest user can be an owner of groups.</span></span> |
|  <ul><li><span data-ttu-id="a683d-162">AllowGuestsToAccessGroups</span><span class="sxs-lookup"><span data-stu-id="a683d-162">AllowGuestsToAccessGroups</span></span><li><span data-ttu-id="a683d-163">Type : booléen</span><span class="sxs-lookup"><span data-stu-id="a683d-163">Type: Boolean</span></span><li><span data-ttu-id="a683d-164">Par défaut : True</span><span class="sxs-lookup"><span data-stu-id="a683d-164">Default: True</span></span> | <span data-ttu-id="a683d-165">Valeur booléenne indiquant si un utilisateur invité peut avoir ou non accès au contenu des groupes unifiés.</span><span class="sxs-lookup"><span data-stu-id="a683d-165">Boolean indicating whether or not a guest user can have access to Unified groups' content.</span></span> |
|  <ul><li><span data-ttu-id="a683d-166">GuestUsageGuidelinesUrl</span><span class="sxs-lookup"><span data-stu-id="a683d-166">GuestUsageGuidelinesUrl</span></span><li><span data-ttu-id="a683d-167">Type : string</span><span class="sxs-lookup"><span data-stu-id="a683d-167">Type: String</span></span><li><span data-ttu-id="a683d-168">Valeur par défaut : “”</span><span class="sxs-lookup"><span data-stu-id="a683d-168">Default: “”</span></span> | <span data-ttu-id="a683d-169">URL d’un lien vers les instructions d’utilisation de l’invité.</span><span class="sxs-lookup"><span data-stu-id="a683d-169">The url of a link to the guest usage guidelines.</span></span> |
|  <ul><li><span data-ttu-id="a683d-170">AllowToAddGuests</span><span class="sxs-lookup"><span data-stu-id="a683d-170">AllowToAddGuests</span></span><li><span data-ttu-id="a683d-171">Type : booléen</span><span class="sxs-lookup"><span data-stu-id="a683d-171">Type: Boolean</span></span><li><span data-ttu-id="a683d-172">Par défaut : True</span><span class="sxs-lookup"><span data-stu-id="a683d-172">Default: True</span></span> | <span data-ttu-id="a683d-173">Une valeur booléenne indiquant si l’utilisateur est autorisé ou non à ajouter des invités à ce répertoire.</span><span class="sxs-lookup"><span data-stu-id="a683d-173">A boolean indicating whether or not is allowed to add guests to this directory.</span></span>|
|  <ul><li><span data-ttu-id="a683d-174">ClassificationList</span><span class="sxs-lookup"><span data-stu-id="a683d-174">ClassificationList</span></span><li><span data-ttu-id="a683d-175">Type : string</span><span class="sxs-lookup"><span data-stu-id="a683d-175">Type: String</span></span><li><span data-ttu-id="a683d-176">Valeur par défaut : “”</span><span class="sxs-lookup"><span data-stu-id="a683d-176">Default: “”</span></span> |<span data-ttu-id="a683d-177">Liste des valeurs de classification valides séparées par des virgules pouvant être appliquées à des groupes unifiés.</span><span class="sxs-lookup"><span data-stu-id="a683d-177">A comma-delimited list of valid classification values that can be applied to Unified Groups.</span></span> |
|  <ul><li><span data-ttu-id="a683d-178">EnableGroupCreation</span><span class="sxs-lookup"><span data-stu-id="a683d-178">EnableGroupCreation</span></span><li><span data-ttu-id="a683d-179">Type : booléen</span><span class="sxs-lookup"><span data-stu-id="a683d-179">Type: Boolean</span></span><li><span data-ttu-id="a683d-180">Par défaut : True</span><span class="sxs-lookup"><span data-stu-id="a683d-180">Default: True</span></span> | <span data-ttu-id="a683d-181">Valeur booléenne indiquant si les utilisateurs non-administrateurs peuvent ou non créer des groupes unifiés.</span><span class="sxs-lookup"><span data-stu-id="a683d-181">A boolean indicating whether or not non-admin users can create new Unified groups.</span></span> |


## <a name="read-settings-at-the-directory-level"></a><span data-ttu-id="a683d-182">Lire les paramètres au niveau du répertoire</span><span class="sxs-lookup"><span data-stu-id="a683d-182">Read settings at the directory level</span></span>
<span data-ttu-id="a683d-183">Les étapes suivantes permettent de lire les paramètres au niveau du répertoire qui s’appliquent à tous les groupes Office du répertoire.</span><span class="sxs-lookup"><span data-stu-id="a683d-183">These steps read settings at directory level, which apply to all Office groups in the directory.</span></span>

1. <span data-ttu-id="a683d-184">Lisez tous les paramètres du répertoire existant :</span><span class="sxs-lookup"><span data-stu-id="a683d-184">Read all existing directory settings:</span></span>
  ```
  Get-AzureADDirectorySetting -All $True
  ```
  <span data-ttu-id="a683d-185">Cette applet de commande retourne une liste de tous les paramètres du répertoire :</span><span class="sxs-lookup"><span data-stu-id="a683d-185">This cmdlet returns a list of all directory settings:</span></span>
  ```
  Id                                   DisplayName   TemplateId                           Values
  --                                   -----------   ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323 Group.Unified 62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  ```

2. <span data-ttu-id="a683d-186">Lisez tous les paramètres d’un groupe spécifique :</span><span class="sxs-lookup"><span data-stu-id="a683d-186">Read all settings for a specific group:</span></span>
  ```
  Get-AzureADObjectSetting -TargetObjectId ab6a3887-776a-4db7-9da4-ea2b0d63c504 -TargetType Groups
  ```

3. <span data-ttu-id="a683d-187">Lisez toutes les valeurs de paramètres de répertoire d’un objet settings de répertoire spécifique, à l’aide du GUID de l’ID de paramètres :</span><span class="sxs-lookup"><span data-stu-id="a683d-187">Read all directory settings values of a specific directory settings object, using Settings Id GUID:</span></span>
  ```
  (Get-AzureADDirectorySetting -Id c391b57d-5783-4c53-9236-cefb5c6ef323).values
  ```
  <span data-ttu-id="a683d-188">Cette applet de commande retourne les noms et les valeurs dans cet objet de paramètres pour ce groupe spécifique :</span><span class="sxs-lookup"><span data-stu-id="a683d-188">This cmdlet returns the names and values in this settings object for this specific group:</span></span>
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

## <a name="update-settings-for-a-specific-group"></a><span data-ttu-id="a683d-189">Mettre à jour les paramètres d’un groupe spécifique</span><span class="sxs-lookup"><span data-stu-id="a683d-189">Update settings for a specific group</span></span>

1. <span data-ttu-id="a683d-190">Recherchez le modèle de paramètres nommé « Groups.Unified.Guest »</span><span class="sxs-lookup"><span data-stu-id="a683d-190">Search for the settings template named "Groups.Unified.Guest"</span></span>
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
2. <span data-ttu-id="a683d-191">Récupérez l’objet de modèle pour le modèle Groups.Unified.Guest :</span><span class="sxs-lookup"><span data-stu-id="a683d-191">Retrieve the template object for the Groups.Unified.Guest template:</span></span>
  ```
  $Template = Get-AzureADDirectorySettingTemplate -Id 08d542b9-071f-4e16-94b0-74abb372e3d9
  ```
3. <span data-ttu-id="a683d-192">Créez un nouvel objet settings à partir du modèle :</span><span class="sxs-lookup"><span data-stu-id="a683d-192">Create a new settings object from the template:</span></span>
  ```
  $Setting = $Template.CreateDirectorySetting()
  ```

4. <span data-ttu-id="a683d-193">Définissez le paramètre sur la valeur requise :</span><span class="sxs-lookup"><span data-stu-id="a683d-193">Set the setting to the required value:</span></span>
  ```
  $Setting["AllowToAddGuests"]=$False
  ```
5. <span data-ttu-id="a683d-194">Créez un nouveau paramètre pour le groupe requis dans le répertoire :</span><span class="sxs-lookup"><span data-stu-id="a683d-194">Create the new setting for the required group in the directory:</span></span>
  ```
  New-AzureADObjectSetting -TargetType Groups -TargetObjectId ab6a3887-776a-4db7-9da4-ea2b0d63c504 -DirectorySetting $Setting
  
  Id                                   DisplayName TemplateId                           Values
  --                                   ----------- ----------                           ------
  25651479-a26e-4181-afce-ce24111b2cb5             08d542b9-071f-4e16-94b0-74abb372e3d9 {class SettingValue {...
  ```

## <a name="update-settings-at-the-directory-level"></a><span data-ttu-id="a683d-195">Mettre à jour des paramètres au niveau du répertoire</span><span class="sxs-lookup"><span data-stu-id="a683d-195">Update settings at the directory level</span></span>

<span data-ttu-id="a683d-196">Les étapes suivantes mettent à jour les paramètres au niveau du répertoire qui s’appliquent à tous les groupes unifiés du répertoire.</span><span class="sxs-lookup"><span data-stu-id="a683d-196">These steps update settings at directory level, which apply to all Unified groups in the directory.</span></span> <span data-ttu-id="a683d-197">Ces exemples supposent qu’un objet Settings existe déjà dans votre répertoire.</span><span class="sxs-lookup"><span data-stu-id="a683d-197">These examples assume there is already a Settings object in your directory.</span></span>

1. <span data-ttu-id="a683d-198">Recherchez l’objet Settings existant :</span><span class="sxs-lookup"><span data-stu-id="a683d-198">Find the existing Settings object:</span></span>
  ```
  Get-AzureADDirectorySetting | Where-object -Property Displayname -Value "Group.Unified" -EQ
  
  Id                                   DisplayName   TemplateId                           Values
  --                                   -----------   ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323 Group.Unified 62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  
  $setting = Get-AzureADDirectorySetting –Id c391b57d-5783-4c53-9236-cefb5c6ef323
  ```
2. <span data-ttu-id="a683d-199">Mettez à jour la valeur :</span><span class="sxs-lookup"><span data-stu-id="a683d-199">Update the value:</span></span>
  
  ```
  $Setting["AllowToAddGuests"] = "false"
  ```
3. <span data-ttu-id="a683d-200">Mettez à jour le paramètre :</span><span class="sxs-lookup"><span data-stu-id="a683d-200">Update the setting:</span></span>
  
  ```
  Set-AzureADDirectorySetting -Id c391b57d-5783-4c53-9236-cefb5c6ef323 -DirectorySetting $Setting
  ```

## <a name="remove-settings-at-the-directory-level"></a><span data-ttu-id="a683d-201">Supprimer des paramètres au niveau du répertoire</span><span class="sxs-lookup"><span data-stu-id="a683d-201">Remove settings at the directory level</span></span>
<span data-ttu-id="a683d-202">Les étapes suivantes permettent de supprimer les paramètres au niveau du répertoire qui s’appliquent à tous les groupes Office du répertoire.</span><span class="sxs-lookup"><span data-stu-id="a683d-202">This step removes settings at directory level, which apply to all Office groups in the directory.</span></span>
  ```
  Remove-AzureADDirectorySetting –Id c391b57d-5783-4c53-9236-cefb5c6ef323c
  ```

## <a name="cmdlet-syntax-reference"></a><span data-ttu-id="a683d-203">Informations de référence sur la syntaxe des applets de commande</span><span class="sxs-lookup"><span data-stu-id="a683d-203">Cmdlet syntax reference</span></span>
<span data-ttu-id="a683d-204">Vous trouverez plus d’informations sur Azure Active Directory PowerShell dans la page dédiée aux [applets de commande Azure Active Directory](/powershell/azure/install-adv2?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="a683d-204">You can find more Azure Active Directory PowerShell documentation at [Azure Active Directory Cmdlets](/powershell/azure/install-adv2?view=azureadps-2.0).</span></span>

## <a name="additional-reading"></a><span data-ttu-id="a683d-205">Documentation supplémentaire</span><span class="sxs-lookup"><span data-stu-id="a683d-205">Additional reading</span></span>

* [<span data-ttu-id="a683d-206">Gestion de l’accès aux ressources avec les groupes Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a683d-206">Managing access to resources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="a683d-207">Intégration de vos identités locales avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a683d-207">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
