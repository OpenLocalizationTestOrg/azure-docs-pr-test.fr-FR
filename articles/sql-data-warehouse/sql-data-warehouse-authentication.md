---
title: "Authentification sur Azure SQL Data Warehouse | Microsoft Docs"
description: Authentification Azure Active Directory (AAD) et SQL Server sur Azure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
tags: 
ms.assetid: fefaaa75-2d0c-4e5d-aadb-410342d1ad73
ms.service: sql-data-warehouse
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.custom: security
ms.date: 03/21/2017
ms.author: rortloff;barbkess
ms.openlocfilehash: 92f48027051bc4aff4d6b8d66fdd6de81bba3657
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="authentication-to-azure-sql-data-warehouse"></a><span data-ttu-id="d9683-103">Authentification sur Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="d9683-103">Authentication to Azure SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d9683-104">Présentation de la sécurité</span><span class="sxs-lookup"><span data-stu-id="d9683-104">Security Overview</span></span>](sql-data-warehouse-overview-manage-security.md)
> * [<span data-ttu-id="d9683-105">Authentification</span><span class="sxs-lookup"><span data-stu-id="d9683-105">Authentication</span></span>](sql-data-warehouse-authentication.md)
> * [<span data-ttu-id="d9683-106">Chiffrement (portail)</span><span class="sxs-lookup"><span data-stu-id="d9683-106">Encryption (Portal)</span></span>](sql-data-warehouse-encryption-tde.md)
> * [<span data-ttu-id="d9683-107">Chiffrement (T-SQL)</span><span class="sxs-lookup"><span data-stu-id="d9683-107">Encryption (T-SQL)</span></span>](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

<span data-ttu-id="d9683-108">Pour vous connecter à SQL Data Warehouse, vous devez transmettre des informations d’identification de sécurité à des fins d’authentification.</span><span class="sxs-lookup"><span data-stu-id="d9683-108">To connect to SQL Data Warehouse, you must pass in security credentials for authentication purposes.</span></span> <span data-ttu-id="d9683-109">Lors de l’établissement d’une connexion, certains paramètres de connexion sont configurés dans le cadre de l’établissement de votre session de requête.</span><span class="sxs-lookup"><span data-stu-id="d9683-109">Upon establishing a connection, certain connection settings are configured as part of establishing your query session.</span></span>  

<span data-ttu-id="d9683-110">Vous pouvez consulter l’article [Sécuriser une base de données dans SQL Data Warehouse][Secure a database in SQL Data Warehouse] pour plus d’informations sur la sécurité et la manière d’activer des connexions à votre entrepôt de données.</span><span class="sxs-lookup"><span data-stu-id="d9683-110">For more information on security and how to enable connections to your data warehouse, see [Secure a database in SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span></span>

## <a name="sql-authentication"></a><span data-ttu-id="d9683-111">Authentification SQL</span><span class="sxs-lookup"><span data-stu-id="d9683-111">SQL authentication</span></span>
<span data-ttu-id="d9683-112">Pour vous connecter à SQL Data Warehouse, vous devez fournir les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="d9683-112">To connect to SQL Data Warehouse, you must provide the following information:</span></span>

* <span data-ttu-id="d9683-113">Nom complet du serveur</span><span class="sxs-lookup"><span data-stu-id="d9683-113">Fully qualified servername</span></span>
* <span data-ttu-id="d9683-114">Authentification SQL</span><span class="sxs-lookup"><span data-stu-id="d9683-114">Specify SQL authentication</span></span>
* <span data-ttu-id="d9683-115">Nom d’utilisateur</span><span class="sxs-lookup"><span data-stu-id="d9683-115">Username</span></span>
* <span data-ttu-id="d9683-116">Mot de passe</span><span class="sxs-lookup"><span data-stu-id="d9683-116">Password</span></span>
* <span data-ttu-id="d9683-117">Base de données par défaut (facultatif)</span><span class="sxs-lookup"><span data-stu-id="d9683-117">Default database (optional)</span></span>

<span data-ttu-id="d9683-118">Par défaut, votre connexion se connecte à la base de données *MASTER* et non à votre base de données utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d9683-118">By default your connection connects to the *master* database and not your user database.</span></span> <span data-ttu-id="d9683-119">Pour vous connecter à votre base de données utilisateur, vous pouvez choisir d’effectuer l’une des deux opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="d9683-119">To connect to your user database, you can choose to do one of two things:</span></span>

* <span data-ttu-id="d9683-120">Spécifiez la base de données par défaut lors de l’inscription de votre serveur auprès de l’Explorateur d’objets SQL Server dans SQL Server Data Tools (SSDT), SSMS, ou dans votre chaîne de connexion d’application.</span><span class="sxs-lookup"><span data-stu-id="d9683-120">Specify the default database when registering your server with the SQL Server Object Explorer in SSDT, SSMS, or in your application connection string.</span></span> <span data-ttu-id="d9683-121">Par exemple, insérez le paramètre InitialCatalog pour une connexion ODBC.</span><span class="sxs-lookup"><span data-stu-id="d9683-121">For example, include the InitialCatalog parameter for an ODBC connection.</span></span>
* <span data-ttu-id="d9683-122">Sélectionnez la base de données utilisateur avant de créer une session dans SSDT.</span><span class="sxs-lookup"><span data-stu-id="d9683-122">Highlight the user database before creating a session in SSDT.</span></span>

> [!NOTE]
> <span data-ttu-id="d9683-123">L’instruction Transact-SQL **USE MyDatabase;** n’est pas prise en charge pour la modification de la base de données pour une connexion.</span><span class="sxs-lookup"><span data-stu-id="d9683-123">The Transact-SQL statement **USE MyDatabase;** is not supported for changing the database for a connection.</span></span> <span data-ttu-id="d9683-124">Pour obtenir des conseils en matière de connexion à SQL Data Warehouse avec SSDT, consultez l’article [Envoyer des requêtes avec Visual Studio][Query with Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="d9683-124">For guidance connecting to SQL Data Warehouse with SSDT, refer to the [Query with Visual Studio][Query with Visual Studio] article.</span></span>
> 
> 

## <a name="azure-active-directory-aad-authentication"></a><span data-ttu-id="d9683-125">Authentification Azure Active Directory (AAD)</span><span class="sxs-lookup"><span data-stu-id="d9683-125">Azure Active Directory (AAD) authentication</span></span>
<span data-ttu-id="d9683-126">L’[authentification Azure Active Directory][What is Azure Active Directory] est un mécanisme servant à se connecter à Microsoft Azure SQL Data Warehouse à l’aide d’identités dans Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d9683-126">[Azure Active Directory][What is Azure Active Directory] authentication is a mechanism of connecting to Microsoft Azure SQL Data Warehouse by using identities in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="d9683-127">Avec l’authentification Azure Active Directory, vous pouvez gérer de manière centralisée les identités des utilisateurs de base de données et d’autres services Microsoft dans un emplacement centralisé.</span><span class="sxs-lookup"><span data-stu-id="d9683-127">With Azure Active Directory authentication, you can centrally manage the identities of database users and other Microsoft services in one central location.</span></span> <span data-ttu-id="d9683-128">La gestion centralisée des ID fournit un emplacement unique pour gérer les utilisateurs SQL Data Warehouse et elle simplifie la gestion des autorisations.</span><span class="sxs-lookup"><span data-stu-id="d9683-128">Central ID management provides a single place to manage SQL Data Warehouse users and simplifies permission management.</span></span> 

### <a name="benefits"></a><span data-ttu-id="d9683-129">Avantages</span><span class="sxs-lookup"><span data-stu-id="d9683-129">Benefits</span></span>
<span data-ttu-id="d9683-130">Les avantages d’Azure Active Directory incluent :</span><span class="sxs-lookup"><span data-stu-id="d9683-130">Azure Active Directory benefits include:</span></span>

* <span data-ttu-id="d9683-131">Fournit une alternative à l’authentification SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d9683-131">Provides an alternative to SQL Server authentication.</span></span>
* <span data-ttu-id="d9683-132">Permet de bloquer la prolifération des identités utilisateur sur plusieurs serveurs de base de données.</span><span class="sxs-lookup"><span data-stu-id="d9683-132">Helps stop the proliferation of user identities across database servers.</span></span>
* <span data-ttu-id="d9683-133">Permet la rotation de mot de passe à un emplacement unique</span><span class="sxs-lookup"><span data-stu-id="d9683-133">Allows password rotation in a single place</span></span>
* <span data-ttu-id="d9683-134">Gérer les autorisations de base de données à l’aide de groupes (AAD) externes.</span><span class="sxs-lookup"><span data-stu-id="d9683-134">Manage database permissions using external (AAD) groups.</span></span>
* <span data-ttu-id="d9683-135">Élimine le stockage des mots de passe en activant l’authentification intégrée Windows et les autres formes d’authentification prises en charge par Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d9683-135">Eliminates storing passwords by enabling integrated Windows authentication and other forms of authentication supported by Azure Active Directory.</span></span>
* <span data-ttu-id="d9683-136">Utilise les utilisateurs de base de données à relation contenant-contenu pour authentifier les identités au niveau de la base de données.</span><span class="sxs-lookup"><span data-stu-id="d9683-136">Uses contained database users to authenticate identities at the database level.</span></span>
* <span data-ttu-id="d9683-137">Prend en charge l’authentification basée sur les jetons pour les applications se connectant à SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="d9683-137">Supports token-based authentication for applications connecting to SQL Data Warehouse.</span></span>
* <span data-ttu-id="d9683-138">Prend en charge Multi-Factor Authentication avec l’authentification universelle Active Directory pour SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="d9683-138">Supports Multi-Factor authentication through Active Directory Universal Authentication for SQL Server Management Studio.</span></span> <span data-ttu-id="d9683-139">Pour obtenir une description de Multi-Factor Authentication, consultez [Prise en charge SSMS de Azure AD MFA avec la base de données SQL et SQL Data Warehouse](../sql-database/sql-database-ssms-mfa-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="d9683-139">For a description of Multi-Factor Authentication, see [SSMS support for Azure AD MFA with SQL Database and SQL Data Warehouse](../sql-database/sql-database-ssms-mfa-authentication.md).</span></span>

> [!NOTE]
> <span data-ttu-id="d9683-140">Azure Active Directory est encore relativement nouveau et présente certaines limitations.</span><span class="sxs-lookup"><span data-stu-id="d9683-140">Azure Active Directory is still relatively new and has some limitations.</span></span> <span data-ttu-id="d9683-141">Pour vérifier qu’Azure Active Directory est adapté à votre environnement, consultez [Limitations et fonctionnalités Azure AD][Azure AD features and limitations], en particulier la section Considérations supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="d9683-141">To ensure that Azure Active Directory is a good fit for your environment, see [Azure AD features and limitations][Azure AD features and limitations], specifically the Additional considerations.</span></span>
> 
> 

### <a name="configuration-steps"></a><span data-ttu-id="d9683-142">Configuration</span><span class="sxs-lookup"><span data-stu-id="d9683-142">Configuration steps</span></span>
<span data-ttu-id="d9683-143">Suivez ces étapes pour configurer l’authentification Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d9683-143">Follow these steps to configure Azure Active Directory authentication.</span></span>

1. <span data-ttu-id="d9683-144">Créer et renseigner un répertoire Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d9683-144">Create and populate an Azure Active Directory</span></span>
2. <span data-ttu-id="d9683-145">Facultatif : associer ou modifier le répertoire actif actuellement associé à votre abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="d9683-145">Optional: Associate or change the active directory that is currently associated with your Azure Subscription</span></span>
3. <span data-ttu-id="d9683-146">Créer un administrateur Azure Active Directory pour Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="d9683-146">Create an Azure Active Directory administrator for Azure SQL Data Warehouse.</span></span>
4. <span data-ttu-id="d9683-147">Configurer vos ordinateurs clients</span><span class="sxs-lookup"><span data-stu-id="d9683-147">Configure your client computers</span></span>
5. <span data-ttu-id="d9683-148">Créer des utilisateurs de base de données à relation contenant-contenu dans votre base de données mappés sur les identités Azure AD</span><span class="sxs-lookup"><span data-stu-id="d9683-148">Create contained database users in your database mapped to Azure AD identities</span></span>
6. <span data-ttu-id="d9683-149">Se connecter à l’entrepôt de données à l’aide des identités Azure AD</span><span class="sxs-lookup"><span data-stu-id="d9683-149">Connect to your data warehouse by using Azure AD identities</span></span>

<span data-ttu-id="d9683-150">Actuellement, les utilisateurs Azure Active Directory ne sont pas affichés dans l’Explorateur d’objets SSDT.</span><span class="sxs-lookup"><span data-stu-id="d9683-150">Currently Azure Active Directory users are not shown in SSDT Object Explorer.</span></span> <span data-ttu-id="d9683-151">Comme solution de contournement, vous pouvez afficher les utilisateurs dans [sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx).</span><span class="sxs-lookup"><span data-stu-id="d9683-151">As a workaround, view the users in [sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx).</span></span>

### <a name="find-the-details"></a><span data-ttu-id="d9683-152">Rechercher des informations détaillées</span><span class="sxs-lookup"><span data-stu-id="d9683-152">Find the details</span></span>
* <span data-ttu-id="d9683-153">Les étapes de configuration et d’utilisation de l’authentification Azure Active Directory sont presque identiques pour Azure SQL Database et Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="d9683-153">The steps to configure and use Azure Active Directory authentication are nearly identical for Azure SQL Database and Azure SQL Data Warehouse.</span></span> <span data-ttu-id="d9683-154">Suivez les étapes détaillées dans la rubrique [Connexion à SQL Database ou SQL Data Warehouse avec l’authentification Azure Active Directory](../sql-database/sql-database-aad-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="d9683-154">Follow the detailed steps in the topic [Connecting to SQL Database or SQL Data Warehouse By Using Azure Active Directory Authentication](../sql-database/sql-database-aad-authentication.md).</span></span>
* <span data-ttu-id="d9683-155">Créez des rôles de base de données personnalisés et ajoutez des utilisateurs aux rôles.</span><span class="sxs-lookup"><span data-stu-id="d9683-155">Create custom database roles and add users to the roles.</span></span> <span data-ttu-id="d9683-156">Accordez ensuite des autorisations granulaires aux rôles.</span><span class="sxs-lookup"><span data-stu-id="d9683-156">Then grant granular permissions to the roles.</span></span> <span data-ttu-id="d9683-157">Pour plus d’informations, consultez [Prise en main des autorisations du moteur de base de données](https://msdn.microsoft.com/library/mt667986.aspx).</span><span class="sxs-lookup"><span data-stu-id="d9683-157">For more information, see [Getting Started with Database Engine Permissions](https://msdn.microsoft.com/library/mt667986.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d9683-158">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d9683-158">Next steps</span></span>
<span data-ttu-id="d9683-159">Pour commencer à interroger votre entrepôt de données avec Visual Studio et d’autres applications, consultez [Soumettre des requêtes avec Visual Studio][Query with Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="d9683-159">To start querying your data warehouse with Visual Studio and other applications, see [Query with Visual Studio][Query with Visual Studio].</span></span>

<!-- Article references -->
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md
[Query with Visual Studio]: ./sql-data-warehouse-query-visual-studio.md
[What is Azure Active Directory]: ../active-directory/active-directory-whatis.md
[Azure AD features and limitations]: ../sql-database/sql-database-aad-authentication.md#azure-ad-features-and-limitations
