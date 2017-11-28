---
title: "aaaCreate et gérer la base de données Azure pour MySQL server à l’aide du portail Azure | Documents Microsoft"
description: "Cet article décrit comment vous pouvez rapidement créer une nouvelle base de données Azure pour le serveur MySQL et gérer le serveur hello à l’aide de hello portail Azure."
services: mysql
author: v-chenyh
ms.author: nolanwu
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: c532df43b3d2124d7bd34875b32d52357f162af8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-mysql-server-using-azure-portal"></a><span data-ttu-id="673bc-103">Création et gestion d’un serveur Azure Database pour MySQL à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="673bc-103">Create and manage Azure Database for MySQL server using Azure portal</span></span>
<span data-ttu-id="673bc-104">Cet article décrit comment vous pouvez rapidement créer une nouvelle base de données Azure pour le serveur MySQL et gérer le serveur hello à l’aide de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="673bc-104">This article describes how you can quickly create a new Azure Database for MySQL server and manage hello server using hello Azure Portal.</span></span> <span data-ttu-id="673bc-105">Gestion des serveurs inclut l’affichage des détails du serveur et les bases de données, de la réinitialisation de mot de passe et de suppression du serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="673bc-105">Server management includes viewing server details & databases, resetting password and deleting hello server.</span></span>

