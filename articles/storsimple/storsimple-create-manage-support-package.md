---
title: aaaCreate un package de support StorSimple | Documents Microsoft
description: "Découvrez comment toocreate, déchiffrer et modifier un package de prise en charge pour votre appareil StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: eac76f5f-5db1-4c92-af8c-54053b91e66c
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 209aeee50e823fd2ca96ababd1d0cf3ea9cdad53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-a-storsimple-support-package"></a><span data-ttu-id="41f75-103">Création et gestion d’un package de prise en charge StorSimple</span><span class="sxs-lookup"><span data-stu-id="41f75-103">Create and manage a StorSimple support package</span></span>
## <a name="overview"></a><span data-ttu-id="41f75-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="41f75-104">Overview</span></span>
<span data-ttu-id="41f75-105">Un package de prise en charge de StorSimple est un mécanisme facile à utiliser qui collecte tous les journaux appropriés tooassist Support technique de Microsoft à résoudre les problèmes de votre appareil StorSimple.</span><span class="sxs-lookup"><span data-stu-id="41f75-105">A StorSimple support package is an easy-to-use mechanism that collects all relevant logs tooassist Microsoft Support with troubleshooting any StorSimple device issues.</span></span> <span data-ttu-id="41f75-106">Hello fichiers journaux collectés sont chiffrés et compressés.</span><span class="sxs-lookup"><span data-stu-id="41f75-106">hello collected logs are encrypted and compressed.</span></span>

<span data-ttu-id="41f75-107">Ce didacticiel inclut des instructions pas à pas toocreate et à gérer hello prise en charge.</span><span class="sxs-lookup"><span data-stu-id="41f75-107">This tutorial includes step-by-step instructions toocreate and manage hello support package.</span></span>

## <a name="create-and-upload-a-support-package-in-hello-azure-classic-portal"></a><span data-ttu-id="41f75-108">Créer et télécharger un package de prise en charge dans hello portail Azure classic</span><span class="sxs-lookup"><span data-stu-id="41f75-108">Create and upload a support package in hello Azure classic portal</span></span>
<span data-ttu-id="41f75-109">Vous pouvez créer et télécharger un site de Support technique de Microsoft support package toohello via hello **Maintenance** page du service hello Bonjour portail Azure classic.</span><span class="sxs-lookup"><span data-stu-id="41f75-109">You can create and upload a support package toohello Microsoft Support site through hello **Maintenance** page of hello service in hello Azure classic portal.</span></span>

> [!NOTE]
> <span data-ttu-id="41f75-110">téléchargement de Hello nécessite une clé de la prise en charge.</span><span class="sxs-lookup"><span data-stu-id="41f75-110">hello upload requires a support passkey.</span></span> <span data-ttu-id="41f75-111">Votre ingénieur du support technique doit fournir ce tooyou dans un message électronique.</span><span class="sxs-lookup"><span data-stu-id="41f75-111">Your support engineer should provide this tooyou in an email.</span></span>
> 
> 

<span data-ttu-id="41f75-112">Un package de prise en charge chiffré et compressé (fichier .cab) est créé et téléchargé toohello prise en charge de site.</span><span class="sxs-lookup"><span data-stu-id="41f75-112">An encrypted and compressed support package (.cab file) is created and uploaded toohello Support site.</span></span> <span data-ttu-id="41f75-113">ingénieur de support Hello peut ensuite extraire ce package à partir du site du support technique pour résoudre les problème hello hello.</span><span class="sxs-lookup"><span data-stu-id="41f75-113">hello support engineer can then retrieve this package from hello Support site for troubleshooting hello issue.</span></span>

<span data-ttu-id="41f75-114">Effectuer hello dans toocreate portail classique hello un package de prise en charge comme suit.</span><span class="sxs-lookup"><span data-stu-id="41f75-114">Perform hello following steps in hello classic portal toocreate a support package.</span></span>

