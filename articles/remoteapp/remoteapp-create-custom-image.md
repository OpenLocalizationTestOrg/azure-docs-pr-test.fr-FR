---
title: "aaaHow toocreate une image de modèle personnalisé pour Azure RemoteApp | Documents Microsoft"
description: "Découvrez comment l’image toocreate un modèle personnalisé pour Azure RemoteApp. Vous pouvez utiliser ce modèle avec une collection hybride ou cloud."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: b9ec5b51-f7cd-470b-8545-d0fd714c5982
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 9e3a0b2d3cc56177ea51406e6cecfe19ff235340
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-custom-template-image-for-azure-remoteapp"></a>Comment l’image toocreate un modèle personnalisé pour Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp ne sera plus disponible à partir du 31 août 2017. Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.
> 
> 

Azure RemoteApp utilise un toohost d’image de modèle Windows Server 2012 R2 tous les programmes hello que vous souhaitez tooshare avec vos utilisateurs. toocreate une image de modèle RemoteApp personnalisée, vous pouvez commencer par une image existante ou créez-en un. 

> [!TIP]
> Saviez-vous que vous pouvez créer une image à partir d’une machine virtuelle Azure ? Récit true et il réduit sur hello temps il prend tooimport hello image. Découvrez les étapes hello [ici](remoteapp-image-on-azurevm.md).
> 
> 

exigences de Hello d’image hello qui peuvent être téléchargés pour une utilisation avec Azure RemoteApp sont :

