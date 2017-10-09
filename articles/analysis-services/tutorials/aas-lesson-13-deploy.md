---
<span data-ttu-id="de9d1-101">titre : aaa « leçon du didacticiel Azure Analysis Services 13 : déployer | Description de Microsoft Docs » : décrit comment le didacticiel de hello toodeploy project tooAzure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="de9d1-101">title: aaa"Azure Analysis Services tutorial lesson 13: Deploy | Microsoft Docs" description:  Describes how toodeploy hello tutorial project tooAzure Analysis Services.</span></span>
<span data-ttu-id="de9d1-102">Services : analysis services documentationcenter : '' auteur : minewiskan manager : erikre éditeur : '' balises : ».</span><span class="sxs-lookup"><span data-stu-id="de9d1-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="de9d1-103">MS.AssetId : ms.service : ms.devlang d’analysis services : NA ms.topic : get-started-article ms.tgt_pltfrm : NA ms.workload : na ms.date : 17/07/2017 ms.author : owend</span><span class="sxs-lookup"><span data-stu-id="de9d1-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 07/17/2017 ms.author: owend</span></span>
---
# <a name="lesson-13-deploy"></a><span data-ttu-id="de9d1-104">Leçon 13 : Déployer</span><span class="sxs-lookup"><span data-stu-id="de9d1-104">Lesson 13: Deploy</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="de9d1-105">Dans cette leçon, vous configurez les propriétés de déploiement ; spécification d’un ordinateur Azure Analysis Services server toodeploy tooand un nom pour le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="de9d1-105">In this lesson, you configure deployment properties; specifying an Azure Analysis Services server toodeploy tooand a name for hello model.</span></span> <span data-ttu-id="de9d1-106">Vous déployez ensuite hello modèle toothat instance.</span><span class="sxs-lookup"><span data-stu-id="de9d1-106">You then deploy hello model toothat instance.</span></span> <span data-ttu-id="de9d1-107">Une fois votre modèle est déployé, les utilisateurs peuvent se connecter à tooit à l’aide d’une application cliente de création de rapports.</span><span class="sxs-lookup"><span data-stu-id="de9d1-107">After your model is deployed, users can connect tooit by using a reporting client application.</span></span> <span data-ttu-id="de9d1-108">toolearn, voir [déployer tooAzure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-deploy).</span><span class="sxs-lookup"><span data-stu-id="de9d1-108">toolearn more, see [Deploy tooAzure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-deploy).</span></span>  
  
<span data-ttu-id="de9d1-109">Estimé temps toocomplete cette leçon : **5 minutes**</span><span class="sxs-lookup"><span data-stu-id="de9d1-109">Estimated time toocomplete this lesson: **5 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="de9d1-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="de9d1-110">Prerequisites</span></span>  
<span data-ttu-id="de9d1-111">Cette rubrique fait partie d’un didacticiel de modélisation tabulaire, qui doit être suivi dans l’ordre prévu.</span><span class="sxs-lookup"><span data-stu-id="de9d1-111">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="de9d1-112">Avant d’effectuer les tâches de hello dans cette leçon, vous devez avoir terminé les leçon précédente hello : [leçon 12 : analyser dans Excel](../tutorials/aas-lesson-12-analyze-in-excel.md).</span><span class="sxs-lookup"><span data-stu-id="de9d1-112">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 12: Analyze in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md).</span></span>  

> [!IMPORTANT]  
> <span data-ttu-id="de9d1-113">Vous devez avoir [des autorisations d’administrateur](../analysis-services-server-admins.md) on hello distant Analysis Services server dans l’ordre toodeploy tooit.</span><span class="sxs-lookup"><span data-stu-id="de9d1-113">You must have [Administrator permissions](../analysis-services-server-admins.md) on hello remote Analysis Services server in-order toodeploy tooit.</span></span>  

