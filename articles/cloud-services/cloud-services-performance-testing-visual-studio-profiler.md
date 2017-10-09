---
title: "aaaProfiling un Service Cloud localement dans l’émulateur de calcul de hello | Documents Microsoft"
services: cloud-services
description: "Résoudre les problèmes de performances dans les services de cloud avec le profileur Visual Studio de hello"
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
ms.openlocfilehash: fc37c85dad4db4cc0310f73afad56fc0fe5f3963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="testing-hello-performance-of-a-cloud-service-locally-in-hello-azure-compute-emulator-using-hello-visual-studio-profiler"></a><span data-ttu-id="55ce5-103">Test hello performances d’un Service Cloud localement Bonjour Azure Compute Emulator à l’aide de hello profileur Visual Studio</span><span class="sxs-lookup"><span data-stu-id="55ce5-103">Testing hello Performance of a Cloud Service Locally in hello Azure Compute Emulator Using hello Visual Studio Profiler</span></span>
<span data-ttu-id="55ce5-104">Divers outils et techniques sont disponibles pour tester les performances de hello des services de cloud computing.</span><span class="sxs-lookup"><span data-stu-id="55ce5-104">A variety of tools and techniques are available for testing hello performance of cloud services.</span></span>
<span data-ttu-id="55ce5-105">Lorsque vous publiez un tooAzure de service cloud, vous pouvez avoir Visual Studio collecter les données de profilage et puis les analyser localement, comme décrit dans [profilage d’une Application Azure][1].</span><span class="sxs-lookup"><span data-stu-id="55ce5-105">When you publish a cloud service tooAzure, you can have Visual Studio collect profiling data and then analyze it locally, as described in [Profiling an Azure Application][1].</span></span>
<span data-ttu-id="55ce5-106">Vous pouvez également utiliser tootrack diagnostics des compteurs de performances diverses, comme décrit dans [à l’aide des compteurs de performances dans Azure][2].</span><span class="sxs-lookup"><span data-stu-id="55ce5-106">You can also use diagnostics tootrack a variety of performance counters, as described in [Using performance counters in Azure][2].</span></span>
<span data-ttu-id="55ce5-107">Vous pouvez également vous tooprofile votre application localement dans l’émulateur de calcul hello avant de le déployer toohello cloud.</span><span class="sxs-lookup"><span data-stu-id="55ce5-107">You might also want tooprofile your application locally in hello compute emulator before deploying it toohello cloud.</span></span>

<span data-ttu-id="55ce5-108">Cet article décrit la méthode d’échantillonnage de l’UC hello de profilage, ce qui peut être effectué localement dans l’émulateur de hello.</span><span class="sxs-lookup"><span data-stu-id="55ce5-108">This article covers hello CPU Sampling method of profiling, which can be done locally in hello emulator.</span></span> <span data-ttu-id="55ce5-109">Cette méthode de profilage est peu intrusive.</span><span class="sxs-lookup"><span data-stu-id="55ce5-109">CPU sampling is a method of profiling that is not very intrusive.</span></span> <span data-ttu-id="55ce5-110">À un intervalle d’échantillonnage désigné, Générateur de profils hello prend un instantané de pile des appels hello.</span><span class="sxs-lookup"><span data-stu-id="55ce5-110">At a designated sampling interval, hello profiler takes a snapshot of hello call stack.</span></span> <span data-ttu-id="55ce5-111">les données de Hello sont collectées sur une période de temps et affichées dans un rapport.</span><span class="sxs-lookup"><span data-stu-id="55ce5-111">hello data is collected over a period of time, and shown in a report.</span></span> <span data-ttu-id="55ce5-112">Cette méthode de profilage a tendance à tooindicate où dans une application nécessitant la plupart du travail de hello du processeur est effectuée.</span><span class="sxs-lookup"><span data-stu-id="55ce5-112">This method of profiling tends tooindicate where in a computationally intensive application most of hello CPU work is being done.</span></span>  <span data-ttu-id="55ce5-113">Ceci permet de vous hello toofocus opportunité sur hello « chemin réactif » où votre application passe hello plus de temps.</span><span class="sxs-lookup"><span data-stu-id="55ce5-113">This gives you hello opportunity toofocus on hello "hot path" where your application is spending hello most time.</span></span>

