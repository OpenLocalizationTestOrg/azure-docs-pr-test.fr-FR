---
title: aaaGet en main de Microsoft Power BI Embedded
description: "Power BI incorporée, ajoutez des rapports interactifs Power BI dans votre application business intelligence"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 4787cf44-5d1c-4bc3-b3fd-bf396e5c1176
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: ebb550cb4eba761dde3c23e4dd0314fc885817e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-microsoft-power-bi-embedded"></a><span data-ttu-id="7ead6-103">Prise en main de Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="7ead6-103">Get started with Microsoft Power BI Embedded</span></span>

<span data-ttu-id="7ead6-104">**Power BI Embedded** est un service Azure qui tooadd de développeurs active application interactif Power BI des rapports dans leurs propres applications.</span><span class="sxs-lookup"><span data-stu-id="7ead6-104">**Power BI Embedded** is an Azure service that enables application developers tooadd interactive Power BI reports into their own applications.</span></span> <span data-ttu-id="7ead6-105">**Power BI Embedded** fonctionne avec les applications existantes sans avoir besoin de nouvelle conception ou la modification de hello manière dont les utilisateurs se connecter.</span><span class="sxs-lookup"><span data-stu-id="7ead6-105">**Power BI Embedded** works with existing applications without needing redesign or changing hello way users sign in.</span></span>

