---
title: Guide pratique pour restaurer un serveur dans Azure Database pour MySQL | Microsoft Docs
description: "Cet article décrit comment restaurer un serveur Azure Database pour MySQL à l’aide du portail."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 8c06dce534b628a602127fd02b152c8e04e02cc4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-backup-and-restore-a-server-in-azure-database-for-mysql-using-the-azure-portal"></a><span data-ttu-id="d20c7-103">Guide pratique pour sauvegarder et restaurer un serveur Azure Database pour MySQL à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="d20c7-103">How To Backup and Restore a server in Azure Database for MySQL using the Azure portal</span></span>

## <a name="backup-happens-automatically"></a><span data-ttu-id="d20c7-104">La sauvegarde s’effectue automatiquement</span><span class="sxs-lookup"><span data-stu-id="d20c7-104">Backup happens Automatically</span></span>
<span data-ttu-id="d20c7-105">Lorsque vous utilisez Azure Database pour MySQL, le service de base de données crée automatiquement une sauvegarde du service toutes les 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="d20c7-105">When using Azure Database for MySQL, the database service automatically makes a backup of the service every 5 minutes.</span></span> 

<span data-ttu-id="d20c7-106">Les sauvegardes sont disponibles pendant 7 jours avec le niveau De base et 35 jours lors de l’utilisation de niveau Standard.</span><span class="sxs-lookup"><span data-stu-id="d20c7-106">The backups are available for 7 days when using Basic Tier, and 35 days when using Standard Tier.</span></span> <span data-ttu-id="d20c7-107">Pour plus d’informations, consultez [Niveaux de service d’Azure Database pour MySQL](concepts-service-tiers.md)</span><span class="sxs-lookup"><span data-stu-id="d20c7-107">For more information, see [Azure Database for MySQL service tiers](concepts-service-tiers.md)</span></span>

<span data-ttu-id="d20c7-108">À l’aide de cette fonctionnalité de sauvegarde automatique, vous pouvez restaurer le serveur et toutes ses bases de données dans un nouveau serveur à un moment antérieur.</span><span class="sxs-lookup"><span data-stu-id="d20c7-108">Using this automatic backup feature you may restore the server and all its databases into a new server to an earlier point-in-time.</span></span>

## <a name="restore-in-the-azure-portal"></a><span data-ttu-id="d20c7-109">Restauration dans le portail Azure</span><span class="sxs-lookup"><span data-stu-id="d20c7-109">Restore in the Azure portal</span></span>
<span data-ttu-id="d20c7-110">Azure Database pour MySQL vous permet de restaurer le serveur à un moment donné et dans une nouvelle copie du serveur.</span><span class="sxs-lookup"><span data-stu-id="d20c7-110">Azure Database for MySQL allows you to restore the server back to a point in time and into to a new copy of the server.</span></span> <span data-ttu-id="d20c7-111">Vous pouvez utiliser ce nouveau serveur pour récupérer vos données.</span><span class="sxs-lookup"><span data-stu-id="d20c7-111">You can use this new server to recover your data.</span></span> 

<span data-ttu-id="d20c7-112">Par exemple, si une table a été accidentellement supprimée à midi aujourd'hui, vous pourrez restaurer à l’heure juste avant midi et retrouver la table et les données manquantes à partir de cette nouvelle copie du serveur.</span><span class="sxs-lookup"><span data-stu-id="d20c7-112">For example, if a table was accidentally dropped at noon today, you could restore to the time just before noon and retrieve the missing table and data from that new copy of the server.</span></span>

<span data-ttu-id="d20c7-113">Les étapes suivantes restaurent l’exemple de serveur à un point dans le temps :</span><span class="sxs-lookup"><span data-stu-id="d20c7-113">The following steps restore the sample server to a point in time:</span></span>

