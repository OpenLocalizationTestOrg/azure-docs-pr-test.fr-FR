---
title: "aaaCreate et gérer la base de données Azure PostgreSQL aux règles de pare-feu à l’aide de hello portail Azure | Documents Microsoft"
description: "Créer et gérer la base de données Azure PostgreSQL aux règles de pare-feu à l’aide de hello portail Azure"
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 6a41a077168657769e442401e9df9931aa809240
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-postgresql-firewall-rules-using-hello-azure-portal"></a><span data-ttu-id="261d6-103">Créer et gérer la base de données Azure PostgreSQL aux règles de pare-feu à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="261d6-103">Create and manage Azure Database for PostgreSQL firewall rules using hello Azure portal</span></span>
<span data-ttu-id="261d6-104">Les règles de pare-feu de niveau serveur activer administrateurs tooaccess une base de données Azure pour PostgreSQL serveur à partir d’une adresse IP spécifiée ou la plage d’adresses IP.</span><span class="sxs-lookup"><span data-stu-id="261d6-104">Server-level firewall rules enable administrators tooaccess an Azure Database for PostgreSQL Server from a specified IP address or range of IP addresses.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="261d6-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="261d6-105">Prerequisites</span></span>
<span data-ttu-id="261d6-106">toostep via ce tooguide de procédure, vous devez :</span><span class="sxs-lookup"><span data-stu-id="261d6-106">toostep through this how-tooguide, you need:</span></span>
- <span data-ttu-id="261d6-107">Un serveur [Création d’une base de données Azure pour PostgreSQL](quickstart-create-server-database-portal.md)</span><span class="sxs-lookup"><span data-stu-id="261d6-107">A server [Create an Azure Database for PostgreSQL](quickstart-create-server-database-portal.md)</span></span>

