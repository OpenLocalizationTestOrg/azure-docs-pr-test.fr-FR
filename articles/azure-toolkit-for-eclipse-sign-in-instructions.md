---
title: "aaaSign dans des Instructions pour hello boîte à outils Azure pour Eclipse | Documents Microsoft"
description: "Découvrez comment toosign dans Microsoft Azure à l’aide de hello boîte à outils Azure pour Eclipse."
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
ms.openlocfilehash: 95be64750ca0147f76dae8f364fad80cb9ccc969
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sign-in-instructions-for-hello-azure-toolkit-for-eclipse"></a><span data-ttu-id="3f92b-103">Connexion Azure dans des Instructions pour hello boîte à outils Azure pour Eclipse</span><span class="sxs-lookup"><span data-stu-id="3f92b-103">Azure Sign In Instructions for hello Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="3f92b-104">Hello boîte à outils Azure pour Eclipse fournit deux méthodes pour la connexion à votre compte Azure :</span><span class="sxs-lookup"><span data-stu-id="3f92b-104">hello Azure Toolkit for Eclipse provides two methods for signing into your Azure account:</span></span>

  * <span data-ttu-id="3f92b-105">**Interactive** : si vous utilisez cette méthode, vous devez entrer vos informations d’identification Azure à chaque fois que vous vous connectez à votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="3f92b-105">**Interactive** - when you are using this method, you will enter your Azure credentials each time you sign into your Azure account.</span></span>
  * <span data-ttu-id="3f92b-106">**Automatisée** - lorsque vous utilisez cette méthode, vous allez créer un fichier d’informations d’identification qui contient vos données de principal du service, après laquelle vous pouvez utiliser le signe de tooautomatically fichier hello informations d’identification à votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="3f92b-106">**Automated** - when you are using this method, you will create a credentials file which contains your service principal data, after which you can use hello credentials file tooautomatically sign into your Azure account.</span></span>

<span data-ttu-id="3f92b-107">Hello étapes Bonjour les sections suivantes décrivent comment toouse chaque méthode.</span><span class="sxs-lookup"><span data-stu-id="3f92b-107">hello steps in hello following sections will describe how toouse each method.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="signing-into-your-azure-account-interactively"></a><span data-ttu-id="3f92b-108">Connexion interactive à votre compte Azure</span><span class="sxs-lookup"><span data-stu-id="3f92b-108">Signing into your Azure account interactively</span></span>

<span data-ttu-id="3f92b-109">Hello suit illustre comment toosign dans Azure en entrant manuellement vos informations d’identification Azure.</span><span class="sxs-lookup"><span data-stu-id="3f92b-109">hello following steps will illustrate how toosign into Azure by manually entering your Azure credentials.</span></span>

1. <span data-ttu-id="3f92b-110">Ouvrez votre projet avec Eclipse.</span><span class="sxs-lookup"><span data-stu-id="3f92b-110">Open your project with Eclipse.</span></span>

1. <span data-ttu-id="3f92b-111">Cliquez successivement sur **Outils**, **Azure** et **Se connecter**.</span><span class="sxs-lookup"><span data-stu-id="3f92b-111">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>

   ![Menu d’Eclipse pour la connexion à Azure][I01]

1. <span data-ttu-id="3f92b-113">Hello lorsque **Azure Sign In** boîte de dialogue s’affiche, sélectionnez **Interactive**, puis cliquez sur **connexion**.</span><span class="sxs-lookup"><span data-stu-id="3f92b-113">When hello **Azure Sign In** dialog box appears, select **Interactive**, and then click **Sign In**.</span></span>

   ![Boîte de dialogue Se connecter][I02]

1. <span data-ttu-id="3f92b-115">Hello lorsque **Azure journal dans** boîte de dialogue s’affiche, entrez vos informations d’identification Azure, puis cliquez sur **connexion**.</span><span class="sxs-lookup"><span data-stu-id="3f92b-115">When hello **Azure Log In** dialog box appears, enter your Azure credentials, and then click **Sign In**.</span></span>

   ![Boîte de dialogue Connexion à Azure][I03]

1. <span data-ttu-id="3f92b-117">Hello lorsque **sélectionnez les abonnements** boîte de dialogue s’affiche, abonnements hello select que vous souhaitez toouse, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="3f92b-117">When hello **Select Subscriptions** dialog box appears, select hello subscriptions that you want toouse, and then click **OK**.</span></span>

   ![Boîte de dialogue Sélectionner des abonnements][I04]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-interactively"></a><span data-ttu-id="3f92b-119">Déconnexion de votre compte Azure lorsque vous vous êtes connecté de manière interactive</span><span class="sxs-lookup"><span data-stu-id="3f92b-119">Signing out of your Azure account when you signed in interactively</span></span>

