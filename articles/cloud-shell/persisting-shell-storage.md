---
title: "fichiers aaaPersist dans Azure Cloud Shell (version préliminaire) | Documents Microsoft"
description: "Procédure pas à pas de conservation des fichiers avec Azure Cloud Shell."
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: juluk
ms.openlocfilehash: b230453d5551c545553d63559741950206e4f1b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="persist-files-in-azure-cloud-shell"></a>Conserver des fichiers dans Azure Cloud Shell
Interpréteur de commandes de nuage tire parti Azure fichier toopersist des fichiers de stockage entre les sessions.

## <a name="set-up-a-clouddrive-file-share"></a>Créer un partage de fichiers `clouddrive`
Au démarrage initial, Cloud Shell vous invite tooassociate un fichier nouveau ou existant partager les fichiers toopersist sessions.

### <a name="create-new-storage"></a>Créer un stockage

Lorsque vous utilisez des paramètres de base et que vous sélectionnez qu’un abonnement, Shell de Cloud crée trois ressources de votre part dans la région de hello pris en charge est le plus proche tooyou :
* Groupe de ressources : `cloud-shell-storage-<region>`
* Compte de stockage : `cs<uniqueGuid>`
* Partage de fichiers : `cs-<user>-<domain>-com-<uniqueGuid>`

![paramètre d’abonnement Hello](media/basic-storage.png)

partage de fichiers Hello monte comme `clouddrive` dans votre `$Home` active. Bonjour partage de fichiers est également utilisé toostore une image de 5 Go est créée automatiquement pour vous et qui met à jour et persiste votre `$Home` active. Il s’agit d’une action unique, et partage de fichiers hello monte automatiquement dans les sessions ultérieures.

### <a name="use-existing-resources"></a>Utiliser les ressources existantes

À l’aide de hello option avancée, vous pouvez associer des ressources existantes. Invite de commandes d’installation de stockage hello, sélectionnez **afficher les paramètres avancés** tooview des options supplémentaires. Les partages de fichiers existant recevoir un toopersist d’image utilisateur de 5 Go votre `$Home` active. déroulants Hello sont filtrés pour votre région Cloud Shell et comptes de stockage redondant local & géo-redondant.

![paramètre de groupe de ressources Hello](media/advanced-storage.png)

### <a name="restrict-resource-creation-with-an-azure-resource-policy"></a>Restreindre la création de ressources avec une stratégie de ressource Azure
Les comptes de stockage que vous créez dans Cloud Shell sont identifiés à l’aide de la balise `ms-resource-usage:azure-cloud-shell`. Si vous souhaitez toodisallow les utilisateurs de créer des comptes de stockage dans un environnement de Cloud, créez un [stratégie de ressources Azure pour les balises](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-policy-tags) qui sont déclenchés par cette balise spécifique.

## <a name="how-cloud-shell-works"></a>Fonctionnement de Cloud Shell
Shell de cloud enregistre les fichiers à la fois de hello méthodes suivantes :
* Création d’une image de disque de votre `$Home` toopersist Active tous les contenus dans le répertoire de hello. image de disque Hello est enregistré dans votre partage de fichier spécifié en tant que `acc_<User>.img` à `fileshare.storage.windows.net/fileshare/.cloudconsole/acc_<User>.img`, et il synchronise automatiquement les modifications.

* Montage du partage de fichiers spécifié en tant que `clouddrive` dans votre répertoire `$Home` pour l’interaction directe avec le partage de fichiers. `/Home/<User>/clouddrive`est mappé trop`fileshare.storage.windows.net/fileshare`.
 
> [!NOTE]
> Tous les fichiers figurant dans votre répertoire `$Home`, tels que les clés SSH, sont conservés dans l’image disque utilisateur qui est stockée dans votre partage de fichiers monté. Appliquez les bonnes pratiques lors de la conservation d’informations dans votre répertoire `$Home` et votre partage de fichiers monté.

## <a name="use-hello-clouddrive-command"></a>Hello d’utilisation `clouddrive` commande
Avec Cloud, vous pouvez exécuter une commande appelée `clouddrive`, qui permet de vous toomanually mise à jour hello de partage de fichiers tooCloud monté de Shell.
![Exécution de la commande « clouddrive » hello](media/clouddrive-h.png)

## <a name="mount-a-new-clouddrive"></a>Monter un nouveau `clouddrive`

### <a name="prerequisites-for-manual-mounting"></a>Prérequis pour le montage manuel
Vous pouvez mettre à jour de partage de fichiers hello associé Cloud Shell à l’aide de hello `clouddrive mount` commande.

Si vous montez un partage de fichiers existant, les comptes de stockage hello doivent être :
* Stockage redondant en local ou partages de fichiers toosupport stockage géo-redondant.
* Situés dans votre région affectée. Lorsque vous êtes l’intégration, région de hello vous sont assignés toois répertoriées dans le nom de groupe de ressources hello `cloud-shell-storage-<region>`.