1. <span data-ttu-id="d20c7-114">Connectez-vous au [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="d20c7-114">Sign into the [Azure portal](https://portal.azure.com/)</span></span>

2. <span data-ttu-id="d20c7-115">Recherchez votre serveur Azure Database pour MySQL.</span><span class="sxs-lookup"><span data-stu-id="d20c7-115">Locate your Azure Database for MySQL server.</span></span> <span data-ttu-id="d20c7-116">Dans le volet gauche, sélectionnez **Toutes les ressources**, puis choisissez votre serveur dans la liste.</span><span class="sxs-lookup"><span data-stu-id="d20c7-116">In the left pane, select **All resources**, then select your server from the list.</span></span>

3.  <span data-ttu-id="d20c7-117">En haut du panneau de vue d’ensemble du serveur, cliquez sur **Restaurer** dans la barre d’outils.</span><span class="sxs-lookup"><span data-stu-id="d20c7-117">On the top of the server overview blade, click **Restore** on the toolbar.</span></span> <span data-ttu-id="d20c7-118">Le panneau de restauration s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="d20c7-118">The Restore blade opens.</span></span>
<span data-ttu-id="d20c7-119">![Cliquez sur le bouton Restaurer](./media/howto-restore-server-portal/click-restore-button.png)</span><span class="sxs-lookup"><span data-stu-id="d20c7-119">![click restore button](./media/howto-restore-server-portal/click-restore-button.png)</span></span>

4. <span data-ttu-id="d20c7-120">Remplissez le formulaire Restaurer avec les informations requises :</span><span class="sxs-lookup"><span data-stu-id="d20c7-120">Fill out the Restore form with the required information:</span></span>

- <span data-ttu-id="d20c7-121">**Point de restauration (UTC)** : à l’aide du sélecteur de date et d’heure, sélectionnez un point dans le temps à restaurer.</span><span class="sxs-lookup"><span data-stu-id="d20c7-121">**Restore point (UTC)**: Using the Date picker and time picker, select a point-in-time to restore to.</span></span> <span data-ttu-id="d20c7-122">L’heure étant spécifiée au format UTC, vous devrez probablement convertir l’heure locale en heure UTC.</span><span class="sxs-lookup"><span data-stu-id="d20c7-122">The time specified is in UTC format, so you likely need to convert the local time into UTC.</span></span>
- <span data-ttu-id="d20c7-123">**Restaurer sur un nouveau serveur** : indiquez le nom d’un nouveau serveur vers lequel le serveur existant sera restauré.</span><span class="sxs-lookup"><span data-stu-id="d20c7-123">**Restore to new server**: Provide a new server name to restore the existing server into.</span></span>
- <span data-ttu-id="d20c7-124">**Emplacement**: le champ de la région est automatiquement défini sur la région du serveur source et ne peut pas être modifié.</span><span class="sxs-lookup"><span data-stu-id="d20c7-124">**Location**: The region choice automatically populates with the source server region, and cannot be changed.</span></span>
- <span data-ttu-id="d20c7-125">**Niveau de tarification** : le niveau de tarification est automatiquement défini sur le même niveau de tarification que le serveur source et ne peut pas être modifié ici.</span><span class="sxs-lookup"><span data-stu-id="d20c7-125">**Pricing tier**: The pricing tier choice automatically populates with the same pricing tier as the source server, and cannot be changed here.</span></span> 
<span data-ttu-id="d20c7-126">![Restauration PITR](./media/howto-restore-server-portal/pitr-restore.png)</span><span class="sxs-lookup"><span data-stu-id="d20c7-126">![PITR Restore](./media/howto-restore-server-portal/pitr-restore.png)</span></span>

5. <span data-ttu-id="d20c7-127">Cliquez sur **OK** pour restaurer le serveur à restaurer à un moment donné.</span><span class="sxs-lookup"><span data-stu-id="d20c7-127">Click **OK** to restore the server to restore to a point in time.</span></span> 

6. <span data-ttu-id="d20c7-128">Une fois la restauration terminée, recherchez le nouveau serveur créé pour vérifier que les bases de données ont été restaurées correctement.</span><span class="sxs-lookup"><span data-stu-id="d20c7-128">After the restore finishes, locate the new server that was created to verify the databases were restored as expected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d20c7-129">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d20c7-129">Next steps</span></span>
- [<span data-ttu-id="d20c7-130">Bibliothèques de connexions de la base de données Azure pour MySQL</span><span class="sxs-lookup"><span data-stu-id="d20c7-130">Connection libraries for Azure Database for MySQL</span></span>](concepts-connection-libraries.md)