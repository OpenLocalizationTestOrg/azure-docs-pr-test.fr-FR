---
title: "aaaManage des données personnelles dans Microsoft Azure | Documents Microsoft"
description: "obtenir des conseils sur la façon dont toocorrect, mettre à jour, supprimer et exporter des données personnelles dans Azure Active Directory et de la base de données SQL Azure"
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
ms.openlocfilehash: 032f70d32377cb9395cb2c35c27dad05001537c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-personal-data-in-microsoft-azure"></a><span data-ttu-id="737cc-103">Gérer les données personnelles dans Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="737cc-103">Manage personal data in Microsoft Azure</span></span>

<span data-ttu-id="737cc-104">Cet article fournit des conseils sur la façon dont toocorrect, mettre à jour, supprimer et exporter des données personnelles dans Azure Active Directory et de la base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="737cc-104">This article provides guidance on how toocorrect, update, delete, and export personal data in Azure Active Directory and Azure SQL Database.</span></span>

## <a name="scenario"></a><span data-ttu-id="737cc-105">Scénario</span><span class="sxs-lookup"><span data-stu-id="737cc-105">Scenario</span></span>

<span data-ttu-id="737cc-106">Une société de Dublin fournit guichet unique pour mariage de destination haut de gamme en Irlande et autour Bonjour pour à la fois une base de client local et international.</span><span class="sxs-lookup"><span data-stu-id="737cc-106">A Dublin-based company provides one-stop shopping for high end destination weddings in Ireland and around hello world for both a local and international customer base.</span></span> <span data-ttu-id="737cc-107">Ils ont des bureaux, clients, employés et fournisseurs situés dans des lieux hello hello world toofully service qu’elles proposent.</span><span class="sxs-lookup"><span data-stu-id="737cc-107">They have offices, customers, employees, and vendors located around hello world toofully service hello venues they offer.</span></span>

<span data-ttu-id="737cc-108">Parmi les nombreux autres éléments, société de hello effectue le suivi de RSVP qui incluent des allergies alimentaires et préférences alimentaires.</span><span class="sxs-lookup"><span data-stu-id="737cc-108">Among many other items, hello company keeps track of RSVPs that include food allergies and dietary preferences.</span></span> <span data-ttu-id="737cc-109">Les invités mariage enregistrez pour diverses activités telles que horseback riding, de navigation, bateau trajets, etc. et même interagissent entre eux sur une page web central au cours des mois hello mènent toohello événement.</span><span class="sxs-lookup"><span data-stu-id="737cc-109">Wedding guests can register for various activities such as horseback riding, surfing, boat rides, etc., and even interact with one another on a central web page during hello months leading up toohello event.</span></span> <span data-ttu-id="737cc-110">société de Hello recueille des informations personnelles à partir des employés, les fournisseurs, les clients et les invités de mariage.</span><span class="sxs-lookup"><span data-stu-id="737cc-110">hello company collects personal information from employees, vendors, customers, and wedding guests.</span></span> <span data-ttu-id="737cc-111">En raison de hello nature internationale de hello hello société doit être conforme à plusieurs niveaux du règlement.</span><span class="sxs-lookup"><span data-stu-id="737cc-111">Because of hello international nature of hello business hello company must comply with multiple levels of regulation.</span></span>

## <a name="problem-statement"></a><span data-ttu-id="737cc-112">Définition du problème</span><span class="sxs-lookup"><span data-stu-id="737cc-112">Problem statement</span></span>

- <span data-ttu-id="737cc-113">Admins de données doit être toocorrect en mesure d’inexactes mise à jour et des informations incomplètes ou modifiées personnelles informations personnelles.</span><span class="sxs-lookup"><span data-stu-id="737cc-113">Data admins must be able toocorrect inaccurate personal information and update incomplete or changing personal information.</span></span>

- <span data-ttu-id="737cc-114">Nécessité d’administrateurs de données doit être en mesure de toodelete des informations personnelles à la demande de hello d’un objet de données.</span><span class="sxs-lookup"><span data-stu-id="737cc-114">Data admins need must be able toodelete personal information upon hello request of a data subject.</span></span>

