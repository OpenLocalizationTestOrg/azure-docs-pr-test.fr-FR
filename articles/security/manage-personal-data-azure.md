---
title: "Gérer les données personnelles dans Microsoft Azure | Microsoft Docs"
description: "conseils pour corriger, mettre à jour, supprimer et exporter des données personnelles dans Azure Active Directory et Azure SQL Database"
services: security
documentationcenter: na
author: barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: barclayn
ms.openlocfilehash: b04c745feb710d3d1d8a1fce23807168d6e6fa3d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-personal-data-in-microsoft-azure"></a><span data-ttu-id="2a7c8-103">Gérer les données personnelles dans Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="2a7c8-103">Manage personal data in Microsoft Azure</span></span>

<span data-ttu-id="2a7c8-104">Cet article fournit des conseils pour corriger, mettre à jour, supprimer et exporter des données personnelles dans Azure Active Directory et Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="2a7c8-104">This article provides guidance on how to correct, update, delete, and export personal data in Azure Active Directory and Azure SQL Database.</span></span>

## <a name="scenario"></a><span data-ttu-id="2a7c8-105">Scénario</span><span class="sxs-lookup"><span data-stu-id="2a7c8-105">Scenario</span></span>

<span data-ttu-id="2a7c8-106">Une entreprise basée à Dublin propose à sa clientèle nationale et internationale des services clé en main d’organisation de mariages haut de gamme en Irlande et dans le monde entier.</span><span class="sxs-lookup"><span data-stu-id="2a7c8-106">A Dublin-based company provides one-stop shopping for high end destination weddings in Ireland and around the world for both a local and international customer base.</span></span> <span data-ttu-id="2a7c8-107">Elle possède des bureaux, des clients, des employés et des prestataires dans le monde entier pour assurer des services complets sur place.</span><span class="sxs-lookup"><span data-stu-id="2a7c8-107">They have offices, customers, employees, and vendors located around the world to fully service the venues they offer.</span></span>

<span data-ttu-id="2a7c8-108">Parmi les différents services qu’elle propose, l’entreprise assure le suivi des réponses et prend en compte les allergies et préférences alimentaires des invités.</span><span class="sxs-lookup"><span data-stu-id="2a7c8-108">Among many other items, the company keeps track of RSVPs that include food allergies and dietary preferences.</span></span> <span data-ttu-id="2a7c8-109">Les personnes invitées à un mariage peuvent s’inscrire à diverses activités, comme l’équitation, le surf, les promenades en bateau, etc. et même échanger entre eux sur une page web centrale dans les mois qui précèdent l’événement.</span><span class="sxs-lookup"><span data-stu-id="2a7c8-109">Wedding guests can register for various activities such as horseback riding, surfing, boat rides, etc., and even interact with one another on a central web page during the months leading up to the event.</span></span> <span data-ttu-id="2a7c8-110">L’entreprise collecte des informations personnelles sur les employés, les prestataires, les clients et les invités du mariage.</span><span class="sxs-lookup"><span data-stu-id="2a7c8-110">The company collects personal information from employees, vendors, customers, and wedding guests.</span></span> <span data-ttu-id="2a7c8-111">Compte tenu de la dimension internationale de l’activité, l’entreprise doit se conformer à plusieurs niveaux de réglementation.</span><span class="sxs-lookup"><span data-stu-id="2a7c8-111">Because of the international nature of the business the company must comply with multiple levels of regulation.</span></span>

## <a name="problem-statement"></a><span data-ttu-id="2a7c8-112">Définition du problème</span><span class="sxs-lookup"><span data-stu-id="2a7c8-112">Problem statement</span></span>

- <span data-ttu-id="2a7c8-113">Les administrateurs de données doivent pouvoir corriger les informations personnelles inexactes et mettre à jour celles qui sont incomplètes ou qui ont changé.</span><span class="sxs-lookup"><span data-stu-id="2a7c8-113">Data admins must be able to correct inaccurate personal information and update incomplete or changing personal information.</span></span>

