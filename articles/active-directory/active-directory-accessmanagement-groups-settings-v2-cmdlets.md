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
# <a name="azure-active-directory-version-2-cmdlets-for-group-management"></a><span data-ttu-id="d0d1b-104">Cmdlets d’Azure Active Directory version 2 pour la gestion de groupe</span><span class="sxs-lookup"><span data-stu-id="d0d1b-104">Azure Active Directory version 2 cmdlets for group management</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d0d1b-105">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="d0d1b-105">Azure portal</span></span>](active-directory-groups-create-azure-portal.md)
> * [<span data-ttu-id="d0d1b-106">Portail Azure Classic</span><span class="sxs-lookup"><span data-stu-id="d0d1b-106">Azure classic portal</span></span>](active-directory-accessmanagement-manage-groups.md)
> * [<span data-ttu-id="d0d1b-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d0d1b-107">PowerShell</span></span>](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

<span data-ttu-id="d0d1b-108">Cet article contient des exemples de toouse PowerShell toomanage vos groupes dans Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d0d1b-108">This article contains examples of how toouse PowerShell toomanage your groups in Azure Active Directory (Azure AD).</span></span>  <span data-ttu-id="d0d1b-109">Il vous indique également comment configurer tooget avec le module PowerShell Azure AD de hello.</span><span class="sxs-lookup"><span data-stu-id="d0d1b-109">It also tells you how tooget set up with hello Azure AD PowerShell module.</span></span> <span data-ttu-id="d0d1b-110">Vous devez tout d’abord, [télécharger le module PowerShell Azure AD hello](https://www.powershellgallery.com/packages/AzureAD/).</span><span class="sxs-lookup"><span data-stu-id="d0d1b-110">First, you must [download hello Azure AD PowerShell module](https://www.powershellgallery.com/packages/AzureAD/).</span></span>

## <a name="installing-hello-azure-ad-powershell-module"></a><span data-ttu-id="d0d1b-111">Installation du module PowerShell Azure AD de hello</span><span class="sxs-lookup"><span data-stu-id="d0d1b-111">Installing hello Azure AD PowerShell module</span></span>
<span data-ttu-id="d0d1b-112">tooinstall hello module PowerShell Azure AD, utilisez hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="d0d1b-112">tooinstall hello Azure AD PowerShell module, use hello following commands:</span></span>

    PS C:\Windows\system32> install-module azuread

<span data-ttu-id="d0d1b-113">tooverify qui hello module a été installé, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="d0d1b-113">tooverify that hello module was installed, use hello following command:</span></span>

    PS C:\Windows\system32> get-module azuread

    ModuleType Version      Name                                ExportedCommands
    ---------- ---------    ----                                ----------------
    Binary     2.0.0.115    azuread                      {Add-AzureADAdministrati...}

<span data-ttu-id="d0d1b-114">Vous pouvez maintenant commencer à l’aide des applets de commande hello dans le module de hello.</span><span class="sxs-lookup"><span data-stu-id="d0d1b-114">Now you can start using hello cmdlets in hello module.</span></span> <span data-ttu-id="d0d1b-115">Pour obtenir une description complète des applets de commande hello dans le module de hello Azure AD, reportez-vous à la documentation de référence en ligne toohello pour [Azure Active Directory PowerShell Version 2](/powershell/azure/install-adv2?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="d0d1b-115">For a full description of hello cmdlets in hello Azure AD module, please refer toohello online reference documentation for [Azure Active Directory PowerShell Version 2](/powershell/azure/install-adv2?view=azureadps-2.0).</span></span>

## <a name="connecting-toohello-directory"></a><span data-ttu-id="d0d1b-116">Connexion toohello Active</span><span class="sxs-lookup"><span data-stu-id="d0d1b-116">Connecting toohello directory</span></span>
<span data-ttu-id="d0d1b-117">Avant de commencer la gestion des groupes à l’aide des applets de commande PowerShell Azure AD, vous devez vous connecter à votre répertoire de toohello de session de PowerShell vous souhaitez toomanage.</span><span class="sxs-lookup"><span data-stu-id="d0d1b-117">Before you can start managing groups using Azure AD PowerShell cmdlets, you must connect your PowerShell session toohello directory you want toomanage.</span></span> <span data-ttu-id="d0d1b-118">Utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="d0d1b-118">Use hello following command:</span></span>

    PS C:\Windows\system32> Connect-AzureAD

<span data-ttu-id="d0d1b-119">Hello applet de commande vous invite pour les informations d’identification de hello vous souhaitez toouse tooaccess votre répertoire.</span><span class="sxs-lookup"><span data-stu-id="d0d1b-119">hello cmdlet prompts you for hello credentials you want toouse tooaccess your directory.</span></span> <span data-ttu-id="d0d1b-120">Dans cet exemple, nous utilisons karen@drumkit.onmicrosoft.com tooaccess hello active de démonstration.</span><span class="sxs-lookup"><span data-stu-id="d0d1b-120">In this example, we are using karen@drumkit.onmicrosoft.com tooaccess hello demonstration directory.</span></span> <span data-ttu-id="d0d1b-121">Hello applet de commande renvoie une session de hello tooshow confirmation a été correctement connectée tooyour active :</span><span class="sxs-lookup"><span data-stu-id="d0d1b-121">hello cmdlet returns a confirmation tooshow hello session was connected successfully tooyour directory:</span></span>

    Account                       Environment Tenant
    -------                       ----------- ------
    Karen@drumkit.onmicrosoft.com AzureCloud  85b5ff1e-0402-400c-9e3c-0f…

<span data-ttu-id="d0d1b-122">Vous pouvez maintenant démarrer à l’aide de groupes de toomanage hello organisation applets de commande dans votre annuaire.</span><span class="sxs-lookup"><span data-stu-id="d0d1b-122">Now you can start using hello AzureAD cmdlets toomanage groups in your directory.</span></span>

## <a name="retrieving-groups"></a><span data-ttu-id="d0d1b-123">Récupération des groupes</span><span class="sxs-lookup"><span data-stu-id="d0d1b-123">Retrieving groups</span></span>
<span data-ttu-id="d0d1b-124">à partir de votre annuaire, que vous pouvez utiliser des groupes existants tooretrieve hello applet de commande Get-AzureADGroups.</span><span class="sxs-lookup"><span data-stu-id="d0d1b-124">tooretrieve existing groups from your directory you can use hello Get-AzureADGroups cmdlet.</span></span> <span data-ttu-id="d0d1b-125">tooretrieve tous les groupes dans le répertoire hello, utilisez hello applet de commande sans paramètres :</span><span class="sxs-lookup"><span data-stu-id="d0d1b-125">tooretrieve all groups in hello directory, use hello cmdlet without parameters:</span></span>

    PS C:\Windows\system32> get-azureadgroup

<span data-ttu-id="d0d1b-126">applet de commande Hello retourne tous les groupes dans l’annuaire connecté de hello.</span><span class="sxs-lookup"><span data-stu-id="d0d1b-126">hello cmdlet returns all groups in hello connected directory.</span></span>

<span data-ttu-id="d0d1b-127">Vous pouvez utiliser hello - objectID paramètre tooretrieve un groupe spécifique pour lequel vous spécifiez les objectID du groupe hello :</span><span class="sxs-lookup"><span data-stu-id="d0d1b-127">You can use hello -objectID parameter tooretrieve a specific group for which you specify hello group’s objectID:</span></span>

    PS C:\Windows\system32> get-azureadgroup -ObjectId e29bae11-4ac0-450c-bc37-6dae8f3da61b

<span data-ttu-id="d0d1b-128">applet de commande Hello retourne maintenant groupe hello dont objectID correspond à la valeur hello du paramètre hello que vous avez entré :</span><span class="sxs-lookup"><span data-stu-id="d0d1b-128">hello cmdlet now returns hello group whose objectID matches hello value of hello parameter you entered:</span></span>

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

<span data-ttu-id="d0d1b-129">Vous pouvez rechercher un groupe spécifique à l’aide de hello - paramètre de filtre.</span><span class="sxs-lookup"><span data-stu-id="d0d1b-129">You can search for a specific group using hello -filter parameter.</span></span> <span data-ttu-id="d0d1b-130">Ce paramètre accepte une clause de filtre ODATA et retourne tous les groupes qui correspondent au filtre hello, comme dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="d0d1b-130">This parameter takes an ODATA filter clause and returns all groups that match hello filter, as in hello following example:</span></span>

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
> <span data-ttu-id="d0d1b-131">Hello applets de commande PowerShell de AzureAD implémenter hello requête OData standard.</span><span class="sxs-lookup"><span data-stu-id="d0d1b-131">hello AzureAD PowerShell cmdlets implement hello OData query standard.</span></span> <span data-ttu-id="d0d1b-132">Pour plus d’informations, consultez **$filter** dans [options de requête système OData à l’aide du point de terminaison OData hello](https://msdn.microsoft.com/library/gg309461.aspx#BKMK_filter).</span><span class="sxs-lookup"><span data-stu-id="d0d1b-132">For more information, see **$filter** in [OData system query options using hello OData endpoint](https://msdn.microsoft.com/library/gg309461.aspx#BKMK_filter).</span></span>

## <a name="creating-groups"></a><span data-ttu-id="d0d1b-133">Création de groupes</span><span class="sxs-lookup"><span data-stu-id="d0d1b-133">Creating groups</span></span>
<span data-ttu-id="d0d1b-134">toocreate un nouveau groupe dans votre annuaire, l’applet de commande utilisez hello AzureADGroup de nouveau.</span><span class="sxs-lookup"><span data-stu-id="d0d1b-134">toocreate a new group in your directory, use hello New-AzureADGroup cmdlet.</span></span> <span data-ttu-id="d0d1b-135">Cette applet de commande crée un nouveau groupe de sécurité appelé « Marketing » :</span><span class="sxs-lookup"><span data-stu-id="d0d1b-135">This cmdlet creates a new security group called “Marketing":</span></span>

    PS C:\Windows\system32> New-AzureADGroup -Description "Marketing" -DisplayName "Marketing" -MailEnabled $false -SecurityEnabled $true -MailNickName "Marketing"

## <a name="updating-groups"></a><span data-ttu-id="d0d1b-136">Mise à jour des groupes</span><span class="sxs-lookup"><span data-stu-id="d0d1b-136">Updating groups</span></span>
<span data-ttu-id="d0d1b-137">tooupdate un groupe existant, utilisez l’applet de commande de hello AzureADGroup de jeu.</span><span class="sxs-lookup"><span data-stu-id="d0d1b-137">tooupdate an existing group, use hello Set-AzureADGroup cmdlet.</span></span> <span data-ttu-id="d0d1b-138">Dans cet exemple, nous passons hello DisplayName, propriété du groupe de hello « Administrateurs de Intune ».</span><span class="sxs-lookup"><span data-stu-id="d0d1b-138">In this example, we’re changing hello DisplayName property of hello group “Intune Administrators.”</span></span> <span data-ttu-id="d0d1b-139">Tout d’abord, nous avons observé groupe hello à l’aide d’applet de commande Get-AzureADGroup hello et filtre en utilisant l’attribut DisplayName de hello :</span><span class="sxs-lookup"><span data-stu-id="d0d1b-139">First, we’re finding hello group using hello Get-AzureADGroup cmdlet and filter using hello DisplayName attribute:</span></span>

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

<span data-ttu-id="d0d1b-140">Ensuite, nous passons hello Description toohello nouvelle valeur de la propriété « Administrateurs de l’appareil Intune » :</span><span class="sxs-lookup"><span data-stu-id="d0d1b-140">Next, we’re changing hello Description property toohello new value “Intune Device Administrators”:</span></span>

    PS C:\Windows\system32> Set-AzureADGroup -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -Description "Intune Device Administrators"

<span data-ttu-id="d0d1b-141">Maintenant si nous trouvons à nouveau groupe de hello, nous voyons de propriété de Description hello est mise à jour tooreflect hello nouvelle valeur :</span><span class="sxs-lookup"><span data-stu-id="d0d1b-141">Now if we find hello group again, we see hello Description property is updated tooreflect hello new value:</span></span>

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

## <a name="deleting-groups"></a><span data-ttu-id="d0d1b-142">Suppression de groupes</span><span class="sxs-lookup"><span data-stu-id="d0d1b-142">Deleting groups</span></span>
<span data-ttu-id="d0d1b-143">groupes de toodelete à partir de votre annuaire, utilisez applet de commande Remove-AzureADGroup hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="d0d1b-143">toodelete groups from your directory, use hello Remove-AzureADGroup cmdlet as follows:</span></span>

    PS C:\Windows\system32> Remove-AzureADGroup -ObjectId b11ca53e-07cc-455d-9a89-1fe3ab24566b

## <a name="managing-members-of-groups"></a><span data-ttu-id="d0d1b-144">Gestion des membres des groupes</span><span class="sxs-lookup"><span data-stu-id="d0d1b-144">Managing members of groups</span></span>
<span data-ttu-id="d0d1b-145">Si vous devez de nouveau groupe de tooa membres tooadd, utiliser l’applet de commande Add-AzureADGroupMember de hello.</span><span class="sxs-lookup"><span data-stu-id="d0d1b-145">If you need tooadd new members tooa group, use hello Add-AzureADGroupMember cmdlet.</span></span> <span data-ttu-id="d0d1b-146">Cette commande ajoute un groupe d’administrateurs Intune toohello membre que nous avons utilisé dans l’exemple précédent de hello :</span><span class="sxs-lookup"><span data-stu-id="d0d1b-146">This command adds a member toohello Intune Administrators group we used in hello previous example:</span></span>

    PS C:\Windows\system32> Add-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -RefObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

<span data-ttu-id="d0d1b-147">paramètre - ObjectId Hello est hello ObjectID de hello groupe toowhich nous souhaitons tooadd membre et hello ObjectID est hello - RefObjectId d’utilisateur de hello que vous souhaitez tooadd en tant que membre toohello groupe.</span><span class="sxs-lookup"><span data-stu-id="d0d1b-147">hello -ObjectId parameter is hello ObjectID of hello group toowhich we want tooadd a member, and hello -RefObjectId is hello ObjectID of hello user we want tooadd as a member toohello group.</span></span>

<span data-ttu-id="d0d1b-148">membres existants de hello tooget d’un groupe, utilisez la cmdlet Get-AzureADGroupMember de hello, comme dans cet exemple :</span><span class="sxs-lookup"><span data-stu-id="d0d1b-148">tooget hello existing members of a group, use hello Get-AzureADGroupMember cmdlet, as in this example:</span></span>

    PS C:\Windows\system32> Get-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df

    DeletionTimeStamp ObjectId                             ObjectType
    ----------------- --------                             ----------
                          72cd4bbd-2594-40a2-935c-016f3cfeeeea User
                          8120cc36-64b4-4080-a9e8-23aa98e8b34f User

<span data-ttu-id="d0d1b-149">membre de hello tooremove nous avons ajouté précédemment toohello groupe, utilisez hello Remove-AzureADGroupMember applet de commande, comme est indiqué ici :</span><span class="sxs-lookup"><span data-stu-id="d0d1b-149">tooremove hello member we previously added toohello group, use hello Remove-AzureADGroupMember cmdlet, as is shown here:</span></span>

    PS C:\Windows\system32> Remove-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -MemberId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

<span data-ttu-id="d0d1b-150">appartenances tooverify hello d’un utilisateur, utilisez l’applet de commande Select-AzureADGroupIdsUserIsMemberOf hello.</span><span class="sxs-lookup"><span data-stu-id="d0d1b-150">tooverify hello group membership(s) of a user, use hello Select-AzureADGroupIdsUserIsMemberOf cmdlet.</span></span> <span data-ttu-id="d0d1b-151">Cette applet de commande prend comme ses paramètres hello ObjectId de l’utilisateur de hello pour les membres du groupe toocheck hello et une liste de groupes pour les appartenances de hello toocheck.</span><span class="sxs-lookup"><span data-stu-id="d0d1b-151">This cmdlet takes as its parameters hello ObjectId of hello user for which toocheck hello group memberships, and a list of groups for which toocheck hello memberships.</span></span> <span data-ttu-id="d0d1b-152">liste Hello des groupes doit être fournie sous forme de hello d’une variable complexe de type « Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck », par conséquent, nous devons créons d’abord une variable avec ce type :</span><span class="sxs-lookup"><span data-stu-id="d0d1b-152">hello list of groups must be provided in hello form of a complex variable of type “Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck”, so we first must create a variable with that type:</span></span>

    PS C:\Windows\system32> $g = new-object Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck

<span data-ttu-id="d0d1b-153">Ensuite, nous fournissons des valeurs de toocheck les GroupID de hello dans l’attribut hello « Les GroupID » de cette variable complexe :</span><span class="sxs-lookup"><span data-stu-id="d0d1b-153">Next, we provide values for hello groupIds toocheck in hello attribute “GroupIds” of this complex variable:</span></span>

    PS C:\Windows\system32> $g.GroupIds = "b11ca53e-07cc-455d-9a89-1fe3ab24566b", "31f1ff6c-d48c-4f8a-b2e1-abca7fd399df"

<span data-ttu-id="d0d1b-154">Maintenant, si nous voulons appartenances toocheck hello d’un utilisateur avec 72cd4bbd-2594-40a2-935c-016f3cfeeeea ObjectID sur des groupes de hello dans $g, nous devons utiliser :</span><span class="sxs-lookup"><span data-stu-id="d0d1b-154">Now, if we want toocheck hello group memberships of a user with ObjectID 72cd4bbd-2594-40a2-935c-016f3cfeeeea against hello groups in $g, we should use:</span></span>

    PS C:\Windows\system32> Select-AzureADGroupIdsUserIsMemberOf -ObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea -GroupIdsForMembershipCheck $g

    OdataMetadata                                                                                                 Value
    -------------                                                                                                  -----
    https://graph.windows.net/85b5ff1e-0402-400c-9e3c-0f9e965325d1/$metadata#Collection(Edm.String)             {31f1ff6c-d48c-4f8a-b2e1-abca7fd399df}


<span data-ttu-id="d0d1b-155">valeur Hello retournée est une liste de groupes dont cet utilisateur est membre.</span><span class="sxs-lookup"><span data-stu-id="d0d1b-155">hello value returned is a list of groups of which this user is a member.</span></span> <span data-ttu-id="d0d1b-156">Vous pouvez également appliquer cette toocheck méthode appartenance Contacts, groupes ou principaux du Service pour obtenir la liste des groupes, à l’aide de Select-AzureADGroupIdsContactIsMemberOf, sélectionnez-AzureADGroupIdsGroupIsMemberOf donnée ou Sélectionnez-AzureADGroupIdsServicePrincipalIsMemberOf</span><span class="sxs-lookup"><span data-stu-id="d0d1b-156">You can also apply this method toocheck Contacts, Groups or Service Principals membership for a given list of groups, using Select-AzureADGroupIdsContactIsMemberOf, Select-AzureADGroupIdsGroupIsMemberOf or Select-AzureADGroupIdsServicePrincipalIsMemberOf</span></span>

## <a name="managing-owners-of-groups"></a><span data-ttu-id="d0d1b-157">Gestion des propriétaires de groupes</span><span class="sxs-lookup"><span data-stu-id="d0d1b-157">Managing owners of groups</span></span>
<span data-ttu-id="d0d1b-158">groupe du tooa tooadd propriétaires, utilisez hello Add-AzureADGroupOwner applet de commande :</span><span class="sxs-lookup"><span data-stu-id="d0d1b-158">tooadd owners tooa group, use hello Add-AzureADGroupOwner cmdlet:</span></span>

    PS C:\Windows\system32> Add-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -RefObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

<span data-ttu-id="d0d1b-159">paramètre - ObjectId Hello est hello ObjectID de hello groupe toowhich nous souhaitons tooadd un propriétaire et hello ObjectID est hello - RefObjectId d’utilisateur de hello que vous souhaitez tooadd en tant que propriétaire du groupe de hello.</span><span class="sxs-lookup"><span data-stu-id="d0d1b-159">hello -ObjectId parameter is hello ObjectID of hello group toowhich we want tooadd an owner, and hello -RefObjectId is hello ObjectID of hello user we want tooadd as an owner of hello group.</span></span>

<span data-ttu-id="d0d1b-160">propriétaires de hello tooretrieve d’un groupe, utilisez l’applet de commande Get-AzureADGroupOwner hello :</span><span class="sxs-lookup"><span data-stu-id="d0d1b-160">tooretrieve hello owners of a group, use hello Get-AzureADGroupOwner cmdlet:</span></span>

    PS C:\Windows\system32> Get-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df

<span data-ttu-id="d0d1b-161">applet de commande Hello retourne la liste hello des propriétaires de groupe spécifié de hello :</span><span class="sxs-lookup"><span data-stu-id="d0d1b-161">hello cmdlet returns hello list of owners for hello specified group:</span></span>

    DeletionTimeStamp ObjectId                             ObjectType
    ----------------- --------                             ----------
                          e831b3fd-77c9-49c7-9fca-de43e109ef67 User

<span data-ttu-id="d0d1b-162">Si vous voulez tooremove un propriétaire d’un groupe, utilisez l’applet de commande Remove-AzureADGroupOwner hello :</span><span class="sxs-lookup"><span data-stu-id="d0d1b-162">If you want tooremove an owner from a group, use hello Remove-AzureADGroupOwner cmdlet:</span></span>

    PS C:\Windows\system32> remove-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -OwnerId e831b3fd-77c9-49c7-9fca-de43e109ef67

## <a name="reserved-aliases"></a><span data-ttu-id="d0d1b-163">Alias réservés</span><span class="sxs-lookup"><span data-stu-id="d0d1b-163">Reserved aliases</span></span> 
<span data-ttu-id="d0d1b-164">Lors de la création d’un groupe, certains points de terminaison autorisent hello utilisateur final toospecify un toobe mailNickname ou l’alias utilisé dans le cadre de l’adresse de messagerie hello du groupe de hello.</span><span class="sxs-lookup"><span data-stu-id="d0d1b-164">When a group is created, certain endpoints allow hello end user toospecify a mailNickname or alias toobe used as part of hello email address of hello group.</span></span> <span data-ttu-id="d0d1b-165">Groupes avec hello suivant des alias de messagerie hautement privilégiés peuvent uniquement être créés par un administrateur global Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d0d1b-165">Groups with hello following highly privileged email aliases can only be created by an Azure AD global administrator.</span></span> 
  
* <span data-ttu-id="d0d1b-166">abuse</span><span class="sxs-lookup"><span data-stu-id="d0d1b-166">abuse</span></span> 
* <span data-ttu-id="d0d1b-167">admin</span><span class="sxs-lookup"><span data-stu-id="d0d1b-167">admin</span></span> 
* <span data-ttu-id="d0d1b-168">administrator</span><span class="sxs-lookup"><span data-stu-id="d0d1b-168">administrator</span></span> 
* <span data-ttu-id="d0d1b-169">hostmaster</span><span class="sxs-lookup"><span data-stu-id="d0d1b-169">hostmaster</span></span> 
* <span data-ttu-id="d0d1b-170">majordomo</span><span class="sxs-lookup"><span data-stu-id="d0d1b-170">majordomo</span></span> 
* <span data-ttu-id="d0d1b-171">postmaster</span><span class="sxs-lookup"><span data-stu-id="d0d1b-171">postmaster</span></span> 
* <span data-ttu-id="d0d1b-172">root</span><span class="sxs-lookup"><span data-stu-id="d0d1b-172">root</span></span> 
* <span data-ttu-id="d0d1b-173">secure</span><span class="sxs-lookup"><span data-stu-id="d0d1b-173">secure</span></span> 
* <span data-ttu-id="d0d1b-174">security</span><span class="sxs-lookup"><span data-stu-id="d0d1b-174">security</span></span> 
* <span data-ttu-id="d0d1b-175">ssl-admin</span><span class="sxs-lookup"><span data-stu-id="d0d1b-175">ssl-admin</span></span> 
* <span data-ttu-id="d0d1b-176">webmaster</span><span class="sxs-lookup"><span data-stu-id="d0d1b-176">webmaster</span></span> 

## <a name="next-steps"></a><span data-ttu-id="d0d1b-177">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d0d1b-177">Next steps</span></span>
<span data-ttu-id="d0d1b-178">Vous trouverez plus d’informations sur Azure Active Directory PowerShell dans la page dédiée aux [applets de commande Azure Active Directory](/powershell/azure/install-adv2?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="d0d1b-178">You can find more Azure Active Directory PowerShell documentation at [Azure Active Directory Cmdlets](/powershell/azure/install-adv2?view=azureadps-2.0).</span></span>

* [<span data-ttu-id="d0d1b-179">La gestion des accès tooresources avec les groupes Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d0d1b-179">Managing access tooresources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="d0d1b-180">Intégration de vos identités locales avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d0d1b-180">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
