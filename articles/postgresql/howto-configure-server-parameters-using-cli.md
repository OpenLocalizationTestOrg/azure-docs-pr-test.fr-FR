---
title: "Configuration des paramètres de service dans Azure Database pour PostgreSQL | Microsoft Docs"
description: "Cet article décrit comment configurer les paramètres du service dans Azure Database pour PostgreSQL à l’aide de l’interface de ligne de commande (CLI) Azure."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: c8a3b5a0225c2cede180d8d57681f2e1a6c6cc3a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="customize-server-configuration-parameters-using-azure-cli"></a><span data-ttu-id="e2404-103">Personnalisation des paramètres de configuration du serveur à l’aide de l’interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="e2404-103">Customize server configuration parameters using Azure CLI</span></span>
<span data-ttu-id="e2404-104">Vous pouvez répertorier, afficher et mettre à jour les paramètres de configuration d’un serveur Azure PostgreSQL à l’aide de l’interface de ligne de commande (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="e2404-104">You can list, show and update configuration parameters for an Azure PostgreSQL server using the Command Line Interface (Azure CLI).</span></span> <span data-ttu-id="e2404-105">Toutefois, un seul sous-ensemble de configurations de moteur est exposé au niveau du serveur et peut être modifié.</span><span class="sxs-lookup"><span data-stu-id="e2404-105">However, only a subset of engine configurations are exposed at server-level and can be modified.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="e2404-106">Composants requis</span><span class="sxs-lookup"><span data-stu-id="e2404-106">Prerequisites</span></span>
<span data-ttu-id="e2404-107">Pour parcourir ce guide pratique, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="e2404-107">To step through this how-to guide, you need:</span></span>
- <span data-ttu-id="e2404-108">Un serveur et une base de données [Création d’une base de données Azure POUR PostgreSQL](quickstart-create-server-database-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="e2404-108">A server and database [Create an Azure Database for PostgreSQL](quickstart-create-server-database-azure-cli.md)</span></span>
- <span data-ttu-id="e2404-109">Installer l’utilitaire de ligne de commande [Azure CLI 2.0](/cli/azure/install-azure-cli) ou utiliser Azure Cloud Shell dans le navigateur.</span><span class="sxs-lookup"><span data-stu-id="e2404-109">Install [Azure CLI 2.0](/cli/azure/install-azure-cli) command line utility or use the Azure Cloud Shell in the browser.</span></span>

## <a name="list-server-configuration-parameters-for-azure-database-for-postgresql-server"></a><span data-ttu-id="e2404-110">Répertorier les paramètres de configuration de Base de données Azure pour le serveur PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="e2404-110">List server configuration parameters for Azure Database for PostgreSQL server</span></span>
<span data-ttu-id="e2404-111">Pour répertorier tous les paramètres modifiables dans un serveur, ainsi que leurs valeurs, exécutez la commande [az postgres server configuration list](/cli/azure/postgres/server/configuration#list).</span><span class="sxs-lookup"><span data-stu-id="e2404-111">To list all modifiable parameters in a server and their values, run the [az postgres server configuration list](/cli/azure/postgres/server/configuration#list) command.</span></span>

<span data-ttu-id="e2404-112">Par exemple, vous pouvez répertorier les paramètres de configuration du serveur **mypgserver-20170401.postgres.database.azure.com** du groupe de ressources **myresourcegroup**.</span><span class="sxs-lookup"><span data-stu-id="e2404-112">You can list the server configuration parameters for the server **mypgserver-20170401.postgres.database.azure.com** under resource group **myresourcegroup**.</span></span>
```azurecli-interactive
az postgres server configuration list --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="show-server-configuration-parameter-details"></a><span data-ttu-id="e2404-113">Affichage des détails des paramètres de configuration du serveur</span><span class="sxs-lookup"><span data-stu-id="e2404-113">Show server configuration parameter details</span></span>
<span data-ttu-id="e2404-114">Pour afficher les détails d’un paramètre de configuration particulier pour un serveur, exécutez la commande [az postgres server configuration show](/cli/azure/postgres/server/configuration#show).</span><span class="sxs-lookup"><span data-stu-id="e2404-114">To show details about a particular configuration parameter for a server, run the [az postgres server configuration show](/cli/azure/postgres/server/configuration#show)  command.</span></span>

<span data-ttu-id="e2404-115">Cet exemple affiche les détails du paramètre de configuration de serveur **log\_min\_messages** pour le serveur **mypgserver-20170401.postgres.database.azure.com** du groupe de ressources **myresourcegroup.**</span><span class="sxs-lookup"><span data-stu-id="e2404-115">This example shows details of the **log\_min\_messages** server configuration parameter for server **mypgserver-20170401.postgres.database.azure.com** under resource group **myresourcegroup.**</span></span>
```azurecli-interactive
az postgres server configuration show --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="modify-server-configuration-parameter-value"></a><span data-ttu-id="e2404-116">Modification de la valeur de paramètre de configuration du serveur</span><span class="sxs-lookup"><span data-stu-id="e2404-116">Modify server configuration parameter value</span></span>
<span data-ttu-id="e2404-117">Vous pouvez également modifier la valeur d’un paramètre de configuration de serveur, ce qui a pour effet de mettre à jour la valeur de configuration sous-jacente du moteur du serveur PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="e2404-117">You can also modify the value of a certain server configuration parameter, and this updates the underlying configuration value for the PostgreSQL server engine.</span></span> <span data-ttu-id="e2404-118">Pour mettre à jour la configuration, exécutez la commande [az postgres server configuration set](/cli/azure/postgres/server/configuration#set).</span><span class="sxs-lookup"><span data-stu-id="e2404-118">To update the configuration use the [az postgres server configuration set](/cli/azure/postgres/server/configuration#set) command.</span></span> 

<span data-ttu-id="e2404-119">Pour mettre à jour le paramètre de configuration de serveur **log\_min\_messages** pour le serveur **mypgserver-20170401.postgres.database.azure.com** du groupe de ressources **myresourcegroup**.</span><span class="sxs-lookup"><span data-stu-id="e2404-119">To update the **log\_min\_messages** server configuration parameter of server **mypgserver-20170401.postgres.database.azure.com** under resource group **myresourcegroup.**</span></span>
```azurecli-interactive
az postgres server configuration set --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401 --value INFO
```
<span data-ttu-id="e2404-120">Si vous souhaitez réinitialiser la valeur d’un paramètre de configuration, il vous suffit de ne pas définir le paramètre `--value` facultatif. Le service applique alors la valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="e2404-120">If you want to reset the value of a configuration parameter, you simply choose to leave out the optional `--value` parameter, and the service will apply the default value.</span></span> <span data-ttu-id="e2404-121">Dans l’exemple ci-dessus, elle peut se présenter comme suit :</span><span class="sxs-lookup"><span data-stu-id="e2404-121">In above example, it would look like:</span></span>
```azurecli-interactive
az postgres server configuration set --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401
```
<span data-ttu-id="e2404-122">Cette opération réinitialise la configuration **log\_min\_messages** à la valeur par défaut **WARNING**.</span><span class="sxs-lookup"><span data-stu-id="e2404-122">This will reset the **log\_min\_messages** configuration to the default value **WARNING**.</span></span> <span data-ttu-id="e2404-123">Pour plus d’informations sur la configuration du serveur et les valeurs autorisées, consultez la documentation PostgreSQL à la rubrique [Configuration du serveur](https://www.postgresql.org/docs/9.6/static/runtime-config.html).</span><span class="sxs-lookup"><span data-stu-id="e2404-123">For further details on server configuration and permissible values, see PostgreSQL documentation on [Server Configuration](https://www.postgresql.org/docs/9.6/static/runtime-config.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e2404-124">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e2404-124">Next steps</span></span>
- <span data-ttu-id="e2404-125">Pour configurer et accéder aux journaux du serveur, consultez la rubrique [Journaux de serveur dans Azure Database pour PostgreSQL](concepts-server-logs.md)</span><span class="sxs-lookup"><span data-stu-id="e2404-125">To configure and access server logs, see [Server Logs in Azure Database for PostgreSQL](concepts-server-logs.md)</span></span>
