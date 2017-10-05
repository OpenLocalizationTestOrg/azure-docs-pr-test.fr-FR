---
title: "Référence d’API d’audit Azure Active Directory | Microsoft Docs"
description: "Prise en main de l’API d’audit Azure Active Directory"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 44e46be8-09e5-4981-be2b-d474aaa92792
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/05/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 573e940c5390e7b990d889681eb37b73c5b253d9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-audit-api-reference"></a><span data-ttu-id="623bd-103">Référence d’API d’audit Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="623bd-103">Azure Active Directory audit API reference</span></span>
<span data-ttu-id="623bd-104">Cette rubrique fait partie d’un ensemble de rubriques relatives à l’API de création de rapports Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="623bd-104">This topic is part of a collection of topics about the Azure Active Directory reporting API.</span></span>  
<span data-ttu-id="623bd-105">La création de rapports Azure AD fournit une API qui vous permet d’accéder aux données d’audit à l’aide de code ou d’outils associés.</span><span class="sxs-lookup"><span data-stu-id="623bd-105">Azure AD reporting provides you with an API that enables you to access audit data using code or related tools.</span></span>
<span data-ttu-id="623bd-106">Cette rubrique a pour but de vous fournir des informations de référence sur **l’API d’audit**.</span><span class="sxs-lookup"><span data-stu-id="623bd-106">The scope of this topic is to provide you with reference information about the **audit API**.</span></span>

<span data-ttu-id="623bd-107">Consultez l'article :</span><span class="sxs-lookup"><span data-stu-id="623bd-107">See:</span></span>

