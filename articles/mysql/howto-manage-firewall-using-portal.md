---
title: "aaaCreate et gérer la base de données Azure MySQL aux règles de pare-feu à l’aide de hello portail Azure | Documents Microsoft"
description: "Créer et gérer la base de données Azure MySQL aux règles de pare-feu à l’aide de hello portail Azure"
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 30dbdde4299df564fbf6581419e908186fe3b823
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-mysql-firewall-rules-using-hello-azure-portal"></a><span data-ttu-id="23f0e-103">Créer et gérer la base de données Azure MySQL aux règles de pare-feu à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="23f0e-103">Create and manage Azure Database for MySQL firewall rules using hello Azure portal</span></span>
<span data-ttu-id="23f0e-104">Les règles de pare-feu de niveau serveur activer administrateurs tooaccess une base de données Azure pour MySQL Server à partir d’une adresse IP spécifiée ou la plage d’adresses IP.</span><span class="sxs-lookup"><span data-stu-id="23f0e-104">Server-level firewall rules enable administrators tooaccess an Azure Database for MySQL Server from a specified IP address or range of IP addresses.</span></span> 

## <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a><span data-ttu-id="23f0e-105">Créer une règle de pare-feu de niveau serveur dans hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="23f0e-105">Create a server-level firewall rule in hello Azure portal</span></span>

