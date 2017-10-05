---
title: "Profilage d’un service cloud local dans l’émulateur de calcul | Microsoft Docs"
services: cloud-services
description: "Examen des problèmes de performances dans les services cloud à l’aide du profileur Visual Studio"
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
tags: 
ms.assetid: 25e40bf3-eea0-4b0b-9f4a-91ffe797f6c3
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: 51c8192d8312dc5cf546b4c357aeecf6f19d56b8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="testing-the-performance-of-a-cloud-service-locally-in-the-azure-compute-emulator-using-the-visual-studio-profiler"></a><span data-ttu-id="23b4d-103">Test des performances d'un service cloud local dans l'émulateur de calcul Azure avec le profileur Visual Studio</span><span class="sxs-lookup"><span data-stu-id="23b4d-103">Testing the Performance of a Cloud Service Locally in the Azure Compute Emulator Using the Visual Studio Profiler</span></span>
<span data-ttu-id="23b4d-104">Différents outils et diverses techniques permettent de tester les performances des services cloud.</span><span class="sxs-lookup"><span data-stu-id="23b4d-104">A variety of tools and techniques are available for testing the performance of cloud services.</span></span>
<span data-ttu-id="23b4d-105">Lorsque vous publiez un service cloud sur Azure, vous pouvez demander à ce que Visual Studio collecte des données de profilage, puis les analyse en local, comme décrit dans la page [Analyse du profil d’une application Azure][1].</span><span class="sxs-lookup"><span data-stu-id="23b4d-105">When you publish a cloud service to Azure, you can have Visual Studio collect profiling data and then analyze it locally, as described in [Profiling an Azure Application][1].</span></span>
<span data-ttu-id="23b4d-106">Vous pouvez également utiliser le diagnostic pour suivre tout un ensemble de compteurs de performances, comme décrit dans la rubrique [Utilisation de compteurs de performances dans Azure][2].</span><span class="sxs-lookup"><span data-stu-id="23b4d-106">You can also use diagnostics to track a variety of performance counters, as described in [Using performance counters in Azure][2].</span></span>
<span data-ttu-id="23b4d-107">Vous pouvez également profiler votre application en local dans l'émulateur de calcul avant de la déployer dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="23b4d-107">You might also want to profile your application locally in the compute emulator before deploying it to the cloud.</span></span>

<span data-ttu-id="23b4d-108">Cet article présente la méthode de profilage par échantillonnage de l'UC, qui peut se faire en local dans l'émulateur.</span><span class="sxs-lookup"><span data-stu-id="23b4d-108">This article covers the CPU Sampling method of profiling, which can be done locally in the emulator.</span></span> <span data-ttu-id="23b4d-109">Cette méthode de profilage est peu intrusive.</span><span class="sxs-lookup"><span data-stu-id="23b4d-109">CPU sampling is a method of profiling that is not very intrusive.</span></span> <span data-ttu-id="23b4d-110">Selon une fréquence d'échantillonnage définie, le profileur enregistre un instantané de la pile d'appels.</span><span class="sxs-lookup"><span data-stu-id="23b4d-110">At a designated sampling interval, the profiler takes a snapshot of the call stack.</span></span> <span data-ttu-id="23b4d-111">Les données sont collectées pendant un certain temps, puis sont présentées dans un rapport.</span><span class="sxs-lookup"><span data-stu-id="23b4d-111">The data is collected over a period of time, and shown in a report.</span></span> <span data-ttu-id="23b4d-112">Cette méthode de profilage indique plutôt, dans une application qui effectue beaucoup de calculs, où se fait la plus grande part du travail du processeur.</span><span class="sxs-lookup"><span data-stu-id="23b4d-112">This method of profiling tends to indicate where in a computationally intensive application most of the CPU work is being done.</span></span>  <span data-ttu-id="23b4d-113">Ceci vous permet de vous occuper en priorité des « points chauds », là où votre application passe le plus de temps.</span><span class="sxs-lookup"><span data-stu-id="23b4d-113">This gives you the opportunity to focus on the "hot path" where your application is spending the most time.</span></span>

