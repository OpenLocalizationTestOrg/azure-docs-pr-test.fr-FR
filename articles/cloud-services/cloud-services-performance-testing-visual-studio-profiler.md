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
# <a name="testing-hello-performance-of-a-cloud-service-locally-in-hello-azure-compute-emulator-using-hello-visual-studio-profiler"></a>Test hello performances d’un Service Cloud localement Bonjour Azure Compute Emulator à l’aide de hello profileur Visual Studio
Divers outils et techniques sont disponibles pour tester les performances de hello des services de cloud computing.
Lorsque vous publiez un tooAzure de service cloud, vous pouvez avoir Visual Studio collecter les données de profilage et puis les analyser localement, comme décrit dans [profilage d’une Application Azure][1].
Vous pouvez également utiliser tootrack diagnostics des compteurs de performances diverses, comme décrit dans [à l’aide des compteurs de performances dans Azure][2].
Vous pouvez également vous tooprofile votre application localement dans l’émulateur de calcul hello avant de le déployer toohello cloud.

Cet article décrit la méthode d’échantillonnage de l’UC hello de profilage, ce qui peut être effectué localement dans l’émulateur de hello. Cette méthode de profilage est peu intrusive. À un intervalle d’échantillonnage désigné, Générateur de profils hello prend un instantané de pile des appels hello. les données de Hello sont collectées sur une période de temps et affichées dans un rapport. Cette méthode de profilage a tendance à tooindicate où dans une application nécessitant la plupart du travail de hello du processeur est effectuée.  Ceci permet de vous hello toofocus opportunité sur hello « chemin réactif » où votre application passe hello plus de temps.

## <a name="1-configure-visual-studio-for-profiling"></a>1. Configuration de Visual Studio pour le profilage
Tout d'abord, certaines options de configuration de Visual Studio peuvent s'avérer utiles dans le cadre du profilage. décryptage toomake hello des rapports de profilage, vous aurez besoin de symboles (.pdb) pour votre application, ainsi que les symboles pour les bibliothèques système. Vous souhaiterez toomake assurer que vous référencez des serveurs de symboles disponibles hello. toodo cette, hello **outils** menu dans Visual Studio, choisissez **Options**, puis choisissez **débogage**, puis **symboles**. Assurez-vous que Microsoft Symbol Servers figure bien dans **Emplacements du fichier de symboles (.pdb)**.  Vous pouvez également faire référence à http://referencesource.microsoft.com/symbols, qui peut comporter d'autres fichiers de symboles.

![Options de symbole][4]

Si vous le souhaitez, vous pouvez simplifier hello signale ce profileur hello génère en définissant uniquement mon Code. Avec uniquement mon Code est activée, les piles d’appels de fonction sont simplifiées ainsi que les appels toolibraries entièrement interne hello .NET Framework sont masqués à partir de rapports de hello. Sur hello **outils** menu, choisissez **Options**. Puis développez hello **outils de performances** nœud, puis choisissez **général**. Sélectionnez la case à cocher hello **activer uniquement mon Code pour les rapports de profileur**.

![Options Uniquement mon code][17]

Vous pouvez utiliser ces instructions dans un projet existant ou un nouveau projet.  Si vous créez un nouveau Bonjour de tootry projet techniques décrites ci-dessous, choisissez c# **Azure Cloud Service** le projet, puis sélectionnez un **rôle Web** et un **rôle de travail**.

![Rôles de projet Azure Cloud Services][5]

Par exemple, à des fins, ajouter un projet de tooyour de code qui prend beaucoup de temps et présente un problème de performances évidente. Par exemple, ajouter hello suivant du projet de rôle de travail tooa code :

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

Appeler ce code à partir de la méthode RunAsync dans une classe dérivée de RoleEntryPoint du rôle de travail hello de hello. (Ignorer l’avertissement hello sur la méthode hello exécuter de façon synchrone.)

        private async Task RunAsync(CancellationToken cancellationToken)
        {
            // TODO: Replace hello following with your own logic.
            while (!cancellationToken.IsCancellationRequested)
            {
                Trace.TraceInformation("Working");
                Concatenator.Concatenate(10000);
            }
        }

Générer et exécuter votre service cloud localement sans débogage (Ctrl + F5), avec la configuration de la solution hello définie trop**version**. Cela garantit que tous les fichiers et dossiers sont créés pour l’application hello s’exécute et garantit que tous les émulateurs hello sont démarrés. Démarrez hello Compute Emulator UI de tooverify de la barre des tâches de hello votre rôle de travail est en cours d’exécution.

## <a name="2-attach-tooa-process"></a>2 : attacher le processus de tooa
Au lieu de profiler l’application hello en le démarrant à partir de hello IDE de Visual Studio 2010, vous devez joindre tooa de profileur hello processus en cours d’exécution. 

tooattach hello profiler tooa processus sur hello **analyser** menu, choisissez **Profiler** et **Attacher/Détacher**.

![Option Joindre un profil][6]

Pour un rôle de travail, de trouver le processus de WaWorkerHost.exe hello.

![Processus WaWorkerHost][7]

Si votre dossier de projet se trouve sur un lecteur réseau, Générateur de profils hello vous demandera tooprovide hello de toosave un autre emplacement des rapports de profilage.

 Vous pouvez également attacher le rôle web de tooa en attachant tooWaIISHost.exe.
