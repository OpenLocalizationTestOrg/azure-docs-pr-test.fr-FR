---
title: "Comment tooRestore un serveur de base de données PostgreSQL Azure | Documents Microsoft"
description: "Cet article décrit comment toorestore un serveur de base de données Azure pour l’utilisation de PostgreSQL hello portail Azure."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 07/20/2017
ms.openlocfilehash: bc7351f384607397806d837afd3e1d7a26575e0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toobackup-and-restore-a-server-in-azure-database-for-postgresql-using-hello-azure-portal"></a><span data-ttu-id="2917c-103">Comment tooBackup et restauration d’un serveur de base de données Azure pour l’utilisation de PostgreSQL hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="2917c-103">How tooBackup and Restore a server in Azure Database for PostgreSQL using hello Azure portal</span></span>

## <a name="backup-happens-automatically"></a><span data-ttu-id="2917c-104">La sauvegarde s’effectue automatiquement</span><span class="sxs-lookup"><span data-stu-id="2917c-104">Backup happens Automatically</span></span>
<span data-ttu-id="2917c-105">Lors de l’utilisation de base de données Azure pour PostgreSQL, service de base de données hello effectue automatiquement une sauvegarde du service de hello toutes les 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="2917c-105">When using Azure Database for PostgreSQL, hello database service automatically makes a backup of hello service every 5 minutes.</span></span> 

<span data-ttu-id="2917c-106">sauvegardes de Hello sont disponibles pour les 7 jours lors de l’utilisation de niveau de base et de 35 jours lors de l’utilisation de niveau Standard.</span><span class="sxs-lookup"><span data-stu-id="2917c-106">hello backups are available for 7 days when using Basic Tier, and 35 days when using Standard Tier.</span></span> <span data-ttu-id="2917c-107">Pour plus d’informations, consultez [Niveaux de service d’Azure Database pour PostgreSQL](concepts-service-tiers.md)</span><span class="sxs-lookup"><span data-stu-id="2917c-107">For more information, see [Azure Database for PostgreSQL service tiers](concepts-service-tiers.md)</span></span>

<span data-ttu-id="2917c-108">À l’aide de cette fonctionnalité de sauvegarde automatique vous pouvez restaurer le serveur de hello et toutes ses bases de données dans un nouveau serveur tooan précédemment point-à-temps.</span><span class="sxs-lookup"><span data-stu-id="2917c-108">Using this automatic backup feature you may restore hello server and all its databases into a new server tooan earlier point-in-time.</span></span>

## <a name="restore-in-hello-azure-portal"></a><span data-ttu-id="2917c-109">Restaurer Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="2917c-109">Restore in hello Azure portal</span></span>
<span data-ttu-id="2917c-110">Base de données Azure pour PostgreSQL vous permet de toorestore hello server tooa précédent point dans le temps et en tooa une nouvelle copie du serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="2917c-110">Azure Database for PostgreSQL allows you toorestore hello server back tooa point in time and into tooa new copy of hello server.</span></span> <span data-ttu-id="2917c-111">Vous pouvez utiliser cette nouvelle toorecover de serveur à vos données.</span><span class="sxs-lookup"><span data-stu-id="2917c-111">You can use this new server toorecover your data.</span></span> 

<span data-ttu-id="2917c-112">Par exemple, si une table a été accidentellement supprimé à midi aujourd'hui, vous pourriez restaurer temps toohello juste avant midi et les récupérer hello manquant de table et les données à partir de la copie du serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="2917c-112">For example, if a table was accidentally dropped at noon today, you could restore toohello time just before noon and retrieve hello missing table and data from that new copy of hello server.</span></span>

