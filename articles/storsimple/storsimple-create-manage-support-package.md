---
title: "Création d'un package de support StorSimple | Microsoft Docs"
description: "Apprenez à créer, déchiffrer et modifier un package de support pour votre appareil StorSimple."
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
ms.openlocfilehash: 32d20e7a8adcfc646c592213fe7395b87a93c985
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-a-storsimple-support-package"></a><span data-ttu-id="7d106-103">Création et gestion d’un package de prise en charge StorSimple</span><span class="sxs-lookup"><span data-stu-id="7d106-103">Create and manage a StorSimple support package</span></span>
## <a name="overview"></a><span data-ttu-id="7d106-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="7d106-104">Overview</span></span>
<span data-ttu-id="7d106-105">Un package de support StorSimple est un mécanisme facile à utiliser qui collecte tous les journaux appropriés afin d’aider le support Microsoft à résoudre tout problème lié à votre appareil StorSimple.</span><span class="sxs-lookup"><span data-stu-id="7d106-105">A StorSimple support package is an easy-to-use mechanism that collects all relevant logs to assist Microsoft Support with troubleshooting any StorSimple device issues.</span></span> <span data-ttu-id="7d106-106">Les fichiers journaux collectés sont chiffrés et compressés.</span><span class="sxs-lookup"><span data-stu-id="7d106-106">The collected logs are encrypted and compressed.</span></span>

<span data-ttu-id="7d106-107">Ce didacticiel inclut des instructions détaillées pour créer et gérer le package de support.</span><span class="sxs-lookup"><span data-stu-id="7d106-107">This tutorial includes step-by-step instructions to create and manage the support package.</span></span>

## <a name="create-and-upload-a-support-package-in-the-azure-classic-portal"></a><span data-ttu-id="7d106-108">Créer et charger un package de support dans le portail Azure Classic</span><span class="sxs-lookup"><span data-stu-id="7d106-108">Create and upload a support package in the Azure classic portal</span></span>
<span data-ttu-id="7d106-109">Vous pouvez créer et télécharger un package de support sur le site de support technique de Microsoft à l’aide de la page **Maintenance** du service dans le portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="7d106-109">You can create and upload a support package to the Microsoft Support site through the **Maintenance** page of the service in the Azure classic portal.</span></span>

> [!NOTE]
> <span data-ttu-id="7d106-110">Le chargement nécessite une clé de sécurité de support.</span><span class="sxs-lookup"><span data-stu-id="7d106-110">The upload requires a support passkey.</span></span> <span data-ttu-id="7d106-111">Votre ingénieur du support technique doit vous la fournir par e-mail.</span><span class="sxs-lookup"><span data-stu-id="7d106-111">Your support engineer should provide this to you in an email.</span></span>
> 
> 

<span data-ttu-id="7d106-112">Un package de support chiffré et compressé (fichier .cab) est créé et chargé sur le site de support.</span><span class="sxs-lookup"><span data-stu-id="7d106-112">An encrypted and compressed support package (.cab file) is created and uploaded to the Support site.</span></span> <span data-ttu-id="7d106-113">L’ingénieur du support technique peut ensuite récupérer ce package à partir du site de support pour résoudre le problème.</span><span class="sxs-lookup"><span data-stu-id="7d106-113">The support engineer can then retrieve this package from the Support site for troubleshooting the issue.</span></span>

<span data-ttu-id="7d106-114">Procédez comme suit dans le portail classique pour créer un package de support.</span><span class="sxs-lookup"><span data-stu-id="7d106-114">Perform the following steps in the classic portal to create a support package.</span></span>