> [!IMPORTANT]  
> <span data-ttu-id="de9d1-114">Si vous avez installé la base de données exemple hello AdventureWorksDW2014 sur un ordinateur local SQL Server, et que vous déployez votre serveur Azure Analysis Services de tooan de modèle, un [passerelle de données locale](../analysis-services-gateway.md) est requis.</span><span class="sxs-lookup"><span data-stu-id="de9d1-114">If you installed hello AdventureWorksDW2014 sample database on an on-premises SQL Server, and you're deploying your model tooan Azure Analysis Services server, an [On-premises data gateway](../analysis-services-gateway.md) is required.</span></span>
  
## <a name="deploy-hello-model"></a><span data-ttu-id="de9d1-115">Déployer le modèle de hello</span><span class="sxs-lookup"><span data-stu-id="de9d1-115">Deploy hello model</span></span>  
  
#### <a name="tooconfigure-deployment-properties"></a><span data-ttu-id="de9d1-116">propriétés de déploiement tooconfigure</span><span class="sxs-lookup"><span data-stu-id="de9d1-116">tooconfigure deployment properties</span></span>  

  
1.  <span data-ttu-id="de9d1-117">Dans **l’Explorateur de solutions**, avec le bouton hello **AW Internet Sales** de projet, puis cliquez sur **propriétés**.</span><span class="sxs-lookup"><span data-stu-id="de9d1-117">In **Solution Explorer**, right-click hello **AW Internet Sales** project, and then click **Properties**.</span></span>  
  
2.  <span data-ttu-id="de9d1-118">Bonjour **Pages de propriétés de AW Internet Sales** boîte de dialogue **serveur de déploiement**, Bonjour **Server** propriété, entrez le serveur complet de hello.</span><span class="sxs-lookup"><span data-stu-id="de9d1-118">In hello **AW Internet Sales Property Pages** dialog box, under **Deployment Server**, in hello **Server** property, enter hello full server.</span></span>  

    ![aas-lesson13-deploy-property](../tutorials/media/aas-lesson13-deploy-property.png)
  
3.  <span data-ttu-id="de9d1-120">Bonjour **base de données** , tapez **Internet Sales Adventure Works**.</span><span class="sxs-lookup"><span data-stu-id="de9d1-120">In hello **Database** property, type **Adventure Works Internet Sales**.</span></span>  
  
4.  <span data-ttu-id="de9d1-121">Bonjour **Nom_modèle** , tapez **Adventure Works Internet Sales Model**.</span><span class="sxs-lookup"><span data-stu-id="de9d1-121">In hello **Model Name** property, type **Adventure Works Internet Sales Model**.</span></span>  
  
5.  <span data-ttu-id="de9d1-122">Passez en revue vos sélections, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="de9d1-122">Verify your selections and then click **OK**.</span></span>  
  
#### <a name="toodeploy-hello-adventure-works-internet-sales"></a><span data-ttu-id="de9d1-123">toodeploy hello Adventure Works Internet Sales</span><span class="sxs-lookup"><span data-stu-id="de9d1-123">toodeploy hello Adventure Works Internet Sales</span></span>
  
1.  <span data-ttu-id="de9d1-124">Dans **l’Explorateur de solutions**, avec le bouton hello **AW Internet Sales** projet > **Build**.</span><span class="sxs-lookup"><span data-stu-id="de9d1-124">In **Solution Explorer**, right-click hello **AW Internet Sales** project > **Build**.</span></span>  

2.  <span data-ttu-id="de9d1-125">Avec le bouton hello **AW Internet Sales** projet > **déployer**.</span><span class="sxs-lookup"><span data-stu-id="de9d1-125">Right-click hello **AW Internet Sales** project > **Deploy**.</span></span>

    <span data-ttu-id="de9d1-126">Lorsque vous déployez tooAzure Analysis Services, vous pouvez être invité à tooenter votre compte.</span><span class="sxs-lookup"><span data-stu-id="de9d1-126">When deploying tooAzure Analysis Services, you may be prompted tooenter your account.</span></span> <span data-ttu-id="de9d1-127">Entrez votre compte professionnel et votre mot de passe, par exemple nancy@adventureworks.com. Ce compte doit être dans les administrateurs sur le serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="de9d1-127">Enter your organizational account and password, for example nancy@adventureworks.com. This account must be in Admins on hello server.</span></span>
  
    <span data-ttu-id="de9d1-128">boîte de dialogue déployer Hello apparaît et affiche l’état du déploiement des métadonnées de hello hello et chaque table incluse dans le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="de9d1-128">hello Deploy dialog box appears and displays hello deployment status of hello metadata and each table included in hello model.</span></span>  
    
    ![aas-lesson13-deploy-status](../tutorials/media/aas-lesson13-deploy-status.png)
  
