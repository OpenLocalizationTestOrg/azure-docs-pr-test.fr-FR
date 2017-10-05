---
title: Instructions de connexion pour le Kit de ressources Azure pour IntelliJ | Documents Microsoft
description: "Découvrez comment vous connecter à Microsoft Azure à l’aide du Kit de ressources Azure pour IntelliJ."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 4e2ed072bdaea0a71fef042c0c72b7656a42bbe8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="sign-in-instructions-for-the-azure-toolkit-for-intellij"></a><span data-ttu-id="ae552-103">Instructions de connexion pour le Kit de ressources Azure pour IntelliJ</span><span class="sxs-lookup"><span data-stu-id="ae552-103">Sign-in instructions for the Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="ae552-104">Le Kit de ressources Azure pour IntelliJ vous permet de vous connecter à votre compte Azure à l’aide de deux méthodes :</span><span class="sxs-lookup"><span data-stu-id="ae552-104">The Azure Toolkit for IntelliJ provides two methods for signing in to your Azure account:</span></span>

  * <span data-ttu-id="ae552-105">**Interactive**: vous entrez vos informations d’identification Azure chaque fois que vous vous connectez à votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="ae552-105">**Interactive**: You enter your Azure credentials each time you sign in to your Azure account.</span></span>
  * <span data-ttu-id="ae552-106">**Automatisée** : vous créez un fichier d’informations d’identification que vous pouvez utiliser pour vous connecter automatiquement à votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="ae552-106">**Automated**: You create a credentials file that you can use to automatically sign in to your Azure account.</span></span>

<span data-ttu-id="ae552-107">Les sections suivantes décrivent comment utiliser chaque méthode.</span><span class="sxs-lookup"><span data-stu-id="ae552-107">The following sections describe how to use each method.</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="sign-in-to-your-azure-account-interactively"></a><span data-ttu-id="ae552-108">Connexion à votre compte Azure de façon interactive</span><span class="sxs-lookup"><span data-stu-id="ae552-108">Sign in to your Azure account interactively</span></span>

<span data-ttu-id="ae552-109">Pour vous connecter à Azure en entrant manuellement vos informations d’identification, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="ae552-109">To sign in to Azure by manually entering your Azure credentials, do the following:</span></span>

1. <span data-ttu-id="ae552-110">Ouvrez votre projet avec IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="ae552-110">Open your project with IntelliJ IDEA.</span></span>

2. <span data-ttu-id="ae552-111">Cliquez sur **Outils**, pointez sur **Azure**, puis cliquez sur **Connexion à Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="ae552-111">Click **Tools**, point to **Azure**, and then click **Azure Sign In**.</span></span>

   ![Commande IntelliJ de connexion à Azure][I01]

3. <span data-ttu-id="ae552-113">Dans la fenêtre **Connexion à Azure** qui s’affiche, sélectionnez **Interactive**, puis cliquez sur **Se connecter**.</span><span class="sxs-lookup"><span data-stu-id="ae552-113">In the **Azure Sign In** window, select **Interactive**, and then click **Sign in**.</span></span>

   ![Fenêtre Connexion à Azure avec l’option Interactive activée][I02]

4. <span data-ttu-id="ae552-115">Dans la boîte de dialogue **Connexion à Azure** qui s’affiche, entrez vos informations d’identification Azure, puis cliquez sur **Se connecter**.</span><span class="sxs-lookup"><span data-stu-id="ae552-115">In the **Azure Log In** dialog box appears, enter your Azure credentials, and then click **Sign in**.</span></span>

   ![Boîte de dialogue Connexion à Azure][I03]

5. <span data-ttu-id="ae552-117">Lorsque la boîte de dialogue **Sélectionner des abonnements**, sélectionnez les abonnements que vous souhaitez utiliser, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="ae552-117">In the **Select Subscriptions** dialog box, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![Boîte de dialogue Sélectionner des abonnements][I04]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-interactively"></a><span data-ttu-id="ae552-119">Déconnexion de votre compte Azure après vous être connecté de manière interactive</span><span class="sxs-lookup"><span data-stu-id="ae552-119">Sign out of your Azure account after you have signed in interactively</span></span>

<span data-ttu-id="ae552-120">Après que vous avez configuré votre compte en procédant de la manière décrite les étapes précédentes, vous êtes automatiquement déconnecté de votre compte Azure à chaque redémarrage d’IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="ae552-120">After you have configured your account by using the preceding steps, you will be automatically signed out of your Azure account each time you restart IntelliJ IDEA.</span></span> <span data-ttu-id="ae552-121">En revanche, si vous souhaitez vous déconnecter de votre compte Azure *sans* redémarrer IntelliJ IDEA, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="ae552-121">However, if you want to sign out of your Azure account *without* restarting IntelliJ IDEA, do the following.</span></span>

