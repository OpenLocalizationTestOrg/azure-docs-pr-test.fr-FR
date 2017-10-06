---
title: "exemples d’aaaPowerShell pour la gestion des groupes dans Azure Active Directory | Documents Microsoft"
description: "Cette page fournit PowerShell exemples toohelp vous gérez vos groupes dans Azure Active Directory"
keywords: Azure AD, Azure Active Directory, PowerShell, Groupes, Gestion des groupes
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 7a5023dc-2727-4c25-8254-b531fc3244ac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: curtand
ms.reviewer: rodejo
ms.openlocfilehash: ba049babc436e99a290f20899b3a87bcfa811d9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-version-2-cmdlets-for-group-management"></a>Cmdlets d’Azure Active Directory version 2 pour la gestion de groupe
> [!div class="op_single_selector"]
> * [Portail Azure](active-directory-groups-create-azure-portal.md)
> * [Portail Azure Classic](active-directory-accessmanagement-manage-groups.md)
> * [PowerShell](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

Cet article contient des exemples de toouse PowerShell toomanage vos groupes dans Azure Active Directory (Azure AD).  Il vous indique également comment configurer tooget avec le module PowerShell Azure AD de hello. Vous devez tout d’abord, [télécharger le module PowerShell Azure AD hello](https://www.powershellgallery.com/packages/AzureAD/).

## <a name="installing-hello-azure-ad-powershell-module"></a>Installation du module PowerShell Azure AD de hello
tooinstall hello module PowerShell Azure AD, utilisez hello suivant de commandes :

    PS C:\Windows\system32> install-module azuread

tooverify qui hello module a été installé, utilisez hello de commande suivante :

    PS C:\Windows\system32> get-module azuread

    ModuleType Version      Name                                ExportedCommands
    ---------- ---------    ----                                ----------------
    Binary     2.0.0.115    azuread                      {Add-AzureADAdministrati...}

Vous pouvez maintenant commencer à l’aide des applets de commande hello dans le module de hello. Pour obtenir une description complète des applets de commande hello dans le module de hello Azure AD, reportez-vous à la documentation de référence en ligne toohello pour [Azure Active Directory PowerShell Version 2](/powershell/azure/install-adv2?view=azureadps-2.0).

## <a name="connecting-toohello-directory"></a>Connexion toohello Active
Avant de commencer la gestion des groupes à l’aide des applets de commande PowerShell Azure AD, vous devez vous connecter à votre répertoire de toohello de session de PowerShell vous souhaitez toomanage. Utilisez hello de commande suivante :

    PS C:\Windows\system32> Connect-AzureAD

Hello applet de commande vous invite pour les informations d’identification de hello vous souhaitez toouse tooaccess votre répertoire. Dans cet exemple, nous utilisons karen@drumkit.onmicrosoft.com tooaccess hello active de démonstration. Hello applet de commande renvoie une session de hello tooshow confirmation a été correctement connectée tooyour active :

    Account                       Environment Tenant
    -------                       ----------- ------
    Karen@drumkit.onmicrosoft.com AzureCloud  85b5ff1e-0402-400c-9e3c-0f…

Vous pouvez maintenant démarrer à l’aide de groupes de toomanage hello organisation applets de commande dans votre annuaire.

## <a name="retrieving-groups"></a>Récupération des groupes
à partir de votre annuaire, que vous pouvez utiliser des groupes existants tooretrieve hello applet de commande Get-AzureADGroups. tooretrieve tous les groupes dans le répertoire hello, utilisez hello applet de commande sans paramètres :

    PS C:\Windows\system32> get-azureadgroup

applet de commande Hello retourne tous les groupes dans l’annuaire connecté de hello.

Vous pouvez utiliser hello - objectID paramètre tooretrieve un groupe spécifique pour lequel vous spécifiez les objectID du groupe hello :

    PS C:\Windows\system32> get-azureadgroup -ObjectId e29bae11-4ac0-450c-bc37-6dae8f3da61b

applet de commande Hello retourne maintenant groupe hello dont objectID correspond à la valeur hello du paramètre hello que vous avez entré :

    DeletionTimeStamp            :
    ObjectId                     : e29bae11-4ac0-450c-bc37-6dae8f3da61b
    ObjectType                   : Group
    Description                  :
    DirSyncEnabled               :
    DisplayName                  : Pacific NW Support
    LastDirSyncTime              :
    Mail                         :
    MailEnabled                  : False
    MailNickName                 : 9bb4139b-60a1-434a-8c0d-7c1f8eee2df9
    OnPremisesSecurityIdentifier :
    ProvisioningErrors           : {}
    ProxyAddresses               : {}
    SecurityEnabled              : True

Vous pouvez rechercher un groupe spécifique à l’aide de hello - paramètre de filtre. Ce paramètre accepte une clause de filtre ODATA et retourne tous les groupes qui correspondent au filtre hello, comme dans hello l’exemple suivant :

    PS C:\Windows\system32> Get-AzureADGroup -Filter "DisplayName eq 'Intune Administrators'"


    DeletionTimeStamp            :
    ObjectId                     : 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df
    ObjectType                   : Group
    Description                  : Intune Administrators
    DirSyncEnabled               :
    DisplayName                  : Intune Administrators
    LastDirSyncTime              :
    Mail                         :
    MailEnabled                  : False
    MailNickName                 : 4dd067a0-6515-4f23-968a-cc2ffc2eff5c
    OnPremisesSecurityIdentifier :
    ProvisioningErrors           : {}
    ProxyAddresses               : {}
    SecurityEnabled              : True

> [!NOTE] 
> Hello applets de commande PowerShell de AzureAD implémenter hello requête OData standard. Pour plus d’informations, consultez **$filter** dans [options de requête système OData à l’aide du point de terminaison OData hello](https://msdn.microsoft.com/library/gg309461.aspx#BKMK_filter).

## <a name="creating-groups"></a>Création de groupes
toocreate un nouveau groupe dans votre annuaire, l’applet de commande utilisez hello AzureADGroup de nouveau. Cette applet de commande crée un nouveau groupe de sécurité appelé « Marketing » :

    PS C:\Windows\system32> New-AzureADGroup -Description "Marketing" -DisplayName "Marketing" -MailEnabled $false -SecurityEnabled $true -MailNickName "Marketing"

## <a name="updating-groups"></a>Mise à jour des groupes
tooupdate un groupe existant, utilisez l’applet de commande de hello AzureADGroup de jeu. Dans cet exemple, nous passons hello DisplayName, propriété du groupe de hello « Administrateurs de Intune ». Tout d’abord, nous avons observé groupe hello à l’aide d’applet de commande Get-AzureADGroup hello et filtre en utilisant l’attribut DisplayName de hello :

    PS C:\Windows\system32> Get-AzureADGroup -Filter "DisplayName eq 'Intune Administrators'"


    DeletionTimeStamp            :
    ObjectId                     : 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df
    ObjectType                   : Group
    Description                  : Intune Administrators
    DirSyncEnabled               :
    DisplayName                  : Intune Administrators
    LastDirSyncTime              :
    Mail                         :
    MailEnabled                  : False
    MailNickName                 : 4dd067a0-6515-4f23-968a-cc2ffc2eff5c
    OnPremisesSecurityIdentifier :
    ProvisioningErrors           : {}
    ProxyAddresses               : {}
    SecurityEnabled              : True

Ensuite, nous passons hello Description toohello nouvelle valeur de la propriété « Administrateurs de l’appareil Intune » :

    PS C:\Windows\system32> Set-AzureADGroup -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -Description "Intune Device Administrators"

Maintenant si nous trouvons à nouveau groupe de hello, nous voyons de propriété de Description hello est mise à jour tooreflect hello nouvelle valeur :

    PS C:\Windows\system32> Get-AzureADGroup -Filter "DisplayName eq 'Intune Administrators'"


    DeletionTimeStamp            :
    ObjectId                     : 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df
    ObjectType                   : Group
    Description                  : Intune Device Administrators
    DirSyncEnabled               :
    DisplayName                  : Intune Administrators
    LastDirSyncTime              :
    Mail                         :
    MailEnabled                  : False
    MailNickName                 : 4dd067a0-6515-4f23-968a-cc2ffc2eff5c
    OnPremisesSecurityIdentifier :
    ProvisioningErrors           : {}
    ProxyAddresses               : {}
    SecurityEnabled              : True

## <a name="deleting-groups"></a>Suppression de groupes
groupes de toodelete à partir de votre annuaire, utilisez applet de commande Remove-AzureADGroup hello comme suit :

    PS C:\Windows\system32> Remove-AzureADGroup -ObjectId b11ca53e-07cc-455d-9a89-1fe3ab24566b

## <a name="managing-members-of-groups"></a>Gestion des membres des groupes
Si vous devez de nouveau groupe de tooa membres tooadd, utiliser l’applet de commande Add-AzureADGroupMember de hello. Cette commande ajoute un groupe d’administrateurs Intune toohello membre que nous avons utilisé dans l’exemple précédent de hello :

    PS C:\Windows\system32> Add-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -RefObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

paramètre - ObjectId Hello est hello ObjectID de hello groupe toowhich nous souhaitons tooadd membre et hello ObjectID est hello - RefObjectId d’utilisateur de hello que vous souhaitez tooadd en tant que membre toohello groupe.

membres existants de hello tooget d’un groupe, utilisez la cmdlet Get-AzureADGroupMember de hello, comme dans cet exemple :

    PS C:\Windows\system32> Get-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df

    DeletionTimeStamp ObjectId                             ObjectType
    ----------------- --------                             ----------
                          72cd4bbd-2594-40a2-935c-016f3cfeeeea User
                          8120cc36-64b4-4080-a9e8-23aa98e8b34f User

membre de hello tooremove nous avons ajouté précédemment toohello groupe, utilisez hello Remove-AzureADGroupMember applet de commande, comme est indiqué ici :

    PS C:\Windows\system32> Remove-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -MemberId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

appartenances tooverify hello d’un utilisateur, utilisez l’applet de commande Select-AzureADGroupIdsUserIsMemberOf hello. Cette applet de commande prend comme ses paramètres hello ObjectId de l’utilisateur de hello pour les membres du groupe toocheck hello et une liste de groupes pour les appartenances de hello toocheck. liste Hello des groupes doit être fournie sous forme de hello d’une variable complexe de type « Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck », par conséquent, nous devons créons d’abord une variable avec ce type :

    PS C:\Windows\system32> $g = new-object Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck

Ensuite, nous fournissons des valeurs de toocheck les GroupID de hello dans l’attribut hello « Les GroupID » de cette variable complexe :

    PS C:\Windows\system32> $g.GroupIds = "b11ca53e-07cc-455d-9a89-1fe3ab24566b", "31f1ff6c-d48c-4f8a-b2e1-abca7fd399df"

Maintenant, si nous voulons appartenances toocheck hello d’un utilisateur avec 72cd4bbd-2594-40a2-935c-016f3cfeeeea ObjectID sur des groupes de hello dans $g, nous devons utiliser :

    PS C:\Windows\system32> Select-AzureADGroupIdsUserIsMemberOf -ObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea -GroupIdsForMembershipCheck $g

    OdataMetadata                                                                                                 Value
    -------------                                                                                                  -----
    https://graph.windows.net/85b5ff1e-0402-400c-9e3c-0f9e965325d1/$metadata#Collection(Edm.String)             {31f1ff6c-d48c-4f8a-b2e1-abca7fd399df}


valeur Hello retournée est une liste de groupes dont cet utilisateur est membre. Vous pouvez également appliquer cette toocheck méthode appartenance Contacts, groupes ou principaux du Service pour obtenir la liste des groupes, à l’aide de Select-AzureADGroupIdsContactIsMemberOf, sélectionnez-AzureADGroupIdsGroupIsMemberOf donnée ou Sélectionnez-AzureADGroupIdsServicePrincipalIsMemberOf

## <a name="managing-owners-of-groups"></a>Gestion des propriétaires de groupes
groupe du tooa tooadd propriétaires, utilisez hello Add-AzureADGroupOwner applet de commande :

    PS C:\Windows\system32> Add-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -RefObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

paramètre - ObjectId Hello est hello ObjectID de hello groupe toowhich nous souhaitons tooadd un propriétaire et hello ObjectID est hello - RefObjectId d’utilisateur de hello que vous souhaitez tooadd en tant que propriétaire du groupe de hello.

propriétaires de hello tooretrieve d’un groupe, utilisez l’applet de commande Get-AzureADGroupOwner hello :

    PS C:\Windows\system32> Get-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df

applet de commande Hello retourne la liste hello des propriétaires de groupe spécifié de hello :

    DeletionTimeStamp ObjectId                             ObjectType
    ----------------- --------                             ----------
                          e831b3fd-77c9-49c7-9fca-de43e109ef67 User

Si vous voulez tooremove un propriétaire d’un groupe, utilisez l’applet de commande Remove-AzureADGroupOwner hello :

    PS C:\Windows\system32> remove-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -OwnerId e831b3fd-77c9-49c7-9fca-de43e109ef67

## <a name="reserved-aliases"></a>Alias réservés 
Lors de la création d’un groupe, certains points de terminaison autorisent hello utilisateur final toospecify un toobe mailNickname ou l’alias utilisé dans le cadre de l’adresse de messagerie hello du groupe de hello. Groupes avec hello suivant des alias de messagerie hautement privilégiés peuvent uniquement être créés par un administrateur global Azure AD. 
  
* abuse 
* admin 
* administrator 
* hostmaster 
* majordomo 
* postmaster 
* root 
* secure 
* security 
* ssl-admin 
* webmaster 

## <a name="next-steps"></a>Étapes suivantes
Vous trouverez plus d’informations sur Azure Active Directory PowerShell dans la page dédiée aux [applets de commande Azure Active Directory](/powershell/azure/install-adv2?view=azureadps-2.0).

* [La gestion des accès tooresources avec les groupes Azure Active Directory](active-directory-manage-groups.md)
* [Intégration de vos identités locales avec Azure Active Directory](active-directory-aadconnect.md)
