---
title: "Activation de l’accès à distance pour les déploiements Azure dans Eclipse"
description: "Découvrez comment activer l’accès à distance pour les déploiements Azure à l’aide de la Boîte à outils Azure pour Eclipse."
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
ms.openlocfilehash: 654d511bd5a62341f87569317e97360c94a6f26c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="enabling-remote-access-for-azure-deployments-in-eclipse"></a><span data-ttu-id="48527-103">Activation de l’accès à distance pour les déploiements Azure dans Eclipse</span><span class="sxs-lookup"><span data-stu-id="48527-103">Enabling Remote Access for Azure Deployments in Eclipse</span></span>
<span data-ttu-id="48527-104">Pour faciliter le dépannage de vos déploiements, vous pouvez activer et utiliser l’accès à distance pour vous connecter à la machine virtuelle hébergeant votre déploiement.</span><span class="sxs-lookup"><span data-stu-id="48527-104">To help troubleshoot your deployments, you may enable and use Remote Access to connect to the virtual machine hosting your deployment.</span></span> <span data-ttu-id="48527-105">La fonctionnalité d’accès à distance s’appuie sur le protocole RDP (Remote Desktop Protocol).</span><span class="sxs-lookup"><span data-stu-id="48527-105">The Remote Access functionality relies on the Remote Desktop Protocol (RDP).</span></span> <span data-ttu-id="48527-106">Vous pouvez configurer l’accès à distance pour votre déploiement après l’avoir publié dans Azure ou, si vous utilisez Eclipse avec un système d’exploitation Windows, avant de le publier dans Azure.</span><span class="sxs-lookup"><span data-stu-id="48527-106">You can configure Remote Access for your deployment after you have published it to Azure, or if you are using Eclipse with a Windows operating system, you can configure Remote Access before you publish to Azure.</span></span> <span data-ttu-id="48527-107">Notez que, pour vous connecter à la machine virtuelle de votre déploiement dans Azure, vous avez besoin d’un client Bureau à distance compatible avec votre système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="48527-107">Note that you will need a remote desktop client that is compatible with your operating system in order to connect to your deployment's virtual machine in Azure.</span></span>

## <a name="how-to-enable-remote-access-before-you-deploy-to-azure"></a><span data-ttu-id="48527-108">Comment activer l’accès distant avant le déploiement dans Azure</span><span class="sxs-lookup"><span data-stu-id="48527-108">How to enable Remote Access before you deploy to Azure</span></span>
> [!NOTE]
> <span data-ttu-id="48527-109">Pour activer l’accès à distance avant de déployer votre application dans Azure, vous devez exécuter Eclipse dans Windows.</span><span class="sxs-lookup"><span data-stu-id="48527-109">To enable Remote Access before you deploy your application to Azure, you need to be running Eclipse on Windows.</span></span>
> 
> 

<span data-ttu-id="48527-110">L’illustration suivante montre la boîte de dialogue de propriétés **Accès distant** qui permet d’activer l’accès à distance.</span><span class="sxs-lookup"><span data-stu-id="48527-110">The following image shows the **Remote Access** properties dialog used to enable remote access.</span></span>

![][ic719494]

<span data-ttu-id="48527-111">Il existe deux manières d’afficher la boîte de dialogue de propriétés **Accès distant** :</span><span class="sxs-lookup"><span data-stu-id="48527-111">There are two ways to display the **Remote Access** properties dialog:</span></span>

* <span data-ttu-id="48527-112">Cliquer sur le lien **Avancé** dans la section **Accès distant** de la boîte de dialogue **Publier sur Azure**.</span><span class="sxs-lookup"><span data-stu-id="48527-112">Click the **Advanced** link in the **Remote Access** section of the **Publish to Azure** dialog.</span></span>

* <span data-ttu-id="48527-113">Ouvrir la boîte de dialogue **Propriétés** de votre projet Azure.</span><span class="sxs-lookup"><span data-stu-id="48527-113">Open the **Properties** dialog of your Azure project.</span></span>

