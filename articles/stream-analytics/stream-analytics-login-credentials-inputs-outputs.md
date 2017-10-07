---
title: "Stream Analytics : inverser les informations d'identification de connexion pour les entrées et sorties | Microsoft Docs"
description: "Découvrez comment tooupdate hello les informations d’identification pour les sorties et les entrées de flux de données Analytique."
keywords: "informations d’identification"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 42ae83e1-cd33-49bb-a455-a39a7c151ea4
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: ac2374c539012b66ab390656c5750024e02f6bdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="rotate-login-credentials-for-inputs-and-outputs-in-stream-analytics-jobs"></a><span data-ttu-id="2744b-104">Rotation des informations d'identification pour les entrées et les sorties dans des travaux Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="2744b-104">Rotate login credentials for inputs and outputs in Stream Analytics Jobs</span></span>
## <a name="abstract"></a><span data-ttu-id="2744b-105">Résumé</span><span class="sxs-lookup"><span data-stu-id="2744b-105">Abstract</span></span>
<span data-ttu-id="2744b-106">Analytique de flux de données Azure aujourd'hui n’autorise pas remplacer les informations d’identification hello sur une entrée/sortie pendant l’exécution du travail de hello.</span><span class="sxs-lookup"><span data-stu-id="2744b-106">Azure Stream Analytics today doesn’t allow replacing hello credentials on an input/output while hello job is running.</span></span>

<span data-ttu-id="2744b-107">Analytique de flux de données Azure ne prend pas en charge la reprise d’une tâche à partir de la dernière sortie, nous voulions processus tooshare hello pour minimiser le retard hello entre hello l’arrêt et démarrage du travail de hello et faire pivoter les informations d’identification de connexion hello.</span><span class="sxs-lookup"><span data-stu-id="2744b-107">While Azure Stream Analytics does support resuming a job from last output, we wanted tooshare hello entire process for minimizing hello lag between hello stopping and starting of hello job and rotating hello login credentials.</span></span>

## <a name="part-1---prepare-hello-new-set-of-credentials"></a><span data-ttu-id="2744b-108">Partie 1 : préparer les hello nouvel ensemble d’informations d’identification :</span><span class="sxs-lookup"><span data-stu-id="2744b-108">Part 1 - Prepare hello new set of credentials:</span></span>
<span data-ttu-id="2744b-109">Cette partie est applicable toohello suivant des entrées/sorties :</span><span class="sxs-lookup"><span data-stu-id="2744b-109">This part is applicable toohello following inputs/outputs:</span></span>

* <span data-ttu-id="2744b-110">Stockage d’objets blob</span><span class="sxs-lookup"><span data-stu-id="2744b-110">Blob Storage</span></span>
* <span data-ttu-id="2744b-111">Hubs d'événements</span><span class="sxs-lookup"><span data-stu-id="2744b-111">Event Hubs</span></span>
* <span data-ttu-id="2744b-112">Base de données SQL</span><span class="sxs-lookup"><span data-stu-id="2744b-112">SQL Database</span></span>
* <span data-ttu-id="2744b-113">Stockage de tables</span><span class="sxs-lookup"><span data-stu-id="2744b-113">Table Storage</span></span>

<span data-ttu-id="2744b-114">Pour les autres entrées/sorties, passez à la partie 2.</span><span class="sxs-lookup"><span data-stu-id="2744b-114">For other inputs/outputs, proceed with Part 2.</span></span>

### <a name="blob-storagetable-storage"></a><span data-ttu-id="2744b-115">Stockage d’objets blob/de tables</span><span class="sxs-lookup"><span data-stu-id="2744b-115">Blob storage/Table storage</span></span>
1. <span data-ttu-id="2744b-116">Consulter l’extension du stockage toohello le portail de gestion Azure hello :</span><span class="sxs-lookup"><span data-stu-id="2744b-116">Go toohello Storage extention on hello Azure Management portal:</span></span>  
   ![graphic1][graphic1]
2. <span data-ttu-id="2744b-118">Recherchez stockage hello utilisé par votre travail et allez dans celui-ci :</span><span class="sxs-lookup"><span data-stu-id="2744b-118">Locate hello storage used by your job and go into it:</span></span>  
   ![graphic2][graphic2]
