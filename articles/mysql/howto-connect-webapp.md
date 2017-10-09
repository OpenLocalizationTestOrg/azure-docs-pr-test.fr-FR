---
title: "aaaConnect existant du Service d’applications Azure tooAzure base de données MySQL | Documents Microsoft"
description: "Instructions de la tooproperly connexion d’un tooAzure Azure App Service existant de base de données pour MySQL"
services: mysql
author: v-chenyh
ms.author: v-chenyh
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/23/2017
ms.openlocfilehash: 6d5b16f316e186d665370adcd8b7c7bb38c8d51a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-an-existing-azure-app-service-tooazure-database-for-mysql-server"></a><span data-ttu-id="6d698-103">Se connecter à un tooAzure Azure App Service existant de base de données du serveur MySQL</span><span class="sxs-lookup"><span data-stu-id="6d698-103">Connect an existing Azure App Service tooAzure Database for MySQL server</span></span>
<span data-ttu-id="6d698-104">Ce document explique comment tooconnect un tooyour Azure App Service existant Azure de base de données du serveur MySQL.</span><span class="sxs-lookup"><span data-stu-id="6d698-104">This document explains how tooconnect an existing Azure App Service tooyour Azure Database for MySQL server.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="6d698-105">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="6d698-105">Before you begin</span></span>
<span data-ttu-id="6d698-106">Connectez-vous à toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6d698-106">Log in toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="6d698-107">Créez un serveur de base de données Azure pour MySQL.</span><span class="sxs-lookup"><span data-stu-id="6d698-107">Create an Azure Database for MySQL server.</span></span> <span data-ttu-id="6d698-108">Pour plus d’informations, consultez trop[comment toocreate Azure de base de données MySQL server à partir du portail](quickstart-create-mysql-server-database-using-azure-portal.md) ou [comment toocreate Azure de base de données MySQL server à l’aide de CLI](quickstart-create-mysql-server-database-using-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="6d698-108">For details, refer too[How toocreate Azure Database for MySQL server from Portal](quickstart-create-mysql-server-database-using-azure-portal.md) or [How toocreate Azure Database for MySQL server using CLI](quickstart-create-mysql-server-database-using-azure-cli.md).</span></span>

<span data-ttu-id="6d698-109">Il existe actuellement deux solutions tooenable d’accès à partir d’un base de données Azure du tooan Azure App Service pour MySQL.</span><span class="sxs-lookup"><span data-stu-id="6d698-109">Currently there are two solutions tooenable access from an Azure App Service tooan Azure Database for MySQL.</span></span> <span data-ttu-id="6d698-110">Ces deux solutions impliquent de configurer des règles de pare-feu au niveau du serveur.</span><span class="sxs-lookup"><span data-stu-id="6d698-110">Both solutions involve setting up server-level firewall rules.</span></span>

## <a name="solution-1---create-a-firewall-rule-tooallow-all-ips"></a><span data-ttu-id="6d698-111">Solution 1 : créer un tooallow de règle de pare-feu toutes les adresses IP</span><span class="sxs-lookup"><span data-stu-id="6d698-111">Solution 1 - Create a firewall rule tooallow all IPs</span></span>
<span data-ttu-id="6d698-112">Base de données Azure pour MySQL fournit la sécurité d’accès à l’aide d’un pare-feu tooprotect vos données.</span><span class="sxs-lookup"><span data-stu-id="6d698-112">Azure Database for MySQL provides access security using a firewall tooprotect your data.</span></span> <span data-ttu-id="6d698-113">Lors de la connexion à partir d’un tooAzure Azure App Service de base de données du serveur MySQL, gardez à l’esprit que hello sortant des adresses IP du Service d’applications sont dynamiques par nature.</span><span class="sxs-lookup"><span data-stu-id="6d698-113">When connecting from an Azure App Service tooAzure Database for MySQL server, keep in mind that hello outbound IPs of App Service are dynamic in nature.</span></span> 

<span data-ttu-id="6d698-114">disponibilité de hello tooensure de votre Service d’applications Azure, nous recommandons d’utiliser cette tooallow solution toutes les adresses IP.</span><span class="sxs-lookup"><span data-stu-id="6d698-114">tooensure hello availability of your Azure App Service, we recommend using this solution tooallow ALL IPs.</span></span>

> [!NOTE]
> <span data-ttu-id="6d698-115">Microsoft s’emploie pour un tooavoid solution à long terme consistant à autoriser toutes les adresses IP pour les services Azure tooconnect tooAzure base de données MySQL.</span><span class="sxs-lookup"><span data-stu-id="6d698-115">Microsoft is working for a long-term solution tooavoid allowing all IPs for Azure services tooconnect tooAzure Database for MySQL.</span></span>

