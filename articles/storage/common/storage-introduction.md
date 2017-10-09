---
title: aaaIntroduction tooAzure stockage | Documents Microsoft
description: "Introduction tooAzure Storage, stockage des données de Microsoft dans le cloud de hello."
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: a4a1bc58-ea14-4bf5-b040-f85114edc1f1
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/09/2017
ms.author: robinsh
ms.openlocfilehash: f61324f98d0a8eb24023e4344acdb4ca58bb27f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
<!-- this is hello same version that is in hello MVC branch -->
# <a name="introduction-toomicrosoft-azure-storage"></a>Introduction tooMicrosoft stockage Azure

Le stockage Microsoft Azure est un service cloud géré par Microsoft qui fournit un stockage hautement disponible, sécurisé, durable, évolutif et redondant. Microsoft prend en charge la maintenance et gère les problèmes critiques pour vous. 

Le stockage Azure se compose de trois services de données : le stockage d’objets blob, le stockage de fichiers et le stockage de files d’attente. Stockage d’objets BLOB prend en charge le stockage standard et premium, avec un stockage premium à l’aide uniquement les disques SSD pour accélérer au maximum performance hello. Une autre fonctionnalité est utile stockage, ce qui vous toostorage de grandes quantités de données rarement utilisées pour un coût inférieur.

Dans cet article, vous en savoir plus sur les éléments suivants de hello :
* services de stockage Azure Hello
* types de comptes de stockage Hello
* comment accéder aux objets blob, aux files d’attente et aux fichiers
* le chiffrement
* la réplication 
* comment transférer des données vers le stockage ou hors du stockage
* Bonjour nombreuses bibliothèques clientes de stockage disponibles. 


<!-- RE-ENABLE THESE AFTER MVC GOES LIVE 
tooget up and running with Azure Storage quickly, check out one of hello following Quickstarts:
* [Create a storage account using PowerShell](storage-quick-create-storage-account-powershell.md)
* [Create a storage account using CLI](storage-quick-create-storage-account-cli.md)
-->


## <a name="introducing-hello-azure-storage-services"></a>Présentation des services de stockage Azure hello

toouse hello services fournis par le stockage Azure : stockage d’objets Blob, le stockage de fichiers et le stockage de file d’attente--d’abord créer un compte de stockage, puis vous pouvez transférer des données vers/à partir d’un service spécifique dans ce compte de stockage. 

## <a name="blob-storage"></a>Stockage d'objets blob

Les objets blob sont essentiellement des fichiers semblables à ceux que vous stockez sur votre ordinateur (ou tablette, appareil mobile, etc). Il peut s’agir d’images, de fichiers Microsoft Excel, de fichiers HTML, de disques durs virtuels (VHD), de Big Data telle que des journaux ou des sauvegardes de base de données. Objets BLOB sont stockés dans des conteneurs, qui sont toofolders similaire. 

Après le stockage des fichiers dans le stockage Blob, vous pouvez y accéder depuis n’importe où dans Bonjour à l’aide d’URL, hello interface REST ou l’une des bibliothèques clientes de stockage de Windows Azure SDK hello. Les bibliothèques clientes de stockage sont disponibles dans plusieurs langages, tels que Node.js, Java, PHP, Ruby, Python et .NET. 

Il existe trois types d’objets blob : les objets blob de blocs, les objets blob d’ajouts et les objets blob de pages (utilisés avec les fichiers VHD).

* Objets BLOB de blocs est utilisés toohold de fichiers ordinaires des tooabout 4,7 To. 
* Objets BLOB de pages est des fichiers d’accès aléatoire de toohold utilisé jusqu'à to too8 taille. Ils sont utilisés pour les fichiers de disque dur virtuel hello sauvegarder des machines virtuelles.
* Ajouter des objets BLOB sont composés de blocs comme objets BLOB de blocs hello, mais sont optimisés pour les opérations d’ajout. Elles sont utilisées pour des éléments tels que la journalisation toohello informations même d’objets blob à partir de plusieurs machines virtuelles.

Pour les jeux de données où les contraintes de réseau effectuer le chargement ou téléchargement de stockage des données tooBlob acheminement hello irréaliste très volumineux, vous pouvez expédier un ensemble de disques durs tooMicrosoft tooimport ou exporter des données directement à partir de centre de données hello. Consultez [utiliser hello Service Microsoft Azure Import/Export tooTransfer données tooBlob stockage](../storage-import-export-service.md).

