---
title: "notes de version de l’Explorateur de stockage Azure (aperçu) aaaMicrosoft | Documents Microsoft"
description: "Notes de publication pour Microsoft Azure Storage Explorer (préversion)"
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
ms.date: 07/31/2017
ms.author: cawa
ms.openlocfilehash: 44ff6dc8e2015f4eb71fa13098b832fbbf48ccac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-storage-explorer-preview-release-notes"></a>Notes de publication pour Microsoft Azure Storage Explorer (préversion)

Cet article contient des notes pour Azure Storage Explorer 0.8.16 (version préliminaire) version, ainsi que les notes de publication pour les versions précédentes de la mise en production hello.

[Explorateur de stockage Microsoft Azure (aperçu)](./vs-azure-tools-storage-manage-with-storage-explorer.md) est une application autonome qui vous permet de travail tooeasily avec des données de stockage Azure sur Windows, Mac OS et Linux.

## <a name="version-0816-preview"></a>Version 0.8.16 (préversion)
8/21/2017

### <a name="download-azure-storage-explorer-0816-preview"></a>Télécharger l’explorateur de stockage Azure 0.8.16 (préversion)
- [Explorateur de stockage Azure 0.8.16 (préversion) pour Windows](https://go.microsoft.com/fwlink/?LinkId=708343)
- [Explorateur de stockage Azure 0.8.16 (préversion) pour Mac](https://go.microsoft.com/fwlink/?LinkId=708342)
- [Explorateur de stockage Azure 0.8.16 (préversion) pour Linux](https://go.microsoft.com/fwlink/?LinkId=722418)

### <a name="new"></a>Nouveau
* Lorsque vous ouvrez un objet blob, Explorateur de stockage vous demandera tooupload hello téléchargé fichier si une modification est détectée.
* Expérience de connexion Azure Stack améliorée
* Performances améliorées hello du téléchargement de nombreuses petits fichiers hello même temps


### <a name="fixes"></a>Correctifs
* Pour certains types d’objets blob, en choisissant trop « replace » pendant un conflit de téléchargement parfois entraînerait téléchargement hello en cours de redémarrage. 
* Dans la version 0.8.15, les chargements se bloquaient quelquefois à 99 %.
* Lors du chargement de partage de fichiers tooa fichiers, si vous avez choisi le répertoire de tooa tooupload qui n’existe pas encore, le téléchargement échoue.
* L’explorateur de stockage créait de façon incorrecte des horodatages pour les requêtes de table et les signatures d’accès partagé.


Problèmes connus
* Actuellement, l’utilisation d’une chaîne de connexion clé et nom ne fonctionne pas. Il sera résolu dans une prochaine version de hello. En attendant, vous pouvez utiliser l’attachement avec le nom et la clé.
* Si vous essayez de tooopen un fichier avec un nom de fichier Windows non valide, le téléchargement de hello entraîne un erreur fichier non trouvé.
* Après avoir cliqué sur « Annuler » sur une tâche, il peut prendre un certain temps pour toocancel de cette tâche. Il s’agit d’une limitation de la bibliothèque de nœud de stockage Azure hello.
* Après avoir effectué un téléchargement de l’objet blob, onglet hello initiée par le téléchargement de hello est actualisé. Cela est une modification du comportement précédent et entraîne également vous toobe pris nouveau conteneur hello dans toohello racine.
* Si vous choisissez hello mauvais code confidentiel de carte à puce/certificat, vous devez toorestart dans l’ordre toohave Explorateur de stockage oubliez cette décision.
* Panneau de paramètres de compte Hello peut indiquer que vous avez besoin d’abonnements de toofilter tooreenter informations d’identification.
* Les captures instantanées ne sont pas conservées lorsque les blobs sont renommés (individuellement ou dans un conteneur d’objets blob renommé). Lors d’un changement de nom, toutes les autres propriétés et métadonnées des objets blob, fichiers et entités sont conservées.
* Bien que Azure Stack ne prend actuellement pas en charge les partages de fichiers, un nœud de partages de fichiers apparaît toujours sous un compte de stockage d’Azure Stack joint.
* Pour les utilisateurs sur Ubuntu 14.04, vous devez tooensure GCC est toodate - cela est possible en exécutant hello suivant de commandes, puis le redémarrage de votre ordinateur :

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```

* Pour les utilisateurs sur Ubuntu 17.04, vous devez tooinstall GConf - cela hello suivant de commandes, puis le redémarrage de votre ordinateur en cours d’exécution :

    ```
    sudo apt-get install libgconf-2-4
    ```

## <a name="version-0814-preview"></a>Version 0.8.14 (aperçu)
06/22/2017

### <a name="download-azure-storage-explorer-0814-preview"></a>Télécharger Azure Storage Explorer 0.8.14 (préversion)
* [Télécharger l’explorateur de stockage Azure 0.8.14 (aperçu) pour Windows](https://go.microsoft.com/fwlink/?LinkId=809306)
* [Télécharger Azure Storage Explorer 0.8.14 (préversion) pour Mac](https://go.microsoft.com/fwlink/?LinkId=809307)
* [Télécharger l’explorateur de stockage Azure 0.8.14 (aperçu) pour Linux](https://go.microsoft.com/fwlink/?LinkId=809308)

### <a name="new"></a>Nouveau

* Mise à jour too1.7.2 de version électronique dans parti de tootake d’ordre de plusieurs mises à jour critiques
* Vous pouvez maintenant accéder rapidement aux guide de dépannage en ligne hello à partir du menu d’aide hello
* [Guide][2] de dépannage de Storage Explorer
* [Instructions] [ 3] sur la connexion d’abonnement de Azure pile tooan

### <a name="known-issues"></a>Problèmes connus

* Boutons de la boîte de dialogue de confirmation à dossier hello delete n’inscrivez pas avec les clics de souris hello sur Linux. Solution de contournement est la clé d’entrée toouse hello
* Si vous choisissez hello mauvais code confidentiel de carte à puce/certificat, vous devez toorestart dans l’ordre toohave Explorateur de stockage oublier la décision de hello
* Plus de 3 groupes des objets BLOB ou des fichiers de téléchargement à hello même temps peut provoquer des erreurs
* Panneau de paramètres de compte Hello peut indiquer que vous avez besoin d’informations d’identification tooreenter dans les abonnements toofilter de commande
* Les captures instantanées ne sont pas conservées lorsque les blobs sont renommés (individuellement ou dans un conteneur d’objets blob renommé). Lors d’un changement de nom, toutes les autres propriétés et métadonnées des objets blob, fichiers et entités sont conservées.
* Bien qu’Azure Stack ne prend actuellement pas en charge les partages de fichiers, un nœud de partages de fichiers apparaît toujours sous un compte de stockage d’Azure Stack joint. 
* Ubuntu 14.04 installation besoins gcc version mise à jour ou mise à niveau – tooupgrade d’étapes sont répertoriées ci-dessous :

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```




## <a name="previous-releases"></a>Versions précédentes

* [Version 0.8.13](#version-0813)
* [Version 0.8.12 / 0.8.11 / 0.8.10](#version-0812--0811--0810)
* [Version 0.8.9 / 0.8.8](#version-089--088)
* [Version 0.8.7](#version-087)
* [Version 0.8.6](#version-086)
* [Version 0.8.5](#version-085)
* [Version 0.8.4](#version-084)
* [Version 0.8.3](#version-083)
* [Version 0.8.2](#version-082)
* [Version 0.8.0](#version-080)
* [Version 0.7.20160509.0](#version-07201605090)
* [Version 0.7.20160325.0](#version-07201603250)
* [Version 0.7.20160129.1](#version-07201601291)
* [Version 0.7.20160105.0](#version-07201601050)
* [Version 0.7.20151116.0](#version-07201511160)


### <a name="version-0813"></a>Version 0.8.13
05/12/2017

#### <a name="new"></a>Nouveau

* [Guide][2] de dépannage de Storage Explorer
* [Instructions] [ 3] sur la connexion d’abonnement de Azure pile tooan

#### <a name="fixes"></a>Correctifs

* Problème résolu : le chargement du fichier peut provoquer très probablement une erreur de mémoire insuffisante
* Problème résolu : vous pouvez maintenant vous connecter avec le code PIN/carte à puce
* Problème résolu : l’ouverture dans le portail fonctionne à présent avec Azure Chine, Azure Allemagne, Azure US Government et Azure Stack
* Problème résolu : Lors du téléchargement d’un conteneur d’objets blob tooa dossier, une erreur « Opération non conforme » se produisait parfois
* Problème résolu : sélectionner tout est désactivé lors de gestion des instantanés
* Problème résolu : hello des métadonnées de l’objet blob de base hello risquent d’être écrasées après affichage des propriétés hello ses instantanés

#### <a name="known-issues"></a>Problèmes connus

* Si vous choisissez hello mauvais code confidentiel de carte à puce/certificat, vous devez toorestart dans l’ordre toohave Explorateur de stockage oublier la décision de hello
* Alors que le zoom avant ou arrière, niveau de zoom hello peut réinitialiser momentanément toohello au niveau de la valeur par défaut
* Plus de 3 groupes des objets BLOB ou des fichiers de téléchargement à hello même temps peut provoquer des erreurs
* Panneau de paramètres de compte Hello peut indiquer que vous avez besoin d’informations d’identification tooreenter dans les abonnements toofilter de commande
* Les captures instantanées ne sont pas conservées lorsque les blobs sont renommés (individuellement ou dans un conteneur d’objets blob renommé). Lors d’un changement de nom, toutes les autres propriétés et métadonnées des objets blob, fichiers et entités sont conservées.
* Bien que Azure Stack ne prend actuellement pas en charge les partages de fichiers, un nœud de partages de fichiers apparaît toujours sous un compte de stockage d’Azure Stack joint. 
* Ubuntu 14.04 installation besoins gcc version mise à jour ou mise à niveau – tooupgrade d’étapes sont répertoriées ci-dessous :

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```


### <a name="version-0812--0811--0810"></a>Version 0.8.12 / 0.8.11 / 0.8.10
04/07/2017

#### <a name="new"></a>Nouveau

* Explorateur de stockage se ferme désormais automatiquement lorsque vous installez une mise à jour à partir de la notification de mise à jour hello
* L’accès rapide sur place fournit une expérience améliorée pour utiliser vos ressources fréquemment sollicitées
* Dans l’éditeur de conteneur d’objets Blob hello, vous pouvez maintenant voir quel ordinateur virtuel auquel appartient un objet blob loué
* Vous pouvez désormais réduire le panneau de gauche de hello
* Découverte maintenant s’exécute sur hello même temps en tant que téléchargement
* Utilisation des statistiques Bonjour conteneur d’objets Blob, de partage de fichiers et de Table éditeurs toosee hello taille de votre ressource ou de la sélection
* Vous pouvez maintenant tooAzure de connexion dans Active Directory (AAD) basée sur les comptes Azure pile. 
* Vous pouvez à présent les comptes de stockage de plus de 32 Mo tooPremium les fichiers d’archives de téléchargement
* Prise en charge de l’accessibilité améliorée
* Vous pouvez maintenant ajouter approuvé Base-64 encodé de certificats X.509 SSL en accédant tooEdit -&gt; les certificats SSL -&gt; les certificats d’importation

#### <a name="fixes"></a>Correctifs

* Problème résolu : après l’actualisation des informations d’identification d’un compte, arborescence hello est parfois pas actualiser automatiquement
* Problème résolu : générer une SAP pour les tables et les files d’attente de l’émulateur peut entraîner une URL non valide
* Problème résolu : les comptes de stockage premium peuvent maintenant être développés lorsqu’un proxy est activé
* Problème résolu : hello bouton Appliquer sur les comptes hello page de gestion ne fonctionnera pas si vous aviez 1 ou 0 comptes sélectionnés
* Problème résolu : le téléchargement d’objets blob qui nécessitent des résolutions de conflit peut échouer - résolu dans 0.8.11 
* Problème résolu : l’envoi de commentaires a été interrompu dans 0.8.11 - résolu dans 0.8.12 

#### <a name="known-issues"></a>Problèmes connus

* Après la mise à niveau too0.8.10, vous devez toorefresh toutes vos informations d’identification.
* Alors que le zoom avant ou arrière, niveau de zoom hello peut réinitialiser momentanément toohello au niveau de la valeur par défaut.
* Plus de 3 groupes des objets BLOB ou des fichiers de téléchargement à hello même temps peut provoquer des erreurs.
* Panneau de paramètres de compte Hello peut indiquer que vous avez besoin d’informations d’identification tooreenter dans les abonnements toofilter de commande.
* Les captures instantanées ne sont pas conservées lorsque les blobs sont renommés (individuellement ou dans un conteneur d’objets blob renommé). Lors d’un changement de nom, toutes les autres propriétés et métadonnées des objets blob, fichiers et entités sont conservées.
* Bien que Azure Stack ne prend actuellement pas en charge les partages de fichiers, un nœud de partages de fichiers apparaît toujours sous un compte de stockage d’Azure Stack joint. 
* Ubuntu 14.04 installation besoins gcc version mise à jour ou mise à niveau – tooupgrade d’étapes sont répertoriées ci-dessous :

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```


### <a name="version-089--088"></a>Version 0.8.9 / 0.8.8
02/23/2017

<iframe width="560" height="315" src="https://www.youtube.com/embed/R6gonK3cYAc?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/SrRPCm94mfE?ecver=1" frameborder="0" allowfullscreen></iframe>


#### <a name="new"></a>Nouveau

* Explorateur de stockage 0.8.9 téléchargera automatiquement version la plus récente hello pour les mises à jour.
* Correctif : à l’aide d’un portail généré tooattach URI SAS qu'un compte de stockage entraînerait une erreur.
* Vous pouvez désormais créer, gérer et promouvoir des instantanés d’objets blob.
* Vous pouvez désormais vous connecter dans les comptes de tooAzure en Chine, Azure situés en Allemagne et Azure du gouvernement.
* Vous pouvez maintenant modifier le niveau de zoom hello. Utiliser les options de hello hello tooZoom de menu vue en Zoom arrière et réinitialiser le Zoom.
* Les caractères Unicode sont désormais pris en charge dans les métadonnées de l’utilisateur pour les fichiers et les objets blob.
* Améliorations de l’accessibilité.
* notes de publication de la version suivante Hello peuvent être affichés à partir de la notification de mise à jour hello. Vous pouvez également afficher hello notes de publication à partir du menu d’aide hello.

#### <a name="fixes"></a>Correctifs

* Problème résolu : numéro de version hello s’affiche désormais correctement dans le panneau de configuration sur Windows
* Problème résolu : recherche n’est plus limitée too50, 000 nœuds
* Problème résolu : partage de fichiers de téléchargement tooa tourné indéfiniment si le répertoire de destination hello n’existait pas
* Problème résolu : stabilité améliorée pour de longs chargements et téléchargements

#### <a name="known-issues"></a>Problèmes connus

* Alors que le zoom avant ou arrière, niveau de zoom hello peut réinitialiser momentanément toohello au niveau de la valeur par défaut.
* L’Accès rapide fonctionne uniquement avec les éléments basés sur l’abonnement. Les ressources locales ou attachées par le biais d’une clé ou d’un jeton SAP ne sont pas prises en charge dans cette version.
* Accès rapide peut prendre quelques secondes toonavigate toohello ressource cible, selon le nombre de ressources.
* Plus de 3 groupes des objets BLOB ou des fichiers de téléchargement à hello même temps peut provoquer des erreurs.

12/16/2016
### <a name="version-087"></a>Version 0.8.7

<iframe width="560" height="315" src="https://www.youtube.com/embed/Me4Y4jxoer8?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a>Nouveau

* Vous pouvez choisir comment conflits tooresolve au début de hello d’une mise à jour, télécharger ou copier la session dans la fenêtre des activités hello
* Placez le curseur sur un onglet toosee hello chemin d’accès complet de la ressource de stockage hello
* Lorsque vous cliquez sur un onglet, il se synchronise avec son emplacement dans le volet de navigation de gauche hello

#### <a name="fixes"></a>Correctifs

* Problème résolu : Storage Explorer est désormais une application approuvée sur Mac
* Problème résolu : Ubuntu 14.04 est de nouveau pris en charge
* Problème résolu : Parfois hello Ajouter compte UI clignote lors du chargement des abonnements
* Problème résolu : Parfois pas toutes les ressources de stockage ont été répertoriés dans le volet de navigation de gauche hello
* Problème résolu : hello volet Actions parfois affiche les actions vides
* Problème résolu : la taille de la fenêtre de session de la dernière fermé de hello hello est maintenant conservé
* Résolution : Vous pouvez ouvrir plusieurs onglets pour hello même ressource à l’aide du menu contextuel de hello

#### <a name="known-issues"></a>Problèmes connus

* L’Accès rapide fonctionne uniquement avec les éléments basés sur l’abonnement. Les ressources locales ou attachées par le biais d’une clé ou d’un jeton SAP ne sont pas prises en charge dans cette version
* Accès rapide peut prendre quelques secondes toonavigate toohello ressource cible, selon le nombre de ressources
* Plus de 3 groupes des objets BLOB ou des fichiers de téléchargement à hello même temps peut provoquer des erreurs
* Les recherches peuvent porter sur 50 000 nœuds environ. Au-delà, elles affectent les performances ou peuvent entraîner des exceptions non prises en charge
* Pourquoi première fois à l’aide de hello Explorateur de stockage sur macOS, vous pouvez voir plusieurs invites demandant trousseau de tooaccess d’autorisation de l’utilisateur. Nous vous suggérons de que sélectionner toujours autoriser afin de l’invite de commandes hello ne s’afficheront à nouveau

11/18/2016
### <a name="version-086"></a>Version 0.8.6

#### <a name="new"></a>Nouveau

* Vous pouvez maintenant le code confidentiel plus fréquemment utilisés services toohello accès rapide pour faciliter la navigation
* Vous pouvez désormais ouvrir plusieurs éditeurs dans différents onglets. Tooopen un onglet temporaire ; par simple clic Double-cliquez sur tooopen un onglet permanent. Vous pouvez également cliquer sur hello onglet temporaire toomake il un onglet permanent
* Des améliorations notables en termes de stabilité et de performances pour les chargements et téléchargements ont été réalisés, en particulier pour les fichiers volumineux sur des machines rapides
* Des dossiers « virtuels » vides peuvent maintenant être créés dans des conteneurs d’objets blob
* Nous avons réintroduit une recherche étendue avec notre nouvelle recherche de sous-chaîne améliorée. Vous disposez désormais de deux options de recherche : 
    * Global recherche - simplement entrer un terme à rechercher dans la zone de texte Rechercher hello
    * Recherche thématique - cliquez sur hello loupe icône tooa nœud suivant, ajouter une fin de toohello de terme de recherche du chemin de hello, ou avec le bouton droit et sélectionnez « Recherche d’ici »
* Nous avons ajouté différents thèmes : Clair (par défaut), Foncé, Contraste noir élevé et Contraste blanc élevé. Accédez tooEdit -&gt; thèmes toochange votre préférence de thèmes
* Vous pouvez modifier les propriétés des objets blob et des fichiers
* Nous prenons désormais en charge les messages des files d’attente codés (base 64) et non codés
* Sous Linux, un système d’exploitation 64 bits est désormais obligatoire. Pour cette version, nous ne prenons en charge que Ubuntu 16.04.1 LTS 64 bits
* Nous avons mis à jour notre logo.

#### <a name="fixes"></a>Correctifs

* Problème résolu : blocage de l’écran
* Sécurité améliorée
* Problème résolu : il peut arriver que des comptes joints en double s’affichent
* Problème résolu : un objet blob avec un type de contenu non défini peut générer une exception
* Problème résolu : Hello lors de l’ouverture du Panneau de requête sur une table vide n’était pas possible
* Problème résolu : bogues différents dans la recherche
* Problème résolu : Augmenté nombre hello de ressources chargées à partir de 50 too100 lorsque vous cliquez sur « Charge plus »
* Problème résolu : lors de la première exécution, si un compte est connecté, tous les abonnements sont sélectionnés pour ce compte par défaut 

#### <a name="known-issues"></a>Problèmes connus

* Cette version de hello Explorateur de stockage ne fonctionne pas sur Ubuntu 14.04
* tooopen plusieurs onglets pour hello même ressource, effectuez pas continuellement cliquez sur hello même ressource. Cliquez sur une autre ressource, puis revenir en arrière, puis cliquez sur tooopen de ressource d’origine hello il à nouveau dans un autre onglet 
* L’Accès rapide fonctionne uniquement avec les éléments basés sur l’abonnement. Les ressources locales ou attachées par le biais d’une clé ou d’un jeton SAP ne sont pas prises en charge dans cette version
* Accès rapide peut prendre quelques secondes toonavigate toohello ressource cible, selon le nombre de ressources
* Plus de 3 groupes des objets BLOB ou des fichiers de téléchargement à hello même temps peut provoquer des erreurs
* Les recherches peuvent porter sur 50 000 nœuds environ. Au-delà, elles affectent les performances ou peuvent entraîner des exceptions non prises en charge

10/03/2016
### <a name="version-085"></a>Version 0.8.5

#### <a name="new"></a>Nouveau

* Peuvent désormais utiliser les associations de sécurité générés par le portail de clés tooattach tooStorage comptes et des ressources

#### <a name="fixes"></a>Correctifs

* Problème résolu : condition de concurrence lors de la recherche parfois dû toobecome de nœuds non extensible
* Problème résolu : « Utiliser HTTP » ne fonctionne pas lors de la connexion des comptes tooStorage avec la clé et le nom du compte
* Problème résolu : les clés SAP (en particulier celles qui sont générées par le portail) renvoient une erreur « barre oblique »
* Problème résolu : problèmes d’importation de tables
    * Parfois, la clé de partition et la clé de ligne ont été inversées
    * Impossible de tooread « null » les clés de Partition

#### <a name="known-issues"></a>Problèmes connus

* Les recherches peuvent porter sur 50 000 nœuds environ. Au-delà, elles affectent les performances
* Pile Azure ne prend actuellement en charge les fichiers, afin de la tentative de tooexpand fichiers affichera une erreur

09/12/2016
### <a name="version-084"></a>Version 0.8.4

<iframe width="560" height="315" src="https://www.youtube.com/embed/cr5tOGyGrIQ?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a>Nouveau

* Générer des comptes toostorage de liens directs, des conteneurs, des files d’attente, des tableaux ou des partages de fichiers simple pour le partage et accéder aux ressources de tooyour - Windows et prend en charge de Mac OS
* Rechercher vos conteneurs d’objets blob, les tables, les files d’attente, les partages de fichiers ou les comptes de stockage à partir de la zone de recherche hello
* Vous pouvez maintenant regrouper des clauses dans le Générateur de requêtes de table hello
* Renommer et copier/coller des conteneurs d’objets blob, des partages de fichiers, des tables, des objets blob, des dossiers d’objets blob, des fichiers et répertoires depuis des comptes et conteneurs joint par SAP
* Le changement de nom et la& copie des conteneurs d’objets blob et des partages de fichiers préservent désormais les métadonnées et propriétés

#### <a name="fixes"></a>Correctifs

* Problème résolu : impossible de modifier des entités de tables si elles contiennent des propriétés booléennes ou binaires

#### <a name="known-issues"></a>Problèmes connus

* Les recherches peuvent porter sur 50 000 nœuds environ. Au-delà, elles affectent les performances

08/03/2016
### <a name="version-083"></a>Version 0.8.3

<iframe width="560" height="315" src="https://www.youtube.com/embed/HeGW-jkSd9Y?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a>Nouveau

* Renommez des conteneurs, tables et partages de fichiers
* Meilleure expérience de générateur de requête
* Capacité toosave et charge les requêtes
* Diriger les tables des comptes ou des conteneurs, les files d’attente, toostorage liens ou des partages pour le partage et facilement l’accès à vos ressources de fichiers (Windows uniquement - macOS prennent en charge sera bientôt disponible !)
* Capacité toomanage et configurer les règles CORS

#### <a name="fixes"></a>Correctifs

* Problème résolu : les comptes Microsoft nécessitent une nouvelle authentification toutes les 8 à 12 heures

#### <a name="known-issues"></a>Problèmes connus

* Parfois hello l’interface utilisateur peut sembler bloquée - agrandissement de fenêtre hello permet de résoudre ce problème
* L’installation de macOS peut nécessiter des autorisations élevées
* Panneau des paramètres de compte peut indiquer que vous avez besoin d’informations d’identification tooreenter dans les abonnements toofilter de commande
* Changement de nom des partages de fichiers, les conteneurs d’objets blob et les tables ne conserve pas les métadonnées ou autres propriétés sur le conteneur de hello, telles que le quota du partage de fichiers, de niveau d’accès public ou de stratégies d’accès
* Les captures instantanées ne sont pas conservées lorsque les blobs sont renommés (individuellement ou dans un conteneur d’objets blob renommé). Lors d’un changement de nom, toutes les autres propriétés et métadonnées des objets blob, fichiers et entités sont conservées
* Copier ou renommer des ressources ne fonctionne pas à l’intérieur des comptes joints par SAP

07/07/2016
### <a name="version-082"></a>Version 0.8.2

<iframe width="560" height="315" src="https://www.youtube.com/embed/nYgKbRUNYZA?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a>Nouveau

* Les comptes de stockage sont regroupés par abonnements ; le stockage de développement et les ressources jointes via la clé ou SAP sont affichés sous le nœud (local et joint)
* Se déconnecter depuis des comptes dans le panneau « Paramètres du compte Azure »
* Configurer les tooenable des paramètres de proxy et gérer les connexion
* Créer et annuler des baux d’objets blob
* Ouvrir des conteneurs d’objets blob, des files d’attente, des tables et des fichiers avec un simple clic

#### <a name="fixes"></a>Correctifs

* Problème résolu : les messages de files d’attente insérés à l’aide des bibliothèques .NET ou Java ne sont pas correctement décodés depuis base64
* Problème résolu : les tables $metrics ne figurent pas pour les comptes de stockage d’objets blob
* Problème résolu : le nœud de la table ne fonctionne pas pour le stockage local (développement)

#### <a name="known-issues"></a>Problèmes connus

* L’installation de macOS peut nécessiter des autorisations élevées

06/15/2016
### <a name="version-080"></a>Version 0.8.0

<iframe width="560" height="315" src="https://www.youtube.com/embed/ycfQhKztSIY?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/k4_kOUCZ0WA?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/3zEXJcGdl_k?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a>Nouveau

* Prise en charge du partage de fichiers : affichage, téléchargement, chargement, copie de fichiers et de répertoires, URI SAP (créer et connecter)
* Amélioration de l’expérience utilisateur pour la connexion tooStorage avec SAS URI ou des clés de compte
* Exporter des résultats de requêtes de table
* Réorganisation et personnalisation des colonnes de table
* Affichage des conteneurs d’objets blob $logs et de tables $metrics pour les comptes de stockage avec les mesures activées
* L’amélioration du comportement d’exportation et d’importation, inclut désormais le type de valeur de propriété

#### <a name="fixes"></a>Correctifs

* Problème résolu : le chargement ou le téléchargement d’objets blob volumineux peut entraîner des chargements/téléchargements incomplets
* Modification fixe :, l’ajout ou l’importation d’une entité avec une valeur de chaîne numérique (« 1 »), il sera converti toodouble
* Problème résolu : Nœud de table hello tooexpand impossible dans un environnement de développement local hello

#### <a name="known-issues"></a>Problèmes connus

* Les tables $metrics ne figurent pas pour les comptes de stockage d’objets blob
* File d’attente des messages ajoutés par programmation ne peuvent pas s’afficher correctement si les messages de type hello sont codés en Base64

05/17/2016
### <a name="version-07201605090"></a>Version 0.7.20160509.0

#### <a name="new"></a>Nouveau

* Une meilleure gestion des erreurs pour les incidents d’applications

#### <a name="fixes"></a>Correctifs

* Bogue résolu dans lequel les messages de la barre d’informations parfois n’apparaissent pas lorsque les informations d’identification de connexion sont requises

#### <a name="known-issues"></a>Problèmes connus

* Tables : Ajout, modification, ou l’importation d’une entité qui a une propriété avec une valeur numérique ambiguë, comme « 1 » ou « 1.0 », et hello utilisateur tentatives toosend comme un `Edm.String`, valeur de hello reviendra via le client hello API comme un Edm.Double

03/31/2016

### <a name="version-07201603250"></a>Version 0.7.20160325.0

<iframe width="560" height="315" src="https://www.youtube.com/embed/imbgBRHX65A?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/ceX-P8XZ-s8?ecver=1" frameborder="0" allowfullscreen></iframe>


#### <a name="new"></a>Nouveau

* Prise en charge de la table : opérations d’affichage, d’interrogation, d’exportation, d’importation et CRUD pour les entités
* Prise en charge de la file d’attente : affichage, ajout, retrait de la file d’attente des messages
* Génération d’URI SAP pour les comptes de stockage
* Connecter des comptes de tooStorage à des URI SAS
* Notifications de mise à jour pour les futures mises à jour tooStorage Explorer
* Apparence mise à jour

#### <a name="fixes"></a>Correctifs

* Améliorations des performances et de la fiabilité

### <a name="known-issues-amp-mitigations"></a>Problèmes connus &amp; atténuations des risques

* Le téléchargement de fichiers d’objets blob volumineux ne fonctionne pas correctement, nous vous recommandons d’utiliser AzCopy pendant que nous résolvons ce problème 
* Informations d’identification de compte ne seront pas récupérées ni mis en cache si le dossier de base hello est introuvable ou ne peut pas être écrit pour
* Si nous sommes Ajout, modification ou l’importation d’une entité qui a une propriété avec une valeur numérique ambiguë, comme « 1 » ou « 1.0 », et l’utilisateur de hello tente toosend comme un `Edm.String`, valeur de hello reviendra via le client hello API comme un Edm.Double
* Lors de l’importation de fichiers CSV avec des enregistrements multilignes, les données de salutation peuvent obtenir coupées ou brouillées

02/03/2016

### <a name="version-07201601291"></a>Version 0.7.20160129.1

#### <a name="fixes"></a>Correctifs

* Amélioration des performances globales lors du chargement, du téléchargement et de la copie des objets blob

01/14/2016

### <a name="version-07201601050"></a>Version 0.7.20160105.0

#### <a name="new"></a>Nouveau

* Prise en charge de Linux (tooOSX de fonctionnalités de parité)
* Ajouter des conteneurs d’objets blob avec une clé Signatures d’accès partagé (SAP)
* Ajouter des comptes de stockage Azure Chine
* Ajouter des comptes de stockage avec des points de terminaison personnalisés
* Ouvrir et consulter les BLOB hello contenu texte et image
* Affichez et modifiez les propriétés et métadonnées des blobs

#### <a name="fixes"></a>Correctifs

* Fixe : chargement ou téléchargement un grand nombre d’objets BLOB (500) peut parfois provoquer hello application toohave un écran blanc 
* Problème résolu : lors de la définition de niveau accès public du conteneur d’objets blob, nouvelle valeur de hello n'est pas mis à jour tant que vous définissez nouveau hello de se concentrer sur le conteneur de hello. En outre, boîte de dialogue hello toujours par défaut est trop « n’accès aucun public » et non hello actuelle de valeur réelle.
* Une meilleure prise en charge globale du clavier/accessibilité et de l’interface utilisateur
* Le texte de l’historique des vues miniatures est encapsulé lorsqu’il est long avec un espace blanc
* La boîte de dialogue SAP prend en charge la validation d’entrée
* Stockage local continue toobe disponible, même si les informations d’identification de l’utilisateur ont expiré
* Lorsqu’un conteneur d’objets blob ouvert est supprimé, l’Explorateur d’objets blob hello sur droite hello est fermé

#### <a name="known-issues"></a>Problèmes connus

* Besoins d’installation Linux gcc version mise à jour ou mise à niveau – tooupgrade d’étapes sont répertoriées ci-dessous : 
    * `sudo add-apt-repository ppa:ubuntu-toolchain-r/test`
    * `sudo apt-get update`
    * `sudo apt-get upgrade`
    * `sudo apt-get dist-upgrade`

11/18/2015
### <a name="version-07201511160"></a>Version 0.7.20151116.0

#### <a name="new"></a>Nouveau

* Versions macOS et Windows
* Connecter vos comptes de stockage tooview : utiliser votre compte professionnels Microsoft Account, 2FA, etc..
* Stockage de développement local (utilisez l’émulateur de stockage, Windows uniquement)
* Prise en charge d’Azure Resource Manager et des ressources classiques
* Créez et supprimez des objets blob, des files d’attente ou des tables
* Recherchez des objets blob, des files d’attente ou des tables spécifiques
* Explorer le contenu de hello de conteneurs d’objets blob
* Affichez et parcourez les répertoires
* Chargez, téléchargez et supprimez des objets blob et des dossiers
* Affichez et modifiez les propriétés et métadonnées des blobs
* Générez des clés SAP
* Gérez et créez des stratégies d’accès stockés (SAS)
* Recherchez les blobs par préfixe
* Faites glisser et déplacer tooupload de fichiers ou de téléchargement

#### <a name="known-issues"></a>Problèmes connus

* Lorsque vous définissez le niveau accès public du conteneur d’objets blob, nouvelle valeur de hello n’est pas mis à jour tant que vous définissez nouveau hello de se concentrer sur le conteneur de hello
* Lorsque vous ouvrez le niveau d’accès public hello dialogue tooset hello, il n’affiche toujours « Aucun accès public » comme valeur par défaut de hello et non hello actuelle de valeur réelle
* Impossible de renommer des objets blob téléchargés
* Entrées de journal d’activité est parfois « coincés » dans un en cours d’état lorsqu’une erreur se produit et hello erreur n’apparaît pas
* Parfois les pannes ou désactive complètement blanc lors de la tentative de tooupload ou téléchargez un grand nombre d’objets BLOB
* Parfois, l’annulation d’une opération de copie ne fonctionne pas
* Au cours de la création d’un conteneur (table/file d’attente/blob), si vous entrez un nom non valide et que vous passez toocreate une autre sous un type de conteneur différents Impossible de définir le focus sur le nouveau type de hello
* Impossible de créer un nouveau dossier ou de renommer un dossier




[2]: https://support.microsoft.com/en-us/help/4021389/storage-explorer-troubleshooting-guide
[3]: vs-azure-tools-storage-manage-with-storage-explorer.md