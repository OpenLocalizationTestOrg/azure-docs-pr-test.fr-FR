---
title: "aaaHow tooRestore un serveur de base de données Azure pour MySQL | Documents Microsoft"
description: "Cet article décrit comment un serveur de base de données Azure pour MySQL à l’aide de toorestore hello portail Azure."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 4b990d5b37c5d4924de9571192b923e3c81094ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toobackup-and-restore-a-server-in-azure-database-for-mysql-using-hello-azure-portal"></a><span data-ttu-id="b50e6-103">Comment tooBackup et restauration d’un serveur de base de données Azure pour l’utilisation de MySQL hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="b50e6-103">How tooBackup and Restore a server in Azure Database for MySQL using hello Azure portal</span></span>

## <a name="backup-happens-automatically"></a><span data-ttu-id="b50e6-104">La sauvegarde s’effectue automatiquement</span><span class="sxs-lookup"><span data-stu-id="b50e6-104">Backup happens Automatically</span></span>
<span data-ttu-id="b50e6-105">Lors de l’utilisation de base de données Azure pour MySQL, service de base de données hello effectue automatiquement une sauvegarde du service de hello toutes les 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="b50e6-105">When using Azure Database for MySQL, hello database service automatically makes a backup of hello service every 5 minutes.</span></span> 

<span data-ttu-id="b50e6-106">sauvegardes de Hello sont disponibles pour les 7 jours lors de l’utilisation de niveau de base et de 35 jours lors de l’utilisation de niveau Standard.</span><span class="sxs-lookup"><span data-stu-id="b50e6-106">hello backups are available for 7 days when using Basic Tier, and 35 days when using Standard Tier.</span></span> <span data-ttu-id="b50e6-107">Pour plus d’informations, consultez [Niveaux de service d’Azure Database pour MySQL](concepts-service-tiers.md)</span><span class="sxs-lookup"><span data-stu-id="b50e6-107">For more information, see [Azure Database for MySQL service tiers](concepts-service-tiers.md)</span></span>

<span data-ttu-id="b50e6-108">À l’aide de cette fonctionnalité de sauvegarde automatique vous pouvez restaurer le serveur de hello et toutes ses bases de données dans un nouveau serveur tooan précédemment point-à-temps.</span><span class="sxs-lookup"><span data-stu-id="b50e6-108">Using this automatic backup feature you may restore hello server and all its databases into a new server tooan earlier point-in-time.</span></span>

## <a name="restore-in-hello-azure-portal"></a><span data-ttu-id="b50e6-109">Restaurer Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="b50e6-109">Restore in hello Azure portal</span></span>
<span data-ttu-id="b50e6-110">Base de données Azure pour MySQL vous permet de toorestore hello server tooa précédent point dans le temps et en tooa une nouvelle copie du serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="b50e6-110">Azure Database for MySQL allows you toorestore hello server back tooa point in time and into tooa new copy of hello server.</span></span> <span data-ttu-id="b50e6-111">Vous pouvez utiliser cette nouvelle toorecover de serveur à vos données.</span><span class="sxs-lookup"><span data-stu-id="b50e6-111">You can use this new server toorecover your data.</span></span> 

<span data-ttu-id="b50e6-112">Par exemple, si une table a été accidentellement supprimé à midi aujourd'hui, vous pourriez restaurer temps toohello juste avant midi et les récupérer hello manquant de table et les données à partir de la copie du serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="b50e6-112">For example, if a table was accidentally dropped at noon today, you could restore toohello time just before noon and retrieve hello missing table and data from that new copy of hello server.</span></span>

<span data-ttu-id="b50e6-113">Hello suit restaurer hello exemple server tooa point dans le temps :</span><span class="sxs-lookup"><span data-stu-id="b50e6-113">hello following steps restore hello sample server tooa point in time:</span></span>

