---
title: "notes d’aaaRelease pour la passerelle de gestion des données | Documents Microsoft"
description: "Notes de version pour la passerelle de gestion des données"
services: data-factory
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: 14762e82-76d9-41c4-ba9f-14a54da29c36
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: abnarain
published: True
ms.openlocfilehash: 3165d7537410a0531e0bb7f7fe584767f9155574
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="release-notes-for-data-management-gateway"></a>Notes de version pour la passerelle de gestion des données
Un des défis hello pour l’intégration de données moderne est tooand de données toomove de local toocloud. Fabrique de données permet l’intégration avec la passerelle de gestion des données, qui est un agent que vous pouvez installer le déplacement des données sur site tooenable hybride.

Consultez hello suivant des articles pour plus d’informations sur la passerelle de gestion des données et comment toouse il :

*  [Passerelle de gestion de données](data-factory-data-management-gateway.md)
*  [Déplacement de données entre des emplacements locaux et le cloud à l'aide d’Azure Data Factory](data-factory-move-data-between-onprem-and-cloud.md)


## <a name="current-version-21063477"></a>VERSION ACTUELLE (2.10.6347.7)

### <a name="enhancements-"></a>Améliorations
- Vous pouvez ajouter le bus des services DNS entrées toowhitelist plutôt que de création de listes autorisées toutes les adresses IP Azure à partir de votre pare-feu (le cas échéant). Vous pouvez trouver l’entrée DNS concernée sur le portail Azure (Data Factory -> Créer et déployer > Passerelles > ServiceUrls (dans JSON))
- Le connecteur HDFS prend désormais en charge le certificat public auto-signé en vous permettant d’ignorer la validation SSL.
- Résolu : Problème avec la passerelle en mode hors connexion pendant la mise à jour (en raison d’inclinaison de tooclock)



## <a name="earlier-versions"></a>Versions antérieures

## <a name="2963132"></a>2.9.6313.2
### <a name="enhancements-"></a>Améliorations
-   Vous pouvez ajouter toowhitelist des entrées DNS Service Bus au lieu des liste approuvées toutes les adresses IP Azure à partir de votre pare-feu (le cas échéant). Plus de détails ici.
-   Vous pouvez maintenant copier les données vers/à partir d’un objet blob de bloc unique des too4.75 To, ce qui est la taille de hello maximale prise en charge de l’objet blob de blocs. (la limite antérieure était de 195 Go).
-   Résolu : problème de mémoire insuffisante lors de la décompression de plusieurs petits fichiers pendant l’activité de copie.
-   Problème résolu : Index hors problème plage lors de la copie à partir de la base de données de Document tooan local SQL Server avec la fonctionnalité d’idempotence.
-   Résolu : le script de nettoyage SQL ne fonctionne pas avec la version locale de SQL Server à partir de l’Assistant de copie.
-   Problème résolu : Nom de la colonne avec l’espace à la fin de hello ne fonctionne pas dans l’activité de copie.

## <a name="28662833"></a>2.8.66283.3
### <a name="enhancements-"></a>Améliorations
- Résolu : problème d’informations d’identification manquantes au redémarrage de l’ordinateur de la passerelle.
- Résolu : problème lié à l’inscription lors de la restauration de la passerelle à l’aide d’un fichier de sauvegarde.


## <a name="2762401"></a>2.7.6240.1
### <a name="enhancements-"></a>Améliorations
- Résolu : lecture incorrecte d’une valeur null décimale à partir d’Oracle comme source.

## <a name="2661922"></a>2.6.6192.2
### <a name="whats-new"></a>Nouveautés
- Les clients peuvent faire part de leurs commentaires sur l’expérience d’inscription à la passerelle.
- Prise en charge d’un nouveau format de compression : ZIP (Deflate)

### <a name="enhancements-"></a>Améliorations
- Amélioration des performances pour le récepteur d’Oracle, source HDFS.
- Correctif de bogue pour la mise à jour automatique de la passerelle, capacité de traitement parallèle de la passerelle.


## <a name="2561641"></a>2.5.6164.1
### <a name="enhancements"></a>Améliorations
- Améliorée et plus robuste passerelle inscription expérience-maintenant vous pouvez suivre l’état de la progression pendant le processus de l’inscription hello passerelle, ce qui rend l’inscription de hello expérience plus réactive.
- Amélioration de la passerelle restaurer processus - vous pouvez toujours récupérer passerelle même si vous n’avez pas de fichier de sauvegarde de passerelle hello avec cette mise à jour. Cette situation exigerait informations d’identification du Service lié tooreset dans le portail.
- Résolution de bogue.

## <a name="2461511"></a>2.4.6151.1

### <a name="whats-new"></a>Nouveautés

- Vous pouvez désormais stocker localement les informations d’identification de la source de données. informations d’identification de Hello sont chiffrées. informations d’identification de source de données Hello peuvent être récupérées et restaurées à l’aide du fichier de sauvegarde hello qui peut être exportée à partir de hello existant de passerelle, locaux.

### <a name="enhancements-"></a>Améliorations

- Expérience d’inscription de la passerelle améliorée et plus robuste.
- Prend en charge la détection automatique de la configuration de l’élément QuoteChar pour le format de texte dans l’Assistant copie d’et améliorer hello format global de précision de la détection.

## <a name="2361002"></a>2.3.6100.2

- Prise en charge de la détection automatique firstRowAsHeader et SkipLineCount dans l’Assistant de copie pour les fichiers texte dans le système de fichiers local et HDFS.
- Améliorer la stabilité hello de connexion réseau entre la passerelle et le Service Bus
- Résolution de quelques bogues


## <a name="2260721"></a>2.2.6072.1

*  Prend en charge la définition du proxy HTTP pour l’utilisation de passerelle hello hello Gestionnaire de Configuration de passerelle. Si configurés, Azure Blob, Azure Table, Azure Data Lake et Document DB sont accessibles via le proxy HTTP.
*  En-tête prend en charge la gestion de TextFormat lors de la copie des données à partir de / tooAzure Blob, Azure Data Lake Store, système de fichiers local et HDFS local.
*  Prend en charge la copie de données d’ajouter un objet Blob et l’objet Blob de pages, ainsi que de hello déjà pris en charge l’objet Blob de blocs.
*  Introduit un nouvel état de la passerelle **en ligne (limité)**, ce qui signifie que hello principale fonctionnalité de passerelle de hello fonctionne à l’exception de prise en charge de hello opération interactive de l’Assistant copie de.
*  Améliore la robustesse de hello d’enregistrement de la passerelle à l’aide de la clé d’inscription.

## <a name="216040"></a>2.1.6040.

*  Pilote DB2 est inclus dans le package d’installation hello passerelle maintenant. Vous n’avez pas besoin de tooinstall il séparément.
*  Pilote DB2 prend désormais en charge z/OS et DB2 pour i (AS / 400), ainsi que les plateformes hello déjà pris en charge (Windows, Unix et Linux).
*  Prend en charge l’utilisation d’Azure Cosmos DB comme source ou destination des banques de données locales
*  Prend en charge la copie de stockage des données à partir de/toocold/attentivement les objets blob, ainsi que de hello déjà pris en charge le compte de stockage à usage général.
*  Vous permet de tooconnect tooon local SQL Server via une passerelle avec des droits de connexion à distance.  

## <a name="2060131"></a>2.0.6013.1

*  Vous pouvez sélectionner hello toobe de langue/culture utilisée par une passerelle de pendant l’installation manuelle.

*  Lors de la passerelle ne fonctionne pas comme prévu, vous pouvez choisir les journaux de la passerelle toosend dernière sept jours tooMicrosoft toofacilitate résolution des problèmes d’émission de hello. Si la passerelle n’est pas connecté toohello service de cloud, vous pouvez choisir toosave et archivez les journaux de la passerelle.  

*  Améliorations de l’interface utilisateur du gestionnaire de configuration de la passerelle :

    *  Afficher l’état de la passerelle plus hello accueil onglet.

    *  Commandes réorganisées et simplifiées.

    *  Vous pouvez copier des données à partir d’un stockage à l’aide de hello [outil Aperçu de la copie sans code](data-factory-copy-data-wizard-tutorial.md). Pour plus d’informations sur cette fonctionnalité, consultez [Copie intermédiaire](data-factory-copy-activity-performance.md#staged-copy) .
*  Vous pouvez utiliser les données de tooingress de passerelle de gestion des données directement à partir d’une base de données SQL Server locale dans Azure Machine Learning.

*  Amélioration des performances

    * Amélioration des performances d’affichage du schéma/de l’aperçu par rapport à SQL Server dans l’outil de prévisualisation de copie sans code.

## <a name="11259531"></a>1.12.5953.1

*  Résolution des bogues

## <a name="11159181"></a>1.11.5918.1

*  Taille maximale du journal des événements hello passerelle a été augmentée à partir de 1 Mo too40 Mo.

*  Une boîte de dialogue d’avertissement s’affiche si un redémarrage est nécessaire pendant la mise à jour automatique de la passerelle. Vous pouvez choisir toorestart droite puis ou version ultérieure.

*  En cas d’échec de la mise à jour automatique, le programme d’installation de la passerelle retente la mise à jour automatique trois fois au maximum.

*  Amélioration des performances

    * Améliorez les performances lors du chargement de tables de grande taille à partir du serveur local dans le scénario de copie sans code.

*  Résolution des bogues

## <a name="11058921"></a>1.10.5892.1

*  Amélioration des performances

*  Résolution des bogues

## <a name="1958652"></a>1.9.5865.2

*  Capacité de mise à jour automatique Zero Touch
*  Nouvelle icône de barre d’état système avec des indicateurs d’état de la passerelle
*  Possibilité de trop « mettre à jour maintenant » à partir du client de hello
*  Heure de planification de capacité tooset mise à jour
*  Script PowerShell disponible pour activer/désactiver la mise à jour automatique
*  Prise en charge du format JSON  
*  Amélioration des performances
*  Résolution des bogues

## <a name="1858221"></a>1.8.5822.1

*  Amélioration de l’expérience de résolution des problèmes
*  Amélioration des performances
*  Résolution des bogues

### <a name="1757951"></a>1.7.5795.1

*  Amélioration des performances
*  Résolution des bogues

### <a name="1757641"></a>1.7.5764.1

*  Amélioration des performances
*  Résolution des bogues

### <a name="1657351"></a>1.6.5735.1

*  Prise en charge de la source/du récepteur HDFS en local
*  Amélioration des performances
*  Résolution des bogues

### <a name="1656961"></a>1.6.5696.1

*  Amélioration des performances
*  Résolution des bogues

### <a name="1656761"></a>1.6.5676.1

*  Prise en charge des outils de diagnostic dans le Gestionnaire de configuration
*  Prise en charge des colonnes de table pour les sources de données tabulaires pour Microsoft Azure Data Factory
*  Prise en charge de SQL DW pour Microsoft Azure Data Factory
*  Prise en charge de Reclusive dans BlobSource et FileSource pour Microsoft Azure Data Factory
*  Prise en charge de CopyBehavior (MergeFiles, PreserveHierarchy et FlattenHierarchy) dans BlobSink et FileSink avec copie binaire pour Microsoft Azure Data Factory
*  Prise en charge du signalement de progression de l’activité de copie pour Microsoft Azure Data Factory
*  Prise en charge de la validation de connectivité des sources de données pour Microsoft Azure Data Factory
*  Résolution des bogues

### <a name="1656721"></a>1.6.5672.1

*  Prise en charge des noms de tables pour la source de données ODBC pour Microsoft Azure Data Factory
*  Amélioration des performances
*  Résolution des bogues

### <a name="1656581"></a>1.6.5658.1

*  Prise en charge du récepteur de fichier pour Microsoft Azure Data Factory
*  Prise en charge de la conservation de la hiérarchie dans une copie binaire pour Microsoft Azure Data Factory
*  Prise en charge de l’idempotence de l’activité de copie pour Microsoft Azure Data Factory
*  Résolution des bogues

### <a name="1656401"></a>1.6.5640.1

*  Prise en charge de 3 sources de données supplémentaires pour Microsoft Azure Data Factory (ODBC, OData, HDFS)
*  Prise en charge du caractère guillemet dans l’analyseur CSV pour Microsoft Azure Data Factory
*  Prise en charge de la compression (BZip2)
*  Résolution des bogues

### <a name="1556121"></a>1.5.5612.1

*  Prise en charge de cinq bases de données relationnelles pour Microsoft Azure Data Factory (MySQL, PostgreSQL, DB2, Teradata et Sybase)
*  Prise en charge de la compression (Gzip et Deflate)
*  Amélioration des performances
*  Résolution des bogues

### <a name="1455491"></a>1.4.5549.1

*  Ajout de la prise en charge de source de données Oracle pour Microsoft Azure Data Factory
*  Amélioration des performances
*  Résolution des bogues

### <a name="1454921"></a>1.4.5492.1

*  Binaire unifié qui prend en charge à la fois des services Microsoft Azure Data Factory et Office 365 Power BI
*  Affiner le processus d’inscription et de l’interface utilisateur de Configuration de hello
*  Microsoft Azure Data Factory : prise en charge des entrées et sorties Azure pour la source de données SQL Server

### <a name="1253031"></a>1.2.5303.1

*  Corrigez toosupport de problème de délai d’attente plus long connexions source de données.

### <a name="1155268"></a>1.1.5526.8

*  .NET Framework 4.5.1 est requis pour l’installation.

### <a name="1051442"></a>1.0.5144.2

*  Aucune modification affectant les scénarios Microsoft Azure Data Factory.