## <a name="1-configure-visual-studio-for-profiling"></a><span data-ttu-id="55ce5-114">1. Configuration de Visual Studio pour le profilage</span><span class="sxs-lookup"><span data-stu-id="55ce5-114">1: Configure Visual Studio for profiling</span></span>
<span data-ttu-id="55ce5-115">Tout d'abord, certaines options de configuration de Visual Studio peuvent s'avérer utiles dans le cadre du profilage.</span><span class="sxs-lookup"><span data-stu-id="55ce5-115">First, there are a few Visual Studio configuration options that might be helpful when profiling.</span></span> <span data-ttu-id="55ce5-116">décryptage toomake hello des rapports de profilage, vous aurez besoin de symboles (.pdb) pour votre application, ainsi que les symboles pour les bibliothèques système.</span><span class="sxs-lookup"><span data-stu-id="55ce5-116">toomake sense of hello profiling reports, you'll need symbols (.pdb files) for your application and also symbols for system libraries.</span></span> <span data-ttu-id="55ce5-117">Vous souhaiterez toomake assurer que vous référencez des serveurs de symboles disponibles hello.</span><span class="sxs-lookup"><span data-stu-id="55ce5-117">You'll want toomake sure that you reference hello available symbol servers.</span></span> <span data-ttu-id="55ce5-118">toodo cette, hello **outils** menu dans Visual Studio, choisissez **Options**, puis choisissez **débogage**, puis **symboles**.</span><span class="sxs-lookup"><span data-stu-id="55ce5-118">toodo this, on hello **Tools** menu in Visual Studio, choose **Options**, then choose **Debugging**, then **Symbols**.</span></span> <span data-ttu-id="55ce5-119">Assurez-vous que Microsoft Symbol Servers figure bien dans **Emplacements du fichier de symboles (.pdb)**.</span><span class="sxs-lookup"><span data-stu-id="55ce5-119">Make sure that Microsoft Symbol Servers is listed under **Symbol file (.pdb) locations**.</span></span>  <span data-ttu-id="55ce5-120">Vous pouvez également faire référence à http://referencesource.microsoft.com/symbols, qui peut comporter d'autres fichiers de symboles.</span><span class="sxs-lookup"><span data-stu-id="55ce5-120">You can also reference http://referencesource.microsoft.com/symbols, which might have additional symbol files.</span></span>

![Options de symbole][4]

<span data-ttu-id="55ce5-122">Si vous le souhaitez, vous pouvez simplifier hello signale ce profileur hello génère en définissant uniquement mon Code.</span><span class="sxs-lookup"><span data-stu-id="55ce5-122">If desired, you can simplify hello reports that hello profiler generates by setting Just My Code.</span></span> <span data-ttu-id="55ce5-123">Avec uniquement mon Code est activée, les piles d’appels de fonction sont simplifiées ainsi que les appels toolibraries entièrement interne hello .NET Framework sont masqués à partir de rapports de hello.</span><span class="sxs-lookup"><span data-stu-id="55ce5-123">With Just My Code enabled, function call stacks are simplified so that calls entirely internal toolibraries and hello .NET Framework are hidden from hello reports.</span></span> <span data-ttu-id="55ce5-124">Sur hello **outils** menu, choisissez **Options**.</span><span class="sxs-lookup"><span data-stu-id="55ce5-124">On hello **Tools** menu, choose **Options**.</span></span> <span data-ttu-id="55ce5-125">Puis développez hello **outils de performances** nœud, puis choisissez **général**.</span><span class="sxs-lookup"><span data-stu-id="55ce5-125">Then expand hello **Performance Tools** node, and choose **General**.</span></span> <span data-ttu-id="55ce5-126">Sélectionnez la case à cocher hello **activer uniquement mon Code pour les rapports de profileur**.</span><span class="sxs-lookup"><span data-stu-id="55ce5-126">Select hello checkbox for **Enable Just My Code for profiler reports**.</span></span>