<span data-ttu-id="3f92b-120">Après avoir configuré les étapes hello dans la section précédente de hello, sera automatiquement déconnecté de votre compte Azure, chaque fois que vous redémarrez Eclipse.</span><span class="sxs-lookup"><span data-stu-id="3f92b-120">After you have configured hello steps in hello previous section, you will automatically signed out of your Azure account each time you restart Eclipse.</span></span> <span data-ttu-id="3f92b-121">Toutefois, si vous souhaitez toosign hors de votre compte Azure sans avoir à redémarrer Eclipse, utilisez hello comme suit.</span><span class="sxs-lookup"><span data-stu-id="3f92b-121">However, if you want toosign out of your Azure account without restarting Eclipse, use hello following steps.</span></span>

1. <span data-ttu-id="3f92b-122">Dans Eclipse, cliquez successivement sur **Outils**, **Azure** et **Se déconnecter**.</span><span class="sxs-lookup"><span data-stu-id="3f92b-122">In Eclipse, click **Tools**, then click **Azure**, and then click **Sign Out**.</span></span>

   ![Menu d’Eclipse pour la déconnexion d’Azure][L01]

1. <span data-ttu-id="3f92b-124">Hello lorsque **Azure se déconnecter** boîte de dialogue s’affiche, cliquez sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="3f92b-124">When hello **Azure Sign Out** dialog box appears, click **Yes**.</span></span>

   ![Boîte de dialogue Se déconnecter][L02]

## <a name="signing-into-your-azure-account-automatically-and-creating-a-credentials-file-toouse-in-hello-future"></a><span data-ttu-id="3f92b-126">Connecter automatiquement à votre compte Azure et la création d’un informations d’identification de fichier toouse Bonjour future</span><span class="sxs-lookup"><span data-stu-id="3f92b-126">Signing into your Azure account automatically and creating a credentials file toouse in hello future</span></span>

<span data-ttu-id="3f92b-127">Hello étapes suivantes vous guidera dans la création d’un fichier d’informations d’identification qui contient vos données de principal du service.</span><span class="sxs-lookup"><span data-stu-id="3f92b-127">hello following steps will walk you through creating a credentials file which contains your service principal data.</span></span> <span data-ttu-id="3f92b-128">Une fois que vous avez terminé ces étapes, la volonté d’Eclipse automatiquement utilisez hello informations d’identification de fichier tooautomatically signe que vous dans Azure chaque fois que vous ouvrez votre projet.</span><span class="sxs-lookup"><span data-stu-id="3f92b-128">Once you have completed these steps, Eclipse will automatically use hello credentials file tooautomatically sign you into Azure each time you open your project.</span></span>

1. <span data-ttu-id="3f92b-129">Ouvrez votre projet avec Eclipse.</span><span class="sxs-lookup"><span data-stu-id="3f92b-129">Open your project with Eclipse.</span></span>

1. <span data-ttu-id="3f92b-130">Cliquez successivement sur **Outils**, **Azure** et **Se connecter**.</span><span class="sxs-lookup"><span data-stu-id="3f92b-130">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>

   ![Menu d’Eclipse pour la connexion à Azure][A01]

1. <span data-ttu-id="3f92b-132">Hello lorsque **Azure Sign In** boîte de dialogue s’affiche, sélectionnez **automatisée**, puis cliquez sur **nouveau**.</span><span class="sxs-lookup"><span data-stu-id="3f92b-132">When hello **Azure Sign In** dialog box appears, select **Automated**, and then click **New**.</span></span>

   ![Boîte de dialogue Se connecter][A02]

1. <span data-ttu-id="3f92b-134">Hello lorsque **Azure journal dans** boîte de dialogue s’affiche, entrez vos informations d’identification Azure, puis cliquez sur **connexion**.</span><span class="sxs-lookup"><span data-stu-id="3f92b-134">When hello **Azure Log In** dialog box appears, enter your Azure credentials, and then click **Sign In**.</span></span>

   ![Boîte de dialogue Connexion à Azure][A03]

1. <span data-ttu-id="3f92b-136">Hello lorsque **créer les fichiers d’authentification** boîte de dialogue s’affiche, abonnements hello select que vous souhaitez toouse, choisissez votre répertoire de destination, puis cliquez sur **Démarrer**.</span><span class="sxs-lookup"><span data-stu-id="3f92b-136">When hello **Create authentication files** dialog box appears, select hello subscriptions that you want toouse, choose your destination directory, and then click **Start**.</span></span>

   ![Boîte de dialogue Connexion à Azure][A04]

