---
title: "audit d’Active Directory aaaAzure référence de l’API | Documents Microsoft"
description: "Comment tooget main hello API d’audit Azure Active Directory"
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
ms.openlocfilehash: 5f33b62ede9be445f35704739e328580dc454368
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-audit-api-reference"></a><span data-ttu-id="29c56-103">Référence d’API d’audit Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="29c56-103">Azure Active Directory audit API reference</span></span>
<span data-ttu-id="29c56-104">Cette rubrique fait partie d’une collection de rubriques hello Azure Active Directory sur les API de création de rapports.</span><span class="sxs-lookup"><span data-stu-id="29c56-104">This topic is part of a collection of topics about hello Azure Active Directory reporting API.</span></span>  
<span data-ttu-id="29c56-105">Création de rapports Azure AD fournit une API qui vous permet de tooaccess les données d’audit à l’aide de code ou les outils connexes.</span><span class="sxs-lookup"><span data-stu-id="29c56-105">Azure AD reporting provides you with an API that enables you tooaccess audit data using code or related tools.</span></span>
<span data-ttu-id="29c56-106">Hello cette rubrique traite de tooprovide des informations de référence sur hello **audit API**.</span><span class="sxs-lookup"><span data-stu-id="29c56-106">hello scope of this topic is tooprovide you with reference information about hello **audit API**.</span></span>

<span data-ttu-id="29c56-107">Consultez l'article :</span><span class="sxs-lookup"><span data-stu-id="29c56-107">See:</span></span>