## <a name="1-configure-visual-studio-for-profiling"></a><span data-ttu-id="23b4d-114">1. Configuration de Visual Studio pour le profilage</span><span class="sxs-lookup"><span data-stu-id="23b4d-114">1: Configure Visual Studio for profiling</span></span>
<span data-ttu-id="23b4d-115">Tout d'abord, certaines options de configuration de Visual Studio peuvent s'avérer utiles dans le cadre du profilage.</span><span class="sxs-lookup"><span data-stu-id="23b4d-115">First, there are a few Visual Studio configuration options that might be helpful when profiling.</span></span> <span data-ttu-id="23b4d-116">Afin de bien comprendre les rapports de profilage, vous aurez besoin de symboles (fichiers .pdb) pour votre application, ainsi que de symboles pour les bibliothèques système.</span><span class="sxs-lookup"><span data-stu-id="23b4d-116">To make sense of the profiling reports, you'll need symbols (.pdb files) for your application and also symbols for system libraries.</span></span> <span data-ttu-id="23b4d-117">Assurez-vous que vous faites référence aux serveurs de symboles disponibles.</span><span class="sxs-lookup"><span data-stu-id="23b4d-117">You'll want to make sure that you reference the available symbol servers.</span></span> <span data-ttu-id="23b4d-118">Pour cela, dans le menu **Outils** de Visual Studio, sélectionnez **Options**, puis **Débogage**, et enfin **Symboles**.</span><span class="sxs-lookup"><span data-stu-id="23b4d-118">To do this, on the **Tools** menu in Visual Studio, choose **Options**, then choose **Debugging**, then **Symbols**.</span></span> <span data-ttu-id="23b4d-119">Assurez-vous que Microsoft Symbol Servers figure bien dans **Emplacements du fichier de symboles (.pdb)**.</span><span class="sxs-lookup"><span data-stu-id="23b4d-119">Make sure that Microsoft Symbol Servers is listed under **Symbol file (.pdb) locations**.</span></span>  <span data-ttu-id="23b4d-120">Vous pouvez également faire référence à http://referencesource.microsoft.com/symbols, qui peut comporter d'autres fichiers de symboles.</span><span class="sxs-lookup"><span data-stu-id="23b4d-120">You can also reference http://referencesource.microsoft.com/symbols, which might have additional symbol files.</span></span>

![Options de symbole][4]

<span data-ttu-id="23b4d-122">Si vous le souhaitez, vous pouvez simplifier les rapports générés par le profileur en choisissant Uniquement mon code.</span><span class="sxs-lookup"><span data-stu-id="23b4d-122">If desired, you can simplify the reports that the profiler generates by setting Just My Code.</span></span> <span data-ttu-id="23b4d-123">Lorsque cette option est activée, les piles d'appels de fonction sont simplifiées afin que les appels purement internes aux bibliothèques et à .NET Framework soient masqués dans les rapports.</span><span class="sxs-lookup"><span data-stu-id="23b4d-123">With Just My Code enabled, function call stacks are simplified so that calls entirely internal to libraries and the .NET Framework are hidden from the reports.</span></span> <span data-ttu-id="23b4d-124">Dans le menu **Outils**, choisissez **Options**.</span><span class="sxs-lookup"><span data-stu-id="23b4d-124">On the **Tools** menu, choose **Options**.</span></span> <span data-ttu-id="23b4d-125">Développez le nœud **Outils de performances** et choisissez **Général**.</span><span class="sxs-lookup"><span data-stu-id="23b4d-125">Then expand the **Performance Tools** node, and choose **General**.</span></span> <span data-ttu-id="23b4d-126">Activez la case à cocher **Activer Uniquement mon code pour les rapports du profileur**.</span><span class="sxs-lookup"><span data-stu-id="23b4d-126">Select the checkbox for **Enable Just My Code for profiler reports**.</span></span>

![Options Uniquement mon code][17]