3. <span data-ttu-id="2744b-120">Cliquez sur commande de gérer les clés d’accès hello :</span><span class="sxs-lookup"><span data-stu-id="2744b-120">Click hello Manage Access Keys command:</span></span>  
   ![graphic3][graphic3]
4. <span data-ttu-id="2744b-122">Entre hello clé d’accès primaire et hello clé d’accès secondaire, **pick hello ne pas utilisé par votre travail**.</span><span class="sxs-lookup"><span data-stu-id="2744b-122">Between hello Primary Access Key and hello Secondary Access Key, **pick hello one not used by your job**.</span></span>
5. <span data-ttu-id="2744b-123">Appuyez sur Régénérer : </span><span class="sxs-lookup"><span data-stu-id="2744b-123">Hit regenerate:</span></span>  
   ![graphic4][graphic4]
6. <span data-ttu-id="2744b-125">Copiez la clé de hello qui vient d’être généré :</span><span class="sxs-lookup"><span data-stu-id="2744b-125">Copy hello newly generated key:</span></span>  
   ![graphic5][graphic5]
7. <span data-ttu-id="2744b-127">Continuer tooPart 2.</span><span class="sxs-lookup"><span data-stu-id="2744b-127">Continue tooPart 2.</span></span>

### <a name="event-hubs"></a><span data-ttu-id="2744b-128">Hubs d'événements</span><span class="sxs-lookup"><span data-stu-id="2744b-128">Event hubs</span></span>
1. <span data-ttu-id="2744b-129">Atteindre l’extension de Service Bus toohello sur le portail de gestion Azure hello :</span><span class="sxs-lookup"><span data-stu-id="2744b-129">Go toohello Service Bus extension on hello Azure Management portal:</span></span>  
   ![graphic6][graphic6]
2. <span data-ttu-id="2744b-131">Recherchez hello Namespace de Bus de Service utilisé par votre tâche et allez dans celui-ci :</span><span class="sxs-lookup"><span data-stu-id="2744b-131">Locate hello Service Bus Namespace used by your job and go into it:</span></span>  
   ![graphic7][graphic7]
3. <span data-ttu-id="2744b-133">Si votre projet utilise une stratégie d’accès partagé sur hello Namespace de Bus de Service, passer toostep 6</span><span class="sxs-lookup"><span data-stu-id="2744b-133">If your job uses a shared access policy on hello Service Bus Namespace, jump toostep 6</span></span>  
4. <span data-ttu-id="2744b-134">Consultez l’onglet de concentrateurs d’événements toohello :</span><span class="sxs-lookup"><span data-stu-id="2744b-134">Go toohello Event Hubs tab:</span></span>  
   ![graphic8][graphic8]
5. <span data-ttu-id="2744b-136">Recherchez hello concentrateur d’événements utilisée par votre travail et allez dans celui-ci :</span><span class="sxs-lookup"><span data-stu-id="2744b-136">Locate hello Event Hub used by your job and go into it:</span></span>  
   ![graphic9][graphic9]
6. <span data-ttu-id="2744b-138">Accédez toohello onglet Configurer :</span><span class="sxs-lookup"><span data-stu-id="2744b-138">Go toohello Configure Tab:</span></span>  
   ![graphic10][graphic10]
7. <span data-ttu-id="2744b-140">Hello déroulante Nom de la stratégie, recherchez la stratégie d’accès hello partagé utilisée par votre projet :</span><span class="sxs-lookup"><span data-stu-id="2744b-140">On hello Policy Name drop-down, locate hello shared access policy used by your job:</span></span>  
   ![graphic11][graphic11]
8. <span data-ttu-id="2744b-142">Entre hello Primary Key et hello clé secondaire, **pick hello ne pas utilisé par votre travail**.</span><span class="sxs-lookup"><span data-stu-id="2744b-142">Between hello Primary Key and hello Secondary Key, **pick hello one not used by your job**.</span></span>  
9. <span data-ttu-id="2744b-143">Appuyez sur Régénérer : </span><span class="sxs-lookup"><span data-stu-id="2744b-143">Hit regenerate:</span></span>  
   ![graphic12][graphic12]
10. <span data-ttu-id="2744b-145">Copiez la clé de hello qui vient d’être généré :</span><span class="sxs-lookup"><span data-stu-id="2744b-145">Copy hello newly generated key:</span></span>  
   ![graphic13][graphic13]