1. <span data-ttu-id="3f92b-138">Hello **état de création d’un système Principal du Service** boîte de dialogue s’affiche et une fois que vos fichiers ont été créées avec succès, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="3f92b-138">hello **Service Principal Creatation Status** dialog box will be displayed, and after your files have been created successfully, click **OK**.</span></span>

   ![Boîte de dialogue Service Principal Creation Status (État de création du principal de service)][A05]

1. <span data-ttu-id="3f92b-140">Hello lorsque **Azure Sign In** boîte de dialogue s’affiche, cliquez sur **connexion**.</span><span class="sxs-lookup"><span data-stu-id="3f92b-140">When hello **Azure Sign In** dialog box appears, click **Sign In**.</span></span>

   ![Boîte de dialogue Connexion à Azure][A06]

1. <span data-ttu-id="3f92b-142">Hello lorsque **sélectionnez les abonnements** boîte de dialogue s’affiche, abonnements hello select que vous souhaitez toouse, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="3f92b-142">When hello **Select Subscriptions** dialog box appears, select hello subscriptions that you want toouse, and then click **OK**.</span></span>

   ![Boîte de dialogue Sélectionner des abonnements][A07]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-automatically"></a><span data-ttu-id="3f92b-144">Déconnexion de votre compte Azure lorsque vous vous êtes connecté automatiquement</span><span class="sxs-lookup"><span data-stu-id="3f92b-144">Signing out of your Azure account when you signed in automatically</span></span>

<span data-ttu-id="3f92b-145">Après avoir configuré les étapes hello dans la section précédente de hello, hello boîte à outils Azure sera automatiquement connecté à votre compte Azure, chaque fois que vous redémarrez Eclipse.</span><span class="sxs-lookup"><span data-stu-id="3f92b-145">After you have configured hello steps in hello previous section, hello Azure Toolkit will automatically sign you into your Azure account each time you restart Eclipse.</span></span> <span data-ttu-id="3f92b-146">Toutefois, toosign hors de votre compte Azure et hello boîte à outils Azure empêche de vous connecter automatiquement, utilisez les hello comme suit.</span><span class="sxs-lookup"><span data-stu-id="3f92b-146">However, toosign out of your Azure account and prevent hello Azure Toolkit from signing you in automatically, use hello following steps.</span></span>

1. <span data-ttu-id="3f92b-147">Dans Eclipse, cliquez successivement sur **Outils**, **Azure** et **Se déconnecter**.</span><span class="sxs-lookup"><span data-stu-id="3f92b-147">In Eclipse, click **Tools**, then click **Azure**, and then click **Sign Out**.</span></span>

   ![Menu d’Eclipse pour la déconnexion d’Azure][L01]

1. <span data-ttu-id="3f92b-149">Hello lorsque **Azure se déconnecter** boîte de dialogue s’affiche, cliquez sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="3f92b-149">When hello **Azure Sign Out** dialog box appears, click **Yes**.</span></span>

   ![Boîte de dialogue Se déconnecter][L03]

## <a name="signing-into-your-azure-account-automatically-using-a-credentials-file-which-you-have-already-created"></a><span data-ttu-id="3f92b-151">Connexion automatique à votre compte Azure et utilisation d’un fichier d’informations d’identification que vous avez déjà créé</span><span class="sxs-lookup"><span data-stu-id="3f92b-151">Signing into your Azure account automatically using a credentials file which you have already created</span></span>

<span data-ttu-id="3f92b-152">Si vous vous connectez en dehors d’Azure lorsque vous utilisez Eclipse, vous devez tooreconfigure hello boîte à outils Azure pour Eclipse toouse un fichier d’informations d’identification qui ont créé avant de vous connecter automatiquement à votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="3f92b-152">If you sign out of Azure when you are using Eclipse, you will need tooreconfigure hello Azure Toolkit for Eclipse toouse a credentials file which have created before you can automatically sign into your Azure acccount.</span></span> <span data-ttu-id="3f92b-153">Hello étapes suivantes vous guidera dans la configuration toouse de boîte à outils Azure hello un fichier d’informations d’identification existant.</span><span class="sxs-lookup"><span data-stu-id="3f92b-153">hello following steps will walk you through configuring hello Azure Toolkit toouse an existing credentials file.</span></span>

1. <span data-ttu-id="3f92b-154">Ouvrez votre projet avec Eclipse.</span><span class="sxs-lookup"><span data-stu-id="3f92b-154">Open your project with Eclipse.</span></span>

1. <span data-ttu-id="3f92b-155">Cliquez successivement sur **Outils**, **Azure** et **Se connecter**.</span><span class="sxs-lookup"><span data-stu-id="3f92b-155">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>

   ![Menu d’Eclipse pour la connexion à Azure][A01]

