---
<span data-ttu-id="2fb5a-101">titre : aaa « leçon du didacticiel Azure Analysis Services 11 : créer des rôles | Description de Microsoft Docs » : décrit comment les rôles toocreate dans hello projet du didacticiel Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="2fb5a-101">title: aaa"Azure Analysis Services tutorial lesson 11: Create roles | Microsoft Docs" description: Describes how toocreate roles in hello Azure Analysis Services tutorial project.</span></span> <span data-ttu-id="2fb5a-102">Services : analysis services documentationcenter : '' auteur : minewiskan manager : erikre éditeur : '' balises : ».</span><span class="sxs-lookup"><span data-stu-id="2fb5a-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="2fb5a-103">MS.AssetId : ms.service : ms.devlang d’analysis services : NA ms.topic : get-started-article ms.tgt_pltfrm : NA ms.workload : na ms.date : 26/05/2017 ms.author : owend</span><span class="sxs-lookup"><span data-stu-id="2fb5a-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span></span>
---
# <a name="lesson-11-create-roles"></a><span data-ttu-id="2fb5a-104">Leçon 11 : Créer des rôles</span><span class="sxs-lookup"><span data-stu-id="2fb5a-104">Lesson 11: Create roles</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="2fb5a-105">Dans cette leçon, vous allez créer des rôles.</span><span class="sxs-lookup"><span data-stu-id="2fb5a-105">In this lesson, you create roles.</span></span> <span data-ttu-id="2fb5a-106">Les rôles fournissent la sécurité de données et l’objet de base de données de modèle en limitant l’accès tooonly les utilisateurs qui sont membres du rôle.</span><span class="sxs-lookup"><span data-stu-id="2fb5a-106">Roles provide model database object and data security by limiting access tooonly those users that are role members.</span></span> <span data-ttu-id="2fb5a-107">Chaque rôle est défini avec une autorisation unique : aucune autorisation, autorisation de lecture, autorisation de lecture et de traitement, autorisation de traitement ou autorisation d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="2fb5a-107">Each role is defined with a single permission: None, Read, Read and Process, Process, or Administrator.</span></span> <span data-ttu-id="2fb5a-108">Les rôles peuvent être définis lors de la création des modèles à l’aide du Gestionnaire de rôles.</span><span class="sxs-lookup"><span data-stu-id="2fb5a-108">Roles can be defined during model authoring by using Role Manager.</span></span> <span data-ttu-id="2fb5a-109">Une fois un modèle déployé, vous pouvez gérer des rôles à l’aide de SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="2fb5a-109">After a model has been deployed, you can manage roles by using SQL Server Management Studio (SSMS).</span></span> <span data-ttu-id="2fb5a-110">toolearn, voir [rôles](https://docs.microsoft.com/sql/analysis-services/tabular-models/roles-ssas-tabular).</span><span class="sxs-lookup"><span data-stu-id="2fb5a-110">toolearn more, see [Roles](https://docs.microsoft.com/sql/analysis-services/tabular-models/roles-ssas-tabular).</span></span>
  
> [!NOTE]  
> <span data-ttu-id="2fb5a-111">Création de rôles est toocomplete n’est pas nécessaire de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="2fb5a-111">Creating roles is not necessary toocomplete this tutorial.</span></span> <span data-ttu-id="2fb5a-112">Par défaut, compte hello que vous êtes actuellement connecté dispose des privilèges d’administrateur sur le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="2fb5a-112">By default, hello account you are currently logged in with has Administrator privileges on hello model.</span></span> <span data-ttu-id="2fb5a-113">Toutefois, pour les autres utilisateurs toobrowse de votre organisation à l’aide d’un client de création de rapports, vous devez créer au moins un rôle avec la lecture des autorisations et ajouter ces utilisateurs en tant que membres.</span><span class="sxs-lookup"><span data-stu-id="2fb5a-113">However, for other users in your organization toobrowse by using a reporting client, you must create at least one role with Read permissions and add those users as members.</span></span>  
  
