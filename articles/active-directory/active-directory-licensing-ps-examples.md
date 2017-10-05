---
title: "Exemples PowerShell pour les licences basées sur les groupes dans Azure AD | Microsoft Docs"
description: "Scénarios PowerShell pour la licence basée sur le groupe Azure Active Directory"
services: active-directory
keywords: Gestion des licences Azure AD
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/05/2017
ms.author: curtand
ms.openlocfilehash: b561dd29faff63d4898f351b2c9a39d359b89539
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="powershell-examples-for-group-based-licensing-in-azure-ad"></a><span data-ttu-id="e100c-104">Exemples PowerShell pour les licences basées sur les groupes dans Azure AD</span><span class="sxs-lookup"><span data-stu-id="e100c-104">PowerShell examples for group-based licensing in Azure AD</span></span>

<span data-ttu-id="e100c-105">Toutes les fonctionnalités pour l’affectation de licences basée sur les groupes sont disponibles via le [portail Azure](https://portal.azure.com), et la prise en charge de PowerShell est actuellement limitée.</span><span class="sxs-lookup"><span data-stu-id="e100c-105">Full functionality for group-based licensing is available through the [Azure portal](https://portal.azure.com), and currently PowerShell support is limited.</span></span> <span data-ttu-id="e100c-106">Toutefois, il existe certaines tâches utiles qui peuvent être effectuées à l’aide des [applets de commande MSOnline PowerShell](https://docs.microsoft.com/powershell/msonline/v1/azureactivedirectory).</span><span class="sxs-lookup"><span data-stu-id="e100c-106">However, there are some useful tasks that can be performed using the existing [MSOnline PowerShell cmdlets](https://docs.microsoft.com/powershell/msonline/v1/azureactivedirectory).</span></span> <span data-ttu-id="e100c-107">Ce document fournit des exemples de ce qui est possible.</span><span class="sxs-lookup"><span data-stu-id="e100c-107">This document provides examples of what is possible.</span></span>

> [!NOTE]
> <span data-ttu-id="e100c-108">Avant de commencer à exécuter les applets de commande, veillez d’abord à vous connecter à votre client en exécutant l’applet de commande `Connect-MsolService`.</span><span class="sxs-lookup"><span data-stu-id="e100c-108">Before you begin running cmdlets, make sure you connect to your tenant first, by running the `Connect-MsolService` cmdlet.</span></span>

## <a name="view-product-licenses-assigned-to-a-group"></a><span data-ttu-id="e100c-109">Afficher les licences de produit attribuées à un groupe</span><span class="sxs-lookup"><span data-stu-id="e100c-109">View product licenses assigned to a group</span></span>
<span data-ttu-id="e100c-110">L’applet de commande [Get-MsolGroup](/powershell/module/msonline/get-msolgroup?view=azureadps-1.0) peut être utilisé pour récupérer l’objet de groupe et vérifier la propriété *Licences* : elle répertorie toutes les licences de produit actuellement affectées au groupe.</span><span class="sxs-lookup"><span data-stu-id="e100c-110">The [Get-MsolGroup](/powershell/module/msonline/get-msolgroup?view=azureadps-1.0) cmdlet can be used to retrieve the group object and check the *Licenses* property: it lists all product licenses currently assigned to the group.</span></span>
```
(Get-MsolGroup -ObjectId 99c4216a-56de-42c4-a4ac-e411cd8c7c41).Licenses
| Select SkuPartNumber
```
<span data-ttu-id="e100c-111">Output:</span><span class="sxs-lookup"><span data-stu-id="e100c-111">Output:</span></span>
```
SkuPartNumber
-------------
ENTERPRISEPREMIUM
EMSPREMIUM
```

> [!NOTE]
> <span data-ttu-id="e100c-112">Les données sont limitées aux informations liées au produit (SKU).</span><span class="sxs-lookup"><span data-stu-id="e100c-112">The data is limited to product (SKU) information.</span></span> <span data-ttu-id="e100c-113">Il n’est pas possible de répertorier les plans de service désactivés dans la licence.</span><span class="sxs-lookup"><span data-stu-id="e100c-113">It is not possible to list the service plans disabled in the license.</span></span>

## <a name="get-all-groups-with-licenses"></a><span data-ttu-id="e100c-114">Obtenir tous les groupes avec des licences</span><span class="sxs-lookup"><span data-stu-id="e100c-114">Get all groups with licenses</span></span>

<span data-ttu-id="e100c-115">Vous trouverez tous les groupes avec une licence affectée en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="e100c-115">You can find all groups with any license assigned by running the following command:</span></span>
```
Get-MsolGroup | Where {$_.Licenses}
```
<span data-ttu-id="e100c-116">Vous pouvez afficher plus de détails sur les produits affectés :</span><span class="sxs-lookup"><span data-stu-id="e100c-116">More details can be displayed about what products are assigned:</span></span>
```
Get-MsolGroup | Where {$_.Licenses} | Select `
    ObjectId, `
    DisplayName, `
    @{Name="Licenses";Expression={$_.Licenses | Select -ExpandProperty SkuPartNumber}}
```

<span data-ttu-id="e100c-117">Output:</span><span class="sxs-lookup"><span data-stu-id="e100c-117">Output:</span></span>
```
ObjectId                             DisplayName              Licenses
--------                             -----------              --------
7023a314-6148-4d7b-b33f-6c775572879a EMS E5 – Licensed users  EMSPREMIUM
cf41f428-3b45-490b-b69f-a349c8a4c38e PowerBi - Licensed users POWER\_BI\_STANDARD
962f7189-59d9-4a29-983f-556ae56f19a5 O365 E3 - Licensed users ENTERPRISEPACK
c2652d63-9161-439b-b74e-fcd8228a7074 EMSandOffice             {ENTERPRISEPREMIUM,EMSPREMIUM}
```

## <a name="get-statistics-for-groups-with-licenses"></a><span data-ttu-id="e100c-118">Obtenir des statistiques sur les groupes avec des licences</span><span class="sxs-lookup"><span data-stu-id="e100c-118">Get statistics for groups with licenses</span></span>
<span data-ttu-id="e100c-119">Vous pouvez rapporter des statistiques de base sur les groupes avec des licences.</span><span class="sxs-lookup"><span data-stu-id="e100c-119">You can report basic statistics for groups with licenses.</span></span> <span data-ttu-id="e100c-120">Dans l’exemple ci-dessous, nous indiquons le nombre total d’utilisateurs, le nombre d’utilisateurs ayant déjà des licences attribuées par le groupe et le nombre d’utilisateurs pour lesquels des licences n’ont pas pu être affectées par le groupe.</span><span class="sxs-lookup"><span data-stu-id="e100c-120">In the example below we list the total user count, the count of users with licenses already assigned by the group, and the count of users for whom licenses could not be assigned by the group.</span></span>

```
#get all groups with licenses
Get-MsolGroup -All | Where {$_.Licenses}  | Foreach {
    $groupId = $_.ObjectId;
    $groupName = $_.DisplayName;
    $groupLicenses = $_.Licenses | Select -ExpandProperty SkuPartNumber
    $totalCount = 0;
    $licenseAssignedCount = 0;
    $licenseErrorCount = 0;

    Get-MsolGroupMember -All -GroupObjectId $groupId |
    #get full info about each user in the group
    Get-MsolUser -ObjectId {$_.ObjectId} |
    Foreach {
        $user = $_;
        $totalCount++

        #check if any licenses are assigned via this group
        if($user.Licenses | ? {$_.GroupsAssigningLicense -ieq $groupId })
        {
            $licenseAssignedCount++
        }
        #check if user has any licenses that failed to be assigned from this group
        if ($user.IndirectLicenseErrors | ? {$_.ReferencedObjectId -ieq $groupId })
        {
            $licenseErrorCount++
        }     
    }

    #aggregate results for this group
    New-Object Object |
                    Add-Member -NotePropertyName GroupName -NotePropertyValue $groupName -PassThru |
                    Add-Member -NotePropertyName GroupId -NotePropertyValue $groupId -PassThru |
                    Add-Member -NotePropertyName GroupLicenses -NotePropertyValue $groupLicenses -PassThru |
                    Add-Member -NotePropertyName TotalUserCount -NotePropertyValue $totalCount -PassThru |
                    Add-Member -NotePropertyName LicensedUserCount -NotePropertyValue $licenseAssignedCount -PassThru |
                    Add-Member -NotePropertyName LicenseErrorCount -NotePropertyValue $licenseErrorCount -PassThru

    } | Format-Table
```


<span data-ttu-id="e100c-121">Output:</span><span class="sxs-lookup"><span data-stu-id="e100c-121">Output:</span></span>
```
GroupName         GroupId                              GroupLicenses       TotalUserCount LicensedUserCount LicenseErrorCount
---------         -------                              -------------       -------------- ----------------- -----------------
Dynamics Licen... 9160c903-9f91-4597-8f79-22b6c47eafbf AAD_PREMIUM_P2                   0                 0                 0
O365 E5 - base... 055dcca3-fb75-4398-a1b8-f8c6f4c24e65 ENTERPRISEPREMIUM                2                 2                 0
O365 E5 - extr... 6b14a1fe-c3a9-4786-9ee4-3a2bb54dcb8e ENTERPRISEPREMIUM                3                 3                 0
EMS E5 - all s... 7023a314-6148-4d7b-b33f-6c775572879a EMSPREMIUM                       2                 2                 0
PowerBi - Lice... cf41f428-3b45-490b-b69f-a349c8a4c38e POWER_BI_STANDARD                2                 2                 0
O365 E3 - all ... 962f7189-59d9-4a29-983f-556ae56f19a5 ENTERPRISEPACK                   2                 2                 0
O365 E5 - EXO     102fb8f4-bbe7-462b-83ff-2145e7cdd6ed ENTERPRISEPREMIUM                1                 1                 0
Access to Offi... 11151866-5419-4d93-9141-0603bbf78b42 STANDARDPACK                     4                 3                 1
```

## <a name="get-all-groups-with-license-errors"></a><span data-ttu-id="e100c-122">Obtenir tous les groupes avec des erreurs de licence</span><span class="sxs-lookup"><span data-stu-id="e100c-122">Get all groups with license errors</span></span>
<span data-ttu-id="e100c-123">Pour rechercher les groupes qui contiennent des utilisateurs pour lesquels des licences n’ont pas pu être affectées :</span><span class="sxs-lookup"><span data-stu-id="e100c-123">To find groups that contain some users for whom licenses could not be assigned:</span></span>
```
Get-MsolGroup -HasLicenseErrorsOnly $true
```
<span data-ttu-id="e100c-124">Output:</span><span class="sxs-lookup"><span data-stu-id="e100c-124">Output:</span></span>
```
ObjectId                             DisplayName             GroupType Description
--------                             -----------             --------- -----------
11151866-5419-4d93-9141-0603bbf78b42 Access to Office 365 E1 Security  Users who should have E1 licenses
```
## <a name="get-all-users-with-license-errors-in-a-group"></a><span data-ttu-id="e100c-125">Obtenir tous les utilisateurs avec des erreurs de licence dans un groupe</span><span class="sxs-lookup"><span data-stu-id="e100c-125">Get all users with license errors in a group</span></span>

<span data-ttu-id="e100c-126">Pour un groupe contenant des erreurs liées aux licences, vous pouvez maintenant répertorier tous les utilisateurs affectés par ces erreurs.</span><span class="sxs-lookup"><span data-stu-id="e100c-126">Given a group that contains some license related errors, you can now list all users affected by those errors.</span></span> <span data-ttu-id="e100c-127">Un utilisateur peut aussi avoir des erreurs d’autres groupes.</span><span class="sxs-lookup"><span data-stu-id="e100c-127">A jser can have errors from other groups, too.</span></span> <span data-ttu-id="e100c-128">Toutefois, dans cet exemple, nous limitons les résultats uniquement aux erreurs pertinentes au groupe en question en cochant la propriété **ReferencedObjectId** de chaque entrée **IndirectLicenseError** sur l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="e100c-128">However, in this example we limit results only to errors relevant to the group in question by checking the **ReferencedObjectId** property of each **IndirectLicenseError** entry on the user.</span></span>

```
#a sample group with errors
$groupId = '11151866-5419-4d93-9141-0603bbf78b42'

#get all user members of the group
Get-MsolGroupMember -All -GroupObjectId $groupId |
    #get full information about user objects
    Get-MsolUser -ObjectId {$_.ObjectId} |
    #filter out users without license errors and users with licenense errors from other groups
    Where {$_.IndirectLicenseErrors -and $_.IndirectLicenseErrors.ReferencedObjectId -eq $groupId} |
    #display id, name and error detail. Note: we are filtering out license errors from other groups
    Select ObjectId, `
           DisplayName, `
           @{Name="LicenseError";Expression={$_.IndirectLicenseErrors | Where {$_.ReferencedObjectId -eq $groupId} | Select -ExpandProperty Error}}
```

<span data-ttu-id="e100c-129">Output:</span><span class="sxs-lookup"><span data-stu-id="e100c-129">Output:</span></span>
```
ObjectId                             DisplayName      License Error
--------                             -----------      ------------
6d325baf-22b7-46fa-a2fc-a2500613ca15 Catherine Gibson MutuallyExclusiveViolation
```
## <a name="get-all-users-with-license-errors-in-the-entire-tenant"></a><span data-ttu-id="e100c-130">Obtenir tous les utilisateurs avec des erreurs de licence dans le client entier</span><span class="sxs-lookup"><span data-stu-id="e100c-130">Get all users with license errors in the entire tenant</span></span>

<span data-ttu-id="e100c-131">Pour répertorier tous les utilisateurs qui ont des erreurs de licence à partir d’un ou plusieurs groupes, le script suivant peut être utilisé.</span><span class="sxs-lookup"><span data-stu-id="e100c-131">To list all users who have license errors from one or more groups, the following script can be used.</span></span> <span data-ttu-id="e100c-132">Ce script répertoriera une ligne par utilisateur et par erreur de licence, ce qui vous permet d’identifier clairement la source de chaque erreur.</span><span class="sxs-lookup"><span data-stu-id="e100c-132">This script will list one row per user, per license error which allows you to clearly identify the source of each error.</span></span>

> [!NOTE]
> <span data-ttu-id="e100c-133">Ce script énumère tous les utilisateurs dans le client, ce qui peut ne pas être optimal pour les locataires volumineux.</span><span class="sxs-lookup"><span data-stu-id="e100c-133">This script will enumerate all users in the tenant, which might not be optimal for large tenants.</span></span>

```
Get-MsolUser -All | Where {$_.IndirectLicenseErrors } | % {   
    $user = $_;
    $user.IndirectLicenseErrors | % {
            New-Object Object |
                Add-Member -NotePropertyName UserName -NotePropertyValue $user.DisplayName -PassThru |
                Add-Member -NotePropertyName UserId -NotePropertyValue $user.ObjectId -PassThru |
                Add-Member -NotePropertyName GroupId -NotePropertyValue $_.ReferencedObjectId -PassThru |
                Add-Member -NotePropertyName LicenseError -NotePropertyValue $_.Error -PassThru
        }
    }  
```

<span data-ttu-id="e100c-134">Output:</span><span class="sxs-lookup"><span data-stu-id="e100c-134">Output:</span></span>

```
UserName         UserId                               GroupId                              LicenseError
--------         ------                               -------                              ------------
Anna Bergman     0d0fd16d-872d-4e87-b0fb-83c610db12bc 7946137d-b00d-4336-975e-b1b81b0666d0 MutuallyExclusiveViolation
Catherine Gibson 6d325baf-22b7-46fa-a2fc-a2500613ca15 f2503e79-0edc-4253-8bed-3e158366466b CountViolation
Catherine Gibson 6d325baf-22b7-46fa-a2fc-a2500613ca15 11151866-5419-4d93-9141-0603bbf78b42 MutuallyExclusiveViolation
Drew Fogarty     f2af28fc-db0b-4909-873d-ddd2ab1fd58c 1ebd5028-6092-41d0-9668-129a3c471332 MutuallyExclusiveViolation
```

<span data-ttu-id="e100c-135">Voici une autre version du script qui effectue une recherche uniquement dans les groupes qui contiennent des erreurs de licence.</span><span class="sxs-lookup"><span data-stu-id="e100c-135">Here is another version of the script that searches only through groups that contain license errors.</span></span> <span data-ttu-id="e100c-136">Elle peut être davantage optimisée pour les scénarios où vous prévoyez d’avoir plusieurs groupes avec des problèmes.</span><span class="sxs-lookup"><span data-stu-id="e100c-136">It may be more optimized for scenarios where you expect to have few groups with problems.</span></span>

```
Get-MsolUser -All | Where {$_.IndirectLicenseErrors } | % {   
    $user = $_;
    $user.IndirectLicenseErrors | % {
            New-Object Object |
                Add-Member -NotePropertyName UserName -NotePropertyValue $user.DisplayName -PassThru |
                Add-Member -NotePropertyName UserId -NotePropertyValue $user.ObjectId -PassThru |
                Add-Member -NotePropertyName GroupId -NotePropertyValue $_.ReferencedObjectId -PassThru |
                Add-Member -NotePropertyName LicenseError -NotePropertyValue $_.Error -PassThru
        }
    }
```

## <a name="check-if-user-license-is-assigned-directly-or-inherited-from-a-group"></a><span data-ttu-id="e100c-137">Vérifier si les licences utilisateur sont directement affectées ou héritées d’un groupe</span><span class="sxs-lookup"><span data-stu-id="e100c-137">Check if user license is assigned directly or inherited from a group</span></span>

<span data-ttu-id="e100c-138">Pour un objet utilisateur, il est possible de vérifier si une licence de produit spécifique est affectée à partir d’un groupe ou si elle est directement affectée.</span><span class="sxs-lookup"><span data-stu-id="e100c-138">For a user object it is possible to check if a particular product license is assigned from a group or if it is assigned directly.</span></span>

<span data-ttu-id="e100c-139">Les deux exemples de fonctions ci-dessous peuvent être utilisés pour analyser le type d’affectation sur un utilisateur individuel :</span><span class="sxs-lookup"><span data-stu-id="e100c-139">The two sample functions below can be used to analyze the type of assignment on an individual user:</span></span>
```
#Returns TRUE if the user has the license assigned directly
function UserHasLicenseAssignedDirectly
{
    Param([Microsoft.Online.Administration.User]$user, [string]$skuId)

    foreach($license in $user.Licenses)
    {
        #we look for the specific license SKU in all licenses assigned to the user
        if ($license.AccountSkuId -ieq $skuId)
        {
            #GroupsAssigningLicense contains a collection of IDs of objects assigning the license
            #This could be a group object or a user object (contrary to what the name suggests)
            #If the collection is empty, this means the license is assigned directly - this is the case for users who have never been licensed via groups in the past
            if ($license.GroupsAssigningLicense.Count -eq 0)
            {
                return $true
            }

            #If the collection contains the ID of the user object, this means the license is assigned directly
            #Note: the license may also be assigned through one or more groups in addition to being assigned directly
            foreach ($assignmentSource in $license.GroupsAssigningLicense)
            {
                if ($assignmentSource -ieq $user.ObjectId)
                {
                    return $true
                }
            }
            return $false
        }
    }
    return $false
}
#Returns TRUE if the user is inheriting the license from a group
function UserHasLicenseAssignedFromGroup
{
    Param([Microsoft.Online.Administration.User]$user, [string]$skuId)

    foreach($license in $user.Licenses)
    {
        #we look for the specific license SKU in all licenses assigned to the user
        if ($license.AccountSkuId -ieq $skuId)
        {
            #GroupsAssigningLicense contains a collection of IDs of objects assigning the license
            #This could be a group object or a user object (contrary to what the name suggests)
            foreach ($assignmentSource in $license.GroupsAssigningLicense)
            {
                #If the collection contains at least one ID not matching the user ID this means that the license is inherited from a group.
                #Note: the license may also be assigned directly in addition to being inherited
                if ($assignmentSource -ine $user.ObjectId)
                {
                    return $true
                }
            }
            return $false
        }
    }
    return $false
}
```

<span data-ttu-id="e100c-140">Ce script exécute ces fonctions sur chaque utilisateur dans le locataire, à l’aide de l’ID de référence SKU en tant qu’entrée : dans cet exemple, nous nous intéressons à la licence pour *Enterprise Mobility + Security*, qui, dans notre locataire, est représentée par l’ID *contoso:EMS*:</span><span class="sxs-lookup"><span data-stu-id="e100c-140">This script executes those functions on each user in the tenant, using the SKU ID as input - in this example we are interested in the license for *Enterprise Mobility + Security*, which in our tenant is represented with ID *contoso:EMS*:</span></span>
```
#the license SKU we are interested in. use Msol-GetAccountSku to see a list of all identifiers in your tenant
$skuId = "contoso:EMS"

#find all users that have the SKU license assigned
Get-MsolUser -All | where {$_.isLicensed -eq $true -and $_.Licenses.AccountSKUID -eq $skuId} | select `
    ObjectId, `
    @{Name="SkuId";Expression={$skuId}}, `
    @{Name="AssignedDirectly";Expression={(UserHasLicenseAssignedDirectly $_ $skuId)}}, `
    @{Name="AssignedFromGroup";Expression={(UserHasLicenseAssignedFromGroup $_ $skuId)}}
```

<span data-ttu-id="e100c-141">Output:</span><span class="sxs-lookup"><span data-stu-id="e100c-141">Output:</span></span>
```
ObjectId                             SkuId       AssignedDirectly AssignedFromGroup
--------                             -----       ---------------- -----------------
157870f6-e050-4b3c-ad5e-0f0a377c8f4d contoso:EMS             True             False
1f3174e2-ee9d-49e9-b917-e8d84650f895 contoso:EMS            False              True
240622ac-b9b8-4d50-94e2-dad19a3bf4b5 contoso:EMS             True              True
```

## <a name="remove-direct-licenses-for-users-with-group-licenses"></a><span data-ttu-id="e100c-142">Suppression des licences directes pour les utilisateurs avec des licences de groupe</span><span class="sxs-lookup"><span data-stu-id="e100c-142">Remove direct licenses for users with group licenses</span></span>
<span data-ttu-id="e100c-143">L’objectif de ce script consiste à supprimer les licences directes inutiles des utilisateurs qui héritent déjà de la même licence auprès d’un groupe ; par exemple, dans le cadre d’une [transition vers l’affectation de licences basée sur les groupes](https://docs.microsoft.com/azure/active-directory/active-directory-licensing-group-migration-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="e100c-143">The purpose of this script is to remove unnecessary direct licenses from users who already inherit the same license from a group; for example, as part of a [transitioning to group-based licensing](https://docs.microsoft.com/azure/active-directory/active-directory-licensing-group-migration-azure-portal).</span></span>
> [!NOTE]
> <span data-ttu-id="e100c-144">Il est important de commencer par confirmer que les licences directes à supprimer n’activent pas davantage de fonctionnalités de service que les licences héritées.</span><span class="sxs-lookup"><span data-stu-id="e100c-144">It is important to first validate that the direct licenses to be removed do not enable more service functionality than the inherited licenses.</span></span> <span data-ttu-id="e100c-145">Dans le cas contraire, la suppression de la licence directe peut désactiver l’accès aux services et données pour les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="e100c-145">Otherwise, removing the direct license may disable access to services and data for users.</span></span> <span data-ttu-id="e100c-146">Actuellement, il n’est pas possible de vérifier avec PowerShell les services qui sont activés par licence héritée et ceux qui le sont pas licence directe.</span><span class="sxs-lookup"><span data-stu-id="e100c-146">Currently it is not possible to check via PowerShell which services are enabled via inherited licenses vs direct.</span></span> <span data-ttu-id="e100c-147">Dans le script, nous allons spécifier le niveau minimal de services dont nous savons qu’ils héritent de groupes, et nous allons effectuer la vérification par rapport à cette valeur.</span><span class="sxs-lookup"><span data-stu-id="e100c-147">In the script we will specify the minimum level of services we know are being inherited from groups and we will check against that.</span></span>

```
#BEGIN: Helper functions used by the script

#Returns TRUE if the user has the license assigned directly
function UserHasLicenseAssignedDirectly
{
    Param([Microsoft.Online.Administration.User]$user, [string]$skuId)

    $license = GetUserLicense $user $skuId

    if ($license -ne $null)
    {
        #GroupsAssigningLicense contains a collection of IDs of objects assigning the license
        #This could be a group object or a user object (contrary to what the name suggests)
        #If the collection is empty, this means the license is assigned directly - this is the case for users who have never been licensed via groups in the past
        if ($license.GroupsAssigningLicense.Count -eq 0)
        {
            return $true
        }

        #If the collection contains the ID of the user object, this means the license is assigned directly
        #Note: the license may also be assigned through one or more groups in addition to being assigned directly
        foreach ($assignmentSource in $license.GroupsAssigningLicense)
        {
            if ($assignmentSource -ieq $user.ObjectId)
            {
                return $true
            }
        }
        return $false
    }
    return $false
}
#Returns TRUE if the user is inheriting the license from a specific group
function UserHasLicenseAssignedFromThisGroup
{
    Param([Microsoft.Online.Administration.User]$user, [string]$skuId, [Guid]$groupId)

    $license = GetUserLicense $user $skuId

    if ($license -ne $null)
    {
        #GroupsAssigningLicense contains a collection of IDs of objects assigning the license
        #This could be a group object or a user object (contrary to what the name suggests)
        foreach ($assignmentSource in $license.GroupsAssigningLicense)
        {
            #If the collection contains at least one ID not matching the user ID this means that the license is inherited from a group.
            #Note: the license may also be assigned directly in addition to being inherited
            if ($assignmentSource -ieq $groupId)
            {
                return $true
            }
        }
        return $false
    }
    return $false
}

#Returns the license object corresponding to the skuId. Returns NULL if not found
function GetUserLicense
{
    Param([Microsoft.Online.Administration.User]$user, [string]$skuId, [Guid]$groupId)
    #we look for the specific license SKU in all licenses assigned to the user
    foreach($license in $user.Licenses)
    {
        if ($license.AccountSkuId -ieq $skuId)
        {
            return $license
        }
    }
    return $null
}

#produces a list of disabled service plan names for a set of plans we want to leave enabled
function GetDisabledPlansForSKU
{
    Param([string]$skuId, [string[]]$enabledPlans)

    $allPlans = Get-MsolAccountSku | where {$_.AccountSkuId -ieq $skuId} | Select -ExpandProperty ServiceStatus | Where {$_.ProvisioningStatus -ieq "PendingActivation"} | Select -ExpandProperty ServicePlan | Select -ExpandProperty ServiceName
    $disabledPlans = $allPlans | Where {$enabledPlans -inotcontains $_}

    return $disabledPlans
}

function GetUnexpectedEnabledPlansForUser
{
    Param([Microsoft.Online.Administration.User]$user, [string]$skuId, [string[]]$expectedDisabledPlans)

    $license = GetUserLicense $user $skuId

    $extraPlans = @();

    if($license -ne $null)
    {
        $userDisabledPlans = $license.ServiceStatus | where {$_.ProvisioningStatus -ieq "Disabled"} | Select -ExpandProperty ServicePlan | Select -ExpandProperty ServiceName

        $extraPlans = $expectedDisabledPlans | where {$userDisabledPlans -notcontains $_}
    }
    return $extraPlans
}
#END: helper functions

#BEGIN: executing the script
#the group to be processed
$groupId = "48ca647b-7e4d-41e5-aa66-40cab1e19101"

#license to be removed - Office 365 E3
$skuId = "contoso:ENTERPRISEPACK"

#minimum set of service plans we know are inherited from groups - we want to make sure that there aren't any users who have more services enabled
#which could mean that they may lose access after we remove direct licenses
$servicePlansFromGroups = ("EXCHANGE_S_ENTERPRISE", "SHAREPOINTENTERPRISE", "OFFICESUBSCRIPTION")

$expectedDisabledPlans = GetDisabledPlansForSKU $skuId $servicePlansFromGroups

#process all members in the group
Get-MsolGroupMember -All -GroupObjectId $groupId |
    #get full info about each user in the group
    Get-MsolUser -ObjectId {$_.ObjectId} |
    Foreach {
        $user = $_;
        $operationResult = "";

        #check if Direct license exists on the user
        if (UserHasLicenseAssignedDirectly $user $skuId)
        {
            #check if the license is assigned from this group, as expected
            if (UserHasLicenseAssignedFromThisGroup $user $skuId $groupId)
            {
                #check if there are any extra plans we didn't expect - we are being extra careful not to remove unexpected services
                $extraPlans = GetUnexpectedEnabledPlansForUser $user $skuId $expectedDisabledPlans
                if ($extraPlans.Count -gt 0)
                {
                    $operationResult = "User has extra plans that may be lost - license removal was skipped. Extra plans: $extraPlans"
                }
                else
                {
                    #remove the direct license from user
                    Set-MsolUserLicense -ObjectId $user.ObjectId -RemoveLicenses $skuId
                    $operationResult = "Removed direct license from user."   
                }

            }
            else
            {
                $operationResult = "User does not inherit this license from this group. License removal was skipped."
            }
        }
        else
        {
            $operationResult = "User has no direct license to remove. Skipping."
        }

        #format output
        New-Object Object |
                    Add-Member -NotePropertyName UserId -NotePropertyValue $user.ObjectId -PassThru |
                    Add-Member -NotePropertyName OperationResult -NotePropertyValue $operationResult -PassThru
    } | Format-Table
#END: executing the script
```

<span data-ttu-id="e100c-148">Output:</span><span class="sxs-lookup"><span data-stu-id="e100c-148">Output:</span></span>
```
UserId                               OperationResult                                                                                
------                               ---------------                                                                                
7c7f860f-700a-462a-826c-f50633931362 Removed direct license from user.                                                              
0ddacdd5-0364-477d-9e4b-07eb6cdbc8ea User has extra plans that may be lost - license removal was skipped. Extra plans: SHAREPOINTWAC
aadbe4da-c4b5-4d84-800a-9400f31d7371 User has no direct license to remove. Skipping.                                                
```

## <a name="next-steps"></a><span data-ttu-id="e100c-149">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e100c-149">Next steps</span></span>

<span data-ttu-id="e100c-150">Pour plus d’informations sur l’ensemble de fonctionnalités de gestion des licences par le biais des groupes, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="e100c-150">To learn more about the feature set for license management through groups, see the following:</span></span>

* [<span data-ttu-id="e100c-151">What is group-based licensing in Azure Active Directory? (Présentation des licences basées sur le groupe dans Azure Active Directory)</span><span class="sxs-lookup"><span data-stu-id="e100c-151">What is group-based licensing in Azure Active Directory?</span></span>](active-directory-licensing-whatis-azure-portal.md)
* [<span data-ttu-id="e100c-152">Affectation de licences à un groupe dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e100c-152">Assigning licenses to a group in Azure Active Directory</span></span>](active-directory-licensing-group-assignment-azure-portal.md)
* [<span data-ttu-id="e100c-153">Identification et résolution des problèmes de licence pour un groupe dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e100c-153">Identifying and resolving license problems for a group in Azure Active Directory</span></span>](active-directory-licensing-group-problem-resolution-azure-portal.md)
* [<span data-ttu-id="e100c-154">Migration des utilisateurs individuels sous licence vers les licences basées sur les groupes dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e100c-154">How to migrate individual licensed users to group-based licensing in Azure Active Directory</span></span>](active-directory-licensing-group-migration-azure-portal.md)
* [<span data-ttu-id="e100c-155">Autres scénarios de licences basées sur les groupes Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e100c-155">Azure Active Directory group-based licensing additional scenarios</span></span>](active-directory-licensing-group-advanced.md)
