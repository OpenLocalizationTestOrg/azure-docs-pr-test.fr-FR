---
title: "instructions d’aaaSign pour hello boîte à outils Azure pour IntelliJ | Documents Microsoft"
description: "Découvrez comment toosign dans tooMicrosoft Azure à l’aide de hello boîte à outils Azure pour IntelliJ."
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
ms.openlocfilehash: 2de781fc19267cce133b1e6456481497e165fce4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-instructions-for-hello-azure-toolkit-for-intellij"></a><span data-ttu-id="14bc7-103">Instructions d’authentification pour hello boîte à outils Azure pour IntelliJ</span><span class="sxs-lookup"><span data-stu-id="14bc7-103">Sign-in instructions for hello Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="14bc7-104">Bonjour Azure Toolkit pour IntelliJ propose deux méthodes pour établir la connexion tooyour compte Azure :</span><span class="sxs-lookup"><span data-stu-id="14bc7-104">hello Azure Toolkit for IntelliJ provides two methods for signing in tooyour Azure account:</span></span>

  * <span data-ttu-id="14bc7-105">**Interactive**: vous permet d’entrer vos informations d’identification Azure chaque fois que vous vous connecterez dans tooyour compte Azure.</span><span class="sxs-lookup"><span data-stu-id="14bc7-105">**Interactive**: You enter your Azure credentials each time you sign in tooyour Azure account.</span></span>
  * <span data-ttu-id="14bc7-106">**Automatisée**: vous créez un fichier d’informations d’identification que vous pouvez utiliser l’authentification tooautomatically dans tooyour compte Azure.</span><span class="sxs-lookup"><span data-stu-id="14bc7-106">**Automated**: You create a credentials file that you can use tooautomatically sign in tooyour Azure account.</span></span>

<span data-ttu-id="14bc7-107">Hello sections suivantes décrivent comment toouse chaque méthode.</span><span class="sxs-lookup"><span data-stu-id="14bc7-107">hello following sections describe how toouse each method.</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="sign-in-tooyour-azure-account-interactively"></a><span data-ttu-id="14bc7-108">Se connecter interactivement tooyour compte Azure</span><span class="sxs-lookup"><span data-stu-id="14bc7-108">Sign in tooyour Azure account interactively</span></span>

<span data-ttu-id="14bc7-109">toosign dans tooAzure en entrant manuellement vos informations d’identification Azure, procédez comme hello suivant :</span><span class="sxs-lookup"><span data-stu-id="14bc7-109">toosign in tooAzure by manually entering your Azure credentials, do hello following:</span></span>

1. <span data-ttu-id="14bc7-110">Ouvrez votre projet avec IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="14bc7-110">Open your project with IntelliJ IDEA.</span></span>

2. <span data-ttu-id="14bc7-111">Cliquez sur **outils**, pointez trop**Azure**, puis cliquez sur **Azure Sign In**.</span><span class="sxs-lookup"><span data-stu-id="14bc7-111">Click **Tools**, point too**Azure**, and then click **Azure Sign In**.</span></span>

   ![Hello IntelliJ Azure signe de commandes][I01]

3. <span data-ttu-id="14bc7-113">Bonjour **Azure Sign In** fenêtre, sélectionnez **Interactive**, puis cliquez sur **connectez-vous**.</span><span class="sxs-lookup"><span data-stu-id="14bc7-113">In hello **Azure Sign In** window, select **Interactive**, and then click **Sign in**.</span></span>

   ![Bonjour Azure fenêtre de connexion avec Interactive sélectionné][I02]

4. <span data-ttu-id="14bc7-115">Bonjour **Azure journal dans** boîte de dialogue s’affiche, entrez vos informations d’identification Azure, puis cliquez sur **connectez-vous**.</span><span class="sxs-lookup"><span data-stu-id="14bc7-115">In hello **Azure Log In** dialog box appears, enter your Azure credentials, and then click **Sign in**.</span></span>

   ![fenêtre de boîte de dialogue de connexion Azure Hello][I03]

5. <span data-ttu-id="14bc7-117">Bonjour **sélectionnez les abonnements** boîte de dialogue, les abonnements hello select que vous souhaitez toouse, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="14bc7-117">In hello **Select Subscriptions** dialog box, select hello subscriptions that you want toouse, and then click **OK**.</span></span>

   ![boîte de dialogue Sélectionnez les abonnements Hello][I04]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-interactively"></a><span data-ttu-id="14bc7-119">Déconnexion de votre compte Azure après vous être connecté de manière interactive</span><span class="sxs-lookup"><span data-stu-id="14bc7-119">Sign out of your Azure account after you have signed in interactively</span></span>