11. <span data-ttu-id="2744b-147">Continuer tooPart 2.</span><span class="sxs-lookup"><span data-stu-id="2744b-147">Continue tooPart 2.</span></span>  

### <a name="sql-database"></a><span data-ttu-id="2744b-148">Base de données SQL</span><span class="sxs-lookup"><span data-stu-id="2744b-148">SQL Database</span></span>
> [!NOTE]
> <span data-ttu-id="2744b-149">Remarque : vous devrez tooconnect toohello Service de base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="2744b-149">Note: you will need tooconnect toohello SQL Database Service.</span></span> <span data-ttu-id="2744b-150">Nous allons tooshow comment toodo à l’aide de cette hello expérience de gestion sur hello portail de gestion Azure, mais vous pouvez choisir toouse un outil côté client telles que SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="2744b-150">We are going tooshow how toodo this using hello management experience on hello Azure Management portal but you may choose toouse some client-side tool such as SQL Server Management Studio as well.</span></span>
>
> 

1. <span data-ttu-id="2744b-151">Consulter le portail de gestion Azure hello extension des bases de données SQL toohello :</span><span class="sxs-lookup"><span data-stu-id="2744b-151">Go toohello SQL Databases extension on hello Azure Management portal:</span></span>  
   ![graphic14][graphic14]
2. <span data-ttu-id="2744b-153">Recherchez hello utilisée par votre travail de la base de données SQL et **cliquez sur le serveur de hello** lier sur hello même ligne :</span><span class="sxs-lookup"><span data-stu-id="2744b-153">Locate hello SQL Database used by your job and **click on hello server** link on hello same line:</span></span>  
   <span data-ttu-id="2744b-154">![graphic15][graphic15]</span><span class="sxs-lookup"><span data-stu-id="2744b-154">![graphic15][graphic15]</span></span>
3. <span data-ttu-id="2744b-155">Cliquez sur hello gérer commande :</span><span class="sxs-lookup"><span data-stu-id="2744b-155">Click hello Manage command:</span></span>  
   ![graphic16][graphic16]
4. <span data-ttu-id="2744b-157">Tapez Base de données principale : </span><span class="sxs-lookup"><span data-stu-id="2744b-157">Type Database Master:</span></span>  
   ![graphic17][graphic17]
5. <span data-ttu-id="2744b-159">Tapez votre nom d’utilisateur, votre mot de passe, puis cliquez sur Ouvrir une session : </span><span class="sxs-lookup"><span data-stu-id="2744b-159">Type in your User Name, Password, and click Log on:</span></span>  
   ![graphic18][graphic18]
6. <span data-ttu-id="2744b-161">Cliquez sur Nouvelle requête : </span><span class="sxs-lookup"><span data-stu-id="2744b-161">Click New Query:</span></span>  
   ![graphic19][graphic19]
7. <span data-ttu-id="2744b-163">Type Bonjour suivant la requête en remplaçant < login_name > avec votre nom d’utilisateur et le remplacement <enterStrongPasswordHere> avec votre nouveau mot de passe :</span><span class="sxs-lookup"><span data-stu-id="2744b-163">Type in hello following query replacing <login_name> with your User Name and replacing <enterStrongPasswordHere> with your new password:</span></span>  
   `CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>'`
8. <span data-ttu-id="2744b-164">Cliquez sur Exécuter : </span><span class="sxs-lookup"><span data-stu-id="2744b-164">Click Run:</span></span>  
   ![graphic20][graphic20]
9. <span data-ttu-id="2744b-166">Revenir en arrière toostep 2 et cette fois, cliquez sur base de données hello :</span><span class="sxs-lookup"><span data-stu-id="2744b-166">Go back toostep 2 and this time click hello database:</span></span>  
   ![graphic21][graphic21]
10. <span data-ttu-id="2744b-168">Cliquez sur hello gérer commande :</span><span class="sxs-lookup"><span data-stu-id="2744b-168">Click hello Manage command:</span></span>  
   ![graphic22][graphic22]
11. <span data-ttu-id="2744b-170">Tapez votre nom d’utilisateur, votre mot de passe, puis cliquez sur Ouvrir une session : </span><span class="sxs-lookup"><span data-stu-id="2744b-170">type in your User Name, Password, and click Logon:</span></span>  
   ![graphic23][graphic23]