1. <span data-ttu-id="ae552-122">Dans IntelliJ IDEA, dans le menu **Outils**, pointez sur **Azure**, puis cliquez sur **Déconnexion de Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="ae552-122">In IntelliJ IDEA, on the **Tools** menu, point to **Azure**, and then click **Azure Sign Out**.</span></span>

   ![Commande IntelliJ de déconnexion d’Azure][L01]

2. <span data-ttu-id="ae552-124">Dans la fenêtre de confirmation **e déconnecter de Microsoft Azure**, cliquez sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="ae552-124">In the **Azure Sign Out** confirmation window, click **Yes**.</span></span>

   ![Fenêtre de confirmation de déconnexion d’Azure][L02]

## <a name="sign-in-to-your-azure-account-automatically"></a><span data-ttu-id="ae552-126">Connexion automatique à votre compte Azure</span><span class="sxs-lookup"><span data-stu-id="ae552-126">Sign in to your Azure account automatically</span></span>

<span data-ttu-id="ae552-127">Cette section vous guide dans la création d’un fichier d’informations d’identification contenant les données de votre principal de service.</span><span class="sxs-lookup"><span data-stu-id="ae552-127">This section walks you through creating a credentials file that contains your service principal data.</span></span> <span data-ttu-id="ae552-128">Une fois ce processus terminé, Eclipse utilise le fichier d’informations d’identification pour vous connecter automatiquement à Azure chaque fois que vous ouvrez votre projet.</span><span class="sxs-lookup"><span data-stu-id="ae552-128">After you have completed this process, Eclipse uses the credentials file to automatically sign you in to Azure each time you open your project.</span></span>

1. <span data-ttu-id="ae552-129">Ouvrez votre projet avec IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="ae552-129">Open your project with IntelliJ IDEA.</span></span>

2. <span data-ttu-id="ae552-130">Dans le menu **Outils**, pointez sur **Azure**, puis cliquez sur **Connexion à Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="ae552-130">On the **Tools** menu, point to **Azure**, and then click **Azure Sign In**.</span></span>

   ![Commande IntelliJ de connexion à Azure][A01]

3. <span data-ttu-id="ae552-132">Dans la fenêtre **Connexion à Microsoft Azure**, sélectionnez **Automatisée**, puis cliquez sur **Nouveau**.</span><span class="sxs-lookup"><span data-stu-id="ae552-132">In the **Azure Sign In** window, select **Automated**, and then click **New**.</span></span>

   ![Fenêtre Connexion à Microsoft Azure avec l’option Automatique activée][A02]

4. <span data-ttu-id="ae552-134">Dans la boîte de dialogue **Connexion à Azure** qui s’affiche, entrez vos informations d’identification Azure, puis cliquez sur **Se connecter**.</span><span class="sxs-lookup"><span data-stu-id="ae552-134">In the **Azure Login Dialog** window, enter your Azure credentials, and then click **Sign in**.</span></span>

   ![Boîte de dialogue Connexion à Azure][A03]

5. <span data-ttu-id="ae552-136">Dans la fenêtre **Créer les fichiers d’authentification**, sélectionnez les abonnements que vous souhaitez utiliser, choisissez votre répertoire de destination, puis cliquez sur **Démarrer**.</span><span class="sxs-lookup"><span data-stu-id="ae552-136">In the **Create Authentication Files** window, select the subscriptions that you want to use, choose your destination directory, and then click **Start**.</span></span>

   ![Fenêtre Créer les fichiers d’authentification][A04]

6. <span data-ttu-id="ae552-138">Dans la boîte de dialogue **État de création du principal de service** qui s’affiche, une fois vos fichiers créés, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="ae552-138">In the **Service Principal Creation Status** dialog box, after your files have been created successfully, click **OK**.</span></span>

   ![Boîte de dialogue État de création du principal de service][A05]

7. <span data-ttu-id="ae552-140">Dans la fenêtre **Connexion à Microsoft Azure**, cliquez sur **Se connecter**.</span><span class="sxs-lookup"><span data-stu-id="ae552-140">In the **Azure Sign In** window, click **Sign in**.</span></span>

   ![Boîte de dialogue Connexion à Azure][A06]

8. <span data-ttu-id="ae552-142">Lorsque la boîte de dialogue **Sélectionner des abonnements**, sélectionnez les abonnements que vous souhaitez utiliser, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="ae552-142">In the **Select Subscriptions** dialog box, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![Boîte de dialogue Sélectionner des abonnements][A07]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-automatically"></a><span data-ttu-id="ae552-144">Déconnexion de votre compte Azure après vous être connecté automatiquement</span><span class="sxs-lookup"><span data-stu-id="ae552-144">Sign out of your Azure account after you have signed in automatically</span></span>