* <span data-ttu-id="29c56-108">[Journaux d’audit](active-directory-reporting-azure-portal.md#activity-reports) pour plus d’informations conceptuelles</span><span class="sxs-lookup"><span data-stu-id="29c56-108">[Audit logs](active-directory-reporting-azure-portal.md#activity-reports)  for more conceptual information</span></span>

* <span data-ttu-id="29c56-109">[Prise en main de hello API Azure Active Directory Reporting](active-directory-reporting-api-getting-started.md) pour plus d’informations sur les API de création de rapports de hello.</span><span class="sxs-lookup"><span data-stu-id="29c56-109">[Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md) for more information about hello reporting API.</span></span>


<span data-ttu-id="29c56-110">Pour :</span><span class="sxs-lookup"><span data-stu-id="29c56-110">For:</span></span>

- <span data-ttu-id="29c56-111">Consulter les questions les plus fréquentes, lisez notre [FAQ](active-directory-reporting-faq.md).</span><span class="sxs-lookup"><span data-stu-id="29c56-111">Frequently asked questions, read our [FAQ](active-directory-reporting-faq.md)</span></span> 

- <span data-ttu-id="29c56-112">En savoir plus les problèmes, consultez [Envoyer un ticket de support](active-directory-troubleshooting-support-howto.md).</span><span class="sxs-lookup"><span data-stu-id="29c56-112">Issues, please [file a support ticket](active-directory-troubleshooting-support-howto.md)</span></span> 


## <a name="who-can-access-hello-data"></a><span data-ttu-id="29c56-113">Qui peut accéder à des données de salutation ?</span><span class="sxs-lookup"><span data-stu-id="29c56-113">Who can access hello data?</span></span>
* <span data-ttu-id="29c56-114">Utilisateurs dans le rôle d’administrateur de la sécurité ou de sécurité Reader hello</span><span class="sxs-lookup"><span data-stu-id="29c56-114">Users in hello Security Admin or Security Reader role</span></span>
* <span data-ttu-id="29c56-115">Administrateurs généraux</span><span class="sxs-lookup"><span data-stu-id="29c56-115">Global Admins</span></span>
* <span data-ttu-id="29c56-116">N’importe quelle application qui a l’autorisation tooaccess hello API (autorisation de l’application peut être configurés uniquement en fonction d’autorisation de l’administrateur Global)</span><span class="sxs-lookup"><span data-stu-id="29c56-116">Any app that has authorization tooaccess hello API (app authorization can be setup only based on Global Admin’s permission)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="29c56-117">Composants requis</span><span class="sxs-lookup"><span data-stu-id="29c56-117">Prerequisites</span></span>
<span data-ttu-id="29c56-118">Dans tooaccess commande par le biais de ce rapport hello API de création de rapports, vous devez avoir :</span><span class="sxs-lookup"><span data-stu-id="29c56-118">In order tooaccess this report through hello Reporting API, you must have:</span></span>

* <span data-ttu-id="29c56-119">Une [édition Azure Active Directory gratuite ou une édition récente](active-directory-editions.md)</span><span class="sxs-lookup"><span data-stu-id="29c56-119">An [Azure Active Directory Free or better edition](active-directory-editions.md)</span></span>
* <span data-ttu-id="29c56-120">Hello terminé [API reporting de conditions préalables tooaccess hello Azure AD](active-directory-reporting-api-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="29c56-120">Completed hello [prerequisites tooaccess hello Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span> 

## <a name="accessing-hello-api"></a><span data-ttu-id="29c56-121">L’accès aux API de hello</span><span class="sxs-lookup"><span data-stu-id="29c56-121">Accessing hello API</span></span>
<span data-ttu-id="29c56-122">Vous pouvez soit accéder à cette API via hello [Explorateur graphique](https://graphexplorer2.cloudapp.net) ou par programmation à l’aide, par exemple, PowerShell.</span><span class="sxs-lookup"><span data-stu-id="29c56-122">You can either access this API through hello [Graph Explorer](https://graphexplorer2.cloudapp.net) or programmatically using, for example, PowerShell.</span></span> <span data-ttu-id="29c56-123">Dans l’ordre pour PowerShell toocorrectly interpréter la syntaxe de filtre OData hello utilisée dans les appels de Graph AAD REST, vous devez utiliser hello backtick (aka : accent grave) caractère trop « caractère d’échappement « hello $.</span><span class="sxs-lookup"><span data-stu-id="29c56-123">In order for PowerShell toocorrectly interpret hello OData filter syntax used in AAD Graph REST calls, you must use hello backtick (aka: grave accent) character too“escape” hello $ character.</span></span> <span data-ttu-id="29c56-124">sert de caractère de guillemet inversé Hello [caractère d’échappement de PowerShell](https://technet.microsoft.com/library/hh847755.aspx), ce qui permet de PowerShell toodo une interprétation littéral de caractère de $ hello et éviter toute confusion entre elle en tant que nom d’une variable PowerShell (ie : $filter).</span><span class="sxs-lookup"><span data-stu-id="29c56-124">hello backtick character serves as [PowerShell’s escape character](https://technet.microsoft.com/library/hh847755.aspx), allowing PowerShell toodo a literal interpretation of hello $ character, and avoid confusing it as a PowerShell variable name (ie: $filter).</span></span>

<span data-ttu-id="29c56-125">Hello de cette rubrique concerne les hello Explorateur graphique.</span><span class="sxs-lookup"><span data-stu-id="29c56-125">hello focus of this topic is on hello Graph Explorer.</span></span> <span data-ttu-id="29c56-126">Pour obtenir un exemple PowerShell, consultez ce [script PowerShell](active-directory-reporting-api-audit-samples.md#powershell-script).</span><span class="sxs-lookup"><span data-stu-id="29c56-126">For a PowerShell example, see this [PowerShell script](active-directory-reporting-api-audit-samples.md#powershell-script).</span></span>

## <a name="api-endpoint"></a><span data-ttu-id="29c56-127">Point de terminaison d’API</span><span class="sxs-lookup"><span data-stu-id="29c56-127">API Endpoint</span></span>
<span data-ttu-id="29c56-128">Vous pouvez accéder à cette API à l’aide de hello suivant l’URI :</span><span class="sxs-lookup"><span data-stu-id="29c56-128">You can access this API using hello following URI:</span></span>  

    https://graph.windows.net/contoso.com/activities/audit?api-version=beta

<span data-ttu-id="29c56-129">Il n’existe aucune limite sur le nombre de hello d’enregistrements retournés par l’API d’audit hello Azure AD (à l’aide de la pagination de OData).</span><span class="sxs-lookup"><span data-stu-id="29c56-129">There is no limit on hello number of records returned by hello Azure AD audit API (using OData pagination).</span></span>
<span data-ttu-id="29c56-130">Pour connaître les limites de rétention de données de rapports, consultez [Stratégies de rétention des rapports](active-directory-reporting-retention.md).</span><span class="sxs-lookup"><span data-stu-id="29c56-130">For retention limits on reporting data, check out [Reporting Retention Policies](active-directory-reporting-retention.md).</span></span>

<span data-ttu-id="29c56-131">Cet appel retourne les données de hello dans des lots.</span><span class="sxs-lookup"><span data-stu-id="29c56-131">This call returns hello data in batches.</span></span> <span data-ttu-id="29c56-132">Chaque lot comporte un maximum de 1 000 enregistrements.</span><span class="sxs-lookup"><span data-stu-id="29c56-132">Each batch has a maximum of 1000 records.</span></span>  
<span data-ttu-id="29c56-133">tooget hello suivant lot d’enregistrements, utilisez hello de lien suivant.</span><span class="sxs-lookup"><span data-stu-id="29c56-133">tooget hello next batch of records, use hello Next link.</span></span> <span data-ttu-id="29c56-134">Permet d’obtenir des informations de skiptoken hello hello premier ensemble d’enregistrements retournés.</span><span class="sxs-lookup"><span data-stu-id="29c56-134">Get hello skiptoken information from hello first set of returned records.</span></span> <span data-ttu-id="29c56-135">jeton d’évitement Hello sera à fin hello hello du jeu de résultats.</span><span class="sxs-lookup"><span data-stu-id="29c56-135">hello skip token will be at hello end of hello result set.</span></span>  

    https://graph.windows.net/contoso.com/activities/audit?api-version=beta&%24skiptoken=-1339686058




## <a name="supported-filters"></a><span data-ttu-id="29c56-136">Filtres pris en charge</span><span class="sxs-lookup"><span data-stu-id="29c56-136">Supported filters</span></span>
<span data-ttu-id="29c56-137">Vous pouvez réduire nombre hello d’enregistrements retournés par une API appeler sous forme d’un filtre.</span><span class="sxs-lookup"><span data-stu-id="29c56-137">You can narrow down hello number of records that are returned by an API call in form of a filter.</span></span>  
<span data-ttu-id="29c56-138">Connectez-vous API hello suivant des filtres, les données associées sont prises en charge :</span><span class="sxs-lookup"><span data-stu-id="29c56-138">For sign-in API related data, hello following filters are supported:</span></span>

* <span data-ttu-id="29c56-139">**$top =\<retourné de nombre d’enregistrements toobe\>**  -nombre de hello toolimit d’enregistrements renvoyés.</span><span class="sxs-lookup"><span data-stu-id="29c56-139">**$top=\<number of records toobe returned\>** - toolimit hello number of returned records.</span></span> <span data-ttu-id="29c56-140">Il s’agit d’une opération coûteuse.</span><span class="sxs-lookup"><span data-stu-id="29c56-140">This is an expensive operation.</span></span> <span data-ttu-id="29c56-141">Vous ne devez pas utiliser ce filtre si vous souhaitez tooreturn des milliers d’objets.</span><span class="sxs-lookup"><span data-stu-id="29c56-141">You should not use this filter if you want tooreturn thousands of objects.</span></span>     
* <span data-ttu-id="29c56-142">**$filter =\<votre instruction de filtrage\>**  -toospecify, sur la base de hello de champs de filtre pris en charge, type hello d’enregistrements qui vous intéressent</span><span class="sxs-lookup"><span data-stu-id="29c56-142">**$filter=\<your filter statement\>** - toospecify, on hello basis of supported filter fields, hello type of records you care about</span></span>

## <a name="supported-filter-fields-and-operators"></a><span data-ttu-id="29c56-143">Opérateurs et champs de filtre pris en charge</span><span class="sxs-lookup"><span data-stu-id="29c56-143">Supported filter fields and operators</span></span>
<span data-ttu-id="29c56-144">type de hello toospecify d’enregistrements qui que vous intéressent, vous pouvez générer une instruction de filtrage qui peut contenir un ou une combinaison de hello suivant des champs de filtre :</span><span class="sxs-lookup"><span data-stu-id="29c56-144">toospecify hello type of records you care about, you can build a filter statement that can contain either one or a combination of hello following filter fields:</span></span>

* <span data-ttu-id="29c56-145">[activityDate](#activitydate) : définit une date ou une plage de dates</span><span class="sxs-lookup"><span data-stu-id="29c56-145">[activityDate](#activitydate)  - defines a date or date range</span></span>
* <span data-ttu-id="29c56-146">[catégorie](#category) -définit hello catégorie toofilter sur.</span><span class="sxs-lookup"><span data-stu-id="29c56-146">[category](#category) - defines hello category you want toofilter on.</span></span>
* <span data-ttu-id="29c56-147">[activityStatus](#activitystatus) -définit l’état de hello d’une activité</span><span class="sxs-lookup"><span data-stu-id="29c56-147">[activityStatus](#activitystatus) - defines hello status of an activity</span></span>
* <span data-ttu-id="29c56-148">[type d’activité](#activitytype) -définit le type hello d’une activité</span><span class="sxs-lookup"><span data-stu-id="29c56-148">[activityType](#activitytype)  - defines hello type of an activity</span></span>
* <span data-ttu-id="29c56-149">[activité](#activity) -définit l’activité hello en tant que chaîne</span><span class="sxs-lookup"><span data-stu-id="29c56-149">[activity](#activity) - defines hello activity as string</span></span>  
* <span data-ttu-id="29c56-150">[nom del’acteur/](#actorname) -définit l’acteur de hello sous forme de nom de hello acteur</span><span class="sxs-lookup"><span data-stu-id="29c56-150">[actor/name](#actorname) -   defines hello actor in form of hello actor's name</span></span>
* <span data-ttu-id="29c56-151">[acteur/objectid](#actorobjectid) -définit l’acteur de hello sous forme d’ID de hello acteur</span><span class="sxs-lookup"><span data-stu-id="29c56-151">[actor/objectid](#actorobjectid) - defines hello actor in form of hello actor's ID</span></span>   
* <span data-ttu-id="29c56-152">[acteur/upn](#actorupn) -définit l’acteur de hello sous forme nom d’acteur hello d’utilisateur principal (UPN)</span><span class="sxs-lookup"><span data-stu-id="29c56-152">[actor/upn](#actorupn)  - defines hello actor in form of hello actor's user principle name (UPN)</span></span> 
* <span data-ttu-id="29c56-153">[nom de la cible](#targetname) -définit la cible de hello sous forme de nom de hello acteur</span><span class="sxs-lookup"><span data-stu-id="29c56-153">[target/name](#targetname)  - defines hello target in form of hello actor's name</span></span>
* <span data-ttu-id="29c56-154">[cible/objectid](#targetobjectid) -définit la cible de hello sous forme de hello ID cible</span><span class="sxs-lookup"><span data-stu-id="29c56-154">[target/objectid](#targetobjectid) - defines hello target in form of hello target's ID</span></span>  
* <span data-ttu-id="29c56-155">[cible/upn](#targetupn) -définit l’acteur de hello sous forme nom d’acteur hello d’utilisateur principal (UPN)</span><span class="sxs-lookup"><span data-stu-id="29c56-155">[target/upn](#targetupn) - defines hello actor in form of hello actor's user principle name (UPN)</span></span>   

- - -
### <a name="activitydate"></a><span data-ttu-id="29c56-156">activityDate</span><span class="sxs-lookup"><span data-stu-id="29c56-156">activityDate</span></span>
<span data-ttu-id="29c56-157">**Opérateurs pris en charge**: eq, ge, le, gt, lt</span><span class="sxs-lookup"><span data-stu-id="29c56-157">**Supported operators**: eq, ge, le, gt, lt</span></span>

<span data-ttu-id="29c56-158">**Exemple**:</span><span class="sxs-lookup"><span data-stu-id="29c56-158">**Example**:</span></span>

    $filter=tdomain + 'activities/audit?api-version=beta&`$filter=activityDate gt ' + $7daysago    

<span data-ttu-id="29c56-159">**Remarques**:</span><span class="sxs-lookup"><span data-stu-id="29c56-159">**Notes**:</span></span>

<span data-ttu-id="29c56-160">datetime doit être au format UTC</span><span class="sxs-lookup"><span data-stu-id="29c56-160">datetime should be in UTC format</span></span>

- - -
### <a name="category"></a><span data-ttu-id="29c56-161">category</span><span class="sxs-lookup"><span data-stu-id="29c56-161">category</span></span>

<span data-ttu-id="29c56-162">**Valeurs prises en charge** :</span><span class="sxs-lookup"><span data-stu-id="29c56-162">**Supported values**:</span></span>

| <span data-ttu-id="29c56-163">Catégorie</span><span class="sxs-lookup"><span data-stu-id="29c56-163">Category</span></span>                         | <span data-ttu-id="29c56-164">Valeur</span><span class="sxs-lookup"><span data-stu-id="29c56-164">Value</span></span>     |
| :--                              | ---       |
| <span data-ttu-id="29c56-165">Annuaire principal</span><span class="sxs-lookup"><span data-stu-id="29c56-165">Core Directory</span></span>                   | <span data-ttu-id="29c56-166">Répertoire</span><span class="sxs-lookup"><span data-stu-id="29c56-166">Directory</span></span> |
| <span data-ttu-id="29c56-167">Gestion des mots de passe en libre-service</span><span class="sxs-lookup"><span data-stu-id="29c56-167">Self-service Password Management</span></span> | <span data-ttu-id="29c56-168">SSPR</span><span class="sxs-lookup"><span data-stu-id="29c56-168">SSPR</span></span>      |
| <span data-ttu-id="29c56-169">Gestion des groupes en libre-service</span><span class="sxs-lookup"><span data-stu-id="29c56-169">Self-service Group Management</span></span>    | <span data-ttu-id="29c56-170">SSGM</span><span class="sxs-lookup"><span data-stu-id="29c56-170">SSGM</span></span>      |
| <span data-ttu-id="29c56-171">Approvisionnement des comptes</span><span class="sxs-lookup"><span data-stu-id="29c56-171">Account Provisioning</span></span>             | <span data-ttu-id="29c56-172">Synchronisation</span><span class="sxs-lookup"><span data-stu-id="29c56-172">Sync</span></span>      |
| <span data-ttu-id="29c56-173">Substitution de mot de passe automatique</span><span class="sxs-lookup"><span data-stu-id="29c56-173">Automated Password Rollover</span></span>      | <span data-ttu-id="29c56-174">Substitution de mot de passe automatique</span><span class="sxs-lookup"><span data-stu-id="29c56-174">Automated Password Rollover</span></span> |
| <span data-ttu-id="29c56-175">Identity Protection</span><span class="sxs-lookup"><span data-stu-id="29c56-175">Identity Protection</span></span>              | <span data-ttu-id="29c56-176">IdentityProtection</span><span class="sxs-lookup"><span data-stu-id="29c56-176">IdentityProtection</span></span> |
| <span data-ttu-id="29c56-177">Utilisateurs invités</span><span class="sxs-lookup"><span data-stu-id="29c56-177">Invited Users</span></span>                    | <span data-ttu-id="29c56-178">Utilisateurs invités</span><span class="sxs-lookup"><span data-stu-id="29c56-178">Invited Users</span></span> |
| <span data-ttu-id="29c56-179">Service MIM</span><span class="sxs-lookup"><span data-stu-id="29c56-179">MIM Service</span></span>                      | <span data-ttu-id="29c56-180">Service MIM</span><span class="sxs-lookup"><span data-stu-id="29c56-180">MIM Service</span></span> |



<span data-ttu-id="29c56-181">**Opérateurs pris en charge**: eq</span><span class="sxs-lookup"><span data-stu-id="29c56-181">**Supported operators**: eq</span></span>

<span data-ttu-id="29c56-182">**Exemple**:</span><span class="sxs-lookup"><span data-stu-id="29c56-182">**Example**:</span></span>

    $filter=category eq 'SSPR'
- - -
### <a name="activitystatus"></a><span data-ttu-id="29c56-183">activityStatus</span><span class="sxs-lookup"><span data-stu-id="29c56-183">activityStatus</span></span>

<span data-ttu-id="29c56-184">**Valeurs prises en charge** :</span><span class="sxs-lookup"><span data-stu-id="29c56-184">**Supported values**:</span></span>

| <span data-ttu-id="29c56-185">État de l’activité</span><span class="sxs-lookup"><span data-stu-id="29c56-185">Activity Status</span></span> | <span data-ttu-id="29c56-186">Valeur</span><span class="sxs-lookup"><span data-stu-id="29c56-186">Value</span></span> |
| :--             | ---   |
| <span data-ttu-id="29c56-187">Succès</span><span class="sxs-lookup"><span data-stu-id="29c56-187">Success</span></span>         | <span data-ttu-id="29c56-188">0</span><span class="sxs-lookup"><span data-stu-id="29c56-188">0</span></span>     |
| <span data-ttu-id="29c56-189">Échec</span><span class="sxs-lookup"><span data-stu-id="29c56-189">Failure</span></span>         | <span data-ttu-id="29c56-190">- 1</span><span class="sxs-lookup"><span data-stu-id="29c56-190">- 1</span></span>   |

<span data-ttu-id="29c56-191">**Opérateurs pris en charge**: eq</span><span class="sxs-lookup"><span data-stu-id="29c56-191">**Supported operators**: eq</span></span>

<span data-ttu-id="29c56-192">**Exemple**:</span><span class="sxs-lookup"><span data-stu-id="29c56-192">**Example**:</span></span>

    $filter=activityStatus eq -1    

---
### <a name="activitytype"></a><span data-ttu-id="29c56-193">activityType</span><span class="sxs-lookup"><span data-stu-id="29c56-193">activityType</span></span>
<span data-ttu-id="29c56-194">**Opérateurs pris en charge**: eq</span><span class="sxs-lookup"><span data-stu-id="29c56-194">**Supported operators**: eq</span></span>

<span data-ttu-id="29c56-195">**Exemple**:</span><span class="sxs-lookup"><span data-stu-id="29c56-195">**Example**:</span></span>

    $filter=activityType eq 'User'    

<span data-ttu-id="29c56-196">**Remarques**:</span><span class="sxs-lookup"><span data-stu-id="29c56-196">**Notes**:</span></span>

<span data-ttu-id="29c56-197">respecte la casse</span><span class="sxs-lookup"><span data-stu-id="29c56-197">case-sensitive</span></span>

- - -
### <a name="activity"></a><span data-ttu-id="29c56-198">activity</span><span class="sxs-lookup"><span data-stu-id="29c56-198">activity</span></span>
<span data-ttu-id="29c56-199">**Opérateurs pris en charge**: eq, contains, startsWith</span><span class="sxs-lookup"><span data-stu-id="29c56-199">**Supported operators**: eq, contains, startsWith</span></span>

<span data-ttu-id="29c56-200">**Exemple**:</span><span class="sxs-lookup"><span data-stu-id="29c56-200">**Example**:</span></span>

    $filter=activity eq 'Add application' or contains(activity, 'Application') or startsWith(activity, 'Add')    

<span data-ttu-id="29c56-201">**Remarques**:</span><span class="sxs-lookup"><span data-stu-id="29c56-201">**Notes**:</span></span>

<span data-ttu-id="29c56-202">respecte la casse</span><span class="sxs-lookup"><span data-stu-id="29c56-202">case-sensitive</span></span>

- - -
### <a name="actorname"></a><span data-ttu-id="29c56-203">actor/name</span><span class="sxs-lookup"><span data-stu-id="29c56-203">actor/name</span></span>
<span data-ttu-id="29c56-204">**Opérateurs pris en charge**: eq, contains, startsWith</span><span class="sxs-lookup"><span data-stu-id="29c56-204">**Supported operators**: eq, contains, startsWith</span></span>

<span data-ttu-id="29c56-205">**Exemple**:</span><span class="sxs-lookup"><span data-stu-id="29c56-205">**Example**:</span></span>

    $filter=actor/name eq 'test' or contains(actor/name, 'test') or startswith(actor/name, 'test')    

<span data-ttu-id="29c56-206">**Remarques**:</span><span class="sxs-lookup"><span data-stu-id="29c56-206">**Notes**:</span></span>

<span data-ttu-id="29c56-207">ne respecte pas la casse</span><span class="sxs-lookup"><span data-stu-id="29c56-207">case-insensitive</span></span>

- - -
### <a name="actorobjectid"></a><span data-ttu-id="29c56-208">actor/objectid</span><span class="sxs-lookup"><span data-stu-id="29c56-208">actor/objectId</span></span>
<span data-ttu-id="29c56-209">**Opérateurs pris en charge**: eq</span><span class="sxs-lookup"><span data-stu-id="29c56-209">**Supported operators**: eq</span></span>

<span data-ttu-id="29c56-210">**Exemple**:</span><span class="sxs-lookup"><span data-stu-id="29c56-210">**Example**:</span></span>

    $filter=actor/objectId eq 'e8096343-86a2-4384-b43a-ebfdb17600ba'    


- - -
### <a name="targetname"></a><span data-ttu-id="29c56-211">target/name</span><span class="sxs-lookup"><span data-stu-id="29c56-211">target/name</span></span>
<span data-ttu-id="29c56-212">**Opérateurs pris en charge**: eq, contains, startsWith</span><span class="sxs-lookup"><span data-stu-id="29c56-212">**Supported operators**: eq, contains, startsWith</span></span>

<span data-ttu-id="29c56-213">**Exemple**:</span><span class="sxs-lookup"><span data-stu-id="29c56-213">**Example**:</span></span>

    $filter=targets/any(t: t/name eq 'some name')    

<span data-ttu-id="29c56-214">**Remarques**:</span><span class="sxs-lookup"><span data-stu-id="29c56-214">**Notes**:</span></span>

<span data-ttu-id="29c56-215">ne respecte pas la casse</span><span class="sxs-lookup"><span data-stu-id="29c56-215">Case-insensitive</span></span>

- - -
### <a name="targetupn"></a><span data-ttu-id="29c56-216">target/upn</span><span class="sxs-lookup"><span data-stu-id="29c56-216">target/upn</span></span>
<span data-ttu-id="29c56-217">**Opérateurs pris en charge**: eq, startsWith</span><span class="sxs-lookup"><span data-stu-id="29c56-217">**Supported operators**: eq, startsWith</span></span>

<span data-ttu-id="29c56-218">**Exemple**:</span><span class="sxs-lookup"><span data-stu-id="29c56-218">**Example**:</span></span>

    $filter=targets/any(t: startswith(t/Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity/userPrincipalName,'abc'))    

<span data-ttu-id="29c56-219">**Remarques**:</span><span class="sxs-lookup"><span data-stu-id="29c56-219">**Notes**:</span></span>

* <span data-ttu-id="29c56-220">ne respecte pas la casse</span><span class="sxs-lookup"><span data-stu-id="29c56-220">Case-insensitive</span></span>
* <span data-ttu-id="29c56-221">Vous avez besoin d’espace de noms complet tooadd hello lors de l’interrogation Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity</span><span class="sxs-lookup"><span data-stu-id="29c56-221">You need tooadd hello full namespace when querying  Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity</span></span>

- - -
### <a name="targetobjectid"></a><span data-ttu-id="29c56-222">target/objectid</span><span class="sxs-lookup"><span data-stu-id="29c56-222">target/objectId</span></span>
<span data-ttu-id="29c56-223">**Opérateurs pris en charge**: eq</span><span class="sxs-lookup"><span data-stu-id="29c56-223">**Supported operators**: eq</span></span>

<span data-ttu-id="29c56-224">**Exemple**:</span><span class="sxs-lookup"><span data-stu-id="29c56-224">**Example**:</span></span>

    $filter=targets/any(t: t/objectId eq 'e8096343-86a2-4384-b43a-ebfdb17600ba')    

- - -
### <a name="actorupn"></a><span data-ttu-id="29c56-225">actor/upn</span><span class="sxs-lookup"><span data-stu-id="29c56-225">actor/upn</span></span>
<span data-ttu-id="29c56-226">**Opérateurs pris en charge**: eq, startsWith</span><span class="sxs-lookup"><span data-stu-id="29c56-226">**Supported operators**: eq, startsWith</span></span>

<span data-ttu-id="29c56-227">**Exemple**:</span><span class="sxs-lookup"><span data-stu-id="29c56-227">**Example**:</span></span>

    $filter=startswith(actor/Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity/userPrincipalName,'abc')    

<span data-ttu-id="29c56-228">**Remarques**:</span><span class="sxs-lookup"><span data-stu-id="29c56-228">**Notes**:</span></span>

* <span data-ttu-id="29c56-229">ne respecte pas la casse</span><span class="sxs-lookup"><span data-stu-id="29c56-229">Case-insensitive</span></span> 
* <span data-ttu-id="29c56-230">Vous avez besoin d’espace de noms complet tooadd hello lors de l’interrogation Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity</span><span class="sxs-lookup"><span data-stu-id="29c56-230">You need tooadd hello full namespace when querying Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity</span></span>

- - -
## <a name="next-steps"></a><span data-ttu-id="29c56-231">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="29c56-231">Next Steps</span></span>
* <span data-ttu-id="29c56-232">Voulez-vous toosee exemples pour les activités filtrées système ?</span><span class="sxs-lookup"><span data-stu-id="29c56-232">Do you want toosee examples for filtered system activities?</span></span> <span data-ttu-id="29c56-233">Extraire hello [exemples d’API d’audit Azure Active Directory](active-directory-reporting-api-audit-samples.md).</span><span class="sxs-lookup"><span data-stu-id="29c56-233">Check out hello [Azure Active Directory audit API samples](active-directory-reporting-api-audit-samples.md).</span></span>
* <span data-ttu-id="29c56-234">Voulez-vous tooknow plus d’informations sur les API de création de rapports hello Azure AD ?</span><span class="sxs-lookup"><span data-stu-id="29c56-234">Do you want tooknow more about hello Azure AD reporting API?</span></span> <span data-ttu-id="29c56-235">Consultez [prise en main de hello API Azure Active Directory Reporting](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="29c56-235">See [Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>