* <span data-ttu-id="623bd-108">[Journaux d’audit](active-directory-reporting-azure-portal.md#activity-reports) pour plus d’informations conceptuelles</span><span class="sxs-lookup"><span data-stu-id="623bd-108">[Audit logs](active-directory-reporting-azure-portal.md#activity-reports)  for more conceptual information</span></span>

* <span data-ttu-id="623bd-109">[Prise en main de l’API de création de rapports Azure Active Directory](active-directory-reporting-api-getting-started.md) pour plus d’informations sur l’API de création de rapports.</span><span class="sxs-lookup"><span data-stu-id="623bd-109">[Getting started with the Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md) for more information about the reporting API.</span></span>


<span data-ttu-id="623bd-110">Pour :</span><span class="sxs-lookup"><span data-stu-id="623bd-110">For:</span></span>

- <span data-ttu-id="623bd-111">Consulter les questions les plus fréquentes, lisez notre [FAQ](active-directory-reporting-faq.md).</span><span class="sxs-lookup"><span data-stu-id="623bd-111">Frequently asked questions, read our [FAQ](active-directory-reporting-faq.md)</span></span> 

- <span data-ttu-id="623bd-112">En savoir plus les problèmes, consultez [Envoyer un ticket de support](active-directory-troubleshooting-support-howto.md).</span><span class="sxs-lookup"><span data-stu-id="623bd-112">Issues, please [file a support ticket](active-directory-troubleshooting-support-howto.md)</span></span> 


## <a name="who-can-access-the-data"></a><span data-ttu-id="623bd-113">Qui peut accéder aux données ?</span><span class="sxs-lookup"><span data-stu-id="623bd-113">Who can access the data?</span></span>
* <span data-ttu-id="623bd-114">Utilisateurs ayant le rôle d’administrateur de sécurité ou de lecteur de la sécurité</span><span class="sxs-lookup"><span data-stu-id="623bd-114">Users in the Security Admin or Security Reader role</span></span>
* <span data-ttu-id="623bd-115">Administrateurs généraux</span><span class="sxs-lookup"><span data-stu-id="623bd-115">Global Admins</span></span>
* <span data-ttu-id="623bd-116">Toute application qui a l’autorisation d’accéder à l’API (l’autorisation de l’application peut être configurée uniquement en fonction de l’autorisation Administrateur général)</span><span class="sxs-lookup"><span data-stu-id="623bd-116">Any app that has authorization to access the API (app authorization can be setup only based on Global Admin’s permission)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="623bd-117">Composants requis</span><span class="sxs-lookup"><span data-stu-id="623bd-117">Prerequisites</span></span>
<span data-ttu-id="623bd-118">Pour accéder à ce rapport via l’API de création de rapports, vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="623bd-118">In order to access this report through the Reporting API, you must have:</span></span>

* <span data-ttu-id="623bd-119">Une [édition Azure Active Directory gratuite ou une édition récente](active-directory-editions.md)</span><span class="sxs-lookup"><span data-stu-id="623bd-119">An [Azure Active Directory Free or better edition](active-directory-editions.md)</span></span>
* <span data-ttu-id="623bd-120">Avoir respecté la [configuration requise pour accéder à l’API de création de rapports Azure AD](active-directory-reporting-api-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="623bd-120">Completed the [prerequisites to access the Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span> 

## <a name="accessing-the-api"></a><span data-ttu-id="623bd-121">Accès à l’API</span><span class="sxs-lookup"><span data-stu-id="623bd-121">Accessing the API</span></span>
<span data-ttu-id="623bd-122">Vous pouvez soit accéder à cette API via [l’Afficheur Graph](https://graphexplorer2.cloudapp.net) , soit par programme à l’aide, par exemple, de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="623bd-122">You can either access this API through the [Graph Explorer](https://graphexplorer2.cloudapp.net) or programmatically using, for example, PowerShell.</span></span> <span data-ttu-id="623bd-123">Pour que PowerShell puisse interpréter correctement la syntaxe de filtre OData utilisée dans les appels REST Graph AAD, vous devez utiliser le caractère accent grave (\`) pour « échapper » au caractère $.</span><span class="sxs-lookup"><span data-stu-id="623bd-123">In order for PowerShell to correctly interpret the OData filter syntax used in AAD Graph REST calls, you must use the backtick (aka: grave accent) character to “escape” the $ character.</span></span> <span data-ttu-id="623bd-124">Le caractère accent grave sert de [caractère d’échappement de PowerShell](https://technet.microsoft.com/library/hh847755.aspx), ce qui permet à PowerShell d’effectuer une interprétation littérale du caractère $ et de ne pas le confondre avec un nom de variable PowerShell (par exemple : $filter).</span><span class="sxs-lookup"><span data-stu-id="623bd-124">The backtick character serves as [PowerShell’s escape character](https://technet.microsoft.com/library/hh847755.aspx), allowing PowerShell to do a literal interpretation of the $ character, and avoid confusing it as a PowerShell variable name (ie: $filter).</span></span>

<span data-ttu-id="623bd-125">Cette rubrique porte sur l’Afficheur Graph.</span><span class="sxs-lookup"><span data-stu-id="623bd-125">The focus of this topic is on the Graph Explorer.</span></span> <span data-ttu-id="623bd-126">Pour obtenir un exemple PowerShell, consultez ce [script PowerShell](active-directory-reporting-api-audit-samples.md#powershell-script).</span><span class="sxs-lookup"><span data-stu-id="623bd-126">For a PowerShell example, see this [PowerShell script](active-directory-reporting-api-audit-samples.md#powershell-script).</span></span>

## <a name="api-endpoint"></a><span data-ttu-id="623bd-127">Point de terminaison d’API</span><span class="sxs-lookup"><span data-stu-id="623bd-127">API Endpoint</span></span>
<span data-ttu-id="623bd-128">Vous pouvez accéder à cette API à l’aide de l’URI suivant :</span><span class="sxs-lookup"><span data-stu-id="623bd-128">You can access this API using the following URI:</span></span>  

    https://graph.windows.net/contoso.com/activities/audit?api-version=beta

<span data-ttu-id="623bd-129">Il n’existe aucune limite quant au nombre d’enregistrements retournés par l’API d’audit Azure AD (à l’aide de la pagination OData).</span><span class="sxs-lookup"><span data-stu-id="623bd-129">There is no limit on the number of records returned by the Azure AD audit API (using OData pagination).</span></span>
<span data-ttu-id="623bd-130">Pour connaître les limites de rétention de données de rapports, consultez [Stratégies de rétention des rapports](active-directory-reporting-retention.md).</span><span class="sxs-lookup"><span data-stu-id="623bd-130">For retention limits on reporting data, check out [Reporting Retention Policies](active-directory-reporting-retention.md).</span></span>

<span data-ttu-id="623bd-131">Cet appel renvoie les données par lots.</span><span class="sxs-lookup"><span data-stu-id="623bd-131">This call returns the data in batches.</span></span> <span data-ttu-id="623bd-132">Chaque lot comporte un maximum de 1 000 enregistrements.</span><span class="sxs-lookup"><span data-stu-id="623bd-132">Each batch has a maximum of 1000 records.</span></span>  
<span data-ttu-id="623bd-133">Pour obtenir le lot d’enregistrements suivant, cliquez sur le lien Suivant.</span><span class="sxs-lookup"><span data-stu-id="623bd-133">To get the next batch of records, use the Next link.</span></span> <span data-ttu-id="623bd-134">Obtenez les informations du jeton d’évitement dans le premier jeu d’enregistrements retournés.</span><span class="sxs-lookup"><span data-stu-id="623bd-134">Get the skiptoken information from the first set of returned records.</span></span> <span data-ttu-id="623bd-135">Le jeton d’évitement se trouve à la fin du jeu de résultats.</span><span class="sxs-lookup"><span data-stu-id="623bd-135">The skip token will be at the end of the result set.</span></span>  

    https://graph.windows.net/contoso.com/activities/audit?api-version=beta&%24skiptoken=-1339686058




## <a name="supported-filters"></a><span data-ttu-id="623bd-136">Filtres pris en charge</span><span class="sxs-lookup"><span data-stu-id="623bd-136">Supported filters</span></span>
<span data-ttu-id="623bd-137">Vous pouvez réduire le nombre d’enregistrements qui sont retournés par un appel d’API à l’aide d’un filtre.</span><span class="sxs-lookup"><span data-stu-id="623bd-137">You can narrow down the number of records that are returned by an API call in form of a filter.</span></span>  
<span data-ttu-id="623bd-138">Pour les données liées à l’API de connexion, les filtres suivants sont pris en charge :</span><span class="sxs-lookup"><span data-stu-id="623bd-138">For sign-in API related data, the following filters are supported:</span></span>

* <span data-ttu-id="623bd-139">**$top=\<<nombre d’enregistrements à retourner>\>** : pour limiter le nombre d’enregistrements retournés.</span><span class="sxs-lookup"><span data-stu-id="623bd-139">**$top=\<number of records to be returned\>** - to limit the number of returned records.</span></span> <span data-ttu-id="623bd-140">Il s’agit d’une opération coûteuse.</span><span class="sxs-lookup"><span data-stu-id="623bd-140">This is an expensive operation.</span></span> <span data-ttu-id="623bd-141">N’utilisez pas ce filtre si vous souhaitez retourner des milliers d’objets.</span><span class="sxs-lookup"><span data-stu-id="623bd-141">You should not use this filter if you want to return thousands of objects.</span></span>     
* <span data-ttu-id="623bd-142">**$filter=\<<votre instruction de filtre>\>** : pour spécifier, en fonction des champs de filtre pris en charge, les types d’enregistrements qui vous intéressent</span><span class="sxs-lookup"><span data-stu-id="623bd-142">**$filter=\<your filter statement\>** - to specify, on the basis of supported filter fields, the type of records you care about</span></span>

## <a name="supported-filter-fields-and-operators"></a><span data-ttu-id="623bd-143">Opérateurs et champs de filtre pris en charge</span><span class="sxs-lookup"><span data-stu-id="623bd-143">Supported filter fields and operators</span></span>
<span data-ttu-id="623bd-144">Pour indiquer le type d’enregistrements qui vous intéressent, vous pouvez créer une déclaration de filtre contenant l’un des champs de filtre suivants ou une combinaison de ceux-ci :</span><span class="sxs-lookup"><span data-stu-id="623bd-144">To specify the type of records you care about, you can build a filter statement that can contain either one or a combination of the following filter fields:</span></span>

* <span data-ttu-id="623bd-145">[activityDate](#activitydate) : définit une date ou une plage de dates</span><span class="sxs-lookup"><span data-stu-id="623bd-145">[activityDate](#activitydate)  - defines a date or date range</span></span>
* <span data-ttu-id="623bd-146">[category](#category) : définit la catégorie que vous voulez filtrer.</span><span class="sxs-lookup"><span data-stu-id="623bd-146">[category](#category) - defines the category you want to filter on.</span></span>
* <span data-ttu-id="623bd-147">[activityStatus](#activitystatus) : définit l’état d’une activité</span><span class="sxs-lookup"><span data-stu-id="623bd-147">[activityStatus](#activitystatus) - defines the status of an activity</span></span>
* <span data-ttu-id="623bd-148">[activityType](#activitytype) : définit le type d’une activité</span><span class="sxs-lookup"><span data-stu-id="623bd-148">[activityType](#activitytype)  - defines the type of an activity</span></span>
* <span data-ttu-id="623bd-149">[activity](#activity) : définit l’activité en tant que chaîne</span><span class="sxs-lookup"><span data-stu-id="623bd-149">[activity](#activity) - defines the activity as string</span></span>  
* <span data-ttu-id="623bd-150">[actor/name](#actorname) : définit l’acteur sous forme de nom de l’acteur</span><span class="sxs-lookup"><span data-stu-id="623bd-150">[actor/name](#actorname) -   defines the actor in form of the actor's name</span></span>
* <span data-ttu-id="623bd-151">[actor/objectid](#actorobjectid) : définit l’acteur sous forme de l’ID de l’acteur</span><span class="sxs-lookup"><span data-stu-id="623bd-151">[actor/objectid](#actorobjectid) - defines the actor in form of the actor's ID</span></span>   
* <span data-ttu-id="623bd-152">[actor/upn](#actorupn) : définit l’acteur sous forme de nom d’utilisateur principal (UPN) de l’acteur</span><span class="sxs-lookup"><span data-stu-id="623bd-152">[actor/upn](#actorupn)  - defines the actor in form of the actor's user principle name (UPN)</span></span> 
* <span data-ttu-id="623bd-153">[target/name](#targetname) : définit la cible sous forme de nom de l’acteur</span><span class="sxs-lookup"><span data-stu-id="623bd-153">[target/name](#targetname)  - defines the target in form of the actor's name</span></span>
* <span data-ttu-id="623bd-154">[target/objectid](#targetobjectid) : définit la cible sous forme de l’ID de la cible</span><span class="sxs-lookup"><span data-stu-id="623bd-154">[target/objectid](#targetobjectid) - defines the target in form of the target's ID</span></span>  
* <span data-ttu-id="623bd-155">[target/upn](#targetupn) : définit l’acteur sous forme de nom d’utilisateur principal (UPN) de l’acteur</span><span class="sxs-lookup"><span data-stu-id="623bd-155">[target/upn](#targetupn) - defines the actor in form of the actor's user principle name (UPN)</span></span>   

- - -
### <a name="activitydate"></a><span data-ttu-id="623bd-156">activityDate</span><span class="sxs-lookup"><span data-stu-id="623bd-156">activityDate</span></span>
<span data-ttu-id="623bd-157">**Opérateurs pris en charge**: eq, ge, le, gt, lt</span><span class="sxs-lookup"><span data-stu-id="623bd-157">**Supported operators**: eq, ge, le, gt, lt</span></span>

<span data-ttu-id="623bd-158">**Exemple**:</span><span class="sxs-lookup"><span data-stu-id="623bd-158">**Example**:</span></span>

    $filter=tdomain + 'activities/audit?api-version=beta&`$filter=activityDate gt ' + $7daysago    

<span data-ttu-id="623bd-159">**Remarques**:</span><span class="sxs-lookup"><span data-stu-id="623bd-159">**Notes**:</span></span>

<span data-ttu-id="623bd-160">datetime doit être au format UTC</span><span class="sxs-lookup"><span data-stu-id="623bd-160">datetime should be in UTC format</span></span>

- - -
### <a name="category"></a><span data-ttu-id="623bd-161">category</span><span class="sxs-lookup"><span data-stu-id="623bd-161">category</span></span>

<span data-ttu-id="623bd-162">**Valeurs prises en charge** :</span><span class="sxs-lookup"><span data-stu-id="623bd-162">**Supported values**:</span></span>

| <span data-ttu-id="623bd-163">Catégorie</span><span class="sxs-lookup"><span data-stu-id="623bd-163">Category</span></span>                         | <span data-ttu-id="623bd-164">Valeur</span><span class="sxs-lookup"><span data-stu-id="623bd-164">Value</span></span>     |
| :--                              | ---       |
| <span data-ttu-id="623bd-165">Annuaire principal</span><span class="sxs-lookup"><span data-stu-id="623bd-165">Core Directory</span></span>                   | <span data-ttu-id="623bd-166">Répertoire</span><span class="sxs-lookup"><span data-stu-id="623bd-166">Directory</span></span> |
| <span data-ttu-id="623bd-167">Gestion des mots de passe en libre-service</span><span class="sxs-lookup"><span data-stu-id="623bd-167">Self-service Password Management</span></span> | <span data-ttu-id="623bd-168">SSPR</span><span class="sxs-lookup"><span data-stu-id="623bd-168">SSPR</span></span>      |
| <span data-ttu-id="623bd-169">Gestion des groupes en libre-service</span><span class="sxs-lookup"><span data-stu-id="623bd-169">Self-service Group Management</span></span>    | <span data-ttu-id="623bd-170">SSGM</span><span class="sxs-lookup"><span data-stu-id="623bd-170">SSGM</span></span>      |
| <span data-ttu-id="623bd-171">Approvisionnement des comptes</span><span class="sxs-lookup"><span data-stu-id="623bd-171">Account Provisioning</span></span>             | <span data-ttu-id="623bd-172">Synchronisation</span><span class="sxs-lookup"><span data-stu-id="623bd-172">Sync</span></span>      |
| <span data-ttu-id="623bd-173">Substitution de mot de passe automatique</span><span class="sxs-lookup"><span data-stu-id="623bd-173">Automated Password Rollover</span></span>      | <span data-ttu-id="623bd-174">Substitution de mot de passe automatique</span><span class="sxs-lookup"><span data-stu-id="623bd-174">Automated Password Rollover</span></span> |
| <span data-ttu-id="623bd-175">Identity Protection</span><span class="sxs-lookup"><span data-stu-id="623bd-175">Identity Protection</span></span>              | <span data-ttu-id="623bd-176">IdentityProtection</span><span class="sxs-lookup"><span data-stu-id="623bd-176">IdentityProtection</span></span> |
| <span data-ttu-id="623bd-177">Utilisateurs invités</span><span class="sxs-lookup"><span data-stu-id="623bd-177">Invited Users</span></span>                    | <span data-ttu-id="623bd-178">Utilisateurs invités</span><span class="sxs-lookup"><span data-stu-id="623bd-178">Invited Users</span></span> |
| <span data-ttu-id="623bd-179">Service MIM</span><span class="sxs-lookup"><span data-stu-id="623bd-179">MIM Service</span></span>                      | <span data-ttu-id="623bd-180">Service MIM</span><span class="sxs-lookup"><span data-stu-id="623bd-180">MIM Service</span></span> |



<span data-ttu-id="623bd-181">**Opérateurs pris en charge**: eq</span><span class="sxs-lookup"><span data-stu-id="623bd-181">**Supported operators**: eq</span></span>

<span data-ttu-id="623bd-182">**Exemple**:</span><span class="sxs-lookup"><span data-stu-id="623bd-182">**Example**:</span></span>

    $filter=category eq 'SSPR'
- - -
### <a name="activitystatus"></a><span data-ttu-id="623bd-183">activityStatus</span><span class="sxs-lookup"><span data-stu-id="623bd-183">activityStatus</span></span>

<span data-ttu-id="623bd-184">**Valeurs prises en charge** :</span><span class="sxs-lookup"><span data-stu-id="623bd-184">**Supported values**:</span></span>

| <span data-ttu-id="623bd-185">État de l’activité</span><span class="sxs-lookup"><span data-stu-id="623bd-185">Activity Status</span></span> | <span data-ttu-id="623bd-186">Valeur</span><span class="sxs-lookup"><span data-stu-id="623bd-186">Value</span></span> |
| :--             | ---   |
| <span data-ttu-id="623bd-187">Succès</span><span class="sxs-lookup"><span data-stu-id="623bd-187">Success</span></span>         | <span data-ttu-id="623bd-188">0</span><span class="sxs-lookup"><span data-stu-id="623bd-188">0</span></span>     |
| <span data-ttu-id="623bd-189">Échec</span><span class="sxs-lookup"><span data-stu-id="623bd-189">Failure</span></span>         | <span data-ttu-id="623bd-190">- 1</span><span class="sxs-lookup"><span data-stu-id="623bd-190">- 1</span></span>   |

<span data-ttu-id="623bd-191">**Opérateurs pris en charge**: eq</span><span class="sxs-lookup"><span data-stu-id="623bd-191">**Supported operators**: eq</span></span>

<span data-ttu-id="623bd-192">**Exemple**:</span><span class="sxs-lookup"><span data-stu-id="623bd-192">**Example**:</span></span>

    $filter=activityStatus eq -1    

---
### <a name="activitytype"></a><span data-ttu-id="623bd-193">activityType</span><span class="sxs-lookup"><span data-stu-id="623bd-193">activityType</span></span>
<span data-ttu-id="623bd-194">**Opérateurs pris en charge**: eq</span><span class="sxs-lookup"><span data-stu-id="623bd-194">**Supported operators**: eq</span></span>

<span data-ttu-id="623bd-195">**Exemple**:</span><span class="sxs-lookup"><span data-stu-id="623bd-195">**Example**:</span></span>

    $filter=activityType eq 'User'    

<span data-ttu-id="623bd-196">**Remarques**:</span><span class="sxs-lookup"><span data-stu-id="623bd-196">**Notes**:</span></span>

<span data-ttu-id="623bd-197">respecte la casse</span><span class="sxs-lookup"><span data-stu-id="623bd-197">case-sensitive</span></span>

- - -
### <a name="activity"></a><span data-ttu-id="623bd-198">activity</span><span class="sxs-lookup"><span data-stu-id="623bd-198">activity</span></span>
<span data-ttu-id="623bd-199">**Opérateurs pris en charge**: eq, contains, startsWith</span><span class="sxs-lookup"><span data-stu-id="623bd-199">**Supported operators**: eq, contains, startsWith</span></span>

<span data-ttu-id="623bd-200">**Exemple**:</span><span class="sxs-lookup"><span data-stu-id="623bd-200">**Example**:</span></span>

    $filter=activity eq 'Add application' or contains(activity, 'Application') or startsWith(activity, 'Add')    

<span data-ttu-id="623bd-201">**Remarques**:</span><span class="sxs-lookup"><span data-stu-id="623bd-201">**Notes**:</span></span>

<span data-ttu-id="623bd-202">respecte la casse</span><span class="sxs-lookup"><span data-stu-id="623bd-202">case-sensitive</span></span>

- - -
### <a name="actorname"></a><span data-ttu-id="623bd-203">actor/name</span><span class="sxs-lookup"><span data-stu-id="623bd-203">actor/name</span></span>
<span data-ttu-id="623bd-204">**Opérateurs pris en charge**: eq, contains, startsWith</span><span class="sxs-lookup"><span data-stu-id="623bd-204">**Supported operators**: eq, contains, startsWith</span></span>

<span data-ttu-id="623bd-205">**Exemple**:</span><span class="sxs-lookup"><span data-stu-id="623bd-205">**Example**:</span></span>

    $filter=actor/name eq 'test' or contains(actor/name, 'test') or startswith(actor/name, 'test')    

<span data-ttu-id="623bd-206">**Remarques**:</span><span class="sxs-lookup"><span data-stu-id="623bd-206">**Notes**:</span></span>

<span data-ttu-id="623bd-207">ne respecte pas la casse</span><span class="sxs-lookup"><span data-stu-id="623bd-207">case-insensitive</span></span>

- - -
### <a name="actorobjectid"></a><span data-ttu-id="623bd-208">actor/objectid</span><span class="sxs-lookup"><span data-stu-id="623bd-208">actor/objectId</span></span>
<span data-ttu-id="623bd-209">**Opérateurs pris en charge**: eq</span><span class="sxs-lookup"><span data-stu-id="623bd-209">**Supported operators**: eq</span></span>

<span data-ttu-id="623bd-210">**Exemple**:</span><span class="sxs-lookup"><span data-stu-id="623bd-210">**Example**:</span></span>

    $filter=actor/objectId eq 'e8096343-86a2-4384-b43a-ebfdb17600ba'    


- - -
### <a name="targetname"></a><span data-ttu-id="623bd-211">target/name</span><span class="sxs-lookup"><span data-stu-id="623bd-211">target/name</span></span>
<span data-ttu-id="623bd-212">**Opérateurs pris en charge**: eq, contains, startsWith</span><span class="sxs-lookup"><span data-stu-id="623bd-212">**Supported operators**: eq, contains, startsWith</span></span>

<span data-ttu-id="623bd-213">**Exemple**:</span><span class="sxs-lookup"><span data-stu-id="623bd-213">**Example**:</span></span>

    $filter=targets/any(t: t/name eq 'some name')    

<span data-ttu-id="623bd-214">**Remarques**:</span><span class="sxs-lookup"><span data-stu-id="623bd-214">**Notes**:</span></span>

<span data-ttu-id="623bd-215">ne respecte pas la casse</span><span class="sxs-lookup"><span data-stu-id="623bd-215">Case-insensitive</span></span>

- - -
### <a name="targetupn"></a><span data-ttu-id="623bd-216">target/upn</span><span class="sxs-lookup"><span data-stu-id="623bd-216">target/upn</span></span>
<span data-ttu-id="623bd-217">**Opérateurs pris en charge**: eq, startsWith</span><span class="sxs-lookup"><span data-stu-id="623bd-217">**Supported operators**: eq, startsWith</span></span>

<span data-ttu-id="623bd-218">**Exemple**:</span><span class="sxs-lookup"><span data-stu-id="623bd-218">**Example**:</span></span>

    $filter=targets/any(t: startswith(t/Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity/userPrincipalName,'abc'))    

<span data-ttu-id="623bd-219">**Remarques**:</span><span class="sxs-lookup"><span data-stu-id="623bd-219">**Notes**:</span></span>

* <span data-ttu-id="623bd-220">Non-respect de la casse</span><span class="sxs-lookup"><span data-stu-id="623bd-220">Case-insensitive</span></span>
* <span data-ttu-id="623bd-221">Vous devez ajouter l’espace de noms complet lors de l’interrogation de Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity</span><span class="sxs-lookup"><span data-stu-id="623bd-221">You need to add the full namespace when querying  Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity</span></span>

- - -
### <a name="targetobjectid"></a><span data-ttu-id="623bd-222">target/objectid</span><span class="sxs-lookup"><span data-stu-id="623bd-222">target/objectId</span></span>
<span data-ttu-id="623bd-223">**Opérateurs pris en charge**: eq</span><span class="sxs-lookup"><span data-stu-id="623bd-223">**Supported operators**: eq</span></span>

<span data-ttu-id="623bd-224">**Exemple**:</span><span class="sxs-lookup"><span data-stu-id="623bd-224">**Example**:</span></span>

    $filter=targets/any(t: t/objectId eq 'e8096343-86a2-4384-b43a-ebfdb17600ba')    

- - -
### <a name="actorupn"></a><span data-ttu-id="623bd-225">actor/upn</span><span class="sxs-lookup"><span data-stu-id="623bd-225">actor/upn</span></span>
<span data-ttu-id="623bd-226">**Opérateurs pris en charge**: eq, startsWith</span><span class="sxs-lookup"><span data-stu-id="623bd-226">**Supported operators**: eq, startsWith</span></span>

<span data-ttu-id="623bd-227">**Exemple**:</span><span class="sxs-lookup"><span data-stu-id="623bd-227">**Example**:</span></span>

    $filter=startswith(actor/Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity/userPrincipalName,'abc')    

<span data-ttu-id="623bd-228">**Remarques**:</span><span class="sxs-lookup"><span data-stu-id="623bd-228">**Notes**:</span></span>

* <span data-ttu-id="623bd-229">ne respecte pas la casse</span><span class="sxs-lookup"><span data-stu-id="623bd-229">Case-insensitive</span></span> 
* <span data-ttu-id="623bd-230">Vous devez ajouter l’espace de noms complet lors de l’interrogation de Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity</span><span class="sxs-lookup"><span data-stu-id="623bd-230">You need to add the full namespace when querying Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity</span></span>

- - -
## <a name="next-steps"></a><span data-ttu-id="623bd-231">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="623bd-231">Next Steps</span></span>
* <span data-ttu-id="623bd-232">Voulez-vous voir des exemples d’activités système filtrées ?</span><span class="sxs-lookup"><span data-stu-id="623bd-232">Do you want to see examples for filtered system activities?</span></span> <span data-ttu-id="623bd-233">Consultez les [exemples d’API d’audit Azure Active Directory](active-directory-reporting-api-audit-samples.md).</span><span class="sxs-lookup"><span data-stu-id="623bd-233">Check out the [Azure Active Directory audit API samples](active-directory-reporting-api-audit-samples.md).</span></span>
* <span data-ttu-id="623bd-234">Vous souhaitez en savoir plus sur l’API de création de rapports Azure AD ?</span><span class="sxs-lookup"><span data-stu-id="623bd-234">Do you want to know more about the Azure AD reporting API?</span></span> <span data-ttu-id="623bd-235">Consultez [Prise en main de l’API de création de rapports Azure Active Directory](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="623bd-235">See [Getting started with the Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>