<span data-ttu-id="23b4d-128">Vous pouvez utiliser ces instructions dans un projet existant ou un nouveau projet.</span><span class="sxs-lookup"><span data-stu-id="23b4d-128">You can use these instructions with an existing project or with a new project.</span></span>  <span data-ttu-id="23b4d-129">Si vous créez un projet pour tester une des techniques décrites plus bas, choisissez un projet C# **Service cloud Azure** et sélectionnez un **rôle web** et un **rôle de travail**.</span><span class="sxs-lookup"><span data-stu-id="23b4d-129">If you create a new project to try the techniques described below, choose a C# **Azure Cloud Service** project, and select a **Web Role** and a **Worker Role**.</span></span>

![Rôles de projet Azure Cloud Services][5]

<span data-ttu-id="23b4d-131">Pour l'exemple, ajoutez à votre projet du code qui demande beaucoup de temps et provoque des problèmes de performances évidents.</span><span class="sxs-lookup"><span data-stu-id="23b4d-131">For example purposes, add some code to your project that takes a lot of time and demonstrates some obvious performance problem.</span></span> <span data-ttu-id="23b4d-132">Par exemple, ajoutez le code suivant à un projet de rôle de travail :</span><span class="sxs-lookup"><span data-stu-id="23b4d-132">For example, add the following code to a worker role project:</span></span>

    public class Concatenator
    {
        public static string Concatenate(int number)
        {
            int count;
            string s = "";
            for (count = 0; count < number; count++)
            {
                s += "\n" + count.ToString();
            }
            return s;
        }
    }

<span data-ttu-id="23b4d-133">Appelez ce code depuis la méthode RunAsync dans la classe RoleEntryPoint-derived du rôle de travail.</span><span class="sxs-lookup"><span data-stu-id="23b4d-133">Call this code from the RunAsync method in the worker role's RoleEntryPoint-derived class.</span></span> <span data-ttu-id="23b4d-134">(Ne tenez pas compte de l'avertissement indiquant l'exécution synchrone de la méthode.)</span><span class="sxs-lookup"><span data-stu-id="23b4d-134">(Ignore the warning about the method running synchronously.)</span></span>

        private async Task RunAsync(CancellationToken cancellationToken)
        {
            // TODO: Replace the following with your own logic.
            while (!cancellationToken.IsCancellationRequested)
            {
                Trace.TraceInformation("Working");
                Concatenator.Concatenate(10000);
            }
        }

<span data-ttu-id="23b4d-135">Générez et exécutez le service cloud en local sans débogage (Ctrl+F5), la configuration de solution étant définie sur **Version finale**.</span><span class="sxs-lookup"><span data-stu-id="23b4d-135">Build and run your cloud service locally without debugging (Ctrl+F5), with the solution configuration set to **Release**.</span></span> <span data-ttu-id="23b4d-136">Les fichiers et dossiers sont ainsi créés pour l'exécution de l'application en local et tous les émulateurs sont démarrés.</span><span class="sxs-lookup"><span data-stu-id="23b4d-136">This ensures that all files and folders are created for running the application locally, and ensures that all the emulators are started.</span></span> <span data-ttu-id="23b4d-137">Démarrez l'interface de l'émulateur de calcul à partir de la barre des tâches pour vérifier que votre rôle de travail fonctionne correctement.</span><span class="sxs-lookup"><span data-stu-id="23b4d-137">Start the Compute Emulator UI from the taskbar to verify that your worker role is running.</span></span>

## <a name="2-attach-to-a-process"></a><span data-ttu-id="23b4d-138">2. Attachement à un processus</span><span class="sxs-lookup"><span data-stu-id="23b4d-138">2: Attach to a process</span></span>
<span data-ttu-id="23b4d-139">Au lieu de profiler l'application en la démarrant depuis l'interface de développement de Visual Studio 2010, vous devez attacher le profileur à un processus en cours d'exécution.</span><span class="sxs-lookup"><span data-stu-id="23b4d-139">Instead of profiling the application by starting it from the Visual Studio 2010 IDE, you must attach the profiler to a running process.</span></span> 

