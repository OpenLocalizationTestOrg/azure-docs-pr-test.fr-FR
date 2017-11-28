---
title: "journaux du serveur aaaConfigure et accès pour PostgreSQL à l’aide d’Azure CLI | Documents Microsoft"
description: "Cet article décrit la façon dont les journaux du serveur de hello tooconfigure et d’accès dans la base de données Azure pour PostgreSQL à l’aide de la ligne de commande CLI d’Azure."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 924d4e7634cc48405bcb0f813cf61d8b72ad8aa0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-access-server-logs-using-azure-cli"></a><span data-ttu-id="35427-103">Configuration et accès aux journaux du serveur à l’aide de la ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="35427-103">Configure and access server logs using Azure CLI</span></span>
<span data-ttu-id="35427-104">Vous pouvez télécharger les journaux d’erreurs hello PostgreSQL server à l’aide de hello Interface de ligne de commande (CLI d’Azure).</span><span class="sxs-lookup"><span data-stu-id="35427-104">You can download hello PostgreSQL server error logs using hello Command Line Interface (Azure CLI).</span></span> <span data-ttu-id="35427-105">Toutefois, les journaux d’accès tootransaction n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="35427-105">However, access tootransaction logs is not supported.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="35427-106">Composants requis</span><span class="sxs-lookup"><span data-stu-id="35427-106">Prerequisites</span></span>
<span data-ttu-id="35427-107">toostep via ce tooguide de procédure, vous devez :</span><span class="sxs-lookup"><span data-stu-id="35427-107">toostep through this how-tooguide, you need:</span></span>
- <span data-ttu-id="35427-108">Un [serveur Azure Database pour PostgreSQL](quickstart-create-server-database-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="35427-108">An [Azure Database for PostgreSQL server](quickstart-create-server-database-azure-cli.md)</span></span>
- <span data-ttu-id="35427-109">Installer [Azure CLI 2.0](/cli/azure/install-azure-cli) de ligne de commande utilitaires ou utilisez hello Azure Cloud Shell dans le navigateur de hello.</span><span class="sxs-lookup"><span data-stu-id="35427-109">Install [Azure CLI 2.0](/cli/azure/install-azure-cli) command-line utility or use hello Azure Cloud Shell in hello browser.</span></span>

## <a name="configure-logging-for-azure-database-for-postgresql"></a><span data-ttu-id="35427-110">Configuration de la journalisation pour Azure Database pour PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="35427-110">Configure logging for Azure Database for PostgreSQL</span></span>
<span data-ttu-id="35427-111">Vous pouvez configurer les journaux de requête tooaccess hello server et les journaux d’erreurs.</span><span class="sxs-lookup"><span data-stu-id="35427-111">You can configure hello server tooaccess query logs and error logs.</span></span> <span data-ttu-id="35427-112">Les journaux d’erreurs peuvent contenir des informations sur le nettoyage automatique, la connexion et les points de contrôle.</span><span class="sxs-lookup"><span data-stu-id="35427-112">Error logs can contain auto-vacuum, connection, and checkpoints information.</span></span>
1. <span data-ttu-id="35427-113">Activation de la journalisation</span><span class="sxs-lookup"><span data-stu-id="35427-113">Turn on logging</span></span>
2. <span data-ttu-id="35427-114">Journal de mise à jour\_instruction et journal\_min\_durée\_journalisation des requêtes tooenable instruction</span><span class="sxs-lookup"><span data-stu-id="35427-114">Update log\_statement and log\_min\_duration\_statement tooenable query logging</span></span>
3. <span data-ttu-id="35427-115">Mise à jour de la période de rétention</span><span class="sxs-lookup"><span data-stu-id="35427-115">Update retention period</span></span>

<span data-ttu-id="35427-116">Pour plus d’informations, consultez [Personnalisation des paramètres de configuration du serveur](howto-configure-server-parameters-using-cli.md).</span><span class="sxs-lookup"><span data-stu-id="35427-116">For more information, see [customizing server configuration parameters](howto-configure-server-parameters-using-cli.md).</span></span>

## <a name="list-logs-for-azure-database-for-postgresql-server"></a><span data-ttu-id="35427-117">Répertorier les journaux pour le serveur Azure Database pour PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="35427-117">List logs for Azure Database for PostgreSQL server</span></span>
<span data-ttu-id="35427-118">fichiers de journaux disponibles toolist hello pour votre serveur, exécutez hello [liste de journaux du serveur az postgres](/cli/azure/postgres/server-logs#list) commande.</span><span class="sxs-lookup"><span data-stu-id="35427-118">toolist hello available log files for your server, run hello [az postgres server-logs list](/cli/azure/postgres/server-logs#list) command.</span></span>

<span data-ttu-id="35427-119">Vous pouvez répertorier les fichiers de journaux hello pour le serveur **mypgserver-20170401.postgres.database.azure.com** sous le groupe de ressources **myresourcegroup**et lui demander tooa texte fichier appelé **journal\_fichiers\_liste.txt.**</span><span class="sxs-lookup"><span data-stu-id="35427-119">You can list hello log files for server **mypgserver-20170401.postgres.database.azure.com** under Resource Group **myresourcegroup**, and direct it tooa text file called **log\_files\_list.txt.**</span></span>
```azurecli-interactive
az postgres server-logs list --resource-group myresourcegroup --server mypgserver-20170401 > log_files_list.txt
```
## <a name="download-logs-locally-from-hello-server"></a><span data-ttu-id="35427-120">Télécharger les journaux localement à partir du serveur de hello</span><span class="sxs-lookup"><span data-stu-id="35427-120">Download logs locally from hello server</span></span>
<span data-ttu-id="35427-121">Hello [téléchargement des journaux de serveur az postgres](/cli/azure/postgres/server-logs#download) commande vous permet de différents fichiers journaux individuels toodownload pour votre serveur.</span><span class="sxs-lookup"><span data-stu-id="35427-121">hello [az postgres server-logs download](/cli/azure/postgres/server-logs#download) command allows you toodownload individual log files for your server.</span></span> 

<span data-ttu-id="35427-122">Cet exemple télécharge hello fichier journal spécifique pour le serveur de hello **mypgserver-20170401.postgres.database.azure.com** sous le groupe de ressources **myresourcegroup** tooyour des environnement local.</span><span class="sxs-lookup"><span data-stu-id="35427-122">This example downloads hello specific log file for hello server **mypgserver-20170401.postgres.database.azure.com** under Resource Group **myresourcegroup** tooyour local environment.</span></span>
```azurecli-interactive
az postgres server-logs download --name 20170414-mypgserver-20170401-postgresql.log --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="next-steps"></a><span data-ttu-id="35427-123">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="35427-123">Next steps</span></span>
- <span data-ttu-id="35427-124">toolearn en savoir plus sur les journaux du serveur, consultez [journaux du serveur de base de données PostgreSQL Azure](concepts-server-logs.md)</span><span class="sxs-lookup"><span data-stu-id="35427-124">toolearn more about server logs, see [Server Logs in Azure Database for PostgreSQL](concepts-server-logs.md)</span></span>
- <span data-ttu-id="35427-125">Pour plus d’informations sur les paramètres du serveur, consultez la rubrique [Personnalisation des paramètres de configuration de serveur à l’aide de l’interface de ligne de commande Azure](howto-configure-server-parameters-using-cli.md)</span><span class="sxs-lookup"><span data-stu-id="35427-125">For more information on server parameters, see [Customize server configuration parameters using Azure CLI](howto-configure-server-parameters-using-cli.md)</span></span>