1. <span data-ttu-id="b50e6-114">L’authentification à hello [portail Azure](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="b50e6-114">Sign into hello [Azure portal](https://portal.azure.com/)</span></span>

2. <span data-ttu-id="b50e6-115">Recherchez votre serveur Azure Database pour MySQL.</span><span class="sxs-lookup"><span data-stu-id="b50e6-115">Locate your Azure Database for MySQL server.</span></span> <span data-ttu-id="b50e6-116">Dans le volet gauche de hello, sélectionnez **toutes les ressources**, puis sélectionnez votre serveur à partir de la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="b50e6-116">In hello left pane, select **All resources**, then select your server from hello list.</span></span>

3.  <span data-ttu-id="b50e6-117">Dans le haut de hello du Panneau de vue d’ensemble du serveur hello, cliquez sur **restaurer** sur la barre d’outils hello.</span><span class="sxs-lookup"><span data-stu-id="b50e6-117">On hello top of hello server overview blade, click **Restore** on hello toolbar.</span></span> <span data-ttu-id="b50e6-118">Panneau de restauration Hello s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="b50e6-118">hello Restore blade opens.</span></span>
<span data-ttu-id="b50e6-119">![Cliquez sur le bouton Restaurer](./media/howto-restore-server-portal/click-restore-button.png)</span><span class="sxs-lookup"><span data-stu-id="b50e6-119">![click restore button](./media/howto-restore-server-portal/click-restore-button.png)</span></span>

4. <span data-ttu-id="b50e6-120">Remplissez le formulaire de restauration de hello avec les informations de hello requis :</span><span class="sxs-lookup"><span data-stu-id="b50e6-120">Fill out hello Restore form with hello required information:</span></span>

- <span data-ttu-id="b50e6-121">**(UTC) de point de restauration**: à l’aide du sélecteur de dates hello time picker, sélectionnez un toorestore point-à-temps pour.</span><span class="sxs-lookup"><span data-stu-id="b50e6-121">**Restore point (UTC)**: Using hello Date picker and time picker, select a point-in-time toorestore to.</span></span> <span data-ttu-id="b50e6-122">heure de Hello spécifiée est au format UTC, donc vous devez probablement tooconvert hello local heure en UTC.</span><span class="sxs-lookup"><span data-stu-id="b50e6-122">hello time specified is in UTC format, so you likely need tooconvert hello local time into UTC.</span></span>
- <span data-ttu-id="b50e6-123">**Restaurer le serveur de toonew**: fournir un nouveau serveur serveur existant de nom toorestore hello dans.</span><span class="sxs-lookup"><span data-stu-id="b50e6-123">**Restore toonew server**: Provide a new server name toorestore hello existing server into.</span></span>
- <span data-ttu-id="b50e6-124">**Emplacement**: choix de la région de hello remplit avec la région du serveur source hello automatiquement et ne peut pas être modifié.</span><span class="sxs-lookup"><span data-stu-id="b50e6-124">**Location**: hello region choice automatically populates with hello source server region, and cannot be changed.</span></span>
- <span data-ttu-id="b50e6-125">**Niveau de tarification**: hello choix du niveau de tarification automatiquement remplit avec hello tarification même niveau en tant que serveur de source de hello et ne peut pas être modifiées ici.</span><span class="sxs-lookup"><span data-stu-id="b50e6-125">**Pricing tier**: hello pricing tier choice automatically populates with hello same pricing tier as hello source server, and cannot be changed here.</span></span> 
<span data-ttu-id="b50e6-126">![Restauration PITR](./media/howto-restore-server-portal/pitr-restore.png)</span><span class="sxs-lookup"><span data-stu-id="b50e6-126">![PITR Restore](./media/howto-restore-server-portal/pitr-restore.png)</span></span>

5. <span data-ttu-id="b50e6-127">Cliquez sur **OK** toorestore hello server toorestore tooa point dans le temps.</span><span class="sxs-lookup"><span data-stu-id="b50e6-127">Click **OK** toorestore hello server toorestore tooa point in time.</span></span> 

6. <span data-ttu-id="b50e6-128">Après la restauration de hello, recherchez hello nouveau serveur qui a été créé hello tooverify bases de données ont été restaurés comme prévu.</span><span class="sxs-lookup"><span data-stu-id="b50e6-128">After hello restore finishes, locate hello new server that was created tooverify hello databases were restored as expected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b50e6-129">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b50e6-129">Next steps</span></span>
- [<span data-ttu-id="b50e6-130">Bibliothèques de connexions de la base de données Azure pour MySQL</span><span class="sxs-lookup"><span data-stu-id="b50e6-130">Connection libraries for Azure Database for MySQL</span></span>](concepts-connection-libraries.md)