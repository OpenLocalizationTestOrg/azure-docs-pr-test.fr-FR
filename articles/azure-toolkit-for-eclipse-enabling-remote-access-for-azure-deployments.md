---
title: "aaaEnabling l’accès à distance pour les déploiements Azure dans Eclipse"
description: "Découvrez comment l’accès à distance de tooenable pour les déploiements Azure à l’aide de hello boîte à outils Azure pour Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: b6150006-9a7f-4d83-be18-d35ec780c7c5
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 00c2bf22c1f3ec792098f154f771c87506e87881
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-remote-access-for-azure-deployments-in-eclipse"></a><span data-ttu-id="97720-103">Activation de l’accès à distance pour les déploiements Azure dans Eclipse</span><span class="sxs-lookup"><span data-stu-id="97720-103">Enabling Remote Access for Azure Deployments in Eclipse</span></span>
<span data-ttu-id="97720-104">toohelp dépannage de vos déploiements, vous pouvez activer et utiliser l’accès à distance tooconnect toohello virtual machine hébergeant votre déploiement.</span><span class="sxs-lookup"><span data-stu-id="97720-104">toohelp troubleshoot your deployments, you may enable and use Remote Access tooconnect toohello virtual machine hosting your deployment.</span></span> <span data-ttu-id="97720-105">Hello fonctionnalité accès à distance s’appuie sur hello protocole RDP (Remote Desktop).</span><span class="sxs-lookup"><span data-stu-id="97720-105">hello Remote Access functionality relies on hello Remote Desktop Protocol (RDP).</span></span> <span data-ttu-id="97720-106">Après avoir publié tooAzure, ou si vous utilisez Eclipse avec un système d’exploitation de Windows, vous pouvez configurer l’accès à distance avant de publier tooAzure, vous pouvez configurer l’accès à distance pour votre déploiement.</span><span class="sxs-lookup"><span data-stu-id="97720-106">You can configure Remote Access for your deployment after you have published it tooAzure, or if you are using Eclipse with a Windows operating system, you can configure Remote Access before you publish tooAzure.</span></span> <span data-ttu-id="97720-107">Notez que vous avez besoin d’un client Bureau à distance qui est compatible avec votre système d’exploitation dans une machine virtuelle dans Azure, de déploiement de l’ordre tooconnect tooyour.</span><span class="sxs-lookup"><span data-stu-id="97720-107">Note that you will need a remote desktop client that is compatible with your operating system in order tooconnect tooyour deployment's virtual machine in Azure.</span></span>

## <a name="how-tooenable-remote-access-before-you-deploy-tooazure"></a><span data-ttu-id="97720-108">Comment tooenable l’accès à distance avant de déployer tooAzure</span><span class="sxs-lookup"><span data-stu-id="97720-108">How tooenable Remote Access before you deploy tooAzure</span></span>
> [!NOTE]
> <span data-ttu-id="97720-109">tooenable l’accès à distance avant de déployer votre tooAzure d’application, vous devez toobe exécuter Eclipse sur Windows.</span><span class="sxs-lookup"><span data-stu-id="97720-109">tooenable Remote Access before you deploy your application tooAzure, you need toobe running Eclipse on Windows.</span></span>
> 
> 

<span data-ttu-id="97720-110">Hello image suivante montre hello **l’accès à distance** boîte de dialogue de propriétés utilisée tooenable l’accès à distance.</span><span class="sxs-lookup"><span data-stu-id="97720-110">hello following image shows hello **Remote Access** properties dialog used tooenable remote access.</span></span>

![][ic719494]

<span data-ttu-id="97720-111">Il existe deux hello toodisplay de façons **l’accès à distance** boîte de dialogue Propriétés :</span><span class="sxs-lookup"><span data-stu-id="97720-111">There are two ways toodisplay hello **Remote Access** properties dialog:</span></span>

* <span data-ttu-id="97720-112">Cliquez sur hello **avancé** lien Bonjour **l’accès à distance** section Hello **publier tooAzure** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="97720-112">Click hello **Advanced** link in hello **Remote Access** section of hello **Publish tooAzure** dialog.</span></span>

* <span data-ttu-id="97720-113">Ouvrez hello **propriétés** boîte de dialogue de votre projet Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="97720-113">Open hello **Properties** dialog of your Azure project.</span></span>

