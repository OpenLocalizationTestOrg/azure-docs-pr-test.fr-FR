---
title: "Vue d’ensemble des modèles de programmation Service Fabric | Microsoft Docs"
description: "Service Fabric propose deux infrastructures pour la création de services : l’infrastructure d’acteurs et l’infrastructure de services. Elles offrent des compromis distincts en termes de simplicité et de contrôle."
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
ms.openlocfilehash: ca36f42897cd44d6da1a3cb6db53f656cf6256ee
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2017
---
# <a name="service-fabric-programming-model-overview"></a>Vue d’ensemble des modèles de programmation Service Fabric
Service Fabric offre plusieurs méthodes pour écrire et gérer vos services. Les services peuvent choisir d’utiliser les API de Service Fabric pour tirer pleinement parti des infrastructures d’application et des fonctionnalités de la plateforme. Les services peuvent être n’importe quel programme exécutable compilé, écrit dans n’importe quel langage ou code exécuté dans un conteneur simplement hébergé sur un cluster Service Fabric.

## <a name="guest-executables"></a>Exécutables invités
Un [exécutable invité](service-fabric-deploy-existing-app.md) désigne un exécutable existant quelconque (écrit dans n’importe quel langage) qui peut être exécuté en tant que service dans votre application. Les exécutables invités n’appellent pas directement les API du SDK Service Fabric. Cependant, ils bénéficient toujours des fonctionnalités offertes par la plateforme, comme la détectabilité des services ainsi que la création de rapports d’intégrité et de chargement personnalisés par le biais d’un appel aux API REST exposées par Service Fabric. Ils prennent également en charge le cycle de vie complet des applications.

Familiarisez-vous avec les exécutables invités en déployant votre première [application d’exécutable invité](service-fabric-deploy-existing-app.md).

## <a name="containers"></a>Conteneurs
Par défaut, Service Fabric déploie et active les services en tant que processus. Service Fabric permet également de déployer les services dans des [conteneurs](service-fabric-containers-overview.md). Service Fabric prend en charge le déploiement de conteneurs Linux et de conteneurs Windows sur Windows Server 2016. Les images conteneur peuvent être extraites d’un référentiel de conteneur et déployées vers la machine. Vous pouvez déployer des applications existantes en tant qu’exécutables invités, services Service Fabric sans état, services Reliable Services avec état ou Reliable Actors dans des conteneurs. Vous pouvez aussi combiner des services de processus et services de conteneur dans la même application.

[En savoir plus sur la conteneurisation de vos services dans Windows ou Linux](service-fabric-deploy-container.md)

## <a name="reliable-services"></a>Services fiables (Reliable Services)
Reliable Services est une infrastructure légère d'écriture de services qui s'intègrent à la plateforme Service Fabric et tirent parti de l'ensemble de ses fonctionnalités. Reliable Services fournissent un ensemble minimal d'API qui permettent au runtime Service Fabric de gérer le cycle de vie de vos services et permettent à vos services d’interagir avec le runtime. L'infrastructure d'application est minime, ce qui vous donne un contrôle total sur les choix de conception et d'implémentation. Elle peut être utilisée pour héberger une autre infrastructure d'application, par exemple ASP.NET Core.

Reliable Services peut être sans état, comme la plupart des plateformes de service, comme les serveurs web, dans lesquels toutes les instances du service sont égales et l’état est conservé dans une solution externe, telle que la base de données Azure ou Azure Table Storage.

Reliable Services peut également être avec état, ce qui est propre à Service Fabric, où l’état est conservé directement dans le service lui-même à l'aide de Reliable Collections. L’état est hautement disponible grâce à la réplication et distribué grâce au partitionnement, l’ensemble étant géré automatiquement par Service Fabric.

[En savoir plus sur Reliable Services](service-fabric-reliable-services-introduction.md) ou commencez par [écrire votre premier service Reliable Services](service-fabric-reliable-services-quick-start.md).

## <a name="reliable-actors"></a>Acteurs fiables (Reliable Actors)
Reposant sur Reliable Services, l'infrastructure Reliable Actor est une infrastructure d'application qui implémente le modèle Reliable Actor, selon le modèle de conception des acteurs. L'infrastructure Reliable Actor utilise des unités indépendantes d'état et de calcul avec exécution monothread, nommées acteurs. L'infrastructure Reliable Actor fournit une communication intégrée aux acteurs, ainsi que des configurations prédéfinies de persistance d’état et de montée en charge.

Étant donné que Reliable Actors lui-même est une infrastructure d'application conçue sur Reliable Services, il est entièrement intégré à la plateforme Service Fabric et bénéficie de l'ensemble complet des fonctionnalités offertes par la plateforme.

[En savoir plus sur Reliable Actors](service-fabric-reliable-actors-introduction.md) ou commencez par [écrire votre premier service Reliable Actors](service-fabric-reliable-actors-get-started.md).

## <a name="aspnet-core"></a>ASP.NET Core
Service Fabric s’intègre dans [ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md) pour la création de services Web et API dans votre application. 

[Créer un service frontal à l’aide d’ASP.NET Core](service-fabric-add-a-web-frontend.md)

## <a name="next-steps"></a>Étapes suivantes
[Vue d’ensemble de Service Fabric et des conteneurs](service-fabric-containers-overview.md)

[Présentation de Reliable Services](service-fabric-reliable-services-introduction.md)

[Présentation de Reliable Services](service-fabric-reliable-actors-introduction.md)

[ASP.NET Core et Service Fabric ](service-fabric-reliable-services-communication-aspnetcore.md)




