---
title: "Instructions de connexion à Azure pour le kit de ressources Azure pour Eclipse | Microsoft Docs"
description: "Découvrez comment vous connecter à Microsoft Azure à l’aide du kit de ressources Azure pour Eclipse."
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
ms.openlocfilehash: 02dd9935086c4c40d9ed54cc9ff2412ca96889f5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-sign-in-instructions-for-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="f9c1a-103">Instructions de connexion à Azure pour le kit de ressources Azure pour Eclipse</span><span class="sxs-lookup"><span data-stu-id="f9c1a-103">Azure Sign In Instructions for the Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="f9c1a-104">Le kit de ressources Azure pour Eclipse propose deux méthodes pour vous connecter à votre compte Azure :</span><span class="sxs-lookup"><span data-stu-id="f9c1a-104">The Azure Toolkit for Eclipse provides two methods for signing into your Azure account:</span></span>

  * <span data-ttu-id="f9c1a-105">**Interactive** : si vous utilisez cette méthode, vous devez entrer vos informations d’identification Azure à chaque fois que vous vous connectez à votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="f9c1a-105">**Interactive** - when you are using this method, you will enter your Azure credentials each time you sign into your Azure account.</span></span>
  * <span data-ttu-id="f9c1a-106">**Automatisée** : si vous utilisez cette méthode, vous devez créer un fichier d’informations d’identification qui contiendra vos données de principal de service, après quoi vous pourrez utiliser le fichier d’informations d’identification pour vous connecter automatiquement à votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="f9c1a-106">**Automated** - when you are using this method, you will create a credentials file which contains your service principal data, after which you can use the credentials file to automatically sign into your Azure account.</span></span>

<span data-ttu-id="f9c1a-107">Les étapes décrites dans les sections suivantes décrivent l’utilisation de chaque méthode.</span><span class="sxs-lookup"><span data-stu-id="f9c1a-107">The steps in the following sections will describe how to use each method.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="signing-into-your-azure-account-interactively"></a><span data-ttu-id="f9c1a-108">Connexion interactive à votre compte Azure</span><span class="sxs-lookup"><span data-stu-id="f9c1a-108">Signing into your Azure account interactively</span></span>

<span data-ttu-id="f9c1a-109">La procédure suivante indique comment vous connecter à Azure en entrant manuellement vos informations d’identification Azure.</span><span class="sxs-lookup"><span data-stu-id="f9c1a-109">The following steps will illustrate how to sign into Azure by manually entering your Azure credentials.</span></span>

1. <span data-ttu-id="f9c1a-110">Ouvrez votre projet avec Eclipse.</span><span class="sxs-lookup"><span data-stu-id="f9c1a-110">Open your project with Eclipse.</span></span>

1. <span data-ttu-id="f9c1a-111">Cliquez successivement sur **Outils**, **Azure** et **Se connecter**.</span><span class="sxs-lookup"><span data-stu-id="f9c1a-111">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>

   ![Menu d’Eclipse pour la connexion à Azure][I01]

1. <span data-ttu-id="f9c1a-113">Lorsque la boîte de dialogue **Connexion à Azure** s’affiche, sélectionnez **Interactive**, puis cliquez sur **Se connecter**.</span><span class="sxs-lookup"><span data-stu-id="f9c1a-113">When the **Azure Sign In** dialog box appears, select **Interactive**, and then click **Sign In**.</span></span>

   ![Boîte de dialogue Se connecter][I02]

1. <span data-ttu-id="f9c1a-115">Lorsque la boîte de dialogue **Connexion à Azure** s’affiche, entrez vos informations d’identification Azure, puis cliquez sur **Se connecter**.</span><span class="sxs-lookup"><span data-stu-id="f9c1a-115">When the **Azure Log In** dialog box appears, enter your Azure credentials, and then click **Sign In**.</span></span>

   ![Boîte de dialogue Connexion à Azure][I03]

