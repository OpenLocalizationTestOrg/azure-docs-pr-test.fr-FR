---
title: "Sécurité au niveau des lignes avec Power BI Embedded"
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
ms.openlocfilehash: 1cde5b9ee4c716af07d427d4d0eb3f0775d456ac
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="row-level-security-with-power-bi-embedded"></a><span data-ttu-id="7c266-103">Sécurité au niveau des lignes avec Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="7c266-103">Row level security with Power BI Embedded</span></span>

<span data-ttu-id="7c266-104">La sécurité au niveau des lignes (RLS) peut être utilisée pour restreindre l’accès des utilisateurs à des données particulières au sein d’un rapport ou d’un jeu de données, permettant à plusieurs utilisateurs différents d’utiliser le même rapport pour voir des données différentes.</span><span class="sxs-lookup"><span data-stu-id="7c266-104">Row level security (RLS) can be used to restrict user access to particular data within a report or dataset, allowing for multiple different users to use the same report while all seeing different data.</span></span> <span data-ttu-id="7c266-105">Power BI Embedded prend désormais en charge les jeux de données configurés avec la fonction RLS.</span><span class="sxs-lookup"><span data-stu-id="7c266-105">Power BI Embedded now supports datasets configured with RLS.</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-flow-1.png)

<span data-ttu-id="7c266-106">Pour tirer parti de la fonction RLS, il est important de comprendre trois concepts principaux : les utilisateurs, les rôles et les règles.</span><span class="sxs-lookup"><span data-stu-id="7c266-106">In order to take advantage of RLS, it’s important you understand three main concepts; Users, Roles, and Rules.</span></span> <span data-ttu-id="7c266-107">Examinons-les de plus près :</span><span class="sxs-lookup"><span data-stu-id="7c266-107">Let’s take a closer look at each:</span></span>

<span data-ttu-id="7c266-108">**Utilisateurs** : il s’agit des utilisateurs finaux réels visualisant les rapports.</span><span class="sxs-lookup"><span data-stu-id="7c266-108">**Users** –  These are the actual end-users viewing reports.</span></span> <span data-ttu-id="7c266-109">Dans Power BI Embedded, les utilisateurs sont identifiés par la propriété de nom d’utilisateur dans un jeton d’application.</span><span class="sxs-lookup"><span data-stu-id="7c266-109">In Power BI Embedded, users are identified by the username property in an App Token.</span></span>

<span data-ttu-id="7c266-110">**Rôles** : les utilisateurs appartiennent à des rôles.</span><span class="sxs-lookup"><span data-stu-id="7c266-110">**Roles** – Users belong to roles.</span></span> <span data-ttu-id="7c266-111">Un rôle fait office de conteneur pour les règles et peut avoir pour nom « Directeur des ventes » ou « Représentant ».</span><span class="sxs-lookup"><span data-stu-id="7c266-111">A role is a container for rules and can be named something like “Sales Manager” or “Sales Rep”.</span></span> <span data-ttu-id="7c266-112">Dans Power BI Embedded, les utilisateurs sont identifiés par la propriété de rôle dans un jeton d’application.</span><span class="sxs-lookup"><span data-stu-id="7c266-112">In Power BI Embedded, users are identified by the roles property in an App Token.</span></span>

<span data-ttu-id="7c266-113">**Règles** : les rôles ont des règles, et ces règles sont les filtres réels qui seront appliqués aux données.</span><span class="sxs-lookup"><span data-stu-id="7c266-113">**Rules** – Roles have rules, and those rules are the actual filters that are going to be applied to the data.</span></span> <span data-ttu-id="7c266-114">Cela peut être aussi simple que « Pays = États-Unis » ou bien quelque chose de plus dynamique.</span><span class="sxs-lookup"><span data-stu-id="7c266-114">This could be as simple as “Country = USA” or something much more dynamic.</span></span>

### <a name="example"></a><span data-ttu-id="7c266-115">Exemple</span><span class="sxs-lookup"><span data-stu-id="7c266-115">Example</span></span>

