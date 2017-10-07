---
title: "aaaUsing Azure Import/Export tootransfer données tooand depuis le stockage blob | Documents Microsoft"
description: "Découvrez comment toocreate importer et exporter les tâches Bonjour portail Azure pour le transfert de données tooand depuis le stockage blob."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 668f53f2-f5a4-48b5-9369-88ec5ea05eb5
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2017
ms.author: muralikk
ms.openlocfilehash: 84471d736d2433ffee9f49fbef91856d3dd56bb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-microsoft-azure-importexport-service-tootransfer-data-tooblob-storage"></a>Utiliser le stockage de tooblob du service tootransfer données hello Microsoft Azure Import/Export
Hello service Azure Import/Export vous permet de toosecurely transfèrent de grandes quantités de stockage d’objets blob de données tooAzure par centre de données Azure expédition des lecteurs de disque dur tooan. Vous pouvez également utiliser ces données tootransfer de service à partir de lecteurs de disque de toohard de stockage blob Azure et expédier tooyour sur site local. Ce service est approprié dans les situations où vous souhaitez tootransfer plusieurs téraoctets (To) de tooor de données à partir d’Azure, mais chargement ou téléchargement réseau hello est impossible en raison de la bande passante toolimited ou élevé les coûts de réseau.

service de Hello requiert que les lecteurs de disque dur doit être chiffré pour la sécurité de vos données hello BitLocker. service de Hello prend en charge les deux hello classique et Azure Resource Manager comptes de stockage (niveau standard et froid) présentes dans toutes les régions hello Azure publique. Vous devez expédier tooone de lecteurs de disque dur des emplacements hello pris en charge spécifiées plus loin dans cet article.

Dans cet article, vous en savoir plus sur le service d’importation/exportation Azure hello et comment tooship lecteurs pour la copie de votre tooand de données à partir du stockage d’objets Blob Azure.

## <a name="when-should-i-use-hello-azure-importexport-service"></a>Quand dois-je utiliser le service d’importation/exportation Azure hello ?
Envisagez d’utiliser le service Azure Import/Export lors du téléchargement ou le téléchargement des données réseau hello est trop lent, ou mise en route de la bande passante réseau supplémentaire est onéreux.

Vous pouvez utiliser ce service dans des scénarios tels que :

* Migration cloud toohello de données : déplacer de grandes quantités de données tooAzure rapidement et à moindre coût.
* La distribution de contenu : envoyer rapidement des sites clients tooyour de données.
* Sauvegarde : Effectuer des sauvegardes de votre toostore de données locale dans le stockage blob Azure.
* Récupération de données : récupérer la grande quantité de données stockées dans le stockage d’objets blob et fournir l’emplacement de tooyour local.

## <a name="prerequisites"></a>Composants requis
Dans cette section nous liste toouse de hello conditions préalables requises à ce service. Vérifiez-les soigneusement avant d’expédier vos disques.

