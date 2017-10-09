---
title: aaaIntroduction tooAzure stockage de fichiers | Documents Microsoft
description: "Une vue d’ensemble de stockage Azure, un service qui permet de vous toocreate et l’utilisation réseau fichier partage Bonjour Cloud de Microsoft à l’aide de la norme industrielle de hello."
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
ms.openlocfilehash: a0a6a80a2ccd9742aa470bdd02ff375387a1629b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-file-storage"></a>Introduction tooAzure stockage de fichiers
Stockage de fichiers Azure offre les partages de fichiers du réseau dans le cloud hello à l’aide de la norme industrielle de hello [les protocole Server Message Block (SMB)](https://msdn.microsoft.com/library/windows/desktop/aa365233.aspx) et [commune CIFS Internet File System ()](https://technet.microsoft.com/library/cc939973.aspx). Les partages de fichiers Azure peuvent être montés simultanément par les clients, par exemple via les déploiements locaux de Windows, macOS et Linux ou via des machines virtuelles Azure. Un stockage à usage général compte vous donne accès tooAzure stockage de fichiers et autres services tels que les objets BLOB, les disques de machine virtuelle Azure, les files d’attente sous un compte unique.



## <a name="videos"></a>Vidéos
| Présentation du Stockage Fichier Azure (27 min) | Didacticiel sur le Stockage Fichier Azure (5 minutes)  |
|-|-|
| [![ScreenCap de vidéo de stockage de présentation des fichiers Azure hello - cliquez sur tooplay !](media/storage-file-storage/azure-files-introduction-video-snapshot1.png)](https://www.youtube.com/watch?v=zlrpomv5RLs) | [![ScreenCap hello Azure de stockage de fichiers didacticiel - cliquez sur tooplay !](media/storage-file-storage/azure-files-introduction-video-snapshot2.png)](https://channel9.msdn.com/Blogs/Azure/Azure-File-storage-with-Windows/) |

## <a name="why-azure-file-storage-is-useful"></a>Avantages du Stockage Fichier Azure
Stockage de fichier Azure vous permet de tooreplace Windows Server, Linux, ou les serveurs de fichiers NAS hébergé localement ou dans le cloud de hello avec un fichier de cloud du système d’exploitation sans partagent. Cela a hello avantages suivants :

* **Accès partagé :**. Les partages de fichiers Azure industrie hello de prise en charge de protocole SMB standard, ce qui signifie que vous pouvez remplacer en toute transparence vos partages de fichiers locaux avec les partages de fichiers Azure sans se préoccuper de la compatibilité des applications. Être en mesure de tooshare un système de fichiers sur plusieurs ordinateurs, applications/instances est un avantage significatif avec stockage de fichier Azure pour les applications qui doivent Partageabilité les. 
* **Gestion intégrale**. Les partages de fichiers Azure peuvent être créés sans matériel de toomanage besoin hello ou un système d’exploitation. Cela signifie que vous n’avez pas toodeal avec la mise à jour corrective de système d’exploitation de serveur hello avec les mises à jour de sécurité critiques ou de remplacer les disques durs défectueux.
* **Écriture de scripts et outils**. Applets de commande PowerShell et CLI d’Azure peuvent être utilisé toocreate, montez et gérer des partages de fichiers de stockage dans le cadre de l’administration hello des applications Azure. Vous pouvez créer et gérer les partages de fichiers Azure à l’aide du portail Azure et Explorer le stockage Azure. 
* **Résilience**. Stockage de fichier Azure a été construit à partir de hello toobe toujours disponible d’arrière-plan. En remplaçant les partages de fichiers locaux avec Azure fichier stockage signifie que vous n’avez plus toowake des toodeal avec les coupures de courant locales ou des problèmes réseau. 
* **Programmabilité familière**. Les applications s’exécutant dans Azure peuvent accéder à un partage hello via fichier [I/O APIs système](https://msdn.microsoft.com/library/system.io.file.aspx). Les développeurs peuvent ainsi exploiter leur code existant et les applications existantes de compétences toomigrate. En plus de l’API d’e/s de tooSystem, vous pouvez utiliser [bibliothèques clientes de stockage Azure](https://msdn.microsoft.com/library/azure/dn261237.aspx) ou hello [API REST de stockage Azure](/rest/api/storageservices/file-service-rest-api).

Les partages de fichiers Azure peuvent être utilisés pour :

* **Remplacer les serveurs de fichiers locaux** :  
    Stockage de fichier Azure peut être toocompletely utilisé remplacer les partages de fichiers sur les serveurs de fichiers traditionnel sur site ou les périphériques NAS. Les systèmes d’exploitation courants tels que Windows, Mac OS et Linux peuvent monter facilement un partage de fichiers Azure où qu’ils soient dans Bonjour.

* **Migration « lift-and-shift » des applications** :  
    Stockage de fichier Azure permet de facilement trop « de courbes d’élévation et MAJ » cloud toohello applications qui utilisent le fichier local partage tooshare des données entre les parties de l’application hello. toomake cela, chaque machine virtuelle connecte partage de fichiers toohello et puis peut lire et écrire des fichiers exactement comme elle serait par rapport à un fichier local partager.

* **Simplifier le développement cloud** :  
    Azure stockage de fichier peut être utilisé dans un nombre de différentes façons toosimplify nouveaux cloud projets de développement.
    * **Paramètres d’application partagés** :  
        Un modèle commun pour les applications distribuées est toohave les fichiers de configuration dans un emplacement centralisé où ils sont accessibles à partir de nombreux ordinateurs virtuels différents. Ces fichiers de configuration peuvent désormais être stockés dans un partage de fichiers Azure, puis lus par toutes les instances de l’application. Ces paramètres peuvent également être gérés via l’interface REST hello, qui autorise l’accès dans le monde toohello les fichiers de configuration.

    * **Partage de diagnostic** :  
        Un partage de fichiers Azure peut également être toosave utilisé diagnostic les fichiers journaux, les mesures et les vidages sur incident. Ils sont disponibles à travers l’interface REST et hello SMB autorise les applications toobuild ou tirer parti de divers outils d’analyse pour traiter et analyser des données de diagnostic hello.

    * **Développement / test / débogage** :  
        Lorsque vous travaillez sur des machines virtuelles dans le cloud de hello développeurs ou administrateurs, ils doivent souvent un ensemble d’outils ou utilitaires. Les procédures d’installation et de distribution de ces utilitaires sur chaque machine virtuelle, à l’endroit requis, peuvent prendre du temps. Avec le stockage de fichiers Azure, un développeur ou un administrateur peut stocker leurs outils favoris sur un partage de fichiers, ce qui peut être facilement connecté toofrom n’importe quel ordinateur virtuel.
        
## <a name="how-does-it-work"></a>Comment cela fonctionne-t-il ?
La gestion des partages de fichiers Azure est beaucoup plus simple que la gestion des partages de fichiers locaux. Hello suivant schéma illustre les constructions de gestion hello fichier Azure storage :

![Structure de fichiers](../../includes/media/storage-file-concepts-include/files-concepts.png)

* **Compte de stockage**: tous les accès tooAzure stockage s’effectue via un compte de stockage. Pour plus d’informations sur la capacité du compte de stockage, consultez la page Objectifs de performance et évolutivité du stockage Azure.
* **Partage** : un partage de stockage de fichiers est un partage de fichiers SMB dans Azure. Tous les répertoires et fichiers doivent être créés dans un partage parent. Un compte peut contenir un nombre illimité de partages, et un partage peut stocker un nombre illimité de fichiers, la capacité totale de 5 to toohello hello du partage de fichiers.
* **Répertoire** : hiérarchie facultative de répertoires.
* **Fichier**: un fichier dans le partage de hello. Un fichier peut être jusqu'à to too1 taille.
* **Format d’URL**: les fichiers sont adressables en utilisant hello suivant le format d’URL :  

    ```
    https://<storage account>.file.core.windows.net/<share>/<directory/directories>/<file>
    ```
## <a name="next-steps"></a>Étapes suivantes
* [Création d’un partage de fichiers Azure](storage-file-how-to-create-file-share.md)
* [Connexion et montage sous Windows](storage-file-how-to-use-files-windows.md)
* [Connexion et montage sous Linux](storage-how-to-use-files-linux.md)
* [Connexion et montage sous macOS](storage-file-how-to-use-files-mac.md)
* [FAQ](storage-files-faq.md)
* [Dépannage](storage-troubleshoot-file-connection-problems.md)

### <a name="conceptual-articles-and-videos"></a>Vidéos et articles conceptuels
* [Stockage Fichier Azure : un système de fichiers SMB dans le cloud sans friction pour Windows et Linux](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)

### <a name="tooling-support-for-azure-file-storage"></a>Outils pour le Stockage Fichier Azure
* [Utilisation d'Azure PowerShell avec Azure Storage](storage-powershell-guide-full.md)
* [Comment toouse AzCopy avec Microsoft Azure Storage](storage-use-azcopy.md)
* [À l’aide de hello CLI d’Azure avec le stockage Azure](storage-azure-cli.md#create-and-manage-file-shares)

### <a name="blog-posts"></a>Billets de blog :
* [Le stockage de fichiers Azure est désormais mis à la disposition générale](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [Dans le Stockage Fichier Azure](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [Présentation de Microsoft Azure File Service](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [Migration tooAzure de données fichier](https://azure.microsoft.com/blog/migrating-data-to-microsoft-azure-files/)

### <a name="reference"></a>Référence
* [Référence de la bibliothèque cliente de stockage pour .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [Référence de l’API REST du service de fichiers](http://msdn.microsoft.com/library/azure/dn167006.aspx)