<span data-ttu-id="7c266-116">Pour le reste de cet article, nous fournirons un exemple de création RLS et d’utilisation au sein d’une application intégrée.</span><span class="sxs-lookup"><span data-stu-id="7c266-116">For the rest of this article, we’ll provide an example of authoring RLS, and then consuming that within an embedded application.</span></span> <span data-ttu-id="7c266-117">Notre exemple utilise le fichier PBIX [Exemple d’analyse des données de vente](http://go.microsoft.com/fwlink/?LinkID=780547) .</span><span class="sxs-lookup"><span data-stu-id="7c266-117">Our example uses the [Retail Analysis Sample](http://go.microsoft.com/fwlink/?LinkID=780547) PBIX file.</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-scenario-2.png)

<span data-ttu-id="7c266-118">Notre exemple d’analyse des données de vente affiche les ventes pour tous les magasins dans une chaîne de magasins spécifique.</span><span class="sxs-lookup"><span data-stu-id="7c266-118">Our Retail Analysis sample shows sales for all the stores in a particular retail chain.</span></span> <span data-ttu-id="7c266-119">Sans RLS, peu importe le directeur régional qui se connecte et visualise le rapport, les données affichées sont identiques.</span><span class="sxs-lookup"><span data-stu-id="7c266-119">Without RLS, no matter which district manager signs in and views the report, they’ll see the same data.</span></span> <span data-ttu-id="7c266-120">La direction a déterminé que chaque directeur régional devait uniquement voir les ventes des magasins qu’il gérait, et pour ce faire, nous devons donc avoir recours à RLS.</span><span class="sxs-lookup"><span data-stu-id="7c266-120">Senior management has determined each district manager should only see the sales for the stores they manage, and to do this, we can use RLS.</span></span>

<span data-ttu-id="7c266-121">RLS est créé dans Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="7c266-121">RLS is authored in Power BI Desktop.</span></span> <span data-ttu-id="7c266-122">Lorsque le jeu de données et les rapports sont ouverts, nous pouvons basculer vers la vue schématique pour afficher le schéma :</span><span class="sxs-lookup"><span data-stu-id="7c266-122">When the dataset and report are opened, we can switch to diagram view to see the schema:</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-3.png)

<span data-ttu-id="7c266-123">Voici quelques points à noter concernant ce schéma :</span><span class="sxs-lookup"><span data-stu-id="7c266-123">Here are a few things to notice with this schema:</span></span>

* <span data-ttu-id="7c266-124">Toutes les mesures, comme **Total Sales**, sont stockées dans la table de faits **Sales**.</span><span class="sxs-lookup"><span data-stu-id="7c266-124">All measures, like **Total Sales**, are stored in the **Sales** fact table.</span></span>
* <span data-ttu-id="7c266-125">Il existe quatre tables de dimension connexes supplémentaires : **Item**, **Time**, **Store** et **District**.</span><span class="sxs-lookup"><span data-stu-id="7c266-125">There are four additional related dimension tables: **Item**, **Time**, **Store**, and **District**.</span></span>
* <span data-ttu-id="7c266-126">Les flèches sur les lignes de relation indiquent de quelle façon les filtres peuvent circuler d’une table à l’autre.</span><span class="sxs-lookup"><span data-stu-id="7c266-126">The arrows on the relationship lines indicate which way filters can flow from one table to another.</span></span> <span data-ttu-id="7c266-127">Par exemple, si un filtre est placé sur **Time[Date]**, dans le schéma actuel, il filtre uniquement sur les valeurs de la table **Sales**.</span><span class="sxs-lookup"><span data-stu-id="7c266-127">For example, if a filter is placed on **Time[Date]**, in the current schema it would only filter down values in the **Sales** table.</span></span> <span data-ttu-id="7c266-128">Aucune autre table n’est affectée par ce filtre, car tous les flèches sur les lignes de relation pointent vers la table des ventes (et pas en direction opposée).</span><span class="sxs-lookup"><span data-stu-id="7c266-128">No other tables would be affected by this filter since all of the arrows on the relationship lines point to the sales table and not away.</span></span>
* <span data-ttu-id="7c266-129">La table **Région** indique qui est le directeur pour chaque région :</span><span class="sxs-lookup"><span data-stu-id="7c266-129">The **District** table indicates who the manager is for each district:</span></span>
  
  ![](media/power-bi-embedded-rls/pbi-embedded-rls-district-table-4.png)

