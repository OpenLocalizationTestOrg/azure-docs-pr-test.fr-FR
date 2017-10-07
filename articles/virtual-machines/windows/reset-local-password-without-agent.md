---
title: aaaReset un mot de passe local Windows sans agent Azure | Documents Microsoft
description: "Comment tooreset hello mot de passe d’un compte d’utilisateur Windows local lorsque l’agent invité de Azure de hello n’est pas installé ou qu’il fonctionne sur une machine virtuelle"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: cf353dd3-89c9-47f6-a449-f874f0957013
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 04/07/2017
ms.author: iainfou
ms.openlocfilehash: c559c31ea142f9cf50d2c5b6182c5355fec9bac5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-local-windows-password-for-azure-vm"></a><span data-ttu-id="f7480-103">Comment tooreset Windows mot de passe local pour la machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="f7480-103">How tooreset local Windows password for Azure VM</span></span>
<span data-ttu-id="f7480-104">Vous pouvez réinitialiser hello Windows mot de passe local d’une machine virtuelle dans Azure à l’aide de hello [portail Azure ou Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) fournie hello invité de Azure agent est installée.</span><span class="sxs-lookup"><span data-stu-id="f7480-104">You can reset hello local Windows password of a VM in Azure using hello [Azure portal or Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) provided hello Azure guest agent is installed.</span></span> <span data-ttu-id="f7480-105">Cette méthode est hello principal moyen tooreset un mot de passe pour une machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="f7480-105">This method is hello primary way tooreset a password for an Azure VM.</span></span> <span data-ttu-id="f7480-106">Si vous rencontrez des problèmes avec l’agent invité de Azure a hello ne répond ne pas ou le basculement tooinstall après avoir téléchargé une image personnalisée, vous pouvez réinitialiser manuellement un mot de passe Windows.</span><span class="sxs-lookup"><span data-stu-id="f7480-106">If you encounter issues with hello Azure guest agent not responding, or failing tooinstall after uploading a custom image, you can manually reset a Windows password.</span></span> <span data-ttu-id="f7480-107">Cet article décrit en détail comment tooreset un mot de passe du compte local en attachant hello tooanother de disque virtuel de la source du système d’exploitation machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f7480-107">This article details how tooreset a local account password by attaching hello source OS virtual disk tooanother VM.</span></span> 

> [!WARNING]
> <span data-ttu-id="f7480-108">N’utilisez ce processus qu’en dernier recours.</span><span class="sxs-lookup"><span data-stu-id="f7480-108">Only use this process as a last resort.</span></span> <span data-ttu-id="f7480-109">Essayez toujours d’un mot de passe à l’aide de hello tooreset [portail Azure ou Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) première.</span><span class="sxs-lookup"><span data-stu-id="f7480-109">Always try tooreset a password using hello [Azure portal or Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) first.</span></span>
> 
> 

## <a name="overview-of-hello-process"></a><span data-ttu-id="f7480-110">Vue d’ensemble du processus de hello</span><span class="sxs-lookup"><span data-stu-id="f7480-110">Overview of hello process</span></span>
<span data-ttu-id="f7480-111">étapes de base Hello pour l’exécution d’un mot de passe local réinitialisée pour un ordinateur virtuel Windows Azure lorsqu’il n’existe aucun agent invité de Azure d’accès toohello est la suivante :</span><span class="sxs-lookup"><span data-stu-id="f7480-111">hello core steps for performing a local password reset for a Windows VM in Azure when there is no access toohello Azure guest agent is as follows:</span></span>