<span data-ttu-id="14bc7-120">Après avoir configuré votre compte à l’aide de hello étapes précédentes, vous allez être automatiquement déconnecté votre compte Azure, chaque fois que vous redémarrez IntelliJ idée.</span><span class="sxs-lookup"><span data-stu-id="14bc7-120">After you have configured your account by using hello preceding steps, you will be automatically signed out of your Azure account each time you restart IntelliJ IDEA.</span></span> <span data-ttu-id="14bc7-121">Toutefois, si vous souhaitez dans votre compte Azure toosign *sans* redémarrage IntelliJ idée, hello suivant.</span><span class="sxs-lookup"><span data-stu-id="14bc7-121">However, if you want toosign out of your Azure account *without* restarting IntelliJ IDEA, do hello following.</span></span>

1. <span data-ttu-id="14bc7-122">Dans l’idée IntelliJ, hello **outils** menu, pointez trop**Azure**, puis cliquez sur **Azure se déconnecter**.</span><span class="sxs-lookup"><span data-stu-id="14bc7-122">In IntelliJ IDEA, on hello **Tools** menu, point too**Azure**, and then click **Azure Sign Out**.</span></span>

   ![Hello commande IntelliJ Azure se déconnecter][L01]

2. <span data-ttu-id="14bc7-124">Bonjour **Azure se déconnecter** fenêtre de confirmation, cliquez sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="14bc7-124">In hello **Azure Sign Out** confirmation window, click **Yes**.</span></span>

   ![fenêtre Hello Azure se déconnecter confirmation][L02]

## <a name="sign-in-tooyour-azure-account-automatically"></a><span data-ttu-id="14bc7-126">Se connecter automatiquement tooyour compte Azure</span><span class="sxs-lookup"><span data-stu-id="14bc7-126">Sign in tooyour Azure account automatically</span></span>

<span data-ttu-id="14bc7-127">Cette section vous guide dans la création d’un fichier d’informations d’identification contenant les données de votre principal de service.</span><span class="sxs-lookup"><span data-stu-id="14bc7-127">This section walks you through creating a credentials file that contains your service principal data.</span></span> <span data-ttu-id="14bc7-128">Après avoir terminé ce processus, Eclipse utilise hello tooautomatically informations d’identification de fichier signe dans tooAzure chaque fois que vous ouvrez votre projet.</span><span class="sxs-lookup"><span data-stu-id="14bc7-128">After you have completed this process, Eclipse uses hello credentials file tooautomatically sign you in tooAzure each time you open your project.</span></span>

1. <span data-ttu-id="14bc7-129">Ouvrez votre projet avec IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="14bc7-129">Open your project with IntelliJ IDEA.</span></span>

2. <span data-ttu-id="14bc7-130">Sur hello **outils** menu, pointez trop**Azure**, puis cliquez sur **Azure Sign In**.</span><span class="sxs-lookup"><span data-stu-id="14bc7-130">On hello **Tools** menu, point too**Azure**, and then click **Azure Sign In**.</span></span>

   ![Hello IntelliJ Azure signe de commandes][A01]

3. <span data-ttu-id="14bc7-132">Bonjour **Azure Sign In** fenêtre, sélectionnez **automatisée**, puis cliquez sur **nouveau**.</span><span class="sxs-lookup"><span data-stu-id="14bc7-132">In hello **Azure Sign In** window, select **Automated**, and then click **New**.</span></span>

   ![Bonjour Azure fenêtre de connexion avec automatisée sélectionnée][A02]

4. <span data-ttu-id="14bc7-134">Bonjour **boîte de dialogue de connexion Azure** fenêtre, entrez vos informations d’identification Azure, puis cliquez sur **connectez-vous**.</span><span class="sxs-lookup"><span data-stu-id="14bc7-134">In hello **Azure Login Dialog** window, enter your Azure credentials, and then click **Sign in**.</span></span>

   ![fenêtre de boîte de dialogue de connexion Azure Hello][A03]

5. <span data-ttu-id="14bc7-136">Bonjour **créer des fichiers de l’authentification** (fenêtre), les abonnements hello select que vous souhaitez toouse, choisissez votre répertoire de destination, puis cliquez sur **Démarrer**.</span><span class="sxs-lookup"><span data-stu-id="14bc7-136">In hello **Create Authentication Files** window, select hello subscriptions that you want toouse, choose your destination directory, and then click **Start**.</span></span>

   ![fenêtre Créer les fichiers d’authentification de Hello][A04]

