---
title: "Création et gestion d’un serveur Azure Database pour MySQL à l’aide du portail Azure | Microsoft Docs"
description: "Cet article explique comment créer rapidement un nouveau serveur Azure Database pour MySQL et gérer le serveur à l’aide du portail Azure."
services: mysql
author: v-chenyh
ms.author: nolanwu
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 4605518b6955d9943e76c25df2d4105a6a94433d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-azure-database-for-mysql-server-using-azure-portal"></a><span data-ttu-id="4728c-103">Création et gestion d’un serveur Azure Database pour MySQL à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="4728c-103">Create and manage Azure Database for MySQL server using Azure portal</span></span>
<span data-ttu-id="4728c-104">Cet article explique comment créer rapidement un nouveau serveur Azure Database pour MySQL et gérer le serveur à l’aide du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="4728c-104">This article describes how you can quickly create a new Azure Database for MySQL server and manage the server using the Azure Portal.</span></span> <span data-ttu-id="4728c-105">La gestion du serveur inclut l’affichage des détails de ce serveur et les bases de données, la réinitialisation de mot de passe et la suppression du serveur.</span><span class="sxs-lookup"><span data-stu-id="4728c-105">Server management includes viewing server details & databases, resetting password and deleting the server.</span></span>

## <a name="log-in-to-the-azure-portal"></a><span data-ttu-id="4728c-106">Connectez-vous au portail Azure.</span><span class="sxs-lookup"><span data-stu-id="4728c-106">Log in to the Azure portal</span></span>
<span data-ttu-id="4728c-107">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4728c-107">Log in to the [Azure portal](https://portal.azure.com).</span></span>

## <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="4728c-108">Création d’un serveur Azure Database pour MySQL</span><span class="sxs-lookup"><span data-stu-id="4728c-108">Create an Azure Database for MySQL server</span></span>
<span data-ttu-id="4728c-109">Suivez ces étapes pour créer un serveur Azure Database pour MySQL nommé « mysqlserver4demo »</span><span class="sxs-lookup"><span data-stu-id="4728c-109">Follow these steps to create an Azure Database for MySQL server named “mysqlserver4demo”</span></span>

<span data-ttu-id="4728c-110">1 - Cliquez sur le bouton **Nouveau** dans le coin supérieur gauche du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="4728c-110">1- Click **New** button found on the upper left-hand corner of the Azure portal.</span></span>

<span data-ttu-id="4728c-111">2- Sélectionnez **Bases de données** dans la page Nouveau, puis **Base de données Azure pour MySQL** dans la page Bases de données.</span><span class="sxs-lookup"><span data-stu-id="4728c-111">2- Select **Databases** from the New page, and select **Azure Database for MySQL** from the Databases page.</span></span>

> <span data-ttu-id="4728c-112">Un serveur Azure Database pour MySQL est créé avec un ensemble défini de [ressources de calcul et de stockage](./concepts-compute-unit-and-storage.md).</span><span class="sxs-lookup"><span data-stu-id="4728c-112">An Azure Database for MySQL server is created with a defined set of [compute and storage](./concepts-compute-unit-and-storage.md) resources.</span></span> <span data-ttu-id="4728c-113">La base de données est créée dans un groupe de ressources Azure et dans un serveur Azure Database pour MySQL.</span><span class="sxs-lookup"><span data-stu-id="4728c-113">The database is created within an Azure resource group and in an Azure Database for MySQL server.</span></span>

![create-new-server](./media/howto-create-manage-server-portal/create-new-server.png)

<span data-ttu-id="4728c-115">3 - remplissez le formulaire de la base de données Azure pour MySQL avec les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="4728c-115">3- Fill out the Azure Database for MySQL form with the following information:</span></span>