![Options Uniquement mon code][17]

<span data-ttu-id="55ce5-128">Vous pouvez utiliser ces instructions dans un projet existant ou un nouveau projet.</span><span class="sxs-lookup"><span data-stu-id="55ce5-128">You can use these instructions with an existing project or with a new project.</span></span>  <span data-ttu-id="55ce5-129">Si vous créez un nouveau Bonjour de tootry projet techniques décrites ci-dessous, choisissez c# **Azure Cloud Service** le projet, puis sélectionnez un **rôle Web** et un **rôle de travail**.</span><span class="sxs-lookup"><span data-stu-id="55ce5-129">If you create a new project tootry hello techniques described below, choose a C# **Azure Cloud Service** project, and select a **Web Role** and a **Worker Role**.</span></span>

![Rôles de projet Azure Cloud Services][5]

<span data-ttu-id="55ce5-131">Par exemple, à des fins, ajouter un projet de tooyour de code qui prend beaucoup de temps et présente un problème de performances évidente.</span><span class="sxs-lookup"><span data-stu-id="55ce5-131">For example purposes, add some code tooyour project that takes a lot of time and demonstrates some obvious performance problem.</span></span> <span data-ttu-id="55ce5-132">Par exemple, ajouter hello suivant du projet de rôle de travail tooa code :</span><span class="sxs-lookup"><span data-stu-id="55ce5-132">For example, add hello following code tooa worker role project:</span></span>

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

<span data-ttu-id="55ce5-133">Appeler ce code à partir de la méthode RunAsync dans une classe dérivée de RoleEntryPoint du rôle de travail hello de hello.</span><span class="sxs-lookup"><span data-stu-id="55ce5-133">Call this code from hello RunAsync method in hello worker role's RoleEntryPoint-derived class.</span></span> <span data-ttu-id="55ce5-134">(Ignorer l’avertissement hello sur la méthode hello exécuter de façon synchrone.)</span><span class="sxs-lookup"><span data-stu-id="55ce5-134">(Ignore hello warning about hello method running synchronously.)</span></span>

        private async Task RunAsync(CancellationToken cancellationToken)
        {
            // TODO: Replace hello following with your own logic.
            while (!cancellationToken.IsCancellationRequested)
            {
                Trace.TraceInformation("Working");
                Concatenator.Concatenate(10000);
            }
        }

<span data-ttu-id="55ce5-135">Générer et exécuter votre service cloud localement sans débogage (Ctrl + F5), avec la configuration de la solution hello définie trop**version**.</span><span class="sxs-lookup"><span data-stu-id="55ce5-135">Build and run your cloud service locally without debugging (Ctrl+F5), with hello solution configuration set too**Release**.</span></span> <span data-ttu-id="55ce5-136">Cela garantit que tous les fichiers et dossiers sont créés pour l’application hello s’exécute et garantit que tous les émulateurs hello sont démarrés.</span><span class="sxs-lookup"><span data-stu-id="55ce5-136">This ensures that all files and folders are created for running hello application locally, and ensures that all hello emulators are started.</span></span> <span data-ttu-id="55ce5-137">Démarrez hello Compute Emulator UI de tooverify de la barre des tâches de hello votre rôle de travail est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="55ce5-137">Start hello Compute Emulator UI from hello taskbar tooverify that your worker role is running.</span></span>

## <a name="2-attach-tooa-process"></a><span data-ttu-id="55ce5-138">2 : attacher le processus de tooa</span><span class="sxs-lookup"><span data-stu-id="55ce5-138">2: Attach tooa process</span></span>
<span data-ttu-id="55ce5-139">Au lieu de profiler l’application hello en le démarrant à partir de hello IDE de Visual Studio 2010, vous devez joindre tooa de profileur hello processus en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="55ce5-139">Instead of profiling hello application by starting it from hello Visual Studio 2010 IDE, you must attach hello profiler tooa running process.</span></span> 