<span data-ttu-id="48527-114">Lorsque vous créez un projet de déploiement Azure, par défaut l’accès à distance n’est pas activé pour celui-ci.</span><span class="sxs-lookup"><span data-stu-id="48527-114">When you create a new Azure deployment project, the project will not have Remote Access enabled by default.</span></span> <span data-ttu-id="48527-115">Toutefois, vous pouvez facilement activer l’accès à distance en spécifiant le nom d’utilisateur et le mot de passe dans la boîte de dialogue **Publier sur Azure** .</span><span class="sxs-lookup"><span data-stu-id="48527-115">However, you can easily enable remote access by specifying the user name and password in the **Publish to Azure** dialog.</span></span> <span data-ttu-id="48527-116">Le mot de passe d’accès à distance est chiffré à l’aide de certificats X.509.</span><span class="sxs-lookup"><span data-stu-id="48527-116">The Remote Access password is encrypted using X.509 certificates.</span></span> <span data-ttu-id="48527-117">Si vous n’utilisez pas votre propre certificat, le chiffrement s’appuie sur un certificat auto-signé fourni avec le plug-in Azure pour Eclipse.</span><span class="sxs-lookup"><span data-stu-id="48527-117">If you do not use provide your own certificate, the encryption relies on a self-signed certificate shipped with the Azure Plugin for Eclipse.</span></span> <span data-ttu-id="48527-118">Ce certificat auto-signé se trouve dans le dossier **cert** de votre projet Azure, stocké à la fois en tant que fichier de certificat public (SampleRemoteAccessPublic.cer) et en tant que fichier de certificat d’échange d’informations personnelles (PFX) (SampleRemoteAccessPrivate.pfx).</span><span class="sxs-lookup"><span data-stu-id="48527-118">This self-signed certificate is in the **cert** folder of your Azure project, stored both as a public certificate file (SampleRemoteAccessPublic.cer) and as a Personal Information Exchange (PFX) certificate file (SampleRemoteAccessPrivate.pfx).</span></span> <span data-ttu-id="48527-119">Ce dernier contient la clé privée du certificat, et il a un mot de passe par défaut, **Password1**.</span><span class="sxs-lookup"><span data-stu-id="48527-119">The latter contains the private key for the certificate, and it has a default password, **Password1**.</span></span> <span data-ttu-id="48527-120">Toutefois, ce mot de passe étant publiquement connu, le certificat par défaut convient uniquement pour l’apprentissage, et non pour un déploiement de production.</span><span class="sxs-lookup"><span data-stu-id="48527-120">However, since this password is public knowledge, the default certificate should be used only for learning purposes, not for a production deployment.</span></span> <span data-ttu-id="48527-121">Si ce n’est à des fins d’apprentissage, quand vous souhaitez activer les sessions à distance pour vos déploiements, vous devez cliquer sur le lien **Avancé** dans la boîte de dialogue **Publier sur Azure** pour spécifier votre propre certificat.</span><span class="sxs-lookup"><span data-stu-id="48527-121">So other than for learning purposes, when you want to enabled remote sessions for your deployments, you should click the **Advanced** link in the **Publish to Azure** dialog to specify your own certificate.</span></span> <span data-ttu-id="48527-122">Notez que vous devez charger la version PFX du certificat vers votre service hébergé dans le portail de gestion Azure, pour qu’Azure puisse déchiffrer le mot de passe utilisateur.</span><span class="sxs-lookup"><span data-stu-id="48527-122">Note that you'll need to upload the PFX version of the certificate to your hosted service within the Azure Management Portal, so that Azure can decrypt the user password.</span></span>

<span data-ttu-id="48527-123">La suite de ce didacticiel montre comment activer l’accès à distance pour un projet de déploiement Azure créé initialement avec l’accès à distance désactivé.</span><span class="sxs-lookup"><span data-stu-id="48527-123">The remainder of the tutorial shows you how to enable remote access for an Azure deployment project that was initially created with remote access disabled.</span></span> <span data-ttu-id="48527-124">Pour les besoins de ce didacticiel, nous allons créer un certificat auto-signé, dont le fichier .pfx aura le mot de passe de votre choix.</span><span class="sxs-lookup"><span data-stu-id="48527-124">For purposes of this tutorial, we'll create a new self-signed certificate, and its .pfx file will have a password of your choice.</span></span> <span data-ttu-id="48527-125">Vous pouvez également utiliser un certificat émis par une autorité de certification.</span><span class="sxs-lookup"><span data-stu-id="48527-125">You also have the option of using a certificate issued by a certificate authority.</span></span>