## <a name="log-in-toohello-azure-portal"></a><span data-ttu-id="673bc-106">Ouvrez une session dans toohello portail Azure</span><span class="sxs-lookup"><span data-stu-id="673bc-106">Log in toohello Azure portal</span></span>
<span data-ttu-id="673bc-107">Connectez-vous à toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="673bc-107">Log in toohello [Azure portal](https://portal.azure.com).</span></span>

## <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="673bc-108">Créer un serveur de base de données Azure pour MySQL</span><span class="sxs-lookup"><span data-stu-id="673bc-108">Create an Azure Database for MySQL server</span></span>
<span data-ttu-id="673bc-109">Suivez ces étapes de toocreate serveur MySQL nommé « mysqlserver4demo » dans une base de données Azure</span><span class="sxs-lookup"><span data-stu-id="673bc-109">Follow these steps toocreate an Azure Database for MySQL server named “mysqlserver4demo”</span></span>

<span data-ttu-id="673bc-110">1-click **nouveau** bouton se trouve sur le coin supérieur gauche hello Hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="673bc-110">1- Click **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>

<span data-ttu-id="673bc-111">2-Sélectionnez **bases de données** à partir de la nouvelle page de hello, puis sélectionnez **base de données Azure pour MySQL** à partir de la page de bases de données hello.</span><span class="sxs-lookup"><span data-stu-id="673bc-111">2- Select **Databases** from hello New page, and select **Azure Database for MySQL** from hello Databases page.</span></span>

> <span data-ttu-id="673bc-112">Un serveur Azure Database pour MySQL est créé avec un ensemble défini de [ressources de calcul et de stockage](./concepts-compute-unit-and-storage.md).</span><span class="sxs-lookup"><span data-stu-id="673bc-112">An Azure Database for MySQL server is created with a defined set of [compute and storage](./concepts-compute-unit-and-storage.md) resources.</span></span> <span data-ttu-id="673bc-113">base de données Hello est créé dans un groupe de ressources Azure et dans une base de données Azure pour le serveur MySQL.</span><span class="sxs-lookup"><span data-stu-id="673bc-113">hello database is created within an Azure resource group and in an Azure Database for MySQL server.</span></span>

![create-new-server](./media/howto-create-manage-server-portal/create-new-server.png)

<span data-ttu-id="673bc-115">3 - remplir hello Azure de base de données MySQL formulaire avec hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="673bc-115">3- Fill out hello Azure Database for MySQL form with hello following information:</span></span>

| <span data-ttu-id="673bc-116">**Champ de formulaire**</span><span class="sxs-lookup"><span data-stu-id="673bc-116">**Form Field**</span></span> | <span data-ttu-id="673bc-117">**Description du champ**</span><span class="sxs-lookup"><span data-stu-id="673bc-117">**Field Description**</span></span> |
|----------------|-----------------------|
| <span data-ttu-id="673bc-118">*Nom du serveur*</span><span class="sxs-lookup"><span data-stu-id="673bc-118">*Server name*</span></span> | <span data-ttu-id="673bc-119">azure-mysql (le nom du serveur est globalement unique)</span><span class="sxs-lookup"><span data-stu-id="673bc-119">azure-mysql (server name is globally unique)</span></span> |
| <span data-ttu-id="673bc-120">*Abonnement*</span><span class="sxs-lookup"><span data-stu-id="673bc-120">*Subscription*</span></span> | <span data-ttu-id="673bc-121">MySQLaaS (sélectionnez une option dans le menu déroulant)</span><span class="sxs-lookup"><span data-stu-id="673bc-121">MySQLaaS (select from drop down)</span></span> |
| <span data-ttu-id="673bc-122">*Groupe de ressources*</span><span class="sxs-lookup"><span data-stu-id="673bc-122">*Resource group*</span></span> | <span data-ttu-id="673bc-123">myresource (créez un nouveau groupe de ressources ou utilisez un groupe existant)</span><span class="sxs-lookup"><span data-stu-id="673bc-123">myresource (create a new resource group or use an existing one)</span></span> |
| <span data-ttu-id="673bc-124">*Connexion d’administrateur serveur*</span><span class="sxs-lookup"><span data-stu-id="673bc-124">*Server admin login*</span></span> | <span data-ttu-id="673bc-125">myadmin (nom du compte administrateur de l’installation)</span><span class="sxs-lookup"><span data-stu-id="673bc-125">myadmin (setup admin account name)</span></span> |
| <span data-ttu-id="673bc-126">*Mot de passe*</span><span class="sxs-lookup"><span data-stu-id="673bc-126">*Password*</span></span> | <span data-ttu-id="673bc-127">mot de passe du compte administrateur de l’installation</span><span class="sxs-lookup"><span data-stu-id="673bc-127">setup admin account password</span></span> |
| <span data-ttu-id="673bc-128">*Confirmer le mot de passe*</span><span class="sxs-lookup"><span data-stu-id="673bc-128">*Confirm password*</span></span> | <span data-ttu-id="673bc-129">confirmez le mot de passe du compte administrateur</span><span class="sxs-lookup"><span data-stu-id="673bc-129">confirm admin account password</span></span> |
| <span data-ttu-id="673bc-130">*Emplacement*</span><span class="sxs-lookup"><span data-stu-id="673bc-130">*Location*</span></span> | <span data-ttu-id="673bc-131">Europe du Nord (sélection Europe du Nord ou États-Unis de l'Ouest)</span><span class="sxs-lookup"><span data-stu-id="673bc-131">North Europe (select between North Europe and West US)</span></span> |
| <span data-ttu-id="673bc-132">*Version*</span><span class="sxs-lookup"><span data-stu-id="673bc-132">*Version*</span></span> | <span data-ttu-id="673bc-133">5.6 (choisissez la version du serveur Azure Database pour MySQL)</span><span class="sxs-lookup"><span data-stu-id="673bc-133">5.6 (choose Azure Database for MySQL server version)</span></span> |

<span data-ttu-id="673bc-134">4-Cliquez **niveau tarifaire** toospecify hello performances et la couche de niveau de service pour votre nouveau serveur.</span><span class="sxs-lookup"><span data-stu-id="673bc-134">4- Click **Pricing tier** toospecify hello service tier and performance level for your new server.</span></span> <span data-ttu-id="673bc-135">L’unité de calcul peut être configurée entre 50 et 100 dans le niveau de base, entre 100 et 200 dans le niveau standard, et vous pouvez augmenter le stockage en fonction du montant inclus.</span><span class="sxs-lookup"><span data-stu-id="673bc-135">Compute Unit can be configured between 50 and 100 in Basic tier, 100 and 200 in Standard tier, and storage can be added based on included amount.</span></span> <span data-ttu-id="673bc-136">Pour ce guide pratique, choisissons 50 unités de calcul et 50 Go.</span><span class="sxs-lookup"><span data-stu-id="673bc-136">For this HowTo guide, let’s choose 50 Compute Unit and 50GB.</span></span> <span data-ttu-id="673bc-137">Cliquez sur **OK** toosave votre sélection.</span><span class="sxs-lookup"><span data-stu-id="673bc-137">Click **OK** toosave your selection.</span></span>
<span data-ttu-id="673bc-138">![create-server-pricing-tier](./media/howto-create-manage-server-portal/create-server-pricing-tier.png)</span><span class="sxs-lookup"><span data-stu-id="673bc-138">![create-server-pricing-tier](./media/howto-create-manage-server-portal/create-server-pricing-tier.png)</span></span>

<span data-ttu-id="673bc-139">Cliquez sur 5 **créer** serveur hello de tooprovision.</span><span class="sxs-lookup"><span data-stu-id="673bc-139">5- Click **Create** tooprovision hello server.</span></span> <span data-ttu-id="673bc-140">L’approvisionnement prend quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="673bc-140">Provisioning takes a few minutes.</span></span>

> <span data-ttu-id="673bc-141">Vérifiez hello **toodashboard du code confidentiel** option tooallow simplifier le suivi de vos déploiements.</span><span class="sxs-lookup"><span data-stu-id="673bc-141">Check hello **Pin toodashboard** option tooallow easy tracking of your deployments.</span></span>
> [!NOTE]
> <span data-ttu-id="673bc-142">Bien que les too1000GB dans le niveau de base et 10000 Go dans la norme couche est prises en charge pour le stockage, version préliminaire publique, maximale de stockage hello est toujours limitée too1000GB temporairement.</span><span class="sxs-lookup"><span data-stu-id="673bc-142">Although up too1000GB in Basic tier and 10000GB in Standard tier will be supported for storage, for Public Preview, hello maximum storage is still limited too1000GB temporarily.</span></span> 
</Include>

## <a name="update-an-azure-database-for-mysql-server"></a><span data-ttu-id="673bc-143">Mise à jour d’un serveur Azure Database pour MySQL</span><span class="sxs-lookup"><span data-stu-id="673bc-143">Update an Azure Database for MySQL server</span></span>
<span data-ttu-id="673bc-144">Une fois le nouveau serveur est configuré, utilisateur dispose d’un serveur existant 2 options tooedit : réinitialiser le mot de passe administrateur ou d’échelle haut/bas server de hello en modifiant les unités de calcul hello.</span><span class="sxs-lookup"><span data-stu-id="673bc-144">After new server is provisioned, user has 2 options tooedit an existing server: reset administrator password or scale up/down hello server by changing hello compute-units.</span></span>

### <a name="change-hello-administrator-user-password"></a><span data-ttu-id="673bc-145">Mot de passe de l’utilisateur d’administrateur modification hello</span><span class="sxs-lookup"><span data-stu-id="673bc-145">Change hello administrator user password</span></span>
<span data-ttu-id="673bc-146">1 - sur le serveur de hello **vue d’ensemble** panneau, cliquez sur **réinitialisation de mot de passe** toopopulate une fenêtre d’entrée et la confirmation de mot de passe.</span><span class="sxs-lookup"><span data-stu-id="673bc-146">1- On hello server **Overview** blade, click **Reset password** toopopulate a password input and confirmation window.</span></span>

<span data-ttu-id="673bc-147">2 - Entrez le nouveau mot de passe et confirmer le mot de passe hello dans la fenêtre hello comme indiqué ci-dessous : ![réinitialisation de mot de passe](./media/howto-create-manage-server-portal/reset-password.png)</span><span class="sxs-lookup"><span data-stu-id="673bc-147">2- Enter new password and confirm hello password in hello window as below: ![reset-password](./media/howto-create-manage-server-portal/reset-password.png)</span></span>

<span data-ttu-id="673bc-148">3-Cliquez **OK** toosave hello nouveau mot de passe.</span><span class="sxs-lookup"><span data-stu-id="673bc-148">3- Click **OK** toosave hello new password.</span></span>

### <a name="scale-updown-by-changing-compute-units"></a><span data-ttu-id="673bc-149">Montée/descente en puissance en modifiant les unités de calcul</span><span class="sxs-lookup"><span data-stu-id="673bc-149">Scale up/down by changing Compute Units</span></span>

<span data-ttu-id="673bc-150">1 - sur le panneau de serveur hello, sous **paramètres**, cliquez sur **niveau tarifaire** Panneau de niveau de tarification de hello tooopen pour hello Azure de base de données du serveur MySQL.</span><span class="sxs-lookup"><span data-stu-id="673bc-150">1- On hello server blade, under **Settings**, click **Pricing tier** tooopen hello Pricing tier blade for hello Azure Database for MySQL server.</span></span>

<span data-ttu-id="673bc-151">Étape 2-Suivez 4 dans **créer une base de données Azure pour le serveur MySQL** toochange les unités de calcul en hello même niveau de tarification.</span><span class="sxs-lookup"><span data-stu-id="673bc-151">2- Follow Step 4 in **Create an Azure Database for MySQL server** toochange Compute Units in hello same pricing tier.</span></span>

## <a name="delete-an-azure-database-for-mysql-server"></a><span data-ttu-id="673bc-152">Suppression d’un serveur Azure Database pour MySQL</span><span class="sxs-lookup"><span data-stu-id="673bc-152">Delete an Azure Database for MySQL server</span></span>

<span data-ttu-id="673bc-153">1 - sur le serveur de hello **vue d’ensemble** panneau, cliquez sur **supprimer** Panneau de confirmation de commande bouton tooopen hello suppression.</span><span class="sxs-lookup"><span data-stu-id="673bc-153">1- On hello server **Overview** blade, click **Delete** command button tooopen hello Deleting confirmation blade.</span></span>

<span data-ttu-id="673bc-154">Nom de serveur correct 2-type hello dans la zone d’entrée du panneau hello confirmation double.</span><span class="sxs-lookup"><span data-stu-id="673bc-154">2- Type hello correct server name in input box of hello blade for double confirmation.</span></span>

<span data-ttu-id="673bc-155">3-Cliquez **supprimer** bouton Nouveau tooconfirm suppression d’action et attendez que « Suppression de réussite » le menu contextuel sur la barre de notification hello.</span><span class="sxs-lookup"><span data-stu-id="673bc-155">3- Click **Delete** button again tooconfirm deleting action and wait for “Deleting success” popup on hello notification bar.</span></span>

## <a name="list-hello-azure-database-for-mysql-databases"></a><span data-ttu-id="673bc-156">Liste hello Azure de base de données pour les bases de données MySQL</span><span class="sxs-lookup"><span data-stu-id="673bc-156">List hello Azure Database for MySQL databases</span></span>
<span data-ttu-id="673bc-157">Sur le serveur de hello **vue d’ensemble** panneau, faites défiler vers le bas jusqu'à ce que vous voyiez de la base de données hello vignette sous hello.</span><span class="sxs-lookup"><span data-stu-id="673bc-157">On hello server **Overview** blade, scroll down until you see hello database tile on hello bottom.</span></span> <span data-ttu-id="673bc-158">Toutes les bases de données hello seront afficheront dans la table de hello.</span><span class="sxs-lookup"><span data-stu-id="673bc-158">All hello databases will be listed in hello table.</span></span> <span data-ttu-id="673bc-159">Cliquez sur **supprimer** Panneau de confirmation de commande bouton tooopen hello suppression.</span><span class="sxs-lookup"><span data-stu-id="673bc-159">click **Delete** command button tooopen hello Deleting confirmation blade.</span></span>

![show-databases](./media/howto-create-manage-server-portal/show-databases.png)

## <a name="show-details-of-an-azure-database-for-mysql-server"></a><span data-ttu-id="673bc-161">Affichage des détails d’un serveur Azure Database pour MySQL</span><span class="sxs-lookup"><span data-stu-id="673bc-161">Show details of an Azure Database for MySQL server</span></span>
<span data-ttu-id="673bc-162">Cliquez sur **propriétés** sous **paramètres** sur le serveur de hello panneau hello **propriétés** panneau.</span><span class="sxs-lookup"><span data-stu-id="673bc-162">Click **Properties** under **Settings** on hello server blade will open hello **Properties** blade.</span></span> <span data-ttu-id="673bc-163">Vous pouvez afficher toutes les informations détaillées sur les serveur hello.</span><span class="sxs-lookup"><span data-stu-id="673bc-163">Then you can view all detailed information about hello server.</span></span>

## <a name="next-steps"></a><span data-ttu-id="673bc-164">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="673bc-164">Next steps</span></span>

[<span data-ttu-id="673bc-165">Démarrage rapide : création d’un serveur Azure Database pour MySQL à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="673bc-165">Quickstart: Create Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