#### <a name="toocreate-a-support-package-in-hello-azure-classic-portal"></a><span data-ttu-id="41f75-115">toocreate un package de prise en charge dans hello portail Azure classic</span><span class="sxs-lookup"><span data-stu-id="41f75-115">toocreate a support package in hello Azure classic portal</span></span>
1. <span data-ttu-id="41f75-116">Sélectionnez **Appareils** > **Maintenance**.</span><span class="sxs-lookup"><span data-stu-id="41f75-116">Select **Devices** > **Maintenance**.</span></span>
2. <span data-ttu-id="41f75-117">Bonjour **package de Support** section, sélectionnez **package de prise en charge de création et téléchargement**.</span><span class="sxs-lookup"><span data-stu-id="41f75-117">In hello **Support package** section, select **Create and upload support package**.</span></span>
3. <span data-ttu-id="41f75-118">Bonjour **package de prise en charge de création et téléchargement** boîte de dialogue zone, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="41f75-118">In hello **Create and upload support package** dialog box, do hello following:</span></span>
   
    ![Créer un package de support](./media/storsimple-create-manage-support-package/IC740923.png)
   
   * <span data-ttu-id="41f75-120">Bonjour **de support** texte, entrez la clé de sécurité hello.</span><span class="sxs-lookup"><span data-stu-id="41f75-120">In hello **Support Passkey** text box, enter hello passkey.</span></span> <span data-ttu-id="41f75-121">Votre ingénieur de support technique de Microsoft doit envoyer tooyou de cette clé de sécurité par courrier électronique.</span><span class="sxs-lookup"><span data-stu-id="41f75-121">Your Microsoft support engineer should send this passkey tooyou in email.</span></span>
   * <span data-ttu-id="41f75-122">Sélectionnez hello case tooprovide consentement tooautomatically téléchargement hello prise en charge de package toohello Support Microsoft site.</span><span class="sxs-lookup"><span data-stu-id="41f75-122">Select hello check box tooprovide consent tooautomatically upload hello support package toohello Microsoft Support site.</span></span>
   * <span data-ttu-id="41f75-123">Cliquez sur une icône de coche hello</span><span class="sxs-lookup"><span data-stu-id="41f75-123">Click hello check icon</span></span> ![Icône en forme de coche](./media/storsimple-create-manage-support-package/IC740895.png)<span data-ttu-id="41f75-125">.</span><span class="sxs-lookup"><span data-stu-id="41f75-125">.</span></span>

## <a name="manually-create-a-support-package"></a><span data-ttu-id="41f75-126">Créer manuellement un package de support</span><span class="sxs-lookup"><span data-stu-id="41f75-126">Manually create a support package</span></span>
<span data-ttu-id="41f75-127">Dans certains cas, vous devez toomanually créer le package de prise en charge de hello via Windows PowerShell pour StorSimple.</span><span class="sxs-lookup"><span data-stu-id="41f75-127">In some cases, you'll need toomanually create hello support package through Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="41f75-128">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="41f75-128">For example:</span></span>

* <span data-ttu-id="41f75-129">Si vous avez besoin des informations sensibles tooremove à partir de votre journal des fichiers préalable toosharing avec le Support technique de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="41f75-129">If you need tooremove sensitive information from your log files prior toosharing with Microsoft Support.</span></span>
* <span data-ttu-id="41f75-130">Si vous avez des difficultés à télécharger le package hello en raison de problèmes de tooconnectivity.</span><span class="sxs-lookup"><span data-stu-id="41f75-130">If you are having difficulty uploading hello package due tooconnectivity issues.</span></span>

<span data-ttu-id="41f75-131">Vous pouvez partager votre package de support généré manuellement avec le support Microsoft par e-mail.</span><span class="sxs-lookup"><span data-stu-id="41f75-131">You can share your manually generated support package with Microsoft Support over email.</span></span> <span data-ttu-id="41f75-132">Effectuer hello suivant les étapes toocreate un package de prise en charge dans Windows PowerShell pour StorSimple.</span><span class="sxs-lookup"><span data-stu-id="41f75-132">Perform hello following steps toocreate a support package in Windows PowerShell for StorSimple.</span></span>

