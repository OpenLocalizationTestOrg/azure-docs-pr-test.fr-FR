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
# <a name="how-tooreset-local-windows-password-for-azure-vm"></a>Comment tooreset Windows mot de passe local pour la machine virtuelle Azure
Vous pouvez réinitialiser hello Windows mot de passe local d’une machine virtuelle dans Azure à l’aide de hello [portail Azure ou Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) fournie hello invité de Azure agent est installée. Cette méthode est hello principal moyen tooreset un mot de passe pour une machine virtuelle Azure. Si vous rencontrez des problèmes avec l’agent invité de Azure a hello ne répond ne pas ou le basculement tooinstall après avoir téléchargé une image personnalisée, vous pouvez réinitialiser manuellement un mot de passe Windows. Cet article décrit en détail comment tooreset un mot de passe du compte local en attachant hello tooanother de disque virtuel de la source du système d’exploitation machine virtuelle. 

> [!WARNING]
> N’utilisez ce processus qu’en dernier recours. Essayez toujours d’un mot de passe à l’aide de hello tooreset [portail Azure ou Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) première.
> 
> 

## <a name="overview-of-hello-process"></a>Vue d’ensemble du processus de hello
étapes de base Hello pour l’exécution d’un mot de passe local réinitialisée pour un ordinateur virtuel Windows Azure lorsqu’il n’existe aucun agent invité de Azure d’accès toohello est la suivante :

* Supprimer la machine virtuelle de la source hello. les disques virtuels Hello sont conservés.
* Attacher le disque tooanother machine virtuelle de la machine virtuelle de source de hello du système d’exploitation sur hello même emplacement au sein de votre abonnement Azure. Cette machine virtuelle est hello visé tooas résolution des problèmes de la machine virtuelle.
* Hello, résolution des problèmes de la machine virtuelle, créez des fichiers de configuration sur le disque du système d’exploitation de la machine virtuelle de source de hello.
* Détacher un disque de système d’exploitation hello VM de hello, résolution des problèmes de la machine virtuelle.
* Utilisez un toocreate de modèle de gestionnaire de ressources une machine virtuelle, à l’aide du disque virtuel d’origine de hello.
* Lorsque les fichiers de configuration hello hello nouvelle machine virtuelle démarre, vous créez un mot de passe hello mise à jour de l’utilisateur de hello requis.

## <a name="detailed-steps"></a>Procédure détaillée
Essayez toujours d’un mot de passe à l’aide de hello tooreset [portail Azure ou Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) avant d’essayer de hello comme suit. Avant de commencer, vérifiez que vous disposez d’une sauvegarde de votre machine virtuelle. 

1. Supprimer hello affectées de machine virtuelle dans le portail Azure. Suppression hello VM supprime uniquement les métadonnées hello, référence hello Hello machine virtuelle dans Azure. les disques virtuels Hello sont conservés lors de la suppression de hello machine virtuelle :
   
   * Sélectionnez hello VM Bonjour portail Azure, cliquez sur *supprimer*:
     
     ![Supprimer une machine virtuelle existante](./media/reset-local-password-without-agent/delete_vm.png)
2. Attachez toohello de disque du système d’exploitation de la machine virtuelle de source de hello résolution des problèmes de la machine virtuelle. Hello, résolution des problèmes de la machine virtuelle doit être Bonjour même région que le disque du système d’exploitation de la machine virtuelle de source de hello (tel que `West US`) :
   
   * Sélectionnez hello résolution des problèmes de la machine virtuelle dans hello portail Azure. Cliquez sur *Disques* | *Attacher existant* :
     
     ![Attachement d’un disque existant](./media/reset-local-password-without-agent/disks_attach_existing.png)
     
     Sélectionnez *fichier VHD* , puis sélectionnez le compte de stockage hello qui contient votre machine virtuelle source :
     
     ![Sélectionner le compte de stockage](./media/reset-local-password-without-agent/disks_select_storageaccount.PNG)
     
     Sélectionnez le conteneur source de hello. conteneur de source de Hello est généralement *disques durs virtuels*:
     
     ![Sélectionner le conteneur de stockage](./media/reset-local-password-without-agent/disks_select_container.png)
     
     Sélectionnez hello tooattach de disque dur virtuel du système d’exploitation. Cliquez sur *sélectionnez* processus de hello toocomplete :
     
     ![Sélectionner le disque virtuel source](./media/reset-local-password-without-agent/disks_select_source_vhd.png)
3. Se connecter toohello résolution des problèmes de la machine virtuelle à l’aide du Bureau à distance et vérifiez le disque du système d’exploitation de la machine virtuelle de source de hello est visible :
   
   * Sélectionnez hello résolution des problèmes de la machine virtuelle dans hello portail Azure, cliquez sur *connexion*.
   * Ouvrez le fichier RDP hello qui télécharge. Entrez les nom d’utilisateur hello et le mot de passe hello résolution des problèmes de la machine virtuelle.
   * Dans l’Explorateur de fichiers, recherchez le disque de données hello que vous attaché. Si hello source de que disque dur virtuel est hello toohello de disque attaché uniquement les données résolution des problèmes de la machine virtuelle, il convient de lecteur F: de hello :
     
     ![Afficher le disque de données attaché](./media/reset-local-password-without-agent/troubleshooting_vm_fileexplorer.png)