12. <span data-ttu-id="2744b-172">Cliquez sur Nouvelle requête : </span><span class="sxs-lookup"><span data-stu-id="2744b-172">Click New Query:</span></span>  
   ![graphic24][graphic24]
13. <span data-ttu-id="2744b-174">Tapez Bonjour suivant la requête en remplaçant < nom_utilisateur > avec un nom en fonction duquel vous voulez tooidentify cette connexion dans le contexte de hello de cette base de données (vous pouvez fournir hello la même valeur que vous avez attribué < login_name >, par exemple) et en remplaçant < login_name > par votre nouveau nom d’utilisateur :</span><span class="sxs-lookup"><span data-stu-id="2744b-174">Type in hello following query replacing <user_name> with a name by which you want tooidentify this login in hello context of this database (you can provide hello same value you gave for <login_name>, for example) and replacing <login_name> with your new user name:</span></span>  
   `CREATE USER <user_name> FROM LOGIN <login_name>`
14. <span data-ttu-id="2744b-175">Cliquez sur Exécuter : </span><span class="sxs-lookup"><span data-stu-id="2744b-175">Click Run:</span></span>  
   ![graphic25][graphic25]
15. <span data-ttu-id="2744b-177">Vous devez maintenant fournir votre nouvel utilisateur hello mêmes rôles et les privilèges votre utilisateur d’origine.</span><span class="sxs-lookup"><span data-stu-id="2744b-177">You should now provide your new user with hello same roles and privileges your original user had.</span></span>
16. <span data-ttu-id="2744b-178">Continuer tooPart 2.</span><span class="sxs-lookup"><span data-stu-id="2744b-178">Continue tooPart 2.</span></span>

## <a name="part-2-stopping-hello-stream-analytics-job"></a><span data-ttu-id="2744b-179">Partie 2 : Arrêt hello tâche Analytique de flux de données</span><span class="sxs-lookup"><span data-stu-id="2744b-179">Part 2: Stopping hello Stream Analytics Job</span></span>
1. <span data-ttu-id="2744b-180">Consulter le portail de gestion Azure hello extension du flux de données Analytique toohello :</span><span class="sxs-lookup"><span data-stu-id="2744b-180">Go toohello Stream Analytics extension on hello Azure Management portal:</span></span>  
   ![graphic26][graphic26]
2. <span data-ttu-id="2744b-182">Recherchez votre travail et accédez-y : </span><span class="sxs-lookup"><span data-stu-id="2744b-182">Locate your job and go into it:</span></span>  
   ![graphic27][graphic27]
3. <span data-ttu-id="2744b-184">Accédez toohello entrées onglet ou hello sorties selon si vous faites pivoter les informations d’identification hello sur une entrée ou une sortie.</span><span class="sxs-lookup"><span data-stu-id="2744b-184">Go toohello Inputs tab or hello Outputs tab based on whether you are rotating hello credentials on an Input or on an Output.</span></span>  
   ![graphic28][graphic28]
4. <span data-ttu-id="2744b-186">Cliquez sur la commande d’arrêt hello et vérifiez le travail de hello s’est arrêté :</span><span class="sxs-lookup"><span data-stu-id="2744b-186">Click hello Stop command and confirm hello job has stopped:</span></span>  
   <span data-ttu-id="2744b-187">![graphic29][graphic29] attendre hello travail toostop.</span><span class="sxs-lookup"><span data-stu-id="2744b-187">![graphic29][graphic29] Wait for hello job toostop.</span></span>
5. <span data-ttu-id="2744b-188">Recherchez hello d’entrée/sortie souhaité informations d’identification toorotate active et accédez dans celui-ci :</span><span class="sxs-lookup"><span data-stu-id="2744b-188">Locate hello input/output you want toorotate credentials on and go into it:</span></span>  
   ![graphic30][graphic30]
6. <span data-ttu-id="2744b-190">Continuer tooPart 3.</span><span class="sxs-lookup"><span data-stu-id="2744b-190">Proceed tooPart 3.</span></span>

