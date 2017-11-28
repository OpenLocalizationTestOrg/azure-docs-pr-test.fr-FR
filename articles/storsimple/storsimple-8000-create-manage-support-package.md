---
title: package de support aaaCreate un StorSimple 8000 series | Documents Microsoft
description: "Découvrez comment toocreate, déchiffrer et modifier un package de prise en charge pour votre appareil de série StorSimple 8000."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/05/2017
ms.author: alkohli
ms.openlocfilehash: 857555b6ba31b1527f8f00d19818ebbec6005d0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-a-support-package-for-storsimple-8000-series"></a><span data-ttu-id="e3213-103">Création et gestion d’un package de prise en charge pour la gamme StorSimple 8000</span><span class="sxs-lookup"><span data-stu-id="e3213-103">Create and manage a support package for StorSimple 8000 series</span></span>

## <a name="overview"></a><span data-ttu-id="e3213-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="e3213-104">Overview</span></span>

<span data-ttu-id="e3213-105">Un package de prise en charge de StorSimple est un mécanisme facile à utiliser qui collecte tous les journaux appropriés tooassist Support technique de Microsoft à résoudre les problèmes de votre appareil StorSimple.</span><span class="sxs-lookup"><span data-stu-id="e3213-105">A StorSimple support package is an easy-to-use mechanism that collects all relevant logs tooassist Microsoft Support with troubleshooting any StorSimple device issues.</span></span> <span data-ttu-id="e3213-106">Hello fichiers journaux collectés sont chiffrés et compressés.</span><span class="sxs-lookup"><span data-stu-id="e3213-106">hello collected logs are encrypted and compressed.</span></span>