<span data-ttu-id="2fb5a-114">Vous devez créer trois rôles :</span><span class="sxs-lookup"><span data-stu-id="2fb5a-114">You create three roles:</span></span>  
  
-   <span data-ttu-id="2fb5a-115">**Responsable des ventes** – ce rôle peut inclure des utilisateurs de votre organisation pour lequel vous souhaitez que les données et les objets de modèle toohave tooall de l’autorisation en lecture.</span><span class="sxs-lookup"><span data-stu-id="2fb5a-115">**Sales Manager** – This role can include users in your organization for which you want toohave Read permission tooall model objects and data.</span></span>  
  
-   <span data-ttu-id="2fb5a-116">**Analyste des ventes aux États-Unis** – ce rôle peut inclure des utilisateurs de votre organisation pour lequel vous ne souhaitez que les données en mesure de toobrowse toobe liés toosales Bonjour États-Unis.</span><span class="sxs-lookup"><span data-stu-id="2fb5a-116">**Sales Analyst US** – This role can include users in your organization for which you want only toobe able toobrowse data related toosales in hello United States.</span></span> <span data-ttu-id="2fb5a-117">Pour ce rôle, vous utilisez un toodefine de formule DAX un *filtre de lignes*, qui limite les membres toobrowse uniquement les données hello États-Unis.</span><span class="sxs-lookup"><span data-stu-id="2fb5a-117">For this role, you use a DAX formula toodefine a *Row Filter*, which restricts members toobrowse data only for hello United States.</span></span>  
  
-   <span data-ttu-id="2fb5a-118">**Administrateur** – ce rôle peut inclure des utilisateurs pour lesquels vous souhaitez toohave les autorisations d’administrateur, ce qui permet un accès illimité et autorisations tooperform des tâches d’administration sur la base de données model hello.</span><span class="sxs-lookup"><span data-stu-id="2fb5a-118">**Administrator** – This role can include users for which you want toohave Administrator permission, which allows unlimited access and permissions tooperform administrative tasks on hello model database.</span></span>  
  
<span data-ttu-id="2fb5a-119">Étant donné que les comptes d’utilisateur et de groupe Windows dans votre organisation sont uniques, vous pouvez ajouter des comptes à partir de toomembers de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="2fb5a-119">Because Windows user and group accounts in your organization are unique, you can add accounts from your particular organization toomembers.</span></span> <span data-ttu-id="2fb5a-120">Toutefois, pour ce didacticiel, vous pouvez également laisser les membres hello vide.</span><span class="sxs-lookup"><span data-stu-id="2fb5a-120">However, for this tutorial, you can also leave hello members blank.</span></span> <span data-ttu-id="2fb5a-121">Test d’effet hello de chaque rôle plus tard dans la leçon 12 : analyser dans Excel.</span><span class="sxs-lookup"><span data-stu-id="2fb5a-121">You test hello effect of each role later in Lesson 12: Analyze in Excel.</span></span>  
  
<span data-ttu-id="2fb5a-122">Estimé temps toocomplete cette leçon : **15 minutes**</span><span class="sxs-lookup"><span data-stu-id="2fb5a-122">Estimated time toocomplete this lesson: **15 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="2fb5a-123">Composants requis</span><span class="sxs-lookup"><span data-stu-id="2fb5a-123">Prerequisites</span></span>  
<span data-ttu-id="2fb5a-124">Cette rubrique fait partie d’un didacticiel de modélisation tabulaire, qui doit être suivi dans l’ordre prévu.</span><span class="sxs-lookup"><span data-stu-id="2fb5a-124">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="2fb5a-125">Avant d’effectuer les tâches de hello dans cette leçon, vous devez avoir terminé les leçon précédente hello : [leçon 10 : créer des partitions](../tutorials/aas-lesson-10-create-partitions.md).</span><span class="sxs-lookup"><span data-stu-id="2fb5a-125">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 10: Create partitions](../tutorials/aas-lesson-10-create-partitions.md).</span></span>  
  