## <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a><span data-ttu-id="261d6-108">Créer une règle de pare-feu de niveau serveur dans hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="261d6-108">Create a server-level firewall rule in hello Azure portal</span></span>
1. <span data-ttu-id="261d6-109">Sur le panneau serveur PostgreSQL hello, sous paramètres de titre, cliquez sur **sécurité de connexion** Panneau de sécurité de connexion tooopen hello pour hello Azure base de données PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="261d6-109">On hello PostgreSQL server blade, under Settings heading, click **Connection Security** tooopen hello Connection Security blade for hello Azure Database for PostgreSQL.</span></span>

  ![Portail Azure - cliquez sur Sécurité des connexions](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. <span data-ttu-id="261d6-111">Cliquez sur **ajouter une adresse IP Mes** sur la barre d’outils hello.</span><span class="sxs-lookup"><span data-stu-id="261d6-111">Click **Add My IP** on hello toolbar.</span></span> <span data-ttu-id="261d6-112">Cela crée une règle automatiquement avec l’adresse IP de hello de votre ordinateur, comme perçue par hello système Azure.</span><span class="sxs-lookup"><span data-stu-id="261d6-112">This will create a rule automatically with hello IP address of your computer, as perceived by hello Azure system.</span></span>

  ![Portail Azure - cliquez sur Ajouter mon adresse IP](./media/howto-manage-firewall-using-portal/2-add-my-ip.png)

3. <span data-ttu-id="261d6-114">Vérifiez votre adresse IP avant d’enregistrer la configuration de hello.</span><span class="sxs-lookup"><span data-stu-id="261d6-114">Verify your IP address before saving hello configuration.</span></span> <span data-ttu-id="261d6-115">Dans certaines situations, adresse IP de hello observée par le portail Azure diffère à partir de l’adresse IP de hello utilisée lorsque l’accès à hello internet et les serveurs Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="261d6-115">In some situations, hello IP address observed by Azure portal differs from hello IP address used when accessing hello internet and Azure servers.</span></span> <span data-ttu-id="261d6-116">Par conséquent, vous devrez peut-être toochange hello IP de début et de fin IP toomake hello règle fonctionnent comme prévu.</span><span class="sxs-lookup"><span data-stu-id="261d6-116">Therefore, you may need toochange hello Start IP and End IP toomake hello rule function as expected.</span></span>
<span data-ttu-id="261d6-117">Utiliser un moteur de recherche ou d’autres toocheck de l’outil en ligne de votre adresse IP (par exemple, la recherche Bing « quel est mon IP »).</span><span class="sxs-lookup"><span data-stu-id="261d6-117">Use a search engine or other online tool toocheck your own IP address (for example, Bing search "what is my IP").</span></span>

  ![Recherche Bing « quelle est mon adresse IP »](./media/howto-manage-firewall-using-portal/3-what-is-my-ip.png)

4. <span data-ttu-id="261d6-119">Ajoutez des plages d’adresses supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="261d6-119">Add additional address ranges.</span></span> <span data-ttu-id="261d6-120">Dans règles de hello pour hello Azure de base de données PostgreSQL pare-feu, vous pouvez spécifier une adresse IP unique, ou une plage d’adresses.</span><span class="sxs-lookup"><span data-stu-id="261d6-120">In hello rules for hello Azure Database for PostgreSQL firewall, you can specify a single IP address, or a range of addresses.</span></span> <span data-ttu-id="261d6-121">Si vous souhaitez toolimit hello règle tooone adresse IP unique, hello type identique à une adresse dans le champ de hello pour IP de début et IP de fin.</span><span class="sxs-lookup"><span data-stu-id="261d6-121">If you want toolimit hello rule tooone single IP address, type hello same address in hello field for Start IP and End IP.</span></span> <span data-ttu-id="261d6-122">Ouvrir le pare-feu hello permet aux administrateurs et utilisateurs toologin tooany base de données sur hello PostgreSQL toowhich de serveur disposent des informations d’identification valides.</span><span class="sxs-lookup"><span data-stu-id="261d6-122">Opening hello firewall enables administrators and users toologin tooany database on hello PostgreSQL server toowhich they have valid credentials.</span></span>

  ![<span data-ttu-id="261d6-123">Portail Azure - règles de pare-feu</span><span class="sxs-lookup"><span data-stu-id="261d6-123">Azure portal - firewall rules</span></span> ](./media/howto-manage-firewall-using-portal/4-specify-addresses.png)

5. <span data-ttu-id="261d6-124">Cliquez sur **enregistrer** sur hello toosave de barre d’outils, cette règle de pare-feu de niveau serveur.</span><span class="sxs-lookup"><span data-stu-id="261d6-124">Click **Save** on hello toolbar toosave this server-level firewall rule.</span></span> <span data-ttu-id="261d6-125">Attendez la confirmation de hello que les règles de pare-feu toohello hello mise à jour a réussi.</span><span class="sxs-lookup"><span data-stu-id="261d6-125">Wait for hello confirmation that hello update toohello firewall rules was successful.</span></span>

  ![Portail Azure - cliquez sur Enregistrer](./media/howto-manage-firewall-using-portal/5-save-firewall-rule.png)


## <a name="manage-existing-server-level-firewall-rules-through-hello-azure-portal"></a><span data-ttu-id="261d6-127">Gérer les règles de pare-feu de niveau serveur existante via hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="261d6-127">Manage existing server-level firewall rules through hello Azure portal</span></span>
<span data-ttu-id="261d6-128">Répétez les règles de pare-feu hello étapes toomanage hello.</span><span class="sxs-lookup"><span data-stu-id="261d6-128">Repeat hello steps toomanage hello firewall rules.</span></span>
* <span data-ttu-id="261d6-129">tooadd hello ordinateur en cours, cliquez sur le bouton de hello + **ajouter une adresse IP Mes**.</span><span class="sxs-lookup"><span data-stu-id="261d6-129">tooadd hello current computer, click hello button too+ **Add My IP**.</span></span> <span data-ttu-id="261d6-130">Cliquez sur **enregistrer** modifications de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="261d6-130">Click **Save** toosave hello changes.</span></span>
* <span data-ttu-id="261d6-131">tooadd des adresses IP supplémentaires, tapez Bonjour, nom de la règle, adresse IP de début et adresse IP de fin.</span><span class="sxs-lookup"><span data-stu-id="261d6-131">tooadd additional IP addresses, type in hello Rule Name, Start IP Address, and End IP Address.</span></span> <span data-ttu-id="261d6-132">Cliquez sur **enregistrer** modifications de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="261d6-132">Click **Save** toosave hello changes.</span></span>
* <span data-ttu-id="261d6-133">toomodify une règle existante, cliquez sur un des champs hello dans la règle de hello et modifier.</span><span class="sxs-lookup"><span data-stu-id="261d6-133">toomodify an existing rule, click any of hello fields in hello rule and modify.</span></span> <span data-ttu-id="261d6-134">Cliquez sur **enregistrer** modifications de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="261d6-134">Click **Save** toosave hello changes.</span></span>
* <span data-ttu-id="261d6-135">toodelete une règle existante, sur hello de points de suspension [...], puis cliquez sur Supprimer la règle hello remove.</span><span class="sxs-lookup"><span data-stu-id="261d6-135">toodelete an existing rule, click hello ellipsis […] and click Delete remove hello rule.</span></span> <span data-ttu-id="261d6-136">Cliquez sur **enregistrer** modifications de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="261d6-136">Click **Save** toosave hello changes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="261d6-137">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="261d6-137">Next steps</span></span>
- <span data-ttu-id="261d6-138">De même, vous pouvez écrire un script trop[créer et gérer la base de données Azure PostgreSQL aux règles de pare-feu à l’aide de CLI d’Azure](howto-manage-firewall-using-cli.md)</span><span class="sxs-lookup"><span data-stu-id="261d6-138">Similarly, you can script too[Create and manage Azure Database for PostgreSQL firewall rules using Azure CLI](howto-manage-firewall-using-cli.md)</span></span>
- <span data-ttu-id="261d6-139">Pour la connexion tooan Azure de base de données PostgreSQL serveur, consultez [bibliothèques de connexions de base de données Azure pour PostgreSQL](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="261d6-139">For help in connecting tooan Azure Database for PostgreSQL server, see [Connection libraries for Azure Database for PostgreSQL](concepts-connection-libraries.md)</span></span>
