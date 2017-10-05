---
title: "Création d’un package de prise en charge de la gamme StorSimple 8000 | Microsoft Docs"
description: "Apprenez à créer, déchiffrer et modifier un package de prise en charge pour votre appareil de la gamme StorSimple 8000."
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
ms.openlocfilehash: 92abbb96b2117e10800de61b5c405a784453265b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-a-support-package-for-storsimple-8000-series"></a><span data-ttu-id="69e0f-103">Création et gestion d’un package de prise en charge pour la gamme StorSimple 8000</span><span class="sxs-lookup"><span data-stu-id="69e0f-103">Create and manage a support package for StorSimple 8000 series</span></span>

## <a name="overview"></a><span data-ttu-id="69e0f-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="69e0f-104">Overview</span></span>

<span data-ttu-id="69e0f-105">Un package de support StorSimple est un mécanisme facile à utiliser qui collecte tous les journaux appropriés afin d’aider le support Microsoft à résoudre tout problème lié à votre appareil StorSimple.</span><span class="sxs-lookup"><span data-stu-id="69e0f-105">A StorSimple support package is an easy-to-use mechanism that collects all relevant logs to assist Microsoft Support with troubleshooting any StorSimple device issues.</span></span> <span data-ttu-id="69e0f-106">Les fichiers journaux collectés sont chiffrés et compressés.</span><span class="sxs-lookup"><span data-stu-id="69e0f-106">The collected logs are encrypted and compressed.</span></span>