<span data-ttu-id="97720-114">Lorsque vous créez un nouveau projet de déploiement d’Azure, projet de hello n’aura pas accès à distance activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="97720-114">When you create a new Azure deployment project, hello project will not have Remote Access enabled by default.</span></span> <span data-ttu-id="97720-115">Toutefois, vous pouvez facilement activer l’accès à distance en spécifiant le nom d’utilisateur hello et le mot de passe Bonjour **publier tooAzure** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="97720-115">However, you can easily enable remote access by specifying hello user name and password in hello **Publish tooAzure** dialog.</span></span> <span data-ttu-id="97720-116">mot de passe de l’accès à distance Hello est chiffré à l’aide de certificats X.509.</span><span class="sxs-lookup"><span data-stu-id="97720-116">hello Remote Access password is encrypted using X.509 certificates.</span></span> <span data-ttu-id="97720-117">Si vous n’utilisez pas fournir votre propre certificat, le chiffrement hello s’appuie sur un certificat auto-signé fourni avec hello plug-in Azure pour Eclipse.</span><span class="sxs-lookup"><span data-stu-id="97720-117">If you do not use provide your own certificate, hello encryption relies on a self-signed certificate shipped with hello Azure Plugin for Eclipse.</span></span> <span data-ttu-id="97720-118">Ce certificat auto-signé est Bonjour **cert** dossier de votre projet Windows Azure, stocké à la fois en tant que fichier de certificat public (SampleRemoteAccessPublic.cer) et comme un Exchange informations personnelles (PFX) (fichier de certificat SampleRemoteAccessPrivate.pfx).</span><span class="sxs-lookup"><span data-stu-id="97720-118">This self-signed certificate is in hello **cert** folder of your Azure project, stored both as a public certificate file (SampleRemoteAccessPublic.cer) and as a Personal Information Exchange (PFX) certificate file (SampleRemoteAccessPrivate.pfx).</span></span> <span data-ttu-id="97720-119">Hello ce dernier contient hello clé privée hello, et a un mot de passe par défaut, **Password1**.</span><span class="sxs-lookup"><span data-stu-id="97720-119">hello latter contains hello private key for hello certificate, and it has a default password, **Password1**.</span></span> <span data-ttu-id="97720-120">Toutefois, ce mot de passe étant publiquement connu, certificat par défaut de hello doit être utilisé uniquement pour l’apprentissage, pas pour un déploiement de production.</span><span class="sxs-lookup"><span data-stu-id="97720-120">However, since this password is public knowledge, hello default certificate should be used only for learning purposes, not for a production deployment.</span></span> <span data-ttu-id="97720-121">Par conséquent, autre qu’à des fins pédagogiques, lorsque vous souhaitez tooenabled les sessions à distance pour vos déploiements, vous devez cliquer sur hello **avancé** lien Bonjour **publier tooAzure** toospecify de la boîte de dialogue votre propre certificat.</span><span class="sxs-lookup"><span data-stu-id="97720-121">So other than for learning purposes, when you want tooenabled remote sessions for your deployments, you should click hello **Advanced** link in hello **Publish tooAzure** dialog toospecify your own certificate.</span></span> <span data-ttu-id="97720-122">Notez que vous devez avoir la version PFX hello tooupload hello tooyour hébergé du service de certificats dans hello portail de gestion Azure afin qu’Azure puisse déchiffrer le mot de passe utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="97720-122">Note that you'll need tooupload hello PFX version of hello certificate tooyour hosted service within hello Azure Management Portal, so that Azure can decrypt hello user password.</span></span>

<span data-ttu-id="97720-123">reste Hello du didacticiel de hello vous montre comment l’accès à distance de tooenable d’un projet de déploiement d’Azure qui a été initialement créé avec l’accès à distance est désactivé.</span><span class="sxs-lookup"><span data-stu-id="97720-123">hello remainder of hello tutorial shows you how tooenable remote access for an Azure deployment project that was initially created with remote access disabled.</span></span> <span data-ttu-id="97720-124">Pour les besoins de ce didacticiel, nous allons créer un certificat auto-signé, dont le fichier .pfx aura le mot de passe de votre choix.</span><span class="sxs-lookup"><span data-stu-id="97720-124">For purposes of this tutorial, we'll create a new self-signed certificate, and its .pfx file will have a password of your choice.</span></span> <span data-ttu-id="97720-125">Vous avez également option hello d’à l’aide d’un certificat émis par une autorité de certification.</span><span class="sxs-lookup"><span data-stu-id="97720-125">You also have hello option of using a certificate issued by a certificate authority.</span></span>