<span data-ttu-id="7c266-130">Selon ce schéma, si nous appliquons un filtre à la colonne **District Manager** dans la table District, et si ce filtre correspond à l’utilisateur qui consulte le rapport, ce filtre est également appliqué aux tables **Store** et **Sales** de façon à afficher uniquement les données de ce directeur régional.</span><span class="sxs-lookup"><span data-stu-id="7c266-130">Based on this schema, if we apply a filter to the **District Manager** column in the District table, and if that filter matches the user viewing the report, that filter will also filter down the **Store** and **Sales** tables to only show data for that particular district manager.</span></span>

<span data-ttu-id="7c266-131">Voici comment procéder :</span><span class="sxs-lookup"><span data-stu-id="7c266-131">Here’s how:</span></span>

1. <span data-ttu-id="7c266-132">Dans l’onglet de modélisation, cliquez sur **Gérer les rôles**.</span><span class="sxs-lookup"><span data-stu-id="7c266-132">On the Modeling tab, click **Manage Roles**.</span></span>  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-modeling-tab-5.png)
2. <span data-ttu-id="7c266-133">Créer un rôle nommé **Directeur**.</span><span class="sxs-lookup"><span data-stu-id="7c266-133">Create a new role called **Manager**.</span></span>  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-manager-role-6.png)
3. <span data-ttu-id="7c266-134">Dans la table **District**, entrez l’expression DAX suivante : **[District Manager] = USERNAME()**</span><span class="sxs-lookup"><span data-stu-id="7c266-134">In the **District** table enter the following DAX expression: **[District Manager] = USERNAME()**</span></span>  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-manager-role-7.png)
4. <span data-ttu-id="7c266-135">Pour vérifier que les règles fonctionnent, sous l’onglet **Modélisation**, cliquez sur **Afficher comme rôles**, puis entrez ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="7c266-135">To make sure the rules are working, on the **Modeling** tab, click **View as Roles**, and then enter the following:</span></span>  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-view-as-roles-8.png)
   
   <span data-ttu-id="7c266-136">Les rapports affichent désormais les données comme si vous étiez connecté en tant que **Andrew Ma**.</span><span class="sxs-lookup"><span data-stu-id="7c266-136">The reports will now show data as if you were signed in as **Andrew Ma**.</span></span>

<span data-ttu-id="7c266-137">L’application du filtre comme nous l’avons indiqué retourne tous les enregistrements des tables **District**, **Store** et **Sales**.</span><span class="sxs-lookup"><span data-stu-id="7c266-137">Applying the filter, the way we did here, will filter down all records in the **District**, **Store**, and **Sales** tables.</span></span> <span data-ttu-id="7c266-138">Cependant, en raison de la direction du filtre sur les relations entre **Sales** et **Time**, **Sales** et **Item**, et **Item** et **Time**, les tables ne sont pas filtrées.</span><span class="sxs-lookup"><span data-stu-id="7c266-138">However, because of the filter direction on the relationships between **Sales** and **Time**, **Sales** and **Item**, and **Item** and **Time** tables will not be filtered down.</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-9.png)

<span data-ttu-id="7c266-139">Cela n’est peut-être pas problématique dans le cadre de notre recherche actuelle, mais si nous ne voulons pas que les directeurs voient des éléments dont la vente ne les concerne pas, nous pouvons activer le filtrage croisé bidirectionnel pour la relation et appliquer le filtre de sécurité dans les deux directions.</span><span class="sxs-lookup"><span data-stu-id="7c266-139">That may be ok for this requirement, however, if we don’t want managers to see items for which they don’t have any sales, we could turn on bidirectional cross-filtering for the relationship and flow the security filter in both directions.</span></span> <span data-ttu-id="7c266-140">Ceci est possible en modifiant la relation entre **Sales** et **Item**, comme ceci :</span><span class="sxs-lookup"><span data-stu-id="7c266-140">This can be done by editing the relationship between **Sales** and **Item**, like this:</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-edit-relationship-10.png)

