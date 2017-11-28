---
title: "sécurité au niveau aaaRow avec Power BI Embedded"
description: "Détails sur la sécurité au niveau des lignes avec Power BI Embedded"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 7936ade5-2c75-435b-8314-ea7ca815867a
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: 384f78826ecc710cf8f101b251ae68b074f3e98b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="row-level-security-with-power-bi-embedded"></a><span data-ttu-id="82f7b-103">Sécurité au niveau des lignes avec Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="82f7b-103">Row level security with Power BI Embedded</span></span>

<span data-ttu-id="82f7b-104">Sécurité au niveau des lignes (RLS) peut être utilisé toorestrict utilisateur accès tooparticular données dans un rapport ou un jeu de données, permettant de plusieurs utilisateurs différents toouse hello même rapport lors de voir toutes les données de différents.</span><span class="sxs-lookup"><span data-stu-id="82f7b-104">Row level security (RLS) can be used toorestrict user access tooparticular data within a report or dataset, allowing for multiple different users toouse hello same report while all seeing different data.</span></span> <span data-ttu-id="82f7b-105">Power BI Embedded prend désormais en charge les jeux de données configurés avec la fonction RLS.</span><span class="sxs-lookup"><span data-stu-id="82f7b-105">Power BI Embedded now supports datasets configured with RLS.</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-flow-1.png)

<span data-ttu-id="82f7b-106">Dans parti tootake de commande de la sécurité RLS, il est important de que comprendre les trois concepts principaux ; Les utilisateurs, rôles et des règles.</span><span class="sxs-lookup"><span data-stu-id="82f7b-106">In order tootake advantage of RLS, it’s important you understand three main concepts; Users, Roles, and Rules.</span></span> <span data-ttu-id="82f7b-107">Examinons-les de plus près :</span><span class="sxs-lookup"><span data-stu-id="82f7b-107">Let’s take a closer look at each:</span></span>

<span data-ttu-id="82f7b-108">**Les utilisateurs** : ces utilisateurs finaux réelle de hello les rapports sont affichés.</span><span class="sxs-lookup"><span data-stu-id="82f7b-108">**Users** –  These are hello actual end-users viewing reports.</span></span> <span data-ttu-id="82f7b-109">Dans Power BI Embedded, les utilisateurs sont identifiés par la propriété de nom d’utilisateur hello dans un jeton d’application.</span><span class="sxs-lookup"><span data-stu-id="82f7b-109">In Power BI Embedded, users are identified by hello username property in an App Token.</span></span>

<span data-ttu-id="82f7b-110">**Rôles** – les utilisateurs appartiennent tooroles.</span><span class="sxs-lookup"><span data-stu-id="82f7b-110">**Roles** – Users belong tooroles.</span></span> <span data-ttu-id="82f7b-111">Un rôle fait office de conteneur pour les règles et peut avoir pour nom « Directeur des ventes » ou « Représentant ».</span><span class="sxs-lookup"><span data-stu-id="82f7b-111">A role is a container for rules and can be named something like “Sales Manager” or “Sales Rep”.</span></span> <span data-ttu-id="82f7b-112">Dans Power BI Embedded, les utilisateurs sont identifiés par la propriété de rôles hello dans un jeton d’application.</span><span class="sxs-lookup"><span data-stu-id="82f7b-112">In Power BI Embedded, users are identified by hello roles property in an App Token.</span></span>

<span data-ttu-id="82f7b-113">**Règles** : rôles ont des règles, et ces règles sont les filtres réel hello qui vont toobe appliqué toohello données.</span><span class="sxs-lookup"><span data-stu-id="82f7b-113">**Rules** – Roles have rules, and those rules are hello actual filters that are going toobe applied toohello data.</span></span> <span data-ttu-id="82f7b-114">Cela peut être aussi simple que « Pays = États-Unis » ou bien quelque chose de plus dynamique.</span><span class="sxs-lookup"><span data-stu-id="82f7b-114">This could be as simple as “Country = USA” or something much more dynamic.</span></span>

### <a name="example"></a><span data-ttu-id="82f7b-115">Exemple</span><span class="sxs-lookup"><span data-stu-id="82f7b-115">Example</span></span>