#### <a name="toocreate-a-support-package-in-windows-powershell-for-storsimple"></a><span data-ttu-id="41f75-133">toocreate un package de prise en charge dans Windows PowerShell pour StorSimple</span><span class="sxs-lookup"><span data-stu-id="41f75-133">toocreate a support package in Windows PowerShell for StorSimple</span></span>
1. <span data-ttu-id="41f75-134">toostart une session Windows PowerShell en tant qu’administrateur sur l’ordinateur distant hello qui a utilisé l’appareil StorSimple tooconnect tooyour, entrez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="41f75-134">toostart a Windows PowerShell session as an administrator on hello remote computer that's used tooconnect tooyour StorSimple device, enter hello following command:</span></span>
   
    `Start PowerShell`
2. <span data-ttu-id="41f75-135">Dans la session Windows PowerShell de hello, connectez-vous toohello SSAdmin Console de votre appareil :</span><span class="sxs-lookup"><span data-stu-id="41f75-135">In hello Windows PowerShell session, connect toohello SSAdmin Console of your device:</span></span>
   
   * <span data-ttu-id="41f75-136">À l’invite de commandes hello, entrez :</span><span class="sxs-lookup"><span data-stu-id="41f75-136">At hello command prompt, enter:</span></span>
     
       `$MS = New-PSSession -ComputerName <IP address for DATA 0> -Credential SSAdmin -ConfigurationName "SSAdminConsole"`
   * <span data-ttu-id="41f75-137">Dans la boîte de dialogue hello qui s’ouvre, entrez votre mot de passe administrateur.</span><span class="sxs-lookup"><span data-stu-id="41f75-137">In hello dialog box that opens, enter your device administrator password.</span></span> <span data-ttu-id="41f75-138">mot de passe par défaut Hello est la suivante :</span><span class="sxs-lookup"><span data-stu-id="41f75-138">hello default password is:</span></span>
     
      `Password1`
     
      ![Boîte de dialogue des informations d’identification PowerShell](./media/storsimple-create-manage-support-package/IC740962.png)
   * <span data-ttu-id="41f75-140">Sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="41f75-140">Select **OK**.</span></span>
   * <span data-ttu-id="41f75-141">À l’invite de commandes hello, entrez :</span><span class="sxs-lookup"><span data-stu-id="41f75-141">At hello command prompt, enter:</span></span>
     
      `Enter-PSSession $MS`
