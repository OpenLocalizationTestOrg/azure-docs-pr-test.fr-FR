---
title: "paramètres de service aaaConfigure hello dans la base de données Azure pour PostgreSQL | Documents Microsoft"
description: "Cet article décrit comment les paramètres de service hello tooconfigure dans la base de données Azure pour l’utilisation de PostgreSQL hello ligne de commande CLI d’Azure."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 84a11de24ba87fc0eb6744aaa4b53f65a183903d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-server-configuration-parameters-using-azure-cli"></a><span data-ttu-id="ee180-103">Personnalisation des paramètres de configuration du serveur à l’aide de l’interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="ee180-103">Customize server configuration parameters using Azure CLI</span></span>
<span data-ttu-id="ee180-104">Vous pouvez répertorier, afficher et mettre à jour les paramètres de configuration pour un serveur Azure PostgreSQL à l’aide de hello Interface de ligne de commande (CLI d’Azure).</span><span class="sxs-lookup"><span data-stu-id="ee180-104">You can list, show and update configuration parameters for an Azure PostgreSQL server using hello Command Line Interface (Azure CLI).</span></span> <span data-ttu-id="ee180-105">Toutefois, un seul sous-ensemble de configurations de moteur est exposé au niveau du serveur et peut être modifié.</span><span class="sxs-lookup"><span data-stu-id="ee180-105">However, only a subset of engine configurations are exposed at server-level and can be modified.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="ee180-106">Composants requis</span><span class="sxs-lookup"><span data-stu-id="ee180-106">Prerequisites</span></span>
<span data-ttu-id="ee180-107">toostep via ce tooguide de procédure, vous devez :</span><span class="sxs-lookup"><span data-stu-id="ee180-107">toostep through this how-tooguide, you need:</span></span>
- <span data-ttu-id="ee180-108">Un serveur et une base de données [Création d’une base de données Azure POUR PostgreSQL](quickstart-create-server-database-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="ee180-108">A server and database [Create an Azure Database for PostgreSQL](quickstart-create-server-database-azure-cli.md)</span></span>
- <span data-ttu-id="ee180-109">Installer [Azure CLI 2.0](/cli/azure/install-azure-cli) ligne de commande utilitaires ou utilisez hello Azure Cloud Shell dans le navigateur de hello.</span><span class="sxs-lookup"><span data-stu-id="ee180-109">Install [Azure CLI 2.0](/cli/azure/install-azure-cli) command line utility or use hello Azure Cloud Shell in hello browser.</span></span>

## <a name="list-server-configuration-parameters-for-azure-database-for-postgresql-server"></a><span data-ttu-id="ee180-110">Répertorier les paramètres de configuration de Base de données Azure pour le serveur PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="ee180-110">List server configuration parameters for Azure Database for PostgreSQL server</span></span>
<span data-ttu-id="ee180-111">l’exécution de tous les paramètres modifiables dans un serveur et leurs valeurs, toolist hello [liste de configuration du serveur az postgres](/cli/azure/postgres/server/configuration#list) commande.</span><span class="sxs-lookup"><span data-stu-id="ee180-111">toolist all modifiable parameters in a server and their values, run hello [az postgres server configuration list](/cli/azure/postgres/server/configuration#list) command.</span></span>

<span data-ttu-id="ee180-112">Vous pouvez répertorier les paramètres de configuration de serveur hello pour le serveur de hello **mypgserver-20170401.postgres.database.azure.com** sous le groupe de ressources **myresourcegroup**.</span><span class="sxs-lookup"><span data-stu-id="ee180-112">You can list hello server configuration parameters for hello server **mypgserver-20170401.postgres.database.azure.com** under resource group **myresourcegroup**.</span></span>
```azurecli-interactive
az postgres server configuration list --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="show-server-configuration-parameter-details"></a><span data-ttu-id="ee180-113">Affichage des détails des paramètres de configuration du serveur</span><span class="sxs-lookup"><span data-stu-id="ee180-113">Show server configuration parameter details</span></span>
<span data-ttu-id="ee180-114">tooshow plus d’informations sur un paramètre de configuration particulière pour un serveur, exécutez hello [afficher de configuration serveur az postgres](/cli/azure/postgres/server/configuration#show) commande.</span><span class="sxs-lookup"><span data-stu-id="ee180-114">tooshow details about a particular configuration parameter for a server, run hello [az postgres server configuration show](/cli/azure/postgres/server/configuration#show)  command.</span></span>

<span data-ttu-id="ee180-115">Cet exemple affiche les détails de hello **journal\_min\_messages** paramètre de configuration du serveur pour le serveur **mypgserver-20170401.postgres.database.azure.com** sous groupe de ressources **myresourcegroup.**</span><span class="sxs-lookup"><span data-stu-id="ee180-115">This example shows details of hello **log\_min\_messages** server configuration parameter for server **mypgserver-20170401.postgres.database.azure.com** under resource group **myresourcegroup.**</span></span>
```azurecli-interactive
az postgres server configuration show --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="modify-server-configuration-parameter-value"></a><span data-ttu-id="ee180-116">Modification de la valeur de paramètre de configuration du serveur</span><span class="sxs-lookup"><span data-stu-id="ee180-116">Modify server configuration parameter value</span></span>
<span data-ttu-id="ee180-117">Vous pouvez également modifier la valeur hello un certain paramètre de configuration du serveur, et cela met à jour la valeur de configuration sous-jacente hello pour le moteur de serveur hello PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="ee180-117">You can also modify hello value of a certain server configuration parameter, and this updates hello underlying configuration value for hello PostgreSQL server engine.</span></span> <span data-ttu-id="ee180-118">hello d’utilisation tooupdate hello configuration [jeu de configuration de serveur az postgres](/cli/azure/postgres/server/configuration#set) commande.</span><span class="sxs-lookup"><span data-stu-id="ee180-118">tooupdate hello configuration use hello [az postgres server configuration set](/cli/azure/postgres/server/configuration#set) command.</span></span> 

<span data-ttu-id="ee180-119">tooupdate hello **journal\_min\_messages** paramètre de configuration du serveur du serveur **mypgserver-20170401.postgres.database.azure.com** sous le groupe de ressources **myresourcegroup.**</span><span class="sxs-lookup"><span data-stu-id="ee180-119">tooupdate hello **log\_min\_messages** server configuration parameter of server **mypgserver-20170401.postgres.database.azure.com** under resource group **myresourcegroup.**</span></span>
```azurecli-interactive
az postgres server configuration set --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401 --value INFO
```
<span data-ttu-id="ee180-120">Si vous voulez la valeur de hello tooreset d’un paramètre de configuration, vous choisissez simplement tooleave out hello facultatif `--value` paramètre et le service hello seront applique par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="ee180-120">If you want tooreset hello value of a configuration parameter, you simply choose tooleave out hello optional `--value` parameter, and hello service will apply hello default value.</span></span> <span data-ttu-id="ee180-121">Dans l’exemple ci-dessus, elle peut se présenter comme suit :</span><span class="sxs-lookup"><span data-stu-id="ee180-121">In above example, it would look like:</span></span>
```azurecli-interactive
az postgres server configuration set --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401
```
<span data-ttu-id="ee180-122">Cette action réinitialisera hello **journal\_min\_messages** valeur par défaut de configuration toohello **avertissement**.</span><span class="sxs-lookup"><span data-stu-id="ee180-122">This will reset hello **log\_min\_messages** configuration toohello default value **WARNING**.</span></span> <span data-ttu-id="ee180-123">Pour plus d’informations sur la configuration du serveur et les valeurs autorisées, consultez la documentation PostgreSQL à la rubrique [Configuration du serveur](https://www.postgresql.org/docs/9.6/static/runtime-config.html).</span><span class="sxs-lookup"><span data-stu-id="ee180-123">For further details on server configuration and permissible values, see PostgreSQL documentation on [Server Configuration](https://www.postgresql.org/docs/9.6/static/runtime-config.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ee180-124">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ee180-124">Next steps</span></span>
- <span data-ttu-id="ee180-125">journaux du serveur tooconfigure et l’accès, consultez [journaux du serveur de base de données PostgreSQL Azure](concepts-server-logs.md)</span><span class="sxs-lookup"><span data-stu-id="ee180-125">tooconfigure and access server logs, see [Server Logs in Azure Database for PostgreSQL](concepts-server-logs.md)</span></span>