1. <span data-ttu-id="6d698-116">Sur le panneau de serveur MySQL hello, sous paramètres de titre, cliquez sur **sécurité de connexion** Panneau de sécurité de connexion tooopen hello pour hello Azure de base de données de MySQL.</span><span class="sxs-lookup"><span data-stu-id="6d698-116">On hello MySQL server blade, under Settings heading, click **Connection Security** tooopen hello Connection Security blade for hello Azure Database for MySQL.</span></span>

   ![Portail Azure - cliquez sur Sécurité des connexions](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. <span data-ttu-id="6d698-118">Entrez **NOM DE LA RÈGLE**, **ADRESSE IP DE DÉBUT** et **ADRESSE IP DE FIN**.</span><span class="sxs-lookup"><span data-stu-id="6d698-118">Enter **RULE NAME**, **START IP**, and **END IP**.</span></span> <span data-ttu-id="6d698-119">Cliquez ensuite sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="6d698-119">Then click **Save**.</span></span>
   - <span data-ttu-id="6d698-120">Nom de la règle : Allow-All-IPs</span><span class="sxs-lookup"><span data-stu-id="6d698-120">Rule name: Allow-All-IPs</span></span>
   - <span data-ttu-id="6d698-121">Adresse IP de début : 0.0.0.0</span><span class="sxs-lookup"><span data-stu-id="6d698-121">Start IP: 0.0.0.0</span></span>
   - <span data-ttu-id="6d698-122">Adresse IP de fin : 255.255.255.255</span><span class="sxs-lookup"><span data-stu-id="6d698-122">End IP: 255.255.255.255</span></span>

   ![Portail Azure - Ajouter toutes les adresses IP](./media/howto-connect-webapp/1_2-add-all-ips.png)

## <a name="solution-2---create-a-firewall-rule-tooexplicitly-allow-outbound-ips"></a><span data-ttu-id="6d698-124">Solution 2 : création d’un pare-feu tooexplicitly de règle Autoriser les adresses IP sortante</span><span class="sxs-lookup"><span data-stu-id="6d698-124">Solution 2 - Create a firewall rule tooexplicitly allow outbound IPs</span></span>
<span data-ttu-id="6d698-125">Vous pouvez ajouter explicitement que tous les hello sortant adresses IP de votre Service d’applications Azure.</span><span class="sxs-lookup"><span data-stu-id="6d698-125">You can explicitly add all hello outbound IPs of your Azure App Service.</span></span>

1. <span data-ttu-id="6d698-126">Sur le panneau des propriétés de Service d’application hello, affichez votre **adresse IP sortante**.</span><span class="sxs-lookup"><span data-stu-id="6d698-126">On hello App Service Properties blade, view your **OUTBOUND IP ADDRESS**.</span></span>

   ![Portail Azure - Afficher des adresses IP sortantes](./media/howto-connect-webapp/2_1-outbound-ip-address.png)

2. <span data-ttu-id="6d698-128">Dans Panneau de sécurité de connexion MySQL hello, ajouter des adresses IP sortant un par un.</span><span class="sxs-lookup"><span data-stu-id="6d698-128">On hello MySQL Connection security blade, add outbound IPs one by one.</span></span>

   ![Portail Azure - Ajouter des adresses IP explicites](./media/howto-connect-webapp/2_2-add-explicit-ips.png)

3. <span data-ttu-id="6d698-130">N’oubliez pas trop**enregistrer** vos règles de pare-feu.</span><span class="sxs-lookup"><span data-stu-id="6d698-130">Remember too**Save** your firewall rules.</span></span>

<span data-ttu-id="6d698-131">Si hello Azure App service tente de tookeep IP adresses constante au fil du temps, il existe des cas où les adresses IP de hello peuvent changer.</span><span class="sxs-lookup"><span data-stu-id="6d698-131">Though hello Azure App service attempts tookeep IP addresses constant over time, there are cases where hello IP addresses may change.</span></span> <span data-ttu-id="6d698-132">Par exemple, hello lorsque les recyclages de l’application ou une opération de mise à l’échelle se produit lorsque les nouveaux ordinateurs sont ajoutés dans les données régionales Azure centres de capacité de hello tooincrease.</span><span class="sxs-lookup"><span data-stu-id="6d698-132">For example, when hello app recycles or a scale operation occurs, or when new machines are added in Azure regional data centers tooincrease hello capacity.</span></span> <span data-ttu-id="6d698-133">Lors de la modification des adresses IP de hello, application hello peut rencontrer des temps d’arrêt dans l’événement hello il peut ne plus se connecter toohello MySQL server.</span><span class="sxs-lookup"><span data-stu-id="6d698-133">When hello IP addresses change, hello app could experience downtime in hello event it can no longer connect toohello MySQL server.</span></span> <span data-ttu-id="6d698-134">Envisagez cette possibilité lorsque vous choisissez une des hello précédant les solutions.</span><span class="sxs-lookup"><span data-stu-id="6d698-134">Consider this potential when choosing one of hello preceding solutions.</span></span>

## <a name="ssl-configuration"></a><span data-ttu-id="6d698-135">Configuration SSL</span><span class="sxs-lookup"><span data-stu-id="6d698-135">SSL configuration</span></span>
<span data-ttu-id="6d698-136">SSL est activé par défaut sur la base de données Azure pour MySQL.</span><span class="sxs-lookup"><span data-stu-id="6d698-136">Azure Database for MySQL has SSL Enabled by default.</span></span> <span data-ttu-id="6d698-137">Si votre application n’utilise pas de base de données SSL tooconnect toohello, vous devez toodisable SSL sur le serveur MySQL.</span><span class="sxs-lookup"><span data-stu-id="6d698-137">If your application is not using SSL tooconnect toohello database, then you need toodisable SSL on MySQL server.</span></span> <span data-ttu-id="6d698-138">Pour plus d’informations sur la façon de tooconfigure SSL, voir [à l’aide de SSL avec la base de données Azure pour MySQL](howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="6d698-138">For details on how tooconfigure SSL, See [Using SSL with Azure Database for MySQL](howto-configure-ssl.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6d698-139">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6d698-139">Next steps</span></span>
<span data-ttu-id="6d698-140">Pour plus d’informations sur les chaînes de connexion, consultez trop[les chaînes de connexion](howto-connection-string.md).</span><span class="sxs-lookup"><span data-stu-id="6d698-140">For more information about connection strings, refer too[Connection Strings](howto-connection-string.md).</span></span>