## <a name="how-tooenable-remote-access-after-you-have-deployed-tooazure"></a><span data-ttu-id="97720-126">Comment tooenable l’accès à distance après l’avoir déployé tooAzure</span><span class="sxs-lookup"><span data-stu-id="97720-126">How tooenable Remote Access after you have deployed tooAzure</span></span>
<span data-ttu-id="97720-127">accès à distance tooenable après avoir déployé tooAzure, hello utilisation comme suit :</span><span class="sxs-lookup"><span data-stu-id="97720-127">tooenable remote access after you have deployed tooAzure, use hello following steps:</span></span>

1. <span data-ttu-id="97720-128">Connectez-vous au portail de gestion Azure hello à l’aide de votre compte Azure</span><span class="sxs-lookup"><span data-stu-id="97720-128">Log into hello Azure management portal using your Azure account</span></span>

2. <span data-ttu-id="97720-129">Dans la liste **Cloud Services**, sélectionnez votre service cloud déployé.</span><span class="sxs-lookup"><span data-stu-id="97720-129">In your list of **Cloud Services**, select your deployed cloud service</span></span>

3. <span data-ttu-id="97720-130">Dans la page web de hello cloud service, cliquez sur hello **configurer** lien</span><span class="sxs-lookup"><span data-stu-id="97720-130">In hello cloud service web page, click hello **Configure** link</span></span>

4. <span data-ttu-id="97720-131">Hello le bas de la page de configuration hello, cliquez sur hello **distant** lien</span><span class="sxs-lookup"><span data-stu-id="97720-131">On hello bottom of hello configuration page, click hello **Remote** link</span></span>

5. <span data-ttu-id="97720-132">Lorsque la boîte de dialogue contextuelle hello s’affiche :</span><span class="sxs-lookup"><span data-stu-id="97720-132">When hello pop-up dialog box appears:</span></span>
   
   * <span data-ttu-id="97720-133">Spécifiez hello rôle pour lequel que vous voulez tooenable l’accès à distance</span><span class="sxs-lookup"><span data-stu-id="97720-133">Specify hello Role you for which you want tooenable remote access</span></span>

   * <span data-ttu-id="97720-134">Cliquez sur tooselect hello **activer le Bureau à distance** case à cocher</span><span class="sxs-lookup"><span data-stu-id="97720-134">Click tooselect hello **Enable Remote Desktop** checkbox</span></span>
   
   * <span data-ttu-id="97720-135">Spécifiez un nom d’utilisateur et un mot de passe toouse pour l’accès à distance</span><span class="sxs-lookup"><span data-stu-id="97720-135">Specify a user name and password you want toouse for remote access</span></span>
   
   * <span data-ttu-id="97720-136">Sélectionnez hello certificat toouse</span><span class="sxs-lookup"><span data-stu-id="97720-136">Select hello certificate toouse</span></span>

6. <span data-ttu-id="97720-137">Cliquez sur **OK**</span><span class="sxs-lookup"><span data-stu-id="97720-137">Click **OK**</span></span> 

<span data-ttu-id="97720-138">Vous verrez un message indiquant que la modification de votre configuration est en cours d’exécution, ce qui peut prendre quelques minutes toocomplete.</span><span class="sxs-lookup"><span data-stu-id="97720-138">You will see a message stating that your configuration change is in progress, which may take a few minutes toocomplete.</span></span> <span data-ttu-id="97720-139">Une fois la modification de configuration hello terminée, suivez les étapes de hello Bonjour **toolog dans à distance** section plus loin dans cet article.</span><span class="sxs-lookup"><span data-stu-id="97720-139">After hello configuration change has completed, follow hello steps in hello **toolog in remotely** section later in this article.</span></span>