| <span data-ttu-id="4728c-116">**Champ de formulaire**</span><span class="sxs-lookup"><span data-stu-id="4728c-116">**Form Field**</span></span> | <span data-ttu-id="4728c-117">**Description du champ**</span><span class="sxs-lookup"><span data-stu-id="4728c-117">**Field Description**</span></span> |
|----------------|-----------------------|
| <span data-ttu-id="4728c-118">*Nom du serveur*</span><span class="sxs-lookup"><span data-stu-id="4728c-118">*Server name*</span></span> | <span data-ttu-id="4728c-119">azure-mysql (le nom du serveur est globalement unique)</span><span class="sxs-lookup"><span data-stu-id="4728c-119">azure-mysql (server name is globally unique)</span></span> |
| <span data-ttu-id="4728c-120">*Abonnement*</span><span class="sxs-lookup"><span data-stu-id="4728c-120">*Subscription*</span></span> | <span data-ttu-id="4728c-121">MySQLaaS (sélectionnez une option dans le menu déroulant)</span><span class="sxs-lookup"><span data-stu-id="4728c-121">MySQLaaS (select from drop down)</span></span> |
| <span data-ttu-id="4728c-122">*Groupe de ressources*</span><span class="sxs-lookup"><span data-stu-id="4728c-122">*Resource group*</span></span> | <span data-ttu-id="4728c-123">myresource (créez un nouveau groupe de ressources ou utilisez un groupe existant)</span><span class="sxs-lookup"><span data-stu-id="4728c-123">myresource (create a new resource group or use an existing one)</span></span> |
| <span data-ttu-id="4728c-124">*Connexion d’administrateur serveur*</span><span class="sxs-lookup"><span data-stu-id="4728c-124">*Server admin login*</span></span> | <span data-ttu-id="4728c-125">myadmin (nom du compte administrateur de l’installation)</span><span class="sxs-lookup"><span data-stu-id="4728c-125">myadmin (setup admin account name)</span></span> |
| <span data-ttu-id="4728c-126">*Mot de passe*</span><span class="sxs-lookup"><span data-stu-id="4728c-126">*Password*</span></span> | <span data-ttu-id="4728c-127">mot de passe du compte administrateur de l’installation</span><span class="sxs-lookup"><span data-stu-id="4728c-127">setup admin account password</span></span> |
| <span data-ttu-id="4728c-128">*Confirmer le mot de passe*</span><span class="sxs-lookup"><span data-stu-id="4728c-128">*Confirm password*</span></span> | <span data-ttu-id="4728c-129">confirmez le mot de passe du compte administrateur</span><span class="sxs-lookup"><span data-stu-id="4728c-129">confirm admin account password</span></span> |
| <span data-ttu-id="4728c-130">*Emplacement*</span><span class="sxs-lookup"><span data-stu-id="4728c-130">*Location*</span></span> | <span data-ttu-id="4728c-131">Europe du Nord (sélection Europe du Nord ou États-Unis de l'Ouest)</span><span class="sxs-lookup"><span data-stu-id="4728c-131">North Europe (select between North Europe and West US)</span></span> |
| <span data-ttu-id="4728c-132">*Version*</span><span class="sxs-lookup"><span data-stu-id="4728c-132">*Version*</span></span> | <span data-ttu-id="4728c-133">5.6 (choisissez la version du serveur Azure Database pour MySQL)</span><span class="sxs-lookup"><span data-stu-id="4728c-133">5.6 (choose Azure Database for MySQL server version)</span></span> |

<span data-ttu-id="4728c-134">4 - Cliquez sur **Niveau tarifaire** pour spécifier le niveau de service et le niveau de performances pour votre nouveau serveur.</span><span class="sxs-lookup"><span data-stu-id="4728c-134">4- Click **Pricing tier** to specify the service tier and performance level for your new server.</span></span> <span data-ttu-id="4728c-135">L’unité de calcul peut être configurée entre 50 et 100 dans le niveau de base, entre 100 et 200 dans le niveau standard, et vous pouvez augmenter le stockage en fonction du montant inclus.</span><span class="sxs-lookup"><span data-stu-id="4728c-135">Compute Unit can be configured between 50 and 100 in Basic tier, 100 and 200 in Standard tier, and storage can be added based on included amount.</span></span> <span data-ttu-id="4728c-136">Pour ce guide pratique, choisissons 50 unités de calcul et 50 Go.</span><span class="sxs-lookup"><span data-stu-id="4728c-136">For this HowTo guide, let’s choose 50 Compute Unit and 50GB.</span></span> <span data-ttu-id="4728c-137">Cliquez sur **OK** pour enregistrer votre sélection.</span><span class="sxs-lookup"><span data-stu-id="4728c-137">Click **OK** to save your selection.</span></span>
<span data-ttu-id="4728c-138">![create-server-pricing-tier](./media/howto-create-manage-server-portal/create-server-pricing-tier.png)</span><span class="sxs-lookup"><span data-stu-id="4728c-138">![create-server-pricing-tier](./media/howto-create-manage-server-portal/create-server-pricing-tier.png)</span></span>

<span data-ttu-id="4728c-139">5 - Cliquez sur **Créer** pour approvisionner le serveur.</span><span class="sxs-lookup"><span data-stu-id="4728c-139">5- Click **Create** to provision the server.</span></span> <span data-ttu-id="4728c-140">L’approvisionnement prend quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="4728c-140">Provisioning takes a few minutes.</span></span>

> <span data-ttu-id="4728c-141">Cochez l’option **Épingler au tableau de bord** pour faciliter le suivi de vos déploiements.</span><span class="sxs-lookup"><span data-stu-id="4728c-141">Check the **Pin to dashboard** option to allow easy tracking of your deployments.</span></span>
> [!NOTE]
> <span data-ttu-id="4728c-142">Bien que les niveaux de base et standard prennent en charge jusqu'à 1 000 Go et 10 000 Go de stockage respectivement, le stockage maximum pour la version préliminaire publique reste temporairement limité à 1 000 Go.</span><span class="sxs-lookup"><span data-stu-id="4728c-142">Although up to 1000GB in Basic tier and 10000GB in Standard tier will be supported for storage, for Public Preview, the maximum storage is still limited to 1000GB temporarily.</span></span> 
</Include>

## <a name="update-an-azure-database-for-mysql-server"></a><span data-ttu-id="4728c-143">Mise à jour d’un serveur Azure Database pour MySQL</span><span class="sxs-lookup"><span data-stu-id="4728c-143">Update an Azure Database for MySQL server</span></span>
<span data-ttu-id="4728c-144">Une fois le nouveau serveur approvisionné, l’utilisateur dispose de 2 options pour modifier un serveur existant : réinitialiser un mot de passe administrateur ou effectuer une montée/descente en puissance du serveur en modifiant les unités de calcul.</span><span class="sxs-lookup"><span data-stu-id="4728c-144">After new server is provisioned, user has 2 options to edit an existing server: reset administrator password or scale up/down the server by changing the compute-units.</span></span>

### <a name="change-the-administrator-user-password"></a><span data-ttu-id="4728c-145">Modification du mot de passe administrateur</span><span class="sxs-lookup"><span data-stu-id="4728c-145">Change the administrator user password</span></span>
<span data-ttu-id="4728c-146">1 - Dans le panneau **Vue d’ensemble** du serveur, cliquez sur **Réinitialiser le mot de passe** pour afficher une fenêtre de saisie puis de confirmation du mot de passe.</span><span class="sxs-lookup"><span data-stu-id="4728c-146">1- On the server **Overview** blade, click **Reset password** to populate a password input and confirmation window.</span></span>

<span data-ttu-id="4728c-147">2 - Saisissez puis confirmez le nouveau mot de passe dans la fenêtre, comme indiqué ci-dessous : ![reset-password](./media/howto-create-manage-server-portal/reset-password.png)</span><span class="sxs-lookup"><span data-stu-id="4728c-147">2- Enter new password and confirm the password in the window as below: ![reset-password](./media/howto-create-manage-server-portal/reset-password.png)</span></span>

<span data-ttu-id="4728c-148">3 - Cliquez sur **OK** pour enregistrer le nouveau mot de passe.</span><span class="sxs-lookup"><span data-stu-id="4728c-148">3- Click **OK** to save the new password.</span></span>

### <a name="scale-updown-by-changing-compute-units"></a><span data-ttu-id="4728c-149">Montée/descente en puissance en modifiant les unités de calcul</span><span class="sxs-lookup"><span data-stu-id="4728c-149">Scale up/down by changing Compute Units</span></span>

<span data-ttu-id="4728c-150">1 - Dans le panneau du serveur, sous **Paramètres**, cliquez sur **Niveau de tarification** pour ouvrir le panneau Niveau de tarification du serveur Azure Database pour MySQL.</span><span class="sxs-lookup"><span data-stu-id="4728c-150">1- On the server blade, under **Settings**, click **Pricing tier** to open the Pricing tier blade for the Azure Database for MySQL server.</span></span>

<span data-ttu-id="4728c-151">2 - Suivez l’étape 4 de la rubrique **Création d’un serveur Azure Database pour MySQL** pour modifier les unités de calcul dans le même niveau de tarification.</span><span class="sxs-lookup"><span data-stu-id="4728c-151">2- Follow Step 4 in **Create an Azure Database for MySQL server** to change Compute Units in the same pricing tier.</span></span>

## <a name="delete-an-azure-database-for-mysql-server"></a><span data-ttu-id="4728c-152">Suppression d’un serveur Azure Database pour MySQL</span><span class="sxs-lookup"><span data-stu-id="4728c-152">Delete an Azure Database for MySQL server</span></span>

<span data-ttu-id="4728c-153">1 - Dans le panneau **Vue d’ensemble** du serveur, cliquez sur le bouton de commande **Supprimer** pour ouvrir le panneau de confirmation de suppression.</span><span class="sxs-lookup"><span data-stu-id="4728c-153">1- On the server **Overview** blade, click **Delete** command button to open the Deleting confirmation blade.</span></span>

<span data-ttu-id="4728c-154">2 - Tapez le nom du serveur dans la zone d’entrée du panneau de double confirmation.</span><span class="sxs-lookup"><span data-stu-id="4728c-154">2- Type the correct server name in input box of the blade for double confirmation.</span></span>

<span data-ttu-id="4728c-155">3 - Cliquez de nouveau sur le bouton **Supprimer** pour confirmer l’action de suppression, puis attendez l’affichage du message « Deleting success » (suppression réussie) dans la barre de notification.</span><span class="sxs-lookup"><span data-stu-id="4728c-155">3- Click **Delete** button again to confirm deleting action and wait for “Deleting success” popup on the notification bar.</span></span>

## <a name="list-the-azure-database-for-mysql-databases"></a><span data-ttu-id="4728c-156">Liste des bases de données Azure pour MySQL</span><span class="sxs-lookup"><span data-stu-id="4728c-156">List the Azure Database for MySQL databases</span></span>
<span data-ttu-id="4728c-157">Dans le panneau **Vue d’ensemble** du serveur, faites défiler vers le bas jusqu'à atteindre la mosaïque des bases de données.</span><span class="sxs-lookup"><span data-stu-id="4728c-157">On the server **Overview** blade, scroll down until you see the database tile on the bottom.</span></span> <span data-ttu-id="4728c-158">Toutes les bases de données apparaissent dans le tableau.</span><span class="sxs-lookup"><span data-stu-id="4728c-158">All the databases will be listed in the table.</span></span> <span data-ttu-id="4728c-159">Cliquez sur le bouton de commande **Supprimer** pour ouvrir le panneau de confirmation de suppression.</span><span class="sxs-lookup"><span data-stu-id="4728c-159">click **Delete** command button to open the Deleting confirmation blade.</span></span>

![show-databases](./media/howto-create-manage-server-portal/show-databases.png)

## <a name="show-details-of-an-azure-database-for-mysql-server"></a><span data-ttu-id="4728c-161">Affichage des détails d’un serveur Azure Database pour MySQL</span><span class="sxs-lookup"><span data-stu-id="4728c-161">Show details of an Azure Database for MySQL server</span></span>
<span data-ttu-id="4728c-162">Cliquez sur **Propriétés** sous **Paramètres** dans le panneau du serveur pour ouvrir le panneau **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="4728c-162">Click **Properties** under **Settings** on the server blade will open the **Properties** blade.</span></span> <span data-ttu-id="4728c-163">Toutes les informations détaillées sur le serveur y sont indiquées.</span><span class="sxs-lookup"><span data-stu-id="4728c-163">Then you can view all detailed information about the server.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4728c-164">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4728c-164">Next steps</span></span>

[<span data-ttu-id="4728c-165">Démarrage rapide : création d’un serveur Azure Database pour MySQL à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="4728c-165">Quickstart: Create Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
