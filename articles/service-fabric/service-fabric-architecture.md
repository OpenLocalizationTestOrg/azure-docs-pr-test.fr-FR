---
title: "aaaArchitecture d’Azure Service Fabric | Documents Microsoft"
description: "Service Fabric est qu'une plateforme de systèmes distribués utilisé toobuild évolutive, fiable et facile à gérer les applications de cloud de hello. Cet article explique l’architecture hello de Service Fabric."
services: service-fabric
documentationcenter: .net
author: rishirsinha
manager: timlt
editor: rishirsinha
ms.assetid: 6b554243-70cb-4c22-9b28-1a8b4703f45e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/19/2017
ms.author: rsinha
ms.openlocfilehash: 0268578094ad1a0010ef44ed940f828b985f6c40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-architecture"></a>Architecture de Service Fabric
Service Fabric est constitué de sous-systèmes en couches. Ces sous-systèmes activer toowrite les applications qui sont :

* Haute disponibilité
* Extensibilité
* Facilité de gestion
* Testable

Hello suivant schéma montre hello principaux sous-systèmes de l’infrastructure de Service.

![Diagramme de l’architecture de Service Fabric](media/service-fabric-architecture/service-fabric-architecture.png)

Dans un système distribué, hello capacité toosecurely communiquer entre les nœuds dans un cluster est essentiel. Base de pile de hello hello est sous-système de transport hello, qui fournit une communication sécurisée entre les nœuds. Au-dessus de transport de hello sous-système réside sous-système de fédération hello, les clusters hello différents nœuds dans une seule entité (nommée clusters) afin que le Service Fabric peut détecter les défaillances, effectuer élection du chef et fournir un routage cohérent. sous-système de fiabilité Hello, la couche supérieure de sous-système de fédération hello, est responsable de la fiabilité de hello des services de Fabric de Service via des mécanismes tels que la réplication, la gestion des ressources et le basculement. sous-système de fédération Hello sous-jacente également hello hébergement et activation sous-système qui gère les hello du cycle de vie d’une application sur un nœud unique. sous-système de gestion Hello gère hello du cycle de vie des applications et services. sous-système de testabilité Hello permet aux développeurs d’applications de tester leurs services via des erreurs simulés avant et après le déploiement d’environnements de tooproduction des applications et services. Service Fabric permet hello tooresolve les emplacements de service via son sous-système de communication. Bonjour les modèles de programmation d’application exposés toodevelopers sont superposées ces sous-systèmes ainsi que les outils de tooenable modèle hello application.

## <a name="transport-subsystem"></a>Sous-système de transport
sous-système de transport Hello implémente un canal de communication point à point datagramme. Ce canal est utilisé pour la communication au sein des clusters de l’infrastructure de service et la communication entre les clients et le cluster hello service fabric. Il prend en charge unidirectionnel et modèles de communication demande-réponse, qui fournit la base de hello pour l’implémentation de diffusion et la multidiffusion dans hello couche de fédération. sous-système de transport Hello sécurise les communications à l’aide de X509 certificats ou la sécurité Windows. Ce sous-système est utilisé en interne par l’infrastructure de Service et n’est pas directement accessible toodevelopers pour la programmation d’applications.

## <a name="federation-subsystem"></a>Sous-système de fédération
Dans l’ordre des tooreason sur un ensemble de nœuds dans un système distribué, vous devez toohave une vue cohérente de système de hello. sous-système de fédération Hello utilise des primitives de communication hello fournies par le sous-système de transport hello et mailles hello différents nœuds dans un cluster d’unifié unique, il peut analyser. Il fournit des primitives de systèmes distribué de hello nécessitent par hello autres sous-systèmes - détection de défaillance, élection du chef et cohérent de routage. sous-système de fédération Hello repose sur des tables de hachage distribuée avec un espace de jeton de 128 bits. sous-système de Hello crée une topologie en anneau sur les nœuds hello, chaque nœud dans l’anneau hello alloué un sous-ensemble de l’espace de jeton hello pour la propriété. Pour la détection de défaillance, couche de hello utilise un mécanisme de bail en fonction de cœur battre et arbitrage. sous-système de fédération Hello garantit également que via les protocoles de départ uniquement un seul propriétaire d’un jeton existant à tout moment et de jointure complexe. Cela fournit des garanties de choix d’instance responsable et de routage cohérent.

## <a name="reliability-subsystem"></a>Sous-système de fiabilité
état de hello hello mécanisme toomake d’un service Service Fabric hautement disponible via l’utilisation de hello de hello fournit Hello sous-système de fiabilité *Replicator*, *Gestionnaire de basculement*, et  *Équilibrage des ressources*.

