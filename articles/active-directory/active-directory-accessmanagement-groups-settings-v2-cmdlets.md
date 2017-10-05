---
title: "Exemples PowerShell pour gérer des groupes dans Azure Active Directory | Documents Microsoft"
description: "Cette page fournit des exemples PowerShell pour vous aider à gérer vos groupes dans Azure Active Directory"
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
ms.openlocfilehash: a81820bc778c26f6e8051e2817ebd2b9c24b697a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-version-2-cmdlets-for-group-management"></a><span data-ttu-id="8300c-104">Cmdlets d’Azure Active Directory version 2 pour la gestion de groupe</span><span class="sxs-lookup"><span data-stu-id="8300c-104">Azure Active Directory version 2 cmdlets for group management</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8300c-105">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="8300c-105">Azure portal</span></span>](active-directory-groups-create-azure-portal.md)
> * [<span data-ttu-id="8300c-106">Portail Azure Classic</span><span class="sxs-lookup"><span data-stu-id="8300c-106">Azure classic portal</span></span>](active-directory-accessmanagement-manage-groups.md)
> * [<span data-ttu-id="8300c-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8300c-107">PowerShell</span></span>](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

<span data-ttu-id="8300c-108">Cet article contient des exemples expliquant comment utiliser PowerShell pour gérer vos groupes dans Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8300c-108">This article contains examples of how to use PowerShell to manage your groups in Azure Active Directory (Azure AD).</span></span>  <span data-ttu-id="8300c-109">Il fournit également des informations sur la configuration à l’aide du module Azure AD PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8300c-109">It also tells you how to get set up with the Azure AD PowerShell module.</span></span> <span data-ttu-id="8300c-110">Vous devez tout d’abord [télécharger le module Azure AD PowerShell](https://www.powershellgallery.com/packages/AzureAD/).</span><span class="sxs-lookup"><span data-stu-id="8300c-110">First, you must [download the Azure AD PowerShell module](https://www.powershellgallery.com/packages/AzureAD/).</span></span>

## <a name="installing-the-azure-ad-powershell-module"></a><span data-ttu-id="8300c-111">Installation du module Azure AD PowerShell</span><span class="sxs-lookup"><span data-stu-id="8300c-111">Installing the Azure AD PowerShell module</span></span>
<span data-ttu-id="8300c-112">Pour installer le module PowerShell Azure AD, utilisez les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="8300c-112">To install the Azure AD PowerShell module, use the following commands:</span></span>

    PS C:\Windows\system32> install-module azuread

<span data-ttu-id="8300c-113">Pour vérifier que le module a été installé, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="8300c-113">To verify that the module was installed, use the following command:</span></span>

    PS C:\Windows\system32> get-module azuread

    ModuleType Version      Name                                ExportedCommands
    ---------- ---------    ----                                ----------------
    Binary     2.0.0.115    azuread                      {Add-AzureADAdministrati...}

<span data-ttu-id="8300c-114">Vous pouvez désormais utiliser les applets de commande dans le module.</span><span class="sxs-lookup"><span data-stu-id="8300c-114">Now you can start using the cmdlets in the module.</span></span> <span data-ttu-id="8300c-115">Pour obtenir une description complète des applets de commande du module Azure AD, consultez la documentation de référence en ligne pour [Azure Active Directory PowerShell Version 2](/powershell/azure/install-adv2?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="8300c-115">For a full description of the cmdlets in the Azure AD module, please refer to the online reference documentation for [Azure Active Directory PowerShell Version 2](/powershell/azure/install-adv2?view=azureadps-2.0).</span></span>

## <a name="connecting-to-the-directory"></a><span data-ttu-id="8300c-116">Connexion au répertoire</span><span class="sxs-lookup"><span data-stu-id="8300c-116">Connecting to the directory</span></span>
<span data-ttu-id="8300c-117">Avant de pouvoir gérer des groupes à l’aide des applets de commande Azure AD PowerShell, vous devez connecter votre session PowerShell au répertoire que vous voulez gérer.</span><span class="sxs-lookup"><span data-stu-id="8300c-117">Before you can start managing groups using Azure AD PowerShell cmdlets, you must connect your PowerShell session to the directory you want to manage.</span></span> <span data-ttu-id="8300c-118">Utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="8300c-118">Use the following command:</span></span>

    PS C:\Windows\system32> Connect-AzureAD

<span data-ttu-id="8300c-119">L’applet de commande vous demande de fournir les informations d’identification à utiliser pour accéder à votre répertoire.</span><span class="sxs-lookup"><span data-stu-id="8300c-119">The cmdlet prompts you for the credentials you want to use to access your directory.</span></span> <span data-ttu-id="8300c-120">Dans cet exemple, nous utilisons karen@drumkit.onmicrosoft.com pour accéder au répertoire de démonstration.</span><span class="sxs-lookup"><span data-stu-id="8300c-120">In this example, we are using karen@drumkit.onmicrosoft.com to access the demonstration directory.</span></span> <span data-ttu-id="8300c-121">L’applet de commande renvoie une confirmation pour indiquer que la session a été correctement connectée à votre répertoire :</span><span class="sxs-lookup"><span data-stu-id="8300c-121">The cmdlet returns a confirmation to show the session was connected successfully to your directory:</span></span>

    Account                       Environment Tenant
    -------                       ----------- ------
    Karen@drumkit.onmicrosoft.com AzureCloud  85b5ff1e-0402-400c-9e3c-0f…

<span data-ttu-id="8300c-122">À présent, vous pouvez commencer à utiliser les applets de commande Azure AD pour gérer des groupes dans votre répertoire.</span><span class="sxs-lookup"><span data-stu-id="8300c-122">Now you can start using the AzureAD cmdlets to manage groups in your directory.</span></span>

## <a name="retrieving-groups"></a><span data-ttu-id="8300c-123">Récupération des groupes</span><span class="sxs-lookup"><span data-stu-id="8300c-123">Retrieving groups</span></span>
<span data-ttu-id="8300c-124">Pour récupérer des groupes existants à partir de votre répertoire, vous pouvez utiliser l’applet de commande Get-AzureADGroups.</span><span class="sxs-lookup"><span data-stu-id="8300c-124">To retrieve existing groups from your directory you can use the Get-AzureADGroups cmdlet.</span></span> <span data-ttu-id="8300c-125">Pour récupérer tous les groupes dans le répertoire, utilisez l’applet de commande sans paramètres :</span><span class="sxs-lookup"><span data-stu-id="8300c-125">To retrieve all groups in the directory, use the cmdlet without parameters:</span></span>

    PS C:\Windows\system32> get-azureadgroup

<span data-ttu-id="8300c-126">L’applet de commande renvoie tous les groupes dans le répertoire connecté.</span><span class="sxs-lookup"><span data-stu-id="8300c-126">The cmdlet returns all groups in the connected directory.</span></span>

<span data-ttu-id="8300c-127">Vous pouvez utiliser le paramètre -objectID pour récupérer un groupe spécifique pour lequel vous spécifiez le paramètre objectID du groupe :</span><span class="sxs-lookup"><span data-stu-id="8300c-127">You can use the -objectID parameter to retrieve a specific group for which you specify the group’s objectID:</span></span>

    PS C:\Windows\system32> get-azureadgroup -ObjectId e29bae11-4ac0-450c-bc37-6dae8f3da61b

<span data-ttu-id="8300c-128">L’applet de commande renvoie à présent l’objectID correspond à la valeur du paramètre que vous avez saisi :</span><span class="sxs-lookup"><span data-stu-id="8300c-128">The cmdlet now returns the group whose objectID matches the value of the parameter you entered:</span></span>

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

<span data-ttu-id="8300c-129">Vous pouvez rechercher un groupe spécifique en utilisant le paramètre -filter.</span><span class="sxs-lookup"><span data-stu-id="8300c-129">You can search for a specific group using the -filter parameter.</span></span> <span data-ttu-id="8300c-130">Ce paramètre utilise une clause de filtre ODATA et renvoie tous les groupes qui correspondent au filtre, comme dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="8300c-130">This parameter takes an ODATA filter clause and returns all groups that match the filter, as in the following example:</span></span>

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
> <span data-ttu-id="8300c-131">Les applets de commande AzureAD PowerShell mettent en œuvre la norme de requête OData.</span><span class="sxs-lookup"><span data-stu-id="8300c-131">The AzureAD PowerShell cmdlets implement the OData query standard.</span></span> <span data-ttu-id="8300c-132">Pour plus d’informations, consultez **$filter** dans [options de requête système OData à l’aide du point de terminaison OData](https://msdn.microsoft.com/library/gg309461.aspx#BKMK_filter).</span><span class="sxs-lookup"><span data-stu-id="8300c-132">For more information, see **$filter** in [OData system query options using the OData endpoint](https://msdn.microsoft.com/library/gg309461.aspx#BKMK_filter).</span></span>

## <a name="creating-groups"></a><span data-ttu-id="8300c-133">Création de groupes</span><span class="sxs-lookup"><span data-stu-id="8300c-133">Creating groups</span></span>
<span data-ttu-id="8300c-134">Pour créer un nouveau groupe dans votre répertoire, utilisez l’applet de commande New-AzureADGroup.</span><span class="sxs-lookup"><span data-stu-id="8300c-134">To create a new group in your directory, use the New-AzureADGroup cmdlet.</span></span> <span data-ttu-id="8300c-135">Cette applet de commande crée un nouveau groupe de sécurité appelé « Marketing » :</span><span class="sxs-lookup"><span data-stu-id="8300c-135">This cmdlet creates a new security group called “Marketing":</span></span>

    PS C:\Windows\system32> New-AzureADGroup -Description "Marketing" -DisplayName "Marketing" -MailEnabled $false -SecurityEnabled $true -MailNickName "Marketing"

## <a name="updating-groups"></a><span data-ttu-id="8300c-136">Mise à jour des groupes</span><span class="sxs-lookup"><span data-stu-id="8300c-136">Updating groups</span></span>
<span data-ttu-id="8300c-137">Pour mettre à jour un groupe existant, utilisez l’applet de commande Set-AzureADGroup.</span><span class="sxs-lookup"><span data-stu-id="8300c-137">To update an existing group, use the Set-AzureADGroup cmdlet.</span></span> <span data-ttu-id="8300c-138">Dans cet exemple, nous modifions la propriété DisplayName du groupe « Administrateurs Intune ».</span><span class="sxs-lookup"><span data-stu-id="8300c-138">In this example, we’re changing the DisplayName property of the group “Intune Administrators.”</span></span> <span data-ttu-id="8300c-139">Tout d’abord, nous recherchons le groupe à l’aide de l’applet de commande Get-AzureADGroup et filtrons à l’aide de l’attribut DisplayName :</span><span class="sxs-lookup"><span data-stu-id="8300c-139">First, we’re finding the group using the Get-AzureADGroup cmdlet and filter using the DisplayName attribute:</span></span>

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

<span data-ttu-id="8300c-140">Ensuite, nous attribuons à la propriété Description la nouvelle valeur « Administrateurs d’appareil Intune » :</span><span class="sxs-lookup"><span data-stu-id="8300c-140">Next, we’re changing the Description property to the new value “Intune Device Administrators”:</span></span>

    PS C:\Windows\system32> Set-AzureADGroup -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -Description "Intune Device Administrators"

<span data-ttu-id="8300c-141">À présent, si nous recherchons à nouveau le groupe, nous constatons que la propriété Description est mise à jour pour refléter la nouvelle valeur :</span><span class="sxs-lookup"><span data-stu-id="8300c-141">Now if we find the group again, we see the Description property is updated to reflect the new value:</span></span>

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

## <a name="deleting-groups"></a><span data-ttu-id="8300c-142">Suppression de groupes</span><span class="sxs-lookup"><span data-stu-id="8300c-142">Deleting groups</span></span>
<span data-ttu-id="8300c-143">Pour supprimer des groupes de votre répertoire, utilisez l’applet de commande Remove-AzureADGroup comme suit :</span><span class="sxs-lookup"><span data-stu-id="8300c-143">To delete groups from your directory, use the Remove-AzureADGroup cmdlet as follows:</span></span>

    PS C:\Windows\system32> Remove-AzureADGroup -ObjectId b11ca53e-07cc-455d-9a89-1fe3ab24566b

## <a name="managing-members-of-groups"></a><span data-ttu-id="8300c-144">Gestion des membres des groupes</span><span class="sxs-lookup"><span data-stu-id="8300c-144">Managing members of groups</span></span>
<span data-ttu-id="8300c-145">Si vous devez ajouter de nouveaux membres à un groupe, utilisez l’applet de commande Add-AzureADGroupMember.</span><span class="sxs-lookup"><span data-stu-id="8300c-145">If you need to add new members to a group, use the Add-AzureADGroupMember cmdlet.</span></span> <span data-ttu-id="8300c-146">Cette commande ajoute un membre au groupe Administrateurs Intune que nous avons utilisé dans l’exemple précédent :</span><span class="sxs-lookup"><span data-stu-id="8300c-146">This command adds a member to the Intune Administrators group we used in the previous example:</span></span>

    PS C:\Windows\system32> Add-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -RefObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

<span data-ttu-id="8300c-147">Le paramètre -ObjectId est l’ObjectID du groupe auquel nous souhaitons ajouter un membre et le paramètre -RefObjectId est l’ObjectID de l’utilisateur que nous souhaitons ajouter au groupe en tant que membre.</span><span class="sxs-lookup"><span data-stu-id="8300c-147">The -ObjectId parameter is the ObjectID of the group to which we want to add a member, and the -RefObjectId is the ObjectID of the user we want to add as a member to the group.</span></span>

<span data-ttu-id="8300c-148">Pour obtenir les membres existants d’un groupe, utilisez l’applet de commande Get-AzureADGroupMember, comme dans cet exemple :</span><span class="sxs-lookup"><span data-stu-id="8300c-148">To get the existing members of a group, use the Get-AzureADGroupMember cmdlet, as in this example:</span></span>

    PS C:\Windows\system32> Get-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df

    DeletionTimeStamp ObjectId                             ObjectType
    ----------------- --------                             ----------
                          72cd4bbd-2594-40a2-935c-016f3cfeeeea User
                          8120cc36-64b4-4080-a9e8-23aa98e8b34f User

<span data-ttu-id="8300c-149">Pour supprimer le membre, que nous avons ajouté précédemment au groupe, utilisez l’applet de commande Remove-AzureADGroupMember, comme illustré ici :</span><span class="sxs-lookup"><span data-stu-id="8300c-149">To remove the member we previously added to the group, use the Remove-AzureADGroupMember cmdlet, as is shown here:</span></span>

    PS C:\Windows\system32> Remove-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -MemberId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

<span data-ttu-id="8300c-150">Pour vérifier l’appartenance d’un utilisateur à un groupe, utilisez l’applet de commande Select-AzureADGroupIdsUserIsMemberOf.</span><span class="sxs-lookup"><span data-stu-id="8300c-150">To verify the group membership(s) of a user, use the Select-AzureADGroupIdsUserIsMemberOf cmdlet.</span></span> <span data-ttu-id="8300c-151">Cette applet de commande utilise comme paramètres l’ObjectId de l’utilisateur pour lequel vérifier l’appartenance au groupe et une liste de groupes pour lesquels vérifier les appartenances.</span><span class="sxs-lookup"><span data-stu-id="8300c-151">This cmdlet takes as its parameters the ObjectId of the user for which to check the group memberships, and a list of groups for which to check the memberships.</span></span> <span data-ttu-id="8300c-152">La liste des groupes doit être spécifiée sous la forme d’une variable complexe de type « Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck », donc nous devons tout d’abord créer une variable de ce type :</span><span class="sxs-lookup"><span data-stu-id="8300c-152">The list of groups must be provided in the form of a complex variable of type “Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck”, so we first must create a variable with that type:</span></span>

    PS C:\Windows\system32> $g = new-object Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck

<span data-ttu-id="8300c-153">Ensuite, nous fournissons des valeurs pour les groupIds à vérifier dans l’attribut « GroupIds » de cette variable complexe :</span><span class="sxs-lookup"><span data-stu-id="8300c-153">Next, we provide values for the groupIds to check in the attribute “GroupIds” of this complex variable:</span></span>

    PS C:\Windows\system32> $g.GroupIds = "b11ca53e-07cc-455d-9a89-1fe3ab24566b", "31f1ff6c-d48c-4f8a-b2e1-abca7fd399df"

<span data-ttu-id="8300c-154">À présent, pour vérifier les appartenances aux groupes d’un utilisateur avec l’ObjectID 72cd4bbd-2594-40a2-935c-016f3cfeeeea sur les groupes dans $g, nous devons utiliser :</span><span class="sxs-lookup"><span data-stu-id="8300c-154">Now, if we want to check the group memberships of a user with ObjectID 72cd4bbd-2594-40a2-935c-016f3cfeeeea against the groups in $g, we should use:</span></span>

    PS C:\Windows\system32> Select-AzureADGroupIdsUserIsMemberOf -ObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea -GroupIdsForMembershipCheck $g

    OdataMetadata                                                                                                 Value
    -------------                                                                                                  -----
    https://graph.windows.net/85b5ff1e-0402-400c-9e3c-0f9e965325d1/$metadata#Collection(Edm.String)             {31f1ff6c-d48c-4f8a-b2e1-abca7fd399df}


<span data-ttu-id="8300c-155">La valeur retournée est une liste de groupes dont cet utilisateur est membre.</span><span class="sxs-lookup"><span data-stu-id="8300c-155">The value returned is a list of groups of which this user is a member.</span></span> <span data-ttu-id="8300c-156">Vous pouvez également appliquer cette méthode pour vérifier l’appartenance aux Contacts, Groupes ou Principaux du service pour une liste donnée de groupes, à l’aide de Select-AzureADGroupIdsContactIsMemberOf, Select-AzureADGroupIdsGroupIsMemberOf ou Select-AzureADGroupIdsServicePrincipalIsMemberOf</span><span class="sxs-lookup"><span data-stu-id="8300c-156">You can also apply this method to check Contacts, Groups or Service Principals membership for a given list of groups, using Select-AzureADGroupIdsContactIsMemberOf, Select-AzureADGroupIdsGroupIsMemberOf or Select-AzureADGroupIdsServicePrincipalIsMemberOf</span></span>

## <a name="managing-owners-of-groups"></a><span data-ttu-id="8300c-157">Gestion des propriétaires de groupes</span><span class="sxs-lookup"><span data-stu-id="8300c-157">Managing owners of groups</span></span>
<span data-ttu-id="8300c-158">Pour ajouter des propriétaires à un groupe, utilisez l’applet de commande Add-AzureADGroupOwner :</span><span class="sxs-lookup"><span data-stu-id="8300c-158">To add owners to a group, use the Add-AzureADGroupOwner cmdlet:</span></span>

    PS C:\Windows\system32> Add-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -RefObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

<span data-ttu-id="8300c-159">Le paramètre -ObjectId est l’ObjectID du groupe auquel nous souhaitons ajouter un propriétaire et le paramètre -RefObjectId est l’ObjectID de l’utilisateur que nous souhaitons ajouter au groupe en tant que propriétaire.</span><span class="sxs-lookup"><span data-stu-id="8300c-159">The -ObjectId parameter is the ObjectID of the group to which we want to add an owner, and the -RefObjectId is the ObjectID of the user we want to add as an owner of the group.</span></span>

<span data-ttu-id="8300c-160">Pour récupérer les propriétaires d’un groupe, utilisez l’applet de commande Get-AzureADGroupOwner :</span><span class="sxs-lookup"><span data-stu-id="8300c-160">To retrieve the owners of a group, use the Get-AzureADGroupOwner cmdlet:</span></span>

    PS C:\Windows\system32> Get-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df

<span data-ttu-id="8300c-161">L’applet de commande renvoie la liste des propriétaires du groupe spécifié :</span><span class="sxs-lookup"><span data-stu-id="8300c-161">The cmdlet returns the list of owners for the specified group:</span></span>

    DeletionTimeStamp ObjectId                             ObjectType
    ----------------- --------                             ----------
                          e831b3fd-77c9-49c7-9fca-de43e109ef67 User

<span data-ttu-id="8300c-162">Si vous souhaitez supprimer un propriétaire d’un groupe, utilisez l’applet de commande Remove-AzureADGroupOwner :</span><span class="sxs-lookup"><span data-stu-id="8300c-162">If you want to remove an owner from a group, use the Remove-AzureADGroupOwner cmdlet:</span></span>

    PS C:\Windows\system32> remove-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -OwnerId e831b3fd-77c9-49c7-9fca-de43e109ef67

## <a name="reserved-aliases"></a><span data-ttu-id="8300c-163">Alias réservés</span><span class="sxs-lookup"><span data-stu-id="8300c-163">Reserved aliases</span></span> 
<span data-ttu-id="8300c-164">Quand un groupe est créé, certain points de terminaison autorisent l’utilisateur final à spécifier un mailNickname ou alias à utiliser dans l’adresse e-mail du groupe.</span><span class="sxs-lookup"><span data-stu-id="8300c-164">When a group is created, certain endpoints allow the end user to specify a mailNickname or alias to be used as part of the email address of the group.</span></span> <span data-ttu-id="8300c-165">Les groupes avec les alias de messagerie hautement privilégiés suivants peuvent uniquement être créés par un administrateur général Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8300c-165">Groups with the following highly privileged email aliases can only be created by an Azure AD global administrator.</span></span> 
  
* <span data-ttu-id="8300c-166">abuse</span><span class="sxs-lookup"><span data-stu-id="8300c-166">abuse</span></span> 
* <span data-ttu-id="8300c-167">admin</span><span class="sxs-lookup"><span data-stu-id="8300c-167">admin</span></span> 
* <span data-ttu-id="8300c-168">administrator</span><span class="sxs-lookup"><span data-stu-id="8300c-168">administrator</span></span> 
* <span data-ttu-id="8300c-169">hostmaster</span><span class="sxs-lookup"><span data-stu-id="8300c-169">hostmaster</span></span> 
* <span data-ttu-id="8300c-170">majordomo</span><span class="sxs-lookup"><span data-stu-id="8300c-170">majordomo</span></span> 
* <span data-ttu-id="8300c-171">postmaster</span><span class="sxs-lookup"><span data-stu-id="8300c-171">postmaster</span></span> 
* <span data-ttu-id="8300c-172">root</span><span class="sxs-lookup"><span data-stu-id="8300c-172">root</span></span> 
* <span data-ttu-id="8300c-173">secure</span><span class="sxs-lookup"><span data-stu-id="8300c-173">secure</span></span> 
* <span data-ttu-id="8300c-174">security</span><span class="sxs-lookup"><span data-stu-id="8300c-174">security</span></span> 
* <span data-ttu-id="8300c-175">ssl-admin</span><span class="sxs-lookup"><span data-stu-id="8300c-175">ssl-admin</span></span> 
* <span data-ttu-id="8300c-176">webmaster</span><span class="sxs-lookup"><span data-stu-id="8300c-176">webmaster</span></span> 

## <a name="next-steps"></a><span data-ttu-id="8300c-177">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8300c-177">Next steps</span></span>
<span data-ttu-id="8300c-178">Vous trouverez plus d’informations sur Azure Active Directory PowerShell dans la page dédiée aux [applets de commande Azure Active Directory](/powershell/azure/install-adv2?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="8300c-178">You can find more Azure Active Directory PowerShell documentation at [Azure Active Directory Cmdlets](/powershell/azure/install-adv2?view=azureadps-2.0).</span></span>

* [<span data-ttu-id="8300c-179">Gestion de l’accès aux ressources avec les groupes Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8300c-179">Managing access to resources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="8300c-180">Intégration de vos identités locales avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8300c-180">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
