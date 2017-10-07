---
title: "Vue d’ensemble du service de base de données relationnelle d’Azure Database pour MySQL | Microsoft Docs"
description: "Vue d’ensemble du service de base de données relationnelle d’Azure Database pour MySQL."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 08/02/2017
ms.custom: mvc
ms.openlocfilehash: a1becaf8465f68ecac768c5c6b2dbc95e8ff7278
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="what-is-azure-database-for-mysql-service-introduction"></a><span data-ttu-id="4ef43-103">Qu’est-ce qu’Azure Database pour MySQL ?</span><span class="sxs-lookup"><span data-stu-id="4ef43-103">What is Azure Database for MySQL?</span></span> <span data-ttu-id="4ef43-104">Présentation du service</span><span class="sxs-lookup"><span data-stu-id="4ef43-104">Service Introduction</span></span>
<span data-ttu-id="4ef43-105">Azure Database pour MySQL est un service de base de données relationnelle dans le cloud de Microsoft basé sur le moteur de base de données [MySQL Community Edition](https://www.mysql.com/products/community/).</span><span class="sxs-lookup"><span data-stu-id="4ef43-105">Azure Database for MySQL is a relational database service in the Microsoft cloud based on [MySQL Community Edition](https://www.mysql.com/products/community/) database engine.</span></span>  <span data-ttu-id="4ef43-106">Azure Database pour MySQL offre :</span><span class="sxs-lookup"><span data-stu-id="4ef43-106">Azure Database for MySQL delivers:</span></span>

- <span data-ttu-id="4ef43-107">Performances prévisibles sur plusieurs niveaux de service</span><span class="sxs-lookup"><span data-stu-id="4ef43-107">Predictable performance at multiple service levels</span></span>
- <span data-ttu-id="4ef43-108">Évolutivité dynamique sans interruption de l’application</span><span class="sxs-lookup"><span data-stu-id="4ef43-108">Dynamic scalability with no application downtime</span></span>
- <span data-ttu-id="4ef43-109">Haute disponibilité intégrée</span><span class="sxs-lookup"><span data-stu-id="4ef43-109">Built-in high availability</span></span>
- <span data-ttu-id="4ef43-110">Protection des données</span><span class="sxs-lookup"><span data-stu-id="4ef43-110">Data protection</span></span>

<span data-ttu-id="4ef43-111">Ces fonctionnalités ne nécessitent presque aucune administration, et toutes sont fournies sans coût supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="4ef43-111">These capabilities require almost no administration, and all are provided at no additional cost.</span></span> <span data-ttu-id="4ef43-112">Elles vous permettent de vous concentrer sur le développement rapide de vos applications et d’accélérer leur mise sur le marché, plutôt que de consacrer du temps et des ressources à la gestion des machines virtuelles et de leur infrastructure.</span><span class="sxs-lookup"><span data-stu-id="4ef43-112">They allow you to focus on rapid app development and accelerating your time to market, rather than allocating precious time and resources to managing virtual machines and infrastructure.</span></span> <span data-ttu-id="4ef43-113">En outre, vous pouvez continuer à développer votre application avec les outils open source et la plateforme de votre choix et fournir avec la vitesse et l’efficacité que vos activités professionnelles exigent sans avoir à acquérir de nouvelles compétences.</span><span class="sxs-lookup"><span data-stu-id="4ef43-113">In addition, you can continue to develop your application with the open source tools and platform of your choice, and deliver with the speed and efficiency your business demands without having to learn new skills.</span></span>

![Diagramme conceptuel d’Azure Database pour MySQL](media/overview/1-azure-db-for-mysql-conceptual-diagram.png)

<span data-ttu-id="4ef43-115">Cet article présente les principaux concepts et fonctionnalités d’Azure Database pour MySQL qui ont trait aux performances, à l’extensibilité et à la facilité de gestion. Il contient également des liens pour en explorer les détails.</span><span class="sxs-lookup"><span data-stu-id="4ef43-115">This article is an introduction to Azure Database for MySQL core concepts and features related to performance, scalability, and manageability, with links to explore details.</span></span> <span data-ttu-id="4ef43-116">Consultez ces démarrages rapides pour bien commencer :</span><span class="sxs-lookup"><span data-stu-id="4ef43-116">See these quick starts to get you started:</span></span>
- [<span data-ttu-id="4ef43-117">Création d’un serveur Azure Database pour MySQL à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="4ef43-117">Create an Azure Database for MySQL server using Azure portal</span></span>](quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="4ef43-118">Création d’un serveur Azure Database pour MySQL à l’aide de la CLI Azure</span><span class="sxs-lookup"><span data-stu-id="4ef43-118">Create an Azure Database for MySQL server using Azure CLI</span></span>](quickstart-create-mysql-server-database-using-azure-cli.md)

<span data-ttu-id="4ef43-119">Pour accéder à des exemples Azure CLI, consultez :</span><span class="sxs-lookup"><span data-stu-id="4ef43-119">For a set of Azure CLI samples, see:</span></span>
- [<span data-ttu-id="4ef43-120">Exemples de CLI Azure pour Azure Database pour MySQL</span><span class="sxs-lookup"><span data-stu-id="4ef43-120">Azure CLI samples for Azure Database for MySQL</span></span>](sample-scripts-azure-cli.md)

## <a name="adjust-performance-and-scale-without-downtime"></a><span data-ttu-id="4ef43-121">Ajustez les performances et la mise à l'échelle sans interruption de service</span><span class="sxs-lookup"><span data-stu-id="4ef43-121">Adjust performance and scale without downtime</span></span>
<span data-ttu-id="4ef43-122">Le service Azure Database pour MySQL propose deux niveaux de service : De base et Standard.</span><span class="sxs-lookup"><span data-stu-id="4ef43-122">Azure Database for MySQL service offers two service tiers: Basic and Standard.</span></span> <span data-ttu-id="4ef43-123">Chaque niveau offre différentes performances et fonctionnalités pour prendre en charge des charges de travail de base de données plus ou moins denses.</span><span class="sxs-lookup"><span data-stu-id="4ef43-123">Each tier offers different performance and capabilities to support lightweight to heavyweight database workloads.</span></span> <span data-ttu-id="4ef43-124">Vous pouvez créer votre première application sur une petite base de données pour quelques dollars par mois, puis changer de niveau de votre service pour vous adapter aux besoins de votre solution sans interruption de service.</span><span class="sxs-lookup"><span data-stu-id="4ef43-124">You can build your first app on a small database for a few dollars a month, then change your service tier to scale with needs of your solution with no downtime.</span></span> <span data-ttu-id="4ef43-125">L’évolutivité dynamique permet de répondre en toute transparence à l’évolution rapide des besoins en ressources de votre base de données.</span><span class="sxs-lookup"><span data-stu-id="4ef43-125">Dynamic scalability enables your database to transparently respond to rapidly changing resource requirements.</span></span> <span data-ttu-id="4ef43-126">Vous payez uniquement pour les ressources dont vous avez besoin, quand vous en avez besoin.</span><span class="sxs-lookup"><span data-stu-id="4ef43-126">You only pay for the resources you need, when you need them.</span></span>

## <a name="monitoring-and-alerting"></a><span data-ttu-id="4ef43-127">Surveillance et alerte</span><span class="sxs-lookup"><span data-stu-id="4ef43-127">Monitoring and alerting</span></span>
<span data-ttu-id="4ef43-128">Comment faire la part des choses entre les différents niveaux de service selon une mise à l'échelle verticale ?</span><span class="sxs-lookup"><span data-stu-id="4ef43-128">How do you know the right click-stop when you dial up and down?</span></span> <span data-ttu-id="4ef43-129">Utilisez les fonctionnalités intégrées de surveillance et d’alerte de performances, combinées avec les évaluations de performance basées sur les unités de calcul.</span><span class="sxs-lookup"><span data-stu-id="4ef43-129">Use the built-in performance monitoring and alerting features, combined with the performance ratings based on Compute Unit.</span></span> <span data-ttu-id="4ef43-130">Ces fonctionnalités vous permettent d’évaluer rapidement l’impact des mises à l’échelle (montées ou descentes en charge) en fonction de vos besoins en performances actuels ou pour un projet.</span><span class="sxs-lookup"><span data-stu-id="4ef43-130">Using these features, you can quickly assess the impact of scaling up or down based on your current or project performance needs.</span></span> <span data-ttu-id="4ef43-131">Consultez [Concepts : niveaux de service](concepts-service-tiers.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="4ef43-131">See [Concepts: Service tiers](concepts-service-tiers.md) for details.</span></span>

## <a name="keep-your-app-and-business-running"></a><span data-ttu-id="4ef43-132">Votre application et votre activité ne s’arrêtent jamais</span><span class="sxs-lookup"><span data-stu-id="4ef43-132">Keep your app and business running</span></span>
<span data-ttu-id="4ef43-133">Avec un temps de disponibilité de 99,99 %, l’excellent contrat de niveau de service (SLA) d’Azure, soutenu par un réseau mondial de centres de données gérés par Microsoft, permet d’exécuter votre application 24 heures sur 24, 7 jours sur 7.</span><span class="sxs-lookup"><span data-stu-id="4ef43-133">Azure's industry leading 99.99% availability service level agreement (SLA), powered by a global network of Microsoft-managed datacenters, helps keep your app running 24/7.</span></span> <span data-ttu-id="4ef43-134">Avec chaque serveur Azure Database pour MySQL, vous tirez parti de la sécurité intégrée, d’une tolérance en cas de panne et de la protection des données que vous seriez de toute manière contraint d’acheter ou de concevoir, de créer et de gérer.</span><span class="sxs-lookup"><span data-stu-id="4ef43-134">With every Azure Database for MySQL server, you take advantage of built-in security, fault tolerance, and data protection that you would otherwise have to buy or design, build, and manage.</span></span> <span data-ttu-id="4ef43-135">Avec Azure Database pour MySQM, vous pouvez utiliser la limite de restauration dans le temps pour récupérer un serveur à un état antérieur, jusqu’à 35 jours.</span><span class="sxs-lookup"><span data-stu-id="4ef43-135">With Azure Database for MySQL, you can use point-in-time restore to recover a server to an earlier state, as far back as 35 days.</span></span>

## <a name="secure-your-data"></a><span data-ttu-id="4ef43-136">Sécurisez vos données</span><span class="sxs-lookup"><span data-stu-id="4ef43-136">Secure your data</span></span>
<span data-ttu-id="4ef43-137">Les services de base de données Azure ont une tradition de sécurité des données qu’Azure Database pour MySQL respecte avec des fonctionnalités qui limitent l’accès, protègent les données au repos et en mouvement, et vous aident à surveiller l’activité.</span><span class="sxs-lookup"><span data-stu-id="4ef43-137">Azure database services have a tradition of data security that Azure Database for MySQL upholds with features that limit access, protect data at-rest and in-motion, and help you monitor activity.</span></span> <span data-ttu-id="4ef43-138">Visitez le [Centre de gestion de la confidentialité Azure](https://www.microsoft.com/en-us/TrustCenter/Security/default.aspx) pour plus d’informations sur la sécurité de la plateforme Azure.</span><span class="sxs-lookup"><span data-stu-id="4ef43-138">Visit the [Azure Trust Center](https://www.microsoft.com/en-us/TrustCenter/Security/default.aspx) for information about Azure's platform security.</span></span>

<span data-ttu-id="4ef43-139">Le service Base de données Azure pour MySQL utilise le chiffrement de stockage pour les données au repos.</span><span class="sxs-lookup"><span data-stu-id="4ef43-139">The Azure Database for MySQL service uses storage encryption for data at-rest.</span></span> <span data-ttu-id="4ef43-140">Les données incluant des sauvegardes sont chiffrées sur le disque (à l’exception des fichiers temporaires créés par le moteur lors de l’exécution des requêtes).</span><span class="sxs-lookup"><span data-stu-id="4ef43-140">Data including backups, are encrypted on disk (with the exception of temporary files created by the engine while running queries).</span></span> <span data-ttu-id="4ef43-141">Le service utilise le chiffrement AES 256 bits qui est inclus dans le chiffrement de stockage Azure, et les clés sont gérées par le système.</span><span class="sxs-lookup"><span data-stu-id="4ef43-141">The service uses AES 256-bit cipher that is included in Azure storage encryption, and the keys are system managed.</span></span> <span data-ttu-id="4ef43-142">Le chiffrement de stockage est toujours activé et ne peut pas être désactivé.</span><span class="sxs-lookup"><span data-stu-id="4ef43-142">Storage encryption is always on and cannot be disabled.</span></span>

<span data-ttu-id="4ef43-143">Par défaut, le service Base de données Azure pour MySQL est configuré afin de requérir la [sécurité de connexion SSL](./concepts-ssl-connection-security.md) pour les données en mouvement sur le réseau.</span><span class="sxs-lookup"><span data-stu-id="4ef43-143">By default, the Azure Database for MySQL service is configured to require [SSL connection security](./concepts-ssl-connection-security.md) for data in-motion across the network.</span></span> <span data-ttu-id="4ef43-144">L’application de connexions SSL entre votre serveur de base de données et vos applications clientes vous protège contre les « attaques de l’intercepteur » en chiffrant le flux de données entre le serveur et votre application.</span><span class="sxs-lookup"><span data-stu-id="4ef43-144">Enforcing SSL connections between your database server and your client applications helps protect against "man in the middle" attacks by encrypting the data stream between the server and your application.</span></span>  <span data-ttu-id="4ef43-145">Vous avez la possibilité de désactiver le recours obligatoire au protocole SSL pour la connexion à votre service de base de données si votre application cliente ne prend pas en charge la connectivité SSL.</span><span class="sxs-lookup"><span data-stu-id="4ef43-145">Optionally, you can disable requiring SSL for connecting to your database service if your client application does not support SSL connectivity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4ef43-146">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4ef43-146">Next Steps</span></span>
<span data-ttu-id="4ef43-147">Maintenant que vous avez lu l’introduction à Azure Database pour MySQL et répondu à la question « Qu’est-ce qu’Azure Database pour MySQL ? », vous êtes prêt à effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="4ef43-147">Now that you've read an introduction to Azure Database for MySQL and answered the question "What is Azure Database for MySQL?", you're ready to:</span></span>
- <span data-ttu-id="4ef43-148">Consultez la page de tarification pour des comparaisons de coûts et des calculatrices.</span><span class="sxs-lookup"><span data-stu-id="4ef43-148">See the pricing page for cost comparisons and calculators.</span></span> [<span data-ttu-id="4ef43-149">Tarification</span><span class="sxs-lookup"><span data-stu-id="4ef43-149">Pricing</span></span>](https://azure.microsoft.com/pricing/details/mysql/)
- <span data-ttu-id="4ef43-150">Commencez par créer votre premier serveur.</span><span class="sxs-lookup"><span data-stu-id="4ef43-150">Get started by creating your first server.</span></span> [<span data-ttu-id="4ef43-151">Création d’un serveur Azure Database pour MySQL à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="4ef43-151">Create an Azure Database for MySQL server using Azure portal</span></span>](quickstart-create-mysql-server-database-using-azure-portal.md)
- <span data-ttu-id="4ef43-152">Créer votre première application en Python, PHP, Ruby, C\#, Java, Node.js : [les bibliothèques de connectivité utilisées pour se connecter à Azure Database pour MySQL](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="4ef43-152">Build your first app in Python, PHP, Ruby, C\#, Java, Node.js: [Connectivity libraries used to connect to Azure Database for MySQL](concepts-connection-libraries.md)</span></span>