3. <span data-ttu-id="de9d1-130">Si le déploiement se termine sans erreurs, cliquez sur **Fermer**.</span><span class="sxs-lookup"><span data-stu-id="de9d1-130">When deployment successfully completes, go ahead and click **Close**.</span></span>  
  
## <a name="conclusion"></a><span data-ttu-id="de9d1-131">Conclusion</span><span class="sxs-lookup"><span data-stu-id="de9d1-131">Conclusion</span></span>  
<span data-ttu-id="de9d1-132">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="de9d1-132">Congratulations!</span></span> <span data-ttu-id="de9d1-133">Vous venez de terminer la création et le déploiement de votre premier modèle tabulaire Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="de9d1-133">You're finished authoring and deploying your first Analysis Services Tabular model.</span></span> <span data-ttu-id="de9d1-134">Ce didacticiel a permis de vous guider dans la réalisation des tâches courantes de hello lors de la création d’un modèle tabulaire.</span><span class="sxs-lookup"><span data-stu-id="de9d1-134">This tutorial has helped guide you through completing hello most common tasks in creating a tabular model.</span></span> <span data-ttu-id="de9d1-135">Maintenant que votre modèle Internet Sales Adventure Works est déployé, vous pouvez utiliser le modèle de SQL Server Management Studio toomanage hello ; créer des scripts de processus et d’un plan de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="de9d1-135">Now that your Adventure Works Internet Sales model is deployed, you can use SQL Server Management Studio toomanage hello model; create process scripts and a backup plan.</span></span> <span data-ttu-id="de9d1-136">Les utilisateurs peuvent également connectez-vous de modèle toohello à l’aide d’une application cliente de création de rapports tels que Microsoft Excel ou Power BI.</span><span class="sxs-lookup"><span data-stu-id="de9d1-136">Users can also now connect toohello model using a reporting client application such as Microsoft Excel or Power BI.</span></span>  

![aas-lesson13-ssms](../tutorials/media/aas-lesson13-ssms.png)
  
  
  
## <a name="whats-next"></a><span data-ttu-id="de9d1-138">Et ensuite ?</span><span class="sxs-lookup"><span data-stu-id="de9d1-138">What's next?</span></span>
<span data-ttu-id="de9d1-139">[Connect with Power BI Desktop (Se connecter avec Power BI Desktop)](../analysis-services-connect-pbi.md) </span><span class="sxs-lookup"><span data-stu-id="de9d1-139">[Connect with Power BI Desktop](../analysis-services-connect-pbi.md) </span></span>  
<span data-ttu-id="de9d1-140">[Leçon supplémentaire – Sécurité dynamique](../tutorials/aas-supplemental-lesson-dynamic-security.md) </span><span class="sxs-lookup"><span data-stu-id="de9d1-140">[Supplemental Lesson - Dynamic security](../tutorials/aas-supplemental-lesson-dynamic-security.md) </span></span>  
<span data-ttu-id="de9d1-141">[Leçon supplémentaire – Lignes de détails](../tutorials/aas-supplemental-lesson-detail-rows.md) </span><span class="sxs-lookup"><span data-stu-id="de9d1-141">[Supplemental Lesson - Detail rows](../tutorials/aas-supplemental-lesson-detail-rows.md) </span></span>  
[<span data-ttu-id="de9d1-142">Leçon supplémentaire – Hiérarchies déséquilibrées</span><span class="sxs-lookup"><span data-stu-id="de9d1-142">Supplemental Lesson - Ragged hierarchies</span></span>](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)   
