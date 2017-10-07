---
title: "Comment tooback et restaurer un serveur de base de données Azure pour PostgreSQL | Documents Microsoft"
description: "Découvrez comment tooback haut et restaurer un serveur de base de données Azure pour PostgreSQL à l’aide de hello CLI d’Azure."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 0b9ed25e3e3a88dd5c7ffe2ae7c27f8eef9be710
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooback-up-and-restore-a-server-in-azure-database-for-postgresql-by-using-hello-azure-cli"></a><span data-ttu-id="6ee0d-103">Comment tooback des et restaurer un serveur de base de données Azure pour PostgreSQL à l’aide de hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="6ee0d-103">How tooback up and restore a server in Azure Database for PostgreSQL by using hello Azure CLI</span></span>

<span data-ttu-id="6ee0d-104">Utilisez base de données Azure pour PostgreSQL toorestore un tooan de base de données de serveur date antérieure qui s’étend du too35 des 7 derniers jours.</span><span class="sxs-lookup"><span data-stu-id="6ee0d-104">Use Azure Database for PostgreSQL toorestore a server database tooan earlier date that spans from 7 too35 days.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6ee0d-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="6ee0d-105">Prerequisites</span></span>
<span data-ttu-id="6ee0d-106">toocomplete cette procédure-tooguide, vous devez :</span><span class="sxs-lookup"><span data-stu-id="6ee0d-106">toocomplete this how-tooguide, you need:</span></span>
- <span data-ttu-id="6ee0d-107">Un [serveur Azure Database pour PostgreSQL et une base de données](quickstart-create-server-database-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="6ee0d-107">An [Azure Database for PostgreSQL server and database](quickstart-create-server-database-azure-cli.md)</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

 

> [!IMPORTANT]
> <span data-ttu-id="6ee0d-108">Si vous installez et utilisez hello CLI d’Azure localement, cette procédure-tooguide nécessite que vous utilisez Azure CLI 2.0 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="6ee0d-108">If you install and use hello Azure CLI locally, this how-tooguide requires that you use Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="6ee0d-109">version de hello tooconfirm, à l’invite de commande CLI d’Azure hello, entrez `az --version`.</span><span class="sxs-lookup"><span data-stu-id="6ee0d-109">tooconfirm hello version, at hello Azure CLI command prompt, enter `az --version`.</span></span> <span data-ttu-id="6ee0d-110">tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="6ee0d-110">tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="back-up-happens-automatically"></a><span data-ttu-id="6ee0d-111">La sauvegarde s’effectue automatiquement</span><span class="sxs-lookup"><span data-stu-id="6ee0d-111">Back up happens automatically</span></span>
<span data-ttu-id="6ee0d-112">Lorsque vous utilisez la base de données Azure pour PostgreSQL, service de base de données hello effectue automatiquement une sauvegarde du service de hello toutes les 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="6ee0d-112">When you use Azure Database for PostgreSQL, hello database service automatically makes a backup of hello service every 5 minutes.</span></span> 

<span data-ttu-id="6ee0d-113">Pour le niveau de base, les sauvegardes de hello sont disponibles pendant 7 jours.</span><span class="sxs-lookup"><span data-stu-id="6ee0d-113">For Basic Tier, hello backups are available for 7 days.</span></span> <span data-ttu-id="6ee0d-114">Pour le niveau Standard, les sauvegardes de hello sont disponibles pour des 35 derniers jours.</span><span class="sxs-lookup"><span data-stu-id="6ee0d-114">For Standard Tier, hello backups are available for 35 days.</span></span> <span data-ttu-id="6ee0d-115">Pour plus d’informations, consultez [Niveaux tarifaires dans Base de données Azure pour PostgreSQL](concepts-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="6ee0d-115">For more information, see [Azure Database for PostgreSQL pricing tiers](concepts-service-tiers.md).</span></span>

<span data-ttu-id="6ee0d-116">Avec cette fonctionnalité de sauvegarde automatique, vous pouvez restaurer les serveur hello et son tooan de bases de données de date antérieure, ou point dans le temps.</span><span class="sxs-lookup"><span data-stu-id="6ee0d-116">With this automatic backup feature, you can restore hello server and its databases tooan earlier date, or point in time.</span></span>

## <a name="restore-a-database-tooa-previous-point-in-time-by-using-hello-azure-cli"></a><span data-ttu-id="6ee0d-117">Restaurer un état antérieur de tooa de base de données dans le temps à l’aide de hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="6ee0d-117">Restore a database tooa previous point in time by using hello Azure CLI</span></span>
<span data-ttu-id="6ee0d-118">Utiliser la base de données Azure pour point précédent tooa de serveur hello PostgreSQL toorestore dans le temps.</span><span class="sxs-lookup"><span data-stu-id="6ee0d-118">Use Azure Database for PostgreSQL toorestore hello server tooa previous point in time.</span></span> <span data-ttu-id="6ee0d-119">les données de salutation restaurée sont tooa copié un nouveau serveur, et serveur existant de hello demeure en l’état.</span><span class="sxs-lookup"><span data-stu-id="6ee0d-119">hello restored data is copied tooa new server, and hello existing server is left as is.</span></span> <span data-ttu-id="6ee0d-120">Par exemple, si une table est supprimée par inadvertance à midi aujourd'hui, vous pouvez restaurer le temps toohello juste avant midi.</span><span class="sxs-lookup"><span data-stu-id="6ee0d-120">For example, if a table is accidentally dropped at noon today, you can restore toohello time just before noon.</span></span> <span data-ttu-id="6ee0d-121">Ensuite, vous pouvez récupérer hello manquant de table et les données à partir de la copie restaurée de hello du serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="6ee0d-121">Then, you can retrieve hello missing table and data from hello restored copy of hello server.</span></span> 

<span data-ttu-id="6ee0d-122">serveur de hello toorestore, utilisez hello CLI d’Azure [restauration du serveur az postgres](/cli/azure/postgres/server#restore) commande.</span><span class="sxs-lookup"><span data-stu-id="6ee0d-122">toorestore hello server, use hello Azure CLI [az postgres server restore](/cli/azure/postgres/server#restore) command.</span></span>

### <a name="run-hello-restore-command"></a><span data-ttu-id="6ee0d-123">Exécutez la commande de restauration hello</span><span class="sxs-lookup"><span data-stu-id="6ee0d-123">Run hello restore command</span></span>

<span data-ttu-id="6ee0d-124">serveur de hello toorestore, à l’invite de commande CLI d’Azure hello, entrez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="6ee0d-124">toorestore hello server, at hello Azure CLI command prompt, enter hello following command:</span></span>

```azurecli-interactive
az postgres server restore --resource-group myResourceGroup --name mypgserver-restored --restore-point-in-time 2017-04-13T13:59:00Z --source-server mypgserver-20170401
```

<span data-ttu-id="6ee0d-125">Hello `az postgres server restore` commande nécessite hello paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="6ee0d-125">hello `az postgres server restore` command requires hello following parameters:</span></span>
| <span data-ttu-id="6ee0d-126">Paramètre</span><span class="sxs-lookup"><span data-stu-id="6ee0d-126">Setting</span></span> | <span data-ttu-id="6ee0d-127">Valeur suggérée</span><span class="sxs-lookup"><span data-stu-id="6ee0d-127">Suggested value</span></span> | <span data-ttu-id="6ee0d-128">Description</span><span class="sxs-lookup"><span data-stu-id="6ee0d-128">Description</span></span>  |
| --- | --- | --- |
| <span data-ttu-id="6ee0d-129">resource-group</span><span class="sxs-lookup"><span data-stu-id="6ee0d-129">resource-group</span></span> |  <span data-ttu-id="6ee0d-130">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="6ee0d-130">myResourceGroup</span></span> |  <span data-ttu-id="6ee0d-131">Le groupe de ressources dans lequel le serveur de source de hello existe.</span><span class="sxs-lookup"><span data-stu-id="6ee0d-131">The resource group where hello source server exists.</span></span>  |
| <span data-ttu-id="6ee0d-132">name</span><span class="sxs-lookup"><span data-stu-id="6ee0d-132">name</span></span> | <span data-ttu-id="6ee0d-133">mypgserver-restored</span><span class="sxs-lookup"><span data-stu-id="6ee0d-133">mypgserver-restored</span></span> | <span data-ttu-id="6ee0d-134">nom Hello hello nouveau serveur qui est créé par la commande de restauration hello.</span><span class="sxs-lookup"><span data-stu-id="6ee0d-134">hello name of hello new server that is created by hello restore command.</span></span> |
| <span data-ttu-id="6ee0d-135">restore-point-in-time</span><span class="sxs-lookup"><span data-stu-id="6ee0d-135">restore-point-in-time</span></span> | <span data-ttu-id="6ee0d-136">2017-04-13T13:59:00Z</span><span class="sxs-lookup"><span data-stu-id="6ee0d-136">2017-04-13T13:59:00Z</span></span> | <span data-ttu-id="6ee0d-137">Sélectionnez un point dans toorestore de temps à.</span><span class="sxs-lookup"><span data-stu-id="6ee0d-137">Select a point in time toorestore to.</span></span> <span data-ttu-id="6ee0d-138">Cette date / heure doivent être dans hello du serveur source dans une période de rétention.</span><span class="sxs-lookup"><span data-stu-id="6ee0d-138">This date and time must be within hello source server's back up retention period.</span></span> <span data-ttu-id="6ee0d-139">Utilisez le format de date et d’heure hello ISO8601.</span><span class="sxs-lookup"><span data-stu-id="6ee0d-139">Use hello ISO8601 date and time format.</span></span> <span data-ttu-id="6ee0d-140">Par exemple, vous pouvez utiliser votre fuseau horaire local, comme `2017-04-13T05:59:00-08:00`.</span><span class="sxs-lookup"><span data-stu-id="6ee0d-140">For example, you can use your own local time zone, such as `2017-04-13T05:59:00-08:00`.</span></span> <span data-ttu-id="6ee0d-141">Vous pouvez également utiliser hello UTC Zoulou mettre en forme, par exemple, `2017-04-13T13:59:00Z`.</span><span class="sxs-lookup"><span data-stu-id="6ee0d-141">You can also use hello UTC Zulu format, for example, `2017-04-13T13:59:00Z`.</span></span> |
| <span data-ttu-id="6ee0d-142">source-server</span><span class="sxs-lookup"><span data-stu-id="6ee0d-142">source-server</span></span> | <span data-ttu-id="6ee0d-143">mypgserver-20170401</span><span class="sxs-lookup"><span data-stu-id="6ee0d-143">mypgserver-20170401</span></span> | <span data-ttu-id="6ee0d-144">nom de Hello ou ID de hello toorestore de serveur source à partir de.</span><span class="sxs-lookup"><span data-stu-id="6ee0d-144">hello name or ID of hello source server toorestore from.</span></span> |

<span data-ttu-id="6ee0d-145">Lorsque vous restaurez un serveur tooan point antérieur dans le temps, un nouveau serveur est créé.</span><span class="sxs-lookup"><span data-stu-id="6ee0d-145">When you restore a server tooan earlier point in time, a new server is created.</span></span> <span data-ttu-id="6ee0d-146">serveur d’origine de Hello et ses bases de données à partir de hello spécifié de point dans le temps sont copiés toohello nouveau serveur.</span><span class="sxs-lookup"><span data-stu-id="6ee0d-146">hello original server and its databases from hello specified point in time are copied toohello new server.</span></span>

<span data-ttu-id="6ee0d-147">valeurs de niveau de Hello emplacement et la tarification pour le serveur hello restauré sont toujours hello même en tant que serveur d’origine de hello.</span><span class="sxs-lookup"><span data-stu-id="6ee0d-147">hello location and pricing tier values for hello restored server remain hello same as hello original server.</span></span> 

<span data-ttu-id="6ee0d-148">Hello `az postgres server restore` commande est synchrone.</span><span class="sxs-lookup"><span data-stu-id="6ee0d-148">hello `az postgres server restore` command is synchronous.</span></span> <span data-ttu-id="6ee0d-149">Après que hello serveur est restauré, vous pouvez l’utiliser à nouveau processus de hello toorepeat pour un autre point dans le temps.</span><span class="sxs-lookup"><span data-stu-id="6ee0d-149">After hello server is restored, you can use it again toorepeat hello process for a different point in time.</span></span> 

<span data-ttu-id="6ee0d-150">Après avoir hello se termine le processus de restauration, recherche hello nouveau serveur et vérifier que les données de salutation sont restaurées comme prévu.</span><span class="sxs-lookup"><span data-stu-id="6ee0d-150">After hello restore process finishes, locate hello new server and verify that hello data is restored as expected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6ee0d-151">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6ee0d-151">Next steps</span></span>
[<span data-ttu-id="6ee0d-152">Bibliothèques de connexions pour Azure Database pour PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="6ee0d-152">Connection libraries for Azure Database for PostgreSQL</span></span>](concepts-connection-libraries.md)