## <a name="part-3-editing-hello-credentials-on-hello-stream-analytics-job"></a><span data-ttu-id="2744b-191">Partie 3 : Modification hello informations d’identification sur hello tâche Analytique de flux de données</span><span class="sxs-lookup"><span data-stu-id="2744b-191">Part 3: Editing hello credentials on hello Stream Analytics Job</span></span>
### <a name="blob-storagetable-storage"></a><span data-ttu-id="2744b-192">Stockage d’objets blob/de tables</span><span class="sxs-lookup"><span data-stu-id="2744b-192">Blob storage/Table storage</span></span>
1. <span data-ttu-id="2744b-193">Rechercher le champ de clé de compte de stockage hello et collez votre clé qui vient d’être générée :</span><span class="sxs-lookup"><span data-stu-id="2744b-193">Find hello Storage Account Key field and paste your newly generated key into it:</span></span>  
   ![graphic31][graphic31]
2. <span data-ttu-id="2744b-195">Cliquez sur la commande hello et confirmer l’enregistrement de vos modifications :</span><span class="sxs-lookup"><span data-stu-id="2744b-195">Click hello Save command and confirm saving your changes:</span></span>  
   ![graphic32][graphic32]
3. <span data-ttu-id="2744b-197">Un test de connexion démarre automatiquement lorsque vous enregistrez vos modifications ; assurez-vous qu’il a réussi.</span><span class="sxs-lookup"><span data-stu-id="2744b-197">A connection test will automatically start when you save your changes, make sure that is has successfully passed.</span></span>
4. <span data-ttu-id="2744b-198">Continuer tooPart 4.</span><span class="sxs-lookup"><span data-stu-id="2744b-198">Proceed tooPart 4.</span></span>

### <a name="event-hubs"></a><span data-ttu-id="2744b-199">Hubs d'événements</span><span class="sxs-lookup"><span data-stu-id="2744b-199">Event hubs</span></span>
1. <span data-ttu-id="2744b-200">Rechercher le champ de clé stratégie Hub d’événements hello et collez votre clé qui vient d’être générée :</span><span class="sxs-lookup"><span data-stu-id="2744b-200">Find hello Event Hub Policy Key field and paste your newly generated key into it:</span></span>  
   ![graphic33][graphic33]
2. <span data-ttu-id="2744b-202">Cliquez sur la commande hello et confirmer l’enregistrement de vos modifications :</span><span class="sxs-lookup"><span data-stu-id="2744b-202">Click hello Save command and confirm saving your changes:</span></span>  
   ![graphic34][graphic34]
3. <span data-ttu-id="2744b-204">Un test de connexion démarre automatiquement lorsque vous enregistrez vos modifications ; assurez-vous qu’il a réussi.</span><span class="sxs-lookup"><span data-stu-id="2744b-204">A connection test will automatically start when you save your changes, make sure that it has successfully passed.</span></span>
4. <span data-ttu-id="2744b-205">Continuer tooPart 4.</span><span class="sxs-lookup"><span data-stu-id="2744b-205">Proceed tooPart 4.</span></span>

### <a name="power-bi"></a><span data-ttu-id="2744b-206">Power BI</span><span class="sxs-lookup"><span data-stu-id="2744b-206">Power BI</span></span>
1. <span data-ttu-id="2744b-207">Cliquez sur l’autorisation de renouveler hello :</span><span class="sxs-lookup"><span data-stu-id="2744b-207">Click hello Renew authorization:</span></span>  

   ![graphic35][graphic35]
2. <span data-ttu-id="2744b-209">Vous obtiendrez hello après confirmation :</span><span class="sxs-lookup"><span data-stu-id="2744b-209">You will get hello following confirmation:</span></span>  

   ![graphic36][graphic36]
3. <span data-ttu-id="2744b-211">Cliquez sur la commande hello et confirmer l’enregistrement de vos modifications :</span><span class="sxs-lookup"><span data-stu-id="2744b-211">Click hello Save command and confirm saving your changes:</span></span>  
   ![graphic37][graphic37]
4. <span data-ttu-id="2744b-213">Un test de connexion démarre automatiquement lorsque vous enregistrez vos modifications ; assurez-vous qu’il a réussi.</span><span class="sxs-lookup"><span data-stu-id="2744b-213">A connection test will automatically start when you save your changes, make sure it has successfully passed.</span></span>
5. <span data-ttu-id="2744b-214">Continuer tooPart 4.</span><span class="sxs-lookup"><span data-stu-id="2744b-214">Proceed tooPart 4.</span></span>