<span data-ttu-id="e3213-107">Ce didacticiel inclut des instructions pas à pas toocreate et à gérer hello prise en charge pour votre appareil de série StorSimple 8000.</span><span class="sxs-lookup"><span data-stu-id="e3213-107">This tutorial includes step-by-step instructions toocreate and manage hello support package for your StorSimple 8000 series device.</span></span> <span data-ttu-id="e3213-108">Si vous travaillez avec un tableau virtuel StorSimple, passez trop[générer un package de journaux](storsimple-ova-web-ui-admin.md#generate-a-log-package).</span><span class="sxs-lookup"><span data-stu-id="e3213-108">If you are working with a StorSimple Virtual Array, go too[generate a log package](storsimple-ova-web-ui-admin.md#generate-a-log-package).</span></span>

## <a name="create-a-support-package"></a><span data-ttu-id="e3213-109">Création d’un package de prise en charge</span><span class="sxs-lookup"><span data-stu-id="e3213-109">Create a support package</span></span>

<span data-ttu-id="e3213-110">Dans certains cas, vous devez toomanually créer le package de prise en charge de hello via Windows PowerShell pour StorSimple.</span><span class="sxs-lookup"><span data-stu-id="e3213-110">In some cases, you'll need toomanually create hello support package through Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="e3213-111">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="e3213-111">For example:</span></span>

* <span data-ttu-id="e3213-112">Si vous avez besoin des informations sensibles tooremove à partir de votre journal des fichiers préalable toosharing avec le Support technique de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e3213-112">If you need tooremove sensitive information from your log files prior toosharing with Microsoft Support.</span></span>
* <span data-ttu-id="e3213-113">Si vous avez des difficultés à télécharger le package hello en raison de problèmes de tooconnectivity.</span><span class="sxs-lookup"><span data-stu-id="e3213-113">If you are having difficulty uploading hello package due tooconnectivity issues.</span></span>

<span data-ttu-id="e3213-114">Vous pouvez partager votre package de support généré manuellement avec le support Microsoft par e-mail.</span><span class="sxs-lookup"><span data-stu-id="e3213-114">You can share your manually generated support package with Microsoft Support over email.</span></span> <span data-ttu-id="e3213-115">Effectuer hello suivant les étapes toocreate un package de prise en charge dans Windows PowerShell pour StorSimple.</span><span class="sxs-lookup"><span data-stu-id="e3213-115">Perform hello following steps toocreate a support package in Windows PowerShell for StorSimple.</span></span>

#### <a name="toocreate-a-support-package-in-windows-powershell-for-storsimple"></a><span data-ttu-id="e3213-116">toocreate un package de prise en charge dans Windows PowerShell pour StorSimple</span><span class="sxs-lookup"><span data-stu-id="e3213-116">toocreate a support package in Windows PowerShell for StorSimple</span></span>

1. <span data-ttu-id="e3213-117">toostart une session Windows PowerShell en tant qu’administrateur sur l’ordinateur distant hello qui a utilisé l’appareil StorSimple tooconnect tooyour, entrez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="e3213-117">toostart a Windows PowerShell session as an administrator on hello remote computer that's used tooconnect tooyour StorSimple device, enter hello following command:</span></span>
   
    `Start PowerShell`
2. <span data-ttu-id="e3213-118">Dans la session Windows PowerShell de hello, connectez-vous toohello SSAdmin Console de votre appareil :</span><span class="sxs-lookup"><span data-stu-id="e3213-118">In hello Windows PowerShell session, connect toohello SSAdmin Console of your device:</span></span>
   
   1. <span data-ttu-id="e3213-119">À l’invite de commandes hello, entrez :</span><span class="sxs-lookup"><span data-stu-id="e3213-119">At hello command prompt, enter:</span></span>
     
       `$MS = New-PSSession -ComputerName <IP address for DATA 0> -Credential SSAdmin -ConfigurationName "SSAdminConsole"`
   2. <span data-ttu-id="e3213-120">Dans la boîte de dialogue hello qui s’ouvre, entrez votre mot de passe administrateur.</span><span class="sxs-lookup"><span data-stu-id="e3213-120">In hello dialog box that opens, enter your device administrator password.</span></span> <span data-ttu-id="e3213-121">mot de passe Hello _Password1_.</span><span class="sxs-lookup"><span data-stu-id="e3213-121">hello default password is _Password1_.</span></span>
     
      ![Boîte de dialogue des informations d’identification PowerShell](./media/storsimple-8000-create-manage-support-package/IC740962.png)
   3. <span data-ttu-id="e3213-123">Sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="e3213-123">Select **OK**.</span></span>
   4. <span data-ttu-id="e3213-124">À l’invite de commandes hello, entrez :</span><span class="sxs-lookup"><span data-stu-id="e3213-124">At hello command prompt, enter:</span></span>
     
      `Enter-PSSession $MS`
3. <span data-ttu-id="e3213-125">Dans session hello qui s’ouvre, entrez la commande appropriée hello.</span><span class="sxs-lookup"><span data-stu-id="e3213-125">In hello session that opens, enter hello appropriate command.</span></span>
   
   * <span data-ttu-id="e3213-126">Pour les partages réseau protégés par un mot de passe, saisissez :</span><span class="sxs-lookup"><span data-stu-id="e3213-126">For network shares that are password protected, enter:</span></span>
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" –Credential "Username" -Force`
     
       <span data-ttu-id="e3213-127">Vous êtes invité à entrer pour un mot de passe, un dossier partagé du réseau toohello chemin d’accès et un mot de passe de chiffrement (car le package de prise en charge hello est chiffré).</span><span class="sxs-lookup"><span data-stu-id="e3213-127">You'll be prompted for a password, a path toohello network shared folder, and an encryption passphrase (because hello support package is encrypted).</span></span> <span data-ttu-id="e3213-128">Un package de prise en charge est ensuite créé dans le dossier spécifié de hello.</span><span class="sxs-lookup"><span data-stu-id="e3213-128">A support package is then created in hello specified folder.</span></span>
   * <span data-ttu-id="e3213-129">Pour les partages qui ne sont pas protégé par mot de passe, vous n’avez pas besoin hello `-Credential` paramètre.</span><span class="sxs-lookup"><span data-stu-id="e3213-129">For shares that are not password protected, you do not need hello `-Credential` parameter.</span></span> <span data-ttu-id="e3213-130">Entrez hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="e3213-130">Enter hello following:</span></span>
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" -Force`
     
       <span data-ttu-id="e3213-131">package de prise en charge Hello est créé pour les deux contrôleurs dans le dossier partagé du réseau spécifié hello.</span><span class="sxs-lookup"><span data-stu-id="e3213-131">hello support package is created for both controllers in hello specified network shared folder.</span></span> <span data-ttu-id="e3213-132">Il s’agit d’un fichier chiffré et compressé, qui peut être envoyé tooMicrosoft prise en charge pour le dépannage.</span><span class="sxs-lookup"><span data-stu-id="e3213-132">It's an encrypted, compressed file that can be sent tooMicrosoft Support for troubleshooting.</span></span> <span data-ttu-id="e3213-133">Pour plus d'informations, consultez [Contacter le support technique de Microsoft](storsimple-8000-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="e3213-133">For more information, see [Contact Microsoft Support](storsimple-8000-contact-microsoft-support.md).</span></span>

### <a name="hello-export-hcssupportpackage-cmdlet-parameters"></a><span data-ttu-id="e3213-134">Hello des paramètres d’applet de commande Export-HcsSupportPackage</span><span class="sxs-lookup"><span data-stu-id="e3213-134">hello Export-HcsSupportPackage cmdlet parameters</span></span>

<span data-ttu-id="e3213-135">Vous pouvez utiliser hello paramètres avec l’applet de commande Export-HcsSupportPackage de hello suivants.</span><span class="sxs-lookup"><span data-stu-id="e3213-135">You can use hello following parameters with hello Export-HcsSupportPackage cmdlet.</span></span>

| <span data-ttu-id="e3213-136">Paramètre</span><span class="sxs-lookup"><span data-stu-id="e3213-136">Parameter</span></span> | <span data-ttu-id="e3213-137">Obligatoire ou facultatif</span><span class="sxs-lookup"><span data-stu-id="e3213-137">Required/Optional</span></span> | <span data-ttu-id="e3213-138">Description</span><span class="sxs-lookup"><span data-stu-id="e3213-138">Description</span></span> |
| --- | --- | --- |
| `-Path` |<span data-ttu-id="e3213-139">Requis</span><span class="sxs-lookup"><span data-stu-id="e3213-139">Required</span></span> |<span data-ttu-id="e3213-140">Utilisez emplacement de hello tooprovide du dossier partagé sur le réseau hello dans le hello package de prise en charge est placé.</span><span class="sxs-lookup"><span data-stu-id="e3213-140">Use tooprovide hello location of hello network shared folder in which hello support package is placed.</span></span> |
| `-EncryptionPassphrase` |<span data-ttu-id="e3213-141">Requis</span><span class="sxs-lookup"><span data-stu-id="e3213-141">Required</span></span> |<span data-ttu-id="e3213-142">Utilisez tooprovide une phrase secrète de toohelp chiffrer hello prise en charge du package.</span><span class="sxs-lookup"><span data-stu-id="e3213-142">Use tooprovide a passphrase toohelp encrypt hello support package.</span></span> |
| `-Credential` |<span data-ttu-id="e3213-143">Facultatif</span><span class="sxs-lookup"><span data-stu-id="e3213-143">Optional</span></span> |<span data-ttu-id="e3213-144">Utilisez toosupply informations d’identification pour le dossier partagé du réseau hello.</span><span class="sxs-lookup"><span data-stu-id="e3213-144">Use toosupply access credentials for hello network shared folder.</span></span> |
| `-Force` |<span data-ttu-id="e3213-145">Facultatif</span><span class="sxs-lookup"><span data-stu-id="e3213-145">Optional</span></span> |<span data-ttu-id="e3213-146">Utilisez l’étape de confirmation de phrase secrète tooskip hello chiffrement.</span><span class="sxs-lookup"><span data-stu-id="e3213-146">Use tooskip hello encryption passphrase confirmation step.</span></span> |
| `-PackageTag` |<span data-ttu-id="e3213-147">Facultatif</span><span class="sxs-lookup"><span data-stu-id="e3213-147">Optional</span></span> |<span data-ttu-id="e3213-148">Utilisez toospecify un répertoire sous *chemin d’accès* prise en charge hello package est placé.</span><span class="sxs-lookup"><span data-stu-id="e3213-148">Use toospecify a directory under *Path* in which hello support package is placed.</span></span> <span data-ttu-id="e3213-149">valeur par défaut Hello est [nom appareil]-[date et actuelles : dd-mm-aaaa-hh-mm-ss].</span><span class="sxs-lookup"><span data-stu-id="e3213-149">hello default is [device name]-[current date and time:yyyy-MM-dd-HH-mm-ss].</span></span> |
| `-Scope` |<span data-ttu-id="e3213-150">Facultatif</span><span class="sxs-lookup"><span data-stu-id="e3213-150">Optional</span></span> |<span data-ttu-id="e3213-151">Spécifiez en tant que **Cluster** (par défaut), toocreate un package de prise en charge pour les deux contrôleurs.</span><span class="sxs-lookup"><span data-stu-id="e3213-151">Specify as **Cluster** (default) toocreate a support package for both controllers.</span></span> <span data-ttu-id="e3213-152">Si vous souhaitez toocreate un package uniquement pour le contrôleur actuel de hello, spécifiez **contrôleur**.</span><span class="sxs-lookup"><span data-stu-id="e3213-152">If you want toocreate a package only for hello current controller, specify **Controller**.</span></span> |

## <a name="edit-a-support-package"></a><span data-ttu-id="e3213-153">Modification d'un package de support</span><span class="sxs-lookup"><span data-stu-id="e3213-153">Edit a support package</span></span>

<span data-ttu-id="e3213-154">Une fois que vous avez généré un package de prise en charge, vous devrez peut-être des informations sensibles tooedit hello package tooremove.</span><span class="sxs-lookup"><span data-stu-id="e3213-154">After you have generated a support package, you might need tooedit hello package tooremove sensitive information.</span></span> <span data-ttu-id="e3213-155">Cela peut inclure les noms de volume, adresses IP d’appareil et sauvegarde des fichiers de journaux hello.</span><span class="sxs-lookup"><span data-stu-id="e3213-155">This can include volume names, device IP addresses, and backup names from hello log files.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e3213-156">Vous pouvez uniquement modifier un package de support qui a été généré à l'aide de Windows PowerShell pour StorSimple.</span><span class="sxs-lookup"><span data-stu-id="e3213-156">You can only edit a support package that was generated through Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="e3213-157">Vous ne pouvez pas modifier un package créé dans hello portail Azure avec le service du Gestionnaire de périphériques StorSimple.</span><span class="sxs-lookup"><span data-stu-id="e3213-157">You can't edit a package created in hello Azure portal with StorSimple Device Manager service.</span></span>

<span data-ttu-id="e3213-158">tooedit un package de support avant de le télécharger sur le site de Support technique de Microsoft hello, package de support hello d’abord le déchiffrer, modifier des fichiers de hello, puis le rechiffrer.</span><span class="sxs-lookup"><span data-stu-id="e3213-158">tooedit a support package before uploading it on hello Microsoft Support site, first decrypt hello support package, edit hello files, and then re-encrypt it.</span></span> <span data-ttu-id="e3213-159">Effectuer hello comme suit.</span><span class="sxs-lookup"><span data-stu-id="e3213-159">Perform hello following steps.</span></span>

#### <a name="tooedit-a-support-package-in-windows-powershell-for-storsimple"></a><span data-ttu-id="e3213-160">tooedit un package de prise en charge dans Windows PowerShell pour StorSimple</span><span class="sxs-lookup"><span data-stu-id="e3213-160">tooedit a support package in Windows PowerShell for StorSimple</span></span>

1. <span data-ttu-id="e3213-161">Générer un package de prise en charge, comme décrit dans les versions antérieures, [toocreate un package de prise en charge dans Windows PowerShell pour StorSimple](#to-create-a-support-package-in-windows-powershell-for-storsimple).</span><span class="sxs-lookup"><span data-stu-id="e3213-161">Generate a support package as described earlier, in [toocreate a support package in Windows PowerShell for StorSimple](#to-create-a-support-package-in-windows-powershell-for-storsimple).</span></span>
2. <span data-ttu-id="e3213-162">[Télécharger le script de hello](http://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) localement sur votre client.</span><span class="sxs-lookup"><span data-stu-id="e3213-162">[Download hello script](http://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) locally on your client.</span></span>
3. <span data-ttu-id="e3213-163">Importez le module Windows PowerShell de hello.</span><span class="sxs-lookup"><span data-stu-id="e3213-163">Import hello Windows PowerShell module.</span></span> <span data-ttu-id="e3213-164">Spécifiez hello chemin d’accès toohello dossier local dans lequel vous avez téléchargé le script de hello.</span><span class="sxs-lookup"><span data-stu-id="e3213-164">Specify hello path toohello local folder in which you downloaded hello script.</span></span> <span data-ttu-id="e3213-165">module de hello tooimport, entrez :</span><span class="sxs-lookup"><span data-stu-id="e3213-165">tooimport hello module, enter:</span></span>
   
    `Import-module <Path toohello folder that contains hello Windows PowerShell script>`
4. <span data-ttu-id="e3213-166">Tous les fichiers de hello sont *.aes* fichiers compressés et chiffrés.</span><span class="sxs-lookup"><span data-stu-id="e3213-166">All hello files are *.aes* files that are compressed and encrypted.</span></span> <span data-ttu-id="e3213-167">toodecompress et déchiffrer les fichiers, entrez :</span><span class="sxs-lookup"><span data-stu-id="e3213-167">toodecompress and decrypt files, enter:</span></span>
   
    `Open-HcsSupportPackage <Path toohello folder that contains support package files>`
   
    <span data-ttu-id="e3213-168">Notez que les extensions de fichier réel hello sont maintenant affichées pour tous les fichiers hello.</span><span class="sxs-lookup"><span data-stu-id="e3213-168">Note that hello actual file extensions are now displayed for all hello files.</span></span>
   
    ![Modifier un package de support](./media/storsimple-8000-create-manage-support-package/IC750706.png)
5. <span data-ttu-id="e3213-170">Lorsque vous êtes invité à entrer hello phrase secrète de chiffrement, entrez la phrase secrète hello que vous avez utilisé lors de la création de package de support hello.</span><span class="sxs-lookup"><span data-stu-id="e3213-170">When you're prompted for hello encryption passphrase, enter hello passphrase that you used when hello support package was created.</span></span>
   
        cmdlet Open-HcsSupportPackage at command pipeline position 1
   
        Supply values for hello following parameters:EncryptionPassphrase: ****
6. <span data-ttu-id="e3213-171">Parcourir un dossier toohello qui contient les fichiers journaux hello.</span><span class="sxs-lookup"><span data-stu-id="e3213-171">Browse toohello folder that contains hello log files.</span></span> <span data-ttu-id="e3213-172">Hello fichiers journaux sont désormais décompressés et déchiffrés, il aura donc des extensions de fichier d’origine.</span><span class="sxs-lookup"><span data-stu-id="e3213-172">Because hello log files are now decompressed and decrypted, these will have original file extensions.</span></span> <span data-ttu-id="e3213-173">Modifier ces tooremove fichiers toutes les informations spécifiques au client, telles que les noms de volume et les adresses IP d’appareil et enregistrez les fichiers de hello.</span><span class="sxs-lookup"><span data-stu-id="e3213-173">Modify these files tooremove any customer-specific information, such as volume names and device IP addresses, and save hello files.</span></span>
7. <span data-ttu-id="e3213-174">Hello fermer les fichiers toocompress avec gzip et leur chiffrement avec AES-256.</span><span class="sxs-lookup"><span data-stu-id="e3213-174">Close hello files toocompress them with gzip and encrypt them with AES-256.</span></span> <span data-ttu-id="e3213-175">Il s’agit de la vitesse et de sécurité lors du transfert du package de support hello sur un réseau.</span><span class="sxs-lookup"><span data-stu-id="e3213-175">This is for speed and security in transferring hello support package over a network.</span></span> <span data-ttu-id="e3213-176">toocompress et chiffrer des fichiers, entrez hello suivante :</span><span class="sxs-lookup"><span data-stu-id="e3213-176">toocompress and encrypt files, enter hello following:</span></span>
   
    `Close-HcsSupportPackage <Path toohello folder that contains support package files>`
   
    ![Modifier un package de support](./media/storsimple-8000-create-manage-support-package/IC750707.png)
8. <span data-ttu-id="e3213-178">Lorsque vous y êtes invité, fournissez une phrase secrète de chiffrement pour le package de prise en charge modifié hello.</span><span class="sxs-lookup"><span data-stu-id="e3213-178">When prompted, provide an encryption passphrase for hello modified support package.</span></span>
   
        cmdlet Close-HcsSupportPackage at command pipeline position 1
        Supply values for hello following parameters:EncryptionPassphrase: ****
9. <span data-ttu-id="e3213-179">Écrivez hello nouvelle phrase secrète, afin que vous pouvez le partager avec le Support technique de Microsoft lorsqu’il est demandé.</span><span class="sxs-lookup"><span data-stu-id="e3213-179">Write down hello new passphrase, so that you can share it with Microsoft Support when requested.</span></span>

### <a name="example-editing-files-in-a-support-package-on-a-password-protected-share"></a><span data-ttu-id="e3213-180">Exemple : Modification de fichiers dans un package de support sur un partage protégé par mot de passe</span><span class="sxs-lookup"><span data-stu-id="e3213-180">Example: Editing files in a support package on a password-protected share</span></span>

<span data-ttu-id="e3213-181">Bonjour à l’exemple suivant montre comment toodecrypt, modifier et rechiffrer un package de prise en charge.</span><span class="sxs-lookup"><span data-stu-id="e3213-181">hello following example shows how toodecrypt, edit, and re-encrypt a support package.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="e3213-182">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e3213-182">Next steps</span></span>

* <span data-ttu-id="e3213-183">En savoir plus sur hello [les informations collectées dans le package de prise en charge de hello](https://support.microsoft.com/help/3193606/storsimple-support-packages-and-device-logs)</span><span class="sxs-lookup"><span data-stu-id="e3213-183">Learn about hello [information collected in hello Support package](https://support.microsoft.com/help/3193606/storsimple-support-packages-and-device-logs)</span></span>
* <span data-ttu-id="e3213-184">Découvrez comment trop[utilisation prise en charge de packages et périphérique se connecte tootroubleshoot votre déploiement de périphérique](storsimple-troubleshoot-deployment.md#support-packages-and-device-logs-available-for-troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="e3213-184">Learn how too[use support packages and device logs tootroubleshoot your device deployment](storsimple-troubleshoot-deployment.md#support-packages-and-device-logs-available-for-troubleshooting).</span></span>
* <span data-ttu-id="e3213-185">Découvrez comment trop[utilisez hello tooadminister du service Gestionnaire de périphériques StorSimple votre appareil StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="e3213-185">Learn how too[use hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

