---
title: "aaaGeneric étape par le connecteur SQL étape | Documents Microsoft"
description: "Cet article est en marche vous via un système de ressources humaines simple à l’aide de pas à pas hello connecteur SQL générique."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 28c1cc60-24fd-4d0d-a36d-b4aba6de86e7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: b1b5f89ab588de6f92f173a7bc00f97180067669
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="generic-sql-connector-step-by-step"></a><span data-ttu-id="4eb5d-103">Connecteur SQL générique - Guide pas à pas</span><span class="sxs-lookup"><span data-stu-id="4eb5d-103">Generic SQL Connector step-by-step</span></span>
<span data-ttu-id="4eb5d-104">Cette rubrique est un guide pas à pas.</span><span class="sxs-lookup"><span data-stu-id="4eb5d-104">This topic is a step-by-step guide.</span></span> <span data-ttu-id="4eb5d-105">Elle explique comment créer un simple exemple de base de données Ressources humaines et l’utiliser pour importer certains utilisateurs et leur appartenance à un groupe.</span><span class="sxs-lookup"><span data-stu-id="4eb5d-105">It creates a simple sample HR database and use it for importing some users and their group membership.</span></span>

## <a name="prepare-hello-sample-database"></a><span data-ttu-id="4eb5d-106">Préparer la base de données exemple hello</span><span class="sxs-lookup"><span data-stu-id="4eb5d-106">Prepare hello sample database</span></span>
<span data-ttu-id="4eb5d-107">Sur un serveur exécutant SQL Server, exécuter un script SQL hello trouvé dans [annexe A](#appendix-a). Ce script crée une base de données portant le nom hello GSQLDEMO.</span><span class="sxs-lookup"><span data-stu-id="4eb5d-107">On a server running SQL Server, run hello SQL script found in [Appendix A](#appendix-a). This script creates a sample database with hello name GSQLDEMO.</span></span> <span data-ttu-id="4eb5d-108">modèle d’objet Hello pour hello créé ressemble de base de données de cette image :</span><span class="sxs-lookup"><span data-stu-id="4eb5d-108">hello object model for hello created database looks like this picture:</span></span>  
<span data-ttu-id="4eb5d-109">![Modèle objet](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/objectmodel.png)</span><span class="sxs-lookup"><span data-stu-id="4eb5d-109">![Object Model](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/objectmodel.png)</span></span>

<span data-ttu-id="4eb5d-110">Également créer un utilisateur de base de données de toouse tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="4eb5d-110">Also create a user you want toouse tooconnect toohello database.</span></span> <span data-ttu-id="4eb5d-111">Dans cette procédure pas à pas, hello utilisateur appelée FABRIKAM\SQLUser et situé dans le domaine de hello.</span><span class="sxs-lookup"><span data-stu-id="4eb5d-111">In this walkthrough, hello user is called FABRIKAM\SQLUser and located in hello domain.</span></span>

## <a name="create-hello-odbc-connection-file"></a><span data-ttu-id="4eb5d-112">Créer le fichier de connexion ODBC hello</span><span class="sxs-lookup"><span data-stu-id="4eb5d-112">Create hello ODBC connection file</span></span>
<span data-ttu-id="4eb5d-113">Hello connecteur SQL générique à l’aide de ODBC tooconnect toohello à distance.</span><span class="sxs-lookup"><span data-stu-id="4eb5d-113">hello Generic SQL Connector is using ODBC tooconnect toohello remote server.</span></span> <span data-ttu-id="4eb5d-114">Tout d’abord, nous devons toocreate un fichier avec les informations de connexion ODBC de hello.</span><span class="sxs-lookup"><span data-stu-id="4eb5d-114">First we need toocreate a file with hello ODBC connection information.</span></span>

1. <span data-ttu-id="4eb5d-115">Démarrer l’utilitaire de gestion hello ODBC sur votre serveur :</span><span class="sxs-lookup"><span data-stu-id="4eb5d-115">Start hello ODBC management utility on your server:</span></span>  
   ![ODBC](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc.png)
2. <span data-ttu-id="4eb5d-117">Onglet de hello sélectionnez **DSN de fichier**.</span><span class="sxs-lookup"><span data-stu-id="4eb5d-117">Select hello tab **File DSN**.</span></span> <span data-ttu-id="4eb5d-118">Cliquez sur **Ajouter...**.</span><span class="sxs-lookup"><span data-stu-id="4eb5d-118">Click **Add...**.</span></span>  
   <span data-ttu-id="4eb5d-119">![ODBC1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc1.png)</span><span class="sxs-lookup"><span data-stu-id="4eb5d-119">![ODBC1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc1.png)</span></span>
3. <span data-ttu-id="4eb5d-120">Hello out-of-box pilote fonctionne fine, par conséquent, sélectionnez-le, puis cliquez sur **suivante >**.</span><span class="sxs-lookup"><span data-stu-id="4eb5d-120">hello out-of-box driver works fine, so select it and click **Next>**.</span></span>  
   <span data-ttu-id="4eb5d-121">![ODBC2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc2.png)</span><span class="sxs-lookup"><span data-stu-id="4eb5d-121">![ODBC2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc2.png)</span></span>
4. <span data-ttu-id="4eb5d-122">Nommez le fichier de hello, tel que **GenericSQL**.</span><span class="sxs-lookup"><span data-stu-id="4eb5d-122">Give hello file a name, such as **GenericSQL**.</span></span>  
   <span data-ttu-id="4eb5d-123">![ODBC3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc3.png)</span><span class="sxs-lookup"><span data-stu-id="4eb5d-123">![ODBC3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc3.png)</span></span>
5. <span data-ttu-id="4eb5d-124">Cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="4eb5d-124">Click **Finish**.</span></span>  
   <span data-ttu-id="4eb5d-125">![ODBC4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc4.png)</span><span class="sxs-lookup"><span data-stu-id="4eb5d-125">![ODBC4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc4.png)</span></span>
6. <span data-ttu-id="4eb5d-126">Connexion au moment tooconfigure hello.</span><span class="sxs-lookup"><span data-stu-id="4eb5d-126">Time tooconfigure hello connection.</span></span> <span data-ttu-id="4eb5d-127">Donner de source de données hello une bonne description et fournir le nom hello du serveur hello exécutant SQL Server.</span><span class="sxs-lookup"><span data-stu-id="4eb5d-127">Give hello data source a good description and provide hello name of hello server running SQL Server.</span></span>  
   ![ODBC5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc5.png)
7. <span data-ttu-id="4eb5d-129">Sélectionnez la façon dont tooauthenticate avec SQL.</span><span class="sxs-lookup"><span data-stu-id="4eb5d-129">Select how tooauthenticate with SQL.</span></span> <span data-ttu-id="4eb5d-130">Dans ce cas, nous utilisons l’authentification Windows.</span><span class="sxs-lookup"><span data-stu-id="4eb5d-130">In this case, we use Windows Authentication.</span></span>  
   ![ODBC6](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc6.png)
8. <span data-ttu-id="4eb5d-132">Fournir le nom hello de base de données exemple hello **GSQLDEMO**.</span><span class="sxs-lookup"><span data-stu-id="4eb5d-132">Provide hello name of hello sample database, **GSQLDEMO**.</span></span>  
   <span data-ttu-id="4eb5d-133">![ODBC7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc7.png)</span><span class="sxs-lookup"><span data-stu-id="4eb5d-133">![ODBC7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc7.png)</span></span>
9. <span data-ttu-id="4eb5d-134">Conservez toutes les valeurs par défaut sur cet écran.</span><span class="sxs-lookup"><span data-stu-id="4eb5d-134">Keep everything default on this screen.</span></span> <span data-ttu-id="4eb5d-135">Cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="4eb5d-135">Click **Finish**.</span></span>  
   <span data-ttu-id="4eb5d-136">![ODBC8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc8.png)</span><span class="sxs-lookup"><span data-stu-id="4eb5d-136">![ODBC8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc8.png)</span></span>
10. <span data-ttu-id="4eb5d-137">tooverify que tout fonctionne comme prévu, cliquez sur **Source de données de Test**.</span><span class="sxs-lookup"><span data-stu-id="4eb5d-137">tooverify everything is working as expected, click **Test Data Source**.</span></span>  
    <span data-ttu-id="4eb5d-138">![ODBC9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc9.png)</span><span class="sxs-lookup"><span data-stu-id="4eb5d-138">![ODBC9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc9.png)</span></span>
11. <span data-ttu-id="4eb5d-139">Vérifiez que hello test est réussi.</span><span class="sxs-lookup"><span data-stu-id="4eb5d-139">Make sure hello test is successful.</span></span>  
    ![ODBC10](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc10.png)
12. <span data-ttu-id="4eb5d-141">fichier de configuration Hello ODBC doit maintenant être visible dans le fichier DSN.</span><span class="sxs-lookup"><span data-stu-id="4eb5d-141">hello ODBC configuration file should now be visible in File DSN.</span></span>  
    ![ODBC11](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc11.png)

<span data-ttu-id="4eb5d-143">Nous disposons de fichier hello vous avez besoin et que vous pouvez commencer à créer hello connecteur.</span><span class="sxs-lookup"><span data-stu-id="4eb5d-143">We now have hello file we need and can start creating hello Connector.</span></span>

## <a name="create-hello-generic-sql-connector"></a><span data-ttu-id="4eb5d-144">Créer hello connecteur SQL générique</span><span class="sxs-lookup"><span data-stu-id="4eb5d-144">Create hello Generic SQL Connector</span></span>
1. <span data-ttu-id="4eb5d-145">Dans le Gestionnaire de Service de synchronisation UI de hello, sélectionnez **connecteurs** et **créer**.</span><span class="sxs-lookup"><span data-stu-id="4eb5d-145">In hello Synchronization Service Manager UI, select **Connectors** and **Create**.</span></span> <span data-ttu-id="4eb5d-146">Sélectionnez **SQL générique (Microsoft)** et donnez-lui un nom descriptif.</span><span class="sxs-lookup"><span data-stu-id="4eb5d-146">Select **Generic SQL (Microsoft)** and give it a descriptive name.</span></span>  
   <span data-ttu-id="4eb5d-147">![Connecteur1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector1.png)</span><span class="sxs-lookup"><span data-stu-id="4eb5d-147">![Connector1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector1.png)</span></span>
2. <span data-ttu-id="4eb5d-148">Trouver le fichier de source de données hello que vous avez créé dans la section précédente de hello et téléchargez-le toohello server.</span><span class="sxs-lookup"><span data-stu-id="4eb5d-148">Find hello DSN file you created in hello previous section and upload it toohello server.</span></span> <span data-ttu-id="4eb5d-149">Fournir de base de données toohello tooconnect des informations d’identification hello.</span><span class="sxs-lookup"><span data-stu-id="4eb5d-149">Provide hello credentials tooconnect toohello database.</span></span>  
   ![Connecteur2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector2.png)
3. <span data-ttu-id="4eb5d-151">Pour simplifier cette procédure pas à pas, disons qu’il existe deux types d’objet : **Utilisateur** et **Groupe**.</span><span class="sxs-lookup"><span data-stu-id="4eb5d-151">In this walkthrough, we are making it easy for us and say that there are two object types, **User** and **Group**.</span></span>
   <span data-ttu-id="4eb5d-152">![Connecteur3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector3.png)</span><span class="sxs-lookup"><span data-stu-id="4eb5d-152">![Connector3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector3.png)</span></span>
4. <span data-ttu-id="4eb5d-153">attributs de hello toofind, nous souhaitons hello connecteur toodetect ces attributs en examinant la table hello elle-même.</span><span class="sxs-lookup"><span data-stu-id="4eb5d-153">toofind hello attributes, we want hello Connector toodetect those attributes by looking at hello table itself.</span></span> <span data-ttu-id="4eb5d-154">Étant donné que **utilisateurs** est un mot réservé dans SQL, nous devons tooprovide dans le carré des crochets [].</span><span class="sxs-lookup"><span data-stu-id="4eb5d-154">Since **Users** is a reserved word in SQL, we need tooprovide it in square brackets [ ].</span></span>  
   <span data-ttu-id="4eb5d-155">![Connecteur4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector4.png)</span><span class="sxs-lookup"><span data-stu-id="4eb5d-155">![Connector4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector4.png)</span></span>
5. <span data-ttu-id="4eb5d-156">Attribut d’ancrage temps toodefine hello et attribut DN de hello.</span><span class="sxs-lookup"><span data-stu-id="4eb5d-156">Time toodefine hello anchor attribute and hello DN attribute.</span></span> <span data-ttu-id="4eb5d-157">Pour **utilisateurs**, nous utilisons la combinaison de hello de hello deux attributs username et EmployeeID.</span><span class="sxs-lookup"><span data-stu-id="4eb5d-157">For **Users**, we use hello combination of hello two attributes username and EmployeeID.</span></span> <span data-ttu-id="4eb5d-158">Pour **Groupe**, nous utilisons GroupName (rappelons qu’il ne s’agit ici que d’un exemple).</span><span class="sxs-lookup"><span data-stu-id="4eb5d-158">For **group**, we use GroupName (not realistic in real-life, but for this walkthrough it works).</span></span>
   <span data-ttu-id="4eb5d-159">![Connecteur5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector5.png)</span><span class="sxs-lookup"><span data-stu-id="4eb5d-159">![Connector5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector5.png)</span></span>
6. <span data-ttu-id="4eb5d-160">Tous les types d’attribut ne peuvent pas être détectés dans une base de données SQL,</span><span class="sxs-lookup"><span data-stu-id="4eb5d-160">Not all attribute types can be detected in a SQL database.</span></span> <span data-ttu-id="4eb5d-161">type d’attribut de référence de Hello en particulier ne peut pas.</span><span class="sxs-lookup"><span data-stu-id="4eb5d-161">hello reference attribute type in particular cannot.</span></span> <span data-ttu-id="4eb5d-162">Pour le type d’objet groupe de hello, nous devons toochange hello OwnerID et MemberID tooreference.</span><span class="sxs-lookup"><span data-stu-id="4eb5d-162">For hello group object type, we need toochange hello OwnerID and MemberID tooreference.</span></span>  
   ![Connecteur6](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector6.png)
7. <span data-ttu-id="4eb5d-164">attributs de Hello que nous avons sélectionné comme attributs de référence à l’étape précédente de hello nécessitent le type d’objet hello à que ces valeurs sont une référence.</span><span class="sxs-lookup"><span data-stu-id="4eb5d-164">hello attributes we selected as reference attributes in hello previous step require hello object type these values are a reference to.</span></span> <span data-ttu-id="4eb5d-165">Dans notre cas, hello type d’objet utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4eb5d-165">In our case, hello User object type.</span></span>  
   ![Connecteur7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector7.png)
8. <span data-ttu-id="4eb5d-167">Sur la page de paramètres globaux de hello, sélectionnez **filigrane** en tant que stratégie de delta hello.</span><span class="sxs-lookup"><span data-stu-id="4eb5d-167">On hello Global Parameters page, select **Watermark** as hello delta strategy.</span></span> <span data-ttu-id="4eb5d-168">Tapez également dans le format de date/heure hello **AAAA-MM-JJ HH : mm :**.</span><span class="sxs-lookup"><span data-stu-id="4eb5d-168">Also type in hello date/time format **yyyy-MM-dd HH:mm:ss**.</span></span>
   <span data-ttu-id="4eb5d-169">![Connecteur8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector8.png)</span><span class="sxs-lookup"><span data-stu-id="4eb5d-169">![Connector8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector8.png)</span></span>
9. <span data-ttu-id="4eb5d-170">Sur hello **configurer des Partitions et des hiérarchies** , sélectionnez les deux types d’objets.</span><span class="sxs-lookup"><span data-stu-id="4eb5d-170">On hello **Configure Partitions and Hierarchies** page, select both object types.</span></span>
   <span data-ttu-id="4eb5d-171">![Connecteur9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector9.png)</span><span class="sxs-lookup"><span data-stu-id="4eb5d-171">![Connector9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector9.png)</span></span>
10. <span data-ttu-id="4eb5d-172">Sur hello **sélectionner les Types d’objet** et **sélectionner les attributs**, sélectionnez les types d’objet et tous les attributs.</span><span class="sxs-lookup"><span data-stu-id="4eb5d-172">On hello **Select Object Types** and **Select Attributes**, select both object types and all attributes.</span></span> <span data-ttu-id="4eb5d-173">Sur hello **configurer des points d’ancrage** , cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="4eb5d-173">On hello **Configure Anchors** page, click **Finish**.</span></span>

## <a name="create-run-profiles"></a><span data-ttu-id="4eb5d-174">Créer les profils d’exécution</span><span class="sxs-lookup"><span data-stu-id="4eb5d-174">Create Run Profiles</span></span>
1. <span data-ttu-id="4eb5d-175">Dans le Gestionnaire de Service de synchronisation UI de hello, sélectionnez **connecteurs**, et **configurer des profils d’exécution**.</span><span class="sxs-lookup"><span data-stu-id="4eb5d-175">In hello Synchronization Service Manager UI, select **Connectors**, and **Configure Run Profiles**.</span></span> <span data-ttu-id="4eb5d-176">Cliquez sur **Nouveau profil**.</span><span class="sxs-lookup"><span data-stu-id="4eb5d-176">Click **New Profile**.</span></span> <span data-ttu-id="4eb5d-177">Nous commençons par **Importation intégrale**.</span><span class="sxs-lookup"><span data-stu-id="4eb5d-177">We start with **Full Import**.</span></span>  
   <span data-ttu-id="4eb5d-178">![ProfilExecution1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile1.png)</span><span class="sxs-lookup"><span data-stu-id="4eb5d-178">![Runprofile1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile1.png)</span></span>
2. <span data-ttu-id="4eb5d-179">Sélectionnez le type de hello **importation intégrale (phase uniquement)**.</span><span class="sxs-lookup"><span data-stu-id="4eb5d-179">Select hello type **Full Import (Stage Only)**.</span></span>  
   <span data-ttu-id="4eb5d-180">![ProfilExecution2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile2.png)</span><span class="sxs-lookup"><span data-stu-id="4eb5d-180">![Runprofile2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile2.png)</span></span>
3. <span data-ttu-id="4eb5d-181">Sélectionnez la partition de hello **objet = utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="4eb5d-181">Select hello partition **OBJECT=User**.</span></span>  
   <span data-ttu-id="4eb5d-182">![ProfilExecution3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile3.png)</span><span class="sxs-lookup"><span data-stu-id="4eb5d-182">![Runprofile3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile3.png)</span></span>
4. <span data-ttu-id="4eb5d-183">Sélectionnez **Table** et tapez **[USERS]**.</span><span class="sxs-lookup"><span data-stu-id="4eb5d-183">Select **Table** and type **[USERS]**.</span></span> <span data-ttu-id="4eb5d-184">Défiler vers le bas la section de type d’objet à valeurs multiples toohello et entrer des données hello comme hello illustration suivante.</span><span class="sxs-lookup"><span data-stu-id="4eb5d-184">Scroll down toohello multi-valued object type section and enter hello data as in hello following picture.</span></span> <span data-ttu-id="4eb5d-185">Sélectionnez **Terminer** étape de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="4eb5d-185">Select **Finish** toosave hello step.</span></span>  
   <span data-ttu-id="4eb5d-186">![ProfilExecution4a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4a.png)</span><span class="sxs-lookup"><span data-stu-id="4eb5d-186">![Runprofile4a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4a.png)</span></span>  
   <span data-ttu-id="4eb5d-187">![ProfilExecution4b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4b.png)</span><span class="sxs-lookup"><span data-stu-id="4eb5d-187">![Runprofile4b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4b.png)</span></span>  
5. <span data-ttu-id="4eb5d-188">Sélectionnez **Nouvelle étape**.</span><span class="sxs-lookup"><span data-stu-id="4eb5d-188">Select **New Step**.</span></span> <span data-ttu-id="4eb5d-189">Cette fois, sélectionnez **OBJECT=Group**.</span><span class="sxs-lookup"><span data-stu-id="4eb5d-189">This time, select **OBJECT=Group**.</span></span> <span data-ttu-id="4eb5d-190">Sur la dernière page de hello, utilisez la configuration hello comme hello illustration suivante.</span><span class="sxs-lookup"><span data-stu-id="4eb5d-190">On hello last page, use hello configuration as in hello following picture.</span></span> <span data-ttu-id="4eb5d-191">Cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="4eb5d-191">Click **Finish**.</span></span>  
   <span data-ttu-id="4eb5d-192">![ProfilExecution5a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5a.png)</span><span class="sxs-lookup"><span data-stu-id="4eb5d-192">![Runprofile5a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5a.png)</span></span>  
   <span data-ttu-id="4eb5d-193">![ProfilExecution5b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5b.png)</span><span class="sxs-lookup"><span data-stu-id="4eb5d-193">![Runprofile5b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5b.png)</span></span>  
6. <span data-ttu-id="4eb5d-194">Facultatif : si vous le souhaitez, vous pouvez configurer des profils d’exécution supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="4eb5d-194">Optional: If you want to, you can configure additional run profiles.</span></span> <span data-ttu-id="4eb5d-195">Pour cette procédure pas à pas, uniquement hello importation intégrale est utilisé.</span><span class="sxs-lookup"><span data-stu-id="4eb5d-195">For this walkthrough, only hello Full Import is used.</span></span>
7. <span data-ttu-id="4eb5d-196">Cliquez sur **OK** toofinish modification de profils d’exécution.</span><span class="sxs-lookup"><span data-stu-id="4eb5d-196">Click **OK** toofinish changing run profiles.</span></span>

## <a name="add-some-test-data-and-test-hello-import"></a><span data-ttu-id="4eb5d-197">Ajouter des test d’importation hello données et de test</span><span class="sxs-lookup"><span data-stu-id="4eb5d-197">Add some test data and test hello import</span></span>
<span data-ttu-id="4eb5d-198">Remplissez quelques données de test dans votre exemple de base de données.</span><span class="sxs-lookup"><span data-stu-id="4eb5d-198">Fill out some test data in your sample database.</span></span> <span data-ttu-id="4eb5d-199">Lorsque vous êtes prêt, sélectionnez **Exécuter** et **Importation intégrale**.</span><span class="sxs-lookup"><span data-stu-id="4eb5d-199">When you are ready, select **Run** and **Full import**.</span></span>

<span data-ttu-id="4eb5d-200">Voici un utilisateur avec deux numéros de téléphone et un groupe avec quelques membres.</span><span class="sxs-lookup"><span data-stu-id="4eb5d-200">Here is a user with two phone numbers and a group with some members.</span></span>  
![cs1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/cs1.png)  
![cs2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/cs2.png)  

## <a name="appendix-a"></a><span data-ttu-id="4eb5d-203">Annexe A</span><span class="sxs-lookup"><span data-stu-id="4eb5d-203">Appendix A</span></span>
<span data-ttu-id="4eb5d-204">**Base de données SQL script toocreate hello exemple**</span><span class="sxs-lookup"><span data-stu-id="4eb5d-204">**SQL script toocreate hello sample database**</span></span>

```SQL
---Creating hello Database---------
Create Database GSQLDEMO
Go
-------Using hello Database-----------
Use [GSQLDEMO]
Go
-------------------------------------
USE [GSQLDEMO]
GO
/****** Object:  Table [dbo].[GroupMembers]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[GroupMembers](
    [MemberID] [int] NOT NULL,
    [Group_ID] [int] NOT NULL
) ON [PRIMARY]

GO
/****** Object:  Table [dbo].[GROUPS]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[GROUPS](
    [GroupID] [int] NOT NULL,
    [GROUPNAME] [nvarchar](200) NOT NULL,
    [DESCRIPTION] [nvarchar](200) NULL,
    [WATERMARK] [datetime] NULL,
    [OwnerID] [int] NULL,
PRIMARY KEY CLUSTERED
(
    [GroupID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]

GO
/****** Object:  Table [dbo].[USERPHONE]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
SET ANSI_PADDING ON
GO
CREATE TABLE [dbo].[USERPHONE](
    [USER_ID] [int] NULL,
    [Phone] [varchar](20) NULL
) ON [PRIMARY]

GO
SET ANSI_PADDING OFF
GO
/****** Object:  Table [dbo].[USERS]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[USERS](
    [USERID] [int] NOT NULL,
    [USERNAME] [nvarchar](200) NOT NULL,
    [FirstName] [nvarchar](100) NULL,
    [LastName] [nvarchar](100) NULL,
    [DisplayName] [nvarchar](100) NULL,
    [ACCOUNTDISABLED] [bit] NULL,
    [EMPLOYEEID] [int] NOT NULL,
    [WATERMARK] [datetime] NULL,
PRIMARY KEY CLUSTERED
(
    [USERID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]

GO
ALTER TABLE [dbo].[GroupMembers]  WITH CHECK ADD  CONSTRAINT [FK_GroupMembers_GROUPS] FOREIGN KEY([Group_ID])
REFERENCES [dbo].[GROUPS] ([GroupID])
GO
ALTER TABLE [dbo].[GroupMembers] CHECK CONSTRAINT [FK_GroupMembers_GROUPS]
GO
ALTER TABLE [dbo].[GroupMembers]  WITH CHECK ADD  CONSTRAINT [FK_GroupMembers_USERS] FOREIGN KEY([MemberID])
REFERENCES [dbo].[USERS] ([USERID])
GO
ALTER TABLE [dbo].[GroupMembers] CHECK CONSTRAINT [FK_GroupMembers_USERS]
GO
ALTER TABLE [dbo].[GROUPS]  WITH CHECK ADD  CONSTRAINT [FK_GROUPS_USERS] FOREIGN KEY([OwnerID])
REFERENCES [dbo].[USERS] ([USERID])
GO
ALTER TABLE [dbo].[GROUPS] CHECK CONSTRAINT [FK_GROUPS_USERS]
GO
ALTER TABLE [dbo].[USERPHONE]  WITH CHECK ADD  CONSTRAINT [FK_USERPHONE_USER] FOREIGN KEY([USER_ID])
REFERENCES [dbo].[USERS] ([USERID])
GO
ALTER TABLE [dbo].[USERPHONE] CHECK CONSTRAINT [FK_USERPHONE_USER]
GO
```