1. <span data-ttu-id="f9c1a-117">Lorsque la boîte de dialogue **Sélectionner des abonnements** s’affiche, sélectionnez les abonnements que vous souhaitez utiliser, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="f9c1a-117">When the **Select Subscriptions** dialog box appears, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![Boîte de dialogue Sélectionner des abonnements][I04]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-interactively"></a><span data-ttu-id="f9c1a-119">Déconnexion de votre compte Azure lorsque vous vous êtes connecté de manière interactive</span><span class="sxs-lookup"><span data-stu-id="f9c1a-119">Signing out of your Azure account when you signed in interactively</span></span>

<span data-ttu-id="f9c1a-120">Après avoir configuré les étapes indiquées dans la section précédente, vous êtes déconnecté automatiquement de votre compte Azure à chaque redémarrage d’Eclipse.</span><span class="sxs-lookup"><span data-stu-id="f9c1a-120">After you have configured the steps in the previous section, you will automatically signed out of your Azure account each time you restart Eclipse.</span></span> <span data-ttu-id="f9c1a-121">Toutefois, si vous souhaitez vous déconnecter de votre compte Azure sans redémarrer Eclipse, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="f9c1a-121">However, if you want to sign out of your Azure account without restarting Eclipse, use the following steps.</span></span>

1. <span data-ttu-id="f9c1a-122">Dans Eclipse, cliquez successivement sur **Outils**, **Azure** et **Se déconnecter**.</span><span class="sxs-lookup"><span data-stu-id="f9c1a-122">In Eclipse, click **Tools**, then click **Azure**, and then click **Sign Out**.</span></span>

   ![Menu d’Eclipse pour la déconnexion d’Azure][L01]

1. <span data-ttu-id="f9c1a-124">Lorsque la boîte de dialogue **Déconnexion d’Azure** s’affiche, cliquez sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="f9c1a-124">When the **Azure Sign Out** dialog box appears, click **Yes**.</span></span>

   ![Boîte de dialogue Se déconnecter][L02]

## <a name="signing-into-your-azure-account-automatically-and-creating-a-credentials-file-to-use-in-the-future"></a><span data-ttu-id="f9c1a-126">Connexion automatique à votre compte Azure et création d’un fichier d’informations d’identification à utiliser à l’avenir</span><span class="sxs-lookup"><span data-stu-id="f9c1a-126">Signing into your Azure account automatically and creating a credentials file to use in the future</span></span>

<span data-ttu-id="f9c1a-127">La procédure suivante vous guide dans la création d’un fichier d’informations d’identification qui contient vos données de principal de service.</span><span class="sxs-lookup"><span data-stu-id="f9c1a-127">The following steps will walk you through creating a credentials file which contains your service principal data.</span></span> <span data-ttu-id="f9c1a-128">Une fois que vous avez effectué ces étapes, Eclipse utilise automatiquement le fichier d’informations d’identification pour vous connecter automatiquement à Azure à chaque fois que vous ouvrez votre projet.</span><span class="sxs-lookup"><span data-stu-id="f9c1a-128">Once you have completed these steps, Eclipse will automatically use the credentials file to automatically sign you into Azure each time you open your project.</span></span>

1. <span data-ttu-id="f9c1a-129">Ouvrez votre projet avec Eclipse.</span><span class="sxs-lookup"><span data-stu-id="f9c1a-129">Open your project with Eclipse.</span></span>

1. <span data-ttu-id="f9c1a-130">Cliquez successivement sur **Outils**, **Azure** et **Se connecter**.</span><span class="sxs-lookup"><span data-stu-id="f9c1a-130">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>

   ![Menu d’Eclipse pour la connexion à Azure][A01]

1. <span data-ttu-id="f9c1a-132">Lorsque la boîte de dialogue **Connexion à Azure** s’affiche, sélectionnez **Automatisée**, puis cliquez sur **Nouveau**.</span><span class="sxs-lookup"><span data-stu-id="f9c1a-132">When the **Azure Sign In** dialog box appears, select **Automated**, and then click **New**.</span></span>

   ![Boîte de dialogue Se connecter][A02]