<span data-ttu-id="55ce5-140">tooattach hello profiler tooa processus sur hello **analyser** menu, choisissez **Profiler** et **Attacher/Détacher**.</span><span class="sxs-lookup"><span data-stu-id="55ce5-140">tooattach hello profiler tooa process, on hello **Analyze** menu, choose **Profiler** and **Attach/Detach**.</span></span>

![Option Joindre un profil][6]

<span data-ttu-id="55ce5-142">Pour un rôle de travail, de trouver le processus de WaWorkerHost.exe hello.</span><span class="sxs-lookup"><span data-stu-id="55ce5-142">For a worker role, find hello WaWorkerHost.exe process.</span></span>

![Processus WaWorkerHost][7]

<span data-ttu-id="55ce5-144">Si votre dossier de projet se trouve sur un lecteur réseau, Générateur de profils hello vous demandera tooprovide hello de toosave un autre emplacement des rapports de profilage.</span><span class="sxs-lookup"><span data-stu-id="55ce5-144">If your project folder is on a network drive, hello profiler will ask you tooprovide another location toosave hello profiling reports.</span></span>

 <span data-ttu-id="55ce5-145">Vous pouvez également attacher le rôle web de tooa en attachant tooWaIISHost.exe.</span><span class="sxs-lookup"><span data-stu-id="55ce5-145">You can also attach tooa web role by attaching tooWaIISHost.exe.</span></span>
<span data-ttu-id="55ce5-146">S’il existe plusieurs processus de rôle de travail dans votre application, vous devez toouse hello processID toodistinguish les.</span><span class="sxs-lookup"><span data-stu-id="55ce5-146">If there are multiple worker role processes in your application, you need toouse hello processID toodistinguish them.</span></span> <span data-ttu-id="55ce5-147">Vous pouvez interroger hello processID par programme en accédant à des objets de processus hello.</span><span class="sxs-lookup"><span data-stu-id="55ce5-147">You can query hello processID programmatically by accessing hello Process object.</span></span> <span data-ttu-id="55ce5-148">Par exemple, si vous ajoutez cette méthode d’exécution toohello code de classe dérivée de RoleEntryPoint de hello dans un rôle, vous pouvez consulter le journal dans hello Compute Emulator UI tooknow le tooconnect de processus pour.</span><span class="sxs-lookup"><span data-stu-id="55ce5-148">For example, if you add this code toohello Run method of hello RoleEntryPoint-derived class in a role, you can look at the log in hello Compute Emulator UI tooknow what process tooconnect to.</span></span>

    var process = System.Diagnostics.Process.GetCurrentProcess();
    var message = String.Format("Process ID: {0}", process.Id);
    Trace.WriteLine(message, "Information");

<span data-ttu-id="55ce5-149">journal de hello tooview, début hello Compute Emulator UI.</span><span class="sxs-lookup"><span data-stu-id="55ce5-149">tooview hello log, start hello Compute Emulator UI.</span></span>

![Démarrer hello Compute Emulator UI][8]

<span data-ttu-id="55ce5-151">Ouvrez fenêtre de console hello travail rôle journal Bonjour Compute Emulator UI en cliquant sur la barre de titre de la fenêtre de console hello.</span><span class="sxs-lookup"><span data-stu-id="55ce5-151">Open hello worker role log console window in hello Compute Emulator UI by clicking on hello console window's title bar.</span></span> <span data-ttu-id="55ce5-152">Vous pouvez voir les ID de processus hello dans le journal de hello.</span><span class="sxs-lookup"><span data-stu-id="55ce5-152">You can see hello process ID in hello log.</span></span>

![Afficher l’ID du processus][9]

<span data-ttu-id="55ce5-154">Un que vous avez joint, effectuez les opérations de hello dans l’interface utilisateur (si nécessaire) tooreproduce hello scénario de votre application.</span><span class="sxs-lookup"><span data-stu-id="55ce5-154">One you've attached, perform hello steps in your application's UI (if needed) tooreproduce hello scenario.</span></span>

