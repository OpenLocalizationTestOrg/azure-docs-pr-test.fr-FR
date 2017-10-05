---
title: "Création et gestion des règles de pare-feu Azure Database pour MySQL à l’aide du portail Azure | Microsoft Docs"
description: "Création et gestion des règles de pare-feu Azure Database pour MySQL à l’aide du portail Azure"
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 33198e5a6e11df2db3a17fc96a0b3cd4b1a284e8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-azure-database-for-mysql-firewall-rules-using-the-azure-portal"></a><span data-ttu-id="a02ad-103">Création et gestion des règles de pare-feu Azure Database pour MySQL à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="a02ad-103">Create and manage Azure Database for MySQL firewall rules using the Azure portal</span></span>
<span data-ttu-id="a02ad-104">Les règles de pare-feu au niveau du serveur permettent aux administrateurs d’accéder à un serveur Azure Database pour MySQL à partir d’une adresse IP spécifiée ou d’une plage d’adresses IP.</span><span class="sxs-lookup"><span data-stu-id="a02ad-104">Server-level firewall rules enable administrators to access an Azure Database for MySQL Server from a specified IP address or range of IP addresses.</span></span> 

## <a name="create-a-server-level-firewall-rule-in-the-azure-portal"></a><span data-ttu-id="a02ad-105">Créer une règle de pare-feu au niveau du serveur dans le portail Azure</span><span class="sxs-lookup"><span data-stu-id="a02ad-105">Create a server-level firewall rule in the Azure portal</span></span>

