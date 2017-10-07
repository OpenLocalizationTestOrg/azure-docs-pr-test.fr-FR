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
# <a name="application-development-overview-for-azure-database-for-mysql"></a><span data-ttu-id="a579c-103">Vue d’ensemble du développement d’applications pour la base de données Azure pour MySQL</span><span class="sxs-lookup"><span data-stu-id="a579c-103">Application development overview for Azure Database for MySQL</span></span> 
<span data-ttu-id="a579c-104">Cet article traite des considérations de conception, un développeur doit suivre lors de l’écriture d’applications code tooconnect tooAzure base de données pour MySQL</span><span class="sxs-lookup"><span data-stu-id="a579c-104">This article discusses design considerations that a developer should follow when writing application code tooconnect tooAzure Database for MySQL</span></span> 

> [!TIP]
> <span data-ttu-id="a579c-105">Pour un didacticiel montrant vous comment toocreate un serveur, créer un pare-feu basé sur le serveur, affichez les propriétés du serveur, créez la base de données, vous connecter et interrogez à l’aide de banc d’essai et mysql.exe, consultez [concevoir votre première base de données MySQL de Azure](tutorial-design-database-using-portal.md)</span><span class="sxs-lookup"><span data-stu-id="a579c-105">For a tutorial showing you how toocreate a server, create a server-based firewall, view server properties, create database, connect and query using workbench and mysql.exe, see [Design your first Azure MySQL database](tutorial-design-database-using-portal.md)</span></span>