6. <span data-ttu-id="14bc7-138">Bonjour **état de la création de Principal du Service** boîte de dialogue, une fois que vos fichiers ont été créées avec succès, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="14bc7-138">In hello **Service Principal Creation Status** dialog box, after your files have been created successfully, click **OK**.</span></span>

   ![Hello, boîte de dialogue État de la création de Principal du Service][A05]

7. <span data-ttu-id="14bc7-140">Bonjour **Azure Sign In** fenêtre, cliquez sur **connectez-vous**.</span><span class="sxs-lookup"><span data-stu-id="14bc7-140">In hello **Azure Sign In** window, click **Sign in**.</span></span>

   ![Boîte de dialogue Connexion à Azure][A06]

8. <span data-ttu-id="14bc7-142">Bonjour **sélectionnez les abonnements** boîte de dialogue, les abonnements hello select que vous souhaitez toouse, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="14bc7-142">In hello **Select Subscriptions** dialog box, select hello subscriptions that you want toouse, and then click **OK**.</span></span>

   ![boîte de dialogue Sélectionnez les abonnements Hello][A07]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-automatically"></a><span data-ttu-id="14bc7-144">Déconnexion de votre compte Azure après vous être connecté automatiquement</span><span class="sxs-lookup"><span data-stu-id="14bc7-144">Sign out of your Azure account after you have signed in automatically</span></span>

<span data-ttu-id="14bc7-145">Après avoir configuré votre compte à l’aide des étapes précédentes de hello, hello boîte à outils Azure vous connecte automatiquement tooyour compte Azure, chaque fois que vous redémarrez IntelliJ idée.</span><span class="sxs-lookup"><span data-stu-id="14bc7-145">After you have configured your account by using hello preceding steps, hello Azure Toolkit automatically signs you in tooyour Azure account each time you restart IntelliJ IDEA.</span></span> <span data-ttu-id="14bc7-146">Toutefois, toosign hors de votre compte Azure et empêcher hello boîte à outils Azure à partir de la connexion automatique, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="14bc7-146">However, toosign out of your Azure account and prevent hello Azure Toolkit from signing you in automatically, do hello following:</span></span>

1. <span data-ttu-id="14bc7-147">Dans l’idée IntelliJ, hello **outils** menu, pointez trop**Azure**, puis cliquez sur **Azure se déconnecter**.</span><span class="sxs-lookup"><span data-stu-id="14bc7-147">In IntelliJ IDEA, on hello **Tools** menu, point too**Azure**, and then click **Azure Sign Out**.</span></span>

   ![Hello commande IntelliJ Azure se déconnecter][L01]

2. <span data-ttu-id="14bc7-149">Bonjour **Azure se déconnecter** fenêtre de confirmation, cliquez sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="14bc7-149">In hello **Azure Sign Out** confirmation window, click **Yes**.</span></span>

   ![fenêtre Hello Azure se déconnecter confirmation][L03]

## <a name="sign-in-tooyour-azure-account-automatically-by-using-an-existing-credentials-file"></a><span data-ttu-id="14bc7-151">Connectez-vous tooyour compte Azure automatiquement à l’aide d’un fichier d’informations d’identification existant</span><span class="sxs-lookup"><span data-stu-id="14bc7-151">Sign in tooyour Azure account automatically by using an existing credentials file</span></span>

<span data-ttu-id="14bc7-152">Si vous vous déconnecter de votre compte Azure lorsque vous utilisez IntelliJ idée, vous devez utiliser un signe de tooautomatically du fichier d’informations d’identification existantes dans toohello compte.</span><span class="sxs-lookup"><span data-stu-id="14bc7-152">If you sign out of your Azure account when you are using IntelliJ IDEA, you must use an existing credentials file tooautomatically sign back in toohello account.</span></span> <span data-ttu-id="14bc7-153">tooconfigure hello boîte à outils Azure pour Eclipse toouse un fichier d’informations d’identification existant, procédez comme hello suivant :</span><span class="sxs-lookup"><span data-stu-id="14bc7-153">tooconfigure hello Azure Toolkit for Eclipse toouse an existing credentials file, do hello following:</span></span>

1. <span data-ttu-id="14bc7-154">Ouvrez votre projet avec IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="14bc7-154">Open your project with IntelliJ IDEA.</span></span>

2. <span data-ttu-id="14bc7-155">Sur hello **outils** menu, pointez trop**Azure**, puis cliquez sur **Azure Sign In**.</span><span class="sxs-lookup"><span data-stu-id="14bc7-155">On hello **Tools** menu, point too**Azure**, and then click **Azure Sign In**.</span></span>

   ![Hello IntelliJ Azure signe de commandes][A01]

