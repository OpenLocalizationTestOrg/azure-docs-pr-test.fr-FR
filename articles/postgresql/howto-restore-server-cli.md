---
title: "Sauvegarde et restauration d’un serveur dans Base de données Azure pour PostgreSQL | Microsoft Docs"
description: "Découvrez comment sauvegarder et restaurer un serveur dans Base de données Azure pour PostgreSQL à l’aide de l’interface Azure CLI."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 871887e67d686a965a0648d2c6f0c72b3008db05
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-back-up-and-restore-a-server-in-azure-database-for-postgresql-by-using-the-azure-cli"></a><span data-ttu-id="6f5ee-103">Sauvegarde et restauration d’un serveur Base de données Azure pour PostgreSQL à l’aide de l’interface Azure CLI</span><span class="sxs-lookup"><span data-stu-id="6f5ee-103">How to back up and restore a server in Azure Database for PostgreSQL by using the Azure CLI</span></span>

<span data-ttu-id="6f5ee-104">Utilisez Base de données Azure pour PostgreSQL afin de restaurer une base de données de serveur à une date antérieure couvrant une période de 7 à 35 jours.</span><span class="sxs-lookup"><span data-stu-id="6f5ee-104">Use Azure Database for PostgreSQL to restore a server database to an earlier date that spans from 7 to 35 days.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6f5ee-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="6f5ee-105">Prerequisites</span></span>
<span data-ttu-id="6f5ee-106">Pour utiliser ce guide pratique, il vous faut :</span><span class="sxs-lookup"><span data-stu-id="6f5ee-106">To complete this how-to guide, you need:</span></span>
- <span data-ttu-id="6f5ee-107">Un [serveur Azure Database pour PostgreSQL et une base de données](quickstart-create-server-database-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="6f5ee-107">An [Azure Database for PostgreSQL server and database](quickstart-create-server-database-azure-cli.md)</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

 

> [!IMPORTANT]
> <span data-ttu-id="6f5ee-108">Si vous installez et utilisez l’interface Azure CLI localement, vous devez exécuter Azure CLI version 2.0 ou une version ultérieure pour mettre en œuvre la procédure décrite dans ce guide pratique.</span><span class="sxs-lookup"><span data-stu-id="6f5ee-108">If you install and use the Azure CLI locally, this how-to guide requires that you use Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="6f5ee-109">Pour vérifier la version, à l’invite de commande de l’interface Azure CLI, entrez `az --version`.</span><span class="sxs-lookup"><span data-stu-id="6f5ee-109">To confirm the version, at the Azure CLI command prompt, enter `az --version`.</span></span> <span data-ttu-id="6f5ee-110">Pour installer ou mettre à niveau l’interface Azure CLI, consultez [Installation d’Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="6f5ee-110">To install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="back-up-happens-automatically"></a><span data-ttu-id="6f5ee-111">La sauvegarde s’effectue automatiquement</span><span class="sxs-lookup"><span data-stu-id="6f5ee-111">Back up happens automatically</span></span>
<span data-ttu-id="6f5ee-112">Lorsque vous utilisez Base de données Azure pour PostgreSQL, le service de base de données crée automatiquement une sauvegarde du service toutes les 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="6f5ee-112">When you use Azure Database for PostgreSQL, the database service automatically makes a backup of the service every 5 minutes.</span></span> 

<span data-ttu-id="6f5ee-113">Pour le niveau De base, les sauvegardes sont disponibles pendant 7 jours.</span><span class="sxs-lookup"><span data-stu-id="6f5ee-113">For Basic Tier, the backups are available for 7 days.</span></span> <span data-ttu-id="6f5ee-114">Pour le niveau Standard, les sauvegardes sont disponibles pendant 35 jours.</span><span class="sxs-lookup"><span data-stu-id="6f5ee-114">For Standard Tier, the backups are available for 35 days.</span></span> <span data-ttu-id="6f5ee-115">Pour plus d’informations, consultez [Niveaux tarifaires dans Base de données Azure pour PostgreSQL](concepts-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="6f5ee-115">For more information, see [Azure Database for PostgreSQL pricing tiers](concepts-service-tiers.md).</span></span>

<span data-ttu-id="6f5ee-116">À l’aide de cette fonctionnalité de sauvegarde automatique, vous pouvez restaurer le serveur et ses bases de données à une date ou un état antérieur.</span><span class="sxs-lookup"><span data-stu-id="6f5ee-116">With this automatic backup feature, you can restore the server and its databases to an earlier date, or point in time.</span></span>

## <a name="restore-a-database-to-a-previous-point-in-time-by-using-the-azure-cli"></a><span data-ttu-id="6f5ee-117">Restaurer une base de données à un état antérieur à l’aide de l’interface Azure CLI</span><span class="sxs-lookup"><span data-stu-id="6f5ee-117">Restore a database to a previous point in time by using the Azure CLI</span></span>
<span data-ttu-id="6f5ee-118">Utilisez Base de données Azure pour PostgreSQL pour restaurer le serveur à un état antérieur.</span><span class="sxs-lookup"><span data-stu-id="6f5ee-118">Use Azure Database for PostgreSQL to restore the server to a previous point in time.</span></span> <span data-ttu-id="6f5ee-119">Les données restaurées sont copiées dans un nouveau serveur et le serveur existant est conservé tel quel.</span><span class="sxs-lookup"><span data-stu-id="6f5ee-119">The restored data is copied to a new server, and the existing server is left as is.</span></span> <span data-ttu-id="6f5ee-120">Par exemple, si une table est accidentellement supprimée à midi aujourd’hui, vous pouvez restaurer le serveur à l’état qu’il présentait juste avant midi.</span><span class="sxs-lookup"><span data-stu-id="6f5ee-120">For example, if a table is accidentally dropped at noon today, you can restore to the time just before noon.</span></span> <span data-ttu-id="6f5ee-121">Vous pouvez ensuite récupérer la table et les données manquantes à partir de la copie restaurée du serveur.</span><span class="sxs-lookup"><span data-stu-id="6f5ee-121">Then, you can retrieve the missing table and data from the restored copy of the server.</span></span> 

<span data-ttu-id="6f5ee-122">Pour restaurer le serveur, utilisez la commande [az postgres server restore](/cli/azure/postgres/server#restore) de l’interface Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="6f5ee-122">To restore the server, use the Azure CLI [az postgres server restore](/cli/azure/postgres/server#restore) command.</span></span>

### <a name="run-the-restore-command"></a><span data-ttu-id="6f5ee-123">Exécuter la commande de restauration</span><span class="sxs-lookup"><span data-stu-id="6f5ee-123">Run the restore command</span></span>

<span data-ttu-id="6f5ee-124">Pour restaurer le serveur, à l’invite de commande de l’interface Azure CLI, entrez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="6f5ee-124">To restore the server, at the Azure CLI command prompt, enter the following command:</span></span>

```azurecli-interactive
az postgres server restore --resource-group myResourceGroup --name mypgserver-restored --restore-point-in-time 2017-04-13T13:59:00Z --source-server mypgserver-20170401
```

<span data-ttu-id="6f5ee-125">La commande `az postgres server restore` requiert les paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="6f5ee-125">The `az postgres server restore` command requires the following parameters:</span></span>
| <span data-ttu-id="6f5ee-126">Paramètre</span><span class="sxs-lookup"><span data-stu-id="6f5ee-126">Setting</span></span> | <span data-ttu-id="6f5ee-127">Valeur suggérée</span><span class="sxs-lookup"><span data-stu-id="6f5ee-127">Suggested value</span></span> | <span data-ttu-id="6f5ee-128">Description</span><span class="sxs-lookup"><span data-stu-id="6f5ee-128">Description</span></span>  |
| --- | --- | --- |
| <span data-ttu-id="6f5ee-129">resource-group</span><span class="sxs-lookup"><span data-stu-id="6f5ee-129">resource-group</span></span> |  <span data-ttu-id="6f5ee-130">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="6f5ee-130">myResourceGroup</span></span> |  <span data-ttu-id="6f5ee-131">Groupe de ressources où se trouve le serveur source.</span><span class="sxs-lookup"><span data-stu-id="6f5ee-131">The resource group where the source server exists.</span></span>  |
| <span data-ttu-id="6f5ee-132">name</span><span class="sxs-lookup"><span data-stu-id="6f5ee-132">name</span></span> | <span data-ttu-id="6f5ee-133">mypgserver-restored</span><span class="sxs-lookup"><span data-stu-id="6f5ee-133">mypgserver-restored</span></span> | <span data-ttu-id="6f5ee-134">Nom du serveur créé par la commande de restauration.</span><span class="sxs-lookup"><span data-stu-id="6f5ee-134">The name of the new server that is created by the restore command.</span></span> |
| <span data-ttu-id="6f5ee-135">restore-point-in-time</span><span class="sxs-lookup"><span data-stu-id="6f5ee-135">restore-point-in-time</span></span> | <span data-ttu-id="6f5ee-136">2017-04-13T13:59:00Z</span><span class="sxs-lookup"><span data-stu-id="6f5ee-136">2017-04-13T13:59:00Z</span></span> | <span data-ttu-id="6f5ee-137">Sélectionnez un état antérieur auquel effectuer la restauration.</span><span class="sxs-lookup"><span data-stu-id="6f5ee-137">Select a point in time to restore to.</span></span> <span data-ttu-id="6f5ee-138">La date et l’heure doivent être comprises dans la période de rétention de la sauvegarde du serveur source.</span><span class="sxs-lookup"><span data-stu-id="6f5ee-138">This date and time must be within the source server's back up retention period.</span></span> <span data-ttu-id="6f5ee-139">Utilisez le format de date et d’heure ISO8601.</span><span class="sxs-lookup"><span data-stu-id="6f5ee-139">Use the ISO8601 date and time format.</span></span> <span data-ttu-id="6f5ee-140">Par exemple, vous pouvez utiliser votre fuseau horaire local, comme `2017-04-13T05:59:00-08:00`.</span><span class="sxs-lookup"><span data-stu-id="6f5ee-140">For example, you can use your own local time zone, such as `2017-04-13T05:59:00-08:00`.</span></span> <span data-ttu-id="6f5ee-141">Vous pouvez également utiliser le format UTC Zulu, par exemple, `2017-04-13T13:59:00Z`.</span><span class="sxs-lookup"><span data-stu-id="6f5ee-141">You can also use the UTC Zulu format, for example, `2017-04-13T13:59:00Z`.</span></span> |
| <span data-ttu-id="6f5ee-142">source-server</span><span class="sxs-lookup"><span data-stu-id="6f5ee-142">source-server</span></span> | <span data-ttu-id="6f5ee-143">mypgserver-20170401</span><span class="sxs-lookup"><span data-stu-id="6f5ee-143">mypgserver-20170401</span></span> | <span data-ttu-id="6f5ee-144">Nom ou identifiant du serveur source à partir duquel la restauration s’effectuera.</span><span class="sxs-lookup"><span data-stu-id="6f5ee-144">The name or ID of the source server to restore from.</span></span> |

<span data-ttu-id="6f5ee-145">Lorsque vous restaurez un serveur à un état antérieur, un nouveau serveur est créé.</span><span class="sxs-lookup"><span data-stu-id="6f5ee-145">When you restore a server to an earlier point in time, a new server is created.</span></span> <span data-ttu-id="6f5ee-146">Le serveur d’origine et ses bases de données à l’état spécifié sont copiés sur le nouveau serveur.</span><span class="sxs-lookup"><span data-stu-id="6f5ee-146">The original server and its databases from the specified point in time are copied to the new server.</span></span>

<span data-ttu-id="6f5ee-147">Les valeurs d’emplacement et de niveau tarifaire du serveur restauré restent les mêmes que celles du serveur d’origine.</span><span class="sxs-lookup"><span data-stu-id="6f5ee-147">The location and pricing tier values for the restored server remain the same as the original server.</span></span> 

<span data-ttu-id="6f5ee-148">La commande `az postgres server restore` est synchrone.</span><span class="sxs-lookup"><span data-stu-id="6f5ee-148">The `az postgres server restore` command is synchronous.</span></span> <span data-ttu-id="6f5ee-149">Une fois le serveur restauré, vous pouvez l’utiliser à nouveau afin de répéter la procédure pour un autre état.</span><span class="sxs-lookup"><span data-stu-id="6f5ee-149">After the server is restored, you can use it again to repeat the process for a different point in time.</span></span> 

<span data-ttu-id="6f5ee-150">Une fois la restauration terminée, recherchez le nouveau serveur et vérifiez que les données ont été restaurées correctement.</span><span class="sxs-lookup"><span data-stu-id="6f5ee-150">After the restore process finishes, locate the new server and verify that the data is restored as expected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6f5ee-151">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6f5ee-151">Next steps</span></span>
[<span data-ttu-id="6f5ee-152">Bibliothèques de connexions pour Azure Database pour PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="6f5ee-152">Connection libraries for Azure Database for PostgreSQL</span></span>](concepts-connection-libraries.md)
