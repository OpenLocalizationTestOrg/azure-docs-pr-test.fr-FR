---
title: "données d’utilisateur aaaMigrate à partir d’Azure RemoteApp | Documents Microsoft"
description: "Découvrez comment toomigrate vos données utilisateur vers et depuis Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: d7e4fbf1-cb42-4430-94a0-ed6d4676fc86
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: aefc6ccc2c6173754acf6cad06102f27c8cb1d26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomigrate-data-into-and-out-of-azure-remoteapp"></a>Comment toomigrate des données dans et hors d’Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp ne sera plus disponible à partir du 31 août 2017. Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.
> 
> 

Vous pouvez utiliser de nombreux différents outils et méthodes tootransfer [données utilisateur](remoteapp-upd.md) dans et hors d’Azure RemoteApp. Voici quelques méthodes :

* Copier et coller en utilisant le partage du Presse-papiers
* Copiez les fichiers et les données de serveur de fichiers tooa
* Copiez les fichiers tooOneDrive for Business via un navigateur
* Copier des fichiers à l’aide de la redirection

> [!NOTE]
> Vous ne pouvez pas activer hello OneDrive pour les agents de synchronisation professionnels et particuliers - ils [ne sont pas pris en charge](remoteapp-onedrive.md) dans Azure RemoteApp.
> 
> 

## <a name="use-copy-and-paste-in-file-explorer"></a>Utiliser le copier-coller dans l’Explorateur de fichiers
Copier et coller à l’aide de Presse-papiers de hello est activé dans les déploiements de RemoteApp [par défaut](remoteapp-redirection.md). Cela permet aux utilisateurs de copier des fichiers entre leur ordinateur local et les applications RemoteApp. Souvent, via hello normales à l’aide d’applications dans RemoteApp, les utilisateurs ont enregistré les fichiers des tootheir - déplacement que les données de RemoteApp sont faciles :

1. [Publiez l’Explorateur de fichiers en tant qu’application](remoteapp-publish.md) dans une collection RemoteApp. (Notez qu’il s’agit d’une tâche administrative.)
2. Directement votre application de l’Explorateur de fichiers utilisateurs toolaunch hello que vous avez publié et toouse qui toocopy et coller les fichiers dans leur UPD et de sortie.

## <a name="upload-files-and-data-tooa-file-server-by-using-standard-network-file-copy"></a>Télécharger les fichiers et serveur de fichiers de données tooa à l’aide de la copie de fichiers réseau standard
Souvent, les organisations utilisent le fichier serveurs toostore général des données. Si vous connaissez le nom du serveur hello ou un emplacement, vos utilisateurs peuvent parcourir hello de réseau local pour le serveur de hello et copier puis leurs fichiers, comme c’était le cas ci-dessus. Nouveau vous souhaitez tooRemoteApp de l’Explorateur de fichiers toopublish et puis de le partager avec vos utilisateurs.

> [!NOTE]
> serveur de fichiers Hello doit être sur un réseau routable hello RemoteApp a été déployé dans.
> 
> 

## <a name="copy-files-tooonedrive-for-business"></a>Copier les fichiers tooOneDrive for Business
Bien que vous ne pouvez pas activer hello OneDrive pour l’agent de synchronisation d’entreprise dans RemoteApp, vous pouvez toujours copier les fichiers à partir de votre tooOneDrive UPD for Business via un navigateur. 

1. Publication tooRemoteApp de l’Explorateur de fichiers et ensuite d’indiquer aux utilisateurs tooaccess hello fichiers grâce à cette application. 
2. Il est plus simple tootransfer fichiers si elles sont compressées, donc les utilisateurs doivent créer un fichier .zip qui contienne tous les hello fichiers toomove tooOneDrive de l’entreprise.
3. Demander le portail d’utilisateurs toogo toohello Office 365, puis passez tooOneDrive et téléchargez le fichier .zip de hello.

## <a name="copy-files-by-using-drive-redirection"></a>Copier des fichiers à l’aide de la redirection de lecteur
Si vous avez activé [la redirection de lecteur](remoteapp-redirection.md), vous avez déjà créé un lecteur mappé pour vos utilisateurs. Dans ce cas, ils peuvent leurs fichiers sur le lecteur de hello redirigé zip et enregistrez-les tootheir PC local.

## <a name="how-administrators-can-export-data"></a>Comment les administrateurs peuvent exporter des données

Administre pour Azure RemoteApp peut exporter tous les disques de profil utilisateur (UPD) pour toutes les collections dans un stockage à l’aide d’Azure PowerShell de tooAzure abonnement applet de commande Export-AzureRemoteAppUserDisk.  Il n’existe aucune possibilité tooselect individuels UPD.  Lors de l’exécution de commande PowerShell de hello, chaque disque de l’utilisateur sera un 50 Go de taille de disque fixe et être exporté tooAzure stockage.  Les coûts de stockage Azure sont immédiatement exposés pour ce stockage.  Lors de l’exécution de cette commande garantit il n’y a aucune session sinon hello exportation échoue.

Les disques de profil utilisateur pour les déploiements Azure RemoteApp joints à un domaine peuvent être réutilisés uniquement dans un déploiement de services Bureau à distance, et les déploiements non-joints à un domaine ne peuvent pas être utilisés.  Si ces disques seront utilisés dans un déploiement services Bureau à distance nous vous recommandons de toouse notre [scripts automatisés](https://github.com/arcadiahlyy/aramigration) qui sera exporter, de convertir et importer hello d’UPD un déploiement services Bureau à distance.

