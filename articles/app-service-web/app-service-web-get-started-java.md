---
title: "aaaCreate votre première application de web Java dans Azure"
description: "Découvrez comment toorun web des applications dans le Service d’applications en déployant une application Java de base."
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
ms.openlocfilehash: 81315c07b5aa84cbec50a17b2cb3914927b19c00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-java-web-app-in-azure"></a><span data-ttu-id="33804-103">Créer votre première application web Java dans Azure</span><span class="sxs-lookup"><span data-stu-id="33804-103">Create your first Java web app in Azure</span></span>

<span data-ttu-id="33804-104">Hello [Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) fonctionnalité de [Azure App Service](../app-service/app-service-value-prop-what-is.md) fournit une service d’hébergement web hautement évolutif et correction automatique.</span><span class="sxs-lookup"><span data-stu-id="33804-104">hello [Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) feature of [Azure App Service](../app-service/app-service-value-prop-what-is.md) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="33804-105">Ce démarrage rapide montre comment toodeploy Java web application tooApp Service à l’aide de hello [IDE Eclipse pour développeurs Java EE](http://www.eclipse.org/).</span><span class="sxs-lookup"><span data-stu-id="33804-105">This quickstart shows how toodeploy a Java web app tooApp Service by using hello [Eclipse IDE for Java EE Developers](http://www.eclipse.org/).</span></span>

![« Hello Azure ! »](./media/app-service-web-get-started-java/browse-web-app-1.png)

## <a name="prerequisites"></a><span data-ttu-id="33804-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="33804-108">Prerequisites</span></span>

<span data-ttu-id="33804-109">toocomplete ce démarrage rapide, installer :</span><span class="sxs-lookup"><span data-stu-id="33804-109">toocomplete this quickstart, install:</span></span>

* <span data-ttu-id="33804-110">Hello libre [IDE Eclipse pour développeurs Java EE](http://www.eclipse.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="33804-110">hello free [Eclipse IDE for Java EE Developers](http://www.eclipse.org/downloads/).</span></span> <span data-ttu-id="33804-111">Ce démarrage rapide utilise Eclipse Neon.</span><span class="sxs-lookup"><span data-stu-id="33804-111">This quickstart uses Eclipse Neon.</span></span>
* <span data-ttu-id="33804-112">Hello [boîte à outils Azure pour Eclipse](/azure/azure-toolkit-for-eclipse-installation).</span><span class="sxs-lookup"><span data-stu-id="33804-112">hello [Azure Toolkit for Eclipse](/azure/azure-toolkit-for-eclipse-installation).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-dynamic-web-project-in-eclipse"></a><span data-ttu-id="33804-113">Créer un projet web dynamique dans Eclipse</span><span class="sxs-lookup"><span data-stu-id="33804-113">Create a dynamic web project in Eclipse</span></span>

<span data-ttu-id="33804-114">Dans Eclipse, sélectionnez **File (Fichier)** > **New (Nouveau)** > **Dynamic Web Project (Projet web dynamique)**.</span><span class="sxs-lookup"><span data-stu-id="33804-114">In Eclipse, select **File** > **New** > **Dynamic Web Project**.</span></span>

<span data-ttu-id="33804-115">Bonjour **nouveau projet Web dynamique** boîte de dialogue, les projets de hello nom **MyFirstJavaOnAzureWebApp**, puis sélectionnez **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="33804-115">In hello **New Dynamic Web Project** dialog box, name hello project **MyFirstJavaOnAzureWebApp**, and select **Finish**.</span></span>
   
![Boîte de dialogue Projet web dynamique](./media/app-service-web-get-started-java/new-dynamic-web-project-dialog-box.png)

### <a name="add-a-jsp-page"></a><span data-ttu-id="33804-117">Ajouter une page JSP</span><span class="sxs-lookup"><span data-stu-id="33804-117">Add a JSP page</span></span>

<span data-ttu-id="33804-118">Si l’Explorateur de projets n’est pas affiché, restaurez-le.</span><span class="sxs-lookup"><span data-stu-id="33804-118">If Project Explorer is not displayed, restore it.</span></span>

![Espace de travail Java EE pour Eclipse](./media/app-service-web-get-started-java/pe.png)

<span data-ttu-id="33804-120">Dans l’Explorateur de projets, développez hello **MyFirstJavaOnAzureWebApp** projet.</span><span class="sxs-lookup"><span data-stu-id="33804-120">In Project Explorer, expand hello **MyFirstJavaOnAzureWebApp** project.</span></span>
<span data-ttu-id="33804-121">Cliquez avec le bouton droit sur **WebContent**, puis sélectionnez **New (Nouveau)** > **JSP File (Fichier JSP)**.</span><span class="sxs-lookup"><span data-stu-id="33804-121">Right-click **WebContent**, and then select **New** > **JSP File**.</span></span>

![Menu d’un nouveau fichier JSP dans l’Explorateur de projets](./media/app-service-web-get-started-java/new-jsp-file-menu.png)

<span data-ttu-id="33804-123">Bonjour **nouveau fichier JSP** boîte de dialogue :</span><span class="sxs-lookup"><span data-stu-id="33804-123">In hello **New JSP File** dialog box:</span></span>

* <span data-ttu-id="33804-124">Nom de fichier hello **index.jsp**.</span><span class="sxs-lookup"><span data-stu-id="33804-124">Name hello file **index.jsp**.</span></span>
* <span data-ttu-id="33804-125">Sélectionnez **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="33804-125">Select **Finish**.</span></span>

  ![Boîte de dialogue New JSP File (Nouveau fichier JSP)](./media/app-service-web-get-started-java/new-jsp-file-dialog-box-page-1.png)

<span data-ttu-id="33804-127">Dans le fichier index.jsp de hello, remplacez hello `<body></body>` élément avec hello suivant de balisage :</span><span class="sxs-lookup"><span data-stu-id="33804-127">In hello index.jsp file, replace hello `<body></body>` element with hello following markup:</span></span>

```jsp
<body>
<h1><% out.println("Hello Azure!"); %></h1>
</body>
```

<span data-ttu-id="33804-128">Enregistrer les modifications de hello.</span><span class="sxs-lookup"><span data-stu-id="33804-128">Save hello changes.</span></span>

## <a name="publish-hello-web-app-tooazure"></a><span data-ttu-id="33804-129">Publier hello web application tooAzure</span><span class="sxs-lookup"><span data-stu-id="33804-129">Publish hello web app tooAzure</span></span>

<span data-ttu-id="33804-130">Dans l’Explorateur de projets, cliquez sur le projet de hello et sélectionnez **Azure** > **publier en tant qu’application Web Azure**.</span><span class="sxs-lookup"><span data-stu-id="33804-130">In Project Explorer, right-click hello project, and then select **Azure** > **Publish as Azure Web App**.</span></span>

![Menu contextuel Publish as Azure Web App (Publier en tant qu’application web Azure)](./media/app-service-web-get-started-java/publish-as-azure-web-app-context-menu.png)

<span data-ttu-id="33804-132">Bonjour **Azure Sign In** boîte de dialogue, gardez hello **Interactive** option et sélectionnez **connectez-vous**.</span><span class="sxs-lookup"><span data-stu-id="33804-132">In hello **Azure Sign In** dialog box, keep hello **Interactive** option, and then select **Sign in**.</span></span>

<span data-ttu-id="33804-133">Suivez hello connectez-vous instructions.</span><span class="sxs-lookup"><span data-stu-id="33804-133">Follow hello sign-in instructions.</span></span>

### <a name="deploy-web-app-dialog-box"></a><span data-ttu-id="33804-134">Boîte de dialogue Déployer une application web</span><span class="sxs-lookup"><span data-stu-id="33804-134">Deploy Web App dialog box</span></span>

<span data-ttu-id="33804-135">Une fois que vous avez connecté tooyour compte Azure, hello **déployer l’application Web** boîte de dialogue s’affiche.</span><span class="sxs-lookup"><span data-stu-id="33804-135">After you have signed in tooyour Azure account, hello **Deploy Web App** dialog box appears.</span></span>

<span data-ttu-id="33804-136">Sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="33804-136">Select **Create**.</span></span>

![Boîte de dialogue Déployer une application web](./media/app-service-web-get-started-java/deploy-web-app-dialog-box.png)

### <a name="create-app-service-dialog-box"></a><span data-ttu-id="33804-138">Boîte de dialogue Créer App Service</span><span class="sxs-lookup"><span data-stu-id="33804-138">Create App Service dialog box</span></span>

<span data-ttu-id="33804-139">Hello **créer un Service application** boîte de dialogue s’affiche avec les valeurs par défaut.</span><span class="sxs-lookup"><span data-stu-id="33804-139">hello **Create App Service** dialog box appears with default values.</span></span> <span data-ttu-id="33804-140">nombre de Hello **170602185241** illustré hello suivant image est différente dans votre boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="33804-140">hello number **170602185241** shown in hello following image is different in your dialog box.</span></span>

![Boîte de dialogue Créer App Service](./media/app-service-web-get-started-java/cas1.png)

<span data-ttu-id="33804-142">Bonjour **créer un Service application** boîte de dialogue :</span><span class="sxs-lookup"><span data-stu-id="33804-142">In hello **Create App Service** dialog box:</span></span>

* <span data-ttu-id="33804-143">Conservez le nom hello généré pour l’application web de hello.</span><span class="sxs-lookup"><span data-stu-id="33804-143">Keep hello generated name for hello web app.</span></span> <span data-ttu-id="33804-144">Ce nom doit être unique au sein d’Azure.</span><span class="sxs-lookup"><span data-stu-id="33804-144">This name must be unique across Azure.</span></span> <span data-ttu-id="33804-145">nom de Hello fait partie de l’adresse URL de hello pour l’application web de hello.</span><span class="sxs-lookup"><span data-stu-id="33804-145">hello name is part of hello URL address for hello web app.</span></span> <span data-ttu-id="33804-146">Par exemple : si le nom de l’application web hello est **MyJavaWebApp**, hello URL est *myjavawebapp.azurewebsites.net*.</span><span class="sxs-lookup"><span data-stu-id="33804-146">For example: if hello web app name is **MyJavaWebApp**, hello URL is *myjavawebapp.azurewebsites.net*.</span></span>
* <span data-ttu-id="33804-147">Conserver le conteneur de web hello par défaut.</span><span class="sxs-lookup"><span data-stu-id="33804-147">Keep hello default web container.</span></span>
* <span data-ttu-id="33804-148">Sélectionnez un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="33804-148">Select an Azure subscription.</span></span>
* <span data-ttu-id="33804-149">Sur hello **plan App service** onglet :</span><span class="sxs-lookup"><span data-stu-id="33804-149">On hello **App service plan** tab:</span></span>

  * <span data-ttu-id="33804-150">**Créer de nouveaux**: conserver la valeur par défaut de hello, qui est le nom hello Hello plan App Service.</span><span class="sxs-lookup"><span data-stu-id="33804-150">**Create new**: Keep hello default, which is hello name of hello App Service plan.</span></span>
  * <span data-ttu-id="33804-151">**Emplacement** : sélectionnez **Europe de l’Ouest** ou un emplacement près de chez vous.</span><span class="sxs-lookup"><span data-stu-id="33804-151">**Location**: Select **West Europe** or a location near you.</span></span>
  * <span data-ttu-id="33804-152">**Niveau de tarification**: sélectionnez hello option disponible.</span><span class="sxs-lookup"><span data-stu-id="33804-152">**Pricing tier**: Select hello free option.</span></span> <span data-ttu-id="33804-153">Pour plus d’informations sur les fonctionnalités, consultez la page [Tarification de App Service](https://azure.microsoft.com/pricing/details/app-service/).</span><span class="sxs-lookup"><span data-stu-id="33804-153">For features, see [App Service pricing](https://azure.microsoft.com/pricing/details/app-service/).</span></span>

   ![Boîte de dialogue Créer App Service](./media/app-service-web-get-started-java/create-app-service-dialog-box.png)

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

### <a name="resource-group-tab"></a><span data-ttu-id="33804-155">Onglet Groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="33804-155">Resource group tab</span></span>

<span data-ttu-id="33804-156">Sélectionnez hello **groupe de ressources** onglet. Conservez hello générée par défaut pour le groupe de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="33804-156">Select hello **Resource group** tab. Keep hello default generated value for hello resource group.</span></span>

![Onglet Groupe de ressources](./media/app-service-web-get-started-java/create-app-service-resource-group.png)

[!INCLUDE [resource-group](../../includes/resource-group.md)]

<span data-ttu-id="33804-158">Sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="33804-158">Select **Create**.</span></span>

<!--
### hello JDK tab

Select hello **JDK** tab. Keep hello default, and then select **Create**.

![Create App Service plan](./media/app-service-web-get-started-java/create-app-service-specify-jdk.png)
-->

<span data-ttu-id="33804-159">Hello boîte à outils Azure crée l’application web hello et affiche une boîte de dialogue de progression.</span><span class="sxs-lookup"><span data-stu-id="33804-159">hello Azure Toolkit creates hello web app and displays a progress dialog box.</span></span>

![Boîte de dialogue indiquant la progression de la création du service App Service](./media/app-service-web-get-started-java/create-app-service-progress-bar.png)

### <a name="deploy-web-app-dialog-box"></a><span data-ttu-id="33804-161">Boîte de dialogue Déployer une application web</span><span class="sxs-lookup"><span data-stu-id="33804-161">Deploy Web App dialog box</span></span>

<span data-ttu-id="33804-162">Bonjour **déployer l’application Web** boîte de dialogue, sélectionnez **déployer tooroot**.</span><span class="sxs-lookup"><span data-stu-id="33804-162">In hello **Deploy Web App** dialog box, select **Deploy tooroot**.</span></span> <span data-ttu-id="33804-163">Si vous avez un service d’application à *wingtiptoys.azurewebsites.net* et vous ne déployez pas toohello racine, l’application hello web nommée **MyFirstJavaOnAzureWebApp** est déployé trop *wingtiptoys.azurewebsites.net/MyFirstJavaOnAzureWebApp*.</span><span class="sxs-lookup"><span data-stu-id="33804-163">If you have an app service at *wingtiptoys.azurewebsites.net* and you do not deploy toohello root, hello web app named **MyFirstJavaOnAzureWebApp** is deployed too*wingtiptoys.azurewebsites.net/MyFirstJavaOnAzureWebApp*.</span></span>

![Boîte de dialogue Déployer une application web](./media/app-service-web-get-started-java/deploy-web-app-to-root.png)

<span data-ttu-id="33804-165">zone de boîte de dialogue Hello indique Bonjour Azure JDK et les sélections web conteneur.</span><span class="sxs-lookup"><span data-stu-id="33804-165">hello dialog box shows hello Azure, JDK, and web container selections.</span></span>

<span data-ttu-id="33804-166">Sélectionnez **déployer** toopublish hello web application tooAzure.</span><span class="sxs-lookup"><span data-stu-id="33804-166">Select **Deploy** toopublish hello web app tooAzure.</span></span>

<span data-ttu-id="33804-167">Une fois la publication hello, sélectionnez hello **publié** lien Bonjour **journal des activités Azure** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="33804-167">When hello publishing finishes, select hello **Published** link in hello **Azure Activity Log** dialog box.</span></span>

![Boîte de dialogue Journal d’activité Azure](./media/app-service-web-get-started-java/aal.png)

<span data-ttu-id="33804-169">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="33804-169">Congratulations!</span></span> <span data-ttu-id="33804-170">Vous avez correctement déployé votre tooAzure d’application web.</span><span class="sxs-lookup"><span data-stu-id="33804-170">You have successfully deployed your web app tooAzure.</span></span> 

![« Hello Azure ! »](./media/app-service-web-get-started-java/browse-web-app-1.png)

## <a name="update-hello-web-app"></a><span data-ttu-id="33804-173">Mettre à jour de l’application web hello</span><span class="sxs-lookup"><span data-stu-id="33804-173">Update hello web app</span></span>

<span data-ttu-id="33804-174">Modifier un exemple JSP code tooa autre message de type hello.</span><span class="sxs-lookup"><span data-stu-id="33804-174">Change hello sample JSP code tooa different message.</span></span>

```jsp
<body>
<h1><% out.println("Hello again Azure!"); %></h1>
</body>
```

<span data-ttu-id="33804-175">Enregistrer les modifications de hello.</span><span class="sxs-lookup"><span data-stu-id="33804-175">Save hello changes.</span></span>

<span data-ttu-id="33804-176">Dans l’Explorateur de projets, cliquez sur le projet de hello et sélectionnez **Azure** > **publier en tant qu’application Web Azure**.</span><span class="sxs-lookup"><span data-stu-id="33804-176">In Project Explorer, right-click hello project, and then select **Azure** > **Publish as Azure Web App**.</span></span>

<span data-ttu-id="33804-177">Hello **déployer l’application Web** boîte de dialogue apparaît et affiche hello du service d’applications que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="33804-177">hello **Deploy Web App** dialog box appears and shows hello app service that you previously created.</span></span> 

> [!NOTE]
> <span data-ttu-id="33804-178">Sélectionnez **déployer tooroot** chaque fois que vous publiez.</span><span class="sxs-lookup"><span data-stu-id="33804-178">Select **Deploy tooroot** each time you publish.</span></span>
>

<span data-ttu-id="33804-179">Sélectionnez l’application web hello **déployer**, qui publie les modifications hello.</span><span class="sxs-lookup"><span data-stu-id="33804-179">Select hello web app and select **Deploy**, which publishes hello changes.</span></span>

<span data-ttu-id="33804-180">Hello lorsque **publication** lien s’affiche, sélectionner l’application web toobrowse toohello et voir les modifications hello.</span><span class="sxs-lookup"><span data-stu-id="33804-180">When hello **Publishing** link appears, select it toobrowse toohello web app and see hello changes.</span></span>

## <a name="manage-hello-web-app"></a><span data-ttu-id="33804-181">Gérer l’application hello web</span><span class="sxs-lookup"><span data-stu-id="33804-181">Manage hello web app</span></span>

<span data-ttu-id="33804-182">Accédez toohello <a href="https://portal.azure.com" target="_blank">portail Azure</a> toosee hello web application que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="33804-182">Go toohello <a href="https://portal.azure.com" target="_blank">Azure portal</a> toosee hello web app that you created.</span></span>

<span data-ttu-id="33804-183">Dans le menu de gauche hello, sélectionnez **groupes de ressources**.</span><span class="sxs-lookup"><span data-stu-id="33804-183">From hello left menu, select **Resource Groups**.</span></span>

![Groupes de navigation du portail tooresource](media/app-service-web-get-started-java/rg.png)

<span data-ttu-id="33804-185">Sélectionnez le groupe de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="33804-185">Select hello resource group.</span></span> <span data-ttu-id="33804-186">page de Hello montre les ressources hello que vous avez créé dans ce démarrage rapide.</span><span class="sxs-lookup"><span data-stu-id="33804-186">hello page shows hello resources that you created in this quickstart.</span></span>

![Groupe de ressources myResourceGroup](media/app-service-web-get-started-java/rg2.png)

<span data-ttu-id="33804-188">Sélectionnez hello web app (**webapp-170602193915** Bonjour précédant l’image).</span><span class="sxs-lookup"><span data-stu-id="33804-188">Select hello web app (**webapp-170602193915** in hello preceding image).</span></span>

<span data-ttu-id="33804-189">Hello **vue d’ensemble** page s’affiche.</span><span class="sxs-lookup"><span data-stu-id="33804-189">hello **Overview** page appears.</span></span> <span data-ttu-id="33804-190">Cette page vous donne un aperçu du faire des application hello.</span><span class="sxs-lookup"><span data-stu-id="33804-190">This page gives you a view of how hello app is doing.</span></span> <span data-ttu-id="33804-191">Elle vous permet d’exécuter des tâches de gestion de base, telles que parcourir, arrêter, démarrer, redémarrer et supprimer.</span><span class="sxs-lookup"><span data-stu-id="33804-191">Here, you can  perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="33804-192">affichent les onglets Hello sur le côté gauche de hello de page de hello hello différentes configurations que vous pouvez ouvrir.</span><span class="sxs-lookup"><span data-stu-id="33804-192">hello tabs on hello left side of hello page show hello different configurations that you can open.</span></span> 

![Page App Service du Portail Azure](media/app-service-web-get-started-java/web-app-blade.png)

[!INCLUDE [clean-up-section-portal-web-app](../../includes/clean-up-section-portal-web-app.md)]

## <a name="next-steps"></a><span data-ttu-id="33804-194">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="33804-194">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="33804-195">Mapper un domaine personnalisé</span><span class="sxs-lookup"><span data-stu-id="33804-195">Map custom domain</span></span>](app-service-web-tutorial-custom-domain.md)
