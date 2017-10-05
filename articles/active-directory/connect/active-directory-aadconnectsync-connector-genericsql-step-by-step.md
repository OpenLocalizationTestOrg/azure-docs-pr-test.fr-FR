---
title: "Connecteur SQL générique - Guide pas à pas | Microsoft Docs"
description: "Cet article vous guide dans une procédure pas à pas pour créer un simple système de base de données Ressources humaines à l’aide du connecteur SQL générique."
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
ms.openlocfilehash: 3fdc1b405b95180d031aa4ad45b406f7fc149d8f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="generic-sql-connector-step-by-step"></a><span data-ttu-id="6a67f-103">Connecteur SQL générique - Guide pas à pas</span><span class="sxs-lookup"><span data-stu-id="6a67f-103">Generic SQL Connector step-by-step</span></span>
<span data-ttu-id="6a67f-104">Cette rubrique est un guide pas à pas.</span><span class="sxs-lookup"><span data-stu-id="6a67f-104">This topic is a step-by-step guide.</span></span> <span data-ttu-id="6a67f-105">Elle explique comment créer un simple exemple de base de données Ressources humaines et l’utiliser pour importer certains utilisateurs et leur appartenance à un groupe.</span><span class="sxs-lookup"><span data-stu-id="6a67f-105">It creates a simple sample HR database and use it for importing some users and their group membership.</span></span>

