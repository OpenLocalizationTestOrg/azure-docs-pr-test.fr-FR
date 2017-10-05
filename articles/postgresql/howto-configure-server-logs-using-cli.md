---
title: "Configuration et accès aux journaux du serveur pour PostgreSQL à l’aide de la ligne de commande Azure | Microsoft Docs"
description: "Cet article décrit comment configurer les journaux du serveur dans Azure Database pour PostgreSQL à l’aide de l’interface de ligne de commande Azure, et comment y accéder."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 26f8e12c493904f722cad5191ee053feff20f7fc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="configure-and-access-server-logs-using-azure-cli"></a><span data-ttu-id="79bd9-103">Configuration et accès aux journaux du serveur à l’aide de la ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="79bd9-103">Configure and access server logs using Azure CLI</span></span>
<span data-ttu-id="79bd9-104">Vous pouvez télécharger les journaux d’erreurs du serveur PostgreSQL à l’aide de l’interface de ligne de commande Azure.</span><span class="sxs-lookup"><span data-stu-id="79bd9-104">You can download the PostgreSQL server error logs using the Command Line Interface (Azure CLI).</span></span> <span data-ttu-id="79bd9-105">Toutefois, l’accès aux journaux des transactions n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="79bd9-105">However, access to transaction logs is not supported.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="79bd9-106">Prérequis</span><span class="sxs-lookup"><span data-stu-id="79bd9-106">Prerequisites</span></span>
<span data-ttu-id="79bd9-107">Pour parcourir ce guide pratique, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="79bd9-107">To step through this how-to guide, you need:</span></span>
- <span data-ttu-id="79bd9-108">Un [serveur Azure Database pour PostgreSQL](quickstart-create-server-database-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="79bd9-108">An [Azure Database for PostgreSQL server](quickstart-create-server-database-azure-cli.md)</span></span>
- <span data-ttu-id="79bd9-109">Installer l’utilitaire de ligne de commande [Azure CLI 2.0](/cli/azure/install-azure-cli) ou utiliser Azure Cloud Shell dans le navigateur.</span><span class="sxs-lookup"><span data-stu-id="79bd9-109">Install [Azure CLI 2.0](/cli/azure/install-azure-cli) command-line utility or use the Azure Cloud Shell in the browser.</span></span>

## <a name="configure-logging-for-azure-database-for-postgresql"></a><span data-ttu-id="79bd9-110">Configuration de la journalisation pour Azure Database pour PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="79bd9-110">Configure logging for Azure Database for PostgreSQL</span></span>
<span data-ttu-id="79bd9-111">Vous pouvez configurer le serveur afin d’accéder aux journaux de requêtes et aux journaux d’erreurs.</span><span class="sxs-lookup"><span data-stu-id="79bd9-111">You can configure the server to access query logs and error logs.</span></span> <span data-ttu-id="79bd9-112">Les journaux d’erreurs peuvent contenir des informations sur le nettoyage automatique, la connexion et les points de contrôle.</span><span class="sxs-lookup"><span data-stu-id="79bd9-112">Error logs can contain auto-vacuum, connection, and checkpoints information.</span></span>
1. <span data-ttu-id="79bd9-113">Activation de la journalisation</span><span class="sxs-lookup"><span data-stu-id="79bd9-113">Turn on logging</span></span>
2. <span data-ttu-id="79bd9-114">Mise à jour de l\_’instruction de journalisation et de l’instruction de\_ \_durée minimale\_de journalisation pour activer la journalisation des requêtes</span><span class="sxs-lookup"><span data-stu-id="79bd9-114">Update log\_statement and log\_min\_duration\_statement to enable query logging</span></span>
3. <span data-ttu-id="79bd9-115">Mise à jour de la période de rétention</span><span class="sxs-lookup"><span data-stu-id="79bd9-115">Update retention period</span></span>

<span data-ttu-id="79bd9-116">Pour plus d’informations, consultez [Personnalisation des paramètres de configuration du serveur](howto-configure-server-parameters-using-cli.md).</span><span class="sxs-lookup"><span data-stu-id="79bd9-116">For more information, see [customizing server configuration parameters](howto-configure-server-parameters-using-cli.md).</span></span>

## <a name="list-logs-for-azure-database-for-postgresql-server"></a><span data-ttu-id="79bd9-117">Répertorier les journaux pour le serveur Azure Database pour PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="79bd9-117">List logs for Azure Database for PostgreSQL server</span></span>
<span data-ttu-id="79bd9-118">Pour répertorier les fichiers journaux disponibles pour votre serveur, exécutez la commande [az postgres server-logs list](/cli/azure/postgres/server-logs#list).</span><span class="sxs-lookup"><span data-stu-id="79bd9-118">To list the available log files for your server, run the [az postgres server-logs list](/cli/azure/postgres/server-logs#list) command.</span></span>

<span data-ttu-id="79bd9-119">Vous pouvez répertorier les fichiers journaux pour le serveur **mypgserver-20170401.postgres.database.azure.com** sous le groupe de ressources **myresourcegroup** et les diriger vers un fichier texte appelé **liste\_fichiers\_journaux.txt.**</span><span class="sxs-lookup"><span data-stu-id="79bd9-119">You can list the log files for server **mypgserver-20170401.postgres.database.azure.com** under Resource Group **myresourcegroup**, and direct it to a text file called **log\_files\_list.txt.**</span></span>
```azurecli-interactive
az postgres server-logs list --resource-group myresourcegroup --server mypgserver-20170401 > log_files_list.txt
```
## <a name="download-logs-locally-from-the-server"></a><span data-ttu-id="79bd9-120">Téléchargement des journaux localement à partir du serveur</span><span class="sxs-lookup"><span data-stu-id="79bd9-120">Download logs locally from the server</span></span>
<span data-ttu-id="79bd9-121">La commande [az postgres server-logs download](/cli/azure/postgres/server-logs#download) vous permet de télécharger des fichiers journaux individuels pour votre serveur.</span><span class="sxs-lookup"><span data-stu-id="79bd9-121">The [az postgres server-logs download](/cli/azure/postgres/server-logs#download) command allows you to download individual log files for your server.</span></span> 

<span data-ttu-id="79bd9-122">Cet exemple télécharge le fichier journal spécifique pour le serveur **mypgserver-20170401.postgres.database.azure.com** sous le groupe de ressources **myresourcegroup** dans votre environnement local.</span><span class="sxs-lookup"><span data-stu-id="79bd9-122">This example downloads the specific log file for the server **mypgserver-20170401.postgres.database.azure.com** under Resource Group **myresourcegroup** to your local environment.</span></span>
```azurecli-interactive
az postgres server-logs download --name 20170414-mypgserver-20170401-postgresql.log --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="next-steps"></a><span data-ttu-id="79bd9-123">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="79bd9-123">Next steps</span></span>
- <span data-ttu-id="79bd9-124">Pour en savoir plus sur les journaux de serveur, consultez la rubrique [Journaux de serveur dans la base de données Azure pour PostgreSQL](concepts-server-logs.md)</span><span class="sxs-lookup"><span data-stu-id="79bd9-124">To learn more about server logs, see [Server Logs in Azure Database for PostgreSQL](concepts-server-logs.md)</span></span>
- <span data-ttu-id="79bd9-125">Pour plus d’informations sur les paramètres du serveur, consultez la rubrique [Personnalisation des paramètres de configuration de serveur à l’aide de l’interface de ligne de commande Azure](howto-configure-server-parameters-using-cli.md)</span><span class="sxs-lookup"><span data-stu-id="79bd9-125">For more information on server parameters, see [Customize server configuration parameters using Azure CLI](howto-configure-server-parameters-using-cli.md)</span></span>