<span data-ttu-id="ae552-145">Après que vous avez configuré votre compte en suivant la procédure précédente, le Kit de ressources Azure vous connecte automatiquement à votre compte Azure chaque fois que vous redémarrez IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="ae552-145">After you have configured your account by using the preceding steps, the Azure Toolkit automatically signs you in to your Azure account each time you restart IntelliJ IDEA.</span></span> <span data-ttu-id="ae552-146">Toutefois, pour vous déconnecter de votre compte Azure et empêcher le Kit de ressources Azure de vous connecter automatiquement, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="ae552-146">However, to sign out of your Azure account and prevent the Azure Toolkit from signing you in automatically, do the following:</span></span>

1. <span data-ttu-id="ae552-147">Dans IntelliJ IDEA, dans le menu **Outils**, pointez sur **Azure**, puis cliquez sur **Déconnexion de Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="ae552-147">In IntelliJ IDEA, on the **Tools** menu, point to **Azure**, and then click **Azure Sign Out**.</span></span>

   ![Commande IntelliJ de déconnexion d’Azure][L01]

2. <span data-ttu-id="ae552-149">Dans la fenêtre de confirmation **e déconnecter de Microsoft Azure**, cliquez sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="ae552-149">In the **Azure Sign Out** confirmation window, click **Yes**.</span></span>

   ![Fenêtre de confirmation de déconnexion d’Azure][L03]

## <a name="sign-in-to-your-azure-account-automatically-by-using-an-existing-credentials-file"></a><span data-ttu-id="ae552-151">Connexion automatique à votre compte Azure à l’aide d’un fichier d’informations d’identification existant</span><span class="sxs-lookup"><span data-stu-id="ae552-151">Sign in to your Azure account automatically by using an existing credentials file</span></span>

<span data-ttu-id="ae552-152">Si vous vous déconnectez de votre compte Azure alors que vous utilisez IntelliJ IDEA, vous devez utiliser un fichier d’informations d’identification existant pour vous reconnecter automatiquement au compte.</span><span class="sxs-lookup"><span data-stu-id="ae552-152">If you sign out of your Azure account when you are using IntelliJ IDEA, you must use an existing credentials file to automatically sign back in to the account.</span></span> <span data-ttu-id="ae552-153">Pour configurer le Kit de ressources Azure pour Eclipse afin d’utiliser un fichier d’informations d’identification existant, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="ae552-153">To configure the Azure Toolkit for Eclipse to use an existing credentials file, do the following:</span></span>

1. <span data-ttu-id="ae552-154">Ouvrez votre projet avec IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="ae552-154">Open your project with IntelliJ IDEA.</span></span>

2. <span data-ttu-id="ae552-155">Dans le menu **Outils**, pointez sur **Azure**, puis cliquez sur **Connexion à Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="ae552-155">On the **Tools** menu, point to **Azure**, and then click **Azure Sign In**.</span></span>

   ![Commande IntelliJ de connexion à Azure][A01]

3. <span data-ttu-id="ae552-157">Dans la fenêtre **Connexion à Microsoft Azure**, sélectionnez **Automatisée**, puis cliquez sur **Parcourir**.</span><span class="sxs-lookup"><span data-stu-id="ae552-157">In the **Azure Sign In** window, select **Automated**, and then click **Browse**.</span></span>

   ![Fenêtre Connexion à Microsoft Azure avec l’option Automatique activée][A02]

4. <span data-ttu-id="ae552-159">Dans la boîte de dialogue **Sélectionner le fichier d’authentification**, choisissez un fichier d’informations d’identification créé précédemment, puis cliquez sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="ae552-159">In the **Select Authentication File** dialog box, select a previously created credentials file, and then click **Select**.</span></span>

   ![Boîte de dialogue Sélectionner le fichier d’authentification][A08]

5. <span data-ttu-id="ae552-161">Dans la fenêtre **Connexion à Microsoft Azure**, cliquez sur **Se connecter**.</span><span class="sxs-lookup"><span data-stu-id="ae552-161">In the **Azure Sign In** window, click **Sign in**.</span></span>

   ![Fenêtre Connexion à Microsoft Azure avec l’option Automatique activée][A06]

6. <span data-ttu-id="ae552-163">Lorsque la boîte de dialogue **Sélectionner des abonnements**, sélectionnez les abonnements que vous souhaitez utiliser, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="ae552-163">In the **Select Subscriptions** dialog box, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![Boîte de dialogue Sélectionner des abonnements][A07]