<span data-ttu-id="82f7b-116">Pour le reste de hello de cet article, nous vous fournirons un exemple de création de lignes et qui consomme ensuite au sein d’une application embedded.</span><span class="sxs-lookup"><span data-stu-id="82f7b-116">For hello rest of this article, we’ll provide an example of authoring RLS, and then consuming that within an embedded application.</span></span> <span data-ttu-id="82f7b-117">Notre exemple utilise hello [Retail Analysis Sample](http://go.microsoft.com/fwlink/?LinkID=780547) fichier PBIX.</span><span class="sxs-lookup"><span data-stu-id="82f7b-117">Our example uses hello [Retail Analysis Sample](http://go.microsoft.com/fwlink/?LinkID=780547) PBIX file.</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-scenario-2.png)

<span data-ttu-id="82f7b-118">Notre exemple analyse de vente au détail affiche les ventes pour tous les magasins hello dans une chaîne de vente au détail spécifique.</span><span class="sxs-lookup"><span data-stu-id="82f7b-118">Our Retail Analysis sample shows sales for all hello stores in a particular retail chain.</span></span> <span data-ttu-id="82f7b-119">Sans RLS, quel que soit le secteur manager se connecte et vues hello des rapports, il voit hello des mêmes données.</span><span class="sxs-lookup"><span data-stu-id="82f7b-119">Without RLS, no matter which district manager signs in and views hello report, they’ll see hello same data.</span></span> <span data-ttu-id="82f7b-120">Direction a déterminé que chaque directeur de district doit voir uniquement hello ventes des magasins hello qu’elles gèrent, toodo cela, nous pouvons utiliser des lignes.</span><span class="sxs-lookup"><span data-stu-id="82f7b-120">Senior management has determined each district manager should only see hello sales for hello stores they manage, and toodo this, we can use RLS.</span></span>

<span data-ttu-id="82f7b-121">RLS est créé dans Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="82f7b-121">RLS is authored in Power BI Desktop.</span></span> <span data-ttu-id="82f7b-122">Lors de l’ouverture hello dataset et le rapport, nous pouvons basculer toodiagram afficher le schéma hello toosee :</span><span class="sxs-lookup"><span data-stu-id="82f7b-122">When hello dataset and report are opened, we can switch toodiagram view toosee hello schema:</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-3.png)

<span data-ttu-id="82f7b-123">Voici quelques éléments toonotice, avec ce schéma :</span><span class="sxs-lookup"><span data-stu-id="82f7b-123">Here are a few things toonotice with this schema:</span></span>

* <span data-ttu-id="82f7b-124">Toutes les mesures, telles que **Total des ventes**, sont stockés dans hello **Sales** table de faits.</span><span class="sxs-lookup"><span data-stu-id="82f7b-124">All measures, like **Total Sales**, are stored in hello **Sales** fact table.</span></span>
* <span data-ttu-id="82f7b-125">Il existe quatre tables de dimension connexes supplémentaires : **Item**, **Time**, **Store** et **District**.</span><span class="sxs-lookup"><span data-stu-id="82f7b-125">There are four additional related dimension tables: **Item**, **Time**, **Store**, and **District**.</span></span>
* <span data-ttu-id="82f7b-126">Hello sur les lignes de relation hello indiquent la manière dont les filtres peuvent être transmis à partir d’une table tooanother.</span><span class="sxs-lookup"><span data-stu-id="82f7b-126">hello arrows on hello relationship lines indicate which way filters can flow from one table tooanother.</span></span> <span data-ttu-id="82f7b-127">Par exemple, si un filtre est placé sur **heure [Date]**, dans le schéma actuel de hello elle permet uniquement de filtrer les valeurs Bonjour **Sales** table.</span><span class="sxs-lookup"><span data-stu-id="82f7b-127">For example, if a filter is placed on **Time[Date]**, in hello current schema it would only filter down values in hello **Sales** table.</span></span> <span data-ttu-id="82f7b-128">Aucune autre table ne serait affectés par ce filtre toutes les flèches hello sur la table ventes du point toohello lignes relation hello et pas immédiatement.</span><span class="sxs-lookup"><span data-stu-id="82f7b-128">No other tables would be affected by this filter since all of hello arrows on hello relationship lines point toohello sales table and not away.</span></span>
* <span data-ttu-id="82f7b-129">Hello **District** table indique qui est responsable de hello pour chaque zone géographique :</span><span class="sxs-lookup"><span data-stu-id="82f7b-129">hello **District** table indicates who hello manager is for each district:</span></span>
  
  ![](media/power-bi-embedded-rls/pbi-embedded-rls-district-table-4.png)