## <a name="how-to-enable-remote-access-after-you-have-deployed-to-azure"></a><span data-ttu-id="48527-126">Comment activer l’accès à distance après le déploiement dans Azure</span><span class="sxs-lookup"><span data-stu-id="48527-126">How to enable Remote Access after you have deployed to Azure</span></span>
<span data-ttu-id="48527-127">Pour activer l’accès à distance après avoir déployé votre application dans Azure, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="48527-127">To enable remote access after you have deployed to Azure, use the following steps:</span></span>

1. <span data-ttu-id="48527-128">Connectez-vous au portail de gestion Azure avec votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="48527-128">Log into the Azure management portal using your Azure account</span></span>

2. <span data-ttu-id="48527-129">Dans la liste **Cloud Services**, sélectionnez votre service cloud déployé.</span><span class="sxs-lookup"><span data-stu-id="48527-129">In your list of **Cloud Services**, select your deployed cloud service</span></span>

3. <span data-ttu-id="48527-130">Dans la page web du service cloud, cliquez sur le lien **Configurer** .</span><span class="sxs-lookup"><span data-stu-id="48527-130">In the cloud service web page, click the **Configure** link</span></span>

4. <span data-ttu-id="48527-131">Au bas de la page de configuration, cliquez sur le lien **À distance** .</span><span class="sxs-lookup"><span data-stu-id="48527-131">On the bottom of the configuration page, click the **Remote** link</span></span>

5. <span data-ttu-id="48527-132">Lorsque la boîte de dialogue contextuelle s’affiche :</span><span class="sxs-lookup"><span data-stu-id="48527-132">When the pop-up dialog box appears:</span></span>
   
   * <span data-ttu-id="48527-133">Spécifiez le rôle pour lequel vous souhaitez activer l’accès à distance.</span><span class="sxs-lookup"><span data-stu-id="48527-133">Specify the Role you for which you want to enable remote access</span></span>

   * <span data-ttu-id="48527-134">Cochez la case **Activer le Bureau à distance** .</span><span class="sxs-lookup"><span data-stu-id="48527-134">Click to select the **Enable Remote Desktop** checkbox</span></span>
   
   * <span data-ttu-id="48527-135">Spécifiez un nom d’utilisateur et un mot de passe à utiliser pour l’accès à distance.</span><span class="sxs-lookup"><span data-stu-id="48527-135">Specify a user name and password you want to use for remote access</span></span>
   
   * <span data-ttu-id="48527-136">Sélectionnez le certificat à utiliser.</span><span class="sxs-lookup"><span data-stu-id="48527-136">Select the certificate to use</span></span>

6. <span data-ttu-id="48527-137">Cliquez sur **OK**</span><span class="sxs-lookup"><span data-stu-id="48527-137">Click **OK**</span></span> 

<span data-ttu-id="48527-138">Un message indique que la modification de votre configuration est en cours et que cela peut prendre quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="48527-138">You will see a message stating that your configuration change is in progress, which may take a few minutes to complete.</span></span> <span data-ttu-id="48527-139">Une fois la modification de la configuration terminée, suivez les étapes de la section **Connexion à distance** plus loin dans cet article.</span><span class="sxs-lookup"><span data-stu-id="48527-139">After the configuration change has completed, follow the steps in the **To log in remotely** section later in this article.</span></span>

## <a name="how-to-enable-remote-access-in-your-package"></a><span data-ttu-id="48527-140">Comment activer l’accès à distance dans votre package</span><span class="sxs-lookup"><span data-stu-id="48527-140">How to enable Remote Access in your package</span></span>
1. <span data-ttu-id="48527-141">Dans le volet de l’Explorateur de projets d’Eclipse, cliquez avec le bouton droit sur votre projet Azure, puis sur **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="48527-141">Within Eclipse's Project Explorer pane, right-click your Azure project and click **Properties**.</span></span>