S’il existe plusieurs processus de rôle de travail dans votre application, vous devez toouse hello processID toodistinguish les. Vous pouvez interroger hello processID par programme en accédant à des objets de processus hello. Par exemple, si vous ajoutez cette méthode d’exécution toohello code de classe dérivée de RoleEntryPoint de hello dans un rôle, vous pouvez consulter le journal dans hello Compute Emulator UI tooknow le tooconnect de processus pour.

    var process = System.Diagnostics.Process.GetCurrentProcess();
    var message = String.Format("Process ID: {0}", process.Id);
    Trace.WriteLine(message, "Information");

journal de hello tooview, début hello Compute Emulator UI.

![Démarrer hello Compute Emulator UI][8]

Ouvrez fenêtre de console hello travail rôle journal Bonjour Compute Emulator UI en cliquant sur la barre de titre de la fenêtre de console hello. Vous pouvez voir les ID de processus hello dans le journal de hello.

![Afficher l’ID du processus][9]

Un que vous avez joint, effectuez les opérations de hello dans l’interface utilisateur (si nécessaire) tooreproduce hello scénario de votre application.

Lorsque vous souhaitez toostop de profilage, choisissez hello **arrêter le profilage** lien.

![Option Terminer le profilage][10]

## <a name="3-view-performance-reports"></a>3. Affichage des rapports de performances
rapport de performances Hello pour votre application s’affiche.

À ce stade, Générateur de profils hello arrête l’exécution, enregistre les données dans un fichier .vsp et affiche un rapport qui affiche une analyse de ces données.

![Rapport du profileur][11]

Si vous voyez String.wstrcpy dans hello chemin réactif, cliquez sur uniquement mon Code toochange hello vue tooshow code utilisateur uniquement.  Si vous voyez String.Concat, essayez de cliquer sur Afficher tout Code hello.

Vous devez voir la méthode de concaténation hello et String.Concat occuper une grande partie du temps d’exécution hello.

![Analyse du rapport][12]

Si vous avez ajouté le code de concaténation de chaîne hello dans cet article, vous devez voir un avertissement dans la liste des tâches de hello pour cela. Vous pouvez également voir un avertissement que qu’il existe une quantité excessive de garbage collection, en raison du nombre de toohello de chaînes qui sont créés et supprimés.

![Avertissements liés aux performances][14]

## <a name="4-make-changes-and-compare-performance"></a>4 : Application de modifications et comparaison des performances
Vous pouvez également comparer les performances de hello avant et après une modification du code.  Arrêter le processus en cours d’exécution de hello et modifiez hello code tooreplace hello concaténation de chaînes avec utilisation de hello de StringBuilder :

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

Effectuez une autre exécution de performances et comparer les performances de hello. Dans l’Explorateur de performances de hello, si hello s’exécute est Bonjour même session, vous pouvez simplement sélectionner ces deux rapports, ouvrez le menu contextuel de hello et choisissez **comparer les rapports de performances**. Si vous souhaitez toocompare avec une exécution dans une autre session de performance, ouvrez hello **analyser** menu, puis choisissez **comparer les rapports de performances**. Dans la boîte de dialogue hello qui s’affiche, spécifiez les deux fichiers.

![Option Comparer les rapports de performances][15]

rapports de Hello mettre en évidence les différences entre deux exécutions de hello.

![Rapport de comparaison][16]

Félicitations ! Vous avez obtenu en main du Générateur de profils hello.

## <a name="troubleshooting"></a>Résolution des problèmes
* Assurez-vous que le profilage porte bien sur une build Release et exécutez sans débogage.
* Si hello Attacher/Détacher option n’est pas activé sur le menu du Générateur de profils hello, exécutez hello Assistant Performance.
* Utilisez hello Compute Emulator UI tooview hello statut de votre application. 
* Si vous rencontrez des problèmes de démarrage des applications dans l’émulateur de hello ou attachement hello du Générateur de profils, arrêtez d’émulateur de calcul hello et redémarrez-le. Si cela ne résout pas le problème de hello, essayez de redémarrer. Ce problème peut se produire si vous utilisez toosuspend d’émulateur de calcul hello et supprimez les déploiements en cours d’exécution.
* Si vous avez utilisé des hello profilage des commandes à partir de la ligne de commande, hello en particulier les paramètres globaux, vérifiez que VSPerfClrEnv /globaloff a été appelée et que VsPerfMon.exe a été arrêté.
* Si lors de l’échantillonnage, vous voyez le message de type hello « PRF0025 : aucune donnée n’a été collectée, « vérifiez que hello processus attaché de toohas processeur activité. Les applications qui n'effectuent pas de calculs peuvent ne pas produire de données d'échantillonnage.  Il est également possible que les processus de hello est fermé avant tout échantillonnage a été effectuée. Vérifiez toosee méthode Run de hello pour un rôle que vous profilez n’arrête pas.

## <a name="next-steps"></a>Étapes suivantes
L’instrumentation de binaires Azure dans l’émulateur de hello n’est pas pris en charge dans le Générateur de profils Visual Studio hello, mais si vous souhaitez que l’allocation de mémoire tootest, vous pouvez choisir cette option lors du profilage. Vous pouvez également choisir de profilage d’accès concurrentiel, qui vous permet de déterminer si les threads sont gaspiller temps en concurrence pour les verrous, soit au niveau le profilage d’interaction, qui vous permet de détecter les problèmes de performances lors de l’interaction entre les couches d’une application, plus fréquemment entre la couche de données hello et un rôle de travail.  Vous pouvez afficher les requêtes de base de données hello que votre application génère et utiliser hello tooimprove de données de profilage de l’utilisation de base de données hello. Pour plus d’informations sur le profilage d’interaction de couche, voir blog de hello [procédure pas à pas : utilisation de hello profileur d’Interaction de couche dans Visual Studio Team System 2010][3].

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