## <a name="create-roles"></a><span data-ttu-id="2fb5a-126">Créer des rôles</span><span class="sxs-lookup"><span data-stu-id="2fb5a-126">Create roles</span></span>  
  
#### <a name="toocreate-a-sales-manager-user-role"></a><span data-ttu-id="2fb5a-127">toocreate un rôle d’utilisateur Sales Manager</span><span class="sxs-lookup"><span data-stu-id="2fb5a-127">toocreate a Sales Manager user role</span></span>  
  
1.  <span data-ttu-id="2fb5a-128">Dans l’Explorateur de modèle tabulaire, cliquez avec le bouton droit sur **Rôles** > **Rôles**.</span><span class="sxs-lookup"><span data-stu-id="2fb5a-128">In Tabular Model Explorer, right-click **Roles** > **Roles**.</span></span>  
  
2.  <span data-ttu-id="2fb5a-129">Dans le Gestionnaire de rôles, cliquez sur **Nouveau**.</span><span class="sxs-lookup"><span data-stu-id="2fb5a-129">In Role Manager, click **New**.</span></span>  
  
3.  <span data-ttu-id="2fb5a-130">Cliquez sur Nouveau rôle de hello, puis dans hello **nom** colonne, renommez le rôle de hello trop**responsable des ventes**.</span><span class="sxs-lookup"><span data-stu-id="2fb5a-130">Click hello new role, and then in hello **Name** column, rename hello role too**Sales Manager**.</span></span>  
  
4.  <span data-ttu-id="2fb5a-131">Bonjour **autorisations** colonne, cliquez sur la liste déroulante hello et sélectionnez hello **en lecture** autorisation.</span><span class="sxs-lookup"><span data-stu-id="2fb5a-131">In hello **Permissions** column, click hello dropdown list, and then select hello **Read** permission.</span></span> 

    ![aas-lesson11-new-role](../tutorials/media/aas-lesson11-new-role.png) 
  
5.  <span data-ttu-id="2fb5a-133">Facultatif : Cliquez sur hello **membres** onglet, puis cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="2fb5a-133">Optional: Click hello **Members** tab, and then click **Add**.</span></span> <span data-ttu-id="2fb5a-134">Bonjour **sélectionner des utilisateurs ou groupes** boîte de dialogue, entrez hello utilisateurs ou groupes Windows à partir de votre organisation, vous souhaitez tooinclude dans le rôle de hello.</span><span class="sxs-lookup"><span data-stu-id="2fb5a-134">In hello **Select Users or Groups** dialog box, enter hello Windows users or groups from your organization you want tooinclude in hello role.</span></span>  
  
#### <a name="toocreate-a-sales-analyst-us-user-role"></a><span data-ttu-id="2fb5a-135">toocreate un rôle d’utilisateur Sales Analyst US</span><span class="sxs-lookup"><span data-stu-id="2fb5a-135">toocreate a Sales Analyst US user role</span></span>  
  
1.  <span data-ttu-id="2fb5a-136">Dans le Gestionnaire de rôles, cliquez sur **Nouveau**.</span><span class="sxs-lookup"><span data-stu-id="2fb5a-136">In Role Manager, click **New**.</span></span>    
  
2.  <span data-ttu-id="2fb5a-137">Renommer le rôle de hello trop**Sales Analyst US**.</span><span class="sxs-lookup"><span data-stu-id="2fb5a-137">Rename hello role too**Sales Analyst US**.</span></span>  
  
3.  <span data-ttu-id="2fb5a-138">Attribuez à ce rôle l’autorisation **Lecture**.</span><span class="sxs-lookup"><span data-stu-id="2fb5a-138">Give this role **Read** permission.</span></span>  
  