## <a name="prepare-the-sample-database"></a><span data-ttu-id="6a67f-106">Préparer l’exemple de base de données</span><span class="sxs-lookup"><span data-stu-id="6a67f-106">Prepare the sample database</span></span>
<span data-ttu-id="6a67f-107">Sur un serveur exécutant SQL Server, exécutez le script SQL disponible dans [l’Annexe A](#appendix-a). Un exemple de base de données portant le nom GSQLDEMO est créé.</span><span class="sxs-lookup"><span data-stu-id="6a67f-107">On a server running SQL Server, run the SQL script found in [Appendix A](#appendix-a). This script creates a sample database with the name GSQLDEMO.</span></span> <span data-ttu-id="6a67f-108">Le modèle objet pour la base de données créée a l’aspect suivant : </span><span class="sxs-lookup"><span data-stu-id="6a67f-108">The object model for the created database looks like this picture:</span></span>  
<span data-ttu-id="6a67f-109">![Modèle objet](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/objectmodel.png)</span><span class="sxs-lookup"><span data-stu-id="6a67f-109">![Object Model](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/objectmodel.png)</span></span>

<span data-ttu-id="6a67f-110">Créez également l’utilisateur que vous souhaitez utiliser pour vous connecter à la base de données.</span><span class="sxs-lookup"><span data-stu-id="6a67f-110">Also create a user you want to use to connect to the database.</span></span> <span data-ttu-id="6a67f-111">Dans cette procédure pas à pas, l’utilisateur est appelé FABRIKAM\SQLUser et il est situé dans le domaine.</span><span class="sxs-lookup"><span data-stu-id="6a67f-111">In this walkthrough, the user is called FABRIKAM\SQLUser and located in the domain.</span></span>

## <a name="create-the-odbc-connection-file"></a><span data-ttu-id="6a67f-112">Créer le fichier de connexion ODBC</span><span class="sxs-lookup"><span data-stu-id="6a67f-112">Create the ODBC connection file</span></span>
<span data-ttu-id="6a67f-113">Le connecteur SQL générique utilise ODBC pour se connecter au serveur distant.</span><span class="sxs-lookup"><span data-stu-id="6a67f-113">The Generic SQL Connector is using ODBC to connect to the remote server.</span></span> <span data-ttu-id="6a67f-114">Nous devons tout d’abord créer un fichier avec les informations de connexion ODBC.</span><span class="sxs-lookup"><span data-stu-id="6a67f-114">First we need to create a file with the ODBC connection information.</span></span>

1. <span data-ttu-id="6a67f-115">Démarrez l’utilitaire de gestion ODBC sur votre serveur : </span><span class="sxs-lookup"><span data-stu-id="6a67f-115">Start the ODBC management utility on your server:</span></span>  
   ![ODBC](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc.png)
2. <span data-ttu-id="6a67f-117">Sélectionnez l’onglet **Fichier DSN**.</span><span class="sxs-lookup"><span data-stu-id="6a67f-117">Select the tab **File DSN**.</span></span> <span data-ttu-id="6a67f-118">Cliquez sur **Ajouter...**.</span><span class="sxs-lookup"><span data-stu-id="6a67f-118">Click **Add...**.</span></span>  
   <span data-ttu-id="6a67f-119">![ODBC1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc1.png)</span><span class="sxs-lookup"><span data-stu-id="6a67f-119">![ODBC1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc1.png)</span></span>
3. <span data-ttu-id="6a67f-120">Le pilote prêt à l’emploi fonctionne parfaitement. Par conséquent, sélectionnez-le, puis cliquez sur **Suivant>**.</span><span class="sxs-lookup"><span data-stu-id="6a67f-120">The out-of-box driver works fine, so select it and click **Next>**.</span></span>  
   <span data-ttu-id="6a67f-121">![ODBC2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc2.png)</span><span class="sxs-lookup"><span data-stu-id="6a67f-121">![ODBC2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc2.png)</span></span>
4. <span data-ttu-id="6a67f-122">Nommez le fichier, par exemple **GenericSQL**.</span><span class="sxs-lookup"><span data-stu-id="6a67f-122">Give the file a name, such as **GenericSQL**.</span></span>  
   <span data-ttu-id="6a67f-123">![ODBC3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc3.png)</span><span class="sxs-lookup"><span data-stu-id="6a67f-123">![ODBC3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc3.png)</span></span>
5. <span data-ttu-id="6a67f-124">Cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="6a67f-124">Click **Finish**.</span></span>  
   <span data-ttu-id="6a67f-125">![ODBC4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc4.png)</span><span class="sxs-lookup"><span data-stu-id="6a67f-125">![ODBC4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc4.png)</span></span>
6. <span data-ttu-id="6a67f-126">Il est temps de configurer la connexion.</span><span class="sxs-lookup"><span data-stu-id="6a67f-126">Time to configure the connection.</span></span> <span data-ttu-id="6a67f-127">Décrivez la source de données et fournissez le nom du serveur exécutant SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6a67f-127">Give the data source a good description and provide the name of the server running SQL Server.</span></span>  
   ![ODBC5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc5.png)
7. <span data-ttu-id="6a67f-129">Sélectionnez le mode d’authentification avec SQL.</span><span class="sxs-lookup"><span data-stu-id="6a67f-129">Select how to authenticate with SQL.</span></span> <span data-ttu-id="6a67f-130">Dans ce cas, nous utilisons l’authentification Windows.</span><span class="sxs-lookup"><span data-stu-id="6a67f-130">In this case, we use Windows Authentication.</span></span>  
   ![ODBC6](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc6.png)
8. <span data-ttu-id="6a67f-132">Indiquez le nom de l’exemple de base de données **GSQLDEMO**.</span><span class="sxs-lookup"><span data-stu-id="6a67f-132">Provide the name of the sample database, **GSQLDEMO**.</span></span>  
   <span data-ttu-id="6a67f-133">![ODBC7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc7.png)</span><span class="sxs-lookup"><span data-stu-id="6a67f-133">![ODBC7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc7.png)</span></span>
9. <span data-ttu-id="6a67f-134">Conservez toutes les valeurs par défaut sur cet écran.</span><span class="sxs-lookup"><span data-stu-id="6a67f-134">Keep everything default on this screen.</span></span> <span data-ttu-id="6a67f-135">Cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="6a67f-135">Click **Finish**.</span></span>  
   <span data-ttu-id="6a67f-136">![ODBC8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc8.png)</span><span class="sxs-lookup"><span data-stu-id="6a67f-136">![ODBC8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc8.png)</span></span>
10. <span data-ttu-id="6a67f-137">Pour vérifier que tout fonctionne comme prévu, cliquez sur **Tester la source de données**.</span><span class="sxs-lookup"><span data-stu-id="6a67f-137">To verify everything is working as expected, click **Test Data Source**.</span></span>  
    <span data-ttu-id="6a67f-138">![ODBC9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc9.png)</span><span class="sxs-lookup"><span data-stu-id="6a67f-138">![ODBC9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc9.png)</span></span>
11. <span data-ttu-id="6a67f-139">Vérifiez que le test a réussi.</span><span class="sxs-lookup"><span data-stu-id="6a67f-139">Make sure the test is successful.</span></span>  
    ![ODBC10](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc10.png)
12. <span data-ttu-id="6a67f-141">Le fichier de configuration ODBC doit maintenant être visible dans le fichier DSN.</span><span class="sxs-lookup"><span data-stu-id="6a67f-141">The ODBC configuration file should now be visible in File DSN.</span></span>  
    ![ODBC11](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc11.png)

<span data-ttu-id="6a67f-143">Nous avons maintenant le fichier dont nous avons besoin et pouvons commencer à créer le connecteur.</span><span class="sxs-lookup"><span data-stu-id="6a67f-143">We now have the file we need and can start creating the Connector.</span></span>

## <a name="create-the-generic-sql-connector"></a><span data-ttu-id="6a67f-144">Créer le connecteur SQL générique</span><span class="sxs-lookup"><span data-stu-id="6a67f-144">Create the Generic SQL Connector</span></span>
1. <span data-ttu-id="6a67f-145">Dans l’interface Synchronization Service Manager, cliquez sur **Connecteurs**, puis sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="6a67f-145">In the Synchronization Service Manager UI, select **Connectors** and **Create**.</span></span> <span data-ttu-id="6a67f-146">Sélectionnez **SQL générique (Microsoft)** et donnez-lui un nom descriptif.</span><span class="sxs-lookup"><span data-stu-id="6a67f-146">Select **Generic SQL (Microsoft)** and give it a descriptive name.</span></span>  
   <span data-ttu-id="6a67f-147">![Connecteur1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector1.png)</span><span class="sxs-lookup"><span data-stu-id="6a67f-147">![Connector1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector1.png)</span></span>
2. <span data-ttu-id="6a67f-148">Recherchez le fichier DSN que vous avez créé dans la section précédente et téléchargez-le sur le serveur.</span><span class="sxs-lookup"><span data-stu-id="6a67f-148">Find the DSN file you created in the previous section and upload it to the server.</span></span> <span data-ttu-id="6a67f-149">Entrez les informations de connexion à la base de données.</span><span class="sxs-lookup"><span data-stu-id="6a67f-149">Provide the credentials to connect to the database.</span></span>  
   ![Connecteur2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector2.png)
3. <span data-ttu-id="6a67f-151">Pour simplifier cette procédure pas à pas, disons qu’il existe deux types d’objet : **Utilisateur** et **Groupe**.</span><span class="sxs-lookup"><span data-stu-id="6a67f-151">In this walkthrough, we are making it easy for us and say that there are two object types, **User** and **Group**.</span></span>
   <span data-ttu-id="6a67f-152">![Connecteur3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector3.png)</span><span class="sxs-lookup"><span data-stu-id="6a67f-152">![Connector3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector3.png)</span></span>
4. <span data-ttu-id="6a67f-153">Pour rechercher les attributs, nous voulons que le connecteur les détecte en examinant la table elle-même.</span><span class="sxs-lookup"><span data-stu-id="6a67f-153">To find the attributes, we want the Connector to detect those attributes by looking at the table itself.</span></span> <span data-ttu-id="6a67f-154">Étant donné que **Utilisateurs** est un mot réservé dans SQL, nous devons l’indiquer entre crochets [ ].</span><span class="sxs-lookup"><span data-stu-id="6a67f-154">Since **Users** is a reserved word in SQL, we need to provide it in square brackets [ ].</span></span>  
   <span data-ttu-id="6a67f-155">![Connecteur4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector4.png)</span><span class="sxs-lookup"><span data-stu-id="6a67f-155">![Connector4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector4.png)</span></span>
5. <span data-ttu-id="6a67f-156">Il est temps de définir l’attribut d’ancrage et l’attribut de nom de domaine.</span><span class="sxs-lookup"><span data-stu-id="6a67f-156">Time to define the anchor attribute and the DN attribute.</span></span> <span data-ttu-id="6a67f-157">Pour **Utilisateurs**, nous utilisons la combinaison des deux attributs username et EmployeeID.</span><span class="sxs-lookup"><span data-stu-id="6a67f-157">For **Users**, we use the combination of the two attributes username and EmployeeID.</span></span> <span data-ttu-id="6a67f-158">Pour **Groupe**, nous utilisons GroupName (rappelons qu’il ne s’agit ici que d’un exemple).</span><span class="sxs-lookup"><span data-stu-id="6a67f-158">For **group**, we use GroupName (not realistic in real-life, but for this walkthrough it works).</span></span>
   <span data-ttu-id="6a67f-159">![Connecteur5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector5.png)</span><span class="sxs-lookup"><span data-stu-id="6a67f-159">![Connector5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector5.png)</span></span>
6. <span data-ttu-id="6a67f-160">Tous les types d’attribut ne peuvent pas être détectés dans une base de données SQL,</span><span class="sxs-lookup"><span data-stu-id="6a67f-160">Not all attribute types can be detected in a SQL database.</span></span> <span data-ttu-id="6a67f-161">le type d’attribut de référence en particulier.</span><span class="sxs-lookup"><span data-stu-id="6a67f-161">The reference attribute type in particular cannot.</span></span> <span data-ttu-id="6a67f-162">Pour le type d’objet de groupe, nous devons modifier OwnerID et MemberID en attributs de référence.</span><span class="sxs-lookup"><span data-stu-id="6a67f-162">For the group object type, we need to change the OwnerID and MemberID to reference.</span></span>  
   ![Connecteur6](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector6.png)
7. <span data-ttu-id="6a67f-164">Les attributs que nous avons sélectionnés en tant qu’attributs de référence à l’étape précédente nécessitent le type d’objet auquel ces valeurs font référence.</span><span class="sxs-lookup"><span data-stu-id="6a67f-164">The attributes we selected as reference attributes in the previous step require the object type these values are a reference to.</span></span> <span data-ttu-id="6a67f-165">Dans notre cas, il s’agit du type d’objet User.</span><span class="sxs-lookup"><span data-stu-id="6a67f-165">In our case, the User object type.</span></span>  
   ![Connecteur7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector7.png)
8. <span data-ttu-id="6a67f-167">Dans la page Paramètres généraux, sélectionnez **Filigrane** comme stratégie delta.</span><span class="sxs-lookup"><span data-stu-id="6a67f-167">On the Global Parameters page, select **Watermark** as the delta strategy.</span></span> <span data-ttu-id="6a67f-168">Entrez également le format de date/heure **yyyy-MM-dd HH:mm:ss**.</span><span class="sxs-lookup"><span data-stu-id="6a67f-168">Also type in the date/time format **yyyy-MM-dd HH:mm:ss**.</span></span>
   <span data-ttu-id="6a67f-169">![Connecteur8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector8.png)</span><span class="sxs-lookup"><span data-stu-id="6a67f-169">![Connector8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector8.png)</span></span>
9. <span data-ttu-id="6a67f-170">Dans la page **Configurer les partitions et hiérarchies** , sélectionnez les deux types d’objet.</span><span class="sxs-lookup"><span data-stu-id="6a67f-170">On the **Configure Partitions and Hierarchies** page, select both object types.</span></span>
   <span data-ttu-id="6a67f-171">![Connecteur9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector9.png)</span><span class="sxs-lookup"><span data-stu-id="6a67f-171">![Connector9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector9.png)</span></span>
10. <span data-ttu-id="6a67f-172">Dans **Sélectionner les types d’objet** et **Sélectionner les attributs**, sélectionnez les types d’objet et tous les attributs.</span><span class="sxs-lookup"><span data-stu-id="6a67f-172">On the **Select Object Types** and **Select Attributes**, select both object types and all attributes.</span></span> <span data-ttu-id="6a67f-173">Sur la page **Configurer les ancres**, cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="6a67f-173">On the **Configure Anchors** page, click **Finish**.</span></span>

## <a name="create-run-profiles"></a><span data-ttu-id="6a67f-174">Créer les profils d’exécution</span><span class="sxs-lookup"><span data-stu-id="6a67f-174">Create Run Profiles</span></span>
1. <span data-ttu-id="6a67f-175">Dans l’interface Synchronization Service Manager, cliquez sur **Connecteurs**, puis sur **Configurer les profils d’exécution**.</span><span class="sxs-lookup"><span data-stu-id="6a67f-175">In the Synchronization Service Manager UI, select **Connectors**, and **Configure Run Profiles**.</span></span> <span data-ttu-id="6a67f-176">Cliquez sur **Nouveau profil**.</span><span class="sxs-lookup"><span data-stu-id="6a67f-176">Click **New Profile**.</span></span> <span data-ttu-id="6a67f-177">Nous commençons par **Importation intégrale**.</span><span class="sxs-lookup"><span data-stu-id="6a67f-177">We start with **Full Import**.</span></span>  
   <span data-ttu-id="6a67f-178">![ProfilExecution1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile1.png)</span><span class="sxs-lookup"><span data-stu-id="6a67f-178">![Runprofile1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile1.png)</span></span>
2. <span data-ttu-id="6a67f-179">Sélectionnez le type **Importation intégrale (intermédiaire uniquement)**.</span><span class="sxs-lookup"><span data-stu-id="6a67f-179">Select the type **Full Import (Stage Only)**.</span></span>  
   <span data-ttu-id="6a67f-180">![ProfilExecution2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile2.png)</span><span class="sxs-lookup"><span data-stu-id="6a67f-180">![Runprofile2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile2.png)</span></span>
3. <span data-ttu-id="6a67f-181">Sélectionnez la partition **OBJECT=User**.</span><span class="sxs-lookup"><span data-stu-id="6a67f-181">Select the partition **OBJECT=User**.</span></span>  
   <span data-ttu-id="6a67f-182">![ProfilExecution3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile3.png)</span><span class="sxs-lookup"><span data-stu-id="6a67f-182">![Runprofile3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile3.png)</span></span>
4. <span data-ttu-id="6a67f-183">Sélectionnez **Table** et tapez **[USERS]**.</span><span class="sxs-lookup"><span data-stu-id="6a67f-183">Select **Table** and type **[USERS]**.</span></span> <span data-ttu-id="6a67f-184">Faites défiler jusqu’à la section de type d’objet à valeurs multiples et entrez les données tel qu’indiqué dans l’image suivante.</span><span class="sxs-lookup"><span data-stu-id="6a67f-184">Scroll down to the multi-valued object type section and enter the data as in the following picture.</span></span> <span data-ttu-id="6a67f-185">Sélectionnez **Terminer** pour enregistrer l’étape.</span><span class="sxs-lookup"><span data-stu-id="6a67f-185">Select **Finish** to save the step.</span></span>  
   <span data-ttu-id="6a67f-186">![ProfilExecution4a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4a.png)</span><span class="sxs-lookup"><span data-stu-id="6a67f-186">![Runprofile4a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4a.png)</span></span>  
   <span data-ttu-id="6a67f-187">![ProfilExecution4b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4b.png)</span><span class="sxs-lookup"><span data-stu-id="6a67f-187">![Runprofile4b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4b.png)</span></span>  
5. <span data-ttu-id="6a67f-188">Sélectionnez **Nouvelle étape**.</span><span class="sxs-lookup"><span data-stu-id="6a67f-188">Select **New Step**.</span></span> <span data-ttu-id="6a67f-189">Cette fois, sélectionnez **OBJECT=Group**.</span><span class="sxs-lookup"><span data-stu-id="6a67f-189">This time, select **OBJECT=Group**.</span></span> <span data-ttu-id="6a67f-190">Sur la dernière page, utilisez la configuration indiquée dans l’image suivante.</span><span class="sxs-lookup"><span data-stu-id="6a67f-190">On the last page, use the configuration as in the following picture.</span></span> <span data-ttu-id="6a67f-191">Cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="6a67f-191">Click **Finish**.</span></span>  
   <span data-ttu-id="6a67f-192">![ProfilExecution5a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5a.png)</span><span class="sxs-lookup"><span data-stu-id="6a67f-192">![Runprofile5a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5a.png)</span></span>  
   <span data-ttu-id="6a67f-193">![ProfilExecution5b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5b.png)</span><span class="sxs-lookup"><span data-stu-id="6a67f-193">![Runprofile5b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5b.png)</span></span>  
6. <span data-ttu-id="6a67f-194">Facultatif : si vous le souhaitez, vous pouvez configurer des profils d’exécution supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="6a67f-194">Optional: If you want to, you can configure additional run profiles.</span></span> <span data-ttu-id="6a67f-195">Pour cette procédure pas à pas, seule l’importation intégrale est utilisée.</span><span class="sxs-lookup"><span data-stu-id="6a67f-195">For this walkthrough, only the Full Import is used.</span></span>
7. <span data-ttu-id="6a67f-196">Cliquez sur **OK** pour terminer de modifier les profils d’exécution.</span><span class="sxs-lookup"><span data-stu-id="6a67f-196">Click **OK** to finish changing run profiles.</span></span>

## <a name="add-some-test-data-and-test-the-import"></a><span data-ttu-id="6a67f-197">Ajouter quelques données de test et tester l’importation</span><span class="sxs-lookup"><span data-stu-id="6a67f-197">Add some test data and test the import</span></span>
<span data-ttu-id="6a67f-198">Remplissez quelques données de test dans votre exemple de base de données.</span><span class="sxs-lookup"><span data-stu-id="6a67f-198">Fill out some test data in your sample database.</span></span> <span data-ttu-id="6a67f-199">Lorsque vous êtes prêt, sélectionnez **Exécuter** et **Importation intégrale**.</span><span class="sxs-lookup"><span data-stu-id="6a67f-199">When you are ready, select **Run** and **Full import**.</span></span>

<span data-ttu-id="6a67f-200">Voici un utilisateur avec deux numéros de téléphone et un groupe avec quelques membres.</span><span class="sxs-lookup"><span data-stu-id="6a67f-200">Here is a user with two phone numbers and a group with some members.</span></span>  
![cs1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/cs1.png)  
![cs2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/cs2.png)  

## <a name="appendix-a"></a><span data-ttu-id="6a67f-203">Annexe A</span><span class="sxs-lookup"><span data-stu-id="6a67f-203">Appendix A</span></span>
<span data-ttu-id="6a67f-204">**Script SQL pour créer l’exemple de base de données**</span><span class="sxs-lookup"><span data-stu-id="6a67f-204">**SQL script to create the sample database**</span></span>

```SQL
---Creating the Database---------
Create Database GSQLDEMO
Go
-------Using the Database-----------
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