3. <span data-ttu-id="14bc7-157">Bonjour **Azure Sign In** fenêtre, sélectionnez **automatisée**, puis cliquez sur **Parcourir**.</span><span class="sxs-lookup"><span data-stu-id="14bc7-157">In hello **Azure Sign In** window, select **Automated**, and then click **Browse**.</span></span>

   ![Bonjour Azure fenêtre de connexion avec automatisée sélectionnée][A02]

4. <span data-ttu-id="14bc7-159">Bonjour **sélectionner le fichier d’authentification** boîte de dialogue, sélectionnez un fichier d’informations d’identification créé précédemment, puis cliquez sur **sélectionnez**.</span><span class="sxs-lookup"><span data-stu-id="14bc7-159">In hello **Select Authentication File** dialog box, select a previously created credentials file, and then click **Select**.</span></span>

   ![boîte de dialogue Sélectionner le fichier d’authentification Hello][A08]

5. <span data-ttu-id="14bc7-161">Bonjour **Azure Sign In** fenêtre, cliquez sur **connectez-vous**.</span><span class="sxs-lookup"><span data-stu-id="14bc7-161">In hello **Azure Sign In** window, click **Sign in**.</span></span>

   ![Bonjour Azure fenêtre de connexion avec automatisée sélectionnée][A06]

6. <span data-ttu-id="14bc7-163">Bonjour **sélectionnez les abonnements** boîte de dialogue, les abonnements hello select que vous souhaitez toouse, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="14bc7-163">In hello **Select Subscriptions** dialog box, select hello subscriptions that you want toouse, and then click **OK**.</span></span>

   ![boîte de dialogue Sélectionnez les abonnements Hello][A07]

## <a name="next-steps"></a><span data-ttu-id="14bc7-165">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="14bc7-165">Next steps</span></span>
<span data-ttu-id="14bc7-166">Pour plus d’informations sur hello boîtes à outils Azure pour Java IDE, consultez hello suivant liens :</span><span class="sxs-lookup"><span data-stu-id="14bc7-166">For more information about hello Azure Toolkits for Java IDEs, see hello following links:</span></span>

* <span data-ttu-id="14bc7-167">[boîte à outils Azure pour Eclipse]</span><span class="sxs-lookup"><span data-stu-id="14bc7-167">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="14bc7-168">[Nouveautés de hello boîte à outils Azure pour Eclipse]</span><span class="sxs-lookup"><span data-stu-id="14bc7-168">[What's new in hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="14bc7-169">[Lors de l’installation hello boîte à outils Azure pour Eclipse]</span><span class="sxs-lookup"><span data-stu-id="14bc7-169">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="14bc7-170">[Instructions de connexion pour hello boîte à outils Azure pour Eclipse]</span><span class="sxs-lookup"><span data-stu-id="14bc7-170">[Sign-in instructions for hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="14bc7-171">[Créer une application web Hello World pour Azure dans Eclipse]</span><span class="sxs-lookup"><span data-stu-id="14bc7-171">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="14bc7-172">[Kit de ressources Azure pour IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="14bc7-172">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="14bc7-173">[Quelles sont les nouveautés Bonjour Azure Toolkit pour IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="14bc7-173">[What's new in hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="14bc7-174">[Lors de l’installation Bonjour Azure Toolkit pour IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="14bc7-174">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="14bc7-175">*Instructions d’authentification pour hello boîte à outils Azure pour IntelliJ* (cet article)</span><span class="sxs-lookup"><span data-stu-id="14bc7-175">*Sign-in instructions for hello Azure Toolkit for IntelliJ* (this article)</span></span>
  * <span data-ttu-id="14bc7-176">[Créer une application web Hello World pour Azure dans IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="14bc7-176">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="14bc7-177">Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez hello [centre de développement Java Azure] et hello [outils Java pour Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="14bc7-177">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

[boîte à outils Azure pour Eclipse]: ./azure-toolkit-for-eclipse.md
[Kit de ressources Azure pour IntelliJ]: ./azure-toolkit-for-intellij.md
[Créer une application web Hello World pour Azure dans Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Créer une application web Hello World pour Azure dans IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Lors de l’installation hello boîte à outils Azure pour Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[Lors de l’installation Bonjour Azure Toolkit pour IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[Instructions de connexion pour hello boîte à outils Azure pour Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Sign-in instructions for hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Nouveautés de hello boîte à outils Azure pour Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[Quelles sont les nouveautés Bonjour Azure Toolkit pour IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[centre de développement Java Azure]: https://azure.microsoft.com/develop/java/
[outils Java pour Visual Studio Team Services]: https://java.visualstudio.com/

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