<span data-ttu-id="7ead6-106">Ressources pour **Microsoft Power BI Embedded** approvisionnés via hello [Azure ARM API](https://msdn.microsoft.com/library/mt712306.aspx).</span><span class="sxs-lookup"><span data-stu-id="7ead6-106">Resources for **Microsoft Power BI Embedded** are provisioned through hello [Azure ARM APIs](https://msdn.microsoft.com/library/mt712306.aspx).</span></span> <span data-ttu-id="7ead6-107">Dans ce cas, la ressource hello vous approvisionner est un **collecte d’espace de travail Power BI**.</span><span class="sxs-lookup"><span data-stu-id="7ead6-107">In this case, hello resource you provision is a **Power BI Workspace Collection**.</span></span>

![](media/power-bi-embedded-get-started/introduction.png)

## <a name="create-a-workspace-collection"></a><span data-ttu-id="7ead6-108">Création d’une collection d’espaces de travail</span><span class="sxs-lookup"><span data-stu-id="7ead6-108">Create a workspace collection</span></span>

<span data-ttu-id="7ead6-109">A **Collection de l’espace de travail** est une ressource de Azure de niveau supérieur hello et un conteneur pour le contenu de hello qui est incorporé dans votre application.</span><span class="sxs-lookup"><span data-stu-id="7ead6-109">A **Workspace Collection** is hello top-level Azure resource and a container for hello content that will be embedded in your application.</span></span> <span data-ttu-id="7ead6-110">Pour créer une **collection d’espaces de travail** , deux possibilités s’offrent à vous :</span><span class="sxs-lookup"><span data-stu-id="7ead6-110">A **Workspace Collection** can be created in two ways::</span></span>

* <span data-ttu-id="7ead6-111">Manuellement à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="7ead6-111">Manually using hello Azure Portal</span></span>
* <span data-ttu-id="7ead6-112">Par programmation à l’aide de hello API Manager(ARM) de ressources Azure</span><span class="sxs-lookup"><span data-stu-id="7ead6-112">Programmatically using hello Azure Resource Manager(ARM) APIs</span></span>

<span data-ttu-id="7ead6-113">Examinons hello étapes toobuild un **Collection de l’espace de travail** à l’aide de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="7ead6-113">Let's walk through hello steps toobuild a **Workspace Collection** using hello Azure Portal.</span></span>

1. <span data-ttu-id="7ead6-114">Ouvrez le **portail Azure**à l’adresse [http://portal.azure.com](http://portal.azure.com)et connectez-vous-y.</span><span class="sxs-lookup"><span data-stu-id="7ead6-114">Open and sign into **Azure Portal**: [http://portal.azure.com](http://portal.azure.com).</span></span>
2. <span data-ttu-id="7ead6-115">Cliquez sur **+ nouveau** sur le panneau supérieur de hello.</span><span class="sxs-lookup"><span data-stu-id="7ead6-115">Click **+ New** on hello top panel.</span></span>
   
   ![](media/power-bi-embedded-get-started/create-workspace-1.png)
3. <span data-ttu-id="7ead6-116">Sous **Données + analyse**, cliquez sur **Power BI Embedded**.</span><span class="sxs-lookup"><span data-stu-id="7ead6-116">Under **Data + Analytics** click **Power BI Embedded**.</span></span>
4. <span data-ttu-id="7ead6-117">Sur hello **espace de travail de Collection panneau**, entrez les informations de hello requis.</span><span class="sxs-lookup"><span data-stu-id="7ead6-117">On hello **Workspace Collection Blade**, enter hello required information.</span></span> <span data-ttu-id="7ead6-118">Pour connaître la **tarification**, consultez la page [Tarification de Power BI Embedded](http://go.microsoft.com/fwlink/?LinkID=760527).</span><span class="sxs-lookup"><span data-stu-id="7ead6-118">For **Pricing**, see [Power BI Embedded pricing](http://go.microsoft.com/fwlink/?LinkID=760527).</span></span>
   
   ![](media/power-bi-embedded-get-started/create-workspace-2.png)
5. <span data-ttu-id="7ead6-119">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="7ead6-119">Click **Create**.</span></span>

<span data-ttu-id="7ead6-120">Hello **Collection de l’espace de travail** prendra quelques instants tooprovision.</span><span class="sxs-lookup"><span data-stu-id="7ead6-120">hello **Workspace Collection** will take a few moments tooprovision.</span></span> <span data-ttu-id="7ead6-121">Issue, vous serez dirigé toohello **Panneau de collecte d’espace de travail**.</span><span class="sxs-lookup"><span data-stu-id="7ead6-121">When completed, you'll be taken toohello **Workspace Collection Blade**.</span></span>

   ![](media/power-bi-embedded-get-started/create-workspace-3.png)

<span data-ttu-id="7ead6-122">Hello **création panneau** contient les informations de hello nécessaires toocall hello API qui créent des espaces de travail et de déployer du contenu toothem.</span><span class="sxs-lookup"><span data-stu-id="7ead6-122">hello **Creation Blade** contains hello information you need toocall hello APIs that create workspaces and deploy content toothem.</span></span>

<a name="view-access-keys"/>

## <a name="view-power-bi-api-access-keys"></a><span data-ttu-id="7ead6-123">Affichage des touches d’accès rapide aux API de Power BI</span><span class="sxs-lookup"><span data-stu-id="7ead6-123">View Power BI API access keys</span></span>

<span data-ttu-id="7ead6-124">Un des principaux éléments d’informations nécessaires toocall hello API REST de Power BI de hello sont hello **clés d’accès**.</span><span class="sxs-lookup"><span data-stu-id="7ead6-124">One of hello most important pieces of information needed toocall hello Power BI REST APIs are hello **Access Keys**.</span></span> <span data-ttu-id="7ead6-125">Ceux-ci sont utilisés toogenerate hello **jetons d’application** qui sont utilisé tooauthenticate vos demandes API.</span><span class="sxs-lookup"><span data-stu-id="7ead6-125">These are used toogenerate hello **app tokens** that are used tooauthenticate your API requests.</span></span> <span data-ttu-id="7ead6-126">tooview votre **clés d’accès**, cliquez sur **clés d’accès** sur hello **panneau paramètres**.</span><span class="sxs-lookup"><span data-stu-id="7ead6-126">tooview your **Access Keys**, click **Access Keys** on hello **Settings Blade**.</span></span> <span data-ttu-id="7ead6-127">Pour en savoir plus sur les **jetons d’application**, voir [Authentification et autorisation avec Power BI Embedded](power-bi-embedded-app-token-flow.md).</span><span class="sxs-lookup"><span data-stu-id="7ead6-127">For more about **app tokens**, see [Authenticating and authorizing with Power BI Embedded](power-bi-embedded-app-token-flow.md).</span></span>

   ![](media/power-bi-embedded-get-started/access-keys.png)

<span data-ttu-id="7ead6-128">Vous allez constater que vous disposez de deux touches.</span><span class="sxs-lookup"><span data-stu-id="7ead6-128">You'll'notice that you have two keys.</span></span>

   ![](media/power-bi-embedded-get-started/access-keys-2.png)

<span data-ttu-id="7ead6-129">Copiez-les et stockez-les de manière sécurisée dans votre application.</span><span class="sxs-lookup"><span data-stu-id="7ead6-129">Copy these keys and store them securely in your application.</span></span> <span data-ttu-id="7ead6-130">Il est très important de traiter ces clés comme vous le feriez pour un mot de passe, car ils vous fournirons accès tooall hello contenu dans votre **Collection de l’espace de travail**.</span><span class="sxs-lookup"><span data-stu-id="7ead6-130">It's very important that you treat these keys as you would a password, because they'll provide access tooall hello content in your **Workspace Collection**.</span></span>

<span data-ttu-id="7ead6-131">Même si deux touches sont répertoriées, une seule est nécessaire à un moment donné.</span><span class="sxs-lookup"><span data-stu-id="7ead6-131">While two keys are listed, only one key is needed at a particular time.</span></span> <span data-ttu-id="7ead6-132">deuxième clé de Hello est fournie afin de régénérer régulièrement les clés sans interrompre le service d’accès toohello.</span><span class="sxs-lookup"><span data-stu-id="7ead6-132">hello second key is provided so you can periodically regenerate keys without interrupting access toohello service.</span></span>

<span data-ttu-id="7ead6-133">Maintenant que vous disposez d’une instance de Power BI pour votre application, ainsi que des **touches d’accès rapide**, vous pouvez importer un rapport dans votre propre application.</span><span class="sxs-lookup"><span data-stu-id="7ead6-133">Now that you have an instance of Power BI for your application, and **Access Keys**, you can import a report into your own app.</span></span> <span data-ttu-id="7ead6-134">Avant, vous allez apprendre comment tooimport un rapport, la section suivante de hello décrit la création tooembed de jeux de données et rapports Power BI dans une application.</span><span class="sxs-lookup"><span data-stu-id="7ead6-134">Before you learn how tooimport a report, hello next section describes creating Power BI datasets and reports tooembed into an app.</span></span>

## <a name="working-with-workspaces"></a><span data-ttu-id="7ead6-135">Utilisation des espaces de travail</span><span class="sxs-lookup"><span data-stu-id="7ead6-135">Working with workspaces</span></span>

<span data-ttu-id="7ead6-136">Après avoir créé votre collection de l’espace de travail, vous devez toocreate un espace de travail qui héberger vos rapports et les jeux de données.</span><span class="sxs-lookup"><span data-stu-id="7ead6-136">After you have created your workspace collection, you will need toocreate a workspace that will house your reports and datasets.</span></span> <span data-ttu-id="7ead6-137">toocreate un espace de travail, vous devez toouse hello [Post espace de travail REST API](https://msdn.microsoft.com/library/azure/mt711503.aspx).</span><span class="sxs-lookup"><span data-stu-id="7ead6-137">toocreate a workspace, you will need toouse hello [Post Worksapce REST API](https://msdn.microsoft.com/library/azure/mt711503.aspx).</span></span>

## <a name="create-power-bi-datasets-and-reports-tooembed-into-an-app-using-power-bi-desktop"></a><span data-ttu-id="7ead6-138">Créer des tooembed de jeux de données et rapports Power BI dans une application à l’aide de Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="7ead6-138">Create Power BI datasets and reports tooembed into an app using Power BI Desktop</span></span>

<span data-ttu-id="7ead6-139">Maintenant que vous avez créé une instance de Power BI pour votre application et avoir **clés d’accès**, vous devez toocreate hello Power BI datasets et les rapports que vous souhaitez tooembed.</span><span class="sxs-lookup"><span data-stu-id="7ead6-139">Now that you have created an instance of Power BI for your application, and have **Access Keys**, you will need toocreate hello Power BI datasets and reports that you want tooembed.</span></span> <span data-ttu-id="7ead6-140">Vous pouvez créer des rapports et des jeux de données à l’aide de **Power BI Desktop**.</span><span class="sxs-lookup"><span data-stu-id="7ead6-140">Datasets and reports can be created by using **Power BI Desktop**.</span></span> <span data-ttu-id="7ead6-141">Vous pouvez télécharger [Power BI Desktop gratuitement](https://go.microsoft.com/fwlink/?LinkId=521662).</span><span class="sxs-lookup"><span data-stu-id="7ead6-141">You can download [Power BI Desktop for free](https://go.microsoft.com/fwlink/?LinkId=521662).</span></span> <span data-ttu-id="7ead6-142">Ou, tooquickly prise en main, vous pouvez télécharger hello [PBIX d’exemple Retail Analysis](http://go.microsoft.com/fwlink/?LinkID=780547).</span><span class="sxs-lookup"><span data-stu-id="7ead6-142">Or, tooquickly get started, you can download hello [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547).</span></span>

> [!NOTE]
> <span data-ttu-id="7ead6-143">plus sur la façon de toolearn toouse **Power BI Desktop**, consultez [prise en main de Power BI Desktop](https://powerbi.microsoft.com/guided-learning/powerbi-learning-0-2-get-started-power-bi-desktop).</span><span class="sxs-lookup"><span data-stu-id="7ead6-143">toolearn more about how toouse **Power BI Desktop**, see [Getting Started with Power BI Desktop](https://powerbi.microsoft.com/guided-learning/powerbi-learning-0-2-get-started-power-bi-desktop).</span></span>

<span data-ttu-id="7ead6-144">Avec **Power BI Desktop**, vous vous connectez la source de données tooyour en important une copie de données hello dans **Power BI Desktop** ou se connectant directement toohello données source à l’aide **DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="7ead6-144">With **Power BI Desktop**, you connect tooyour data source by importing a copy of hello data into **Power BI Desktop** or connecting directly toohello data source using **DirectQuery**.</span></span>

<span data-ttu-id="7ead6-145">Voici hello les différences entre l’utilisation de **importation** et **DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="7ead6-145">Here are hello differences between using **Import** and **DirectQuery**.</span></span>

| <span data-ttu-id="7ead6-146">Importer</span><span class="sxs-lookup"><span data-stu-id="7ead6-146">Import</span></span> | <span data-ttu-id="7ead6-147">DirectQuery</span><span class="sxs-lookup"><span data-stu-id="7ead6-147">DirectQuery</span></span> |
| --- | --- |
| <span data-ttu-id="7ead6-148">Les tables, colonnes *et données* sont importées ou copiées dans **Power BI Desktop**.</span><span class="sxs-lookup"><span data-stu-id="7ead6-148">Tables, columns, *and data* are imported or copied into **Power BI Desktop**.</span></span> <span data-ttu-id="7ead6-149">Lorsque vous travaillez avec des visualisations, **Power BI Desktop** interroge une copie des données de hello.</span><span class="sxs-lookup"><span data-stu-id="7ead6-149">As you work with visualizations, **Power BI Desktop** queries a copy of hello data.</span></span> <span data-ttu-id="7ead6-150">toosee des modifications des données sous-jacentes toohello s’est produite, vous devez actualiser ou importez, à nouveau un dataset complet, en cours.</span><span class="sxs-lookup"><span data-stu-id="7ead6-150">toosee any changes that occurred toohello underlying data, you must refresh, or import, a complete, current dataset again.</span></span> |<span data-ttu-id="7ead6-151">Seules les *tables et colonnes* sont importées ou copiées dans **Power BI Desktop**.</span><span class="sxs-lookup"><span data-stu-id="7ead6-151">Only *tables and columns* are imported or copied into **Power BI Desktop**.</span></span> <span data-ttu-id="7ead6-152">Lorsque vous travaillez avec des visualisations, **Power BI Desktop** requêtes hello source de données sous-jacente, ce qui signifie que vous visualisez toujours des données en cours.</span><span class="sxs-lookup"><span data-stu-id="7ead6-152">As you work with visualizations, **Power BI Desktop** queries hello underlying data source, which means you're always viewing current data.</span></span> |

<span data-ttu-id="7ead6-153">Pour plus d’informations sur la source de données tooa connexion, consultez [source de données de se connecter tooa](power-bi-embedded-connect-datasource.md).</span><span class="sxs-lookup"><span data-stu-id="7ead6-153">For more about connecting tooa data source, see [Connect tooa data source](power-bi-embedded-connect-datasource.md).</span></span>

<span data-ttu-id="7ead6-154">Lorsque vous enregistrez votre travail dans **Power BI Desktop**, un fichier PBIX est créé.</span><span class="sxs-lookup"><span data-stu-id="7ead6-154">After you save your work in **Power BI Desktop**, a PBIX file is created.</span></span> <span data-ttu-id="7ead6-155">Ce fichier contient votre rapport.</span><span class="sxs-lookup"><span data-stu-id="7ead6-155">This file contains your report.</span></span> <span data-ttu-id="7ead6-156">En outre, si vous importez hello données PBIX contient hello dans le jeu de données complet, ou si vous utilisez **DirectQuery**, hello PBIX contient uniquement le schéma d’un dataset.</span><span class="sxs-lookup"><span data-stu-id="7ead6-156">In addition, if you import data hello PBIX contains hello complete dataset, or if you use **DirectQuery**, hello PBIX contains just a dataset schema.</span></span> <span data-ttu-id="7ead6-157">Vous déployez par programme hello PBIX dans votre espace de travail à l’aide de hello [API de Power BI importation](https://msdn.microsoft.com/library/mt711504.aspx).</span><span class="sxs-lookup"><span data-stu-id="7ead6-157">You programmatically deploy hello PBIX into your workspace using hello [Power BI Import API](https://msdn.microsoft.com/library/mt711504.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="7ead6-158">**Power BI Embedded** dispose d’autres API toochange hello serveur et base de données que votre jeu de données pointe tooand ensemble une information d’identification du compte de service qui hello dataset utilisera tooconnect tooyour base de données.</span><span class="sxs-lookup"><span data-stu-id="7ead6-158">**Power BI Embedded** has additional APIs toochange hello server and database that your dataset is pointing tooand set a service account credential that hello dataset will use tooconnect tooyour database.</span></span> <span data-ttu-id="7ead6-159">Consultez les pages [Post SetAllConnections](https://msdn.microsoft.com/library/mt711505.aspx) et [Patch Gateway Datasource](https://msdn.microsoft.com/library/mt711498.aspx).</span><span class="sxs-lookup"><span data-stu-id="7ead6-159">See [Post SetAllConnections](https://msdn.microsoft.com/library/mt711505.aspx) and [Patch Gateway Datasource](https://msdn.microsoft.com/library/mt711498.aspx).</span></span>

## <a name="create-power-bi-datasets-and-reports-using-apis"></a><span data-ttu-id="7ead6-160">Création de rapports et de jeux de données Power BI avec des API</span><span class="sxs-lookup"><span data-stu-id="7ead6-160">Create Power BI datasets and reports using APIs</span></span>

### <a name="datsets"></a><span data-ttu-id="7ead6-161">Jeux de données</span><span class="sxs-lookup"><span data-stu-id="7ead6-161">Datsets</span></span>

<span data-ttu-id="7ead6-162">Vous pouvez créer des jeux de données dans Power BI Embedded à l’aide des API REST de hello.</span><span class="sxs-lookup"><span data-stu-id="7ead6-162">You can create datasets within Power BI Embedded using hello REST API.</span></span> <span data-ttu-id="7ead6-163">Vous pouvez ensuite transmettre les données dans votre jeu de données.</span><span class="sxs-lookup"><span data-stu-id="7ead6-163">You can then push data into your dataset.</span></span> <span data-ttu-id="7ead6-164">Cela vous permet de toowork avec des données sans avoir besoin de hello de Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="7ead6-164">This allows you toowork with data without hello need of Power BI Desktop.</span></span> <span data-ttu-id="7ead6-165">Pour plus d’informations, consultez [Post Datasets](https://msdn.microsoft.com/library/azure/mt778875.aspx) (Opération Post Datasets).</span><span class="sxs-lookup"><span data-stu-id="7ead6-165">For more information, see [Post Datasets](https://msdn.microsoft.com/library/azure/mt778875.aspx).</span></span>

### <a name="reports"></a><span data-ttu-id="7ead6-166">Rapports</span><span class="sxs-lookup"><span data-stu-id="7ead6-166">Reports</span></span>

<span data-ttu-id="7ead6-167">Vous pouvez créer un rapport à partir d’un jeu de données directement dans votre application à l’aide de hello API JavaScript.</span><span class="sxs-lookup"><span data-stu-id="7ead6-167">You can create a report from a dataset directly in your application using hello JavaScript API.</span></span> <span data-ttu-id="7ead6-168">Pour plus d’informations, consultez [Create a new report from a dataset in Power BI Embedded](power-bi-embedded-create-report-from-dataset.md) (Créer un rapport à partir d’un jeu de données dans Power BI Embedded).</span><span class="sxs-lookup"><span data-stu-id="7ead6-168">For more information, see [Create a new report from a dataset in Power BI Embedded](power-bi-embedded-create-report-from-dataset.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="7ead6-169">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="7ead6-169">See Also</span></span>

[<span data-ttu-id="7ead6-170">Prise en main de l’exemple</span><span class="sxs-lookup"><span data-stu-id="7ead6-170">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="7ead6-171">Authentification et autorisation dans Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="7ead6-171">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
<span data-ttu-id="7ead6-172">[Embed a report](power-bi-embedded-embed-report.md) (Intégrer un rapport)</span><span class="sxs-lookup"><span data-stu-id="7ead6-172">[Embed a report](power-bi-embedded-embed-report.md)</span></span>  
<span data-ttu-id="7ead6-173">[Create a new report from a dataset in Power BI Embedded](power-bi-embedded-create-report-from-dataset.md) (Créer un rapport à partir d’un jeu de données dans Power BI Embedded)
[Save reports in Power BI Embedded](power-bi-embedded-save-reports.md) (Enregistrer des rapports dans Power BI Embedded)</span><span class="sxs-lookup"><span data-stu-id="7ead6-173">[Create a new report from a dataset in Power BI Embedded](power-bi-embedded-create-report-from-dataset.md)
[Save reports](power-bi-embedded-save-reports.md)</span></span>  
[<span data-ttu-id="7ead6-174">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="7ead6-174">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="7ead6-175">Exemple d’incorporation JavaScript</span><span class="sxs-lookup"><span data-stu-id="7ead6-175">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
<span data-ttu-id="7ead6-176">Des questions ?</span><span class="sxs-lookup"><span data-stu-id="7ead6-176">More questions?</span></span> [<span data-ttu-id="7ead6-177">Essayez de hello Communauté Power BI</span><span class="sxs-lookup"><span data-stu-id="7ead6-177">Try hello Power BI Community</span></span>](http://community.powerbi.com/)