- <span data-ttu-id="2a7c8-114">Nécessité d’administrateurs de données doit être en mesure de supprimer les informations personnelles à la demande d’un objet de données.</span><span class="sxs-lookup"><span data-stu-id="2a7c8-114">Data admins need must be able to delete personal information upon the request of a data subject.</span></span>

- <span data-ttu-id="2a7c8-115">Les administrateurs de données doivent pouvoir exporter les données et les fournir dans un format courant et structuré à la personne concernée qui en fait la demande.</span><span class="sxs-lookup"><span data-stu-id="2a7c8-115">Data admins need to export data and provide it to a data subject in a common, structured format upon his or her request.</span></span>

## <a name="company-goals"></a><span data-ttu-id="2a7c8-116">Objectifs de l’entreprise</span><span class="sxs-lookup"><span data-stu-id="2a7c8-116">Company goals</span></span>

- <span data-ttu-id="2a7c8-117">Les informations inexactes ou incomplètes sur les clients, les invités du mariage, les employés et les fournisseurs doivent être corrigées ou mises à jour dans Azure Active Directory et Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="2a7c8-117">Inaccurate or incomplete customer, wedding guest, employee, and vendor personal information must be corrected or updated in Azure Active Directory and Azure SQL Database.</span></span>

- <span data-ttu-id="2a7c8-118">Les informations personnelles doivent pouvoir être supprimées dans Azure Active Directory et Azure SQL Database à la demande de la personne concernée.</span><span class="sxs-lookup"><span data-stu-id="2a7c8-118">Personal information must be deleted in Azure Active Directory and Azure SQL Database upon the request of a data subject.</span></span>

- <span data-ttu-id="2a7c8-119">Les données personnelles doivent pouvoir être exportées dans un format commun et structuré à la demande de la personne concernée.</span><span class="sxs-lookup"><span data-stu-id="2a7c8-119">Personal data must be exported in a common, structured format upon the request of a data subject.</span></span>

## <a name="solutions"></a><span data-ttu-id="2a7c8-120">Solutions</span><span class="sxs-lookup"><span data-stu-id="2a7c8-120">Solutions</span></span>

### <a name="azure-active-directory-rectifycorrect-inaccurate-or-incomplete-personal-data-and-erasedelete-personal-datauser-profiles"></a><span data-ttu-id="2a7c8-121">Azure Active Directory : rectifier/corriger des données personnelles inexactes ou incomplètes et effacer/supprimer des données personnelles/profils utilisateur</span><span class="sxs-lookup"><span data-stu-id="2a7c8-121">Azure Active Directory: rectify/correct inaccurate or incomplete personal data and erase/delete personal data/user profiles</span></span>

