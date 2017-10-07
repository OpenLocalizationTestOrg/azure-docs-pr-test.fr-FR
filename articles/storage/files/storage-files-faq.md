---
title: aaaFrequently aux questions sur le stockage de fichiers Azure | Documents Microsoft
description: "Trouvez des réponses elles sonttrop aux questions sur le stockage de fichiers Azure."
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
ms.date: 07/19/2017
ms.author: renash
ms.openlocfilehash: d8a94fdc77e928dbc6996e1e635cd3527e0c67d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-about-azure-file-storage"></a>Questions fréquemment posées sur Stockage Fichier Azure

## <a name="general"></a>Généralités
* **Q. Qu’est-ce que Stockage Fichier Azure ?**  
   
    Stockage Fichier Azure est un système de fichiers distribué dans Azure. Il fournit une interface de protocole SMB qui permet de stockage de hello toomount les utilisateurs en tant que natif partage sur une Machine virtuelle Azure pris en charge ou l’ordinateur local.

* **Q. Pourquoi Stockage Fichier Azure est-il utile ?**  
   
    Stockage Fichier Azure fournit un accès aux données partagé entre plusieurs machines virtuelles et plateformes. Consultez trop[pourquoi les fichiers Azure stockage est utile](storage-files-introduction.md#why-azure-file-storage-is-useful).

* **Q. Quand utiliser Stockage Fichier Azure, Stockage Blob Azure ou un stockage sur disque Azure ?**  
   
    Microsoft Azure offre plusieurs moyens de toostore et accès aux données dans le cloud de hello.  
   
    Stockage de fichier Azure - fournit une interface SMB, les bibliothèques clientes et une interface REST qui permet un accès facile à partir de n’importe quel endroit toostored fichiers.  
   
    Azure BLOB - fournit des bibliothèques clientes et une interface REST qui permet de toobe des données non structurées stockées et accessibles à une grande échelle dans les objets BLOB de blocs.  
   
    Données Azure disques - fournit des bibliothèques clientes et une interface REST qui permet des données toobe persistante stockées et accessibles à partir d’un disque dur virtuel attaché.  
   
    En savoir plus sur [choix entre lorsque les objets BLOB de Azure toouse, des fichiers de Azure ou des disques de données Azure](../common/storage-decide-blobs-files-disks.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)

* **Q. Comment commencer à utiliser Stockage Fichier Azure ?**  
   
    Commencez par créer un partage de fichiers Azure. Vous pouvez créer des partages de fichiers Azure à l’aide du portail Azure, les applets de commande PowerShell de stockage Azure hello, les bibliothèques clientes de stockage Azure hello ou hello API REST de stockage Azure. Dans ce didacticiel, vous allez apprendre :

    * [Découvrez comment toocreate fichier Azure partager à l’aide de hello portail](storage-how-to-create-file-share.md#create-file-share-through-the-portal)
    * [Découvrez comment toocreate fichier Azure partager à l’aide de Powershell](storage-how-to-create-file-share.md#create-file-share-through-powershell)
    * [Découvrez comment toocreate fichier Azure partager à l’aide de CLI](storage-how-to-create-file-share.md#create-file-share-through-command-line-interface-cli)

* **Q. Quelles réplications Stockage Fichier Azure prend-il en charge ?**  
   
    Stockage Fichier Azure ne prend en charge actuellement que les stockages LRS ou GRS. Nous prévoyons de toosupport RA-GRS, mais il n’existe encore aucune tooshare de chronologie.

## <a name="security-authentication-and-access-control"></a>Sécurité, authentification et contrôle d'accès

* **Q. Quelles sont les fichiers de tooaccess de différentes façons dans le stockage de fichier Azure ?**
    
    Vous pouvez monter le partage de fichiers hello sur votre ordinateur local à l’aide du protocole SMB 3.0 ou utiliser les outils tels que [Explorateur de stockage](http://storageexplorer.com/) fichiers tooaccess dans votre partage de fichiers. À partir de votre application, vous pouvez utiliser les bibliothèques clientes de stockage, API REST ou tooaccess Powershell que partagent de vos fichiers dans le fichier Azure.

* **Q. Comment puis-je fournir les fichiers spécifiques tooa accès à l’aide d’un navigateur web ?**
    
    À l’aide des SAP, vous pouvez générer des jetons assortis d’autorisations spécifiques, qui restent valides pendant une période définie. Par exemple, vous pouvez générer un jeton avec le fichier tooa accès en lecture seule pour une période spécifique. Toute personne qui possède cette url peut accéder au fichier de hello directement à partir de n’importe quel navigateur web alors qu’il est valide. Les clés SAP peuvent être facilement générées à partir d’une interface utilisateur telle que Storage Explorer.

* **Q. Il est possible toospecify des autorisations en lecture seule ou en écriture seule sur les dossiers de partage de hello ?**
    
    Vous n’avez ce niveau de contrôle des autorisations si vous montez le partage de fichiers hello via SMB. Toutefois, vous pouvez y parvenir en créant une signature d’accès partagé (SAS) via l’API REST de hello ou des bibliothèques clientes.  

* **Q. Comment activer le chiffrement côté serveur pour Stockage Fichier Azure ?**

    Le [chiffrement côté serveur](../common/storage-service-encryption.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json) pour Stockage Fichier Azure est généralement disponible dans toutes les régions et tous les clouds publics et nationaux. Vous pouvez activer SSE pour Stockage Fichier Azure à l’aide du [portail Azure](https://portal.azure.com/), de [l’API du fournisseur de ressources de Stockage Microsoft Azure](/rest/api/storagerp/storageaccounts), d’[Azure PowerShell](https://msdn.microsoft.com/library/azure/mt607151.aspx) ou d’[Azure CLI](../common/storage-azure-cli.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).
    
    Après avoir activé SSE sur le stockage de fichiers Azure, toutes les nouvelles données écrites toohello le stockage de fichiers dans ce compte de stockage seront automatiquement chiffrées. Cette fonctionnalité est disponible pour toutes les nouvelles données écrites tooexisting ou nouveaux partages dans un compte de stockage existant ou nouveau. L’activation de cette fonction sera sans frais supplémentaires. En savoir plus sur [comment tooenable SSE sur le stockage de fichiers Azure](../common/storage-service-encryption.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).

* **Q. Stockage Fichier Azure prend-il en charge l’authentification Azure Active Directory ?**
   
    À l’heure actuelle, l’authentification ou les listes de contrôle d’accès basées sur Active Directory ne sont pas prises en charge, mais elles figurent dans notre liste de demandes de fonctionnalités. Pour l’instant, les clés de compte de stockage Azure hello sont partage de fichiers toohello tooprovide utilisé l’authentification. Nous offrent une solution de contournement à l’aide de signatures d’accès partagé (SAS) via les bibliothèques de client API REST ou hello hello. À l’aide des SAP, vous pouvez générer des jetons assortis d’autorisations spécifiques, qui restent valides pendant une période définie. Par exemple, vous pouvez générer un jeton avec accès en lecture seule les tooa fichier expiration de 10 minutes. Toute personne qui possède ce jeton, alors qu’il est valide a un fichier de toothat d’accès en lecture seule pendant les 10 minutes.
   
    SAP est uniquement pris en charge via les bibliothèques API REST ou de client hello. Lorsque vous montez le partage de fichiers hello via hello protocole SMB, vous ne pouvez pas utiliser un contenu de tooits SAS toodelegate accès. 
    
* **Q. Quelles sont les stratégies de conformité données hello pris en charge pour le stockage de fichiers Azure ?**

   Stockage de fichier Azure s’exécute sur hello même architecture de stockage comme autre support de stockage dans le stockage Azure des services et s’applique hello mêmes stratégies de conformité des données. Plus d’informations sur la conformité des données de stockage Azure, vous pouvez télécharger et faire référence trop[document de Microsoft Azure Data Protection](http://go.microsoft.com/fwlink/?LinkID=398382&clcid=0x409).

## <a name="on-premises-access"></a>Accès local

* **Q.Do je dispose de stockage de fichiers toouse Azure ExpressRoute tooconnect tooAzure à partir d’une machine virtuelle locale ?**
   
    Non. Si vous n’avez pas ExpressRoute, vous pouvez toujours accéder partage de fichiers hello sur site, que vous avez le port 445 (TCP sortant) ouvert pour l’accès à Internet. Vous pouvez toutefois utiliser ExpressRoute avec Stockage Fichier Azure si vous le souhaitez.

* **Q. Comment monter un partage de fichiers Azure sur mon ordinateur local ?** 
    
    Vous pouvez monter le partage de fichiers hello via le protocole SMB de hello tant que le port 445 (TCP sortant) est ouvert et que votre client prend en charge le protocole de hello SMB 3.0 (par exemple, vous utilisez Windows 10 ou Windows Server 2012). Collaborez avec votre fournisseur de services Internet fournisseur toounblock hello de voies. Bonjour intermédiaire, vous pouvez afficher vos fichiers à l’aide de [Explorateur de stockage](../../vs-azure-tools-storage-explorer-files.md#view-a-file-shares-contents).


## <a name="billing-and-pricing"></a>Facturation et la tarification
* **Q. De hello le trafic réseau entre une machine virtuelle Azure et un nombre de partage de fichiers que la bande passante externe qui est facturée toohello abonnement ?**
   
    Si le partage de fichiers hello et les ordinateurs virtuels se trouvent dans hello même région Azure, hello le trafic entre eux est gratuit. Si elles sont dans des régions différentes, vous serez facturé trafic hello entre eux en tant que la bande passante externe.

## <a name="backup"></a>Sauvegarde

* **Q. Comment sauvegarder les mon partage de fichiers Azure ?**
    
    Vous pouvez utiliser AzCopy, RoboCopy ou un outil de sauvegarde tiers capable de sauvegarder un partage de fichiers monté. Nous pensons que toohave hello capacité tootake des instantanés des partages de fichiers Bonjour proche avenir ; vous serez en mesure de toouse toobackup de cette fonctionnalité de partage de vos fichiers de Azure.

## <a name="performance"></a>Performances

* **Q. Quelles sont les limites d’échelle hello de stockage Azure ?**
    Pour plus d’informations sur les objectifs d’extensibilité et de performance de Stockage Fichier Azure, voir [Objectifs de performance et évolutivité d'Azure Storage](../common/storage-scalability-targets.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#scalability-targets-for-blobs-queues-tables-and-files).

* **Q. Mes performances était lente lors de la tentative de toounzip fichiers dans le stockage des fichiers Azure. Que dois-je faire ?**
    
    tootransfer un grand nombre de fichiers dans le stockage des fichiers Azure, nous vous recommandons d’utiliser AzCopy (Windows, version préliminaire pour Linux/Unix) ou Azure Powershell que ces outils ont été optimisées pour transfert réseau.

* **Q. Les correctifs qui a été publié le problème de performances lentes toofix avec le stockage de fichiers Azure ?**
    
    l’équipe Windows Hello a récemment publié un correctif logiciel de toofix un problème de ralentissement des performances lorsque les clients hello accède au stockage de fichiers Azure à partir de Windows 8.1 ou Windows Server 2012 R2. Pour plus d’informations, veuillez out hello associés à l’article, [ralentir les performances lorsque vous accédez à stockage Azure Files à partir de Windows 8.1 ou Server 2012 R2](https://support.microsoft.com/kb/3114025).

## <a name="features-and-interoperability-with-other-services"></a>Fonctionnalités et interopérabilité avec d’autres services
* **Q. Est un « témoin de partage de fichiers » pour un cluster de basculement, un des hello cas d’usage pour le stockage de fichiers Azure ?**
   
    Cela n’est actuellement pas pris en charge.

* **Q. Existe-t-il une opération de changement de nom dans l’API REST de hello ?**
   
    Pas pour l'instant.

* **Q. Est-il possible d’avoir des partages imbriqués, autrement dit, un partage sous un partage ?**
    
    Non. partage de fichiers Hello étant pilote hello virtuel que vous pouvez monter, partages imbriqués ne sont pas pris en charge.

* **Q. Utilisation de Stockage Fichier Azure avec Linux**
    
    IBM a publié aux clients de document tooguide IBM MQ lors de la configuration de stockage Azure files avec leur service. Pour plus d’informations, consultez [comment toosetup IBM MQ Multi instance Gestionnaire de file d’attente avec Microsoft Azure File Service](https://github.com/ibm-messaging/mq-azure/wiki/How-to-setup-IBM-MQ-Multi-instance-queue-manager-with-Microsoft-Azure-File-Service).


## <a name="troubleshooting"></a>Résolution des problèmes
* **Q. Comment résoudre les erreurs de Stockage Fichier Azure ?**
    
    Vous pouvez faire référence trop[le stockage de fichiers Azure Article de résolution des problèmes](storage-troubleshoot-windows-file-connection-problems.md) de bout en bout des conseils de dépannage. 


## <a name="see-also"></a>Voir aussi
Pour plus d’informations sur le stockage de fichiers Azure, consultez ces liens.

### <a name="conceptual-articles-and-videos"></a>Vidéos et articles conceptuels
* [Stockage Fichier Azure : un système de fichiers SMB dans le cloud sans friction pour Windows et Linux](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)
* [Comment toouse stockage Azure files avec Linux](storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-file-storage"></a>Outils pris en charge pour le stockage de fichiers
* [Comment toouse AzCopy avec Microsoft Azure Storage](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)
* [À l’aide de hello CLI d’Azure avec le stockage Azure](../common/storage-azure-cli.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)
* [Résolution des problèmes de stockage de fichiers Azure](storage-troubleshoot-linux-file-connection-problems.md)

### <a name="blog-posts"></a>Billets de blog :
* [Le stockage de fichiers Azure est désormais mis à la disposition générale](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [Dans le Stockage Fichier Azure](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [Présentation de Microsoft Azure File Service](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [Migration données tooAzure stockage de fichiers](https://azure.microsoft.com/blog/migrating-data-to-microsoft-azure-files/)

### <a name="reference"></a>Référence
* [Référence de la bibliothèque cliente de stockage pour .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [Référence de l’API REST du service de fichiers](http://msdn.microsoft.com/library/azure/dn167006.aspx)