#### <a name="to-create-a-support-package-in-the-azure-classic-portal"></a><span data-ttu-id="7d106-115">Pour créer un package de support dans le portail Azure Classic</span><span class="sxs-lookup"><span data-stu-id="7d106-115">To create a support package in the Azure classic portal</span></span>
1. <span data-ttu-id="7d106-116">Sélectionnez **Appareils** > **Maintenance**.</span><span class="sxs-lookup"><span data-stu-id="7d106-116">Select **Devices** > **Maintenance**.</span></span>
2. <span data-ttu-id="7d106-117">Dans la section **Package de support**, sélectionnez **Créer et télécharger le package de support**.</span><span class="sxs-lookup"><span data-stu-id="7d106-117">In the **Support package** section, select **Create and upload support package**.</span></span>
3. <span data-ttu-id="7d106-118">Dans la boîte de dialogue **Créer et télécharger le package de support** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="7d106-118">In the **Create and upload support package** dialog box, do the following:</span></span>
   
    ![Créer un package de support](./media/storsimple-create-manage-support-package/IC740923.png)
   
   * <span data-ttu-id="7d106-120">Dans la zone de texte **Clé de sécurité de support** , entrez la clé de sécurité.</span><span class="sxs-lookup"><span data-stu-id="7d106-120">In the **Support Passkey** text box, enter the passkey.</span></span> <span data-ttu-id="7d106-121">Votre ingénieur de support technique Microsoft doit vous envoyer cette clé de sécurité par e-mail.</span><span class="sxs-lookup"><span data-stu-id="7d106-121">Your Microsoft support engineer should send this passkey to you in email.</span></span>
   * <span data-ttu-id="7d106-122">Cochez la case pour accepter de télécharger automatiquement le package de support sur le site de support de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="7d106-122">Select the check box to provide consent to automatically upload the support package to the Microsoft Support site.</span></span>
   * <span data-ttu-id="7d106-123">Cliquez sur l’icône en forme de coche </span><span class="sxs-lookup"><span data-stu-id="7d106-123">Click the check icon</span></span> ![Icône en forme de coche](./media/storsimple-create-manage-support-package/IC740895.png)<span data-ttu-id="7d106-125">.</span><span class="sxs-lookup"><span data-stu-id="7d106-125">.</span></span>

## <a name="manually-create-a-support-package"></a><span data-ttu-id="7d106-126">Créer manuellement un package de support</span><span class="sxs-lookup"><span data-stu-id="7d106-126">Manually create a support package</span></span>
<span data-ttu-id="7d106-127">Dans certains cas, vous devez créer manuellement le package de support via Windows PowerShell pour StorSimple.</span><span class="sxs-lookup"><span data-stu-id="7d106-127">In some cases, you'll need to manually create the support package through Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="7d106-128">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="7d106-128">For example:</span></span>

* <span data-ttu-id="7d106-129">Si vous devez supprimer des informations sensibles de vos fichiers journaux avant de le partager avec le support Microsoft.</span><span class="sxs-lookup"><span data-stu-id="7d106-129">If you need to remove sensitive information from your log files prior to sharing with Microsoft Support.</span></span>
* <span data-ttu-id="7d106-130">Si vous rencontrez des difficultés à charger le package en raison de problèmes de connectivité.</span><span class="sxs-lookup"><span data-stu-id="7d106-130">If you are having difficulty uploading the package due to connectivity issues.</span></span>

<span data-ttu-id="7d106-131">Vous pouvez partager votre package de support généré manuellement avec le support Microsoft par e-mail.</span><span class="sxs-lookup"><span data-stu-id="7d106-131">You can share your manually generated support package with Microsoft Support over email.</span></span> <span data-ttu-id="7d106-132">Procédez comme suit pour créer un package de support dans Windows PowerShell pour StorSimple.</span><span class="sxs-lookup"><span data-stu-id="7d106-132">Perform the following steps to create a support package in Windows PowerShell for StorSimple.</span></span>

#### <a name="to-create-a-support-package-in-windows-powershell-for-storsimple"></a><span data-ttu-id="7d106-133">Pour créer un package de support dans Windows PowerShell pour StorSimple</span><span class="sxs-lookup"><span data-stu-id="7d106-133">To create a support package in Windows PowerShell for StorSimple</span></span>
1. <span data-ttu-id="7d106-134">Pour démarrer une session Windows PowerShell en tant qu’administrateur sur l’ordinateur distant utilisé pour la connexion à votre appareil StorSimple, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="7d106-134">To start a Windows PowerShell session as an administrator on the remote computer that's used to connect to your StorSimple device, enter the following command:</span></span>
   
    `Start PowerShell`