## <a name="how-tooenable-remote-access-in-your-package"></a><span data-ttu-id="97720-140">Comment tooenable l’accès à distance dans votre package.</span><span class="sxs-lookup"><span data-stu-id="97720-140">How tooenable Remote Access in your package</span></span>
1. <span data-ttu-id="97720-141">Dans le volet de l’Explorateur de projets d’Eclipse, cliquez avec le bouton droit sur votre projet Azure, puis sur **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="97720-141">Within Eclipse's Project Explorer pane, right-click your Azure project and click **Properties**.</span></span>

2. <span data-ttu-id="97720-142">Bonjour **propriétés** boîte de dialogue, développez **Azure** dans le volet gauche de hello et cliquez sur **l’accès à distance**.</span><span class="sxs-lookup"><span data-stu-id="97720-142">In hello **Properties** dialog, expand **Azure** in hello left-hand pane and click **Remote Access**.</span></span>

3. <span data-ttu-id="97720-143">Bonjour **l’accès à distance** boîte de dialogue, vérifiez **activer tous les rôles tooaccept les connexions Bureau à distance avec ces informations d’identification de connexion** est activée.</span><span class="sxs-lookup"><span data-stu-id="97720-143">In hello **Remote Access** dialog, ensure **Enable all roles tooaccept Remote Desktop Connections with these login credentials** is checked.</span></span>

4. <span data-ttu-id="97720-144">Spécifiez un nom d’utilisateur pour hello connexion Bureau à distance.</span><span class="sxs-lookup"><span data-stu-id="97720-144">Specify a user name for hello Remote Desktop connection.</span></span>

5. <span data-ttu-id="97720-145">Spécifiez et confirmez le mot de passe hello pour hello.</span><span class="sxs-lookup"><span data-stu-id="97720-145">Specify and confirm hello password for hello user.</span></span> <span data-ttu-id="97720-146">vous servira Hello utilisateur nom et mot de passe valeurs définies dans cette boîte de dialogue lorsque vous établissez une connexion Bureau à distance.</span><span class="sxs-lookup"><span data-stu-id="97720-146">hello user name and password values set in this dialog will be used when you make a Remote Desktop connection.</span></span> <span data-ttu-id="97720-147">(Notez qu’il s’agit d’un mot de passe distinct de celui de votre fichier PFX.)</span><span class="sxs-lookup"><span data-stu-id="97720-147">(Note that this is a separate password from your PFX password.)</span></span>

6. <span data-ttu-id="97720-148">Spécifiez la date d’expiration de hello hello compte d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="97720-148">Specify hello expiration date for hello user account.</span></span>

