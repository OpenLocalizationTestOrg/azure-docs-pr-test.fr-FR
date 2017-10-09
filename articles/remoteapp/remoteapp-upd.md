---
title: "aaaHow est Azure RemoteApp enregistrer les paramètres et données utilisateur ? | Microsoft Docs"
description: "Découvrez comment Azure RemoteApp enregistre les données utilisateur à l’aide du disque de profil utilisateur hello."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: e125af62-5c1a-4186-a238-52f537f7bb34
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: dccebc7861e8a0d87cb3ee174f399a2df7fe023c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-azure-remoteapp-save-user-data-and-settings"></a>Comment Azure RemoteApp enregistre-t-il les paramètres et les données utilisateur ?
> [!IMPORTANT]
> Azure RemoteApp ne sera plus disponible à partir du 31 août 2017. Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.
> 
> 

Azure RemoteApp enregistre l'identité de l'utilisateur et les personnalisations entre les périphériques et les sessions. Ces données utilisateur sont stockées dans un disque par utilisateur et par collection, appelé disque de profil utilisateur (UPD). disque de Hello suit hello utilisateur et garantit l’utilisateur de hello possède une expérience cohérente, quel que soit l’endroit où ils se connectent.

Disques de profil utilisateur sont totalement transparente toohello utilisateur : utilisateurs enregistrer le dossier de Documents tootheir documents (sur ce qui s’affiche toobe un lecteur local) et modifier leurs paramètres d’application comme d’habitude. AT hello même les paramètres de temps, toutes les personnels sont conservés lors de la connexion tooAzure RemoteApp à partir de n’importe quel appareil. Tous les utilisateurs de hello voit est leurs données Bonjour même endroit.

Chaque UPD offre 50 Go de stockage persistant et contient à la fois les paramètres d'application et les données utilisateur. 

Continuez votre lecture pour obtenir des détails spécifiques sur les données de profil utilisateur.

