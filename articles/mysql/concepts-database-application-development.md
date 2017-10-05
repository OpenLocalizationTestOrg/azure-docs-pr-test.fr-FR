---
title: "Vue d’ensemble du développement d’applications de base de données Azure pour MySQL | Microsoft Docs"
description: "Présente les considérations relatives à la conception que les développeurs doivent suivre pour écrire du code d’application permettant de se connecter à la base de données Azure pour MySQL."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 350dd775e172120d806d1193877a34d94f4d3f6a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="application-development-overview-for-azure-database-for-mysql"></a><span data-ttu-id="4f4a0-103">Vue d’ensemble du développement d’applications pour la base de données Azure pour MySQL</span><span class="sxs-lookup"><span data-stu-id="4f4a0-103">Application development overview for Azure Database for MySQL</span></span> 
<span data-ttu-id="4f4a0-104">Cet article aborde les considérations relatives à la conception que les développeurs doivent suivre pour écrire du code d’application permettant de se connecter à la base de données Azure pour MySQL.</span><span class="sxs-lookup"><span data-stu-id="4f4a0-104">This article discusses design considerations that a developer should follow when writing application code to connect to Azure Database for MySQL</span></span> 

> [!TIP]
> <span data-ttu-id="4f4a0-105">Vous trouverez un didacticiel pour apprendre à créer un serveur, créer un pare-feu sur le serveur, afficher les propriétés du serveur, créer une base de données, se connecter et effectuer des requêtes à l’aide de workbench et de mysql.exe à la page [Concevoir une première base de données Azure MySQL](tutorial-design-database-using-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4f4a0-105">For a tutorial showing you how to create a server, create a server-based firewall, view server properties, create database, connect and query using workbench and mysql.exe, see [Design your first Azure MySQL database](tutorial-design-database-using-portal.md)</span></span>

## <a name="language-and-platform"></a><span data-ttu-id="4f4a0-106">Langage et plateforme</span><span class="sxs-lookup"><span data-stu-id="4f4a0-106">Language and platform</span></span>
<span data-ttu-id="4f4a0-107">Plusieurs exemples de code sont à votre disposition pour divers langages et plateformes de programmation.</span><span class="sxs-lookup"><span data-stu-id="4f4a0-107">There are code samples available for various programming languages and platforms.</span></span> <span data-ttu-id="4f4a0-108">Vous trouverez des liens vers des exemples de code à la page [Bibliothèques de connectivité utilisées pour se connecter à la base de données Azure pour MySQL](concepts-connection-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="4f4a0-108">You can find links to the code samples at: [Connectivity libraries used to connect to Azure Database for MySQL](concepts-connection-libraries.md)</span></span>

## <a name="tools"></a><span data-ttu-id="4f4a0-109">Outils</span><span class="sxs-lookup"><span data-stu-id="4f4a0-109">Tools</span></span>
<span data-ttu-id="4f4a0-110">La base de données Azure pour MySQL utilise la version Community de MySQL, compatible avec les outils de gestion MySQL courants, notamment les utilitaires Workbench et MySQL, par exemple mysql.exe, [phpMyAdmin](https://www.phpmyadmin.net/) ou [Navicat](https://www.navicat.com/products/navicat-for-mysql).</span><span class="sxs-lookup"><span data-stu-id="4f4a0-110">Azure Database for MySQL uses the MySQL community version, compatible with MySQL common management tools such as Workbench or MySQL utilities such as mysql.exe, [phpMyAdmin](https://www.phpmyadmin.net/), [Navicat](https://www.navicat.com/products/navicat-for-mysql), and others.</span></span> <span data-ttu-id="4f4a0-111">Vous pouvez également utiliser le Portail Azure, Azure CLI et les API REST pour interagir avec le service de base de données.</span><span class="sxs-lookup"><span data-stu-id="4f4a0-111">You can also use the Azure portal, Azure CLI, and REST APIs to interact with the database service.</span></span>

## <a name="resource-limitations"></a><span data-ttu-id="4f4a0-112">Limitations des ressources</span><span class="sxs-lookup"><span data-stu-id="4f4a0-112">Resource limitations</span></span>
<span data-ttu-id="4f4a0-113">La base de données Azure MySQL gère les ressources accessibles à un serveur selon deux mécanismes différents :</span><span class="sxs-lookup"><span data-stu-id="4f4a0-113">Azure MySQL Database manages the resources available to a server using two different mechanisms:</span></span> 
- <span data-ttu-id="4f4a0-114">gouvernance des ressources ;</span><span class="sxs-lookup"><span data-stu-id="4f4a0-114">Resources Governance</span></span> 
- <span data-ttu-id="4f4a0-115">application des limites.</span><span class="sxs-lookup"><span data-stu-id="4f4a0-115">Enforcement of Limits.</span></span>

## <a name="security"></a><span data-ttu-id="4f4a0-116">Sécurité</span><span class="sxs-lookup"><span data-stu-id="4f4a0-116">Security</span></span>
<span data-ttu-id="4f4a0-117">La base de données MySQL Azure fournit des ressources permettant de limiter l’accès, de protéger les données, de configurer les utilisateurs et les rôles et de surveiller les activités sur une base de données MySQL.</span><span class="sxs-lookup"><span data-stu-id="4f4a0-117">Azure MySQL Database provides resources for limiting access, protecting data, configuring users and role, and monitoring activities on a MySQL Database.</span></span>

## <a name="authentication"></a><span data-ttu-id="4f4a0-118">Authentification</span><span class="sxs-lookup"><span data-stu-id="4f4a0-118">Authentication</span></span>
<span data-ttu-id="4f4a0-119">La base de données MySQL Azure prend en charge l’authentification serveur des utilisateurs et des connexions.</span><span class="sxs-lookup"><span data-stu-id="4f4a0-119">Azure MySQL Database supports server authentication of users and logins.</span></span>

## <a name="resiliency"></a><span data-ttu-id="4f4a0-120">Résilience</span><span class="sxs-lookup"><span data-stu-id="4f4a0-120">Resiliency</span></span>
<span data-ttu-id="4f4a0-121">Si une erreur temporaire se produit au cours de la connexion à la base de données MySQL, votre code doit effectuer une nouvelle tentative d’appel.</span><span class="sxs-lookup"><span data-stu-id="4f4a0-121">When a transient error occurs while connecting to MySQL Database, your code should retry the call.</span></span> <span data-ttu-id="4f4a0-122">Nous vous recommandons d’utiliser une logique de nouvelle tentative basée sur une logique d’interruption, afin d’éviter que la base de données SQL ne soit inondée de tentatives simultanées de plusieurs clients.</span><span class="sxs-lookup"><span data-stu-id="4f4a0-122">We recommend the retry logic use back off logic, so that it does not overwhelm the SQL Database with multiple clients retrying simultaneously.</span></span>

- <span data-ttu-id="4f4a0-123">Exemples de code : vous trouverez des exemples de code qui illustrent la logique de nouvelle tentative dans le langage de votre choix à la page [Bibliothèques de connectivité utilisées pour se connecter à la base de données Azure pour MySQL](concepts-connection-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="4f4a0-123">Code samples: For code samples that illustrate retry logic, see samples for the language of your choice at: [Connectivity libraries used to connect to Azure Database for MySQL](concepts-connection-libraries.md)</span></span>

## <a name="managing-connections"></a><span data-ttu-id="4f4a0-124">Gestion des connexions</span><span class="sxs-lookup"><span data-stu-id="4f4a0-124">Managing Connections</span></span>
<span data-ttu-id="4f4a0-125">Les connexions de base de données étant une ressource limitée, nous vous recommandons d’en faire un usage raisonnable lorsque vous accédez à votre base de données MySQL, afin d’améliorer les performances.</span><span class="sxs-lookup"><span data-stu-id="4f4a0-125">Database connections are a limited resource, so we recommend sensible use of connections when accessing your MySQL Database to achieve better performance.</span></span>
- <span data-ttu-id="4f4a0-126">Accédez à la base de données en utilisant le regroupement de connexions ou les connexions persistantes.</span><span class="sxs-lookup"><span data-stu-id="4f4a0-126">Access the database by using connection pooling or persistent connections.</span></span>
- <span data-ttu-id="4f4a0-127">Accédez à la base de données sur une courte durée de connexion.</span><span class="sxs-lookup"><span data-stu-id="4f4a0-127">Access the database by using short connection life span.</span></span> 
- <span data-ttu-id="4f4a0-128">Utilisez la logique de nouvelle tentative dans votre application au moment de la tentative de connexion, de façon à intercepter les connexions simultanées qui ont atteint le nombre maximal autorisé.</span><span class="sxs-lookup"><span data-stu-id="4f4a0-128">Use retry logic in your application at the point of the connection attempt, to catch failures due to concurrent connections have reached the maximum allowed.</span></span> <span data-ttu-id="4f4a0-129">Dans cette logique, définissez un délai court et attendez pendant une durée aléatoire avant les autres tentatives de connexion.</span><span class="sxs-lookup"><span data-stu-id="4f4a0-129">In the retry logic, set a short delay, and then wait for a random time before the additional connection attempts.</span></span>