3. <span data-ttu-id="41f75-142">Dans session hello qui s’ouvre, entrez la commande appropriée hello.</span><span class="sxs-lookup"><span data-stu-id="41f75-142">In hello session that opens, enter hello appropriate command.</span></span>
   
   * <span data-ttu-id="41f75-143">Pour les partages réseau protégés par un mot de passe, saisissez :</span><span class="sxs-lookup"><span data-stu-id="41f75-143">For network shares that are password protected, enter:</span></span>
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" –Credential "Username" -Force`
     
       <span data-ttu-id="41f75-144">Vous êtes invité à entrer pour un mot de passe, un dossier partagé du réseau toohello chemin d’accès et un mot de passe de chiffrement (car le package de prise en charge hello est chiffré).</span><span class="sxs-lookup"><span data-stu-id="41f75-144">You'll be prompted for a password, a path toohello network shared folder, and an encryption passphrase (because hello support package is encrypted).</span></span> <span data-ttu-id="41f75-145">Un package de prise en charge est ensuite créé dans le dossier spécifié de hello.</span><span class="sxs-lookup"><span data-stu-id="41f75-145">A support package is then created in hello specified folder.</span></span>
   * <span data-ttu-id="41f75-146">Pour les partages qui ne sont pas protégé par mot de passe, vous n’avez pas besoin hello `-Credential` paramètre.</span><span class="sxs-lookup"><span data-stu-id="41f75-146">For shares that are not password protected, you do not need hello `-Credential` parameter.</span></span> <span data-ttu-id="41f75-147">Entrez hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="41f75-147">Enter hello following:</span></span>
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" -Force`
     
       <span data-ttu-id="41f75-148">package de prise en charge Hello est créé pour les deux contrôleurs dans le dossier partagé du réseau spécifié hello.</span><span class="sxs-lookup"><span data-stu-id="41f75-148">hello support package is created for both controllers in hello specified network shared folder.</span></span> <span data-ttu-id="41f75-149">Il s’agit d’un fichier chiffré et compressé, qui peut être envoyé tooMicrosoft prise en charge pour le dépannage.</span><span class="sxs-lookup"><span data-stu-id="41f75-149">It's an encrypted, compressed file that can be sent tooMicrosoft Support for troubleshooting.</span></span> <span data-ttu-id="41f75-150">Pour plus d'informations, consultez [Contacter le support technique de Microsoft](storsimple-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="41f75-150">For more information, see [Contact Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>

### <a name="hello-export-hcssupportpackage-cmdlet-parameters"></a><span data-ttu-id="41f75-151">Hello des paramètres d’applet de commande Export-HcsSupportPackage</span><span class="sxs-lookup"><span data-stu-id="41f75-151">hello Export-HcsSupportPackage cmdlet parameters</span></span>
<span data-ttu-id="41f75-152">Vous pouvez utiliser hello paramètres avec l’applet de commande Export-HcsSupportPackage de hello suivants.</span><span class="sxs-lookup"><span data-stu-id="41f75-152">You can use hello following parameters with hello Export-HcsSupportPackage cmdlet.</span></span>

| <span data-ttu-id="41f75-153">Paramètre</span><span class="sxs-lookup"><span data-stu-id="41f75-153">Parameter</span></span> | <span data-ttu-id="41f75-154">Obligatoire ou facultatif</span><span class="sxs-lookup"><span data-stu-id="41f75-154">Required/Optional</span></span> | <span data-ttu-id="41f75-155">Description</span><span class="sxs-lookup"><span data-stu-id="41f75-155">Description</span></span> |
| --- | --- | --- |
| `-Path` |<span data-ttu-id="41f75-156">Requis</span><span class="sxs-lookup"><span data-stu-id="41f75-156">Required</span></span> |<span data-ttu-id="41f75-157">Utilisez emplacement de hello tooprovide du dossier partagé sur le réseau hello dans le hello package de prise en charge est placé.</span><span class="sxs-lookup"><span data-stu-id="41f75-157">Use tooprovide hello location of hello network shared folder in which hello support package is placed.</span></span> |
| `-EncryptionPassphrase` |<span data-ttu-id="41f75-158">Requis</span><span class="sxs-lookup"><span data-stu-id="41f75-158">Required</span></span> |<span data-ttu-id="41f75-159">Utilisez tooprovide une phrase secrète de toohelp chiffrer hello prise en charge du package.</span><span class="sxs-lookup"><span data-stu-id="41f75-159">Use tooprovide a passphrase toohelp encrypt hello support package.</span></span> |
| `-Credential` |<span data-ttu-id="41f75-160">Facultatif</span><span class="sxs-lookup"><span data-stu-id="41f75-160">Optional</span></span> |<span data-ttu-id="41f75-161">Utilisez toosupply informations d’identification pour le dossier partagé du réseau hello.</span><span class="sxs-lookup"><span data-stu-id="41f75-161">Use toosupply access credentials for hello network shared folder.</span></span> |
| `-Force` |<span data-ttu-id="41f75-162">Facultatif</span><span class="sxs-lookup"><span data-stu-id="41f75-162">Optional</span></span> |<span data-ttu-id="41f75-163">Utilisez l’étape de confirmation de phrase secrète tooskip hello chiffrement.</span><span class="sxs-lookup"><span data-stu-id="41f75-163">Use tooskip hello encryption passphrase confirmation step.</span></span> |
| `-PackageTag` |<span data-ttu-id="41f75-164">Facultatif</span><span class="sxs-lookup"><span data-stu-id="41f75-164">Optional</span></span> |<span data-ttu-id="41f75-165">Utilisez toospecify un répertoire sous *chemin d’accès* prise en charge hello package est placé.</span><span class="sxs-lookup"><span data-stu-id="41f75-165">Use toospecify a directory under *Path* in which hello support package is placed.</span></span> <span data-ttu-id="41f75-166">valeur par défaut Hello est [nom appareil]-[date et actuelles : dd-mm-aaaa-hh-mm-ss].</span><span class="sxs-lookup"><span data-stu-id="41f75-166">hello default is [device name]-[current date and time:yyyy-MM-dd-HH-mm-ss].</span></span> |
| `-Scope` |<span data-ttu-id="41f75-167">Facultatif</span><span class="sxs-lookup"><span data-stu-id="41f75-167">Optional</span></span> |<span data-ttu-id="41f75-168">Spécifiez en tant que **Cluster** (par défaut), toocreate un package de prise en charge pour les deux contrôleurs.</span><span class="sxs-lookup"><span data-stu-id="41f75-168">Specify as **Cluster** (default) toocreate a support package for both controllers.</span></span> <span data-ttu-id="41f75-169">Si vous souhaitez toocreate un package uniquement pour le contrôleur actuel de hello, spécifiez **contrôleur**.</span><span class="sxs-lookup"><span data-stu-id="41f75-169">If you want toocreate a package only for hello current controller, specify **Controller**.</span></span> |

## <a name="edit-a-support-package"></a><span data-ttu-id="41f75-170">Modification d'un package de support</span><span class="sxs-lookup"><span data-stu-id="41f75-170">Edit a support package</span></span>
<span data-ttu-id="41f75-171">Une fois que vous avez généré un package de prise en charge, vous devrez peut-être des informations sensibles tooedit hello package tooremove.</span><span class="sxs-lookup"><span data-stu-id="41f75-171">After you have generated a support package, you might need tooedit hello package tooremove sensitive information.</span></span> <span data-ttu-id="41f75-172">Cela peut inclure les noms de volume, adresses IP d’appareil et sauvegarde des fichiers de journaux hello.</span><span class="sxs-lookup"><span data-stu-id="41f75-172">This can include volume names, device IP addresses, and backup names from hello log files.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="41f75-173">Vous pouvez uniquement modifier un package de support qui a été généré à l'aide de Windows PowerShell pour StorSimple.</span><span class="sxs-lookup"><span data-stu-id="41f75-173">You can only edit a support package that was generated through Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="41f75-174">Vous ne pouvez pas modifier un package créé dans hello portail classique Azure avec le service StorSimple Manager.</span><span class="sxs-lookup"><span data-stu-id="41f75-174">You can't edit a package created in hello Azure classic portal with StorSimple Manager service.</span></span>
> 
> 

<span data-ttu-id="41f75-175">tooedit un package de support avant de le télécharger sur le site de Support technique de Microsoft hello, package de support hello d’abord le déchiffrer, modifier des fichiers de hello, puis le rechiffrer.</span><span class="sxs-lookup"><span data-stu-id="41f75-175">tooedit a support package before uploading it on hello Microsoft Support site, first decrypt hello support package, edit hello files, and then re-encrypt it.</span></span> <span data-ttu-id="41f75-176">Effectuer hello comme suit.</span><span class="sxs-lookup"><span data-stu-id="41f75-176">Perform hello following steps.</span></span>

#### <a name="tooedit-a-support-package-in-windows-powershell-for-storsimple"></a><span data-ttu-id="41f75-177">tooedit un package de prise en charge dans Windows PowerShell pour StorSimple</span><span class="sxs-lookup"><span data-stu-id="41f75-177">tooedit a support package in Windows PowerShell for StorSimple</span></span>
1. <span data-ttu-id="41f75-178">Générer un package de prise en charge, comme décrit dans les versions antérieures, [toocreate un package de prise en charge dans Windows PowerShell pour StorSimple](#to-create-a-support-package-in-windows-powershell-for-storsimple).</span><span class="sxs-lookup"><span data-stu-id="41f75-178">Generate a support package as described earlier, in [toocreate a support package in Windows PowerShell for StorSimple](#to-create-a-support-package-in-windows-powershell-for-storsimple).</span></span>
2. <span data-ttu-id="41f75-179">[Télécharger le script de hello](http://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) localement sur votre client.</span><span class="sxs-lookup"><span data-stu-id="41f75-179">[Download hello script](http://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) locally on your client.</span></span>
3. <span data-ttu-id="41f75-180">Importez le module Windows PowerShell de hello.</span><span class="sxs-lookup"><span data-stu-id="41f75-180">Import hello Windows PowerShell module.</span></span> <span data-ttu-id="41f75-181">Spécifiez hello chemin d’accès toohello dossier local dans lequel vous avez téléchargé le script de hello.</span><span class="sxs-lookup"><span data-stu-id="41f75-181">Specify hello path toohello local folder in which you downloaded hello script.</span></span> <span data-ttu-id="41f75-182">module de hello tooimport, entrez :</span><span class="sxs-lookup"><span data-stu-id="41f75-182">tooimport hello module, enter:</span></span>
   
    `Import-module <Path toohello folder that contains hello Windows PowerShell script>`
4. <span data-ttu-id="41f75-183">Tous les fichiers de hello sont *.aes* fichiers compressés et chiffrés.</span><span class="sxs-lookup"><span data-stu-id="41f75-183">All hello files are *.aes* files that are compressed and encrypted.</span></span> <span data-ttu-id="41f75-184">toodecompress et déchiffrer les fichiers, entrez :</span><span class="sxs-lookup"><span data-stu-id="41f75-184">toodecompress and decrypt files, enter:</span></span>
   
    `Open-HcsSupportPackage <Path toohello folder that contains support package files>`
   
    <span data-ttu-id="41f75-185">Notez que les extensions de fichier réel hello sont maintenant affichées pour tous les fichiers hello.</span><span class="sxs-lookup"><span data-stu-id="41f75-185">Note that hello actual file extensions are now displayed for all hello files.</span></span>
   
    ![Modifier un package de support](./media/storsimple-create-manage-support-package/IC750706.png)
5. <span data-ttu-id="41f75-187">Lorsque vous êtes invité à entrer hello phrase secrète de chiffrement, entrez la phrase secrète hello que vous avez utilisé lors de la création de package de support hello.</span><span class="sxs-lookup"><span data-stu-id="41f75-187">When you're prompted for hello encryption passphrase, enter hello passphrase that you used when hello support package was created.</span></span>
   
        cmdlet Open-HcsSupportPackage at command pipeline position 1
   
        Supply values for hello following parameters:EncryptionPassphrase: ****
6. <span data-ttu-id="41f75-188">Parcourir un dossier toohello qui contient les fichiers journaux hello.</span><span class="sxs-lookup"><span data-stu-id="41f75-188">Browse toohello folder that contains hello log files.</span></span> <span data-ttu-id="41f75-189">Hello fichiers journaux sont désormais décompressés et déchiffrés, il aura donc des extensions de fichier d’origine.</span><span class="sxs-lookup"><span data-stu-id="41f75-189">Because hello log files are now decompressed and decrypted, these will have original file extensions.</span></span> <span data-ttu-id="41f75-190">Modifier ces tooremove fichiers toutes les informations spécifiques au client, telles que les noms de volume et les adresses IP d’appareil et enregistrez les fichiers de hello.</span><span class="sxs-lookup"><span data-stu-id="41f75-190">Modify these files tooremove any customer-specific information, such as volume names and device IP addresses, and save hello files.</span></span>
7. <span data-ttu-id="41f75-191">Hello fermer les fichiers toocompress avec gzip et leur chiffrement avec AES-256.</span><span class="sxs-lookup"><span data-stu-id="41f75-191">Close hello files toocompress them with gzip and encrypt them with AES-256.</span></span> <span data-ttu-id="41f75-192">Il s’agit de la vitesse et de sécurité lors du transfert du package de support hello sur un réseau.</span><span class="sxs-lookup"><span data-stu-id="41f75-192">This is for speed and security in transferring hello support package over a network.</span></span> <span data-ttu-id="41f75-193">toocompress et chiffrer des fichiers, entrez hello suivante :</span><span class="sxs-lookup"><span data-stu-id="41f75-193">toocompress and encrypt files, enter hello following:</span></span>
   
    `Close-HcsSupportPackage <Path toohello folder that contains support package files>`
   
    ![Modifier un package de support](./media/storsimple-create-manage-support-package/IC750707.png)
8. <span data-ttu-id="41f75-195">Lorsque vous y êtes invité, fournissez une phrase secrète de chiffrement pour le package de prise en charge modifié hello.</span><span class="sxs-lookup"><span data-stu-id="41f75-195">When prompted, provide an encryption passphrase for hello modified support package.</span></span>
   
        cmdlet Close-HcsSupportPackage at command pipeline position 1
        Supply values for hello following parameters:EncryptionPassphrase: ****
9. <span data-ttu-id="41f75-196">Écrivez hello nouvelle phrase secrète, afin que vous pouvez le partager avec le Support technique de Microsoft lorsqu’il est demandé.</span><span class="sxs-lookup"><span data-stu-id="41f75-196">Write down hello new passphrase, so that you can share it with Microsoft Support when requested.</span></span>

### <a name="example-editing-files-in-a-support-package-on-a-password-protected-share"></a><span data-ttu-id="41f75-197">Exemple : Modification de fichiers dans un package de support sur un partage protégé par mot de passe</span><span class="sxs-lookup"><span data-stu-id="41f75-197">Example: Editing files in a support package on a password-protected share</span></span>
<span data-ttu-id="41f75-198">Bonjour à l’exemple suivant montre comment toodecrypt, modifier et rechiffrer un package de prise en charge.</span><span class="sxs-lookup"><span data-stu-id="41f75-198">hello following example shows how toodecrypt, edit, and re-encrypt a support package.</span></span>

        PS C:\WINDOWS\system32> Import-module C:\Users\Default\StorSimple\SupportPackage\HCSSupportPackageTools.psm1

        PS C:\WINDOWS\system32> Open-HcsSupportPackage \\hcsfs\Logs\TD48\TD48Logs\C0-A\etw

        cmdlet Open-HcsSupportPackage at command pipeline position 1

        Supply values for hello following parameters:

        EncryptionPassphrase: ****

        PS C:\WINDOWS\system32> Close-HcsSupportPackage \\hcsfs\Logs\TD48\TD48Logs\C0-A\etw

        cmdlet Close-HcsSupportPackage at command pipeline position 1

        Supply values for hello following parameters:

        EncryptionPassphrase: ****

        PS C:\WINDOWS\system32>

## <a name="next-steps"></a><span data-ttu-id="41f75-199">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="41f75-199">Next steps</span></span>
* <span data-ttu-id="41f75-200">Découvrez comment trop[utilisation prise en charge de packages et périphérique se connecte tootroubleshoot votre déploiement de périphérique](storsimple-troubleshoot-deployment.md#support-packages-and-device-logs-available-for-troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="41f75-200">Learn how too[use support packages and device logs tootroubleshoot your device deployment](storsimple-troubleshoot-deployment.md#support-packages-and-device-logs-available-for-troubleshooting).</span></span>
* <span data-ttu-id="41f75-201">Découvrez comment trop[utilisez hello tooadminister du service StorSimple Manager de votre appareil StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="41f75-201">Learn how too[use hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

