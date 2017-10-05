---
title: "Connecter un service Azure App Service existant à une base de données Azure pour MySQL | Microsoft Docs"
description: "Instructions pour connecter correctement un service Azure App Service existant à une base de données Azure pour MySQL"
services: mysql
author: v-chenyh
ms.author: v-chenyh
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/23/2017
ms.openlocfilehash: 735e21e8135d67405ec6b88d75be1711a2f071f0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-an-existing-azure-app-service-to-azure-database-for-mysql-server"></a><span data-ttu-id="43e68-103">Connecter un service Azure App Service existant à un serveur de base de données Azure pour MySQL</span><span class="sxs-lookup"><span data-stu-id="43e68-103">Connect an existing Azure App Service to Azure Database for MySQL server</span></span>
<span data-ttu-id="43e68-104">Ce document explique comment connecter un service Azure App Service existant à votre serveur de base de données Azure pour MySQL.</span><span class="sxs-lookup"><span data-stu-id="43e68-104">This document explains how to connect an existing Azure App Service to your Azure Database for MySQL server.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="43e68-105">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="43e68-105">Before you begin</span></span>
<span data-ttu-id="43e68-106">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="43e68-106">Log in to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="43e68-107">Créez un serveur de base de données Azure pour MySQL.</span><span class="sxs-lookup"><span data-stu-id="43e68-107">Create an Azure Database for MySQL server.</span></span> <span data-ttu-id="43e68-108">Pour plus d’informations, reportez-vous à [Guide pratique pour créer un serveur de base de données Azure pour MySQL à partir du portail](quickstart-create-mysql-server-database-using-azure-portal.md) ou à [Guide pratique pour créer un serveur de base de données Azure pour MySQL à l’aide de l’interface CLI](quickstart-create-mysql-server-database-using-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="43e68-108">For details, refer to [How to create Azure Database for MySQL server from Portal](quickstart-create-mysql-server-database-using-azure-portal.md) or [How to create Azure Database for MySQL server using CLI](quickstart-create-mysql-server-database-using-azure-cli.md).</span></span>

<span data-ttu-id="43e68-109">Il existe actuellement deux solutions pour activer l’accès à partir d’un service Azure App Service vers une base de données Azure pour MySQL.</span><span class="sxs-lookup"><span data-stu-id="43e68-109">Currently there are two solutions to enable access from an Azure App Service to an Azure Database for MySQL.</span></span> <span data-ttu-id="43e68-110">Ces deux solutions impliquent de configurer des règles de pare-feu au niveau du serveur.</span><span class="sxs-lookup"><span data-stu-id="43e68-110">Both solutions involve setting up server-level firewall rules.</span></span>

## <a name="solution-1---create-a-firewall-rule-to-allow-all-ips"></a><span data-ttu-id="43e68-111">Solution 1 - Créer une règle de pare-feu pour autoriser toutes les adresses IP</span><span class="sxs-lookup"><span data-stu-id="43e68-111">Solution 1 - Create a firewall rule to allow all IPs</span></span>
<span data-ttu-id="43e68-112">La base de données Azure pour MySQL fournit une sécurité d’accès à l’aide d’un pare-feu afin de protéger vos données.</span><span class="sxs-lookup"><span data-stu-id="43e68-112">Azure Database for MySQL provides access security using a firewall to protect your data.</span></span> <span data-ttu-id="43e68-113">Lors de la connexion d’un service Azure App Service à une base de données Azure pour MySQL, gardez à l’esprit que les adresses IP sortantes d’App Service sont dynamiques par nature.</span><span class="sxs-lookup"><span data-stu-id="43e68-113">When connecting from an Azure App Service to Azure Database for MySQL server, keep in mind that the outbound IPs of App Service are dynamic in nature.</span></span> 

<span data-ttu-id="43e68-114">Pour garantir la disponibilité de votre service Azure App Service, nous recommandons d’utiliser cette solution pour autoriser TOUTES les adresses IP.</span><span class="sxs-lookup"><span data-stu-id="43e68-114">To ensure the availability of your Azure App Service, we recommend using this solution to allow ALL IPs.</span></span>

> [!NOTE]
> <span data-ttu-id="43e68-115">Microsoft travaille à une solution à long terme pour éviter d’autoriser toutes les adresses IP des services Azure à se connecter à la base de données Azure pour MySQL.</span><span class="sxs-lookup"><span data-stu-id="43e68-115">Microsoft is working for a long-term solution to avoid allowing all IPs for Azure services to connect to Azure Database for MySQL.</span></span>

1. <span data-ttu-id="43e68-116">Dans le panneau du serveur MySQL, sous le titre Paramètres, cliquez sur **Sécurité des connexions** afin d’ouvrir le panneau Sécurité des connexions pour la base de données Azure pour MySQL.</span><span class="sxs-lookup"><span data-stu-id="43e68-116">On the MySQL server blade, under Settings heading, click **Connection Security** to open the Connection Security blade for the Azure Database for MySQL.</span></span>

   ![Portail Azure - cliquez sur Sécurité des connexions](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. <span data-ttu-id="43e68-118">Entrez **NOM DE LA RÈGLE**, **ADRESSE IP DE DÉBUT** et **ADRESSE IP DE FIN**.</span><span class="sxs-lookup"><span data-stu-id="43e68-118">Enter **RULE NAME**, **START IP**, and **END IP**.</span></span> <span data-ttu-id="43e68-119">Cliquez ensuite sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="43e68-119">Then click **Save**.</span></span>
   - <span data-ttu-id="43e68-120">Nom de la règle : Allow-All-IPs</span><span class="sxs-lookup"><span data-stu-id="43e68-120">Rule name: Allow-All-IPs</span></span>
   - <span data-ttu-id="43e68-121">Adresse IP de début : 0.0.0.0</span><span class="sxs-lookup"><span data-stu-id="43e68-121">Start IP: 0.0.0.0</span></span>
   - <span data-ttu-id="43e68-122">Adresse IP de fin : 255.255.255.255</span><span class="sxs-lookup"><span data-stu-id="43e68-122">End IP: 255.255.255.255</span></span>

   ![Portail Azure - Ajouter toutes les adresses IP](./media/howto-connect-webapp/1_2-add-all-ips.png)

## <a name="solution-2---create-a-firewall-rule-to-explicitly-allow-outbound-ips"></a><span data-ttu-id="43e68-124">Solution 2 - Créer une règle de pare-feu pour autoriser explicitement des adresses IP sortantes</span><span class="sxs-lookup"><span data-stu-id="43e68-124">Solution 2 - Create a firewall rule to explicitly allow outbound IPs</span></span>
<span data-ttu-id="43e68-125">Vous pouvez ajouter explicitement toutes les adresses IP sortantes de votre service Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="43e68-125">You can explicitly add all the outbound IPs of your Azure App Service.</span></span>

1. <span data-ttu-id="43e68-126">Dans le panneau Propriétés d’App Service, affichez votre **ADRESSE IP SORTANTE**.</span><span class="sxs-lookup"><span data-stu-id="43e68-126">On the App Service Properties blade, view your **OUTBOUND IP ADDRESS**.</span></span>

   ![Portail Azure - Afficher des adresses IP sortantes](./media/howto-connect-webapp/2_1-outbound-ip-address.png)

2. <span data-ttu-id="43e68-128">Dans le panneau Sécurité de la connexion de MySQL, ajoutez une par une des adresses IP sortantes.</span><span class="sxs-lookup"><span data-stu-id="43e68-128">On the MySQL Connection security blade, add outbound IPs one by one.</span></span>

   ![Portail Azure - Ajouter des adresses IP explicites](./media/howto-connect-webapp/2_2-add-explicit-ips.png)

3. <span data-ttu-id="43e68-130">N’oubliez pas d’**Enregistrer** vos règles de pare-feu.</span><span class="sxs-lookup"><span data-stu-id="43e68-130">Remember to **Save** your firewall rules.</span></span>

<span data-ttu-id="43e68-131">Bien que le service Azure App Service tente de maintenir les adresses IP constantes au fil du temps, il existe des cas où les adresses IP peuvent changer.</span><span class="sxs-lookup"><span data-stu-id="43e68-131">Though the Azure App service attempts to keep IP addresses constant over time, there are cases where the IP addresses may change.</span></span> <span data-ttu-id="43e68-132">Par exemple, quand l’application est recyclée, qu’une opération de mise à l’échelle se produit ou que de nouvelles machines sont ajoutées dans des centres de données régionaux Azure pour augmenter la capacité.</span><span class="sxs-lookup"><span data-stu-id="43e68-132">For example, when the app recycles or a scale operation occurs, or when new machines are added in Azure regional data centers to increase the capacity.</span></span> <span data-ttu-id="43e68-133">Quand les adresses IP changent, l’application peut subir des temps d’arrêt s’il ne peut plus se connecter au serveur MySQL.</span><span class="sxs-lookup"><span data-stu-id="43e68-133">When the IP addresses change, the app could experience downtime in the event it can no longer connect to the MySQL server.</span></span> <span data-ttu-id="43e68-134">Envisagez cette éventualité lors du choix de l’une des solutions précédentes.</span><span class="sxs-lookup"><span data-stu-id="43e68-134">Consider this potential when choosing one of the preceding solutions.</span></span>

## <a name="ssl-configuration"></a><span data-ttu-id="43e68-135">Configuration SSL</span><span class="sxs-lookup"><span data-stu-id="43e68-135">SSL configuration</span></span>
<span data-ttu-id="43e68-136">SSL est activé par défaut sur la base de données Azure pour MySQL.</span><span class="sxs-lookup"><span data-stu-id="43e68-136">Azure Database for MySQL has SSL Enabled by default.</span></span> <span data-ttu-id="43e68-137">Si votre application n’utilise pas le protocole SSL pour se connecter à la base de données, vous devez le désactiver sur le serveur MySQL.</span><span class="sxs-lookup"><span data-stu-id="43e68-137">If your application is not using SSL to connect to the database, then you need to disable SSL on MySQL server.</span></span> <span data-ttu-id="43e68-138">Pour plus d’informations sur la configuration de SSL, consultez [Utilisation de SSL avec une base de données Azure pour MySQL](howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="43e68-138">For details on how to configure SSL, See [Using SSL with Azure Database for MySQL](howto-configure-ssl.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="43e68-139">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="43e68-139">Next steps</span></span>
<span data-ttu-id="43e68-140">Pour plus d’informations sur les chaînes de connexion, reportez-vous à [Chaînes de connexions](howto-connection-string.md).</span><span class="sxs-lookup"><span data-stu-id="43e68-140">For more information about connection strings, refer to [Connection Strings](howto-connection-string.md).</span></span>