4. Créer `gpt.ini` dans `\Windows\System32\GroupPolicy` sur le lecteur de l’ordinateur virtuel de source de hello (si le fichier gpt.ini existe, renommez toogpt.ini.bak) :
   
   > [!WARNING]
   > Assurez-vous que vous ne pas accidentellement créer hello fichiers dans C:\Windows suivants, hello lecteur du système d’exploitation pour hello résolution des problèmes de la machine virtuelle. Créer hello suivant des fichiers dans le lecteur de hello du système d’exploitation pour votre machine virtuelle qui est attaché en tant que disque de données source.
   > 
   > 
   
   * Ajouter hello lignes suivantes dans hello `gpt.ini` fichier que vous avez créé :
     
     ```
     [General]
     gPCFunctionalityVersion=2
     gPCMachineExtensionNames=[{42B5FAAE-6536-11D2-AE5A-0000F87571E3}{40B6664F-4972-11D1-A7CA-0000F87571E3}]
     Version=1
     ```
     
     ![Créer le fichier gpt.ini](./media/reset-local-password-without-agent/create_gpt_ini.png)
5. Créez `scripts.ini` dans `\Windows\System32\GroupPolicy\Machine\Scripts`. Vérifiez que les dossiers masqués sont affichés. Si nécessaire, créez hello `Machine` ou `Scripts` dossiers.
   
   * Ajouter hello suivant hello de lignes `scripts.ini` fichier que vous avez créé :
     
     ```
     [Startup]
     0CmdLine=C:\Windows\System32\FixAzureVM.cmd
     0Parameters=
     ```
     
     ![Créer scripts.ini](./media/reset-local-password-without-agent/create_scripts_ini.png)
6. Créer `FixAzureVM.cmd` dans `\Windows\System32` avec hello suivant le contenu, en remplaçant `<username>` et `<newpassword>` avec vos propres valeurs :
   
    ```
    net user <username> <newpassword> /add
    net localgroup administrators <username> /add
    net localgroup "remote desktop users" <username> /add

    ```

    ![Créer FixAzureVM.cmd](./media/reset-local-password-without-agent/create_fixazure_cmd.png)
   
    Vous devez remplir les exigences de complexité de mot de passe hello configurée pour votre machine virtuelle lors de la définition du nouveau mot de passe hello.
7. Dans le portail Azure, détachez le disque hello hello résolution des problèmes de la machine virtuelle :
   
   * Sélectionnez hello résolution des problèmes de la machine virtuelle dans hello portail Azure, cliquez sur *disques*.
   * Disque de données Sélectionnez hello attaché à l’étape 2, cliquez sur *détachement*:
     
     ![Détacher le disque](./media/reset-local-password-without-agent/detach_disk.png)
8. Avant de créer une machine virtuelle, obtenez le disque du système d’exploitation source hello URI tooyour :
   
   * Cliquez sur le compte de stockage hello sélectionnez Bonjour portail Azure, *BLOB*.
   * Sélectionnez le conteneur de hello. conteneur de source de Hello est généralement *disques durs virtuels*:
     
     ![Sélectionner l’objet blob de compte de stockage](./media/reset-local-password-without-agent/select_storage_details.png)
     
     Sélectionnez votre disque dur virtuel du système d’exploitation de machine virtuelle source et cliquez sur hello *copie* toohello suivant du bouton *URL* nom :
     
     ![Copier l’URI de disque](./media/reset-local-password-without-agent/copy_source_vhd_uri.png)
9. Créer une machine virtuelle à partir du disque du système d’exploitation de la machine virtuelle de source de hello :
   
   * Utilisez [ce modèle Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) toocreate une machine virtuelle à partir d’un disque dur virtuel spécialisé. Cliquez sur hello `Deploy tooAzure` hello tooopen de bouton portail Azure avec des détails basés sur des modèles de hello remplie pour vous.
   * Si vous souhaitez tooretain tous les paramètres précédents hello pour hello machine virtuelle, sélectionnez *modifier un modèle de* tooprovide votre réseau virtuel existant, un sous-réseau, une carte réseau ou une adresse IP publique.
   * Bonjour `OSDISKVHDURI` zone de texte du paramètre, hello coller l’URI de votre disque dur virtuel source obtenir Bonjour précédant l’étape :
     
     ![Créer une machine virtuelle à partir d’un modèle](./media/reset-local-password-without-agent/create_new_vm_from_template.png)
10. Après la nouvelle machine virtuelle est en cours d’exécution de hello, se connecter toohello machine virtuelle à l’aide du Bureau à distance avec le nouveau mot de passe hello spécifié dans hello `FixAzureVM.cmd` script.
11. À partir de votre session à distance de toohello nouvelle machine virtuelle, hello remove suivant fichiers tooclean d’environnement de hello :
    
    * Dans %windir%\System32
      * supprimez FixAzureVM.cmd
    * Dans %windir%\System32\GroupPolicy\Machine\
      * supprimez scripts.ini
    * Dans %windir%\System32\GroupPolicy
      * supprimer le fichier gpt.ini (le cas gpt.ini existait avant, et vous l’avez renommée toogpt.ini.bak, toogpt.ini précédent du fichier .bak hello renommer)

## <a name="next-steps"></a>Étapes suivantes
Si vous ne pouvez pas toujours vous connecter à l’aide du Bureau à distance, consultez hello [guide de dépannage RDP](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Hello [détaillées RDP guide de dépannage](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) examine la résolution des problèmes de méthodes au lieu des étapes spécifiques. Vous pouvez également [ouvrir une demande de support Azure](https://azure.microsoft.com/support/options/) pour obtenir une assistance pratique.