1. <span data-ttu-id="a02ad-106">Dans le panneau du serveur MySQL, sous le titre Paramètres, cliquez sur **Sécurité des connexions** afin d’ouvrir le panneau Sécurité des connexions pour la base de données Azure pour MySQL.</span><span class="sxs-lookup"><span data-stu-id="a02ad-106">On the MySQL server blade, under Settings heading, click **Connection Security** to open the Connection Security blade for the Azure Database for MySQL.</span></span>

   ![Portail Azure - cliquez sur Sécurité des connexions](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. <span data-ttu-id="a02ad-108">Cliquez sur **Ajouter mon adresse IP** dans la barre d’outils pour créer une règle avec l’adresse IP de votre ordinateur, telle que détectée par le système Azure.</span><span class="sxs-lookup"><span data-stu-id="a02ad-108">Click **Add My IP** on the toolbar to create a rule with the IP address of your computer, as perceived by the Azure system.</span></span>

   ![Portail Azure - cliquez sur Ajouter mon adresse IP](./media/howto-manage-firewall-using-portal/2-add-my-ip.png)

3. <span data-ttu-id="a02ad-110">Vérifiez votre adresse IP avant d’enregistrer la configuration.</span><span class="sxs-lookup"><span data-stu-id="a02ad-110">Verify your IP address before saving the configuration.</span></span> <span data-ttu-id="a02ad-111">Dans certains cas, l’adresse IP identifiée par le portail Azure diffère de l’adresse IP utilisée lors de l’accès à Internet et aux serveurs Azure.</span><span class="sxs-lookup"><span data-stu-id="a02ad-111">In some situations, the IP address observed by Azure portal differs from the IP address used when accessing the internet and Azure servers.</span></span> <span data-ttu-id="a02ad-112">Par conséquent, vous devrez peut-être modifier l’adresse IP de début et l’adresse IP de fin pour que la règle fonctionne comme prévu.</span><span class="sxs-lookup"><span data-stu-id="a02ad-112">Therefore, you may need to change the Start IP and End IP to make the rule function as expected.</span></span>

   <span data-ttu-id="a02ad-113">Utilisez un moteur de recherche ou tout autre outil en ligne pour vérifier votre adresse IP (par exemple, lancez une recherche « quelle est mon adresse IP »).</span><span class="sxs-lookup"><span data-stu-id="a02ad-113">Use a search engine or other online tool to check your own IP address (for example, search "what is my IP address").</span></span>

   ![Recherche Bing « quelle est mon adresse IP »](./media/howto-manage-firewall-using-portal/3-what-is-my-ip.png)

4. <span data-ttu-id="a02ad-115">Ajoutez des plages d’adresses supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="a02ad-115">Add additional address ranges.</span></span> <span data-ttu-id="a02ad-116">Dans les règles de pare-feu de la base de données MySQL, vous pouvez spécifier une seule adresse IP ou une plage d’adresses.</span><span class="sxs-lookup"><span data-stu-id="a02ad-116">In the rules for the Azure Database for MySQL firewall, you can specify a single IP address, or a range of addresses.</span></span> <span data-ttu-id="a02ad-117">Si vous souhaitez limiter la règle à une seule adresse IP, saisissez la même adresse dans le champ d’adresse IP de début et d’adresse IP de fin.</span><span class="sxs-lookup"><span data-stu-id="a02ad-117">If you want to limit the rule to one single IP address, type the same address in the field for Start IP and End IP.</span></span> <span data-ttu-id="a02ad-118">Ouvrir le pare-feu permet aux administrateurs et utilisateurs d’accéder à toute base de données sur le serveur MySQL pour laquelle ils disposent d’informations d’identification valides.</span><span class="sxs-lookup"><span data-stu-id="a02ad-118">Opening the firewall enables administrators and users to access any database on the MySQL server to which they have valid credentials.</span></span>

   ![<span data-ttu-id="a02ad-119">Portail Azure - règles de pare-feu</span><span class="sxs-lookup"><span data-stu-id="a02ad-119">Azure portal - firewall rules</span></span> ](./media/howto-manage-firewall-using-portal/5-specify-addresses.png)


5. <span data-ttu-id="a02ad-120">Cliquez sur **Enregistrer** sur la barre d’outils pour enregistrer cette règle de pare-feu de niveau serveur.</span><span class="sxs-lookup"><span data-stu-id="a02ad-120">Click **Save** on the toolbar to save this server-level firewall rule.</span></span> <span data-ttu-id="a02ad-121">Attendez la confirmation que la mise à jour des règles de pare-feu a réussi.</span><span class="sxs-lookup"><span data-stu-id="a02ad-121">Wait for the confirmation that the update to the firewall rules was successful.</span></span>

   ![Portail Azure - cliquez sur Enregistrer](./media/howto-manage-firewall-using-portal/4-save-firewall-rule.png)

## <a name="manage-existing-server-level-firewall-rules-through-the-azure-portal"></a><span data-ttu-id="a02ad-123">Gérer des règles de pare-feu au niveau du serveur existantes via le portail Azure</span><span class="sxs-lookup"><span data-stu-id="a02ad-123">Manage existing server-level firewall rules through the Azure portal</span></span>
<span data-ttu-id="a02ad-124">Répétez les étapes pour gérer les règles de pare-feu.</span><span class="sxs-lookup"><span data-stu-id="a02ad-124">Repeat the steps to manage the firewall rules.</span></span>
* <span data-ttu-id="a02ad-125">Pour ajouter l’ordinateur actuel, cliquez sur **Ajouter mon adresse IP**.</span><span class="sxs-lookup"><span data-stu-id="a02ad-125">To add the current computer, click **+ Add My IP**.</span></span>
* <span data-ttu-id="a02ad-126">Pour ajouter des adresses IP supplémentaires, remplissez les champs **Nom de la règle**, **Adresse IP de début** et **Adresse IP de fin**.</span><span class="sxs-lookup"><span data-stu-id="a02ad-126">To add additional IP addresses, type in the **RULE NAME**, **START IP**, and **END IP**.</span></span>
* <span data-ttu-id="a02ad-127">Pour modifier une règle existante, cliquez sur les champs dans la règle et modifiez-les.</span><span class="sxs-lookup"><span data-stu-id="a02ad-127">To modify an existing rule, click any of the fields in the rule and modify.</span></span>
* <span data-ttu-id="a02ad-128">Pour supprimer une règle existante, cliquez sur les points de suspension [...] puis sur **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="a02ad-128">To delete an existing rule, click the ellipsis […] and click **Delete**.</span></span>
* <span data-ttu-id="a02ad-129">Cliquez sur **Enregistrer** pour enregistrer les modifications.</span><span class="sxs-lookup"><span data-stu-id="a02ad-129">Click **Save** to save the changes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a02ad-130">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a02ad-130">Next steps</span></span>
- <span data-ttu-id="a02ad-131">Pour vous aider à vous connecter à un serveur Azure Database pour MySQL, consultez la rubrique [Bibliothèques de connexions pour Azure Database pour MySQL](./concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="a02ad-131">For help in connecting to an Azure Database for MySQL server, see [Connection libraries for Azure Database for MySQL](./concepts-connection-libraries.md)</span></span>