<span data-ttu-id="69e0f-107">Ce didacticiel inclut des instructions détaillées pour créer et gérer le package de prise en charge de votre appareil de la gamme StorSimple 8000.</span><span class="sxs-lookup"><span data-stu-id="69e0f-107">This tutorial includes step-by-step instructions to create and manage the support package for your StorSimple 8000 series device.</span></span> <span data-ttu-id="69e0f-108">Si vous travaillez avec un tableau virtuel StorSimple, accédez à [Générer un package de journaux](storsimple-ova-web-ui-admin.md#generate-a-log-package).</span><span class="sxs-lookup"><span data-stu-id="69e0f-108">If you are working with a StorSimple Virtual Array, go to [generate a log package](storsimple-ova-web-ui-admin.md#generate-a-log-package).</span></span>

## <a name="create-a-support-package"></a><span data-ttu-id="69e0f-109">Création d’un package de prise en charge</span><span class="sxs-lookup"><span data-stu-id="69e0f-109">Create a support package</span></span>

<span data-ttu-id="69e0f-110">Dans certains cas, vous devez créer manuellement le package de support via Windows PowerShell pour StorSimple.</span><span class="sxs-lookup"><span data-stu-id="69e0f-110">In some cases, you'll need to manually create the support package through Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="69e0f-111">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="69e0f-111">For example:</span></span>

* <span data-ttu-id="69e0f-112">Si vous devez supprimer des informations sensibles de vos fichiers journaux avant de le partager avec le support Microsoft.</span><span class="sxs-lookup"><span data-stu-id="69e0f-112">If you need to remove sensitive information from your log files prior to sharing with Microsoft Support.</span></span>
* <span data-ttu-id="69e0f-113">Si vous rencontrez des difficultés à charger le package en raison de problèmes de connectivité.</span><span class="sxs-lookup"><span data-stu-id="69e0f-113">If you are having difficulty uploading the package due to connectivity issues.</span></span>

<span data-ttu-id="69e0f-114">Vous pouvez partager votre package de support généré manuellement avec le support Microsoft par e-mail.</span><span class="sxs-lookup"><span data-stu-id="69e0f-114">You can share your manually generated support package with Microsoft Support over email.</span></span> <span data-ttu-id="69e0f-115">Procédez comme suit pour créer un package de support dans Windows PowerShell pour StorSimple.</span><span class="sxs-lookup"><span data-stu-id="69e0f-115">Perform the following steps to create a support package in Windows PowerShell for StorSimple.</span></span>

#### <a name="to-create-a-support-package-in-windows-powershell-for-storsimple"></a><span data-ttu-id="69e0f-116">Pour créer un package de support dans Windows PowerShell pour StorSimple</span><span class="sxs-lookup"><span data-stu-id="69e0f-116">To create a support package in Windows PowerShell for StorSimple</span></span>

1. <span data-ttu-id="69e0f-117">Pour démarrer une session Windows PowerShell en tant qu’administrateur sur l’ordinateur distant utilisé pour la connexion à votre appareil StorSimple, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="69e0f-117">To start a Windows PowerShell session as an administrator on the remote computer that's used to connect to your StorSimple device, enter the following command:</span></span>
   
    `Start PowerShell`
2. <span data-ttu-id="69e0f-118">Dans la session Windows PowerShell, connectez-vous à la console SSAdmin de votre appareil :</span><span class="sxs-lookup"><span data-stu-id="69e0f-118">In the Windows PowerShell session, connect to the SSAdmin Console of your device:</span></span>
   
   1. <span data-ttu-id="69e0f-119">À l’invite de commandes, tapez :</span><span class="sxs-lookup"><span data-stu-id="69e0f-119">At the command prompt, enter:</span></span>
     
       `$MS = New-PSSession -ComputerName <IP address for DATA 0> -Credential SSAdmin -ConfigurationName "SSAdminConsole"`
   2. <span data-ttu-id="69e0f-120">Dans la boîte de dialogue qui s’affiche, saisissez votre mot de passe administrateur.</span><span class="sxs-lookup"><span data-stu-id="69e0f-120">In the dialog box that opens, enter your device administrator password.</span></span> <span data-ttu-id="69e0f-121">Le mot de passe par défaut est _Password1_.</span><span class="sxs-lookup"><span data-stu-id="69e0f-121">The default password is _Password1_.</span></span>
     
      ![Boîte de dialogue des informations d’identification PowerShell](./media/storsimple-8000-create-manage-support-package/IC740962.png)
   3. <span data-ttu-id="69e0f-123">Sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="69e0f-123">Select **OK**.</span></span>
   4. <span data-ttu-id="69e0f-124">À l’invite de commandes, tapez :</span><span class="sxs-lookup"><span data-stu-id="69e0f-124">At the command prompt, enter:</span></span>
     
      `Enter-PSSession $MS`
3. <span data-ttu-id="69e0f-125">Dans la session qui s’ouvre, saisissez la commande appropriée.</span><span class="sxs-lookup"><span data-stu-id="69e0f-125">In the session that opens, enter the appropriate command.</span></span>
   
   * <span data-ttu-id="69e0f-126">Pour les partages réseau protégés par un mot de passe, saisissez :</span><span class="sxs-lookup"><span data-stu-id="69e0f-126">For network shares that are password protected, enter:</span></span>
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" –Credential "Username" -Force`
     
       <span data-ttu-id="69e0f-127">Vous serez invité à entrer un mot de passe, le chemin d’accès au dossier réseau partagé et une phrase secrète de chiffrement (car le package de support est chiffré).</span><span class="sxs-lookup"><span data-stu-id="69e0f-127">You'll be prompted for a password, a path to the network shared folder, and an encryption passphrase (because the support package is encrypted).</span></span> <span data-ttu-id="69e0f-128">Un package de support est ensuite créé dans le dossier spécifié.</span><span class="sxs-lookup"><span data-stu-id="69e0f-128">A support package is then created in the specified folder.</span></span>
   * <span data-ttu-id="69e0f-129">Pour les partages qui ne sont pas protégés par un mot de passe, vous n’avez pas besoin du paramètre `-Credential` .</span><span class="sxs-lookup"><span data-stu-id="69e0f-129">For shares that are not password protected, you do not need the `-Credential` parameter.</span></span> <span data-ttu-id="69e0f-130">Entrez les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="69e0f-130">Enter the following:</span></span>
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" -Force`
     
       <span data-ttu-id="69e0f-131">Le package de support est créé pour les deux contrôleurs dans le dossier réseau partagé spécifié.</span><span class="sxs-lookup"><span data-stu-id="69e0f-131">The support package is created for both controllers in the specified network shared folder.</span></span> <span data-ttu-id="69e0f-132">Il s’agit d’un fichier compressé et chiffré qui peut être envoyé au support technique de Microsoft à des fins de dépannage.</span><span class="sxs-lookup"><span data-stu-id="69e0f-132">It's an encrypted, compressed file that can be sent to Microsoft Support for troubleshooting.</span></span> <span data-ttu-id="69e0f-133">Pour plus d'informations, consultez [Contacter le support technique de Microsoft](storsimple-8000-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="69e0f-133">For more information, see [Contact Microsoft Support](storsimple-8000-contact-microsoft-support.md).</span></span>

### <a name="the-export-hcssupportpackage-cmdlet-parameters"></a><span data-ttu-id="69e0f-134">Les paramètres de l’applet de commande Export-HcsSupportPackage</span><span class="sxs-lookup"><span data-stu-id="69e0f-134">The Export-HcsSupportPackage cmdlet parameters</span></span>

<span data-ttu-id="69e0f-135">Vous pouvez utiliser les paramètres suivants avec l’applet de commande Export-HcsSupportPackage.</span><span class="sxs-lookup"><span data-stu-id="69e0f-135">You can use the following parameters with the Export-HcsSupportPackage cmdlet.</span></span>

| <span data-ttu-id="69e0f-136">Paramètre</span><span class="sxs-lookup"><span data-stu-id="69e0f-136">Parameter</span></span> | <span data-ttu-id="69e0f-137">Obligatoire ou facultatif</span><span class="sxs-lookup"><span data-stu-id="69e0f-137">Required/Optional</span></span> | <span data-ttu-id="69e0f-138">Description</span><span class="sxs-lookup"><span data-stu-id="69e0f-138">Description</span></span> |
| --- | --- | --- |
| `-Path` |<span data-ttu-id="69e0f-139">Requis</span><span class="sxs-lookup"><span data-stu-id="69e0f-139">Required</span></span> |<span data-ttu-id="69e0f-140">Permet d’indiquer l’emplacement du dossier réseau partagé dans lequel le package de support est placé.</span><span class="sxs-lookup"><span data-stu-id="69e0f-140">Use to provide the location of the network shared folder in which the support package is placed.</span></span> |
| `-EncryptionPassphrase` |<span data-ttu-id="69e0f-141">Requis</span><span class="sxs-lookup"><span data-stu-id="69e0f-141">Required</span></span> |<span data-ttu-id="69e0f-142">Permet de fournir une phrase secrète permettant de chiffrer le package de support.</span><span class="sxs-lookup"><span data-stu-id="69e0f-142">Use to provide a passphrase to help encrypt the support package.</span></span> |
| `-Credential` |<span data-ttu-id="69e0f-143">Facultatif</span><span class="sxs-lookup"><span data-stu-id="69e0f-143">Optional</span></span> |<span data-ttu-id="69e0f-144">Permet de fournir des informations d’identification d’accès pour le dossier réseau partagé.</span><span class="sxs-lookup"><span data-stu-id="69e0f-144">Use to supply access credentials for the network shared folder.</span></span> |
| `-Force` |<span data-ttu-id="69e0f-145">Facultatif</span><span class="sxs-lookup"><span data-stu-id="69e0f-145">Optional</span></span> |<span data-ttu-id="69e0f-146">Permet d'ignorer l'étape de confirmation de la phrase secrète de chiffrement.</span><span class="sxs-lookup"><span data-stu-id="69e0f-146">Use to skip the encryption passphrase confirmation step.</span></span> |
| `-PackageTag` |<span data-ttu-id="69e0f-147">Facultatif</span><span class="sxs-lookup"><span data-stu-id="69e0f-147">Optional</span></span> |<span data-ttu-id="69e0f-148">Permet de spécifier un répertoire sous *Chemin d’accès* dans lequel le package de support est placé.</span><span class="sxs-lookup"><span data-stu-id="69e0f-148">Use to specify a directory under *Path* in which the support package is placed.</span></span> <span data-ttu-id="69e0f-149">La valeur par défaut est [nom de l’appareil]-[date et heure actuelles : aaaa-MM-jj-HH-mm-ss].</span><span class="sxs-lookup"><span data-stu-id="69e0f-149">The default is [device name]-[current date and time:yyyy-MM-dd-HH-mm-ss].</span></span> |
| `-Scope` |<span data-ttu-id="69e0f-150">Facultatif</span><span class="sxs-lookup"><span data-stu-id="69e0f-150">Optional</span></span> |<span data-ttu-id="69e0f-151">Définir sur **Cluster** (valeur par défaut) pour créer un package de support pour les deux contrôleurs.</span><span class="sxs-lookup"><span data-stu-id="69e0f-151">Specify as **Cluster** (default) to create a support package for both controllers.</span></span> <span data-ttu-id="69e0f-152">Si vous souhaitez créer un package uniquement pour le contrôleur actuel, spécifiez **Contrôleur**.</span><span class="sxs-lookup"><span data-stu-id="69e0f-152">If you want to create a package only for the current controller, specify **Controller**.</span></span> |

## <a name="edit-a-support-package"></a><span data-ttu-id="69e0f-153">Modification d'un package de support</span><span class="sxs-lookup"><span data-stu-id="69e0f-153">Edit a support package</span></span>

<span data-ttu-id="69e0f-154">Une fois que vous avez généré un package de support, vous devrez peut-être modifier le package pour en supprimer les informations sensibles.</span><span class="sxs-lookup"><span data-stu-id="69e0f-154">After you have generated a support package, you might need to edit the package to remove sensitive information.</span></span> <span data-ttu-id="69e0f-155">Cela peut inclure des noms de volume, les adresses IP d’appareil et les noms des sauvegardes des fichiers journaux.</span><span class="sxs-lookup"><span data-stu-id="69e0f-155">This can include volume names, device IP addresses, and backup names from the log files.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="69e0f-156">Vous pouvez uniquement modifier un package de support qui a été généré à l'aide de Windows PowerShell pour StorSimple.</span><span class="sxs-lookup"><span data-stu-id="69e0f-156">You can only edit a support package that was generated through Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="69e0f-157">Vous ne pouvez pas modifier un package créé dans le portail Azure avec le service StorSimple Device Manager.</span><span class="sxs-lookup"><span data-stu-id="69e0f-157">You can't edit a package created in the Azure portal with StorSimple Device Manager service.</span></span>

<span data-ttu-id="69e0f-158">Pour modifier un package de support avant de le télécharger sur le site de support technique de Microsoft, vous devez déchiffrer le package de support, modifier les fichiers et le chiffrer de nouveau.</span><span class="sxs-lookup"><span data-stu-id="69e0f-158">To edit a support package before uploading it on the Microsoft Support site, first decrypt the support package, edit the files, and then re-encrypt it.</span></span> <span data-ttu-id="69e0f-159">Procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="69e0f-159">Perform the following steps.</span></span>

#### <a name="to-edit-a-support-package-in-windows-powershell-for-storsimple"></a><span data-ttu-id="69e0f-160">Pour modifier un package de support dans Windows PowerShell pour StorSimple</span><span class="sxs-lookup"><span data-stu-id="69e0f-160">To edit a support package in Windows PowerShell for StorSimple</span></span>

1. <span data-ttu-id="69e0f-161">Générez un package de support, comme décrit dans la section [Création d’un package de support dans Windows PowerShell pour StorSimple](#to-create-a-support-package-in-windows-powershell-for-storsimple).</span><span class="sxs-lookup"><span data-stu-id="69e0f-161">Generate a support package as described earlier, in [To create a support package in Windows PowerShell for StorSimple](#to-create-a-support-package-in-windows-powershell-for-storsimple).</span></span>
2. <span data-ttu-id="69e0f-162">[Téléchargez le script](http://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) localement sur votre ordinateur client.</span><span class="sxs-lookup"><span data-stu-id="69e0f-162">[Download the script](http://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) locally on your client.</span></span>
3. <span data-ttu-id="69e0f-163">Importez le module Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="69e0f-163">Import the Windows PowerShell module.</span></span> <span data-ttu-id="69e0f-164">Spécifiez le chemin d’accès au dossier local dans lequel vous avez téléchargé le script.</span><span class="sxs-lookup"><span data-stu-id="69e0f-164">Specify the path to the local folder in which you downloaded the script.</span></span> <span data-ttu-id="69e0f-165">Pour importer le module, entrez :</span><span class="sxs-lookup"><span data-stu-id="69e0f-165">To import the module, enter:</span></span>
   
    `Import-module <Path to the folder that contains the Windows PowerShell script>`
4. <span data-ttu-id="69e0f-166">Tous les fichiers sont des fichiers *.aes* compressés et chiffrés.</span><span class="sxs-lookup"><span data-stu-id="69e0f-166">All the files are *.aes* files that are compressed and encrypted.</span></span> <span data-ttu-id="69e0f-167">Pour décompresser et déchiffrer les fichiers, entrez :</span><span class="sxs-lookup"><span data-stu-id="69e0f-167">To decompress and decrypt files, enter:</span></span>
   
    `Open-HcsSupportPackage <Path to the folder that contains support package files>`
   
    <span data-ttu-id="69e0f-168">Sachez que les extensions sont maintenant affichées pour tous les fichiers.</span><span class="sxs-lookup"><span data-stu-id="69e0f-168">Note that the actual file extensions are now displayed for all the files.</span></span>
   
    ![Modifier un package de support](./media/storsimple-8000-create-manage-support-package/IC750706.png)
5. <span data-ttu-id="69e0f-170">Lorsque vous êtes invité à entrer la phrase secrète de chiffrement, tapez la phrase secrète utilisée lors de la création du package de support.</span><span class="sxs-lookup"><span data-stu-id="69e0f-170">When you're prompted for the encryption passphrase, enter the passphrase that you used when the support package was created.</span></span>
   
        cmdlet Open-HcsSupportPackage at command pipeline position 1
   
        Supply values for the following parameters:EncryptionPassphrase: ****
6. <span data-ttu-id="69e0f-171">Accédez au dossier qui contient les fichiers journaux.</span><span class="sxs-lookup"><span data-stu-id="69e0f-171">Browse to the folder that contains the log files.</span></span> <span data-ttu-id="69e0f-172">Étant donné que les fichiers journaux sont désormais décompressés et déchiffrés, leurs extensions d’origine sont affichées.</span><span class="sxs-lookup"><span data-stu-id="69e0f-172">Because the log files are now decompressed and decrypted, these will have original file extensions.</span></span> <span data-ttu-id="69e0f-173">Modifiez ces fichiers pour supprimer toutes les informations spécifiques au client, comme les noms de volumes et les adresses IP d’appareils, puis enregistrez les fichiers.</span><span class="sxs-lookup"><span data-stu-id="69e0f-173">Modify these files to remove any customer-specific information, such as volume names and device IP addresses, and save the files.</span></span>
7. <span data-ttu-id="69e0f-174">Fermez les fichiers pour les compresser au format gzip et les chiffrer avec AES-256.</span><span class="sxs-lookup"><span data-stu-id="69e0f-174">Close the files to compress them with gzip and encrypt them with AES-256.</span></span> <span data-ttu-id="69e0f-175">Cette opération est exécutée à des fins de sécurité et de rapidité lors du transfert du package de support sur un réseau.</span><span class="sxs-lookup"><span data-stu-id="69e0f-175">This is for speed and security in transferring the support package over a network.</span></span> <span data-ttu-id="69e0f-176">Pour compresser et chiffrer les fichiers, entrez les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="69e0f-176">To compress and encrypt files, enter the following:</span></span>
   
    `Close-HcsSupportPackage <Path to the folder that contains support package files>`
   
    ![Modifier un package de support](./media/storsimple-8000-create-manage-support-package/IC750707.png)
8. <span data-ttu-id="69e0f-178">Lorsque vous y êtes invité, fournissez une phrase secrète de chiffrement pour le package de support modifié.</span><span class="sxs-lookup"><span data-stu-id="69e0f-178">When prompted, provide an encryption passphrase for the modified support package.</span></span>
   
        cmdlet Close-HcsSupportPackage at command pipeline position 1
        Supply values for the following parameters:EncryptionPassphrase: ****
9. <span data-ttu-id="69e0f-179">Notez la nouvelle phrase secrète afin de pouvoir la partager avec le support technique de Microsoft si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="69e0f-179">Write down the new passphrase, so that you can share it with Microsoft Support when requested.</span></span>

### <a name="example-editing-files-in-a-support-package-on-a-password-protected-share"></a><span data-ttu-id="69e0f-180">Exemple : Modification de fichiers dans un package de support sur un partage protégé par mot de passe</span><span class="sxs-lookup"><span data-stu-id="69e0f-180">Example: Editing files in a support package on a password-protected share</span></span>

<span data-ttu-id="69e0f-181">L’exemple suivant illustre comment déchiffrer, modifier et re-chiffrer un package de support.</span><span class="sxs-lookup"><span data-stu-id="69e0f-181">The following example shows how to decrypt, edit, and re-encrypt a support package.</span></span>

        PS C:\WINDOWS\system32> Import-module C:\Users\Default\StorSimple\SupportPackage\HCSSupportPackageTools.psm1

        PS C:\WINDOWS\system32> Open-HcsSupportPackage \\hcsfs\Logs\TD48\TD48Logs\C0-A\etw

        cmdlet Open-HcsSupportPackage at command pipeline position 1

        Supply values for the following parameters:

        EncryptionPassphrase: ****

        PS C:\WINDOWS\system32> Close-HcsSupportPackage \\hcsfs\Logs\TD48\TD48Logs\C0-A\etw

        cmdlet Close-HcsSupportPackage at command pipeline position 1

        Supply values for the following parameters:

        EncryptionPassphrase: ****

        PS C:\WINDOWS\system32>

## <a name="next-steps"></a><span data-ttu-id="69e0f-182">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="69e0f-182">Next steps</span></span>

* <span data-ttu-id="69e0f-183">Apprenez-en davantage sur les [informations collectées dans le package de prise en charge](https://support.microsoft.com/help/3193606/storsimple-support-packages-and-device-logs).</span><span class="sxs-lookup"><span data-stu-id="69e0f-183">Learn about the [information collected in the Support package](https://support.microsoft.com/help/3193606/storsimple-support-packages-and-device-logs)</span></span>
* <span data-ttu-id="69e0f-184">Découvrez comment [utiliser les packages de support et les journaux de l’appareil pour dépanner votre déploiement](storsimple-troubleshoot-deployment.md#support-packages-and-device-logs-available-for-troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="69e0f-184">Learn how to [use support packages and device logs to troubleshoot your device deployment](storsimple-troubleshoot-deployment.md#support-packages-and-device-logs-available-for-troubleshooting).</span></span>
* <span data-ttu-id="69e0f-185">Découvrez comment [utiliser le service StorSimple Device Manager pour gérer votre appareil StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="69e0f-185">Learn how to [use the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

