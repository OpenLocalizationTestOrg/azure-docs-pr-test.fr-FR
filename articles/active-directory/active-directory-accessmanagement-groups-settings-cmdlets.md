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
# <a name="azure-active-directory-cmdlets-for-configuring-group-settings"></a>Configuration des paramètres de groupe avec les applets de commande Azure Active Directory

> [!IMPORTANT]
> Ce contenu s’applique uniquement les groupes de 365 tooOffice. Pour plus d’informations sur la façon de définir des groupes de sécurité utilisateurs toocreate tooallow, `Set-MSOLCompanySettings -UsersPermissionToCreateGroupsEnabled $True` comme décrit dans [Set-MSOLCompanySettings](https://docs.microsoft.com/en-us/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0). 

Les paramètres des groupes Office 365 sont configurés à l’aide d’un objet Settings et d’un objet SettingsTemplate. Au départ, vous ne voyez tous les objets de paramètres dans votre annuaire, votre répertoire étant configuré avec des paramètres par défaut hello. paramètres par défaut de hello toochange, vous devez créer un nouvel objet de paramètres à l’aide d’un modèle de paramètres. Les modèles de paramètres sont définis par Microsoft. Il existe différents modèles de paramètres. paramètres de groupe tooconfigure Office 365 de votre annuaire, vous utilisez modèle hello nommé « Group.Unified ». tooconfigure Office 365 les paramètres de groupe sur un seul groupe, utilisez modèle hello nommé « Group.Unified.Guest ». Ce modèle est un groupe de toomanage utilisé invité accès tooan Office 365. 

applets de commande Hello font partie du module de hello Azure Active Directory PowerShell V2. Pour obtenir des instructions toodownload et le module de hello installer sur votre ordinateur, voir l’article de hello [Azure Active Directory PowerShell Version 2](https://docs.microsoft.com/powershell/azuread/). Vous pouvez installer la mise en production de la version 2 hello module hello [galerie de PowerShell hello](https://www.powershellgallery.com/packages/AzureAD/).

## <a name="retrieve-a-specific-settings-value"></a>Récupérer une valeur de paramètres spécifique
Si vous connaissez le nom hello de hello paramètre, vous souhaitez tooretrieve, vous pouvez utiliser hello sous la valeur de paramètres en cours d’applet de commande tooretrieve hello. Dans cet exemple, nous récupérons valeur hello pour un paramètre nommé « UsageGuidelinesUrl ». Vous trouverez plus d’informations sur les paramètres de répertoire et leurs noms plus loin dans cet article.

```powershell
(Get-AzureADDirectorySetting).Values | Where-Object -Property Name -Value UsageGuidelinesUrl -EQ
```

## <a name="create-settings-at-hello-directory-level"></a>Créer des paramètres au niveau du répertoire hello
Les étapes suivantes créent des paramètres au niveau de l’annuaire, qui s’appliquent tooall Office 365 groupes (unifié) dans le répertoire de hello.

1. Bonjour DirectorySettings applets de commande, vous devez spécifier les ID de hello Hello SettingsTemplate vous souhaitez toouse. Si vous ne connaissez pas cet ID, cette applet de commande renvoie la liste hello de tous les modèles de paramètres :
  
  ```
  PS C:> Get-AzureADDirectorySettingTemplate
  ```
  Cet appel d’applet de commande retourne tous les modèles disponibles :
  
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
2. tooadd une URL de l’indication d’utilisation, vous devez tooget hello SettingsTemplate objet qui définit la valeur d’URL indications hello d’utilisation ; Autrement dit, hello Group.Unified modèle :
  
  ```
  $Template = Get-AzureADDirectorySettingTemplate -Id 62375ab9-6b52-47ed-826b-58e47e0e304b
  ```
3. Ensuite, créez un nouvel objet Settings basé sur ce modèle :
  
  ```
  $Setting = $template.CreateDirectorySetting()
  ```  
4. Puis mettez à jour la valeur hello utilisation indication :
  
  ```
  $setting["UsageGuidelinesUrl"] = "<https://guideline.com>"
  ```  
5. Enfin, appliquez les paramètres hello :
  
  ```
  New-AzureADDirectorySetting -DirectorySetting $setting
  ```

En cas de réussite, hello applet de commande renvoie les ID de hello du nouvel objet de paramètres hello :
  ```
  Id                                   DisplayName TemplateId                           Values
  --                                   ----------- ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323             62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  ```
Voici les paramètres hello définis dans hello Group.Unified SettingsTemplate.

| **Paramètre** | **Description** |
| --- | --- |
|  <ul><li>EnableGroupCreation<li>Type : booléen<li>Par défaut : True |indicateur Hello indiquant si la création du groupe d’unifié est autorisée dans le répertoire de hello. |
|  <ul><li>GroupCreationAllowedGroupId<li>Type : string<li>Valeur par défaut : “” |GUID du groupe de sécurité hello pour le hello les membres sont autorisés à toocreate Unified Groups même lorsque EnableGroupCreation == false. |
|  <ul><li>UsageGuidelinesUrl<li>Type : string<li>Valeur par défaut : “” |Un lien toohello consignes d’utilisation de groupe. |
|  <ul><li>ClassificationDescriptions<li>Type : string<li>Valeur par défaut : “” | Liste séparée par des virgules des descriptions de classification. |
|  <ul><li>DefaultClassification<li>Type : string<li>Valeur par défaut : “” | classification de Hello est toobe utilisé en tant que classement par défaut de hello pour un groupe, si aucun n’a été spécifié.|
|  <ul><li>PrefixSuffixNamingRequirement<li>Type : string<li>Valeur par défaut : “” |Pas encore implémenté
|  <ul><li>AllowGuestsToBeGroupOwner<li>Type : booléen<li>Par défaut : False | Valeur booléenne indiquant si un utilisateur invité peut être ou non un propriétaire de groupes. |
|  <ul><li>AllowGuestsToAccessGroups<li>Type : booléen<li>Par défaut : True | Valeur booléenne indiquant si un utilisateur invité peut avoir le contenu des groupes d’accès tooUnified. |
|  <ul><li>GuestUsageGuidelinesUrl<li>Type : string<li>Valeur par défaut : “” | url de Hello une instructions d’utilisation de lien toohello invité. |
|  <ul><li>AllowToAddGuests<li>Type : booléen<li>Par défaut : True | Une valeur booléenne indiquant si est autorisée tooadd ou non invités toothis active.|
|  <ul><li>ClassificationList<li>Type : string<li>Valeur par défaut : “” |Une liste délimitée par des virgules des valeurs de classification valides qui peuvent être appliqués tooUnified des groupes. |
|  <ul><li>EnableGroupCreation<li>Type : booléen<li>Par défaut : True | Valeur booléenne indiquant si les utilisateurs non-administrateurs peuvent ou non créer des groupes unifiés. |


## <a name="read-settings-at-hello-directory-level"></a>Lire les paramètres au niveau du répertoire hello
Ces étapes de lire les paramètres au niveau de l’annuaire, qui s’appliquent à des groupes de Office tooall dans le répertoire de hello.

1. Lisez tous les paramètres du répertoire existant :
  ```
  Get-AzureADDirectorySetting -All $True
  ```
  Cette applet de commande retourne une liste de tous les paramètres du répertoire :
  ```
  Id                                   DisplayName   TemplateId                           Values
  --                                   -----------   ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323 Group.Unified 62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  ```

2. Lisez tous les paramètres d’un groupe spécifique :
  ```
  Get-AzureADObjectSetting -TargetObjectId ab6a3887-776a-4db7-9da4-ea2b0d63c504 -TargetType Groups
  ```

3. Lisez toutes les valeurs de paramètres de répertoire d’un objet settings de répertoire spécifique, à l’aide du GUID de l’ID de paramètres :
  ```
  (Get-AzureADDirectorySetting -Id c391b57d-5783-4c53-9236-cefb5c6ef323).values
  ```
  Cette applet de commande renvoie les noms hello et les valeurs dans cet objet de paramètres pour ce groupe spécifique :
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

## <a name="update-settings-for-a-specific-group"></a>Mettre à jour les paramètres d’un groupe spécifique

1. Recherchez le modèle de paramètres de hello nommé « Groups.Unified.Guest »
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
2. Récupérer l’objet de modèle hello pour le modèle de Groups.Unified.Guest hello :
  ```
  $Template = Get-AzureADDirectorySettingTemplate -Id 08d542b9-071f-4e16-94b0-74abb372e3d9
  ```
3. Créer un nouvel objet de paramètres de modèle de hello :
  ```
  $Setting = $Template.CreateDirectorySetting()
  ```

4. Définir la valeur hello toohello requis :
  ```
  $Setting["AllowToAddGuests"]=$False
  ```
5. Créer nouveau paramètre de hello pour les groupes requis hello dans le répertoire de hello :
  ```
  New-AzureADObjectSetting -TargetType Groups -TargetObjectId ab6a3887-776a-4db7-9da4-ea2b0d63c504 -DirectorySetting $Setting
  
  Id                                   DisplayName TemplateId                           Values
  --                                   ----------- ----------                           ------
  25651479-a26e-4181-afce-ce24111b2cb5             08d542b9-071f-4e16-94b0-74abb372e3d9 {class SettingValue {...
  ```

## <a name="update-settings-at-hello-directory-level"></a>Paramètres de mise à jour au niveau du répertoire hello

Ces étapes de mettre à jour les paramètres au niveau de l’annuaire, qui s’appliquent les groupes d’unifiée tooall dans le répertoire de hello. Ces exemples supposent qu’un objet Settings existe déjà dans votre répertoire.

1. Rechercher un objet de paramètres hello existant :
  ```
  Get-AzureADDirectorySetting | Where-object -Property Displayname -Value "Group.Unified" -EQ
  
  Id                                   DisplayName   TemplateId                           Values
  --                                   -----------   ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323 Group.Unified 62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  
  $setting = Get-AzureADDirectorySetting –Id c391b57d-5783-4c53-9236-cefb5c6ef323
  ```
2. Mettre à jour la valeur de hello :
  
  ```
  $Setting["AllowToAddGuests"] = "false"
  ```
3. Mise à jour du paramètre de hello :
  
  ```
  Set-AzureADDirectorySetting -Id c391b57d-5783-4c53-9236-cefb5c6ef323 -DirectorySetting $Setting
  ```

## <a name="remove-settings-at-hello-directory-level"></a>Supprimer les paramètres au niveau du répertoire hello
Cette étape supprime les paramètres au niveau de l’annuaire, qui s’appliquent à des groupes de Office tooall dans le répertoire de hello.
  ```
  Remove-AzureADDirectorySetting –Id c391b57d-5783-4c53-9236-cefb5c6ef323c
  ```

## <a name="cmdlet-syntax-reference"></a>Informations de référence sur la syntaxe des applets de commande
Vous trouverez plus d’informations sur Azure Active Directory PowerShell dans la page dédiée aux [applets de commande Azure Active Directory](/powershell/azure/install-adv2?view=azureadps-2.0).

## <a name="additional-reading"></a>Documentation supplémentaire

* [La gestion des accès tooresources avec les groupes Azure Active Directory](active-directory-manage-groups.md)
* [Intégration de vos identités locales avec Azure Active Directory](active-directory-aadconnect.md)