2. <span data-ttu-id="7d106-135">Dans la session Windows PowerShell, connectez-vous à la console SSAdmin de votre appareil :</span><span class="sxs-lookup"><span data-stu-id="7d106-135">In the Windows PowerShell session, connect to the SSAdmin Console of your device:</span></span>
   
   * <span data-ttu-id="7d106-136">À l’invite de commandes, tapez :</span><span class="sxs-lookup"><span data-stu-id="7d106-136">At the command prompt, enter:</span></span>
     
       `$MS = New-PSSession -ComputerName <IP address for DATA 0> -Credential SSAdmin -ConfigurationName "SSAdminConsole"`
   * <span data-ttu-id="7d106-137">Dans la boîte de dialogue qui s’affiche, saisissez votre mot de passe administrateur.</span><span class="sxs-lookup"><span data-stu-id="7d106-137">In the dialog box that opens, enter your device administrator password.</span></span> <span data-ttu-id="7d106-138">Le mot de passe par défaut est :</span><span class="sxs-lookup"><span data-stu-id="7d106-138">The default password is:</span></span>
     
      `Password1`
     
      ![Boîte de dialogue des informations d’identification PowerShell](./media/storsimple-create-manage-support-package/IC740962.png)
   * <span data-ttu-id="7d106-140">Sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="7d106-140">Select **OK**.</span></span>
   * <span data-ttu-id="7d106-141">À l’invite de commandes, tapez :</span><span class="sxs-lookup"><span data-stu-id="7d106-141">At the command prompt, enter:</span></span>
     
      `Enter-PSSession $MS`