- <span data-ttu-id="737cc-115">Admins de données besoin tooexport de données et fournir tooa concernée dans un format commun et structurée sur sa demande.</span><span class="sxs-lookup"><span data-stu-id="737cc-115">Data admins need tooexport data and provide it tooa data subject in a common, structured format upon his or her request.</span></span>

## <a name="company-goals"></a><span data-ttu-id="737cc-116">Objectifs de la société</span><span class="sxs-lookup"><span data-stu-id="737cc-116">Company goals</span></span>

- <span data-ttu-id="737cc-117">Les informations inexactes ou incomplètes sur les clients, les invités du mariage, les employés et les fournisseurs doivent être corrigées ou mises à jour dans Azure Active Directory et Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="737cc-117">Inaccurate or incomplete customer, wedding guest, employee, and vendor personal information must be corrected or updated in Azure Active Directory and Azure SQL Database.</span></span>

- <span data-ttu-id="737cc-118">Les informations personnelles doivent être supprimées dans Azure Active Directory et de la base de données SQL Azure à la demande de hello d’un objet de données.</span><span class="sxs-lookup"><span data-stu-id="737cc-118">Personal information must be deleted in Azure Active Directory and Azure SQL Database upon hello request of a data subject.</span></span>

- <span data-ttu-id="737cc-119">Les données personnelles doivent être exportées dans un format commun et structuré sur demande hello d’un objet de données.</span><span class="sxs-lookup"><span data-stu-id="737cc-119">Personal data must be exported in a common, structured format upon hello request of a data subject.</span></span>

## <a name="solutions"></a><span data-ttu-id="737cc-120">Solutions</span><span class="sxs-lookup"><span data-stu-id="737cc-120">Solutions</span></span>

### <a name="azure-active-directory-rectifycorrect-inaccurate-or-incomplete-personal-data-and-erasedelete-personal-datauser-profiles"></a><span data-ttu-id="737cc-121">Azure Active Directory : rectifier/corriger des données personnelles inexactes ou incomplètes et effacer/supprimer des données personnelles/profils utilisateur</span><span class="sxs-lookup"><span data-stu-id="737cc-121">Azure Active Directory: rectify/correct inaccurate or incomplete personal data and erase/delete personal data/user profiles</span></span>

