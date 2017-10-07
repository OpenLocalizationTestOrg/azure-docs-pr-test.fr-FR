---
title: aaaIntroduction tooAzure stockage de fichiers | Documents Microsoft
description: "Introduction tooAzure stockage de fichiers, qui fournit le fichier réseau partage Bonjour Microsoft Cloud"
services: storage
documentationcenter: 
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/27/2017
ms.author: renash
ms.openlocfilehash: fe6826e79c364a6956831d2e273c4342a5fd47f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-file-storage"></a>Introduction tooAzure stockage de fichiers

Stockage de fichiers Azure offre les partages de fichiers du réseau dans le cloud hello à l’aide de la norme industrielle de hello [les protocole Server Message Block (SMB)](https://msdn.microsoft.com/library/windows/desktop/aa365233.aspx) et [commune CIFS Internet File System ()](https://technet.microsoft.com/library/cc939973.aspx). Les partages de fichiers Azure peuvent être montés simultanément par les machines virtuelles Azure et les déploiements locaux sous Windows, macOS ou Linux. Un stockage à usage général compte vous donne accès tooAzure le stockage de fichiers, le stockage Blob Azure et de stockage de la file d’attente Azure.

## <a name="videos"></a>Vidéos
| Présentation du Stockage Fichier Azure (27 min) | Didacticiel sur le Stockage Fichier Azure (5 minutes)  |
|-|-|
| [![Capture de la vidéo de stockage de présentation des fichiers Azure hello - cliquez sur tooplay !](./media/storage-files-introduction/azure-files-introduction-video-snapshot1.png)](https://www.youtube.com/watch?v=zlrpomv5RLs) | [![Capture de stockage de fichier Azure hello didacticiel - cliquez sur tooplay !](./media/storage-files-introduction/azure-files-introduction-video-snapshot2.png)](https://channel9.msdn.com/Blogs/Azure/Azure-File-storage-with-Windows/) |

## <a name="why-azure-file-storage-is-useful"></a>Avantages du Stockage Fichier Azure

Stockage de fichier Azure vous permet de tooreplace Windows Server, Linux, ou les serveurs de fichiers NAS hébergé localement ou dans le cloud de hello avec un fichier de cloud du système d’exploitation sans partagent. Stockage de fichier Azure a hello avantages suivants :

* **Accès partagé** industrie hello de prise en charge de protocole SMB standard, ce qui signifie que vous pouvez remplacer en toute transparence vos partages de fichiers locaux avec les partages de fichiers Azure sans se préoccuper de la compatibilité des applications de partages de fichiers de Azure. En mesure de tooaccess un partage de fichiers à partir de plusieurs ordinateurs et applications/instances est un avantage significatif avec le stockage de fichiers Azure.

* **Entièrement gérés** partages de fichiers Azure peuvent être créés sans matériel de toomanage besoin hello ou un système d’exploitation, ce qui signifie que vous n’avez pas toodeal avec la mise à jour corrective de système d’exploitation de serveur hello avec les mises à jour de sécurité critiques ou de remplacer les disques durs défectueux.

* **Écriture de scripts et les outils** CLI d’Azure et les applets de commande PowerShell peuvent être utilisé toocreate, montez et gérer des partages de fichiers Azure dans le cadre de l’administration hello des applications Azure. Vous pouvez créer et gérer les partages de fichiers Azure à l’aide de hello [portail Azure](https://portal.azure.com) et hello [Azure Storage Explorer](https://storageexplorer.com). 

* **Résilience** stockage Azure files a été généré à partir de hello toobe toujours disponible d’arrière-plan. En remplaçant les partages de fichiers locaux avec Azure fichier stockage signifie que vous n’avez plus toowake des toodeal avec les coupures de courant locales ou des problèmes réseau. 

* **Programmabilité familier** Applications s’exécutant dans Azure peuvent accéder aux données partage hello via [I/O APIs du système de fichiers](https://msdn.microsoft.com/library/system.io.file.aspx). Les développeurs peuvent ainsi exploiter leur code existant et les applications existantes de compétences toomigrate. En outre tooSystem API d’e/s, vous pouvez utiliser une des client de stockage Azure hello bibliothèques, telles que hello une pour [.NET](/dotnet/api/overview/azure/storage?view=azure-dotnet), ou hello [API REST de stockage Azure](/rest/api/storageservices/file-service-rest-api).

Les partages de fichiers Azure peuvent être utilisés pour :

* **Remplacer local serveurs de fichiers** stockage Azure peut être toocompletely utilisé remplacer les partages de fichiers sur les serveurs de fichiers traditionnel sur site ou les périphériques NAS. Les systèmes d’exploitation courants tels que Windows, Mac OS et Linux peuvent monter facilement un partage de fichiers Azure où qu’ils soient dans Bonjour.

* **Migration « lift-and-shift » des applications**

    Stockage de fichier Azure permet de facilement trop « de courbes d’élévation et MAJ » cloud toohello applications qui utilisent le fichier local partage tooshare des données entre les parties de l’application hello. tooimplement, chaque machine virtuelle connecte partage de fichiers toohello et puis peut lire et écrire des fichiers exactement comme elle serait par rapport à un fichier local partager.

* **Simplifier le développement cloud**
    
    Azure stockage de fichier peut être utilisé dans un nombre de différentes façons toosimplify nouveaux cloud projets de développement.
    
    * **Paramètres d’application partagés**
    
        Un modèle commun pour les applications distribuées est toohave les fichiers de configuration dans un emplacement centralisé où ils sont accessibles à partir de nombreux ordinateurs virtuels différents. Ces fichiers de configuration peuvent désormais être stockés dans un partage de fichiers Azure, puis lus par toutes les instances de l’application. Ces paramètres peuvent également être gérés via l’interface REST hello, qui autorise l’accès dans le monde toohello les fichiers de configuration.

    * **Partage de diagnostic**
    
        Un partage de fichiers Azure peut également être toosave utilisé diagnostic les fichiers journaux, les mesures et les vidages sur incident. Partages de fichiers disponibles à travers l’interface REST et hello SMB autorise les applications toobuild ou tirer parti de divers outils d’analyse pour traiter et analyser des données de diagnostic hello.

    * **Développement / test / débogage**

        Lorsque vous travaillez sur des machines virtuelles dans le cloud de hello développeurs ou administrateurs, ils doivent souvent un ensemble d’outils ou utilitaires. Les procédures d’installation et de distribution de ces utilitaires sur chaque machine virtuelle, à l’endroit requis, peuvent prendre du temps. Avec le stockage de fichiers Azure, un développeur ou un administrateur peut stocker leurs outils favoris sur un partage de fichiers, ce qui peut être facilement connecté toofrom n’importe quel ordinateur virtuel.
        
## <a name="how-does-it-work"></a>Comment cela fonctionne-t-il ?

La gestion des partages de fichiers Azure est beaucoup plus simple que la gestion des partages de fichiers locaux. Hello suivant schéma illustre les constructions de gestion hello fichier Azure storage :

![Structure de fichiers](./media/storage-files-introduction/files-concepts.png)

* **Compte de stockage** tous accéder tooAzure stockage s’effectue via un compte de stockage. Pour plus d’informations sur la capacité du compte de stockage, consultez la page [Objectifs de performance et évolutivité](../common/storage-scalability-targets.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).

* **Partage** : un partage de stockage de fichiers est un partage de fichiers SMB dans Azure. Tous les répertoires et fichiers doivent être créés dans un partage parent. Un compte peut contenir un nombre illimité de partages, et un partage peut stocker un nombre illimité de fichiers, la capacité totale de 5 to toohello hello du partage de fichiers.

* **Répertoire** : hiérarchie facultative de répertoires.

* **Fichier** un fichier dans le partage de hello. Un fichier peut être jusqu'à to too1 taille.

* **Format d’URL** fichiers sont adressables hello suivant le format d’URL :  

    ```
    https://<storage account>.file.core.windows.net/<share>/<directory/directories>/<file>
    ```

## <a name="next-steps"></a>Étapes suivantes

* [Création d’un partage de fichiers Azure](storage-how-to-create-file-share.md)
* [Connexion et montage sous Windows](storage-how-to-use-files-windows.md)
* [Connexion et montage sous Linux](storage-how-to-use-files-linux.md)
* [Connexion et montage sous macOS](storage-how-to-use-files-mac.md)
* [FAQ](../storage-files-faq.md)
* [Résolution des problèmes sur Windows](storage-troubleshoot-windows-file-connection-problems.md)   
* [Résolution des problèmes sur Linux](storage-troubleshoot-linux-file-connection-problems.md)   

<!-- Rena I would remove any articles from here that are more than a year old. - Robin-->
### <a name="conceptual-articles-and-videos"></a>Vidéos et articles conceptuels
* [Stockage Fichier Azure : un système de fichiers SMB dans le cloud sans friction pour Windows et Linux](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)

### <a name="tooling-support-for-azure-file-storage"></a>Outils pour le Stockage Fichier Azure
* [Comment toouse AzCopy avec Microsoft Azure Storage](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)
* [À l’aide de hello CLI d’Azure avec le stockage Azure](../common/storage-azure-cli.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#create-and-manage-file-shares)

### <a name="blog-posts"></a>Billets de blog :
* [Le stockage de fichiers Azure est désormais mis à la disposition générale](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [Dans le Stockage Fichier Azure](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [Présentation de Microsoft Azure File Service](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [Migration tooAzure de données fichier](https://azure.microsoft.com/blog/migrating-data-to-microsoft-azure-files/)

### <a name="reference"></a>Référence
* [Référence de la bibliothèque cliente de stockage pour .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [Référence de l’API REST du service de fichiers](http://msdn.microsoft.com/library/azure/dn167006.aspx)