<span data-ttu-id="23b4d-140">Pour ce faire, dans le menu **Analyse**, sélectionnez **Profileur**, puis **Attacher/Détacher**.</span><span class="sxs-lookup"><span data-stu-id="23b4d-140">To attach the profiler to a process, on the **Analyze** menu, choose **Profiler** and **Attach/Detach**.</span></span>

![Option Joindre un profil][6]

<span data-ttu-id="23b4d-142">Pour un rôle de travail, recherchez le processus WaWorkerHost.exe.</span><span class="sxs-lookup"><span data-stu-id="23b4d-142">For a worker role, find the WaWorkerHost.exe process.</span></span>

![Processus WaWorkerHost][7]

<span data-ttu-id="23b4d-144">Si votre dossier de projet se trouve sur un disque réseau, le profileur vous demande d'indiquer un autre emplacement pour enregistrer les rapports de profilage.</span><span class="sxs-lookup"><span data-stu-id="23b4d-144">If your project folder is on a network drive, the profiler will ask you to provide another location to save the profiling reports.</span></span>

 <span data-ttu-id="23b4d-145">Vous pouvez également l'attacher à un rôle web en l'attachant à WaIISHost.exe.</span><span class="sxs-lookup"><span data-stu-id="23b4d-145">You can also attach to a web role by attaching to WaIISHost.exe.</span></span>
<span data-ttu-id="23b4d-146">Si votre application comporte plusieurs processus de rôle de travail, utilisez l'ID de processus pour les distinguer les uns des autres.</span><span class="sxs-lookup"><span data-stu-id="23b4d-146">If there are multiple worker role processes in your application, you need to use the processID to distinguish them.</span></span> <span data-ttu-id="23b4d-147">Vous pouvez effectuer une requête par programme sur l'ID de processus en accédant à l'objet Process.</span><span class="sxs-lookup"><span data-stu-id="23b4d-147">You can query the processID programmatically by accessing the Process object.</span></span> <span data-ttu-id="23b4d-148">Par exemple, si vous ajoutez ce code à la méthode Run de la classe RoleEntryPoint-derived dans un rôle, vous pouvez consulter le journal dans l'interface de l'émulateur de calcul pour savoir à quel processus se connecter.</span><span class="sxs-lookup"><span data-stu-id="23b4d-148">For example, if you add this code to the Run method of the RoleEntryPoint-derived class in a role, you can look at the log in the Compute Emulator UI to know what process to connect to.</span></span>

    var process = System.Diagnostics.Process.GetCurrentProcess();
    var message = String.Format("Process ID: {0}", process.Id);
    Trace.WriteLine(message, "Information");

<span data-ttu-id="23b4d-149">Pour consulter le journal, ouvrez l'interface utilisateur de l'émulateur de calcul.</span><span class="sxs-lookup"><span data-stu-id="23b4d-149">To view the log, start the Compute Emulator UI.</span></span>

![Démarrage de l’interface de l’émulateur de calcul][8]

<span data-ttu-id="23b4d-151">Ouvrez la fenêtre de console du journal du rôle de travail dans l'interface utilisateur de l'émulateur de calcul en cliquant sur la barre de titre de la fenêtre de la console.</span><span class="sxs-lookup"><span data-stu-id="23b4d-151">Open the worker role log console window in the Compute Emulator UI by clicking on the console window's title bar.</span></span> <span data-ttu-id="23b4d-152">L'ID du processus figure dans le journal.</span><span class="sxs-lookup"><span data-stu-id="23b4d-152">You can see the process ID in the log.</span></span>

![Afficher l’ID du processus][9]

<span data-ttu-id="23b4d-154">Une fois le profileur attaché, suivez les étapes de l'interface utilisateur de votre application (le cas échéant) afin de reproduire le scénario.</span><span class="sxs-lookup"><span data-stu-id="23b4d-154">One you've attached, perform the steps in your application's UI (if needed) to reproduce the scenario.</span></span>

<span data-ttu-id="23b4d-155">Lorsque vous souhaitez arrêter le profilage, cliquez sur le lien **Terminer le profilage** .</span><span class="sxs-lookup"><span data-stu-id="23b4d-155">When you want to stop profiling, choose the **Stop Profiling** link.</span></span>

