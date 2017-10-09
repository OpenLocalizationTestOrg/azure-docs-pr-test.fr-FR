---
title: aaaAuthentication tooAzure SQL Data Warehouse | Documents Microsoft
description: Azure Active Directory (AAD) et SQL Server authentication tooAzure SQL Data Warehouse.
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
ms.openlocfilehash: 66673ce1d4761243755254c8f64de1078a0ea82e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-tooazure-sql-data-warehouse"></a><span data-ttu-id="606bb-103">Authentification tooAzure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="606bb-103">Authentication tooAzure SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="606bb-104">Présentation de la sécurité</span><span class="sxs-lookup"><span data-stu-id="606bb-104">Security Overview</span></span>](sql-data-warehouse-overview-manage-security.md)
> * [<span data-ttu-id="606bb-105">Authentification</span><span class="sxs-lookup"><span data-stu-id="606bb-105">Authentication</span></span>](sql-data-warehouse-authentication.md)
> * [<span data-ttu-id="606bb-106">Chiffrement (portail)</span><span class="sxs-lookup"><span data-stu-id="606bb-106">Encryption (Portal)</span></span>](sql-data-warehouse-encryption-tde.md)
> * [<span data-ttu-id="606bb-107">Chiffrement (T-SQL)</span><span class="sxs-lookup"><span data-stu-id="606bb-107">Encryption (T-SQL)</span></span>](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

<span data-ttu-id="606bb-108">tooconnect tooSQL l’entrepôt de données, vous devez passer les informations d’identification de sécurité à des fins d’authentification.</span><span class="sxs-lookup"><span data-stu-id="606bb-108">tooconnect tooSQL Data Warehouse, you must pass in security credentials for authentication purposes.</span></span> <span data-ttu-id="606bb-109">Lors de l’établissement d’une connexion, certains paramètres de connexion sont configurés dans le cadre de l’établissement de votre session de requête.</span><span class="sxs-lookup"><span data-stu-id="606bb-109">Upon establishing a connection, certain connection settings are configured as part of establishing your query session.</span></span>  

<span data-ttu-id="606bb-110">Pour plus d’informations sur la sécurité et la manière dont entrepôt de données tooyour tooenable connexions, consultez [sécuriser une base de données SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="606bb-110">For more information on security and how tooenable connections tooyour data warehouse, see [Secure a database in SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span></span>

## <a name="sql-authentication"></a><span data-ttu-id="606bb-111">Authentification SQL</span><span class="sxs-lookup"><span data-stu-id="606bb-111">SQL authentication</span></span>
<span data-ttu-id="606bb-112">tooconnect tooSQL l’entrepôt de données, vous devez fournir hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="606bb-112">tooconnect tooSQL Data Warehouse, you must provide hello following information:</span></span>

* <span data-ttu-id="606bb-113">Nom complet du serveur</span><span class="sxs-lookup"><span data-stu-id="606bb-113">Fully qualified servername</span></span>
* <span data-ttu-id="606bb-114">Authentification SQL</span><span class="sxs-lookup"><span data-stu-id="606bb-114">Specify SQL authentication</span></span>
* <span data-ttu-id="606bb-115">Nom d’utilisateur</span><span class="sxs-lookup"><span data-stu-id="606bb-115">Username</span></span>
* <span data-ttu-id="606bb-116">Mot de passe</span><span class="sxs-lookup"><span data-stu-id="606bb-116">Password</span></span>
* <span data-ttu-id="606bb-117">Base de données par défaut (facultatif)</span><span class="sxs-lookup"><span data-stu-id="606bb-117">Default database (optional)</span></span>

<span data-ttu-id="606bb-118">Par défaut, la connexion connecte toohello *master* pas votre base de données utilisateur et de base de données.</span><span class="sxs-lookup"><span data-stu-id="606bb-118">By default your connection connects toohello *master* database and not your user database.</span></span> <span data-ttu-id="606bb-119">base de données tooconnect tooyour utilisateur, vous pouvez choisir toodo deux choses :</span><span class="sxs-lookup"><span data-stu-id="606bb-119">tooconnect tooyour user database, you can choose toodo one of two things:</span></span>

* <span data-ttu-id="606bb-120">Spécifiez la base de données par défaut hello lors de l’inscription de votre serveur avec l’Explorateur d’objets SQL Server dans SSDT, SSMS, ou dans votre chaîne de connexion d’application de hello.</span><span class="sxs-lookup"><span data-stu-id="606bb-120">Specify hello default database when registering your server with hello SQL Server Object Explorer in SSDT, SSMS, or in your application connection string.</span></span> <span data-ttu-id="606bb-121">Par exemple, inclure le paramètre de InitialCatalog hello pour une connexion ODBC.</span><span class="sxs-lookup"><span data-stu-id="606bb-121">For example, include hello InitialCatalog parameter for an ODBC connection.</span></span>
* <span data-ttu-id="606bb-122">Mettez en surbrillance la base de données utilisateur hello avant de créer une session dans SSDT.</span><span class="sxs-lookup"><span data-stu-id="606bb-122">Highlight hello user database before creating a session in SSDT.</span></span>

> [!NOTE]
> <span data-ttu-id="606bb-123">instruction Transact-SQL de Hello **utilisez MyDatabase ;** n’est pas prise en charge pour la modification de la base de données hello pour une connexion.</span><span class="sxs-lookup"><span data-stu-id="606bb-123">hello Transact-SQL statement **USE MyDatabase;** is not supported for changing hello database for a connection.</span></span> <span data-ttu-id="606bb-124">Pour obtenir des conseils connexion tooSQL l’entrepôt de données avec SSDT, consultez toohello [requête avec Visual Studio] [ Query with Visual Studio] l’article.</span><span class="sxs-lookup"><span data-stu-id="606bb-124">For guidance connecting tooSQL Data Warehouse with SSDT, refer toohello [Query with Visual Studio][Query with Visual Studio] article.</span></span>
> 
> 

## <a name="azure-active-directory-aad-authentication"></a><span data-ttu-id="606bb-125">Authentification Azure Active Directory (AAD)</span><span class="sxs-lookup"><span data-stu-id="606bb-125">Azure Active Directory (AAD) authentication</span></span>
<span data-ttu-id="606bb-126">[Azure Active Directory] [ What is Azure Active Directory] l’authentification est un mécanisme de connexion tooMicrosoft Azure SQL Data Warehouse à l’aide des identités dans Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="606bb-126">[Azure Active Directory][What is Azure Active Directory] authentication is a mechanism of connecting tooMicrosoft Azure SQL Data Warehouse by using identities in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="606bb-127">Avec l’authentification Azure Active Directory, vous pouvez gérer de manière centralisée les identités hello d’utilisateurs de base de données et d’autres services de Microsoft dans un emplacement central.</span><span class="sxs-lookup"><span data-stu-id="606bb-127">With Azure Active Directory authentication, you can centrally manage hello identities of database users and other Microsoft services in one central location.</span></span> <span data-ttu-id="606bb-128">Gestion des ID fournit un emplacement unique aux utilisateurs de SQL Data Warehouse toomanage et simplifie la gestion de l’autorisation.</span><span class="sxs-lookup"><span data-stu-id="606bb-128">Central ID management provides a single place toomanage SQL Data Warehouse users and simplifies permission management.</span></span> 

### <a name="benefits"></a><span data-ttu-id="606bb-129">Avantages</span><span class="sxs-lookup"><span data-stu-id="606bb-129">Benefits</span></span>
<span data-ttu-id="606bb-130">Les avantages d’Azure Active Directory incluent :</span><span class="sxs-lookup"><span data-stu-id="606bb-130">Azure Active Directory benefits include:</span></span>

* <span data-ttu-id="606bb-131">Fournit une authentification de serveur alternatif tooSQL.</span><span class="sxs-lookup"><span data-stu-id="606bb-131">Provides an alternative tooSQL Server authentication.</span></span>
* <span data-ttu-id="606bb-132">Vous aide à arrêter la prolifération hello des identités des utilisateurs sur les serveurs de base de données.</span><span class="sxs-lookup"><span data-stu-id="606bb-132">Helps stop hello proliferation of user identities across database servers.</span></span>
* <span data-ttu-id="606bb-133">Permet la rotation de mot de passe à un emplacement unique</span><span class="sxs-lookup"><span data-stu-id="606bb-133">Allows password rotation in a single place</span></span>
* <span data-ttu-id="606bb-134">Gérer les autorisations de base de données à l’aide de groupes (AAD) externes.</span><span class="sxs-lookup"><span data-stu-id="606bb-134">Manage database permissions using external (AAD) groups.</span></span>
* <span data-ttu-id="606bb-135">Élimine le stockage des mots de passe en activant l’authentification intégrée Windows et les autres formes d’authentification prises en charge par Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="606bb-135">Eliminates storing passwords by enabling integrated Windows authentication and other forms of authentication supported by Azure Active Directory.</span></span>
* <span data-ttu-id="606bb-136">Base de données utilise contenus utilisateurs tooauthenticate des identités au niveau de base de données hello.</span><span class="sxs-lookup"><span data-stu-id="606bb-136">Uses contained database users tooauthenticate identities at hello database level.</span></span>
* <span data-ttu-id="606bb-137">Prend en charge l’authentification basée sur le jeton pour les applications qui se connectent tooSQL l’entrepôt de données.</span><span class="sxs-lookup"><span data-stu-id="606bb-137">Supports token-based authentication for applications connecting tooSQL Data Warehouse.</span></span>
* <span data-ttu-id="606bb-138">Prend en charge Multi-Factor Authentication avec l’authentification universelle Active Directory pour SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="606bb-138">Supports Multi-Factor authentication through Active Directory Universal Authentication for SQL Server Management Studio.</span></span> <span data-ttu-id="606bb-139">Pour obtenir une description de Multi-Factor Authentication, consultez [Prise en charge SSMS de Azure AD MFA avec la base de données SQL et SQL Data Warehouse](../sql-database/sql-database-ssms-mfa-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="606bb-139">For a description of Multi-Factor Authentication, see [SSMS support for Azure AD MFA with SQL Database and SQL Data Warehouse](../sql-database/sql-database-ssms-mfa-authentication.md).</span></span>

> [!NOTE]
> <span data-ttu-id="606bb-140">Azure Active Directory est encore relativement nouveau et présente certaines limitations.</span><span class="sxs-lookup"><span data-stu-id="606bb-140">Azure Active Directory is still relatively new and has some limitations.</span></span> <span data-ttu-id="606bb-141">tooensure qu’Azure Active Directory est adapté à votre environnement, consultez [les fonctionnalités Azure AD et limitations][Azure AD features and limitations], plus précisément hello considérations supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="606bb-141">tooensure that Azure Active Directory is a good fit for your environment, see [Azure AD features and limitations][Azure AD features and limitations], specifically hello Additional considerations.</span></span>
> 
> 

### <a name="configuration-steps"></a><span data-ttu-id="606bb-142">Configuration</span><span class="sxs-lookup"><span data-stu-id="606bb-142">Configuration steps</span></span>
<span data-ttu-id="606bb-143">Suivez ces étapes tooconfigure Active d’authentification Azure Directory.</span><span class="sxs-lookup"><span data-stu-id="606bb-143">Follow these steps tooconfigure Azure Active Directory authentication.</span></span>

1. <span data-ttu-id="606bb-144">Créer et renseigner un répertoire Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="606bb-144">Create and populate an Azure Active Directory</span></span>
2. <span data-ttu-id="606bb-145">Associer facultatif : Ou modifier hello active directory qui est associé à votre abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="606bb-145">Optional: Associate or change hello active directory that is currently associated with your Azure Subscription</span></span>
3. <span data-ttu-id="606bb-146">Créer un administrateur Azure Active Directory pour Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="606bb-146">Create an Azure Active Directory administrator for Azure SQL Data Warehouse.</span></span>
4. <span data-ttu-id="606bb-147">Configurer vos ordinateurs clients</span><span class="sxs-lookup"><span data-stu-id="606bb-147">Configure your client computers</span></span>
5. <span data-ttu-id="606bb-148">Créer des utilisateurs de base de données dans votre base de données mappée de tooAzure identités AD</span><span class="sxs-lookup"><span data-stu-id="606bb-148">Create contained database users in your database mapped tooAzure AD identities</span></span>
6. <span data-ttu-id="606bb-149">Se connecter tooyour l’entrepôt de données à l’aide d’identités Azure AD</span><span class="sxs-lookup"><span data-stu-id="606bb-149">Connect tooyour data warehouse by using Azure AD identities</span></span>

<span data-ttu-id="606bb-150">Actuellement, les utilisateurs Azure Active Directory ne sont pas affichés dans l’Explorateur d’objets SSDT.</span><span class="sxs-lookup"><span data-stu-id="606bb-150">Currently Azure Active Directory users are not shown in SSDT Object Explorer.</span></span> <span data-ttu-id="606bb-151">Pour résoudre ce problème, afficher les utilisateurs de hello dans [sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx).</span><span class="sxs-lookup"><span data-stu-id="606bb-151">As a workaround, view hello users in [sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx).</span></span>

### <a name="find-hello-details"></a><span data-ttu-id="606bb-152">Rechercher des détails de hello</span><span class="sxs-lookup"><span data-stu-id="606bb-152">Find hello details</span></span>
* <span data-ttu-id="606bb-153">authentification Azure Active Directory Hello étapes tooconfigure et d’utilisation sont presque identiques pour la base de données SQL Azure et Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="606bb-153">hello steps tooconfigure and use Azure Active Directory authentication are nearly identical for Azure SQL Database and Azure SQL Data Warehouse.</span></span> <span data-ttu-id="606bb-154">Suivez hello détaillées des étapes décrites dans la rubrique de hello [tooSQL de connexion de base de données ou SQL données entrepôt par à l’aide d’authentification Azure Active Directory](../sql-database/sql-database-aad-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="606bb-154">Follow hello detailed steps in hello topic [Connecting tooSQL Database or SQL Data Warehouse By Using Azure Active Directory Authentication](../sql-database/sql-database-aad-authentication.md).</span></span>
* <span data-ttu-id="606bb-155">Créer des rôles de base de données personnalisée et ajouter des rôles d’utilisateurs toohello.</span><span class="sxs-lookup"><span data-stu-id="606bb-155">Create custom database roles and add users toohello roles.</span></span> <span data-ttu-id="606bb-156">Accordez ensuite des autorisations granulaires toohello rôles.</span><span class="sxs-lookup"><span data-stu-id="606bb-156">Then grant granular permissions toohello roles.</span></span> <span data-ttu-id="606bb-157">Pour plus d’informations, consultez [Prise en main des autorisations du moteur de base de données](https://msdn.microsoft.com/library/mt667986.aspx).</span><span class="sxs-lookup"><span data-stu-id="606bb-157">For more information, see [Getting Started with Database Engine Permissions](https://msdn.microsoft.com/library/mt667986.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="606bb-158">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="606bb-158">Next steps</span></span>
<span data-ttu-id="606bb-159">toostart interrogation votre entrepôt de données avec Visual Studio et d’autres applications, consultez [requête avec Visual Studio][Query with Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="606bb-159">toostart querying your data warehouse with Visual Studio and other applications, see [Query with Visual Studio][Query with Visual Studio].</span></span>

<!-- Article references -->
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md
[Query with Visual Studio]: ./sql-data-warehouse-query-visual-studio.md
[What is Azure Active Directory]: ../active-directory/active-directory-whatis.md
[Azure AD features and limitations]: ../sql-database/sql-database-aad-authentication.md#azure-ad-features-and-limitations
