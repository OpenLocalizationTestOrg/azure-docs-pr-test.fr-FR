---
title: "aaaMicrosoft Azure Storage Explorer 0.8.7 (version préliminaire) | Documents Microsoft"
description: "Notes de publication pour l’explorateur de stockage Microsoft Azure 0.8.7 (version préliminaire)"
services: storage
documentationcenter: na
author: cawa
manager: paulyuk
editor: 
ms.assetid: 
ms.service: storage
ms.devlang: multiple
ms.topic: release-notes
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/18/2017
ms.author: cawa
ms.openlocfilehash: 9fdd491a3ea838e20f9d4f82c176cfb02fbe306b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-storage-explorer-087-preview"></a>Explorateur de stockage Microsoft Azure 0.8.7 (version préliminaire)
## <a name="overview"></a>Vue d'ensemble
Cet article contient les notes de publication hello pour la version préliminaire de Azure Storage Explorer 0.8.7.

[Explorateur de stockage Microsoft Azure (aperçu)](./vs-azure-tools-storage-manage-with-storage-explorer.md) est une application autonome qui vous permet de travail tooeasily avec des données de stockage Azure sur Windows, Mac OS et Linux.

## <a name="azure-storage-explorer-087-preview"></a>Explorateur de stockage Azure 0.8.7 (version préliminaire)
### <a name="download-azure-storage-explorer-087-preview"></a>Télécharger l’explorateur de stockage Azure 0.8.7 (version préliminaire)
- [Version préliminaire de l’explorateur de stockage Azure 0.8.7 pour Windows](https://go.microsoft.com/fwlink/?LinkId=708343)
- [Version préliminaire de l’explorateur de stockage Azure 0.8.7 pour Mac](https://go.microsoft.com/fwlink/?LinkId=708342)
- [Version préliminaire de l’explorateur de stockage Azure 0.8.7 pour Linux](https://go.microsoft.com/fwlink/?LinkId=722418)

### <a name="new-updates"></a>Nouvelles mises à jour
* Vous pouvez choisir comment conflits tooresolve au début de hello d’une mise à jour, télécharger ou copier session Bonjour **activités** fenêtre.
* Pointez sur un onglet toosee hello chemin d’accès complet de la ressource de stockage hello.
* Lorsque vous cliquez sur un onglet, il se synchronise avec son emplacement dans le volet de navigation de gauche hello.

### <a name="fixes"></a>Correctifs
* Problème résolu : l’explorateur de stockage est désormais une application de confiance sur macOS.
* Problème résolu : Ubuntu 14.04 est de nouveau pris en charge.
* Problème résolu : Parfois hello ajouter de l’interface utilisateur compte clignote lors du chargement des abonnements.
* Problème résolu : Parfois pas toutes les ressources de stockage ont été répertoriés dans le volet de navigation de gauche hello.
* Problème résolu : volet Actions de hello affiche parfois actions vides.
* Problème résolu : taille de la fenêtre de session de la dernière fermé de hello hello est maintenant conservé.
* Résolution : Vous pouvez ouvrir plusieurs onglets pour hello même ressource à l’aide du menu contextuel de hello.

### <a name="known-issues"></a>Problèmes connus
* L’Accès rapide fonctionne uniquement avec les éléments basés sur un abonnement. Les ressources locales ou attachées par le biais d’une clé ou d’un jeton SAP ne sont pas prises en charge dans cette version.
* Accès rapide peut prendre quelques secondes toonavigate toohello ressource cible, selon le nombre de ressources.
* Ayant plus de trois groupes d’objets BLOB ou télécharger à hello, même les fichiers temps peut provoquer des erreurs.
* Les recherches peuvent porter sur 50 000 nœuds environ. Au-delà, elles affecteront les performances ou pourront entraîner des exceptions non prises en charge.
* Pourquoi première fois à l’aide de hello Explorateur de stockage sur macOS, vous pouvez voir plusieurs invites demandant trousseau de l’utilisateur autorisation tooaccess hello. Nous vous suggérons de sélectionner **toujours autoriser** afin de l’invite de commandes hello n’affiche à nouveau

## <a name="previous-releases"></a>Versions précédentes
### <a name="features"></a>Caractéristiques
#### <a name="main-features"></a>Caractéristiques principales
* Versions macOS, Linux et Windows
* La connexion tooview vos comptes de stockage regroupés par abonnement :
    * Utilisez votre compte professionnel ou Microsoft, 2FA, etc.
    * Configurez et gérez les paramètres de proxy
    * Supprimez des comptes en vous déconnectant
* Se connecter à l’aide des comptes tooStorage :
    * Nom et clé du compte
    * Points de terminaison personnalisés (y compris Azure China)
    * URI SAP pour les comptes de stockage
* Prise en charge d’Azure Resource Manager et du stockage classique
* Générez des clés SAP pour les blobs, conteneurs d’objets blob, files d’attente, tables ou partages de fichiers
* Se connecter tooblob conteneurs, des files d’attente, des tables ou des partages de fichiers avec la clé de Signatures d’accès partagé (SAS)
* Gérez les stratégies d’accès stockées pour les conteneurs d’objets blob, files d’attente, tables ou partages de fichiers
* Stockage de développement local avec l’Émulateur de stockage (Windows uniquement)
* Créez et supprimez des conteneurs d’objets blob, files d’attente ou tables
* Affichez les conteneurs d’objets blob $logs et les tables $metrics
* Recherchez des blobs, files d’attente, tables ou partages de fichiers spécifiques
* Comptes toostorage de liens directs ou des conteneurs, des files d’attente, des tables ou des fichier partage pour le partage et facilement l’accès à vos ressources
* Renommez des conteneurs d’objets blob, tables et partages de fichiers
* Capacité toomanage et configurer les règles CORS
* Copiez facilement des clés primaires et secondaires pour les comptes de stockage
* Vérifications MD5 pour contrôler l’intégrité et la cohérence des données lors du chargement et du téléchargement
* Rechercher vos conteneurs d’objets blob, les tables, les files d’attente, les partages de fichiers ou les comptes de stockage à partir de la zone de recherche hello
* Vous pouvez maintenant le code confidentiel plus fréquemment utilisés services toohello accès rapide pour faciliter la navigation
* Vous pouvez désormais ouvrir plusieurs éditeurs dans différents onglets. Tooopen un onglet temporaire ; par simple clic Double-cliquez sur tooopen un onglet permanent. Vous pouvez également cliquer sur hello onglet temporaire toomake il un onglet permanent
* Améliorations notables en termes de stabilité et de performances pour les chargements et téléchargements, en particulier pour les fichiers volumineux sur des machines rapides
* Nous sommes réintroduction de recherche thématique améliorée de hello et concept hello ajouté de portée. Entrez le nœud tooa de chemin d’accès hello via l’icône de pointage hello, clic droit -> « Recherche d’ici », ou manuellement tooscope ce nœud. Une fois la portée, vous pouvez ajouter une fin de toohello recherche terme de recherche de toodeep hello chemin d’accès à partir de ce nœud
* Nous avons ajouté différents thèmes : Clair (par défaut), Foncé, Contraste noir élevé et Contraste blanc élevé.
* Accédez tooEdit -> thèmes toochange votre préférence de thèmes
* Sous Linux, un système d’exploitation 64 bits est désormais obligatoire
* Nous avons mis à jour notre logo.
#### <a name="blobs"></a>Objets blob
* Affichez les blobs et parcourez les répertoires
* Chargez, téléchargez, supprimez et copiez des blobs et des dossiers
* Ouvrir et consulter les BLOB hello contenu texte et image
* Affichez et modifiez les propriétés et métadonnées des blobs
* Recherchez les blobs par préfixe
* Créez et annulez les baux des blobs et conteneurs d’objets blob
* Faites glisser et déplacer tooupload de fichiers
* Renommez les blobs et dossiers
* Des dossiers « virtuels » vides peuvent maintenant être créés dans des conteneurs d’objets blob
* Vous pouvez modifier les propriétés d’objet Blob et le fichier hello
#### <a name="tables"></a>Tables
* Afficher et interroger des entités avec ODATA ou utiliser des requêtes complexes toocreate du Générateur de requête
* Ajoutez, modifiez ou supprimez des entités
* Importez et exportez le contenu des tables au format CSV (avec exportation des résultats des requêtes)
* Personnalisez l’ordre des colonnes
* Requêtes toosave de capacité
#### <a name="queues"></a>Files d’attente
* Affichez un aperçu des 32 derniers messages
* Ajoutez, enlevez de la file d’attente et affichez les messages
* Effacez la file d’attente
* Nous avons fait en sorte que pour vous toodecide si vous souhaitez tooencode/décoder votre file d’attente messages
#### <a name="file-shares"></a>Partages de fichiers
* Affichez les fichiers et parcourez les répertoires
* Chargez, téléchargez, supprimez et copiez des fichiers et des répertoires
* Affichez les propriétés de fichier
* Renommez les fichiers et répertoires

### <a name="bug-fixes"></a>Résolution des bogues
* Problème résolu : blocage de l’écran
* Sécurité améliorée

### <a name="known-issues"></a>Problèmes connus
* Les recherches peuvent porter sur 50 000 nœuds environ. Au-delà, elles affecteront les performances et les installations macOS nécessiteront peut-être des autorisations élevées
* Panneau des paramètres de compte peut indiquer que vous avez besoin d’abonnements de toofilter tooreenter informations d’identification
* Les captures instantanées ne sont pas conservées lorsque les blobs sont renommés (individuellement ou dans un conteneur d’objets blob renommé). Cependant, lors d’un changement de nom, toutes les autres propriétés et métadonnées des blobs, fichiers et entités sont conservées.
* Pile Azure ne prend actuellement en charge des fichiers, par conséquent, la tentative de tooexpand hello **fichiers** nœud entraîne une erreur
* L’installation de Linux 14.04 requiert la mise à jour ou la mise à niveau de la version gcc. Hello étapes suivantes illustrent comment tooupgrade :

```
sudo add-apt-repository ppa:ubuntu-toolchain-r/test
sudo apt-get update
sudo apt-get upgrade
sudo apt-get dist-upgrade
```

### <a name="previous-versions"></a>Versions antérieures
#### <a name="october-2016-release-version-085"></a>Version d’octobre 2016 (version 0.8.5)
* [Téléchargement pour Windows](https://go.microsoft.com/fwlink/?LinkId=809306)
* [Téléchargement pour Mac](https://go.microsoft.com/fwlink/?LinkId=809307)
* [Téléchargement pour Linux](https://go.microsoft.com/fwlink/?LinkId=809308)
