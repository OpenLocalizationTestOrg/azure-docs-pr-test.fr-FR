---
title: "aaaExample procédure pas à pas de Azure Infrastructure | Documents Microsoft"
description: "Découvrez hello clé conception et implémentation des recommandations pour le déploiement d’une infrastructure d’exemple dans Azure."
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 281fc2c0-b533-45fa-81a3-728c0049c73d
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b6b307c0112203aa83e1fada81966fc265397a40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="example-azure-infrastructure-walkthrough-for-linux-vms"></a>Procédure pas à pas d’exemple d’infrastructure Azure pour les machines virtuelles Linux

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

Cet article vous guide à travers la création d’un exemple d’infrastructure d’application. Nous avons décrit en détail la conception d’une infrastructure pour un magasin en ligne simple qui réunit toutes les décisions concernant les conventions d’affectation de noms, des groupes à haute disponibilité, des réseaux virtuels et des équilibreurs de charge et les recommandations de hello et déployer vos machines virtuelles (VM).

## <a name="example-workload"></a>Exemple de charge de travail
Adventure Works Cycles veut toobuild une application de magasin en ligne dans Azure se compose de :

* Deux serveurs nginx client hello frontal dans une couche web en cours d’exécution
* Deux serveurs nginx pour le traitement des données et des commandes dans une couche d’application
* Deux serveurs MongoDB faisant partie d’un cluster partitionné pour le stockage des données sur les produits et des commandes dans une couche de base de données
* Deux contrôleurs de domaine Active Directory pour les comptes clients et les fournisseurs dans une couche d’authentification
* Tous les serveurs hello se trouvent dans deux sous-réseaux :
  * un sous-réseau frontal pour les serveurs web de hello 
  * un sous-réseau principal pour les serveurs d’applications hello, MongoDB cluster et les contrôleurs de domaine

![Diagramme de différentes couches pour l’infrastructure d’applications](./media/infrastructure-example/example-tiers.png)

Entrant sécuriser le trafic web doit être équilibrée entre les serveurs web de hello clients parcourir la Boutique en ligne hello. Le trafic à l’écran hello du serveur proxy de traitement de la commande demande à partir du web hello serveurs doivent être équilibrée entre les serveurs d’application hello. En outre, l’infrastructure de hello doit être conçue pour la haute disponibilité.

conception de résultant Hello doit intégrer :

* Un compte et un abonnement Azure
* un seul groupe de ressources.
* Azure Managed Disks
* un réseau virtuel avec deux sous-réseaux ;
* Haute disponibilité pour hello machines virtuelles avec un rôle similaire
* Machines virtuelles

Tous les hello ci-dessus suivre les conventions d’affectation de noms :

* Adventure Works Cycles utilise **[Charge de travail informatique]-[Emplacement]-[Ressources Azure]** comme préfixe
  * Pour cet exemple, «**azos**» (magasin d’Azure en ligne) est hello nom de la charge de travail informatique et «**utiliser**» (est des États-Unis 2) est l’emplacement de hello
* Les réseaux virtuels utilisent AZOS-USE-VN**[numéro]**
* Les groupes à haute disponibilité utilisent azos-use-as-**[rôle]**
* Les noms de machine virtuelle utilisent azos-use-vm-**[nom de machine virtuelle]**

## <a name="azure-subscriptions-and-accounts"></a>Abonnements et comptes Azure
Adventure Works Cycles est à l’aide de leur abonnement Enterprise, nommé abonnement d’entreprise Adventure Works, tooprovide de facturation pour cette charge de travail informatique.

## <a name="storage"></a>Storage
Adventure Works Cycles a déterminé que des disques managés Azure doivent être utilisés. Lors de la création de machines virtuelles, les deux niveaux de stockage disponibles sont utilisés :

* **Stockage standard** pour les serveurs web de hello, les serveurs d’applications et les contrôleurs de domaine et leurs disques de données.
* **Stockage Premium** pour les serveurs en cluster partitionnée MongoDB hello et leurs disques de données.

## <a name="virtual-network-and-subnets"></a>Réseau virtuel et sous-réseaux
Car le réseau virtuel de hello ne doit pas de réseau local de connectivité en cours toohello Cycles de travail Adventure, ils ont choisi un réseau virtuel cloud uniquement.

Ils créé un réseau virtuel cloud uniquement avec hello suivant les paramètres à l’aide de hello portail Azure :

* Nom : AZOS-USE-VN01
* Emplacement : East US 2
* Espace d’adressage du réseau virtuel : 10.0.0.0/8
* Premier sous-réseau :
  * Nom : FrontEnd
  * Espace d’adressage : 10.0.1.0/24
* Second sous-réseau :
  * Nom : BackEnd
  * Espace d’adressage : 10.0.2.0/24

## <a name="availability-sets"></a>Groupes à haute disponibilité
toomaintain haute disponibilité de toutes les quatre niveaux de leur magasin en ligne, Adventure Works Cycles décidé sur quatre groupes à haute disponibilité :

* **Utilisez azos comme web** pour les serveurs web de hello
* **Utilisez azos en tant qu’application** des serveurs d’applications hello
* **Utilisez azos en tant que db** pour serveurs hello cluster partitionnée de hello MongoDB
* **Utilisez azos comme dc** hello des contrôleurs de domaine

## <a name="virtual-machines"></a>Machines virtuelles
Adventure Works Cycles choisi hello suivant des noms pour leurs machines virtuelles Azure :

* **azos-utilisation-vm-web01** pour le premier serveur web de hello
* **azos-utilisation-vm-web02** pour le second serveur web de hello
* **azos-utilisation-vm-app01** hello premier serveur d’applications
* **azos-utilisation-vm-app02** hello deuxième serveur d’applications
* **azos-utilisation-vm-db01** pour hello première MongoDB serveur hello cluster
* **azos-utilisation-vm-BD02** pour hello deuxième MongoDB serveur hello cluster
* **azos-utilisation-vm-dc01** hello premier contrôleur de domaine
* **azos-utilisation-vm-dc02** hello deuxième contrôleur de domaine

Voici la configuration obtenue de hello.

![Infrastructure d’applications finale déployée dans Azure](./media/infrastructure-example/example-config.png)

Cette configuration comprend :

* un réseau virtuel cloud avec deux sous-réseaux (FrontEnd et BackEnd) ;
* des disques managés Azure utilisant à la fois des disques Standard et Premium
* Quatre groupes à haute disponibilité, une pour chaque niveau de la Boutique en ligne hello
* machines virtuelles de Hello pour les couches de hello quatre
* Un jeu d’équilibrage de charge externe pour le trafic web basé sur HTTPS à partir de serveurs web de hello Internet toohello
* Un jeu pour le trafic non chiffré web à partir de serveurs d’applications toohello hello web serveurs d’équilibrage interne
* un seul groupe de ressources.
