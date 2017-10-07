---
title: aaaIntroduction tooAzure stockage | Documents Microsoft
description: "Vue d’ensemble du stockage Azure, stockage de données en ligne de Microsoft dans le cloud de hello. Découvrez comment toouse hello la meilleure solution de stockage cloud disponibles dans vos applications."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: a4a1bc58-ea14-4bf5-b040-f85114edc1f1
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/26/2017
ms.author: marsma
ms.openlocfilehash: dec8280c77f4b23df4c2a471e1d755e365c14e58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toomicrosoft-azure-storage"></a>Introduction tooMicrosoft stockage Azure

## <a name="overview"></a>Vue d'ensemble
Stockage Azure est la solution de stockage cloud hello pour les applications modernes qui s’appuient sur la durabilité, disponibilité et évolutivité toomeet hello aux besoins de leurs clients. En lisant cet article, les développeurs, les professionnels de l’informatique et les décideurs économiques peuvent découvrir :

* ce qu’est Azure Storage et comment vous pouvez en tirer parti dans vos applications cloud, mobiles, serveur et bureautiques ;
* Les types de données que vous pouvez stocker avec les services de stockage Azure hello : objet blob de données (objet), les données de table NoSQL, les messages de la file d’attente et les partages de fichiers.
* La gestion de données de tooyour d’accès dans le stockage Azure
* comment vos données Azure Storage sont préservées par la redondance et la réplication ;
* Où les toobuild suivant toogo votre première application Azure Storage

<!-- after our quick starts are available, replace this link with a link tooone of those. 
Had tooremove this article, it refers toohello VS quickstarts, and they've stopped publishing them. Robin --> 
<!-- tooget up and running with Azure Storage quickly, see [Get started with Azure Storage in five minutes](storage-getting-started-guide.md). -->