1. <span data-ttu-id="f9c1a-134">Lorsque la boîte de dialogue **Connexion à Azure** s’affiche, entrez vos informations d’identification Azure, puis cliquez sur **Se connecter**.</span><span class="sxs-lookup"><span data-stu-id="f9c1a-134">When the **Azure Log In** dialog box appears, enter your Azure credentials, and then click **Sign In**.</span></span>

   ![Boîte de dialogue Connexion à Azure][A03]

1. <span data-ttu-id="f9c1a-136">Lorsque la boîte de dialogue **Create authentication files (Créer des fichiers d’authentification)** s’affiche, sélectionnez les abonnements que vous souhaitez utiliser, choisissez votre répertoire de destination, puis cliquez sur **Démarrer**.</span><span class="sxs-lookup"><span data-stu-id="f9c1a-136">When the **Create authentication files** dialog box appears, select the subscriptions that you want to use, choose your destination directory, and then click **Start**.</span></span>

   ![Boîte de dialogue Connexion à Azure][A04]

1. <span data-ttu-id="f9c1a-138">La boîte de dialogue **Service Principal Creation Status (État de création du principal de service)** s’affiche, et une fois que vos fichiers ont été créés, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="f9c1a-138">The **Service Principal Creatation Status** dialog box will be displayed, and after your files have been created successfully, click **OK**.</span></span>

   ![Boîte de dialogue Service Principal Creation Status (État de création du principal de service)][A05]

1. <span data-ttu-id="f9c1a-140">Lorsque la boîte de dialogue **Connexion à Azure** s’affiche, cliquez sur **Se connecter**.</span><span class="sxs-lookup"><span data-stu-id="f9c1a-140">When the **Azure Sign In** dialog box appears, click **Sign In**.</span></span>

   ![Boîte de dialogue Connexion à Azure][A06]

1. <span data-ttu-id="f9c1a-142">Lorsque la boîte de dialogue **Sélectionner des abonnements** s’affiche, sélectionnez les abonnements que vous souhaitez utiliser, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="f9c1a-142">When the **Select Subscriptions** dialog box appears, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![Boîte de dialogue Sélectionner des abonnements][A07]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-automatically"></a><span data-ttu-id="f9c1a-144">Déconnexion de votre compte Azure lorsque vous vous êtes connecté automatiquement</span><span class="sxs-lookup"><span data-stu-id="f9c1a-144">Signing out of your Azure account when you signed in automatically</span></span>

<span data-ttu-id="f9c1a-145">Après avoir configuré les étapes indiquées dans la section précédente, le kit de ressources Azure vous connecte automatiquement à votre compte Azure à chaque redémarrage d’Eclipse.</span><span class="sxs-lookup"><span data-stu-id="f9c1a-145">After you have configured the steps in the previous section, the Azure Toolkit will automatically sign you into your Azure account each time you restart Eclipse.</span></span> <span data-ttu-id="f9c1a-146">Toutefois, pour vous déconnecter de votre compte Azure et empêcher le kit de ressources Azure de vous connecter automatiquement, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="f9c1a-146">However, to sign out of your Azure account and prevent the Azure Toolkit from signing you in automatically, use the following steps.</span></span>

1. <span data-ttu-id="f9c1a-147">Dans Eclipse, cliquez successivement sur **Outils**, **Azure** et **Se déconnecter**.</span><span class="sxs-lookup"><span data-stu-id="f9c1a-147">In Eclipse, click **Tools**, then click **Azure**, and then click **Sign Out**.</span></span>

   ![Menu d’Eclipse pour la déconnexion d’Azure][L01]

1. <span data-ttu-id="f9c1a-149">Lorsque la boîte de dialogue **Déconnexion d’Azure** s’affiche, cliquez sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="f9c1a-149">When the **Azure Sign Out** dialog box appears, click **Yes**.</span></span>

   ![Boîte de dialogue Se déconnecter][L03]