![Option Terminer le profilage][10]

## <a name="3-view-performance-reports"></a><span data-ttu-id="23b4d-157">3. Affichage des rapports de performances</span><span class="sxs-lookup"><span data-stu-id="23b4d-157">3: View performance reports</span></span>
<span data-ttu-id="23b4d-158">Le rapport de performances de votre application s'affiche.</span><span class="sxs-lookup"><span data-stu-id="23b4d-158">The performance report for your application is displayed.</span></span>

<span data-ttu-id="23b4d-159">À ce stade, le profileur s'arrête, il enregistre les données dans un fichier .vsp et il affiche un rapport présentant une analyse des données.</span><span class="sxs-lookup"><span data-stu-id="23b4d-159">At this point, the profiler stops executing, saves data in a .vsp file, and displays a report that shows an analysis of this data.</span></span>

![Rapport du profileur][11]

<span data-ttu-id="23b4d-161">Si vous voyez String.wstrcpy dans le Chemin réactif, cliquez sur Uniquement mon code pour modifier l'affichage et ne voir que le code utilisateur.</span><span class="sxs-lookup"><span data-stu-id="23b4d-161">If you see String.wstrcpy in the Hot Path, click on Just My Code to change the view to show user code only.</span></span>  <span data-ttu-id="23b4d-162">Si vous voyez String.Concat, essayez de cliquer sur le bouton Afficher tout le code.</span><span class="sxs-lookup"><span data-stu-id="23b4d-162">If you see String.Concat, try pressing the Show All Code button.</span></span>

<span data-ttu-id="23b4d-163">Vous devez voir que la méthode Concatenate et String.Concat occupent une grande partie du temps d'exécution.</span><span class="sxs-lookup"><span data-stu-id="23b4d-163">You should see the Concatenate method and String.Concat taking up a large portion of the execution time.</span></span>

![Analyse du rapport][12]

<span data-ttu-id="23b4d-165">Si vous avez ajouté le code de concaténation de chaîne dans cet article, vous devez obtenir un avertissement correspondant dans la Liste des tâches.</span><span class="sxs-lookup"><span data-stu-id="23b4d-165">If you added the string concatenation code in this article, you should see a warning in the Task List for this.</span></span> <span data-ttu-id="23b4d-166">Il est possible que vous voyiez également un avertissement lié au nettoyage de la mémoire, ce qui est dû au nombre de chaînes créées et rejetées.</span><span class="sxs-lookup"><span data-stu-id="23b4d-166">You may also see a warning that there is an excessive amount of garbage collection, which is due to the number of strings that are created and disposed.</span></span>

![Avertissements liés aux performances][14]

## <a name="4-make-changes-and-compare-performance"></a><span data-ttu-id="23b4d-168">4 : Application de modifications et comparaison des performances</span><span class="sxs-lookup"><span data-stu-id="23b4d-168">4: Make changes and compare performance</span></span>
<span data-ttu-id="23b4d-169">Vous pouvez également comparer les performances avant et après la modification du code.</span><span class="sxs-lookup"><span data-stu-id="23b4d-169">You can also compare the performance before and after a code change.</span></span>  <span data-ttu-id="23b4d-170">Interrompez le processus en cours d'exécution et modifiez le code de façon à remplacer l'opération de concaténation de chaîne à l'aide de StringBuilder :</span><span class="sxs-lookup"><span data-stu-id="23b4d-170">Stop the running process, and edit the code to replace the string concatenation operation with the use of StringBuilder:</span></span>

    public static string Concatenate(int number)
    {
        int count;
        System.Text.StringBuilder builder = new System.Text.StringBuilder("");
        for (count = 0; count < number; count++)
        {
             builder.Append("\n" + count.ToString());
        }
        return builder.ToString();
    }