### <a name="sql-database"></a><span data-ttu-id="2744b-215">Base de données SQL</span><span class="sxs-lookup"><span data-stu-id="2744b-215">SQL Database</span></span>
1. <span data-ttu-id="2744b-216">Recherche des champs de nom d’utilisateur et mot de passe hello et collez votre nouveau jeu créé des informations d’identification :</span><span class="sxs-lookup"><span data-stu-id="2744b-216">Find hello User Name and Password fields and paste your newly created set of credentials into them:</span></span>  
   ![graphic38][graphic38]
2. <span data-ttu-id="2744b-218">Cliquez sur la commande hello et confirmer l’enregistrement de vos modifications :</span><span class="sxs-lookup"><span data-stu-id="2744b-218">Click hello Save command and confirm saving your changes:</span></span>  
   ![graphic39][graphic39]
3. <span data-ttu-id="2744b-220">Un test de connexion démarre automatiquement lorsque vous enregistrez vos modifications ; assurez-vous qu’il a réussi.</span><span class="sxs-lookup"><span data-stu-id="2744b-220">A connection test will automatically start when you save your changes, make sure that it has successfully passed.</span></span>  
4. <span data-ttu-id="2744b-221">Continuer tooPart 4.</span><span class="sxs-lookup"><span data-stu-id="2744b-221">Proceed tooPart 4.</span></span>

## <a name="part-4-starting-your-job-from-last-stopped-time"></a><span data-ttu-id="2744b-222">Partie 4 – Démarrage de votre travail à partir de l’heure du dernier arrêt</span><span class="sxs-lookup"><span data-stu-id="2744b-222">Part 4: Starting your job from last stopped time</span></span>
1. <span data-ttu-id="2744b-223">Quittez hello d’entrée/sortie :</span><span class="sxs-lookup"><span data-stu-id="2744b-223">Navigate away from hello Input/Output:</span></span>  
   ![graphic40][graphic40]
2. <span data-ttu-id="2744b-225">Cliquez sur commande de démarrage hello :</span><span class="sxs-lookup"><span data-stu-id="2744b-225">Click hello Start command:</span></span>  
   ![graphic41][graphic41]
3. <span data-ttu-id="2744b-227">Choisir l’heure du dernier arrêt de hello et cliquez sur OK :</span><span class="sxs-lookup"><span data-stu-id="2744b-227">Pick hello Last Stopped Time and click OK:</span></span>  
   ![graphic42][graphic42]
4. <span data-ttu-id="2744b-229">Continuer tooPart 5.</span><span class="sxs-lookup"><span data-stu-id="2744b-229">Proceed tooPart 5.</span></span>  

## <a name="part-5-removing-hello-old-set-of-credentials"></a><span data-ttu-id="2744b-230">Partie 5 : Suppression hello ancien jeu d’informations d’identification</span><span class="sxs-lookup"><span data-stu-id="2744b-230">Part 5: Removing hello old set of credentials</span></span>
<span data-ttu-id="2744b-231">Cette partie est applicable toohello suivant des entrées/sorties :</span><span class="sxs-lookup"><span data-stu-id="2744b-231">This part is applicable toohello following inputs/outputs:</span></span>

* <span data-ttu-id="2744b-232">Stockage d’objets blob</span><span class="sxs-lookup"><span data-stu-id="2744b-232">Blob Storage</span></span>
* <span data-ttu-id="2744b-233">Hubs d'événements</span><span class="sxs-lookup"><span data-stu-id="2744b-233">Event Hubs</span></span>
* <span data-ttu-id="2744b-234">Base de données SQL</span><span class="sxs-lookup"><span data-stu-id="2744b-234">SQL Database</span></span>
* <span data-ttu-id="2744b-235">Stockage de tables</span><span class="sxs-lookup"><span data-stu-id="2744b-235">Table Storage</span></span>

### <a name="blob-storagetable-storage"></a><span data-ttu-id="2744b-236">Stockage d’objets blob/de tables</span><span class="sxs-lookup"><span data-stu-id="2744b-236">Blob storage/Table storage</span></span>
<span data-ttu-id="2744b-237">Répétez partie 1 pour hello clé d’accès qui était utilisé précédemment par votre tâche toorenew hello désormais inutilisée clé d’accès.</span><span class="sxs-lookup"><span data-stu-id="2744b-237">Repeat Part 1 for hello Access Key that was previously used by your job toorenew hello now unused Access Key.</span></span>