## <a name="next-steps"></a><span data-ttu-id="ae552-165">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ae552-165">Next steps</span></span>
<span data-ttu-id="ae552-166">Pour plus d’informations sur les boîtes à outils Azure pour les environnements de développement Java, consultez les liens suivants :</span><span class="sxs-lookup"><span data-stu-id="ae552-166">For more information about the Azure Toolkits for Java IDEs, see the following links:</span></span>

* <span data-ttu-id="ae552-167">[Kit de ressources Azure pour Eclipse]</span><span class="sxs-lookup"><span data-stu-id="ae552-167">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="ae552-168">[Nouveautés du Kit de ressources Azure pour Eclipse]</span><span class="sxs-lookup"><span data-stu-id="ae552-168">[What's new in the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="ae552-169">[Installation du kit de ressources Azure pour Eclipse]</span><span class="sxs-lookup"><span data-stu-id="ae552-169">[Installing the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="ae552-170">[Instructions de connexion pour le Kit de ressources Azure pour Eclipse]</span><span class="sxs-lookup"><span data-stu-id="ae552-170">[Sign-in instructions for the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="ae552-171">[Créer une application web Hello World pour Azure dans Eclipse]</span><span class="sxs-lookup"><span data-stu-id="ae552-171">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="ae552-172">[Kit de ressources Azure pour IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="ae552-172">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="ae552-173">[Nouveautés du Kit de ressources Azure pour IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="ae552-173">[What's new in the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="ae552-174">[Installation du kit de ressources Azure pour IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="ae552-174">[Installing the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="ae552-175">*Instructions de connexion pour le Kit de ressources Azure pour IntelliJ* (cet article)</span><span class="sxs-lookup"><span data-stu-id="ae552-175">*Sign-in instructions for the Azure Toolkit for IntelliJ* (this article)</span></span>
  * <span data-ttu-id="ae552-176">[Créer une application web Hello World pour Azure dans IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="ae552-176">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="ae552-177">Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez le [Centre de développement Java pour Azure] et les [outils Java pour Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="ae552-177">For more information about using Azure with Java, see the [Azure Java Developer Center] and the [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

<span data-ttu-id="ae552-178">[Kit de ressources Azure pour Eclipse]: ./azure-toolkit-for-eclipse.md</span><span class="sxs-lookup"><span data-stu-id="ae552-178">[Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse.md</span></span>
<span data-ttu-id="ae552-179">[Kit de ressources Azure pour IntelliJ]: ./azure-toolkit-for-intellij.md</span><span class="sxs-lookup"><span data-stu-id="ae552-179">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md</span></span>
<span data-ttu-id="ae552-180">[Créer une application web Hello World pour Azure dans Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="ae552-180">[Create a Hello World Web App for Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span></span>
<span data-ttu-id="ae552-181">[Créer une application web Hello World pour Azure dans IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="ae552-181">[Create a Hello World web app for Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span></span>
<span data-ttu-id="ae552-182">[Installation du kit de ressources Azure pour Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span><span class="sxs-lookup"><span data-stu-id="ae552-182">[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span></span>
<span data-ttu-id="ae552-183">[Installation du kit de ressources Azure pour IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span><span class="sxs-lookup"><span data-stu-id="ae552-183">[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span></span>
<span data-ttu-id="ae552-184">[Instructions de connexion pour le Kit de ressources Azure pour Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="ae552-184">[Sign-in instructions for the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span></span>
[Sign-in instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
<span data-ttu-id="ae552-185">[Nouveautés du Kit de ressources Azure pour Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="ae552-185">[What's new in the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span></span>
<span data-ttu-id="ae552-186">[Nouveautés du Kit de ressources Azure pour IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="ae552-186">[What's new in the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span></span>

<span data-ttu-id="ae552-187">[Centre de développement Java pour Azure]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="ae552-187">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
<span data-ttu-id="ae552-188">[outils Java pour Visual Studio Team Services]: https://java.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="ae552-188">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span></span>

<!-- IMG List -->

[I01]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I01.png
[I02]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I02.png
[I03]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I03.png
[I04]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I04.png

[A01]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A01.png
[A02]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A02.png
[A03]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A03.png
[A04]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A04.png
[A05]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A05.png
[A06]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A06.png
[A07]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A07.png
[A08]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A08.png

[L01]: ./media/azure-toolkit-for-intellij-sign-in-instructions/L01.png
[L02]: ./media/azure-toolkit-for-intellij-sign-in-instructions/L02.png
[L03]: ./media/azure-toolkit-for-intellij-sign-in-instructions/L03.png