* <span data-ttu-id="f7480-112">Supprimer la machine virtuelle de la source hello.</span><span class="sxs-lookup"><span data-stu-id="f7480-112">Delete hello source VM.</span></span> <span data-ttu-id="f7480-113">les disques virtuels Hello sont conservés.</span><span class="sxs-lookup"><span data-stu-id="f7480-113">hello virtual disks are retained.</span></span>
* <span data-ttu-id="f7480-114">Attacher le disque tooanother machine virtuelle de la machine virtuelle de source de hello du système d’exploitation sur hello même emplacement au sein de votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="f7480-114">Attach hello source VM's OS disk tooanother VM on hello same location within your Azure subscription.</span></span> <span data-ttu-id="f7480-115">Cette machine virtuelle est hello visé tooas résolution des problèmes de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f7480-115">This VM is referred tooas hello troubleshooting VM.</span></span>
* <span data-ttu-id="f7480-116">Hello, résolution des problèmes de la machine virtuelle, créez des fichiers de configuration sur le disque du système d’exploitation de la machine virtuelle de source de hello.</span><span class="sxs-lookup"><span data-stu-id="f7480-116">Using hello troubleshooting VM, create some config files on hello source VM's OS disk.</span></span>
* <span data-ttu-id="f7480-117">Détacher un disque de système d’exploitation hello VM de hello, résolution des problèmes de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f7480-117">Detach hello VM's OS disk from hello troubleshooting VM.</span></span>
* <span data-ttu-id="f7480-118">Utilisez un toocreate de modèle de gestionnaire de ressources une machine virtuelle, à l’aide du disque virtuel d’origine de hello.</span><span class="sxs-lookup"><span data-stu-id="f7480-118">Use a Resource Manager template toocreate a VM, using hello original virtual disk.</span></span>
* <span data-ttu-id="f7480-119">Lorsque les fichiers de configuration hello hello nouvelle machine virtuelle démarre, vous créez un mot de passe hello mise à jour de l’utilisateur de hello requis.</span><span class="sxs-lookup"><span data-stu-id="f7480-119">When hello new VM boots, hello config files you create update hello password of hello required user.</span></span>