<span data-ttu-id="2917c-113">Hello suit restaurer hello exemple server tooa point dans le temps :</span><span class="sxs-lookup"><span data-stu-id="2917c-113">hello following steps restore hello sample server tooa point in time:</span></span>
1. <span data-ttu-id="2917c-114">L’authentification à hello [portail Azure](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="2917c-114">Sign into hello [Azure portal](https://portal.azure.com/)</span></span>
2. <span data-ttu-id="2917c-115">Recherchez votre serveur Azure Database pour PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="2917c-115">Locate your Azure Database for PostgreSQL server.</span></span> <span data-ttu-id="2917c-116">Bonjour portail Azure, cliquez sur **toutes les ressources** de menu à gauche hello et tapez Bonjour nom, tel que **mypgserver-20170401**, toosearch de votre serveur existant.</span><span class="sxs-lookup"><span data-stu-id="2917c-116">In hello Azure portal, click **All Resources** from hello left-hand menu and type in hello name, such as **mypgserver-20170401**, toosearch for your existing server.</span></span> <span data-ttu-id="2917c-117">Cliquez sur le nom du serveur hello répertorié dans les résultats de recherche hello.</span><span class="sxs-lookup"><span data-stu-id="2917c-117">Click hello server name listed in hello search result.</span></span> <span data-ttu-id="2917c-118">Hello **vue d’ensemble** pour votre serveur s’ouvre et fournit des options pour poursuivre la configuration de la page.</span><span class="sxs-lookup"><span data-stu-id="2917c-118">hello **Overview** page for your server opens and provides options for further configuration.</span></span>

   ![Portail Azure - rechercher toolocate votre serveur](media/postgresql-howto-restore-server-portal/1-locate.png)

3. <span data-ttu-id="2917c-120">Dans le haut de hello du Panneau de vue d’ensemble du serveur hello, cliquez sur **restaurer** sur la barre d’outils hello.</span><span class="sxs-lookup"><span data-stu-id="2917c-120">On hello top of hello server overview blade, click **Restore** on hello toolbar.</span></span> <span data-ttu-id="2917c-121">Panneau de restauration Hello s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="2917c-121">hello Restore blade opens.</span></span>

   ![Azure Database pour PostgreSQL - Vue d’ensemble - Bouton Restaurer](./media/postgresql-howto-restore-server-portal/2_server.png)

4. <span data-ttu-id="2917c-123">Remplissez le formulaire de restauration de hello avec les informations de hello requis :</span><span class="sxs-lookup"><span data-stu-id="2917c-123">Fill out hello Restore form with hello required information:</span></span>

   ![<span data-ttu-id="2917c-124">Azure Database pour PostgreSQL - Informations de restauration</span><span class="sxs-lookup"><span data-stu-id="2917c-124">Azure Database for PostgreSQL - Restore information</span></span> ](./media/postgresql-howto-restore-server-portal/3_restore.png)
  - <span data-ttu-id="2917c-125">**Point de restauration**: sélectionnez un point dans le temps qui se produit avant que le serveur de hello a été modifié</span><span class="sxs-lookup"><span data-stu-id="2917c-125">**Restore point**: Select a point-in-time that occurs before hello server was changed</span></span>
  - <span data-ttu-id="2917c-126">**Serveur cible**: fournir un nouveau nom du serveur toorestore à</span><span class="sxs-lookup"><span data-stu-id="2917c-126">**Target server**: Provide a new server name you want toorestore to</span></span>
  - <span data-ttu-id="2917c-127">**Emplacement**: vous ne pouvez pas sélectionner la région de hello, par défaut, il est identique au serveur de source de hello</span><span class="sxs-lookup"><span data-stu-id="2917c-127">**Location**: You cannot select hello region, by default it is same as hello source server</span></span>
  - <span data-ttu-id="2917c-128">**Niveau tarifaire** : vous ne pouvez pas modifier cette valeur lors de la restauration d’un serveur.</span><span class="sxs-lookup"><span data-stu-id="2917c-128">**Pricing tier**: You cannot change this value when restoring a server.</span></span> <span data-ttu-id="2917c-129">Il est identique au serveur de source de hello.</span><span class="sxs-lookup"><span data-stu-id="2917c-129">It is same as hello source server.</span></span> 

5. <span data-ttu-id="2917c-130">Cliquez sur **OK** toorestore hello server toorestore tooa point dans le temps.</span><span class="sxs-lookup"><span data-stu-id="2917c-130">Click **OK** toorestore hello server toorestore tooa point in time.</span></span> 

6. <span data-ttu-id="2917c-131">Une fois hello restauration terminée, recherchez hello nouveau serveur qui est créé hello tooverify données ont été restaurées comme prévu.</span><span class="sxs-lookup"><span data-stu-id="2917c-131">Once hello restore finishes, locate hello new server that is created tooverify hello data was restored as expected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2917c-132">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2917c-132">Next steps</span></span>
- [<span data-ttu-id="2917c-133">Bibliothèques de connexions pour Azure Database pour PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="2917c-133">Connection libraries for Azure Database for PostgreSQL</span></span>](concepts-connection-libraries.md)