4.  <span data-ttu-id="2fb5a-139">Cliquez sur hello onglet Filtres de lignes, puis pour hello **DimGeography** table uniquement, dans la colonne de filtre DAX hello, hello type formule suivante :</span><span class="sxs-lookup"><span data-stu-id="2fb5a-139">Click hello Row Filters tab, and then for hello **DimGeography** table only, in hello DAX Filter column, type hello following formula:</span></span>  
  
    ```Administrator
    =DimGeography[CountryRegionCode] = "US" 
    ```
    
    <span data-ttu-id="2fb5a-140">Formule de filtre de lignes d’une valeur booléenne (TRUE/FALSE) de tooa doit être résolue.</span><span class="sxs-lookup"><span data-stu-id="2fb5a-140">A Row Filter formula must resolve tooa Boolean (TRUE/FALSE) value.</span></span> <span data-ttu-id="2fb5a-141">Avec cette formule, vous spécifiez que seules les lignes avec hello valeur Country Region Code « US » sont visibles toohello utilisateur.</span><span class="sxs-lookup"><span data-stu-id="2fb5a-141">With this formula, you are specifying that only rows with hello Country Region Code value of “US” are visible toohello user.</span></span>  
    ![aas-lesson11-role-filter](../tutorials/media/aas-lesson11-role-filter.png) 
  
6.  <span data-ttu-id="2fb5a-143">Facultatif : Cliquez sur hello **membres** onglet, puis cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="2fb5a-143">Optional: Click hello **Members** tab, and then click **Add**.</span></span> <span data-ttu-id="2fb5a-144">Bonjour **sélectionner des utilisateurs ou groupes** boîte de dialogue, entrez hello utilisateurs ou groupes Windows à partir de votre organisation, vous souhaitez tooinclude dans le rôle de hello.</span><span class="sxs-lookup"><span data-stu-id="2fb5a-144">In hello **Select Users or Groups** dialog box, enter hello Windows users or groups from your organization you want tooinclude in hello role.</span></span>  
  
#### <a name="toocreate-an-administrator-user-role"></a><span data-ttu-id="2fb5a-145">toocreate un rôle d’utilisateur administrateur</span><span class="sxs-lookup"><span data-stu-id="2fb5a-145">toocreate an Administrator user role</span></span>  
  
1.  <span data-ttu-id="2fb5a-146">Cliquez sur **Nouveau**.</span><span class="sxs-lookup"><span data-stu-id="2fb5a-146">Click **New**.</span></span>  
  
2.  <span data-ttu-id="2fb5a-147">Renommer le rôle de hello trop**administrateur**.</span><span class="sxs-lookup"><span data-stu-id="2fb5a-147">Rename hello role too**Administrator**.</span></span>  
  
3.  <span data-ttu-id="2fb5a-148">Attribuez à ce rôle l’autorisation **Administrateur**.</span><span class="sxs-lookup"><span data-stu-id="2fb5a-148">Give this role **Administrator** permission.</span></span>  
  
4.  <span data-ttu-id="2fb5a-149">Facultatif : Cliquez sur hello **membres** onglet, puis cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="2fb5a-149">Optional: Click hello **Members** tab, and then click **Add**.</span></span> <span data-ttu-id="2fb5a-150">Bonjour **sélectionner des utilisateurs ou groupes** boîte de dialogue, entrez hello utilisateurs ou groupes Windows à partir de votre organisation, vous souhaitez tooinclude dans le rôle de hello.</span><span class="sxs-lookup"><span data-stu-id="2fb5a-150">In hello **Select Users or Groups** dialog box, enter hello Windows users or groups from your organization you want tooinclude in hello role.</span></span> 
  
  
## <a name="whats-next"></a><span data-ttu-id="2fb5a-151">Et ensuite ?</span><span class="sxs-lookup"><span data-stu-id="2fb5a-151">What's next?</span></span>
<span data-ttu-id="2fb5a-152">[Leçon 12 : Analyser dans Excel](../tutorials/aas-lesson-12-analyze-in-excel.md).</span><span class="sxs-lookup"><span data-stu-id="2fb5a-152">[Lesson 12: Analyze in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md).</span></span>

  
  
