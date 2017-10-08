---
title: "référence de l’API de rapport d’activité aaaAzure connexion dans Active Directory | Documents Microsoft"
description: "Informations de référence pour le rapport d’activité hello signe dans Azure Active Directory API"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ddcd9ae0-f6b7-4f13-a5e1-6cbf51a25634
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 8123f308a291503f2c61ac5de26696806c6402ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-sign-in-activity-report-api-reference"></a><span data-ttu-id="77f31-103">Référence d’API de création de rapports sur l’activité de connexion Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="77f31-103">Azure Active Directory sign-in activity report API reference</span></span>
<span data-ttu-id="77f31-104">Cette rubrique fait partie d’une collection de rubriques hello Azure Active Directory sur les API de création de rapports.</span><span class="sxs-lookup"><span data-stu-id="77f31-104">This topic is part of a collection of topics about hello Azure Active Directory reporting API.</span></span>  
<span data-ttu-id="77f31-105">Création de rapports Azure AD fournit une API qui vous permet de tooaccess données de rapport activité de connexion à l’aide de code ou les outils connexes.</span><span class="sxs-lookup"><span data-stu-id="77f31-105">Azure AD reporting provides you with an API that enables you tooaccess sign-in activity report data using code or related tools.</span></span>
<span data-ttu-id="77f31-106">Hello cette rubrique traite de tooprovide des informations de référence sur hello **API de rapport d’activité de connexion**.</span><span class="sxs-lookup"><span data-stu-id="77f31-106">hello scope of this topic is tooprovide you with reference information about hello **sign-in activity report API**.</span></span>

<span data-ttu-id="77f31-107">Consultez l'article :</span><span class="sxs-lookup"><span data-stu-id="77f31-107">See:</span></span>