<span data-ttu-id="7c266-141">À présent, les filtres peuvent également circuler entre la table Ventes et la table **Élément** :</span><span class="sxs-lookup"><span data-stu-id="7c266-141">Now, filters can also flow from the Sales table to the **Item** table:</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-11.png)

> [!NOTE]
> <span data-ttu-id="7c266-142">Si vous utilisez le mode DirectQuery pour vos données, vous devez activer le filtrage croisé bidirectionnel en sélectionnant ces deux options :</span><span class="sxs-lookup"><span data-stu-id="7c266-142">If you're using DirectQuery mode for your data, you will need to enable bidirectional-cross filtering by selecting these two options:</span></span>

1. <span data-ttu-id="7c266-143">**Fichier** -> **Options et paramètres** -> **Fonctionnalités en préversion** -> **Activer le filtrage croisé dans les deux directions pour DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="7c266-143">**File** -> **Options and Settings** -> **Preview Features** -> **Enable cross filtering in both directions for DirectQuery**.</span></span>
2. <span data-ttu-id="7c266-144">**Fichier** -> **Options et paramètres** -> **DirectQuery** -> **Autoriser la mesure sans restriction en mode DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="7c266-144">**File** -> **Options and Settings** -> **DirectQuery** -> **Allow unrestricted measure in DirectQuery mode**.</span></span>