## <a name="detailed-steps"></a><span data-ttu-id="f7480-120">Procédure détaillée</span><span class="sxs-lookup"><span data-stu-id="f7480-120">Detailed steps</span></span>
<span data-ttu-id="f7480-121">Essayez toujours d’un mot de passe à l’aide de hello tooreset [portail Azure ou Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) avant d’essayer de hello comme suit.</span><span class="sxs-lookup"><span data-stu-id="f7480-121">Always try tooreset a password using hello [Azure portal or Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before trying hello following steps.</span></span> <span data-ttu-id="f7480-122">Avant de commencer, vérifiez que vous disposez d’une sauvegarde de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f7480-122">Make sure you have a backup of your VM before you start.</span></span> 

1. <span data-ttu-id="f7480-123">Supprimer hello affectées de machine virtuelle dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="f7480-123">Delete hello affected VM in Azure portal.</span></span> <span data-ttu-id="f7480-124">Suppression hello VM supprime uniquement les métadonnées hello, référence hello Hello machine virtuelle dans Azure.</span><span class="sxs-lookup"><span data-stu-id="f7480-124">Deleting hello VM only deletes hello metadata, hello reference of hello VM within Azure.</span></span> <span data-ttu-id="f7480-125">les disques virtuels Hello sont conservés lors de la suppression de hello machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="f7480-125">hello virtual disks are retained when hello VM is deleted:</span></span>
   
   * <span data-ttu-id="f7480-126">Sélectionnez hello VM Bonjour portail Azure, cliquez sur *supprimer*:</span><span class="sxs-lookup"><span data-stu-id="f7480-126">Select hello VM in hello Azure portal, click *Delete*:</span></span>
     
     ![Supprimer une machine virtuelle existante](./media/reset-local-password-without-agent/delete_vm.png)
2. <span data-ttu-id="f7480-128">Attachez toohello de disque du système d’exploitation de la machine virtuelle de source de hello résolution des problèmes de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f7480-128">Attach hello source VM’s OS disk toohello troubleshooting VM.</span></span> <span data-ttu-id="f7480-129">Hello, résolution des problèmes de la machine virtuelle doit être Bonjour même région que le disque du système d’exploitation de la machine virtuelle de source de hello (tel que `West US`) :</span><span class="sxs-lookup"><span data-stu-id="f7480-129">hello troubleshooting VM must be in hello same region as hello source VM's OS disk (such as `West US`):</span></span>
   
   * <span data-ttu-id="f7480-130">Sélectionnez hello résolution des problèmes de la machine virtuelle dans hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="f7480-130">Select hello troubleshooting VM in hello Azure portal.</span></span> <span data-ttu-id="f7480-131">Cliquez sur *Disques* | *Attacher existant* :</span><span class="sxs-lookup"><span data-stu-id="f7480-131">Click *Disks* | *Attach existing*:</span></span>
     
     ![Attachement d’un disque existant](./media/reset-local-password-without-agent/disks_attach_existing.png)
     
     <span data-ttu-id="f7480-133">Sélectionnez *fichier VHD* , puis sélectionnez le compte de stockage hello qui contient votre machine virtuelle source :</span><span class="sxs-lookup"><span data-stu-id="f7480-133">Select *VHD File* and then select hello storage account that contains your source VM:</span></span>
     
     ![Sélectionner le compte de stockage](./media/reset-local-password-without-agent/disks_select_storageaccount.PNG)
     
     <span data-ttu-id="f7480-135">Sélectionnez le conteneur source de hello.</span><span class="sxs-lookup"><span data-stu-id="f7480-135">Select hello source container.</span></span> <span data-ttu-id="f7480-136">conteneur de source de Hello est généralement *disques durs virtuels*:</span><span class="sxs-lookup"><span data-stu-id="f7480-136">hello source container is typically *vhds*:</span></span>
     
     ![Sélectionner le conteneur de stockage](./media/reset-local-password-without-agent/disks_select_container.png)
     
     <span data-ttu-id="f7480-138">Sélectionnez hello tooattach de disque dur virtuel du système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="f7480-138">Select hello OS vhd tooattach.</span></span> <span data-ttu-id="f7480-139">Cliquez sur *sélectionnez* processus de hello toocomplete :</span><span class="sxs-lookup"><span data-stu-id="f7480-139">Click *Select* toocomplete hello process:</span></span>
     
     ![Sélectionner le disque virtuel source](./media/reset-local-password-without-agent/disks_select_source_vhd.png)
3. <span data-ttu-id="f7480-141">Se connecter toohello résolution des problèmes de la machine virtuelle à l’aide du Bureau à distance et vérifiez le disque du système d’exploitation de la machine virtuelle de source de hello est visible :</span><span class="sxs-lookup"><span data-stu-id="f7480-141">Connect toohello troubleshooting VM using Remote Desktop and ensure hello source VM's OS disk is visible:</span></span>
   
   * <span data-ttu-id="f7480-142">Sélectionnez hello résolution des problèmes de la machine virtuelle dans hello portail Azure, cliquez sur *connexion*.</span><span class="sxs-lookup"><span data-stu-id="f7480-142">Select hello troubleshooting VM in hello Azure portal and click *Connect*.</span></span>
   * <span data-ttu-id="f7480-143">Ouvrez le fichier RDP hello qui télécharge.</span><span class="sxs-lookup"><span data-stu-id="f7480-143">Open hello RDP file that downloads.</span></span> <span data-ttu-id="f7480-144">Entrez les nom d’utilisateur hello et le mot de passe hello résolution des problèmes de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f7480-144">Enter hello username and password of hello troubleshooting VM.</span></span>
   * <span data-ttu-id="f7480-145">Dans l’Explorateur de fichiers, recherchez le disque de données hello que vous attaché.</span><span class="sxs-lookup"><span data-stu-id="f7480-145">In File Explorer, look for hello data disk you attached.</span></span> <span data-ttu-id="f7480-146">Si hello source de que disque dur virtuel est hello toohello de disque attaché uniquement les données résolution des problèmes de la machine virtuelle, il convient de lecteur F: de hello :</span><span class="sxs-lookup"><span data-stu-id="f7480-146">If hello source VM’s VHD is hello only data disk attached toohello troubleshooting VM, it should be hello F: drive:</span></span>
     
     ![Afficher le disque de données attaché](./media/reset-local-password-without-agent/troubleshooting_vm_fileexplorer.png)
4. <span data-ttu-id="f7480-148">Créer `gpt.ini` dans `\Windows\System32\GroupPolicy` sur le lecteur de l’ordinateur virtuel de source de hello (si le fichier gpt.ini existe, renommez toogpt.ini.bak) :</span><span class="sxs-lookup"><span data-stu-id="f7480-148">Create `gpt.ini` in `\Windows\System32\GroupPolicy` on hello source VM’s drive (if gpt.ini exists, rename toogpt.ini.bak):</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="f7480-149">Assurez-vous que vous ne pas accidentellement créer hello fichiers dans C:\Windows suivants, hello lecteur du système d’exploitation pour hello résolution des problèmes de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f7480-149">Make sure that you do not accidentally create hello following files in C:\Windows, hello OS drive for hello troubleshooting VM.</span></span> <span data-ttu-id="f7480-150">Créer hello suivant des fichiers dans le lecteur de hello du système d’exploitation pour votre machine virtuelle qui est attaché en tant que disque de données source.</span><span class="sxs-lookup"><span data-stu-id="f7480-150">Create hello following files in hello OS drive for your source VM that is attached as a data disk.</span></span>
   > 
   > 
   
   * <span data-ttu-id="f7480-151">Ajouter hello lignes suivantes dans hello `gpt.ini` fichier que vous avez créé :</span><span class="sxs-lookup"><span data-stu-id="f7480-151">Add hello following lines into hello `gpt.ini` file you created:</span></span>
     
     ```
     [General]
     gPCFunctionalityVersion=2
     gPCMachineExtensionNames=[{42B5FAAE-6536-11D2-AE5A-0000F87571E3}{40B6664F-4972-11D1-A7CA-0000F87571E3}]
     Version=1
     ```
     
     ![Créer le fichier gpt.ini](./media/reset-local-password-without-agent/create_gpt_ini.png)
5. <span data-ttu-id="f7480-153">Créez `scripts.ini` dans `\Windows\System32\GroupPolicy\Machine\Scripts`.</span><span class="sxs-lookup"><span data-stu-id="f7480-153">Create `scripts.ini` in `\Windows\System32\GroupPolicy\Machine\Scripts`.</span></span> <span data-ttu-id="f7480-154">Vérifiez que les dossiers masqués sont affichés.</span><span class="sxs-lookup"><span data-stu-id="f7480-154">Make sure hidden folders are shown.</span></span> <span data-ttu-id="f7480-155">Si nécessaire, créez hello `Machine` ou `Scripts` dossiers.</span><span class="sxs-lookup"><span data-stu-id="f7480-155">If needed, create hello `Machine` or `Scripts` folders.</span></span>
   
   * <span data-ttu-id="f7480-156">Ajouter hello suivant hello de lignes `scripts.ini` fichier que vous avez créé :</span><span class="sxs-lookup"><span data-stu-id="f7480-156">Add hello following lines hello `scripts.ini` file you created:</span></span>
     
     ```
     [Startup]
     0CmdLine=C:\Windows\System32\FixAzureVM.cmd
     0Parameters=
     ```
     
     ![Créer scripts.ini](./media/reset-local-password-without-agent/create_scripts_ini.png)
6. <span data-ttu-id="f7480-158">Créer `FixAzureVM.cmd` dans `\Windows\System32` avec hello suivant le contenu, en remplaçant `<username>` et `<newpassword>` avec vos propres valeurs :</span><span class="sxs-lookup"><span data-stu-id="f7480-158">Create `FixAzureVM.cmd` in `\Windows\System32` with hello following contents, replacing `<username>` and `<newpassword>` with your own values:</span></span>
   
    ```
    net user <username> <newpassword> /add
    net localgroup administrators <username> /add
    net localgroup "remote desktop users" <username> /add

    ```

    ![Créer FixAzureVM.cmd](./media/reset-local-password-without-agent/create_fixazure_cmd.png)
   
    <span data-ttu-id="f7480-160">Vous devez remplir les exigences de complexité de mot de passe hello configurée pour votre machine virtuelle lors de la définition du nouveau mot de passe hello.</span><span class="sxs-lookup"><span data-stu-id="f7480-160">You must meet hello configured password complexity requirements for your VM when defining hello new password.</span></span>
7. <span data-ttu-id="f7480-161">Dans le portail Azure, détachez le disque hello hello résolution des problèmes de la machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="f7480-161">In Azure portal, detach hello disk from hello troubleshooting VM:</span></span>
   
   * <span data-ttu-id="f7480-162">Sélectionnez hello résolution des problèmes de la machine virtuelle dans hello portail Azure, cliquez sur *disques*.</span><span class="sxs-lookup"><span data-stu-id="f7480-162">Select hello troubleshooting VM in hello Azure portal, click *Disks*.</span></span>
   * <span data-ttu-id="f7480-163">Disque de données Sélectionnez hello attaché à l’étape 2, cliquez sur *détachement*:</span><span class="sxs-lookup"><span data-stu-id="f7480-163">Select hello data disk attached in step 2, click *Detach*:</span></span>
     
     ![Détacher le disque](./media/reset-local-password-without-agent/detach_disk.png)
8. <span data-ttu-id="f7480-165">Avant de créer une machine virtuelle, obtenez le disque du système d’exploitation source hello URI tooyour :</span><span class="sxs-lookup"><span data-stu-id="f7480-165">Before you create a VM, obtain hello URI tooyour source OS disk:</span></span>
   
   * <span data-ttu-id="f7480-166">Cliquez sur le compte de stockage hello sélectionnez Bonjour portail Azure, *BLOB*.</span><span class="sxs-lookup"><span data-stu-id="f7480-166">Select hello storage account in hello Azure portal, click *Blobs*.</span></span>
   * <span data-ttu-id="f7480-167">Sélectionnez le conteneur de hello.</span><span class="sxs-lookup"><span data-stu-id="f7480-167">Select hello container.</span></span> <span data-ttu-id="f7480-168">conteneur de source de Hello est généralement *disques durs virtuels*:</span><span class="sxs-lookup"><span data-stu-id="f7480-168">hello source container is typically *vhds*:</span></span>
     
     ![Sélectionner l’objet blob de compte de stockage](./media/reset-local-password-without-agent/select_storage_details.png)
     
     <span data-ttu-id="f7480-170">Sélectionnez votre disque dur virtuel du système d’exploitation de machine virtuelle source et cliquez sur hello *copie* toohello suivant du bouton *URL* nom :</span><span class="sxs-lookup"><span data-stu-id="f7480-170">Select your source VM OS VHD and click hello *Copy* button next toohello *URL* name:</span></span>
     
     ![Copier l’URI de disque](./media/reset-local-password-without-agent/copy_source_vhd_uri.png)
9. <span data-ttu-id="f7480-172">Créer une machine virtuelle à partir du disque du système d’exploitation de la machine virtuelle de source de hello :</span><span class="sxs-lookup"><span data-stu-id="f7480-172">Create a VM from hello source VM’s OS disk:</span></span>
   
   * <span data-ttu-id="f7480-173">Utilisez [ce modèle Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) toocreate une machine virtuelle à partir d’un disque dur virtuel spécialisé.</span><span class="sxs-lookup"><span data-stu-id="f7480-173">Use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) toocreate a VM from a specialized VHD.</span></span> <span data-ttu-id="f7480-174">Cliquez sur hello `Deploy tooAzure` hello tooopen de bouton portail Azure avec des détails basés sur des modèles de hello remplie pour vous.</span><span class="sxs-lookup"><span data-stu-id="f7480-174">Click hello `Deploy tooAzure` button tooopen hello Azure portal with hello templated details populated for you.</span></span>
   * <span data-ttu-id="f7480-175">Si vous souhaitez tooretain tous les paramètres précédents hello pour hello machine virtuelle, sélectionnez *modifier un modèle de* tooprovide votre réseau virtuel existant, un sous-réseau, une carte réseau ou une adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="f7480-175">If you want tooretain all hello previous settings for hello VM, select *Edit template* tooprovide your existing VNet, subnet, network adapter, or public IP.</span></span>
   * <span data-ttu-id="f7480-176">Bonjour `OSDISKVHDURI` zone de texte du paramètre, hello coller l’URI de votre disque dur virtuel source obtenir Bonjour précédant l’étape :</span><span class="sxs-lookup"><span data-stu-id="f7480-176">In hello `OSDISKVHDURI` parameter text box, paste hello URI of your source VHD obtain in hello preceding step:</span></span>
     
     ![Créer une machine virtuelle à partir d’un modèle](./media/reset-local-password-without-agent/create_new_vm_from_template.png)