<span data-ttu-id="23b4d-171">Lancez un nouveau test de performances, et comparez les résultats.</span><span class="sxs-lookup"><span data-stu-id="23b4d-171">Do another performance run, and then compare the performance.</span></span> <span data-ttu-id="23b4d-172">Dans l'Explorateur de performances, si les tests font partie de la même session, vous pouvez simplement sélectionner les deux rapports, ouvrir le menu contextuel et sélectionner **Comparer les rapports de performances**.</span><span class="sxs-lookup"><span data-stu-id="23b4d-172">In the Performance Explorer, if the runs are in the same session, you can just select both reports, open the shortcut menu, and choose **Compare Performance Reports**.</span></span> <span data-ttu-id="23b4d-173">Si vous souhaitez comparer un test avec un test d’une autre session de performances, ouvrez le menu **Analyse**, puis sélectionnez **Comparer les rapports de performances**.</span><span class="sxs-lookup"><span data-stu-id="23b4d-173">If you want to compare with a run in another performance session, open the **Analyze** menu, and choose **Compare Performance Reports**.</span></span> <span data-ttu-id="23b4d-174">Spécifiez les deux fichiers dans la boîte de dialogue qui s'affiche.</span><span class="sxs-lookup"><span data-stu-id="23b4d-174">Specify both files in the dialog box that appears.</span></span>

![Option Comparer les rapports de performances][15]

<span data-ttu-id="23b4d-176">Les rapports indiquent les différences entre les deux tests.</span><span class="sxs-lookup"><span data-stu-id="23b4d-176">The reports highlight differences between the two runs.</span></span>

![Rapport de comparaison][16]

<span data-ttu-id="23b4d-178">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="23b4d-178">Congratulations!</span></span> <span data-ttu-id="23b4d-179">Vous avez fait connaissance avec le profileur.</span><span class="sxs-lookup"><span data-stu-id="23b4d-179">You've gotten started with the profiler.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="23b4d-180">Résolution de problèmes</span><span class="sxs-lookup"><span data-stu-id="23b4d-180">Troubleshooting</span></span>
* <span data-ttu-id="23b4d-181">Assurez-vous que le profilage porte bien sur une build Release et exécutez sans débogage.</span><span class="sxs-lookup"><span data-stu-id="23b4d-181">Make sure you are profiling a Release build and start without debugging.</span></span>
* <span data-ttu-id="23b4d-182">Si l'option Attacher/Détacher n'est pas activée dans le menu Profileur, exécutez l'Assistant Performance.</span><span class="sxs-lookup"><span data-stu-id="23b4d-182">If the Attach/Detach option is not enabled on the Profiler menu, run the Performance Wizard.</span></span>
* <span data-ttu-id="23b4d-183">Utilisez l'émulateur de calcul pour connaître l'état de votre application.</span><span class="sxs-lookup"><span data-stu-id="23b4d-183">Use the Compute Emulator UI to view the status of your application.</span></span> 
* <span data-ttu-id="23b4d-184">Si vous rencontrez des problèmes pour démarrer les applications dans l'émulateur de calcul ou pour attacher le profileur, arrêtez l'émulateur de calcul et redémarrez-le.</span><span class="sxs-lookup"><span data-stu-id="23b4d-184">If you have problems starting applications in the emulator, or attaching the profiler, shut down the compute emulator and restart it.</span></span> <span data-ttu-id="23b4d-185">Si cela ne résout pas le problème, essayez de redémarrer votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="23b4d-185">If that doesn't solve the problem, try rebooting.</span></span> <span data-ttu-id="23b4d-186">Ce problème peut survenir lorsque vous utilisez l'émulateur de calcul pour suspendre et supprimer des déploiements en cours d'exécution.</span><span class="sxs-lookup"><span data-stu-id="23b4d-186">This problem can occur if you use the Compute Emulator to suspend and remove running deployments.</span></span>
* <span data-ttu-id="23b4d-187">Si vous avez utilisé une des commandes de profilage depuis la ligne de commande, en particulier les paramètres globaux, assurez-vous que VSPerfClrEnv /globaloff a été appelé et que VsPerfMon.exe est arrêté.</span><span class="sxs-lookup"><span data-stu-id="23b4d-187">If you have used any of the profiling commands from the command line, especially the global settings, make sure that VSPerfClrEnv /globaloff has been called and that VsPerfMon.exe has been shut down.</span></span>
* <span data-ttu-id="23b4d-188">Si lors de l’échantillonnage, le message « PRF0025 : aucune donnée n’a été collectée » s’affiche, vérifiez si le processus que vous avez attaché présente une activité dans le processeur.</span><span class="sxs-lookup"><span data-stu-id="23b4d-188">If when sampling, you see the message "PRF0025: No data was collected," check that the process you attached to has CPU activity.</span></span> <span data-ttu-id="23b4d-189">Les applications qui n'effectuent pas de calculs peuvent ne pas produire de données d'échantillonnage.</span><span class="sxs-lookup"><span data-stu-id="23b4d-189">Applications that are not doing any computational work might not produce any sampling data.</span></span>  <span data-ttu-id="23b4d-190">Il est également possible que le processus se soit terminé avant l'exécution de l'échantillonnage.</span><span class="sxs-lookup"><span data-stu-id="23b4d-190">It's also possible that the process exited before any sampling was done.</span></span> <span data-ttu-id="23b4d-191">Vérifiez si la méthode Run du rôle pour lequel vous établissez le profil ne s'est pas terminée.</span><span class="sxs-lookup"><span data-stu-id="23b4d-191">Check to see that the Run method for a role that you are profiling does not terminate.</span></span>