<span data-ttu-id="55ce5-155">Lorsque vous souhaitez toostop de profilage, choisissez hello **arrêter le profilage** lien.</span><span class="sxs-lookup"><span data-stu-id="55ce5-155">When you want toostop profiling, choose hello **Stop Profiling** link.</span></span>

![Option Terminer le profilage][10]

## <a name="3-view-performance-reports"></a><span data-ttu-id="55ce5-157">3. Affichage des rapports de performances</span><span class="sxs-lookup"><span data-stu-id="55ce5-157">3: View performance reports</span></span>
<span data-ttu-id="55ce5-158">rapport de performances Hello pour votre application s’affiche.</span><span class="sxs-lookup"><span data-stu-id="55ce5-158">hello performance report for your application is displayed.</span></span>

<span data-ttu-id="55ce5-159">À ce stade, Générateur de profils hello arrête l’exécution, enregistre les données dans un fichier .vsp et affiche un rapport qui affiche une analyse de ces données.</span><span class="sxs-lookup"><span data-stu-id="55ce5-159">At this point, hello profiler stops executing, saves data in a .vsp file, and displays a report that shows an analysis of this data.</span></span>

![Rapport du profileur][11]

<span data-ttu-id="55ce5-161">Si vous voyez String.wstrcpy dans hello chemin réactif, cliquez sur uniquement mon Code toochange hello vue tooshow code utilisateur uniquement.</span><span class="sxs-lookup"><span data-stu-id="55ce5-161">If you see String.wstrcpy in hello Hot Path, click on Just My Code toochange hello view tooshow user code only.</span></span>  <span data-ttu-id="55ce5-162">Si vous voyez String.Concat, essayez de cliquer sur Afficher tout Code hello.</span><span class="sxs-lookup"><span data-stu-id="55ce5-162">If you see String.Concat, try pressing hello Show All Code button.</span></span>

<span data-ttu-id="55ce5-163">Vous devez voir la méthode de concaténation hello et String.Concat occuper une grande partie du temps d’exécution hello.</span><span class="sxs-lookup"><span data-stu-id="55ce5-163">You should see hello Concatenate method and String.Concat taking up a large portion of hello execution time.</span></span>

![Analyse du rapport][12]

<span data-ttu-id="55ce5-165">Si vous avez ajouté le code de concaténation de chaîne hello dans cet article, vous devez voir un avertissement dans la liste des tâches de hello pour cela.</span><span class="sxs-lookup"><span data-stu-id="55ce5-165">If you added hello string concatenation code in this article, you should see a warning in hello Task List for this.</span></span> <span data-ttu-id="55ce5-166">Vous pouvez également voir un avertissement que qu’il existe une quantité excessive de garbage collection, en raison du nombre de toohello de chaînes qui sont créés et supprimés.</span><span class="sxs-lookup"><span data-stu-id="55ce5-166">You may also see a warning that there is an excessive amount of garbage collection, which is due toohello number of strings that are created and disposed.</span></span>

![Avertissements liés aux performances][14]

## <a name="4-make-changes-and-compare-performance"></a><span data-ttu-id="55ce5-168">4 : Application de modifications et comparaison des performances</span><span class="sxs-lookup"><span data-stu-id="55ce5-168">4: Make changes and compare performance</span></span>
<span data-ttu-id="55ce5-169">Vous pouvez également comparer les performances de hello avant et après une modification du code.</span><span class="sxs-lookup"><span data-stu-id="55ce5-169">You can also compare hello performance before and after a code change.</span></span>  <span data-ttu-id="55ce5-170">Arrêter le processus en cours d’exécution de hello et modifiez hello code tooreplace hello concaténation de chaînes avec utilisation de hello de StringBuilder :</span><span class="sxs-lookup"><span data-stu-id="55ce5-170">Stop hello running process, and edit hello code tooreplace hello string concatenation operation with hello use of StringBuilder:</span></span>

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