1. <span data-ttu-id="23f0e-106">Sur le panneau de serveur MySQL hello, sous paramètres de titre, cliquez sur **sécurité de connexion** Panneau de sécurité de connexion tooopen hello pour hello Azure de base de données de MySQL.</span><span class="sxs-lookup"><span data-stu-id="23f0e-106">On hello MySQL server blade, under Settings heading, click **Connection Security** tooopen hello Connection Security blade for hello Azure Database for MySQL.</span></span>

   ![Portail Azure - cliquez sur Sécurité des connexions](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. <span data-ttu-id="23f0e-108">Cliquez sur **ajouter une adresse IP Mes** sur la barre d’outils de hello toocreate une règle avec l’adresse IP de hello de votre ordinateur, comme perçue par hello système Azure.</span><span class="sxs-lookup"><span data-stu-id="23f0e-108">Click **Add My IP** on hello toolbar toocreate a rule with hello IP address of your computer, as perceived by hello Azure system.</span></span>

   ![Portail Azure - cliquez sur Ajouter mon adresse IP](./media/howto-manage-firewall-using-portal/2-add-my-ip.png)

3. <span data-ttu-id="23f0e-110">Vérifiez votre adresse IP avant d’enregistrer la configuration de hello.</span><span class="sxs-lookup"><span data-stu-id="23f0e-110">Verify your IP address before saving hello configuration.</span></span> <span data-ttu-id="23f0e-111">Dans certaines situations, adresse IP de hello observée par le portail Azure diffère à partir de l’adresse IP de hello utilisée lorsque l’accès à hello internet et les serveurs Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="23f0e-111">In some situations, hello IP address observed by Azure portal differs from hello IP address used when accessing hello internet and Azure servers.</span></span> <span data-ttu-id="23f0e-112">Par conséquent, vous devrez peut-être toochange hello IP de début et de fin IP toomake hello règle fonctionnent comme prévu.</span><span class="sxs-lookup"><span data-stu-id="23f0e-112">Therefore, you may need toochange hello Start IP and End IP toomake hello rule function as expected.</span></span>

   <span data-ttu-id="23f0e-113">Utiliser un moteur de recherche ou d’autres toocheck de l’outil en ligne de votre adresse IP (par exemple, recherchez « quel est mon adresse IP »).</span><span class="sxs-lookup"><span data-stu-id="23f0e-113">Use a search engine or other online tool toocheck your own IP address (for example, search "what is my IP address").</span></span>

   ![Recherche Bing « quelle est mon adresse IP »](./media/howto-manage-firewall-using-portal/3-what-is-my-ip.png)

4. <span data-ttu-id="23f0e-115">Ajoutez des plages d’adresses supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="23f0e-115">Add additional address ranges.</span></span> <span data-ttu-id="23f0e-116">Dans règles de hello pour hello Azure de base de données MySQL pare-feu, vous pouvez spécifier une adresse IP unique, ou une plage d’adresses.</span><span class="sxs-lookup"><span data-stu-id="23f0e-116">In hello rules for hello Azure Database for MySQL firewall, you can specify a single IP address, or a range of addresses.</span></span> <span data-ttu-id="23f0e-117">Si vous souhaitez toolimit hello règle tooone adresse IP unique, hello type identique à une adresse dans le champ de hello pour IP de début et IP de fin.</span><span class="sxs-lookup"><span data-stu-id="23f0e-117">If you want toolimit hello rule tooone single IP address, type hello same address in hello field for Start IP and End IP.</span></span> <span data-ttu-id="23f0e-118">Ouvrir le pare-feu hello permet tooaccess administrateurs et utilisateurs chaque base de données hello toowhich de serveur MySQL comportant des informations d’identification valides.</span><span class="sxs-lookup"><span data-stu-id="23f0e-118">Opening hello firewall enables administrators and users tooaccess any database on hello MySQL server toowhich they have valid credentials.</span></span>

   ![<span data-ttu-id="23f0e-119">Portail Azure - règles de pare-feu</span><span class="sxs-lookup"><span data-stu-id="23f0e-119">Azure portal - firewall rules</span></span> ](./media/howto-manage-firewall-using-portal/5-specify-addresses.png)


5. <span data-ttu-id="23f0e-120">Cliquez sur **enregistrer** sur hello toosave de barre d’outils, cette règle de pare-feu de niveau serveur.</span><span class="sxs-lookup"><span data-stu-id="23f0e-120">Click **Save** on hello toolbar toosave this server-level firewall rule.</span></span> <span data-ttu-id="23f0e-121">Attendez la confirmation de hello que les règles de pare-feu toohello hello mise à jour a réussi.</span><span class="sxs-lookup"><span data-stu-id="23f0e-121">Wait for hello confirmation that hello update toohello firewall rules was successful.</span></span>

   ![Portail Azure - cliquez sur Enregistrer](./media/howto-manage-firewall-using-portal/4-save-firewall-rule.png)

## <a name="manage-existing-server-level-firewall-rules-through-hello-azure-portal"></a><span data-ttu-id="23f0e-123">Gérer les règles de pare-feu de niveau serveur existante via hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="23f0e-123">Manage existing server-level firewall rules through hello Azure portal</span></span>
<span data-ttu-id="23f0e-124">Répétez les règles de pare-feu hello étapes toomanage hello.</span><span class="sxs-lookup"><span data-stu-id="23f0e-124">Repeat hello steps toomanage hello firewall rules.</span></span>
* <span data-ttu-id="23f0e-125">tooadd hello ordinateur en cours, cliquez sur **+ ajouter Mes IP**.</span><span class="sxs-lookup"><span data-stu-id="23f0e-125">tooadd hello current computer, click **+ Add My IP**.</span></span>
* <span data-ttu-id="23f0e-126">les adresses IP supplémentaires tooadd, tapez Bonjour **nom de la règle**, **IP de début**, et **IP de fin**.</span><span class="sxs-lookup"><span data-stu-id="23f0e-126">tooadd additional IP addresses, type in hello **RULE NAME**, **START IP**, and **END IP**.</span></span>
* <span data-ttu-id="23f0e-127">toomodify une règle existante, cliquez sur un des champs hello dans la règle de hello et modifier.</span><span class="sxs-lookup"><span data-stu-id="23f0e-127">toomodify an existing rule, click any of hello fields in hello rule and modify.</span></span>
* <span data-ttu-id="23f0e-128">règle de toodelete existant sur hello de points de suspension [...] et cliquez sur **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="23f0e-128">toodelete an existing rule, click hello ellipsis […] and click **Delete**.</span></span>
* <span data-ttu-id="23f0e-129">Cliquez sur **enregistrer** modifications de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="23f0e-129">Click **Save** toosave hello changes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="23f0e-130">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="23f0e-130">Next steps</span></span>
- <span data-ttu-id="23f0e-131">Pour vous aider à la connexion tooan base de données Azure pour le serveur MySQL, consultez [bibliothèques de connexions de base de données Azure pour MySQL](./concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="23f0e-131">For help in connecting tooan Azure Database for MySQL server, see [Connection libraries for Azure Database for MySQL](./concepts-connection-libraries.md)</span></span>