10. <span data-ttu-id="f7480-178">Après la nouvelle machine virtuelle est en cours d’exécution de hello, se connecter toohello machine virtuelle à l’aide du Bureau à distance avec le nouveau mot de passe hello spécifié dans hello `FixAzureVM.cmd` script.</span><span class="sxs-lookup"><span data-stu-id="f7480-178">After hello new VM is running, connect toohello VM using Remote Desktop with hello new password you specified in hello `FixAzureVM.cmd` script.</span></span>
11. <span data-ttu-id="f7480-179">À partir de votre session à distance de toohello nouvelle machine virtuelle, hello remove suivant fichiers tooclean d’environnement de hello :</span><span class="sxs-lookup"><span data-stu-id="f7480-179">From your remote session toohello new VM, remove hello following files tooclean up hello environment:</span></span>
    
    * <span data-ttu-id="f7480-180">Dans %windir%\System32</span><span class="sxs-lookup"><span data-stu-id="f7480-180">From %windir%\System32</span></span>
      * <span data-ttu-id="f7480-181">supprimez FixAzureVM.cmd</span><span class="sxs-lookup"><span data-stu-id="f7480-181">remove FixAzureVM.cmd</span></span>
    * <span data-ttu-id="f7480-182">Dans %windir%\System32\GroupPolicy\Machine\\</span><span class="sxs-lookup"><span data-stu-id="f7480-182">From %windir%\System32\GroupPolicy\Machine\\</span></span>
      * <span data-ttu-id="f7480-183">supprimez scripts.ini</span><span class="sxs-lookup"><span data-stu-id="f7480-183">remove scripts.ini</span></span>
    * <span data-ttu-id="f7480-184">Dans %windir%\System32\GroupPolicy</span><span class="sxs-lookup"><span data-stu-id="f7480-184">From %windir%\System32\GroupPolicy</span></span>
      * <span data-ttu-id="f7480-185">supprimer le fichier gpt.ini (le cas gpt.ini existait avant, et vous l’avez renommée toogpt.ini.bak, toogpt.ini précédent du fichier .bak hello renommer)</span><span class="sxs-lookup"><span data-stu-id="f7480-185">remove gpt.ini (if gpt.ini existed before, and you renamed it toogpt.ini.bak, rename hello .bak file back toogpt.ini)</span></span>

## <a name="next-steps"></a><span data-ttu-id="f7480-186">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f7480-186">Next steps</span></span>
<span data-ttu-id="f7480-187">Si vous ne pouvez pas toujours vous connecter à l’aide du Bureau à distance, consultez hello [guide de dépannage RDP](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f7480-187">If you still cannot connect using Remote Desktop, see hello [RDP troubleshooting guide](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="f7480-188">Hello [détaillées RDP guide de dépannage](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) examine la résolution des problèmes de méthodes au lieu des étapes spécifiques.</span><span class="sxs-lookup"><span data-stu-id="f7480-188">hello [detailed RDP troubleshooting guide](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) looks at troubleshooting methods rather than specific steps.</span></span> <span data-ttu-id="f7480-189">Vous pouvez également [ouvrir une demande de support Azure](https://azure.microsoft.com/support/options/) pour obtenir une assistance pratique.</span><span class="sxs-lookup"><span data-stu-id="f7480-189">You can also [open an Azure support request](https://azure.microsoft.com/support/options/) for hands-on assistance.</span></span>