## <a name="language-and-platform"></a><span data-ttu-id="a579c-106">Langage et plateforme</span><span class="sxs-lookup"><span data-stu-id="a579c-106">Language and platform</span></span>
<span data-ttu-id="a579c-107">Plusieurs exemples de code sont à votre disposition pour divers langages et plateformes de programmation.</span><span class="sxs-lookup"><span data-stu-id="a579c-107">There are code samples available for various programming languages and platforms.</span></span> <span data-ttu-id="a579c-108">Vous trouverez des exemples de code toohello à : [les bibliothèques de connectivité permettant tooconnect tooAzure base de données MySQL](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="a579c-108">You can find links toohello code samples at: [Connectivity libraries used tooconnect tooAzure Database for MySQL](concepts-connection-libraries.md)</span></span>

## <a name="tools"></a><span data-ttu-id="a579c-109">Outils</span><span class="sxs-lookup"><span data-stu-id="a579c-109">Tools</span></span>
<span data-ttu-id="a579c-110">Base de données Azure pour MySQL utilise hello MySQL version communautaire, compatible avec les outils de gestion courants MySQL tels que les utilitaires de banc d’essai ou MySQL, tels que mysql.exe, [phpMyAdmin](https://www.phpmyadmin.net/), [Navicat](https://www.navicat.com/products/navicat-for-mysql)et d’autres.</span><span class="sxs-lookup"><span data-stu-id="a579c-110">Azure Database for MySQL uses hello MySQL community version, compatible with MySQL common management tools such as Workbench or MySQL utilities such as mysql.exe, [phpMyAdmin](https://www.phpmyadmin.net/), [Navicat](https://www.navicat.com/products/navicat-for-mysql), and others.</span></span> <span data-ttu-id="a579c-111">Vous pouvez également utiliser les API REST toointeract hello portail Azure et CLI d’Azure avec le service de base de données hello.</span><span class="sxs-lookup"><span data-stu-id="a579c-111">You can also use hello Azure portal, Azure CLI, and REST APIs toointeract with hello database service.</span></span>

## <a name="resource-limitations"></a><span data-ttu-id="a579c-112">Limitations des ressources</span><span class="sxs-lookup"><span data-stu-id="a579c-112">Resource limitations</span></span>
<span data-ttu-id="a579c-113">Base de données MySQL Azure gère hello ressources disponibles tooa server à l’aide de deux mécanismes différents :</span><span class="sxs-lookup"><span data-stu-id="a579c-113">Azure MySQL Database manages hello resources available tooa server using two different mechanisms:</span></span> 
- <span data-ttu-id="a579c-114">gouvernance des ressources ;</span><span class="sxs-lookup"><span data-stu-id="a579c-114">Resources Governance</span></span> 
- <span data-ttu-id="a579c-115">application des limites.</span><span class="sxs-lookup"><span data-stu-id="a579c-115">Enforcement of Limits.</span></span>

## <a name="security"></a><span data-ttu-id="a579c-116">Sécurité</span><span class="sxs-lookup"><span data-stu-id="a579c-116">Security</span></span>
<span data-ttu-id="a579c-117">La base de données MySQL Azure fournit des ressources permettant de limiter l’accès, de protéger les données, de configurer les utilisateurs et les rôles et de surveiller les activités sur une base de données MySQL.</span><span class="sxs-lookup"><span data-stu-id="a579c-117">Azure MySQL Database provides resources for limiting access, protecting data, configuring users and role, and monitoring activities on a MySQL Database.</span></span>

## <a name="authentication"></a><span data-ttu-id="a579c-118">Authentification</span><span class="sxs-lookup"><span data-stu-id="a579c-118">Authentication</span></span>
<span data-ttu-id="a579c-119">La base de données MySQL Azure prend en charge l’authentification serveur des utilisateurs et des connexions.</span><span class="sxs-lookup"><span data-stu-id="a579c-119">Azure MySQL Database supports server authentication of users and logins.</span></span>

## <a name="resiliency"></a><span data-ttu-id="a579c-120">Résilience</span><span class="sxs-lookup"><span data-stu-id="a579c-120">Resiliency</span></span>
<span data-ttu-id="a579c-121">Lorsqu’une erreur temporaire se produit lors de la connexion tooMySQL de base de données, votre code doit réessayer d’appel de hello.</span><span class="sxs-lookup"><span data-stu-id="a579c-121">When a transient error occurs while connecting tooMySQL Database, your code should retry hello call.</span></span> <span data-ttu-id="a579c-122">Nous vous recommandons d’utilisation de logique de nouvelle tentative hello, la logique d’interruption afin qu’elle ne surchargent pas hello de base de données SQL avec une nouvelle tentative simultanée de plusieurs clients.</span><span class="sxs-lookup"><span data-stu-id="a579c-122">We recommend hello retry logic use back off logic, so that it does not overwhelm hello SQL Database with multiple clients retrying simultaneously.</span></span>

- <span data-ttu-id="a579c-123">Exemples de code : pour les exemples de code qui illustrent la logique de nouvelle tentative, consultez les exemples pour la langue hello de votre choix à : [les bibliothèques de connectivité permettant tooconnect tooAzure base de données MySQL](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="a579c-123">Code samples: For code samples that illustrate retry logic, see samples for hello language of your choice at: [Connectivity libraries used tooconnect tooAzure Database for MySQL](concepts-connection-libraries.md)</span></span>

## <a name="managing-connections"></a><span data-ttu-id="a579c-124">Gestion des connexions</span><span class="sxs-lookup"><span data-stu-id="a579c-124">Managing Connections</span></span>
<span data-ttu-id="a579c-125">Connexions de base de données sont une ressource limitée, nous vous recommandons d’utilisation pratique de connexions lors de l’accès à votre base de données MySQL tooachieve de meilleur performances.</span><span class="sxs-lookup"><span data-stu-id="a579c-125">Database connections are a limited resource, so we recommend sensible use of connections when accessing your MySQL Database tooachieve better performance.</span></span>
- <span data-ttu-id="a579c-126">Base de données Access hello en utilisant le regroupement de connexions ou des connexions persistantes.</span><span class="sxs-lookup"><span data-stu-id="a579c-126">Access hello database by using connection pooling or persistent connections.</span></span>
- <span data-ttu-id="a579c-127">Base de données Access hello à l’aide de durée de vie courte de connexion.</span><span class="sxs-lookup"><span data-stu-id="a579c-127">Access hello database by using short connection life span.</span></span> 
- <span data-ttu-id="a579c-128">Utilisez une logique de nouvelle tentative dans votre application au point hello de tentative de connexion hello, toocatch les échecs en raison de connexions de tooconcurrent avez atteint le nombre maximal de hello autorisé.</span><span class="sxs-lookup"><span data-stu-id="a579c-128">Use retry logic in your application at hello point of hello connection attempt, toocatch failures due tooconcurrent connections have reached hello maximum allowed.</span></span> <span data-ttu-id="a579c-129">Bonjour logique de nouvelle tentative, définir un délai court, puis attendez un délai aléatoire avant les tentatives de connexion supplémentaires hello.</span><span class="sxs-lookup"><span data-stu-id="a579c-129">In hello retry logic, set a short delay, and then wait for a random time before hello additional connection attempts.</span></span>