1. <span data-ttu-id="3f92b-157">Hello lorsque **Azure Sign In** boîte de dialogue s’affiche, sélectionnez **automatisée**, puis cliquez sur **Parcourir**.</span><span class="sxs-lookup"><span data-stu-id="3f92b-157">When hello **Azure Sign In** dialog box appears, select **Automated**, and then click **Browse**.</span></span>

   ![Boîte de dialogue Se connecter][A02]

1. <span data-ttu-id="3f92b-159">Hello lorsque **sélectionner le fichier authentifié** boîte de dialogue s’affiche, sélectionnez un fichier d’informations d’identification que vous avez créé précédemment, puis cliquez sur **sélectionnez**.</span><span class="sxs-lookup"><span data-stu-id="3f92b-159">When hello **Select Authenticated File** dialog box appears, select a credentials file which you created earlier, and then click **Select**.</span></span>

   ![Boîte de dialogue Se connecter][A08]

1. <span data-ttu-id="3f92b-161">Hello lorsque **Azure Sign In** boîte de dialogue s’affiche, cliquez sur **connexion**.</span><span class="sxs-lookup"><span data-stu-id="3f92b-161">When hello **Azure Sign In** dialog box appears, click **Sign In**.</span></span>

   ![Boîte de dialogue Connexion à Azure][A06]

1. <span data-ttu-id="3f92b-163">Hello lorsque **sélectionnez les abonnements** boîte de dialogue s’affiche, abonnements hello select que vous souhaitez toouse, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="3f92b-163">When hello **Select Subscriptions** dialog box appears, select hello subscriptions that you want toouse, and then click **OK**.</span></span>

   ![Boîte de dialogue Sélectionner des abonnements][A07]

## <a name="see-also"></a><span data-ttu-id="3f92b-165">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="3f92b-165">See Also</span></span>
<span data-ttu-id="3f92b-166">Pour plus d’informations sur hello boîtes à outils Azure pour Java IDE, consultez hello suivant liens :</span><span class="sxs-lookup"><span data-stu-id="3f92b-166">For more information about hello Azure Toolkits for Java IDEs, see hello following links:</span></span>

* <span data-ttu-id="3f92b-167">[boîte à outils Azure pour Eclipse]</span><span class="sxs-lookup"><span data-stu-id="3f92b-167">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="3f92b-168">[Nouveautés dans hello boîte à outils Azure pour Eclipse]</span><span class="sxs-lookup"><span data-stu-id="3f92b-168">[What's New in hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="3f92b-169">[Lors de l’installation hello boîte à outils Azure pour Eclipse]</span><span class="sxs-lookup"><span data-stu-id="3f92b-169">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="3f92b-170">*Authentification dans des Instructions pour hello boîte à outils Azure pour Eclipse (Cet Article)*</span><span class="sxs-lookup"><span data-stu-id="3f92b-170">*Sign In Instructions for hello Azure Toolkit for Eclipse (This Article)*</span></span>
  * <span data-ttu-id="3f92b-171">[Créer une application web « Hello World » pour Azure dans Eclipse]</span><span class="sxs-lookup"><span data-stu-id="3f92b-171">[Create a Hello World Web App for Azure in Eclipse]</span></span>
* <span data-ttu-id="3f92b-172">[Kit de ressources Azure pour IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="3f92b-172">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="3f92b-173">[Nouveautés dans hello Azure Toolkit pour IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="3f92b-173">[What's New in hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="3f92b-174">[Lors de l’installation Bonjour Azure Toolkit pour IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="3f92b-174">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="3f92b-175">[Authentification dans des Instructions pour hello Azure Toolkit pour IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="3f92b-175">[Sign In Instructions for hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="3f92b-176">[Créer une application web « Hello World » pour Azure dans IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="3f92b-176">[Create a Hello World Web App for Azure in IntelliJ]</span></span>

<span data-ttu-id="3f92b-177">Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez hello [centre de développement Java Azure] et hello [outils Java pour Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="3f92b-177">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

[boîte à outils Azure pour Eclipse]: ./azure-toolkit-for-eclipse.md
[Kit de ressources Azure pour IntelliJ]: ./azure-toolkit-for-intellij.md
[Créer une application web « Hello World » pour Azure dans Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Créer une application web « Hello World » pour Azure dans IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Lors de l’installation hello boîte à outils Azure pour Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[Lors de l’installation Bonjour Azure Toolkit pour IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[Sign In Instructions for hello Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Authentification dans des Instructions pour hello Azure Toolkit pour IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Nouveautés dans hello boîte à outils Azure pour Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[Nouveautés dans hello Azure Toolkit pour IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[centre de développement Java Azure]: https://azure.microsoft.com/develop/java/
[outils Java pour Visual Studio Team Services]: https://java.visualstudio.com/

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