### <a name="event-hubs"></a><span data-ttu-id="2744b-238">Hubs d'événements</span><span class="sxs-lookup"><span data-stu-id="2744b-238">Event hubs</span></span>
<span data-ttu-id="2744b-239">Répétez partie 1 pour hello clé qui était utilisé précédemment par votre tâche toorenew hello clé maintenant inutilisé.</span><span class="sxs-lookup"><span data-stu-id="2744b-239">Repeat Part 1 for hello Key that was previously used by your job toorenew hello now unused Key.</span></span>

### <a name="sql-database"></a><span data-ttu-id="2744b-240">Base de données SQL</span><span class="sxs-lookup"><span data-stu-id="2744b-240">SQL Database</span></span>
1. <span data-ttu-id="2744b-241">Revenir en arrière fenêtre de requête toohello à partir de la partie 1 étape 7 et tapez Bonjour suivant la requête, en remplaçant < previous_login_name > par nom d’utilisateur qui a été utilisé précédemment par votre tâche de hello :</span><span class="sxs-lookup"><span data-stu-id="2744b-241">Go back toohello query window from Part 1 Step 7 and type in hello following query, replacing <previous_login_name> with hello User Name that was previously used by your job:</span></span>  
   `DROP LOGIN <previous_login_name>`  
2. <span data-ttu-id="2744b-242">Cliquez sur Exécuter : </span><span class="sxs-lookup"><span data-stu-id="2744b-242">Click Run:</span></span>  
   ![graphic43][graphic43]  

<span data-ttu-id="2744b-244">Vous devez obtenir hello après confirmation :</span><span class="sxs-lookup"><span data-stu-id="2744b-244">You should get hello following confirmation:</span></span> 

    Command(s) completed successfully.