<span data-ttu-id="82f7b-130">En fonction de ce schéma, si nous appliquons un filtre toohello **directeur de District** colonne hello table du secteur, et si ce filtre correspond à l’utilisateur hello affichage rapport de hello, que le filtre sera également filtrer vers le bas hello **magasin**et **Sales** tables tooonly affichent des données pour ce secteur particulier manager.</span><span class="sxs-lookup"><span data-stu-id="82f7b-130">Based on this schema, if we apply a filter toohello **District Manager** column in hello District table, and if that filter matches hello user viewing hello report, that filter will also filter down hello **Store** and **Sales** tables tooonly show data for that particular district manager.</span></span>

<span data-ttu-id="82f7b-131">Voici comment procéder :</span><span class="sxs-lookup"><span data-stu-id="82f7b-131">Here’s how:</span></span>

1. <span data-ttu-id="82f7b-132">Sous l’onglet de modélisation hello, cliquez sur **gérer les rôles**.</span><span class="sxs-lookup"><span data-stu-id="82f7b-132">On hello Modeling tab, click **Manage Roles**.</span></span>  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-modeling-tab-5.png)
2. <span data-ttu-id="82f7b-133">Créer un rôle nommé **Directeur**.</span><span class="sxs-lookup"><span data-stu-id="82f7b-133">Create a new role called **Manager**.</span></span>  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-manager-role-6.png)
3. <span data-ttu-id="82f7b-134">Bonjour **District** table entrez hello DAX expression suivante : **[directeur de District] = USERNAME()**</span><span class="sxs-lookup"><span data-stu-id="82f7b-134">In hello **District** table enter hello following DAX expression: **[District Manager] = USERNAME()**</span></span>  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-manager-role-7.png)
4. <span data-ttu-id="82f7b-135">les règles hello que toomake travaillez sur hello **modélisation** , cliquez sur **afficher comme rôles**et puis entrez hello qui suit :</span><span class="sxs-lookup"><span data-stu-id="82f7b-135">toomake sure hello rules are working, on hello **Modeling** tab, click **View as Roles**, and then enter hello following:</span></span>  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-view-as-roles-8.png)
   
   <span data-ttu-id="82f7b-136">Hello rapports maintenant affichent les données comme si vous étiez connecté en tant que **Andrew Ma**.</span><span class="sxs-lookup"><span data-stu-id="82f7b-136">hello reports will now show data as if you were signed in as **Andrew Ma**.</span></span>

<span data-ttu-id="82f7b-137">L’application hello filtre, méthode hello nous l’avons fait ici, filtre vers le bas tous les enregistrements de hello **District**, **magasin**, et **Sales** tables.</span><span class="sxs-lookup"><span data-stu-id="82f7b-137">Applying hello filter, hello way we did here, will filter down all records in hello **District**, **Store**, and **Sales** tables.</span></span> <span data-ttu-id="82f7b-138">Toutefois, en raison de la direction du filtrage hello sur les relations hello entre **Sales** et **temps**, **Sales** et **élément**et **Élément** et **temps** tables ne sont pas filtrés vers le bas.</span><span class="sxs-lookup"><span data-stu-id="82f7b-138">However, because of hello filter direction on hello relationships between **Sales** and **Time**, **Sales** and **Item**, and **Item** and **Time** tables will not be filtered down.</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-9.png)

<span data-ttu-id="82f7b-139">Qui peut être OK de cette exigence, cependant, si nous ne voulons pas gestionnaires toosee les éléments pour lesquels ils n’ont pas de ventes, nous pouvons activer bidirectionnel le filtrage croisé pour hello relation et flux hello filtre de sécurité dans les deux sens.</span><span class="sxs-lookup"><span data-stu-id="82f7b-139">That may be ok for this requirement, however, if we don’t want managers toosee items for which they don’t have any sales, we could turn on bidirectional cross-filtering for hello relationship and flow hello security filter in both directions.</span></span> <span data-ttu-id="82f7b-140">Cela est possible en modifiant la relation hello entre **Sales** et **élément**, comme suit :</span><span class="sxs-lookup"><span data-stu-id="82f7b-140">This can be done by editing hello relationship between **Sales** and **Item**, like this:</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-edit-relationship-10.png)