## <a name="file-storage"></a>Stockage Fichier

Hello service de fichiers Azure vous permet de tooset des partages de fichiers réseau hautement disponible qui sont accessibles à l’aide du protocole Server Message Block (SMB) standard de hello. Que signifie que plusieurs machines virtuelles peuvent partager hello même les fichiers en lecture et accès en écriture. Vous pouvez également lire les fichiers de hello via l’interface REST de hello ou des bibliothèques clientes de stockage hello. 

Une chose qui le distingue du stockage Azure Files à partir de fichiers sur un partage de fichiers d’entreprise est que vous pouvez accéder à des fichiers de hello depuis n’importe où dans Bonjour à l’aide d’une URL qui pointe le fichier de toohello et inclut un jeton de signature (SAP) d’accès partagé. Vous pouvez générer des jetons SAS ; ils autoriser accès spécifique tooa privé pour une durée spécifique. 

Les partages de fichiers peuvent être utilisés dans de nombreux scénarios courants : 

* Par exemple, de nombreuses applications locales utilisent les partages de fichiers. Cette fonctionnalité permet de toomigrate plus facilement les applications qui partagent des données tooAzure. Si vous montez hello toohello de partage de fichier même lettre hello de lecteur local application utilise, partie hello de votre application qui accède au partage de fichiers hello doit fonctionner avec des modifications minimales, le cas échéant.

* Les fichiers de configuration peuvent être stockés sur un partage de fichiers et sont accessibles à partir de plusieurs machines virtuelles. Outils et utilitaires utilisées par plusieurs développeurs dans un groupe peuvent être stockées sur un partage de fichiers, s’assurer que tout le monde peut trouver, et qu’elles utilisent hello même version.

* Journaux de diagnostic, les mesures et les vidages sur incident sont trois exemples de données qui peuvent être écrites de partage de fichiers tooa et traitées ou analyser ultérieurement.

Listes de contrôle (ACL) à ce temps, l’authentification basée sur Active Directory et l’accès ne sont pas pris en charge, mais elles seront à un moment donné dans hello futures. informations d’identification de compte de stockage Hello sont utilisées tooprovide l’authentification pour le partage de fichiers toohello accès. Cela signifie que toute personne avec partage hello monté aura le partage de toohello d’accès complet en lecture/écriture.

## <a name="queue-storage"></a>Stockage de files d'attente

Hello service de file d’attente Azure est toostore et récupérer les messages utilisés. Messages de file d’attente peuvent être des too64 Ko et une file d’attente peut contenir des millions de messages. Les files d’attente sont des listes de toostore généralement utilisée de toobe de messages traités de manière asynchrone. 

Par exemple, vous souhaitez que vos images tooupload en mesure de toobe clients, et que vous souhaitez toocreate miniatures de chaque image. Vous pourriez avoir à votre client d’attendre que vous toocreate des miniatures hello lors du téléchargement d’images de hello. Une alternative serait toouse une file d’attente. Client de hello après son téléchargement, écrivez une file d’attente de message toohello. Récupérer le message de type hello à partir de la file d’attente hello et créer des miniatures de hello puis demandez à une fonction d’Azure. Chacune des parties hello de ce traitement peut être monté en séparément, ce qui vous donne davantage de contrôle lors de son paramétrage pour votre utilisation.