<span data-ttu-id="2a7c8-122">[Azure Active Directory](https://azure.microsoft.com/services/active-directory/) est le service Microsoft de gestion d’annuaires et d’identités multilocataire basé sur le cloud.</span><span class="sxs-lookup"><span data-stu-id="2a7c8-122">[Azure Active Directory](https://azure.microsoft.com/services/active-directory/) is Microsoft’s cloud-based, multi-tenant directory and identity management service.</span></span>
<span data-ttu-id="2a7c8-123">Vous pouvez corriger, mettre à jour ou supprimer les profils utilisateur de clients et d’employés et les informations professionnelles utilisateur qui contiennent des données personnelles, telles que le nom d’utilisateur, la fonction, l’adresse ou le numéro de téléphone dans votre environnement [Azure Active Directory](https://azure.microsoft.com/services/active-directory/) (AAD) via le [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="2a7c8-123">You can correct, update, or delete customer and employee user profiles and user work information that contain personal data, such as a user’s name, work title, address, or phone number, in your [Azure Active Directory](https://azure.microsoft.com/services/active-directory/) (AAD) environment by using the [Azure portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="2a7c8-124">Vous devez vous connecter avec un compte d’administrateur général de l’annuaire.</span><span class="sxs-lookup"><span data-stu-id="2a7c8-124">You must sign in with an account that’s a global admin for the directory.</span></span>

#### <a name="how-do-i-correct-or-update-user-profile-and-work-information-in-azure-active-directory"></a><span data-ttu-id="2a7c8-125">Comment corriger ou mettre à jour des informations professionnelles et de profil utilisateur dans Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="2a7c8-125">How do I correct or update user profile and work information in Azure Active Directory?</span></span>

1. <span data-ttu-id="2a7c8-126">Connectez-vous au [portail Azure](https://portal.azure.com) en utilisant un compte d’administrateur général pour le répertoire.</span><span class="sxs-lookup"><span data-stu-id="2a7c8-126">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>

2. <span data-ttu-id="2a7c8-127">Sélectionnez **Plus de services**, saisissez **Utilisateurs et groupes** dans la zone de texte, puis sélectionnez **Entrée**.</span><span class="sxs-lookup"><span data-stu-id="2a7c8-127">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

    ![media/image1.png](media/manage-personal-data-azure/image001.png)

3. <span data-ttu-id="2a7c8-129">Dans le panneau **Utilisateurs et groupes**, sélectionnez **Utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="2a7c8-129">On the **Users and groups** blade, select **Users**.</span></span>

    ![media/image2.png](media/manage-personal-data-azure/image003.png)

4. <span data-ttu-id="2a7c8-131">Dans le panneau **Utilisateurs et groupes - Utilisateurs**, sélectionnez un utilisateur dans la liste puis, dans le panneau de l’utilisateur sélectionné, sélectionnez **Profil** pour afficher les informations de profil utilisateur qu’il convient de corriger ou de mettre à jour.</span><span class="sxs-lookup"><span data-stu-id="2a7c8-131">On the **Users and groups - Users** blade, select a user from the list, and then, on the blade for the selected user, select **Profile** to view the user profile information that needs to be corrected or updated.</span></span>

    ![media/image3.png](media/manage-personal-data-azure/image005.png)

5. <span data-ttu-id="2a7c8-133">Corrigez ou mettez à jour les informations puis, dans la barre de commandes, sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="2a7c8-133">Correct or update the information, and then, in the command bar, select **Save.**</span></span>

6.  <span data-ttu-id="2a7c8-134">Dans le panneau de l’utilisateur sélectionné, sélectionnez **Informations professionnelles** pour afficher les informations professionnelles utilisateur qu’il convient de corriger ou de mettre à jour.</span><span class="sxs-lookup"><span data-stu-id="2a7c8-134">On the blade for the selected user, select **Work Info** to view user work information that needs to be corrected or updated.</span></span>

    ![media/image4.png](media/manage-personal-data-azure/image007.png)

7. <span data-ttu-id="2a7c8-136">Corrigez ou mettez à jour les informations professionnelles utilisateur puis, dans la barre de commandes, sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="2a7c8-136">Correct or update the user work information, and then, in the command bar, select **Save.**</span></span>

#### <a name="how-do-i-delete-a-user-profile-in-azure-active-directory"></a><span data-ttu-id="2a7c8-137">Comment supprimer un profil utilisateur dans Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="2a7c8-137">How do I delete a user profile in Azure Active Directory?</span></span>

1. <span data-ttu-id="2a7c8-138">Connectez-vous au [portail Azure](https://portal.azure.com) en utilisant un compte d’administrateur général pour le répertoire.</span><span class="sxs-lookup"><span data-stu-id="2a7c8-138">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>

2. <span data-ttu-id="2a7c8-139">Sélectionnez **Plus de services**, saisissez **Utilisateurs et groupes** dans la zone de texte, puis sélectionnez **Entrée**.</span><span class="sxs-lookup"><span data-stu-id="2a7c8-139">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

    ![](media/manage-personal-data-azure/image001.png)

3. <span data-ttu-id="2a7c8-140">Dans le panneau **Utilisateurs et groupes**, sélectionnez **Utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="2a7c8-140">On the **Users and groups** blade, select **Users**.</span></span>

    ![media/image2.png](media/manage-personal-data-azure/image003.png)

4. <span data-ttu-id="2a7c8-142">Sur le panneau **Utilisateurs et groupes - Utilisateurs -** , sélectionnez un utilisateur dans la liste.</span><span class="sxs-lookup"><span data-stu-id="2a7c8-142">On the **Users and groups - Users** blade, select a user from the list.</span></span>

    ![media/image3.png](media/manage-personal-data-azure/image007.png)

5. <span data-ttu-id="2a7c8-144">Dans le panneau de l’utilisateur sélectionné, sélectionnez **Vue d’ensemble**, puis, dans la barre de commandes, sélectionnez **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="2a7c8-144">On the blade for the selected user, select **Overview**, and then in the command bar, select **Delete**.</span></span>

    ![](media/manage-personal-data-azure/image013.png)

### <a name="sql-database-rectifycorrect-inaccurate-or-incomplete-personal-data-erasedelete-personal-data-export-personal-data"></a><span data-ttu-id="2a7c8-145">SQL Database : rectifier/corriger des données personnelles inexactes ou incomplètes ; effacer/supprimer des données personnelles ; exporter des données personnelles</span><span class="sxs-lookup"><span data-stu-id="2a7c8-145">SQL Database: rectify/correct inaccurate or incomplete personal data; erase/delete personal data; export personal data</span></span> 

<span data-ttu-id="2a7c8-146">[Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) est une base de données cloud qui permet aux développeurs de créer et tenir à jour des applications.</span><span class="sxs-lookup"><span data-stu-id="2a7c8-146">[Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) is a cloud database that helps developers build and maintain applications.</span></span>

<span data-ttu-id="2a7c8-147">Les données personnelles peuvent être mises à jour dans [Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) à l’aide de requêtes SQL standard et peuvent aussi être supprimées.</span><span class="sxs-lookup"><span data-stu-id="2a7c8-147">Personal data can be updated in [Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) using standard SQL queries, and it can also be deleted.</span></span> <span data-ttu-id="2a7c8-148">Par ailleurs, les données personnelles peuvent être exportées à partir de SQL Database selon différentes méthodes, notamment à l’aide de l’Assistant Importation et Exportation Azure SQL Server, et dans divers formats, notamment sous forme de fichier BACPAC.</span><span class="sxs-lookup"><span data-stu-id="2a7c8-148">Additionally, personal data can be exported from SQL Database using a variety of methods, including the Azure SQL Server import and export wizard, and in a variety of formats, including a BACPAC file.</span></span>

#### <a name="how-do-i-correct-update-or-erase-personal-data-in-sql-database"></a><span data-ttu-id="2a7c8-149">Comment corriger, mettre à jour ou supprimer des données personnelles dans SQL Database ?</span><span class="sxs-lookup"><span data-stu-id="2a7c8-149">How do I correct, update, or erase personal data in SQL Database?</span></span>

<span data-ttu-id="2a7c8-150">Pour savoir comment corriger ou mettre à jour des données personnelles dans SQL Database, consultez la documentation [Update (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/queries/update-transact-sql), [Update Text](https://docs.microsoft.com/sql/t-sql/queries/updatetext-transact-sql), [Update with Common Table Expression](https://docs.microsoft.com/sql/t-sql/queries/with-common-table-expression-transact-sql) ou [Update Write Text](https://docs.microsoft.com/sql/t-sql/queries/writetext-transact-sql).</span><span class="sxs-lookup"><span data-stu-id="2a7c8-150">To learn how to correct or update personal data in SQL Database, visit the [Update (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/queries/update-transact-sql), [Update Text](https://docs.microsoft.com/sql/t-sql/queries/updatetext-transact-sql), [Update with Common Table Expression](https://docs.microsoft.com/sql/t-sql/queries/with-common-table-expression-transact-sql), or [Update Write Text](https://docs.microsoft.com/sql/t-sql/queries/writetext-transact-sql) documentation.</span></span>

<span data-ttu-id="2a7c8-151">Pour savoir comment supprimer des données personnelles dans SQL Database, consultez la documentation [Delete (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/delete-transact-sql).</span><span class="sxs-lookup"><span data-stu-id="2a7c8-151">To learn how to delete personal data in SQL Database, visit the [Delete (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/delete-transact-sql) documentation.</span></span>

#### <a name="how-do-i-export-personal-data-to-a-bacpac-file-in-sql-database"></a><span data-ttu-id="2a7c8-152">Comment exporter des données personnelles dans un fichier BACPAC dans SQL Database ?</span><span class="sxs-lookup"><span data-stu-id="2a7c8-152">How do I export personal data to a BACPAC file in SQL Database?</span></span>

<span data-ttu-id="2a7c8-153">Un fichier BACPAC comporte des données et des métadonnées SQL Database. Il s’agit d’un fichier compressé doté d’une extension BACPAC.</span><span class="sxs-lookup"><span data-stu-id="2a7c8-153">A BACPAC file includes the SQL Database data and metadata and is a zip file with a BACPAC extension.</span></span> <span data-ttu-id="2a7c8-154">Cette opération peut se faire via le [portail Azure](https://portal.azure.com/), l’utilitaire en ligne de commande SQLPackage, SQL Server Management Studio (SSMS) ou PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2a7c8-154">This can be done using the [Azure portal](https://portal.azure.com/), the SQLPackage command-line utility, SQL Server Management Studio (SSMS), or PowerShell.</span></span>

<span data-ttu-id="2a7c8-155">Pour savoir comment exporter des données dans un fichier BACPAC, consultez la page [Exporter une base de données SQL Azure dans un fichier BACPAC](https://docs.microsoft.com/azure/sql-database/sql-database-export). Vous y trouverez des instructions détaillées pour chaque méthode mentionnée ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="2a7c8-155">To learn how to export data to a BACPAC file, visit the [Export an Azure SQL database to a BACPAC file](https://docs.microsoft.com/azure/sql-database/sql-database-export) page, which includes detailed instructions for each method listed above.</span></span>

<span data-ttu-id="2a7c8-156">Comment exporter des données personnelles à partir de SQL Database avec l’Assistant Importation et Exportation SQL Server ?</span><span class="sxs-lookup"><span data-stu-id="2a7c8-156">How do I export personal data from SQL Database with the SQL Server Import and Export Wizard?</span></span>

<span data-ttu-id="2a7c8-157">Cet Assistant vous permet de copier des données d’une source vers une destination.</span><span class="sxs-lookup"><span data-stu-id="2a7c8-157">This wizard helps you copy data from a source to a destination.</span></span> <span data-ttu-id="2a7c8-158">Pour obtenir une présentation de l’Assistant, notamment des informations d’autorisation, et pour savoir comment vous procurer l’outil et obtenir de l’aide sur celui-ci, consultez la page web [Importer et exporter des données avec l’Assistant Importation et Exportation SQL Server](https://docs.microsoft.com/sql/integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard).</span><span class="sxs-lookup"><span data-stu-id="2a7c8-158">For an introduction to the wizard, including how to get it, permissions information, and how to get help with the tool, visit the [Import and Export Data with the SQL Server Import and Export Wizard](https://docs.microsoft.com/sql/integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard) web page.</span></span>

<span data-ttu-id="2a7c8-159">Pour obtenir une vue d’ensemble des étapes de l’Assistant, consultez la page web [Étapes de l’Assistant Importation et Exportation SQL Server](https://docs.microsoft.com/sql/integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard).</span><span class="sxs-lookup"><span data-stu-id="2a7c8-159">For an overview of steps for the wizard, visit the [Steps in the SQL Server Import and Export Wizard](https://docs.microsoft.com/sql/integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard) web page.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2a7c8-160">Étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="2a7c8-160">Next Steps:</span></span>

[<span data-ttu-id="2a7c8-161">Base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="2a7c8-161">Azure SQL Database</span></span>](https://azure.microsoft.com/services/sql-database/?v=16.50) 

[<span data-ttu-id="2a7c8-162">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2a7c8-162">Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