3. <span data-ttu-id="7d106-142">Dans la session qui s’ouvre, saisissez la commande appropriée.</span><span class="sxs-lookup"><span data-stu-id="7d106-142">In the session that opens, enter the appropriate command.</span></span>
   
   * <span data-ttu-id="7d106-143">Pour les partages réseau protégés par un mot de passe, saisissez :</span><span class="sxs-lookup"><span data-stu-id="7d106-143">For network shares that are password protected, enter:</span></span>
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" –Credential "Username" -Force`
     
       <span data-ttu-id="7d106-144">Vous serez invité à entrer un mot de passe, le chemin d’accès au dossier réseau partagé et une phrase secrète de chiffrement (car le package de support est chiffré).</span><span class="sxs-lookup"><span data-stu-id="7d106-144">You'll be prompted for a password, a path to the network shared folder, and an encryption passphrase (because the support package is encrypted).</span></span> <span data-ttu-id="7d106-145">Un package de support est ensuite créé dans le dossier spécifié.</span><span class="sxs-lookup"><span data-stu-id="7d106-145">A support package is then created in the specified folder.</span></span>
   * <span data-ttu-id="7d106-146">Pour les partages qui ne sont pas protégés par un mot de passe, vous n’avez pas besoin du paramètre `-Credential` .</span><span class="sxs-lookup"><span data-stu-id="7d106-146">For shares that are not password protected, you do not need the `-Credential` parameter.</span></span> <span data-ttu-id="7d106-147">Entrez les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="7d106-147">Enter the following:</span></span>
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" -Force`
     
       <span data-ttu-id="7d106-148">Le package de support est créé pour les deux contrôleurs dans le dossier réseau partagé spécifié.</span><span class="sxs-lookup"><span data-stu-id="7d106-148">The support package is created for both controllers in the specified network shared folder.</span></span> <span data-ttu-id="7d106-149">Il s’agit d’un fichier compressé et chiffré qui peut être envoyé au support technique de Microsoft à des fins de dépannage.</span><span class="sxs-lookup"><span data-stu-id="7d106-149">It's an encrypted, compressed file that can be sent to Microsoft Support for troubleshooting.</span></span> <span data-ttu-id="7d106-150">Pour plus d'informations, consultez [Contacter le support technique de Microsoft](storsimple-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="7d106-150">For more information, see [Contact Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>

### <a name="the-export-hcssupportpackage-cmdlet-parameters"></a><span data-ttu-id="7d106-151">Les paramètres de l’applet de commande Export-HcsSupportPackage</span><span class="sxs-lookup"><span data-stu-id="7d106-151">The Export-HcsSupportPackage cmdlet parameters</span></span>
<span data-ttu-id="7d106-152">Vous pouvez utiliser les paramètres suivants avec l’applet de commande Export-HcsSupportPackage.</span><span class="sxs-lookup"><span data-stu-id="7d106-152">You can use the following parameters with the Export-HcsSupportPackage cmdlet.</span></span>

| <span data-ttu-id="7d106-153">Paramètre</span><span class="sxs-lookup"><span data-stu-id="7d106-153">Parameter</span></span> | <span data-ttu-id="7d106-154">Obligatoire ou facultatif</span><span class="sxs-lookup"><span data-stu-id="7d106-154">Required/Optional</span></span> | <span data-ttu-id="7d106-155">Description</span><span class="sxs-lookup"><span data-stu-id="7d106-155">Description</span></span> |
| --- | --- | --- |
| `-Path` |<span data-ttu-id="7d106-156">Requis</span><span class="sxs-lookup"><span data-stu-id="7d106-156">Required</span></span> |<span data-ttu-id="7d106-157">Permet d’indiquer l’emplacement du dossier réseau partagé dans lequel le package de support est placé.</span><span class="sxs-lookup"><span data-stu-id="7d106-157">Use to provide the location of the network shared folder in which the support package is placed.</span></span> |
| `-EncryptionPassphrase` |<span data-ttu-id="7d106-158">Requis</span><span class="sxs-lookup"><span data-stu-id="7d106-158">Required</span></span> |<span data-ttu-id="7d106-159">Permet de fournir une phrase secrète permettant de chiffrer le package de support.</span><span class="sxs-lookup"><span data-stu-id="7d106-159">Use to provide a passphrase to help encrypt the support package.</span></span> |
| `-Credential` |<span data-ttu-id="7d106-160">Facultatif</span><span class="sxs-lookup"><span data-stu-id="7d106-160">Optional</span></span> |<span data-ttu-id="7d106-161">Permet de fournir des informations d’identification d’accès pour le dossier réseau partagé.</span><span class="sxs-lookup"><span data-stu-id="7d106-161">Use to supply access credentials for the network shared folder.</span></span> |
| `-Force` |<span data-ttu-id="7d106-162">Facultatif</span><span class="sxs-lookup"><span data-stu-id="7d106-162">Optional</span></span> |<span data-ttu-id="7d106-163">Permet d'ignorer l'étape de confirmation de la phrase secrète de chiffrement.</span><span class="sxs-lookup"><span data-stu-id="7d106-163">Use to skip the encryption passphrase confirmation step.</span></span> |
| `-PackageTag` |<span data-ttu-id="7d106-164">Facultatif</span><span class="sxs-lookup"><span data-stu-id="7d106-164">Optional</span></span> |<span data-ttu-id="7d106-165">Permet de spécifier un répertoire sous *Chemin d’accès* dans lequel le package de support est placé.</span><span class="sxs-lookup"><span data-stu-id="7d106-165">Use to specify a directory under *Path* in which the support package is placed.</span></span> <span data-ttu-id="7d106-166">La valeur par défaut est [nom de l’appareil]-[date et heure actuelles : aaaa-MM-jj-HH-mm-ss].</span><span class="sxs-lookup"><span data-stu-id="7d106-166">The default is [device name]-[current date and time:yyyy-MM-dd-HH-mm-ss].</span></span> |
| `-Scope` |<span data-ttu-id="7d106-167">Facultatif</span><span class="sxs-lookup"><span data-stu-id="7d106-167">Optional</span></span> |<span data-ttu-id="7d106-168">Définir sur **Cluster** (valeur par défaut) pour créer un package de support pour les deux contrôleurs.</span><span class="sxs-lookup"><span data-stu-id="7d106-168">Specify as **Cluster** (default) to create a support package for both controllers.</span></span> <span data-ttu-id="7d106-169">Si vous souhaitez créer un package uniquement pour le contrôleur actuel, spécifiez **Contrôleur**.</span><span class="sxs-lookup"><span data-stu-id="7d106-169">If you want to create a package only for the current controller, specify **Controller**.</span></span> |

## <a name="edit-a-support-package"></a><span data-ttu-id="7d106-170">Modification d'un package de support</span><span class="sxs-lookup"><span data-stu-id="7d106-170">Edit a support package</span></span>
<span data-ttu-id="7d106-171">Une fois que vous avez généré un package de support, vous devrez peut-être modifier le package pour en supprimer les informations sensibles.</span><span class="sxs-lookup"><span data-stu-id="7d106-171">After you have generated a support package, you might need to edit the package to remove sensitive information.</span></span> <span data-ttu-id="7d106-172">Cela peut inclure des noms de volume, les adresses IP d’appareil et les noms des sauvegardes des fichiers journaux.</span><span class="sxs-lookup"><span data-stu-id="7d106-172">This can include volume names, device IP addresses, and backup names from the log files.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7d106-173">Vous pouvez uniquement modifier un package de support qui a été généré à l'aide de Windows PowerShell pour StorSimple.</span><span class="sxs-lookup"><span data-stu-id="7d106-173">You can only edit a support package that was generated through Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="7d106-174">Vous ne pouvez pas modifier un package créé dans le portail Azure Classic avec le service StorSimple Manager.</span><span class="sxs-lookup"><span data-stu-id="7d106-174">You can't edit a package created in the Azure classic portal with StorSimple Manager service.</span></span>
> 
> 

<span data-ttu-id="7d106-175">Pour modifier un package de support avant de le télécharger sur le site de support technique de Microsoft, vous devez déchiffrer le package de support, modifier les fichiers et le chiffrer de nouveau.</span><span class="sxs-lookup"><span data-stu-id="7d106-175">To edit a support package before uploading it on the Microsoft Support site, first decrypt the support package, edit the files, and then re-encrypt it.</span></span> <span data-ttu-id="7d106-176">Procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="7d106-176">Perform the following steps.</span></span>

#### <a name="to-edit-a-support-package-in-windows-powershell-for-storsimple"></a><span data-ttu-id="7d106-177">Pour modifier un package de support dans Windows PowerShell pour StorSimple</span><span class="sxs-lookup"><span data-stu-id="7d106-177">To edit a support package in Windows PowerShell for StorSimple</span></span>
1. <span data-ttu-id="7d106-178">Générez un package de support, comme décrit dans la section [Création d’un package de support dans Windows PowerShell pour StorSimple](#to-create-a-support-package-in-windows-powershell-for-storsimple).</span><span class="sxs-lookup"><span data-stu-id="7d106-178">Generate a support package as described earlier, in [To create a support package in Windows PowerShell for StorSimple](#to-create-a-support-package-in-windows-powershell-for-storsimple).</span></span>
2. <span data-ttu-id="7d106-179">[Téléchargez le script](http://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) localement sur votre ordinateur client.</span><span class="sxs-lookup"><span data-stu-id="7d106-179">[Download the script](http://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) locally on your client.</span></span>
3. <span data-ttu-id="7d106-180">Importez le module Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7d106-180">Import the Windows PowerShell module.</span></span> <span data-ttu-id="7d106-181">Spécifiez le chemin d’accès au dossier local dans lequel vous avez téléchargé le script.</span><span class="sxs-lookup"><span data-stu-id="7d106-181">Specify the path to the local folder in which you downloaded the script.</span></span> <span data-ttu-id="7d106-182">Pour importer le module, entrez :</span><span class="sxs-lookup"><span data-stu-id="7d106-182">To import the module, enter:</span></span>
   
    `Import-module <Path to the folder that contains the Windows PowerShell script>`
4. <span data-ttu-id="7d106-183">Tous les fichiers sont des fichiers *.aes* compressés et chiffrés.</span><span class="sxs-lookup"><span data-stu-id="7d106-183">All the files are *.aes* files that are compressed and encrypted.</span></span> <span data-ttu-id="7d106-184">Pour décompresser et déchiffrer les fichiers, entrez :</span><span class="sxs-lookup"><span data-stu-id="7d106-184">To decompress and decrypt files, enter:</span></span>
   
    `Open-HcsSupportPackage <Path to the folder that contains support package files>`
   
    <span data-ttu-id="7d106-185">Sachez que les extensions sont maintenant affichées pour tous les fichiers.</span><span class="sxs-lookup"><span data-stu-id="7d106-185">Note that the actual file extensions are now displayed for all the files.</span></span>
   
    ![Modifier un package de support](./media/storsimple-create-manage-support-package/IC750706.png)
5. <span data-ttu-id="7d106-187">Lorsque vous êtes invité à entrer la phrase secrète de chiffrement, tapez la phrase secrète utilisée lors de la création du package de support.</span><span class="sxs-lookup"><span data-stu-id="7d106-187">When you're prompted for the encryption passphrase, enter the passphrase that you used when the support package was created.</span></span>
   
        cmdlet Open-HcsSupportPackage at command pipeline position 1
   
        Supply values for the following parameters:EncryptionPassphrase: ****
6. <span data-ttu-id="7d106-188">Accédez au dossier qui contient les fichiers journaux.</span><span class="sxs-lookup"><span data-stu-id="7d106-188">Browse to the folder that contains the log files.</span></span> <span data-ttu-id="7d106-189">Étant donné que les fichiers journaux sont désormais décompressés et déchiffrés, leurs extensions d’origine sont affichées.</span><span class="sxs-lookup"><span data-stu-id="7d106-189">Because the log files are now decompressed and decrypted, these will have original file extensions.</span></span> <span data-ttu-id="7d106-190">Modifiez ces fichiers pour supprimer toutes les informations spécifiques au client, comme les noms de volumes et les adresses IP d’appareils, puis enregistrez les fichiers.</span><span class="sxs-lookup"><span data-stu-id="7d106-190">Modify these files to remove any customer-specific information, such as volume names and device IP addresses, and save the files.</span></span>
7. <span data-ttu-id="7d106-191">Fermez les fichiers pour les compresser au format gzip et les chiffrer avec AES-256.</span><span class="sxs-lookup"><span data-stu-id="7d106-191">Close the files to compress them with gzip and encrypt them with AES-256.</span></span> <span data-ttu-id="7d106-192">Cette opération est exécutée à des fins de sécurité et de rapidité lors du transfert du package de support sur un réseau.</span><span class="sxs-lookup"><span data-stu-id="7d106-192">This is for speed and security in transferring the support package over a network.</span></span> <span data-ttu-id="7d106-193">Pour compresser et chiffrer les fichiers, entrez les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="7d106-193">To compress and encrypt files, enter the following:</span></span>
   
    `Close-HcsSupportPackage <Path to the folder that contains support package files>`
   
    ![Modifier un package de support](./media/storsimple-create-manage-support-package/IC750707.png)
8. <span data-ttu-id="7d106-195">Lorsque vous y êtes invité, fournissez une phrase secrète de chiffrement pour le package de support modifié.</span><span class="sxs-lookup"><span data-stu-id="7d106-195">When prompted, provide an encryption passphrase for the modified support package.</span></span>
   
        cmdlet Close-HcsSupportPackage at command pipeline position 1
        Supply values for the following parameters:EncryptionPassphrase: ****
9. <span data-ttu-id="7d106-196">Notez la nouvelle phrase secrète afin de pouvoir la partager avec le support technique de Microsoft si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="7d106-196">Write down the new passphrase, so that you can share it with Microsoft Support when requested.</span></span>

### <a name="example-editing-files-in-a-support-package-on-a-password-protected-share"></a><span data-ttu-id="7d106-197">Exemple : Modification de fichiers dans un package de support sur un partage protégé par mot de passe</span><span class="sxs-lookup"><span data-stu-id="7d106-197">Example: Editing files in a support package on a password-protected share</span></span>
<span data-ttu-id="7d106-198">L’exemple suivant illustre comment déchiffrer, modifier et re-chiffrer un package de support.</span><span class="sxs-lookup"><span data-stu-id="7d106-198">The following example shows how to decrypt, edit, and re-encrypt a support package.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="7d106-199">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7d106-199">Next steps</span></span>
* <span data-ttu-id="7d106-200">Découvrez comment [utiliser les packages de support et les journaux de l’appareil pour dépanner votre déploiement](storsimple-troubleshoot-deployment.md#support-packages-and-device-logs-available-for-troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="7d106-200">Learn how to [use support packages and device logs to troubleshoot your device deployment](storsimple-troubleshoot-deployment.md#support-packages-and-device-logs-available-for-troubleshooting).</span></span>
* <span data-ttu-id="7d106-201">Découvrez comment [utiliser le service StorSimple Manager pour gérer votre appareil StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="7d106-201">Learn how to [use the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