## <a name="get-help"></a><span data-ttu-id="2744b-245">Obtenir de l’aide</span><span class="sxs-lookup"><span data-stu-id="2744b-245">Get help</span></span>
<span data-ttu-id="2744b-246">Pour obtenir une assistance, essayez notre [forum Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="2744b-246">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="2744b-247">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2744b-247">Next steps</span></span>
* [<span data-ttu-id="2744b-248">Introduction tooAzure Analytique de flux de données</span><span class="sxs-lookup"><span data-stu-id="2744b-248">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="2744b-249">Prise en main d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="2744b-249">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="2744b-250">Mise à l'échelle des travaux Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="2744b-250">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="2744b-251">Références sur le langage des requêtes d'Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="2744b-251">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="2744b-252">Références sur l’API REST de gestion d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="2744b-252">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

[graphic1]: ./media/stream-analytics-login-credentials-inputs-outputs/1-stream-analytics-login-credentials-inputs-outputs.png
[graphic2]: ./media/stream-analytics-login-credentials-inputs-outputs/2-stream-analytics-login-credentials-inputs-outputs.png
[graphic3]: ./media/stream-analytics-login-credentials-inputs-outputs/3-stream-analytics-login-credentials-inputs-outputs.png
[graphic4]: ./media/stream-analytics-login-credentials-inputs-outputs/4-stream-analytics-login-credentials-inputs-outputs.png
[graphic5]: ./media/stream-analytics-login-credentials-inputs-outputs/5-stream-analytics-login-credentials-inputs-outputs.png
[graphic6]: ./media/stream-analytics-login-credentials-inputs-outputs/6-stream-analytics-login-credentials-inputs-outputs.png
[graphic7]: ./media/stream-analytics-login-credentials-inputs-outputs/7-stream-analytics-login-credentials-inputs-outputs.png
[graphic8]: ./media/stream-analytics-login-credentials-inputs-outputs/8-stream-analytics-login-credentials-inputs-outputs.png
[graphic9]: ./media/stream-analytics-login-credentials-inputs-outputs/9-stream-analytics-login-credentials-inputs-outputs.png
[graphic10]: ./media/stream-analytics-login-credentials-inputs-outputs/10-stream-analytics-login-credentials-inputs-outputs.png
[graphic11]: ./media/stream-analytics-login-credentials-inputs-outputs/11-stream-analytics-login-credentials-inputs-outputs.png
[graphic12]: ./media/stream-analytics-login-credentials-inputs-outputs/12-stream-analytics-login-credentials-inputs-outputs.png
[graphic13]: ./media/stream-analytics-login-credentials-inputs-outputs/13-stream-analytics-login-credentials-inputs-outputs.png
[graphic14]: ./media/stream-analytics-login-credentials-inputs-outputs/14-stream-analytics-login-credentials-inputs-outputs.png
[graphic15]: ./media/stream-analytics-login-credentials-inputs-outputs/15-stream-analytics-login-credentials-inputs-outputs.png
[graphic16]: ./media/stream-analytics-login-credentials-inputs-outputs/16-stream-analytics-login-credentials-inputs-outputs.png
[graphic17]: ./media/stream-analytics-login-credentials-inputs-outputs/17-stream-analytics-login-credentials-inputs-outputs.png
[graphic18]: ./media/stream-analytics-login-credentials-inputs-outputs/18-stream-analytics-login-credentials-inputs-outputs.png
[graphic19]: ./media/stream-analytics-login-credentials-inputs-outputs/19-stream-analytics-login-credentials-inputs-outputs.png
[graphic20]: ./media/stream-analytics-login-credentials-inputs-outputs/20-stream-analytics-login-credentials-inputs-outputs.png
[graphic21]: ./media/stream-analytics-login-credentials-inputs-outputs/21-stream-analytics-login-credentials-inputs-outputs.png
[graphic22]: ./media/stream-analytics-login-credentials-inputs-outputs/22-stream-analytics-login-credentials-inputs-outputs.png
[graphic23]: ./media/stream-analytics-login-credentials-inputs-outputs/23-stream-analytics-login-credentials-inputs-outputs.png
[graphic24]: ./media/stream-analytics-login-credentials-inputs-outputs/24-stream-analytics-login-credentials-inputs-outputs.png
[graphic25]: ./media/stream-analytics-login-credentials-inputs-outputs/25-stream-analytics-login-credentials-inputs-outputs.png
[graphic26]: ./media/stream-analytics-login-credentials-inputs-outputs/26-stream-analytics-login-credentials-inputs-outputs.png
[graphic27]: ./media/stream-analytics-login-credentials-inputs-outputs/27-stream-analytics-login-credentials-inputs-outputs.png
[graphic28]: ./media/stream-analytics-login-credentials-inputs-outputs/28-stream-analytics-login-credentials-inputs-outputs.png
[graphic29]: ./media/stream-analytics-login-credentials-inputs-outputs/29-stream-analytics-login-credentials-inputs-outputs.png
[graphic30]: ./media/stream-analytics-login-credentials-inputs-outputs/30-stream-analytics-login-credentials-inputs-outputs.png
[graphic31]: ./media/stream-analytics-login-credentials-inputs-outputs/31-stream-analytics-login-credentials-inputs-outputs.png
[graphic32]: ./media/stream-analytics-login-credentials-inputs-outputs/32-stream-analytics-login-credentials-inputs-outputs.png
[graphic33]: ./media/stream-analytics-login-credentials-inputs-outputs/33-stream-analytics-login-credentials-inputs-outputs.png
[graphic34]: ./media/stream-analytics-login-credentials-inputs-outputs/34-stream-analytics-login-credentials-inputs-outputs.png
[graphic35]: ./media/stream-analytics-login-credentials-inputs-outputs/35-stream-analytics-login-credentials-inputs-outputs.png
[graphic36]: ./media/stream-analytics-login-credentials-inputs-outputs/36-stream-analytics-login-credentials-inputs-outputs.png
[graphic37]: ./media/stream-analytics-login-credentials-inputs-outputs/37-stream-analytics-login-credentials-inputs-outputs.png
[graphic38]: ./media/stream-analytics-login-credentials-inputs-outputs/38-stream-analytics-login-credentials-inputs-outputs.png
[graphic39]: ./media/stream-analytics-login-credentials-inputs-outputs/39-stream-analytics-login-credentials-inputs-outputs.png
[graphic40]: ./media/stream-analytics-login-credentials-inputs-outputs/40-stream-analytics-login-credentials-inputs-outputs.png
[graphic41]: ./media/stream-analytics-login-credentials-inputs-outputs/41-stream-analytics-login-credentials-inputs-outputs.png
[graphic42]: ./media/stream-analytics-login-credentials-inputs-outputs/42-stream-analytics-login-credentials-inputs-outputs.png
[graphic43]: ./media/stream-analytics-login-credentials-inputs-outputs/43-stream-analytics-login-credentials-inputs-outputs.png

