---
title: "Comment Azure RemoteApp enregistre-t-il les paramètres et les données utilisateur ? | Microsoft Docs"
description: "Découvrez comment Azure RemoteApp enregistre les données utilisateur à l'aide du disque de profil utilisateur."
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
ms.openlocfilehash: 4993bf507536659d7951e1552559cf0a6061d345
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-does-azure-remoteapp-save-user-data-and-settings"></a>Comment Azure RemoteApp enregistre-t-il les paramètres et les données utilisateur ?
> [!IMPORTANT]
> Azure RemoteApp ne sera plus disponible à partir du 31 août 2017. Pour plus d’informations, lisez [l’annonce](https://go.microsoft.com/fwlink/?linkid=821148) .
> 
> 

Azure RemoteApp enregistre l'identité de l'utilisateur et les personnalisations entre les périphériques et les sessions. Ces données utilisateur sont stockées dans un disque par utilisateur et par collection, appelé disque de profil utilisateur (UPD). Le disque suit l'utilisateur et s’assure que l'utilisateur bénéficie d’une expérience cohérente, quel que soit l’endroit où il se connecte.

Les disques de profil utilisateur sont totalement transparents pour l'utilisateur : les utilisateurs enregistrent des documents dans leur dossier Documents (sans doute sur un lecteur local) et modifient leurs paramètres d'application comme d'habitude. En même temps, tous les paramètres personnels sont conservés lors de la connexion à Azure RemoteApp à partir de n'importe quel périphérique. L'utilisateur voit seulement ses données dans un même endroit.

Chaque UPD offre 50 Go de stockage persistant et contient à la fois les paramètres d'application et les données utilisateur. 

Continuez votre lecture pour obtenir des détails spécifiques sur les données de profil utilisateur.

> [!NOTE]
> Vous avez besoin de désactiver le disque de profil utilisateur ? À présent, vous pouvez le faire. Consultez le billet de blog de Pavithra, [Désactiver les disques de profil utilisateur (UPD) dans Azure RemoteApp](https://blogs.technet.microsoft.com/enterprisemobility/2015/11/11/disable-user-profile-disks-upds-in-azure-remoteapp/), pour plus d’informations.
> 
> 

## <a name="how-can-an-admin-get-to-the-data"></a>Comment un administrateur peut-il accéder aux données ?
Si vous avez besoin d’accéder aux données pour l’un de vos utilisateurs (pour la récupération d’urgence ou si l’utilisateur quitte l’entreprise), contactez le support Azure et fournissez les informations d’abonnement de la collection et l’identité de l’utilisateur. L’équipe Azure RemoteApp vous fournira une URL pour accéder au disque dur virtuel. Téléchargez ce disque dur virtuel et récupérez les documents ou fichiers dont vous avez besoin. Notez que le disque dur virtuel est de 50 Go, il prendra donc un peu de temps à télécharger.

## <a name="is-the-data-backed-up"></a>Les données sont-elles sauvegardées ?
Oui, nous enregistrons une sauvegarde des données utilisateur par emplacement géographique. Les données sont en lecture seule et accessibles de la même façon que des données standard (contactez Azure RemoteApp si besoin), si le centre de données principal est arrêté. Les données sont copiées en temps réel vers l'emplacement de sauvegarde, et nous ne conservons aucune copies des différentes versions. Par conséquent, en cas de corruption des données, nous ne serons pas en mesure de les restaurer à une version correcte connue précédente, mais si le centre de données principal est en panne, vous ne pourrez pas obtenir de données utilisateur de l'autre emplacement.

## <a name="how-do-users-see-the-upd-on-the-server-side"></a>Comment les utilisateurs voient-ils l’UPD côté serveur ?
Chaque utilisateur disposera de son propre répertoire sur le serveur, pointant vers leur UPD : c:\Users\username.

## <a name="whats-the-best-way-to-use-outlook-and-upd"></a>Quelle est la meilleure façon d'utiliser Outlook et UPD ?
Azure RemoteApp enregistre l'état d'Outlook (boîtes aux lettres, PST) entre les sessions. Pour cela, le fichier PST doit être stocké dans les données du profil utilisateur (c:\users\<username>). Il s’agit de l'emplacement par défaut des données, par conséquent, tant que vous ne modifiez pas cet emplacement, les données seront conservées entre les sessions.

Nous vous recommandons également d'utiliser le mode « mise en cache » dans Outlook et d'utiliser le mode « serveur/en ligne » pour la recherche.

Consultez [cet article](remoteapp-outlook.md) pour plus d’informations sur l’utilisation d’Outlook et d’Azure RemoteApp.

## <a name="what-about-redirection"></a>Qu'en est-il de la redirection ?
Vous pouvez configurer Azure RemoteApp pour permettre aux utilisateurs d’accéder aux périphériques locaux en configurant une [redirection](remoteapp-redirection.md). Les périphériques locaux pourront ensuite accéder aux données sur l’UPD.

## <a name="can-i-use-my-upd-as-a-network-share"></a>Puis-je utiliser mon UPD comme partage réseau ?
Non. Les UPD ne peuvent pas être utilisés comme partage réseau. Un UPD est disponible pour l’utilisateur uniquement lorsque l'utilisateur est connecté activement à Azure RemoteApp.

## <a name="if-i-delete-a-user-from-a-collection-is-their-upd-deleted"></a>Si je supprime un utilisateur d'une collection, son UPD est-il supprimé ?
Non, lorsque vous supprimez un utilisateur, nous ne supprimons pas automatiquement l’UPD : nous stockons les données jusqu'à ce que vous supprimiez la collection. 90 jours après la suppression de la collection, nous supprimons tous les UPD. 

Si vous devez supprimer un UPD d'une collection, contactez Azure RemoteApp - nous pouvons supprimer l’UPD de notre côté.

## <a name="can-i-access-my-users-upds-either-current-or-deleted-users"></a>Puis-je accéder aux UPD de mes utilisateurs (utilisateurs actuels ou supprimés) ?
Oui, si vous contactez [Azure RemoteApp](mailto:remoteappforum@microsoft.com), nous pouvons vous fournir une URL pour accéder aux données. Vous disposez environ de 10 heures pour télécharger les données ou les fichiers de l’UPD avant expiration de l'accès.

## <a name="are-upds-available-offline"></a>Les UPD sont-ils disponibles hors connexion ?
Nous ne proposons actuellement pas d'accès hors connexion aux UPD au-delà de la fenêtre d'accès de 10 heures décrite ci-dessus. Cela signifie que nous ne sommes actuellement pas en mesure de vous fournir un accès suffisamment long pour effectuer des tâches plus complexes, par exemple l’exécution de logiciels antivirus sur les UPD ou l'accès aux données en vue d’un audit.

## <a name="do-registry-key-settings-persist"></a>Les paramètres de clé de registre sont-ils conservés ?
Oui, tout ce qui écrit dans la clé HKEY_Current_User fait partie de l’UPD.

## <a name="can-i-disable-upds-for-a-collection"></a>Puis-je désactiver les UPD d’une collection ?
Oui, vous pouvez demander à Azure RemoteApp de désactiver les UPD d’un abonnement, mais vous ne pouvez pas effectuer cette opération vous-même. Cela signifie que les UPD seront désactivés pour toutes les collections de l’abonnement.

Vous souhaiterez peut-être désactiver les UPD dans les situations suivantes : 

* Vous avez besoin d’un accès et d’un contrôle complet des données utilisateur (aux fins d’audit et de vérification ; p. ex., institutions financières).
* Vous possédez des solutions tierces de gestion des profils utilisateur en local, et souhaitez continuer à les utiliser dans votre déploiement Azure RemoteApp joint à un domaine. Cela nécessiterait le chargement de l’agent de profil dans l’image Gold. 
* Vous n’avez pas besoin de stockage de données local, toutes vos données sont dans le cloud ou dans un partage de fichiers, et vous aimeriez contrôler l’enregistrement des données en local à l’aide d’Azure RemoteApp.

Consultez [Désactiver les disques de profil utilisateur (UPD) dans Azure RemoteApp](https://blogs.technet.microsoft.com/enterprisemobility/2015/11/11/disable-user-profile-disks-upds-in-azure-remoteapp/) pour plus d’informations.

## <a name="can-i-restrict-users-from-saving-data-to-the-system-drive"></a>Puis-je empêcher les utilisateurs d’enregistrer des données sur le lecteur système ?
Oui, mais vous devrez configurer cette opération dans l'image du modèle avant de créer la collection. Utilisez les étapes suivantes pour bloquer l’accès au lecteur système :

1. Exécutez **gpedit.msc** sur l’image du modèle.
2. Accédez à **Configuration utilisateur > Modèles d’administration > Composants Windows > Explorateur**.
3. Sélectionnez les options suivantes :
   * **Dans Poste de travail, masquer ces lecteurs spécifiés**
   * **Empêcher l'accès aux lecteurs à partir du Poste de travail**

## <a name="can-i-seed-upds-i-want-to-put-some-data-in-the-upd-thats-available-the-first-time-the-user-signs-in"></a>Puis-je amorcer des UPD ? Je souhaite insérer des données UPD disponibles la première fois que l'utilisateur ouvre une session.
Oui, lorsque vous créez l'image de modèle, vous pouvez ajouter des informations au profil par défaut. Ces informations sont ensuite ajoutées à l’UPD.

## <a name="can-i-change-the-size-of-the-upd-depending-on-how-much-data-i-want-to-store"></a>Puis-je modifier la taille de l’UPD selon la quantité de données à stocker ?
Non, tous les UPD ont une capacité de stockage de 50 Go. Si vous souhaitez stocker d’autres quantités de données, essayez ce qui suit :

1. Désactivez les UPD de la collection.
2. Configurez un partage de fichiers accessible aux utilisateurs.
3. Chargez le partage de fichiers à l'aide d'un script de démarrage. Voir ci-dessous pour plus d'informations sur les scripts de démarrage dans Azure RemoteApp.
4. Demandez aux utilisateurs d'enregistrer toutes les données sur le partage de fichiers.

## <a name="how-do-i-run-a-startup-script-in-azure-remoteapp"></a>Comment puis-je exécuter un script de démarrage dans Azure RemoteApp ?
Si vous souhaitez exécuter un script de démarrage, commencez par créer une tâche planifiée dans l'image de modèle que vous souhaitez utiliser pour la collection. (Procédez ainsi *avant* d’exécuter sysprep.) 

![Création d’une tâche système](./media/remoteapp-upd/upd1.png)

![Création d’une tâche système qui s'exécute lorsqu'un utilisateur ouvre une session](./media/remoteapp-upd/upd2.png)

Dans l'onglet **Général**, veillez à choisir "BUILTIN\Users" comme **Compte utilisateur** sous Sécurité.

![Remplacement du compte d'utilisateur par un groupe](./media/remoteapp-upd/upd4.png)

La tâche planifiée lancera le script de démarrage à l'aide des informations d'identification de l'utilisateur. Planifiez l’exécution de la tâche chaque fois qu'un utilisateur ouvre une session.

![Définition du déclencheur pour la tâche sur « à l’ouverture de la session »](./media/remoteapp-upd/upd3.png)

Vous pouvez également utiliser [des scripts de démarrage basés sur une stratégie de groupe](https://technet.microsoft.com/library/cc779329%28v=ws.10%29.aspx). 

## <a name="what-about-placing-a-startup-script-in-the-start-menu-would-that-work"></a>Qu’en est-il du placement d’un script de démarrage dans le menu Démarrer ? Cette méthode fonctionne-t-elle ?
En d'autres termes, puis-je créer un fichier .bat qui exécute un script de fenêtre de configuration et l’enregistre dans le dossier c:\ProgramData\Microsoft\Windows\Start Menu\Programs\StartUp, puis exécuter ce script chaque fois qu'un utilisateur démarre une session RemoteApp ?

Non, cette opération n'est pas prise en charge dans Azure RemoteApp, qui utilise RDSH, qui ne prend pas en charge non plus les scripts de démarrage dans le menu Démarrer.

## <a name="can-i-use-mstscexe-the-remote-desktop-program-to-configure-logon-scripts"></a>Puis-je utiliser mstsc.exe (le programme Bureau à distance) pour configurer des scripts d'ouverture de session ?
Non, cette fonctionnalité n’est pas prise en charge dans Azure RemoteApp.

## <a name="can-i-store-data-on-the-vm-locally"></a>Est-il possible de stocker localement des données sur la machine virtuelle ?
NON, les données stockées sur la machine virtuelle ailleurs que dans l'UPD seront perdues. Il est fort probable que l'utilisateur ne recevra pas la même machine virtuelle la prochaine fois qu'il se connecte à Azure RemoteApp. Les machines virtuelles n'étant pas dédiées à un utilisateur spécifique, celui-ci ne se connecte donc pas à la même machine virtuelle, et les données seront perdues. En outre, lorsque nous mettre à jour la collection, les machines virtuelles existantes sont remplacées par un nouvel ensemble de machines virtuelles - ce qui signifie que toutes les données stockées sur la machine virtuelle elle-même sont perdues. Il est recommandé de stocker les données dans l’UPD, un stockage partagé comme des fichiers Azure, un serveur de fichiers à l’intérieur d’un réseau virtuel, ou sur le cloud à l’aide d’un système de stockage cloud pris en charge comme DropBox.

## <a name="how-do-i-mount-an-azure-file-share-on-a-vm-using-powershell"></a>Comment monter un partage de fichiers Azure sur une machine virtuelle à l'aide de PowerShell ?
Vous pouvez utiliser l'applet de commande Net-PSDrive pour monter le lecteur, comme suit :

    New-PSDrive -Name <drive-name> -PSProvider FileSystem -Root \\<storage-account-name>.file.core.windows.net\<share-name> -Credential :<storage-account-name>


Vous pouvez également enregistrer vos informations d'identification en exécutant la commande suivante :

    cmdkey /add:<storage-account-name>.file.core.windows.net /user:<storage-account-name> /pass:<storage-account-key>


Vous pouvez ainsi ignorer le paramètre -Credential dans l'applet de commande New-PSDrive.