2. <span data-ttu-id="48527-142">Dans la boîte de dialogue **Propriétés**, développez **Azure** dans le volet gauche et cliquez sur **Accès distant**.</span><span class="sxs-lookup"><span data-stu-id="48527-142">In the **Properties** dialog, expand **Azure** in the left-hand pane and click **Remote Access**.</span></span>

3. <span data-ttu-id="48527-143">Dans la boîte de dialogue **Accès distant**, assurez-vous que l’option **Activer tous les rôles pour qu’ils acceptent les connexions Bureau à distance avec les informations d’identification de connexion suivantes** soit activée.</span><span class="sxs-lookup"><span data-stu-id="48527-143">In the **Remote Access** dialog, ensure **Enable all roles to accept Remote Desktop Connections with these login credentials** is checked.</span></span>

4. <span data-ttu-id="48527-144">Spécifiez un nom d’utilisateur pour la connexion Bureau à distance.</span><span class="sxs-lookup"><span data-stu-id="48527-144">Specify a user name for the Remote Desktop connection.</span></span>

5. <span data-ttu-id="48527-145">Spécifiez et confirmez le mot de passe de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="48527-145">Specify and confirm the password for the user.</span></span> <span data-ttu-id="48527-146">Les valeurs de nom d’utilisateur et de mot de passe définies dans cette boîte de dialogue seront utilisées lors de l’établissement de votre connexion Bureau à distance.</span><span class="sxs-lookup"><span data-stu-id="48527-146">The user name and password values set in this dialog will be used when you make a Remote Desktop connection.</span></span> <span data-ttu-id="48527-147">(Notez qu’il s’agit d’un mot de passe distinct de celui de votre fichier PFX.)</span><span class="sxs-lookup"><span data-stu-id="48527-147">(Note that this is a separate password from your PFX password.)</span></span>

6. <span data-ttu-id="48527-148">Spécifiez la date d’expiration du compte d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="48527-148">Specify the expiration date for the user account.</span></span>