<span data-ttu-id="7c266-145">Pour en savoir plus sur le filtrage croisé bidirectionnel, téléchargez le livre blanc [Bidirectional cross-filtering in SQL Server Analysis Services 2016 and Power BI Desktop](http://download.microsoft.com/download/2/7/8/2782DF95-3E0D-40CD-BFC8-749A2882E109/Bidirectional cross-filtering in Analysis Services 2016 and Power BI.docx).</span><span class="sxs-lookup"><span data-stu-id="7c266-145">To learn more about bidirectional cross-filtering, download the [Bidirectional cross-filtering in SQL Server Analysis Services 2016 and Power BI Desktop](http://download.microsoft.com/download/2/7/8/2782DF95-3E0D-40CD-BFC8-749A2882E109/Bidirectional cross-filtering in Analysis Services 2016 and Power BI.docx) whitepaper.</span></span>

<span data-ttu-id="7c266-146">Cela conclut le travail qui doit être fait dans Power BI Desktop, mais plusieurs autres tâches doivent encore être effectuées pour que les règles RLS définies puissent fonctionner dans Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="7c266-146">This wraps up all the work that needs to be done in Power BI Desktop, but there’s one more piece of work that needs to be done to make the RLS rules we defined work in Power BI Embedded.</span></span> <span data-ttu-id="7c266-147">Les utilisateurs sont authentifiés et autorisés par votre application, et les jetons d’application sont utilisés pour accorder l’accès utilisateur à un rapport Power BI Embedded spécifique.</span><span class="sxs-lookup"><span data-stu-id="7c266-147">Users are authenticated and authorized by your application and App tokens are used to grant that user access to a specific Power BI Embedded report.</span></span> <span data-ttu-id="7c266-148">Power BI Embedded ne dispose pas d’informations spécifiques relatives à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="7c266-148">Power BI Embedded doesn’t have any specific information on who your user is.</span></span> <span data-ttu-id="7c266-149">Pour que RLS fonctionne, vous devez transmettre des informations supplémentaires dans le cadre du jeton d’application :</span><span class="sxs-lookup"><span data-stu-id="7c266-149">For RLS to work, you’ll need to pass some additional context as part of your app token:</span></span>

* <span data-ttu-id="7c266-150">**username** (facultatif) : utilisé avec la fonction RLS, ceci est une chaîne qui peut aider à identifier l’utilisateur lors de l’application des règles RLS.</span><span class="sxs-lookup"><span data-stu-id="7c266-150">**username** (optional) – Used with RLS this is a string that can be used to help identify the user when applying RLS rules.</span></span> <span data-ttu-id="7c266-151">Voir Utilisation de la sécurité au niveau des lignes avec Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="7c266-151">See Using Row Level Security with Power BI Embedded</span></span>
* <span data-ttu-id="7c266-152">**roles** : chaîne contenant les rôles à sélectionner lors de l’application des règles de sécurité au niveau des lignes.</span><span class="sxs-lookup"><span data-stu-id="7c266-152">**roles** – A string containing the roles to select when applying Row Level Security rules.</span></span> <span data-ttu-id="7c266-153">Si vous transmettez plusieurs rôles, ils doivent l’être en tant que table de chaînes.</span><span class="sxs-lookup"><span data-stu-id="7c266-153">If passing more than one role, they should be passed as a string array.</span></span>

<span data-ttu-id="7c266-154">Vous créez le jeton à l’aide de la méthode [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#Microsoft_PowerBI_Security_PowerBIToken_CreateReportEmbedToken_System_String_System_String_System_String_System_DateTime_System_String_System_Collections_Generic_IEnumerable_System_String__).</span><span class="sxs-lookup"><span data-stu-id="7c266-154">You create the token by using the [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#Microsoft_PowerBI_Security_PowerBIToken_CreateReportEmbedToken_System_String_System_String_System_String_System_DateTime_System_String_System_Collections_Generic_IEnumerable_System_String__) method.</span></span> <span data-ttu-id="7c266-155">Si la propriété de nom d’utilisateur est présente, vous devez également transmettre au moins une valeur dans les rôles.</span><span class="sxs-lookup"><span data-stu-id="7c266-155">If the username property is present, you must also pass at least one value in roles.</span></span>

<span data-ttu-id="7c266-156">Par exemple, vous pouvez modifier EmbedSample.</span><span class="sxs-lookup"><span data-stu-id="7c266-156">For example, you could change the EmbedSample.</span></span> <span data-ttu-id="7c266-157">La ligne 55 de DashboardController peut être changée, de</span><span class="sxs-lookup"><span data-stu-id="7c266-157">DashboardController line 55 could be updated from</span></span>

    var embedToken = PowerBIToken.CreateReportEmbedToken(this.workspaceCollection, this.workspaceId, report.Id);

<span data-ttu-id="7c266-158">to</span><span class="sxs-lookup"><span data-stu-id="7c266-158">to</span></span>

    var embedToken = PowerBIToken.CreateReportEmbedToken(this.workspaceCollection, this.workspaceId, report.Id, "Andrew Ma", ["Manager"]);'

<span data-ttu-id="7c266-159">Le jeton d’application complet ressemblera à ceci :</span><span class="sxs-lookup"><span data-stu-id="7c266-159">The full app token will look something like this:</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-app-token-string-12.png)

<span data-ttu-id="7c266-160">Avec tous ces éléments, lorsqu’un utilisateur se connecte à notre application pour afficher ce rapport, il pourra seulement voir les données qu’il est autorisé à voir, comme défini par notre sécurité au niveau des lignes.</span><span class="sxs-lookup"><span data-stu-id="7c266-160">Now, with all the pieces together, when someone logs into our application to view this report, they’ll only be able to see the data that they are allowed to see, as defined by our row-level security.</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-dashboard-13.png)

## <a name="see-also"></a><span data-ttu-id="7c266-161">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="7c266-161">See also</span></span>

[<span data-ttu-id="7c266-162">Sécurité au niveau des lignes (RLS) avec Power BI</span><span class="sxs-lookup"><span data-stu-id="7c266-162">Row-level security (RLS) with Power</span></span>](https://powerbi.microsoft.com/en-us/documentation/powerbi-admin-rls/)  
[<span data-ttu-id="7c266-163">Authentification et autorisation dans Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="7c266-163">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="7c266-164">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="7c266-164">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="7c266-165">Exemple d’incorporation JavaScript</span><span class="sxs-lookup"><span data-stu-id="7c266-165">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
<span data-ttu-id="7c266-166">Des questions ?</span><span class="sxs-lookup"><span data-stu-id="7c266-166">More questions?</span></span> [<span data-ttu-id="7c266-167">Essayer la communauté Power BI</span><span class="sxs-lookup"><span data-stu-id="7c266-167">Try the Power BI Community</span></span>](http://community.powerbi.com/)