<span data-ttu-id="82f7b-141">Désormais, les filtres peuvent également se dérouler à partir de hello Sales table toohello **élément** table :</span><span class="sxs-lookup"><span data-stu-id="82f7b-141">Now, filters can also flow from hello Sales table toohello **Item** table:</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-11.png)

> [!NOTE]
> <span data-ttu-id="82f7b-142">Si vous utilisez le mode DirectQuery pour vos données, vous devez tooenable bidirectionnel cross filtrage en sélectionnant ces deux options :</span><span class="sxs-lookup"><span data-stu-id="82f7b-142">If you're using DirectQuery mode for your data, you will need tooenable bidirectional-cross filtering by selecting these two options:</span></span>

1. <span data-ttu-id="82f7b-143">**Fichier** -> **Options et paramètres** -> **Fonctionnalités en préversion** -> **Activer le filtrage croisé dans les deux directions pour DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="82f7b-143">**File** -> **Options and Settings** -> **Preview Features** -> **Enable cross filtering in both directions for DirectQuery**.</span></span>
2. <span data-ttu-id="82f7b-144">**Fichier** -> **Options et paramètres** -> **DirectQuery** -> **Autoriser la mesure sans restriction en mode DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="82f7b-144">**File** -> **Options and Settings** -> **DirectQuery** -> **Allow unrestricted measure in DirectQuery mode**.</span></span>

<span data-ttu-id="82f7b-145">toolearn plus d’informations sur le filtrage croisé bidirectionnel, téléchargement hello [filtrage croisé bidirectionnel dans SQL Server Analysis Services 2016 et Power BI Desktop](http://download.microsoft.com/download/2/7/8/2782DF95-3E0D-40CD-BFC8-749A2882E109/Bidirectional cross-filtering in Analysis Services 2016 and Power BI.docx) livre blanc.</span><span class="sxs-lookup"><span data-stu-id="82f7b-145">toolearn more about bidirectional cross-filtering, download hello [Bidirectional cross-filtering in SQL Server Analysis Services 2016 and Power BI Desktop](http://download.microsoft.com/download/2/7/8/2782DF95-3E0D-40CD-BFC8-749A2882E109/Bidirectional cross-filtering in Analysis Services 2016 and Power BI.docx) whitepaper.</span></span>

<span data-ttu-id="82f7b-146">Ceci conclut tout le travail hello doit toobe effectué dans Power BI Desktop, mais il existe un plus d’élément de travail qui doit toobe fait toomake hello RLS règles que nous avons défini le travail dans Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="82f7b-146">This wraps up all hello work that needs toobe done in Power BI Desktop, but there’s one more piece of work that needs toobe done toomake hello RLS rules we defined work in Power BI Embedded.</span></span> <span data-ttu-id="82f7b-147">Les utilisateurs sont authentifiés et autorisés par votre application et les jetons de l’application sont toogrant utilisé ce tooa spécifique Power BI Embedded rapport d’accès utilisateur.</span><span class="sxs-lookup"><span data-stu-id="82f7b-147">Users are authenticated and authorized by your application and App tokens are used toogrant that user access tooa specific Power BI Embedded report.</span></span> <span data-ttu-id="82f7b-148">Power BI Embedded ne dispose pas d’informations spécifiques relatives à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="82f7b-148">Power BI Embedded doesn’t have any specific information on who your user is.</span></span> <span data-ttu-id="82f7b-149">Pour la sécurité RLS toowork, vous aurez besoin de toopass un contexte supplémentaire dans le cadre de votre jeton d’application :</span><span class="sxs-lookup"><span data-stu-id="82f7b-149">For RLS toowork, you’ll need toopass some additional context as part of your app token:</span></span>

* <span data-ttu-id="82f7b-150">**nom d’utilisateur** (facultatif) : utilisé avec la sécurité RLS Ceci est une chaîne qui peut être utilisée toohelp identifier l’utilisateur de hello lors de l’application des règles RLS.</span><span class="sxs-lookup"><span data-stu-id="82f7b-150">**username** (optional) – Used with RLS this is a string that can be used toohelp identify hello user when applying RLS rules.</span></span> <span data-ttu-id="82f7b-151">Voir Utilisation de la sécurité au niveau des lignes avec Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="82f7b-151">See Using Row Level Security with Power BI Embedded</span></span>
* <span data-ttu-id="82f7b-152">**rôles** : une chaîne contenant hello rôles tooselect lors de l’application des règles de sécurité de niveau ligne.</span><span class="sxs-lookup"><span data-stu-id="82f7b-152">**roles** – A string containing hello roles tooselect when applying Row Level Security rules.</span></span> <span data-ttu-id="82f7b-153">Si vous transmettez plusieurs rôles, ils doivent l’être en tant que table de chaînes.</span><span class="sxs-lookup"><span data-stu-id="82f7b-153">If passing more than one role, they should be passed as a string array.</span></span>

<span data-ttu-id="82f7b-154">Vous créez un jeton de hello à l’aide de hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#Microsoft_PowerBI_Security_PowerBIToken_CreateReportEmbedToken_System_String_System_String_System_String_System_DateTime_System_String_System_Collections_Generic_IEnumerable_System_String__) (méthode).</span><span class="sxs-lookup"><span data-stu-id="82f7b-154">You create hello token by using hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#Microsoft_PowerBI_Security_PowerBIToken_CreateReportEmbedToken_System_String_System_String_System_String_System_DateTime_System_String_System_Collections_Generic_IEnumerable_System_String__) method.</span></span> <span data-ttu-id="82f7b-155">Si la propriété de nom d’utilisateur hello est présente, vous devez également passer au moins une valeur dans les rôles.</span><span class="sxs-lookup"><span data-stu-id="82f7b-155">If hello username property is present, you must also pass at least one value in roles.</span></span>

<span data-ttu-id="82f7b-156">Par exemple, vous pouvez modifier hello EmbedSample.</span><span class="sxs-lookup"><span data-stu-id="82f7b-156">For example, you could change hello EmbedSample.</span></span> <span data-ttu-id="82f7b-157">La ligne 55 de DashboardController peut être changée, de</span><span class="sxs-lookup"><span data-stu-id="82f7b-157">DashboardController line 55 could be updated from</span></span>

    var embedToken = PowerBIToken.CreateReportEmbedToken(this.workspaceCollection, this.workspaceId, report.Id);

<span data-ttu-id="82f7b-158">to</span><span class="sxs-lookup"><span data-stu-id="82f7b-158">to</span></span>

    var embedToken = PowerBIToken.CreateReportEmbedToken(this.workspaceCollection, this.workspaceId, report.Id, "Andrew Ma", ["Manager"]);'

<span data-ttu-id="82f7b-159">jeton d’application complet Hello ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="82f7b-159">hello full app token will look something like this:</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-app-token-string-12.png)