> [!NOTE]
> Devez toodisable hello UPD ? À présent, vous pouvez le faire. Consultez le billet de blog de Pavithra, [Désactiver les disques de profil utilisateur (UPD) dans Azure RemoteApp](https://blogs.technet.microsoft.com/enterprisemobility/2015/11/11/disable-user-profile-disks-upds-in-azure-remoteapp/), pour plus d’informations.
> 
> 

## <a name="how-can-an-admin-get-toohello-data"></a>Comment un administrateur peut obtenir les données toohello ?
Si vous avez besoin des données de salutation tooaccess pour l’une de vos utilisateurs (pour la récupération d’urgence ou si les utilisateurs hello quitte hello société), contactez le Support d’Azure et fournissent des informations d’abonnement hello pour la collection de hello et identité de l’utilisateur hello. équipe de Azure RemoteApp Hello vous fournira un disque dur virtuel de toohello URL. Téléchargez ce disque dur virtuel et récupérez les documents ou fichiers dont vous avez besoin. Notez ce disque dur virtuel hello est 50 Go, afin qu’elle nécessitera une toodownload bits il.

## <a name="is-hello-data-backed-up"></a>Les données de salutation sont sauvegardées ?
Oui, nous enregistrer une sauvegarde des données d’utilisateur hello par emplacement géographique. Hello données est en lecture seule et peuvent être accessibles dans hello même façon que les données régulières hello serait (contacter Azure RemoteApp tooget il), si le centre de données principal hello est arrêté. les données de salutation sont l’emplacement de sauvegarde copiés toohello en temps réel, et nous ne pas conserver des copies des versions différentes. Par conséquent, à la corruption de données, ne sera pas en mesure de toorestore il tooa anciennement version correcte, mais si Centre de données principal hello est arrêté, vous serez en mesure de tooget les données d’utilisateur à partir de hello autre emplacement.

## <a name="how-do-users-see-hello-upd-on-hello-server-side"></a>Comment les utilisateurs Voir hello UPD côté serveur de hello ?
Chaque utilisateur aura son propre annuaire sur serveur hello qui mappe tootheir UPD : c:\Users\username.

## <a name="whats-hello-best-way-toouse-outlook-and-upd"></a>Qu’est hello meilleure manière toouse Outlook et UPD ?
Azure RemoteApp enregistre l’état de Outlook de hello (boîtes aux lettres, pst) entre les sessions. tooenable, nous devons hello toobe PST stockée dans les données de profil utilisateur hello (c:\users\<nom d’utilisateur >). Il s’agit d’emplacement par défaut de hello pour les données hello, par conséquent, tant que vous ne modifiez pas l’emplacement de hello, les données de salutation seront conservés entre les sessions.

Nous vous recommandons également d'utiliser le mode « mise en cache » dans Outlook et d'utiliser le mode « serveur/en ligne » pour la recherche.

Consultez [cet article](remoteapp-outlook.md) pour plus d’informations sur l’utilisation d’Outlook et d’Azure RemoteApp.

## <a name="what-about-redirection"></a>Qu'en est-il de la redirection ?
Vous pouvez configurer Azure RemoteApp toolet utilisateurs accéder aux périphériques locaux en configurant [redirection](remoteapp-redirection.md). Périphériques locaux seront en mesure de tooaccess données hello hello UPD.

## <a name="can-i-use-my-upd-as-a-network-share"></a>Puis-je utiliser mon UPD comme partage réseau ?
Non. Les UPD ne peuvent pas être utilisés comme partage réseau. Un UPD est uniquement disponible toohello utilisateur lorsque l’utilisateur de hello est activement connecté tooAzure RemoteApp.

## <a name="if-i-delete-a-user-from-a-collection-is-their-upd-deleted"></a>Si je supprime un utilisateur d'une collection, son UPD est-il supprimé ?
Non, lorsque vous supprimez un utilisateur, nous ne supprimez pas automatiquement hello UPD - au lieu de cela, nous stockons les données de salutation tant que vous supprimez la collection de hello. 90 jours après la suppression de la collection de hello, nous supprimons des tous les. 

Si vous devez toodelete une UPD à partir d’une collection, contacter Azure RemoteApp - nous pouvons supprimer UPD à partir de notre côté.

## <a name="can-i-access-my-users-upds-either-current-or-deleted-users"></a>Puis-je accéder aux UPD de mes utilisateurs (utilisateurs actuels ou supprimés) ?
Oui, si vous contactez [Azure RemoteApp](mailto:remoteappforum@microsoft.com), nous pouvons configurer vous avec une URL tooaccess les données de salutation. Vous aurez sur toodownload de 10 heures des données ou des fichiers à partir de hello UPD avant l’expiration de l’accès hello.

## <a name="are-upds-available-offline"></a>Les UPD sont-ils disponibles hors connexion ?
Maintenant, nous n’assurons pas tooUPDs accès hors connexion, au-delà de la fenêtre d’accès de 10 heures hello décrite ci-dessus. Cela signifie que nous n’avons pas actuellement un tooprovide moyen des accès pour les tâches suffisamment longue toocomplete plus compliqué, comme un logiciel antivirus en cours d’exécution sur de hello ou l’accès aux données pour un audit.

## <a name="do-registry-key-settings-persist"></a>Les paramètres de clé de registre sont-ils conservés ?
Oui, écriture tooHKEY_Current_User participe hello UPD.

## <a name="can-i-disable-upds-for-a-collection"></a>Puis-je désactiver les UPD d’une collection ?
Oui, vous pouvez demander un abonnement Azure RemoteApp toodisable des, mais vous ne pouvez pas effectuer cela vous-même. Cela signifie que des seront désactivées pour toutes les collections dans l’abonnement de hello.

Vous souhaiterez peut-être des toodisable dans un des hello suivant situations : 

* Vous avez besoin d’un accès et d’un contrôle complet des données utilisateur (aux fins d’audit et de vérification ; p. ex., institutions financières).
* Vous avez 3 rd-party utilisateur profil de gestion des solutions locales et souhaitez toocontinue leur utilisation dans votre déploiement d’Azure RemoteApp appartenant au domaine. Cela nécessiterait hello profil agent toobe est chargé dans l’image de hello gold. 
* Vous n’avez pas besoin d’un stockage de données local ou que vous disposez de toutes les données en hello cloud ou partage de fichiers et que vous souhaitez que l’enregistrement de toocontrol de données localement à l’aide d’Azure RemoteApp.

Consultez [Désactiver les disques de profil utilisateur (UPD) dans Azure RemoteApp](https://blogs.technet.microsoft.com/enterprisemobility/2015/11/11/disable-user-profile-disks-upds-in-azure-remoteapp/) pour plus d’informations.

## <a name="can-i-restrict-users-from-saving-data-toohello-system-drive"></a>Puis-je restreindre les utilisateurs à partir de l’enregistrement de lecteur de données toohello système ?
Oui, mais vous devez tooset qui les dans le modèle de hello de l’image avant de créer de collection de hello. Utilisez hello suivant le lecteur système toohello étapes tooblock accès :

1. Exécutez **gpedit.msc** sur l’image de modèle hello.
2. Accédez trop**Configuration utilisateur > modèles d’administration > composants Windows > Explorateur**.
3. Sélectionnez hello options suivantes :
   * **Dans Poste de travail, masquer ces lecteurs spécifiés**
   * **Empêcher toodrives d’accès à partir du poste de travail**

## <a name="can-i-seed-upds-i-want-tooput-some-data-in-hello-upd-thats-available-hello-first-time-hello-user-signs-in"></a>Puis-je amorcer des UPD ? Je veux tooput certaines données Bonjour UPD est disponible hello premier moment hello utilisateur se connecte.
Oui, lorsque vous créez des images de modèle hello, vous pouvez ajouter le profil par défaut de toohello plus d’informations. Cette information est ajoutée puis toohello UPD.

## <a name="can-i-change-hello-size-of-hello-upd-depending-on-how-much-data-i-want-toostore"></a>Puis-je modifier taille hello Hello UPD selon la quantité de données, je veux toostore ?
Non, tous les UPD ont une capacité de stockage de 50 Go. Si vous souhaitez toostore différentes quantités de données, essayez suivante de hello :

1. Désactiver pour collection de hello.
2. Configurer un partage de fichiers pour les utilisateurs tooaccess.
3. Charge le partage de fichiers hello à l’aide d’un script de démarrage. Voir ci-dessous pour plus d'informations sur les scripts de démarrage dans Azure RemoteApp.
4. Diriger les utilisateurs toosave partage de fichiers de toutes les données toohello.

## <a name="how-do-i-run-a-startup-script-in-azure-remoteapp"></a>Comment puis-je exécuter un script de démarrage dans Azure RemoteApp ?
Si vous voulez toorun un script de démarrage, démarrer en créant une tâche planifiée dans l’image de modèle hello vous allez toouse pour la collection de hello. (Procédez ainsi *avant* d’exécuter sysprep.) 

![Création d’une tâche système](./media/remoteapp-upd/upd1.png)

![Création d’une tâche système qui s'exécute lorsqu'un utilisateur ouvre une session](./media/remoteapp-upd/upd2.png)

Sur hello **général** être vraiment toochange hello, onglet **compte d’utilisateur** sous sécurité trop « BUILTIN\Users ».

![Modifier le groupe de tooa hello utilisateur compte](./media/remoteapp-upd/upd4.png)

tâche planifiée Hello lance votre script de démarrage, à l’aide des informations d’identification de l’utilisateur hello. Planifier hello tâche toorun toutes une fois qu’un utilisateur ouvre une session.

![Définir un déclencheur de tâche hello en tant que « Dans le journal sur » hello](./media/remoteapp-upd/upd3.png)

Vous pouvez également utiliser [des scripts de démarrage basés sur une stratégie de groupe](https://technet.microsoft.com/library/cc779329%28v=ws.10%29.aspx). 

## <a name="what-about-placing-a-startup-script-in-hello-start-menu-would-that-work"></a>Qu’en est-il en plaçant un script de démarrage dans hello du menu Démarrer ? Cette méthode fonctionne-t-elle ?
En d’autres termes, puis-je créer un fichier .bat qui exécute un script de fenêtre de configuration et enregistrez-le toohello c:\ProgramData\Microsoft\Windows\Start Démarrer\Programmes\Démarrage et puis demandez à ce script à exécuter lorsqu’un utilisateur démarre une session de RemoteApp ?

Non, qui n'est pas pris en charge avec Azure RemoteApp qui utilise des postes de travail, ce qui est également ne prend pas en charge les scripts de démarrage dans le menu Démarrer de hello.

## <a name="can-i-use-mstscexe-hello-remote-desktop-program-tooconfigure-logon-scripts"></a>Puis-je utiliser des scripts d’ouverture de session mstsc.exe (programme de bureau à distance hello) tooconfigure ?
Non, cette fonctionnalité n’est pas prise en charge dans Azure RemoteApp.

## <a name="can-i-store-data-on-hello-vm-locally"></a>Puis-je stocker des données sur la machine virtuelle hello localement ?
NON, les données stockées n’importe où sur hello VM autre que Bonjour UPD seront perdues. Il existe un risque élevé hello l’utilisateur n’obtient hello hello de machine virtuelle même prochaine fois qu’ils se connectent à Azure RemoteApp. Nous ne conservent pas de persistance de la machine virtuelle de l’utilisateur, afin de l’utilisateur de hello se connecteront pas aux hello même machine virtuelle, et les données de salutation seront perdues. En outre, lorsque nous mettre à jour la collection de hello, hello que des machines virtuelles existantes sont remplacées par un nouvel ensemble d’ordinateurs virtuels - ce qui signifie que toutes les données stockées sur la machine virtuelle proprement dite de hello est perdue. recommandation de Hello est données toostore Bonjour UPD, stockage partagé, comme les fichiers Azure, un serveur de fichiers à l’intérieur d’un réseau virtuel, ou sur le cloud hello à l’aide d’un système de stockage cloud comme DropBox.

## <a name="how-do-i-mount-an-azure-file-share-on-a-vm-using-powershell"></a>Comment monter un partage de fichiers Azure sur une machine virtuelle à l'aide de PowerShell ?
Vous pouvez utiliser hello lecteur de hello toomount Net-PSDrive applet de commande, comme suit :

    New-PSDrive -Name <drive-name> -PSProvider FileSystem -Root \\<storage-account-name>.file.core.windows.net\<share-name> -Credential :<storage-account-name>


Vous pouvez également enregistrer vos informations d’identification en exécutant hello suivante :

    cmdkey /add:<storage-account-name>.file.core.windows.net /user:<storage-account-name> /pass:<storage-account-key>


Qui vous permet d’ignorer hello - paramètre d’informations d’identification dans l’applet de commande New-PSDrive de hello.

