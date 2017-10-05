---
title: "Créer votre première application web Java dans Azure"
description: "Découvrez comment exécuter des applications web dans App Service en déployant une application Java de base."
services: app-service\web
documentationcenter: 
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 8bacfe3e-7f0b-4394-959a-a88618cb31e1
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: quickstart
ms.date: 6/7/2017
ms.author: cephalin;robmcm
ms.custom: mvc
ms.openlocfilehash: b91b9bde5eb8ea0d7e2196056b635fe54095e748
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="create-your-first-java-web-app-in-azure"></a><span data-ttu-id="196ff-103">Créer votre première application web Java dans Azure</span><span class="sxs-lookup"><span data-stu-id="196ff-103">Create your first Java web app in Azure</span></span>

<span data-ttu-id="196ff-104">La fonctionnalité [Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) [d’Azure App Service](../app-service/app-service-value-prop-what-is.md) offre un service d’hébergement web hautement évolutif appliquant des mises à jour correctives automatiques.</span><span class="sxs-lookup"><span data-stu-id="196ff-104">The [Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) feature of [Azure App Service](../app-service/app-service-value-prop-what-is.md) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="196ff-105">Ce guide de démarrage rapide indique comment déployer une application web Java dans App Service à l’aide de [l’environnement de développement intégré (IDE) Eclipse pour développeurs Java EE](http://www.eclipse.org/).</span><span class="sxs-lookup"><span data-stu-id="196ff-105">This quickstart shows how to deploy a Java web app to App Service by using the [Eclipse IDE for Java EE Developers](http://www.eclipse.org/).</span></span>

![« Hello Azure ! »](./media/app-service-web-get-started-java/browse-web-app-1.png)

## <a name="prerequisites"></a><span data-ttu-id="196ff-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="196ff-108">Prerequisites</span></span>

<span data-ttu-id="196ff-109">Pour effectuer ce démarrage rapide, installez les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="196ff-109">To complete this quickstart, install:</span></span>

* <span data-ttu-id="196ff-110">[L’Environnement de développement intégré Eclipse pour développeurs Java EE](http://www.eclipse.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="196ff-110">The free [Eclipse IDE for Java EE Developers](http://www.eclipse.org/downloads/).</span></span> <span data-ttu-id="196ff-111">Ce démarrage rapide utilise Eclipse Neon.</span><span class="sxs-lookup"><span data-stu-id="196ff-111">This quickstart uses Eclipse Neon.</span></span>
* <span data-ttu-id="196ff-112">Le [kit de ressources Azure pour Eclipse](/azure/azure-toolkit-for-eclipse-installation).</span><span class="sxs-lookup"><span data-stu-id="196ff-112">The [Azure Toolkit for Eclipse](/azure/azure-toolkit-for-eclipse-installation).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-dynamic-web-project-in-eclipse"></a><span data-ttu-id="196ff-113">Créer un projet web dynamique dans Eclipse</span><span class="sxs-lookup"><span data-stu-id="196ff-113">Create a dynamic web project in Eclipse</span></span>

<span data-ttu-id="196ff-114">Dans Eclipse, sélectionnez **File (Fichier)** > **New (Nouveau)** > **Dynamic Web Project (Projet web dynamique)**.</span><span class="sxs-lookup"><span data-stu-id="196ff-114">In Eclipse, select **File** > **New** > **Dynamic Web Project**.</span></span>

<span data-ttu-id="196ff-115">Dans la boîte de dialogue **New Dynamic Web Project (Nouveau projet web dynamique)**, nommez le projet **MyFirstJavaOnAzureWebApp**, puis sélectionnez **Finish (Terminer)**.</span><span class="sxs-lookup"><span data-stu-id="196ff-115">In the **New Dynamic Web Project** dialog box, name the project **MyFirstJavaOnAzureWebApp**, and select **Finish**.</span></span>
   
![Boîte de dialogue Projet web dynamique](./media/app-service-web-get-started-java/new-dynamic-web-project-dialog-box.png)

### <a name="add-a-jsp-page"></a><span data-ttu-id="196ff-117">Ajouter une page JSP</span><span class="sxs-lookup"><span data-stu-id="196ff-117">Add a JSP page</span></span>

<span data-ttu-id="196ff-118">Si l’Explorateur de projets n’est pas affiché, restaurez-le.</span><span class="sxs-lookup"><span data-stu-id="196ff-118">If Project Explorer is not displayed, restore it.</span></span>

![Espace de travail Java EE pour Eclipse](./media/app-service-web-get-started-java/pe.png)

<span data-ttu-id="196ff-120">Dans l’Explorateur de projets, développez le projet **MyFirstJavaOnAzureWebApp**.</span><span class="sxs-lookup"><span data-stu-id="196ff-120">In Project Explorer, expand the **MyFirstJavaOnAzureWebApp** project.</span></span>
<span data-ttu-id="196ff-121">Cliquez avec le bouton droit sur **WebContent**, puis sélectionnez **New (Nouveau)** > **JSP File (Fichier JSP)**.</span><span class="sxs-lookup"><span data-stu-id="196ff-121">Right-click **WebContent**, and then select **New** > **JSP File**.</span></span>

![Menu d’un nouveau fichier JSP dans l’Explorateur de projets](./media/app-service-web-get-started-java/new-jsp-file-menu.png)

<span data-ttu-id="196ff-123">Dans la boîte de dialogue **New JSP File (Nouveau fichier JSP)** :</span><span class="sxs-lookup"><span data-stu-id="196ff-123">In the **New JSP File** dialog box:</span></span>

* <span data-ttu-id="196ff-124">Nommez le fichier **index.jsp**.</span><span class="sxs-lookup"><span data-stu-id="196ff-124">Name the file **index.jsp**.</span></span>
* <span data-ttu-id="196ff-125">Sélectionnez **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="196ff-125">Select **Finish**.</span></span>

  ![Boîte de dialogue New JSP File (Nouveau fichier JSP)](./media/app-service-web-get-started-java/new-jsp-file-dialog-box-page-1.png)

<span data-ttu-id="196ff-127">Dans le fichier index.jsp, remplacez l’élément `<body></body>` par le balisage suivant :</span><span class="sxs-lookup"><span data-stu-id="196ff-127">In the index.jsp file, replace the `<body></body>` element with the following markup:</span></span>

```jsp
<body>
<h1><% out.println("Hello Azure!"); %></h1>
</body>
```

<span data-ttu-id="196ff-128">Enregistrez les modifications.</span><span class="sxs-lookup"><span data-stu-id="196ff-128">Save the changes.</span></span>

## <a name="publish-the-web-app-to-azure"></a><span data-ttu-id="196ff-129">Publier l’application web dans Azure</span><span class="sxs-lookup"><span data-stu-id="196ff-129">Publish the web app to Azure</span></span>

<span data-ttu-id="196ff-130">Dans l’Explorateur de projets, cliquez avec le bouton droit sur le projet, puis sélectionnez **Azure** > **Publish as Azure Web App (Publier en tant qu’application web Azure)**.</span><span class="sxs-lookup"><span data-stu-id="196ff-130">In Project Explorer, right-click the project, and then select **Azure** > **Publish as Azure Web App**.</span></span>

![Menu contextuel Publish as Azure Web App (Publier en tant qu’application web Azure)](./media/app-service-web-get-started-java/publish-as-azure-web-app-context-menu.png)

<span data-ttu-id="196ff-132">Dans la boîte de dialogue **Connexion à Azure**, conservez l’option **Interactive**, puis sélectionnez **Connexion**.</span><span class="sxs-lookup"><span data-stu-id="196ff-132">In the **Azure Sign In** dialog box, keep the **Interactive** option, and then select **Sign in**.</span></span>

<span data-ttu-id="196ff-133">Suivez les instructions de connexion.</span><span class="sxs-lookup"><span data-stu-id="196ff-133">Follow the sign-in instructions.</span></span>

### <a name="deploy-web-app-dialog-box"></a><span data-ttu-id="196ff-134">Boîte de dialogue Déployer une application web</span><span class="sxs-lookup"><span data-stu-id="196ff-134">Deploy Web App dialog box</span></span>

<span data-ttu-id="196ff-135">Une fois que vous vous êtes connecté à votre compte Azure, la boîte de dialogue **Déployer une application web** s’affiche.</span><span class="sxs-lookup"><span data-stu-id="196ff-135">After you have signed in to your Azure account, the **Deploy Web App** dialog box appears.</span></span>

<span data-ttu-id="196ff-136">Sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="196ff-136">Select **Create**.</span></span>

![Boîte de dialogue Déployer une application web](./media/app-service-web-get-started-java/deploy-web-app-dialog-box.png)

### <a name="create-app-service-dialog-box"></a><span data-ttu-id="196ff-138">Boîte de dialogue Créer App Service</span><span class="sxs-lookup"><span data-stu-id="196ff-138">Create App Service dialog box</span></span>

<span data-ttu-id="196ff-139">La boîte de dialogue **Créer App Service** apparaît avec les valeurs par défaut.</span><span class="sxs-lookup"><span data-stu-id="196ff-139">The **Create App Service** dialog box appears with default values.</span></span> <span data-ttu-id="196ff-140">La valeur **170602185241** illustrée dans la figure précédente diffère de celle indiquée dans votre boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="196ff-140">The number **170602185241** shown in the following image is different in your dialog box.</span></span>

![Boîte de dialogue Créer App Service](./media/app-service-web-get-started-java/cas1.png)

<span data-ttu-id="196ff-142">Dans la boîte de dialogue **Créer App Service** :</span><span class="sxs-lookup"><span data-stu-id="196ff-142">In the **Create App Service** dialog box:</span></span>

* <span data-ttu-id="196ff-143">Conservez le nom généré pour l’application web.</span><span class="sxs-lookup"><span data-stu-id="196ff-143">Keep the generated name for the web app.</span></span> <span data-ttu-id="196ff-144">Ce nom doit être unique au sein d’Azure.</span><span class="sxs-lookup"><span data-stu-id="196ff-144">This name must be unique across Azure.</span></span> <span data-ttu-id="196ff-145">Le nom fait partie intégrante de l’adresse URL de l’application web.</span><span class="sxs-lookup"><span data-stu-id="196ff-145">The name is part of the URL address for the web app.</span></span> <span data-ttu-id="196ff-146">Par exemple : si l’application web porte le nom **MyJavaWebApp**, l’URL correspond à *myjavawebapp.azurewebsites.net*.</span><span class="sxs-lookup"><span data-stu-id="196ff-146">For example: if the web app name is **MyJavaWebApp**, the URL is *myjavawebapp.azurewebsites.net*.</span></span>
* <span data-ttu-id="196ff-147">Conservez le conteneur web par défaut.</span><span class="sxs-lookup"><span data-stu-id="196ff-147">Keep the default web container.</span></span>
* <span data-ttu-id="196ff-148">Sélectionnez un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="196ff-148">Select an Azure subscription.</span></span>
* <span data-ttu-id="196ff-149">Dans l’onglet **Plan App Service** :</span><span class="sxs-lookup"><span data-stu-id="196ff-149">On the **App service plan** tab:</span></span>

  * <span data-ttu-id="196ff-150">**Créer un nouveau** : conservez la valeur par défaut, qui correspond au nom du plan App Service.</span><span class="sxs-lookup"><span data-stu-id="196ff-150">**Create new**: Keep the default, which is the name of the App Service plan.</span></span>
  * <span data-ttu-id="196ff-151">**Emplacement** : sélectionnez **Europe de l’Ouest** ou un emplacement près de chez vous.</span><span class="sxs-lookup"><span data-stu-id="196ff-151">**Location**: Select **West Europe** or a location near you.</span></span>
  * <span data-ttu-id="196ff-152">**Niveau tarifaire** : sélectionnez l’option de tarification gratuite.</span><span class="sxs-lookup"><span data-stu-id="196ff-152">**Pricing tier**: Select the free option.</span></span> <span data-ttu-id="196ff-153">Pour plus d’informations sur les fonctionnalités, consultez la page [Tarification de App Service](https://azure.microsoft.com/pricing/details/app-service/).</span><span class="sxs-lookup"><span data-stu-id="196ff-153">For features, see [App Service pricing](https://azure.microsoft.com/pricing/details/app-service/).</span></span>

   ![Boîte de dialogue Créer App Service](./media/app-service-web-get-started-java/create-app-service-dialog-box.png)

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

### <a name="resource-group-tab"></a><span data-ttu-id="196ff-155">Onglet Groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="196ff-155">Resource group tab</span></span>

<span data-ttu-id="196ff-156">Sélectionnez l’onglet **Groupe de ressources**. Conservez la valeur générée par défaut pour le groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="196ff-156">Select the **Resource group** tab. Keep the default generated value for the resource group.</span></span>

![Onglet Groupe de ressources](./media/app-service-web-get-started-java/create-app-service-resource-group.png)

[!INCLUDE [resource-group](../../includes/resource-group.md)]

<span data-ttu-id="196ff-158">Sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="196ff-158">Select **Create**.</span></span>

<!--
### The JDK tab

Select the **JDK** tab. Keep the default, and then select **Create**.

![Create App Service plan](./media/app-service-web-get-started-java/create-app-service-specify-jdk.png)
-->

<span data-ttu-id="196ff-159">Le kit de ressources Azure crée l’application web et affiche une boîte de dialogue indiquant la progression de l’opération.</span><span class="sxs-lookup"><span data-stu-id="196ff-159">The Azure Toolkit creates the web app and displays a progress dialog box.</span></span>

![Boîte de dialogue indiquant la progression de la création du service App Service](./media/app-service-web-get-started-java/create-app-service-progress-bar.png)

### <a name="deploy-web-app-dialog-box"></a><span data-ttu-id="196ff-161">Boîte de dialogue Déployer une application web</span><span class="sxs-lookup"><span data-stu-id="196ff-161">Deploy Web App dialog box</span></span>

<span data-ttu-id="196ff-162">Dans la boîte de dialogue **Déployer une application web**, sélectionnez **Deploy to root (Déployer à la racine)**.</span><span class="sxs-lookup"><span data-stu-id="196ff-162">In the **Deploy Web App** dialog box, select **Deploy to root**.</span></span> <span data-ttu-id="196ff-163">Si vous disposez d’un App Service à l’emplacement *wingtiptoys.azurewebsites.net* et que vous ne choisissez pas le déploiement à la racine, l’application web nommée **MyFirstJavaOnAzureWebApp** est déployée dans *wingtiptoys.azurewebsites.net/MyFirstJavaOnAzureWebApp*.</span><span class="sxs-lookup"><span data-stu-id="196ff-163">If you have an app service at *wingtiptoys.azurewebsites.net* and you do not deploy to the root, the web app named **MyFirstJavaOnAzureWebApp** is deployed to *wingtiptoys.azurewebsites.net/MyFirstJavaOnAzureWebApp*.</span></span>

![Boîte de dialogue Déployer une application web](./media/app-service-web-get-started-java/deploy-web-app-to-root.png)

<span data-ttu-id="196ff-165">La boîte de dialogue affiche les valeurs sélectionnées pour Azure, JDK et le conteneur web.</span><span class="sxs-lookup"><span data-stu-id="196ff-165">The dialog box shows the Azure, JDK, and web container selections.</span></span>

<span data-ttu-id="196ff-166">Sélectionnez **Déployer** pour publier l’application web dans Azure.</span><span class="sxs-lookup"><span data-stu-id="196ff-166">Select **Deploy** to publish the web app to Azure.</span></span>

<span data-ttu-id="196ff-167">Une fois la publication terminée, sélectionnez le lien **Publié** dans la boîte de dialogue **Journal d’activité Azure**.</span><span class="sxs-lookup"><span data-stu-id="196ff-167">When the publishing finishes, select the **Published** link in the **Azure Activity Log** dialog box.</span></span>

![Boîte de dialogue Journal d’activité Azure](./media/app-service-web-get-started-java/aal.png)

<span data-ttu-id="196ff-169">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="196ff-169">Congratulations!</span></span> <span data-ttu-id="196ff-170">Vous avez correctement déployé votre application web dans Azure.</span><span class="sxs-lookup"><span data-stu-id="196ff-170">You have successfully deployed your web app to Azure.</span></span> 

![« Hello Azure ! »](./media/app-service-web-get-started-java/browse-web-app-1.png)

## <a name="update-the-web-app"></a><span data-ttu-id="196ff-173">Mettre à jour l’application web</span><span class="sxs-lookup"><span data-stu-id="196ff-173">Update the web app</span></span>

<span data-ttu-id="196ff-174">Remplacez l’exemple de code JSP par un autre message.</span><span class="sxs-lookup"><span data-stu-id="196ff-174">Change the sample JSP code to a different message.</span></span>

```jsp
<body>
<h1><% out.println("Hello again Azure!"); %></h1>
</body>
```

<span data-ttu-id="196ff-175">Enregistrez les modifications.</span><span class="sxs-lookup"><span data-stu-id="196ff-175">Save the changes.</span></span>

<span data-ttu-id="196ff-176">Dans l’Explorateur de projets, cliquez avec le bouton droit sur le projet, puis sélectionnez **Azure** > **Publish as Azure Web App (Publier en tant qu’application web Azure)**.</span><span class="sxs-lookup"><span data-stu-id="196ff-176">In Project Explorer, right-click the project, and then select **Azure** > **Publish as Azure Web App**.</span></span>

<span data-ttu-id="196ff-177">La boîte de dialogue **Déployer une application web** s’affiche en vous présentant le service App Service que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="196ff-177">The **Deploy Web App** dialog box appears and shows the app service that you previously created.</span></span> 

> [!NOTE]
> <span data-ttu-id="196ff-178">Sélectionnez **Deploy to root (Déployer à la racine)** chaque fois que vous effectuez une publication.</span><span class="sxs-lookup"><span data-stu-id="196ff-178">Select **Deploy to root** each time you publish.</span></span>
>

<span data-ttu-id="196ff-179">Sélectionnez l’application web, puis sélectionnez **Déployer**, ce qui publie les modifications.</span><span class="sxs-lookup"><span data-stu-id="196ff-179">Select the web app and select **Deploy**, which publishes the changes.</span></span>

<span data-ttu-id="196ff-180">Lorsque le lien **Publication** apparaît, sélectionnez-le pour accéder à l’application web et voir les modifications.</span><span class="sxs-lookup"><span data-stu-id="196ff-180">When the **Publishing** link appears, select it to browse to the web app and see the changes.</span></span>

## <a name="manage-the-web-app"></a><span data-ttu-id="196ff-181">Gérer l’application web</span><span class="sxs-lookup"><span data-stu-id="196ff-181">Manage the web app</span></span>

<span data-ttu-id="196ff-182">Accédez au <a href="https://portal.azure.com" target="_blank">Portail Azure</a> pour visualiser l’application web que vous avez créée.</span><span class="sxs-lookup"><span data-stu-id="196ff-182">Go to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> to see the web app that you created.</span></span>

<span data-ttu-id="196ff-183">Dans le menu de gauche, sélectionnez **Groupes de ressources**.</span><span class="sxs-lookup"><span data-stu-id="196ff-183">From the left menu, select **Resource Groups**.</span></span>

![Accès aux groupes de ressources au moyen du portail](media/app-service-web-get-started-java/rg.png)

<span data-ttu-id="196ff-185">Sélectionnez le groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="196ff-185">Select the resource group.</span></span> <span data-ttu-id="196ff-186">La page affiche les ressources que vous avez créées dans ce guide de démarrage rapide.</span><span class="sxs-lookup"><span data-stu-id="196ff-186">The page shows the resources that you created in this quickstart.</span></span>

![Groupe de ressources myResourceGroup](media/app-service-web-get-started-java/rg2.png)

<span data-ttu-id="196ff-188">Sélectionnez l’application web (**webapp-170602193915** dans la figure précédente).</span><span class="sxs-lookup"><span data-stu-id="196ff-188">Select the web app (**webapp-170602193915** in the preceding image).</span></span>

<span data-ttu-id="196ff-189">La page **Vue d’ensemble** s’affiche.</span><span class="sxs-lookup"><span data-stu-id="196ff-189">The **Overview** page appears.</span></span> <span data-ttu-id="196ff-190">Cette page présente un aperçu de l’application.</span><span class="sxs-lookup"><span data-stu-id="196ff-190">This page gives you a view of how the app is doing.</span></span> <span data-ttu-id="196ff-191">Elle vous permet d’exécuter des tâches de gestion de base, telles que parcourir, arrêter, démarrer, redémarrer et supprimer.</span><span class="sxs-lookup"><span data-stu-id="196ff-191">Here, you can  perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="196ff-192">Les onglets figurant sur le côté gauche de la page affichent les différentes configurations que vous pouvez ouvrir.</span><span class="sxs-lookup"><span data-stu-id="196ff-192">The tabs on the left side of the page show the different configurations that you can open.</span></span> 

![Page App Service du Portail Azure](media/app-service-web-get-started-java/web-app-blade.png)

[!INCLUDE [clean-up-section-portal-web-app](../../includes/clean-up-section-portal-web-app.md)]

## <a name="next-steps"></a><span data-ttu-id="196ff-194">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="196ff-194">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="196ff-195">Mapper un domaine personnalisé</span><span class="sxs-lookup"><span data-stu-id="196ff-195">Map custom domain</span></span>](app-service-web-tutorial-custom-domain.md)
