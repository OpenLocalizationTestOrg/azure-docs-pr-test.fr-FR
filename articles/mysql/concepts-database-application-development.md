---
title: "vue d’ensemble du développement d’application aaaDatabase pour la base de données Azure pour MySQL | Documents Microsoft"
description: "Présente les considérations de conception un développeur doit suivre lors de l’écriture d’applications code tooconnect tooAzure base de données pour MySQL"
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: f08df605eba21b4ba4b43565c0a7ded95779a171
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="application-development-overview-for-azure-database-for-mysql"></a>Vue d’ensemble du développement d’applications pour la base de données Azure pour MySQL 
Cet article traite des considérations de conception, un développeur doit suivre lors de l’écriture d’applications code tooconnect tooAzure base de données pour MySQL 

> [!TIP]
> Pour un didacticiel montrant vous comment toocreate un serveur, créer un pare-feu basé sur le serveur, affichez les propriétés du serveur, créez la base de données, vous connecter et interrogez à l’aide de banc d’essai et mysql.exe, consultez [concevoir votre première base de données MySQL de Azure](tutorial-design-database-using-portal.md)

## <a name="language-and-platform"></a>Langage et plateforme
Plusieurs exemples de code sont à votre disposition pour divers langages et plateformes de programmation. Vous trouverez des exemples de code toohello à : [les bibliothèques de connectivité permettant tooconnect tooAzure base de données MySQL](concepts-connection-libraries.md)

## <a name="tools"></a>Outils
Base de données Azure pour MySQL utilise hello MySQL version communautaire, compatible avec les outils de gestion courants MySQL tels que les utilitaires de banc d’essai ou MySQL, tels que mysql.exe, [phpMyAdmin](https://www.phpmyadmin.net/), [Navicat](https://www.navicat.com/products/navicat-for-mysql)et d’autres. Vous pouvez également utiliser les API REST toointeract hello portail Azure et CLI d’Azure avec le service de base de données hello.

## <a name="resource-limitations"></a>Limitations des ressources
Base de données MySQL Azure gère hello ressources disponibles tooa server à l’aide de deux mécanismes différents : 
- gouvernance des ressources ; 
- application des limites.

## <a name="security"></a>Sécurité
La base de données MySQL Azure fournit des ressources permettant de limiter l’accès, de protéger les données, de configurer les utilisateurs et les rôles et de surveiller les activités sur une base de données MySQL.

## <a name="authentication"></a>Authentification
La base de données MySQL Azure prend en charge l’authentification serveur des utilisateurs et des connexions.

## <a name="resiliency"></a>Résilience
Lorsqu’une erreur temporaire se produit lors de la connexion tooMySQL de base de données, votre code doit réessayer d’appel de hello. Nous vous recommandons d’utilisation de logique de nouvelle tentative hello, la logique d’interruption afin qu’elle ne surchargent pas hello de base de données SQL avec une nouvelle tentative simultanée de plusieurs clients.

- Exemples de code : pour les exemples de code qui illustrent la logique de nouvelle tentative, consultez les exemples pour la langue hello de votre choix à : [les bibliothèques de connectivité permettant tooconnect tooAzure base de données MySQL](concepts-connection-libraries.md)

## <a name="managing-connections"></a>Gestion des connexions
Connexions de base de données sont une ressource limitée, nous vous recommandons d’utilisation pratique de connexions lors de l’accès à votre base de données MySQL tooachieve de meilleur performances.
- Base de données Access hello en utilisant le regroupement de connexions ou des connexions persistantes.
- Base de données Access hello à l’aide de durée de vie courte de connexion. 
- Utilisez une logique de nouvelle tentative dans votre application au point hello de tentative de connexion hello, toocatch les échecs en raison de connexions de tooconcurrent avez atteint le nombre maximal de hello autorisé. Bonjour logique de nouvelle tentative, définir un délai court, puis attendez un délai aléatoire avant les tentatives de connexion supplémentaires hello.