<!-- this bookmark is used by other articles; you'll need tooupdate them before this goes into production ROBIN-->
## <a name="table-storage"></a>Stockage de tables
<!-- add a link toohello old table storage toothis paragraph once it's moved -->
Le stockage de tables Azure Standard fait désormais partie de Cosmos DB. Le service de tables Premium pour le stockage de tables Azure est également disponible et propose des tables optimisées pour le débit, la distribution globale et les index secondaires automatiques. toolearn plus et essayer hello nouvelle expérience, consultez [base de données Azure Cosmos : API de Table](https://aka.ms/premiumtables).

## <a name="disk-storage"></a>Stockage sur disque

équipe du stockage Azure Hello possède également des disques, qui inclut toutes les hello géré et les capacités de disque non managées utilisées par les ordinateurs virtuels. Pour plus d’informations sur ces fonctionnalités, consultez hello [documentation sur le Service de calcul](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).

## <a name="types-of-storage-accounts"></a>Types de compte de stockage 

Ce tableau montre des différents types de comptes de stockage et les objets peuvent être utilisés avec chaque hello.

|**Type de compte de stockage**|**Édition Standard à usage général**|**Édition Premium à usage général**|**Stockage d’objets blob, niveaux d’accès froid et chaud**|
|-----|-----|-----|-----|
|**Services pris en charge**| Services d’objet blob, de fichier et de file d’attente | Service blob | Service blob|
|**Types d’objets blob pris en charge**|Objets blob de blocs, objets blob de pages et objets blob d’ajout | Objets blob de pages | Objets blob de blocs et objets blob d’ajout|

### <a name="general-purpose-storage-accounts"></a>Comptes de stockage à usage général

Il existe deux types de comptes de stockage à usage général. 

#### <a name="standard-storage"></a>Stockage Standard 

comptes de stockage Hello plus largement utilisé sont les comptes de stockage standard, qui peuvent être utilisés pour tous les types de données. Comptes de stockage standard utilisent des données toostore de bande magnétique.

#### <a name="premium-storage"></a>Stockage Premium

Le service de stockage Premium offre un stockage hautes performances pour les objets blob de pages, principalement utilisés avec les fichiers VHD. Comptes de stockage Premium utilisent des données de toostore SSD. Microsoft recommande l’utilisation du service de stockage Premium pour toutes vos machines virtuelles.

### <a name="blob-storage-accounts"></a>Comptes de stockage d’objets blob

compte de stockage d’objets Blob Hello est un compte de stockage spécialisé utilisé toostore objets BLOB de blocs et objets BLOB d’ajout. Il est impossible d’y stocker des objets blob de pages et donc d’y stocker des fichiers VHD. Ces comptes vous permettent de tooset un tooHot de niveau d’accès ou utile ; niveau de Hello peut être modifié à tout moment. 

niveau d’accès à chaud Hello est utilisé pour les fichiers qui sont fréquemment accédées--vous payez un coût plus élevé pour le stockage, mais coût hello d’accéder aux objets BLOB de hello est beaucoup plus faible. Pour les objets BLOB stockés dans la couche d’accès froid hello, vous payez un coût plus élevé pour l’accès aux objets BLOB de hello, mais le coût du stockage hello est beaucoup plus faible.

## <a name="accessing-your-blobs-files-and-queues"></a>Accéder aux objets blob, aux fichiers et aux files d’attente

Chaque compte de stockage dispose deux clés d’authentification, qu’il est possible d’utiliser pour n’importe quelle opération. Il existe deux clés, donc vous pouvez substituer hello clés occasionnellement tooenhance sécurité. Il est essentiel que ces clés être conservé en lieu sûr, car leur possession, avec le nom de compte hello, permet des données de tooall un accès illimité hello compte de stockage. 

Cette section présente deux façons toosecure hello de stockage Azure et ses données. Pour plus d’informations sur la sécurisation de votre compte de stockage et de vos données, consultez hello [guide de sécurité de stockage Azure](storage-security-guide.md).

### <a name="securing-access-toostorage-accounts-using-azure-ad"></a>Sécurisation de l’accès à l’aide d’Azure AD des comptes toostorage

Données de stockage tooyour toosecure monodirectionnelle accès consiste à contrôler les clés de compte de stockage toohello accès. Avec le Gestionnaire de ressources du contrôle d’accès en fonction du rôle (RBAC), vous pouvez affecter des rôles toousers, des groupes ou des applications. Ces rôles sont liés ensemble spécifique de tooa d’actions qui sont autorisées ou non. Compte de stockage tooa toogrant accès à l’aide de RBAC gère uniquement les opérations de gestion de hello pour ce compte de stockage, telles que la modification du niveau d’accès hello. Impossible d’utiliser des objets de toodata RBAC toogrant accès à un partage de fichier ou le conteneur spécifique. Vous pouvez, toutefois, utiliser des RBAC toogrant accès toohello clés compte de stockage, qui peuvent ensuite être utilisé tooread hello des objets. 

### <a name="securing-access-using-shared-access-signatures"></a>Sécuriser l’accès à l’aide des signatures d’accès partagé 

Vous pouvez utiliser des signatures d’accès partagé et stockées toosecure de stratégies d’accès à vos objets de données. Une signature d’accès partagé (SAP) est une chaîne qui contient un jeton de sécurité qui peut être attachés toohello URI d’un composant qui vous permet des objets de stockage toodelegate access toospecific et contraintes toospecify tels que les autorisations et la plage de date/heure hello d’accès. Cette fonctionnalité dispose de fonctionnalités étendues. Pour plus d’informations, consultez trop[à l’aide de Signatures SAP (accès partagé)](storage-dotnet-shared-access-signature-part-1.md).

### <a name="public-access-tooblobs"></a>Accès public tooblobs

Hello Blob Service vous permet de tooprovide accès public tooa conteneur et ses objets BLOB ou un objet blob spécifique. Lorsque vous indiquez qu'un conteneur ou un objet blob est public, n'importe qui peut le lire de manière anonyme ; aucune authentification n'est requise. Par exemple, lorsque vous serez toodo est lorsque vous avez un site Web qui utilise des images, des vidéos ou des documents à partir du stockage d’objets Blob. Pour plus d’informations, consultez [gérer l’accès en lecture anonyme toocontainers et les objets BLOB](../blobs/storage-manage-access-to-resources.md) 

## <a name="encryption"></a>Chiffrement

Il existe deux types de chiffrement de base pour les services de stockage hello. 

### <a name="encryption-at-rest"></a>Chiffrement au repos 

Vous pouvez activer le chiffrement de Service de stockage (SSE) sur aucun de ces services de fichiers hello (version préliminaire) ou hello service Blob pour un compte de stockage Azure. S’il est activé, toutes les données écrites service spécifique de toohello est chiffré avant l’écriture. Lorsque vous lisez des données de salutation, il est déchiffré avant retourné. 

### <a name="client-side-encryption"></a>chiffrement côté client

Hello bibliothèques clientes de stockage ont des méthodes que vous pouvez appeler tooprogrammatically chiffrer les données avant de l’envoyer sur le câble de hello de hello client tooAzure. Les données sont chiffrées et stockées, ce qui signifie qu’elles sont également chiffrées au repos. Lors de la lecture des données hello, déchiffrer les informations hello après sa réception. 

### <a name="encryption-in-transit-with-azure-file-shares"></a>Chiffrement en transit avec des partages de fichiers Azure

Pour plus d’informations sur les signatures d’accès partagé, consultez [Utilisation des signatures d’accès partagé (SAP)](../storage-dotnet-shared-access-signature-part-1.md) . Consultez [gérer l’accès en lecture anonyme toocontainers et les objets BLOB](../blobs/storage-manage-access-to-resources.md) et [l’authentification pour hello Services de stockage Azure](https://msdn.microsoft.com/library/azure/dd179428.aspx) pour plus d’informations sur le compte de stockage tooyour un accès sécurisé.

Pour plus d’informations sur la sécurisation de votre compte de stockage et le chiffrement, consultez hello [guide de sécurité de stockage Azure](storage-security-guide.md).

## <a name="replication"></a>Réplication

Dans tooensure ordre que vos données sont durables, le stockage Azure a hello capacité tookeep (et gérer) plusieurs copies de vos données. On parle alors de réplication, ou parfois de redondance. Lorsque vous configurez votre compte de stockage, vous choisissez le type de réplication. Dans la plupart des cas, ce paramètre peut être modifié une fois que le compte de stockage hello est configuré. 

Tous les comptes de stockage disposent du **stockage localement redondant (LRS)**. Cela signifie que les trois copies de vos données sont gérés par le stockage Azure dans le centre de données hello spécifié lorsque compte de stockage hello a été configuré. Lorsque les modifications sont validée tooone copier, hello autres deux copies sont mis à jour avant de retourner les cas de réussite. Cela signifie hello trois réplicas sont toujours synchronisées. En outre, hello trois copies résident dans des domaines d’erreur distincts et mettre à niveau des domaines, ce qui signifie que vos données sont disponibles même si un nœud de stockage contenant vos données échoue ou est la mise à jour effectuée toobe hors connexion. 

**Stockage localement redondant (LRS)**

Comme expliqué ci-dessus, avec le stockage LRS, vous disposez de trois copies de vos données dans un seul centre de données. Cela permet de gérer problème hello de données deviennent indisponibles si un nœud de stockage échoue ou est effectuée en mode hors connexion toobe mis à jour, mais pas hello cas d’un centre de données entier deviennent indisponibles.

**Stockage redondant dans une zone (ZRS)**

Stockage à redondance de zone (ZRS) maintient hello trois copies locales de vos données ainsi qu’un autre jeu de trois copies de vos données. Hello deuxième ensemble de trois copies est répliquée de manière asynchrone dans les centres de données au sein d’une ou deux régions. Remarque : Le stockage ZRS est uniquement disponible pour les objets blob de blocs dans les comptes de stockage à usage général. En outre, une fois que vous avez créé votre compte de stockage et sélectionné ZRS, vous ne peut pas convertir toouse tooany autre type de réplication, ou vice versa.

Les comptes ZRS fournissent confère une durabilité supérieure par rapport au stockage LRS, mais les comptes ZRS ne disposent pas de mesures ni de capacité d’enregistrement. 

**Stockage géo-redondant (GRS)**

Stockage géo-redondant (GRS) maintient hello trois copies locales de vos données dans une région primaire et un autre jeu de trois copies de vos données dans une région secondaire des centaines de miles en dehors de la région principale de hello. Dans l’événement hello d’un échec de la région principale de hello, le stockage Azure bascule toohello la région secondaire. 

**Stockage géo-redondant avec accès en lecture (RA-GRS)** 

Un stockage géo-redondant avec accès en lecture est exactement comme GRS, sauf que vous obtenez les données de toohello d’accès en lecture dans l’emplacement secondaire de hello. Si le centre de données principal hello devient temporairement indisponible, vous pouvez continuer aux données de salutation tooread à partir de l’emplacement secondaire de hello. Cela peut être très utile. Par exemple, vous pourriez avoir une application web qui se transforme en mode lecture seule et de points de copie secondaire de toohello, ce qui permet un accès, même si elles ne sont pas disponibles. 

> [!IMPORTANT]
> Vous pouvez modifier la façon dont vos données sont répliquées une fois que votre compte de stockage a été créé, à moins que vous avez spécifié ZRS lorsque vous avez créé le compte de hello. Toutefois, notez que vous risquez de subir un supplémentaires frais de transfert si vous passez du LRS tooGRS ou RA-GRS.
>

Pour en savoir plus, consultez [Réplication de Stockage Azure](storage-redundancy.md).

Pour plus d’informations de récupération d’urgence, consultez [le toodo en cas de panne de stockage Azure](storage-disaster-recovery-guidance.md).

Pour obtenir un exemple de procédure tooleverage RA-GRS tooensure haute disponibilité du stockage, consultez [conception hautement disponible d’Applications à l’aide de RA-GRS](storage-designing-ha-apps-with-ragrs.md).

## <a name="transferring-data-tooand-from-azure-storage"></a>Transfert de données tooand depuis le stockage Azure

Vous pouvez utiliser hello AzCopy utilitaire de ligne de commande toocopy blob et données de fichier au sein de votre compte de stockage ou entre les comptes de stockage. Consultez les articles hello suivantes de l’aide :

* [Transférer des données avec AzCopy pour Windows](storage-use-azcopy.md)
* [Transférer des données avec AzCopy pour Linux](storage-use-azcopy-linux.md)

AzCopy est construite sur hello [bibliothèque de déplacement des données Azure](https://www.nuget.org/packages/Microsoft.Azure.Storage.DataMovement/), qui est actuellement disponible en version préliminaire.

Hello service Azure Import/Export peut être utilisé tooimport ou exportation de grandes quantités de tooor des données blob à partir de votre compte de stockage. Vous préparez et plusieurs disques durs tooan Azure centre de données où elles transférera les données de salutation à partir de disques durs de hello et renvoyer les disques durs hello tooyou. Pour plus d’informations sur le service d’importation/exportation de hello, consultez [utiliser hello Service Microsoft Azure Import/Export tooTransfer données tooBlob stockage](../storage-import-export-service.md).

## <a name="pricing"></a>Tarification

Pour plus d’informations sur la tarification pour le stockage Azure, consultez hello [page de tarification](https://azure.microsoft.com/pricing/details/storage/blobs/).

## <a name="storage-apis-libraries-and-tools"></a>Outils, bibliothèques et API de stockage
Les ressources Azure Storage sont accessibles par n’importe quel langage capable de créer des requêtes HTTP/HTTPS. Par ailleurs, Stockage Azure offre des bibliothèques de programmation pour plusieurs langages répandus. Ces bibliothèques simplifient l’utilisation du stockage Azure sous de nombreux aspects en gérant des détails tels que l’invocation synchrone et asynchrone, le traitement par lots des opérations, la gestion des exceptions, les nouvelles tentatives automatiques, le comportement opérationnel, etc. Bibliothèques sont actuellement disponibles pour hello suivant langues et plateformes, avec d’autres personnes dans hello pipeline :

### <a name="azure-storage-data-services"></a>Services de données Azure Storage
* [API REST des services de stockage](/rest/api/storageservices/)
* [Bibliothèque cliente de stockage pour .NET](https://docs.microsoft.com/dotnet/api/?view=azurestorage-8.1.1)
* [Bibliothèque cliente de stockage pour C++](https://github.com/Azure/azure-storage-cpp)
* [Bibliothèque cliente de stockage pour Java/Android](https://azure.microsoft.com/develop/java/)
* [Bibliothèque cliente de stockage pour Node.js](http://dl.windowsazure.com/nodestoragedocs/index.html)
* [Bibliothèque cliente de stockage pour PHP](https://azure.microsoft.com/develop/php/)
* [Bibliothèque cliente de stockage pour Python](https://azure.microsoft.com/develop/python/)
* [Bibliothèque cliente de stockage pour Ruby](https://azure.microsoft.com/develop/ruby/)
* [Cmdlets de stockage pour PowerShell](/powershell/module/azure.storage/?view=azurermps-4.1.0&viewFallbackFrom=azurermps-4.0.0)
* [Commandes de stockage pour CLI 2.0](/cli/azure/storage)

## <a name="next-steps"></a>Étapes suivantes

* [En savoir plus sur le stockage d’objets blob](../blobs/storage-blobs-introduction.md)
* [En savoir plus sur le stockage de fichiers](../storage-files-introduction.md)
* [En savoir plus sur le stockage de file d’attente](../queues/storage-queues-introduction.md)

<!-- RE-ENABLE THESE AFTER MVC GOES LIVE 
tooget up and running with Azure Storage quickly, check out one of hello following Quickstarts:
* [Create a storage account using PowerShell](storage-quick-create-storage-account-powershell.md)
* [Create a storage account using CLI](storage-quick-create-storage-account-cli.md)
-->

<!-- FIGURE OUT WHAT tooDO WITH ALL THESE LINKS.

Azure Storage resources can be accessed by any language that can make HTTP/HTTPS requests. Additionally, Azure Storage offers programming libraries for several popular languages. These libraries simplify many aspects of working with Azure Storage by handling details such as synchronous and asynchronous invocation, batching of operations, exception management, automatic retries, operational behavior and so forth. Libraries are currently available for hello following languages and platforms, with others in hello pipeline:

### Azure Storage data services
* [Storage Services REST API](https://docs.microsoft.com/rest/api/storageservices/)
* [Storage Client Library for .NET](https://docs.microsoft.com/dotnet/api/?view=azurestorage-8.1.1)
* [Storage Client Library for C++](https://github.com/Azure/azure-storage-cpp)
* [Storage Client Library for Java/Android](https://azure.microsoft.com/develop/java/)
* [Storage Client Library for Node.js](http://dl.windowsazure.com/nodestoragedocs/index.html)
* [Storage Client Library for PHP](https://azure.microsoft.com/develop/php/)
* [Storage Client Library for Python](https://azure.microsoft.com/develop/python/)
* [Storage Client Library for Ruby](https://azure.microsoft.com/develop/ruby/)
* [Storage Cmdlets for PowerShell](/powershell/module/azure.storage/?view=azurermps-4.1.0&viewFallbackFrom=azurermps-4.0.0)

### Azure Storage management services
* [Storage Resource Provider REST API Reference](/rest/api/storagerp/)
* [Storage Resource Provider Client Library for .NET](/dotnet/api/microsoft.azure.management.storage)
* [Storage Resource Provider Cmdlets for PowerShell 1.0](/powershell/module/azure.storage)
* [Storage Service Management REST API (Classic)](https://msdn.microsoft.com/library/azure/ee460790.aspx)

### Azure Storage data movement services
* [Storage Import/Export Service REST API](../storage-import-export-service.md)
* [Storage Data Movement Client Library for .NET](https://www.nuget.org/packages/Microsoft.Azure.Storage.DataMovement/)

### Tools and utilities
* [Microsoft Azure Storage Explorer](../../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.
* [Azure Storage Client Tools](../storage-explorers.md)
* [Azure SDKs and Tools](https://azure.microsoft.com/tools/)
* [Azure Storage Emulator](http://www.microsoft.com/download/details.aspx?id=43709)
* [Azure PowerShell](/powershell/azure/overview)
* [AzCopy Command-Line Utility](http://aka.ms/downloadazcopy)

## Next steps
toolearn more about Azure Storage, explore these resources:

### Documentation
* [Azure Storage Documentation](https://azure.microsoft.com/documentation/services/storage/)
* [Create a storage account](../storage-create-storage-account.md)

<!-- after our quick starts are available, replace this link with a link tooone of those. 
Had tooremove this article, it refers toohello VS quickstarts, and they've stopped publishing them. Robin --> 
<!--* [Get started with Azure Storage in five minutes](storage-getting-started-guide.md)
-->

### <a name="for-administrators"></a>Pour les administrateurs
* [Utilisation d'Azure PowerShell avec Azure Storage](storage-powershell-guide-full.md)
* [Utilisation de la CLI Microsoft Azure avec Microsoft Azure Storage](../storage-azure-cli.md)

### <a name="for-net-developers"></a>Pour les développeurs .NET
* [Prise en main d’Azure Blob Storage à l’aide de .NET](../blobs/storage-dotnet-how-to-use-blobs.md)
* [Prise en main d’Azure Table Storage à l’aide de .NET](../../cosmos-db/table-storage-how-to-use-dotnet.md)
* [Prise en main du stockage de files d’attente Azure à l’aide de .NET](../storage-dotnet-how-to-use-queues.md)
* [Prise en main d’Azure File Storage sur Windows](../storage-dotnet-how-to-use-files.md)

### <a name="for-javaandroid-developers"></a>Pour les développeurs Java/Android
* [Comment toouse stockage d’objets Blob à partir de Java](../blobs/storage-java-how-to-use-blob-storage.md)
* [Comment toouse le stockage de Table à partir de Java](../../cosmos-db/table-storage-how-to-use-java.md)
* [Comment toouse stockage de file d’attente à partir de Java](../storage-java-how-to-use-queue-storage.md)
* [Comment toouse stockage de fichiers à partir de Java](../storage-java-how-to-use-file-storage.md)

### <a name="for-nodejs-developers"></a>Pour les développeurs Node.js
* [Comment toouse stockage d’objets Blob à partir de Node.js](../blobs/storage-nodejs-how-to-use-blob-storage.md)
* [Comment toouse le stockage de Table à partir de Node.js](../../cosmos-db/table-storage-how-to-use-nodejs.md)
* [Comment toouse stockage de file d’attente à partir de Node.js](../storage-nodejs-how-to-use-queues.md)

### <a name="for-php-developers"></a>Pour les développeurs PHP
* [Comment toouse stockage d’objets Blob à partir de PHP](../blobs/storage-php-how-to-use-blobs.md)
* [Comment toouse le stockage de Table à partir de PHP](../../cosmos-db/table-storage-how-to-use-php.md)
* [Comment toouse stockage de file d’attente à partir de PHP](../storage-php-how-to-use-queues.md)

### <a name="for-ruby-developers"></a>Pour les développeurs Ruby
* [Comment toouse stockage d’objets Blob à partir de Ruby](../blobs/storage-ruby-how-to-use-blob-storage.md)
* [Comment toouse le stockage de Table à partir de Ruby](../../cosmos-db/table-storage-how-to-use-ruby.md)
* [Comment toouse stockage de file d’attente à partir de Ruby](../storage-ruby-how-to-use-queue-storage.md)

### <a name="for-python-developers"></a>Pour les développeurs Python
* [Comment toouse stockage d’objets Blob à partir de Python](../blobs/storage-python-how-to-use-blob-storage.md)
* [Comment toouse le stockage de Table à partir de Python](../../cosmos-db/table-storage-how-to-use-python.md)
* [Comment toouse stockage de file d’attente à partir de Python](../storage-python-how-to-use-queue-storage.md)   
* [Comment toouse stockage de fichiers à partir de Python](../storage-python-how-to-use-file-storage.md) 
-->