<span data-ttu-id="55ce5-171">Effectuez une autre exécution de performances et comparer les performances de hello.</span><span class="sxs-lookup"><span data-stu-id="55ce5-171">Do another performance run, and then compare hello performance.</span></span> <span data-ttu-id="55ce5-172">Dans l’Explorateur de performances de hello, si hello s’exécute est Bonjour même session, vous pouvez simplement sélectionner ces deux rapports, ouvrez le menu contextuel de hello et choisissez **comparer les rapports de performances**.</span><span class="sxs-lookup"><span data-stu-id="55ce5-172">In hello Performance Explorer, if hello runs are in hello same session, you can just select both reports, open hello shortcut menu, and choose **Compare Performance Reports**.</span></span> <span data-ttu-id="55ce5-173">Si vous souhaitez toocompare avec une exécution dans une autre session de performance, ouvrez hello **analyser** menu, puis choisissez **comparer les rapports de performances**.</span><span class="sxs-lookup"><span data-stu-id="55ce5-173">If you want toocompare with a run in another performance session, open hello **Analyze** menu, and choose **Compare Performance Reports**.</span></span> <span data-ttu-id="55ce5-174">Dans la boîte de dialogue hello qui s’affiche, spécifiez les deux fichiers.</span><span class="sxs-lookup"><span data-stu-id="55ce5-174">Specify both files in hello dialog box that appears.</span></span>

![Option Comparer les rapports de performances][15]

<span data-ttu-id="55ce5-176">rapports de Hello mettre en évidence les différences entre deux exécutions de hello.</span><span class="sxs-lookup"><span data-stu-id="55ce5-176">hello reports highlight differences between hello two runs.</span></span>

![Rapport de comparaison][16]

<span data-ttu-id="55ce5-178">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="55ce5-178">Congratulations!</span></span> <span data-ttu-id="55ce5-179">Vous avez obtenu en main du Générateur de profils hello.</span><span class="sxs-lookup"><span data-stu-id="55ce5-179">You've gotten started with hello profiler.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="55ce5-180">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="55ce5-180">Troubleshooting</span></span>
* <span data-ttu-id="55ce5-181">Assurez-vous que le profilage porte bien sur une build Release et exécutez sans débogage.</span><span class="sxs-lookup"><span data-stu-id="55ce5-181">Make sure you are profiling a Release build and start without debugging.</span></span>
* <span data-ttu-id="55ce5-182">Si hello Attacher/Détacher option n’est pas activé sur le menu du Générateur de profils hello, exécutez hello Assistant Performance.</span><span class="sxs-lookup"><span data-stu-id="55ce5-182">If hello Attach/Detach option is not enabled on hello Profiler menu, run hello Performance Wizard.</span></span>
* <span data-ttu-id="55ce5-183">Utilisez hello Compute Emulator UI tooview hello statut de votre application.</span><span class="sxs-lookup"><span data-stu-id="55ce5-183">Use hello Compute Emulator UI tooview hello status of your application.</span></span> 
* <span data-ttu-id="55ce5-184">Si vous rencontrez des problèmes de démarrage des applications dans l’émulateur de hello ou attachement hello du Générateur de profils, arrêtez d’émulateur de calcul hello et redémarrez-le.</span><span class="sxs-lookup"><span data-stu-id="55ce5-184">If you have problems starting applications in hello emulator, or attaching hello profiler, shut down hello compute emulator and restart it.</span></span> <span data-ttu-id="55ce5-185">Si cela ne résout pas le problème de hello, essayez de redémarrer.</span><span class="sxs-lookup"><span data-stu-id="55ce5-185">If that doesn't solve hello problem, try rebooting.</span></span> <span data-ttu-id="55ce5-186">Ce problème peut se produire si vous utilisez toosuspend d’émulateur de calcul hello et supprimez les déploiements en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="55ce5-186">This problem can occur if you use hello Compute Emulator toosuspend and remove running deployments.</span></span>
* <span data-ttu-id="55ce5-187">Si vous avez utilisé des hello profilage des commandes à partir de la ligne de commande, hello en particulier les paramètres globaux, vérifiez que VSPerfClrEnv /globaloff a été appelée et que VsPerfMon.exe a été arrêté.</span><span class="sxs-lookup"><span data-stu-id="55ce5-187">If you have used any of hello profiling commands from the command line, especially hello global settings, make sure that VSPerfClrEnv /globaloff has been called and that VsPerfMon.exe has been shut down.</span></span>
* <span data-ttu-id="55ce5-188">Si lors de l’échantillonnage, vous voyez le message de type hello « PRF0025 : aucune donnée n’a été collectée, « vérifiez que hello processus attaché de toohas processeur activité.</span><span class="sxs-lookup"><span data-stu-id="55ce5-188">If when sampling, you see hello message "PRF0025: No data was collected," check that hello process you attached toohas CPU activity.</span></span> <span data-ttu-id="55ce5-189">Les applications qui n'effectuent pas de calculs peuvent ne pas produire de données d'échantillonnage.</span><span class="sxs-lookup"><span data-stu-id="55ce5-189">Applications that are not doing any computational work might not produce any sampling data.</span></span>  <span data-ttu-id="55ce5-190">Il est également possible que les processus de hello est fermé avant tout échantillonnage a été effectuée.</span><span class="sxs-lookup"><span data-stu-id="55ce5-190">It's also possible that hello process exited before any sampling was done.</span></span> <span data-ttu-id="55ce5-191">Vérifiez toosee méthode Run de hello pour un rôle que vous profilez n’arrête pas.</span><span class="sxs-lookup"><span data-stu-id="55ce5-191">Check toosee that hello Run method for a role that you are profiling does not terminate.</span></span>