Pour plus d’informations sur les outils, bibliothèques et autres ressources pour utiliser Azure Storage, consultez [Étapes suivantes](#next-steps) ci-dessous.

## <a name="what-is-azure-storage"></a>Présentation d’Azure Storage
Le cloud computing permet d'élaborer de nouveaux scénarios pour les applications qui exigent un stockage évolutif, durable et à haute disponibilité pour leurs données, et c'est la raison pour laquelle Microsoft a développé Azure Storage. En outre toomaking il possible pour de nouveaux scénarios développeurs toobuild applications à grande échelle toosupport, le stockage Azure propose également hello storage foundation Machines virtuelles pour Azure, une robustesse de tooits témoigne supplémentaire.

Le stockage Azure est très évolutif, donc vous pouvez stocker et traiter des centaines de téraoctets de données toosupport hello big de scénarios de données requis par une analyse scientifique et financière et les applications de support. Ou vous pouvez stocker hello petites quantités de données requises pour un site Web de petite entreprise. Chaque fois que vos besoins se situent, vous payez uniquement pour les données hello que vous stockez. Azure Storage stocke actuellement des dizaines de billions d'objets client uniques et traite en moyenne des millions de requêtes par seconde.

Le stockage Azure est élastique, afin de pouvoir concevoir des applications pour un public international volumineux et l’échelle de ces applications en fonction des besoins - à la fois en termes de quantité hello des données stockées et hello du nombre de demandes effectuées par rapport à elle. Vous payez uniquement pour ce que vous utilisez, et pour la durée d'utilisation.

Azure Storage utilise un système de partitionnement automatique qui équilibre automatiquement la charge représentée par vos données sur la base du trafic. Cela signifie que, selon les besoins de hello sur le développement de votre application, le stockage Azure alloue automatiquement hello ressources appropriées toomeet les.

Le stockage Azure est accessible à partir de n’importe où dans hello world, dans n’importe quel type d’application, si elle s’exécute dans le cloud hello, sur le bureau de hello, sur un serveur local ou sur un appareil mobile ou tablette. Vous pouvez utiliser le stockage Azure dans les scénarios où application hello stocke un sous-ensemble de données sur l’appareil de hello et il synchronise avec un jeu complet des données stockées dans le cloud de hello.

Azure Storage prend en charge les clients avec divers systèmes d’exploitation (notamment Windows et Linux) et divers langages de programmation (notamment .NET, Java, Node.js, Python, Ruby, PHP et C++, ainsi que les langages de programmation mobiles) pour un développement pratique. Le stockage Azure expose également les ressources de données via les API REST simple, qui sont des clients disponibles tooany capable d’envoyer et recevoir des données via HTTP/HTTPS.

Azure Premium Storage offre des performances élevées et une prise en charge à faible latence du disque pour des charges de travail d’E/S intensives exécutées sur Azure Virtual Machines. Avec le stockage Azure Premium, vous pouvez attacher plusieurs données persistantes disques tooa virtual machines et configurez-les toomeet vos besoins. Chaque disque de données est approvisionné par un disque SSD dans Azure Premium Storage pour une performance d’E/S maximale. Pour plus d’informations, consultez [Stockage Premium : stockage hautes performances pour les charges de travail des machines virtuelles Azure](storage-premium-storage.md) .

## <a name="introducing-hello-azure-storage-services"></a>Présentation des services de stockage Azure hello
Le stockage Azure fournit hello suivant quatre services : stockage, le stockage de Table, stockage de file d’attente et le stockage de fichiers d’objets Blob.

* Blob Storage stocke les données d’objets non structurées. Un objet blob peut correspondre à n'importe quel type de données texte ou binaires, par exemple, un document, un fichier multimédia ou un programme d'installation d'application. Stockage d’objets BLOB est également référencé tooas stockage d’objets.
* Table Storage stocke des jeux de données structurés. Stockage de table est un magasin de données d’attribut de clé NoSQL, qui permet un développement rapide et quantités de toolarge un accès rapide des données.
* Queue Storage fournit une messagerie fiable pour le traitement des flux de travail et pour la communication entre les composants des services cloud.
* Stockage de fichiers offre un stockage partagé pour les applications héritées à l’aide du protocole SMB standard de hello. Machines virtuelles et services de cloud computing peuvent partager des données de fichier entre les composants d’application via des partages montés, et des applications locales peuvent accéder à des données de fichier dans un partage via hello API REST du service de fichier.

Un compte de stockage Azure est un compte sécurisé qui vous donne accès tooservices dans le stockage Azure. Votre compte de stockage fournit l’espace de noms unique hello pour vos ressources de stockage. image Hello ci-dessous montre les relations entre les ressources de stockage Azure hello dans un compte de stockage hello :

![Azure Storage Resources](./media/storage-introduction/storage-concepts.png)

[!INCLUDE [storage-account-types-include](../../includes/storage-account-types-include.md)]

[!INCLUDE [storage-versions-include](../../includes/storage-versions-include.md)]

## <a name="blob-storage"></a>Stockage d'objets blob
Pour les utilisateurs de grandes quantités de toostore de données d’objet non structurées dans le cloud de hello, stockage d’objets Blob offre une solution économique et évolutive. Vous pouvez utiliser le contenu toostore stockage Blob tels que :

* Documents
* Données sociales telles que photos, vidéos, musique et blogs
* Sauvegardes de fichiers, d'ordinateurs, de bases de données et d'appareils
* Images et textes pour applications Web
* Données de configuration pour applications cloud
* Big Data tels que journaux et autres jeux de données volumineux

Chaque objet blob est organisé dans un conteneur. Les conteneurs fournissent également un toogroups de stratégies de sécurité de tooassign moyen utile d’objets. Un compte de stockage peut contenir n’importe quel nombre de conteneurs, et un conteneur peut contenir n’importe quel nombre d’objets BLOB, de la limite de capacité de 500 To toohello hello du compte de stockage.

Le stockage d’objets blob propose trois types d’objets : les objets blob de bloc, les objets blob d’ajout et les objets blob de page (disques).

* Les objets blob de bloc sont optimisés pour la diffusion en continu et le stockage d’objets cloud. Ils constituent une solution de choix pour stocker des documents, des fichiers multimédias, des sauvegardes, etc.
* Ajouter des objets BLOB sont des objets BLOB de tooblock similaire, mais sont optimisés pour les opérations d’ajout. Un objet blob d’ajout peut être mis à jour qu’en ajoutant une nouvelle fin toohello de bloc. Ajouter les objets BLOB sont un bon choix pour les scénarios tels que la journalisation, où les nouvelles données doivent toobe écrit uniquement toohello fin de l’objet blob de hello.
* Objets BLOB de pages est optimisés pour représenter les disques IaaS et prise en charge aléatoire écrit et peut être jusqu'à to too1 taille. Un disque IaaS rattaché à un réseau de machines virtuelles Azure est un disque dur virtuel stocké en tant qu'objet blob de page.

Pour les jeux de données où les contraintes de réseau effectuer le chargement ou téléchargement de stockage des données tooBlob acheminement hello irréaliste très volumineux, vous pouvez expédier un tooimport tooMicrosoft de disque dur ou exporter des données directement à partir de centre de données hello. Consultez [utiliser hello Service Microsoft Azure Import/Export tooTransfer données tooBlob stockage](storage-import-export-service.md).

## <a name="table-storage"></a>Stockage de tables

[!INCLUDE [storage-table-cosmos-db-tip-include](../../includes/storage-table-cosmos-db-tip-include.md)]

Les applications modernes exigent souvent des magasins de données avec plus d'évolutivité et de souplesse que ne l'exigeaient les précédentes générations de logiciels. Stockage de table offre un stockage hautement disponible et très évolutif, afin que votre application peut automatiquement mettre à l’échelle à la demande de toomeet utilisateur. Le Stockage Table est le magasin de clés/attributs NoSQL de Microsoft ; il a une conception sans schéma, ce en quoi il diffère des bases de données relationnelles classiques. Avec un magasin de données schemaless, il est facile tooadapt d’evolve de votre application a besoin de vos données en tant que hello. Stockage de table étant toouse simple, les développeurs peuvent créer rapidement des applications. Accès toodata est rapide et économique pour tous les types d’applications.  Normalement, le stockage de tables est considérablement moins coûteux que le SQL traditionnel pour des volumes de données similaires.

Le stockage de tables est un magasin de clés/attributs : cela signifie que chaque valeur dans une table est stockée avec un nom de propriété typé. nom de la propriété Hello peut être utilisé pour le filtrage et la spécification des critères de sélection. Une collection de propriétés et leurs valeurs constituent une entité. Étant donné que le stockage de Table est schemaless, deux entités dans hello même table peut contenir différents ensembles de propriétés, et ces propriétés peuvent être de types différents.

Vous pouvez utiliser la Table stockage toostore flexible jeux de données, telles que les données utilisateur pour les applications web, carnets d’adresses, les informations de périphérique et tout autre type de métadonnées nécessaires à votre service.  Vous pouvez stocker n’importe quel nombre d’entités dans une table, et un compte de stockage peut contenir n’importe quel nombre de tables, des limites de capacité toohello hello du compte de stockage.

Comme les objets BLOB et files d’attente, les développeurs peuvent gérer et accéder au stockage de Table à l’aide de protocoles standard de REST et toutefois stockage de Table également prend en charge un sous-ensemble du protocole OData de hello, ce qui simplifie les avancées de fonctions d’interrogation et de l’activation de JSON et AtomPub (XML basé) met en forme.

Pour les applications d’aujourd'hui basés sur Internet, tels que le stockage de Table, les bases de données NoSQL offrent un tootraditional autre populaires bases de données relationnelles.

## <a name="queue-storage"></a>Stockage de files d'attente
Lors de la conception d'applications pour la mise à l'échelle, des composants d'application sont souvent découplés, de sorte qu'ils peuvent être mis à l'échelle indépendamment. Stockage de file d’attente fournit une solution de messagerie fiable pour la communication asynchrone entre les composants d’application, qu’elles s’exécutent dans le cloud hello, sur le bureau de hello, sur un serveur local ou sur un appareil mobile. Le Stockage File d'attente prend également en charge la gestion des tâches asynchrones et la création des workflows de processus.

Un compte de stockage peut contenir un nombre quelconque de files d'attente. Une file d’attente peut contenir n’importe quel nombre de messages, des limites de capacité toohello hello du compte de stockage. Les messages individuels peuvent être des too64 Ko.

## <a name="file-storage"></a>Stockage Fichier
Hello service de fichiers Azure vous permet de tooset des partages de fichiers réseau hautement disponible qui sont accessibles à l’aide du protocole Server Message Block (SMB) standard de hello. Que signifie que plusieurs machines virtuelles peuvent partager hello même les fichiers en lecture et accès en écriture. Vous pouvez également lire les fichiers de hello via l’interface REST de hello ou des bibliothèques clientes de stockage hello.

Une chose qui le distingue du stockage Azure Files à partir de fichiers sur un partage de fichiers d’entreprise est que vous pouvez accéder à des fichiers de hello depuis n’importe où dans Bonjour à l’aide d’une URL qui pointe le fichier de toohello et inclut un jeton de signature (SAP) d’accès partagé. Vous pouvez générer des jetons SAS ; ils autoriser accès spécifique tooa privé pour une durée spécifique.

Les partages de fichiers peuvent être utilisés dans de nombreux scénarios courants :

* Par exemple, de nombreuses applications locales utilisent les partages de fichiers. Cette fonctionnalité permet de toomigrate plus facilement les applications qui partagent des données tooAzure. Si vous montez hello toohello de partage de fichier même lettre hello de lecteur local application utilise, partie hello de votre application qui accède au partage de fichiers hello doit fonctionner avec des modifications minimales, le cas échéant.

* Les fichiers de configuration peuvent être stockés sur un partage de fichiers et sont accessibles à partir de plusieurs machines virtuelles. Outils et utilitaires utilisées par plusieurs développeurs dans un groupe peuvent être stockées sur un partage de fichiers, s’assurer que tout le monde peut trouver, et qu’elles utilisent hello même version.

* Journaux de diagnostic, les mesures et les vidages sur incident sont trois exemples de données qui peuvent être écrites de partage de fichiers tooa et traitées ou analyser ultérieurement.

Listes de contrôle (ACL) à ce temps, l’authentification basée sur Active Directory et l’accès ne sont pas pris en charge, mais elles seront à un moment donné dans hello futures. informations d’identification de compte de stockage Hello sont utilisées tooprovide l’authentification pour le partage de fichiers toohello accès. Cela signifie que toute personne avec partage hello monté aura le partage de toohello d’accès complet en lecture/écriture.

## <a name="access-tooblob-table-queue-and-file-resources"></a>Accès tooBlob, Table, de file d’attente et de fichier de ressources
Par défaut, seul hello stockage propriétaire du compte peut accéder aux ressources de stockage Azure hello. Pour une sécurité hello de vos données, chaque demande adressée aux ressources de votre compte doit être authentifiée. L'authentification s'appuie sur un modèle de clé partagée. Objets BLOB peut également être toosupport configuré l’authentification anonyme.

Deux clés d'accès privées sont attribuées à votre compte de stockage lors de sa création. Elles sont utilisées pour l'authentification. Deux clés permet de garantir que votre application reste disponible lorsque vous régénérez régulièrement les clés hello en pratique de gestion de clés de sécurité courantes.

Si vous avez besoin des ressources de stockage tooyour tooallow utilisateurs sous contrôlés de l’accès, vous pouvez créer une signature d’accès partagé. Une signature d’accès partagé (SAS) est un jeton qui peut être ajouté tooa les URL qu’Active délégué accès tooa des ressources de stockage. Toute personne qui possède le jeton de hello peut accéder aux ressources hello qu'il pointe il spécifie des autorisations hello toowith, pour la période hello qu’elle est valide. Depuis la version 2015-04-05, Azure Storage prend en charge deux types de signatures d'accès partagé : SAP de service et SAP de compte SAP.

les délégués SAS Hello service d’accès tooa des ressources dans un seul des services de stockage hello : hello service Blob, file d’attente, Table ou de fichier.

Un compte SAP délègue tooresources d’accès dans une ou plusieurs des services de stockage hello. Vous pouvez déléguer des opérations tooservice de niveau d’accès qui ne sont pas disponibles avec un service SAS. Vous pouvez également déléguer l’accès tooread, écriture et les opérations de suppression sur les conteneurs d’objets blob, tables, files d’attente et les partages de fichiers qui ne sont pas autorisées avec un service SAS.

Enfin, vous pouvez spécifier qu'un conteneur et ses objets blob, ou un objet blob particulier, sont disponibles pour l'accès public. Lorsque vous indiquez qu'un conteneur ou un objet blob est public, n'importe qui peut le lire de manière anonyme ; aucune authentification n'est requise.  Les conteneurs et les objets blob publics sont utiles pour exposer des ressources telles que des médias et des documents hébergés sur des sites Web.  toodecrease latence du réseau pour un public international, vous pouvez mettre en cache les données blob utilisées par les sites Web avec hello Azure CDN.

Pour plus d’informations sur les signatures d’accès partagé, consultez [Utilisation des signatures d’accès partagé (SAP)](storage-dotnet-shared-access-signature-part-1.md) . Consultez [gérer l’accès en lecture anonyme toocontainers et les objets BLOB](storage-manage-access-to-resources.md) et [l’authentification pour hello Services de stockage Azure](https://msdn.microsoft.com/library/azure/dd179428.aspx) pour plus d’informations sur le compte de stockage tooyour un accès sécurisé.

## <a name="replication-for-durability-and-high-availability"></a>Réplication pour la durabilité et la haute disponibilité
Hello dans votre compte de stockage est toujours de Microsoft Azure répliquées tooensure la durabilité et la haute disponibilité. Copies de réplication hello de vos données, au sein même centre de données ou la deuxième centre de données tooa, selon l’option de réplication que vous choisissez. La réplication protège vos données et préserve votre application un temps d’exécution dans l’événement hello de défaillances matérielles temporaires. Si vos données sont répliquées tooa deuxième centre de données, également protège vos données contre une défaillance irrémédiable dans l’emplacement principal de hello.

La réplication garantit que votre compte de stockage répond aux hello [contrat de niveau de Service (SLA) pour le stockage](https://azure.microsoft.com/support/legal/sla/storage/) même en face de hello d’échecs. Consultez hello SLA pour plus d’informations sur le stockage Azure des garanties de durabilité et de disponibilité.

Lorsque vous créez un compte de stockage, vous pouvez sélectionner un des hello options de réplication suivantes :

* **Stockage localement redondant (LRS).** Le stockage localement redondant effectue trois copies de vos données. Le stockage LRS est répliqué trois fois par centre de données et par région. LRS protège vos données contre les défaillances matérielles normales, mais pas à partir de la défaillance de hello d’un centre de données.

    Vous pouvez bénéficier d'une réduction pour le stockage LRS. Pour une durabilité maximale, nous vous recommandons d’utiliser le stockage géo-redondant décrit ci-dessous.
* **Stockage redondant dans une zone (ZRS).** Le stockage redondant dans une zone effectue trois copies de vos données. Le stockage ZRS est répliqué trois fois sur deux installations toothree, dans un ou deux régions, en fournissant une durabilité élevée au stockage LRS. Le stockage ZRS garantie la durabilité de vos données au sein d'une même région.

    Le stockage ZRS offre un niveau de durabilité supérieur à celui du stockage LRS ; toutefois, pour une durabilité maximale, nous vous recommandons d'utiliser le stockage géo-redondant décrit ci-dessous.

  > [!NOTE]
  > ZRS est actuellement disponible uniquement pour les objets BLOB de blocs et est pris en charge uniquement dans les versions 2014-02-14 et versions ultérieures.
  >
  > Une fois que vous avez créé votre compte de stockage et sélectionné ZRS, vous ne pouvez pas convertir toouse tooany autres type de réplication, ou vice versa.
  >
  >
* **Stockage géo-redondant (GRS)**. Le stockage GRS effectue six copies de vos données. Avec GRS, vos données sont répliquées trois fois au sein de la région principale de hello et sont également répliquées trois fois dans une région secondaire des centaines de miles en dehors de la région principale hello, fournissant hello plus haut niveau de durabilité. Dans événement hello d’un échec de la région principale de hello, le stockage Azure sera région secondaire de basculement toohello. Le stockage GRS assure la durabilité de vos données dans deux régions distinctes.

    Pour plus d’informations sur les associations de régions principales et secondaires, voir [Régions Azure](https://azure.microsoft.com/regions/).
* **Stockage géo-redondant avec accès en lecture (RA-GRS)**. Un stockage géo-redondant avec accès en lecture réplique vos données tooa secondaire géographique et fournit également des données de tooyour d’accès en lecture dans l’emplacement secondaire de hello. Un stockage géo-redondant avec accès en lecture vous permet de tooaccess vos données à partir de hello principal ou emplacement secondaire hello, dans l’événement hello qu’un seul emplacement devient indisponible. Un stockage géo-redondant avec accès en lecture est l’option par défaut de hello pour votre compte de stockage par défaut lors de sa création.

  > [!IMPORTANT]
  > Vous pouvez modifier la façon dont vos données sont répliquées une fois que votre compte de stockage a été créé, à moins que vous avez spécifié ZRS lorsque vous avez créé le compte de hello. Toutefois, notez que vous risquez de subir un supplémentaires frais de transfert si vous passez du LRS tooGRS ou RA-GRS.
  >
  >

Pour plus d’informations sur les options de réplication de stockage, voir [Réplication Azure Storage](storage-redundancy.md) .

Pour plus d’informations sur la tarification relative à la réplication du compte de stockage, consultez la page [Prix appliqués à Azure Storage](https://azure.microsoft.com/pricing/details/storage/). Pour plus d’informations sur les services disponibles dans chaque région, voir [Régions Azure](https://azure.microsoft.com/regions/#services) .

Pour plus d’informations sur la durabilité avec Azure Storage, consultez [Document SOSP - Azure Storage : service de stockage sur le cloud à haute disponibilité et à cohérence forte](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx).

## <a name="transferring-data-tooand-from-azure-storage"></a>Transfert de données tooand depuis le stockage Azure
Vous pouvez utiliser le blob de toocopy hello AzCopy utilitaire de ligne de commande, de fichier et de données de la table au sein de votre compte de stockage ou entre les comptes de stockage. Consultez [transférer des données avec l’utilitaire de ligne de commande AzCopy de hello](storage-use-azcopy.md) pour plus d’informations.

AzCopy est construite sur hello [bibliothèque de déplacement des données Azure](https://www.nuget.org/packages/Microsoft.Azure.Storage.DataMovement/), qui est actuellement disponible en version préliminaire.

Hello service Azure Import/Export fournit un moyen tooimport objet blob de données dans ou exporter des données blob à partir de votre compte de stockage via un disque dur envoyé du centre de données Azure toohello. Pour plus d’informations sur le service d’importation/exportation de hello, consultez [utiliser hello Service Microsoft Azure Import/Export tooTransfer données tooBlob stockage](storage-import-export-service.md).

## <a name="pricing"></a>Tarification
[!INCLUDE [storage-account-billing-include](../../includes/storage-account-billing-include.md)]

## <a name="storage-apis-libraries-and-tools"></a>Outils, bibliothèques et API de stockage
Les ressources Azure Storage sont accessibles par n’importe quel langage capable de créer des requêtes HTTP/HTTPS. Par ailleurs, Azure Storage offre des bibliothèques de programmation pour plusieurs langages populaires. Ces bibliothèques simplifient l'utilisation d'Azure Storage sous de nombreux aspects en gérant des détails tels que l'invocation synchrone et asynchrone, le traitement par lots des opérations, la gestion des exceptions, les nouvelles tentatives automatiques, le comportement opérationnel, etc. Bibliothèques sont actuellement disponibles pour hello suivant langues et plateformes, avec d’autres personnes dans hello pipeline :

### <a name="azure-storage-data-services"></a>Services de données Azure Storage
* [API REST des services de stockage](http://msdn.microsoft.com/library/azure/dd179355.aspx)
* [Bibliothèque cliente de stockage pour .NET, Windows Phone et Windows Runtime](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [Bibliothèque cliente de stockage pour C++](https://github.com/Azure/azure-storage-cpp)
* [Bibliothèque cliente de stockage pour Java/Android](https://azure.microsoft.com/develop/java/)
* [Bibliothèque cliente de stockage pour Node.js](http://dl.windowsazure.com/nodestoragedocs/index.html)
* [Bibliothèque cliente de stockage pour PHP](https://azure.microsoft.com/develop/php/)
* [Bibliothèque cliente de stockage pour Ruby](https://azure.microsoft.com/develop/ruby/)
* [Bibliothèque cliente de stockage pour Python](https://azure.microsoft.com/develop/python/)
* [Applets de commande de stockage pour PowerShell 1.0](/powershell/module/azurerm.storage/#storage)

### <a name="azure-storage-management-services"></a>Services de gestion Azure Storage
* [Informations de référence sur l’API REST des fournisseurs de ressources de stockage](/rest/api/storagerp/)
* [Bibliothèque cliente des fournisseurs de ressources de stockage pour .NET](/dotnet/api/microsoft.azure.management.storage)
* [Applets de commande des fournisseurs de ressources de stockage pour PowerShell 1.0](/powershell/module/azure.storage)
* [API REST de gestion des services de stockage (classique)](https://msdn.microsoft.com/library/azure/ee460790.aspx)

### <a name="azure-storage-data-movement-services"></a>Services de déplacement de données Azure Storage
* [API REST du service Import/Export Storage](storage-import-export-service.md)
* [Bibliothèque cliente de déplacement de données de stockage pour .NET](https://www.nuget.org/packages/Microsoft.Azure.Storage.DataMovement/)

### <a name="tools-and-utilities"></a>Outils et utilitaires
* [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) est une application autonome gratuit, à partir de Microsoft qui vous permet de toowork visuellement avec des données de stockage Azure sur Windows, Mac OS et Linux.
* [Outils clients d’Azure Storage](storage-explorers.md)
* [Outils et Kit de développement logiciel (SDK) d’Azure](https://azure.microsoft.com/tools/)
* [Émulateur de stockage Azure](http://www.microsoft.com/download/details.aspx?id=43709)
* [Azure PowerShell](/powershell/azure/overview)
* [Utilitaire de ligne de commande AzCopy](http://aka.ms/downloadazcopy)

## <a name="next-steps"></a>Étapes suivantes
toolearn en savoir plus sur le stockage Azure, Explorez ces ressources :

### <a name="documentation"></a>Documentation
* [Documentation d'Azure Storage](https://azure.microsoft.com/documentation/services/storage/)
* [Créer un compte de stockage](storage-create-storage-account.md)

<!-- after our quick starts are available, replace this link with a link tooone of those. 
Had tooremove this article, it refers toohello VS quickstarts, and they've stopped publishing them. Robin --> 
<!--* [Get started with Azure Storage in five minutes](storage-getting-started-guide.md)
-->

### <a name="for-administrators"></a>Pour les administrateurs
* [Utilisation d'Azure PowerShell avec Azure Storage](storage-powershell-guide-full.md)
* [Utilisation de la CLI Microsoft Azure avec Microsoft Azure Storage](storage-azure-cli.md)

### <a name="for-net-developers"></a>Pour les développeurs .NET
* [Prise en main d’Azure Blob Storage à l’aide de .NET](storage-dotnet-how-to-use-blobs.md)
* [Prise en main d’Azure Table Storage à l’aide de .NET](storage-dotnet-how-to-use-tables.md)
* [Prise en main du stockage de files d’attente Azure à l’aide de .NET](storage-dotnet-how-to-use-queues.md)
* [Prise en main d’Azure File Storage sur Windows](storage-dotnet-how-to-use-files.md)

### <a name="for-javaandroid-developers"></a>Pour les développeurs Java/Android
* [Comment toouse stockage d’objets Blob à partir de Java](storage-java-how-to-use-blob-storage.md)
* [Comment toouse le stockage de Table à partir de Java](storage-java-how-to-use-table-storage.md)
* [Comment toouse stockage de file d’attente à partir de Java](storage-java-how-to-use-queue-storage.md)
* [Comment toouse stockage de fichiers à partir de Java](storage-java-how-to-use-file-storage.md)

### <a name="for-nodejs-developers"></a>Pour les développeurs Node.js
* [Comment toouse stockage d’objets Blob à partir de Node.js](storage-nodejs-how-to-use-blob-storage.md)
* [Comment toouse le stockage de Table à partir de Node.js](storage-nodejs-how-to-use-table-storage.md)
* [Comment toouse stockage de file d’attente à partir de Node.js](storage-nodejs-how-to-use-queues.md)

### <a name="for-php-developers"></a>Pour les développeurs PHP
* [Comment toouse stockage d’objets Blob à partir de PHP](storage-php-how-to-use-blobs.md)
* [Comment toouse le stockage de Table à partir de PHP](storage-php-how-to-use-table-storage.md)
* [Comment toouse stockage de file d’attente à partir de PHP](storage-php-how-to-use-queues.md)

### <a name="for-ruby-developers"></a>Pour les développeurs Ruby
* [Comment toouse stockage d’objets Blob à partir de Ruby](storage-ruby-how-to-use-blob-storage.md)
* [Comment toouse le stockage de Table à partir de Ruby](storage-ruby-how-to-use-table-storage.md)
* [Comment toouse stockage de file d’attente à partir de Ruby](storage-ruby-how-to-use-queue-storage.md)

### <a name="for-python-developers"></a>Pour les développeurs Python
* [Comment toouse stockage d’objets Blob à partir de Python](storage-python-how-to-use-blob-storage.md)
* [Comment toouse le stockage de Table à partir de Python](storage-python-how-to-use-table-storage.md)
* [Comment toouse stockage de file d’attente à partir de Python](storage-python-how-to-use-queue-storage.md)
* [Comment toouse stockage de fichiers à partir de Python](storage-python-how-to-use-file-storage.md)