### <a name="storage-account"></a>Compte de stockage
Vous devez disposer d’un abonnement Azure et un ou plusieurs comptes toouse hello importation/exportation de service de stockage de. Chaque travail peut être tooor de données tootransfer utilisé à partir d’un seul compte de stockage. Autrement dit, une même tâche d’importation/exportation ne peut pas englober plusieurs comptes de stockage. Pour plus d’informations sur la création d’un compte de stockage, consultez [comment tooCreate un compte de stockage](storage-create-storage-account.md#create-a-storage-account).

### <a name="blob-types"></a>Types d’objet blob
Vous pouvez utiliser des données toocopy du service Azure Import/Export trop**bloc** objets BLOB ou **Page** objets BLOB. En revanche, vous ne pouvez qu’exporter les objets blob de **bloc**, de **page** ou **d’ajout** depuis le stockage Azure.

### <a name="job"></a>Travail
processus de hello toobegin d’importation tooor exportation à partir du stockage d’objets Blob, vous créez tout d’abord une tâche. Il peut s'agir d'une tâche d'importation ou d'une tâche d'exportation :

* Créer un travail d’importation lorsque vous souhaitez que les données tootransfer avoir local tooblobs dans votre compte de stockage Azure.
* Créer un travail d’exportation tootransfer les données actuellement stockées comme objets BLOB dans les lecteurs de toohard de compte de stockage qui sont livrés tooyou.s lorsque vous créez une tâche, vous pouvez vous en avertir hello importation/exportation de service que vous allez expédier un ou plus difficile lecteurs tooan Azure Centre de données.

* Dans le cas d’un travail d’importation, vous expédiez des disques durs contenant vos données.
* Dans le cas d’un travail d’exportation, vous expédiez des disques durs vides.
* Vous pouvez expédier les lecteurs de disque dur too10 par travail.

Vous pouvez créer une importation ou exportation de travail à l’aide de hello portail Azure ou hello [API REST d’importation/exportation de stockage Azure](/rest/api/storageimportexport).

### <a name="waimportexport-tool"></a>Outil WAImportExport
Hello première étape de création d’un **importer** travail est tooprepare vos lecteurs qui sont livrés à importer. tooprepare vos lecteurs, vous devez vous connecter serveur local de tooa et exécution hello outil WAImportExport sur le serveur local de hello. Cet outil WAImportExport facilite la copie de votre lecteur de toohello de données, le chiffrement des données hello sur lecteur hello avec BitLocker et générer des fichiers journaux d’unité hello.

fichiers de journal de Hello stockent des informations de base sur votre travail et d’un lecteur tel que le numéro de série de lecteur et du nom de compte de stockage. Ce fichier journal n’est pas stocké sur le lecteur de hello. Il est utilisé lors de la création de travaux d’importation. Une procédure détaillée de la création de ces tâches est fournie plus loin dans cet article.

outil de WAImportExport Hello est uniquement compatible avec le système d’exploitation de Windows 64 bits. Consultez hello [système d’exploitation](#operating-system) section pour des versions spécifiques du système d’exploitation pris en charge.

Télécharger la version la plus récente de hello hello [outil WAImportExport](http://download.microsoft.com/download/3/6/B/36BFF22A-91C3-4DFC-8717-7567D37D64C5/WAImportExportV2.zip). Pour plus d’informations sur l’utilisation de hello l’outil WAImportExport, consultez hello [Using hello outil WAImportExport](storage-import-export-tool-how-to.md).

>[!NOTE]
>**La Version précédente :** vous pouvez [télécharger WAImportExpot V1](http://download.microsoft.com/download/0/C/D/0CD6ABA7-024F-4202-91A0-CE2656DCE413/WaImportExportV1.zip) version de hello outil et consultez trop[guide d’utilisation de WAImportExpot V1](storage-import-export-tool-how-to-v1.md). Version WAImportExpot V1 de l’outil de hello assure une prise en charge de **préparation des disques lorsque les données sont écrites déjà préalable toohello disque**. Vous devez également toouse WAImportExpot V1 outil si seule clé hello disponible est la clé SAS.

>

### <a name="hard-disk-drives"></a>Disques durs
2,5 pouces uniquement SSD ou 2,5" ou 3,5" SATA II ou disque dur interne de III est pris en charge pour une utilisation avec le service d’importation/exportation de hello. Une même tâche d’importation/exportation peut avoir un maximum de 10 disques durs/SSD (quelle que soit la taille de chaque disque). Grand nombre de lecteurs peut être répartie sur plusieurs tâches et il n’existe aucune limite sur le nombre hello de travaux qui peuvent être créés. 

Pour les travaux d’importation, uniquement hello premier volume de données sur le lecteur de hello est traité. volume de données Hello doit être formaté avec NTFS.

> [!IMPORTANT]
> Les disques durs externes équipés d’un adaptateur USB intégré ne sont pas pris en charge par ce service. En outre, disque hello à l’intérieur de casse hello d’un disque dur externe ne peut pas être utilisée ; Veuillez ne pas envoyer de disques durs externes.
> 
> 

Vous trouverez ci-dessous qu'une liste des adaptateurs USB externes utilisée toocopy données toointernal HDD. Anker 68UPSATAA-02BU Anker 68UPSHHDS-BU Startech SATADOCK22UE Orico 6628SUS3-C-BK (6628 Series) Thermaltake BlacX Hot-Swap SATA External Hard Drive Docking Station (USB 2.0 & eSATA)

### <a name="encryption"></a>Chiffrement
données de Hello sur le lecteur de hello doivent être chiffrées à l’aide du chiffrement de lecteur BitLocker. Cette opération permet de protéger vos données pendant qu'elles sont en transit.

Pour les travaux d’importation, il existe le chiffrement de hello tooperform deux façons. Hello première avère toospecify hello lors de l’utilisation du fichier CSV de jeu de données lors de l’exécution d’outil de WAImportExport hello lors de la préparation du lecteur. Hello deuxième façon est le chiffrement BitLocker tooenable manuellement sur le lecteur de hello et spécifiez clé de chiffrement hello dans hello driveset volumes partagés de cluster lors de l’exécution de WAImportExport outil de ligne de commande lors de la préparation du lecteur.

Pour les travaux d’exportation, une fois que vos données sont copiées toohello lecteurs, service de hello chiffrer lecteur hello à l’aide de BitLocker avant de le livrer tooyou précédent. clé de chiffrement Hello sera fournie tooyou via hello portail Azure.  

### <a name="operating-system"></a>Système d’exploitation
Vous pouvez utiliser une des hello suivant 64 bits systèmes d’exploitation tooprepare hello disque dur à l’aide de hello outil WAImportExport avant de le livrer hello lecteur tooAzure :

Windows 7 Entreprise, Windows 7 Édition intégrale, Windows 8 Professionnel, Windows 8 Entreprise, Windows 8.1 Professionnel, Windows 8.1 Entreprise, Windows 10<sup>1</sup>, Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2. Tous ces systèmes d’exploitation prennent en charge le chiffrement de lecteur BitLocker.

### <a name="locations"></a>Emplacements
Hello service d’importation/exportation Azure prend en charge la copie tooand de données à partir de tous les comptes de stockage Azure publique. Vous pouvez expédier tooone de lecteurs de disque dur de hello emplacements suivants. Si votre compte de stockage se trouve dans un emplacement Azure public qui n’est pas spécifié ici, un emplacement d’expédition de remplacement sera fourni lors de la création à l’aide du travail hello hello portail Azure ou hello API REST importation/exportation.

Emplacements d’expédition pris en charge :

* Est des États-Unis
* Ouest des États-Unis
* Est des États-Unis 2
* Ouest des États-Unis 2
* Centre des États-Unis
* États-Unis - partie centrale septentrionale
* Centre-Sud des États-Unis
* Centre-Ouest des États-Unis
* Europe du Nord
* Europe de l'Ouest
* Est de l'Asie
* Asie du Sud-Est
* Est de l’Australie
* Sud-est de l’Australie
* Ouest du Japon
* Est du Japon
* Inde centrale
* Inde du Sud
* Inde occidentale
* Centre du Canada
* Est du Canada
* Sud du Brésil
* Centre de la Corée
* Gouvernement américain - Virginie
* US Gov Iowa
* Est des États-Unis – US DoD
* Centre des États-Unis – US DoD
* Chine orientale
* Chine du Nord
* Sud du Royaume-Uni

### <a name="shipping"></a>Expédition
**Expédition des lecteurs centre de données toohello :**

Lorsque vous créez un travail d’importation ou d’exportation, vous avez fourni qu'une adresse de livraison de l’un des hello pris en charge les emplacements tooship vos lecteurs. Hello copie l’adresse fournie dépend emplacement hello de votre compte de stockage, mais il peut être le même hello en tant que votre emplacement de compte de stockage.

Vous pouvez utiliser des opérateurs comme FedEx, DHL, onduleur ou hello US Postal Service tooship votre toohello lecteurs adresse de livraison.

**Expédition des lecteurs à partir du centre de données hello :**

Lorsque vous créez un travail d’importation ou d’exportation, vous devez fournir une adresse de retour pour Microsoft toouse lors de l’expédition des lecteurs hello sauvegarder une fois votre travail terminé. Vérifiez que vous fournissez une adresse de retournée valide tooavoid les retards de traitement.

Vous pouvez utiliser un opérateur de votre choix dans le disque dur hello ordre tooforward destinataire. opérateur de Hello doit avoir suivi approprié dans la chaîne de responsabilité toomaintain d’ordre. Vous devez également fournir un support FedEx ou DHL valid toobe numéro de compte utilisé par Microsoft pour l’expédition des lecteurs hello précédent. Un numéro de compte FedEx est requis pour l’expédition des lecteurs de hello des États-Unis et des emplacements en Europe. Un numéro de compte DHL est requis pour les retours de disque à partir d’Asie et d’Australie. Vous pouvez créer un compte de transporteur [FedEx](http://www.fedex.com/us/oadr/) (pour les États-Unis et l’Europe) ou [DHL](http://www.dhl.com/) (pour l’Asie et l’Australie) si vous n’en avez pas. Si vous avez déjà un compte de transporteur, vérifiez qu’il est valide.

De l’expédition de vos packages, vous devez suivre des termes du contrat de hello sur [termes du contrat de Service Microsoft Azure](https://azure.microsoft.com/support/legal/services-terms/).

> [!IMPORTANT]
> Veuillez noter que support physique hello qui vous pouvez être amené à toocross des frontières internationales. Vous êtes responsable de votre média physique et les données sont importées et/ou exportées conformément aux lois hello. Avant de livrer un support physique hello, vérifiez avec votre tooverify conseillers que votre support et les données peuvent être légalement centre de données expédiées toohello identifié. Cela aidera tooensure qu’elles atteignent Microsoft en temps voulu. Par exemple, n’importe quel package qui se croisent frontières internationales doit un toobe facture commerciale accompagnée d’un package hello (sauf si franchissement des frontières au sein de l’Union européenne). Vous pouvez imprimer un exemplaire remplie de facture commerciale de hello à partir du site Web de support. Exemples de factures commerciales : [facture commerciale DHL](http://invoice-template.com/wp-content/uploads/dhl-commercial-invoice-template.pdf) et [facture commerciale FedEx](http://images.fedex.com/downloads/shared/shipdocuments/blankforms/commercialinvoice.pdf). Assurez-vous que Microsoft n’a pas été indiqué en tant que l’exportateur hello.
> 
> 

## <a name="how-does-hello-azure-importexport-service-work"></a>Fonctionne de hello service Azure Import/Export
Vous pouvez transférer des données entre votre site local et le stockage d’objets blob Azure à l’aide du service d’importation/exportation Azure hello en créant des travaux et de livraison de centre de données Azure tooan de lecteurs de disque dur. Chaque disque dur expédié est associé à un seul travail. Chaque travail est associé à un seul compte de stockage. Hello de révision [section des conditions préalables](#pre-requisites) soigneusement toolearn sur les spécificités de hello de cette expédition, les types de disques, des emplacements et types d’objet blob service tel que pris en charge.

Dans cette section, nous décrivent un impliqués dans l’importation des étapes de hello de niveau élevé et travaux d’exportation. Plus loin dans hello [démarrage rapide de la section](#quick-start), nous fournissent des instructions pas à pas toocreate une importation et le travail d’exportation.

### <a name="inside-an-import-job"></a>Dans un travail d’importation
À un niveau élevé, une tâche d’importation implique hello comme suit :

* Déterminez hello toobe de données importé et hello du nombre de disques que nécessaires.
* Identifier l’emplacement d’objets blob de destination hello pour vos données dans le stockage d’objets Blob.
* Utilisez hello outil WAImportExport toocopy tooone de vos données ou de plusieurs lecteurs de disque dur et leur chiffrement avec BitLocker.
* Créer un travail d’importation dans votre compte de stockage cible à l’aide de hello portail Azure ou hello API REST importation/exportation. Si vous utilisez hello portail Azure, télécharger des fichiers de journal de lecteur hello.
* Fournir l’adresse de retour de hello et toobe de numéro de compte transporteur utilisé pour l’expédition tooyou arrière de lecteurs hello.
* Livraison toohello de lecteurs de disque dur hello adresse fournie lors de la création du travail de copie.
* Mettre à jour de la remise hello numéro dans les détails de la tâche hello importation de suivi et soumettre le travail d’importation hello.
* Les disques sont reçues et traitées au centre de données Azure hello.
* Lecteurs sont fournis à l’aide de votre transporteur compte toohello adresse de retour fourni dans le travail d’importation hello.
  
    ![Figure 1 : flux d’importation de travail](./media/storage-import-export-service/importjob.png)

### <a name="inside-an-export-job"></a>Dans un travail d’exportation
À un niveau élevé, un travail d’exportation implique hello comme suit :

* Déterminer hello données toobe exporté et hello du nombre de disques que nécessaires.
* Identifier les objets BLOB sources de hello ou des chemins d’accès du conteneur de vos données dans le stockage d’objets Blob.
* Créer un travail d’exportation de votre compte de stockage source à l’aide de hello portail Azure ou hello API REST importation/exportation.
* Spécifiez hello d’objets BLOB sources ou de tâche d’exportation de chemins d’accès du conteneur de vos données dans hello.
* Fournissez hello retour adresse et support de numéro de compte pour toobe de tooyou arrière de lecteurs hello.
* Livraison toohello de lecteurs de disque dur hello adresse fournie lors de la création du travail de copie.
* Mettre à jour de la remise hello numéro dans les détails de la tâche hello exportation de suivi et soumettre le travail d’exportation hello.
* Hello lecteurs sont reçus et traités au centre de données Azure hello.
* lecteurs de Hello sont chiffrés avec BitLocker. les clés de Hello sont disponibles via hello portail Azure.  
* Hello lecteurs sont fournis à l’aide de votre transporteur compte toohello adresse de retour fourni dans le travail d’importation hello.
  
    ![Figure 2 : flux d’exportation de travail](./media/storage-import-export-service/exportjob.png)

### <a name="viewing-your-job-and-drive-status"></a>Affichage de l’état de vos tâches et de vos disques
Vous pouvez suivre l’état de hello de votre importation ou exporter des travaux à partir de hello portail Azure. Cliquez sur hello **Import/Export** onglet. Une liste de vos projets s’affiche sur la page de hello.

![Afficher l’état des tâches](./media/storage-import-export-service/jobstate.png)

Vous verrez une Hello suivant des États de travail selon l’emplacement votre lecteur dans le processus de hello.

| Statut de tâche | Description |
|:--- |:--- |
| Creating | Après la création d’une tâche, son état est défini à tooCreating. Lors de la tâche de hello est en état de la création de hello, hello service d’importation/exportation suppose hello lecteurs n’ont pas été expédiés toohello Datacenter. Un travail peut rester en état de création de hello pour les semaines tootwo, après laquelle il est automatiquement supprimé par le service de hello. |
| Expédition | Après avoir expédié votre package, vous devez mettre à jour hello Bonjour portail Azure, les informations de suivi.  Cela transforme le travail de hello en « Shipping ». travail de Hello reste en état d’expédition hello pour les tootwo semaines. 
| Reçu | Une fois que tous les lecteurs ont été reçues au centre de données hello, état de la tâche hello définira toohello reçus. |
| Transferring | Une fois que le traitement a commencé au moins un lecteur, état de la tâche hello définira toohello transfert. Voir les États de lecteur hello section ci-dessous pour plus d’informations. |
| Packaging | Une fois que tous les lecteurs ont terminé le traitement, hello travail est placé dans un état d’emballage hello jusqu'à ce que hello lecteurs sont expédié tooyou précédent. |
| Completed | Une fois que tous les lecteurs ont été expédiés toohello précédent client, si hello est terminée sans erreur, puis les travaux hello seront définie toohello état terminé. travail de Hello sera automatiquement supprimé après 90 jours Bonjour état terminé. |
| Fermés | Une fois que tous les lecteurs ont été expédiés toohello précédent client, si des erreurs ont été lors du traitement de hello du travail de hello, puis les travaux hello seront définie toohello des état fermé. Hello travail sera automatiquement supprimé après 90 jours dans l’état fermé de hello. |

tableau Hello ci-dessous décrit le cycle de vie de hello d’un lecteur individuel lorsqu’il passe par un travail d’importation ou d’exportation. Hello état actuel de chaque lecteur d’un travail est maintenant visible à partir de hello portail Azure.
Hello tableau suivant décrit chaque état de chaque lecteur d’un travail peut passer.

| État du disque | Description |
|:--- |:--- |
| Spécifié | Pour un travail d’importation, lorsque le travail de hello est créé à partir de hello portail Azure, hello initiale pour un lecteur agit hello spécifié état. Pour un travail d’exportation, car aucun lecteur n’est spécifié lors de la tâche de hello est créée, hello initial du lecteur agit hello reçus état. |
| Reçu | lecteur de Hello basculer toohello reçu lors de l’opérateur du service d’importation/exportation hello a traité les lecteurs hello qui ont été reçus à partir de hello entreprise pour un travail d’importation de livraison. Pour un travail d’exportation, hello initial du lecteur agit hello reçus état. |
| NeverReceived (Jamais reçu) | lecteur de Hello déplacera toohello NeverReceived état lorsque le package hello pour un travail arrive mais hello ne contient pas le lecteur de hello. Un lecteur peut également déplacer dans cet état si elle a été deux semaines, car le service de hello reçu les informations d’expédition hello, mais le package de hello n’a pas encore arrivé au centre de données hello. |
| Transferring | Un lecteur passe toohello transfert état au commencement de service de hello tootransfer des données à partir de hello lecteur tooWindows le stockage Azure. |
| Completed | Un lecteur passe toohello état terminé lorsque hello service a correctement transféré toutes les données hello sans erreurs.
| CompletedMoreInfo (Terminé avec des informations) | Un lecteur entre toohello CompletedMoreInfo état lorsque hello service a rencontré des problèmes lors de la copie des données à partir d’ou toohello. informations de Hello peuvent inclure des erreurs, des avertissements ou messages d’information concernant le remplacement des objets BLOB.
| ShippedBack (Renvoyé) | lecteur de Hello déplacera toohello ShippedBack état lorsqu’il a été livré à partir de l’adresse de retour hello données centre toohello. |

Cette image à partir de hello portail Azure affiche l’état du lecteur d’un travail de l’exemple hello :

![Afficher l’état des disques](./media/storage-import-export-service/drivestate.png)

Hello tableau suivant décrit États d’échec lecteur hello et les actions de hello effectuées pour chaque état.

| État du disque | Événement | Résolution / Étape suivante |
|:--- |:--- |:--- |
| NeverReceived (Jamais reçu) | Un lecteur qui est marqué comme NeverReceived (car il n’a pas été reçu dans le cadre de l’expédition du travail hello) arrive dans une autre expédition. | équipe Hello déplacera hello lecteur toohello état Received. |
| N/A | Un lecteur qui ne fait pas partie d’un travail arrive au centre de données hello dans le cadre d’une autre tâche. | lecteur de Hello sera marquée comme un lecteur supplémentaire et est renvoyée toohello client lors de la tâche hello associé au package d’origine de hello est terminée. |

### <a name="time-tooprocess-job"></a>Tooprocess de travail du minuteur
quantité Hello de temps tooprocess un travail d’importation/exportation varie en fonction de différents facteurs, notamment lors de l’envoi de journaux, type de tâche, tapez et la taille de hello des données copiées, hello la taille des disques hello fourni. Hello service d’importation/exportation n’a pas d’un contrat SLA, mais après avoir reçu les disques hello service de hello s’efforce toocomplete hello copie too10 des 7 derniers jours. Vous pouvez utiliser progression du travail hello API REST tootrack hello plus en détail. Il existe un paramètre de pourcentage terminé dans hello opération de liste des travaux qui donne une indication de la progression de la copie. Atteindre toous si vous avez besoin d’un toocomplete estimation une tâche d’importation/exportation critiques de temps.

### <a name="pricing"></a>Tarification
**Frais de manipulation de disque**

Des frais de manipulation sont appliqués pour chaque disque traité dans le cadre de votre travail d’importation/exportation. Consultez les détails de hello sur hello [de la tarification Azure Import/Export](https://azure.microsoft.com/pricing/details/storage-import-export/).

**Frais d’expédition**

Lorsque vous expédiez tooAzure de disques, vous payez hello transporteur toohello de coût d’expédition. Microsoft retourne hello lecteurs tooyou hello frais d’expédition est facturé compte du transporteur toohello que vous avez fournies lors de la création du travail hello.

**Frais de transaction**

Aucuns frais de transaction ne s’appliquent pour l’importation de données dans Stockage Blob. les frais de sortie standard de Hello sont applicables lorsque les données sont exportées à partir du stockage d’objets blob. Pour plus d’informations sur les frais de transaction, consultez [Tarification - Transfert de données](https://azure.microsoft.com/pricing/details/data-transfers/)

## <a name="quick-start"></a>Démarrage rapide
Cette section vous explique en détail comment créer un travail d’importation et d’exportation. Vérifiez que vous remplissez toutes les Hello [préalables](#pre-requisites) avant de le déplacer vers l’avant.

> [!IMPORTANT]
> service de Hello prend en charge un seul compte de stockage standard par importation ou de travail d’exportation et ne prend pas en charge les comptes de stockage premium. 
> 
> 
## <a name="create-an-import-job"></a>Créer une tâche d’importation
Créer un tooyour de données d’importation travail toocopy compte de stockage Azure à partir de disques durs par un ou plusieurs disques contenant le centre de données spécifié de données toohello de livraison. travail d’importation Hello donne plus d’informations sur les lecteurs de disque dur, toobe des données copiées, compte de stockage cible et le service d’importation/exportation Azure toohello informations d’expédition. La création d’un travail d’importation comprend trois étapes. Tout d’abord, préparez vos lecteurs à l’aide d’outil de WAImportExport hello. En second lieu, soumettre un travail d’importation à l’aide de hello portail Azure. Troisièmement, expédier toohello de lecteurs hello adresse fourni pendant hello la création et la mise à jour de tâche dans les détails de votre travail, les informations d’expédition de livraison.   

### <a name="prepare-your-drives"></a>Préparation des lecteurs
Bonjour première étape lors de l’importation de données à l’aide du service d’importation/exportation Azure hello est tooprepare vos lecteurs à l’aide d’outil de WAImportExport hello. Suivez les étapes de hello ci-dessous tooprepare vos lecteurs.

1. Identifiez hello toobe de données importée. Cela peut être des répertoires et fichiers autonomes sur le serveur local de hello ou un partage réseau.  
2. Déterminer le nombre hello de disques que nécessaires en fonction de la taille totale des données de hello. Fournissez des disques durs SATA II et III hello requis nombre de SSD de 2,5 pouces 2,5" ou 3,5".
3. Identifier le compte de stockage cible hello, conteneur, répertoires virtuels et les objets BLOB.
4.  Déterminer les répertoires hello et/ou les fichiers autonomes qui seront copiés tooeach lecteur de disque dur.
5.  Créer des fichiers CSV pour le jeu de données et driveset hello.
    
    **Fichier CSV du jeu de données**
    
    Voici un exemple de fichier CSV de jeu de données :
    
    ```
    BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
    "F:\50M_original\100M_1.csv.txt","containername/100M_1.csv.txt",BlockBlob,rename,"None",None
    "F:\50M_original\","containername/",BlockBlob,rename,"None",None 
    ```
   
    Bonjour exemple ci-dessus, 100M_1.csv.txt sera copié toohello racine conteneur hello nommé « containername ». Si le nom de conteneur hello « containername » n’existe pas, il sera créé. Tous les fichiers et dossiers situés sous 50M_original sera toocontainername de copier de manière récursive. La structure des dossiers sera conservée.

    En savoir plus sur [préparation d’un fichier CSV hello dataset](storage-import-export-tool-preparing-hard-drives-import.md#prepare-the-dataset-csv-file).
    
    **N’oubliez pas**: par défaut, les données hello seront importées en tant qu’objets BLOB de blocs. Vous pouvez utiliser les données de valeur de champ tooimport hello BlobType comme un objet BLOB de Page. Par exemple, si vous importez des fichiers de disque dur virtuel qui seront montés comme des disques sur une machine virtuelle Azure, vous devez les importer en tant qu’objets blob de page.

    **Fichier CSV du jeu de disques**

    valeur Hello driveset hello indicateur est un fichier CSV qui contient la liste de hello de lettres de lecteurs de disques toowhich hello sont mappés par ordre de hello outil toocorrectly liste de choix hello de toobe disques préparé. 

    Voici un exemple hello du fichier CSV de driveset :
    
    ```
    DriveLetter,FormatOption,SilentOrPromptOnFormat,Encryption,ExistingBitLockerKey
    G,AlreadyFormatted,SilentMode,AlreadyEncrypted,060456-014509-132033-080300-252615-584177-672089-411631 |
    H,Format,SilentMode,Encrypt,
    ```

    Bonjour exemple ci-dessus, il est supposé que deux disques sont attachés et les volumes NTFS de base avec la lettre de volume G:\ et H:\ ont été créés. outil de Hello mettre en forme et chiffrer disque hello qui héberge H:\ et ne sera pas mettre en forme ou chiffrer disque hello volume G:\ d’hébergement.

    En savoir plus sur [préparation d’un fichier CSV hello driveset](storage-import-export-tool-preparing-hard-drives-import.md#prepare-initialdriveset-or-additionaldriveset-csv-file).

6.  Hello d’utilisation [outil WAImportExport](http://download.microsoft.com/download/3/6/B/36BFF22A-91C3-4DFC-8717-7567D37D64C5/WAImportExport.zip) toocopy tooone de vos données ou de plusieurs disques durs.
7.  Vous pouvez spécifier « Encrypt » sur le champ de chiffrement dans tooenable le chiffrement de BitLocker sur un lecteur de disque dur hello drivset CSV. Vous pouvez également vous pourriez également activer le chiffrement BitLocker manuellement sur le lecteur de disque dur hello et spécifier « AlreadyEncrypted » et fournir la clé hello dans hello driveset volumes partagés de cluster lors de l’exécution d’outil de hello.

8. Ne modifiez pas les données hello sur les lecteurs de disque dur hello ou un fichier de journal hello après avoir effectué la préparation du disque.

> [!IMPORTANT]
> Un fichier journal est créé pour chaque disque dur que vous préparez. Lorsque vous créez un travail d’importation hello à l’aide de hello portail Azure, vous devez télécharger tous les fichiers de journal hello de lecteurs hello qui font partie de cette tâche d’importation. Les disques sans fichier journal ne sont pas traités.
> 
>

Ci-dessous sont commandes hello et des exemples pour la préparation de lecteur de disque dur hello à l’aide d’outil WAImportExport.

L’outil WAImportExport commande PrepImport pour hello tout d’abord copier les répertoires toocopy de session et/ou de fichiers avec une nouvelle session de copie :

```
WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> [/logdir:<LogDirectory>] [/sk:<StorageAccountKey>] [/silentmode] [/InitialDriveSet:<driveset.csv>] DataSet:<dataset.csv>
```

**Exemple d’importation 1**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#1  /sk:************* /InitialDriveSet:driveset-1.csv /DataSet:dataset-1.csv /logdir:F:\logs
```

Dans l’ordre trop**ajouter des disques**, un qui peut créer un nouveau fichier driveset et exécutez la commande hello comme indiqué ci-dessous. Pour la copie suivante sessions toohello différents lecteurs de disque à celle spécifiée dans le fichier .csv de InitialDriveset, spécifiez un fichier CSV driveset et fournit en tant que valeur toohello paramètre « AdditionalDriveSet ». Hello d’utilisation **même fichier journal** nommer et de fournir un **nouvel ID de session**. format Hello du fichier AdditionalDriveset CSV est identique au format de InitialDriveSet.

```
WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> /AdditionalDriveSet:<driveset.csv>
```

**Exemple d’importation 2**
```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#3  /AdditionalDriveSet:driveset-2.csv
```

Dans l’ordre tooadd des données supplémentaires toohello driveset même, l’outil WAImportExport PrepImport commande peut être appelée pour la copie suivante sessions toocopy supplémentaires/répertoire des fichiers : de copie suivantes sessions toohello mêmes disques durs spécifié dans InitialDriveset .csv de fichiers, spécifiez hello **même fichier journal** nommer et de fournir un **nouvel ID de session**; il n’existe aucune clé de compte de stockage nécessaire tooprovide hello.

```
WAImportExport PrepImport /j:<JournalFile> /id:<SessionId> /j:<JournalFile> /id:<SessionId> [/logdir:<LogDirectory>] DataSet:<dataset.csv>
```

**Exemple d’importation 3**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2  /DataSet:dataset-2.csv
```

Afficher plus de détails sur l’utilisation de l’outil WAImportExport hello du [préparation des disques durs pour l’importation](storage-import-export-tool-preparing-hard-drives-import.md).

En outre, consultez toohello [exemple de flux de travail tooprepare les disques durs pour un travail d’importation](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow.md) pour plus d’instructions pas à pas.  

### <a name="create-hello-import-job"></a>Créer le travail d’importation hello
1. Une fois que vous avez préparé votre disque, accédez de compte de stockage tooyour Bonjour portail Azure et afficher hello du tableau de bord. Sous **Aperçu rapide**, cliquez sur **Créer une tâche d'importation**. Passez en revue les étapes hello et sélectionnez hello case à cocher tooindicate que vous avez préparé votre disque et que vous disposez de fichier journal d’unité hello disponible.
2. À l’étape 1, fournissent des informations de contact pour hello responsable de cette tâche d’importation et une adresse de retournée valide. Si vous souhaitez toosave les données de journal détaillé pour le travail d’importation hello, vérifiez les option hello trop**enregistrer le journal détaillé hello dans mon conteneur d’objets blob 'waimportexport'**.
3. À l’étape 2, téléchargez les fichiers journaux hello lecteur que vous avez obtenue au cours de l’étape de préparation du lecteur hello. Vous devez un fichier de tooupload pour chaque lecteur que vous avez préparé.
   
   ![Créer une tâche d'importation - Étape 3](./media/storage-import-export-service/import-job-03.png)
4. À l’étape 3, entrez un nom descriptif pour le travail d’importation hello. Notez que nom hello que vous entrez peut contenir uniquement des lettres minuscules, des chiffres, des traits d’union et des traits de soulignement, doit commencer par une lettre et ne peut pas contenir des espaces. Vous allez utiliser le nom hello choisissez tootrack vos travaux lorsqu’ils sont en cours d’exécution et une fois qu’elles sont terminées.
   
   Ensuite, sélectionnez votre région de centre de données à partir de la liste de hello. région de centre de données Hello indiquera hello Datacenter et adresse toowhich vous devez expédier votre package. Consultez le Forum aux questions de hello ci-dessous pour plus d’informations.
5. À l’étape 4, sélectionnez votre transporteur pour le retour à partir de la liste de hello et entrez votre numéro de compte du transporteur. Microsoft utilisera ce compte tooship hello lecteurs arrière tooyou une fois votre travail d’importation est terminée.
   
   Si vous avez le numéro de suivi, sélectionnez votre transporteur à partir de la liste de hello et entrez votre numéro de suivi.
   
   Si vous n’avez pas de suivi nombre encore, choisissez **je fournirai mes informations d’expédition pour ce travail d’importation après envoi de mon colis**, puis terminez le processus d’importation hello.
6. retour de votre numéro de suivi une fois que vous avez envoyé votre package, tooenter toohello **Import/Export** page de votre compte de stockage dans hello portail Azure, sélectionnez votre projet à partir de la liste de hello et choisissez **informations d’expédition**. Naviguer dans l’Assistant de hello et entrez votre numéro de suivi à l’étape 2.
   
    Si hello numéro de suivi n’est pas mis à jour dans les 2 semaines de la création du travail de hello, le travail de hello va expirer.
   
    Si le travail de hello est en état de création, expédition ou transfert hello, vous pouvez également mettre à jour votre numéro de compte du transporteur à l’étape 2 de l’Assistant de hello. Une fois le travail de hello est en état d’emballage hello, vous ne peut pas mettre à jour votre compte du transporteur pour ce travail.
7. Vous pouvez suivre votre progression du travail sur le tableau de bord de portail hello. Voir la signification de chaque état de la tâche dans la section précédente de hello par [affichage de l’état de votre travail](#viewing-your-job-status).

## <a name="create-an-export-job"></a>Création d’une tâche d’exportation
Créer un hello toonotify du travail exportation service d’importation/exportation que vous allez expédier un ou du centre de données de toohello de disques vides plus afin que les données peuvent être exportées à partir de vos lecteurs de toohello de compte de stockage et les lecteurs hello puis expédié tooyou.

### <a name="prepare-your-drives"></a>Préparation des lecteurs
Les vérifications préalables suivantes sont recommandées pour préparer vos disques en vue d’un travail d’exportation :

1. Vérifiez le nombre hello de disques requis à l’aide de la commande PreviewExport de l’outil WAImportExport de hello. Pour plus d’informations, consultez [Aperçu de l’utilisation des lecteurs pour un travail d’exportation](https://msdn.microsoft.com/library/azure/dn722414.aspx). Il vous permet d’afficher un aperçu de l’utilisation des lecteurs pour les objets BLOB de hello sélectionné, en fonction de taille hello hello lecteurs que vous vous apprêtez toouse.
2. Vérifiez que vous pouvez en lecture/écriture toohello disque dur qui est livré pour le travail d’exportation hello.

### <a name="create-hello-export-job"></a>Créer le travail d’exportation hello
1. toocreate un travail d’exportation, accédez de compte de stockage tooyour Bonjour portail Azure et afficher hello du tableau de bord. Sous **aperçu rapide**, cliquez sur **créer un travail d’exportation** et suivez les étapes hello Assistant.
2. À l’étape 2, fournissent des informations de contact pour hello responsable de ce travail d’exportation. Si vous souhaitez toosave les données de journal détaillé pour le travail d’exportation hello, vérifiez les option hello trop**enregistrer le journal détaillé hello dans mon conteneur d’objets blob 'waimportexport'**.
3. À l’étape 3, spécifiez l’objets blob de lecteur de données tooexport à partir de votre espace de tooyour de compte de stockage ou des lecteurs. Vous pouvez choisir tooexport toutes les données blob dans le compte de stockage hello, ou vous pouvez spécifier laquelle des objets BLOB ou ensembles d’objets BLOB tooexport.
   
   toospecify tooexport un objet blob, utilisez hello **égal à** sélecteur et spécifiez l’objet blob de toohello de chemin d’accès relatif hello, commençant par le nom du conteneur hello. Utilisez *$root* conteneur racine de hello toospecify.
   
   toospecify tous les objets BLOB commençant par un préfixe, utilisez hello **commence par** sélecteur et spécifiez le préfixe hello, commençant par une barre oblique « / ». préfixe de Hello peut-être hello préfixe du nom du conteneur hello, nom du conteneur terminée hello ou nom de conteneur complet hello suivi par nom d’objet blob hello préfixe hello.
   
   Hello tableau suivant présente des exemples de chemins d’accès de l’objet blob valide :
   
   | Sélecteur | Chemin d'accès d'objet blob | Description |
   | --- | --- | --- |
   | Starts With |/ |Exporte tous les objets BLOB dans le compte de stockage hello |
   | Starts With |/$root/ |Exporte tous les objets BLOB dans le conteneur racine de hello |
   | Starts With |/book |Exporte tous les objets blob présents dans un conteneur commençant par le préfixe **book** |
   | Starts With |/music/ |Exporte tous les objets blob présents dans le conteneur **music** |
   | Starts With |/music/love |Exporte tous les objets blob présents dans le conteneur **music** qui commencent par le préfixe **love**. |
   | Trop d’égal|$root/logo.bmp |Objet blob d’exportations **logo.bmp** dans le conteneur racine de hello |
   | Trop d’égal|videos/story.mp4 |Exporte l’objet blob **story.mp4** présent dans le conteneur **videos**. |
   
   Vous devez fournir chemins hello dans des formats valides tooavoid erreurs au cours du traitement, comme indiqué dans cette capture d’écran.
   
   ![Créer une tâche d'exportation - Étape 3](./media/storage-import-export-service/export-job-03.png)
4. À l’étape 4, entrez un nom descriptif pour le travail d’exportation hello. nom que vous entrez hello peut contenir uniquement des lettres minuscules, des chiffres, des traits d’union et des traits de soulignement, doit commencer par une lettre et ne peut pas contenir des espaces.
   
   région de centre de données Hello indique toowhich de centre de données hello vous devez expédier votre package. Consultez le Forum aux questions de hello ci-dessous pour plus d’informations.
5. À l’étape 5, sélectionnez votre transporteur pour le retour à partir de la liste de hello et entrez votre numéro de compte du transporteur. Microsoft utilisera cette tooship compte vos lecteurs sauvegarder tooyou une fois votre travail d’exportation est terminée.
   
   Si vous avez le numéro de suivi, sélectionnez votre transporteur à partir de la liste de hello et entrez votre numéro de suivi.
   
   Si vous n’avez pas de suivi nombre encore, choisissez **je fournirai mes informations d’expédition pour ce travail d’exportation après envoi de mon colis**, puis terminez le processus d’exportation hello.
6. retour de votre numéro de suivi une fois que vous avez envoyé votre package, tooenter toohello **Import/Export** page de votre compte de stockage dans hello portail Azure, sélectionnez votre projet à partir de la liste de hello et choisissez **informations d’expédition**. Naviguer dans l’Assistant de hello et entrez votre numéro de suivi à l’étape 2.
   
    Si hello numéro de suivi n’est pas mis à jour dans les 2 semaines de la création du travail de hello, le travail de hello va expirer.
   
    Si le travail de hello est en état de création, expédition ou transfert hello, vous pouvez également mettre à jour votre numéro de compte du transporteur à l’étape 2 de l’Assistant de hello. Une fois le travail de hello est en état d’emballage hello, vous ne peut pas mettre à jour votre compte du transporteur pour ce travail.
   
   > [!NOTE]
   > Si toobe d’objets blob hello exportée est en cours d’utilisation au moment de hello de copie toohard lecteur, service Azure Import/Export prendra un instantané de l’instantané du hello hello blob et de copie.
   > 
   > 
7. Vous pouvez suivre votre progression du travail sur le tableau de bord hello Bonjour portail Azure. Voir la signification de chaque état de la tâche dans la section précédente de hello sur « Affichage de l’état de votre travail ».
8. Après avoir reçu les lecteurs hello avec vos données exportées, vous pouvez afficher et copier les clés BitLocker de hello générés par le service hello pour votre lecteur. Accédez de compte de stockage tooyour Bonjour portail Azure et sur hello importation/exportation. Sélectionnez votre travail d’exportation à partir de la liste de hello et cliquez sur le bouton Afficher les clés de hello. les clés BitLocker Hello s’affichent comme illustré ci-dessous :
   
   ![Afficher les clés BitLocker pour une tâche d'exportation](./media/storage-import-export-service/export-job-bitlocker-keys.png)

Passez en revue Forum aux questions hello ci-dessous comme il couvre les questions courantes hello rencontrés lors de l’utilisation de ce service.

## <a name="frequently-asked-questions"></a>Forum Aux Questions

**Puis-je copier stockage Azure Files à l’aide du service d’importation/exportation Azure hello ?**

Non, hello service Azure Import/Export uniquement prend en charge les objets BLOB de blocs et objets BLOB de pages. Aucun autre type de stockage, y compris Stockage Fichier Azure, Stockage Table et Stockage File d’attente n’est pris en charge.

**Service d’importation/exportation Azure hello n’est disponible pour les abonnements de fournisseur de services cryptographiques ?**

Le service Azure Import/Export prend en charge les abonnements de fournisseur de services de chiffrement.

**Puis-je ignorer la fonctionnalité étape de préparation du lecteur hello pour un travail d’importation ou puis-je préparer un lecteur sans copier ?**

N’importe quel lecteur que vous souhaitez tooship pour l’importation de données doit être préparé à l’aide d’outil de Azure WAImportExport hello. Vous devez utiliser le lecteur de toohello hello WAImportExport outil toocopy données.

**Dois-je tooperform une préparation du disque lors de la création d’un travail d’exportation ?**

Non, mais certaines vérifications préalables sont recommandées. Vérifiez le nombre hello de disques requis à l’aide de la commande PreviewExport de l’outil WAImportExport de hello. Pour plus d’informations, consultez [Aperçu de l’utilisation des lecteurs pour un travail d’exportation](https://msdn.microsoft.com/library/azure/dn722414.aspx). Il vous permet d’afficher un aperçu de l’utilisation des lecteurs pour les objets BLOB de hello sélectionné, en fonction de taille hello hello lecteurs que vous vous apprêtez toouse. Également vérifier que vous pouvez lire et du disque dur écriture toohello livrés pour hello travail d’exportation.

**Que se passe-t-il si j’envoie par inadvertance un disque dur qui n’est pas conforme toohello requise prise en charge ?**

Centre de données Azure Hello retournera lecteur hello qui n’est pas conforme tooyou d’exigences toohello pris en charge. Si seuls certains lecteurs hello dans le package de hello requise hello prise en charge, ces lecteurs seront traités, et les lecteurs hello qui ne répondent pas aux exigences de hello seront affichera tooyou.

**Puis-je annuler une tâche ?**

Vous pouvez annuler une tâche dont le statut est Creating ou Shipping.

**Combien puis-je afficher état hello de travaux terminés Bonjour portail Azure ?**

Vous pouvez afficher l’état hello pour les tâches terminées pour too90 jours. Au-delà de ce délai, les travaux terminés sont supprimés.

**Si je tooimport ou les exporter de plus de 10 lecteurs, que dois-je faire ?**

Une importation ou de la tâche d’exportation peut faire référence uniquement 10 lecteurs dans une seule tâche pour le service d’importation/exportation hello. Si vous souhaitez tooship plus de 10 disques, vous pouvez créer plusieurs travaux. Les lecteurs qui sont associés à hello même travail doive être fourni ensemble dans hello même package.
Microsoft propose des conseils et une assistance quand la capacité de données s’étend sur plusieurs travaux d’importation de disques. Pour plus d’informations, contactez bulkimport@microsoft.com.

**Hello service format hello lecteurs avant de les retourner ?**

Non. Tous les disques sont chiffrés avec BitLocker.

**Est-il possible d’acheter des lecteurs auprès de Microsoft pour des tâches d’importation/exportation ?**

Non. Vous devez tooship vos propres lecteurs à la fois pour importer et exporter des travaux.

** Comment accéder aux données importées par ce service**

données de Hello sous votre compte de stockage Azure sont accessibles via hello portail Azure ou à l’aide d’un outil autonome appelé Explorateur de stockage. https://docs.Microsoft.com/fr-fr/azure/vs-azure-tools-storage-manage-with-storage-explorer 

**Après la tâche d’importation hello, ce que mon données ressemblera hello compte de stockage ? Mon arborescence sera-t-elle préservée ?**

Lorsque vous préparez un disque dur pour un travail d’importation, destination de hello est spécifiée par hello DstBlobPathOrPrefix champ dataset CSV. Il s’agit de conteneur de destination hello dans toowhich de compte de stockage hello du disque dur de hello, les données sont copiées. Dans ce conteneur de destination, les répertoires virtuels sont créés pour les dossiers de disque dur de hello et des objets BLOB est créés pour les fichiers. 

**Si le lecteur de hello a des fichiers qui existent déjà dans mon compte de stockage, service de hello remplacer des objets BLOB existants dans mon compte de stockage ?**

Lorsque vous préparez le lecteur de hello, vous pouvez spécifier si les fichiers de destination hello doivent être remplacés ou ignorées à l’aide du champ de hello dans le fichier CSV de dataset appelé Disposition : < renommer | non-remplacer | remplacer >. Par défaut, hello service sera renommer des fichiers de nouveau hello plutôt que remplacer les objets BLOB existants.

**Outil de WAImportExport hello n’est compatible avec les systèmes d’exploitation 32 bits ?**
Non. outil de WAImportExport Hello est uniquement compatible avec les systèmes d’exploitation Windows 64 bits. Veuillez consulter la section des systèmes d’exploitation toohello Bonjour [préalables](#pre-requisites) pour une liste complète des versions de système d’exploitation pris en charge.

**Dois-je inclure autre chose qu’un lecteur de disque dur hello dans mon package ?**

Incluez uniquement vos disques durs. N’incluez pas d’accessoires tels que des câbles d’alimentation ou USB.

**Dois-je tooship mes disques à l’aide de FedEx ou DHL ?**

Vous pouvez expédier le centre de données toohello de lecteurs à l’aide de n’importe quel opérateur connu comme FedEx, DHL, UPS ou US Postal Service. Toutefois, pour l’envoi de journaux hello lecteurs arrière tooyou hello centre de données, vous devez fournir un numéro de compte FedEx Bonjour des États-Unis et l’Union européenne, ou un numéro de compte DHL hello Asie et régions de l’Australie.

**Existe-t-il des restrictions à l’expédition de mon disque dur hors des frontières ?**

Veuillez noter que support physique hello qui vous pouvez être amené à toocross des frontières internationales. Vous êtes responsable de votre média physique et les données sont importées et/ou exportées conformément aux lois hello. Avant de livrer un support physique hello, vérifiez avec votre tooverify conseillers que votre support et les données peuvent être légalement centre de données expédiées toohello identifié. Cela aidera tooensure qu’elles atteignent Microsoft en temps voulu.

**Lorsque vous créez une tâche, hello adresse de livraison est un emplacement différent de mon emplacement du compte de stockage. Que dois-je faire ?**

Certains emplacements de compte de stockage sont mappé tooalternate emplacements d’envoi. Précédemment emplacements d’expédition disponible peuvent également être temporairement mappé tooalternate emplacements. Vérifiez toujours hello adresse fournie lors de la création du travail avant d’expédier vos lecteurs de livraison.

**Lors de l’expédition de mon lecteur, opérateur de hello demande hello données center contact adresse et numéro de téléphone. Que dois-je indiquer ?**

Hello numéro de téléphone et de contrôleur de domaine adresse est fournie dans le cadre de la création du travail.

**Puis-je utiliser les boîtes aux lettres de service toocopy PST hello Azure Import/Export et tooO365 de données SharePoint ?**

Reportez-vous trop[fichiers PST d’importation ou tooOffice de données SharePoint 365](https://technet.microsoft.com/library/ms.o365.cc.ingestionhelp.aspx).

**Puis-je utiliser toocopy de service d’importation/exportation Azure hello de mon toohello hors connexion de sauvegardes Service Azure Backup ?**

Reportez-vous trop[flux de travail de sauvegarde en mode hors connexion dans Azure Backup](../backup/backup-azure-backup-import-export.md).

**Nouveautés de numéros de hello maximale de disque dur pour dans une livraison ?**

Un nombre quelconque de lecteurs de disque dur peut être en une expédition et si les disques hello appartiennent toomultiple travaux il est recommandé de trop un) ont des disques hello étiquetés avec des noms de la tâche correspondante hello. b) travaux de hello mise à jour avec un numéro de suivi portant la valeur -1, etc. de-2.
  
**Qu’est hello objet Blob de blocs maximale et taille d’objet Blob de Page prises en charge par le disque Import/Export ?**

La taille maximale des objets blob de blocs est d’environ 4,768 To ou 5 000 000 Mo.
La taille maximale des objets blob de pages est de 1 To.

**L’importation/exportation de disque prennent-elles en charge le chiffrement AES 256 ?**

Service d’importation/exportation Azure par défaut chiffre avec le chiffrement AES 128 bitlocker, mais cela peut être accrue tooAES 256 en chiffrant manuellement avec bitlocker avant que les données sont copiées. 

Si vous utilisez [WAImportExpot V1](http://download.microsoft.com/download/0/C/D/0CD6ABA7-024F-4202-91A0-CE2656DCE413/WaImportExportV1.zip), voici un exemple de commande.
```
WAImportExport PrepImport /sk:<StorageAccountKey> /csas:<ContainerSas> /t: <TargetDriveLetter> [/format] [/silentmode] [/encrypt] [/bk:<BitLockerKey>] [/logdir:<LogDirectory>] /j:<JournalFile> /id:<SessionId> /srcdir:<SourceDirectory> /dstdir:<DestinationBlobVirtualDirectory> [/Disposition:<Disposition>] [/BlobType:<BlockBlob|PageBlob>] [/PropertyFile:<PropertyFile>] [/MetadataFile:<MetadataFile>] 
```
Si vous utilisez [outil WAImportExport](http://download.microsoft.com/download/3/6/B/36BFF22A-91C3-4DFC-8717-7567D37D64C5/WAImportExport.zip) spécifier « AlreadyEncrypted » et fournir la clé hello dans hello driveset CSV.
```
DriveLetter,FormatOption,SilentOrPromptOnFormat,Encryption,ExistingBitLockerKey
G,AlreadyFormatted,SilentMode,AlreadyEncrypted,060456-014509-132033-080300-252615-584177-672089-411631 |
```
## <a name="next-steps"></a>Étapes suivantes

* [Configuration de l’outil WAImportExport de hello](storage-import-export-tool-how-to.md)
* [Transfert de données avec hello utilitaire de ligne de commande AzCopy](storage-use-azcopy.md)
* [Exemple d’API REST Azure Import Export](https://azure.microsoft.com/documentation/samples/storage-dotnet-import-export-job-management/)