7. <span data-ttu-id="48527-149">Cliquez sur **Nouveau** pour créer un certificat auto-signé.</span><span class="sxs-lookup"><span data-stu-id="48527-149">Click **New** to create a new self-signed certificate.</span></span> <span data-ttu-id="48527-150">(Vous pouvez aussi sélectionner un certificat de votre espace de travail ou de votre système de fichiers, respectivement à l’aide des boutons **Espace de travail** ou **Système de fichiers**, mais pour les besoins de ce didacticiel nous allons créer un certificat.)</span><span class="sxs-lookup"><span data-stu-id="48527-150">(Alternatively, you could select a certificate from your workspace or file system through the **Workspace** or **FileSystem** buttons, respectively, but for purposes of this tutorial we'll create a new certificate.)</span></span>

   * <span data-ttu-id="48527-151">Dans la boîte de dialogue **Nouveau certificat** , spécifiez et confirmez le mot de passe que vous utiliserez pour votre fichier PFX.</span><span class="sxs-lookup"><span data-stu-id="48527-151">In the **New Certificate** dialog, specify and confirm the password you'll use for your PFX file.</span></span>

   * <span data-ttu-id="48527-152">Acceptez la valeur fournie pour **Nom (CN)**ou utilisez un nom personnalisé.</span><span class="sxs-lookup"><span data-stu-id="48527-152">Accept the value provided for **Name (CN)**, or use a custom name.</span></span>

   * <span data-ttu-id="48527-153">Spécifiez le chemin d’accès et le nom de fichier sous lesquels le nouveau certificat sera enregistré au format .cer.</span><span class="sxs-lookup"><span data-stu-id="48527-153">Specify the path and file name where the new certificate, in .cer form, will be saved.</span></span> <span data-ttu-id="48527-154">Pour cette étape et la suivante, vous pouvez utiliser le dossier **cert** de votre projet Azure, mais vous êtes libre de choisir un autre emplacement.</span><span class="sxs-lookup"><span data-stu-id="48527-154">For this step and the next step, you could use the **cert** folder of your Azure project, but you're free to choose another location.</span></span> <span data-ttu-id="48527-155">Dans le cadre de ce didacticiel, nous utiliserons **c:\mycert\mycert.cer**.</span><span class="sxs-lookup"><span data-stu-id="48527-155">For purposes of this tutorial, we'll use **c:\mycert\mycert.cer**.</span></span> <span data-ttu-id="48527-156">(Avant de continuer, créez le dossier **c:\mycert** ou choisissez un dossier existant.)</span><span class="sxs-lookup"><span data-stu-id="48527-156">(Create the **c:\mycert** folder prior to proceeding, or use an existing folder if desired.)</span></span>

   * <span data-ttu-id="48527-157">Spécifiez le chemin d’accès et le nom de fichier sous lesquels le nouveau certificat et sa clé privée seront enregistrés au format .pfx.</span><span class="sxs-lookup"><span data-stu-id="48527-157">Specify the path and file name where the new certificate and its private key, in .pfx form, will be saved.</span></span> <span data-ttu-id="48527-158">Dans le cadre de ce didacticiel, nous utiliserons **c:\mycert\mycert.pfx**.</span><span class="sxs-lookup"><span data-stu-id="48527-158">For purposes of this tutorial, we'll use **c:\mycert\mycert.pfx**.</span></span> <span data-ttu-id="48527-159">La boîte de dialogue **Nouveau certificat** doit ressembler à ce qui suit (si vous n’utilisez pas **c:\mycert**, mettez à jour les chemins d’accès au dossier) :</span><span class="sxs-lookup"><span data-stu-id="48527-159">Your **New Certificate** dialog should look similar to the following (update the folder paths if you did not use **c:\mycert**):</span></span>
     
      ![][ic712275]

   * <span data-ttu-id="48527-160">Cliquez sur **OK** pour fermer la boîte de dialogue **Nouveau certificat**.</span><span class="sxs-lookup"><span data-stu-id="48527-160">Click **OK** to close the **New Certificate** dialog.</span></span>

8. <span data-ttu-id="48527-161">La boîte de dialogue **Accès distant** doit ressembler à celle-ci :</span><span class="sxs-lookup"><span data-stu-id="48527-161">Your **Remote Access** dialog should look similar to the following:</span></span></p>
   
   ![][ic719495]

9. <span data-ttu-id="48527-162">Cliquez sur **OK** pour fermer la boîte de dialogue **Accès distant**.</span><span class="sxs-lookup"><span data-stu-id="48527-162">Click **OK** to close the **Remote Access** dialog.</span></span>

<span data-ttu-id="48527-163">Régénérez votre application, avec la build définie pour le déploiement dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="48527-163">Rebuild your application, with the build set for deployment to cloud.</span></span>

## <a name="to-log-in-remotely"></a><span data-ttu-id="48527-164">Connexion à distance</span><span class="sxs-lookup"><span data-stu-id="48527-164">To log in remotely</span></span>
<span data-ttu-id="48527-165">Une fois votre instance de rôle prête, vous pouvez vous connecter à distance à la machine virtuelle hébergeant votre application.</span><span class="sxs-lookup"><span data-stu-id="48527-165">Once your role instance is ready, you can remotely log in to the virtual machine that is hosting your application.</span></span>

* <span data-ttu-id="48527-166">Si vous utilisez Eclipse dans Windows et que vous avez sélectionné l’option **Démarrer le Bureau à distance lors du déploiement** durant le déploiement dans Azure, l’écran d’ouverture de session Connexion Bureau à distance s’affiche au démarrage du déploiement.</span><span class="sxs-lookup"><span data-stu-id="48527-166">If are using Eclipse on Windows and you selected the **Start remote desktop on deploy** option during your deployment to Azure, you will be presented with a Remote Desktop Connection logon screen when your deployment starts.</span></span> <span data-ttu-id="48527-167">Lorsque vous êtes invité à entrer le nom d’utilisateur et le mot de passe, entrez les valeurs que vous avez spécifiées pour l’utilisateur distant pour établir la connexion.</span><span class="sxs-lookup"><span data-stu-id="48527-167">When you are prompted for the user name and password, enter the values that you specified for the remote user and will be able to log in.</span></span>

* <span data-ttu-id="48527-168">Une autre façon de se connecter à distance consiste à utiliser le <a href="http://go.microsoft.com/fwlink/?LinkID=512959">portail de gestion Azure</a> :</span><span class="sxs-lookup"><span data-stu-id="48527-168">Another way to log in remotely is through the <a href="http://go.microsoft.com/fwlink/?LinkID=512959">Azure Management Portal</a>:</span></span>
  
  * <span data-ttu-id="48527-169">Dans l’affichage **Cloud Services** du portail de gestion Azure, cliquez sur votre service cloud, sur **Instances**, sur une instance spécifique, puis sur le bouton **Connexion**.</span><span class="sxs-lookup"><span data-stu-id="48527-169">Within the **Cloud Services** view of the Azure Management portal, click your cloud service, click **Instances**, click a specific instance, and then click the **Connect** button.</span></span> <span data-ttu-id="48527-170">Le bouton **Connexion** s’affiche comme suit dans la barre de commandes :</span><span class="sxs-lookup"><span data-stu-id="48527-170">The **Connect** button appears as the following in the command bar:</span></span>
    
      ![][ic659273]

  * <span data-ttu-id="48527-171">Après avoir cliqué sur le bouton **Connexion** , vous êtes invité à ouvrir un fichier RDP.</span><span class="sxs-lookup"><span data-stu-id="48527-171">After clicking the **Connect** button, you will be prompted to open an RDP file.</span></span> <span data-ttu-id="48527-172">Ouvrez le fichier et suivez les invites.</span><span class="sxs-lookup"><span data-stu-id="48527-172">Open the file and follow the prompts.</span></span> <span data-ttu-id="48527-173">(Vous pouvez aussi enregistrer ce fichier sur votre ordinateur local, puis l’exécuter en double-cliquant dessus pour vous connecter à distance à votre machine virtuelle sans avoir à accéder d’abord au portail de gestion).</span><span class="sxs-lookup"><span data-stu-id="48527-173">(You could also save this file to your local computer, and then run the file by double-clicking it to remote log in to your virtual machine without needing to first go the management portal.)</span></span>

  * <span data-ttu-id="48527-174">Lorsque vous êtes invité à entrer le nom d’utilisateur et le mot de passe, entrez les valeurs que vous avez spécifiées pour l’utilisateur distant pour établir la connexion.</span><span class="sxs-lookup"><span data-stu-id="48527-174">When you are prompted for the user name and password, enter the values that you specified for the remote user and will be able to log in.</span></span>

> [!NOTE]
> <span data-ttu-id="48527-175">Si vous exécutez un système d’exploitation autre que Windows, vous devez utiliser un client Bureau à distance compatible avec votre système d’exploitation et suivre les étapes de configuration de ce client avec les paramètres définis dans le fichier RDP que vous avez téléchargé.</span><span class="sxs-lookup"><span data-stu-id="48527-175">If you are on a non-Windows operating system, you need to use a Remote Desktop client that is compatible with your operating system and follow the steps to configure that client with the settings in the RDP file that you downloaded.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="48527-176">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="48527-176">See Also</span></span>
<span data-ttu-id="48527-177">[Kit de ressources Azure pour Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="48527-177">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="48527-178">[Création d’une application Hello World pour Azure dans Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="48527-178">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="48527-179">[Installation du kit de ressources Azure pour Eclipse][Installing the Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="48527-179">[Installing the Azure Toolkit for Eclipse][Installing the Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="48527-180">Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez le [Centre de développement Java pour Azure][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="48527-180">For more information about using Azure with Java, see the [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic712275]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic712275.png
[ic719495]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic719495.png
[ic719494]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic719494.png
[ic659273]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic659273.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690951.aspx -->