* Hello réplicateur garantit que les modifications d’état dans le réplica de service principal hello seront automatiquement répliquées toosecondary réplicas, maintenir la cohérence entre les réplicas principal et secondaire de hello dans un jeu de réplicas de service. Réplicateur de Hello est responsable de la gestion de quorum de réplicas hello dans le jeu de réplicas hello. Il interagit avec hello basculement tooget hello liste des opérations tooreplicate, et l’agent de reconfiguration hello lui fournit configuration hello hello du jeu de réplicas. Cette configuration indique les opérations de hello réplicas doivent toobe répliquée. L’infrastructure de service fournit un réplicateur par défaut appelé réplicateur Fabric, ce qui peut être utilisé par hello programmation modèle API toomake hello état du service hautement disponible et fiable.
* Hello Gestionnaire de basculement garantit que lorsque les nœuds sont ajoutés tooor supprimé hello cluster, hello charge est automatiquement redistribuée entre les nœuds disponibles hello. Si un nœud de cluster de hello échoue, le cluster de hello va reconfigurer automatiquement disponibilité toomaintain réplicas du service de hello.
* Hello Gestionnaire de ressources place les réplicas de service de domaine de défaillance de cluster de hello et garantit que toutes les unités de basculement sont opérationnelles. Hello Gestionnaire de ressources équilibre également les ressources de service sur hello sous-jacent pool partagé de distribution de cluster nœuds tooachieve charge uniforme optimale.

## <a name="management-subsystem"></a>Sous-système de gestion
sous-système de gestion Hello fournit des services de bout en bout et la gestion du cycle de vie des applications. Les API d’administration et les applets de commande PowerShell vous tooprovision, déployer, correctif, mise à niveau et annuler la configuration des applications sans perte de disponibilité. sous-système de gestion Hello effectue cela via hello suivant des services.

* **Le Gestionnaire du cluster**: il s’agit hello service principal qui interagit avec hello Gestionnaire de basculement à partir d’applications de hello fiabilité tooplace sur les nœuds hello basés sur les contraintes de placement du service hello. Hello Gestionnaire de ressources dans le sous-système de basculement garantit que les contraintes hello ne sont jamais interrompues. le Gestionnaire du cluster Hello gère hello du cycle de vie des applications de hello à disposition toode-disposition. Il s’intègre à tooensure de gestionnaire de contrôle d’intégrité hello que la disponibilité des applications n’est pas perdue à partir d’un point de vue sémantique d’intégrité au cours des mises à niveau.
* **Gestionnaire d’intégrité**: ce service permet la surveillance de l’intégrité des applications, des services et des entités du cluster. Les entités de cluster (par exemple, les nœuds, les partitions de service et les réplicas) peuvent signaler des informations de contrôle d’intégrité, qui sont regroupées en magasin de contrôle d’intégrité centralisée hello. Ces informations d’intégrité fournissent un instantané de la santé globale dans le temps de services de hello et nœuds répartis sur plusieurs nœuds de cluster hello, ce qui vous tootake les actions correctives nécessaires. Requête d’intégrité Qu'api permettent d’événements de contrôle d’intégrité tooquery hello signalé sous-système de contrôle d’intégrité toohello. API de requête de contrôle d’intégrité Hello retourner du magasin de données brutes d’intégrité de hello stockées dans le contrôle d’intégrité hello ou hello agrégées, interpréter les données de contrôle d’intégrité pour une entité spécifique du cluster.
* **Magasin d’images**: ce service fournit le stockage et la distribution de hello fichiers binaires d’application. Ce service fournit un magasin de fichiers distribués simple où les applications de hello sont téléchargée tooand téléchargé à partir de.

## <a name="hosting-subsystem"></a>Sous-système d'hébergement
le Gestionnaire du cluster Hello informe hello hébergement sous-système (en cours d’exécution sur chaque nœud), les services qu’il a besoin de toomanage pour un nœud particulier. Hello hébergement sous-système puis gère hello du cycle de vie de l’application hello sur ce nœud. Il interagit avec hello la fiabilité et l’intégrité des composants tooensure que les réplicas hello sont correctement placées et fonctionnent correctement.

## <a name="communication-subsystem"></a>Sous-système de communication
Ce sous-système fournit une messagerie fiable au sein de la détection de cluster et le service hello via le service d’affectation de noms de hello. Hello Naming service résout l’emplacement de tooa de noms de service dans un cluster de hello et permet les propriétés et les noms de service toomanage les utilisateurs. À l’aide du service d’affectation de noms de hello, les clients peuvent en toute sécurité communiquer avec n’importe quel nœud hello cluster tooresolve un nom de service et de récupérer les métadonnées de service. À l’aide d’un API simple d’affectation de noms client, les utilisateurs de l’infrastructure de Service peuvent développer des services et clients capables de résoudre l’emplacement réseau actuel de hello en dépit de dynamisme de nœud ou de dimensionnement nouveau du cluster de hello hello.

## <a name="testability-subsystem"></a>Sous-système de testabilité
La testabilité est une suite d'outils conçus spécifiquement pour tester les services créés sur la plateforme Service Fabric. Hello outils permettent à un développeur facilement induire des erreurs significatives tooexercise de scénarios de test et exécutez valider hello de nombreux États et transitions qui subissent un service tout au long de sa durée de vie, tous les de manière contrôlée et sans échec. Testabilité fournit également un mécanisme toorun des tests plus longue durée qui peuvent itérer dans diverses défaillances possible sans perte de disponibilité. Vous bénéficiez ainsi d’un environnement de test en production.