<span data-ttu-id="737cc-122">[Azure Active Directory](https://azure.microsoft.com/services/active-directory/) est le service Microsoft de gestion d’annuaires et d’identités multilocataire basé sur le cloud.</span><span class="sxs-lookup"><span data-stu-id="737cc-122">[Azure Active Directory](https://azure.microsoft.com/services/active-directory/) is Microsoft’s cloud-based, multi-tenant directory and identity management service.</span></span>
<span data-ttu-id="737cc-123">Vous pouvez corriger, mettre à jour ou supprimer des profils utilisateur clients et des employés et les informations de travail utilisateur qui contiennent des données personnelles, telles que le nom, titre de travail, adresse ou numéro de téléphone d’un utilisateur dans votre [Azure Active Directory](https://azure.microsoft.com/services/active-directory/) (DAS) environnement à l’aide de hello [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="737cc-123">You can correct, update, or delete customer and employee user profiles and user work information that contain personal data, such as a user’s name, work title, address, or phone number, in your [Azure Active Directory](https://azure.microsoft.com/services/active-directory/) (AAD) environment by using hello [Azure portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="737cc-124">Vous devez vous connecter avec un compte qui est un administrateur global pour le répertoire de hello.</span><span class="sxs-lookup"><span data-stu-id="737cc-124">You must sign in with an account that’s a global admin for hello directory.</span></span>

#### <a name="how-do-i-correct-or-update-user-profile-and-work-information-in-azure-active-directory"></a><span data-ttu-id="737cc-125">Comment corriger ou mettre à jour des informations professionnelles et de profil utilisateur dans Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="737cc-125">How do I correct or update user profile and work information in Azure Active Directory?</span></span>

1. <span data-ttu-id="737cc-126">Connectez-vous à toohello [portail Azure](https://portal.azure.com) avec un compte qui est un administrateur global pour le répertoire de hello.</span><span class="sxs-lookup"><span data-stu-id="737cc-126">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>

2. <span data-ttu-id="737cc-127">Sélectionnez **davantage de services**, entrez **utilisateurs et groupes** dans hello de zone de texte, puis sélectionnez **entrée**.</span><span class="sxs-lookup"><span data-stu-id="737cc-127">Select **More services**, enter **Users and groups** in hello text box, and then select **Enter**.</span></span>

    ![media/image1.png](media/manage-personal-data-azure/image001.png)

3. <span data-ttu-id="737cc-129">Sur hello **utilisateurs et groupes** panneau, sélectionnez **utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="737cc-129">On hello **Users and groups** blade, select **Users**.</span></span>

    ![media/image2.png](media/manage-personal-data-azure/image003.png)

4. <span data-ttu-id="737cc-131">Sur hello **les utilisateurs et groupes d’utilisateurs -** panneau, sélectionnez un utilisateur à partir de la liste de hello, puis, dans Panneau de hello pour l’utilisateur sélectionné de hello, **profil** informations de profil tooview hello utilisateur nécessitant toobe corrigé ou mis à jour.</span><span class="sxs-lookup"><span data-stu-id="737cc-131">On hello **Users and groups - Users** blade, select a user from hello list, and then, on hello blade for hello selected user, select **Profile** tooview hello user profile information that needs toobe corrected or updated.</span></span>

    ![media/image3.png](media/manage-personal-data-azure/image005.png)

5. <span data-ttu-id="737cc-133">Corriger ou mettre à jour les informations de hello et, dans la barre de commandes hello, sélectionnez **enregistrer.**</span><span class="sxs-lookup"><span data-stu-id="737cc-133">Correct or update hello information, and then, in hello command bar, select **Save.**</span></span>

6.  <span data-ttu-id="737cc-134">Dans le panneau hello pour l’utilisateur sélectionné de hello, sélectionnez **Info de travail** tooview utilisateur travail informations dont a besoin toobe corrigée ou mis à jour.</span><span class="sxs-lookup"><span data-stu-id="737cc-134">On hello blade for hello selected user, select **Work Info** tooview user work information that needs toobe corrected or updated.</span></span>

    ![media/image4.png](media/manage-personal-data-azure/image007.png)

7. <span data-ttu-id="737cc-136">Corriger ou mettre à jour les informations de travail utilisateur hello et, dans la barre de commandes hello, sélectionnez **enregistrer.**</span><span class="sxs-lookup"><span data-stu-id="737cc-136">Correct or update hello user work information, and then, in hello command bar, select **Save.**</span></span>

#### <a name="how-do-i-delete-a-user-profile-in-azure-active-directory"></a><span data-ttu-id="737cc-137">Comment supprimer un profil utilisateur dans Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="737cc-137">How do I delete a user profile in Azure Active Directory?</span></span>

1. <span data-ttu-id="737cc-138">Connectez-vous à toohello [portail Azure](https://portal.azure.com) avec un compte qui est un administrateur global pour le répertoire de hello.</span><span class="sxs-lookup"><span data-stu-id="737cc-138">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>

2. <span data-ttu-id="737cc-139">Sélectionnez **davantage de services**, entrez **utilisateurs et groupes** dans hello de zone de texte, puis sélectionnez **entrée**.</span><span class="sxs-lookup"><span data-stu-id="737cc-139">Select **More services**, enter **Users and groups** in hello text box, and then select **Enter**.</span></span>

    ![](media/manage-personal-data-azure/image001.png)

3. <span data-ttu-id="737cc-140">Sur hello **utilisateurs et groupes** panneau, sélectionnez **utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="737cc-140">On hello **Users and groups** blade, select **Users**.</span></span>

    ![media/image2.png](media/manage-personal-data-azure/image003.png)

4. <span data-ttu-id="737cc-142">Sur hello **les utilisateurs et groupes d’utilisateurs -** panneau, sélectionnez un utilisateur à partir de la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="737cc-142">On hello **Users and groups - Users** blade, select a user from hello list.</span></span>

    ![media/image3.png](media/manage-personal-data-azure/image007.png)

5. <span data-ttu-id="737cc-144">Dans le panneau hello pour l’utilisateur sélectionné de hello, sélectionnez **vue d’ensemble**, puis, dans la barre de commandes hello, sélectionnez **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="737cc-144">On hello blade for hello selected user, select **Overview**, and then in hello command bar, select **Delete**.</span></span>

    ![](media/manage-personal-data-azure/image013.png)

### <a name="sql-database-rectifycorrect-inaccurate-or-incomplete-personal-data-erasedelete-personal-data-export-personal-data"></a><span data-ttu-id="737cc-145">SQL Database : rectifier/corriger des données personnelles inexactes ou incomplètes ; effacer/supprimer des données personnelles ; exporter des données personnelles</span><span class="sxs-lookup"><span data-stu-id="737cc-145">SQL Database: rectify/correct inaccurate or incomplete personal data; erase/delete personal data; export personal data</span></span> 

<span data-ttu-id="737cc-146">[Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) est une base de données cloud qui permet aux développeurs de créer et tenir à jour des applications.</span><span class="sxs-lookup"><span data-stu-id="737cc-146">[Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) is a cloud database that helps developers build and maintain applications.</span></span>

<span data-ttu-id="737cc-147">Les données personnelles peuvent être mises à jour dans [Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) à l’aide de requêtes SQL standard et peuvent aussi être supprimées.</span><span class="sxs-lookup"><span data-stu-id="737cc-147">Personal data can be updated in [Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) using standard SQL queries, and it can also be deleted.</span></span> <span data-ttu-id="737cc-148">En outre, les données personnelles peuvent être exportées à partir de la base de données SQL à l’aide de plusieurs méthodes, y compris hello import Azure SQL Server et l’Assistant Exportation et dans divers formats, y compris un fichier BACPAC.</span><span class="sxs-lookup"><span data-stu-id="737cc-148">Additionally, personal data can be exported from SQL Database using a variety of methods, including hello Azure SQL Server import and export wizard, and in a variety of formats, including a BACPAC file.</span></span>

#### <a name="how-do-i-correct-update-or-erase-personal-data-in-sql-database"></a><span data-ttu-id="737cc-149">Comment corriger, mettre à jour ou supprimer des données personnelles dans SQL Database ?</span><span class="sxs-lookup"><span data-stu-id="737cc-149">How do I correct, update, or erase personal data in SQL Database?</span></span>

<span data-ttu-id="737cc-150">toolearn comment toocorrect ou mise à jour des données personnelles dans la base de données SQL, visitez hello [mise à jour (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/queries/update-transact-sql), [mettre à jour le texte](https://docs.microsoft.com/sql/t-sql/queries/updatetext-transact-sql), [mettre à jour avec l’Expression de Table commune](https://docs.microsoft.com/sql/t-sql/queries/with-common-table-expression-transact-sql), ou [ Mettre à jour écrire le texte](https://docs.microsoft.com/sql/t-sql/queries/writetext-transact-sql) documentation.</span><span class="sxs-lookup"><span data-stu-id="737cc-150">toolearn how toocorrect or update personal data in SQL Database, visit hello [Update (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/queries/update-transact-sql), [Update Text](https://docs.microsoft.com/sql/t-sql/queries/updatetext-transact-sql), [Update with Common Table Expression](https://docs.microsoft.com/sql/t-sql/queries/with-common-table-expression-transact-sql), or [Update Write Text](https://docs.microsoft.com/sql/t-sql/queries/writetext-transact-sql) documentation.</span></span>

<span data-ttu-id="737cc-151">toolearn comment toodelete des données personnelles dans la base de données SQL, visitez hello [supprimer (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/delete-transact-sql) documentation.</span><span class="sxs-lookup"><span data-stu-id="737cc-151">toolearn how toodelete personal data in SQL Database, visit hello [Delete (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/delete-transact-sql) documentation.</span></span>

#### <a name="how-do-i-export-personal-data-tooa-bacpac-file-in-sql-database"></a><span data-ttu-id="737cc-152">Comment exporter le fichier BACPAC tooa de données personnelles dans la base de données SQL ?</span><span class="sxs-lookup"><span data-stu-id="737cc-152">How do I export personal data tooa BACPAC file in SQL Database?</span></span>

<span data-ttu-id="737cc-153">Un fichier BACPAC inclut les métadonnées et les données de base de données SQL hello et est un fichier zip avec une extension de fichier BACPAC.</span><span class="sxs-lookup"><span data-stu-id="737cc-153">A BACPAC file includes hello SQL Database data and metadata and is a zip file with a BACPAC extension.</span></span> <span data-ttu-id="737cc-154">Cela est possible à l’aide de hello [portail Azure](https://portal.azure.com/), hello SQLPackage utilitaire de ligne de commande, SQL Server Management Studio (SSMS) ou PowerShell.</span><span class="sxs-lookup"><span data-stu-id="737cc-154">This can be done using hello [Azure portal](https://portal.azure.com/), hello SQLPackage command-line utility, SQL Server Management Studio (SSMS), or PowerShell.</span></span>

<span data-ttu-id="737cc-155">toolearn comment tooexport tooa BACPAC fichier, visitez hello [exporter un fichier BACPAC de tooa de base de données SQL Azure](https://docs.microsoft.com/azure/sql-database/sql-database-export) page, ce qui inclut des instructions détaillées pour chaque méthode répertoriés ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="737cc-155">toolearn how tooexport data tooa BACPAC file, visit hello [Export an Azure SQL database tooa BACPAC file](https://docs.microsoft.com/azure/sql-database/sql-database-export) page, which includes detailed instructions for each method listed above.</span></span>

<span data-ttu-id="737cc-156">Comment exporter des données personnelles à partir de la base de données SQL hello SQL Server Import et l’Assistant Exportation ?</span><span class="sxs-lookup"><span data-stu-id="737cc-156">How do I export personal data from SQL Database with hello SQL Server Import and Export Wizard?</span></span>

<span data-ttu-id="737cc-157">Cet Assistant vous permet de copier des données à partir d’une source de destination tooa.</span><span class="sxs-lookup"><span data-stu-id="737cc-157">This wizard helps you copy data from a source tooa destination.</span></span> <span data-ttu-id="737cc-158">Pour un Assistant toohello introduction, y compris comment tooget, informations sur les autorisations et comment aider à tooget avec l’outil de hello, visitez hello [et exporter des données avec SQL Server Import de hello Assistant Importation et exportation](https://docs.microsoft.com/sql/integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard) page web.</span><span class="sxs-lookup"><span data-stu-id="737cc-158">For an introduction toohello wizard, including how tooget it, permissions information, and how tooget help with hello tool, visit hello [Import and Export Data with hello SQL Server Import and Export Wizard](https://docs.microsoft.com/sql/integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard) web page.</span></span>

<span data-ttu-id="737cc-159">Pour une vue d’ensemble des étapes de l’Assistant de hello, visitez hello [étapes hello SQL Server Import et Assistant Exportation](https://docs.microsoft.com/sql/integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard) page web.</span><span class="sxs-lookup"><span data-stu-id="737cc-159">For an overview of steps for hello wizard, visit hello [Steps in hello SQL Server Import and Export Wizard](https://docs.microsoft.com/sql/integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard) web page.</span></span>

## <a name="next-steps"></a><span data-ttu-id="737cc-160">Étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="737cc-160">Next Steps:</span></span>

[<span data-ttu-id="737cc-161">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="737cc-161">Azure SQL Database</span></span>](https://azure.microsoft.com/services/sql-database/?v=16.50) 

[<span data-ttu-id="737cc-162">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="737cc-162">Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