* taille de l’image Hello doit être un multiple de nombre de Mo. Si vous essayez de tooupload une image qui n’est pas un multiple exact, le téléchargement de hello échoue.
* taille de l’image Hello doit être 127 Go ou plus petit.
* Elle doit se trouver dans un fichier VHD (pour l'instant, les fichiers VHDX [disques durs virtuels Hyper-V] ne sont pas pris en charge).
* Hello disque dur virtuel ne doit pas être un ordinateur virtuel de génération 2.
* Hello disque dur virtuel peut être de taille fixe ou expansion dynamique. Un disque dur virtuel de taille dynamique est recommandé, car il prend moins tooAzure tooupload de temps qu’un fichier de disque dur virtuel de taille fixe.
* disque de Hello doit être initialisé à l’aide du style de partitionnement hello enregistrement de démarrage principal (MBR). Hello style de partition GUID partition GPT (table) n’est pas pris en charge.
* Hello disque dur virtuel doit contenir une seule installation de Windows Server 2012 R2. Il peut contenir plusieurs volumes, mais un seul contenant une installation de Windows.
* rôle d’ordinateur hôte de Session de bureau à distance (RDSH) Hello et la fonctionnalité expérience utilisateur hello doivent être installés.
* rôle du service Broker pour les connexions Bureau à distance Hello doit *pas* être installé.
* Hello EFS (ENCRYPTING file) doit être désactivée.
* Hello image doit être préparée avec Sysprep à l’aide des paramètres de hello **/oobe /generalize /shutdown** (ne pas utiliser hello **/mode : VM** paramètre).
* Le téléchargement de votre disque dur virtuel à partir d’une chaîne d’instantanés n’est pas pris en charge.

**Avant de commencer**

Éléments de hello toodo suivants avant de créer le service de hello sont nécessaires :

* [S'inscrire](https://azure.microsoft.com/services/remoteapp/) à RemoteApp.
* Créer un compte d’utilisateur dans Active Directory toouse en tant que compte de service RemoteApp de hello. Limitez les autorisations de hello pour ce compte pour qu’il puisse rejoindre uniquement domaine toohello de machines. Consultez [Configuration d'Azure Active Directory pour RemoteApp](remoteapp-ad.md) pour plus d'informations.
* Collecter des informations sur votre réseau local : adresse IP et périphérique VPN.
* Installer hello [Azure PowerShell](/powershell/azure/overview) module.
* Collecter des informations sur les utilisateurs hello auxquels vous souhaitez accéder toogrant à. Il peut s'agir d'informations sur le compte Microsoft ou sur le compte professionnel Active Directory pour les utilisateurs.

## <a name="create-a-template-image"></a>Création d'une image de modèle
Il s’agit hello étapes générales toocreate une nouvelle image de modèle à partir de zéro :

1. Recherchez une image ISO ou DVD de mise à jour de Windows Server 2012 R2.
2. Créez un disque dur virtuel.
3. Installez Windows Server 2012 R2.
4. Installez le rôle d’ordinateur hôte de Session de bureau à distance (RDSH) hello et la fonctionnalité expérience utilisateur hello.
5. Installez les fonctionnalités supplémentaires dont vos applications ont besoin.
6. Installez et configurez vos applications. applications de partage toomake plus faciles, ajouter des applications ou programmes que vous souhaitez tooshare toohello **Démarrer** menu de hello image, en particulier en **%systemdrive%\ProgramData\Microsoft\Windows\Start Menu\Programs.
7. Exécutez les éventuelles opérations de configuration Windows supplémentaires requises par vos applications.
8. Désactiver hello EFS (ENCRYPTING file).
9. **REQUIRED :** tooWindows mise à jour et installez toutes les mises à jour importantes.
10. Image de hello SYSPREP.

Hello des étapes détaillées pour la création d’une nouvelle image sont :

1. Recherchez une image ISO ou DVD de mise à jour de Windows Server 2012 R2.
2. Créez un fichier VHD à l'aide de la fonction Gestion des disques.
   
   1. Lancez la fonction Gestion des disques (diskmgmt.msc).
   2. Créez un disque dur virtuel de taille dynamique d'une taille minimale de 40 Go. (Estimation hello quantité d’espace nécessaire pour Windows, vos applications et des personnalisations. Windows serveur avec le rôle de postes de travail hello et la fonctionnalité expérience utilisateur installée nécessite environ 10 Go d’espace).
      
      1. Cliquez sur **Action > Créer un disque dur virtuel**.
      2. Spécifier l’emplacement de hello, la taille et le format de disque dur virtuel. Sélectionnez **Taille dynamique**, puis cliquez sur **OK**.
      
      Cette opération va prendre plusieurs secondes. Lorsque la création du disque dur virtuel de hello est terminée, vous devez voir un nouveau disque sans aucune lettre de lecteur et en état de « Non initialisé » dans la console de gestion des disques hello.
      
      * Cliquez sur le disque hello (pas l’espace non alloué de hello), puis cliquez sur **initialiser le disque**. Sélectionnez **MBR** (Master Boot Record) comme style de partition hello, puis cliquez sur **OK**.
      * Créer un nouveau volume : hello espace non alloué d’avec le bouton droit, puis cliquez sur **nouveau Volume Simple**. Vous pouvez accepter les valeurs par défaut hello dans l’Assistant de hello, mais assurez-vous que vous assignez un lecteur lettre tooavoid les problèmes potentiels lorsque vous téléchargez l’image de modèle hello.
      * Cliquez sur le disque de hello, puis cliquez sur **détacher un disque dur virtuel**.
3. Installation de Windows Server 2012 R2 :
   
   1. Créez une machine virtuelle. Utilisez hello les Assistant Nouvel ordinateur virtuel dans le Gestionnaire Hyper-V ou le Client Hyper-V.
      1. Dans la page spécifier la génération de hello, choisissez **génération 1**.
      2. Sur la page de connecter un disque dur virtuel hello, sélectionnez **utiliser un disque dur virtuel existant**, puis accédez toohello disque dur virtuel créé à l’étape précédente de hello.
      3. Sur la page d’Options d’Installation Bonjour, sélectionnez **installer un système d’exploitation à partir d’un CD/ce dernier**, puis sélectionnez emplacement hello de votre support d’installation de Windows Server 2012 R2.
      4. Choisissez les autres options de hello Assistant tooinstall nécessaire Windows et de vos applications. Terminer l’Assistant hello.
   2. Fin hello Assistant, modifier les paramètres de la machine virtuelle de hello hello et apporter d’autres modifications nécessaires tooinstall Windows et vos programmes, telles que nombre hello de processeurs virtuels et puis cliquez sur **OK**.
   3. Connecter l’ordinateur virtuel de toohello et installez Windows Server 2012 R2.
4. Installer le rôle d’ordinateur hôte de Session de bureau à distance (RDSH) hello et la fonctionnalité expérience utilisateur hello :
   1. Lancez le Gestionnaire de serveur.
   2. Cliquez sur **Ajout de rôles et fonctionnalités** sur l’écran d’accueil hello ou à partir de hello **gérer** menu.
   3. Cliquez sur **suivant** sur la page de hello avant de commencer.
   4. Sélectionnez **Installation basée sur un rôle ou une fonctionnalité**, puis cliquez sur **Suivant**.
   5. Sélectionnez l’ordinateur local de hello à partir de la liste de hello, puis cliquez sur **suivant**.
   6. Sélectionnez **Services Bureau à distance**, puis cliquez sur **Suivant**.
   7. Développez l'entrée **Interfaces utilisateur et infrastructure** et sélectionnez **Expérience utilisateur**.
   8. Sélectionnez **Ajouter des fonctionnalités**, puis cliquez sur **Suivant**.
   9. Dans la page Services Bureau à distance de hello, cliquez sur **suivant**.
   10. Cliquez sur **Hôte de session Bureau à distance**.
   11. Sélectionnez **Ajouter des fonctionnalités**, puis cliquez sur **Suivant**.
   12. Sur la page sélections d’installation hello confirmer, sélectionnez **redémarrez le serveur de destination hello automatiquement si nécessaire**, puis cliquez sur **Oui** sur hello avertissement relatif au redémarrage.
   13. Cliquez sur **Installer**. Hello ordinateur redémarre.
5. Installer des fonctionnalités supplémentaires requises par vos applications, telles que hello .NET Framework 3.5. fonctionnalités de hello tooinstall, exécutez hello Ajout de rôles et fonctionnalités Assistant.
6. Installez et configurez les programmes de hello et les applications que vous souhaitez toopublish via RemoteApp.

> [!IMPORTANT]
> Installer le rôle de postes de travail hello avant d’installer des applications tooensure que tous les problèmes de compatibilité des applications sont détectés hello image avant est téléchargement tooRemoteApp.
> 
> Assurez-vous d’une application tooyour de raccourci (**.lnk** fichier) s’affiche dans hello **Démarrer** menu pour tous les utilisateurs (%systemdrive%\ProgramData\Microsoft\Windows\Start Menu\Programs). Vérifiez également cette icône hello vous consultez Bonjour **Démarrer** menu est ce que vous voulez toosee d’utilisateurs. Sinon, changez-la. (Vous ne spécifiez aucune *ont* le menu Démarrer toohello tooadd hello application, mais il rend beaucoup plus facile application de hello toopublish dans RemoteApp. Dans le cas contraire, vous devez chemin d’installation de hello tooprovide pour l’application hello lorsque vous publiez l’application hello.)
> 
> 

1. Exécutez les éventuelles opérations de configuration Windows supplémentaires requises par vos applications.
2. Désactiver hello EFS (ENCRYPTING file). Exécutez hello suivant de commande à partir d’une fenêtre de commande avec élévation de privilèges :
   
     Fsutil behavior set disableencryption 1
   
   Ou bien, vous pouvez définir ou ajouter hello valeur DWORD dans le Registre de hello suivante :
   
     HKLM\System\CurrentControlSet\Control\FileSystem\NtfsDisableEncryption = 1
3. Si vous générez votre image à l’intérieur d’une machine virtuelle Azure, renommez hello  **\%windir%\Panther\Unattend.xml** de fichiers, comme cela bloquera le script de téléchargement hello utilisée ultérieurement à partir du travail. Renommer hello tooUnattend.old de ce fichier afin que vous aurez toujours les fichiers hello en cas de besoin toorevert votre déploiement.
4. Accédez tooWindows mise à jour et installer toutes les mises à jour importantes. Les mises à jour, vous devrez peut-être toorun Windows Update tooget de plusieurs fois. (Parfois, vous installez une mise à jour et celle-ci requiert elle-même une mise à jour.)
5. Image de hello SYSPREP. À une invite de commandes avec élévation de privilèges, exécutez hello de commande suivante :
   
   **C:\Windows\System32\sysprep\sysprep.exe /generalize /oobe /shutdown**
   
   **Remarque :** n’utilisez pas hello **/mode : VM** commutateur Hello SYSPREP commande même s’il s’agit d’un ordinateur virtuel.

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez votre image de modèle personnalisé, vous devez tooupload que tooyour image collection RemoteApp. Utilisez les informations de hello Bonjour suivant articles toocreate votre collection :

* [Comment toocreate une collection hybride de RemoteApp](remoteapp-create-hybrid-deployment.md)
* [Comment toocreate une collection de cloud de RemoteApp](remoteapp-create-cloud-deployment.md)