## <a name="next-steps"></a><span data-ttu-id="23b4d-192">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="23b4d-192">Next Steps</span></span>
<span data-ttu-id="23b4d-193">L'instrumentalisation d'exécutables Azure dans l'émulateur de calcul n'est pas prise en charge par le profileur Visual Studio, mais si vous souhaitez tester l'allocation de la mémoire, vous pouvez choisir cette option au moment du profilage.</span><span class="sxs-lookup"><span data-stu-id="23b4d-193">Instrumenting Azure binaries in the emulator is not supported in the Visual Studio profiler, but if you want to test memory allocation, you can choose that option when profiling.</span></span> <span data-ttu-id="23b4d-194">Vous pouvez également choisir le profilage d'accès concurrentiel, qui vous aide à savoir si des threads perdent du temps à se disputer les verrouillages, ou bien le profilage d'interaction de couche, qui permet de détecter les problèmes de performances lors de l'interaction entre différentes couches de l'application, la plupart du temps entre la couche de données et un rôle de travail.</span><span class="sxs-lookup"><span data-stu-id="23b4d-194">You can also choose concurrency profiling, which helps you determine whether threads are wasting time competing for locks, or tier interaction profiling, which helps you track down performance problems when interacting between tiers of an application, most frequently between the data tier and a worker role.</span></span>  <span data-ttu-id="23b4d-195">Vous pouvez consulter les requêtes de base de données que votre application génère et utiliser les données de profilage pour optimiser l'utilisation de la base de données.</span><span class="sxs-lookup"><span data-stu-id="23b4d-195">You can view the database queries that your app generates and use the profiling data to improve your use of the database.</span></span> <span data-ttu-id="23b4d-196">Pour plus d’informations sur le profilage d’interaction de couche, consultez le billet de blog intitulé [Procédure pas à pas : utilisation du profileur d’interaction de couche dans Visual Studio Team System 2010][3].</span><span class="sxs-lookup"><span data-stu-id="23b4d-196">For information about tier interaction profiling, see the blog post [Walkthrough: Using the Tier Interaction Profiler in Visual Studio Team System 2010][3].</span></span>

[1]: http://msdn.microsoft.com/library/azure/hh369930.aspx
[2]: http://msdn.microsoft.com/library/azure/hh411542.aspx
[3]: http://blogs.msdn.com/b/habibh/archive/2009/06/30/walkthrough-using-the-tier-interaction-profiler-in-visual-studio-team-system-2010.aspx
[4]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally09.png
[5]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally10.png
[6]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally02.png
[7]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally05.png
[8]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally010.png
[9]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally07.png
[10]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally06.png
[11]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally03.png
[12]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally011.png
[14]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally04.png 
[15]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally013.png
[16]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally012.png
[17]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally08.png