### <a name="supported-storage-regions"></a>Régions de stockage prises en charge
Bonjour Azure fichiers doivent résider dans hello même région que hello Cloud Shell ordinateur que vous êtes le montage de leur. Clusters de Shell cloud existent actuellement dans hello suivant régions :
|Domaine|Région|
|---|---|
|Amérique|Est des États-Unis, Sud du centre des États-Unis, Ouest des États-Unis|
|Europe|Europe du Nord, Europe de l’Ouest|
|Asie-Pacifique|Inde-Centre, Sud-Est asiatique|

### <a name="hello-clouddrive-mount-command"></a>Hello `clouddrive mount` commande

> [!NOTE]
> Si vous êtes le montage d’un partage de fichiers, une nouvelle image de l’utilisateur est créée pour votre `$Home` active, car votre précédente `$Home` image est conservée dans le partage de fichiers hello précédente.

Exécutez hello `clouddrive mount` avec hello paramètres suivants :

```
clouddrive mount -s mySubscription -g myRG -n storageAccountName -f fileShareName
```

l’exécution de plus de détails, tooview `clouddrive mount -h`, comme illustré ici :

![En cours d’exécution hello ' clouddrive mount'command](media/mount-h.png)

## <a name="unmount-clouddrive"></a>Démonter `clouddrive`
Vous pouvez démonter un partage de fichiers tooCloud monté de Shell à tout moment. Une fois que le partage de fichiers est démonté, vous serez invité à toomount un tooyour préalable du partage de fichier nouveau session suivante.

tooremove un fichier de partage à partir de l’interpréteur de commandes de Cloud :
1. Exécutez `clouddrive unmount`.
2. Accuser réception et confirmez les invites de hello.

Le partage de fichiers continue tooexist, sauf si vous la supprimiez manuellement. Cloud Shell ne fera plus de recherche pour ce partage de fichiers lors des sessions ultérieures.

l’exécution de plus de détails, tooview `clouddrive unmount -h`, comme illustré ici :

![En cours d’exécution hello ' clouddrive unmount'command](media/unmount-h.png)

> [!WARNING]
> L’exécution de cette commande ne supprime pas de ressources. Suppression manuelle d’un groupe de ressources, le compte de stockage ou le partage de fichiers qui est mappé à tooCloud Shell supprimera définitivement votre `$Home` image de répertoire et tous les autres fichiers dans le partage de fichiers. Il est impossible d’annuler cette opération.

## <a name="list-clouddrive-file-shares"></a>Répertorier les partages de fichiers `clouddrive`
toodiscover le partage de fichiers est monté en tant que `clouddrive`, exécutez hello `df` commande. 

tooclouddrive de chemin d’accès de fichier Hello affiche que votre nom de compte de stockage et partage de fichiers dans l’URL de hello. Par exemple, `//storageaccountname.file.core.windows.net/filesharename`

```
justin@Azure:~$ df
Filesystem                                               1K-blocks     Used Available Use% Mounted on
overlay                                                   30428648 15585636  14826628  52% /
tmpfs                                                       986704        0    986704   0% /dev
tmpfs                                                       986704        0    986704   0% /sys/fs/cgroup
/dev/sda1                                                 30428648 15585636  14826628  52% /etc/hosts
shm                                                          65536        0     65536   0% /dev/shm
//mystoragename.file.core.windows.net/fileshareName        6291456  5242944   1048512  84% /usr/justin/clouddrive
/dev/loop0                                                 5160576   601652   4296780  13% /home/justin
```

## <a name="transfer-local-files-toocloud-shell"></a>Transfert de fichiers locaux tooCloud Shell
Hello `clouddrive` se synchronise de répertoire avec le panneau de stockage portail Azure hello. Utilisez cette tooor de fichiers locaux tootransfer panneau à partir de votre partage de fichiers. Mise à jour des fichiers à partir d’un environnement de Cloud est répercutée dans le stockage de fichier hello GUI lors de l’actualisation du Panneau de hello.

### <a name="download-files"></a>Téléchargement de fichiers

![Liste de fichiers locaux](media/download.png)
1. Bonjour portail Azure, passez le partage de fichiers monté toohello.
2. Sélectionnez le fichier cible de hello.
3. Sélectionnez hello **télécharger** bouton.

### <a name="upload-files"></a>Charger des fichiers

![Toobe fichiers locaux téléchargé](media/upload.png)
1. Passez le partage de fichiers monté tooyour.
2. Sélectionnez hello **télécharger** bouton.
3. Sélectionnez hello ou les fichiers que vous souhaitez tooupload.
4. Confirmer le téléchargement de hello.

Vous devez maintenant voir les fichiers hello qui sont accessibles dans votre `clouddrive` répertoire dans un environnement de Cloud.

## <a name="next-steps"></a>Étapes suivantes
[Démarrage rapide de Cloud Shell](quickstart.md) <br>
[En savoir plus sur Azure Stockage Fichier](https://docs.microsoft.com/azure/storage/storage-introduction#file-storage) <br>
[En savoir plus sur les balises de stockage](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags) <br>