* <span data-ttu-id="77f31-108">[Activités de connexion](active-directory-reporting-azure-portal.md#activity-reports) pour plus d’informations conceptuelles</span><span class="sxs-lookup"><span data-stu-id="77f31-108">[Sign-in activities](active-directory-reporting-azure-portal.md#activity-reports) for more conceptual information</span></span>
* <span data-ttu-id="77f31-109">[Prise en main de hello API Azure Active Directory Reporting](active-directory-reporting-api-getting-started.md) pour plus d’informations sur les API de création de rapports de hello.</span><span class="sxs-lookup"><span data-stu-id="77f31-109">[Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md) for more information about hello reporting API.</span></span>


## <a name="who-can-access-hello-api-data"></a><span data-ttu-id="77f31-110">Qui peut accéder à des données d’API hello ?</span><span class="sxs-lookup"><span data-stu-id="77f31-110">Who can access hello API data?</span></span>
* <span data-ttu-id="77f31-111">Les utilisateurs et principaux du Service de rôle d’administrateur de la sécurité ou de sécurité Reader hello</span><span class="sxs-lookup"><span data-stu-id="77f31-111">Users and Service Principals in hello Security Admin or Security Reader role</span></span>
* <span data-ttu-id="77f31-112">Administrateurs généraux</span><span class="sxs-lookup"><span data-stu-id="77f31-112">Global Admins</span></span>
* <span data-ttu-id="77f31-113">N’importe quelle application qui a l’autorisation tooaccess hello API (autorisation de l’application peut être configurés uniquement en fonction d’autorisation de l’administrateur Global)</span><span class="sxs-lookup"><span data-stu-id="77f31-113">Any app that has authorization tooaccess hello API (app authorization can be setup only based on Global Admin’s permission)</span></span>

<span data-ttu-id="77f31-114">accès tooconfigure pour un application tooaccess API de sécurité comme les événements d’ouverture de session, hello utilisation suivant des applications de hello tooadd PowerShell Principal du Service dans le rôle de sécurité Reader hello</span><span class="sxs-lookup"><span data-stu-id="77f31-114">tooconfigure access for an application tooaccess security APIs such as signin events, use hello following PowerShell tooadd hello applications Service Principal into hello Security Reader role</span></span>

```PowerShell
Connect-MsolService
$servicePrincipal = Get-MsolServicePrincipal -AppPrincipalId "<app client id>"
$role = Get-MsolRole | ? Name -eq "Security Reader"
Add-MsolRoleMember -RoleObjectId $role.ObjectId -RoleMemberType ServicePrincipal -RoleMemberObjectId $servicePrincipal.ObjectId
```

## <a name="prerequisites"></a><span data-ttu-id="77f31-115">Composants requis</span><span class="sxs-lookup"><span data-stu-id="77f31-115">Prerequisites</span></span>
<span data-ttu-id="77f31-116">Ce rapport par le biais de tooaccess hello API de création de rapports, vous devez avoir :</span><span class="sxs-lookup"><span data-stu-id="77f31-116">tooaccess this report through hello reporting API, you must have:</span></span>

* <span data-ttu-id="77f31-117">Une [édition Azure Active Directory Premium P1 ou P2](active-directory-editions.md)</span><span class="sxs-lookup"><span data-stu-id="77f31-117">An [Azure Active Directory Premium P1 or P2 edition](active-directory-editions.md)</span></span>
* <span data-ttu-id="77f31-118">Hello terminé [API reporting de conditions préalables tooaccess hello Azure AD](active-directory-reporting-api-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="77f31-118">Completed hello [prerequisites tooaccess hello Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span> 

## <a name="accessing-hello-api"></a><span data-ttu-id="77f31-119">L’accès aux API de hello</span><span class="sxs-lookup"><span data-stu-id="77f31-119">Accessing hello API</span></span>
<span data-ttu-id="77f31-120">Vous pouvez soit accéder à cette API via hello [Explorateur graphique](https://graphexplorer2.cloudapp.net) ou par programmation à l’aide, par exemple, PowerShell.</span><span class="sxs-lookup"><span data-stu-id="77f31-120">You can either access this API through hello [Graph Explorer](https://graphexplorer2.cloudapp.net) or programmatically using, for example, PowerShell.</span></span> <span data-ttu-id="77f31-121">Dans l’ordre pour PowerShell toocorrectly interpréter la syntaxe de filtre OData hello utilisée dans les appels de Graph AAD REST, vous devez utiliser hello backtick (aka : accent grave) caractère trop « caractère d’échappement « hello $.</span><span class="sxs-lookup"><span data-stu-id="77f31-121">In order for PowerShell toocorrectly interpret hello OData filter syntax used in AAD Graph REST calls, you must use hello backtick (aka: grave accent) character too“escape” hello $ character.</span></span> <span data-ttu-id="77f31-122">sert de caractère de guillemet inversé Hello [caractère d’échappement de PowerShell](https://technet.microsoft.com/library/hh847755.aspx), ce qui permet de PowerShell toodo une interprétation littéral de caractère de $ hello et éviter toute confusion entre elle en tant que nom d’une variable PowerShell (ie : $filter).</span><span class="sxs-lookup"><span data-stu-id="77f31-122">hello backtick character serves as [PowerShell’s escape character](https://technet.microsoft.com/library/hh847755.aspx), allowing PowerShell toodo a literal interpretation of hello $ character, and avoid confusing it as a PowerShell variable name (ie: $filter).</span></span>

<span data-ttu-id="77f31-123">Hello de cette rubrique concerne les hello Explorateur graphique.</span><span class="sxs-lookup"><span data-stu-id="77f31-123">hello focus of this topic is on hello Graph Explorer.</span></span> <span data-ttu-id="77f31-124">Pour obtenir un exemple PowerShell, consultez ce [script PowerShell](active-directory-reporting-api-sign-in-activity-samples.md#powershell-script).</span><span class="sxs-lookup"><span data-stu-id="77f31-124">For a PowerShell example, see this [PowerShell script](active-directory-reporting-api-sign-in-activity-samples.md#powershell-script).</span></span>

## <a name="api-endpoint"></a><span data-ttu-id="77f31-125">Point de terminaison d’API</span><span class="sxs-lookup"><span data-stu-id="77f31-125">API Endpoint</span></span>
<span data-ttu-id="77f31-126">Vous pouvez accéder à cette API à l’aide de hello suivant l’URI de base :</span><span class="sxs-lookup"><span data-stu-id="77f31-126">You can access this API using hello following base URI:</span></span>  

    https://graph.windows.net/contoso.com/activities/signinEvents?api-version=beta  



<span data-ttu-id="77f31-127">En raison de toohello le volume de données, cette API a une limite d’un million d’enregistrements retournés.</span><span class="sxs-lookup"><span data-stu-id="77f31-127">Due toohello volume of data, this API has a limit of one million returned records.</span></span> 

<span data-ttu-id="77f31-128">Cet appel retourne les données de hello dans des lots.</span><span class="sxs-lookup"><span data-stu-id="77f31-128">This call returns hello data in batches.</span></span> <span data-ttu-id="77f31-129">Chaque lot comporte un maximum de 1 000 enregistrements.</span><span class="sxs-lookup"><span data-stu-id="77f31-129">Each batch has a maximum of 1000 records.</span></span>  
<span data-ttu-id="77f31-130">tooget hello suivant lot d’enregistrements, utilisez hello de lien suivant.</span><span class="sxs-lookup"><span data-stu-id="77f31-130">tooget hello next batch of records, use hello Next link.</span></span> <span data-ttu-id="77f31-131">Obtenir hello [skiptoken](https://msdn.microsoft.com/library/dd942121.aspx) plus d’informations à partir de hello premier ensemble d’enregistrements retournés.</span><span class="sxs-lookup"><span data-stu-id="77f31-131">Get hello [skiptoken](https://msdn.microsoft.com/library/dd942121.aspx) information from hello first set of returned records.</span></span> <span data-ttu-id="77f31-132">jeton d’évitement Hello sera à fin hello hello du jeu de résultats.</span><span class="sxs-lookup"><span data-stu-id="77f31-132">hello skip token will be at hello end of hello result set.</span></span>  

    https://graph.windows.net/$tenantdomain/activities/signinEvents?api-version=beta&%24skiptoken=-1339686058


## <a name="supported-filters"></a><span data-ttu-id="77f31-133">Filtres pris en charge</span><span class="sxs-lookup"><span data-stu-id="77f31-133">Supported filters</span></span>
<span data-ttu-id="77f31-134">Vous pouvez réduire nombre hello d’enregistrements retournés par une API appeler sous forme d’un filtre.</span><span class="sxs-lookup"><span data-stu-id="77f31-134">You can narrow down hello number of records that are returned by an API call in form of a filter.</span></span>  
<span data-ttu-id="77f31-135">Connectez-vous API hello suivant des filtres, les données associées sont prises en charge :</span><span class="sxs-lookup"><span data-stu-id="77f31-135">For sign-in API related data, hello following filters are supported:</span></span>

* <span data-ttu-id="77f31-136">**$top =\<retourné de nombre d’enregistrements toobe\>**  -nombre de hello toolimit d’enregistrements renvoyés.</span><span class="sxs-lookup"><span data-stu-id="77f31-136">**$top=\<number of records toobe returned\>** - toolimit hello number of returned records.</span></span> <span data-ttu-id="77f31-137">Il s’agit d’une opération coûteuse.</span><span class="sxs-lookup"><span data-stu-id="77f31-137">This is an expensive operation.</span></span> <span data-ttu-id="77f31-138">Vous ne devez pas utiliser ce filtre si vous souhaitez tooreturn des milliers d’objets.</span><span class="sxs-lookup"><span data-stu-id="77f31-138">You should not use this filter if you want tooreturn thousands of objects.</span></span>  
* <span data-ttu-id="77f31-139">**$filter =\<votre instruction de filtrage\>**  -toospecify, sur la base de hello de champs de filtre pris en charge, type hello d’enregistrements qui vous intéressent</span><span class="sxs-lookup"><span data-stu-id="77f31-139">**$filter=\<your filter statement\>** - toospecify, on hello basis of supported filter fields, hello type of records you care about</span></span>

## <a name="supported-filter-fields-and-operators"></a><span data-ttu-id="77f31-140">Opérateurs et champs de filtre pris en charge</span><span class="sxs-lookup"><span data-stu-id="77f31-140">Supported filter fields and operators</span></span>
<span data-ttu-id="77f31-141">type de hello toospecify d’enregistrements qui que vous intéressent, vous pouvez générer une instruction de filtrage qui peut contenir un ou une combinaison de hello suivant des champs de filtre :</span><span class="sxs-lookup"><span data-stu-id="77f31-141">toospecify hello type of records you care about, you can build a filter statement that can contain either one or a combination of hello following filter fields:</span></span>

* <span data-ttu-id="77f31-142">[signinDateTime](#signindatetime) : définit une date ou une plage de dates</span><span class="sxs-lookup"><span data-stu-id="77f31-142">[signinDateTime](#signindatetime) - defines a date or date range</span></span>
* <span data-ttu-id="77f31-143">[userId](#userid) -définit. un hello d’utilisateur spécifique en fonction de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="77f31-143">[userId](#userid) - defines a specific user based hello user's ID.</span></span>
* <span data-ttu-id="77f31-144">[userPrincipalName](#userprincipalname) -définit le nom d’un utilisateur spécifique en fonction hello utilisateur utilisateur principal (UPN)</span><span class="sxs-lookup"><span data-stu-id="77f31-144">[userPrincipalName](#userprincipalname) - defines a specific user based hello user's user principal name (UPN)</span></span>
* <span data-ttu-id="77f31-145">[appId](#appid) -définit l’ID de l’application de hello une application spécifique en fonction</span><span class="sxs-lookup"><span data-stu-id="77f31-145">[appId](#appid) - defines a specific app based hello app's ID</span></span>
* <span data-ttu-id="77f31-146">[appDisplayName](#appdisplayname) -définit le nom d’affichage d’une application hello application spécifique en fonction</span><span class="sxs-lookup"><span data-stu-id="77f31-146">[appDisplayName](#appdisplayname) - defines a specific app based hello app's display name</span></span>
* <span data-ttu-id="77f31-147">[loginStatus](#loginStatus) -définit l’état de hello de connexions de hello (réussite / échec)</span><span class="sxs-lookup"><span data-stu-id="77f31-147">[loginStatus](#loginStatus) - defines hello status of hello logins (success / failure)</span></span>

> [!NOTE]
> <span data-ttu-id="77f31-148">Lorsque vous utilisez l’Explorateur graphique, hello vous devez hello toouse correct de cas pour chaque lettre est vos champs de filtre.</span><span class="sxs-lookup"><span data-stu-id="77f31-148">When using Graph Explorer, you hello need toouse hello correct case for each letter is your filter fields.</span></span>
> 
> 

<span data-ttu-id="77f31-149">toonarrow étendue hello Hello a retourné des données, vous pouvez créer des combinaisons de filtres de hello pris en charge et les champs de filtre.</span><span class="sxs-lookup"><span data-stu-id="77f31-149">toonarrow down hello scope of hello returned data, you can build combinations of hello supported filters and filter fields.</span></span> <span data-ttu-id="77f31-150">Par exemple, hello instruction suivante retourne hello top 10 enregistrements entre le 1er juillet 2016 et juillet 2016 de 6 :</span><span class="sxs-lookup"><span data-stu-id="77f31-150">For example, hello following statement returns hello top 10 records between July 1st 2016 and July 6th 2016:</span></span>

    https://graph.windows.net/contoso.com/activities/signinEvents?api-version=beta&$top=10&$filter=signinDateTime+ge+2016-07-01T17:05:21Z+and+signinDateTime+le+2016-07-07T00:00:00Z


- - -
### <a name="signindatetime"></a><span data-ttu-id="77f31-151">signinDateTime</span><span class="sxs-lookup"><span data-stu-id="77f31-151">signinDateTime</span></span>
<span data-ttu-id="77f31-152">**Opérateurs pris en charge**: eq, ge, le, gt, lt</span><span class="sxs-lookup"><span data-stu-id="77f31-152">**Supported operators**: eq, ge, le, gt, lt</span></span>

<span data-ttu-id="77f31-153">**Exemple**:</span><span class="sxs-lookup"><span data-stu-id="77f31-153">**Example**:</span></span>

<span data-ttu-id="77f31-154">Utilisation d’une date spécifique</span><span class="sxs-lookup"><span data-stu-id="77f31-154">Using a specific date</span></span>

    $filter=signinDateTime+eq+2016-04-25T23:59:00Z    



<span data-ttu-id="77f31-155">Utilisation d’une plage de dates</span><span class="sxs-lookup"><span data-stu-id="77f31-155">Using a date range</span></span>    

    $filter=signinDateTime+ge+2016-07-01T17:05:21Z+and+signinDateTime+le+2016-07-07T17:05:21Z


<span data-ttu-id="77f31-156">**Remarques**:</span><span class="sxs-lookup"><span data-stu-id="77f31-156">**Notes**:</span></span>

<span data-ttu-id="77f31-157">paramètre de Hello datetime doit être au format UTC de hello</span><span class="sxs-lookup"><span data-stu-id="77f31-157">hello datetime parameter should be in hello UTC format</span></span> 

- - -
### <a name="userid"></a><span data-ttu-id="77f31-158">userId</span><span class="sxs-lookup"><span data-stu-id="77f31-158">userId</span></span>
<span data-ttu-id="77f31-159">**Opérateurs pris en charge**: eq</span><span class="sxs-lookup"><span data-stu-id="77f31-159">**Supported operators**: eq</span></span>

<span data-ttu-id="77f31-160">**Exemple**:</span><span class="sxs-lookup"><span data-stu-id="77f31-160">**Example**:</span></span>

    $filter=userId+eq+’00000000-0000-0000-0000-000000000000’

<span data-ttu-id="77f31-161">**Remarques**:</span><span class="sxs-lookup"><span data-stu-id="77f31-161">**Notes**:</span></span>

<span data-ttu-id="77f31-162">Hello Id_utilisateur est une valeur de chaîne</span><span class="sxs-lookup"><span data-stu-id="77f31-162">hello value of userId is a string value</span></span>

- - -
### <a name="userprincipalname"></a><span data-ttu-id="77f31-163">userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="77f31-163">userPrincipalName</span></span>
<span data-ttu-id="77f31-164">**Opérateurs pris en charge**: eq</span><span class="sxs-lookup"><span data-stu-id="77f31-164">**Supported operators**: eq</span></span>

<span data-ttu-id="77f31-165">**Exemple**:</span><span class="sxs-lookup"><span data-stu-id="77f31-165">**Example**:</span></span>

    $filter=userPrincipalName+eq+'audrey.oliver@wingtiptoysonline.com' 


<span data-ttu-id="77f31-166">**Remarques**:</span><span class="sxs-lookup"><span data-stu-id="77f31-166">**Notes**:</span></span>

<span data-ttu-id="77f31-167">valeur Hello userPrincipalName est une valeur de chaîne</span><span class="sxs-lookup"><span data-stu-id="77f31-167">hello value of userPrincipalName is a string value</span></span>

- - -
### <a name="appid"></a><span data-ttu-id="77f31-168">appId</span><span class="sxs-lookup"><span data-stu-id="77f31-168">appId</span></span>
<span data-ttu-id="77f31-169">**Opérateurs pris en charge**: eq</span><span class="sxs-lookup"><span data-stu-id="77f31-169">**Supported operators**: eq</span></span>

<span data-ttu-id="77f31-170">**Exemple**:</span><span class="sxs-lookup"><span data-stu-id="77f31-170">**Example**:</span></span>

    $filter=appId+eq+’00000000-0000-0000-0000-000000000000’



<span data-ttu-id="77f31-171">**Remarques**:</span><span class="sxs-lookup"><span data-stu-id="77f31-171">**Notes**:</span></span>

<span data-ttu-id="77f31-172">valeur Hello appId est une valeur de chaîne</span><span class="sxs-lookup"><span data-stu-id="77f31-172">hello value of appId is a string value</span></span>

- - -
### <a name="appdisplayname"></a><span data-ttu-id="77f31-173">appDisplayName</span><span class="sxs-lookup"><span data-stu-id="77f31-173">appDisplayName</span></span>
<span data-ttu-id="77f31-174">**Opérateurs pris en charge**: eq</span><span class="sxs-lookup"><span data-stu-id="77f31-174">**Supported operators**: eq</span></span>

<span data-ttu-id="77f31-175">**Exemple**:</span><span class="sxs-lookup"><span data-stu-id="77f31-175">**Example**:</span></span>

    $filter=appDisplayName+eq+'Azure+Portal' 


<span data-ttu-id="77f31-176">**Remarques**:</span><span class="sxs-lookup"><span data-stu-id="77f31-176">**Notes**:</span></span>

<span data-ttu-id="77f31-177">valeur Hello appDisplayName est une valeur de chaîne</span><span class="sxs-lookup"><span data-stu-id="77f31-177">hello value of appDisplayName is a string value</span></span>

- - -
### <a name="loginstatus"></a><span data-ttu-id="77f31-178">loginStatus</span><span class="sxs-lookup"><span data-stu-id="77f31-178">loginStatus</span></span>
<span data-ttu-id="77f31-179">**Opérateurs pris en charge**: eq</span><span class="sxs-lookup"><span data-stu-id="77f31-179">**Supported operators**: eq</span></span>

<span data-ttu-id="77f31-180">**Exemple**:</span><span class="sxs-lookup"><span data-stu-id="77f31-180">**Example**:</span></span>

    $filter=loginStatus+eq+'1'  


<span data-ttu-id="77f31-181">**Remarques**:</span><span class="sxs-lookup"><span data-stu-id="77f31-181">**Notes**:</span></span>

<span data-ttu-id="77f31-182">Il existe deux options pour hello loginStatus : 0 - Réussite, 1 - Échec</span><span class="sxs-lookup"><span data-stu-id="77f31-182">There are two options for hello loginStatus: 0 - success, 1 - failure</span></span>

- - -
## <a name="next-steps"></a><span data-ttu-id="77f31-183">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="77f31-183">Next steps</span></span>
* <span data-ttu-id="77f31-184">Voulez-vous toosee exemples pour les activités filtrées connectez-vous ?</span><span class="sxs-lookup"><span data-stu-id="77f31-184">Do you want toosee examples for filtered sign-in activities?</span></span> <span data-ttu-id="77f31-185">Extraire hello [exemples de rapports API d’activité de connexion Azure Active Directory](active-directory-reporting-api-sign-in-activity-samples.md).</span><span class="sxs-lookup"><span data-stu-id="77f31-185">Check out hello [Azure Active Directory sign-in activity report API samples](active-directory-reporting-api-sign-in-activity-samples.md).</span></span>
* <span data-ttu-id="77f31-186">Voulez-vous tooknow plus d’informations sur les API de création de rapports hello Azure AD ?</span><span class="sxs-lookup"><span data-stu-id="77f31-186">Do you want tooknow more about hello Azure AD reporting API?</span></span> <span data-ttu-id="77f31-187">Consultez [prise en main de hello API Azure Active Directory Reporting](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="77f31-187">See [Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>

