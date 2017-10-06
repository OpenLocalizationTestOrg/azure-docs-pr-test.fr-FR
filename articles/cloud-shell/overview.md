---
title: "vue d’ensemble du Cloud Shell (version préliminaire) aaaAzure | Documents Microsoft"
description: "Vue d’ensemble de hello Azure Cloud Shell."
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
ms.date: 07/10/2017
ms.author: juluk
ms.openlocfilehash: 45c6c85b167a90947a333f44a9186e2c01b4fa7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-cloud-shell-preview"></a>Vue d’ensemble d’Azure Cloud Shell (version préliminaire)
Azure Cloud Shell est un shell interactif, accessible par navigateur pour la gestion des ressources Azure.

![](media/overview-pic.png)

## <a name="features"></a>Caractéristiques
### <a name="browser-based-shell-experience"></a>Expérience shell basée sur navigateur
Interpréteur de commandes permet l’accès tooa basée sur navigateur de ligne de commande expérience générée à l’aide des tâches de gestion Azure à l’esprit le cloud. Tirer parti de toowork Cloud Shell disposerez à partir d’un ordinateur local de façon uniquement des cloud hello peut fournir.

### <a name="pre-configured-azure-workstation"></a>Station de travail Azure préconfigurée
Cloud Shell est préinstallé avec des outils de ligne de commande et la prise en charge de langages populaires afin de pouvoir travailler plus rapidement.

[Hello complète d’outils liste d’affichage pour Azure Cloud Shell ici.](features.md#tools)

### <a name="automatic-authentication"></a>Authentification automatique
Interpréteur de commandes de nuage en toute sécurité authentifie automatiquement sur chaque session pour les ressources de tooyour accès instantané via hello Azure CLI 2.0.

### <a name="connect-your-azure-file-storage"></a>Connexion à votre stockage de fichiers Azure
Cloud Shell machines sont temporaires et ainsi nécessiter une toobe de partage de fichiers Azure monté en tant que `clouddrive` toopersist votre répertoire $Home.
Au premier lancement Cloud Shell invite toocreate qu'un groupe de ressources, compte de stockage et partage de fichiers à votre place. Il s’agit d’une étape unique, et ces ressources sont automatiquement jointes pour toutes les sessions. 

#### <a name="create-new-storage"></a>Créer un stockage
![](media/basic-storage.png)

Un compte de stockage localement redondant (LRS) peut être créé en votre nom avec un partage de fichiers Azure contenant une image de disque de 5 Go par défaut. partage de fichiers Hello monte comme `clouddrive` pour le fichier partagent une interaction avec l’image de disque hello en cours toosync utilisé et conserver votre répertoire $Home. Les coûts de stockage standard s’appliquent.

Trois ressources sont créées en votre nom :
1. Groupe de ressources nommé : `cloud-shell-storage-<region>`
2. Compte de stockage nommé : `cs<uniqueGuid>`
3. Partage de fichiers nommé : `cs-<user>-<domain>-com-uniqueGuid`

> [!Note]
> Tous les fichiers figurant dans votre répertoire $Home, tels que les clés SSH, sont conservés dans l’image de disque utilisateur stockée dans votre partage de fichiers monté. Appliquez les meilleures pratiques lors de l’enregistrement des fichiers dans votre répertoire $Home et le partage de fichiers monté.

#### <a name="use-existing-resources"></a>Utiliser les ressources existantes
![](media/advanced-storage.png)

Une option avancée est également autoriser vous tooassociate existant ressources tooCloud Shell. Présenté avec l’invite de commandes d’installation de stockage hello, cliquez sur « Paramètres Show advanced » tooselect des options supplémentaires. Les listes déroulantes sont filtrées pour la région Cloud Shell qui vous a été attribuée et pour les comptes de stockage localement/globalement redondant.

[Découvrez le stockage Cloud Shell, la mise à jour des partages de fichiers et le chargement/téléchargement de fichiers.] (persisting-shell-storage.md)

## <a name="concepts"></a>Concepts
* Cloud Shell s’exécute sur une machine temporaire fournie par session et par utilisateur
* Cloud Shell expire après 20 minutes sans activité interactive
* Cloud Shell est accessible uniquement avec un partage de fichiers attaché
* Cloud Shell est affecté à une machine par compte d’utilisateur
* Les autorisations sont définies en tant qu’utilisateur Linux standard

[Découvrez-en davantage sur toutes les fonctionnalités de Cloud Shell.](features.md)

## <a name="examples"></a>Exemples
* Créer ou modifier des scripts tooautomate gestion Azure
* Gérer simultanément des ressources via le portail Azure et Azure CLI 2.0
* Essayer Azure CLI 2.0

[Essayer tous ces exemples au démarrage rapide du Cloud Shell hello.](quickstart.md)

## <a name="pricing"></a>Tarification
ordinateur Hello Shell de Cloud d’hébergement est libre, avec un composant requis d’un fichier Azure monté partager toopersist votre répertoire $Home. Les coûts de stockage standard s’appliquent.

## <a name="supported-browsers"></a>Navigateurs pris en charge
Cloud Shell est recommandé pour Chrome, Safari et Edge. Interface de Cloud est pris en charge de Chrome, Firefox, Safari, Internet Explorer et session, interpréteur de commandes de Cloud est paramètres du navigateur toospecific sujet.

## <a name="troubleshooting"></a>Résolution des problèmes
1. Lorsque vous utilisez un abonnement Azure Active Directory, je ne peux pas créer de stockage tooError échéance : DisallowedOperation 400. tooresolve, veuillez utiliser un abonnement Azure capable de créer des ressources de stockage. Les abonnements AD est des ressources Azure n’a pas pu toocreate.

Pour connaître les limitations spécifiques connues, consultez les [limitations de Cloud Shell](limitations.md).