<span data-ttu-id="82f7b-160">Désormais, avec toutes les parties hello ensemble, lorsqu’un utilisateur connecte à notre tooview application ce rapport, ils uniquement serez qu’ils sont autorisés à toosee, les données de salutation toosee en mesure de tel que défini par la sécurité au niveau des lignes.</span><span class="sxs-lookup"><span data-stu-id="82f7b-160">Now, with all hello pieces together, when someone logs into our application tooview this report, they’ll only be able toosee hello data that they are allowed toosee, as defined by our row-level security.</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-dashboard-13.png)

## <a name="see-also"></a><span data-ttu-id="82f7b-161">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="82f7b-161">See also</span></span>

[<span data-ttu-id="82f7b-162">Sécurité au niveau des lignes (RLS) avec Power BI</span><span class="sxs-lookup"><span data-stu-id="82f7b-162">Row-level security (RLS) with Power</span></span>](https://powerbi.microsoft.com/en-us/documentation/powerbi-admin-rls/)  
[<span data-ttu-id="82f7b-163">Authentification et autorisation dans Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="82f7b-163">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="82f7b-164">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="82f7b-164">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="82f7b-165">Exemple d’incorporation JavaScript</span><span class="sxs-lookup"><span data-stu-id="82f7b-165">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
<span data-ttu-id="82f7b-166">Des questions ?</span><span class="sxs-lookup"><span data-stu-id="82f7b-166">More questions?</span></span> [<span data-ttu-id="82f7b-167">Essayez de hello Communauté Power BI</span><span class="sxs-lookup"><span data-stu-id="82f7b-167">Try hello Power BI Community</span></span>](http://community.powerbi.com/)

