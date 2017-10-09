---
title: "Présentation du modèle programmation aaaService Fabric | Documents Microsoft"
description: "L’infrastructure de service propose deux infrastructures pour construire des services : hello framework d’acteur et infrastructure de services hello. Elles offrent des compromis distincts en termes de simplicité et de contrôle."
services: service-fabric
documentationcenter: .net
author: seanmck
manager: timlt
editor: vturecek
ms.assetid: 974b2614-014e-4587-a947-28fcef28b382
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/02/2017
ms.author: vturecek
ms.openlocfilehash: b48af2a7b41935bdf0e4594c765f363e520c254e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-programming-model-overview"></a>Vue d’ensemble des modèles de programmation Service Fabric
Service Fabric offre plusieurs façons toowrite et gérer vos services. Services peuvent choisir toouse hello Service Fabric API tootake pleinement parti des fonctionnalités de plateforme hello et les infrastructures d’application. Les services peuvent être n’importe quel programme exécutable compilé, écrit dans n’importe quel langage ou code exécuté dans un conteneur simplement hébergé sur un cluster Service Fabric.

## <a name="guest-executables"></a>Exécutables invités
Un [exécutable invité](service-fabric-deploy-existing-app.md) désigne un exécutable existant quelconque (écrit dans n’importe quel langage) qui peut être exécuté en tant que service dans votre application. Les exécutables invité n’appellent pas directement hello API du Kit de développement logiciel Service Fabric. Cependant ils bénéficient toujours de plateforme hello de fonctionnalités offre, telles que la détectabilité de service, l’intégrité personnalisée et charge la création de rapports en appelant l’API REST exposées par le Service Fabric. Ils prennent également en charge le cycle de vie complet des applications.

Familiarisez-vous avec les exécutables invités en déployant votre première [application d’exécutable invité](service-fabric-deploy-existing-app.md).

## <a name="containers"></a>Conteneurs
Par défaut, Service Fabric déploie et active les services en tant que processus. Service Fabric permet également de déployer les services dans des [conteneurs](service-fabric-containers-overview.md). Service Fabric prend en charge le déploiement de conteneurs Linux et de conteneurs Windows sur Windows Server 2016. Les images de conteneur peuvent être extraites d’un référentiel de conteneur et déploiement toohello ordinateur. Vous pouvez déployer des applications existantes en tant qu’invité exectuables, l’infrastructure de Service sans état ou avec état fiable services ou Reliable Actors dans des conteneurs et vous peuvent combiner des services dans les processus et services dans des conteneurs hello même application.

[En savoir plus sur la conteneurisation de vos services dans Windows ou Linux](service-fabric-deploy-container.md)

## <a name="reliable-services"></a>Services fiables (Reliable Services)
Services fiables est une infrastructure de léger pour l’écriture de services qui s’intègrent avec la plateforme de Service Fabric hello et tirer parti de l’ensemble hello des fonctionnalités de plateforme. Services fiables fournissent un ensemble minimal d’API qui permettent de hello Service Fabric runtime toomanage hello du cycle de vie de vos services et autorisent votre toointeract services avec hello runtime. infrastructure d’application Hello est minime, ce qui vous complète contrôler le choix de conception et d’implémentation, et peut être utilisé toohost n’importe quel autre infrastructure d’application, telles que ASP.NET Core.

Services fiables peuvent être toomost sans état, comme les plateformes de service, tels que les serveurs web, dans laquelle chaque instance du service de hello est égales et état est rendu persistant dans une solution externe, telles que la base de données Azure ou le stockage de Table Azure.

Services fiables peuvent également être tooService avec état, exclusif Fabric, où l’état est persistant directement dans le service hello lui-même à l’aide de Collections fiable. L’état est hautement disponible grâce à la réplication et distribué grâce au partitionnement, l’ensemble étant géré automatiquement par Service Fabric.

[En savoir plus sur Reliable Services](service-fabric-reliable-services-introduction.md) ou commencez par [écrire votre premier service Reliable Services](service-fabric-reliable-services-quick-start.md).

## <a name="reliable-actors"></a>Acteurs fiables (Reliable Actors)
Reposant sur des Services fiables, hello acteur fiable est une application infrastructure qui implémente le modèle Virtual Actor de hello, selon le modèle de conception d’acteur hello. framework d’acteur fiable Hello utilise des unités indépendantes de calcul et l’état avec une exécution monothread acteurs. Hello Reliable Actor offre communication intégrée pour les acteurs et des configurations de persistance et la montée en puissance parallèle état prédéfini.

Comme Reliable Actors lui-même est une infrastructure d’application basée sur les Services fiables, il est entièrement intégré avec la plateforme de Service Fabric hello et les avantages de hello ensemble des fonctionnalités offertes par la plateforme de hello.

[En savoir plus sur Reliable Actors](service-fabric-reliable-actors-introduction.md) ou commencez par [écrire votre premier service Reliable Actors](service-fabric-reliable-actors-get-started.md).

## <a name="aspnet-core"></a>ASP.NET Core
Service Fabric s’intègre dans [ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md) pour la création de services Web et API dans votre application. 

[Créer un service frontal à l’aide d’ASP.NET Core](service-fabric-add-a-web-frontend.md)

## <a name="next-steps"></a>Étapes suivantes
[Vue d’ensemble de Service Fabric et des conteneurs](service-fabric-containers-overview.md)

[Présentation de Reliable Services](service-fabric-reliable-services-introduction.md)

[Présentation de Reliable Services](service-fabric-reliable-actors-introduction.md)

[ASP.NET Core et Service Fabric ](service-fabric-reliable-services-communication-aspnetcore.md)