## <a name="signing-into-your-azure-account-automatically-using-a-credentials-file-which-you-have-already-created"></a><span data-ttu-id="f9c1a-151">Connexion automatique à votre compte Azure et utilisation d’un fichier d’informations d’identification que vous avez déjà créé</span><span class="sxs-lookup"><span data-stu-id="f9c1a-151">Signing into your Azure account automatically using a credentials file which you have already created</span></span>

<span data-ttu-id="f9c1a-152">Si vous vous déconnectez d’Azure lorsque vous utilisez Eclipse, vous devez reconfigurer le kit de ressources Azure pour Eclipse afin d’utiliser un fichier d’informations d’identification qui a été créé pour pouvoir vous connecter automatiquement à votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="f9c1a-152">If you sign out of Azure when you are using Eclipse, you will need to reconfigure the Azure Toolkit for Eclipse to use a credentials file which have created before you can automatically sign into your Azure acccount.</span></span> <span data-ttu-id="f9c1a-153">La procédure suivante vous guide dans la configuration du kit de ressources Azure pour utiliser un fichier d’informations d’identification existant.</span><span class="sxs-lookup"><span data-stu-id="f9c1a-153">The following steps will walk you through configuring the Azure Toolkit to use an existing credentials file.</span></span>

1. <span data-ttu-id="f9c1a-154">Ouvrez votre projet avec Eclipse.</span><span class="sxs-lookup"><span data-stu-id="f9c1a-154">Open your project with Eclipse.</span></span>

1. <span data-ttu-id="f9c1a-155">Cliquez successivement sur **Outils**, **Azure** et **Se connecter**.</span><span class="sxs-lookup"><span data-stu-id="f9c1a-155">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>

   ![Menu d’Eclipse pour la connexion à Azure][A01]

1. <span data-ttu-id="f9c1a-157">Lorsque la boîte de dialogue **Connexion à Azure** s’affiche, sélectionnez **Automatisée**, puis cliquez sur **Parcourir**.</span><span class="sxs-lookup"><span data-stu-id="f9c1a-157">When the **Azure Sign In** dialog box appears, select **Automated**, and then click **Browse**.</span></span>

   ![Boîte de dialogue Se connecter][A02]

1. <span data-ttu-id="f9c1a-159">Lorsque la boîte de dialogue **Select Authenticated File (Sélectionner un fichier authentifié)** s’affiche, sélectionnez un fichier d’informations d’identification que vous avez créé précédemment, puis cliquez sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="f9c1a-159">When the **Select Authenticated File** dialog box appears, select a credentials file which you created earlier, and then click **Select**.</span></span>

   ![Boîte de dialogue Se connecter][A08]

1. <span data-ttu-id="f9c1a-161">Lorsque la boîte de dialogue **Connexion à Azure** s’affiche, cliquez sur **Se connecter**.</span><span class="sxs-lookup"><span data-stu-id="f9c1a-161">When the **Azure Sign In** dialog box appears, click **Sign In**.</span></span>

   ![Boîte de dialogue Connexion à Azure][A06]

1. <span data-ttu-id="f9c1a-163">Lorsque la boîte de dialogue **Sélectionner des abonnements** s’affiche, sélectionnez les abonnements que vous souhaitez utiliser, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="f9c1a-163">When the **Select Subscriptions** dialog box appears, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![Boîte de dialogue Sélectionner des abonnements][A07]

## <a name="see-also"></a><span data-ttu-id="f9c1a-165">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="f9c1a-165">See Also</span></span>
<span data-ttu-id="f9c1a-166">Pour plus d’informations sur les boîtes à outils Azure pour les environnements de développement Java, consultez les liens suivants :</span><span class="sxs-lookup"><span data-stu-id="f9c1a-166">For more information about the Azure Toolkits for Java IDEs, see the following links:</span></span>

