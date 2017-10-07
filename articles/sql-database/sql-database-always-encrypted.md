---
title: "Always Encrypted : Azure SQL Database - Magasin de certificats Windows | Microsoft Docs"
description: "Cet article vous explique comment toosecure des données sensibles dans une base de données SQL avec le chiffrement de base de données à l’aide de hello Assistant Always Encrypted dans SQL Server Management Studio (SSMS). Il vous montre également comment toostore stocker vos clés de chiffrement dans le certificat de Windows hello."
keywords: "chiffrer les données, chiffrement sql, chiffrement de base de données, données sensibles, chiffrement intégral"
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: cgronlun
ms.assetid: ce7e052e-8bf6-4d7c-9204-4c6f4afeba4b
ms.service: sql-database
ms.custom: security
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/02/2017
ms.author: sstein
ms.openlocfilehash: 483f9a2120cc42b732142fc07807d3d8830a0c33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="always-encrypted-protect-sensitive-data-in-sql-database-and-store-your-encryption-keys-in-hello-windows-certificate-store"></a><span data-ttu-id="d194a-105">Always Encrypted : Protéger les données sensibles dans la base de données SQL et de stocker vos clés de chiffrement dans le magasin de certificats Windows hello</span><span class="sxs-lookup"><span data-stu-id="d194a-105">Always Encrypted: Protect sensitive data in SQL Database and store your encryption keys in hello Windows certificate store</span></span>