7. <span data-ttu-id="97720-149">Cliquez sur **nouveau** toocreate un nouveau certificat auto-signé.</span><span class="sxs-lookup"><span data-stu-id="97720-149">Click **New** toocreate a new self-signed certificate.</span></span> <span data-ttu-id="97720-150">(Ou bien, vous pouvez sélectionner un certificat à partir de votre système de fichiers ou d’espace de travail via hello **espace de travail** ou **FileSystem** des boutons, respectivement, mais pour les besoins de ce didacticiel, nous allons créer un nouveau certificat.)</span><span class="sxs-lookup"><span data-stu-id="97720-150">(Alternatively, you could select a certificate from your workspace or file system through hello **Workspace** or **FileSystem** buttons, respectively, but for purposes of this tutorial we'll create a new certificate.)</span></span>

   * <span data-ttu-id="97720-151">Bonjour **nouveau certificat** boîte de dialogue, spécifiez et confirmez le mot de passe hello vous utiliserez pour votre fichier PFX.</span><span class="sxs-lookup"><span data-stu-id="97720-151">In hello **New Certificate** dialog, specify and confirm hello password you'll use for your PFX file.</span></span>

   * <span data-ttu-id="97720-152">Acceptez la valeur hello fournie pour **nom (CN)**, ou utilisez un nom personnalisé.</span><span class="sxs-lookup"><span data-stu-id="97720-152">Accept hello value provided for **Name (CN)**, or use a custom name.</span></span>

   * <span data-ttu-id="97720-153">Spécifiez hello chemin d’accès et nom de fichier dans lequel hello nouveau certificat, au format .cer doit être enregistré.</span><span class="sxs-lookup"><span data-stu-id="97720-153">Specify hello path and file name where hello new certificate, in .cer form, will be saved.</span></span> <span data-ttu-id="97720-154">Pour cette étape et hello suivante, vous pouvez utiliser hello **cert** dossier de votre projet Windows Azure, mais vous êtes libre toochoose un autre emplacement.</span><span class="sxs-lookup"><span data-stu-id="97720-154">For this step and hello next step, you could use hello **cert** folder of your Azure project, but you're free toochoose another location.</span></span> <span data-ttu-id="97720-155">Dans le cadre de ce didacticiel, nous utiliserons **c:\mycert\mycert.cer**.</span><span class="sxs-lookup"><span data-stu-id="97720-155">For purposes of this tutorial, we'll use **c:\mycert\mycert.cer**.</span></span> <span data-ttu-id="97720-156">(Créer hello **c:\mycert** tooproceeding préalable du dossier, ou choisissez un dossier existant si vous le souhaitez.)</span><span class="sxs-lookup"><span data-stu-id="97720-156">(Create hello **c:\mycert** folder prior tooproceeding, or use an existing folder if desired.)</span></span>

   * <span data-ttu-id="97720-157">Spécifiez hello chemin d’accès et nom de fichier où seront enregistrées hello nouveau certificat et sa clé privée, au format .pfx.</span><span class="sxs-lookup"><span data-stu-id="97720-157">Specify hello path and file name where hello new certificate and its private key, in .pfx form, will be saved.</span></span> <span data-ttu-id="97720-158">Dans le cadre de ce didacticiel, nous utiliserons **c:\mycert\mycert.pfx**.</span><span class="sxs-lookup"><span data-stu-id="97720-158">For purposes of this tutorial, we'll use **c:\mycert\mycert.pfx**.</span></span> <span data-ttu-id="97720-159">Votre **nouveau certificat** boîte de dialogue doit se présenter comme toohello suivant (mettre à jour les chemins d’accès du dossier hello si vous n’utilisez pas **c:\mycert**) :</span><span class="sxs-lookup"><span data-stu-id="97720-159">Your **New Certificate** dialog should look similar toohello following (update hello folder paths if you did not use **c:\mycert**):</span></span>
     
      ![][ic712275]

   * <span data-ttu-id="97720-160">Cliquez sur **OK** tooclose hello **nouveau certificat** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="97720-160">Click **OK** tooclose hello **New Certificate** dialog.</span></span>

8. <span data-ttu-id="97720-161">Votre **l’accès à distance** boîte de dialogue doit se présenter comme toohello suivantes :</span><span class="sxs-lookup"><span data-stu-id="97720-161">Your **Remote Access** dialog should look similar toohello following:</span></span></p>
   
   ![][ic719495]

9. <span data-ttu-id="97720-162">Cliquez sur **OK** tooclose hello **l’accès à distance** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="97720-162">Click **OK** tooclose hello **Remote Access** dialog.</span></span>

<span data-ttu-id="97720-163">Régénérez votre application, avec hello générer ensemble pour toocloud de déploiement.</span><span class="sxs-lookup"><span data-stu-id="97720-163">Rebuild your application, with hello build set for deployment toocloud.</span></span>

## <a name="toolog-in-remotely"></a><span data-ttu-id="97720-164">toolog dans à distance</span><span class="sxs-lookup"><span data-stu-id="97720-164">toolog in remotely</span></span>
<span data-ttu-id="97720-165">Une fois que votre instance de rôle est prêt, vous pouvez vous connecter à distance dans la machine virtuelle toohello qui héberge votre application.</span><span class="sxs-lookup"><span data-stu-id="97720-165">Once your role instance is ready, you can remotely log in toohello virtual machine that is hosting your application.</span></span>

* <span data-ttu-id="97720-166">Si vous utilisez Eclipse sur Windows et vous hello sélectionné **démarrer le Bureau à distance sur déploiement** option lors de votre déploiement tooAzure, s’affiche avec un écran d’ouverture de session de connexion Bureau à distance au démarrage de votre déploiement.</span><span class="sxs-lookup"><span data-stu-id="97720-166">If are using Eclipse on Windows and you selected hello **Start remote desktop on deploy** option during your deployment tooAzure, you will be presented with a Remote Desktop Connection logon screen when your deployment starts.</span></span> <span data-ttu-id="97720-167">Lorsque vous êtes invité hello nom d’utilisateur et mot de passe, entrez les valeurs hello que vous avez spécifié pour l’utilisateur distant de hello et sera en mesure de toolog dans.</span><span class="sxs-lookup"><span data-stu-id="97720-167">When you are prompted for hello user name and password, enter hello values that you specified for hello remote user and will be able toolog in.</span></span>

* <span data-ttu-id="97720-168">Un autre toolog moyen dans est à distance via hello <a href="http://go.microsoft.com/fwlink/?LinkID=512959">portail de gestion Azure</a>:</span><span class="sxs-lookup"><span data-stu-id="97720-168">Another way toolog in remotely is through hello <a href="http://go.microsoft.com/fwlink/?LinkID=512959">Azure Management Portal</a>:</span></span>
  
  * <span data-ttu-id="97720-169">Au sein de hello **Services de cloud computing** vue Hello portail de gestion Azure, cliquez sur votre service cloud, cliquez sur **Instances**et cliquez sur une instance spécifique, puis cliquez sur hello **Connect**bouton.</span><span class="sxs-lookup"><span data-stu-id="97720-169">Within hello **Cloud Services** view of hello Azure Management portal, click your cloud service, click **Instances**, click a specific instance, and then click hello **Connect** button.</span></span> <span data-ttu-id="97720-170">Hello **Connect** bouton s’affiche comme suit hello dans la barre de commandes hello :</span><span class="sxs-lookup"><span data-stu-id="97720-170">hello **Connect** button appears as hello following in hello command bar:</span></span>
    
      ![][ic659273]

  * <span data-ttu-id="97720-171">Après avoir cliqué sur hello **Connect** bouton, vous serez invité à tooopen un fichier RDP.</span><span class="sxs-lookup"><span data-stu-id="97720-171">After clicking hello **Connect** button, you will be prompted tooopen an RDP file.</span></span> <span data-ttu-id="97720-172">Ouvrir le fichier de hello et suivez les invites hello.</span><span class="sxs-lookup"><span data-stu-id="97720-172">Open hello file and follow hello prompts.</span></span> <span data-ttu-id="97720-173">(Votre peut également enregistrer cet ordinateur local tooyour de fichier, puis exécutez hello fichier en double-cliquant dessus tooremote journal dans tooyour machine virtuelle sans avoir besoin de toofirst atteindre le portail de gestion hello.)</span><span class="sxs-lookup"><span data-stu-id="97720-173">(You could also save this file tooyour local computer, and then run hello file by double-clicking it tooremote log in tooyour virtual machine without needing toofirst go hello management portal.)</span></span>

  * <span data-ttu-id="97720-174">Lorsque vous êtes invité hello nom d’utilisateur et mot de passe, entrez les valeurs hello que vous avez spécifié pour l’utilisateur distant de hello et sera en mesure de toolog dans.</span><span class="sxs-lookup"><span data-stu-id="97720-174">When you are prompted for hello user name and password, enter hello values that you specified for hello remote user and will be able toolog in.</span></span>

> [!NOTE]
> <span data-ttu-id="97720-175">Si vous êtes sur un système d’exploitation non-Windows, vous devez toouse un client Bureau à distance qui est compatible avec votre système d’exploitation et suivez hello étapes tooconfigure que le client avec les paramètres de hello dans le fichier RDP hello que vous avez téléchargé.</span><span class="sxs-lookup"><span data-stu-id="97720-175">If you are on a non-Windows operating system, you need toouse a Remote Desktop client that is compatible with your operating system and follow hello steps tooconfigure that client with hello settings in hello RDP file that you downloaded.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="97720-176">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="97720-176">See Also</span></span>
<span data-ttu-id="97720-177">[Kit de ressources Azure pour Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="97720-177">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="97720-178">[Création d’une application Hello World pour Azure dans Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="97720-178">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="97720-179">[Lors de l’installation hello boîte à outils Azure pour Eclipse][Installing hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="97720-179">[Installing hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="97720-180">Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez hello [centre de développement Java Azure][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="97720-180">For more information about using Azure with Java, see hello [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic712275]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic712275.png
[ic719495]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic719495.png
[ic719494]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic719494.png
[ic659273]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic659273.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690951.aspx -->