* <span data-ttu-id="f9c1a-167">[Kit de ressources Azure pour Eclipse]</span><span class="sxs-lookup"><span data-stu-id="f9c1a-167">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="f9c1a-168">[Nouveautés du kit de ressources Azure pour Eclipse]</span><span class="sxs-lookup"><span data-stu-id="f9c1a-168">[What's New in the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="f9c1a-169">[Installation du kit de ressources Azure pour Eclipse]</span><span class="sxs-lookup"><span data-stu-id="f9c1a-169">[Installing the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="f9c1a-170">*Instructions de connexion à Azure pour le kit de ressources Azure pour Eclipse (cet article)*</span><span class="sxs-lookup"><span data-stu-id="f9c1a-170">*Sign In Instructions for the Azure Toolkit for Eclipse (This Article)*</span></span>
  * <span data-ttu-id="f9c1a-171">[Créer une application web « Hello World » pour Azure dans Eclipse]</span><span class="sxs-lookup"><span data-stu-id="f9c1a-171">[Create a Hello World Web App for Azure in Eclipse]</span></span>
* <span data-ttu-id="f9c1a-172">[Kit de ressources Azure pour IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="f9c1a-172">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="f9c1a-173">[Nouveautés du Kit de ressources Azure pour IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="f9c1a-173">[What's New in the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="f9c1a-174">[Installation du kit de ressources Azure pour IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="f9c1a-174">[Installing the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="f9c1a-175">[Instructions de connexion à Azure pour le kit de ressources Azure pour IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="f9c1a-175">[Sign In Instructions for the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="f9c1a-176">[Créer une application web « Hello World » pour Azure dans IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="f9c1a-176">[Create a Hello World Web App for Azure in IntelliJ]</span></span>

<span data-ttu-id="f9c1a-177">Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez le [Centre de développement Java pour Azure] et les [outils Java pour Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="f9c1a-177">For more information about using Azure with Java, see the [Azure Java Developer Center] and the [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

<span data-ttu-id="f9c1a-178">[Kit de ressources Azure pour Eclipse]: ./azure-toolkit-for-eclipse.md</span><span class="sxs-lookup"><span data-stu-id="f9c1a-178">[Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse.md</span></span>
<span data-ttu-id="f9c1a-179">[Kit de ressources Azure pour IntelliJ]: ./azure-toolkit-for-intellij.md</span><span class="sxs-lookup"><span data-stu-id="f9c1a-179">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md</span></span>
<span data-ttu-id="f9c1a-180">[Créer une application web « Hello World » pour Azure dans Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="f9c1a-180">[Create a Hello World Web App for Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span></span>
<span data-ttu-id="f9c1a-181">[Créer une application web « Hello World » pour Azure dans IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="f9c1a-181">[Create a Hello World Web App for Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span></span>
<span data-ttu-id="f9c1a-182">[Installation du kit de ressources Azure pour Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span><span class="sxs-lookup"><span data-stu-id="f9c1a-182">[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span></span>
<span data-ttu-id="f9c1a-183">[Installation du kit de ressources Azure pour IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span><span class="sxs-lookup"><span data-stu-id="f9c1a-183">[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span></span>
[Sign In Instructions for the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
<span data-ttu-id="f9c1a-184">[Instructions de connexion à Azure pour le kit de ressources Azure pour IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md (Instructions de connexion à Azure pour le kit de ressources Azure pour IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="f9c1a-184">[Sign In Instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span></span>
<span data-ttu-id="f9c1a-185">[Nouveautés du kit de ressources Azure pour Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="f9c1a-185">[What's New in the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span></span>
<span data-ttu-id="f9c1a-186">[Nouveautés du Kit de ressources Azure pour IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="f9c1a-186">[What's New in the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span></span>

<span data-ttu-id="f9c1a-187">[Centre de développement Java pour Azure]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="f9c1a-187">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
<span data-ttu-id="f9c1a-188">[outils Java pour Visual Studio Team Services]: https://java.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="f9c1a-188">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span></span>

<!-- IMG List -->

[I01]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/I01.png
[I02]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/I02.png
[I03]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/I03.png
[I04]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/I04.png

[A01]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A01.png
[A02]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A02.png
[A03]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A03.png
[A04]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A04.png
[A05]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A05.png
[A06]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A06.png
[A07]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A07.png
[A08]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A08.png

[L01]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/L01.png
[L02]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/L02.png
[L03]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/L03.png