<span data-ttu-id="d194a-106">Cet article vous explique comment toosecure des données sensibles dans un SQL de base de données avec le chiffrement de base de données à l’aide de hello [Assistant Always Encrypted](https://msdn.microsoft.com/library/mt459280.aspx) dans [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/hh213248.aspx).</span><span class="sxs-lookup"><span data-stu-id="d194a-106">This article shows you how toosecure sensitive data in a SQL database with database encryption by using hello [Always Encrypted Wizard](https://msdn.microsoft.com/library/mt459280.aspx) in [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/hh213248.aspx).</span></span> <span data-ttu-id="d194a-107">Il vous montre également comment toostore stocker vos clés de chiffrement dans le certificat de Windows hello.</span><span class="sxs-lookup"><span data-stu-id="d194a-107">It also shows you how toostore your encryption keys in hello Windows certificate store.</span></span>

<span data-ttu-id="d194a-108">Always Encrypted est une nouvelle technologie de chiffrement de données dans la base de données SQL Azure et SQL Server qui vous aide à protéger les données sensibles au repos sur le serveur de hello, au cours de déplacement entre client et serveur, et pendant que les données de salutation sont en cours d’utilisation, garantissant que les données sensibles ne s’affiche en tant que texte en clair à l’intérieur du système de base de données hello.</span><span class="sxs-lookup"><span data-stu-id="d194a-108">Always Encrypted is a new data encryption technology in Azure SQL Database and SQL Server that helps protect sensitive data at rest on hello server, during movement between client and server, and while hello data is in use, ensuring that sensitive data never appears as plaintext inside hello database system.</span></span> <span data-ttu-id="d194a-109">Une fois que vous chiffrez les données, uniquement les applications clientes ou les serveurs d’applications qui ont des clés d’accès toohello peuvent accéder aux données de texte en clair.</span><span class="sxs-lookup"><span data-stu-id="d194a-109">After you encrypt data, only client applications or app servers that have access toohello keys can access plaintext data.</span></span> <span data-ttu-id="d194a-110">Pour plus d’informations, consultez [Chiffrement intégral (moteur de base de données)](https://msdn.microsoft.com/library/mt163865.aspx).</span><span class="sxs-lookup"><span data-stu-id="d194a-110">For detailed information, see [Always Encrypted (Database Engine)](https://msdn.microsoft.com/library/mt163865.aspx).</span></span>

<span data-ttu-id="d194a-111">Après avoir configuré hello toouse de base de données Always Encrypted, vous allez créer une application cliente en c# avec toowork de Visual Studio avec des données hello chiffré.</span><span class="sxs-lookup"><span data-stu-id="d194a-111">After configuring hello database toouse Always Encrypted, you will create a client application in C# with Visual Studio toowork with hello encrypted data.</span></span>

<span data-ttu-id="d194a-112">Suivez les étapes de hello dans cet article de toolearn comment tooset d’Always Encrypted pour une base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="d194a-112">Follow hello steps in this article toolearn how tooset up Always Encrypted for an Azure SQL database.</span></span> <span data-ttu-id="d194a-113">Dans cet article, vous allez apprendre des tâches de hello tooperform suivant :</span><span class="sxs-lookup"><span data-stu-id="d194a-113">In this article, you will learn how tooperform hello following tasks:</span></span>

* <span data-ttu-id="d194a-114">Utilisez l’Assistant Always Encrypted hello dans SSMS toocreate [clés Always Encrypted](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_3).</span><span class="sxs-lookup"><span data-stu-id="d194a-114">Use hello Always Encrypted wizard in SSMS toocreate [Always Encrypted Keys](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_3).</span></span>
  * <span data-ttu-id="d194a-115">Créer une [clé principale de colonne (CMK)](https://msdn.microsoft.com/library/mt146393.aspx).</span><span class="sxs-lookup"><span data-stu-id="d194a-115">Create a [Column Master Key (CMK)](https://msdn.microsoft.com/library/mt146393.aspx).</span></span>
  * <span data-ttu-id="d194a-116">Créer une [clé de chiffrement de colonne (CEK)](https://msdn.microsoft.com/library/mt146372.aspx).</span><span class="sxs-lookup"><span data-stu-id="d194a-116">Create a [Column Encryption Key (CEK)](https://msdn.microsoft.com/library/mt146372.aspx).</span></span>
* <span data-ttu-id="d194a-117">Créer une table de base de données et chiffrer des colonnes.</span><span class="sxs-lookup"><span data-stu-id="d194a-117">Create a database table and encrypt columns.</span></span>
* <span data-ttu-id="d194a-118">Créer une application qui insère, sélectionne et affiche les données des colonnes de hello chiffré.</span><span class="sxs-lookup"><span data-stu-id="d194a-118">Create an application that inserts, selects, and displays data from hello encrypted columns.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d194a-119">Composants requis</span><span class="sxs-lookup"><span data-stu-id="d194a-119">Prerequisites</span></span>
<span data-ttu-id="d194a-120">Pour ce didacticiel, vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="d194a-120">For this tutorial, you'll need:</span></span>

* <span data-ttu-id="d194a-121">Un compte et un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="d194a-121">An Azure account and subscription.</span></span> <span data-ttu-id="d194a-122">Si vous n’en avez pas, inscrivez-vous pour un [essai gratuit](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d194a-122">If you don't have one, sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="d194a-123">[SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt238290.aspx) , version 13.0.700.242 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="d194a-123">[SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) version 13.0.700.242 or later.</span></span>
* <span data-ttu-id="d194a-124">[.NET framework 4.6](https://msdn.microsoft.com/library/w0x726c2.aspx) ou version ultérieure (sur l’ordinateur client de hello).</span><span class="sxs-lookup"><span data-stu-id="d194a-124">[.NET Framework 4.6](https://msdn.microsoft.com/library/w0x726c2.aspx) or later (on hello client computer).</span></span>
* <span data-ttu-id="d194a-125">[Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="d194a-125">[Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx).</span></span>

## <a name="create-a-blank-sql-database"></a><span data-ttu-id="d194a-126">Créer une base de données SQL vide</span><span class="sxs-lookup"><span data-stu-id="d194a-126">Create a blank SQL database</span></span>
1. <span data-ttu-id="d194a-127">Connectez-vous à toohello [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="d194a-127">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="d194a-128">Cliquez sur **Nouveau** > **Données + stockage** > **SQL Database**.</span><span class="sxs-lookup"><span data-stu-id="d194a-128">Click **New** > **Data + Storage** > **SQL Database**.</span></span>
3. <span data-ttu-id="d194a-129">Créez une base de données **vide** nommée **Clinique** sur un serveur nouveau ou existant.</span><span class="sxs-lookup"><span data-stu-id="d194a-129">Create a **Blank** database named **Clinic** on a new or existing server.</span></span> <span data-ttu-id="d194a-130">Pour obtenir des instructions détaillées sur la création d’une base de données Bonjour portail Azure, consultez [votre première base de données SQL Azure](sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d194a-130">For detailed instructions about creating a database in hello Azure portal, see [Your first Azure SQL database](sql-database-get-started-portal.md).</span></span>
   
    ![Créer une base de données vide](./media/sql-database-always-encrypted/create-database.png)

<span data-ttu-id="d194a-132">Vous devrez la chaîne de connexion hello plus loin dans le didacticiel de hello.</span><span class="sxs-lookup"><span data-stu-id="d194a-132">You will need hello connection string later in hello tutorial.</span></span> <span data-ttu-id="d194a-133">Après la création de la base de données hello, accédez à toohello nouvelle clinique de base de données et copie hello chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="d194a-133">After hello database is created, go toohello new Clinic database and copy hello connection string.</span></span> <span data-ttu-id="d194a-134">Vous pouvez obtenir la chaîne de connexion hello à tout moment, mais il est facile toocopy il lorsque vous êtes dans hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="d194a-134">You can get hello connection string at any time, but it's easy toocopy it when you're in hello Azure portal.</span></span>

1. <span data-ttu-id="d194a-135">Cliquez sur **Bases de données SQL** > **Clinique** > **Afficher les chaînes de connexion de la base de données**.</span><span class="sxs-lookup"><span data-stu-id="d194a-135">Click **SQL databases** > **Clinic** > **Show database connection strings**.</span></span>
2. <span data-ttu-id="d194a-136">Copier la chaîne de connexion hello pour **ADO.NET**.</span><span class="sxs-lookup"><span data-stu-id="d194a-136">Copy hello connection string for **ADO.NET**.</span></span>
   
    ![Copier la chaîne de connexion hello](./media/sql-database-always-encrypted/connection-strings.png)

## <a name="connect-toohello-database-with-ssms"></a><span data-ttu-id="d194a-138">Connexion de base de données toohello avec SSMS</span><span class="sxs-lookup"><span data-stu-id="d194a-138">Connect toohello database with SSMS</span></span>
<span data-ttu-id="d194a-139">Ouvrez SSMS et se connecter toohello server avec base de données de la clinique hello.</span><span class="sxs-lookup"><span data-stu-id="d194a-139">Open SSMS and connect toohello server with hello Clinic database.</span></span>

1. <span data-ttu-id="d194a-140">Ouvrez SSMS.</span><span class="sxs-lookup"><span data-stu-id="d194a-140">Open SSMS.</span></span> <span data-ttu-id="d194a-141">(Cliquez sur **Connect** > **moteur de base de données** tooopen hello **connecter tooServer** fenêtre si elle n’est pas ouvert).</span><span class="sxs-lookup"><span data-stu-id="d194a-141">(Click **Connect** > **Database Engine** tooopen hello **Connect tooServer** window if it is not open).</span></span>
2. <span data-ttu-id="d194a-142">Entrez le nom du serveur et vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="d194a-142">Enter your server name and credentials.</span></span> <span data-ttu-id="d194a-143">nom du serveur Hello se trouve sur le panneau de base de données SQL hello et dans la chaîne de connexion hello que vous avez copiée précédemment.</span><span class="sxs-lookup"><span data-stu-id="d194a-143">hello server name can be found on hello SQL database blade and in hello connection string you copied earlier.</span></span> <span data-ttu-id="d194a-144">Notamment de nom complet du serveur de type hello *database.windows.net*.</span><span class="sxs-lookup"><span data-stu-id="d194a-144">Type hello complete server name including *database.windows.net*.</span></span>
   
    ![Copier la chaîne de connexion hello](./media/sql-database-always-encrypted/ssms-connect.png)

<span data-ttu-id="d194a-146">Si hello **nouvelle règle de pare-feu** s’affiche, connectez-vous à tooAzure et SSMS permettent de créer une règle de pare-feu pour vous.</span><span class="sxs-lookup"><span data-stu-id="d194a-146">If hello **New Firewall Rule** window opens, sign in tooAzure and let SSMS create a new firewall rule for you.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="d194a-147">Création d’une table</span><span class="sxs-lookup"><span data-stu-id="d194a-147">Create a table</span></span>
<span data-ttu-id="d194a-148">Dans cette section, vous allez créer des données patient toohold table.</span><span class="sxs-lookup"><span data-stu-id="d194a-148">In this section, you will create a table toohold patient data.</span></span> <span data-ttu-id="d194a-149">Ce sera une table normale au départ, vous allez configurer le chiffrement dans la section suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="d194a-149">This will be a normal table initially--you will configure encryption in hello next section.</span></span>

1. <span data-ttu-id="d194a-150">Développez **Bases de données**.</span><span class="sxs-lookup"><span data-stu-id="d194a-150">Expand **Databases**.</span></span>
2. <span data-ttu-id="d194a-151">Avec le bouton hello **Clinic** de base de données et cliquez sur **nouvelle requête**.</span><span class="sxs-lookup"><span data-stu-id="d194a-151">Right-click hello **Clinic** database and click **New Query**.</span></span>
3. <span data-ttu-id="d194a-152">Hello coller suivant Transact-SQL (T-SQL) dans la nouvelle fenêtre de requête hello et **Execute** il.</span><span class="sxs-lookup"><span data-stu-id="d194a-152">Paste hello following Transact-SQL (T-SQL) into hello new query window and **Execute** it.</span></span>

        CREATE TABLE [dbo].[Patients](
         [PatientId] [int] IDENTITY(1,1),
         [SSN] [char](11) NOT NULL,
         [FirstName] [nvarchar](50) NULL,
         [LastName] [nvarchar](50) NULL,
         [MiddleName] [nvarchar](50) NULL,
         [StreetAddress] [nvarchar](50) NULL,
         [City] [nvarchar](50) NULL,
         [ZipCode] [char](5) NULL,
         [State] [char](2) NULL,
         [BirthDate] [date] NOT NULL
         PRIMARY KEY CLUSTERED ([PatientId] ASC) ON [PRIMARY] );
         GO


## <a name="encrypt-columns-configure-always-encrypted"></a><span data-ttu-id="d194a-153">Chiffrer des colonnes (configurer le chiffrement intégral)</span><span class="sxs-lookup"><span data-stu-id="d194a-153">Encrypt columns (configure Always Encrypted)</span></span>
<span data-ttu-id="d194a-154">SSMS fournit un Assistant tooeasily configurer Always Encrypted en définissant hello CMK, CEK et les colonnes chiffrées pour vous.</span><span class="sxs-lookup"><span data-stu-id="d194a-154">SSMS provides a wizard tooeasily configure Always Encrypted by setting up hello CMK, CEK, and encrypted columns for you.</span></span>

1. <span data-ttu-id="d194a-155">Développez **Bases de données** > **Clinique** > **Tables**.</span><span class="sxs-lookup"><span data-stu-id="d194a-155">Expand **Databases** > **Clinic** > **Tables**.</span></span>
2. <span data-ttu-id="d194a-156">Avec le bouton hello **Patients** de table et sélectionnez **chiffrer les colonnes** Assistant de chiffrement intégral hello tooopen :</span><span class="sxs-lookup"><span data-stu-id="d194a-156">Right-click hello **Patients** table and select **Encrypt Columns** tooopen hello Always Encrypted wizard:</span></span>
   
    ![Chiffrer les colonnes](./media/sql-database-always-encrypted/encrypt-columns.png)

<span data-ttu-id="d194a-158">Assistant Always Encrypted Hello comprend les sections suivantes de hello : **sélection de la colonne**, **Configuration de la clé principale de** (CMK), **Validation**, et  **Résumé**.</span><span class="sxs-lookup"><span data-stu-id="d194a-158">hello Always Encrypted wizard includes hello following sections: **Column Selection**, **Master Key Configuration** (CMK), **Validation**, and **Summary**.</span></span>

### <a name="column-selection"></a><span data-ttu-id="d194a-159">Sélection de colonnes</span><span class="sxs-lookup"><span data-stu-id="d194a-159">Column Selection</span></span>
<span data-ttu-id="d194a-160">Cliquez sur **suivant** sur hello **Introduction** hello tooopen de page **sélection de la colonne** page.</span><span class="sxs-lookup"><span data-stu-id="d194a-160">Click **Next** on hello **Introduction** page tooopen hello **Column Selection** page.</span></span> <span data-ttu-id="d194a-161">Dans cette page, vous sélectionnerez quelles colonnes vous souhaitez tooencrypt, [hello du type de chiffrement et quelle clé de chiffrement de colonne (CEK)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) toouse.</span><span class="sxs-lookup"><span data-stu-id="d194a-161">On this page, you will select which columns you want tooencrypt, [hello type of encryption, and what column encryption key (CEK)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) toouse.</span></span>

<span data-ttu-id="d194a-162">Chiffrez les informations **SSN** et **BirthDate** pour chaque patient.</span><span class="sxs-lookup"><span data-stu-id="d194a-162">Encrypt **SSN** and **BirthDate** information for each patient.</span></span> <span data-ttu-id="d194a-163">Hello **SSN** colonne utilise le chiffrement déterministe, qui prend en charge les recherches d’égalité, de jointures et de group by.</span><span class="sxs-lookup"><span data-stu-id="d194a-163">hello **SSN** column will use deterministic encryption, which supports equality lookups, joins, and group by.</span></span> <span data-ttu-id="d194a-164">Hello **BirthDate** colonne utilise le chiffrement aléatoire, qui ne prend pas en charge les opérations.</span><span class="sxs-lookup"><span data-stu-id="d194a-164">hello **BirthDate** column will use randomized encryption, which does not support operations.</span></span>

<span data-ttu-id="d194a-165">Ensemble hello **le Type de chiffrement** pour hello **SSN** colonne trop**déterministe** et hello **BirthDate** colonne trop **Aléatoire**.</span><span class="sxs-lookup"><span data-stu-id="d194a-165">Set hello **Encryption Type** for hello **SSN** column too**Deterministic** and hello **BirthDate** column too**Randomized**.</span></span> <span data-ttu-id="d194a-166">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="d194a-166">Click **Next**.</span></span>

![Chiffrer les colonnes](./media/sql-database-always-encrypted/column-selection.png)

### <a name="master-key-configuration"></a><span data-ttu-id="d194a-168">Configuration de la clé principale</span><span class="sxs-lookup"><span data-stu-id="d194a-168">Master Key Configuration</span></span>
<span data-ttu-id="d194a-169">Hello **Master Key Configuration** page est où vous configurez votre clé CMK et le fournisseur de magasin de clés hello sélectionnez où hello CMK sera stocké.</span><span class="sxs-lookup"><span data-stu-id="d194a-169">hello **Master Key Configuration** page is where you set up your CMK and select hello key store provider where hello CMK will be stored.</span></span> <span data-ttu-id="d194a-170">Actuellement, vous pouvez stocker une clé CMK dans le magasin de certificats Windows hello, Azure Key Vault ou un module de sécurité matériel (HSM).</span><span class="sxs-lookup"><span data-stu-id="d194a-170">Currently, you can store a CMK in hello Windows certificate store, Azure Key Vault, or a hardware security module (HSM).</span></span> <span data-ttu-id="d194a-171">Ce didacticiel montre comment toostore stocker vos clés de certificat de Windows hello.</span><span class="sxs-lookup"><span data-stu-id="d194a-171">This tutorial shows how toostore your keys in hello Windows certificate store.</span></span>

<span data-ttu-id="d194a-172">Vérifiez que l’option **Magasin de certificats Windows** est sélectionnée, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="d194a-172">Verify that **Windows certificate store** is selected and click **Next**.</span></span>

![Configuration de la clé principale](./media/sql-database-always-encrypted/master-key-configuration.png)

### <a name="validation"></a><span data-ttu-id="d194a-174">Validation</span><span class="sxs-lookup"><span data-stu-id="d194a-174">Validation</span></span>
<span data-ttu-id="d194a-175">Vous pouvez chiffrer les colonnes hello maintenant ou enregistrer un toorun de script PowerShell plus tard.</span><span class="sxs-lookup"><span data-stu-id="d194a-175">You can encrypt hello columns now or save a PowerShell script toorun later.</span></span> <span data-ttu-id="d194a-176">Pour ce didacticiel, sélectionnez **continuer toofinish maintenant** et cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="d194a-176">For this tutorial, select **Proceed toofinish now** and click **Next**.</span></span>

### <a name="summary"></a><span data-ttu-id="d194a-177">Résumé</span><span class="sxs-lookup"><span data-stu-id="d194a-177">Summary</span></span>
<span data-ttu-id="d194a-178">Vérifiez que les paramètres de hello sont correctes, cliquez sur **Terminer** le programme d’installation de toocomplete hello pour Always Encrypted.</span><span class="sxs-lookup"><span data-stu-id="d194a-178">Verify that hello settings are all correct and click **Finish** toocomplete hello setup for Always Encrypted.</span></span>

![Résumé](./media/sql-database-always-encrypted/summary.png)

### <a name="verify-hello-wizards-actions"></a><span data-ttu-id="d194a-180">Vérifier les actions de l’Assistant hello</span><span class="sxs-lookup"><span data-stu-id="d194a-180">Verify hello wizard's actions</span></span>
<span data-ttu-id="d194a-181">Une fois hello Assistant terminé, votre base de données est configurée pour Always Encrypted.</span><span class="sxs-lookup"><span data-stu-id="d194a-181">After hello wizard is finished, your database is set up for Always Encrypted.</span></span> <span data-ttu-id="d194a-182">Bonjour Bonjour d’Assistant effectué suivant des actions :</span><span class="sxs-lookup"><span data-stu-id="d194a-182">hello wizard performed hello following actions:</span></span>

* <span data-ttu-id="d194a-183">Création d’une CMK.</span><span class="sxs-lookup"><span data-stu-id="d194a-183">Created a CMK.</span></span>
* <span data-ttu-id="d194a-184">Création d’une CEK.</span><span class="sxs-lookup"><span data-stu-id="d194a-184">Created a CEK.</span></span>
* <span data-ttu-id="d194a-185">Hello configuré sélectionné des colonnes pour le chiffrement.</span><span class="sxs-lookup"><span data-stu-id="d194a-185">Configured hello selected columns for encryption.</span></span> <span data-ttu-id="d194a-186">Votre **Patients** table a actuellement pas de données, mais les données existantes dans les colonnes hello sélectionné sont désormais chiffrées.</span><span class="sxs-lookup"><span data-stu-id="d194a-186">Your **Patients** table currently has no data, but any existing data in hello selected columns is now encrypted.</span></span>

<span data-ttu-id="d194a-187">Vous pouvez vérifier la création de hello de clés hello dans SSMS en accédant trop**Clinic** > **sécurité** > **clés Always Encrypted**.</span><span class="sxs-lookup"><span data-stu-id="d194a-187">You can verify hello creation of hello keys in SSMS by going too**Clinic** > **Security** > **Always Encrypted Keys**.</span></span> <span data-ttu-id="d194a-188">Vous pouvez maintenant voir hello nouvelles clés hello généré pour vous par un Assistant.</span><span class="sxs-lookup"><span data-stu-id="d194a-188">You can now see hello new keys that hello wizard generated for you.</span></span>

## <a name="create-a-client-application-that-works-with-hello-encrypted-data"></a><span data-ttu-id="d194a-189">Créer une application cliente qui fonctionne avec les données de salutation chiffrée</span><span class="sxs-lookup"><span data-stu-id="d194a-189">Create a client application that works with hello encrypted data</span></span>
<span data-ttu-id="d194a-190">Maintenant que le chiffrement intégral est configuré, vous pouvez générer une application qui effectue *insère* et *sélectionne* sur hello des colonnes chiffrées.</span><span class="sxs-lookup"><span data-stu-id="d194a-190">Now that Always Encrypted is set up, you can build an application that performs *inserts* and *selects* on hello encrypted columns.</span></span> <span data-ttu-id="d194a-191">toosuccessfully exécuter hello, exemple d’application, vous devez l’exécuter sur hello même ordinateur où vous avez exécuté Assistant Always Encrypted de hello.</span><span class="sxs-lookup"><span data-stu-id="d194a-191">toosuccessfully run hello sample application, you must run it on hello same computer where you ran hello Always Encrypted wizard.</span></span> <span data-ttu-id="d194a-192">application de hello toorun sur un autre ordinateur, vous devez déployer votre ordinateur de toohello de certificats Always Encrypted hello client application en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="d194a-192">toorun hello application on another computer, you must deploy your Always Encrypted certificates toohello computer running hello client app.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="d194a-193">Votre application doit utiliser [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) objets lors du passage du serveur de toohello de données de texte en clair avec des colonnes toujours chiffrées.</span><span class="sxs-lookup"><span data-stu-id="d194a-193">Your application must use [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) objects when passing plaintext data toohello server with Always Encrypted columns.</span></span> <span data-ttu-id="d194a-194">La transmission de valeurs littérales sans objets SqlParameter entraînera une exception.</span><span class="sxs-lookup"><span data-stu-id="d194a-194">Passing literal values without using SqlParameter objects will result in an exception.</span></span>
> 
> 

1. <span data-ttu-id="d194a-195">Ouvrez Visual Studio et créez une nouvelle application console C#.</span><span class="sxs-lookup"><span data-stu-id="d194a-195">Open Visual Studio and create a new C# console application.</span></span> <span data-ttu-id="d194a-196">Assurez-vous que votre projet est trop**.NET Framework 4.6** ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="d194a-196">Make sure your project is set too**.NET Framework 4.6** or later.</span></span>
2. <span data-ttu-id="d194a-197">Projet de hello nom **AlwaysEncryptedConsoleApp** et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="d194a-197">Name hello project **AlwaysEncryptedConsoleApp** and click **OK**.</span></span>

![Nouvelle application de console](./media/sql-database-always-encrypted/console-app.png)

## <a name="modify-your-connection-string-tooenable-always-encrypted"></a><span data-ttu-id="d194a-199">Modifier votre tooenable de chaîne de connexion Always Encrypted</span><span class="sxs-lookup"><span data-stu-id="d194a-199">Modify your connection string tooenable Always Encrypted</span></span>
<span data-ttu-id="d194a-200">Cette section explique comment tooenable toujours chiffré dans votre chaîne de connexion de base de données.</span><span class="sxs-lookup"><span data-stu-id="d194a-200">This section explains how tooenable Always Encrypted in your database connection string.</span></span> <span data-ttu-id="d194a-201">Vous allez modifier les applications de console hello que vous venez de créer dans la section suivante hello, « Always Encrypted exemple d’application console. »</span><span class="sxs-lookup"><span data-stu-id="d194a-201">You will modify hello console app you just created in hello next section, "Always Encrypted sample console application."</span></span>

<span data-ttu-id="d194a-202">tooenable Always Encrypted, vous devez tooadd hello **Column Encryption Setting** connexion tooyour de mot clé de chaîne et la définir trop**activé**.</span><span class="sxs-lookup"><span data-stu-id="d194a-202">tooenable Always Encrypted, you need tooadd hello **Column Encryption Setting** keyword tooyour connection string and set it too**Enabled**.</span></span>

<span data-ttu-id="d194a-203">Vous pouvez définir cette option directement dans la chaîne de connexion hello, ou vous pouvez la définir en utilisant un [SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx).</span><span class="sxs-lookup"><span data-stu-id="d194a-203">You can set this directly in hello connection string, or you can set it by using a [SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx).</span></span> <span data-ttu-id="d194a-204">exemple d’application Hello Bonjour section suivante montre comment toouse **SqlConnectionStringBuilder**.</span><span class="sxs-lookup"><span data-stu-id="d194a-204">hello sample application in hello next section shows how toouse **SqlConnectionStringBuilder**.</span></span>

> [!NOTE]
> <span data-ttu-id="d194a-205">Il s’agit de hello seul changement nécessaire dans une application de client spécifique tooAlways chiffré.</span><span class="sxs-lookup"><span data-stu-id="d194a-205">This is hello only change required in a client application specific tooAlways Encrypted.</span></span> <span data-ttu-id="d194a-206">Si vous avez une application existante qui stocke la chaîne de connexion en externe (autrement dit, dans un fichier de configuration), vous pouvez être en mesure de tooenable Always Encrypted sans modification de code.</span><span class="sxs-lookup"><span data-stu-id="d194a-206">If you have an existing application that stores its connection string externally (that is, in a config file), you might be able tooenable Always Encrypted without changing any code.</span></span>
> 
> 

### <a name="enable-always-encrypted-in-hello-connection-string"></a><span data-ttu-id="d194a-207">Activer le chiffrement intégral dans la chaîne de connexion hello</span><span class="sxs-lookup"><span data-stu-id="d194a-207">Enable Always Encrypted in hello connection string</span></span>
<span data-ttu-id="d194a-208">Ajoutez hello suivant de chaîne de connexion mot clé tooyour :</span><span class="sxs-lookup"><span data-stu-id="d194a-208">Add hello following keyword tooyour connection string:</span></span>

    Column Encryption Setting=Enabled


### <a name="enable-always-encrypted-with-a-sqlconnectionstringbuilder"></a><span data-ttu-id="d194a-209">Activation du chiffrement intégral avec un paramètre SqlConnectionStringBuilder</span><span class="sxs-lookup"><span data-stu-id="d194a-209">Enable Always Encrypted with a SqlConnectionStringBuilder</span></span>
<span data-ttu-id="d194a-210">Hello de code suivant montre comment tooenable Always Encrypted en définissant hello [SqlConnectionStringBuilder.ColumnEncryptionSetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx) trop[activé](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx).</span><span class="sxs-lookup"><span data-stu-id="d194a-210">hello following code shows how tooenable Always Encrypted by setting hello [SqlConnectionStringBuilder.ColumnEncryptionSetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx) too[Enabled](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx).</span></span>

    // Instantiate a SqlConnectionStringBuilder.
    SqlConnectionStringBuilder connStringBuilder =
       new SqlConnectionStringBuilder("replace with your connection string");

    // Enable Always Encrypted.
    connStringBuilder.ColumnEncryptionSetting =
       SqlConnectionColumnEncryptionSetting.Enabled;



## <a name="always-encrypted-sample-console-application"></a><span data-ttu-id="d194a-211">Exemple d’application console intégralement chiffrée</span><span class="sxs-lookup"><span data-stu-id="d194a-211">Always Encrypted sample console application</span></span>
<span data-ttu-id="d194a-212">Cet exemple montre comment :</span><span class="sxs-lookup"><span data-stu-id="d194a-212">This sample demonstrates how to:</span></span>

* <span data-ttu-id="d194a-213">Modifiez votre tooenable de chaîne de connexion Always Encrypted.</span><span class="sxs-lookup"><span data-stu-id="d194a-213">Modify your connection string tooenable Always Encrypted.</span></span>
* <span data-ttu-id="d194a-214">Insérer des données dans des colonnes de hello chiffré.</span><span class="sxs-lookup"><span data-stu-id="d194a-214">Insert data into hello encrypted columns.</span></span>
* <span data-ttu-id="d194a-215">Sélectionner un enregistrement en filtrant une valeur spécifique dans une colonne chiffrée.</span><span class="sxs-lookup"><span data-stu-id="d194a-215">Select a record by filtering for a specific value in an encrypted column.</span></span>

<span data-ttu-id="d194a-216">Remplacez le contenu hello de **Program.cs** avec hello suivant de code.</span><span class="sxs-lookup"><span data-stu-id="d194a-216">Replace hello contents of **Program.cs** with hello following code.</span></span> <span data-ttu-id="d194a-217">Remplacez la chaîne de connexion hello pour la variable de connectionString global hello dans la ligne hello directement au-dessus de la méthode Main de hello avec votre chaîne de connexion valide à partir de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="d194a-217">Replace hello connection string for hello global connectionString variable in hello line directly above hello Main method with your valid connection string from hello Azure portal.</span></span> <span data-ttu-id="d194a-218">Il s’agit de hello seule modification que vous avez besoin de toomake toothis code.</span><span class="sxs-lookup"><span data-stu-id="d194a-218">This is hello only change you need toomake toothis code.</span></span>

<span data-ttu-id="d194a-219">Exécuter toosee d’application hello Always Encrypted en action.</span><span class="sxs-lookup"><span data-stu-id="d194a-219">Run hello app toosee Always Encrypted in action.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using System.Data;
    using System.Data.SqlClient;

    namespace AlwaysEncryptedConsoleApp
    {
    class Program
    {
        // Update this line with your Clinic database connection string from hello Azure portal.
        static string connectionString = @"Replace with your connection string";

        static void Main(string[] args)
        {
            Console.WriteLine("Original connection string copied from hello Azure portal:");
            Console.WriteLine(connectionString);

            // Create a SqlConnectionStringBuilder.
            SqlConnectionStringBuilder connStringBuilder =
                new SqlConnectionStringBuilder(connectionString);

            // Enable Always Encrypted for hello connection.
            // This is hello only change specific tooAlways Encrypted
            connStringBuilder.ColumnEncryptionSetting =
                SqlConnectionColumnEncryptionSetting.Enabled;

            Console.WriteLine(Environment.NewLine + "Updated connection string with Always Encrypted enabled:");
            Console.WriteLine(connStringBuilder.ConnectionString);

            // Update hello connection string with a password supplied at runtime.
            Console.WriteLine(Environment.NewLine + "Enter server password:");
            connStringBuilder.Password = Console.ReadLine();


            // Assign hello updated connection string tooour global variable.
            connectionString = connStringBuilder.ConnectionString;


            // Delete all records toorestart this demo app.
            ResetPatientsTable();

            // Add sample data toohello Patients table.
            Console.Write(Environment.NewLine + "Adding sample patient data toohello database...");

            InsertPatient(new Patient() {
                SSN = "999-99-0001", FirstName = "Orlando", LastName = "Gee", BirthDate = DateTime.Parse("01/04/1964") });
            InsertPatient(new Patient() {
                SSN = "999-99-0002", FirstName = "Keith", LastName = "Harris", BirthDate = DateTime.Parse("06/20/1977") });
            InsertPatient(new Patient() {
                SSN = "999-99-0003", FirstName = "Donna", LastName = "Carreras", BirthDate = DateTime.Parse("02/09/1973") });
            InsertPatient(new Patient() {
                SSN = "999-99-0004", FirstName = "Janet", LastName = "Gates", BirthDate = DateTime.Parse("08/31/1985") });
            InsertPatient(new Patient() {
                SSN = "999-99-0005", FirstName = "Lucy", LastName = "Harrington", BirthDate = DateTime.Parse("05/06/1993") });


            // Fetch and display all patients.
            Console.WriteLine(Environment.NewLine + "All hello records currently in hello Patients table:");

            foreach (Patient patient in SelectAllPatients())
            {
                Console.WriteLine(patient.FirstName + " " + patient.LastName + "\tSSN: " + patient.SSN + "\tBirthdate: " + patient.BirthDate);
            }

            // Get patients by SSN.
            Console.WriteLine(Environment.NewLine + "Now let's locate records by searching hello encrypted SSN column.");

            string ssn;

            // This very simple validation only checks that hello user entered 11 characters.
            // In production be sure toocheck all user input and use hello best validation for your specific application.
            do
            {
                Console.WriteLine("Please enter a valid SSN (ex. 123-45-6789):");
                ssn = Console.ReadLine();
            } while (ssn.Length != 11);

            // hello example allows duplicate SSN entries so we will return all records
            // that match hello provided value and store hello results in selectedPatients.
            Patient selectedPatient = SelectPatientBySSN(ssn);

            // Check if any records were returned and display our query results.
            if (selectedPatient != null)
            {
                Console.WriteLine("Patient found with SSN = " + ssn);
                Console.WriteLine(selectedPatient.FirstName + " " + selectedPatient.LastName + "\tSSN: "
                    + selectedPatient.SSN + "\tBirthdate: " + selectedPatient.BirthDate);
            }
            else
            {
                Console.WriteLine("No patients found with SSN = " + ssn);
            }

            Console.WriteLine("Press Enter tooexit...");
            Console.ReadLine();
        }


        static int InsertPatient(Patient newPatient)
        {
            int returnValue = 0;

            string sqlCmdText = @"INSERT INTO [dbo].[Patients] ([SSN], [FirstName], [LastName], [BirthDate])
         VALUES (@SSN, @FirstName, @LastName, @BirthDate);";

            SqlCommand sqlCmd = new SqlCommand(sqlCmdText);


            SqlParameter paramSSN = new SqlParameter(@"@SSN", newPatient.SSN);
            paramSSN.DbType = DbType.AnsiStringFixedLength;
            paramSSN.Direction = ParameterDirection.Input;
            paramSSN.Size = 11;

            SqlParameter paramFirstName = new SqlParameter(@"@FirstName", newPatient.FirstName);
            paramFirstName.DbType = DbType.String;
            paramFirstName.Direction = ParameterDirection.Input;

            SqlParameter paramLastName = new SqlParameter(@"@LastName", newPatient.LastName);
            paramLastName.DbType = DbType.String;
            paramLastName.Direction = ParameterDirection.Input;

            SqlParameter paramBirthDate = new SqlParameter(@"@BirthDate", newPatient.BirthDate);
            paramBirthDate.SqlDbType = SqlDbType.Date;
            paramBirthDate.Direction = ParameterDirection.Input;

            sqlCmd.Parameters.Add(paramSSN);
            sqlCmd.Parameters.Add(paramFirstName);
            sqlCmd.Parameters.Add(paramLastName);
            sqlCmd.Parameters.Add(paramBirthDate);

            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    sqlCmd.ExecuteNonQuery();
                }
                catch (Exception ex)
                {
                    returnValue = 1;
                    Console.WriteLine("hello following error was encountered: ");
                    Console.WriteLine(ex.Message);
                    Console.WriteLine(Environment.NewLine + "Press Enter key tooexit");
                    Console.ReadLine();
                    Environment.Exit(0);
                }
            }
            return returnValue;
        }


        static List<Patient> SelectAllPatients()
        {
            List<Patient> patients = new List<Patient>();


            SqlCommand sqlCmd = new SqlCommand(
              "SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients]",
                new SqlConnection(connectionString));


            using (sqlCmd.Connection = new SqlConnection(connectionString))

            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    SqlDataReader reader = sqlCmd.ExecuteReader();

                    if (reader.HasRows)
                    {
                        while (reader.Read())
                        {
                            patients.Add(new Patient()
                            {
                                SSN = reader[0].ToString(),
                                FirstName = reader[1].ToString(),
                                LastName = reader["LastName"].ToString(),
                                BirthDate = (DateTime)reader["BirthDate"]
                            });
                        }
                    }
                }
                catch (Exception ex)
                {
                    throw;
                }
            }

            return patients;
        }


        static Patient SelectPatientBySSN(string ssn)
        {
            Patient patient = new Patient();

            SqlCommand sqlCmd = new SqlCommand(
                "SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE [SSN]=@SSN",
                new SqlConnection(connectionString));

            SqlParameter paramSSN = new SqlParameter(@"@SSN", ssn);
            paramSSN.DbType = DbType.AnsiStringFixedLength;
            paramSSN.Direction = ParameterDirection.Input;
            paramSSN.Size = 11;

            sqlCmd.Parameters.Add(paramSSN);


            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    SqlDataReader reader = sqlCmd.ExecuteReader();

                    if (reader.HasRows)
                    {
                        while (reader.Read())
                        {
                            patient = new Patient()
                            {
                                SSN = reader[0].ToString(),
                                FirstName = reader[1].ToString(),
                                LastName = reader["LastName"].ToString(),
                                BirthDate = (DateTime)reader["BirthDate"]
                            };
                        }
                    }
                    else
                    {
                        patient = null;
                    }
                }
                catch (Exception ex)
                {
                    throw;
                }
            }
            return patient;
        }


        // This method simply deletes all records in hello Patients table tooreset our demo.
        static int ResetPatientsTable()
        {
            int returnValue = 0;

            SqlCommand sqlCmd = new SqlCommand("DELETE FROM Patients");
            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    sqlCmd.ExecuteNonQuery();

                }
                catch (Exception ex)
                {
                    returnValue = 1;
                }
            }
            return returnValue;
        }
    }

    class Patient
    {
        public string SSN { get; set; }
        public string FirstName { get; set; }
        public string LastName { get; set; }
        public DateTime BirthDate { get; set; }
    }
    }


## <a name="verify-that-hello-data-is-encrypted"></a><span data-ttu-id="d194a-220">Vérifiez que les données de salutation sont chiffrées.</span><span class="sxs-lookup"><span data-stu-id="d194a-220">Verify that hello data is encrypted</span></span>
<span data-ttu-id="d194a-221">Vous pouvez vérifier rapidement le chiffrement des données réelles de hello sur le serveur de hello en interrogeant hello **Patients** données à l’aide de SSMS.</span><span class="sxs-lookup"><span data-stu-id="d194a-221">You can quickly check that hello actual data on hello server is encrypted by querying hello **Patients** data with SSMS.</span></span> <span data-ttu-id="d194a-222">(Utilisez votre connexion actuelle où le paramètre de chiffrement de colonne hello n’est pas encore activé.)</span><span class="sxs-lookup"><span data-stu-id="d194a-222">(Use your current connection where hello column encryption setting is not yet enabled.)</span></span>

<span data-ttu-id="d194a-223">Exécutez hello suivant de requête de base de données de la clinique hello.</span><span class="sxs-lookup"><span data-stu-id="d194a-223">Run hello following query on hello Clinic database.</span></span>

    SELECT FirstName, LastName, SSN, BirthDate FROM Patients;

<span data-ttu-id="d194a-224">Vous pouvez voir que les colonnes hello chiffré ne contiennent pas toutes les données en texte clair.</span><span class="sxs-lookup"><span data-stu-id="d194a-224">You can see that hello encrypted columns do not contain any plaintext data.</span></span>

   ![Nouvelle application de console](./media/sql-database-always-encrypted/ssms-encrypted.png)

<span data-ttu-id="d194a-226">toouse SSMS tooaccess hello des données en texte brut, vous pouvez ajouter des hello **paramètre de chiffrement de colonne = activé** connexion toohello de paramètre.</span><span class="sxs-lookup"><span data-stu-id="d194a-226">toouse SSMS tooaccess hello plaintext data, you can add hello **Column Encryption Setting=enabled** parameter toohello connection.</span></span>

1. <span data-ttu-id="d194a-227">Dans SSMS, cliquez avec le bouton droit sur votre serveur dans **l’Explorateur d’objets**, puis cliquez sur **Déconnexion**.</span><span class="sxs-lookup"><span data-stu-id="d194a-227">In SSMS, right-click your server in **Object Explorer**, and then click **Disconnect**.</span></span>
2. <span data-ttu-id="d194a-228">Cliquez sur **Connect** > **moteur de base de données** tooopen hello **connecter tooServer** fenêtre, puis cliquez sur **Options**.</span><span class="sxs-lookup"><span data-stu-id="d194a-228">Click **Connect** > **Database Engine** tooopen hello **Connect tooServer** window, and then click **Options**.</span></span>
3. <span data-ttu-id="d194a-229">Cliquez sur **Paramètres de connexion supplémentaires** et tapez **Column Encryption Setting=enabled**.</span><span class="sxs-lookup"><span data-stu-id="d194a-229">Click **Additional Connection Parameters** and type **Column Encryption Setting=enabled**.</span></span>
   
    ![Nouvelle application de console](./media/sql-database-always-encrypted/ssms-connection-parameter.png)
4. <span data-ttu-id="d194a-231">Exécution hello requête sur hello suivante **Clinic** base de données.</span><span class="sxs-lookup"><span data-stu-id="d194a-231">Run hello following query on hello **Clinic** database.</span></span>
   
        SELECT FirstName, LastName, SSN, BirthDate FROM Patients;
   
     <span data-ttu-id="d194a-232">Vous pouvez maintenant voir les données de texte en clair hello dans les colonnes hello chiffré.</span><span class="sxs-lookup"><span data-stu-id="d194a-232">You can now see hello plaintext data in hello encrypted columns.</span></span>

    ![Nouvelle application de console](./media/sql-database-always-encrypted/ssms-plaintext.png)



> [!NOTE]
> <span data-ttu-id="d194a-234">Si vous vous connectez avec SSMS (ou n’importe quel client) à partir d’un autre ordinateur, il n’aura pas accès aux clés de chiffrement de toohello et ne sera pas en mesure de toodecrypt les données de salutation.</span><span class="sxs-lookup"><span data-stu-id="d194a-234">If you connect with SSMS (or any client) from a different computer, it will not have access toohello encryption keys and will not be able toodecrypt hello data.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="d194a-235">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d194a-235">Next steps</span></span>
<span data-ttu-id="d194a-236">Après avoir créé une base de données qui utilise le chiffrement intégral, vous souhaiterez peut-être suivant de hello toodo :</span><span class="sxs-lookup"><span data-stu-id="d194a-236">After you create a database that uses Always Encrypted, you may want toodo hello following:</span></span>

* <span data-ttu-id="d194a-237">Exécuter cet exemple à partir d'un autre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="d194a-237">Run this sample from a different computer.</span></span> <span data-ttu-id="d194a-238">Il n’avez pas accès aux clés de chiffrement toohello, donc il n’aura pas accès aux données de texte en clair toohello et ne fonctionnera pas correctement.</span><span class="sxs-lookup"><span data-stu-id="d194a-238">It won't have access toohello encryption keys, so it will not have access toohello plaintext data and will not run successfully.</span></span>
* <span data-ttu-id="d194a-239">[Faire pivoter et nettoyer vos clés](https://msdn.microsoft.com/library/mt607048.aspx).</span><span class="sxs-lookup"><span data-stu-id="d194a-239">[Rotate and clean up your keys](https://msdn.microsoft.com/library/mt607048.aspx).</span></span>
* <span data-ttu-id="d194a-240">[Migrer des données déjà chiffrées avec le chiffrement intégral](https://msdn.microsoft.com/library/mt621539.aspx).</span><span class="sxs-lookup"><span data-stu-id="d194a-240">[Migrate data that is already encrypted with Always Encrypted](https://msdn.microsoft.com/library/mt621539.aspx).</span></span>
* <span data-ttu-id="d194a-241">[Déployer des ordinateurs du client des tooother de certificats Always Encrypted](https://msdn.microsoft.com/library/mt723359.aspx#Anchor_1) (voir la section de « Rendre tooApplications disponibles des certificats et les utilisateurs » hello).</span><span class="sxs-lookup"><span data-stu-id="d194a-241">[Deploy Always Encrypted certificates tooother client machines](https://msdn.microsoft.com/library/mt723359.aspx#Anchor_1) (see hello "Making Certificates Available tooApplications and Users" section).</span></span>

## <a name="related-information"></a><span data-ttu-id="d194a-242">Informations connexes</span><span class="sxs-lookup"><span data-stu-id="d194a-242">Related information</span></span>
* [<span data-ttu-id="d194a-243">Chiffrement intégral (développement client)</span><span class="sxs-lookup"><span data-stu-id="d194a-243">Always Encrypted (client development)</span></span>](https://msdn.microsoft.com/library/mt147923.aspx)
* [<span data-ttu-id="d194a-244">Chiffrement transparent des données</span><span class="sxs-lookup"><span data-stu-id="d194a-244">Transparent Data Encryption</span></span>](https://msdn.microsoft.com/library/bb934049.aspx)
* [<span data-ttu-id="d194a-245">Chiffrement SQL Server</span><span class="sxs-lookup"><span data-stu-id="d194a-245">SQL Server Encryption</span></span>](https://msdn.microsoft.com/library/bb510663.aspx)
* [<span data-ttu-id="d194a-246">Assistant Chiffrement intégral.</span><span class="sxs-lookup"><span data-stu-id="d194a-246">Always Encrypted Wizard</span></span>](https://msdn.microsoft.com/library/mt459280.aspx)
* [<span data-ttu-id="d194a-247">Blog Chiffrement intégral.</span><span class="sxs-lookup"><span data-stu-id="d194a-247">Always Encrypted Blog</span></span>](http://blogs.msdn.com/b/sqlsecurity/archive/tags/always-encrypted/)