## <a name="next-steps"></a><span data-ttu-id="55ce5-192">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="55ce5-192">Next Steps</span></span>
<span data-ttu-id="55ce5-193">L’instrumentation de binaires Azure dans l’émulateur de hello n’est pas pris en charge dans le Générateur de profils Visual Studio hello, mais si vous souhaitez que l’allocation de mémoire tootest, vous pouvez choisir cette option lors du profilage.</span><span class="sxs-lookup"><span data-stu-id="55ce5-193">Instrumenting Azure binaries in hello emulator is not supported in hello Visual Studio profiler, but if you want tootest memory allocation, you can choose that option when profiling.</span></span> <span data-ttu-id="55ce5-194">Vous pouvez également choisir de profilage d’accès concurrentiel, qui vous permet de déterminer si les threads sont gaspiller temps en concurrence pour les verrous, soit au niveau le profilage d’interaction, qui vous permet de détecter les problèmes de performances lors de l’interaction entre les couches d’une application, plus fréquemment entre la couche de données hello et un rôle de travail.</span><span class="sxs-lookup"><span data-stu-id="55ce5-194">You can also choose concurrency profiling, which helps you determine whether threads are wasting time competing for locks, or tier interaction profiling, which helps you track down performance problems when interacting between tiers of an application, most frequently between hello data tier and a worker role.</span></span>  <span data-ttu-id="55ce5-195">Vous pouvez afficher les requêtes de base de données hello que votre application génère et utiliser hello tooimprove de données de profilage de l’utilisation de base de données hello.</span><span class="sxs-lookup"><span data-stu-id="55ce5-195">You can view hello database queries that your app generates and use hello profiling data tooimprove your use of hello database.</span></span> <span data-ttu-id="55ce5-196">Pour plus d’informations sur le profilage d’interaction de couche, voir blog de hello [procédure pas à pas : utilisation de hello profileur d’Interaction de couche dans Visual Studio Team System 2010][3].</span><span class="sxs-lookup"><span data-stu-id="55ce5-196">For information about tier interaction profiling, see hello blog post [Walkthrough: Using hello Tier Interaction Profiler in Visual Studio Team System 2010][3].</span></span>

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
